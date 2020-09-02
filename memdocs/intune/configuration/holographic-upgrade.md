---
title: Een upgrade uitvoeren naar Windows Holographic for Business in Microsoft Intune - Azure | Microsoft Docs
description: Een upgrade uitvoeren naar Windows 10 Holographic for Business met behulp van een apparaatconfiguratieprofiel in Microsoft Intune.
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
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65a45b13a91671c1de9bcf04f23156d75313285f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907766"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Apparaten met Windows Holographic upgraden naar Windows Holographic for Business

Microsoft Intune bevat veel instellingen waarmee u uw apparaten kunt beheren en beveiligen. In dit artikel worden de instellingen beschreven waarmee u Windows Holographic-apparaten kunt upgraden naar Windows Holographic for Business.

Gebruik deze instellingen voor het upgraden van uw Windows Holographic-apparaten als onderdeel van uw MDM-oplossing (Mobile Device Management). Voor Microsoft HoloLens kunt u de Commercial Suite aanschaffen om de vereiste licentie voor de upgrade op te halen. Zie [Windows Holographic for Business-functies ontgrendelen](/hololens/hololens1-upgrade-enterprise) voor meer informatie.

Als Intune-beheerder kunt u deze instellingen maken en toewijzen aan uw apparaten.

Zie [Upgrade Windows 10 editions or enable S mode](edition-upgrade-configure-windows-10.md) (Windows 10-edities upgraden of S-modus inschakelen) voor meer informatie over deze functie.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een Windows 10-configuratieprofiel voor een editie-upgrade en modusschakelaar](edition-upgrade-configure-windows-10.md#create-the-profile).

Wanneer u een Windows 10-configuratieprofiel voor een editie-upgrade en modusschakelaar maakt, zijn er meer instellingen dan in dit artikel worden vermeld. De instellingen in dit artikel worden ondersteund op apparaten met Windows Holographic for Business.

## <a name="edition-upgrade"></a>Editie-upgrade

- **Editie bijwerken naar**: selecteer **Windows 10 Holographic for Business**.
- **Licentiebestand**: blader naar het XML-licentiebestand dat u hebt gekregen en selecteer dit bestand.

  :::image type="content" source="./media/holographic-upgrade/Holographic-edition-upgrade.png" alt-text="Voer in Intune de naam van het XML-bestand in dat de gegevens over de licentie voor Holographic for Business bevat.":::

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook editie-upgradeprofielen maken voor apparaten met [Windows 10 en hoger](edition-upgrade-windows-settings.md).