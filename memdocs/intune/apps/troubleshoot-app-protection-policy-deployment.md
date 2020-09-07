---
title: Problemen oplossen met de implementatie van Intune-beveiligingsbeleid voor apps
description: In dit artikel wordt beschreven hoe u problemen oplost die kunnen optreden wanneer u Intune-beveiligingsbeleid voor apps implementeert.
author: simonxjx
manager: dcscontentpm
localization_priority: Normal
search.appverid:
- MET150
audience: ITPro
ms.date: 4/17/2020
ms.service: microsoft-intune
ms.subservice: apps
ms.topic: troubleshooting
ms.author: v-six
ms.custom: CSSTroubleshoot
appliesto:
- Intune
ms.openlocfilehash: 9aceb4d2b8b0b67af297fa5d15cdf66ae04a83f4
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996619"
---
# <a name="troubleshooting-app-protection-policy-deployment-in-intune"></a>Problemen oplossen met de implementatie van Intune-beveiligingsbeleid voor apps

## <a name="introduction"></a>Inleiding

Dit artikel biedt u inzicht in en oplossingen voor problemen met het toepassen van beveiligingsbeleid voor apps in Microsoft Intune. Volg de secties die van toepassing zijn op uw situatie.

## <a name="basic-steps"></a>Basisstappen

### <a name="collect-initial-data"></a>Initiële gegevens verzamelen

Voordat u begint met het oplossen van problemen, moet u wat basisinformatie verzamelen om meer inzicht te krijgen in het probleem en sneller een oplossing te vinden.

Verzamel de volgende gegevens:

- Welke beleidsinstelling is niet toegepast? Wordt een beleid toegepast?
- Wat is de gebruikerservaring? Hebben gebruikers de beoogde app geïnstalleerd en gestart?
- Wanneer is het probleem begonnen? Heeft app-beveiliging ooit gewerkt?
- Op welk platform (Android of iOS) bevindt zich het probleem?
- Hoeveel gebruikers treft het probleem? Zijn alle apparaten of alleen bepaalde apparaten betrokken?
- Voor hoeveel apparaten geldt het probleem? Zijn alle apparaten of alleen bepaalde apparaten betrokken?
- Hoewel voor het Intune-beveiligingsbeleid voor apps geen Mobile Device Management-service (MDM) is vereist, gebruiken getroffen gebruikers Intune of EMM van derden?
- Zijn alle beheerde apps of alleen specifieke apps betrokken? Zijn bijvoorbeeld LOB-apps met [Intune App SDK](../developer/app-sdk-get-started.md) betrokken, maar Store-apps niet?

U kunt nu beginnen met de oplossing van het probleem op basis van de antwoorden op deze vragen.

### <a name="verify-prerequisites"></a>De vereisten controleren

De volgende stap in de oplossing van het probleem is controleren of aan alle vereisten is voldaan.

Hoewel u het Intune-beveiligingsbeleid voor apps onafhankelijk van een MDM-oplossing kunt gebruiken, moet aan de volgende vereisten worden voldaan:

- Er moet een Intune-licentie zijn toegewezen aan de gebruiker.
- De gebruiker moet behoren tot een beveiligingsgroep waarop een beleidsregel voor de beveiliging van apps is gericht. Dezelfde beleidsregel voor de beveiliging van apps moet ook zijn gericht op de specifieke app die wordt gebruikt.
- Android-apparaten moeten beschikken over de bedrijfsportal-app om app-beveiligingsbeleid te krijgen.
- Als u de apps [Word, Excel of Power Point](https://products.office.com/business/office) gebruikt, moet aan de volgende aanvullende vereisten worden voldaan:
    - De gebruiker moet een licentie voor [Microsoft 365 Apps voor Business of Enterprise](https://products.office.com/business/compare-more-office-365-for-business-plans) aan zijn/haar Azure Active Directory-account (Azure AD) hebben gekoppeld. Het abonnement moet de Office-apps voor mobiele apparaten bevatten en kan een cloudopslagaccount met [OneDrive voor Bedrijven](https://onedrive.live.com/about/business/) bevatten. Microsoft 365-licenties kunnen aan de hand van de volgende [instructies](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc) worden toegewezen in het [Microsoft 365-beheercentrum](https://admin.microsoft.com).
    - De gebruiker moet een beheerde locatie hebben die is geconfigureerd met behulp van de gedetailleerde functionaliteit **Opslaan als**. Deze opdracht bevindt zich onder de instelling **Kopieën van organisatiegegevens opslaan** in het beveiligingsbeleid van de toepassing. Als bijvoorbeeld [OneDrive](https://onedrive.live.com/about/) de beheerde locatie is, moet de OneDrive-app worden geconfigureerd in de Word-, Excel- of PowerPoint-app van de gebruiker.
    - Als OneDrive de beheerde locatie is, moet de app het doel zijn van het app-beveiligingsbeleid dat voor de gebruiker is geïmplementeerd.

  > [!NOTE]
  > De mobiele Office-apps bieden momenteel alleen ondersteuning voor SharePoint Online en niet voor SharePoint On-Premises.

- Als u Intune-beveiligingsbeleid voor apps gebruikt in combinatie met on-premises resources (Microsoft Skype voor bedrijven en Microsoft Exchange Server), moet u [Hybrid Modern Authentication (HMA) inschakelen voor Skype voor bedrijven en Exchange](/office365/enterprise/hybrid-modern-auth-overview).

Voor het app-beveiligingsbeleid van Intune moet de identiteit van de gebruiker in de app consistent zijn met [Intune App SDK](../developer/app-sdk-get-started.md). Deze consistentie kan alleen worden gegarandeerd via moderne verificatie. Er zijn scenario's waarin apps kunnen werken in een on-premises configuratie zonder moderne verificatie. De resultaten zijn echter niet consistent of gegarandeerd.

Raadpleeg de volgende artikelen voor meer informatie over het inschakelen van HMA voor hybride en on-premises configuraties van Skype voor bedrijven:

- **Hybride**<br>
[Hybride, moderne authenticatie voor SfB en Exchange wordt algemeen beschikbaar](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756)

- **On-premises**<br>
[Moderne authenticatie voor SfB On-premises met Azure AD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910)

### <a name="check-app-protection-policy-status"></a>De status van het app-beveiligingsbeleid controleren

Voer de volgende stappen uit om de beveiligingsstatus van uw app te controleren:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Bewaken** > **App-beveiligingsstatus** en vervolgens de tegel **Toegewezen gebruikers**.
3. Op de pagina **App-rapportage** selecteert u **Gebruiker selecteren** voor een lijst met gebruikers en groepen.
4. Zoek en selecteer een van de betrokken gebruikers in de lijst en selecteer vervolgens **Gebruiker selecteren**. Bovenaan het deelvenster App-rapportage ziet u of de gebruiker een licentie voor app-beveiliging heeft en over een licentie voor Microsoft 365 beschikt. U kunt ook de app-status voor alle apparaten van de gebruiker bekijken.
5. Noteer deze belangrijke informatie, zoals de beoogde apps, apparaattypen, beleidsregels, de incheckstatus van het apparaat en het laatste synchronisatietijdstip.

> [!NOTE]
> App-beveiligingsbeleid wordt alleen toegepast wanneer apps in de context van het werk worden gebruikt. Wanneer de gebruiker bijvoorbeeld apps opent met behulp van een werkaccount.

Zie [De configuratie van uw beveiligingsbeleid voor apps valideren in Microsoft Intune](../apps/app-protection-policies-validate.md) voor meer informatie.

### <a name="verify-that-user-identity-is-consistent-between-app-and-intune-app-sdk"></a>Controleren of de identiteit van de gebruiker in de app consistent is met Intune App SDK

In de meeste scenario's melden gebruikers zich aan bij hun accounts met behulp van hun user principal name (UPN). In sommige omgevingen (zoals in on-premises scenario's) kunnen gebruikers echter een andere vorm van aanmeldingsreferenties gebruiken. In dergelijke gevallen is het mogelijk dat de UPN die in de app wordt gebruikt, niet overeenkomt met het UPN-object in Azure AD. Als dit probleem zich voordoet, wordt het beveiligingsbeleid voor apps niet zoals verwacht toegepast.

Op basis van de best practices van Microsoft moet de UPN met het primaire SMTP-adres overeenkomen. Met deze procedure kunnen gebruikers zich dankzij een consistente identiteit aanmelden bij beheerde apps, Intune-beveiliging voor apps en andere Azure AD-resources. Zie [Azure AD UserPrincipalName-populatie](/azure/active-directory/connect/active-directory-aadconnect-userprincipalname)voor meer informatie.

Als voor uw omgeving alternatieve aanmeldingsmethoden zijn vereist, raadpleegt u [Een alternatieve aanmeldings-id configureren](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id), met name [HMA met alternatieve-id](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id#hybrid-modern-authentication-with-alternate-id).

### <a name="verify-that-the-user-is-targeted"></a>Controleren of het beleid op de gebruiker is gericht

Het Intune-beveiligingsbeleid voor apps moet zijn gericht op gebruikers. Als u geen app-beveiligingsbeleid aan een gebruiker of gebruikersgroep toewijst, wordt het beleid niet toegepast.

Voer de volgende stappen uit om te controleren of het beleid wordt toegepast op de beoogde gebruiker:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Controleren** > **Status app-beveiliging** en selecteer vervolgens de tegel **Gebruikersstatus** (op basis van het besturingssysteemplatform van het apparaat).
Selecteer in het geopende deelvenster **App-rapportage** de optie **Gebruiker selecteren** om naar een gebruiker te zoeken.
3. Selecteer de gebruiker uit de lijst. U kunt de gegevens van die gebruiker bekijken.

Wanneer u het beleid toewijst aan een gebruikersgroep, moet u ervoor zorgen dat de gebruiker zich in de gebruikersgroep bevindt. Volg hiervoor de volgende stappen:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Groepen > Alle groepen**, zoek vervolgens de groep op die wordt gebruikt voor de toewijzing van uw app-beveiligingsbeleid en selecteer deze.
3. Selecteer onder de sectie **Beheren** **Leden**.
4. Als de betrokken gebruiker niet wordt weergegeven, controleert u [Toegang tot apps en resources beheren met Azure Active Directory-groepen](/azure/active-directory/fundamentals/active-directory-manage-groups) en uw lidmaatschapsregels voor de groep. Controleer of de betrokken gebruiker deel uitmaakt van de groep.
5. Controleer of de betrokken gebruiker zich niet in een voor het beleid uitgesloten groep bevindt.

> [!IMPORTANT]
> - Het Intune-beveiligingsbeleid voor apps moet zijn toegewezen aan gebruikersgroepen en niet aan apparaatgroepen.
> - Als het betrokken apparaat gebruikmaakt van Apple Device Enrollment Program (DEP), moet u ervoor zorgen dat de optie **Gebruikersaffiniteit** is ingeschakeld. Gebruikersaffiniteit is vereist voor elke app die verificatie van gebruikers vereist volgens het DEP.
> - Als het betrokken apparaat gebruikmaakt van Android Enterprise, bieden alleen werkprofielen ondersteuning voor app-beveiligingsbeleid.


### <a name="verify-that-the-managed-app-is-targeted"></a>Controleren of het beleid op de beheerde app is gericht

Wanneer u Intune-beveiligingsbeleid voor apps configureert, moeten de beoogde apps gebruikmaken van [Intune App SDK](../developer/app-sdk-get-started.md). Als dat niet het geval is, werkt het beveiligingsbeleid voor apps mogelijk niet goed.

Zorg ervoor dat de beoogde app wordt weergegeven bij de [met Microsoft Intune beveiligde apps](../apps/apps-supported-intune-apps.md). Controleer ten aanzien van LOB-apps of aangepaste apps of de apps de nieuwste versie van [Intune app SDK](../developer/app-sdk-get-started.md) gebruiken, en let op het volgende:

Voor iOS is deze praktijk belangrijk, omdat elke versie oplossingen bevat die van invloed zijn op de manier waarop deze beleidsregels worden toegepast en hoe ze werken. Zie [iOS-releases van Intune App SDK](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios/releases) voor meer informatie.
Voor Android is deze praktijk niet zo belangrijk. Gebruikers moeten echter de nieuwste versie van de bedrijfsportal-app geïnstalleerd hebben, omdat de bedrijfsportal-app als broker-agent voor het beleid werkt.

> [!NOTE]
> Vanaf september 2019 biedt Intune ondersteuning voor iOS-apps met Intune App SDK 8.1.1 en nieuwere versies. Apps die zijn gebouwd met behulp van SDK-versies ouder dan 8.1.1 worden niet meer ondersteund. 

## <a name="more-information"></a>Meer informatie

### <a name="special-requirements-for-intune-mdm-managed-devices"></a>Speciale vereisten voor met MDM-beheerde apparaten in Intune

Wanneer u een app-beveiligingsbeleid maakt, kunt u dit richten op alle app-typen of aan de volgende app-typen:

- Apps op niet-beheerde apparaten
- Apps op door Intune beheerde apparaten
- Apps in Android-werkprofiel

> [!NOTE] 
> Als u de typen apps wilt opgeven, stelt u de optie **Doel voor alle app-typen** in op **Geen** en selecteert u deze vervolgens in de lijst **App-typen**.

Voor iOS zijn de volgende extra [app-configuratie-instellingen](../apps/app-configuration-policies-use-ios.md) vereist om de APP-instellingen (beveiligingsbeleid voor apps) te richten op apps op apparaten die zijn ingeschreven bij Intune:

- **IntuneMAMUPN** moet zijn geconfigureerd voor alle met MDM (Intune of EMM van derden) beheerde toepassingen. Zie UPN-gebruikersinstelling configureren voor Microsoft Intune of EMM van derden voor meer informatie.
- **IntuneMAMDeviceID** moet zijn geconfigureerd voor alle toepassingen van derden en met LOB MDM beheerde toepassingen.
- **IntuneMAMDeviceID** moet zijn geconfigureerd als apparaat-id-token. Bijvoorbeeld: key=IntuneMAMDeviceID, value={{deviceID}}. Zie [App-configuratiebeleidsregels toevoegen voor beheerde iOS-apparaten](../apps/app-configuration-policies-use-ios.md) voor meer informatie.
- Als alleen de waarde **IntuneMAMDeviceID** is geconfigureerd, wordt het apparaat in Intune APP beschouwd als niet-beheerd.

### <a name="scenario-policy-changes-are-not-working"></a>Scenario: Beleidswijzigingen werken niet
De [Intune App SDK](../developer/app-sdk-get-started.md) controleert regelmatig op beleidswijzigingen. Dit proces kan echter om een van de volgende redenen worden vertraagd:

- De app is niet ingecheckt bij de service.
- De bedrijfsportal-app is van het apparaat verwijderd.

Het Intune-beveiligingsbeleid voor apps is afhankelijk van de identiteit van de gebruiker. Daarom is een geldige aanmelding waarbij gebruik wordt gemaakt van een werk- of schoolaccount voor de app en een consistente verbinding met de service vereist. Als de gebruiker niet is aangemeld bij de app, of als de bedrijfsportal-app is verwijderd van het apparaat, zijn beleidsupdates niet van toepassing.

Het kan bovendien 8 uur duren voordat wijzigingen in en updates voor het app-beveiligingsbeleid worden toegepast. Indien van toepassing, wordt de beleidsupdate doorgaans eerder toegepast wanneer alle apps worden gesloten en het apparaat opnieuw wordt opgestart.

Voer de volgende stappen uit om de beveiligingsstatus van de app te controleren:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Bewaken** > **App-beveiligingsstatus** en vervolgens de tegel **Toegewezen gebruikers**.
3. Op de pagina App-rapportage selecteert u **Gebruiker selecteren** om een lijst met gebruikers en groepen te openen.
4. Zoek en selecteer een van de betrokken gebruikers in de lijst en selecteer vervolgens **Gebruiker selecteren**.
5. Controleer de beleidsregels die momenteel zijn toegepast, met inbegrip van de status en de laatste synchronisatietijd.
6. Als de status **niet ingecheckt** is of als in de weergave wordt aangegeven dat er geen recente synchronisatie heeft plaatsgevonden, controleert u of de gebruiker een consistente netwerkverbinding heeft. Zorg er ten aanzien van Android-gebruikers voor dat de meest recente versie van de bedrijfsportal-app bij hen is geïnstalleerd.

> [!IMPORTANT]
> De [Intune App SDK](../developer/app-sdk-get-started.md) controleert elke 30 minuten op selectief wissen. Wijzigingen in het bestaande beleid voor gebruikers die al zijn aangemeld, worden echter niet meer dan acht uur weergegeven. Als u dit proces wilt versnellen, laat u de gebruiker zich afmelden bij de app en zich vervolgens opnieuw aanmelden of laat u deze het apparaat opnieuw opstarten.

Het Intune-beveiligingsbeleid voor apps bevat ondersteuning voor meerdere identiteiten. Intune kan het beveiligingsbeleid voor apps alleen toepassen op het werk- of schoolaccount dat is aangemeld bij de app. Er wordt echter slechts één werk- of schoolaccount per apparaat ondersteund.

### <a name="scenario-the-policy-is-applied-but-ios-users-can-still-transfer-work-files-to-unmanaged-apps"></a>Scenario: Het beleid wordt toegepast, maar iOS-gebruikers kunnen nog wel werkbestanden overdragen aan niet-beheerde apps
Met de functie **Open-In-beheer** (![Open-In-knop](media/troubleshoot-app-protection/troubleshoot-app-protection.jpg)) voor iOS-apparaten wordt de bestandsoverdracht beperkt tussen apps die zijn geïmplementeerd via het MDM-kanaal. De gebruiker kan mogelijk werkbestanden van beheerde locaties, zoals OneDrive en Exchange, overdragen naar onbeheerde apps of locaties, afhankelijk van de configuratie. De iOS-functie **Open-In-beheer** werkt buiten andere methoden voor gegevensoverdracht. Daarom is dit niet van invloed op de instellingen **Opslaan als** en **Kopiëren/plakken**.

U kunt Intune-beveiligingsbeleid voor apps gebruiken met de beheerde iOS-functie **Open-in-beheer** om bedrijfsgegevens op de volgende manieren te beveiligen:

- **Apparaten die eigendom zijn van werknemers en die niet worden beheerd met een MDM-oplossing:** : u kunt de app-beveiligingsbeleidsinstellingen instellen op **App toestaan om alleen gegevens over te dragen naar door beleid beheerde apps**. Het op deze manier geconfigureerde **Open-In**-gedrag in een door beleid beheerde app biedt alleen andere door beleid beheerde apps als opties voor delen. Als een gebruiker bijvoorbeeld een beveiligd bestand als bijlage van OneDrive via de systeemeigen e-mail-app probeert te verzenden, is dat bestand onleesbaar.

- **Apparaten die worden beheerd door MDM-oplossingen**: Voor apparaten die zijn ingeschreven bij Intune of externe MDM-oplossingen, wordt het delen van gegevens tussen apps met behulp van app-beveiligingsbeleid en andere beheerde iOS-apps die via MDM zijn geïmplementeerd, beheerd door Intune APP en de iOS-functie **Open-In-beheer**.<br/><br/>
Als u ervoor wilt zorgen dat apps die u implementeert met behulp van een MDM-oplossing, ook onderhevig zijn aan het app-beveiligingsbeleid in Intune, configureert u de UPN-gebruikersinstelling zoals beschreven in [UPN-gebruikersinstelling configureren](../apps/data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm).<br/><br/>Als u wilt opgeven hoe u gegevensoverdracht naar andere apps wilt toestaan, schakelt u **Organisatiegegevens naar andere apps verzenden** in en selecteert u vervolgens het gewenste deelniveau.<br/><br/>Als u wilt opgeven hoe u apps wilt toestaan om gegevens te ontvangen van andere apps, schakelt u **Organisatiegegevens naar andere apps verzenden** in en selecteert u vervolgens het gewenste niveau voor het ontvangen van gegevens.

Zie [Instellingen voor herlocatie van gegevens](../apps/app-protection-policy-settings-ios.md#data-protection) voor meer informatie over het ontvangen en delen van app-gegevens.

Zie [Gegevensoverdracht beheren tussen iOS-apps met Microsoft Intune](../apps/data-transfer-between-apps-manage-ios.md) voor meer informatie.

## <a name="references"></a>Verwijzingen

Als u nog steeds op zoek bent naar een oplossing voor een verwant probleem, of als u meer informatie wilt over Intune, plaatst u een vraag op ons [Microsoft Intune-forum](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Veel ondersteuningstechnici, MVP's en leden van ons ontwikkelteam bezoeken de forums. Daarom is er een goede kans dat u iemand kunt vinden met de informatie die u nodig hebt.

Als u een ondersteuningsaanvraag van het Microsoft Intune-productondersteuningsteam wilt openen, raadpleegt u [Ondersteuning krijgen voor Microsoft Intune](../fundamentals/get-support.md).

Raadpleeg de volgende artikelen voor meer informatie over het Intune-beveiligingsbeleid voor apps:

- [Problemen met Mobile Application Management oplossen](../apps/troubleshoot-mam.md)
- [Veelgestelde vragen over MAM en app-beveiliging](../apps/mam-faq.md)
- [Ondersteuningstip: Problemen met het Intune-beveiligingsbeleid voor apps oplossen met behulp van logboekbestanden op lokale apparaten](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-Intune-app-protection-policy-using/ba-p/330372)

Ga naar onze officiële blogs voor al het laatste nieuws, informatie en technische tips:

- [The Microsoft Intune Support Team blog](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess) (De blog van het ondersteuningsteam van Microsoft Intune)
- [The Microsoft Enterprise Mobility and Security blog](https://cloudblogs.microsoft.com/enterprisemobility) (De blog over Microsoft Enterprise Mobility and Security)

## <a name="next-steps"></a>Volgende stappen

- Raadpleeg [De portal voor probleemoplossing gebruiken om gebruikers in uw bedrijf te helpen](../fundamentals/help-desk-operators.md) voor meer informatie over probleemoplossing met Intune. 
- Ontdek meer over bekende problemen in Microsoft Intune. Zie [Intune-klantsucces](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess) voor meer informatie.
- Extra hulp nodig? Zie [Ondersteuning voor Microsoft Intune krijgen](../fundamentals/get-support.md).