---
title: Onderhoudstaken
titleSuffix: Configuration Manager
description: Begrijp welke onderhouds taken moeten worden uitgevoerd voor Configuration Manager-sites en-hiërarchieën en wanneer ze moeten worden uitgevoerd.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0a71fc2f09e967944adfc4266e25eb20acfb9fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713728"
---
# <a name="maintenance-tasks-for-configuration-manager"></a>Onderhouds taken voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager-sites en-hiërarchieën hebben regel matig onderhoud en bewaking nodig om services effectief en continu te kunnen leveren. Regel matig onderhoud zorgt ervoor dat de hardware-, software-en Configuration Manager-Data Base op de juiste en efficiënte wijze blijven functioneren. Optimale prestaties verminderen het risico op fouten aanzienlijk.  

 Zie [waarschuwingen en het status systeem voor Configuration Manager gebruiken](../../../core/servers/manage/use-alerts-and-the-status-system.md)om waarschuwingen in te stellen en het status systeem te gebruiken om de status van Configuration Manager te controleren.  

## <a name="maintenance-tasks"></a><a name="bkmk_MTs"></a>Onderhouds taken

 Regel matig onderhoud is belang rijk om te zorgen voor de juiste site bewerkingen. Bewaar een onderhouds logboek voor het vastleggen van onderhouds datums, die onderhoud hebben ondervonden en eventuele opmerkingen met betrekking tot het onderhoud van de taken. Overweeg dagelijks of wekelijks onderhoud om uw site bij te houden. Voor sommige taken is mogelijk een andere planning vereist. Algemeen onderhoud kan zowel de ingebouwde onderhouds taken als andere taken zoals account onderhoud bevatten om naleving van uw bedrijfs beleid te behouden.  

 Gebruik de volgende informatie als richt lijn om te helpen bij het plannen van verschillende onderhouds taken. Gebruik deze lijsten als uitgangs punt en voeg taken toe die u mogelijk nodig hebt.  

### <a name="daily-tasks"></a>Dagelijkse taken
Hieronder vindt u onderhouds taken die u bij een dagelijks schema kunt overwegen:  

- Controleer of vooraf gedefinieerde onderhouds taken die dagelijks moeten worden uitgevoerd, correct worden uitgevoerd.  

- Controleer de status van de Configuration Manager-Data Base.  

- Controleer de status van de site server.  

- Controleer Configuration Manager in het postvak in van het site systeem op bestands achterstand.  

- Controleer de status van site systemen.  

- Controleer de gebeurtenis logboeken van het besturings systeem op de site systemen.  

- Controleer het SQL Server fouten logboek van de site database computer.  

- Controleer de systeem prestaties.  

- Controleer Configuration Manager waarschuwingen.  

### <a name="weekly-tasks"></a>Wekelijks taken

Hieronder vindt u onderhouds taken die u kunt overwegen voor een wekelijks schema:  

- Controleer of vooraf gedefinieerde onderhouds taken die wekelijks worden uitgevoerd, correct worden uitgevoerd.  

- Verwijder onnodige bestanden van site systemen.  

- Maak en distribueer zo nodig rapporten van eind gebruikers.  

- Maak een back-up van de toepassings-, beveiligings-en systeem gebeurtenis logboeken en schakel deze uit.  

- Controleer de grootte van de site database en controleer of er voldoende schijf ruimte beschikbaar is op de site database server, zodat de site database kan groeien.  

- SQL Server database onderhoud in de site database op basis van uw SQL Server onderhouds plan.  

- Controleer de beschik bare schijf ruimte op alle site systemen.  

- Hulpprogram ma's voor Schijfdefragmentatie uitvoeren op alle site systemen.  

### <a name="periodic-tasks"></a>Periodieke taken

Sommige taken waarvoor dagelijks of wekelijks onderhoud niet is vereist, zijn belang rijk om de algehele status van de site te garanderen. Deze taken zorgen er ook voor dat de plannen voor beveiliging en herstel na nood gevallen up-to-date zijn. Hieronder vindt u onderhouds taken die u kunt overwegen voor een meer periodieke planning dan de dagelijkse of wekelijkse taken:  

- Wijzig accounts en wacht woorden, indien nodig, volgens uw beveiligings plan.  

- Bekijk het onderhouds plan om te controleren of geplande onderhouds taken correct en effectief zijn gepland, afhankelijk van de geconfigureerde site-instellingen.  

- Bekijk het ontwerp van de Configuration Manager-hiërarchie voor alle vereiste wijzigingen.  

- Controleer de netwerk prestaties om er zeker van te zijn dat er geen wijzigingen zijn aangebracht die van invloed zijn op site bewerkingen.  

- Controleer of Active Directory instellingen die van invloed zijn op site bewerkingen, niet zijn gewijzigd. Controleer bijvoorbeeld of subnetten die zijn toegewezen aan Active Directory sites en die als grenzen worden gebruikt voor Configuration Manager site niet zijn gewijzigd.  

- Raadpleeg uw plan voor herstel na nood gevallen voor alle vereiste wijzigingen.  

- Voer een site Recovery uit op basis van het herstel plan voor nood gevallen in een testlab met behulp van een back-up van de meest recente back-up die de onderhouds taak van de back-upserver van site heeft gemaakt.

- Controleer de hardware op fouten of beschik bare hardware-updates.  

- Controleer de algemene status van de site.  

## <a name="maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a>De operationele status van uw site database onderhouden

 Hoewel uw Configuration Manager-site en-hiërarchie de taken uitvoeren die u plant en instelt, voegen site onderdelen voortdurend gegevens toe aan de Configuration Manager-Data Base. Naarmate de hoeveelheid gegevens toeneemt, wordt de prestaties van de data base en de vrije opslag ruimte in de data base geweigerd. U kunt site-onderhouds taken instellen om verouderde gegevens te verwijderen die u niet meer nodig hebt.  

 Configuration Manager biedt vooraf gedefinieerde onderhouds taken die u kunt gebruiken om de status van de Configuration Manager-Data Base te behouden. Niet alle onderhouds taken zijn standaard beschikbaar op elke site. Er zijn verschillende taken ingeschakeld terwijl er nog geen zijn en er wordt een schema ondersteund dat u kunt instellen.  

 De meeste onderhouds taken verwijderen regel matig verouderde gegevens uit de Configuration Manager Data Base. Het verminderen van de grootte van de data base door overbodige gegevens te verwijderen verbetert de prestaties en de integriteit van de data base, waardoor de efficiëntie van de site en hiërarchie wordt verhoogd. Andere taken, zoals het **opnieuw samen stellen van indexen**, helpen bij het onderhouden van de efficiëntie van de data base. Andere taken, zoals de taak **back-upserver van site** , helpen u voor te bereiden op nood herstel.  

> [!IMPORTANT]
> Wanneer u de planning van een taak plant waarmee gegevens worden verwijderd, moet u rekening houden met het gebruik van die gegevens in de hiërarchie. Wanneer een taak die gegevens verwijdert op een site wordt uitgevoerd, wordt de informatie uit de Configuration Manager-Data Base verwijderd en wordt deze wijziging gerepliceerd naar alle sites in de hiërarchie. Deze verwijdering kan van invloed zijn op andere taken die afhankelijk zijn van die gegevens. Op de centrale beheer site kunt u bijvoorbeeld detectie instellen om één keer per maand uit te voeren om niet-client computers te identificeren. U bent van plan de Configuration Manager-client op deze computers binnen twee weken na de detectie te installeren. Op één site in de hiërarchie wordt de taak verouderde detectie gegevens verwijderen echter ingesteld om elke zeven dagen uit te voeren. Het resultaat is dat zeven dagen nadat niet-client computers zijn gedetecteerd, worden verwijderd uit de Configuration Manager Data Base. Op de centrale beheer site gaat u de push-installatie van de Configuration Manager-client naar deze nieuwe computers op dag 10 voorbereiden. Maar omdat de taak verouderde detectie gegevens verwijderen onlangs is uitgevoerd en verwijderde gegevens die zeven dagen of ouder zijn, zijn de onlangs ontdekte computers niet meer beschikbaar in de data base.

Nadat u een Configuration Manager-site hebt geïnstalleerd, controleert u de beschik bare onderhouds taken en schakelt u de taken in die voor uw bewerkingen zijn vereist. Controleer het standaard schema van elke taak en stel, indien nodig, de planning in om de onderhouds taak af te stemmen op uw hiërarchie en omgeving. Hoewel het standaard schema van elke taak aan de meeste omgevingen moet voldoen, kunt u de prestaties van uw sites en data base bewaken en verwacht de taken te verfijnen om de efficiëntie van uw implementatie te verg Roten. Plan om de prestaties van de site en de data base periodiek te controleren en onderhouds taken en de bijbehorende planningen opnieuw te configureren om de efficiëntie te hand haven.  

## <a name="set-up-maintenance-tasks"></a>Onderhouds taken instellen

 Elke Configuration Manager site ondersteunt onderhouds taken die de operationele efficiëntie van de site database helpen houden. Er zijn standaard verschillende onderhouds taken ingeschakeld op elke site, en alle taken bieden ondersteuning voor onafhankelijke schema's. Onderhouds taken worden afzonderlijk ingesteld voor elke site en gelden voor de Data Base op die site. Sommige taken, zoals **verouderde detectie gegevens verwijderen**, zijn echter van invloed op de informatie die beschikbaar is in alle sites in een hiërarchie.  

 Alleen de onderhouds taken die u op een site kunt instellen, worden weer gegeven in de Configuration Manager-console. Zie [naslag voor onderhouds taken voor Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md)voor een volledige lijst met onderhouds taken per site type.  

 Gebruik de volgende procedure om u te helpen bij het instellen van de algemene instellingen van onderhouds taken.  

### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1906"></a><a name="bkmk_MTs1906"></a>Onderhouds taken instellen voor Configuration Manager versie 1906
<!--3555894-->
Vanaf versie 1906 kunnen onderhouds taken voor site servers nu worden weer gegeven, bewerkt en gecontroleerd op hun eigen tabblad in de detail weergave van een site server. U kunt nog steeds onderhouds taken bewerken door **site onderhoud** te kiezen in de groep **instellingen** , zoals in eerdere versies van Configuration Manager.

1. Ga in de Configuration Manager-console naar **beheer** > **site configuratie** >**sites**.
1. Selecteer een site in de lijst en klik vervolgens op het tabblad **onderhouds taken** in het deel venster Details.
1. Alleen taken die beschikbaar zijn op de geselecteerde site worden weer gegeven. Klik met de rechter muisknop op een van de onderhouds taken en kies een van de volgende opties:
   - **Schakel** de taak inschakelen in.
   - **Schakel** de taak uit.
   - **Bewerken** : Bewerk het taak schema of de eigenschappen ervan.

![Tabblad voor onderhouds taken in de detail weergave van een site server](./media/3555894-maintenance-tasks.png)

Op het tabblad **onderhouds taken** vindt u informatie zoals:

- Als de taak is ingeschakeld
- Het taak schema
- Laatste start tijd
- Tijdstip van de laatste voltooiing
- Als de taak is voltooid
 
### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1902-and-prior"></a>Onderhouds taken voor Configuration Manager versie 1902 en eerder instellen

1. Ga in de Configuration Manager-console naar **beheer** > **site configuratie** >**sites**.
2. Kies de site met de onderhouds taak die u wilt instellen.  
3. Klik op het tabblad **Start** in de groep **instellingen** op **site onderhoud**en kies vervolgens de onderhouds taak die u wilt instellen. Alleen taken die beschikbaar zijn op de geselecteerde site worden weer gegeven.

4. Als u de taak wilt instellen, kiest u **bewerken**. Zorg ervoor dat het selectie vakje **deze taak inschakelen** is ingeschakeld en stel een schema in voor wanneer de taak wordt uitgevoerd. Als de taak ook verouderde gegevens verwijdert, stelt u de ouderdom van gegevens in die uit de Data Base worden verwijderd wanneer de taak wordt uitgevoerd. Kies **OK** om de taak **Eigenschappen**te sluiten.

   > [!NOTE]  
   > Als u **verouderde status berichten wilt verwijderen**, stelt u de ouderdom van gegevens in die u wilt verwijderen wanneer u status filter regels instelt.  

5. Als u de taak wilt in-of uitschakelen zonder de taak eigenschappen te bewerken, kiest u de knop **inschakelen** of **uitschakelen** . Het knop Label wordt gewijzigd, afhankelijk van de huidige configuratie van de taak.  
6. Wanneer u klaar bent met het configureren van de onderhouds taken, kiest u **OK** om de procedure te volt ooien.

## <a name="next-steps"></a>Volgende stappen

[Naslaginformatie voor onderhoudstaken](reference-for-maintenance-tasks.md)
