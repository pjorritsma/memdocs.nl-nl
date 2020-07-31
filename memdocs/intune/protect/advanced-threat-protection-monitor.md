---
title: Integratie van Microsoft Defender Advanced Threat Protection (ATP) bewaken in Microsoft Intune - Azure | Microsoft Docs
description: Integratie van Microsoft Defender Advanced Threat Protection (ATP) bewaken met Microsoft Intune, inclusief apparaatcompatibiliteit en onboardingstatus.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cedb255a575d4b6ea04dd684b5592748e63397c8
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264518"
---
# <a name="monitor-device-status-when-you-integrate-microsoft-defender-atp-with-intune"></a>Apparaatstatus bewaken wanneer u Microsoft Defender ATP integreert met Intune

Wanneer u Microsoft Intune en Microsoft Defender Advanced Threat Protection (ATP) integreert, kunt u informatie weergeven over apparaatcompatibiliteit en onboarding in het Microsoft Endpoint Manager-beheercentrum.

## <a name="monitor-device-compliance"></a>Apparaatcompatibiliteit bewaken

Bewaak vervolgens de status van apparaten die het nalevingsbeleid voor Microsoft Defender ATP hebben.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Bewaken** > **Beleidsnaleving**.

3. Zoek uw Microsoft Defender ATP-beleid in de lijst op en ga na welke apparaten conform of non-conform zijn.

U kunt vanaf dezelfde locatie ook het *operationele* rapport gebruiken voor niet-compatibele apparaten:

- Selecteer **Apparaten** > **Bewaken** > **Niet-compatibele apparaten**.

Zie [Intune-rapporten](../fundamentals/reports.md) voor meer informatie over rapporten.

## <a name="view-onboarding-status"></a>Status voor onboarding weergeven

Als u de status voor onboarding van uw door Intune beheerde apparaten wilt weergeven, gaat u naar **Eindpuntbeveiliging** > **Microsoft Defender ATP**. Op deze pagina kunt u ook een apparaatconfiguratieprofiel maken om meer apparaten naar Microsoft Defender ATP te onboarden.

## <a name="next-steps"></a>Volgende stappen

[Naleving voor Microsoft Defender ATP met voorwaardelijke toegang in Intune afdwingen](../protect/advanced-threat-protection.md)
