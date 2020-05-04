---
title: Gebruik van diagnostische gegevens
titleSuffix: Configuration Manager
description: Meer informatie over de wijze waarop micro soft gebruikmaakt van de diagnostische en gebruiks gegevens die Configuration Manager verzamelt.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715611"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Hoe micro soft gebruikmaakt van Configuration Manager diagnostische en gebruiks gegevens

*Van toepassing op: Configuration Manager (huidige vertakking)*

Diagnostische en gebruiks gegevens die door Configuration Manager verzameld, bieden micro soft vrijwel onmiddellijk feedback over hoe het product werkt en wordt gebruikt om toekomstige updates aan te passen. Micro soft kan ook configuratie gegevens zien die u helpen bij het ontwikkelen en testen van de configuraties die u in de productie omgeving gebruikt. Bijvoorbeeld:

- De versies van Windows Server die worden gebruikt op site servers

- Geïnstalleerde taal pakketten

- De verschillen van het SQL-schema ten opzichte van de productstandaard

Met deze gegevens kan het engineering team toekomstige tests plannen om ervoor te zorgen dat u de beste ervaring hebt met de meest voorkomende configuraties. Deze gegevens zijn essentieel om snel aan te passen en aan te passen met een frequente release cyclus.

Net zo belang rijk is hoe de diagnostische en gebruiks gegevens niet worden gebruikt. Micro soft gebruikt deze gegevens niet voor:

- Licentiecontroles, bijvoorbeeld het vergelijken van het gebruik van de klant met de licentieovereenkomsten

- Controle van producten die niet worden ondersteund

- Adverteren op basis van beschik bare gegevens, zoals het gebruik van functies of geolocatie (tijd zone)

Micro soft gebruikt beschik bare gegevens voor het verbeteren van het product. Bijvoorbeeld:

- De eerste ondersteuning die wordt aangeboden door de huidige vertakking van Configuration Manager beperkt de ondersteunings tijdlijn voor Windows Server 2008 R2. Micro soft heeft de gebruiks gegevens onderzocht van klanten die een upgrade hadden uitgevoerd naar de huidige branch Configuration Manager. Ze hebben vervolgens vastgesteld dat deze tijd lijn moet worden herzien en uitgebreid om klanten te ondersteunen die nog steeds gebruikmaken van dit besturings systeem.

- Micro soft heeft de vereisten controles voor het installeren van een update verbeterd. Ze hebben verouderde regels verwijderd, geadministratief voor aanvullende cases en er zijn automatisch problemen opgelost.  

> [!div class="nextstepaction"]
> [Gegevens verzamelen met Configuration Manager](how-diagnostics-and-usage-data-is-collected.md)
