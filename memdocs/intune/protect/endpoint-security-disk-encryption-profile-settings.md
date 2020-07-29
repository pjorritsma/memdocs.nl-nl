---
title: Intune-eindpuntbeveiligingsinstellingen voor schijfversleuteling | Microsoft Docs
description: Beleidsinstellingen van eindpuntbeveiliging voor schijfversleuteling voor BitLocker en FileVault in Microsoft Intune
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
ms.openlocfilehash: 3760aa9820495db6c2460bf2e6d2e9a08d705a10
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462028"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Instellingen voor schijfversleutelingsbeleid voor eindpuntbeveiliging in Intune

Bekijk de instellingen die u kunt configureren in profielen voor beleid voor *Schijfversleuteling* in het knooppunt voor eindpuntbeveiliging van Intune als onderdeel van een [eindpuntbeveiligingsbeleid](../protect/endpoint-security-policy.md).

Ondersteunde platforms en profielen:

- **macOS**:
  - Profiel: **FileVault**
- **Windows 10 en hoger**:
  - Profiel: **BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>Versleuteling

**FileValt inschakelen**  
- **Niet geconfigureerd** (*standaard*)
- **Ja** - U kunt volledige schijfversleuteling inschakelen met behulp van XTS-AES 128 met FileVault op apparaten waarop macOS 10.13 of later wordt uitgevoerd. FileVault wordt ingeschakeld wanneer de gebruiker zich afmeldt bij het apparaat.

  Wanneer u deze instelling instelt op *Ja*, kunt u aanvullende instellingen voor FileVault configureren.

  - **Herstelsleutels van het type **
    *Persoonlijke sleutel* zijn gemaakt voor apparaten. Configureer de volgende instellingen voor de persoonlijke sleutel:

    - **Roulering van persoonlijk herstelsleutel**  
      Geef op hoe vaak de persoonlijke herstelsleutel voor een apparaat wordt gerouleerd. U kunt de standaardinstelling, **Niet geconfigureerd** of een waarde van **1** tot **12** maanden selecteren.
    - **Escrow-locatiebeschrijving van persoonlijke herstelsleutel**  
      Geef een kort bericht op voor de gebruiker waarin wordt uitgelegd hoe ze de persoonlijke herstelsleutel kunnen ophalen. De gebruiker ziet dit bericht op het aanmeldingsscherm ziet wanneer hij of zij wordt gevraagd de persoonlijke herstelsleutel in te voeren als een wachtwoord is vergeten.

  - **Toegestaan aantal keren voor overslaan**  
    Stel in hoe vaak de gebruiker de vraag om FileVault in te schakelen kan negeren voordat FileVault vereist is voor aanmelding van de gebruiker.
    - **Niet geconfigureerd** (*standaard*): versleuteling op het apparaat is vereist voordat de volgende aanmelding is toegestaan.
    - **1** tot **10**: sta een gebruiker toe de vraag tussen 1 en 10 keer te negeren voordat versleuteling op het apparaat wordt vereist.
    - **Geen limiet, altijd vragen**: de gebruiker wordt gevraagd om FileVault in te schakelen, maar versleuteling is nooit vereist.

  - **Uitstel toestaan tot afmelden**  
    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: Stel de prompt om FileVault in te schakelen uit totdat de gebruiker zich afmeldt.  

  - **Vraag bij afmelden uitschakelen**  
    Voorkom dat de gebruiker bij het afmelden wordt gevraagd om FileVault in te schakelen. Wanneer Uitschakelen is ingesteld, wordt de vraag niet gesteld als de gebruiker zich afmeldt, maar als deze zich aanmeldt.
    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: schakel de prompt om FileVault in te schakelen uit die wordt weergegeven bij afmelden.

  - **Herstelsleutel verbergen**  
     Verberg de persoonlijke herstelsleutel tijdens de versleuteling in Intune voor de gebruiker van het macOS-apparaat. Nadat de schijf is versleuteld, kan een gebruiker elk apparaat gebruiken om de persoonlijke herstelsleutel weer te geven via de Intune-bedrijfsportalwebsite of de Bedrijfsportal-app op een ondersteund platform.
    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: Verberg de persoonlijke herstelsleutel tijdens het versleutelen van het apparaat.

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker - Basisinstellingen

- **Volledige schijfversleuteling voor systeemstations en vaste gegevensstations inschakelen**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Als het station is versleuteld voordat dit beleid werd toegepast, wordt er geen extra actie ondernomen. Als de versleutelingsmethode en opties overeenkomen met die van dit beleid, wordt aangegeven dat de configuratie is geslaagd. Als een actieve BitLocker-configuratie niet overeenkomt met dit beleid, wordt waarschijnlijk een fout geretourneerd.
  
  Om dit beleid toe te passen op een schijf die al is versleuteld, ontsleutelt u het station en past u het MDM-beleid opnieuw toe. Voor Windows is standaard geen BitLocker-stationsversleuteling vereist. Echter, bij Azure AD-deelname en Microsoft-accountregistratie/-aanmelding kan met de automatische versleuteling ook BitLocker ingeschakeld worden (XTS-AES 128-bits versleuteling).

  - **Niet geconfigureerd** (*standaard*): het gebruik van BitLocker wordt niet afgedwongen.
  - **Ja**: het gebruik van BitLocker wordt afgedwongen.

- **Vereisen dat opslagkaarten worden versleuteld (alleen mobiel)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Deze instelling geldt alleen voor Windows Mobile- en Mobile Enterprise SKU-apparaten.
  - **Niet geconfigureerd** (*standaard*) - De instelling wordt teruggezet naar de standaardwaarde van het besturingssysteem; hierbij is geen versleuteling van de opslagkaart vereist.
  - **Ja**: versleuteling op opslagkaarten is vereist voor mobiele apparaten.

- **Vraag over versleuteling door derden verbergen**  
  CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  Als BitLocker is ingeschakeld op een systeem dat al is versleuteld met een versleutelingsproduct van derden, kan het apparaat onbruikbaar worden. Gegevensverlies kan optreden en u moet Windows mogelijk opnieuw installeren. Het is zeer aanbevolen om BitLocker nooit in te schakelen op een apparaat waarop versleuteling van derden is geïnstalleerd of ingeschakeld.

  Standaard worden gebruikers door de installatiewizard van BitLocker gevraagd om te bevestigen dat er geen versleuteling van derden is geïnstalleerd.

  - **Niet geconfigureerd** (*standaard*): de BitLocker-installatiewizard geeft een waarschuwing weer en vraagt gebruikers om te bevestigen dat er geen versleuteling van derden aanwezig is.
  - **Ja**: de prompt van de BitLocker-installatiewizards verbergen voor gebruikers.

  Als stille activeringsfuncties van BitLocker vereist zijn, moet de waarschuwing voor de versleuteling van derden worden verborgen omdat de vereiste prompt werkstromen voor stille activering verbreekt.

  Als de optie is ingesteld op *Ja*, kunt u vervolgens de volgende instelling configureren:

  - **Standaardgebruikers toestaan versleuteling in te schakelen tijdens Autopilot**  
    CSP: [AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **Niet geconfigureerd** (*standaard*): tijdens stille activeringsscenario’s van Azure Active Directory-gekoppeld (AADJ) hoeven gebruikers geen lokale beheerders te zijn om BitLocker in te schakelen.
    - **Ja**: de instelling wordt als standaardwaarde van de client gelaten, waardoor toegang van lokale beheerders nodig is om BitLocker in te schakelen.

    Voor niet-stille activering en Autopilot-scenario's moet de gebruiker een lokale beheerder zijn om de installatiewizard van BitLocker te voltooien.

- **Clientgestuurde herstelwachtwoorden inschakelen voor**  
  CSP: [ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  Een werkaccount toevoegen (AWA, voormalig werkplek toegevoegd) wordt niet ondersteund voor het roteren van sleutels.
  - **Niet geconfigureerd** (*standaard*): de client roteert geen BitLocker-herstelsleutels.
  - **Uitgeschakeld**
  - **Azure AD-toegevoegde apparaten**
  - **Hybride en apparaten die zijn toegevoegd aan Azure AD**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker - Instellingen voor vast station

- **BitLocker-beleid voor vaste stations**  
  [Instellingen voor BitLocker-groepsbeleid](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Vast-stationherstel**  
    CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    Beheer hoe met BitLocker beveiligde vaste gegevensstations worden hersteld als de vereiste opstartsleutelgegevens ontbreken.

    - **Niet geconfigureerd** (*standaard*): De standaardherstelopties ondersteund voor BitLocker-herstel, waaronder de agent voor gegevensherstel. De eindgebruiker kan herstelopties opgeven en er wordt geen back-up gemaakt van de herstelgegevens naar Azure Active Directory.
    - **Configureren**: Hiermee schakelt u toegang in om verschillende hersteltechnieken voor schijven te configureren.

    Indien ingesteld op *Configureren* zijn de volgende instellingen beschikbaar:

    - **Herstelsleutel maken door gebruiker**  
      - **Geblokkeerd** (*standaard*)
      - **Vereist**
      - **Toegestaan**

    - **BitLocker-herstelpakket configureren**
      - **Wachtwoord en sleutel** (*standaard*): Bevatten zowel het BitLocker-herstelwachtwoord dat door beheerders en gebruikers wordt gebruikt om beveiligde stations te ontgrendelen, en de herstelsleutelpakketten die door beheerders worden gebruikt voor gegevenshersteldoeleinden) in Active Directory.
      - **Enkel wachtwoord**: de herstelsleutelpakketten zijn mogelijk niet toegankelijk als dat nodig is.

    - **Vereisen dat het apparaat een back-up van herstelgegevens maakt in Azure AD**
      - **Niet geconfigureerd** (*standaard*): BitLocker-activering wordt voltooid, zelfs als de back-up van de herstelsleutel naar Azure AD mislukt. Dit kan ertoe leiden dat er geen herstelgegevens extern worden opgeslagen.
      - **Ja**: de activering van BitLocker wordt pas voltooid nadat de herstelsleutels succesvol zijn opgeslagen op Azure Active Directory.

    - **Herstelwachtwoord maken door gebruiker**  
      - **Geblokkeerd** (*standaard*)
      - **Vereist**
      - **Toegestaan**

    - **Herstelopties verbergen tijdens de BitLocker-installatie**
      - **Niet geconfigureerd** (*standaard*): hiermee staat u de gebruiker toe om toegang te krijgen tot extra herstelopties.
      - **Ja**: de eindgebruiker niet in staat stellen om extra herstelopties te kiezen, zoals het afdrukken van herstelsleutels tijdens de installatiewizard van BitLocker.

    - **BitLocker inschakelen na herstelgegevens om op te slaan**
      - **Niet geconfigureerd** (*standaard*)  
      - **Ja**

    - **Het gebruik van de gegevensherstelagent (DRA) op basis van certificaten blokkeren**
      - **Niet geconfigureerd** (*standaard*): Hiermee staat u het gebruik van de DRA toe die moet worden ingesteld. Voor het instellen van DRA zijn een bedrijfs-PKI en groepsbeleidsobjecten vereist voor het implementeren van de DRA-agent en certificaten.
      - **Ja**: de mogelijkheid om gegevensherstelagent (DRA) te gebruiken voor het herstellen van BitLocker-stations blokkeren.

  - **Schrijftoegang blokkeren voor vaste gegevensstations die niet zijn beveiligd door BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Deze instelling is beschikbaar als het *beleid voor vaste BitLocker-stations* is ingesteld op *Configureren*.

    - **Niet-geconfigureerd** (*standaard*): gegevens kunnen naar niet-versleutelde vaste stations worden geschreven.
    - **Ja**: Windows staat niet toe dat er gegevens naar vaste stations worden geschreven die niet met BitLocker zijn beveiligd. Als een vast station niet is versleuteld, moet de gebruiker de BitLocker-installatiewizard voor het station doorlopen voordat schrijftoegang wordt verleend.

  - **Versleutelingsmethode voor vaste gegevensstations configureren**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    Configureer de versleutelingsmethode en coderingssterkte voor vaste gegevensstations. *XTS-AES, 128-bits* is de standaardversleutelingsmethode van Windows en de aanbevolen waarde.

    - **Niet geconfigureerd** (*standaard*)
    - **AES 128-bits CBC**
    - **AES 256-bits CBC**
    - **AES 128-bits XTS**
    - **AES 256-bits XTS**

### <a name="bitlocker---os-drive-settings"></a>BitLocker - instellingen voor station met besturingssysteem

- **BitLocker-beleid voor systeemstations**  
  CSP: [Instellingen voor BitLocker-groepsbeleid](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configureren** (*standaard*)  
  - **Niet geconfigureerd**

  Als de optie is ingesteld op *Configureren*, kunt u de volgende instellingen configureren:

  - **Opstartverificatie is vereist**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: configureer aanvullende verificatievereisten voor bij het opstarten van de computer, inclusief het gebruik van Trusted Platform Module (TPM), of kunt u pincodevereisten configureren voor bij het opstarten.

    Als de optie is ingesteld op *Ja*, kunt u de volgende instellingen configureren:

    - **Compatibele TPM opstarten**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Het is raadzaam om een TPM voor BitLocker te vereisen. Deze instelling is alleen van toepassing wanneer u BitLocker inschakelt en heeft geen effect als BitLocker al is ingeschakeld.

      - **Geblokkeerd** (*standaard*): BitLocker gebruikt de TPM niet.
      - **Vereist**: BitLocker schakelt alleen in als er een TPM aanwezig en bruikbaar is.
      - **Toegestaan**: BitLocker gebruikt de TPM als deze aanwezig is.

    - **Compatibele TPM-opstartpincode**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Geblokkeerd** (*standaard*): het gebruik van een pincode blokkeren.
      - **Vereist**: vereisen dat een pincode en TPM aanwezig zijn om BitLocker in te schakelen.
      - **Toegestaan**: BitLocker gebruikt de TPM als deze aanwezig is en er kan een opstartpincode worden geconfigureerd door de gebruiker.

      Voor de stille activeringsscenario's moet u dit instellen op *Geblokkeerd*. Het stil activeren van scenario's (met inbegrip van Autopilot) mislukt wanneer gebruikersinteractie vereist is.

    - **Compatibele TPM-opstartsleutel**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Geblokkeerd** (*standaard*): het gebruik van opstartsleutels blokkeren.
      - **Vereist**: vereisen dat een opstartsleutel en TPM aanwezig zijn om BitLocker in te schakelen.
      - **Toegestaan**-BitLocker gebruikt de TPM als deze aanwezig is, en er kan opstartsleutel (zoals een USB-station) aanwezig zijn om de stations te ontgrendelen.

      Voor de stille activeringsscenario's moet u dit instellen op *Geblokkeerd*. Het stil activeren van scenario's (met inbegrip van Autopilot) mislukt wanneer gebruikersinteractie vereist is.

    - **Compatibele opstartsleutel en pincode voor TPM**  
      CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **Geblokkeerd** (*standaard*): het gebruik van een combinatie van opstartsleutel en pincode blokkeren.
      - **Vereist**: vereist dat BitLocker een opstartsleutel en een pincode bevatten om ingeschakeld te worden.
      - **Toegestaan**: BitLocker gebruikt de TPM als deze aanwezig is en er kan een combinatie van een opstartsleutel en pincode worden gebruikt.

      Voor de stille activeringsscenario's moet u dit instellen op *Geblokkeerd*. Het stil activeren van scenario's (met inbegrip van Autopilot) mislukt wanneer gebruikersinteractie vereist is.

    - **BitLocker uitschakelen op apparaten met incompatibele TPM**  
    CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      Als er geen TPM aanwezig is, vereist BitLocker een wachtwoord of een USB-station voor opstarten.

      Deze instelling is alleen van toepassing wanneer u BitLocker inschakelt en heeft geen effect als BitLocker al is ingeschakeld.

      - **Niet geconfigureerd** (*standaard*)
      - **Ja**: BitLocker blokkeren zodat deze niet wordt geconfigureerd zonder een compatibele TPM-chip.

    - **Pre-bootherstelbericht en URL inschakelen**  
      CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)configureren

      - **Niet geconfigureerd** (*standaard*): gebruik de standaardherstelgegevens voor BitLocker vóór het opstarten.
      - **Ja**: schakel de configuratie in van een aangepast pre-boot herstelbericht en een URL om uw gebruikers te helpen begrijpen hoe ze hun herstelwachtwoord kunnen vinden. Het pre-bootbericht en de URL worden weergegeven door gebruikers wanneer hun pc is vergrendeld in de herstelmodus.

      Als de optie is ingesteld op *Ja*, kunt u de volgende instellingen configureren:

      - **Preboot-herstelbericht**  
        Geef een aangepast pre-boot herstelbericht op.

      - **Preboot-herstel-URL**  
        Geef een aangepaste herstel-URL vóór het opstarten op.

    - **Systeemstationherstel**  
      CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **Niet geconfigureerd** (*standaard*)  
      - **Configureren**: hiermee schakelt u de configuratie van extra instellingen in.

      Indien ingesteld op *Configureren* zijn de volgende instellingen beschikbaar:

      - **Herstelsleutel maken door gebruiker**  
        - **Geblokkeerd** (*standaard*)
        - **Vereist**
        - **Toegestaan**

      - **BitLocker-herstelpakket configureren**
        - **Wachtwoord en sleutel** (*standaard*): Bevatten zowel het BitLocker-herstelwachtwoord dat door beheerders en gebruikers wordt gebruikt om beveiligde stations te ontgrendelen, en de herstelsleutelpakketten die door beheerders worden gebruikt voor gegevenshersteldoeleinden) in Active Directory.
        - **Enkel wachtwoord**: de herstelsleutelpakketten zijn mogelijk niet toegankelijk als dat nodig is.

      - **Vereisen dat het apparaat een back-up van herstelgegevens maakt in Azure AD**
        - **Niet geconfigureerd** (*standaard*): BitLocker-activering wordt voltooid, zelfs als de back-up van de herstelsleutel naar Azure AD mislukt. Dit kan ertoe leiden dat er geen herstelgegevens extern worden opgeslagen.
        - **Ja**: de activering van BitLocker wordt pas voltooid nadat de herstelsleutels succesvol zijn opgeslagen op Azure Active Directory.

      - **Herstelwachtwoord maken door gebruiker**  
        - **Geblokkeerd** (*standaard*)
        - **Vereist**
        - **Toegestaan**

      - **Herstelopties verbergen tijdens de BitLocker-installatie**
        - **Niet geconfigureerd** (*standaard*): hiermee staat u de gebruiker toe om toegang te krijgen tot extra herstelopties.
        - **Ja**: de eindgebruiker niet in staat stellen om extra herstelopties te kiezen, zoals het afdrukken van herstelsleutels tijdens de installatiewizard van BitLocker.

      - **BitLocker inschakelen na herstelgegevens om op te slaan**
        - **Niet geconfigureerd** (*standaard*)  
        - **Ja**

      - **Het gebruik van de gegevensherstelagent (DRA) op basis van certificaten blokkeren**
        - **Niet geconfigureerd** (*standaard*): Hiermee staat u het gebruik van de DRA toe die moet worden ingesteld. Voor het instellen van DRA zijn een bedrijfs-PKI en groepsbeleidsobjecten vereist voor het implementeren van de DRA-agent en certificaten.
        - **Ja**: de mogelijkheid om gegevensherstelagent (DRA) te gebruiken voor het herstellen van BitLocker-stations blokkeren.

    - **Minimale lengte pincode**  
      CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      Geef de minimale opstartpincode op wanneer TPM en pincode is vereist tijdens de activering van BitLocker. De minimale lengte van de pincode moet tussen de 4 en 20 tekens zijn.

      Als u deze instelling niet configureert, kunnen gebruikers een opstartpincode met een lengte (tussen 4 en 20 cijfers) configureren

      Deze instelling is alleen van toepassing wanneer u BitLocker inschakelt en heeft geen effect als BitLocker al is ingeschakeld.

  - **Versleutelingsmethode voor systeemstations configureren**  
   CSP: [EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    Configureer de versleutelingsmethode en coderingssterkte voor OS-stations. *XTS-AES, 128-bits* is de standaardversleutelingsmethode van Windows en de aanbevolen waarde.

    - **Niet geconfigureerd** (*standaard*)
    - **AES 128-bits CBC**
    - **AES 256-bits CBC**
    - **AES 128-bits XTS**
    - **AES 256-bits XTS**

### <a name="bitlocker---removable-drive-settings"></a>BitLocker - Instellingen voor verwisselbare stations

- **Versleutelingsmethode voor systeemstations configureren**  
  CSP: [Instellingen voor BitLocker-groepsbeleid](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Niet geconfigureerd** (*standaard*)  
  - **Configureerer**

  Als de optie is ingesteld op *Configureren*, kunt u de volgende instellingen configureren.

  - **Versleutelingsmethode voor verwijderbare gegevensstations configureren**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    Kies de gewenste versleutelingsmethode voor verwisselbare gegevensstationschijven.

    - **Niet geconfigureerd** (*standaard*)
    - **AES 128-bits CBC**
    - **AES 256-bits CBC**
    - **AES 128-bits XTS**
    - **AES 256-bits XTS**

  - **Schrijftoegang blokkeren voor verwisselbare gegevensstations die niet zijn beveiligd door BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **Niet-geconfigureerd** (*standaard*): gegevens kunnen naar niet-versleutelde verwijderbare stations worden geschreven.
    - **Ja**: Windows staat niet toe dat er gegevens naar verwijderbare stations worden geschreven die niet met BitLocker zijn beveiligd. Als een ingevoegd verwijderbaar station niet is versleuteld, moet de gebruiker de BitLocker-installatiewizard voor het station doorlopen voordat schrijftoegang tot het station wordt verleend.

    - **Schrijftoegang blokkeren voor verwisselbare gegevensstations die niet zijn beveiligd door BitLocker**  
      CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **Niet geconfigureerd** (*standaard*): elke door BitLocker versleutelde schijf kan worden gebruikt.
      - **Ja**: de toegang tot verwisselbare stations blokkeren, tenzij ze zijn versleuteld op een computer die eigendom is van uw organisatie.

## <a name="next-steps"></a>Volgende stappen

[Instellingen voor eindpuntbeveiliging voor schijfversleuteling](../protect/endpoint-security-disk-encryption-policy.md)
