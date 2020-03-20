---
title: Wat is appbeheer in Microsoft Intune?
titleSuffix: ''
description: Hier vindt u meer informatie over de beheermogelijkheden voor client-apps per platform voor Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/05/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 1975a2dc-3a14-4cb9-9afb-e2ba01a1c51b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 98eba2cd2905a70157cfb50299bb9b11a6319fcc
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342332"
---
# <a name="what-is-microsoft-intune-app-management"></a>Wat is Microsoft Intune-appbeheer?


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

U kunt, als IT-beheerder, Microsoft Intune gebruiken om de client-apps te beheren die de werknemers van uw bedrijf gebruiken. Deze functionaliteit is een aanvulling op het beheren van apparaten en beschermen van gegevens. Een van de prioriteiten van een beheerder is om ervoor te zorgen dat eindgebruikers toegang hebben tot de apps die ze nodig hebben voor hun werk. Dit doel kan om de volgende redenen een uitdaging zijn:
- Er is een breed scala aan apparaatplatformen en app-typen.
- U moet apps wellicht op zowel bedrijfsapparaten als de persoonlijke apparaten van gebruikers beheren.
- U moet ervoor zorgen dat uw netwerk en uw gegevens beveiligd blijven.

Verder wilt u misschien apps toewijzen en beheren op apparaten die niet bij Intune zijn geregistreerd.

## <a name="mobile-application-management-mam-basics"></a>Basisinformatie over Mobile Application Management (MAM)

[Intune Mobile Application Management](app-lifecycle.md) verwijst naar de suite met Intune-beheerfuncties waarmee u mobiele apps voor uw gebruikers kunt publiceren, pushen, configureren, beveiligen, controleren en bijwerken.

Met MAM kunt u de gegevens van uw organisatie in een toepassing beheren en beveiligen. Met **MAM zonder registratie** (MAM-WE) kunt u op bijna elk [apparaat](app-management.md#app-management-capabilities-by-platform), inclusief persoonlijke apparaten in BYOD-scenario's (**Bring-Your-Own-Device**), een werk- of schoolgerelateerde app beheren die gevoelige gegevens bevat. Veel productiviteits-apps, zoals Microsoft Office-apps, kunnen worden beheerd met Intune MAM. Bekijk de officiële lijst met de [door Microsoft Intune beveiligde apps](apps-supported-intune-apps.md) die beschikbaar zijn voor openbaar gebruik.

Intune MAM ondersteunt twee configuraties:
- **Intune MDM + MAM**: IT-beheerders kunnen apps alleen met MAM en beleidsregels voor de beveiliging van apps beheren op apparaten die zijn geregistreerd bij Intune Mobile Device Management (MDM). Als klanten apps willen beheren met MDM + MAM, moeten zij de Intune-console Azure Portal op https://portal.azure.com gebruiken.
- **MAM zonder apparaatregistratie**: MAM zonder apparaatregistratie, of MAM-WE, biedt IT-beheerders de mogelijkheid apps te beheren met MAM en beleidsregels voor app-beveiliging op apparaten die niet zijn geregistreerd met Intune MDM. Dit betekent dat apps door Intune kunnen worden beheerd op apparaten die zijn geregistreerd bij externe EMM providers. Als klanten apps willen beheren met MAM-WE, moeten zij de Intune-console in Azure Portal op https://portal.azure.com gebruiken. Apps kunnen ook door Intune worden beheerd op apparaten die zijn geregistreerd bij externe Enterprise Mobility Management-providers of die helemaal niet bij een MDM zijn geregistreerd. Zie [Beslissingen voor de technologie voor het inschakelen van BYOD met Microsoft Enterprise Mobility + Security (EMS)](../fundamentals/byod-technology-decisions.md) voor meer informatie over BYOD en EMS.

## <a name="app-management-capabilities-by-platform"></a>App-beheermogelijkheden per platform

Intune biedt een scala aan mogelijkheden om u te helpen de benodigde apps op de apparaten te krijgen waarop u deze wilt uitvoeren. De volgende tabel bevat een samenvatting van de mogelijkheden voor app-beheer.

|  | Android/Android Enterprise | iOS/iPadOS | macOS | Windows 10 | Windows Phone 8.1 |
|-------------------------------------------------------------------------------------|---------|-----|-------|------------|-------------------|
| Apps toevoegen en aan apparaten en gebruikers toewijzen | Ja | Ja | Ja | Ja | Ja |
| Apps toewijzen aan apparaten die niet zijn geregistreerd met Intune | Ja | Ja | Nee | Nee | Nee |
| Beleidsregels voor app-configuratie gebruiken om het opstartgedrag van apps te beheren | Ja | Ja | Nee | Nee | Nee |
| Beleid gebruiken voor de inrichting van mobiele apps om verlopen apps te vernieuwen | Nee | Ja | Nee | Nee | Nee |
| Bedrijfsgegevens in apps beveiligen met app-beveiligingsbeleid | Ja | Ja | Nee | Nee <sup>1</sup> | Nee |
| Alleen zakelijke gegevens verwijderen uit een geïnstalleerde app (app selectief wissen) | Ja | Ja | Nee | Ja | Ja |
| App-toewijzingen controleren | Ja | Ja | Ja | Ja | Ja |
| Apps die in een app-winkel zijn gekocht via een volumeaankoopprogramma, toewijzen en bijhouden | Nee | Nee | Nee | Ja | Nee |
| Verplichte installatie van apps op apparaten (vereist) <sup>2</sup> | Ja | Ja | Ja | Ja | Ja |
| Optionele installatie op apparaten via de bedrijfsportal (beschikbare installatie) | Ja <sup>3</sup> | Ja | Ja | Ja | Ja |
| Installatiesnelkoppeling naar een app op internet (webkoppeling) | Ja <sup>4</sup> | Ja | Ja | Ja | Ja |
| Interne apps (Line-Of-Business-apps) | Ja | Ja | Ja | Ja | Nee |
| Apps uit een store | Ja | Ja | Nee | Ja | Ja |
| Apps bijwerken | Ja | Ja | Nee | Ja | Ja |

<sup>1</sup> U kunt gebruikmaken van [Windows Information Protection](../protect/windows-information-protection-configure.md) om apps op apparaten met Windows 10 te beveiligen.<br>
<sup>2</sup> Alleen van toepassing op apparaten die worden beheerd door Intune.<br>
<sup>3</sup> Intune ondersteunt beschikbare apps uit beheerde Google Play Store op Android Enterprise-apparaten.<br>
<sup>4</sup> Het is niet mogelijk in Intune om een snelkoppeling naar een app te installeren als een webkoppeling op standaard Android Enterprise-apparaten. Er wordt wel ondersteuning geboden voor webkoppelingen voor [toegewezen Android Enterprise-apparaten voor meerdere apps](../configuration/device-restrictions-android-for-work.md#dedicated-device-settings). 


## <a name="get-started"></a>Aan de slag

U vindt de meeste app-gerelateerde informatie in de workload **Apps** die als volgt toegankelijk is:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecteer **Apps**.

    ![Het workloaddeelvenster Apps](./media/app-management/apps-workload.png)

Het workloadvenster bevat koppelingen voor toegang tot algemene app-informatie en -functionaliteit. 

Boven in het navigatiemenu voor de app-workload vindt u informatie over veelgebruikte apps:
- **Overzicht**: Selecteer deze optie om de tenantnaam, de MDM-instantie, de tenantlocatie, de accountstatus, de app-installatiestatus en de status van het app-beveiligingsbeleid weer te geven.
- **Alle apps**: Selecteer deze optie om een lijst met alle beschikbare apps weer te geven. U kunt via deze pagina aanvullende apps toevoegen. Daarnaast kunt u de status van elke pagina bekijken en voor elke app zien of deze is toegewezen. Zie [Apps toevoegen](apps-add.md) en [Apps toewijzen](apps-deploy.md) voor meer informatie.
- **Apps controleren**
    - **App-licenties**: apps die in de app-stores zijn gekocht via een volume-aankoopprogramma weergeven, toewijzen en bewaken. Zie [iOS-apps die zijn gekocht via het volume-aankoopprogramma (VPP; Volume Purchase Program)](vpp-apps-ios.md) en [Apps die via het volume-aankoopprogramma zijn gekocht in de Microsoft Store voor Bedrijven](windows-store-for-business.md) voor meer informatie.
    - **Gedetecteerde apps**: hier worden apps weergegeven die zijn toegewezen door Intune of op een apparaat zijn geïnstalleerd. Zie [Door Intune gedetecteerde apps](app-discovered-apps.md) voor meer informatie.
    - **Installatiestatus van de app**: hier wordt de status weergegeven van een app-toewijzing die u hebt gemaakt. Zie [App-gegevens en -toewijzingen controleren met Microsoft Intune](apps-monitor.md#device-and-user-status-graphs) voor meer informatie.
    - **Status van de app-beveiliging**: hier wordt de status weergegeven van een app-beveiligingsbeleid voor een gebruiker die u selecteert.
- **Op platform**: Selecteer deze platforms om de beschikbare apps per platform te bekijken.
    - Windows
    - iOS
    - macOS
    - Android
- **Beleid**:
    - **Beleid voor app-beveiliging**: selecteer deze optie om instellingen aan een app te koppelen om de bedrijfsgegevens te beveiligen die in de app worden gebruikt. U kunt bijvoorbeeld de mogelijkheden van een app om met andere apps te communiceren beperken of u kunt vereisen dat de gebruiker een pincode voor toegang tot een bedrijfsapp invoert. Zie [Beleid voor app-beveiliging](app-protection-policies.md) voor meer informatie.
    - **App-configuratiebeleid**: selecteer deze optie om instellingen op te geven die mogelijk vereist zijn wanneer een gebruiker een app uitvoert. Zie [Configuratiebeleid voor apps](app-configuration-policies-use-ios.md), [Configuratiebeleid voor iOS-apps](app-configuration-policies-use-ios.md) en [Configuratiebeleid voor Android-apps](app-configuration-policies-overview.md) voor meer informatie.
    - **Inrichtingsprofielen voor iOS-app**: iOS-apps hebben een inrichtingsprofiel en code die zijn ondertekend met een certificaat. Wanneer het certificaat is verlopen, kan de app niet meer worden uitgevoerd. Intune biedt u de hulpmiddelen om proactief een nieuw beleid voor inrichtingsprofielen toe te wijzen aan apparaten met apps die bijna zijn verlopen. Zie [Inrichtingsprofielen voor iOS-apps](app-provisioning-profile-ios.md) voor meer informatie.
    - **Aanvullende beleidsregels S-modus**: Selecteer deze optie om toe te staan dat er aanvullende toepassingen op uw beheerde S-modusapparaten worden uitgevoerd. Zie [Aanvullend beleid voor de S-modus](apps-win32-s-mode.md) voor meer informatie.
    - **Beleidssets**: Selecteer deze optie om een toewijsbare verzameling apps, beleidsregels en andere door u gemaakte beheerobjecten te maken. Zie [Beleidssets](../fundamentals/policy-sets.md) voor meer informatie.
- **Overige**:   
    - **App selectief wissen**: selecteer deze optie om alleen bedrijfsgegevens van een geselecteerd gebruikersapparaat te verwijderen. Zie [App selectief wissen](apps-selective-wipe.md) voor meer informatie.
    - **App-categorieën**: voor het toevoegen, vastmaken en verwijderen van namen van app-categorieën.
    - **eBooks**: Sommige app stores bieden u de mogelijkheid meerdere licenties te kopen voor apps of boeken die u in uw bedrijf wilt gebruiken. Zie [Apps en boeken met Microsoft Intune beheren die via het Volume Purchase Program zijn gekocht](vpp-apps.md) voor meer informatie.
- **Help en ondersteuning**: problemen oplossen, ondersteuning aanvragen of de status van Intune weergeven. Zie [Problemen oplossen](../fundamentals/help-desk-operators.md) voor meer informatie.

## <a name="additional-information"></a>Aanvullende informatie
De volgende items in de console leveren app-gerelateerde functionaliteit:
- **Microsoft Store voor Bedrijven**: een verbinding met de Microsoft Store voor Bedrijven configureren. Nadat u dit hebt gedaan, kunt u gekochte toepassingen synchroniseren met Intune, deze toewijzen en uw licentiegebruik bijhouden. Zie [Apps die zijn gekocht via het volumeaankoopprogramma in de Microsoft Store voor Bedrijven](windows-store-for-business.md) voor meer informatie.
- **Windows Enterprise-certificaat**: voor het toepassen of weergeven van de status van een certificaat voor ondertekening van programmacode die wordt gebruikt voor het distribueren van LOB-apps naar uw beheerde Windows-apparaten.
- **Windows Symantec-certificaat**: voor het toepassen of weergeven van een Symantec-certificaat voor ondertekening van programmacode die nodig is voor het distribueren van XAP- en WP8.x-appx-bestanden naar Windows 10 Mobile-apparaten.
- **Windows-sleutels voor extern laden**: u kunt een Windows-sleutel voor extern laden toevoegen die kan worden gebruikt om een app rechtstreeks te installeren op apparaten in plaats van de app te publiceren en downloaden vanuit de Windows Store. Zie [Een Windows-app sideloaden](app-sideload-windows.md) voor meer informatie.
- **Apple VPP-tokens**: voor het toepassen en weergeven van uw VPP-licenties (Volume Purchase Program) voor iOS/iPadOS. Zie [iOS-/iPadOS-apps die zijn aangeschaft via een volumeaankoopprogramma](vpp-apps-ios.md) voor meer informatie.
- **Beheerde Google Play**: Beheerde Google Play is de zakelijke App Store van Google en tevens de enige bron van toepassingen voor Android Enterprise. Zie [Beheerde Google Play-apps toevoegen aan Android Enterprise-apparaten met Intune](apps-add-android-for-work.md) voor meer informatie.
- **Huisstijl en aanpassing**: u kunt de bedrijfsportal aanpassen aan de huisstijl van uw bedrijf. Zie [De bedrijfsportal-app configureren](company-portal-app.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- [Een app toevoegen aan Microsoft Intune](apps-add.md)
