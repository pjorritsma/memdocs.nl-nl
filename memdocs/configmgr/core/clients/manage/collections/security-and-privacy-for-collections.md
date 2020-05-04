---
title: Incasso beveiliging en privacy
titleSuffix: Configuration Manager
description: Bekijk aanbevolen procedures voor beveiliging en privacy in verzamelingen in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714491"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Beveiliging en privacy voor verzamelingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat aanbevolen procedures voor beveiliging en privacy-informatie voor verzamelingen in Configuration Manager.  

 Er zijn geen privacygegevens specifiek voor verzamelingen in Configuration Manager. Verzamelingen zijn containers voor resources, zoals gebruikers en apparaten. Lidmaatschap van een verzameling is vaak afhankelijk van de informatie die Configuration Manager verzameld tijdens de normale werking. U kunt bijvoorbeeld op basis van met een detectie of inventarisatie verzamelde resourcegegevens een verzameling configureren om de apparaten te bevatten die voldoen aan opgegeven criteria. Verzamelingen kunnen ook worden gebaseerd op de huidige statusinformatie voor clientbeheeroperaties, zoals het implementeren van software en het controleren op naleving. Naast deze op query's gebaseerde verzamelingen kunnen gebruikers met beheerdersrechten ook resources aan verzamelingen toevoegen.  

 Zie [Inleiding tot verzamelingen](../../../../core/clients/manage/collections/introduction-to-collections.md)voor meer informatie over verzamelingen. Zie voor meer informatie over aanbevolen procedures voor beveiliging en privacy-informatie voor Configuration Manager bewerkingen die kunnen worden gebruikt voor het configureren van het lidmaatschap van een verzameling, [Aanbevolen procedures voor beveiliging en privacy-informatie voor Configuration Manager](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md).  

## <a name="security-best-practices-for-collections"></a>Aanbevolen procedures voor verzamelingen  
 Gebruik de volgende aanbevolen beveiligingsprocedures voor verzamelingen.  

|Aanbevolen beveiligingsprocedure|Meer informatie|  
|----------------------------|----------------------|  
|Wanneer u een verzameling in een MOF-bestand (Managed Object Format) wilt exporteren naar of importeren van een netwerklocatie, beveiligt u die locatie en het netwerkkanaal.|Hiermee beperkt u wie toegang heeft tot de netwerkmap.<br /><br /> Gebruik SBS-ondertekening (Server Message Block) of IPsec (Internet Protocol Security) tussen de netwerklocatie en de siteserver om te voorkomen dat een kwaadwillende persoon met de geëxporteerde verzamelingsgegevens kan knoeien. Gebruik IPsec om de gegevens op het netwerk te versleutelen om openbaarmaking van informatie te voorkomen.|  

### <a name="security-issues-for-collections"></a>Beveiligingsproblemen voor verzamelingen  
 Bij verzamelingen komen de volgende beveiligingsproblemen kijken:  

-   Als u verzamelingsvariabelen gebruikt, kunnen lokale beheerders potentieel gevoelige informatie lezen.  

     Verzamelingsvariabelen kunnen worden gebruikt wanneer u een besturingssysteem implementeert.  
