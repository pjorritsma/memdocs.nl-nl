---
title: Veelgestelde vragen over diagnostische en gebruiks gegevens
titleSuffix: Configuration Manager
description: Veelgestelde vragen over diagnostische en gebruiks gegevens voor Configuration Manager
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60634ed8e275ff8496a08969054aa912a81b9d07
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709542"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>Veelgestelde vragen over diagnostische gegevens en gebruiksgegevens

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u antwoorden op veelgestelde vragen over diagnostische en gebruiks gegevens in Configuration Manager.

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a>Kan ik diagnostische en gebruiks gegevens uitschakelen?

Gebruik het service aansluitpunt in de offline modus om te helpen bij het verzenden van gegevens door de site. Gebruik vervolgens het hulp programma voor service verbindingen om gegevens hand matig te verzenden. Raadpleeg voor meer informatie de volgende artikelen:

- [Het serviceverbindingspunt](../../servers/deploy/configure/about-the-service-connection-point.md)
- [Het hulpprogramma voor serviceverbindingen gebruiken](../../servers/manage/use-the-service-connection-tool.md)

Ter ondersteuning van nieuwe versies van Windows 10 en Cloud Services zoals Microsoft Intune, moet u de huidige vertakking van Configuration Manager regel matig bijwerken. Micro soft vereist ten minste het niveau basis voor diagnostische en gebruiks gegevens. Deze gegevens worden gebruikt om het product up-to-date te houden, de update-ervaring te verbeteren en de kwaliteit en beveiliging van het product te verbeteren.

Er worden geen gegevens naar de service verzonden wanneer het service aansluitpunt zich in de offline modus bevindt. Wanneer u overschakelt naar de online modus of het hulp programma voor service verbindingen gebruikt, worden gegevens naar de service verzonden om te controleren op updates.

U kunt ook het gegevens niveau kiezen dat Configuration Manager verzamelt. Zie [niveaus van diagnostische gebruiks gegevens](levels-overview.md)voor meer informatie.

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a>Wat is de Bewaar periode voor gegevens?

Micro soft slaat Configuration Manager diagnostische en gebruiks gegevens voor één jaar op.

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a>Worden er diagnostische en gebruiks gegevens verzonden wanneer het installatie programma wordt uitgevoerd?

Nee. Diagnostische gegevens en gebruiksgegevens worden alleen verzonden nadat de site is geïnstalleerd en operationeel is geworden.

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a>Hoe vaak worden de gegevens verzonden?

De in SQL opgeslagen procedures worden elke zeven dagen uitgevoerd vanaf de datum waarop u de site hebt geïnstalleerd.

- In de online modus worden de gegevens na de uitvoering van de query's geüpload met het service aansluitpunt.

- In de offline modus gebruikt u het hulp programma voor service verbindingen om de gegevens te uploaden. (De gegevens zijn in eerste instantie niet beschikbaar voor offline gebruik tot zeven dagen nadat u de site hebt geïnstalleerd.)  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a>Kunnen de gegevens worden gebruikt om een netwerk overzicht te maken?

Nee. Deze gegevens omvatten geen netwerk gegevens, zoals IP-adressen of gedetailleerde geografische informatie. Zie [niveaus van diagnostische gebruiks gegevens](levels-overview.md#bkmk_versions)voor meer informatie en vind meer Details voor de versie die u gebruikt.

De gegevens bevatten informatie over de tijd zone van elke site. Deze informatie kan inzicht bieden in de brede geolocatie en wereld wijde sprei ding van sites in een hiërarchie.

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a>Kunt u gegevens in aangepaste SQL-tabellen zien?

Nee. Configuration Manager verzamelt diagnostische en gebruiks gegevens via opgeslagen SQL-procedures. Deze opgeslagen procedures worden uitgevoerd op basis van standaard product tabellen in de-data base. Al deze SQL-tabellen worden voorafgegaan door **TEL_**. Als onderdeel van de query met betrekking tot SQL-schemadetectie worden alle tabelnamen gehasht ter vergelijking met de bekende standaardinstellingen. Dit gedrag bepaalt dat er aangepaste tabellen in de Data Base voor komen. De aanwezigheid van aangepaste tabellen informeert micro soft dat het database schema is uitgebreid op basis van de standaard waarde. Het bevat geen van de gegevens die in deze tabellen zijn opgeslagen.

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a>Kunt u andere data bases zien?

Nee. De opgeslagen procedures voor het verzamelen van gegevens zijn beperkt tot de Configuration Manager-site database. De namen van andere data bases of gegevens in andere data bases kunnen niet worden weer gegeven in micro soft.

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a>Worden er gegevens verzonden naar andere geïntegreerde Cloud Services?

Ja, wanneer u deze services integreert met Configuration Manager. Als onderdeel van de interactie met een Cloud service, wordt Configuration Manager een aantal gegevens naar die service verzonden. Deze gegevens zijn specifiek voor die Cloud service en worden gescheiden van Configuration Manager diagnostische gegevens en gebruik. Zie de documentatie voor die service voor meer informatie over de specifieke gegevens die worden gebruikt in de interactie met een andere Cloud service.

De volgende Cloud Services maken bijvoorbeeld deel uit van micro soft Endpoint Manager:

- [Gegevens privacy voor desktop Analytics](../../../desktop-analytics/privacy.md)
- [Privacy en persoonlijke gegevens in Intune](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Windows auto pilot-vereisten](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a>Verzamelt Configuration Manager persoonlijke gegevens?

Nee. Met de configuratie worden geen persoonlijke gegevens of klant gegevens verzameld of verzonden. Het is een on-premises product dat u rechtstreeks implementeert, beheert en gebruikt. De diagnostische en gebruiks gegevens die door micro soft worden verzameld, verbeteren de installatie-ervaring, kwaliteit en beveiliging van toekomstige releases.

Zie [niveaus van diagnostische gebruiks gegevens](levels-overview.md)voor meer informatie over het Configuration Manager van gegevens.
