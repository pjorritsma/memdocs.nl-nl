---
title: Hulpprogramma voor het uitvoeren van meteroverzichten
titleSuffix: Configuration Manager
description: Gebruik het hulp programma voor het samen vatting van metingen uitvoeren om de taken overzicht van software licentie controle in Configuration Manager te activeren.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723171"
---
# <a name="run-meter-summarization-tool"></a>Hulpprogramma voor het uitvoeren van meteroverzichten

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het samenvattings programma voor het uitvoeren van metingen is een van de [Configuration Manager-hulpprogram ma's](tools.md). Gebruik dit om de onderhouds taken voor de samen vatting van software licentie controle op primaire sites direct te activeren. Deze taken worden standaard uitgevoerd zoals gepland in **site-onderhouds** taken die na 12:00 uur elke dag beginnen. 

Deze taken samenvatten de gegevens in de SQL-tabel **MeterData** en schrijven de samenvattings resultaten naar de tabellen **FileUsageSummary** en **MonthlyUsageSummary** . Vervolgens ziet u het overzicht van de resultaten in software meter rapporten. Elke Configuration Manager gebruiker met beheerders rechten die verbinding kan maken met de data base van de primaire site, kan dit hulp programma gebruiken om samen vatting uit te voeren. 

Met dit hulp programma worden de taken overzicht van het samen vatting van **Bestands gebruik** en het **overzicht van maandelijkse gebruiks** gegevens van software meters uitgevoerd. Er wordt een overzicht gegeven van alle bestaande meter gegevens zonder de gebruikelijke wacht tijd van 12 uur. Voer deze uit op de SQL-Server die als host fungeert voor de site database. Als samen vatting is geslaagd, wordt de afsluit code ingesteld op `0`. Als er een fout is opgetreden, is `1`de afsluit code.



## <a name="usage"></a>Gebruik

### <a name="command-line"></a>Opdrachtregel

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Opties

#### <a name="database-name"></a>Databasenaam
De naam van de site database op de SQL-Server.

#### <a name="delay-in-hours-for-summarization"></a>Vertraging in uren voor samen vatting
Het hulp programma geeft een overzicht van het gebruik van software licentie controle dat is gegenereerd voor de vertraging. Deze vertraging is standaard nul.


### <a name="example"></a>Voorbeeld

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Het gebruik van software licentie controle samenvatten dat 12 uur geleden is gegenereerd

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Zie ook

- [Onderhoudstaken](../servers/manage/maintenance-tasks.md)
- [Het app-gebruik controleren met softwaremeter](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)
