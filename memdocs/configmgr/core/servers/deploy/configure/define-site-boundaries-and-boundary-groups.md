---
title: Grenzen en grens groepen gebruiken
titleSuffix: Configuration Manager
description: Gebruik grenzen en grens groepen om netwerk locaties en toegankelijke site systemen te definiëren voor apparaten die u beheert.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 385dc1b2f542c964b52515e755a9202ee951bc5c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126372"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Site grenzen en grens groepen definiëren

*Van toepassing op: Configuration Manager (huidige vertakking)*

*Grenzen* in Configuration Manager netwerk locaties op uw intranet definiëren. Deze locaties bevatten apparaten die u wilt beheren. *Grens groepen* zijn logische groepen van grenzen die u configureert.

Een hiërarchie kan een wille keurig aantal grens groepen bevatten. Elke grens groep kan een combi natie van de volgende grens typen bevatten:  

- IP-subnet  
- Active Directory-sitenaam  
- IPv6-voor voegsel  
- IP-adresbereik  
- VPN (vanaf versie 2006)

Clients op het intranet evalueren hun huidige netwerklocatie en gebruiken deze informatie vervolgens om vast te stellen tot welke grensgroepen ze behoren.  

Clients gebruiken grensgroepen voor de volgende doeleinden:  

- **Een toegewezen site zoeken:** Met grens groepen kunnen clients een primaire site vinden voor client toewijzing. Dit gedrag staat ook bekend als *automatische site toewijzing*.  

- **Zoek naar bepaalde site systeem rollen die kunnen worden gebruikt:** Een grens groep koppelen aan bepaalde site systeem rollen. De site levert clients die lijst met site systemen in de grens groep. Clients gebruiken deze site systemen voor acties zoals het zoeken naar inhoud of een nabijgelegen beheer punt.  

Clients die zich op internet bevinden of die zijn geconfigureerd als clients met alleen Internet, gebruiken geen grens gegevens. Deze clients kunnen geen automatische site toewijzing gebruiken. Ze kunnen inhoud downloaden vanaf een op internet gebaseerd distributie punt van hun toegewezen site of een distributie punt in de Cloud.  

Vanaf versie 1902 kunt u een Cloud beheer gateway (CMG) koppelen aan een grens groep. Zie [CMG Hierarchy design](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design)(Engelstalig) voor meer informatie.<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a>Vereisten

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Gebruik een combi natie van de minste grenzen die aan uw behoeften voldoen

Gebruik het type grens of de typen die u kiest voor uw omgeving. Gebruik voor het vereenvoudigen van uw beheer taken grens typen waarmee u het minste aantal grenzen kunt gebruiken.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Voorkom overlappende grenzen voor automatische site toewijzing

Hoewel elke grens groep zowel site toewijzing als site systeem verwijzing ondersteunt, maakt u een afzonderlijke set grens groepen die alleen worden gebruikt voor site toewijzing. Zorg ervoor dat elke grens in een grens groep geen lid is van een andere grens groep met een andere site toewijzing.

- Een enkele grens kan worden opgenomen in meerdere grens groepen  

- Elke grensgroep kan worden gekoppeld aan een andere primaire site voor sitetoewijzing  

- Voor een grens die lid is van twee verschillende grens groepen met verschillende site toewijzingen, selecteren clients wille keurig een site om deel te nemen. Dit gedrag is mogelijk niet van de site waaraan u de client wilt toevoegen. Deze configuratie wordt *overlappende grenzen*genoemd.  

    Overlappende grenzen zijn geen probleem voor de locatie van inhoud. Het kan een handige configuratie zijn die clients extra bronnen of inhouds locaties biedt die ze kunnen gebruiken.  


## <a name="next-steps"></a>Volgende stappen

- [Netwerk locaties definiëren als grenzen](boundaries.md)

- [Grens groepen configureren](boundary-groups.md)
