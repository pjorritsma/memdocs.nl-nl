---
title: Herinitialisatie voor globale gegevens
titleSuffix: Configuration Manager
description: Gebruik dit diagram om te beginnen met het oplossen van problemen met het opnieuw initialiseren van SQL-replicatie voor globale gegevens in een Configuration Manager-hiërarchie
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fed8a5b257591aa95fcd53b4e12a82249fce762
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713630"
---
# <a name="troubleshoot-global-data-reinit"></a>Problemen met het opnieuw initialiseren van globale gegevens oplossen

In een hiërarchie met meerdere sites Configuration Manager gebruikt SQL-replicatie om gegevens over te dragen tussen sites. Zie [database replicatie](../../../plan-design/hierarchy/database-replication.md)voor meer informatie.

Gebruik het volgende diagram om te beginnen met het oplossen van problemen met het opnieuw initialiseren van SQL-replicatie voor globale gegevens in een Configuration Manager-hiërarchie:

![Diagram voor het oplossen van problemen met globale gegevens opnieuw initialiseren](media/global-data-reinit.svg)

## <a name="queries"></a>Query's

Dit diagram maakt gebruik van de volgende query's:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Controleren of de replicatie van de site niet is voltooid

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>De TrackingGuid-& status ophalen van de primaire site

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>De TrackingGuid-& status ophalen uit de certificerings instantie

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>Status van de aanvraag controleren voor de tracerings-ID

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Volgende stappen

- [Herinitialisatie voor ontbrekend bericht](reinit-missing-message.md)
