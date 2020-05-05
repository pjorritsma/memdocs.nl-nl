---
title: SQL-replicatie opnieuw initialiseren
titleSuffix: Configuration Manager
description: Gebruik dit diagram om te beginnen met het oplossen van problemen met het opnieuw initialiseren van SQL-replicatie tussen Configuration Manager sites
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6207ed4eeeef892de38c85096d2cc80189214d1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078550"
---
# <a name="sql-replication-reinit"></a>SQL-replicatie opnieuw initialiseren

In een hiërarchie met meerdere sites Configuration Manager gebruikt SQL-replicatie om gegevens over te dragen tussen sites. Zie [database replicatie](../../../plan-design/hierarchy/database-replication.md)voor meer informatie.

Gebruik het volgende diagram om te beginnen met het oplossen van problemen met de initialisatie van SQL-replicatie (opnieuw initialiseren):

![Diagram voor het oplossen van problemen met SQL-replicatie opnieuw initialiseren](media/sql-replication-reinit.svg)

## <a name="queries"></a>Query's

Dit diagram maakt gebruik van de volgende query's:

### <a name="check-if-site-is-in-maintenance-mode"></a>Controleren of de site zich in de onderhouds modus bevindt

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>Controleren welke replicatie groep nog niet opnieuw is geiniteerd

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>Globale gegevens controleren

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>Site gegevens controleren

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Volgende stappen

- [Herinitialisatie voor globale gegevens](global-data-reinit.md)
- [Herinitialisatie voor sitegegevens](site-data-reinit.md)
- [SQL-configuratie](sql-configuration.md)
