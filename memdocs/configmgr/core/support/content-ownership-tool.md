---
title: Hulpprogramma voor eigendom van inhoud
titleSuffix: Configuration Manager
description: Gebruik het hulp programma voor inhouds eigendom om het eigendom van zwevende pakketten in Configuration Manager te wijzigen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee1a24a93bb71178af3a4cfbba2a406bdd958d19
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723388"
---
# <a name="content-ownership-tool"></a>Hulpprogramma voor eigendom van inhoud

*Van toepassing op: Configuration Manager (huidige vertakking)*

Hulp programma voor inhouds eigendom is een van de [Configuration Manager-hulpprogram ma's](tools.md). Het wijzigt het eigendom van zwevende pakketten in Configuration Manager. Zwevende pakketten hebben geen eigenaar van de site server. Pakketten kunnen zwevend worden door de site server te verwijderen terwijl ze nog steeds het eigendom zijn van deze site server.

Voer het hulp programma voor inhouds eigendom uit op een site server in de hiërarchie van Configuration Manager. Meld u aan als een gebruiker met beheerders rechten met voldoende pakket machtigingen.  

> [!Tip]  
> Gebruik **ContentLibraryCleanup. exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` om zwevende inhoud te *verwijderen* van een distributie punt. Zie [hulp programma voor opruimen van inhouds bibliotheken](../plan-design/hierarchy/content-library-cleanup-tool.md)voor meer informatie.  



## <a name="features"></a>Functies

- Alle zwevende pakketten weer geven  

- Alle pakketten weer geven, zelfs als ze niet zwevend zijn  

- De status van de verbinding met een site weer geven  

- Pakketten filteren op naam, site code of pakket type  

- Sorteren op elke weer gegeven kolom  

- Toewijzing van een of meer pakketten met één actie wijzigen  

- De voortgang van de overdrachts activiteit van de eigenaar weer geven  



## <a name="usage"></a>Gebruik

Voer **ContentOwnershipTool. exe** uit om het hulp programma te starten. Lokale beheerders machtigingen op de computer zijn niet vereist om het hulp programma uit te voeren.

Er zijn geen opdracht regel parameters.

> [!Important]   
> Dit hulp programma wijzigt het eigendom van een zwevend pakket. Het pakket zelf wordt niet verplaatst van het distributie punt waarop het is opgeslagen. Door deze wijziging van de eigendom wordt het pakket niet bijgewerkt op distributie punten. Ook kunnen clients het beleid voor de implementatie van het pakket niet opnieuw evalueren. Nadat het eigendom is gewijzigd, controleert u of de nieuwe site server toegang heeft tot de bron bestanden. Het moet mini maal **Lees** machtigingen hebben voor de bron bestanden van elk pakket. 



## <a name="see-also"></a>Zie ook

- [Basisconcepten voor inhoudsbeheer](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [De inhoudsbibliotheek](../plan-design/hierarchy/the-content-library.md)
