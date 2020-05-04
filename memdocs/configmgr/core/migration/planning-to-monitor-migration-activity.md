---
title: Migratie bewaken
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van de Configuration Manager-console voor het bewaken van de voortgang en het slagen van migratie taken.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713000"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>Planning voor het bewaken van migratie activiteiten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met Configuration Manager kunt u de migratie bewaken in de Configuration Manager-console die verbinding maakt met de doel hiërarchie. In de Configuration Manager-console in de werk ruimte **beheer** kunt u het knoop punt **migratie** gebruiken om de voortgang en het slagen van migratie taken te controleren. U kunt samenvattings informatie weer geven voor elke migratie taak waarmee objecten worden geïdentificeerd die zijn gemigreerd, objecten die nog niet zijn gemigreerd en het aantal objecten dat is uitgesloten van een migratie taak. U ziet ook details over eventuele migratie problemen.  

## <a name="view-migration-progress"></a>Voortgang van migratie weer geven  
 Als u de voortgang van een migratie taak wilt weer geven, gebruikt u een van de volgende acties:  

-   Vouw in de werk ruimte **beheer** van de Configuration Manager-console het knoop punt **migratie taken** uit, selecteer een migratie taak en selecteer vervolgens het tabblad **objecten in taak** .  

-   Gebruik de Configuration Manager-logboek bestanden om de voortgang van de migratie te controleren of om problemen te identificeren. Migratie beheer is het Configuration Manager proces dat migratie acties bijhoudt en registreert deze in het bestand bestand migmctrl. log in de ** \&map\>\\lt; InstallationPath logs** op de site server.  

    > [!NOTE]  
    >  Als een migratie taak mislukt, controleert u zo snel mogelijk de details in het bestand bestand migmctrl. log. De vermeldingen in het migratie logboek worden doorlopend toegevoegd aan het bestand en oude gegevens worden overschreven. Als de vermeldingen worden overschreven, kunt u mogelijk niet bepalen of er problemen zijn die zich kunnen voordoen met de gemigreerde objecten met betrekking tot migratie problemen. Migratie activiteit wordt vastgelegd op de site\-op het hoogste niveau van de hiërarchie, ongeacht de site waarmee uw Configuration Manager-console verbinding maakt wanneer u de migratie configureert.  

-   Gebruik Configuration Manager rapportage. Configuration Manager biedt diverse ingebouwde\-rapporten voor migratie of u kunt deze rapporten bewerken zodat ze aan uw vereisten voldoen. Zie [Introduction to Reporting](../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over Configuration Manager-rapporten.  
