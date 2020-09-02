---
title: Instellingen voor accountbeveiliging tegen aanvallen beheren met eindpuntbeveiligingsbeleid in Microsoft Intune | Microsoft Docs
description: Configureer en implementeer beleidsregels voor apparaten die u beheert met eindpuntbeveiligingsinstellingen voor accountbeveiligingsbeleid in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f08282fe6bd8675474415290d50c0b07b4e1fc25
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915055"
---
# <a name="account-protection-policy-for-endpoint-security-in-intune"></a>Accountbeveiligingsbeleid voor eindpuntbeveiliging in Intune

Gebruik eindpuntbeveiligingsbeleid van Intune voor accountbeveiliging om de identiteit en accounts van uw gebruikers te beschermen. Het accountbeveiligingsbeleid is gericht op instellingen voor Windows Hello en Credential Guard, dat deel uitmaakt van de Windows-functionaliteit voor identiteits- en toegangsbeheer.

- *Windows Hello voor Bedrijven* vervangt wachtwoorden door een krachtige tweeledige verificatiemethode op pc's en mobiele apparaten.
- *Credential Guard* helpt bij het beveiligen van referenties en geheimen die u gebruikt voor de apparaten.

Zie [Identiteits- en toegangsbeheer](/windows/security/identity-protection/) in de documentatie voor identiteits- en toegangsbeheer van Windows voor meer informatie.

U kunt het eindpuntbeveiligingsbeleid vinden bij Accountbeveiliging onder *Beheren* in het knooppunt **Eindpuntbeveiliging** van het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

Bekijk de [instellingen voor accountbeveiligingsprofielen](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-account-protection-profiles"></a>Vereisten voor accountbeveiligingsprofielen

- Windows 10 of hoger

## <a name="account-protection-profiles"></a>Accountbeveiligingsprofielen

*Accountbeveiligingsprofielen zijn beschikbaar als preview-versie*.

**Windows 10-profielen**:

- **Accountbeveiliging** *(preview)* : instellingen voor accountbeveiligingsbeleid waarmee u gebruikersreferenties kunt beschermen.

## <a name="next-steps"></a>Volgende stappen

[Eindpuntbeveiligingsbeleid configureren](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)