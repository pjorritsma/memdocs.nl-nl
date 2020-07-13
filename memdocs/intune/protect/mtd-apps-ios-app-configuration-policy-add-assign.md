---
title: MTD-apps toevoegen en toewijzen aan Microsoft Intune
titleSuffix: Microsoft Intune
description: Gebruik Intune om Mobile Thread Defense (MTD)-apps, de Microsoft Authenticator-app en het iOS-configuratiebeleid toe te voegen in Azure Portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 00356258-76a8-4a84-9cf5-64ceedb58e72
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4782c2a8f2c8791929ca4e585dab96031bf550fa
ms.sourcegitcommit: f999131e513d50967f88795e400d5b089ebc5878
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85914618"
---
# <a name="add-and-assign-mobile-threat-defense-mtd-apps-with-intune"></a>MTD-apps (Mobile Threat Defense) toevoegen en toewijzen met Intune

U kunt Intune gebruiken om MTD-apps (Mobile Threat Defense) toe te voegen en te implementeren. Eindgebruikers kunnen dan meldingen ontvangen wanneer op hun mobiele apparaten een bedreiging wordt vastgesteld en ze kunnen richtlijnen ontvangen om de bedreigingen te verhelpen.

> [!NOTE]
> Dit artikel is van toepassing op alle Mobile Threat Defense-partners.

## <a name="before-you-begin"></a>Voordat u begint

Voer de volgende stappen in Intune uit: Zorg ervoor dat u bekend bent met de volgende procedures:

- [Een app toevoegen in Intune](../apps/apps-add.md).
- [Een configuratiebeleid voor iOS-apps toevoegen in Intune](../apps/app-configuration-policies-use-ios.md).
- [Een app toewijzen met Intune](../apps/apps-deploy.md).

> [!TIP]
> De Intune-bedrijfsportal werkt als de broker op Android-apparaten, zodat de identiteit van gebruikers kan worden gecontroleerd door Azure AD.

## <a name="configure-microsoft-authenticator-for-ios"></a>Microsoft Authenticator voor iOS configureren

Voor iOS-apparaten hebt u de app [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) nodig, zodat de identiteit van gebruikers kan worden gecontroleerd door Azure AD. Bovendien hebt u een configuratiebeleid voor iOS-apps nodig, waarmee wordt bepaald welke MTD iOS-app moet worden gebruikt met Intune.

Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de App Store voor Microsoft Authenticator](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) wanneer u **App-gegevens** configureert.

## <a name="configure-your-mtd-apps-with-an-app-configuration-policy"></a>MTD-apps configureren met configuratiebeleid voor apps

De MTD-apps (Mobile Threat Defense) op met MDM beheerde apparaten maken gebruik van app-configuratie om de onboarding van gebruikers te vereenvoudigen. Voor niet-ingeschreven apparaten is app-configuratie op basis van MDM niet beschikbaar. Raadpleeg in dit geval [Mobile Threat Defense-apps toevoegen aan niet-ingeschreven apparaten](../protect/mtd-add-apps-unenrolled-devices.md).

### <a name="lookout-for-work-app-configuration-policy"></a>Beleid voor de configuratie van Lookout for Work-apps

Maak het configuratiebeleid voor iOS-apps volgens de instructies in het artikel [using iOS app configuration policy](../apps/app-configuration-policies-use-ios.md) (App-configuratiebeleid voor iOS gebruiken).

### <a name="sep-mobile-app-configuration-policy"></a>Beleid voor de configuratie van SEP Mobile-apps

Gebruik hetzelfde Azure AD-account dat eerder is geconfigureerd in de [Symantec Endpoint Protection-beheerconsole](https://aad.skycure.com). Dit moet hetzelfde account zijn als het account waarmee u zich hebt aangemeld bij Intune.

- **Download** het configuratiebeleidsbestand voor de iOS-app:
  - Ga naar de [Symantec Endpoint Protection Mobile-beheerconsole](https://aad.skycure.com) en meld u aan met uw beheerdersreferenties.

  - Ga naar **Instellingen** en kies onder **Integraties** de optie **Intune**. Kies **EMM Integration Selection**. Kies **Microsoft** en sla uw selectie vervolgens op.

  - Klik op de koppeling voor de **installatiebestanden voor de integratie** en sla het gegenereerde bestand \*.zip op. Het .zip-bestand bevat het bestand * **.plist** waarmee het configuratiebeleid voor de iOS-app wordt gemaakt in Intune.

  - Zie de Engelstalige instructies voor het [gebruiken van app-configuratiebeleid voor iOS van Microsoft Intune](../apps/app-configuration-policies-use-ios.md) om het configuratiebeleid voor de iOS-app SEP Mobile toe te voegen.

    - Selecteer voor **Indeling van de configuratie-instellingen** de optie **XML-gegevens invoeren**, kopieer de inhoud van het bestand * **.plist** en plak de inhoud in de hoofdtekst van het configuratiebeleid.

> [!NOTE]
> Neem contact op met [Symantec Endpoint Protection Mobile Enterprise-ondersteuning](https://support.symantec.com/en_US/contact-support.html) als u de bestanden niet kunt ophalen.

### <a name="check-point-sandblast-mobile-app-configuration-policy"></a>Configuratiebeleid voor Check Point SandBlast Mobile-apps

Zie de Engelstalige instructies voor het [gebruiken van app-configuratiebeleid voor iOS van Microsoft Intune](../apps/app-configuration-policies-use-ios.md) om het configuratiebeleid voor de iOS-app Check Point SandBlast Mobile toe te voegen.

- Selecteer voor **Indeling van de configuratie-instellingen** de optie **XML-gegevens invoeren**, kopieer de volgende inhoud en plak de inhoud in de hoofdtekst van het configuratiebeleid.

  `<dict><key>MDM</key><string>INTUNE</string></dict>`


### <a name="zimperium-app-configuration-policy"></a>Configuratiebeleid voor Zimperium-apps

Zie de Engelstalige instructies voor het [gebruiken van app-configuratiebeleid voor iOS van Microsoft Intune](../apps/app-configuration-policies-use-ios.md) om het configuratiebeleid voor de iOS-app Zimperium toe te voegen.

- Selecteer voor **Indeling van de configuratie-instellingen** de optie **XML-gegevens invoeren**, kopieer de volgende inhoud en plak de inhoud in de hoofdtekst van het configuratiebeleid.

   ```
   <dict>
   <key>provider</key><string>Intune</string>
   <key>userprincipalname</key><string>{{userprincipalname}}</string>
   <key>deviceid</key>
   <string>{{deviceid}}</string>
   <key>serialnumber</key>
   <string>{{serialnumber}}</string>
   <key>udidlast4digits</key>
   <string>{{udidlast4digits}}</string>
   </dict>
   ```

### <a name="pradeo-app-configuration-policy"></a>Configuratiebeleid voor Pradeo-apps

Pradeo biedt geen ondersteuning voor toepassingsconfiguratiebeleid in iOS/iPadOS.  Als u een geconfigureerde app wilt krijgen, moet u in plaats daarvan Pradeo gebruiken om aangepaste IPA- of APK-bestanden te implementeren die al vooraf zijn geconfigureerd met de gewenste instellingen.

### <a name="better-mobile-app-configuration-policy"></a>Configuratiebeleid voor Better Mobile-apps

Zie de Engelstalige instructies voor het [gebruiken van app-configuratiebeleid voor iOS van Microsoft Intune](../apps/app-configuration-policies-use-ios.md) om het configuratiebeleid voor de iOS-app Better Mobile toe te voegen.

- Selecteer voor **Indeling van de configuratie-instellingen** de optie **XML-gegevens invoeren**, kopieer de volgende inhoud en plak de inhoud in de hoofdtekst van het configuratiebeleid. Vervang de `https://client.bmobi.net` URL dor de juiste console-URL.

   ```
    <dict>
   <key>better_server_url</key>
   <string>https://client.bmobi.net</string>
   <key>better_udid</key>
   <string>{{aaddeviceid}}</string>
   <key>better_user</key>
   <string>{{userprincipalname}}</string>
   </dict>
   ```

### <a name="sophos-mobile-app-configuration-policy"></a>Configuratiebeleid voor Sophos Mobile-apps

Maak het configuratiebeleid voor iOS-apps volgens de instructies in het artikel [using iOS app configuration policy](../apps/app-configuration-policies-use-ios.md) (App-configuratiebeleid voor iOS gebruiken). Zie [Sophos Intercept X for Mobile iOS - Available managed settings](https://community.sophos.com/kb/133963) (Sophos Intercept X voor Mobile iOS - beschikbare beheerde instellingen) in de kennisbank van Sophos voor meer informatie.

### <a name="wandera-app-configuration-policy"></a>Configuratiebeleid voor Wandera-app

> [!NOTE]
> Gebruik voor de eerste test een testgroep wanneer u gebruikers en apparaten toevoegt in de sectie Toewijzingen van het configuratiebeleid. 

- **Android**
  - Bekijk de instructies voor het [gebruik van app-configuratiebeleid voor Android van Microsoft Intune](../apps/app-configuration-policies-use-android.md) om het configuratiebeleid voor de Wandera Android-app toe te voegen, wanneer u hierom wordt gevraagd, met behulp van de informatie hieronder.

1. Klik in de **RADAR Wandera-portal** op de knop **Toevoegen** onder de indeling van de **Configuratie-instellingen**.
2. Selecteer **Activeringsprofiel-URL** in de lijst met **Configuratiesleutels**. Klik op **OK**.
3. Selecteer voor **Activeringsprofiel-URL** de **tekenreeks** uit het menu **Waardetype**. Kopieer vervolgens de **URL voor deelbare koppeling** uit het gewenste activeringsprofiel in RADAR.
4. Selecteer in de **gebruikersinterface van de Intune-beheerconsole-app** **Instellingen**, definieer **Configuratie-instellingenindeling > Configuration Designer gebruiken** en plak de **deelbare URL**.  

> [!NOTE] 
> In tegenstelling tot bij iOS moet u uniek configuratiebeleid voor de Android Enterprise-app definiëren voor elk Wandera-activeringsprofiel. Als u niet meerdere Wandera-activeringsprofielen nodig hebt, kunt u één Android-app-configuratie gebruiken voor alle doelapparaten. Als u activeringsprofielen maakt in Wandera, moet u ervoor zorgen dat u Azure Active Directory selecteert onder de configuratie voor de gekoppelde gebruiker om er zeker van te zijn dat het apparaat in Wandera kan worden gesynchroniseerd met Intune via UEM Connect.

- **iOS**
  - Bekijk de instructies voor het [gebruik van app-configuratiebeleid voor iOS van Microsoft Intune](../apps/app-configuration-policies-use-ios.md) om het configuratiebeleid voor de Wandera iOS-app toe te voegen, wanneer u hierom wordt gevraagd, met behulp van de informatie hieronder.

1. Ga in de **RADAR Wandera-portal** naar **Apparaten > Activeringen** en selecteer een activeringsprofiel. Klik op **Implementatiestrategieën > Beheerde apparaten > Microsoft Intune** en zoek de **Configuratie-instellingen voor iOS-apps**.  
2. Vouw het vak uit om de configuratie-XML voor de iOS-app weer te geven en kopieer deze op het systeemklembord.  
3. Definieer in de **instellingen voor de gebruikersinterface van de Intune-beheerconsole-app** **Configuratie-instellingenindeling > XML-gegevens invoeren**. 
4. Plak de XML in het tekstvak voor de app-configuratie.

> [!NOTE]
> U kunt één iOS-configuratiebeleid gebruiken op alle apparaten die moeten worden ingericht met Wandera.  

## <a name="assigning-mobile-threat-defense-apps-to-end-users-via-intune"></a>Mobile Threat Defense-apps toewijzen aan eindgebruikers via Intune

Als u de Mobile Threat Defense-app wilt installeren op het apparaat van de eindgebruiker, volgt u onderstaande stappen in de Azure-portal. Zorg ervoor dat u bekend bent met de volgende procedures:

- [Apps toewijzen aan groepen met Intune](../apps/apps-deploy.md)

Kies de sectie die overeenkomt met uw MTD-provider:

- [Lookout for Work](#assigning-lookout-for-work)
- [SEP Mobile (Symantec Endpoint Protection Mobile)](#assigning-symantec-endpoint-protection-mobile)
- [Check Point SandBlast Mobile](#assigning-check-point-sandblast-mobile)
- [Zimperium](#assigning-zimperium)
- [Pradeo](#assigning-pradeo)
- [Better Mobile](#assigning-better-mobile)
- [Sophos Mobile](#assigning-sophos)
- [Wandera](#assigning-wandera)

### <a name="assigning-lookout-for-work"></a>Lookout for Work Toewijzen

- **Android**
  - Zie de instructies in het artikel [Android Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-android.md). Gebruik deze [URL voor Lookout for Work in Google Play](https://play.google.com/store/apps/details?id=com.lookout.enterprise) voor de **URL App Store**.

- **iOS**
  - Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de iTunes Store voor Lookout for Work](https://itunes.apple.com/us/app/lookout-for-work/id997193468?mt=8) voor de **URL App Store**.

- **Lookout for Work-app buiten de Apple Store**
  - U moet de Lookout for Work-app voor iOS opnieuw ondertekenen. De Lookout for Work-app voor iOS wordt gedistribueerd buiten de iOS App Store. Voordat u de app distribueert, moet u de app opnieuw ondertekenen met het iOS Enterprise Developer-certificaat.  
  - Zie het [proces voor het opnieuw ondertekenen van Lookout for Work-apps voor iOS](https://personal.support.lookout.com/hc/articles/114094038714) (Engelstalig) op de website van Lookout voor gedetailleerde instructies voor het opnieuw ondertekenen van Lookout for Work-apps voor iOS.

  - **Azure AD-verificatie inschakelen voor gebruikers van de iOS-app Lookout for Work**

    1. Ga naar [Azure Portal](https://portal.azure.com), meld u aan en navigeer naar de toepassingspagina.

    2. Voeg de **Lookout for Work-app voor iOS** toe als een **native clienttoepassing**.

    3. Vervang **com.lookout.enterprise.yourcompanyname** door de klantbundel-id die u hebt geselecteerd bij het ondertekenen van de IPA.

    4. Voeg de aanvullende omleidings-URI **&lt;companyportal://code/>** toe, gevolgd door een versie met URL-codering van uw oorspronkelijke omleidings-URI.

    5. Voeg **overgedragen machtigingen** toe aan uw app.

    > [!NOTE]
    > Zie voor meer informatie de Engelstalige instructies voor het [configureren van een native clienttoepassing met Azure AD](https://azure.microsoft.com/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).

  - **Het IPA-bestand van Lookout for Work toevoegen.**

    - Upload het opnieuw ondertekende IPA-bestand, volgens de instructies in het artikel [iOS-Line-Of-Business-apps (LOB) toevoegen aan Microsoft Intune](../apps/lob-apps-ios.md). U moet ook de minimale versie van het besturingssysteem instellen op iOS 8.0 of hoger.

### <a name="assigning-symantec-endpoint-protection-mobile"></a>Symantec Endpoint Protection Mobile toewijzen

- **Android**
  - Zie de instructies in het artikel [Android Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-android.md). Gebruik deze [URL voor de App Store voor SEP Mobile](https://play.google.com/store/apps/details?id=com.skycure.skycure) voor de **URL App Store**.  Selecteer **Android 4.0 (Ice Cream Sandwich)** voor de **minimale versie van het besturingssysteem**.

- **iOS**
  - Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de App Store voor SEP Mobile](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) voor de **URL App Store**.

### <a name="assigning-check-point-sandblast-mobile"></a>Check Point SandBlast Mobile toewijzen

- **Android**  
  - Zie de instructies in het artikel [Android Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-android.md). Gebruik deze [URL voor de App Store voor Check Point SandBlast](https://play.google.com/store/apps/details?id=com.lacoon.security.fox) voor de **URL App Store**.

- **iOS**
  - Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de App Store voor Check Point SandBlast](https://apps.apple.com/us/app/sandblast-mobile-protect/id1006390797) voor de **URL App Store**.  

### <a name="assigning-zimperium"></a>Zimperium toewijzen

- **Android**
  - Zie de instructies in het artikel [Android Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-android.md). Gebruik deze [URL voor de App Store voor Zimperium](https://play.google.com/store/apps/details?id=com.zimperium.zips&hl=en) voor de **URL App Store**.

- **iOS**
  - Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de App Store voor Zimperium](https://itunes.apple.com/us/app/zimperium-zips/id1030924459?mt=8) voor de **URL App Store**.  
 
### <a name="assigning-pradeo"></a>Pradeo toewijzen

- **Android**
  - Zie de instructies in het artikel [Android Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-android.md). Gebruik deze [URL voor de App Store voor Pradeo](https://play.google.com/store/apps/details?id=net.pradeo.service&hl=en_US) voor de **URL App Store**.

- **iOS**
  - Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de App Store voor Pradeo](https://itunes.apple.com/us/app/pradeo-agent/id547979360?mt=8) voor de **URL App Store**.

### <a name="assigning-better-mobile"></a>Better Mobile toewijzen

- **Android**
  - Zie de instructies in het artikel [Android Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-android.md). Gebruik deze [URL voor de App Store voor Active Shield](https://play.google.com/store/apps/details?id=com.better.active.shield.enterprise) voor de **URL App Store**.

- **iOS**
  - Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de App Store voor Active Shield](https://itunes.apple.com/us/app/activeshield/id980234260?mt=8&uo=4) voor de **URL App Store**.

### <a name="assigning-sophos"></a>Sophos toewijzen

- **Android**
  - Zie de instructies in het artikel [Android Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-android.md). Gebruik deze [URL voor de App Store voor Sophos](https://play.google.com/store/apps/details?id=com.sophos.smsec) voor de **URL App Store**.

- **iOS**
  - Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de App Store voor Active Shield](https://itunes.apple.com/us/app/sophos-mobile-security/id1086924662?mt=8) voor de **URL App Store**.

### <a name="assigning-wandera"></a>Wandera toewijzen

- **Android**
  - Zie de instructies in het artikel [Android Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-android.md). Gebruik deze [URL voor de mobiele app-store van Wandera](https://play.google.com/store/apps/details?id=com.wandera.android) voor de **URL App Store**. Selecteer **Android 5.0**  voor de **minimale versie van het besturingssysteem**.

- **iOS**
  - Zie de instructies in het artikel [iOS Store-apps toevoegen aan Microsoft Intune](../apps/store-apps-ios.md). Gebruik deze [URL voor de mobiele app-store van Wandera](https://itunes.apple.com/app/wandera/id605469330) voor de **URL App Store**.

## <a name="next-steps"></a>Volgende stappen

- [Het nalevingsbeleid voor MTD-apparaten configureren](mtd-device-compliance-policy-create.md)
