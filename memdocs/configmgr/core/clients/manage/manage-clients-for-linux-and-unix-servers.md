---
title: Linux-en UNIX-clients beheren
titleSuffix: Configuration Manager
description: Clients beheren op Linux-en UNIX-servers in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710641"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Clients voor Linux-en UNIX-servers beheren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients. 
> 
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

Wanneer u Linux-en UNIX-servers beheert met Configuration Manager, kunt u verzamelingen, onderhouds Vensters en client instellingen configureren om de servers te beheren. Hoewel de Configuration Manager-client voor Linux en UNIX geen gebruikers interface heeft, kunt u afdwingen dat de client hand matig op client beleid controleert.

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 Gebruik verzamelingen om groepen Linux-en UNIX-servers te beheren op dezelfde manier als u verzamelingen gebruikt voor het beheren van andere client typen. Verzamelingen kunnen directe lidmaatschaps verzamelingen of op query's gebaseerde verzamelingen zijn. Op query's gebaseerde verzamelingen identificeren client besturingssystemen, hardwareconfiguraties of andere details over de client die zijn opgeslagen in de site database. U kunt bijvoorbeeld verzamelingen gebruiken die Linux-en UNIX-servers omvatten om de volgende instellingen te beheren:  

- Clientinstellingen  

- Software-implementatie  

- Onderhoudsvensters afdwingen  

  Voordat u een Linux-of UNIX-client kunt identificeren aan de hand van het besturings systeem of de distributie, moet u [hardware-inventaris](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) van de client verzamelen.  

  De standaard client instellingen voor hardware-inventarisatie bevatten informatie over het besturings systeem van de client computer. U kunt de eigenschap **Bijschrift** van de klasse **Besturingssysteem** gebruiken voor het identificeren van het besturingssysteem van een Linux- of UNIX-server.  

  U kunt details weer geven over computers die de Configuration Manager-client voor Linux en UNIX uitvoeren in het knoop punt **apparaten** van de werk ruimte **activa en naleving** in de Configuration Manager-console. In de werk ruimte **activa en naleving** van de Configuration Manager-console kunt u de naam van het besturings systeem van elke computer weer geven in de kolom **besturings systeem** .  

  Standaard maken Linux- en UNIX-servers deel uit van de verzameling **Alle systemen** . U wordt aangeraden aangepaste verzamelingen te bouwen die alleen Linux-en UNIX-servers of een subset ervan bevatten. Met aangepaste verzamelingen kunt u bewerkingen beheren, zoals het implementeren van software of het toewijzen van client instellingen aan groepen van, zoals computers, zodat u het succes van een implementatie nauw keurig in het goede kan meten.   

  Wanneer u een aangepaste verzameling voor Linux- en UNIX-servers maakt, neem daarin dan lidmaatschapregelquery's op met het kenmerk Bijschrift voor het kenmerk Besturingssysteem. Zie [verzamelingen maken](../../../core/clients/manage/collections/create-collections.md)voor meer informatie over het maken van verzamelingen.  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 De Configuration Manager-client voor Linux-en UNIX-servers ondersteunt het gebruik van [onderhouds Vensters](../../../core/clients/manage/collections/use-maintenance-windows.md). Deze ondersteuning is ongewijzigd ten opzichte van Windows-clients.  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 U kunt [client instellingen](../../../core/clients/deploy/configure-client-settings.md) die van toepassing zijn op Linux-en UNIX-servers op dezelfde manier configureren als u instellingen voor andere clients configureert.  

 **Standaard clientagentinstellingen** is standaard van toepassing op Linux- en UNIX-servers. U kunt ook aangepaste client instellingen maken en deze implementeren in verzamelingen specifieke clients.  

 Er zijn geen aanvullende clientinstellingen die alleen van toepassing zijn op Linux- en UNIX-clients. Er zijn echter standaard client instellingen die niet van toepassing zijn op Linux-en UNIX-clients. De-client voor Linux en UNIX past alleen instellingen toe voor functionaliteit die wordt ondersteund.  

 Zo kan een aangepaste instelling voor client apparaat waarmee instellingen voor beheer op afstand worden ingeschakeld en geconfigureerd, worden genegeerd door de Linux-en UNIX-servers, omdat de client voor Linux en UNIX geen ondersteuning biedt voor extern beheer.  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a>Computer beleid voor Linux-en UNIX-servers  
 De-client voor Linux-en UNIX-servers pollt regel matig de site voor computer beleid om meer te weten te komen over de aangevraagde configuraties en om te controleren op implementaties.  

 Ook kunt u de client op een Linux- of UNIX-server dwingen onmiddellijk naar computerbeleid te pollen. Als u dit wilt doen, gebruikt u **hoofd** referenties op de server om de volgende opdracht uit te voeren: **/opt/Microsoft/ConfigMgr/bin/ccmexec-RS-beleid**  

 Details over de computerbeleidpoll worden ingevoerd in het logboekbestand van de gedeelde client; **scxcm.log**.  

> [!NOTE]  
>  De Configuration Manager-client voor Linux en UNIX vraagt nooit naar gebruikers beleid of verwerkt deze.  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a>Certificaten beheren op de client voor Linux en UNIX  
 Nadat u de client voor Linux en UNIX hebt geïnstalleerd, kunt u het hulpprogramma **certutil** gebruiken om de client bij te werken met een nieuw PKI-certificaat, en om een nieuwe certificaatintrekkingslijst (CRL) te importeren. Wanneer u de-client voor Linux en UNIX installeert, wordt dit hulp programma `/opt/microsoft/configmgr/bin/certutil`geplaatst in. 

 Om certificaten te beheren, voert u elke client certutil met een van de volgende opties uit:  

|Optie|Meer informatie|  
|------------|----------------------|  
|`importPFX`|Gebruik deze optie om een certificaat op te geven ter vervanging van het certificaat dat momenteel door een client wordt gebruikt.<br /><br /> Wanneer u gebruikt `-importPFX`, moet u ook de `-password` opdracht regel parameter gebruiken om het wacht woord op te geven dat is gekoppeld aan het PKCS # 12-bestand.<br /><br /> Gebruik `-rootcerts` om aanvullende vereisten voor basis certificaten op te geven.<br /><br /> Voorbeeld: `certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|Gebruik deze optie om het ondertekeningscertificaat voor de siteserver bij te werken dat zich op beheerserver bevindt.<br /><br /> Voorbeeld: `certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|Gebruik deze optie om de certificaatintrekkingslijst op de client bij te werken met een of meer paden naar certificaatintrekkingslijstbestanden.<br /><br /> Voorbeeld: `certutil -importcrl <comma separated CRL file paths>`|  
