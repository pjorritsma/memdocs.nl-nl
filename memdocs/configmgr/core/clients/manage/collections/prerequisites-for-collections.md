---
title: Vereisten voor verzamelingen
titleSuffix: Configuration Manager
description: Bekijk de vereisten voor het gebruik van verzamelingen in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 313c3183cd6401390d743575ba513026a3e3f607
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714498"
---
# <a name="prerequisites-for-collections-in-configuration-manager"></a>Vereisten voor verzamelingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Verzamelingen in Configuration Manager bevatten alleen afhankelijkheden binnen het product.  

## <a name="configuration-manager-dependencies"></a>Configuration Manager-afhankelijkheden  

|Afhankelijkheid|Meer informatie|  
|----------------|----------------------|  
|Reporting Services-punt|De sitesysteemrol Reporting Services-punt moet zijn geïnstalleerd voordat u rapporten kunt uitvoeren voor verzamelingen. Zie [Introduction to Reporting](../../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.|  
|Er moeten specifieke beveiligingsmachtigingen zijn verleend om verzamelingen te beheren|U moet over de volgende beveiligingsmachtigingen beschikken om instellingen voor naleving te beheren:<br /><br /> -Voor het maken en beheren van verzamelingen: **maken**, **verwijderen**, **wijzigen**, **map wijzigen**, **object verplaatsen**, **lezen** en **resource lezen** voor het object **verzameling** .<br /><br /> -Verzamelings instellingen beheren: de instelling voor **het verzamelings** object **wijzigen** .<br /><br /> De machtiging **Map wijzigen** is vereist voor alle verzamelingsmappen, met inbegrip van de hoofdmap.|  
