---
title: Aanbevolen hardware
titleSuffix: Configuration Manager
description: Krijg aanbevelingen voor hardware om uw Configuration Manager omgeving te schalen buiten een eenvoudige implementatie.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 36b90627f25c5cf19b867a78e141b69266478c58
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428786"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Aanbevolen hardware voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De volgende aanbevelingen zijn richt lijnen waarmee u uw Configuration Manager-omgeving kunt schalen om meer dan een zeer eenvoudige implementatie van sites, site systemen en clients te ondersteunen. Ze zijn niet bedoeld voor het bedekken van alle mogelijke site-en hiërarchie configuraties.  

Gebruik de informatie in de volgende secties als richt lijn om u te helpen bij het plannen van hardware. Zorg ervoor dat uw hardware kan voldoen aan de verwerkings belasting voor clients en sites die gebruikmaken van de beschik bare Configuration Manager-functies.

Zie voor meer informatie het [Configuration Manager technisch document over prestaties en schaal](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e)baarheid.

## <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Site systemen

In deze sectie vindt u aanbevolen hardwareconfiguraties voor Configuration Manager-site systemen. Gebruik deze aanbevelingen om het maximum aantal clients te ondersteunen en de meeste of alle Configuration Manager functies te gebruiken. Als uw omgeving minder dan het maximum aantal clients ondersteunt en geen gebruik maakt van alle beschik bare functies, is het mogelijk dat er minder bronnen nodig zijn. In het algemeen zijn de volgende belang rijke factoren de prestaties van het algehele systeem beperkt:

1. I/O-prestaties schijf

2. Beschikbaar geheugen

3. CPU

Gebruik voor de beste prestaties RAID 10-configuraties voor alle gegevens stations en een 1 Gbps Ethernet-netwerk.

### <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Site servers

|Site configuratie|CPU (kern geheugens)|Geheugen (GB)|Geheugen toewijzing voor SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Zelfstandige primaire site server met een database siterol op dezelfde server <sup> [Opmerking 1](#bkmk_note1)</sup>|16|96|80|  
|Zelfstandige primaire siteserver met een externe sitedatabase|8|16|-|  
|Externe databaseserver voor een zelfstandige primaire site|16|72|90|  
|Server van de centrale beheer site met een database siterol op dezelfde server <sup> [Opmerking 1](#bkmk_note1)</sup>|20|128|80|  
|Server van de centrale beheersite met een externe sitedatabase|8|16|-|  
|Externe databaseserver voor een centrale beheersite|16|96|90|  
|Onderliggende primaire site met een database siterol op dezelfde server|16|96|80|  
|Onderliggende primaire siteserver met een externe sitedatabase|8|16|-|  
|Externe databaseserver voor een onderliggende primaire site|16|72|90|  
|Secundaire siteserver|8|16|-|  

#### <a name="note-1-collocated-sql"></a><a name="bkmk_note1"></a>Opmerking 1: Co SQL

Wanneer u de-site server en SQL Server op dezelfde computer installeert, ondersteunt de implementatie de maximale [grootte-en schaal nummers](size-and-scale-numbers.md) voor sites en clients. Deze configuratie kan [Opties voor hoge Beschik baarheid](../../servers/deploy/configure/high-availability-options.md)beperken, zoals het gebruik van een SQL Server cluster. Als u een grotere omgeving hebt, kunt u een externe SQL Server gebruiken als gevolg van de hogere I/O-vereisten voor de ondersteuning van beide rollen op dezelfde computer.

### <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Externe site systeem servers

De volgende richt lijnen zijn voor computers die één site systeemrol bevatten. Plan om aan te passen wanneer u meerdere site systeem rollen op dezelfde computer installeert.

|Sitesysteemrol|CPU (kern geheugens)|Geheugen (GB)|Schijfruimte (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Beheerpunt|4|8|50|  
|Distributiepunt|2|8|Zoals vereist door het besturings systeem en voor het opslaan van inhoud die u implementeert|  
|Opmerking over software-update punt <sup> [2](#bkmk_note2)</sup>|8|16|Zoals vereist door het besturings systeem en voor het opslaan van updates die u implementeert|  
|Alle andere sitesysteemrollen|4|8|50|  

#### <a name="note-2-wsus-configurations"></a><a name="bkmk_note2"></a>Opmerking 2: WSUS-configuraties

De computer die als host fungeert voor een software-update punt vereist de volgende configuraties voor groepen van IIS-toepassingen:  

- Verhoog de **lengte** van de WsusPool-wachtrij naar **2000**.  

- Verhoog de **WsusPool privé-geheugen limiet** met vier keer of stel deze in op **0** (onbeperkt).  

### <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Schijf ruimte voor site systemen

Schijf toewijzing en-configuratie dragen bij aan de prestaties van Configuration Manager. Omdat elke Configuration Manager omgeving anders is, kunnen de door u geïmplementeerde waarden variëren van de volgende richt lijnen.

Voor de beste prestaties plaatst u elk object op een afzonderlijk, speciaal RAID-volume. Gebruik voor alle gegevens volumes voor Configuration Manager en de bijbehorende database bestanden RAID 10 voor de beste prestaties.

|Gegevensgebruik|Minimale schijfruimte|25.000 clients|50.000 clients|100.000 clients|150.000 clients|700.000-clients (centrale beheer site)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Toepassings-en logboek bestanden Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|MDF-bestand van sitedatabase|75 GB voor elke 25.000 clients|75 GB|150 GB|300 GB|500 GB|2 TB|  
|LDF-bestand van sitedatabase|25 GB voor elke 25.000 clients|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Tijdelijke databasebestanden (MDF en LDF)|Indien nodig|Indien nodig|Indien nodig|Indien nodig|Indien nodig|Indien nodig|  

Zie aanpassings richtlijnen voor de geïnstalleerde versie van het besturings systeem voor de Windows-systeem schijf.

Voor inhoud op distributie punten is deze afhankelijk van uw implementaties. Deze richt lijnen omvatten niet de benodigde schijf ruimte voor de inhouds bibliotheek op de site server of distributie punten. Zie [de inhouds bibliotheek](../../../core/plan-design/hierarchy/the-content-library.md)voor meer informatie.

Houd rekening met de volgende aanvullende richt lijnen wanneer u de vereisten voor de schijf ruimte plant:

- Elke client vereist ongeveer 5-10 MB aan ruimte in de data base. Dit aantal is afhankelijk van het hiërarchie type, de configuratie en het aantal clients. De grootte is over het algemeen minder voor grotere omgevingen. Kleinere sites hebben meer database gebruik per client.<!-- SCCMDocs#1048 -->

- Voor de tijdelijke data base van de primaire site plant u een gecombineerde grootte van 25% tot 30% van het MDF-bestand van de site database. De werkelijke grootte kan kleiner of groter zijn. Dit is afhankelijk van de prestaties van de site server en het volume van binnenkomende gegevens gedurende zowel korte als lange Peri Oden.

  > [!NOTE]
  > Wanneer u 50.000 of meer clients op een site hebt, plan dan om vier of meer tijdelijke data base. MDF-bestanden te gebruiken.

- De grootte van de tijdelijke Data Base voor een centrale beheer site is doorgaans veel kleiner dan voor een primaire site.

- Als u SQL Server Express gebruikt voor de data base van de secundaire site, wordt de grootte van de data base beperkt tot 10 GB.

## <a name="clients"></a><a name="bkmk_ScaleClient"></a>Clients

In deze sectie vindt u aanbevolen hardwareconfiguraties voor computers die u beheert met behulp van Configuration Manager-client software.

### <a name="client-for-windows-computers"></a>Client voor Windows-computers:

De volgende minimale vereisten gelden voor op Windows gebaseerde computers die u beheert met behulp van Configuration Manager, waaronder Inge sloten edities:

- **Processor en geheugen:** Raadpleeg de vereisten voor de processor en het RAM-geheugen voor het besturings systeem.

- **Schijf ruimte:** 500 MB beschik bare schijf ruimte, waarbij 5 GB wordt aanbevolen voor de Configuration Manager-client cache. Als u aangepaste instellingen gebruikt om de Configuration Manager-client te installeren, is minder schijf ruimte vereist.

  - Gebruik de client. msi-eigenschap **SMSCACHESIZE** om een cache grootte in te stellen die kleiner is dan de standaard waarde van 5120 MB. De minimumgrootte is 1 MB. In het volgende voor beeld wordt een cache van 2 MB gemaakt:`CCMSetup.exe SMSCACHESIZE=2`

    Zie [over eigenschappen van client installatie](../../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie.

    > [!TIP]
    > Het installeren van de client met minimale schijfruimte is handig voor Windows Embedded-apparaten die doorgaans over een kleinere schijf beschikken dan de gewone Windows-computers.

De volgende aanvullende minimale hardwarevereisten zijn voor optionele functies in Configuration Manager:

- **Implementatie van besturings systeem:** Ten minste 384 MB RAM-geheugen

- **Software Center:** Ten minste een 500-MHz processor

- **Beheer op afstand:** Voor een optimale ervaring is ten minste een Pentium 4-verbinding met 3 GHz (single core) of een vergelijk bare CPU, met ten minste 1 GB RAM-geheugen.

### <a name="client-for-linux-and-unix"></a>Client voor Linux en UNIX

De volgende minimum vereisten gelden voor Linux-en UNIX-servers die u beheert met Configuration Manager.

|Vereiste|Details|  
|-----------------|-------------|  
|Processor en geheugen|Raadpleeg de vereisten voor de processor en het RAM-geheugen voor het besturings systeem van de computer.|  
|Schijfruimte|500 MB beschik bare schijf ruimte, waarbij 5 GB wordt aanbevolen voor de Configuration Manager-client cache.|  
|Netwerkconnectiviteit|Configuration Manager-client computers moeten over een netwerk verbinding met Configuration Manager site systemen beschikken om het beheer mogelijk te maken.|  

## <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Configuration Manager-console

De volgende minimale hardwarevereisten zijn van toepassing op elke computer waarop de Configuration Manager-console wordt uitgevoerd:

- Intel i3 of vergelijkbare CPU  

- 2 GB RAM-geheugen  

- 2 GB schijf ruimte  

|DPI-instelling|Minimale resolutie|  
|-----------------|------------------------|  
|96 / 100%|1024 x 768|  
|120 / 125%|1280 x 960|  
|144 / 150%|1600 x 1200|  
|196 / 200%|2500 x 1600|  

## <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Lab-implementaties

Gebruik de volgende minimale hardwarevereisten voor Lab-en test implementaties van Configuration Manager. Deze aanbevelingen zijn van toepassing op alle site typen, Maxi maal 100 clients:  

|Rol|CPU (kern geheugens)|Geheugen (GB)|Schijfruimte (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Site- en databaseserver|2 - 4|8 - 12|100|  
|Sitesysteemserver|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  
