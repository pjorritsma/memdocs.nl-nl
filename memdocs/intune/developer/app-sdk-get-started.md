---
title: Aan de slag met de Microsoft Intune App SDK
description: Maak uw mobiele app snel geschikt voor Mobile Application Management (MAM) met Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 38ebd3f5-cfcc-4204-8a75-6e2f162cd7c1
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52dd81efb13bcfcda02c8574e065814f49b5564c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911842"
---
# <a name="get-started-with-the-microsoft-intune-app-sdk"></a>Aan de slag met de Microsoft Intune App SDK

Met deze handleiding kunt u uw mobiele app snel geschikt maken voor ondersteuning van het beleid voor app-beveiliging met Microsoft Intune. Wellicht vindt u het handig om eerst inzicht te krijgen in de voordelen van de Intune App SDK, zoals uitgelegd in [Overzicht van de Intune App SDK](app-sdk.md).

De Intune App SDK biedt ondersteuning voor vergelijkbare scenario's op iOS en Android, en is ervoor bedoeld om een consistente ervaring voor IT-beheerders te leveren op de verschillende platformen. Er zijn kleine verschillen in de ondersteuning van bepaalde functies vanwege vrschillen tussen en beperkingen van de platformen.

## <a name="register-your-store-app-with-microsoft"></a>Uw Store-app registreren bij Microsoft

### <a name="if-your-app-is-internal-to-your-organization-and-will-not-be-publicly-available"></a>Als uw app alleen intern in uw organisatie wordt gebruikt en niet openbaar beschikbaar wordt gesteld, geldt het volgende:

U hoeft uw app _**niet**_ te registreren. Voor interne [line-Of-Business-apps (LOB)](../apps/apps-add.md#app-types-in-microsoft-intune) die zijn geschreven door of voor uw bedrijf implementeert de IT-beheerder de app intern. Intune detecteert dat de app is gemaakt met de SDK waarna de IT-beheerder het beleid voor app-beveiliging erop kan toepassen. U kunt verdergaan naar de sectie [Uw mobiele iOS- of Android-app geschikt maken voor beleid voor app-beveiliging](#enable-your-ios-or-android-app-for-app-protection-policy).

### <a name="if-your-app-will-be-released-to-a-public-app-store-like-the-apple-app-store-or-google-play"></a>Als uw app wordt uitgebracht in een openbare app-store, zoals de Apple App Store of Google Play, geldt het volgende:

U _**moet**_ uw app eerst registreren bij Microsoft Intune en akkoord gaan met de voorwaarden van de registratie. Na de registratie kunnen IT-beheerders een beleid voor app-beveiliging toepassen op de beheerde app, die wordt vermeld als met [Intune beveiligde app-partner](../apps/apps-supported-intune-apps.md#partner-apps).

Zolang de registratie nog niet is voltooid en bevestigd door het team van Microsoft Intune, krijgen Intune-beheerders nog niet de mogelijkheid om beleid voor app-beveiliging toe te passen op de dieptekoppeling van uw app. Uw app wordt ook toegevoegd aan de [pagina voor Microsoft Intune-partners](https://www.microsoft.com/cloud-platform/microsoft-intune-apps). Op deze pagina wordt het pictogram van uw app weergegeven om aan te geven dat de app het Intune-beleid voor app-beveiliging ondersteunt.

### <a name="the-registration-process"></a>Het registratieproces
Als u aan het registratieproces wilt beginnen en u nog niet werkt met een Microsoft-contactpersoon, vult u de [enquête voor Microsoft Intune-app-partners](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR80SNPjnVA1KsGiZ89UxSdVUMEpZNUFEUzdENENOVEdRMjM5UEpWWjJFVi4u) in.

De e-mailadressen die u vermeldt in uw antwoorden, worden gebruikt om contact met u op te nemen voor het vervolg van het registratieproces. Ook wordt het e-mailadres voor registratie gebruikt om contact met u op te nemen bij verdere vragen.

> [!NOTE]
> Op alle gegevens die via de vragenlijst en via e-mailcorrespondentie met het Microsoft Intune-team worden verzameld, is de [privacyverklaring van Microsoft](https://www.microsoft.com/privacystatement/default.aspx) van toepassing.

**Wat u tijdens het registratieproces kunt verwachten**:

1. Nadat u de vragenlijst hebt verzonden, wordt er via het e-mailadres voor registratie contact met u opgenomen om de ontvangst te bevestigen of om aanvullende informatie te vragen waarmee de registratie kan worden voltooid.

2. Nadat alle benodigde informatie is ontvangen, ontvangt u de Overeenkomst voor app-partners van Microsoft Intune ter ondertekening. In deze overeenkomst worden de voorwaarden beschreven die uw bedrijf moet accepteren voordat u een app-partner van Microsoft Intune kunt worden.

3. U ontvangt een bericht wanneer de registratie van uw app bij de Microsoft Intune-service is geslaagd en wanneer uw app wordt weergegeven op de site voor [Microsoft Intune-partners](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).

4. Tot slot wordt de dieptekoppeling voor uw app toegevoegd aan de volgende maandelijkse service-update voor Intune. Als u de registratiegegevens bijvoorbeeld in juli hebt ingevuld, wordt de dieptekoppeling vanaf half augustus ondersteund.

De dieptekoppeling is de koppeling naar de vermelding van uw app in de openbare App Store. Als de dieptekoppeling voor uw app in de Store in de toekomst wordt gewijzigd, moet u de app opnieuw registreren.

> [!NOTE]
> U moet het ons laten weten als u uw app bijwerkt naar een nieuwe versie van de Intune App SDK.

## <a name="download-the-sdk-files"></a>De SDK-bestanden downloaden

De SDK's voor Intune-apps voor systeemeigen iOS en Android worden gehost op een Microsoft GitHub-account. De volgende openbare opslagplaatsen bevatten de SDK-bestanden voor respectievelijk systeemeigen iOS en Android:

* [SDK voor Intune-apps voor iOS](https://github.com/msintuneappsdk/ms-intune-app-sdk-ios)
* [SDK voor Intune-apps voor Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android)

Als uw app een Xamarin-app is, gebruikt u deze SDK-variant:

* [Microsoft Intune App SDK Xamarin Bindings](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)

Het is verstandig om u te registreren voor een GitHub-account waarmee u splitsingen en pulls vanuit de opslagplaatsen kunt uitvoeren. Met GitHub kunnen ontwikkelaars communiceren met het productteam, problemen melden en snel antwoord ontvangen, opmerkingen bij de release bekijken en feedback naar Microsoft verzenden. Voor vragen over de GitHub van de Intune App SDK kunt u contact opnemen met msintuneappsdk@microsoft.com.

## <a name="enable-your-ios-or-android-app-for-app-protection-policy"></a>Uw mobiele iOS- of Android-app geschikt maken voor beleid voor app-beveiliging

U hebt een van de volgende handleidingen voor ontwikkelaars nodig om de App Intune SDK te integreren in uw app:

* **[Ontwikkelaarshandleiding voor Intune App SDK voor iOS](app-sdk-ios.md)** : in dit document wordt u stapsgewijs begeleid bij het geschikt maken van uw systeemeigen iOS-app voor de Intune App SDK.

* **[Ontwikkelaarshandleiding voor Intune App SDK voor Android](app-sdk-android.md)** : in dit document wordt u stapsgewijs begeleid bij het geschikt maken van uw systeemeigen Android-app voor de Intune App SDK.

* **[Handleiding voor Intune App SDK Xamarin Bindings](app-sdk-xamarin.md)** : dit document bevat informatie over het maken van iOS- en Android-apps met Xamarin voor het beveiligingsbeleid voor apps in Intune.



## <a name="enable-your-ios-or-android-app-for-app-based-conditional-access"></a>Uw mobiele iOS- of Android-app geschikt maken voor voorwaardelijke toegang op basis van een app

Als u uw app geschikt hebt gemaakt voor het app-beveiligingsbeleid, is daarnaast het volgende vereist voor uw app om deze correct te laten functioneren met voorwaardelijke toegang op basis van een app voor Azure ActiveDirectory (AAD):

* De app is gebouwd met de [Azure Active Directory-verificatiebibliotheek](/azure/active-directory/develop/active-directory-authentication-libraries) en geschikt gemaakt voor AAD Broker-verificatie.

* De [AAD-client-id](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#configure-a-native-client-application) voor uw app moet uniek zijn voor de iOS- en Android-platformen.

## <a name="configure-telemetry-for-your-app"></a>Telemetrie configureren voor uw app

Met Microsoft Intune worden gebruiksstatistieken verzameld voor uw app.

* **Intune App SDK voor iOS**: de SDK registreert standaard SDK-telemetriegegevens voor gebruiksgebeurtenissen. Deze gegevens worden naar Microsoft Intune verzonden.

  * Als u ervoor kiest geen SDK-telemetriegegevens vanuit uw app naar Microsoft Intune te verzenden, moet u het vastleggen van telemetriegegevens uitschakelen door 'JA' in te schakelen voor de eigenschap `MAMTelemetryDisabled` in het IntuneMAMSettings-woordenboek .

* **Intune App SDK voor Android**: De Intune App SDK voor Android beheert niet de gegevensverzameling vanuit uw app. De bedrijfsportal-app registreert standaard telemetriegegevens. Deze gegevens worden naar Microsoft Intune verzonden. Geheel volgens het Microsoft-beleid worden er geen persoonsgegevens verzameld. 

  * Als eindgebruikers ervoor kiezen deze gegevens niet te verzenden, moeten ze telemetrie uitschakelen onder Instellingen op de bedrijfsportal-app. Zie [Gegevensverzameling door Microsoft uitschakelen](../user-help/turn-off-microsoft-usage-data-collection-android.md) voor meer informatie. 

## <a name="line-of-business-app-version-numbers"></a>Versienummers van line-of-business-apps

In line-of-business-apps in Intune wordt nu het versienummer getoond voor iOS- en Android-apps. Het nummer wordt in de Azure Portal in de app-lijst en in de blade App-overzicht getoond. Eindgebruikers kunnen het app-nummer in de bedrijfsportal-app en in de webportal zien.

### <a name="full-version-number"></a>Volledig versienummer

Het volledige versienummer duidt een specifieke release van de app aan. Het nummer wordt weergegeven als _Versie_(_Build_). Bijvoorbeeld 2.2(2.2.17560800). 

Het volledige versienummer bevat twee onderdelen:

- **Versie**  
  Het versienummer is het door mensen leesbare releasenummer van de app. Dit wordt door eindgebruikers gebruikt om de verschillende releases van de app aan te duiden.

- **Buildnummer**  
  Het buildnummer is een intern nummer dat voor de detectie van apps en het beheer van apps via een programma kan worden gebruikt. Het buildnummer verwijst naar een iteratie van de app die refereert aan wijzigingen in de code.

### <a name="version-and-build-number-in-android-and-ios"></a>Versie- en buildnummer in Android en iOS

Zowel Android als iOS gebruiken versie- en buildnummers ter verwijzing naar apps. Beide besturingssystemen bevatten echter betekenissen die specifiek zijn voor het besturingssysteem. De volgende tabel biedt een verklaring van de samenhang van deze termen.

Let op dat u zowel het versie- als het buildnummer gebruikt wanneer u een line-of-business-app ontwikkelt voor gebruik in Intune. Beheereigenschappen van een Intune-app zijn afhankelijk van een zinvolle **CFBundleVersion** (voor iOS) en **PackageVersionCode** (voor Android). Deze nummers zijn opgenomen in het app-manifest. 

Intune|iOS|Android|Beschrijving|
|---|---|---|---|
Versienummer|CFBundleShortVersionString|PackageVersionName |Dit nummer geeft een specifieke release van de app aan voor eindgebruikers.|
Buildnummer|CFBundleVersion|PackageVersionCode |Met dit nummer wordt een iteratie in de app-code aangegeven.|

#### <a name="ios"></a>iOS

- **CFBundleShortVersionString**  
  Hiermee wordt het releaseversienummer van de bundel opgegeven. Dit nummer duidt een releaseversie van de app aan. Met dit nummer kunnen eindgebruikers aan de app refereren.
- **CFBundleVersion**  
  De buildversie van de bundel, die een iteratie van de bundel aanduidt. Het nummer duidt eventueel een release of een releasebundel aan. Met dit nummer vindt detectie van apps plaats.

#### <a name="android"></a>Android

- **PackageVersionName**  
  Het versienummer dat zichtbaar is voor gebruikers. Dit kenmerk kan als onbewerkte tekenreeks of als referentie aan een tekenreeksbron worden ingesteld. De tekenreeks is enkel bedoeld om aan gebruikers te worden getoond.
- **PackageVersionCode**  
  Een intern versienummer. Dit nummer wordt alleen gebruikt om te bepalen of een versie meer recent is dan een andere, waarbij hogere nummers meer recente versies aangeven. Dit is niet de versie 

## <a name="next-steps-after-integration"></a>Vervolgstappen na de integratie

### <a name="test-your-app"></a>Uw app testen
Nadat u de benodigde stappen hebt uitgevoerd om uw iOS- of Android-app te integreren met de Intune App SDK, moet u ervoor zorgen dat alle beleid voor app-beveiliging is ingeschakeld en correct werkt voor de gebruiker en de IT-beheerder. Als u uw geïntegreerde app wilt testen, gaat u als volgt te werk:

* **Microsoft Intune-testaccount**: als u uw door Intune beheerde app wilt testen aan de hand van beveiligingsfuncties voor apps in Intune, hebt u een Microsoft Intune-account nodig.

  * Als u een ISV bent die apps voor de iOS of Android Store wilt inschakelen voor Intune-beleid voor app-beveiliging, ontvangt u een promotiecode nadat u de registratie bij Microsoft Intune hebt voltooid. Dit wordt beschreven in de registratiestap. Met de promotiecode kunt u zich aanmelden voor een Microsoft Intune-proefversie met uitgebreid gebruik van één jaar.

  * Als u een Line-Of-Business-app ontwikkelt die niet naar de Store word verzonden, wordt ervan uitgegaan dat u via uw organisatie toegang hebt tot Microsoft Intune. U kunt zich ook registreren voor een gratis proefversie van één maand via [Microsoft Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0).

  * Zorg ervoor, als u uw app op een mobiel apparaat met een eindgebruikeraccount test, dat u dat account een Intune-licentie hebt gegeven op de website van ht Microsoft 365-beheercentrum nadat u bent aangemeld met een beheerdersaccount. Zie [Microsoft Intune-licentie toewijzen](../fundamentals/licenses-assign.md).

* **Beveiligingsbeleid voor apps in Intune**: als u uw app wilt testen aan de hand van al het beveiligingsbeleid voor apps in Intune, moet u voor elke beleidsinstelling het te verwachten gedrag kennen. Zie de beschrijvingen van [iOS-beleid voor app-beveiliging](../apps/app-protection-policy-settings-ios.md) en [Android-beleid voor app-beveiliging](../apps/app-protection-policy-settings-android.md). Als uw app met de Intune SDK is geïntegreerd, maar niet wordt weergegeven in de lijst met apps waarop beleid kan worden gericht, kunt u de bundel-id van de app (iOS) of de pakketnaam (Android) opgeven in het tekstvak wanneer u Aangepaste apps selecteert. 

* **Probleemoplossing**: als u problemen ondervindt tijdens het handmatig testen van de gebruikerservaring van uw app-installatie, gaat u naar [Problemen met app-installatie oplossen](../apps/troubleshoot-app-install.md). 

### <a name="give-your-app-access-to-the-intune-app-protection-service-optional"></a>Uw app toegang geven tot de Intune-app-beveiliging (optioneel)

Als uw app zijn eigen aangepaste Azure Active Directory-instellingen (AAD) voor verificatie gebruikt, moet u de volgende stappen volgen voor zowel apps uit de openbare store als interne LOB-apps. De stappen **hoeven niet te worden genomen als uw app momenteel gebruikmaakt van de standaard client-id van de Intune-SDK**. 

Nadat u uw app hebt geregistreerd in een Azure-tenant en deze wordt weergegeven onder **Alle toepassingen**, moet u uw app toegang geven tot de Intune-app-beveiliging (eerder bekend als MAM-service). In Azure Portal:

1. Ga naar de blade **Azure Active Directory**.
2. Ga onder **App-registraties** naar de vermelding die voor de toepassing is ingesteld.
3. Klik op **+ Een machtiging toevoegen**.
4. Klik op **API's die in mijn organisatie worden gebruikt**. 
5. Voer in het zoekvak **Microsoft Mobile Application Management** in.
6. Schakel onder **Gedelegeerde machtigingen** het selectievakje **DeviceManagementManagedApps.ReadWrite: de app-beheergegevens van de gebruiker lezen en schrijven*** in.
7. Klik op **Machtigingen toevoegen**.

> [!NOTE]
> Als uw app uw aanmelding beperkt vanwege een fout bij het openen van de resource https\://intunemam.microsoftonline.com, moet u een bericht verzenden naar msintuneappsdk@microsoft.com met de client-id van uw app. Dit is momenteel een handmatig goedkeuringsproces.

### <a name="badge-your-app-optional"></a>Uw app van een logo voorzien (optioneel)

Nadat u de werking van Intune-beleid voor app-beveiliging hebt gevalideerd in uw app, kunt u het pictogram van uw app voorzien van het logo van Intune-beleid voor app-beveiliging.

Aan de hand van dit logo kunnen IT-beheerders, eindgebruikers en potentiële Intune-klanten zien dat uw app werkt met Intune-beleid voor app-beveiliging. Hiermee wordt de aanvaarding en het gebruik van uw app door Intune-klanten aangemoedigd.

Het logo ziet eruit als het pictogram van een aktetas zoals in de voorbeelden hieronder wordt weergegeven:

![Beveiligingsbeleid voor apps in Intune - logovoorbeeld 1](./media/app-sdk-get-started/badge-example-1.png) ![Beveiligingsbeleid voor apps in Intune - logovoorbeeld 2](./media/app-sdk-get-started/badge-example-2.png)

**Wat u nodig hebt om uw app van een logo te voorzien**:

* Een toepassing voor het bewerken van afbeeldingen die **EPS**-bestanden kan lezen of een Adobe-toepassing die **AI**-bestanden kan lezen.

* U kunt de [hulpmiddelen en richtlijnen voor het app-logo van Intune](https://github.com/msintuneappsdk/intune-app-partner-badge) vinden op de Microsoft Intune GitHub.