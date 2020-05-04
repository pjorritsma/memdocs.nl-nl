---
title: Linux/UNIX-clients bewaken
titleSuffix: Configuration Manager
description: Controleer clients op Linux-en UNIX-servers in Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2ea3a0b630e1710aeaf74a4349f202806d45039
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715359"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Clients controleren voor Linux-en UNIX-servers in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients. 
> 
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

U kunt informatie weer geven van Linux-en UNIX-servers in de Configuration Manager-console met dezelfde methoden die u gebruikt om informatie weer te geven van Windows-clients.  

 U kunt de volgende gegevens bekijken:  

- Status gegevens van clients, in de Dash boards van de Configuration Manager-console  

- Details over clients in de standaard Configuration Manager rapporten  

- Inventarisgegevens in Resource Explorer  

  In de volgende secties wordt beschreven hoe u deze gegevens ophaalt uit resource Explorer en-rapporten.  

##  <a name="use-resource-explorer-to-view-inventory-for-linux-and-unix-servers"></a><a name="BKMK_UseResourceExpforLnU"></a>Resource Explorer gebruiken om de inventaris voor Linux-en UNIX-servers weer te geven  

 Nadat een Configuration Manager-client Hardware-inventarisatie naar de Configuration Manager-site heeft verzonden, kunt u resource Explorer gebruiken om deze gegevens weer te geven. Met de Configuration Manager-client voor Linux en UNIX worden geen nieuwe klassen of weer gaven voor de inventaris toegevoegd aan resource Explorer. De Linux- en UNIX-inventarisgegevens zijn gekoppeld aan bestaande WMI-klassen. U kunt de inventarisgegevens voor Linux- en UNIX-servers met Resource Explorer bekijken in de Windows-classificaties.  

 U kunt bijvoorbeeld de lijst met alle systeemeigen geïnstalleerde programma's op uw Linux- en UNIX-servers verzamelen. Voorbeelden van systeemeigen geïnstalleerde programma's zijn **.rpms** in Linux of **.pkgs** in Solaris. Nadat de inventarisatie is verzonden door een Linux-of UNIX-client, kunt u de lijst met alle systeem eigen geïnstalleerde Linux-of UNIX-Program ma's bekijken in resource Explorer in de Configuration Manager-console.  

 Zie [resource Explorer gebruiken om de hardware-inventaris te bekijken](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)voor meer informatie over het gebruik van resource Explorer.  

##  <a name="how-to-use-reports-to-view-information-for-linux-and-unix-servers"></a><a name="BKMK_UseReportsforLnU"></a> Rapporten gebruiken om gegevens over Linux- en UNIX-servers te bekijken  
 Rapporten voor Configuration Manager bevatten informatie van Linux-en UNIX-servers samen met informatie van Windows-computers. Er zijn geen aanvullende configuraties nodig om de Linux- en UNIX-gegevens in de rapporten te integreren.  

 Als u bijvoorbeeld het rapport met de naam Aantal besturingssysteemversies uitvoert, wordt er een lijst weergegeven met de verschillende besturingssystemen en het aantal clients waarop elk besturingssysteem wordt uitgevoerd. Het rapport is gebaseerd op de hardware-inventarisatie gegevens die zijn verzonden door de verschillende Configuration Manager-clients die worden uitgevoerd op de verschillende besturings systemen.  

 Het is ook mogelijk om aangepaste rapporten te maken die specifiek zijn voor Linux-en UNIX-server gegevens. De eigenschap **Bijschrift** van de hardware-inventarisklasse **Besturingssysteem** is een nuttig kenmerk waarmee u de specifieke besturingssystemen kunt aangeven in de rapportquery.  

 Zie [Introduction to Reporting](../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over rapporten in Configuration Manager.  
