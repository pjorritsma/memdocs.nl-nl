---
title: Beveiliging en privacy voor query's
titleSuffix: Configuration Manager
description: Krijg inzicht in de aanbevolen procedures voor beveiliging en privacy bij het opvragen van gegevens uit de site database.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714610"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Beveiliging en privacy voor query's in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met query's in Configuration Manager kunt u gegevens uit de site database ophalen op basis van de criteria die u opgeeft. Configuration Manager verzamelt site database gegevens tijdens een standaard bewerking. Als u bijvoorbeeld gegevens gebruikt die zijn verzameld tijdens de detectie of inventaris, kunt u een query configureren om apparaten te identificeren die voldoen aan opgegeven criteria.  

 Zie [Inleiding tot query's](../../../core/servers/manage/introduction-to-queries.md)voor meer informatie over query's. Zie [beveiliging en privacy voor Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)voor de aanbevolen procedures voor beveiliging en privacy-informatie over Configuration Manager bewerkingen voor het verzamelen van de gegevens die u kunt ophalen met behulp van query's.  

## <a name="security-best-practices-for-queries"></a>Aanbevolen beveiligings procedures voor query's

 Gebruik deze beveiligings best practice voor query's.  

|Aanbevolen beveiligingsprocedure|Meer informatie|  
|----------------------------|----------------------|  
|Beveilig de locatie en het netwerk kanaal wanneer u een query exporteert of importeert die wordt opgeslagen op een netwerk locatie.|Beperk wie toegang heeft tot de netwerkmap.<br /><br /> Gebruik SMB-ondertekening (Server Message Block) of Internet Protocol Security (IPsec) tussen de netwerk locatie en de site server om te voor komen dat een kwaadwillende persoon knoeit met de query gegevens voordat deze wordt geïmporteerd.|  

## <a name="next-steps"></a>Volgende stappen
  
[Beveiliging en privacy voor Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
