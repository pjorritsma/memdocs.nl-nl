---
title: Aangepaste locaties voor database bestanden
titleSuffix: Configuration Manager
description: Meer informatie over het opgeven van aangepaste locaties voor SQL Server database bestanden.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff992361959fcaad51acf3b78f5618e95f5af9e0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692601"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Aangepaste locaties voor Configuration Manager site database bestanden

*Van toepassing op: Configuration Manager (huidige vertakking)*

 Configuration Manager ondersteunt aangepaste locaties voor SQL Server database bestanden.  

> [!NOTE]  
>  De optie voor het opgeven van niet-standaard bestands locaties is niet beschikbaar wanneer u een SQL Server cluster gebruikt.  

 **Tijdens de installatie** van een nieuwe primaire site of centrale beheer site kunt u het volgende doen:  

-   **Niet-standaard bestands locaties opgeven voor de site database: bij**de installatie van Configuration Manager wordt vervolgens de site database gemaakt op basis van deze locaties.  

-   **Geef het gebruik van een vooraf gemaakte SQL Server Data Base op die gebruikmaakt van aangepaste bestands locaties**: Configuration Manager Setup gebruikt vervolgens die vooraf gemaakte data base en de vooraf geconfigureerde bestands locaties.  

**Na de installatie**kunt u de locatie van de database bestanden van de site wijzigen. Hiervoor moet u de site stoppen en de bestands locatie in SQL Server bewerken:  

-   Stop de **SMS_Executive** -service op de site server van Configuration Manager.  

-   Zie [data bases van gebruikers verplaatsen](/sql/relational-databases/databases/move-user-databases?view=sql-server-2014)voor meer informatie over het verplaatsen van een gebruikers database.  

-   Nadat u de verplaatsing van het database bestand hebt voltooid, start u de **SMS_Executive** -service opnieuw op de Configuration Manager site server.