---
title: Een software-update punt configureren voor het gebruik van TLS/SSL met een PKI-certificaat zelf studie
titleSuffix: Configuration Manager
description: Zelf studie-Windows Server Update Services (WSUS)-servers en de software-update punten configureren voor het gebruik van TLS/SSL met een PKI-certificaat.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
ms.openlocfilehash: 4f21af0a5431b5d06f6d96504fa99b52aa43e324
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814461"
---
# <a name="tutorial-configure-a-software-update-point-to-use-tlsssl-with-a-pki-certificate"></a>Zelf studie: een software-update punt configureren voor het gebruik van TLS/SSL met een PKI-certificaat

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het configureren van Windows Server Update Services-servers (WSUS) en de bijbehorende software-update punten (SUP) voor het gebruik van TLS/SSL kan de mogelijkheid van een mogelijke aanvaller om een client op afstand inbreuk maken en bevoegdheden verhogen te verminderen. We raden u ten zeerste aan het TLS/SSL-protocol te gebruiken om de infra structuur voor software-updates te beveiligen, om ervoor te zorgen dat de beste beveiligings protocollen aanwezig zijn. Dit artikel begeleidt u stapsgewijs door de stappen die nodig zijn voor het configureren van elke WSUS-server en het software-update punt voor het gebruik van HTTPS. Zie voor meer informatie over het beveiligen van WSUS het artikel [Secure WSUS with the Secure Sockets Layer Protocol](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) (Engelstalig) in de WSUS-documentatie.

In deze zelfstudie leert u het volgende:
> [!div class="checklist"]
> * Een PKI-certificaat verkrijgen, indien nodig
> * Het certificaat binden aan de WSUS-beheer website
> * De WSUS-webservices configureren zodat SSL is vereist
> * De WSUS-toepassing configureren voor het gebruik van SSL
> * Controleren of de WSUS-console verbinding SSL kan gebruiken
> * Configureer het software-update punt voor het vereisen van SSL-communicatie met de WSUS-server
> * De functionaliteit controleren met Configuration Manager

## <a name="considerations-and-limitations"></a>Overwegingen en beperkingen

WSUS gebruikt TLS/SSL om client computers en downstream-WSUS-servers te verifiëren op de upstream-WSUS-server. WSUS gebruikt ook TLS/SSL om de meta gegevens van de update te versleutelen. WSUS gebruikt geen TLS/SSL voor de inhouds bestanden van een update. De inhouds bestanden worden ondertekend en de hash van het bestand is opgenomen in de meta gegevens van de update. Voordat de bestanden worden gedownload en geïnstalleerd door de client, worden zowel de digitale hand tekening als de hash gecontroleerd. Als een van beide controles mislukt, wordt de update niet geïnstalleerd.

Houd rekening met de volgende beperkingen wanneer u TLS/SSL gebruikt voor het beveiligen van een WSUS-implementatie:

- Met TLS/SSL wordt de werk belasting van de server verhoogd. U moet een klein prestatie verlies verwachten van het versleutelen van alle meta gegevens die via het netwerk worden verzonden.
- Als u WSUS gebruikt met een externe SQL Server-Data Base, wordt de verbinding tussen de WSUS-server en de database server niet beveiligd met TLS/SSL. Als de verbinding met de data base moet worden beveiligd, moet u rekening houden met de volgende aanbevelingen:
   - Verplaats de WSUS-Data Base naar de WSUS-server.
   - Verplaats de externe database server en de WSUS-server naar een particulier netwerk.
   - Implementeer IP-beveiligingsbeleid (IPsec) om netwerkverkeer te helpen beveiligen.

Bij het configureren van WSUS-servers en hun software-update punten voor het gebruik van TLS/SSL, is het raadzaam om de wijzigingen voor grote Configuration Manager-hiërarchieën in te stellen. Als u ervoor kiest om in deze wijzigingen te faseren, begint u onder aan de hiërarchie en gaat u verder met de centrale beheer site.

## <a name="prerequisites"></a>Vereisten

In deze zelf studie wordt de meest voorkomende methode voor het verkrijgen van een certificaat voor gebruik met Internet Information Services (IIS) besproken. Welke methode uw organisatie gebruikt, zorg ervoor dat het certificaat voldoet aan de [PKI-certificaat vereisten](../../core/plan-design/network/pki-certificate-requirements.md) voor een Configuration Manager software-update punt. Net als bij elk certificaat moet de certificerings instantie worden vertrouwd door apparaten die communiceren met de WSUS-server.

- Een WSUS-server waarop de rol software-update punt is geïnstalleerd
- Controleer of u de [Aanbevolen procedures](/troubleshoot/mem/configmgr/windows-server-update-services-best-practices#disable-recycling-and-configure-memory-limits) voor het uitschakelen van recycling en het configureren van geheugen limieten voor WSUS hebt gevolgd voordat u TLS/SSL inschakelt.
- Een van de volgende twee opties:
   - Er komt al een geschikt PKI-certificaat voor in het **persoonlijke** certificaat archief van de WSUS-server.
   - De mogelijkheid om een geschikt PKI-certificaat voor de WSUS-server aan te vragen en te verkrijgen bij de basis certificerings instantie (CA) van uw onderneming.
      - De meeste certificaat sjablonen met inbegrip van het webserver certificaat sjabloon worden standaard alleen verleend aan domein Administrators. Als de aangemelde gebruiker geen domein beheerder is, moet aan het gebruikers account de machtiging **Inschrijven** worden verleend voor het certificaat sjabloon.

## <a name="obtain-the-certificate-from-the-ca-if-needed"></a><a name="bkmk_pki"></a> Het certificaat ophalen van de certificerings instantie, indien nodig

Als u al een geschikt certificaat in het **persoonlijke** certificaat archief van de WSUS-server hebt, kunt u deze sectie overs Laan en beginnen met de sectie [het certificaat binden](#bkmk_bind) . Als u een certificaat aanvraag naar uw interne certificerings instantie wilt verzenden om een nieuw certificaat te installeren, volgt u de instructies in deze sectie.
 
1. Open vanaf de WSUS-server een opdracht prompt voor beheer en voer uit `certlm.msc` . Uw gebruikers account moet een lokale beheerder zijn om certificaten voor de lokale computer te kunnen beheren.

   Het hulp programma certificaat beheer voor het lokale apparaat wordt weer gegeven.

1. Vouw **persoonlijke**uit en klik met de rechter muisknop op **certificaten**.
1. Selecteer **alle taken** en vervolgens **Nieuw certificaat aanvragen**.
1. Kies **volgende** om de certificaat inschrijving te starten.
1. Kies het type certificaat dat u wilt inschrijven. Het doel van het certificaat is **Server verificatie** en het micro soft-certificaat sjabloon dat moet worden gebruikt, is **webserver** of een aangepaste sjabloon waarvoor **Server verificatie** is opgegeven als **uitgebreid sleutel gebruik**. U wordt mogelijk gevraagd om aanvullende informatie over het registreren van het certificaat. Normaal gesp roken geeft u de volgende gegevens op minimale:

   - **Algemene naam:** Op het tabblad **onderwerp** , stelt u de waarde voor de FQDN van de WSUS-server in.
   - **Beschrijvende naam:** Op het tabblad **Algemeen** , stel de waarde in op een beschrijvende naam zodat u het certificaat later kunt identificeren.
   
   :::image type="content" source="media/certificate-properties.png" alt-text="Venster Eigenschappen van certificaat om meer informatie voor inschrijving op te geven":::

1. Selecteer **Inschrijven** en vervolgens **volt ooien** om de registratie te volt ooien.
1. Open het certificaat als u details wilt weer geven, zoals de vinger afdruk van het certificaat.

> [!TIP]
> Als uw WSUS-server Internet gericht is, hebt u de externe FQDN in het onderwerp of de alternatieve naam voor het onderwerp (SAN) in uw certificaat nodig.

## <a name="bind-the-certificate-to-the-wsus-administration-site"></a><a name="bkmk_bind"></a> Het certificaat binden aan de WSUS-beheer site

Zodra u het certificaat in het persoonlijke certificaat archief van de WSUS-server hebt, bindt u dit aan de WSUS-beheer site in IIS.

1. Open IIS-beheer (Internet Information Services) op de WSUS-server.
1. Ga naar **sites**  >  **WSUS-beheer**.
1. Selecteer **bindingen** in het menu actie of klik met de rechter muisknop op de site.
1. Selecteer in het venster **site bindingen** de regel voor **https**en selecteer vervolgens **bewerken...**.

   - Verwijder de HTTP-site binding niet. WSUS gebruikt HTTP voor de update-inhouds bestanden.
   
1. Kies onder de optie **SSL-certificaat** het certificaat dat u wilt verbinden met de WSUS-beheer site. De beschrijvende naam van het certificaat wordt weer gegeven in de vervolg keuzelijst. Als er geen beschrijvende naam is opgegeven, wordt het veld van het certificaat `IssuedTo` weer gegeven. Als u niet zeker weet welk certificaat u moet gebruiken, selecteert u **weer gave** en controleert u of de vinger afdruk overeenkomt met de naam die u hebt verkregen.

   :::image type="content" source="media/edit-site-binding.png" alt-text="Venster site binding bewerken met selectie van SSL-certificaat":::

1. Selecteer **OK** wanneer u klaar bent en **sluit** vervolgens de site bindingen af. Blijf Internet Information Services (IIS) Manager geopend voor de volgende stappen.



## <a name="configure-the-wsus-web-services-to-require-ssl"></a><a name="bkmk_webserv"></a> De WSUS-webservices configureren zodat SSL is vereist

1. Ga in IIS-beheer op de WSUS-server naar **sites**  >  **WSUS-beheer**.
1. Vouw de WSUS-beheer site uit zodat u de lijst met webservices en virtuele mappen voor WSUS ziet.
1. Voor elk van de onderstaande WSUS-webservices:
   - ApiRemoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   Breng de volgende wijzigingen aan:
   
   1. Selecteer **SSL-instellingen**.
   1. Schakel de optie **SSL vereisen** in.
   1. Controleer of de optie voor **client certificaten** is ingesteld op **negeren**.
   1. Selecteer **Toepassen**.

Stel de SSL-instellingen niet in op de WSUS-beheer site op het hoogste niveau omdat bepaalde functies, zoals inhoud, HTTP moeten gebruiken.

## <a name="configure-the-wsus-application-to-use-ssl"></a><a name="bkmk_wsusutil"></a> De WSUS-toepassing configureren voor het gebruik van SSL

Zodra de webservices zijn ingesteld om SSL te vereisen, moet de WSUS-toepassing worden geïnformeerd zodat er een extra configuratie kan worden uitgevoerd om de wijziging te ondersteunen.

1. Open een opdracht prompt met beheerders rechten op de WSUS-server. Het gebruikers account dat deze opdracht uitvoert, moet lid zijn van de groep WSUS-Administrators of de lokale groep Administrators.
1. Wijzig de map in de map hulpprogram ma's voor WSUS:

   `cd "c:\Program Files\Update Services\Tools"`
   
1. Configureer WSUS voor het gebruik van SSL met de volgende opdracht:

    `WsusUtil.exe configuressl server.contoso.com`
   
   Waarbij *server.contoso.com* de FQDN-naam van de WSUS-server is.
   
1. WsusUtil retourneert de URL van de WSUS-server met het poort nummer dat aan het einde is opgegeven. De poort is 8531 (standaard) of 443. Controleer of de geretourneerde URL is wat u verwacht. Als er een fout is opgetreden, kunt u de opdracht opnieuw uitvoeren.

   :::image type="content" source="media/wsusutil.png" alt-text="De wsusutil configuressl opdracht die de HTTPS-URL voor WSUS retourneert":::

> [!TIP] 
> Als uw WSUS-server Internet gericht is, geeft u de externe FQDN op wanneer u uitvoert `WsusUtil.exe configuressl` .

## <a name="verify-the-wsus-console-can-connect-using-ssl"></a><a name="bkmk_wsus_console"></a> Controleren of de WSUS-console verbinding kan maken met SSL

De WSUS-console maakt gebruik van de ApiRemoting30-webservice voor verbinding. De Configuration Manager van het software-update punt (SUP) gebruikt dezelfde webservice voor het direct uitvoeren van WSUS om bepaalde acties uit te voeren, zoals:

- Synchronisatie van software-updates initiëren
- De juiste upstream-server voor WSUS instellen, afhankelijk van waar de site van de SUP zich in uw Configuration Manager-hiërarchie bevindt
- Het toevoegen of verwijderen van producten en classificaties voor synchronisatie vanuit de WSUS-server op het hoogste niveau van de hiërarchie.
- Verlopen updates verwijderen

Open de WSUS-console om te controleren of u een SSL-verbinding met de ApiRemoting30-webservice van de WSUS-server kunt gebruiken. Enkele van de andere webservices worden later getest.

1. Open de WSUS-console en selecteer **actie**  >  **verbinding maken met server**.
1. Voer de FQDN van de WSUS-server in voor de optie **Server naam** .
1. Kies het **poort nummer** dat wordt geretourneerd in de URL van WSUSutil.

1. Het **gebruik Secure Sockets Layer (SSL) voor het maken van een verbinding met deze server** optie wordt automatisch ingeschakeld wanneer 8531 (standaard) of 443 wordt gekozen.

       :::image type="content" source="media/connect-wsus-console.png" alt-text="Connect to the WSUS console over the HTTPS port":::
       
1. Als uw Configuration Manager-site server extern is van het software-update punt, start u de WSUS-console vanaf de site server en controleert u of de WSUS-console verbinding kan maken via SSL.
   - Als de externe WSUS-console geen verbinding kan maken, duidt dit op een probleem met het vertrouwen van het certificaat, de naam omzetting of de poort die wordt geblokkeerd.

## <a name="configure-the-software-update-point-to-require-ssl-communication-to-the-wsus-server"></a><a name="bkmk_cm_sup"></a> Configureer het software-update punt voor het vereisen van SSL-communicatie met de WSUS-server

Zodra WSUS is ingesteld voor het gebruik van TLS/SSL, moet u het bijbehorende Configuration Manager software-update punt bijwerken om te vereisen dat SSL is vereist. Wanneer u deze wijziging aanbrengt, voert Configuration Manager de volgende handelingen uit:

- Controleren of de WSUS-server kan worden geconfigureerd voor het software-update punt
- Direct clients gebruiken de SSL-poort wanneer ze worden geadviseerd om te scannen op deze WSUS-server.

Voer de volgende stappen uit om het software-update punt te configureren voor het vereisen van SSL-communicatie met de WSUS-server: 

1. Open de Configuration Manager-console en maak verbinding met de centrale beheer site of de primaire site server voor het software-update punt dat u wilt bewerken.
1. Ga naar **beheer**  >  **overzicht**  >  **site configuratie**  >  **servers en site systeem rollen**.
1. Selecteer de site systeem server waarop WSUS is geïnstalleerd en selecteer vervolgens de site systeemrol van het software-update punt.
1. Kies **Eigenschappen**in het lint.
1. Schakel de optie **SSL-communicatie vereisen met de WSUS-server** in.

   :::image type="content" source="media/sup-properties.png" alt-text="SUP-eigenschappen met de optie voor het vereisen van SSL-communicatie met de WSUS-server":::
   
1. In het [**bestand WCM. log**](../../core/plan-design/hierarchy/log-files.md#BKMK_SUPLog) voor de site ziet u de volgende vermeldingen wanneer u de wijziging toepast:

   ```
   SCF change notification triggered.
   Populating config from SCF
   Setting new configuration state to 1 (WSUS_CONFIG_PENDING)
   ...
   Attempting connection to local WSUS server
   Successfully connected to local WSUS server
   ...
   Setting new configuration state to 2 (WSUS_CONFIG_SUCCESS)
   ```

Voor beelden van logboek bestanden zijn bewerkt voor het verwijderen van overbodige gegevens voor dit scenario.  

## <a name="verify-functionality-with-configuration-manager"></a><a name="bkmk_cm_verify"></a> De functionaliteit controleren met Configuration Manager

### <a name="verify-the-site-server-can-sync-updates"></a>Controleren of de site server updates kan synchroniseren

1. Verbind de Configuration Manager-console met de site op het hoogste niveau.
1. Ga naar **software bibliotheek**  >  **overzicht**  >  **software-updates**  >  **alle software-updates**.
1. Selecteer op het lint de optie **software-updates synchroniseren**.
1. Selecteer **Ja** in het bericht waarin u wordt gevraagd of u een synchronisatie voor de gehele site wilt initiëren voor software-updates.

   - Sinds de WSUS-configuratie is gewijzigd, treedt er een volledige synchronisatie van software-updates op in plaats van een Delta synchronisatie.
   
1. Open **bestand Wsyncmgr. log** voor de site. Als u een onderliggende site bewaken, moet u wachten tot de bovenliggende site de synchronisatie eerst voltooit. Controleer of de server is gesynchroniseerd door het logboek te controleren op items die vergelijkbaar zijn met het volgende:

   ```
   Starting Sync
   ...
   Full sync required due to changes in main WSUS server location.
   ...
   Found active SUP SERVER.CONTOSO.COM from SCF File.
   ...
   https://SERVER.CONTOSO.COM:8531
   ...
   Done synchronizing WSUS Server SERVER.CONTOSO.COM
   ...
   sync: Starting SMS database synchronization
   ...
   Done synchronizing SMS with WSUS Server SERVER.CONTOSO.COM
   ```

### <a name="verify-a-client-can-scan-for-updates"></a>Controleren of een client kan scannen op updates

Wanneer u het software-update punt wijzigt zodat SSL is vereist, ontvangen Configuration Manager-clients de bijgewerkte WSUS-URL wanneer een locatie aanvraag voor een software-update punt wordt gemaakt. Door een client te testen, kunnen we het volgende doen:
-  Bepaal of de client het certificaat van de WSUS-server vertrouwt. 
- Als de SimpleAuthWebService en de ClientWebService voor WSUS functioneel zijn.
-  Of de virtuele map van WSUS-inhoud functioneel is, als de client heeft plaatsgevonden om een gebruiksrecht overeenkomst op te halen tijdens de scan

1. Identificeer een client die scant op het software-update punt dat recent is gewijzigd voor het gebruik van TLS/SSL. Gebruik [scripts uitvoeren](../..//apps/deploy-use/create-deploy-scripts.md) met het onderstaande Power shell-script als u hulp nodig hebt bij het identificeren van een client:

   ```powershell
   $Last = (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").LastSuccessScanPath
   $Current= Write-Output (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").CurrentScanPath
   Write-Host "LastGoodSUP- $last"
   Write-Host "CurrentSUP- $current"
   ```

1. Voer een scan cyclus voor software-updates op de test client uit. U kunt een scan afdwingen met het volgende Power shell-script:

   ```powershell
   Invoke-WMIMethod -Namespace root\ccm -Class SMS_CLIENT -Name TriggerSchedule "{00000000-0000-0000-0000-000000000113}"
   ```

1. Controleer de **ScanAgent. log** van de client om te controleren of het bericht dat u wilt scannen op het software-update punt is ontvangen.

   ```
   Message received: '<?xml version='1.0' ?>
   <UpdateSourceMessage MessageType='ScanByUpdateSource'>
      <ForceScan>TRUE</ForceScan>
      <UpdateSourceIDs>
            <ID>{A1B2C3D4-1234-1234-A1B2-A1B2C3D41234}</ID>
      </UpdateSourceIDs>
    </UpdateSourceMessage>'
   ```

1. Controleer **bestand locationservices. log** om te controleren of de client de juiste WSUS-URL ziet.
**LocationServices.log**

   ```
   WSUSLocationReply : <WSUSLocationReply SchemaVersion="1
   ...
   <LocationRecord WSUSURL="https://SERVER.CONTOSO.COM:8531" ServerName="SERVER.CONTOSO.COM"
   ...
   </WSUSLocationReply>
   ```

1. Controleer de **WUAHandler. log** om te controleren of de client kan scannen.

   ```
   Enabling WUA Managed server policy to use server: https://SERVER.CONTOSO.COM:8531
   ...
   Successfully completed scan.
   ```

## <a name="next-steps"></a>Volgende stappen

[Software-updates implementeren](../deploy-use/deploy-software-updates.md)
