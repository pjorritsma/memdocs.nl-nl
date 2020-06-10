---
title: Community-hub en GitHub
titleSuffix: Configuration Manager
description: Community hub inschakelen en gebruiken in Configuration Manager
ms.date: 06/02/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d3dd8f8af7a3add38d8003da12078d393041631d
ms.sourcegitcommit: 5e339c07001e911cf75ef922e6c66a7efdeab6f1
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/10/2020
ms.locfileid: "84637728"
---
# <a name="community-hub-and-github"></a>Community-hub en GitHub
<!--3555935, 3555936-->

De IT-beheerder heeft een schat aan kennis ontwikkeld over de jaren. In plaats van items zoals scripts en rapporten helemaal opnieuw te hoeven maken, hebben we een **Configuration Manager Community-hub** gebouwd waar IT-beheerders met elkaar kunnen delen. Door gebruik te maken van anderen, kunt u uren werk besparen. De Community hub bevordert creativiteit door anderen aan het werk te bouwen en anderen te laten bouwen. GitHub heeft al branchespecifieke processen en hulpprogram ma's die zijn ontworpen voor delen. De Community-hub maakt nu gebruik van deze hulpprogram ma's rechtstreeks in de Configuration Manager-console als basis onderdelen voor het aansturen van deze nieuwe community. Voor de eerste release wordt de inhoud die beschikbaar is in de Community hub alleen geüpload door micro soft. De IT-beheerder kan in de toekomst inhoud uploaden met behulp van hun eigen GitHub-account.

> [!Note]  
> Community hub is een optioneel Cloud onderdeel. Het is voor het eerst geïntroduceerd in juni 2020. Zie [optionele functies](install-in-console-updates.md#bkmk_options)voor meer informatie over het kiezen van een Community-hub.

## <a name="about-community-hub"></a>Over Community hub

Community hub ondersteunt de volgende objecten:
- PowerShell-scripts
- Rapporten
- Takenreeksen
- Toepassingen
- Configuratie-items  

## <a name="prerequisites"></a>Vereisten

- Op het apparaat waarop de Configuration Manager-console wordt uitgevoerd voor toegang tot de hub, zijn de volgende items nodig:
   - Windows 10 build 17110 of hoger
   - .NET Framework versie 4,6 of hoger


- Als u rapporten wilt downloaden, moet u de optie **Configuration Manager gegenereerde certificaten gebruiken voor HTTP-site systemen** op de site die u in importeert. Zie [Enhanced http](/sccm/core/plan-design/hierarchy/enhanced-http)(Engelstalig) voor meer informatie.
   1. Ga naar **beheer**  >  **site configuratie**  >  **sites**.
   1. Selecteer de site en kies **Eigenschappen** in het lint.
   1. Selecteer op het tabblad **communicatie beveiliging** de optie voor het **gebruik van door Configuration Manager gegenereerde certificaten voor http-site systemen**.

## <a name="permissions"></a>Machtigingen

- Een script importeren: machtiging **maken** voor **SMS_Scripts** klasse.
- Een rapport importeren: volledige beheerder beveiligingsrol.


## <a name="use-the-community-hub"></a>De Community-hub gebruiken

1. Ga naar het knoop punt **Community-hub** in de werk ruimte **Community** .
1. Selecteer een item om te downloaden.
1. U hebt de juiste machtigingen op uw Configuration Manager-site nodig om objecten van de hub te downloaden en te importeren in de-site.
    - Een script importeren: machtiging **maken** voor SMS_Scripts klasse.
    - Een rapport importeren: volledige beheerder beveiligingsrol.
1. Gedownloade rapporten worden geïmplementeerd naar een rapportmap met de naam **hub** op het Reporting Services-punt. Gedownloade scripts kunnen worden weer gegeven in het knoop punt **Run scripts** .
1. Bekijk alle items die zijn gedownload van de hub door uw organisatie door te klikken op **uw down loads** in het knoop punt **Community hub** .

[![Alle items die zijn gedownload van de Community-hub](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="next-steps"></a>Volgende stappen

Meer informatie over het maken en gebruiken van de volgende objecten:

- [PowerShell-scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md)
- [Inleiding op rapportage](introduction-to-reporting.md)
- [Taken reeksen maken en beheren](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Een toepassing maken en implementeren](../../../apps/get-started/create-and-deploy-an-application.md)
- [Configuratie-items maken](../../../compliance/deploy-use/create-configuration-items.md)