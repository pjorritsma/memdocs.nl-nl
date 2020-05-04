---
title: Pakketten analyseren en converteren
titleSuffix: Configuration Manager
description: Meer informatie over het analyseren en converteren van pakketten met package Conversion Manager in Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f72e7330909bc5653e69790e38ae043e539cc239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709934"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Pakketten analyseren en converteren met pakket conversie beheer

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1357861-->

Voordat u een pakket kunt converteren, moet u het eerst analyseren. Afhankelijk van de resultaten van de analyse, kunt u een van de volgende taken uitvoeren:

- **Converteer** het pakket naar een toepassing. De gereedheids status wordt **automatisch**weer gegeven in de **pakket** lijst in de-console.  

- **Herstel en converteer** het pakket, voeg verzamelingen toe en maak globale voor waarden. De gereedheids status wordt **automatisch**weer gegeven in de **pakket** lijst in de-console.  

- **Herstel en converteer** het pakket. In de **pakket** lijst in de-console wordt de gereedheids status weer gegeven als **hand matig**.  

- Het pakket niet-geconverteerd laten. De gereedheids status wordt **niet van toepassing**op de **pakket** lijst in de-console.  



## <a name="how-to-analyze-packages"></a><a name="bkmk_analyze"></a>Pakketten analyseren

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **toepassings beheer**uit en selecteer het knoop punt **pakketten** .  

2. Selecteer het pakket dat u wilt converteren. Selecteer op het tabblad **Start** van het lint in de groep **pakket conversie** het **pakket analyseren**. Pakket conversie beheer analyseert het pakket.  

3. Als u de gereedheids status van het pakket wilt zien, voegt u de kolom **gereedheids** toe aan de lijst met pakketten. De gereedheids status van het pakket bepaalt uw volgende actie:  

    - **Automatisch**: [pakketten converteren](#bkmk_convert)  

        Zie [pakketten herstellen en converteren](#bkmk_fix)om ook verzamelingen te koppelen en globale voor waarden te maken met een **automatische** gereedheids status.  

    - **Hand matig**: [pakketten herstellen en converteren](#bkmk_fix)

    - **Niet van toepassing**: in dit pakket ontbreekt de vereiste inhoud of een programma. Voeg ontbrekende inhoud of Program ma's toe en probeer de analyse opnieuw uit te voeren. Of zorg ervoor dat de status niet is geconverteerd en ga door met het implementeren van een pakket.  

    - **Onbekend**: Voer eerst de taak **analyseren** uit of wacht op de volgende geplande analyse. Zie [problemen met pakket conversie beheer oplossen](troubleshoot-pcm.md)als de status niet verandert.<!-- SCCMDocs#2044 -->

## <a name="how-to-convert-packages"></a><a name="bkmk_convert"></a>Pakketten converteren

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **toepassings beheer**uit en selecteer het knoop punt **pakketten** .  

2. Selecteer het pakket dat u wilt converteren met de gereedheids status **automatisch**. Op het tabblad **Start** van het lint selecteert u **pakket converteren**in de groep **pakket conversie** . De wizard pakket converteren naar toepassing wordt geopend.  

3. Controleer in de wizard pakket converteren naar toepassing de lijst met geselecteerde pakketten. Verwijder de pakketten die u niet wilt converteren en selecteer **OK**. Pakket conversie beheer converteert het pakket. In het venster conversie voltooid wordt de conversie status van de nieuwe toepassingen vermeld.  

    > [!Note]  
    > Wanneer u een pakket converteert, registreert de site de datum en tijd van de conversie als UTC-tijd.  

4. Volg de instructies in het venster. Selecteer **toepassingen weer geven** of **sluiten**.  



## <a name="how-to-fix-and-convert-packages"></a><a name="bkmk_fix"></a>Pakketten herstellen en converteren

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **toepassings beheer**uit en selecteer het knoop punt **pakketten** .  

2. Selecteer een pakket met de gereedheids status **hand matig** of **automatisch**. Klik op het tabblad **Start** van het lint in de groep **pakket conversie** op **herstellen en converteren**.  

3. Controleer de informatie op de pagina **pakket selectie** in de wizard pakket conversie en los de items op **die u wilt herstellen**. Selecteer **volgende**.  

4. Controleer op de pagina **afhankelijkheids controle** of het pakket afhankelijk is van andere pakketten in de lijst en selecteer **volgende**.  

    > [!Note]  
    > Als u een van de vermelde afhankelijke pakketten niet hebt geconverteerd, moet u deze pakketten eerst converteren. Start vervolgens het pakket conversie proces opnieuw.  
    >  
    > Als een afhankelijkheid niet vereist is, verwijdert u deze of negeert u deze en gaat u verder met het conversie proces.  

5. Controleer op de pagina **implementatie type** de implementatie typen voor de nieuwe toepassing. Wijzig hun prioriteiten of verwijder de implementatie typen.  

6. Als een van de nieuwe implementatie typen geen bijbehorende detectie methode heeft, wordt in de kolom **detectie methode** een waarschuwings pictogram weer gegeven. Voer de volgende acties uit:  

    1. Selecteer **detectie methode bewerken**.  

    2. Selecteer **Toevoegen**.  

    3. Geef in het dialoog venster detectie regel een **instellings type**op.  

    4. Geef voor het opgegeven instellings type de aanvullende informatie op die vereist is voor de detectie regel.  

    5. Selecteer **OK**. Herhaal dit proces zo nodig om meerdere detectie methoden toe te voegen aan elk implementatie type.  

    6. Selecteer **OK**. Controleer of in de kolom **detectie methode** een pictogram wordt weer gegeven om een correct opgegeven detectie methode te bevestigen.  

7. Selecteer **Volgende**.  

8. Controleer op de pagina **vereisten selecteren** de implementatie typen van de nieuwe toepassing. Selecteer een implementatie type en controleer de vereisten voor het implementatie type.  

    > [!Note]  
    > De wizard geeft alleen de vereisten weer die door package Conversion Manager worden geconverteerd. Alle WQL-query's in verzamelingen worden niet geconverteerd naar vereisten.  

9. Voeg indien nodig vereisten toe voor een geselecteerd implementatie type.  

10. Selecteer **Volgende**.  

11. Voltooi de wizard om de toepassing te maken.  

    > [!Note]  
    > Wanneer u een pakket converteert, registreert de site de datum en tijd van de conversie als UTC-tijd.  



## <a name="monitor"></a><a name="bkmk_monitor"></a>Monitoren

Ga naar de werk ruimte **bewaking** van de Configuration Manager-console en selecteer **pakket conversie status**. Dit dash board toont de algemene analyse-en conversie status van de pakketten op de site. Met een nieuwe achtergrond taak worden automatisch de analyse gegevens samenvatten.

> [!Tip]  
> Pakket conversie beheer dat is geïntegreerd met Configuration Manager vereist niet dat u de analyse van pakketten plant. Deze actie wordt verwerkt door de taak Integrated samenvatting.

![Scherm afbeelding van voor beeld van pakket conversie status dashboard](media/1357861-pcm-dashboard.png)
