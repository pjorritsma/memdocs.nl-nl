---
title: Include-bestand
description: Include-bestand
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 79e2694cfd34f1db8bf11969506ec3d8cbc453d4
ms.sourcegitcommit: 8a9b85d1c879060ea541f7c8ad1ae34a4ed33ed0
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/31/2020
ms.locfileid: "87507653"
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

### <a name="move-to-the-microsoft-endpoint-manager-admin-center-for-all-your-intune-management"></a>Gebruik het Microsoft Endpoint Manager-beheercentrum voor alle Intune-beheertaken
In MC208118 hebben we afgelopen maart een nieuwe, eenvoudige URL geïntroduceerd voor uw Microsoft Endpoint Manager – Intune-beheer: [https://endpoint.microsoft.com](https://endpoint.microsoft.com). Microsoft Endpoint Manager is een uniform platform dat Microsoft Intune en Configuration Manager bevat. **Per 1 augustus 2020** wordt Intune-beheer verwijderd van [https://portal.azure.com](https://portal.azure.com). Het is raadzaam dat u [https://endpoint.microsoft.com](https://endpoint.microsoft.com) voor het beheer van eindpunten gebruikt. 


### <a name="decreasing-support-for-android-device-administrator--7371518--"></a>Afgenomen ondersteuning voor Android-apparaatbeheerder<!--7371518-->
Het beheer door Android-apparaatbeheerders werd in Android 2.2 uitgebracht als een manier om Android-apparaten te beheren. Vervolgens werd, te beginnen met Android 5, het modernere beheerframework van [Android Enterprise](../enrollment/connect-intune-android-enterprise.md) uitgebracht (voor apparaten die op betrouwbare wijze verbinding kunnen maken met Google Mobile Services). Google stimuleert de afschaffing van beheer door apparaatbeheerders door de beheerondersteuning in nieuwe Android-releases te verminderen.

#### <a name="how-does-this-affect-me"></a>Wat betekent dit voor mij?
Door deze veranderingen van Google beschikt u in het vierde kwartaal van 2020 niet meer over uitgebreide beheermogelijkheden op de apparaten die door een apparaatbeheerder worden beheerd. 

> [!NOTE]
> In eerdere communicaties werd het derde kwartaal van 2020 genoemd, maar de datum is verplaatst naar aanleiding van de [meest recente informatie van Google](https://www.blog.google/products/android-enterprise/da-migration/).

##### <a name="device-types-that-will-be-impacted"></a>Apparaattypen die worden beïnvloed
De apparaten die worden beïnvloed door de afgeschafte ondersteuning van apparaatbeheerders zijn de apparaten waarvoor de drie onderstaande voorwaarden gelden:
- Ingeschreven bij beheer door apparaatbeheerder.
- Android 10 of hoger.
- Geen Samsung-apparaat.

Apparaten worden niet beïnvloed als ze een van de volgende zijn:
- Niet ingeschreven bij beheer door apparaatbeheerder.
- Een Android-versie lager dan Android 10.
- Samsung-apparaten. Samsung Knox-apparaten worden gedurende deze periode niet beïnvloed, omdat uitgebreide ondersteuning wordt geboden via de integratie van Intune met het Knox-platform. Dit geeft u extra tijd om de overgang van het beheer door apparaatbeheerders voor Samsung-apparaten te plannen.

##### <a name="settings-that-will-be-impacted"></a>Instellingen die worden beïnvloed
[De verminderde ondersteuning van de apparaatbeheerder van Google](https://developers.google.com/android/work/device-admin-deprecation) voorkomt dat de configuratie van deze instellingen van toepassing is op getroffen apparaten.

###### <a name="configuration-profile-device-restriction-settings"></a>Configuratieprofiel voor beperking van apparaatinstellingen

- **Camera** blokkeren
- **Minimale wachtwoordlengte** instellen
- **Aantal mislukte aanmeldingen voordat het apparaat wordt gewist** instellen (is niet van toepassing op apparaten zonder wachtwoord, maar is van toepassing op apparaten met een wachtwoord)
- **Wachtwoordverlooptijd (dagen)** instellen
- **Vereist wachtwoordtype** instellen
- **Het gebruik van eerdere wachtwoorden voorkomen** instellen
- **Smart Lock en andere trustagenten** blokkeren

###### <a name="compliance-policy-settings"></a>Instellingen voor nalevingsbeleid

- **Vereist wachtwoordtype** instellen
- **Minimale wachtwoordlengte** instellen
- **Het aantal dagen totdat het wachtwoord verloopt** instellen
- **Aantal eerdere wachtwoorden dat niet opnieuw mag worden gebruikt** instellen


![Schermopname van de pagina met het Android-nalevingsbeleid](../fundamentals/media/notices/android-compliance-settings.png)

###### <a name="additional-impacts-based-on-android-os-version"></a>Extra effecten op basis van de Android-besturingssysteemversie

**Android 10**: Voor alle apparaten die door de apparaatbeheerder worden beheerd (inclusief Samsung) met Android 10 en later, heeft Google de mogelijkheid voor apparaatbeheerders om toegang te krijgen tot informatie over de apparaatidentificatie beperkt, zoals de Bedrijfsportal. Nadat een apparaat naar Android 10 of hoger is bijgewerkt, heeft deze beperking gevolgen voor de volgende Intune-functies:
- Netwerktoegangsbeheer voor VPN werkt niet meer
- Als u apparaten identificeert als bedrijfseigendom met een IMEI of serienummer, wordt het apparaat niet automatisch gemarkeerd als In bedrijfseigendom
- Het IMEI en serienummer zijn niet langer zichtbaar voor IT-beheerders in Intune

**Android 11**: Momenteel wordt Android 11-ondersteuning op de nieuwste bètaversie van de ontwikkelaar getest om te evalueren of deze invloed zal hebben op apparaten die door een apparaatbeheerder worden beheerd.

#### <a name="user-experience-of-impacted-settings-on-impacted-devices"></a>Ervaring van gebruikers met beïnvloede instellingen op beïnvloede apparaten

Beïnvloede configuratie-instellingen:
- Voor reeds ingeschreven apparaten waarop de instellingen al is toegepast, zullen de betreffende configuratie-instellingen verder worden afgedwongen.
- Voor nieuw ingeschreven apparaten, nieuw toegewezen instellingen en bijgewerkte instellingen worden de betreffende configuratie-instellingen niet afgedwongen (maar alle andere configuratie-instellingen worden wel afgedwongen).

Beïnvloede compliance-instellingen:
- Voor reeds ingeschreven apparaten waarop de instellingen al is toegepast, zullen de beïnvloede nalevingsinstellingen nog steeds worden weergegeven als redenen voor niet-compatibel op de pagina Apparaatinstellingen bijwerken, zal het apparaat niet meer voldoen aan de vereisten en zullen de vereisten voor het wachtwoord nog steeds worden afgedwongen in de instellingen-app.
- Voor nieuw ingeschreven apparaten, nieuw toegewezen en bijgewerkte instellingen zullen de betreffende nalevingsinstellingen nog steeds worden weergegeven als redenen voor niet-compatibel op de pagina Apparaatinstellingen bijwerken en zal het apparaat niet meer voldoen aan de eisen, maar strengere eisen voor het wachtwoord zullen niet worden afgedwongen in de instellingen-app.

#### <a name="cause-of-impact"></a>Oorzaak van de impact 
Apparaten worden beïnvloed in het vierde kwartaal van 2020. Op dat moment zal de Bedrijfsportal-app worden bijgewerkt, waardoor de API-doelen van de Bedrijfsportal API van niveau 28 naar niveau 29 zullen gaan ([ zoals vereist door Google](https://www.blog.google/products/android-enterprise/da-migration/)). 

Op dat moment zullen apparaten die door een apparaatbeheerder worden beheerd en niet door Samsung zijn gemaakt, worden beïnvloed zodra de gebruiker deze acties heeft voltooid:
- Updates voor Android 10 of hoger.
- Hiermee wordt de Bedrijfsportal-app bijgewerkt naar de versie waarop API-niveau 29 is gericht.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Wat moet ik doen om me voor te bereiden op deze wijziging?
Het volgende wordt aanbevolen om vermindering van de functionaliteit in het vierde kwartaal van 2020 te voorkomen:
- **Nieuwe inschrijvingen**: Onboard nieuwe apparaten in [Android Enterprise](../enrollment/connect-intune-android-enterprise.md)-beheer (indien beschikbaar) en/of [app-beveiligingsbeleid](../apps/app-protection-policies.md). Onboard geen nieuwe apparaten in beheer door een apparaatbeheerder. 
- **Eerder ingeschreven apparaten**: Als op een apparaat dat door de apparaatbeheerder wordt beheerd Android 10 of later wordt uitgevoerd of dit kan worden bijgewerkt naar Android 10 of later (met name als het geen Samsung-apparaat is), moet u het apparaat van apparaatbeheer naar [Android Enterprise](../enrollment/connect-intune-android-enterprise.md)-beheer en/of [app-beveiligingsbeleid](../apps/app-protection-policies.md) verplaatsen. U kunt de gestroomlijnde stroom gebruiken om [Android-apparaten van apparaatbeheerder naar werkprofielbeheer te verplaatsen](../enrollment/android-move-device-admin-work-profile.md).

#### <a name="additional-information"></a>Aanvullende informatie
- [Android-apparaten verplaatsen van beheer door apparaatbeheerder naar werkprofielbeheer](../enrollment/android-move-device-admin-work-profile.md)
- [Inschrijving van apparaten met een Android Enterprise-werkprofiel instellen](../enrollment/android-work-profile-enroll.md)
- [Inschrijving van toegewezen Android Enterprise-apparaten instellen](../enrollment/android-kiosk-enroll.md)
- [Inschrijving van volledig beheerde Android Enterprise-apparaten instellen](../enrollment/android-fully-managed-enroll.md)
- [App-beveiligingsbeleid maken en toewijzen](../apps/app-protection-policies.md)
- [Intune gebruiken in omgevingen zonder Google Mobile Services](../apps/manage-without-gms.md)
- [Inzicht in toepassingsbeveiligingsbeleid en werkprofielen op Android Enterprise-apparaten](../apps/android-deployment-scenarios-app-protection-work-profiles.md)
- [Google's blog over wat u moet weten over de afschaffing van apparaatbeheer](https://www.blog.google/products/android-enterprise/da-migration/)
- [Google-richtlijnen voor migratie van apparaatbeheerder naar Android Enterprise](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Google-documentatie over het plan om de apparaatbeheerder-API af te schaffen](https://developers.google.com/android/work/device-admin-deprecation)


### <a name="plan-for-change-intune-enrollment-flow-update-for-apples-automated-device-enrollment-for-iosipados"></a>Geplande wijziging: Intune-inschrijvingsstroom bijwerken voor geautomatiseerde apparaatinschrijving voor iOS/iPadOS van Apple
In de juli-editie van Bedrijfsportal wordt de iOS/iPadOS-inschrijvingsstroom voor de geautomatiseerde apparaatinschrijving (voorheen bekend als DEP) van Apple gewijzigd. De wijziging van de inschrijvingsstroom vindt alleen plaats tijdens de stroom Inschrijven met gebruikersaffiniteit. Voorheen, als u de optie Bedrijfsportal installeren had ingesteld op Nee als onderdeel van uw configuratie, konden gebruikers nog steeds de Bedrijfsportal-app installeren vanuit de store, wat vervolgens de inschrijving zou activeren waarbij de gebruiker het bijbehorende serienummer konden invoeren. In de aankomende versie van Bedrijfsportal is het bevestigingsscherm voor het serienummer verwijderd. In plaats daarvan moet u een overeenkomend app-configuratiebeleid maken dat naast Bedrijfsportal wordt verzonden om ervoor te zorgen dat gebruikers kunnen worden ingeschreven. U kunt ook Bedrijfsportal installeren instellen op Ja als onderdeel van uw configuratie. 
 - Zie de post [hier](https://techcommunity.microsoft.com/t5/intune-customer-success/intune-enrollment-flow-update-for-apple-s-automated-device/ba-p/1431629) voor meer informatie.
