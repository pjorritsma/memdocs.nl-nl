---
title: BitLocker-gebeurtenislogboeken
titleSuffix: Configuration Manager
description: Meer informatie over het werken met BitLocker-informatie in het Windows-gebeurtenis logboek om problemen op te lossen
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: troubleshooting
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef1d5f9a7e8f3c009d1993b82ddef22ce22e235d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127998"
---
# <a name="bitlocker-event-logs"></a>BitLocker-gebeurtenislogboeken

*Van toepassing op: Configuration Manager (huidige vertakking)*

De BitLocker-beheer agent en Web Services gebruiken Windows-gebeurtenis Logboeken om berichten op te nemen. Ga in het Logboeken naar de **Logboeken toepassingen en services**, **micro soft**, **Windows**. Het logboek kanaal (knoop punt) varieert afhankelijk van de computer en het onderdeel:

- **MBAM**: BitLocker-beheer agent op een client computer
- **MBAM-Web**:
  - Herstel service op het beheer punt
  - Selfservice portal
  - Website voor beheer en controle

Raadpleeg de volgende artikelen voor meer informatie over specifieke berichten in deze logboeken:

- [Clientgebeurtenislogboeken](client-event-logs.md)
- [Servergebeurtenislogboeken](server-event-logs.md)

In elk knoop punt ziet u standaard twee logboek kanalen: **beheerder** en **operationeel**. Voor meer gedetailleerde informatie over probleem oplossing kunt u ook [Logboeken voor analyse en fout opsporing](#bkmk_debug)weer geven.

## <a name="log-properties"></a>Logboek eigenschappen

Selecteer een specifiek logboek in Windows Logboeken. Bijvoorbeeld **beheerder**. Ga naar het **actie** menu en selecteer **Eigenschappen**. Configureer de volgende instellingen:

- **Maximale logboek grootte (KB)**: standaard is deze instelling `1028` (1 MB) voor alle logboeken.
- **Als de maximale grootte van het gebeurtenis logboek is bereikt**: standaard worden de **beheerder** en de **operationele** logboeken zo ingesteld dat **gebeurtenissen indien nodig worden overschreven (oudste gebeurtenissen eerst)**.

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a>Logboeken voor analyse en fout opsporing

U kunt gedetailleerdere logboeken inschakelen voor het oplossen van problemen. Ga in Logboeken naar het menu **weer gave** en selecteer **analyseren en logboeken voor fout opsporing weer geven**. Wanneer u nu naar het logboek kanaal bladert, ziet u twee extra logboeken: **analyse** en **fout opsporing**.

> [!TIP]
> Standaard hebben deze logboeken de volgende eigenschappen:
>
> - **Maximale logboek grootte (KB)**: `1028` (1 MB)
> - **Gebeurtenissen niet overschrijven (logboeken hand matig Wissen)**

## <a name="export-logs-to-text"></a>Logboeken naar tekst exporteren

Met name bij de [Logboeken analyse en fout opsporing](#bkmk_debug)kunt u de logboek vermeldingen gemakkelijker bekijken in één tekst bestand. Gebruik de volgende Power shell-opdrachten om de vermeldingen in het gebeurtenis logboek te exporteren naar tekst bestanden:

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
