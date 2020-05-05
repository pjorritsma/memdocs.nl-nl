---
title: Takenreeksstappen voor het beheren van de conversie van BIOS naar UEFI
titleSuffix: Configuration Manager
description: Meer informatie over het aanpassen van een taken reeks voor het implementeren van besturings systemen om een FAT32-partitie voor te bereiden voor overgang naar UEFI.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9183efd622cb425027500d3fe51ed7b86d3a94e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079362"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Takenreeksstappen voor het beheren van de conversie van BIOS naar UEFI
Windows 10 biedt veel nieuwe beveiligings functies waarvoor UEFI-apparaten zijn vereist. Mogelijk hebt u moderne Windows-Pc's die ondersteuning bieden voor UEFI, maar gebruikmaken van een verouderd BIOS. Als u een apparaat omzet in UEFI, moet u naar elke PC gaan, de harde schijf opnieuw partitioneren en de firmware opnieuw configureren. Met behulp van taken reeksen in Configuration Manager kunt u een harde schijf voorbereiden voor de conversie van BIOS naar UEFI, het converteren van BIOS naar UEFI als onderdeel van het in-place upgrade proces en UEFI-gegevens verzamelen als onderdeel van de hardware-inventaris.

## <a name="hardware-inventory-collects-uefi-information"></a>De hardware-inventaris verzamelt UEFI-gegevens
Vanaf versie 1702 is een nieuwe hardware-inventaris klasse (**SMS_Firmware**) en-eigenschap (**UEFI**) beschikbaar om u te helpen bepalen of een computer in de UEFI-modus wordt gestart. Wanneer een computer in de UEFI-modus wordt gestart, wordt de eigenschap **UEFI** ingesteld op **True**. Dit is standaard ingeschakeld in Hardware-inventarisatie. Zie [hardware-inventaris configureren](../../core/clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over hardware-inventarisatie.

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Een aangepaste taken reeks maken om de vaste schijf voor te bereiden voor de conversie van BIOS naar UEFI
Vanaf Configuration Manager versie 1610 kunt u nu een taken reeks voor besturingssysteem implementatie aanpassen met een nieuwe variabele, TSUEFIDrive, zodat de stap **computer opnieuw opstarten** een FAT32-partitie op de harde schijf voorbereidt voor overgang naar UEFI. De volgende procedure bevat een voor beeld van hoe u taken reeks stappen kunt maken om de harde schijf voor te bereiden voor de conversie van BIOS naar UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Voor bereiding van de FAT32-partitie voor de conversie naar UEFI:
In een bestaande taken reeks om een besturings systeem te installeren, voegt u een nieuwe groep toe met stappen om de conversie van het BIOS naar UEFI uit te voeren.

1. Maak een nieuwe taken reeks groep na de stappen voor het vastleggen van bestanden en instellingen en vóór de stappen voor het installeren van het besturings systeem. U kunt bijvoorbeeld een groep maken na de **opname bestanden en instellingen groep met** de naam **BIOS-naar-UEFI**.
2. Voeg op het tabblad **Opties** van de nieuwe groep een nieuwe taken reeks variabele toe als een voor waarde **_SMSTSBootUEFI** waarbij _SMSTSBootUEFI **niet gelijk** is aan **waar**. Zo voor komt u dat de stappen in de groep worden uitgevoerd wanneer een computer zich al in de UEFI-modus bevindt.

   ![Groep BIOS naar UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Voeg onder de nieuwe groep de taken reeks stap **computer opnieuw opstarten** toe. In **opgeven wat moet worden uitgevoerd na het opnieuw opstarten**, selecteert u **de opstart installatie kopie die is toegewezen aan deze taken reeks wordt geselecteerd** om de computer te starten in Windows PE.  
4. Voeg op het tabblad **Opties** een taken reeks variabele toe als een voor waarde waarbij **_SMSTSInWinPE gelijk is aan False**. Dit voor komt dat deze stap wordt uitgevoerd als de computer al aanwezig is in Windows PE.

   ![Computer stap opnieuw opstarten](../../core/get-started/media/restart-in-windows-pe.png)
5. Voeg een stap toe om het OEM-hulp programma te starten waarmee de firmware wordt geconverteerd van BIOS naar UEFI. Dit is doorgaans een taken reeks stap **opdracht regel uitvoeren** met een opdracht regel om het OEM-hulp programma te starten.
6. Voeg de taken reeks stap schijf Format teren en partitioneren toe voor het partitioneren en Format teren van de harde schijf. In de stap gaat u als volgt te werk:
   1. Maak de FAT32-partitie die wordt geconverteerd naar UEFI voordat het besturings systeem wordt geïnstalleerd. Kies **GPT** voor het **schijf type**.
    ![Schijf stap Format teren en partitioneren](../media/format-and-partition-disk.png)
   2. Ga naar de eigenschappen van de FAT32-partitie. Voer **TSUEFIDrive** in het veld **variabele** in. Wanneer de taken reeks deze variabele detecteert, wordt de UEFI-overgang voor bereid voordat de computer opnieuw wordt opgestart.
    ![Partitie-eigenschappen](../../core/get-started/media/partition-properties.png)
   3. Maak een NTFS-partitie die wordt gebruikt door de taken reeks Engine om de status op te slaan en logboek bestanden op te slaan.
7. Voeg de taken reeks stap **computer opnieuw opstarten** toe. In **opgeven wat moet worden uitgevoerd na het opnieuw opstarten**, selecteert u **de opstart installatie kopie die is toegewezen aan deze taken reeks wordt geselecteerd** om de computer te starten in Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversie van BIOS naar UEFI tijdens een in-place upgrade
In de update voor Windows 10 Crea tors wordt een eenvoudig conversie programma geïntroduceerd waarmee het proces voor het opnieuw partitioneren van de harde schijf voor UEFI-hardware wordt geautomatiseerd en het conversie programma wordt geïntegreerd in het Windows 7-in-place upgrade proces. Wanneer u dit hulp programma combineert met de taken reeks voor de upgrade van het besturings systeem en het OEM-hulp programma dat de firmware converteert van BIOS naar UEFI, kunt u uw computers converteren van BIOS naar UEFI tijdens een in-place upgrade naar de update voor Windows 10 Crea tors.

**Vereisten**:
- Update voor Windows 10 Crea tors
- Computers die ondersteuning bieden voor UEFI
- OEM-hulp programma dat de firmware van de computer converteert van BIOS naar UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversie van BIOS naar UEFI tijdens een in-place upgrade
1. Maak een upgrade taken reeks van een besturings systeem waarmee een in-place upgrade wordt uitgevoerd voor de update van Windows 10-makers.
2. Bewerk de taken reeks. Voeg in de groep die moet worden **verwerkt**de volgende taken reeks stappen toe:
   1. Voeg vanuit algemeen een **Run-opdracht regel** stap toe. U voegt de opdracht regel voor het hulp programma MBR2GPT toe waarmee een schijf wordt omgezet van MBR naar GPT zonder gegevens van de schijf te wijzigen of te verwijderen. Typ het volgende in de opdracht regel: **MBR2GPT/Convert/disk: 0/AllowFullOS**. U kunt er ook voor kiezen om de MBR2GPT uit te voeren. EXE-hulp programma in Windows PE in plaats van in het volledige besturings systeem. U kunt dit doen door een stap toe te voegen om de computer opnieuw op te starten in WinPE vóór de stap voor het uitvoeren van de MBR2GPT. EXE-hulp programma en verwijdert u de optie/AllowFullOS van de opdracht regel. Zie MBR2GPT voor meer informatie over het hulp programma en de beschik bare opties [. EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Voeg een stap toe om het OEM-hulp programma te starten waarmee de firmware wordt geconverteerd van BIOS naar UEFI. Dit is doorgaans een taken reeks stap opdracht regel uitvoeren met een opdracht regel om het OEM-hulp programma te starten.
   3. Voeg in het algemeen de stap **computer opnieuw opstarten** toe. Als u wilt opgeven wat moet worden uitgevoerd na het opnieuw opstarten, selecteert u **het momenteel geïnstalleerde standaard besturings systeem**.
3. Implementeer de taken reeks.
