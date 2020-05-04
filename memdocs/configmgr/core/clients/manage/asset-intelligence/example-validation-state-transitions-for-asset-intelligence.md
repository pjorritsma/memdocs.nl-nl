---
title: Voorbeeld van validatie van statusovergangen
titleSuffix: Configuration Manager
description: Zie voor beelden van validatie status overgangen voor Asset Intelligence in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2af9243d6720d5821c641e5c80589457a33b638e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714176"
---
# <a name="example-validation-state-transitions-for-asset-intelligence"></a>Voorbeeld van validatie van statusovergangen voor Asset Intelligence

*Van toepassing op: Configuration Manager (huidige vertakking)*

Asset Intelligence validatie status in Configuration Manager zijn niet statisch en kunnen wijzigingen aanbrengen in de beheer acties die u onderneemt om invloed te hebben op de gegevens die zijn opgeslagen in de Asset Intelligence catalogus. In dit onderwerp vindt u voor beelden van mogelijke overgangen voor validatie status.

##  <a name="uncategorized-catalog-item-is-categorized-by-the-administrative-user"></a><a name="BKMK_UncategorizedIsCategorized"></a> Niet-gecategoriseerd catalogusitem wordt gecategoriseerd door de gebruiker met beheerdersrechten  

|**Statusovergang**|**Beschrijving van statusovergang**|  
|--------------------------|--------------------------------------|  
|**Niet-gecategoriseerd**|Een geïnventariseerde softwaretitel die niet eerder is gecategoriseerd door System Center Online of die de gebruiker met beheerdersrechten in de Asset Intelligence-catalogus heeft ingevoerd.|  
|**Niet-gecategoriseerd** naar **Door de gebruikergedefinieerd**|Het niet-gecategoriseerde catalogusitem wordt gecategoriseerd door de gebruiker met beheerdersrechten|  

##  <a name="categorized-catalog-item-is-recategorized-by-the-administrative-user"></a><a name="BKMK_CategorizedIsReCategorized"></a> Niet-gecategoriseerd catalogusitem wordt gecategoriseerd door de gebruiker met beheerdersrechten  

|**Statusovergang**|**Beschrijving van statusovergang**|  
|--------------------------|--------------------------------------|  
|**Gevalideerd**|Catalogusitem is gedefinieerd door System Center Online-onderzoekers en is aanwezig in de Asset Intelligence-catalogus.|  
|**Gevalideerd** naar **Door de gebruiker gedefinieerd**|Het gevalideerde catalogusitem wordt opnieuw gecategoriseerd door de gebruiker met beheerdersrechten.|  

> [!NOTE]  
>  Omdat categorisatie-informatie die is verkregen van System Center Online is opgeslagen in de database en niet kan worden verwijderd, kan de gebruiker met beheerdersrechten later terugkeren naar de System Center Online-categorisatie.  

##  <a name="user-defined-catalog-item-is-recategorized-by-system-center-online"></a><a name="BKMK_UserDefinedIsRecategorized"></a>Door de gebruiker gedefinieerd catalogus item wordt opnieuw gecategoriseerd door System Center online  

|**Statusovergang**|**Beschrijving van statusovergang**|  
|--------------------------|--------------------------------------|  
|**Niet-gecategoriseerd**|Een geïnventariseerde softwaretitel die niet eerder door System Center Online of de gebruiker met beheerdersrechten is gecategoriseerd, wordt in de Asset Intelligence-catalogus ingevoerd.|  
|**Door de gebruiker gedefinieerd**|Het niet-gecategoriseerde catalogusitem wordt gecategoriseerd door de gebruiker met beheerdersrechten|  
|**Door de gebruiker gedefinieerd** naar **Kan worden bijgewerkt**|Een door de gebruiker gedefinieerd catalogusitem is anders gecategoriseerd door System Center Online tijdens latere handmatige bulksgewijze updates van de Asset Intelligence-catalogus.<br /><br /> De gebruiker met beheerdersrechten kan in het dialoogvenster **Conflictoplossing softwaredetails** aangeven of de nieuwe indelingsinformatie of de eerdere door de gebruiker gedefinieerde waarde moet worden gebruikt.|  
|**Kan worden bijgewerkt** naar **Gevalideerd**|De gebruiker met beheerdersrechten kan in het dialoogvenster **Conflictoplossing softwaredetails** de nieuw categorisatie-informatie gebruiken die tijdens de vorige catalogusupdate van System Center Online is ontvangen.|  
|of||  
|**Kan worden bijgewerkt** naar **Door de gebruiker gedefinieerd**|De gebruiker met beheerdersrechten kan in het dialoogvenster **Conflictoplossing softwaredetails** de eerder door de gebruiker gedefinieerde waarde gebruiken.|  

> [!NOTE]  
>  Omdat categorisatie-informatie die is verkregen van System Center Online is opgeslagen in de database en niet kan worden verwijderd, kan de gebruiker met beheerdersrechten later terugkeren naar de System Center Online-categorisatie.  

##  <a name="uncategorized-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UncategorizedIsSubmitted"></a>Niet-gecategoriseerd catalogus item wordt verzonden naar System Center online voor categorisatie  

|**Statusovergang**|**Beschrijving van statusovergang**|  
|--------------------------|--------------------------------------|  
|**Niet-gecategoriseerd**|Een geïnventariseerde softwaretitel die niet eerder door System Center Online of de gebruiker met beheerdersrechten is gecategoriseerd, wordt in de Asset Intelligence-database ingevoerd.|  
|**Niet-gecategoriseerd** naar **In behandeling**|Het niet-gecategoriseerde item wordt verzonden naar System Center Online om door de gebruiker met beheerdersrechten te worden gecategoriseerd.|  
|**In behandeling** naar **Gevalideerd**|Het item wordt gecategoriseerd door System Center Online. De gebruiker met beheerdersrechten importeert het item in de Asset Intelligence-catalogus met behulp van een bulkcatalogusupdate of met behulp van synchronisatie van de Asset Intelligence-catalogus. Beide mogelijkheden zijn beschikbaar via de Asset Intelligence-synchronisatiepuntsitesysteemrol.|  

##  <a name="user-defined-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UserDefinedIsSubmitted"></a>Door de gebruiker gedefinieerd catalogus item wordt verzonden naar System Center online voor categorisatie  

|**Statusovergang**|**Beschrijving van statusovergang**|  
|--------------------------|--------------------------------------|  
|**Niet-gecategoriseerd**|Een geïnventariseerde softwaretitel die niet eerder door een gebruiker met beheerdersrechten of System Center Online is gecategoriseerd, wordt in de Asset Intelligence-database ingevoerd.|  
|**Door de gebruiker gedefinieerd**|U hebt het niet-gecategoriseerde item gecategoriseerd.|  
|**Door de gebruiker gedefinieerd** naar **In behandeling**|U verzendt het door de gebruiker gedefinieerde item ter categorisatie naar System Center Online.|  
|**In behandeling** naar **Kan worden bijgewerkt**|Een door de gebruiker gedefinieerd catalogusitem is tijdens een volgende catalogussynchronisatie anders gecategoriseerd door System Center Online. U kunt de actie **Conflict oplossen** gebruiken om te bepalen of u de nieuwe categorisatiegegevens of de vorige door de gebruiker gedefinieerde waarde wilt gebruiken. Zie [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)voor meer informatie over het oplossen van conflicten.|  
|**Kan worden bijgewerkt** naar **Gevalideerd**|U gebruikt de actie **Conflict oplossen** en selecteert de nieuwe categorisatiegegevens van System Center Online die u tijdens de vorige catalogusupdate hebt ontvangen. Zie [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)voor meer informatie over het oplossen van conflicten.|  
|of||  
|**Kan worden bijgewerkt** naar **Door de gebruiker gedefinieerd**|U gebruikt de actie **Conflict oplossen** en selecteert de vorige door de gebruiker gedefinieerde waarde om te gebruiken. Zie [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)voor meer informatie over het oplossen van conflicten.|  

> [!NOTE]  
>  Omdat categorisatiegegevens die van System Center Online zijn verkregen, worden opgeslagen in de database en niet kunnen worden verwijderd, kunt u later terugkeren naar de System Center Online-categorisatie.  
