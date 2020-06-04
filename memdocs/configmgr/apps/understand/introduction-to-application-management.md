---
title: Inleiding tot app-beheer
titleSuffix: Configuration Manager
description: Ontdek de basis informatie die u nodig hebt voor het beheren en implementeren van toepassingen in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b2fc0dfe37ad51ce1a549545c3eaa716395438d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347105"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Inleiding tot toepassings beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel leert u de basis principes voordat u aan de slag gaat met Configuration Manager-toepassingen.  

> [!TIP]  
> Als u al bekend bent met het beheren van toepassingen in Configuration Manager, kunt u dit artikel overs Laan. Ga naar om een voorbeeld toepassing te maken: [een toepassing maken en implementeren](../get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Wat is een toepassing?

Hoewel *toepassing* of *app* een veelgebruikte term voor het berekenen van toepassingen is, betekent dit in Configuration Manager dat er iets specifiek is. U kunt een toepassing zien als een doos. Dit vak bevat een of meer sets installatie bestanden voor een software pakket (ook wel een *implementatie type*genoemd), plus instructies voor het implementeren van de software.  

Wanneer u de toepassing implementeert op apparaten, bepalen de **vereisten** welk implementatie type Configuration Manager geïnstalleerd op het apparaat.  

U kunt veel meer dingen doen met een toepassing. In deze hand leiding leest u meer over deze dingen. In de volgende secties vindt u enkele concepten die u moet weten voordat u begint te dieper:  

### <a name="deployment-type"></a>Implementatie type

Als de *toepassing* het vak is, is het *implementatie type* de set inhoud in het vak. Een toepassing heeft ten minste één implementatie type nodig, omdat deze bepaalt hoe de app moet worden geïnstalleerd. Gebruik meer dan één implementatie type om verschillende inhoud en een ander installatie programma voor dezelfde toepassing te configureren.

Uw bedrijf heeft bijvoorbeeld een line-of-Business-toepassing met de naam Astoria. De ontwikkel aars van toepassingen bieden de volgende manieren om de app te installeren:

- Windows Installer-pakket voor volledige functionaliteit op Windows 10-apparaten
- Een app-V-pakket voor gebruik in de Terminal server-farm
- Een web-app voor mobiele gebruikers  

U maakt één toepassing voor Astoria in Configuration Manager. De toepassing definieert de meta gegevens op hoog niveau over de app die wordt gebruikt voor alle installatie methoden en platformen. Vervolgens maakt u drie implementatie typen voor de beschik bare installatie methoden en implementeert u de toepassing voor alle gebruikers. Op basis van de vereisten en andere configuraties van de implementatie typen, bepaalt Configuration Manager de juiste methode in elk use-case.

Zie [implementatie typen voor de toepassing maken](../deploy-use/create-applications.md#bkmk_create-dt)voor meer informatie.

### <a name="requirements"></a>Vereisten

In vorige versies van Configuration Manager maakt u een verzameling apparaten waarop een toepassing moet worden geïmplementeerd. Hoewel u nog steeds een verzameling kunt maken, moet u de *vereisten* gebruiken om meer gedetailleerde criteria op te geven voor een toepassings implementatie.

U kunt bijvoorbeeld opgeven dat een toepassing alleen kan worden geïnstalleerd op apparaten met Windows 10. Wanneer u de toepassing implementeert op al uw apparaten, wordt deze alleen geïnstalleerd op apparaten met Windows 10.

Configuration Manager evalueert vereisten om te bepalen of een toepassing en alle implementatie typen ervan worden geïnstalleerd. Vervolgens bepaalt de client het juiste implementatietype waarmee een installatie moet worden geïnstalleerd. De Configuration Manager-client evalueert standaard elke zeven dagen de regels voor vereisten om de naleving te bepalen volgens de client instelling **nieuwe evaluatie voor implementaties plannen**.

Zie vereisten voor toepassingen en [implementatie typen](../deploy-use/create-applications.md#bkmk_dt-require) [maken en implementeren](../get-started/create-and-deploy-an-application.md) voor meer informatie.

### <a name="global-conditions"></a>Globale voorwaarden

Hoewel u vereisten met een specifiek implementatie type in één toepassing gebruikt, kunt u ook *globale voor waarden*maken. Deze voor waarden zijn een bibliotheek met vooraf gedefinieerde vereisten die u kunt gebruiken met alle toepassingen en implementatie typen. Configuration Manager bevat een reeks ingebouwde globale voor waarden, of u kunt uw eigen situatie maken.

Zie [globale voor waarden maken](../deploy-use/create-global-conditions.md)voor meer informatie.

### <a name="simulated-deployment"></a>Gesimuleerde implementatie

Een *gesimuleerde implementatie* evalueert de vereisten, detectie methode en afhankelijkheden voor een toepassing. Een client rapporteert de resultaten zonder de toepassing daad werkelijk te installeren.

Zie [toepassings implementaties simuleren](../deploy-use/simulate-application-deployments.md)voor meer informatie.  

### <a name="deployment-action"></a>Implementatieactie

Een *implementatie actie* geeft aan of u de toepassing die u wilt implementeren, wilt installeren of verwijderen. Niet alle implementatie typen ondersteunen de verwijderings actie.

Zie [toepassingen implementeren](../deploy-use/deploy-applications.md)voor meer informatie.  

### <a name="deployment-purpose"></a>Implementatiedoel

Het *doel* van de implementatie geeft aan of de implementatie-app **vereist** of **beschikbaar**is:  

- De client installeert automatisch een *vereiste* implementatie volgens het schema dat u hebt ingesteld. Als de toepassing niet is verborgen, kan een gebruiker de implementatie status ervan volgen. Ze kunnen ook software Center gebruiken om de toepassing te installeren vóór de deadline.  

- Als u de toepassing implementeert voor een gebruiker die *beschikbaar*is, wordt deze in Software Center weer geven en kan hij deze op aanvraag aanvragen.  

Zie [toepassingen implementeren](../deploy-use/deploy-applications.md)voor meer informatie.  

### <a name="revisions"></a>Revisies

Wanneer u *wijzigingen* aanbrengt in een toepassing of een implementatie type, maakt Configuration Manager een nieuwe versie van de toepassing. Voer de volgende acties uit in de Configuration Manager-console:

- De geschiedenis van elke toepassings revisie weer geven
- De eigenschappen weer geven
- Een vorige versie van een toepassing herstellen
- Een oude versie verwijderen

Zie [toepassingen herzien](../deploy-use/revise-and-supersede-applications.md#application-revisions)voor meer informatie.  

### <a name="detection-method"></a>Detectiemethode

Gebruik *detectie methoden* om te detecteren of een apparaat al een toepassing heeft geïnstalleerd. Als de detectie methode aangeeft dat de toepassing is geïnstalleerd, probeert Configuration Manager deze niet opnieuw te installeren.

Zie Opties voor de [detectie methode voor implementatie typen](../deploy-use/create-applications.md#bkmk_dt-detect)voor meer informatie.

### <a name="dependencies"></a>Afhankelijkheden

*Afhankelijkheden* definiëren een of meer implementatie typen van een andere toepassing die de client moet installeren voordat dit implementatie type wordt geïnstalleerd.

Zie [implementatie type afhankelijkheden](../deploy-use/create-applications.md#bkmk_dt-depend)voor meer informatie.  

### <a name="supersedence"></a>Vervanging

Met Configuration Manager kunt u bestaande toepassingen bijwerken of vervangen door gebruik te maken van een *vervangings* relatie. Wanneer u een toepassing vervangt, kunt u een nieuw implementatie type opgeven om het implementatie type van de vervangen toepassing te vervangen. U kunt ook bepalen of u de vervangen toepassing wilt upgraden of verwijderen voordat de client de vervangende toepassing installeert.

Zie voor meer informatie [Application vervanging](../deploy-use/revise-and-supersede-applications.md#application-supersedence).  

### <a name="user-centric-management"></a>Op de gebruiker gericht beheer

Configuration Manager-toepassingen bieden ondersteuning voor *gebruikers gericht beheer*, waarmee u specifieke gebruikers kunt koppelen aan specifieke apparaten. In plaats van de naam van het apparaat van een gebruiker te onthouden, implementeert u apps voor de gebruiker en het apparaat. Deze functie helpt u ervoor te zorgen dat de belangrijkste apps altijd beschikbaar zijn op elk van de apparaten van de gebruiker. Als een gebruiker een nieuwe computer aanschaft, installeert Configuration Manager automatisch hun apps op het apparaat voordat ze zich aanmelden.

Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.  

### <a name="application-group"></a>Toepassings groep

Met ingang van versie 1906 maakt u een groep toepassingen die u kunt verzenden naar een gebruiker of een apparaat-verzameling als één implementatie. De meta gegevens die u opgeeft over de app-groep worden gezien in Software Center als één entiteit. U kunt de apps in de groep ordenen, zodat de client deze in een specifieke volg orde installeert.

Zie [toepassings groepen maken](../deploy-use/create-app-groups.md)voor meer informatie.

## <a name="what-application-types-can-you-deploy"></a>Welke toepassingstypen kunt u implementeren?

Met Configuration Manager kunt u de volgende typen Apps implementeren:  

- Windows Installer (MSI)  

- Windows-app-pakket en app-bundels (appx, appxbundle, msix, msixbundle)  

- Windows-app-pakket in de Microsoft Store  

- Script installatie programma voor installatie Programma's van derden en script wrappers

- Micro soft app-V v4 en V5  

- macOS  

- Een taken reeks voor de implementatie van een niet-besturings systeem voor complexe apps

Wanneer u apparaten beheert via Configuration Manager [on-premises Apparaatbeheer](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md), kunt u bovendien deze nieuwe app-typen beheren:  

- App-pakket voor Windows Phone (XAP)  

- Windows Phone app-pakket in de Microsoft Store  

- Windows Installer via MDM (MSI)  

- Webtoepassing

## <a name="state-based-applications"></a>Toepassingen op basis van status  

Configuration Manager toepassingen gebruiken op status gebaseerde bewaking. U kunt de laatste status van de toepassings implementatie bijhouden voor gebruikers en apparaten. In deze statusberichten wordt informatie over afzonderlijke apparaten weergegeven. Als u bijvoorbeeld een toepassing implementeert voor een verzameling gebruikers, kunt u de nalevings status van de implementatie en het implementatie doel weer geven in de Configuration Manager-console. Bewaak de implementatie van alle software vanuit de werk ruimte **bewaking** in de Configuration Manager-console. Zie [toepassingen bewaken](../deploy-use/monitor-applications-from-the-console.md)voor meer informatie.  

De Configuration Manager-client evalueert regel matig de toepassings implementaties. Bijvoorbeeld:  

- Een gebruiker verwijdert een geïmplementeerde toepassing. Tijdens de volgende evaluatie cyclus detecteert Configuration Manager dat de app niet aanwezig is. De-client installeert vervolgens automatisch de app.  

- Configuration Manager heeft geen toepassing geïnstalleerd op een apparaat omdat het niet voldeed aan de vereisten. Vervolgens wordt het apparaat gewijzigd en voldoet het aan de vereisten. Configuration Manager detecteert deze wijziging en de client installeert de toepassing.  

U kunt het interval voor nieuwe evaluatie van toepassings implementaties instellen. Gebruik de client instelling **nieuwe evaluatie voor implementaties plannen** in de **software-implementatie** groep. Zie [over client instellingen](../../core/clients/deploy/about-client-settings.md#software-deployment)voor meer informatie.  

## <a name="get-started-creating-an-application"></a>Een toepassing maken  

Als u meteen naar rechts wilt gaan en een toepassing wilt maken, vindt u in het artikel [een toepassing maken en implementeren](../get-started/create-and-deploy-an-application.md) een overzicht.  

Als u bekend bent met de basis principes en gedetailleerde Naslag informatie over alle beschik bare opties zoekt, kunt u beginnen met het [maken van toepassingen](../deploy-use/create-applications.md).  

## <a name="software-center"></a>Software Center  

Software Center is een Windows-toepassing die is geïnstalleerd met de Configuration Manager-client. Gebruik deze voor de volgende acties:  

- Zoeken naar toepassingen die zijn geïmplementeerd op het apparaat of de gebruiker en deze aanvragen
- Software-installaties installeren en plannen
- De installatie status voor toepassingen, software-updates en besturings systemen weer geven
- Instellingen voor beheer op afstand configureren
- Energie beheer instellen

Raadpleeg voor meer informatie de volgende artikelen:  

- [Toepassingsbeheer plannen en configureren](../plan-design/plan-for-and-configure-application-management.md)
- [Software Center plannen](../plan-design/plan-for-software-center.md)
- [Gebruikershandleiding van Software Center](../../core/understand/software-center.md)

> [!Note]  
> Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910. Zie [de Application Catalog verwijderen](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)voor meer informatie.  

## <a name="packages-and-programs"></a>Pakketten en programma's  

Configuration Manager blijft ondersteuning bieden voor pakketten en Program ma's die in eerdere versies van het product werden gebruikt.

Zie [pakketten en Program ma's](../deploy-use/packages-and-programs.md)voor meer informatie.  

## <a name="next-steps"></a>Volgende stappen

Nu u de basis concepten van toepassings beheer in Configuration Manager begrijpt, kunt u door gaan met de volgende artikelen:

- [Een voorbeeld toepassing maken en implementeren](../get-started/create-and-deploy-an-application.md)
- [Toepassingsbeheer plannen en configureren](../plan-design/plan-for-and-configure-application-management.md)
- [Toepassingen maken](../deploy-use/create-applications.md)
