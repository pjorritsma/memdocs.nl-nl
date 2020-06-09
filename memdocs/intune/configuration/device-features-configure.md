---
title: iOS-/iPadOS- of macOS-apparaatprofielen maken met Microsoft Intune - Azure | Microsoft Docs
description: Een profiel voor een iOS-, iPadOS- of macOS-apparaat maken. Instellingen voor AirPrint, de indeling van het startscherm, appmeldingen, gedeelde apparaten, eenmalige aanmelding en het filteren van webinhoud, in Microsoft Intune configureren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 349fdc7b0f13f0999b8c9993bcaba1d458ebac59
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989188"
---
# <a name="add-ios-ipados-or-macos-device-feature-settings-in-intune"></a>Instellingen van apparaatfuncties voor iOS, iPadOS of macOS toevoegen in Intune

Intune bevat veel functies en instellingen waarmee beheerders iOS, iPadOS en macOS-apparaten kunnen beheren. Beheerders kunnen bijvoorbeeld het volgende:

- Gebruikers toegang toestaan tot de AirPrint-printers in uw netwerk
- Apps en mappen toevoegen aan het startscherm, inclusief het toevoegen van nieuwe pagina's
- Kiezen of en hoe app-meldingen worden weergegeven
- Het vergrendelingsscherm configureren voor weergave van een bericht of de inventaristag, met name voor gedeelde apparaten
- Gebruikers beveiligde eenmalige aanmelding bieden om referenties tussen apps te kunnen delen
- Websites filteren waarop grof taalgebruik wordt gebruikt en specifieke websites toestaan of blokkeren

Intune maakt gebruik van configuratieprofielen om deze instellingen te maken voor en af te stemmen op de behoeften van uw organisatie. Nadat u deze functies aan een profiel hebt toegevoegd, kunt u het profiel pushen naar en implementeren op iOS-/iPadOS- en macOS-apparaten in uw organisatie.

In dit artikel wordt beschreven welke functies u kunt configureren en hoe u een apparaatconfiguratieprofiel kunt maken. U ziet ook de beschikbare instellingen voor [iOS-/iPadOS](ios-device-features-settings.md)- en [macOS](macos-device-features-settings.md)-apparaten.

## <a name="airprint"></a>AirPrint

AirPrint is een Apple-functie waarmee apparaten kunnen afdrukken naar bestanden via een draadloos netwerk. In Intune kunt u AirPrint-gegevens toevoegen aan apparaten.

Zie [AirPrint op iOS/iPadOS](ios-device-features-settings.md#airprint) en [AirPrint op macOS](macos-device-features-settings.md#airprint) voor een lijst met instellingen die u kunt configureren in Intune.

Zie [Over AirPrint](https://support.apple.com/HT201311) op de website van Apple voor meer informatie over AirPrint.

Van toepassing op:

- iOS 7.0 en hoger
- iPadOS 13.0 en hoger
- macOS 10.10 en hoger

## <a name="app-notifications"></a>App-meldingen

Kies hoe apps op uw iOS- en iPadOS-apparaten meldingen ontvangen. U kunt bijvoorbeeld appmeldingen verzenden, zodat deze in het meldingencentrum of op het vergrendelingsscherm worden weergegeven of een geluid afspelen.

Zie [App-meldingen op iOS/iPadOS](ios-device-features-settings.md#app-notifications) voor een lijst met instellingen die u kunt configureren in Intune.

Zie [Meldingen](https://developer.apple.com/notifications/) op de website van Apple voor meer informatie over deze functie.

Van toepassing op:

- iOS 9.3 en hoger
- iPadOS 13.0 en hoger

## <a name="associated-domains"></a>Gekoppelde domeinen

Hiermee kunt u een relatie maken tussen uw apps en uw domeinen, zoals `contoso.com`. Met deze functie kunt u het volgende doen:

- Gegevens en aanmeldingsgegevens tussen apps en websites in uw organisatie delen.
- App-functies gebruiken die zijn gebaseerd op uw website, zoals een app-extensie voor eenmalige aanmelding, universele koppelingen en het automatisch invullen van wachtwoorden.

  Maak bijvoorbeeld een gekoppeld domein zodat aanmeldingsgegevens, zoals een wachtwoord, automatisch kunnen worden ingevuld voor websites die aan uw app zijn gekoppeld.

Zie [Gekoppelde domeinen op macOS](macos-device-features-settings.md#associated-domains) voor een lijst met instellingen die u kunt configureren in Intune.

Zie [Setting Up an App’s Associated Domains](https://developer.apple.com/documentation/security/password_autofill/setting_up_an_app_s_associated_domains) (gekoppelde domeinen van een app instellen) op de website van Apple voor meer informatie over deze functie.

Van toepassing op:

- macOS 10.15 of hoger

## <a name="home-screen-layout"></a>Indeling van het startscherm

Met deze instellingen configureert u de indeling van apps en mappen in de dock en het startscherm van iOS- en iPadOS-apparaten. U kunt het volgende doen:

- Gebruik de **dock**-instellingen om apps of mappen aan het scherm toe te voegen. U kunt bijvoorbeeld Safari en de app Mail in de dock van het apparaat weergeven.
- Voeg de **pagina's** toe die u wilt weergeven op het startscherm en de apps die moeten worden weergegeven op elke pagina. Voeg bijvoorbeeld de pagina **Contoso** toe, en voeg vervolgens de app Instellingen toe op deze pagina.

Zie [Indeling van startscherm op iOS/iPadOS](ios-device-features-settings.md#home-screen-layout) voor een lijst met instellingen die u kunt configureren in Intune.

Van toepassing op:

- iOS 9.3 en hoger
- iPadOS 13.0 en hoger

## <a name="lock-screen-message"></a>Bericht voor vergrendelingsscherm

Gebruik deze instellingen om een aangepast bericht of aangepaste tekst in het aanmeldingsvenster en vergrendelingsscherm weer te geven. U kunt bijvoorbeeld een bericht weergeven met de tekst 'Indien gevonden, graag contact opnemen met...' en informatie over de assettag weergeven.

Zie [Instellingen voor vergrendelingsscherm op iOS/iPadOS](ios-device-features-settings.md#lock-screen-message) voor een lijst met instellingen die u kunt configureren in Intune.

Zie [LockScreenMessage](https://developer.apple.com/documentation/devicemanagement/lockscreenmessage) op de website van Apple voor meer informatie over het bericht voor het vergrendelingsscherm.

Van toepassing op:

- iOS 9.3 en hoger
- iPadOS 13.0 en hoger

## <a name="login-items"></a>Aanmeldingsitems

Met deze functie kunt u kiezen welke apps, aangepaste apps, bestanden en mappen worden geopend wanneer gebruikers zich aanmelden bij de apparaten.

Zie [Aanmeldingsitems op macOS](macos-device-features-settings.md#login-items) voor een lijst met instellingen die u kunt configureren in Intune.

Van toepassing op:

- macOS 10.13 en hoger

## <a name="login-window"></a>Aanmeldingsvenster

Hiermee bepaalt u de weergave van het aanmeldingsscherm en de beschikbare functies voor gebruikers voordat ze zich aanmelden. U kunt bijvoorbeeld een banner toevoegen met een aangepast bericht, kiezen of de slaapstandknop wordt weergegeven en nog veel meer.

Zie [Aanmeldingsvenster op macOS](macos-device-features-settings.md#login-window) voor een lijst met instellingen die u kunt configureren in Intune.

Van toepassing op:

- macOS 10.7 en hoger

## <a name="single-sign-on"></a>Eenmalige aanmelding

De meeste LOB-apps (Line-Of-Business) vereisen een zekere mate van gebruikersverificatie om beveiliging te ondersteunen. In veel gevallen moeten gebruikers bij de verificatie herhaaldelijk dezelfde referenties invoeren. Ontwikkelaars kunnen apps maken die gebruikmaken van eenmalige aanmelding (SSO) ter verbetering van de gebruikerservaring. Met eenmalige aanmelding hoeft een gebruiker minder vaak referenties in te voeren.

Het profiel voor eenmalige aanmelding is gebaseerd op Kerberos. Kerberos is een netwerkverificatieprotocol waarbij gebruik wordt gemaakt van geheime-sleutelcryptografie om client-servertoepassingen te verifiëren. De Intune-instellingen definiëren Kerberos-accountgegevens wanneer er toegang wordt verkregen tot servers of opgegeven apps, en verwerken Kerberos-vragen voor webpagina's en systeemeigen apps. Apple raadt u aan de instellingen van de [Kerberos SSO-app-extensie](#single-sign-on-app-extension) (in dit artikel) in plaats van de SSO-instellingen te gebruiken.  

Voor het gebruik van eenmalige aanmelding, moet u over het volgende beschikken:

- Een app die is gecodeerd om te zoeken naar de gebruikersreferentieopslagplaats in eenmalige aanmelding op het apparaat.
- Intune geconfigureerd voor eenmalige aanmelding vanaf iOS-/iPadOS-apparaten.

Zie [Eenmalige aanmelding op iOS/iPadOS](ios-device-features-settings.md#single-sign-on) voor een lijst met instellingen die u kunt configureren in Intune.

Van toepassing op:

- iOS 7.0 en hoger
- iPadOS 13.0 en hoger

## <a name="single-sign-on-app-extension"></a>App-extensie voor eenmalige aanmelding

Met deze instellingen configureert u een app-extensie die eenmalige aanmelding (SSO) voor uw iOS-, iPadOS- en macOS-apparaten mogelijk maakt. De meeste LOB-apps (Line-Of-Business) vereisen een zekere mate van beveiligde gebruikersverificatie. In veel gevallen moeten gebruikers bij de verificatie herhaaldelijk dezelfde referenties invoeren. Met SSO hebben gebruikers toegang tot apps en websites nadat ze hun referenties eenmaal hebben ingevoerd. SSO biedt gebruikers ook een betere authenticatie-ervaring en vermindert het aantal herhaalde prompts voor referenties.

Gebruik deze instellingen in Intune voor het configureren van een SSO-app-extensie die is gemaakt door uw organisatie, uw id-provider, Microsoft of Apple. Met de SSO-app-extensie wordt de verificatie voor uw gebruikers afgehandeld. Met deze instellingen worden het omleidingstype en de SSO-app-extensies voor het referentietype geconfigureerd.

- Het omleidingstype is ontworpen voor moderne verificatieprotocollen, zoals OpenID Connect, OAuth en SAML2. U kunt een algemene omleidingsextensie gebruiken op macOS-apparaten. Voor iOS- en iPadOS-apparaten kunt u kiezen tussen de Azure AD SSO-extensie van Microsoft ([Microsoft Enterprise SSO-invoegtoepassing](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin)) en een algemene omleidingsextensie.
- Het referentietype is ontworpen voor verificatiestromen met vraag en antwoord. U kunt kiezen tussen een Kerberos-referentie-extensie van Apple en een algemene referentie-extensie.

Zie [SSO-app-extensie voor iOS/iPadOS](ios-device-features-settings.md#single-sign-on-app-extension) en [SSO-app-extensie voor macOS](macos-device-features-settings.md#single-sign-on-app-extension) voor een lijst met instellingen die u kunt configureren in Intune.

Bekijk [Extensible Enterprise SSO](https://developer.apple.com/videos/play/tech-talks/301) op de website van Apple voor meer informatie over het ontwikkelen van een SSO-app-extensie. Als u de beschrijving van Apple over de functie wilt lezen, gaat u naar [Instellingen voor de payload 'Extensies eenmalige aanmelding'](https://support.apple.com/guide/mdm/single-sign-on-extensions-mdmfd9cdf845/web). 

> [!NOTE]
> De functie **App-extensie voor eenmalige aanmelding** is niet hetzelfde als de functie **Eenmalige aanmelding**:
>
> - De instellingen van **App-extensie voor eenmalige aanmelding** zijn van toepassing op iPadOS 13.0 (en hoger), iOS 13.0 (en hoger) en macOS 10.15 (en hoger). De instellingen van **Eenmalige aanmelding** zijn van toepassing op iPadOS 13.0 (en hoger) en iOS 7.0 en hoger.
>
> - Met de **app-extensie voor eenmalige aanmelding** kunt u extensies definiëren voor gebruik door id-providers of organisaties om een naadloze zakelijke aanmeldingservaring te bieden. In de instellingen voor **Eenmalige aanmelding** worden Kerberos-accountgegevens gedefinieerd voor toegang van gebruikers tot servers of apps.
>
> - De **app-extensie voor eenmalige aanmelding** maakt gebruik van het Apple-besturingssysteem voor de verificatie. Zo kan dus een eindgebruikerservaring worden geboden die beter is dan die van **eenmalige aanmelding**.
>
> - Vanuit het oogpunt van ontwikkeling is een **app-extensie voor eenmalige aanmelding** weer beter, omdat u dan elk type referenties voor omleiding van eenmalige aanmelding of eenmalige aanmelding voor verificatie kunt gebruiken. Bij **Eenmalige aanmelding** kunt u alleen gebruikmaken van Kerberos-verificatie.
>
> - De Kerberos-**app-extensie voor eenmalige aanmelding** is ontwikkeld door Apple en is ingebouwd in de iOS/iPadOS 13.0+- en macOS 10.15+-platforms. De ingebouwde Kerberos-uitbreiding kan worden gebruikt om gebruikers te registreren in systeemeigen apps en websites die ondersteuning bieden voor Kerberos-verificatie. **Eenmalige aanmelding** is geen Apple-implementatie van Kerberos.
>
> - Met de ingebouwde Kerberos-**app-extensie voor eenmalige aanmelding** worden Kerberos-vragen voor webpagina's en apps op dezelfde manier behandeld als **eenmalige aanmelding**. De ingebouwde Kerberos-extensie ondersteunt echter wachtwoordwijzigingen en is geschikter voor bedrijfsnetwerken. Als moet worden gekozen tussen de Kerberos-**app-extensie voor eenmalige aanmelding** en **eenmalige aanmelding**, wordt aanbevolen de extensie te gebruiken vanwege verbeterde prestaties en mogelijkheden.

Van toepassing op:

- iOS 13.0 en hoger
- iPadOS 13.0 en hoger
- macOS 10.15 of hoger

## <a name="wallpaper"></a>Achtergrond

Een aangepaste PNG-, JPG- of JPEG-afbeelding toevoegen aan uw onder supervisie staande iOS-/iPadOS-apparaten. U kunt bijvoorbeeld Intune gebruiken om een bedrijfslogo toe te voegen aan het vergrendelingsscherm op uw apparaten.

Zie [Achtergrond op iOS/iPadOS](ios-device-features-settings.md#wallpaper) voor een lijst met instellingen die u kunt configureren in Intune.

Van toepassing op:

- iOS
- iPadOS 13.0 en hoger

## <a name="web-content-filter"></a>Webinhoudsfilter

Met deze instellingen wordt het ingebouwde AutoFilter-algoritme van Apple gebruikt om webpagina's te evalueren en inhoud voor volwassenen te blokkeren. U kunt ook een lijst met toegestane en beperkte webkoppelingen maken. U kunt bijvoorbeeld instellen dat alleen websites van `contoso` mogen worden geopend.

Zie [Webinhoudsfilter op iOS/iPadOS](ios-device-features-settings.md#web-content-filter) voor een lijst met instellingen die u kunt configureren in Intune.

Van toepassing op:

- iOS 7.0 en hoger
- iPadOS 13.0 en hoger

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Kies het platform van uw apparaten. Uw opties zijn:  

        - **iOS/iPadOS**
        - **macOS**

    - **Profiel**: Selecteer **Apparaatfuncties**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **macOS: Aanmeldingsscherm configureren**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Kies uw platform voor gedetailleerde instellingen:

    - [iOS/iPadOS](ios-device-features-settings.md)
    - [macOS](macos-device-features-settings.md)

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt mogelijk nog niets. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

Bekijk alle instellingen voor apparaatfuncties voor [iOS-/iPadOS](ios-device-features-settings.md)- en [macOS](macos-device-features-settings.md)-apparaten.
