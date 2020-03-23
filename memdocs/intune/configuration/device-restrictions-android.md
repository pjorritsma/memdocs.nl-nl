---
title: Apparaatbeperkingsinstellingen voor Android in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk een lijst met alle Android-apparaatinstellingen die u kunt beheren en beperken in Microsoft Intune. Gebruik deze instellingen om het wachtwoord te beheren, Google Play te openen, apps toe te staan of te blokkeren, browserinstellingen te beheren, apps te blokkeren, back-ups te maken in de Google-cloud en de verbindingsopties te beheren voor berichten, spraak, dataroaming, wifi en bluetooth.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/19/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: ayesham, chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a38a7a0e191990871724e217d84c6bd8babb12dc
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361858"
---
# <a name="android-and-samsung-knox-standard-device-restriction-settings-lists-in-intune"></a>Lijsten met apparaatbeperkingen voor Android en Samsung Knox Standard in Intune

In dit artikel komt u meer te weten over de Microsoft Intune-apparaatbeperkingsinstellingen die u kunt configureren voor apparaten met Android.

>[!TIP]
>Als de gewenste instellingen niet beschikbaar zijn, kunt u uw apparaten mogelijk configureren met een [aangepast profiel](custom-settings-android.md).

## <a name="general"></a>Algemeen

- **Camera**: Kies **Blokkeren** om toegang tot de camera te voorkomen. **Niet geconfigureerd**: staat toegang tot de camera van het apparaat toe.
- **Kopiëren en plakken (alleen Samsung Knox)** : Kies **Blokkeren** om kopiëren en plakken te voorkomen. **Niet geconfigureerd**: hiermee worden functies voor kopiëren en plakken toegestaan op het apparaat.
- **Klembord delen tussen apps (alleen Samsung Knox)** : Kies **Blokkeren** om gebruik van het Klembord voor kopiëren en plakken tussen apps te voorkomen. **Niet geconfigureerd**: hiermee staat u het gebruik van het Klembord toe voor kopiëren en plakken tussen apps.
- **Verzenden van diagnostische gegevens (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat de gebruiker bugrapporten vanaf het apparaat verzendt. **Niet geconfigureerd**: staat de gebruiker toe de gegevens te verzenden.
- **Wissen (alleen Samsung Knox)** : Hiermee staat u de gebruiker toe het apparaat te [wissen](../remote-actions/devices-wipe.md).
- **Geolocatie (alleen Samsung Knox)** : Kies **Blokkeren** om het gebruik van locatiegegevens op het apparaat te voorkomen. **Niet geconfigureerd**: hiermee kunnen op het apparaat locatiegegevens worden gebruikt.
- **Uitschakelen (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat de gebruiker het apparaat uitschakelt. Als deze instelling is uitgeschakeld, kan **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist** niet worden ingesteld en werkt deze optie niet. **Niet geconfigureerd**: hiermee staat u toe dat de gebruiker het apparaat mag uitschakelen.
- **Schermafbeelding (alleen Samsung Knox)** : Kies **Blokkeren** om schermopnamen te voorkomen. **Niet geconfigureerd**: stelt de gebruiker in staat om de inhoud van het scherm vast te leggen als afbeelding.
- **Spraakassistent (alleen Samsung Knox)** : Kies **Blokkeren** om de S Voice-service uit te schakelen. **Niet geconfigureerd**: hiermee staat u het gebruik van de S Voice-service en -app toe op het apparaat. Deze instelling geldt niet voor Bixby of de spraakassistent voor toegankelijkheid waarmee inhoud op het scherm hardop wordt voorgelezen.
- **YouTube (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat gebruikers de YouTube-app gebruiken. **Niet geconfigureerd**: staat gebruik van de YouTube-app toe op het apparaat.
- **Gedeelde apparaten (alleen Samsung Knox)** : Configureer een beheerd Samsung Knox Standard-apparaat als gedeeld apparaat. Als deze optie is ingesteld op  **Toestaan**, kunnen eindgebruikers hun Azure AD-referenties gebruiken om zich aan en af te melden bij het apparaat. Het apparaat blijft beheerd, ongeacht of het in gebruik is of niet.</br>Wanneer deze functie wordt gebruikt met een SCEP-certificaatprofiel, zorgt u er hiermee voor dat eindgebruikers een apparaat met dezelfde apps kunnen delen voor alle gebruikers. Elke gebruiker heeft wel een eigen SCEP-gebruikerscertificaat. Wanneer ze zich afmelden, worden alle app-gegevens gewist. Deze functie is beperkt tot LOB-apps. </br>**Niet geconfigureerd**: hiermee wordt voorkomen dat meerdere eindgebruikers zich met hun eigen Azure AD-referenties aanmelden bij de bedrijfsportal-app op het apparaat.
- **Wijzigingen in datum en tijd blokkeren (Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat de gebruiker de datum- en tijdinstellingen op het apparaat kan wijzigen. **Niet geconfigureerd**: staat gebruikers toe om de datum- en tijdinstellingen te wijzigen.

## <a name="password"></a>Wachtwoord

- **Wachtwoord**: **Vereisen** dat de eindgebruiker een wachtwoord invoert voor toegang tot het apparaat. **Niet geconfigureerd**: geeft gebruikers toegang tot het apparaat zonder dat ze een wachtwoord hoeven in te voeren.

    > [!NOTE]
    > Voor Samsung Knox-apparaten is tijdens MDM-inschrijving automatisch een pincode van vier cijfers vereist. Voor systeemeigen Android-apparaten is mogelijk automatisch een pincode vereist om te voldoen aan voorwaardelijke toegang.

- **Minimale wachtwoordlengte**: Voer de minimumlengte van het wachtwoord in dat een gebruiker moet opgeven (tussen 4 en 16 tekens).
- **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**: Voer het maximale aantal minuten van inactiviteit in dat is toegestaan op het apparaat totdat het scherm wordt vergrendeld. Een eindgebruiker kan op een apparaat geen tijdwaarde instellen die groter is dan de geconfigureerde tijd in het profiel. Een eindgebruiker kan een lagere tijdwaarde instellen. Bijvoorbeeld: als het profiel is ingesteld op 15 minuten, kan een eindgebruiker de waarde instellen op 5 minuten. Een eindgebruiker kan de waarde niet instellen op 30 minuten. 
- **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal mislukte aanmeldingen in dat is toegestaan voordat het apparaat wordt gewist.
- **Wachtwoordverlooptijd (dagen)** : Geef op na hoeveel dagen het wachtwoord voor het apparaat moet worden gewijzigd.
- **Vereist wachtwoordtype**: Voer het vereiste complexiteitsniveau voor het wachtwoord in en geef aan of biometrische apparaten kunnen worden gebruikt. Uw opties zijn:
  - **Standaardwaarde apparaat**
  - **Lage beveiligingsbiometrie**
  - **Ten minste numeriek**
  - **Complex numeriek**: Herhaalde of opeenvolgende cijfers, zoals '1111' of '1234', zijn niet toegestaan.<sup>1</sup>
  - **Ten minste alfabetisch**
  - **Ten minste alfanumeriek**
  - **Minstens alfanumeriek met symbolen**
- **Wachtwoorden niet opnieuw gebruiken**: Hiermee voorkomt u dat eindgebruikers een wachtwoord kunnen opgeven dat zij al eerder hebben gebruikt.
- **Ontgrendelen met vingerafdruk (alleen Samsung Knox)** : Selecteer **Blokkeren** om te voorkomen dat vingerafdrukken kunnen worden gebruikt om het apparaat te ontgrendelen. **Niet geconfigureerd**: staat de gebruiker toe het apparaat te ontgrendelen met een vingerafdruk.
- **Smart Lock en andere trustagenten**: Kies **Blokkeren** als u wilt voorkomen dat Smart Lock of andere vertrouwde agenten instellingen voor het vergrendelingsscherm aanpassen (Samsung Knox Standard 5.0+). Met deze telefoonfunctie, ook wel een vertrouwensagent genoemd, kunt u het wachtwoord voor het vergrendelingsscherm op het apparaat uitschakelen of overslaan als het apparaat zich op een vertrouwde locatie bevindt. Deze functie kan bijvoorbeeld worden gebruikt wanneer het apparaat is verbonden met een bepaald Bluetooth-apparaat of wanneer het zich in de buurt van een NFC-tag bevindt. U kunt deze instelling gebruiken om te voorkomen dat gebruikers Smart Lock configureren.
- **Versleuteling**: Kies **Vereisen** om bestanden op het apparaat te versleutelen. Niet alle apparaten ondersteunen versleuteling. Om deze functie te gebruiken, moet u ook het volgende doen: 
  1. Stel **Wachtwoord** in op **Vereisen**.
  2. Stel **Vereist wachtwoordtype** in op **Ten minste numeriek**.
  3. Stel **Minimale wachtwoordlengte** in op ten minste 4 om naleving voor deze instelling juist te rapporteren.

  > [!NOTE]
  > Als er een versleutelingsbeleid van kracht is, moeten gebruikers van Samsung Knox-apparaten een complex wachtwoord van zes tekens instellen als wachtwoordcode voor het apparaat.

<sup>1</sup> Voordat u deze instelling aan apparaten toewijst, moet u controleren of de bedrijfsportal-app op deze apparaten is bijgewerkt naar de nieuwste versie.

Als u  **Vereist wachtwoordtype** instelt op **Numeriek complex** en het beleid vervolgens toewijst aan een apparaat waarop een versie van Android eerder dan 5.0 wordt uitgevoerd, is het volgende van toepassing:

- Als er een eerdere versie dan versie 1704 van de bedrijfsportal-app wordt uitgevoerd, wordt er geen pincodebeleid toegepast op het apparaat en wordt er een foutmelding weergegeven in het Microsoft Endpoint Manager-beheercentrum.
- Als versie 1704 of later wordt uitgevoerd, kan er alleen een eenvoudig pincode worden toegepast. Versies van Android die ouder zijn dan 5.0 bieden geen ondersteuning voor deze instelling. Er wordt geen fout weergegeven in het Microsoft Endpoint Manager-beheercentrum.

## <a name="google-play-store"></a>Google Play Store

- **Google Play Store (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat gebruikers Google Play Store gebruiken. **Niet geconfigureerd**: hiermee staat u toe dat de gebruiker toegang heeft tot de Google Play Store op het apparaat.

## <a name="restricted-apps"></a>Beperkte apps

Gebruik deze instellingen om bepaalde apps op het apparaat toe te staan of te blokkeren. Deze functie wordt ondersteund op Android- en Samsung Knox Standard-apparaten:

- **Niet-toegestane apps**: Een lijst met apps die niet worden beheerd in Intune waarvan u niet wilt dat deze op het apparaat worden geïnstalleerd. Als een gebruiker een app uit deze lijst installeert, ontvangt u een melding van Intune.
- **Goedgekeurde apps**: Een lijst met apps die gebruikers mogen installeren. Om te voldoen aan het beleid, mogen gebruikers geen andere apps installeren. Apps die worden beheerd door Intune, zijn automatisch toegestaan.

Als u apps wilt toevoegen aan deze lijsten, kunt u:

- De Google Play Store-URL van de gewenste app **toevoegen**. Als u bijvoorbeeld de app voor het Extern bureaublad van Microsoft voor Android wilt toevoegen, voert u `https://play.google.com/store/apps/details?id=com.microsoft.rdc.android` in. Als u de URL van een app wilt vinden, opent u de [Google Play Store](https://play.google.com/store/apps) en zoekt u de app. Zoek bijvoorbeeld naar `Microsoft Remote Desktop Play Store` of `Microsoft Planner`. Selecteer de app en kopieer de URL.
- Importeer een CSV-bestand met details over de app, inclusief de URL. Gebruik de indeling <*app-url*>, <*appnaam*>, <*app-uitgever*>. Of een bestaande lijst **exporteren** die de beperkte apps bevat in dezelfde indeling.

> [!IMPORTANT]
> Apparaatprofielen die instellingen voor beperkte apps gebruiken, moeten worden toegewezen aan groepen gebruikers.

## <a name="browser"></a>Browser

- **Webbrowser (alleen Samsung Knox )** : Kies **Blokkeren** om te voorkomen dat de standaardwebbrowser op het apparaat wordt gebruikt. **Niet geconfigureerd**: hiermee kan de standaardwebbrowser van het apparaat worden gebruikt.
- **Automatisch invullen (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat tekst automatisch wordt ingevuld in de browser. **Niet geconfigureerd**: hiermee staat u het gebruik van de functie voor automatisch invullen van de webbrowser toe.
- **Cookies (alleen Samsung Knox)** : geef aan hoe u cookies van websites wilt afhandelen op het apparaat. Uw opties zijn:
  - Toestaan
  - Alle cookies blokkeren
  - Cookies van bezochte websites toestaan
  - Cookies van huidige website toestaan
- **JavaScript (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat er Java-scripts worden uitgevoerd in de browser. **Niet geconfigureerd**: hiermee staat u toe dat de webbrowser Java-scripts uitvoert op het apparaat.
- **Pop-ups (alleen Samsung Knox)** : kies **Blokkeren** om de weergave van pop-ups in de webbrowser te voorkomen. Met **Niet geconfigureerd** zijn pop-ups toegestaan in de webbrowser.

## <a name="allow-or-block-apps"></a>Apps toestaan of blokkeren

Gebruik deze instellingen om specifieke apps toe te staan, te blokkeren of te verbergen voor Samsung Knox Standard-apparaten. Apps die verborgen zijn, kunnen niet worden geopend of worden uitgevoerd door de gebruiker.

Uw opties zijn:

- **Apps die mogen worden geïnstalleerd (alleen Samsung Knox Standard)**
- **Apps die nu kunnen worden geopend (alleen Samsung Knox Standard)**
- **Apps die verborgen zijn voor de gebruiker (alleen Samsung Knox Standard)**

Voeg voor elke instelling een lijst met apps toe. Uw opties zijn:

- **Apps toevoegen op pakketnaam**: Primair gebruikt voor line-of-business-apps. Vul de naam van de app en de naam van het app-pakket in.
- **Apps toevoegen op URL**: Voer de naam van de app en de URL in de Google Play Store in.
- **Store-app toevoegen**: Selecteer een app in de bestaande lijst met apps die u in Intune beheert.

## <a name="cloud-and-storage"></a>Cloud en opslag

- **Google-back-up (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat het apparaat wordt gesynchroniseerd met Google-back-up. **Niet geconfigureerd**: hiermee staat u het gebruik van Google-back-up toe.
- **Google-account automatisch synchroniseren (alleen Samsung Knox)** : Kies **Blokkeren** om de functie voor automatische synchronisatie van het Google-account op het apparaat te blokkeren. **Niet geconfigureerd**: toestaan dat instellingen voor Google-accounts automatisch worden gesynchroniseerd.
- **Verwisselbare opslag (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat op het apparaat verwisselbare opslag wordt gebruikt. **Niet geconfigureerd**: hiermee staat u het gebruik toe van verwisselbare opslag, zoals een SD-kaart, op het apparaat.
- **Versleuteling voor opslagkaarten (alleen Samsung Knox)** : Met **Vereisen** dwingt u af dat opslagkaarten moeten worden versleuteld. **Niet geconfigureerd**: hiermee kunnen niet-versleutelde opslagkaarten worden gebruikt. Niet alle apparaten ondersteunen versleuteling van opslagkaarten. Neem voor meer informatie contact op met de fabrikant van het apparaat.

## <a name="cellular-and-connectivity"></a>Mobiel en connectiviteit

- **Dataroaming (alleen Samsung Knox)** : Selecteer **Blokkeren** om dataroaming via het mobiele netwerk te voorkomen. **Niet geconfigureerd**: staat dataroaming toe wanneer het apparaat verbinding heeft met een mobiel netwerk.
- **Sms-/mms-berichten (alleen Samsung Knox)** : Kies **blokkeren** om berichten op het apparaat te voorkomen. **Niet geconfigureerd**: hiermee staat u het gebruik van sms- en mms-berichten toe op het apparaat.
- **Nummer inspreken (alleen Samsung Knox)** : Selecteer **Blokkeren** om te voorkomen dat gebruikers de functie Voicedialing op het apparaat kunnen gebruiken. **Niet geconfigureerd**: hiermee wordt Nummer inspreken toegestaan op het apparaat.
- **Spraakroaming (alleen Samsung Knox)** : Selecteer **Blokkeren** om gespreksroaming via het mobiele netwerk te voorkomen. **Niet geconfigureerd**: staat spraakroaming toe wanneer het apparaat verbinding heeft met een mobiel netwerk.
- **Bluetooth (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat Bluetooth wordt gebruikt op het apparaat. **Niet geconfigureerd**: hiermee kan de gebruiker Bluetooth op het apparaat gebruiken.
- **NFC (alleen Samsung Knox)** : Kies **Blokkeren** om de NFC-technologie (Near Field Communication) te stoppen. **Niet geconfigureerd**: hiermee staat u bewerkingen toe waarvoor NFC wordt gebruikt op ondersteunde apparaten.
- **Wi-Fi (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat Wi-Fi wordt gebruikt op het apparaat. **Niet geconfigureerd**: staat het gebruik van Wi-Fi-functies toe op het apparaat.
- **Wi-Fi-tethering (alleen Samsung Knox)** : Kies **Blokkeren** om te voorkomen dat Wi-Fi-tethering wordt gebruikt op het apparaat. **Niet geconfigureerd**: hiermee wordt het gebruik van Wi-Fi-tethering op het apparaat toegestaan.

## <a name="kiosk"></a>Kiosk

Kioskinstellingen zijn alleen van toepassing op apparaten met Samsung Knox Standard en alleen op apps die u beheert via Intune.

- Voeg apps toe die moeten worden uitgevoerd wanneer het apparaat in de kiosk-modus staat. In de kiosk-modus worden alleen de apps uitgevoerd die u toevoegt. Apps die niet zijn toegevoegd, worden niet uitgevoerd. Vooraf geïnstalleerde browsers worden niet uitgevoerd als een app wanneer het apparaat in de kiosk-modus staat. Als een browser is vereist, kunt u overwegen de [Managed Browser](../apps/app-configuration-managed-browser.md) te gebruiken.

  Opties voor uw app:

  - **Apps toevoegen op pakketnaam**: Primair gebruikt voor line-of-business-apps. Vul de naam van de app en de naam van het app-pakket in.
  - **Apps toevoegen op URL**: Voer de naam van de app en de URL in de Google Play Store in.
  - **Store-app toevoegen**: Selecteer een app in de bestaande lijst met apps die u in Intune beheert.

- **Schermsluimerknop**: Kies **Blokkeren** om te voorkomen dat de schermsluimerknop wordt gebruikt of om de knop te verbergen. **Niet geconfigureerd**: hiermee kan de knop voor de slaapstand/activeren van het scherm worden gebruikt op het apparaat.
- **Volumeknoppen**: Kies **Blokkeren** om te voorkomen dat de gebruiker het volume aanpast door de volumeknoppen uit te schakelen. **Niet geconfigureerd**: staat gebruik van de volumeknoppen toe op het apparaat.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook kiosk-profielen maken voor apparaten met [Android Enterprise](device-restrictions-android-for-work.md#dedicated-device-settings) en [Windows 10](kiosk-settings.md).