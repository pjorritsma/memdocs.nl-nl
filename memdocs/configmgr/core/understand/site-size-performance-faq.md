---
title: Veelgestelde vragen over site grootte en-prestaties
titleSuffix: Configuration Manager
description: Antwoorden op Configuration Manager Veelgestelde vragen over de grootte en prestaties van de site.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 3e7b9f6bc861ef5a60e4c0857dc253e3c806a851
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073259"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Veelgestelde vragen over de site grootte en-prestaties Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit document vindt u veelgestelde vragen over Configuration Manager richt lijnen voor site grootte en veelvoorkomende prestatie problemen.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Veelgestelde vragen en voor beelden van computer-en schijf configuratie

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Hoe moet ik de schijven op mijn site server en SQL Server format teren?

Scheid de Configuration Manager postvak in-en SQL-bestanden op ten minste twee verschillende volumes. Met deze schei ding kunt u de grootte van cluster toewijzing optimaliseren voor de verschillende soorten I/O's die ze uitvoeren. 

Voor het volume dat als host fungeert voor de post vakken van uw site server, gebruikt u NTFS met 4 KB of 8K toewijzings eenheden. ReFS schrijft 64 KB zelfs voor kleine bestanden. Configuration Manager heeft veel kleine bestanden, zodat ReFS onnodig schijf overhead kan opleveren.

Gebruik voor schijven met SQL database bestanden NTFS-of ReFS-notatie, met 64K toewijzings eenheden.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>Hoe en waar moet ik mijn SQL database-bestanden indelen?

Moderne matrices van SSD (Solid-state drives) en Azure Premium Storage kunnen hoge IOPS bieden op één volume, met weinig schijven. Normaal gesp roken voegt u meer stations toe aan een matrix voor extra opslag, niet meer door voer. Als u fysieke schijven op basis van de spindle gebruikt, hebt u mogelijk meer IOPS nodig dan u op één volume kunt genereren. U moet 60% van de totale aanbevolen IOPS en schijf ruimte voor het *. MDF* -bestand, 20% voor het *ldf* -bestand en 20% voor de tijdelijke logboek bestanden en gegevens toewijzen. De *ldf* -en tijdelijke bestanden kunnen zich op één volume bevinden met 40% (20% + 20%) van uw toegewezen IOPS.

SQL-servers ouder dan SQL Server 2016 standaard slechts één tijdelijk gegevens bestand gemaakt. U moet meer maken om SQL-vergren delingen te voor komen en te wachten op toegang tot één bestand. Community-adviezen kunnen variëren op het beste aantal tijdelijke gegevens bestanden dat kan worden gemaakt, van vier tot acht. Bij het testen is weinig verschil tussen vier en acht. u kunt dus vier, op te *nemen tijdelijke gegevens* bestanden maken. Uw TempDB-gegevens bestanden moeten Maxi maal 20-25% de grootte van uw volledige data base zijn.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Zijn er andere aanbevelingen voor schijf installatie?

Stel bij configureerbaar RAID-controller geheugen in op 70% toewijzing voor schrijf bewerkingen en 30% voor lees bewerkingen. In het algemeen gebruikt u een configuratie van een RAID 10-matrix voor de site database. RAID 1 is ook geschikt voor kleinschalige sites met lage I/O-vereisten of als u snelle Ssd's gebruikt. Met grotere schijf matrices configureert u reserve schijven om automatisch defecte schijven te vervangen.

**Voor beeld: fysieke machine met fysieke schijven** 

[Richt lijnen](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) voor het aanpassen van een site server met één locatie en SQL server met **100.000** -clients zijn 1200 IOPS voor het postvak in van de site server en 5000 IOPS voor SQL Server-bestanden.

De resulterende schijf configuratie kan er als volgt uitzien:

| Stations<sup>1</sup> | RAID | Indeling | Volume-inhoud | Minimale IOPS vereist| Ong. IOPS opgegeven<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS-8k     | Post vakken ConfigMgr    |     1700            | 1751             |
| 12x15k         | 10        | 64.000 ReFS    | SQL. MDF             | 60% * 5000 = 3000     | 3476             |
| 8x15k          | 10        | 64.000 ReFS    | SQL. ldf, tijdelijke bestanden | 40% * 5000 = 2000     | 2322             |

1. Bevat geen aanbevolen reserve schijven. 
2. Deze waarde is van de [voor beeld-schijf configuraties](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Ik gebruik Hyper-V op Windows Server. Hoe moet ik de schijven voor mijn Configuration Manager Vm's configureren voor de beste prestaties?

Hyper-V levert vergelijk bare prestaties op een fysieke server, als hardwarebronnen (CPU-kernen en doorgangs opslag) 100% zijn toegewezen aan de virtuele machine (VM). Het gebruik van schijf bestanden met een vaste grootte *. VHD* of *. vhdx* veroorzaakt een minimale invloed van 1-5% I/O-prestaties. Het gebruik van dynamisch uitbreid bare *. VHD* -of *. vhdx* -schijf bestanden resulteert in een invloed van Maxi maal 25% I/O-prestaties voor de Configuration Manager workload. Als u dynamisch uitbreid bare schijven nodig hebt, moet u de prestaties van 25% IOPS toevoegen aan de matrix.

Wanneer u uw Configuration Manager-site server of SQL binnen een virtuele machine uitvoert, isoleert u de stations van het Hyper-V-hostbesturingssysteem vanuit het besturings systeem en de gegevens stations van de virtuele machine.

Zie [prestaties afstemmen voor Hyper-V-servers](/windows-server/administration/performance-tuning/role/hyper-v-server/)voor meer informatie over het optimaliseren van vm's.

**Voor beeld: Hyper-V VM op basis van een site server** 

[Richt lijnen](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) voor het aanpassen van een site server met één locatie en SQL server met **150.000** -clients zijn 1800 IOPS voor het postvak in van de site server en 7400 IOPS voor SQL Server-bestanden.

De resulterende schijf configuratie kan er als volgt uitzien:

| Stations<sup>1</sup> | RAID | Indeling<sup>2</sup> | Volume-inhoud | Minimale IOPS vereist| Ong. IOPS opgegeven<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Hyper-V-host-besturings systeem           | -                    | -                |
| 2x10k          | 1         | -              | (VM) besturings systeem van site server       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS-8k        | (VM) postvak in ConfigMgr    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | 64.000 ReFS       | (VM) host SQL (alle bestanden) | 7400                 | 14346            |

1. Bevat geen aanbevolen reserve schijven. 
2. Vaste grootte, Pass-Through *. vhdx* voor het VM-station dat is toegewezen aan het onderliggende volume. 
3. Deze waarde is van de [voor beeld-schijf configuraties](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Zijn er suggesties voor Configuration Manager omgevingen in Microsoft Azure?

Lees eerst de [Configuration Manager op veelgestelde vragen over Azure](configuration-manager-on-azure.md).

Azure Infrastructure as a Service (IaaS) Vm's die gebruikmaken van Premium Storage-schijven kunnen hoge IOPS hebben. Configureer op deze Vm's extra schijven voor verwachte schijfruimte behoeften, in plaats van voor extra IOPS.

Azure Storage is inherent overbodig en vereist geen meerdere schijven voor Beschik baarheid. U kunt schijven in schijf beheer of opslag ruimten verwijderen om extra ruimte en prestaties te bieden.

Zie voor meer informatie en aanbevelingen voor het maximaliseren van Premium Storage prestaties en het uitvoeren van SQL-servers in azure IaaS Vm's:

- [Prestaties van de toepassing optimaliseren](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Richt lijnen voor schijven](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Voor beeld: site server op basis van Azure** 

[Richt lijnen](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) voor het aanpassen van de grootte van een site server met een colocatie en SQL server met **50.000** -clients zijn acht kernen, 32 GB en 1200 IOPS voor het postvak in van de site server en 2800 IOPS voor SQL Server-bestanden.

Uw resulterende Azure-machine is mogelijk een DS13v2 (acht kernen, 56 GB) met de volgende schijf configuratie:

| Aandrijfeenheden | Indeling | Contains | Minimale IOPS vereist| Ong. IOPS opgegeven<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standaard&gt; | -             | Besturings systeem van site server     | -                    | -                |
| 1xP20 (512 GB)    | NTFS-8k       | Post vakken ConfigMgr  | 1200                 | 2334             |
| 1xP30 (1024 GB)   | 64.000 ReFS      | SQL (alle bestanden<sup>2</sup>) | 2800                 | 3112             |

1. Deze waarde is van de [voor beeld-schijf configuraties](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations).
2. Met [Azure-richt lijnen](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) kunt u de tempdb op het lokale, op SSD gebaseerde *D:* -station plaatsen, op voor waarde dat de beschik bare ruimte niet groter is en dat er extra schijf-I/O-distributie kan worden uitgevoerd.

**Voor beeld: site server op basis van Azure (voor een verhoging van de prestaties van instant)** 

De door Voer van een Azure-schijf wordt beperkt door de grootte van de virtuele machine. De configuratie in het voor gaande voor beeld van Azure kan de toekomstige uitbrei ding of extra prestaties beperken. Als u tijdens de eerste implementatie van uw Azure-VM extra schijven toevoegt, kunt u uw Azure-VM een hoger formaat hebben, zodat deze in de toekomst meer verwerkings kracht biedt, met een minimale investering vooraf. Het is veel eenvoudiger om de prestaties van de site te verbeteren naarmate de vereisten veranderen, in plaats van later een ingewik kelder migratie uit te voeren.

Wijzig de schijven in het voor gaande voor beeld van Azure om te zien hoe de IOPS wijzigt.

**DS13v2** 

| Stations<sup>1</sup> | Indeling | Contains | Minimale IOPS vereist| Ong. IOPS opgegeven<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standaard&gt; | -             | Besturings systeem van site server     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS-8k       | Post vakken ConfigMgr  | 1200                 | 3984             |
| 2xP30 (2048 GB)   | 64.000 ReFS      | SQL (alle bestanden<sup>3</sup>) | 2800                 | 3984             |

1. Schijven worden gestripd met opslag ruimten.
2. Deze waarde is van de [voor beeld-schijf configuraties](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). De VM-grootte beperkt de prestaties.
3. Met [Azure-richt lijnen](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) kunt u de tempdb op het lokale, op SSD gebaseerde *D:* -station plaatsen, op voor waarde dat de beschik bare ruimte niet groter is en dat er extra schijf-I/O-distributie kan worden uitgevoerd.

Als u in de toekomst meer prestaties nodig hebt, kunt u uw virtuele machine converteren naar een DS14v2, die dubbele CPU en geheugen. De extra schijf bandbreedte die wordt toegestaan door die VM-grootte, verhoogt ook onmiddellijk de beschik bare schijf-IOPS op de eerder geconfigureerde schijven.

**DS14v2**

| Stations<sup>1</sup> | RAID | Indeling | Contains | Minimale IOPS vereist| Ong. IOPS opgegeven<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standaard&gt; | -             | Besturings systeem van site server     | -                    | -                |
| 2xP20 (1024 GB)   | NTFS-8k       | Post vakken ConfigMgr  | 1200                 | 4639             |
| 2xP30 (2048 GB)   | 64.000 ReFS      | SQL (alle bestanden<sup>3</sup>) | 2800                 | 6182             |

1. Schijven worden gestripd met opslag ruimten.
2. Deze waarde is van de [voor beeld-schijf configuraties](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). De VM-grootte beperkt de prestaties.
3. Met [Azure-richt lijnen](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) kunt u de tempdb op het lokale, op SSD gebaseerde *D:* -station plaatsen, op voor waarde dat de beschik bare ruimte niet groter is en dat er extra schijf-I/O-distributie kan worden uitgevoerd.

## <a name="other-common-sql-server-related-performance-questions"></a>Andere algemene vragen over SQL Server-gerelateerde prestaties 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>Is het beter om uit te voeren met SQL die zich bevindt met de site server of om het op een externe server uit te voeren?

Beide kunnen adequaat worden uitgevoerd, ervan uitgaande dat de ene server de juiste grootte heeft of dat de netwerk verbinding voldoende is tussen de twee servers.

Externe SQL vereist de vooraf werkende en operationele kosten van een extra server, maar is doorgaans een van de meeste grootschalige klanten. De voor delen van deze configuratie zijn onder andere:

- Verbeterde Beschik baarheid van de site, zoals SQL always on
- De mogelijkheid om zware rapporten uit te voeren met minder overgehoord voor site verwerking
- Eenvoudig herstel na nood gevallen in sommige situaties
- Eenvoudiger beveiligings beheer
- Schei ding van rollen voor SQL-beheer, zoals met een afzonderlijk DBA-team

Voor SQL-locaties is een enkele server vereist. Dit is gebruikelijk voor de meeste kleinschalige klanten. De voor delen van deze configuratie zijn onder andere:

- Lagere kosten voor computers, licenties en onderhoud
- Minder storings punten in de site
- Beter beheer voor de planning van downtime

### <a name="how-much-ram-should-i-allocate-for-sql"></a>Hoeveel RAM moet ik toewijzen voor SQL?

SQL maakt standaard gebruik van alle beschik bare geheugen op uw server, waardoor het besturings systeem en andere processen op de computer kunnen worden Starving. Om potentiële prestatie problemen te voor komen, is het belang rijk dat u geheugen expliciet aan SQL toewijst. Op site servers die zijn gekoppeld aan SQL-servers, moet u ervoor zorgen dat het besturings systeem voldoende RAM-geheugen heeft voor het opslaan van bestanden in de cache en andere bewerkingen. Zorg ervoor dat er voldoende RAM resteert voor SMSExec en andere Configuration Manager processen. Wanneer u SQL op een externe server uitvoert, kunt u het *meren* deel van het geheugen toewijzen aan SQL, maar niet alle. Raadpleeg de [richt lijnen](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) voor het aanpassen van de eerste richt lijnen. 

SQL Server geheugen toewijzing moet worden afgerond op de hele GB. Naarmate het RAM-geheugen toeneemt tot grote hoeveel heden, kunt u SQL een hoger percentage laten hebben. Als er bijvoorbeeld 256 GB of meer RAM-geheugen beschikbaar is, kunt u SQL voor Maxi maal 95% configureren, omdat er nog steeds veel geheugen voor het besturings systeem wordt bewaard. Het bewaken van het wissel bestand is een goede manier om ervoor te zorgen dat er voldoende geheugen is voor het besturings systeem en eventuele Configuration Manager processen.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Kern geheugens zijn deze dagen goedkope tijd. Moet ik er gewoon een aantal toevoegen aan mijn SQL Server?

Als er meer dan 16 fysieke kernen en onvoldoende RAM-geheugen op de SQL-Server zijn, kunt u problemen met de inhoud van het geheugen uitvoeren. De Configuration Manager workload werkt beter wanneer er ten minste 3-4 GB RAM per kern beschikbaar is voor SQL. Wanneer u kernen toevoegt aan uw SQL-servers, moet u ervoor zorgen dat u het RAM-geheugen in proportionele hoeveel heden verhoogt.

### <a name="will-sql-always-on-impact-my-performance"></a>Zijn de prestaties van SQL altijd van invloed op mijn prestatie?

Over het algemeen heeft SQL always een ververwaarlozd effect op de prestaties van het systeem wanneer voldoende netwerk beschikbaar is tussen de SQL-replica servers. U kunt de groei van het bestand data base Log *. ldf* in een drukke SQL always on-omgeving. De ruimte van het logboek bestand wordt echter automatisch vrijgegeven na een geslaagde back-up van de data base. Voeg een SQL-taak voor de Configuration Manager-Data Base toe om een back-up uit te voeren, bijvoorbeeld elke 24 uur en een *. ldf* -back-up om de zes uur. Zie voor meer informatie over SQL always on en Configuration Manager, inclusief meer informatie over SQL-back-upstrategieen, [SQL Server altijd aan voor een Maxi maal beschik bare site database](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="should-i-enable-sql-compression-on-my-database"></a>Moet ik SQL-compressie inschakelen voor mijn data base?

SQL-compressie wordt niet aanbevolen voor de Configuration Manager-Data Base. Hoewel er geen functionele problemen zijn met het inschakelen van compressie voor een Configuration Manager-Data Base, worden in de test resultaten geen veel omvang van de grootte weer gegeven vergeleken met de mogelijke gevolgen voor de prestaties van het systeem.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>Moet ik SQL-versleuteling inschakelen voor mijn data base?

Eventuele geheimen in de Configuration Manager-Data Base zijn al veilig opgeslagen, maar het toevoegen van SQL-code ring kan nog een andere beveiligingslaag toevoegen. Er zijn geen functionele problemen met het inschakelen van versleuteling voor uw data base, maar er kan een prestatie vermindering van 25% zijn, afhankelijk van de tabellen die u wilt versleutelen en de versie van SQL die u gebruikt. Versleutelen daarom voorzichtig, vooral in grootschalige omgevingen. Vergeet ook niet om uw back-up-en herstel plannen bij te werken om ervoor te zorgen dat u de versleutelde gegevens kunt herstellen.

### <a name="what-version-of-sql-should-i-run"></a>Welke versie van SQL moet ik uitvoeren?

Zie [ondersteuning voor SQL Server versies](../plan-design/configs/support-for-sql-server-versions.md)voor ondersteunde versies van SQL. Vanuit een prestatie oogpunt voldoen alle ondersteunde versies van SQL aan de vereiste prestatie criteria. SQL 2012 en SQL 2016 of nieuwer zijn echter vaak leverde SQL 2014 in sommige aspecten van de Configuration Manager-workload. Ook wordt het uitvoeren van SQL 2014 op het niveau van SQL 2012-compatibiliteit (110) de prestaties in het algemeen verbeterd. Op het moment van installatie worden Configuration Manager data bases die worden uitgevoerd op SQL 2012 en SQL 2014 ingesteld op compatibiliteits niveau 110. SQL 2016 of nieuwer is ingesteld op het standaard compatibiliteits niveau van de SQL-versie, zoals 130 voor SQL 2016. Bij de upgrade van SQL in place worden de compatibiliteits niveaus niet bijgewerkt totdat u de volgende primaire Configuration Manager huidige versie van de vertakking installeert. 

Als er ongebruikelijke time-outs of vertraging voor bepaalde SQL-query's in SQL 2016 of hoger worden weer geven, kunt u het SQL-compatibiliteits niveau wijzigen op de Configuration Manager data base in 110 als u gebruikmaakt van RBAC in de beheer console. Het uitvoeren van SQL-compatibiliteits niveau 110 op SQL 2014 en nieuwere versies van SQL wordt volledig ondersteund. Zie [SQL query time-out of console langzaam op bepaalde Configuration Manager database query's](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d)voor meer informatie.

Vanaf januari 2018 moet u de volgende SQL-versies *voor komen* , omdat er verschillende bekende of andere mogelijke problemen zijn:

- SQL 2012 SP3 CU1 naar CU5
- SQL 2014 SP1 CU6 naar SP2 CU2
- SQL 2016 RTM naar CU3, SP1 CU3 naar CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>Moet ik extra SQL-indexerings taken implementeren?

Ja, Indexeer indexen zo vaak als één keer per week en statistieken, net zo vaak als één keer per dag om SQL-prestaties te verbeteren. Scripts van derden en aanvullende informatie die beschikbaar zijn via de Configuration Manager en SQL-community's kunnen helpen bij het optimaliseren van deze taken.

In grote sites kunnen sommige SQL-tabellen, zoals CI\_CurrentComplianceStatusDetails, HinvChangeLog, groot zijn, afhankelijk van uw gebruiks patronen. Mogelijk moet u de onderhouds benadering voor deze een voor een verminderen of wijzigen.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>Wanneer moet ik volledige SQL Server gebruiken in plaats van SQL Express op mijn secundaire sites?

SQL Express heeft geen aanzienlijke gevolgen voor de prestaties van secundaire sites en is geschikt voor de meeste klanten. Het is ook eenvoudig te implementeren en te beheren, en is de aanbevolen configuratie voor bijna alle klanten op elke omvang.

Er is een situatie waarin de installatie van een volledige SQL Server mogelijk nodig is. Als u een groot aantal distributie punten en pakketten of bronnen in uw omgeving hebt, is het mogelijk om de maximale grootte van 10 GB van SQL Express te overschrijden. Als het aantal pakketten het aantal distributie punten meer overschrijdt dan 4.000.000, zoals 2.000 DPs met 2.000 stukjes inhoud, kunt u de volledige SQL Server op uw secundaire sites gebruiken. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>Moet ik de MaxDOP-instellingen voor mijn data base wijzigen?

Als u de instelling op 0 (alle beschik bare processors gebruiken) gebruikt, is dit in de meeste gevallen optimaal voor algemene verwerkings prestaties.

Veel Configuration Manager beheerders volgen de richt lijnen bij [aanbevelingen en richt lijnen voor de configuratie optie maximale graad van parallellisme in SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). Op de meeste moderne grote hardware leidt deze richt lijn tot een aanbevolen maximum instelling van acht. Als u echter veel kleinere query's uitvoert vergeleken met het aantal processors, kan het helpen om deze in te stellen op een hoger nummer. Het beperken van jezelf tot acht is niet noodzakelijkerwijs de beste instelling op grotere sites wanneer er meer kern geheugens beschikbaar zijn. 

Op SQL-servers met meer dan acht kernen begint u met een instelling van 0 en brengt u alleen wijzigingen aan als u prestatie problemen of overmatige vergren delingen ondervindt. Als u MaxDOP moet wijzigen omdat u problemen hebt met de prestaties van 0, begint u met een nieuwe waarde ten minste groter dan of gelijk aan het minimale aanbevolen aantal kern geheugens voor de SQL Server-grootte van die site. Bijna altijd lager is dan deze waarde, heeft een negatieve invloed op de prestaties. Een externe SQL Server voor een 100.000-client site moet bijvoorbeeld ten minste 12 kernen hebben. Als uw SQL-Server 16 kern geheugens heeft, kunt u de MaxDOP-instelling testen met een waarde van 12.

## <a name="other-common-performance-related-questions"></a>Andere algemene vragen over prestaties

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Welke mappen op de site server (of andere functies) moet ik uitsluiten voor antivirus software?

Wees voorzichtig wanneer u antivirus beveiliging op elk systeem uitschakelt. In een hoog volume en beveiligde omgevingen is het raadzaam om *actieve bewaking* uit te scha kelen voor optimale prestaties.

Zie voor meer informatie over aanbevolen anti virus-uitsluitingen de [Aanbevolen anti virus-uitsluitingen voor Configuration Manager 2012 en current branch site servers, site systemen en clients](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu).

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>Wat kan ik doen om WSUS beter te laten werken wanneer het wordt gebruikt met Configuration Manager?

Het wijzigen van een aantal belang rijke IIS-instellingen, zoals WsusPool-wachtrij lengte en WsusPool, kan de WSUS-prestaties verbeteren, zelfs op kleinere installaties. Zie [Aanbevolen hardware](../plan-design/configs/recommended-hardware.md)voor meer informatie.

Zorg er ook voor dat u de nieuwste updates hebt geïnstalleerd voor het besturings systeem waarop WSUS wordt uitgevoerd:

- Windows Server 2012: een cumulatieve update van niet "alleen beveiliging", uitgebracht op 2017 of hoger. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: elke cumulatieve update die niet ' beveiliging alleen ' is uitgegeven, augustus 2017 of hoger. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Windows Server 2016: een cumulatieve update van niet "alleen beveiliging", uitgebracht op 2017 of hoger. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>Welk type onderhoud moet ik uitvoeren op mijn WSUS-servers?

Raadpleeg [de volledige hand leiding voor micro soft WSUS en Configuration Manager sup-onderhoud](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Ik wil de basis prestatie bewaking voor mijn site instellen. Wat moet ik bekijken?

De traditionele server prestatie bewaking werkt effectief voor algemene Configuration Manager. U kunt ook gebruikmaken van de verschillende System Center Operations Manager Management Packs voor Configuration Manager, SQL Server en Windows Server om de basis status van uw servers te bewaken. U kunt ook rechtstreeks de prestatie meter items van Windows (PerfMon) controleren Configuration Manager levert. Bewaak de achterstand in de verschillende post vakken voor vroegtijdige waarschuwings signalen over mogelijke problemen met de site prestatie of achterstand.

## <a name="see-also"></a>Zie ook

- [Richt lijnen voor site grootte en-prestaties](../plan-design/configs/site-size-performance-guidelines.md)
- [Veelgestelde vragen over Azure Configuration Manager](configuration-manager-on-azure.md)
