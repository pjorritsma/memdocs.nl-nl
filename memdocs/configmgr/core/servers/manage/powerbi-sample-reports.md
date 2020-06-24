---
title: Voorbeeld rapporten van Power BI installeren
titleSuffix: Configuration Manager
description: Meer informatie over het installeren van de Power BI-voorbeeld rapporten in Configuration Manager
ms.date: 06/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 340f10a486594f78053dcfd0febde40bb5a6697f
ms.sourcegitcommit: c5c17af545fd9df94f9b99fd44b56f10ff1f695e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/24/2020
ms.locfileid: "85310636"
---
# <a name="install-power-bi-sample-reports"></a>Voorbeeld rapporten van Power BI installeren
<!--5679791-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

Vanaf versie 2002 kunt u [Power bi Report Server](https://docs.microsoft.com/power-bi/report-server/get-started) integreren met Configuration Manager-rapportage. Er zijn voorbeeld rapporten beschikbaar voor down loads die u in Configuration Manager kunt installeren. In dit artikel wordt uitgelegd hoe u de Power BI voorbeeld rapporten kunt installeren in Configuration Manager.

## <a name="prerequisites"></a>Vereisten

- Configuration Manager Reporting Services-punt met [Power bi Report Server geïntegreerd](powerbi-report-server.md)
- [Micro soft power bi Desktop (geoptimaliseerd voor Power bi Report Server-September 2019)](https://www.microsoft.com/download/details.aspx?id=57271)of hoger

    > [!IMPORTANT]
    > - Gebruik alleen versies van Power BI Desktop van het [micro soft Download centrum](https://www.microsoft.com/download/), maar geen versie van de Microsoft Store.
    > - Gebruik alleen een versie van [Power bi Desktop die **voor Power bi Report Server is geoptimaliseerd**](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

## <a name="download-the-sample-reports"></a>De voorbeeld rapporten downloaden

De voorbeeld rapporten downloaden:

1. De voorbeeld rapporten van Power BI downloaden van het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=101452).
1. Sla het bestand `ConfigMgrSamplePowerBIReports.exe` op. 
1. Verplaats het bestand naar een computer met micro soft Power BI Desktop (geoptimaliseerd voor Power BI Report Server) geïnstalleerd als u het hebt gedownload vanaf een ander apparaat.
1. Voer het `ConfigMgrSamplePowerBIReports.exe` bestand uit om de. pbit-bestanden uit te pakken.

## <a name="install-the-sample-reports"></a>De voorbeeld rapporten installeren

De voorbeeld rapporten installeren:

1. Maak op de Power BI rapport server een nieuwe map `Sample Reports` met de naam in de map root Configuration Manager Reporting.
   
   :::image type="content" source="media/create-sample-reports-folder.png" alt-text="De map voor het voorbeeld rapport wordt gemaakt in de map root Configuration Manager Reporting van" lightbox="media/create-sample-reports-folder.png":::


1. Start micro soft Power BI Desktop (geoptimaliseerd voor Power BI Report Server).
1. Selecteer **bestand** en vervolgens **openen** en navigeer naar de locatie waar u de uitgepakte. pbit-bestanden hebt opgeslagen.
1. Selecteer een van de. pbit-bestanden die u uit het `ConfigMgrSamplePowerBIReports.exe` bestand hebt geëxtraheerd.
1. Geef de naam van uw Configuration Manager database en de database server op wanneer u hierom wordt gevraagd en selecteer vervolgens **laden**.
   - Wanneer u het gegevens model laadt of toepast, negeert u eventuele fouten als u er een hebt.
   
    :::image type="content" source="media/sample-report-database.png" alt-text="De naam van de data base en database server opgeven" lightbox="media/sample-report-database.png":::

1. Wanneer de rapport gegevens zijn geladen, selecteert u **bestand**  >  **Opslaan als**en selecteert u **Power bi Report Server**.
   
   :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Opslaan als Power BI Report Server" lightbox="media/save-powerbi-report-server.png":::

1. Sla het rapport op naar de `Sample Reports` map die u hebt gemaakt op het rapportage punt.
     
   :::image type="content" source="media/save-sample-report.png" alt-text="Opslaan in de map met voorbeeld rapporten" lightbox="media/save-sample-report.png":::

1. Herhaal de stappen voor andere voorbeeld rapporten. Wanneer u klaar bent, sluit u micro soft Power BI Desktop (geoptimaliseerd voor Power BI Report Server).
1. Ga in de Configuration Manager-console naar **controle**  >  **rapporten Power bi rapporten**  >  **Sample Reports**.
1. Klik met de rechter muisknop op een van de rapporten en selecteer **uitvoeren in browser** om het rapport te starten.

   :::image type="content" source="media/view-powerbi-report.png" alt-text="Het voorbeeld rapport uitvoeren vanuit de Configuration Manager-console" lightbox="media/view-powerbi-report.png":::

## <a name="next-steps"></a>Volgende stappen

[Integreren met Power BI Report Server](powerbi-report-server.md)