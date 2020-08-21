---
title: Mogelijkheden van Technical Preview 1702
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1702.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 7a4c42891276b36fd888f0f70495bdcd504f23a1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693009"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1702 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1702. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Feedback verzenden vanuit de Configuration Manager-console

In deze preview worden nieuwe feedback opties geïntroduceerd in de Configuration Manager-console. Met de feedback opties kunt u feedback rechtstreeks naar het ontwikkel team verzenden via de website van Configuration Manager UserVoice-feedback.  

> U kunt de volgende **feedback** optie vinden:
> -  In het lint helemaal links op het tabblad Start van elk knoop punt.  
>    ![Vaandel](./media/feedback-home.png)

-  Wanneer u met de rechter muisknop op een object in de-console klikt.   
    ![Recht: Klik op optie](./media/feedback-option.png)   

Als u **feedback** kiest, wordt uw browser geopend op de website van Configuration Manager UserVoice-feedback, op https://configurationmanager.uservoice.com/forums/300492-ideas .
##  <a name="changes-for-updates-and-servicing"></a>Wijzigingen voor updates en onderhoud
Het volgende is geïntroduceerd in deze preview-versie.

**Eenvoudigere Update opties**  
De volgende keer dat uw infra structuur in aanmerking komt voor twee of meer updates, wordt alleen de meest recente update gedownload. Als uw huidige site versie bijvoorbeeld twee of meer ouder is dan de meest recente versie die beschikbaar is, wordt alleen de meest recente update versie automatisch gedownload.  

U hebt de mogelijkheid om de andere beschik bare updates te downloaden en te installeren, zelfs als dit niet de meest recente versie is. Er wordt echter een waarschuwing weer gegeven dat de update is vervangen door een nieuwere versie. Als u een update wilt downloaden die *beschikbaar is om te downloaden*, selecteert u de update in de-console en klikt u vervolgens op **downloaden**.

**Verbeterde opschoning van oudere updates**   
We hebben een automatische opschoon functie toegevoegd waarmee overbodige down loads uit de map ' EasySetupPayload ' op de site server worden verwijderd.  


## <a name="peer-cache-improvements"></a>Verbeteringen in de peer-cache
Vanaf deze release weigert een peer-cache bron computer een aanvraag voor inhoud wanneer de bron computer van de peer-cache aan een van de volgende voor waarden voldoet:  
-  Bevindt zich in de modus voor laag accu niveau.
-  CPU-belasting overschrijdt 80% op het moment dat de inhoud wordt aangevraagd.
-  Schijf-I/O heeft een *AvgDiskQueueLength* die groter is dan 10.
-  Er zijn geen meer beschik bare verbindingen met de computer.   

U kunt deze instellingen configureren met behulp van de configuratie klasse van de client agent voor de functie peer source (*SMS_WinPEPeerCacheConfig*) wanneer u de Configuration Manager SDK gebruikt.

Wanneer de computer een aanvraag voor de inhoud weigert, blijft de aanvragende computer in de groep beschik bare inhouds bron locaties zoeken naar andere bronnen.   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a> Azure Active Directory Domain Services gebruiken om apparaten, gebruikers en groepen te beheren

Met deze technische preview-versie kunt u apparaten beheren die zijn gekoppeld aan een door Azure Active Directory (AD) Domain Services beheerd domein. U kunt ook apparaten, gebruikers en groepen in dat domein detecteren met verschillende Configuration Manager detectie methoden.

De technische preview-site infrastructuur,-clients en het Azure AD Domain Services domein moeten allemaal worden uitgevoerd in Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Configuration Manager instellen voor het gebruik van Azure AD
Als u Azure AD met Configuration Manager wilt gebruiken, hebt u het volgende nodig:
- Azure-abonnement.
- Azure AD met Domain Services (DS).
- Een Configuration Manager-site die wordt uitgevoerd op een virtuele Azure-machine die is gekoppeld aan uw Azure AD.
- Configuration Manager-clients die worden uitgevoerd in dezelfde Azure AD-omgeving.

Zie aan de [slag met Azure AD Domain Services](/azure/active-directory-domain-services/create-instance)voor het configureren van de Azure AD-domein service.

### <a name="discover-resources"></a>Resources ontdekken
Nadat u Configuration Manager hebt ingesteld om te worden uitgevoerd in azure AD, kunt u de volgende Active Directory detectie methoden gebruiken om te zoeken in azure AD voor resources:  
- Active Directory-systeemdetectie
- Detectie Active Directory-gebruiker
- Active Directory-groepdetectie  

Voor elke methode die u gebruikt, bewerkt u de LDAP-query om de Azure AD-OE-structuren te doorzoeken in plaats van de containers die gebruikelijk zijn voor on-premises Active Directory. Hiervoor moet u de query omleiden om uw Active Directory in uw Azure-abonnement te doorzoeken.  

In de volgende voor beelden wordt een Azure AD- *contoso.onmicrosoft.com*gebruikt:
- **Systeem detectie**   
  Met Azure AD worden apparaten onder de organisatie-eenheid **AADDC computers** opgeslagen.  Configureer het volgende:  
  - *LDAP://OU = AADDC computers, DC = contoso, DC = onmicrosoft, DC = com*  


- **Gebruikers detectie** AAD slaat gebruikers op onder de OE van **AADDC-gebruikers** .  Configureer het volgende:
  - *LDAP://OU = AADDC gebruikers, DC = contoso, DC = onmicrosoft, DC = com*


- **Groeps detectie**  
Azure AD heeft geen organisatie-eenheid waarin groepen worden opgeslagen. Gebruik in plaats daarvan dezelfde algemene structuur als het systeem of de gebruiker query's en configureer de LDAP-query zodanig dat deze verwijst naar de organisatie-eenheid die de groepen bevat die u wilt detecteren.

Zie het volgende voor meer informatie over Azure AD:  
- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds) op Azure.Microsoft.com.
- [Active Directory Domain Services documentatie](/azure/active-directory-domain-services) op docs.Microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Verbeteringen in nalevings beleid voor voorwaardelijke toegang

Een nieuwe regel voor nalevings beleid voor apparaten is beschikbaar om u te helpen bij het blok keren van de toegang tot bedrijfs bronnen die ondersteuning bieden voor voorwaardelijke toegang, wanneer gebruikers apps gebruiken die deel uitmaken van een niet-compatibele lijst met apps. De lijst met niet-compatibele apps kan worden gedefinieerd door de beheerder bij het toevoegen van de nieuwe compatibele regel- **apps die niet kunnen worden geïnstalleerd**. Voor deze regel moet de beheerder de naam van de **app**, de **App-ID**en de uitgever van de **app** (optioneel) invoeren bij het toevoegen van een app aan de lijst die niet aan de vereisten voldoet. Deze instelling is alleen van toepassing op iOS-en Android-apparaten.

Dit helpt organisaties bovendien bij het beperken van gegevens die worden gelekt via onbeveiligde apps en om te voor komen dat er veel gegevens worden verbruikt via bepaalde apps.

### <a name="try-it-out"></a>Probeer het eens

**Scenario:** Identificeer apps die mogelijk gegevens lekken veroorzaken door zakelijke gegevens buiten uw bedrijf te verzenden of die een buitensporig gegevens verbruik veroorzaken, en [Maak vervolgens een nalevings beleid voor voorwaardelijke toegang](../../mdm/understand/what-happened-to-hybrid.md) om deze apps toe te voegen aan de lijst met niet-compatibele apps. Hiermee blokkeert u de toegang tot bedrijfs bronnen die ondersteuning bieden voor voorwaardelijke toegang totdat de gebruiker de geblokkeerde app kan verwijderen.

## <a name="antimalware-client-version-alert"></a>Waarschuwing voor versie van antimalware-client
Met ingang van deze preview-versie biedt Configuration Manager Endpoint Protection een waarschuwing als meer dan 20% (standaard) van beheerde clients een verlopen versie van de antimalware-client (bijvoorbeeld Windows Defender of Endpoint Protection-client) gebruiken.

### <a name="try-it-out"></a>Probeer het eens
Zorg ervoor dat Endpoint Protection is ingeschakeld op alle bureau blad-en Server-clients met het beleid voor client instellingen. U kunt nu de **antimalware-client versie** en **Endpoint Protection implementatie status** weer geven door te gaan naar **activa en naleving**  >  **overzicht**  >  **apparaten**  >  **alle Desk tops en clients te leveren**. Als u wilt controleren op een waarschuwing, bekijkt u **waarschuwingen** in de werk ruimte **bewaking** . Als er meer dan 20% van beheerde clients een verlopen versie van de antimalware-software uitvoert, wordt de antimalware-client versie verouderde waarschuwing weer gegeven. Deze waarschuwing wordt niet weer gegeven op het tabblad **controle**  >  **overzicht** . Schakel software-updates voor antimalware-clients in om verlopen antimalware-clients bij te werken.

Als u het percentage wilt configureren waarmee de waarschuwing wordt gegenereerd, vouwt u **bewakings**  >  **waarschuwingen**  >  **alle waarschuwingen**uit, dubbelklikt u op **antimalware-clients verouderd** en wijzigt u de **waarschuwing voor het activeren als het percentage beheerde clients met een verouderde versie van de antimalware meer is dan de** optie.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Nalevings beoordeling voor Windows Update voor zakelijke updates
U kunt nu een update regel voor nalevings beleid configureren om een Windows Update voor bedrijfs evaluatie resultaat op te nemen als onderdeel van de evaluatie van voorwaardelijke toegang.
> [!IMPORTANT]
> U moet Windows 10 Insider preview build 15019 of hoger hebben om nalevings beoordeling te kunnen gebruiken voor Windows Update voor zakelijke updates.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Windows Update voor bedrijven toestaan om Windows 10-updates te beheren
Als u informatie over de nalevings beoordeling wilt verzamelen voor Windows Update voor zakelijke updates, gebruikt u de volgende procedure om de instelling van de client agent zodanig te configureren dat Windows Update voor bedrijven voor het beheren van Windows 10-updates expliciet wordt toegestaan.
1. Ga in de Configuration Manager-console naar **Administration**  >  **client instellingen**voor beheer.
2. Ga in de eigenschappen voor de client instellingen naar **software-updates**en selecteer **Ja** voor de instelling **Windows 10-updates beheren met Windows Update voor bedrijven** .

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Een nalevings beleid maken voor de evaluatie van Windows Update voor bedrijven
1. Ga in de Configuration Manager-console naar instellingen voor nalevings beleid voor **activa en naleving**  >  **Compliance Settings**  >  **Compliance policies**.
2. Klik op **nalevings beleid maken** of selecteer een bestaand nalevings beleid dat u wilt wijzigen.
3. Geef op de pagina algemeen een naam en beschrijving op, selecteer **nalevings regels voor apparaten die worden beheerd met de Configuration Manager-client**, stel de ernst van niet-naleving in voor rapportage en klik op **volgende**.
4. Selecteer op de pagina ondersteunde platforms de optie **Windows 10**en klik vervolgens op **volgende**.
5. Klik op de pagina regels op **Nieuw....** en vervolgens op voor **waarde** kiezen **vereisen Windows Update voor bedrijfs naleving**. De instelling **waarde** wordt automatisch ingesteld op **waar**.

Het nieuwe beleid wordt weergegeven in het knooppunt **Nalevingsbeleid** van de werkruimte **Activa en naleving**.

### <a name="deploy-a-compliance-policy"></a>Een nalevingsbeleid implementeren
1. Ga in de Configuration Manager-console naar instellingen voor de naleving van **assets en**naleving  >  **Compliance Settings**en klik vervolgens op **nalevings beleid**.
2. Klik op het tabblad **Start** in de groep **Implementatie** op **Implementeren**.
3. Klik in het dialoogvenster **Nalevingsbeleid implementeren** op **Bladeren** om de gebruikersverzameling te selecteren waarvoor het beleid moet worden geïmplementeerd.
   Verder kunt u opties selecteren om waarschuwingen te genereren als het beleid niet compatibel is en ook om het schema te configureren waarmee dit beleid wordt beoordeeld op naleving.
4. Wanneer u klaar bent, klikt u op **OK**.

### <a name="monitor-the-compliance-policy"></a>Het nalevingsbeleid bewaken
Nadat u het nalevings beleid hebt gemaakt, kunt u de nalevings resultaten controleren in de Configuration Manager-console. Zie [het nalevings beleid bewaken](../../mdm/understand/what-happened-to-hybrid.md)voor meer informatie.


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Verbeteringen aan software Center-instellingen en meldings berichten voor taken reeksen met een hoge impact
Deze release bevat de volgende verbeteringen voor Software Center-instellingen en meldings berichten voor implementatie taken reeksen met een hoge impact:

- In de eigenschappen voor de taken reeks kunt u nu elke taken reeks configureren, inclusief niet-besturings systeem taken reeksen, als een implementatie met een hoog risico. Elke taken reeks die aan bepaalde voor waarden voldoet, wordt automatisch gedefinieerd als hoge impact. Zie [implementaties met een hoog risico beheren](../servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.
- In de eigenschappen voor de taken reeks kunt u kiezen of u het standaard meldings bericht wilt gebruiken of uw eigen aangepaste meldings bericht wilt maken voor implementaties met hoge impact.
- In de eigenschappen voor de taken reeks kunt u eigenschappen van software Center configureren, zoals het opnieuw opstarten vereist, de download grootte van de taken reeks en de geschatte uitvoerings tijd.
- In het standaard bericht van hoge impact voor in-place upgrades wordt nu aangegeven dat uw apps, gegevens en instellingen automatisch worden gemigreerd. Voorheen werd het standaard bericht voor een installatie van het besturings systeem aangegeven dat alle apps, gegevens en instellingen verloren zouden zijn gegaan. Dit is niet waar voor een in-place upgrade.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Een taken reeks instellen als een taken reeks met hoge impact
Gebruik de volgende procedure om een taken reeks als hoge impact in te stellen.
> [!NOTE]
> Elke taken reeks die aan bepaalde voor waarden voldoet, wordt automatisch gedefinieerd als hoge impact. Zie [implementaties met een hoog risico beheren](../servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.

1. Ga in de Configuration Manager-console naar **Software Library**de  >  **Operating Systems**  >  **taken reeks**besturings systemen software bibliotheek.
2. Selecteer de taken reeks die u wilt bewerken en klik op **Eigenschappen**.
3. Op het tabblad **gebruikers melding** selecteert u **Dit is een taken reeks met hoge impact**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Een aangepaste melding maken voor implementaties met een hoog risico
1. Ga in de Configuration Manager-console naar **Software Library**de  >  **Operating Systems**  >  **taken reeks**besturings systemen software bibliotheek.
2. Selecteer de taken reeks die u wilt bewerken en klik op **Eigenschappen**.
3. Op het tabblad **gebruikers melding** selecteert **u aangepaste tekst gebruiken**.
   > [!NOTE]
   >  U kunt alleen tekst van de gebruikers melding instellen als de **taken reeks met een hoge impact** is geselecteerd.

4. Configureer de volgende instellingen (Maxi maal 255 tekens voor elk tekstvak):

   **Kopregel tekst van gebruikers melding**: Hiermee geeft u de blauwe tekst op die wordt weer gegeven op de gebruikers melding van het Software Center. In de standaard gebruikers melding bevat deze sectie bijvoorbeeld ' Bevestig dat u een upgrade van het besturings systeem op deze computer wilt uitvoeren '.

   **Bericht tekst van gebruikers melding**: er zijn drie tekst vakken die de hoofd tekst van de aangepaste melding geven.
   - 1e tekstvak: Hiermee geeft u de hoofd tekst op, meestal met instructies voor de gebruiker. In de standaard gebruikers melding bevat deze sectie bijvoorbeeld een ' upgrade van het besturings systeem wordt uitgevoerd en kan uw computer enkele keren opnieuw worden opgestart '.
   - 2e tekstvak: Hiermee geeft u de vetgedrukte tekst onder de hoofd tekst van het bericht op. In de standaard gebruikers melding bevat deze sectie bijvoorbeeld het volgende: "met deze in-place upgrade wordt het nieuwe besturings systeem geïnstalleerd en worden uw apps, gegevens en instellingen automatisch gemigreerd."
   - 3e tekstvak: Hiermee geeft u de laatste regel tekst onder de vetgedrukte tekst op. In de standaard gebruikers melding bevat deze sectie bijvoorbeeld een ' Klik op installeren om te beginnen. Klik anders op Annuleren.   

   Stel dat u de volgende aangepaste melding wilt configureren in eigenschappen.

   ![Aangepaste melding voor een taken reeks](./media/user-notification.png)

   Het volgende meldings bericht wordt weer gegeven wanneer de eind gebruiker de installatie opent vanuit software Center.

   ![Aangepaste melding voor een taken reeks](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Eigenschappen van software Center configureren
Gebruik de volgende procedure om de details te configureren voor de taken reeks die wordt weer gegeven in Software Center. Deze details zijn alleen ter informatie.  
1. Ga in de Configuration Manager-console naar **Software Library**de  >  **Operating Systems**  >  **taken reeks**besturings systemen software bibliotheek.
2. Selecteer de taken reeks die u wilt bewerken en klik op **Eigenschappen**.
3. Op het tabblad **Algemeen** zijn de volgende instellingen voor Software Center beschikbaar:
   - **Opnieuw opstarten vereist**: Hiermee geeft u aan dat de gebruiker weet of opnieuw opstarten is vereist tijdens de installatie.
   - **Download grootte (MB)**: Hiermee geeft u op hoeveel MB in Software Center voor de taken reeks wordt weer gegeven.  
   - **Geschatte uitvoerings tijd (minuten)**: Hiermee geeft u de geschatte uitvoerings tijd in minuten op die wordt weer gegeven in Software Center voor de taken reeks.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Controleren of uitvoer bare bestanden worden uitgevoerd voordat een toepassing wordt geïnstalleerd

In het *\<deployment type name>* dialoog venster **Eigenschappen** van een implementatie type op het tabblad installatie gedrag kunt u nu een van de meer uitvoer bare bestanden opgeven die, indien actief, de installatie van het implementatie type blokkeert. De gebruiker moet het uitgevoerde uitvoer bare bestand sluiten (of het kan automatisch worden gesloten voor implementaties met een vereist doel) voordat het implementatie type kan worden geïnstalleerd.

### <a name="try-it-out"></a>Probeer het maar.

1. Klik in de eigenschappen van een Configuration Manager implementatie type op het tabblad **installatie gedrag** .
2. Kies **toevoegen** om een of meer namen van uitvoer bare bestanden toe te voegen die u wilt controleren. U kunt ook een weergave naam toevoegen om ervoor te zorgen dat gebruikers gemakkelijker toepassingen in de lijst kunnen identificeren.
3. Als de implementatie een vereist doel heeft, kunt u in de wizard software implementeren desgewenst kiezen voor **het automatisch sluiten van uitvoer bare bestanden die u hebt opgegeven op het tabblad installatie gedrag van het dialoog venster Eigenschappen van implementatie type**.

Als de toepassing is geïmplementeerd als **beschikbaar**en een eind gebruiker probeert een toepassing te installeren, wordt u gevraagd of u de door u opgegeven uitvoer bare bestanden wilt sluiten voordat de installatie kan worden voortgezet.

Als de toepassing is geïmplementeerd als **vereist**en de optie **voor het automatisch sluiten van uitvoer bare bestanden die u hebt opgegeven op het tabblad installatie gedrag van het dialoog venster Eigenschappen van implementatie type** , wordt een dialoog venster weer gegeven waarin wordt gemeld dat de uitvoer bare bestanden die u hebt opgegeven automatisch worden gesloten wanneer de deadline voor de installatie van de toepassing wordt bereikt. U kunt deze dialoog vensters plannen in **client instellingen**  >  **computer agent**. Als u niet wilt dat de eind gebruiker deze berichten ziet, selecteert u **verbergen in Software Center en alle meldingen** op het tabblad **gebruikers ervaring** van de eigenschappen van de implementatie.

Als de toepassing is geïmplementeerd als **vereist** en de optie **voor het automatisch sluiten van uitvoer bare bestanden die u hebt opgegeven op het tabblad installatie gedrag van het dialoog venster Eigenschappen van implementatie type** , wordt de installatie van de app mislukt als een of meer van de opgegeven toepassingen worden uitgevoerd.

## <a name="create-pfx-certificates-with-s-mime-support"></a>PFX-certificaten maken met S MIME-ondersteuning

U kunt nu een PFX-certificaat profiel maken dat S/MIME ondersteunt en dit implementeert voor gebruikers.  Dit certificaat kan vervolgens worden gebruikt voor S/MIME-versleuteling en ontsleuteling op alle apparaten die de gebruiker heeft inge schreven.

Daarnaast kunt u nu meerdere certificerings instanties (Ca's) opgeven op meerdere site systeem rollen voor het certificaat registratiepunt en vervolgens de aanvragen van het CAs-proces toewijzen als onderdeel van het certificaat profiel.

Voor iOS-apparaten kunt u een PFX-certificaat profiel aan een e-mail profiel koppelen en S/MIME-versleuteling inschakelen.  Vervolgens wordt S/MIME in de systeem eigen e-mailclient op iOS ingeschakeld en wordt het juiste S/MIME-versleutelings certificaat aan het bestand gekoppeld.

Zie [Inleiding tot certificaat profielen]( /sccm/protect/deploy-use/introduction-to-certificate-profiles)voor meer informatie over certificaten in Configuration Manager.


## <a name="new-compliance-settings-for-ios-devices"></a>Nieuwe instellingen voor naleving voor iOS-apparaten

Er zijn nieuwe instellingen toegevoegd die u kunt gebruiken in uw configuratie-items voor iOS-apparaten. Dit zijn instellingen die voorheen aanwezig waren in Microsoft Intune in een zelfstandige configuratie en zijn nu beschikbaar wanneer u intune gebruikt met Configuration Manager. Als u hulp nodig hebt bij een van deze instellingen, raadpleegt u [IOS-beleids instellingen in Microsoft intune](../../../intune/configuration/device-restrictions-ios.md).

- **Gegevens van beheerde apps synchroniseren met iCloud**
- **Te leveren om activiteiten op een ander apparaat voort te zetten**
- **iCloud-Foto's delen**
- **iCloud-foto bibliotheek**
- **Nieuwe auteurs van bedrijfsapps vertrouwen**
- **De gebruiker toestaan om inhoud te downloaden van de iBooks Store die als ' erotisch ' is gemarkeerd** (alleen in de modus Super visie)
- **Forceren dat de gekoppelde Apple Watch Wrist Detection gebruikt**
- **Wacht woord voor uitgaande AirPlay-aanvragen**
- **Account instellingen wijzigen** (alleen in de modus Super visie)
- **Wijzigingen in de instellingen voor het gebruik van mobiel data verkeer voor apps** (alleen in de modus Super visie)
- **Alle inhoud en instellingen wissen** (alleen onder Super visie modus)
- **Beperkingen op het apparaat configureren** (alleen onder Super visie modus)
- **Koppelen met een host gebruiken om te bepalen met welke apparaten een IOS-apparaat kan worden gekoppeld** (alleen onder Super visie modus)
- **Configuratie profielen en certificaten installeren** (alleen in de modus Super visie)
- **Apparaatnaam wijzigen** (alleen in de modus Super visie)
- **Wachtwoord code wijzigen** (alleen in de modus Super visie)
- **Koppeling voor Apple Watch** (alleen onder Super visie)
- **Wijziging van meldings instellingen** (alleen onder Super visie modus)
- **Wijzigen** van de achtergrond (alleen in de modus Super visie)
- **Instellingen voor het verzenden van diagnostische gegevens** (alleen in de modus Super visie)
- **Bluetooth-wijziging** (alleen in de modus Super visie)
- **Disdrop** (alleen onder Super visie modus)
- **Gebruik SIRI om door gebruikers gegenereerde inhoud te doorzoeken van Internet** (alleen in de modus Super visie)
- **SIRI-filter voor scheld woorden** (alleen onder Super visie modus)
- **Resultaten van Internet retour neren in Spotlight zoeken** (alleen in de modus Super visie)
- **Opzoeken van definities van woorden** (alleen in de modus Super visie)
- **Voorspellende toetsen borden** (alleen in de modus Super visie)
- **Automatische correctie** (alleen in de modus Super visie)
- **Spelling controle** (alleen in de modus Super visie)
- **Sneltoetsen** (alleen in de modus Super visie)
  <!--- - **Enterprise app trust settings modification** --->
- **Apps installeren met behulp van Apple Configurator en alleen iTunes** (alleen onder Super visie modus)
- **Automatisch downloaden van apps** (alleen onder Super visie modus)
- **Wijzigingen aanbrengen in de instellingen van de app Zoek vrienden** (alleen onder Super visie)
- **Toegang tot de iBooks Store** (alleen onder Super visie modus)
- **Berichten-app** (alleen onder Super visie modus)
- **Podcasts** (alleen modus met Super visie)
- **Apple Music** (alleen onder Super visie modus)
- **iTunes radio** (alleen onder Super visie modus)
- **Apple News** (alleen onder Super visie modus)
- **Game Center** (alleen onder Super visie modus)
- **Disdrop behandelen als een onbeheerd doel**

## <a name="android-for-work-support"></a>Ondersteuning van Android for Work

Vanaf Technical Preview versie 1702 kunt u een Google-account binden aan uw Hybrid MDM-Tenant. Hiermee kunt u het volgende doen:

- [Ondersteunde Android-apparaten](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) als Android for work registreren, werk profielen maken op die geregistreerde apparaten
- Apps goed keuren in het Play for work-archief, synchroniseer ze met de Configuration Manager-console en implementeer ze vervolgens op werk profielen van apparaten
- Configuratie-items maken en implementeren om het werk profiel en de wachtwoord instellingen voor deze apparaten te configureren
- Nalevings beleids items en bron toegangs profielen voor Android for work-apparaten maken en implementeren, zoals u al hebt gedaan voor Android-apparaten
- Selectief wissen uitvoeren op Android for work-apparaten

Wanneer u een apparaat inschrijft als Android for work, wordt er een werk profiel gemaakt op het apparaat dat door intune kan worden beheerd. Dit werk profiel bestaat naast het persoonlijke profiel op het Android-apparaat. Gebruikers kunnen eenvoudig scha kelen tussen werk profiel-apps en persoonlijke profiel-apps. U kunt geen items beheren in het persoonlijke profiel. Persoonlijke apps en gegevens blijven onbeheerd. Configuration Manager heeft volledige controle over het werk profiel en de inhoud ervan en kan het verwijderen van het apparaat.

Android for work is een afzonderlijk platform van Android en u moet bepalen welk beheer formulier moet worden gebruikt voor Android-apparaten die ondersteuning bieden voor werk profielen.

### <a name="try-it-out"></a>Probeer het nu!
In de volgende secties wordt Android for work-beheer beschreven.

#### <a name="enable-android-for-work-management"></a>Android for work-beheer inschakelen
1. Maak een Google-account op https://accounts.google.com/SignUp om te gebruiken als uw Android for work-beheerders account dat wordt gekoppeld aan alle Android for work-Beheer taken voor deze intune-Tenant. Dit kan een Google-account zijn dat wordt gedeeld tussen de beheerders die Android-apparaten beheren. Dit is het Google-account dat uw organisatie gebruikt voor het beheren en publiceren van apps in de Play for Work-console. U gebruikt dit account voor het goed keuren van apps in de Play for work-Store, dus houd de account naam en het wacht woord bij.
2. Schakel Android-inschrijving in door het Google-account te binden aan de intune-Tenant die wordt beheerd in Configuration Manager:
   1. Ga naar **beheer**  >  **overzicht**  >  **Cloud Services**  >  **Microsoft intune-abonnementen** en selecteer uw intune-abonnement.
   2. Klik in het lint op **platformen**  >  **Android** configureren en zorg ervoor dat **Android-registratie inschakelen** is ingeschakeld.
   3. Klik in het lint op **platformen**  >  **Android for work**configureren.
   4. Klik in het dialoog venster op **Android for work configureren in de intune-console**. De intune-console wordt geopend in uw webbrowser.
   5. Gebruik uw intune-beheerders referenties om u aan te melden bij de intune-Portal.
   6. Klik op **configureren** om de Android for work-website van Google Play te openen.
   7. Op de aanmeldings pagina van Google voert u de referenties voor het Google-account uit stap 1 in en geeft u de gegevens van uw bedrijf op.
3. Wanneer u terugkeert naar de intune-Portal, wordt Android for work ingeschakeld en hebt u drie registratie opties voor Android for work-apparaten:
   - **Alle apparaten beheren als Android** : (uitgeschakeld) alle Android-apparaten, met inbegrip van apparaten die ondersteuning bieden voor Android for work, worden geregistreerd als conventionele Android-apparaten
   - **Ondersteunde apparaten beheren als Android for Work-apparaten**: (ingeschakeld) alle apparaten met ondersteuning voor Android for Work worden geregistreerd als Android for Work-apparaten. Alle Android-apparaten die geen ondersteuning bieden voor Android for Work, worden geregistreerd als conventionele Android-apparaten.
   - **Alleen ondersteunde apparaten voor de gebruikers in deze groepen beheren als Android for work** -(testen) Hiermee kunt u Android for work-beheer aan een beperkt aantal gebruikers richten. Alleen voor leden van de geselecteerde groepen worden apparaten met ondersteuning voor Android for Work geregistreerd als Android for Work-apparaten. Alle overige apparaten worden geregistreerd als Android-apparaten.
  
> [!NOTE]
> Een bekend probleem verhindert dat de optie **alleen ondersteunde apparaten voor gebruikers in deze groepen beheren als Android for work** werkt zoals verwacht. De apparaten van gebruikers in de opgegeven Azure AD-groepen worden geregistreerd als Android in plaats van Android for work. Als u Android for work wilt testen, moet u de **alle ondersteunde apparaten beheren gebruiken als Android for work**.


  Als u Android for work-inschrijving wilt inschakelen, moet u een van de twee onderste opties kiezen. Voor de optie **alleen ondersteunde apparaten voor gebruikers in deze groepen beheren als Android for work** moeten Azure Active Directory beveiligings groepen eerst zijn ingesteld.

U ziet de account naam en de naam van de organisatie in de intune-Portal wanneer de binding is voltooid. op dat moment kunt u beide browsers sluiten.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Android for work-apps goed keuren en implementeren
Volg deze stappen voor het goed keuren van apps in de Play for work-Store, synchroniseer ze met de Configuration Manager-console en implementeer ze op beheerde Android for work-apparaten. Als u apps wilt implementeren op werk profielen van gebruikers, moet u de apps goed keuren in Play for work en vervolgens de apps synchroniseren met de Configuration Manager-console.

1. Open een browser en ga naar: https://play.google.com/work .
2. Meld u aan met het Google-beheerders account dat u hebt gebonden aan uw intune-Tenant.
3. Blader naar de apps die u in uw omgeving wilt implementeren en klik op **goed keuren** voor elk van deze toepassingen.
4. Ga in de Configuration Manager-console naar overzicht van de **beheerder**  >  **Overview**  >  **Cloud Services**  >  **Android for work** en klik op **synchroniseren**.
5. Wacht Maxi maal tien minuten voor het synchroniseren van apps en ga vervolgens naar **software bibliotheek**  >  **overzicht**  >  **Application Management**-  >  **licentie gegevens voor Store-apps**.
6. Klik op een app die is gesynchroniseerd vanuit Play for work en klik vervolgens op **create Application**.
7. Voltooi de wizard en klik op **sluiten**.
8. Ga naar **software bibliotheek**  >  **overzicht**toepassingen voor  >  **toepassings beheer**  >  **Applications**, selecteer een Android for work-apps en implementeer dit op de gebruikelijke manier.

Als u Play for work-apps met Configuration Manager wilt synchroniseren, moet u ten minste één app goed keuren op de website Play for work.

#### <a name="enroll-an-android-for-work-device"></a>Een Android for work-apparaat inschrijven
Hoe u Android for work-apparaten inschrijft, is vergelijkbaar met de inschrijving voor Android. Down load de Bedrijfsportal-app voor Android op uw mobiele apparaat en voer deze uit. U wordt gevraagd om een werk profiel te maken als onderdeel van het registratie proces.  Zodra het werk profiel is gemaakt, moet u overschakelen naar de beheerde versie van de Bedrijfsportal. De beheerde Bedrijfsportal is gelabeld met een kleine oranje werkmap in de rechter benedenhoek.

#### <a name="create-and-deploy-a-configuration-item"></a>Een configuratie-item maken en implementeren
Android for Work heeft twee instellings groepen voor configuratie-items:
- Wachtwoord
- Werk profiel

U kunt het delen van inhoud configureren tussen werk profielen, evenals de volgende configuratie-items op apparaten met Android 6 of hoger:
- Het gedrag voor apps die om specifieke machtigingen vragen
- Of meldingen voor toepassingen binnen het werk profiel zichtbaar zijn op het vergrendelings scherm

Als u dit wilt proberen, maakt u een configuratie-item via de werk stroom standaard, kiest u **Android for work** op de pagina **Algemeen** en configureert u de instellingen voor elk van de instellings groepen, voegt u het configuratie-item toe aan een basis lijn en implementeert u dit op de gebruikelijke manier. Deze instellingen zijn alleen van toepassing op apparaten die zijn Inge schreven als Android for work, en niet die zijn Inge schreven als Android.

#### <a name="perform-selective-wipe"></a>Selectief wissen uitvoeren
Apparaten die zijn Inge schreven als Android for work kunnen alleen selectief worden gewist omdat u het werk profiel alleen beheert. Hiermee wordt het persoonlijke profiel beschermd tegen wissen. Als u selectief wissen op een Android for work-apparaat uitvoert, wordt het werk profiel verwijderd, inclusief alle apps en gegevens, en wordt de registratie van het apparaat ongedaan gemaakt.

Als u selectief wilt wissen voor een Android for work-apparaat, gebruikt u het normale [proces voor selectief wissen](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) in de Configuration Manager-console.

#### <a name="known-issues-for-android-for-work"></a>Bekende problemen voor Android for work
Het **configureren van een synchronisatie schema in Android for work e-mail profielen zorgt ervoor dat ze niet kunnen worden geïmplementeerd** Een van de opties in de Configuration Manager-gebruikers interface voor Android for work-e-mail profielen is schema. Op andere platforms kan de beheerder een planning configureren voor het synchroniseren van e-mail en andere e-mail account gegevens op de mobiele apparaten waarop deze is geïmplementeerd. Het werkt echter niet voor e-mail profielen voor Android for work en als u een andere optie dan ' niet geconfigureerd ' kiest, wordt het profiel niet geïmplementeerd op apparaten.