---
title: Hulp programma voor service verbindingen
titleSuffix: Configuration Manager
description: Meer informatie over dit hulp programma waarmee u verbinding kunt maken met de Cloud service van Configuration Manager om hand matig gebruiks gegevens te uploaden.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8b56b849be6abd2634e29d35e58494d4d3215857
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126083"
---
# <a name="use-the-service-connection-tool-for-configuration-manager"></a>Gebruik het hulp programma voor service verbindingen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het **hulp programma voor service verbindingen** wanneer uw service verbindings punt zich in de offline modus bevindt. U kunt deze ook gebruiken wanneer uw Configuration Manager-site systeem servers niet zijn verbonden met internet. Het hulp programma kan u helpen uw site up-to-date te houden met de meest recente updates voor Configuration Manager.

Wanneer u het hulp programma uitvoert, maakt het verbinding met de Configuration Manager Cloud service, worden gebruiks gegevens voor uw hiërarchie geüpload en worden updates gedownload. Het uploaden van gebruiks gegevens is nood zakelijk om ervoor te zorgen dat de Cloud service de juiste updates voor uw omgeving kan leveren.

## <a name="prerequisites"></a>Vereisten

- De site heeft een service verbindings punt en u configureert deze voor een **offline-verbinding op aanvraag**.

- Voer het hulp programma uit vanaf een opdracht prompt als beheerder. Er is geen gebruikers interface.

- U voert het hulp programma uit vanaf het service aansluitpunt en een computer die verbinding kan maken met internet. Elk van deze computers moet een x64-bits besturings systeem hebben en de volgende onderdelen hebben:

  - De x86- en x64-bestanden van **Visual C++ Redistributable** . Configuration Manager installeert standaard de x64-versie op de computer die het service verbindings punt host. Zie [herdistribueerbare Visual C++-pakketten voor Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)voor informatie over het downloaden van dit onderdeel.

  - **.NET Framework 4.5.2** of hoger

- Het account dat u gebruikt om het hulp programma uit te voeren, heeft de volgende machtigingen nodig:

  - **Lokale beheerder** op de computer die het service verbindings punt host

  - **Lees** machtigingen voor de site database

- U hebt een methode nodig om de bestanden over te dragen tussen de computer met Internet toegang en het service verbindings punt. Bijvoorbeeld een USB-station met voldoende beschik bare ruimte voor het opslaan van bestanden en updates.

## <a name="overview"></a>Overzicht

1. **Voorbereiden**: Voer het hulp programma uit op het service aansluitpunt. Hiermee worden de gebruiks gegevens in een CAB-bestand geplaatst op de locatie die u opgeeft. Kopieer het gegevens bestand naar de computer met een Internet verbinding.

2. **Verbinding maken**: Voer het hulp programma uit op de computer met een Internet verbinding. Uw gebruiks gegevens worden geüpload en vervolgens Configuration Manager updates gedownload. Kopieer de gedownloade updates naar het service verbindings punt.

    U kunt meerdere gegevens bestanden tegelijk uploaden, elk uit een andere hiërarchie. U kunt ook een proxy server en een gebruiker voor de proxy server opgeven.

3. **Importeren**: Voer het hulp programma uit op het service verbindings punt. De updates worden geïmporteerd en toegevoegd aan uw site. U kunt [deze updates](install-in-console-updates.md) vervolgens weer geven en installeren in de Configuration Manager-console.

### <a name="upload-multiple-data-files"></a>Meerdere gegevens bestanden uploaden

- Plaats alle geëxporteerde gegevens bestanden van afzonderlijke hiërarchieën in dezelfde map. Geef elk bestand een unieke naam. Als dat nodig is, kunt u ze hand matig een andere naam geven.

- Wanneer u het hulp programma uitvoert om gegevens te uploaden naar micro soft, geeft u de map op die de gegevens bestanden bevat.

- Wanneer u het hulp programma uitvoert om gegevens te importeren, worden met het hulp programma alleen de gegevens voor die hiërarchie geïmporteerd.

### <a name="specify-a-proxy-server"></a>Een proxy server opgeven

Als voor de computer met een Internet verbinding een proxy server is vereist, ondersteunt het hulp programma een basis proxy configuratie. Gebruik de optionele para meters **-proxyserveruri** en **-proxy username**. Zie [opdracht regel parameters](#bkmk_cmd)voor meer informatie.

### <a name="specify-the-type-of-updates-to-download"></a>Geef het type updates op dat u wilt downloaden

Het hulp programma ondersteunt opties om te bepalen welke bestanden u downloadt. Het hulp programma downloadt standaard alleen de meest recente beschik bare update die van toepassing is op de versie van uw site. Hotfixes worden niet gedownload.

Als u dit gedrag wilt wijzigen, gebruikt u een van de volgende para meters om te wijzigen welke bestanden worden gedownload:

- **-downloadall**: down load alle updates, inclusief updates en hotfixes, ongeacht de versie van uw site.
- **-downloadhotfix**: down load alle hotfixes, ongeacht de versie van uw site.
- **-downloadsiteversion**: downloadt updates en hotfixes met een latere versie dan de versie van uw site.

    > [!IMPORTANT]
    > Vanwege een bekend probleem in Configuration Manager versie 2002, werkt het standaard gedrag niet zoals verwacht. Werk bij naar versie 2006, of gebruik de para meter **-downloadsiteversion** om de vereiste updates voor versie 2002 te downloaden.<!-- 7594517 -->

Zie [opdracht regel parameters](#bkmk_cmd)voor meer informatie.

> [!TIP]
> Het hulp programma bepaalt de versie van uw site van het gegevens bestand. Als u de versie wilt controleren, zoekt u in het CAB-bestand naar het tekst bestand met de naam met de site versie.

## <a name="use-the-tool"></a>Het hulp programma gebruiken  

Het hulp programma voor service verbindingen bevindt zich in de Configuration Manager installatie media op het volgende pad: `SMSSETUP\TOOLS\ServiceConnectionTool\ServiceConnectionTool.exe` . Gebruik altijd het hulp programma voor service verbindingen dat overeenkomt met de versie van Configuration Manager die u gebruikt. Al deze bestanden moeten zich in dezelfde map bevindt om te kunnen werken met het hulp programma voor service verbindingen.

Kopieer de map **ServiceConnectionTool** met alle inhoud ervan naar de computer met een Internet verbinding.

In deze procedure worden de volgende bestands namen en maplocaties in de voor beelden van de opdracht regels gebruikt. U hoeft deze paden en bestands namen niet te gebruiken. U kunt alternatieven gebruiken die overeenkomen met uw omgeving en voor keuren.

- Het pad naar de bron bestanden voor de Configuration Manager installatie media op het service verbindings punt:`C:\Source`

- Het pad naar een USB-station waar u de gegevens opslaat voor overdracht tussen computers:`D:\USB\`

- De naam van het gegevens bestand dat u van de site exporteert:`UsageData.cab`

- De naam van de lege map waar het hulp programma gedownloade updates opslaat voor Configuration Manager:`UpdatePacks`

### <a name="prepare"></a>Voorbereiden

1. Open een opdracht prompt als beheerder op de computer die als host fungeert voor het service aansluitpunt en wijzig de map in de locatie van het hulp programma. Bijvoorbeeld:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Voer de volgende opdracht uit om het gegevens bestand voor te bereiden:

    `ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

    > [!NOTE]
    > Als u gegevens bestanden van meer dan één hiërarchie tegelijk uploadt, geeft u elk gegevens bestand een unieke naam. Indien nodig kunt u later de naam van bestanden wijzigen.

    De gegevens in het bestand zijn gebaseerd op het niveau van de diagnostische en gebruiks gegevens die u voor de site configureert. Zie [overzicht van diagnose-en gebruiks gegevens](../../plan-design/diagnostics/diagnostics-and-usage-data.md)voor meer informatie. U kunt het hulp programma gebruiken om de gegevens naar een CSV-bestand te exporteren om de inhoud weer te geven. Zie [exporteren](#-export)voor meer informatie.

1. Wanneer het hulp programma klaar is met het exporteren van de gebruiks gegevens, kopieert u het gegevens bestand naar een computer die toegang heeft tot internet.

### <a name="connect"></a>Verbinding maken

1. Open op de computer met Internet toegang een opdracht prompt als beheerder en wijzig de map naar de locatie van het hulp programma. Deze locatie is een kopie van de volledige map **ServiceConnectionTool** . Bijvoorbeeld:

    `cd D:\USB\ServiceConnectionTool\`

1. Voer de volgende opdracht uit om het gegevens bestand te uploaden en de Configuration Manager-updates te downloaden:

    `ServiceConnectionTool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

    Zie [opdracht regel parameters](#bkmk_cmd)voor meer voor beelden.

    > [!NOTE]  
    > Wanneer u deze opdracht regel uitvoert, ziet u mogelijk de volgende fout:
    >
    > **Onverwerkte uitzonde ring: System. UnauthorizedAccessException: toegang tot het pad ' C:\Users\jqpublic\AppData\Local\Temp\extractmanifestcab\95F8A562.sql ' is geweigerd.**
    >
    > U kunt deze fout gewoon negeren. Sluit het fout venster om door te gaan.

1. Wanneer het hulp programma de updates heeft gedownload, kopieert u deze naar het service verbindings punt.

### <a name="import"></a>Importeren

1. Open een opdracht prompt als beheerder op de computer die als host fungeert voor het service aansluitpunt en wijzig de map in de locatie van het hulp programma. Bijvoorbeeld:

    `cd C:\Source\SMSSETUP\TOOLS\ServiceConnectionTool\`

1. Voer de volgende opdracht uit om de updates te importeren:

    `ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

1. Nadat het importeren is voltooid, sluit u de opdracht prompt. Er worden alleen updates voor de toepasselijke hiërarchie geïmporteerd.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **updates en onderhoud** . Geïmporteerde updates zijn nu beschikbaar om te installeren. Zie [updates binnen de console installeren](install-in-console-updates.md)voor meer informatie.

## <a name="log-files"></a>Logboekbestanden

- **ServiceConnectionTool. log**: telkens wanneer u het hulp programma voor service verbindingen uitvoert, wordt het naar dit logboek bestand geschreven. Het pad van het logboek bestand is altijd dezelfde locatie als het hulp programma. Dit logboek bestand bevat eenvoudige Details over het gebruik van het hulp programma op basis van de para meters die u gebruikt. Telkens wanneer u het hulp programma uitvoert, vervangt het hulp programma een bestaand logboek bestand.

- **ConfigMgrSetup. log**: tijdens de [verbindings](#connect) fase schrijft het hulp programma naar dit logboek bestand in de hoofdmap van het systeem station. Dit logboek bestand bevat meer gedetailleerde informatie. Bijvoorbeeld welk bestand het hulp programma downloadt en als de hash-controles zijn geslaagd.

## <a name="command-line-parameters"></a><a name="bkmk_cmd"></a>Opdracht regel parameters

In deze sectie worden alle beschik bare para meters voor het hulp programma voor service verbindingen alfabetisch gesorteerd.

### <a name="-connect"></a>-verbinden

Gebruiken tijdens de [verbindings](#connect) fase op de computer met Internet toegang. Er wordt verbinding gemaakt met de Configuration Manager Cloud service om het gegevens bestand te uploaden en updates te downloaden.

Hiervoor zijn de volgende para meters vereist:

- **-usagedatasrc**: de locatie van het gegevens bestand dat moet worden geüpload
- **-updatepackdest**: een pad voor de gedownloade updates

U kunt ook de volgende optionele para meters gebruiken:

- **-proxyserveruri**: de FQDN-naam van de proxy server
- **-proxy username**: een gebruikers naam voor de proxy server
- **-downloadall**: down load alles, inclusief updates en hotfixes, ongeacht de versie van uw site.
- **-downloadhotfix**: down load alle hotfixes, ongeacht de versie van uw site.
- **-downloadsiteversion**: down load updates en hotfixes die een hogere versie hebben dan de versie van uw site.

#### <a name="example-of-connect-without-a-proxy-server"></a>Voor beeld van verbinding maken zonder proxy server

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks`

#### <a name="example-of-connect-with-a-proxy-server"></a>Voor beeld van verbinding maken met een proxy server

`ServiceConnectionTool.exe -connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itproxy.contoso.com -proxyusername jqpublic`

#### <a name="example-of-connect-to-download-only-site-version-applicable-updates"></a>Voor beeld van verbinding maken om alleen updates te downloaden die van toepassing zijn op de site versie

`ServiceConnectionTool.exe -connect -downloadsiteversion -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks`

### <a name="-dest"></a>-doel

Een vereiste para meter met de para meter **-export** om het pad en de bestands naam op te geven van het CSV-bestand dat moet worden geëxporteerd. Zie [exporteren](#-export)voor meer informatie.

### <a name="-downloadall"></a>-downloadall

Een optionele para meter met de para meter **-Connect** voor het downloaden van alles, inclusief updates en hotfixes, ongeacht de versie van uw site. Zie [-Connect](#connect)voor meer informatie.

### <a name="-downloadhotfix"></a>-downloadhotfix

Een optionele para meter met de para meter **-Connect** om alleen alle hotfixes te downloaden, ongeacht de versie van uw site. Zie [-Connect](#-connect)voor meer informatie.

### <a name="-downloadsiteversion"></a>-downloadsiteversion

Een optionele para meter met de para meter **-Connect** voor het downloaden van updates en hotfixes met een latere versie dan de versie van uw site. Zie [-Connect](#-connect)voor meer informatie.

### <a name="-export"></a>-exporteren

Gebruik tijdens de [voorbereidings](#prepare) fase om gebruiks gegevens te exporteren naar een CSV-bestand. Voer deze uit als beheerder op het service verbindings punt. Met deze actie kunt u de inhoud van de gebruiks gegevens controleren voordat u naar micro soft uploadt. Hiervoor is de para meter **-doel** vereist om de locatie van het CSV-bestand op te geven.

#### <a name="example-of-export"></a>Voor beeld van exporteren

`-export -dest D:\USB\usagedata.csv`

### <a name="-import"></a>-importeren

Gebruik tijdens de [import](#import) fase op het service verbindings punt om de updates te importeren op de site. Hiervoor is de para meter **-updatepacksrc** vereist voor het opgeven van de locatie van de gedownloade updates.

#### <a name="example-of-import"></a>Voor beeld van importeren

`ServiceConnectionTool.exe -import -updatepacksrc D:\USB\UpdatePacks`

### <a name="-prepare"></a>-voorbereiden

Gebruiken tijdens de [voorbereidings](#prepare) fase op het service verbindings punt om gebruiks gegevens van de site te exporteren. Hiervoor is de para meter **-usagedatadest** vereist om de locatie van het geëxporteerde-gegevens bestand op te geven.

#### <a name="example-of-prepare"></a>Voor beeld van voorbereiden

`ServiceConnectionTool.exe -prepare -usagedatadest D:\USB\UsageData.cab`

### <a name="-proxyserveruri"></a>-proxyserveruri

Een optionele para meter met de para meter **-Connect** om de FQDN-naam van uw proxy server op te geven. Zie [-Connect](#-connect)voor meer informatie.

### <a name="-proxyusername"></a>-proxy username

Een optionele para meter met de para meter **-Connect** om de gebruikers naam op te geven die bij de proxy server moet worden geverifieerd. Zie [-Connect](#-connect)voor meer informatie.

### <a name="-updatepackdest"></a>-updatepackdest

Een vereiste para meter met de para meter **-Connect** om een pad op te geven voor de gedownloade updates. Zie [-Connect](#-connect)voor meer informatie.

### <a name="-updatepacksrc"></a>-updatepacksrc

Een vereiste para meter met de para meter **-import** om een pad van de gedownloade updates op te geven. Zie [-importeren](#-import)voor meer informatie.

### <a name="-usagedatadest"></a>-usagedatadest

Een vereiste para meter met de para meter **-Prepare** voor het opgeven van een pad en een bestands naam van het geëxporteerde-gegevens bestand. Zie voor meer informatie [-voor bereiding](#-prepare).

## <a name="next-steps"></a>Volgende stappen

[Updates binnen de console installeren](install-in-console-updates.md)

[Diagnostische gegevens en gebruiksgegevens weergeven](../../plan-design/diagnostics/view-diagnostics-and-usage-data.md)
