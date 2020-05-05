---
title: Opstartbare media gebruiken om Windows te implementeren via het netwerk
titleSuffix: Configuration Manager
description: Gebruik opstart bare media-implementaties in Configuration Manager om het besturings systeem te implementeren wanneer de doel computer wordt gestart.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22a3219cdf0bb09061e57f34e52ca7a061f55a2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724361"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Opstart bare media gebruiken om Windows via het netwerk te implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt het besturings systeem implementeren wanneer de doel computer met behulp van een opstart bare media-implementatie begint. Het medium bevat een verwijzing naar de taken reeks, de installatie kopie van het besturings systeem en andere vereiste inhoud van het netwerk. Wanneer de doel computer wordt gestart, haalt de computer de items op waarnaar wordt verwezen in de wijzer. Met de opstart bare media vrije inhoud kunt u het doel bijwerken zonder dat u het op de media hoeft te vervangen.

U kunt besturings systemen via het netwerk implementeren met behulp van multi cast in de volgende implementatie scenario's voor besturings systemen:

-   [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)  

-   [Een bestaande computer vervangen en de instellingen overzetten](replace-an-existing-computer-and-transfer-settings.md)  

Voer de stappen in een van de implementatiescenario's voor besturingssystemen uit en gebruik vervolgens de volgende secties om het besturingssysteem te implementeren met opstartbare media.  

## <a name="configure-deployment-settings"></a>Implementatie-instellingen configureren  
Wanneer u opstart bare media gebruikt om het implementatie proces van het besturings systeem te starten, moet u de implementatie configureren om het besturings systeem beschikbaar te maken voor de media. U kunt deze optie instellen op de pagina **implementatie-instellingen** van de wizard software implementeren of op het tabblad implementatie- **instellingen** in de eigenschappen voor de implementatie. Configureer een van de volgende waarden voor de instelling **Toegankelijk maken voor de volgende** :

-   Configuration Manager-clients, media en PXE

-   Alleen media en PXE

-   Alleen media en PXE (verborgen)

## <a name="create-the-bootable-media"></a>De opstartbare media maken
U kunt opgeven of de opstart bare media een USB-flash station of een CD/DVD-set is. De computer die de media start, moet ondersteuning bieden voor de optie die u kiest als een opstartbaar station. Zie [opstart bare media maken](create-bootable-media.md)voor meer informatie.  

##  <a name="install-the-operating-system-from--bootable-media"></a><a name="BKMK_Deploy"></a> Het besturingssysteem installeren vanaf opstartbare media  
De opstartbare media invoegen in een opstartbaar station op de computer en deze vervolgens inschakelen om het besturingssysteem te installeren.
