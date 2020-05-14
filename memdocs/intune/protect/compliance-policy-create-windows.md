---
title: Nalevingsinstellingen voor Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk een overzicht van alle instellingen die u kunt gebruiken bij het instellen van naleving voor uw Windows 10-, Windows Holographic- en Surface Hub-apparaten in Microsoft Intune. Controleer de naleving van de minimum- en maximumversie van het besturingssysteem, stel wachtwoordbeperkingen en -lengte in, controleer op antivirusoplossingen van partners, schakel versleuteling voor de gegevensopslag in en meer.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/09/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: dfcedebf32c8f08450e3eaa87c99f9bc11dd7431
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906901"
---
# <a name="windows-10-and-later-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Instellingen in Windows 10 en later om te markeren of apparaten wel of niet conform zijn met behulp van Intune

Dit artikel bevat een overzicht en beschrijving van de verschillende nalevingsinstellingen die u kunt configureren op apparaten met Windows 10 of later in Intune. Gebruik deze instellingen als onderdeel van uw MDM-oplossing (Mobile Device Management) om BitLocker te vereisen, een minimum- en maximumversie van het besturingssysteem in te stellen, een risiconiveau in te stellen met behulp van Microsoft Defender Advanced Threat Protection (ATP), en meer.

Deze functie is van toepassing op:

- Windows 10 en hoger
- Windows Holographic for Business
- Surface Hub

Gebruik deze nalevingsinstellingen als Intune-beheerder om de resources van uw organisatie beter te beschermen. Zie [Aan de slag met apparaatnalevingsbeleid](device-compliance-get-started.md) voor meer informatie over nalevingsbeleid en wat dit doet.

## <a name="before-you-begin"></a>Voordat u begint

[Een nalevingsbeleid maken](create-compliance-policy.md#create-the-policy). Voor **Platform** selecteert u **Windows 10 en hoger**.

## <a name="device-health"></a>Apparaatstatus

### <a name="windows-health-attestation-service-evaluation-rules"></a>Evaluatieregels voor Windows Health Attestation-service

- **BitLocker vereisen**:  
   Windows BitLocker-stationsversleuteling versleutelt alle gegevens die zijn opgeslagen op het volume met het Windows-besturingssysteem. BitLocker gebruikt de TPM (Trusted Platform Module) om het Windows-besturingssysteem en de gebruikersgegevens te beveiligen. Het helpt ook om te bevestigen dat een computer niet is gemanipuleerd, zelfs als deze zonder toezicht, kwijtgeraakt of gestolen is. Als de computer is uitgerust met een compatibele TPM, gebruikt BitLocker de TPM om de versleutelingssleutels te vergrendelen die de gegevens beschermen. Als gevolg hiervan kunnen de sleutels niet worden gebruikt tot met de TPM de status van de computer is gecontroleerd.  

   - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
   - **Vereisen** - Het apparaat kan gegevens die op de schijf zijn opgeslagen, beveiligen tegen onbevoegde toegang wanneer het systeem is uitgeschakeld of zich in de slaapstand bevindt.  


- **Vereisen dat beveiligd opstarten wordt ingeschakeld op het apparaat**:  
    - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
    - **Vereisen** - Het systeem wordt geforceerd opgestart in een vertrouwde fabrieksstatus. De belangrijkste onderdelen die worden gebruikt om de machine op te starten, moeten de juiste cryptografische handtekeningen hebben die worden vertrouwd door de organisatie die het apparaat heeft gemaakt. De UEFI-firmware verifieert de digitale handtekening voordat de computer kan worden opgestart. Als de bestanden zijn gemanipuleerd, waardoor de bijbehorende handtekening is beschadigd, kan het systeem niet worden gestart.

  > [!NOTE]
  > De instelling **Vereisen dat beveiligd opstarten wordt ingeschakeld op het apparaat** wordt ondersteund op bepaalde TPM 1.2- en 2.0-apparaten. Voor apparaten die geen ondersteuning bieden voor TPM 2.0 of later, wordt de beleidsstatus in Intune weergegeven als **Niet-conform**. Zie [Apparaatstatusverklaring](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview#device-health-attestation) voor meer informatie over ondersteunde versies.

- **Code-integriteit vereisen**:  
  Code-integriteit is een functie waarmee de integriteit van een stuurprogramma of systeembestand wordt gevalideerd telkens wanneer dit in het geheugen wordt geladen.
  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  -  **Vereisen** - Code-integriteit vereisen, dit detecteert of een niet-ondertekend stuurprogramma of systeembestand naar de kernel wordt geladen. Ook wordt gedetecteerd of een systeembestand wordt gewijzigd door schadelijke software of wordt uitgevoerd via een gebruikersaccount met beheerdersbevoegdheden.

Meer resources:

- Zie [Health Attestation CSP](https://docs.microsoft.com/windows/client-management/mdm/healthattestation-csp) voor meer informatie over de werking van de Health Attestation-service.
- [Ondersteuningstip: Apparaatstatusverklaring gebruiken als onderdeel van uw Intune-nalevingsbeleid](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Using-Device-Health-Attestation-Settings-as-Part-of/ba-p/282643).

## <a name="device-properties"></a>Apparaateigenschappen

### <a name="operating-system-version"></a>Versie van besturingssysteem

- **Minimale versie van het besturingssysteem**:  
  Voer de minimaal toegestane versie in de nummerindeling **major.minor.build.CU** in. Als u de juiste waarde wilt ophalen, opent u een opdrachtprompt en typt u `ver`. De opdracht `ver` retourneert de versie in de volgende indeling:

  `Microsoft Windows [Version 10.0.17134.1]`

  Wanneer een apparaat een eerdere versie heeft dan de ingevoerde versie van het besturingssysteem, wordt de versie als niet-compatibel gerapporteerd. Er wordt een koppeling met informatie over het uitvoeren van een upgrade weergegeven. De eindgebruiker kan kiezen om het apparaat bij te werken. Na het bijwerken zijn de bedrijfsresources toegankelijk.

- **Maximale versie van het besturingssysteem**:  
  Voer de maximaal toegestane versie in de nummerindeling **major.minor.build.versienummer** in. Als u de juiste waarde wilt ophalen, opent u een opdrachtprompt en typt u `ver`. De opdracht `ver` retourneert de versie in de volgende indeling:

  `Microsoft Windows [Version 10.0.17134.1]`

  Wanneer een apparaat een versie van het besturingssysteem gebruikt die hoger is dan de versie die is ingevoerd, wordt de toegang tot organisatieresources geblokkeerd. De eindgebruiker wordt gevraagd contact op te nemen met de IT-beheerder. Op dit apparaat kan geen toegang worden verkregen tot organisatieresources zolang de regel niet zodanig is gewijzigd dat de versie van het besturingssysteem is toegestaan.

- **Minimale besturingssysteem voor mobiel apparaten**:  
  Voer de minimaal toegestane versie in de nummerindeling major.minor.buildnummer in.

  Wanneer een apparaat een eerdere versie heeft dan de ingevoerde versie van het besturingssysteem, wordt de versie als niet-compatibel gerapporteerd. Er wordt een koppeling met informatie over het uitvoeren van een upgrade weergegeven. De eindgebruiker kan kiezen om het apparaat bij te werken. Na het bijwerken zijn de bedrijfsresources toegankelijk.

- **Maximale besturingssysteem voor mobiel apparaten**:  
  Voer de maximaal toegestane versie in de nummerindeling major.minor.buildnummer in.

  Wanneer een apparaat een versie van het besturingssysteem gebruikt die hoger is dan de versie die is ingevoerd, wordt de toegang tot organisatieresources geblokkeerd. De eindgebruiker wordt gevraagd contact op te nemen met de IT-beheerder. Op dit apparaat kan geen toegang worden verkregen tot organisatieresources zolang de regel niet zodanig is gewijzigd dat de versie van het besturingssysteem is toegestaan.

- **Geldige build van het besturingssysteem**:  
  Voer een bereik in voor de acceptabele versies van besturingssystemen, met inbegrip van een minimum en maximum. U kunt ook een bestandslijst met door komma's gescheiden waarden (CSV) met de toegestane versienummers van besturingssystemen **exporteren**.

## <a name="configuration-manager-compliance"></a>Configuration Manager-compatibiliteit

Geldt alleen voor gezamenlijk beheerde apparaten met Windows 10 en hoger. Apparaten met alleen Intune retourneren de status Niet beschikbaar.

- **Apparaatcompatibiliteit van Configuration Manager vereisen**:  
  - **Niet geconfigureerd** (*standaard*) -Intune zoekt niet naar de Configuration Manager-instellingen voor naleving.
  - **Vereisen**: vereisen dat alle instellingen (configuratie-items) in Configuration Manager compatibel zijn.  

    U kunt bijvoorbeeld vereisen dat alle software-updates worden geïnstalleerd op apparaten. Deze vereiste heeft in Configuration Manager de status Geïnstalleerd. Als programma's op het apparaat een onbekende status hebben, is het apparaat niet-compatibel in Intune.

## <a name="system-security"></a>Systeembeveiliging

### <a name="password"></a>Wachtwoord

- **Wachtwoord vereist voor het ontgrendelen van mobiele apparaten**:  
  - **Niet geconfigureerd** (*standaard*) - Deze instelling wordt niet beoordeeld op naleving of niet-naleving.
  - **Vereisen** - Gebruikers moeten een wachtwoord invoeren voordat ze toegang kunnen krijgen tot hun apparaat. 

- **Eenvoudige wachtwoorden**:  
  - **Niet geconfigureerd** (*standaard*): gebruikers kunnen eenvoudige wachtwoorden maken, zoals **1234** of **1111**.
  - **Blokkeren** - Gebruikers kunnen geen eenvoudige wachtwoorden maken, zoals **1234** of **1111**.

- **Wachtwoordtype**:  
  Kies het type wachtwoord of pincode dat is vereist. Uw opties zijn:
  - **Standaardwaarde apparaat** (*standaard*): een wachtwoord, een numerieke pincode of een alfanumerieke pincode vereisen
  - **Numeriek**: een wachtwoord of numerieke pincode vereisen
  - **Alfanumeriek**: een wachtwoord of alfanumerieke pincode vereisen.  
  
  Wanneer deze optie is ingesteld op *Alfanumeriek*, zijn de volgende instellingen beschikbaar:  
  - **Wachtwoordcomplexiteit**:  
    Uw opties zijn: 
    - **Cijfers en kleine letters vereisen** (*standaard*)
    - **Cijfers, kleine letters en hoofdletters vereisen**
    - **Cijfers, kleine letters, hoofdletters en speciale tekens vereisen**

    > [!TIP]
    > Beleidsregels van alfanumerieke wachtwoorden kunnen ingewikkeld zijn. Wij raden beheerders aan om de CSP's te lezen voor meer informatie:
    >
    > - [DeviceLock/AlphanumericDevicePasswordRequired CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)
    > - [DeviceLock/MinDevicePasswordComplexCharacters CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordcomplexcharacters)

- **Minimale wachtwoordlengte**:  
  Voer het aantal cijfers of tekens in waaruit het wachtwoord minimaal moet bestaan.

- **Maximum aantal minuten inactief voordat wachtwoord is vereist**:  
  Voer in na hoeveel niet-actieve tijd gebruikers hun wachtwoord opnieuw moeten invoeren.

- **Wachtwoordverlooptijd (dagen)** :  
  Voer het aantal dagen (tussen 1 en 730) in waarna het wachtwoord verloopt en gebruikers een nieuw wachtwoord moeten maken.

- **Aantal eerdere wachtwoorden dat niet opnieuw mag worden gebruikt**:  
  Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt.

- **Wachtwoord vereisen wanneer het apparaat wordt geactiveerd vanuit een niet-actieve status (mobiel en Holographic)** :  
  - **Niet geconfigureerd** (*standaard*)
  - **Vereisen** - Vereisen dat de gebruiker telkens het wachtwoord invoert wanneer het apparaat terugkeert uit een niet-actieve status.

  > [!IMPORTANT]
  > Als de wachtwoordvereiste op een Windows-bureaublad wordt gewijzigd, heeft dit een invloed op gebruikers de volgende keer dat ze zich aanmelden, omdat het apparaat op dat moment van niet-actief naar actief gaat. Gebruikers met wachtwoorden die aan de vereisten voldoen, worden nog steeds gevraagd hun wachtwoord te wijzigen.

### <a name="encryption"></a>Versleuteling

- **Versleuteling van gegevensopslag op een apparaat**:  
  Deze instelling geldt voor alle stations op een apparaat.
  - **Niet geconfigureerd** (*standaard*)
  - **Vereisen** - Gebruik *Vereisen* om de gegevensopslag op uw apparaten te versleutelen.

  > [!NOTE]
  > Met de instelling **Versleuteling van gegevensopslag op een apparaat** wordt algemeen gecontroleerd of er op het apparaat wordt versleuteld. Voor betere versleutelingsinstelling kunt u overwegen om **BitLocker vereisen** te gebruiken. Hierbij wordt gebruikgemaakt van de Windows-apparaatstatusverklaring om de Bitlocker-status op TPM-niveau te valideren.

### <a name="device-security"></a>Apparaatbeveiliging  

- **Firewall**:  
  - **Niet geconfigureerd** (*standaard*): Intune beheert de Microsoft Defender-firewall niet en wijzigt evenmin bestaande instellingen.
  - **Vereisen**: Microsoft Defender-firewall inschakelen en voorkomen dat gebruikers deze functie kunnen uitschakelen.  

  [Firewall-CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp)

  > [!NOTE]
  > Als het apparaat onmiddellijk wordt gesynchroniseerd nadat het opnieuw is opgestart, of als het apparaat direct wordt gesynchroniseerd na te zijn geactiveerd uit de slaapstand, rapporteert deze instelling mogelijk **fout**. Dit scenario heeft mogelijk geen invloed op de algehele compatibiliteitsstatus van de apparaat. Als u de compatibiliteitsstatus opnieuw wilt evalueren, moet u [het apparaat handmatig synchroniseren](https://docs.microsoft.com/mem/intune/user-help/sync-your-device-manually-windows).

- **Trusted Platform Module (TPM)** :  
  - **Niet geconfigureerd** (*standaard*): Intune controleert het apparaat niet op een TPM-chipversie.
  - **Vereisen**: Intune controleert of de TPM-chipversie compatibel is. Het apparaat is compatibel als de TPM-chipversie groter is dan **0** (nul). Het apparaat is niet compatibel als er zich geen TPM-versie op het apparaat bevindt.  

  [DeviceStatus CSP - DeviceStatus/TPM/SpecificationVersion node](https://docs.microsoft.com/windows/client-management/mdm/devicestatus-csp)
  
- **Antivirus**:  
  - **Niet geconfigureerd** (*standaard*) - Intune controleert niet of er antivirusoplossingen op het apparaat zijn geïnstalleerd. 
  - **Vereisen** - Controleer de naleving met behulp van antivirusoplossingen die zijn geregistreerd bij [Windows Security Center](https://blogs.windows.com/windowsexperience/2017/01/23/introducing-windows-defender-security-center/), zoals Symantec en Microsoft Defender.
  
  [DeviceStatus CSP - DeviceStatus/Antivirus/Status](https://docs.microsoft.com/windows/client-management/mdm/devicestatus-csp)

  > [!NOTE]
  > De DeviceStatus CSP voor antivirus wordt niet ondersteund voor *Windows 10 Home* en rapporteert de status *Niet van toepassing*. Het Intune-team werkt aan een oplossing. U kunt dit probleem omzeilen door [Windows Defender](#defender)-instellingen te gebruiken in het compliancebeleid voor apparaten. Windows Defender-instellingen worden ondersteund voor Windows 10 Home.  

- **Antispyware**:  
  - **Niet geconfigureerd** (*standaard*) - Intune controleert niet of er antispywareoplossingen op het apparaat zijn geïnstalleerd.
  - **Vereisen** - Controleer de naleving met behulp van antispywareoplossingen die zijn geregistreerd bij [Windows Security Center](https://blogs.windows.com/windowsexperience/2017/01/23/introducing-windows-defender-security-center/), zoals Symantec en Microsoft Defender.  
  
  [DeviceStatus CSP - DeviceStatus/Antispyware/Status](https://docs.microsoft.com/windows/client-management/mdm/devicestatus-csp)

  > [!NOTE]
  > De DeviceStatus CSP voor antispyware wordt niet ondersteund voor *Windows 10 Home* en rapporteert de status *Niet van toepassing*. Het Intune-team werkt aan een oplossing. U kunt dit probleem omzeilen door [Windows Defender](#defender)-instellingen te gebruiken in het compliancebeleid voor apparaten. Windows Defender-instellingen worden ondersteund voor Windows 10 Home. 

### <a name="defender"></a>Defender

*De volgende compliance-instellingen worden ondersteund met Windows 10 Desktop.*

- **Microsoft Defender Antimalware**:  
  - **Niet geconfigureerd** (*standaard*): Intune beheert de service niet en wijzigt evenmin bestaande instellingen.
  - **Vereisen**: Microsoft Defender Antimalware-service inschakelen en voorkomen dat gebruikers deze functie kunnen uitschakelen.

- **Minimale versie van Microsoft Defender Antimalware**:  
  Voer de minimaal toegestane versie van de Microsoft Defender Antimalware-service in. Voer bijvoorbeeld `4.11.0.0` in. Als dit veld leeg blijft, kan elke versie van de Microsoft Defender Antimalware-service worden gebruikt.  

  *Standaard is er geen versie geconfigureerd*.

- **Beveiligingsinformatie van Microsoft Defender Antimalware up-to-date**:  
  Hiermee beheert u updates van de virus- en bedreigingsbeveiliging van Windows Security op de apparaten.
  - **Niet geconfigureerd** (*standaard*): Intune dwingt geen vereisten af.
  - **Vereisen**: afdwingen dat de beveiligingsinformatie van Microsoft Defender- up-to-date is.

  [Defender/Health/SignatureOutOfDate CSP](https://docs.microsoft.com/windows/client-management/mdm/defender-csp)
  
  Zie [Updates van beveiligingsinformatie voor Microsoft Defender Antivirus en andere Microsoft-antimalware](https://www.microsoft.com/en-us/wdsi/defenderupdates) voor meer informatie.

- **Realtime-beveiliging**:  
  - **Niet geconfigureerd** (*standaard*): Intune beheert deze functie niet en wijzigt evenmin bestaande instellingen.
  - **Vereisen**: realtime-beveiliging inschakelen, waarmee op malware, spyware en andere ongewenste software wordt gescand.  

  [Defender/AllowRealtimeMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

### <a name="microsoft-defender-advanced-threat-protection-rules"></a>Microsoft Defender Advanced Threat Protection-regels

- **Vereisen dat het apparaat de risicoscore voor computers niet overschrijdt**:  
  Gebruik deze instelling om de risicobeoordeling van de beveiligingsservices bij bedreigingen te gebruiken als voorwaarde voor naleving. Kies het maximaal toegestane bedreigingsniveau:
  - **Niet geconfigureerd** (*standaard*)  
  - **Wissen** - Deze optie is het veiligst, omdat het apparaat geen bedreigingen kan hebben. Als een van de bedreigingsniveaus voor het apparaat wordt gedetecteerd, wordt het apparaat geëvalueerd als niet-conform.
  - **Laag** - Het apparaat wordt als compatibel beoordeeld als er alleen bedreigingen met een laag niveau op staan. Als een hoger niveau wordt aangetroffen, krijgt het apparaat de status niet-compatibel.
  - **Gemiddeld** - Het apparaat wordt als compatibel beoordeeld als bestaande bedreigingen op het apparaat van laag of gemiddeld niveau zijn. Als bedreigingen met hoog niveau worden aangetroffen op het apparaat, wordt het apparaat als niet-conform beoordeeld.
  - **Hoog** - Deze optie is het minst veilig, omdat alle bedreigingsniveaus zijn toegestaan. Deze optie kan handig zijn als u deze alleen gebruikt voor rapportagedoeleinden.
  
  Zie [Microsoft Defender ATP met voorwaardelijke toegang inschakelen](advanced-threat-protection.md) als u Microsoft Defender ATP (Advanced Threat Protection) wilt gebruiken tegen bedreigingen.


## <a name="windows-holographic-for-business"></a>Windows Holographic for Business

Windows Holographic for Business gebruikt het **Windows 10 en hoger**-platform. De volgende instelling wordt in Windows Holographic for Business ondersteund:

- **Systeembeveiliging** > **Versleuteling** > **Versleuteling van opslag van gegevens op apparaat**.

Zie [Verify device encryption](https://docs.microsoft.com/hololens/hololens-encryption#verify-device-encryption) (Apparaatversleuteling controleren) om apparaatversleuteling te controleren op de Microsoft HoloLens.

## <a name="surface-hub"></a>Surface Hub

Surface Hub gebruikt het **Windows 10 en hoger**-platform. Surface Hubs worden ondersteund voor naleving en voorwaardelijke toegang. Voor het inschakelen van deze functies in Surface Hubs raden we u aan [Automatische inschrijving van Windows 10 in te schakelen](../enrollment/windows-enroll.md) in Intune (hiervoor is Microsoft Azure Active Directory (Azure AD) vereist) en te streven naar Surface Hub-apparaten als apparaatgroepen. Surface Hubs moeten zijn gekoppeld aan Azure AD om naleving en voorwaardelijke toegang te laten werken.

Zie [Inschrijving voor Windows-apparaten instellen](../enrollment/windows-enroll.md) voor hulp.

## <a name="next-steps"></a>Volgende stappen

- [Voeg acties voor niet-conforme apparaten toe](actions-for-noncompliance.md) en [gebruik bereiktags om beleidsregels te filteren](../fundamentals/scope-tags.md).
- [Controleer uw nalevingsbeleid](compliance-policy-monitor.md).
- Zie de [Instellingen voor nalevingsbeleid voor Windows 8.1-apparaten](compliance-policy-create-windows-8-1.md).
