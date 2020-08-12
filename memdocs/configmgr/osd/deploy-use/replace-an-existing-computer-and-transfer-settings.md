---
title: Een bestaande computer vervangen en de instellingen overzetten
titleSuffix: Configuration Manager
description: Kies in Configuration Manager een van de implementatie methoden, zoals opstart bare media, multi cast of software Center, om een bestaande computer te vervangen door een nieuwe computer.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 860ee3aeb255921ccd8bf3b1695a9647b514752f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124865"
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-configuration-manager"></a>Een bestaande computer vervangen en de instellingen overzetten met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat de algemene stappen in Configuration Manager een bestaande computer vervangen door een nieuwe computer. U kunt voor dit scenario kiezen uit veel verschillende implementatiemethoden, zoals het implementeren via opstartbare media, multicast of Software Center. U kunt er ook voor kiezen om een statusmigratiepunt te installeren waarin de instellingen kunnen worden opgeslagen om deze vervolgens terug te zetten in het nieuwe besturingssysteem nadat dit is geïnstalleerd. Zie [scenario's voor het implementeren van ENTER prise-besturings systemen](scenarios-to-deploy-enterprise-operating-systems.md)als u niet zeker weet of dit het juiste scenario voor besturingssysteem implementatie voor u is.  

 Gebruik de volgende secties om een bestaande computer te vernieuwen met een nieuwe versie van Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Fonds  

-   **Infrastructuurvereisten plannen en implementeren**  

     Er zijn verschillende vereisten voor de infra structuur die moeten worden uitgevoerd voordat u besturings systemen kunt implementeren, zoals Windows ADK, Hulpprogramma voor migratie van gebruikersstatus (USMT), Windows Deployment Services (WDS), ondersteunde vaste-schijf configuraties, enzovoort. Zie [vereisten voor de infra structuur voor de implementatie van besturings systemen](../plan-design/infrastructure-requirements-for-operating-system-deployment.md) voor meer informatie  

-   **Een statusmigratiepunt installeren (alleen vereist als u instellingen overzet)**  

     Wanneer u de instellingen van een bestaande computer wilt vastleggen om deze vervolgens terug te zetten in het nieuwe besturingssysteem, moet u een statusmigratiepunt installeren. Zie [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)voor meer informatie.  

##  <a name="configure"></a><a name="BKMK_Configure"></a>Geconfigureerd  

1.  **Een opstartinstallatiekopie voorbereiden**  

     Opstartinstallatiekopieën starten een computer op in een Windows PE-omgeving (minimaal besturingssysteem met beperkte onderdelen en services), waarna er een volledig Windows-besturingssysteem op de computer kan worden geïnstalleerd. Wanneer u besturingssystemen implementeert, moet u de opstartinstallatiekopie selecteren die u wilt gebruiken en de installatiekopie distribueren naar een distributiepunt. Gebruik de volgende informatie om een opstartinstallatiekopie voor te bereiden:  

    -   Zie [opstart installatie kopieën beheren](../get-started/manage-boot-images.md)voor meer informatie over opstart installatie kopieën.  

    -   Zie [opstart installatie kopieën aanpassen](../get-started/customize-boot-images.md)voor meer informatie over het aanpassen van een opstart installatie kopie.  

    -   Distribueer de opstartinstallatiekopie naar distributiepunten. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Een installatiekopie van een besturingssysteem voorbereiden**  

     De installatiekopie van het besturingssysteem bevat de bestanden die nodig zijn om het besturingssysteem op de doelcomputer te installeren. Gebruik de volgende informatie om de installatiekopie van het besturingssysteem voor te bereiden:  

    -   Zie [installatie kopieën van besturings systemen beheren](../get-started/manage-operating-system-images.md)voor meer informatie over het maken van een installatie kopie van een besturings systeem.  

    -   Distribueer de installatiekopie van het besturingssysteem naar distributiepunten. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Een takenreeks maken om besturingssystemen via het netwerk te implementeren**  

     Maak een takenreeks om de installatie van het besturingssysteem via het netwerk te automatiseren. Volg de stappen in [een taken reeks maken om een besturings systeem te installeren](create-a-task-sequence-to-install-an-operating-system.md) om de taken reeks te maken om het besturings systeem te implementeren. Afhankelijk van de implementatiemethode waarvoor u kiest, kunnen er aanvullende overwegingen zijn bij het samenstellen van de takenreeks.  

    > [!NOTE]  
    >  Als u in dit scenario gebruikersinstellingen en bestanden vastlegt en terugzet, kunt u ervoor kiezen om een statusmigratiepunt te gebruiken om de bestanden lokaal op te slaan. Zie [gebruikers status beheren](../get-started/manage-user-state.md)voor meer informatie.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Zetten  

-   Gebruik een van de volgende implementatiemethoden om het besturingssysteem te implementeren:  

    -   [Windows met Software Center via het netwerk implementeren](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Opstartbare media gebruiken om Windows te implementeren via het netwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Multicast gebruiken om Windows via het netwerk te implementeren](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Een installatiekopie voor een OEM in de fabriek of bij een lokaal depot maken](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Controleren  

-   **De takenreeksimplementatie controleren**  

     Zie [implementaties van besturings systemen](monitor-operating-system-deployments.md)bewaken voor het bewaken van de taken reeks implementatie om het besturings systeem te installeren.  
