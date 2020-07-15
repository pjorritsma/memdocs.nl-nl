---
title: SQL Server Always On
titleSuffix: Configuration Manager
description: Gebruik van een SQL Server always on-beschikbaarheids groep plannen met Configuration Manager
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce8c10d9d59d97caa53ece12dd43d90c78546bb
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384839"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Het gebruik van SQL Server AlwaysOn-beschikbaarheids groepen met Configuration Manager voorbereiden

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik dit artikel om Configuration Manager voor te bereiden op het gebruik van SQL Server AlwaysOn-beschikbaarheids groepen. Deze functie biedt een oplossing voor hoge Beschik baarheid en herstel na nood gevallen voor de site database.  

Configuration Manager ondersteunt het gebruik van beschikbaarheids groepen:

- Op primaire sites en de centrale beheer site.
- On-premises of in Microsoft Azure.

Als u beschikbaarheids groepen gebruikt in Microsoft Azure, kunt u de beschik baarheid van uw site database verder verhogen met behulp van *Azure-beschikbaarheids sets*. Zie voor meer informatie over beschikbaarheidssets van Azure [Manage the availability of virtual machines](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/)(De beschikbaarheid van virtuele machines beheren).

> [!Important]
> Voordat u doorgaat, moet u vertrouwd zijn met het configureren van SQL Server en SQL Server beschikbaarheids groepen. De volgende informatie bevat verwijzingen naar de documentatie bibliotheek en-procedures van SQL Server.


## <a name="supported-scenarios"></a>Ondersteunde scenario's

De volgende scenario's worden ondersteund voor het gebruik van beschikbaarheids groepen met Configuration Manager. Zie [Configure Availability groups for Configuration Manager](configure-aoag.md)voor meer informatie en procedures voor elk scenario.

- [Een beschikbaarheids groep maken voor gebruik met Configuration Manager](configure-aoag.md#bkmk_create)  
- [Een site configureren voor het gebruik van de beschikbaarheids groep](configure-aoag.md#bkmk_configure)  
- [Synchrone replica leden toevoegen aan of verwijderen uit een beschikbaarheids groep die als host fungeert voor een site database](configure-aoag.md#bkmk_sync)  
- [Een site configureren of herstellen vanuit een asynchrone doorvoer replica's](configure-aoag.md#bkmk_async)  
- [Een site database van een beschikbaarheids groep naar een standaard-of benoemd exemplaar van een zelfstandige SQL Server verplaatsen](configure-aoag.md#bkmk_stop)  


## <a name="prerequisites"></a>Vereisten

De volgende vereisten zijn van toepassing op alle scenario's. Als er aanvullende vereisten van toepassing zijn op een specifiek scenario, worden deze gedetailleerd beschreven in dat scenario.

### <a name="configuration-manager-accounts-and-permissions"></a>Configuration Manager accounts en machtigingen

#### <a name="installation-account"></a>Installatie account

Het account dat u gebruikt om Configuration Manager configuratie uit te voeren, moet zijn:

- Een lid van de lokale groep **Administrators** op elke computer die lid is van de beschikbaarheids groep.
- Een **sysadmin** voor elk exemplaar van SQL Server dat als host fungeert voor de site database.

#### <a name="site-server-to-replica-member-access"></a>Site server voor toegang tot replica leden

Het computer account van de site server moet lid zijn van de lokale groep **Administrators** op elke computer die lid is van de beschikbaarheids groep.

### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Versie

Elke replica in de beschikbaarheids groep moet een versie van SQL Server uitvoeren die wordt ondersteund door uw versie van Configuration Manager. Wanneer de verschillende knoop punten van een beschikbaarheids groep worden ondersteund door SQL Server, kunnen verschillende versies van SQL Server worden uitgevoerd. Zie [ondersteunde SQL Server-versies voor Configuration Manager](../../../plan-design/configs/support-for-sql-server-versions.md)voor meer informatie.<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Editie

Gebruik een *Enter prise* -editie van SQL Server.

#### <a name="account"></a>Account

Elk exemplaar van SQL Server kan worden uitgevoerd onder een domein gebruikers account (**Service account**) of een niet-domein account. Elke replica in een groep kan een andere configuratie hebben.

- Gebruik een account met de laagst mogelijke machtigingen. Zie [beveiligings overwegingen voor een SQL Server-installatie](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)voor meer informatie.  

- Zie [Windows-service accounts en-machtigingen configureren](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions)voor meer informatie over het configureren van service accounts en machtigingen voor SQL Server.  

- Als u een niet-domein account wilt gebruiken, moet u certificaten gebruiken. Zie [certificaten gebruiken voor een Data Base mirroring-eind punt (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql)voor meer informatie.  

- Zie [een Data Base mirroring-eind punt maken voor](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell)AlwaysOn-beschikbaarheids groepen voor meer informatie.  


### <a name="database"></a>Database

#### <a name="configure-the-database-on-a-new-replica"></a>De Data Base op een nieuwe replica configureren

Configureer de data base van elke replica met de volgende instellingen:  

- **CLR-integratie**inschakelen:

    ``` SQL
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
    sp_configure 'clr enabled', 1;  
    GO  
    RECONFIGURE;  
    GO
    ```

    Zie [CLR-integratie](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling)voor meer informatie.  

- Stel **maximale grootte van tekst repl** in op `2147483647` :  

    ``` SQL
    EXECUTE sp_configure 'max text repl size (B)', 2147483647
    ```

- Stel de data base-eigenaar in op het *sa-account*. U hoeft dit account niet in te scha kelen.

- De **betrouw bare** **instelling inschakelen:**

    ``` SQL
    ALTER DATABASE [CM_xxx] SET TRUSTWORTHY ON;
    ```

    Zie de [eigenschap TRUSTWORTHY data base](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property)voor meer informatie.

- De **Service Broker**inschakelen:  

    ``` SQL
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER
    ```

    > [!Note]  
    > U kunt de optie Service Broker niet inschakelen voor een Data Base die al deel uitmaakt van een beschikbaarheids groep. U moet deze optie inschakelen voordat u deze toevoegt aan de beschikbaarheids groep.<!-- SCCMDocs#1432 -->

- Configureer de Service Broker prioriteit:

    ``` SQL
    ALTER DATABASE [CM_xxx] SET HONOR_BROKER_PRIORITY ON;
    ALTER DATABASE [CM_xxx] SET ENABLE_BROKER WITH ROLLBACK IMMEDIATE

    ```

Maak deze configuraties alleen op een primaire replica. Als u een secundaire replica wilt configureren, moet u eerst een failover uitvoeren van de primaire naar de secundaire. Met deze actie wordt de secundaire nieuwe primaire replica gemaakt.

#### <a name="database-verification-script"></a>Script voor database verificatie

Voer het volgende SQL-script uit om database configuraties te controleren voor zowel primaire als secundaire replica's. Voordat u een probleem op een secundaire replica kunt oplossen, wijzigt u de secundaire replica in de primaire replica.

``` SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targeting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```


### <a name="availability-group-configurations"></a>Configuraties van beschikbaarheids groep

#### <a name="replica-members"></a>Replica leden

- De beschikbaarheids groep moet één primaire replica hebben.  

- Gebruik hetzelfde aantal en type replica's in een beschikbaarheids groep die wordt ondersteund door uw versie van SQL Server.

- U kunt een replica met asynchrone door Voer gebruiken om uw synchrone replica te herstellen. Zie Opties voor herstel van de [site database](../../manage/recover-sites.md#site-database-recovery-options)voor meer informatie.  

    > [!Warning]  
    > Configuration Manager biedt geen ondersteuning voor *failover* om de asynchrone doorvoer replica als uw site database te gebruiken. Zie [failover-en failover-modi (AlwaysOn-beschikbaarheids groepen)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups)voor meer informatie.  

Configuration Manager valideert de status van de asynchrone doorvoer replica niet om te controleren of deze actueel is. Het gebruik van een asynchrone doorvoer replica als de site database kan de integriteit van uw site en gegevens risico in beslaan. Deze replica kan niet worden gesynchroniseerd met het ontwerp. Zie [overzicht van SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)AlwaysOn-beschikbaarheids groepen voor meer informatie.

Elk lid van een replica moet de volgende configuratie hebben:

- Het *standaard exemplaar* of een *benoemd exemplaar* gebruiken  

- Met de instelling **verbindingen in primaire rol** worden **alle verbindingen toegestaan**  

- De **Lees bare secundaire** instelling is **Ja**  

- Ingeschakeld voor **hand matige failover**

    > [!Note]
    > In versie 1902 en eerder moet u alle beschikbaarheids groepen configureren op de SQL Server voor hand matige failover. Deze configuratie is vereist, zelfs als deze geen host is van de site database.
    >
    > Vanaf versie 1906 ondersteunt Configuration Manager het gebruik van de synchrone replica's van de beschikbaarheids groep als deze zijn ingesteld op **automatische failover**. Stel **hand matige failover** in wanneer:
    >
    > - U voert Configuration Manager Setup uit om het gebruik van de site database in de beschikbaarheids groep op te geven.  
    > - U installeert een update voor Configuration Manager. (Niet alleen updates die van toepassing zijn op de site database).  

- Alle leden hebben dezelfde [seeding-modus](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas)nodig.<!-- SCCMDocs-pr#3899 --> Configuration Manager Setup bevat een controle van vereisten om deze configuratie te controleren bij het maken van een Data Base via installeren of herstellen.

    > [!Note]  
    > Wanneer de data base door Setup wordt gemaakt en u **automatische** seeding configureert, moet de beschikbaarheids groep machtigingen hebben voor het maken van de data base. Deze vereiste is van toepassing op zowel een nieuwe Data Base als een herstel bewerking. Zie [automatische seeding voor secundaire replica](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas#security)voor meer informatie.<!-- SCCMDocs-pr#3900 -->

#### <a name="replica-member-location"></a>Locatie van replica-lid

Host alle replica's in een beschikbaarheids groep op locatie of host deze allemaal op Microsoft Azure. Een groep die een on-premises lid bevat en een lid in azure, wordt niet ondersteund.

> [!NOTE]
> Als u een virtuele machine van Azure gebruikt voor de SQL-Server, schakelt u **zwevende IP**in. Zie [een Load Balancer configureren voor een SQL Server AlwaysOn-beschikbaarheids groep in virtuele machines van Azure](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/availability-group-load-balancer-portal-configure)voor meer informatie.<!-- SCCMDocs#1928 -->

Configuration Manager Setup moet verbinding maken met elke replica. Wanneer u een beschikbaarheids groep in azure instelt en de groep zich achter een interne of externe load balancer bevindt, opent u de volgende standaard poorten:

- RPC-eindpunttoewijzer: **TCP 135**

- SQL Server Service Broker: **TCP 4022**  

- SQL via TCP: **tcp 1433**

Nadat de installatie is voltooid, moeten deze poorten open blijven voor Configuration Manager en Replication link Analyzer.<!-- MEMDocs#375 -->

U kunt aangepaste poorten voor deze configuraties gebruiken. Gebruik dezelfde aangepaste poorten voor het eind punt en voor alle replica's in de beschikbaarheids groep.

Voor SQL om gegevens tussen sites te repliceren, maakt u een taakverdelings regel voor elke poort in de Azure-load balancer. Zie [poorten met hoge Beschik baarheid configureren voor een interne Load Balancer](https://docs.microsoft.com/azure/load-balancer/load-balancer-configure-ha-ports)voor meer informatie.<!-- MEMDocs#252 -->

#### <a name="listener"></a>Listener

De beschikbaarheidsgroep moet ten minste één *beschikbaarheidsgroeplistener*hebben. Wanneer u Configuration Manager configureert om de site database in de beschikbaarheids groep te gebruiken, gebruikt deze de virtuele naam van deze listener. Hoewel een beschikbaarheids groep meerdere listeners kan bevatten, kan Configuration Manager slechts één listener gebruiken. Zie [een SQL Server beschikbaarheids groep-listener maken of configureren](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server)voor meer informatie.

#### <a name="file-paths"></a>Bestands paden

Wanneer u Configuration Manager Setup uitvoert om een site te configureren voor het gebruik van de data base in een beschikbaarheids groep, moet elke secundaire replica server een SQL Server bestandspad hebben dat identiek is aan het bestandspad voor de site database bestanden op de huidige primaire replica. Als een identiek pad niet bestaat, kan Setup het exemplaar voor de beschikbaarheids groep niet toevoegen als de nieuwe locatie van de site database.  

De lokale SQL Server-service account moet de machtiging **volledig beheer** voor deze map hebben.

Op de secundaire replica servers is dit bestandspad alleen vereist tijdens het gebruik van Configuration Manager Setup om het data base-exemplaar in de beschikbaarheids groep op te geven. Nadat de configuratie van de site database in de beschikbaarheids groep is voltooid, kunt u het ongebruikte pad verwijderen van secundaire replica servers.

Denk bijvoorbeeld eens aan het volgende scenario:

- U maakt een beschikbaarheids groep die gebruikmaakt van drie SQL-servers.  

- Uw primaire replicaserver is een nieuwe installatie van SQL Server 2014. Standaard wordt de data base opgeslagen. MDF en. LDF-bestanden in `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` .  

- U hebt uw secundaire replica servers bijgewerkt naar SQL Server 2014 van eerdere versies. Bij de upgrade blijven deze servers het oorspronkelijke bestandspad voor het opslaan van database bestanden: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA` .  

- Voordat u de site database naar deze beschikbaarheids groep verplaatst, maakt u op elke secundaire replica server het volgende bestandspad: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA` . Dit pad is een duplicaat van het pad dat wordt gebruikt voor de primaire replica, zelfs als de secundaire replica's deze bestands locatie niet gebruiken.  

- Vervolgens verleent u de SQL Server-service account op elke secundaire replica volledige controle over de toegang tot de zojuist gemaakte bestands locatie op die server.  

- U kunt nu Configuration Manager Setup uitvoeren om de site te configureren voor het gebruik van de site database in de beschikbaarheids groep.  

#### <a name="multi-subnet-failover"></a>Failover met meerdere subnetten

<!-- SCCMDocs-pr#3734 -->
Vanaf versie 1906 kunt u het [sleutel woord MultiSubnetFailover Connection String](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) in SQL Server inschakelen. U moet ook de volgende waarden hand matig toevoegen aan het Windows-REGI ster op de site server:

``` Registry
HKLM:\SOFTWARE\Microsoft\SMS\Identification
HKLM:\SOFTWARE\Microsoft\SMS\SQL Server

MSF Enabled : 1 (DWORD)
```

> [!Warning]  
> Het gebruik van de [hoge Beschik baarheid van de site server](site-server-high-availability.md) en SQL Server altijd met failover met meerdere subnetten bieden niet de volledige mogelijkheden van een automatische failover voor nood herstel scenario's.

Als u een beschikbaarheids groep met een lid op een externe locatie wilt maken, geeft u een prioriteit op basis van de laagste netwerk latentie. Hoge netwerk latentie kan leiden tot replicatie fouten.<!-- SCCMDocs#1381 -->


## <a name="limitations-and-known-issues"></a>Beperkingen en bekende problemen

De volgende beperkingen zijn van toepassing op alle scenario's.

### <a name="unsupported-sql-server-options-and-configurations"></a>Niet-ondersteunde SQL Server opties en configuraties

- **Basis beschikbaarheids groepen**die zijn geïntroduceerd met SQL Server 2016 Standard Edition, bieden geen ondersteuning voor lees toegang tot secundaire replica's. Voor de configuratie is deze toegang vereist. Zie voor meer informatie [Basic-SQL Server-beschikbaarheids groepen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Failover-cluster exemplaar**: exemplaren van failoverclusters worden niet ondersteund voor een replica die u gebruikt met Configuration Manager. Zie [SQL Server always on failover cluster instances](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server)voor meer informatie.  

- **MultiSubnetFailover**: in versie 1902 en lager, wordt niet ondersteund voor het gebruik van een beschikbaarheids groep met Configuration Manager in een configuratie met meerdere subnetten. U kunt ook het tref woord connection string [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) niet gebruiken.

    Als u deze configuratie wilt ondersteunen, moet u Configuration Manager bijwerken naar versie 1906 of hoger. Zie voor meer informatie de [failover-vereiste voor meerdere subnetten](sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover) .

### <a name="sql-servers-that-host-additional-availability-groups"></a>SQL-servers die extra beschikbaarheids groepen hosten

<!--SCCMDocs issue 649-->
Wanneer de SQL Server een of meer beschikbaarheids groepen host naast de groep die u voor Configuration Manager gebruikt, heeft deze specifieke instellingen nodig op het moment dat u Configuration Manager Setup uitvoert. Deze instellingen zijn ook nodig voor het installeren van een update voor Configuration Manager. Elke replica in elke beschikbaarheids groep moet de volgende configuraties hebben:

- Hand matige failover  
- Wille keurige alleen-lezen verbinding toestaan  

> [!Note]
> In versie 1902 en eerder moet u alle beschikbaarheids groepen configureren op de SQL Server voor hand matige failover. Deze configuratie is vereist, zelfs als deze geen host is van de site database.
>
> Vanaf versie 1906 ondersteunt Configuration Manager het gebruik van de synchrone replica's van de beschikbaarheids groep als deze zijn ingesteld op **automatische failover**. Stel **hand matige failover** in wanneer:
>
> - U voert Configuration Manager Setup uit om het gebruik van de site database in de beschikbaarheids groep op te geven.  
> - U installeert een update voor Configuration Manager. (Niet alleen updates die van toepassing zijn op de site database).  

### <a name="unsupported-database-use"></a>Niet-ondersteund database gebruik

#### <a name="configuration-manager-supports-only-the-site-database-in-an-availability-group"></a>Configuration Manager ondersteunt alleen de site database in een beschikbaarheids groep

De volgende data bases worden niet ondersteund door Configuration Manager in een SQL Server AlwaysOn-beschikbaarheids groep:  

- Rapportagedatabase  
- WSUS-database  

#### <a name="pre-existing-database"></a>Vooraf bestaande data base

U kunt geen nieuwe Data Base gebruiken die op de replica is gemaakt. Wanneer u een beschikbaarheids groep configureert, herstelt u een kopie van een bestaande Configuration Manager-Data Base naar de primaire replica.  

#### <a name="distributed-views"></a>Gedistribueerde weergaven

<!-- SCCMDocs-pr#3792 -->
Als u in versie 1902 en eerder de site database host op een SQL Server AlwaysOn-beschikbaarheids groep, kunt u [gedistribueerde weer gaven](../../../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) niet inschakelen voor database replicatie. Als u deze configuratie wilt ondersteunen, moet u bijwerken naar versie 1906 of hoger.


### <a name="setup-errors-in-configmgrsetuplog"></a>Setup-fouten in ConfigMgrSetup. log

Wanneer u Configuration Manager Setup uitvoert om een site database te verplaatsen naar een beschikbaarheids groep, probeert database rollen te verwerken op secundaire replica's van de beschikbaarheids groep. In het bestand **ConfigMgrSetup. log** wordt de volgende fout weer gegeven:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Deze fouten zijn veilig om te negeren.

### <a name="site-expansion"></a>Site-uitbrei ding

<!--SCCMDocs issue 568-->
Als u de site database voor een zelfstandige primaire site configureert voor het gebruik van SQL AlwaysOn, kunt u de site niet uitbreiden voor het toevoegen van een centrale beheer site. Als u dit proces probeert, mislukt dit. Als u de site wilt uitbreiden, moet u de data base van de primaire site tijdelijk verwijderen uit de beschikbaarheids groep.

U hoeft geen wijzigingen aan te brengen in de configuratie wanneer u een secundaire site toevoegt.


## <a name="changes-for-site-backup"></a>Wijzigingen voor site back-up

### <a name="backup-database-files"></a>Back-up van database bestanden
  
Wanneer een site database gebruikmaakt van een beschikbaarheids groep, voert u de ingebouwde onderhouds taak van de **back-upserver van site** uit om een back-up te maken van algemene Configuration Manager instellingen en-bestanden. Gebruik niet de. MDF of. LDF-bestanden die door deze back-up zijn gemaakt. Maak in plaats daarvan directe back-ups van deze database bestanden met behulp van SQL Server.

### <a name="transaction-log"></a>Transactie logboek  

Stel het herstel model van de site database in op **Full**. Deze configuratie is een vereiste voor het Configuration Manager gebruiken in een beschikbaarheids groep. Plan de grootte van het transactie logboek van de site database te controleren en te onderhouden. In het volledige herstel model worden de trans acties niet gehard totdat een volledige back-up van de data base of het transactie logboek wordt gemaakt. Zie [back-up en herstel van SQL server-data bases](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases)voor meer informatie.


## <a name="changes-for-site-recovery"></a>Wijzigingen voor site Recovery

Als ten minste één knoop punt van de beschikbaarheids groep nog steeds functioneel is, gebruikt u de site Recovery-optie om **database herstel over te slaan (deze optie gebruiken als de site database onbeschadigd is)**.

Vanaf versie 1906 kan site Recovery de data base opnieuw maken op basis van een SQL always on-groep. Dit proces werkt met zowel hand matige als automatische seeding.<!-- SCCMDocs-pr#3846 -->

Wanneer u in versie 1902 of eerder alle knoop punten van een beschikbaarheids groep kwijtraakt, moet u eerst de beschikbaarheids groep opnieuw maken voordat u de site kunt herstellen. Configuration Manager kan het beschikbaarheids knooppunt niet opnieuw samen stellen of herstellen. Maak de groep opnieuw, herstel de back-up en configureer de SQL-Server opnieuw. Gebruik vervolgens de site Recovery-optie om **database herstel over te slaan (gebruik deze optie als de site database onbeschadigd is)**.

Zie [back-up en herstel](../../manage/backup-and-recovery.md)voor meer informatie.


## <a name="changes-for-reporting"></a>Wijzigingen voor rapportage

### <a name="install-the-reporting-service-point"></a>Het Reporting service-punt installeren

Het Reporting Services-punt biedt geen ondersteuning voor het gebruik van de virtuele listener-naam van de beschikbaarheids groep. Er wordt ook geen ondersteuning geboden voor het hosten van de data base in een SQL Server AlwaysOn-beschikbaarheids groep.  

- Standaard wordt de naam van de **site database server** door de Reporting Services-punt installatie ingesteld op de virtuele naam die is opgegeven als listener. Wijzig deze instelling om een computer naam en exemplaar van een replica in de beschikbaarheids groep op te geven.  

- Als u de rapportage wilt offloaden en de beschik baarheid wilt verg Roten wanneer een replica knooppunt offline is, kunt u overwegen extra Reporting Services-punten op elk replica knooppunt te installeren. Configureer vervolgens elk Reporting Services-punt voor het gebruik van de eigen computer naam. Wanneer u een Reporting service-punt installeert op elke replica van de beschikbaarheids groep, kan Reporting altijd verbinding maken met een actieve Reporting Point-server.  

### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Het Reporting Services-punt dat wordt gebruikt door de console, overschakelen

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en selecteer het knoop punt **rapporten** .

1. Selecteer in het lint **rapport opties**.  

1. Selecteer in het dialoog venster rapport opties het Reporting Services-punt dat u wilt gebruiken.  


## <a name="next-steps"></a>Volgende stappen

In dit artikel worden de vereisten, beperkingen en wijzigingen beschreven in algemene taken die Configuration Manager vereist wanneer u beschikbaarheids groepen gebruikt. Zie [beschikbaarheids groepen configureren](configure-aoag.md)voor procedures voor het instellen en configureren van uw site voor het gebruik van beschikbaarheids groepen.
