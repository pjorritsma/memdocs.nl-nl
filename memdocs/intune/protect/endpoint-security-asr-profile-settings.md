---
title: Intune-eindpuntbeveiligingsinstellingen om kwetsbaarheid voor aanvallen te verminderen | Microsoft Docs
description: Eindpuntbeveiligingsinstellingen om kwetsbaarheid voor aanvallen te verminderen in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
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
ms.openlocfilehash: a2b404e1741c93a6dbf5023f394f3b9528020617
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913457"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Beleidsinstellingen om kwetsbaarheid voor aanvallen te verminderen voor eindpuntbeveiliging in Intune

Bekijk de instellingen die u kunt configureren in profielen voor beleid voor *Kwetsbaarheid voor aanvallen verminderen* in het knooppunt voor eindpuntbeveiliging van Intune als onderdeel van een [eindpuntbeveiligingsbeleid](../protect/endpoint-security-policy.md).

Ondersteunde platforms en profielen:

- **Windows 10 en hoger**:
  - Profiel: **App- en browserisolatie**
  - Profiel: **Webbeveiliging**
  - Profiel: **Toepassingsbeheer**
  - Profiel: **Regels voor het verminderen van kwetsbaarheid voor aanvallen**
  - Profiel: **Apparaatbeheer**
  - Profiel: **Exploit Protection**

## <a name="app-and-browser-isolation-profile"></a>App- en browserisolatieprofiel

### <a name="app-and-browser-isolation"></a>App- en browserisolatie

- **Application Guard inschakelen voor Microsoft Edge (opties)**  
  CSP: [AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Niet geconfigureerd** (*standaard*)
  - **Ingeschakeld voor Edge** Application Guard is ingeschakeld voor Microsoft Edge, worden hiermee niet-goedgekeurde sites in een door Hyper-V gevirtualiseerde browsercontainer geopend.

  Indien ingesteld op *Ingeschakeld voor Microsoft Edge* zijn de volgende instellingen beschikbaar:
  
  - **Klembordgedrag**  
    CSP: [ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Kiezen welke kopieer- en plakbewerkingen zijn toegestaan van de lokale pc en een virtuele Application Guard-browser.
    - **Niet geconfigureerd** (*standaard*)
    - **Kopiëren en plakken tussen de pc en de browser blokkeren**
    - **Alleen kopiëren en plakken van de browser naar de pc toestaan**
    - **Alleen kopiëren en plakken van de pc naar de browser toestaan**
    - **Kopiëren en plakken tussen de pc en de browser toestaan**

  - **Externe inhoud blokkeren van sites die niet goedgekeurd zijn door het bedrijf**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: Voorkom dat inhoud van niet-goedgekeurde websites kan worden geladen.

  - **Logboeken verzamelen voor gebeurtenissen die plaatsvinden tijdens een browsesessie met Application Guard**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: logboeken verzamelen voor gebeurtenissen die plaatsvinden binnen een virtuele Application Guard-browsersessie.

  - **Toestaan dat door de gebruiker gegenereerde browsergegevens worden opgeslagen**  
    CSP: [AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: toestaan dat gebruikersgegevens die zijn gemaakt tijdens een virtuele Application Guard-browsersessie, moeten worden opgeslagen. Voorbeelden van gebruikersgegevens zijn wachtwoorden, favorieten en cookies.

  - **Hardwareversnelling voor grafische weergave inschakelen**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: binnen de virtuele browsesessie van Application Guard gebruikt u een virtuele grafische verwerkingseenheid om grafisch intensieve websites sneller te laden.

  - **Gebruikers toestaan om bestanden te downloaden op de host**  
    CSP: [SaveFilestoHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: gebruikers toestaan om bestanden te downloaden van de virtuele browser op het hostbesturingssysteem.

- **Application Guard: afdrukken naar lokale printers toestaan**  

  - **Niet geconfigureerd** (*standaard*)
  - **Ja** : afdrukken naar lokale printers toestaan.

- **Application Guard: afdrukken naar netwerkprinters toestaan**  

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: afdrukken naar netwerkprinters toestaan.

- **Application Guard: afdrukken naar PDF toestaan**  

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: afdrukken naar PDF toestaan.

- **Application Guard: afdrukken naar XPS**  

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: afdrukken naar XPS toestaan.

- **Windows-beleid voor netwerkisolatie**  
  
  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: Windows-beleid voor netwerkisolatie configureren.  
  
  Als de optie is ingesteld op *Ja*, kunt u de volgende instellingen configureren.

  - **IP-bereiken**  
    Vouw de vervolgkeuzelijst uit, selecteer **Toevoegen** en geef een *lager adres* en vervolgens een *hoger adres* op.

  - **Cloudresources**  
    Vouw de vervolgkeuzelijst uit, selecteer **Toevoegen**en geef vervolgens een *IP-adres of FQDN* en een *Proxy* op.

  - **Netwerkdomeinen**  
   Vouw de vervolgkeuzelijst uit, selecteer **Toevoegen**en geef vervolgens *Netwerkdomeinen* op.

  - **Proxyservers**  
    Vouw de vervolgkeuzelijst uit, selecteer **Toevoegen** en geef vervolgens *Proxyservers* op.

  - **Interne proxyservers**  
    Vouw de vervolgkeuzelijst uit, selecteer **Toevoegen** en geef vervolgens *Interne proxyservers* op.

  - **Neutrale resources**  
    Vouw de vervolgkeuzelijst uit, selecteer **Toevoegen**en geef vervolgens *Neutrale resources* op.

  - **Automatische detectie van andere proxyservers van ondernemingen uitschakelen**  
    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: automatische detectie van andere proxyservers van ondernemingen uitschakelen.

  - **Automatische detectie van andere IP-bereiken van ondernemingen uitschakelen**  
    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: automatische detectie van andere IP-bereiken van ondernemingen uitschakelen.

## <a name="web-protection-profile"></a>Webbeveiligingsprofiel

### <a name="web-protection"></a>Webbeveiliging

- **Netwerkbeveiliging inschakelen**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen**: netwerkbeveiliging wordt ingeschakeld voor alle gebruikers in het systeem.
  - **Controlemodus**: gebruikers worden niet geweerd uit gevaarlijke domeinen; in plaats daarvan worden er Windows-gebeurtenissen geregistreerd.

- **SmartScreen vereisen voor Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Ja**: gebruik SmartScreen om gebruikers tegen mogelijke oplichting door phishing en schadelijke software te beschermen.
  - **Niet geconfigureerd** (*standaard*)

- **Toegang tot schadelijke sites blokkeren**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Ja**: Gebruikers kunnen de Microsoft Defender SmartScreen-filterwaarschuwingen niet negeren en kunnen niet naar de site gaan.
  - **Niet geconfigureerd** (*standaard*)

- **Downloaden van niet-geverifieerde bestanden blokkeren**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Ja**: gebruikers kunnen de Microsoft Defender SmartScreen-filterwaarschuwingen niet negeren en kunnen geen niet-geverifieerde bestanden downloaden.
  - **Niet geconfigureerd** (*standaard*)

## <a name="application-control-profile"></a>Toepassingsbeheerprofiel

### <a name="microsoft-defender-application-control"></a>Microsoft Defender-toepassingsbeheer

- **Toepassingsbeheer app-kluis**  
  CSP: [AppLocker](/windows/client-management/mdm/applocker-csp)

  - **Niet geconfigureerd** (*standaard*)
  - **Onderdelen afdwingen en apps opslaan**
  - **Onderdelen controleren en apps opslaan**
  - **Onderdelen afdwingen, apps opslaan en Smartlocker**
  - **Onderdelen controleren, apps opslaan en Smartlocker**
   

- **Blokkeren dat gebruikers SmartScreen-waarschuwingen kunnen negeren**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Niet geconfigureerd** (*standaard*): gebruikers kunnen SmartScreen-waarschuwingen voor bestanden en schadelijke apps negeren.
  - **Ja**: SmartScreen is ingeschakeld en gebruikers kunnen geen waarschuwingen over bestanden of schadelijke apps overslaan.

- **Windows SmartScreen inschakelen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Niet-geconfigureerd** (*standaard*): hiermee wordt de standaardinstelling van Windows teruggezet. Dit betekent dat SmartScreen wordt ingeschakeld, maar gebruikers kunnen deze instelling indien gewenst wijzigen. Als u SmartScreen wilt uitschakelen, gebruikt u een aangepaste URI.
  - **Ja**: het gebruik van SmartScreen afdwingen voor alle gebruikers.

## <a name="attack-surface-reduction-rules-profile"></a>Regelprofiel voor het verminderen van kwetsbaarheid voor aanvallen

### <a name="attack-surface-reduction-rules"></a>Regels voor het verminderen van kwetsbaarheid voor aanvallen

- **Blokkeer referentiediefstal in het Windows-subsysteem voor de lokale beveiligingsautoriteit (lsass.exe)**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874499)

  Deze regel voor het verminderen van de kwetsbaarheid voor aanvallen wordt beheerd via de volgende GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen**: alle pogingen om referenties te stelen via lsass.exe worden geblokkeerd.
  - **Controlemodus**: gebruikers worden niet geweerd uit gevaarlijke domeinen; in plaats daarvan worden er Windows-gebeurtenissen geregistreerd.

- **Blokkeren dat onderliggende processen kunnen worden gemaakt in Adobe Reader**  
  [Regels voor het verminderen van kwetsbaarheid voor aanvallen beperken](https://go.microsoft.com/fwlink/?linkid=853979)
  
  Deze ASR-regel wordt beheerd via de volgende GUID: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Niet geconfigureerd** (*standaard*): de Windows-standaardwaarde wordt hersteld. Dit houdt in dat het maken van onderliggende processen niet wordt geblokkeerd.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen**: Adobe Reader mag geen onderliggende processen maken.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat onderliggende processen worden geblokkeerd.

- **Voorkomen dat Office-toepassingen code in andere processen injecteren**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872974)

  Deze ASR-regel wordt beheerd via de volgende GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**: Office-toepassingen mogen geen code in andere processen injecteren.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat Office-toepassingen uitvoerbare inhoud maken**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872975)

  Deze ASR-regel wordt beheerd via de volgende GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**: uitvoerbare inhoud maken wordt geblokkeerd in Office-toepassingen.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat Office-toepassingen onderliggende processen maken**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872976)

  Deze ASR-regel wordt beheerd via de volgende GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**: onderliggende processen maken wordt geblokkeerd in Office-toepassingen.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Win32 API-aanroepen blokkeren vanuit Office-macro's**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872977)

  Deze ASR-regel wordt beheerd via de volgende GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren** Office-macro's mogen niet gebruikmaken van Win32 API-aanroepen.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat Office-communicatietoepassingen onderliggende processen maken**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874499)  

  Deze ASR-regel wordt beheerd via de volgende GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Niet geconfigureerd** (*standaard*): de standaardinstelling van Windows is hersteld. Hierdoor kan het aanmaken van onderliggende processen niet worden geblokkeerd.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen**: voorkomen dat Office-communicatietoepassingen onderliggende processen maken.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat onderliggende processen worden geblokkeerd.

- **Uitvoering van mogelijk verborgen scripts (js/vbs/ps) voorkomen**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872978)

  Deze ASR-regel wordt beheerd via de volgende GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**: Defender blokkeert de uitvoering van verborgen scripts.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat JavaScript of VBScript gedownloade uitvoerbare inhoud start**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872979)

   Deze ASR-regel wordt beheerd via de volgende GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**: Defender blokkeert het uitvoeren van JavaScript- en VBScript-bestanden die van internet zijn gedownload.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat processen worden gemaakt die afkomstig zijn van PSExec- en WMI-opdrachten**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874500)

  Deze ASR-regel wordt beheerd via de volgende GUID: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**: het maken van processen door PSExec of WMI-opdrachten wordt geblokkeerd.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat niet-vertrouwde en niet-ondertekende processen kunnen worden uitgevoerd vanaf een USB**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874502)

  Deze ASR-regel wordt beheerd via de volgende GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**: niet-vertrouwde en niet-ondertekende processen die worden uitgevoerd vanaf een USB-stick worden geblokkeerd.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat uitvoerbare bestanden worden uitgevoerd tenzij deze voldoen aan een bepaalde gangbaarheid, ouderdom of criteria voor vertrouwde lijsten**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874503)

  Deze ASR-regel wordt beheerd via de volgende GUID: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Downloaden van uitvoerbare inhoud via e-mail- en webmailclients blokkeren**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Blokkeren**: het downloaden van uitvoerbare inhoud uit e-mail- en webmailclients wordt geblokkeerd.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Geavanceerde bescherming tegen ransomware gebruiken**  
   [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874504)

  Deze ASR-regel wordt beheerd via de volgende GUID: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet naar de standaardinstelling van Windows, die is uitgeschakeld.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen**
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Mapbeveiliging inschakelen**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Niet geconfigureerd** (*standaard*): deze instelling wordt teruggezet naar de standaardwaarde, die niet wordt gelezen of geschreven, en wordt geblokkeerd.
  - **Inschakelen**: voor niet-vertrouwde apps worden pogingen tot het wijzigen of verwijderen van bestanden in beveiligde mappen, of het schrijven naar schijfsectoren, door Defender geblokkeerd. Defender bepaalt automatisch welke toepassingen kunnen worden vertrouwd. U kunt ook uw eigen lijst met vertrouwde toepassingen definiëren.
  - **Controlemodus**: Windows-gebeurtenissen worden gegenereerd wanneer niet-vertrouwde toepassingen beheerde mappen gebruiken, maar er wordt geen blokkering afgedwongen.
  - **Schijfwijziging blokkeren**: alleen pogingen om naar schijfsectoren te schrijven, worden geblokkeerd.
  - **Schijfwijziging controleren**: er worden Windows-gebeurtenissen gegenereerd in plaats van pogingen om naar schijfsectoren te schrijven te blokkeren.
  
- **Bestanden en paden uitsluiten van regels voor het verminderen van kwetsbaarheid voor aanvallen**  
  CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  Vouw de vervolgkeuzelijst uit en selecteer vervolgens **Toevoegen** om een **Pad** te definiëren aan een bestand of map die u wilt uitsluiten van uw regels voor het verminderen van kwetsbaarheid voor aanvallen.

## <a name="device-control-profile"></a>Apparaatbeheerprofiel

### <a name="device-control"></a>Apparaatbeheer

- **Installatie van hardwareapparaten op basis van apparaat-id's**  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Met deze instelling kunt u een lijst opgeven met Plug en Play-hardware id's en compatibele id's voor apparaten die niet mogen worden geïnstalleerd in Windows. Deze beleidsinstelling heeft een hogere prioriteit dan welke andere beleidsinstelling dan ook waarmee Windows wordt toegestaan een apparaat te installeren.  Als u deze beleidsinstelling inschakelt op een externe desktopserver, heeft deze invloed op de omleiding van de opgegeven apparaten van een externe desktopclient naar de externe desktopserver.

  - **Niet geconfigureerd**
  - **Installatie van hardwareapparaten toestaan**: apparaten kunnen worden geïnstalleerd en bijgewerkt, voor zover dat door andere beleidsinstellingen is toegestaan of verboden.
  - **Installatie van hardwareapparaten blokkeren** (*standaard*): apparaten waarvan de hardware-id of compatibele id die in de door u gemaakte lijst staan, worden niet geïnstalleerd in Windows.

  Wanneer *Installatie van hardwareapparaten blokkeren* is ingesteld, kunt u de volgende instellingen configureren:

  - **Overeenkomende hardwareapparaten verwijderen**

    Deze instelling is alleen beschikbaar als *Installatie hardwareapparaten op apparaat-id* is ingesteld op *Installatie van hardwareapparaten blokkeren*.
    - **Ja**
    - **Niet geconfigureerd**

  - **Hardwareapparaat-id's die zijn geblokkeerd**  

    Deze instelling is alleen beschikbaar als *Installatie hardwareapparaten op apparaat-id* is ingesteld op *Installatie van hardwareapparaten blokkeren*.

    Selecteer **Toevoegen** en geef vervolgens de hardwareapparaat-id op die u wilt blokkeren.

- **Installatie van hardwareapparaten op basis van installatieklassen**  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  Met deze beleidsinstelling kunt u een lijst opgeven met GUID's (Globally Unique Identifiers) voor de installatieklasse van apparaten voor apparaatstuurprogramma's die niet mogen worden geïnstalleerd in Windows. Deze beleidsinstelling heeft een hogere prioriteit dan welke andere beleidsinstelling dan ook waarmee Windows wordt toegestaan een apparaat te installeren. Als u deze beleidsinstelling inschakelt op een externe desktopserver, heeft deze invloed op de omleiding van de opgegeven apparaten van een externe desktopclient naar de externe desktopserver.

  - **Niet geconfigureerd**
  - **Installatie van hardwareapparaten toestaan**: Windows kan apparaten installeren en bijwerken, voor zover dat door andere beleidsinstellingen is toegestaan of verboden.
  - **Installatie van hardwareapparaten blokkeren** (*standaard*): apparaten waarvan de installatieklasse-GUID's in de door u gemaakte lijst staan, worden niet geïnstalleerd in Windows.

  Als u deze instelling instelt op *Installatie van hardwareapparaten blokkeren*, kunt u *Overeenkomende hardwareapparaten verwijderen* en *Hardwareapparaat-id's die worden geblokkeerd* configureren.

  - **Overeenkomende hardwareapparaten verwijderen**

    Deze instelling is alleen beschikbaar als *Installatie hardwareapparaten op apparaat-id* is ingesteld op *Installatie van hardwareapparaten blokkeren*.
    - **Ja**
    - **Niet geconfigureerd**

  - **Hardwareapparaat-id's die zijn geblokkeerd**

    Deze instelling is alleen beschikbaar als *Installatie hardwareapparaten op apparaat-id* is ingesteld op *Installatie van hardwareapparaten blokkeren*.

    Selecteer **Toevoegen** en geef vervolgens de hardwareapparaat-id op die u wilt blokkeren.

- **Verwijderbare stations scannen tijdens een volledige scan**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Niet-geconfigureerd** (*standaard*): bij deze instelling wordt de standaardwaarde van de client teruggezet: hierbij worden verwijderbare stations gescand, maar de gebruiker kan het scannen uitschakelen.
  - **Ja**: tijdens een volledige scan worden verwijderbare stations (bijvoorbeeld USB-sticks) gescand.

- **Direct Memory Access blokkeren**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)

  Deze beleidsinstelling wordt uitsluitend afgedwongen wanneer BitLocker of apparaatversleuteling is ingeschakeld.

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: Blokkeer directe geheugentoegang (DMA) voor alle downstream hot-pluggable PCI-poorten totdat een gebruiker zich bij Windows aanmeldt. Zodra een gebruiker zich heeft aangemeld, wordt in Windows een lijst gemaakt van de PCI-apparaten die met de PCI-poorten van de host zijn verbonden. Steeds wanneer de gebruiker het apparaat vergrendelt, wordt DMA geblokkeerd op hot-pluggable PCI-poorten zonder onderliggende apparaten totdat de gebruiker zich opnieuw aanmeldt. Apparaten die al waren geïnventariseerd toen het apparaat was ontgrendeld, blijven werken totdat ze worden losgekoppeld.

- **Opsomming van externe apparaten die niet compatibel zijn met DMA-beveiliging van kernel**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Dit beleid biedt extra beveiliging tegen externe DMA-compatibele apparaten. Het geeft u meer controle over de opsomming van externe DMA-compatibele apparaten die niet compatibel zijn met hertoewijzing/apparaatgeheugenisolatie en sandbox van DMA.

  Dit beleid wordt alleen uitgevoerd als DMA-beveiliging van kernel wordt ondersteund en ingeschakeld door de systeemfirmware. De kernel-DMA-beveiliging is een platformfunctie die op het moment van productie moet worden ondersteund door het systeem. Bekijk het veld DMA-beveiliging van kernel op de overzichtspagina van MSINFO32.exe om te controleren of het systeem DMA-beveiliging van kernel ondersteunt.

  - **Niet-geconfigureerd** - (*standaard*)
  - **Alles blokkeren**
  - **Alles toestaan**

- **Bluetooth-verbindingen blokkeren**  
  CSP: [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: Bluetooth-verbindingen van en naar het apparaat blokkeren.

- **Bluetooth-zichtbaarheid blokkeren**  
  CSP: [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: Hiermee wordt voorkomen dat het apparaat kan worden gedetecteerd door andere Bluetooth-apparaten.

- **Vooraf koppelen van Bluetooth blokkeren**  
  CSP: [Bluetooth/AllowPrepairing](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: Hiermee wordt voorkomen dat bepaalde Bluetooth-apparaten automatisch worden gekoppeld met een hostapparaat.

- **Bluetooth-reclame blokkeren**  
  CSP: [Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: Hiermee wordt voorkomen dat het apparaat Bluetooth-reclames verzendt.  

- **Dichtstbijzijnde Bluetooth-verbindingen blokkeren**  
  CSP: [Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections): : Hiermee wordt voorkomen dat gebruikers Swift Pair en andere scenario’s op basis van nabijheid gebruiken

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: Hiermee wordt voorkomen dat een apparaatgebruiker Swift Pair en andere op nabijheid gebaseerde scenario's gebruikt.  

  [Bluetooth/AllowPromptedProximalConnections CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Services waarvoor Bluetooth is toegestaan**  
  CSP: [Bluetooth/ServicesAllowedList](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist).  
  Raadpleeg [ServicesAllowedList usage guide](/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) (Engelstalig) voor meer informatie over de lijst met services

  - **Toevoegen** : Hiermee geeft u toegestane Bluetooth-services en -profielen op als hexadecimale tekenreeksen, zoals `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.
  - **Importeren**: Hiermee importeert u een CSV-bestand met een lijst met Bluetooth-services en -profielen als hexadecimale tekenreeksen, zoals `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`

## <a name="exploit-protection-profile"></a>Exploit Protection-profiel

### <a name="exploit-protection"></a>Exploit Protection

- **XML uploaden**  
  CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  Hiermee kan de IT-beheerder een configuratie pushen die de gewenste systeem- en toepassingbeperkingsopties voor alle apparaten in de organisatie aangeeft. De configuratie wordt vertegenwoordigd door een XML-bestand. Exploit Protection kan apparaten helpen te beschermen tegen malware die exploits gebruikt om zichzelf te verspreiden en andere apparaten te infecteren. U gebruikt de Windows-beveiligingsapp of PowerShell om een set beperkingen te maken (dit wordt een configuratie genoemd). U kunt deze configuratie vervolgens als XML-bestand exporteren en delen met meerdere apparaten in uw netwerk, zodat ze allemaal dezelfde set beperkingsinstellingen hebben. U kunt ook een bestaand XML-bestand met een EMET-configuratie naar een XML-bestand voor exploitbeveiligingsconfiguratie converteren en importeren.

  Kies **XML-bestand selecteren**, geef de XML-bestandsupload op en klik vervolgens op **Selecteren**.
  - **Niet geconfigureerd** (*standaard*)
  - **Ja**

- **Blokkeren dat gebruikers de beveiligingsinterface van Exploit Guard kunnen bewerken**  
  CSP: [DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Niet-geconfigureerd** (*default*) - lokale gebruikers mogen geen wijzigingen aanbrengen in het instellingengebied voor Exploit Protection.
  - **Ja** - Hiermee voorkomt u dat gebruikers wijzigingen aanbrengen in de Exploit Protection-instellingen in het Microsoft Defender-beveiligingscentrum.

## <a name="next-steps"></a>Volgende stappen

[Instellingen voor eindpuntbeveiliging voor ASR](../protect/endpoint-security-asr-policy.md)