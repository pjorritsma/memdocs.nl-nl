---
title: Windows 10 bijwerken en S-modusinstellingen in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk een lijst van alle instellingen en wat ze doen bij het bijwerken van een Windows 10-editie op een apparaat of schakel de S-modus in op een apparaat met een apparaatconfiguratieprofiel in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ab94c3cc8bb9009d49a6b301d9a67fa6ffc5f1a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364302"
---
# <a name="windows-10-and-newer-device-settings-to-upgrade-editions-or-enable-s-mode-in-intune"></a>Apparaatinstellingen voor Windows 10 (en hoger) om edities bij te werken of de S-modus in te schakelen in Intune

Microsoft Intune bevat veel instellingen waarmee u uw apparaten kunt beheren en beveiligen. In dit artikel worden de instellingen beschreven waarmee edities kunnen worden bijgewerkt en de S-modus kan worden ingeschakeld op apparaten met Windows 10. Deze instellingen worden gedefinieerd in een upgradeconfiguratieprofiel in Intune dat wordt gepusht naar of geïmplementeerd op apparaten.

Gebruik deze instellingen om de editie- en S-modusinstellingen van uw Windows 10-apparaten te beheren, als onderdeel van uw MDM-oplossing (Mobile Device Management).

Zie [Upgrade Windows 10 editions or enable S mode](edition-upgrade-configure-windows-10.md) (Windows 10-edities upgraden of S-modus inschakelen) voor meer informatie over deze functie.

## <a name="before-you-begin"></a>Voordat u begint

[Maak het profiel](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Editie-upgrade

- **Editie bijwerken naar**: Selecteer de Windows 10-editie waarnaar u upgradet. De apparaten waarop dit beleid is gericht, worden geüpgraded naar de door u gekozen editie.
- **Productsleutel**: Voer de productsleutel in die u hebt ontvangen van Microsoft. Nadat u het beleid met de productcode hebt gemaakt, kan de sleutel niet worden bijgewerkt en wordt deze uit veiligheidsoverwegingen verborgen. Als u de productcode wilt wijzigen, voert u de volledige code opnieuw in.
- **Licentiebestand**: Voor **Windows 10 Holographic for Business** of **Windows 10 Mobile-editie** kiest u **Bladeren** om het licentiebestand te selecteren dat u hebt ontvangen van Microsoft. Dit licentiebestand bevat licentiegegevens over de edities waarnaar u de apparaten upgradet.

## <a name="mode-switch"></a>Van modus wisselen

- **Geen configuratie**: Een S-modusapparaat blijft in de S-modus. Een eindgebruiker kan de S-modus op het apparaat uitschakelen.
- **In de S-modus blijven**: Hierdoor kan de eindgebruiker de S-modus op het apparaat niet uitschakelen.
- **Schakelen**: Hiermee wordt de S-modus op het apparaat uitgeschakeld.

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt mogelijk nog niets. Zorg ervoor dat u [het profiel toewijst](device-profile-assign.md) en [de status ervan controleert](device-profile-monitor.md).

U kunt ook editie-upgradeprofielen maken voor apparaten met [Windows Holographic for Business](holographic-upgrade.md).