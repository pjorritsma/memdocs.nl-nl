---
title: Site Recovery
titleSuffix: Configuration Manager
description: Meer informatie over het herstellen van uw sites in Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b17c8c9ed0c1f6f9a5aeb487e07ad3d3dc66cbae
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82903960"
---
# <a name="recover-a-configuration-manager-site"></a>Een Configuration Manager-site herstellen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Een Configuration Manager site Recovery uitvoeren nadat een site is mislukt of gegevens verlies optreedt in de site database. Het herstellen en opnieuw synchroniseren van gegevens zijn de belangrijkste taken van een siteherstel en zijn nodig om een onderbreking van de bewerkingen te voorkomen.

De secties in dit artikel kunnen u helpen bij het herstellen van een Configuration Manager-site. Zie [back-up voor Configuration Manager voor](backup-and-recovery.md)het maken van een back-up.

## <a name="considerations-before-recovering-a-site"></a>Overwegingen voor het herstellen van een site

> [!Important]  
> Deze informatie is alleen van toepassing op site Recovery-scenario's. Als u een upgrade uitvoert van uw on-premises infra structuur en een mislukte site niet actief herstelt, raadpleegt u de informatie in de volgende artikelen:
>
> - [Lokale infrastructuur bijwerken](upgrade-on-premises-infrastructure.md)
> - [Uw infrastructuur wijzigen](modify-your-infrastructure.md)

### <a name="prepare-the-server-hardware"></a>De serverhardware voorbereiden

<!-- 2841893 -->

Zorg ervoor dat bestaande configuraties niet aanwezig zijn op de site server. Eerdere configuraties kunnen conflicten veroorzaken tijdens het herstel proces van de site. Gebruik een van de volgende opties voor de serverhardware:

- Gebruik een nieuwe server die voldoet aan de vereisten voor algemeen gebruik en herstel.

- Format teer de schijven en installeer het besturings systeem op de bestaande server opnieuw. Zorg ervoor dat het voldoet aan de algemene en herstel vereisten.

- Een bestaande server die u hebt opgeschoond opnieuw gebruiken

Gebruik een van de volgende procedures om een bestaande server op te schonen:

#### <a name="clean-an-existing-server-for-site-server-recovery-only"></a>Een bestaande server alleen voor herstel van de site server opschonen

1. SMS-register sleutels verwijderen:`HKLM\Software\Microsoft\SMS`
2. Verwijder register vermeldingen die beginnen met `SMS` van `HKLM\System\CurrentControlSet\Services` . Bijvoorbeeld:
    - SMS_DISCOVERY_DATA_MANAGER
    - SMS_EXECUTIVE
    - SMS_INBOX_MONITOR
    - SMS_INVENTORY_DATA_LOADER
    - SMS_LAN_SENDER
    - SMS_MP_FILE_DISPATCH_MANAGER
    - SMS_SCHEDULER
    - SMS_SITE_BACKUP
    - SMS_SITE_COMPONENT_MANAGER
    - SMS_SITE_SQL_BACKUP
    - SMS_SITE_VSS_WRITER
    - SMS_SOFTWARE_METERING_PROCESSOR
    - SMS_STATE_SYSTEM
    - SMS_STATUS_MANAGER
    - SMS_WSUS_SYNC_MANAGER
    - SMSvcHost 3.0.0.0
    - SMSvcHost 4.0.0.0
3. De Configuration Manager-console verwijderen
4. Start de server opnieuw
5. Controleer of alle bovenstaande register sleutels zijn verwijderd.

De server is nu gereed voor de procedure voor het herstellen van Configuration Manager.

#### <a name="clean-an-existing-server-for-site-database-recovery-only"></a>Een bestaande server alleen voor herstel van de site database opschonen

1. Maak een back-up van de site database. Maak ook een back-up van alle andere ondersteunende data bases, zoals WSUS.
2. Noteer de naam van de SQL-Server en de exemplaar naam
3. De site database hand matig verwijderen uit de SQL Server
4. De SQL Server opnieuw opstarten

De server is nu gereed voor de procedure voor het herstellen van Configuration Manager.

#### <a name="clean-an-existing-server-for-full-recovery"></a>Een bestaande server opschonen voor volledig herstel

1. Maak een back-up van de site database. Maak ook een back-up van alle andere ondersteunende data bases, zoals WSUS.
2. Een kopie maken van de inhouds bibliotheek
3. De site database hand matig verwijderen uit de SQL Server
4. De Configuration Manager-site verwijderen
5. Verwijder de Configuration Manager installatiemap en alle andere Configuration Manager mappen hand matig
6. Start de server opnieuw
7. De inhouds bibliotheek en andere data bases zoals WSUS herstellen

De server is nu gereed voor de procedure voor het herstellen van Configuration Manager.

### <a name="use-a-supported-version-and-same-edition-of-sql-server"></a>Een ondersteunde versie en dezelfde editie van SQL Server gebruiken

<!-- SCCMDocs#751 -->

Gebruik, indien mogelijk, dezelfde versie van SQL Server. Het is echter wel mogelijk om een Data Base te herstellen naar een nieuwere versie.

Wijzig de SQL Server versie niet. Het herstellen van een site database van Standard Edition naar Enter prise Edition wordt niet ondersteund.

Aanvullende SQL Server configuratie vereisten:

- SQL Server kan niet worden ingesteld op de **modus voor één gebruiker**.
- Controleer of de MDF-en LDF-bestanden geldig zijn. Wanneer u een site herstelt, wordt er niet gecontroleerd op de status van de bestanden.  

### <a name="sql-server-always-on-availability-groups"></a>SQL Server AlwaysOn-beschikbaarheidsgroepen

Als u SQL Server AlwaysOn-beschikbaarheids groepen gebruikt om de site database te hosten, wijzigt u de herstel plannen, zoals wordt beschreven in [voor bereiding voor het gebruik van SQL Server always on](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-recovery).

### <a name="database-replicas"></a>Database replica's

Nadat u een site database hebt hersteld die u hebt geconfigureerd voor database replica's, moet u elke replica opnieuw configureren. Voordat u de database replica's kunt gebruiken, moet u de publicaties en abonnementen opnieuw maken.

## <a name="determine-your-recovery-options"></a>Uw herstelopties bepalen

Er zijn twee hoofd gebieden waarmee u rekening moet houden voor Configuration Manager primaire site server en het herstellen van de centrale beheer site (CAS): de **Site Server** en de **site database**.
De volgende secties kunnen u helpen bij het selecteren van de beste opties voor uw herstel scenario.

> [!NOTE]  
> Wanneer Configuration Manager Setup een bestaande site op de server detecteert, kunt u een site herstel starten, maar de herstel opties voor de site server zijn beperkt. Als u het installatieprogramma bijvoorbeeld uitvoert op een bestaande siteserver, wanneer u herstel kiest, kunt u de sitedatabaseserver herstellen, maar is de optie om de siteserver te herstellen uitgeschakeld.

### <a name="site-server-recovery-options"></a>Opties voor herstel van de siteserver

Configuration Manager Setup starten vanuit een kopie van de **cd. De meest recente** map die u hebt gemaakt buiten de map Configuration Manager installation.  

- Als u Setup vanuit het menu **Start** op de site server uitvoert, is de optie **een site herstellen** niet beschikbaar.  

- Als u updates hebt geïnstalleerd vanuit de Configuration Manager-console voordat u een back-up hebt gemaakt, kunt u de site niet opnieuw installeren met behulp van de installatie vanaf de volgende locaties:

  - Installatie media
  - Het installatiepad van Configuration Manager

Selecteer vervolgens de optie **een site herstellen** . U hebt de volgende herstel opties voor de mislukte site server:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>De site server herstellen met een bestaande back-up

Gebruik deze optie wanneer u een Configuration Manager back-up van de site server hebt voordat de site fout is opgetreden. De site maakt deze back-up als onderdeel van de onderhouds taak van de **back-upserver van site** . De site wordt opnieuw geïnstalleerd en de site-instellingen worden geconfigureerd op basis van de site waarvan een back-up is gemaakt.  

#### <a name="reinstall-the-site-server"></a>De site server opnieuw installeren

Gebruik deze optie wanneer u geen back-up van de site server hebt. De site server wordt opnieuw geïnstalleerd en u moet de site-instellingen opgeven zoals u dat tijdens een eerste installatie zou doen.  

- Dezelfde site code en site database naam gebruiken die u hebt gebruikt toen de mislukte site voor het eerst werd geïnstalleerd.  

- U kunt de site opnieuw installeren op een nieuwe computer waarop een nieuwe versie van het besturings systeem wordt uitgevoerd.  

- De server moet dezelfde hostnaam en Fully Qualified Domain Name (FQDN) van de oorspronkelijke site server gebruiken.

### <a name="site-database-recovery-options"></a>Opties voor herstel van de sitedatabase

Wanneer u Configuration Manager Setup uitvoert, hebt u de volgende herstel opties voor de site database:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>De site database herstellen met een back-upset

Gebruik deze optie wanneer u een Configuration Manager back-up van de site database hebt voordat de data base is mislukt. De site maakt deze back-up als onderdeel van de onderhouds taak van de **back-upserver van site** . Bij het herstellen van een primaire site, haalt het herstel proces in een hiërarchie alle wijzigingen op die zijn aangebracht in de site database na de laatste back-up. Bij het herstellen van de CAS haalt het herstel proces deze wijzigingen op uit een primaire referentie site. Wanneer u de site database voor een zelfstandige primaire site herstelt, gaan de site wijzigingen na de laatste back-up verloren.  

Wanneer u de site database voor een site in een hiërarchie herstelt, is het herstel gedrag verschillend voor een certificerings instantie en een primaire site. Het gedrag verschilt ook wanneer de laatste back-up binnen of buiten de Bewaar periode van SQL Server wijzigingen bijhouden. Zie de sectie [herstel scenario's voor site database](#site-database-recovery-scenarios) in dit artikel voor meer informatie.  

> [!NOTE]  
> Als u de site database herstelt met behulp van een back-upset, maar de site database al bestaat, mislukt de herstel bewerking.  

#### <a name="create-a-new-database-for-this-site"></a>Een nieuwe data base maken voor deze site

Gebruik deze optie wanneer u geen back-up van de site database hebt. In een hiërarchie wordt met het herstel proces een nieuwe site database gemaakt. Bij het herstellen van een onderliggende primaire site worden de gegevens hersteld door te repliceren van de CAS. Bij het herstellen van de CAS worden gegevens uit een primaire referentie site gerepliceerd. Deze optie is niet beschikbaar wanneer u een zelfstandige primaire site herstelt of een certificerings instantie die geen primaire sites heeft.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Een site database gebruiken die hand matig is hersteld

Gebruik deze optie wanneer u de data base van de Configuration Manager-site al hebt hersteld, maar het herstel proces moet volt ooien.  

- Configuration Manager kunt de site database herstellen vanuit een van de volgende processen:  

  - De Configuration Manager onderhouds taak voor back-up  
  - Een back-up van de site database met behulp van Data Protection Manager (DPM)  
  - Een ander back-upproces  

    Nadat u de site database hebt hersteld met behulp van een methode buiten Configuration Manager, voert u Setup uit en selecteert u deze optie om het herstel van de site database te volt ooien.  

    > [!NOTE]  
    > Wanneer u DPM gebruikt om een back-up te maken van uw site database, gebruikt u de DPM-procedures om de site database te herstellen naar een opgegeven locatie voordat u doorgaat met het herstel proces in Configuration Manager. Zie de documentatie bibliotheek van [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) voor meer informatie over DPM.  

- Wanneer u een primaire site database herstelt, haalt het herstel proces in een hiërarchie alle wijzigingen op die zijn aangebracht in de site database na de laatste back-up. Bij het herstellen van de CAS haalt het herstel proces deze wijzigingen op uit een primaire referentie site. Wanneer u de site database voor een zelfstandige primaire site herstelt, gaan de site wijzigingen na de laatste back-up verloren.  

#### <a name="skip-database-recovery"></a>Database herstel overs Laan

Gebruik deze optie wanneer er geen gegevens verlies is opgetreden op de Configuration Manager-site database server. Deze optie is alleen geldig wanneer de site database zich op een andere computer bevindt dan de site server die u wilt herstellen.  

### <a name="sql-server-change-tracking-retention-period"></a>Bewaarperiode voor het bijhouden van wijzigingen van de SQL Server

Configuration Manager kunt wijzigingen bijhouden inschakelen voor de site database in SQL Server. Met de functie voor het bijhouden van wijzigingen kan Configuration Manager query's uitvoeren op informatie over de wijzigingen die zijn aangebracht in database tabellen na een eerder tijdstip. De Bewaar periode geeft aan hoe lang de gegevens voor het bijhouden van wijzigingen worden bewaard. De site database is standaard geconfigureerd voor een Bewaar periode van vijf dagen. Wanneer u een sitedatabase herstelt, vindt het herstelproces anders plaats als uw back-up binnen of buiten de bewaarperiode valt. Als uw SQL Server bijvoorbeeld uitvalt en uw laatste back-up zeven dagen oud is, is het buiten de Bewaar periode.

Voor meer informatie over SQL Server interne wijzigingen bijhouden raadpleegt u de volgende blog berichten van het SQL Server team: [Wijzigingen bijhouden opschonen-deel 1](https://docs.microsoft.com/archive/blogs/sql_server_team/change-tracking-cleanup-part-1) en [Wijzigingen bijhouden opschoning onderdeel 2](https://docs.microsoft.com/archive/blogs/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Opnieuw initialiseren van site of globale gegevens

Het proces om site- of algemene gegevens opnieuw te initialiseren vervangt bestaande gegevens in de sitedatabase door gegevens uit een andere sitedatabase. Wanneer site ABC bijvoorbeeld gegevens opnieuw initialiseert van site XYR, dan vinden de volgende stappen plaats:

- De gegevens worden van site XYZ naar site ABC gekopieerd.
- De bestaande gegevens voor site XYZ worden verwijderd uit de sitedatabase op site ABC.
- De gekopieerde gegevens van site XYZ worden opgenomen in de sitedatabase op site ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-cas"></a>Voorbeeld scenario 1: de primaire site initialiseert de globale gegevens van de CAS opnieuw

Het herstel proces verwijdert de bestaande algemene gegevens voor de primaire site in de data base van de primaire site en vervangt de gegevens door de algemene gegevens die zijn gekopieerd uit de certificerings instantie.

#### <a name="example-scenario-2-the-cas-reinitializes-the-site-data-from-a-primary-site"></a>Voorbeeld scenario 2: de certificerings instantie initialiseert de site gegevens van een primaire site opnieuw

Het herstel proces verwijdert de bestaande site gegevens voor die primaire site in de CAS-data base. De gegevens worden vervangen door de site gegevens die zijn gekopieerd van de primaire site. De site gegevens voor andere primaire sites worden niet beïnvloed.

### <a name="site-database-recovery-scenarios"></a>Scenario's voor het herstel van een sitedatabase

Nadat een site database is hersteld op basis van een back-up, probeert Configuration Manager de wijzigingen in de site en algemene gegevens na de laatste back-up van de data base te herstellen. Configuration Manager start de volgende acties nadat een site database is hersteld vanuit een back-up:  

#### <a name="recovered-site-is-a-cas"></a>De herstelde site is een CAS

- Back-up van database binnen de bewaarperiode voor het bijhouden van wijzigingen  

  - **Globale gegevens**: de wijzigingen in algemene gegevens na de back-up worden gerepliceerd van alle primaire sites.  

  - **Site gegevens**: de wijzigingen in site gegevens na de back-up worden gerepliceerd van alle primaire sites.  

- Databaseback-up ouder is dan de bewaarperiode voor het bijhouden van wijzigingen  

  - **Globale gegevens**: de CAS initialiseert de globale gegevens uit de primaire referentie site opnieuw als u deze opgeeft. Vervolgens initialiseren alle andere primaire sites de algemene gegevens uit de certificerings instantie opnieuw. Als u geen referentie site opgeeft, initialiseren alle primaire sites de algemene gegevens uit de certificerings instantie opnieuw. Deze gegevens worden teruggezet vanuit een back-up.  

  - **Site gegevens**: de CAS initialiseert de site gegevens van elke primaire site opnieuw.  

#### <a name="recovered-site-is-a-primary-site"></a>De herstelde site is een primaire site

- Back-up van database binnen de bewaarperiode voor het bijhouden van wijzigingen  

  - **Globale gegevens**: de wijzigingen in globale gegevens na de back-up worden gerepliceerd vanuit de CAS.  

  - **Site gegevens**: de CAS initialiseert de site gegevens van de primaire site opnieuw. Wijzigingen na de back-up gaan verloren. Clients genereren de meeste gegevens opnieuw wanneer ze informatie verzenden naar de primaire site.  

- Databaseback-up ouder is dan de bewaarperiode voor het bijhouden van wijzigingen  

  - **Globale gegevens**: de primaire site initialiseert de algemene gegevens van de CAS opnieuw.  

  - **Site gegevens**: de CAS initialiseert de site gegevens van de primaire site opnieuw. Wijzigingen na de back-up gaan verloren. Clients genereren de meeste gegevens opnieuw wanneer ze informatie verzenden naar de primaire site.  

## <a name="site-recovery-procedures"></a>Procedures voor het herstellen van een site

Gebruik een van de volgende procedures om u te helpen uw site server en site database te herstellen:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Een site herstel starten in de installatie wizard

1. Kopieer de [cd. De meest recente map](the-cd.latest-folder.md) naar een locatie buiten de Configuration Manager installatiemap. Van de kopie van de CD. Meest recente map, voert u de wizard Configuration Manager Setup uit.  

2. Selecteer op de pagina **aan** de slag de optie **een site herstellen**en selecteer **volgende**.  

3. Voltooi de wizard met behulp van de opties die geschikt zijn voor uw siteherstel.  

     - Tijdens het herstel identificeert het installatie programma de SQL Server Service Broker (SSB) die wordt gebruikt door de SQL Server. Wijzig deze poort instelling niet tijdens het herstel of de gegevens replicatie zal niet goed werken nadat het herstel is voltooid.  

     - U kunt het oorspronkelijke of een nieuw pad opgeven dat moet worden gebruikt voor de installatie van de Configuration Manager in de installatie wizard.  

### <a name="start-an-unattended-site-recovery"></a>Een site herstel zonder toezicht starten

1. Bereid het script voor de installatie zonder toezicht voor voor de opties die u nodig hebt voor het siteherstel. Zie [site Recovery zonder toezicht](unattended-recovery.md)voor meer informatie.  

2. Voer Configuration Manager Setup uit met behulp van de `/script` opdracht regel optie. U maakt bijvoorbeeld een Setup-initialisatie bestand **installatie bijvoorbeeld configmgrunattend. ini**. U slaat deze op in de `C:\Temp` map van de computer waarop u het installatie programma uitvoert. Gebruik de volgende opdracht:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  

> [!NOTE]  
> Nadat u een certificerings instantie hebt hersteld, kan de replicatie van bepaalde site gegevens van onderliggende sites niet tot stand worden gebracht. Deze gegevens kunnen betrekking hebben op hardware-inventaris, software-inventaris en status berichten.
>
> Als dit probleem optreedt, initialiseert u de **ConfigMgrDRSSiteQueue** opnieuw voor database replicatie. Gebruik **SQL Server beheer** om de volgende query uit te voeren op de site database voor de ca's:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```

## <a name="post-recovery-tasks"></a>Taken na herstel

Nadat u uw site hebt hersteld, moet u rekening houden met verschillende taken na herstel voordat uw site herstel is voltooid. Gebruik de volgende secties voor hulp bij het voltooien van uw proces voor siteherstel.

### <a name="reenter-user-account-passwords"></a>Wacht woorden van gebruikers accounts opnieuw invoeren

Nadat een site server is hersteld, voert u de wacht woorden opnieuw in voor gebruikers accounts in de site. Deze wacht woorden worden opnieuw ingesteld tijdens het herstel van de site. De accounts worden weer gegeven op de pagina **voltooid** van de installatie wizard nadat het herstel van de site is voltooid. De lijst wordt ook opgeslagen `C:\ConfigMgrPostRecoveryActions.html` op de herstelde site server.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Wacht woorden van gebruikers accounts opnieuw invoeren na site Recovery

1. Open de Configuration Manager-console en maak verbinding met de herstelde site.  

2. Ga naar de werk ruimte **beheer** , vouw **beveiliging**uit en selecteer vervolgens **accounts**.  

3. Voer voor elk account de volgende stappen uit om het wacht woord opnieuw in te voeren:  

     1. Selecteer het account in de lijst die is geïdentificeerd na site Recovery.  

     2. Selecteer **Eigenschappen** in het lint.  

     3. Selecteer op het tabblad **Algemeen** de optie **instellen**en voer het wacht woord voor het account opnieuw in.  

     4. Selecteer **verifiëren**, kies de juiste gegevens bron voor het geselecteerde gebruikers account en selecteer vervolgens **verbinding testen**. Met deze stap wordt getest of het gebruikers account verbinding kan maken met de gegevens bron en de referenties verifieert.  

     5. Selecteer **OK** om de wachtwoord wijzigingen op te slaan en selecteer **OK** om de pagina account eigenschappen te sluiten.  

#### <a name="reenter-pxe-passwords"></a>Voer de PXE-wacht woorden opnieuw in

<!-- SCCMDocs#1683 -->

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **distributie punten** . Alle on-premises distributie punten met **Ja** in de kolom **PXE** zijn ingeschakeld voor PXE en kunnen een wacht woord opgeven om het opnieuw in te voeren.

1. Selecteer een distributie punt met PXE-functionaliteit en selecteer **Eigenschappen** in het lint.

1. Ga naar het tabblad **PXE** .

1. Als de optie voor het **vereisen van een wacht woord wanneer computers PXE gebruiken** is ingeschakeld, voert u het wacht woord in en bevestigt u dit.

1. Selecteer **OK** om de eigenschappen op te slaan en te sluiten.

Herhaal dit proces voor elk ander PXE-ingeschakelde on-premises distributie punt.

#### <a name="reenter-task-sequence-passwords"></a>Wacht woorden van taken reeksen opnieuw invoeren

<!-- SCCMDocs#1683 -->

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer het knoop punt **taken reeksen** .

1. Selecteer een taken reeks en selecteer vervolgens **bewerken**in het lint.

1. Bekijk de volgende stappen om wacht woorden opnieuw in te voeren:

    - **Windows-instellingen Toep assen**: als u het wacht woord van de lokale beheerder inschakelt en opgeeft, voert u het wacht woord opnieuw in en bevestig dit.

    - **Netwerk instellingen Toep assen**: Selecteer **instellen**voor het account dat is gemachtigd om lid te worden van het domein. Voer het wacht woord in en bevestig dit en selecteer vervolgens **verifiëren**.

    - **Installatie kopie van het besturings systeem vastleggen**: Selecteer **instellen**voor het account dat wordt gebruikt om toegang te krijgen tot de bestemming. Voer het wacht woord in en bevestig dit en selecteer vervolgens **verifiëren**.

    - **Verbinding maken**met netwerkmap: Selecteer **instellen**voor het account dat wordt gebruikt om verbinding te maken met een netwerkmap. Voer het wacht woord in en bevestig dit en selecteer vervolgens **verifiëren**.

    - **BitLocker inschakelen**: als u de optie **TPM en pincode**voor sleutel beheer gebruikt, voert u de pincode opnieuw in.

    - **Lid worden van domein of werk groep**: Selecteer **instellen**voor het account dat is gemachtigd om lid te worden van het domein. Voer het wacht woord in en bevestig dit en selecteer vervolgens **verifiëren**.

    - **Opdracht regel uitvoeren**: als u de optie gebruikt om **deze stap uit te voeren als het volgende account**, selecteert u **instellen**. Voer het wacht woord in en bevestig dit en selecteer vervolgens **verifiëren**.

    - **Power shell-script uitvoeren**: als u de optie gebruikt om **deze stap uit te voeren als het volgende account**, selecteert u **instellen**. Voer het wacht woord in en bevestig dit en selecteer vervolgens **verifiëren**.

Herhaal dit proces voor alle taken reeksen.

### <a name="reenter-sideloading-keys"></a>Sideloading-codes opnieuw invoeren

Nadat een site server is hersteld, voert u de Windows-sideloading-codes voor de site opnieuw in. Deze sleutels worden opnieuw ingesteld tijdens het herstel van de site. Nadat u de sideloading-codes opnieuw hebt ingevoerd, wordt de telling in de kolom **gebruikte activeringen** voor Windows-sideloading-codes opnieuw ingesteld op de site.

Voordat de site het **totale aantal activeringen** heeft mislukt, wordt bijvoorbeeld weer gegeven als **100**. Het aantal sleutels dat is gebruikt voor apparaten of **geactiveerde activeringen**, is **90**. Na het herstel van de site wordt in de waarde voor **Totaal aantal activeringen** nog steeds **100**weer gegeven, maar de kolom **gebruikte activeringen** bevat onjuist **0**. Nadat 10 nieuwe apparaten een sideloading-code hebben gebruikt, zijn er geen sideloading-codes meer en kan het elfde apparaat geen sideloading-code Toep assen.

### <a name="recreate-azure-services"></a>Azure-Services opnieuw maken

<!-- SCCMDocs#1022 -->

In Configuration Manager versie 1806 ziet u na site Recovery de volgende fout code in cloudmgr. log:

`Index (zero-based) must be greater than or equal to zero`

U kunt dit oplossen door [de geheime sleutel](../deploy/configure/azure-services-wizard.md#bkmk_renew) voor elke Azure-Tenant verbinding te vernieuwen.

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>SSL configureren voor sitesysteemrollen die gebruikmaken van IIS

Wanneer u site systemen herstelt waarop IIS wordt uitgevoerd en u voor HTTPS hebt geconfigureerd, moet u IIS opnieuw configureren voor het gebruik van het webserver certificaat.

### <a name="reinstall-hotfixes"></a>Hotfixes opnieuw installeren

Nadat een site is hersteld, moet u alle [out-of-band-hotfixes](updates.md#bkmk_outofband) die op de site server zijn toegepast, opnieuw installeren. Nadat site Recovery is uitgevoerd, bekijkt u de lijst met eerder geïnstalleerde hotfixes op de pagina **voltooid** van de installatie wizard. Deze lijst wordt ook opgeslagen `C:\ConfigMgrPostRecoveryActions.html` op de herstelde site server.

### <a name="recover-custom-reports"></a>Aangepaste rapporten herstellen

Sommige klanten maken aangepaste rapporten in SQL Server Reporting Services. Wanneer dit onderdeel mislukt, herstelt u de rapporten van een back-up van de rapport server. Zie [back-up-en herstel bewerkingen voor Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services)voor meer informatie over het herstellen van uw aangepaste rapporten in Reporting Services.

### <a name="recover-content-files"></a>Inhoudsbestanden herstellen

De site database houdt in dat de site server de inhouds bestanden opslaat. Er wordt geen back-up gemaakt van de inhouds bestanden en deze worden niet teruggezet als onderdeel van het back-up-en herstel proces. Als u inhouds bestanden volledig wilt herstellen, herstelt u de inhouds bibliotheek en pakket bron bestanden op de oorspronkelijke locatie. Er zijn verschillende methoden om uw inhouds bestanden te herstellen. De eenvoudigste methode is om de bestanden terug te zetten vanuit een back-up van een bestands systeem van de site server.

Als u geen back-up van het bestands systeem voor de pakket bron bestanden hebt, moet u deze hand matig kopiëren of downloaden. Dit proces is vergelijkbaar met wanneer u het pakket oorspronkelijk hebt gemaakt. Voer de volgende query uit in SQL Server om de bron locatie van het pakket voor alle pakketten en toepassingen te vinden: `SELECT * FROM v_Package` . Bepaal de bron site van het pakket door de eerste drie tekens van de pakket-ID te bekijken. Als de pakket-id bijvoorbeeld CEN00001 is, is de sitecode van de bronsite CEN. Wanneer u de pakketbronbestanden herstelt, moeten deze op dezelfde locatie worden hersteld waar deze zich vóór de fout bevonden.

Als u geen bestandssysteem back-up hebt die de inhouds bibliotheek bevat, hebt u de volgende opties voor terugzetten:  

- **Een voor bereid inhouds bestand importeren**: In een Configuration Manager-hiërarchie kunt u een voor bereid inhouds bestand maken met alle pakketten en toepassingen van een andere locatie. Importeer vervolgens het voor bereide inhouds bestand om de inhouds bibliotheek op de site server te herstellen.  

- **Inhoud bijwerken**: Configuration Manager kopieert de inhoud van de pakket bron naar de inhouds bibliotheek. De pakket bron bestanden moeten beschikbaar zijn op de oorspronkelijke locatie om deze actie te kunnen volt ooien. Voer deze actie uit voor elk pakket en elke toepassing.

### <a name="recover-custom-software-updates"></a>Aangepaste software-updates herstellen

Wanneer u System Center Updates Publisher database bestanden in uw back-upschema hebt opgenomen, kunt u de data bases herstellen als de updates Publisher-computer uitvalt. Zie [System Center updates Publisher](../../../sum/tools/updates-publisher.md)voor meer informatie over updates Publisher.

#### <a name="restore-the-updates-publisher-database"></a>De updates Publisher-data base herstellen

1. Installeer updates Publisher opnieuw op de herstelde computer.  

2. Kopieer het database bestand **Scupdb. sdf** van de back-upbestemming naar `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` op de computer waarop updates Publisher wordt uitgevoerd.  

3. Wanneer meer dan één gebruiker updates Publisher op de computer uitvoert, kopieert u elk database bestand naar de juiste locatie van het gebruikers profiel.  

### <a name="user-state-migration-data"></a>Migratiegegevens van de gebruikersstatus

Als onderdeel van de eigenschappen van het status migratie punt geeft u de mappen op waarin de gebruikers status gegevens worden opgeslagen. Nadat u een status migratie punt hebt hersteld, moet u de gebruikers status gegevens op de server hand matig herstellen. Zet het bestand terug naar dezelfde mappen waarin de gegevens werden opgeslagen vóór de fout.

### <a name="regenerate-the-certificates-for-distribution-points"></a>De certificaten voor distributiepunten opnieuw genereren

Nadat u een site hebt hersteld, kan in het **distmgr. log** de volgende vermelding voor een of meer distributie punten worden weer gegeven: `Failed to decrypt cert PFX data` . Deze vermelding geeft aan dat de certificaat gegevens van het distributie punt niet door de site kunnen worden ontsleuteld. U kunt dit probleem oplossen door het certificaat opnieuw te genereren of opnieuw te importeren voor de betrokken distributie punten. Gebruik de Power shell [-cmdlet Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) .

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Certificaten bijwerken die worden gebruikt voor distributie punten in de Cloud

Voor Configuration Manager is een Azure-beheer certificaat vereist om de site server te laten communiceren met distributie punten in de Cloud. Nadat een site Recovery is uitgevoerd, werkt u de certificaten voor distributie punten in de Cloud bij.

## <a name="recover-a-secondary-site"></a>Een secundaire site herstellen

Configuration Manager biedt geen ondersteuning voor het maken van een back-up van de Data Base op een secundaire site, maar biedt wel ondersteuning voor herstel door de secundaire site opnieuw te installeren. Herstel van secundaire site is vereist wanneer een Configuration Manager secundaire site uitvalt.

### <a name="requirements"></a>Vereisten

- De server moet aan alle vereisten voor de secundaire site voldoen en de juiste beveiligings rechten hebben geconfigureerd.  

- Gebruik hetzelfde installatiepad dat is gebruikt voor de mislukte site.  

- Gebruik een server met dezelfde configuratie als de server waarop de fout is opgetreden. Deze configuratie bevat de Fully Qualified Domain Name (FQDN).  

- De server moet dezelfde SQL Server configuratie hebben als de mislukte site.  

  - Tijdens het herstel van een secundaire site installeert Configuration Manager SQL Server Express niet als dit nog niet is geïnstalleerd op de computer.  

  - Gebruik dezelfde versie van SQL Server en hetzelfde exemplaar van SQL Server dat u voor de data base van de secundaire site hebt gebruikt vóór de fout.  

### <a name="procedure"></a>Procedure

Gebruik de actie **secundaire site herstellen** vanuit het knoop punt **Sites** in de Configuration Manager-console. In tegens telling tot andere typen sites, wordt bij herstel voor een secundaire site geen back-upbestand gebruikt. Met dit proces worden de bestanden van de secundaire site opnieuw geïnstalleerd op de server die is mislukt. Nadat de site opnieuw is geïnstalleerd, worden de gegevens van de secundaire site opnieuw geïnitialiseerd vanaf de bovenliggende primaire site.

Tijdens het herstel proces wordt door Configuration Manager gecontroleerd of de inhouds bibliotheek zich op de secundaire site server bevindt. Er wordt ook gecontroleerd of de juiste inhoud beschikbaar is. De secundaire site maakt gebruik van de bestaande inhouds bibliotheek als deze de juiste inhoud bevat. Als dat niet het geval is, moet u de inhoud opnieuw distribueren of voorbereiden op de server om de inhouds bibliotheek van een secundaire site te herstellen.

Wanneer u een distributie punt hebt dat zich niet op de secundaire site server bevindt, hoeft u het distributie punt niet opnieuw te installeren tijdens het herstellen van de secundaire site. Wanneer de secundaire site is hersteld, wordt de site automatisch gesynchroniseerd met het distributiepunt.

U kunt de status van het herstel van de secundaire site controleren met behulp van de actie **installatie status weer geven** in het knoop punt **Sites** in de Configuration Manager-console.
