---
title: Instellingen voor schijfversleuteling tegen aanvallen beheren met eindpuntbeveiligingsbeleid in Microsoft Intune | Microsoft Docs
description: Configureer en implementeer beleidsregels voor apparaten die u beheert met eindpuntbeveiligingsinstellingen voor schijfversleutelingbeleid in Microsoft Endpoint Manager.
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
ms.openlocfilehash: 3e01e54eb6e74c8139c266d677a6406554119273
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972064"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Schijfversleutelingsbeleid voor eindpuntbeveiliging in Intune

De schijfversleutelingsprofielen voor eindpuntbeveiliging zijn alleen gericht op de instellingen die relevant zijn voor een ingebouwde versleutelingsmethode voor apparaten, zoals FileVault of BitLocker. Op deze manier kunnen beveiligingsbeheerders de instellingen voor schijfversleuteling eenvoudig beheren zonder door een massa niet-gerelateerde instellingen te hoeven navigeren.

Hoewel u dezelfde apparaatinstellingen kunt configureren met behulp van *Endpoint Protection*-apparaatconfiguratieprofielen, bevatten de apparaatconfiguratieprofielen aanvullende categorieën instellingen. Deze extra instellingen zijn niet gerelateerd aan schijfversleuteling en kunnen de taak voor het configureren van alleen schijfversleuteling voor uw omgeving bemoeilijken.

U vindt het eindpuntbeveiligingsbeleid voor schijfversleuteling onder *Beheren* in het knooppunt **Eindpuntbeveiliging** van het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

## <a name="prerequisites-for-disk-encryption-policy"></a>Vereisten voor het beleid voor schijfversleuteling

- **macOs**: macOS 10.13 of hoger
- **Windows**: Windows 10 of hoger

## <a name="disk-encryption-profiles"></a>Schijfversleutelingprofielen

**macOS-profielen**:

- **FileVault** - FileVault biedt ingebouwde volledige schijfversleuteling voor macOS-apparaten.

  [FileVault-instellingen](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) voor macOS beheren.

  Zie [FileVault-schijfversleuteling voor macOS gebruiken](../protect/encrypt-devices-filevault.md) om een FileVault-profiel te maken.

**Windows 10-profielen**:

- **BitLocker** - BitLocker-stationsversleuteling is een functie voor gegevensbescherming die is geïntegreerd met het besturingssysteem en die beschermt tegen de bedreigingen van diefstal of blootstelling van gegevens als een computer kwijtraakt, wordt gestolen of niet volgens de voorschriften buiten bedrijf wordt gesteld

  [BitLocker-instellingen](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) voor Windows 10 beheren.

  Zie [BitLocker-schijfversleuteling voor Windows 10 gebruiken](../protect/encrypt-devices.md) voor het maken van een BitLocker-profiel.

## <a name="manage-device-encryption"></a>Versleuteling van apparaat beheren

Nadat u het beleid voor het versleutelen van een schijf hebt geïmplementeerd, raadpleegt u de volgende artikelen voor meer informatie over het beheren van versleuteling:

- [BitLocker beheren](../protect/encrypt-devices.md#manage-bitlocker)
- [FileVault beheren](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Apparaatversleuteling controleren](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Volgende stappen

- [Een FileVault-profiel maken](../protect/encrypt-devices-filevault.md#create-endpoint-security-policy-for-filevault)
- [Een BitLocker-profiel maken](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
