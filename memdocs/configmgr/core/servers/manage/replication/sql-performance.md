---
title: SQL-prestaties
titleSuffix: Configuration Manager
description: Gebruik dit diagram om te beginnen met het oplossen van problemen met SQL-prestaties voor Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9930a8a4-4d7f-47a4-bf6b-4c36d0ed5528
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e492b4495e811b21eb582de7314d2ef41241775
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714624"
---
# <a name="sql-performance"></a>SQL-prestaties

In een hiërarchie met meerdere sites Configuration Manager gebruikt SQL-replicatie om gegevens over te dragen tussen sites. Zie [database replicatie](../../../plan-design/hierarchy/database-replication.md)voor meer informatie.

Gebruik het volgende diagram om te beginnen met het oplossen van SQL-prestaties die van invloed kunnen zijn op de replicatie status:

![Diagram voor het oplossen van problemen met SQL-prestaties](media/sql-performance.png)

<!-- PNG used instead of SVG because the SQL statements wrap weird in the SVG. The SVG file exists in the same location. -->

## <a name="queries"></a>Query's

Dit diagram maakt gebruik van de volgende query's:

### <a name="make-sure-sql-change-tracking-table-is-cleaned-up"></a>Controleer of de SQL-tabel voor het bijhouden van wijzigingen is opgeruimd

```sql
DECLARE @RetentionUnit INT = 0;
DECLARE @RetentionPeriod INT = 0;
DECLARE @CTCutOffTime DATETIME;
DECLARE @CTMinTime DATETIME;

SELECT @RetentionPeriod=retention_period,  
    @RetentionUnit=retention_period_units  
FROM sys.change_tracking_databases  
WHERE database_id = DB_ID();

IF @RetentionUnit = 1
    SET @CTCutOffTime = DATEADD(MINUTE,-@RetentionPeriod,GETUTCDATE())
ELSE IF @RetentionUnit = 2
    SET @CTCutOffTime = DATEADD(HOUR,-@RetentionPeriod,GETUTCDATE())
ELSE IF @RetentionUnit = 3
    SET @CTCutOffTime = DATEADD(DAY,-@RetentionPeriod,GETUTCDATE())

-- give a buffer of two days
SET @CTCutOffTime = DATEADD(DAY, -2, @CTCutOffTime)
select top 1 @CTMinTime=commit_time from sys.dm_tran_commit_table order by commit_ts asc
IF @CTMinTime < @CTCutOffTime
    PRINT 'there is change tracking backlog, please contact Microsoft support'
```

### <a name="change-current-sessions-that-handle-sql-service-broker-messages-are-blocked"></a>De huidige sessies wijzigen waarmee de SQL Service Broker-berichten worden verwerkt, worden geblokkeerd

```sql
select
       req.session_id
       ,req.blocking_session_id
       ,req.last_wait_type
       ,req.wait_type
       ,req.wait_resource
       ,t.text
from sys.dm_exec_sessions s
inner join sys.dm_exec_requests req on s.Session_id=req.session_id
cross apply sys.dm_exec_sql_text(sql_handle) t
where program_name='SMS_data_replication_service'
```

### <a name="check-sessions-asking-too-much-memory"></a>Sessies controleren die te veel geheugen vragen

```sql
SELECT * FROM sys.dm_exec_query_memory_grants
ORDER BY requested_memory_kb DESC
```

### <a name="check-sessions-taking-too-many-locks"></a>Controleren of sessies te veel vergren delingen

```sql
SELECT TOP 10 request_session_id,
program_name = (SELECT program_name FROM sys.dm_exec_sessions WHERE session_id=request_session_id),
COUNT (*) num_locks
FROM sys.dm_tran_locks
GROUP BY request_session_id
ORDER BY count (*) DESC
```

## <a name="see-also"></a>Zie ook

[SQL-configuratie](sql-configuration.md)
