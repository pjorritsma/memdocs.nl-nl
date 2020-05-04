---
title: Hulp programma Registratie bijwerken
titleSuffix: Configuration Manager
description: Ontdek wanneer en hoe u het hulp programma voor het registreren van updates gebruikt om een update hand matig te importeren in de Configuration Manager-console.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 420b13005e8f9ac3d79f7d94398e6aa0ddcc190c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711236"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-configuration-manager"></a>Gebruik het hulp programma Registratie bijwerken om hotfixes te importeren naar Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Sommige updates voor Configuration Manager zijn niet beschikbaar in de micro soft-Cloud service en worden alleen out-of-band verkregen. Een voorbeeld is een beperkt uitgegeven hotfix voor een specifiek probleem.   
Wanneer u een out-of-band-versie moet installeren en de naam van de update of het hotfixbestand eindigt met de extensie **Update. exe**, gebruikt u het **hulp programma Registratie bijwerken** om de update hand matig te importeren in de Configuration Manager-console. Met het hulpprogramma kunt u het updatepakket uitpakken en overdragen naar de siteserver en de update registreren bij de Configuration Manager-console.  

 Als het hotfixbestand de extensie **. exe** heeft (niet **Update. exe**), raadpleegt u [het installatie programma voor hotfixes gebruiken om updates te installeren voor Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  In dit onderwerp vindt u algemene richt lijnen voor het installeren van hotfixes die Configuration Manager bijwerken. Raadpleeg voor meer informatie over een specifieke hotfix of update het betreffende Knowledge Base-artikel (KB) op Microsoft Ondersteuning.  

 **Vereisten voor het gebruik van het hulpprogramma Registratie bijwerken:**  

-   Alleen out-of-band-updates die eindigen met de extensie **. update. exe** kunnen worden geïnstalleerd met dit hulp programma  

-   Het hulp programma is zelf opgenomen in de afzonderlijke updates die u rechtstreeks van micro soft ontvangt  

-   Het hulpprogramma is niet afhankelijk van de modus van het serviceaansluitpunt  

-   Het hulpprogramma moet worden uitgevoerd op de computer die het serviceaansluitpunt host  

-   Op de computer waarop het hulp programma wordt uitgevoerd (de computer met het service verbindings punt) moet de .NET Framework 4,52 zijn geïnstalleerd  

-   Het account waarmee u het hulp programma uitvoert, moet over **lokale beheerders** machtigingen beschikken op de computer waarop het service verbindings punt wordt gehost (waarop het hulp programma wordt uitgevoerd)  

-   Het account waarmee u het hulp programma uitvoert, moet **Schrijf** machtigingen hebben voor de volgende map op de computer die als host fungeert voor het service verbindings punt: ** &lt;ConfigMgr-installatie directory\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Het hulpprogramma Registratie bijwerken gebruiken  

1. Op de computer die het serviceverbindingspunt host:  

   -   Open een opdracht prompt met beheerders bevoegdheden en wijzig de mappen in de locatie met ** &lt;\>-&lt;product\>-&lt;product versie KB artikel id\>-ConfigMgr. update. exe**  

2. Voer de volgende opdracht uit om het hulpprogramma Registratie bijwerken te openen:  

   -   **&lt;\>-Product&lt;\>product versie-KB artikel-\>id-ConfigMgr. update. exe&lt;**  

   Wanneer de hotfix is geregistreerd, wordt deze binnen 24 uur weergegeven als nieuwe update in de console.  U kunt het proces versnellen:

   - Open de Configuration Manager-console, ga naar **beheer** > **updates en onderhoud**en klik vervolgens op **controleren op updates**. (Vóór versie 1702 werden updates en onderhoud onder **beheer** > **Cloud Services**.) 

   Het hulpprogramma Registratie bijwerken registreert de uitgevoerde bewerkingen in een logboekbestand op de lokale computer. Het logboek bestand heeft dezelfde naam als het bestand hotfix. exe en wordt naar de map **% System root%/Temp** geschreven.  

    Wanneer de update is geregistreerd, kunt u het hulpprogramma Registratie bijwerken sluiten.  

3. Open de Configuration Manager-console en ga naar **beheer** > **updates en onderhoud**. De geïmporteerde hotfixes kunnen nu worden geïnstalleerd. (Vóór versie 1702 werden updates en onderhoud onder **beheer** > **Cloud Services**.)

   Zie [updates in de console installeren voor Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) voor meer informatie over het installeren van updates.  
