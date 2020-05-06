---
title: Include-bestand
description: Include-bestand
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183042"
---
Deze mededelingen bevatten belangrijke informatie die u kan helpen om voorbereid te zijn op toekomstige wijzigingen en functies in Intune.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Microsoft Intune-ondersteuning voor Windows 10 Mobile wordt afgeschaft<!--3544938-->
Microsoft-ondersteuning voor Windows 10 Mobile is in december 2019 afgeschaft. Zoals is vermeld in deze verklaring, komen gebruikers van Windows 10 Mobile niet meer in aanmerking voor nieuwe beveiligingspatches, hotfixes anders dan beveiligings, gratis ondersteuningsopties of online technische contentupdates van Microsoft. Op basis van de ondersteuning voor het mobiele besturingssysteem beëindigt Microsoft Intune op 10 augustus 2020 de ondersteuning voor zowel de bedrijfsportal voor de mobiele Windows 10-app als het besturingssysteem van Windows 10 Mobile.

#### <a name="how-does-this-affect-me"></a>Wat betekent dit voor mij?
Als u Windows 10 Mobile-apparaten gebruikt in uw organisatie, kunt u tussen nu en 10 augustus 2020 nieuwe apparaten inschrijven, beleid en apps toevoegen of verwijderen of beheerinstellingen bijwerken. Na 10 augustus zijn geen nieuwe inschrijvingen meer mogelijk en verwijderen we uiteindelijk Windows 10 Mobile-beheer uit de Intune-gebruikersinterface. Apparaten checken niet langer in bij de Intune-service en we verwijderen apparaat- en beleidsgegevens.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Wat moet ik doen om me voor te bereiden op deze wijziging?
Controleer uw Intune-rapporten om na te gaan voor welke apparaten of gebruikers dit gevolgen kan hebben. Ga naar **Apparaten** > **Alle apparaten** en filter op besturingssysteem. U kunt extra kolommen toevoegen, zodat u eenvoudiger kunt vaststellen wie in uw organisatie apparaten met Windows 10 Mobile gebruikt. Vraag uw eindgebruikers hun apparaten te vernieuwen of stop het gebruik van deze apparaten voor zakelijke toegang.


### <a name="end-of-support-for-legacy-pc-management"></a>Einde van ondersteuning voor verouderd pc-beheer

Verouderd pc-beheer wordt vanaf 15 oktober 2020 niet meer ondersteund. Werk apparaten bij naar Windows 10 en registreer deze opnieuw als MDM-apparaten (Mobile Device Management) om ze door Intune te blijven laten beheren.

[Meer informatie](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>Afgenomen ondersteuning voor Android-apparaatbeheerder<!--5857738-->
Android-apparaatbeheerder (soms aangeduid met het verouderde Android-beheer, uitgebracht met Android 2.2) is een manier om Android-apparaten te beheren. Er is nu echter verbeterde beheerfunctionaliteit beschikbaar met [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) (uitgebracht met Android 5.0). In een poging om apparaatbeheer moderner, breder en veiliger te maken, vermindert Google ondersteuning voor apparaatbeheerder in nieuwe Android-versies.

#### <a name="how-does-this-affect-me"></a>Wat betekent dit voor mij?
Deze wijzigingen van Google zijn op de volgende manieren van invloed op Intune-gebruikers:  
- Intune biedt slechts tot het tweede kwartaal van 2020 nog ondersteuning voor Android-apparaten met Android 10 en hoger die door apparaatbeheerder worden beheerd. Apparaten die worden beheerd met apparaatbeheerder en worden uitgevoerd met Android 10 of hoger, kunnen na dit moment niet langer volledig worden beheerd. Betrokken apparaten ontvangen met name geen nieuwe wachtwoordvereisten meer.
    - Samsung Knox-apparaten worden gedurende deze periode niet beïnvloed, omdat uitgebreide ondersteuning wordt geboden via de integratie van Intune met het Knox-platform. Dit geeft u meer tijd om af te stappen van apparaatbeheerder.    
- Android-apparaten die worden beheerd met apparaatbeheerder en worden uitgevoerd met oudere versies dan Android 10, worden niet getroffen en kunnen volledig beheerd blijven worden met apparaatbeheerder.    
- Voor alle apparaten met Android 10 of hoger heeft Google de toegang voor apparaatbeheerderagents als de Bedrijfsportal tot apparaat-id's beperkt. Nadat een apparaat naar Android 10 of hoger is bijgewerkt, heeft deze beperking gevolgen voor de volgende Intune-functies:  
    - Netwerktoegangsbeheer voor VPN werkt niet meer.   
    - Als u apparaten identificeert als 'In bedrijfseigendom' met een IMEI of serienummer, wordt het apparaat niet automatisch gemarkeerd als 'In bedrijfseigendom'.  
    - Het IMEI en serienummers zijn niet langer zichtbaar voor IT-beheerder in Intune. 
        > [!NOTE]
        > Dit heeft alleen gevolgen voor apparaten die worden beheerder met apparaatbeheerder en worden uitgevoerd met Android 10 of hoger en is niet van invloed op apparaten die worden beheerd met Android Enterprise. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Wat moet ik doen om me voor te bereiden op deze wijziging?
Volg de volgende aanbevelingen op om te voorkomen dat u in het derde kwartaal van 2020 te kampen hebt met beperkte functionaliteit:
- Leg geen nieuwe apparaten vast in apparaatbeheerder.
- Als bij een apparaat een update naar Android 10 wordt verwacht, migreert u deze van apparaatbeheerder naar Android Enterprise-beheer en/of app-beveiligingsbeleid.

#### <a name="additional-information"></a>Aanvullende informatie
- [Google-richtlijnen voor migratie van apparaatbeheerder naar Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google-documentatie over het plan om de apparaatbeheerder-API af te schaffen](https://developers.google.com/android/work/device-admin-deprecation)