---
title: Databasereplicatie
titleSuffix: Configuration Manager
description: Meer informatie over de Configuration Manager database replicatie gebruikt SQL Server voor het overdragen van gegevens in de-hiërarchie.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b495b02-c966-4eb3-92b9-52ebbf5c38ae
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d1a2c8baa349e6499aa483f947d94f7459357be4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720196"
---
# <a name="database-replication"></a>Databasereplicatie

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager database replicatie gebruikt SQL Server om gegevens over te dragen. Deze methode wordt gebruikt om wijzigingen in de site database samen te voegen met de informatie uit de Data Base op andere sites in de hiërarchie.

Houd rekening met de volgende punten over database replicatie:

- Alle sites delen dezelfde informatie.  

- Wanneer u een site in een hiërarchie installeert, wordt door Configuration Manager automatisch een database replicatie tussen de nieuwe site en de bovenliggende site tot stand gebracht.  

- Wanneer de installatie van de site is voltooid, wordt de database replicatie automatisch gestart.  

Wanneer u een nieuwe site aan een hiërarchie toevoegt, maakt Configuration Manager een algemene data base op de nieuwe site. De bovenliggende site maakt een moment opname van de relevante gegevens in de data base. Vervolgens wordt de moment opname overgebracht naar de nieuwe site met behulp van [replicatie op basis van een bestand](file-based-replication.md). De nieuwe site gebruikt vervolgens het SQL Server-programma voor bulksgewijs kopiëren (BCP) om de informatie in de lokale kopie van de Configuration Manager-Data Base te laden. Nadat de momentopname is geladen, voert elke site databasereplicatie uit met de andere site.  

Configuration Manager maakt gebruik van een eigen data base Replication-service om gegevens tussen sites te repliceren. De data base Replication-service gebruikt SQL Server wijzigingen bijhouden om de lokale site database te controleren op wijzigingen. Vervolgens worden de wijzigingen naar andere sites gerepliceerd met behulp van SQL Server Service Broker (SSB). Dit proces maakt standaard gebruik van TCP-poort 4022.  


## <a name="replication-groups"></a>Replicatie groepen

Configuration Manager groeps gegevens die door database replicatie in verschillende replicatie groepen worden gerepliceerd. Elke replicatie groep heeft een afzonderlijk schema voor vaste replicatie. De site gebruikt dit schema om te bepalen hoe vaak wijzigingen worden gerepliceerd naar andere sites.  

Een wijziging in een op rollen gebaseerde beheer configuratie repliceert bijvoorbeeld snel naar andere sites. Dit gedrag zorgt ervoor dat de andere site deze wijzigingen snel kan afdwingen. Een configuratie wijziging met een lagere prioriteit, zoals een aanvraag om een nieuwe secundaire site te installeren, repliceert met minder urgentie. Het kan enkele minuten duren voordat een nieuwe site aanvraag de primaire doel site bereikt.  


## <a name="settings"></a>Instellingen

U kunt de volgende instellingen wijzigen voor database replicatie:  

- **Database replicatie koppelingen**: bepalen wanneer specifiek verkeer het netwerk passeert.  

- **Gedistribueerde weer gaven**: wanneer een centrale beheer site (CAS) geselecteerde site gegevens aanvraagt, kan de gegevens rechtstreeks vanuit de Data Base op een onderliggende primaire site worden geopend.  

- **Schema's**: Geef op wanneer een replicatie koppeling wordt gebruikt en wanneer verschillende typen site gegevens worden gerepliceerd.  

- **Samen vatting**: instellingen wijzigen voor gegevens overzichten over netwerk verkeer waarmee replicatie koppelingen worden gepasseerd. De samenvatting wordt standaard om de 15 minuten uitgevoerd. Deze wordt gebruikt in rapporten voor database replicatie.  

- **Drempel waarden voor database replicatie**: Definieer wanneer de site rapporteert als gedegradeerd of mislukt. U kunt ook configureren wanneer Configuration Manager waarschuwingen genereert over replicatie koppelingen met een gedegradeerde of mislukte status.  


## <a name="types-of-data"></a>Typen gegevens

Configuration Manager classificeert voornamelijk de gegevens die worden gerepliceerd als *globale gegevens* of *site gegevens*. Wanneer database replicatie plaatsvindt, brengt de site wijzigingen aan in globale gegevens en site gegevens via de database replicatie koppeling. Globale gegevens worden gerepliceerd naar een bovenliggende of onderliggende site. Site gegevens worden alleen gerepliceerd naar een bovenliggende site. Een derde gegevens type, *lokale gegevens*, wordt niet gerepliceerd naar andere sites. Lokale gegevens zijn informatie die niet nodig is voor andere sites.  

### <a name="global-data"></a>Globale gegevens

Globale gegevens zijn objecten die door de beheerder zijn gemaakt en die repliceren naar alle sites in de gehele hiërarchie. Secundaire sites ontvangen alleen een subset van globale gegevens, als algemene proxy gegevens. U maakt globale gegevens op de CA'S en primaire sites. Dit type bevat de volgende gegevens:

- Software-implementatie
- Software-updates
- Verzamelings definities
- Beveiligingsbereiken voor beheer op basis van rollen

### <a name="site-data"></a>Site gegevens

Site gegevens zijn operationele gegevens die zijn gemaakt door Configuration Manager primaire sites en hun toegewezen clients. Site gegevens worden gerepliceerd naar de certificerings instantie, maar niet naar andere primaire sites. Site gegevens zijn alleen zichtbaar op de CA'S en op de primaire site waar de gegevens vandaan komen. U kunt site gegevens alleen wijzigen op de primaire site waar u deze hebt gemaakt. Dit type bevat de volgende gegevens:

- Hardware-inventaris
- Statusberichten
- Waarschuwingen
- De resultaten van op query's gebaseerde verzamelingen

Alle site gegevens worden gerepliceerd naar de CAS. De certificerings instantie beheert beheer en rapportage voor de hele site hiërarchie.  


## <a name="database-replication-links"></a><a name="bkmk_Dblinks"></a> Koppelingen voor databasereplicatie

Wanneer u een nieuwe site in een hiërarchie installeert, maakt Configuration Manager automatisch een database replicatie koppeling tussen de bovenliggende site en de nieuwe site. Er wordt één koppeling gemaakt voor de verbinding tussen de twee sites.  

Wijzig de instellingen voor elke koppeling om de overdracht van gegevens over de replicatie koppeling te beheren. Elke replicatiekoppeling ondersteunt afzonderlijke configuraties. Elke database replicatie koppeling bevat de volgende besturings elementen:  

- Stop de replicatie van geselecteerde site gegevens van een primaire site naar de CAS. Deze actie zorgt ervoor dat de certificerings instanties rechtstreeks toegang hebben tot deze gegevens vanuit de data base van de primaire site.  

- Plannen dat geselecteerde site gegevens van een onderliggende primaire site naar de CAS worden overgedragen.

- Definieer de instellingen die bepalen wanneer een database replicatie koppeling een gedegradeerde of mislukte status heeft.

- Geef op wanneer waarschuwingen moeten worden gegenereerd voor een mislukte replicatie koppeling.

- Geef op hoe vaak Configuration Manager gegevens wilt samenvatten over het replicatie verkeer dat gebruikmaakt van de replicatie koppeling. Deze gegevens worden in rapporten gebruikt.

Als u een database replicatie koppeling wilt configureren, gaat u in de Configuration Manager-console naar de werk ruimte **bewaking** . Selecteer het knoop punt **database replicatie** en bewerk de eigenschappen voor de koppeling. Dit knoop punt bevindt zich ook in de werk ruimte **beheer** onder het knoop punt **hiërarchie configuratie** . Bewerk een replicatie koppeling van ofwel de bovenliggende site of de onderliggende site van de replicatie koppeling.  

> [!TIP]  
> U kunt databasereplicatiekoppelingen bewerken vanuit het knooppunt **Databasereplicatie** in beide werkruimten. Wanneer u echter het knoop punt **database replicatie** gebruikt in de werk ruimte **bewaking** , kunt u ook de status van database replicatie weer geven. Het biedt ook toegang tot het hulp programma [Replication link Analyzer](../../servers/manage/monitor-replication.md#BKMK_RLA) . Gebruik dit hulp programma om te helpen bij het onderzoeken van problemen met database replicatie.  

Zie [besturings elementen voor site database replicatie](#BKMK_DBRepControls)voor meer informatie over het configureren van replicatie koppelingen. Zie [Data Base-replicatie bewaken](../../servers/manage/monitor-replication.md)voor meer informatie over het bewaken van de replicatie.  


## <a name="distributed-views"></a><a name="bkmk_distviews"></a> Gedistribueerde weergaven  

Wanneer u via gedistribueerde weer gaven een aanvraag op de CAS voor geselecteerde site gegevens maakt, krijgt deze rechtstreeks toegang tot de Data Base op de onderliggende primaire site. Deze rechtstreekse toegang vervangt de nood zaak om site gegevens van de primaire site naar de CAS te repliceren. Omdat elke replicatie koppeling onafhankelijk is van andere replicatie koppelingen, kunt u gedistribueerde weer gaven gebruiken op de replicatie koppelingen die u kiest. U kunt geen gedistribueerde weer gaven gebruiken tussen een primaire site en een secundaire site.  

Gedistribueerde weer gaven bieden de volgende voor delen:  

- Verminder de CPU-belasting om database wijzigingen op de CA'S en primaire sites te verwerken

- Verminder de hoeveelheid gegevens die over het netwerk worden overgedragen naar de CAS

- Verbeter de prestaties van de SQL Server die als host fungeert voor de CAS-data base

- De schijf ruimte beperken die wordt gebruikt door de CAS-data base

Overweeg het gebruik van gedistribueerde weer gaven wanneer een primaire site zich nauw bevindt voor de CAS in het netwerk, de twee sites zijn altijd ingeschakeld en altijd verbonden. Gedistribueerde weer gaven vervangen de replicatie van de geselecteerde gegevens tussen de sites met rechtstreekse verbindingen tussen de SQL-servers op elke site. Elke keer dat u deze gegevens aanvraagt, maakt de certificerings instantie een directe verbinding.

De site verzoekt gedistribueerde weergave gegevens in de volgende voorbeeld scenario's:

- Wanneer u rapporten of query's uitvoert
- Wanneer u gegevens in resource Explorer bekijkt
- Verzamelings evaluatie voor verzamelingen die regels op basis van site gegevens bevatten

Gedistribueerde weer gaven zijn standaard uitgeschakeld voor elke replicatie koppeling. Wanneer u gedistribueerde weer gaven inschakelt, selecteert u site gegevens die niet worden gerepliceerd naar de certificerings instantie op die koppeling. De certificerings instanties hebben rechtstreeks toegang tot deze gegevens vanuit de data base van de onderliggende primaire site die de koppeling deelt. U kunt de volgende types van sitegegevens voor gedistribueerde weergaven configureren:  

- **Hardware-inventaris** gegevens van clients
- **Software-inventarisatie en software licentie controle** gegevens van clients
- **Status berichten** van clients, de primaire site en alle secundaire sites

Wanneer u gegevens in de Configuration Manager-console of in rapporten bekijkt, zijn gedistribueerde weer gaven onzichtbaar voor u. Wanneer u gegevens aanvraagt die zijn ingeschakeld voor gedistribueerde weer gaven, heeft de CAS-site database server rechtstreeks toegang tot de data base van de onderliggende primaire site om de informatie op te halen.

U gebruikt bijvoorbeeld een Configuration Manager-console die is verbonden met de CAS. U vraagt informatie over hardware-inventaris van twee primaire sites: ABC en XYZ. U hebt alleen hardware-inventaris ingeschakeld voor gedistribueerde weer gaven op site ABC. De certificerings instantie haalt inventarisatie-informatie voor XYZ-clients op uit een eigen data base. De CAS haalt inventarisatie-informatie voor ABC-clients rechtstreeks op uit de Data Base op de site ABC. Deze informatie wordt weer gegeven in de Configuration Manager-console of in een rapport zonder de bron te identificeren.  

Als een replicatie koppeling een type gegevens ingeschakeld heeft voor gedistribueerde weer gaven, repliceert de onderliggende primaire site die gegevens niet naar de CAS. Wanneer u gedistribueerde weer gaven voor een type gegevens uitschakelt, hervat de onderliggende primaire site de normale gegevens replicatie naar de CAS. Voordat deze gegevens beschikbaar zijn op de CAS, moeten de replicatie groepen voor deze gegevens opnieuw worden geïnitialiseerd tussen de primaire site en de certificerings instanties. Nadat u een primaire site hebt verwijderd waarop gedistribueerde weer gaven zijn ingeschakeld, moeten de certificerings instanties de herinitialisatie van de gegevens volt ooien voordat u toegang krijgt tot gegevens die u hebt ingeschakeld voor gedistribueerde weer gaven op de CA'S.  

> [!IMPORTANT]  
> Wanneer u gedistribueerde weer gaven gebruikt op een replicatie koppeling in de site hiërarchie, moet u gedistribueerde weer gaven uitschakelen voor alle replicatie koppelingen voordat u een primaire site verwijdert. Zie [een primaire site verwijderen die gebruikmaakt van gedistribueerde weer gaven](../../servers/deploy/install/uninstall-sites-and-hierarchies.md#bkmk_distviews)voor meer informatie.  

### <a name="prerequisites-and-limitations-for-distributed-views"></a>Vereisten en beperkingen voor gedistribueerde weer gaven  

- Gebruik gedistribueerde weer gaven op replicatie koppelingen tussen de CA'S en een primaire site.

- De CA'S moeten SQL Server Enterprise-editie gebruiken. Deze vereiste is niet vereist voor de primaire site.

- De CA'S kunnen slechts één exemplaar van de SMS-provider hebben. Installeer dat ene exemplaar op de site database server. Deze configuratie biedt ondersteuning voor Kerberos-verificatie. Voor de SQL Server op de CAS is Kerberos vereist om toegang te krijgen tot de SQL-Server op de onderliggende primaire site. Er zijn geen beperkingen met betrekking tot de SMS-provider op de onderliggende primaire site.

- U kunt slechts één Reporting Services-punt op de CAS installeren. Installeer SQL Server Reporting Services op de site database server. Deze configuratie biedt ondersteuning voor Kerberos-verificatie. Voor de SQL Server op de CAS is Kerberos vereist om toegang te krijgen tot de SQL-Server op de onderliggende primaire site.

- U kunt de site database niet hosten op een [SQL Server cluster](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).

- In versie 1902 en eerder kunt u de site database niet hosten op een SQL Server AlwaysOn- [beschikbaarheids groep](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md). Als u deze configuratie wilt ondersteunen, moet u bijwerken naar versie 1906 of hoger.<!-- SCCMDocs-pr#3792 -->

- Het computer account van de CAS-database server vereist **Lees** machtigingen voor de data base van de primaire site.

> [!IMPORTANT]  
> Gedistribueerde weer gaven en [schema's](#BKMK_schedules) voor wanneer gegevens kunnen worden gerepliceerd, zijn instellingen die elkaar uitsluiten voor een database replicatie koppeling.  


## <a name="schedule-transfers-of-site-data"></a><a name="BKMK_schedules"></a>Overdracht van site gegevens plannen

Om u te helpen de netwerk bandbreedte te beheren die wordt gebruikt om site gegevens van een onderliggende primaire site naar de CAS te repliceren, moet u plannen wanneer een replicatie koppeling wordt gebruikt. Geef vervolgens op wanneer verschillende typen site gegevens worden gerepliceerd. U kunt controleren wanneer de primaire site statusberichten, inventarissen en metergegevens repliceert. Database replicatie koppelingen van secundaire sites ondersteunen geen schema's voor site gegevens. U kunt de overdracht van globale gegevens niet plannen.  

Wanneer u een schema voor database replicatie koppelingen configureert, kunt u de overdracht van geselecteerde site gegevens van de primaire site naar de CAS beperken. U kunt ook verschillende tijdstippen configureren om verschillende typen site gegevens te repliceren.  

> [!IMPORTANT]  
> [Gedistribueerde weer gaven](#bkmk_distviews) en schema's voor wanneer gegevens kunnen worden gerepliceerd, zijn onderling exclusieve configuraties voor een database replicatie koppeling.  


## <a name="summarization-of-traffic"></a><a name="BKMK_SummarizeDBReplication"></a>Samen vatting van verkeer  

Elke site samenvat regel matig gegevens over het netwerk verkeer waarmee database replicatie koppelingen voor de site worden gepasseerd. De site gebruikt samen vattingen van gegevens in rapporten voor database replicatie. Beide sites op een replicatiekoppeling vatten het netwerkverkeer samen dat de replicatiekoppeling passeert. De site database server geeft een overzicht van de gegevens. Nadat de gegevens zijn samengevoegd, worden de gegevens gerepliceerd naar andere sites als globale gegevens.  

De samenvatting wordt standaard om de 15 minuten uitgevoerd. Als u de frequentie van de samen vatting voor netwerk verkeer wilt wijzigen, bewerkt u het **samenvattings interval**in de eigenschappen van de database replicatie koppeling. De frequentie van de samen vatting is van invloed op de informatie die u ziet in rapporten over database replicatie. U kunt een interval van 5 tot 60 minuten kiezen. Als u de samenvattingsfrequentie verhoogt, verhoogt u de verwerkingsbelasting op de SQL Server op elke site op de replicatiekoppeling.  

## <a name="database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a>Drempel waarden voor database replicatie

Met drempel waarden voor database replicatie wordt gedefinieerd wanneer Configuration Manager de status van een database replicatie koppeling rapporteert als een gedegradeerd of mislukt. Standaard wordt een koppeling ingesteld als *gedegradeerd* wanneer een replicatie groep de replicatie voor 12 opeenvolgende pogingen niet kan volt ooien. De koppeling wordt ingesteld als *mislukt* wanneer een replicatie groep in 24 opeenvolgende pogingen niet kan worden gerepliceerd.  

U kunt aangepaste waarden opgeven voor een gedegradeerde of mislukte status. Als u deze waarden aanpast, kunt u de status van database replicatie op de koppelingen nauw keuriger controleren.  

Een of meer replicatie groepen kunnen niet worden gerepliceerd, terwijl andere replicatie groepen blijven repliceren. Plan om de replicatie status van een koppeling te controleren wanneer het de eerste keer rapporteert als gedegradeerd.

U kunt in de volgende situaties de waarden voor nieuwe pogingen voor de gedegradeerde of mislukte status van de koppeling wijzigen:

- Er zijn herhaalde vertragingen voor specifieke replicatie groepen en de vertraging is niet van een probleem

- De netwerk koppeling tussen sites heeft een lage beschik bare band breedte

Wanneer u het aantal nieuwe pogingen verhoogt voordat de site de koppeling naar gedegradeerd of mislukt, kunt u onterechte waarschuwingen voor bekende problemen elimineren. Met deze actie kunt u de status van de koppeling nauw keuriger bijhouden.  

Om te begrijpen hoe vaak de replicatie van die groep plaatsvindt, moet u rekening houden met het interval voor replicatie synchronisatie voor elke replicatie groep. Als u het **synchronisatie-interval** voor replicatie groepen wilt weer geven, gaat u naar de werk ruimte **bewaking** in de Configuration Manager-console. Selecteer in het knoop punt **database replicatie** het tabblad **replicatie Details** van een replicatie koppeling.  

Zie [Data Base-replicatie bewaken](../../servers/manage/monitor-replication.md)voor meer informatie over het bewaken van database replicatie, inclusief het weer geven van de replicatie status.  


## <a name="site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a>Besturings elementen voor site database replicatie  

Om u te helpen de netwerk bandbreedte te beheren die wordt gebruikt voor database replicatie, wijzigt u de instellingen voor elke site database. De instellingen zijn alleen van toepassing op de site database waarin u de instellingen configureert. De instellingen worden altijd gebruikt wanneer de site gegevens repliceert door database replicatie naar een andere site.  

U kunt de volgende replicatie besturings elementen voor elke site database wijzigen:  

- De SSB-poort  

- De tijd die moet worden gewacht voordat de replicatie fouten de site activeren om de kopie van de site database opnieuw te initialiseren  

- Comprimeer de gegevens die een site repliceert. De gegevens worden alleen gecomprimeerd voor overdracht tussen sites en niet voor opslag in de site database op een van beide locaties.  

Als u de instellingen voor de replicatie besturings elementen voor een site database wilt wijzigen, bewerkt u in de Configuration Manager-console in het knoop punt **database replicatie** de eigenschappen van de site database. Dit knoop punt wordt weer gegeven onder het knoop punt **hiërarchie configuratie** in de werk ruimte **beheer** en wordt ook weer gegeven in de werk ruimte **bewaking** . Als u de eigenschappen van de site database wilt bewerken, selecteert u de replicatie koppeling tussen de sites en opent u eigenschappen van **bovenliggende data base** of **Eigenschappen van onderliggende data base**.  

> [!TIP]  
> U kunt de besturingselementen voor databasereplicatie configureren in het knooppunt **Databasereplicatie** in beide werkruimten. Wanneer u echter het knoop punt **database replicatie** gebruikt in de werk ruimte **bewaking** , kunt u ook de status van de database replicatie bekijken voor een replicatie koppeling en het hulp programma Replication link Analyzer gebruiken om u te helpen bij het onderzoeken van problemen met replicatie.  


## <a name="see-also"></a>Zie ook

[Replicatie controleren](../../servers/manage/monitor-replication.md)

[Problemen met SQL-replicatie oplossen](../../servers/manage/replication/overview.md)
