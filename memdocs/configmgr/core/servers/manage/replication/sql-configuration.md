---
title: SQL-configuratie
titleSuffix: Configuration Manager
description: Gebruik dit diagram om te beginnen met het oplossen van problemen met SQL-configuratie voor Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95ab8cbd-0807-4422-823a-f5f9314ba623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b909d992dc16b6e786c62143347ed420d913dbc5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723227"
---
# <a name="sql-configuration"></a>SQL-configuratie

In een hiërarchie met meerdere sites Configuration Manager gebruikt SQL-replicatie om gegevens over te dragen tussen sites. Zie [database replicatie](../../../plan-design/hierarchy/database-replication.md)voor meer informatie.

Gebruik het volgende diagram om te beginnen met het oplossen van problemen met SQL-configuratie met betrekking tot SQL Service Broker:

![Diagram voor het oplossen van problemen met SQL-configuratie](media/sql-configuration.svg)

## <a name="queries"></a>Query's

Dit diagram bevat de volgende query's en acties:

### <a name="check-if-sql-can-deliver-ssb-messages"></a>Controleren of SQL SSB-berichten kan leveren

```sql
SELECT transmission_status, *
FROM sys.transmission_queue
ORDER BY enqueue_time DESC
```

## <a name="remediation-actions"></a>Herstelacties

### <a name="remediate-the-issues-reported-from-transmission_status"></a>Herstel de problemen die worden gerapporteerd uit transmission_status

Veelvoorkomende problemen:

- Firewallconfiguratie
- Netwerkconfiguratie
- SSB-certificaat onjuist geconfigureerd

### <a name="run-sql-profiler-to-trace-ssb-events"></a>SQL Profiler uitvoeren om SSB-gebeurtenissen te traceren

Voer SQL Profiler uit op de CAS-en primaire-site database om gebeurtenissen te traceren die betrekking hebben op de SQL-Service Broker:

- **Controle Broker-aanmelding**
- **Broker-conversatie controleren**
- Gebeurtenissen in de categorie **Broker**
