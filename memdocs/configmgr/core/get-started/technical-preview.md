---
title: Technical Preview-releases
titleSuffix: Configuration Manager
description: Meer informatie over de technische preview-vertakking om nieuwe functies en mogelijkheden in Configuration Manager te testen.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fd1e0bb45972bb9b3ba2a3e0bbfbb3d0509c4a8
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729298"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat informatie over de maandelijkse technische preview-vertakking van Configuration Manager. De Technical Preview introduceert nieuwe functionaliteit waaraan micro soft werkt. Het introduceert nieuwe functies die nog niet zijn opgenomen in de huidige vertakking van Configuration Manager. Deze functies zijn mogelijk uiteindelijk opgenomen in een update voor de huidige vertakking. Voordat we de functies volt ooien, willen we het uitproberen en ons feedback geven.

Omdat deze release een technische preview is, zijn de details en functionaliteit onderhevig aan wijzigingen.

Deze informatie is van toepassing op alle versies van de Configuration Manager Technical Preview-vertakking. In dit artikel vindt u een overzicht van elke nieuwe functie, samen met de Technical Preview-versie waarin deze voor het eerst wordt weer gegeven. Bijvoorbeeld versie **2001** voor januari (`01`) van 2020 (`20`). Voor afzonderlijke artikelen die aan elke preview-versie zijn toegewezen, worden de afzonderlijke functies beschreven.

Voor informatie over wat er nieuw is in de *huidige vertakking* van Configuration Manager raadpleegt u [Wat is er nieuw in Configuration Manager incrementele versies](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer:`https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a>Vereisten en beperkingen

> [!IMPORTANT]
> De Technical Preview is gelicentieerd voor gebruik in een test omgeving. Micro soft biedt mogelijk geen ondersteunings services en bepaalde functies zijn mogelijk niet beschikbaar in Technical previews. Daarnaast hebben technische preview-software mogelijk gereduceerde of andere beveiligings-, privacy-, toegankelijkheids-, beschik baarheids-en betrouwbaarheids normen ten opzichte van commerciële software.

Voor de meeste product vereisten gebruikt u de informatie in de [ondersteunde configuraties](../plan-design/configs/supported-configurations.md). De volgende uitzonde ringen zijn van toepassing op de Technical Preview-vertakking:

- Elke installatie is gedurende 90 dagen actief voordat deze inactief wordt.

- Engels is de enige ondersteunde taal.

- Alleen de volgende Setup-opdracht regel parameters worden ondersteund:

  - `/silent`
  - `/testdbupgrade`

- Het service verbindings punt wordt geïnstalleerd in de online modus. Het biedt geen ondersteuning voor de offline modus.

- De afzonderlijke artikelen voor elke specifieke versie van de Technical Preview bevatten aanvullende beperkingen of vereisten, zoals van toepassing.

- De volgende functies worden niet ondersteund voor de Technical Preview-vertakking:

  - [Migratie](../migration/migrate-data-between-hierarchies.md) naar of van deze preview-vertakking.

  - Voer een [upgrade uit](../servers/deploy/install/upgrade-to-configuration-manager.md) naar deze preview-vertakking.

  - [Site Recovery](../servers/manage/recover-sites.md) vanuit de map cd. latest.<!--507106-->

- Er is geen ondersteuning voor het bijwerken van de huidige vertakking vanuit deze preview-vertakking.

    > [!Note]
    > Als er updates beschikbaar zijn voor een preview-versie, kunt u deze nog steeds vinden en installeren vanuit het knoop punt **updates en onderhoud** van de Configuration Manager-console. Zie [Configuration Manager update pakketten installeren](https://www.youtube.com/embed/KBd_EGFbUT8) op YouTube.com voor een video van het upgrade proces in de console.

- Het ondersteunt alleen een zelfstandige primaire site. Er is geen ondersteuning voor een centrale beheer site, meerdere primaire sites of secundaire sites.

De technische preview-vertakking van Configuration Manager ondersteunt de volgende producten en technologieën:

- Tenzij anders vermeld, ondersteunt de branch Technical Preview dezelfde versies van SQL Server als de huidige vertakking. Zie [ondersteunde versies van SQL Server](../plan-design/configs/support-for-sql-server-versions.md)voor meer informatie.

- De site ondersteunt Maxi maal 10 clients, waarmee elke [ondersteunde client versie van het besturings systeem](../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)kan worden uitgevoerd.<!-- SCCMDocs#1656 -->

> [!Note]
> Het opnemen van deze producten in deze inhoud impliceert geen uitbrei ding van ondersteuning voor een versie die niet langer is dan de levens cyclus. Configuration Manager biedt geen ondersteuning voor producten die niet langer zijn dan de levens cyclus. Zie [micro soft Lifecycle-beleid](https://go.microsoft.com/fwlink/p/?LinkId=208270)voor meer informatie.

## <a name="install-and-update"></a><a name="bkmk_install"></a>Installeren en bijwerken

De Configuration Manager Technical Preview-vertakking voor het gebruik van Lab is verschillend van de Configuration Manager huidige vertakking voor productie gebruik.

Installeer eerst een basislijn versie van de Technical Preview-vertakking. Nadat u een basislijn versie hebt geïnstalleerd, gebruikt u in-console updates om de installatie up-to-date te zetten met de meest recente preview-versie. Normaal gesp roken zijn er elke maand nieuwe versies van de Technical Preview beschikbaar.

Micro soft biedt ondersteuning voor elke technische preview-versie tot drie opeenvolgende versies beschikbaar zijn. Als versie 1908 bijvoorbeeld is uitgebracht, wordt versie 1904 niet meer ondersteund. Versie 1905, 1906 en 1907 bleven in ondersteuning. Wanneer een basis lijn niet meer wordt ondersteund, wordt deze nog steeds ondersteund voor het installeren van een nieuwe Technical Preview-site, ervan uitgaande dat u onmiddellijk een ondersteunde versie bijwerkt. De oudere basis lijn wordt ondersteund totdat er een nieuwe basislijn versie beschikbaar is. Werk bij naar de meest recente beschik bare versie van de basis lijn en herhaal het update proces totdat u de nieuwste versie van Technical Preview installeert.

> [!TIP]
> Wanneer u een update installeert voor de Technical Preview, werkt u uw preview-installatie bij naar die nieuwe technische preview-versie. Een technische preview-installatie heeft nooit de mogelijkheid om een upgrade uit te kunnen uitvoeren naar een huidige vertakkings installatie. Er worden ook nooit updates van de huidige vertakkings versie ontvangen.
>
> Tijdens het hele jaar zijn er technische preview-vertakkingen en huidige branch-versies met hetzelfde versie nummer. Er is bijvoorbeeld een technische preview-versie 1910 en een actuele Branch versie 1910.

### <a name="active-baseline-versions"></a>Actieve basislijn versies

Installeer een basislijn versie van Maxi maal één jaar na de release. Gebruik de meest recente basislijn versie wanneer u een nieuwe Technical Preview-site installeert.

- **Technical Preview-versie 2002**: de Configuration Manager Technical Preview-vertakking versie 2002 is beschikbaar als een update in de console en als nieuwe basislijn versie.

Down load een basislijn versie van het [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a>Feedback geven

We horen graag uw feedback over de nieuwe functies in de Technical Preview. Zie [product feedback](../understand/find-help.md#product-feedback)voor meer informatie.

Als u ideeën hebt over nieuwe functies die u graag wilt zien, laat het ons weten! Verzend nieuwe ideeën en stem op de ideeën door anderen: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a>Functies in de meest recente versie

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2003.md) <!--ID-->

De volgende functies zijn beschikbaar met de meest recente versie van Configuration Manager Technical Preview:

### <a name="technical-preview-version-2004"></a>Technical Preview-versie 2004

- [Micro soft Endpoint Manager-Tenant bijvoegen: ConfigMgr-client Details](2020/technical-preview-2004.md#bkmk_mem) <!--6374854-->
- [Meldingen van micro soft](2020/technical-preview-2004.md#notifications-from-microsoft) <!--3953121-->
- [Detectie gegevens kopiëren vanaf de-console](2020/technical-preview-2004.md#bkmk_copydisco) <!--6890051-->
- [Verbeteringen in CMPivot](2020/technical-preview-2004.md#improvements-to-cmpivot) <!--6518631-->
- [Ondersteuning voor Power shell-versie 7](2020/technical-preview-2004.md#bkmk_pwsh7) <!--6023299-->
- [Verbetering van de taken reeks stap schijf Format teren en partitioneren](2020/technical-preview-2004.md#bkmk_osdpart) <!--6610288-->
- [Beheer Insight-regels voor implementatie van besturings systemen](2020/technical-preview-2004.md#bkmk_osdmi) <!--6982275-->
- [Power shell-cmdlets voor typen taken reeks implementatie](2020/technical-preview-2004.md#bkmk_osdpwsh) <!--7019342-->

> [!NOTE]
> Functies die beschikbaar waren in een eerdere versie van de Technical Preview blijven beschikbaar in latere versies. Op dezelfde manier blijven functies die worden toegevoegd aan de Configuration Manager huidige vertakking beschikbaar in de vertakking Technical Preview.

## <a name="features-in-recent-technical-previews"></a>Functies in recente technische previews

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

De volgende functies zijn uitgebracht met eerdere versies van de Configuration Manager Technical Preview-vertakking sinds huidige versie 2002 van de branch:

> [!TIP]
> Wanneer er een nieuwe huidige branch-versie beschikbaar is, worden de functies die beschikbaar zijn in die versie weer gegeven in het laatste artikel *Wat is er nieuw* . Zie [Wat is er nieuw in incrementele versies](../plan-design/changes/whats-new-incremental-versions.md#supported-versions)? voor meer informatie.

### <a name="technical-preview-version-2003"></a>Technical Preview-versie 2003

- [Configuration Manager-clients onboarden naar micro soft Defender ATP via de micro soft Endpoint Manager-console](2020/technical-preview-2003.md#bkmk_atp) <!--5691658-->
- [Herbemiddelingen van configuratie-items bijhouden](2020/technical-preview-2003.md#bkmk_track) <!--4261411 in 2002-->
- [Grens groepen voor apparaten weer geven](2020/technical-preview-2003.md#bkmk_boundary) <!--6521835 in 2002-->
- [Wizard Nieuwe feedback](2020/technical-preview-2003.md#bkmk_feedback) <!--3180826-->
- [Verbeteringen aan micro soft Edge Management dash board](2020/technical-preview-2003.md#bkmk_edge) <!--5907383-->
- [Verbeteringen in CMPivot](2020/technical-preview-2003.md#bkmk_cmpivot) <!--6518631-->
- [Query's verzenden naar micro soft om feedback te geven](2020/technical-preview-2003.md#bkmk_smile) <!--6488450-->
- [Nieuwe SDK-methode voor de voortgang van taken reeksen](2020/technical-preview-2003.md#bkmk_tsapi) <!--6448458-->
- [Verbeteringen in de implementatie van het besturings systeem](2020/technical-preview-2003.md#bkmk_osd) <!--6452769-->

## <a name="features-in-previous-technical-previews"></a>Functies in vorige technische previews

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

De volgende functies zijn uitgebracht met eerdere versies van de Configuration Manager Technical Preview-vertakking. Deze functies blijven beschikbaar in latere versies, maar zijn nog niet beschikbaar in de huidige vertakking.

| Functie        | Technical Preview-versie |
|----------------|---------------------------|
| Bestanden aan feedback toevoegen <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Verbeteringen aan multi cast-distributie punten <!--3785535--> | [Tech Preview 1908,2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Gefaseerde implementatie sjablonen <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Overal beheer op afstand met behulp van Cloud beheer gateway <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Verbeteringen in Community Hub <!--3555935--> | [Tech Preview 1906](2019/technical-preview-1906.md#bkmk_hub) |
| Verbeteringen in Community Hub <!--4224401--> | [Tech Preview 1905](2019/technical-preview-1905.md#bkmk_hub) |
| Community Hub en GitHub <!--3555935--> | [Tech Preview 1904](2019/technical-preview-1904.md#community-hub-and-github) |
| Kosten Estimator Cloud Services <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
| Rapporten downloaden van de Community Hub <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Community Hub <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| PXE-responder-service op basis van client <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| PXE-netwerk opstart ondersteuning voor IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Azure Active Directory gebruiken <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Verbeteringen in Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Zie ook

Raadpleeg voor meer informatie de volgende artikelen:

- [Configuration Manager evalueren in een lab](evaluate-with-lab-environment.md)
- [Wat is er nieuw in de incrementele versies van Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)
- [Inleiding tot Configuration Manager](../understand/introduction.md)

> [!Tip]
> Zie [voorlopige functies](../servers/manage/pre-release-features.md)voor meer informatie over de huidige branch-functies die toestemming nodig hebben om in te scha kelen.
>
> Zie [optionele functies van updates inschakelen](../servers/manage/install-in-console-updates.md#bkmk_options)voor meer informatie over de huidige branch-functies die u eerst moet inschakelen.
