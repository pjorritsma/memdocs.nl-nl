---
title: Mogelijkheden van Technical Preview 1604
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1604.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1785880af8c7d0d106abfe3eea8ecd390f6ce6b1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074449"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1604 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1604. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site.      Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.  

 Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a>Apps die zijn gekocht via het volume-aankoop programma beheren vanuit Windows Store voor bedrijven  
 In de [Windows Store voor bedrijven](https://www.microsoft.com/business-store) kunt u apps zoeken en kopen voor uw organisatie, afzonderlijk of op volume. Als u de Store verbindt met Configuration Manager, kunt u apps die zijn gekocht via het volume-aankoop programma beheren via de Configuration Manager-console, bijvoorbeeld:  

-   U kunt de lijst met aangeschafte apps synchroniseren met Configuration Manager  

-   Apps die zijn gesynchroniseerd, worden weer gegeven in de Configuration Manager-console en u kunt deze op dezelfde manier implementeren als andere apps  

-   U kunt bijhouden hoeveel licenties er beschikbaar zijn en hoeveel er worden gebruikt in de Configuration Manager-console  

### <a name="try-it-out"></a>Probeer het nu!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Scenario 1: Windows Store voor bedrijven-synchronisatie instellen  

1.  Registreer Configuration Manager in Azure Active Directory als een hulp programma voor het beheer van webtoepassingen en/of Web-API. Hiermee krijgt u een client-ID die u later nodig hebt.  

    1.  Selecteer uw **Active Directory** Azure Active Directory in het [https://manage.windowsazure.com](https://manage.windowsazure.com)knoop punt Active Directory van en klik vervolgens op **toepassingen** > **toevoegen**.  

    2.  Klik op **een toepassing toevoegen die mijn organisatie ontwikkelt**.  

    3.  Voer een naam in voor de toepassing, selecteer **Webtoepassing** en/of **Web-API**en klik op de pijl Volgende.  

    4.  Voer dezelfde URL in voor zowel de **aanmeldings-URL** als de **URI van de App-ID**.  De URL kan iets zijn en hoeft niet te worden omgezet naar een echt adres. U kunt bijvoorbeeld **&lt;https://domein\>-/SCCM**invoeren.  

    5.  Voltooi de wizard.  

2.  In Azure Active Directory maakt u een client sleutel voor het geregistreerde beheer programma.  

    1.  Markeer de toepassing die u zojuist hebt gemaakt en klik op **configureren**.  

    2.  Onder **sleutels**selecteert u een duur in de lijst en klikt u op **Opslaan**.  Hiermee wordt een nieuwe client sleutel gemaakt.  Verlaat deze pagina pas als u Windows Store voor bedrijven hebt gerepareerd naar Configuration Manager.  

3.  Configureer in de Windows Store voor bedrijven Configuration Manager als het hulp programma voor het beheer van opslag.  

    1.  Open [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) en meld u aan als u hierom wordt gevraagd.  

    2.  Accepteer de gebruiks voorwaarden, indien nodig.  

    3.  Klik onder **beheer hulpprogramma's**op **een beheer programma toevoegen**.  

    4.  Typ in **zoeken naar het hulp programma op naam**de naam van de toepassing die u eerder hebt gemaakt in Aad en klik vervolgens op **toevoegen**.  

    5.  Klik op **activeren** naast de toepassing die u zojuist hebt geïmporteerd.  

    6.  Klik in de wizard **apps met offline licenties weer geven** op **Ja** als u wilt toestaan dat toepassingen met een offline licentie worden gekocht.  

4.  Koop ten minste één app vanuit Windows Store voor bedrijven.  

5.  Vouw in de werk ruimte **beheer** van de Configuration Manager-console **Cloud Services**uit en klik vervolgens op **Windows Store voor bedrijven**.  

6.  Klik op het tabblad **Start** in de groep **maken** op **Windows Store voor bedrijven-account toevoegen**.  

7.  Voeg uw Tenant-ID, client-id en client sleutel van Azure Active Directory toe en voltooi vervolgens de wizard.  

8.  Wanneer u klaar bent, ziet u het account dat u hebt geconfigureerd in de lijst met **Windows Store voor bedrijven-accounts** in de Configuration Manager-console.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Scenario 2: een Configuration Manager-toepassing maken en implementeren vanuit een Windows Store voor bedrijven-app met een offline licentie  

1.  Vouw in de werk ruimte **software bibliotheek** van de Configuration Manager-console het knoop punt **toepassings beheer**uit en klik vervolgens op **licentie-informatie voor Store-apps**.  

2.  De lijst met **aangeschafte apps van Windows Store voor bedrijven** bevat een lijst met apps die zijn gesynchroniseerd vanuit de Store. Kies de app die u wilt implementeren en klik vervolgens op het tabblad **Start** in de groep **maken** op **toepassing maken**.  

3.  Er wordt een Configuration Manager-toepassing gemaakt met daarin de app Windows Store voor bedrijven. U kunt deze toepassing vervolgens implementeren en bewaken op dezelfde manier als andere Configuration Manager-toepassingen.  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a>Verbeteringen aan Microsoft Passport for Work beheer  
 U kunt nu Pass Port for Work-beleid implementeren voor Windows 10-apparaten die zijn toegevoegd aan een domein en die worden beheerd door de Configuration Manager-client.  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a>Optie voor clients om over te scha kelen naar een nieuw software-update punt  
 In de 1604 Technical Preview kunt u de optie inschakelen om Configuration Manager-clients over te scha kelen naar een nieuw software-update punt wanneer er problemen zijn met het actieve software-update punt. Voor deze optie moet u meerdere software-update punten beschikbaar hebben op een primaire site. Als u deze optie inschakelt op een apparaat, en eenmaal is ingeschakeld, zoeken de clients in de verzameling naar een ander software-update punt bij de volgende scan wanneer de client geen verbinding kan maken met het actieve software-update punt. Afhankelijk van de configuratie-instellingen van uw WSUS (update classificaties, producten, enzovoort), wordt door de switch naar een nieuw software-update punt extra netwerk verkeer gegenereerd. Gebruik deze optie daarom alleen wanneer dat nodig is.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>De optie inschakelen om van software-updatepunt te wisselen  

1.  Klik in de Configuration Manager-console op **Activa en naleving > Overzicht > Apparaatverzamelingen**.  

2.  Klik op het tabblad **Start** in de groep **Verzameling** op **Clientmelding** en klik vervolgens op **Overschakelen naar het volgende software-updatepunt**.  

> [!NOTE]  
>  Deze optie is alleen beschikbaar op sites met meerdere software-update punten.  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a>Client instellingen voor het beheren van de client cache-instellingen en client-peer-cache  
 Technical Preview versie 1604 introduceert twee nieuwe client instellingen voor apparaten die van invloed zijn op het gebruik van de cache van een client. Beide kunnen afzonderlijk worden gebruikt, maar worden geconfigureerd op hetzelfde eigenschappen blad voor client instellingen en combi neren om u te helpen bij het beheren van de implementatie van inhoud naar uw clients op externe locaties.  

-   Eerste is **client-peer-cache**, een ingebouwde Configuration Manager oplossing voor clients om inhoud rechtstreeks vanuit hun lokale cache te delen met andere clients. Als peer-cache-clients inhoud willen delen, moeten ze lid zijn van dezelfde grens groep. Peer-cache vervangt niet het gebruik van andere oplossingen, zoals BracnchCache, maar werkt naast elkaar om meer opties te bieden voor het uitbreiden van traditionele oplossingen voor inhouds implementatie, zoals distributie punten.  

     Nadat u client instellingen hebt geïmplementeerd waarmee peer-cache voor een verzameling wordt ingeschakeld, kunnen leden van die verzameling fungeren als een peer-inhouds bron voor andere clients in de grens groep.  De client die als peer-inhouds bron fungeert, verzendt een lijst met beschik bare inhoud die in de cache is opgeslagen op het beheer punt. Wanneer de volgende client in die grens groep die inhoud aanvraagt, wordt de bron van de peer-cache aangeboden als een potentiële inhouds bron samen met alle distributie punten die zijn geconfigureerd om snel te worden. De client selecteert een wille keurige inhouds bron uit deze gecombineerde groep met inhouds bronnen. Clients zoeken alleen inhoud van een distributie punt dat is geconfigureerd om traag te zijn wanneer er geen snelle distributie punten of peer-cache bronnen aanwezig zijn in de grens groep.  

-   Met de tweede nieuwe instelling kunt u **de grootte van de cache** op clients beheren. U kunt instellen dat de cache een maximale grootte in mega bytes heeft en een maximale grootte als percentage van de schijf ruimte van de clients.  De-client dwingt de instelling af die het eerst wordt bereikt.  

Om het gebruik van client-peer-cache te begrijpen, kunt u het dash board **client gegevens bronnen** weer geven. Ga in de-console naar **bewaking > client Status > client-gegevens bronnen**. Hier kunt u een periode selecteren die u wilt Toep assen op het dash board. In de weer gave kunt u vervolgens de grens groep of het pakket selecteren waarvoor u informatie wilt weer geven. Bij het weer geven van informatie kunt u de muis aanwijzer op het Opper vlak aanwijzen om meer informatie over de verschillende inhoud of beleids bronnen weer te geven.  

 U kunt ook een nieuw rapport, **gegevens bronnen van de client-samen vatting**, gebruiken om een samen vatting van de client gegevens bronnen voor elke grens groep weer te geven.   
**Vereisten voor het gebruik van peer-cache:**  

-   U moet uw site configureren met een **netwerk toegangs account** met **volledige controle** over de cachemap op elke client. Standaard is dit **%windir%\ccmcache**  

-   Clients kunnen alleen inhoud overdragen met behulp van peer-cache wanneer ze lid zijn van dezelfde grens groep.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Instellingen voor client peer cache-client configureren  

1.  Beide instellingen worden geconfigureerd op dezelfde pagina van client instellingen. Ga in de Configuration Manager-console naar **beheer > client instellingen**en open vervolgens het object voor client instellingen voor apparaten dat u wilt gebruiken. U kunt ook het standaard object voor client instellingen wijzigen.  

2.  Selecteer in de lijst met beschik bare instellingen de instellingen voor de **client cache**.  

3.  Als u de grootte van de cache wilt beheren, stelt u de **cache grootte** voor de client in op **Ja**. Vervolgens kunt u de maximale cache grootte voor zowel mega bytes als een percentage van de schijf ruimte van de clients configureren.  

4.  Als u wilt dat clients kunnen deel nemen aan client-peer-cache, stelt u **Configuration Manager client in volledig besturings systeem in om inhoud** gelijk aan **Ja**te kunnen delen. U kunt vervolgens de poorten configureren die clients gebruiken, inclusief als ze HTTP of HTTPS zijn.  

### <a name="try-it-out"></a>Probeer het nu!  
 Voer de volgende taken uit en gebruik daarna de feedback informatie boven aan dit onderwerp om ons te laten weten hoe het werkt:  

1.  Wijzig de client instellingen om een nieuwe grootte op te geven voor de client cache en bevestig deze instelling op een client.  

2.  Client instellingen gebruiken om meerdere clients te configureren voor het gebruik van peer-cache  

3.  Implementeer inhoud op clients zodat sommige of de meeste clients die inhoud van een andere client ophalen met behulp van peer-cache.  U kunt de inhouds bron bevestigen die wordt gebruikt door het nieuwe dash board weer te geven.  

    > [!NOTE]  
    >  Als u deze taak wilt volt ooien met de technische preview-versie en een enkel distributie punt, configureert u het distributie punt voor de netwerk locatie van al uw clients. Distribueer de inhoud vervolgens naar één client.  Nadat de-client de inhoud heeft opgehaald, kunt u de inhoud distribueren naar extra clients die lokale peers moeten vinden om te gebruiken als inhouds bron voordat u het distributie punt gebruikt dat wordt beschouwd als langzaam van de locatie van de client.  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a>Ondersteuning voor Pass Port for Work als een SLEUTELARCHIEFPROVIDER  
 Met Configuration Manager kunt u integreren met Microsoft Passport for Work die een alternatieve aanmeldings methode is waarbij Active Directory of een Azure Active Directory-account wordt gebruikt om een wacht woord, Smart Card of virtuele Smart Card te vervangen.  
Met pass Port kunt u een gebruikers beweging gebruiken om u aan te melden in plaats van een wacht woord. Een gebaar van de gebruiker kan een eenvoudige pincode zijn, biometrische verificatie zoals Windows Hello of een extern apparaat zoals een vingerafdruklezer.  

-   U kunt Configuration Manager gebruiken om te bepalen welke gebaren gebruikers wel en niet kunnen gebruiken om zich aan te melden en om complexiteits vereisten voor PINCODEs te configureren.  

-   U kunt verificatiecertificaten opslaan in de sleutelarchiefprovider (KSP) van Passport for Work.  

Wanneer een gebruiker een Pass Port-pincode maakt, stuurt Windows een melding dat Configuration Manager luistert naar.  Hiermee kan Configuration Manager snel worden geweet welke gebruikers een Pass Port-pincode hebben gemaakt. Configuration Manager kunt vervolgens ook nieuwe certificaten aan deze gebruikers verzenden als Pass Port als de sleutelarchiefprovider wordt gebruikt in een certificaat profiel.  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a>On-premises Apparaatstatusverklaring  
 Health Attestation voor Windows 10-apparaten kan nu worden geconfigureerd om te communiceren met behulp van de on-premises infra structuur.  Beheerders kunnen opgeven of rapportage plaatsvindt via de Cloud of on-premises resources.  Als **on-premises** is geselecteerd voor Health Attestation-rapportage, kan een URI worden opgegeven voor de service. Hierdoor kunnen client-Pc's zonder Internet toegang apparaten inschakelen en beheren met Health Attestation.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Status verklaring inschakelen voor on-premises apparaten  

1.  Navigeer in de Configuration Manager-console naar **beheer** > **overzicht** > **client instellingen**en stel **on-premises goed werkende Attestation-service gebruiken** in op **Ja**.  

2.  Geef de **URL op voor de on-premises statusverklaringsservice**en klik op **OK**.  

Als u dit wilt uitproberen, configureert u de on-premises Health Attestation-service met de instellingen van de client agent.  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a>Smart Lock-instelling voor Android-apparaten  
 Een nieuwe instelling, **toestaan dat Smart Lock en andere vertrouwde agents** zijn toegevoegd aan het **Android-en Samsung KNOX** -configuratie-item waarmee u de Smart Lock-functie op compatibele Android-apparaten kunt beheren. Met deze telefoonmogelijkheid (soms ook wel vertrouwde agent genoemd) kunt u het vergrendelingsschermwachtwoord op het apparaat uitschakelen of overslaan als het zich op een vertrouwde locatie bevindt, zoals wanneer het is verboden met een bepaald Bluetooth-apparaat, of wanneer het zich in de buurt bevindt van een NFC-tag. U kunt deze instelling gebruiken om te voor komen dat eind gebruikers Smart Lock configureren.  
