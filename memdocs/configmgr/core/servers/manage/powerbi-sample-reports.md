---
title: Power BI-voorbeeldrapporten installeren
titleSuffix: Configuration Manager
description: Meer informatie over het installeren van de Power BI-voorbeeld rapporten in Configuration Manager
ms.date: 08/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 025788a4ed4a26123f24ec667348eae97821295e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699684"
---
# <a name="install-power-bi-sample-reports"></a>Power BI-voorbeeldrapporten installeren
<!--5679791-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Vanaf versie 2002 kunt u [Power bi Report Server](/power-bi/report-server/get-started) integreren met Configuration Manager-rapportage. Er zijn voorbeeld rapporten beschikbaar voor down loads die u in Configuration Manager kunt installeren. In dit artikel wordt uitgelegd hoe u de Power BI voorbeeld rapporten kunt installeren in Configuration Manager.

## <a name="prerequisites"></a>Vereisten

- Configuration Manager Reporting Services-punt met [Power bi Report Server geïntegreerd](powerbi-report-server.md)

- [Micro soft power bi Desktop (geoptimaliseerd voor Power bi Report Server-September 2019)](https://www.microsoft.com/download/details.aspx?id=57271)of hoger

- Het [Update pakket (4560496) voor versie 2002](https://support.microsoft.com/help/4560496) wordt aanbevolen, maar is niet vereist.

    > [!IMPORTANT]
    > Gebruik alleen versies van Power BI Desktop van het [micro soft Download centrum](https://www.microsoft.com/download/). Gebruik geen versie van de Microsoft Store.
    >
    > Gebruik alleen een versie van Power BI Desktop die is [geoptimaliseerd voor Power bi Report Server](/power-bi/report-server/install-powerbi-desktop).

## <a name="download-the-sample-reports"></a>De voorbeeld rapporten downloaden

De voorbeeld rapporten downloaden:

1. De voorbeeld rapporten van Power BI downloaden van het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=101452).

1. Sla het bestand `ConfigMgrSamplePowerBIReports.exe` op.

1. Verplaats het bestand naar een computer met micro soft Power BI Desktop (geoptimaliseerd voor Power BI Report Server) geïnstalleerd als u het hebt gedownload vanaf een ander apparaat.

1. Voer het `ConfigMgrSamplePowerBIReports.exe` bestand uit om de. pbit-bestanden uit te pakken.

## <a name="install-the-sample-reports"></a>De voorbeeld rapporten installeren

De voorbeeld rapporten installeren:

1. Maak op de Power BI rapport server een nieuwe map `Sample Reports` met de naam in de map root Configuration Manager Reporting.

    :::image type="content" source="media/create-sample-reports-folder.png" alt-text="De map voor het voorbeeld rapport wordt gemaakt in de map root Configuration Manager Reporting van " lightbox="media/create-sample-reports-folder.png":::

1. Start micro soft Power BI Desktop (geoptimaliseerd voor Power BI Report Server).

1. Selecteer **bestand** en vervolgens **openen** en navigeer naar de locatie waar u de uitgepakte. pbit-bestanden hebt opgeslagen.

1. Selecteer een van de. pbit-bestanden die u uit het `ConfigMgrSamplePowerBIReports.exe` bestand hebt geëxtraheerd.

1. Geef de naam van uw Configuration Manager database en de database server op wanneer u hierom wordt gevraagd en selecteer vervolgens **laden**.

    :::image type="content" source="media/sample-report-database.png" alt-text="De naam van de data base en database server opgeven" lightbox="media/sample-report-database.png":::

    > [!NOTE]
    > Wanneer u het gegevens model laadt of toepast, negeert u eventuele fouten als u er een hebt. Als u bijvoorbeeld de volgende fout ziet: ' verbinding maken met tabellen vanuit meer dan één Data Base wordt niet ondersteund in de DirectQuery-modus ', selecteert u **sluiten**. Vernieuw vervolgens de instellingen voor de gegevens Bron:
    >
    > 1. Selecteer in Power BI Desktop in het lint de optie **Query's bewerken**en selecteer vervolgens **gegevens bron instellingen**.
    > 1. Selecteer **Bron wijzigen**, bevestig de namen van de server en de data base en selecteer **OK**.
    > 1. Sluit het venster instellingen voor gegevens bron en selecteer vervolgens **wijzigingen Toep assen**.

1. Wanneer de rapport gegevens zijn geladen, selecteert u **bestand**  >  **Opslaan als**en selecteert u **Power bi Report Server**.

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Opslaan als Power BI Report Server" lightbox="media/save-powerbi-report-server.png":::

1. Sla het rapport op naar de `Sample Reports` map die u hebt gemaakt op het rapportage punt.

    :::image type="content" source="media/save-sample-report.png" alt-text="Opslaan in de map met voorbeeld rapporten" lightbox="media/save-sample-report.png":::

1. Herhaal de stappen voor andere voorbeeld rapporten. Wanneer u klaar bent, sluit u micro soft Power BI Desktop (geoptimaliseerd voor Power BI Report Server).

1. Ga in de Configuration Manager-console naar **controle**  >  **rapporten Power bi rapporten**  >  **Sample Reports**.

1. Klik met de rechter muisknop op een van de rapporten en selecteer **uitvoeren in browser** om het rapport te starten.

    :::image type="content" source="media/view-powerbi-report.png" alt-text="Het voorbeeld rapport uitvoeren vanuit de Configuration Manager-console" lightbox="media/view-powerbi-report.png":::