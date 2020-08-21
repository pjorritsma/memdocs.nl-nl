---
title: Evaluatie van verzameling
titleSuffix: Configuration Manager
description: Meer informatie over het verzamelings evaluatie proces, typen en triggers. Meer informatie over het verzamelings evaluatie diagram en de hiërarchie.
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15b58b841ca87cf2b5e04c98dfd35c487c941e78
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693315"
---
# <a name="collection-evaluation-in-configuration-manager"></a>Evaluatie van verzamelingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager *verzamelings evaluatie* gebruikt voor het bijwerken van het lidmaatschap van de verzameling, op basis van de door u gedefinieerde verzamelings regels. Het bereik van de verzameling en timing van verzamelingen variëren, afhankelijk van de configuratie en het evaluatie type van de site en verzameling. 

Het is belang rijk om inzicht te krijgen in het beoordelings gedrag van verzamelingen, zodat u passende ontwerp beslissingen kunt nemen. Zie [Aanbevolen procedures voor verzamelingen](best-practices-for-collections.md)voor meer informatie over het evalueren van verzamelingen en aanbevelingen.

## <a name="evaluation-process"></a>Evaluatie proces

De records in [colleval. log](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs) wanneer de verzameling-evaluator verzamelingen maakt, wijzigt en verwijdert.

Op hoog niveau volgt elke evaluatie en update van afzonderlijke verzamelingen de volgende stappen:

![Update proces op hoog niveau](media/high-level-collection-update-process.png)

1. Voer de verzamelings query uit.
1. Voeg systemen toe die direct leden zijn.
1. Alle *insluit* verzamelingen evalueren.
   
   Als de include-verzamelingen ook query regels hebben of verzamelingen bevatten of uitsluiten, moet u ze ook evalueren. Als de insluit verzamelingen zelf verzamelingen beperken, evalueert u de verzamelingen daaronder. Nadat de structuur volledig is geëvalueerd, retourneert u de resultaten naar de aanroepende verzameling.
   
1. Voer een logische `AND` tussen de geretourneerde resultaten en de beperkende verzameling uit.
1. De *uitsluitings* verzamelingen evalueren.
   
   Als de uitsluitings verzamelingen ook query regels hebben of verzamelingen bevatten of uitsluiten, moet u ze ook evalueren. Als deze verzamelingen zelf verzamelingen beperken, moet u de verzamelingen hieronder evalueren. Nadat de structuur volledig is geëvalueerd, retourneert u de resultaten naar de aanroepende verzameling.
   
1. Vergelijk de resultatenset van het evalueren van de directe leden en voeg verzamelingen toe met de uitkomsten van het evalueren van de uitsluitingen van verzamelingen.
1. Schrijf de wijzigingen in de data base en voer updates uit.
1. Activeer ook alle afhankelijke verzamelingen die moeten worden bijgewerkt. Afhankelijke verzamelingen zijn verzamelingen die de huidige verzameling beperken of die verwijzen naar de huidige verzameling met regels voor opnemen of uitsluiten.

## <a name="collection-evaluation-types-and-triggers"></a>Verzamelings evaluatie typen en-triggers

Deze typen threads verwerken verzamelings evaluatie, afhankelijk van het evaluatie type:

- **Primair** voor geplande verzamelings updates
- **Hulp** om verzamelingen hand matig bij te werken met afhankelijke verzamelingen
- **Eén** om verzamelingen hand matig bij te werken zonder afhankelijke verzamelingen
- **Express** voor incrementele updates van verzamelingen

In de volgende tabel worden de evaluatie triggers voor verzamelingen en de bijbehorende evaluatie typen beschreven. 

| Trigger | Evaluatie type | Beschrijving |
|---------|-----------------|-------------|
|Handmatig|Eén of meer hulp|Hand matig is de evaluatie van de hoogste prioriteit. Wanneer een beheerder een hand matige verzamelings evaluatie aanvraagt, wijst de verzamelings evaluator de volgende beschik bare evaluatie-thread toe aan de evaluatie.|
|Gepland|Primair|Het proces van geplande evaluatie is hetzelfde als hand matige evaluatie, met uitzonde ring van de evaluatie tijd in plaats van gebeurtenissen die worden gestuurd.|
|Staging|Eén of meer hulp|Alle verzamelingen zijn direct of indirect afhankelijk van **alle systemen** of **alle gebruikers en gebruikers groepen**. Beide verzamelingen voeren dagelijks een volledige verzamelings evaluatie uit op 4:00 uur. Een wijziging in een van deze verzamelingen activeert updates van afhankelijke verzamelingen, op basis van een [volledige verzamelings grafiek](#collection-evaluation-graph).
|Incrementeel|Express|Incrementele evaluatie maakt gebruik van een verzamelings evaluatie grafiek om afhankelijke verzamelingen te evalueren en bij te werken als een update van het lidmaatschap van de incrementele verzameling wordt gewijzigd. Configuration Manager worden bronnen-objecten bewaakt en bijgewerkt in alle verzamelingen die zijn geconfigureerd voor incrementele updates.<br /><br />Als een verzamelings query is gebaseerd op gegevens die later worden bijgewerkt, zoals hardware-inventaris, wordt Configuration Manager alleen de resource toegevoegd aan of verwijderd uit de verzameling tijdens het bijwerken van de geplande verzameling.|

## <a name="collection-evaluation-graph"></a>Evaluatie grafiek verzameling

Een *verzamelings evaluatie grafiek* wijst alle verzamelingen toe die betrekking hebben op de verzameling die is bedoeld voor evaluatie. Een verzamelings evaluatie omvat de doel verzameling en alle gerelateerde verzamelingen in het verzamelings evaluatie diagram.

Wanneer de verzamelings evaluatie begint, maakt Configuration Manager een grafiek die alle verzamelingen bevat die mogelijk moeten worden geëvalueerd als gevolg van wijzigingen in de doel verzameling, beginnend vanaf het hoogste niveau in de cyclus. De verzamelings-evaluator gaat vervolgens door de grafiek in de juiste volg orde, waarbij elk verzamelings lidmaatschap op zijn beurt wordt geëvalueerd. Nadat de verzameling volledig is geëvalueerd, worden verzamelingen op lager niveau die niet worden beïnvloed door deze cyclus, verwijderd uit de evaluatie grafiek van de verzameling.

Als een of meer van de verzamelingen die worden geëvalueerd een regel voor opnemen of uitsluiten heeft, voegt de verzamelings-evaluator de opgenomen of uitgesloten verzameling toe aan de grafiek, samen met eventuele verzamelingen die verzamelings limieten. Als er wijzigingen zijn tijdens de evaluatie van de verzamelingen include en exclude, blijft de grafiek op die vertakking staan voordat deze naar de hoofd vertakking wordt geretourneerd.

Configuration Manager bouwt twee typen evaluatie grafieken, *Incrementeel* of *volledig*.

### <a name="incremental-collection-evaluation"></a>Evaluatie van incrementele verzameling

Wanneer tabel gegevens worden gewijzigd, voegt een SQL-trigger een rij in de tabel **CollectionNotifications** . De volgende keer dat een evaluatie planning voor een verzameling wordt geactiveerd, wordt `AND` de resource-id met de bestaande verzamelings query en worden er updates geactiveerd voor verzamelingen die zijn ingeschakeld voor *incrementele* verzamelingen.

Met de evaluatie van incrementele verzameling wordt één query per computer uitgevoerd. De standaard site configuratie voor de evaluatie van incrementele verzamelingen is om de vijf minuten.

In een incrementele verzamelings evaluatie grafiek worden verzamelingen waarnaar wordt verwezen, alleen toegewezen als deze zijn ingeschakeld voor incrementele evaluatie. Als een incrementele evaluatie beperkt is tot een verzameling die niet is ingeschakeld voor incrementele evaluatie, evalueert de grafiek de verzameling op basis van het bestaande lidmaatschap van de beperkende verzameling. 

In het volgende diagram ziet u bijvoorbeeld nieuw gedetecteerde resources die van toepassing zijn op alle verzamelingen. Met verzamelings evaluatie worden echter alleen de verzamelingen **alle servers** en **alle domein controllers** bijgewerkt. De verzamelings-evaluator evalueert de andere verzamelingen niet, omdat de verzameling **servers voor alle leden** niet is ingeschakeld voor incrementele evaluatie.

![Voor beeld van evaluatie grafiek voor incrementele verzameling](media/incremental-collection-evaluation-graph.png)

### <a name="full-collection-evaluation"></a>Volledige verzamelings evaluatie

Hand matige of geplande verzamelings evaluaties maken een *volledige* verzamelings evaluatie grafiek van alle afhankelijke verzamelingen. De grafiek bevat alle verzamelingen die verwijzen naar de verzameling die wordt bijgewerkt en de volgende verzamelingen. Configuration Manager gaat door met het evalueren van de grafiek zolang er updates worden uitgevoerd op de verzamelingen die worden verwerkt.

In het volgende diagram ziet u hoe een geplande of hand matige aanvraag voor het bijwerken van aanvragen voor de verzameling **alle servers** een volledige grafiek produceert die alle van toepassing zijnde verzamelingen bevat. De nieuwe bronnen voor de DNS-server en de domein controller bevinden zich binnen het bereik van de lidmaatschaps query's van alle verzamelingen, dus alle verzamelingen worden bijgewerkt.

![Volledige verzameling evaluatie grafiek voor beeld 1](media/full-collection-evaluation-graph-1.png)

Bij een volledige evaluatie worden niet altijd alle verzamelingen geëvalueerd. De verzamelings evaluatie grafiek blijft alleen afhankelijk verzamelingen evalueren als er een update plaatsvindt voor de huidige verzameling waarnaar wordt verwezen. Als er tijdens geplande incrementele evaluaties incrementele updates worden bijgewerkt, worden verwijzingen naar verzamelingen die niet zijn ingeschakeld voor incrementele updates, mogelijk niet bijgewerkt. Bij een volledige evaluatie wordt de verzameling niet bijgewerkt, waarna de verzamelings evaluatie grafiek wordt beëindigd en eventuele referentie-evaluaties voor die cyclus worden opgehaald. 

In het volgende voor beeld maakt de installatie van DNS op de bestaande server deel uit van de **DNS-servers** verzameling, maar omdat er geen update is voor het beperken van de verzameling van **alle lidservers** , wordt de verzameling van **DNS-servers** niet door de volledige evaluatie geëvalueerd. In de volgende incrementele evaluatie cyclus wordt de **DNS-server** verzameling geëvalueerd, omdat het een incrementele verzameling is.

![Volledige verzameling evaluatie grafiek voor beeld 2](media/full-collection-evaluation-graph-2.png)

## <a name="next-steps"></a>Volgende stappen
- [Verzamelingen maken](create-collections.md)
- [Aanbevolen procedures voor verzamelingen](best-practices-for-collections.md)
- [Viewer voor collectie-evaluatie](../../../support/ceviewer.md)
- [ConfigMgrDogs voor het oplossen van problemen met de ConfigMgr 2012](https://channel9.msdn.com/Events/TechEd/Australia/2014/DCI411) -sessie bij TechEd Australië