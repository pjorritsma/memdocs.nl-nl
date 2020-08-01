---
title: CMPivot-overzicht van gekoppelde Tenant
titleSuffix: Configuration Manager
description: Overzicht van CMPivot voor aan micro soft Endpoint Manager gekoppelde apparaten.
ms.date: 07/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 31bf1359-54e5-4416-9f39-6bb0070db542
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07bb8cd913c945198d181e6191c540eeb8b2dffc
ms.sourcegitcommit: 5a58af4f7d40bbde88a273fba859bf69eeff6107
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473665"
---
# <a name="tenant-attach-cmpivot-overview"></a>Tenant koppelen: overzicht van CMPivot

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

> [!Important]
> Dit artikel is van toepassing op de Technical Preview-vertakking voor Configuration Manager. Zie [Configuration Manager Technical Preview versie 2005](../core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot)voor meer informatie.

Met CMPivot kunt u snel de status van een apparaat in uw omgeving beoordelen en actie ondernemen. Wanneer u een query invoert, wordt in CMPivot een query in realtime uitgevoerd op het apparaat dat momenteel is verbonden. De geretourneerde gegevens kunnen vervolgens worden gefilterd, gegroepeerd en verfijnd voor het beantwoorden van zakelijke vragen, het oplossen van problemen in uw omgeving of het reageren op beveiligings Risico's. Zie [CMPivot gebruiken](../core/servers/manage/cmpivot.md)voor meer informatie over het gebruik van CMPivot.

## <a name="refine-cmpivot-queries"></a><a name="bkmk_refine"></a>CMPivot query's verfijnen

Wanneer u CMPivot gebruikt vanuit de beheer console van micro soft Endpoint Manager, moet u controleren of uw query's zijn afgestemd op de prestaties. Als u een query aanvraagt met een gegevensset die te groot is, wordt u mogelijk ontvangen `Error: The query result is too large, retry with additional filters` . Verfijn uw query zodat deze meer specifiek is als u deze fout ziet. De volgende Opera tors worden vaak gebruikt voor het verfijnen van query's:

- Gebruik `count` Als u alleen het aantal geretourneerde items nodig hebt.
- Gebruik deze `project` Als u alleen specifieke kolommen nodig hebt.
- Gebruiken `take` om het opgegeven aantal rijen te retour neren.
- Gebruiken `top` om de eerste N records te retour neren, gesorteerd op opgegeven kolommen.

> [!Important]
> Wanneer u CMPivot gebruikt om een apparaat op te vragen, als er niet binnen tien minuten een reactie is, is de query een time-out. <!--7802754-->


[!INCLUDE [Overview article sections for both Microsoft Endpoint Manager and Configuration Manager use](../core/servers/manage/includes/cmpivot-overview-shared.md)]

## <a name="next-steps"></a>Volgende stappen

Zie voor meer voorbeeld scripts [micro soft Endpoint Manager Tenant koppelen: CMPivot-script voorbeelden](cmpivot-samples-attached.md).
