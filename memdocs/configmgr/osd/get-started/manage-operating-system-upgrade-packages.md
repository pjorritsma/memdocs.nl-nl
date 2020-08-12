---
title: Upgradepakketten voor besturingssysteem beheren
titleSuffix: Configuration Manager
description: Meer informatie over het beheren van upgrade pakketten voor besturings systemen in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a50592815ed4581c01489f90b6c3701e53bb4981
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124411"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Upgrade pakketten van het besturings systeem beheren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Een upgrade pakket voor het besturings systeem in Configuration Manager bevat de bron bestanden van de Windows-installatie om een bestaand besturings systeem op een computer bij te werken. In dit artikel wordt beschreven hoe u een upgrade pakket voor het besturings systeem kunt toevoegen, distribueren en onderhouden.

> [!NOTE]
> Upgrade pakketten voor het besturings systeem kunnen ook worden gebruikt voor nieuwe installaties van Windows. Het is echter afhankelijk van Stuur Programma's die compatibel zijn met deze methode. Bij het uitvoeren van nieuwe installaties van Windows vanuit een upgrade pakket voor het besturings systeem, worden Stuur Programma's geïnstalleerd in Windows PE en alleen worden ingevoegd in Windows PE. Sommige Stuur Programma's zijn niet compatibel met geïnstalleerd tijdens de installatie van Windows PE. Als Stuur Programma's niet compatibel zijn met de installatie van in Windows PE, gebruikt u in plaats daarvan een [installatie kopie van een besturings systeem](manage-operating-system-images.md), zoals **install. Wim**.

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a>Een upgrade pakket voor het besturings systeem toevoegen  

Voordat u een upgrade pakket voor het besturings systeem kunt gebruiken, moet u het eerst toevoegen aan uw Configuration Manager-site.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **upgrade pakketten van het besturings systeem** .  

2. Klik op het tabblad **Start** van het lint in de groep **maken** op **upgrade pakket besturings systeem toevoegen**. Met deze actie wordt de wizard upgrade van besturings systeem toevoegen gestart.  

3. Geef op de pagina **gegevens bron** de volgende instellingen op:

    - Het netwerkpad **naar de** installatie bron bestanden van het upgrade pakket voor het besturings systeem. Bijvoorbeeld `\\server\share\path`.  

        > [!NOTE]  
        >  De bron bestanden van de installatie bevatten setup.exe en andere bestanden en mappen om het besturings systeem te installeren.  

        > [!IMPORTANT]  
        >  Beperk de toegang tot deze installatie bron bestanden om ongewenste manipulatie te voor komen.  

    - **Extraheer een specifieke installatie kopie-index uit het bestand install. Wim van het geselecteerde upgrade pakket** en selecteer vervolgens een installatie kopie-index in de lijst.<!--4931110--> Vanaf versie 1910 wordt met deze optie automatisch één index geïmporteerd in plaats van alle afbeeldings indexen in het bestand. Als u deze optie gebruikt, resulteert dit in een kleiner afbeeldings bestand en snellere offline onderhoud. Het ondersteunt ook het proces voor het [optimaliseren van installatie kopieën](#bkmk_resetbase)voor een kleiner installatie kopie bestand na het Toep assen van software-updates.  

        > [!IMPORTANT]  
        > Configuration Manager overschrijft de bestaande install. Wim in het upgrade pakket van het besturings systeem. De afbeeldings index wordt naar een tijdelijke locatie geëxtraheerd en vervolgens verplaatst naar de oorspronkelijke bronmap. Voordat u een upgrade pakket voor het besturings systeem importeert en deze optie inschakelt, moet u een back-up maken van de oorspronkelijke bron bestanden.

    - Als u inhoud vooraf in de cache wilt opslaan op een client, geeft u de **architectuur** en **taal** van de installatie kopie op. Zie [inhoud vooraf in cache configureren](../deploy-use/configure-precache-content.md)voor meer informatie.  

4. Geef op de pagina **Algemeen** de volgende informatie op. Deze informatie is nuttig voor identificatie doeleinden wanneer u meer dan één upgrade pakket voor het besturings systeem hebt.  

    - **Naam**: een unieke naam voor het upgrade pakket van het besturings systeem.  

    - **Versie**: een optionele versie-id. Deze eigenschap hoeft niet de versie van het besturings systeem van het upgrade pakket te zijn. Het is vaak de versie van uw organisatie voor het pakket.  

    - **Opmerking**: een optionele korte beschrijving.  

5. Voltooi de wizard.  

Distribueer vervolgens het upgrade pakket van het besturings systeem naar distributie punten.  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a>Inhoud naar een distributie punt distribueren  

OS-upgrade pakketten naar distributie punten distribueren hetzelfde als andere inhoud. Voordat u de taken reeks implementeert, distribueert u het upgrade pakket van het besturings systeem naar ten minste één distributie punt. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>Volgende stappen

[Een takenreeks maken voor het bijwerken van een besturingssysteem](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
