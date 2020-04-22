---
title: Hoe uw iOS-/iPadOS-gebruikers hun apps downloaden
description: Manieren om iOS-/iPadOS-apps beschikbaar te stellen voor eindgebruikers
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "79344087"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>Hoe uw iOS-/iPadOS-gebruikers hun apps downloaden

Gebruik deze informatie om te begrijpen hoe en waar uw eindgebruikers de apps downloaden die u distribueert via Microsoft Intune.

**Vereiste apps**: apps die door de beheerder worden vereist en die op het apparaat worden geïnstalleerd met minimale tussenkomst van de gebruiker, afhankelijk van het platform.

**Beschikbare apps**: apps die zijn opgegeven in de lijst van de bedrijfsportal-app en die een gebruiker optioneel kan installeren.

**Beheerde apps** zijn apps die kunnen worden beheerd via beleid en die zijn 'verpakt' door Intune of zijn gebouwd met de Intune App Software Development Kit (SDK). Deze apps kunnen worden beheerd door Intune en hierop kan app-beveiligingsbeleid worden toegepast.

**Niet-beheerde apps**: apps die gebruikers kunnen downloaden uit de iOS/iPadOS App Store die niet zijn geïntegreerd met de Intune App SDK. Intune heeft geen controle over de distributie, het beheer of het selectief wissen van deze apps.  

Geregistreerde gebruikers krijgen hun apps door te tikken op de volgende tegels op het scherm Apps van de bedrijfsportal-app:

- **Alle apps** verwijst naar een lijst met alle apps op het tabblad ALLE van de [bedrijfsportalwebsite](https://portal.manage.microsoft.com).

- Gebruikers gaan met **Aanbevolen apps** naar het tabblad AANBEVOLEN van de bedrijfsportalwebsite.

- **Categorieën** verwijst naar het tabblad CATEGORIEËN van de bedrijfsportalwebsite.

![Scherm iOS-bedrijfsportal-apps](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

Zie [Apps toevoegen aan Microsoft Intune](../apps/apps-add.md) voor informatie over het toevoegen van apps.

## <a name="app-management-takeover"></a>Overname van app-beheer
Als er al een app is geïnstalleerd op het apparaat van een eindgebruiker, wordt in het iOS/iPadOS-apparaat een waarschuwing weergegeven om beheer van de app door uw organisatie toe te staan. De eindgebruiker moet de organisatie toestaan om beheer van de app over te nemen voordat de app-configuraties kunnen worden toegepast op een beheerd apparaat. Als de gebruiker de waarschuwing annuleert, wordt de waarschuwing regelmatig weergegeven zolang het apparaat wordt beheerd en de app is toegewezen.  


![Afbeelding van de waarschuwing met betrekking tot het wijzigen van app-beheer, met opties voor annuleren en beheren.](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>Zie ook  

[Hoe uw Android-gebruikers apps downloaden](end-user-apps-android.md)

[Hoe uw Windows-gebruikers apps downloaden](end-user-apps-windows.md)
