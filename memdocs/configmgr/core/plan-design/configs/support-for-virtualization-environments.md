---
title: Ondersteuning voor virtualisatie
titleSuffix: Configuration Manager
description: De vereisten voor het installeren van Configuration Manager client-en site systeem rollen in een Virtualization-omgeving.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2e266373667efebccdb84fe743f66beeaa5a0e88
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709591"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Ondersteuning voor virtualisatie-omgevingen met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager ondersteunt het installeren van de client en site systeem rollen op ondersteunde besturings systemen die worden uitgevoerd als een virtuele machine in de Virtualization-omgevingen in dit artikel. Deze ondersteuning bestaat zelfs wanneer de virtuele-machinehost (Virtualization Environment) niet wordt ondersteund als een client of site server.  

U kunt bijvoorbeeld Microsoft Hyper-V Server 2012 gebruiken om een virtuele machine te hosten waarop Windows Server 2012 wordt uitgevoerd. U kunt de client-of site systeem rollen installeren op de virtuele machine met Windows Server 2012. U kunt de client niet installeren op de host met Microsoft Hyper-V Server 2012.  

## <a name="virtualization-environments"></a>Virtualisatiemogelijkheden

- Windows Server 2019  
- Windows Server 2016 <sup> [Opmerking 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Opmerking 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

### <a name="note-1-nested-virtualization"></a><a name="bkmk_note1"></a>Opmerking 1: geneste virtualisatie

Configuration Manager biedt geen ondersteuning voor [geneste virtualisatie](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), wat nieuw is in Windows Server 2016.

### <a name="virtualization-environment-support"></a>Ondersteuning van de Virtualization Environment

Elke virtuele computer moet dezelfde of meer hardware-en software vereisten hebben die u zou gebruiken voor een fysieke Configuration Manager computer.  

Als u wilt controleren of uw virtualisatieserver wordt ondersteund voor Configuration Manager, gebruikt u het validatie programma voor Server-virtualisatie. Het bevat een ondersteunings beleid voor het programma voor online-virtualisatie. Zie [validatie programma voor Windows Server-virtualisatie](https://www.windowsservercatalog.com/svvp.aspx)voor meer informatie.  

> [!NOTE]  
> Configuration Manager biedt geen ondersteuning voor virtuele-PC-of Virtual Server-gast besturingssystemen die worden uitgevoerd op Mac-computers.  

Configuration Manager kan geen virtuele machines beheren als ze offline zijn. Een installatie kopie van een virtuele machine die offline is, kan niet worden bijgewerkt en kan niet worden verzameld met behulp van de Configuration Manager-client op de hostcomputer.  

Er wordt geen speciale aandacht besteed aan virtuele machines. Configuration Manager kan bijvoorbeeld niet bepalen of een update opnieuw moet worden toegepast op een installatie kopie van een virtuele machine als de virtuele machine is gestopt en opnieuw is opgestart zonder dat de status van de virtuele machine waarop de update is toegepast, wordt opgeslagen.  

##  <a name="microsoft-azure-virtual-machines"></a><a name="bkmk_Azure"></a> Virtuele Microsoft Azure-machines  

Configuration Manager kunnen worden uitgevoerd op virtuele machines in azure, net zoals het on-premises wordt uitgevoerd binnen uw Data Center. Gebruik Configuration Manager met virtuele Azure-machines in de volgende scenario's:  

- **Scenario 1**: Voer Configuration Manager uit op een virtuele machine van Azure. Gebruik het om clients te beheren op andere virtuele machines van Azure.  

- **Scenario 2**: Voer Configuration Manager uit op een virtuele machine van Azure. Gebruik het om clients te beheren die niet worden uitgevoerd op Azure.  

- **Scenario 3**: verschillende Configuration Manager site systeem rollen uitvoeren op virtuele machines van Azure. Voer andere rollen uit in uw on-premises Data Center, op de juiste manier verbonden met Azure.  

Dezelfde Configuration Manager vereisten voor netwerken, ondersteunde configuraties en hardwarevereisten die van toepassing zijn op on-premises installatie, zijn ook van toepassing op virtuele machines van Azure.  

Zie [Configuration Manager op Azure](../../understand/configuration-manager-on-azure.md)voor meer informatie.

> [!IMPORTANT]  
> Configuration Manager-sites en-clients die worden uitgevoerd op virtuele Azure-machines gelden dezelfde licentie vereisten als voor on-premises installaties.  

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Virtueel bureau blad van Windows](https://docs.microsoft.com/azure/virtual-desktop/) is een preview-functie van Microsoft Azure en Microsoft 365. Vanaf versie 1906 gebruikt u Configuration Manager voor het beheren van deze virtuele apparaten waarop Windows wordt uitgevoerd in Azure. Zie [ondersteunde besturings systemen voor clients en apparaten](supported-operating-systems-for-clients-and-devices.md)voor meer informatie.
