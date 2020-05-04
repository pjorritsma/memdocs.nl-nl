---
title: Inleiding op query's
titleSuffix: Configuration Manager
description: Query's maken en uitvoeren om objecten in een Configuration Manager-hiërarchie te zoeken die voldoen aan uw query criteria.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713819"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Inleiding tot query's in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt query's maken en uitvoeren om objecten in een Configuration Manager-hiërarchie te zoeken die voldoen aan uw query criteria. Tot deze objecten behoren items zoals bepaalde typen computers of gebruikers groepen. Query's kunnen de meeste typen Configuration Manager-objecten retour neren, waaronder sites, verzamelingen, toepassingen en inventaris gegevens.  

## <a name="query-creation-overview"></a>Overzicht van het maken van query's

 Wanneer u een query maakt, moet u minstens twee parameters opgeven: waar u wilt zoeken en wat u wilt zoeken. Als u bijvoorbeeld de hoeveelheid vasteschijfruimte wilt vinden die beschikbaar is op alle computers in een Configuration Manager site, kunt u een query maken om te zoeken naar de kenmerk klasse **logische schijf** en het kenmerk **vrije ruimte (MB)** voor de beschik bare ruimte op de vaste schijf.  

 Wanneer u een eerste query hebt gemaakt, kunt u aanvullende querycriteria opgeven. U kunt bijvoorbeeld opgeven dat de queryresultaten alleen computers moeten bevatten die zijn toegewezen aan een opgegeven site. U kunt ook wijzigen hoe resultaten worden weer gegeven, zodat u de resultaten kunt weer geven in een volg orde die voor u zinvol is. U kunt bijvoorbeeld opgeven dat de resultaten worden gesorteerd op de hoeveelheid vrije schijf ruimte, in oplopende of aflopende volg orde.  

 Wanneer u een query maakt, wordt deze opgeslagen door Configuration Manager en weer gegeven in het knoop punt **query's** in de werk ruimte **bewaking** . Vanuit deze locatie kunt u nieuwe query's maken en bestaande query's uitvoeren, bijwerken en beheren.  

 U kunt een query ook importeren in een query regel in een Configuration Manager verzameling. Zie [verzamelingen maken](../../../core/clients/manage/collections/create-collections.md)voor meer informatie.  

## <a name="next-steps"></a>Volgende stappen

 [Query's maken](../../../core/servers/manage/create-queries.md)
