---
title: Hulp programma voor overdracht van inhouds bibliotheek
titleSuffix: Configuration Manager
description: Gebruik het hulp programma voor het overdragen van de inhouds bibliotheek om inhoud te verzenden van een schijf station naar een andere op een Configuration Manager distributie punt.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7401c80c89b1f1674bdae0b20482d7164837b724
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720084"
---
# <a name="content-library-transfer-tool"></a>Hulp programma voor overdracht van inhouds bibliotheek

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het hulp programma voor het overdragen van inhouds bibliotheken is een van de [Configuration Manager-hulpprogram ma's](tools.md). Het brengt inhoud over van het ene schijf station naar het andere. Het hulp programma is ontworpen om te worden uitgevoerd op de site systemen van het distributie punt. Het ondersteunt distributie punten die zijn gekoppeld aan een site of externe site systemen.  

Het hulp programma is handig voor het scenario wanneer het schijf station dat als host fungeert voor de inhouds bibliotheek vol is. U moet eerst een andere harde schijf met voldoende ruimte toevoegen of identificeren om de inhouds bibliotheek te hosten. Gebruik vervolgens **ContentLibraryTransfer. exe** om inhoud over te dragen van de oude, gevulde harde schijf naar de nieuwe, lege schijf.
 
Zodra de overdracht is voltooid, is de inhoud toegankelijk voor client computers vanaf de nieuwe locatie.



## <a name="usage"></a>Gebruik 

Voer **ContentLibraryTransfer. exe** uit als een gebruiker met beheerders machtigingen op het distributie punt. 

#### <a name="syntax"></a>Syntaxis 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Voorbeeld
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Beperkingen

- Voer het hulp programma lokaal uit op het distributie punt. U kunt deze niet uitvoeren vanaf een externe computer.  

- Gebruik deze alleen wanneer clients niet actief toegang hebben tot het distributie punt. Als u het hulp programma uitvoert terwijl clients toegang hebben tot inhoud, bevat de inhouds bibliotheek op het doel station mogelijk onvolledige gegevens. De gegevens overdracht kan mislukken als gevolg van een onbruikbaar inhouds bibliotheek.  

- Distribueer geen inhoud naar het distributie punt wanneer u het hulp programma uitvoert. Als u het hulp programma uitvoert terwijl er inhoud naar het distributie punt wordt geschreven, bevat de inhouds bibliotheek op het doel station mogelijk onvolledige gegevens. De gegevens overdracht kan mislukken als gevolg van een onbruikbaar inhouds bibliotheek.



## <a name="see-also"></a>Zie ook

- [Basisconcepten voor inhoudsbeheer](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [De inhoudsbibliotheek](../plan-design/hierarchy/the-content-library.md)
