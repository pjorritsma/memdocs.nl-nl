---
title: Intune gebruiken in omgevingen zonder Google Mobile Services
titleSuffix: Microsoft Intune
description: Leer hoe u Intune gebruikt in omgevingen zonder Google Mobile Services.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5aa91a84b2fe5d8870afc93022ab5a468b30e0db
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074789"
---
# <a name="how-to-use-intune-in-environments-without-google-mobile-services"></a>Intune gebruiken in omgevingen zonder Google Mobile Services

Microsoft Intune gebruikt GMS (Google Mobile Services) om te communiceren met de Microsoft Intune-bedrijfsportal bij het beheren van Android-apparaten. In sommige gevallen hebben apparaten mogelijk tijdelijk of permanent geen toegang tot GMS. Een apparaat kan bijvoorbeeld worden verzonden zonder GMS, of het apparaat maakt misschien verbinding met een gesloten netwerk waar GMS niet beschikbaar is. Dit document biedt een overzicht van de verschillen en beperkingen die u kunt waarnemen wanneer u Intune installeert en gebruikt om Android-apparaten te beheren zonder GMS.

## <a name="install-the-intune-company-portal-app-without-access-to-the-google-play-store"></a>De Intune-bedrijfsportal-app installeren zonder toegang tot de Google Play Store 

### <a name="for-users-outside-of-mainland-china"></a>Voor gebruikers buiten het vasteland van China 

Als Google Play niet beschikbaar is, kan de  [Microsoft Intune-bedrijfsportal voor Android](https://www.microsoft.com/en-us/download/details.aspx?id=49140) worden gedownload op Android-apparaten en kan de app worden gesideload. Wanneer de app op deze manier is geïnstalleerd, worden er niet automatisch updates en fixes in geïnstalleerd. Zorg er daarom voor dat u regelmatig handmatig updates en patches voor de app installeert. 

### <a name="for-users-in-mainland-china"></a>Voor gebruikers op het vasteland van China 

Omdat de Google Play Store momenteel niet beschikbaar is op het vasteland van China, kunnen Android-apparaten apps alleen verkrijgen via Chinese app-marktplaatsen. Raadpleeg [De bedrijfsportal-app installeren op het vasteland van China](../user-help/install-company-portal-android-china.md) voor meer informatie.

## <a name="limitations-of-intune-device-administrator-management-when-gms-is-unavailable"></a>Beperkingen van het Intune-beheer van apparaatbeheerders als GMS niet beschikbaar is 

### <a name="unavailable-intune-features"></a>Niet-beschikbare Intune-functies

Sommige Intune-functies zijn afhankelijk van onderdelen van GMS, zoals de Google Play Store of Google Play Services. Omdat deze onderdelen niet beschikbaar zijn in omgevingen zonder GMS, zijn de volgende functies in de Intune-beheerconsole mogelijk niet beschikbaar.  

| Scenario  | Functies  |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Nalevingsbeleid voor apparaten  | Wanneer u nalevingsbeleid voor Android-apparaatbeheer maakt of bewerkt, zijn de opties die worden vermeld onder **Google Play Protect**, niet beschikbaar.  |
| App-beveiligingsbeleid (voorwaardelijk starten)  | De apparaatvoorwaarden **SafetyNet-apparaatbevestiging** en **Bedreigingsscans voor apps vereisen** kunnen niet worden gebruikt voor voorwaardelijk starten.  |
| Client-apps  | Apps van het type **Android** zijn niet beschikbaar. Gebruik in plaats hiervan **Line-Of-Business-app** om apps te implementeren en te beheren.  |
| Mobile Threat Defense  | Werk samen met uw MTD-leverancier om te begrijpen of hun oplossing is geïntegreerd met Intune, of deze beschikbaar is in de desbetreffende regio, en of deze afhankelijk is van GMS.  |

### <a name="some-tasks-may-be-delayed"></a>Sommige taken hebben mogelijk vertraging 

In omgevingen waar GMS beschikbaar is, is Intune afhankelijk van pushmeldingen om taken sneller te voltooien. Als u bijvoorbeeld probeert het apparaat op afstand te wissen, bereiken meldingen doorgaans binnen enkele seconden het apparaat. In situaties waarin GMS niet beschikbaar is, zijn pushmeldingen mogelijk ook niet beschikbaar. Daarom moet Intune wachten op de volgende keer dat het apparaat wordt ingecheckt om de taken te voltooien.  

Ingeschreven Android-apparaten rapporteren elke 8 uur aan Intune. Als een apparaat bijvoorbeeld om 13:00 rapporteert aan Intune, en de externe taken om 13:05 worden uitgegeven, neemt Intune om 21:00 contact op met het apparaat om de taken te voltooien. 

Het voltooien van de volgende taken kan maximaal 8 uur duren: 

**Intune-console**:
- Volledig wissen
- Selectief wissen
- Nieuwe of bijgewerkte app-implementaties
- Vergrendelen op afstand
- Wachtwoordcode opnieuw instellen

**Intune bedrijfsportal-app voor Android**:
- Extern apparaat verwijderen
- Apparaat opnieuw instellen
- Installatie van beschikbare line-of-business-apps

**Intune-bedrijfsportalwebsite**:
- Apparaat verwijderen (lokaal en extern)
- Apparaat opnieuw instellen
- Wachtwoordcode van apparaat opnieuw instellen

Als het apparaat onlangs is ingeschreven, wordt het inchecken voor naleving, niet-naleving en configuratie vaker uitgevoerd. Zie [Algemene vragen, problemen en oplossingen met apparaatbeleid en -profielen in Microsoft Intune](../configuration/device-profile-troubleshoot.md) voor meer informatie over check-ins van apparaten. 

## <a name="next-steps"></a>Volgende stappen

- [Apps toewijzen aan groepen met Microsoft Intune](../apps/apps-deploy.md)
