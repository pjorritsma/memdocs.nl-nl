---
title: Beveiligingsbasislijninstellingen van Intune voor Microsoft Defender Advanced Threat Protection
titleSuffix: Microsoft Intune
description: Beveiligingsbasislijninstellingen die door Intune worden ondersteund voor het beheren van Microsoft Defender Advanced Threat Protection
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: e1081395c733807c38dc940ebd1b7c2765da7a9a
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693400"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Microsoft Defender Advanced Threat Protection-basislijninstellingen voor Intune

Bekijk de basislijninstellingen voor Microsoft Defender Advanced Threat Protection die worden ondersteund door Microsoft Intune. De standaardinstellingen van de basislijn Advanced Threat Protection (ATP) vertegenwoordigen de aanbevolen configuratie voor ATP en komen mogelijk niet overeen met de standaardinstellingen voor andere beveiligingsbasislijnen.

::: zone pivot="atp-april-2020"

De informatie in dit artikel is van toepassing op versie 4 van de Microsoft Defender ATP-basislijn die is uitgebracht op 21 april 2020. Als u wilt weten wat er is gewijzigd met deze versie van de basislijn in vergelijking met vorige versies, gebruikt u de actie [Basislijnen vergelijken](../protect/security-baselines.md#compare-baseline-versions) die beschikbaar is wanneer u het deelvenster *Versies* voor deze basislijn weergeeft.

::: zone-end
::: zone pivot="atp-march-2020"

De informatie in dit artikel is van toepassing op versie 3 van de Microsoft Defender ATP-basislijn die is uitgebracht op 1 maart 2020. Als u wilt weten wat er is gewijzigd met deze versie van de basislijn in vergelijking met vorige versies, gebruikt u de actie [Basislijnen vergelijken](../protect/security-baselines.md#compare-baseline-versions) die beschikbaar is wanneer u het deelvenster *Versies* voor deze basislijn weergeeft.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


De basislijn Microsoft Defender Advanced Threat Protection is beschikbaar als uw omgeving voldoet aan de vereisten voor het gebruik van [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites).

Deze basislijn is geoptimaliseerd voor fysieke apparaten en wordt momenteel niet aanbevolen voor gebruik met virtuele machines (VM's) of VDI-eindpunten. Bepaalde basislijninstellingen kunnen invloed hebben op externe interactieve sessies in gevirtualiseerde omgevingen. Voor meer informatie ziet u [Increase compliance to the Microsoft Defender ATP security baseline](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) (Naleving met de Microsoft Defender ATP-beveiligingsbasislijn vergroten) in de Windows-documentatie.


## <a name="application-guard"></a>Application Guard

Zie [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) in de Windows-documentatie voor meer informatie.  

Wanneer u Microsoft Edge gebruikt, beschermt Microsoft Defender Application Guard uw omgeving tegen sites die niet worden vertrouwd door uw organisatie. Als gebruikers sites bezoeken die niet worden vermeld in uw geïsoleerde netwerkgrens, worden deze sites geopend in een virtuele browsersessie in Hyper-V. Vertrouwde sites worden gedefinieerd door een netwerkgrens.  

- **Application Guard inschakelen voor Microsoft Edge (opties)**  
  CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Ingeschakeld voor Edge** (*standaard*): Application Guard opent niet-goedgekeurde sites in door Hyper-V gevirtualiseerde browsercontainers.
  - **Niet geconfigureerd**: elke site (vertrouwd en niet-vertrouwd) wordt op het apparaat geopend, en niet in een gevirtualiseerde container.  
  
  Als deze optie is ingesteld op *Inschakelen voor Edge*, kunt u *Externe inhoud blokkeren van sites die niet goedgekeurd zijn door het bedrijf* en *Klembordgedrag* configureren.

  - **Externe inhoud blokkeren van sites die niet goedgekeurd zijn door het bedrijf**  
    CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Ja** (*standaard*): inhoud van niet-goedgekeurde websites blokkeren, zodat deze niet kan worden geladen.
    - **Niet geconfigureerd**: niet-bedrijfssites kunnen op het apparaat worden geopend

  - **Klembordgedrag**  
    CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Kies welke kopieer- en plakbewerkingen zijn toegestaan tussen de lokale pc en de virtuele browser van Application Guard. Opties zijn onder andere:
    - **Niet geconfigureerd**  
    - **Kopiëren en plakken tussen de pc en de browser blokkeren** (*standaard*): beide blokkeren. Er kunnen geen gegevens tussen de pc en de virtuele browser worden overgedragen.
    - **Kopiëren en plakken van browser naar pc toestaan**: gegevens kunnen niet worden overgedragen van de pc naar de virtuele browser.
    - **Uitsluitend kopiëren en plakken van pc naar browser toestaan**: gegevens kunnen niet worden overgedragen van de virtuele browser naar de host-pc.
    - **Kopiëren en plakken tussen de pc en de browser toestaan**: er vindt geen blokkering van inhoud plaats.

- **Windows-beleid voor netwerkisolatie**  
  CSP: [CSP-beleid - NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation)

  Geef een lijst met *netwerkdomeinen* op; dit zijn bedrijfsresources die worden gehost in de cloud die Application Guard als bedrijfssite behandelt
  - **Configureren** (*standaard*)
  - **Niet geconfigureerd**

  Als dit wordt ingesteld op *Configureren*, kunt u vervolgens *Netwerkdomeinen* definiëren.

  - **Netwerkdomeinen**  
    Selecteer **Toevoegen** en geef domeinen, IP-adresbereiken en netwerkgrenzen op. Standaard is *securitycenter.windows.com* geconfigureerd.

## <a name="bitlocker"></a>BitLocker

Zie [BitLocker Group Policy settings](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) (Instellingen voor BitLocker-groepsbeleid) in de Windows-documentatie voor meer informatie.

- **Vereisen dat opslagkaarten worden versleuteld (alleen mobiel)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  Deze instelling geldt alleen voor Windows Mobile- en Mobile Enterprise SKU-apparaten.
  - **Ja** (*standaard*): versleuteling op opslagkaarten is vereist voor mobiele apparaten.
  - **Niet geconfigureerd**: de instelling wordt teruggezet naar de standaardwaarde van het besturingssysteem; hierbij is geen versleuteling van de opslagkaart vereist.

- **Volledige schijfversleuteling voor systeemstations en vaste gegevensstations inschakelen**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  Als het station is versleuteld voordat dit beleid werd toegepast, wordt er geen extra actie ondernomen. Als de versleutelingsmethode en opties overeenkomen met die van dit beleid, wordt aangegeven dat de configuratie is geslaagd. Als een actieve BitLocker-configuratie niet overeenkomt met dit beleid, wordt waarschijnlijk een fout geretourneerd.
  
  Om dit beleid toe te passen op een schijf die al is versleuteld, ontsleutelt u het station en past u het MDM-beleid opnieuw toe. In Windows is standaard geen BitLocker-stationversleuteling vereist, maar bij Azure AD-deelname en Microsoft-accountregistratie/-aanmelding wordt met de automatische versleuteling mogelijk ook BitLocker ingeschakeld (XTS-AES 128-bits versleuteling).

  - **Ja** (*standaard*): het gebruik van BitLocker wordt afgedwongen.
  - **Niet geconfigureerd**: het gebruik van BitLocker wordt niet afgedwongen.

- **BitLocker-beleid voor systeemstations**  
  [Instellingen voor BitLocker-groepsbeleid](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configureren** (*standaard*)
  - **Niet geconfigureerd**

  Als deze optie wordt ingesteld op *Configureren*, kunt u de *versleutelingsmethode voor systeemstations configureren*.

  - **Versleutelingsmethode voor systeemstations configureren**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Deze instelling is beschikbaar als het *beleid voor BitLocker-systeemstations* is ingesteld op *Configureren*.  

    Configureer de versleutelingsmethode en coderingssterkte voor systeemstations.  *XTS-AES, 128-bits* is de standaardversleutelingsmethode van Windows en de aanbevolen waarde.

    - **Niet geconfigureerd** (*standaard*)
    - **AES 128-bits CBC**
    - **AES 256-bits CBC**
    - **AES 128-bits XTS**
    - **AES 256-bits XTS**

- **BitLocker-beleid voor vaste stations**  
  [Instellingen voor BitLocker-groepsbeleid](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Configureren** (*standaard*)
  - **Niet geconfigureerd**

  Als deze optie is ingesteld op *Configureren*, kunt u *Schrijftoegang blokkeren configureren voor vaste gegevensstations die niet zijn beveiligd door BitLocker* en de *Versleutelingsmethode voor vaste gegevensstations configureren*.

  - **Schrijftoegang blokkeren voor vaste gegevensstations die niet zijn beveiligd door BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    Deze instelling is beschikbaar als het *beleid voor vaste BitLocker-stations* is ingesteld op *Configureren*.

    - **Niet-geconfigureerd** (*standaard*): gegevens kunnen naar niet-versleutelde vaste stations worden geschreven.
    - **Ja**: Windows staat niet toe dat er gegevens naar vaste stations worden geschreven die niet met BitLocker zijn beveiligd. Als een vast station niet is versleuteld, moet de gebruiker de BitLocker-installatiewizard voor het station doorlopen voordat schrijftoegang wordt verleend.

  - **Versleutelingsmethode voor vaste gegevensstations configureren**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Deze instelling is beschikbaar als het *beleid voor vaste BitLocker-stations* is ingesteld op *Configureren*.

    Configureer de versleutelingsmethode en coderingssterkte voor vaste gegevensstations. *XTS-AES, 128-bits* is de standaardversleutelingsmethode van Windows en de aanbevolen waarde.

    - **Niet geconfigureerd** (*standaard*)
    - **AES 128-bits CBC**
    - **AES 256-bits CBC**
    - **AES 128-bits XTS**
    - **AES 256-bits XTS**

- **BitLocker-beleid voor losse stations**  
  [Instellingen voor BitLocker-groepsbeleid](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Configureren** (*standaard*)
  - **Niet geconfigureerd**

  Als deze optie is ingesteld op *Configureren*, kunt u de *Versleutelingsmethode voor verwijderbare gegevensstations configureren* en de *Schrijftoegang blokkeren configureren voor vaste gegevensstations die niet zijn beveiligd door BitLocker*.

  - **Versleutelingsmethode voor verwijderbare gegevensstations configureren**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    Deze instelling is beschikbaar als het *BitLocker-beleid voor verwijderbare stations* is ingesteld op *Configureren*.

    Configureer de versleutelingsmethode en coderingssterkte voor verwijderbare gegevensstations. *XTS-AES, 128-bits* is de standaardversleutelingsmethode van Windows en de aanbevolen waarde.

    - **Niet geconfigureerd**
    - **AES 128-bits CBC**
    - **AES 256-bits CBC** (*standaard*)
    - **AES 128-bits XTS**
    - **AES 256-bits XTS**

  - **Schrijftoegang blokkeren voor verwisselbare gegevensstations die niet zijn beveiligd door BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    Deze instelling is beschikbaar als het *Bitlocker-beleid voor verwijderbare stations* is ingesteld op *Configureren*.

    - **Niet-geconfigureerd** (*standaard*): gegevens kunnen naar niet-versleutelde verwijderbare stations worden geschreven.  
    - **Ja**: Windows staat niet toe dat er gegevens naar verwijderbare stations worden geschreven die niet met BitLocker zijn beveiligd. Als een verwijderbaar station niet is versleuteld, moet de gebruiker de BitLocker-installatiewizard voor het station doorlopen voordat schrijftoegang wordt verleend.

## <a name="browser"></a>Browser

- **SmartScreen vereisen voor Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Ja** (*standaard*): gebruik SmartScreen om gebruikers tegen mogelijke oplichting door phishing en schadelijke software te beschermen.
  - **Niet geconfigureerd**

- **Toegang tot schadelijke sites blokkeren**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Ja** (*standaard*): gebruikers kunnen de Microsoft Defender SmartScreen-filterwaarschuwingen niet negeren en kunnen niet naar de site gaan.
  - **Niet geconfigureerd**

- **Downloaden van niet-geverifieerde bestanden blokkeren**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Ja** (*standaard*): gebruikers kunnen de Microsoft Defender SmartScreen-filterwaarschuwingen niet negeren en kunnen geen niet-geverifieerde bestanden downloaden.
  - **Niet geconfigureerd**

## <a name="data-protection"></a>Gegevensbescherming

- **Direct Memory Access blokkeren**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  Deze beleidsinstelling wordt uitsluitend afgedwongen wanneer BitLocker of apparaatversleuteling is ingeschakeld.

  - **Ja** (*standaard*): blokkeert directe geheugentoegang (DMA) voor alle downstream hot-pluggable PCI-poorten totdat een gebruiker zich bij Windows aanmeldt. Zodra een gebruiker zich heeft aangemeld, wordt in Windows een lijst gemaakt van de PCI-apparaten die met de PCI-poorten van de host zijn verbonden. Steeds wanneer de gebruiker het apparaat vergrendelt, wordt DMA geblokkeerd op hot-pluggable PCI-poorten zonder onderliggende apparaten totdat de gebruiker zich opnieuw aanmeldt. Apparaten die al waren geïnventariseerd toen het apparaat was ontgrendeld, blijven werken totdat ze worden losgekoppeld.
  - **Niet geconfigureerd**

## <a name="device-guard"></a>Device Guard  

- **Credential Guard inschakelen**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard maakt gebruik van de Windows Hypervisor om beveiliging te bieden. Hierbij zijn beveiligd opstarten en DMA-beveiliging nodig én moet aan de hardwarevereisten worden voldaan.

  - **Niet-geconfigureerd** : het gebruik van Credential Guard uitschakelen. Dit is de Windows-standaardinstelling.
  - **Inschakelen met UEFI-vergrendeling** (*standaard*): hiermee schakelt u Credential Guard in en staat u niet toe dat deze extern wordt uitgeschakeld. De permanente UEFI-configuratie moet namelijk handmatig worden gewist.
  - **Inschakelen zonder UEFI-vergrendeling**: Credential Guard inschakelen en toestaan dat deze wordt uitgeschakeld zonder fysieke toegang tot de computer.

## <a name="device-installation"></a>Apparaatinstallatie

- **Installatie van hardwareapparaten op basis van apparaat-id's**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  Met deze beleidsinstelling kunt u een lijst opgeven met Plug en Play-hardware id's en compatibele id's voor apparaten die niet mogen worden geïnstalleerd in Windows. Deze beleidsinstelling heeft een hogere prioriteit dan welke andere beleidsinstelling dan ook waarmee Windows wordt toegestaan een apparaat te installeren.  Als u deze beleidsinstelling inschakelt op een externe desktopserver, heeft deze invloed op de omleiding van de opgegeven apparaten van een externe desktopclient naar de externe desktopserver.

  - **Niet geconfigureerd**
  - **Installatie van hardwareapparaten toestaan**: apparaten kunnen worden geïnstalleerd en bijgewerkt, voor zover dat door andere beleidsinstellingen is toegestaan of verboden.
  - **Installatie van hardwareapparaten blokkeren** (*standaard*): apparaten waarvan de hardware-id of compatibele id die in de door u gemaakte lijst staan, worden niet geïnstalleerd in Windows.

  Als u deze instelling instelt op *Installatie van hardwareapparaten blokkeren*, kunt u *Overeenkomende hardwareapparaten verwijderen* en *Hardwareapparaat-id's die worden geblokkeerd* configureren.

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

## <a name="dma-guard"></a>DMA Guard

- **Opsomming van externe apparaten die niet compatibel zijn met DMA-beveiliging van kernel**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  Dit beleid biedt extra beveiliging tegen externe DMA-compatibele apparaten. Het geeft u meer controle over de opsomming van externe DMA-compatibele apparaten die niet compatibel zijn met hertoewijzing/apparaatgeheugenisolatie en sandbox van DMA.
  
  Dit beleid wordt alleen uitgevoerd als DMA-beveiliging van kernel wordt ondersteund en ingeschakeld door de systeemfirmware. De kernel-DMA-beveiliging is een platformfunctie die op het moment van productie moet worden ondersteund door het systeem. Bekijk het veld DMA-beveiliging van kernel op de overzichtspagina van MSINFO32.exe om te controleren of het systeem DMA-beveiliging van kernel ondersteunt.

  - **Niet-geconfigureerd** - (*standaard*)
  - **Alles blokkeren**
  - **Alles toestaan**

## <a name="endpoint-detection-and-response"></a>Eindpuntdetectie en -respons

Zie [WindowsAdvancedThreatProtection](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) CSP in de Windows-documentatie voor meer informatie over de volgende instellingen.

- **Voorbeelddeling voor alle bestanden**  
  CSP: [Configuration/SampleSharing](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Hiermee wordt de configuratieparameter van de voorbeelddeling van Microsoft Defender Advanced Threat Protection geretourneerd of ingesteld.  
  
  - **Ja** (*standaard*)
  - **Niet geconfigureerd**

- **Frequentie van telemetrierapporten versnellen**  
  CSP: [Configuration/TelemetryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  De frequentie van telemetrierapporten van Microsoft Defender Advanced Threat Protection versnellen.  

  - **Ja** (*standaard*)
  - **Niet geconfigureerd**

## <a name="firewall"></a>Firewall

Raadpleeg [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) in de Windows-documentatie voor meer informatie.

- **Stateful File Transfer Protocol (FTP) blokkeren**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Ja** (*standaard*)
  - **Niet geconfigureerd**: de firewall maakt gebruik van een FTP om secundaire netwerkverbindingen te controleren en te filteren, waardoor uw firewallregels mogelijk worden genegeerd.

- **Aantal seconden dat een beveiligingskoppeling inactief kan zijn voordat deze wordt verwijderd**  
CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Geef op hoe lang de beveiligingskoppelingen worden bewaard als er geen sprake meer is van netwerkverkeer. Als dit niet wordt geconfigureerd, verwijdert het systeem een beveiligingskoppeling nadat deze gedurende *300* seconden inactief is geweest (de standaardinstelling).
  
  Het getal moet tussen de **300** en **3600** seconden liggen.

- **Codering van vooraf-gedeelde sleutels**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   Als u geen UTF-8 vereist, worden vooraf gedeelde sleutels in eerste instantie versleuteld met UTF-8. Daarna kunnen gebruikers van het apparaat een andere versleutelingsmethode kiezen.

  - **Niet geconfigureerd**
  - **Geen**
  - **UTF8** (*standaard*)

- **Verificatie van certificaatintrekkingslijst (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Geef aan hoe de controle van certificaatintrekkingslijsten (CRL's) wordt afgedwongen.  

  - **Niet-geconfigureerd** (*standaard*): CRL-verificatie is uitgeschakeld.
  - **Geen**
  - **Poging**
  - **Vereisen**

- **Pakketten in wachtrij plaatsen**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Hiermee kunt u opgeven hoe schalen voor software aan de ontvangstzijde wordt ingeschakeld voor versleuteld ontvangen en ongecodeerd doorsturen in het scenario voor de IPsec-tunnelgateway. Met deze instelling wordt gegarandeerd dat de pakketvolgorde behouden blijft.

  - **Niet-geconfigureerd** (*standaard*): voor het in de wachtrij plaatsen van pakketten wordt de standaardinstelling van de client gebruikt. Dit is uitgeschakeld.
  - **Uitgeschakeld**
  - **Inkomende wachtrij**
  - **Uitgaande wachtrij**
  - **Beide wachtrijen**

- **Persoonlijk firewallprofiel**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Configureren** (*standaard*)
  - **Niet geconfigureerd**

  Wanneer dit is ingeschakeld op *Configureren*, kunt u de volgende aanvullende instellingen configureren.

  - **Geblokkeerde binnenkomende verbindingen**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Unicast-antwoorden voor multicast-broadcasts vereist**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Verborgen modus vereist**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Uitgaande verbindingen vereist**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Binnenkomende meldingen geblokkeerd**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Globale poortregels van groepsbeleid samengevoegd**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Verborgen modus geblokkeerd**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Firewall ingeschakeld**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Niet geconfigureerd**
    - **Geblokkeerd**
    - **Toegestaan** (*standaard*)

  - **Regels voor gemachtigde toepassingen van groepsbeleid niet samengevoegd**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Beveiligingsregels voor verbindingen van groepsbeleid niet samengevoegd**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Inkomend verkeer vereist**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Beleidsregels van groepsbeleid niet samengevoegd**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

- **Openbaar firewallprofiel**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Configureren** (*standaard*)
  - **Niet geconfigureerd**

  Wanneer dit is ingeschakeld op *Configureren*, kunt u de volgende aanvullende instellingen configureren.

  - **Geblokkeerde binnenkomende verbindingen**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Unicast-antwoorden voor multicast-broadcasts vereist**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Verborgen modus vereist**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Uitgaande verbindingen vereist**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Regels voor gemachtigde toepassingen van groepsbeleid niet samengevoegd**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Binnenkomende meldingen geblokkeerd**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Globale poortregels van groepsbeleid samengevoegd**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Verborgen modus geblokkeerd**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Firewall ingeschakeld**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Niet geconfigureerd**
    - **Geblokkeerd**
    - **Toegestaan** (*standaard*)

  - **Beveiligingsregels voor verbindingen van groepsbeleid niet samengevoegd**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Inkomend verkeer vereist**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Beleidsregels van groepsbeleid niet samengevoegd**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

- **Firewallprofiel voor domein**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Unicast-antwoorden voor multicast-broadcasts vereist**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Regels voor gemachtigde toepassingen van groepsbeleid niet samengevoegd**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**  

  - **Binnenkomende meldingen geblokkeerd**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Globale poortregels van groepsbeleid samengevoegd**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Verborgen modus geblokkeerd**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Firewall ingeschakeld**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Niet geconfigureerd**
    - **Geblokkeerd**
    - **Toegestaan** (*standaard*)

  - **Beveiligingsregels voor verbindingen van groepsbeleid niet samengevoegd**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

  - **Beleidsregels van groepsbeleid niet samengevoegd**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Ja** (*standaard*)
    - **Niet geconfigureerd**

## <a name="microsoft-defender"></a>Microsoft Defender

- **Dagelijkse snelle scan uitvoeren om**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Configureer wanneer de dagelijkse snelle scan wordt uitgevoerd. Standaard wordt de scan uitgevoerd om **2:00 uur**.

- **Geplande begintijd voor het scannen**  
  
  Standaard is **2:00 uur** ingesteld.

- **Lage CPU-prioriteit voor geplande scans configureren**  
  CSP: [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Ja** (*standaard*)
  - **Niet geconfigureerd**

- **Voorkomen dat Office-communicatietoepassingen onderliggende processen maken**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874499)  

  Deze ASR-regel wordt beheerd via de volgende GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Niet geconfigureerd**: de Windows-standaardwaarde wordt hersteld. Dit houdt in dat het maken van onderliggende processen niet wordt geblokkeerd.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen** (*standaard*): voorkomen dat Office-communicatietoepassingen onderliggende processen maken.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat onderliggende processen worden geblokkeerd.

- **Blokkeren dat onderliggende processen kunnen worden gemaakt in Adobe Reader**  
  [Regels voor het verminderen van kwetsbaarheid voor aanvallen beperken](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **Niet geconfigureerd**: de Windows-standaardwaarde wordt hersteld. Dit houdt in dat het maken van onderliggende processen niet wordt geblokkeerd.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen** (*standaard*): Adobe Reader mag geen onderliggende processen maken.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat onderliggende processen worden geblokkeerd.

- **Inkomende e-mailberichten scannen**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Ja** (*standaard*): het postvak IN en mailbestanden (bijvoorbeeld met de indelingen PST, DBX, MNX, MIME en BINHEX) worden gescand.
  - **Niet-geconfigureerd**: de instelling krijgt weer de standaardwaarde van de client bij e-mailbestanden die niet worden gescand.

- **Realtime-beveiliging inschakelen**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Ja** (*standaard*): er wordt realtime bewaking afgedwongen en de gebruiker kan dit niet uitschakelen.
  - **Niet-geconfigureerd**: de instelling krijgt weer de standaardwaarde van de client. Deze standaardwaarde is Ingeschakeld en de gebruiker kan dit niet wijzigen. Als u realtime bewaking wilt uitschakelen, gebruikt u een aangepaste URI.

- **Aantal dagen (0-90) voor het bewaren van schadelijke software in quarantaine**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Configureer het aantal dagen dat items moeten worden bewaard in de quarantainemap voordat ze worden verwijderd. De standaardwaarde is nul (**0**), wat erin resulteert dat in quarantaine geplaatste bestanden nooit worden verwijderd.

- **Defender-systeemscan plannen**  
  CSP: [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Plan op welke dag Defender apparaten moet scannen. Standaard wordt de scan **door de gebruiker gedefinieerd**, maar er kan ook worden gekozen voor *elke dag*, een specifieke dag van de week of *Geen scan inplannen*.

- **Extra tijd (0-50 seconden) om de time-out voor cloudbeveiliging uit te breiden**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender Antivirus blokkeert automatisch verdachte bestanden gedurende tien seconden, zodat de bestanden in de cloud kunnen worden gescand om er zeker van te zijn dat ze veilig zijn. Met deze instelling kunt u maximaal 50 seconden extra toevoegen aan deze time-out.  De time-out is standaard ingesteld op nul (**0**).

- **Toegewezen netwerkschijven scannen tijdens een volledige scan**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Ja** (*standaard*): tijdens een volledige scan worden ook toegewezen netwerkschijven gescand.
  - **Niet-geconfigureerd**: de client maakt gebruik van de standaardinstellingen, waarbij het scannen van toegewezen netwerkschijven wordt uitgeschakeld.

- **Netwerkbeveiliging inschakelen**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Ja** (*standaard*): schadelijk verkeer blokkeren dat is gedetecteerd door handtekeningen in het netwerkinspectiesysteem (NIS).
  - **Niet geconfigureerd**

- **Alle gedownloade bestanden en bijlagen scannen**  
  CSP: [Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Ja** (*standaard*): alle gedownloade bestanden en bijlagen worden gescand. De instelling krijgt weer de standaardwaarde van de client. Deze standaardwaarde is Ingeschakeld en de gebruiker kan dit niet wijzigen. Als u deze instelling wilt uitschakelen, gebruikt u een aangepaste URI.
  - **Niet-geconfigureerd**: de instelling krijgt weer de standaardwaarde van de client. Deze standaardwaarde is Ingeschakeld en de gebruiker kan dit niet wijzigen. Als u deze instelling wilt uitschakelen, gebruikt u een aangepaste URI.

::: zone-end
::: zone pivot="atp-april-2020"

- **Beveiliging Blokkeren bij toegang**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Ja**
  - **Niet geconfigureerd** (*standaard*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Beveiliging Blokkeren bij toegang**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Ja** (*standaard*)
  - **Niet geconfigureerd**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Browserscripts scannen**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Ja** (*standaard*): de functie voor het scannen van scripts van Microsoft Defender wordt afgedwongen en de gebruiker kan deze niet uitschakelen.
  - **Niet geconfigureerd**: de instelling wordt teruggezet op de standaardinstelling van de client. Dat betekent dat het scannen van scripts is ingeschakeld. De gebruiker kan dit echter uitschakelen.

- **Gebruikerstoegang tot de Microsoft Defender-app blokkeren**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **Ja** (*standaard*): de gebruikersinterface (UI) van Microsoft Defender is niet toegankelijk en meldingen worden onderdrukt
  - **Niet-geconfigureerd**: als dit wordt ingesteld op Ja, wordt de gebruikersinterface (UI) van Windows Defender ontoegankelijk en worden meldingen onderdrukt. Als dit wordt ingesteld op Niet-geconfigureerd, wordt de instelling teruggezet op de standaardinstelling van de client, waarbij de gebruikersinterface en meldingen zijn toegestaan

- **Maximaal toegestane CPU-gebruik (0-100 procent) per scan**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Geef als percentage de maximale hoeveelheid CPU op die moet worden gebruikt voor een scan. De standaardwaarde is **50**.

- **Type scan**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **Door de gebruiker gedefinieerd**
  - **Uitgeschakeld**
  - **Snelle scan** (*standaard*)
  - **Volledige scan**

- **Voer in hoe vaak (0-24 uur) er moet worden gecontroleerd op updates van de beveiligingsinformatie**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Geef op hoe vaak er moet worden gecontroleerd op bijgewerkte handtekeningen, in uren. Met een waarde van 1 wordt bijvoorbeeld elk uur gecontroleerd. Met de waarde 2 wordt elke twee uur gecontroleerd, enzovoort.

  Als er geen waarde is gedefinieerd, gebruiken apparaten de standaardwaarde van de client: **8** uur.

- **Voorbeeld van een Defender-toestemming voor indiening**  
  CSP: [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Hiermee wordt het gebruikerstoestemmingsniveau in Microsoft Defender gecontroleerd om gegevens te verzenden. Als de vereiste toestemming al is verleend, worden de gegevens door Microsoft Defender ingediend. Als dit niet het geval is (en als de gebruiker heeft opgegeven dat deze vraag nooit mag worden gesteld), wordt de gebruikersinterface geopend om de gebruiker om toestemming te vragen (wanneer *Cloudbeveiliging* is ingesteld op *Ja*) voordat gegevens worden verzonden.

  - **Veilige voorbeelden automatisch verzenden** (*standaard*)
  - **Altijd vragen**
  - **Nooit verzenden**
  - **Alle voorbeelden automatisch verzenden**

- **Cloudbeveiligingsniveau**  
  CSP: [CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Configureer hoe strikt Defender Antivirus te werk gaat bij het blokkeren en scannen van verdachte bestanden.
  - **Niet geconfigureerd** (*standaard*): standaardblokkeringsniveau van Defender.
  - **Hoog**: onbekende bestanden wordt strikt geblokkeerd met optimalisatie van clientprestaties. Dit kan leiden tot meer onterechte positieven.
  - **Hoog plus**: onbekende bestanden wordt strikt geblokkeerd met toepassing van aanvullende beveiligingsmaatregelen die invloed kunnen hebben op clientprestaties.
  - **Zero tolerance**: alle onbekende uitvoerbare bestanden worden geblokkeerd.

- **Archiefbestanden scannen**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Ja** (*standaard*): het scannen van archiefbestanden zoals ZIP- en CAB-bestanden wordt afgedwongen.
  - **Niet geconfigureerd**: de instelling wordt teruggezet op de standaardwaarde van de client, namelijk het scannen van gearchiveerde bestanden. De gebruiker kan dit echter uitschakelen.

- **Gedragscontrole inschakelen**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Ja** (*standaard*): er wordt gedragsbewaking afgedwongen en de gebruiker kan dit niet uitschakelen.
  - **Niet-geconfigureerd**: de instelling krijgt weer de standaardwaarde van de client. Deze standaardwaarde is Ingeschakeld en de gebruiker kan dit niet wijzigen. Als u realtime bewaking wilt uitschakelen, gebruikt u een aangepaste URI.
  
- **Verwijderbare stations scannen tijdens een volledige scan**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Ja** (*standaard*): tijdens een volledige scan worden verwijderbare stations (bijvoorbeeld USB-sticks) gescand.
  - **Niet-geconfigureerd**: bij deze instelling wordt de standaardwaarde van de client teruggezet: hierbij worden verwijderbare stations gescand, maar de gebruiker kan het scannen uitschakelen.
  
- **Netwerkbestanden scannen**  
  CSP: [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Ja** (*standaard*): Microsoft Defender scant netwerkbestanden.
  - **Niet-geconfigureerd**: de client maakt gebruik van de standaardinstellingen, waarbij het scannen van netwerkbestanden wordt uitgeschakeld.
  
- **Defender: mogelijk ongewenste app-actie**  
  CSP: [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Geef het detectieniveau op voor mogelijk ongewenste toepassingen (PUA's). Defender waarschuwt gebruikers wanneer mogelijk ongewenste software wordt gedownload of op een apparaat wordt geïnstalleerd.
  - **Standaardwaarde apparaat**
  - **Blokkeren** (*standaard*): gedetecteerde items worden geblokkeerd en worden samen met andere bedreigingen in de geschiedenis weergegeven.
  - **Controle**: Microsoft Defender detecteert mogelijk ongewenste toepassingen, maar neemt geen verdere acties. U kunt informatie nalezen over de toepassingen waartegen Windows Defender actie zou hebben ondernomen, door te zoeken naar gebeurtenissen die door Windows Defender in Logboeken zijn gemaakt.

- **Cloudbeveiliging inschakelen**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  Standaard stuurt Defender op desktopapparaten met Windows 10 informatie naar Microsoft over eventuele gevonden problemen. Microsoft analyseert die gegevens om meer te weten te komen over problemen die u en andere klanten ondervinden, om verbeterde oplossingen te kunnen bieden.

  - **Ja** (*standaard*): cloudbeveiliging is ingeschakeld.  Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de systeemstandaard.

- **Voorkomen dat Office-toepassingen code in andere processen injecteren**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872974)

  Deze ASR-regel wordt beheerd via de volgende GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Blokkeren** (*standaard*): Office-toepassingen mogen geen code in andere processen injecteren.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat Office-toepassingen uitvoerbare inhoud maken**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872975)

  Deze ASR-regel wordt beheerd via de volgende GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Blokkeren** (*standaard*): Office-toepassingen mogen geen uitvoerbare inhoud maken.
  - **Controlemodus** : er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.
  
- **Voorkomen dat JavaScript of VBScript gedownloade uitvoerbare inhoud start**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872979)

   Deze ASR-regel wordt beheerd via de volgende GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Blokkeren** (*standaard*): Defender blokkeert het uitvoeren van JavaScript- en VBScript-bestanden die van internet zijn gedownload.
  - **Controlemodus** : er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.
  
- **Netwerkbeveiliging inschakelen**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen**: netwerkbeveiliging wordt ingeschakeld voor alle gebruikers in het systeem.
  - **Controlemodus** (*standaard*): gebruikers worden niet geweerd uit gevaarlijke domeinen; in plaats daarvan worden er Windows-gebeurtenissen geregistreerd.

- **Voorkomen dat niet-vertrouwde en niet-ondertekende processen kunnen worden uitgevoerd vanaf een USB**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874502)

  Deze ASR-regel wordt beheerd via de volgende GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Blokkeren** (*standaard*): niet-vertrouwde en niet-ondertekende processen die worden uitgevoerd vanaf een USB-stick worden geblokkeerd.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Blokkeer referentiediefstal in het Windows-subsysteem voor de lokale beveiligingsautoriteit (lsass.exe)**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=874499)

  Deze ASR-regel wordt beheerd via de volgende GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Door de gebruiker gedefinieerd**
  - **Inschakelen** (*standaard*): alle pogingen om referenties te stelen via lsass.exe worden geblokkeerd.
  - **Controlemodus**: gebruikers worden niet geweerd uit gevaarlijke domeinen; in plaats daarvan worden er Windows-gebeurtenissen geregistreerd.

- **Downloaden van uitvoerbare inhoud via e-mail- en webmailclients blokkeren**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Blokkeren** (*standaard*): het downloaden van uitvoerbare inhoud uit e-mail- en webmailclients wordt geblokkeerd.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Voorkomen dat Office-toepassingen onderliggende processen maken**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872976)

  Deze ASR-regel wordt beheerd via de volgende GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Blokkeren** (*standaard*)
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Uitvoering van mogelijk verborgen scripts (js/vbs/ps) voorkomen**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872978)

  Deze ASR-regel wordt beheerd via de volgende GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Blokkeren** (*standaard*): Defender blokkeert de uitvoering van verborgen scripts.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

- **Win32 API-aanroepen blokkeren vanuit Office-macro's**  
  [Apparaten beveiligen tegen misbruik](https://go.microsoft.com/fwlink/?linkid=872977)

  Deze ASR-regel wordt beheerd via de volgende GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Niet-geconfigureerd**: de instelling wordt teruggezet op de Windows-standaardwaarde: Uitgeschakeld.
  - **Blokkeren** (*standaard*): Office-macro's mogen niet gebruikmaken van Win32 API-aanroepen.
  - **Controlemodus**: er treden Windows-gebeurtenissen op in plaats van dat deze worden geblokkeerd.

## <a name="microsoft-defender-security-center"></a>Microsoft Defender-beveiligingscentrum

- **Blokkeren dat gebruikers de beveiligingsinterface van Exploit Guard kunnen bewerken**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Ja** (*standaard*): hiermee voorkomt u dat gebruikers wijzigingen aanbrengen in de Exploit Protection-instellingen in het Microsoft Defender-beveiligingscentrum.
  - **Niet-geconfigureerd**: lokale gebruikers mogen geen wijzigingen aanbrengen in het instellingengebied voor Exploit Protection.

## <a name="smart-screen"></a>SmartScreen

- **Blokkeren dat gebruikers SmartScreen-waarschuwingen kunnen negeren**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   Voor deze instelling moet de instelling SmartScreen afdwingen voor apps en bestanden worden ingeschakeld.
  - **Ja** (*standaard*): er wordt in SmartScreen geen optie weergegeven voor de gebruiker om de waarschuwing te negeren en de app uit te voeren. De waarschuwing wordt weergegeven, maar de gebruiker kan deze omzeilen.
  - **Niet-geconfigureerd**: hiermee wordt de Windows-standaardinstelling teruggezet, waardoor de gebruiker kan overschrijven.

- **Alleen apps uit store vereisen**  

  - **Ja** (*standaard*)
  - **Niet geconfigureerd**

- **Windows SmartScreen inschakelen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Ja** (*standaard*): het gebruik van SmartScreen afdwingen voor alle gebruikers.
  - **Niet-geconfigureerd**: hiermee wordt de standaardinstelling van Windows teruggezet. Dit betekent dat SmartScreen wordt ingeschakeld, maar gebruikers kunnen deze instelling indien gewenst wijzigen. Als u SmartScreen wilt uitschakelen, gebruikt u een aangepaste URI.

## <a name="windows-hello-for-business"></a>Windows Hello voor Bedrijven

Raadpleeg [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) in de Windows-documentatie voor meer informatie.

- **Windows Hello voor Bedrijven blokkeren**  

   Windows Hello voor Bedrijven is een alternatieve aanmeldmethode voor Windows die wachtwoorden, smartcards en virtuele smartcards vervangt.

  - **Niet-geconfigureerd**: op apparaten wordt Windows Hello voor Bedrijven ingericht; dit is de standaardinstelling van Windows.
  - **Uitgeschakeld** (*standaard*): op apparaten wordt Windows Hello voor Bedrijven ingericht.
  - **Ingeschakeld**: op apparaten wordt Windows Hello voor Bedrijven ingericht voor alle gebruikers.

  Als de optie wordt ingesteld op *Uitgeschakeld*, kunt u de volgende instellingen configureren:

  - **Kleine letters in pincode**  
    - **Niet toegestaan**
    - **Vereist**
    - **Toegestaan** (*standaard*)

  - **Speciale tekens in pincode**
    - **Niet toegestaan**
    - **Vereist**
    - **Toegestaan** (*standaard*)

  - **Hoofdletters in pincode**
    - **Niet toegestaan**
    - **Vereist**
    - **Toegestaan** (*standaard*)

::: zone-end

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over beveiligingsbasislijnen](security-baselines.md)
- [Conflicten voorkomen](security-baselines.md#avoid-conflicts)
- [Beleidsregels en profielen voor het oplossen van problemen in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)