---
title: Multicast gebruiken om Windows via het netwerk te implementeren
titleSuffix: Configuration Manager
description: Gebruik multi cast in uw Configuration Manager omgeving zodat op meerdere computers tegelijkertijd de installatie kopie van het besturings systeem kan worden gedownload.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f81b23d3783d397d83a3925b98c0c8f601fa4012
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720119"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Multi cast gebruiken om Windows via het netwerk te implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Multi cast is een methode voor netwerk optimalisatie die u kunt gebruiken in uw Configuration Manager omgeving waarin meerdere clients tegelijkertijd dezelfde installatie kopie van het besturings systeem downloaden. Wanneer multicast wordt gebruikt, kunnen meerdere computers tegelijkertijd de installatiekopie van het besturingssysteem downloaden, aangezien deze door het distributiepunt wordt aangeboden via multicasting. Het distributiepunt verzendt dus geen kopie van de gegevens via een aparte verbinding naar elke client.  

 U kunt besturingssystemen via het netwerk implementeren met behulp van multicast in de volgende implementatiescenario's voor besturingssystemen:  

- [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)  

  Voer de stappen in een van de implementatiescenario’s voor besturingssystemen uit en gebruik de volgende secties om multicast te ondersteunen.  

##  <a name="configure-a-distribution-point-to-support-multicast"></a><a name="BKMK_Configure"></a> Een distributiepunt configureren voor de ondersteuning van multicast  
 Als u multicast wilt gebruiken om het besturingssysteem te implementeren, moet u een distributiepunt configureren voor de ondersteuning van multicast. Zie [distributie punten installeren en configureren](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)voor meer informatie. Zie [poorten](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2)voor een lijst met poorten die vereist zijn voor de ondersteuning van multi cast.  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>De installatiekopie van een besturingssysteem voorbereiden voor multicast-implementaties  
 Zie [Prepare the operating system image for multicast deployments](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast)als u pakket voor de installatiekopie van het besturingssysteem wilt configureren voor de ondersteuning van multicast.  

##  <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> De takenreeks implementeren  
 Implementeer het besturingssysteem in een doelverzameling. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.  
