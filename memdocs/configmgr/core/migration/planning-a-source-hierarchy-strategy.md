---
title: Strategie van de bron hiërarchie
titleSuffix: Configuration Manager
description: Configureer een bron hiërarchie en Verzamel gegevens van een bron site voordat u een Configuration Manager migratie taak configureert.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28960753da06058ef181f94a5d11d9f2327ebf56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719678"
---
# <a name="plan-a-source-hierarchy-strategy-in-configuration-manager"></a>Een strategie voor een bron hiërarchie plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u een migratie taak in uw Configuration Manager omgeving instelt, moet u een bron hiërarchie configureren en gegevens uit minstens één bron site in die hiërarchie verzamelen. Gebruik de volgende secties om u te helpen bij het plannen van het configureren van bron hiërarchieën, het configureren van bron sites en het bepalen van de manier waarop Configuration Manager informatie verzamelt van de bron sites in de bron hiërarchie. 

##  <a name="source-hierarchies"></a><a name="BKMK_Source_Hierarchies"></a>Bron hiërarchieën  
Een bron hiërarchie is een Configuration Manager-hiërarchie die gegevens bevat die u wilt migreren. Wanneer u de migratie instelt en een bron hiërarchie opgeeft, geeft u de site op het hoogste niveau van de bron hiërarchie op. Deze site wordt ook een bronsite genoemd. Extra sites waaruit u gegevens kunt migreren in de bron hiërarchie worden ook wel bron sites genoemd.  

-   Wanneer u een migratie taak instelt om gegevens van een Configuration Manager 2007-bron hiërarchie te migreren, configureert u deze voor het migreren van gegevens van een of meer specifieke bron sites in de bron hiërarchie.  

-   Wanneer u een migratie taak instelt voor het migreren van gegevens uit een bron hiërarchie waarop System Center 2012 Configuration Manager of hoger wordt uitgevoerd, hoeft u alleen de site op het hoogste niveau op te geven.  

U kunt slechts één bron hiërarchie per keer instellen.  

-   Als u een nieuwe bron hiërarchie instelt, wordt die hiërarchie automatisch de huidige bron hiërarchie, waarbij de vorige bron hiërarchie wordt vervangen.  

-   Bij het instellen van een bron hiërarchie moet u de site op het hoogste niveau van de bron hiërarchie opgeven en referenties opgeven voor Configuration Manager die moeten worden gebruikt om verbinding te maken met de SMS-provider en de site database van die bron site.  

-   Configuration Manager gebruikt deze referenties voor het uitvoeren van gegevens verzameling om informatie op te halen over de objecten en distributie punten van de bron site.  

-   Als onderdeel van het proces voor gegevensverzameling worden onderliggende sites in de bronhiërarchie geïdentificeerd.  

-   Als de bron hiërarchie een Configuration Manager 2007-hiërarchie is, kunt u die aanvullende sites instellen als bron sites met afzonderlijke referenties voor elke bron site.  

Hoewel u meerdere bron hiërarchieën achter elkaar kunt instellen, is migratie slechts voor één bron hiërarchie tegelijk actief.  

-   Als u een aanvullende bron hiërarchie instelt voordat u de migratie van de huidige bron hiërarchie voltooit, Configuration Manager alle actieve migratie taken geannuleerd en worden geplande migratie taken voor de huidige bron hiërarchie uitgesteld.  

-   De zojuist geconfigureerde bron hiërarchie wordt vervolgens de huidige bron hiërarchie en de oorspronkelijke bron hiërarchie is nu inactief.  

-   Vervolgens kunt u verbindings referenties, aanvullende bron sites en migratie taken voor de nieuwe bron hiërarchie instellen.  

Als u een inactieve bron hiërarchie herstelt en nog niet eerder **opschoon migratie gegevens**hebt gebruikt, kunt u de eerder geconfigureerde migratie taken voor die bron hiërarchie weer geven. Voordat u de migratie vanuit die hiërarchie kunt voortzetten, moet u de referenties opnieuw configureren om verbinding te maken met de betreffende bronsites in de hiërarchie. Plan vervolgens de migratietaken opnieuw die niet zijn voltooid.  

> [!CAUTION]  
>  Als u gegevens uit meerdere bronhiërarchieën wilt migreren, moet elke aanvullende bronhiërarchie een unieke verzameling sitecodes bevatten.  
> Bron-en doel hiërarchieën moeten ook een andere set site codes hebben.

Zie voor meer informatie over het configureren van een bron hiërarchie [bron hiërarchieën en bron sites configureren voor migratie naar Configuration Manager current branch](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="source-sites"></a><a name="BKMK_Source_Sites"></a> Bronsites  
 Bronsites zijn de sites in de bronhiërarchie met de gegevens die u wilt migreren. De site op het hoogste niveau van de bronhiërarchie is altijd de eerste bronsite. Wanneer tijdens de migratie gegevens uit de eerste bronsite van een nieuwe bronhiërarchie worden verzameld, wordt er informatie over aanvullende sites in die hiërarchie gedetecteerd.  

 Welke acties u na het verzamelen van gegevens voor de oorspronkelijke bronsite kunt uitvoeren, is afhankelijk van de productversie van de bronhiërarchie.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Bronsites waarop Configuration Manager 2007 SP2 wordt uitgevoerd  
 Nadat de gegevens zijn verzameld van de oorspronkelijke bron site van de Configuration Manager 2007 SP2-hiërarchie, hoeft u geen aanvullende bron sites in te stellen voordat u migratie taken maakt. Voordat u gegevens van aanvullende sites kunt migreren, moet u echter aanvullende sites als bron sites instellen en Configuration Manager moet gegevens van deze sites worden verzameld.  

 Als u gegevens wilt verzamelen uit extra sites, stelt u elke site afzonderlijk in als een bron site. Hiervoor moet u de referenties voor Configuration Manager opgeven om verbinding te maken met de SMS-provider en de site database van elke bron site. Nadat u de referenties voor een bron site hebt ingesteld, begint het proces voor het verzamelen van gegevens voor die site.  

 Wanneer u aanvullende bron sites in een Configuration Manager 2007 SP2-bron hiërarchie hebt ingesteld, moet u de bron sites van boven naar beneden instellen. Dit betekent dat u de sites op het laagste niveau als laatste hebt ingesteld. U kunt op elk gewenst moment bron sites in een vertakking van de hiërarchie configureren, maar u moet een site als een bron site instellen voordat u een van de onderliggende sites als bron sites instelt.  

> [!NOTE]  
>  Alleen primaire sites in een Configuration Manager 2007 SP2-hiërarchie worden ondersteund voor migratie.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Bron sites waarop System Center 2012 Configuration Manager of hoger wordt uitgevoerd  
 Nadat de gegevens zijn verzameld van de oorspronkelijke bron site van de hiërarchie van System Center 2012 Configuration Manager of hoger, hoeft u geen aanvullende bron sites in die bron hiërarchie in te stellen. Dit komt doordat in tegens telling tot Configuration Manager 2007, deze versies van Configuration Manager gebruikmaken van een gedeelde data base, en met de gedeelde data base kunt u alle beschik bare objecten van de oorspronkelijke bron site identificeren en vervolgens migreren.  

 Wanneer u de toegangs accounts hebt ingesteld om gegevens te verzamelen, moet u mogelijk het **SMS-provider account van de bron site** toegang verlenen tot meerdere computers in de bron hiërarchie. Dit kan nodig zijn wanneer de bronsite meerdere exemplaren van de SMS-provider ondersteunt, elk op een andere computer. Wanneer wordt begonnen met het verzamelen van gegevens, neemt de site op het hoogste niveau van de doelhiërarchie contact op met de site op het hoogste niveau in de bronhiërarchie om de locaties van de SMS-provider voor die site te identificeren. Alleen het eerste exemplaar van de SMS-provider wordt geïdentificeerd. Als het proces voor gegevensverzameling geen toegang tot de SMS-provider op de geïdentificeerde locatie krijgt, mislukt het proces en wordt er geen verbinding gemaakt met andere computers waarop een exemplaar van de SMS-provider voor die site wordt uitgevoerd.  

##  <a name="data-gathering"></a><a name="BKMK_Data_Gathering"></a> Gegevens verzamelen  
 Nadat u een bron hiërarchie hebt opgegeven, moet u de referenties voor elke extra bron site in een bron hiërarchie instellen, of de distributie punten voor een bron site delen Configuration Manager begint met het verzamelen van gegevens van de bron site.  

 Het proces voor gegevensverzameling wordt vervolgens herhaald op basis van een eenvoudig schema om ervoor te zorgen dat eventuele wijzigingen in de bronsite worden gesynchroniseerd. Standaard wordt het proces elke vier uur herhaald. U kunt de planning voor deze cyclus wijzigen door de **Eigenschappen** van de bron site te bewerken. Het eerste proces voor het verzamelen van gegevens moet alle objecten in de Configuration Manager-Data Base controleren en kan een lange tijd duren om te volt ooien. Omdat tijdens volgende processen voor gegevensverzameling alleen wijzigingen in de gegevens worden geïdentificeerd, nemen deze minder tijd in beslag.  

 De site op het hoogste niveau in de doelhiërarchie maakt verbinding met de SMS-provider en de sitedatabase van de bronsite om een lijst met objecten en distributiepunten op te halen. Voor deze verbindingen worden de toegangsaccounts van de bronsite gebruikt. Zie [vereisten voor migratie](../../core/migration/prerequisites-for-migration.md)voor informatie over de vereiste configuraties voor het verzamelen van gegevens.  

 U kunt het proces voor gegevens verzameling starten en stoppen met behulp van **gegevens verzamelen nu** en stoppen met het **verzamelen van gegevens** in de Configuration Manager-console.  

 Nadat u het **verzamelen van gegevens** voor een bron site om welke reden dan ook hebt gebruikt, moet u de referenties voor de site opnieuw configureren voordat u weer gegevens van die site kunt verzamelen. Totdat u de bron site opnieuw configureert, kunnen Configuration Manager nieuwe objecten of wijzigingen in eerder gemigreerde objecten op die site niet identificeren.  

> [!NOTE]  
>  Voordat u een zelfstandige primaire site uitbreidt in een hiërarchie met een centrale beheer site, moet u stoppen met het verzamelen van gegevens. U kunt het verzamelen van gegevens opnieuw configureren nadat de site-uitbrei ding is voltooid.  

### <a name="gather-data-now"></a>Gegevens nu verzamelen  
 Wanneer het oorspronkelijke gegevensverzamelingsproces voor een site is voltooid, wordt dit proces herhaald om objecten te identificeren die zijn bijgewerkt sinds de laatste gegevensverzamelingscyclus. U kunt ook de actie **gegevens nu verzamelen** in de Configuration Manager-console gebruiken om het proces direct te starten en de start tijd van de volgende cyclus opnieuw in te stellen.  

 Wanneer een proces voor gegevensverzameling is voltooid voor een bronsite, kunt u de distributiepunten delen vanaf de bronsite en migratietaken zo configureren dat gegevens via de site worden gemigreerd. Gegevens verzameling is een herhalend proces voor migratie en wordt voortgezet totdat u de bron hiërarchie wijzigt of het **verzamelen van gegevens stopt** om het proces voor het verzamelen van gegevens voor die site te beëindigen.  

### <a name="stop-gathering-data"></a>Geen gegevens meer verzamelen  
 U kunt **Stop gegevens verzamelen** gebruiken om het proces voor het verzamelen van gegevens voor een bron site te beëindigen wanneer u niet langer wilt Configuration Manager om nieuwe of gewijzigde objecten van die site te identificeren. Deze actie voor komt ook dat Configuration Manager clients in de doel hiërarchie aanbiedt als gedeelde distributie punten van de bron als inhouds locaties voor de inhoud die u hebt gemigreerd.  

 Als u het verzamelen van gegevens van elke bron site wilt stoppen, moet u stoppen met het **verzamelen van gegevens** op de bron sites op de onderste laag en het proces vervolgens op elke bovenliggende site herhalen. De site op het hoogste niveau van de bronhiërarchie moet de laatste site zijn waarop u de gegevensverzameling beëindigt. U moet de gegevensverzameling voor elke onderliggende site beëindigen voordat u deze actie uitvoert voor een bovenliggende site. U kunt de gegevensverzameling alleen beëindigen wanneer u klaar bent om het migratieproces te voltooien.  

 Nadat u het verzamelen van gegevens voor een bron site hebt gestopt, blijven de eerder verzamelde gegevens over objecten en verzamelingen van die site beschikbaar voor gebruik bij het instellen van nieuwe migratie taken. Er worden echter geen nieuwe objecten of verzamelingen weer gegeven, en ook de wijzigingen die zijn aangebracht aan bestaande objecten worden niet weer gegeven. Als u de bronsite opnieuw configureert en weer begint met het verzamelen van gegevens, worden de status en andere gegevens over eerder gemigreerde objecten weergegeven.  
