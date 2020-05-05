---
title: Downloadprogramma voor het installatieprogramma
titleSuffix: Configuration Manager
description: Meer informatie over deze zelfstandige toepassing, die is bedoeld om ervoor te zorgen dat uw site-installatie gebruikmaakt van de huidige versies van de sleutel installatie bestanden.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2fa1899f8e7dc14812f9f9ecf889350a153b2d25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718075"
---
# <a name="setup-downloader-for-configuration-manager"></a>Download programma instellen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u het installatie programma uitvoert om een Configuration Manager site te installeren of bij te werken, kunt u de zelfstandige toepassing voor installatie van Downloader gebruiken uit de versie van Configuration Manager die u wilt installeren om bijgewerkte Setup-bestanden te downloaden.  

Met behulp van bijgewerkte installatie bestanden zorgt u ervoor dat uw site-installatie gebruikmaakt van de huidige versies van de sleutel installatie bestanden. In oveview:   
-   Wanneer u het download programma voor de installatie van gebruikt om bestanden te downloaden voordat u het installatie programma start, geeft u een map op waarin de bestanden moeten worden opgeslagen.  
-   Het account waarmee u het download programma voor de installatie uitvoert, moet machtigingen voor **volledig beheer** hebben voor de downloadmap.  
-   Wanneer u het installatie programma uitvoert om een site te installeren of bij te werken, kunt u het gebruiken om deze lokale kopie van bestanden die u eerder hebt gedownload. Hiermee wordt voor komen dat het installatie formulier verbinding kan maken met micro soft wanneer u de installatie of upgrade van de site start.  
-   U kunt dezelfde lokale kopie van de installatie bestanden gebruiken voor de volgende site-installaties of-upgrades.  

De volgende typen bestanden worden gedownload door het download programma voor de installatie:  
-   Vereiste herdistribueerbare bestanden  
-   Taalpakketten  
-   De nieuwste product updates voor Setup  

U hebt twee opties voor het uitvoeren van Setup Downloader:
- De toepassing uitvoeren met de gebruikers interface
- Voor opdracht regel opties voert u de toepassing uit vanaf een opdracht prompt


## <a name="run-setup-downloader-with-the-user-interface"></a><a name="bkmk_ui"></a>Het download programma voor de installatie uitvoeren met de gebruikers interface  

1.  Op een computer met Internet toegang opent u Windows Verkenner en gaat u ** &lt;naar ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**.  

2.  Om het download programma voor de installatie te openen, dubbelklikt u op **Setupdl. exe**.   

3. Geef het pad op voor de map die als host moet fungeren voor de bijgewerkte installatie bestanden en klik vervolgens op **downloaden**. Setup Downloader verifieert de bestanden die zich momenteel in de downloadmap bevinden. Hiermee downloadt u alleen bestanden die ontbreken of die nieuwer zijn dan de bestaande bestanden. Setup Downloader maakt submappen voor gedownloade talen en andere vereiste submappen.  

4.  Als u de download resultaten wilt bekijken, opent u het bestand **ConfigMgrSetup. log** in de hoofdmap van station C.  .  

## <a name="run-setup-downloader-from-a-command-prompt"></a><a name="bkmk_cmd"></a>Het download programma voor de installatie uitvoeren vanaf een opdracht prompt  

1.  Ga ** &lt;in een opdracht prompt venster naar *Configuration Manager installation media*\>\SMSSETUP\BIN\X64**.   

2.  Als u het download programma wilt openen, voert u **Setupdl. exe**uit.

    U kunt de volgende opdracht regel opties gebruiken met **Setupdl. exe**:   

    -   **/Verify**: gebruik deze optie om de bestanden in de downloadmap te controleren, waaronder taal bestanden. Raadpleeg het bestand ConfigMgrSetup. log in de hoofdmap van station C voor een lijst met bestanden die verouderd zijn. Er worden geen bestanden gedownload wanneer u deze optie gebruikt.  

    -   **/VERIFYLANG**: gebruik deze optie om de taal bestanden in de downloadmap te controleren. Raadpleeg het bestand ConfigMgrSetup. log in de hoofdmap van station C voor een lijst met taal bestanden die verouderd zijn.

    -   **/Lang**: gebruik deze optie om alleen de taal bestanden te downloaden naar de downloadmap.  

    -   **/NOUI**: gebruik deze optie om het download programma voor de installatie te starten zonder de gebruikers interface weer te geven. Wanneer u deze optie gebruikt, moet u het **downloadmap** opgeven als onderdeel van de opdracht bij de opdracht prompt.  

    -   Downloadpad: u kunt het pad naar de downloadmap opgeven om de verificatie of het download proces automatisch te starten. ** &lt;\>** U moet het pad naar de down load opgeven wanneer u de **/NOUI** -optie gebruikt. Als u geen pad voor downloaden opgeeft, moet u het pad opgeven wanneer het download programma voor de installatie wordt geopend. Het download programma voor de installatie maakt de map als deze nog niet bestaat.  

    Voorbeeldopdrachten:

    -   **setupdl &lt;downloadpad\>**  

        -   Setup Downloader start, controleert de bestanden in de opgegeven downloadmap en downloadt alleen de bestanden die ontbreken of die nieuwere versies hebben dan bestaande bestanden.     

    -   **setupdl/VERIFY &lt;downloadpad\>**  

        -   Setup Downloader start en controleert de bestanden in de opgegeven downloadmap.  

    -   **setupdl/NOUI &lt;downloadpad\>**  

        -   Setup Downloader start, controleert de bestanden in de opgegeven downloadmap en downloadt alleen de bestanden die ontbreken of die nieuwer zijn dan de bestaande bestanden.  

    -   **setupdl/LANG &lt;downloadpad\>**  

        -   Setup Downloader start, controleert de taal bestanden in de opgegeven downloadmap en downloadt vervolgens alleen de taal bestanden die ontbreken of die nieuwer zijn dan de bestaande bestanden.  

    -   **setupdl/VERIFY**  

        -   Het download programma voor de installatie wordt gestart en vervolgens moet u het pad naar de downloadmap opgeven. Nadat u vervolgens op **verifiëren**hebt geklikt, controleert Setup Downloader de bestanden in de downloadmap.  

3.  Als u de download resultaten wilt bekijken, opent u het bestand **ConfigMgrSetup. log** in de hoofdmap van station C.

## <a name="copy-setup-downloader-files-to-another-computer"></a><a name="bkmk_cp-files"></a>Setup-Download bestanden kopiëren naar een andere computer

1. Ga in Windows Verkenner naar een van de volgende locaties:

    - **&lt;Configuration Manager installatie media> \SMSSETUP\BIN\X64**
    - **&lt;Configuration Manager installatiepad> \BIN\X64**
    
1. Kopieer de volgende bestanden naar dezelfde doelmap op de andere computer:
    
    - **setupdl. exe**
    - **. \\taal>\\setupdlres &lt;. dll**
      - Dit bestand bevindt zich in de submap voor de taal van de installatie. Bijvoorbeeld: Engels bevindt zich `00000409` in de submap.

    Als voor beeld moeten de doel mappen op het apparaat er als volgt uitzien:
    - C:\ConfigManInstall\setupdl.exe
    - C:\ConfigManInstall\00000409\setupdlres.dll

1. Start het download programma voor de installatie van de computer met behulp van de [gebruikers interface](#bkmk_ui) of de [opdracht prompt](#bkmk_cmd), zoals beschreven in de bovenstaande secties.
