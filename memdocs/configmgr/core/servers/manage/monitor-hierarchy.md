---
title: De hiërarchie bewaken
titleSuffix: Configuration Manager
description: Lees hoe u uw infra structuur in Configuration Manager kunt controleren met behulp van de werk ruimte bewaking in de-console.
ms.date: 06/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 007dbb73-18a7-48a3-a489-97cf9fc4f140
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 504943df58c0471a0ef821a269cc22b2d12d76d8
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068035"
---
# <a name="monitor-the-hierarchy"></a>De hiërarchie bewaken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u uw hiërarchie in Configuration Manager wilt bewaken, gebruikt u de werk ruimte **bewaking** in de Configuration Manager-console.  

> [!NOTE]  
> De uitzonde ring op deze locatie is bij het migreren van sites. Dit proces wordt bewaakt in het knoop punt **migratie** van de werk ruimte **beheer** . Zie [bewerkingen voor de migratie naar Configuration Manager current branch](../../migration/operations-for-migration.md)voor meer informatie.  

Gebruik de volgende functies in combi natie met de Configuration Manager-console voor bewaking:

- [Inleiding op rapportage](introduction-to-reporting.md)
- [Logboek bestanden](../../plan-design/hierarchy/log-files.md).  

Als u sites controleert, zoekt u tekens die duiden op problemen waarvoor u actie moet ondernemen. Bijvoorbeeld:  

- Achterstand van bestanden op siteservers en sitesystemen.  

- Statusberichten die wijzen op een fout of een probleem.  

- Intrasitecommunicatie mislukt.  

- Fout- en waarschuwingsberichten in het logboek voor systeemgebeurtenissen op servers.  

- Fout- en waarschuwingsberichten in het foutenlogboek van Microsoft SQL Server.  

- Sites of clients die gedurende een lange periode geen status hebben gerapporteerd.  

- Trage reactie van de SQL Server-database.  

- Tekenen van hardwarefout.  

Als bewakings taken signalen van problemen onthullen, onderzoekt u de bron van het probleem. Herstel het vervolgens snel om het risico van een storing van een site te minimaliseren.  


## <a name="monitor-common-management-tasks"></a><a name="BKMK_MonintorMgmtTasks"></a> Algemene beheer taken bewaken

Configuration Manager biedt ingebouwde bewaking vanuit de Configuration Manager-console.

### <a name="alerts"></a>Waarschuwingen

Zie [waarschuwingen controleren](use-alerts-and-the-status-system.md#BKMK_MonitorAlerts)voor meer informatie.  

### <a name="compliance-settings"></a>Instellingen voor naleving

Zie [nalevings instellingen controleren](../../../compliance/deploy-use/monitor-compliance-settings.md)voor meer informatie.

### <a name="content"></a>Inhoud

Zie [inhoud en infra structuur](../deploy/configure/manage-content-and-content-infrastructure.md)voor inhoud beheren voor algemene informatie over het bewaken van inhoud.  

Voor meer informatie over het bewaken van specifieke typen inhoud:

- [Toepassingen bewaken](../../../apps/deploy-use/monitor-applications-from-the-console.md)

- [Pakketten en Program ma's bewaken](../../../apps/deploy-use/packages-and-programs.md#monitor-packages-and-programs)  

- [Inhoud voor software-updates bewaken](../../../sum/deploy-use/monitor-software-updates.md#BKMK_MonitorContent)

- [Inhoud bewaken voor besturingssysteem implementaties](../../../osd/deploy-use/monitor-operating-system-deployments.md#BKMK_MonitorContent)

### <a name="endpoint-protection"></a>Endpoint Protection

Zie [Endpoint Protection bewaken](../../../protect/deploy-use/monitor-endpoint-protection.md)voor meer informatie.  

### <a name="os-deployment"></a>Besturingssysteemimplementatie

Zie [implementaties van besturings systemen bewaken](../../../osd/deploy-use/monitor-operating-system-deployments.md)voor meer informatie.

### <a name="monitor-power-management"></a>Energie beheer controleren

Zie [energie beheer bewaken en plannen voor](../../clients/manage/power/monitor-and-plan-for-power-management.md)meer informatie.  

### <a name="monitor-software-metering"></a>Software licentie controle bewaken

Zie [app-gebruik controleren met software meter](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)voor meer informatie.  

### <a name="monitor-software-updates"></a>Software-updates controleren

Zie [software-updates bewaken](../../../sum/deploy-use/monitor-software-updates.md)voor meer informatie.  


## <a name="monitor-the-site-hierarchy"></a><a name="BKMK_SH_Node"></a> De site hiërarchie bewaken

Het knoop punt **site hiërarchie** van de werk ruimte **bewaking** biedt u een overzicht van uw Configuration Manager hiërarchie en intersite-koppelingen. 

Gebruik het knoop punt **site hiërarchie** om de status van elke site te controleren. Bewaak ook de koppelingen voor intersitereplicatie en hun relatie met externe factoren, zoals een geografische locatie.  

Zowel site status als intersite-koppelings status worden gerepliceerd als site gegevens en niet als algemene gegevens. Wanneer u uw Configuration Manager-console verbindt met een onderliggende primaire site, kunt u de site of de koppelings status voor andere primaire sites of hun onderliggende secundaire sites niet weer geven. Als u bijvoorbeeld in een hiërarchie met meerdere primaire sites verbinding maakt met de-console met een primaire site, kunt u de status van onderliggende secundaire sites, de primaire site en de centrale beheer site weer geven. In deze weer gave kunt u de status voor andere sites onder de centrale beheer site niet zien.  

Als u de weer gave in het knoop punt **site hiërarchie** wilt beheren, gebruikt u de actie **instellingen configureren** . De hiërarchie repliceert de instellingen die u configureert in dit knoop punt.  

### <a name="hierarchy-diagram"></a>Diagram van hiërarchie

Het hiërarchiediagram geeft uw sites in een topologiekaart weer. Selecteer een site en Bekijk een samen vatting van status berichten van die site. Zoom in om status berichten weer te geven en toegang te krijgen tot de **Eigenschappen**van de site.  

Als u de status op hoog niveau wilt weer geven voor een site of replicatie koppeling tussen sites, plaatst u de muis aanwijzer boven het object. De replicatie koppelings status wordt niet globaal gerepliceerd. Als u de details van de replicatie koppeling tussen alle primaire sites in een hiërarchie wilt weer geven, koppelt u de console aan de centrale beheer site.  

De volgende opties wijzigen het hiërarchiediagram:  

#### <a name="groups"></a>Groepen

Het aantal primaire sites en secundaire sites configureren die een wijziging activeren in het hiërarchie diagram. Met deze wijziging in de weer gave worden de sites gecombineerd in één object. Vervolgens ziet u het totaal aantal sites en een Rollup van status berichten en de status van de site.

#### <a name="favorite-sites"></a>Favoriete sites

Geef afzonderlijke sites op als favoriete site. Een ster-icoontje identificeert een favoriete site in het hiërarchiediagram. Favoriete sites worden niet gecombineerd met andere sites wanneer u groepen gebruikt. Ze worden altijd afzonderlijk weer gegeven.  

### <a name="geographical-view"></a>Geografische weergave

> [!IMPORTANT]
> Vanaf 2020 augustus is deze functie afgeschaft. Gebruik de optie **hiërarchie diagram** .<!--8116777-->

De geografische weergave toont de locatie van elke site op een geografische kaart. Alleen de sites die u met een locatie configureert worden weer gegeven. Wanneer u een site in deze weer gave selecteert, worden de replicatie koppelingen naar bovenliggende of onderliggende sites weer gegeven. In tegens telling tot de weer gave hiërarchie diagram kunt u geen site status bericht of Details van replicatie koppelingen weer geven in deze weer gave.  

> [!NOTE]  
> Als u de geografische weer gave wilt gebruiken, moet de computer waarop uw Configuration Manager-console verbinding maakt, Internet Explorer hebben geïnstalleerd en toegang hebben tot Bing-Kaarten met behulp van het HTTP-protocol.  

De volgende optie wijzigt de geografische weer gave:  

#### <a name="site-location"></a>Site locatie

Geef een geografische locatie voor elke site op met behulp van een van de volgende typen:

- Een adres
- Een naam van een plaats, zoals de naam van een stad
- Door coördinaten voor breedte graad en lengte graad

Als u bijvoorbeeld de breedte graad en de lengte graad van Redmond, Washington wilt gebruiken, geeft u **N 47 40 26,3572 W 122 7 17,4432** op als locatie van de site. U hoeft de symbolen voor de graden, minuten of seconden van de breedte graad of lengte graad niet op te geven. Configuration Manager maakt gebruik van Bing Maps om de locatie in de geografische weer gave weer te geven. Vervolgens kunt u uw hiërarchie weer geven met de geografische locaties. Deze weer gave biedt inzicht in regionale problemen die van invloed kunnen zijn op specifieke sites of intersitereplicatie.  

Wanneer u een locatie opgeeft, kunt u het vak **Locatie** gebruiken om naar een specifieke site in uw hiërarchie te zoeken. Als de site is geselecteerd is, voert u de locatie in als stadsnaam of straatadres in de kolom **Locatie** . Configuration Manager gebruikt Bing-Kaarten om de locatie op te lossen.  

<a name="BKMK_MonitorRepLinksAndStatuss"></a>

## <a name="next-steps"></a>Volgende stappen

[Database replicatie bewaken](monitor-replication.md)
