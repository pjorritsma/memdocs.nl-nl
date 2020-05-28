---
title: Ondersteuningscentrum OneTrace (preview)
titleSuffix: Configuration Manager
description: OneTrace is een nieuwe logboek weergave met het ondersteunings centrum met verbeteringen ten opzichte van CMTrace.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 150090556d63b1bdf0b35dc9b53b450137d7f9d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723108"
---
# <a name="support-center-onetrace-preview"></a>Ondersteuningscentrum OneTrace (preview)

<!--3555962-->

Vanaf versie 1906 is OneTrace een nieuwe logboek weergave met het ondersteunings centrum. Het werkt op dezelfde manier als CMTrace, met de volgende verbeteringen:

- Een weer gave met tabbladen
- Dockable Windows
- Verbeterde zoek mogelijkheden
- Mogelijkheid om filters in te scha kelen zonder de logboek weergave te verlaten
- Schuif balk hints om snel cluster fouten te identificeren
- Snel logboek openen voor grote bestanden

[![Scherm opname van OneTrace log viewer](media/3555962-onetrace.png)](media/3555962-onetrace.png#lightbox)

OneTrace werkt met veel soorten logboek bestanden, zoals:

- Client logboeken Configuration Manager
- Configuration Manager-server logboeken
- Statusberichten
- Windows Update ETW-logboek bestand in Windows 10
- Windows Update logboek bestand in Windows 7 & Windows 8,1

## <a name="prerequisites"></a>Vereisten

- .NET Framework versie 4,6 of hoger

## <a name="install"></a>Installeren

OneTrace wordt geïnstalleerd met het ondersteunings centrum. Zoek het installatie programma voor het ondersteunings centrum op de site server op het volgende pad: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` .

Standaard wordt de toepassing OneTrace geïnstalleerd op `C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe` .

> [!Note]  
> Het ondersteunings centrum en OneTrace gebruiken Windows Presentation Foundation (WPF). Dit onderdeel is niet beschikbaar in Windows PE. Ga door met het gebruik van CMTrace in opstart installatie kopieën met taken reeks implementaties.  

## <a name="log-groups"></a>Logboek groepen

<!--5559993-->

Vanaf versie 2002 ondersteunt OneTrace aanpas bare logboek groepen, vergelijkbaar met de functie in het ondersteunings centrum. Met logboek groepen kunt u alle logboek bestanden openen voor één scenario. OneTrace bevat momenteel groepen voor de volgende scenario's:

- Toepassingsbeheer
- Instellingen voor naleving (ook wel gewenst configuratie beheer genoemd)
- Software-updates

Als u logboek groepen wilt weer geven, gaat u naar het menu **weer gave** en selecteert u **logboek groepen**.

![Scherm opname van OneTrace-logboek groep voor toepassings beheer](media/5559993-onetrace-log-groups.png)

### <a name="customize-log-groups"></a>Logboek groepen aanpassen

U kunt deze groepen aanpassen door de configuratie-XML te wijzigen, die standaard zich in het volgende pad bevindt: `C:\Program Files (x86)\Configuration Manager Support Center\LogGroups.xml` .

Het volgende voor beeld is een gedeelte van het standaard configuratie bestand:

``` XML
<LogGroups>
  <LogGroup Name="Desired Configuration Management" GroupType="1" GroupFilePath="">
    <LogFile>CIAgent.log</LogFile>
    <LogFile>CIDownloader.log</LogFile>
    <LogFile>CIStateStore.log</LogFile>
    <LogFile>CIStore.log</LogFile>
    <LogFile>CITaskMgr.log</LogFile>
    <LogFile>ccmsdkprovider.log</LogFile>
    <LogFile>DCMAgent.log</LogFile>
    <LogFile>DCMReporting.log</LogFile>
    <LogFile>DcmWmiProvider.log</LogFile>
  </LogGroup>
</LogGroups>
```

De `GroupType` eigenschap accepteert de volgende waarden:

- `0`: Onbekend of ander
- `1`: Configuration Manager-client logboeken
- `2`: Configuration Manager-server logboeken

De `GroupFilePath` eigenschap kan een expliciet pad voor de logboek bestanden bevatten. Als deze leeg is, is OneTrace afhankelijk van de Register configuratie voor het groeps type. Als u bijvoorbeeld instelt `GroupType=1` , wordt standaard OneTrace automatisch gezocht in `C:\Windows\CCM\Logs` de logboeken in de groep. In dit voor beeld hoeft u niet op te geven `GroupFilePath` .

## <a name="see-also"></a>Zie ook

- [Logboek viewer voor ondersteunings centrum](support-center-ui-reference.md#bkmk_log-viewer)

- [CMTrace](cmtrace.md)
