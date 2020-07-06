---
title: Beperkingen voor apparaatinschrijving voor het configuratieframework voor beveiliging van Android Enterprise
titleSuffix: Microsoft Intune
description: Beperkingen voor apparaatinschrijving voor het configuratieframework voor beveiliging van Android Enterprise.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d26040c5a009a9c3877abbc25512e317f584f114
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502932"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Inschrijvingsbeperkingen voor Android Enterprise-apparaten

Voordat apparaten worden ingeschreven voor het [configuratieframework voor beveiliging van Android Enterprise]() moeten organisaties de juiste beperkingen configureren. Deze beperkingen zorgen ervoor dat gebruikers alleen het volgende kunnen inschrijven:
- goedgekeurde apparaten.
- een opgegeven aantal apparaten.
- apparaten met opgegeven platformen.
- apparaten met opgegeven besturingssystemen.
- apparaten van opgegeven fabrikanten.

Zie [Inschrijvingsbeperkingen instellen](enrollment-restrictions-set.md) voor meer informatie over de beperkingen voor apparaatinschrijving.

## <a name="work-profile-basic-level-1-security-restrictions"></a>Beperkingen voor standaardbeveiliging van werkprofielen (niveau 1)

Voor standaardbeveiliging voor Android Enterprise-werkprofielen (niveau 1) moeten de volgende apparaatbeperkingen worden geïmplementeerd:

| Type | Platform | Versie | Staat persoonlijke apparaten toe |
|--------|--------|--------|--------|
| Android Enterprise | Toestaan | Android 5.0 en hoger.<p>Microsoft raadt aan de minimale primaire versie van Android te configureren, zodat deze overeenkomt met de ondersteunde Android-versies voor Microsoft-apps. OEM's en apparaten die voldoen aan de aanbevolen Android Enterprise-vereisten, moeten ondersteuning bieden voor de release die nu wordt vrijgegeven + upgrade van één letter.   Op dit moment wordt Android 8.0 of hoger door Android aangeraden voor kennismedewerkers. Zie [Aanbevolen Android Enterprise-vereisten](https://www.android.com/enterprise/recommended/requirements/) voor meer informatie. | Ja |
| Android-apparaatbeheerder| Blokkeren | Alle versies | Ja |

## <a name="work-profile-high-level-3-security-restrictions"></a>Beperkingen voor hoge beveiliging van werkprofielen (niveau 3)
Voor hoge beveiliging voor Android Enterprise-werkprofielen (niveau 3) moeten de volgende apparaatbeperkingen worden geïmplementeerd:

| Type | Platform | Versie | Staat persoonlijke apparaten toe |
|--------|--------|--------|--------|
| Android Enterprise | Toestaan | Android 8.0 en hoger | Ja |
| Android-apparaatbeheerder| Blokkeren | Alle versies | Ja |

## <a name="fully-managed-security-restrictions"></a>Volledig beheerd: beveiligingsbeperkingen
Zorg ervoor dat de organisatie ondersteuning biedt voor de inschrijving van volledig beheerde Android Enterprise-apparaten, door de inschrijving van volledig beheerde Android Enterprise-apparaten te controleren. 

## <a name="next-steps"></a>Volgende stappen

[App-configuratiebeleid instellen](android-app-configuration-policies.md)
