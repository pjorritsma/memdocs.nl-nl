---
title: IntuneManagementExtension-entiteit
titleSuffix: Microsoft Intune
description: Naslagonderwerp voor de categorie IntuneManagementExtension van entiteitverzamelingen in de Intune-datawarehouse-API.
keywords: Intune-datawarehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 73DF3B90-6D52-4EF6-AFFD-1873A18C7421
ms.reviewer: dariusz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: aac78143e2b1e15f7b718c70d2dc7168c00f8fd4
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165291"
---
# <a name="reference-for-intune-management-extensions"></a>Naslag voor Intune-beheeruitbreidingen

De categorie **intuneManagementExtensions** bevat entiteiten voor mobiele apparaten waarmee gegevens worden bijgehouden, zoals:

- Versies van een IntuneManagementExtension
- Installatiestatus van een IntuneManagementExtension

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions

De entiteit **intuneManagementExtensionVersion** bevat een lijst van alle versies die worden gebruikt door intuneManagementExtensions.

| Eigenschap  | Beschrijving | Voorbeeld |
|---------|------------|--------|
| extensionVersionKey |De unieke id van de intuneManagementExtensions-versie. | 1 |
| extensionVersion |Het versienummer, bestaande uit vier cijfers. |1.0.2.0 |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates

De **intuneManagementExtensionHealthState** bevat een lijst van alle mogelijke statussen van de intuneManagementExtensions.

| Eigenschap  | Beschrijving | Voorbeeld |
|---------|------------|--------|
| extensionStateKey |Unieke id van de status. | 2 |
| extensionState |De status van een IntuneManagementExtension. | In orde |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions

De **intuneManagementExtension** bevat een lijst met dagelijkse intuneManagementExtensions-statussen voor elk apparaat met Windows 10.
De gegevens voor de afgelopen 60 dagen worden bewaard. 


|      Eigenschap       |                         Beschrijving                         | Voorbeeld |
|---------------------|-------------------------------------------------------------|---------|
|       dateKey       |               De unieke id van de datum.                |   123   |
|      tenantKey      |              De unieke id van de tenant.               |   456   |
|      deviceKey      |              Unieke id van het apparaat.               |   789   |
| extensionVersionKey | De unieke id van de intuneManagementExtension-versie. |    1    |
|  extensionStateKey  |             Unieke id van de status.              |    2    |

