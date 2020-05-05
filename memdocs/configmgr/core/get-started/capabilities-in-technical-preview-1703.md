---
title: Mogelijkheden van Technical Preview 1703
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1703.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d06bda9d07a53e022de27afc68f40f9ce706867f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076149"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1703 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1703. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Door het volume gekochte iOS-Apps implementeren in apparaat verzamelingen

U kunt nu gelicentieerde Apps implementeren op apparaten en gebruikers. Afhankelijk van de mogelijkheden van de apps om de ondersteuning van een apparaat te ondersteunen, wordt een geschikte licentie gevraagd wanneer u deze implementeert, als volgt:

|||||
|-|-|-|-|
|Configuration Manager versie|App ondersteunt apparaat-licenties?|Type implementatie verzameling|Geclaimde licentie|
|Ouder dan 1702|Ja|Gebruiker|Gebruikers licentie|
|Ouder dan 1702|Nee|Gebruiker|Gebruikers licentie|
|Ouder dan 1702|Ja|Apparaat|Gebruikers licentie|
|Ouder dan 1702|Nee|Apparaat|Gebruikers licentie|
|1702 en hoger|Ja|Gebruiker|Gebruikers licentie|
|1702 en hoger|Nee|Gebruiker|Gebruikers licentie|
|1702 en hoger|Ja|Apparaat|Apparaatlicentie|
|1702 en hoger|Nee|Apparaat|Gebruikers licentie|


## <a name="direct-links-to-applications-in-software-center"></a>Directe koppelingen naar toepassingen in Software Center

U kunt eind gebruikers nu voorzien van een directe koppeling naar een toepassing in Software Center. Dit betekent dat ze software Center niet meer hoeven te openen en te zoeken naar een toepassing voordat ze deze kunnen installeren. Dit is alleen beschikbaar voor Configuration Manager toepassingen, niet voor pakketten en Program ma's of taken reeksen.

### <a name="try-it-out"></a>Uitproberen                 

Gebruik de volgende URL-indeling om software Center te openen voor een bepaalde toepassing:

**Softwarecenter: SoftwareId =_toepassings-id_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>De toepassings-id van een toepassing ophalen.

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.
2. In de werkruimte Softwarebibliotheek vouwt u **Toepassingsbeheer**uit en klikt u op **Toepassingen**.
3. Klik in de weer gave **toepassingen** met de rechter muisknop op een van de kolom koppen en selecteer vervolgens in de lijst **CI-unieke id**. U ziet dat de unieke ID van elke toepassing nu wordt weer gegeven in de lijst.
4. Noteer de **CI-id** van de toepassing waarvoor u een koppeling wilt opgeven, bijvoorbeeld: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5. Verwijder vervolgens alle tekst na de GUID van de toepassing, in dit geval **/2**. Hiermee verlaat u de toepassings-id.
6. Ten slotte kunt u het bouwen van de koppeling volt ooien door **Softwarecenter: SoftwareID =**. Met het bovenstaande voor beeld wordt de laatste koppeling gelezen: **Softwarecenter: SoftwareId = ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Met deze koppeling kunnen eind gebruikers software Center rechtstreeks openen in de toepassing die u hebt opgegeven.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>PFX-certificaten voor Configuration Manager Windows-client computers

U kunt nu PFX-certificaat profielen implementeren die u hebt geïmporteerd op Configuration Manager-client computers met Windows 10.

### <a name="try-it-out"></a>Uitproberen

Volg de instructies in [PFX-certificaat profielen maken](../../mdm/deploy-use/create-pfx-certificate-profiles.md) om een pfx-profiel te importeren, het profiel te implementeren en vervolgens te controleren of het certificaat is geïnstalleerd voor de doel gebruiker.



## <a name="configure-azure-services-wizard"></a>Wizard Azure-Services configureren
Technical Preview 1703 introduceert de wizard **Azure-Services configureren** . Deze wizard biedt een algemene configuratie-ervaring waarmee de afzonderlijke werk stromen worden vervangen voor het instellen van de Cloud Services die u gebruikt met Configuration Manager. Dit doet u door een **Azure-web-app** te gebruiken om het abonnement en de configuratie gegevens op te geven die u op een andere manier invoert, telkens wanneer u een nieuw Configuration Manager onderdeel of service met Azure instelt.

Met Technical Preview 1703 wordt alleen Windows Store voor bedrijven (WSfB) geconfigureerd met behulp van deze wizard.  Andere Cloud Services worden geconfigureerd met behulp van hun afzonderlijke werk stromen.

- Gebruik de informatie in dit voor beeld om de configuratie stappen te vervangen die zijn gevonden in de sectie [Windows Store voor bedrijven-synchronisatie instellen](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup) van het current branch onderwerp [apps beheren vanuit Windows Store voor bedrijven met Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

- Zie [verificatie en autorisatie in azure app service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)en [Web apps overzicht](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)voor meer informatie over web-apps.

### <a name="prerequisites-and-planning"></a>Vereisten en planning
Wanneer u een verbinding instelt tussen Configuration Manager en Windows Store voor bedrijven, moet u een map opgeven waarin app-inhoud uit de Store wordt gesynchroniseerd. Om ervoor te zorgen dat deze map beveiligd is en dat de inhoud ervan kan worden geïmplementeerd op apparaten, moet u ervoor zorgen dat de volgende machtigingen aanwezig zijn:
- De computer waarop u de site systeemrol voor het service aansluitpunt installeert (de site op het hoogste niveau in de hiërarchie) moet lees-en schrijf machtigingen hebben voor de map die u hebt opgegeven bij het gebruik van de **computer $** -account.  

- De auteur van de app moet Lees machtigingen hebben voor de map die u hebt opgegeven.  

- De **computer** account van elke computer die als host fungeert voor een exemplaar van de SMS-provider moet de door u opgegeven map kunnen gebruiken.

Registreer Configuration Manager in Azure Active Directory als webtoepassing of Web API Management-hulp programma. Hiermee maakt u de client-ID die u later nodig hebt.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Gebruik de wizard voor het configureren van de WSfB-Cloud service

1. Ga in de-console naar **beheer** > **overzicht** > **Cloud Services Management** > **Azure** > **Azure-Services**en kies vervolgens **Azure-Services configureren** om de **wizard Azure-Services**te starten.

2. Selecteer op de pagina **Azure-Services** de service die u wilt configureren en klik vervolgens op **volgende**. Met deze preview-versie kan alleen WSfB worden geconfigureerd.

3. Geef op de pagina **Algemeen** een beschrijvende naam op voor de **naam** van de Azure-service en een optionele beschrijving en klik vervolgens op **volgende**.

4. Geef uw Azure-omgeving op de pagina **app** op en klik vervolgens op **Bladeren** om het venster Server toepassing te openen.

5. Selecteer in het venster van de **server-app** de server-app die u wilt gebruiken en klik vervolgens op **OK**.
   Server-apps zijn de Azure-web-apps die de configuraties voor uw Azure-account bevatten, inclusief uw Tenant-ID, client-ID en een geheime sleutel voor clients. Als er geen beschik bare server-app is, gebruikt u een van de volgende opties:
   - **Maken**: als u een nieuwe server-app wilt maken, klikt u op **maken**. Geef een beschrijvende naam op voor de app en de Tenant. Nadat u zich hebt aangemeld bij Azure, maakt Configuration Manager de web-app in azure voor u, met inbegrip van de client-ID en de geheime sleutel voor gebruik met de web-app. Later kunt u deze bekijken in de Azure Portal.
   - **Importeren**: als u een web-app wilt gebruiken die al in uw Azure-abonnement bestaat, klikt u op **importeren**. Geef een beschrijvende naam op voor de app en de Tenant, en geef vervolgens de Tenant-ID, de client-ID en de geheime sleutel op voor de Azure-web-app die u Configuration Manager wilt gebruiken. Nadat u de informatie hebt **gecontroleerd** , klikt u op **OK** om door te gaan.  </br></br>

6. Bekijk de **informatie** pagina en voltooi eventuele extra stappen en configuraties. Deze configuraties zijn nodig voor het gebruik van de service met Configuration Manager.
   Bijvoorbeeld om WSfB te configureren:

   1. In azure moet u Configuration Manager registreren als webtoepassing of Web-API en de client-ID opnemen. U geeft ook een client sleutel op voor gebruik door het beheer programma (Configuration Manager).

   2.    In de WSfB-console moet u Configuration Manager configureren als het hulp programma voor het opslaan van een archief, ondersteuning inschakelen voor offline gelicentieerde apps en vervolgens ten minste één app aanschaffen.   </br>

   Klik op **volgende** wanneer u klaar bent om door te gaan.

7. Op de pagina **app-configuraties** voert u de app-catalogus en taal configuraties voor deze service uit en klikt u vervolgens op **volgende**.
8. Nadat de wizard is voltooid, ziet u in de Configuration Manager-console dat u **Windows Store voor bedrijven** hebt geconfigureerd als een **type Cloud service**.

U kunt nu de rest van de [Current Branch inhoud](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) voor het beheren van apps uit de WSfB gebruiken om Windows Store voor bedrijven-apps te synchroniseren, te maken en te implementeren en te bewaken.

### <a name="modify-a-cloud-service-configuration"></a>Een Cloud service configuratie wijzigen
U kunt de eigenschappen van een Cloud service weer geven en bewerken om de configuratie te wijzigen.

Ga in de-console naar **beheer** > **overzicht** > **Cloud Services beheer** > **Azure** > **Azure-Services**, en kies vervolgens **Azure-Services configureren**, selecteer een Cloud service en kies vervolgens **Eigenschappen**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversie van BIOS naar UEFI tijdens een in-place upgrade
In de update voor Windows 10 Crea tors wordt een eenvoudig conversie programma geïntroduceerd waarmee het proces voor het opnieuw partitioneren van de harde schijf voor UEFI-hardware wordt geautomatiseerd en het conversie programma wordt geïntegreerd in het Windows 7-in-place upgrade proces. Wanneer u dit hulp programma combineert met de taken reeks voor de upgrade van het besturings systeem en het OEM-hulp programma dat de firmware converteert van BIOS naar UEFI, kunt u uw computers converteren van BIOS naar UEFI tijdens een in-place upgrade naar de update voor Windows 10 Crea tors. Zie [taken reeks stappen voor het beheren van de conversie van BIOS naar UEFI](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade)voor meer informatie.

## <a name="collapsible-task-sequence-groups"></a>Samenvouw bare taken reeks groepen
Deze versie introduceert de mogelijkheid om taken reeks groepen uit te vouwen en samen te vouwen. U kunt afzonderlijke groepen uitvouwen of samen vouwen of alle groepen in één keer uitvouwen of samen vouwen.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Client instellingen voor het configureren van Windows Analytics voor Upgradegereedheid
Vanaf deze versie kunt u de client instellingen voor apparaten gebruiken om de configuratie te vereenvoudigen van de Windows diagnostische gegevens die nodig zijn voor het gebruik van Windows Analytics-oplossingen, zoals Upgradegereedheid met Configuration Manager. Configuration Manager kunt gegevens ophalen uit Windows Analytics die waardevolle inzichten kunnen bieden in de huidige status van uw omgeving op basis van de diagnostische gegevens van Windows die zijn gerapporteerd door uw client computers. Windows diagnostische gegevens worden gerapporteerd door client computers aan de Windows diagnostische service, en vervolgens worden de relevante gegevens overgebracht naar Windows Analytics-oplossingen die worden gehost in een van de OMS-werk ruimten van uw organisatie. Upgradegereedheid is een Windows Analytics-oplossing die u kan helpen bij het bepalen van beslissingen over Windows-upgrades voor uw beheerde apparaten.

### <a name="prerequisites"></a>Vereisten
- U moet uw site hebben geconfigureerd voor het gebruik van de Upgradegereedheid-Cloud service.

### <a name="configure-windows-analytics-client-settings"></a>Windows Analytics-client instellingen configureren
Als u Windows Analytics wilt configureren, gaat u in de Configuration Manager-console naar **beheer** > **client instellingen**en dubbelklikt u op **aangepaste client instellingen voor apparaten maken** en controleert u vervolgens **Windows Analytics**.  

Configureer vervolgens het volgende nadat u naar het tabblad instellingen van **Windows Analytics** hebt genavigeerd:
- **Commerciële ID**  
De commerciële ID-sleutel wijst informatie toe van apparaten die u beheert tot de OMS-werk ruimte die als host fungeert voor de Windows Analytics-gegevens van uw organisatie. Als u al een commerciële ID-sleutel hebt geconfigureerd voor gebruik met Upgradegereedheid, gebruikt u die ID. Als u nog geen commerciële ID-sleutel hebt, genereert u uw commerciële ID-sleutel.

- Een **niveau van diagnostische gegevens instellen voor Windows 10-apparaten**

- Kies voor het kiezen van **commerciële gegevens verzameling op Windows 7-, 8-en 8,1-apparaten**   

- **Gegevens verzameling via Internet verkennen configureren** Op apparaten met Windows 8,1 of eerder kan met gegevens verzameling in Internet Explorer Upgradegereedheid incompatibiliteiten met webtoepassingen worden gedetecteerd die een probleemloze upgrade naar Windows 10 kunnen voor komen. Het verzamelen van gegevens in Internet Explorer kan per Internet zone worden ingeschakeld.
