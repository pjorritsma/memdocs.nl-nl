---
title: Endpoint Protection configureren op macOS-apparaten met Microsoft Intune | Microsoft Docs
description: Gebruik Intune om macOS-apparaten te configureren om de ingebouwde firewall te gebruiken om specifieke apps toe te staan of te blokkeren of om de verborgen modus te gebruiken, om Gatekeeper te gebruiken om te bepalen waar apps worden geïnstalleerd en om FileVault-schijfversleuteling te gebruiken.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107509"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Instellingen in Intune voor Endpoint Protection in macOS

In dit artikel komt u meer te weten over de eindpuntbeschermingsinstellingen die u kunt configureren voor apparaten waarop macOS wordt uitgevoerd. U kunt deze instellingen configureren met behulp van een configuratieprofiel voor macOS-apparaten voor [Endpoint Protection](endpoint-protection-configure.md) in Intune.

## <a name="before-you-begin"></a>Voordat u begint

[Een macOS-eindpuntbeveiligingsprofiel maken](endpoint-protection-configure.md).

## <a name="firewall"></a>Firewall

Gebruik de firewall om verbindingen per toepassing te beheren, in plaats van per poort. Met de instellingen per toepassing kunt u beter profiteren van de voordelen van firewallbeveiliging. Bovendien helpt het te voorkomen dat ongewenste apps gebruikmaken van netwerkpoorten die zijn geopend voor legitieme apps.

- **Firewall inschakelen**

  Schakel de firewall op macOS in en configureer hoe binnenkomende verbindingen in uw omgeving worden verwerkt.

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**

- **Alle binnenkomende verbindingen blokkeren**

  Hiermee blokkeert u alle binnenkomende verbindingen, behalve de verbindingen die vereist zijn voor basisinternetservices, zoals DHCP, Bonjour en IPSec. Hiermee worden ook alle services voor delen (zoals delen van bestanden en delen van het scherm) geblokkeerd. Als u services voor delen gebruikt, moet u *Niet geconfigureerd* gebruiken.

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**

  Wanneer u *Alle binnenkomende verbindingen blokkeren* instelt op *Niet geconfigureerd*, kunt u configureren welke apps wel of niet binnenkomende verbindingen kunnen ontvangen.

  **Toegestane apps**: Configureer een lijst met apps die inkomende verbindingen mogen ontvangen.

  - **Apps toevoegen op bundel-id**: Voer de [bundel-id](../configuration/bundle-ids-built-in-ios-apps.md) van de app in. De website van Apple bevat een lijst met [ingebouwde Apple-apps](https://support.apple.com/HT208094).
  - **Store-app toevoegen**: Selecteer een Store-app die u eerder aan Intune hebt toegevoegd. Zie [Web-apps toevoegen aan Microsoft Intune](../apps/apps-add.md) voor meer informatie.

  **Geblokkeerde apps**: Configureer een lijst met apps waarvoor binnenkomende verbindingen zijn geblokkeerd.

  - **Apps toevoegen op bundel-id**: Voer de [bundel-id](../configuration/bundle-ids-built-in-ios-apps.md) van de app in. De website van Apple bevat een lijst met [ingebouwde Apple-apps](https://support.apple.com/HT208094).
  - **Store-app toevoegen**: Selecteer een Store-app die u eerder aan Intune hebt toegevoegd. Zie [Web-apps toevoegen aan Microsoft Intune](../apps/apps-add.md) voor meer informatie.

- **Verborgen modus inschakelen**

  Schakel deze optie in om te voorkomen dat de computer reageert op peilverzoeken. Het apparaat reageert nog wel op binnenkomende verzoeken voor toegestane apps. Onverwachte aanvragen, zoals ICMP (ping), worden genegeerd.

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**

## <a name="gatekeeper"></a>Gatekeeper

- **Toestaan dat apps worden gedownload van deze locaties**

  Beperk de apps die op een apparaat kunnen worden gestart, afhankelijk van waar de apps zijn gedownload. Het doel hiervan is om de apparaten te beschermen tegen malware en alleen apps toe te staan van bronnen die u vertrouwt.

  - **Niet geconfigureerd** (*standaard*)
  - **Mac App Store**
  - **Mac App Store en geïdentificeerde ontwikkelaars**
  - **Overal**

- **Niet toestaan dat de gebruiker Gatekeeper negeert**

  Hiermee voorkomt u dat gebruikers de Gatekeeper-instelling kunnen overschrijven en voorkomt u dat ze op Control kunnen klikken om een app te installeren. Wanneer dit is ingeschakeld, kunnen gebruikers op Control klikken om een app te installeren.

  - **Niet geconfigureerd** (*standaard*): gebruikers kunnen op Control klikken om apps te installeren.
  - **Ja**: voorkomen dat gebruikers op Control klikken om apps te installeren.

## <a name="filevault"></a>FileVault

Zie [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) in de Apple-inhoud voor ontwikkelaars voor meer informatie over de Apple FileVault-instellingen.

> [!IMPORTANT]
> Vanaf macOS 10.15 is een door de gebruiker goedgekeurde MDM-inschrijving vereist voor FileVault-configuratie.

- **FileValt inschakelen**  

  U kunt volledige schijfversleuteling *inschakelen* met behulp van XTS-AES 128 met FileVault op apparaten waarop macOS 10.13 of later wordt uitgevoerd.

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**

  Als *FileVault inschakelen* is ingesteld op *Ja*, kunt u de volgende instellingen configureren:

  - **Herstelsleuteltype**

    Herstelsleutels van het type *Persoonlijke sleutel* zijn gemaakt voor apparaten. Configureer de volgende instellingen voor de persoonlijke sleutel.

  - **Escrow-locatiebeschrijving van persoonlijke herstelsleutel**

    Geef een kort bericht op voor gebruikers waarin wordt uitgelegd hoe en waar ze de persoonlijke herstelsleutel kunnen ophalen. Deze tekst wordt ingevoegd in het bericht dat de gebruiker op het aanmeldingsscherm ziet wanneer wordt gevraagd de persoonlijke herstelsleutel in te voeren als een wachtwoord is vergeten.

  - **Roulering van persoonlijk herstelsleutel**

    Geef op hoe vaak de persoonlijke herstelsleutel voor een apparaat wordt gerouleerd. U kunt de standaardinstelling, **Niet geconfigureerd** of een waarde van **1** tot **12** maanden selecteren.

  - **Herstelsleutel verbergen**

    Kies deze instelling om de persoonlijke sleutel te verbergen voor de eindgebruiker tijdens de FileVault 2-versleuteling.

    - **Niet geconfigureerd** (*standaard*): de persoonlijke sleutel is tijdens de versleuteling zichtbaar voor de apparaatgebruiker.
    - **Ja**: de persoonlijke sleutel is tijdens de versleuteling verborgen voor de apparaatgebruiker.

    Na versleuteling kunnen apparaatgebruikers hun persoonlijke herstelsleutel voor een versleuteld macOS-apparaat bekijken op de volgende locaties:
    - Bedrijfsportal-app voor iOS/iPadOS
    - Intune-app
    - bedrijfsportalwebsite
    - Android-bedrijfsportal-app

    Als u de sleutel wilt weergeven, gaat u, vanaf de app of website, naar de apparaatgegevens van het versleutelde macOS-apparaat en selecteert u *Herstelsleutel ophalen*.

  - **Vraag bij afmelden uitschakelen**

    Voorkom dat de gebruiker bij het afmelden wordt gevraagd om FileVault in te schakelen.  Wanneer Uitschakelen is ingesteld, wordt de vraag niet gesteld als de gebruiker zich afmeldt, maar als deze zich aanmeldt.

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: de vraag bij afmelden uitschakelen.

  - **Toegestaan aantal keren voor overslaan**

    Stel in hoe vaak de gebruiker de vraag om FileVault in te schakelen kan negeren voordat FileVault vereist is voor aanmelding van de gebruiker.

    - **Niet geconfigureerd**: versleuteling op het apparaat is vereist voordat de volgende aanmelding is toegestaan.
    - **0**: vereisen dat apparaten worden versleuteld de volgende keer dat een gebruiker zich aanmeldt bij het apparaat.
    - **1** tot **10**: sta een gebruiker toe de vraag tussen 1 en 10 keer te negeren voordat versleuteling op het apparaat wordt vereist.
    - **Geen limiet, altijd vragen**: de gebruiker wordt gevraagd om FileVault in te schakelen, maar versleuteling is nooit vereist.

    De standaardwaarde voor deze instelling is afhankelijk van de configuratie van *Prompt uitschakelen bij afmelden*. Wanneer *Vraag bij afmelden uitschakelen* is ingesteld op **Niet geconfigureerd**, is deze instelling standaard **Niet geconfigureerd**. Als *Vraag bij afmelden uitschakelen* is ingesteld op **Ja**, is de standaardwaarde van deze instelling **1** en is de waarde **Niet geconfigureerd** geen optie.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](../configuration/device-profile-assign.md) en [de status ervan controleren](../configuration/device-profile-monitor.md).

U kunt ook eindpuntbeveiliging configureren op [apparaten met Windows 10 of nieuwer](endpoint-protection-windows-10.md).
