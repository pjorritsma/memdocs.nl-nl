---
title: SQL-replicatie
titleSuffix: Configuration Manager
description: Dit diagram gebruiken om problemen met SQL-replicatie tussen Configuration Manager sites op te lossen
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a25218e53313b7a8c3192959b54b65d2a32fae7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717522"
---
# <a name="sql-replication"></a>SQL-replicatie

In een hiërarchie met meerdere sites Configuration Manager gebruikt SQL-replicatie om gegevens over te dragen tussen sites. Zie [database replicatie](../../../plan-design/hierarchy/database-replication.md)voor meer informatie.

Gebruik het volgende diagram om te beginnen met het oplossen van problemen met SQL-replicatie wanneer een koppeling mislukt:

![Diagram voor het oplossen van problemen met SQL-replicatie](media/sql-replication.svg)

## <a name="queries"></a>Query's

Dit diagram maakt gebruik van de volgende query's:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>Controleer of de koppeling van de replicatie groep is gedegradeerd of mislukt

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>Controleren of de koppeling van de replicatie groep onlangs is berekend

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>De onderhouds modus van SQL controleren

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Volgende stappen

- [SQL-replicatie opnieuw initialiseren (herinitialisatie)](sql-replication-reinit.md)
- [SQL-prestaties](sql-performance.md)
- [SQL-configuratie](sql-configuration.md)
