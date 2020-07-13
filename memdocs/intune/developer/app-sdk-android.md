---
title: Ontwikkelaarshandleiding voor Microsoft Intune App SDK voor Android
description: Met de Microsoft Intune App SDK voor Android kunt u Intune Mobile App Management (MAM) opnemen in uw Android-app.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 0100e1b5-5edd-4541-95f1-aec301fb96af
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: a222a1f4adfd2f73731c40946169338989162e5e
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022361"
---
# <a name="microsoft-intune-app-sdk-for-android-developer-guide"></a>Ontwikkelaarshandleiding voor Microsoft Intune App SDK voor Android

> [!NOTE]
> U kunt desgewenst eerst [Overzicht van de Intune App SDK](app-sdk.md) lezen voor meer informatie over de huidige functies en hoe u de integratie voor elk ondersteund platform voorbereidt.
>
> Raadpleeg [SDK-bestanden downloaden](../developer/app-sdk-get-started.md#download-the-sdk-files) om de SDK te downloaden.

Met de Microsoft-SDK voor de Intune-app voor Android kunt u Intune-beveiligingsbeleid voor apps (ook wel **APP-** of MAM-beleid genoemd) opnemen in uw systeemeigen Android-app. Een toepassing die door Intune wordt beheerd, is een toepassing die is geïntegreerd in de SDK voor de Intune-app. Intune-beheerders kunnen eenvoudig app-beveiligingsbeleid implementeren in uw door Intune beheerde app wanneer de app actief door Intune wordt beheerd.


## <a name="whats-in-the-sdk"></a>Inhoud van de SDK

De SDK voor de Intune-app bevat de volgende bestanden:

* **Microsoft.Intune.MAM.SDK.aar**: De SDK-onderdelen, met uitzondering van de JAR-bestanden voor de ondersteuningsbibliotheek.
* **Microsoft.Intune.MAM.SDK.Suppof eent.v4.jar**: De klassen die nodig zijn om MAM in te schakelen in apps die gebruikmaken van de Android v4-ondersteuningsbibliotheek.
* **Microsoft.Intune.MAM.SDK.Suppof eent.v7.jar**: De klassen die nodig zijn om MAM in te schakelen in apps die gebruikmaken van de Android v7-ondersteuningsbibliotheek.
* **Microsoft.Intune.MAM.SDK.Support.v17.jar**: De klassen die nodig zijn om MAM in te schakelen in apps die gebruikmaken van de Android v17-ondersteuningsbibliotheek. 
* **Microsoft.Intune.MAM.SDK.Support.Text.jar**: De klassen die nodig zijn om MAM in te schakelen in apps die gebruikmaken van klassen in de Android-ondersteuningsbibliotheek in het `android.support.text`-pakket.
* **Microsoft.Intune.MAM.SDK.DownlevelStubs.aar**: Deze AAR bevat stubs voor Android-systeemklassen die alleen aanwezig zijn op nieuwere apparaten, maar waarnaar wordt verwezen door methoden in `MAMActivity`. Deze stub-klassen worden door nieuwere apparaten genegeerd. Deze AAR is alleen nodig als uw app reflectie uitvoert op klassen die zijn afgeleid van `MAMActivity`. Deze meeste apps hebben deze jar niet nodig. De AAR bevat ProGuard-regels om alle klassen uit te sluiten.
* **com.microsoft.intune.mam.build.jar**: Een Gradle-invoegtoepassing die [helpt bij integratie van de SDK](#build-tooling).
* **CHANGELOG.md**: Bevat een overzicht van wijzigingen in elke SDK-versie.
* **THIRDPARTYNOTICES.TXT**:  Een bijdragekennisgeving waarin code van derden of OSS-code die in uw app wordt gecompileerd aan de rechthebbenden wordt toegeschreven.


## <a name="requirements"></a>Vereisten

### <a name="android-versions"></a>Android-versies
De SDK biedt ondersteuning voor Android API 21 (Android 5.0) tot en met Android API 29 (Android 10.0). Het kan zijn geïntegreerd in een app met een Android-minSDKVersion van slechts 14, maar op die oudere versies van het besturingssysteem is het niet mogelijk om de Intune-bedrijfsportal-app te installeren of MAM-beleid te gebruiken.

### <a name="company-portal-app"></a>Bedrijfsportal-app
De SDK voor de Intune-app voor Android is afhankelijk van de aanwezigheid van de [bedrijfsportal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)-app op het apparaat voor het inschakelen van app-beveiligingsbeleid. De bedrijfsportal haalt het app-beveiligingsbeleid op van de Intune-service. Tijdens de initialisatie van de app worden het beleid en de code geladen om het betreffende beleid af te dwingen bij de bedrijfsportal.

> [!NOTE]
> Wanneer de bedrijfsportal-app zich niet op het apparaat bevindt, gedraagt een door Intune beheerde app zich hetzelfde als een normale app die geen ondersteuning biedt voor Intune-beleid voor de beveiliging van apps.

Voor app-beveiliging zonder apparaatregistratie hoeft de gebruiker het apparaat _**niet**_ te registreren via de bedrijfsportal-app.

## <a name="sdk-integration"></a>SDK-integratie

### <a name="sample-app"></a>Voorbeeldapp
Op [GitHub](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App) is een voorbeeld beschikbaar van een goede integratie met de Intune-app-SDK. Voor dit voorbeeld wordt de [Gradle-invoegtoepassing voor builds](#gradle-build-plugin) gebruikt.

### <a name="referencing-intune-app-libraries"></a>Verwijzen naar Intune-app-bibliotheken

De SDK voor de Intune-app is een standaard-Android-bibliotheek zonder externe afhankelijkheden. **Microsoft.Intune.MAM.SDK.aar** bevat zowel de benodigde interfaces om app-beveiligingsbeleid te activeren als de code die nodig is om samen te werken met de Microsoft Intune-bedrijfsportal-app.

**Microsoft.Intune.MAM.SDK.aar** moet worden opgegeven als een Android-bibliotheekverwijzing. Hiervoor opent u uw app-project in Android Studio en gaat u naar **Bestand > Nieuw > Nieuwe module** en selecteert u **.JAR/.AAR-pakket importeren**. Selecteer vervolgens het Android-archiefpakket Microsoft.Intune.MAM.SDK.aar om een module voor de .AAR te maken. Klik met de rechtermuisknop op de module(s) die uw app-code bevat(ten) en ga naar **Module-instellingen** > **het tabblad Afhankelijkheden** >  **+-pictogram** > **Module-afhankelijkheid** > Selecteer de MAM SDK AAR-module die u zojuist hebt gemaakt > **OK**. Dit zorgt ervoor dat uw module voldoet aan de MAM SDK wanneer u uw project maakt.

De **Microsoft.Intune.MAM.SDK.Support.XXX.jar**-bibliotheken bevatten ook Intune-varianten van de bijbehorende `android.support.XXX`-bibliotheken. Ze zijn niet ingebouwd in Microsoft.Intune.MAM.SDK.aar voor het geval de ondersteuningsbibliotheken niet nodig zijn voor een app.

#### <a name="proguard"></a>ProGuard

Als [ProGuard](http://proguard.sourceforge.net/) (of een ander mechanisme voor verkleining/versleuteling) wordt gebruikt als een build-stap, moeten aanvullende configuratieregels uit de SDK worden opgenomen. Wanneer u de .AAR in uw build insluit, worden onze regels automatisch geïntegreerd in de ProGuard-stap en worden de noodzakelijke klassebestanden bewaard.

De [Microsoft Authentication Library (MSAL)](https://docs.microsoft.com/azure/active-directory/develop/msal-overview#languages-and-frameworks) kan eigen ProGuard-beperkingen hebben. Als uw app MSAL integreert, moet u de documentatie van de MSAL volgen voor deze beperkingen.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.

### <a name="policy-enforcement"></a>Afdwingen van beleid
De SDK van de Intune-app is een Android-bibliotheek waarmee beleid van Intune in uw app kan worden ondersteund en afgedwongen. 

De meeste beleidsregels worden semi-automatisch afgedwongen, maar voor sommige beleidsregels is [expliciete deelname van uw app om af te dwingen](#enable-features-that-require-app-participation) vereist.
Of u nu bronintegratie uitvoert of build-hulpprogramma's gebruikt voor integratie, de beleidsregels die expliciete deelname vereisen moeten in de code worden opgenomen.

Voor beleidsregels die automatisch worden afgedwongen, is vereist dat apps overname van verschillende Android-basisklassen vervangen door overname van MAM-equivalenten. Op vergelijkbare wijze is vereist dat aanroepen van bepaalde Android-systeemserviceklassen worden vervangen door aanroepen van MAM-equivalenten. De specifieke vervangingen die nodig zijn, staan [hierna](#class-and-method-replacements) beschreven en kunnen handmatig worden uitgevoerd met bronintegratie of automatisch worden uitgevoerd via build-hulpprogramma's.

### <a name="build-tooling"></a>Build-hulpprogramma's
De SDK biedt in build-hulpprogramma's (een invoegtoepassing voor Gradle-builds en een opdrachtregelprogramma voor niet-Gradle-builds) waarmee de MAM-vervangingen automatisch worden uitgevoerd. Deze hulpprogramma's transformeren de klassebestanden die zijn gegenereerd door Java-compilatie en zijn niet van invloed op de oorspronkelijke broncode.

De hulpprogramma's voeren alleen [directe vervangingen](#class-and-method-replacements) uit. De hulpprogramma's voeren geen complexere SDK-integraties uit, zoals [Opslaan als beleid](#enable-features-that-require-app-participation), [Meerdere identiteiten](#multi-identity-optional), [App-WE-registratie](#app-protection-policy-without-device-enrollment) of [AndroidManifest-wijzigingen](#manifest-replacements). Deze moeten worden voltooid voordat uw app volledig geschikt is voor Intune. Controleer zorgvuldig de rest van deze documentatie op integratiepunten die relevant zijn voor uw app.

> [!NOTE]
> U kunt de hulpprogramma's uitvoeren op een project waarvoor de bronintegratie van de MAM-SDK al geheel of gedeeltelijk is uitgevoerd via handmatige vervangingen. In uw project moet de MAM-SDK nog steeds worden vermeld als een afhankelijkheid.

### <a name="gradle-build-plugin"></a>Gradle-invoegtoepassing voor builds
Als uw app niet wordt gecompileerd met Gradle, gaat u naar [Integreren met het opdrachtregelprogramma](#command-line-build-tool). 

De invoegtoepassing voor de app-SDK wordt gedistribueerd als onderdeel van de SDK als **GradlePlugin/com.microsoft.intune.mam.build.jar**. Om de invoegtoepassing vindbaar te maken voor Gradle, moet deze worden toegevoegd aan het klassepad van het buildscript. De invoegtoepassing is afhankelijk van [Javassist](https://jboss-javassist.github.io/javassist/), dat ook moet worden toegevoegd. Om deze toe te voegen aan het klassepad, voegt u het volgende toe aan uw basis-`build.gradle`

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.javassist:javassist:3.22.0-GA"
        classpath files("$PATH_TO_MAM_SDK/GradlePlugin/com.microsoft.intune.mam.build.jar")
    }
}
```

Vervolgens past u de invoegtoepassing in het bestand `build.gradle` voor uw APK-project toe als

```groovy
apply plugin: 'com.microsoft.intune.mam'
```

Standaard is de invoegtoepassing **alleen** van invloed op `project`-afhankelijkheden.
De testcompilatie wordt niet beïnvloed. Configuratie kan worden opgegeven voor het weergeven van
* Projecten die moeten worden uitgesloten
* [Externe afhankelijkheden die moeten worden ingesloten](#usage-of-includeexternallibraries) 
* Specifieke klassen die moeten worden uitgesloten van verwerking
* Varianten die moeten worden uitgesloten van verwerking. Deze kunnen verwijzen naar de volledige naam van een variant of naar een enkele smaak. Bijvoorbeeld
  * Als u een app met de buildtypen `debug` en `release` met de smaken {`savory`, `sweet`} en {`vanilla`, `chocolate`} hebt, kunt u
  * `savory` opgeven om alle varianten met de smaak 'hartig' uit te sluiten of `savoryVanillaRelease` opgeven om alleen die specifieke variant uit te sluiten.

#### <a name="example-partial-buildgradle"></a>Voorbeeld van gedeeltelijke build.gradle

```groovy

apply plugin: 'com.microsoft.intune.mam'

dependencies {
    implementation project(':product:FooLib')
    implementation project(':product:foo-project')
    implementation fileTree(dir: "libs", include: ["bar.jar"])
    implementation fileTree(dir: "libs", include: ["zap.jar"])
    implementation "com.contoso.foo:zap-artifact:1.0.0"
    implementation "com.microsoft.bar:baz:1.0.0"
    implementation "com.microsoft.qux:foo:2.0"

    // Include the MAM SDK
    implementation files("$PATH_TO_MAM_SDK/Microsoft.Intune.MAM.SDK.aar")
}
intunemam {
    excludeProjects = [':product:FooLib']
    includeExternalLibraries = ['bar.jar', "com.contoso.foo:zap-artifact", "com.microsoft.*", "!com.microsoft.qux*"]
    excludeClasses = ['com.contoso.SplashActivity']
    excludeVariants=['savory']
}
```

Hierdoor gebeurt het volgende:
* `:product:FooLib` wordt niet opnieuw geschreven omdat het is opgenomen in `excludeProjects`
* `:product:foo-project` wordt opnieuw geschreven, met uitzondering van `com.contoso.SplashActivity` dat wordt overgeslagen omdat het is opgenomen in `excludeClasses`
* `bar.jar` wordt opnieuw geschreven omdat het is opgenomen in `includeExternalLibraries`
* `zap.jar` wordt **niet** opnieuw geschreven omdat het geen project is en niet is opgenomen in `includeExternalLibraries`
* `com.contoso.foo:zap-artifact:1.0.0` wordt opnieuw geschreven omdat het is opgenomen in `includeExternalLibraries`
* `com.microsoft.bar:baz:1.0.0` wordt opnieuw geschreven omdat het is opgenomen in `includeExternalLibraries` via een jokerteken (`com.microsoft.*`).
* `com.microsoft.qux:foo:2.0` wordt niet herschreven, hoewel deze overeenkomt met hetzelfde jokerteken als het vorige item omdat deze expliciet is uitgesloten via een onderhandelingspatroon.

#### <a name="usage-of-includeexternallibraries"></a>Gebruik van includeExternalLibraries

Omdat de invoegtoepassing alleen van invloed is op projectafhankelijkheden (gewoonlijk geleverd door de functie `project()`) standaard, moeten eventuele afhankelijkheden die zijn opgegeven door `fileTree(...)` of die zijn verkregen van maven of andere pakketbronnen (bijvoorbeeld `com.contoso.bar:baz:1.2.0`), worden opgegeven in de eigenschap `includeExternalLibraries` als daarvoor MAM-verwerking vereist is op basis van de criteria die hieronder wordt uitgelegd. Jokertekens (*) worden ondersteund. Een item dat met `!` begint, is een onderhandeling en kan worden gebruikt om bibliotheken uit te sluiten die anders met een jokerteken wel zouden worden opgenomen.

Wanneer u externe afhankelijkheden met de artefactnotatie opgeeft, wordt aanbevolen het versieonderdeel in de waarde van `includeExternalLibraries` weg te laten. Als u wel een versie opgeeft, moet dit exact de juiste versie zijn. Dynamische versiespecificaties (zoals `1.+`) worden niet ondersteund.

U kunt bepalen of u bibliotheken in `includeExternalLibraries` moet opnemen op basis van de volgende twee vragen:
1. Bevat de bibliotheek klassen waarvoor MAM-equivalenten beschikbaar zijn? Voorbeelden: `Activity`, `Fragment`, `ContentProvider`, `Service`, enzovoort.
2. Zo ja, maakt uw app gebruik van deze klassen?

Als het antwoord op beide vragen 'Ja' is, moet u die bibliotheek opnemen in `includeExternalLibraries`. 

| Scenario | Opnemen? |
|--|--|
| U neemt een PDF-viewer-bibliotheek op in uw app en u gebruikt de viewer `Activity` in uw toepassing wanneer gebruikers PDF-bestanden willen weergeven | Ja |
| U neemt een HTTP-bibliotheek in uw app op voor betere webprestaties | Nee |
| U neemt een bibliotheek zoals React Native op met klassen die zijn afgeleid van `Activity`, `Application` en `Fragment`, en u gebruikt die klassen of leidt ze verder af in uw app | Ja |
| U neemt een bibliotheek zoals React Native op met klassen die zijn afgeleid van `Activity`, `Application` en `Fragment`, maar u gebruikt alleen statische helpers of hulpklassen | Nee |
| U neemt een bibliotheek op met weergaveklassen die zijn afgeleid van `TextView`, en u gebruikt die klassen of leidt ze verder af in uw app | Ja |

#### <a name="reporting"></a>Rapporten
Met de invoegtoepassing voor builds kan een HTML-rapport worden gegenereerd waarin de gemaakte wijzigingen staan. Als u het genereren van dit rapport wilt aanvragen, geeft u `report = true` op in het configuratieblok `intunemam`. Als het rapport wordt gegenereerd, wordt het naar `outputs/logs` in de directory met builds geschreven.

```groovy
intunemam {
    report = true
}
```

#### <a name="verification"></a>Verificatie
De build-invoegtoepassing kan extra verificatie uitvoeren om te zoeken naar mogelijke fouten in verwerkingsklassen. Als u dit wilt aanvragen, geeft u `verify = true` op in het configuratieblok `intunemam`. Houd er rekening mee dat hierdoor de taak van de invoegtoepassing enkele seconden langer kan duren.

```groovy
intunemam {
    verify = true
}
```


#### <a name="incremental-builds"></a>Incrementele builds
Als u de ondersteuning voor het incrementeel bouwen wilt inschakelen, geeft u `incremental = true` op in het configuratieblok `intunemam`.  Dit is een experimentele functie die is gericht op het verhogen van de prestaties van de build door alleen de invoerbestanden te verwerken die zijn gewijzigd.  De standaardconfiguratie is `false`.

```groovy
intunemam {
    incremental = true
}
```


#### <a name="dependencies"></a>Afhankelijkheden

De Gradle-invoegtoepassing heeft een afhankelijkheid van [Javassist](https://jboss-javassist.github.io/javassist/), dat beschikbaar moet zijn om de afhankelijkheid van Gradle op te lossen (zoals hierboven beschreven). Javassist wordt uitsluitend gebruikt tijdens het opbouwen van de build met de invoegtoepassing. Er wordt geen Javassist-code aan uw app toegevoegd.

> [!NOTE] 
> U moet versie 3.0 of hoger van de Gradle-invoegtoepassing voor Android en Gradle 4.1 of hoger gebruiken.

### <a name="command-line-build-tool"></a>Build-opdrachtregelprogramma
Als u Gradle gebruikt voor uw build, gaat u naar de [volgende sectie](#class-and-method-replacements).

Het build-opdrachtregelprogramma is beschikbaar in de map `BuildTool` van het SDK-pakket. Het voert dezelfde functie uit als de hierboven beschreven Gradle-invoegtoepassing, maar kan worden geïntegreerd in aangepaste of niet-Gradle-build-systemen. Het opdrachtregelprogramma is algemener en complexer om aan te roepen. Daarom kunt u waar mogelijk beter de Gradle-invoegtoepassing gebruiken.

#### <a name="using-the-command-line-tool"></a>Het opdrachtregelprogramma gebruiken

Het opdrachtregelprogramma kan worden aangeroepen met behulp van de verstrekte helperscripts in de map `BuildTool\bin`.

In het hulpprogramma worden de volgende parameters verwacht.

| Parameter | Beschrijving |
| -- | -- |
| `--input` | Een door puntkomma's gescheiden lijst met jar-bestanden en mappen van klassebestanden die u moet wijzigen. Dit omvat alle JAR-bestanden/mappen die u van plan bent opnieuw te schrijven. |
| `--output` | Een door puntkomma's gescheiden lijst met JAR-bestanden en mappen waarin u de gewijzigde klassebestanden moet opslaan. Voor elke invoervermelding moet er één uitvoervermelding zijn, en alle vermeldingen moeten op volgorde staan. |
| `--classpath` | Het klassepad voor de build. Dit kan zowel JAR-bestanden als mappen van klassen bevatten. |
| `--excludeClasses`| Een door puntkomma's gescheiden lijst met de namen van de klassen die niet opnieuw moeten worden geschreven. |

Alle parameters zijn vereist, met uitzondering van de optionele parameter `--excludeClasses`.

> [!NOTE]
> Op met Unix vergelijkbare systemen worden opdrachten gescheiden door een puntkomma. Als u wilt voorkomen dat opdrachten door de shell worden gesplitst, moet u ervoor zorgen dat u elke puntkomma laat voorafgaan door een \' of dat er aanhalingstekens rondom de volledige parameter staan.

#### <a name="example-command-line-tool-invocation"></a>Voorbeeld van een aanroep van het opdrachtregelprogramma

``` batch
> BuildTool\bin\BuildTool.bat --input build\product-foo-project;libs\bar.jar --output mam-build\product-foo-project;mam-build\libs\bar.jar --classpath build\zap.jar;libs\Microsoft.Intune.MAM.SDK\classes.jar;%ANDROID_SDK_ROOT%\platforms\android-27\android.jar --excludeClasses com.contoso.SplashActivity
```

Hierdoor gebeurt het volgende:

* de map `product-foo-project` wordt opnieuw geschreven naar `mam-build\product-foo-project`
* `bar.jar` wordt opnieuw geschreven naar `mam-build\libs\bar.jar`
* `zap.jar` wordt **niet** opnieuw geschreven omdat deze alleen voorkomt in `--classpath`
* De klasse `com.contoso.SplashActivity` wordt **niet** opnieuw geschreven, ook al bevindt deze zich in `--input`

> [!NOTE] 
> AAR-bestanden worden momenteel niet ondersteund in het build-hulpprogramma. Als `classes.jar` niet al wordt uitgepakt door uw build-systeem als er sprake is van AAR-bestanden, moet u dit doen voordat u het build-hulpprogramma aanroept.


## <a name="class-and-method-replacements"></a>Klasse- en methodevervangingen
> [!NOTE] 
> Apps *moeten* integreren met de SDK [build-hulpprogramma's](#build-tooling), die al deze vervangingen automatisch uitvoeren (met uitzondering van [manifestvervangingen](#manifest-replacements))

Android-basisklassen moeten worden vervangen door hun respectieve MAM-equivalenten om Intune-beheer mogelijk te maken. De SDK-klassen begeven zich tussen de Android-basisklasse en de eigen afgeleide app-versie van die klasse. Een app-activiteit kan voorbeeld een overnamehiërarchie krijgen die er als volgt uitziet: `Activity` > `MAMActivity` >
`AppSpecificActivity`. De MAM-laag filtert aanroepen naar systeembewerkingen om uw app naadloos te voorzien van een beheerde weergave van de wereld.

Naast basisklassen kunnen voor bepaalde klassen die uw app gebruikt zonder afleiding (bijvoorbeeld `MediaPlayer`) ook MAM-equivalenten vereist zijn, en [sommige methodeaanroepen moeten ook worden vervangen](#wrapped-system-services). De precieze details worden hieronder beschreven.

> [!NOTE] 
> Als uw app wordt geïntegreerd met [build-hulpprogramma's](#build-tooling) van SDK, worden de volgende klasse- en methodevervangingen automatisch uitgevoerd.

| Android-basisklasse | Intune App SDK-vervanging |
|--|--|
| enroid.app.Activity | MAMActivity |
| enroid.app.ActivityGroup | MAMActivityGroup |
| enroid.app.AliasActivity | MAMAliasActivity |
| enroid.app.Application | MAMApplication |
| android.app.Dialog | MAMDialog |
| android.app.AlertDialog.Builder | MAMAlertDialogBuilder |
| enroid.app.DialogFragment | MAMDialogFragment |
| enroid.app.ExpenableListActivity | MAMExpenableListActivity |
| enroid.app.Fragment | MAMFragment |
| enroid.app.IntentService | MAMIntentService |
| enroid.app.LauncherActivity | MAMLauncherActivity |
| enroid.app.ListActivity | MAMListActivity |
| android.app.ListFragment | MAMListFragment |
| enroid.app.NativeActivity | MAMNativeActivity |
| enroid.app.PendingIntent | MAMPendingIntent (Zie [Pending Intent](#pendingintent)) |
| enroid.app.Service | MAMService |
| enroid.app.TabActivity | MAMTabActivity |
| enroid.app.TaskStackBuilder | MAMTaskStackBuilder |
| enroid.app.backup.BackupAgent | MAMBackupAgent |
| enroid.app.backup.BackupAgentHelper | MAMBackupAgentHelper |
| enroid.app.backup.FileBackupHelper | MAMFileBackupHelper |
| enroid.app.backup.SharePreferencesBackupHelper | MAMSharedPreferencesBackupHelper |
| enroid.content.BroadcastReceiver | MAMBroadcastReceiver |
| enroid.content.ContentProvider | MAMContentProvider |
| enroid.os.Binder | MAMBinder (alleen vereist als de Binder niet is gegenereerd op basis van een AIDL-interface (Android Interface Definition Language)) |
| android.media.MediaPlayer | MAMMediaPlayer |
| android.media.MediaMetadataRetriever | MAMMediaMetadataRetriever |
| enroid.provider.DocumentsProvider | MAMDocumentsProvider |
| enroid.preference.PreferenceActivity | MAMPreferenceActivity |
| android.support.multidex.MultiDexApplication | MAMMultiDexApplication |
| android.widget.TextView | MAMTextView |
| android.widget.AutoCompleteTextView | MAMAutoCompleteTextView |
| android.widget.CheckedTextView | MAMCheckedTextView |
| android.widget.EditText | MAMEditText |
| android.inputmethodservice.ExtractEditText | MAMExtractEditText |
| android.widget.MultiAutoCompleteTextView | MAMMultiAutoCompleteTextView |


> [!NOTE]
> Zelfs als uw toepassing geen eigen afgeleide `Application` klasse nodig heeft, [raadpleegt u `MAMApplication` hieronder](#mamapplication)

### <a name="microsoftintunemamsdksupportv4jar"></a>Microsoft.Intune.MAM.SDK.Support.v4.jar:

| Android-klasse | Intune App SDK-vervanging |
|--|--|
| enroid.suppof eent.v4.app.DialogFragment | MAMDialogFragment
| enroid.suppof eent.v4.app.FragmentActivity | MAMFragmentActivity
| enroid.suppof eent.v4.app.Fragment | MAMFragment
| android.support.v4.app.JobIntentService | MAMJobIntentService
| enroid.suppof eent.v4.app.TaskStackBuilder | MAMTaskStackBuilder
| enroid.suppof eent.v4.content.FileProvider | MAMFileProvider
| android.support.v4.content.WakefulBroadcastReceiver | MAMWakefulBroadcastReceiver

### <a name="microsoftintunemamsdksupportv7jar"></a>Microsoft.Intune.MAM.SDK.Support.v7.jar:

|Android-klasse | Intune App SDK-vervanging |
|--|--|
| android.support.v7.app.AlertDialog.Builder | MAMAlertDialogBuilder |
| android.support.v7.app.AppCompatActivity | MAMAppCompatActivity |
| android.support.v7.widget.AppCompatAutoCompleteTextView | MAMAppCompatAutoCompleteTextView |
| android.support.v7.widget.AppCompatCheckedTextView | MAMAppCompatCheckedTextView |
| android.support.v7.widget.AppCompatEditText | MAMAppCompatEditText |
| android.support.v7.widget.AppCompatMultiAutoCompleteTextView | MAMAppCompatMultiAutoCompleteTextView |
| android.support.v7.widget.AppCompatTextView | MAMAppCompatTextView |

### <a name="microsoftintunemamsdksupportv17jar"></a>Microsoft.Intune.MAM.SDK.Support.v17.jar:
|Android-klasse | Intune App SDK-vervanging |
|--|--|
| android.support.v17.leanback.widget.SearchEditText | MAMSearchEditText |

### <a name="microsoftintunemamsdksupporttextjar"></a>Microsoft.Intune.MAM.SDK.Support.Text.jar:
|Android-klasse | Intune App SDK-vervanging |
|--|--|
| android.support.text.emoji.widget.EmojiAppCompatEditText | MAMEmojiAppCompatEditText |
| android.support.text.emoji.widget.EmojiAppCompatTextView | MAMEmojiAppCompatTextView |
| android.support.text.emoji.widget.EmojiEditText | MAMEmojiEditText |
| android.support.text.emoji.widget.EmojiTextView | MAMEmojiTextView |

### <a name="renamed-methods"></a>Methoden waarvan de naam is gewijzigd

In veel gevallen is een methode die in de Android-klasse beschikbaar is, in de vervangende MAM-klasse als definitief gemarkeerd. De vervangende MAM klasse biedt in dit geval een gelijknamige methode (meestal voorafgegaan door `MAM`) die in plaats daarvan moet worden overschreven. Wanneer een activiteit wordt afgeleid van `MAMActivity`, moet niet `onCreate()` worden overschreven en niet `super.onCreate()` worden aangeroepen, maar moet `Activity``onMAMCreate()` overschrijven en `super.onMAMCreate()` aanroepen. De Java-compiler moet de laatste beperkingen afdwingen om het onbedoeld onderdrukken van de oorspronkelijke methode in plaats van de MAM-equivalent te voorkomen.

### <a name="mamapplication"></a>MAMApplication
Als uw app een subklasse van `android.app.Application` creëert, dan **moet** u in plaats daarvan de subklasse `com.microsoft.intune.mam.client.app.MAMApplication` maken. Als uw app geen subklasse voor `android.app.Application` maakt, dan **moet** u `"com.microsoft.intune.mam.client.app.MAMApplication"` instellen als `"android:name"`-kenmerk in de tag `<application>` van uw AndroidManifest.xml.

### <a name="pendingintent"></a>PendingIntent
In plaats van `PendingIntent.get*` moet u de methode `MAMPendingIntent.get*` gebruiken. Vervolgens kunt u gewoon de resulterende `PendingIntent` gebruiken.

### <a name="wrapped-system-services"></a>Verpakte systeemservices
Voor sommige systeemserviceklassen is het nodig om een statische methode aan te roepen op een MAP-wrapperklasse in plaats van de gewenste methode rechtstreeks aan te roepen op het service-exemplaar. Zo moet een aanroep naar `getSystemService(ClipboardManager.class).getPrimaryClip()` bijvoorbeeld een aanroep naar `MAMClipboardManager.getPrimaryClip(getSystemService(ClipboardManager.class)` worden. Het wordt niet aanbevolen deze vervangingen handmatig aan te brengen. In plaats daarvan kunt u de BuildPlugin dit laten doen.

| Android-klasse | Intune App SDK-vervanging |
|--|--|
| android.content.ClipboardManager | MAMClipboard |
| android.content.ContentProviderClient | MAMContentProviderClientManagement |
| android.content.ContentResolver | MAMContentResolverManagement |
| android.content.pm.PackageManager | MAMPackageManagement |
| android.app.DownloadManager | MAMDownloadManagement |
| android.print.PrintManager | MAMPrintManagement |
| android.support.v4.print.PrintHelper | MAMPrintHelperManagement |
| android.view.View | MAMViewManagement |
| android.view.DragEvent | MAMDragEventManagement |
| android.app.NotificationManager | MAMNotificationManagement |
| android.support.v4.app.NotificationManagerCompat | MAMNotificationCompatManagement |

Voor een aantal klassen zijn de meeste methoden verpakt, zoals `ClipboardManager`, `ContentProviderClient`, `ContentResolver` en `PackageManager`; voor andere klassen zijn slechts een of twee methoden verpakt, zoals  `DownloadManager`, `PrintManager`, `PrintHelper`, `View`, `DragEvent`, `NotificationManager` en `NotificationManagerCompat`. Raadpleeg de API's die beschikbaar worden gemaakt door klassen die het equivalent zijn van MAM voor de exacte methode als u de BuildPlugin niet gebruikt.

### <a name="manifest-replacements"></a>Manifestvervangingen
Het kan nodig zijn om enkele van de bovenstaande klassevervangingen uit te voeren, zowel in het manifest als in de Java-code. Speciale opmerking:
* Manifestverwijzingen naar `android.support.v4.content.FileProvider` moeten worden vervangen door `com.microsoft.intune.mam.client.support.v4.content.MAMFileProvider`.

## <a name="androidx-libraries"></a>AndroidX-bibliotheken
Google heeft met Android P een nieuwe (gewijzigde) set ondersteuningsbibliotheken, AndroidX, aangekondigd en versie 28 is de laatste belangrijke nieuwe versie van de bestaande ondersteuningsbibliotheken voor Android.

In tegenstelling tot de Android-ondersteuningsbibliotheken bieden we geen MAM-varianten van de AndroidX-bibliotheken. In plaats daarvan moet AndroidX worden behandeld als een externe bibliotheek en moet deze worden geconfigureerd om opnieuw te worden geschreven met de build-invoegtoepassing of het build-hulpprogramma. Voor Gradle-builds kunt u dit doen door `androidx.*` op te nemen in het veld `includeExternalLibraries` van de configuratie van de invoegtoepassing. In aanroepen van het opdrachtregelprogramma moeten alle JAR-bestanden expliciet worden vermeld.

### <a name="pre-androidx-architecture-components"></a>Architectuuronderdelen vóór AndroidX
Veel Android-architectuuronderdelen, waaronder Room, ViewModel en WorkManager, zijn opnieuw ingepakt voor AndroidX. Als uw app gebruikmaakt van de varianten van vóór AndroidX van deze bibliotheken, moet u ervoor zorgen dat herschrijfbewerkingen van toepassing zijn door `android.arch.*` op te nemen in het veld `includeExternalLibraries` van de configuratie van de invoegtoepassing. U kunt de bibliotheken ook bijwerken naar de bijbehorende AndroidX-equivalenten.

### <a name="troubleshooting-androidx-migration"></a>Problemen met AndroidX-migratie oplossen
Tijdens het migreren van uw met SDK geïntegreerde app naar AndroidX kan een fout als de volgende optreden:

```log
incompatible types: android.support.v7.app.ActionBar cannot be converted to androidx.appcompat.app.ActionBar
```

Deze fouten kunnen optreden omdat uw app verwijst naar MAM-ondersteuningsklassen. MAM-ondersteuningsklassen verpakken Android-ondersteuningsklassen die zijn verplaatst in AndroidX. Als u dergelijke fouten wilt bestrijden, vervangt u alle MAM-ondersteuningsklasseverwijzingen door hun AndroidX-equivalenten. Dit kan worden bereikt door eerst de afhankelijkheden van de MAM-ondersteuningsbibliotheek te verwijderen uit uw Gradle-build-bestanden. De betreffende regels zien er ongeveer als volgt uit:

```Gradle
implementation "com.microsoft.intune.mam:android-sdk-support-v4:$intune_mam_version"
implementation "com.microsoft.intune.mam:android-sdk-support-v7:$intune_mam_version"
```

Los vervolgens de resulterende compilatiefouten op door alle verwijzingen naar MAM-klassen in de pakketten `com.microsoft.intune.mam.client.support.v7` en `com.microsoft.intune.mam.client.support.v4` te vervangen door hun AndroidX-equivalenten. Verwijzingen naar `MAMAppCompatActivity` moeten bijvoorbeeld worden gewijzigd in de `AppCompatActivity` van AndroidX. Zoals hierboven wordt beschreven, herschrijft de invoegtoepassing/het hulpprogramma van de MAM-build automatisch klassen in de AndroidX-bibliotheken met de juiste MAM-equivalenten tijdens het compileren.

## <a name="sdk-permissions"></a>SDK-machtigingen

De Intune App SDK vereist drie [Android-systeemmachtigingen](https://developer.android.com/guide/topics/security/permissions.html) voor apps waarin de SDK wordt geïntegreerd:

* `android.permission.GET_ACCOUNTS` (indien nodig aangevraagd tijdens runtime)

* `android.permission.MANAGE_ACCOUNTS`

* `android.permission.USE_CREDENTIALS`

Deze machtigingen zijn vereist voor Azure Active Directory Authentication Library ([ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/)) om brokered verificatie uit te voeren. Als deze machtigingen niet worden toegekend aan de app of worden ingetrokken door de gebruiker, worden verificatiestromen waarvoor de broker (de bedrijfsportal-app) is vereist, uitgeschakeld.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.

## <a name="logging"></a>Logboekregistratie

Logboekregistratie moet vroegtijdig worden geïnitialiseerd om de meeste waarde uit de gegevens in het logboek te halen. `Application.onMAMCreate()` is doorgaans de beste plaats om logboekregistratie te initialiseren.

Als u MAM-logboeken in uw app wilt ontvangen, maakt u een [Java-handler](https://docs.oracle.com/javase/7/docs/api/java/util/logging/Handler.html) en voegt u deze toe aan de `MAMLogHandlerWrapper`. Zodoende wordt `publish()` aangeroepen voor de toepassingshandler voor elk logboekbericht.

```java
/**
 * Global log handler that enables fine grained PII filtering within MAM logs.  
 *
 * To start using this you should build your own log handler and add it via
 * MAMComponents.get(MAMLogHandlerWrapper.class).addHandler(myHandler, false);  
 *
 * You may also remove the handler entirely via
 * MAMComponents.get(MAMLogHandlerWrapper.class).removeHandler(myHandler);
 */
public interface MAMLogHandlerWrapper {
    /**
     * Add a handler, PII can be toggled.
     *
     * @param handler handler to add.
     * @param wantsPII if PII is desired in the logs.    
     */
    void addHandler(final Handler handler, final boolean wantsPII);

    /**
     * Remove a handler.
     *
     * @param handler handler to remove.
     */
    void removeHandler(final Handler handler);
}
```

## <a name="diagnostics-information"></a>Diagnostische informatie
Apps kunnen de methode `MAMPolicyManager.showDiagnostics(context)` aanroepen waarmee een activiteit wordt gestart die de gebruikersinterface weergeeft om logboeken van Bedrijfsportal te verzamelen en diagnostische MAM-gegevens weer te geven.
Dit is een optionele functie die kan helpen bij het opsporen van fouten.

Als Bedrijfsportal niet op het apparaat is geïnstalleerd, wordt er een dialoogvenster weergegeven om de gebruiker te informeren dat deze informatie op dit moment niet beschikbaar is. Wanneer apps worden beheerd door MAM-beleid, worden gedetailleerde MAM-beleidsinstellingen weergegeven.

## <a name="mam-strict-mode"></a>Strict-modus voor MAM
De Strict-modus voor MAM biedt een mechanisme om 'geuren' te detecteren in app-gebruik van MAM API's of door MAM beperkte platform-API's. Het is losjes gebaseerd op de StrictMode van Android en voert een set controles uit die fouten veroorzaken wanneer ze mislukken. Het is niet bedoeld om ingeschakeld te blijven in productieversies, maar het wordt *ten zeerste aangeraden* om het te gebruiken in de interne builds voor ontwikkeling, foutopsporing en/of testen van uw app.

Als u deze optie wilt inschakelen, roept u

```java
MAMStrictMode.enable();
```
 vroeg in de initialisatie van de toepassing aan (bijvoorbeeld `Application.onCreate`). 

Wanneer een MAM Strict Mode-controle mislukt, probeert u vast te stellen of het een echt probleem is dat in uw app kan worden opgelost of dat het een fout-positief is. Als u denkt dat het een fout-positief is, of als u het niet zeker weet, informeert u het Intune MAM-team. Wij kunnen dan kijken of de vaststelling van de fout-positief klopt en proberen detectie voor toekomstige releases te verbeteren. Als u fout-positieven wilt onderdrukken, schakelt u de mislukte controle uit (meer informatie hieronder).

### <a name="handling-violations"></a>Overtredingen verwerken
Wanneer een controle mislukt, wordt een `MAMStrictViolationHandler` uitgevoerd. De standaardhandler genereert een `Error`, waardoor de app waarschijnlijk zal vastlopen. Dit wordt gedaan om storingen zo opvallend mogelijk te maken en past bij de bedoeling dat de strikte modus niet moet worden ingeschakeld in productie-builds.

Als uw app overtredingen op een andere manier wil afhandelen, kan deze een eigen handler leveren door het volgende aan te roepen:

```java
MAMStrictMode.global().setHandler(handler);
```

waar `handler` `MAMStrictViolationHandler` implementeert:

```java
public interface MAMStrictViolationHandler {
    /**
     * Called when a MAM Strict Mode check fails.
     *
     * @param check
     *         the check that failed
     * @param detail
     *         additional detail. Note that this might contain usernames or filepaths.
     * @param error
     *         error containing a stack trace. The default implementation throws this error
     */
    void checkFailed(@NonNull MAMStrictCheck check, @NonNull String detail, @NonNull Error error);
}
```

### <a name="suppressing-checks"></a>Controles onderdrukken
Als een controle mislukt wanneer uw app niets verkeerd doet, meldt u dit dan zoals hierboven is vermeld. Soms kan het echter nodig zijn om de controle die een fout-positief tegenkomt uit te schakelen, in ieder geval tijdens het wachten op een bijgewerkte SDK. De controle die mislukt wordt weergegeven in de fout die wordt veroorzaakt door de standaardhandler, of wordt doorgegeven aan een aangepaste handler als deze is ingesteld.

Onderdrukking kan op algemene schaal plaatsvinden, maar het tijdelijk uitschakelen per thread op de specifieke aanroepsite verdient de voorkeur. In de volgende voorbeelden ziet u verschillende manieren om `MAMStrictCheck.IDENTITY_NO_SUCH_FILE` uit te schakelen (deze gebeurtenis treedt op als wordt geprobeerd om een bestand te beveiligen dat niet bestaat).


#### <a name="per-thread-temporary-suppression"></a>Tijdelijke onderdrukking per thread
Dit is het voorkeursmechanisme voor onderdrukking.
```java
try (StrictScopedDisable disable = MAMStrictMode.thread().disableScoped(MAMStrictCheck.IDENTITY_NO_SUCH_FILE)) {
    // Perform the operation which raised a violation here
}
// The check is no longer disabled once the block exits
```

#### <a name="per-thread-permanent-suppression"></a>Permanente onderdrukking per thread
```java
MAMStrictMode.thread().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```

#### <a name="global-process-wide-suppression"></a>Globale onderdrukking (procesbreed)
```java
MAMStrictMode.global().disable(MAMStrictCheck.IDENTITY_NO_SUCH_FILE);
```



## <a name="enable-features-that-require-app-participation"></a>Functies inschakelen waarvoor app-deelname is vereist

Er zijn verschillende beleidsregels voor de beveiliging van apps die de SDK niet op zichzelf kan implementeren. De app kan het eigen gedrag voor deze functies bepalen door gebruik te maken van de verschillende API's in de volgende `AppPolicy`-interface. Als u een exemplaar van `AppPolicy` wilt ophalen, gebruikt u `MAMPolicyManager.getPolicy`.

```java
/**
 * External facing application policies.
 */
public interface AppPolicy {

/**
 * Restrict where an app can save personal data.
 * This function is now deprecated. Use getIsSaveToLocationAllowed(SaveLocation, String) instead
 * @return True if the app is allowed to save to personal data stores; false otherwise.
 */
@Deprecated
boolean getIsSaveToPersonalAllowed();

/**
 * Check if policy prohibits saving to a content provider location.
 *
 * @param location
 *            a content URI to check
 * @return True if location is not a content URI or if policy does not prohibit saving to the content location.
 */
boolean getIsSaveToLocationAllowed(Uri location);

/**
 * Determines if the SaveLocation passed in can be saved to by the username associated with the cloud service.
 *
 * @param service
 *           The SaveLocation the data will be saved to.
 * @param username
 *           The AAD UPN associated with the cloud service being saved to. Use null if a mapping between
 *           the AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the location can be saved to by the identity, false if otherwise.
 */
boolean getIsSaveToLocationAllowed(SaveLocation service, String username);

/**
 * Determines if data from the OpenLocation can be opened for the username associated with the data.
 *
 * @param location
 *      The OpenLocation that the data will be opened from.
 * @param username
 *      The AAD UPN associated with the location the data is being opened from. Use null if a mapping between the
 *      AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the data can be opened from the location for the identity, false if otherwise.
 */
boolean getIsOpenFromLocationAllowed(@NonNull OpenLocation location, @Nullable String username);

/**
 * Checks whether any activities which could handle the given intent are allowed by policy. Returns false only if all
 * activities which could otherwise handle the intent are blocked. If there are no activities which could handle the intent
 * regardless of policy, returns true. If some activities are allowed and others blocked, returns true. Note that it is not
 * necessary to use this method for policy enforcement. If your app attempts to launch an intent for which there are no
 * allowed activities, MAM will display a dialog explaining the situation to the user.
 *
 * @param intent
 *         intent to check
 *
 * @return whether any activities which could handle this intent are allowed.
*/
boolean areIntentActivitiesAllowed(Intent intent);

/**
 * Whether the SDK PIN prompt is enabled for the app.
 *
 * @return True if the PIN is enabled. False otherwise.
 */
boolean getIsPinRequired();

/**
 * Whether the Intune Managed Browser is required to open web links.
 * @return True if the Managed Browser is required, false otherwise
 */
boolean getIsManagedBrowserRequired();

/**
 * Check if policy allows taking screenshots.
 *
 * @return True if screenshots will be blocked, false otherwise
 */
boolean getIsScreenCaptureAllowed();

/**
 * Check if policy allows Contact sync to local contact list.
 *
 * @return True if Contact sync is allowed to save to local contact list; false otherwise.
 */
boolean getIsContactSyncAllowed();

/**
 * Get the notification restriction. If {@link NotificationRestriction#BLOCKED BLOCKED}, the app must not show any notifications
 * for the user associated with this policy. If {@link NotificationRestriction#BLOCK_ORG_DATA BLOCK_ORG_DATA}, the app must show
 * a modified notification that does not contain organization data. If {@link NotificationRestriction#UNRESTRICTED
 * UNRESTRICTED}, all notifications are allowed.
 *
 * @return The notification restriction.
 */
NotificationRestriction getNotificationRestriction();

/**
 * This method is intended for diagnostic/telemetry purposes only. It can be used to discover whether file encryption is in use.
 * File encryption is transparent to the app and the app should not need to make any business logic decisions based on this.
 * @return True if file encryption is in use.
 */
boolean diagnosticIsFileEncryptionInUse();

/**
 * Return the policy in string format to the app.
 *  
 * @return The string representing the policy.
 */
String toString();

}
```

> [!NOTE]
> `MAMPolicyManager.getPolicy` retourneert altijd een niet-null-app-beleid, zelfs als voor het apparaat of de app geen Intune-beheerbeleid van toepassing is.

### <a name="example-determine-if-pin-is-required-for-the-app"></a>Voorbeeld: Bepalen of er een pincode is vereist voor de app

Als de app zijn eigen gebruikerservaring voor de pincode heeft, wilt u deze mogelijk uitschakelen als de IT-beheerder de SDK zodanig heeft geconfigureerd dat naar de pincode van het apparaat wordt gevraagd. Als u wilt bepalen of de IT-beheerder het app-pincodebeleid voor deze app heeft geïmplementeerd voor de huidige gebruiker, roept u de volgende methode aan:

```java

MAMPolicyManager.getPolicy(currentActivity).getIsPinRequired();
```

### <a name="example-determine-the-primary-intune-user"></a>Voorbeeld: De primaire Intune-gebruiker bepalen

Naast de API's die worden weergegeven in AppPolicy, wordt ook de user principal name (**UPN**) weergegeven door de `getPrimaryUser()`-API zoals gedefinieerd in de `MAMUserInfo`-interface. U kunt de UPN verkrijgen door het volgende aan te roepen:

```java
MAMComponents.get(MAMUserInfo.class).getPrimaryUser();
```

De volledige definitie van de MAMUserInfo-interface vindt u hieronder:

```java
/**
 * External facing user information.
 *
 */
public interface MAMUserInfo {
       /**
        * Get the primary user name.
        *
        * @return the primary user name or null if neither the device nor app is enrolled.
        */
       String getPrimaryUser();
}
```

### <a name="example-data-transfer-between-apps-and-device-or-cloud-storage-locations"></a>Voorbeeld: Gegevensoverdracht tussen apps en apparaten of opslaglocaties in de cloud

Veel apps implementeren functies waarmee de eindgebruiker gegevens kan opslaan of gegevens kan openen vanuit lokale bestands- of cloudopslagservices.
Met de Intune App SDK kunnen IT-beheerders beveiliging instellen tegen inkomende gegevens en het lekken van gegevens door naar eigen goeddunken beleidsbeperkingen binnen hun organisatie toe te passen.

**Voor het inschakelen van de functie is app-deelname vereist.**
Als uw app de mogelijkheid biedt om rechtstreeks vanuit de app naar persoonlijke of cloudlocaties op te slaan *of* toestaat dat gegevens rechtstreeks in de app worden geopend, moet u deze functie implementeren om ervoor te zorgen dat de IT-beheerder kan bepalen of opslaan naar of openen vanaf een locatie is toegestaan.

#### <a name="saving-to-device-or-cloud-storage"></a>Opslaan op apparaat of in cloudopslag

De onderstaande API laat de app weten of opslaan naar een persoonlijke opslag volgens het huidige beleid van de Intune-beheerder is toegestaan.

Voer de volgende aanroep uit om te bepalen of het beleid wordt afgedwongen:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(
SaveLocation service, String username);
```

De parameter `service` moet een van de volgende `SaveLocation`-waarden hebben:

* `SaveLocation.ONEDRIVE_FOR_BUSINESS`
* `SaveLocation.SHAREPOINT`
* `SaveLocation.LOCAL`
* `SaveLocation.ACCOUNT_DOCUMENT`
* `SaveLocation.OTHER`

Als u wilt bepalen of `ACCOUNT_DOCUMENT` of `OTHER` moet worden door gegeven aan `getIsSaveToLocationAllowed`, raadpleegt u [Onbekende of niet-vermelde locaties](#unknown-or-unlisted-locations) voor meer informatie.

Zie [Gebruikersnaam voor gegevensoverdracht](#username-for-data-transfer) voor meer informatie voor de parameter `username`.

De vorige methode waarmee kon worden bepaald of het overeenkomstig het beleid van een gebruiker was toegestaan om gegevens op te slaan naar verschillende locaties, was `getIsSaveToPersonalAllowed()` in dezelfde **AppPolicy**-klasse.
Deze functie wordt nu **afgeschaft** en mag niet worden gebruikt. De volgende aanroep is gelijk aan `getIsSaveToPersonalAllowed()`:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(SaveLocation.LOCAL, null);
```

#### <a name="opening-data-from-a-local-or-cloud-storage-location"></a>Gegevens openen vanuit een lokale locatie of een cloudopslaglocatie

De onderstaande API laat de app weten of openen vanaf een persoonlijke opslag volgens het huidige beleid van de Intune-beheerder is toegestaan.

Voer de volgende aanroep uit om te bepalen of het beleid wordt afgedwongen:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsOpenFromLocationAllowed(
OpenLocation location, String username);
```

De parameter `location` moet een van de volgende `OpenLocation`-waarden hebben:

* `OpenLocation.ONEDRIVE_FOR_BUSINESS`
* `OpenLocation.SHAREPOINT`
* `OpenLocation.CAMERA`
* `OpenLocation.LOCAL`
* `OpenLocation.ACCOUNT_DOCUMENT`
* `OpenLocation.OTHER`

De locatie `OpenLocation.CAMERA` moet worden door gegeven wanneer de app gegevens vanuit de camera opent.
De locatie `OpenLocation.LOCAL` moet worden door gegeven wanneer de app gegevens opent vanuit de externe opslag op het lokale apparaat.
De locatie `OpenLocation.ACCOUNT_DOCUMENT` moet worden doorgegeven wanneer de app gegevens opent die horen bij een AAD-account dat is aangemeld bij de app.

Als u wilt bepalen of `ACCOUNT_DOCUMENT` of `OTHER` moet worden door gegeven aan `getIsOpenFromLocationAllowed`, raadpleegt u [Onbekende of niet-vermelde locaties](#unknown-or-unlisted-locations) voor meer informatie.

Zie [Gebruikersnaam voor gegevensoverdracht](#username-for-data-transfer) voor meer informatie voor de parameter `username`.

#### <a name="unknown-or-unlisted-locations"></a>Onbekende of niet-vermelde locaties

Wanneer de gewenste locatie niet wordt weergegeven in de opsommingen `SaveLocation` of `OpenLocation` of onbekend is, zijn er twee opties voor de `service`/`location`-parameter, `ACCOUNT_DOCUMENT` en `OTHER`.
`ACCOUNT_DOCUMENT` moet worden gebruikt wanneer de gegevens horen bij een AAD-account dat is aangemeld bij de app, maar niet `ONEDRIVE_FOR_BUSINESS` of `SHAREPOINT` is, terwijl `OTHER` moet worden gebruikt als dat niet het geval is.

Het is belangrijk om het verschil duidelijk te maken tussen het beheerde account en een account dat de UPN van het beheerde account deelt.
Een beheerd account met UPN user@contoso.com dat is aangemeld in OneDrive is bijvoorbeeld niet hetzelfde als een account met UPN user@contoso.com dat is aangemeld in Dropbox.
Als een onbekende of niet-vermelde service wordt geopend door aanmelding bij het beheerde account (user@contoso.com is bijvoorbeeld aangemeld bij OneDrive), moet dit worden vertegenwoordigd door de `ACCOUNT_DOCUMENT`-locatie.
Als de onbekende of niet-vermelde service wordt aangemeld via een ander account (bijvoorbeeld user@contoso.com, ondertekend in Dropbox), heeft het geen toegang tot de locatie met een beheerd account en moet het worden vertegenwoordigd door de `OTHER`-locatie.

#### <a name="username-for-data-transfer"></a>Gebruikersnaam voor gegevensoverdracht

Wanneer het beleid voor opslaan wordt gecontroleerd, moet de `username` de waarde voor UPN/gebruikersnaam/e-mailadres zijn die aan de cloudservice is gekoppeld waarin items worden opgeslagen (*niet* noodzakelijkerwijs dezelfde gebruiker als de eigenaar van het document dat wordt opgeslagen).
`SaveLocation.LOCAL` is geen cloudservice en moet dus altijd worden gebruikt met een `null`-gebruikersnaamparameter.

Bij het controleren van het beleid voor openen, moet de `username` het UPN/gebruikersnaam/e-mailadres zijn dat is gekoppeld aan de cloudservice die wordt geopend.
`OpenLocation.LOCAL` en `OpenLocation.CAMERA` zijn geen cloudservicelocaties en moeten dus altijd worden gebruikt met een `null`-gebruikersnaamparameter.

Op de volgende locaties wordt altijd een gebruikersnaam verwacht die een toewijzing bevat tussen de AAD-UPN en de gebruikersnaam van de cloudservice: `ONEDRIVE_FOR_BUSINESS`, `SHAREPOINT` en `ACCOUNT_DOCUMENT`.

Als er geen toewijzing tussen de AAD UPN en de gebruikersnaam voor de cloudservice bestaat of als de gebruikersnaam onbekend is, gebruikt u `null`.

#### <a name="sharing-blocked-dialog"></a>Dialoogvenster delen geblokkeerd

De SDK biedt een dialoogvenster waarmee de gebruiker wordt gewaarschuwd dat een actie voor gegevensoverdracht is geblokkeerd door MAM-beleid.

Het dialoogvenster moet worden weergegeven aan de gebruiker wanneer de API-aanroep `isSaveToAllowedForLocation` of `isOpenFromAllowedForLocation` ertoe leidt dat de actie opslaan/openen wordt geblokkeerd.
In het dialoogvenster wordt een algemeen bericht weergegeven. Er wordt teruggekeerd naar de `Activity` die het heeft aangeroepen wanneer deze wordt genegeerd.

Als u het dialoogvenster wilt weergeven, maakt u de volgende aanroep:

``` java
MAMUIHelper.showSharingBlockedDialog(currentActivity)
```

### <a name="allow-for-file-sharing"></a>Delen van bestanden toestaan

Als het opslaan naar een openbare opslag locatie niet is toegestaan, moet uw app de gebruiker nog steeds bestanden laten weergeven door deze te downloaden naar [privé-opslag van de app](https://developer.android.com/training/data-storage) en deze vervolgens te openen met de systeemkiezer.

### <a name="example-determine-if-notifications-with-organization-data-need-to-be-restricted"></a>Voorbeeld: Bepalen of meldingen met organisatiegegevens moeten worden beperkt

Als uw app meldingen weergeeft, moet u het restrictiebeleid voor de gebruiker controleren dat is gekoppeld aan de melding voordat de melding wordt weergegeven. Voer de volgende aanroep uit om te bepalen of het beleid wordt afgedwongen.

```java
NotificationRestriction notificationRestriction =
    MAMPolicyManager.getPolicyForIdentity(notificationIdentity).getNotificationRestriction();
```

Als de beperking `BLOCKED` is, mag de app geen meldingen weergeven voor de gebruiker die aan dit beleid is gekoppeld. Indien `BLOCK_ORG_DATA`, moet de app een gewijzigde melding weergeven die geen organisatiegegevens bevat. Indien `UNRESTRICTED`, zijn alle meldingen toegestaan.

Als `getNotificationRestriction` niet wordt aangeroepen, probeert de MAM SDK om meldingen automatisch te beperken voor apps met één identiteit. Als automatisch blokkeren is ingeschakeld en `BLOCK_ORG_DATA` is ingesteld, wordt de melding helemaal niet weergegeven. Controleer voor meer nauwkeurige controle de waarde van `getNotificationRestriction` en wijzig app-meldingen dienovereenkomstig.

## <a name="register-for-notifications-from-the-sdk"></a>Registreren voor meldingen van de SDK

### <a name="overview"></a>Overzicht
Met de SDK voor de Intune-app kan uw app de werking van bepaald beleid, zoals selectief wissen, beheren bij implementatie door de IT-beheerder. Als een IT-beheerder dergelijk beleid implementeert, wordt met de Intune-service een melding naar de SDK verzonden.

Uw app moet worden geregistreerd voor meldingen van de SDK door een `MAMNotificationReceiver` te maken en deze te registreren met `MAMNotificationReceiverRegistry`. Dit wordt gedaan door de ontvanger en het gewenste type melding op te geven in `App.onCreate`, zoals in het volgende voorbeeld te zien is:

```java
@Override
public void onCreate() {
  super.onCreate();
  MAMComponents.get(MAMNotificationReceiverRegistry.class)
    .registerReceiver(
      new ToastNotificationReceiver(),
      MAMNotificationType.WIPE_USER_DATA);
}
```

### <a name="mamnotificationreceiver"></a>MAMNotificationReceiver

De `MAMNotificationReceiver`-interface ontvangt gewoon meldingen van de Intune-service. Sommige meldingen worden rechtstreeks door de SDK verwerkt, terwijl andere deelname van de app vereisen. Een app **moet** Waar of Onwaar retourneren vanaf een melding. De app moet altijd Waar retourneren, tenzij een bepaalde actie die de app naar aanleiding van de melding probeerde uit te voeren, is mislukt.

* Deze fout kan worden gerapporteerd aan de Intune-service. Een voorbeeld van een scenario waarin moet worden gerapporteerd, is als de app geen gebruikersgegevens kan wissen nadat de IT-beheerder een wisactie heeft gestart.

>[!NOTE]
> Het is veilig om te blokkeren in `MAMNotificationReceiver.onReceive`, omdat de callback niet wordt uitgevoerd op de UI-thread.

De interface van `MAMNotificationReceiver`, zoals gedefinieerd in de SDK, is hieronder opgenomen:

```java
/**
 * The SDK is signaling that a MAM event has occurred.
 *
 */
public interface MAMNotificationReceiver {

    /**
     * A notification was received.
     *
     * @param notification
     *            The notification that was received.
     * @return The receiver should return true if it handled the
     *   notification without error (or if it decided to ignore the
     *   notification). If the receiver tried to take some action in
     *   response to the notification but failed to complete that
     *   action it should return false.
     */
    boolean onReceive(MAMNotification notification);
}
```

### <a name="types-of-notifications"></a>Typen meldingen

De volgende meldingen worden verzonden naar de app en enkele ervan vereisen mogelijk app-deelname:

* **WIPE_USER_DATA**: Deze melding wordt verzonden in een `MAMUserNotification`-klasse. Wanneer deze melding wordt ontvangen, *moet* de app alle gegevens verwijderen die zijn gekoppeld aan de beheerde identiteit (van `MAMUserNotification.getUserIdentity()`). De melding kan om verschillende redenen optreden, bijvoorbeeld wanneer uw app `unregisterAccountForMAM` aanroept, wanneer een IT-beheerder een wisopdracht initieert of wanneer er niet wordt voldaan aan door de beheerder vereiste beleidsregels voor voorwaardelijke toegang. Als uw app niet voor deze melding wordt geregistreerd, wordt het standaardgedrag voor wissen uitgevoerd. Het standaardgedrag verwijdert alle bestanden voor een app met één identiteit of alle bestanden die zijn gelabeld met de beheerde identiteit in het geval van een app met meerdere identiteiten. Deze melding wordt nooit verzonden op de UI-thread.

* **WIPE_USER_AUXILIARY_DATA**: Apps kunnen zich voor deze melding registreren als de Intune App SDK de standaardactie voor selectief wissen moet uitvoeren, maar er nog steeds bepaalde aanvullende gegevens moeten worden verwijderd wanneer het wissen wordt uitgevoerd. Deze melding is niet beschikbaar voor apps met één identiteit, maar wordt alleen verzonden naar apps met meerdere identiteiten. Deze melding wordt nooit verzonden op de UI-thread.

* **REFRESH_POLICY**: Deze melding wordt verzonden in een `MAMUserNotification`. Wanneer deze melding wordt ontvangen, moeten alle beslissingen over Intune-beleid die via uw app in de cache zijn geplaatst, ongeldig worden gemaakt en worden bijgewerkt. Als beleidsveronderstellingen niet door uw app worden opgeslagen, hoeft u de app niet te registreren voor deze melding. Er worden geen garanties gegeven met betrekking tot naar welke thread deze melding wordt verzonden.

* **REFRESH_APP_CONFIG**: Deze melding wordt verzonden in een `MAMUserNotification`. Wanneer deze melding wordt ontvangen, moeten alle toepassingsconfiguratiegegevens in de cache ongeldig worden gemaakt en worden bijgewerkt. Er worden geen garanties gegeven met betrekking tot naar welke thread deze melding wordt verzonden.

* **MANAGEMENT_REMOVED**: Deze melding wordt verzonden in een `MAMUserNotification` en informeert de app dat deze binnenkort niet meer wordt beheerd. Zodra de app niet meer wordt beheerd, kan deze geen versleutelde bestanden en met MAMDataProtectionManager versleutelde gegevens meer lezen, geen gebruik meer maken van het versleutelde klembord of anderszins deelnemen aan het ecosysteem van beheerde apps. Zie hieronder voor meer informatie. Deze melding wordt nooit verzonden op de UI-thread.

* **MAM_ENROLLMENT_RESULT**: Deze melding wordt verzonden in een `MAMEnrollmentNotification` om de app ervan op de hoogte te brengen dat de poging tot APP-WE-inschrijving is voltooid en om de status van die poging op te geven. Er worden geen garanties gegeven met betrekking tot naar welke thread deze melding wordt verzonden.

* **COMPLIANCE_STATUS**: Deze melding wordt verzonden in een `MAMComplianceNotification` om de app op de hoogte te brengen van de resultaten van een nalevingsherstelpoging. Er worden geen garanties gegeven met betrekking tot naar welke thread deze melding wordt verzonden.

> [!NOTE]
> Een app moet nooit voor zowel `WIPE_USER_DATA`- als `WIPE_USER_AUXILIARY_DATA`-meldingen.

### <a name="management_removed"></a>MANAGEMENT_REMOVED

De melding `MANAGEMENT_REMOVED` geeft aan dat een eerder door beleid beheerde gebruiker niet langer door het Intune MAM-beleid wordt beheerd. Gebruikersgegevens hoeven hiervoor niet te worden gewist en gebruikers hoeven niet te worden afgemeld (als wissen is vereist, wordt een `WIPE_USER_DATA`-melding verzonden). Deze melding hoeft door de meeste apps helemaal niet te worden verwerkt, maar apps die `MAMDataProtectionManager` gebruiken, moeten wel [aandacht besteden van deze melding](#data-protection).

Wanneer de `MANAGEMENT_REMOVED`-ontvanger van de app door MAM wordt aangeroepen, is het volgende waar:
* Eerder versleutelde bestanden die bij de app horen, zijn al door MAM versleuteld (maar gegevensbuffers zijn niet beveiligd). Bestanden op openbare locaties op de SD-kaart die niet direct bij de app horen (zoals de mappen Documenten of Download), worden niet versleuteld.
* Nieuwe bestanden of beveiligde gegevensbuffers die volgens de ontvangermethode (of volgens andere code die wordt uitgevoerd zodra de ontvanger is gestart) zijn gemaakt, worden niet versleuteld.
* De app heeft nog steeds toegang tot versleutelingssleutels, dus bewerkingen zoals de ontsleuteling van gegevensbuffers worden uitgevoerd.

Zodra de ontvanger van uw app wordt geretourneerd, heeft deze niet langer toegang tot versleutelingssleutels.

## <a name="configure-azure-active-directory-authentication-library-adal"></a>Azure Active Directory Authentication Library (ADAL) configureren

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.

Lees eerst de richtlijnen voor de integratie van ADAL in de [ADAL-bibliotheek op GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android).

De SDK is afhankelijk van [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) voor de [verificatie](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) en voorwaardelijke startscenario's, die vereisen dat apps worden geconfigureerd met [Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-whatis/). De configuratiewaarden worden aan de SDK doorgegeven via de metagegevens van AndroidManifest.

Als u uw app wilt configureren en de juiste verificatie wilt inschakelen, voegt u het volgende toe aan het app-knooppunt in het bestand AndroidManifest.xml. Sommige van deze configuratie-instellingen zijn alleen vereist als uw app gebruikmaakt van ADAL voor verificatie in het algemeen. In dat geval hebt u de specifieke waarden nodig waarmee uw app zich bij AAD registreert. Dit wordt gedaan om ervoor te zorgen dat de eindgebruiker niet twee keer om verificatie wordt gevraagd doordat AAD twee afzonderlijke registratiewaarden herkent: één van de app en één van de SDK.

```xml
<meta-data
    android:name="com.microsoft.intune.mam.aad.Authority"
    android:value="https://AAD authority/" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.ClientID"
    android:value="your-client-ID-GUID" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.NonBrokerRedirectURI"
    android:value="your-redirect-URI" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.SkipBroker"
    android:value="[true | false]" />
```

### <a name="adal-metadata"></a>ADAL-metagegevens

* **Instantie** is de huidige AAD-instantie die wordt gebruikt. Als deze waarde afwezig is, wordt de openbare AAD-omgeving gebruikt.
    > [!NOTE]
    > Stel dit veld niet in als uw toepassing bewust is van onafhankelijke clouds.

* **ClientID** is de ClientID van AAD (ook wel toepassings-id genoemd) die moet worden gebruikt. U moet de ClientID van uw eigen app gebruiken als deze is geregistreerd bij Azure AD of gebruikmaken van [Standaardinschrijving](#default-enrollment-optional) als deze niet is geïntegreerd met ADAL.

* **NonBrokerRedirectURI** AAD-omleidings-URI die moet worden gebruikt in gevallen zonder broker. Als er niets is opgegeven, wordt er een standaardwaarde van `urn:ietf:wg:oauth:2.0:oob` gebruikt. Deze standaardinstellingen is geschikt voor meeste apps.

  * De NonBrokerRedirectURI wordt alleen gebruikt als SkipBroker de waarde true heeft.

* **SkipBroker** wordt gebruikt om het standaardgedrag van ADAL-deelname aan eenmalige aanmelding te overschrijven. SkipBroker moet alleen worden opgegeven voor apps waarvoor een ClientID is opgegeven **en** die geen ondersteuning bieden voor brokered verificatie/apparaatbrede eenmalige aanmelding. In dit geval moet de waarde true worden ingesteld. Voor de meeste apps moet de SkipBroker-parameter niet worden ingesteld.

  * Er **moet** een ClientID worden opgegeven in het manifest om een SkipBroker-waarde op te geven.

  * Als er een ClientID is opgegeven, is de standaardwaarde false.

  * Als SkipBroker is ingesteld op true, wordt de NonBrokerRedirectURI gebruikt. Apps zonder integratie van ADAL (en die daarom geen ClientID hebben) worden standaard ook ingesteld op true.

### <a name="common-adal-configurations"></a>Algemene ADAL-configuraties

Hieronder volgen enkele algemene manieren waarop een app kan worden geconfigureerd met ADAL. Zoek de configuratie van uw app en zorg ervoor dat u de metagegevens van de ADAL-parameters (hierboven uitgelegd) instelt op de benodigde waarden. In alle gevallen kan er desgewenst een autoriteit worden opgegeven voor niet-standaard omgevingen. Als er niets wordt opgegeven, wordt de openbare AAD-autoriteit voor productie gebruikt.

#### <a name="1-app-does-not-integrate-adal"></a>1. App is niet geïntegreerd met ADAL
ADAL-metagegevens **mogen niet** aanwezig zijn in het manifest.

#### <a name="2-app-integrates-adal"></a>2. App is geïntegreerd met ADAL

|Vereiste ADAL-parameter| Waarde |
|--|--|
| ClientID | De ClientID van de app (gegenereerd door Azure AD toen de app is geregistreerd) |

Waar nodig kan een autoriteit worden opgegeven.

U moet uw app bij Azure AD registreren en uw app toegang geven tot de beveiligingsbeleidsservice voor apps:
* Kijk [hier](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications) voor informatie over het registreren van toepassingen met Azure AD.
* Zorg ervoor dat de stappen om uw Android-app te machtigen voor het app-beschermingsbeleid (APP) zijn gevolgd. Gebruik de instructies in de handleiding [Aan de slag met de Intune-SDK](https://docs.microsoft.com/intune/app-sdk-get-started#next-steps-after-integration) onder 'Uw app toegang geven tot de Intune-app-beveiliging (optioneel)'. 

Bekijk hieronder ook de vereisten voor [Voorwaardelijke toegang](#conditional-access).


#### <a name="3-app-integrates-adal-but-does-not-support-brokered-authenticationdevice-wide-sso"></a>3. App integreert ADAL, maar biedt geen ondersteuning voor brokered verificatie/apparaatbrede eenmalige aanmelding

|Vereiste ADAL-parameter| Waarde |
|--|--|
| ClientID | De ClientID van de app (gegenereerd door Azure AD toen de app is geregistreerd) |
| SkipBroker | **True** |

Autoriteit en NonBrokerRedirectURI kunnen indien gewenst worden opgegeven.


### <a name="conditional-access"></a>Voorwaardelijke toegang
Voorwaardelijke toegang (CA) is een [functie](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer) van Azure Active Directory die kan worden gebruikt om toegang tot AAD-resources te beheren. [Intune-beheerders kunnen CA-regels definiëren](https://docs.microsoft.com/intune/conditional-access) waardoor toegang tot resources is beperkt tot apparaten of apps die worden beheerd door Intune. Als u ervoor wilt zorgen dat uw app waar nodig toegang heeft tot resources, moet u de onderstaande stappen volgen. Als uw app geen AAD-toegangstokens ophaalt, of alleen toegang heeft tot resources die niet door CA kunnen worden beveiligd, kunt u deze stappen overslaan.

1. Volg [de richtlijnen voor ADAL-integratie](https://github.com/AzureAD/azure-activedirectory-library-for-android#how-to-use-this-library). 
   Bekijk met name stap 11 voor brokergebruik.
2. [Registreer uw toepassing met Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration). 
   U vindt de omleidings-URI hierboven in de richtlijnen voor ADAL-integratie.
3. Stel de metagegevensparameters voor het manifest in volgens de [algemene ADAL-configuraties](#common-adal-configurations), item 2, hierboven.
4. Controleer of alles goed is geconfigureerd door [op apparaat gebaseerde CA](https://docs.microsoft.com/intune/conditional-access-intune-common-ways-use) in te schakelen vanuit [Azure Portal](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExchangeConnectorMenu/aad/connectorType/2) en bevestig:
    - Dat er bij aanmelding bij uw app wordt gevraagd naar installatie en inschrijving van de Intune-bedrijfsportal
    - Dat na inschrijving goed wordt aangemeld bij uw app.
5. Nadat uw app Intune APP SDK-integratie heeft verzonden, neemt u contact op met msintuneappsdk@microsoft.com om aan de lijst met goedgekeurde apps te worden toegevoegd voor [voorwaardelijke toegang op basis van een app](https://docs.microsoft.com/intune/conditional-access-intune-common-ways-use#app-based-conditional-access)
6. Zodra uw app is toegevoegd aan de goedgekeurde lijst, voert u een validatie uit door [op apps gebaseerde CA te configureren](https://docs.microsoft.com/intune/app-based-conditional-access-intune-create) en te controleren of u zich bij uw app kunt aanmelden.

## <a name="app-protection-policy-without-device-enrollment"></a>App-beveiligingsbeleid zonder apparaatinschrijving

### <a name="overview"></a>Overzicht
Met Intune-beveiligingsbeleid voor apps zonder apparaatregistratie, ook wel PP-WE of MAM-WE genoemd, kunnen apps worden beheerd door Intune zonder dat het apparaat hoeft te worden ingeschreven voor Intune MDM. APP-WE werkt met of zonder apparaatregistratie. De bedrijfsportal moet nog altijd op het apparaat worden geïnstalleerd, maar de gebruiker hoeft zich niet aan te melden bij de bedrijfsportal en hoeft het apparaat niet te registreren.

> [!NOTE]
> Alle apps moeten app-beveiligingsbeleid ondersteunen zonder apparaatregistratie.

### <a name="workflow"></a>Werkstroom

Wanneer er een nieuwe gebruikersaccount met een app wordt gemaakt, moet het account voor beheer worden geregistreerd bij de SDK voor de Intune-app. De SDK verwerkt de details met betrekking tot de registratie van de app bij de APP-WE-service. Indien nodig worden mislukte registraties na een toepasselijke tijdsinterval opnieuw uitgevoerd.

De app kan ook de status van een geregistreerde gebruiker via de SDK voor de Intune-app opvragen om te bepalen of de toegang van de gebruiker tot de bedrijfsinhoud moet worden geblokkeerd. Er kunnen meerdere accounts worden geregistreerd voor beheer, maar momenteel kan er slechts één account tegelijkertijd actief worden geregistreerd bij de APP-WE-service. Dit betekent dat het app-beveiligingsbeleid slechts door één account op de app tegelijkertijd kan worden ontvangen.

De app is vereist voor het opgeven van een callback om namens de SDK het juiste toegangstoken te verkrijgen van de Azure Active Directory Authentication Library (ADAL). Er wordt verondersteld dat de app al gebruikmaakt van ADAL om gebruikers te verifiëren en om de eigen toegangstokens te verkrijgen.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.

Wanneer de app een account volledig verwijdert, moet de registratie van dat account door de app ongedaan worden gemaakt om aan te geven dat de app geen beleid meer moet toepassen voor de betreffende gebruiker. Als de gebruiker is geregistreerd in de MAM-service, wordt de registratie van de gebruiker ongedaan gemaakt en wordt de app gewist.


### <a name="overview-of-app-requirements"></a>Een overzicht van de app-vereisten

Als u APP-WE-integratie wilt implementeren, moet uw app het gebruikersaccount registreren bij de MAM SDK:

1. De app _moet_ een instantie van de `MAMServiceAuthenticationCallback`-interface implementeren en registreren. De callbackinstantie moet zo vroeg mogelijk worden geregistreerd in de levenscyclus van de app (doorgaans in de methode `onMAMCreate()` van de toepassingsklasse).

2. Wanneer er een gebruikersaccount is gemaakt en de gebruiker zich heeft aangemeld bij ADAL, _moet_ de app `registerAccountForMAM()` aanroepen.

3. Wanneer een gebruikersaccount wordt verwijderd, moet de app `unregisterAccountForMAM()` aanroepen om het account te verwijderen uit het Intune-beheerprogramma.

    > [!NOTE]
    > Als een gebruiker zich tijdelijk bij d app afmeldt, hoeft de app `unregisterAccountForMAM()` niet aan te roepen. De aanroep kan een wisbewerking initiëren waarmee de bedrijfsgegevens voor de gebruiker volledig worden gewist.


### <a name="mamenrollmentmanager"></a>MAMEnrollmentManager

Alle benodigde verificatie- en registratie-API's vindt u in de `MAMEnrollmentManager`-interface. Een verwijzing naar de `MAMEnrollmentManager` kunt u als volgt verkrijgen:

```java
MAMEnrollmentManager mgr = MAMComponents.get(MAMEnrollmentManager.class);

// make use of mgr
```

De geretourneerde `MAMEnrollmentManager`-instantie is gegarandeerd niet null. De API-methoden worden onderverdeeld in twee categorieën: **verificatie** en **accountregistratie**.

```java
package com.microsoft.intune.mam.policy;

public interface MAMEnrollmentManager {
    public enum Result {
        AUTHORIZATION_NEEDED,
        NOT_LICENSED,
        ENROLLMENT_SUCCEEDED,
        ENROLLMENT_FAILED,
        WRONG_USER,
        MDM_ENROLLED,
        UNENROLLMENT_SUCCEEDED,
        UNENROLLMENT_FAILED,
        PENDING,
        COMPANY_PORTAL_REQUIRED;
    }

    //Authentication methods
    interface MAMServiceAuthenticationCallback {
        String acquireToken(String upn, String aadId, String resourceId);
    }
    void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
    void updateToken(String upn, String aadId, String resourceId, String token);

    //Registration methods
    void registerAccountForMAM(String upn, String aadId, String tenantId);
    void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
    void unregisterAccountForMAM(String upn);
    Result getRegisteredAccountStatus(String upn);
}
```

### <a name="account-authentication"></a>Accountverificatie

In deze sectie worden de verificatie-API-methoden in `MAMEnrollmentManager` beschreven en hoe ze gebruikt.

```java
interface MAMServiceAuthenticationCallback {
    String acquireToken(String upn, String aadId, String resourceId);
}
void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
void updateToken(String upn, String aadId, String resourceId, String token);
```

1. De app moet de `MAMServiceAuthenticationCallback`-interface implementeren om de SDK toe te staan een ADAL-token voor de opgegeven gebruiker en resource-id aan te vragen. De callbackinstantie moet worden opgegeven voor de `MAMEnrollmentManager` door de bijbehorende `registerAuthenticationCallback()`-methode aan te roepen. Er is mogelijk al vroeg in de levenscyclus van de app een token nodig voor nieuwe registratiepogingen of check-ins voor het vernieuwen van het app-beveiligingsbeleid. De ideale plaats om de callback te registreren, is in de methode `onMAMCreate()` van de subklasse `MAMApplication` van de app.

  > [!NOTE]
  > Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.

2. Met de `acquireToken()`-methode moet het toegangstoken worden gekregen voor de aangevraagde resource-id voor de opgegeven gebruiker. Als het aangevraagde token niet kan worden verkregen, moet null worden geretourneerd.

    > [!NOTE]
    > Zorg ervoor dat voor uw app de parameters `resourceId` en `aadId` worden gebruikt die aan `acquireToken()` zijn doorgegeven, zodat het juiste token wordt verkregen.

    ```java
    class MAMAuthCallback implements MAMServiceAuthenticationCallback {
        public String acquireToken(String upn, String aadId, String resourceId) {
            return mAuthContext.acquireTokenSilentSync(resourceId, ClientID, aadId).getAccessToken();
        }
    }
    ```

3. Als de app kan geen token kan verstrekken wanneer de SDK `acquireToken()` aanroept, bijvoorbeeld als de verificatie op de achtergrond is mislukt en het geen geschikt moment is om een gebruikersinterface weer te geven, kan de app op een later tijdstip een token verstrekken door de methode `updateToken()` aan te roepen. Dezelfde UPN, AAD-id en resource-id die zijn aangevraagd door de vorige aanroep naar `acquireToken()`, moeten worden doorgegeven aan `updateToken()`, samen met het token dat uiteindelijk is verkregen. De app moet deze methode zo snel mogelijk aanroepen nadat via de verstrekte callback null is geretourneerd.

    > [!NOTE]
    > De SDK roept `acquireToken()` periodiek aan om het token te verkrijgen. Het is dus niet strikt noodzakelijk om `updateToken()` aan te roepen. Dit wordt echter wel sterk aanbevolen omdat dit kan helpen bij het tijdig voltooien van het inchecken voor de registratie en app-beveiligingsbeleid.


### <a name="account-registration"></a>Accountregistratie

In deze sectie worden de accountregistratie-API-methoden in `MAMEnrollmentManager` beschreven en hoe ze gebruikt.

```java
void registerAccountForMAM(String upn, String aadId, String tenantId);
void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
void unregisterAccountForMAM(String upn);
Result getRegisteredAccountStatus(String upn);
```

1. Als u een account wilt registreren voor beheer, moet de app `registerAccountForMAM()` aanroepen. Een gebruikersaccount wordt geïdentificeerd aan de hand van de bijbehorende UPN en de AAD-gebruikers-id. De tenant-id is ook vereist registratiegegevens aan de AAD-tenant van de gebruiker te koppelen. De autoriteit van de gebruiker kan ook worden opgegeven om inschrijving toe te staan bij specifieke onafhankelijk clouds. Zie [Registratie bij onafhankelijke clouds](#sovereign-cloud-registration) voor meer informatie.  De SDK probeert de app voor de betreffende gebruiker mogelijk te registreren in de MAM-service. Als de registratie mislukt, zal de registratie periodiek opnieuw worden uitgevoerd totdat de registratie van het account ongedaan is gemaakt. U kunt het doorgaans na 12 tot 24 uur opnieuw proberen. De SDK verstrekt op asynchrone wijze informatie over de status van registratiepogingen via meldingen.

2. Omdat de AAD-verificatie is vereist, kan het gebruikersaccount het beste worden geregistreerd nadat de gebruiker is aangemeld bij de app en is geverifieerd met behulp van de ADAL. De AAD-id en tenant-id van de gebruiker worden als onderdeel van het object [`AuthenticationResult`](https://github.com/AzureAD/azure-activedirectory-library-for-android) geretourneerd via de aanroep voor de ADAL-verificatie.
    * De tenant-id is afkomstig uit de `AuthenticationResult.getTenantID()`-methode.
    * Informatie over de gebruiker vindt u een subobject van het type `UserInfo` die afkomstig is van `AuthenticationResult.getUserInfo()`, en de AAD-gebruikers-id die wordt opgehaald via dat object door `UserInfo.getUserId()` aan te roepen.

  > [!NOTE]
  > Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.

3. Als u de registratie van een account bij Intune-beheer ongedaan wilt maken, moet de app `unregisterAccountForMAM()` aanroepen. Als het account is geregistreerd en wordt beheerd, wordt de SDK-registratie van het account ongedaan gemaakt en worden de gegevens gewist. Periodieke registratiepogingen voor het account worden gestopt. De SDK verstrekt op asynchrone wijze via een melding de status van aanvragen om de registratie ongedaan te maken.

### <a name="sovereign-cloud-registration"></a>Registratie bij onafhankelijke clouds

Voor toepassingen die [bewust zijn van onafhankelijke clouds](https://www.microsoft.com/trustcenter/cloudservices/nationalcloud) **moet** de `authority` voor `registerAccountForMAM()` worden opgeven.  U krijgt deze door `instance_aware=true` op te geven in de [1.14.0+](https://github.com/AzureAD/azure-activedirectory-library-for-android/releases/tag/v1.14.0) acquireToken extraQueryParameters van ADAL, gevolgd door het intrekken van `getAuthority()` in het AuthenticationCallback AuthenticationResult.

```java
mAuthContext.acquireToken(this, RESOURCE_ID, CLIENT_ID, REDIRECT_URI, PromptBehavior.FORCE_PROMPT, "instance_aware=true",
        new AuthenticationCallback<AuthenticationResult>() {
            @Override
            public void onError(final Exception exc) {
                // authentication failed
            }

            @Override
            public void onSuccess(final AuthenticationResult result) {
                mAuthority = result.getAuthority();
                // handle other parts of the result
            }
        });
```

> [!NOTE]
> Stel het metagegevensitem `com.microsoft.intune.mam.aad.Authority` in AndroidManifest.xml niet in.

> [!NOTE]
> Zorg ervoor dat de autoriteit goed is ingesteld in uw `MAMServiceAuthenticationCallback::acquireToken()`-methode.

#### <a name="currently-supported-sovereign-clouds"></a>Momenteel ondersteunde onafhankelijke clouds

1. Azure-cloud van de Amerikaanse overheid
2. Microsoft Azure beheerd door 21Vianet (Azure China)


### <a name="important-implementation-notes"></a>Belangrijke opmerkingen voor de implementatie

#### <a name="authentication"></a>Verificatie

* Wanneer de app `registerAccountForMAM()` aanroept, wordt er mogelijk kort daarna, op een andere thread, een callback ontvangen op de `MAMServiceAuthenticationCallback`-interface. In het ideale geval heeft de app voorafgaand aan de registratie van het account zijn eigen token uit ADAL verkregen om het ophalen van het aangevraagde token te versnellen. Als de app een geldige token retourneert uit de callback, wordt de registratie voortgezet en ontvangt de app het uiteindelijke resultaat via een melding.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.

* Als de app geen geldig AAD-token retourneert, is het uiteindelijke resultaat van de registratiepoging `AUTHORIZATION_NEEDED`. Als de app dit resultaat ontvangt via een melding, wordt ten zeerste aangeraden om het registratieproces te versnellen door het token voor de gebruiker en de resource die eerder zijn aangevraagd, op te halen bij `acquireToken()` en de methode `updateToken()` aan te roepen om het registratieproces opnieuw te initiëren.

* De geregistreerde `MAMServiceAuthenticationCallback` van de app wordt ook aangeroepen om een token te verkrijgen voor check-ins voor het periodiek vernieuwen van het app-beveiligingsbeleid. Als de app geen token kan verstrekken wanneer dit wordt aangevraagd, wordt er geen melding ontvangen, maar moet de app proberen een token te verkrijgen en op he volgende geschikte tijdstip `updateToken()` aanroepen om het check-inproces te versnellen. Als een token niet is opgegeven, wordt de callback bij de volgende check-inpoging gewoon aangeroepen.

* Voor ondersteuning voor onafhankelijke clouds moet de autoriteit worden opgegeven.

#### <a name="registration"></a>Registratie

* Voor uw gemak zijnde registratiemethoden idempotent. `registerAccountForMAM()` zal bijvoorbeeld een account alleen registreren en een app alleen proberen te registreren als het account nog niet is geregistreerd, en `unregisterAccountForMAM()` maakt de registratie van een account alleen ongedaan als het account moment is geregistreerd. Alle volgende aanroepen zijn 'no-ops', zodat deze methoden zonder problemen meerdere keren kunnen worden aangeroepen. Daarnaast kan de correspondentie tussen aanroepen naar deze methoden en meldingen van de resultaten niet worden gegarandeerd: oftewel, als `registerAccountForMAM()` wordt aangeroepen voor een identiteit die al is geregistreerd, de melding mogelijk niet opnieuw wordt verzonden voor die identiteit. Het is mogelijk dat er meldingen worden verzonden die niet overeenkomen met de aanroepen voor deze methoden, aangezien de SDK mogelijk periodiek registratie op de achtergrond uitvoert en er registraties ongedaan kunnen worden gemaakt op basis van wisverzoeken die van de Intune-service zijn ontvangen.

* De registratiemethoden kunnen worden aangeroepen voor elk aantal verschillende identiteiten, maar momenteel kan er slechts één gebruikersaccount worden geregistreerd. Als er op hetzelfde of vrijwel hetzelfde moment meerdere gebruikersaccounts met een licentie voor Intune en app-beveiligingsbeleid worden geregistreerd, kan niet worden gegarandeerd welk account de race wint.

* Tot slot kunt gegevens bij `MAMEnrollmentManager` opvragen om te zien of een bepaald account is geregistreerd en om de huidige status op te halen met de methode `getRegisteredAccountStatus()`. Als het opgegeven account niet is geregistreerd, resulteert deze methode **null**. Als het account is geregistreerd, retourneert deze methode de status van het account als een van de leden van de `MAMEnrollmentManager.Result`-opsomming.

### <a name="result-and-status-codes"></a>Resultaat en statuscodes

Als een account voor het eerst wordt geregistreerd, krijgt het account eerst de status `PENDING`, waarmee wordt aangegeven dat de eerste registratie van de MAM-service nog niet is voltooid. Nadat de registratiepoging is voltooid, wordt er een melding met een van de resultaatcodes in de onderstaande tabel verzonden. Daarnaast retourneert de methode `getRegisteredAccountStatus()` de status van het account, zodat de app altijd kan bepalen of de toegang tot de bedrijfsinhoud voor die gebruiker is geblokkeerd. Als de registratiepoging mislukt, kan de status van het account na verloop van tijd worden gewijzigd, aangezien er op de achtergrond nieuwe registratiepogingen door de SDK worden uitgevoerd.

|Resultaatcode | Uitleg |
| -- | -- |
| `AUTHORIZATION_NEEDED` | Dit resultaat geeft aan dat er geen token is verstrekt door de geregistreerde `MAMServiceAuthenticationCallback`-instantie van de app of dat het token ongeldig is.  De app moet een geldig token ophalen en indien mogelijk `updateToken()` aanroepen. |
| `NOT_LICENSED` | De gebruiker heeft geen licentie voor Intune of er kan geen contact met de Intune MAM-service worden opgenomen.  De onbeheerde (normale) status van de app moet blijven gehandhaafd en de gebruiker moet worden geblokkeerd.  Er worden periodiek nieuwe registratiepogingen uitgevoerd voor het geval de gebruiker in de toekomst alsnog een licentie wordt verleend. |
| `ENROLLMENT_SUCCEEDED` | De registratie is geslaagd of de gebruiker is al geregistreerd.  In het geval van een geslaagde registratie wordt er vóór deze melding een melding voor beleidsvernieuwing verzonden.  Toegang tot bedrijfsgegevens moet worden toegestaan. |
| `ENROLLMENT_FAILED` | De registratie is mislukt.  Meer informatie vindt u in de logboeken van het apparaat.  De app moet in deze status geen toegang tot de bedrijfsgegevens verlenen, omdat eerder is vastgesteld dat de gebruiker een licentie heeft voor Intune.|
| `WRONG_USER` | Slechts één gebruiker per apparaat kan een app met de MAM-service registreren. Dit resultaat geeft aan dat de gebruiker voor wie dit resultaat is geleverd (de tweede gebruiker) is gericht op MAM-beleid, maar dat er al een andere gebruiker is ingeschreven. Het MAM-beleid kan niet worden afgedwongen voor de tweede gebruiker. Uw app mag geen toegang tot de gegevens van deze gebruiker toestaan (mogelijk door de gebruiker uit uw app te verwijderen) tenzij/totdat de registratie van deze gebruiker op een later tijdstip slaagt. Tegelijk met het leveren van dit `WRONG_USER`-resultaat, geeft MAM de optie om het bestaande account te verwijderen. Als de gebruiker bevestigend antwoordt, is het inderdaad mogelijk om de tweede gebruiker korte tijd later te registreren. Zolang de tweede gebruiker geregistreerd blijft, probeert MAM de registratie regelmatig opnieuw. |
| `UNENROLLMENT_SUCCEEDED` | De registratie is ongedaan gemaakt.|
| `UNENROLLMENT_FAILED` | Het ongedaan maken van de registratie is mislukt.  Meer informatie vindt u in de logboeken van het apparaat. In het algemeen gebeurt dit niet zolang de app een geldige UPN (niet null en niet leeg) doorgeeft. Er is geen directe, betrouwbare herstelactie die de app kan uitvoeren. Als deze waarde wordt ontvangen bij het ongedaan maken van de registratie van een geldige UPN, meldt u dit als een bug bij het Intune MAM-team.|
| `PENDING` | De eerste registratiepoging voor de gebruiker wordt uitgevoerd.  De app kan de toegang tot de bedrijfsgegevens blokkeren totdat het resultaat van de registratie bekend is. Dit is echter geen vereiste. |
| `COMPANY_PORTAL_REQUIRED` | De gebruiker heeft een licentie voor Intune, maar de app kan pas worden geregistreerd nadat de bedrijfsportal-app is geïnstalleerd op het apparaat. De SDK voor de Intune-app probeert de toegang tot de app te blokkeren voor de opgegeven gebruiker en instrueert de gebruiker om de bedrijfsportal-app te installeren(zie hieronder voor meer informatie). |


### <a name="company-portal-requirement-prompt-override-optional"></a>Vereisteprompt voor de bedrijfsportal negeren (optioneel)

Als het resultaat `COMPANY_PORTAL_REQUIRED` wordt ontvangen, blokkeert de SDK het gebruik van activiteiten die gebruikmaken van de identiteit waarvoor de registratie is aangevraagd. In plaats daarvan zorgt de SDK ervoor dat er een prompt wordt weergegeven om de bedrijfsportal te downloaden. Als u dit gedrag in uw app wilt voorkomen, kunnen de activiteiten `MAMActivity.onMAMCompanyPortalRequired` implementeren.

Deze methode wordt aangeroepen voordat de SDK de standaardblokkerings-UI weergeeft. Als de app de identiteit van de activiteit wijzigt of de registratie ongedaan maakt van de gebruiker die registratiepoging heeft uitgevoerd, wordt de activiteit niet door de SDK geblokkeerd. In deze situatie is het aan de app om te voorkomen dat er bedrijfsgegevens worden gelekt. Alleen apps met meerdere identiteiten (dit bespreken we later) kunnen de activiteitsidentiteit wijzigen.

Als u `MAMActivity` niet expliciet overneemt (omdat die wijziging wordt aangebracht met een build-hulpprogramma), maar deze melding nog steeds moet afhandelen, kunt u in plaats daarvan `MAMActivityBlockingListener` implementeren.

### <a name="notifications"></a>Meldingen

Als de app wordt geregistreerd voor meldingen van het type **MAM_ENROLLMENT_RESULT**, wordt een `MAMEnrollmentNotification` verzonden om de app ervan op de hoogte te brengen dat de aanvraag is voltooid. De `MAMEnrollmentNotification` worden ontvangen via de `MAMNotificationReceiver` interface zoals beschreven in de sectie [Registreren voor meldingen van de SDK](#register-for-notifications-from-the-sdk).

```java
public interface MAMEnrollmentNotification extends MAMUserNotification {
    MAMEnrollmentManager.Result getEnrollmentResult();
}
```

De methode `getEnrollmentResult()` retourneert het resultaat van het registratieverzoek.  Aangezien `MAMEnrollmentNotification``MAMUserNotification` uitbreidt, is ook de identiteit van de gebruiker beschikbaar voor wie de registratiepoging is uitgevoerd. De app moet de `MAMNotificationReceiver`-interface implementeren om deze meldingen te ontvangen, zoals uiteengezet in de sectie [Registreren voor meldingen van de SDK](#register-for-notifications-from-the-sdk).

De status van een geregistreerd gebruikersaccount kan worden gewijzigd wanneer een registratiemelding wordt ontvangen, maar de status zal niet in alle gevallen worden gewijzigd. Als de melding `AUTHORIZATION_NEEDED` wordt ontvangen na een meer informatief resultaat als `WRONG_USER`, wordt het meer informatieve resultaat bijvoorbeeld gehandhaafd als de status van het account.  Zodra het account is ingeschreven, blijft de status `ENROLLMENT_SUCCEEDED` totdat het account wordt uitgeschreven of gewist.


## <a name="app-ca-with-policy-assurance"></a>Voorwaardelijke toegang tot apps (APP CA) met beleidsverzekering

### <a name="overview"></a>Overzicht
Met voorwaardelijke toegang tot apps met beleidsverzekering, gelden de voorwaarden van het Intune-app-beveiligingsbeleid voor toegang tot resources vanuit de app.  Dit wordt door AAD afgedwongen omdat de app moet worden ingeschreven bij en beheerd door APP voordat u een token toegang kunt verlenen tot een resource die door een APP CA met beleidsverzekering wordt beschermd.  Voor de app moet de ADAL-broker worden gebruikt om een token te verkrijgen. De installatie is hetzelfde als die hierboven wordt beschreven bij [Voorwaardelijke toegang](#conditional-access).

### <a name="adal-changes"></a>ADAL-wijzigingen
De ADAL-bibliotheek heeft een nieuwe foutcode om de app te informeren dat het niet kunnen verkrijgen van een token is veroorzaakt doordat het APP-beheer niet werd nageleefd.  Als deze foutcode in de app wordt ontvangen, moet de SDK worden aangeroepen om naleving proberen te herstellen door de app in te schrijven en beleid toe te passen. De `onError()`-methode ontvangt een uitzondering van de ADAL-`AuthenticationCallback`. Deze uitzondering heeft foutcode `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED`.  In dit geval kan de uitzondering worden geconverteerd naar een `IntuneAppProtectionPolicyRequiredException`, van waaruit aanvullende parameters kunnen worden geëxtraheerd die voor het herstellen van de naleving kunnen worden gebruikt (zie het onderstaande codevoorbeeld). Zodra de naleving is hersteld, kan opnieuw worden geprobeerd om vanuit de app het token te verkrijgen via ADAL.

> [!NOTE]
> Voor deze nieuwe foutcode en andere ondersteuning voor APP CA met beleidsverzekering is versie 1.15.0 (of hoger) van de ADAL-bibliotheek vereist.

> [!NOTE]
> Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.

### <a name="mamcompliancemanager"></a>MAMComplianceManager

De `MAMComplianceManager`-interface wordt gebruikt wanneer er een door beleid vereiste fout van ADAL wordt ontvangen.  Deze bevat de `remediateCompliance()`-methode die moet worden aangeroepen om de app in een compatibele status te plaatsen. Een verwijzing naar de `MAMComplianceManager` kunt u als volgt verkrijgen:

```java
MAMComplianceManager mgr = MAMComponents.get(MAMComplianceManager.class);

// make use of mgr
```

De geretourneerde `MAMComplianceManager`-instantie is gegarandeerd niet null.

```java
package com.microsoft.intune.mam.policy;

public interface MAMComplianceManager {
    void remediateCompliance(String upn, String aadId, String tenantId, String authority, boolean showUX);
}
```

De `remediateCompliance()`-methode wordt aangeroepen om de app onder beheer te plaatsen zodat er wordt voldaan aan de voorwaarden om het aangevraagde token door AAD te laten toekennen.  De eerste vier parameters kunnen worden geëxtraheerd uit de uitzondering die u via de `AuthenticationCallback.onError()`-methode van ADAL hebt ontvangen (zie het onderstaande codevoorbeeld).  De laatste parameter is een Booleaanse waarde waarmee u kunt bepalen of een UX tijdens de nalevingspoging wordt weergegeven.  Dit is een eenvoudige interface zoals wanneer voortgang wordt geblokkeerd, die standaard wordt aangeboden voor apps waarvoor tijdens deze bewerking geen aangepaste UX hoeft te worden weergegeven.  De blokkering wordt alleen toegepast zolang het nalevingsherstel nog wordt uitgevoerd. Het uiteindelijke resultaat zal niet worden weergegeven.  Voor de app moet een meldingsontvanger worden geregistreerd voor de verwerking van een geslaagde of mislukte nalevingsherstelpoging (zie hieronder).

Mogelijk wordt een MAM-inschrijving door de `remediateCompliance()`-methode uitgevoerd als onderdeel van het tot stand brengen van naleving.  Mogelijk ontvangt de app een inschrijvingsmelding als er voor de app een meldingsontvanger voor inschrijvingsmeldingen is geregistreerd.  Van de geregistreerde `MAMServiceAuthenticationCallback` van de app wordt de `acquireToken()`-methode aangeroepen om een token voor de MAM-inschrijving op te halen. `acquireToken()` wordt aangeroepen voordat de app het eigen token heeft verkregen, dus alle administratieve taken of taken voor het maken van accounts die worden uitgevoerd nadat de app het token heeft verkregen, zijn mogelijk nog niet uitgevoerd.  De callback moet een token in dit geval kunnen verkrijgen.  Als u geen token van `acquireToken()` kunt retourneren, mislukt de nalevingsherstelpoging.  Als u `updateToken()` later aanroept met een geldig token voor de aangevraagde resource, wordt het nalevingsherstel onmiddellijk opnieuw geprobeerd met de het opgegeven token.

> [!NOTE]
> In `acquireToken()` kunnen tokens nog wel op de achtergrond worden opgehaald, omdat de gebruiker al is geïnstrueerd om de broker te installeren en het apparaat te registreren voordat de fout `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED` is ontvangen.  Hierdoor krijgt de broker een geldig vernieuwingstoken in de cache, waardoor het aangevraagde token op de achtergrond kan worden opgehaald.

Hier ziet u een voorbeeld van een door beleid vereiste fout die wordt ontvangen via de `AuthenticationCallback.onError()`-methode en de `MAMComplianceManager` die wordt aangeroepen om de fout te verwerken.

```java
public void onError(@Nullable Exception exc) {
    if (exc instanceof AuthenticationException && 
        ((AuthenticationException) exc).getCode() == ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED) {

        final IntuneAppProtectionPolicyRequiredException policyRequiredException = 
            (IntuneAppProtectionPolicyRequiredException) ex;

        final String upn = policyRequiredException.getAccountUpn();
        final String aadId = policyRequiredException.getAccountUserId();
        final String tenantId = policyRequiredException.getTenantId();
        final String authority = policyRequiredException.getAuthorityURL();

        MAMComplianceManager complianceManager = MAMComponents.get(MAMComplianceManager.class);
        complianceManager.remediateCompliance(upn, aadId, tenantId, authority, showUX);
    }
}
```

### <a name="status-notifications"></a>Statusmeldingen

Als de app wordt geregistreerd voor meldingen van het type **COMPLIANCE_STATUS**, wordt `MAMComplianceNotification` verzonden om de app op de hoogte te brengen van de uiteindelijke status van de nalevingsherstelpoging. De `MAMComplianceNotification` worden ontvangen via de `MAMNotificationReceiver` interface zoals beschreven in de sectie [Registreren voor meldingen van de SDK](#register-for-notifications-from-the-sdk).

```java
public interface MAMComplianceNotification extends MAMUserNotification {
    MAMCAComplianceStatus getComplianceStatus();
    String getComplianceErrorTitle();
    String getComplianceErrorMessage();
}
```

De `getComplianceStatus()`-methode retourneert het resultaat van de nalevingsherstelpoging als een waarde van de `MAMCAComplianceStatus`-opsomming.

|Statuscode | Uitleg |
| -- | -- |
| UNKNOWN | De status is onbekend. Dit kan duiden op een niet-verwachte reden voor de fout. Raadpleeg de logboeken van Bedrijfsportal voor aanvullende informatie. |
| COMPLIANT | Nalevingsherstel is geslaagd en de app voldoet nu aan het beleid. Probeer opnieuw het ADAL-token op te halen. |
| NOT_COMPLIANT | De poging om de naleving te herstellen, is mislukt.  De app voldoet niet en u kunt niet opnieuw proberen het ADAL-token op te halen voordat de foutvoorwaarde is hersteld.  Er worden aanvullende foutgegevens verzonden met MAMComplianceNotification. |
| SERVICE_FAILURE | Er heeft zich een fout voorgedaan bij de poging om nalevingsgegevens van de Intune-service op te halen. Raadpleeg de logboeken van Bedrijfsportal voor aanvullende informatie. |
| NETWORK_FAILURE | Er heeft zich een fout voorgedaan bij het maken van een verbinding met de Intune-service. Probeer opnieuw de token van de app op te halen zodra de netwerkverbinding is hersteld. |
| CLIENT_ERROR | De poging om naleving te herstellen, is mislukt door een oorzaak met betrekking tot de client.  Bijvoorbeeld: er is geen token of een verkeerde gebruiker. Er worden aanvullende foutgegevens verzonden met MAMComplianceNotification. |
| PENDING | De poging om naleving te herstellen, is mislukt omdat het statusantwoord niet van de service is ontvangen toen de tijdslimiet werd overschreden. Probeer later het token van de app opnieuw op te halen. |
| COMPANY_PORTAL_REQUIRED | Voor een geslaagd nalevingsherstel moet Bedrijfsportal op het apparaat zijn geïnstalleerd.  Als Bedrijfsportal al op het apparaat is geïnstalleerd, moet de app opnieuw worden opgestart.  In dit geval wordt een dialoogvenster weergegeven waarin de gebruiker wordt gevraagd de app opnieuw op te starten. |

Als de nalevingsstatus `MAMCAComplianceStatus.COMPLIANT` is, wordt de oorspronkelijke tokenverwerving van de app opnieuw gestart (voor de eigen resource van de app). Als de nalevingsherstelpoging is mislukt, worden door de methoden `getComplianceErrorTitle()` en `getComplianceErrorMessage()` gelokaliseerde tekenreeksen geretourneerd die in de app kunnen worden weergegeven als de eindgebruiker hiervoor kiest.  De meeste fouten kunnen niet door de app worden hersteld, dus over het algemeen kunt u het maken van het account of het aanmelden het beste laten mislukken, zodat gebruikers het later opnieuw kunnen proberen.  Als een fout zich blijft voordoen, kunt u de oorzaak proberen te achterhalen met behulp van de MAM-logboeken.  De eindgebruiker kan de logboeken verzenden aan de hand van de instructies die [hier](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android "Logboeken via e-mail naar het ondersteuningsteam van uw bedrijf verzenden") beschikbaar zijn.

Aangezien met `MAMComplianceNotification` wordt `MAMUserNotification` uitgebreid, is ook de identiteit van de gebruiker beschikbaar voor wie de herstelpoging is uitgevoerd.

Hier ziet u een voorbeeld van de registratie van een ontvanger met behulp van een anonieme klasse om de MAMNotificationReceiver-interface te implementeren:

```java
final MAMNotificationReceiverRegistry notificationRegistry = MAMComponents.get(MAMNotificationReceiverRegistry.class);
// create a receiver
final MAMNotificationReceiver receiver = new MAMNotificationReceiver() {
    public boolean onReceive(MAMNotification notification) {
        if (notification.getType() == MAMNotificationType.COMPLIANCE_STATUS) {
            MAMComplianceNotification complianceNotification = (MAMComplianceNotification) notification;
            
            // take appropriate action based on complianceNotification.getComplianceStatus()
            
            // unregister this receiver if no longer needed
            notificationRegistry.unregisterReceiver(this, MAMNotificationType.COMPLIANCE_STATUS);
        }
        return true;
    }
};
// register the receiver
notificationRegistry.registerReceiver(receiver, MAMNotificationType.COMPLIANCE_STATUS);
```

> [!NOTE]
> De meldingenontvanger moet worden geregistreerd voordat u `remediateCompliance()` aanroept om een racevoorwaarde te voorkomen die ertoe kan leiden dat u de melding mist.

### <a name="implementation-notes"></a>Implementatienotities

> [!NOTE]
> **Belangrijke wijziging!**  <br>
> De methode `MAMServiceAuthenticationCallback.acquireToken()` van de app moet *false* voor de nieuwe `forceRefresh`-vlag doorgeven aan `acquireTokenSilentSync()`.
> Eerder hebben we aangeraden om *true* door te geven om een probleem met het vernieuwen van tokens van de broker aan te pakken.Er is echter een probleem gevonden met ADAL dat kan verhinderen dat in sommige scenario's tokens worden verkregen indien deze vlag *true* is.
```java
AuthenticationResult result = acquireTokenSilentSync(resourceId, clientId, userId, /* forceRefresh */ false);
```

> [!NOTE]
> Als u aangepaste blokkerende UX wilt weergeven tijdens de herstelpoging, moet u *false* voor de showUX-parameter doorgeven aan `remediateCompliance()`. U moet ervoor zorgen dat uw UX wordt weergegeven en dat u eerst uw meldingenlistener registreert voordat u `remediateCompliance()` aanroept.  Hierdoor voorkomt u dat er een racevoorwaarde optreedt waarbij de melding mogelijk wordt gemist als `remediateCompliance()` heel snel mislukt.  De methode `onCreate()` of `onMAMCreate()` van de subklasse Activiteit is bijvoorbeeld de ideale locatie om de meldingenlistener te plaatsen en vervolgens `remediateCompliance()` aan te roepen.  De parameters voor `remediateCompliance()` kunnen aan uw UX worden doorgegeven als extra intenties.  Zodra de melding over de nalevingsstatus is ontvangen, kunt u het resultaat weergeven of de activiteit simpelweg voltooien.

> [!NOTE]
> Het account wordt door `remediateCompliance()` geregistreerd en er wordt een inschrijvingspoging ondernomen.  Zodra het hoofdtoken is verkregen, is het niet nodig om `registerAccountForMAM()` aan te roepen. Dit kan echter geen kwaad. Anderzijds, als het token niet kan worden opgehaald en het gebruikersaccount moet worden verwijderd, moet `unregisterAccountForMAM()` via de app worden aangeroepen om het account te verwijderen en om te voorkomen dat op de achtergrond opnieuw wordt geprobeerd de app in te schrijven.

## <a name="protecting-backup-data"></a>Beveiligen van back-upgegevens

Vanaf Android Marshmallow (API 23) biedt Android apps twee manieren om een back-up van gegevens te maken. Elke optie is beschikbaar voor uw app en vereist andere stappen om ervoor te zorgen dat Intune-gegevensbeveiliging correct worden geïmplementeerd. U kunt de onderstaande tabel gebruiken voor een overzicht van de bijbehorende acties die zijn vereist voor een correct gegevensbeveiligingsgedrag.  In de [Android-API-handleiding](https://developer.android.com/guide/topics/data/backup.html) vindt u meer informatie over de back-upmethoden.

### <a name="auto-backup-for-apps"></a>Automatische back-ups voor apps

Android begon met het aanbieden van [automatische volledige back-ups](https://developer.android.com/guide/topics/data/autobackup.html) naar Google Drive for apps op Android Marshmallow-apparaten, ongeacht de doel-API van de app. Als u in uw AndroidManifest.xml `android:allowBackup` expliciet hebt ingesteld op **onwaar**, wordt uw app door Android nooit opgenomen in de wachtrij voor back-ups en blijven de bedrijfsgegevens in de app. In dit geval is er geen verdere actie nodig.

Het kenmerk `android:allowBackup` is echter standaard ingesteld op waar, zelfs als `android:allowBackup` niet in het manifestbestand is opgegeven. Dit betekent dat van alle app-gegevens automatisch een back-up in het Google Drive-account van de gebruiker wordt gemaakt. Deze standaardwerking vormt een **risico op het lekken van gegevens**. Daarom vereist de SDK de wijzigingen die hieronder worden beschreven om ervoor te zorgen dat gegevensbescherming wordt toegepast.  Het is belangrijk dat u de onderstaande richtlijnen voor het beveiligen van klantgegevens volgt als u uw app op Android Marshmallow-apparaten wilt uitvoeren.  

U kunt met Intune alle [functies voor automatische back-ups](https://developer.android.com/guide/topics/data/autobackup.html) gebruiken die door Android beschikbaar worden gesteld, inclusief de mogelijkheid om aangepaste regels in XML te definiëren, maar u moet de volgende stappen uitvoeren om uw gegevens te beveiligen:

1. Als uw app **geen** eigen aangepaste BackupAgent gebruikt, gebruikt u de standaard-MAMBackupAgent voor automatische volledige back-ups die aan het Intune-beleid voldoen. Plaats het volgende in het app-manifest:

    ```xml
    android:fullBackupOnly="true"
    android:backupAgent="com.microsoft.intune.mam.client.app.backup.MAMDefaultBackupAgent"
    ```
    
2. **[Optioneel]**  Als u een optionele aangepaste BackupAgent hebt geïmplementeerd, moet u ervoor zorgen dat MAMBackupAgent of MAMBackupAgentHelper gebruikt. Zie de volgende secties. Overweeg over te schakelen naar het gebruik van de **MAMDefaultFullBackupAgent** van Intune (zoals beschreven in stap 1). Hiermee kunt u eenvoudig back-ups maken op Android M en later.

3. Als u beslist welk type volledige back-up uw app moet ontvangen (niet gefilterd, gefilterd of geen), moet u het kenmerk `android:fullBackupContent` instellen op waar, onwaar of een XML-bron in uw app.

4. Vervolgens _**moet**_ alles wat u in `android:fullBackupContent` plaatst, kopiëren naar het manifest, naar een metagegevenscode met naam `com.microsoft.intune.mam.FullBackupContent`.

    **Voorbeeld 1**: Als u wilt dat er volledige back-ups zonder uitsluitingen van uw app worden gemaakt, stelt u zowel het kenmerk `android:fullBackupContent` als de metagegevenscode `com.microsoft.intune.mam.FullBackupContent` in op **true** (waar):

    ```xml
    android:fullBackupContent="true"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="true" />  
    ```

    **Voorbeeld 2**: Als u wilt dat uw app gebruikmaakt van de aangepaste BackupAgent en moet worden afgemeld voor volledige automatische back-ups die voldoen aan het Intune-beleid, moet u het kenmerk en de metagegevenscode instellen op **false** (onwaar):

    ```xml
    android:fullBackupContent="false"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="false" />  
    ```

    **Voorbeeld 3**: als u wilt dat er volledige back-ups van uw app worden gemaakt volgens de aangepaste regels die in een XML-bestand zijn gedefinieerd, stelt u het kenmerk en de metagegevenscode in op dezelfde XML-bron:

    ```xml
    android:fullBackupContent="@xml/my_scheme"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:resource="@xml/my_scheme" />  
    ```


### <a name="keyvalue-backup"></a>Key/Value-back-up

De optie [Key/Value-back-up](https://developer.android.com/guide/topics/data/keyvaluebackup.html) is beschikbaar voor alle API's 8+ en uploadt de app-gegevens naar de [Android Backup Service](https://developer.android.com/google/backup/index.html). De hoeveelheid gegevens per gebruiker van uw app is beperkt tot 5 MB. Als u Key/Value-back-up gebruikt, moet u een **BackupAgentHelper** of een **BackupAgent** gebruiken.

### <a name="backupagenthelper"></a>BackupAgentHelper

BackupAgentHelper is eenvoudiger te implementeren dan BackupAgent, zowel op het gebied van systeemeigen Android-functionaliteit als Intune MAM-integratie. Met BackupAgentHelper kan de ontwikkelaar volledige bestanden en gedeelde voorkeuren registreren bij respectievelijk een **FileBackupHelper** en **SharedPreferencesBackupHelper**, die vervolgens worden toegevoegd aan de BackupAgentHelper wanneer deze wordt gemaakt. Volg de onderstaande stappen om een BackupAgentHelper met Intune MAM te gebruiken:

1. Als u back-ups van meerdere identiteiten wilt maken met een BackupAgentHelper, volgt u de Android-richtlijn voor [het uitbreiden van BackupAgentHelper](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgentHelper).

2. Laat uw klasse de MAM-equivalent van BackupAgentHelper, FileBackupHelper en SharedPreferencesBackupHelper uitbreiden.

|Android-klasse | MAM-equivalent |
|--|--|
|BackupAgentHelper |MAMBackupAgentHelper |
|FileBackupHelper | MAMFileBackupHelper
|SharedPreferencesBackupHelper| MAMSharedPreferencesBackupHelper|

Als u deze richtlijnen volgt, kunt back-ups meerdere identiteiten maken en deze herstellen.

### <a name="backupagent"></a>BackupAgent

Met een BackupAgent kunt u veel explicieter aangeven van welke gegevens een back-up wordt gemaakt. Omdat de ontwikkelaar redelijk verantwoordelijk is voor de implementatie, zijn er meer stappen vereist om te zorgen voor de juiste mate van gegevensbeveiliging van Intune. Omdat het meeste werk naar u, de ontwikkelaar, wordt doorgeschoven, is de Intune-integratie iets bewerkelijker.

**MAM integreren:**

1. Lees de Android-handleiding [Key/Value Backup](https://developer.android.com/guide/topics/data/keyvaluebackup.html) en met name de sectie [Extending BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) aandachtig door om ervoor te zorgen dat uw implementatie van BackupAgent de Android-richtlijnen volgt.

2. Laat uw klasse `MAMBackupAgent` uitbreiden.

**Back-up maken van meerdere identiteiten:**

1. Voordat u een back-up start, controleert u of **de IT-beheerder u toestaat** een back-up van de gewenste bestanden of gegevensbuffers te maken in scenario's met meerdere identiteiten. U beschikt over de functie `isBackupAllowed` in `MAMFileProtectionManager` en `MAMDataProtectionManager` om dit te bepalen. Als er geen back-up van het bestand of de gegevensbuffer mag worden gemaakt, moet u deze te blijven opnemen in uw back-up.

2. Op een bepaald moment moet u tijdens de back-up, als u een back-up wilt maken van de identiteit voor de bestanden die u in stap 1 hebt gecontroleerd, `backupMAMFileIdentity(BackupDataOutput data, File … files)` aanroepen met de bestanden waaruit u gegevens wilt extraheren. Hierdoor worden automatisch nieuwe back-upentiteiten voor u gemaakt en naar de `BackupDataOutput` geschreven. Deze entiteiten worden automatisch gebruikt bij het herstellen.

**Meerdere identiteiten herstellen:**

De handleiding voor het maken van gegevensback-ups bevat een algemeen algoritme voor het herstellen van de gegevens van uw toepassing. Daarnaast bevat de sectie [Extending BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent) een codevoorbeeld. Als u meerdere identiteiten wilt herstellen, moet u de algemene structuur in deze voorbeeldcode volgen en met name letten op het volgende:

1. U moet een `while(data.readNextHeader())`-lus* gebruiken om door de back-upentiteiten te gaan.

2. U moet `data.skipEntityData()`* aanroepen als `data.getKey()`* niet overeenkomt met de sleutel die u in `onBackup` hebt geschreven. Als deze stap niet wordt uitgevoerd, is het mogelijk dat uw herstelbewerkingen mislukken.

3. Voorkom dat er tijdens het verbruik van back-entiteiten in de `while(data.readNextHeader())`-constructie* wordt geretourneerd, zodat de automatisch geschreven entiteiten niet verloren gaan.

* Waar `data` de lokale variabelenaam voor de **MAMBackupDataInput** is die tijdens de herstelbewerking wordt doorgegeven naar uw app.

## <a name="multi-identity-optional"></a>Meerdere identiteiten (optioneel)

### <a name="overview"></a>Overzicht
De Intune App SDK past beleid standaard op de hele app toe. Meerdere identiteiten is een optionele beveiligingsfunctie voor Intune-apps die kan worden ingeschakeld zodat beleid per identiteitsniveau kan worden toegepast. Hiervoor wordt aanzienlijk meer deelname van een app vereist dan bij andere app-beveiligingsfuncties.

> [!NOTE]
> Als de app niet op de juiste manier reageert, kan dit gegevensverlies of andere beveiligingsproblemen tot gevolg hebben.

Zodra de gebruiker het apparaat of de app registreert, registreert de SDK deze identiteit en beschouwt de SDK deze identiteit als de primaire beheerde identiteit. Andere gebruikers in de app worden behandeld als niet-beheerd, met onbeperkte beleidsinstellingen.

> [!NOTE]
> Op dit moment wordt per apparaat slechts één met Intune beheerde identiteit ondersteund.

Een identiteit wordt gedefinieerd als een tekenreeks. Identiteiten zijn **hoofdlettergevoelig** en in geretourneerde identiteitsaanvragen, die waren gericht aan de SDK, wordt mogelijk niet hetzelfde gebruik van hoofd- en kleine letters toegepast als oorspronkelijk is gebruikt toen de identiteit werd ingesteld.

De app *moet* aan de SDK melden wanneer de actieve identiteit zal worden gewijzigd. In sommige gevallen meldt de SDK ook aan de app wanneer er een identiteitswijziging is vereist. In de meeste gevallen kan MAM echter niet weten welke gegevens worden weergegeven in de gebruikersinterface of op enig moment in een thread worden gebruikt, en wordt ervan uitgegaan dat de app de juiste identiteit instelt om gegevensverlies te voorkomen. In de volgende secties worden een aantal specifieke scenario’s genoemd die actie door de app vereisen.

### <a name="enabling-multi-identity"></a>Meerdere identiteiten inschakelen

Alle apps worden standaard beschouwd als apps met één identiteit. U kunt aangeven dat een app met meerdere identiteiten kan werken door de volgende metagegevens in het bestand AndroidManifest.xml te plaatsen.

```xml
  <meta-data
    android:name="com.microsoft.intune.mam.MAMMultiIdentity"
    android:value="true" />
```

### <a name="setting-the-identity"></a>De identiteit instellen

Ontwikkelaars kunnen de identiteit van de app-gebruiker instellen op de volgende niveaus met aflopende prioriteit:

  1. Threadniveau
  2. Niveau `Context` (doorgaans `Activity`)
  3. Procesniveau

Een identiteit die is ingesteld op threadniveau, vervangt een identiteit die is ingesteld op het niveau `Context`, die weer een identiteit vervangt die is ingesteld op procesniveau. Een identiteit die is ingesteld voor een `Context` wordt alleen gebruikt in de juiste gekoppelde scenario’s. Zo hebben bestands-I/O-bewerkingen geen gekoppelde `Context`. Meestal stellen apps de `Context`-identiteit in voor een `Activity`. Een app *mag* geen gegevens weergeven voor een beheerde identiteit, tenzij de identiteit van de `Activity` is ingesteld op dezelfde identiteit. In het algemeen is de identiteit op procesniveau alleen nuttig als de app voor alle threads werkt met een enkele gebruiker tegelijk. Veel apps hoeven hiervan geen gebruik te maken.

Als uw app de `Application`-context gebruikt om systeemservices op te halen, moet u ervoor zorgen dat de thread- of procesidentiteit is ingesteld of dat u de UI-identiteit hebt ingesteld voor de `Application`-context van uw app.

Als uw app gebruikmaakt van een `Service`-context voor het starten van intenties, gebruikt u inhoudsoplossers of andere systeemservices en moet u ervoor zorgen dat u de identiteit instelt op de context `Service`.

Als u speciale gevallen wilt verwerken tijdens het bijwerken van de UI-identiteit met `setUIPolicyIdentity` of `switchMAMIdentity`, kunnen beide methoden worden doorgegeven als een set `IdentitySwitchOption`-waarden.

* `IGNORE_INTENT`: Gebruik deze optie als u een identiteitswisseling wilt aanvragen die de intentie die aan de huidige activiteit is gekoppeld, moet negeren.
  Bijvoorbeeld:

  1. Uw app ontvangt een intentie van een beheerde identiteit met daarin een beheerd document. In de app wordt het document weergegeven.
  2. De gebruiker schakelt over naar de persoonlijke identiteit, waardoor in de app dus een identiteitswisseling van de gebruikersinterface wordt aangevraagd. In de persoonlijke identiteit wordt in de app niet langer het document weergegeven, dus u kunt `IGNORE_INTENT` gebruiken om een identiteitswisseling aan te vragen.

  Als dit niet is ingesteld, gaat de SDK ervan uit dat de meest recente intentie nog steeds door de app wordt gebruikt. Hierdoor wordt de intentie door het ontvangstbeleid voor de nieuwe identiteit als inkomende gegevens behandeld en wordt die identiteit gebruikt.

>[!NOTE]
> Omdat de `CLIPBOARD_SERVICE` voor bewerkingen in de gebruikersinterface wordt gebruikt, wordt de UI-identiteit van de activiteit op de voorgrond door de SDK gebruikt voor `ClipboardManager`-bewerkingen.

De volgende methoden in `MAMPolicyManager` kunnen worden gebruikt om de identiteit in te stellen en de eerder ingestelde identiteitswaarden op te halen.

```java
public static void setUIPolicyIdentity(final Context context, final String identity, final MAMSetUIIdentityCallback mamSetUIIdentityCallback,
final EnumSet<IdentitySwitchOption> options);

public static String getUIPolicyIdentity(final Context context);

public static MAMIdentitySwitchResult setProcessIdentity(final String identity);

public static String getProcessIdentity();

public static MAMIdentitySwitchResult setCurrentThreadIdentity(final String identity);

public static String getCurrentThreadIdentity();

/**
 * Get the current app policy. This does NOT take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use the overload below.
 */
public static AppPolicy getPolicy();

/**
 * Get the current app policy. This DOES take the UI (Context) identity into account.
 * If the current operation has any context (e.g. an Activity) associated with it, use this function.
 */
public static AppPolicy getPolicy(final Context context);


public static AppPolicy getPolicyForIdentity(final String identity);

public static boolean getIsIdentityManaged(final String identity);
```

>[!NOTE]
> U kunt de identiteit van de app wissen door deze op null in te stellen.
>
> De lege tekenreeks kan worden gebruikt als een identiteit waarvoor nooit app-beveiligingsbeleid geldt.

#### <a name="results"></a>Resultaten
Alle methoden die worden gebruikt om de identiteit in te stellen, rapporteren resultaatwaarden via `MAMIdentitySwitchResult`. Er zijn vier waarden die kunnen worden geretourneerd:

| Retourwaarde | Scenario |
|--            |--        |
| `SUCCEEDED`    | De identiteit is gewijzigd. |
| `NOT_ALLOWED`  | De identiteit kan niet worden gewijzigd. Dit doet zich voor als is geprobeerd de identiteit van de gebruikersinterface (`Context`) in te stellen wanneer er een andere identiteit op de huidige thread is ingesteld. |
| `CANCELLED`    | De identiteitswijziging is geannuleerd door de gebruiker, in het algemeen door op de knop Terug te klikken bij een pincode-/verificatieprompt. |
| `FAILED`       | De identiteitswijziging is mislukt vanwege een niet-opgegeven reden.|

De app moet garanderen dat een identiteitswijziging is voltooid voordat bedrijfsgegevens worden weergegeven of gebruikt. Momenteel slagen wijzigingen van proces- en thread-identiteit altijd in een app waarvoor het gebruik van meerdere identiteiten is ingeschakeld, maar we behouden ons het recht voor om foutomstandigheden toe te voegen. De identiteitswijziging via de gebruikersinterface kan mislukken door ongeldige argumenten, als deze een conflict zou veroorzaken met de thread-identiteit, of als de gebruiker een voorwaarde voor voorwaardelijk starten annuleert (door bijvoorbeeld op backspace te drukken in het scherm voor het invoeren van de pincode). Het standaardgedrag voor een mislukte overschakeling naar een andere UI-identiteit bij een activiteit is om de activiteit te voltooien (zie `onSwitchMAMIdentityComplete` hierna).

Bij het instellen van een `Context`-identiteit via `setUIPolicyIdentity` wordt het resultaat asynchroon gerapporteerd. Als de `Context` een `Activity` is, weet de SDK pas of de identiteitswijziging is geslaagd nadat de voorwaardelijke start is uitgevoerd, waarvoor de gebruiker mogelijk een pincode of de volledige bedrijfsreferenties moet invoeren. De app kan een `MAMSetUIIdentityCallback` implementeren om dit resultaat te ontvangen of kan null doorgeven voor het callback-object. Merk op dat als een aanroep wordt gedaan naar `setUIPolicyIdentity` terwijl het resultaat van een eerdere aanroep naar `setUIPolicyIdentity` *in dezelfde context* nog niet is bezorgd, de nieuwe callback de oude vervangt en dat de oorspronkelijke callback nooit een resultaat ontvangt.

```java
  public interface MAMSetUIIdentityCallback {
    void notifyIdentityResult(MAMIdentitySwitchResult identitySwitchResult);
  }
```

U kunt de identiteit van een activiteit ook rechtstreeks instellen via een methode in `MAMActivity` in plaats van `MAMPolicyManager.setUIPolicyIdentity` aan te roepen. Gebruik de volgende methode om dit te doen:

```java
     public final void switchMAMIdentity(final String newIdentity, final EnumSet<IdentitySwitchOption> options);
```

U kunt ook een methode in `MAMActivity` als u wilt dat de app op de hoogte wordt gebracht van het resultaat van de pogingen om de identiteit van die activiteit te wijzigen.

``` java
    public void onSwitchMAMIdentityComplete(final MAMIdentitySwitchResult result);
```

Als u `onSwitchMAMIdentityComplete` niet overschrijft (of de `super`-methode niet aanroept), leidt een mislukte identiteitswisseling bij een activiteit tot voltooiing van de activiteit. Als u de methode overschrijft, moet u ervoor zorgen dat er geen bedrijfsgegevens worden weergegeven na een mislukte identiteitswisseling.

>[!NOTE]
> Bij het overschakelen naar een andere identiteit moet de activiteit mogelijk opnieuw worden gemaakt. In dit geval wordt de `onSwitchMAMIdentityComplete`-callback geleverd aan het nieuwe exemplaar van de activiteit.


### <a name="implicit-identity-changes"></a>Impliciete identiteitswijzigingen

Naast de mogelijkheid van de app om de identiteit in te stellen, kan de identiteit van een thread of context worden gewijzigd op basis van binnenkomende gegevens vanuit een andere door Intune beheerde app waarop app-beveiligingsbeleid is toegepast.

#### <a name="examples"></a>Voorbeelden
1. Als een activiteit wordt gestart vanuit een `Intent` die door een andere MAM-app is verzonden, wordt de identiteit van de activiteit ingesteld op basis van de geldige identiteit in de andere app op het moment dat de `Intent` werd verzonden.

2. Voor services wordt de threadidentiteit op ongeveer dezelfde manier ingesteld als voor de duur van een `onStart`- of `onBind`-aanroep. Aanroepen naar de `Binder` die is geretourneerd door `onBind`, stellen ook tijdelijk de threadidentiteit in.

3. Aanroepen naar een `ContentProvider` stellen op dezelfde manier de threadidentiteit voor hun duur in.


  Bovendien kan de gebruikersinteractie met een activiteit een impliciete identiteitswisseling veroorzaken.

  **Voorbeeld:** Als een gebruiker tijdens `Resume` een autorisatieprompt annuleert, resulteert dit in een impliciete overgang naar een lege identiteit.

  De app wordt de mogelijkheid geboden om op de hoogte te worden gebracht van deze wijzigingen en ze zo nodig te verbieden. `MAMService` en `MAMContentProvider` maken de volgende methode beschikbaar die door subklassen kan worden overschreven:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchResultCallback callback);
  ```

  In de klasse `MAMActivity` is een extra parameter aanwezig in de methode:

  ```java
  public void onMAMIdentitySwitchRequired(final String identity,
          final AppIdentitySwitchReason reason,
          final AppIdentitySwitchResultCallback callback);
  ```

  * De `AppIdentitySwitchReason` registreert de bron van de impliciete wisseling en kan de waarden `CREATE`, `RESUME_CANCELLED` en `NEW_INTENT` accepteren.  De reden `RESUME_CANCELLED` wordt gebruikt wanneer het voortzetten van de activiteit ertoe leidt dat de gebruikersinterface voor een pincode, verificatie of andere naleving wordt weergegeven en de gebruiker die gebruikersinterface probeert te annuleren, meestal door de knop Terug te gebruiken.


    * De `AppIdentitySwitchResultCallback` ziet er als volgt uit:

      ```java
      public interface AppIdentitySwitchResultCallback {
          /**
            * @param result
            *            whether the identity switch can proceed.
            */
          void reportIdentitySwitchResult(AppIdentitySwitchResult result);
        }
        ```

      Waarbij ```AppIdentitySwitchResult``` ofwel `SUCCESS` of `FAILURE` is.

De methode `onMAMIdentitySwitchRequired` wordt aangeroepen voor alle impliciete identiteitswijzigingen behalve de wijzigingen die zijn aangebracht via een Binder die is geretourneerd door `MAMService.onMAMBind`. Met de standaardimplementaties van `onMAMIdentitySwitchRequired` wordt onmiddellijk het volgende aangeroepen:

* `reportIdentitySwitchResult(FAILURE)` als `RESUME_CANCELLED` de reden is.

* `reportIdentitySwitchResult(SUCCESS)` in alle andere gevallen.

  Het is niet waarschijnlijk dat de meeste apps een identiteitswisseling op een andere manier moeten blokkeren of vertragen, maar als dit voor een app toch nodig is, zijn de volgende punten van belang:

  * Als het overschakelen naar een andere identiteit wordt geblokkeerd, is het resultaat hetzelfde als wanneer de `Receive`-instellingen voor delen de gegevensinvoer verbieden.

  * Als een service wordt uitgevoerd op de hoofdthread, **moet** `reportIdentitySwitchResult` synchroon worden aangeroepen, anders reageert de UI-thread niet meer.

  * Voor het maken van **`Activity`** wordt eerst `onMAMIdentitySwitchRequired` en vervolgens `onMAMCreate` aangeroepen. Als de app UI moet weergeven om te bepalen of de identiteitswisseling is toegestaan, moet die UI worden weergegeven met een *andere* activiteit.

  * Wanneer in een **`Activity`** een overgang naar de lege identiteit wordt aangevraagd met een reden zoals `RESUME_CANCELLED`, moet de app de voortgezette activiteit wijzigen om gegevens consistent met die identiteitswisseling weer te geven.  Als dit niet mogelijk is, moet de app de overschakeling weigeren en wordt de gebruiker opnieuw gevraagd te voldoen aan het beleid voor de identiteit die wordt voortgezet (bijvoorbeeld doordat het invoerscherm voor de pincode van app wordt weergegeven).

    > [!NOTE]
    > Een app met meerdere identiteiten ontvangt altijd inkomende gegevens van beheerde en onbeheerde apps. Het is de verantwoordelijkheid van de app om gegevens van beheerde identiteiten op een beheerde manier te behandelen.

  Als een aangevraagde identiteit wordt beheerd (gebruik `MAMPolicyManager.getIsIdentityManaged` om dit te controleren), maar de app dat account niet kan gebruiken (bijvoorbeeld omdat accounts, zoals e-mailaccounts, eerst in de app moeten worden ingesteld), moet de identiteitswisseling worden geweigerd.

#### <a name="build-plugin--tool-considerations"></a>Overwegingen voor build-invoegtoepassing/build-hulpprogramma
Als u de gegevens niet expliciet overneemt van `MAMActivity`, `MAMService` of `MAMContentProvider` (omdat u die wijziging door een build-hulpprogramma laat aanbrengen), maar identiteitswisselingen nog moet verwerken, kunt u in plaats daarvan `MAMActivityIdentityRequirementListener` implementeren (voor een `Activity`) of `MAMIdentityRequirementListener` (voor een `Service` of `ContentProviders`).
Het standaardgedrag voor `MAMActivity.onMAMIdentitySwitchRequired` kan worden geopend door het aanroepen van de statische methode `MAMActivity.defaultOnMAMIdentitySwitchRequired(activity, identity,
reason, callback)`.

Op dezelfde manier geldt: als u `MAMActivity.onSwitchMAMIdentityComplete` wilt overschrijven, kunt u `MAMActivityIdentitySwitchListener` implementeren zonder expliciete overname van `MAMActivity`.

### <a name="preserving-identity-in-async-operations"></a>Identiteit In asynchrone bewerkingen behouden
Bewerkingen voor de UI-thread verzenden gewoonlijk achtergrondtaken naar een andere thread. Een app met meerdere identiteiten zorgt ervoor dat deze achtergrondtaken werken met de juiste identiteit, vaak dezelfde identiteit die wordt gebruikt door de activiteit die ze heeft verzonden. De MAM SDK biedt `MAMAsyncTask` en `MAMIdentityExecutors` als hulpmiddel bij het behouden van de identiteit.
Deze moeten worden gebruikt als via een asynchrone bewerking bedrijfsgegevens naar een bestand kunnen worden geschreven of als er met andere apps kan worden gecommuniceerd.

#### <a name="mamasynctask"></a>MAMAsyncTask

Als u `MAMAsyncTask` wilt gebruiken, neemt u deze over in plaats van een `AsyncTask` en vervangt u onderdrukkingen van `doInBackground` en `onPreExecute` door respectievelijk `doInBackgroundMAM` en `onPreExecuteMAM`. De constructor `MAMAsyncTask` neemt een activiteitscontext. Bijvoorbeeld:

```java
AsyncTask<Object, Object, Object> task = new MAMAsyncTask<Object, Object, Object>(thisActivity) {

    @Override
    protected Object doInBackgroundMAM(final Object[] params) {
        // Do operations.
    }

    @Override
    protected void onPreExecuteMAM() {
        // Do setup.
    };
}
```

### <a name="mamidentityexecutors"></a>MAMIdentityExecutors
Met `MAMIdentityExecutors` kunt u een bestaand exemplaar van `Executor` of `ExecutorService` verpakken als een `Executor`/`ExecutorService` met behoud van de identiteit met de methoden `wrapExecutor` en `wrapExecutorService`. Bijvoorbeeld

```java
Executor wrappedExecutor = MAMIdentityExecutors.wrapExecutor(originalExecutor, activity);
ExecutorService wrappedService = MAMIdentityExecutors.wrapExecutorService(originalExecutorService, activity);
```

### <a name="file-protection"></a>Bestandsbeveiliging
Op het moment dat een bestand wordt gemaakt, wordt er op basis van een thread- en procesidentiteit een identiteit aan het bestand gekoppeld. Deze identiteit wordt gebruikt voor zowel bestandsversleuteling als selectief wissen. Alleen bestanden waarvan de identiteit word beheerd en een beleid heeft dat versleuteling vereist, worden versleuteld. De standaard-SDK-actie voor het selectief wissen van functies wist alleen bestanden die zijn gekoppeld aan de beheerde identiteit waarvoor wissen is aangevraagd. De app kan de identiteit van een bestand opvragen of wijzigen met de klasse `MAMFileProtectionManager`.

```java
public final class MAMFileProtectionManager {

   /**
    * Protect a file or directory. This will synchronously trigger whatever protection is required for the file, and will tag the
    * file for future protection changes. If an identity is set on a directory, it is set recursively on all files and
    * subdirectories. New files or directories will inherit their parent directory's identity. If MAM is operating in offline mode,
    * this method will silently do nothing.
    *
    * @param identity
    *        Identity to set.
    * @param file
    *        File to protect.
    *
    * @throws IOException
    *         If the file cannot be protected.
    */
   public static void protect(final File file, final String identity) throws IOException;

   /**
     * Protect a file obtained from a content provider. This is intended to be used for
     * sdcard (whether internal or removable) files accessed through the Storage Access Framework.
     * It may also be used with descriptors referring to private files owned by this app.
     * It is not intended to be used for files owned by other apps and such usage will fail. If
     * creating a new file via a content provider exposed by another MAM-integrated app, the new
     * file identity will automatically be set correctly if the ContentResolver in use was
     * obtained via a Context with an identity or if the thread identity is set.
     *
     * This will synchronously trigger whatever protection is required for the file, and will tag
     * the file for future protection changes. If an identity is set on a directory, it is set
     * recursively on all files and subdirectories. If MAM is operating in offline mode, this
     * method will silently do nothing.
     *
     * @param identity
     *            Identity to set.
     * @param file
     *            File to protect.
     *
     * @throws IOException
     *             If the file cannot be protected.
     */
    public static void protect(final ParcelFileDescriptor file, final String identity) throws IOException;

   /**
    * Get the protection info on a file. This method should only be used if the file is located in the calling application's
    * private storage or the device's shared storage. If opening a file with a content resolver, use the overload which
    * takes a ParcelFileDescriptor instead.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final File file) throws IOException;

   /**
    * Get the protection info on a file descriptor such as one opened through a content resolver.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final ParcelFileDescriptor file) throws IOException;

}

public interface MAMFileProtectionInfo {
    String getIdentity();
}
 ```

#### <a name="app-responsibility"></a>App-verantwoordelijkheid
MAM kan niet automatisch een relatie afleiden tussen bestanden die worden gelezen en gegevens die worden weergegeven in een `Activity`. Apps *moeten* de identiteit van de gebruikersinterface goed instellen voordat bedrijfsgegevens worden weergegeven. Dit geldt ook voor gegevens die worden gelezen uit bestanden. Als een bestand afkomstig is van buiten de app (van een `ContentProvider` of gelezen vanaf een openbaar leesbare locatie), *moet* de app proberen de bestandsidentiteit vast te stellen (met de correcte `MAMFileProtectionManager.getProtectionInfo` overbelasting voor de gegevensbron) voordat de uit het bestand gelezen informatie wordt weergegeven. Als `getProtectionInfo` aangeeft dat de identiteit niet null en niet leeg is, *moet* de identiteit van de gebruikersinterface worden ingesteld op deze identiteit (met `MAMActivity.switchMAMIdentity` of `MAMPolicyManager.setUIPolicyIdentity`). Als de identiteitswijziging mislukt, moeten de gegevens uit het bestand *niet* worden weergegeven.

Het proces verloopt ongeveer als volgt:
  * De gebruiker selecteert een document om in de app te openen.
  * Tijdens het openen en voordat gegevens van schijf worden gelezen, bevestigt de app de identiteit die moet worden gebruikt voor het weergeven van de inhoud:

    ```java
    MAMFileProtectionInfo info = MAMFileProtectionManager.getProtectionInfo(docPath)
    if (info != null)
        MAMPolicyManager.setUIPolicyIdentity(activity, info.getIdentity(), callback, EnumSet.noneOf<IdentitySwitchOption.class>)
    ```

  * De app wacht tot een resultaat wordt gerapporteerd voor retouraanroep.
  * Als het gerapporteerde resultaat ‘mislukt’ is, geeft de app het document niet weer.
  * De app opent het bestand en geeft het weer.
  
Als een app gebruikmaakt van de `DownloadManager` van Android om bestanden te downloaden, probeert de MAM SDK deze bestanden automatisch te beveiligen met de procesidentiteit. Als de gedownloade bestanden bedrijfsgegevens bevatten, is het de verantwoordelijkheid van de app om `protect` aan te roepen als de bestanden na het downloaden worden verplaatst of opnieuw worden gemaakt.

#### <a name="single-identity-to-multi-identity-transition"></a>Overgang van één identiteit naar meerdere identiteiten
Als een app die eerder is uitgebracht met Intune-integratie met één identiteit, later wordt geïntegreerd met meerdere identiteiten, wordt voor eerder geïnstalleerde apps een overgang uitgevoerd (niet zichtbaar voor de gebruiker, er is geen gekoppelde UX). Het is niet *vereist* dat de app expliciet wordt gebruikt om deze overgang te verwerken. Alle bestanden die zijn gemaakt voordat de overgang wordt voorgezet, worden als beheerd beschouwd (ze blijven dus versleuteld als er versleutelingsbeleid is ingeschakeld). Indien gewenst kunt u de upgrade detecteren en `MAMFileProtectionManager.protect` gebruiken om specifieke bestanden of directory's met de lege identiteit te taggen (als deze zijn versleuteld, wordt hiermee de versleuteling verwijderd).

#### <a name="offline-scenarios"></a>Scenario’s voor offline
Het labelen van de bestandsidentiteit is gevoelig voor de offlinemodus. U moet rekening houden met de volgende punten:

* Als de bedrijfsportal niet is geïnstalleerd, is taggen van bestandsidentiteit niet mogelijk.

* Als de bedrijfsportal is geïnstalleerd maar de app geen Intune MAM-beleid heeft, is niet mogelijk om bestanden op een betrouwbare manier worden getagd met identiteitslabels.

* Wanneer het taggen van bestandsidentiteit beschikbaar komt, worden alle eerder gemaakte bestanden als persoonlijk/onbeheerd behandeld (behorend bij de identiteit met een lege tekenreeks), tenzij de app eerder is geïnstalleerd als een beheerde app met één identiteit. In dat geval wordt deze behandeld als behorend tot de geregistreerde gebruiker.

### <a name="directory-protection"></a>Mapbeveiliging

Mappen kunnen worden beveiligd met dezelfde `protect`-methode als voor de beveiliging van bestanden. Houd er rekening mee dat de mapbeveiliging recursief wordt toegepast op alle bestanden en submappen in de map en wordt toegepast op nieuwe bestanden die in de map worden gemaakt. Omdat mapbeveiliging recursief wordt toegepast, kan het even duren voordat de aanroep `protect` is voltooid voor grote mappen. Om die reden is het mogelijk dat apps die beveiliging toepassen op een map met een groot aantal bestanden, `protect` asynchroon willen uitvoeren op een thread op de achtergrond.

### <a name="data-protection"></a>Gegevensbescherming

Het is niet mogelijk om een bestand te taggen als behorend bij meerdere identiteiten. Wanneer voor apps gegevens moeten worden opgeslagen die behoren tot verschillende gebruikers in hetzelfde bestand, kan dit handmatig worden gedaan met de functies van `MAMDataProtectionManager`. De app kan dan gegevens versleutelen en deze koppelen aan een bepaalde gebruiker. De versleutelde gegevens zijn geschikt voor het opslaan naar schijf in een bestand. U kunt de gegevens opvragen die aan de identiteit zijn gekoppeld. De gegevens kunnen later worden ontsleuteld.

Apps die gebruikmaken van `MAMDataProtectionManager` moeten een ontvanger implementeren voor de melding `MANAGEMENT_REMOVED`. Nadat deze melding is voltooid, kunnen de buffers die via deze klasse zijn beveiligd, niet meer worden gelezen als bestandsversleuteling was ingeschakeld op het moment dat de buffers werden beveiligd. Een app kan deze situatie oplossen door tijdens deze melding `MAMDataProtectionManager.unprotect` aan te roepen voor alle buffers. U kunt ook zonder problemen de beveiliging aanroepen tijdens deze melding als u de identiteitsgegevens wilt behouden. De versleuteling is gegarandeerd uitgeschakeld tijdens de melding.


```java

public final class MAMDataProtectionManager {
    /**
     * Protect a stream. This will return a stream containing the protected
     * input.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect, read sequentially. This function
     *            will change the position of the stream but may not have
     *            read the entire stream by the time it returns. The
     *            returned stream will wrap this one. Calls to read on the
     *            returned stream may cause further reads on the original
     *            input stream. Callers should not expect to read directly
     *            from the input stream after passing it to this method.
     *            Calling close on the returned stream will close this one.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static InputStream protect(final InputStream input, final String identity);

    /**
     * Protect a byte array. This will return protected bytes.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static byte[] protect(final byte[] input, final String identity) throws IOException;

    /**
     * Unprotect a stream. This will return a stream containing the
     * unprotected input.
     *
     * @param input
     *            Input data to protect, read sequentially.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static InputStream unprotect(final InputStream input) throws IOException;

    /**
     * Unprotect a byte array. This will return unprotected bytes.
     *
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static byte[] unprotect(final byte[] input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input stream to get information on. Either this input
     *            stream must have been returned by a previous call to
     *            protect OR input.markSupported() must return true.
     *            Otherwise it will be impossible to get protection info
     *            without advancing the stream position. The stream must be
     *            positioned at the beginning of the protected data.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final InputStream input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input bytes to get information on. These must be bytes
     *            returned by a previous call to protect() or a copy of
     *            such bytes.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final byte[] input) throws IOException;
}
```


### <a name="content-providers"></a>Inhoudsproviders

Als de app andere bedrijfsgegevens biedt dan een `ParcelFileDescriptor` via een `ContentProvider`, moet de app de methode `isProvideContentAllowed(String)` in `MAMContentProvider` aanroepen om de UPN (user principal name) van de identiteit van de eigenaar door te geven voor de inhoud. Als deze functie onwaar retourneert, moet de inhoud *niet* worden geretourneerd aan de oproepende functie. Bestandsdescriptors die zijn geretourneerd via een inhoudsprovider, worden automatisch verwerkt op basis van de bestandsidentiteit.

Als u `MAMContentProvider` niet expliciet overneemt en in plaats daarvan toestaat dat de wijzigingen door de bouwhulpprogramma's kunnen worden gemaakt, kunt u een statische versie van dezelfde methode aanroepen: `MAMContentProvider.isProvideContentAllowed(provider,
contentIdentity)`.

### <a name="selective-wipe"></a>Selectief wissen

Als een app met meerdere identiteiten wordt geregistreerd voor de melding `WIPE_USER_DATA`, is het de verantwoordelijkheid van de app dat alle gegevens voor de gebruiker worden gewist, met inbegrip van alle bestanden waarvan de identiteit is getagd als behorend aan die gebruiker. Als de app gebruikersgegevens uit een bestand verwijdert maar andere gegevens in het bestand wil bewaren, *moet* het de identiteit van het bestand wijzigen (via `MAMFileProtectionManager.protect` voor een persoonlijke gebruiker of de lege identiteit). Als versleutelingsbeleid wordt gebruikt, worden alle resterende bestanden van de gebruiker die worden gewist, niet ontsleuteld, en zijn deze na het wissen niet langer toegankelijk voor de app.

Een app die wordt geregistreerd voor `WIPE_USER_DATA` profiteert niet van het voordeel van het standaardgedrag van de SDK voor selectief wissen. Voor apps die met meerdere identiteiten kunnen werken, kan dit verlies belangrijker zijn omdat met de standaard-MAM-actie voor selectief wissen alleen bestanden worden gewist waarvan de identiteit het doel is van een wisbewerking. Als een app die met meerdere identiteiten kan werken, de standaard-MAM-functie voor selectief wissen wil uitvoeren _**en**_ eigen wisacties wil uitvoeren, moet de app worden geregistreerd voor `WIPE_USER_AUXILIARY_DATA`-meldingen. Deze melding wordt direct door de SDK verzonden, nog voordat u de standaard-MAM-actie voor selectief wissen wordt uitgevoerd. Een app mag nooit voor zowel `WIPE_USER_DATA` als `WIPE_USER_AUXILIARY_DATA` worden geregistreerd.

Dankzij de standaardinstelling voor selectief wissen wordt de app zorgvuldig gesloten, worden activiteiten afgerond en wordt het app-proces beëindigd. Als de standaardbewerking voor selectief wissen door de app wordt overschreven, kunt u de app handmatig sluiten om te voorkomen dat gebruikers toegang hebben tot gegevens in het geheugen nadat een wisbewerking is uitgevoerd.


## <a name="enabling-mam-targeted-configuration-for-your-android-applications-optional"></a>Op MAM gerichte configuratie inschakelen voor Android-toepassingen (optioneel)
Toepassingsspecifieke sleutel-waardeparen kunnen worden geconfigureerd in de Intune-console voor [MAM-WE](https://docs.microsoft.com/intune/app-configuration-policies-managed-app) en [Android Enterprise](https://docs.microsoft.com/intune/app-configuration-policies-use-android).
Deze sleutel-waardeparen worden niet geïnterpreteerd door Intune, maar doorgegeven aan de app. Toepassingen die een dergelijke configuratie moeten ontvangen, kunnen dat doen met de klassen `MAMAppConfigManager` en `MAMAppConfig`. Als er meerdere beleidsregels zijn gericht op dezelfde app, kunnen er meerdere conflicterende waarden beschikbaar zijn voor dezelfde sleutel.

> [!NOTE] 
> De installatie van configuraties voor levering via MAM-WE kan niet worden geleverd in `offline` (wanneer de Bedrijfsportal niet is geïnstalleerd).  In dit geval worden alleen Android Enterprise AppRestrictions via een `MAMUserNotification` voor een lege identiteit geleverd.

### <a name="get-the-app-config-for-a-user"></a>De app-configuratie voor een gebruiker ophalen
App-configuratie kan als volgt worden opgehaald:
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
```

Als er geen MAM-geregistreerde gebruiker is, maar uw app wil wel een Android Enterprise-configuratie ophalen (die niet wordt gericht op een specifieke gebruiker), kunt u een null of een lege tekenreeks doorgeven.

### <a name="conflicts"></a>Conflicten
Een waarde die is ingesteld in MAM-app-configuratie, overschrijft een waarde met dezelfde sleutel die in Android Enterprise-configuratie is ingesteld. 

Als een beheerder conflicterende waarden configureert voor dezelfde sleutel (bijvoorbeeld door verschillende app-configuratiesets met dezelfde sleutel te richten op meerdere groepen met dezelfde gebruiker), heeft Intune geen manier om dit conflict automatisch op te lossen en worden alle waarden beschikbaar voor uw app. 

Uw app kan alle waarden voor een bepaalde sleutel opvragen bij een `MAMAppConfig`-object:
```java
List<Boolean> getAllBooleansForKey(String key)
List<Long> getAllIntegersForKey(final String key)
List<Double> getAllDoublesForKey(final String key)
List<String> getAllStringsForKey(final String key)
```

of kan vragen dat er een waarde wordt gekozen:
```java
Boolean getBooleanForKey(String key, BooleanQueryType queryType)
Long getIntegerForKey(String key, NumberQueryType queryType)
Double getDoubleForKey(String key, NumberQueryType queryType)
String getStringForKey(String key, StringQueryType queryType)

enum BooleanQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns true if any of the values are true.
     */
    Or,
    /**
     * In case of conflict, returns false if any of the values are false.
     */
    And
}

enum NumberQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the minimum Integer.
     */
    Min,
    /**
     * In case of conflict, returns the maximum Integer.
     */
    Max
}

enum StringQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the first result ordered alphabetically.
     */
    Min,

    /**
     * In case of conflict, returns the last result ordered alphabetically.
     */
    Max
}
```

Uw app kan ook de onbewerkte gegevens aanvragen als een lijst met sets van sleutel-waardeparen.

```java
List<Map<String, String>> getFullData()
```


### <a name="full-example"></a>Compleet voorbeeld
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
String fooValue = null;
if (appConfig.hasConflict("foo")) {
    List<String> values = appConfig.getAllStringsForKey("foo");
    fooValue = chooseBestValue(values);
} else {
    valueToUse = appConfig.getStringForKey("foo", MAMAppConfig.StringQueryType.Any);
}
Long barValue = appConfig.getIntegerForKey("bar", MAMAppConfig.NumberQueryType.Min);
```

### <a name="notification"></a>Melding
App-configuratie voegt een nieuw type melding toe:
* **REFRESH_APP_CONFIG**: Deze melding wordt verzonden in een `MAMUserNotification` om de app te informeren dat er nieuwe configuratiegegevens voor de app beschikbaar zijn.

### <a name="further-reading"></a>Meer lezen
Als u meer wilt weten over het maken van een op MAM gericht app-configuratiebeleid in Android, raadpleegt u het onderwerp over op MAM gerichte app-configuratie in [How to use Microsoft Intune app configuration policies for Android](https://docs.microsoft.com/intune/app-configuration-policies-managed-app) (App-configuratiebeleid van Microsoft Intune voor Android gebruiken).

App-configuratie kan ook worden geconfigureerd met behulp van de Graph API. Zie de [Graph API-documentatie voor gerichte MAM-configuratie](https://docs.microsoft.com/graph/api/resources/intune-mam-targetedmanagedappconfiguration) voor meer informatie.

## <a name="custom-themes-optional"></a>Aangepaste thema's (optioneel)
Er kan een aangepast thema worden ingesteld voor de MAM SDK die wordt toegepast op alle schermen en dialoogvensters van MAM. Als er geen thema wordt gegeven, wordt een standaard MAM-thema gebruikt.

### <a name="how-to-provide-a-theme"></a>Een thema opgeven
Als u een thema wilt opgeven, moet u de volgende regel code toevoegen in de methode `Application.onCreate`:

```java
MAMThemeManager.setAppTheme(R.style.AppTheme);
```

In het bovenstaande voorbeeld moet u `R.style.AppTheme` vervangen door het stijlthema dat de SDK moet toepassen.

## <a name="style-customization-deprecated"></a>Stijlaanpassing (afgeschaft)

Dit is nu afgeschaft en Aangepaste thema's (hierboven) is de voorkeursmanier om weergaven aan te passen.

Weergaven die worden gegenereerd door de MAM SDK kunnen visueel worden aangepast aan de app waarin de MAM SDK is geïntegreerd. U kunt de primaire, secundaire en achtergrondkleuren en de grootte van het app-logo aanpassen. Deze stijlaanpassing is optioneel. Als er geen aangepaste stijl is geconfigureerd, worden de standaardinstellingen gebruikt.


### <a name="how-to-customize"></a>Aanpassingen maken
Als de stijlwijzigingen moeten worden toegepast op de Intune MAM-weergavenviews, moet u eerst een XML-bestand met stijloverschrijvingen maken. Dit bestand moet in de map /res/xml van uw app worden geplaatst. U kunt het bestand elke gewenste naam geven. Hieronder volgt een voorbeeld van de indeling die voor dit bestand moet worden gevolgd.

```xml
<?xml version="1.0" encoding="utf-8"?>
<styleOverrides>
    <item
        name="foreground_color"
        resource="@color/red"/>
    <item
        name="accent_color"
        resource="@color/blue"/>
    <item
        name="background_color"
        resource="@color/green"/>
    <item
        name="logo_image"
        resource="@drawable/app_logo"/>
</styleOverrides>
```

U moet de bestaande resources in uw app opnieuw gebruiken. U moet bijvoorbeeld de kleur groen in het bestand colors.xml file definiëren en een verwijzing aan het bestand toevoegen. U kunt niet de hexadecimale kleurencode #0000ff gebruiken. De maximale grootte voor het app-logo is 110 dip (dp). U kunt desgewenst een kleinere logoafbeelding gebruiken, maar de maximale grootte resulteert in de best uitziende resultaten. Als u de limiet van 110 dip overschrijdt, wordt de afbeelding verkleind, waardoor deze mogelijk onscherp wordt weergegeven.

Hieronder volgt een compleet overzicht van de toegestane stijlkenmerken, de UI-elementen die ze besturen, hun itemnamen van de XML-kenmerken en het type resource dat voor elk kenmerk wordt verwacht.

|Stijlkenmerk | UI-elementen die worden beïnvloed | Itemnaam van het kenmerk | Verwacht resourcetype |
| -- | -- | -- | -- |
| Achtergrondkleur | Achtergrondkleur van het scherm voor het invoeren van de pincode <Br>Opvulkleur van het vak voor de pincode | background_color | Kleur |
| Voorgrondkleur | Kleur van de voorgrondtekst <br> Kaderrand van het pincodevak met standaardstatus <br> Tekens (inclusief verborgen tekens) in het pincodevak wanneer de gebruiker een pincode invoert| foreground_color | Kleur|
| Accentkleur | Kaderrand van het gemarkeerde pincodevak <br> Hyperlinks |accent_color | Kleur |
| App-logo | Grote pictogrammen die worden weergegeven in het pincodescherm van de Intune-app | logo_image | Tekenbaar |

## <a name="default-enrollment-optional"></a>Standaard inschrijving (optioneel)

Hier volgen richtlijnen voor het vereisen van gebruikersprompts bij het starten van een app voor automatische registratie bij de APP-WE-service (dit wordt **standaardinschrijving** genoemd in deze sectie), waarvoor beveiligingsbeleid voor apps in Intune is vereist om uw in SDK geïntegreerde Android LOB-app te gebruiken. Ook wordt beschreven hoe u eenmalige aanmelding kunt inschakelen voor uw in SDK geïntegreerde Android LOB-apps. Dit wordt **niet** ondersteund voor Store-apps die kunnen worden gebruikt door niet-Intune-gebruikers.

> [!NOTE] 
> Een van de voordelen van **standaardinschrijving** is dat u eenvoudiger beleid kunt ophalen uit de APP-WE-service voor een app op het apparaat.

> [!NOTE] 
> **Standaardinschrijving** is compatibel met onafhankelijke clouds.

Schakel standaardinschrijving in aan de hand van de volgende stappen:

1. Als ADAL in uw app is geïntegreerd of als u eenmalige aanmelding moet inschakelen, moet u [ADAL configureren](#configure-azure-active-directory-authentication-library-adal) volgens [algemene ADAL-configuratie](#common-adal-configurations) nummer 2. Als dit niet het geval is, kunt u deze stap overslaan.

  > [!NOTE]
  > Azure Active Directory (Azure AD) Authentication Library (ADAL) en Azure AD Graph API worden afgeschaft. Zie [Uw toepassingen bijwerken voor het gebruik van Microsoft Authentication Library (MSAL) en Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363) voor meer informatie.
   
2. Schakel standaardinschrijving in door de volgende waarde toe te voegen in het manifest onder de tag `<application>`:

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.DefaultMAMServiceEnrollment" android:value="true" />
   ```

   > [!NOTE] 
   > Dit moet de enige MAM-WE-integratie in de app zijn. Als er andere pogingen zijn gedaan om MAMEnrollmentManager-API's aan te roepen, treden er conflicten op.

3. Schakel vereist MAM-beleid in door de volgende waarde toe te voegen in het manifest onder de tag `<application>`:

   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.MAMPolicyRequired" android:value="true" />
   ```

   > [!NOTE] 
   > Dit zorgt ervoor dat de gebruiker de bedrijfsportal op het apparaat moet downloaden en de standaardstroom voor inschrijving moet voltooien vóór gebruik.


## <a name="limitations"></a>Beperkingen

### <a name="policy-enforcement-limitations"></a>Beperkingen op het afdwingen van beleid

* **Inhoudsoplossers gebruiken**: het Intune-beleid voor 'overdracht of ontvangst' kan het gebruik van een inhoudsoplosser geheel of gedeeltelijk blokkeren voor toegang tot de inhoudsprovider in een andere app. Dit zorgt ervoor dat `ContentResolver`-methoden null retourneren of een foutwaarde afgeven (bijvoorbeeld: `openOutputStream` genereert `FileNotFoundException`, indien geblokkeerd). De app kan bepalen of het mislukte schrijven van gegevens via een inhoudsoplosser is veroorzaakt door beleid (of zou worden veroorzaakt door beleid) door de volgende oproep te plaatsen:

    ```java
    MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(contentURI);
    ```

    of als er geen gekoppelde activiteit is:

    ```java
    MAMPolicyManager.getPolicy().getIsSaveToLocationAllowed(contentURI);
    ```

    In dit tweede geval moeten apps met meerdere identiteiten ervoor zorgen dat de thread-identiteit goed is ingesteld (of een expliciete identiteit doorgeven aan de `getPolicy`-aanroep).

### <a name="exported-services"></a>Geëxporteerde services
Het bestand AndroidManifest.xml, dat deel uitmaakt van de SDK voor de Intune-app, bevat **MAMNotificationReceiverService**, wat een geëxporteerde service moet zijn om toe te staan dat de bedrijfsportal meldingen naar een beheerde app verzendt. De service controleert de oproepende functie om ervoor te zorgen dat alleen de Bedrijfsportal meldingen mag verzenden.

### <a name="reflection-limitations"></a>Reflectiebeperkingen
Sommige MAM-basisklassen (bijvoorbeeld `MAMActivity`, `MAMDocumentsProvider`) bevatten methoden (op basis van de oorspronkelijke Android-basisklassen) die alleen gebruikmaken van parameters of typen retourneren die aanwezig zijn boven bepaalde API-niveaus. Daarom is het niet altijd mogelijk om reflectie te gebruiken om alle methoden van app-onderdelen op te sommen. Deze beperking is niet beperkt tot MAM en is dezelfde beperking die van toepassing zou zijn als de app zelf deze methoden van de Android-basisklassen heeft geïmplementeerd.

### <a name="robolectric"></a>Robolectric
Het testen van het MAM SDK-gedrag onder Robolectric wordt niet ondersteund. Er zijn bekende problemen bij het uitvoeren van de MAM SDK onder Robolectric vanwege aanwezig gedrag onder Robolectric dat niet nauwkeurig het gedrag op echte apparaten of emulatoren simuleert.

Als u uw toepassing onder Robolectric moet testen, is het de aanbevolen tijdelijke oplossing om de klasselogica van uw toepassing te verplaatsen naar een helper en uw test-APK voor eenheden te produceren met een toepassingsklasse die niet erft van MAMApplication.

## <a name="expectations-of-the-sdk-consumer"></a>Verwachtingen van de SDK-consument

De Intune SDK onderhoudt het contract geleverd door de Android-API, hoewel er vaker foutmeldingen als gevolg van beleidsafdwinging kunnen worden geactiveerd. Deze aanbevolen Android-procedures verminderen de kans op fouten:

* Android SDK-functies die null kunnen retourneren, hebben nu een grotere kans om null te zijn.  Om problemen tot een minimum te beperken, zorgt u ervoor dat null-controles op de juiste plaatsen worden uitgevoerd.

* Functies die kunnen worden gecontroleerd, moeten worden gecontroleerd via hun MAM-vervangings-API's.

* Eventuele afgeleide functies moeten oproepen uitvoeren via de versies van hun bovenliggende klasse.

* Vermijd het niet-eenduidige gebruik van API's. Bijvoorbeeld: wanneer u `Activity.startActivityForResult` zonder te controleren of de requestCode vreemd gedrag kan veroorzaken.

### <a name="services"></a>Services
Beleidsafdwinging kan invloed hebben op service-interacties.
Methoden die verbinding maken met een afhankelijke service, zoals `Context.bindService`, kunnen mislukken vanwege het afdwingen van het onderliggende beleid in `Service.onBind` en kunnen leiden tot `ServiceConnection.onNullBinding` of `ServiceConnection.onServiceDisconnected`.
Interactie met een gevestigde gebonden service kan een `SecurityException` veroorzaken vanwege het afdwingen van het beleid in `Binder.onTransact`.

## <a name="telemetry"></a>Telemetrie

De Intune App SDK voor Android beheert niet de gegevensverzameling vanuit uw app. De toepassing Bedrijfsportal registreert standaard door het systeem gegenereerde gegevens. Deze gegevens worden naar Microsoft Intune verzonden. Conform het Microsoft-beleid worden er geen persoonsgegevens verzameld.

> [!NOTE]
> Als eindgebruikers ervoor kiezen deze gegevens niet te verzenden, moeten ze telemetrie uitschakelen onder Instellingen op de bedrijfsportal-app. Zie [Gegevensverzameling door Microsoft uitschakelen](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android) voor meer informatie. 

## <a name="recommended-android-best-practices"></a>Aanbevolen procedures voor Android

* Waar mogelijk, moeten alle bibliotheekprojecten hetzelfde android:package delen. Dit zal niet sporadisch mislukken tijdens de uitvoeringstijd. Het is puur een probleem dat zich voordoet tijdens het opbouwen. In nieuwere versies van de SDK voor de Intune-app, zal de redundantie deels worden verwijderd.

* Gebruik de nieuwste hulpprogramma's van de Android SDK-build.

* Verwijder alle overbodige en ongebruikte bibliotheken (bijvoorbeeld android.support.v4).

## <a name="testing"></a>Testen
Raadpleeg de [Testhandleiding](app-sdk-android-testing-guide.md).
