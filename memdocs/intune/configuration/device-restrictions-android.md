---
title: Apparaatbeperkingsinstellingen voor Android in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk een lijst met alle Android-apparaatbeheerinstellingen die u kunt beheren en beperken in Microsoft Intune. Gebruik deze instellingen om het wachtwoord te beheren, Google Play te openen, apps toe te staan of te blokkeren, browserinstellingen te beheren, apps te blokkeren, back-ups te maken in de Google-cloud en de verbindingsopties te beheren voor berichten, spraak, dataroaming, wifi en bluetooth.
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
ms.reviewer: chmaguir, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4afc27680c464f67756340ebcb0958887ae6f795
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407878"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Lijsten met apparaatbeperkingen voor Android en Samsung Knox Standard in Intune

In dit artikel komt u meer te weten over de Microsoft Intune-apparaatbeperkingsinstellingen die u kunt configureren voor apparaten met Android.

>[!TIP]
>Als de gewenste instellingen niet beschikbaar zijn, kunt u uw apparaten mogelijk configureren met een [aangepast profiel](custom-settings-android.md).

## <a name="before-you-begin"></a>Voordat u begint

[Maak een apparaatconfiguratieprofiel](device-restrictions-configure.md).

## <a name="general"></a>Algemeen

- **Camera**: Met **Blokkeren** voorkomt u dat toegang wordt verkregen tot de camera van het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toegang tot de camera van het apparaat toestaan.

  Intune beheert alleen de toegang tot de camera van het apparaat. Het heeft geen toegang tot afbeeldingen of video's.

- **Kopiëren en plakken (alleen Samsung Knox)** : **Blokkeren** voorkomt dat wordt gekopieerd en geplakt. **Niet geconfigureerd** staat de functies voor kopiëren en plakken op het apparaat toe.
- **Klembord delen tussen apps (alleen Samsung Knox)** : **Blokkeren** voorkomt dat het klembord wordt gebruikt voor kopiëren en plakken tussen apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de functies voor kopiëren en plakken op apparaten toestaan.
- **Verzenden van diagnostische gegevens (alleen Samsung Knox)** : **Blokkeren** voorkomt dat gebruikers foutrapporten verzenden vanaf apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat de gebruikers gegevens verzenden.
- **Wissen (alleen Samsung Knox)** : Staat gebruikers toe een actie voor [wissen](../remote-actions/devices-wipe.md) uit te voeren op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Geolocatie (alleen Samsung Knox)** : **Blokkeren** voorkomt dat apparaten locatiegegevens gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat apparaten de locatiegegevens gebruiken.
- **Uitschakelen (alleen Samsung Knox)** : **Blokkeren** voorkomt dat gebruikers het apparaat uitschakelen. Ook wordt voorkomen dat de instelling **Aantal mislukte aanmeldingen voordat het apparaat wordt gewist** wordt geconfigureerd en werkt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers apparaten uitschakelen.
- **Schermafbeelding (alleen Samsung Knox)** : **Blokkeren** voorkomt dat schermopnamen worden gemaakt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers de scherminhoud vastleggen als een afbeelding.
- **Spraakassistent (alleen Samsung Knox)** : **Blokkeren** schakelt de S Voice-service uit. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat de S Voice-service en -app op apparaten worden gebruikt. Deze instelling geldt niet voor Bixby of de spraakassistent voor toegankelijkheid waarmee inhoud op het scherm hardop wordt voorgelezen.
- **YouTube (alleen Samsung Knox)** : **Blokkeren** voorkomt dat gebruikers de YouTube-app gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat de YouTube-app op apparaten wordt gebruikt.
- **Gedeelde apparaten (alleen Samsung Knox)** : Configureer een beheerd Samsung Knox Standard-apparaat als gedeeld apparaat. **Toestaan** stelt gebruikers in staat om zich op apparaten aan- en af te melden met hun Azure AD-referenties. Apparaten blijven beheerd, ongeacht of ze al dan niet worden gebruikt.

  Wanneer deze functie wordt gebruikt met een SCEP-certificaatprofiel, kunnen gebruikers een apparaat met dezelfde apps voor alle gebruikers delen. Elke gebruiker heeft wel een eigen SCEP-gebruikerscertificaat. Wanneer ze zich afmelden, worden alle app-gegevens gewist. Deze functie is beperkt tot LOB-apps.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard voorkomen dat meerdere gebruikers zich bij de bedrijfsportal-app op apparaten aanmelden met hun Azure AD-referenties.
- **Wijzigingen in datum en tijd blokkeren (Samsung Knox)** : **Blokkeren** voorkomt dat gebruikers de instellingen voor datum en tijd op apparaten wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers de instellingen voor datum en tijd wijzigen.

## <a name="password"></a>Wachtwoord

- **Wachtwoord**: **Vereisen** dat gebruikers een wachtwoord invoeren om toegang te krijgen tot apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers toegang verkrijgen tot apparaten zonder dat zij een wachtwoord invoeren.

    > [!NOTE]
    > Voor Samsung Knox-apparaten is tijdens MDM-inschrijving automatisch een pincode van vier cijfers vereist. Voor systeemeigen Android-apparaten is mogelijk automatisch een pincode vereist om te voldoen aan voorwaardelijke toegang.

- **Minimale wachtwoordlengte**: Voer het minimum aantal vereiste tekens (tussen 4 en 16 tekens) in. Voer bijvoorbeeld `6` in om in te stellen dat een wachtwoord minimaal zes cijfers of tekens moet bevatten.
- **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**: Voer de tijdsduur in gedurende welke een apparaat inactief moet zijn voordat het scherm automatisch wordt vergrendeld. Voer bijvoorbeeld `5` in om apparaten te vergrendelen nadat deze vijf minuten lang inactief zijn geweest. Wanneer de waarde leeg is of is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  Gebruikers kunnen op een apparaat geen tijdwaarde instellen die groter is dan de geconfigureerde tijd in het profiel. Gebruikers kunnen een lagere tijdwaarde instellen. Als het profiel bijvoorbeeld is ingesteld op `15` minuten, kunnen gebruikers de waarde instellen op 5 minuten. Gebruikers kunnen de waarde niet instellen op 30 minuten.

- **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal onjuiste wachtwoorden (tussen 4 en 11) in dat is toegestaan voordat apparaten worden gewist. Met `0` (nul) kan de functionaliteit voor het wissen van apparaten worden uitgeschakeld. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Wachtwoordverlooptijd (dagen)** : Geef het aantal dagen, tussen 1 en 365, op waarna het wachtwoord voor het apparaat moet worden gewijzigd. Voer bijvoorbeeld `90` als u wilt dat het wachtwoord na 90 dagen verloopt. Wanneer het wachtwoord is verlopen, wordt gebruikers gevraagd een nieuw wachtwoord te maken. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Vereist wachtwoordtype**: Voer het vereiste complexiteitsniveau voor het wachtwoord in en geef aan of biometrische apparaten kunnen worden gebruikt. Uw opties zijn:
  - **Standaardwaarde apparaat**
  - **Lage beveiligingsbiometrie**: [Sterke versus zwakke biometrie](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (hiermee wordt een Android-website geopend)
  - **Ten minste numeriek**: Bevat numerieke tekens, zoals `123456789`.
  - **Complex numeriek**: Herhaalde of opeenvolgende cijfers, zoals '1111' of '1234', zijn niet toegestaan. Voordat u deze instelling aan apparaten toewijst, moet u ervoor zorgen dat de bedrijfsportal-app op deze apparaten is bijgewerkt naar de nieuwste versie.

    Wanneer deze optie is ingesteld op **Complex numeriek** en u de instelling toewijst aan apparaten met een Android-versie die ouder is dan 5.0, is het volgende van toepassing:

    - Als er een eerdere versie dan versie 1704 van de bedrijfsportal-app wordt uitgevoerd, wordt er geen pincodebeleid toegepast op apparaten en wordt er een foutmelding weergegeven in het Microsoft Endpoint Manager-beheercentrum.
    - Als versie 1704 of later wordt uitgevoerd, kan er alleen een eenvoudig pincode worden toegepast. Versies van Android die ouder zijn dan 5.0 bieden geen ondersteuning voor deze instelling. Er wordt geen fout weergegeven in het Microsoft Endpoint Manager-beheercentrum.

  - **Ten minste alfabetisch**: Bevat letters uit het alfabet. Er zijn geen cijfers en symbolen vereist.
  - **Ten minste alfanumeriek**: Dit zijn hoofdletters, kleine letters en numerieke tekens.
  - **Ten minste alfanumeriek met symbolen**: Dit zijn hoofdletters, kleine letters, numerieke tekens, leestekens en symbolen.

- **Wachtwoorden niet opnieuw gebruiken**: Gebruik deze instelling om te voorkomen dat gebruikers eerder gebruikte wachtwoorden hergebruiken. Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld `5` invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Ontgrendelen met vingerafdruk (alleen Samsung Knox)** : **Blokkeren** voorkomt het gebruik van een vingerafdruk om apparaten te ontgrendelen. Als deze optie is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers apparaten ontgrendelen met een vingerafdruk.
- **Smart Lock en andere trustagenten**: **Blokkeren** voorkomt dat de instellingen voor het vergrendelingsscherm kunnen worden aangepast door Smart Lock of andere trustagenten. Als het apparaat zich op een vertrouwde locatie bevindt, kunt u met deze functie, ook wel trustsagent genoemd, het vergrendelingsschermwachtwoord op het apparaat uitschakelen of overslaan. Gebruik deze functie bijvoorbeeld wanneer apparaten zijn verbonden met een bepaald Bluetooth-apparaat of wanneer ze zich in de buurt van een NFC-tag bevinden. U kunt deze instelling gebruiken om te voorkomen dat gebruikers Smart Lock configureren.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  Deze instelling is van toepassing op:

  - Samsung KNOX Standard 5.0+

- **Versleuteling**: Kies **Vereisen** om bestanden op het apparaat te versleutelen. Niet alle apparaten ondersteunen versleuteling. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Als u deze instelling wilt configureren en de naleving op juiste wijze wilt rapporteren, moet u ook het volgende configureren:
  1. **Wachtwoord**: Stel dit in op **Vereisen**.
  2. **Vereist wachtwoordtype**: Stel dit in op **Ten minste numeriek**.
  3. **Minimale wachtwoordlengte**: Stel dit in op ten minste `4`.

  > [!NOTE]
  > Als er een versleutelingsbeleid van kracht is, moeten gebruikers van Samsung Knox-apparaten een complex wachtwoord van zes tekens instellen als wachtwoordcode voor het apparaat.

## <a name="google-play-store"></a>Google Play Store

- **Google Play Store (alleen Samsung Knox)** : **Blokkeren** voorkomt dat gebruikers Google Play Store gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat gebruikers toegang krijgen tot Google Play Store op apparaten.

## <a name="restricted-apps"></a>Beperkte apps

Gebruik deze instellingen om bepaalde apps op apparaten toe te staan of te blokkeren. Deze functie wordt ondersteund op Android- en Samsung Knox Standard-apparaten.

- **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
- **Niet-toegestane apps**: Hiermee maakt u een lijst met apps die niet worden beheerd door Intune en die gebruikers niet mogen installeren en uitvoeren. Als een gebruiker een app uit deze lijst installeert, ontvangt u een melding van Intune.
- **Goedgekeurde apps**: Hiermee maakt u een lijst met apps die gebruikers mogen installeren. Om te voldoen aan het beleid, mogen gebruikers geen andere apps installeren.  Apps die worden beheerd door Intune worden automatisch toegestaan, zoals de bedrijfsportal-app.
- **Apps-lijst**: U moet uw app **toevoegen**:
  - **App-bundel-id**: Voer de bundel-id van de app in.
  - **URL van de App Store**: Voer de Google Play Store-URL van de gewenste app in. Als u bijvoorbeeld de app voor het Extern bureaublad van Microsoft voor Android wilt toevoegen, voert u `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android` in.

    Als u de URL van een app wilt vinden, opent u de [Google Play Store](https://play.google.com/store/apps) en zoekt u de app. Zoek bijvoorbeeld naar `Microsoft Remote Desktop Play Store` of `Microsoft Planner`. Selecteer de app en kopieer de URL.
  
  - **App-naam**: Voer de gewenste naam in. Deze naam wordt weergegeven voor gebruikers.
  - **Uitgever** (optioneel): Voer de uitgever van de app in, zoals `Microsoft`.

U kunt ook een CSV-bestand **importeren** met details van de app, zoals de URL. Gebruik de indeling <*app-url*>, <*appnaam*>, <*app-uitgever*>. Of een bestaande lijst **exporteren** die de beperkte apps bevat in dezelfde indeling.

> [!IMPORTANT]
> Apparaatprofielen die instellingen voor beperkte apps gebruiken, moeten worden toegewezen aan gebruikersgroepen, niet aan apparaatgroepen.

## <a name="browser"></a>Browser

- **Webbrowser (alleen Samsung Knox )** : **Blokkeren** voorkomt dat de standaardwebbrowser op apparaten wordt gebruikt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat de standaardwebbrowser van het apparaat wordt gebruikt.
- **Automatisch invullen (alleen Samsung Knox)** : **Blokkeren** voorkomt dat de browser automatisch tekst invult. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard automatisch aanvullen toestaan.
- **Cookies (alleen Samsung Knox)** : Kies hoe cookies van websites op apparaten moeten worden verwerkt. Uw opties zijn:
  - Toestaan
  - Alle cookies blokkeren
  - Cookies van bezochte websites toestaan
  - Cookies van huidige website toestaan
- **JavaScript (alleen Samsung Knox)** : **Blokkeren** voorkomt dat JavaScript wordt uitgevoerd in de browser. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard deze scripts toestaan.
- **Pop-ups (alleen Samsung Knox)** : **Blokkeren** schakelt de pop-upblokkering in zodat er geen pop-ups worden weergegeven in de webbrowser. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard pop-ups toestaan.

## <a name="allow-or-block-apps"></a>Apps toestaan of blokkeren

Gebruik deze instellingen om specifieke apps toe te staan, te blokkeren of te verbergen voor Samsung Knox Standard-apparaten. Apps die verborgen zijn, kunnen niet door gebruikers worden geopend of uitgevoerd.

Uw opties zijn:

- **Apps die mogen worden geïnstalleerd (alleen Samsung Knox Standard)** : Voeg apps toe die gebruikers kunnen installeren. Gebruikers kunnen geen apps installeren die niet in de lijst worden vermeld.
- **Apps waarvoor het starten is geblokkeerd (alleen Samsung Knox Standard)** : Voer de apps in die gebruikers niet op hun apparaat kunnen uitvoeren.
- **Apps die verborgen zijn voor de gebruiker (alleen Samsung Knox Standard)** : Voer de apps in die verborgen moeten worden op apparaten. Gebruikers kunnen deze apps niet vinden of uitvoeren.

Voeg voor elke instelling uw apps toe:

- **Apps toevoegen op pakketnaam**: Vul de naam van de app en de naam van het app-pakket in. Primair gebruikt voor line-of-business-apps. 
- **Apps toevoegen op URL**: Voer de naam van de app en de URL in de Google Play Store in.
- **Store-app toevoegen**: Selecteer een app in de bestaande lijst met apps die u in Intune beheert.

## <a name="cloud-and-storage"></a>Cloud en opslag

- **Google-back-up (alleen Samsung Knox)** : **Blokkeren** voorkomt dat apparaten worden gesynchroniseerd met Google-back-up. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard het gebruik van Google-back-up toestaan.
- **Google-account automatisch synchroniseren (alleen Samsung Knox)** : **Blokkeren** voorkomt de functie voor automatische synchronisatie van het Google-account. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat instellingen van Google-accounts automatisch worden gesynchroniseerd.
- **Verwisselbare opslag (alleen Samsung Knox)** : **Blokkeren** voorkomt dat apparaten gebruikmaken van verwisselbare opslag. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat apparaten gebruikmaken van verwisselbare opslag, zoals een SD-kaart.
- **Versleuteling voor opslagkaarten (alleen Samsung Knox)** : Met **Vereisen** dwingt u af dat opslagkaarten moeten worden versleuteld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toestaan dat niet-versleutelde opslagkaarten worden gebruikt. Niet alle apparaten ondersteunen versleuteling van opslagkaarten. Neem voor meer informatie contact op met de fabrikant van het apparaat.

## <a name="cellular-and-connectivity"></a>Mobiel en connectiviteit

- **Dataroaming (alleen Samsung Knox)** : **Blokkeren** voorkomt dataroaming via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard dataroaming toestaan.
- **Sms-/mms-berichten (alleen Samsung Knox)** : **Blokkeren** voorkomt tekstberichten op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard het gebruik van sms-/mms-berichten toestaan.
- **Nummer inspreken (alleen Samsung Knox)** : **Blokkeren** voorkomt dat gebruikers de functie voor het inspreken van nummers kunnen gebruiken op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard het inspreken van nummers toestaan.
- **Spraakroaming (alleen Samsung Knox)** : **Blokkeren** voorkomt spraakroaming via het mobiele netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard spraakroaming toestaan.
- **Bluetooth (alleen Samsung Knox)** : **Blokkeren** voorkomt dat Bluetooth wordt gebruikt op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard het gebruik van Bluetooth toestaan.
- **NFC (alleen Samsung Knox)** : **Blokkeren** schakelt bewerkingen uit waarbij Near Field Communication (NFC) wordt gebruikt op apparaten die dit ondersteunen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard NFC-bewerkingen toestaan.
- **Wi-Fi (alleen Samsung Knox)** : **Blokkeren** voorkomt dat Wi-Fi wordt gebruikt op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard het gebruik van Wi-Fi toestaan.
- **Wi-Fi-tethering (alleen Samsung Knox)** : **Blokkeren** voorkomt dat Wi-Fi-tethering wordt gebruikt op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard het gebruik van Wi-Fi-tethering toestaan.

## <a name="kiosk"></a>Kiosk

Kioskinstellingen zijn alleen van toepassing op apparaten met Samsung Knox Standard en alleen op apps die u beheert via Intune.

- Voeg apps toe die moeten worden uitgevoerd wanneer het apparaat in de kiosk-modus staat. In de kiosk-modus worden alleen de apps uitgevoerd die u toevoegt. Apps die niet zijn toegevoegd, worden niet uitgevoerd. Vooraf geïnstalleerde browsers worden niet uitgevoerd als een app wanneer het apparaat in de kiosk-modus staat. Als een browser is vereist, kunt u overwegen de [Managed Browser](../apps/app-configuration-managed-browser.md) te gebruiken.

  Opties voor uw app:

  - **Apps toevoegen op pakketnaam**: Primair gebruikt voor line-of-business-apps. Vul de naam van de app en de naam van het app-pakket in.
  - **Apps toevoegen op URL**: Voer de naam van de app en de URL in de Google Play Store in.
  - **Store-app toevoegen**: Selecteer een app in de bestaande lijst met apps die u in Intune beheert.

- **Schermsluimerknop**: **Blokkeren** voorkomt of verbergt de schermsluimerknop. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de schermsluimerknop toestaan op apparaten.
- **Volumeknoppen**: **Blokkeren** voorkomt dat gebruikers het volume aanpassen door de volumeknoppen uit te schakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard het gebruik van de volumeknoppen toestaan op apparaten.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook kiosk-profielen maken voor apparaten met [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) en [Windows 10](kiosk-settings.md).
