---
title: Surface Device-dash board
titleSuffix: Configuration Manager
description: Bekijk informatie over Surface-apparaten met behulp van het dash board.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 08baf595199bdda121f897d507de97cb7e93e620
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715065"
---
# <a name="surface-device-dashboard-in-configuration-manager"></a>Dash board van Surface-apparaat in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Vanaf versie 1802 biedt het Surface Device-dash board informatie over Surface-apparaten die in uw omgeving in één oogopslag worden gevonden. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Het Surface Device-dash board openen

Voer de volgende stappen uit om het Surface Device-dash board te openen: 

1. Open de Configuration Manager-console. 
2. Klik op het knoop punt **bewaking** . 
3. Klik op **Surface devices**om het dash board te laden.

**Surface device dashboard**
![Dash board van Surface-apparaat dashboard](media/Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Informatie bekijken in het Surface Device-dash board

Het Surface Device-dash board toont drie grafieken voor uw omgeving. 

- **Percentage van Surface-apparaten** : geeft u het percentage Surface-apparaten in uw omgeving.

    ![Grafiek percentage van Surface-apparaten](media/Percent-Surface-Devices.PNG)
- **Surface-modellen** : hier wordt het aantal apparaten per surface model weer gegeven. 
  - Als u de muis aanwijzer boven een grafiek sectie houdt, geeft u het percentage Surface-apparaten weer dat door het model is geselecteerd. 

       ![Grafiek van oppervlak modellen](media/Surface-Models-Hover.PNG)
  - Als u op een grafiek gedeelte klikt, gaat u naar een lijst met apparaten voor het model. 
      ![Lijst met apparaten voor Surface model](media/Surface-Model-Device-List.PNG)

- **Top vijf van firmware versies**: geeft een grafiek weer met de vijf meest voorkomende firmware modellen in uw omgeving. 
  - Als u de muis aanwijzer boven een grafiek sectie houdt, geeft u het aantal Surface-apparaten weer dat de firmware versie is geselecteerd. Vanaf Configuration Manager versie 1806, klikken op een grafiek sectie, wordt een lijst met relevante apparaten weer gegeven. <!--1358654-->
     ![Lijst met apparaten voor Surface model](media/Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Meer informatie

Zie voor meer informatie over Surface-apparaten:
- De [Surface]( https://go.microsoft.com/fwlink/?linkid=861998) -website.

Zie voor meer informatie over het implementeren van Surface firmware-updates in Configuration Manager:
- [Updates van Surface drivers beheren in Configuration Manager]( https://support.microsoft.com/help/4098906).




