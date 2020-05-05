---
title: Voorbereiden op onbekende computerimplementaties
titleSuffix: Configuration Manager
description: Meer informatie over het implementeren van besturings systemen op computers die niet worden beheerd door Configuration Manager in uw Configuration Manager omgeving.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e79e2ec1d42c7ed0e520b5e117fbac73817511a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724067"
---
# <a name="prepare-for-unknown-computer-deployments-in-configuration-manager"></a>Voorbereiden op onbekende computer implementaties in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de informatie in dit onderwerp om besturings systemen te implementeren op onbekende computers in uw Configuration Manager omgeving. Een onbekende computer is een computer die niet wordt beheerd door Configuration Manager. Dit betekent dat er geen records zijn van deze computers in de Configuration Manager-Data Base. Onbekende computers omvatten het volgende:  

- Een computer waarop de Configuration Manager-client niet is geïnstalleerd  

- Een computer die niet is geïmporteerd in Configuration Manager  

- Een computer die niet is gedetecteerd door Configuration Manager  

  U kunt de volgende implementatiemethoden gebruiken om besturingssystemen op onbekende computers te implementeren:  

- [PXE gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Opstartbare media gebruiken om een besturingssysteem te implementeren](../deploy-use/create-bootable-media.md)  

- [Voorbereide media gebruiken om een besturingssysteem te implementeren](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Werkstroom voor de implementatie op een onbekende computer  
 De volgende werkstroom bevat de basisstappen om een besturingssysteem op een onbekende computer te implementeren:  

-   Selecteer een onbekend computerobject dat in de implementatie moet worden gebruikt. U kunt het besturingssysteem implementeren op een van de onbekende computerobjecten in de verzameling **Alle onbekende computers** of u kunt de objecten in de verzameling **Alle onbekende computers** toevoegen aan een andere verzameling. Configuration Manager biedt twee onbekende computer objecten in de verzameling **alle onbekende computers** . Het ene object is voor x86-computers en het andere object is voor x64-computers.  

    > [!NOTE]  
    >  Het object **Onbekende x86-compute** is bedoeld voor computers die alleen in x86-architectuur werken. Het object **Onbekende x64-computer** is bedoeld voor computers die x86- en x64-architectuur ondersteunen. Met andere woorden, deze objecten beschrijven de architectuur van de doelcomputer. Ze beschrijven niet het besturingssysteem dat u op de doelcomputer wilt implementeren.  

-   Configureer een distributiepunt met PXE-functionaliteit of maak media om implementaties op onbekende computers te ondersteunen.  

-   Implementeer de takenreeks om het besturingssysteem te installeren.  

## <a name="unknown-computer-installation-process"></a>Installatieproces van onbekende computer  
 Wanneer een computer voor het eerst wordt gestart vanuit PXE of vanaf media, controleert Configuration Manager of er een record voor die computer in de Configuration Manager-Data Base aanwezig is. Als er een record is, wordt Configuration Manager gecontroleerd of er taken reeksen voor de record zijn geïmplementeerd. Als er geen record is, wordt Configuration Manager gecontroleerd of er taken reeksen zijn geïmplementeerd op een onbekend computer object. In beide gevallen voert Configuration Manager een van de volgende acties uit:  

- Als er een beschik bare taken reeks is, wordt de gebruiker door Configuration Manager gevraagd om de taken reeks uit te voeren.  

- Als er een vereiste taken reeks is, wordt de taken reeks automatisch door Configuration Manager uitgevoerd.  

- Als er voor de record geen taken reeks is geïmplementeerd, wordt door Configuration Manager een fout gegenereerd dat er geen geïmplementeerde taken reeks voor de doel computer is.  

  Wanneer een onbekende computer wordt gestart, herkent Configuration Manager de computer als een niet-ingerichte computer in plaats van een onbekende computer. Dit betekent dat de computer nu de takenreeksen kan ontvangen die zijn geïmplementeerd voor het onbekende computerobject. De geïmplementeerde taken reeks installeert vervolgens een installatie kopie van het besturings systeem die de Configuration Manager-client moet bevatten.  

  Nadat de Configuration Manager-client is geïnstalleerd, wordt er een record voor de computer gemaakt en wordt de computer weer gegeven in de juiste Configuration Manager verzameling. Als de computer de installatie kopie van het besturings systeem of de Configuration Manager-client niet kan installeren, wordt een record ' onbekend ' voor de computer gemaakt en wordt de computer weer gegeven in de verzameling **alle systemen** .  

> [!NOTE]  
>  Tijdens de installatie van de installatiekopie van het besturingssysteem kan de takenreeks verzamelingsvariabelen, maar geen computervariabelen van deze computer ophalen.  

##  <a name="enabling-unknown-computer-support"></a><a name="BKMK_EnablingUnknown"></a> Ondersteuning van onbekende computers inschakelen  
 Gebruik de volgende informatie om ondersteuning van onbekende computers in te schakelen wanneer u een besturingssysteem implementeert met PXE, opstartbare media en voorbereide media.  

-   **PXE**  

     Schakel het selectievakje **Ondersteuning van onbekende computers inschakelen** in op het tabblad **PXE** voor een distributiepunt met PXE-functionaliteit. Zie [Distributiepunten configureren voor de acceptatie van PXE-aanvragen](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)voor meer informatie.  

-   **Opstartbare media**  

     Schakel het selectievakje **Ondersteuning van onbekende computers inschakelen** in op de pagina **Beveiliging** van de wizard Takenreeksmedia maken. Zie [distributie punten configureren voor het accepteren van PXE-aanvragen](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) en [PXE gebruiken om Windows via het netwerk te implementeren met Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie.  

-   **Voorbereide media**  

     Schakel het selectievakje **Ondersteuning van onbekende computers inschakelen** in op de pagina **Beveiliging** van de wizard Takenreeksmedia maken. Zie voor [bereide media maken met Configuration Manager](../deploy-use/create-prestaged-media.md)voor meer informatie.  
