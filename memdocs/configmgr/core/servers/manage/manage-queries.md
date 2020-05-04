---
title: Query's beheren
titleSuffix: Configuration Manager
description: Meer informatie over het beheren van uw query's. Bevat een tabel voor gedetailleerde Naslag informatie.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 37050a3a96b732df3f56269592e049077008ab2b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713749"
---
# <a name="how-to-manage-queries-in-configuration-manager"></a>Query's beheren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u meer informatie over het beheren van query's in Configuration Manager.  

 Zie [query's maken](../../../core/servers/manage/create-queries.md)voor meer informatie over het maken van query's.  

## <a name="manage-queries"></a>Query's beheren
 In de werkruimte **Bewaking** selecteert u **Query's**, selecteert u de query die u wilt beheren en selecteert u vervolgens een beheertaak.  

 De volgende tabel bevat informatie over de beheer taken.  

|Beheertaak|Details| 
|---------------------|-------------|
|**Uitvoeringsrun**|Hiermee wordt de geselecteerde query uitgevoerd en worden de resultaten weer gegeven in de Configuration Manager-console.|
|**Client installeren**|Hiermee opent u de **wizard Client installeren**, waarmee u de Configuration Manager-client kunt installeren op computers die door de geselecteerde query worden geretourneerd.<br /><br /> Deze optie is niet beschikbaar voor query's die mobiele apparaten, gebruikers of gebruikers groepen retour neren. <br /><br /> Zie [clients implementeren op Windows-computers](../../clients/deploy/deploy-clients-to-windows-computers.md)voor meer informatie over het installeren van Configuration Manager-clients met behulp van client push.| 
|**Exporteren**|Hiermee opent u de **wizard objecten exporteren**. Met deze wizard kunt u de query exporteren naar een MOF-bestand (Managed Object Format) dat u vervolgens kunt importeren op een andere site.
|**Verplaatsen**|Hiermee opent u het dialoog venster **geselecteerde items verplaatsen** . In dit dialoog venster kunt u de geselecteerde query verplaatsen naar een map die u eerder hebt gemaakt onder het knoop punt **query's** .|

## <a name="next-steps"></a>Volgende stappen 
 [Query's maken](../../../core/servers/manage/create-queries.md)
