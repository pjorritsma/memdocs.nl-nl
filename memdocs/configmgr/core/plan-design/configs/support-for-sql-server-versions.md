---
title: Ondersteunde SQL Server-versies
titleSuffix: Configuration Manager
description: SQL Server versie-en configuratie vereisten ophalen voor het hosten van een Configuration Manager-site database.
ms.date: 06/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5043967a640b937784c22ea2b74269a2f2043ba9
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607633"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Ondersteunde SQL Server versies voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor elke Configuration Manager-site is een ondersteunde SQL Server versie en configuratie vereist om de site database te hosten.  

## <a name="sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> SQL Server-exemplaren en -locaties

### <a name="central-administration-site-and-primary-sites"></a>Centrale beheer site en primaire sites

De site database moet een volledige installatie van SQL Server gebruiken.  

SQL Server kunnen zich bevinden op:  

- De site Server computer.  
- Een computer die zich op afstand van de site server bevindt.  

De volgende exemplaren worden ondersteund:  

- Het standaard of benoemd exemplaar van SQL Server.  
- Configuraties met meerdere exemplaren.  
- Een SQL Server cluster. Zie [een SQL Server-cluster gebruiken om de site database te hosten](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
- Een SQL Server AlwaysOn-beschikbaarheids groep. Zie [SQL Server AlwaysOn voor een Maxi maal beschik bare site database](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie.

### <a name="secondary-sites"></a>Secundaire sites

De site database kan gebruikmaken van het standaard exemplaar van een volledige installatie van SQL Server of SQL Server Express.  

SQL Server moet zich op de site Server computer bevinden.  

### <a name="limitations-to-support"></a>Beperkingen voor ondersteuning

De volgende configuraties worden niet ondersteund:

- Een SQL Server cluster in een NLB-cluster configuratie (Network Load Balancing)
- Een SQL Server cluster op een Cluster Shared Volume (CSV)
- SQL Server Data Base mirroring-technologie en peer-to-peer-replicatie

SQL Server transactionele replicatie wordt alleen ondersteund voor het repliceren van objecten naar beheer punten die zijn geconfigureerd voor het gebruik van [database replica's](../../servers/deploy/configure/database-replicas-for-management-points.md).  

## <a name="supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Ondersteunde versies van SQL Server

In een hiërarchie met meerdere sites kunnen verschillende sites verschillende versies van SQL Server gebruiken om de site database te hosten. Zolang de volgende punten van toepassing zijn:

- Configuration Manager ondersteunt de versies van SQL Server die u gebruikt.
- De SQL Server versies die u gebruikt, blijven in de ondersteuning van micro soft.
- SQL Server ondersteunt replicatie tussen de twee versies van SQL Server. Zie [SQL Server replicatie achterwaartse compatibiliteit](/sql/relational-databases/replication/replication-backward-compatibility)voor meer informatie.

Voor SQL Server 2016 en voorafgaand aan de ondersteuning voor elke SQL-versie en Service Pack wordt het [micro soft Lifecycle-beleid](https://aka.ms/sqllifecycle)gevolgd. Ondersteuning voor een specifiek SQL Server Service Pack bevat cumulatieve updates, tenzij ze achterwaartse compatibiliteit met de versie van het basis Service Pack verstoren. Vanaf SQL Server 2017 worden service packs niet vrijgegeven, omdat het een [modern service model](/archive/blogs/sqlreleaseservices/announcing-the-modern-servicing-model-for-sql-server)volgt. Het SQL Server-team raadt voortdurend, [proactieve installatie van cumulatieve updates](/archive/blogs/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism) aan zodra deze beschikbaar komen.

Tenzij anders aangegeven, worden de volgende versies van SQL Server ondersteund met alle actieve versies van Configuration Manager. Als ondersteuning voor een nieuwe SQL Server-versie wordt toegevoegd, wordt de Configuration Manager versie die ondersteuning biedt, vermeld. Als de ondersteuning is afgeschaft, zoekt u naar details over betrokken versies van Configuration Manager.

> [!IMPORTANT]  
> Wanneer u SQL Server Standard voor de Data Base op de centrale beheer site gebruikt, beperkt u het totale aantal clients dat een hiërarchie kan ondersteunen. Zie [Grootte en schaalgetallen](size-and-scale-numbers.md).

### <a name="sql-server-2019-standard-enterprise"></a>SQL Server 2019: Standard, Enter prise

Vanaf Configuration Manager versie 1910 kunt u deze versie gebruiken met cumulatieve update 5 (CU5) of hoger, zolang de cumulatieve update versie wordt ondersteund door de SQL-levens cyclus. CU5 is de minimale vereiste voor SQL Server 2019, omdat hiermee een probleem met [scalaire UDF](/sql/relational-databases/user-defined-functions/scalar-udf-inlining)-INACTIE wordt opgelost.

Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een centrale beheer site
- Een primaire site
- Een secundaire site

<!--
#### Known issue with SQL Server 2019

There's a known issue<!--6436234 with the new [scalar UDF inlining](/sql/relational-databases/user-defined-functions/scalar-udf-inlining) feature in SQL 2019. To work around this issue and disable UDF lining, run the following script on the SQL 2019 server:

```sql
ALTER DATABASE SCOPED CONFIGURATION SET TSQL_SCALAR_UDF_INLINING = OFF  
```

While not always necessary, you may need to restart the SQL server after you run this script. For more information, see [Disabling Scalar UDF Inlining without changing the compatibility level](/sql/relational-databases/user-defined-functions/scalar-udf-inlining#disabling-scalar-udf-inlining-without-changing-the-compatibility-level).

You can safely disable this SQL feature for the site database server because Configuration Manager doesn't use it.

If you don't disable scalar UDF inlining in SQL 2019, the site server will randomly fail to query the site database. For example, you'll see the following errors in **hman.log**:

```hman.log
*** [HY000][0][Microsoft][SQL Server Native Client 11.0]Unspecified error occurred on SQL Server. Connection may have been terminated by the server.
*** select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
*** [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.
Failed to execute SQL command select dbo.fnGetSiteMode(dbo.fnGetSiteCode())
```

You may see similar errors in other logs, such as **SmsAdminUI.log**.

SQL Server version 2019 logs the following error:

`Microsoft SQL Server reported SQL message 596, severity 21: [HY000][596][Microsoft][SQL Server Native Client 11.0][SQL Server]Cannot continue the execution because the session is in the kill state.`

You'll also see crash dumps (`.mdump` files) from SQL in its log directory, which by default is `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log`.
-->

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enter prise

U kunt deze versie gebruiken met [cumulatieve update versie 2](https://support.microsoft.com/help/4052574) of hoger, op voor waarde dat de cumulatieve update versie wordt ondersteund door de SQL-levens cyclus. Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een centrale beheer site  
- Een primaire site  
- Een secundaire site  
  <!--SMS.498506-->

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enter prise  
<!--514985-->
U kunt deze versie gebruiken met het minimale Service Pack en de cumulatieve update die wordt ondersteund door de SQL-levens cyclus. Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een centrale beheer site  
- Een primaire site  
- Een secundaire site  

### <a name="sql-server-2014-standard-enterprise"></a>SQL Server 2014: Standard, Enter prise

U kunt deze versie gebruiken met het minimale Service Pack en de cumulatieve update die wordt ondersteund door de SQL-levens cyclus. Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een centrale beheer site  
- Een primaire site  
- Een secundaire site

### <a name="sql-server-2012-standard-enterprise"></a>SQL Server 2012: Standard, Enter prise

U kunt deze versie gebruiken met het minimale Service Pack en de cumulatieve update die wordt ondersteund door de SQL-levens cyclus. Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een centrale beheer site  
- Een primaire site  
- Een secundaire site  

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express

U kunt deze versie gebruiken met [cumulatieve update versie 2](https://support.microsoft.com/help/4052574) of hoger, op voor waarde dat de cumulatieve update versie wordt ondersteund door de SQL-levens cyclus. Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een secundaire site
<!--SMS.498506-->

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express

U kunt deze versie gebruiken met het minimale Service Pack en de cumulatieve update die wordt ondersteund door de SQL-levens cyclus. Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een secundaire site

### <a name="sql-server-2014-express"></a>SQL Server 2014 Express

U kunt deze versie gebruiken met het minimale Service Pack en de cumulatieve update die wordt ondersteund door de SQL-levens cyclus. Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een secundaire site  

### <a name="sql-server-2012-express"></a>SQL Server 2012 Express

U kunt deze versie gebruiken met het minimale Service Pack en de cumulatieve update die wordt ondersteund door de SQL-levens cyclus. Deze versie van SQL kan worden gebruikt voor de volgende sites:

- Een secundaire site  

## <a name="required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Vereiste configuraties voor SQL Server

De volgende configuraties zijn vereist voor alle installaties van SQL Server die u gebruikt voor een site database, inclusief SQL Server Express. Als Configuration Manager SQL Server Express installeert als onderdeel van een installatie van een secundaire site, worden deze configuraties automatisch gemaakt.  

### <a name="sql-server-architecture-version"></a>SQL Server architectuur versie

Configuration Manager is een 64-bits versie van SQL Server om de site database te hosten.  

### <a name="database-collation"></a>Sortering van data base

Op elke site moet het exemplaar van SQL Server dat wordt gebruikt voor de site en de site database de volgende sortering gebruiken: **SQL_Latin1_General_CP1_CI_AS**.  

Configuration Manager ondersteunt twee uitzonde ringen op deze sortering voor de standaard van China. Zie [internationale ondersteuning](../hierarchy/international-support.md)voor meer informatie.  

### <a name="database-compatibility-level"></a>Compatibiliteits niveau van data base

Configuration Manager vereist dat het compatibiliteits niveau voor de site database niet lager is dan de laagste versie die wordt ondersteund SQL Server voor uw Configuration Manager versie. Bijvoorbeeld, beginnend met versie 1702, moet u een [compatibiliteits niveau voor de data base](/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) hebben dat groter is dan of gelijk is aan 110. <!-- SMS.506266-->

### <a name="sql-server-features"></a>SQL Server functies

Alleen het onderdeel **Database-engineservices** is vereist voor elke siteserver.  

Voor Configuration Manager database replicatie is de functie voor **SQL Server replicatie** niet vereist. Deze SQL Server configuratie is echter vereist als u [database replica's gebruikt voor beheer punten](../../servers/deploy/configure/database-replicas-for-management-points.md).  

### <a name="windows-authentication"></a>Windows-verificatie

Configuration Manager vereist **Windows-verificatie** voor het valideren van verbindingen met de data base.  

### <a name="sql-server-instance"></a>SQL Server-exemplaar

Gebruik een toegewezen exemplaar van SQL Server voor elke site. Het exemplaar kan een **benoemd exemplaar** of het **standaard exemplaar**zijn.  

### <a name="sql-server-memory"></a>SQL Server geheugen

Reserveer geheugen voor de SQL Server met behulp van SQL Server Management Studio. Stel de instelling **minimum server geheugen** in onder **Server geheugen opties**. Zie [SQL Server-configuratie van geheugen server](/sql/database-engine/configure-windows/server-memory-server-configuration-options)voor meer informatie over het configureren van deze instelling.  

- **Voor een database server die u installeert op dezelfde computer als de site server**: Beperk het geheugen voor SQL Server tot 50 tot 80 procent van het beschik bare systeem geheugen dat kan worden aanhouden.  

- **Voor een speciale database server die zich op afstand van de site server**bevinden: Beperk het geheugen voor SQL Server tot 80 tot 90 procent van het beschik bare systeem geheugen dat kan worden besteld.  

- **Voor een geheugen reserve voor de buffer groep van elk SQL Server exemplaar dat in gebruik**is:  

  - Voor een centrale beheer site: Stel mini maal 8 GB in.  
  - Voor een primaire site: Stel mini maal 8 GB in.  
  - Voor een secundaire site: Stel mini maal 4 GB in.  

### <a name="sql-nested-triggers"></a>Geneste SQL-triggers

Genest SQL-triggers moet zijn ingeschakeld. Zie [configuratie van de geneste triggers-server configureren](/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option) voor meer informatie.

### <a name="sql-server-clr-integration"></a>SQL Server CLR-integratie

SQL Server Common Language Runtime (CLR) moet zijn ingeschakeld voor de sitedatabase. Deze optie wordt automatisch ingeschakeld wanneer Configuration Manager wordt geïnstalleerd. Zie [Introduction to SQL Server CLR Integration](/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration)(Engelstalig) voor meer informatie over CLR.  

### <a name="sql-server-service-broker-ssb"></a>SQL Server Service Broker (SSB)

De SQL Server Service Broker is vereist voor intersite-replicatie en voor één primaire site.

### <a name="trustworthy-setting"></a>Betrouw bare instelling

Configuration Manager schakelt automatisch de [eigenschap SQL TRUSTWORTHY data base](/sql/relational-databases/security/trustworthy-database-property)in. Configuration Manager moet zijn **ingeschakeld**voor deze eigenschap.

## <a name="optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Optionele configuraties voor SQL Server

De volgende configuraties zijn optioneel voor elke database die een volledige installatie van SQL Server gebruikt.  

### <a name="sql-server-service"></a>SQL Server-service

U kunt de SQL Server-service zo configureren dat deze wordt uitgevoerd met:  

- Een *domein gebruikers account met weinig rechten* :  

  - Deze configuratie is een best practice. mogelijk moet u de Service Principal Name (SPN) voor het account hand matig registreren.  

- Het **lokale systeem** account van de computer waarop SQL Server wordt uitgevoerd:  

  - Gebruik het account voor het lokale systeem om het configuratieproces te vereenvoudigen.  
  - Wanneer u het lokale systeem account gebruikt, registreert Configuration Manager automatisch de SPN voor de SQL Server-service.  
  - Het gebruik van het lokale systeem account voor de SQL Server-service is geen SQL Server best practice.  

Wanneer de computer met SQL Server niet het lokale systeem account gebruikt om de SQL Server-service uit te voeren, configureert u de SPN van het account waarmee de SQL Server-service in Active Directory Domain Services wordt uitgevoerd. (Wanneer het systeem account wordt gebruikt, wordt de SPN automatisch voor u geregistreerd.)

Zie [de SPN voor de site database server beheren](../../servers/manage/modify-your-infrastructure.md#bkmk_SPN)voor meer informatie over spn's voor de site database.  

Voor informatie over het wijzigen van het account dat wordt gebruikt door de SQL Server-service, raadpleegt u [SCM Services-het account voor het opstarten van de service wijzigen](/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services is vereist voor het installeren van een Reporting Services-punt waarmee u rapporten kunt uitvoeren. Configuration Manager ondersteunt dezelfde versies van SQL Server voor rapportage als voor de site database.

Zie [vereisten voor rapportage in Configuration Manager](../../servers/manage/prerequisites-for-reporting.md)voor meer informatie.

> [!IMPORTANT]  
> Nadat u SQL Server van een vorige versie hebt bijgewerkt, ziet u mogelijk de volgende fout: *Report Builder bestaat niet*.  
> U moet de site systeemrol van het Reporting Services-punt opnieuw installeren om deze fout op te lossen.  

### <a name="data-warehouse-service-point"></a>Data Warehouse-service punt

Het Data Warehouse maakt gebruik van een afzonderlijke data base. U kunt het hosten op de site database server of een afzonderlijke SQL Server. Zie [het Data Warehouse-service punt voor Configuration Manager](../../servers/manage/data-warehouse.md)voor meer informatie.

### <a name="sql-server-ports"></a>SQL Server poorten

Voor communicatie met de SQL Server data base-engine en voor intersitereplicatie kunt u de standaard SQL Server poort configuraties gebruiken of aangepaste poorten opgeven:  

- **Intersite-communicatie** maakt gebruik van de SQL Server Service Broker, die standaard poort TCP 4022 gebruikt.  
- **Intra site-communicatie** tussen de SQL server data base-engine en verschillende Configuration Manager site systeem rollen gebruiken standaard poort TCP 1433. De volgende sitesysteemrollen communiceren direct met de SQL Server database:  

  - Beheerpunt  
  - Computer van de SMS-provider  
  - Reporting Services-punt  
  - Siteserver  

Wanneer een computer met SQL Server een Data Base van meer dan één site host, moet elke Data Base een afzonderlijk exemplaar van SQL Server gebruiken. Daarnaast moet elk exemplaar worden geconfigureerd voor het gebruik van een unieke set poorten.  

> [!WARNING]  
> Configuration Manager biedt geen ondersteuning voor dynamische poorten. Omdat benoemde exemplaren van SQL Server standaard dynamische poorten gebruiken voor verbindingen naar de database-engine, moet u, wanneer u een benoemd exemplaar gebruikt, de statische poort, die u wenst te gebruiken voor intrasite-communicatie, handmatig configureren.  

Als u een firewall hebt ingeschakeld op de computer waarop SQL Server, moet u ervoor zorgen dat deze is geconfigureerd zodat de poorten die worden gebruikt door uw implementatie en op elke locatie in het netwerk tussen computers die met de SQL Server communiceren, worden toegestaan.  

Zie [een server configureren om te Luis teren naar een specifieke TCP-poort](/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)voor een voor beeld van het configureren van SQL Server voor het gebruik van een specifieke poort.  

## <a name="upgrade-options-for-sql-server"></a>Upgrade opties voor SQL Server

Als u uw versie van SQL Server wilt bijwerken, gebruikt u een van de volgende methoden, van eenvoudig te complexere:  

- [Upgrade SQL Server ter plekke](../../servers/manage/upgrade-on-premises-infrastructure.md#to-upgrade-sql-server-on-the-site-database-server) (aanbevolen)  

- Installeer een nieuwe versie van SQL Server op een nieuwe computer en gebruik vervolgens [de optie voor het verplaatsen van de data base](../../servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) van Configuration Manager Setup om uw site server te laten verwijzen naar de nieuwe SQL Server  

- [Back-up en herstel](../../servers/manage/backup-and-recovery.md)gebruiken. Het gebruik van back-up en herstel voor een SQL-upgrade scenario wordt ondersteund. U kunt de vereiste voor SQL-versie beheer negeren bij het controleren van [overwegingen voordat u een site herstelt](../../servers/manage/recover-sites.md#considerations-before-recovering-a-site).