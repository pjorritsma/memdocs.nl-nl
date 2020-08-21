---
title: Het besturings systeem van een bestaande computer vernieuwen
titleSuffix: Configuration Manager
description: U kunt verschillende methoden in Configuration Manager gebruiken om een bestaande computer te partitioneren en Format teren en een nieuw besturings systeem op de computer te installeren.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5972f930e0f8026f0ca1004d797bf34605af201e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697837"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Een bestaande computer vernieuwen met een nieuwe versie van Windows

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik Configuration Manager om een bestaande computer te partitioneren en Format teren en vervolgens een nieuw besturings systeem te installeren. Dit proces wordt soms *reimaging* of *wissen en laden*genoemd. Voor dit scenario kiest u uit een groot aantal verschillende implementatie methoden, zoals PXE, opstart bare media of software Center. U kunt ook een status migratie punt gebruiken om instellingen op te slaan en deze vervolgens terug te zetten in het nieuwe besturings systeem.

Zie [scenario's voor het implementeren van ENTER prise-besturings systemen](scenarios-to-deploy-enterprise-operating-systems.md)om het juiste scenario voor de implementatie van het besturings systeem te kiezen.  

## <a name="plan"></a><a name="BKMK_Plan"></a> Fonds  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Infrastructuur vereisten plannen en implementeren

Er zijn verschillende vereisten voor de infra structuur die moeten worden uitgevoerd voordat u een besturings systeem kunt implementeren. Enkele van deze vereisten zijn onder andere de Windows ADK, de Hulpprogramma voor migratie van gebruikersstatus (USMT) en Windows Deployment Services (WDS). Zie [vereisten voor de infra structuur voor besturingssysteem implementatie](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)voor meer informatie.  

### <a name="install-a-state-migration-point"></a>Een status migratie punt installeren

Als u instellingen van een bestaande computer wilt vastleggen en vervolgens de instellingen wilt herstellen naar het nieuwe besturings systeem, overweeg dan het gebruik van een status migratie punt. Zie [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)voor meer informatie.  

## <a name="configure"></a><a name="BKMK_Configure"></a> Geconfigureerd  

### <a name="prepare-a-boot-image"></a>Een opstartinstallatiekopie voorbereiden

Opstart installatie kopieën starten een computer op in een Windows PE-omgeving. Windows PE is een mini maal besturings systeem met beperkte onderdelen en services. In Windows PE kan Configuration Manager vervolgens een volledig Windows-besturings systeem op de computer installeren.

Raadpleeg voor meer informatie de volgende artikelen:

- [Opstartinstallatiekopieën beheren](../get-started/manage-boot-images.md)

- [Opstartinstallatiekopieën aanpassen](../get-started/customize-boot-images.md)

- [Inhoud distribueren](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Een installatie kopie van een besturings systeem voorbereiden

De installatie kopie van het besturings systeem bevat de bestanden die nodig zijn om het besturings systeem op de doel computer te installeren.

Raadpleeg voor meer informatie de volgende artikelen:

- [Installatiekopieën van besturingssysteem beheren](../get-started/manage-operating-system-images.md)

- [Inhoud distribueren](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Een taken reeks maken om een besturings systeem te implementeren

Gebruik een taken reeks om de installatie van het besturings systeem te automatiseren. Afhankelijk van de implementatiemethode waarvoor u kiest, kunnen er aanvullende overwegingen zijn bij het samenstellen van de takenreeks.

Raadpleeg voor meer informatie de volgende artikelen:

- [Een takenreeks maken voor het installeren van een besturingssysteem](create-a-task-sequence-to-install-an-operating-system.md)

- [De gebruikersstatus beheren](../get-started/manage-user-state.md)

## <a name="deploy"></a><a name="BKMK_Deploy"></a> Zetten

- Gebruik een van de volgende implementatie methoden om het besturings systeem te implementeren:  

  - [PXE gebruiken om Windows via het netwerk te implementeren](use-pxe-to-deploy-windows-over-the-network.md)  

  - [Multicast gebruiken om Windows via het netwerk te implementeren](use-multicast-to-deploy-windows-over-the-network.md)  

  - [Een installatiekopie voor een OEM in de fabriek of bij een lokaal depot maken](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

  - [Zelfstandige media gebruiken om Windows te implementeren zonder gebruik van het netwerk](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

  - [Opstartbare media gebruiken om Windows te implementeren via het netwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  

  - [Windows met Software Center via het netwerk implementeren](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Controleren  

Zie [implementaties van besturings systemen bewaken](monitor-operating-system-deployments.md)voor meer informatie.  

> [!Note]
> Wanneer u een installatie kopie van een UEFI-apparaat opnieuw wilt maken, wordt er in Windows Boot Manager een nieuwe vermelding in de opstart lader gemaakt. Dit gedrag is het meest merkbaar wanneer u een apparaat herhaaldelijk opnieuw beveiligt, bijvoorbeeld in een test omgeving of een student Lab. Dit heeft doorgaans geen invloed op de prestaties of het gebruik van het apparaat. Als de lijst te groot wordt, kunnen bepaalde hardwareapparaten problemen ondervinden. Bijvoorbeeld, niet opstarten naar een extern USB-station of kan de huidige opstart vermelding niet selecteren in de lijst. Gebruik de Windows **bcdedit** -opdracht om ongebruikte opstart vermeldingen te wissen. Zie [bcdedit/deletevalue](/windows-hardware/drivers/devtest/bcdedit--deletevalue)voor meer informatie.<!-- 2841926 -->