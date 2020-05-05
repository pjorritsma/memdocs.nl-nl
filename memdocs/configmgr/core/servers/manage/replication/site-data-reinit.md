---
title: Herinitialisatie voor sitegegevens
titleSuffix: Configuration Manager
description: Gebruik dit diagram om te beginnen met het oplossen van problemen met het opnieuw initialiseren van SQL-replicatie voor site gegevens in een Configuration Manager-hiërarchie
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19741d45-2d42-438e-a9f3-15bb365d63ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6a336bdf323fbb81a16082e9c308577763a7c104
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078584"
---
# <a name="troubleshoot-site-data-reinit"></a>Problemen met het opnieuw initialiseren van site gegevens oplossen

In een hiërarchie met meerdere sites Configuration Manager gebruikt SQL-replicatie om gegevens over te dragen tussen sites. Zie [database replicatie](../../../plan-design/hierarchy/database-replication.md)voor meer informatie.

Gebruik het volgende diagram om te beginnen met het oplossen van problemen met het opnieuw initialiseren van SQL-replicatie voor site gegevens in een Configuration Manager-hiërarchie:

![Diagram voor het oplossen van problemen met het opnieuw initialiseren van site gegevens](media/site-data-reinit.svg)

## <a name="queries"></a>Query's

Dit diagram maakt gebruik van de volgende query's:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Controleren of de replicatie van de site niet is voltooid

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Site'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>De TrackingGuid-& status ophalen uit de certificerings instantie

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>De TrackingGuid-& status ophalen van de primaire site

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-primary-site-isnt-in-maintenance-mode"></a>Controleren of primaire site niet in onderhouds modus is

```sql
SELECT * FROM ServerData
WHERE SiteStatus = 125
AND SiteCode=dbo.fnGetSiteCode()
AND ServerRole=N'Peer'
```

### <a name="check-request-status-for-the-tracking-id"></a>Status van de aanvraag controleren voor de tracerings-ID

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Volgende stappen

- [Herinitialisatie voor ontbrekend bericht](reinit-missing-message.md)
- [Herinitialisatie voor globale gegevens](global-data-reinit.md)
