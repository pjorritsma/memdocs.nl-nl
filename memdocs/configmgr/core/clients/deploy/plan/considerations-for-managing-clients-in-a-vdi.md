---
title: VDI-clients beheren
titleSuffix: Configuration Manager
description: Beheer Configuration Manager-clients in een VDI (Virtual Desktop Infrastructure).
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d79edb5ad1a60c5876163281ec5c1d1c17eff0a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692805"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Configuration Manager-clients beheren in een virtuele desktop infrastructuur (VDI)

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager ondersteunt de installatie van de Configuration Manager-client in de volgende VDI-scenario's (Virtual Desktop Infrastructure):

- **Persoonlijke virtuele machines**: de virtuele machine (VM) houdt gebruikers gegevens en instellingen tussen sessies bij.

- **Extern bureaublad-services sessies**: host meerdere, gelijktijdige client sessies op een gecentraliseerde server. Gebruikers maken verbinding met een sessie en voeren toepassingen uit op die server.

- **Gegroepeerde virtuele machines**: de virtuele machine blijft niet behouden tussen sessies. Wanneer een gebruiker een sessie sluit, worden alle gegevens en instellingen verwijderd. Gegroepeerde virtuele machines zijn handig wanneer u Extern bureaublad-services niet kunt gebruiken. Bijvoorbeeld als een vereiste toepassing niet kan worden uitgevoerd op de Windows-Server die als host fungeert voor de client sessies.

- **Virtueel bureau blad van Windows**: een desktop-en app Virtualization-service die wordt uitgevoerd op Microsoft Azure. Vanaf versie 1906 gebruikt u Configuration Manager voor het beheren van deze virtuele apparaten waarop Windows wordt uitgevoerd in Azure.

## <a name="personal-vms"></a>Persoonlijke Vm's

Configuration Manager worden persoonlijke Vm's behandeld als een fysieke computer. U kunt de Configuration Manager-client vooraf installeren op de VM-installatie kopie of nadat u deze hebt ingericht.

Zie [ondersteuning voor virtualisatie omgevingen](../../../plan-design/configs/support-for-virtualization-environments.md)voor meer informatie.

## <a name="remote-desktop-services"></a>Externe bureaubladservices

U installeert de Configuration Manager-client niet voor afzonderlijke Extern bureaublad-sessies. Installeer het eenmaal op de server die als host fungeert voor Extern bureaublad-services. U kunt alle Configuration Manager-client functies op de Extern bureaublad-services-server gebruiken.

Zie [Welkom bij extern bureaublad-services](/windows-server/remote/remote-desktop-services/welcome-to-rds)voor meer informatie.

## <a name="pooled-vms"></a>Gegroepeerde Vm's

Wanneer u een gegroepeerde virtuele machine buiten gebruik stelt, gaan alle wijzigingen die zijn aangebracht door Configuration Manager verloren.

Omdat de virtuele machine gedurende korte tijd alleen operationeel kan zijn, retour neren sommige Configuration Manager functies mogelijk geen relevante gegevens. Bijvoorbeeld hardware-inventaris, software-inventarisatie en software licentie controle. Overweeg gegroepeerde virtuele machines uit inventaris taken uit te sluiten.

## <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

Zie [ondersteunde besturings systemen voor clients en apparaten](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)voor meer informatie.

## <a name="other-considerations"></a>Andere overwegingen

Omdat virtualisatie ondersteuning biedt voor het uitvoeren van meerdere Configuration Manager-clients op dezelfde fysieke computer, hebben veel client bewerkingen een ingebouwde wille keurige vertraging voor geplande acties. Bijvoorbeeld hardware-en software-inventaris, antimalware-scans, software-installaties en software-update scans. Deze vertraging helpt de CPU-verwerking en gegevens overdracht te distribueren voor een server met meerdere virtuele machines waarop de Configuration Manager-client wordt uitgevoerd.

Behalve voor Windows Embedded-clients in de onderhouds modus, gebruiken Configuration Manager clients in gevirtualiseerde omgevingen ook deze wille keurige vertraging. Dit gedrag helpt pieken in de netwerk bandbreedte te voor komen. Het vermindert ook de CPU-verwerking op site systemen, zoals het beheer punt en de site server. Het interval voor de vertraging is afhankelijk van de Configuration Manager mogelijkheid. Zie bijvoorbeeld [about client settings-deadline wille keurigheid uitschakelen](../about-client-settings.md#disable-deadline-randomization).

Voor hulp bij de Configuration Manager client prestaties in virtuele omgevingen die ondersteuning bieden voor meerdere gebruikers sessies, wordt het gebruikers beleid standaard uitgeschakeld. Vanaf versie 1910 kunt u het gebruikers beleid inschakelen in dit scenario. Zie voor meer informatie [over client instellingen-gebruikers beleid inschakelen voor meerdere gebruikers sessies](../about-client-settings.md#enable-user-policy-for-multiple-user-sessions).