---
title: Takenreeksmedia maken
titleSuffix: Configuration Manager
description: Maak een taken reeks medium om een besturings systeem te implementeren op een doel computer in uw Configuration Manager omgeving.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711026"
---
# <a name="create-task-sequence-media"></a>Takenreeksmedia maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt media gebruiken om een installatie kopie van een besturings systeem vast te leggen vanaf een referentie computer of om een besturings systeem te implementeren op een doel computer in uw Configuration Manager-omgeving. Het kan hierbij gaan om een cd, een dvd-set of een USB-flashstation.  

Media worden meestal gebruikt om besturings systemen te implementeren op doel computers die geen netwerk verbinding hebben of die een verbinding met lage band breedte hebben met uw Configuration Manager-site. U kunt echter ook media gebruiken om een besturingssysteem implementatie buiten een bestaand Windows-besturings systeem te starten. Deze methode is handig als er geen bestaand besturings systeem is, het besturings systeem niet werkt of als u de harde schijf opnieuw wilt partitioneren.  

Implementatiemedia bestaan uit opstartbare media, zelfstandige media en voorbereide media. De inhoud van de media varieert, afhankelijk van het type media dat u gebruikt. Zo bevatten zelfstandige media bijvoorbeeld de taken reeks waarmee het besturings systeem wordt geïmplementeerd. Andere typen media ophalen taken reeksen van het beheer punt.  

> [!IMPORTANT]  
> Als u taken reeks media wilt maken, moet u een beheerder zijn op de computer waarop u de Configuration Manager-console uitvoert. Als u geen beheerder bent, wordt u gevraagd om beheerders referenties wanneer u de wizard taken reeks media maken start.  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a>Vastleg media

Met vastleg media kunt u een installatie kopie van een besturings systeem van een referentie computer vastleggen. Vastleg media bevatten de opstart installatie kopie waarmee de referentie computer wordt gestart en de taken reeks waarmee de installatie kopie van het besturings systeem wordt vastgelegd.

Zie [Capture-media maken](create-capture-media.md)voor meer informatie over het maken van vastleg media.  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a>Opstart bare media

Opstart bare media bevatten de volgende onderdelen:

- De opstart installatie kopie
- Optionele [prestart-opdrachten](../understand/prestart-commands-for-task-sequence-media.md) en de vereiste bestanden
- Configuration Manager binaire bestanden

Wanneer de doel computer wordt gestart, maakt deze verbinding met het netwerk en haalt de taken reeks, de installatie kopie van het besturings systeem en alle andere vereiste inhoud van het netwerk op. Omdat de taken reeks zich niet op de media bevindt, kunt u de taken reeks of de inhoud wijzigen zonder dat u de media opnieuw hoeft te maken.  

> [!IMPORTANT]  
> De pakketten op opstart bare media zijn niet versleuteld. Neem de juiste beveiligings maatregelen, zoals het toevoegen van een wacht woord aan de media, om ervoor te zorgen dat de pakket inhoud beveiligd is tegen onbevoegde gebruikers.  

Voor meer informatie over het maken van opstart bare media [maakt u opstart bare media](create-bootable-media.md).  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a>Voor bereide media

Met voor bereide media kunt u opstart bare media en een installatie kopie van een besturings systeem Toep assen op een harde schijf vóór het inrichtings proces. De voorgefaseerde media zijn een Windows-installatie kopie (WIM)-bestand. De software kan worden geïnstalleerd op een bare-metal computer door de fabrikant of in het faserings centrum dat niet is verbonden met de productie Configuration Manager omgeving.  

Voor bereide media bevatten de opstart installatie kopie die wordt gebruikt voor het starten van de doel computer en de installatie kopie van het besturings systeem die wordt toegepast op de doel computer. U kunt ook toepassingen, pakketten en stuurprogrammapakketten opgeven die moeten worden opgenomen als onderdeel van de voorgefaseerde media. De taken reeks die het besturings systeem implementeert, is niet opgenomen in de media. Wanneer u een taken reeks implementeert die gebruikmaakt van vooraf geplaatste media, controleert de client eerst de lokale taken reeks cache op geldige inhoud. Als de inhoud niet wordt gevonden of is gewijzigd, downloadt de client de inhoud van een distributie punt of peer.  

Voorbereide media worden toegepast op de harde schijf van een nieuwe computer voordat de computer wordt verzonden naar de eindgebruiker. Wanneer de computer voor de eerste keer wordt opgestart nadat u de voor bereide media hebt toegepast, wordt de computer gestart in Windows PE. Er wordt verbinding gemaakt met een beheer punt om de taken reeks te vinden waarmee het implementatie proces van het besturings systeem wordt voltooid.  

> [!IMPORTANT]  
> De pakketten op voor bereide media zijn niet versleuteld. Neem de juiste beveiligings maatregelen, zoals het toevoegen van een wacht woord aan de media, om ervoor te zorgen dat de pakket inhoud beveiligd is tegen onbevoegde gebruikers.  

Zie voor bereide media [maken](create-prestaged-media.md)voor meer informatie over het maken van voor bereide media.  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a>Zelfstandige media

Zelfstandige media bevatten alles wat u nodig hebt om het besturings systeem te implementeren. Deze inhoud bevat de taken reeks en alle overige vereiste inhoud. Omdat alles wat nodig is om het besturings systeem te implementeren, wordt opgeslagen op de zelfstandige media, is de benodigde schijf ruimte voor zelfstandige media groter dan voor andere media typen.  

Zie voor meer informatie over het maken van zelfstandige media [zelfstandige media maken](create-stand-alone-media.md).  


## <a name="considerations-when-using-https"></a>Overwegingen bij het gebruik van HTTPS

Wanneer u uw beheer punten en distributie punten configureert voor het gebruik van HTTPS, maakt u opstart media en voor bereide media op een primaire site, niet op de centrale beheer site. Houd ook rekening met het volgende punt om te bepalen of de media moeten worden geconfigureerd als dynamisch of op de site gebaseerd:  

- Als u de media wilt configureren als dynamische media, moeten alle primaire sites de basis certificerings instantie (CA) hebben van de site van waaruit u de media hebt gemaakt. U kunt de basiscertificeringsinstantie importeren voor alle primaire sites in de hiërarchie.  

- Wanneer primaire sites in uw Configuration Manager-hiërarchie verschillende basis certificerings instanties gebruiken, moet u op elke site op de site gebaseerde media gebruiken.  
