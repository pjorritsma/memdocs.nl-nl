---
title: Plan voor migratie
titleSuffix: Configuration Manager
description: Meer informatie over sites en hiërarchieën voordat u gegevens migreert naar een Configuration Manager huidige vertakkings doel hiërarchie.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b514e2bb0843801cfa6f0f307af8a5013fc3f9e6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719657"
---
# <a name="plan-for-migration-to-configuration-manager-current-branch"></a>Migratie plannen naar Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u gegevens migreert naar een Configuration Manager huidige branch-doel hiërarchie, moet u ervoor zorgen dat u bekend bent met-sites en-hiërarchieën in Configuration Manager. Zie [Fundamentals of Configuration Manager](../../core/understand/fundamentals.md)voor meer informatie over sites en hiërarchieën.  

Installeer een Configuration Manager huidige vertakkings hiërarchie om de doel hiërarchie te zijn voordat u gegevens migreert vanuit een ondersteunde bron hiërarchie.  

Nadat u de doel hiërarchie hebt geïnstalleerd, stelt u de beheer functies en-functies in die u in de doel hiërarchie wilt gebruiken voordat u begint met het migreren van gegevens.  

Daarnaast moet u mogelijk de overlap ping tussen de bron hiërarchie en de doel hiërarchie plannen. U kunt bijvoorbeeld instellen dat de bron hiërarchie dezelfde netwerk locaties of grenzen als uw doel hiërarchie gebruikt, en u installeert vervolgens nieuwe clients in uw doel hiërarchie en gebruikt automatische site toewijzing. In dit scenario, omdat een nieuw geïnstalleerde Configuration Manager-client een site kan selecteren om vanuit een van beide hiërarchieën toe te voegen, kan de client onjuist worden toegewezen aan de bron hiërarchie. Plan daarom elke nieuwe client in de doel hiërarchie toe te wijzen aan een specifieke site in die hiërarchie in plaats van automatische site toewijzing te gebruiken.  

Zie [overwegingen voor client site toewijzing](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) in [samen werking tussen verschillende versies van Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)voor meer informatie over site toewijzingen.  

Gebruik de volgende artikelen om u te helpen plannen hoe u een ondersteunde bron hiërarchie naar een Configuration Manager-doel hiërarchie migreert:

-   [Vereisten voor migratie](../../core/migration/prerequisites-for-migration.md)  

-   [Controlelijst voor beheerders voor migratieplanning](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Bepalen of gegevens naar Configuration Manager huidige vertakking moeten worden gemigreerd](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Een strategie voor een bron hiërarchie plannen](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Controlelijst voor beheerders voor migratieplanning](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Een strategie voor client migratie plannen](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Een strategie voor de migratie van een inhouds implementatie plannen](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Plannen voor de migratie van Configuration Manager objecten naar Configuration Manager huidige vertakking](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Het bewaken van migratie activiteiten plannen](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Het volt ooien van de migratie plannen](../../core/migration/planning-to-complete-migration.md)  
