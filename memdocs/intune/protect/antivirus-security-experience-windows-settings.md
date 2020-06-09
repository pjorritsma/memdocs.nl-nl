---
title: Instellingen van het Antivirus-beleid voor Windows 10 voor Windows-beveiligingservaring voor Intune | Microsoft Docs
description: Instellingen voor beveiligingsbeleid voor eindpunten voor de Windows-beveiligingstoepassing in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 78cc6182cf8682935ecaa6c319e30ee8261fc2fb
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455256"
---
# <a name="settings-for-the-windows-security-experience-profile-in-microsoft-intune"></a>Instellingen voor het Windows-beveiligingservaringsprofiel in Microsoft Intune

Bekijk de Antivirus-beleidsinstellingen die u kunt configureren voor het profiel **Windows-beveiligingservaring** voor Windows 10 in Microsoft Intune als onderdeel van een [eindpuntbeveiligingsbeleid](../protect/endpoint-security-policy.md).

**Windows-beveiliging**

- **Manipulatiebeveiliging inschakelen om te voorkomen dat Microsoft Defender wordt uitgeschakeld**  
  [Wijzigingen in beveiligingsinstellingen voorkomen met Manipulatiebeveiliging](https://go.microsoft.com/fwlink/?linkid=2066083)

  - **Niet geconfigureerd** (*standaard*): wanneer de staat *Inschakelen* of *Uitschakelen* bestaat op een client, heeft het implementeren van *Niet geconfigureerd* geen invloed op de instelling. 
  - **Inschakelen**: De beperking voor Manipulatiebeveiliging inschakelen. Als u de status wilt wijzigen van ingeschakeld of uitgeschakeld, implementeert u de tegenovergestelde instelling zodat deze van kracht wordt.
  - **Uitschakelen**: De beperking voor Manipulatiebeveiliging uitschakelen. Als u de status wilt wijzigen van ingeschakeld of uitgeschakeld, implementeert u de tegenovergestelde instelling zodat deze van kracht wordt.

- **Het gebied voor beveiliging tegen virussen en bedreigingen verbergen in de Windows-beveiligings-app**  
  CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Ja**: Het gebied voor beveiliging tegen virussen en bedreigingen in de Windows-beveiligings-app wordt verborgen voor eindgebruikers. Meldingen met betrekking tot beveiliging tegen virussen- en bedreigingen worden onderdrukt.

  - **Het gebied voor ransomware-gegevensherstel verbergen in de Windows-beveiligings-app**  
    CSP: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Ja**: Het gebied voor gegevensherstel bij ransomware in de Windows-beveiligings-app wordt verborgen voor eindgebruikers. Meldingen gerelateerd aan ransomware worden onderdrukt.

- **Het gebied voor accountbeveiliging verbergen in de Windows-beveiligings-app**  
  CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Ja**: Het gebied voor accountbeveiliging in de Windows-beveiligings-app wordt verborgen voor eindgebruikers. Meldingen met betrekking tot accountbeveiliging worden onderdrukt.

- **Het gebied voor firewall- en netwerkbeveiliging verbergen in de Windows-beveiligings-app**  
  CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Ja**: Het gebied voor firewall- en netwerkbeveiliging in de Windows-beveiligings-app wordt verborgen voor eindgebruikers. Meldingen met betrekking tot firewall- en netwerkbeveiliging worden onderdrukt.

- **Het gebied voor app- en browserbeheer verbergen in de Windows-beveiligings-app**  
  CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Ja**Het gebied voor app- en browserbesturing in de Windows-beveiligings-app wordt verborgen voor eindgebruikers. Meldingen over de app-en browserbesturing zijn onderdrukt.

- **Het gebied voor apparaatbeveiliging verbergen in de Windows-beveiligings-app**  
  CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Ja**: Het gebied voor hardwarebeveiliging in de Windows-beveiligings-app wordt verborgen voor eindgebruikers. Meldingen met betrekking tot hardwarebeveiliging worden onderdrukt.
  
- **Het gebied voor apparaatprestaties en -status verbergen in de app Windows-beveiliging**  
  CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Ja**: het gebied voor apparaatprestaties en -status verbergen in de app Windows-beveiliging wordt verborgen voor eindgebruikers. Meldingen met betrekking tot apparaatprestaties en -status worden onderdrukt

- **Het gebied voor gezinsopties verbergen in de Windows-beveiligings-app**  
  CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij interface en meldingen zijn toegestaan.
  - **Ja**: het gebied voor gezinsopties in de Windows-beveiligings-app wordt verborgen voor eindgebruikers. Ook worden meldingen die betrekking hebben op de gezinsopties onderdrukt.

- **Meldingen van de Windows-beveiligings-app**  
  CSP: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)

  Gebruik deze instelling om Windows-beveiligingsmeldingen voor uw gebruikers te blokkeren voor alle voorgaande functie-instellingen. U kunt ook de Windows-beveiligings-app-meldingen per onderdeel beheren door de instellingen voor doorvoeren te gebruiken.

  - **Niet geconfigureerd** (*standaard*): alle meldingen van Windows-beveiligings-apps die niet worden beheerd door een andere instelling, zijn toegestaan.
  - **Niet-kritieke meldingen blokkeren**: meldingen zoals het voltooien van scans worden geblokkeerd.
  - **Alle meldingen blokkeren**: essentiële en niet-kritieke meldingen worden geblokkeerd voor alle Windows-beveiligingsfuncties.

- **Het Windows-beveiligingspictogram in het systeemvak verbergen**  
  CSP: [HideWindowsSecurityNotificationAreaControl](https://go.microsoft.com/fwlink/?linkid=2114313&clcid=0x409)

  De gebruiker moet zich afmelden en weer aanmelden of de computer opnieuw opstarten om deze instelling toe te passen.
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij de pictogrammen worden weergegeven.
  - **Ja**: het Windows-beveiligingspictogram in het systeemvak van de gebruiker verbergen.
  
- **Schakel de optie TPM wissen uit in de Windows-beveiligingstoepassing**  
  CSP: [DisableClearTpmButton](https://go.microsoft.com/fwlink/?linkid=2114125&clcid=0x409)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij toegang tot de knoppen wordt toegestaan.
  - **Ja**: Schakel de toegang tot de knop TPM wissen uit in de Windows-beveiligings-app.

- **Gebruikers vragen om TPM-firmware bij te werken indien een beveiligingsprobleem wordt gedetecteerd**  
  CSP: [DisableTpmFirmwareUpdateWarning](https://go.microsoft.com/fwlink/?linkid=2114212&clcid=0x409)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de standaardinstelling van de client, waarbij gebruikers geen instructies ontvangen.
  - **Ja**: hiermee staat u toe dat Windows eindgebruikers instructies geeft wanneer een mogelijk beveiligingsprobleem wordt gevonden in de TPM-firmware. Vervolgens wordt geadviseerd om firmware-updates uit te voeren om het beveiligingsprobleem op te lossen.

- **Contactgegevens voor ondersteuning van uw organisatie**  
  CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)

  Geef aan waar u de informatie van uw IT-organisatie moet worden weergegeven in de Windows-beveiligings-app en meldingen.
  - **Niet geconfigureerd** (*standaard*)
  - **In app en in meldingen weergeven**
  - **Alleen in app weergeven**
  - **Alleen in meldingen weergeven**
