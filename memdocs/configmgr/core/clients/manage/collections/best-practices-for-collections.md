---
title: Aanbevolen procedures voor verzamelingen
titleSuffix: Configuration Manager
description: Krijg aanbevelingen voor het configureren van verzamelingen en verzamelings evaluatie in Configuration Manager.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ee640a70eea9f2e8470e852409911d28e542bc2
ms.sourcegitcommit: 1d8bf691780b94a945e94945115d4d1df4242808
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/10/2020
ms.locfileid: "84663367"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Aanbevolen procedures voor verzamelingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Sommige richt lijnen voor het beheer van verzamelingen kunnen tegen strijdige informatie zijn. Om prestatie redenen moet u bijvoorbeeld het aantal verzamelingen beperken dat regel matig wordt bijgewerkt. Het bijwerken van verzamelingen is vaak handig, omdat de meeste Configuration Manager functionaliteit afhankelijk is van verzamelingen. Houd zorgvuldig rekening met de prestatie-effecten en de zakelijke vereisten wanneer u verzamelingen en verzamelings evaluaties ontwerpt en configureert.

Gebruik de volgende aanbevolen procedures voor verzamelingen in Configuration Manager.  

## <a name="configure-maintenance-window-for-updates"></a>Onderhouds venster voor updates configureren

U kunt onderhouds Vensters voor Apparaatsets configureren om de tijden te beperken dat Configuration Manager software op deze apparaten kan installeren. Als u het onderhouds venster te klein configureert, kan de client mogelijk geen essentiële software-updates installeren, waardoor de client kwetsbaar is voor de problemen die de update vermindert.

Belang rijke overwegingen voor het plannen van uw onderhouds Vensters:

- De standaard waarde voor de maximale uitvoerings tijd van de software-update is 60 minuten.
- Wanneer Configuration Manager berekent of een update kan worden geïnstalleerd, wordt er vijf minuten aan de maximale uitvoerings tijd toegevoegd om het systeem opnieuw op te starten.
- De resterende duur van een onderhouds venster moet langer zijn dan de maximale uitvoerings tijd van de software-update plus vijf minuten.

## <a name="avoid-frequent-collection-evaluation"></a>Evaluatie van frequente verzamelingen voor komen

Een volledige verzamelings evaluatie evalueert niet alleen de doel verzameling, maar ook de verzamelingen die de verzameling beperkt als er een update wordt uitgevoerd. Ook wordt er nog steeds een verzameling zonder schema geëvalueerd als de beperkende verzameling wordt bijgewerkt. Het is dus mogelijk dat sommige verzamelingen vaker worden geëvalueerd dan u verwacht.

In een omgeving met een drukke Configuration Manager kunt u de prestaties van de verzamelings evaluatie verbeteren door schema's terug te schalen om herhaalde evaluaties te voor komen. In een diepe structuur kunt u de frequentie van de verzamelings evaluatie verlagen naarmate de verzamelingen dieper in de structuur dalen, omdat verzamelings evaluaties van een hoger niveau ook de evaluaties op lagere niveaus kunnen activeren.

## <a name="understand-the-collection-evaluation-graph"></a>Meer informatie over de verzameling evaluatie grafiek

Houd rekening met de werking van de verzamelings evaluatie grafiek, zodat u een geschikte verzamelings structuur kunt ontwerpen. Vertrouw niet op de evaluatie van de volledige verzameling om alle verzamelingen altijd bij te werken. Als een incrementeel bijgewerkte verzameling updates volgens een planning wordt uitgevoerd, worden verwijzingen naar verzamelingen die niet zijn ingeschakeld voor incrementele updates, mogelijk niet bijgewerkt. Omdat er waarschijnlijk updates zijn opgetreden tijdens incrementele evaluaties, wordt de verzameling mogelijk niet bijgewerkt door een volledige evaluatie, waardoor de verzamelings evaluatie grafiek voor die cyclus wordt beëindigd. In dat geval worden er geen verwijzende verzamelings evaluaties uitgevoerd. Zie [evaluatie grafiek verzameling](collection-evaluation.md#collection-evaluation-graph)voor meer informatie.

## <a name="limit-incremental-updates"></a><a name="bkmk_incremental"></a>Incrementele updates beperken

Het inschakelen van incrementele updates voor veel verzamelingen kan leiden tot evaluatie vertragingen. Het is het beste om het aantal incrementele bijgewerkte verzamelingen te beperken tot 200. Het exacte aantal is afhankelijk van:

- Het totale aantal verzamelingen
- De frequentie van nieuwe resources die worden toegevoegd en gewijzigd in de hiërarchie
- Het aantal clients in een hiërarchie
- De complexiteit van de lidmaatschaps regels voor verzamelingen in een hiërarchie

Als de incrementele evaluatie cyclus langer duurt dan de geconfigureerde update frequentie, wordt de verzamelings evaluaties door Configuration Manager continu verwerkt, wat van invloed kan zijn op de systeem prestaties. Verminder het aantal incrementele bijgewerkte verzamelingen of verg root de tijd tussen incrementele evaluatie cycli.

Gezien de mogelijke gevolgen van incrementele verzamelingen, is het belang rijk om een beleid of procedure te hebben voor het maken van de verzamelingen en het toewijzen van update planningen. Voor beelden van beleids overwegingen zijn:

- Gebruik alleen incrementele updates voor verzamelingen die worden gebruikt voor beveiligings bereik, client instellingen en onderhouds Vensters. Deze verzamelings updates zijn van invloed op client gedrag en toegang tot resources.
- Voor toepassingen zonder goed keuring van de licentie verlening adverteert u toepassingen aan bestaande verzamelingen en gebruikt u globale voor waarden om de beschik baarheid te beperken.
- Een overzicht van de juiste Peri Oden voor andere verzamelingen waarvoor volledige verzamelings updates zijn gepland.

## <a name="avoid-evaluation-of-large-trees-from-the-cas"></a>Voor komen dat grote structuren van de CAS worden geëvalueerd

In een Configuration Manager omgeving wordt het lidmaatschap van de verzameling niet geëvalueerd door de centrale beheer site (CA'S). Primaire sites zijn de enige sites waarmee verzamelingen worden geëvalueerd. Secundaire sites fungeren als proxy's die alleen gegevens gebruiken die ze repliceren vanaf hun primaire site.

Voor het aanvragen van een verzamelings update verzendt de certificerings instantie een aanvraag naar elke primaire site. De primaire sites evalueren de verzameling en verzenden de resultaten terug naar de CAS. De resultaten van de verzamelings evaluatie worden pas weer gegeven nadat alle instructies voor het verzamelen van de verzameling zijn gerepliceerd naar alle sites, alle sites evalueren alle verzamelingen en alle gegevens worden teruggezet naar de CAS en consolideren.

In het volgende diagram ziet u de stroom wanneer de CAS een hand matige verzamelings update aanvraagt:

![Hand matige update verzameling van een certificerings instantie](media/manual-collection-update-from-cas.png)

Het bijwerken van een verzameling van een certificerings instantie met meerdere primaire sites kan tijdrovend zijn. Als een verzameling niet tijdig wordt geëvalueerd, kunt u de aanvraag het beste herhalen.

Zodra een evaluatie-thread voor een verzameling begint en de evaluatie grafiek laadt, wordt de evaluatie voortgezet totdat de evaluatie grafiek voor verzamelingen leeg is. De thread wordt vervolgens beëindigd en wordt voor de volgende evaluatie beschikbaar. Als er echter een andere wachtrij voor verzamelings evaluatie cyclus is terwijl de thread verzamelingen evalueert, wordt de thread onmiddellijk opnieuw opgestart om een evaluatie van de ' gemiste ' cyclus te proberen.

Elke evaluatie methode wordt uitgevoerd in een eigen thread. Het is mogelijk dat Configuration Manager in de thread meerdere keren probeert om dezelfde verzameling te tekenen. Configuration Manager worden vervolgens de tweede en volgende aanvragen afbreekt.

U kunt deze scenario's voor komen door hand matige verzamelings evaluaties van grote structuren te vermijden, met name wanneer u vanuit de certificerings instantie met meerdere sites werkt.

## <a name="consider-collection-depth-and-cross-referencing"></a>Verzamelings diepte en kruis verwijzingen overwegen

Als u een balans wilt maken tussen bedrijfs vereisten en prestaties, is het belang rijk om inzicht te krijgen in de verzamelings structuur die u maakt, en de bijbehorende afhankelijkheden van andere verzamelingen. Als u een verzameling maakt met regels die verwijzen naar een of meer verzamelingen die ook verwijzen naar andere verzamelingen, worden al deze verzamelingen geëvalueerd om het lidmaatschap van de verzameling te maken.

Met de regels voor het opnemen en uitsluiten van verzamelingen in Configuration Manager het maken van verwijzingen naar verzamelingen eenvoudiger dan het schrijven van een aangepaste WQL-query. Als het gebruik van verzamelingen met include en exclude echter een hoge prestaties levert, kunt u in plaats daarvan de WQL-query methode gebruiken:

Behoort

`Select * from SMSRSystem where SMSRSystem.ResourceId in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

Weekend

`Select * from SMSRSystem where SMSRSystem.ResourceId not in (select ResourceID from SMS_CM_RES_COLL_[collection id])`

## <a name="use-ceviewer-to-monitor-collection-evaluation"></a>CEViewer gebruiken om verzamelings evaluaties te bewaken

U kunt de [verzameling evaluatie Viewer (CEViewer)](https://docs.microsoft.com/mem/configmgr/core/support/ceviewer) gebruiken om te controleren hoeveel verzamelingen worden geëvalueerd en hoe lang elke verzameling moet worden bijgewerkt. De CEViewer bevindt zich op de *cd. Meest recente* map op de site server.

Als u hand matig een vergelijk bare controle met SQL wilt uitvoeren, kunt u de volgende query gebruiken:

```sql
SELECT [t2].[CollectionName], [t2].[SiteID], [t2].[value] AS [Seconds], [t2].[LastIncrementalRefreshTime], [t2].[IncrementalMemberChanges] AS [IncChanges], [t2].[LastMemberChangeTime] AS [MemberChangeTime]
FROM (
    SELECT [t0].[CollectionName], [t0].[SiteID], DATEDIFF(Millisecond, [t1].[IncrementalEvaluationStartTime], [t1].[LastIncrementalRefreshTime]) * 0.001 AS [value], [t1].[LastIncrementalRefreshTime], [t1].[IncrementalMemberChanges], [t1].[LastMemberChangeTime], [t1].[IncrementalEvaluationStartTime], v1.[RefreshType]
    FROM [dbo].[Collections_G] AS [t0]
    INNER JOIN [dbo].[Collections_L] AS [t1] ON [t0].[CollectionID] = [t1].[CollectionID]
    inner join v_Collection v1 on [t0].[siteid] = v1.CollectionID
    ) AS [t2]
WHERE ([t2].[IncrementalEvaluationStartTime] IS NOT NULL) AND ([t2].[LastIncrementalRefreshTime] IS NOT NULL) and (refreshtype='4' or refreshtype='6')
ORDER BY [t2].[value] DESC
```


