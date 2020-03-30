---
title: Aangepaste apparaatinstellingen gebruiken in Microsoft Intune - Azure | Microsoft Docs
description: Maak een profiel of voeg een profiel toe om aangepaste instellingen te gebruiken voor apparaten met Windows 10 en hoger en Windows Phone-, Windows 8.1-, Android-apparaatbeheer-, Android Enterprise-, macOS- en iOS-/iPadOS-apparaten met Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6122f4624cc40152184c1c460afa6a7a39976063
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083987"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Een profiel maken met aangepaste instellingen in Intune

Microsoft Intune bevat veel ingebouwde instellingen om verschillende functies op een apparaat te beheren. U kunt ook aangepaste profielen maken, die vergelijkbaar zijn met ingebouwde profielen. Aangepaste profielen zijn ideaal wanneer u apparaatinstellingen en -functies wilt gebruiken die niet in Intune zijn ingebouwd. Deze profielen bevatten functies en instellingen die u op apparaten in uw organisatie kunt beheren. U kunt bijvoorbeeld een aangepast profiel maken waarmee u dezelfde functie voor elk iOS-/iPadOS-apparaat instelt.

Aangepaste instellingen worden voor elk platform anders geconfigureerd. Om bijvoorbeeld functies op Android- en Windows-apparaten te beheren, kunt u OMA-URI-waarden (Open Mobile Alliance Uniform Resource Identifier) opgeven. Voor Apple-apparaten kunt u een bestand importeren dat u met [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) of [Apple Profile Manager](https://support.apple.com/profile-manager) hebt gemaakt.

Zie [Wat zijn Microsoft Intune-apparaatprofielen?](device-profiles.md) voor meer informatie over configuratieprofielen.

In dit artikel wordt beschreven hoe u een aangepast profiel maakt voor Android-apparaatbeheer, Android Enterprise, iOS/iPadOS, macOS en Windows. U kunt ook alle beschikbare instellingen voor de verschillende platformen zien.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **Windows 10: Aangepast profiel waarmee aangepaste AllowVPNOverCellular OMA-URI** wordt ingeschakeld.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Selecteer het platform van uw apparaten. Uw opties zijn:

      - **Android-apparaatbeheerder**
      - **Android Enterprise**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 en hoger**
      - **Windows 8.1 en hoger**

    - **Profieltype**: Selecteer **Aangepast**.

4. De instellingen zijn verschillend voor elk platform. Om de instellingen voor een specifiek platform te bekijken, selecteert u uw platform:

    - [Android-apparaatbeheerder](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

5. Wanneer u klaar bent, selecteert u **Profiel maken** > **Maken**.

Het profiel wordt gemaakt en wordt weergegeven in de lijst met profielen (**Apparaatconfiguratie** > **Profielen**).

## <a name="next-steps"></a>Volgende stappen

Nadat het profiel is gemaakt, is het klaar om te worden toegewezen. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).
