---
title: Takenreeksmedia maken
titleSuffix: Configuration Manager
description: Maak een taken reeks medium om een besturings systeem te implementeren op een doel computer in uw Configuration Manager omgeving.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf7ce32ed9e126b5526c68b7da03cf44d9b5062d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125165"
---
# <a name="create-task-sequence-media"></a>Takenreeksmedia maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt media gebruiken om een installatie kopie van een besturings systeem vast te leggen vanaf een referentie computer of om een besturings systeem te implementeren op een doel computer in uw Configuration Manager-omgeving. Het kan hierbij gaan om een cd, een dvd-set of een USB-flashstation.

Media worden voornamelijk gebruikt voor het implementeren van een besturings systeem op computers die geen netwerk verbinding hebben of die een verbinding met lage band breedte met de site hebben. U kunt echter ook media gebruiken om een besturingssysteem implementatie buiten een bestaand Windows-besturings systeem te starten. Deze methode is handig wanneer er geen besturings systeem is, het besturings systeem niet werkt of als u de schijf opnieuw wilt partitioneren.

Implementatie media omvatten opstart bare media, zelfstandige media en voor bereide media. De inhoud van de media varieert, afhankelijk van het type media dat u gebruikt. Zo bevatten zelfstandige media bijvoorbeeld de taken reeks waarmee het besturings systeem wordt geïmplementeerd. Andere typen media ophalen taken reeksen van het beheer punt.

> [!IMPORTANT]
> Als u taken reeks media wilt maken, moet u een beheerder zijn op de computer waarop u de Configuration Manager-console uitvoert. Als u geen beheerder bent, wordt u gevraagd om beheerders referenties wanneer u de wizard taken reeks media maken start.

## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a>Vastleg media

Met vastleg media kunt u een installatie kopie van een besturings systeem van een referentie computer vastleggen. Vastleg media bevatten de opstart installatie kopie waarmee de referentie computer wordt gestart en de taken reeks waarmee de installatie kopie van het besturings systeem wordt vastgelegd.

## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a>Opstart bare media

Opstart bare media bevatten de volgende onderdelen:

- De opstart installatie kopie
- Optionele [prestart-opdrachten](../understand/prestart-commands-for-task-sequence-media.md) en de vereiste bestanden
- Configuration Manager binaire bestanden

Wanneer de doel computer wordt gestart, maakt deze verbinding met het netwerk en haalt de taken reeks, de installatie kopie van het besturings systeem en alle andere vereiste inhoud van het netwerk op. Omdat de taken reeks zich niet op de media bevindt, kunt u de taken reeks of de inhoud wijzigen zonder dat u de media opnieuw hoeft te maken.  

> [!IMPORTANT]  
> De pakketten op opstart bare media zijn niet versleuteld. Neem de juiste beveiligings maatregelen, zoals het toevoegen van een wacht woord aan de media, om ervoor te zorgen dat de pakket inhoud beveiligd is tegen onbevoegde gebruikers.  

Vanaf versie 2006 kunnen opstart bare media op basis van de Cloud inhoud downloaden. Het apparaat heeft nog steeds een intranet verbinding met het beheer punt nodig. Dit kan inhoud ophalen van een CMG (Cloud Management Gateway) of een Cloud distributiepunt.<!--6209223--> Zie [ondersteuning voor Cloud inhoud](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content)voor meer informatie.

## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a>Voor bereide media

Met voor bereide media kunt u opstart bare media en een installatie kopie van een besturings systeem Toep assen op een harde schijf vóór het inrichtings proces. De voorgefaseerde media zijn een Windows-installatie kopie (WIM)-bestand. De fabrikant kan deze tijdens hun bouw proces installeren op de bare-metal computer. U kunt deze ook gebruiken in een faserings centrum dat niet is verbonden met de productie Configuration Manager omgeving.

Voor bereide media bevatten de opstart installatie kopie die wordt gebruikt voor het starten van de doel computer en de installatie kopie van het besturings systeem die wordt toegepast op de doel computer. U kunt ook toepassingen, pakketten en stuurprogrammapakketten opgeven die moeten worden opgenomen als onderdeel van de voorgefaseerde media. De taken reeks die het besturings systeem implementeert, is niet opgenomen in de media. Wanneer u een taken reeks implementeert die gebruikmaakt van vooraf geplaatste media, controleert de client eerst de lokale taken reeks cache op geldige inhoud. Als de inhoud niet wordt gevonden of is gewijzigd, downloadt de client de inhoud van een distributie punt of peer.  

U past voor bereide media op de harde schijf van een nieuwe computer toe voordat u de computer naar de gebruiker verzendt. Wanneer de computer voor de eerste keer wordt opgestart nadat u de voor bereide media hebt toegepast, wordt de computer gestart in Windows PE. Er wordt verbinding gemaakt met een beheer punt om de taken reeks te vinden waarmee het implementatie proces van het besturings systeem wordt voltooid.  

> [!IMPORTANT]
> De pakketten op voor bereide media zijn niet versleuteld. Neem de juiste beveiligings maatregelen, zoals het toevoegen van een wacht woord aan de media, om ervoor te zorgen dat de pakket inhoud beveiligd is tegen onbevoegde gebruikers.

## <a name="standalone-media"></a><a name="BKMK_PlanStandaloneMedia"></a>Zelfstandige media

Zelfstandige media bevatten alles wat u nodig hebt om het besturings systeem te implementeren. Deze inhoud bevat de taken reeks en alle overige vereiste inhoud. Omdat alles op de media staat, is de benodigde schijf ruimte groter dan voor andere media typen.

## <a name="considerations-when-using-https"></a>Overwegingen bij het gebruik van HTTPS

Wanneer u uw beheer punten en distributie punten configureert voor het gebruik van HTTPS, maakt u opstart media en voor bereide media op een primaire site, niet op de centrale beheer site. Houd ook rekening met het volgende punt om te bepalen of de media moeten worden geconfigureerd als dynamisch of op de site gebaseerd:  

- Als u de media wilt configureren als dynamische media, moeten alle primaire sites de basis certificerings instantie (CA) hebben van de site van waaruit u de media hebt gemaakt. U kunt de basiscertificeringsinstantie importeren voor alle primaire sites in de hiërarchie.  

- Wanneer primaire sites in uw Configuration Manager-hiërarchie verschillende basis certificerings instanties gebruiken, moet u op elke site op de site gebaseerde media gebruiken.  

## <a name="next-steps"></a>Volgende stappen

- [Vastelegmedia maken](create-capture-media.md)

- [Opstartbare media maken](create-bootable-media.md)

- [Voorbereide media maken](create-prestaged-media.md)

- [Zelfstandige media maken](create-stand-alone-media.md)
