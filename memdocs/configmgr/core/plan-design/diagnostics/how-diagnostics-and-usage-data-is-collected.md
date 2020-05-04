---
title: Verzameling diagnostische gegevens
titleSuffix: Configuration Manager
description: Meer informatie over de manier waarop Configuration Manager diagnostische en gebruiks gegevens over zichzelf verzamelt.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ca40891c840e954f2828833c179f01bcbc6e7448
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709535"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Informatie over het verzamelen van diagnostische en gebruiks gegevens Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor het verzamelen van diagnostische en gebruiks gegevens voor Configuration Manager worden elke primaire site op een wekelijkse basis uitgevoerd SQL Server query's. In een hiërarchie met meerdere sites worden de gegevens gerepliceerd naar de centrale beheersite.  

Op de site op het hoogste niveau van een hiërarchie wordt deze informatie door het service aansluitpunt verzonden wanneer er wordt gecontroleerd op updates. De modus van het service verbindings punt bepaalt hoe de gegevens worden overgedragen:

- **Online**: eenmaal per week verzendt het service verbindings punt automatisch diagnostische en gebruiks gegevens naar de Cloud service.

- **Offline**: u kunt Diagnostische en gebruiks gegevens hand matig overdragen met het [hulp programma voor service verbindingen](../../servers/manage/use-the-service-connection-tool.md).

Zie [about the Service Connection Point](../../servers/deploy/configure/about-the-service-connection-point.md)(Engelstalig) voor meer informatie.

> [!div class="nextstepaction"]
> [Diagnostische gegevens en gebruiksgegevens weergeven](view-diagnostics-and-usage-data.md)
