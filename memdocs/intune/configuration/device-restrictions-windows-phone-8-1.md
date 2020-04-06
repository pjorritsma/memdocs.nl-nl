---
title: Microsoft Intune-apparaatbeperkingsinstellingen voor Windows Phone 8.1
titleSuffix: ''
description: Meer informatie over de Intune-instellingen die u kunt gebruiken voor het beheren van apparaatinstellingen en functionaliteit op apparaten met Windows Phone 8.1.
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
ms.openlocfilehash: 285144e42f2a029bf2d24b96493c54922727d6dc
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407649"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Microsoft Intune Windows Phone 8.1-apparaatbeperkingsinstellingen

In dit artikel komt u meer te weten over de Microsoft Intune-apparaatbeperkingsinstellingen die u kunt configureren voor apparaten met Windows Phone 8.1.

## <a name="general"></a>Algemeen

- **Camera**: Met **Blokkeren** voorkomt u dat toegang wordt verkregen tot de camera van het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  Intune beheert alleen de toegang tot de camera van het apparaat. Het heeft geen toegang tot afbeeldingen of video's.

- **Kopiëren en plakken**: Met **Blokkeren** kan er niet worden gekopieerd en geplakt tussen apps op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Verwisselbare opslag**: Met **Blokkeren** voorkomt u dat externe opslagapparaten, zoals SD-kaarten, kunnen worden gebruikt op apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Geolocatie**: Met **Blokkeren** voorkomt u dat locatieservices op apparaten kunnen worden ingeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Microsoft-account**: Met **Blokkeren** kunnen gebruikers geen Microsoft-account aan het apparaat koppelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Schermopname**: Met **Blokkeren** kunnen geen schermopnamen op apparaten worden gemaakt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Verzending van diagnostische gegevens**: Met **Blokkeren** kunnen apparaten geen diagnostische gegevens en telemetriegegevens over het gebruik naar Microsoft sturen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Aangepaste e-mailaccounts synchroniseren**: Met **Blokkeren** kunnen apparaten geen verbinding maken met niet-Microsoft-e-mailaccounts. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="password"></a>Wachtwoord

- **Wachtwoord**: Met **Vereisen** moeten gebruikers een wachtwoord invoeren om toegang te krijgen tot apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Is alleen van toepassing op lokale accounts. Wachtwoorden van domeinaccounts blijven geconfigureerd door Active Directory (AD) en Azure AD.
  - **Vereist wachtwoordtype**: Kies het type wachtwoord. Uw opties zijn:
    - **Standaardwaarde apparaat**: Het wachtwoord kan cijfers en letters bevatten.
    - **Alfanumeriek**: Het wachtwoord moet een combinatie van cijfers en letters zijn.
    - **Numeriek**: Het wachtwoord mag alleen uit cijfers bestaan.
  - **Minimale wachtwoordlengte**: Voer het minimumaantal vereiste tekens (tussen 4 en 16 tekens) in. Voer bijvoorbeeld `6` in om in te stellen dat een wachtwoord minimaal 6 tekens bevat.
  - **Eenvoudige wachtwoorden**: Met **Blokkeren** voorkomt u dat gebruikers eenvoudige wachtwoorden kunnen maken, zoals `1234` of `1111`. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal onjuiste wachtwoorden in dat is toegestaan voordat apparaten worden gewist.
  - **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**: Voer de tijdsduur in gedurende welke een apparaat inactief moet zijn voordat het scherm automatisch wordt vergrendeld. Voer bijvoorbeeld `5` in om apparaten te vergrendelen nadat deze vijf minuten lang inactief zijn geweest. Wanneer dit is ingesteld op **Niet geconfigureerd** of leeg wordt gelaten, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Wachtwoordverlooptijd (dagen)** : Voer de tijdsduur (tussen 1 en 255 dagen) in waarna het wachtwoord van een apparaat moet worden gewijzigd. Voer bijvoorbeeld `90` als u wilt dat het wachtwoord na 90 dagen verloopt. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Wachtwoorden niet opnieuw gebruiken**: Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld `5` invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Versleuteling**: Met **Vereisen** is versleuteling op het apparaat, inclusief voor bestanden, vereist. Niet alle apparaten ondersteunen versleuteling. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Als u deze instelling wilt configureren en de naleving op juiste wijze wilt rapporteren, moet u ook het volgende configureren:
  - **Wachtwoord vereisen**: Stel dit in op **Vereisen**.
  - **Vereist wachtwoordtype**: Stel dit in op ten minste **Numeriek**.
  - **Minimale wachtwoordlengte**: Stel dit in op ten minste `4`.

## <a name="app-store"></a>App Store

- **App Store**: Met **Blokkeren** voorkomt u dat gebruikers toegang hebben tot de App Store. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="restricted-apps"></a>Beperkte apps

Configureer een van de volgende lijsten in de lijst met beperkte apps:

- **Geblokkeerde apps**: Hiermee maakt u een lijst met apps die niet worden beheerd door Intune en die gebruikers niet mogen installeren en uitvoeren.
- **Toegestane apps**: Hiermee maakt u een lijst met apps die gebruikers mogen installeren. Apps die worden beheerd door Intune, zijn automatisch toegestaan.

Als u de lijst wilt configureren, klikt u op **Toevoegen** en geeft u een naam van uw keuze op, eventueel de uitgever van de app, en de URL van de app in de App Store.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>De URL naar een app in de Store opgeven

Als u een app-URL wilt opgeven in de lijst met toegestane en geblokkeerde apps, gebruikt u de volgende notatie:

Zoek op de pagina [Windows Phone Store](https://www.microsoft.com/store/apps/windows-phone) naar de app die u wilt gebruiken.

Open de pagina van de app en kopieer de URL naar het klembord. U kunt deze URL nu gebruiken in de lijst met toegestane apps of de lijst met geblokkeerde apps.

Voorbeeld: Zoek in de store naar de Skype-app. De URL die u gebruikt, is `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### <a name="additional-options"></a>Extra opties

U kunt ook op **Importeren** klikken om de lijst te vullen met waarden uit een CSV-bestand in de indeling <*app-URL*>, <*app-naam*>, <*app-uitgever*>. Of klik op **Exporteren** om een CSV-bestand (met dezelfde indeling) te maken met de inhoud van de lijst met beperkte apps.

## <a name="browser"></a>Browser

- **Webbrowser**: Met **Blokkeren** wordt de ingebouwde webbrowser op apparaten uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="cellular-and-connectivity"></a>Mobiel en connectiviteit

- **Wi-Fi**: Met **Blokkeren** wordt de Wi-Fi-functionaliteit op apparaten uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Wi-Fi-tethering**: Met **Blokkeren** wordt Wi-Fi-tethering op apparaten uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Automatisch verbinding maken met Wi-Fi-hotspots**: Hiermee staat u apparaten toe automatisch verbinding te maken met gratis Wi-Fi-hotspots en automatisch alle gebruiksvoorwaarden te accepteren.
- **Wi-Fi-hotspots melden**: Met **Blokkeren** voorkomt u dat apparaten verbindingsgegevens van Wi-Fi-hotspots versturen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **NFC**: Met **Blokkeren** schakelt u bewerkingen uit waarbij Near Field Communication (NFC) wordt gebruikt op apparaten die dit ondersteunen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Bluetooth**: Met **Blokkeren** wordt voorkomen dat gebruikers Bluetooth inschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="next-steps"></a>Volgende stappen

Zie [Apparaatbeperkingsinstellingen configureren in Microsoft Intune](device-restrictions-configure.md) voor een algemeen overzicht van het profiel voor apparaatbeperkingen.
