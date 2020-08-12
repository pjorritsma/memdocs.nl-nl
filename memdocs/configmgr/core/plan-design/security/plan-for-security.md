---
title: De beveiliging plannen
titleSuffix: Configuration Manager
description: Aanbevolen procedures en andere informatie over beveiliging in Configuration Manager ophalen.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6fa5ebf25de0f695661b18c4379c080dad42cf08
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128491"
---
# <a name="plan-for-security-in-configuration-manager"></a>Beveiliging plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel worden de concepten beschreven waarmee u rekening moet houden bij het plannen van beveiliging met uw Configuration Manager-implementatie. De sectie bevat de volgende secties:  

- [Certificaten plannen (zelf ondertekend en PKI)](#BKMK_PlanningForCertificates)  
  - [Crypto grafie: Next Generation (CNG)-certificaten](#bkmk_plan-cng)  
  - [Verbeterde HTTP](#bkmk_plan-ehttp)  
  - [Certificaten voor CMG en CDP](#bkmk_plan-cmgcdp)  
  - [Het handtekening certificaat van de site server (zelfondertekend)](#bkmk_plansitesign)  
  - [Intrekken van PKI-certificaten](#BKMK_PlanningForCRLs)  
  - [De vertrouwde PKI-basis certificaten en de certificaat verleners](#BKMK_PlanningForRootCAs)  
  - [PKI-client certificaat selecteren](#BKMK_PlanningForClientCertificateSelection)  
  - [Een overgangs strategie voor PKI-certificaten en client beheer op Internet](#BKMK_PlanningForPKITransition)  

- [Plan voor de vertrouwde basis sleutel](#BKMK_PlanningForRTK)  

- [Plan voor ondertekening en versleuteling](#BKMK_PlanningForSigningEncryption)  

- [Plannen voor op rollen gebaseerd beheer](#BKMK_PlanningForRBA)  

- [Azure Active Directory plannen](#bkmk_planazuread)  

- [Verificatie van de SMS-provider plannen](#bkmk_auth)



##  <a name="plan-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a>Certificaten plannen (zelf ondertekend en PKI)  

Configuration Manager gebruikt een combi natie van zelfondertekende certificaten en PKI-certificaten (Public Key Infrastructure).  

Gebruik waar mogelijk PKI-certificaten. Zie [PKI-certificaat vereisten](../network/pki-certificate-requirements.md)voor meer informatie. Wanneer Configuration Manager PKI-certificaten aanvraagt tijdens de inschrijving voor mobiele apparaten, moet u Active Directory Domain Services en een bedrijfs certificerings instantie gebruiken. Voor alle andere PKI-certificaten moet u ze onafhankelijk van Configuration Manager implementeren en beheren. 

PKI-certificaten zijn vereist wanneer client computers verbinding maken met site systemen op internet. Voor sommige scenario's met de Cloud beheer gateway en het Cloud distributiepunt zijn ook PKI-certificaten vereist. Zie [clients op Internet beheren](../../clients/manage/manage-clients-internet.md)voor meer informatie.

Wanneer u een PKI gebruikt, kunt u ook IPsec gebruiken om de server-naar-server-communicatie tussen site systemen in een site, tussen sites en andere gegevens overdracht tussen computers te beveiligen. De implementatie van IPsec is onafhankelijk van Configuration Manager.  

Als er geen PKI-certificaten beschikbaar zijn, genereert Configuration Manager automatisch zelfondertekende certificaten. Sommige certificaten in Configuration Manager zijn altijd zelfondertekend. In de meeste gevallen beheert Configuration Manager automatisch de zelfondertekende certificaten en hoeft u geen verdere actie te ondernemen. Een voor beeld is het handtekening certificaat van de site server. Dit certificaat is altijd zelfondertekend. Het zorgt ervoor dat de beleids regels die clients downloaden van het beheer punt zijn verzonden vanaf de site server en niet zijn gemanipuleerd.  


### <a name="cryptography-next-generation-cng-certificates"></a><a name="bkmk_plan-cng"></a>Crypto grafie: Next Generation (CNG)-certificaten  

Configuration Manager ondersteunt crypto grafie: Next Generation (CNG)-certificaten. Configuration Manager-clients kunnen een PKI-certificaat voor client verificatie gebruiken met een persoonlijke sleutel in de SLEUTELARCHIEFPROVIDER. Met de SLEUTELARCHIEFPROVIDER-ondersteuning ondersteunen Configuration Manager-clients op hardware gebaseerde persoonlijke sleutel, zoals TPM-SLEUTELARCHIEFPROVIDER voor PKI-client verificatie certificaten. Zie voor meer informatie [overzicht CNG-certificaten](../network/cng-certificates-overview.md).


### <a name="enhanced-http"></a><a name="bkmk_plan-ehttp"></a>Verbeterde HTTP  

Het gebruik van HTTPS-communicatie wordt aanbevolen voor alle Configuration Manager communicatie paden, maar is lastig voor sommige klanten vanwege de overhead van het beheer van PKI-certificaten. De introductie van de integratie van Azure Active Directory (Azure AD) vermindert enkele, maar niet alle certificaat vereisten. Vanaf versie 1806 kunt u de site inschakelen voor het gebruik van **verbeterde http**. Deze configuratie ondersteunt HTTPS op site systemen door gebruik te maken van een combi natie van zelfondertekende certificaten en Azure AD. Hiervoor is geen PKI vereist. Zie [Enhanced http](../hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie.  


### <a name="certificates-for-cmg-and-cdp"></a><a name="bkmk_plan-cmgcdp"></a>Certificaten voor CMG en CDP

Het gebruik van certificaten is vereist voor het beheren van clients op Internet via de Cloud beheer gateway (CMG) en het Cloud distributiepunt (CDP). Het aantal en het type certificaten variëren afhankelijk van uw specifieke scenario's. Raadpleeg voor meer informatie de volgende artikelen:
- [Certificaten voor de Cloud beheer gateway](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)  
- [Certificaten voor het Cloud distributiepunt](../hierarchy/use-a-cloud-based-distribution-point.md#bkmk_certs)  


### <a name="plan-for-the-site-server-signing-certificate-self-signed"></a><a name="bkmk_plansitesign"></a>Het handtekening certificaat van de site server (zelf-ondertekend) plannen  

Clients kunnen veilig een kopie van het handtekening certificaat van de site server verkrijgen van Active Directory Domain Services en van client push installatie. Als clients geen kopie van dit certificaat kunnen verkrijgen met een van deze mechanismen, installeert u dit wanneer u de-client installeert. Dit proces is vooral belang rijk als de eerste communicatie van de client met de site een beheer punt op internet is. Omdat deze server is verbonden met een niet-vertrouwd netwerk, is dit kwetsbaar voor aanvallen. Als u deze extra stap niet uitvoert, downloaden clients automatisch een kopie van het handtekening certificaat van de site server van het beheer punt.  

Clients kunnen niet veilig een kopie van het certificaat van de site server ophalen in de volgende scenario's:  

- U installeert de client niet met behulp van client-push en:  

  - U hebt het Active Directory schema voor Configuration Manager niet uitgebreid.  

  - U hebt de site van de client niet gepubliceerd op Active Directory Domain Services.  

  - De client is van een niet-vertrouwde forest of een werkgroep.  

- U gebruikt client beheer op internet en u installeert de-client wanneer deze op internet is.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Installeren van clients met een kopie van het handtekeningcertificaat van de siteserver  

1.  Zoek het handtekening certificaat van de site server op de primaire site server. Het certificaat wordt opgeslagen in het **SMS** -certificaat archief van Windows. Het heeft de object naam **Site Server** en de beschrijvende naam, het **handtekening certificaat van de site server**.  

2.  Exporteer het certificaat zonder de persoonlijke sleutel, sla het bestand veilig op en open het alleen vanuit een beveiligd kanaal.  

3.  Installeer de client met behulp van de volgende client.msi eigenschap:`SMSSIGNCERT=<full path and file name>`  


###  <a name="plan-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a>Het intrekken van het PKI-certificaat plannen  

Wanneer u PKI-certificaten gebruikt met Configuration Manager, kunt u het gebruik van een certificaatintrekkingslijst (CRL) plannen. Apparaten gebruiken de CRL om het certificaat op de verbinding computer te verifiëren. De CRL is een bestand dat door een certificerings instantie (CA) wordt gemaakt en ondertekend. Het bevat een lijst met certificaten die de CA heeft uitgegeven, maar ingetrokken. Wanneer een certificaat beheerder certificaten intrekt, wordt de vinger afdruk toegevoegd aan de CRL. Als een uitgegeven certificaat bijvoorbeeld bekend is of wordt vermoed dat het is aangetast.

> [!IMPORTANT]  
> Omdat de locatie van de CRL wordt toegevoegd aan een certificaat wanneer een certificerings instantie dit uitgeeft, moet u ervoor zorgen dat u de CRL plant voordat u PKI-certificaten implementeert die Configuration Manager gebruiken.  

IIS controleert de CRL altijd voor client certificaten en u kunt deze configuratie niet wijzigen in Configuration Manager. Configuration Manager-clients controleren standaard altijd de CRL voor site systemen. Schakel deze instelling uit door een site-eigenschap op te geven en door een CCMSetup-eigenschap op te geven.  

Computers die gebruikmaken van de controle op ingetrokken certificaten, maar de CRL niet kunnen vinden alsof alle certificaten in de certificerings keten zijn ingetrokken. Dit probleem wordt veroorzaakt door het feit dat ze niet kunnen controleren of de certificaten in de lijst met certificaatintrekkingslijsten staan. In dit scenario mislukken alle verbindingen waarvoor certificaten zijn vereist en moet de CRL-controle worden toegevoegd. Wanneer u valideert dat de CRL toegankelijk is door naar de HTTP-locatie te bladeren, is het belang rijk te weten dat de Configuration Manager-client wordt uitgevoerd als lokaal systeem. Daarom kan het testen van de CRL-toegankelijkheid met een webbrowser die wordt uitgevoerd onder gebruikers context slagen, maar het computer account kan echter worden geblokkeerd bij het maken van een http-verbinding met dezelfde CRL-URL vanwege de interne oplossing voor webfiltering. White List de URL van de CRL in een oplossing voor webfiltering mogelijk nodig is in deze situatie.

Het controleren van de CRL telkens wanneer een certificaat wordt gebruikt, biedt meer beveiliging tegen het gebruik van een certificaat dat is ingetrokken. Hoewel er sprake is van een vertraging van de verbinding en extra verwerking op de client. Uw organisatie vereist mogelijk deze aanvullende beveiligings controle voor clients op internet of een niet-vertrouwd netwerk.  

Neem contact op met uw PKI-beheerders voordat u besluit of Configuration Manager-clients de CRL moeten controleren. Houd deze optie vervolgens ingeschakeld in Configuration Manager als aan beide volgende voor waarden wordt voldaan:  

- Uw PKI-infra structuur ondersteunt een CRL en deze wordt gepubliceerd waar alle Configuration Manager-clients deze kunnen vinden. Deze clients kunnen apparaten op het internet bevatten en zich in niet-vertrouwde forests.  

- De vereiste om de CRL te controleren voor elke verbinding met een site systeem dat is geconfigureerd voor het gebruik van een PKI-certificaat is groter dan de volgende vereisten:  
  - Snellere verbindingen  
  - Efficiënte verwerking op de client  
  - Het risico van clients die geen verbinding kunnen maken met servers als de CRL niet kan worden gevonden  


###  <a name="plan-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a>Plan voor de vertrouwde PKI-basis certificaten en de lijst met certificaat verleners  

Als uw IIS-site systemen PKI-client certificaten gebruiken voor client verificatie via HTTP of voor client verificatie en versleuteling over HTTPS, moet u mogelijk basis-CA-certificaten importeren als een site-eigenschap. Dit zijn de twee scenario's:  

- U implementeert besturings systemen met behulp van Configuration Manager en de beheer punten accepteren alleen HTTPS-client verbindingen.  

- U kunt PKI-client certificaten gebruiken die niet zijn gekoppeld aan een basis certificaat dat door de beheer punten wordt vertrouwd.  

  > [!NOTE]  
  > Wanneer u client-PKI-certificaten uitgeeft van dezelfde CA-hiërarchie die de server certificaten uitgeeft die u gebruikt voor beheer punten, hoeft u dit basis-CA-certificaat niet op te geven. Als u echter meerdere CA-hiërarchieën gebruikt en u niet zeker weet of ze elkaar vertrouwen, importeert u de basis certificerings instantie voor de CA-hiërarchie van de clients.  

Als u basis-CA-certificaten voor Configuration Manager moet importeren, exporteert u ze van de verlenende CA of van de client computer. Als u het certificaat exporteert van de verlenende CA die ook de basis-CA is, moet u ervoor zorgen dat u de persoonlijke sleutel niet exporteert. Sla het geëxporteerde certificaat bestand op een veilige locatie op om manipulatie te voor komen. U hebt toegang tot het bestand nodig bij het instellen van de site. Als u het bestand via het netwerk opent, moet u ervoor zorgen dat de communicatie beveiligd is tegen knoeien met behulp van IPsec.  

Als een door u geïmporteerd basis-CA-certificaat wordt verlengd, moet u het verlengde certificaat importeren.  

Deze geïmporteerde basis-CA-certificaten en het basis-CA-certificaat van elk beheer punt maken de lijst met certificaat verleners die Configuration Manager computers op de volgende manieren gebruiken:  

- Wanneer clients verbinding maken met beheer punten, controleert het beheer punt of het client certificaat wordt gekoppeld aan een vertrouwd basis certificaat in de lijst met certificaat verleners van de site. Als dat niet het geval is, wordt het certificaat geweigerd en mislukt de PKI-verbinding.  

- Wanneer clients een PKI-certificaat selecteren en een lijst met certificaat verleners hebben, selecteren ze een certificaat dat is gekoppeld aan een vertrouwd basis certificaat in de lijst met certificaat verleners. Als er geen overeenkomst is, selecteert de client geen PKI-certificaat. Zie voor meer informatie [plannen voor het selecteren van PKI-client certificaten](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="plan-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a>De selectie van het PKI-client certificaat plannen  

Als uw IIS-site systemen PKI-client certificaten gebruiken voor client verificatie via HTTP of voor client verificatie en versleuteling over HTTPS, plan dan hoe Windows-clients het certificaat selecteren dat moet worden gebruikt voor Configuration Manager.  

> [!NOTE]  
> Sommige apparaten bieden geen ondersteuning voor een methode voor het selecteren van certificaten. In plaats daarvan selecteren ze automatisch het eerste certificaat dat voldoet aan de certificaat vereisten. Clients op Mac-computers en mobiele apparaten ondersteunen bijvoorbeeld geen methode voor het selecteren van certificaten.  

In veel gevallen zijn de standaard configuratie en-gedrag voldoende. De Configuration Manager-client op Windows-computers filtert meerdere certificaten met behulp van deze criteria in deze volg orde:  

1.  De lijst met certificaat verleners: het certificaat is gekoppeld aan een basis-CA die wordt vertrouwd door het beheer punt.  

2.  Het certificaat bevindt zich in het standaardcertificaatarchief **Persoonlijk**.  

3.  Het certificaat is geldig, is niet ingetrokken en niet verlopen. De geldigheids controle controleert ook of de persoonlijke sleutel toegankelijk is.  

4.  Het certificaat heeft een mogelijkheid voor client verificatie.

5.  De onderwerpnaam van het certificaat bevat de naam van de lokale computer als een subtekenreeks.  

6.  Het certificaat heeft de langste geldigheidsduur.  

Clients configureren voor het gebruik van de lijst met certificaat verleners met behulp van de volgende mechanismen:  

- Publiceer het met Configuration Manager site-informatie naar Active Directory Domain Services.  

- Clients installeren met behulp van client push.  

- Clients downloaden deze van het beheer punt nadat ze zijn toegewezen aan hun site.  

- Geef deze tijdens de client installatie op als een CCMSetup client.msi-eigenschap van CCMCERTISSUERS.  

Clients die geen lijst met certificaat verleners hebben wanneer ze voor het eerst worden geïnstalleerd en nog niet zijn toegewezen aan de site, slaan deze controle over. Als clients de lijst met certificaat verleners hebben en geen PKI-certificaat hebben dat is gekoppeld aan een vertrouwd basis certificaat in de lijst met certificaat verleners, mislukt de certificaat selectie. Clients blijven niet verder met de selectie criteria van het certificaat.  

In de meeste gevallen identificeert de Configuration Manager-client een uniek en geschikt PKI-certificaat correct. Als dit gedrag echter niet het geval is, kunt u twee alternatieve selectie methoden instellen, in plaats van het certificaat te selecteren op basis van de mogelijkheid voor client verificatie:  

- Een gedeeltelijke teken reeks die overeenkomt met de onderwerpnaam van het client certificaat. Deze methode is hoofdletter gevoelig. Het is geschikt als u de Fully Qualified Domain Name (FQDN) van een computer gebruikt in het onderwerpveld en de certificaat selectie wilt baseren op het domein achtervoegsel, bijvoorbeeld **contoso.com**. U kunt deze selectie methode echter gebruiken om een reeks opeenvolgende tekens te identificeren in de onderwerpnaam van het certificaat die het certificaat onderscheidt van andere in het certificaat archief van de client.  

  > [!NOTE]
  > U kunt de gedeeltelijke teken reeks overeenkomst met de alternatieve naam voor het onderwerp (SAN) niet gebruiken als een site-instelling. Hoewel u een gedeeltelijke teken reeks overeenkomst kunt opgeven voor de SAN door gebruik te maken van CCMSetup, wordt deze in de volgende scenario's overschreven door de site-eigenschappen:  
  > 
  > - Clients halen site-informatie op die is gepubliceerd in Active Directory Domain Services.  
  >   - Clients worden met behulp van clientpushinstallatie geïnstalleerd.  
  > 
  >   Gebruik een gedeeltelijke teken reeks overeenkomst in de SAN alleen wanneer u clients hand matig installeert en wanneer ze geen site-informatie ophalen van Active Directory Domain Services. Deze voor waarden zijn bijvoorbeeld van toepassing op clients met alleen Internet verbinding.  

- Een overeenkomst op de kenmerk waarden van de onderwerpnaam van het client certificaat of de kenmerk waarden van de alternatieve naam voor het onderwerp (SAN). Deze methode is een hoofdletter gevoelige overeenkomst. Het is geschikt als u een DN-naam (een x500 Distinguished Name) of gelijkwaardige object-id's (Oid's) gebruikt in overeenstemming met RFC 3280 en u wilt dat de certificaat selectie wordt gebaseerd op de kenmerk waarden. U kunt alleen de kenmerken en hun waarden opgeven die u nodig hebt om het certificaat uniek te identificeren of valideren en het certificaat te onderscheiden van andere in het certificaatarchief.  

De volgende tabel bevat de kenmerk waarden die Configuration Manager ondersteunt voor de selectie criteria van het client certificaat.  

|OID-kenmerk|DN-naamkenmerk|Kenmerkdefinitie|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domeinonderdeel|  
|1.2.840.113549.1.9.1|E of e-mailbericht|E-mailadres|  
|2.5.4.3|CN|Algemene naam|  
|2.5.4.4|SN|Onderwerpnaam|  
|2.5.4.5|SERIENUMMER|Serienummer|  
|2.5.4.6|C|Landcode|  
|2.5.4.7|L|Lokaliteit|  
|2.5.4.8|S of ST|Naam van staat of provincie|  
|2.5.4.9|STRAAT|Adres|  
|2.5.4.10|O|Organisatienaam|  
|2.5.4.11|ORGANISATIE-EENHEID|Organisatie-eenheid|  
|2.5.4.12|T of titel|Titel|  
|2.5.4.42|G of GN of voornaam|Voornaam|  
|2.5.4.43|I of initialen|Initialen|  
|2.5.29.17|(geen waarde)|Alternatieve onderwerpnaam| 

  > [!NOTE]
  > Als u een van de bovenstaande alternatieve certificaat selectie methoden configureert, hoeft de onderwerpnaam van het certificaat de naam van de lokale computer niet te bevatten.

Als er meer dan één geschikt certificaat zich bevindt nadat de selectie criteria zijn toegepast, kunt u de standaard configuratie onderdrukken om het certificaat te selecteren dat de langste geldigheids periode heeft en in plaats daarvan opgeven dat er geen certificaat is geselecteerd. In dit scenario kan de client niet communiceren met IIS-site systemen met een PKI-certificaat. De client stuurt een fout bericht naar het toegewezen terugval status punt om u te waarschuwen over het mislukken van de certificaat selectie zodat u de selectie criteria voor certificaten kunt wijzigen of verfijnen. Het clientgedrag is dan afhankelijk van of de mislukte verbinding zich voordeed via HTTPS of HTTP:  

- Als de mislukte verbinding zich voordoet via HTTPS: de client probeert verbinding te maken via HTTP en maakt gebruik van het zelfondertekende certificaat van de client.  

- Als de mislukte verbinding via HTTP: de client probeert opnieuw verbinding te maken via HTTP met behulp van het zelfondertekende client certificaat.  

U kunt een uniek PKI-client certificaat helpen identificeren door ook een aangepast archief op te geven dan de standaard instelling **persoonlijk** in het archief van de **computer** . U moet dit archief echter onafhankelijk van Configuration Manager maken. U moet certificaten kunnen implementeren op deze aangepaste opslag en deze vernieuwen voordat de geldigheids periode verloopt.  

Zie [instellingen voor client-PKI-certificaten configureren](configure-security.md#BKMK_ConfigureClientPKI)voor meer informatie.  


###  <a name="plan-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a>Een overgangs strategie plannen voor PKI-certificaten en client beheer op Internet  

Met de flexibele configuratie opties in Configuration Manager kunt u clients en de site geleidelijk laten overstappen om PKI-certificaten te gebruiken om client eindpunten te helpen beveiligen. PKI-certificaten bieden betere beveiliging en stellen u in staat om internetclients te beheren.  

Vanwege het aantal configuratie opties en-opties in Configuration Manager is er geen enkele manier om een site over te zetten, zodat alle clients HTTPS-verbindingen gebruiken. U kunt echter deze stappen volgen als richtlijn:  

1. Installeer de Configuration Manager-site en configureer deze zodat site systemen client verbindingen via HTTPS en HTTP accepteren.  

2. Configureer het tabblad **communicatie client computer** in de site-eigenschappen zodat de **site systeem instellingen zijn ingesteld** op **http of https**, en selecteer vervolgens **PKI-client certificaat gebruiken (verificatie mogelijkheid voor client) indien beschikbaar**.  Zie [instellingen voor client-PKI-certificaten configureren](configure-security.md#BKMK_ConfigureClientPKI)voor meer informatie.  

    > [!Note]
    > Vanaf versie 1906 wordt dit tabblad **communicatie beveiliging**genoemd.<!-- SCCMDocs#1645 -->  

3. Proef uitvoeren van een PKI-rollout voor clientcertificaten. Zie [het client certificaat voor Windows-computers implementeren](../network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)voor een voorbeeld implementatie.  

4. Clients met behulp van de clientpushinstallatiemethode installeren. Zie voor meer informatie de [installatie van Configuration Manager-clients met behulp van client push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

5. Bewaak client implementatie en-status met behulp van de rapporten en informatie in de Configuration Manager-console.  

6. Volg hoeveel clients een PKI-clientcertificaat gebruiken in de kolom **Clientcertificaat** in de werkruimte **Activa en naleving** en het knooppunt **Apparaten** .  

    U kunt ook het Configuration Manager HTTPS Readiness Assessment Tool (**cmHttpsReadiness.exe**) implementeren op computers. Gebruik vervolgens de rapporten om te zien hoeveel computers een PKI-client certificaat kunnen gebruiken met Configuration Manager.  

   > [!NOTE]
   >  Wanneer u de Configuration Manager-client installeert, wordt het **CMHttpsReadiness.exe** -hulp programma geïnstalleerd in de `%windir%\CCM` map. De volgende opdracht regel opties zijn beschikbaar wanneer u dit hulp programma uitvoert:  
   > 
   > - `/Store:<name>`: Deze optie is hetzelfde als de eigenschap **CCMCERTSTORE** client.msi  
   > - `/Issuers:<list>`: Deze optie is hetzelfde als de eigenschap **CCMCERTISSUERS** client.msi    
   > - `/Criteria:<criteria>`: Deze optie is hetzelfde als de eigenschap **CCMCERTSEL** client.msi    
   > - `/SelectFirstCert`: Deze optie is hetzelfde als de eigenschap **CCMFIRSTCERT** client.msi    
   > 
   >   Zie [over eigenschappen van client installatie](../../clients/deploy/about-client-installation-properties.md)voor meer informatie.  

7. Voer de volgende stappen uit als u zeker weet dat voldoende clients hun PKI-client certificaat gebruiken voor verificatie via HTTP:  

   1.  Implementeer een PKI-webserver certificaat op een lidserver waarop een extra beheer punt voor de site wordt uitgevoerd, en configureer dat certificaat in IIS. Zie [het webserver certificaat implementeren voor site systemen die IIS uitvoeren](../network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)voor meer informatie.  

   2.  Installeer de beheerpuntrol op deze server en configureer de optie **Clientverbindingen** in de beheerpunteigenschappen voor **HTTPS**  

8. Controleer en verifieer of clients die een PKI-certificaat hebben het nieuwe beheerpunt via HTTPS gebruiken. U kunt de IIS-logboek registratie of prestatie meter items gebruiken om te controleren.  

9. Configureer andere sitesysteemrollen opnieuw voor het gebruik van HTTPS-clientverbindingen. Als u clients op internet wilt beheren, moet u ervoor zorgen dat site systemen een Internet-FQDN hebben. Configureer afzonderlijke beheer punten en distributie punten om client verbindingen van het Internet te accepteren.  

    > [!IMPORTANT]  
    > Voordat u site systeem rollen instelt om verbindingen van het Internet te accepteren, raadpleegt u de plannings informatie en vereisten voor client beheer op internet. Zie [communicatie tussen eind punten](../hierarchy/communications-between-endpoints.md)voor meer informatie.  

10. Breid de implementatie van het PKI-certificaat uit voor clients en voor site systemen die IIS uitvoeren. Stel de site systeem rollen voor HTTPS-client verbindingen en Internet verbindingen, indien nodig, in.  

11. Voor de hoogste beveiliging: als u zeker weet dat alle clients een PKI-client certificaat gebruiken voor verificatie en versleuteling, wijzigt u de site-eigenschappen zodanig dat ze alleen HTTPS gebruiken.  

    Dit plan introduceert eerst PKI-certificaten voor verificatie via HTTP en vervolgens voor verificatie en versleuteling via HTTPS. Wanneer u dit plan volgt om deze certificaten geleidelijk te introduceren, verkleint u het risico dat clients niet meer worden beheerd. U profiteert ook van de hoogste beveiliging die Configuration Manager ondersteunt.  

##  <a name="plan-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a>Plan voor de vertrouwde basis sleutel  

De Configuration Manager vertrouwde basis sleutel biedt een mechanisme voor Configuration Manager-clients om te controleren of site systemen deel uitmaken van hun hiërarchie. Elke siteserver genereert een uitwisselingssleutel om te communiceren met andere sites. De uitwisselingssleutel van de site op het hoogste niveau in de hiërarchie wordt de vertrouwde basissleutel genoemd.  

De functie van de vertrouwde basis sleutel in Configuration Manager lijkt op een basis certificaat in een open bare-sleutel infrastructuur. Alles wat is ondertekend door de persoonlijke sleutel van de vertrouwde basis sleutel wordt vertrouwd in de hiërarchie. Clients slaan een kopie op van de vertrouwde basis sleutel van de site in de WMI-naam ruimte **root\ccm\locationservices** . 

De site verzendt bijvoorbeeld een certificaat naar het beheer punt, dat het ondertekent met de persoonlijke sleutel van de vertrouwde basis sleutel. De site deelt met clients de open bare sleutel van de vertrouwde basis sleutel. Vervolgens kunnen clients onderscheid maken tussen beheer punten in hun hiërarchie en beheer punten die zich niet in hun hiërarchie bevinden.   

Clients halen automatisch de open bare kopie van de vertrouwde basis sleutel op met behulp van twee mechanismen:  

- U breidt het Active Directory schema voor Configuration Manager uit en publiceert de site naar Active Directory Domain Services. Vervolgens haalt clients deze site-informatie op uit een globale catalogus server. Zie [Active Directory voorbereiden voor het publiceren van sites](../network/extend-the-active-directory-schema.md)voor meer informatie.  

- Wanneer u clients installeert met behulp van de Push-client installatie methode. Zie [client push Installation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)(Engelstalig) voor meer informatie.  

Als clients de vertrouwde basis sleutel niet kunnen ophalen met behulp van een van deze mechanismen, vertrouwen ze de vertrouwde basis sleutel die wordt verstrekt door het eerste beheer punt waarmee ze communiceren. In dit scenario kan een client mogelijk niet worden omgeleid naar een beheer punt van een aanvaller, waar het beleid van het Rogue-beheer punt zou ontvangen. Voor deze actie is een geavanceerde aanvaller vereist. Deze aanval is beperkt tot de korte periode voordat de client de vertrouwde basis sleutel ophaalt van een geldig beheer punt. Om het risico te verkleinen dat een aanvaller clients naar een Rogue-beheer punt omleidt, moet u de clients vooraf inrichten met de vertrouwde basis sleutel.  

Gebruik de volgende procedures om de vertrouwde basis sleutel voor een Configuration Manager-client vooraf in te richten en te verifiëren:  

- [Een client vooraf inrichten met de vertrouwde basis sleutel met behulp van een bestand](#bkmk_trk-provision-file)  

- [Een client vooraf inrichten met de vertrouwde basis sleutel zonder een bestand te gebruiken](#bkmk_trk-provision-nofile)  

- [De vertrouwde basis sleutel op een client controleren](#bkmk_trk-verify)  

- [De vertrouwde basis sleutel verwijderen of vervangen](#bkmk_trk-reset)  

  > [!NOTE]  
  > Als clients de vertrouwde basis sleutel van Active Directory Domain Services of client-push kunnen verkrijgen, hoeft u deze niet vooraf in te richten. 
  > 
  > Wanneer clients HTTPS-communicatie naar beheer punten gebruiken, hoeft u de vertrouwde basis sleutel niet vooraf in te richten. Ze maken vertrouwen aan de PKI-certificaten.  


### <a name="pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a><a name="bkmk_trk-provision-file"></a>Een client vooraf inrichten met de vertrouwde basis sleutel met behulp van een bestand  

1.  Open het volgende bestand in een tekst editor op de site server:`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Zoek de vermelding **SMSPublicRootKey =**. Kopieer de sleutel van die regel en sluit het bestand zonder wijzigingen.  

3.  Maak een nieuw tekst bestand en plak de belang rijke informatie die u hebt gekopieerd uit het bestand mobileclient. TCF.  

4.  Sla het bestand op een locatie op waar alle computers toegang tot hebben, maar waarbij het bestand veilig kan worden geknoeid.  

5.  Installeer de client met behulp van een installatie methode die client.msi eigenschappen accepteert. Geef de volgende eigenschap op:`SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    > Wanneer u de vertrouwde basis sleutel tijdens de client installatie opgeeft, moet u ook de site code opgeven. Gebruik de volgende client.msi eigenschap:`SMSSITECODE=<site code>`   


### <a name="pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a><a name="bkmk_trk-provision-nofile"></a>Een client vooraf inrichten met de vertrouwde basis sleutel zonder een bestand te gebruiken  

1.  Open het volgende bestand in een tekst editor op de site server:`<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Zoek de vermelding **SMSPublicRootKey =**. Kopieer de sleutel van die regel en sluit het bestand zonder wijzigingen.  

3.  Installeer de client met behulp van een installatie methode die client.msi eigenschappen accepteert. Geef de volgende client.msi eigenschap `SMSPublicRootKey=<key>` op: waar `<key>` is de teken reeks die u hebt gekopieerd uit mobileclient. TCF.  

    > [!IMPORTANT]  
    >  Wanneer u de vertrouwde basis sleutel tijdens de client installatie opgeeft, moet u ook de site code opgeven. Gebruik de volgende client.msi eigenschap:`SMSSITECODE=<site code>`   


### <a name="verify-the-trusted-root-key-on-a-client"></a><a name="bkmk_trk-verify"></a>De vertrouwde basis sleutel op een client controleren  

1. Open een Windows Power shell-console als beheerder.  

2. Voer de volgende opdracht uit:  

    ``` PowerShell
    (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
    ```

De geretourneerde teken reeks is de vertrouwde basis sleutel. Controleer of deze overeenkomt met de waarde **SMSPublicRootKey** in het bestand mobileclient. TCF op de site server.  


### <a name="remove-or-replace-the-trusted-root-key"></a><a name="bkmk_trk-reset"></a>De vertrouwde basis sleutel verwijderen of vervangen  

Verwijder de vertrouwde basis sleutel van een client met behulp van de eigenschap client.msi, **RESETKEYINFORMATION = True**. 

Als u de vertrouwde basis sleutel wilt vervangen, installeert u de client samen met de nieuwe vertrouwde basis sleutel. Gebruik bijvoorbeeld client-push of geef de client.msi eigenschap **SMSPublicRootKey**op.  

Zie [over para meters en eigenschappen van client installatie](../../clients/deploy/about-client-installation-properties.md)voor meer informatie over deze installatie-eigenschappen.



##  <a name="plan-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a>Plan voor ondertekening en versleuteling  
 
Wanneer u PKI-certificaten gebruikt voor alle client communicatie, hoeft u zich niet te plannen voor ondertekening en versleuteling om communicatie van client gegevens te helpen beveiligen. Als u site systemen hebt ingesteld die IIS uitvoeren om HTTP-client verbindingen toe te staan, moet u bepalen hoe u de client communicatie voor de site kunt beveiligen.  

Als u de gegevens die clients naar beheer punten verzenden wilt helpen beveiligen, kunt u vereisen dat clients de gegevens ondertekenen. U kunt ook de SHA-256-algoritme voor ondertekening vereisen. Deze configuratie is veiliger, maar vereist geen SHA-256 tenzij alle clients deze ondersteunen. Veel besturings systemen ondersteunen systeem eigen ondersteuning voor dit algoritme, maar voor oudere besturings systemen is mogelijk een update of hotfix vereist. 

Tijdens het ondertekenen helpt de gegevens te beschermen tegen knoeien, maar de gegevens worden door versleuteling beschermd tegen het vrijgeven van informatie. U kunt 3DES-versleuteling inschakelen voor de inventarisgegevens en faseberichten die door clients verstuurd worden naar beheerpunten in de site. U hoeft geen updates op clients te installeren om deze optie te ondersteunen. Clients en beheer punten vereisen extra CPU-gebruik voor versleuteling en ontsleuteling.  

Zie [ondertekening en versleuteling configureren](configure-security.md#BKMK_ConfigureSigningEncryption)voor meer informatie over het configureren van de instellingen voor ondertekening en versleuteling.  



##  <a name="plan-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a>Plannen voor op rollen gebaseerd beheer  

Zie [basis principes van beheer op basis van rollen](../../understand/fundamentals-of-role-based-administration.md)voor meer informatie.  



## <a name="plan-for-azure-active-directory"></a><a name="bkmk_planazuread"></a>Azure Active Directory plannen

Configuration Manager integreert met Azure Active Directory (Azure AD) om de site en clients in staat te stellen moderne verificatie te gebruiken. Het onboarden van uw site met Azure AD biedt ondersteuning voor de volgende Configuration Manager scenario's:

**Client**  

- [Clients op Internet beheren via de Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

- [Apparaten die lid zijn van het Cloud domein beheren](../../clients/deploy/deploy-clients-cmg-azure.md)  

- [Co-beheer](../../../comanage/overview.md)  

- [Door de gebruiker beschik bare Apps implementeren](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)

- [Microsoft Store voor Business Online-apps](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  

- De infrastructuur vereisten verlagen. Bijvoorbeeld [Software Center waarbij het beheer punt wordt gebruikt](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) in plaats van de toepassings catalogus  

- [Microsoft 365-apps voor bedrijven beheren](../../../sum/deploy-use/manage-office-365-proplus-updates.md)  


**Server**  

- [Desktop Analytics](../../../desktop-analytics/overview.md)  

- [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)  

- [Community Hub](../../get-started/capabilities-in-technical-preview-1807.md#bkmk_hub)  

- [Cloud distributiepunt](../hierarchy/use-a-cloud-based-distribution-point.md)  

- [Gebruikers detectie](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc)  


Zie [Azure-Services configureren](../../servers/deploy/configure/azure-services-wizard.md)voor meer informatie over het verbinden van uw site met Azure AD.


Zie [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/)voor meer informatie over Azure AD.



## <a name="plan-for-sms-provider-authentication"></a><a name="bkmk_auth"></a>Verificatie van de SMS-provider plannen
<!--1357013--> 

Vanaf versie 1810 kunt u het minimale verificatie niveau voor beheerders opgeven om toegang te krijgen tot Configuration Manager-sites. Deze functie dwingt beheerders af om zich aan te melden bij Windows met het vereiste niveau. Dit geldt voor alle onderdelen die toegang hebben tot de SMS-provider. Bijvoorbeeld de Configuration Manager-console, SDK-methoden en Windows Power shell-cmdlets. 

Deze configuratie is een instelling voor de hele hiërarchie. Voordat u deze instelling wijzigt, moet u ervoor zorgen dat alle Configuration Manager beheerders zich kunnen aanmelden bij Windows met het vereiste verificatie niveau. 

De volgende niveaus zijn beschikbaar:

- **Windows-verificatie**: authenticatie met Active Directory domein referenties vereisen.   

- **Certificaat verificatie**: authenticatie vereisen met een geldig certificaat dat is uitgegeven door een vertrouwde PKI-certificerings instantie.  

- **Windows hello voor bedrijven-verificatie**: authenticatie vereisen met een sterke twee ledige verificatie die is gekoppeld aan een apparaat en biometrie of een pincode gebruikt.  

Zie [de SMS-provider plannen](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)voor meer informatie. 



## <a name="see-also"></a>Zie ook
- [Beveiliging en privacy voor Configuration Manager-clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Beveiliging configureren](configure-security.md)  

- [Communicatie tussen eind punten](../hierarchy/communications-between-endpoints.md)  

- [Technische naslaginformatie voor cryptografische besturingselementen](cryptographic-controls-technical-reference.md)  

- [Vereisten voor PKI-certificaten](../network/pki-certificate-requirements.md)  

