---
title: Configuratiebeleid voor beveiliging van Android Enterprise
titleSuffix: Microsoft Intune
description: Krijg meer informatie over de beperkingen en instellingen die zijn voorgesteld voor standaardbeveiliging en hoge beveiliging voor Android Enterprise-apparaten.
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
ms.openlocfilehash: 3735a37d4572454968638d29ab2646d6fda943ad
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546583"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>App-configuratiebeleid voor het configuratieframework voor beveiliging van Android Enterprise

Als onderdeel van het [configuratieframework voor beveiliging van Android Enterprise](android-configuration-framework.md) moet u het app-configuratiebeleid voor Android Enterprise-apparaten juist instellen.

Android Enterprise-apparaten met werkprofiel zijn ontworpen om zakelijke en persoonlijke gegevens van elkaar te scheiden. Volledig beheerde Android Enterprise-apparaten zijn alleen ontworpen voor werk- of schoolgegevens. Daarom moeten Microsoft-apps die zijn geïmplementeerd op deze apparaten, worden geconfigureerd om persoonlijke accounts niet toe te staan.

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>Persoonlijke accounts niet toestaan voor Microsoft-apps op Android Enterprise-apparaten

1. Voeg de apps toe aan Beheerde Google Play. Zie [Beheerde Google Play-apps toevoegen aan Android Enterprise-apparaten met Intune](../apps/apps-add-android-for-work.md) voor meer informatie.
2. Maak beleid voor elke Beheerde Google Play zoals beschreven in [App-configuratiebeleid toevoegen voor beheerde Android Enterprise-apparaten]().
3. Maak de volgende enkele sleutel in elk beleid:

    | Sleutel | Waarden |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | Een of meer door komma's (;) gescheiden UPN's.<br>Alleen beheerde gebruikersaccounts die met deze sleutel zijn gedefinieerd, zijn toegestaan.<br>Voor apparaten die zijn ingeschreven bij Intune, kan het {{userprincipalname}}-token worden gebruikt voor het ingeschreven gebruikersaccount. |


## <a name="next-steps"></a>Volgende stappen
Pas de [beveiligingsinstellingen voor Android Enterprise-werkprofielen](android-work-profile-security-settings.md) of de [beveiligingsinstellingen voor volledig beheerde Android Enterprise-apparaten](android-fully-managed-security-settings.md) toe.