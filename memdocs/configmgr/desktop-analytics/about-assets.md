---
title: Assets in Desktop Analytics
titleSuffix: Configuration Manager
description: Meer informatie over apparaten, stuur Programma's en apps in Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722548"
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

Configureer het **belang** van apps door een van de volgende categorieën in te stellen:

- Kritiek
- Belangrijk
- Negeren
- Niet gecontroleerd
- Niet belang rijk<!-- 3587232 -->

Selecteer de app in de lijst en selecteer **bewerken**. Met deze actie worden Details voor de app weer gegeven. Selecteer de vervolg keuzelijst **urgentie** en stel een waarde in. U kunt ook een **eigenaar**toewijzen. Als u wijzigingen aanbrengt, selecteert u **Opslaan**.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" />Beslissing over automatische upgrade van systeem-en Store-apps

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

In een implementatie plan kunt u ook de beslissing van de **upgrade**instellen. Zie voor meer informatie [fonds beleggingen](about-deployment-plans.md#plan-assets)

### <a name="usage"></a>Gebruik

<!-- 5533890 -->

- **Totale aantal installaties**: deze waarde is het aantal installaties van de geselecteerde app op alle door Desktop Analytics geregistreerde apparaten.

- **Installatie percentage**: deze waarde is het installatie percentage van de geselecteerde app voor het totale aantal Inge schreven Desktop Analytics-apparaten.

- **Apparaten die deze app hebben gestart in de afgelopen 30 dagen**: deze waarde is het aantal apparaten waarbij een gebruiker de geselecteerde app heeft gestart. Het bevat alleen apparaten die het gebruik in de afgelopen 30 dagen hebben gerapporteerd. Dit aantal is op alle apparaten die zijn Inge schreven met Desktop Analytics op elke versie van Windows 10. Het is mogelijk dat dit aantal kan variëren voor een implementatie plan.

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over implementatie plannen voor desktop Analytics](about-deployment-plans.md)  

- [Meer informatie over beveiliging en functie-updates](about-updates.md)  

- [Compatibiliteits evaluatie in Desktop Analytics](compat-assessment.md)  
