---
title: Welke gegevens kan uw bedrijf zien wanneer u uw apparaat inschrijft?
description: Verklaart wat de IT-afdeling wel en niet kan zien op uw beheerde apparaat.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/11/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: bc3ff7b10d3b0ae5779db26fae711bc335c8ec62
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461671"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>Welke gegevens kan mijn organisatie zien wanneer ik mijn apparaat inschrijf?

Uw organisatie kan uw persoonlijke gegevens niet zien wanneer u een apparaat met Microsoft Intune inschrijft. Wanneer u een apparaat inschrijft, geeft u uw organisatie toestemming om bepaalde soorten informatie op uw apparaat weer te geven, zoals het apparaatmodel en serienummer. Uw organisatie gebruikt deze informatie om de zakelijke gegevens op het apparaat te beveiligen.

**Wat uw organisatie nooit kan zien:**

- Oproepen en browsegeschiedenis
- E-mail- en sms-berichten
- Contactpersonen
- Kalender
- Wachtwoorden
- Foto's, met inbegrip van wat er in de app Foto's of het camera-album staat
- Bestanden
- Voor apparaten in bedrijfseigendom met een werkprofiel, de toepassingen en gegevens in uw persoonlijke profiel. 

**Wat uw organisatie altijd kan zien:**

- Apparaatmodel, zoals Google Pixel
- Apparaatfabrikant, zoals Microsoft
- Besturingssysteem en versie, zoals iOS 12.0.1
- Inventaris en namen van apps, zoals Microsoft Word. op persoonlijke apparaten kan uw organisatie alleen uw beheerde apps zien. Wat betreft volledig beheerde en toegewezen apparaten in bedrijfseigendom kan uw organisatie uw gehele app-inventaris zien. Wat betreft apparaten in bedrijfseigendom met een werkprofiel kan uw organisatie alleen de app-inventaris in uw werkprofiel zien.
- Eigenaar van het apparaat
- Apparaatnaam
- Serienummer van apparaat
- IMEI

 > [!NOTE]
 > Voor volledig beheerde en toegewezen Android Enterprise-apparaten kunt u niet de hele app-inventaris weergeven.
 
 > [!NOTE]
 > Een app wordt beschouwd als **beheerde app** wanneer deze op een van de volgende manieren wordt geïnstalleerd:
 > 1. Een gebruiker installeert de app via de bedrijfsportal-app nadat de app door een Intune-beheerder als **beschikbaar** is gepubliceerd.
 > 2. De app is door een Intune-beheerder als **vereist** gepubliceerd en is geïnstalleerd op het apparaat. 
 >
 > Zie [De mogelijkheden van niet-beheerde apps, beheerde apps en MAM-apps](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164) als u een IT-beheerder of ondersteuningsmedewerker in uw organisatie bent en meer informatie wilt over app-beheer in Intune.
    
**Wat uw organisatie mogelijk kan zien:**

- Telefoonnummer: Op apparaten die eigendom zijn van de organisatie is uw volledige telefoonnummer zichtbaar. Voor persoonlijke apparaten zijn alleen de laatste vier cijfers van uw telefoonnummer zichtbaar voor uw organisatie. U kunt het eigendomstype van elk afzonderlijk apparaat zien op de pagina **Apparaatdetails** van dat apparaat.
- Apparaatopslagruimte: als u een vereiste app niet kunt installeren, kan uw organisatie kijken naar de opslagruimte van het apparaat om te controleren of er wellicht te weinig ruimte is.  
- Locatie: Op apparaten in bedrijfseigendom kan uw organisatie de locatie van een zoekgeraakt apparaat bekijken. Voor persoonlijke apparaten kan uw organisatie de locatie van het apparaat nooit bekijken, tenzij wordt geprobeerd om een zoekgeraakt iOS-apparaat onder supervisie op te sporen. Raadpleeg de [Apple iOS-documentatie](https://go.microsoft.com/fwlink/?linkid=853816) voor meer informatie over apparaten onder supervisie.  
- Details app-inventaris: als uw organisatie gebruikmaakt van Mobile Threat Defense, kunnen er details worden weergegeven over de apps die op uw iOS-apparaat zijn geïnstalleerd. Meer informatie over [Mobile Threat Defense](set-up-mobile-threat-defense.md). Op persoonlijke apparaten kan uw organisatie alleen uw beheerde apps zien. Voor apparaten in bedrijfseigendom kan uw organisatie al uw apps zien.
- Netwerkgegevens: bepaalde informatie over netwerkverbindingen voor Android-apparaten kan voor de ondersteuning van uw organisatie beschikbaar zijn. Als uw organisatie bijvoorbeeld vereist dat apparaten binnen een bepaald gebouw blijven, herkent uw apparaat het netwerk waarmee het is verbonden. 
