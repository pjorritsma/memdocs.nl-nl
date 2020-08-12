---
title: Ondersteuning voor virtualisatie
titleSuffix: Configuration Manager
description: De vereisten voor het installeren van Configuration Manager client-en site systeem rollen in een Virtualization-omgeving.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f7d774d620916f3d735a3545db5fe1e41988731d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126678"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Ondersteuning voor virtualisatie-omgevingen met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager ondersteunt het installeren van de client en site systeem rollen op ondersteunde besturings systemen die worden uitgevoerd als een virtuele machine (VM) in bepaalde virtualisatiemogelijkheden. Deze ondersteuning bestaat zelfs wanneer de virtuele host (Virtualization Environment) niet wordt ondersteund als een client of site server.

U kunt bijvoorbeeld Microsoft Hyper-V Server 2016 gebruiken om een VM te hosten waarop Windows Server 2019 wordt uitgevoerd. U kunt de client-of site systeem rollen installeren op de virtuele machine met Windows Server 2019. U kunt de client niet installeren op de host met Microsoft Hyper-V Server 2016.

## <a name="virtualization-environments"></a>Virtualisatiemogelijkheden

- Windows Server 2019  
- Windows Server 2016 <sup> [Opmerking 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [Opmerking 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  

<a name="bkmk_note1"></a>

> [!NOTE]
> Configuration Manager biedt geen ondersteuning voor [geneste virtualisatie](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#nested-virtualization-new), wat nieuw is in Windows Server 2016.

### <a name="virtualization-environment-support"></a>Ondersteuning van de Virtualization Environment

Elke virtuele computer moet dezelfde of meer hardware-en software vereisten hebben die u zou gebruiken voor een fysieke Configuration Manager computer.

Als u wilt valideren dat Configuration Manager de virtualisatie-omgeving ondersteunt, gebruikt u het validatie programma voor Server-virtualisatie. Het bevat een ondersteunings beleid voor het programma voor online-virtualisatie. Zie [validatie programma voor Windows Server-virtualisatie](https://www.windowsservercatalog.com/svvp.aspx)voor meer informatie.

Configuration Manager kan geen Vm's beheren als ze offline zijn. De Configuration Manager-client op de hostcomputer kan geen offline-VM-installatie kopie beheren. Dit kan bijvoorbeeld geen software-updates installeren of hardware-inventaris verzamelen.

Over het algemeen biedt Configuration Manager geen speciale aandacht voor Vm's. Als u bijvoorbeeld een virtuele machine stopt en de status niet opslaat, kan Configuration Manager mogelijk niet bepalen of een software-update opnieuw moet worden geïnstalleerd.

Voor hulp bij de Configuration Manager client prestaties in virtuele omgevingen die ondersteuning bieden voor meerdere gebruikers sessies, wordt het gebruikers beleid standaard uitgeschakeld. Vanaf versie 1910 kunt u het gebruikers beleid inschakelen in dit scenario. Zie voor meer informatie [over client instellingen-gebruikers beleid inschakelen voor meerdere gebruikers sessies](../../clients/deploy/about-client-settings.md#enable-user-policy-for-multiple-user-sessions).

## <a name="microsoft-azure-vms"></a><a name="bkmk_Azure"></a>Microsoft Azure Vm's

Configuration Manager kunnen worden uitgevoerd op virtuele machines in azure, net zoals het on-premises wordt uitgevoerd binnen uw Data Center. Gebruik Configuration Manager met Azure-Vm's in de volgende scenario's:

- **Scenario 1**: Voer Configuration Manager uit op een virtuele Azure-machine. Gebruik het om clients te beheren op andere virtuele machines van Azure.

- **Scenario 2**: Voer Configuration Manager uit op een virtuele Azure-machine. Gebruik het om clients te beheren die niet worden uitgevoerd op Azure.

- **Scenario 3**: verschillende Configuration Manager site systeem rollen uitvoeren op virtuele Azure-machines. Voer andere rollen uit in uw on-premises Data Center, op de juiste manier verbonden met Azure.

Dezelfde Configuration Manager vereisten voor netwerken, ondersteunde configuraties en hardwarevereisten gelden ook voor virtuele Azure-machines.

Zie [Configuration Manager op Azure](../../understand/configuration-manager-on-azure.md)voor meer informatie.

> [!IMPORTANT]
> Configuration Manager-sites en-clients die worden uitgevoerd op virtuele Azure-machines gelden dezelfde licentie vereisten als voor on-premises installaties.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

[Virtueel bureau blad van Windows](https://docs.microsoft.com/azure/virtual-desktop/) is een desktop-en app Virtualization-service die wordt uitgevoerd op Microsoft Azure. Vanaf versie 1906 gebruikt u Configuration Manager voor het beheren van deze virtuele apparaten waarop Windows wordt uitgevoerd in Azure. Zie [ondersteunde besturings systemen voor clients en apparaten](supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Configuration Manager-clients beheren in een virtuele desktop infrastructuur (VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)