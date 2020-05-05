---
title: Logboekverzamelaar
titleSuffix: Configuration Manager
description: Het hulp programma Logboeken verzamelaar gebruiken om problemen met Desktop Analytics op te lossen
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 349b2a69-af46-481f-afb2-24d98774e852
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c101e45eb794ff73599e9612a5aec991be01ae6c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718880"
---
# <a name="desktop-analytics-log-collector"></a>Logboek verzamelaar van Desktop Analytics

Vanaf Configuration Manager versie 1906, gebruikt u het hulp programma **DesktopAnalyticsLogsCollector. ps1** van de installatiemap van Configuration Manager om problemen met de registratie van het apparaat voor desktop Analytics op te lossen. Er worden enkele basis stappen voor probleem oplossing uitgevoerd en de relevante logboeken worden in één werkmap verzameld. U kunt deze inhoud delen met micro soft ondersteuning.


## <a name="prerequisites"></a>Vereisten

- Een desktop Analytics-client met Windows 10, Windows 8,1 of Windows 7 met Service Pack 1

- Voer het script uit op het apparaat als gebruiker met beheerders rechten en **Voer als Administrator uit**.

    > [!Tip]
    > U kunt de functie Configuration Manager **scripts** gebruiken met dit hulp programma. Zie [voor beeld 5: script implementeren via Configuration Manager **scripts**](#bkmk_ex5)voor meer informatie.

- Voor Windows 7 met Service Pack 1, Power shell versie 4,0 of hoger
    - [.NET Framework versie 4,6 of hoger](https://dotnet.microsoft.com/download/dotnet-framework)

    - Windows Management Framework [versie 4,0](https://support.microsoft.com/help/2819745) (aka.MS/wmf4download) of [versie 5,1](https://www.microsoft.com/download/details.aspx?id=54616) (aka.MS/wmf5download)

## <a name="usage"></a>Gebruik

Het script ophalen uit de inhoud van de Configuration Manager-installatie:`SMSSETUP\TOOLS\DesktopAnalyticsLogsCollector\DesktopAnalyticsLogsCollector.ps1`

``` Syntax
DesktopAnalyticsLogsCollector.ps1
    [-LogPath] <String>
    [-LogMode] <Int16>
    [-CollectNetTrace] <Int16>
    [-CollectUTCTrace] <Int16>
```

## <a name="parameters"></a>Parameters

### `-LogPath`

Hiermee geeft u een lokaal of UNC-pad op voor het opslaan van het logboek en andere uitvoer bestanden.

**Waarden**:

- Lokaal pad (maximum lengte = 130), bijvoorbeeld:`c:\myfolder`

- UNC-pad (maximum lengte = 130), bijvoorbeeld:`\\myserver\myfolder`

**Type**: teken reeks

**Positie**: 1

**Standaard waarde**: `$Env:SystemDrive\M365AnalyticsLogs` (als deze para meter is ingesteld op NULL, leeg of witruimte, maakt het script de map M365AnalyticsLogs op het systeem station.)

### `-LogMode`

Hiermee geeft u het niveau van de logboeken uitgebreider op.

**Waarden**:

- `0`: Script-berichten worden alleen in het Power shell-opdracht venster vastgelegd.

- `1`: Script berichten vastleggen in beide logboek bestanden in de map uitvoermap en Power shell-opdracht venster.

- `2`: Script-berichten worden alleen in het logboek bestand onder de uitvoermap vastgelegd.

**Type**: Int16

**Positie**: 2

**Standaard waarde**: `1` (script berichten vastleggen in logboek bestand en Power shell-opdracht venster.)

### `-CollectNetTrace`

Hiermee wordt aangegeven of het script de netwerk tracering verzamelt.

**Waarden**:

- `0`: Schakel de netwerk tracering niet in.

- `1`(een wille keurig geheel getal dat niet gelijk is aan nul): netwerk tracering inschakelen en resultaten verzamelen.

**Type**: Int16

**Positie**: 3

**Standaard waarde**: `0` (Schakel de netwerk tracering niet in)

### `-CollectUTCTrace`

Hiermee geeft u op of het script de Windows UTC-tracering verzamelt en connectiviteits diagnose uitvoert.

**Waarden**:

- `0`: Schakel de UTC-tracering niet in of voer connectiviteits diagnose uit.

- `1`(een wille keurig geheel getal dat niet gelijk is aan nul): Schakel de UTC-tracering in, voer connectiviteits diagnose uit en verzamel resultaten.

**Type**: Int16

**Positie**: 4

**Standaard waarde**: `0` (Schakel de UTC-tracering niet in of voer connectiviteits diagnose uit)


## <a name="output"></a>Uitvoer

Met het script maakt u een *werkmap* onder het opgegeven pad. Bijvoorbeeld **M365AnalyticsLogs_yy_MM_dd_HH_mm_ss**. Alle uitvoer bestanden worden in deze werkmap geplaatst.

Als u het script in staat stelt om naar een *logboek bestand*te schrijven, wordt er een in de werkmap gegenereerd. Bijvoorbeeld **M365AnalyticsLogs_ yy_MM_dd_HH_mm_ss. txt**.

Het script genereert ook andere *Diagnostische bestanden* in de werkmap. Bijvoorbeeld:

- `installedKBs.txt`: een lijst met Windows-updates die op het apparaat zijn geïnstalleerd
- `appcompat`: toepassings compatibiliteits gegevens
- `Reg*.txt`: een reeks bestanden met geëxporteerde gegevens uit het Windows-REGI ster


## <a name="examples"></a>Voorbeelden

### <a name="example-1-run-script-via-powershell-command-window-with-default-values"></a><a name="bkmk_ex1"></a>Voor beeld 1: script uitvoeren via Power shell-opdracht venster met standaard waarden

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1
```

### <a name="example-2-run-script-via-powershell-command-window-with-specified-parameters"></a><a name="bkmk_ex2"></a>Voor beeld 2: script uitvoeren via Power shell-opdracht venster met opgegeven para meters

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogPath "c:\testABC" -LogMode 0 -CollectNetTrace 0 -CollectUTCTrace 0
```

### <a name="example-3-run-script-via-powershell-command-window-with-specified-parameters-in-position"></a><a name="bkmk_ex3"></a>Voor beeld 3: script uitvoeren via Power shell-opdracht venster met opgegeven para meters op positie

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 "c:\testABC" 2 0 0
```

### <a name="example-4-run-script-via-powershell-command-window-with-specified-parameter-and-verbose-messages"></a><a name="bkmk_ex4"></a>Voor beeld 4: script uitvoeren via Power shell-opdracht venster met opgegeven para meter en uitgebreide berichten

```PowerShell
.\DesktopAnalyticsLogsCollector.ps1 -LogMode 1 -Verbose
```

### <a name="example-5-deploy-script-via-configuration-manager-scripts"></a><a name="bkmk_ex5"></a>Voor beeld 5: script implementeren via Configuration Manager **scripts**

Zie [Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console](../apps/deploy-use/create-deploy-scripts.md)voor meer informatie.

DesktopAnalyticsLogsCollector. ps1 is digitaal ondertekend door micro soft. Mogelijk moet u het micro soft-certificaat voor ondertekening van programma code toevoegen als een vertrouwde uitgever op het doel apparaat.

1. Open de eigenschappen van het script in Windows Verkenner. Ga naar het tabblad **digitale hand tekeningen** en selecteer **Details**.

2. Selecteer **certificaat weer geven**op het tabblad **Algemeen** .

    > [!Note]
    > Als u het certificaat wilt distribueren via andere mechanismen, exporteert u het certificaat eerst naar een bestand. Ga naar het tabblad **Details** en selecteer **kopiëren naar bestand**.

3. Selecteer **certificaat installeren**. Importeer het certificaat en plaats het in het archief met **vertrouwde uitgevers** .


## <a name="see-also"></a>Zie ook

- [Problemen met Desktop Analytics oplossen](troubleshooting.md)

- [Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console](../apps/deploy-use/create-deploy-scripts.md)
