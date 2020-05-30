---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/26/2020
ms.openlocfilehash: c450cff20df5dd45daa8097b8132f00d51bf713d
ms.sourcegitcommit: 0d2f6132428b5fa994e5b770ab1d2bf7d78ac179
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/30/2020
ms.locfileid: "84226690"
---
<!--This file is shared by the CMPivot script samples articles for both Microsoft Endpoint Manager tenant attach and Configuration Manager-->


## <a name="operating-system"></a>Besturingssysteem

Hiermee wordt informatie over het besturings systeem opgehaald.

```kusto
// Sample query for OS information
OperatingSystem
```

## <a name="recently-used-applications"></a>Recent gebruikte toepassingen

Met de volgende query worden recent gebruikte toepassingen (afgelopen 2 uur) opgehaald:

```kusto
CCMRecentlyUsedApplications
| where (LastUsedTime > ago(2h))
| project CompanyName, ProductName, ProductVersion, LastUsedTime
```

## <a name="device-start-times"></a>Start tijden van apparaat

De volgende query geeft aan wanneer apparaten zijn gestart in de afgelopen zeven dagen:

```kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
```

## <a name="free-disk-space"></a>Vrije schijfruimte

Met de volgende query wordt de vrije schijf ruimte weer gegeven:

```kusto
LogicalDisk
| project Device, DeviceID, Name, Description, FileSystem, Size, FreeSpace
| order by DeviceID asc
```

## <a name="device-information"></a>Apparaatgegevens

Apparaat, fabrikant, model en niet weer geven:

```kusto 
ComputerSystem
| project Device, Manufacturer, Model
| join (OperatingSystem | project Device, OSVersion=Caption)
```

## <a name="boot-times-for-a-device"></a>Opstart tijden voor een apparaat

Opstart tijden voor apparaten weer geven:

```kusto
SystemBootData
| project Device, SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
| order by SystemStartTime desc
```

## <a name="authentication-failures"></a>Verificatiefouten

Zoek de gebeurtenis logboeken op mislukte verificaties.

```kusto
EventLog('Security')
| where  EventID == 4673
```

## <a name="processmoduleprocessname"></a>ProcessModule ( \<processname> )  

Alle modules (dll's) inventariseren die door een bepaald proces zijn geladen. ProcessModule is handig bij het zoeken naar malware die in legitieme processen wordt verborgen.  

```kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

## <a name="antimalware-software-status"></a>Status van antimalware-software

Hiermee wordt de status opgehaald van de antimalware-software die op de computer is geïnstalleerd.

```kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
```

## <a name="find-bios-manufacturer-that-contains-any-word-like-micro"></a>BIOS-fabrikant zoeken die een woord bevat zoals micro

```kusto
Bios
// Find BIOS Manufacturer that contains any word like Micro, such as Microsoft
| where Manufacturer like '%Micro%'
```

## <a name="find-file-by-its-hash"></a>Bestand zoeken op basis van de bijbehorende hash

Zoek naar een bestand op hash.

```kusto
Device
| join kind=leftouter ( File('%windir%\\system32\\*.exe')
| where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
| project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
```

## <a name="find-scripts-in-the-ccm-logs-in-the-last-hour"></a>' Scripts ' zoeken in de CCM-Logboeken in het afgelopen uur

Met de volgende query worden gebeurtenissen in het afgelopen uur weer geven:

```kusto
CcmLog('Scripts',1h)
```

