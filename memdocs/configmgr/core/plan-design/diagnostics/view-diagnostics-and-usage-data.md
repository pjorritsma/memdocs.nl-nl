---
title: Diagnostische gegevens weer geven
titleSuffix: Configuration Manager
description: Diagnostische en gebruiks gegevens weer geven om te bevestigen dat uw Configuration Manager-hiërarchie geen gevoelige informatie bevat.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 993a3549ddca4c2b5ae1dbbfc0346f28b9c3083e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712538"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-configuration-manager"></a>Diagnostische en gebruiks gegevens weer geven voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt Diagnostische en gebruiks gegevens uit uw Configuration Manager-hiërarchie weer geven om te bevestigen dat deze geen gevoelige of herken bare informatie bevat. De site bevat een samen vatting van de diagnostische gegevens en slaat deze op in de tabel **TEL_TelemetryResults** van de site database. De gegevens worden zo opgemaakt dat ze programmatisch bruikbaar en efficiënt zijn.

De informatie in dit artikel geeft een overzicht van de exacte gegevens die naar micro soft worden verzonden. Het is niet bedoeld om te worden gebruikt voor andere doel einden, zoals gegevens analyse.  

## <a name="view-data-in-database"></a>Gegevens weer geven in data base

Gebruik de volgende SQL-opdracht om de inhoud van deze tabel weer te geven en de exacte gegevens weer te geven die worden verzonden:  

``` SQL
SELECT * FROM TEL_TelemetryResults
```

## <a name="export-the-data"></a>De gegevens exporteren

Wanneer het service verbindings punt zich in de offline modus bevindt, gebruikt u het hulp programma voor service verbindingen om de huidige gegevens te exporteren naar een bestand met door komma's gescheiden waarden (CSV). Voer het hulp programma voor service verbindingen op het service aansluitpunt uit met de para meter **-export** .

Zie [het hulp programma voor service verbindingen gebruiken](../../servers/manage/use-the-service-connection-tool.md)voor meer informatie.

## <a name="one-way-hashes"></a><a name="bkmk_hashes"></a>Eenrichtings-hashes

Sommige gegevens bestaan uit teken reeksen van wille keurige alfanumerieke tekens. Configuration Manager maakt gebruik van de algoritme SHA-256 voor het maken van eenrichtings-hashes. Dit proces zorgt ervoor dat micro soft geen potentieel gevoelige gegevens verzamelt. De gehashte gegevens kunnen nog steeds worden gebruikt voor correlatie-en vergelijkings doeleinden.

In plaats van de namen van tabellen in de site database te verzamelen, wordt de eenrichtings-hash voor elke tabel naam vastgelegd. Dit gedrag zorgt ervoor dat eventuele aangepaste tabel namen niet zichtbaar zijn. Micro soft voert vervolgens hetzelfde eenrichtings hash-proces uit voor de standaard SQL-tabel namen. Als u de resultaten van de twee query's vergelijkt, wordt de afwijking van het database schema van de standaard waarde van het product bepaald. Deze informatie wordt vervolgens gebruikt om updates te verbeteren waarvoor wijzigingen in het SQL-schema zijn vereist.  

Wanneer u de onbewerkte gegevens bekijkt, wordt een gemeen schappelijke gehashte waarde weer gegeven in elke rij gegevens. Deze hash is de hiërarchie-ID. Het wordt gebruikt voor het correleren van gegevens met dezelfde hiërarchie zonder de klant of bron te identificeren.

### <a name="how-the-one-way-hash-works"></a>Hoe de eenrichtings-hash werkt

1. Haal uw hiërarchie-ID op door de volgende SQL-query uit te voeren in SQL Management Studio op de Configuration Manager-Data Base:

    ``` SQL
    select [dbo].[fnGetHierarchyID]()
    ```

2. Gebruik het volgende Windows Power shell-script om de eenrichtings-hash van uw hiërarchie-ID uit te voeren.  

    ``` PowerShell
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()
    # Hash the input
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)
    # Base64 encode the result for transport
    $result = [Convert]::ToBase64String($hashedBytes)
    return $result
    ```

3. Vergelijk de script uitvoer met de GUID in de onbewerkte gegevens. Dit proces laat zien hoe de gegevens worden verborgen.

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Niveaus van diagnostische gebruiks gegevens](levels-overview.md)
