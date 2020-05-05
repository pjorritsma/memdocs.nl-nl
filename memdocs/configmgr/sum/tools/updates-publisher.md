---
title: Updates Publisher
titleSuffix: Configuration Manager
description: System Center Updates Publisher gebruiken om aangepaste updates te beheren
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc1e662eb8eca4740e70743d0971e2d65410f3f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717697"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Van toepassing op: System Center Updates Publisher*

System Center Updates Publisher (updates Publisher) is een zelfstandig hulp programma waarmee onafhankelijke software leveranciers of ontwikkel aars van line-of-business-toepassingen aangepaste updates kunnen beheren. Dit beheer van aangepaste updates bevat updates met afhankelijkheden, zoals Stuur Programma's en update bundels.

Met updates Publisher kunt u het volgende doen:

-   Updates importeren uit externe catalogi (niet-micro soft update Catalogs).
-   Wijzig update definities, inclusief toepas baarheid, en implementatie-meta gegevens.
-   Updates exporteren naar externe catalogi.
-   Updates publiceren op een update server.

Nadat u updates naar een update server hebt gepubliceerd, kunt u Configuration Manager gebruiken om deze updates te detecteren en te implementeren op uw beheerde apparaten.

## <a name="workspaces"></a>Workspaces
Wanneer u updates Publisher opent, wordt standaard het knoop punt overzicht van de *werk ruimte updates gebruikt.*

![Updates Publisher-console](media/console1.png)


Updates Publisher heeft vier werk ruimten waarmee het kan worden georganiseerd.


**Werk ruimte updates:** Gebruik deze werk ruimte om software-updates en update bundels te [maken](create-updates-with-updates-publisher.md) en te [beheren](manage-updates-with-updates-publisher.md) . Deze werk ruimte omvat het toewijzen van updates en bundels aan een publicatie, het publiceren en exporteren naar een andere update-opslag plaats voor Publisher.

**Werk ruimte publicaties:** In deze werk ruimte kunt u [publicaties beheren](updates-publisher-publications.md). Een publicatie is een groep updates die u maakt om het exporteren en publiceren van de updates te vereenvoudigen.

Het beheren van publicaties omvat het publiceren van updates op een server, zodat uw clients ze kunnen vinden en installeren, updates en bundels exporteren voor gebruik door andere updates Publisher-installaties of de inhoud van of Details van een publicatie wijzigen.

**Werk ruimte regels:** Hier kunt u [regels voor toepas baarheid beheren](updates-publisher-applicability-rules.md) die kunnen worden opgeslagen en vervolgens worden gebruikt met updates die u implementeert. Er zijn twee soorten regels:

-   Installeer bare regels: deze regels helpen te bepalen of een-client een update moet installeren.
-   Geïnstalleerde regels: deze regels controleren of een update al is geïnstalleerd.

**Catalogus-werk ruimte:** Gebruik deze werk ruimte om [Software-update catalogussen](updates-publisher-catalogs.md)toe te voegen en te beheren. Deze werk ruimte bevat het importeren van software-updates uit deze catalogussen naar de update-opslag plaats van Publisher.

## <a name="whats-new-in-system-center-updates-publisher"></a>Wat is er nieuw in System Center Updates Publisher

>[!NOTE] 
> De nieuwste versie van System Center Updates Publisher is uitgebracht op 6 november 2019. Zie de sectie [release geschiedenis](#release-history) voor meer informatie.

Er is een nieuwe ontwerp modus System Center Updates Publisher om u te helpen bij het ontwerpen van uw updates. Wanneer u de ontwerp modus inschakelt, wordt er een **categorie werk ruimte** toegevoegd aan het Start scherm. Er wordt ook een nieuwe knop **Detectoid** toegevoegd aan de **werk ruimte updates** wanneer de ontwerp modus is ingeschakeld.

### <a name="to-enable-authoring-mode"></a>De ontwerp modus inschakelen

1. Klik in de linkerbovenhoek van de console op het tabblad **updates Publisher** - **Eigenschappen** en kies vervolgens **Opties**.
1. Ga naar de **ontwerp** opties.
1. Schakel het selectie vakje in om de **ontwerp modus in te scha kelen**.

![De ontwerp modus inschakelen voor updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Informatie over de werk ruimte Categorieën

Met de werk ruimte categorieën kunnen auteurs bijwerken de updates die bij elkaar horen, ordenen. Als u bijvoorbeeld een OEM bent, kunt u uw updates indelen op basis van modellen of product lijnen. U kunt meerdere categorieën en onderliggende categorieën definiëren, maar niet de meest onderliggende categorieën, omdat u beperkt bent tot twee niveaus.

![Scherm afbeelding van de werk ruimte Categorieën](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Een update aan een categorie toewijzen

Zodra u uw update hebt gemaakt, kunt u deze toewijzen aan een categorie door de update te selecteren en vervolgens op de knop **categoriseren** te klikken. U kunt ook met de rechter muisknop op de update klikken en **categoriseren**selecteren.

![Scherm opname van het categoriseren van een update](media/scup-categorize-update.png)

### <a name="about-detectoids"></a>Over detectoids

Zodra de ontwerp modus is ingeschakeld, kunt u detectoids maken voor updates. Detectoids zijn handig wanneer u meerdere updates hebt die dezelfde regel (of een set regels) gebruiken om de toepas baarheid te bepalen. In die gevallen maakt u een detectoid en wijst u deze toe als een vereiste voor een update. U kunt meerdere detectoids toewijzen aan een geschreven update.


### <a name="create-a-detectoid"></a>Een detectoid maken

1. Open de **werk ruimte updates**.
1. Klik op het lint op de knop **Detectoid** .
1. Volg de aanwijzingen in de wizard om uw detectoid te maken.



![Vereisten voor het bijwerken met behulp van een detectoid](media/scup-detectoid-as-prerequisite.png)

## <a name="release-history"></a>Release geschiedenis

- [2019 RTW-versie 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Uitgebracht: november, 6, 2019
- [Update Rollup versie 6.0.283.0 van KB4462765](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Uitgebracht: 7 september 2018.
- [2017 RTW-versie 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Uitgebracht op 26 maart 2018.


## <a name="next-steps"></a>Volgende stappen
Als u aan de slag wilt gaan, moet u eerst [installeren](install-updates-publisher.md)en vervolgens [opties configureren](updates-publisher-options.md) voor updates Publisher.
