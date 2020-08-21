---
title: De site database plannen
titleSuffix: Configuration Manager
description: Houd rekening met de site database en de server functie van de site database bij het plannen van uw Configuration Manager-hiërarchie.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 068511c5b3b0c15eb355c484b241a76d9dd512e2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700177"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>De site database voor Configuration Manager plannen

*Van toepassing op: Configuration Manager (huidige vertakking)*

De site database server is een computer waarop een ondersteunde versie van Microsoft SQL Server wordt uitgevoerd. SQL Server wordt gebruikt om informatie op te slaan voor Configuration Manager-sites. Elke site in een Configuration Manager-hiërarchie bevat een site database en een server waaraan de server functie site database is toegewezen.  

-   Voor centrale beheer sites en primaire sites kunt u SQL Server op de site server installeren of u kunt SQL Server op een andere computer dan de site server installeren.  

-   Voor secundaire sites kunt u SQL Server Express gebruiken in plaats van een volledige SQL Server installatie. De database server moet echter op de secundaire site server worden uitgevoerd.  

-  Voor gebruik van de SQL-beschikbaarheids groep moet het database herstel model zijn ingesteld op volledig  

-  Voor gebruik van niet-SQL-beschikbaarheids groep moet het database herstel model zijn ingesteld op eenvoudig  

Meer informatie over SQL-herstel modi vindt u in [herstel modellen (SQL Server)](/sql/relational-databases/backup-restore/recovery-models-sql-server).

De volgende SQL Server-configuraties kunnen worden gebruikt om de sitedatabase te hosten:  

-   Het standaardexemplaar van SQL Server  

-   Een benoemd exemplaar op één computer met SQL Server  

-   Een benoemd exemplaar op een geclusterd exemplaar van SQL Server  

-   Een SQL Server AlwaysOn-beschikbaarheids groep (vanaf versie 1602 van Configuration Manager)


Als u de site database wilt hosten, moet de SQL Server voldoen aan de vereisten die worden beschreven in [ondersteuning voor SQL Server-versies voor Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



## <a name="remote-database-server-location-considerations"></a>Overwegingen voor locatie van externe database server  

Als u een externe database server computer gebruikt, moet u ervoor zorgen dat de tussenliggende netwerk verbinding een netwerk verbinding met een hoge Beschik baarheid en hoge band breedte is. De site server en sommige site systeem rollen moeten voortdurend communiceren met de externe server die als host fungeert voor de site database.

-   De hoeveelheid band breedte die is vereist voor de communicatie met de database server is afhankelijk van een combi natie van veel verschillende site-en client configuraties. De werkelijke band breedte die vereist is, kan daarom niet voldoende worden voor speld.  

-   Elke computer die de SMS Provider uitvoert en een verbinding maakt met de sitedatabase verhoogt de vereisten met betrekking tot de netwerkbandbreedte.  

-   De computer met SQL Server moet zich in een domein bevinden dat een twee richtings vertrouwensrelatie heeft met de site server en alle computers waarop de SMS-provider wordt uitgevoerd.  

-   U kunt geen geclusterde SQL Server gebruiken voor de sitedatabaseserver wanneer de sitedatabase zich op dezelfde locatie als de siteserver bevindt.  


Normaal gesp roken ondersteunt een site systeem Server site systeem rollen van slechts één Configuration Manager-site. U kunt echter verschillende exemplaren van SQL Server gebruiken op geclusterde of niet-geclusterde servers waarop SQL Server wordt uitgevoerd om een Data Base van verschillende Configuration Manager-sites te hosten. Om databases voor verschillende sites te ondersteunen, moet u elk exemplaar van SQL Server configureren om unieke poorten voor communicatie te gebruiken.