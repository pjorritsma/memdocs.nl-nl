---
title: Kioskinstellingen voor Windows Holographic for Business in Microsoft Intune - Azure | Microsoft Docs
description: Configureer uw Windows Holographic for Business-apparaten als kiosken voor één app en voor meerdere apps, pas het menu Start aan, voeg apps toe, geef de taakbalk weer, en configureer een webbrowser in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8127281069ce4209adfc2aec82a93f5a60669307
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911859"
---
# <a name="windows-holographic-for-business-device-settings-to-run-as-a-kiosk-in-intune"></a>Instellingen voor Windows Holographic for Business-apparaten om ze als kiosk uit te voeren via Intune

Op apparaten met Windows Holographic for Business kunt u configureren dat deze apparaten worden uitgevoerd in de kioskmodus met één app of in de kioskmodus met meerdere apps. Sommige functies worden niet ondersteund in Windows Holographic for Business.

Dit artikel bevat een overzicht en beschrijving van de verschillende instellingen die u kunt beheren op apparaten met Windows Holographic for Business. Gebruik deze instellingen voor het configureren van apparaten met Windows Holographic zodat ze in de kioskmodus worden uitgevoerd, als onderdeel van uw MDM-oplossing (Mobile Device Management).

Als Intune-beheerder kunt u deze instellingen maken en toewijzen aan uw apparaten.

Zie voor meer informatie over de Windows-kioskfunctie in Intune [Configure kiosk settings](kiosk-settings.md) (Kioskinstellingen configureren).

## <a name="before-you-begin"></a>Voordat u begint

- [Een configuratieprofiel voor een Windows 10-kioskapparaat maken](kiosk-settings.md#create-the-profile).

  Wanneer u een configuratieprofiel voor een Windows 10-kioskapparaat maakt, zijn er meer instellingen dan in dit artikel worden vermeld. De instellingen in dit artikel worden ondersteund op apparaten met Windows Holographic for Business.

- Dit kioskprofiel is direct gerelateerd aan het apparaatbeperkingsprofiel dat u maakt met behulp van de [Windows Edge kioskinstellingen](device-restrictions-windows-holographic.md#microsoft-edge-browser). Samenvatting:

  1. Maak dit kioskprofiel om het apparaat in de kioskmodus uit te voeren.
  2. Maak het [apparaatbeperkingsprofiel](device-restrictions-windows-holographic.md#microsoft-edge-browser) en configureer specifieke functies en instellingen die zijn toegestaan in Microsoft Edge.

> [!IMPORTANT]
> Zorg ervoor dat u dit kioskprofiel toewijst aan de dezelfde apparaten als uw [Microsoft Edge-profiel](device-restrictions-windows-holographic.md#microsoft-edge-browser).

## <a name="single-app-full-screen-kiosk"></a>Kiosk met één app, in volledige schermweergave

Hiermee wordt slechts één app op het apparaat uitgevoerd. Wanneer de gebruiker zich aanmeldt, wordt een specifieke app gestart. Deze modus voorkomt ook dat de gebruiker nieuwe apps kan openen of de actieve app kan wijzigen.

- **Aanmeldingstype gebruiker**: Selecteer het accounttype waarmee de app wordt uitgevoerd. Uw opties zijn:

  - **Automatisch aanmelden (Windows 10 versie 1803 en hoger)** : Niet ondersteund in Windows Holographic for Business.
  - **Lokaal gebruikersaccount**: Voeg het lokale (op het apparaat) gebruikersaccount toe. Of voeg een aan de kioskapp gekoppeld Microsoft-account (MSA) toe. Met het account dat u invoert, kunt u zich aanmelden bij de kiosk.

    Voor kiosken in openbare omgevingen moet een gebruikerstype met de minste bevoegdheid worden gebruikt.

- **Toepassingstype**: Selecteer **Store-app toevoegen**.

  - **App uitvoeren in kioskmodus**: Selecteer een app uit de lijst.

    Worden er geen apps in de lijst weergegeven? Voeg er een aantal toe met behulp van de stappen in [Client-apps](../apps/apps-add.md).

## <a name="multi-app-kiosk"></a>Kiosk voor meerdere apps

Apps in deze modus zijn beschikbaar in het startmenu. Deze apps zijn de enige apps die de gebruiker kan openen. Als een app een afhankelijkheid van een andere app heeft, moeten beide worden opgenomen in de lijst met toegestane apps.

- **Gericht op Windows 10-apparaten in de S-modus**: Selecteer **Nee**. De S-modus wordt niet ondersteund in Windows Holographic for Business.

- **Aanmeldingstype gebruiker**: Voer een of meer gebruikersaccounts in die de apps kunnen gebruiken die u toevoegt. Uw opties zijn:

  - **Automatisch aanmelden (Windows 10 versie 1803 en hoger)** : Niet ondersteund in Windows Holographic for Business.
  - **Lokale gebruikersaccounts**: **Voeg** het lokale (op het apparaat) gebruikersaccount toe. Met het account dat u invoert, kunt u zich aanmelden bij de kiosk.
  - **Azure AD-gebruiker of -groep (Windows 10, versie 1803 of hoger)** : Hiervoor zijn gebruikersreferenties voor aanmelding op het apparaat vereist. Selecteer **Toevoegen** als u Azure AD-gebruikers of -groepen in de lijst wilt kiezen. U kunt meerdere gebruikers en groepen selecteren. Kies **Selecteren** om uw wijzigingen op te slaan.
  - **HoloLens-bezoeker**: Het bezoekersaccount is een gastaccount waarvoor geen gebruikersreferenties zijn of verificatie is vereist, zoals wordt beschreven in [Gedeelde pc-modusconcepten](/windows/configuration/set-up-shared-or-guest-pc#shared-pc-mode-concepts).

- **Browser en apps**: Voeg de apps toe die u op het apparaat in kioskmodus wilt uitvoeren. U kunt verschillende apps toevoegen.

  - **Browsers**
    - **Microsoft Edge toevoegen**: Microsoft Edge wordt toegevoegd aan het app-raster en alle apps kunnen in deze kiosk worden uitgevoerd. Selecteer het Microsoft Edge-kioskmodustype:

      - **Normale modus (volledige versie van Microsoft Edge)** : Er wordt een volledige versies van Microsoft Edge uitgevoerd met alle browserfuncties. Gebruikersgegevens en -statussen worden tussen sessies opgeslagen.
      - **Openbaar bladeren (InPrivate)** : hiermee wordt een versie met meerdere tabbladen van Microsoft Edge InPrivate uitgevoerd met een op maat gemaakte toepassing voor kiosken die in volledige schermweergave worden uitgevoerd.

      Zie [Microsoft Edge-kioskmodus implementeren](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types) voor meer informatie over deze opties.

      > [!NOTE]
      > Via deze instelling schakelt u de Microsoft Edge-browser in op het apparaat. Als u specifieke Microsoft Edge-instellingen wilt configureren, maakt u een apparaatbeperkingsprofiel (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **Windows 10** voor platform > **Apparaatbeperkingen** > **Microsoft Edge-browser**). De beschikbare Holographic for Business-instellingen worden in de [Microsoft Edge-browser](device-restrictions-windows-holographic.md#microsoft-edge-browser) vermeld en beschreven.

    - **Kiosk-browser toevoegen**: Niet ondersteund in Windows Holographic for Business.

  - **Toepassingen**
    - **Store-app toevoegen**: Selecteer een bestaande app die u aan Intune hebt toegevoegd of geïmplementeerd als [client-apps](../apps/apps-add.md), waaronder Line-Of-Business-apps. Als er geen apps worden weergegeven, biedt Intune ondersteuning voor veel [app-typen](../apps/apps-add.md) die u [aan Intune toevoegt](../apps/store-apps-windows.md).
    - **Win32-app toevoegen**: Niet ondersteund in Windows Holographic for Business.
    - **Toevoegen via AUMID**: Gebruik deze optie om Postvak IN-apps voor Windows, zoals Kladblok of Calculator toe te voegen. Voer de volgende eigenschappen in:

      - **Toepassingsnaam**: Vereist. Geef een naam op voor de toepassing.
      - **Model-id van toepassingsgebruiker (AUMID)** : Vereist. Voer de AUMID van de Windows-app in. Zie [De model-id van toepassingsgebruiker van een geïnstalleerde app vinden](/windows-hardware/customize/enterprise/find-the-application-user-model-id-of-an-installed-app) als u wilt weten hoe u aan deze id komt.

    - **AutoLaunch**: Optioneel. Nadat u uw apps en browser hebt toegevoegd, selecteert u één app of browser die automatisch moet worden geopend wanneer de gebruiker zich aanmeldt. Er kan slechts één app of browser automatisch worden gestart.
    - **Tegelgrootte**: Vereist. Nadat u uw apps hebt toegevoegd, selecteert u een kleine, middelgrote, brede of grote app-tegelgrootte.

- **Alternatieve indeling van het menu Start gebruiken**: Selecteer **Ja** om een XML-bestand op te geven waarin wordt beschreven hoe de apps worden weergegeven in het menu Start, zoals de volgorde van de apps. Gebruik deze optie als u meer aanpassingsmogelijkheden wilt gebruiken in het startmenu. [Startopmaak aanpassen en exporteren](/hololens/hololens-kiosk#start-layout-for-hololens) biedt instructies en bevat een specifiek XML-bestand voor apparaten met Windows Holographic for Business.

- **Windows-taakbalk**: Niet ondersteund in Windows Holographic for Business.
- **Toegang tot de map Downloads toestaan**: Niet ondersteund in Windows Holographic for Business.
- **Onderhoudsvenster opgeven voor opnieuw opstarten van apps**: Niet ondersteund in Windows Holographic for Business.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook kioskprofielen maken voor apparaten met [Android ](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience) en [Windows 10 en hoger](kiosk-settings-windows.md).