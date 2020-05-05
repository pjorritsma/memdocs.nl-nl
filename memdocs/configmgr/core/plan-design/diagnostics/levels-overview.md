---
title: Niveaus van diagnostische gebruiks gegevens
titleSuffix: Configuration Manager
description: Meer informatie over de niveaus van diagnostische en gebruiks gegevens die worden Configuration Manager verzameld
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9de63280786d620229c7d408f09ef2fe583e231d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720336"
---
# <a name="levels-of-diagnostic-usage-data"></a>Niveaus van diagnostische gebruiks gegevens

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager verzamelt drie niveaus van diagnostiek en gebruiks gegevens: **basis**, **uitgebreid**en **volledig**. Deze functie is standaard ingesteld op het niveau Uitgebreid.

> [!IMPORTANT]
> Configuration Manager verzamelt geen site codes, namen van sites, IP-adressen, gebruikers namen, computer namen, fysieke adressen of e-mail adressen op het niveau basis of uitgebreid. Een verzameling van deze informatie op het volledige niveau is niet doel gericht. Het is mogelijk opgenomen in de geavanceerde diagnostische gegevens, zoals logboek bestanden of moment opnamen van het geheugen. Micro soft gebruikt deze informatie niet om u te identificeren, contact met u op te nemen of reclame te ontwikkelen.

## <a name="levels"></a>Niveaus

### <a name="basic"></a>Basic

Het niveau basis omvat gegevens over uw hiërarchie. Het is vereist om uw installatie-of upgrade-ervaring te verbeteren. Met deze gegevens kunt u ook de Configuration Manager updates bepalen die van toepassing zijn op uw-hiërarchie.

### <a name="enhanced"></a>Verbeterd

Het niveau uitgebreid is de standaard instelling nadat de installatie is voltooid. Dit niveau omvat gegevens die worden verzameld op basis niveau en functie-specifieke gegevens. De frequentie en duur van het gebruik van verschillende functies worden weer gegeven. Het bevat ook Configuration Manager client instellingen gegevens: onderdeel naam, status en bepaalde instellingen, zoals polling-intervallen. Informatie over software-updates is basis van het gebruik van de functie, maar bevat geen gegevens over update compatibiliteit op dit niveau.

Micro soft raadt dit niveau aan omdat het de minimale gegevens biedt om verbeteringen van de product-en service te kunnen aanbrengen.

Enkele voor beelden van gegevens die op dit niveau niet worden verzameld, zijn:

- Namen van sites, gebruikers, computers of andere objecten

- Details van aan beveiliging gerelateerde objecten

- Beveiligings problemen zoals het aantal systemen waarvoor software-updates zijn vereist

### <a name="full"></a>Volledig

Het niveau volledig omvat alle gegevens in de niveaus basis en uitgebreid. Het omvat ook aanvullende informatie over Endpoint Protection, percentages van updatenaleving en informatie over software-updates. Dit niveau kan ook geavanceerde diagnostische gegevens bevatten, zoals systeem bestanden en moment opnamen van het geheugen. Deze geavanceerde gegevens kunnen persoonlijke gegevens bevatten in het geheugen of logboek bestanden op het moment van vastleggen.

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Niveau wijzigen

Als u het niveau van de gegevens verzameling wilt wijzigen **, moet u wijzigings** machtigingen hebben voor de object klasse **site** .

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .
1. Selecteer **hiërarchie-instellingen** in het lint.
1. Schakel over naar het tabblad **Diagnostische en gebruiks gegevens** en kies vervolgens het gegevens niveau.

## <a name="version-specific-details"></a><a name="bkmk_versions"></a>Details van specifieke versie

In de volgende artikelen worden de specifieke gegevens beschreven die Configuration Manager verzameld op elk niveau met elke ondersteunde versie:

- [Diagnostische en gebruiks gegevens voor 2002](levels-of-diagnostic-usage-data-collection-2002.md)
- [Diagnostische en gebruiks gegevens voor 1910](levels-of-diagnostic-usage-data-collection-1910.md)
- [Diagnostische en gebruiks gegevens voor 1906](levels-of-diagnostic-usage-data-collection-1906.md)
- [Diagnostische en gebruiks gegevens voor 1902](levels-of-diagnostic-usage-data-collection-1902.md)
- [Diagnostische en gebruiks gegevens voor 1810](levels-of-diagnostic-usage-data-collection-1810.md)

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Veelgestelde vragen](frequently-asked-questions.md)
