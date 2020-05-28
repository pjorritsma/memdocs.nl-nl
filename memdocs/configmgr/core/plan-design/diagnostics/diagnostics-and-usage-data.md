---
title: Diagnostische gegevens en gebruiksgegevens
titleSuffix: Configuration Manager
description: Meer informatie over de diagnostische en gebruiks gegevens die Configuration Manager over zichzelf verzamelen.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffa50d2cfb3095eb136128c09b74e9ee6a4eb501
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904403"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Diagnostische en gebruiks gegevens voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager verzamelt diagnostiek en gebruiks gegevens over zichzelf, die door micro soft worden gebruikt voor het verbeteren van de installatie-ervaring, kwaliteit en beveiliging van toekomstige releases.  

Met elke Configuration Manager hiërarchie worden diagnostische en gebruiks gegevens ingeschakeld. Het bestaat uit SQL Server query's die wekelijks worden uitgevoerd op elke primaire site en op de centrale beheer site (CAS). Wanneer de hiërarchie een CAS gebruikt, repliceert de onderliggende primaire sites hun gegevens naar die certificerings instanties. Op de site op het hoogste niveau van uw hiërarchie wordt deze informatie door het [service aansluitpunt](../../servers/deploy/configure/about-the-service-connection-point.md) verzonden wanneer er wordt gecontroleerd op updates. Als het service verbindings punt zich in de offline modus bevindt, kunt u de gegevens overdragen met behulp van het [hulp programma voor service verbindingen](../../servers/manage/use-the-service-connection-tool.md).

> [!NOTE]  
> Configuration Manager verzamelt alleen gegevens uit de SQL Server-Data Base van de site en verzamelt geen gegevens rechtstreeks van clients of site servers.  

Zie de [privacyverklaring van micro soft](https://privacy.microsoft.com/privacystatement)voor meer informatie.  

> [!div class="nextstepaction"]
> [Gebruik van diagnostische en gebruiksgegevens door Microsoft](how-diagnostics-and-usage-data-is-used.md)
