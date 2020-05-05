---
title: Herinitialisatie voor ontbrekend bericht
titleSuffix: Configuration Manager
description: Gebruik dit diagram om te beginnen met het oplossen van problemen met een ontbrekend bericht met SQL-replicatie opnieuw initialiseren in Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 39a3001e-2df5-4b36-bd83-4f1d21dda335
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e640c3dd756d96a58e8b54d6056d2adbb7bb99c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720462"
---
# <a name="reinit-missing-message"></a>Herinitialisatie voor ontbrekend bericht

In een hiërarchie met meerdere sites Configuration Manager gebruikt SQL-replicatie om gegevens over te dragen tussen sites. Zie [database replicatie](../../../plan-design/hierarchy/database-replication.md)voor meer informatie.

Gebruik het volgende diagram om te beginnen met het oplossen van problemen met een ontbrekend bericht met de initialisatie van SQL-replicatie (opnieuw initialiseren):

![Diagram voor het oplossen van problemen met het opnieuw initialiseren van ontbrekende berichten](media/reinit-missing-message.svg)

## <a name="queries"></a>Query's

Dit diagram maakt gebruik van de volgende query's:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Controleren of de replicatie van de site niet is voltooid

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-subscriber-site"></a>De TrackingGuid-& status ophalen van de abonnee site

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
```

### <a name="get-the-trackingguid--status-from-the-publishing-site"></a>De TrackingGuid-& status ophalen van de publicatie site

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

## <a name="remediation-actions"></a>Herstelacties

### <a name="version-1902-and-later"></a>Versie 1902 en hoger

Voer de [Replication link Analyzer](../monitor-replication.md#BKMK_RLA)uit om het probleem op te sporen en opnieuw te initialiseren.

### <a name="version-1810-and-earlier"></a>Versie 1810 en lager

Voer de volgende SQL-query uit om `ReplicationGroupID`de:

```sql
SELECT rd.ID AS ReplicationGroupID from ReplicationData rd
INNER JOIN RCM_DrsInitializationTracking it ON rd.ReplicationGroup = it.ReplicationGroup
WHERE it.RequestTrackingGUID=@trackingGuid
```

Gebruik vervolgens de `InitializeData` -methode voor `SMS_ReplicationGroup` de WMI-klasse met de volgende waarden:

- ReplicationGroupID: uit de bovenstaande SQL-query
- SiteCode1: bovenliggende site
- SiteCode2: onderliggende site

Zie [methode InitializeData in klasse SMS_ReplicationGroup](../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md)voor meer informatie.

#### <a name="example"></a>Voorbeeld

```PowerShell
Invoke-WmiMethod –Namespace "root\sms\site_CAS" -Class SMS_ReplicationGroup –Name InitializeData -ArgumentList "20", "CAS", "PR1"
```

## <a name="next-steps"></a>Volgende stappen

- [SQL-replicatie opnieuw initialiseren (herinitialisatie)](sql-replication-reinit.md)
