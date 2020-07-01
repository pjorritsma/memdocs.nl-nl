---
title: Updates in Desktop Analytics
titleSuffix: Configuration Manager
description: Meer informatie over beveiligings-en functie-updates in Desktop Analytics.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 96a014f4919480854b57bae82e982ce783f5f59b
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590963"
---
# <a name="updates-in-desktop-analytics"></a>Updates in Desktop Analytics

Bekijk de status van beveiligings-en functie-updates in de Desktop Analytics-Portal. Selecteer deze knoop punten in de groep monitor van het hoofd menu van Desktop Analytics. Deze knoop punten geven u inzicht in de status van deze updates in uw omgeving.

<!--7362999-->

> [!IMPORTANT]
> Desktop Analytics geeft de update status van beveiliging en onderdelen weer voor apparaten met de commerciële ID die is gekoppeld aan de werk ruimte van uw bureau blad Analytics. Dit gedrag treedt op of u de apparaten hebt Inge schreven bij Configuration Manager. Het totale aantal apparaten op deze tegels komt mogelijk niet overeen met het aantal geregistreerde apparaten in [**verbonden services**](monitor-connection-health.md#commercial-id-configuration).

## <a name="security-updates"></a>Beveiligingsupdates

Als u de huidige status van beveiligings updates wilt controleren, selecteert u **beveiligings updates** in het gedeelte **monitor** van Desktop Analytics:

![Knoop punt beveiligings updates van Desktop Analytics](media/security-updates.png)

In deze weer gave vindt u een overzicht van de *beveiligings* updates voor apparaten met Windows 10. Apparaten in het staaf diagram worden gecategoriseerd op de volgende labels:

#### <a name="latest"></a>Jongste

Op apparaten wordt de meest recente beveiligings update uitgevoerd voor die versie en dit kanaal.

#### <a name="latest-1"></a>Nieuwste-1

Op apparaten wordt een eerdere versie van de beveiligings update uitgevoerd dan de meest recente beschik bare update op dat kanaal.

#### <a name="older"></a>Ouder

Op apparaten wordt een beveiligings update uitgevoerd die ouder is dan de nieuwste-1.

#### <a name="not-measured"></a>Niet gemeten

Het apparaat is niet beoordeeld door Desktop Analytics. Deze status omvat apparaten met Windows 7, Windows 8,1 of Windows 10-apparaten die zijn geregistreerd voor het Windows Insider-programma.  

Als u de trends van de acceptatie voor beveiligings updates wilt zien, selecteert u **meer weer geven** voor een specifieke versie van Windows. In het gestapelde vlak diagram worden apparaten gecategoriseerd op basis van de beveiligings update die ze na verloop van tijd hebben geïnstalleerd.

Als u de implementatie status voor beveiligings updates wilt controleren, selecteert u **alles weer geven**. In deze weer gave ziet u de apparaten in de volgende categorieën:

- Niet gestart
- Wordt uitgevoerd
- Voltooid
- Aandacht vereist: apparaten (gesorteerd op apparaatnaam)
- Aandacht vereist: problemen (gesorteerd op probleem type)

Selecteer **recente gegevens weer**geven om apparaten weer te geven met nieuwe informatie die de service nog wordt verwerkt. In Desktop Analytics wordt deze informatie weer gegeven na de volgende volledige gegevens vernieuwing.

  > [!IMPORTANT]
  > De optie Desktop Analytics om **recente gegevens weer te geven** , is afgeschaft. Deze actie wordt verwijderd in een toekomstige versie van de Desktop Analytics-service. Zie [afgeschafte functies](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.<!--7080949-->  

## <a name="feature-updates"></a>Onderdelenupdates

Als u de huidige status van onderdelen updates wilt controleren, selecteert u **onderdelen updates** in het gedeelte **monitor** van Desktop Analytics:

![Knoop punt functie-updates van Desktop Analytics](media/feature-updates.png)

In deze weer gave vindt u een overzicht van de *functie* -updates voor apparaten met Windows 10.

Zie [Windows levenscyclus](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)voor meer informatie over service perioden.  

Apparaten in het staaf diagram worden gecategoriseerd op de volgende labels:

#### <a name="in-service"></a>In service

Op apparaten wordt de nieuwste functie-update uitgevoerd voor die versie en dit kanaal.  

#### <a name="near-end-of-service"></a>Bijna einde van service

Op apparaten wordt een functie-update uitgevoerd die binnen 90 dagen na het einde van de service valt.

#### <a name="end-of-service"></a>Einde van service

Op apparaten wordt een functie-update uitgevoerd die na het einde van de service datum ligt. Deze datums zijn specifiek voor Enter prise-en onderwijs versies van Windows. Ze zijn niet van toepassing op Home, Pro, Pro education of Pro for Workstation-edities. Zie het [informatieblad over de levenscyclus van Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) voor meer informatie.

#### <a name="not-measured"></a>Niet gemeten

Het apparaat is niet beoordeeld door Desktop Analytics. Deze status omvat apparaten met Windows 7, Windows 8,1 of Windows 10-apparaten die zijn geregistreerd voor het Windows Insider-programma.

Selecteer de tegel om de trends voor de functie-updates te bekijken. In het gestapelde vlak diagram worden apparaten gecategoriseerd op basis van de functie-update die ze na verloop van tijd hebben geïnstalleerd.

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over desktop Analytics-assets](about-assets.md): apparaten, stuur Programma's en apps  

- [Meer informatie over implementatie plannen](about-deployment-plans.md)  
