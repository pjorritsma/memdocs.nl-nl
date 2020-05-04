---
title: Software-inventaris weer geven met resource Explorer
titleSuffix: Configuration Manager
description: Resource Explorer gebruiken om software-inventaris in Configuration Manager weer te geven.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710655"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Resource Explorer gebruiken om software-inventaris in Configuration Manager weer te geven

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik resource Explorer in Configuration Manager om informatie weer te geven over software-inventaris die is verzameld van computers in uw hiërarchie.  

> [!NOTE]  
>  Resource Explorer geeft geen inventaris gegevens weer tot er een software-inventarisatie cyclus is uitgevoerd op de client.  

 Resource Explorer biedt de volgende informatie over software-inventarisatie:  

-   **Software**:  

    -   **Verzamelde bestanden** -bestanden die zijn verzameld tijdens de software-inventarisatie.  

    -   **Bestands Details** -bestanden die zijn geïnventariseerd tijdens de software-inventarisatie die niet zijn gekoppeld aan een specifiek product of een specifieke fabrikant.  

    -   **Laatste software scan** -datum en tijd van de laatste software-inventaris en bestands verzameling voor de client computer.  

    -   **Product gegevens** -software producten die door software-inventarisatie zijn geïnventariseerd, gegroepeerd op fabrikant.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Resource Explorer uitvoeren vanaf de Configuration Manager-console  

1.  Kies in de Configuration Manager-console **activa en naleving**

2.  Kies in de werk ruimte **activa en naleving** de optie **apparaten** of open een verzameling die apparaten weergeeft.  

3.  Kies de computer met de inventaris die u wilt weer geven en kies op het tabblad **Start** > groep **apparaten** de optie**resource Verkenner** **starten** > .

4.  U kunt met de rechter muisknop op een item in het rechterdeel venster van de resource Explorer klikken en **Eigenschappen** kiezen om de verzamelde inventaris gegevens in een meer Lees bare indeling weer te geven.  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> Verzamelde diagnostische bestanden weer geven en beheren

Vanaf Configuration Manager versie 2002 kunt u resource Explorer gebruiken om de verzamelde bestanden weer te geven en te beheren wanneer u client meldingen gebruikt voor het [verzamelen van client logboeken](../client-notification.md#client-diagnostics). 

1. Klik in het knoop punt **apparaten** met de rechter muisknop op het apparaat waarvoor u logboeken wilt weer geven.
1. Selecteer **Start**en vervolgens **resource Explorer**.
1. Klik in **resource Explorer**op **Diagnostische bestanden**.
1. In de lijst **Diagnostische bestanden** ziet u de verzamel datum voor de bestanden. De naam indeling van de client logboeken `Support_<guid>.zip`is.
1. Klik met de rechter muisknop op het zip-bestand en selecteer een van de volgende opties:
    - **Open ondersteunings centrum**: start het [ondersteunings centrum](../../../support/support-center.md).
    - **Kopiëren**: kopieert de gegevens van de rij uit resource Explorer.
    - **Bestand weer geven**: Hiermee opent u de map waarin het zip-bestand zich bevindt met Verkenner.
    - **Opslaan**: Hiermee opent u een dialoog venster bestand opslaan voor het geselecteerde bestand.
    - **Exporteren**: slaat de resource Explorer-kolommen op die worden weer gegeven in **Diagnostische bestanden**.
    - **Vernieuwen**: Hiermee vernieuwt u de bestanden lijst.
    - **Eigenschappen**: retourneert de eigenschappen van het geselecteerde bestand. 

[![Client logboeken controleren en opslaan vanuit resource Explorer](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>Volgende stappen

[Gebruik het ondersteunings centrum](../../../support/support-center.md) om verzamelde diagnostische bestanden weer te geven.
