---
title: Migratie voltooien
titleSuffix: Configuration Manager
description: Meer informatie over het volt ooien van de migratie naar een Configuration Manager huidige vertakkings doel hiërarchie nadat een bron hiërarchie geen gegevens meer heeft.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76cf6b57a4bc1439f2aa9c2e0484271987f85748
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713007"
---
# <a name="plan-to-complete-migration-in-configuration-manager"></a>Het volt ooien van de migratie in Configuration Manager plannen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met Configuration Manager kunt u het migratie proces volt ooien wanneer een bron hiërarchie geen gegevens meer bevat die u naar uw doel hiërarchie wilt migreren. Het volt ooien van de migratie omvat de volgende algemene stappen:  

-   Zorg ervoor dat de gegevens die u nodig hebt, zijn gemigreerd. Voordat u de migratie van een bron hiërarchie voltooit, moet u ervoor zorgen dat u alle resources van de bron hiërarchie hebt gemigreerd die u nodig hebt in de doel hiërarchie. Dit kunnen gegevens en clients zijn.  

-   Stop met het verzamelen van gegevens van bron sites. Als u de migratie van een bron hiërarchie wilt volt ooien, moet u eerst het verzamelen van gegevens van bron sites stoppen.  

-   Migratie gegevens opruimen. Nadat u het verzamelen van gegevens van alle bron sites in een bron hiërarchie hebt gestopt, kunt u gegevens over het migratie proces en de bron hiërarchie verwijderen uit de data base van de doel hiërarchie.  

-   Buiten gebruik stellen van de bron hiërarchie. Nadat u de migratie van een bron hiërarchie hebt voltooid en die hiërarchie geen resources meer heeft die u beheert, kunt u de sites in de bron hiërarchie buiten gebruik stellen en de gerelateerde infra structuur uit uw omgeving verwijderen. Raadpleeg de documentatie voor die versie van Configuration Manager voor meer informatie over het buiten gebruik stellen van sites en bron hiërarchieën.  

Gebruik de volgende secties om u te helpen bij het plannen van de migratie van een bron hiërarchie door het stoppen van het verzamelen van gegevens en het opschonen van migratie gegevens:  

-   [Plannen om het verzamelen van gegevens te stoppen](#Plan_to_Stop_Data_Gath)  

-   [Het opschonen van migratie gegevens plannen](#Plan_to_clean_up)  

##  <a name="plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a>Plannen om het verzamelen van gegevens te stoppen  
 Voordat u de migratie voltooit en de migratie gegevens opruimt, moet u stoppen met het verzamelen van gegevens van elke bron site in de bron hiërarchie. Als u wilt stoppen met het verzamelen van gegevens van elke bron site, moet u de opdracht **gegevens verzamelen stoppen** uitvoeren op de bron sites van de onderste laag en het proces vervolgens op elke bovenliggende site herhalen. De site op het hoogste niveau van de bronhiërarchie moet de laatste site zijn waarop u de gegevensverzameling beëindigt. U moet het verzamelen van gegevens op elke onderliggende site stoppen voordat u deze opdracht uitvoert op een bovenliggende site. Normaal gesp roken stopt u het verzamelen van gegevens wanneer u klaar bent om het migratie proces te volt ooien.  

 Nadat u het verzamelen van gegevens van een bron site hebt gestopt, zijn gedeelde distributie punten van die site niet meer beschikbaar als inhouds locaties voor clients in de doel hiërarchie. Zorg er daarom voor dat alle gemigreerde inhoud waarvan de clients in de doel hiërarchie toegang hebben, beschikbaar moet blijven via een van de volgende opties:  

-   Distribueer de inhoud in de doel hiërarchie naar ten minste één distributie punt.  

-   Voordat u stopt met het verzamelen van gegevens van een bron site, moet u een upgrade uitvoeren of gedeelde distributie punten met de vereiste inhoud opnieuw toewijzen. Voor meer informatie over het bijwerken of opnieuw toewijzen van gedeelde distributie punten, zie de betreffende secties in [een strategie voor de migratie van een inhouds implementatie plannen](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Nadat u het verzamelen van gegevens van elke bron site in de bron hiërarchie hebt gestopt, kunt u de migratie gegevens opruimen. Totdat u de migratie gegevens opschoont, blijft elke migratie taak die is uitgevoerd of die is gepland om te worden uitgevoerd, toegankelijk in de Configuration Manager-console.  

Zie [een strategie voor een bron hiërarchie plannen](../../core/migration/planning-a-source-hierarchy-strategy.md)voor meer informatie over bron sites en het verzamelen van gegevens.  

##  <a name="plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a>Het opschonen van migratie gegevens plannen  
 De laatste stap die is vereist om de migratie te volt ooien, is het opschonen van migratie gegevens. U kunt de opdracht **migratie gegevens opruimen** gebruiken nadat u hebt gestopt met het verzamelen van gegevens voor elke bron site in de bron hiërarchie. Met deze optionele actie worden gegevens over de huidige bron hiërarchie verwijderd uit de data base van de doel hiërarchie.  

 Wanneer u migratie gegevens opruimt, worden de meeste gegevens over de migratie verwijderd uit de data base van de doel hiërarchie. Details over gemigreerde objecten worden echter wel bewaard. Met deze gegevens kunt u de werk ruimte **migratie** gebruiken om de bron hiërarchie opnieuw te configureren die de gegevens bevat die zijn gemigreerd om de migratie van die bron hiërarchie te hervatten, of om de objecten en het eigendom van de site te controleren van de objecten die eerder zijn gemigreerd.  
