---
title: Client upgrades voor Windows uitsluiten
titleSuffix: Configuration Manager
description: Informatie over het uitsluiten van een upgrade van Windows-clients in Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715415"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>Clients uitsluiten van een upgrade in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt een verzameling clients uitsluiten van de automatische installatie van bijgewerkte client versies. Gebruik deze uitsluiting voor een verzameling computers die meer aandacht nodig hebben bij het upgraden van de client. Een client in een uitgesloten verzameling negeert aanvragen voor het installeren van bijgewerkte client software.

Deze uitsluiting is van toepassing op de volgende methoden:

- Automatische upgrade
- Upgrade op basis van software-updates
- Aanmeldings scripts
- Groeps beleid

> [!NOTE]
> Hoewel in de gebruikers interface wordt aangegeven dat clients niet via een van beide methoden worden bijgewerkt, zijn er twee manieren die u kunt gebruiken om deze instellingen te overschrijven. Gebruik client push of hand matige client installatie om deze configuratie te negeren. Zie [een uitgesloten client upgraden](#bkmk_override)voor meer informatie.

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a>Uitsluiting configureren

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit, selecteer het knoop punt **sites** en selecteer vervolgens **hiërarchie-instellingen** in het lint.

2. Schakel over naar het tabblad **client upgrade** .

3. Selecteer de optie om de **opgegeven clients uit te sluiten van de upgrade**. Selecteer vervolgens de **uitsluitings verzameling** die u wilt uitsluiten. U kunt slechts één verzameling voor uitsluiting selecteren.

4. Selecteer **OK** om het venster te sluiten en de configuratie op te slaan.

![Instellingen voor automatische upgrade uitsluiting](media/automatic_upgrade_exclusion.png)

Nadat clients in het beleid voor het bijwerken van de verzameling zijn uitgesloten, worden client updates niet automatisch geïnstalleerd. Zie [clients voor Windows-computers bijwerken voor](upgrade-clients-for-windows-computers.md)meer informatie.

> [!NOTE]
> Uitgesloten clients worden nog steeds gedownload en kunnen Ccmsetup worden uitgevoerd, maar niet upgraden.

Wanneer u een client verwijdert uit de uitsluitings verzameling, wordt deze niet automatisch bijgewerkt tot de volgende cyclus voor automatische upgrades.

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a>Een upgrade uitvoeren van een uitgesloten client

Als een apparaat lid is van een verzameling die u hebt uitgesloten van een upgrade, kunt u de client nog steeds upgraden met een van de volgende methoden:

- **Push-client installatie**: Ccmsetup staat push installatie van de client toe, omdat het uw directe intentie is. Met deze methode kunt u een client bijwerken zonder deze uit de verzameling te verwijderen, of de volledige verzameling uit de uitsluiting verwijderen.

- **Hand matige client installatie**: een uitgesloten client hand matig bijwerken met behulp van de volgende Ccmsetup-opdracht regel parameter: **/IgnoreSkipUpgrade**

    Als u probeert een client die lid is van de uitgesloten verzameling hand matig te upgraden en deze para meter niet gebruikt, wordt de client niet bijgewerkt. Zie [Configuration Manager-clients hand matig installeren](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)voor meer informatie.

## <a name="see-also"></a>Zie ook

- [Clients bijwerken](upgrade-clients.md)

- [Clients implementeren op Windows-computers](../../deploy/deploy-clients-to-windows-computers.md)

- [Uitgebreide interoperabiliteit client](../../../understand/interoperability-client.md)
