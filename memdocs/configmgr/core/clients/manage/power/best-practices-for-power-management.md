---
title: Aanbevelingen voor energie beheer
titleSuffix: Configuration Manager
description: Meer informatie over micro soft-aanbevelingen voor energie beheer in Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715261"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Aanbevelingen voor energie beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de volgende aanbevelingen voor energie beheer in Configuration Manager.  

## <a name="monitor-at-a-representative-time"></a>Bewaken op een representatief tijdstip

De bewakings fase van energie beheer biedt u de volgende gegevens van computers in uw organisatie:

- Energie verbruik
- Activiteit
- Mogelijkheden voor energie beheer
- Uitwerking op het milieu

Kies een representatieve tijd om de apparaten te bewaken. Bijvoorbeeld: bewaking tijdens een open bare feestdag biedt geen realistisch rapport over het energie verbruik van de computer.

## <a name="create-a-control-collection"></a>Een controle verzameling maken

Maak twee verzamelingen van computers om de gevolgen te controleren van het toepassen van energiebeheerschema's op computers. De eerste verzameling moet het meren deel van de computers bevatten waarop u energie-instellingen wilt Toep assen. De *controle verzameling* moet de overige computers bevatten. Pas het vereiste energiebeheer schema toe op de eerste verzameling. Voer vervolgens rapporten uit om de impact tussen de twee verzamelingen te vergelijken.  

## <a name="run-reports-before-you-apply-a-plan"></a>Rapporten uitvoeren voordat u een plan toepast

Voordat u een energiebeheer schema toepast op een verzameling computers, voert u het rapport **energie-instellingen** uit. Gebruik dit rapport om inzicht te krijgen in de energiebeheer instellingen die al zijn geconfigureerd op computers in de verzameling. Als u nieuwe Energiebeheer instellingen op computers toepast zonder eerst de bestaande instellingen te controleren, kan dit het energie verbruik verhogen.  

## <a name="exclude-servers"></a>Servers uitsluiten

Energie beheer voor computers met Windows Server wordt niet ondersteund. Servers toevoegen aan een verzameling en deze uitsluiten van energie beheer.  

> [!NOTE]
> Hoewel Configuration Manager energie beheer van Windows Server niet ondersteunt, verzamelt het nog steeds gegevens over het energie verbruik voor analyse en rapportage.

## <a name="exclude-other-computers"></a>Andere computers uitsluiten

Als u computers hebt die u niet wilt beheren met energie beheer, voegt u deze computers toe aan een uitsluitings verzameling.  

U kunt het beste de volgende typen computers uitsluiten van energie beheer:

- Computers die moeten blijven ingeschakeld.  

- Computers die gebruikers nodig hebben om extern verbinding te maken.  

- Computers die energie beheer niet kunnen gebruiken.  

- Computers waaraan de sitesysteemrol Distributiepunt is toegewezen.  

- Open bare computers, zoals kiosk computers, informatie schermen of bewakings consoles waarbij de computer en de monitor altijd moeten worden ingeschakeld.  

Zie [energie beheer configureren](configuring-power-management.md)voor meer informatie.  

## <a name="apply-power-plans-to-a-test-collection"></a>Energiebeheer schema's Toep assen op een test verzameling

Test het effect van het toepassen van een energiebeheerschema op een testverzameling computers voordat u het energiebeheerschema op een grotere verzameling computers toepast.  

Wanneer u een computer uit energie beheer uitsluit, worden alle energie-instellingen teruggezet naar de oorspronkelijke waarden. U kunt de oorspronkelijke waarden van afzonderlijke energie-instellingen niet herstellen.  

## <a name="apply-power-plan-settings-individually"></a>Energiebeheerschema-instellingen afzonderlijk toepassen

Controleer het effect van het Toep assen van elke energie-instelling voordat u de volgende toepast. Dit proces zorgt ervoor dat elke instelling het vereiste effect heeft. Zie [beschik bare energiebeheer schema-instellingen](create-and-apply-power-plans.md#BKMK_Plans)voor meer informatie over instellingen voor energie schema's.  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>Computers regel matig controleren op meerdere energiebeheer schema's

Energie beheer bevat een rapport met computers waarop meer dan één energiebeheer schema is toegepast: **computers met meerdere energiebeheer schema's**.

Als een computer lid is van meerdere verzamelingen, worden elk verschillende energiebeheer schema's toegepast, dan geldt het volgende gedrag:  

- **Energiebeheer schema**: als u meerdere waarden voor energie-instellingen op een computer toepast, wordt de minst beperkende waarde gebruikt.  

- **Activerings tijd**: als u meerdere activerings tijden op een desktop computer toepast, wordt de tijd gebruikt die het dichtst bij middernacht ligt.  

Zie [computers met meerdere energiebeheer schema's](monitor-and-plan-for-power-management.md#BKMK_Multiple)voor meer informatie.  

## <a name="save-or-export-power-management-information"></a>Energie beheer gegevens opslaan of exporteren

Wanneer u rapporten uitvoert tijdens de controle-en nalevings fase, slaat u de resultaten op of exporteert u deze. Houd de gegevens voor latere vergelijking in het geval Configuration Manager later de gegevens verwijdert.  

Configuration Manager houdt in de site database de volgende informatie over energie beheer:

- Informatie over energie beheer die wordt gebruikt door dagelijkse rapporten: 31 dagen

- Informatie over energie beheer die wordt gebruikt door maandelijkse rapporten: 13 maanden
