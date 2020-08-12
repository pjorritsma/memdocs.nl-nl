---
title: BitLocker vooraf inrichten in Windows PE
titleSuffix: Configuration Manager
description: Met de BitLocker-taak vooraf inrichten in Configuration Manager wordt BitLocker vanaf de Windows Preinstallation Environment vóór de implementatie van het besturings systeem ingeschakeld.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9e9acb35354e9962fe838964d3afad0bacceace
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124940"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-configuration-manager"></a>BitLocker vooraf inrichten in Windows PE met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met de taken reeks stap **BitLocker vooraf inrichten** in Configuration Manager kunt u BitLocker inschakelen vanuit de Windows Preinstallation Environment (Windows PE) voorafgaand aan de implementatie van het besturings systeem. Alleen de gebruikte schijfruimte is versleuteld. De versleutelingstijd is daarom veel sneller. Hierbij wordt een willekeurig gegenereerde lege beveiliging toegepast op het geformatteerde volume en wordt het volume voorafgaand aan het Windows-installatieproces versleuteld. De mogelijkheid om BitLocker vooraf in te richten is ingevoerd in Windows 8 en Windows Server 2012. U kunt echter BitLocker vooraf inrichten op een harde schijf en Windows 7 installeren mits u specifieke stappen volgt. Nadat Setup van Windows 7 is voltooid, moet een BitLocker-sleutelbeveiliging worden ingesteld, omdat in het Windows 7 BitLocker-configuratiescherm geen ondersteuning wordt geboden voor BitLocker met een niet-versleutelde sleutelbeveiliging. U moet een sleutelbeveiliging toevoegen met behulp van de stap **BitLocker inschakelen** of met het opdrachtregelprogramma manage-bde.exe.  

 U moet over het algemeen de volgende stappen nemen om BitLocker in te richten op een computer waarop Windows 7 wordt geïnstalleerd:  

- De computer opnieuw opstarten in Windows PE  

  > [!IMPORTANT]  
  >  U moet een opstartinstallatiekopie met Windows PE 4 of hoger gebruiken om BitLocker vooraf in te richten. Zie voor meer informatie over ondersteunde Windows PE-versies in Configuration Manager [afhankelijkheden extern naar Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

- De vaste schijf partitioneren en formatteren  

- BitLocker vooraf inrichten  

- Windows 7 met specifieke besturingssysteem- en netwerkinstellingen installeren  

- Een sleutelbeveiliging aan BitLocker toevoegen  

  In Configuration Manager is de aanbevolen manier om BitLocker vooraf in te richten op een harde schijf en Windows 7 te installeren, het maken van een nieuwe taken reeks en het selecteren van een **bestaand installatie kopie pakket installeren** op de pagina **nieuwe taken reeks** maken van de **wizard taken reeks maken**. De wizard maakt de takenreeksstappen die in de volgende tabel worden vermeld.  

> [!NOTE]  
>  Er zijn mogelijk extra stappen in de takenreeks afhankelijk van hoe de instellingen in de wizard zijn geconfigureerd. U hebt bijvoorbeeld mogelijk de stap **Windows-instellingen vastleggen** als u de optie **Windows-instellingen vastleggen** hebt geselecteerd op de pagina **Statusmigratie** van de wizard.  

|Takenreeksstap|Details|  
|------------------------|-------------|  
|BitLocker uitschakelen|Met deze stap wordt BitLocker-versleuteling uitgeschakeld, als deze momenteel is ingeschakeld. Zie voor meer informatie [Disable BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Computer opnieuw opstarten in Windows PE|Met deze stap wordt de computer opnieuw opgestart in Windows PE door het uitvoeren van de opstartinstallatiekopie die aan de takenreeks is toegewezen. U moet een opstartinstallatiekopie met Windows PE 4 of hoger gebruiken om BitLocker vooraf in te richten. Zie [Restart Computer](../understand/task-sequence-steps.md#BKMK_RestartComputer)voor meer informatie.|  
|Schijf 0 - BIOS partitioneren<br /><br /> Schijf 0 - UEFI partitioneren|Met deze stappen wordt de opgegeven schijf op de doelcomputer met behulp van BIOS of UEFI geformatteerd en gepartitioneerd. De takenreeks maakt gebruik van UEFI wanneer gedetecteerd wordt dat de doelcomputer zich in UEFI-modus bevindt. Zie voor meer informatie [Format and Partition Disk](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|BitLocker vooraf inrichten|Met deze stap wordt BitLocker op een station ingeschakeld in Windows PE. Alleen de gebruikte schijfruimte wordt versleuteld. Versleuteling gaat erg snel omdat de vaste schijf bij de vorige stap is gepartitioneerd en geformatteerd en alle gegevens zijn gewist. Zie voor meer informatie [Pre-provision BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Besturingssysteem toepassen|In deze stap wordt het antwoordbestand voorbereid dat wordt gebruikt bij het installeren van het besturingssysteem op de doelcomputer en wordt de takenreeksvariabele OSDTargetSystemDrive ingesteld op de stationsletter van de partitie die de besturingssysteembestanden bevat. Het antwoordbestand en de variabele worden gebruikt in de Windows-installatie en ConfigMgr-stap om het besturingssysteem te installeren. Zie voor meer informatie [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Windows-instellingen toepassen|In deze stap worden Windows-instellingen aan het antwoordbestand toegevoegd. Het antwoordbestand wordt gebruikt in de Windows-installatie en ConfigMgr-stap om het besturingssysteem te installeren. Zie [Apply Windows Settings](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings)voor meer informatie.|  
|Netwerkinstellingen toepassen|In deze stap worden netwerkinstellingen aan het antwoordbestand toegevoegd. Het antwoordbestand wordt gebruikt in de Windows-installatie en ConfigMgr-stap om het besturingssysteem te installeren. Zie voor meer informatie [Apply Network Settings Step](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Apparaatstuurprogramma's toepassen|In deze stap worden compatibele stuurprogramma's gezocht en geïnstalleerd als onderdeel van de implementatie van het besturingssysteem. Zie voor meer informatie [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Windows en ConfigMgr installeren|In deze stap wordt de overgang van Windows PE naar het nieuwe besturingssysteem uitgevoerd. Deze takenreeksstap is een vereist onderdeel van iedere besturingssysteemimplementatie. De Configuration Manager-client wordt in het nieuwe besturings systeem geïnstalleerd en bereidt de taken reeks voor op uitvoering in het nieuwe besturings systeem. Zie [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)voor meer informatie.|  
|BitLocker inschakelen|In deze stap wordt BitLocker-versleuteling op de vaste schijf ingeschakeld en de sleutelbeveiligingen ingesteld. Deze stap verloopt erg snel omdat de vaste schijf vooraf is ingericht met BitLocker. Windows 7 vereist dat u een sleutelbeveiliging toevoegt. Als u deze stap niet uitvoert, kunt u het opdrachtregelprogramma manage-bde.exe uitvoeren om een sleutelbeveiliging in te stellen. Zie [Enable BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker)voor meer informatie.|  
