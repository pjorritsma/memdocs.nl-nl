---
title: Replicatie op basis van een bestand
titleSuffix: Configuration Manager
description: Meer informatie over hoe Configuration Manager replicatie op basis van bestanden gebruikt om gegevens over te dragen tussen sites in uw hiërarchie
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720168"
---
# <a name="file-based-replication"></a>Replicatie op basis van een bestand

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager maakt gebruik van op bestanden gebaseerde replicatie om gegevens op basis van bestanden over te dragen tussen sites in uw hiërarchie. Deze gegevens omvatten toepassingen en pakketten die u wilt implementeren naar distributie punten in onderliggende sites. Ook worden niet-verwerkte detectie gegevens records verwerkt die door de site worden overgedragen naar de bovenliggende site en vervolgens processen.  

Communicatie op basis van bestanden tussen sites maakt gebruik van het SMB-protocol ( *Server Message Block* ) op TCP/IP-poort 445. Als u de hoeveelheid gegevens die de site overbrengt over het netwerk wilt beheren, geeft u bandbreedte beperking en Pulse-modus op. Gebruik schema's om te bepalen wanneer gegevens via het netwerk moeten worden verzonden.  

## <a name="routes"></a><a name="bkmk_routes"></a>Stuurt

De volgende informatie kan u helpen bij het instellen en gebruiken van bestands replicatie routes.  

### <a name="file-replication-route"></a>Route voor bestands replicatie

Elke bestands replicatie route identificeert een doel site waarnaar een site gegevens op basis van bestanden overbrengt. Elke site ondersteunt één bestands replicatie route naar een specifieke doel site.  

Als u een route voor bestands replicatie wilt beheren, gaat u naar de werk ruimte **beheer** . Vouw het knoop punt **hiërarchie configuratie** uit en selecteer vervolgens **Bestands replicatie**.  

U kunt de volgende instellingen voor bestands replicatie routes wijzigen:  

#### <a name="file-replication-account"></a>Account voor bestands replicatie

Dit account maakt verbinding met de doel site en schrijft gegevens naar de **SMS_Site** -share van die site. De ontvangende site verwerkt de gegevens die naar deze share zijn geschreven. Wanneer u een site aan de hiërarchie toevoegt, wijst Configuration Manager standaard het computer account van de nieuwe site server toe als het account voor bestands replicatie. Vervolgens wordt dit account toegevoegd aan de groep van `SMS_SiteToSiteConnection_<sitecode>` de doel site. Deze groep is lokaal op de computer die toegang verleent tot de SMS_Site share. U kunt dit account zodanig wijzigen, dat dit een Windows gebruikersaccount is. Als u het account wijzigt, moet u ervoor zorgen dat u het nieuwe account toevoegt aan de `SMS_SiteToSiteConnection_<sitecode>` groep van de doel site.  

> [!NOTE]  
> Secundaire sites gebruiken altijd het computeraccount van de secundaire siteserver als het **Account voor bestandsreplicatie**.  

#### <a name="schedule"></a>Planning

Het schema voor elke bestands replicatie route instellen. Deze actie beperkt het type gegevens en de tijd waarop gegevens naar de doel site kunnen worden overgedragen.  

#### <a name="rate-limits"></a>Frequentie limieten

Geef de frequentie limieten voor elke bestands replicatie route op. Deze actie bepaalt de netwerk bandbreedte die de site gebruikt bij het overdragen van gegevens naar de doel site:  

- **Pulse-modus**: Geef de grootte op van de gegevens blokken die de site naar de doel site verzendt. U kunt daarnaast een vertraging tussen het verzenden van de afzonderlijke gegevensblokken opgeven. Gebruik deze optie wanneer u gegevens via een netwerk verbinding met een lage band breedte naar de doel site moet verzenden.

    U hebt bijvoorbeeld beperkingen om elke vijf seconden 1 KB aan gegevens te verzenden, maar niet elke drie seconden 1 KB. Deze beperking is ongeacht de snelheid van de koppeling of het gebruik ervan op een bepaald moment.

- **Beperkt tot de maximale overdrachts snelheid per uur**: de site verzendt gegevens naar een doel site door alleen het percentage tijd te gebruiken dat u opgeeft. Configuration Manager identificeert de beschik bare band breedte van het netwerk niet. De tijd waarmee gegevens kunnen worden verzonden, wordt gesplitst in segmenten van tijd. Vervolgens worden de gegevens in een kort tijds blok verzonden, gevolgd door tijds blokken waarin geen gegevens worden verzonden.

    U stelt bijvoorbeeld het maximum percentage in op **50%**. Configuration Manager verzendt gegevens gedurende een bepaalde tijd, gevolgd door een periode waarin er geen gegevens worden verzonden. De werkelijke grootte van het gegevens blok dat wordt verzonden, wordt niet beheerd. De site beheert alleen de hoeveelheid tijd waarin gegevens worden verzonden.  

    > [!CAUTION]  
    > Standaard kan een site maximaal drie **gelijktijdige verzendingen** gebruiken om gegevens naar een doelsite over te dragen. Wanneer u frequentie limieten voor een bestands replicatie route inschakelt, worden de **gelijktijdige verzen** dingen naar die site beperkt tot één. Dit gedrag geldt ook wanneer de **limiet beschik bare band breedte (%)** is ingesteld op **100%**. Als u bijvoorbeeld de standaard instellingen voor de afzender gebruikt, wordt hiermee de overdrachts verhouding naar de doel site verminderd tot een derde van de standaard capaciteit.  

#### <a name="routes-between-secondary-sites"></a>Routes tussen secundaire sites

Configureer een route voor bestands replicatie tussen twee secundaire sites om op bestanden gebaseerde inhoud tussen deze sites te routeren.  


### <a name="sender"></a>Afzender

Elke site heeft één afzender. De afzender beheert de netwerk verbinding van de ene site met de doel site. Het kan verbinding maken met meerdere sites tegelijk. Om verbinding te maken met een site, gebruikt de afzender de bestands replicatie route naar de site en identificeert het account dat wordt gebruikt om de netwerk verbinding tot stand te brengen. De afzender gebruikt dit account ook om gegevens naar de SMS_Site share van de doel site te schrijven.  

Standaard schrijft de afzender gegevens naar een doel site door meerdere **gelijktijdige verzen**dingen of een *thread*te gebruiken. Elke thread kan een ander op bestanden gebaseerd object overdragen naar de doel site. Wanneer de afzender een object begint te verzenden, blijft er gegevens blokken voor dat object schrijven totdat het het hele object verzendt. Nadat alle gegevens voor het object zijn verzonden, kan een nieuw object beginnen met verzenden op die thread.  

Als u de afzender voor een site wilt beheren, gaat u naar de werk ruimte **beheer** en vouwt u het knoop punt **site configuratie** uit. Selecteer het knoop punt **sites** en selecteer vervolgens **Eigenschappen** voor de site die u wilt beheren. Ga naar het tabblad **afzender** om de instellingen van de afzender te wijzigen.  

U kunt de volgende instellingen voor een afzender wijzigen:  

#### <a name="maximum-concurrent-sendings"></a>Maximum aantal gelijktijdige verzen dingen

Elke site gebruikt standaard vijf gelijktijdige verzen dingen (threads). Er zijn drie threads beschikbaar voor gebruik bij het verzenden van gegevens naar een wille keurige doel site. Wanneer u dit aantal verhoogt, kunt u de door Voer van gegevens tussen sites verg Roten. Meer threads betekenen dat Configuration Manager op hetzelfde moment meer bestanden kunt overdragen. Door dit aantal te verhogen wordt de vraag voor netwerkbandbreedte tussen sites ook verhoogd.  

#### <a name="retry-settings"></a>Instellingen voor opnieuw proberen

Standaard probeert elke site een probleem verbinding twee keer, met een vertraging van één minuut tussen de verbindings pogingen. U kunt het aantal verbindings pogingen wijzigen dat door de site wordt gemaakt en hoe lang er moet worden gewacht tussen pogingen.  


## <a name="next-steps"></a>Volgende stappen

[Databasereplicatie](database-replication.md)
