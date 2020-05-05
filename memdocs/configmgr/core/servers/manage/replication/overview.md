---
title: Problemen met SQL-replicatie oplossen
titleSuffix: Configuration Manager
description: Gebruik deze diagrammen om SQL-replicatie tussen Configuration Manager sites te begrijpen en problemen op te lossen
ms.date: 02/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 202a3360b5e04d66ada0d3b47ddd4638c2197167
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720469"
---
# <a name="troubleshoot-sql-replication"></a>Problemen met SQL-replicatie oplossen

In een hiërarchie met meerdere sites Configuration Manager gebruikt SQL-replicatie om gegevens over te dragen tussen sites. Zie [database replicatie](../../../plan-design/hierarchy/database-replication.md)voor meer informatie.

Gebruik deze diagrammen om meer inzicht te krijgen in en hulp te bieden bij het oplossen van problemen met SQL-replicatie.

- [SQL-replicatie](sql-replication.md)
- [SQL-configuratie](sql-configuration.md)
- [SQL-prestaties](sql-performance.md)
- [SQL-replicatie opnieuw initialiseren (herinitialisatie)](sql-replication-reinit.md)
- [Herinitialisatie voor globale gegevens](global-data-reinit.md)
- [Herinitialisatie voor sitegegevens](site-data-reinit.md)
- [Herinitialisatie voor ontbrekend bericht](reinit-missing-message.md)

Deze probleemoplossings diagrammen zijn gekoppeld. Gebruik het volgende diagram om inzicht te krijgen in de relaties:

![Overzichts diagram van het proces voor het oplossen van problemen met SQL-replicatie](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Voor meer informatie raadpleegt u de volgende reeks Blogs van Microsoft Ondersteuning:

- [Interne synchronisatie ConfigMgr DRS](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-drs-synchronization-internals/ba-p/1154317)
- [ConfigMgr 2012 Data Replication Service (DRS) ontketend](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-data-replication-service-drs-unleashed/ba-p/339916)
- [ConfigMgr 2012 DRS-problemen met veelgestelde vragen](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-troubleshooting-faqs/ba-p/339934)
- [Interne initialisatie van Configuration Manager 2012 DRS](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-initialization-internals/ba-p/339948)
- [ConfigMgr 2012: DRS-en SQL Service Broker-certificaat problemen](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-2012-drs-and-sql-service-broker-certificate-issues/ba-p/339910)
