---
title: macOS-apparaatinstellingen in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: U kunt instellingen voor macOS-apparaten toevoegen, configureren of maken om functies te beperken, zoals wachtwoordvereisten instellen, het vergrendelingsscherm beheren, ingebouwde apps gebruiken, beperkte of goedgekeurde apps toevoegen, bluetooth-apparaten verwerken, verbinding maken met de cloud voor back-up en opslag, de kioskmodus inschakelen, domeinen toevoegen, en bepalen hoe gebruikers de Safari-webbrowser kunnen gebruiken in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: kakyker; annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e48ba131d97e68570f1d6cb85b285ddc3198971c
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429752"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>Met macOS-apparaatinstellingen kunt u functies toestaan of beperken met behulp van Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen die u kunt beheren op macOS-apparaten. Gebruik deze instellingen als onderdeel van de MDM-oplossing (Mobile Device Management) om functies toe te staan of uit te schakelen, wachtwoordregels in te stellen, bepaalde apps toe te staan of te beperken en nog veel meer.

Deze instellingen worden toegevoegd aan een apparaatconfiguratieprofiel in Intune en vervolgens toegewezen aan of geïmplementeerd op uw macOS-apparaten.

> [!NOTE]
> De gebruikersinterface komt mogelijk niet overeen met de inschrijvingstypen in dit artikel. De informatie in dit artikel is juist. De gebruikersinterface wordt bijgewerkt in een aanstaande release.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een configuratieprofiel voor beperkingen op macOS-apparaten](device-restrictions-configure.md).

> [!NOTE]
> Deze instellingen zijn van toepassing op verschillende inschrijvingstypen. Zie [macOS-inschrijving](../enrollment/macos-enroll.md) voor meer informatie over de verschillende inschrijvingstypen.

## <a name="built-in-apps"></a>Ingebouwde apps

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Automatisch invullen in Safari blokkeren**: Met **Ja** wordt de functie Automatisch invullen in Safari op apparaten uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat de instellingen voor automatisch doorvoeren te wijzigen in de webbrowser.
- **Gebruik van camera blokkeren**: Met **Ja** voorkomt u dat gebruikers toegang hebben tot de camera op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toegang tot de camera van het apparaat toestaan.

  Intune beheert alleen de toegang tot de camera van het apparaat. Het heeft geen toegang tot afbeeldingen of video's.
  
- **Apple Music blokkeren**: Met **Ja** keert u terug naar de klassieke modus van de app Muziek en wordt de Muziek-service uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app Apple Music toestaat.
- **Spotlight-suggesties blokkeren**: Met **Ja** zorgt u ervoor dat Spotlight geen resultaten meer retourneert na een zoekopdracht op internet. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat Zoeken met Spotlight verbinding maakt met internet om zoekresultaten op te halen.
- **Bestandsoverdracht via Finder of iTunes blokkeren**: Met **Ja** worden services voor het delen van toepassingsbestanden uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem services voor het delen van toepassingsbestanden toestaat.

  Deze functie is van toepassing op:  
  - macOS 10.13 en hoger

## <a name="cloud-and-storage"></a>Cloud en opslag

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Synchronisatie van iCloud-sleutelhanger blokkeren**: Meet **Ja** schakelt u de synchronisatie van aanmeldingsgegevens in de sleutelhanger naar iCloud uit. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze aanmeldingsgegevens synchroniseren.
- **Bureaublad- en documentsynchronisatie van iCloud blokkeren**: Met **Ja** voorkomt u dat documenten en gegevens worden gesynchroniseerd met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het synchroniseren van documenten en sleutelwaarden met uw iCloud-opslagruimte toestaat.
- **Back-up van iCloud-mail blokkeren**: Met **Ja** voorkomt u synchronisatie van de app Mail van macOS met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van Mail met iCloud toestaat.
- **Back-up van iCloud-contactpersonen blokkeren**: Met **Ja** voorkomt u synchronisatie van contactpersonen op het apparaat met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van contactpersonen met iCloud toestaat.
- **Back-up van iCloud-agenda blokkeren**: Met **Ja** voorkomt u synchronisatie van de app Agenda van macOS met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van Agenda met iCloud toestaat.
- **Back-up van iCloud-herinneringen blokkeren**: Met **Ja** voorkomt u synchronisatie van de app Herinneringen van macOS met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van Herinneringen met iCloud toestaat.
- **Back-up van iCloud-bladwijzers blokkeren**: Met **Ja** voorkomt u synchronisatie van bladwijzers op het apparaat met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van de bladwijzers met iCloud toestaat.
- **Back-up van iCloud-notities blokkeren**: Met **Ja** voorkomt u synchronisatie van Notities op het apparaat met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van notities met iCloud toestaat.
- **Back-up van iCloud-foto's blokkeren**: Met **Ja** wordt de iCloud-fotobibliotheek uitgeschakeld en wordt voorkomen dat in iCloud de foto’s van het apparaat worden gesynchroniseerd. Foto's die niet volledig uit de iCloud-fotobibliotheek zijn gedownload, worden verwijderd uit de lokale opslag van apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van foto’s toestaat tussen het apparaat en de iCloud-fotobibliotheek.
- **Handoff blokkeren**: Met deze functie kunnen gebruikers aan het werk gaan op een macOS-apparaat en vervolgens hun werk voortzetten op een ander iOS-/iPadOS- of macOS-apparaat. Met **Ja** voorkomt u dat de Handoff-functie werkt op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat op apparaten.

  Deze functie is van toepassing op:  
  - macOS 10.15 of hoger

## <a name="connected-devices"></a>Verbonden apparaten

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **AirDrop blokkeren**: Met **Ja** voorkomt u dat gebruikers AirDrop op apparaten gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de functie AirDrop toestaat voor het uitwisselen van inhoud met apparaten in de omgeving.
- **Automatisch ontgrendelen via Apple Watch blokkeren**: Met **Ja** voorkomt u dat gebruikers hun macOS-apparaat ontgrendelen met hun Apple Watch. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers hun macOS-apparaat kunnen ontgrendelen met hun Apple Watch.

## <a name="domains"></a>Domains

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Niet-gemarkeerde e-maildomeinen**: Voeg een of meer **e-maildomein-URL's** toe aan de lijst. Wanneer gebruikers een e-mail verzenden of ontvangen die afkomstig is van een ander domein dan de domeinen die u hebt toegevoegd, wordt de e-mail in de macOS Mail-app gemarkeerd als niet-vertrouwd.

## <a name="general"></a>Algemeen

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Opzoeken blokkeren**: Met **Ja** voorkomt u dat de gebruiker een woord markeert en vervolgens de definitie ervan opzoekt op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de functie Definitie opzoeken toestaat.
- **Dicteren blokkeren**: Met **Ja** zorgt u ervoor dat gebruikers geen spraakinvoer meer kunnen gebruiken om tekst in te voeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers dicteerinvoer gebruiken.
- **Cacheopslag van inhoud blokkeren**: Met **Ja** voorkomt u dat inhoud in de cache wordt opgeslagen. Met cacheopslag van inhoud worden app-gegevens, webbrowsergegevens, downloads en meer lokale items op apparaten opgeslagen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem caching van inhoud inschakelt.

  Zie [Cacheopslag van inhoud beheren op een Mac](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac) (hiermee wordt een andere website geopend) voor meer informatie over cacheopslag van inhoud in macOS.

  Deze functie is van toepassing op:  
  - macOS 10.13 en hoger

- **Software-updates uitstellen**: Met **Ja** kunt u het weergeven van software-updates op apparaten uitstellen, van 0-90 dagen. Deze instelling bepaalt niet wanneer updates wel of niet worden geïnstalleerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem updates op apparaten weergeeft wanneer Apple deze heeft uitgegeven. Als Apple bijvoorbeeld op een bepaalde datum een macOS-update uitbrengt, wordt deze update rond de releasedatum automatisch op apparaten weergegeven. Seed-buildupdates zijn zonder vertraging toegestaan.  

  - **De zichtbaarheid van software-updates vertragen**: Voer een waarde in tussen 0 en 90 dagen. Wanneer de vertraging verloopt, krijgen gebruikers een melding om een update uit te voeren naar de vroegste versie van het besturingssysteem die beschikbaar was toen de vertraging werd geactiveerd.

    Als een macOS-update bijvoorbeeld beschikbaar komt op **1 januari** en **Zichtbaarheid vertragen** is ingesteld op **5 dagen**, wordt de update niet als beschikbare update weergegeven. Op de **zesde dag** na de release komt deze update beschikbaar en kunnen gebruikers deze installeren.

    Deze functie is van toepassing op:  
    - macOS 10.13.4 en hoger

- **Schermafbeeldingen en -opnamen blokkeren**: Het apparaat moet zijn ingeschreven bij het geautomatiseerde DEP (Device Enrollment Program) van Apple. Met **Ja** kunnen gebruikers geen schermopnamen van de weergave opslaan. Ook wordt het bekijken van externe schermen via de Classroom-app geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat schermopnamen vast te leggen, en de Classroom-app de mogelijkheid biedt om externe schermen weer te geven.

  - **AirPlay, scherm weergeven door Classroom-app en scherm delen uitschakelen**: Met **Ja** wordt AirPlay geblokkeerd en wordt het delen van bestanden met andere apparaten voorkomen. Ook kunnen docenten de Classroom-app niet gebruiken om de schermen van hun studenten te bekijken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem docenten toestaat de schermen van hun leerlingen/studenten te bekijken.

    Als u deze instelling wilt gebruiken, stelt u de instelling **Schermafbeeldingen en -opnamen blokkeren** in op **Niet geconfigureerd** (schermopnamen zijn toegestaan).

  - **Classroom-app toestaan om zonder te vragen AirPlay uit te voeren en het scherm weer te geven**: Met **Ja** kunnen docenten de schermen van hun studenten bekijken zonder dat deze daar toestemming voor hoeven te geven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem vereist dat docenten de schermen pas kunnen zien als studenten akkoord gaan.

    Als u deze instelling wilt gebruiken, stelt u de instelling **Schermafbeeldingen en -opnamen blokkeren** in op **Niet geconfigureerd** (schermopnamen zijn toegestaan).

- **Toestemming van docent vereisen om onbeheerde lessen in de Classroom-app te verlaten**: Met **Ja** hebben studenten die zijn ingeschreven bij een niet-beheerde Classroom-cursus, goedkeuring van de docent nodig om de cursus te verlaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem studenten toestaat de cursus te verlaten wanneer ze willen.

- **De app Classroom toestaan om het apparaat te vergrendelen zonder te vragen**: Met **Ja** kunnen docenten het apparaat of een app van een student vergrendelen zonder goedkeuring van de student. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem vereist dat docenten het apparaat of de app pas kunnen vergrendelen als studenten akkoord gaan.

- **Studenten kunnen automatisch deelnemen aan een Classroom-les zonder te vragen**: Met **Ja** kunnen studenten zich bij een les aansluiten zonder dat aan de docent te hoeven vragen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem vereist dat docenten goedkeuring geven voor deelname aan een klas.

## <a name="password"></a>Wachtwoord

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Wachtwoord vereisen**: Met **Ja** moeten gebruikers een wachtwoord invoeren om toegang te krijgen tot apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem geen wachtwoord vereist. Er worden ook geen beperkingen afgedwongen, zoals het blokkeren van eenvoudige wachtwoorden of het instellen van een minimumlengte.
  - **Vereist wachtwoordtype**: Voer het vereiste complexiteitsniveau voor het wachtwoord in dat uw organisatie nodig heeft. Als u dit leeg laat, wordt deze instelling niet gewijzigd of bijgewerkt door Intune. Uw opties zijn:
    - **Niet geconfigureerd**: Hiermee wordt de standaardwaarde van het apparaat gebruikt.
    - **Alfanumeriek**: Dit zijn hoofdletters, kleine letters en numerieke tekens.
    - **Numeriek**: Het wachtwoord mag alleen uit getallen bestaan, bijvoorbeeld 123456789.

    Deze functie is van toepassing op:  
    - macOS 10.10.3 en hoger

  - **Het aantal niet-alfanumerieke tekens in het wachtwoord**: Geef op hoeveel complexe tekens zijn vereist in het wachtwoord, tussen 0 en 4. Een complex teken is een symbool, zoals `?`. Wanneer dit leeg wordt gelaten of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens. Als u dit leeg laat, wordt deze instelling niet gewijzigd of bijgewerkt door Intune.
  - **Eenvoudige wachtwoorden blokkeren**: Met **Ja** voorkomt u dat er eenvoudige wachtwoorden worden gebruikt, zoals `0000` of `1234`. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem eenvoudige wachtwoorden toestaat.
  - **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**: Voer de tijdsduur in gedurende welke apparaten inactief moeten zijn voordat het scherm automatisch wordt vergrendeld. Voer bijvoorbeeld `5` in om apparaten te vergrendelen nadat deze vijf minuten lang inactief zijn geweest. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Maximum aantal minuten na schermvergrendeling voordat wachtwoord is vereist**: Geef op hoe lang de computer inactief moet zijn voordat een wachtwoord vereist is om te ontgrendelen. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Wachtwoordverlooptijd (dagen)** : Geef het aantal dagen tussen 1 en 65535 op waarna het wachtwoord voor het apparaat moet worden gewijzigd. Voer bijvoorbeeld `90` als u wilt dat het wachtwoord na 90 dagen verloopt. Wanneer het wachtwoord is verlopen, wordt gebruikers gevraagd een nieuw wachtwoord te maken. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Wachtwoorden niet opnieuw gebruiken**: Gebruikers beperken in het hergebruik van eerder gebruikte wachtwoorden. Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld 5 invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

- **Blokkeren dat gebruiker de wachtwoordcode wijzigt**: Met **Ja** voorkomt u dat de wachtwoordcode kan worden gewijzigd, toegevoegd of verwijderd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat wachtwoordcodes worden toegevoegd, gewijzigd of verwijderd.

- **Touch ID voor ontgrendelen van apparaat blokkeren**: Met **Ja** kunnen geen vingerafdrukken worden gebruikt om apparaten te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van een vingerafdruk.

- **Automatisch wachtwoorden invullen blokkeren**: Met **Ja** voorkomt u dat de functie Wachtwoorden automatisch invullen wordt gebruikt in macOS. Als u **Ja** kiest, heeft dat ook de volgende gevolgen:

  - Gebruikers wordt niet meer gevraagd om een wachtwoord te gebruiken dat is opgeslagen in Safari of in een app.
  - Automatische sterke wachtwoorden zijn uitgeschakeld en gebruikers krijgen geen suggesties voor sterke wachtwoorden.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functies toestaat.

- **Aanvragen voor wachtwoordnabijheid blokkeren**: Met **Ja** voorkomt u dat apparaten wachtwoorden van nabijgelegen apparaten aanvragen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze wachtwoordaanvragen toestaat.

- **Wachtwoorden delen blokkeren**: Selecteer **Ja** om te voorkomen dat wachtwoorden via AirDrop tussen apparaten worden gedeeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het delen van wachtwoorden toestaat.

## <a name="privacy-preferences"></a>Privacyvoorkeuren

Op macOS-apparaten vragen apps en processen gebruikers vaak om toegang tot apparaatfuncties toe te staan of te weigeren, zoals de camera, de microfoon, de agenda, de documentenmap en nog veel meer. Met deze instellingen kunnen beheerders de toegang tot deze apparaatfuncties vooraf goedkeuren of weigeren. Wanneer u deze instellingen configureert, beheert u de toestemming voor gegevenstoegang namens uw gebruikers. Uw instellingen overschrijven hun vorige beslissingen.

Het doel van deze instellingen is het verminderen van het aantal prompts door apps en processen.

Deze functie is van toepassing op:

- macOS 10.14 en hoger
- Sommige instellingen zijn van toepassing op macOS 10.15 en hoger.
- Deze instellingen zijn alleen van toepassing op apparaten waarop het profiel voor privacyvoorkeuren is geïnstalleerd voordat de upgrade wordt uitgevoerd.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Deze instellingen zijn van toepassing op: Door de gebruiker goedgekeurde apparaatinschrijving, automatische apparaatregistratie

- **Apps en processen**: **Voeg** apps of processen toe om de toegang te configureren. Voer ook in:
  - **Naam**: Voer een naam in voor uw app of proces. Voer bijvoorbeeld `Microsoft Remote Desktop` of `Microsoft Office 365` in.
  
  - **Id-type**: Uw opties zijn:
    - **Bundel-id**: Selecteer deze optie voor apps.
    - **Pad**: Selecteer deze optie voor niet-gebundelde binaire bestanden. Dit is een proces of een uitvoerbaar bestand.

    Help-programma's die in een toepassingsbundel zijn ingesloten, nemen automatisch de machtigingen over van de insluitende toepassingsbundel.

  - **Id**: Voer de app-bundel-id of het pad naar het installatiebestand van het proces of het uitvoerbare bestand in. Voer bijvoorbeeld `com.contoso.appname` in.

    Als u de app-bundel-id wilt ophalen, opent u de Terminal-app en voert u de `codesign`-opdracht uit. Met deze opdracht wordt de codehandtekening geïdentificeerd. U kunt dan de bundel-id en de codehandtekening tegelijkertijd ophalen.

  - **Codevereiste**: Voer de codehandtekening in voor de toepassing of het proces.

    Er wordt een codehandtekening gemaakt wanneer een app of binair bestand wordt ondertekend door een ontwikkelaarscertificaat. U kunt de toewijzing vinden door de `codesign`-opdracht handmatig uit te voeren in de Terminal-app: `codesign --display -r -/path/to/app/binary`. De codehandtekening is alles wat na `=>` wordt weergegeven.

  - **Statische codevalidatie inschakelen**: Kies **Ja** als u wilt dat de app of het proces het codevereiste statisch valideert. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

    Schakel deze instelling alleen in als het proces de dynamische codehandtekening ongeldig maakt. Gebruik anders **Niet geconfigureerd**.  

  - **Camera blokkeren**: Met **Ja** voorkomt u dat de app toegang krijgt tot de systeemcamera. U kunt geen toegang tot de camera verlenen. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  - **Microfoon blokkeren**: Met **Ja** voorkomt u dat de app toegang krijgt tot de systeemmicrofoon. U kunt geen toegang tot de microfoon verlenen. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  - **Schermopnamen blokkeren**: Met **Ja** kan de app de inhoud van de systeemweergave niet vastleggen. U kunt geen toegang tot schermopnamen en schermafbeeldingen verlenen. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **Bewaking van invoer blokkeren**: Met **Ja** kan de app niet CoreGraphics- en HID-API's gebruiken om te luisteren naar CGEvents- en HID-gebeurtenissen van alle processen. Met **Ja** kunnen apps en processen ook niet luisteren naar gegevens en deze evenmin verzamelen uit invoerapparaten, zoals een muis, toetsenbord of trackpad. U kunt geen toegang tot de CoreGraphics- en HID-API's verlenen.

    Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **Spraakherkenning**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee kan de app toegang krijgen tot de spraakherkenning van het systeem en kunnen spraakgegevens naar Apple worden verzonden.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang kan krijgen tot de spraakherkenning van het systeem en dat spraakgegevens naar Apple worden verzonden.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **Toegankelijkheid**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee kan de app toegang krijgen tot de app Toegankelijkheid van het systeem. Deze app bevat ondertiteling, aanwijstekst en spraakcontrole.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang krijgt tot de app Toegankelijkheid van het systeem.

  - **Contactpersonen**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot contactgegevens die worden beheerd door de app Contactpersonen van het systeem.  
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze contactgegevens.

  - **Agenda**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot agendagegevens die worden beheerd door de app Agenda van het systeem.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze agendagegevens.

  - **Herinneringen**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot herinneringengegevens die worden beheerd door de app Herinneringen van het systeem.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze herinneringsgegevens.

  - **Foto's**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot de afbeeldingen die worden beheerd door de app Foto's van het systeem in `~/Pictures/.photoslibrary`.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze afbeeldingen.

  - **Mediabibliotheek**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot Apple Music, muziek- en videoactiviteit en de mediabibliotheek.  
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze media.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **Aanwezigheid van bestandsprovider**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot de app Bestandsprovider en kan deze detecteren wanneer gebruikers bestanden gebruiken die worden beheerd door Bestandsprovider. Met een bestandsprovider-app kunnen andere bestandsprovider-apps toegang krijgen tot de documenten en mappen die zijn opgeslagen en beheerd door de betreffende app.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot de app Bestandsprovider.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **Toegang tot volledige schijf**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot alle beveiligde bestanden, met inbegrip van systeembeheerbestanden. Wees voorzichtig met het toepassen van deze instelling.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze beveiligde bestanden.

  - **Systeembeheerbestanden**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot bepaalde bestanden die worden gebruikt in het systeembeheer.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze bestanden.

  - **De map Bureaublad**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot bestanden in de map Bureaublad van de gebruiker.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze bestanden.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **De map Documenten**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot bestanden in de map Documenten van de gebruiker.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze bestanden.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **De map Downloads**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot bestanden in de map Downloads van de gebruiker.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze bestanden.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **Netwerkvolumes**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee heeft de app toegang tot bestanden op netwerkvolumes.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze bestanden.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **Verwisselbare volumes**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee kan de app toegang krijgen tot bestanden op verwisselbare volumes, zoals een harde schijf.
    - **Blokkeren**: Hiermee voorkomt u dat de app toegang heeft tot deze bestanden.

    Hiervoor is macOS 10.15 of hoger vereist.

  - **Systeemgebeurtenissen**: Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Toestaan**: Hiermee kan de app CoreGraphics-API's gebruiken om CGEvents naar de gebeurtenisgegevensstroom van het systeem te verzenden.
    - **Blokkeren**: Hiermee voorkomt u dat de app CoreGraphics-API's kan gebruiken om CGEvents naar de gebeurtenisgegevensstroom van het systeem te verzenden.

  - **Apple-gebeurtenissen**: Met deze instelling kunnen apps een beperkte Apple-gebeurtenis verzenden naar een andere app of een ander proces. Selecteer **Toevoegen** om een ontvangende app of ontvangend proces toe te voegen. Voer de volgende informatie in van de ontvangende app of het ontvangend proces:

    - **Id-type**: Selecteer **Bundel-id** als de ontvangende id een toepassing is. Selecteer **Pad** als de ontvangende id een proces of een uitvoerbaar bestand is.
    
    - **Id**: Voer de app-bundel-id of het installatiepad van het proces dat de Apple-gebeurtenis ontvangt.  

    - **Codevereiste**: Voer de codehandtekening in voor de ontvangende toepassing of het ontvangende proces.

      Er wordt een codehandtekening gemaakt wanneer een app of binair bestand wordt ondertekend door een ontwikkelaarscertificaat. U kunt de toewijzing vinden door de `codesign`-opdracht handmatig uit te voeren in de Terminal-app: `codesign --display -r -/path/to/app/binary`. De codehandtekening is alles wat na `=>` wordt weergegeven.

    - **Toegang**: Toestaan dat een macOS Apple-gebeurtenis wordt verzonden naar de ontvangende app of het ontvangende proces. Uw opties zijn:
      - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
      - **Toestaan**: Hiermee kan de app of het proces de beperkte Apple-gebeurtenis verzenden naar de ontvangende app of het ontvangende proces.
      - **Blokkeren**: Hiermee voorkomt u dat de app of het proces de beperkte Apple-gebeurtenis kan verzenden naar de ontvangende app of het ontvangende proces.

  - U moet vervolgens de wijzigingen **Opslaan**.

## <a name="restricted-apps"></a>Beperkte apps

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Lijst met typen beperkte apps**: Hiermee maakt u een lijst met apps die gebruikers niet mogen installeren of gebruiken. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat gebruikers toegang hebben tot door u toegewezen apps en ingebouwde apps.
  - **Goedgekeurde apps**: Hiermee maakt u een lijst met apps die gebruikers mogen installeren. Om te voldoen aan het beleid, mogen gebruikers geen andere apps installeren. Apps die worden beheerd door Intune worden automatisch toegestaan, zoals de bedrijfsportal-app. Er wordt niet voorkomen dat gebruikers een app installeren die niet in de goedgekeurde lijst wordt vermeld. Maar als dat wel het geval is, wordt dit in Intune gerapporteerd.
  - **Niet-toegestane apps**: Hiermee maakt u een lijst met apps die niet worden beheerd door Intune en die gebruikers niet mogen installeren en uitvoeren. Gebruikers kunnen geen verboden apps installeren. Als een gebruiker een app uit deze lijst installeert, wordt deze in Intune gerapporteerd.

- **Apps-lijst**: Apps **toevoegen** aan uw lijst:
  - **App-bundel-id**: Voer de [bundel-id](bundle-ids-built-in-ios-apps.md) van de app in. U kunt ingebouwde apps en Line-Of-Business-apps toevoegen. De website van Apple bevat een lijst met [ingebouwde Apple-apps](https://support.apple.com/HT208094).

    Als u de URL van een app wilt vinden, opent u de iTunes App Store en gaat u naar de app. Zoek bijvoorbeeld naar `Microsoft Remote Desktop` of `Microsoft Word`. Selecteer de app en kopieer de URL. U kunt ook iTunes gebruiken om de app te zoeken en vervolgens de taak **Koppeling kopiëren** gebruiken om de URL van de app te krijgen.

  - **App-naam**: Voer een gebruiksvriendelijke naam in om u te helpen de bundel-id te identificeren. Voer bijvoorbeeld `Intune Company Portal app` in.
  - **Uitgever**: Voer de uitgever van de app in.

- **Importeer** een CSV-bestand met details van de app, waaronder de URL. Gebruik de notatie `<app bundle ID>, <app name>, <app publisher>`. U kunt ook **Exporteren** om een lijst met apps te maken in dezelfde indeling.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook apparaatfuncties en -instellingen beperken op [iOS-/iPadOS](device-restrictions-ios.md)-apparaten.
