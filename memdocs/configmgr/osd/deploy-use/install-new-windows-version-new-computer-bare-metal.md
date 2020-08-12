---
title: Windows installeren op een nieuwe computer
titleSuffix: Configuration Manager
description: Gebruik Configuration Manager om een besturings systeem op een nieuwe computer (bare metal) te installeren met behulp van PXE, OEM of zelfstandige media.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eb880b6cb6f45de06b602bc9caa8ca7b98022d5
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125079"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-configuration-manager"></a>Installeer een nieuwe versie van Windows op een nieuwe computer (bare metal) met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat de algemene stappen in Configuration Manager om een besturings systeem op een nieuwe computer te installeren. U kunt voor dit scenario kiezen uit veel verschillende implementatiemethoden, zoals PXE, OEM of zelfstandige media. Zie [scenario's voor het implementeren van ENTER prise-besturings systemen](scenarios-to-deploy-enterprise-operating-systems.md)als u niet zeker weet of dit het juiste scenario voor besturingssysteem implementatie voor u is.  

Gebruik de volgende secties om een bestaande computer te vernieuwen met een nieuwe versie van Windows.  

##  <a name="plan"></a><a name="BKMK_Plan"></a>Fonds  

-   **Infrastructuurvereisten plannen en implementeren**  

     Er zijn verschillende vereisten voor de infra structuur die moeten worden uitgevoerd voordat u besturings systemen kunt implementeren, zoals Windows ADK, Windows Deployment Services (WDS), ondersteunde configuraties van harde schijven, enzovoort. Zie [vereisten voor de infra structuur voor de implementatie van besturings systemen](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)voor meer informatie.

##  <a name="configure"></a><a name="BKMK_Configure"></a>Geconfigureerd  

1.  **Een opstartinstallatiekopie voorbereiden**  

     Opstartinstallatiekopieën starten een computer op in een Windows PE-omgeving (minimaal besturingssysteem met beperkte onderdelen en services), waarna er een volledig Windows-besturingssysteem op de computer kan worden geïnstalleerd.   Wanneer u besturingssystemen implementeert, moet u de opstartinstallatiekopie selecteren die u wilt gebruiken en de installatiekopie distribueren naar een distributiepunt. Gebruik de volgende informatie om een opstartinstallatiekopie voor te bereiden:  

    -   Zie [opstart installatie kopieën beheren](../get-started/manage-boot-images.md)voor meer informatie over opstart installatie kopieën.  

    -   Zie [opstart installatie kopieën aanpassen](../get-started/customize-boot-images.md)voor meer informatie over het aanpassen van een opstart installatie kopie.  

    -   Distribueer de opstartinstallatiekopie naar distributiepunten. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Een installatiekopie van een besturingssysteem voorbereiden**  

     De installatiekopie van het besturingssysteem bevat de bestanden die nodig zijn om het besturingssysteem op de doelcomputer te installeren. Gebruik de volgende informatie om de installatiekopie van het besturingssysteem voor te bereiden:  

    -   Zie [installatie kopieën van besturings systemen beheren](../get-started/manage-operating-system-images.md)voor meer informatie over het maken van een installatie kopie van een besturings systeem.

    -   Distribueer de installatiekopie van het besturingssysteem naar distributiepunten. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > Nieuwe installaties van Windows kunnen ook worden uitgevoerd op basis van installatie bron bestanden via OS-upgrade pakketten, maar u kunt in plaats daarvan installatie kopieën van het besturings systeem, zoals **install. Wim** , gebruiken.
    >
    > Het implementeren van nieuwe installaties van Windows via upgrade pakketten van het besturings systeem wordt nog steeds ondersteund, maar is afhankelijk van Stuur Programma's die compatibel zijn met deze methode. Wanneer u Windows installeert vanuit een upgrade pakket voor het besturings systeem, worden er Stuur Programma's geïnstalleerd terwijl Windows PE nog steeds wordt toegevoegd in Windows PE. Sommige Stuur Programma's zijn niet compatibel met geïnstalleerd tijdens de installatie van Windows PE. Als Stuur Programma's niet compatibel zijn met de installatie van in Windows PE, gebruikt u in plaats daarvan een installatie kopie van het besturings systeem.  

3.  **Een takenreeks maken om besturingssystemen via het netwerk te implementeren**  

     Maak een takenreeks om de installatie van het besturingssysteem via het netwerk te automatiseren. Volg de stappen in [een taken reeks maken om een besturings systeem te installeren](create-a-task-sequence-to-install-an-operating-system.md) om de taken reeks te maken om het besturings systeem te implementeren. Afhankelijk van de implementatiemethode waarvoor u kiest, kunnen er aanvullende overwegingen zijn bij het samenstellen van de takenreeks.  

##  <a name="deploy"></a><a name="BKMK_Deploy"></a>Zetten  

-   Gebruik een van de volgende implementatiemethoden om het besturingssysteem te implementeren:  

    -   [PXE gebruiken om Windows via het netwerk te implementeren](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Multicast gebruiken om Windows via het netwerk te implementeren](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Een installatiekopie voor een OEM in de fabriek of bij een lokaal depot maken](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Zelfstandige media gebruiken om Windows te implementeren zonder gebruik van het netwerk](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Opstartbare media gebruiken om Windows te implementeren via het netwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Controleren  

-   **De takenreeksimplementatie controleren**  

     Zie [implementaties van besturings systemen](monitor-operating-system-deployments.md)bewaken voor het bewaken van de taken reeks implementatie om het besturings systeem te installeren.  
