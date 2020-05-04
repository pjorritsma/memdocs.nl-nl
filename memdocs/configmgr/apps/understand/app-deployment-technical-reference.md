---
title: Technische Naslag informatie over het oplossen van toepassings implementaties
titleSuffix: Configuration Manager
description: Technische Naslag informatie voor het oplossen van problemen met toepassings implementatie in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5b3513131b73ac2b63cf18f31b1e39e15ee97420
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709815"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Technische documentatie voor de implementatie van toepassingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel leert u hoe toepassings implementaties werken.

## <a name="before-you-begin"></a>Voordat u begint

Bij het oplossen van problemen met toepassings implementaties zijn er meerdere items die handig kunnen zijn bij het controleren van client Logboeken. Deze items zijn onder andere:

- CI-ID van toepassing
- Unieke ID van de toepassing
- Unieke ID implementatie type
- Unieke ID van de toepassings implementatie (ook bekend als toewijzings-unieke ID)
- Doel van toepassings implementatie
- Unieke ID van inhoud
- Verzamelings-ID en naam
- Type verzameling

Om het oplossen van problemen te vereenvoudigen, kunt u een SQL-query uitvoeren die vergelijkbaar is met die van de Configuration Manager Data Base om de hierboven weer gegeven informatie te verkrijgen.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> Wanneer u deze query uitvoert, **moet** u de naam van de toepassing die wordt vermeld op het tabblad Algemene informatie van toepassings eigenschappen gebruiken, in plaats van de gelokaliseerde toepassings naam die wordt vermeld op het tabblad Software Center van eigenschappen van de toepassing.

## <a name="next-steps"></a>Volgende stappen

- [Toepassings implementatie beleid](deployment-policy-technical-reference.md)
