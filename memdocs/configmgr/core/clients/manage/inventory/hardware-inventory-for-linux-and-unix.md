---
title: Hardware-inventaris voor Linux en UNIX
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van hardware-inventaris voor Linux en UNIX in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f4b822475111352c5dcf23f4868a1fa43ec3a7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906275"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Hardware-inventaris voor Linux en UNIX in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients. 
> 
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

De Configuration Manager-client voor Linux en UNIX ondersteunt hardware-inventaris. Nadat u de hardware-inventaris hebt verzameld, kunt u de weer gave-inventarisatie uitvoeren in resource Explorer of Configuration Manager rapporten en deze informatie gebruiken om query's en verzamelingen te maken die de volgende bewerkingen inschakelen:  

- Software-implementatie  

- Onderhoudsvensters afdwingen  

- Aangepaste clientinstellingen implementeren  

Hardware-inventaris voor Linux-en UNIX-servers maakt gebruik van een op standaarden gebaseerde Common Information Model (CIM)-server. De CIM-server wordt uitgevoerd als een softwareservice (of daemon) en biedt een infrastructuur die is gebaseerd op standaarden voor DMTF (Distributed Management Task Force). De CIM-server biedt functionaliteit die vergelijkbaar is met de CIM-mogelijkheden van WMI (Windows Management Infrastructure) die beschikbaar zijn op Windows-computers.  

Vanaf cumulatieve update 1 gebruikt de client voor Linux en UNIX de open-source **omiserver** versie 1.0.6 uit de **geopende groep**. (Voor cumulatieve update 1 gebruikte de client **nanowbem** als CIM-server).  

De CIM-server wordt geïnstalleerd als onderdeel van de client voor Linux en UNIX. De client voor Linux en UNIX communiceert rechtstreeks met de CIM-server en maakt geen gebruik van de WS-MAN-interface van de CIM-server. De WS-MAN-poort op de CIM-server wordt uitgeschakeld als de client wordt geïnstalleerd. Microsoft ontwikkelde de CIM-server die nu als open source beschikbaar is via het OMI-project (Open Management Infrastructure). Zie de website [The Open Group](https://www.opengroup.org/) over het Open Management Infrastructure Project voor meer informatie.  

Hardware-inventaris op Linux- en UNIX-servers werkt via het toewijzen van bestaande Win32 WMI-klassen en eigenschappen aan gelijkwaardige klassen en eigenschappen voor Linux- en UNIX-servers. Deze een-op-een-toewijzing van klassen en eigenschappen maakt het mogelijk Linux en UNIX hardware-inventaris te integreren met Configuration Manager. Inventaris gegevens van Linux-en UNIX-servers worden samen met de inventaris van op Windows gebaseerde computers weer gegeven in de Configuration Manager-console en rapporten. Dit gedrag biedt een consistente heterogene beheer ervaring.  

> [!TIP]  
>  U kunt de waarde **Bijschrift** voor de klasse **Besturingssysteem** gebruiken voor het identificeren van verschillende Linux- en UNIX-besturingssystemen in query's en verzamelingen.  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> Hardware-inventaris voor Linux- en UNIX-servers configureren  
 U kunt de standaardclientinstellingen gebruiken of aangepaste clientapparaatinstellingen maken om de hardware-inventaris te configureren. Wanneer u aangepaste instellingen voor client apparaten gebruikt, kunt u de klassen en eigenschappen configureren die u alleen van uw Linux-en UNIX-servers wilt verzamelen. U kunt ook aangepaste schema's opgeven wanneer u de volledige inventaris en delta-inventaris van uw Linux- en UNIX-servers wilt verzamelen.  

 De client voor Linux en UNIX ondersteunt de volgende hardware-inventarisklassen die beschikbaar op Linux- en UNIX-servers:  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

Niet alle eigenschappen voor deze inventaris klassen zijn ingeschakeld voor Linux-en UNIX-computers in Configuration Manager.  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> Bewerkingen voor hardware-inventaris  
 Nadat u de hardware-inventaris van uw Linux- en UNIX-servers hebt verzameld, kunt u deze informatie op dezelfde manier bekijken en gebruiken als de inventaris die u verzamelt van andere computers:  

- Gebruik Resource Explorer om gedetailleerde informatie weer te geven over de hardware-inventaris die wordt verzameld van Linux- en UNIX-servers.  

- Query's op basis van specifieke hardwareconfiguraties maken  

- Op query’s gebaseerde verzamelingen maken die zijn gebaseerd op specifieke hardwareconfiguraties  

- Rapporten met specifieke details over hardwareconfiguraties uitvoeren  

Hardware-inventaris op een Linux- of UNIX-server wordt uitgevoerd volgens de planning die u in de clientinstellingen configureert. Deze planning is standaard elke zeven dagen. De client voor Linux en UNIX ondersteunt zowel volledige inventarisatiecycli als delta-inventarisatiecycli.  

Ook kunt u de client op een Linux- of UNIX-server dwingen onmiddellijk hardware-inventaris uit te voeren. Als u hardware-inventarisatie wilt uitvoeren, moet u op een client **hoofd** referenties gebruiken om de volgende opdracht uit te voeren om een hardware-inventarisatie cyclus te starten:`/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

Acties voor hardware-inventaris worden ingevoerd in het logboekbestand van de client, **scxcm.log**.  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> Open Management Infrastructure gebruiken om aangepaste een hardware-inventaris te maken  
 De client voor Linux en UNIX ondersteunt aangepaste hardware-inventaris die u kunt maken met behulp van de Open Management Infrastructure (OMI). U kunt dit doen door de volgende stappen uit te voeren:  

1.  Een aangepaste inventarisprovider maken met de OMI-bron  

2.  Computers configureren voor het gebruik van de nieuwe provider voor inventarisrapportage  

3.  Configuration Manager inschakelen voor de ondersteuning van de nieuwe provider  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> Een aangepaste hardware-inventarisprovider maken voor Linux- en UNIX-computers.  
 Als u een aangepaste hardware-inventaris provider wilt maken voor de Configuration Manager-client voor Linux en UNIX, gebruikt u **Omi source-v. 1.0.6** en volgt u de instructies in de hand leiding aan de slag met Omi. Met dit proces maakt u een Managed Object Format-bestand waarmee u het schema van de nieuwe provider definieert. Later importeert u het MOF-bestand naar Configuration Manager om ondersteuning van de nieuwe aangepaste inventaris klasse in te scha kelen.  

 U kunt de OMI Source - v.1.0.6 en de introductiehandleiding voor OMI downloaden van de website [The Open Group](https://github.com/microsoft/omi/blob/master/README.md) . U vindt deze downloads op het tabblad **Documenten** op de volgende webpagina op de website OpenGroup.org: [Open Management Infrastructure (OMI)](https://collaboration.opengroup.org/omi/).  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> Configureer elke computer met Linux of UNIX met de aangepaste hardware-inventarisprovider:  
 Nadat u een aangepaste inventarisprovider hebt gemaakt, moet u het providerbibliotheekbestand kopiëren naar en registreren op elke computer waarvan u de inventaris wilt verzamelen.  

1.  Kopieer de providerbibliotheek naar elke Linux- en UNIX-computer waarvan u de inventaris wilt verzamelen. De naam van de provider bibliotheek lijkt op de volgende naam: **XYZ_MyProvider. so**  

2.  Registreer vervolgens de providerbibliotheek op elke Linux- en UNIX-computer bij de OMI-server. De OMI-server wordt op de computer geïnstalleerd wanneer u de Configuration Manager-client voor Linux en UNIX installeert, maar u moet de aangepaste providers hand matig registreren. Gebruik de volgende opdracht regel om de provider te registreren:`/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  Nadat u de nieuwe provider hebt geregistreerd, test u de provider met behulp van het **omicli** -hulpprogramma. Het hulp programma **omicli** wordt op elke Linux-en UNIX-computer geïnstalleerd wanneer u de Configuration Manager-client voor Linux en UNIX installeert. Voorbeeld: als **XYZ_MyProvider** de naam is van de provider die u hebt gemaakt, voert u de volgende opdracht op de computer: **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     voor informatie over **omicli** het testen van aangepaste providers.  

> [!TIP]  
>  Gebruik softwaredistributie om de aangepaste providers te implementeren en om aangepaste providers op elke Linux- en UNIX-clientcomputer te registreren.  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> Schakel de nieuwe inventarisklasse in Configuration Manager in:  
 Voordat Configuration Manager kunt rapporteren over de inventaris die door de nieuwe provider op Linux-en UNIX-computers wordt gerapporteerd, moet u het Managed Object Format (MOF)-bestand importeren dat het schema van uw aangepaste provider definieert.  

 Zie [hardware-inventaris configureren voor meer informatie over](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)het importeren van een aangepast MOF-bestand in Configuration Manager.  
