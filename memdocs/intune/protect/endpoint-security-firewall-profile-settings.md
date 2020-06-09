---
title: Firewallinstellingen voor Intune-eindpuntbeveiliging | Microsoft Docs
description: Firewallbeleidsinstellingen voor eindpuntbeveiliging voor Windows en macOS in Microsoft Intune
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
ms.openlocfilehash: d90870a60ea292939926816bb74b5d285dc6a09f
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431602"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Instellingen van firewallbeleid voor eindpuntbeveiliging in Intune

Bekijk de instellingen die u kunt configureren in profielen voor beleid voor *Firewall* in het knooppunt voor eindpuntbeveiliging van Intune als onderdeel van een [eindpuntbeveiligingsbeleid](../protect/endpoint-security-policy.md).

Ondersteunde platforms en profielen:

- **macOS**:
  - Profiel: **macOS-firewall**

- **Windows 10 en hoger**:
  - Profiel: **Microsoft Defender Firewall**

## <a name="macos-firewall-profile"></a>Profiel macOs-firewall

### <a name="firewall"></a>Firewall

De volgende instellingen zijn geconfigureerd als [eindpointbeveiligingsbeleid voor macOS-firewalls](../protect/endpoint-security-firewall-policy.md)

- **Firewall inschakelen**

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: Schakel de firewall in.
  
  Als de optie is ingesteld op *Ja*, kunt u de volgende instellingen configureren.  

  - **Alle binnenkomende verbindingen blokkeren**

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: blokkeer alle binnenkomende verbindingen, behalve de verbindingen die vereist zijn voor basisinternetservices, zoals DHCP, Bonjour en IPSec. Dit blokkeert ook alle services voor delen.

  - **Verborgen modus inschakelen**

    - **Niet geconfigureerd** (*standaard*)
    - **Ja**: schakel deze optie in om te voorkomen dat de computer reageert op peilverzoeken. De computer reageert nog wel op binnenkomende verzoeken voor toegestane apps.

  - **Firewall-apps** Vouw de vervolg keuzelijst uit en selecteer vervolgens **Toevoegen** om vervolgens apps en regels voor binnenkomende verbindingen voor de app op te geven.
    - **Binnenkomende verbindingen toestaan**
      - Niet geconfigureerd
      - Blokkeren
      - Toestaan

    - **Bundel-id**: de id identificeert de app. Bijvoorbeeld: *com.apple.app*

## <a name="microsoft-defender-firewall-profile"></a>Microsoft Defender Firewall-profiel

### <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall

De volgende instellingen zijn geconfigureerd als [eindpointbeveiligingsbeleid voor Windows 10-firewalls](../protect/endpoint-security-firewall-policy.md).

- **Stateful File Transfer Protocol (FTP) blokkeren**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **Niet geconfigureerd** (*default*): de firewall maakt gebruik van een FTP om secundaire netwerkverbindingen te controleren en te filteren, waardoor uw firewallregels mogelijk worden genegeerd.
  - **Ja**
  
- **Aantal seconden dat een beveiligingskoppeling inactief kan zijn voordat deze wordt verwijderd**  
  CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Geef tussen de 300 en 3600 seconden op hoe lang de beveiligingskoppelingen worden bewaard als er geen sprake is van netwerkverkeer.
  
  Als u geen waarde opgeeft, verwijdert het systeem een beveiligingskoppeling nadat deze gedurende 300 seconden inactief is geweest.
  
- **Codering van vooraf-gedeelde sleutels**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  Als u geen *UTF*-8 vereist, worden vooraf gedeelde sleutels in eerste instantie versleuteld met UTF-8. Daarna kunnen gebruikers van het apparaat een andere versleutelingsmethode kiezen.

  - **Niet geconfigureerd** (*standaard*)
  - **Geen**
  - **UTF8**

- **IPSec-uitzonderingen voor firewall: neighbordetectie toestaan**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: IPSec-uitzonderingen voor firewall: neighbordetectie toestaan.

- **IPSec-uitzonderingen voor firewall: ICMP toestaan**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: IPSec-uitzonderingen voor firewall: ICMP toestaan.

- **IPSec-uitzonderingen voor firewall: routerdetectie toestaan**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: IPSec-uitzonderingen voor firewall: routerdetectie toestaan.

- **IPSec-uitzonderingen voor firewall: DHCP toestaan**  
  CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja** - IPSec-uitzonderingen voor firewall: DHCP toestaan

- **Verificatie van certificaatintrekkingslijst (CRL)**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   Geef aan hoe de controle van certificaatintrekkingslijsten (CRL's) wordt afgedwongen.
  - **Niet geconfigureerd** (*standaard*): de standaardinstelling is dat de client de CRL-verificatie uitschakelt.
  - **Geen**
  - **Poging**
  - **Vereisen**

- **Vereisen dat sleutelmodules alleen de verificatiesuites negeren die niet door die modules worden ondersteund**  
  CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **Niet geconfigureerd** (*standaard*)
  - **Ja**: sleutelmodules negeren niet-ondersteunde verificatiesuites.

- **Pakketten in wachtrij plaatsen**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Hiermee kunt u opgeven hoe schalen voor software aan de ontvangstzijde wordt ingeschakeld voor versleuteld ontvangen en ongecodeerd doorsturen in het scenario voor de IPsec-tunnelgateway. Hierdoor wordt gegarandeerd dat de pakketvolgorde behouden blijft.
  - **Niet-geconfigureerd** (*standaard*): voor het in de wachtrij plaatsen van pakketten wordt de standaardinstelling van de client gebruikt. Deze is uitgeschakeld.
  - **Uitgeschakeld**
  - **Inkomende wachtrij**
  - **Uitgaande wachtrij**
  - **Beide wachtrijen**

- **Microsoft Defender Firewall inschakelen voor domeinnetwerken**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Niet geconfigureerd** (*standaard*): de client keert terug naar de standaardinstelling om de firewall in te schakelen.
  - **Ja**: de Microsoft Defender Firewall voor het netwerktype van **domein** is ingeschakeld en afgedwongen.
  - **Ja**: schakel de firewall uit.

- **Microsoft Defender Firewall inschakelen voor particuliere netwerken**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Niet geconfigureerd** (*standaard*): de client keert terug naar de standaardinstelling om de firewall in te schakelen.
  - **Ja**: de Microsoft Defender Firewall voor het netwerktype van **privé** is ingeschakeld en afgedwongen.
  - **Ja**: schakel de firewall uit.

- **Microsoft Defender Firewall inschakelen voor openbare netwerken**  
  CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Niet geconfigureerd** (*standaard*): de client keert terug naar de standaardinstelling om de firewall in te schakelen.
  - **Ja**: de Microsoft Defender Firewall voor het netwerktype van **privé** is ingeschakeld en afgedwongen.
  - **Ja**: schakel de firewall uit.

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Microsoft Defender Firewall-regels

*Dit profiel is beschikbaar als Preview*.

De volgende instellingen zijn geconfigureerd als [eindpointbeveiligingsbeleid voor Windows 10-firewalls](../protect/endpoint-security-firewall-policy.md).

#### <a name="windows-firewall-rule"></a>Regel van Windows Firewall

- **Naam**  
  Geef een beschrijvende naam voor uw regel op. Deze naam wordt weergegeven in de lijst met regels, met behulp waarvan u dit kunt identificeren.

- **Beschrijving**  
  Geef een beschrijving van de regel op.

- **Richting**  
  - **Niet geconfigureerd** (*standaard*): deze regel wordt standaard ingesteld op uitgaand verkeer.
  - **Out**: deze regel is van toepassing op uitgaand verkeer.
  - **In**: deze regel is van toepassing op binnenkomend verkeer.

- **Actie**  
  - **Niet geconfigureerd** (*standaard*): Deze regel staat standaard verkeer toe.
  - **Geblokkeerd**: het verkeer wordt geblokkeerd in de *Richting* die u hebt geconfigureerd.
  - **Toegestaan**: verkeer is toegestaan in de *Richting* u hebt geconfigureerd.

- **Netwerktype**  
  Geef het netwerktype op waarvan de regel deel uitmaakt. U kunt uit een van de volgende kiezen. Als u geen optie selecteert, is de regel van toepassing op alle netwerktypen.
  - **Domein**
  - **Privé**
  - **Openbaar**
  - **Niet geconfigureerd**

- **Familienaam van het pakket**  
  [Get-AppxPackage](https://docs.microsoft.com/previous-versions//hh856044(v=technet.10))

  Familienamen van pakketten kunnen worden opgehaald met de opdracht Get-AppxPackage van PowerShell.

- **Pad naar bestand**  
  CSP: [FirewallRules/FirewallRuleName/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)

  Als u het bestandspad van een app wilt opgeven, voert u de locatie van de apps in op het clientapparaat. Bijvoorbeeld: `C:\Windows\System\Notepad.exe` of `%WINDIR%\Notepad.exe`

- **Servicenaam**  
  [FirewallRules/FirewallRuleName/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)

  Een korte naam van een Windows-service gebruiken wanneer een service, niet een toepassing, verkeer verzendt of ontvangt. Korte namen van services worden opgehaald door de `Get-Service` opdracht uit te voeren vanuit PowerShell.

- **Protocol**  
  CSP: [FirewallRules/FirewallRuleName/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)

  Geef het protocol voor deze poortregel op.
  - Met transportlaag-protocollen zoals *TCP (6)* en *UDP (17)* kunt u poorten of poortbereiken opgeven.
  - Voer voor aangepaste protocollen een getal in tussen *0* en *255* dat het IP-protocol vertegenwoordigt.
  - Als er niets is opgegeven, wordt de regel standaard ingesteld op het **willekeurig**.

- **Interfacetypen**  
  Geef het interfacetype op waarvan de regel deel uitmaakt. U kunt uit een van de volgende kiezen. Als u geen optie selecteert, is de regel van toepassing op alle interfacetypen:
  - **Externe toegang**
  - **Draadloos**
  - **Lokaal netwerk**
  - **Niet geconfigureerd**

- **Geautoriseerde gebruikers**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  Geef een lijst met geautoriseerde lokale gebruikers voor deze regel op. Als de *Service-naam* is ingesteld als een Windows-service, kan geen lijst met geautoriseerde gebruikers worden opgegeven. Als er geen gemachtigde gebruiker is opgegeven, wordt de standaardwaarde *Alle gebruikers*.

- **Elk lokaal adres**  
  **Niet geconfigureerd** (*standaard*): gebruik de volgende instelling, *Lokale adresbereiken** om een reeks adressen te configureren die moeten worden ondersteund.
  - **Ja**: een lokaal adres ondersteunen en geen adresbereik configureren.

- **Lokale adresbereiken**  
  CSP: [FirewallRules/FirewallRuleName/LocalAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localaddressranges)  

  Voeg een of meer adressen toe als een lijst met door komma's gescheiden lokale adressen waarop de regel van toepassing is. Geldige invoergegevens (tokens) zijn onder andere de volgende opties:
  - **Een asterisk**: een asterisk (\*) geeft een lokaal adres aan. Als dit het geval is, moet de asterisk het enige token zijn dat is opgenomen.
  - **Een subnet**: Om een subnet op te geven, gebruikt u een subnetmasker of een netwerkvoorvoegselnotatie. Als er geen subnetmasker en ook geen netwerkvoorvoegsel wordt opgegeven, wordt de standaardinstelling 255.255.255.255 voor het subnetmasker gebruikt.
  - **Een geldig IPv6-adres**
  - **Een IPv4-adres bereik**: IPv4-bereiken moeten de indeling hebben van *beginadres-eindadres* en geen spaties bevatten, waarbij het beginadres kleiner is dan het eindadres.
  - **Een IPv6-adres bereik**: IPv6-bereiken moeten de indeling hebben van *beginadres-eindadres* en geen spaties bevatten, waarbij het beginadres kleiner is dan het eindadres.

  Als er geen waarde is opgegeven, wordt de standaardinstelling *Elk adres*.

- **Elk extern adres**  
  **Niet geconfigureerd** (*standaard*): gebruik de volgende instelling, *Externe adresbereiken** om een reeks adressen te configureren die moeten worden ondersteund.
  - **Ja**: een extern adres ondersteunen en geen adresbereik configureren.

- **Externe adresbereiken**  
  CSP: [FirewallRules/FirewallRuleName/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  Voeg een of meer adressen toe als een lijst met door komma's gescheiden externe adressen waarop de regel van toepassing is. Geldige invoergegevens (tokens) zijn onder andere de volgende opties en zijn niet hoofdlettergevoelig:
  - **Een asterisk**: een asterisk (\*) geeft een extern adres aan. Als dit het geval is, moet de asterisk het enige token zijn dat is opgenomen.
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet**: Ondersteund op apparaten met Windows 1809 of hoger.
  - **RmtIntranet**: ondersteund op apparaten met Windows 1809 of hoger.
  - **Ply2Renders**: Ondersteund op apparaten met Windows 1809 of hoger.
  - **LocalSubnet** - Geeft elk willekeurige lokale adres in het lokale subnet aan.
  - **Een subnet**: Om een subnet op te geven, gebruikt u een subnetmasker of een netwerkvoorvoegselnotatie. Als er geen subnetmasker en ook geen netwerkvoorvoegsel wordt opgegeven, wordt de standaardinstelling 255.255.255.255 voor het subnetmasker gebruikt.
  - **Een geldig IPv6-adres**
  - **Een IPv4-adres bereik**: IPv4-bereiken moeten de indeling hebben van *beginadres-eindadres* en geen spaties bevatten, waarbij het beginadres kleiner is dan het eindadres.
  - **Een IPv6-adres bereik**: IPv6-bereiken moeten de indeling hebben van *beginadres-eindadres* en geen spaties bevatten, waarbij het beginadres kleiner is dan het eindadres.

  Als er geen waarde is opgegeven, wordt de standaardinstelling *Elk adres*.

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>Volgende stappen

[Instellingen voor eindpuntbeveiliging voor firewalls](../protect/endpoint-security-firewall-policy.md)
