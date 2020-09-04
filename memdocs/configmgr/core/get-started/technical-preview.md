---
title: Technical Preview-releases
titleSuffix: Configuration Manager
description: Meer informatie over de technische preview-vertakking om nieuwe functies en mogelijkheden in Configuration Manager te testen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eff1ec6a8346132853285195d8e96aa6b8d3a8fa
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432571"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat informatie over de maandelijkse technische preview-vertakking van Configuration Manager. De Technical Preview introduceert nieuwe functionaliteit waaraan micro soft werkt. Het introduceert nieuwe functies die nog niet zijn opgenomen in de huidige vertakking van Configuration Manager. Deze functies zijn mogelijk uiteindelijk opgenomen in een update voor de huidige vertakking. Voordat we de functies volt ooien, willen we het uitproberen en ons feedback geven.

Omdat deze release een technische preview is, zijn de details en functionaliteit onderhevig aan wijzigingen.

Deze informatie is van toepassing op alle versies van de Configuration Manager Technical Preview-vertakking. In dit artikel vindt u een overzicht van elke nieuwe functie, samen met de Technical Preview-versie waarin deze voor het eerst wordt weer gegeven. Bijvoorbeeld versie **2001** voor januari ( `01` ) van 2020 ( `20` ). Voor afzonderlijke artikelen die aan elke preview-versie zijn toegewezen, worden de afzonderlijke functies beschreven.

Voor informatie over wat er nieuw is in de *huidige vertakking* van Configuration Manager raadpleegt u [Wat is er nieuw in Configuration Manager incrementele versies](../plan-design/changes/whats-new-incremental-versions.md).

> [!Tip]
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="requirements-and-limitations"></a><a name="bkmk_reqs"></a> Vereisten en beperkingen

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
> Het opnemen van deze producten in deze inhoud impliceert geen uitbrei ding van ondersteuning voor een versie die niet langer is dan de levens cyclus. Configuration Manager biedt geen ondersteuning voor producten die niet langer zijn dan de levens cyclus. Zie [micro soft Lifecycle-beleid](https://support.microsoft.com/lifecycle)voor meer informatie.

## <a name="install-and-update"></a><a name="bkmk_install"></a> Installeren en bijwerken

De Configuration Manager Technical Preview-vertakking voor het gebruik van Lab is verschillend van de Configuration Manager huidige vertakking voor productie gebruik.

Installeer eerst een basislijn versie van de Technical Preview-vertakking. Nadat u een basislijn versie hebt geïnstalleerd, gebruikt u in-console updates om de installatie up-to-date te zetten met de meest recente preview-versie. Normaal gesp roken zijn er elke maand nieuwe versies van de Technical Preview beschikbaar.

Micro soft biedt ondersteuning voor elke technische preview-versie tot drie opeenvolgende versies beschikbaar zijn. Als versie 1908 bijvoorbeeld is uitgebracht, wordt versie 1904 niet meer ondersteund. Versie 1905, 1906 en 1907 bleven in ondersteuning. Wanneer een basis lijn niet meer wordt ondersteund, wordt deze nog steeds ondersteund voor het installeren van een nieuwe Technical Preview-site, ervan uitgaande dat u onmiddellijk een ondersteunde versie bijwerkt. De oudere basis lijn wordt ondersteund totdat er een nieuwe basislijn versie beschikbaar is. Werk bij naar de meest recente beschik bare versie van de basis lijn en herhaal het update proces totdat u de nieuwste versie van Technical Preview installeert.

> [!TIP]
> Wanneer u een update installeert voor de Technical Preview, werkt u uw preview-installatie bij naar die nieuwe technische preview-versie. Een technische preview-installatie heeft nooit de mogelijkheid om een upgrade uit te kunnen uitvoeren naar een huidige vertakkings installatie. Er worden ook nooit updates van de huidige vertakkings versie ontvangen.
>
> Tijdens het hele jaar zijn er technische preview-vertakkingen en huidige branch-versies met hetzelfde versie nummer. Er is bijvoorbeeld een technische preview-versie 1910 en een actuele Branch versie 1910.

### <a name="active-baseline-versions"></a>Actieve basislijn versies

Installeer een basislijn versie van Maxi maal één jaar na de release. Gebruik de meest recente basislijn versie wanneer u een nieuwe Technical Preview-site installeert. De volgende Configuration Manager Technical Preview-versies van branches zijn beschikbaar als updates in de-console en als nieuwe basislijn versies:

- **Technical Preview-versie 2007**

Down load een basislijn versie van het [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="providing-feedback"></a><a name="BKMK_TPFeedback"></a> Feedback geven

We horen graag uw feedback over de nieuwe functies in de Technical Preview. Zie [product feedback](../understand/find-help.md#product-feedback)voor meer informatie.

Als u ideeën hebt over nieuwe functies die u graag wilt zien, laat het ons weten! Verzend nieuwe ideeën en stem op de ideeën door anderen: [Configuration Manager UserVoice](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="features-in-the-most-recent-version"></a><a name="bkmk_tpCaps"></a> Functies in de meest recente versie

<!-- (explanatory comment)
This is the full list of new features in the latest TP release

bullet format:
<!-- - [title](2020/technical-preview-2007.md) <!--ID-->

De volgende functies zijn beschikbaar met de meest recente versie van Configuration Manager Technical Preview:

### <a name="technical-preview-version-2008"></a>Technical Preview-versie 2008

- [Voor beeld van verzamelings query](2020/technical-preview-2008.md#collection-query-preview) <!--7380401-->
- [SetupDiag-fouten analyseren voor onderdeel updates](2020/technical-preview-2008.md#bkmk_setupdiag) <!--4385028-->
- [Scenario status bewaken](2020/technical-preview-2008.md#bkmk_health) <!--7699463-->
- [Evaluatie weergave verzameling](2020/technical-preview-2008.md#bkmk_colleval) <!--6251274-->
- [Zie de grootte van de taken reeks in de-console](2020/technical-preview-2008.md#bkmk_tssize) <!--7645732-->
- [Taak verouderde verzamelde bestanden voor diagnostische gegevens verwijderen](2020/technical-preview-2008.md#bkmk_logs) <!--6503308-->
- [Objecten importeren in huidige map](2020/technical-preview-2008.md#bkmk_folder) <!--6601203-->

> [!NOTE]
> Functies die beschikbaar waren in een eerdere versie van de Technical Preview blijven beschikbaar in latere versies. Op dezelfde manier blijven functies die worden toegevoegd aan de Configuration Manager huidige vertakking beschikbaar in de vertakking Technical Preview.

## <a name="features-in-recent-technical-previews"></a>Functies in recente technische previews

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

De volgende functies zijn uitgebracht met eerdere versies van de Configuration Manager Technical Preview-vertakking sinds huidige versie 2006 van de branch:

> [!TIP]
> Wanneer er een nieuwe huidige branch-versie beschikbaar is, worden de functies die beschikbaar zijn in die versie weer gegeven in het laatste artikel *Wat is er nieuw* . Zie [Wat is er nieuw in incrementele versies](../plan-design/changes/whats-new-incremental-versions.md#supported-versions)? voor meer informatie.

### <a name="technical-preview-version-2007"></a>Technical Preview-versie 2007

- [Tenant bijvoegen: hardware-inventaris weer geven in micro soft Endpoint Manager-beheer centrum](2020/technical-preview-2007.md#bkmk_mem) <!--6479284-->
- [Verbeteringen in het dash board van client gegevens bronnen](2020/technical-preview-2007.md#bkmk_content) <!--7102084-->
- [Het letter type met de vaste breedte wordt nu in sommige console gebieden gebruikt](2020/technical-preview-2007.md#bkmk_font) <!--7632637-->
- [Grootte van taken reeks beleid beheren](2020/technical-preview-2007.md#bkmk_tspol) <!--6888853-->
- [Verbeteringen in de tijd lijn van het apparaat in het beheer centrum](2020/technical-preview-2007.md#bkmk_timeline)<!--7141381-->

## <a name="features-in-previous-technical-previews"></a>Functies in vorige technische previews

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

De volgende functies zijn uitgebracht met eerdere versies van de Configuration Manager Technical Preview-vertakking. Deze functies blijven beschikbaar in latere versies, maar zijn nog niet beschikbaar in de huidige vertakking.

| Functie        | Technical Preview-versie |
|----------------|---------------------------|
| Verbeteringen in beschik bare apps via CMG <!--7033501--> | [Tech Preview 2006](2020/technical-preview-2006.md#bkmk_availapp) |
| Tenantkoppeling: Tijdlijn van het apparaat in het beheercentrum <!--7141381--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_timeline) |
| Tenantkoppeling: CMPivot vanuit het beheercentrum <!--6024392--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_cmpivot) |
| Tenantkoppeling: Scripts uitvoeren vanuit het beheercentrum <!--6234688--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_scripts) |
| Verbeteringen in de Cloud Management Gateway-cmdlets <!--6978300--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_pwshcmg) |
| Fouten bij het instellen van rapporten en upgrades naar micro soft <!--5622909--> | [Tech Preview 2005](2020/technical-preview-2005.md#report-setup-and-upgrade-failures-to-microsoft) |
| Verbeteringen in het hulp programma voor het opschonen van inhouds bibliotheken <!--6887878--> | [Tech Preview 2005](2020/technical-preview-2005.md#bkmk_content) |
| Detectie gegevens kopiëren vanaf de-console <!--6890051--> | [Tech Preview 2004](2020/technical-preview-2004.md#bkmk_copydisco) |
| Ondersteuning voor Power shell-versie 7 <!--6023299--> | [Tech Preview 2004](2020/technical-preview-2004.md#bkmk_pwsh7) |
| Wizard Nieuwe feedback <!--3180826--> | [Tech Preview 2003](2020/technical-preview-2003.md#bkmk_feedback) |
| Query's verzenden naar micro soft om feedback te geven <!--6488450--> | [Tech Preview 2003](2020/technical-preview-2003.md#bkmk_smile) |
| Bestanden aan feedback toevoegen <!--3556011--> | [Tech Preview 1910](2019/technical-preview-1910.md#attach-files-to-feedback) |
| Verbeteringen aan multi cast-distributie punten <!--3785535--> | [Tech Preview 1908,2](2019/technical-preview-1908-2.md#bkmk_multicast) |
| Gefaseerde implementatie sjablonen <!--4961086--> | [Tech Preview 1908](2019/technical-preview-1908.md#phased-deployment-templates) |
| Overal beheer op afstand met behulp van Cloud beheer gateway <!--4575930--> | [Tech Preview 1906](2019/technical-preview-1906.md#remote-control-anywhere-using-cloud-management-gateway) |
| Kosten Estimator Cloud Services <!--3555774--> | [Tech Preview 1903](2019/technical-preview-1903.md#bkmk_cmg) |
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
