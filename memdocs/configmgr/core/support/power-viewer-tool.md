---
title: Power Viewer-hulpprogramma
titleSuffix: Configuration Manager
description: Gebruik het Power Viewer-hulp programma om de status van de functie energie beheer op een Configuration Manager-client weer te geven.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcab26abe2e2a9062eda5ff80ea958010e8a7f62
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723192"
---
# <a name="power-viewer-tool"></a>Power Viewer-hulpprogramma

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het hulp programma Power Viewer is een van de [Configuration Manager-hulpprogram ma's](tools.md). Gebruik het om de status van de functie energie beheer op een Configuration Manager-client weer te geven.

Voer **PowerVwr. exe** uit als Administrator. Wanneer het hulp programma wordt gestart, worden de energie mogelijkheden en energie-instellingen van de lokale computer weer gegeven op het tabblad **energie beheer** . 

De energie beheer gegevens van een externe computer weer geven:  

1. Ga naar het menu **bestand** en klik op **verbinden**. 

2. Voer, indien nodig, de **computer** naam en een **gebruikers naam** en **wacht woord**in. 

Power Viewer bevat drie tabbladen:  

- **Energie configuratie**: de energie mogelijkheden en energie-instellingen van de doel computer weer geven.  

- **Dagelijkse activiteit**: Bekijk de dagelijkse activiteiten grafieken van de client, met inbegrip van de volgende informatie:  

    - **Computer aan**: de energie status van de computer in één dag. De slaap stand wordt gezien als uitschakeling.  

    - **Bewaken op**: in-of uitschakelen status van monitor op één dag.  

    - **Gebruiker actief**: informatie over gebruikers activiteit op één dag.  

- **Energie gebeurtenissen**: alle dagelijkse energie gebeurtenissen weer geven. De client geeft een overzicht van deze gebeurtenissen op 12:00 uur. Met deze samen vatting worden gegevens voor de grafiek met dagelijkse activiteiten gegenereerd.  
