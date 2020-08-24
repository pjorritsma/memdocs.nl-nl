---
title: Gedetecteerde apps
titleSuffix: Microsoft Intune
description: Meer informatie over de gedetecteerde apps die door Intune op een apparaat zijn gevonden.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 07dd262f-13e7-4cb2-9cc2-b755d1c276cf
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: bed118810be877bf4671571814ee6d151d6f727b
ms.sourcegitcommit: da5bfbe16856fdbfadc40b3797840e0b5110d97d
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512730"
---
# <a name="intune-discovered-apps"></a>Door Intune gedetecteerde apps

In de lijst door Intune **gedetecteerde apps** ziet u de apparaten die bij Intune zijn ingeschreven in uw tenant. De lijst biedt als het ware een software-inventarisatie van uw tenant. **Gedetecteerde apps** is een rapport dat los staat van de rapporten over [app-installaties](apps-monitor.md). Voor persoonlijke apparaten verzamelt Intune nooit informatie over toepassingen die niet worden beheerd. Voor bedrijfsapparaten wordt informatie over alle apps verzameld, of die apps nu worden beheerd of niet. Hieronder staat een tabel waarin het verwachte wordt weergegeven. Over het algemeen wordt het rapport elke zeven dagen vernieuwd vanaf het tijdstip van inschrijving (er is dus geen wekelijkse vernieuwing voor de gehele tenant). De enige uitzondering op deze vernieuwingsperiode heeft te maken met de toepassingsgegevens die worden verzameld via de Intune-beheeruitbreiding voor Win32-apps; deze gegevens worden elke 24 uur verzameld.

## <a name="monitor-discovered-apps-with-intune"></a>Gedetecteerde apps bewaken met Intune

Intune biedt een geaggregeerde lijst met apps die zijn gedetecteerd op de apparaten die in uw tenant bij Intune zijn ingeschreven.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apps** > **Bewaken** > **Gedetecteerde apps**.

>[!NOTE]
>U kunt de lijst met gedetecteerde apps exporteren naar een CSV-bestand. Selecteer hiervoor **Exporteren** in het deelvenster **Gedetecteerde apps**.
>
>Voor gedetecteerde Win32-apps is er momenteel geen totaal aantal. Dit type gegevens kan alleen per apparaat worden weergegeven.

Intune biedt ook een lijst met gedetecteerde apps per afzonderlijk apparaat in uw tenant.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Alle apparaten**.
3. Selecteer een apparaat.
4. Als u gedetecteerde apps voor dit apparaat wilt weergeven, selecteert u **Gedetecteerde apps** in het gedeelte **Monitor**.

## <a name="details-of-discovered-apps"></a>Gegevens van gedetecteerde apps

De volgende lijst bevat de app-platformtypen, de apps die worden bewaakt op persoonlijke apparaten, de apps die worden bewaakt op apparaten die eigendom zijn van het bedrijf en de vernieuwingscyclus. Zie [App-typen in Microsoft Intune](apps-add.md#app-types-in-microsoft-intune) voor meer informatie over de app-typen die door Intune worden ondersteund.

| Platform | Voor apparaten die persoonlijk eigendom zijn | Voor apparaten die bedrijfseigendom zijn | Cyclus vernieuwen |
|------------------------------------------------------------------------|----------------------------------|--------------------------------------------------|---------------------------------------|
| Windows 10 (Win32-apps) OPMERKING: hiervoor is de [Intune-beheeruitbreiding](intune-management-extension.md) vereist op het apparaat | Niet van toepassing | Apps die door MSI op het apparaat zijn geïnstalleerd | Elke 24 uur vanaf het moment dat het apparaat wordt ingeschreven |
| Windows 10 (moderne apps) | Alleen beheerde, moderne apps | Alle moderne apps die op het apparaat zijn geïnstalleerd | Elke zeven dagen vanaf het moment dat het apparaat wordt ingeschreven |
| Windows 8.1 | Alleen beheerde apps | Alleen beheerde apps | Elke zeven dagen vanaf het moment dat het apparaat wordt ingeschreven |
| Windows RT | Alleen beheerde apps | Alleen beheerde apps | Elke zeven dagen vanaf het moment dat het apparaat wordt ingeschreven |
| iOS/iPadOS | Alleen beheerde apps | Alle apps die op het apparaat zijn geïnstalleerd | Elke zeven dagen vanaf het moment dat het apparaat wordt ingeschreven |
| macOS | Alleen beheerde apps | Alle apps die op het apparaat zijn geïnstalleerd | Elke zeven dagen vanaf het moment dat het apparaat wordt ingeschreven |
| Android | Alleen beheerde apps | Alle apps die op het apparaat zijn geïnstalleerd | Elke zeven dagen vanaf het moment dat het apparaat wordt ingeschreven |
| Android Enterprise | Alleen beheerde apps | Alleen apps die in het werkprofiel zijn geïnstalleerd | Elke zeven dagen vanaf het moment dat het apparaat wordt ingeschreven |

> [!NOTE]
> - Op Windows 10-apparaten met co-beheer, zoals weergegeven in de workload [client-apps](https://docs.microsoft.com/mem/configmgr/comanage/workloads#client-apps) in Configuration Manager, wordt momenteel geen app-inventarisatie verzameld met IME (Intune Management Extensie), volgens de bovenstaande planning. Als u dit probleem wilt verhelpen, moet u de workload [client apps](https://docs.microsoft.com/mem/configmgr/comanage/workloads#client-apps) in Configuration Manager overschakelen naar Intune voor de IME, om te worden geïnstalleerd op het apparaat (IME is vereist voor Win32-inventarisatie en PowerShell-implementatie). Opmerking: eventuele wijzigingen in of updates van dit gedrag worden aangekondigd in [In ontwikkeling](../fundamentals/in-development.md) en/of [Nieuwe functies](../fundamentals/whats-new.md).
> - Op macOS-apparaten in persoonlijk eigendom die zijn ingeschreven vóór november 2019 kunnen alle apps die op het apparaat zijn geïnstalleerd in gebruik blijven totdat het apparaat opnieuw wordt inschreven.
> - Volledig beheerde en toegewezen Android Enterprise-apparaten geven geen gedetecteerde apps weer.

Het aantal gedetecteerde apps komt mogelijk niet overeen met de status van het aantal geïnstalleerde apps. Mogelijkheden voor inconsistenties zijn onder andere:

- Een gerichte wijziging in een geïnstalleerde beheerde app kan ervoor zorgen dat het aantal geïnstalleerde apps in het deelvenster Status wordt verminderd. De apps blijven echter vermeld bij de gedetecteerde apps.
- Wanneer u zich richt op meerdere exemplaren van dezelfde app in een tenant, kan een verschil ontstaan in het aantal gedetecteerde apps vanwege mogelijke overlap van gebruikers of apparaten. Via elk exemplaar van de app worden overlappende gebruikers geteld, maar voor de gedetecteerde apps worden dubbele aantallen weergegeven.
- Gedetecteerde apps en de app-status worden op verschillende tijdstippen verzameld, waardoor een verschil kan ontstaan in de aantallen van de app.

## <a name="next-steps"></a>Volgende stappen

- [App-typen in Microsoft Intune](apps-add.md#app-types-in-microsoft-intune)
- [App-gegevens en -toewijzingen controleren met Microsoft Intune](apps-monitor.md)
