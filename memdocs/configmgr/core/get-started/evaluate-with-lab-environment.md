---
title: Evalueren in een test omgeving
titleSuffix: Configuration Manager
description: Een test omgeving maken om Configuration Manager te evalueren voor gebruik in uw organisatie.
ms.date: 02/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db59ad55c52f8d937b23704af310dc8879fe8a6d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692873"
---
# <a name="evaluate-configuration-manager-by-building-your-own-lab-environment"></a>Configuration Manager evalueren door uw eigen test omgeving te bouwen

*Van toepassing op: Configuration Manager (huidige vertakking)*

 Meer informatie over het maken van een test omgeving voor het evalueren van Configuration Manager voor gebruik in uw organisatie.  

 Configuration Manager is een complex en krachtig hulp programma voor het beheren van uw gebruikers, apparaten en software. Het is een goed idee om Configuration Manager grondig te evalueren vóór de volledige implementatie, zodat u inzicht kunt krijgen in de praktijk van beste eerst.  

 Deze hand leiding is hoofd zakelijk bedoeld voor beheerders die het gebruik van Configuration Manager in bedrijfs omgevingen evalueren:  

-   Beheerders die een oplossing willen om Pc's, servers en mobiele apparaten volledig te beheren  

-   Beheerders in branches met een hoge beveiliging die de beveiliging van on-premises Apparaatbeheer nodig hebben met de flexibiliteit van het beheer van Cloud apparaten  

-   Beheerders die de schaal baarheid van hun on-premises server architectuur willen beheren  

## <a name="what-this-lab-does"></a>Wat deze testomgeving biedt  
 Het belangrijkste doel van het maken van deze test omgeving is om u de algemene kennis te geven om aan de slag te gaan met Configuration Manager en om uw kennis van Configuration Manager te verbeteren. U gaat door een snelle assembly van de huidige versie van Configuration Manager met behulp van twee servers:  

-   Een die als host fungeert voor Active Directory, de domein controller en de DNS-server  

-   Een die als host fungeert voor Configuration Manager en alle bijbehorende SQL Server onderdelen  

De clientcomputers zijn geïnstalleerd in Hyper-V. De testomgeving zelf kan ook worden uitgevoerd als een volledig gevirtualiseerd systeem op één server.  

## <a name="what-this-lab-does-not-do"></a>Wat deze testomgeving niet biedt  
 Met deze test omgeving kunt u niet alle Configuration Manager scenario's uitvoeren. Het is niet ontworpen om onmiddellijk te worden gemigreerd naar een actieve omgeving.  

 Wanneer u deze testomgeving opzet, beschikt u over een functionele omgeving waarin u kunt werken. Deze omgeving wordt echter niet geoptimaliseerd voor factoren zoals systeem prestaties, het beheer van vasteschijfruimte en SQL Server opslag.  

##  <a name="recommended-reading-before-you-build-the-lab"></a><a name="BKMK_EvalRec"></a> Aanbevolen lezen voordat u het Lab maakt  
 Er is een schat aan inhoud beschikbaar in de [documentatie voor Configuration Manager](/sccm/). We raden u aan de volgende onderwerpen in deze bibliotheek te lezen voordat u begint met het bouwen van het Lab:  

-   Leer basis concepten over de Configuration Manager-console, portals voor eind gebruikers en voorbeeld scenario's in [Inleiding tot Configuration Manager](../../core/understand/introduction.md).  

-   Meer informatie over de primaire beheer functies van Configuration Manager in [functies en mogelijkheden van Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Hun uw kennis met de [basis principes van Configuration Manager](../../core/understand/fundamentals.md).  

-   Meer informatie over het belang van beveiligings rollen in de [basis principes van beheer op basis van rollen voor Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Meer informatie over inhouds beheer in [concepten voor inhouds beheer](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Meer informatie over het ondersteunen van dagelijkse taken in uw implementatie in [begrijpen hoe clients site bronnen en-services vinden voor Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).