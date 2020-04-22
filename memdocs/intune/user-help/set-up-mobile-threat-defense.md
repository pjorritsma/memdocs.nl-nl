---
title: Mobile Threat Defense installeren op uw mobiele apparaat
description: Lees hoe u Mobile Threat Defense installeert op uw mobiele apparaat.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/25/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: b5df63a14f27b657c585eb43e09b02368d969939
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084401"
---
# <a name="install-mobile-threat-defense"></a>Mobile Threat Defense installeren   

Als onderdeel van de beveiligingsvereisten van uw organisatie moet u mogelijk een MTD-app (Mobile Threat Defense) van een leverancier installeren. Dit type app detecteert bedreigingen op uw apparaat, zoals verdachte apps, netwerken of beveiligingsproblemen van besturingssystemen, en waarschuwt u.  

Als u niet over de vereiste MTD-app beschikt, kunt u zich niet via uw werk- of schoolaccount aanmelden bij beveiligde apps. In dit artikel leert u [hoe u een MTD-app installeert](set-up-mobile-threat-defense.md#install-app) om de blokkering op te heffen.  

Er zijn diverse MTD-apps beschikbaar die u kunt installeren. Uw organisatie laat u weten welke app u moet gebruiken. 


## <a name="information-your-organization-can-see"></a>Informatie die uw organisatie kan zien   

Uw organisatie kan geen gegevens in uw persoonlijke apps bekijken, zoals teksten, e-mails en afbeeldingen. De MTD-app rapporteert wel informatie over uw apps aan uw organisatie, zoals de naam en versie van de app. Welke informatie daadwerkelijk wordt gerapporteerd, is afhankelijk van de MTD-leverancier van uw bedrijf. Uw organisatie kan het volgende zien:   

* App-naam  
* App-id: De unieke naam waarmee de app wordt geïdentificeerd in Google Play.  
* Appversie en verkort versienummer: De specifieke releasenummers van een app.  
* App-bundel en dynamische grootte: De hoeveelheid ruimte die een app op uw apparaat gebruikt. 


## <a name="install-app"></a>App installeren    
Wanneer u zich aanmeldt bij een beveiligde app, wordt u automatisch gevraagd om een MTD-app te installeren. Volg de stappen op het scherm om de installatie te voltooien. Gebruik de stappen in dit gedeelte voor aanvullende ondersteuning.  
 
Mogelijk wordt u ook gevraagd uw apparaat te registreren. Registratie is noodzakelijk om uw identiteit te controleren en om uw school- of werkaccount aan uw apparaat te koppelen. Als u niet bent geregistreerd, wordt u automatisch door het registratieproces geleid voordat u de MTD-app installeert. Zodra het scherm **Toegang krijgen** verschijnt, kunt u de installatiestappen starten.  

Zie [Uw persoonlijke apparaat registreren op het netwerk van uw organisatie](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network) voor meer informatie over apparaatregistratie.  

### <a name="ios-setup"></a>Installeren in iOS  

1. Volg de instructies in het scherm **Toegang krijgen** om de MTD-app te installeren die uw organisatie nodig heeft.   
2. Ga terug naar het scherm **Toegang krijgen** en selecteer **Openen**.  
3. De MTD-app vraagt toestemming om Microsoft Authenticator te openen. Selecteer **Openen**. 
4. Selecteer uw werkaccount om u aan te melden. 
5. Wacht totdat de MTD-app uw apparaat op beveiligingsrisico's heeft gescand. 
6. Keer terug naar de school- of werk-app die u probeerde te openen. Het is mogelijk dat uw organisatie u nu vraagt om andere vereisten voor app-beveiliging te configureren, bijvoorbeeld om een pincode in te stellen.   
7. U hebt nu toegang tot de app. Als u nog steeds bent geblokkeerd:  
    * Selecteer in het scherm **Toegang krijgen** de optie **Opnieuw controleren**.  
    * Ga naar de MTD-app en controleer op bestaande bedreigingen. Voer de aanbevolen stappen uit om de dreiging af te wenden en weer toegang te krijgen.    

### <a name="android-setup"></a>Android-configuratie 

1. Volg de instructies in het scherm **Toegang krijgen** om de MTD-app te installeren die uw organisatie nodig heeft.  
2. Ga terug naar het scherm **Toegang krijgen** en selecteer **Openen**.  
3. De MTD-app vraagt uw toestemming voor toegang tot bepaalde gebieden van uw apparaat, indien nodig. Voor een goede werking van deze app moet u toegang tot uw contacten **Toestaan**. Welke machtigingen worden aangevraagd, kan per MTD-leverancier verschillen.  
4. Selecteer uw werkaccount om u aan te melden.  
5. Wacht totdat de MTD-app uw apparaat op beveiligingsrisico's heeft gescand.  
6. Keer terug naar de school- of werk-app die u probeerde te openen. Het is mogelijk dat uw organisatie u nu vraagt om andere vereisten voor app-beveiliging te configureren, bijvoorbeeld om een pincode in te stellen.  
7. U hebt nu toegang tot de app. Als u nog steeds bent geblokkeerd:  
    * Selecteer in het scherm **Toegang krijgen** de optie **Opnieuw controleren**.  
    * Ga naar de MTD-app en controleer op bestaande bedreigingen. Voer de aanbevolen stappen uit om de dreiging af te wenden en weer toegang te krijgen.  

### <a name="installation-failed"></a>De installatie is mislukt  

Als de installatie mislukt, neemt u contact op met uw IT-ondersteuningsmedewerker. [Ga naar de website van de bedrijfsportal](https://go.microsoft.com/fwlink/?linkid=2010980) om de contactgegevens van uw organisatie op te zoeken.  

U kunt ook uw app-logboeken naar uw IT-ondersteuningsmedewerker sturen om deze meer context over de installatie te geven.  
* Android-gebruikers: [Uw logboeken uploaden en e-mailen](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android) vanuit de bedrijfsportal.   

* Gebruikers van iOS-apparaten: U kunt [uw logboeken ophalen en verzenden](https://docs.microsoft.com/intune/apps/manage-microsoft-edge#use-microsoft-edge-to-access-managed-app-logs) vanuit Microsoft Edge voor iOS.  

## <a name="resolve-a-threat"></a>Een bedreiging oplossen  
Als een bedreiging het gedefinieerde dreigingsniveau van uw organisatie overschrijdt, kan uw organisatie het volgende doen:  
   
* Toegang blokkeren: U kunt geen gebruik van de beveiligde apps van uw organisatie maken als u bent aangemeld met uw werk- of schoolaccount.  
* Gegevens wissen: Uw school- of werkgegevens worden uit een of meer beveiligde apps van uw organisatie verwijderd.  

Als u een bedreiging wilt afwenden en opnieuw toegang wilt krijgen, opent u de MTD-app op uw apparaat. Lees de verstrekte informatie, zodat u weet welke impact de dreiging op uw apparaat kan hebben en hoe u de dreiging kunt afwenden. Nadat u de stappen hebt gevolgd om de dreiging af te wenden, gaat u terug naar de MTD-app en start u een nieuwe scan. Het kan een paar minuten duren voordat u weer toegang hebt tot uw organisatie.  

## <a name="next-steps"></a>Volgende stappen  

Nog hulp nodig? Neem contact op met het ondersteuningsteam van uw bedrijf. Controleer of de contactgegevens beschikbaar zijn op de [bedrijfsportalwebsite](https://go.microsoft.com/fwlink/?linkid=2010980).

