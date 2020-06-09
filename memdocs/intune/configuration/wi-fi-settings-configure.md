---
title: Een Wi-Fi-profiel maken voor apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk de stappen voor het maken van een configuratieprofiel voor een Wi-Fi-apparaat in Microsoft Intune. Maak profielen voor Android-apparaatbeheer, Android Enterprise, Android kiosk, iOS/iPadOS, macOS, Windows 10 en hoger, en Windows Holographic for Business. Gebruik deze profielen voor het maken van een Wi-Fi-verbinding om certificaten te gebruiken, een EAP-type te kiezen, een verificatiemethode te selecteren, een proxy in te schakelen en meer.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca2a5ddd3d2b4c0aa93c7c955d0d688944ee8f95
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985511"
---
# <a name="add-and-use-wi-fi-settings-on-your-devices-in-microsoft-intune"></a>Wi-Fi-instellingen toevoegen en gebruiken op uw apparaten in Microsoft Intune

Wi-Fi is een draadloos netwerk dat door veel mobiele apparaten wordt gebruikt om toegang tot het netwerk te krijgen. Microsoft Intune omvat ingebouwde Wi-Fi-instellingen die kunnen worden geïmplementeerd voor gebruikers en apparaten in uw organisatie. Deze groep instellingen wordt een 'profiel' genoemd en kan worden toegewezen aan verschillende gebruikers en groepen. Wanneer het profiel is toegewezen, krijgen uw gebruikers toegang tot het Wi-Fi-netwerk van uw organisatie zonder dat zij dit zelf hoeven te configureren.

U installeert bijvoorbeeld een nieuw Wi-Fi-netwerk met de naam Contoso Wi-Fi. U wilt vervolgens alle iOS-/iPadOS-apparaten instellen om verbinding te maken met dit netwerk. Dit is het proces:

1. Maak een Wi-Fi-profiel met daarin de instellingen voor de verbinding met het draadloze netwerk Contoso Wi-Fi.
2. Wijs het profiel toe aan een groep die alle gebruikers van iOS-/iPadOS-apparaten omvat.
3. Gebruikers vinden het nieuwe Contoso Wi-Fi-netwerk in de lijst met draadloze netwerken op hun apparaat. Ze kunnen dan verbinding maken met het netwerk via de door u gekozen verificatiemethode.

In dit artikel worden de stappen vermeld voor het maken van een Wi-Fi-profiel. Het bevat ook koppelingen die de verschillende instellingen voor elk platform beschrijven.

## <a name="supported-device-platforms"></a>Ondersteunde apparaatplatformen

Wi-Fi-profielen ondersteunen de volgende apparaatplatformen:

- Android 5 en hoger
- Android Enterprise en kiosk
- iOS 11.0 en hoger
- iPadOS 13.0 en hoger
- macOS X 10.12 en hoger
- Windows 10 en hoger, Windows 10 Mobile en Windows Holographic for Business

> [!NOTE]
> Voor apparaten met Windows 8.1 kunt u een Wi-Fi-configuratie importeren die eerder vanaf een andere apparaat is geëxporteerd.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Kies het platform van uw apparaten. Uw opties zijn:

      - **Android-apparaatbeheerder**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 en hoger**
      - **Windows 8.1 en hoger**

    - **Profiel**: selecteer **Wi-Fi**.

      > [!TIP]
      >
      > - Voor **Android Enterprise**-apparaten die als een toegewezen apparaat (kiosk) worden uitgevoerd, kiest u **Alleen apparaateigenaar** > **Wi-Fi**.
      > - Voor **Windows 8.1 en hoger** kunt u **Wi-Fi importeren** kiezen. Met deze optie kunt u Wi-Fi-instellingen die u eerder vanaf een ander apparaat hebt geëxporteerd, importeren als een XML-bestand.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **Wi-Fi-profiel voor hele bedrijf**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Selecteer uw platform voor gedetailleerde instellingen:

    - [Android-apparaatbeheerder](wi-fi-settings-android.md)
    - [Android Enterprise](wi-fi-settings-android-enterprise.md), inclusief toegewezen apparaten
    - [iOS/iPadOS](wi-fi-settings-ios.md)
    - [macOS](wi-fi-settings-macos.md)
    - [Windows 10 en nieuwer](wi-fi-settings-windows.md)
    - [Instellingen voor Windows 8.1 en hoger](wi-fi-settings-import-windows-8-1.md), inclusief Windows Holographic for Business

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruiker of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

> [!TIP]
> Als u gebruikmaakt van verificatie op basis van certificaten voor uw Wi-Fi-profiel, implementeert u het Wi-Fi-profiel, het certificaatprofiel en het vertrouwde basisprofiel in dezelfde groepen om ervoor te zorgen dat elk apparaat de geldigheid van uw certificeringsinstantie kan herkennen.  Zie [Certificaten configureren met Microsoft Intune](../protect/certificates-configure.md) voor meer informatie.


## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt niets. Vervolgens moet u [dit profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

[Problemen met Wi-Fi-profielen in Intune](troubleshoot-wi-fi-profiles.md).
