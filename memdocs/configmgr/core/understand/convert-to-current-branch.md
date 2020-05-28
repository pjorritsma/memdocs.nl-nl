---
title: De LTSB upgraden naar de huidige branch
titleSuffix: Configuration Manager
description: Meer informatie over hoe u een LTSB-site (Long-term Servicing Branch) converteert naar een huidige branch-site.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722954"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>De Long-term Servicing Branch upgraden naar de huidige vertakking

*Van toepassing op: System Center Configuration Manager (onderhouds branche voor de lange termijn)*

Gebruik dit onderwerp voor meer informatie over het upgraden (converteren) van een-site en-hiërarchie die de Long-term Servicing Branch (LTSB) van Configuration Manager naar de Current Branch uitvoert.

Wanneer u een huidige Software Assurance-overeenkomst (of vergelijk bare licentie rechten) hebt die u de rechten verleent om de Current Branch te gebruiken, kunt u de installatie van de LTSB naar de Current Branch converteren.  Dit is een eenrichtings conversie, omdat er geen ondersteuning is voor het converteren van een Current Branch-site naar de LTSB.

Als u meerdere sites hebt, hoeft u alleen de site op het hoogste niveau van uw hiërarchie te converteren. Nadat de site op het hoogste niveau is geconverteerd:
- Onderliggende primaire sites worden automatisch geconverteerd.
- U moet secundaire sites hand matig bijwerken vanuit de Configuration Manager-console.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Voer Setup uit om de Long-term Servicing branch te converteren
Op de site op het hoogste niveau van uw hiërarchie kunt u Configuration Manager Setup uitvoeren vanuit de in aanmerking komende basislijn media en **site onderhoud**selecteren.  Selecteer vervolgens de optie voor de Current Branch en voltooi de wizard op de pagina licentie verlening.

Wanneer uw site is geconverteerd naar de Current Branch, zijn er eerder niet-beschik bare functies en mogelijkheden beschikbaar voor gebruik.

> [!NOTE]  
> Het kwalificeren van een basislijn media is een medium met een versie die gelijk is aan of hoger is dan uw LTSB-installatie.

Omdat de LTSB bijvoorbeeld is gebaseerd op versie 1606, kunt u de basis-1511-media niet gebruiken om te converteren naar de Current Branch. In plaats daarvan voert u Setup uit vanaf dezelfde versie van 1606 Baseline media die u hebt gebruikt voor het installeren van de LTSB-site en kiest u de optie voor licentie verlening voor de Current Branch.  Als er een latere basis lijn van de Current Branch is uitgebracht, kunt u het installatie programma uitvoeren vanaf die basislijn media.

Voor een lijst met basislijn versies raadpleegt u **basis lijn-en update versies** in [updates voor Configuration Manager](../servers/manage/updates.md).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>De Configuration Manager-console gebruiken om de Long-term Servicing branch te converteren
Als uw site de LTSB uitvoert, kunt u de volgende optie in de console Configuration Manager gebruiken om te converteren naar de Current Branch:

 1. Ga in de-console naar **beheer**  >  **site configuratie**  >  **sites**en open vervolgens **hiërarchie-instellingen**.  

 2. Ga **in hiërarchie-instellingen**naar het tabblad **licenties** . Selecteer de optie die u wilt **converteren naar current branch**en kies vervolgens **Toep assen**.  

Wanneer uw site is geconverteerd naar de Current Branch, zijn er eerder niet-beschik bare functies en mogelijkheden beschikbaar voor gebruik.
