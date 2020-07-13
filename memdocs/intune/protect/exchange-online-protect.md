---
title: Exchange zonder apparaatbeheer
titleSuffix: Microsoft Intune
description: Gebruik Microsoft Intune om werknemers toegang te geven tot hun e-mail van Office 365 Exchange Online zonder een apparaatbeheersysteem in te stellen.
keywords: Toegang tot e-mail van Office 365 Exchange
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/31/2017
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.topic: archived
ms.technology: ''
ms.assetid: 88a0d3b9-2622-403b-8374-1396afd8066e
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9669625225f8ad3960ece39e2a6b04849421ce6
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022178"
---
# <a name="protect-office-365-exchange-online-without-requiring-device-management"></a>Office 365 Exchange Online beveiligen zonder dat apparaatbeheer is vereist

U kunt werknemers toegang geven tot hun werk-e-mail zonder de overhead van het instellen van een apparaatbeheersysteem. U kunt toegang tot Office 365 Exchange Online geven via Intune. Bevestig dat u licenties hebt voor Microsoft 365 of voor Azure Active Directory (premium) en Intune om de benodigde stappen te voltooien. Werknemers moeten beschikken over een [ondersteund iOS-/iPadOS- of Android-apparaat](../fundamentals/supported-devices-browsers.md). 

Als u een apparaatbeheersysteem wilt instellen, is dat mogelijk. Dit type app-beveiliging werkt onafhankelijk van apparaatbeheer. 

## <a name="action-plan"></a>Actieplan

1. [Meer informatie over voorwaardelijke toegang](conditional-access.md). 
2. [Meer informatie over voorwaardelijke toegang op basis van een app](app-based-conditional-access-intune.md).
3. [Beleid voor voorwaardelijke toegang op basis van een app instellen voor Exchange Online](app-based-conditional-access-intune-create.md).
4. [Blokkeer apps die niet kunnen worden beheerd](app-modern-authentication-block.md), met name apps die geen gebruik maken van de Azure Active Directory Authentication Library (ADAL) of de Microsoft Authentication Library (MSAL).
5. (Optioneel) [Beleid voor voorwaardelijke toegang op basis van een app instellen voor SharePoint Online](app-based-conditional-access-intune-create.md). Deze beleidsregels blokkeren de toegang tot uw bedrijfsgegevens vanuit apps die niet kunnen worden beheerd en beveiligd. Dit beleid beperkt bovendien de toegang via mobiele SharePoint. 

## <a name="what-to-tell-employees-and-students"></a>Wat u werknemers en leerlingen/studenten over Intune kunt vertellen

* Vraag uw werknemers en leerlingen/studenten om Microsoft Outlook of Microsoft SharePoint te downloaden en te installeren vanuit de Apple App Store voor iOS/iPadOS, en vanuit Google Play voor Android. 
* Als u de toegang blokkeert tot apps die geen moderne authenticatie gebruiken, stel de werknemers en leerlingen/studenten dan op de hoogte van deze beperking. 

## <a name="next-steps"></a>Volgende stappen

U hebt voorwaardelijke toegang op basis van een app gebruikt om de beveiliging van bedrijfsgegevens te verbeteren. Bij de volgende stappen krijgt u meer informatie over andere manieren waarop u de beveiliging van uw bedrijfsgegevens kunt verbeteren, met inbegrip van: 

* Instellen van [voorwaardelijke toegang op basis van apparaatcompatibiliteit, apparaatrisico, locatie en gebruikerskenmerken in Active Directory en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).  
* Instellen van app-beveiligingsbeleid om uw bedrijfsgegevens te beschermen tegen opzettelijke en niet-opzettelijke gegevenslekken. 
* Gebruik van Azure Information Protection om bedrijfsgegevens buiten uw netwerk te beveiligen. 

Wilt u hulp bij het inschakelen van dit of andere scenario's voor EMS of Office 365? Als u ten minste 150 licenties voor Microsoft 365, Enterprise Mobility + Security of Azure Active Directory Premium hebt, gebruikt u uw [FastTrack-voordelen](https://docs.microsoft.com/enterprise-mobility-security/solutions/enterprise-mobility-fasttrack-program). 
