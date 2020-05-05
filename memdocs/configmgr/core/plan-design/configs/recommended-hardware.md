---
title: Aanbevolen hardware
titleSuffix: Configuration Manager
description: Krijg aanbevelingen voor hardware om uw Configuration Manager omgeving te schalen buiten een eenvoudige implementatie.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d741e34325da859d4fe1f0af554544ce146a42f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719160"
---
# <a name="recommended-hardware-for-configuration-manager"></a>Aanbevolen hardware voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De volgende aanbevelingen zijn richt lijnen waarmee u uw Configuration Manager-omgeving kunt schalen om meer dan een zeer eenvoudige implementatie van sites, site systemen en clients te ondersteunen. Deze aanbevelingen omvatten niet alle mogelijke site- en hiërarchieconfiguraties.  

Gebruik de informatie in de volgende secties als richt lijn voor het plannen van hardware die kan voldoen aan de verwerkings belastingen voor clients en sites die gebruikmaken van de beschik bare Configuration Manager functies met de standaard configuraties.  



##  <a name="site-systems"></a><a name="bkmk_ScaleSieSystems"></a>Site systemen  
In deze sectie vindt u aanbevolen hardwareconfiguraties voor Configuration Manager-site systemen voor implementaties die het maximum aantal clients ondersteunen en de meeste of alle Configuration Manager functies gebruiken. Implementaties die minder dan het maximum aantal clients ondersteunen en die niet alle beschik bare functies gebruiken, vereisen mogelijk minder computer bronnen. In het algemeen zijn dit de belangrijkste factoren die de prestaties van het algehele systeem beperken (in volgorde):  

1.  I/O-prestaties schijf  

2.  Beschikbaar geheugen  

3.  CPU  

Gebruik voor de beste prestaties RAID 10-configuraties voor alle gegevens stations en een 1 Gbps Ethernet-netwerk.  

###  <a name="site-servers"></a><a name="bkmk_ScaleSiteServer"></a>Site servers  

|Site configuratie|CPU (kern geheugens)|Geheugen (GB)|Geheugen toewijzing voor SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Zelfstandige primaire site server met een database siterol op dezelfde server<sup>1</sup>|16|96|80|  
|Zelfstandige primaire siteserver met een externe sitedatabase|8|16|-|  
|Externe databaseserver voor een zelfstandige primaire site|16|72|90|  
|Server van de centrale beheer site met een database siterol op dezelfde server<sup>1</sup>|20|128|80|  
|Server van de centrale beheersite met een externe sitedatabase|8|16|-|  
|Externe databaseserver voor een centrale beheersite|16|96|90|  
|Onderliggende primaire site met een database siterol op dezelfde server|16|96|80|  
|Onderliggende primaire siteserver met een externe sitedatabase|8|16|-|  
|Externe databaseserver voor een onderliggende primaire site|16|72|90|  
|Secundaire siteserver|8|16|-|  

<sup>1</sup> wanneer de site server en SQL Server op dezelfde computer zijn geïnstalleerd, ondersteunt de implementatie de maximale [grootte-en schaal nummers](size-and-scale-numbers.md) voor sites en clients. Maar deze configuratie kan [Opties voor hoge Beschik baarheid voor Configuration Manager](../../servers/deploy/configure/high-availability-options.md)beperken, zoals het gebruik van een SQL Server cluster. Vanwege de hogere I/O-vereisten die nodig zijn om zowel SQL Server als de Configuration Manager-site server te ondersteunen wanneer u beide op dezelfde computer uitvoert, is het een goed idee om een configuratie met een externe SQL Server machine te gebruiken als u een grotere implementatie hebt.  

###  <a name="remote-site-system-servers"></a><a name="bkmk_RemoteSiteSystem"></a>Externe site systeem servers  
De volgende richt lijnen zijn voor computers die één site systeemrol bevatten. Houd er rekening mee dat u wijzigingen moet aanbrengen wanneer u meerdere sitesysteemrollen op dezelfde computer installeert.  

|Sitesysteemrol|CPU (kern geheugens)|Geheugen (GB)|Schijfruimte (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Beheerpunt|4|8|50|  
|Distributiepunt|2|8|Zoals vereist door het besturings systeem en voor het opslaan van inhoud die u implementeert|  
|Software-update punt<sup>1</sup>|8|16|Zoals vereist door het besturings systeem en voor het opslaan van updates die u implementeert|  
|Alle andere sitesysteemrollen|4|8|50|  

<sup>1</sup> de computer die als host fungeert voor een software-update punt vereist de volgende configuraties voor groepen van IIS-toepassingen:  

- Verhoog de **lengte** van de WsusPool-wachtrij naar **2000**.  

- Verhoog de **WsusPool privé-geheugen limiet** met vier keer of stel deze in op **0** (onbeperkt).  

###  <a name="disk-space-for-site-systems"></a><a name="bkmk_DiskSpace"></a>Schijf ruimte voor site systemen  
Schijf toewijzing en-configuratie dragen bij aan de prestaties van Configuration Manager. Omdat elke Configuration Manager omgeving anders is, kunnen de door u geïmplementeerde waarden variëren van de volgende richt lijnen.  

Voor de beste prestaties plaatst u elk object op een afzonderlijk, speciaal RAID-volume. Gebruik voor alle gegevens volumes (Configuration Manager en de bijbehorende database bestanden) RAID 10 voor de beste prestaties.  

|Gegevensgebruik|Minimale schijfruimte|25.000 clients|50.000 clients|100.000 clients|150.000 clients|700.000-clients (centrale beheer site)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Besturingssysteem|Zie de richtlijnen voor het besturingssysteem.|Zie de richtlijnen voor het besturingssysteem.|Zie de richtlijnen voor het besturingssysteem.|Zie de richtlijnen voor het besturingssysteem.|Zie de richtlijnen voor het besturingssysteem.|Zie de richtlijnen voor het besturingssysteem.|  
|Toepassings-en logboek bestanden Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|MDF-bestand van sitedatabase|75 GB voor elke 25.000 clients|75 GB|150 GB|300 GB|500 GB|2 TB|  
|LDF-bestand van sitedatabase|25 GB voor elke 25.000 clients|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Tijdelijke databasebestanden (MDF en LDF)|Indien nodig|Indien nodig|Indien nodig|Indien nodig|Indien nodig|Indien nodig|  
|Inhoud (distributiepuntshares)|Indien nodig<sup>1</sup>|Indien nodig<sup>1</sup>|Indien nodig<sup>1</sup>|Indien nodig<sup>1</sup>|Indien nodig<sup>1</sup>|Indien nodig<sup>1</sup>|  

<sup>1</sup> de richt lijnen voor schijf ruimte bevatten niet de vereiste ruimte voor inhoud die zich bevindt in de inhouds bibliotheek op de site server of distributie punten. Zie [De inhoudsbibliotheek](../../../core/plan-design/hierarchy/the-content-library.md) voor informatie over het plannen van de inhoudsbibliotheek.  

Naast het voorafgaande advies moet u ook rekening houden met de volgende richtlijnen wanneer u de vereisten voor de schijfruimte plant:  

- Voor elke client is ongeveer 5 MB aan ruimte vereist.  

- Wanneer u de grootte van de tijdelijke Data Base voor een primaire site plant, moet u een gecombineerde grootte plannen die 25% tot 30% van het MDF-bestand van de site database is. De daad werkelijke grootte kan aanzienlijk kleiner of groter zijn, maar is afhankelijk van de prestaties van de site server en het volume van binnenkomende gegevens gedurende zowel korte als lange Peri Oden.  

  > [!NOTE]  
  >  Wanneer u 50.000 of meer clients op een site hebt, plan dan om vier of meer tijdelijke data base. MDF-bestanden te gebruiken.  

- De grootte van de tijdelijke Data Base voor een centrale beheer site is doorgaans veel kleiner dan voor een primaire site.  

- De secundaire site database heeft de volgende beperkingen voor de grootte:  

  - SQL Server 2012 Express: 10 GB  

  - SQL Server 2014 Express: 10 GB  

##  <a name="clients"></a><a name="bkmk_ScaleClient"></a>Clients  
In deze sectie vindt u aanbevolen hardwareconfiguraties voor computers die u beheert met behulp van Configuration Manager-client software.  

### <a name="client-for-windows-computers"></a>Client voor Windows-computers:  
Hieronder vindt u de minimale vereisten voor Windows-computers die u beheert met behulp van Configuration Manager, inclusief Inge sloten besturings systemen:  

- **Processor en geheugen:** Raadpleeg de vereisten voor de processor en het RAM-geheugen voor het besturings systeem van de computer.  

- **Schijf ruimte:** 500 MB beschik bare schijf ruimte, waarbij 5 GB wordt aanbevolen voor de Configuration Manager-client cache. Er is minder schijf ruimte vereist als u aangepaste instellingen gebruikt om de Configuration Manager-client te installeren:  

    - Gebruik de Client.msi-eigenschap SMSCACHESIZE om een cachebestand in te stellen dat kleiner is dan de standaardgrootte van 5120 MB. De minimumgrootte is 1 MB. `CCMSetup.exe SMSCachesize=2` Maakt bijvoorbeeld een cache met een grootte van 2 MB.  

    Zie [over eigenschappen van client installatie](../../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie over deze instellingen voor client installatie.  

    > [!TIP]  
    > Het installeren van de client met minimale schijfruimte is handig voor Windows Embedded-apparaten die doorgaans over een kleinere schijf beschikken dan de gewone Windows-computers.  

Hieronder vindt u aanvullende minimale hardwarevereisten voor optionele functies in Configuration Manager.  

- **Implementatie van besturings systeem:** 384 MB RAM-geheugen  

- **Software Center:** 500 MHz-processor  

- **Beheer op afstand:** Pentium 4-verbinding met 3 GHz (één kern) of vergelijk bare CPU, met ten minste 1 GB RAM-geheugen voor optimale ervaring  

### <a name="client-for-linux-and-unix"></a>Client voor Linux en UNIX  
Hieronder vindt u de minimale vereisten voor Linux-en UNIX-servers die u beheert met Configuration Manager.  

|Vereiste|Details|  
|-----------------|-------------|  
|Processor en geheugen|Raadpleeg de vereisten voor de processor en het RAM-geheugen voor het besturings systeem van de computer.|  
|Schijfruimte|500 MB beschik bare schijf ruimte, waarbij 5 GB wordt aanbevolen voor de Configuration Manager-client cache.|  
|Netwerkconnectiviteit|Configuration Manager-client computers moeten over een netwerk verbinding met Configuration Manager site systemen beschikken om het beheer mogelijk te maken.|  

##  <a name="configuration-manager-console"></a><a name="bkmk_ScaleConsole"></a>Configuration Manager-console  
De vereisten in de volgende tabel zijn van toepassing op elke computer waarop de Configuration Manager-console wordt uitgevoerd.  

**Minimale hardwareconfiguratie:**  

- Intel i3 of vergelijkbare CPU  

- 2 GB RAM-geheugen  

- 2 GB schijf ruimte  

|DPI-instelling|Minimale resolutie|  
|-----------------|------------------------|  
|96 / 100%|1024 x 768|  
|120 / 125%|1280 x 960|  
|144 / 150%|1600 x 1200|  
|196 / 200%|2500 x 1600|  

**Ondersteuning voor PowerShell:**  

Wanneer u ondersteuning voor Power shell installeert op een computer waarop de Configuration Manager-console wordt uitgevoerd, kunt u Power shell-cmdlets uitvoeren op die computer om Configuration Manager te beheren.

- Power Shell 3,0 of hoger wordt ondersteund

Naast Power shell wordt Windows Management Framework (WMF) versie 3,0 of hoger ondersteund.   


##  <a name="lab-deployments"></a><a name="bkmk_ScaleLab"></a>Lab-implementaties  
Gebruik de volgende minimale hardwarevereisten voor Lab-en test implementaties van Configuration Manager. Deze aanbevelingen zijn van toepassing op alle site typen, Maxi maal 100 clients:  

|Rol|CPU (kern geheugens)|Geheugen (GB)|Schijfruimte (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Site- en databaseserver|2 - 4|8 - 12|100|  
|Sitesysteemserver|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  
