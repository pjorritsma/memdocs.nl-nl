---
title: Apparaatbeperkingsinstellingen voor Windows 8.1 configureren in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Meer informatie over de Intune-instellingen die u kunt gebruiken voor het beheren van apparaatinstellingen en functionaliteit op apparaten met Windows 8.1.
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
ms.openlocfilehash: 59af48b36cb9c76ce7587457d4921356f542493f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407669"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Microsoft Intune-apparaatbeperkingsinstellingen voor Windows 8.1

In dit artikel komt u meer te weten over de Microsoft Intune-apparaatbeperkingsinstellingen die u kunt configureren voor apparaten met Windows 8.1.

## <a name="general"></a>Algemeen

- **Gebruiksgegevens delen**: **Blokkeren** voorkomt dat apparaten diagnostische gegevens en gebruikstelemetriegegevens naar Microsoft verzenden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Firewall**: **Vereisen** dat Windows Firewall is ingeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Gebruikersaccountbeheer**: Hiermee configureert u Gebruikersaccountbeheer (UAC). Kies hoe gebruikers op de hoogte worden gebracht van wijzigingen op apparaten. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Altijd melden**
  - **Melden bij app-wijzigingen**
  - **Melden bij app-wijzigingen, maar het scherm niet op zwart laten gaan**
  - **Nooit melden**

## <a name="password"></a>Wachtwoord

- **Vereist wachtwoordtype**: Kies deze optie als gebruikers een wachtwoord moeten invoeren voor toegang tot het apparaat. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Alfanumeriek**: Het wachtwoord moet een combinatie van cijfers en letters zijn.
  - **Numeriek**: Het wachtwoord mag alleen uit cijfers bestaan.
- **Minimale wachtwoordlengte**: Voer het minimum aantal vereiste tekens (tussen 6 en 16 tekens) in. Voer bijvoorbeeld `6` in om in te stellen dat een wachtwoord minimaal zes cijfers of tekens moet bevatten.
- **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal onjuiste wachtwoorden (tussen 1 en 14) in dat is toegestaan voordat het apparaat wordt gewist.
- **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld (in minuten)** : Voer de tijdsduur (tussen 1 en 60 minuten) in gedurende welke een apparaat inactief moet zijn voordat het scherm automatisch moet worden vergrendeld. Voer bijvoorbeeld `5` in om het apparaat te vergrendelen nadat dit vijf minuten lang inactief is geweest. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Wachtwoordverlooptijd (dagen)** : Voer de tijdsduur (tussen 1 en 255 dagen) in waarna het wachtwoord van een apparaat moet worden gewijzigd. Voer bijvoorbeeld `90` als u wilt dat het wachtwoord na 90 dagen verloopt. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Wachtwoorden niet opnieuw gebruiken**: Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld `5` invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Afbeeldingswachtwoord en pincode**: **Blokkeren** voorkomt dat een afbeelding of pincode wordt gebruikt als wachtwoord. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Met een afbeeldingswachtwoord kan de gebruiker zich aanmelden met aanraakbewegingen op een afbeelding. Met een pincode kunnen gebruikers zich snel met een code van 4 cijfers aanmelden.
- **Versleuteling**: **Vereisen** dat versleuteling op apparaten, inclusief voor bestanden, wordt gebruikt. Niet alle apparaten ondersteunen versleuteling. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  Als u deze instelling wilt configureren en de naleving op juiste wijze wilt rapporteren, moet u ook het volgende configureren:
  - **Vereist wachtwoordtype**: Stel dit in op ten minste **Numeriek**.
  - **Minimale wachtwoordlengte**: Stel dit in op ten minste `4`.

  Als u versleuteling wilt afdwingen op apparaten met Windows 8.1, moet u op elk apparaat de [December 2014 MDM-clientupdate voor Windows](https://support.microsoft.com/kb/3013816) installeren.

  Als u deze instelling voor Windows 8.1-apparaten inschakelt, moeten alle gebruikers van het apparaat een Microsoft-account hebben.

  Versleuteling werkt alleen indien apparaten voldoen aan de [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97)-certificeringsvereisten voor hardware.

  Wanneer u versleuteling op een apparaat afdwingt, is de herstelsleutel alleen toegankelijk vanuit het Microsoft-account van de gebruiker, waartoe de gebruiker alleen toegang heeft vanuit zijn of haar OneDrive-account. U kunt deze sleutel niet herstellen voor een gebruiker.

## <a name="browser"></a>Browser

- **Automatisch doorvoeren**: **Blokkeren** voorkomt dat gebruikers de instellingen voor automatisch aanvullen in de browser wijzigen en dat formuliervelden automatisch worden gevuld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard automatisch aanvullen toestaan.
- **Fraudewaarschuwingen**: bij **Vereisen** worden fraudewaarschuwingen in de browser weergegeven voor mogelijke frauduleuze websites. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **SmartScreen voor Microsoft Edge**: **Blokkeren** schakelt Microsoft Defender SmartScreen uit. SmartScreen zoekt naar mogelijke phishing-praktijken en schadelijke software bij het openen van sites en het downloaden van bestanden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard SmartScreen inschakelen.
- **JavaScript**: **Blokkeren** voorkomt dat scripts, zoals JavaScript, worden uitgevoerd in de browser. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Pop-ups**: **Blokkeren** schakelt de pop-upblokkering in zodat er geen pop-ups worden weergegeven in de webbrowser. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Do Not Track-headers**: **Blokkeren** voorkomt dat apparaten Do Not Track-headers verzenden naar websites die om traceringsinformatie vragen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Invoegtoepassingen**: **Blokkeren** voorkomt dat gebruikers invoegtoepassingen toevoegen in Internet Explorer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Invoer van één woord op de intranetsite**: Met een invoer van één woord kunnen gebruikers naar een intranetsite gaan door één woord in te voeren, zoals `hr` of `benefits`. Met **Blokkeren** wordt deze functie geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Intranetsite automatisch detecteren**: **Blokkeren** voorkomt dat de browser automatisch intranetsites detecteert. Intranettoewijzingsregels worden geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Internetbeveiligingsniveau**: Hiermee wordt het beveiligingsniveau voor internetsites ingesteld. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Gemiddeld**
  - **Gemiddeld (hoog)**
  - **Hoog**
- **Intranetbeveiligingsniveau**: Hiermee wordt het beveiligingsniveau voor intranetsites ingesteld. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Laag**
  - **Gemiddeld (laag)**
  - **Gemiddeld**
  - **Gemiddeld (hoog)**
  - **Hoog**
- **Beveiligingsniveau van vertrouwde websites**: Hiermee configureert u het beveiligingsniveau voor de zone met vertrouwde sites. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Laag**
  - **Gemiddeld (laag)**
  - **Gemiddeld**
  - **Gemiddeld (hoog)**
  - **Hoog**
- **Hoge beveiliging voor beperkte sites**: Hiermee configureert u het beveiligingsniveau voor de zone met websites met beperkte toegang. **Geconfigureerd** dwingt hoge beveiliging af voor beperkte sites. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Toegang tot Bedrijfsmodus via menu**: **Blokkeren** voorkomt dat gebruikers toegang krijgen tot de Bedrijfsmodus-menuopties in Internet Explorer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Wanneer dit is ingesteld op **Blokkeren**, voert u ook het volgende in:
  - **Locatie van logboekregistratierapport (URL)** : Voer een URL-locatie in waar rapporten worden opgehaald waarin de websites worden vermeld waarvoor Bedrijfsmodus-toegang is ingeschakeld.
- **Locatie van de lijst met websites met bedrijfsmodus (alleen desktops)** : Voer de locatie in van de lijst met websites die kunnen worden geopend in bedrijfsmodus.

## <a name="cellular"></a>Mobiel

- **Gegevensroaming**: **Blokkeren** voorkomt dataroaming wanneer apparaten zich in een mobiel netwerk bevinden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="cloud-and-storage"></a>Cloud en opslag

- **URL voor werkmappen**: Voer de URL van de werkmap in, zodat documenten op verschillende apparaten kunnen worden gesynchroniseerd. Wanneer deze optie is ingesteld op **Niet geconfigureerd** (standaard) of leeg wordt gelaten, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Toegang tot de Windows Mail-app zonder Microsoft-account**: **Blokkeren** voorkomt dat toegang wordt verkregen tot de Windows Mail-app zonder een Microsoft-account. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="next-steps"></a>Volgende stappen

Maak een apparaatbeperkingsprofiel in [Windows 10 en hoger](device-restrictions-windows-10.md).
