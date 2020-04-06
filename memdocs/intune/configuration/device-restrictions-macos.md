---
title: macOS-apparaatinstellingen in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: U kunt instellingen voor macOS-apparaten toevoegen, configureren of maken om functies te beperken, zoals wachtwoordvereisten instellen, het vergrendelingsscherm beheren, ingebouwde apps gebruiken, beperkte of goedgekeurde apps toevoegen, bluetooth-apparaten verwerken, verbinding maken met de cloud voor back-up en opslag, de kioskmodus inschakelen, domeinen toevoegen, en bepalen hoe gebruikers de Safari-webbrowser kunnen gebruiken in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50dd3d245b9a89836e3858d71a7ad124189e0973
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407854"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Met macOS-apparaatinstellingen kunt u functies toestaan of beperken met behulp van Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen die u kunt beheren op macOS-apparaten. Gebruik deze instellingen als onderdeel van de MDM-oplossing (Mobile Device Management) om functies toe te staan of uit te schakelen, wachtwoordregels in te stellen, bepaalde apps toe te staan of te beperken en nog veel meer.

Deze instellingen worden toegevoegd aan een apparaatconfiguratieprofiel in Intune en vervolgens toegewezen aan of geïmplementeerd op uw macOS-apparaten.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een configuratieprofiel voor apparaatbeperkingen](device-restrictions-configure.md).

> [!NOTE]
> Deze instellingen zijn van toepassing op verschillende inschrijvingstypen. Zie [macOS-inschrijving](../enrollment/macos-enroll.md) voor meer informatie over de verschillende inschrijvingstypen.

## <a name="general"></a>Algemeen

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving en geautomatiseerde apparaatinschrijving

- **Definitie opzoeken**: Met **Blokkeren** voorkomt u dat de gebruiker een woord markeert en vervolgens de definitie ervan opzoekt op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de functie Definitie opzoeken toestaat.
- **Dicteren**: **Blokkeren** zorgt ervoor dat gebruikers geen spraakinvoer meer kunnen gebruiken om tekst in te voeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers dicteerinvoer gebruiken.
- **Cacheopslag van inhoud**: Met **Blokkeren** voorkomt u dat inhoud in de cache wordt opgeslagen. Met cacheopslag van inhoud worden app-gegevens, webbrowsergegevens, downloads en meer lokale items op apparaten opgeslagen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem caching van inhoud inschakelt.

  Zie [Cacheopslag van inhoud beheren op een Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (hiermee wordt een andere website geopend) voor meer informatie over cacheopslag van inhoud in macOS.

  Deze functie is van toepassing op:  
  - macOS 10.13 en hoger

- **Software-updates uitstellen**: Met **Inschakelen** kunt u het weergeven van software-updates op apparaten uitstellen, van 0-90 dagen. Deze instelling bepaalt niet wanneer updates wel of niet worden geïnstalleerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem updates op apparaten weergeeft wanneer Apple deze heeft uitgegeven. Als Apple bijvoorbeeld op een bepaalde datum een macOS-update uitbrengt, wordt deze update rond de releasedatum automatisch op apparaten weergegeven. Seed-buildupdates zijn zonder vertraging toegestaan.  

  - **De zichtbaarheid van software-updates vertragen**: Voer een waarde in tussen 0 en 90 dagen. Wanneer de vertraging verloopt, krijgen gebruikers een melding om een update uit te voeren naar de vroegste versie van het besturingssysteem die beschikbaar was toen de vertraging werd geactiveerd.

    Als een macOS-update bijvoorbeeld beschikbaar komt op **1 januari** en **Zichtbaarheid vertragen** is ingesteld op **5 dagen**, wordt de update niet als beschikbare update weergegeven. Op de **zesde dag** na de release komt deze update beschikbaar en kunnen gebruikers deze installeren.

    Deze functie is van toepassing op:  
    - macOS 10.13.4 en hoger

- **Schermopnamen**: Het apparaat moet zijn ingeschreven bij het geautomatiseerde DEP (Device Enrollment Program) van Apple. Met **Blokkeren** kunnen gebruikers geen schermopnamen van de weergave opslaan. Ook wordt het bekijken van externe schermen via de Classroom-app geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat schermopnamen vast te leggen, en de Classroom-app de mogelijkheid biedt om externe schermen weer te geven.

### <a name="settings-apply-to-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving

- **Externe schermobservatie via de Classroom-app**: Met **Uitschakelen** kunnen docenten de Classroom-app niet gebruiken om de schermen van hun studenten te bekijken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem docenten toestaat de schermen van hun leerlingen/studenten te bekijken.

  Als u deze instelling wilt gebruiken, stelt u de instelling **Schermopnamen** in op **Niet geconfigureerd** (schermopnamen zijn toegestaan).

- **Ongevraagde schermobservatie met de app Classroom**: Met **Toestaan** kunnen docenten de schermen van hun studenten bekijken zonder dat deze daar toestemming voor hoeven te geven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem vereist dat docenten de schermen pas kunnen zien als studenten akkoord gaan.

  Als u deze instelling wilt gebruiken, stelt u de instelling **Schermopnamen** in op **Niet geconfigureerd** (schermopnamen zijn toegestaan).

- **Studenten moeten toestemming vragen om de Classroom-les te verlaten**: Met **Vereisen** hebben studenten die zijn ingeschreven bij een niet-beheerde Classroom-cursus, goedkeuring van de docent nodig om de cursus te verlaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem studenten toestaat de cursus te verlaten wanneer ze willen.

- **Docenten kunnen automatisch apparaten of apps vergrendelen in de Classroom-app**: Met **Toestaan** kunnen docenten het apparaat of een app van een student vergrendelen zonder goedkeuring van de student. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem vereist dat docenten het apparaat of de app pas kunnen vergrendelen als studenten akkoord gaan.

- **Studenten kunnen automatisch deelnemen aan een Classroom-les**: Met **Toestaan** kunnen studenten zich bij een les aansluiten zonder dat aan de docent te hoeven vragen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem vereist dat docenten goedkeuring geven voor deelname aan een klas.

## <a name="password"></a>Wachtwoord

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving en geautomatiseerde apparaatinschrijving

- **Wachtwoord**: **Vereisen** dat gebruikers een wachtwoord invoeren om toegang te krijgen tot apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem geen wachtwoord vereist. Er worden ook geen beperkingen afgedwongen, zoals het blokkeren van eenvoudige wachtwoorden of het instellen van een minimumlengte.
  - **Vereist wachtwoordtype**: Voer het vereiste complexiteitsniveau voor het wachtwoord in dat uw organisatie nodig heeft. Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Numeriek**: Het wachtwoord mag alleen uit getallen bestaan, bijvoorbeeld 123456789.
    - **Alfanumeriek**: Dit zijn hoofdletters, kleine letters en numerieke tekens.

    Deze functie is van toepassing op:  
    - macOS 10.10.3 en hoger

  - **Het aantal niet-alfanumerieke tekens in het wachtwoord**: Geef op hoeveel complexe tekens zijn vereist in het wachtwoord, tussen 0 en 4. Een complex teken is een symbool, zoals `?`
  - **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens.
  - **Eenvoudige wachtwoorden**: Sta eenvoudige wachtwoorden toe, zoals `0000` of `1234`.
  - **Maximum aantal minuten na schermvergrendeling voordat wachtwoord is vereist**: Geef op hoe lang de computer inactief moet zijn voordat een wachtwoord vereist is om te ontgrendelen. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**: Voer de tijdsduur in gedurende welke apparaten inactief moeten zijn voordat het scherm automatisch wordt vergrendeld. Voer bijvoorbeeld 5 in om apparaten te vergrendelen nadat deze 5 minuten lang inactief zijn geweest. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Wachtwoordverlooptijd (dagen)** : Geef het aantal dagen tussen 1 en 65535 op waarna het wachtwoord voor het apparaat moet worden gewijzigd. Voer bijvoorbeeld `90` als u wilt dat het wachtwoord na 90 dagen verloopt. Wanneer het wachtwoord is verlopen, wordt gebruikers gevraagd een nieuw wachtwoord te maken. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Wachtwoorden niet opnieuw gebruiken**: Gebruik deze instelling om te voorkomen dat gebruikers eerder gebruikte wachtwoorden hergebruiken. Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld 5 invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

- **Blokkeren dat gebruiker de wachtwoordcode wijzigt**: **Blokkeren** voorkomt dat de wachtwoordcode kan worden gewijzigd, toegevoegd of verwijderd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat wachtwoordcodes worden toegevoegd, gewijzigd of verwijderd.
- **Ontgrendelen met vingerafdruk blokkeren**: Met **Blokkeren** kunnen geen vingerafdrukken worden gebruikt om apparaten te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van een vingerafdruk.

- **Automatisch wachtwoorden invullen blokkeren**: Met **Blokkeren** voorkomt u dat de functie Wachtwoorden automatisch invullen wordt gebruikt in macOS. Als u **Blokkeren** kiest, heeft dat ook de volgende gevolgen:

  - Gebruikers wordt niet meer gevraagd om een wachtwoord te gebruiken dat is opgeslagen in Safari of in een app.
  - Automatische sterke wachtwoorden zijn uitgeschakeld en gebruikers krijgen geen suggesties voor sterke wachtwoorden.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functies toestaat.

- **Aanvragen voor wachtwoordnabijheid blokkeren**: Met **Blokkeren** voorkomt u dat apparaten wachtwoorden van nabijgelegen apparaten aanvragen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze wachtwoordaanvragen toestaat.

- **Wachtwoorden delen blokkeren**: Selecteer **Blokkeren** om te voorkomen dat wachtwoorden via AirDrop tussen apparaten worden gedeeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het delen van wachtwoorden toestaat.

## <a name="built-in-apps"></a>Ingebouwde apps

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving en geautomatiseerde apparaatinschrijving

- **Automatisch invullen in Safari blokkeren**: Met **Blokkeren** wordt de functie Automatisch invullen in Safari op apparaten uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat de instellingen voor automatisch doorvoeren te wijzigen in de webbrowser.
- **Camera blokkeren**: Met **Blokkeren** voorkomt u dat gebruikers toegang hebben tot de camera op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toegang tot de camera van het apparaat toestaan.

  Intune beheert alleen de toegang tot de camera van het apparaat. Het heeft geen toegang tot afbeeldingen of video's.

- **Apple Music blokkeren**: Met **Blokkeren** keert u terug naar de klassieke modus van de app Muziek en wordt de Muziek-service uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app Apple Music toestaat.
- **Zoekresultaten van internet blokkeren in Spotlight**: Met **Blokkeren** zorgt u ervoor dat Spotlight geen resultaten meer retourneert na een zoekopdracht op internet. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat Zoeken met Spotlight verbinding maakt met internet om zoekresultaten op te halen.
- **Bestandsoverdracht via iTunes blokkeren**: Met **Blokkeren** worden services voor het delen van toepassingsbestanden uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem services voor het delen van toepassingsbestanden toestaat.

  Deze functie is van toepassing op:  
  - macOS 10.13 en hoger

## <a name="restricted-apps"></a>Beperkte apps

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving en geautomatiseerde apparaatinschrijving

- **Lijst met typen beperkte apps**: Hiermee maakt u een lijst met apps die gebruikers niet mogen installeren of gebruiken. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat gebruikers toegang hebben tot door u toegewezen apps en ingebouwde apps.
  - **Niet-toegestane apps**: Hiermee maakt u een lijst met apps die niet worden beheerd door Intune en die gebruikers niet mogen installeren en uitvoeren. Gebruikers kunnen geen verboden apps installeren. Als een gebruiker een app uit deze lijst installeert, wordt deze in Intune gerapporteerd.
  - **Goedgekeurde apps**: Hiermee maakt u een lijst met apps die gebruikers mogen installeren. Om te voldoen aan het beleid, mogen gebruikers geen andere apps installeren. Apps die worden beheerd door Intune worden automatisch toegestaan, zoals de bedrijfsportal-app. Er wordt niet voorkomen dat gebruikers een app installeren die niet in de goedgekeurde lijst wordt vermeld. Maar als dat wel het geval is, wordt dit in Intune gerapporteerd.

- **App-bundel-id**: Voer de [App-bundel-id](bundle-ids-built-in-ios-apps.md) van de gewenste app in. U kunt ingebouwde apps en Line-Of-Business-apps weergeven of verbergen. De website van Apple bevat een lijst met [ingebouwde Apple-apps](https://support.apple.com/HT208094).
- **App-naam**: Voer de naam van de gewenste app in. U kunt ingebouwde apps en Line-Of-Business-apps weergeven of verbergen. De website van Apple bevat een lijst met [ingebouwde Apple-apps](https://support.apple.com/HT208094).
- **Uitgever**: Voer de uitgever van de app in.

Als u apps wilt toevoegen aan deze lijsten, kunt u:

- **Toevoegen**: Selecteer deze optie om een lijst met uw apps te maken.
- **Importeer** een CSV-bestand met details van de app, waaronder de URL. Gebruik de notatie `<app bundle ID>, <app name>, <app publisher>`. U kunt ook **Exporteren** om een lijst met apps te maken in dezelfde indeling.

## <a name="connected-devices"></a>Verbonden apparaten

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving en geautomatiseerde apparaatinschrijving

- **AirDrop blokkeren**: Met **Blokkeren** voorkomt u dat gebruikers AirDrop op apparaten gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de functie AirDrop toestaat voor het uitwisselen van inhoud met apparaten in de omgeving.
- **Automatisch ontgrendelen via Apple Watch blokkeren**: Met **Blokkeren** voorkomt u dat gebruikers hun macOS-apparaat ontgrendelen met hun Apple Watch. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers hun macOS-apparaat kunnen ontgrendelen met hun Apple Watch.

## <a name="cloud-and-storage"></a>Cloud en opslag

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving en geautomatiseerde apparaatinschrijving

- **Synchronisatie van iCloud-sleutelhanger blokkeren**: **Blokkeren** schakelt de synchronisatie van aanmeldingsgegevens in de sleutelhanger naar iCloud uit. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze aanmeldingsgegevens synchroniseren.
- **Synchronisatie van clouddocumenten blokkeren**: **Blokkeren**: voorkomt dat documenten en gegevens worden gesynchroniseerd met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het synchroniseren van documenten en sleutelwaarden met uw iCloud-opslagruimte toestaat.
- **Back-up van iCloud-mail blokkeren**: Met **Blokkeren** voorkomt u synchronisatie van de app Mail van macOS met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van Mail met iCloud toestaat.
- **Back-up van iCloud-contactpersonen blokkeren**: Met **Blokkeren** voorkomt u synchronisatie van contactpersonen op het apparaat met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van contactpersonen met iCloud toestaat.
- **Back-up van iCloud-agenda blokkeren**: Met **Blokkeren** voorkomt u synchronisatie van de app Agenda van macOS met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van Agenda met iCloud toestaat.
- **Back-up van iCloud-herinneringen blokkeren**: Met **Blokkeren** voorkomt u synchronisatie van de app Herinneringen van macOS met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van Herinneringen met iCloud toestaat.
- **Back-up van iCloud-bladwijzers blokkeren**: Met **Blokkeren** voorkomt u synchronisatie van bladwijzers op het apparaat met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van de bladwijzers met iCloud toestaat.
- **Back-up van iCloud-notities blokkeren**: Met **Blokkeren** voorkomt u synchronisatie van notities op het apparaat met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van notities met iCloud toestaat.
- **iCloud-fotobibliotheek blokkeren**: Met **Blokkeren** wordt de iCloud-fotobibliotheek uitgeschakeld en wordt voorkomen dat in iCloud de foto’s van het apparaat worden gesynchroniseerd. Foto's die niet volledig uit de iCloud-fotobibliotheek zijn gedownload, worden verwijderd uit de lokale opslag van apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van foto’s toestaat tussen het apparaat en de iCloud-fotobibliotheek.
- **Handoff**: Met deze functie kunnen gebruikers aan het werk gaan op een macOS-apparaat en vervolgens hun werk voortzetten op een ander iOS-/iPadOS- of macOS-apparaat. Met **Blokkeren** wordt voorkomen dat de Handoff-functie werkt op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat op apparaten.

  Deze functie is van toepassing op:  
  - macOS 10.15 of hoger

## <a name="domains"></a>Domains

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving en geautomatiseerde apparaatinschrijving

- **URL voor e-maildomein**: U kunt een of meer URL's **Toevoegen** aan de lijst. Wanneer gebruikers een e-mail ontvangen die afkomstig is van een ander domein dan het domein dat u hebt geconfigureerd, wordt de e-mail in de macOS-app Mail gemarkeerd als niet-vertrouwd.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook apparaatfuncties en -instellingen beperken op [iOS-/iPadOS](device-restrictions-ios.md)-apparaten.
