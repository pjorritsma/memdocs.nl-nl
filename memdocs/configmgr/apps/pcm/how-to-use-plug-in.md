---
title: De conversie-invoeg toepassing gebruiken
titleSuffix: Configuration Manager
description: Gebruik de package Conversion Manager-invoeg toepassing om de analyse-en conversie processen aan te passen.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 4ca16ade5f8581cb124df39294c3cfc27627a346
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709878"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>De package Conversion Manager-invoeg toepassing gebruiken

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1357861-->

De package Conversion Manager-invoeg toepassing helpt u bij het aanpassen van de analyse-en conversie processen. Als u de package Conversion Manager-invoeg toepassing wilt gebruiken, schrijft u een uitvoerbaar bestand of script dat aangepaste bewerkingen uitvoert. Bewerk vervolgens het configuratie bestand micro soft. ConfigurationManagement. exe. config om het uitvoer bare bestand of script aan te roepen. De meest voorkomende talen voor het schrijven van het script zijn VBScript of Power shell.

De package Conversion Manager-invoeg toepassing wordt één keer uitgevoerd voor elk pakket. Als u meerdere pakketten tegelijk analyseert of converteert, wordt de package Conversion Manager-invoeg toepassing elke keer uitgevoerd.

> [!NOTE]  
> Zie voor meer informatie over de package Conversion Manager-elementen in het Configuration Manager configuratie bestand [technische documentatie voor de invoeg toepassing pakket conversie beheer van de configuratie-XML](plugin-config-xml.md).



## <a name="default-process"></a>Standaard proces

Pakket conversie beheer voert standaard de volgende acties uit:

1.  Een Configuration Manager-pakket lezen.  

2.  Maak een toepassing op basis van het pakket en voeg standaard kenmerken toe.  

3.  Analyseer de toepassing en bepaal de gereedheids status van het pakket.  

4.  Voer een van de volgende acties uit, afhankelijk van de beheer bewerking voor pakket conversie:  

    - **Analyseren**: Geef de gereedheids status van het pakket weer in de Configuration Manager-console.  

    - **Converteren**: Schrijf de toepassing naar de Configuration Manager-Data Base.  


## <a name="plug-in-based-process"></a>Proces op basis van een invoeg toepassing 

Wanneer u de invoeg toepassing gebruikt, voert pakket conversie beheer de volgende acties uit:

1.  Een Configuration Manager-pakket lezen.  

2.  Maak een toepassing op basis van het pakket en voeg standaard kenmerken toe.  

3.  Converteer de toepassing naar XML. Sla het bestand vervolgens op schijf op.  

4.  Voer het invoeg script uit om de toepassings-XML te wijzigen. Zie [technische documentatie voor de invoeg toepassing configuratie-XML van package Conversion Manager](plugin-config-xml.md)voor meer informatie.  

5.  Converteer de XML van de toepassing naar een Configuration Manager-toepassing.  

6.  Analyseer de toepassing en bepaal de gereedheids status van het pakket.  

7.  Voer een van de volgende acties uit, afhankelijk van de beheer bewerking voor pakket conversie:  

    - **Analyseren**: Geef de gereedheids status van het pakket weer in de Configuration Manager-console.  

    - **Converteren**: Schrijf de toepassing naar Configuration Manager Data Base.  



## <a name="see-also"></a>Zie ook

[Technische documentatie voor de invoeg toepassing configuratie-XML van package Conversion Manager](plugin-config-xml.md)
