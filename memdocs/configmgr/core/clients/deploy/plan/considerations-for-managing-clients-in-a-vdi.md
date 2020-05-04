---
title: VDI-clients beheren
titleSuffix: Configuration Manager
description: Beheer Configuration Manager-clients in een VDI (Virtual Desktop Infrastructure).
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01348695ac5b3b64ca87a9b42aa52ac235b533d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713322"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>Configuration Manager-clients beheren in een virtuele desktop infrastructuur (VDI)

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager ondersteunt de installatie van de Configuration Manager-client in de volgende VDI-scenario's (Virtual Desktop Infrastructure):  

- **Persoonlijke virtuele machines** -persoonlijke virtuele machines worden meestal gebruikt wanneer u ervoor wilt zorgen dat de gebruikers gegevens en-instellingen op de virtuele machine tussen sessies worden bewaard.  

- **Extern bureaublad-services sessies** : extern bureaublad-services kan een server meerdere, gelijktijdige client sessies hosten. Gebruikers kunnen verbinding maken met een sessie en vervolgens toepassingen uitvoeren op die server.  

- **Gegroepeerde** virtuele machines, gegroepeerd, worden niet persistent gemaakt tussen sessies. Wanneer een sessie wordt gesloten, worden alle gegevens en instellingen verwijderd. Gegroepeerde virtuele machines zijn handig wanneer Extern bureaublad-services niet kan worden gebruikt, omdat een vereiste zakelijke toepassing niet kan worden uitgevoerd op de Windows-Server die als host fungeert voor de client sessies.  

  De volgende tabel bevat overwegingen voor het beheren van de Configuration Manager-client in een virtuele-bureaublad infrastructuur.  

|Type virtuele machine|Overwegingen|  
|--------------------------|--------------------|  
|Persoonlijke virtuele machines|Configuration Manager worden persoonlijke virtuele machines op dezelfde manier behandeld als een fysieke computer. De Configuration Manager-client kan vooraf worden geïnstalleerd op de installatie kopie van de virtuele machine of worden geïmplementeerd nadat de virtuele machine is ingericht.|  
|Externe bureaubladservices|De Configuration Manager-client is niet geïnstalleerd voor afzonderlijke Extern bureaublad-sessies. In plaats daarvan wordt de client slechts één keer geïnstalleerd op de Extern bureaublad-services-server. Alle Configuration Manager-functies kunnen worden gebruikt op de Extern bureaublad-services-server.|  
|Gegroepeerde virtuele machines|Wanneer een gegroepeerde virtuele machine buiten gebruik wordt gesteld, gaan alle wijzigingen die u aanbrengt met Configuration Manager verloren.<br /><br /> Gegevens die worden geretourneerd door Configuration Manager functies, zoals hardware-inventaris, software-inventarisatie en software licentie controle zijn mogelijk niet relevant voor uw behoeften, omdat de virtuele machine mogelijk alleen gedurende korte tijd operationeel is. Overweeg gegroepeerde virtuele machines uit inventaris taken uit te sluiten.|  

 Omdat virtualisatie ondersteuning biedt voor het uitvoeren van meerdere Configuration Manager-clients op dezelfde fysieke computer, hebben veel client bewerkingen een ingebouwde wille keurige vertraging voor geplande acties zoals hardware-en software-inventaris, antimalware-scans, software-installaties en software-update scans. Deze vertraging helpt de CPU-verwerking en gegevens overdracht te distribueren voor een computer met meerdere virtuele machines waarop de Configuration Manager-client wordt uitgevoerd.  

> [!NOTE]  
>  Met uitzonde ring van Windows Embedded-clients die zich in de onderhouds modus bevinden, gebruiken Configuration Manager-clients die niet worden uitgevoerd in gevirtualiseerde omgevingen ook deze wille keurige vertraging. Wanneer u veel geïmplementeerde clients hebt, helpt dit gedrag pieken in netwerk bandbreedte te voor komen en vermindert u de vereiste voor CPU-verwerking op de Configuration Manager-site systemen, zoals het beheer punt en de site server. Het interval voor de vertraging is afhankelijk van de Configuration Manager mogelijkheid.  
>   
>  De vertraging voor wille keurigheid is standaard uitgeschakeld voor vereiste software-updates door gebruik te maken van de volgende client instelling: **computer agent**: **wille keurige deadline uitschakelen**.
