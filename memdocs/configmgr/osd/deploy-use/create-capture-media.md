---
title: Vastelegmedia maken
titleSuffix: Configuration Manager
description: Vastleg media in Configuration Manager gebruiken om een installatie kopie van een besturings systeem van een referentie computer vast te leggen.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d85ab7e9d66c1206c6741117d7b379c998078708
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125369"
---
# <a name="create-capture-media"></a>Vastelegmedia maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met vastleggen media in Configuration Manager kunt u een installatie kopie van een besturings systeem van een referentie computer vastleggen. Vastleg media bevatten de opstart installatie kopie waarmee de referentie computer wordt gestart en de taken reeks waarmee de installatie kopie van het besturings systeem wordt vastgelegd. Gebruik Capture media voor het scenario voor het [maken van een taken reeks om een besturings systeem vast te leggen](create-a-task-sequence-to-capture-an-operating-system.md).  


## <a name="prerequisites"></a>Vereisten

Voordat u vastleg media maakt met behulp van de wizard taken reeks media maken, moet u ervoor zorgen dat aan alle voor waarden wordt voldaan.

### <a name="boot-image"></a>Opstartinstallatiekopie

Houd rekening met de volgende punten over de opstart installatie kopie die u in de taken reeks gebruikt om het besturings systeem te implementeren:

- De architectuur van de opstart installatie kopie moet geschikt zijn voor de architectuur van de doel computer. Op een x64-doelcomputer kan een x86- of x64-opstartinstallatiekopie worden opgestart en uitgevoerd. Op een x86-doelcomputer kan echter alleen een x86-opstartinstallatiekopie worden opgestart en uitgevoerd.
- Zorg ervoor dat de opstart installatie kopie de netwerk-en opslag Stuur Programma's bevat die nodig zijn om de doel computer in te richten.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Alle aan de takenreeks gekoppeld inhoud distribueren

Alle inhoud distribueren die de taken reeks nodig heeft tot ten minste één distributie punt. Deze inhoud bevat de opstart installatie kopie, de installatie kopie van het besturings systeem en andere gekoppelde bestanden. De wizard verzamelt de inhoud van het distributie punt bij het maken van de vastleg media.

Uw gebruikers account moet ten minste **Lees** rechten hebben voor de inhouds bibliotheek op dat distributie punt. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Het verwisselbare USB-station voorbereiden

Als u een verwisselbaar USB-station gebruikt, verbindt u het met de computer waarop u de wizard taken reeks media maken uitvoert. Het USB-station moet detecteerbaar zijn door Windows als een Verwijder apparaat. De wizard schrijft rechtstreeks naar het USB-station wanneer deze het medium maakt.

### <a name="create-an-output-folder"></a>Een uitvoermap maken

Voordat u de wizard taken reeks media maken uitvoert voor het maken van media voor een CD-of DVD-set, moet u een map maken voor de uitvoer bestanden die worden gemaakt. Media die worden gemaakt voor een CD-of DVD-set, worden geschreven als een. ISO-bestand rechtstreeks in de map.


## <a name="process"></a>Proces

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer het knoop punt **taken reeksen** .  

2. Klik op het tabblad **Start** van het lint in de groep **maken** op **taken reeks media maken**. Met deze actie wordt de wizard taken reeks media maken gestart.  

3. Selecteer op de pagina **media type selecteren** de optie **Media vastleggen**.  

4. Geef op de pagina **medium type** op of het medium een **verwisselbaar USB-station** of een **cd/dvd-set**is. Configureer vervolgens de volgende opties:  

    > [!IMPORTANT]  
    > Media maakt gebruik van een FAT32-bestands systeem. U kunt geen media maken op een USB-station waarvan de inhoud een bestand bevat dat groter is dan 4 GB.  

    - Als u **verwisselbaar USB-station**selecteert, selecteert u het station waar u de inhoud wilt opslaan.  

        - **Verwisselbaar USB-station Format teren (FAT32) en maak een opstart bare**: standaard laat Configuration Manager het USB-station voorbereiden. Veel nieuwere UEFI-apparaten vereisen een opstart bare FAT32-partitie. Met deze indeling wordt echter ook de grootte van bestanden en de totale capaciteit van het station beperkt. Als u het Verwissel bare station al hebt geformatteerd en geconfigureerd, schakelt u deze optie uit.

    - Als u **cd/dvd-set**selecteert, geeft u de capaciteit van de media (**Media grootte**) en de naam en het pad op van het uitvoer bestand (**Media bestand**). De wizard schrijft de uitvoerbestanden naar deze locatie. Bijvoorbeeld: `\\servername\folder\outputfile.iso`  

        Als de capaciteit van de media te klein is om de volledige inhoud op te slaan, worden er meerdere bestanden gemaakt. Vervolgens moet u de inhoud op meerdere cd's of Dvd's opslaan. Als er meerdere media bestanden zijn vereist, Configuration Manager een Volg nummer toevoegen aan de naam van elk uitvoer bestand dat wordt gemaakt.  

        > [!IMPORTANT]  
        > Als u een bestaande .iso-afbeelding selecteert, verwijdert de wizard voor het maken van takenreeksmedia die afbeelding uit het station of de share wanneer u doorgaat naar de volgende pagina van de wizard. De bestaande installatiekopie wordt gewist, zelfs als u de wizard annuleert.  

    - **Tijdelijke map**<!--1359388-->: Voor het maken van media kan veel tijdelijke schijf ruimte nodig zijn. Deze locatie is standaard vergelijkbaar met het volgende pad: `%UserProfile%\AppData\Local\Temp` . Vanaf versie 1902, om u meer flexibiliteit te bieden bij het opslaan van deze tijdelijke bestanden, wijzigt u deze waarde in een ander station en pad.  

    - **Media label**<!--1359388-->: Vanaf versie 1902 voegt u een label toe aan de taken reeks media. Dit label helpt u de media beter te identificeren nadat u deze hebt gemaakt. De standaardwaarde is `Configuration Manager`. Dit tekst veld wordt weer gegeven op de volgende locaties:  

        - Als u een ISO-bestand koppelt, geeft Windows dit label weer als de naam van het gekoppelde station  

        - Als u een USB-station formatteert, worden de eerste elf tekens van het label als naam gebruikt  

        - Configuration Manager schrijft een tekst bestand `MediaLabel.txt` met de naam naar de hoofdmap van de media. Het bestand bevat standaard één tekst regel: `label=Configuration Manager` . Als u het label voor media aanpast, gebruikt deze lijn uw aangepaste label in plaats van de standaard waarde.  

    - **Autorun. inf-bestand op media toevoegen**<!-- 4090666 -->: Vanaf versie 1906 wordt Configuration Manager standaard geen autorun. inf-bestand toegevoegd. Dit bestand wordt doorgaans geblokkeerd door antimalware-producten. Zie [een cd-rom-toepassing](https://docs.microsoft.com/windows/desktop/shell/autoplay)voor automatisch aanmelden maken voor meer informatie over de autorun-functie van Windows. Als het scenario nog steeds nodig is, selecteert u deze optie om het bestand op te laten voegen.  

5. Geef op de pagina **opstart installatie kopie** de volgende opties op:  

    > [!IMPORTANT]  
    > De architectuur van de opstart installatie kopie die u distribueert, moet geschikt zijn voor de architectuur van de doel computer. Op een x64-doelcomputer kan een x86- of x64-opstartinstallatiekopie worden opgestart en uitgevoerd. Op een x86-doelcomputer kan echter alleen een x86-opstartinstallatiekopie worden opgestart en uitgevoerd.  

    - **Opstart installatie kopie**: Selecteer de opstart installatie kopie om de doel computer te starten.  

    - **Distributie punt**: Selecteer het distributie punt met de opstart installatie kopie. De wizard haalt de opstartinstallatiekopie op van het distributiepunt en schrijft deze naar de media.  

        > [!NOTE]  
        > Uw gebruikers account heeft mini maal **Lees** machtigingen nodig voor de inhouds bibliotheek op het distributie punt.  

6. Voltooi de wizard.  


## <a name="next-steps"></a>Volgende stappen

[Een takenreeks maken voor het vastleggen van een besturingssysteem](create-a-task-sequence-to-capture-an-operating-system.md)
