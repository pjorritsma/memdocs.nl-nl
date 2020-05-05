---
title: Internationale ondersteuning
titleSuffix: Configuration Manager
description: Configureer Configuration Manager om te voldoen aan specifieke internationale vereisten.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720938"
---
# <a name="international-support-in-configuration-manager"></a>Internationale ondersteuning in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De volgende secties bevatten technische gegevens die u helpen Configuration Manager compatibel te maken met specifieke internationale vereisten.  

## <a name="gb18030-requirements"></a>GB18030-vereisten  
 Configuration Manager voldoet aan de normen die in GB18030 zijn gedefinieerd, zodat u Configuration Manager in China kunt gebruiken. Een Configuration Manager-implementatie moet de volgende configuraties hebben om te voldoen aan de GB18030-vereisten:  

-   Op elke site Server computer en SQL Server computer die u met Configuration Manager gebruikt, moet een Chinees besturings systeem worden gebruikt.  

-   Voor elke sitedatabase en elk exemplaar van SQL Server in de hiërarchie moet dezelfde sortering worden gebruikt, en wel een van de volgende:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Deze database sorteringen vormen een uitzonde ring op de vereisten die worden vermeld in [ondersteuning voor SQL Server versies voor Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   U moet een bestand met de naam **GB18030.SMS** in de hoofdmap van het systeemvolume van elke siteservercomputer in de hiërarchie plaatsen. Dit bestand bevat geen gegevens en mag een leeg tekstbestand zijn dat enkel deze naam heeft gekregen om aan dit vereiste te voldoen.  
