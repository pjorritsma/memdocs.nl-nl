---
title: Multicast gebruiken om Windows via het netwerk te implementeren
titleSuffix: Configuration Manager
description: Gebruik multi cast in uw Configuration Manager omgeving zodat op meerdere computers tegelijkertijd de installatie kopie van het besturings systeem kan worden gedownload.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f580467ccb26209ed20666733e30959bbf50128
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124702"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-configuration-manager"></a>Multi cast gebruiken om Windows via het netwerk te implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Multi cast is een methode voor netwerk optimalisatie die u kunt gebruiken wanneer meerdere clients tegelijkertijd dezelfde installatie kopie van het besturings systeem downloaden. Wanneer u multi cast gebruikt, downloaden meerdere computers tegelijkertijd de installatie kopie van het besturings systeem als multi cast door het distributie punt. Dit gedrag bevindt zich in plaats van elke client, waarbij een kopie van de installatie kopie wordt gedownload via een afzonderlijke verbinding van het distributie punt.

Besturings systemen via het netwerk implementeren met behulp van multi cast in de volgende scenario's voor besturingssysteem implementaties:

- [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)

Voer de stappen in een van deze scenario's voor implementatie van het besturings systeem uit. Gebruik vervolgens de volgende secties om multi cast te ondersteunen.

## <a name="configure-distribution-points-for-multicast"></a><a name="BKMK_Configure"></a>Distributie punten configureren voor multi cast

Als u multi cast wilt gebruiken, moet u ten minste één distributie punt configureren voor de ondersteuning van multi cast. Zie [distributie punten installeren en configureren](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)voor meer informatie.

Zie [poorten](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-DP2)voor een lijst met poorten die vereist zijn voor de ondersteuning van multi cast.

## <a name="prepare-an-os-image-for-multicast"></a>Een installatie kopie van een besturings systeem voorbereiden voor multi cast

U moet de installatie kopie van het besturings systeem configureren voor de ondersteuning van multi cast. Zie [de installatie kopie van het besturings systeem voorbereiden voor multi cast-implementaties](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast)voor meer informatie.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> De takenreeks implementeren

Implementeer het besturings systeem in een doel verzameling. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Gebruikerservaring voor implementatie van besturingssysteem](../understand/user-experience.md)
