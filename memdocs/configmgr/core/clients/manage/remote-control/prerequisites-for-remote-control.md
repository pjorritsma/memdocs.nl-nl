---
title: Vereisten voor beheer op afstand
titleSuffix: Configuration Manager
description: De vereisten voor beheer op afstand in Configuration Manager ophalen.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f19f8799dd90fc61c0bfeeee1dc60125ba491fef
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715114"
---
# <a name="prerequisites-for-remote-control-in-configuration-manager"></a>Vereisten voor extern beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Extern beheer in Configuration Manager heeft externe afhankelijkheden en afhankelijkheden in het product.  

## <a name="dependencies-external-to-configuration-manager"></a>Afhankelijkheden extern aan Configuration Manager  

|Afhankelijkheid|Meer informatie|  
|----------------|----------------------|  
|Videokaartstuurprogramma van de computer|Zorg ervoor dat het meest recente videostuurprogramma is geïnstalleerd op clientcomputers om optimale prestaties van extern beheer te garanderen.|  

 Apparaten waarop Windows Embedded, Windows Embedded voor Point van Service (POS) of Windows Fundamentalss voor Legacy PCs is geïnstalleerd, bieden geen ondersteuning voor de viewer voor extern beheer, maar ze bieden wel ondersteuning voor de client voor extern beheer.  

 Configuration Manager beheer op afstand kan niet worden gebruikt voor het extern beheren van client computers met Systems Management Server 2003 of Configuration Manager 2007.  

> [!NOTE]  
>  Er zijn geen Windows-services vereist als een externe afhankelijkheid voor extern beheer.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Ondersteunde besturingssystemen voor de viewer voor extern beheer  
De viewer voor beheer op afstand wordt ondersteund op alle besturings systemen die worden ondersteund voor de Configuration Manager-console. Zie [ondersteunde configuraties voor Configuration Manager-consoles](../../../../core/plan-design/configs/supported-operating-systems-consoles.md)voor meer informatie.   

## <a name="configuration-manager-dependencies"></a>Configuration Manager-afhankelijkheden  

|Afhankelijkheid|Meer informatie|  
|----------------|----------------------|  
|Beheer op afstand moet worden ingeschakeld voor clients|Beheer op afstand is standaard niet ingeschakeld wanneer u Configuration Manager installeert. Zie [extern beheer configureren](../../../../core/clients/manage/remote-control/configuring-remote-control.md)voor meer informatie over het inschakelen en configureren van beheer op afstand.|  
|Reporting Services-punt|De sitesysteemrol Reporting Services-punt moet zijn geïnstalleerd voordat u rapporten kunt uitvoeren voor extern beheer. Zie [Introduction to Reporting](../../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.|  
|Beveiligingsmachtigingen voor het beheren van extern beheer|Voor toegang tot verzamelings bronnen en het starten van een sessie voor beheer op afstand vanuit de Configuration Manager-console: machtiging **lezen**, **resource lezen**en **beheer op afstand** voor het object **verzameling** .<br /><br /> De beveiligingsrol **operator voor externe Hulpprogram ma's** bevat deze machtigingen die vereist zijn voor het beheren van beheer op afstand in Configuration Manager.<br /><br /> Zie op [rollen gebaseerd beheer configureren voor Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md)voor meer informatie.<br /><br /> Daarnaast moeten toegelaten viewers toestemming krijgen om beheer op afstand te kunnen gebruiken door deze gebruikers toe te voegen aan de lijst **met toegestane viewers van beheer op afstand en hulp** op afstand in de client instellingen voor **externe hulpprogram ma's** .
