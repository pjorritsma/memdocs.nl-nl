---
title: Over upgrades, updates en installaties
titleSuffix: Configuration Manager
description: Meer informatie over het verschil tussen de voor waarden die worden geïnstalleerd, bijgewerkt en bijgewerkt bij het beheren van Configuration Manager-infra structuur.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5af92990a0158172a441b052cdc2210e98fda9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722597"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Over upgrades, updates en installaties voor de site- en hiërarchie-infrastructuur

*Van toepassing op: Configuration Manager (huidige vertakking)*

Bij het beheren van Configuration Manager sites en hiërarchie-infra structuur, worden de voor waarden *bijgewerkt*, *bijgewerkt*en *installeren* gebruikt om drie afzonderlijke concepten te beschrijven.

## <a name="upgrade"></a>Upgraden

*Upgrade* of *in-place upgrade*, wordt gebruikt bij het converteren van uw Configuration Manager 2012-site of-hiërarchie naar een die Configuration Manager current branch uitvoert.

Wanneer u System Center 2012 Configuration Manager op Configuration Manager huidige branch bijwerkt, blijft u dezelfde servers gebruiken om uw sites en site servers te hosten, en behoudt u uw bestaande gegevens en configuraties voor Configuration Manager.  Dit wijkt af van de [migratie](../migration/migrate-data-between-hierarchies.md) . Dit is een manier om uw configuraties en gegevens over beheerde apparaten te bewaren terwijl nieuwe Configuration Manager huidige branch-sites worden geïnstalleerd op nieuwe hardware.

Zie [upgrade naar Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)voor meer informatie.



## <a name="update"></a>Bijwerken
*Update* wordt gebruikt voor het installeren van updates in de console voor Configuration Manager en voor out-of-band-updates die niet kunnen worden geleverd vanuit de Configuration Manager-console. Met updates in de console kunt u de versie van uw Current Branch site (of de Technical Preview-site) aanpassen zodat er een hogere versie wordt uitgevoerd. Als uw site bijvoorbeeld versie 1806 uitvoert, kunt u een update installeren voor versie 1810. Updates kunnen ook oplossingen voor een bekend probleem installeren zonder de site versie te wijzigen.      

Doorgaans worden met updates beveiligings correcties, verbeteringen van de kwaliteit en nieuwe functies aan uw bestaande implementatie toegevoegd. Als u de Technical Preview-vertakking gebruikt, kan een update een nieuwere versie van de Technical Preview installeren.
- U kiest wanneer u de update in de console wilt installeren, beginnend bij de bovenste site van uw hiërarchie.
- U kunt elke update installeren die beschikbaar is via de-console. Als uw site bijvoorbeeld versie 1802 en zowel 1806 als 1810 wordt aangeboden, kunt u overwegen om versie 1810 te installeren, omdat elke versie de functies bevat die voor het eerst beschikbaar werden gesteld in eerder uitgebrachte versies.
- Nadat de installatie van een nieuwe update op de site op het hoogste niveau is voltooid, wordt het proces automatisch door onderliggende primaire sites gestart. U kunt echter [service Windows](../servers/manage/service-windows.md) zo instellen dat de timing van updates wordt bepaald.
- Secundaire sites installeren updates niet automatisch. In plaats daarvan start u de update hand matig vanuit de Configuration Manager-console.

Zie [updates voor Configuration Manager](../servers/manage/updates.md)en [technische preview voor Configuration Manager](../get-started/technical-preview.md)voor meer informatie.



## <a name="install"></a>Installeren
*Installeren* wordt gebruikt bij het maken van een nieuwe Configuration Manager-hiërarchie of het toevoegen van extra sites aan een bestaande hiërarchie.  

Wanneer u een nieuwe primaire site of centrale beheer site installeert, is de locatie van Setup. exe en de bijbehorende bron bestanden die u gebruikt, afhankelijk van uw installatie scenario.

Zie [installatie sites voorbereiden](../servers/deploy/install/prepare-to-install-sites.md)voor meer informatie.
