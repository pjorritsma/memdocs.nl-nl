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
ms.openlocfilehash: a5f479dcad0c293c547edec24f0f835a4fc987e1
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574827"
---
# <a name="unlicensed-admins"></a>Beheerders zonder licentie

> [!Important]
> Met deze optie wordt alleen de licentievereiste voor beheerders verwijderd voor toegang tot Microsoft Endpoint Manager. Voor het gebruik van andere functies of services, zoals Azure Active Directory Premium, kan nog steeds een licentie voor de beheerder zijn vereist.

U kunt het beheercentrum voor Intune/Microsoft Endpoint Manager toegang verlenen tot beheerders zonder intune-licenties.

1. Meld u aan bij [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenantbeheer** > **Rollen** > **Beheerderslicenties**.
2. Kies **Toegang verlenen aan beheerders zonder licentie** > **Ja**.
    >[!WARNING]
    >U kunt deze instelling niet ongedaan maken nadat u op **Ja**hebt geklikt.

3. Vanaf nu is geen Intune-licentie vereist voor gebruikers die zich aanmelden bij het beheercentrum voor Microsoft Endpoint Manager. Het bereik van de toegang wordt gedefinieerd door de rollen die aan hen zijn toegewezen.

Intune biedt ondersteuning voor maximaal 350 beheerders zonder licentie per beveiligingsgroep en is alleen van toepassing op directe leden. Beheerders boven deze limiet zullen onvoorspelbaar gedrag ondervinden.




