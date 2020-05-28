---
title: Hulp programma Setup Downloader
titleSuffix: Configuration Manager
description: Gebruik het zelfstandige hulp programma om de huidige versies van de sleutel installatie bestanden voor installatie te downloaden.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2da8aed5cfe4a478010165445094f1fce4627d9a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428836"
---
# <a name="setup-downloader-for-configuration-manager"></a>Download programma instellen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u Configuration Manager Setup uitvoert om een site te installeren of bij te werken, kunt u het zelfstandige hulp programma voor de installatie van Downloader gebruiken om bijgewerkte Setup-bestanden te downloaden. Voer het hulp programma uit vanaf de versie van Configuration Manager die u wilt installeren. Gebruik bijgewerkte installatie bestanden om te controleren of uw site-installatie de huidige versies van de sleutel installatie bestanden gebruikt.

Wanneer u het download programma voor de installatie gebruikt, geeft u een map op waarin de bestanden moeten worden opgeslagen. Het account dat u gebruikt om het hulp programma uit te voeren, moet machtigingen voor **volledig beheer** hebben voor de downloadmap. Wanneer u het installatie programma uitvoert om een site te installeren of bij te werken, kunt u deze lokale kopie opgeven van bestanden die u eerder hebt gedownload. Dit gedrag zorgt ervoor dat Setup geen verbinding kan maken met micro soft wanneer u de installatie of upgrade van de site start. U kunt dezelfde lokale kopie van installatie bestanden gebruiken voor andere site-installaties of-upgrades van dezelfde versie.

Het hulp programma Setup Downloader downloadt de volgende typen bestanden:

- Vereiste herdistribueerbare bestanden
- Taalpakketten
- De nieuwste product updates voor Setup

U hebt twee opties om Setup Downloader uit te voeren:

- De toepassing uitvoeren met de gebruikers interface
- Voer de toepassing uit vanaf een opdracht prompt voor aanvullende opdracht regel opties

Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u het hulp programma toegang geven tot internet-eind punten. Op het apparaat waarop u het hulp programma uitvoert, moet Internet toegang hetzelfde zijn als het service verbindings punt. Zie [vereisten voor Internet toegang](../../../plan-design/network/internet-endpoints.md#bkmk_scp)voor meer informatie.<!-- SCCMDocs#677 -->

## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Het download programma voor de installatie uitvoeren met de gebruikers interface

1. Op een computer met Internet toegang, bladert u naar de installatie media voor de versie van Configuration Manager die u wilt installeren.

1. Voer **Setupdl. exe**in de submap **SMSSETUP\BIN\X64** uit.

1. Geef het pad op voor de map waarin de bijgewerkte installatie bestanden moeten worden opgeslagen en selecteer vervolgens **downloaden**. Setup Downloader verifieert de bestanden die zich momenteel in de downloadmap bevinden. Hiermee downloadt u alleen bestanden die ontbreken of die nieuwer zijn dan de bestaande bestanden. Er worden submappen gemaakt voor gedownloade talen en andere vereiste onderdelen.

1. Zie **C:\ConfigMgrSetup.log**om de download resultaten te bekijken.

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Het download programma voor de installatie uitvoeren vanaf een opdracht prompt

1. Open een opdracht prompt en wijzig de map naar het installatie medium voor de versie van Configuration Manager die u wilt installeren.

1. Wijzig de map in de submap **SMSSETUP\BIN\X64** en voer **Setupdl. exe** uit met de opties die nodig zijn.

1. Zie **C:\ConfigMgrSetup.log**om de download resultaten te bekijken.

### <a name="command-line-options"></a>Opdrachtregelopties

U kunt de volgende opdracht regel opties gebruiken met **Setupdl. exe**:

- **/Verify**: Controleer de bestanden in de downloadmap, met inbegrip van taal bestanden. Raadpleeg **C:\ConfigMgrSetup.log**voor de lijst met verouderde bestanden. Wanneer u deze optie gebruikt, worden er geen bestanden gedownload.

- **/VERIFYLANG**: Controleer alleen de taal bestanden in de downloadmap. Raadpleeg **C:\ConfigMgrSetup.log**voor de lijst met verouderde taal bestanden.

- **/Lang**: down load alleen de taal bestanden naar de downloadmap.

- **/NOUI**: Start de installatie-Downloader zonder de gebruikers interface. Wanneer u deze optie gebruikt, is het **pad naar de down load** vereist.

- **Pad voor downloaden**: Geef het pad naar de downloadmap op om de verificatie of het download proces automatisch te starten. Wanneer u de optie **/NOUI** gebruikt, is het pad naar de down load vereist. Als u geen pad naar een down load opgeeft, wordt u door het download programma gevraagd het pad op te geven. Als de map nog niet bestaat, wordt deze gemaakt door het download programma voor de installatie.

### <a name="example-commands"></a>Voorbeeldopdrachten

#### <a name="example-1"></a>Voorbeeld 1

Setup Downloader verifieert de bestanden in de opgegeven downloadmap en downloadt vervolgens bestanden.

`setupdl.exe C:\Download`

#### <a name="example-2"></a>Voorbeeld 2

Met het download programma voor installatie worden alleen de bestanden in de opgegeven downloadmap gecontroleerd.

`setupdl.exe /VERIFY C:\Download`

#### <a name="example-3"></a>Voorbeeld 3

Setup Downloader verifieert de bestanden in de opgegeven downloadmap en downloadt vervolgens bestanden. Er wordt geen gebruikers interface weer gegeven in het hulp programma.

`setupdl.exe /NOUI C:\Download`

#### <a name="example-4"></a>Voorbeeld 4

Setup Downloader controleert de taal bestanden in de opgegeven downloadmap en downloadt vervolgens alleen de taal bestanden.

`setupdl.exe /LANG C:\Download`

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Setup-Download bestanden kopiëren naar een andere computer

1. Ga in Windows Verkenner naar een van de volgende locaties:

    - **&lt;Configuration Manager installatie media> \SMSSETUP\BIN\X64**

    - **&lt;Configuration Manager installatiepad> \BIN\X64**

1. Kopieer de volgende bestanden naar dezelfde doelmap op de andere computer:

    - **setupdl. exe**

    - **.\\&lt; taal > \\ setupdlres. dll**

        > [!NOTE]
        > Dit bestand bevindt zich in de submap voor de taal van de installatie. Bijvoorbeeld: Engels bevindt zich in de `00000409` submap.

    De doel mappen op het apparaat moeten eruitzien zoals in het volgende voor beeld:

    - `C:\ConfigManInstall\setupdl.exe`

    - `C:\ConfigManInstall\00000409\setupdlres.dll`

1. Voer het download programma voor de installatie van de doel computer uit. Gebruik de [gebruikers interface](#bkmk_ui) of de [opdracht prompt](#bkmk_cmd).
