---
title: Overzicht van gekoppeld CMPivot-gebruik aan Tenant
titleSuffix: Configuration Manager
description: Overzicht van het gebruik van CMPivot voor aan micro soft Endpoint Manager gekoppelde apparaten.
ms.date: 09/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8967957883a1c8d397377c30409cb94139014214
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564070"
---
# <a name="tenant-attach-cmpivot-preview-usage-overview"></a>Tenant bijvoegen: CMPivot (preview) gebruiks overzicht

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]
> - Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

Met CMPivot kunt u snel de status van een apparaat in uw omgeving beoordelen en actie ondernemen. Wanneer u een query invoert, wordt in CMPivot een query in realtime uitgevoerd op het apparaat dat momenteel is verbonden. De geretourneerde gegevens kunnen vervolgens worden gefilterd, gegroepeerd en verfijnd voor het beantwoorden van zakelijke vragen, het oplossen van problemen in uw omgeving of het reageren op beveiligings Risico's. Zie [CMPivot gebruiken](../core/servers/manage/cmpivot.md)voor meer informatie over het gebruik van CMPivot.

## <a name="refine-cmpivot-queries"></a><a name="bkmk_refine"></a> CMPivot query's verfijnen

Wanneer u CMPivot gebruikt vanuit de beheer console van micro soft Endpoint Manager, moet u controleren of uw query's zijn afgestemd op de prestaties. Als u een query aanvraagt met een gegevensset die te groot is, wordt u mogelijk ontvangen `Error: The query result is too large, retry with additional filters` . Verfijn uw query zodat deze meer specifiek is als u deze fout ziet. De volgende Opera tors worden vaak gebruikt voor het verfijnen van query's:

- Gebruik `count` Als u alleen het aantal geretourneerde items nodig hebt.
- Gebruik deze `project` Als u alleen specifieke kolommen nodig hebt.
- Gebruiken `take` om het opgegeven aantal rijen te retour neren.
- Gebruiken `top` om de eerste N records te retour neren, gesorteerd op opgegeven kolommen.

> [!Important]
> Wanneer u CMPivot gebruikt om een apparaat op te vragen, als er niet binnen tien minuten een reactie is, is de query een time-out. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Endpoint Manager and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]


## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie [Start CMPivot (preview) in het beheer centrum](cmpivot-start.md) voor meer voorbeeld scripts raadpleegt u [micro soft Endpoint Manager Tenant koppelen: CMPivot-script voorbeelden](cmpivot-samples-attached.md).
