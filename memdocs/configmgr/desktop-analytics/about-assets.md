---
title: Assets in Desktop Analytics
titleSuffix: Configuration Manager
description: Meer informatie over apparaten, stuur Programma's en apps in Desktop Analytics.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: f87c4cc1bcbe8039acb5876dc8e26ac597f12e59
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107304"
---
# <a name="assets-in-desktop-analytics"></a>Assets in Desktop Analytics

Nadat apparaten gegevens hebben gerapporteerd aan Desktop Analytics, biedt deze een inventarisatie van de volgende assets:

- Apparaten
- Geïnstalleerde apps  

Selecteer in de Service Portal **assets** in het menu bureau blad Analytics.

## <a name="devices"></a>Apparaten

Op het tabblad **apparaten** vindt u belang rijke informatie over alle apparaten in uw organisatie die u hebt Inge schreven bij Desktop Analytics. U kunt sorteren op een kolom of filter voor bepaalde waarden.

> [!NOTE]  
> Als het dash board niet het aantal apparaten rapporteert dat u verwacht te zien voor uw omgeving, raadpleegt u [problemen met Desktop Analytics oplossen](troubleshooting.md).  

In een implementatie plan is er meer informatie over apparaten. Zie voor meer informatie [fonds beleggingen](about-deployment-plans.md#plan-assets)

## <a name="apps"></a>Apps

Op het tabblad **apps** worden alle geïnstalleerde apps weer gegeven die de service detecteert op uw Windows-apparaten.

Op meer dan 2% van geregistreerde apparaten zijn **interessante** apps geïnstalleerd.

De instelling Details van de **App-versies** is standaard uitgeschakeld. op dit tabblad worden alle versies van apps met dezelfde naam en uitgever gecombineerd.<!-- 5542186 --> Het standaard gedrag helpt bij het verminderen van het totale aantal apps dat u ziet, waardoor u minder inspanningen krijgt om aantekeningen aan de apps te maken. Het aantal apps in de tegel **apps** op de achtergrond is ook gelijk aan deze instelling. In plaats van honderden exemplaren van micro soft Edge te vermelden, is er bijvoorbeeld één exemplaar voor alle versies. U kunt beslissingen voor alle versies eenmaal maken. Als u beslissingen moet nemen over specifieke versies van een app, schakelt u deze instelling in. U kunt deze instelling ook configureren bij het werken met een implementatie plan. Zie [activa plannen](about-deployment-plans.md#plan-assets)voor meer informatie.

Selecteer de app in de lijst en selecteer **bewerken**. Met deze actie worden Details voor de app weer gegeven. Selecteer de vervolg keuzelijst **urgentie** en stel een waarde in. U kunt ook een **eigenaar**toewijzen. Als u wijzigingen aanbrengt, selecteert u **Opslaan**.

Configureer het **belang** van apps door een van de volgende categorieën in te stellen:

- Kritiek
- Belangrijk
- Negeren
- Niet gecontroleerd
- Niet belang rijk<!-- 3587232 -->

Wanneer de instelling Details van de **App-versie** is uitgeschakeld, wordt in het deel venster app-Details het aantal versies en talen van de app weer gegeven dat wordt gecombineerd. Als u wijzigingen in de app-details opslaat, geldt dit voor alle versies. Stel bijvoorbeeld het **belang** of de **eigenaar**in. Bij sommige waarden wordt ' multiple ' weer gegeven, wat betekent dat er niet één consistente waarde in alle versies is.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp"> </a> Beslissing over automatische upgrade van systeem-en Store-apps

<!-- 3587232 -->
Het identificeren van **urgentie** en het **opwaarderen van upgrades** is essentieel voor alle interessantste apps in de Desktop Analytics-werk stroom. Bepaalde typen apps worden automatisch gemarkeerd als *niet belang rijk*om uw inspanningen te verminderen bij het aantekeningen maken op deze apps. De beslissing over de upgrade van het implementatie plan voor deze apps wordt ook gemarkeerd als *gereed*. De volgende apps zijn compatibel en blijven werken na het upgraden van Windows:

- Systeem-apps en-onderdelen die zijn gepubliceerd door micro soft

- Apps die worden beheerd en bijgewerkt via de Microsoft Store

> [!TIP]
> Invoer voor elke app op globaal niveau of per implementatie plan beheren.
>
> 1. Selecteer in de portal voor desktop Analytics in het menu **beheren** de optie **assets**. Selecteer vervolgens **apps**.
>
> 2. Gebruik de kolommen **type** en **categorie** om deze app-categorieën te beheren:
>
>    - Voor Store-apps, filter **type** als **modern**
>    - Voor systeem-apps filter **categorie** als **achtergrond proces** of **Windows-onderdeel**

In een implementatie plan kunt u ook de beslissing van de **upgrade**instellen. Zie [activa plannen](about-deployment-plans.md#plan-assets)voor meer informatie.

### <a name="usage"></a>Gebruik

<!-- 5533890 -->

- **Totale aantal installaties**: deze waarde is het aantal installaties van de geselecteerde app op alle door Desktop Analytics geregistreerde apparaten.

- **Installatie percentage**: deze waarde is het installatie percentage van de geselecteerde app voor het totale aantal Inge schreven Desktop Analytics-apparaten.

- **Apparaten die deze app hebben gestart in de afgelopen 30 dagen**: deze waarde is het aantal apparaten waarbij een gebruiker de geselecteerde app heeft gestart. Het bevat alleen apparaten die het gebruik in de afgelopen 30 dagen hebben gerapporteerd. Dit aantal is op alle apparaten die zijn Inge schreven met Desktop Analytics op elke versie van Windows 10. Het is mogelijk dat dit aantal kan variëren voor een implementatie plan.

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over implementatie plannen voor desktop Analytics](about-deployment-plans.md)  

- [Meer informatie over beveiliging en functie-updates](about-updates.md)  

- [Compatibiliteits evaluatie in Desktop Analytics](compat-assessment.md)  
