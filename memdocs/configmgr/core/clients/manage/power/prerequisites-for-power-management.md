---
title: Vereisten voor energiebeheer
titleSuffix: Configuration Manager
description: De vereisten voor energie beheer in Configuration Manager ophalen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a816d333d96dba6cb1c38f6499ccac78e2db8a3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715184"
---
# <a name="prerequisites-for-power-management-in-configuration-manager"></a>Vereisten voor energie beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Energie beheer in Configuration Manager heeft externe afhankelijkheden en afhankelijkheden binnen het product.  

## <a name="dependencies-external-to-configuration-manager"></a>Afhankelijkheden extern aan Configuration Manager  
 De volgende tabel geeft een lijst van de afhankelijkheden die extern zijn Configuration Manager voor het gebruik van energie beheer.  

|Afhankelijkheid|Meer informatie|  
|----------------|----------------------|  
|Clientcomputers moeten de vereiste energiestatussen ondersteunen|Voor het gebruik van alle functies van energiebeheer moeten clientcomputers de acties slaapstand, sluimerstand, activeren vanuit slaapstand en activeren vanuit sluimerstand ondersteunen. U kunt het rapport **Energiemogelijkheden** gebruiken om te bepalen of computers deze acties ondersteunen. Zie voor meer informatie [energie-mogelijkheden rapport](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) in het onderwerp het [controleren en plannen voor energie beheer](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager-afhankelijkheden  
 De volgende tabel bevat de afhankelijkheden in Configuration Manager voor het gebruik van energie beheer.  

|Afhankelijkheid|Meer informatie|  
|----------------|----------------------|  
|Energiebeheer moet worden ingeschakeld voordat u energiebeheerschema's kunt maken en controleren.|Zie [energie beheer configureren](../../../../core/clients/manage/power/configuring-power-management.md)voor meer informatie over het inschakelen en configureren van energie beheer.|  
|Reporting Services-punt|U moet een Reporting Services-punt configureren voordat u energiebeheerrapporten kunt weergeven. Zie [Introduction to Reporting](../../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.|  
