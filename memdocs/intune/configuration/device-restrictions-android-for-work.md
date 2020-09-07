---
title: Apparaatinstellingen voor Android Enterprise in Microsoft Intune - Azure | Microsoft Docs
description: Op apparaten met Android Enterprise of Android for Work kunt u beperkingen op het apparaat instellen, zoals voor kopiëren en plakken, het weergeven van meldingen, app-machtigingen, het delen van gegevens, de wachtwoordlengte, mislukte aanmeldpogingen, het gebruik van vingerafdrukken om te ontgrendelen, het opnieuw gebruiken van wachtwoorden en het delen van zakelijke contactpersonen via Bluetooth. Configureer apparaten als een toegewezen apparaatkiosk voor het uitvoeren van een of meer apps.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/31/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: chmaguir, chrisbal, priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b213769234d55fd2a542ac166afe59c6e8b9e6c2
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194103"
---
# <a name="android-enterprise-device-settings-to-allow-or-restrict-features-using-intune"></a>Met Android Enterprise-apparaatinstellingen kunt u functies toestaan of beperken met behulp van Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen die u kunt beheren op Android Enterprise-apparaten. Gebruik deze instellingen als onderdeel van de MDM-oplossing (Mobile Device Management) om functies toe te staan of uit te schakelen, apps uit te voeren op tiegewezen apps, beveiliging te beheren en nog veel meer.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een apparaatconfiguratieprofiel](device-restrictions-configure.md).

## <a name="fully-managed-dedicated-and-corporate-owned-work-profile"></a>Volledig beheerd en toegewezen werkprofiel in bedrijfseigendom

Deze instellingen zijn van toepassing op Android Enterprise-inschrijvingstypen waarbij het hele apparaat wordt beheerd in Intune, zoals volledig beheerde, toegewezen Android Enterprise-apparaten met een werkprofiel in bedrijfseigendom.

Sommige instellingen worden niet door alle inschrijvingstypen ondersteund. Zie de gebruikersinterface om na te gaan welke instellingen door welke inschrijvingstypen worden ondersteund. Elke instelling bevindt zich onder een kop die aangeeft welke inschrijvingstypen deze instelling kunnen gebruiken.

![Headers instellen.](./media/device-restrictions-android-for-work/setting-headers.png)

Sommige instellingen zijn alleen van toepassing op het niveau van het werkprofiel voor apparaten in bedrijfseigendom met een werkprofiel. Ten aanzien van volledig beheerde en toegewezen apparaten zijn deze instellingen nog steeds van toepassing op het hele apparaat. Deze instellingen zijn gemarkeerd met een descriptor *(op het niveau van het werkprofiel)* in de gebruikersinterface.

![Headers instellen.](./media/device-restrictions-android-for-work/work-profile-level.png)


### <a name="general"></a>Algemeen

- **Schermopname**: **Blokkeren** voorkomt dat er schermopnamen of schermafbeeldingen met het apparaat worden gemaakt. U voorkomt ook dat de inhoud wordt weergegeven op weergaveapparaten die geen beveiligde video-uitvoer hebben. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers de scherminhoud vastleggen als een afbeelding.
- **Camera**: **Blokkeren** voorkomt toegang tot de camera op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot de camera toestaat.

  Intune beheert alleen de toegang tot de camera van het apparaat. Het heeft geen toegang tot afbeeldingen of video's.

- **Standaardmachtigingsbeleid**: Met deze instelling bepaalt u het standaardmachtigingsbeleid voor aanvragen betreffende runtime-machtigingen. Uw opties
  - **Standaardwaarde apparaat**: De standaardinstelling van het apparaat wordt gebruikt.
  - **Vragen**: Gebruikers wordt gevraagd de machtiging goed te keuren.
  - **Automatisch verlenen**: Machtigingen worden automatisch verleend.
  - **Automatisch weigeren**: Machtigingen worden automatisch geweigerd.
- **Wijzigingen in datum en tijd**: Met **Blokkeren** kunnen gebruikers niet handmatig de datum en tijd instellen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat de instellingen voor datum en tijd te wijzigen.
- **Volumewijzigingen**: **Blokkeren** voorkomt dat gebruikers het volume van het apparaat wijzigingen en dempt ook het hoofdvolume. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat de volume-instellingen op het apparaat te gebruiken.
- **Fabrieksinstellingen terugzetten**: Met **Blokkeren** kunnen gebruikers de optie voor het terugzetten van de fabrieksinstellingen van het apparaat niet gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instelling op het apparaat gebruiken.
- **Opstarten in veilige modus**: Met **Blokkeren** kunnen gebruikers het apparaat niet opnieuw opstarten in de veilige modus. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om het apparaat opnieuw op te starten in de veilige modus.
- **Statusbalk**: Met **Blokkeren** hebben gebruikers geen toegang tot de statusbalk, met inbegrip van meldingen en snelle instellingen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers toegang hebben tot de statusbalk.
- **Roaming gegevensservices**: **Blokkeren** voorkomt dataroaming via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem dataroaming toestaat wanneer het apparaat verbinding heeft met een mobiel netwerk.
- **Wi-Fi-instellingswijzigingen**: Met **Blokkeren** kunnen gebruikers door de eigenaar van het apparaat geconfigureerde Wi-Fi-instellingen niet wijzigen. Gebruikers kunnen hun eigen Wi-Fi-configuraties maken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de Wi-Fi-instellingen van het apparaat kunnen wijzigen.
- **Configuratie van Wi-Fi-toegangspunt**: Met **Blokkeren** kunnen gebruikers geen Wi-Fi-configuraties maken of wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de Wi-Fi-instellingen van het apparaat kunnen wijzigen.
- **Bluetooth-configuratie**: Met **Blokkeren** kunnen gebruikers Bluetooth niet configureren op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het gebruikerssysteem het gebruik van Bluetooth op het apparaat toestaat.
- **Tethering en toegang tot hotspots**: Met **Blokkeren** wordt tethering en toegang tot draagbare hotspots voorkomen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem tethering en toegang tot draagbare hotspots toestaat.
- **USB-opslag**: Kies **Toestaan** als u toegang tot USB-opslag op het apparaat toestaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de toegang tot USB-opslag verhindert.
- **USB-bestandsoverdracht**: Met **Blokkeren** voorkomt u bestandsoverdracht via USB. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem bestandsoverdracht toestaat.
- **Externe media**: Met **Blokkeren** voorkomt u dat er externe media op het apparaat worden gebruikt of dat hiermee verbinding wordt gemaakt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem externe media op het apparaat toestaat.
- **Gegevens beamen met NFC**: Met **Blokkeren** voorkomt u dat gegevens worden verzonden vanuit apps met behulp van de NFC-technologie. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gegevens tussen apparaten worden gedeeld via NFC.
- **Foutopsporingsfuncties**: Kies **Toestaan** als u wilt toestaan dat gebruikers de functies voor foutopsporing gebruiken op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers verhindert om de functies voor foutopsporing te gebruiken op het apparaat.
- **Microfoon aanpassen**: Met **Blokkeren** voorkomt u dat gebruikers de microfoon kunnen inschakelen of het volume van de microfoon kunnen aanpassen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om de microfoon van het apparaat te gebruiken en het volume ervan aan te passen.
- **E-mailadressen resetbeveiliging fabrieksinstellingen**: Kies **e-mailadressen van een Google-account**. Voer de e-mailadressen in van apparaatbeheerders die het apparaat kunnen ontgrendelen nadat dit is gewist. Plaats een puntkomma tussen de e-mailadressen, zoals `admin1@gmail.com;admin2@gmail.com`. Als u geen e-mailadres invoert, kan iedereen het apparaat ontgrendelen nadat de fabrieksinstellingen zijn hersteld. Deze e-mailadressen zijn alleen van toepassing wanneer terugzetten van de fabrieksinstellingen wordt geactiveerd door een niet-gebruiker, zoals een herstelmenu.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

- **Netwerknooduitgang**: Met **Inschakelen** kunnen gebruikers de functie Netwerknooduitgang inschakelen. Als er geen netwerkverbinding tot stand wordt gebracht bij het opstarten van het apparaat, vraagt de functie of er tijdelijk verbinding moet worden gemaakt met een netwerk en of het apparaatbeleid moet worden vernieuwd. Wanneer het beleid is toegepast, wordt het tijdelijke netwerk vergeten en gaat het apparaat verder met opstarten. Deze functie maakt in de volgende gevallen verbinding tussen een apparaat en netwerk:
  - Er bevindt zich geen geschikt netwerk in het laatste beleid.
  - Het apparaat wordt opgestart naar een app in de modus vergrendelingstaak.
  - Gebruikers hebben geen toegang tot de apparaatinstellingen.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers verhindert om de functie Netwerknooduitgang in te schakelen op het apparaat.

- **Systeemupdate**: Kies een optie om te bepalen hoe het apparaat omgaat met draadloze updates. Uw opties
  - **Standaardwaarde apparaat**: De standaardinstelling van het apparaat wordt gebruikt.
  - **Automatisch**: Updates worden automatisch geïnstalleerd zonder interactie van de gebruiker. Wanneer u dit beleid instelt, worden alle eventuele updates die nog niet zijn uitgevoerd, meteen geïnstalleerd.
  - **Uitgesteld**: Updates worden 30 dagen uitgesteld. Na 30 dagen worden gebruikers door Android gevraagd om de update te installeren. Het is mogelijk dat apparaatfabrikanten of leveranciers het uitstellen van belangrijke beveiligingsupdates voorkomen (uitzonderen). Voor een uitzonderingsupdate krijgen gebruikers een systeembericht te zien op het apparaat.
  - **Onderhoudsvenster**: Hiermee worden updates automatisch geïnstalleerd tijdens een dagelijkse onderhoudsperiode die u in Intune instelt. Er wordt gedurende 30 dagen geprobeerd om de updates te installeren. Dit kan mislukken als er te weinig ruimte of onvoldoende accuvermogen is. Na 30 dagen vraagt Android gebruikers om te installeren. Deze periode wordt is ook gebruikt om updates voor Play-apps te installeren. Gebruik deze optie voor specifieke apparaten, zoals kiosken, omdat toegewezen apparaten mt maar één app op de voorgrond kunnen worden bijgewerkt.

- **Meldingsvensters**: Als de optie **Uitschakelen** is ingesteld, worden venstermeldingen, inclusief pop-ups, inkomende oproepen, uitgaande oproepen, systeemwaarschuwingen en systeemfouten niet weergegeven op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem meldingen weergeeft.
- **Hints voor eerste gebruik overslaan**: **Inschakelen** verbergt suggesties (of slaat deze over) van apps die stapsgewijs door zelfstudies gaan, of hints wanneer de app wordt gestart. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze suggesties toont wanneer de app start.

### <a name="system-security"></a>Systeembeveiliging

- **Bedreigingsscan voor apps**: Met **Vereisen** (standaard) kunnen apps worden gescand door Google Play Protect voor- en nadat deze zijn geïnstalleerd. Als er een bedreiging wordt gedetecteerd, kunnen gebruikers de waarschuwing krijgen dat de app moet worden verwijderd van het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem niet Google Play Protect inschakelt of uitvoert om apps te scannen.

### <a name="device-experience"></a>Apparaatervaring

Gebruik deze instellingen om een kioskstijlervaring op uw toegewezen apparaten te configureren of om de ervaring van het startscherm voor uw volledig beheerde apparaten te configureren. U kunt apparaten configureren voor het uitvoeren van één app of een aantal apps. Wanneer een apparaat op de kioskmodus is ingesteld, zijn alleen de apps beschikbaar die u expliciet hebt toegevoegd.

**Type inschrijvingsprofiel**: Selecteer een inschrijvingsprofieltype om Microsoft Launcher of het beheerde Microsoft-startscherm op uw apparaten te configureren. Uw opties zijn:

- **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard kunnen gebruikers het standaardstartscherm van het apparaat zien.
- **Toegewezen apparaat**: Configureer een kioskstijlervaring op uw toegewezen apparaten. Voordat u deze instellingen configureert, moet u de gewenste apps [toevoegen](../apps/apps-add-android-for-work.md) en [toewijzen](../apps/apps-deploy.md) op de apparaten.

  - **Kioskmodus**: Kies dit als op het apparaat één app of meerdere apps worden uitgevoerd. Uw opties zijn:

    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Eén app**: Gebruikers hebben slechts toegang tot één app op het apparaat. Wanneer het apparaat wordt gestart, wordt alleen de specifieke app gestart. Gebruikers kunnen geen nieuwe apps openen of de actieve app wijzigen.

      - **Een app selecteren voor gebruik in de kioskmodus**: Selecteer de beheerde Google Play-app in de lijst.

      > [!IMPORTANT]
      > Wanneer u de kioskmodus voor één app gebruikt, werken de apps voor kiezer/telefoon mogelijk niet goed.
  
    - **Meerdere apps**: Gebruikers hebben toegang tot een beperkte set apps op het apparaat. Wanneer het apparaat wordt gestart, worden alleen de toegevoegde apps gestart. U kunt ook enkele webkoppelingen toevoegen die gebruikers kunnen openen. Wanneer het beleid wordt toegepast, zien gebruikers pictogrammen voor de toegestane apps op het startscherm.

      > [!IMPORTANT]
      > Voor toegewezen apparaten voor meerdere apps **moet** de [app Managed Home Screen](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise) van Google Play zijn:
      >   - [Toegevoegd aan Intune](../apps/apps-add-android-for-work.md)
      >   - [Toegewezen aan de apparaatgroep](../apps/apps-deploy.md) die is gemaakt voor uw toegewezen apparaten
      >
      > De app **Managed Home Screen** hoeft niet te zijn opgenomen in het configuratieprofiel, maar moet wel worden toegevoegd als een app. Wanneer de app **Managed Home Screen** is toegevoegd, worden andere apps die u aan het configuratieprofiel toevoegt, weergegeven als pictogrammen in de app **Managed Home Screen**.
      >
      > Wanneer u de kiosk modus voor meerdere apps gebruikt, werken de apps voor kiezer/telefoon mogelijk niet goed.
      >
      > Zie [Microsoft Managed Home Screen instellen op toegewezen apparaten in de kioskmodus voor meerdere apps](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060) voor meer informatie over Managed Home Screen.

      - **Toevoegen**: Selecteer uw apps in de lijst.

        Als de app **Managed Home Screen** niet wordt vermeld, [voegt u deze toe vanuit Google Play](https://play.google.com/work/apps/details?id=com.microsoft.launcher.enterprise). Zorg ervoor dat u [de app toewijst](../apps/apps-deploy.md) aan de apparaatgroep die is gemaakt voor uw toegewezen apparaten.

        U kunt ook andere [Android-apps](../apps/apps-add-android-for-work.md) toevoegen aan het apparaat, evenals [web-apps](../apps/web-app.md) die zijn gemaakt door uw organisatie. Zorg ervoor dat u [de app toewijst](../apps/apps-deploy.md) aan de apparaatgroep die is gemaakt voor uw toegewezen apparaten.

      - **Mappictogram**: Selecteer de kleur en vorm van het mappictogram dat wordt weergegeven op Managed Home Screen. Uw opties zijn:
        - Niet geconfigureerd 
        - Rechthoek met donker thema
        - Cirkel met donker thema
        - Rechthoek met licht thema
        - Cirkel met licht thema
      - **Pictogramgrootte voor de app en de map**: Selecteer de grootte van het mappictogram dat wordt weergegeven op Managed Home Screen. Uw opties zijn:
        - Niet geconfigureerd 
        - Extra klein
        - Klein
        - Gemiddeld
        - Groot
        - Extra groot

          De werkelijke grootte van het pictogram kan verschillen afhankelijk van de grootte van het scherm.

      - **Schermstand instellen**: Selecteer de richting waarin Managed Home Screen wordt weergegeven op apparaten. Uw opties zijn:
        - Niet geconfigureerd
        - Staand
        - Liggend
        - Automatisch draaien
      - **Badges voor app-meldingen**: Met **Inschakelen** wordt het aantal nieuwe en ongelezen meldingen op app-pictogrammen weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
      - **Virtuele startknop**: Een schermtoets waarmee gebruikers terugkeren naar Managed Home Screen zodat ze kunnen schakelen tussen apps. Uw opties zijn:
        - **Niet geconfigureerd** (standaard): Er wordt geen knop Start weergegeven. Gebruikers moeten de knop Terug gebruiken om tussen apps te schakelen.
        - **Omhoog swipen**: er wordt een knop Start weergegeven wanneer een gebruiker naar boven veegt op het apparaat.
        - **Zwevend**: toont een permanente, zwevende knop Start op het apparaat.

      - **Kioskmodus verlaten**: Met **Inschakelen** kunnen beheerders de kioskmodus tijdelijk onderbreken om het apparaat bij te werken. Voor gebruik van deze functie moet de beheerder het volgende doen:
  
        1. Doorgaan met het selecteren van de knop Terug totdat de knop **Kiosk verlaten** wordt weergegeven. 
        2. Hiermee wordt de knop **Kiosk verlaten** geselecteerd en de pincode voor het **verlaten van de kioskmodus ingevoerd**.
        3. Wanneer u klaar bent, selecteert u de app **Managed Home Screen**. Met deze stap wordt het apparaat weer vergrendeld in de kioskmodus voor gebruik van meerdere apps.

        Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem beheerders verhindert om de kioskmodus tijdelijk te onderbreken. Als de beheerder de knop Terug blijft selecteren en vervolgens de knop **Kiosk verlaten** selecteert, verschijnt er een bericht dat er een wachtwoordcode moet worden ingevoerd.

      - **Code voor verlaten kioskmodus**: Voer een 4-6-cijferige numerieke pincode in. De beheerder gebruikt deze pincode om de kioskmodus tijdelijk te onderbreken.

      - **Achtergrond voor aangepaste URL instellen**: Voer een URL in voor het aanpassen van het achtergrondscherm op het toegewezen apparaat. Voer bijvoorbeeld `http://contoso.com/backgroundimage.jpg` in.

        > [!NOTE]
        > In de meeste gevallen is het aan te raden om te beginnen met installatiekopieën van ten minste de volgende grootten:
        >
        > - Telefoon: 1080 x 1920 pixels
        > - Tablet: 1920 x 1080 pixels
        >
        > Voor de beste ervaring en heldere details is het aan te raden om per apparaatinstallatiekopie assets te maken voor de schermspecificaties.
        >
        > Moderne schermen hebben een hogere pixeldichtheid met de mogelijkheid om definitie-installatiekopieën gelijkwaardig aan 2K/4K weer te geven.

      - **Snelkoppeling naar menu Instellingen**: Met **Uitschakelen** wordt de snelkoppeling Beheerde instellingen op Managed Home Screen verborgen. Gebruikers kunnen nog steeds omlaag swipen om toegang te krijgen tot de instellingen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard wordt de snelkoppeling Beheerde instellingen op apparaten weergegeven. Gebruikers kunnen ook omlaag swipen om toegang te krijgen tot deze instellingen.

      - **Snelle toegang tot menu voor foutopsporing**: Met deze instelling bepaalt u hoe gebruikers toegang krijgen tot het menu voor foutopsporing. Uw opties zijn:

        - **Inschakelen**: Gebruikers kunnen eenvoudiger toegang krijgen tot het menu voor foutopsporing. Ze kunnen namelijk naar beneden swipen of de snelkoppeling Beheerde Instellingen gebruiken. Zoals altijd kunnen ze de knop Vorige 15 keer blijven selecteren.
        - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Eenvoudige toegang tot het menu voor foutopsporing is standaard uitgeschakeld. Gebruikers moeten de knop Vorige 15 keer selecteren om het menu voor foutopsporing te openen.

        Met het menu voor foutopsporing kunnen gebruikers het volgende doen:

        - Managed Home Screen-logboeken bekijken en uploaden
        - De app Android Device Policy van Google openen
        - Open de [Microsoft Intune-app](https://play.google.com/store/apps/details?id=com.microsoft.intune)
        - Kioskmodus verlaten

      - **Wi-Fi-configuratie**: Met **Inschakelen** wordt het Wi-Fi-besturingselement weergegeven in Managed Home Screen en krijgen gebruikers de mogelijkheid om het apparaat te verbinden met verschillende Wi-Fi-netwerken. Als u deze functie inschakelt, wordt ook de apparaatlocatie ingeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem niet het Wi-Fi-besturingselement weergeeft in Managed Home Screen. Hiermee voorkomt u dat gebruikers verbinding kunnen maken met Wi-Fi-netwerken terwijl ze Managed Home Screen gebruiken.

        - **Acceptatielijst voor Wi-Fi**: Maak een lijst met geldige namen voor draadloze netwerken, ook wel de SSID's (Service Set Identifier) genoemd. Managed Home Screen-gebruikers kunnen alleen verbinding maken met de SSID's die u invoert.

          Als u dit leeg laat, wordt deze instelling niet gewijzigd of bijgewerkt door Intune. Standaard zijn alle beschikbare Wi-Fi-netwerken toegestaan.

          **Importeer** een CSV-bestand dat een lijst met geldige SSID's bevat.

          **Exporteer** uw huidige lijst naar een CSV-bestand.

        - **SSID**: U kunt ook de Wi-Fi-netwerknamen (SSID) invoeren waarmee de Managed Home Screen-gebruikers verbinding kunnen maken. Let op dat u geldige SSID's invoert.

      - **Bluetooth-configuratie**: Met **Inschakelen** wordt het Bluetooth-besturingselement weergegeven in Managed Home Screen en krijgen gebruikers de mogelijkheid om apparaten te koppelen via Bluetooth. Als u deze functie inschakelt, wordt ook de apparaatlocatie ingeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem niet het Bluetooth-besturingselement weergeeft in Managed Home Screen. Hiermee voorkomt u dat gebruikers Bluetooth configureren en apparaten koppelen terwijl ze Managed Home Screen gebruiken.

      - **Zaklamp-toegang**: Met **Inschakelen** wordt het Zaklamp-besturingselement weergegeven in Managed Home Screen en krijgen gebruikers de mogelijkheid om de zaklamp in of uit te schakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem niet het zaklamp-besturingselement weergeeft in Managed Home Screen. Hiermee voorkomt u dat gebruikers de zaklamp gebruiken terwijl ze Managed Home Screen gebruiken.

      - **Volumeregeling voor media**: Met **Inschakelen** wordt de volumeregeling voor media weergegeven in Managed Home Screen en krijgen gebruikers de mogelijkheid om het mediavolume van het apparaat aan te passen met een schuifregelaar. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem niet het Volumeregeling voor media-besturingselement weergeeft in Managed Home Screen. Hiermee voorkomt u dat gebruikers het mediavolume van het apparaat aanpassen terwijl ze Managed Home Screen gebruiken, tenzij de hardwareknoppen hier ondersteuning voor bieden.

      - **Snel toegang krijgen tot apparaatgegevens**: Met **Inschakelen** kunnen gebruikers omlaag swipen om de apparaatgegevens op Managed Home Screen te zien, zoals het serienummer, het merk, het modelnummer en het SDK-niveau. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. De apparaatgegevens worden standaard mogelijk niet weergegeven.

      - **Schermbeveiligingsmodus**: Met **Inschakelen** wordt de schermbeveiliging weergegeven in Managed Home Screen wanneer het apparaat is vergrendeld of er een time-out optreedt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem niet een schermbeveiliging weergeeft in Managed Home Screen.

        Wanneer deze functie is ingeschakeld, moet u ook het volgende configureren:

        - **Een aangepaste afbeelding voor schermbeveiliging instellen**: Voer de URL in van een aangepaste PNG-, JPG-, JPEG-, GIF-, BMP-, WebP- of ICO-afbeelding. Als u geen URL opgeeft, wordt de standaardafbeelding van het apparaat gebruikt, indien aanwezig.

          Voer bijvoorbeeld het volgende in:

          - `http://www.contoso.com/image.jpg`
          - `www.contoso.com/image.bmp`
          - `https://www.contoso.com/image.webp`

          > [!TIP]
          > Elke bestandsresource-URL die in een bitmap kan worden omgezet, wordt ondersteund.

        - **Het aantal seconden dat op het apparaat de schermbeveiliging wordt weergegeven voordat het scherm wordt uitgeschakeld**: Kies hoelang de schermbeveiliging wordt weergegeven op het apparaat. Voer een waarde in tussen 0-9.999.999 seconden. De standaardwaarde is `0` seconden. Als deze waarde leeg is of is ingesteld op 0 (`0`), blijft de schermbeveiliging actief totdat een gebruiker met het apparaat communiceert.
        - **Het aantal seconden dat het apparaat inactief is voordat de schermbeveiliging wordt weergegeven**: Kies hoelang het apparaat inactief moet zijn voordat de schermbeveiliging wordt weergegeven. Voer een waarde in tussen 0-9.999.999 seconden. De standaardwaarde is `30` seconden. U moet een getal opgeven dat groter is dan nul (`0`).
        - **Media detecteren voordat de schermbeveiliging wordt gestart**: Met **Inschakelen** (standaard) wordt geen schermbeveiliging weergegeven wanneer er audio of video wordt afgespeeld op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem de schermbeveiliging weergeeft, zelfs als er audio of video wordt afgespeeld.

- **Volledig beheerd**: Hiermee configureert u de Microsoft Launcher-app op volledig beheerde apparaten.

  - **Microsoft Launcher instellen als standaardstartprogramma**: Als u **Inschakelen** kiest, wordt Microsoft Launcher ingesteld als het standaardstartprogramma op het startscherm. Als u Launcher de standaard maakt, kunnen gebruikers geen ander startprogramma gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Microsoft Launcher wordt niet als het standaardstartprogramma afgedwongen.
  - **Aangepaste achtergrond configureren**: Met **Inschakelen** kunt u uw eigen afbeelding toepassen als achtergrond voor het startscherm en kiezen of gebruikers de afbeelding kunnen wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard behoudt het apparaat de huidige achtergrond.
    - **De URL van de achtergrondafbeelding invoeren**: Voer de URL van de achtergrondafbeelding in. Deze afbeelding wordt weergegeven op het startscherm van het apparaat. Voer bijvoorbeeld `http://www.contoso.com/image.jpg` in. 
    - **Gebruiker toestaan om de achtergrond te wijzigen**: Met **Inschakelen** worden gebruikers toegestaan om de achtergrondafbeelding te wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kunnen gebruikers de achtergrond niet wijzigen.
  - **De startfeed inschakelen**: Met **Inschakelen** wordt de startfeed ingeschakeld, waarmee agenda's, documenten en recente activiteiten worden weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard wordt deze feed niet weergegeven.
    - **Gebruikers toestaan om feed in/uit te schakelen**: met **Inschakelen** kunnen gebruikers de startfeed in-of uitschakelen. Met **Inschakelen** wordt deze instelling alleen geforceerd wanneer het profiel voor de eerste keer wordt toegewezen. Bij toekomstige profieltoewijzingen wordt deze instelling niet geforceerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kunnen gebruikers de instellingen voor de startfeed niet wijzigen.
  - **Aanwezigheid van dock**: De dock biedt gebruikers snelle toegang tot hun apps en hulpprogramma's. Uw opties zijn:
    - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Weergeven**: De dock wordt weergegeven op apparaten.
    - **Verbergen**: De dock is verborgen. Gebruikers moeten omhoog swipen om toegang te krijgen tot de dock.
    - **Uitgeschakeld**: De dock wordt niet weergegeven op apparaten en gebruikers kunnen deze niet weergeven.

  - **Gebruikers toestaan de aanwezigheid van het dock te wijzigen**: Met **Inschakelen** kunnen gebruikers de dock weergeven of verbergen. Met **Inschakelen** wordt deze instelling alleen geforceerd wanneer het profiel voor de eerste keer wordt toegewezen. Bij toekomstige profieltoewijzingen wordt deze instelling niet geforceerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard mogen gebruikers de configuratie van de apparaatdock niet wijzigen.

  - **Plaatsing van de zoekbalk**: Kies waar u de zoekbalk wilt plaatsen. Uw opties zijn:
    - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
    - **Boven**: De zoekbalk wordt weergegeven aan de bovenkant van apparaten.
    - **Onder**: De zoekbalk wordt weergegeven aan de onderkant van apparaten.
    - **Verbergen**: De zoekbalk is verborgen.

<!-- MandiA (7.16.2020) The following settings may be in a future release. Per PM, we can leave it in GitHub, not live. Remove comment tags if/when it releases.
  - **Allow user to change search bar placement**: **Enable** allows users to change the location of the search bar. **Enable** only forces this setting the first time the profile is assigned. Any future profile assignments don't force this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, users are prevented from changing the location.
End of comment -->

### <a name="password"></a>Wachtwoord

- **Vergrendelingsscherm uitschakelen**: Kies **Uitschakelen** als u wilt voorkomen dat gebruikers de functie voor het vergrendelen van het scherm Keyguard op het apparaat gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers de Keyguard-functies gebruiken.
- **Uitgeschakelde functies van het vergrendelingsscherm**: Kies, wanneer keyguard is ingeschakeld op het apparaat, welke functies u wilt uitschakelen. Wanneer bijvoorbeeld de optie **Veilige camera** is geselecteerd, wordt de functie van de camera op het apparaat is uitgeschakeld. Alle functies die niet zijn geselecteerd, zijn op het apparaat ingeschakeld.

  Deze functies zijn beschikbaar voor gebruikers wanneer het apparaat is vergrendeld. De geselecteerde functies zijn niet zichtbaar en niet toegankelijk voor gebruikers.

- **Vereist wachtwoordtype**: Voer het vereiste complexiteitsniveau voor het wachtwoord in en geef aan of biometrische apparaten kunnen worden gebruikt. Uw opties zijn:
  - **Standaardwaarde apparaat**
  - **Wachtwoord vereist, geen beperkingen**
  - **Zwakke biometrie**: [Sterke versus zwakke biometrie](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (hiermee wordt een Android-website geopend)
  - **Numeriek**: Het wachtwoord mag alleen uit getallen bestaan, bijvoorbeeld `123456789`. Voer ook in:
    - **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens.
  - **Complex numeriek**: Herhaalde of opeenvolgende cijfers, zoals '1111' of '1234', zijn niet toegestaan. Voer ook in:
    - **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens.
  - **Alfabetisch**: Letters uit het alfabet zijn vereist. Er zijn geen cijfers en symbolen vereist. Voer ook in:
    - **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens.
  - **Alfanumeriek**: Dit zijn hoofdletters, kleine letters en numerieke tekens. Voer ook in:
    - **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens.
  - **Alfanumeriek met symbolen**: Dit zijn hoofdletters, kleine letters, numerieke tekens, leestekens en symbolen. Voer ook in:

    - **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens.
    - **Het vereiste aantal tekens**: Voer het aantal tekens in dat het wachtwoord moet bevatten, tussen 0 en 16 tekens.
    - **Het vereiste aantal kleine letters**: Voer het aantal kleine letters in dat het wachtwoord moet bevatten, tussen 0 en 16 tekens.
    - **Het vereiste aantal hoofdletters**: Voer het aantal hoofdletters in dat het wachtwoord moet bevatten, tussen 0 en 16 tekens.
    - **Het vereiste aantal andere tekens dan letters**: Voer het aantal andere tekens dan alfabetische letters in dat het wachtwoord moet bevatten, tussen 0 en 16 tekens.
    - **Het vereiste aantal numerieke tekens**: Voer het aantal numerieke tekens (`1`, `2`, `3` enzovoort) in dat het wachtwoord moet bevatten, tussen 0 en 16 tekens.
    - **Het vereiste aantal symbolen**: Voer het aantal symbolen (`&`, `#`, `%` enzovoort) in dat het wachtwoord moet bevatten, tussen 0 en 16 tekens.

- **Het aantal dagen totdat het wachtwoord verloopt**: Geef het aantal dagen, tussen 1 en 365, op waarna het wachtwoord voor het apparaat moet worden gewijzigd. Voer bijvoorbeeld `90` als u wilt dat het wachtwoord na 90 dagen verloopt. Wanneer het wachtwoord is verlopen, wordt gebruikers gevraagd een nieuw wachtwoord te maken. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Het vereiste aantal wachtwoorden voordat de gebruiker een wachtwoord opnieuw kan gebruiken**: Gebruik deze instelling om te voorkomen dat gebruikers eerder gebruikte wachtwoorden hergebruiken. Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld `5` invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal onjuiste wachtwoorden tussen 4 en 11 in dat is toegestaan voordat het apparaat wordt gewist. Met `0` (nul) kan de functionaliteit voor het wissen van het apparaat worden uitgeschakeld. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  > [!NOTE]
  > Op volledig beheerde, toegewezen apparaten met een werkprofiel in bedrijfseigendom worden gebruikers niet gevraagd om een wachtwoord in te stellen. De instellingen zijn vereist, maar gebruikers worden mogelijk niet op de hoogte gesteld. Gebruikers moeten het wachtwoord handmatig instellen. Het beleid geeft de melding dat de aanmelding is mislukt totdat de gebruiker een wachtwoord instelt dat voldoet aan uw vereisten.

### <a name="power-settings"></a>Energie-instellingen

- **Tijd tot het scherm wordt vergrendeld**: Voer de maximale tijd tot het apparaat wordt vergrendeld in die een gebruiker kan instellen. Als u deze instelling bijvoorbeeld instelt op `10 minutes`, kunnen gebruikers een tijd instellen tussen 15 seconden en 10 minuten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

- **Scherm aan terwijl het apparaat is aangesloten**: Kies bij welke energiebronnen het scherm aan blijft wanneer het apparaat is aangesloten.

### <a name="users-and-accounts"></a>Gebruikers en accounts

- **Nieuwe gebruikers toevoegen**: Met **Blokkeren** voorkomt u dat gebruikers nieuwe gebruikers kunnen toevoegen. Elke gebruiker heeft een persoonlijke ruimte op het apparaat voor aangepaste beginschermen, accounts, apps en instellingen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers andere gebruikers aan het apparaat toevoegen.
- **Gebruiker verwijderen**: Met **Blokkeren** voorkomt u dat gebruikers andere gebruikers kunnen verwijderen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers andere gebruikers van het apparaat kunnen verwijderen.
- **Accountwijzigingen** (alleen toegewezen apparaten): Met **Blokkeren** voorkomt u dat gebruikers accounts wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers gebruikersaccounts op het apparaat bijwerkt.

  > [!NOTE]
  > Deze instelling wordt niet nageleefd op volledig beheerde, toegewezen apparaten met een werkprofiel in bedrijfseigendom. Als u deze instelling configureert, wordt de instelling genegeerd en heeft deze geen invloed.

- **Gebruiker kan referenties configureren**: **Blokkeren** voorkomt dat gebruikers certificaten configureren die zijn toegewezen aan apparaten, ook bij apparaten die niet zijn gekoppeld aan een gebruikersaccount. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers de mogelijkheid biedt om hun referenties te configureren of te wijzigen wanneer ze deze openen in de sleutelopslag.
- **Persoonlijke Google-accounts**: Met **Blokkeren** wordt voorkomen dat gebruikers hun persoonlijke Google-account toevoegen aan het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om hun persoonlijke Google-account toe te voegen.

### <a name="applications"></a>Toepassingen

- **Installatie vanuit onbekende bronnen toestaan**: Met **Toestaan** kunnen gebruikers **onbekende bronnen** inschakelen. Met deze instelling kunnen apps van onbekende bronnen worden geïnstalleerd, met inbegrip van andere bronnen dan Google Play Store. Hiermee kunnen gebruikers apps op het apparaat side-loaden met behulp van een andere methode dan de Google Play Store. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers verhindert om **onbekende bronnen** in te schakelen.
- **Toegang tot alle apps in Google Play Store toestaan**: Als deze optie is ingesteld op **Toestaan**, krijgen gebruikers toegang tot alle apps in Google Play store. Ze krijgen geen toegang tot apps die de beheerder blokkeert in[Client-apps](../apps/apps-add-android-for-work.md).

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard het volgende doen:
  
  - Gebruikers dwingen om alleen apps te openen die de beheerder beschikbaar maakt in Google Play Store of apps die zijn vereist in [Client-apps](../apps/apps-add-android-for-work.md). 
  - Automatisch apps verwijderen waarvan wordt gedetecteerd dat ze zijn geïnstalleerd door gebruikers buiten de Google Play Store.

  Als u side-loaden wilt inschakelen, stelt **Installatie uit onbekende bronnen toestaan** en **Toegang tot alle apps in Google Play Store toestaan** in op **Toestaan**.

- **App wordt automatisch bijgewerkt**: In apparaten wordt dagelijks gecontroleerd op app-updates. Kies deze optie wanneer updates automatisch worden geïnstalleerd. Uw opties zijn:
  - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Gebruikerskeuze**: Het besturingssysteem wordt mogelijk standaard ingesteld op deze optie. Gebruikers kunnen hun voorkeuren instellen in de beheerde Google Play-app.
  - **Nooit**: Updates worden nooit geïnstalleerd. Deze optie wordt niet aanbevolen.
  - **Alleen Wi-Fi**: Updates worden alleen geïnstalleerd wanneer het apparaat is verbonden met een Wi-Fi-netwerk.
  - **Altijd**: Updates worden geïnstalleerd wanneer deze beschikbaar zijn.

### <a name="connectivity"></a>Connectiviteit

- **Permanente VPN**: Met **Inschakelen** zal de VPN-client automatisch verbinding maken en opnieuw verbinding maken met het VPN. Permanente VPN-verbindingen blijven verbonden. Of maken direct verbinding wanneer gebruikers hun apparaat vergrendelen, het apparaat opnieuw wordt opgestart of het draadloze netwerk wordt gewijzigd.

  Kies **Niet geconfigureerd** om AlwaysOn VPN voor alle VPN-clients uit te schakelen.

  > [!IMPORTANT]
  > Implementeer slechts één AlwaysOn VPN-beleid per apparaat. Het implementeren van meerdere AlwaysOn VPN-beleidsregels op één apparaat wordt niet ondersteund.

- **VPN-client**: Kies een VPN-client die ondersteuning biedt voor AlwaysOn. Uw opties zijn:
  - Cisco AnyConnect
  - F5-toegang
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Aangepast
    - **Pakket-id**: Voer de pakket-id in van de app in Google Play. Als de URL voor de app in Google Play bijvoorbeeld `https://play.google.com/store/details?id=com.contosovpn.android.prod` is, is de pakket-id `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - De VPN-client die u kiest moet op het apparaat worden geïnstalleerd en moet VPN per app in werkprofielen ondersteunen. Anders treedt er een fout op. 
  > - U dient de VPN-client-app goed te keuren in de **Beheerde Google Play Store**, de app te synchroniseren naar Intune en de app te implementeren op het apparaat. Nadat u dit hebt gedaan, is de app geïnstalleerd in het werkprofiel van de gebruiker.
  > - U moet de VPN-client nog steeds configureren met een [VPN-profiel](vpn-settings-android-enterprise.md) of via een [app-configuratieprofiel](../apps/app-configuration-policies-use-android.md).
  > - Er zijn mogelijk bekende problemen bij het gebruik van VPN per app met F5 Access voor Android 3.0.4. Zie [Releaseopmerkingen voor F5 Access voor Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android) voor meer informatie.

- **Vergrendelingsmodus**: Met **Inschakelen** dwingt u af dat al het netwerkverkeer de VPN-tunnel gebruikt. Als er geen VPN-verbinding is ingesteld, heeft het apparaat geen toegang tot het netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat verkeer via de VPN-tunnel of via het mobiele netwerk gaat.

- **Aanbevolen algemene proxy**: Met **Inschakelen** wordt een algemene proxy aan de apparaten toegevoegd. Wanneer deze functie is ingeschakeld, wordt het HTTP- en HTTPS-verkeer, inclusief enkele apps op het apparaat, gebruikt voor de proxy die u invoert. Deze proxy is slechts een aanbeveling. Het kan zijn dat sommige apps de proxy niet gebruiken. **Niet geconfigureerd** (standaard): er wordt geen aanbevolen algemene proxy toegevoegd.

  Zie [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (er wordt een Android-site geopend) voor meer informatie over deze functie.

  Wanneer deze functie is ingeschakeld, voert u ook het **Type** proxy in. Uw opties zijn:

  - **Direct**: Voer de proxyserverinstellingen handmatig in, waaronder:
    - **Host**: Voer de hostnaam of het IP-adres van de proxyserver in. Voer bijvoorbeeld `proxy.contoso.com` of `127.0.0.1` in.
    - **Poortnummer**: Voer het TCP-poortnummer in dat wordt gebruikt voor de proxyserver. Voer bijvoorbeeld `8080` in.
    - **Uitgesloten hosts**: Voer een lijst met hostnamen of IP-adressen in die niet gebruikmaken van de proxy. Deze lijst kan een asterisk (`*`) bevatten en meerdere hosts gescheiden door puntkomma’s (`;`) zonder spaties. Voer bijvoorbeeld `127.0.0.1;web.contoso.com;*.microsoft.com` in.

  - **Automatische proxyconfiguratie**: Voer de **PAC-URL** in van een automatisch script voor de proxyconfiguratie. Voer bijvoorbeeld `https://proxy.contoso.com/proxy.pac` in.

    Zie [PAC-bestand (Proxy Auto-Configuration)](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (hiermee opent u een niet-Microsoft-site) voor meer informatie over PAC-bestanden.

  Zie [setRecommendedGlobalProxy](https://developer.android.com/reference/android/app/admin/DevicePolicyManager.html#setRecommendedGlobalProxy(android.content.ComponentName,%20android.net.ProxyInfo)) (er wordt een Android-site geopend) voor meer informatie over deze functie.

## <a name="work-profile-only"></a>Alleen werkprofiel

Deze instellingen zijn van toepassing op Android Enterprise-inschrijvingstypen waarbij alleen het werkprofiel wordt beheerd in Intune, zoals een inschrijving voor een Android Enterprise-werkprofiel op een persoonlijk apparaat of een BYOD-apparaat (Bring-Your-Own-Device).

### <a name="work-profile-settings"></a>Werkprofielinstellingen

- **Kopiëren en plakken tussen werkprofielen en persoonlijke profielen**: Met **Blokkeren** kunnen gebruikers niet kopiëren en plakken tussen werk-apps en persoonlijke apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers toestaat om gegevens met behulp van kopiëren en plakken te delen met apps in het persoonlijke profiel.
- **Gegevens delen tussen werkprofielen en persoonlijke profielen**: Kies of delen mogelijk is tussen apps in het werkprofiel en apps in het persoonlijke profiel. Met deze instelling kunt u bijvoorbeeld deelacties binnen toepassingen bepalen, zoals de optie **Delen…** in de Chrome-browser-app. Deze instelling geldt niet voor kopiëren en plakken op het klembord. Uw opties zijn:
  - **Standaardwaarde apparaat**: Dit is de standaardinstelling voor het delen van gegevens van het apparaat. Deze instelling is afhankelijk van de Android-versie:
    - Op apparaten met Android 6.0 en hoger is delen van het werkprofiel naar het persoonlijke profiel standaard geblokkeerd. Delen van het persoonlijke profiel naar het werkprofiel is toegestaan.
    - Op apparaten met Android 5.0 en hoger is delen tussen het werkprofiel en het persoonlijke profiel in beide richtingen geblokkeerd.
  - **Met apps in het werkprofiel kunnen aanvragen voor delen van het persoonlijke profiel worden verwerkt**: Hiermee wordt de ingebouwde Android-functie ingeschakeld waarmee het delen van het persoonlijke profiel naar het werkprofiel is toegestaan. Wanneer dit is ingeschakeld, kan een deelverzoek van een app in het persoonlijke profiel worden gedeeld met apps in het werkprofiel. Dit is de standaardinstelling voor Android-apparaten met een oudere versie dan 6.0.
  - **Geen beperkingen voor delen**: Biedt de mogelijkheid om in beide richtingen buiten de grenzen van het werkprofiel te delen. Wanneer u deze instelling selecteert, kunnen apps met het werkprofiel gegevens delen met apps in het persoonlijke profiel die geen badge hebben. Met deze instelling kunnen beheerde apps in het werkprofiel gegevens delen met apps aan de onbeheerde zijde van het apparaat. Gebruik deze instelling daarom zorgvuldig.

- **Werkprofielmeldingen terwijl het apparaat is vergrendeld**: Met **Blokkeren** worden venstermeldingen, inclusief pop-ups, inkomende oproepen, uitgaande oproepen, systeemwaarschuwingen en systeemfouten niet weergegeven op vergrendelde apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem meldingen weergeeft.
- **Standaardapp-machtigingen**: Hiermee stelt u het standaardmachtigingsbeleid in voor alle apps in het werkprofiel. Vanaf Android 6 wordt aan gebruikers gevraagd bepaalde vereiste machtigingen aan apps toe te kennen wanneer de app wordt gestart. Met deze beleidsinstelling kunt u in het werkprofiel bepalen of gebruikers wordt gevraagd om machtigingen toe te kennen voor alle apps in het werkprofiel. U kunt bijvoorbeeld een app aan het werkprofiel toewijzen waarvoor toegang tot de locatie is vereist. Normaal gesproken wordt aan gebruikers gevraagd of deze de app toegang tot de locatie willen geven. Gebruik dit beleid om automatisch machtigingen te verlenen zonder om bevestiging te vragen, automatisch machtigingen te weigeren zonder om bevestiging te vragen, of om gebruikers te laten beslissen. Uw opties zijn:
  - **Standaardwaarde apparaat**
  - **Vragen**
  - **Automatisch verlenen**
  - **Automatisch weigeren**

  U kunt ook een app-configuratiebeleid gebruiken om machtigingen voor afzonderlijke apps te verlenen (**Client-apps** > **App-configuratiebeleid**).

- **Accounts toevoegen en verwijderen**: Met **Blokkeren** voorkomt u dat gebruikers handmatig accounts in het werkprofiel kunnen toevoegen of uit het werkprofiel kunnen verwijderen. Als u de Gmail-app bijvoorbeeld implementeert in een Android-werkprofiel, kunt u verhinderen dat gebruikers accounts toevoegen aan of verwijderen uit dit werkprofiel. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het toevoegen van accounts in het werkprofiel toestaat.  

  > [!NOTE]
  > Google-accounts kunnen niet worden toegevoegd aan een werkprofiel.

- **Contactpersoon delen via Bluetooth**: Met **Inschakelen** kunnen gebruikers contactpersonen in het werkprofiel delen en openen op een ander apparaat, met inbegrip van een auto die is gekoppeld met behulp van Bluetooth. Door deze instelling in te schakelen, kunnen bepaalde Bluetooth-apparaten werkcontactpersonen cachen bij de eerste verbinding. Als u dit beleid uitschakelt na een eerste synchronisatie, zijn de werkcontactpersonen van een Bluetooth-apparaat niet meteen verwijderd.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem geen werkcontactpersonen deelt.

  Deze instelling is van toepassing op:

  - Apparaten met Android-werkprofiel en met Android 6.0 en hoger

- **Schermopname**: Met **Blokkeren** voorkomt u dat in het werkprofiel schermopnamen of schermafbeeldingen worden gemaakt op het apparaat. U voorkomt ook dat de inhoud wordt weergegeven op weergaveapparaten die geen beveiligde video-uitvoer hebben. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het verkrijgen van schermopnamen toestaat.

- **Beller-id van zakelijk contactpersoon weergeven in persoonlijk profiel**: Met **Blokkeren** wordt het telefoonnummer van deze zakelijke contactpersoon niet weergegeven in het persoonlijke profiel. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem telefoongegevens van zakelijke contactpersonen weergeeft.

  Deze instelling is van toepassing op:

  - Android OS v6.0 en nieuwere versies

- **Werkcontacten zoeken in persoonlijk profiel**: Met **Blokkeren** voorkomt u dat gebruikers in apps in het persoonlijke profiel zoeken naar werkcontacten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het zoeken naar werkcontacten in het persoonlijke profiel toestaat.

- **Camera**: Met **Blokkeren** hebben gebruikers geen toegang tot de camera op het apparaat in het werkprofiel. De camera aan de persoonlijke zijde wordt niet beïnvloed door de instelling. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot de camera toestaat.

- **Widgets van apps in het werkprofiel toestaan**: Met **Inschakelen** krijgen gebruikers de mogelijkheid om widgets van apps op het startscherm te plaatsen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie uitschakelt.

  Stel bijvoorbeeld dat Outlook is geïnstalleerd in de werkprofielen van uw gebruikers. Als deze instelling is ingesteld op **Inschakelen**, kunnen gebruikers de agendawidget op het startscherm van het apparaat plaatsen.

- **Werkprofielwachtwoord vereisen**: Met **Vereisen** dwingt u een beleid voor wachtwoordcodes af dat alleen van toepassing is op de apps in het werkprofiel. Standaard kunnen gebruikers de twee afzonderlijk gedefinieerde pincodes gebruiken. Of gebruikers kunnen de pincodes combineren in een sterkere versie van de twee pincodes. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers werk-apps gebruiken zonder dat zij een wachtwoord invoeren.

  Deze instelling is van toepassing op:

  - Android 7.0 en nieuwer waarbij het werkprofiel is ingeschakeld

  Configureer ook het volgende:

  - **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens.
  - **Maximum aantal minuten van inactiviteit voordat het werkprofiel wordt vergrendeld**: Voer de tijdsduur in gedurende welke apparaten inactief moeten zijn voordat het scherm automatisch wordt vergrendeld. Gebruikers moeten hun referenties invoeren om weer toegang te krijgen. Voer bijvoorbeeld `5` in om het apparaat te vergrendelen nadat dit vijf minuten lang inactief is geweest. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

    Gebruikers kunnen op apparaten geen tijdwaarde instellen die groter is dan de geconfigureerde tijd in het profiel. Gebruikers kunnen een lagere tijdwaarde instellen. Als het profiel bijvoorbeeld is ingesteld op `15` minuten, kunnen gebruikers de waarde instellen op 5 minuten. Gebruikers kunnen de waarde niet instellen op 30 minuten.

  - **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal onjuiste wachtwoorden tussen 4 en 11 in dat is toegestaan voordat het werkprofiel op het apparaat wordt gewist. Met `0` (nul) kan de functionaliteit voor het wissen van het apparaat worden uitgeschakeld. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  - **Wachtwoordverlooptijd (dagen)** : Voer het aantal dagen in totdat het wachtwoorden van gebruikers moeten worden gewijzigd (van **1**-**365**).
  - **Vereist wachtwoordtype**: Voer het vereiste complexiteitsniveau voor het wachtwoord in en geef aan of biometrische apparaten kunnen worden gebruikt. Uw opties zijn:
    - **Standaardwaarde apparaat**
    - **Lage beveiligingsbiometrie**: [Sterke versus zwakke biometrie](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (hiermee wordt een Android-website geopend)
    - **Vereist**
    - **Ten minste numeriek**: Bevat numerieke tekens, zoals `123456789`.
    - **Complex numeriek**: Herhaalde of opeenvolgende cijfers, zoals `1111` of `1234`, zijn niet toegestaan.
    - **Ten minste alfabetisch**: Bevat letters uit het alfabet. Er zijn geen cijfers en symbolen vereist.
    - **Ten minste alfanumeriek**: Dit zijn hoofdletters, kleine letters en numerieke tekens.
    - **Ten minste alfanumeriek met symbolen**: Dit zijn hoofdletters, kleine letters, numerieke tekens, leestekens en symbolen.

  - **Wachtwoorden niet opnieuw gebruiken**: Gebruik deze instelling om te voorkomen dat gebruikers eerder gebruikte wachtwoorden hergebruiken. Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld `5` invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Ontgrendelen met gezicht**: Met **Blokkeren** voorkomt u dat gebruikers de gezichtsherkenning van het apparaat gebruiken om het werkprofiel te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van gezichtsherkenning.
  - **Ontgrendelen met vingerafdruk**: Met **Blokkeren** voorkomt u dat gebruikers de vingerafdrukscanner van het apparaat gebruiken om het werkprofiel te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van een vingerafdruk.
  - **Ontgrendelen met iris**: Met **Blokkeren** voorkomt u dat gebruikers de irisscanner van het apparaat gebruiken om het werkprofiel te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van de irisscanner.
  - **Smart Lock en andere trustagenten**: Met **Blokkeren** voorkomt u dat Smart Lock of andere trustagenten instellingen voor het vergrendelingsscherm van compatibele apparaten aanpassen. Als apparaten zich op een vertrouwde locatie bevinden, kunt u met deze functie, ook wel trustagent genoemd, het vergrendelingsschermwachtwoord op apparaten uitschakelen of overslaan. Hiermee kan bijvoorbeeld het wachtwoord van het werkprofiel worden overgeslagen wanneer apparaten zijn verbonden met een bepaald Bluetooth-apparaat of wanneer deze zich in de buurt van een NFC-tag bevinden. Gebruik deze instelling om te voorkomen dat gebruikers Smart Lock configureren.

    Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

### <a name="password"></a>Wachtwoord

Deze wachtwoordinstellingen zijn van toepassing op persoonlijke profielen op apparaten die gebruikmaken van een werkprofiel.

- **Minimale wachtwoordlengte**: Voer de minimale lengte van het wachtwoord in, tussen 4 en 16 tekens.
- **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**: Voer de tijdsduur in gedurende welke apparaten inactief moeten zijn voordat het scherm automatisch wordt vergrendeld. Gebruikers moeten hun referenties invoeren om weer toegang te krijgen. Voer bijvoorbeeld `5` in om het apparaat te vergrendelen nadat dit vijf minuten lang inactief is geweest. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  Gebruikers kunnen op apparaten geen tijdwaarde instellen die groter is dan de geconfigureerde tijd in het profiel. Gebruikers kunnen een lagere tijdwaarde instellen. Als het profiel bijvoorbeeld is ingesteld op `15` minuten, kunnen gebruikers de waarde instellen op 5 minuten. Gebruikers kunnen de waarde niet instellen op 30 minuten.

- **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal onjuiste wachtwoorden tussen 4 en 11 in dat is toegestaan voordat het werkprofiel op het apparaat wordt gewist. Met `0` (nul) kan de functionaliteit voor het wissen van het apparaat worden uitgeschakeld. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Wachtwoordverlooptijd (dagen)** : Geef het aantal dagen, tussen 1 en 365, op waarna het wachtwoord voor het apparaat moet worden gewijzigd. Voer bijvoorbeeld `90` als u wilt dat het wachtwoord na 90 dagen verloopt. Wanneer het wachtwoord is verlopen, wordt gebruikers gevraagd een nieuw wachtwoord te maken. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Vereist wachtwoordtype**: Voer het vereiste complexiteitsniveau voor het wachtwoord in en geef aan of biometrische apparaten kunnen worden gebruikt. Uw opties zijn:
  - **Standaardwaarde apparaat**
  - **Lage beveiligingsbiometrie**: [Sterke versus zwakke biometrie](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (hiermee wordt een Android-website geopend)
  - **Vereist**
  - **Ten minste numeriek**: Bevat numerieke tekens, zoals `123456789`.
  - **Complex numeriek**: Herhaalde of opeenvolgende cijfers, zoals `1111` of `1234`, zijn niet toegestaan.
  - **Ten minste alfabetisch**: Bevat letters uit het alfabet. Er zijn geen cijfers en symbolen vereist.
  - **Ten minste alfanumeriek**: Dit zijn hoofdletters, kleine letters en numerieke tekens.
  - **Ten minste alfanumeriek met symbolen**: Dit zijn hoofdletters, kleine letters, numerieke tekens, leestekens en symbolen.

- **Wachtwoorden niet opnieuw gebruiken**: Gebruik deze instelling om te voorkomen dat gebruikers eerder gebruikte wachtwoorden hergebruiken. Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld `5` invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Ontgrendelen met vingerafdruk**: Met **Blokkeren** voorkomt u dat gebruikers de vingerafdrukscanner van het apparaat gebruiken om het apparaat te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van een vingerafdruk.
- **Ontgrendelen met gezicht**: Met **Blokkeren** voorkomt u dat gebruikers de gezichtsherkenning van het apparaat gebruiken om het apparaat te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van gezichtsherkenning.
- **Ontgrendelen met iris**: Met **Blokkeren** voorkomt u dat gebruikers de irisscanner van het apparaat gebruiken om het apparaat te ontgrendelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers het apparaat ontgrendelen met behulp van de irisscanner.
- **Smart Lock en andere trustagenten**: Met **Blokkeren** voorkomt u dat Smart Lock of andere trustagenten instellingen voor het vergrendelingsscherm van compatibele apparaten aanpassen. Als apparaten zich op een vertrouwde locatie bevinden, kunt u met deze functie, ook wel trustagent genoemd, het vergrendelingsschermwachtwoord op apparaten uitschakelen of overslaan. Hiermee kan bijvoorbeeld het wachtwoord van het werkprofiel worden overgeslagen wanneer apparaten zijn verbonden met een bepaald Bluetooth-apparaat of wanneer deze zich in de buurt van een NFC-tag bevinden. Gebruik deze instelling om te voorkomen dat gebruikers Smart Lock configureren.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

### <a name="system-security"></a>Systeembeveiliging

- **Bedreigingsscan voor apps**: Met **Vereisen** dwingt u af dat de instelling **Apps controleren** wordt ingeschakeld voor werk- en persoonlijke profielen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  Deze instelling is van toepassing op:

  - Android 8 (Oreo) en hoger

- **Voorkomen dat apps uit onbekende bronnen worden geïnstalleerd in het persoonlijke profiel**: Op apparaten met een Android Enterprise-werkprofiel kunnen geen apps worden geïnstalleerd uit andere bronnen dan de Play Store. Met deze instelling krijgen beheerders meer controle over de installatie van apps vanuit onbekende bronnen. **Blokkeren** voorkomt app-installaties in het persoonlijke profiel vanuit andere bronnen dan de Google Play Store. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem app-installaties toestaat die afkomstig zijn van onbekende bronnen in het persoonlijke profiel. Werkprofielapparaten zijn bedoeld voor twee profielen:

  - Een werkprofiel dat wordt beheerd met MDM.
  - Een persoonlijk profiel dat is geïsoleerd van MDM-beheer.

### <a name="connectivity"></a>Connectiviteit

- **Permanente VPN**: Met **Inschakelen** zal een VPN-client automatisch verbinding maken en opnieuw verbinding maken met het VPN. Permanente VPN-verbindingen blijven verbonden. Of maken direct verbinding wanneer gebruikers hun apparaat vergrendelen, het apparaat opnieuw wordt opgestart of het draadloze netwerk wordt gewijzigd.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem AlwaysOn VPN voor alle VPN-clients uitschakelt.

  > [!IMPORTANT]
  > Implementeer slechts één AlwaysOn VPN-beleid per apparaat. Het implementeren van meerdere AlwaysOn VPN-beleidsregels op één apparaat wordt niet ondersteund.

- **VPN-client**: Kies een VPN-client die ondersteuning biedt voor AlwaysOn. Uw opties zijn:
  - Cisco AnyConnect
  - F5-toegang
  - Palo Alto Networks GlobalProtect
  - Pulse Secure
  - Aangepast
    - **Pakket-id**: Voer de pakket-id in van de app in Google Play. Als de URL voor de app in Google Play bijvoorbeeld `https://play.google.com/store/details?id=com.contosovpn.android.prod` is, is de pakket-id `com.contosovpn.android.prod`.

  > [!IMPORTANT]
  > - De VPN-client die u kiest moet op het apparaat worden geïnstalleerd en moet VPN per app in werkprofielen ondersteunen. Anders treedt er een fout op.
  > - U dient de VPN-client-app goed te keuren in de **Beheerde Google Play Store**, de app te synchroniseren naar Intune en de app te implementeren op het apparaat. Nadat u dit hebt gedaan, is de app geïnstalleerd in het werkprofiel van de gebruiker.
  > - Er zijn mogelijk bekende problemen bij het gebruik van VPN per app met F5 Access voor Android 3.0.4. Zie [Releaseopmerkingen voor F5 Access voor Android 3.0.4](https://support.f5.com/kb/en-us/products/big-ip_apm/releasenotes/related/relnote-f5access-android-3-0-4.html#relnotes_known_issues_f5_access_android) voor meer informatie.

- **Vergrendelingsmodus**: Met **Inschakelen** dwingt u af dat al het netwerkverkeer de VPN-tunnel gebruikt. Als er geen VPN-verbinding is ingesteld, heeft het apparaat geen toegang tot het netwerk.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat verkeer via de VPN-tunnel of via het mobiele netwerk gaat.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook kioskprofielen maken voor toegewezen apparaten met [Android](device-restrictions-android.md#kiosk) en [Windows 10](kiosk-settings.md).

[Android Enterprise-apparaten configureren in Microsoft Intune en problemen met deze apparaten oplossen](https://support.microsoft.com/help/4476974).
