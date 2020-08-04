---
title: Mogelijkheden van Technical Preview 1601
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1601.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: be1401f28ccbd15de2561a19169ed67a81a91550
ms.sourcegitcommit: 7e34b561d43aa086fc07ab4edf2230d09c04f05b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2020
ms.locfileid: "87526029"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1601 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1601. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site.      Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.  

 **Bekende problemen met deze technische preview:**  

-   Wanneer u **client update opties** beheert om een pre-productie client te promo veren tot productie, wordt in de tekst voor het selectie vakje een client versie van nul (0) weer gegeven in plaats van het werkelijke client buildnummer. De juiste client versie vóór productie wordt weer gegeven op het Opper vlak boven deze optie en is de client versie die wordt gepromoveerd tot productie wanneer u deze optie selecteert.  

-   Bij het bijwerken van Technical Preview 1601 en kiezen om de Configuration Manager-client te testen in een pre-productie verzameling, wordt het client pakket voor de verzameling niet bijgewerkt. Dit probleem geldt alleen voor Technical Preview 1601.  

     Voer een van de volgende handelingen uit om deze problemen op te lossen:  

    -   Voer het volgende SQL-script uit op de data base van de primaire site:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Voeg een nieuwe site systeemrol voor distributie punten toe aan uw Lab-site. Het nieuwe distributie punt werkt de pre-productie verzameling bij met het nieuwe client pakket.  

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a>Verbeteringen in Microsoft Intune integratie  
In de 1601 Technical Preview is ondersteuning toegevoegd voor de volgende functies:  

### <a name="improvements-to-conditional-access"></a>Verbeteringen in voorwaardelijke toegang  

-   **Ondersteuning voor voorwaardelijke toegang voor Pc's die worden beheerd door Configuration Manager**  

     U kunt nu beleid voor voorwaardelijke toegang instellen voor Pc's die worden beheerd door Configuration Manager, zodat de computers voldoen aan het nalevings beleid om toegang te krijgen tot Exchange Online-en share point Online-Services.  Met deze nieuwe functionaliteit kunt u ook Pc's met Azure AD registreren via het nalevings beleid en de registratie van Azure AD bewaken en rapporteren.  

    > [!NOTE]  
    >  Voorwaardelijke toegang wordt nog niet ondersteund in Windows 10.  

    Hier volgen de vereisten voor het gebruik van deze functie:  

    -   Azure Active Directory Premium-abonnement en ADFS-synchronisatie.  

    -   Een Microsoft Intune-abonnement. Het Microsoft Intune-abonnement moet worden geconfigureerd in Configuration Manager-console.  

    -   [Vereisten voor automatische registratie van Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Als u de optie wilt gebruiken, moet u een nalevings beleid maken in Configuration Manager met specifieke regels die hieronder worden beschreven en een beleid voor voorwaardelijke toegang instellen in de intune-console.  Als u er zeker van wilt zijn dat alleen compatibele Pc's toegang hebben, moet u de Windows-PC-vereiste instellen op **apparaten moet voldoen** aan het beleid. Hieronder vindt u de regels die voldoen aan het beleid dat van toepassing is op Pc's die worden beheerd door Configuration Manager.  

    -   **Registratie in azure ActiveDirectory vereisen:** Deze regel controleert of het apparaat van de gebruiker is toegevoegd aan Azure AD. als dit niet het geval is, wordt het apparaat automatisch geregistreerd in azure AD. Automatische inschrijving wordt alleen ondersteund op Windows 8.1. Implementeer een MSI-bestand om automatische inschrijving voor Windows 7-pc's uit te voeren. Klik [hier](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) voor meer informatie.  

    -   **Alle vereiste updates met een deadline die ouder is dan een bepaald aantal dagen, zijn geïnstalleerd:** Deze regel controleert of het apparaat van de gebruiker alle vereiste updates heeft (opgegeven in de regel **vereiste automatische updates** ) binnen de door u opgegeven deadline en respijt periode, en installeert automatisch de vereiste updates die nog niet zijn geïnstalleerd.  

    -   **BitLocker-stationsversleuteling vereisen:** Dit is een controle om te controleren of het primaire station (bijvoorbeeld C: \\ ) op het apparaat BitLocker is versleuteld. Als Bitlocker-versleuteling niet is ingeschakeld op het primaire station, wordt de toegang tot e-mail en SharePoint-services geblokkeerd.  

    -   **Antimalware vereisen:** Hiermee wordt gecontroleerd of de antimalware-software (alleen System Center Endpoint Protection of Windows Defender) is ingeschakeld en wordt uitgevoerd.  
         Indien dit niet is ingeschakeld, wordt de toegang tot e-mail en SharePoint-services geblokkeerd.  

    Eind gebruikers die zijn geblokkeerd vanwege niet-naleving, zullen compatibiliteits informatie bekijken in het Software Center en een nieuwe beleids evaluatie initiëren wanneer nalevings problemen zijn hersteld.  

-   **Voorwaardelijke toegang met de Health Attestation-service** U kunt de toegang tot e-mail en 0365-Services nu beperken op basis van de status van de apparaten, zoals gerapporteerd door de Health Attestation-service.  Daarnaast worden apparaten die door intune worden beheerd, opgenomen in de status rapporten van het apparaat.  

    Er is een nieuwe regel voor naleving toegevoegd aan de Configuration Manager-console waarmee u kunt opgeven of de toegang tot de apparaten moet worden toegestaan of geblokkeerd op basis van hun status.  Als u deze regel wilt maken, opent u de **wizard nalevings beleid maken**en voegt u een nieuwe regel toe.  Selecteer de **Health Attestation-service** voor de voor waarde gerapporteerd als status en stel de waarde in op **waar**.  Dit zorgt ervoor dat alleen apparaten die zijn gerapporteerd als in orde, toegang hebben tot uw bedrijfs resources. Zie [Apparaatstatusverklaring](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)voor meer informatie over Health Attestation-service en hoe de status van de apparaten in intune wordt gerapporteerd.  

-   **Nieuwe instellingen voor nalevings beleid:** De nieuwe instellingen voor nalevings beleid helpen bij het verbeteren van de beveiliging en beveiliging op apparaten die worden gebruikt voor toegang tot bedrijfs-e-mail en share Point-services:  

    -   **Automatische updates vereisen:** U kunt apparaten met Windows 8,1 of hoger vereisen om automatische installatie van updates toe te staan en ook de klasse van geïnstalleerde updates op te geven.  U kunt kiezen uit: Installeer alleen updates die zijn gemarkeerd als belang rijk of installeer alle aanbevolen updates.  

         Als u een regel voor automatische updates wilt maken, opent u de **wizard nalevings beleid maken**en voegt u een nieuwe regel toe.  Selecteer **minimale classificatie van vereiste updates** als voor waarde en stel de waarde in op een van de beschik bare waarden: **geen**, **Aanbevolen**en **belang rijk**.  

        -   **Geen:** Updates worden niet automatisch geïnstalleerd.  

        -   **Aanbevolen:** Alle aanbevolen updates zijn geïnstalleerd  

        -   **Belang rijk:** Alleen updates die als belang rijk zijn geclassificeerd, worden geïnstalleerd.  

    -   **Wacht woord vereisen voor het ontgrendelen van mobiele apparaten:** Als deze instelling is ingesteld op **Ja**, moeten eind gebruikers een wacht woord invoeren om toegang te krijgen tot hun apparaat.  

         Als u een regel wilt maken voor wacht woord voor het ontgrendelen van mobiele apparaten, opent u de **wizard nalevings beleid maken**en voegt u een nieuwe regel toe. Selecteer **een wacht woord vereisen om een inactief apparaat te ontgrendelen** als voor waarde en stel de waarde in op **waar**.  

    -   **Minuten inactief voordat wachtwoord is vereist**: hiermee geeft u aan na hoeveel niet-actieve tijd gebruikers hun wachtwoord opnieuw moeten invoeren.  

         Als u deze regel wilt maken, opent u de **wizard nalevings beleid maken**en voegt u een nieuwe regel toe. **Selecteer minuten van inactiviteit voordat wacht woord vereist is** als voor waarde en stel de waarde in op een van de beschik bare opties: 1 minuut, 5 minuten, 15 minuten, 30 minuten, I uur.  

-   **Standaard regel negeren: intune Inge schreven en compatibele apparaten altijd toegang tot Exchange on-premises toestaan:**  

     Wanneer u deze optie inschakelt, zijn apparaten die zijn Inge schreven bij intune en voldoen aan het nalevings beleid, toegang tot Exchange on-premises toegestaan. Met deze regel wordt de standaard regel overschreven, wat betekent dat zelfs als u de standaard regel instelt op quarantaine of toegang blokkeert, Inge schreven en compatibele apparaten nog steeds toegang hebben tot Exchange on-premises.  
     Gebruik deze instelling als u wilt dat Inge schreven en compatibele apparaten altijd toegang hebben tot e-mail via Exchange on-premises.  

     Dit wordt ondersteund op de volgende platformen: Windows Phone 8 en hoger, iOS 6 en hoger. Android 4,0 en hoger, Samsung KNOX Standard 4,0 of hoger.  

     Als u deze optie wilt gebruiken, gaat u naar de pagina **Algemeen** van de **wizard beleid voor voorwaardelijke toegang configureren** voor Exchange on-premises.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a>Online status van client  
Vanaf Technical Preview 1601 kunt u in een oogopslag zien of een client online of offline is in de Configuration Manager-console. Met bijgewerkte pictogrammen en kolommen in de lijst met apparaten kunt u de status van clients in uw omgeving beoordelen om probleem gebieden te identificeren en andere problemen die mogelijk uw aandacht vereisen.  

Een client is online als deze momenteel is verbonden met een Configuration Manager beheer punt-site systeemrol. Zolang het beheer punt ping-achtige berichten van de client ontvangt, is de status online. Als het beleid gedurende vijf minuten geen bericht ontvangt, wordt de status van de client gewijzigd in offline.  

### <a name="icons-for-client-status"></a>Pictogrammen voor de client status  

| Pictogram | Beschrijving |
| ---- | ----------- |
|![online-statuspictogram voor clients](media/online-status-icon.png)|De client is online.|  
|![offline-statuspictogram voor clients](media/offline-status-icon.png)|De client is offline.|  
|![onbekende-statuspictogram voor clients](media/unknown-status-icon.png)|De client status is onbekend.|  

### <a name="prerequisites"></a>Vereisten  
 De online status van de client heeft geen vereisten. U kunt deze gaan gebruiken zodra Configuration Manager Technical Preview 1601 is geïnstalleerd.  

### <a name="limitations"></a>Beperkingen  
 De online status van de client is alleen beschikbaar voor Windows-computers waarop de Configuration Manager-client is geïnstalleerd. De online status van de client wordt niet ondersteund voor Mac-, Linux-of UNIX-computers of apparaten die worden beheerd met on- \- premises Mobile Device Management.  

### <a name="to-view-client-online-status"></a>Online status van de client weer geven  

1. Ga in de Configuration Manager-console naar **activa en naleving > overzicht > apparaten**.  

2. Klik met de rechter muisknop op de kolomkop en klik vervolgens op een van de online status velden van de client om deze toe te voegen aan de weer gave apparaat. De velden zijn  

   -   **Onlinestatus van het apparaat** geeft aan of de client op dit moment online of offline is.  

   -   **Laatste tijdstip online** geeft aan wanneer de online status van de client is gewijzigd van offline in online.  

   -   **Laatste tijdstip offline** geeft aan wanneer de status van online naar offline is gewijzigd.  

   Vernieuw de console om recente wijzigingen in de client status weer te geven.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a>Verbeteringen aan toepassings beheer  
 In de 1601 Technical Preview is ondersteuning toegevoegd voor de volgende functies:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Volume-purchased apps voor iOS-apparaten beheren  
 Bepaalde App Stores bieden u de mogelijkheid meerdere licenties te kopen voor een app die u wilt uitvoeren binnen uw bedrijf. Zodoende kunt u de administratieve overhead voor het bijhouden reduceren als u meerdere exemplaren van apps hebt aangeschaft.  

 Configuration Manager helpt u bij het beheren van apps die u via een dergelijk programma hebt aangeschaft door de licentie gegevens uit de App Store te importeren en bij te houden hoeveel licenties u hebt gebruikt.  


### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS-app-configuratie voor toepassingen<br />Hybride  
 Sommige iOS-toepassingen ondersteunen het vooraf configureren van instellingen, zoals een server of database waarmee de toepassing verbinding moet maken. Configuration Manager ondersteunt nu het implementeren van app-configuratie beleidsregels op het apparaat, zodat de gebruiker de app onmiddellijk kan gebruiken zonder dat deze informatie nodig is. Ontwikkel aars moeten deze functionaliteit in hun apps inschakelen.  

 Een beperkt aantal openbaar vrijgegeven Apps ondersteunt momenteel vooraf geconfigureerde instellingen; mogelijk hebt u ook intern ontwikkelde line-of-Business-Apps die ondersteuning bieden voor deze toepassingen.  

#### <a name="prerequisites-for-this-scenario"></a>Vereisten voor dit scenario  

-   U moet een Microsoft Intune-abonnement aan Configuration Manager hebben toegevoegd.  

-   U moet een geldig Apple APNs-certificaat toevoegen aan het intune-abonnement.  

-   U moet een iOS-toepassing hebben geïmplementeerd die toepassings configuratie ondersteunt.  

#### <a name="try-it-out"></a>Probeer het nu!  
 Zodra aan de bovenstaande vereisten wordt voldaan, moet u een Configuration Manager-toepassing maken die gebruikmaakt van een iOS-implementatie type. De app die u gebruikt, moet toepassings configuratie ondersteunen. Raadpleeg de documentatie van de leverancier van de toepassing voor meer informatie over welke specifieke items (naam/waarde-paren) u kunt configureren.  

 Vervolgens koppelt u het app-configuratie beleid aan het iOS-implementatie type tijdens de implementatie van de app. U kunt het beleid ook implementeren vanuit het knoop punt **app-configuratie beleid** , gericht op een bestaande app en verzameling.  

 Voer de volgende taken uit en gebruik daarna de feedback informatie boven aan dit onderwerp om ons te laten weten hoe ze hebben gewerkt:  

-   Als u een iOS-app hebt die app-configuratie ondersteunt, raadpleegt u de documentatie van de app-leverancier voor de naam-en waardeparen die u moet opgeven om de toepassing te configureren.  

-   Start de wizard **app-configuratie beleid maken** . Probeer op de pagina **IOS-beleid** van de wizard de naam en waardeparen toe te voegen die u hebt gevonden in de documentatie van de leverancier van de app of importeer een XML-bestand met de vereiste waarden.  

-   In de wizard **software implementeren** koppelt u op de pagina **app-configuratie beleid** het app-configuratie beleid dat u hebt gemaakt met een compatibel implementatie type van de toepassing.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a>Verbeteringen aan de instellingen voor naleving  
 In de 1601 Technical Preview is ondersteuning toegevoegd voor de volgende functies:  

### <a name="microsoft-edge-browser-settings"></a>Micro soft Edge-browser instellingen  
 Er zijn nieuwe instellingen voor de micro soft Edge-browser toegevoegd aan het configuratie-item voor **windows 8,1 en Windows 10** (de instellingen zijn alleen van toepassing op Windows 10-apparaten).  

 Als u de nieuwe instellingen wilt zien, kiest u **micro soft Edge** op de pagina configuratie-item **Apparaatinstellingen** van de wizard **configuratie-item maken** .  

 Zie [configuratie-items maken voor windows 8,1-en Windows 10-apparaten die worden beheerd zonder de Configuration Manager-client](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)voor meer informatie.  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Nalevings instellingen voor Windows 10 team-apparaten  
 Gebruik deze nieuwe instellingen voor naleving om apparaten te configureren waarop Windows 10 team wordt uitgevoerd, zoals Surface Hub apparaten.  

 Als u de nieuwe instellingen wilt zien, kiest u **Windows 10-team** op de pagina configuratie-item **Apparaatinstellingen** van de wizard **configuratie-item maken** .  

 Zie [configuratie-items maken voor windows 8,1-en Windows 10-apparaten die worden beheerd zonder de Configuration Manager-client](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)voor meer informatie.  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android-kiosk modus voor Samsung KNOX Standard<br />Hybride  
 In de kiosk modus kunt u een apparaat zodanig vergren delen dat alleen bepaalde functies werken. U kunt bijvoorbeeld toestaan dat een apparaat slechts één beheerde app uitvoert die u opgeeft, of kunt u de volumeknoppen op een apparaat uitschakelen. Deze instellingen kunnen worden gebruikt voor een demonstratiemodel van een apparaat of voor een apparaat dat is toegewezen aan slechts één functie, zoals een verkooppuntapparaat. Deze instellingen zijn niet beschikbaar voor Samsung KNOX Standard-apparaten in het **windows 8,1-en Windows 10** -configuratie-item (instellingen zijn alleen van toepassing op Windows 10-apparaten).  

 Als u de nieuwe instellingen wilt zien, kiest u **kiosk modus-Samsung KNOX** op de pagina configuratie-item **Apparaatinstellingen** van de wizard **configuratie-item maken** .  

 Zie [configuratie-items maken voor windows 8,1-en Windows 10-apparaten die worden beheerd zonder de Configuration Manager-client](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)voor meer informatie.  
