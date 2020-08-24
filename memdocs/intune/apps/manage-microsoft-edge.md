---
title: Microsoft Edge voor iOS en Android beheren met Intune
titleSuffix: ''
description: Hanteer het Intune-beveiligings - en configuratiebeleid voor apps met Microsoft Edge voor iOS en Android zodat bedrijfswebsites altijd onder veilige omstandigheden toegankelijk zijn.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/05/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb
ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2eb5a5e87b54fd8a92fc40c6d1295250d90b05c4
ms.sourcegitcommit: f6b14e6fe694a2a05c6ed92e67089e80a00a0908
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/17/2020
ms.locfileid: "88501181"
---
# <a name="manage-web-access-by-using-edge-for-ios-and-android-with-microsoft-intune"></a>Internettoegang beheren met behulp van Microsoft Edge voor iOS en Android met Microsoft Intune

Microsoft Edge voor iOS en Android is ontworpen om gebruikers in staat te stellen op internet te surfen en ondersteunt meerdere identiteiten. Gebruikers kunnen een werkaccount en een persoonlijk account maken om mee te browsen. Er is een volledige scheiding tussen de twee identiteiten, vergelijkbaar met wat wordt aangeboden in andere mobiele apps van Microsoft.

Microsoft Edge voor iOS wordt ondersteund op iOS 12.0 en hoger. Microsoft Edge voor Android wordt ondersteund op Android 5 en hoger.

> [!NOTE]
> Microsoft Edge voor iOS en Android maakt geen gebruik van de instellingen die gebruikers configureren voor de systeemeigen browser op hun apparaten, omdat Microsoft Edge voor iOS en Android geen toegang heeft tot deze instellingen.

De meest veelzijdige en breedste beveiligingsmogelijkheden voor Office 365-gegevens zijn beschikbaar wanneer u zich abonneert op de Enterprise Mobility + Security Suite, die functies bevat van Microsoft Intune en Azure Active Directory Premium, zoals voorwaardelijke toegang. U moet minimaal een beleid voor voorwaardelijke toegang implementeren dat alleen connectiviteit toestaat voor Microsoft Edge voor iOS en Android vanaf mobiele apparaten en een Intune-beleid voor app-beveiliging dat ervoor zorgt dat de surfervaring wordt beschermd.

> [!NOTE]
> Nieuwe webclips (vastgemaakte webtoepassingen) op iOS-apparaten worden geopend in Microsoft Edge voor iOS en Android in plaats van in de Intune Managed Browser wanneer ze in een beveiligde browser moeten worden geopend. Voor oudere iOS-webclips moet u een nieuw doel opgeven om ervoor te zorgen dat ze worden geopend in Microsoft Edge voor iOS en Android in plaats van in de Managed Browser.

## <a name="apply-conditional-access"></a>Voorwaardelijke toegang toepassen
Organisaties kunnen gebruikmaken van het beleid voor voorwaardelijke toegang van Azure AD om ervoor te zorgen dat gebruikers alleen toegang hebben tot werk- of schoolinhoud met behulp van Microsoft Edge voor iOS en Android. Hiervoor hebt u een beleid voor voorwaardelijke toegang nodig dat zich richt op alle potentiële gebruikers. Meer informatie over het maken van dit beleid vindt u in [Beveiligingsbeleid voor apps vereisen voor toegang tot cloud-apps met voorwaardelijke toegang](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Volg [Scenario 2: Voor browser-apps zijn goedgekeurde apps met app-beveiligingsbeleid vereist](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-2-browser-apps-require-approved-apps-with-app-protection-policies), waarmee Microsoft Edge voor iOS en Android is toegestaan, maar andere webbrowsers voor mobiele apparaten worden geblokkeerd en geen verbinding kunnen maken met Office 365-eindpunten.

   >[!NOTE]
   > Dit beleid zorgt ervoor dat mobiele gebruikers toegang hebben tot alle Office 365-eindpunten vanuit Microsoft Edge voor iOS en Android. Dit beleid voorkomt ook dat gebruikers InPrivate gebruiken om toegang te krijgen tot Office 365-eindpunten.

Met voorwaardelijke toegang kunt u zich ook richten op on-premises sites die u zichtbaar hebt gemaakt voor externe gebruikers via de [Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="create-intune-app-protection-policies"></a>Beveiligingsbeleid voor apps in Intune maken

App-beveiligingsbeleid (APP) bepaalt welke apps zijn toegestaan en welke acties deze kunnen uitvoeren met de gegevens van uw organisatie. Dankzij de opties die beschikbaar zijn in APP kunnen organisaties de beveiliging aanpassen aan hun specifieke behoeften. Het is mogelijk niet voor iedereen duidelijk welke beleidsinstellingen vereist zijn om een volledig scenario te implementeren. Microsoft heeft een taxonomie geïntroduceerd voor het APP-gegevensbeschermingsframework voor het beheer van mobiele iOS- en Android-apps om organisaties te helpen bij het bepalen van de prioriteit van de beveiliging van mobiele clienteindpunten.

Het APP-gegevensbeschermingsframework is onderverdeeld in drie afzonderlijke configuratieniveaus, waarbij elk niveau is gebaseerd op het vorige niveau:

- Met **Basisgegevensbescherming voor ondernemingen** (niveau 1) worden apps beveiligd met een pincode en versleuteld, en worden selectieve wisbewerkingen uitgevoerd. Voor Android-apparaten wordt met dit niveau Android-apparaatbevestiging gevalideerd. Dit is een configuratie op instapniveau die vergelijkbare gegevensbescherming biedt in het Exchange Online-postvakbeleid en die IT en de gebruikerspopulatie laat kennismaken met APP.
- Met **Geavanceerde gegevensbescherming voor ondernemingen** (niveau 2) worden mechanismen voor preventie van gegevenslekkage en minimale vereisten voor het besturingssysteem geïntroduceerd. Dit is de configuratie die van toepassing is op de meeste mobiele gebruikers die toegang hebben tot werk- of schoolgegevens.
- Met **Hoge gegevensbeveiliging voor ondernemingen** (niveau 3) worden geavanceerde mechanismen voor gegevensbeveiliging, verbeterde configuratie van de pincode en APP Mobile Threat Defense geïntroduceerd. Deze configuratie is wenselijk voor gebruikers die toegang hebben tot gegevens met een hoog risico.

Als u de specifieke aanbevelingen voor elk configuratieniveau en de apps die minimaal moeten worden beveiligd, wilt bekijken, bestudeert u [Gegevensbeschermingsframework met behulp van beveiligingsbeleid voor apps](app-protection-framework.md).

Of het apparaat nu wel of niet is ingeschreven in een UEM-oplossing (Unified endpoint Management), er moet een Intune-app-beveiligingsbeleid worden gemaakt voor zowel iOS- als Android-apps, met behulp van de stappen in [App-beveiligingsbeleid maken en toewijzen](app-protection-policies.md). Deze beleidsregels moeten minimaal voldoen aan de volgende voorwaarden:

1. Ze omvatten alle mobiele Microsoft 365-toepassingen, zoals Microsoft Edge, Outlook, OneDrive, Office of Teams, omdat dit ervoor zorgt dat gebruikers op een veilige manier toegang hebben tot werk- of schoolgegevens binnen elke Microsoft-app.

2. Ze worden toegewezen aan alle gebruikers. Dit zorgt ervoor dat alle gebruikers worden beveiligd, ongeacht of ze Microsoft Edge voor iOS of Android gebruiken.

3. Bepaal welk frameworkniveau voldoet aan uw vereisten. De meeste organisaties moeten de instellingen implementeren die zijn gedefinieerd in **Geavanceerde gegevensbescherming voor ondernemingen** (niveau 2), omdat hiermee besturingselementen voor gegevensbescherming en toegangsvereisten worden ingeschakeld.

Zie [Beveiligingsbeleidsinstellingen voor Android-apps](app-protection-policy-settings-android.md) en [Beveiligingsbeleidsinstellingen voor iOS-apps](app-protection-policy-settings-ios.md) voor meer informatie over de beschikbare instellingen.

> [!IMPORTANT]
> Als u Intune-app-beveiligingsbeleid wilt toepassen op apps op Android-apparaten die niet zijn ingeschreven bij Intune, moet de gebruiker ook de Intune-bedrijfsportal installeren. Raadpleeg [Wat u kunt verwachten wanneer uw Android-app wordt beheerd door een app-beveiligingsbeleid](../fundamentals/end-user-mam-apps-android.md) voor meer informatie.

## <a name="single-sign-on-to-azure-ad-connected-web-apps-in-policy-protected-browsers"></a>Eenmalige aanmelding voor met Azure AD verbonden web-apps in met beleid beveiligde browsers

In Microsoft Edge voor iOS en Android kan eenmalige aanmelding (SSO) worden gebruikt voor alle web-apps (SaaS en on-premises) die met Azure AD zijn verbonden. Met eenmalige aanmelding kunnen gebruikers toegang krijgen tot met Azure AD verbonden web-apps via Microsoft Edge voor iOS en Android, zonder dat ze hun referenties opnieuw hoeven op te geven.

Voor eenmalige aanmelding moet uw apparaat zijn geregistreerd door de Microsoft Authenticator-app voor iOS-apparaten of de Intune-bedrijfsportal voor Android. Als gebruikers over een van beide beschikken, wordt hen gevraagd hun apparaat te registreren wanneer ze naar een met Azure AD verbonden web-app in een met beleid beschermde browser gaan (dit geldt alleen als hun apparaat nog niet is geregistreerd). Nadat het apparaat is geregistreerd met het gebruikersaccount dat wordt beheerd door Intune, is voor dat account eenmalige aanmelding ingeschakeld voor web-apps die met Azure AD zijn verbonden.

> [!NOTE]
> Apparaatregistratie is eenvoudig inchecken met de Azure AD-service. Dit vereist geen volledige apparaatinschrijving en geeft IT geen extra bevoegdheden op het apparaat.

## <a name="utilize-app-configuration-to-manage-the-browsing-experience"></a>App-configuratie gebruiken om de surfervaring te beheren

Microsoft Edge voor iOS en Android ondersteunt app-instellingen waarmee Unified Endpoint Management-beheerders, zoals Microsoft Endpoint Manager, het gedrag van de app kunnen aanpassen.

App-configuratie kan worden geleverd via het OS-kanaal van Mobile Device Management (MDM) op geregistreerde apparaten (kanaal [Beheerde app-configuratie](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) voor iOS of kanaal [Android in de Enterprise](https://developer.android.com/work/managed-configurations) voor Android) of via het kanaal Intune-app-beveiligingsbeleid (APP). Microsoft Edge voor iOS en Android ondersteunt de volgende configuratiescenario's:

- Alleen werk- of schoolaccounts toestaan
- Algemene configuratie-instellingen voor apps
- Instellingen voor gegevensbeveiliging

> [!IMPORTANT]
> Voor configuratiescenario's waarvoor apparaatregistratie op Android is vereist, moeten de apparaten worden ingeschreven bij Android Enterprise en moet Microsoft Edge voor Android worden geïmplementeerd via de Beheerde Google Play Store. Zie [Inschrijving van apparaten met Android Enterprise-werkprofielen instellen](../enrollment/android-work-profile-enroll.md) en [App-configuratiebeleid toevoegen voor beheerde Android Enterprise-apparaten](app-configuration-policies-use-android.md) voor meer informatie.

Elk configuratiescenario heeft zijn eigen specifieke vereisten. Bijvoorbeeld of voor het configuratiescenario apparaatregistratie vereist is en of dit hierdoor werkt met elke UEM-provider of dat Intune-app-beveiligingsbeleid vereist is.

> [!NOTE]
> Met Microsoft Endpoint Manager wordt de app-configuratie die via het MDM-OS-kanaal wordt geleverd, aangeduid als het app-configuratiebeleid (App Configuration Policy; ACP) **Beheerde apparaten**; app-configuratie die via het kanaal App-beveiligingsbeleid wordt geleverd, wordt het app-configuratiebeleid **Beheerde apps** genoemd.

## <a name="only-allow-work-or-school-accounts"></a>Alleen werk- of schoolaccounts toestaan

Het respecteren van het beleid voor gegevensbeveiliging en naleving van onze grootste en uiterst gereguleerde klanten is een belangrijke pijler van Microsoft 365. Sommige bedrijven zijn verplicht om alle communicatie-informatie in hun bedrijfsomgeving vast te leggen, en om ervoor te zorgen dat de apparaten alleen voor bedrijfscommunicatie worden gebruikt. Ter ondersteuning van deze vereisten kan Microsoft Edge voor iOS en Android op geregistreerde apparaten zo worden geconfigureerd dat maar één bedrijfsaccount kan worden ingericht binnen de app.

Meer informatie over het configureren van de instelling voor door de organisatie toegestane accounts vindt u hier:

- [Android-instelling](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS-instelling](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Dit configuratiescenario werkt alleen met geregistreerde apparaten. Een UEM-provider wordt echter wel ondersteund. Als u geen gebruik maakt van Microsoft Endpoint Manager, moet u de UEM-documentatie raadplegen voor informatie over hoe u deze configuratiesleutels implementeert.

## <a name="general-app-configuration-scenarios"></a>Algemene configuratiescenario's voor apps

Microsoft Edge voor iOS en Android biedt beheerders de mogelijkheid om de standaardconfiguratie voor verschillende in-app-instellingen aan te passen. Deze mogelijkheid is momenteel alleen beschikbaar wanneer voor Microsoft Edge voor iOS en Android een Intune-app-beveiligingsbeleid is toegepast op het werk- of schoolaccount dat is aangemeld bij de app en de beleidsinstellingen worden geleverd door een App Configuration-beleid via beheerde apps.

> [!IMPORTANT]
> Microsoft Edge voor Android biedt geen ondersteuning voor Chromium-instellingen die beschikbaar zijn in Beheerde Google Play.

Microsoft Edge ondersteunt de volgende instellingen voor configuratie:

- Nieuwe tabbladpagina-ervaringen
- Bladwijzerervaringen
- Ervaringen met app-gedrag
- Kioskmodus-ervaringen

Deze instellingen kunnen worden geïmplementeerd in de app, ongeacht de inschrijvingsstatus van het apparaat.

### <a name="new-tab-page-experiences"></a>Nieuwe tabbladpagina-ervaringen

Microsoft Edge voor iOS en Android biedt organisaties verschillende opties om de ervaring Nieuwe tabbladpagina aan te passen.

#### <a name="organization-logo-and-brand-color"></a>Bedrijfslogo en merkkleur

Met deze instellingen kunt u de Nieuwe tabbladpagina voor Microsoft Edge voor iOS en Android aanpassen om het logo en de kleur van uw organisatie weer te geven als achtergrond van de pagina.

Als u het logo en de kleur van uw organisatie wilt uploaden, moet u eerst de volgende stappen uitvoeren:
1. Ga in [Microsoft Endpoint Manager](https://endpoint.microsoft.com) naar **Tenantbeheer** -> **Aanpassing** -> **Bedrijfshuisstijl**.
2. Als u uw merklogo wilt instellen, kiest u naast **Weergeven in koptekst** 'Alleen logo van organisatie'. Transparante achtergrondlogo's worden aanbevolen.
3. Als u de achtergrondkleur van uw merk wilt instellen, selecteert u een **Themakleur**. Microsoft Edge voor iOS en Android past een lichtere tint van de kleur toe op de Nieuwe tabbladpagina. Dit zorgt ervoor dat de pagina goed leesbaar is.

Gebruik vervolgens de volgende sleutel-/waardeparen om het merk van uw organisatie in Microsoft Edge voor iOS en Android weer te geven:

|    Sleutel    |    Waarde    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    **waar** toont het merklogo van de organisatie<br>**onwaar** (standaard) geeft geen logo weer    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    **waar** geeft de merkkleur van de organisatie weer<br>**onwaar** (standaard) geeft geen kleur weer    |

#### <a name="homepage-shortcut"></a>Snelkoppeling voor startpagina

Met deze instelling kunt u een snelkoppeling naar de startpagina voor Microsoft Edge voor iOS en Android configureren. De snelkoppeling naar de startpagina die u configureert, verschijnt als eerste pictogram onder de zoekbalk, wanneer de gebruiker een nieuw tabblad in Microsoft Edge voor iOS en Android opent. De gebruiker kan deze snelkoppeling niet bewerken of verwijderen in zijn beheerde context. De snelkoppeling naar de startpagina geeft voor de duidelijkheid de naam van uw organisatie weer. 

|    Sleutel    |    Waarde    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Geef een geldige URL op. Uit veiligheidsoogpunt worden onjuiste URL's geblokkeerd.<br>Bijvoorbeeld: `https://www.bing.com`     |

#### <a name="multiple-top-site-shortcuts"></a>Meerdere snelkoppelingen naar de bovenste site

Net als bij het configureren van een snelkoppeling naar een startpagina, kunt u meerdere snelkoppelingen naar sites op het hoogste niveau configureren op nieuwe tabbladen in Microsoft Edge voor iOS en Android. De gebruiker kan deze snelkoppelingen niet bewerken of verwijderen in een beheerde context. Opmerking: u kunt in totaal acht snelkoppelingen configureren, waaronder een snelkoppeling naar de startpagina. Als u een snelkoppeling naar de startpagina hebt geconfigureerd, vervangt deze de eerste site op het hoogste niveau die is geconfigureerd. 

|    Sleutel    |    Waarde    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    Specificeer een set waarde-URL's. Elke snelkoppeling naar een site op het hoogste niveau bestaat uit een titel en een URL. Scheid de titel en de URL met het teken `|`.<br>Bijvoorbeeld: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### <a name="industry-news"></a>Branchenieuws

U kunt de Nieuwe tabbladpagina in Microsoft Edge voor iOS en Android configureren zodat er nieuws wordt weergegeven van de branche die relevant is voor uw organisatie. Als u deze functie inschakelt, gebruikt Microsoft Edge voor iOS en Android de domeinnaam van uw organisatie voor het samenvoegen van nieuws van het web over uw organisatie, de branche van uw organisatie en de concurrentie, zodat uw gebruikers relevant extern nieuws kunnen vinden vanuit de nieuwe gecentraliseerde tabbladpagina's in Microsoft Edge voor iOS en Android. Branchenieuws is standaard uitgeschakeld. 

|    Sleutel    |    Waarde    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **waar** geeft Branchenieuws weer op de Nieuwe tabbladpagina<br>**onwaar** (standaard) verbergt Branchenieuws op de Nieuwe tabbladpagina    |

### <a name="bookmark-experiences"></a>Bladwijzerervaringen

Microsoft Edge voor iOS en Android biedt organisaties verschillende opties voor het beheren van bladwijzers.

#### <a name="managed-bookmarks"></a>Beheerde bladwijzers

Voor een betere toegankelijkheid kunt u bladwijzers configureren die u beschikbaar wilt stellen voor de gebruikers wanneer ze Microsoft Edge voor iOS en Android gebruiken.

- Bladwijzers worden alleen weergegeven in het werk- of schoolaccount en zijn niet zichtbaar in persoonlijke accounts.
- Bladwijzers kunnen niet door gebruikers worden verwijderd of gewijzigd.
- Bladwijzers worden boven in de lijst weergegeven. Door de gebruiker gemaakte bladwijzers worden onder deze bladwijzers weergegeven.
- Als u omleiding via een toepassingsproxy hebt ingeschakeld, kunt u web-apps met een toepassingsproxy toevoegen met behulp van hun interne of externe URL.
- Zorg ervoor dat u alle URL's voorziet van het voorvoegsel **http://** of **https://** wanneer u ze in de lijst invoert.
- Bladwijzers worden gemaakt in een map met de naam van de organisatie die is gedefinieerd in Azure Active Directory.

|    Sleutel    |    Waarde    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    De waarde voor deze configuratie is een lijst met bladwijzers. Elke bladwijzer bestaat uit de titel en de URL van de bladwijzer. Scheid de titel en de URL met het teken `|`.<br> Bijvoorbeeld: `Microsoft Bing|https://www.bing.com`<p>Als u meerdere bladwijzers wilt configureren, typt u een dubbel scheidingsteken `||` tussen de bladwijzers.<br>Bijvoorbeeld:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### <a name="my-apps-bookmark"></a>Bladwijzer Mijn apps

Standaard is voor gebruikers de bladwijzer Mijn apps geconfigureerd in de organisatiemap binnen Microsoft Edge voor iOS en Android.

|    Sleutel    |    Waarde    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **waar** (standaard) geeft Mijn apps weer binnen de Microsoft Edge voor iOS- en Android-bladwijzers<br>**onwaar** verbergt Mijn apps binnen Microsoft Edge voor iOS en Android    |

### <a name="app-behavior-experiences"></a>Ervaringen met app-gedrag

Microsoft Edge voor iOS en Android biedt organisaties verschillende opties voor het beheren van het gedrag van de app.

#### <a name="default-protocol-handler"></a>Standaardprotocolhandler

Microsoft Edge voor iOS en Android maakt standaard gebruik van de HTTPS-protocolhandler wanneer de gebruiker het protocol niet in de URL opgeeft. Over het algemeen wordt dit zeer aangeraden, maar het kan worden uitgeschakeld.

|    Sleutel    |    Waarde    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     **waar** (standaard) standaardprotocolhandler is HTTPS<br>**onwaar** standaardprotocolhandler is HTTP     |

#### <a name="disable-data-sharing-for-personalization"></a>Gegevens delen voor persoonlijke instellingen uitschakelen

Standaard vraagt Microsoft Edge voor iOS en Android gebruikers om gebruiksgegevens te verzamelen en surfgeschiedenis te delen om zo de surfervaring te personaliseren. Organisaties kunnen het delen van deze gegevens uitschakelen door te voorkomen dat deze melding wordt weergegeven aan eindgebruikers.

|    Sleutel    |    Waarde    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     **waar** schakelt deze melding uit, waardoor deze niet wordt weergegeven aan eindgebruikers<br>**onwaar** (standaard) gebruikers wordt gevraagd gebruiksgegevens te delen    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     **waar** schakelt deze melding uit, waardoor deze niet wordt weergegeven aan eindgebruikers<br>**onwaar** (standaard) gebruikers wordt gevraagd surfgeschiedenis te delen     |

#### <a name="disable-specific-features"></a>Specifieke functies uitschakelen

Met Microsoft Edge voor iOS en Android kunnen organisaties bepaalde functies uitschakelen die standaard zijn ingeschakeld. Als u deze functies wilt uitschakelen, configureert u de volgende instelling:

|    Sleutel    |    Waarde    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    **wachtwoord** schakelt meldingen uit die de eindgebruiker aanbieden om wachtwoorden op te slaan<br>**inprivate** schakelt InPrivate-surfen uit<p>Als u meerdere functies wilt uitschakelen, moet u de waarden scheiden met `|`. Als u bijvoorbeeld zowel InPrivate als wachtwoordopslag wilt uitschakelen, gebruikt u `inprivate|password`.     |

> [!NOTE]
> Microsoft Edge voor Android biedt geen ondersteuning voor het uitschakelen van wachtwoordbeheer.

#### <a name="disable-extensions"></a>Uitbreidingen uitschakelen

U kunt het uitbreidingsframework in Microsoft Edge voor Android uitschakelen om te voorkomen dat gebruikers appuitbreidingen installeren. Daartoe configureert u de volgende instelling:

|    Sleutel    |    Waarde    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    **waar** schakelt het uitbreidingsframe uit<br>**onwaar** (standaard) schakelt het uitbreidingsframework in    |

### <a name="kiosk-mode-experiences-on-android-devices"></a>Kioskmodus-ervaringen op Android-apparaten

Microsoft Edge voor Android kan worden ingeschakeld als een kiosk-app met de volgende instellingen:

|    Sleutel    |    Waarde    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    **waar** schakelt de kioskmodus voor Microsoft Edge voor Android in<br>**onwaar** (standaard) schakelt kioskmodus uit    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    **waar** geeft de adresbalk in kioskmodus weer<br> met **onwaar** (standaard) wordt de adresbalk verborgen wanneer de kioskmodus is ingeschakeld    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    **waar** geeft de onderste actiebalk weer in kioskmodus<br> met **onwaar** (standaard) wordt de onderste balk verborgen wanneer de kioskmodus is ingeschakeld    |

## <a name="data-protection-app-configuration-scenarios"></a>App-configuratiescenario's voor gegevensbescherming

Microsoft Edge voor iOS en Android ondersteunt beleidsregels voor app-configuratie door de instellingen voor gegevensbeveiliging te volgen wanneer de app wordt beheerd door Microsoft Endpoint Manager met een Intune-app-beveiligingsbeleid dat is toegepast op het werk- of schoolaccount dat is aangemeld bij de app en de beleidsinstellingen worden geleverd door een App Configuration-beleid via beheerde apps:

- Accountsynchronisatie beheren
- Beperkte websites beheren
- Proxyconfiguratie beheren
- Sites voor eenmalige aanmelding met NTLM beheren

Deze instellingen kunnen worden geïmplementeerd in de app, ongeacht de inschrijvingsstatus van het apparaat.

### <a name="manage-account-synchronization"></a>Accountsynchronisatie beheren

Microsoft Edge Sync stelt gebruikers standaard in staat om toegang te krijgen tot hun surfgegevens op alle apparaten die zijn aangemeld. De gegevens die worden ondersteund door synchronisatie zijn onder andere:

- Favorieten
- Wachtwoorden
- Adressen en meer (automatisch invullen van formulieren)

De synchronisatiefunctionaliteit wordt ingeschakeld via toestemming van de gebruiker en gebruikers kunnen synchronisatie in- of uitschakelen voor elk van de hierboven vermelde gegevenstypen. Zie [Microsoft Edge Sync](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync) voor meer informatie.

Organisaties hebben de mogelijkheid om Microsoft Edge-synchronisatie uit te schakelen op iOS en Android. 

|Sleutel  |Waarde  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |**waar** (standaard) staat Microsoft Edge-synchronisatie toe<br>**onwaar** schakelt Microsoft Edge-synchronisatie uit          |

### <a name="manage-restricted-web-sites"></a>Beperkte websites beheren

Organisaties kunnen bepalen tot welke sites gebruikers toegang hebben binnen de context van het werk- of schoolaccount in Microsoft Edge voor iOS en Android. Als u een lijst met toegestane sites gebruikt, hebben gebruikers alleen toegang tot de sites die expliciet worden genoemd. Als u een lijst met geblokkeerde sites gebruikt, hebben gebruikers toegang tot alle sites, met uitzondering van de sites die expliciet zijn geblokkeerd. Gebruik alleen een lijst met toegestane sites of een lijst met geblokkeerde sites, niet beide. Als u beide lijsten gebruikt, heeft alleen de lijst met toegestane sites voorrang.

De organisatie bepaalt ook wat er gebeurt wanneer een gebruiker naar een beperkte website probeert te navigeren. Overgangen zijn standaard toegestaan. Als de organisatie dit toestaat, kunnen websites met beperkte toegang worden geopend in de context van het persoonlijke account, de InPrivate-context van het Azure AD-account en of de site volledig is geblokkeerd. Zie [Beperkte website-overgangen in Microsoft Edge Mobile](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333) voor meer informatie over de verschillende scenario's die worden ondersteund. Door overgangservaringen toe te staan, blijven de gebruikers van de organisatie beveiligd, terwijl bedrijfsresources veilig blijven.

> [!NOTE]
> Microsoft Edge voor iOS en Android kan alleen toegang tot sites blokkeren wanneer de sites rechtstreeks worden geopend. De app kan de toegang niet blokkeren wanneer gebruikers tussenliggende services (zoals een vertaalservice) gebruiken voor toegang tot de site.

Gebruik de volgende sleutel-waardeparen om een lijst met toegestane sites of een lijst met geblokkeerde sites te configureren voor Microsoft Edge voor iOS en Android. 

|Sleutel  |Waarde  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |De overeenkomstige waarde voor de sleutel is een lijst met URL's. U geeft alle URL's die u wilt toestaan op als één waarde, gescheiden door een sluisteken `|`.<p>**Voorbeelden:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |De overeenkomstige waarde voor de sleutel is een lijst met URL's. U geeft alle URL's die u wilt blokkeren op als één waarde, gescheiden door een sluisteken `|`.<br>**Voorbeelden:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |**waar** (standaard) staat Microsoft Edge voor iOS en Android toe om beperkte sites over te dragen. Wanneer persoonlijke accounts niet zijn uitgeschakeld, worden gebruikers gevraagd om over te schakelen naar de persoonlijke context om de beperkte site te openen of om een persoonlijk account toe te voegen. Als com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked is ingesteld op waar, hebben gebruikers de mogelijkheid om de beperkte site te openen in de InPrivate-context.<p>**onwaar** voorkomt dat Microsoft Edge voor iOS en Android gebruikers overzetten. Gebruikers krijgen een bericht te zien waarin staat dat de site die ze proberen te openen, is geblokkeerd.         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |**waar** staat toe dat beperkte sites worden geopend in de InPrivate-context van het Azure AD-account. Als het Azure AD-account het enige account is dat is geconfigureerd in Microsoft Edge voor iOS en Android, wordt de beperkte site automatisch geopend in de InPrivate-context. Als de gebruiker een persoonlijk account heeft geconfigureerd, wordt de gebruiker gevraagd om te kiezen tussen het openen van InPrivate of om over te schakelen naar het persoonlijke account.<p> **onwaar** (standaard) vereist dat de beperkte site wordt geopend in het persoonlijke account van de gebruiker. Als persoonlijke accounts zijn uitgeschakeld, wordt de site geblokkeerd.<p>Om deze instelling door te voeren, moet com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock zijn ingesteld op waar.          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | Voer het aantal seconden in dat gebruikers de volgende snackbarmelding zien: 'Koppeling geopend met InPrivate-modus. Uw organisatie vereist het gebruik van InPrivate-modus voor deze inhoud.' Standaard wordt de snackbarmelding gedurende zeven seconden weergegeven.

De volgende sites zijn altijd toegestaan, ongeacht de instellingen voor de lijst met toegestane en geblokkeerde websites:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### <a name="url-formats-for-allowed-and-blocked-site-list"></a>URL-indelingen voor een lijst met toegestane sites en een lijst met geblokkeerde sites 

U kunt verschillende URL-indelingen gebruiken om uw lijsten met toegestane/geblokkeerde sites te maken. De toegestane patronen worden in de volgende tabel beschreven.

- Zorg ervoor dat u alle URL's voorziet van het voorvoegsel **http://** of **https://** wanneer u ze in de lijst invoert.
- U kunt het jokerteken (\*) gebruiken volgens de regels in de volgende lijst met toegestane patronen.
- Een jokerteken kan alleen overeenkomen met een volledig onderdeel van de hostnaam (gescheiden door punten) of met volledige delen van het pad (gescheiden door slashes). `http://*contoso.com` wordt bijvoorbeeld **niet** ondersteund.
- U kunt poortnummers in het adres opgeven. Als u geen poortnummer opgeeft, worden deze waarden gebruikt:
  - Poort 80 voor http
  - Poort 443 voor https
- Het gebruik van jokertekens voor het poortnummer wordt **niet** ondersteund. `http://www.contoso.com:*` en `http://www.contoso.com:*/` bijvoorbeeld worden niet ondersteund. 

    |    URL    |    Details    |    Komt overeen met    |    Komt niet overeen met    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Komt overeen met één pagina    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Komt overeen met één pagina    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*`   |    Komt overeen met alle URL's die beginnen met `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Komt overeen met alle subdomeinen onder `contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Komt overeen met alle subdomeinen die eindigen op `contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    Komt overeen met een afzonderlijke map    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Komt overeen met één pagina, met gebruik van een poortnummer    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Komt overeen met een enkele, beveiligde pagina    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Komt overeen met een enkele map en alle submappen    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- Hier volgen enkele voorbeelden van een aantal invoerwaarden die u niet kunt opgeven:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP-adressen
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### <a name="manage-proxy-configuration"></a>Proxyconfiguratie beheren

U kunt Microsoft Edge voor iOS en Android en de [Azure AD-toepassingsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) samen gebruiken om gebruikers toegang te verlenen tot intranetsites op hun mobiele apparaten. Bijvoorbeeld: 

- Een gebruiker maakt gebruik van de mobiele app van Outlook, die wordt beveiligd door Intune. De gebruiker klikt vervolgens op een koppeling naar een intranetsite in een e-mailbericht en Microsoft Edge voor iOS en Android herkent dat deze intranetsite beschikbaar is gesteld voor de gebruiker via toepassingsproxy. De gebruiker wordt automatisch omgeleid via de toepassingsproxy om zich bij de betreffende meervoudige verificatie en voorwaardelijke toegang te verifiëren voordat de intranetsite wordt bereikt. De gebruiker heeft nu zelfs op mobiele apparaten toegang tot interne sites en de koppeling in Outlook werkt naar behoren.
- Een gebruiker opent Microsoft Edge voor iOS en Android op het iOS- of Android-apparaat. Als Microsoft Edge voor iOS en Android wordt beveiligd met Intune en de toepassingsproxy is ingeschakeld, kan de gebruiker naar een intranetsite navigeren via de gebruikelijke interne URL. Microsoft Edge voor iOS en Android herkent dat deze intranetsite via toepassingsproxy beschikbaar is gesteld aan de gebruiker. De gebruiker wordt automatisch door de toepassingsproxy gestuurd om zich te verifiëren voordat hij de intranetsite bereikt. 

Voordat u begint:

- Stel de interne toepassingen in via de Azure AD-toepassingsproxy.
  - Raadpleeg [deze documentatie](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy) voor het configureren van de toepassingsproxy en het publiceren van toepassingen.
- Er moet een [Intune-app-beveiligingsbeleid](app-protection-policy.md) worden toegewezen aan de Microsoft Edge voor iOS en Android-app.
- Microsoft-apps moeten beschikken over een app-beveiligingsbeleid waarvan de instelling voor gegevensoverdracht **Overdracht van webinhoud met andere apps beperken** is ingesteld op **Microsoft Edge**.

> [!NOTE]
> Het kan tot 24 uur duren voordat bijgewerkte omleidingsgegevens voor de toepassingsproxy worden doorgevoerd in Microsoft Edge voor iOS en Android.

Wijs aan Microsoft Edge voor iOS het volgende sleutel-waardepaar toe om de toepassingsproxy in te schakelen:

|    Sleutel    |    Waarde    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **waar** schakelt Azure AD App Proxy-omleidingsscenario's in<br>**onwaar** (standaard) verhindert Azure AD App Proxy-scenario's    |

> [!NOTE]
> Microsoft Edge voor Android gebruikt deze sleutel niet. In plaats daarvan gebruikt Microsoft Edge voor Android automatisch de configuratie van Azure AD Application Proxy, mits een app-beveiligingsbeleid is toegepast op het aangemelde Azure AD-account.

Voor meer informatie over het gecombineerde gebruik van Microsoft Edge voor iOS en Android en de Azure AD Application Proxy voor naadloze (en beveiligde) toegang tot on-premises web-apps raadpleegt u [Better together: Intune and Azure Active Directory team up to improve user access](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). (Beter samen: Intune en Azure Active Directory werken samen om de toegang voor gebruikers te verbeteren.) Deze blogpost verwijst naar de Intune Managed Browser, maar de inhoud is ook van toepassing op Microsoft Edge voor iOS en Android.

### <a name="manage-ntlm-single-sign-on-sites"></a>Sites voor eenmalige aanmelding met NTLM beheren

Organisaties kunnen vereisen dat gebruikers zich verifiëren met NTLM om toegang te krijgen tot intranetwebsites. Gebruikers worden standaard elke keer wanneer ze een website openen waarvoor NTLM-verificatie is vereist, gevraagd om referenties in te voeren, omdat NTLM-referenties in de cache zijn uitgeschakeld. 

Organisaties kunnen NTLM-referenties in de cache inschakelen voor bepaalde websites. Nadat de gebruiker referenties heeft ingevoerd en zich heeft geverifieerd, worden de referenties voor deze sites standaard 30 dagen in de cache opgeslagen.


|Sleutel  |Waarde  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |De overeenkomstige waarde voor de sleutel is een lijst met URL's. U geeft alle URL's die u wilt toestaan op als één waarde, gescheiden door een sluisteken `|`.<p>**Voorbeelden:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>Zie [URL-indelingen voor een lijst met toegestane sites en een lijst met geblokkeerde sites](#url-formats-for-allowed-and-blocked-site-list) voor meer informatie over de ondersteunde typen URL-indelingen.         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |Aantal uur dat referenties in de cache moeten worden opgeslagen; de standaardwaarde is 720 uur         |

## <a name="deploy-app-configuration-scenarios-with-microsoft-endpoint-manager"></a>Configuratiescenario's voor apps implementeren met Microsoft Endpoint Manager

Als u Microsoft Endpoint Manager gebruikt als uw provider voor het beheer van mobiele apps, kunt u aan de hand van de volgende stappen een app-configuratiebeleid voor beheerde apps maken. Nadat de configuratie is gemaakt, kunt u de instellingen ervan toewijzen aan groepen gebruikers.

1. Meld u aan bij [Microsoft Endpoint Manager](https://endpoint.microsoft.com).

2. Selecteer **Apps** en selecteer vervolgens **App-configuratiebeleid**.

3. Kies **Toevoegen** op de blade **App-configuratiebeleid** en selecteer **Beheerde apps**.

4. Geef in de sectie **Basisinformatie** een **naam** en een optionele **beschrijving** op voor de app-configuratie-instellingen.

5. Kies voor **Openbare apps** de optie **Openbare apps selecteren** en klik vervolgens op de blade **Beoogde apps** op **Microsoft Edge voor iOS en Android** door de apps voor zowel het iOS- als het Android-platform te selecteren. Klik op **Selecteren** om de geselecteerde openbare apps op te slaan.

6. Klik op **Volgende** om de basisinstellingen van het app-configuratiebeleid te voltooien.

7. Vouw in het gedeelte **Instellingen** de **Configuratie-instellingen voor Microsoft Edge** uit.

8. Als u de instellingen voor gegevensbeveiliging wilt beheren, configureert u de gewenste instellingen dienovereenkomstig:

    - Kies een van de beschikbare opties voor **Toepassingsproxy omleiden**: **Inschakelen**, **Uitschakelen** (standaard).

    - Geef voor **Snelkoppelings-URL voor startpagina** een geldige URL op die het voorvoegsel *http://* of het voorvoegsel *https://* bevat. Uit veiligheidsoogpunt worden onjuiste URL's geblokkeerd.

    - Geef voor **Beheerde bladwijzers** de titel en een geldige URL op die het voorvoegsel *http://* of het voorvoegsel *https://* bevat.

    - Geef voor **Toegestane URL's** een geldige URL op (alleen deze URL's zijn toegestaan; andere sites zijn niet toegankelijk). Zie [URL-indelingen voor een lijst met toegestane sites en een lijst met geblokkeerde sites](#url-formats-for-allowed-and-blocked-site-list) voor meer informatie over de ondersteunde typen URL-indelingen.

    - Geef voor **Geblokkeerde URL's** een geldige URL op (alleen deze URL's worden geblokkeerd). Zie [URL-indelingen voor een lijst met toegestane sites en een lijst met geblokkeerde sites](#url-formats-for-allowed-and-blocked-site-list) voor meer informatie over de ondersteunde typen URL-indelingen.

    - Kies een van de beschikbare opties voor **Beperkte sites omleiden naar een persoonlijke context**: **Inschakelen** (standaard), **Uitschakelen**.

    > [!NOTE]
    > Wanneer zowel Toegestane URL's als Geblokkeerde URL's in het beleid worden gedefinieerd, wordt alleen de lijst met toegestane URL's gehonoreerd.

9. Als u wilt dat aanvullende app-configuratie-instellingen niet worden weergegeven in het bovenstaande beleid, vouwt u het knooppunt **Algemene configuratie-instellingen** uit en voert u de sleutelwaardeparen dienovereenkomstig in.

10. Wanneer u klaar bent met het configureren van de instellingen, kiest u **Volgende**.

11. Kies in de sectie **Toewijzingen** **Groepen selecteren die moeten worden opgenomen**. Selecteer de Azure AD-groep waaraan u de app-configuratie wilt toewijzen en kies vervolgens **Selecteren**.

12. Wanneer u klaar bent met de toewijzingen, kiest u **volgende**.

13. Controleer op de blade **App-configuratiebeleid maken, Controleren en maken** de geconfigureerde instellingen en kies **Maken**.

Het nieuwe configuratiebeleid wordt weergegeven op de blade **App-configuratiebeleid**.

## <a name="use-edge-for-ios-and-android-to-access-managed-app-logs"></a>Microsoft Edge voor iOS en Android gebruiken voor toegang tot logboeken voor beheerde apps

Gebruikers die Microsoft Edge voor iOS en Android op hun iOS- of Android-apparaat hebben geïnstalleerd, kunnen de beheerstatus van alle gepubliceerde Microsoft-apps bekijken. Ze kunnen logboeken verzenden voor het oplossen van problemen met hun beheerde iOS- of Android-apps door de volgende stappen uit te voeren:

1. Open Microsoft Edge voor iOS en Android op het apparaat.
2. Type `about:intunehelp` in het adresvak.
3. Microsoft Edge voor iOS en Android start de probleemoplossingsmodus.

Zie [Logboeken voor beveiliging van client-apps controleren](app-protection-policy-settings-log.md) voor een lijst met instellingen die worden opgeslagen in app-logboeken.

Lees [Send logs to your IT admin by email](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) (Logboeken naar uw IT-beheerder verzenden via e-mail) om te zien hoe u logboeken op Android-apparaten kunt bekijken.

## <a name="next-steps"></a>Volgende stappen

- [Wat zijn beleidsregels voor de beveiliging van apps?](app-protection-policy.md) 
- [App-configuratiebeleid voor Microsoft Intune](app-configuration-policies-overview.md)
