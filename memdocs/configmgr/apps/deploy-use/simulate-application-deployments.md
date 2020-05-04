---
title: De implementatie van een toepassing simuleren
titleSuffix: Configuration Manager
description: Evalueer de detectie methode, vereisten en afhankelijkheden voor een implementatie type zonder de toepassing te installeren.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bed491b4800dd6ae8b53a837618abf3d8a5a597d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710592"
---
# <a name="simulate-application-deployments-with-configuration-manager"></a>Toepassings implementaties simuleren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt gesimuleerde implementaties gebruiken om een toepassings implementatie te testen zonder de toepassing te installeren of te verwijderen. Een gesimuleerde implementatie evalueert de detectie methode, vereisten en afhankelijkheden voor een implementatie type. De resultaten worden gerapporteerd in het knoop punt **implementaties** van de werk ruimte **bewaking** . Gebruik de procedure in dit onderwerp om een toepassings implementatie te simuleren in Configuration Manager.  

> [!NOTE]  
> U kunt gesimuleerde implementaties niet gebruiken voor verzamelingen van mobiele apparaten.  
>   
> U kunt een toepassing niet implementeren met het implementatiedoel **Verwijderen** als een gesimuleerde implementatie van dezelfde toepassing actief is.  

## <a name="configure-a-simulated-application-deployment"></a>Een gesimuleerde toepassings implementatie configureren

1.  Selecteer in de Configuration Manager-console een van de volgende opties:  
    -   Een verzameling gebruikers.  
    -   Een verzameling apparaten.  
    -   Een Configuration Manager-toepassing.  

2.  Kies op het tabblad **Start** in de groep **implementatie** de optie **implementatie simuleren**.  

3.  Stel in de wizard implementatie van toepassing simuleren de volgende gegevens in voor uw gesimuleerde implementatie:  

    -   **Toepassing**. Kies **Bladeren**en selecteer vervolgens de toepassing waarvoor u een gesimuleerde implementatie wilt maken.  

    -   **Verzameling**. Kies **Bladeren**en selecteer vervolgens de verzameling die u wilt gebruiken voor de gesimuleerde implementatie.  

    -   **Actie**. Selecteer in de vervolg keuzelijst of u de installatie of het verwijderen van de geselecteerde toepassing wilt simuleren.  

    -   **Automatisch implementeren met of zonder gebruikers aanmelding**. Als deze optie is ingeschakeld, evalueren de clients de gesimuleerde implementatie, ongeacht of de clients zijn aangemeld.  

4.  Klik op **volgende**, Controleer de informatie op de pagina **samen vatting** en voltooi vervolgens de wizard om de gesimuleerde toepassings implementatie te maken.  

5.  Gesimuleerde toepassingen worden weer gegeven in het knoop punt **implementaties** van de werk ruimte **bewaking** , met het doel te **simuleren**. Zie [toepassingen bewaken in de Configuration Manager-console](../../apps/deploy-use/monitor-applications-from-the-console.md)voor meer informatie over het bewaken van toepassings implementaties.  
