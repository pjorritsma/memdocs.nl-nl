---
title: BIOS converteren naar UEFI
titleSuffix: Configuration Manager
description: Meer informatie over het aanpassen van een implementatie taken reeks van een besturings systeem om een FAT32-partitie voor te bereiden voor overgang naar UEFI.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 761270fe9419330e2d60d0483554ee6c932c1b26
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124882"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Takenreeksstappen voor het beheren van de conversie van BIOS naar UEFI

Windows 10 biedt veel nieuwe beveiligings functies waarvoor UEFI-apparaten zijn vereist. Mogelijk hebt u nieuwere Windows-apparaten die ondersteuning bieden voor UEFI, maar gebruikmaken van verouderde BIOS. Voorheen moest u naar elk apparaat gaan, de harde schijf opnieuw partitioneren en de firmware opnieuw configureren, zodat u een apparaat naar UEFI kunt converteren.

Met Configuration Manager kunt u de volgende acties automatiseren:

- Een harde schijf voorbereiden voor de conversie van BIOS naar UEFI
- Converteren van BIOS naar UEFI als onderdeel van het in-place upgrade proces
- UEFI-informatie verzamelen als onderdeel van hardware-inventaris

## <a name="hardware-inventory-collects-uefi-information"></a>De hardware-inventaris verzamelt UEFI-gegevens

De hardware-inventaris klasse (**SMS_Firmware**) en de eigenschap (**UEFI**) zijn beschikbaar om u te helpen bepalen of een computer in de UEFI-modus wordt gestart. Wanneer een computer in de UEFI-modus wordt gestart, wordt de eigenschap **UEFI** ingesteld op **True**. Deze klasse wordt standaard door de hardware-inventarisatie ingeschakeld. Zie [hardware-inventaris configureren](../../core/clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over hardware-inventarisatie.

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive"></a>Een aangepaste taken reeks maken om de harde schijf voor te bereiden

U kunt een implementatie taken reeks van een besturings systeem aanpassen met de variabele **TSUEFIDrive** . Met de stap **computer opnieuw opstarten** wordt een FAT32-partitie op de harde schijf voor bereid voor overgang naar UEFI. De volgende procedure bevat een voor beeld van hoe u taken reeks stappen kunt maken om deze actie uit te voeren.

### <a name="prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>De FAT32-partitie voorbereiden voor de conversie naar UEFI

In een bestaande taken reeks om een besturings systeem te installeren, voegt u een nieuwe groep toe met stappen om de conversie van BIOS naar UEFI uit te voeren.

1. Maak een nieuwe taken reeks groep na de stappen voor het vastleggen van bestanden en instellingen en vóór de stappen voor het installeren van het besturings systeem. U kunt bijvoorbeeld een groep maken na de **opname bestanden en instellingen groep met** de naam **BIOS-naar-UEFI**.

1. Voeg op het tabblad **Opties** van de nieuwe groep een nieuwe taken reeks variabele toe als een voor waarde. Set **_SMSTSBootUEFI niet gelijk aan waar**. Met deze voor waarde voert de taken reeks deze stappen alleen op BIOS-apparaten uit.

    :::image type="content" source="media/bios-to-uefi-group.png" alt-text="Voor waarde voor de groep BIOS naar UEFI":::

1. Voeg onder de nieuwe groep de taken reeks stap **computer opnieuw opstarten** toe. In **opgeven wat moet worden uitgevoerd na het opnieuw opstarten**, selecteert u **de opstart installatie kopie die is toegewezen aan deze taken reeks is geselecteerd**. Met deze actie wordt de computer opnieuw opgestart in Windows PE.

1. Voeg op het tabblad **Opties** een taken reeks variabele toe als een voor waarde. Set **_SMSTSInWinPE is gelijk aan False**. Met deze voor waarde wordt deze stap niet uitgevoerd door de taken reeks als de computer al aanwezig is in Windows PE.

    :::image type="content" source="media/restart-in-windows-pe.png" alt-text="Voor waarde bij computer opnieuw opstarten":::

1. Voeg een stap toe om een OEM-hulp programma te starten en de firmware te converteren van BIOS naar UEFI. Normaal gesp roken voert u de **opdracht regel uit**met de opdracht om het OEM-hulp programma uit te voeren.

1. Voeg de taken reeks stap **schijf Format teren en partitioneren** toe. In deze stap configureert u de volgende opties:

    1. Maak de FAT32-partitie om te converteren naar UEFI voordat het besturings systeem wordt geïnstalleerd. Kies **GPT**voor **schijf type**.

        :::image type="content" source="media/format-and-partition-disk.png" alt-text="De configuratie van de schijf voor Format teren en partitioneren":::

    1. Ga naar de eigenschappen van de FAT32-partitie. Voer in het veld **variabele** in `TSUEFIDrive` . Wanneer de taken reeks deze variabele detecteert, wordt de partitie voor de UEFI-overgang voor bereid voordat de computer opnieuw wordt opgestart.

        :::image type="content" source="media/partition-properties.png" alt-text="Configuratie van eigenschappen van FAT32-partitie":::

    1. Een NTFS-partitie maken die door de taken reeks wordt gebruikt om de status op te slaan en logboek bestanden op te slaan.

1. Een andere taken reeks stap **computer opnieuw opstarten** toevoegen. In **opgeven wat moet worden uitgevoerd na het opnieuw opstarten**, selecteert u **de opstart installatie kopie die is toegewezen aan deze taken reeks wordt geselecteerd** om de computer te starten in Windows PE.

    > [!TIP]
    > De EFI-partitie grootte is standaard 500 MB. In sommige omgevingen is de opstart installatie kopie te groot om op deze partitie op te slaan. U kunt dit probleem omzeilen door de grootte van de EFI-partitie te verg Roten. Stel de waarde bijvoorbeeld in op 1 GB.<!-- SCCMDocs#1024 -->

## <a name="convert-from-bios-to-uefi-during-in-place-upgrade"></a><a name="bkmk_ipu"></a>Converteren van BIOS naar UEFI tijdens in-place upgrade

Windows 10 bevat een eenvoudig conversie programma, **MBR2GPT**. Het proces voor het opnieuw partitioneren van de harde schijf voor UEFI-hardware wordt geautomatiseerd. U kunt het conversie programma integreren in het in-place upgrade-proces naar Windows 10. Combi neer dit hulp programma met uw upgrade taken reeks en het OEM-hulp programma dat de firmware converteert van BIOS naar UEFI.

### <a name="requirements"></a>Vereisten

- Een ondersteunde versie van Windows 10
- Computers die ondersteuning bieden voor UEFI
- OEM-hulp programma dat de firmware van de computer converteert van BIOS naar UEFI

### <a name="process-to-convert-from-bios-to-uefi-during-an-in-place-upgrade-task-sequence"></a>Proces voor conversie van BIOS naar UEFI tijdens een in-place upgrade taken reeks

1. [Een takenreeks maken voor het bijwerken van een besturingssysteem](create-a-task-sequence-to-upgrade-an-operating-system.md)

1. Bewerk de taken reeks. Breng de volgende wijzigingen aan in de groep **na verwerking** :

    1. Voeg de stap **opdracht regel uitvoeren** toe. Geef de opdracht regel op voor het hulp programma MBR2GPT. Wanneer u uitvoert in het volledige besturings systeem, moet u deze configureren om de schijf van MBR naar GPT te converteren zonder gegevens te wijzigen of te verwijderen. Voer de volgende opdracht in op de **opdracht regel**:`MBR2GPT.exe /convert /disk:0 /AllowFullOS`

    > [!TIP]
    > U kunt er ook voor kiezen om het MBR2GPT.EXE-hulp programma uit te voeren in plaats van in het volledige besturings systeem in Windows PE. Voeg een stap toe om de computer opnieuw op te starten in Windows PE voordat de stap wordt uitgevoerd om het MBR2GPT.EXE-hulp programma uit te voeren. Verwijder vervolgens de optie **/AllowFullOS** van de opdracht regel.

    Zie [MBR2GPT.EXE](https://docs.microsoft.com/windows/deployment/mbr-to-gpt)voor meer informatie over het hulp programma en de beschik bare opties.

    1. Voeg een stap toe om het OEM-hulp programma uit te voeren dat de firmware converteert van BIOS naar UEFI. Deze stap wordt doorgaans **uitgevoerd**met een opdracht regel om het OEM-hulp programma uit te voeren.

    1. Voeg de stap **computer opnieuw opstarten** toe en selecteer **het momenteel geïnstalleerde standaard besturings systeem**.

1. Implementeer de taken reeks.
