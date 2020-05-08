---
title: Endpoint Protection in macOS toevoegen in Microsoft Intune - Azure | Microsoft Docs
description: Gebruik Gatekeeper op macOS-apparaten om te bepalen waar apps kunnen worden geïnstalleerd, inclusief de Mac App Store. Schakel met Microsoft Intune ook een firewall in of configureer een firewall die bepaalde apps toestaat, bepaalde apps blokkeert, de verborgen modus gebruikt en zelfs bepaalde typen binnenkomende verbindingen blokkeert.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/29/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 337f7608b4c75a5a2ce2c85774d2090d549ae1fe
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587263"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Instellingen in Intune voor Endpoint Protection in macOS  

In dit artikel komt u meer te weten over de eindpuntbeschermingsinstellingen die u kunt configureren voor apparaten waarop macOS wordt uitgevoerd. U kunt deze instellingen configureren met behulp van een configuratieprofiel voor macOS-apparaten voor [Endpoint Protection](endpoint-protection-configure.md) in Intune.  

## <a name="before-you-begin"></a>Voordat u begint

[Een macOS-eindpuntbeveiligingsprofiel maken](endpoint-protection-configure.md).

## <a name="gatekeeper"></a>Gatekeeper  

- **Toestaan dat apps worden gedownload van deze locaties**  
  Beperk de apps die op een apparaat kunnen worden gestart, afhankelijk van waar de apps zijn gedownload. Het doel hiervan is om de apparaten te beschermen tegen malware en alleen apps toe te staan van bronnen die u vertrouwt.  

  - **Niet geconfigureerd**  
  - **Mac App Store**  
  - **Mac App Store en geïdentificeerde ontwikkelaars**  
  - **Overal**  

  **Standaardinstelling**: Niet geconfigureerd  

- **Gebruiker kan Gatekeeper overschrijven**  
  Hiermee voorkomt u dat gebruikers de Gatekeeper-instelling kunnen overschrijven en voorkomt u dat ze op Control kunnen klikken om een app te installeren. Wanneer dit is ingeschakeld, kunnen gebruikers op Control klikken om een app te installeren.  
 
  - **Niet geconfigureerd**: gebruikers kunnen op Control klikken om apps te installeren.  
  - **Blokkeren**: voorkomen dat gebruikers op Control klikken om apps te installeren.  

  **Standaardinstelling**: Niet geconfigureerd  

## <a name="firewall"></a>Firewall  

Gebruik de firewall om verbindingen per toepassing te beheren, in plaats van per poort. Met de instellingen per toepassing kunt u beter profiteren van de voordelen van firewallbeveiliging. Bovendien helpt het te voorkomen dat ongewenste apps gebruikmaken van netwerkpoorten die zijn geopend voor legitieme apps.  

**Algemeen**
- **Firewall**  
  Schakel de firewall in om te configureren hoe binnenkomende verbindingen in uw omgeving worden verwerkt.  
  - **Niet geconfigureerd**  
  - **Inschakelen**  

  **Standaardinstelling**: Niet geconfigureerd  

- **Binnenkomende verbindingen**  
  Hiermee blokkeert u alle binnenkomende verbindingen, behalve de verbindingen die vereist zijn voor basisinternetservices, zoals DHCP, Bonjour en IPSec. Hiermee worden ook alle services voor delen (zoals delen van bestanden en delen van het scherm) geblokkeerd. Als u services voor delen gebruikt, moet u *Niet geconfigureerd* gebruiken.  
  - **Niet geconfigureerd**  
  - **Blokkeren**  

  **Standaardinstelling**: Niet geconfigureerd  

**Binnenkomende verbindingen voor specifieke apps blokkeren of toestaan.**  

  - **Toegestane apps**  
    Selecteer de apps die expliciet zijn toegestaan voor het ontvangen van binnenkomende verbindingen.  

  - **Geblokkeerde apps**  
    Selecteer de apps die binnenkomende verbindingen moeten blokkeren.  

  - **Verborgen modus**  
    Schakel deze optie in om te voorkomen dat de computer reageert op peilverzoeken. Het apparaat reageert nog wel op binnenkomende verzoeken voor toegestane apps. Onverwachte aanvragen, zoals ICMP (ping), worden genegeerd.  
    - **Niet geconfigureerd**  
    - **Inschakelen**  

    **Standaardinstelling**: Niet geconfigureerd  

## <a name="filevault"></a>FileVault  
Zie [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) in de Apple-inhoud voor ontwikkelaars voor meer informatie over de Apple FileVault-instellingen. 

> [!IMPORTANT]  
> Vanaf macOS 10.15 is een door de gebruiker goedgekeurde MDM-inschrijving vereist voor FileVault-configuratie. 

- **FileVault**  
  U kunt volledige schijfversleuteling *inschakelen* met behulp van XTS-AES 128 met FileVault op apparaten waarop macOS 10.13 of later wordt uitgevoerd.  
  - **Niet geconfigureerd**  
  - **Inschakelen**  

  **Standaardinstelling**: Niet geconfigureerd  

  - **Herstelsleuteltype**  
    Herstelsleutels van het type *Persoonlijke sleutel* zijn gemaakt voor apparaten. Configureer de volgende instellingen voor de persoonlijke sleutel.  

    - **Locatie van persoonlijke herstelsleutel**: geef een kort bericht op voor de gebruiker waarin wordt uitgelegd hoe en waar deze de persoonlijke herstelsleutel kan ophalen. Deze tekst wordt ingevoegd in het bericht dat de gebruiker op het aanmeldingsscherm ziet wanneer hij of zij wordt gevraagd de persoonlijke herstelsleutel in te voeren als een wachtwoord is vergeten.  

    - **Roulering van persoonlijk herstelsleutel**: geef op hoe vaak de persoonlijke herstelsleutel voor een apparaat wordt gerouleerd. U kunt de standaardinstelling, **Niet geconfigureerd** of een waarde van **1** tot **12** maanden selecteren.  

  - **Vraag bij afmelden uitschakelen**  
    Voorkom dat de gebruiker bij het afmelden wordt gevraagd om FileVault in te schakelen.  Wanneer Uitschakelen is ingesteld, wordt de vraag niet gesteld als de gebruiker zich afmeldt, maar als deze zich aanmeldt.  
    - **Niet geconfigureerd**  
    - **Uitschakelen**: de vraag bij afmelden uitschakelen.

    **Standaardinstelling**: Niet geconfigureerd  

  - **Toegestaan aantal keren voor overslaan**  
  Stel in hoe vaak de gebruiker de vraag om FileVault in te schakelen kan negeren voordat FileVault vereist is voor aanmelding van de gebruiker. 

    > [!IMPORTANT]
    >
    > Er is een bekend probleem met de waarde **Geen limiet, altijd vragen**. In plaats van een gebruiker versleuteling te laten omzeilen wanneer hij zich aanmeldt, is voor deze instelling apparaatversleuteling vereist bij de volgende aanmelding. Dit probleem wordt naar verwachting eind juni opgelost en wordt vermeld in MC210922.
    >
    > Wanneer dit probleem is opgelost, heeft deze instelling de nieuwe optie nul (**0**), waarmee wordt vereist dat apparaten worden versleuteld bij de volgende keer dat een gebruiker zich bij het apparaat aanmeldt. Wanneer deze oplossing wordt opgenomen in Intune-updates, wordt bovendien elk beleid dat is ingesteld op **Geen limiet, altijd vragen** bijgewerkt om de nieuwe waarde van **0** te gebruiken, waarmee het huidige gedrag van het vereisen van versleuteling wordt gehandhaafd.
    >
    > Nadat dit probleem is opgelost, kunt u de mogelijkheid om versleuteling te vereisen overslaan door deze instelling opnieuw te configureren om **Geen limiet, altijd vragen** in te stellen. De instelling werkt namelijk zoals oorspronkelijk werd verwacht en staat toe dat gebruikers het versleutelen van het apparaat overslaan.
    >
    > Als u macOS-apparaten hebt ingeschreven, kunt u meer informatie bekijken wanneer u zich aanmeldt bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431). Ga dan naar **Tenantbeheer** > **Tenantstatus**, selecteer **Servicestatus en berichtencentrum** en zoek de bericht-id **MC210922**.

    <br> 

    - **Niet geconfigureerd**: versleuteling op het apparaat is vereist voordat de volgende aanmelding is toegestaan.  
    - **1** tot **10**: sta een gebruiker toe de vraag tussen 1 en 10 keer te negeren voordat versleuteling op het apparaat wordt vereist.  
    - **Geen limiet, altijd vragen**: de gebruiker wordt gevraagd om FileVault in te schakelen, maar versleuteling is nooit vereist.  
 
    **Standaardinstelling**: *Varieert*: wanneer de instelling *Vraag bij afmelden uitschakelen* is ingesteld op **Niet geconfigureerd**, is de standaardwaarde van deze instelling **Niet geconfigureerd**. Als *Vraag bij afmelden* is ingesteld op **Uitschakelen**, is de standaardwaarde van deze instelling **1** en is de waarde **Niet geconfigureerd** geen optie.

Zie [FileVault-herstelsleutels](encryption-monitor.md#filevault-recovery-keys) voor meer informatie over FileVault met Intune.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](../configuration/device-profile-assign.md) en [de status ervan controleren](../configuration/device-profile-monitor.md).

U kunt ook eindpuntbeveiliging configureren op [apparaten met Windows 10 of nieuwer](endpoint-protection-windows-10.md).
