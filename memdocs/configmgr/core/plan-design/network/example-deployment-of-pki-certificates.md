---
title: Voorbeeld van PKI-certificaatimplementatie
titleSuffix: Configuration Manager
description: Volg een stapsgewijs voor beeld voor meer informatie over het maken en implementeren van PKI-certificaten die Configuration Manager gebruiken.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 45ef103645630b8e203710ec0ff36a71b3cef4cf
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904255"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-configuration-manager-windows-server-2008-certification-authority"></a>Voor beeld van een stapsgewijze implementatie van de PKI-certificaten voor Configuration Manager: Windows Server 2008-certificerings instantie

*Van toepassing op: Configuration Manager (huidige vertakking)*

In deze stapsgewijze voorbeeld implementatie, die gebruikmaakt van een Windows Server 2008-certificerings instantie (CA), bevat procedures die laten zien hoe u de open bare-sleutel infrastructuur (PKI)-certificaten maakt en implementeert die Configuration Manager gebruiken. Bij deze procedures worden een bedrijfscertificeringsinstantie en certificaatsjablonen en gebruikt. De stappen zijn alleen geschikt voor een testnetwerk, voor het testen van het concept.  

Omdat er geen implementatie methode is voor de vereiste certificaten, raadpleegt u de documentatie voor de implementatie van de PKI voor de vereiste procedures en aanbevolen procedures voor het implementeren van de vereiste certificaten voor een productie omgeving. Zie [PKI-certificaat vereisten voor Configuration Manager](pki-certificate-requirements.md)voor meer informatie over de certificaat vereisten.  

> [!TIP]
> U kunt de instructies in dit onderwerp aanpassen voor besturings systemen die niet zijn beschreven in de sectie netwerk vereisten testen. Als u echter de verlenende CA uitvoert op Windows Server 2012, wordt u niet gevraagd om de versie van de certificaat sjabloon. In plaats daarvan geeft u dit op op het tabblad **compatibiliteit** van de sjabloon eigenschappen:  
>
> - **Certificeringsinstantie**: **Windows Server 2003**  
>   - **Ontvanger van het certificaat**: **Windows XP / Server 2003**  

## <a name="test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a>Test netwerk vereisten

De stapsgewijze instructies hebben de volgende vereisten:  

- Het testnetwerk voert Active Directory Domain Services uit met Windows Server 2008 en is geïnstalleerd als een enkel domein, enkel forest.  

- U hebt een lidserver met Windows Server 2008 Enter prise Edition, waarop de Active Directory Certificate Services-rol is geïnstalleerd en die is ingesteld als een basis certificerings instantie (CA) voor ondernemingen.  

- U hebt één computer waarop Windows Server 2008 (Standard Edition of ENTER prise Edition, R2 of hoger) is geïnstalleerd, die computer is aangewezen als lidserver en Internet Information Services (IIS) is geïnstalleerd. Deze computer wordt de Configuration Manager-site systeem server die u configureert met een intranet-Fully Qualified Domain Name (FQDN) voor de ondersteuning van client verbindingen op het intranet en een Internet-FQDN als u mobiele apparaten moet ondersteunen die zijn Inge schreven door Configuration Manager en clients op internet.  

- U hebt een Windows Vista-client met het nieuwste Service Pack geïnstalleerd en deze computer is ingesteld met een computer naam die ASCII-tekens bevat en is toegevoegd aan het domein. Deze computer is een Configuration Manager-client computer.  

- U kunt zich aanmelden met een beheerders account voor het hoofd domein of een beheerders account voor ondernemings domein en dit account gebruiken voor alle procedures in deze voorbeeld implementatie.  

## <a name="overview-of-the-certificates"></a><a name="BKMK_overview2008"></a>Overzicht van de certificaten

De volgende tabel bevat de typen PKI-certificaten die mogelijk vereist zijn voor Configuration Manager en beschrijft hoe ze worden gebruikt.  

|Certificaatvereiste|Certificaatbeschrijving|  
|-----------------------------|-----------------------------|  
|Webservercertificaat voor sitesystemen die IIS uitvoeren|Dit certificaat wordt gebruikt om gegevens te coderen en de server te verifiëren naar clients. Het moet extern worden geïnstalleerd van Configuration Manager op site systeem servers waarop Internet Information Services (IIS) wordt uitgevoerd en die zijn ingesteld in Configuration Manager om HTTPS te gebruiken.<br /><br /> Zie [het webserver certificaat implementeren voor site systemen die IIS uitvoeren](#BKMK_webserver2008_cm2012) in dit onderwerp voor de stappen voor het instellen en installeren van dit certificaat.|  
|Servicecertificaat voor clients voor verbinding maken met cloud-gebaseerde distributiepunten|Zie [het service certificaat voor cloud-gebaseerde distributie punten implementeren](#BKMK_clouddp2008_cm2012) in dit onderwerp voor de stappen voor het configureren en installeren van dit certificaat.<br /><br /> **Belangrijk:** dit certificaat wordt in combinatie met het Microsoft Azure-beheercertificaat gebruikt. Zie [How to Create a Management Certificate](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#create-a-new-self-signed-certificate) (een beheer certificaat maken) en [een beheer certificaat toevoegen aan een Windows Azure-abonnement](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate-portal#step-3-upload-a-certificate)voor meer informatie over het beheer certificaat.|  
|Clientcertificaat voor Windows-computers|Dit certificaat wordt gebruikt om Configuration Manager-client computers te verifiëren naar site systemen die zijn ingesteld voor het gebruik van HTTPS. Het kan ook worden gebruikt voor beheer punten en status migratie punten om hun operationele status te controleren wanneer ze zijn ingesteld voor het gebruik van HTTPS. Het moet extern worden geïnstalleerd van Configuration Manager op computers.<br /><br /> Zie [het client certificaat voor Windows-computers implementeren](#BKMK_client2008_cm2012) in dit onderwerp voor de stappen voor het instellen en installeren van dit certificaat.|  
|Clientcertificaat voor distributiepunten|Dit certificaat heeft twee doeleinden:<br /><br /> Het certificaat wordt gebruikt om het distributiepunt naar een HTTPS-beheerpunt te verifiëren voordat het distributiepunt statusberichten verzendt.<br /><br /> Wanneer de distributiepuntoptie **PXE-ondersteuning voor clients inschakelen** is geselecteerd, wordt het certificaat verzonden naar computers die een PXE-opstartbewerking uitvoeren, zodat ze verbinding kunnen maken met een HTTPS-beheerpunt tijdens de implementatie van het besturingssysteem.<br /><br /> Zie [het client certificaat voor distributie punten implementeren](#BKMK_clientdistributionpoint2008_cm2012) in dit onderwerp voor de stappen voor het instellen en installeren van dit certificaat.|  
|Certificaat voor inschrijving voor mobiele apparaten|Dit certificaat wordt gebruikt voor het verifiëren van Configuration Manager clients voor mobiele apparaten naar site systemen die zijn ingesteld voor het gebruik van HTTPS. Het moet worden geïnstalleerd als onderdeel van inschrijving van mobiele apparaten in Configuration Manager en u kiest het geconfigureerde certificaat sjabloon als een client instelling voor mobiele apparaten.<br /><br /> Zie [het certificaat voor inschrijving voor mobiele apparaten implementeren](#BKMK_mobiledevices2008_cm2012) in dit onderwerp voor de stappen voor het instellen van dit certificaat.|  
|Clientcertificaat voor Mac-computers|U kunt dit certificaat aanvragen en installeren vanaf een Mac-computer wanneer u Configuration Manager-inschrijving gebruikt en het geconfigureerde certificaat sjabloon als een client instelling voor mobiele apparaten kiest.<br /><br /> Zie [het client certificaat voor Mac-computers implementeren](#BKMK_MacClient_SP1) in dit onderwerp voor de stappen voor het instellen van dit certificaat.|  

## <a name="deploy-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a>Het webserver certificaat implementeren voor site systemen die IIS uitvoeren

Deze certificaatimplementatie heeft de volgende procedures:  

- Maken en publiceren van het sjabloon webserver certificaat bij de certificerings instantie  

- Het webserver certificaat aanvragen  

- IIS configureren voor het gebruik van het webserver certificaat  

### <a name="create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a>Maken en publiceren van het sjabloon webserver certificaat bij de certificerings instantie

Met deze procedure maakt u een certificaat sjabloon voor Configuration Manager site systemen en voegt u het toe aan de certificerings instantie.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Maken en publiceren van het sjabloon webservercertificaat bij de certificeringsinstantie

1.  Maak een beveiligings groep met de naam **CONFIGMGR IIS servers** die de lidservers bevat om Configuration Manager-site systemen te installeren die IIS gaan uitvoeren.  

2.  Klik met de rechter muisknop op **certificaat sjablonen** op de lidserver waarop de Certificate Services zijn geïnstalleerd en klik vervolgens op **beheren** om de **certificaat sjablonen** console te laden.  

3.  Klik in het resultaten venster met de rechter muisknop op het item met **webserver** in de kolom **sjabloon weergave naam** en kies **sjabloon dupliceren**.  

4.  Zorg er in het dialoog venster **sjabloon dupliceren** voor dat **Windows 2003 server, Enter prise Edition** is geselecteerd, en kies vervolgens **OK**.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition** niet selecteren.  

5.  Voer in het dialoog venster **Eigenschappen van nieuwe sjabloon** , op het tabblad **Algemeen** , de naam van een sjabloon, zoals **ConfigMgr-webserver certificaat**, in om de webcertificaten te genereren die zullen worden gebruikt op Configuration Manager site systemen.  

6.  Kies het tabblad **onderwerpnaam** en zorg ervoor dat **de optie in de aanvraag** wordt geselecteerd.  

7.  Kies het tabblad **beveiliging** en verwijder de machtiging **Inschrijven** uit de beveiligings groepen **domein Administrators** en **ondernemings Administrators** .  

8.  Klik op **toevoegen**, Voer **ConfigMgr IIS-servers** in het tekstvak in en kies vervolgens **OK**.  

9. Kies de machtiging **Inschrijven** voor deze groep en verwijder de machtiging **lezen** niet.  

10. Klik op **OK**en sluit de **certificaat sjablonen console**.  

11. Klik in de certificerings instantie console met de rechter muisknop op **certificaat sjablonen**, kies **Nieuw**en kies vervolgens **te verlenen certificaat sjablonen**.  

12. Kies in het dialoog venster **certificaat sjablonen inschakelen** de nieuwe sjabloon die u zojuist hebt gemaakt, **ConfigMgr-webserver certificaat**, en kies vervolgens **OK**.  

13. Sluit de **certificerings instantie**als u geen certificaten meer hoeft te maken en verlenen.  

###  <a name="request-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a>Het webserver certificaat aanvragen  
 Met deze procedure kunt u de intranet-en Internet-FQDN-waarden opgeven die worden ingesteld in de eigenschappen van de site systeem server en vervolgens het webserver certificaat installeren op de lidserver waarop IIS wordt uitgevoerd.  

##### <a name="to-request-the-web-server-certificate"></a>Het webservercertificaat aanvragen  

1.  Start de lidserver die IIS uitvoert opnieuw op om te controleren of de computer toegang heeft tot het certificaat sjabloon dat u hebt gemaakt met behulp van de **Lees** -en **registratie** -machtigingen die u hebt geconfigureerd.  

2.  Kies **Start**, kies **uitvoeren**en typ vervolgens **MMC. exe.** Kies in de lege console **bestand**en kies vervolgens **module toevoegen/verwijderen**.  

3.  Kies in het dialoog venster **modules toevoegen of verwijderen** de optie **certificaten** in de lijst met **beschik bare**modules en kies vervolgens **toevoegen**.  

4.  Kies **computer account**in het dialoog venster **certificaat module** en kies **volgende**.  

5.  Zorg er in het dialoog venster **computer selecteren** **voor dat lokale computer: (de computer waarop deze console wordt uitgevoerd)** is geselecteerd en kies vervolgens **volt ooien**.  

6.  Kies **OK**in het dialoog venster **modules toevoegen of verwijderen** .  

7.  Vouw **certificaten (lokale computer)** uit in de console en kies vervolgens **persoonlijk**.  

8.  Klik met de rechter muisknop op **certificaten**, kies **alle taken**en kies vervolgens **Nieuw certificaat aanvragen**.  

9. Klik op de pagina **voordat u begint** op **volgende**.  

10. Als u de pagina certificaatinschrijvingsbeleid **selecteren** ziet, kiest u **volgende**.  

11. Zoek op de pagina **certificaten aanvragen** naar het **ConfigMgr-webserver certificaat** in de lijst met beschik bare certificaten en kies vervolgens **meer informatie vereist voor inschrijving voor dit certificaat. Klik hier om instellingen te configureren**.  

12. In het dialoog venster **Eigenschappen voor certificaat** , op het tabblad **onderwerp** , moet u geen wijzigingen aanbrengen in de **onderwerpnaam**. Dit betekent dat het vak **Waarde** voor het gedeelte **Onderwerpnaam leeg** blijft. In plaats daarvan kiest u in de sectie **alternatieve naam** de vervolg keuzelijst **type** en kiest u vervolgens **DNS**.  

13. Geef in het vak **waarde** de FQDN-waarden op die u wilt opgeven in de Configuration Manager site systeem eigenschappen, en kies vervolgens **OK** om het dialoog venster **Eigenschappen voor certificaat** te sluiten.  

     Voorbeelden:  

    - Als het site systeem alleen client verbindingen van het intranet accepteert en de intranet-FQDN van de site systeem server is **Server1.internal.contoso.com**, voert u **Server1.internal.contoso.com**in en kiest u **toevoegen**.  

    - Als het site systeem client verbindingen accepteert van het intranet en het Internet, en de intranet-FQDN van de site systeem server is **Server1.internal.contoso.com** en de Internet-FQDN van de site systeem server is **server.contoso.com**:  

        1.  Voer **Server1.internal.contoso.com**in en kies vervolgens **toevoegen**.  

        2.  Voer **server.contoso.com**in en kies vervolgens **toevoegen**.  

        > [!NOTE]  
        >  U kunt de FQDN-Configuration Manager in een wille keurige volg orde opgeven. Controleer echter of alle apparaten die het certificaat gaan gebruiken, zoals mobiele apparaten en proxy webservers, een alternatieve naam voor het certificaat onderwerp (SAN) en meerdere waarden in de SAN kunnen gebruiken. Als apparaten beperkt worden ondersteund voor SAN-waarden in certificaten, moet u mogelijk de volgorde van de FQDN's wijzigen of de onderwerpwaarde gebruiken.  

14. Kies op de pagina **certificaten aanvragen** het **ConfigMgr-webserver certificaat** in de lijst met beschik bare certificaten en kies vervolgens **registreren**.  

15. Wacht tot het certificaat is geïnstalleerd op de pagina **resultaten van installatie van certificaten** en kies vervolgens **volt ooien**.  

16. Sluit **Certificaten (lokale computer)**.  

###  <a name="configure-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a>IIS configureren voor het gebruik van het webserver certificaat  
 Met deze procedure koppelt u het geïnstalleerde certificaat aan de **IIS-standaardwebsite**.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>IIS instellen voor het gebruik van het webserver certificaat  

1. Op de lidserver waarop IIS is geïnstalleerd, kiest u **Start**, kiest u **Program ma's**, kiest u **systeem beheer**en kiest u vervolgens **Internet Information Services (IIS) Manager**.  

2. Vouw **sites**uit, klik met de rechter muisknop op **standaard website**en kies vervolgens **bindingen bewerken**.  

3. Kies de **https** -vermelding en kies vervolgens **bewerken**.  

4. Selecteer in het dialoog venster **site binding bewerken** het certificaat dat u hebt aangevraagd met behulp van de sjabloon voor de ConfigMgr-webserver certificaten en kies vervolgens **OK**.  

   > [!NOTE]  
   >  Als u niet zeker weet welk certificaat het juiste is, kiest u er een en kiest u vervolgens **weer gave**. Hiermee kunt u de details van het geselecteerde certificaat vergelijken met de certificaten in de module Certificaten. De module Certificaten bevat bijvoorbeeld het certificaat sjabloon dat is gebruikt om het certificaat aan te vragen. U kunt vervolgens de vinger afdruk vergelijken van het certificaat dat is aangevraagd met behulp van het ConfigMgr-webserver certificaten sjabloon naar de vinger afdruk van het certificaat dat momenteel is geselecteerd in het dialoog venster **site binding bewerken** .  

5. Kies **OK** in het dialoog venster **site binding bewerken** en kies vervolgens **sluiten**.  

6. Sluit **IIS-beheer**.  

   De lidserver is nu ingesteld met een Configuration Manager-webserver certificaat.  

> [!IMPORTANT]  
>  Wanneer u de Configuration Manager-site systeem server op deze computer installeert, moet u ervoor zorgen dat u dezelfde FQDN-namen opgeeft in de site systeem eigenschappen zoals opgegeven wanneer u het certificaat aanvraagt.  

##  <a name="deploy-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a>Het service certificaat voor cloud-gebaseerde distributie punten implementeren  

Deze certificaatimplementatie heeft de volgende procedures:  

- [Een aangepast webserver certificaat sjabloon maken en uitgeven bij de certificerings instantie](#BKMK_clouddpcreating2008)  

- [Het aangepaste webserver certificaat aanvragen](#BKMK_clouddprequesting2008)  

- [Het aangepaste webserver certificaat voor cloud-gebaseerde distributie punten exporteren](#BKMK_clouddpexporting2008)  

###  <a name="create-and-issue-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a>Een aangepast webserver certificaat sjabloon maken en uitgeven bij de certificerings instantie  
 Met deze procedure maakt u een aangepast certificaat sjabloon dat is gebaseerd op het sjabloon webserver certificaat. Het certificaat is voor Configuration Manager cloud-gebaseerde distributie punten en de persoonlijke sleutel moet exporteerbaar zijn. Na het maken van het certificaatsjabloon, wordt het toegevoegd aan de certificeringsinstantie.  

> [!NOTE]
>  In deze procedure wordt een ander certificaat sjabloon gebruikt dan het webserver certificaat sjabloon dat u hebt gemaakt voor site systemen die IIS uitvoeren. Hoewel voor beide certificaten Server verificatie is vereist, moet u voor het certificaat voor cloud-gebaseerde distributie punten een aangepaste waarde opgeven voor de onderwerpnaam en de persoonlijke sleutel exporteren. Als beveiligings best practice moet u geen certificaat sjablonen instellen, zodat de persoonlijke sleutel kan worden geëxporteerd, tenzij deze configuratie vereist is. Het distributie punt in de Cloud vereist deze configuratie omdat u het certificaat als een bestand moet importeren in plaats van het uit het certificaat archief te kiezen.  
> 
>  Wanneer u een nieuw certificaat sjabloon maakt voor dit certificaat, kunt u de computers beperken die een certificaat kunnen aanvragen waarvan de persoonlijke sleutel kan worden geëxporteerd. In een productie netwerk kunt u ook overwegen de volgende wijzigingen toe te voegen voor dit certificaat:  
> 
> - Goed keuring vereisen voor het installeren van het certificaat voor extra beveiliging.  
>   - Vergroten van de geldigheidsduur van het certificaat. Omdat u het certificaat elke keer voordat het verloopt, moet exporteren en importeren, vermindert een toename van de geldigheids periode hoe vaak u deze procedure moet herhalen. Een toename van de geldigheids periode vermindert echter ook de beveiliging van het certificaat omdat het meer tijd biedt voor een aanvaller om de persoonlijke sleutel te ontsleutelen en het certificaat te stelen.  
>   - Gebruik een aangepaste waarde in de SAN (Subject Alternative Name) van het certificaat om dit certificaat te onderscheiden van standaardwebservercertificaten die u bij IIS gebruikt.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Maken en publiceren van het aangepaste sjabloon webserver certificaat bij de certificerings instantie  

1.  Maak een beveiligings groep met de naam **ConfigMgr-site servers** die de lidservers bevat om Configuration Manager primaire site servers te installeren die distributie punten in de cloud gaan beheren.  

2.  Klik met de rechter muisknop op **certificaat sjablonen**op de lidserver waarop de certificerings instantie console wordt uitgevoerd en kies vervolgens **beheren** om de beheer console voor certificaat sjablonen te laden.  

3.  Klik in het resultaten venster met de rechter muisknop op het item met **webserver** in de kolom **sjabloon weergave naam** en kies **sjabloon dupliceren**.  

4.  Zorg er in het dialoog venster **sjabloon dupliceren** voor dat **Windows 2003 server, Enter prise Edition** is geselecteerd, en kies vervolgens **OK**.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition** niet selecteren.  

5.  Voer in het dialoog venster **Eigenschappen van nieuwe sjabloon** , op het tabblad **Algemeen** , de naam van een sjabloon in, zoals **ConfigMgr cloud-gebaseerde distributiepunt certificaat**, om het webserver certificaat voor cloud-gebaseerde distributie punten te genereren.  

6.  Kies het tabblad **afhandeling van aanvragen** en kies vervolgens de optie **persoonlijke sleutel exporteren toestaan**.  

7.  Kies het tabblad **beveiliging** en verwijder de machtiging **Inschrijven** uit de beveiligings groep **ondernemings Administrators** .  

8.  Klik op **toevoegen**, Voer **ConfigMgr-site servers** in het tekstvak in en kies vervolgens **OK**.  

9. Selecteer de machtiging **Inschrijven** voor deze groep en verwijder de machtiging **lezen** niet.  

10. Kies het tabblad **crypto grafie** en zorg ervoor dat de **minimale sleutel grootte** is ingesteld op **2048**.

11. Kies **OK**en sluit de **console certificaat sjablonen**.  

12. Klik in de certificerings instantie console met de rechter muisknop op **certificaat sjablonen**, kies **Nieuw**en kies vervolgens **te verlenen certificaat sjablonen**.  

13. Kies in het dialoog venster **certificaat sjablonen inschakelen** de nieuwe sjabloon die u zojuist hebt gemaakt, **ConfigMgr cloud-gebaseerde distributiepunt certificaat**, en kies vervolgens **OK**.  

14. Sluit de **certificerings instantie**als u geen certificaten meer moet maken en verlenen.  

###  <a name="request-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a>Het aangepaste webserver certificaat aanvragen  
 Met deze procedure vraagt u het aangepaste webserver certificaat aan en installeert u het op de lidserver die de site server gaat uitvoeren.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Het aangepaste webservercertificaat aanvragen  

1.  Start de lidserver opnieuw op nadat u de beveiligings groep **Configuration Manager-site servers** hebt gemaakt en geconfigureerd om ervoor te zorgen dat de computer toegang heeft tot het certificaat sjabloon dat u hebt gemaakt met behulp van de **Lees** -en **registratie** -machtigingen die u hebt geconfigureerd.  

2.  Kies **Start**, kies **uitvoeren**en voer vervolgens **MMC. exe in.** Kies in de lege console **bestand**en kies vervolgens **module toevoegen/verwijderen**.  

3.  Kies in het dialoog venster **modules toevoegen of verwijderen** de optie **certificaten** in de lijst met **beschik bare**modules en kies vervolgens **toevoegen**.  

4.  Kies **computer account**in het dialoog venster **certificaat module** en kies **volgende**.  

5.  Zorg er in het dialoog venster **computer selecteren** **voor dat lokale computer: (de computer waarop deze console wordt uitgevoerd)** is geselecteerd en kies vervolgens **volt ooien**.  

6.  Kies **OK**in het dialoog venster **modules toevoegen of verwijderen** .  

7.  Vouw **certificaten (lokale computer)** uit in de console en kies vervolgens **persoonlijk**.  

8.  Klik met de rechter muisknop op **certificaten**, kies **alle taken**en kies vervolgens **Nieuw certificaat aanvragen**.  

9. Klik op de pagina **voordat u begint** op **volgende**.  

10. Als u de pagina certificaatinschrijvingsbeleid **selecteren** ziet, kiest u **volgende**.  

11. Zoek op de pagina **certificaten aanvragen** naar het **ConfigMgr cloud-gebaseerde distributiepunt certificaat** in de lijst met beschik bare certificaten en kies vervolgens **meer informatie vereist voor inschrijving voor dit certificaat. Klik hier om instellingen te configureren**.  

12. Kies in het dialoog venster **Eigenschappen voor certificaat** , op het tabblad **onderwerp** , voor de **onderwerpnaam** **algemene naam** als het **type**.  

13. Geef in het vak **Waarde** uw keuze op voor de servicenaam en uw domeinnaam met een FQDN-indeling. Bijvoorbeeld: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Zorg ervoor dat de service naam uniek is in uw naam ruimte. U gebruikt DNS om een alias (CNAME-record) te maken om deze servicenaam toe te wijzen aan een automatisch gegenereerd id (GUID) en een IP-adres van Windows Azure.  

14. Kies **toevoegen**en vervolgens **OK** om het dialoog venster **Eigenschappen voor certificaat** te sluiten.  

15. Kies op de pagina **certificaten aanvragen** het **ConfigMgr cloud-gebaseerde distributiepunt certificaat** in de lijst met beschik bare certificaten en kies vervolgens **registreren**.  

16. Wacht tot het certificaat is geïnstalleerd op de pagina **resultaten van installatie van certificaten** en kies vervolgens **volt ooien**.  

17. Sluit **Certificaten (lokale computer)**.  

###  <a name="export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a>Het aangepaste webserver certificaat voor cloud-gebaseerde distributie punten exporteren  
 Met deze procedure exporteert u het aangepaste webservercertificaat naar een bestand zodat het kan worden geïmporteerd wanneer u het cloud-gebaseerde distributiepunt maakt.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Exporteren van het aangepaste webservercertificaat voor cloud-gebaseerde distributiepunten  

1. Klik in de console **certificaten (lokale computer)** met de rechter muisknop op het certificaat dat u zojuist hebt geïnstalleerd, kies **alle taken**en kies **exporteren**.  

2. Klik in de wizard certificaten exporteren op **volgende**.  

3. Kies op de pagina **persoonlijke sleutel exporteren** **de optie Ja, de persoonlijke sleutel exporteren**en klik vervolgens op **volgende**.  

   > [!NOTE]  
   >  Als deze optie niet beschikbaar is, is het certificaat gemaakt zonder de optie om de persoonlijke sleutel te exporteren. In dit scenario kunt u het certificaat niet exporteren in de vereiste indeling. U moet de certificaat sjabloon zo instellen dat de persoonlijke sleutel kan worden geëxporteerd en het certificaat vervolgens opnieuw aanvragen.  

4. Zorg ervoor dat op de pagina **bestands indeling voor export** de **Personal Information Exchange-PKCS #12 (. PFX)** is geselecteerd.  

5. Geef op de pagina **wacht** woord een sterk wacht woord op om het geëxporteerde certificaat met de persoonlijke sleutel te beveiligen en klik vervolgens op **volgende**.  

6. Geef op de pagina **te exporteren bestand** de naam op van het bestand dat u wilt exporteren en klik vervolgens op **volgende**.  

7. Klik op **volt ooien** op de pagina **wizard Certificaat exporteren** om de wizard te sluiten en kies vervolgens **OK** in het bevestigings venster.  

8. Sluit **Certificaten (lokale computer)**.  

9. Sla het bestand veilig op en zorg ervoor dat u het kunt openen vanuit de Configuration Manager-console.  

   Het certificaat kan nu worden geïmporteerd wanneer u een cloud-gebaseerd distributiepunt maakt.  

##  <a name="deploy-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a>Het client certificaat voor Windows-computers implementeren  
 Deze certificaatimplementatie heeft de volgende procedures:  

- Maken en uitgeven van het certificaat sjabloon voor verificatie van werk station bij de certificerings instantie  

- Automatische inschrijving configureren van de sjabloon voor verificatie van werk station met behulp van groepsbeleid  

- Het certificaat voor verificatie van werk station automatisch inschrijven en de installatie ervan controleren op computers  

###  <a name="create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a>Maken en uitgeven van het certificaat sjabloon voor verificatie van werk station bij de certificerings instantie  
 Met deze procedure maakt u een certificaat sjabloon voor Configuration Manager-client computers en voegt u het toe aan de certificerings instantie.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Maken en publiceren van het certificaatsjabloon voor verificatie van werkstation bij de certificeringsinstantie  

1.  Klik met de rechter muisknop op **certificaat sjablonen**op de lidserver waarop de certificerings instantie console wordt uitgevoerd en kies vervolgens **beheren** om de beheer console voor certificaat sjablonen te laden.  

2.  Klik in het resultaten venster met de rechter muisknop op het item met **werk station verificatie** in de kolom **sjabloon weergave naam** en kies **sjabloon dupliceren**.  

3.  Zorg er in het dialoog venster **sjabloon dupliceren** voor dat **Windows 2003 server, Enter prise Edition** is geselecteerd, en kies vervolgens **OK**.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition** niet selecteren.  

4.  Voer in het dialoog venster **Eigenschappen van nieuwe sjabloon** , op het tabblad **Algemeen** , de naam van een sjabloon, zoals **ConfigMgr-client certificaat**, in om de client certificaten te genereren die worden gebruikt op Configuration Manager-client computers.  

5.  Kies het tabblad **beveiliging** , selecteer de groep **domein computers** en selecteer vervolgens de extra machtigingen voor **lezen** en **automatisch inschrijven**. **Inschrijven**niet wissen.  

6.  Kies **OK**en sluit de **console certificaat sjablonen**.  

7.  Klik in de certificerings instantie console met de rechter muisknop op **certificaat sjablonen**, kies **Nieuw**en kies vervolgens **te verlenen certificaat sjablonen**.  

8.  Kies in het dialoog venster **certificaat sjablonen inschakelen** de nieuwe sjabloon die u zojuist hebt gemaakt, **ConfigMgr-client certificaat**en kies vervolgens **OK**.  

9. Sluit de **certificerings instantie**als u geen certificaten meer hoeft te maken en verlenen.  

###  <a name="configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a>Automatische inschrijving configureren van de sjabloon voor verificatie van werk station met behulp van groepsbeleid  
 Met deze procedure stelt u groepsbeleid in voor het automatisch inschrijven van het client certificaat op computers.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Automatische inschrijving van de sjabloon voor verificatie van werk station instellen met behulp van groepsbeleid  

1.  Kies op de domein controller **Start**, kies **systeem beheer**en kies vervolgens **Groepsbeleid beheer**.  

2.  Ga naar uw domein, klik met de rechter muisknop op het domein en kies vervolgens **een groeps beleidsobject in dit domein maken en hier een koppeling**.  

    > [!NOTE]  
    >  De aanbevolen werkwijze voor deze stap is nieuw groepsbeleid maken voor aangepaste instellingen in plaats van het standaardgroepsbeleid te bewerken dat is geïnstalleerd met Active Directory Domain Services. Wanneer u deze groepsbeleid toewijst op domein niveau, past u deze toe op alle computers in het domein. In een productie omgeving kunt u de automatische inschrijving beperken zodat deze alleen op geselecteerde computers wordt Inge schreven. U kunt de groepsbeleid toewijzen op het niveau van een organisatie-eenheid, of u kunt het domein groepsbeleid filteren met een beveiligings groep, zodat deze alleen van toepassing is op de computers in de groep. Als u automatische inschrijving beperkt, vergeet dan niet de server in te voegen die is ingesteld als het beheer punt.  

3.  Voer in het dialoog venster **Nieuw groeps beleidsobject** een naam in, zoals **certificaten voor automatisch inschrijven**, voor het nieuwe Groepsbeleid en kies vervolgens **OK**.  

4.  Klik in het deel venster met resultaten op het tabblad **gekoppelde Groepsbeleid objecten** met de rechter muisknop op de nieuwe Groepsbeleid en kies vervolgens **bewerken**.  

5.  Vouw in het **Groepsbeleidsbeheer-editor** **beleid** uit onder **computer configuratie**en ga vervolgens naar **Windows-instellingen**  /  **beveiligings instellingen**  /  **beleid voor open bare sleutels**.  

6.  Klik met de rechter muisknop op het object type met de naam **Certificate Services-client-automatisch inschrijven**en kies vervolgens **Eigenschappen**.  

7.  Kies in de vervolg keuzelijst **configuratie model** de optie **ingeschakeld**, kies **verlopen certificaten vernieuwen, aangevraagde certificaten bijwerken, ingetrokken certificaten verwijderen**, selecteer **certificaten bijwerken die gebruikmaken van certificaat sjablonen**en kies vervolgens **OK**.  

8.  Sluiten **Groepsbeleidsbeheer**.  

###  <a name="automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-computers"></a><a name="BKMK_client22008"></a>Het certificaat voor verificatie van werk station automatisch inschrijven en de installatie ervan controleren op computers  
 Met deze procedure installeert u het clientcertificaat op computers en verifieert u de installatie.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Het certificaat voor verificatie van werk station automatisch inschrijven en de installatie controleren op de client computer  

1. Start de Werkstationcomputer opnieuw op en wacht enkele minuten voordat u zich aanmeldt.  

   > [!NOTE]  
   >  Opstarten van een computer is de betrouwbaarste methode voor een goed verloop van automatische inschrijving voor certificaten.  

2. Meld u aan met een account met beheerders bevoegdheden.  

3. Voer in het zoekvak **MMC. exe.** en druk op **Enter**.  

4. Kies in de lege beheer console de optie **bestand**en kies vervolgens **module toevoegen/verwijderen**.  

5. Kies in het dialoog venster **modules toevoegen of verwijderen** de optie **certificaten** in de lijst met **beschik bare**modules en kies vervolgens **toevoegen**.  

6. Kies **computer account**in het dialoog venster **certificaat module** en kies **volgende**.  

7. Zorg er in het dialoog venster **computer selecteren** **voor dat lokale computer: (de computer waarop deze console wordt uitgevoerd)** is geselecteerd en kies vervolgens **volt ooien**.  

8. Kies **OK**in het dialoog venster **modules toevoegen of verwijderen** .  

9. Vouw **certificaten (lokale computer)** uit in de console, vouw **persoonlijk**uit en kies vervolgens **certificaten**.  

10. Bevestig in het resultaten venster dat een certificaat **client verificatie** heeft in de kolom **beoogd doel einde** en dat **ConfigMgr-client certificaat** voor komt in de kolom **certificaat sjabloon** .  

11. Sluit **Certificaten (lokale computer)**.  

12. Herhaal stap 1 tot en met 11 voor de lidserver om te controleren of de server die wordt ingesteld als het beheer punt ook een client certificaat heeft.  

    De computer is nu ingesteld met een Configuration Manager-client certificaat.  

##  <a name="deploy-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a>Het client certificaat voor distributie punten implementeren  

> [!NOTE]  
>  Dit certificaat kan ook worden gebruikt voor media-afbeeldingen die geen PXE-opstartapparaat gebruiken omdat de certificaatvereisten dezelfde zijn.  

 Deze certificaatimplementatie heeft de volgende procedures:  

- Een aangepast certificaat sjabloon voor verificatie van werk station maken en uitgeven bij de certificerings instantie  

- Het aangepaste certificaat voor verificatie van werk station aanvragen  

- Het client certificaat voor distributie punten exporteren  

###  <a name="create-and-issue-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a>Een aangepast certificaat sjabloon voor verificatie van werk station maken en uitgeven bij de certificerings instantie  
 Met deze procedure maakt u een aangepast certificaat sjabloon voor Configuration Manager distributie punten, zodat de persoonlijke sleutel kan worden geëxporteerd en het certificaat sjabloon kan worden toegevoegd aan de certificerings instantie.  

> [!NOTE]
>  Deze procedure maakt gebruik van een ander certificaat sjabloon dan het certificaat sjabloon dat u hebt gemaakt voor client computers. Hoewel voor beide certificaten client verificatie is vereist, moet voor het certificaat voor distributie punten de persoonlijke sleutel worden geëxporteerd. Als beveiligings best practice moet u geen certificaat sjablonen instellen, dus de persoonlijke sleutel kan alleen worden geëxporteerd als deze configuratie vereist is. Voor het distributie punt is deze configuratie vereist omdat u het certificaat moet importeren als een bestand in plaats van het te selecteren in het certificaat archief.  
> 
>  Wanneer u een nieuw certificaat sjabloon maakt voor dit certificaat, kunt u de computers beperken die een certificaat kunnen aanvragen waarvan de persoonlijke sleutel kan worden geëxporteerd. In onze voorbeeld implementatie is dit de beveiligings groep die u eerder hebt gemaakt voor Configuration Manager site systeem servers waarop IIS wordt uitgevoerd. Overweeg een nieuwe beveiligingsgroep voor een productienetwerk dat de IIS-sitesysteemrollen distribueert voor de servers die distributiepunten uitvoeren zodat u het certificaat kunt beperken tot alleen deze sitesysteemservers. U kunt ook overwegen de volgende wijzigingen toe te voegen voor dit certificaat:  
> 
> - Goed keuring vereisen voor het installeren van het certificaat voor extra beveiliging.  
>   - Vergroten van de geldigheidsduur van het certificaat. Omdat u het certificaat elke keer voordat het verloopt, moet exporteren en importeren, vermindert een toename van de geldigheids periode hoe vaak u deze procedure moet herhalen. Een toename van de geldigheids periode vermindert echter ook de beveiliging van het certificaat omdat het meer tijd biedt voor een aanvaller om de persoonlijke sleutel te ontsleutelen en het certificaat te stelen.  
>   - Gebruik een aangepaste waarde in het veld Onderwerp of SAN (Subject Alternative Name) om dit certificaat te onderscheiden van standaardclientcertificaten. Dit kan vooral nuttig zijn als u hetzelfde certificaat gaat gebruiken voor meerdere distributiepunten.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Maken en publiceren van het aangepaste certificaatsjabloon voor verificatie van werkstation bij de certificeringsinstantie  

1.  Klik met de rechter muisknop op **certificaat sjablonen**op de lidserver waarop de certificerings instantie console wordt uitgevoerd en kies vervolgens **beheren** om de beheer console voor certificaat sjablonen te laden.  

2.  Klik in het resultaten venster met de rechter muisknop op het item met **werk station verificatie** in de kolom **sjabloon weergave naam** en kies **sjabloon dupliceren**.  

3.  Zorg er in het dialoog venster **sjabloon dupliceren** voor dat **Windows 2003 server, Enter prise Edition** is geselecteerd, en kies vervolgens **OK**.  

    > [!IMPORTANT]  
    >  **Windows 2008 Server, Enterprise Edition** niet selecteren.  

4.  Voer in het dialoog venster **Eigenschappen van nieuwe sjabloon** , op het tabblad **Algemeen** , de naam van een sjabloon in, zoals **ConfigMgr-client distributiepunt certificaat**, om het client verificatie certificaat voor distributie punten te genereren.  

5.  Kies het tabblad **afhandeling van aanvragen** en kies vervolgens de optie **persoonlijke sleutel exporteren toestaan**.  

6.  Kies het tabblad **beveiliging** en verwijder de machtiging **Inschrijven** uit de beveiligings groep **ondernemings Administrators** .  

7.  Klik op **toevoegen**, Voer **ConfigMgr IIS-servers** in het tekstvak in en kies vervolgens **OK**.  

8.  Selecteer de machtiging **Inschrijven** voor deze groep en verwijder de machtiging **lezen** niet.  

9. Kies **OK**en sluit de **console certificaat sjablonen**.  

10. Klik in de certificerings instantie console met de rechter muisknop op **certificaat sjablonen**, kies **Nieuw**en kies vervolgens **te verlenen certificaat sjablonen**.  

11. Kies in het dialoog venster **certificaat sjablonen inschakelen** de nieuwe sjabloon die u zojuist hebt gemaakt, **ConfigMgr-client distributiepunt certificaat**, en kies vervolgens **OK**.  

12. Sluit de **certificerings instantie**als u geen certificaten meer moet maken en verlenen.  

###  <a name="request-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a>Het aangepaste certificaat voor verificatie van werk station aanvragen  
 Met deze procedure vraagt u het aangepaste client certificaat aan en installeert u het op de lidserver die IIS uitvoert en die wordt ingesteld als een distributie punt.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Het aangepaste certificaat voor verificatie van werkstation aanvragen  

1.  Kies **Start**, kies **uitvoeren**en voer vervolgens **MMC. exe in.** Kies in de lege console **bestand**en kies vervolgens **module toevoegen/verwijderen**.  

2.  Kies in het dialoog venster **modules toevoegen of verwijderen** de optie **certificaten** in de lijst met **beschik bare**modules en kies vervolgens **toevoegen**.  

3.  Kies **computer account**in het dialoog venster **certificaat module** en kies **volgende**.  

4.  Zorg er in het dialoog venster **computer selecteren** **voor dat lokale computer: (de computer waarop deze console wordt uitgevoerd)** is geselecteerd en kies vervolgens **volt ooien**.  

5.  Kies **OK**in het dialoog venster **modules toevoegen of verwijderen** .  

6.  Vouw **certificaten (lokale computer)** uit in de console en kies vervolgens **persoonlijk**.  

7.  Klik met de rechter muisknop op **certificaten**, kies **alle taken**en kies vervolgens **Nieuw certificaat aanvragen**.  

8.  Klik op de pagina **voordat u begint** op **volgende**.  

9. Als u de pagina certificaatinschrijvingsbeleid **selecteren** ziet, kiest u **volgende**.  

10. Kies op de pagina **certificaten aanvragen** het **ConfigMgr-client distributiepunt certificaat** in de lijst met beschik bare certificaten en kies vervolgens **registreren**.  

11. Wacht tot het certificaat is geïnstalleerd op de pagina **resultaten van installatie van certificaten** en kies vervolgens **volt ooien**.  

12. Bevestig in het resultaten venster dat een certificaat **client verificatie** heeft in de kolom **beoogd doel einde** en dat het **certificaat van ConfigMgr-client distributie punt** zich in de kolom **certificaat sjabloon** bevindt.  

13. **Certificaten (lokale computer)** niet sluiten.  

###  <a name="export-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a>Het client certificaat voor distributie punten exporteren  
 Met deze procedure exporteert u het aangepaste certificaat voor verificatie van werk station naar een bestand zodat het kan worden geïmporteerd in de eigenschappen van het distributie punt.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Exporteren van het clientcertificaat voor distributiepunten  

1. Klik in de console **certificaten (lokale computer)** met de rechter muisknop op het certificaat dat u zojuist hebt geïnstalleerd, kies **alle taken**en kies **exporteren**.  

2. Klik in de wizard certificaten exporteren op **volgende**.  

3. Kies op de pagina **persoonlijke sleutel exporteren** **de optie Ja, de persoonlijke sleutel exporteren**en klik vervolgens op **volgende**.  

   > [!NOTE]  
   >  Als deze optie niet beschikbaar is, is het certificaat gemaakt zonder de optie om de persoonlijke sleutel te exporteren. In dit scenario kunt u het certificaat niet exporteren in de vereiste indeling. U moet de certificaat sjabloon zo instellen dat de persoonlijke sleutel kan worden geëxporteerd en het certificaat vervolgens opnieuw aanvragen.  

4. Zorg ervoor dat op de pagina **bestands indeling voor export** de **Personal Information Exchange-PKCS #12 (. PFX)** is geselecteerd.  

5. Geef op de pagina **wacht** woord een sterk wacht woord op om het geëxporteerde certificaat met de persoonlijke sleutel te beveiligen en klik vervolgens op **volgende**.  

6. Geef op de pagina **te exporteren bestand** de naam op van het bestand dat u wilt exporteren en klik vervolgens op **volgende**.  

7. Klik op de pagina **wizard Certificaat exporteren** op **volt ooien** om de wizard te sluiten en kies **OK** in het bevestigings venster.  

8. Sluit **Certificaten (lokale computer)**.  

9. Sla het bestand veilig op en zorg ervoor dat u het kunt openen vanuit de Configuration Manager-console.  

   Het certificaat is nu klaar om te worden geïmporteerd wanneer u het distributie punt instelt.  

> [!TIP]  
>  U kunt hetzelfde certificaat bestand gebruiken bij het instellen van media kopieën voor een implementatie van een besturings systeem dat geen gebruik maakt van PXE-opstart bewerking en de taken reeks voor het installeren van de installatie kopie moet contact opnemen met een beheer punt waarvoor HTTPS-client verbindingen zijn vereist.  

##  <a name="deploy-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a>Het certificaat voor inschrijving voor mobiele apparaten implementeren  
 Voor deze certificaatimplementatie wordt een enkele procedure gebruikt om het certificaatsjabloon voor inschrijving te maken en het te publiceren bij de certificeringsinstantie.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Maken en publiceren van het certificaat sjabloon voor inschrijving bij de certificerings instantie  
 Met deze procedure maakt u een certificaat sjabloon voor inschrijving voor Configuration Manager mobiele apparaten en voegt u deze toe aan de certificerings instantie.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Maken en publiceren van het certificaatsjabloon voor inschrijving bij de certificeringsinstantie  

1. Maak een beveiligings groep met gebruikers die mobiele apparaten registreren in Configuration Manager.  

2. Klik met de rechter muisknop op **certificaat sjablonen**op de lidserver waarop de Certificate Services zijn geïnstalleerd en klik vervolgens op **beheren** om de beheer console voor certificaat sjablonen te laden.  

3. Klik in het resultaten venster met de rechter muisknop op het item met de **geauthenticeerde sessie** in de kolom **weergave naam van sjabloon** en kies **sjabloon dupliceren**.  

4. Zorg er in het dialoog venster **sjabloon dupliceren** voor dat **Windows 2003 server, Enter prise Edition** is geselecteerd, en kies vervolgens **OK**.  

   > [!IMPORTANT]  
   >  **Windows 2008 Server, Enterprise Edition** niet selecteren.  

5. Voer in het dialoog venster **Eigenschappen van nieuwe sjabloon** , op het tabblad **Algemeen** , de naam van een sjabloon in, zoals **ConfigMgr-certificaat voor inschrijving van mobiele**apparaten, om de inschrijvings certificaten te genereren voor de mobiele apparaten die worden beheerd door Configuration Manager.  

6. Kies het **tabblad onderwerpnaam** , zorg ervoor dat **op basis van deze Active Directory informatie** is geselecteerd, **Selecteer algemene naam** voor de indeling van de **onderwerpnaam:** en verwijder vervolgens **UPN-naam (User Principal Name)** uit **deze informatie in alternatieve onderwerpnaam toevoegen**.  

7. Kies het tabblad **beveiliging** , kies de beveiligings groep met gebruikers die mobiele apparaten hebben die moeten worden inge schreven, en kies vervolgens de extra machtiging voor **registreren**. **Lezen**niet wissen.  

8. Kies **OK**en sluit de **console certificaat sjablonen**.  

9. Klik in de certificerings instantie console met de rechter muisknop op **certificaat sjablonen**, kies **Nieuw**en kies vervolgens **te verlenen certificaat sjablonen**.  

10. Kies in het dialoog venster **certificaat sjablonen inschakelen** de nieuwe sjabloon die u zojuist hebt gemaakt, **ConfigMgr-certificaat voor inschrijving van mobiele apparaten**en kies vervolgens **OK**.  

11. Sluit de console certificerings instantie als u geen certificaten meer hoeft te maken en verlenen.  

    Het certificaat sjabloon voor inschrijving van mobiele apparaten is nu klaar om te worden geselecteerd wanneer u een inschrijvings profiel voor mobiele apparaten instelt in de client instellingen.  

##  <a name="deploy-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a>Het client certificaat voor Mac-computers implementeren  

Voor deze certificaatimplementatie wordt een enkele procedure gebruikt om het certificaatsjabloon voor inschrijving te maken en het te publiceren bij de certificeringsinstantie.  

###  <a name="create-and-issue-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a>Een sjabloon voor een Mac-client certificaat maken en uitgeven voor de certificerings instantie  
 Met deze procedure maakt u een aangepast certificaat sjabloon voor Configuration Manager Mac-computers en voegt u het certificaat sjabloon toe aan de certificerings instantie.  

> [!NOTE]  
>  Met deze procedure gebruikt u een ander certificaatsjabloon dan het certificaatsjabloon dat u mogelijk hebt gemaakt voor Windows-clientcomputers of voor distributiepunten.  
>   
>  Wanneer u een nieuw certificaat sjabloon maakt voor dit certificaat, kunt u de certificaat aanvraag beperken tot gemachtigde gebruikers.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>De Mac-clientcertificaatsjabloon maken en bij de certificeringsinstantie indienen  

1. Maak een beveiligings groep met gebruikers accounts voor gebruikers met beheerders rechten die het certificaat registreren op de Mac-computer door gebruik te maken van Configuration Manager.  

2. Klik met de rechter muisknop op **certificaat sjablonen**op de lidserver waarop de certificerings instantie console wordt uitgevoerd en kies vervolgens **beheren** om de beheer console voor certificaat sjablonen te laden.  

3. Klik in het resultaten venster met de rechter muisknop op het item dat **geverifieerde sessie** weergeeft in de kolom **weergave naam van sjabloon** en kies **sjabloon dupliceren**.  

4. Zorg er in het dialoog venster **sjabloon dupliceren** voor dat **Windows 2003 server, Enter prise Edition** is geselecteerd, en kies vervolgens **OK**.  

   > [!IMPORTANT]  
   >  **Windows 2008 Server, Enterprise Edition** niet selecteren.  

5. Voer in het dialoog venster **Eigenschappen van nieuwe sjabloon** , op het tabblad **Algemeen** , de naam van een sjabloon in, zoals **ConfigMgr Mac-client certificaat**, om het Mac-client certificaat te genereren.  

6. Kies het **tabblad onderwerpnaam** , zorg ervoor dat **op basis van deze Active Directory informatie** is geselecteerd, **Kies algemene naam** voor de indeling van de **onderwerpnaam:** en verwijder vervolgens **UPN-naam (User Principal Name)** uit **deze informatie in alternatieve onderwerpnaam toevoegen**.  

7. Kies het tabblad **beveiliging** en verwijder de machtiging **Inschrijven** uit de beveiligings groepen **domein Administrators** en **ondernemings Administrators** .  

8. Klik op **toevoegen**, geef de beveiligings groep op die u in stap 1 hebt gemaakt en kies vervolgens **OK**.  

9. Kies de machtiging **Inschrijven** voor deze groep en verwijder de machtiging **lezen** niet.  

10. Kies **OK**en sluit de **console certificaat sjablonen**.  

11. Klik in de certificerings instantie console met de rechter muisknop op **certificaat sjablonen**, kies **Nieuw**en kies vervolgens **te verlenen certificaat sjablonen**.  

12. Kies in het dialoog venster **certificaat sjablonen inschakelen** de nieuwe sjabloon die u zojuist hebt gemaakt, **ConfigMgr Mac-client certificaat**en kies vervolgens **OK**.  

13. Sluit de **certificerings instantie**als u geen certificaten meer moet maken en verlenen.  

    De sjabloon voor het Mac-client certificaat is nu gereed om te worden geselecteerd wanneer u client instellingen voor inschrijving instelt.
