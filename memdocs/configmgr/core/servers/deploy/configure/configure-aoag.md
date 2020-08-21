---
title: Beschikbaarheids groepen configureren
titleSuffix: Configuration Manager
description: SQL Server AlwaysOn-beschikbaarheids groepen instellen en beheren met Configuration Manager
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e85b36d0caeb6ceb99f56220e271774dc0db0f6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699242"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>SQL Server AlwaysOn-beschikbaarheids groepen configureren voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de informatie in dit artikel voor het configureren en beheren van de beschikbaarheids groepen die u gebruikt met Configuration Manager.

Voordat u begint:  

- Zorg ervoor dat u bekend bent met de informatie over het voorbereiden van het gebruik van SQL Server AlwaysOn- [beschikbaarheids groepen met Configuration Manager](sql-server-alwayson-for-a-highly-available-site-database.md).
- Zorg dat u bekend bent met SQL Server documentatie waarin het gebruik van beschikbaarheids groepen en gerelateerde procedures wordt beschreven. Deze informatie is vereist voor het volt ooien van de volgende scenario's.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> Een beschikbaarheids groep maken en configureren

Gebruik de volgende procedure om een beschikbaarheids groep te maken en vervolgens een kopie van de site database naar die beschikbaarheids groep te verplaatsen.

1. Gebruik de volgende opdracht om de Configuration Manager-site te stoppen:

    `preinst.exe /stopsite`

    Zie [Hierarchy maintenance tool](../../manage/hierarchy-maintenance-tool-preinst.exe.md)(Engelstalig) voor meer informatie.

2. Wijzig het back-upmodel voor de site database van **eenvoudig** in **volledig**:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Beschikbaarheids groepen bieden alleen ondersteuning voor het volledige back-upmodel. Zie [het herstel model van een Data Base weer geven of wijzigen](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)voor meer informatie.

3. Gebruik SQL Server om een volledige back-up te maken van uw site database. Kies een van de volgende opties:

    - **Is lid van uw beschikbaarheids groep**: als u deze server gebruikt als eerste lid van de groep voor primaire replica's, hoeft u geen kopie van de site database te herstellen naar deze server of een andere in de groep. De data base is al aanwezig op de primaire replica. SQL Server repliceert de Data Base naar de secundaire replica's tijdens een latere stap.  

    - Is **geen lid van de beschikbaarheids groep**: herstel een kopie van de site database naar de server die als host fungeert voor de primaire replica van de groep.

    Raadpleeg de volgende artikelen in de SQL Server-documentatie voor meer informatie:

    - [Een volledige back-up van de data base maken](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Een Data Base-back-up terugzetten met behulp van SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Als u van plan bent om van een beschikbaarheids groep naar een zelfstandige te gaan op een bestaande replica, verwijdert u eerst de data base uit de beschikbaarheids groep.

4. Op de server die als host moet fungeren voor de eerste primaire replica van de groep, gebruikt u de [wizard Nieuwe beschikbaarheids groep](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) om de beschikbaarheids groep te maken. In de wizard:

    - Selecteer op de pagina **Data Base selecteren** de Data Base voor uw Configuration Manager-site.  

    - Configureer op de pagina **Replica's opgeven** het volgende:

        - **Replica's:** Geef de servers op die als host dienen voor secundaire replica's.

        - **Listener:** Geef de **DNS-naam** van de listener op als een volledige DNS-naam, bijvoorbeeld `<listener_server>.fabrikam.com` . Wanneer u Configuration Manager configureert voor het gebruik van de data base in de beschikbaarheids groep, wordt deze naam gebruikt.

    - Selecteer op de pagina **Eerste gegevenssynchronisatie selecteren** de optie **Volledig**. Nadat de wizard de beschikbaarheids groep heeft gemaakt, maakt de wizard een back-up van de primaire data base en het transactie logboek. Vervolgens worden ze door de wizard hersteld op elke server die als host fungeert voor een secundaire replica.

        > [!Note]  
        > Als u deze stap niet gebruikt, herstelt u een kopie van de site database op elke server die als host fungeert voor een secundaire replica. Voeg deze data base vervolgens hand matig toe aan de groep.

5. Controleer de configuratie van elke replica:

    1. Zorg ervoor dat het computer account van de site server lid is van de lokale groep **Administrators** op elke computer die lid is van de beschikbaarheids groep.  

    2. Voer het [verificatie script](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites) uit om te controleren of de site database op elke replica correct is geconfigureerd.

    3. Als het nodig is om configuraties in te stellen op secundaire replica's, moet u, voordat u doorgaat, hand matig een failover uitvoeren van de primaire replica naar de secundaire replica. U kunt de data base van een primaire replica alleen configureren. Zie [een geplande hand matige failover van een beschikbaarheids groep uitvoeren](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) in de documentatie van SQL Server voor meer informatie.

6. Nadat alle replica's voldoen aan de vereisten, kan de beschikbaarheids groep worden gebruikt met Configuration Manager.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> Een site configureren voor het gebruik van de beschikbaarheids groep

Nadat u [de beschikbaarheids groep hebt gemaakt en geconfigureerd](#bkmk_create), gebruikt u Configuration Manager site onderhoud om de site te configureren voor het gebruik van de data base die wordt gehost door de beschikbaarheids groep.

Het is niet mogelijk om een nieuwe site te installeren met de bijbehorende data base in een beschikbaarheids groep. Als u bijvoorbeeld basislijn media gebruikt, installeert u de site met behulp van één exemplaar van SQL Server. Nadat de site is geïnstalleerd, verplaatst u de site database naar de beschikbaarheids groep.

1. Voer **Configuration Manager Setup** `\BIN\X64\setup.exe` uit: vanuit de installatiemap van de Configuration Manager-site.

2. Selecteer op de pagina **aan de slag** de optie **site onderhoud uitvoeren of deze site opnieuw instellen**en selecteer vervolgens **volgende**.

3. Selecteer **SQL Server configuratie wijzigen**en selecteer **volgende**.

4. Configureer de volgende instellingen opnieuw voor de site database:

    - **SQL Server naam**: Voer de virtuele naam in voor de beschikbaarheids groep- *listener*. U hebt de listener geconfigureerd tijdens het maken van de beschikbaarheids groep. De virtuele naam moet een volledige DNS-naam zijn, zoals `<Listener_Server>.fabrikam.com` .  

    - **Exemplaar:** Als u het standaard exemplaar voor de *listener* van de beschikbaarheids groep wilt opgeven, moet deze waarde leeg zijn. Als de huidige site database wordt uitgevoerd op een benoemd exemplaar, wist u het huidige benoemde exemplaar.

    - **Database** : laat de weergegeven naam ongewijzigd. Deze naam is de huidige site database.

5. Nadat u de informatie voor de nieuwe locatie van de Data Base hebt verstrekt, voltooit u de installatie met uw normale proces en configuraties.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> Synchrone replica leden  

Als uw site database wordt gehost in een beschikbaarheids groep, gebruikt u de volgende procedures om synchrone replica leden toe te voegen of te verwijderen. Zie [configuraties van beschikbaarheids groepen](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations)voor meer informatie over het ondersteunde type en aantal replica's.

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a> Een nieuw lid van de synchrone replica toevoegen

<!--3127336-->
Voer in versie 1906 het Configuration Manager-installatie programma uit om een nieuw lid van de synchrone replica toe te voegen.

1. Voeg een secundaire replica toe met behulp van de SQL Server procedures.

    1. [Voeg een secundaire replica toe aan een](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)AlwaysOn-beschikbaarheids groep.

    1. Bekijk de status in SQL Management Studio. Wacht totdat de beschikbaarheids groep naar de volledige status terugkeert.

1. Voer Configuration Manager Setup uit en selecteer de optie om de site te wijzigen.

1. Geef de naam van de beschikbaarheids groep-listener op als de database naam. Als de listener een niet-standaard netwerk poort gebruikt, geeft u dit ook op. Met deze actie zorgt u ervoor dat elk knoop punt op de juiste wijze is geconfigureerd. Er wordt ook een herstel proces voor de data base gestart.

Configuration Manager Setup gebruikt de SQL database Move-bewerking en zorgt ervoor dat de knoop punten correct zijn geconfigureerd.

Voor meer informatie over hoe u dit proces hand matig doet in versie 1902 of eerder, Zie [ConfigMgr 1702: een nieuw knoop punt (secundaire replica) toevoegen aan een bestaande SQL ao AG](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960).

### <a name="remove-a-replica-member"></a>Een lid van een replica verwijderen

Vanaf versie 1906 kunt u Configuration Manager Setup gebruiken om een lid van een replica te verwijderen. Gebruik hetzelfde proces voor het [toevoegen van een nieuw lid van de synchrone replica](#bkmk_sync-add).

Zie [een secundaire replica uit een beschikbaarheids groep verwijderen](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server)voor meer informatie over hoe u dit proces hand matig kunt uitvoeren in versie 1902 of eerder.  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> Asynchrone replica's

U kunt een asynchrone replica gebruiken in de beschikbaarheids groep die u gebruikt met Configuration Manager. U hoeft de vereiste configuratie scripts voor het configureren van een synchrone replica niet uit te voeren, omdat een asynchrone replica niet wordt ondersteund voor de site database.

### <a name="configure-an-asynchronous-commit-replica"></a>Een asynchrone doorvoer replica configureren

Zie [een secundaire replica toevoegen aan een beschikbaarheids groep](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server)voor meer informatie.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>De asynchrone replica gebruiken om uw site te herstellen

Gebruik de asynchrone replica om uw site database te herstellen.

1. De actieve primaire site stoppen om te voor komen dat er extra schrijf bewerkingen naar de site database worden uitgevoerd. Als u de site wilt stoppen, gebruikt u het [hulp programma voor hiërarchie onderhoud](../../manage/hierarchy-maintenance-tool-preinst.exe.md): `preinst.exe /stopsite`

1. Nadat u de site hebt gestopt, gebruikt u de asynchrone replica in plaats van een [hand matig herstelde data base](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a> Stoppen met het gebruik van een beschikbaarheids groep

Voer de volgende procedure uit als u de sitedatabase niet meer wilt hosten in een beschikbaarheidsgroep. Met dit proces verplaatst u de site database terug naar één exemplaar van SQL Server.

1. Stop de Configuration Manager-site met behulp van de volgende opdracht: `preinst.exe /stopsite` . Zie [Hierarchy maintenance tool](../../manage/hierarchy-maintenance-tool-preinst.exe.md)(Engelstalig) voor meer informatie.

2. Maak met behulp van SQL Server een volledige back-up van uw sitedatabase vanaf de primaire replica: Zie [een volledige back-up van de data base maken](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)voor meer informatie.

3. Herstel met SQL Server de back-up van de sitedatabase naar de server die als host voor de sitedatabase moet dienen. Zie [een back-up van een Data Base terugzetten met behulp van SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)voor meer informatie.

    > [!Note]  
    > Als de primaire replica server voor de beschikbaarheids groep als host fungeert voor één exemplaar van de site database, slaat u deze stap over.

4. Op de server die als host moet fungeren voor de site database, wijzigt u het back-upmodel voor de site database van **volledig** in **eenvoudig**. Zie [het herstel model van een Data Base weer geven of wijzigen](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server)voor meer informatie.

5. Voer **Configuration Manager Setup** `\BIN\X64\setup.exe` uit: vanuit de installatiemap van de Configuration Manager-site.

6. Selecteer op de pagina **aan de slag** de optie **site onderhoud uitvoeren of deze site opnieuw instellen**en selecteer vervolgens **volgende**.  

7. Selecteer **SQL Server configuratie wijzigen**en selecteer **volgende**.  

8. Configureer de volgende instellingen opnieuw voor de site database:

    - **SQL Server-naam:** geef de naam op van de server die nu als host dient voor de sitedatabase.

    - **Exemplaar:** Geef het benoemde exemplaar op dat als host fungeert voor de site database. Als de data base zich op het standaard exemplaar bevindt, laat u dit veld leeg.

    - **Database** : laat de weergegeven naam ongewijzigd. Deze naam is de huidige site database.

9. Nadat u de informatie voor de nieuwe locatie van de Data Base hebt verstrekt, voltooit u de installatie met uw normale proces en configuraties. Wanneer het installatie programma is voltooid, wordt de site opnieuw opgestart en wordt de nieuwe locatie van de data base gebruikt.

10. Volg de richt lijnen in [een beschikbaarheids groep verwijderen](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server)om de servers op te schonen die lid waren van de beschikbaarheids groep.