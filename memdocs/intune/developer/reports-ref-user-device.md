---
title: Gebruikersapparaatkoppeling - Intune-datawarehouse
titleSuffix: Microsoft Intune
description: De entiteit UserDeviceAssociation bevat gebruikersapparaatkoppelingen in uw organisatie.
keywords: Intune-datawarehouse
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 777484A7-09CE-4409-987F-76B3F87DFE93
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6127b365a04ad48a9cbaa98bdef821c4d1334181
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339888"
---
# <a name="reference-for-user-device-association-entity"></a>Naslaginformatie voor entiteit gebruikersapparaatkoppelingen

De entiteit **userDeviceAssociation** bevat gebruikersapparaatkoppelingen in uw organisatie.

## <a name="userdeviceassociations"></a>userDeviceAssociations


|        Naam        |                                           Beschrijving                                            |        Voorbeeld         |
|--------------------|--------------------------------------------------------------------------------------------------|------------------------|
|      userKey       |              Een unieke id van gebruiker in het datawarehouse. (surrogaatsleutel).               |          123           |
|     deviceKey      |                      Een unieke id van het apparaat in het datawarehouse.                      |          123           |
| createdDateTimeUTC |           De datum en tijd wanneer de gebruikersapparaatkoppeling is gemaakt. Hiervoor wordt de UTC-notatie gebruikt.           | 11/23/2016 12:00:00 AM |
|     isDeleted      | Geeft aan dat de gebruiker het apparaat heeft uitgeschreven en dat de koppeling niet meer actueel is. |       Waar/onwaar       |
|  endedDateTimeUTC  |              De datum en tijd in UTC waarop IsDeleted is gewijzigd in <strong>Waar</strong>.               | 23-06-2017 12.00.00 |

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het [Intune-datawarehouse](reports-nav-create-intune-reports.md).
