---
title: Pre-release functies
titleSuffix: Configuration Manager
description: Functies van de voorlopige versie zijn functies die zich in de huidige vertakking bevinden voor vroege tests in een productie omgeving.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720154"
---
# <a name="pre-release-features-in-configuration-manager"></a>Functies van de voorlopige versie van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Functies van de voorlopige versie zijn functies die zich in de huidige vertakking bevinden voor vroege tests in een productie omgeving. Deze functies worden volledig ondersteund, maar zijn nog steeds actief in ontwikkeling. Ze kunnen wijzigingen ontvangen totdat ze de categorie van de voorlopige versie verlaten.

## <a name="give-consent"></a>Toestemming geven  

Voordat u functies van de voorlopige versie gebruikt, moet u toestemming geven voor het gebruik van functies van de voorlopige versie. Het verlenen van toestemming is een eenmalige actie per hiërarchie die u niet ongedaan kunt maken. Totdat u toestemming geeft, kunt u geen nieuwe functies van de evaluatie versie inschakelen die zijn opgenomen in updates. Nadat u een functie van een evaluatie versie hebt ingeschakeld, kunt u deze niet uitschakelen.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Klik op **hiërarchie-instellingen** in het lint.  

3. Schakel op het tabblad **Algemeen** van de eigenschappen van de hiërarchie-instellingen de optie in om **toestemming te geven voor het gebruik van functies van de voorlopige versie**. Klik op **OK**.  

## <a name="enable-pre-release-features"></a>Functies van de voorlopige versie inschakelen

Wanneer u een update installeert die functies van de voorlopige versie bevat, zijn deze functies zichtbaar in de wizard updates en onderhoud met de normale functies die in de update zijn opgenomen.

### <a name="if-you-have-given-consent"></a>Als u toestemming hebt gegeven

Schakel in de wizard updates en onderhoud de functies van de voorlopige versie in. Selecteer de functies van de voorlopige versie, net als bij andere onderdelen.

U kunt de functies van de voorlopige versie desgewenst later van het knoop punt **functies** inschakelen onder **updates en onderhoud** in de werk ruimte **beheer** . Selecteer een functie en klik vervolgens op **inschakelen** in het lint. Deze optie is niet beschikbaar voor gebruik totdat u toestemming geeft.

### <a name="if-you-havent-given-consent"></a>Als u geen toestemming hebt gegeven

In de wizard updates en onderhoud zijn de functies van de voorlopige versie zichtbaar, maar u kunt ze niet inschakelen. Nadat de update is geïnstalleerd, zijn deze functies zichtbaar in het knoop punt **functies** . U kunt ze echter pas inschakelen als u toestemming geeft.

> [!IMPORTANT]  
> In een hiërarchie met meerdere sites kunt u alleen de functies optionele of voorlopige versie inschakelen op de centrale beheer site. Dit gedrag zorgt ervoor dat er geen conflicten zijn tussen de hiërarchie. <!--507197-->  
>
> Als u toestemming hebt gegeven op een zelfstandige primaire site en vervolgens de hiërarchie uitvouwt door een nieuwe centrale beheer site te installeren, moet u opnieuw toestemming geven op de centrale beheer site.  

Wanneer u een voorlopige functie inschakelt, moet de Configuration Manager hiërarchie beheerder (HMAN) de wijziging verwerken voordat deze functie beschikbaar wordt. De verwerking van de wijziging is vaak direct. Afhankelijk van de HMAN-verwerkings cyclus kan het tot 30 minuten duren voordat deze is voltooid. Nadat de wijziging is verwerkt, start u de console opnieuw voordat u de functie gebruikt.

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a>Lijst met functies van de voorlopige versie

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Functie          | Toegevoegd als voorlopige versie | Toegevoegd als een volledige functie |
|------------------|----------------------|-------------------------|
| [Orchestration-groepen](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | Versie 2002 | ![Nog niet](media/red_x.png) |
| [Implementatie type voor taken reeks](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | Versie 2002 | ![Nog niet](media/red_x.png) |
| [De centrale beheer site verwijderen](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | Versie 2002 | ![Nog niet](media/red_x.png) |
| [Fout opsporing voor taken reeksen](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Versie 1906 | ![Nog niet](media/red_x.png) |
| [Toepassings groepen](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Versie 1906 | ![Nog niet](media/red_x.png) |
| [Detectie van gebruikers groepen Azure Active Directory](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Versie 1906 | Versie 2002 |
| [Resultaten van verzamelings lidmaatschap synchroniseren met Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Versie 1906| Versie 2002 |
| [Zelfstandige CMPivot](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | Versie 1906 | Versie 2002 |
| [Beheer service SMS-provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | Versie 1810 | Versie 1906 |
| [Verbeterd HTTP-site systeem](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | Versie 1806 | Versie 1810 |
| [Client-apps voor gezamenlijk beheerde apparaten](../../../comanage/workloads.md#client-apps) <br/> (voorheen bekend als *Mobile Apps voor gezamenlijk beheerde apparaten*) <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Versie 1806 | Versie 2002 |
| [Pakket conversie beheer](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | Versie 1806 | Versie 1810 |
| [Gefaseerde implementaties](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | Versie 1802 | Versie 1806 |
| [Beheer van Windows Defender-toepassingsbeheer](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | Versie 1702 | Versie 1906 |
| [Onderhoud van een cluster bewuste verzameling (Server groepen)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Versie 1602 | ![Nog niet](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> Zie [optionele functies van updates inschakelen](install-in-console-updates.md#bkmk_options)voor meer informatie over niet-voorlopige functies die u eerst moet inschakelen.  
>
> Zie [Technical Preview](../../get-started/technical-preview.md)voor meer informatie over functies die alleen beschikbaar zijn in de vertakking Technical Preview.  
