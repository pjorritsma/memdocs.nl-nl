---
title: Gegevenslekken op niet-beheerde apparaten voorkomen
titleSuffix: Microsoft Intune
description: Sta met Microsoft Intune toegang tot zakelijke gegevens op apparaten toe en beveilig gegevens tegen gegevenslekken.
keywords: bescherming van gegevens voorkomt gegevenslekken op M365 Microsoft 365-apparaten
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: b1512c3a-3bbd-4111-a0df-c874a0a335df
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c979d6cf35611a419c4e27605b696c6ad3d85cd9
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996177"
---
# <a name="prevent-data-leaks-on-non-managed-devices-using-microsoft-intune"></a>Gegevenslekken op niet-beheerde apparaten voorkomen met Microsoft Intune

Als u toegang verleent tot bedrijfsgegevens die worden gehost door Microsoft 365, kunt u bepalen hoe gebruikers gegevens delen en opslaan zonder risico op (on)opzettelijke gegevenslekken. Microsoft Intune biedt app-beveiligingsbeleid voor gegevensbeveiliging dat u instelt voor het beveiligen van uw bedrijfsgegevens op apparaten van gebruikers. De apparaten hoeven niet te zijn ingeschreven in de Intune-service. 

App-beveiligingsbeleid dat is ingesteld met Intune werkt ook op apparaten die worden beheerd met een beheersysteem voor niet-Microsoft-apparaten. De persoonlijke gegevens op de apparaten worden ongemoeid gelaten, alleen bedrijfsgegevens worden beheerd door de IT-afdeling. 

Als u bedrijfsgegevens wilt beveiligen, kunt u app-beveiligingsbeleid instellen voor mobiele Office-apps op apparaten met Windows, iOS/iPadOS of Android. Met deze beleidsregels kunt u beleid instellen voor een PINCODE of bedrijfsgegevensversleuteling op basis van een app. Ook kunt u zo meer geavanceerde instellingen instellen voor het beperken van het gebruik van knippen, kopiëren, plakken en opslagfuncties door gebruikers tussen beheerde en onbeheerde apps. U kunt ook op afstand bedrijfsgegevens wissen zonder dat gebruikers apparaten moeten inschrijven.

Intune-app-beveiligingsbeleid is onafhankelijk van apparaatbeheer. Met app-beveiligingsbeleid kunt u mobiele Office-apps beheren op zowel niet-beheerde als door Intune beheerde apparaten, evenals op apparaten die worden beheerd door niet-Microsoft MDM-oplossingen.

## <a name="before-you-begin"></a>Voordat u begint

Het volgende actieplan kan worden gebruikt wanneer u aan de volgende vereisten voldoet:

* Uw bedrijf is gereed voor een veilige overgang naar de cloud.
* Uw bedrijf gebruikt Microsoft 365 Exchange Online, SharePoint Online, OneDrive voor Bedrijven of Yammer.
* Uw bedrijf heeft licenties voor Microsoft 365, Enterprise Mobility + Security (EMS) of Azure Information Protection.
* Uw bedrijf biedt gebruikers toegang tot bedrijfsgegevens vanaf zakelijke of persoonlijke Windows-, iOS/iPadOS- of Android-apparaten.
* Uw bedrijf wil niet de inschrijving van persoonlijke apparaten in een apparaatbeheerservice verplichten.

## <a name="action-plan"></a>Actieplan

Voor iOS/iPadOS- en Android-apparaten:

1. Ontdek hoe [app-beveiligingsbeleid](../apps/app-protection-policy.md) werkt.
2. Meer informatie over [het maken en implementeren van app-beveiligingsbeleid](../apps/app-protection-policies.md) voor mobiele Office-apps.
3. [Bewaak het app-beveiligingsbeleid ](../apps/app-protection-policies-monitor.md) dat u maakt en implementeert.

Voor Windows 10-apparaten:

1. Ontdek [hoe Windows Information Protection (WIP) werkt](/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip).
2. Aan de slag met de configuratie van [app-beveiligingsbeleid in Windows 10](../apps/app-protection-policies-configure-windows-10.md).
3. [Beveiligingsbeleid voor de beveiliging van apps voor WIP maken en implementeren met Intune](../apps/windows-information-protection-policy-create.md).

## <a name="what-to-tell-employees-and-students"></a>Wat u werknemers en leerlingen/studenten over Intune kunt vertellen

Deel zo nodig de volgende koppelingen voor aanvullende informatie:

* [Wat u kunt verwachten wanneer uw iOS-/iPadOS-app wordt beheerd door een app-beveiligingsbeleid](../fundamentals/end-user-mam-apps-ios.md)
* [Wat u kunt verwachten wanneer uw Android-app wordt beheerd door een app-beveiligingsbeleid](../fundamentals/end-user-mam-apps-android.md)

## <a name="next-steps"></a>Volgende stappen

Wilt u hulp bij het toepassen hiervan of andere scenario's voor EMS of Microsoft 365? Als u ten minste 150 licenties voor Microsoft 365, Enterprise Mobility + Security of Azure Active Directory Premium hebt, gebruikt u uw [FastTrack-voordelen](/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program).
