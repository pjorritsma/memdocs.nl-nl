---
title: Beheerders zonder licentie in Microsoft Intune
description: Meer informatie over het verlenen van machtigingen voor niet-gelicentieerde beheerders voor toegang tot Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6dcd41377234bbb1b40e513f16c3393d763b17f
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088187"
---
# <a name="unlicensed-admins"></a>Beheerders zonder licentie

U kunt het beheercentrum voor Intune/Microsoft Endpoint Manager toegang verlenen tot beheerders zonder intune-licenties.

1. Meld u aan bij [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenantbeheer** > **Rollen** > **Beheerderslicenties**.
2. Kies **Toegang verlenen aan beheerders zonder licentie** > **Ja**.
    >[!WARNING]
    >U kunt deze instelling niet ongedaan maken nadat u op **Ja**hebt geklikt.

3. Vanaf nu is geen Intune-licentie vereist voor gebruikers die zich aanmelden bij het beheercentrum voor Microsoft Endpoint Manager. Het bereik van de toegang wordt gedefinieerd door de rollen die aan hen zijn toegewezen.

Intune biedt ondersteuning voor maximaal 350 beheerders zonder licentie per beveiligingsgroep en is alleen van toepassing op directe leden. Beheerders boven deze limiet zullen onvoorspelbaar gedrag ondervinden.




