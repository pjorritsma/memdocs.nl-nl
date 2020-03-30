---
title: iOS-/iPadOS-apparaatinstellingen in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: U kunt instellingen voor iOS-/iPadOS-apparaten toevoegen, configureren of maken om functies te beperken, zoals wachtwoordvereisten instellen, het vergrendelingsscherm beheren, ingebouwde apps gebruiken, beperkte of goedgekeurde apps toevoegen, Bluetooth-apparaten verwerken, verbinding maken met de cloud voor back-up en opslag, de kioskmodus inschakelen, domeinen toevoegen, en bepalen hoe gebruikers de Safari-webbrowser kunnen gebruiken in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea0968d15572fa9c3bde1e4d133dcb8b4c980274
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/21/2020
ms.locfileid: "80087047"
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

- **Gebruiksgegevens delen**: **Blokkeren** voorkomt dat het apparaat diagnostische gegevens en gebruiksgegevens naar Apple verzendt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de verzending van deze gegevens toestaat.

- **Schermopname**: **Blokkeren** voorkomt dat er schermopnamen of schermafbeeldingen met het apparaat worden gemaakt. In iOS/iPadOS 9.0 en hoger worden hiermee ook schermopnamen geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de inhoud van het scherm vastleggen als een afbeelding of video.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Niet-vertrouwde TLS-certificaten**: **Blokkeren** voorkomt niet-vertrouwde TLS-certificaten (Transport Layer Security) op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem TLS-certificaten toestaat.
- **Draadloze PKI-updates blokkeren**: **Blokkeren** voorkomt dat uw gebruikers software-updates ontvangen tenzij het apparaat is verbonden met een computer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat een apparaat software-updates ontvangt zonder dat het verbonden is met een computer.
- **Bijhouden van advertenties beperken**: Selecteer **Beperken** om de advertentie-id van het apparaat uit te schakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem ingeschakeld blijft.
- **Bedrijfsapps vertrouwen**: Met **Blokkeren** wordt de knop **Ontwikkelaar vertrouwen** op het apparaat verwijderd in Instellingen > Algemeen > Profielen en apparaatbeheer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers laat kiezen of ze apps vertrouwen die niet zijn gedownload uit de App Store.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Aanpassing van instellingen voor het verzenden van diagnostische gegevens**: **Blokkeren** voorkomt dat de gebruiker de instelling voor verzending van diagnostische gegevens en app-analyse wijzigt in **Diagnostische gegevens en gebruik** (in apparaatinstellingen). Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze apparaatinstellingen wijzigen.

  Stel de instelling **Gebruiksgegevens delen** in op **Blokkeren** als u deze instelling wilt gebruiken.

  Deze functie is van toepassing op:  
  - iOS 9.3.2 en hoger
  - iPadOS 13.0 en hoger

- **Observatie van extern scherm met de app Classroom**: **Blokkeren** voorkomt dat het scherm op het apparaat op afstand kan worden bekeken met de app Apple Classroom. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het in het besturingssysteem is toegestaan dat het scherm wordt weergegeven in de app Apple Classroom.

  Stel de instelling **Schermopname** in op **Blokkeren** als u deze instelling wilt gebruiken.

  Deze functie is van toepassing op:  
  - iOS 9.3 en hoger
  - iPadOS 13.0 en hoger

- **Ongevraagde schermobservatie met de app Classroom**: Wanneer deze optie is ingesteld op **Toestaan**, kunnen docenten het scherm op de iOS-/iPadOS-apparaten van leerlingen/studenten observeren via de app Klaslokaal zonder dat de leerlingen/studenten dit weten. Op apparaten van leerlingen/studenten die zijn ingeschreven bij een cursus met behulp van de app Classroom, is toestemming voor de docent van deze cursus automatisch ingeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van deze functie niet toestaat.

  Stel de instelling **Schermopname** in op **Blokkeren** als u deze instelling wilt gebruiken.

- **Accountaanpassing**: Wanneer deze optie is ingesteld op **Blokkeren**, kunnen gebruikers de apparaatspecifieke instellingen niet bijwerken vanuit de app voor iOS-/iPadOS-instellingen. Gebruikers kunnen dan bijvoorbeeld geen nieuwe apparaataccounts maken, of de gebruikersnaam of het wachtwoord wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instellingen wijzigen.

  Deze functie geldt ook voor instellingen die toegankelijk zijn vanuit de app voor iOS-/iPadOS-instellingen, zoals E-mail, Contactpersonen, Agenda, Twitter, en meer. Deze functie geldt niet voor apps met accountinstellingen die niet kunnen worden geconfigureerd vanuit de app voor iOS-/iPadOS-instellingen, zoals de Microsoft Outlook-app.

- **Schermtijd**: **Blokkeren** voorkomt dat gebruikers hun eigen beperkingen in Schermtijd instellen (apparaatinstellingen). Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers apparaatbeperkingen (zoals ouderlijk toezicht, inhoudsbeperkingen en privacybeperkingen) configureren op het apparaat.

  Deze instelling heette eerst **Beperkingen inschakelen in de apparaatinstellingen**. Gevolgen van deze wijziging:  
  
  - iOS 11.4.1 en ouder: **Blokkeren** voorkomt dat eindgebruikers hun eigen beperkingen kunnen instellen bij de apparaatinstellingen. Het gedrag is hetzelfde. Er zijn geen wijzigingen voor gebruikers.
  - iOS 12.0 en nieuwer: **Blokkeren** voorkomt u dat gebruikers hun eigen **Schermtijd** kunnen instellen via de apparaatinstellingen (Instellingen > Algemeen > Schermtijd), waaronder inhouds- en privacybeperkingen. Apparaten die zijn geüpgraded naar iOS 12.0 krijgen het tabblad Beperkingen niet meer te zien bij de apparaatinstellingen (Instellingen > Algemeen > Apparaatbeheer > Beheerprofiel > Beperkingen). Deze instellingen vindt u onder **Schermtijd**.
  
- **Gebruik van de optie voor het wissen van alle inhoud en instellingen op het apparaat**: Selecteer **Blokkeren** zodat gebruikers de optie voor het wissen van alle inhoud en instellingen op het apparaat niet kunnen gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toegang geeft tot deze instellingen.
- **Apparaatnaam wijzigen**: Selecteer **Blokkeren**, zodat de apparaatnaam niet kan worden gewijzigd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de naam van het apparaat wijzigen.
- **Aanpassing van meldingsinstellingen**: Selecteer **Blokkeren**, zodat de instellingen voor meldingen niet kunnen worden gewijzigd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de meldingsinstellingen van het apparaat wijzigen.
- **Aanpassing van achtergrond**: Selecteer **Blokkeren**, zodat de achtergrond niet kan worden gewijzigd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de achtergrond van het apparaat wijzigen.
- **Wijzigingen in configuratieprofielen**: Selecteer **Blokkeren** om te voorkomen dat configuratieprofielen op het apparaat kunnen worden gewijzigd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers configuratieprofielen installeren.
- **Activeringsvergrendeling**: Selecteer **Toestaan** om Activeringsslot op iOS-/iPadOS-apparaten in te schakelen in de supervisiemodus. Met Activeringsslot kan een verloren of gestolen apparaat moeilijker opnieuw worden geactiveerd.
- **Verwijderen van app blokkeren**: **Blokkeren** voorkomt dat gebruikers apps kunnen verwijderen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers apps van het apparaat kunnen verwijderen.
- **USB-accessoires toestaan terwijl het apparaat is vergrendeld**: Met **Toestaan** kunnen USB-accessoires gegevens uitwisselen met een apparaat dat al meer dan een uur is vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de beperkte USB-modus niet bijwerkt op het apparaat, en dat USB-accessoires geen gegevens kunnen overdragen vanaf het apparaat als het langer dan een uur is vergrendeld.
- **Automatisch instellen van datum en tijd afdwingen**: Met **Vereisen** wordt het instellen van de datum en tijd automatisch afgedwongen op apparaten in de supervisiemodus. De tijdzone van het apparaat wordt bijgewerkt wanneer het apparaat mobiele verbindingen heeft of wanneer Wi-Fi met locatieservices is ingeschakeld voor het apparaat.
- **Studenten moeten toestemming vragen om de Classroom-cursus te verlaten**: Met **Vereisen** wordt afgedwongen dat leerlingen/studenten die zijn ingeschreven bij een niet-beheerde cursus met de app Klaslokaal, toestemming aan de docent vragen om de cursus te verlaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem niet afdwingt dat de leerling/student om toestemming vraagt.

  Deze functie is van toepassing op:  
  - iOS 11.3 en hoger
  - iPadOS 13.0 en hoger

- **De app Classroom toestaan om een app te vergrendelen en het apparaat te vergrendelen zonder te vragen**: Met **Inschakelen** kan de docent zonder tussenkomst van de student apps of het apparaat vergrendelen met behulp van de app Classroom. Apps vergrendelen betekent dat alleen door de docent gespecificeerde apps op het apparaat toegankelijk zijn. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voorkomt dat docenten zonder tussenkomst van de student apps of apparaten kunnen vergrendelen met behulp van de app Classroom.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

- **Automatisch lid worden van Classroom-klassen zonder te vragen**: Met **Inschakelen** kunt studenten automatisch deelnemen aan een klas in de app Classroom, zonder tussenkomst van de docent. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de docent informeert dat studenten willen deelnemen aan een klas in de app Classroom.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

- **Het maken van VPN's blokkeren**: Selecteer **Blokkeren** om te voorkomen dat gebruikers instellingen maken voor VPN-configuratie. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers VPN's maken op het apparaat.
- **eSIM-instellingen aanpassen**: Met **Blokkeren** voorkomt u dat gebruikers een mobiel abonnement kunnen verwijderen uit of toevoegen aan de eSIM op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instellingen wijzigen.

  Deze functie is van toepassing op:  
  - iOS 12.1 en hoger
  - iPadOS 13.0 en hoger

- **Software-updates uitstellen**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem software-updates op het apparaat weergeeft wanneer Apple deze heeft uitgegeven. Als Apple bijvoorbeeld op een bepaalde datum een iOS-/iPadOS-update uitbrengt, wordt deze update rond de releasedatum automatisch weergegeven op het apparaat.

  Met **Inschakelen** kunt u het weergeven van software-updates op apparaten uitstellen, van 0-90 dagen. Deze instelling bepaalt niet wanneer updates wel of niet worden geïnstalleerd. 

  - **De zichtbaarheid van software-updates vertragen**: Voer een waarde in tussen 0 en 90 dagen. Wanneer de vertraging verloopt, krijgen gebruikers een melding om een update uit te voeren naar de vroegste versie van het besturingssysteem die beschikbaar was toen de vertraging werd geactiveerd.

    Als iOS 12.a bijvoorbeeld beschikbaar komt op **1 januari** en **Zichtbaarheid vertragen** is ingesteld op **5 dagen**, wordt iOS 12.a niet als beschikbare update weergeven op apparaten van de gebruiker. Op de **zesde dag** na de release komt deze update beschikbaar en kunnen gebruikers deze installeren.

    Deze instelling is van toepassing op:  
    - iOS 11.3 en hoger
    - iPadOS 13.0 en hoger

## <a name="password"></a>Wachtwoord

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Wachtwoord**: **Vereisen** dat gebruikers een wachtwoord invoeren voor toegang tot het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat kunnen gebruiken zonder een wachtwoord in te voeren.

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

- **Vereist wachtwoordtype**: Selecteer het type wachtwoord dat is vereist voor uw organisatie. Uw opties zijn:
  - **Standaardwaarde apparaat**
  - **Numeriek**
  - **Alfanumeriek**
- **Het aantal niet-alfanumerieke tekens in het wachtwoord**: Geef het aantal symbooltekens op, zoals `#` of `@`, dat het wachtwoord moet bevatten.

- **Minimale wachtwoordlengte**: Voer de minimale lengte in die een gebruiker moet invoeren, tussen 4 en 14 tekens. Voer een lengte tussen 4 en 6 tekens in voor door de gebruiker ingeschreven apparaten.
  
  > [!NOTE]
  > Voor apparaten die door de gebruiker zijn ingeschreven, kunnen gebruikers een pincode van meer dan 6 cijfers instellen. Er worden echter niet meer dan 6 cijfers afgedwongen op het apparaat. Stel dat een beheerder de minimale lengte instelt op `8`. Gebruikers hoeven op apparaten die door gebruikers zijn ingeschreven alleen een 6-cijferig pincode in te stellen. Intune dwingt geen pincode van meer dan 6 cijfers af op door gebruikers geregistreerde apparaten.

- **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal mislukte aanmeldingen in dat is toegestaan voordat het apparaat wordt gewist (tussen 4 en 11).
  
  iOS/iPadOS heeft ingebouwde beveiliging die van invloed kan zijn op deze instelling. iOS/iPadOS kan bijvoorbeeld het activeren van beleid vertragen, afhankelijk van het aantal mislukte aanmeldingen. Ook kan het besturingssysteem het herhaaldelijk invoeren van dezelfde toegangscode als één poging beschouwen. De [iOS-/iPadOS-beveiligingshandleiding](https://www.apple.com/business/site/docs/iOS_Security_Guide.pdf) van Apple (opent de website van Apple) is een goede bron en biedt meer specifieke informatie over wachtwoordcodes.
  
- **Maximum aantal minuten na schermvergrendeling voordat wachtwoord is vereist**<sup>1</sup>: Geef op hoe lang het apparaat inactief moet zijn voordat gebruikers hun wachtwoord opnieuw moeten invoeren. Als de ingevoerde tijd langer is dan de tijd die is ingesteld op het apparaat, wordt de door u ingevoerde tijd genegeerd. Wordt ondersteund op apparaten met iOS 8.0+ en iPadOS 13.0+.

- **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**<sup>1</sup>: Voer het maximale aantal minuten van inactiviteit in dat is toegestaan op het apparaat totdat het scherm wordt vergrendeld.

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

- **Wachtwoordverlooptijd (dagen)** : Geef op na hoeveel dagen het wachtwoord voor het apparaat moet worden gewijzigd.
- **Wachtwoorden niet opnieuw gebruiken**: Voer het aantal nieuwe wachtwoorden in dat moet worden gebruikt voordat een oud wachtwoord opnieuw kan worden gebruikt.
- **Ontgrendelen met Touch ID en Face ID**: **Blokkeren** voorkomt het gebruik van een vingerafdruk of gezichtsherkenning om het apparaat te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van deze methoden.

  Door deze instelling te blokkeren, voorkomt u ook dat het apparaat wordt ontgrendeld met behulp van Face ID-verificatie.

  Face ID is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Aanpassing van wachtwoordcode**: **Blokkeren** voorkomt dat de wachtwoordcode kan worden gewijzigd, toegevoegd of verwijderd. Als deze functie is geblokkeerd worden wijzigingen in de wachtwoordcodebeperkingen genegeerd op apparaten in de supervisiemodus. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat wachtwoordcodes worden toegevoegd, gewijzigd of verwijderd.

  - **Aanpassing van Touch ID en Face ID**: **Blokkeren** voorkomt dat gebruikers Touch ID-vingerafdrukken en Face ID kunnen wijzigen, toevoegen of verwijderen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de TouchID-vingerafdrukken en Face ID op het apparaat bijwerken.

    Als u deze instelling blokkeert, kunnen gebruikers ook geen Face ID-verificatie meer wijzigen, toevoegen of verwijderen.

    Face ID is van toepassing op:  
    - iOS 11.0 en hoger
    - iPadOS 13.0 en hoger

- **Automatisch wachtwoorden invullen blokkeren**: **Blokkeren** voorkomt dat de functie Wachtwoorden automatisch invullen kan worden gebruikt in iOS/iPadOS. Als u **Blokkeren** kiest, heeft dat ook de volgende gevolgen:

  - Gebruikers wordt niet meer gevraagd om een wachtwoord te gebruiken dat is opgeslagen in Safari of in een app.
  - Automatische sterke wachtwoorden zijn uitgeschakeld en gebruikers krijgen geen suggesties voor sterke wachtwoorden.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functies toestaat.

- **Aanvragen voor wachtwoordnabijheid blokkeren**: Selecteer **Blokkeren** zodat het apparaat van een gebruiker geen wachtwoorden aanvraagt van apparaten in de omgeving. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze wachtwoordaanvragen toestaat.
- **Wachtwoorden delen blokkeren**: Selecteer **Blokkeren** om te voorkomen dat wachtwoorden via AirDrop tussen apparaten worden gedeeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het delen van wachtwoorden toestaat.
- **Touch ID- of Face ID-verificatie vereisen voor het automatisch invullen van wachtwoorden of creditcardgegevens**: Als **Vereisen** is ingesteld, moeten gebruikers zich verifiëren via Touch ID of Face ID voordat wachtwoorden of creditcardgegevens automatisch kunnen worden ingevuld in Safari en andere apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze functie beheren in de apparaatinstellingen.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger
  
<sup>1</sup>Wanneer u de instellingen **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld** en **Maximum aantal minuten waarna een wachtwoord voor het vergrendelde scherm is vereist** configureert, worden deze opeenvolgend toegepast. Als u de waarde voor beide instellingen bijvoorbeeld instelt op **vijf** minuten, wordt het scherm na vijf minuten automatisch uitgeschakeld en wordt het apparaat vergrendeld na nog eens vijf minuten. Als gebruikers het scherm echter handmatig uitschakelen, wordt de tweede instelling onmiddellijk toegepast. Als gebruikers in hetzelfde voorbeeld het scherm hebben uitgeschakeld, wordt het apparaat vijf minuten later vergrendeld.

## <a name="locked-screen-experience"></a>Vergrendeld scherm

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Toegang tot Beheercentrum wanneer het apparaat is vergrendeld**: **Blokkeren** voorkomt de toegang tot de app Beheercentrum zolang het apparaat is vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de app Beheercentrum openen terwijl het apparaat is vergrendeld.
- **Meldingen terwijl het apparaat is vergrendeld**: Selecteer **Blokkeren** om de toegang tot meldingen te blokkeren terwijl het apparaat is vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers toegang hebben tot meldingen zonder dat ze het apparaat hoeven te ontgrendelen.
- **De weergave Vandaag wanneer het apparaat vergrendeld**: Selecteer **Blokkeren** om de toegang tot de weergave Vandaag te blokkeren terwijl het apparaat is vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de weergave Vandaag kunnen bekijken terwijl het apparaat is vergrendeld.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Wallet-meldingen terwijl het apparaat is vergrendeld**: Selecteer **Blokkeren** om de toegang tot de app Wallet te blokkeren terwijl het apparaat is vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de Wallet-app kunnen bekijken terwijl het apparaat is vergrendeld.

## <a name="app-store-doc-viewing-gaming"></a>App Store, documenten bekijken, gamen

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Zakelijke documenten weergeven in niet-beheerde apps**: Selecteer **Blokkeren** om te voorkomen dat zakelijke documenten in niet-beheerde apps worden weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat zakelijke documenten worden weergegeven in elke willekeurige app. Voorbeeld: u wilt voorkomen dat gebruikers bestanden uit de OneDrive-app opslaan in Dropbox. Configureer deze instelling als **Blokkeren**. Nadat het apparaat het beleid heeft ontvangen (bijvoorbeeld nadat het opnieuw is opgestart), kunnen er geen bestanden meer worden opgeslagen.


  > [!NOTE]
  > Als deze instelling wordt geblokkeerd, worden ook toetsenborden van derden geblokkeerd die vanuit de App Store zijn geïnstalleerd.

  - **Toestaan dat niet-beheerde apps contactpersonen lezen in beheerde accounts voor contactpersonen**: Als deze instelling is ingesteld op **Toestaan**, kunnen niet-beheerde apps (zoals de ingebouwde iOS-/iPadOS-app Contacten) de contactgegevens van beheerde apps lezen en openen, met inbegrip van de mobiele Outlook-app. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem lezen, inclusief het verwijderen van dubbele contactpersonen, uit de ingebouwde app Contacten op het apparaat voorkomt.  
  
    Met deze instelling wordt het lezen van contactgegevens toegestaan of voorkomen. Met de service wordt de synchronisatie van contactpersonen tussen de apps niet beheerd.
  
    Als u deze instelling wilt gebruiken, stelt u **Zakelijke documenten weergeven in niet-beheerde apps** in op **Blokkeren**.

  Voor meer informatie over deze twee instellingen en de invloed ervan op het synchroniseren van geëxporteerde contactpersonen in Outlook voor iOS/iPadOS raadpleegt u [Ondersteuningstip: Aangepaste profielinstellingen in Intune gebruiken voor de systeemeigen contactpersonen-app in iOS/iPadOS](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Use-Intune-custom-profile-settings-with-the-iOS/ba-p/298453).

- **AirDrop behandelen als een onbeheerd doel**: Wanneer deze optie is ingesteld op **Vereisen**, wordt AirDrop beschouwd als een onbeheerde bestemming. Het zorgt ervoor dat via beheerde apps geen gegevens meer kunnen worden verzonden met behulp van AirDrop. 
- **Niet-zakelijke documenten weergeven in zakelijke apps**: Met **Blokkeren** voorkomt u dat niet-zakelijke documenten in zakelijke apps worden weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voorkomt dat documenten worden weergegeven in zakelijke beheerde apps.

  **Blokkeren** voorkomt ook de synchronisatie van geëxporteerde contactpersonen in Outlook voor iOS/iPadOS. Voor meer informatie raadpleegt u [Ondersteuningstip: Synchronisatie van contactpersonen in Outlook voor iOS/iPadOS inschakelen met MDM-besturingselementen in iOS 12](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Enabling-Outlook-iOS-Contact-Sync-with-iOS12-MDM/ba-p/298453).

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **iTunes Store-wachtwoord voor alle aankopen vereisen**: **Vereis** dat gebruikers het Apple ID-wachtwoord invoeren voor elke in-app- of iTunes-aankoop. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem aankopen toestaat zonder dat elke keer om het wachtwoord wordt gevraagd.
- **In-app aankopen**: **Blokkeren** voorkomt in-app aankopen in de Store. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers vanuit een actieve app aankopen doen in de Store.
- **Inhoud uit Book Store met de markering Erotisch downloaden**: **Blokkeren** voorkomt dat gebruikers media downloaden uit de iBooks Store die zijn aangemerkt als Erotisch. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers boeken downloaden uit de categorie Erotisch.
- **Toestaan dat beheerde apps contactpersonen doorgeven aan niet-beheerde accounts voor contactpersonen**: Als deze optie is ingesteld op **Toestaan**, kunnen beheerde apps (zoals de mobiele Outlook-app) contactinformatie, inclusief zakelijke contactpersonen, opslaan in of synchroniseren met de ingebouwde iOS-/iPadOS-app Contacten op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voorkomt dat beheerde apps contactgegevens opslaan op of synchroniseren met de ingebouwde app Contacten op het iOS-/iPadOS-apparaat.
  
  Als u deze instelling wilt gebruiken, stelt u **Zakelijke documenten weergeven in niet-beheerde apps** in op **Blokkeren**.

- **Regio voor restricties**: Selecteer de regio voor restricties die u wilt gebruiken voor toegestane downloads. En kies vervolgens de toegestane beoordelingen voor **Films**, **Tv-programma's** en **Apps**.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **App Store**: Selecteer **Blokkeren** om de toegang tot de App Store te blokkeren op apparaten in de supervisiemodus. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang toestaat.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

  - **Apps installeren via de App Store**: Selecteer **Blokkeren** om de App Store te blokkeren op het startscherm van het apparaat. Gebruikers kunnen iTunes nog steeds gebruiken of met Apple Configurator apps installeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de App Store op het startscherm toestaat.
  - **Automatisch downloaden van apps**: **Blokkeren** voorkomt dat apps die zijn gekocht op andere apparaten, automatisch worden gedownload. Dit is niet van invloed op updates voor bestaande apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om apps die zijn gekocht op andere iOS-/iPadOS-apparaten, te downloaden op het apparaat.

- **Expliciete muziek-, podcast- of nieuwsinhoud op iTunes**: **Blokkeren** voorkomt expliciete muziek-, podcast- of nieuwsinhoud in iTunes. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het apparaat toegang geeft tot inhoud voor volwassenen in de Store.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Game Center-vrienden toevoegen**: Met **Blokkeren** voorkomt u dat gebruikers vrienden kunnen toevoegen in Game Center. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers vrienden kunnen toevoegen in Game Center.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Game Center**: Met **Blokkeren** blokkeert u het gebruik van de Game Center-app. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het gebruikerssysteem het gebruik van de app Game Center op het apparaat toestaat.
- **Games voor meerdere spelers**: **Blokkeren** voorkomt het spelen van games voor meerdere spelers. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers games voor meerdere spelers op het apparaat spelen.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Toegang tot netwerkstation in de app Bestanden**: Met behulp van het Server Message Block-protocol (SMB) kunnen apparaten toegang krijgen tot bestanden of andere resources op een netwerkserver. Met **Uitschakelen** voorkomt u toegang tot bestanden op een netwerkstation via SMB. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang toestaat.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

## <a name="built-in-apps"></a>Ingebouwde apps

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Siri**: Met **Blokkeren** voorkomt u toegang tot Siri. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het gebruikerssysteem het gebruik van de spraakassistent Siri op het apparaat toestaat.
  - **Siri als het apparaat is vergrendeld**: **Blokkeren** voorkomt de toegang tot Siri zolang het apparaat is vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het gebruikerssysteem het gebruik van de spraakassistent Siri op het apparaat toestaat wanneer het apparaat is vergrendeld.

- **Waarschuwingen voor fraude in Safari**: Als u **Vereisen** selecteert, worden fraudewaarschuwingen weergegeven in de webbrowser op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Spotlight-zoekacties voor de weergave van resultaten op internet**: Met **Blokkeren** zorgt u ervoor dat Spotlight geen resultaten meer retourneert na een zoekopdracht op internet. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat Zoeken met Spotlight verbinding maakt met internet om zoekresultaten te verstrekken.

- **Safari-cookies**: Kies hoe cookies moeten worden verwerkt op het apparaat. Uw opties zijn:
  - Toestaan
  - Alle cookies blokkeren
  - Cookies van bezochte websites toestaan
  - Cookies van huidige website toestaan

- **Safari JavaScript**: Met **Blokkeren** voorkomt u dat Java-scripts worden uitgevoerd in de browser op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem Java-scripts toestaat.

- **Safari-pop-ups**: Als u **Blokkeren** selecteert, wordt het gebruik van de pop-upblokkering in de webbrowser uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de pop-upblokkering toestaat.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Camera**: **Blokkeren** voorkomt toegang tot de camera op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot de camera van het apparaat toestaat.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

  - **FaceTime**: Met **Blokkeren** voorkomt u toegang tot de app FaceTime. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot de app FaceTime toestaat op het apparaat.

    Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Siri-filter voor scheldwoorden**: Met **Vereisen** voorkomt u dat grove taal wordt gedicteerd of uitgesproken door Siri.

  Stel de instelling **Siri** in op **Blokkeren** om deze instelling te gebruiken.

- **Query's uitvoeren met Siri op door gebruikers gegenereerde inhoud op internet**: Selecteer **Blokkeren** om te voorkomen dat Siri toegang tot websites krijgt om vragen te beantwoorden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat Siri toegang heeft tot door gebruikers gegenereerde inhoud op internet.

  Stel de instelling **Siri** in op **Blokkeren** om deze instelling te gebruiken.

- **Apple News**: **Blokkeren** voorkomt toegang tot de app Apple News op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app Apple News toestaat.
- **iBooks Store**: Selecteer **Blokkeren** om toegang tot de Book Store op het apparaat te blokkeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om boeken te zoeken en te kopen in de iBooks Store.
- **De app Berichten op het apparaat**: Met **Blokkeren** voorkomt u dat gebruikers de app Berichten gebruiken voor iMessage. Als het apparaat tekstberichten ondersteunt, kunnen gebruikers nog steeds tekstberichten verzenden en ontvangen met behulp van sms. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de Berichten-app toestaat om berichten via internet te verzenden en te lezen.
- **Podcasts**: Selecteer **Blokkeren** om toegang tot de app Podcasts op het apparaat te blokkeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de Podcasts-app toestaat.
- **De service Music**: Met **Blokkeren** keert u terug naar de klassieke modus van de app Muziek en wordt de Muziek-service uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app Apple Music toestaat.
- **iTunes Radio-service**: Selecteer **Blokkeren** om toegang tot de app iTunes Radio op het apparaat te blokkeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de app iTunes Radio toestaat.
- **iTunes Store**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem iTunes op de apparaten toestaat. Met **Blokkeren** voorkomt u dat gebruikers iTunes kunnen gebruiken op het apparaat.

  Deze functie is van toepassing op:  
  - iOS 4.0 en hoger
  - iPadOS 13.0 en hoger

- **Zoek mijn iPhone**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van deze 'Zoek mijn'-app-functie toestaat om de globale locatie van het apparaat te verkrijgen. Met **Blokkeren** voorkomt u het gebruik van deze functie in de Zoek mijn-app. 

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

- **Zoek mijn vrienden**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de 'Zoek mijn'-app-functie toestaat om familie en vrienden te zoeken via een Apple-apparaat of via iCloud.com. Met **Blokkeren** voorkomt u het gebruik van deze functie in de Zoek mijn-app.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

- **Wijzigingen in de instellingen van de app Zoek mijn vrienden**: Met **Blokkeren** voorkomt u wijzigingen in de instellingen van de app Zoek vrienden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de instellingen van de app Zoek mijn vrienden wijzigen.

- **Spotlight-zoekacties voor de weergave van resultaten op internet**: Met **Blokkeren** zorgt u ervoor dat Spotlight geen resultaten meer retourneert na een zoekopdracht op internet. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat Zoeken met Spotlight verbinding maakt met internet om zoekresultaten te verstrekken.

- **Het verwijderen van systeem-apps van apparaat blokkeren**: Selecteer **Blokkeren** om te voorkomen dat systeem-apps van het apparaat worden verwijderd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers systeem-apps kunnen verwijderen.

- **Safari**: Selecteer **Blokkeren** om te voorkomen dat gebruikers de Safari-browser op het apparaat kunnen gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de Safari-browser gebruiken.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Automatisch invullen in Safari**: Selecteer **Blokkeren** om de functie Automatisch invullen in Safari op het apparaat uit te schakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat de instellingen voor automatisch doorvoeren te wijzigen in de webbrowser.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

## <a name="restricted-apps"></a>Beperkte apps

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Lijst met typen beperkte apps**: Hiermee maakt u een lijst met apps die gebruikers niet mogen installeren of gebruiken. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Gebruikers hebben toegang tot apps die u toewijst en tot ingebouwde apps.
  - **Niet-toegestane apps**: Apps die niet worden beheerd in Intune waarvan u niet wilt dat deze op het apparaat worden geïnstalleerd. Gebruikers kunnen geen verboden apps installeren. Maar als een gebruiker een app uit deze lijst installeert, wordt deze in Intune gerapporteerd.
  - **Goedgekeurde apps**: Apps die gebruikers mogen installeren. Gebruikers mogen geen apps installeren die niet worden vermeld. Apps die worden beheerd door Intune, zijn automatisch toegestaan. Er wordt niet voorkomen dat gebruikers een app installeren die niet in de goedgekeurde lijst wordt vermeld. Maar als dat wel het geval is, wordt dit in Intune gerapporteerd.

Als u apps wilt toevoegen aan deze lijsten, kunt u:

- De App Store-URL van de gewenste iTunes-app **toevoegen**. Voer bijvoorbeeld `https://itunes.apple.com/us/app/work-folders/id950878067?mt=8` of `https://apps.apple.com/us/app/work-folders/id950878067?mt=8` in om de app Microsoft Werkmappen toe te voegen.

  Als u de URL van een app wilt vinden, opent u de iTunes App Store en gaat u naar de app. Zoek bijvoorbeeld naar `Microsoft Remote Desktop` of `Microsoft Word`. Selecteer de app en kopieer de URL.

  U kunt ook iTunes gebruiken om de app te zoeken en vervolgens de taak **Koppeling kopiëren** gebruiken om de URL van de app te krijgen.

- **Importeer** een CSV-bestand met details van de app, waaronder de URL. Gebruik de notatie `<app url>, <app name>, <app publisher>`. Of een bestaande lijst **exporteren** die de beperkte apps bevat in dezelfde indeling.

> [!IMPORTANT]
> Apparaatprofielen die instellingen voor beperkte apps gebruiken, moeten worden toegewezen aan groepen gebruikers.

## <a name="show-or-hide-apps"></a>Apps weergeven of verbergen

Van toepassing op apparaten met iOS 9.3+ en iPadOS 13.0+.

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

Opmerking vereist voor dataroaming (tip of belangrijke opmerking om verwarring bij klanten te voorkomen): Deze instelling wordt niet weergegeven in het beheerprofiel van het doelapparaat. Dat komt doordat deze instelling wordt behandeld als een actie voor een extern apparaat. Elke keer dat de status van gegevensroaming op het apparaat wordt gewijzigd, wordt deze weer geblokkeerd door de Intune-service. Hoewel de optie zich niet in het beheerprofiel bevindt, werkt het als er een succesvolle uitvoering wordt weergegeven in de rapportage in de beheerconsole. 
- **Gegevensroaming**: **Blokkeren** voorkomt dataroaming via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem dataroaming toestaat wanneer het apparaat verbinding heeft met een mobiel netwerk.

  > [!IMPORTANT]
  > Deze instelling wordt behandeld als een actie op een extern apparaat. Deze instelling wordt dus niet weergegeven in het beheerprofiel op het apparaat. Steeds wanneer de status van de gegevensroaming op het apparaat wordt gewijzigd, wordt **Gegevensroaming** geblokkeerd door de Intune-service. Als in een Intune-rapport de geslaagde uitvoering wordt weergegeven, weet u zeker dat het werkt, ook al wordt de instelling niet weergegeven in het beheerprofiel op het apparaat.

- **Op de achtergrond ophalen tijdens roaming**: Met **Blokkeren** voorkomt u dat gegevens tijdens roaming op de achtergrond kunnen worden opgehaald via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat het apparaat gegevens, zoals e-mail, ophaalt tijdens roaming op een mobiel netwerk.
- **Voicedialing**: **Blokkeren** voorkomt dat gebruikers de functie Voicedialing op het apparaat kunnen gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem Nummer inspreken op het apparaat toestaat.
- **Gespreksroaming**: **Blokkeren** voorkomt spraakroaming via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem spraakroaming toestaat wanneer het apparaat verbinding heeft met een mobiel netwerk.
- **Persoonlijke hotspot**: **Blokkeren** schakelt de persoonlijke hotspot op apparaten uit bij elke apparaatsynchronisatie. Mogelijk is deze instelling niet compatibel met bepaalde providers. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de configuratie van de persoonlijke hotspot behoudt als de standaardwaarde die is ingesteld door gebruikers.

  > [!IMPORTANT]
  > Deze instelling wordt behandeld als een actie op een extern apparaat. Deze instelling wordt dus niet weergegeven in het beheerprofiel op het apparaat. Steeds wanneer de status van de persoonlijke hotspot op het apparaat wordt gewijzigd, wordt **Persoonlijke hotspot** geblokkeerd door de Intune-service. Als in een Intune-rapport de geslaagde uitvoering wordt weergegeven, weet u zeker dat het werkt, ook al wordt de instelling niet weergegeven in het beheerprofiel op het apparaat.

- **Regels voor mobiel gebruik (alleen beheerde apps)** : Definieer de gegevenstypen die beheerde apps kunnen gebruiken die zijn verbonden met een mobiel netwerk. Uw opties zijn:
  - **Gebruik van mobiel dataverkeer blokkeren**: U kunt het gebruik van mobiel dataverkeer blokkeren voor **Alle beheerde apps** of u kunt **specifieke apps kiezen**.
  - **Gebruik van mobiel dataverkeer tijdens roaming blokkeren**: U kunt het gebruik van mobiel dataverkeer tijdens roaming blokkeren voor **Alle beheerde apps** of u kunt **specifieke apps** kiezen.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Wijzigingen in de instellingen voor het gebruik van mobiel gegevensverkeer voor apps**: **Blokkeren** voorkomt dat er wijzigingen kunnen worden aangebracht in de instellingen voor het gebruik van mobiel dataverkeer voor apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om te bepalen welke apps mobiel dataverkeer mogen gebruiken.
- **Wijzigingen in de instellingen voor mobiel gegevensverkeer**: Met **Blokkeren** voorkomt u dat gebruikers instellingen voor mobiel gegevensverkeer wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers wijzigingen aanbrengen.

  Deze functie is van toepassing op:  
  - iOS 11.0 en hoger
  - iPadOS 13.0 en hoger

- **Aanpassing van Persoonlijke hotspot door gebruiker**: Als u deze optie instelt op **Blokkeren**, kunnen gebruikers de instelling voor persoonlijke hotspot niet wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers hun persoonlijke hotspot in- of uitschakelen.

  Als u deze instelling blokkeert en de instelling voor **Persoonlijke hotspot** blokkeert, wordt de persoonlijke hotspot uitgeschakeld.

  Deze functie is van toepassing op:  
  - iOS 12.2 en hoger
  - iPadOS 13.0 en hoger

- **Toevoegen aan Wi-Fi-netwerken die alleen configuratieprofielen gebruiken**: Met **Vereisen** dwingt u af dat het apparaat alleen Wi-Fi-netwerken gebruikt die zijn ingesteld via Intune-configuratieprofielen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat het apparaat gebruikmaakt van andere Wi-Fi-netwerken.

  Als u deze optie instelt op **Vereist**, moet u ervoor zorgen dat het apparaat een Wi-Fi-profiel heeft. Als u geen Wi-Fi-profiel toewijst, kan deze instelling ertoe leiden dat het apparaat geen verbinding kan maken met internet. Met andere woorden: als dit profiel voor apparaatbeperkingen vóór een Wi-Fi-profiel is toegewezen, kan het apparaat mogelijk geen verbinding maken met internet.
  
  Als er geen verbinding kan worden gemaakt, moet u de registratie van het apparaat ongedaan maken en het apparaat opnieuw inschrijven met een Wi-Fi-profiel. Stel deze instelling vervolgens in op **Vereist** in een profiel voor apparaatbeperkingen en wijs het profiel toe aan het apparaat.

- **Wi-Fi altijd ingeschakeld**: Als de instelling is ingesteld op **Vereist**, blijft Wi-Fi ingeschakeld in de app Instellingen. De optie kan niet worden uitgeschakeld in Instellingen of in het beheercentrum, ook niet als het apparaat zich in de vliegtuigmodus bevindt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om Wi-Fi in of uit te schakelen.

  Als u deze instelling configureert, wordt niet voorkomen dat gebruikers een Wi-Fi-netwerk selecteren.

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

## <a name="connected-devices"></a>Verbonden apparaten

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Draagdetectie voor een gekoppelde Apple Watch**: Als u **Vereisen** selecteert, moet de gekoppelde Apple Watch de functie Draagdetectie gebruiken. Wanneer dit is vereist, worden op de Apple Watch geen meldingen weergegeven wanneer deze niet wordt gedragen. 

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Wachtwoord voor koppelen voor uitgaande AirPlay-aanvragen vereisen**: **Vereis** een wachtwoord voor koppelen wanneer gebruikers AirPlay gebruiken om inhoud te streamen naar andere Apple-apparaten. Met **Niet geconfigureerd** (standaard) kunnen gebruikers inhoud streamen met AirPlay zonder een wachtwoord in te voeren.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **AirDrop**: Selecteer **Blokkeren** om het gebruik van AirDrop op het apparaat te voorkomen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de functie AirDrop toestaat voor het uitwisselen van inhoud met apparaten in de omgeving.
- **Koppelen met Apple Watch**: Selecteer **Blokkeren** om koppeling met een Apple Watch te voorkomen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat het apparaat wordt gekoppeld aan een Apple Watch.
- **Aanpassing van Bluetooth**: **Blokkeren** zorgt ervoor dat de gebruikers geen Bluetooth-instellingen op het apparaat kunnen wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instellingen wijzigen.
- **Koppelen met een host om te bepalen met welke apparaten een iOS-/iPadOS-apparaat kan worden gekoppeld**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het koppelen met een host toestaat, zodat de beheerder kan bepalen aan welke apparaten een iOS-/iPadOS-apparaat kan worden gekoppeld. **Blokkeren**: voorkomt het koppelen met een host.
- **AirPrint blokkeren**: **Blokkeren** voorkomt het gebruik van de functie AirPrint op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers AirPrint gebruiken.
  - **Opslag van AirPrint-referenties in de Sleutelhanger blokkeren**: Met **Blokkeren** voorkomt u het gebruik van de Sleutelhanger om de gebruikersnaam en het wachtwoord op te slaan op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat de gebruikersnaam en het wachtwoord van AirPrint worden opgeslagen in de app Sleutelhanger.
  - **Een vertrouwd TLS-certificaat voor AirPrint vereisen**: Met **Vereisen** dwingt u af dat op het apparaat vertrouwde certificaten worden gebruikt voor TLS-afdrukcommunicatie.
  - **iBeacon-detectie van AirPrint-printers blokkeren**: Met **Blokkeren** voorkomt u phishing met schadelijke AirPrint Bluetooth-bakens voor netwerkverkeer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het adverteren van AirPrint-printers op het apparaat toestaat.
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

- **Definities van woorden opzoeken**: Met **Blokkeren** voorkomt u dat de gebruiker een woord markeert en vervolgens de definitie ervan opzoekt op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de toegang tot de functie Definitie opzoeken toestaat.
- **Tekstvoorspelling**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van toetsenborden met tekstvoorspelling toestaat voor suggesties voor woorden die de gebruiker mogelijk wil invoeren. Met **Blokkeren** wordt deze functie geblokkeerd.
- **Automatische correctie**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem automatische correctie van verkeerd gespelde woorden op het apparaat toestaat. **Blokkeren**: blokkeert het gebruik van Autocorrectie.
- **Spellingcontrole**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het gebruikerssysteem het gebruik van spellingcontrole op het apparaat toestaat. **Blokkeren**: staat de spellingcontrole toe.
- **Sneltoetsen**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van sneltoetsen op het apparaat toestaat. **Blokkeren** zorgt ervoor dat gebruikers geen sneltoetsen meer kunnen gebruiken.
- **Dicteren**: **Blokkeren** zorgt ervoor dat gebruikers geen spraakinvoer meer kunnen gebruiken om tekst in te voeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers dicteerinvoer gebruiken.
- **QuickPath**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om QuickPath te gebruiken, waarmee doorlopende invoer kan worden gebruikt op het toetsenbord van het apparaat. Gebruikers kunnen typen door over de toetsen te vegen om woorden te maken. Met **Blokkeren** voorkomt u dat gebruikers QuickPath kunnen gebruiken. 

  Deze functie is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

## <a name="cloud-and-storage"></a>Cloud en opslag

### <a name="settings-apply-to-all-enrollment-types"></a>Deze instellingen zijn van toepassing op: Alle inschrijvingstypen

- **Versleutelde back-up**: Selecteer **Vereisen** om ervoor te zorgen dat back-ups van het apparaat moeten worden versleuteld.
- **Beheerde apps synchroniseren met de cloud**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat met Intune beheerde apps gegevens synchroniseren naar het iCloud-account van de gebruiker. **Blokkeren**: voorkomt deze gegevenssynchronisatie naar iCloud.
- **Back-ups van Enterprise Book blokkeren**: **Blokkeren** voorkomt dat gebruikers back-ups maken van bedrijfsboeken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers een back-up maken van deze boeken.
- **Synchronisatie van metagegevens van Enterprise Book blokkeren (notities en markeringen)** : Met **Blokkeren** voorkomt u dat notities en markeringen in Enterprise Book-boeken worden gesynchroniseerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de synchronisatie toestaat.

### <a name="settings-apply-to-device-enrollment-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Apparaatinschrijving, automatische apparaatinschrijving (onder supervisie)

- **Photo Stream synchroniseren met iCloud**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers **Mijn fotostream** inschakelen op hun apparaat om te synchroniseren met iCloud, en foto's beschikbaar hebben op alle apparaten van de gebruikers. **Blokkeren**: voorkomt dat met Photo Stream foto’s worden gesynchroniseerd met iCloud. Als u deze functie blokkeert, kan dit leiden tot gegevensverlies. 
- **iCloud-fotobibliotheek**: **Blokkeren** schakelt het gebruik uit van de iCloud-fotobibliotheek voor het opslaan van foto's en video's in de cloud. Foto's die niet volledig naar het apparaat zijn gedownload vanaf de iCloud-fotobibliotheek, worden van het apparaat verwijderd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van de iTunes-fotobibliotheek toestaat.
- **Gedeelde fotostream**: **Blokkeren** schakelt het **delen van foto's via iCloud** uit op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem streaming van gedeelde foto's toestaat.
- **Handoff**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om op een iOS-/iPadOS-apparaat te werken en vervolgens hun werk voort te zetten op een ander iOS-/iPadOS- of macOS-apparaat. **Blokkeren**: voorkomt deze handoff.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **Back-up naar iCloud**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers een back-up van het apparaat maken naar iCloud. **Blokkeren**: zorgt ervoor dat gebruikers geen back-ups van het apparaat meer kunnen opslaan in iCloud.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **iCloud-documentsynchronisatie blokkeren**: Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het synchroniseren van documenten en sleutelwaarden met uw iCloud-opslagruimte toestaat. **Blokkeren**: voorkomt dat documenten en gegevens worden gesynchroniseerd met iCloud.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

- **Synchronisatie van iCloud-sleutelhanger blokkeren**: **Blokkeren** schakelt de synchronisatie van aanmeldingsgegevens in de sleutelhanger naar iCloud uit. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze aanmeldingsgegevens synchroniseren.

  Vanaf iOS/iPadOS 13.0 is het voor deze instelling vereist dat apparaten onder supervisie staan.

## <a name="autonomous-single-app-mode"></a>Autonome modus voor één app

Gebruik deze instellingen om iOS-/iPadOS-apparaten te configureren om specifieke apps in de autonome modus voor één app uit te voeren. Als deze modus is geconfigureerd en gebruikers een van de geconfigureerde apps starten, wordt het apparaat vergrendeld voor deze app. Schakelen tussen apps/taken is uitgeschakeld totdat gebruikers de toegestane app verlaten.

Voeg bijvoorbeeld in een school- of universiteitsomgeving een app toe waarmee gebruikers een test kunnen uitvoeren op het apparaat. Of vergrendel het apparaat in de Bedrijfsportal-app totdat de gebruiker zich verifieert. Wanneer de acties van de app zijn voltooid door gebruikers, of wanneer u het beleid verwijdert, keert het apparaat terug naar de normale staat.

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **App-naam**: Voer de naam in van de gewenste app.
- **App-bundel-id**: Voer de [bundel-id](bundle-ids-built-in-ios-apps.md) in van de gewenste app.
- **Toevoegen**: Selecteer deze optie om een lijst met uw apps te maken.

U kunt ook een CSV-bestand met de lijst met app-namen en de bijbehorende bundel-id’s **importeren**. Of **Exporteer** een bestaande lijst die de apps bevat.

## <a name="kiosk"></a>Kiosk

### <a name="settings-apply-to-automated-device-enrollment-supervised"></a>Deze instellingen zijn van toepassing op: Automatische apparaatinschrijving (onder toezicht)

- **App uitvoeren in kioskmodus**: Selecteer het type apps dat u wilt uitvoeren in de kioskmodus. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat het besturingssysteem geen kioskinstellingen toepast. Het apparaat wordt niet uitgevoerd in de kioskmodus.
  - **Store-app**: Voer de URL in voor een app in de iTunes App Store.
  - **Beheerde app**: Selecteer een app die u hebt toegevoegd aan Intune.
  - **Ingebouwde app**: Voer de [bundel-id](bundle-ids-built-in-ios-apps.md) in van de ingebouwde app.

- **Ondersteunende aanraking**: Selecteer **Vereisen** om de toegankelijkheidsinstelling Ondersteunende aanraking op het apparaat te vereisen. Deze functie helpt gebruikers bij schermbewegingen die mogelijk moeilijk zijn voor hen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Keer kleuren om**: Selecteer **Vereisen** om de toegankelijkheidsinstelling Keer kleuren om in te stellen, zodat gebruikers met een beperkt gezichtsvermogen de display kunnen wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Mono-audio**: Selecteer **Vereisen** om de toegankelijkheidsinstelling Mono-audio op het apparaat te vereisen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Spraakbeheer**: Met **Vereisen** maakt u spraakbesturing op het apparaat mogelijk en stelt u gebruikers in staat om het besturingssysteem volledig te bedienen met behulp van Siri-opdrachten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem spraakbesturing op het apparaat uitschakelt.

  Deze instelling is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger
  
  > [!TIP]
  > Als u Line-Of-Business-apps beschikbaar hebt voor uw organisatie en **Spraakbesturing** niet gereed is op dag 0 als iOS 13.0 wordt uitgebracht, wordt u aangeraden deze instelling te laten staan op **Niet geconfigureerd**.

- **VoiceOver**: Selecteer **Vereisen** om de toegankelijkheidsinstelling VoiceOver te vereisen op het apparaat om tekst op het scherm hardop voor te lezen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Zoomen**: Selecteer **Vereisen**, zodat gebruikers met behulp van aanraken het scherm kunnen inzoomen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie niet inschakelt of uitvoert in de kioskmodus.
- **Automatisch vergrendelen**: Met **Blokkeren** voorkomt u dat het apparaat automatisch wordt vergrendeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Schakelaar voor belsignaal**: Met **Blokkeren** wordt de schakelaar voor belsignaal (dempen) op het apparaat uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Scherm draaien**: **Blokkeren** voorkomt dat de schermstand wordt gewijzigd wanneer gebruikers het apparaat draaien. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Schermsluimerknop**: **Blokkeren** schakelt de knop voor slaapstand/ontwaken van het scherm uit op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.
- **Aanraken**: Met **Blokkeren** wordt het aanraakscherm uitgeschakeld op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het aanraakscherm gebruiken.
- **Volumeknoppen**: Met **Blokkeren** voorkomt u dat de volumeknoppen op het apparaat worden gebruikt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de volumeknoppen toestaat.
- **Besturingselement voor ondersteunende aanraking**: Selecteer **Toestaan**, zodat gebruikers de functie Ondersteunende aanraking kunnen gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.
- **Besturingselement voor kleuren omkeren**: Met **Toestaan** staat u aanpassingen in de functie Keer kleuren om toe, zodat gebruikers deze functie kunnen aanpassen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.
- **Geselecteerde tekst uitspreken**: Selecteer **Toestaan** om de toegankelijkheidsinstellingen Selectie uitspreken op het apparaat toe te staan. Met deze functie wordt de tekst die gebruikers selecteren, hardop gelezen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.
- **Wijziging van spraakbesturing**: Met **Toestaan** stelt u gebruikers in staat om spraakbesturing te regelen op hun apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voorkomt dat gebruikers de status van spraakbesturing op hun apparaten kunnen wijzigen.

  Deze instelling is van toepassing op:  
  - iOS 13.0 en hoger
  - iPadOS 13.0 en hoger

- **Besturingselement voor VoiceOver**: Selecteer **Toestaan**, zodat gebruikers de functie VoiceOver kunnen bijwerken, bijvoorbeeld hoe snel schermtekst hardop wordt gelezen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem voice-overwijzigingen toestaat.
- **Besturingselement voor zoomen**: Hiermee zijn wijzigingen in het zoomniveau door gebruikers **toegestaan**. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem wijzigingen in het zoomniveau voorkomt.

> [!NOTE]
> Voordat u een iOS-/iPadOS-apparaat kunt configureren voor de kioskmodus, moet u het hulpprogramma Apple Configurator of het Device Enrollment Program van Apple gebruiken om het apparaat in de supervisiemodus te plaatsen. Raadpleeg de handleiding van Apple voor het gebruik van het hulpprogramma Apple Configurator.
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

- App-vergrendeling (modus voor één app) 
- Algemene HTTP-proxy 
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
