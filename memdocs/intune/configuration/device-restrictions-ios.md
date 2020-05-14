---
title: iOS-/iPadOS-apparaatinstellingen in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: U kunt instellingen voor iOS-/iPadOS-apparaten toevoegen, configureren of maken om functies te beperken, zoals wachtwoordvereisten instellen, het vergrendelingsscherm beheren, ingebouwde apps gebruiken, beperkte of goedgekeurde apps toevoegen, Bluetooth-apparaten verwerken, verbinding maken met de cloud voor back-up en opslag, de kioskmodus inschakelen, domeinen toevoegen, en bepalen hoe gebruikers de Safari-webbrowser kunnen gebruiken in Microsoft Intune.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49ecd2a1aaa5408a721b06264703720be601c73c
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83269011"
---
# <a name="ios-and-ipados-device-settings-to-allow-or-restrict-features-using-intune"></a>Met instellingen voor iOS- en iPadOS-apparaten kunt u functies toestaan of beperken met behulp van Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen die u kunt beheren op iOS- en iPadOS-apparaten. Gebruik deze instellingen als onderdeel van de MDM-oplossing (Mobile Device Management) om functies toe te staan of uit te schakelen, wachtwoordregels in te stellen, bepaalde apps toe te staan of te beperken en nog veel meer.

Deze instellingen worden toegevoegd aan een apparaatconfiguratieprofiel in Intune en vervolgens toegewezen aan of geïmplementeerd op iOS-/iPadOS-apparaten.

> [!TIP]
> Voor deze instellingen worden de MDM-instellingen van Apple gebruikt. Raadpleeg [Instellingen voor mobielapparaatbeheer van Apple](https://support.apple.com/guide/mdm/welcome/web) (hiermee opent u de website van Apple) voor meer informatie over deze instellingen.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een configuratieprofiel voor apparaatbeperkingen](device-restrictions-configure.md).

> [!NOTE]
> Deze instellingen zijn van toepassing op verschillende inschrijvingstypen, waarbij sommige instellingen van toepassing zijn op alle inschrijvingsopties. Zie [iOS-/iPadOS-inschrijving](../enrollment/ios-enroll.md) voor meer informatie over de verschillende inschrijvingstypen.

## <a name="general"></a>Algemeen

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Gebruiksgegevens delen**: Met **Blokkeren** voorkomt u dat apparaten diagnostische gegevens en gebruiksgegevens naar Apple verzenden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de verzending van deze gegevens toestaat.

- **Schermopname**: Met **Blokkeren** voorkomt u dat er op apparaten schermopnamen of schermafbeeldingen worden gemaakt. In iOS/iPadOS 9.0 en hoger worden hiermee ook schermopnamen geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de inhoud van het scherm vastleggen als een afbeelding of video.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Niet-vertrouwde TLS-certificaten**: Met **Blokkeren** voorkomt u niet-vertrouwde TLS-certificaten (Transport Layer Security) op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem TLS-certificaten toestaat.
- **Draadloze PKI-updates blokkeren**: Met **Blokkeren** voorkomt u dat uw gebruikers software-updates ontvangen tenzij apparaten zijn verbonden met een computer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat een apparaat software-updates ontvangt zonder dat het verbonden is met een computer.
- **Bijhouden van advertenties beperken**: Met **Beperken** wordt de advertentie-id van het apparaat uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem ingeschakeld blijft.
- **Bedrijfsapps vertrouwen**: Met **Blokkeren** wordt de knop **Ontwikkelaar vertrouwen** op het apparaat verwijderd in Instellingen > Algemeen > Profielen en apparaatbeheer van apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers laat kiezen of ze apps vertrouwen die niet zijn gedownload uit de App Store.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Aanpassing van instellingen voor het verzenden van diagnostische gegevens**: **Blokkeren** voorkomt dat de gebruiker de instelling voor verzending van diagnostische gegevens en app-analyse wijzigt in **Diagnostische gegevens en gebruik** (in apparaatinstellingen). Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze apparaatinstellingen wijzigen.

  Stel de instelling **Gebruiksgegevens delen** in op **Blokkeren** als u deze instelling wilt gebruiken.

  Deze functie is van toepassing op:  
  - iOS 9.3.2 en hoger
  - iPadOS 13.0 en hoger

- **Observatie van extern scherm met de app Classroom**: Met **Blokkeren** voorkomt u dat het scherm op apparaten op afstand kan worden bekeken met de app Apple Classroom. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het in het besturingssysteem is toegestaan dat het scherm wordt weergegeven in de app Apple Classroom.

  Stel de instelling **Schermopname** in op **Blokkeren** als u deze instelling wilt gebruiken.

  Deze functie is van toepassing op:  
  - iOS 9.3 en hoger
  - iPadOS 13.0 en hoger

- **Ongevraagde schermobservatie met de app Classroom**: Met **Toestaan** kunnen docenten het scherm op de iOS-/iPadOS-apparaten van leerlingen/studenten observeren via de app Classroom zonder dat de leerlingen/studenten dit weten. Op apparaten van leerlingen/studenten die zijn ingeschreven bij een cursus met behulp van de app Classroom, is toestemming voor de docent van deze cursus automatisch ingeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van deze functie niet toestaat.

  Stel de instelling **Schermopname** in op **Blokkeren** als u deze instelling wilt gebruiken.

- **Accountaanpassing**: Met **Blokkeren** kunnen gebruikers de apparaatspecifieke instellingen niet bijwerken vanuit de app voor iOS-/iPadOS-instellingen. Gebruikers kunnen dan bijvoorbeeld geen nieuwe apparaataccounts maken, of de gebruikersnaam of het wachtwoord wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instellingen wijzigen.

  Deze functie geldt ook voor instellingen die toegankelijk zijn vanuit de app voor iOS-/iPadOS-instellingen, zoals E-mail, Contactpersonen, Agenda, Twitter, en meer. Deze functie geldt niet voor apps met accountinstellingen die niet kunnen worden geconfigureerd vanuit de app voor iOS-/iPadOS-instellingen, zoals de Microsoft Outlook-app.

- **Schermtijd**: **Blokkeren** voorkomt dat gebruikers hun eigen beperkingen in Schermtijd instellen (apparaatinstellingen). Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers apparaatbeperkingen (zoals ouderlijk toezicht, inhoudsbeperkingen en privacybeperkingen) configureren op apparaten.

  Deze instelling heette eerst **Beperkingen inschakelen in de apparaatinstellingen**. Gevolgen van deze wijziging:  
  
  - iOS 11.4.1 en ouder: **Blokkeren** voorkomt dat eindgebruikers hun eigen beperkingen kunnen instellen bij de apparaatinstellingen. Het gedrag is hetzelfde. Er zijn geen wijzigingen voor gebruikers.
  - iOS 12.0 en nieuwer: **Blokkeren** voorkomt u dat gebruikers hun eigen **Schermtijd** kunnen instellen via de apparaatinstellingen (Instellingen > Algemeen > Schermtijd), waaronder inhouds- en privacybeperkingen. Apparaten die zijn geüpgraded naar iOS 12.0 krijgen het tabblad Beperkingen niet meer te zien bij de apparaatinstellingen (Instellingen > Algemeen > Apparaatbeheer > Beheerprofiel > Beperkingen). Deze instellingen vindt u onder **Schermtijd**.
  
- **Gebruik van de optie voor het wissen van alle inhoud en instellingen op het apparaat**: Met **Blokkeren** kan de optie Alle inhoud en instellingen wissen niet worden gebruikt op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toegang geeft tot deze instellingen.
- **Apparaatnaam wijzigen**: Met **Blokkeren** voorkomt u dat de naam van het apparaat wordt gewijzigd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de naam van apparaten wijzigen.
- **Aanpassing van meldingsinstellingen**: Met **Blokkeren** voorkomt u dat de instellingen voor meldingen worden gewijzigd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de meldingsinstellingen van het apparaat wijzigen.
- **Aanpassing van achtergrond**: Selecteer **Blokkeren**, zodat de achtergrond niet kan worden gewijzigd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de achtergrond van apparaten wijzigen.
- **Wijzigingen in configuratieprofielen**: Met **Blokkeren** voorkomt u dat configuratieprofielen op apparaten worden gewijzigd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers configuratieprofielen installeren.
- **Activeringsvergrendeling**: Met **Toestaan** schakelt u Activeringsvergrendeling in op iOS/iPadOS-apparaten in de supervisiemodus. Met Activeringsslot kan een verloren of gestolen apparaat moeilijker opnieuw worden geactiveerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Verwijderen van app blokkeren**: Met **Blokkeren** kunnen gebruikers geen apps verwijderen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers apps van apparaten kunnen verwijderen.
- **USB-accessoires toestaan terwijl het apparaat is vergrendeld**: Met **Toestaan** kunnen gegevens worden uitgewisseld tussen USB-accessoires en apparaten die al meer dan een uur zijn vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de beperkte USB-modus niet bijwerkt op apparaten en dat USB-accessoires geen gegevens kunnen overdragen vanaf apparaten als deze langer dan een uur zijn vergrendeld.

  Deze functie is van toepassing op:  
  - iOS/iPadOS 11.4.1 en hoger

- **Automatisch instellen van datum en tijd afdwingen**: Met **Vereisen** wordt het instellen van de datum en tijd automatisch afgedwongen op apparaten in de supervisiemodus. De tijdzone van het apparaat wordt bijgewerkt wanneer het apparaat mobiele verbindingen heeft of wanneer Wi-Fi met locatieservices is ingeschakeld voor het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Studenten moeten toestemming vragen om de Classroom-cursus te verlaten**: Met **Vereisen** wordt afgedwongen dat leerlingen/studenten die zijn ingeschreven bij een niet-beheerde cursus met de app Klaslokaal, toestemming aan de docent vragen om de cursus te verlaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem niet afdwingt dat de leerling/student om toestemming vraagt.

  Deze functie is van toepassing op:  
  - iOS 11.3 en hoger
  - iPadOS 13.0 en hoger

- **De app Classroom toestaan om een app te vergrendelen en het apparaat te vergrendelen zonder te vragen**: Met **Inschakelen** kan de docent zonder tussenkomst van de student apps of apparaten vergrendelen met behulp van de app Classroom. Apps vergrendelen betekent dat alleen door de docent gespecificeerde apps op apparaten toegankelijk zijn. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voorkomt dat docenten zonder tussenkomst van de student apps of apparaten kunnen vergrendelen met behulp van de app Classroom.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

- **Automatisch lid worden van Classroom-klassen zonder te vragen**: Met **Inschakelen** kunnen studenten automatisch deelnemen aan een les in de app Classroom, zonder tussenkomst van de docent. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de docent informeert dat studenten willen deelnemen aan een les in de app Classroom.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

- **Het maken van VPN's blokkeren**: Selecteer **Blokkeren** om te voorkomen dat gebruikers instellingen maken voor VPN-configuratie. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers VPN's maken op apparaten.
- **eSIM-instellingen aanpassen**: Met **Blokkeren** voorkomt u dat gebruikers een mobiel abonnement verwijderen uit of toevoegen aan de eSIM op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instellingen wijzigen.

  Deze functie is van toepassing op:  
  - iOS 12.1 en hoger
  - iPadOS 13.0 en hoger

- **Software-updates uitstellen**: Met **Inschakelen** kunt u het weergeven van software-updates op apparaten uitstellen, van 0-90 dagen. Deze instelling bepaalt niet wanneer updates wel of niet worden geïnstalleerd.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem software-updates op apparaten weergeeft wanneer Apple deze heeft uitgegeven. Als Apple bijvoorbeeld op een bepaalde datum een iOS-/iPadOS-update uitbrengt, wordt deze update rond de releasedatum automatisch weergegeven op apparaten.  

  - **De zichtbaarheid van software-updates vertragen**: Voer een waarde in tussen 0 en 90 dagen. Wanneer de vertraging verloopt, krijgen gebruikers een melding om een update uit te voeren naar de vroegste versie van het besturingssysteem die beschikbaar was toen de vertraging werd geactiveerd.

    Als iOS 12.a bijvoorbeeld beschikbaar komt op **1 januari** en **Zichtbaarheid vertragen** is ingesteld op **5 dagen**, wordt iOS 12.a niet als beschikbare update weergeven op apparaten van de gebruiker. Op de **zesde dag** na de release komt deze update beschikbaar en kunnen gebruikers deze installeren.

    Deze instelling is van toepassing op:  
    - iOS 11.3 en hoger
    - iPadOS 13.0 en hoger

## <a name="password"></a>Wachtwoord

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Wachtwoord**: **Vereisen** dat gebruikers een wachtwoord invoeren om toegang te krijgen tot apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers toegang verkrijgen tot apparaten zonder dat zij een wachtwoord invoeren.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

> [!IMPORTANT]
> Als u op door de gebruiker ingeschreven apparaten een wachtwoordinstelling configureert, worden de instellingen voor **Eenvoudige wachtwoorden** automatisch ingesteld op **Blokkeren** en wordt een 6-cijferige pincode afgedwongen.
>
> U kunt bijvoorbeeld de instelling **Wachtwoord verloopt** configureren en dit beleid pushen naar de door gebruikers ingeschreven apparaten. Op de apparaten gebeurt dan het volgende:
>
> - De instelling **Wachtwoord verloopt** wordt genegeerd.
> - Eenvoudige wachtwoorden, zoals `1111` of `1234`, worden niet toegestaan.
> - Er wordt een 6-cijferige pincode afgedwongen.

- **Eenvoudige wachtwoorden**: Bij **Blokkeren** zijn complexere wachtwoorden vereist. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem eenvoudige wachtwoorden toestaat, zoals `0000` en `1234`.

- **Vereist wachtwoordtype**: Voer het vereiste complexiteitsniveau voor het wachtwoord in dat uw organisatie nodig heeft. Uw opties zijn:
  - **Standaardwaarde apparaat**
  - **Numeriek**: Het wachtwoord mag alleen uit getallen bestaan, bijvoorbeeld 123456789.
  - **Alfanumeriek**: Dit zijn hoofdletters, kleine letters en numerieke tekens.
- **Het aantal niet-alfanumerieke tekens in het wachtwoord**: Geef het aantal symbooltekens op tussen 1 en 4, zoals `#` of `@`, dat het wachtwoord moet bevatten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

- **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens. Voer een lengte tussen 4 en 6 tekens in voor door de gebruiker ingeschreven apparaten.
  
  > [!NOTE]
  > Voor apparaten die door de gebruiker zijn ingeschreven, kunnen gebruikers een pincode van meer dan 6 cijfers instellen. Er worden echter niet meer dan 6 cijfers afgedwongen op het apparaat. Stel dat een beheerder de minimale lengte instelt op `8`. Gebruikers hoeven op apparaten die door gebruikers zijn ingeschreven alleen een 6-cijferig pincode in te stellen. Intune dwingt geen pincode van meer dan 6 cijfers af op door gebruikers geregistreerde apparaten.

- **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal mislukte aanmeldingen in tussen 4 en 11 voordat het apparaat wordt gewist.
  
  iOS/iPadOS heeft ingebouwde beveiliging die van invloed kan zijn op deze instelling. iOS/iPadOS kan bijvoorbeeld het activeren van beleid vertragen, afhankelijk van het aantal mislukte aanmeldingen. Ook kan het besturingssysteem het herhaaldelijk invoeren van dezelfde toegangscode als één poging beschouwen. De [iOS-/iPadOS-beveiligingshandleiding](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) van Apple (opent de website van Apple) is een goede bron en biedt meer specifieke informatie over wachtwoordcodes.
  
- **Maximum aantal minuten na schermvergrendeling voordat wachtwoord is vereist**<sup>1</sup>: Geef op hoe lang apparaten inactief moeten zijn voordat gebruikers hun wachtwoord opnieuw moeten invoeren. Als de ingevoerde tijd langer is dan de tijd die is ingesteld op het apparaat, wordt de door u ingevoerde tijd genegeerd.

  Deze instelling is van toepassing op:  
  - iOS 8.0+
  - iPadOS 13.0+

- **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**<sup>1</sup>: Voer het maximale aantal minuten van inactiviteit in dat is toegestaan op apparaten totdat het scherm wordt vergrendeld.

  **Opties voor iOS/iPadOS**:  

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Onmiddellijk**: Het scherm wordt vergrendeld na 30 seconden inactiviteit.
  - **1**: Het scherm wordt vergrendeld na 1 minuut inactiviteit.
  - **2**: Het scherm wordt vergrendeld na 2 minuten inactiviteit.
  - **3**: Het scherm wordt vergrendeld na 3 minuten inactiviteit.
  - **4**: Het scherm wordt vergrendeld na 4 minuten inactiviteit.
  - **5**: Het scherm wordt vergrendeld na 5 minuten inactiviteit.

  **Opties voor iPadOS**:  

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Onmiddellijk**: Het scherm wordt vergrendeld na 2 minuten inactiviteit.
  - **2**: Het scherm wordt vergrendeld na 2 minuten inactiviteit.
  - **5**: Het scherm wordt vergrendeld na 5 minuten inactiviteit.
  - **10**: Het scherm wordt vergrendeld na 10 minuten inactiviteit.
  - **15**: Het scherm wordt vergrendeld na 15 minuten inactiviteit.

  Als een waarde niet van toepassing is op iOS en iPadOS, wordt in Apple de dichtstbijzijnde *laagste* waarde gebruikt. Als u bijvoorbeeld `4` minuten invoert, zullen iPadOS-apparaten `2` minuten gebruiken. Als u `10` minuten invoert, gebruiken iOS-apparaten `5` minuten. Dit is een beperking van Apple.
  
  > [!NOTE]
  > De Intune-gebruikersinterface voor deze instelling scheidt de door iOS en iPadOS ondersteunde waarden niet. De gebruikersinterface wordt in een toekomstige versie mogelijk bijgewerkt.

- **Wachtwoordverlooptijd (dagen)** : Geef het aantal dagen op tussen 1 en 65535 tot het wachtwoord voor het apparaat moet worden gewijzigd.
- **Wachtwoorden niet opnieuw gebruiken**: Gebruik deze instelling om te voorkomen dat gebruikers eerder gebruikte wachtwoorden hergebruiken. Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld 5 invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Ontgrendelen met Touch ID en Face ID**: Met **Blokkeren** voorkomt u het gebruik van een vingerafdruk of gezichtsherkenning om apparaten te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers apparaten ontgrendelen met behulp van biometrie.

  Door deze instelling te blokkeren, voorkomt u ook dat apparaten worden ontgrendeld met behulp van Face ID-verificatie.

  Face ID is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Aanpassing van wachtwoordcode**: **Blokkeren** voorkomt dat de wachtwoordcode kan worden gewijzigd, toegevoegd of verwijderd. Als deze functie is geblokkeerd, worden wijzigingen in de wachtwoordcodebeperkingen genegeerd op apparaten in de supervisiemodus. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat wachtwoordcodes worden toegevoegd, gewijzigd of verwijderd.

  - **Aanpassing van Touch ID en Face ID**: **Blokkeren** voorkomt dat gebruikers Touch ID-vingerafdrukken en Face ID kunnen wijzigen, toevoegen of verwijderen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de Touch ID-vingerafdrukken en Face ID op apparaten bijwerken.

    Als u deze instelling blokkeert, kunnen gebruikers ook geen Face ID-verificatie meer wijzigen, toevoegen of verwijderen.

    Face ID is van toepassing op:  
    - iOS 11.0 en hoger
    - iPadOS 13.0 en hoger

- **Automatisch wachtwoorden invullen blokkeren**: **Blokkeren** voorkomt dat de functie Wachtwoorden automatisch invullen kan worden gebruikt in iOS/iPadOS. Als u **Blokkeren** kiest, heeft dat ook de volgende gevolgen:

  - Gebruikers wordt niet meer gevraagd om een wachtwoord te gebruiken dat is opgeslagen in Safari of in een app.
  - Automatische sterke wachtwoorden zijn uitgeschakeld en gebruikers krijgen geen suggesties voor sterke wachtwoorden.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functies toestaat.

- **Aanvragen voor wachtwoordnabijheid blokkeren**: Met **Blokkeren** voorkomt u dat apparaten wachtwoorden van nabijgelegen apparaten aanvragen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze wachtwoordaanvragen toestaat.
- **Wachtwoorden delen blokkeren**: Selecteer **Blokkeren** om te voorkomen dat wachtwoorden via AirDrop tussen apparaten worden gedeeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het delen van wachtwoorden toestaat.
- **Touch ID- of Face ID-verificatie vereisen voor het automatisch invullen van wachtwoorden of creditcardgegevens**: Selecteer **Vereisen** om gebruikers te dwingen zich te verifiëren via Touch ID of Face ID voordat wachtwoorden of creditcardgegevens automatisch kunnen worden ingevuld in Safari en andere apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze functie beheren in de apparaatinstellingen.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger
  
<sup>1</sup>Wanneer u de instellingen **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld** en **Maximum aantal minuten waarna een wachtwoord voor het vergrendelde scherm is vereist** configureert, worden deze opeenvolgend toegepast. Als u de waarde voor beide instellingen bijvoorbeeld instelt op **5** minuten, wordt het scherm na vijf minuten automatisch uitgeschakeld en worden apparaten vergrendeld na nog eens vijf minuten. Als gebruikers het scherm echter handmatig uitschakelen, wordt de tweede instelling onmiddellijk toegepast. Als gebruikers in hetzelfde voorbeeld het scherm hebben uitgeschakeld, wordt het apparaat vijf minuten later vergrendeld.

## <a name="locked-screen-experience"></a>Vergrendeld scherm

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Toegang tot Beheercentrum wanneer het apparaat is vergrendeld**: **Blokkeren** voorkomt de toegang tot de app Beheercentrum zolang het apparaat is vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot de app Beheercentrum toestaat terwijl apparaten zijn vergrendeld.
- **Meldingen terwijl het apparaat is vergrendeld**: Met **Blokkeren** hebben gebruikers geen toegang tot meldingen terwijl apparaten zijn vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot meldingen toestaat zonder dat het apparaat hoeft te worden ontgrendeld.
- **De weergave Vandaag wanneer het apparaat vergrendeld**: Met **Blokkeren** hebben gebruikers geen toegang tot de weergave Vandaag terwijl apparaten zijn vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de weergave Vandaag kunnen bekijken terwijl apparaten zijn vergrendeld.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Wallet-meldingen terwijl het apparaat is vergrendeld**: Met **Blokkeren** hebben gebruikers geen toegang tot de app Wallet terwijl apparaten zijn vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot de app Wallet toestaat terwijl apparaten zijn vergrendeld.

## <a name="app-store-doc-viewing-gaming"></a>App Store, documenten bekijken, gamen

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Zakelijke documenten weergeven in niet-beheerde apps**: Selecteer **Blokkeren** om te voorkomen dat zakelijke documenten in niet-beheerde apps worden weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat zakelijke documenten worden weergegeven in elke willekeurige app.

  Voorbeeld: u wilt voorkomen dat gebruikers bestanden uit de OneDrive-app opslaan in Dropbox. Configureer deze instelling als **Blokkeren**. Nadat apparaten het beleid hebben ontvangen (bijvoorbeeld nadat deze opnieuw zijn opgestart), kunnen er geen bestanden meer worden opgeslagen.

  > [!NOTE]
  > Als deze instelling wordt geblokkeerd, worden ook toetsenborden van derden geblokkeerd die vanuit de App Store zijn geïnstalleerd.

  - **Toestaan dat niet-beheerde apps contactpersonen lezen in beheerde accounts voor contactpersonen**: Met **Toestaan** kunnen niet-beheerde apps, zoals de ingebouwde iOS-/iPadOS-app Contacten, de contactgegevens van beheerde apps lezen en openen, met inbegrip van de mobiele Outlook-app. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem lezen, inclusief het verwijderen van dubbele contactpersonen, uit de ingebouwde app Contacten op apparaten voorkomt.  
  
    Met deze instelling wordt het lezen van contactgegevens toegestaan of voorkomen. Met de service wordt de synchronisatie van contactpersonen tussen de apps niet beheerd.
  
    Als u deze instelling wilt gebruiken, stelt u **Zakelijke documenten weergeven in niet-beheerde apps** in op **Blokkeren**.

  Voor meer informatie over deze twee instellingen en de invloed ervan op het synchroniseren van geëxporteerde contactpersonen in Outlook voor iOS/iPadOS raadpleegt u [Ondersteuningstip: Aangepaste profielinstellingen in Intune gebruiken voor de systeemeigen contactpersonen-app in iOS/iPadOS](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **AirDrop behandelen als een onbeheerd doel**: Wanneer deze optie is ingesteld op **Vereisen**, wordt AirDrop beschouwd als een onbeheerde bestemming. Het zorgt ervoor dat via beheerde apps geen gegevens meer kunnen worden verzonden met behulp van AirDrop. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Niet-zakelijke documenten weergeven in zakelijke apps**: Met **Blokkeren** voorkomt u dat niet-zakelijke documenten in zakelijke apps worden weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voorkomt dat documenten worden weergegeven in zakelijke beheerde apps.

  **Blokkeren** voorkomt ook de synchronisatie van geëxporteerde contactpersonen in Outlook voor iOS/iPadOS. Voor meer informatie raadpleegt u [Ondersteuningstip: Synchronisatie van contactpersonen in Outlook voor iOS/iPadOS inschakelen met MDM-besturingselementen in iOS 12](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **iTunes Store-wachtwoord voor alle aankopen vereisen**: **Vereis** dat gebruikers het Apple ID-wachtwoord invoeren voor elke in-app- of iTunes-aankoop. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem aankopen toestaat zonder dat elke keer om het wachtwoord wordt gevraagd.
- **In-app aankopen**: **Blokkeren** voorkomt in-app aankopen in de Store. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers vanuit een actieve app aankopen doen in de Store.
- **Inhoud uit Book Store met de markering Erotisch downloaden**: Met **Blokkeren** kunnen gebruikers geen media downloaden uit de iBooks Store die zijn aangemerkt als Erotisch. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers boeken downloaden uit de categorie Erotisch.
- **Toestaan dat beheerde apps contactpersonen doorgeven aan niet-beheerde accounts voor contactpersonen**: Met **Toestaan** kunnen beheerde apps (zoals de mobiele Outlook-app) contactinformatie, inclusief zakelijke contactpersonen, opslaan in of synchroniseren met de ingebouwde iOS-/iPadOS-app Contacten op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voorkomt dat beheerde apps contactgegevens opslaan op of synchroniseren met de ingebouwde app Contacten op iOS-/iPadOS-apparaten.
  
  Als u deze instelling wilt gebruiken, stelt u **Zakelijke documenten weergeven in niet-beheerde apps** in op **Blokkeren**.

- **Regio voor restricties**: Selecteer de regio voor restricties die u wilt gebruiken voor toegestane downloads. En selecteer vervolgens de toegestane beoordelingen voor **Films**, **Tv-programma's** en **Apps**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **App Store**: Selecteer **Blokkeren** om de toegang tot de App Store te blokkeren op apparaten in de supervisiemodus. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang toestaat.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

  - **Apps installeren via de App Store**: Met **Blokkeren** wordt de App Store niet weergegeven op het startscherm van apparaten. Gebruikers kunnen iTunes nog steeds gebruiken of met Apple Configurator apps installeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de App Store op het startscherm toestaat.
  - **Automatisch downloaden van apps**: **Blokkeren** voorkomt dat apps die zijn gekocht op andere apparaten automatisch worden gedownload en dat nieuwe apps automatisch worden bijgewerkt. Dit is niet van invloed op updates voor bestaande apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om apps die zijn gekocht op andere iOS-/iPadOS-apparaten op het apparaat te downloaden of bij te werken.

- **Expliciete muziek-, podcast- of nieuwsinhoud op iTunes**: **Blokkeren** voorkomt expliciete muziek-, podcast- of nieuwsinhoud in iTunes. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het apparaat toegang geeft tot inhoud voor volwassenen in de Store.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Game Center-vrienden toevoegen**: Met **Blokkeren** voorkomt u dat gebruikers vrienden kunnen toevoegen in Game Center. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers vrienden kunnen toevoegen in Game Center.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Game Center**: **Blokkeren** dat de Game Center-app wordt gebruikt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app Game Center op apparaten toestaat.
- **Games voor meerdere spelers**: **Blokkeren** voorkomt het spelen van games voor meerdere spelers. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers games voor meerdere spelers op apparaten spelen.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Toegang tot netwerkstation in de app Bestanden**: Met behulp van het Server Message Block-protocol (SMB) kunnen apparaten toegang krijgen tot bestanden of andere resources op een netwerkserver. Met **Uitschakelen** voorkomt u toegang tot bestanden op een netwerkstation via SMB. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang toestaat.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

## <a name="built-in-apps"></a>Ingebouwde apps

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Siri**: Met **Blokkeren** voorkomt u toegang tot Siri. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het gebruikerssysteem het gebruik van de spraakassistent Siri op apparaten toestaat.
  - **Siri als het apparaat is vergrendeld**: Met **Blokkeren** voorkomt u dat gebruikers toegang hebben tot Siri terwijl apparaten zijn vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het gebruikerssysteem het gebruik van de spraakassistent Siri op apparaten toestaat terwijl deze zijn vergrendeld.

- **Waarschuwingen voor fraude in Safari**: Selecteer **Vereisen** om fraudewaarschuwingen weer te geven in de webbrowser op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)


- **Spotlight-zoekacties voor de weergave van resultaten op internet**: Met **Blokkeren** zorgt u ervoor dat Spotlight geen resultaten meer retourneert na een zoekopdracht op internet. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat Zoeken met Spotlight verbinding maakt met internet om zoekresultaten te verstrekken.

  Deze instelling wordt gedupliceerd in de gebruikersinterface, wat in een toekomstige release wordt opgelost. Momenteel is deze instelling van toepassing op apparaten onder supervisie. In een toekomstige versie is deze instelling van toepassing op apparaten die zijn ingeschreven of automatisch zijn ingeschreven en waarvoor geen supervisie nodig is.

- **Safari-cookies**: Selecteer hoe cookies moeten worden verwerkt op het apparaat. Uw opties zijn:
  - Toestaan
  - Alle cookies blokkeren
  - Cookies van bezochte websites toestaan
  - Cookies van huidige website toestaan

- **Safari JavaScript**: Met **Blokkeren** voorkomt u dat Java-scripts worden uitgevoerd in de browser op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem Java-scripts toestaat.

- **Safari-pop-ups**: Met **Blokkeren** worden alle pop-ups in de Safari-webbrowser geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de pop-upblokkering toestaat.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Camera**: **Blokkeren** voorkomt toegang tot de camera op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot de camera van het apparaat toestaat.

  Intune beheert alleen de toegang tot de camera van het apparaat. Het heeft geen toegang tot afbeeldingen of video's.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

  - **FaceTime**: Met **Blokkeren** voorkomt u dat gebruikers toegang hebben tot de app FaceTime. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot de app FaceTime toestaat op apparaten.

    Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Siri-filter voor scheldwoorden**: Met **Vereisen** voorkomt u dat grove taal wordt gedicteerd of uitgesproken door Siri. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  Stel de instelling **Siri** in op **Blokkeren** om deze instelling te gebruiken.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger

- **Query's uitvoeren met Siri op door gebruikers gegenereerde inhoud op internet**: Selecteer **Blokkeren** om te voorkomen dat Siri toegang tot websites krijgt om vragen te beantwoorden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat Siri toegang heeft tot door gebruikers gegenereerde inhoud op internet.

  Stel de instelling **Siri** in op **Blokkeren** om deze instelling te gebruiken.

- **Apple News**: Met **Blokkeren** voorkomt u dat gebruikers toegang hebben tot de app Apple News op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app Apple News toestaat.
- **iBooks Store**: Selecteer **Blokkeren** om toegang tot de Book Store op het apparaat te blokkeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om boeken te zoeken en te kopen in de iBooks Store.
- **De app Berichten op het apparaat**: Met **Blokkeren** voorkomt u dat gebruikers de app Berichten gebruiken voor iMessage. Als apparaten tekstberichten ondersteunen, kunnen gebruikers nog steeds tekstberichten verzenden en ontvangen met behulp van sms. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de Berichten-app toestaat om berichten via internet te verzenden en te lezen.
- **Podcasts**: Selecteer **Blokkeren** om toegang tot de app Podcasts op het apparaat te blokkeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de Podcasts-app toestaat.
- **De service Music**: Met **Blokkeren** keert u terug naar de klassieke modus van de app Muziek en wordt de Muziek-service uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app Apple Music toestaat.
- **iTunes Radio-service**: Met **Blokkeren** voorkomt u dat gebruikers toegang hebben tot de app iTunes Radio op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app iTunes Radio toestaat.
- **iTunes Store**: Met **Blokkeren** voorkomt u dat gebruikers iTunes gebruiken op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem iTunes toestaat.

  Deze functie is van toepassing op:  
  - iOS 4.0 en hoger
  - iPadOS 13.0 en hoger

- **Zoek mijn iPhone**: Met **Blokkeren** voorkomt u het gebruik van deze functie in de Zoek mijn-app. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van deze 'Zoek mijn'-app-functie toestaat om de globale locatie van het apparaat te verkrijgen.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

- **Zoek mijn vrienden**: Met **Blokkeren** voorkomt u het gebruik van deze functie in de Zoek mijn-app. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de 'Zoek mijn'-app-functie toestaat om familie en vrienden te zoeken via een Apple-apparaat of via iCloud.com.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

- **Wijzigingen in de instellingen van de app Zoek mijn vrienden**: Met **Blokkeren** voorkomt u wijzigingen in de instellingen van de app Zoek vrienden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de instellingen van de app Zoek mijn vrienden wijzigen.

- **Spotlight-zoekacties voor de weergave van resultaten op internet**: Met **Blokkeren** zorgt u ervoor dat Spotlight geen resultaten meer retourneert na een zoekopdracht op internet. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat Zoeken met Spotlight verbinding maakt met internet om zoekresultaten te verstrekken.

  Deze instelling wordt gedupliceerd in de gebruikersinterface, wat in een toekomstige release wordt opgelost. Momenteel is deze instelling van toepassing op apparaten onder supervisie. In een toekomstige versie is deze instelling van toepassing op apparaten die zijn ingeschreven of automatisch zijn ingeschreven en waarvoor geen supervisie nodig is.

- **Het verwijderen van systeem-apps van apparaat blokkeren**: Met **Blokkeren** wordt de mogelijkheid uitgeschakeld om systeem-apps van het apparaat te verwijderen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers systeem-apps kunnen verwijderen.

- **Safari**: Selecteer **Blokkeren** om te voorkomen dat gebruikers de Safari-browser op apparaten kunnen gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de Safari-browser gebruiken.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Automatisch invullen in Safari**: Met **Blokkeren** wordt de functie Automatisch invullen in Safari op apparaten uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat de instellingen voor automatisch doorvoeren te wijzigen in de webbrowser.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

## <a name="restricted-apps"></a>Beperkte apps

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Lijst met typen beperkte apps**: Hiermee maakt u een lijst met apps die gebruikers niet mogen installeren of gebruiken. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat het besturingssysteem toegang toestaat tot door u toegewezen apps en ingebouwde apps.
  - **Niet-toegestane apps**: Hiermee maakt u een lijst met apps die niet worden beheerd door Intune en die gebruikers niet mogen installeren en uitvoeren. Gebruikers kunnen geen verboden apps installeren. Als een gebruiker een app uit deze lijst installeert, wordt deze in Intune gerapporteerd.
  - **Goedgekeurde apps**: Hiermee maakt u een lijst met apps die gebruikers mogen installeren. Om te voldoen aan het beleid, mogen gebruikers geen andere apps installeren. Apps die worden beheerd door Intune worden automatisch toegestaan, zoals de bedrijfsportal-app. Er wordt niet voorkomen dat gebruikers een app installeren die niet in de goedgekeurde lijst wordt vermeld. Maar als dat wel het geval is, wordt dit in Intune gerapporteerd.

Als u apps wilt toevoegen aan deze lijsten, kunt u:

- De App Store-URL van de gewenste iTunes-app **toevoegen**. Voer bijvoorbeeld `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` of `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` in om de app Microsoft Werkmappen toe te voegen.

  Als u de URL van een app wilt vinden, opent u de iTunes App Store en gaat u naar de app. Zoek bijvoorbeeld naar `Microsoft Remote Desktop` of `Microsoft Word`. Selecteer de app en kopieer de URL.

  U kunt ook iTunes gebruiken om de app te zoeken en vervolgens de taak **Koppeling kopiëren** gebruiken om de URL van de app te krijgen.

- **Importeer** een CSV-bestand met details van de app, waaronder de URL. Gebruik de notatie `<app url>, <app name>, <app publisher>`. Of een bestaande lijst **exporteren** die de beperkte apps bevat in dezelfde indeling.

> [!IMPORTANT]
> Apparaatprofielen die instellingen voor beperkte apps gebruiken, moeten worden toegewezen aan groepen gebruikers.

## <a name="show-or-hide-apps"></a>Apps weergeven of verbergen

Deze functie is van toepassing op:

- iOS 9.3 en hoger
- iPadOS 13.0 en hoger

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Lijst met typen apps**: Hiermee maakt u een lijst met apps die moeten worden weergegeven of verborgen. U kunt ingebouwde apps en Line-Of-Business-apps weergeven of verbergen. De website van Apple bevat een lijst met [ingebouwde Apple-apps](https://support.apple.com/HT208094). Uw opties zijn:

  - **Verborgen apps**: Voer een lijst met apps in die verborgen zijn voor gebruikers. Gebruikers kunnen deze apps niet weergeven of openen.
  
    Apple voorkomt dat sommige systeemeigen apps worden verborgen. U kunt de app **Instellingen** bijvoorbeeld niet verbergen op het apparaat. [Ingebouwde Apple-apps verwijderen](https://support.apple.com/HT208094) toont de apps die kunnen worden verborgen.
  
  - **Zichtbare apps**: Voer een lijst met apps in die gebruikers kunnen weergeven en starten. Andere apps kunnen niet worden weergegeven of gestart.

- **App-URL**: Voer de Store-URL in voor de app die u wilt weergeven of verbergen. Bijvoorbeeld:

  - Voer `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` of `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` in om de app Microsoft Werkmappen toe te voegen. 

  - Voer `https://itunes.apple.com/de/app/microsoft-word/id586447913` of `https://apps.apple.com/de/app/microsoft-word/id586447913` in om de Microsoft Word-app toe te voegen.

  Als u de URL van een app wilt vinden, opent u de iTunes App Store en gaat u naar de app. Zoek bijvoorbeeld naar `Microsoft Remote Desktop` of `Microsoft Word`. Selecteer de app en kopieer de URL.

  U kunt ook iTunes gebruiken om de app te zoeken en vervolgens de taak **Koppeling kopiëren** gebruiken om de URL van de app te krijgen.

- **App-bundel-id**: Voer de [App-bundel-id](bundle-ids-built-in-ios-apps.md) van de gewenste app in. U kunt ingebouwde apps en Line-Of-Business-apps weergeven of verbergen. De website van Apple bevat een lijst met [ingebouwde Apple-apps](https://support.apple.com/HT208094).
- **App-naam**: Voer de naam van de gewenste app in. U kunt ingebouwde apps en Line-Of-Business-apps weergeven of verbergen. De website van Apple bevat een lijst met [ingebouwde Apple-apps](https://support.apple.com/HT208094).
- **Uitgever**: Voer de uitgever van de gewenste app in.

Ga op een van de volgende manieren te werk om apps toe te voegen:

- **Toevoegen**: Selecteer deze optie om een lijst met uw apps te maken.
- **Importeer** een CSV-bestand met details van de app, waaronder de URL. Gebruik de notatie `<app url>, <app name>, <app publisher>`. U kunt ook **Exporteren** om een lijst in dezelfde indeling te maken met de beperkte apps die u hebt toegevoegd.

## <a name="wireless"></a>Draadloos

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Gegevensroaming**: **Blokkeren** voorkomt dataroaming via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem dataroaming toestaat wanneer het apparaat verbinding heeft met een mobiel netwerk.

  > [!IMPORTANT]
  > Deze instelling wordt behandeld als een actie op een extern apparaat. Deze instelling wordt dus niet weergegeven in het beheerprofiel op apparaten. Steeds wanneer de status van de gegevensroaming op het apparaat wordt gewijzigd, wordt **Gegevensroaming** geblokkeerd door de Intune-service. Als in een Intune-rapport de geslaagde uitvoering wordt weergegeven, weet u zeker dat het werkt, ook al wordt de instelling niet weergegeven in het beheerprofiel op het apparaat.

- **Op de achtergrond ophalen tijdens roaming**: Met **Blokkeren** voorkomt u dat gegevens tijdens roaming op de achtergrond kunnen worden opgehaald via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat apparaten gegevens, zoals e-mail, ophalen tijdens roaming op een mobiel netwerk.
- **Voicedialing**: Met **Blokkeren** voorkomt u dat gebruikers de functie voor het inspreken van nummers gebruiken op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem Nummer inspreken op apparaten toestaat.
- **Gespreksroaming**: **Blokkeren** voorkomt spraakroaming via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem spraakroaming toestaat wanneer apparaten verbinding hebben met een mobiel netwerk.
- **Persoonlijke hotspot**: **Blokkeren** schakelt de persoonlijke hotspot op apparaten uit bij elke apparaatsynchronisatie. Mogelijk is deze instelling niet compatibel met bepaalde providers. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de configuratie van de persoonlijke hotspot behoudt als de standaardwaarde die is ingesteld door gebruikers.

  > [!IMPORTANT]
  > Deze instelling wordt behandeld als een actie op een extern apparaat. Deze instelling wordt dus niet weergegeven in het beheerprofiel op apparaten. Steeds wanneer de status van de persoonlijke hotspot op het apparaat wordt gewijzigd, wordt **Persoonlijke hotspot** geblokkeerd door de Intune-service. Als in een Intune-rapport de geslaagde uitvoering wordt weergegeven, weet u zeker dat het werkt, ook al wordt de instelling niet weergegeven in het beheerprofiel op het apparaat.

- **Regels voor mobiel gebruik (alleen beheerde apps)** : Met **Toestaan** worden de gegevenstypen gedefinieerd die beheerde apps kunnen gebruiken die zijn verbonden met een mobiel netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Uw opties zijn:
  - **Gebruik van mobiel dataverkeer blokkeren**: U kunt het gebruik van mobiel dataverkeer blokkeren voor **Alle beheerde apps** of u kunt **specifieke apps kiezen**.
  - **Gebruik van mobiel dataverkeer tijdens roaming blokkeren**: U kunt het gebruik van mobiel dataverkeer tijdens roaming blokkeren voor **Alle beheerde apps** of u kunt **specifieke apps** kiezen.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Wijzigingen in de instellingen voor het gebruik van mobiel gegevensverkeer voor apps**: **Blokkeren** voorkomt dat er wijzigingen kunnen worden aangebracht in de instellingen voor het gebruik van mobiel dataverkeer voor apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om te bepalen welke apps mobiel dataverkeer mogen gebruiken.
- **Wijzigingen in de instellingen voor mobiel gegevensverkeer**: Met **Blokkeren** voorkomt u dat gebruikers instellingen voor mobiel gegevensverkeer wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers wijzigingen aanbrengen.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

- **Aanpassing van Persoonlijke hotspot door gebruiker**: Met **Blokkeren** voorkomt u dat gebruikers de instelling voor persoonlijke hotspots wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers hun persoonlijke hotspot in- of uitschakelen.

  Als u deze instelling blokkeert en de instelling voor **Persoonlijke hotspot** blokkeert, wordt de persoonlijke hotspot uitgeschakeld.

  Deze functie is van toepassing op:  
  - iOS 12.2 en hoger
  - iPadOS 13.0 en hoger

- **Toevoegen aan Wi-Fi-netwerken die alleen configuratieprofielen gebruiken**: Selecteer **Vereisen** om af te dwingen dat apparaten alleen Wi-Fi-netwerken gebruiken die zijn ingesteld via Intune-configuratieprofielen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat apparaten gebruikmaken van andere Wi-Fi-netwerken.

  Als u deze optie instelt op **Vereist**, moet u ervoor zorgen dat het apparaat een Wi-Fi-profiel heeft. Als u geen Wi-Fi-profiel toewijst, kan deze instelling ertoe leiden dat apparaten geen verbinding kunnen maken met het internet. Met andere woorden: als dit profiel voor apparaatbeperkingen vóór een Wi-Fi-profiel is toegewezen, kan het apparaat mogelijk geen verbinding maken met internet.
  
  Als er geen verbinding kan worden gemaakt, moet u de registratie van het apparaat ongedaan maken en het apparaat opnieuw inschrijven met een Wi-Fi-profiel. Stel deze instelling vervolgens in op **Vereist** in een profiel voor apparaatbeperkingen en wijs het profiel toe aan het apparaat.

- **Wi-Fi altijd ingeschakeld**: Selecteer **Vereisen** om Wi-Fi ingeschakeld te houden in de app Instellingen. De optie kan niet worden uitgeschakeld in Instellingen of in het beheercentrum, ook niet als het apparaat zich in de vliegtuigmodus bevindt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om Wi-Fi in of uit te schakelen.

  Als u deze instelling configureert, wordt niet voorkomen dat gebruikers een Wi-Fi-netwerk selecteren.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

## <a name="connected-devices"></a>Verbonden apparaten

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Draagdetectie voor een gekoppelde Apple Watch**: Als u **Vereisen** selecteert, moet de gekoppelde Apple Watch de functie Draagdetectie gebruiken. Wanneer dit is vereist, worden op de Apple Watch geen meldingen weergegeven wanneer deze niet wordt gedragen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Wachtwoord voor koppelen voor uitgaande AirPlay-aanvragen vereisen**: Selecteer **Vereisen** om een wachtwoord voor koppelen te vereisen wanneer gebruikers AirPlay gebruiken om inhoud te streamen naar andere Apple-apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om AirPlay te gebruiken zonder een wachtwoord in te voeren.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **AirDrop**: Met **Blokkeren** voorkomt u dat gebruikers AirDrop op apparaten gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de functie AirDrop toestaat voor het uitwisselen van inhoud met apparaten in de omgeving.
- **Koppelen met Apple Watch**: Selecteer **Blokkeren** om koppeling met een Apple Watch te voorkomen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat apparaten worden gekoppeld aan een Apple Watch.
- **Aanpassing van Bluetooth**: Met **Blokkeren** voorkomt u dat gebruikers Bluetooth-instellingen op apparaten wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instellingen wijzigen.
- **Koppelen met een host om te bepalen met welke apparaten een iOS-/iPadOS-apparaat kan worden gekoppeld**: **Blokkeren**: voorkomt het koppelen met een host. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het koppelen met een host toestaat, zodat de beheerder kan bepalen aan welke apparaten een iOS-/iPadOS-apparaat kan worden gekoppeld.
- **AirPrint blokkeren**: Met **Blokkeren** voorkomt u dat gebruikers de functie AirPrint op apparaten gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers AirPrint gebruiken.
  - **Opslag van AirPrint-referenties in de Sleutelhanger blokkeren**: Met **Blokkeren** voorkomt u dat gebruikers de Sleutelhanger gebruiken om de gebruikersnaam en het wachtwoord op te slaan op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat de gebruikersnaam en het wachtwoord van AirPrint worden opgeslagen in de app Sleutelhanger.
  - **Een vertrouwd TLS-certificaat voor AirPrint vereisen**: Selecteer **Vereisen** om af te dwingen dat op apparaten vertrouwde certificaten worden gebruikt voor TLS-afdrukcommunicatie. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **iBeacon-detectie van AirPrint-printers blokkeren**: Met **Blokkeren** voorkomt u phishing met schadelijke AirPrint Bluetooth-bakens voor netwerkverkeer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het adverteren van AirPrint-printers op apparaten toestaat.
- **Het instellen van nieuwe apparaten in de buurt blokkeren**: Met **Blokkeren** wordt de vraag om nieuwe apparaten in de buurt in te stellen uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers wordt gevraagd verbinding te maken met andere Apple-apparaten in de buurt.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

- **Toegang tot bestanden op een USB-station**: Apparaten kunnen verbinding maken met een USB-schijf en bestanden die hierop staan openen. Met **Uitschakelen** voorkomt u dat het apparaat toegang heeft tot het USB-schijf in de Bestanden-app als er een USB-verbinding met het apparaat is gemaakt. Als u deze functie uitschakelt, kunnen gebruikers ook geen bestanden overdragen naar een USB-schijf die is verbonden met een iPad. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot een USB-schijf in de app Bestanden toestaat.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

## <a name="keyboard-and-dictionary"></a>Toetsenbord en woordenlijst

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Definities van woorden opzoeken**: Met **Blokkeren** voorkomt u dat gebruikers op apparaten een woord markeren en vervolgens de definitie ervan opzoeken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de toegang tot de functie Definitie opzoeken toestaat.
- **Tekstvoorspelling**: Met **Blokkeren** voorkomt u dat gebruikers toetsenborden met tekstvoorspelling gebruiken voor suggesties voor woorden die de gebruiker mogelijk wil invoeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Automatische correctie**: **Blokkeren**: blokkeert het gebruik van Autocorrectie. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem automatische correctie van verkeerd gespelde woorden op apparaten toestaat.
- **Spellingcontrole**: Met **Blokkeren** voorkomt u dat de spellingcontrole wordt uitgevoerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het gebruikerssysteem het gebruik van spellingcontrole op apparaten toestaat.
- **Sneltoetsen**: **Blokkeren** zorgt ervoor dat gebruikers geen sneltoetsen meer kunnen gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van sneltoetsen op apparaten toestaat.
- **Dicteren**: **Blokkeren** zorgt ervoor dat gebruikers geen spraakinvoer meer kunnen gebruiken om tekst in te voeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers dicteerinvoer gebruiken.
- **QuickPath**: Met **Blokkeren** voorkomt u dat gebruikers QuickPath kunnen gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om QuickPath te gebruiken, waarmee doorlopende invoer kan worden gebruikt op het toetsenbord van het apparaat. Gebruikers kunnen typen door over de toetsen te vegen om woorden te maken.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

## <a name="cloud-and-storage"></a>Cloud en opslag

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Versleutelde back-up**: Selecteer **Vereisen** om ervoor te zorgen dat back-ups van het apparaat moeten worden versleuteld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Beheerde apps synchroniseren met de cloud**: Met **Blokkeren** voorkomt u dat gegevens door Intune beheerde apps worden gesynchroniseerd met het iCloud-account van de gebruiker. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie van deze gegevens met iCloud toestaat.
- **Back-ups van Enterprise Book blokkeren**: Met **Blokkeren** voorkomt u dat gebruikers back-ups maken van bedrijfsboeken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers een back-up maken van deze boeken.
- **Synchronisatie van metagegevens van Enterprise Book blokkeren (notities en markeringen)** : Met **Blokkeren** voorkomt u dat notities en markeringen in Enterprise Book-boeken worden gesynchroniseerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie toestaat.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Photo Stream synchroniseren met iCloud**: **Blokkeren**: voorkomt dat met Photo Stream foto’s worden gesynchroniseerd met iCloud. Als u deze functie blokkeert, kan dit leiden tot gegevensverlies. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers **Mijn fotostream** inschakelen op hun apparaat om te synchroniseren met iCloud, en foto's beschikbaar hebben op alle apparaten van de gebruikers.
- **iCloud-fotobibliotheek**: **Blokkeren** schakelt het gebruik uit van de iCloud-fotobibliotheek voor het opslaan van foto's en video's in de cloud. Foto's die niet volledig naar apparaten zijn gedownload vanaf de iCloud-fotobibliotheek, worden van deze apparaten verwijderd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de iTunes-fotobibliotheek toestaat.
- **Gedeelde fotostream**: Met **Blokkeren** wordt het **delen van foto's via iCloud** uitgeschakeld op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem streaming van gedeelde foto's toestaat.
- **Handoff**: Met **Blokkeren** voorkomt u dat gebruikers aan het werk gaan op een iOS-/iPadOS-apparaat en vervolgens het werk voortzetten op een ander iOS-/iPadOS- of macOS-apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze Handoff toestaat.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Back-up naar iCloud**: Met **Blokkeren** voorkomt u dat gebruikers back-ups van het apparaat maken in iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers back-ups van apparaten maken in iCloud.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **iCloud-documentsynchronisatie blokkeren**: **Blokkeren**: voorkomt dat documenten en gegevens worden gesynchroniseerd met iCloud. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het synchroniseren van documenten en sleutelwaarden met uw iCloud-opslagruimte toestaat.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Synchronisatie van iCloud-sleutelhanger blokkeren**: **Blokkeren** schakelt de synchronisatie van aanmeldingsgegevens in de sleutelhanger naar iCloud uit. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze aanmeldingsgegevens synchroniseren.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

## <a name="autonomous-single-app-mode-asam"></a>Autonome modus voor één app (ASAM)

Gebruik deze instellingen om iOS-/iPadOS-apparaten te configureren om specifieke apps in de autonome modus voor één app (ASAM) uit te voeren. Als deze modus is geconfigureerd en gebruikers een van de geconfigureerde apps starten, wordt het apparaat vergrendeld voor deze app. Schakelen tussen apps/taken is uitgeschakeld totdat gebruikers de toegestane app verlaten.

Voeg bijvoorbeeld in een school- of universiteitsomgeving een app toe waarmee gebruikers een test kunnen uitvoeren op het apparaat. Of vergrendel het apparaat in de Bedrijfsportal-app totdat de gebruiker zich verifieert. Wanneer de acties van de app zijn voltooid door gebruikers, of wanneer u het beleid verwijdert, keert het apparaat terug naar de normale staat.

> [!NOTE]
> Niet alle apps ondersteunen de autonome modus voor één app. Als u een app in de autonome modus voor één app wilt plaatsen, is doorgaans een bundel-ID of een sleutel-/waardepaar geleverd door een app-configuratiebeleid vereist. Zie de [`autonomousSingleAppModePermittedAppIDs` beperking](https://developer.apple.com/documentation/devicemanagement/restrictions) in de MDM-documentatie van Apple voor meer informatie. Zie de documentatie van de leverancier voor meer informatie over de specifieke instellingen die nodig zijn voor de app die u wilt configureren.

Als u bijvoorbeeld Zoom Rooms wilt configureren in de autonome modus voor één app, geeft Zoom aan dat de bundel-id van `us.zoom.zpcontroller` moet worden gebruikt. In dit geval kunt u ook een wijziging aanbrengen in de Zoom-webportal. Zie voor meer informatie het [Zoom-helpcentrum](https://support.zoom.us/hc/articles/360021322632-Autonomous-Single-App-Mode-for-Zoom-Rooms-with-a-Third-Party-MDM).

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **App-naam**: Voer de naam in van de gewenste app.
- **App-bundel-id**: Voer de [bundel-id](bundle-ids-built-in-ios-apps.md) in van de gewenste app.
- **Toevoegen**: Selecteer deze optie om een lijst met uw apps te maken.

U kunt ook een CSV-bestand met de lijst met app-namen en de bijbehorende bundel-id’s **importeren**. Of **Exporteer** een bestaande lijst die de apps bevat.

## <a name="kiosk"></a>Kiosk

[Modus voor één app](https://support.apple.com/guide/mdm/mdm80a981/web) wordt aangeduid als kioskmodus in Intune.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **App uitvoeren in kioskmodus**: Selecteer het type apps dat u wilt uitvoeren in de kioskmodus. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat het besturingssysteem geen kioskinstellingen toepast. Het apparaat wordt niet uitgevoerd in de kioskmodus.
  - **Store-app**: Voer de URL in voor een app in de iTunes App Store.
  - **Beheerde app**: Selecteer een app die u eerder aan Intune hebt toegevoegd.
  - **Ingebouwde app**: Voer de [bundel-id](bundle-ids-built-in-ios-apps.md) in van de ingebouwde app.

- **Ondersteunende aanraking**: Selecteer **Vereisen** om de toegankelijkheidsinstelling Ondersteunende aanraking op apparaten te configureren. Deze functie helpt gebruikers bij schermbewegingen die mogelijk moeilijk zijn voor hen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Keer kleuren om**: Selecteer **Vereisen** om de toegankelijkheidsinstelling Keer kleuren om in te stellen, zodat gebruikers met een beperkt gezichtsvermogen de display kunnen wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Mono-audio**: Selecteer **Vereisen** om de toegankelijkheidsinstelling Mono-audio op het apparaat te configureren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Spraakbeheer**: Selecteer **Vereisen** om spraakbesturing op apparaten in te schakelen en gebruikers toe te staan om het besturingssysteem volledig te bedienen met behulp van Siri-opdrachten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem spraakbesturing uitschakelt.

  Deze instelling is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger
  
  > [!TIP]
  > Als u Line-Of-Business-apps beschikbaar hebt voor uw organisatie en **Spraakbesturing** niet gereed is op dag 0 als iOS 13.0 wordt uitgebracht, wordt u aangeraden deze instelling te laten staan op **Niet geconfigureerd**.

- **VoiceOver**: Selecteer **Vereisen** om de toegankelijkheidsinstelling VoiceOver tekst op het scherm hardop voor te laten lezen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Zoomen**: Selecteer **Vereisen** om de zoominstelling te configureren, zodat gebruikers kunnen inzoomen door het scherm aan te raken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Automatisch vergrendelen**: Met **Blokkeren** voorkomt u dat apparaten automatisch worden vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Schakelaar voor belsignaal**: Met **Blokkeren** wordt de schakelaar voor belsignaal (dempen) op apparaten uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Scherm draaien**: **Blokkeren** voorkomt dat de schermstand wordt gewijzigd wanneer gebruikers het apparaat draaien. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Schermsluimerknop**: Met **Blokkeren** wordt de knop voor slaapstand/ontwaken van het scherm uitgeschakeld op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Aanraken**: Met **Blokkeren** wordt het aanraakscherm uitgeschakeld op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het aanraakscherm gebruiken.
- **Volumeknoppen**: Met **Blokkeren** voorkomt u dat de volumeknoppen op apparaten worden gebruikt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de volumeknoppen toestaat.
- **Besturingselement voor ondersteunende aanraking**: Met **Toestaan** kunnen gebruikers de functie Ondersteunende aanraking gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.
- **Besturingselement voor kleuren omkeren**: Met **Toestaan** staat u aanpassingen in de functie Kleuren omkeren toe, zodat gebruikers deze functie kunnen aanpassen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.
- **Geselecteerde tekst uitspreken**: Selecteer **Toestaan** om de toegankelijkheidsinstellingen voor Selectie uitspreken op apparaten te configureren. Met deze functie wordt de tekst die gebruikers selecteren, hardop gelezen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.
- **Wijziging van spraakbesturing**: Met **Toestaan** stelt u gebruikers in staat om spraakbesturing te regelen op hun apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voorkomt dat gebruikers de status van spraakbesturing op hun apparaten kunnen wijzigen.

  Deze instelling is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

- **Besturingselement voor VoiceOver**: Selecteer **Toestaan**, zodat gebruikers de functie VoiceOver kunnen bijwerken, bijvoorbeeld hoe snel schermtekst hardop wordt gelezen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voice-overwijzigingen toestaat.
- **Besturingselement voor zoomen**: Hiermee zijn wijzigingen in het zoomniveau door gebruikers **toegestaan**. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem wijzigingen in het zoomniveau voorkomt.

> [!NOTE]
> Voordat u een iOS-/iPadOS-apparaat kunt configureren voor de kioskmodus, moet u het hulpprogramma Apple Configurator of het Device Enrollment Program van Apple gebruiken om apparaten in de supervisiemodus te plaatsen. Raadpleeg de handleiding van Apple voor het gebruik van het hulpprogramma Apple Configurator.
> Als de iOS-/iPadOS-app die u invoert, wordt geïnstalleerd nadat u het profiel hebt toegewezen, wordt de kioskmodus van het apparaat pas geactiveerd nadat het opnieuw is opgestart.

## <a name="domains"></a>Domains

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Niet-gemarkeerde e-maildomeinen** > **URL van e-maildomein**: Voeg een of meer URL's toe aan de lijst. Wanneer gebruikers een e-mail ontvangen die afkomstig is van een ander domein dan de domeinen die u invoert, wordt de e-mail in de iOS/iPadOS Mail-app gemarkeerd als niet-vertrouwd.

- **Beheerde webdomeinen** > **Webdomein-URL**: Voeg een of meer URL's toe aan de lijst. Wanneer documenten worden gedownload uit de domeinen die u invoert, worden ze beschouwd als beheerd. Deze instelling geldt alleen voor documenten die zijn gedownload met Safari.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Domeinen voor automatisch invullen van Safari-wachtwoorden** > **Domein-URL**: Voeg een of meer URL's toe aan de lijst. Gebruikers kunnen in deze lijst alleen webwachtwoorden van URL's opslaan. Deze instelling geldt alleen voor Safari en voor apparaten die onder supervisie staan. Als u geen URL's invoert, kunnen wachtwoorden van alle websites worden opgeslagen.

  Deze instelling is van toepassing op:  
  - iOS 9.3 en hoger
  - iPadOS 13.0 en hoger

## <a name="settings-that-require-supervised-mode"></a>Instellingen waarvoor de supervisiemodus is vereist

De supervisiemodus voor iOS/iPadOS kan alleen worden ingeschakeld tijdens de initiële installatie van het apparaat via het Device Enrollment Program van Apple of met behulp van Apple Configurator. Zodra de supervisiemodus is ingeschakeld, kunt u in Intune een apparaat configureren met de volgende functionaliteit:

- Kioskmodus (Modus voor één app): deze wordt 'App-vergrendeling' genoemd in de [Apple-documentatie voor ontwikkelaars](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf).
- Activeringsslot uitschakelen 
- Autonome modus voor één app 
- Webinhoudsfilter 
- Achtergrond en vergrendelingsscherm instellen 
- Stille app-push 
- Permanente VPN 
- Installatie van beheerde app exclusief toestaan 
- iBookstore 
- iMessages 
- Game Center 
- AirDrop 
- AirPlay 
- Koppelen aan host 
- Cloudsynchronisatie 
- Zoeken met Spotlight 
- Handoff 
- Apparaat wissen 
- Beperkingen voor gebruikersinterface 
- Installatie van configuratieprofielen per gebruikersinterface 
- Nieuws 
- Sneltoetsen 
- Wijzigingen van de wachtwoordcode 
- Wijzigingen van de apparaatnaam 
- Automatisch downloaden van apps 
- Apple Music 
- Binnenkomende e-mail 
- Koppelen aan Apple Watch 

> [!NOTE]
> Apple heeft bevestigd dat bepaalde instellingen worden verplaatst naar alleen onder supervisie in 2019. We raden u aan hiermee rekening te houden wanneer u deze instellingen gebruikt in plaats van dat u wacht totdat Apple deze migreert naar alleen onder supervisie:
>
> - App-installatie door eindgebruikers
> - App verwijderen
> - FaceTime
> - Safari
> - iTunes
> - Expliciete inhoud
> - iCloud-documenten en -gegevens
> - Games voor meerdere spelers
> - Game Center-vrienden toevoegen
> - Siri

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook apparaatfuncties en -instellingen beperken op [macOS](device-restrictions-macos.md)-apparaten.
