---
title: Beveiligingsinstellingen voor Windows 10-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Op Windows 10-apparaten kunt u instellingen voor eindpuntbescherming gebruiken of configureren om functies van Microsoft Defender in te schakelen, zoals Application Guard, Firewall, SmartScreen, versleuteling en Bitlocker, Exploit Guard, Application Control, Security Center en beveiliging van lokale apparaten in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 3af7c91b-8292-4c7e-8d25-8834fcf3517a
ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7817a747a01a137fd29ee8aae117cd604da233a5
ms.sourcegitcommit: 4815f07c8c0399c077b71721c6e6b61047c75ae6
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/17/2020
ms.locfileid: "79437098"
---
# <a name="windows-10-and-later-settings-to-protect-devices-using-intune"></a>Instellingen voor Windows 10 (en hoger) om apparaten te beveiligen met Intune

Microsoft Intune bevat veel instellingen om uw apparaten te beveiligen. In dit artikel worden alle instellingen beschreven die u kunt inschakelen en configureren op apparaten met Windows 10 en hoger. Deze instellingen zijn gemaakt in een configuratieprofiel voor eindpuntbeveiliging in Intune om beveiligingsfuncties te beheren, zoals BitLocker en Microsoft Defender.  

Zie [Apparaatbeperkingsinstellingen voor Windows 10](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) als u Microsoft Defender Antivirus wilt configureren.  

## <a name="before-you-begin"></a>Voordat u begint  

[Maak een configuratieprofiel voor eindpuntbeveiliging op een apparaat](endpoint-protection-configure.md).  

Zie de [referentie van de configuratie-serviceprovider](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference) voor meer informatie over configuratie-serviceproviders (CSP's).  

## <a name="microsoft-defender-application-guard"></a>Microsoft Defender Application Guard  

Wanneer u Microsoft Edge gebruikt, beschermt Microsoft Defender Application Guard uw omgeving tegen sites die niet worden vertrouwd door uw organisatie. Als gebruikers sites bezoeken die niet worden vermeld in uw geïsoleerde netwerkgrens, worden deze sites geopend in een virtuele browsersessie in Hyper-V. Vertrouwde sites worden gedefinieerd door een netwerkgrens, die in Apparaatconfiguratie wordt geconfigureerd.  

Application Guard is alleen beschikbaar voor apparaten met de 64 bitsversie van Windows 10. Met dit profiel wordt een Win32-onderdeel geïnstalleerd om Application Guard te activeren.  

- **Application Guard**  
  **Standaardinstelling**: Niet geconfigureerd  
   Application Guard-CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)  

  - **Ingeschakeld voor Edge**: hiermee wordt deze functie ingeschakeld en worden niet-vertrouwde sites geopend in een met Hyper-V gevirtualiseerde browsercontainer.  
  - **Niet geconfigureerd**: op het apparaat kan elke site (vertrouwd en niet-vertrouwd) worden geopend.  

- **Klembordgedrag**  
  **Standaardinstelling**: Niet geconfigureerd  
   Application Guard-CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)  

  Kies welke kopieer- en plakbewerkingen zijn toegestaan tussen de lokale pc en de virtuele browser van Application Guard.  
  - **Niet geconfigureerd**  
  - **Alleen kopiëren en plakken van de pc naar de browser toestaan**  
  - **Alleen kopiëren en plakken van de browser naar de pc toestaan**  
  - **Kopiëren en plakken tussen de pc en de browser toestaan**  
  - **Kopiëren en plakken tussen de pc en de browser blokkeren**  

- **Inhoud van het Klembord**  
  Deze instelling is alleen beschikbaar wanneer *Gedrag van het Klembord* is ingesteld op een van de instellingen voor *Toestaan*.  
  **Standaardinstelling**: Niet geconfigureerd  
  Application Guard-CSP: [Settings/ClipboardFileType](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardfiletype)  

  De toegestane inhoud van het Klembord selecteren.  
  - **Niet geconfigureerd**  
  - **Tekst**  
  - **Afbeeldingen**  
  - **Tekst en afbeeldingen**  

- **Externe inhoud op bedrijfssites**  
  **Standaardinstelling**: Niet geconfigureerd  
  Application Guard-CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)  

  - **Blokkeren**: inhoud van niet-goedgekeurde websites blokkeren, zodat deze niet kan worden geladen.  
  - **Niet geconfigureerd**: niet-bedrijfssites kunnen op het apparaat worden geopend.  
 
- **Afdrukken vanuit virtuele browser**  
  **Standaardinstelling**: Niet geconfigureerd  
  Application Guard-CSP: [Settings/PrintingSettings](https://go.microsoft.com/fwlink/?linkid=872354)  

  - **Toestaan**: hiermee staat u toe dat de geselecteerde inhoud vanuit de virtuele browser kan worden afgedrukt.  
  - **Niet geconfigureerd**: hiermee schakelt u alle afdrukfuncties uit.  

  Wanneer u afdrukken *toestaat*, kunt u de volgende instelling configureren:
  - **Afdruktype(n)** : selecteer een of meer van de volgende opties:  
    - PDF  
    - XPS  
    - Lokale printers
    - Netwerkprinters  

- **Logboeken verzamelen**  
  **Standaardinstelling**: Niet geconfigureerd  
  Application Guard-CSP: [Audit/AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)  

  - **Toestaan**: logboeken verzamelen voor gebeurtenissen die zich voordoen in een Application Guard-browsersessie.  
  - **Niet geconfigureerd**: geen logboeken verzamelen binnen de browsersessie.  

- **Door de gebruiker gegenereerde browsergegevens behouden**  
  **Standaardinstelling**: Niet geconfigureerd  
  Application Guard-CSP: [Settings/AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)  

  - **Toestaan**: gebruikersgegevens (zoals wachtwoorden, favorieten en cookies) opslaan die worden gemaakt tijdens een virtuele browsersessie met Application Guard.  
  - **Niet geconfigureerd**: door de gebruiker gedownloade bestanden en gegevens verwijderen wanneer het apparaat opnieuw wordt opgestart of wanneer een gebruiker zich afmeldt.  

- **Grafische versnelling**  
 **Standaardinstelling**: Niet geconfigureerd  
  Application Guard-CSP: [Settings/AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)  
      
  - **Inschakelen**: grafisch-intensieve websites en video's worden sneller geladen door toegang tot een virtuele grafische verwerkingseenheid.  
  - **Niet geconfigureerd**: hiermee wordt de CPU van het apparaat gebruikt voor grafische weergave; gebruik de virtuele grafische verwerkingseenheid niet.  

- **Bestanden downloaden naar hostbestandssysteem**  
  **Standaardinstelling**: Niet geconfigureerd  
  Application Guard-CSP: [Settings/SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)  

  - **Inschakelen**: gebruikers kunnen bestanden vanuit de gevirtualiseerde browser downloaden naar het hostbesturingssysteem.  
  - **Niet geconfigureerd**: hiermee houdt u de bestanden lokaal op het apparaat en downloadt u bestanden niet naar het hostbestandssysteem.  

## <a name="microsoft-defender-firewall"></a>Microsoft Defender Firewall  
 
### <a name="global-settings"></a>Globale instellingen  

Deze instellingen gelden voor alle netwerktypen.  

- **File Transfer Protocol**  
  **Standaardinstelling**: Niet geconfigureerd  
   Firewall-CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Blokkeren**: stateful FTP uitschakelen.  
  - **Niet geconfigureerd**: de firewall past stateful FTP-filtering toe om secundaire verbindingen toe te staan.  

- **Niet-actieve tijd voordat beveiligingskoppeling wordt verwijderd**  
  **Standaardinstelling**: *Niet geconfigureerd*  
   Firewall-CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)  

   Geef een inactieve tijd in seconden op waarna de beveiligingskoppelingen worden verwijderd.   

- **Vooraf gedeelde sleutels coderen**  
  **Standaardinstelling**: Niet geconfigureerd  
   Firewall-CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)  

   - **Inschakelen**: codeer vooraf gedeelde sleutels met UTF-8.  
   - **Niet geconfigureerd**: codeer vooraf gedeelde sleutels met behulp van de lokale archiefwaarde.  

- **IPsec-uitzonderingen**  
  **Standaardinstelling**: *0 geselecteerd*  
   Firewall-CSP: [MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

   Selecteer een of meer van de volgende verkeerstypen die u van IPsec wilt uitzonderen:  
   - **ICMP-type-codes voor IPv6 detecteren met neighbor**  
   - **ICMP**  
   - **ICMP-type-codes voor IPv6 detecteren met router**  
   - **Zowel IPv4 als IPv6 DHCP-netwerkverkeer**  

- **Controle van certificaatintrekkingslijsten**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)  

  Bepaal hoe het apparaat certificaatintrekkingslijsten controleert. Opties zijn onder andere:  
  - **CRL-controle uitschakelen**  
  - **CRL-verificatie mislukt alleen bij alleen ingetrokken certificaat**  
  - **CRL-verificatie mislukt bij elke fout die wordt aangetroffen**.  
 

- **Verificatieset opportunistisch afstemmen per sleutelmodule**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)  
  
  - **Inschakelen**: sleutelmodules moeten alleen de verificatiepakketten negeren die ze niet ondersteunen.  
  - **Niet geconfigureerd**: sleutelmodules moeten de volledige verificatieset negeren als ze niet alle verificatiepakketten ondersteunen die zijn opgegeven in de set.  


- **Pakketten in wachtrij plaatsen**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)  

  Geef aan hoe schalen voor software aan de ontvangstzijde wordt ingeschakeld voor versleuteld ontvangen en ongecodeerd doorsturen in het scenario met de IPsec-tunnelgateway. Deze instelling garandeert dat de pakketvolgorde behouden blijft. Opties zijn onder andere:  
  - **Niet geconfigureerd**  
  - **In wachtrij plaatsen uitschakelen voor alle pakketten**  
  - **Alleen binnenkomende versleutelde pakketten in wachtrij plaatsen**  
  - **Pakketten in wachtrij plaatsen na ontsleutelen alleen uitvoeren bij doorsturen**  
  - **Binnenkomende en uitgaande pakketten configureren**  

### <a name="network-settings"></a>Netwerkinstellingen  

De volgende instellingen worden in dit artikel elk één keer genoemd, maar zijn allemaal van toepassing op de drie specifieke netwerktypen:  
- **Domeinnetwerk (werkplek)**  
- **Particulier netwerk (detecteerbaar)**  
- **Openbaar netwerk (niet-detecteerbaar)**  

#### <a name="general-settings"></a>Algemene instellingen  

- **Microsoft Defender Firewall**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)  
  
  - **Inschakelen**: de firewall en geavanceerde beveiliging inschakelen. 
  - **Niet geconfigureerd**: hiermee staat u al het netwerkverkeer toe, ongeacht andere beleidsinstellingen.  

- **Verborgen modus**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)  
  - **Niet geconfigureerd**  
  - **Blokkeren**: hiermee blokkeert u de firewall in de verborgen modus. Als u de verborgen modus blokkeert, blokkeert u ook **Uitsluiting van beveiligd IPsec-pakket**.  
  - **Toestaan**: de firewall werkt in verborgen modus, waarmee reacties op probing-aanvragen worden verhinderd.  

- **Vrijstelling van met IPsec beveiligd pakket met afgeschermde modus**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [DisableStealthModeIpsecSecuredPacketExemption](https://go.microsoft.com/fwlink/?linkid=872560)  

  Deze optie wordt genegeerd als *Verborgen modus* is ingesteld op *Blokkeren*.  

  - **Niet geconfigureerd**  
  - **Blokkeren**: pakketten die met IPsec zijn beveiligd, ontvangen geen uitzonderingen.  
  - **Toestaan**: hiermee kunt u uitzonderingen inschakelen. De afgeschermde modus van de firewall MAG NIET voorkomen dat de hostcomputer reageert op ongewenst netwerkverkeer dat met IPsec wordt beveiligd.  

- **Afgeschermd**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [Afgeschermd](https://go.microsoft.com/fwlink/?linkid=872561)  
    - **Niet geconfigureerd**  
    - **Blokkeren**: wanneer Windows Defender Firewall is ingeschakeld en deze instelling op *Blokkeren* is ingesteld, wordt al het binnenkomende verkeer geblokkeerd, ongeacht andere beleidsinstellingen. 
    - **Toestaan**: wanneer *Toestaan* is ingesteld, wordt deze instelling uitgeschakeld en wordt binnenkomend verkeer toegestaan op basis van andere beleidsinstellingen.

- **Unicast-antwoorden voor multicast-broadcasts**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)  
  
  Normaal gesproken wilt u geen unicast-antwoorden voor multicast-broadcasts ontvangen. Deze antwoorden kunnen wijzen op een DOS-aanval (denial of service) of een aanvaller die een computer wil binnendringen.  
  - **Niet geconfigureerd**  
  - **Blokkeren**:  unicast-antwoorden voor multicast-broadcasts uitschakelen.  
  - **Toestaan**: unicast-antwoorden voor multicast-broadcasts toestaan.  

- **Binnenkomende meldingen**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=8725630)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: meldingen aan gebruikers worden verborgen wanneer voor een toepassing het luisteren naar een poort wordt geblokkeerd.  
  - **Toestaan**: hiermee wordt deze instelling ingeschakeld en wordt er mogelijk een melding weergeven aan gebruikers wanneer een app wordt geblokkeerd en niet op een poort mag luisteren.  

- **De standaardactie voor uitgaande verbindingen**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)  
  
  Configureer de standaardactie die met de firewall wordt uitgevoerd voor uitgaande verbindingen. Deze instelling wordt toegepast op Windows versie 1809 en hoger.  

  - **Niet geconfigureerd**  
  - **Blokkeren**: de standaardfirewallactie wordt niet uitgevoerd op uitgaand verkeer, tenzij expliciet wordt opgegeven dat de actie niet moet worden geblokkeerd.  
  - **Toestaan**: hiermee worden standaardfirewallacties uitgevoerd op uitgaande verbindingen.  

- **De standaardactie voor binnenkomende verbindingen**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)  
 
  - **Niet geconfigureerd**  
  - **Blokkeren**: de standaardfirewallactie wordt niet uitgevoerd op binnenkomende verbindingen.  
  - **Toestaan**: standaardfirewallacties worden uitgevoerd op binnenkomende verbindingen.  

#### <a name="rule-merging"></a>Regel samenvoegen  

- **Defender Firewall-regels uit het lokale archief voor de gemachtigde toepassing**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: de firewallregels van de gemachtigde toepassing in het lokale archief worden genegeerd en worden niet afgedwongen.  
  - **Toestaan**: -
   kies **Inschakelen** om firewallregels in het lokale archief toe te passen zodat deze worden herkend en afgedwongen.  

- **Algemene poortfirewallregels van Microsoft Defender uit het lokale archief**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: de firewallregels van de globale poort in het lokale archief worden genegeerd en niet afgedwongen.  
  - **Inschakelen**: algemene poortfirewallregels in het lokale archief toepassen om te herkennen en af te dwingen.  

- **Firewallregels van Microsoft Defender uit het lokale archief**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: hiermee worden de firewallregels van het lokale archief genegeerd en niet afgedwongen.
  - **Inschakelen**: firewallregels in het lokale archief toepassen om te herkennen en af te dwingen.  

- **IPsec-regels vanuit het lokale archief**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: de beveiligingsregels voor verbindingen vanuit het lokale archief worden genegeerd en niet afgedwongen, ongeacht de versie van het schema en de versie van de beveiligingsregel van de verbinding.  
  - **Toestaan**: beveiligingsregels voor verbindingen toepassen vanuit het lokale archief, ongeacht het schema of de versies van de beveiligingsregels voor verbindingen.  

### <a name="firewall-rules"></a>Firewallregels  

U kunt een van meer aangepaste firewallregels **toevoegen**. Zie [Aangepaste firewallregels toevoegen voor Windows 10-apparaten](endpoint-protection-configure.md#add-custom-firewall-rules-for-windows-10-devices) voor meer informatie.  

De volgende opties worden ondersteund door aangepaste firewallregels:  

#### <a name="general-settings"></a>Algemene instellingen:  

- **Naam**  
  **Standaardinstelling**: *Geen naam*  

  Geef een beschrijvende naam voor uw regel op. Deze naam wordt weergegeven in de lijst met regels, met behulp waarvan u dit kunt identificeren.  

- **Beschrijving**  
  **Standaardinstelling**: *Geen beschrijving*  

  Geef een beschrijving van de regel op.  

- **Richting**   
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/Direction](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#direction)  
  
  Geef aan of deze regel van toepassing is op **Binnenkomend** of **Uitgaand** verkeer. Wanneer **Niet geconfigureerd** is ingesteld, wordt de regel automatisch toegepast op uitgaand verkeer.  

- **Actie**  
  **Standaardinstelling**: Niet geconfigureerd  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/Action](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#action) en [FirewallRules/*FirewallRuleName*/Action/Type](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#type)  

  Selecteer **Toestaan** of **Blokkeren**. Wanneer **Niet geconfigureerd** is ingesteld, wordt de regel standaard toegepast op het toestaan van verkeer.  

- **Netwerktype**  
  **Standaardinstelling**: 0 geselecteerd  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/Profiles](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#profiles)  

  Selecteer maximaal drie netwerktypen waarop deze regel moet worden toegepast. De opties **Domein**, **Particulier** en **Openbaar** zijn beschikbaar.  Als er geen netwerktypen zijn geselecteerd, is de regel van toepassing op alle drie de netwerktypen.  

#### <a name="application-settings"></a>Toepassingsinstellingen  

- **Toepassing(en)**  
  **Standaardinstelling**: Alle  

  Beheer de verbindingen voor een app of een programma. Selecteer een van de volgende opties en voltooi daarna de aanvullende configuratie:  
  - **Naam van pakketreeks**: geef een naam op voor de pakketreeks. Gebruik de PowerShell-opdracht **Get-AppxPackage** om de naam van de pakketreeks te zoeken.   
    Firewall-CSP: [FirewallRules/*FirewallRuleName*/App/PackageFamilyName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#packagefamilyname)  
 
  - **Bestandspad**: u moet een bestandspad opgeven naar een app op het clientapparaat. Dit kan een absoluut of een relatief pad zijn. Bijvoorbeeld:  C:\Windows\System\Notepad.exe or %WINDIR%\Notepad.exe.  
    Firewall-CSP: [FirewallRules/*FirewallRuleName*/App/FilePath](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#filepath)  

  - **Windows-service**: geef de korte naam van de Windows-service op als het een service is en geen toepassing die verkeer verzendt of ontvangt. Gebruik de PowerShell-opdracht **Get-Service** om de korte naam van de service te zoeken.  
    Firewall-CSP: [FirewallRules/*FirewallRuleName*/App/ServiceName](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#servicename)  

  - **Alle**: *er is geen aanvullende configuratie beschikbaar*.  

#### <a name="ip-address-settings"></a>Instellingen voor IP-adres  

Geef de lokale en externe adressen op waarop deze regel van toepassing is.  

- **Lokale adressen**    
  **Standaardinstelling**: Willekeurig adres  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  

  Selecteer **Willekeurig adres** of **Opgegeven adres**.  

  Wanneer u *Opgegeven adres* gebruikt, voegt u een of meer adressen toe als een lijst met door komma's gescheiden lokale adressen waarop de regel van toepassing is. Geldige tokens zijn onder andere:  
  - Gebruik een sterretje * voor *willekeurige* lokale adressen. Als u een sterretje gebruikt, mag dit het enige token zijn dat u gebruikt.  
  - Als u een subnet wilt opgeven, gebruikt u een subnetmasker of een netwerkvoorvoegselnotatie. Als er geen subnetmasker en ook geen netwerkvoorvoegsel wordt opgegeven, wordt de standaardinstelling 255.255.255.255 voor het subnetmasker gebruikt.  
  - Een geldig IPv6-adres.  
  - Een IPv4-adresbereik met de indeling 'beginadres - eindadres', zonder spaties.  
  - Een IPv6-adresbereik met de indeling 'beginadres - eindadres', zonder spaties.  

- **Externe adressen**  
  **Standaardinstelling**: Willekeurig adres  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/RemoteAddressRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteaddressranges)  
 
  Selecteer **Willekeurig adres** of **Opgegeven adres**.  

  Wanneer u *Opgegeven adres* gebruikt, voegt u een of meer adressen toe als een lijst met door komma's gescheiden externe adressen waarop de regel van toepassing is. Tokens zijn niet hoofdlettergevoelig. Geldige tokens zijn onder andere:  
  - Gebruik een sterretje * voor *willekeurige* externe adressen. Als u een sterretje gebruikt, mag dit het enige token zijn dat u gebruikt.  
  - "Defaultgateway"  
  - "DHCP"  
  - "DNS"  
  - "WINS"  
  - Intranet (wordt ondersteund op Windows versie 1809 en hoger)  
  - RmtIntranet (wordt ondersteund op Windows versie 1809 en hoger)  
  - Internet (wordt ondersteund op Windows versie 1809 en hoger)  
  - Ply2Renders (wordt ondersteund op Windows versie 1809 en hoger)  
  - LocalSubnet geeft elk willekeurige lokale adres in het lokale subnet aan.  
  - Als u een subnet wilt opgeven, gebruikt u een subnetmasker of een netwerkvoorvoegselnotatie. Als er geen subnetmasker en ook geen netwerkvoorvoegsel wordt opgegeven, wordt de standaardinstelling 255.255.255.255 voor het subnetmasker gebruikt.  
  - Een geldig IPv6-adres.  
  - Een IPv4-adresbereik met de indeling 'beginadres - eindadres', zonder spaties.  
  - Een IPv6-adresbereik met de indeling 'beginadres - eindadres', zonder spaties.  

#### <a name="port-and-protocol-settings"></a>Poort- en protocolinstellingen  
Geef de lokale en externe poorten op waarop de regel van toepassing is.  

- **Protocol**  
  **Standaardinstelling**: Alle  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/Protocol](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#protocol)  
  Selecteer een van de volgende opties en voltooi de vereiste configuraties:  
  - **Alle**: er is geen aanvullende configuratie beschikbaar.  
  - **TCP**: lokale en externe poorten configureren. Alle poorten en Opgegeven poorten worden door beide opties ondersteund. Voer Opgegeven poorten in met behulp van een lijst met door komma's gescheiden items.  
    - **Lokale poorten**: firewall-CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Externe poorten**: firewall-CSP: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **UDP**: lokale en externe poorten configureren. Alle poorten en Opgegeven poorten worden door beide opties ondersteund. Voer Opgegeven poorten in met behulp van een lijst met door komma's gescheiden items.  
    - **Lokale poorten**: firewall-CSP: [FirewallRules/*FirewallRuleName*/LocalPortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#localportranges)  
    - **Externe poorten**: firewall-CSP: [FirewallRules/*FirewallRuleName*/RemotePortRanges](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#remoteportranges)  
  - **Aangepast**: geef een aangepast **protocolnummer** op tussen 0 en 255.  

#### <a name="advanced-configuration"></a>Geavanceerde configuratie  
- **Interfacetypen**  
  **Standaardinstelling**: 0 geselecteerd  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/InterfaceTypes](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp#interfacetypes)  

  Maak een keuze uit de volgende opties:  
  - **Externe toegang**  
  - **Draadloos**  
  - **Lokaal netwerk**  

- **Alleen verbindingen van deze gebruikers toestaan**  
  **Standaardinstelling**: Alle gebruikers *(als er geen lijst wordt opgegeven, wordt Alle gebruikers als standaard ingesteld)*  
  Firewall-CSP: [FirewallRules/*FirewallRuleName*/LocalUserAuthorizationList](https://aka.ms/intunefirewallauthorizedusers)  

  Geef een lijst met geautoriseerde lokale gebruikers voor deze regel op. Als deze regel op een Windows-service van toepassing is, kan geen lijst met geautoriseerde gebruikers worden opgegeven.  


## <a name="microsoft-defender-smartscreen-settings"></a>Instellingen voor Microsoft Defender SmartScreen  
 
Microsoft Edge moet op het apparaat zijn geïnstalleerd.  

- **SmartScreen voor apps en bestanden**  
  **Standaardinstelling**: Niet geconfigureerd  
   SmartScreen-CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)  

  - **Niet geconfigureerd**: hiermee schakelt u het gebruik van SmartScreen uit.  
  - **Inschakelen**: Windows SmartScreen inschakelen voor het uitvoeren van bestanden en apps. SmartScreen is een antiphishing- en antimalwareonderdeel in de cloud.  

- **Niet-geverifieerde bestandsuitvoering**  
  **Standaardinstelling**: Niet geconfigureerd  
   SmartScreen-CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **Niet geconfigureerd**: hiermee wordt deze functie uitgeschakeld, waardoor eindgebruikers bestanden kunnen uitvoeren die niet zijn geverifieerd.  
  - **Blokkeren**: voorkomen dat eindgebruikers bestanden uitvoeren die niet zijn geverifieerd door Windows SmartScreen.  

## <a name="windows-encryption"></a>Windows-versleuteling  
 
### <a name="windows-settings"></a>Windows-instellingen  

- **Apparaten versleutelen**  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)  

  - **Vereisen**: gebruikers vragen om apparaatversleuteling in te schakelen. Afhankelijk van de Windows-editie en de systeemconfiguratie, kunnen gebruikers:  
    - Worden gevraagd te bevestigen dat versleuteling van een andere provider niet is ingeschakeld.  
    - Worden verplicht BitLocker-stationsversleuteling uit te schakelen en vervolgens weer in te schakelen.  
  - **Niet geconfigureerd**  
  
  Als Windows-versleuteling is ingeschakeld terwijl een andere versleutelingsmethode actief is, wordt het apparaat mogelijk instabiel.  

- **Opslagkaart versleutelen (alleen mobiel)**  
  *Deze instelling geldt alleen voor Windows 10 Mobile.*  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)  

  - Selecteer **Vereisen** om ervoor te zorgen dat verwijderbare opslagkaarten die door het apparaat worden gebruikt, worden versleuteld.  
  - **Niet geconfigureerd**: geen versleuteling van de opslagkaart vereisen en de gebruiker niet vragen om dit in te schakelen.  

### <a name="bitlocker-base-settings"></a>Basisinstellingen voor BitLocker  

Basisinstellingen zijn universele BitLocker-instellingen voor alle soorten gegevensstations. Met deze instellingen wordt beheerd welke schijfversleutelingstaken of configuratieopties de eindgebruiker kan wijzigen op alle soorten gegevensstations.  

- **Waarschuwing voor andere schijfversleuteling**  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)  

  - **Blokkeren**: de waarschuwing uitschakelen als op het apparaat een andere service voor schijfversleuteling actief is.  
  - **Niet geconfigureerd**: toestaan dat de waarschuwing voor andere schijfversleuteling wordt weergegeven.  

  > [!TIP]  
  > Deze instelling moet zijn ingesteld op *Blokkeren* als u BitLocker automatisch en op de achtergrond wilt installeren op een apparaat dat aan Azure AD is toegevoegd en waarop Windows 1809 of hoger wordt uitgevoerd. Zie [BitLocker op de achtergrond inschakelen op apparaten](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices) voor meer informatie.

  Als de optie is ingesteld op *Blokkeren*, kunt u de volgende instelling configureren:  

  - **Standaardgebruikers toestaan om versleuteling in te schakelen tijdens Azure AD Join**  
    *Deze instelling is alleen van toepassing op apparaten met Azure Active Directory Joined (Azure ADJ) en is afhankelijk van de vorige instelling, `Warning for other disk encryption`.*  
    **Standaardinstelling**: Niet geconfigureerd  
    BitLocker-CSP: [AllowStandardUserEncryption](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp#allowstandarduserencryption)

     - **Toestaan**: standaardgebruikers (niet-beheerders) kunnen BitLocker-versleuteling inschakelen wanneer de gebruiker is aangemeld.  
     - **Niet geconfigureerd**: alleen beheerders kunnen BitLocker-versleuteling inschakelen op het apparaat.  

  > [!TIP]  
  > Deze instelling moet zijn ingesteld op *Toestaan* als u BitLocker automatisch en op de achtergrond wilt installeren op een apparaat dat aan Azure AD is toegevoegd en waarop Windows 1809 of hoger wordt uitgevoerd. Zie [BitLocker op de achtergrond inschakelen op apparaten](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices) voor meer informatie.

- **Versleutelingsmethoden configureren**  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **Inschakelen**: versleutelingsalgoritmen configureren voor het besturingssysteem, gegevens en verwisselbare stations.  
  - **Niet geconfigureerd**: BitLocker gebruikt XTS-AES-128-bits als de standaardmethode voor versleuteling, of de versleutelingsmethode die wordt opgegeven door een installatiescript.  

  Als de optie is ingesteld op *Inschakelen*, kunt u de volgende instellingen configureren:  

  - **Versleuteling voor stations met besturingssysteem**  
    **Standaardinstelling**: XTS-AES 128 bits  
   
    Kies de versleutelingsmethode voor stations met een besturingssysteem. Het is raadzaam om het algoritme XTS AES te gebruiken.  
    - **AES-CBC 128-bits**  
    - **AES-CBC 256-bits**  
    - **XTS-AES 128-bits**  
    - **XTS-AES 256 bits**  

  - **Versleuteling voor vaste gegevensschijven**  
    **Standaardinstelling**: AES-CBC 128-bits  
   
    Kies de versleutelingsmethode voor vaste (ingebouwde) schijven, ook wel 'harde schijven' genoemd. Het is raadzaam om het algoritme XTS AES te gebruiken.  
    - **AES-CBC 128-bits**  
    - **AES-CBC 256-bits**  
    - **XTS-AES 128-bits**  
    - **XTS-AES 256 bits**  

  - **Versleuteling voor verwisselbare gegevensstations**  
    **Standaardinstelling**: AES-CBC 128-bits  

    Kies de versleutelingsmethode voor verwisselbare gegevensstations. Als het verwisselbare station wordt gebruikt met apparaten waarop Windows 10 niet wordt uitgevoerd, wordt aanbevolen het algoritme AES-CBC te gebruiken.  
    - **AES-CBC 128-bits**  
    - **AES-CBC 256-bits**  
    - **XTS-AES 128-bits**  
    - **XTS-AES 256 bits**  

### <a name="bitlocker-os-drive-settings"></a>BitLocker-instellingen voor station met besturingssysteem  

Deze instellingen zijn van toepassing zijn op gegevensstations van het besturingssysteem.  

- **Aanvullende verificatie bij opstarten**  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)  

  - **Vereisen**: de verificatievereisten voor het opstarten van de computer configureren, waaronder het gebruik van TPM (Trusted Platform Module).  
  - **Niet geconfigureerd**: hiermee configureert u alleen eenvoudige opties op apparaten met een TPM.  

  Als de optie is ingesteld op *Vereisen*, kunt u de volgende instellingen configureren:  

  - **BitLocker met niet-compatibele TPM-chip**  
    **Standaardinstelling**: Niet geconfigureerd  

    - **Blokkeren**: gebruik van BitLocker uitschakelen wanneer een apparaat niet beschikt over een compatibele TPM-chip.  
    - **Niet geconfigureerd**: gebruikers kunnen BitLocker gebruiken zonder een compatibele TPM-chip. BitLocker vereist mogelijk een wachtwoord of een opstartsleutel.  

  - **Compatibele TPM opstarten**  
    **Standaardinstelling**: TPM toestaan  

    Configureren of TPM toegestaan, vereist of niet toegestaan is.  

    - **TPM toestaan**  
    - **TPM niet toestaan**  
    - **TPM vereisen**  

  - **Compatibele TPM-opstartpincode**  
    **Standaardinstelling**: Opstartpincode met TPM toestaan  

    Kies ervoor om het gebruik van een opstartpincode met de TPM-chip toe te staan, niet toe te staan of te vereisen. Voor het inschakelen van een opstartpincode is interactie van de eindgebruiker vereist.  

    - **Opstartpincode met TPM toestaan**  
    - **Opstartpincode met TPM niet toestaan**  
    - **Opstartpincode met TPM vereisen**

    > [!TIP]
    > Deze instelling moet zijn ingesteld op *Opstartpincode met TPM vereisen* als u BitLocker automatisch en op de achtergrond wilt installeren op een apparaat dat aan Azure AD is toegevoegd en waarop Windows 1809 of hoger wordt uitgevoerd. Zie [BitLocker op de achtergrond inschakelen op apparaten](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices) voor meer informatie.

  - **Compatibele TPM-opstartsleutel**  
    **Standaardinstelling**: Opstartsleutel met TPM toestaan  

    Kies ervoor om het gebruik van een opstartsleutel met de TPM-chip toe te staan, niet toe te staan of te vereisen. Voor het inschakelen van een opstartsleutel is interactie van de eindgebruiker vereist.  

    - **Opstartsleutel met TPM toestaan**  
    - **Opstartsleutel met TPM niet toestaan**  
    - **Opstartsleutel met TPM vereisen**  

    > [!TIP]
    > Deze instelling moet zijn ingesteld op *Opstartsleutel met TPM vereisen* als u BitLocker automatisch en op de achtergrond wilt installeren op een apparaat dat aan Azure AD is toegevoegd en waarop Windows 1809 of hoger wordt uitgevoerd. Zie [BitLocker op de achtergrond inschakelen op apparaten](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices) voor meer informatie.

  - **Compatibele opstartsleutel en pincode voor TPM**  
    **Standaardinstelling**: Opstartsleutel en -pincode met TPM toestaan  

    Kies ervoor om het gebruik van een opstartsleutel en -pincode met de TPM-chip toe te staan, niet toe te staan of te vereisen. Voor het inschakelen van een opstartsleutel en een pincode is interactie van de eindgebruiker vereist.  
    - **Opstartsleutel en -pincode met TPM toestaan**  
    - **Opstartsleutel en -pincode met TPM niet toestaan**  
    - **Opstartsleutel en -pincode met TPM vereisen**   

    > [!TIP]  
    > Deze instelling moet zijn ingesteld op *Opstartsleutel en -pincode met TPM vereisen* als u BitLocker automatisch en op de achtergrond wilt installeren op een apparaat dat aan Azure AD is toegevoegd en waarop Windows 1809 of hoger wordt uitgevoerd. Zie [BitLocker op de achtergrond inschakelen op apparaten](../protect/encrypt-devices.md#silently-enable-bitlocker-on-devices) voor meer informatie.

- **Minimale lengte pincode**  
    **Standaardinstelling**: Niet geconfigureerd  
    BitLocker-CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)   

    - **Inschakelen**: hiermee configureert u een minimale lengte voor de TPM-opstartpincode.  
    - **Niet geconfigureerd**: gebruikers kunnen een opstartpincode met een lengte tussen 6 en 20 cijfers configureren.  

  Als de optie is ingesteld op *Inschakelen*, kunt u de volgende instelling configureren:  

  - **Minimum aantal tekens**  
    **Standaardinstelling**: *Niet geconfigureerd* BitLocker-CSP: [SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)  

    Geef het aantal tekens op dat is vereist voor de opstartpincode, tussen **4**-**20**.  

- **Herstellen van besturingssysteemstation**  
  **Standaardinstelling**: Niet geconfigureerd   
  BitLocker-CSP: [SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)  

  - **Inschakelen**: bepalen hoe met BitLocker beveiligde besturingssysteemstations worden hersteld als de vereiste opstartgegevens niet beschikbaar zijn.  
  - **Niet geconfigureerd**: de standaardherstelopties worden ondersteund voor BitLocker-herstel. Standaard is een DRA toegestaan, de opties voor herstel zijn opgegeven door de gebruiker, met inbegrip van het herstelwachtwoord en de herstelsleutel, en er wordt geen reservekopie van herstelinformatie gemaakt op AD DS.  

  Als de optie is ingesteld op *Inschakelen*, kunt u de volgende instellingen configureren:  

  - **Agent voor gegevensherstel op basis van certificaten**  
    **Standaardinstelling**: Niet geconfigureerd  
     
    - **Blokkeren**: voorkom dat er een agent voor gegevensherstel wordt gebruikt in combinatie met besturingssysteemstations die met BitLocker zijn beveiligd.  
    - **Niet geconfigureerd**: agents voor gegevensherstel kunnen worden gebruikt met besturingssysteemstations die met BitLocker zijn beveiligd.  

  - **Herstelwachtwoord maken door gebruiker**  
    **Standaardinstelling**: Herstelwachtwoord van 48 cijfers toestaan  

    Kies of gebruikers verplicht of optioneel een herstelwachtwoord van 48 cijfers mogen genereren, of dat dit niet is toegestaan.  
    - **Herstelwachtwoord van 48 cijfers toestaan**  
    - **Geen herstelwachtwoord van 48 cijfers toestaan**  
    - **Herstelwachtwoord van 48 cijfers vereisen**  

  - **Herstelsleutel maken door gebruiker**  
    **Standaardinstelling**: 256-bits herstelsleutel toestaan  

    Kies of gebruikers verplicht of optioneel een herstelsleutel van 256 bits mogen genereren, of dat dit niet is toegestaan.  
    - **256-bits herstelsleutel toestaan**  
    - **Geen 256-bits herstelsleutel toestaan**  
    - **256-bits herstelsleutel vereisen**  

  - **Herstelopties in de BitLocker-installatiewizard**  
    **Standaardinstelling**: Niet geconfigureerd  

    - **Blokkeren**: gebruikers zien de opties voor herstel niet en kunnen deze dus niet wijzigen. Als deze optie is ingesteld op 
    - **Niet geconfigureerd**: gebruikers kunnen de opties voor herstel zien en wijzigen wanneer ze BitLocker inschakelen. 
 
  - **BitLocker-herstelgegevens opslaan in Azure Active Directory**  
    **Standaardinstelling**: Niet geconfigureerd  

    - **Inschakelen**: de BitLocker-herstelgegevens opslaan in Azure Active Directory (AAD).  
    - **Niet geconfigureerd**: BitLocker-herstelgegevens worden niet opgeslagen in AAD.  

  - **BitLocker-herstelgegevens opgeslagen in Azure Active Directory**  
    **Standaardinstelling**: Back-up maken van herstelwachtwoorden en sleutelpakketten  

    Hiermee bepaalt u welke delen van de BitLocker-herstelgegevens worden opgeslagen in Azure AD. U kunt kiezen uit:  
    - **Back-up maken van herstelwachtwoorden en sleutelpakketten**  
    - **Alleen een back-up maken van herstelwachtwoorden**  

  - **Clientgestuurde rotatie van herstelwachtwoorden**  
    **Standaardinstelling**: Sleutelrotatie is ingeschakeld voor apparaten die zijn toegevoegd aan Azure AD  
    BitLocker-CSP: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Met deze instelling wordt een clientgestuurde rotatie van het herstelwachtwoord gestart na herstel van het besturingssysteemstation (met bootmgr of WinRE).  

    - Niet geconfigureerd  
    - Sleutelrotatie is uitgeschakeld  
    - Sleutelrotatie is ingeschakeld voor apparaten die zijn toegevoegd aan Azure AD  
    - Sleutelrotatie is ingeschakeld voor apparaten die zijn toegevoegd aan Azure AD en hybride Azure AD  

  - **Herstelgegevens opslaan in Azure Active Directory voordat BitLocker wordt ingeschakeld**  
    **Standaardinstelling**: Niet geconfigureerd  
 
     Voorkomen dat gebruikers BitLocker inschakelen, tenzij er back-ups van de BitLocker-herstelgegevens kunnen worden gemaakt in Azure Active Directory.  

    - **Vereisen**: voorkomen dat gebruikers BitLocker inschakelen, tenzij de BitLocker-herstelgegevens zijn opgeslagen in Azure AD.  
    - **Niet geconfigureerd**: gebruikers kunnen BitLocker inschakelen, zelfs als herstelgegevens niet zijn opgeslagen in Azure AD.  

- **Preboot-herstelbericht en -URL**  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530)  

  - **Inschakelen**: hiermee kunt u het bericht en de URL configureren die worden weergegeven op het preboot-scherm voor sleutelherstel.  
  - **Niet geconfigureerd**: deze functie uitschakelen.  
  
  Als de optie is ingesteld op *Inschakelen*, kunt u de volgende instelling configureren:  
  - **Preboot-herstelbericht**  
    **Standaardinstelling**: Standaardherstelbericht en URL gebruiken   
 
    Configureer hoe het preboot-herstelbericht wordt weergegeven aan gebruikers. U kunt kiezen uit:  
    - **Standaardherstelbericht en URL gebruiken**  
    - **Leeg herstelbericht en -URL gebruiken**  
    - **Aangepaste herstelbericht gebruiken**  
    - **Aangepaste herstel-URL gebruiken**  

### <a name="bitlocker-fixed-data-drive-settings"></a>BitLocker-instellingen voor vaste-gegevensstations  

Deze instellingen zijn specifiek van toepassing op vaste gegevensstations.  

- **Schrijftoegang naar vaste-gegevensstations niet door BitLocker beveiligd**  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  

  - **Blokkeren**: alleen-lezentoegang geven aan gegevensstations die niet met BitLocker zijn beveiligd.  
  - **Niet geconfigureerd**: standaard lees- en schrijftoegang tot de gegevensstations die niet met BitLocker zijn beveiligd.  

- **Vast-stationherstel**  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)  

  - **Inschakelen**: bepalen hoe met BitLocker beveiligde vaste schijven worden hersteld als de vereiste opstartgegevens niet beschikbaar zijn.  
  - **Niet geconfigureerd**: deze functie uitschakelen.  

  Als de optie is ingesteld op *Inschakelen*, kunt u de volgende instellingen configureren:  

  - **Agent voor gegevensherstel**  
    **Standaardinstelling**: Niet geconfigureerd  
 
    - **Blokkeren**: voorkomen dat de agent voor gegevensherstel wordt gebruikt met door BitLocker beveiligde vaste schijven met beleidseditor. 
    - **Niet geconfigureerd**: het gebruik van agents voor gegevensherstel met BitLocker beveiligde vaste schijven inschakelen.  

  - **Herstelwachtwoord maken door gebruiker**  
    **Standaardinstelling**: Herstelwachtwoord van 48 cijfers toestaan  

    Kies of gebruikers verplicht of optioneel een herstelwachtwoord van 48 cijfers mogen genereren, of dat dit niet is toegestaan.  
    - **Herstelwachtwoord van 48 cijfers toestaan**  
    - **Geen herstelwachtwoord van 48 cijfers toestaan**  
    - **Herstelwachtwoord van 48 cijfers vereisen**  

  - **Herstelsleutel maken door gebruiker**  
    **Standaardinstelling**: 256-bits herstelsleutel toestaan

    Kies of gebruikers verplicht of optioneel een herstelsleutel van 256 bits mogen genereren, of dat dit niet is toegestaan.
    - **256-bits herstelsleutel toestaan**  
    - **Geen 256-bits herstelsleutel toestaan**  
    - **256-bits herstelsleutel vereisen**  

  - **Herstelopties in de BitLocker-installatiewizard**  
    **Standaardinstelling**: Niet geconfigureerd  

    - **Blokkeren**: gebruikers zien de opties voor herstel niet en kunnen deze dus niet wijzigen. Als deze optie is ingesteld op 
    - **Niet geconfigureerd**: gebruikers kunnen de opties voor herstel zien en wijzigen wanneer ze BitLocker inschakelen.
 
  - **BitLocker-herstelgegevens opslaan in Azure Active Directory**  
    **Standaardinstelling**: Niet geconfigureerd  

    - **Inschakelen**: de BitLocker-herstelgegevens opslaan in Azure Active Directory (AAD).  
    - **Niet geconfigureerd**: BitLocker-herstelgegevens worden niet opgeslagen in AAD.

  - **BitLocker-herstelgegevens opgeslagen in Azure Active Directory**  
    **Standaardinstelling**: Back-up maken van herstelwachtwoorden en sleutelpakketten  

    Hiermee bepaalt u welke delen van de BitLocker-herstelgegevens worden opgeslagen in Azure AD. U kunt kiezen uit:  
    - **Back-up maken van herstelwachtwoorden en sleutelpakketten**  
    - **Alleen een back-up maken van herstelwachtwoorden**  

  - **Clientgestuurde rotatie van herstelwachtwoorden**  
    **Standaardinstelling**: Sleutelrotatie is ingeschakeld voor apparaten die zijn toegevoegd aan Azure AD  
    BitLocker-CSP: [ConfigureRecoveryPasswordRotation](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)  
    
    Met deze instelling wordt een clientgestuurde rotatie van het herstelwachtwoord gestart na herstel van het besturingssysteemstation (met bootmgr of WinRE).  

    - Niet geconfigureerd  
    - Sleutelrotatie is uitgeschakeld  
    - Sleutelrotatie is ingeschakeld voor apparaten die zijn toegevoegd aan Azure AD  
    - Sleutelrotatie is ingeschakeld voor apparaten die zijn toegevoegd aan Azure AD en hybride Azure AD  

  - **Herstelgegevens opslaan in Azure Active Directory voordat BitLocker wordt ingeschakeld**  
    **Standaardinstelling**: Niet geconfigureerd  
 
    Voorkomen dat gebruikers BitLocker inschakelen, tenzij er back-ups van de BitLocker-herstelgegevens kunnen worden gemaakt in Azure Active Directory.  

    - **Vereisen**: voorkomen dat gebruikers BitLocker inschakelen, tenzij de BitLocker-herstelgegevens zijn opgeslagen in Azure AD.  
    - **Niet geconfigureerd**: gebruikers kunnen BitLocker inschakelen, zelfs als herstelgegevens niet zijn opgeslagen in Azure AD.  

### <a name="bitlocker-removable-data-drive-settings"></a>BitLocker-instellingen voor verwisselbare gegevensstations  

Deze instellingen zijn van toepassing op verwisselbare gegevensstations.  

- **Schrijftoegang voor een verwisselbaar gegevensstation dat niet door BitLocker is beveiligd**  
  **Standaardinstelling**: Niet geconfigureerd  
  BitLocker-CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  

  - **Blokkeren**: alleen-lezentoegang geven aan gegevensstations die niet met BitLocker zijn beveiligd.  
  - **Niet geconfigureerd**: standaard lees- en schrijftoegang tot de gegevensstations die niet met BitLocker zijn beveiligd.  

  Als de optie is ingesteld op *Inschakelen*, kunt u de volgende instelling configureren:  

  - **Schrijftoegang voor apparaten die zijn geconfigureerd in een andere organisatie**  
    **Standaardinstelling**: Niet geconfigureerd  

    - **Blokkeren**: schrijftoegang blokkeren voor apparaten die zijn geconfigureerd in een andere organisatie.  
    - **Niet geconfigureerd**: schrijftoegang weigeren.  
 
## <a name="microsoft-defender-exploit-guard"></a>Microsoft Defender Exploit Guard  

Gebruik [Exploit Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/exploit-protection) om de kwetsbaarheid van door uw medewerkers gebruikte apps voor aanvallen te beheren en te verminderen.  

### <a name="attack-surface-reduction"></a>Kwetsbaarheid voor aanvallen verminderen  

Met behulp van regels voor vermindering van oppervlakte-aanvallen helpt u het gedrag te voorkomen dat vaak door malware wordt gebruikt om computers met schadelijke code te infecteren.  

#### <a name="attack-surface-reduction-rules"></a>Regels voor het verminderen van kwetsbaarheid voor aanvallen  

- **Referentiediefstal in het Windows-subsysteem voor de lokale beveiligingsautoriteit markeren**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Blokkeer referentiediefstal in het Windows-subsysteem voor de lokale beveiligingsautoriteit (lsass.exe)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-credential-stealing-from-the-windows-local-security-authority-subsystem-lsassexe)

  Help acties en apps te voorkomen die meestal worden gebruikt door malware om computers te infecteren.  

  - **Niet geconfigureerd**  
  - **Inschakelen**: referentiediefstal in het Windows-subsysteem voor de lokale beveiligingsautoriteit (lsass.exe) markeren.  
  - **Alleen controle**  

- **Proces maken vanuit Adobe Reader (bètaversie)**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Blokkeren dat onderliggende processen kunnen worden gemaakt in Adobe Reader](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-adobe-reader-from-creating-child-processes)  

  - **Niet geconfigureerd**  
  - **Inschakelen**: blokkeer onderliggende processen die met behulp van Adobe Reader worden gemaakt.  
  - **Alleen controle**  

#### <a name="rules-to-prevent-office-macro-threats"></a>Regels voor het voorkomen van bedreigingen voor Office-macro's  

Blokkeer de volgende acties voor Office-apps:  

- **Office-apps injecteren in andere processen (geen uitzonderingen)**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Voorkomen dat Office-toepassingen code in andere processen injecteren](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-injecting-code-into-other-processes)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: voorkom dat vanuit Office-apps kan worden geïnjecteerd in andere processen.  
  - **Alleen controle**  

- **Uitvoerbare inhoud maken met Office-apps/-macro's**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Voorkomen dat Office-toepassingen uitvoerbare inhoud maken](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-applications-from-creating-executable-content)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: voorkom dat met Office-apps en -macro's uitvoerbare inhoud kan worden gemaakt.  
  - **Alleen controle**  

- **Onderliggende processen starten met Office-apps**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Voorkomen dat Office-toepassingen onderliggende processen maken](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-all-office-applications-from-creating-child-processes)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: voorkom dat onderliggende processen kunnen worden gestart met Office-apps.  
  - **Alleen controle**  
  
- **Win32-importbewerkingen uit macrocode van Office**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Win32 API-aanroepen blokkeren vanuit Office-macro's](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-win32-api-calls-from-office-macros)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: Win32-importbewerkingen vanuit macrocode in Office blokkeren.  
  - **Alleen controle**  
  
- **Proces maken vanuit communicatieproducten van Office**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Voorkomen dat Office-communicatietoepassingen onderliggende processen maken](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-office-communication-application-from-creating-child-processes)  

  - **Niet geconfigureerd**  
  - **Inschakelen**: voorkom dat vanuit communicatie-apps voor Office onderliggende processen kunnen worden gemaakt.  
  - **Alleen controle**  

#### <a name="rules-to-prevent-script-threats"></a>Regels om scriptbedreigingen te voorkomen  

Blokkeer de volgende acties om scriptbedreigingen te voorkomen:  

- **Verborgen js-/vbs-/ps-/macrocode**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [De uitvoering voorkomen van mogelijk betekenisloze scripts](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-execution-of-potentially-obfuscated-scripts)    

  - **Niet geconfigureerd**  
  - **Blokkeren**: verborgen js-/vbs-/ps-/macrocode blokkeren.  
  - **Alleen controle**  

- **Van internet gedownloade payloads uitvoeren met js-/vbs-bestanden (geen uitzonderingen)**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Voorkomen dat JavaScript of VBScript gedownloade uitvoerbare inhoud start](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-javascript-or-vbscript-from-launching-downloaded-executable-content)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: voorkom dat van internet gedownloade payloads kunnen worden uitgevoerd met js-/vbs-bestanden.  
  - **Alleen controle**  

- **Het maken van processen met PSExec- en WMI-opdrachten**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Voorkomen dat processen worden gemaakt die afkomstig zijn van PSExec- en WMI-opdrachten](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-process-creations-originating-from-psexec-and-wmi-commands)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: het maken van processen voorkomen die afkomstig zijn van PSExec- en WMI-opdrachten.  
  
  - **Alleen controle**  

- **Niet-vertrouwde en niet-ondertekende processen die worden uitgevoerd via USB**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Voorkomen dat niet-vertrouwde en niet-ondertekende processen kunnen worden uitgevoerd vanaf een USB](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-untrusted-and-unsigned-processes-that-run-from-usb)    

  - **Niet geconfigureerd**  
  - **Blokkeren**: voorkomen dat niet-vertrouwde en niet-ondertekende processen worden uitgevoerd vanaf een USB.  
  - **Alleen controle**  
  
- **Uitvoerbare bestanden die niet voldoen aan een bepaalde gangbaarheid, ouderdom of aan criteria voor vertrouwde lijsten blokkeren**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Voorkomen dat uitvoerbare bestanden worden uitgevoerd tenzij deze voldoen aan een bepaalde gangbaarheid, ouderdom of criteria voor vertrouwde lijsten](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-files-from-running-unless-they-meet-a-prevalence-age-or-trusted-list-criterion)    

  - **Niet geconfigureerd**  
  - **Blokkeren**: voorkomen dat uitvoerbare bestanden worden uitgevoerd tenzij deze voldoen aan een bepaalde gangbaarheid, ouderdom of criteria voor vertrouwde lijsten.  
  - **Alleen controle**  

#### <a name="rules-to-prevent-email-threats"></a>Regels om te e-mailbedreigingen te voorkomen  

Blokkeer de volgende acties om e-mailbedreigingen te voorkomen:  

- **Uitvoering van uitvoerbare inhoud (exe-, dll-, ps-, js-, vbs-bestanden enzovoort) die is verwijderd uit e-mail (webmail/e-mailclient) (geen uitzonderingen)**  
  **Standaardinstelling**: Niet geconfigureerd  
  Regel: [Uitvoerbare inhoud blokkeren van e-mailclient en webmail](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#block-executable-content-from-email-client-and-webmail)  

  - **Niet geconfigureerd**  
  - **Blokkeren**: uitvoering voorkomen van uitvoerbare inhoud (exe-, dll-, ps-, js-, vbs-bestanden, enzovoort) die is verwijderd uit e-mail (webmail/e-mailclient).  
  - **Alleen controle**  

#### <a name="rules-to-protect-against-ransomware"></a>Regels voor bescherming tegen ransomware  

- **Geavanceerde ransomwarebeveiliging**  
  Standaard:  Niet geconfigureerd  
  Regel: [Geavanceerde bescherming tegen ransomware gebruiken](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#use-advanced-protection-against-ransomware)  

  - **Niet geconfigureerd**  
  - **Inschakelen**: agressieve ransomwarebeveiliging gebruiken.  
  - **Alleen controle**  

#### <a name="attack-surface-reduction-exceptions"></a>Regels voor het verminderen van kwetsbaarheid voor aanvallen

- **Bestanden en mappen die worden uitgesloten voor regels voor kwetsbaarheid voor aanvallen verminderen**  
  Defender-CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)  

  - **Importeer** een CSV-bestand met bestanden en mappen die worden uitgesloten voor regels voor Kwetsbaarheid voor aanvallen verminderen.  
  - U kunt handmatig lokale bestanden of mappen **toevoegen**.  

> [!IMPORTANT]  
> Als u wilt toestaan dat LOB Win32-apps goed worden geïnstalleerd en uitgevoerd, moeten via de antimalware-instellingen worden ingesteld dat de volgende mappen niet worden gescand:  
> **Voor X64-clientcomputers**:  
> *C:\Program Files (x86)\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  
>  
> **Voor X86-clientcomputers**:  
> *C:\Program Files\Microsoft Intune Management Extension\Content*  
> *C:\windows\IMECache*  

### <a name="controlled-folder-access"></a>Gecontroleerde mappentoegang  

Hiermee kunt u [waardevolle gegevens beter beveiligen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/controlled-folders) tegen schadelijke apps en bedreigingen zoals ransomware.  

- **Mapbeveiliging**  
  **Standaardinstelling**: Niet geconfigureerd  
  Defender-CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)  

  Beveilig bestanden en mappen tegen niet-geautoriseerde wijzigingen door niet-goedgekeurde apps.  

  - **Niet geconfigureerd**  
  - **Inschakelen**  
  - **Alleen controle**  
  - **Schijfwijziging blokkeren**  
  - **Schijfwijziging controleren**  

  Wanneer u een andere configuratie selecteert dan *Niet geconfigureerd*, kunt u het volgende configureren:  
  - **Lijst met apps met toegang tot beveiligde mappen**  
    Defender-CSP: [ControlledFolderAccessAllowedApplications](https://go.microsoft.com/fwlink/?linkid=872616)  

    - U kunt ook een CSV-bestand met een lijst met apps **importeren**.  
    - U kunt handmatig apps aan deze lijst **toevoegen**.  

  - **Lijst met aanvullende mappen die moeten worden beveiligd**  
    Defender-CSP: [ControlledFolderAccessProtectedFolders](https://go.microsoft.com/fwlink/?linkid=872617)  

    - U kunt ook een CSV-bestand met een lijst met mappen **importeren**.  
    - U kunt handmatig mappen aan deze lijst **toevoegen**.  

### <a name="network-filtering"></a>Netwerk filteren  

Uitgaande verbindingen naar IP-adressen of domeinen met een slechte reputatie blokkeren voor elke app. Netwerkfilters worden ondersteund in zowel de modus Controleren als Blokkeren.  

- **Netwerkbeveiliging**  
  **Standaardinstelling**: Niet geconfigureerd  
  Defender-CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)  

  Deze instelling is bedoeld om eindgebruikers te beschermen tegen apps die toegang bieden tot phishing-praktijken, sites voor het hosten van aanvallen en schadelijke inhoud op internet. Hiermee voorkomt u ook dat browsers van derden verbinding maken met gevaarlijke websites.  

  - **Niet geconfigureerd**: deze functie uitschakelen. Gebruikers en apps kunnen wel verbinding maken met gevaarlijke domeinen. Beheerders kunnen deze activiteit niet bekijken in het Microsoft Defender-beveiligingscentrum.  
  - **Inschakelen**: hiermee schakelt u netwerkbeveiliging in en wordt voorkomen dat gebruikers en apps verbinding kunnen maken met gevaarlijke domeinen. Beheerders kunnen deze activiteit bekijken in het Microsoft Defender-beveiligingscentrum.  
  - **Alleen controle**: hiermee wordt niet voorkomen dat gebruikers en apps verbinding kunnen maken met gevaarlijke domeinen. Beheerders kunnen deze activiteit bekijken in het Microsoft Defender-beveiligingscentrum.  

### <a name="exploit-protection"></a>Exploit Protection  

- **XML uploaden**  
  **Standaardinstelling**: *Niet geconfigureerd*  

  Als u beveiliging tegen misbruik wilt gebruiken om [apparaten tegen misbruik te beschermen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection), maakt u een XML-bestand met de gewenste beperkingsinstellingen voor het systeem en de toepassing. Er zijn twee manieren om het XML-bestand te maken:  

  - *PowerShell*: gebruik een of meer van de PowerShell-cmdlets *Get-ProcessMitigation*, *Set-ProcessMitigation* en *ConvertTo-ProcessMitigationPolicy*. Met de cdmlets worden beperkingsinstellingen geconfigureerd en wordt hiervan een XML-weergave geëxporteerd.  

  - *Gebruikersinterface van het Microsoft Defender-beveiligingscentrum*: klik in het Windows Defender-beveiligingscentrum op het besturingselement voor de app en browser en scrol naar beneden op het scherm om Beveiliging met Exploit Guard te zoeken. Gebruik eerst de tabbladen Systeeminstellingen en Programma-instellingen om de beperkingsinstellingen te configureren. Zoek vervolgens de koppeling Instellingen exporteren onderaan het scherm om een XML-weergave hiervan te exporteren.  

- **Bewerking van beveiligingsinterface van Exploit Guard door gebruikers**  
  **Standaardinstelling**: Niet geconfigureerd  
  ExploitGuard-CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=872887)  


  - **Blokkeren**: upload een XML-bestand waarmee u het geheugen kunt configureren, stromen kunt beheren en beleidsbeperkingen kunt instellen. De instellingen in het XML-bestand kunnen worden gebruikt om een toepassing te blokkeren tegen aanvallen.  
  - **Niet geconfigureerd**: er wordt geen aangepaste configuratie gebruikt.  

## <a name="microsoft-defender-application-control"></a>Microsoft Defender-toepassingsbeheer  

Kies aanvullende apps die moeten worden gecontroleerd door of kunnen worden vertrouwd door Microsoft Defender Application Control. Windows-onderdelen en alle apps uit Windows Store worden automatisch vertrouwd.  


- **Integriteitsbeleidsregels van de stuurcode van de toepassing**  
  **Standaardinstelling**: Niet geconfigureerd  
   CSP: [AppLocker-CSP](https://go.microsoft.com/fwlink/?linkid=874543)  

  - **Afdwingen**: kies de integriteitsbeleidsregels van de stuurcode van de toepassing voor de apparaten van uw gebruikers.  
  
    Als toepassingsbeheer is ingeschakeld op een apparaat, kunt u de functie alleen uitschakelen door de modus te wijzigen van *Afdwingen* in *Alleen controle*. Als u de modus wijzigt van *Afdwingen* in *Niet geconfigureerd*, wordt toepassingsbeheer op toegewezen apparaten nog steeds afgedwongen.  

  - **Niet geconfigureerd**: toepassingsbeheer wordt niet aan apparaten toegevoegd. De instellingen die eerder zijn toegevoegd, worden echter nog steeds afgedwongen op toegewezen apparaten. 
 
  - **Alleen controle**: toepassingen worden niet geblokkeerd. Alle gebeurtenissen worden in de logboeken van de lokale client vastgelegd.  

## <a name="microsoft-defender-credential-guard"></a>Microsoft Defender Credential Guard  

Microsoft Defender Credential Guard beschermt tegen aanvallen waarbij referenties worden gestolen. Het isoleert geheimen zodat alleen bevoegde systeemsoftware er toegang toe heeft.  

- **Credential Guard**  
  **Standaardinstelling**: Uitschakelen  
  [DeviceGuard-CSP](https://go.microsoft.com/fwlink/?linkid=872424)  

  - **Uitschakelen**: Credential Guard op afstand uitschakelen als de functie eerder is ingeschakeld met de optie **Ingeschakeld zonder UEFI-vergrendeling**.  

  - **Inschakelen met UEFI-vergrendeling**: Credential Guard kan niet op afstand worden uitgeschakeld met een registersleutel of via Groepsbeleid.  

    > [!NOTE]
    > Als u deze instelling gebruikt en Credential Guard later wilt uitschakelen, moet u het Groepsbeleid instellen op **Uitgeschakeld**. Ook moet u de UEFI-configuratiegegevens fysiek van elke computer wissen. Zolang de UEFI-configuratie behouden blijft, is Credential Guard ingeschakeld.  

  - **Inschakelen zonder UEFI-vergrendeling**: instellen dat Credential Guard op afstand kan worden uitgeschakeld via Groepsbeleid. Op de apparaten die gebruikmaken van deze instelling moet Windows 10 versie 1511 en hoger worden uitgevoerd.  

  Wanneer u Credential Guard *inschakelt*, worden de volgende vereiste functies ook ingeschakeld:  
  
  - **Beveiliging op basis van virtualisatie** (VBS)  
    Wordt ingeschakeld wanneer de machine de volgende keer opnieuw wordt opgestart. Beveiliging op basis van virtualisatie maakt gebruik van de Windows-Hypervisor om ondersteuning te bieden voor beveiligingsservices.  
  - **Beveiligd opstarten met directe geheugentoegang**  
    Hiermee schakelt u beveiliging op basis van virtualisatie met beveiligd opstarten en directe geheugentoegang (DMA) in. Voor DMA-beveiliging is hardwareondersteuning vereist en deze wordt alleen ingeschakeld op apparaten die juist zijn geconfigureerd.  

## <a name="microsoft-defender-security-center"></a>Microsoft Defender-beveiligingscentrum  

Het Microsoft Defender-beveiligingscentrum werkt als een afzonderlijke app of een afzonderlijk proces van de afzonderlijke functies. Deze geeft meldingen weer via het onderhoudscentrum. Het fungeert als een collector of één afzonderlijke plaats om de status te zien en een configuratie van de functies uit te voeren. Meer informatie in de documenten over [Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-security-center/windows-defender-security-center).  

### <a name="microsoft-defender-security-center-app-and-notifications"></a>Microsoft Defender-beveiligingscentrum-app en meldingen  

Blokkeer de toegang van eindgebruikers tot verschillende gebieden van de Microsoft Defender-beveiligingscentrum-app. Als u een sectie verbergt, worden ook gekoppelde meldingen geblokkeerd.  

- **Virus- en bedreigingsbeveiliging**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [DisableVirusUI](https://go.microsoft.com/fwlink/?linkid=873662)  

  Configureer of eindgebruikers het gebied Virus- en bedreigingsbeveiliging kunnen zien in het Microsoft Defender-beveiligingscentrum. Wanneer u deze sectie verbergt, worden ook alle meldingen geblokkeerd die betrekking hebben op virus- en bedreigingsbeveiliging.  

  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Ransomwarebeveiliging**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [HideRansomwareDataRecovery](https://go.microsoft.com/fwlink/?linkid=873664)  

  Configureer of eindgebruikers het gebied Ransomwarebeveiliging kunnen zien in het Microsoft Defender-beveiligingscentrum. Wanneer u deze sectie verbergt, worden ook alle meldingen geblokkeerd die betrekking hebben op ransomwarebeveiliging.  

  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Accountbeveiliging**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [DisableAccountProtectionUI](https://go.microsoft.com/fwlink/?linkid=873666)  

  Configureer of eindgebruikers het gebied Accountbeveiliging kunnen zien in het Microsoft Defender-beveiligingscentrum. Wanneer u deze sectie verbergt, worden ook alle meldingen geblokkeerd die betrekking hebben op accountbeveiliging.  

  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Firewall- en netwerkbeveiliging**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [DisableNetworkUI](https://go.microsoft.com/fwlink/?linkid=873668)  

  Configureer of eindgebruikers het gebied Firewall- en netwerkbeveiliging kunnen zien in het Microsoft Defender-beveiligingscentrum. Wanneer u deze sectie verbergt, worden ook alle meldingen geblokkeerd die betrekking hebben op firewall- en netwerkbeveiliging.  

  - **Niet geconfigureerd**  
  - **Verbergen**  

- **App- en browserbeheer**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [DisableAppBrowserUI](https://go.microsoft.com/fwlink/?linkid=873669)  

  Configureer of eindgebruikers het gebied App- en browserbeheer kunnen zien in het Microsoft Defender-beveiligingscentrum. Wanneer u deze sectie verbergt, worden ook alle meldingen geblokkeerd die betrekking hebben op app- en browserbeheer.  

  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Hardwarebeveiliging**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [DisableDeviceSecurityUI](https://go.microsoft.com/fwlink/?linkid=873670)  

  Configureer of eindgebruikers het gebied Hardwarebeveiliging kunnen zien in het Microsoft Defender-beveiligingscentrum. Wanneer u deze sectie verbergt, worden ook alle meldingen geblokkeerd die betrekking hebben op hardwarebeveiliging.  

  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Prestaties en status van apparaat**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [DisableHealthUI](https://go.microsoft.com/fwlink/?linkid=873671)  

  Configureer of eindgebruikers het gebied Prestaties en status van apparaat kunnen zien in het Microsoft Defender-beveiligingscentrum. Wanneer u deze sectie verbergt, worden ook alle meldingen geblokkeerd die betrekking hebben op prestaties en status van apparaat.  
  
  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Gezinsopties**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [DisableFamilyUI](https://go.microsoft.com/fwlink/?linkid=873673)  

  Configureer of eindgebruikers het gebied Gezinsopties kunnen zien in het Microsoft Defender-beveiligingscentrum. Wanneer u deze sectie verbergt, worden ook alle meldingen geblokkeerd die betrekking hebben op gezinsopties.  
  
  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Meldingen van de weergegeven gebieden van de app**  
  **Standaardinstelling**: Niet geconfigureerd  
  WindowsDefenderSecurityCenter-CSP: [DisableNotifications](https://go.microsoft.com/fwlink/?linkid=873675)  

  Kies welke meldingen worden weergegeven voor eindgebruikers. Niet-kritieke meldingen zijn bijvoorbeeld samenvattingen van Microsoft Defender Antivirus-activiteiten en meldingen wanneer scans zijn voltooid. Alle andere meldingen worden beschouwd als kritiek.  

  - **Niet geconfigureerd**  
  - **Niet-kritieke meldingen blokkeren**  
  - **Alle meldingen blokkeren**  

- **Windows Security Center-pictogram in het systeemvak**  
  **Standaardinstelling**: Niet geconfigureerd  

  Configureer de weergave van het beheer van het meldingengebied. De gebruiker moet zich afmelden en weer aanmelden of de computer opnieuw opstarten om deze instelling toe te passen.  
  
  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Knop TPM wissen**  
  **Standaardinstelling**: Niet geconfigureerd  

  Configureer de weergave van de knop TPM wissen.  
  
  - **Niet geconfigureerd**  
  - **Uitschakelen**  

- **Waarschuwing TPM-firmware bijwerken**  
  **Standaardinstelling**: Niet geconfigureerd  
  
  Configureer de weergave van TPM-firmware bijwerken wanneer kwetsbare firmware wordt gedetecteerd.  

  - **Niet geconfigureerd**  
  - **Verbergen**  

- **Manipulatiebeveiliging**  
  **Standaardinstelling**: Niet geconfigureerd

  Schakel Manipulatiebeveiliging in of uit op apparaten. Als u Manipulatiebeveiliging wilt gebruiken, moet u [Microsoft Advanced Threat Protection integreren met Intune](advanced-threat-protection.md) en over [Enterprise Mobility + Security E5-licenties](../fundamentals/licenses.md) beschikken.  
  - **Niet geconfigureerd**: de apparaatinstellingen zijn niet gewijzigd.
  - **Ingeschakeld**: Manipulatiebeveiliging wordt ingeschakeld en er worden beperkingen afgedwongen op apparaten.
  - **Uitgeschakeld**: Manipulatiebeveiliging wordt uitgeschakeld en er worden geen beperkingen afgedwongen.

### <a name="it-contact-information"></a>IT-contactgegevens  

Geef de IT-contactgegevens op die in de Microsoft Defender-beveiligingscentrum-app en in de app-meldingen moeten worden weergegeven.  

U kunt kiezen tussen **In app en in meldingen weergeven**, **Alleen in app weergeven**, **Alleen in meldingen weergeven** en **Niet weergeven**. Voer de **IT-organisatienaam** en ten minste één van de volgende contactopties in:  


- **IT-contactgegevens**  
  **Standaardinstelling**: Niet weergeven  
  WindowsDefenderSecurityCenter-CSP: [EnableCustomizedToasts](https://go.microsoft.com/fwlink/?linkid=873676)  
  
  Geef aan waar de contactgegevens van de IT-afdeling voor eindgebruikers moeten worden weergegeven.  
  
  - **In app en in meldingen weergeven**  
  - **Alleen in app weergeven**  
  - **Alleen in meldingen weergeven**  
  - **Niet weergeven**  

  Als dit is geconfigureerd op weergeven, kunt u de volgende instellingen configureren:  

  - **Naam van IT-organisatie**  
    **Standaardinstelling**: *Niet geconfigureerd*  
    WindowsDefenderSecurityCenter-CSP: [CompanyName](https://go.microsoft.com/fwlink/?linkid=873677)  

  - **Telefoonnummer of Skype-ID van de IT-afdeling**  
    **Standaardinstelling**: *Niet geconfigureerd*  
    WindowsDefenderSecurityCenter-CSP: [Telefoon](https://go.microsoft.com/fwlink/?linkid=873678) 

  - **E-mailadres van de IT-afdeling**  
    **Standaardinstelling**: *Niet geconfigureerd*  
    WindowsDefenderSecurityCenter-CSP: [E-mail](https://go.microsoft.com/fwlink/?linkid=873679)  

  - **URL van de IT-ondersteuningswebsite**  
    **Standaardinstelling**: *Niet geconfigureerd*  
    WindowsDefenderSecurityCenter-CSP: [URL](https://go.microsoft.com/fwlink/?linkid=873680)  
 
## <a name="local-device-security-options"></a>Beveiligingsopties van lokale apparaten  

Gebruik deze opties voor het configureren van de lokale beveiligingsinstellingen op Windows 10-apparaten.  

### <a name="accounts"></a>Accounts  

- **Nieuwe Microsoft-accounts toevoegen**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [Accounts_BlockMicrosoftAccounts](https://go.microsoft.com/fwlink/?linkid=867916)  


  - **Blokkeren**: voorkomen dat gebruikers nieuwe Microsoft-accounts aan het apparaat toevoegen.  
  - **Niet geconfigureerd**: gebruikers kunnen Microsoft-accounts gebruiken op het apparaat.  

- **Extern aanmelden zonder wachtwoord**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867890)  


   - **Blokkeren**: lokale accounts met lege wachtwoorden alleen toestaan zich aan te melden met behulp van het toetsenbord van het apparaat.  
   - **Niet geconfigureerd**: lokale accounts met lege wachtwoorden kunnen zich aanmelden vanaf andere locaties dan het fysieke apparaat.  

#### <a name="admin"></a>Administrator  

- **Lokaal beheerdersaccount**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=867850)  


  - **Blokkeren**: hiermee voorkomt u het gebruik van een lokaal beheerdersaccount.  
  - **Niet geconfigureerd**  

- **Naam van beheerdersaccount wijzigen**  
  **Standaardinstelling**: *Niet geconfigureerd*  
  LocalPoliciesSecurityOptions-CSP: [Accounts_RenameAdministratorAccount](https://go.microsoft.com/fwlink/?linkid=867917)  
 

  Definieer een andere accountnaam die moet worden gekoppeld aan de beveiligings-id (SID) van het beheerdersaccount.  

 #### <a name="guest"></a>Gast  

- **Gastaccount**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [LocalPoliciesSecurityOptions](https://go.microsoft.com/fwlink/?linkid=867853)  

  - **Blokkeren**: hiermee voorkomt u het gebruik van een gastaccount.  
  - **Niet geconfigureerd**  

- **Naam van het gastaccount wijzigen**  
  **Standaardinstelling**: *Niet geconfigureerd*  
  LocalPoliciesSecurityOptions-CSP: [Accounts_RenameGuestAccount](https://go.microsoft.com/fwlink/?linkid=867918)  
  
  Definieer een andere accountnaam die moet worden gekoppeld aan de beveiligings-id (SID) van het gastaccount.  

### <a name="devices"></a>Apparaten  

- **Apparaat ontkoppelen zonder aanmelding**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [Devices_AllowUndockWithoutHavingToLogon](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-devices-allowundockwithouthavingtologon)  

  
  - **Blokkeren**: gebruikers kunnen op de fysieke knop voor het uitwerpen van een gedokt draagbaar apparaat drukken om het apparaat veilig te ontkoppelen.  
  - **Niet geconfigureerd**: een gebruiker moet zich aanmelden bij het apparaat en toestemming krijgen om het apparaat los te koppelen.  

- **Stuurprogramma's voor gedeelde printers installeren**  
  **Standaardinstelling**:  Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [Devices_PreventUsersFromInstallingPrinterDriversWhenConnectingToSharedPrinters](https://go.microsoft.com/fwlink/?linkid=867921)  


  - **Ingeschakeld**: elke gebruiker kan een printerstuurprogramma installeren als onderdeel van het maken van verbinding met een gedeelde printer.  
  - **Niet geconfigureerd**: alleen beheerders kunnen een printerstuurprogramma installeren als onderdeel van het maken van een verbinding met een gedeelde printer.  

- **Cd-rom-toegang beperken tot lokale actieve gebruiker**  
  **Standaardinstelling**:  Niet geconfigureerd  
  CSP: [Devices_RestrictCDROMAccessToLocallyLoggedOnUserOnly](https://go.microsoft.com/fwlink/?linkid=867922)  


  - **Ingeschakeld**: alleen de interactief aangemelde gebruiker kan de cd-rom-media gebruiken. Als dit beleid is ingeschakeld en niemand interactief is aangemeld, wordt de cd-rom geopend via het netwerk.  
  - **Niet geconfigureerd**: iedereen heeft toegang tot de cd-rom.  

- **Verwisselbare media formatteren en uitwerpen**  
  **Standaardinstelling**: Beheerders  
  CSP: [Devices_AllowedToFormatAndEjectRemovableMedia](https://go.microsoft.com/fwlink/?linkid=867920)  
 

  Definieer de personen voor wie het is toegestaan om verwisselbare NTFS-media te formatteren en uit te werpen:  
  - **Niet geconfigureerd**  
  - **Beheerders**  
  - **Beheerders en hoofdgebruikers**  
  - **Beheerders en interactieve gebruikers**  

### <a name="interactive-logon"></a>Interactief aanmelden  

- **Minuten van inactiviteit van vergrendelingsscherm totdat de schermbeveiliging wordt geactiveerd**  
  **Standaardinstelling**: *Niet geconfigureerd*  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_MachineInactivityLimit](https://go.microsoft.com/fwlink/?linkid=867891)  


  Voer het maximale aantal minuten van inactiviteit in op het aanmeldingsscherm van het interactieve bureaublad totdat de schermbeveiliging actief wordt. (**0** - **99999**)  

- **CTRL+ALT+DEL vereisen om aan te melden**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_DoNotRequireCTRLALTDEL](https://go.microsoft.com/fwlink/?linkid=867951)  


  - **Inschakelen**: gebruikers hoeven niet op CTRL+ALT+DEL te drukken om zich aan te melden.  
  - **Niet geconfigureerd**: vereisen dat gebruikers op CTRL+ALT+DEL drukken om zich aan te melden bij Windows.  

- **Gedrag bij verwijderen van smartcard**  
  **Standaardinstelling**: Werkstation vergrendelen   
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_SmartCardRemovalBehavior](https://go.microsoft.com/fwlink/?linkid=868437)  
    
  Hiermee bepaalt u wat er gebeurt wanneer de smartcard van een aangemelde gebruiker uit de lezer van de smartcard wordt verwijderd. Uw opties zijn:  

  - **Werkstation vergrendelen**: het werkstation wordt vergrendeld wanneer de smartcard wordt verwijderd. Met deze optie kunnen gebruikers het gebied verlaten, de smartcard meenemen en toch een beveiligde sessie behouden.  
  - **Geen actie**  
  - **Afmelden forceren**: de gebruiker wordt automatisch afgemeld wanneer de smartcard wordt verwijderd.  
  - **Verbinding verbreken bij sessie met Extern bureaublad-services**: als de smartcard wordt verwijderd, wordt de sessie verbroken zonder de gebruiker af te melden. Met deze optie kan de gebruiker de smartcard plaatsen en de sessie later of op een andere met smartcardlezer uitgeruste computer hervatten zonder zich opnieuw te moeten melden. Als de sessie lokaal is, werkt dit beleid op dezelfde manier als Werkstation vergrendelen.  

#### <a name="display"></a>Weergave  

- **Gebruikersinformatie op vergrendelingsscherm**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_DisplayUserInformationWhenTheSessionIsLocked](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-displayuserinformationwhenthesessionislocked)  

  Configureer welke gebruikersinformatie wordt weergegeven wanneer de sessie is vergrendeld. Als deze optie niet is geconfigureerd, worden de weergavenaam van de gebruiker, het domein en de gebruikersnaam weergegeven.  

  - **Niet geconfigureerd**  
  - **Weergavenaam van gebruiker, domein en gebruikersnaam**  
  - **Alleen weergavenaam gebruiker**  
  - **Gebruikersinformatie niet weergeven**  

- **Laatste aangemelde gebruiker verbergen**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_DoNotDisplayLastSignedIn](https://go.microsoft.com/fwlink/?linkid=868437)  
  
  
  - **Inschakelen**: de gebruikersnaam wordt verborgen.  
  - **Niet geconfigureerd**: de laatste gebruikersnaam wordt weergegeven.  

- **Gebruikersnaam verbergen bij aanmelden**
  **Standaard**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_DoNotDisplayUsernameAtSignIn](https://go.microsoft.com/fwlink/?linkid=867959)  

  
  - **Inschakelen**: de gebruikersnaam wordt verborgen.  
  - **Niet geconfigureerd**: de laatste gebruikersnaam wordt weergegeven.  

- **Titel aanmeldingsbericht**  
  **Standaardinstelling**: *Niet geconfigureerd*  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_MessageTitleForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867964)  

  Stel de berichttitel in voor gebruikers die zich aanmelden.  

- **Tekst aanmeldingsbericht**  
  **Standaardinstelling**: *Niet geconfigureerd*  
  LocalPoliciesSecurityOptions-CSP: [InteractiveLogon_MessageTextForUsersAttemptingToLogOn](https://go.microsoft.com/fwlink/?linkid=867962)  

  Stel de berichttekst in voor gebruikers die zich aanmelden.  
  
### <a name="network-access-and-security"></a>Netwerktoegang en -beveiliging

- **Anonieme toegang tot named pipes en shares**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [NetworkAccess_RestrictAnonymousAccessToNamedPipesAndShares](https://go.microsoft.com/fwlink/?linkid=868432)  

  - **Niet geconfigureerd**: anonieme toegang beperken tot instellingen voor delen en named pipes. Van toepassing op de instellingen die anoniem kunnen worden gebruikt.  
  - **Blokkeren**: als u dit beleid uitschakelt, komt anonieme toegang ter beschikking.  

- **Anonieme inventarisatie van SAM-accounts**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSAMAccounts](https://go.microsoft.com/fwlink/?linkid=868434)  
  
  - **Niet geconfigureerd**: anonieme gebruikers kunnen inventarisatie van SAM-accounts uitvoeren.  
  - **Blokkeren**: anonieme inventarisatie van SAM-accounts voorkomen.  

- **Anonieme inventarisatie van SAM-accounts en -shares**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [NetworkAccess_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares](https://go.microsoft.com/fwlink/?linkid=868435)  

  - **Niet geconfigureerd**: anonieme gebruikers kunnen de namen van domeinaccounts en netwerkshares inventariseren.  
  - **Blokkeren**: anonieme inventarisatie van SAM-accounts en -shares voorkomen. 

- **Hash-waarde van LAN Manager opslaan bij wachtwoordwijziging**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_DoNotStoreLANManagerHashValueOnNextPasswordChange](https://go.microsoft.com/fwlink/?linkid=868431)  
   
  Bepaal of de hash-waarde voor wachtwoorden wordt opgeslagen zodra het wachtwoord weer wordt gewijzigd. 
  - **Niet geconfigureerd**: de hash-waarde wordt niet opgeslagen  
  - **Blokkeren**: de hash-waarde voor het nieuwe wachtwoord wordt door de LAN-manager (LM) opgeslagen.  

- **PKU2U-verificatieaanvragen**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_AllowPKU2UAuthenticationRequests](https://go.microsoft.com/fwlink/?linkid=867892)  

  - **Niet geconfigureerd**: PU2U-aanvragen toestaan.  
  - **Blokkeren**: PKU2U-verificatieaanvragen aan het apparaat blokkeren.  

- **Externe RPC-verbindingen met SAM beperken**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [NetworkAccess_RestrictClientsAllowedToMakeRemoteCallsToSAM](https://go.microsoft.com/fwlink/?linkid=867893)  
  
  - **Niet geconfigureerd**: gebruik de standaardinstelling van de Security Descriptor om gebruikers en groepen toe te staan om externe RPC-aanroepen naar de SAM uit te voeren.
  - **Toestaan**: voorkom dat gebruikers en groepen externe RPC-aanroepen kunnen maken naar de Security Accounts Manager (SAM), waarin gebruikersaccounts en wachtwoorden worden opgeslagen. **Toestaan**: hiermee kunt u ook de Security Descriptor Definition Language-standaardtekenreeks (SDDL) wijzigen om gebruikers en groepen expliciet wel of niet toe te staan deze externe aanroepen te maken.  

    - **Beveiligingsdescriptor**  
      **Standaardinstelling**: *Niet geconfigureerd*  
    
- **Minimale sessiebeveiliging voor op NTLM SSP-gebaseerde clients**  
  **Standaardinstelling**: Geen  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedClients](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)  
  
  Via deze beveiligingsinstelling kan een server de onderhandeling van een 128-bits versleuteling en/of een NTLMv2-sessiebeveiliging vereisen.  

  - **Geen**  
  - **NTLMv2-sessiebeveiliging vereisen**  
  - **128-bits versleuteling vereisen**  
  - **NTLMv2 en 128-bits versleuteling**  
 
- **Minimale sessiebeveiliging voor op NTLM SSP-gebaseerde servers**  
  **Standaardinstelling**: Geen  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedServers](https://aka.ms/policy-csp-localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)  

  Met deze beveiligingsinstelling bepaalt u welk vraag/antwoord-verificatieprotocol wordt gebruikt voor netwerkaanmeldingen.  

  - **Geen**  
  - **NTLMv2-sessiebeveiliging vereisen**  
  - **128-bits versleuteling vereisen**  
  - **NTLMv2 en 128-bits versleuteling**  

- **LAN Manager-verificatieniveau**  
  **Standaardinstelling**: LM en NTLM  
  LocalPoliciesSecurityOptions-CSP: [NetworkSecurity_LANManagerAuthenticationLevel](https://aka.ms/policy-csp-localpoliciessecurityoptions-lanmanagerauthenticationlevel)  


  - **LM en NTLM**  
  - **LM, NTLM en NTLMv2**  
  - **NTLM**  
  - **NTLMv2**  
  - **NTLMv2 en niet LM**  
  - **NTLMv2 en niet LM of NTLM**  
  
- **Onveilige gastaanmeldingen**  
  **Standaardinstelling**: Niet geconfigureerd  
  LanmanWorkstation-CSP: [LanmanWorkstation](https://aka.ms/policy-csp-lanmanworkstation-enableinsecureguestlogons)  

  Als u deze instelling inschakelt, weigert de SMB-client onveilige aanmeldingen van gasten.  

  - **Niet geconfigureerd**  
  - **Blokkeren**: onveilige gastaanmeldingen worden door de SMB-client geweigerd.  

### <a name="recovery-console-and-shutdown"></a>Herstelconsole en afsluiten  

- **Wisselbestand voor virtueel geheugen wissen bij het afsluiten**  
  **Standaardinstelling**: Niet geconfigureerd  
   LocalPoliciesSecurityOptions-CSP: [Shutdown_ClearVirtualMemoryPageFile](https://go.microsoft.com/fwlink/?linkid=867914)  


  - **Inschakelen**: het wisselbestand voor virtueel geheugen wissen wanneer het apparaat wordt uitgeschakeld.  
  - **Niet geconfigureerd**: het virtuele geheugen niet wissen.  

- **Afsluiten zonder aanmelden**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [Shutdown_AllowSystemToBeShutDownWithoutHavingToLogOn](https://go.microsoft.com/fwlink/?linkid=867912)  

  
  - **Blokkeren**: de afsluitoptie in het Windows-aanmeldingsscherm verbergen. Gebruikers moet zich aanmelden bij het apparaat en vervolgens afsluiten.  
  - **Niet geconfigureerd**: gebruikers kunnen het apparaat afsluiten vanaf het Windows-aanmeldingsscherm.  

### <a name="user-account-control"></a>Gebruikersaccountbeheer  

- **UIA-integriteit zonder veilige locatie**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867897)  
  
  - **Blokkeren**: apps in een beveiligde locatie in het bestandssysteem kunnen alleen met UI-toegangsintegriteit worden uitgevoerd.  
  - **Niet geconfigureerd**: apps kunnen worden uitgevoerd met UIAccess-integriteit, zelfs als de apps zich niet op een veilige locatie in het bestandssysteem bevinden.  

- **Schrijffouten in bestanden en registers in locaties per gebruiker virtualiseren**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations](https://go.microsoft.com/fwlink/?linkid=867900)  

  - **Ingeschakeld**: in toepassingen die gegevens schrijven naar beveiligde locaties, treden fouten op.  
  - **Niet geconfigureerd**: schrijffouten in toepassingen worden tijdens runtime omgeleid naar gedefinieerde gebruikerslocaties voor het bestandssysteem en register.  

- **Alleen bevoegdheden verhogen voor uitvoerbare bestanden die zijn ondertekend en gevalideerd**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=867965)  

  - **Ingeschakeld**: de validatie van het PKI-certificeringspad afdwingen voor een uitvoerbaar bestand voordat dit mag worden uitgevoerd.  
  - **Niet geconfigureerd**: validatie van het PKI-certificeringspad niet afdwingen voordat een uitvoerbaar bestand kan worden uitgevoerd.  

#### <a name="uia-elevation-prompt-behavior"></a>Gedrag bij vragen om UIA-uitbreiding  

- **Vragen om benodigde bevoegdheden voor beheerders**  
  **Standaardinstelling**: Vragen om toestemming voor niet-Windows binaire bestanden  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_BehaviorOfTheElevationPromptForAdministrators](https://go.microsoft.com/fwlink/?linkid=867895)  

  Definieer het gedrag voor het vragen om benodigde bevoegdheden voor beheerders in de modus Door administrator goedkeuren.  

  - **Niet geconfigureerd**  
  - **Verhogen zonder te vragen**  
  - **Vragen om referenties op het beveiligde bureaublad**  
  - **Vragen om referenties**  
  - **Vragen om toestemming**  
  - **Vragen om toestemming voor niet-Windows binaire bestanden**  


- **Vragen om benodigde bevoegdheden voor standaardgebruikers**  
  **Standaardinstelling**: Vragen om referenties  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_BehaviorOfTheElevationPromptForStandardUsers](https://go.microsoft.com/fwlink/?linkid=867896)  

  Definieer het gedrag voor het vragen om benodigde bevoegdheden voor standaardgebruikers.  

  - **Niet geconfigureerd**  
  - **Vragen voor benodigde bevoegdheden automatisch weigeren**  
  - **Vragen om referenties op het beveiligde bureaublad**  
  - **Vragen om referenties**  

- **Leid vragen over benodigde bevoegdheden naar het interactieve bureaublad van de gebruiker**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_SwitchToTheSecureDesktopWhenPromptingForElevation](https://go.microsoft.com/fwlink/?linkid=867899)  


  - **Ingeschakeld**: alle vragen over bevoegdheden worden naar het bureaublad van de interactieve gebruiker geleid, in plaats van naar het beveiligde bureaublad. Er worden beleidsinstellingen voor gedrag voor beheerders en standaardgebruikers gebruikt.  
  - **Niet geconfigureerd**: afdwingen dat alle aanvragen voor uitbreiding van bevoegdheden naar het beveiligde bureaublad gaan, ongeacht eventuele beleidsinstellingen voor gedrag voor beheerders en standaardgebruikers.

- **Prompt met verhoogde bevoegdheden voor app-installaties**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_DetectApplicationInstallationsAndPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867901)  

   - **Ingeschakeld**: installatiepakketten voor toepassingen worden niet gedetecteerd en worden niet om benodigde bevoegdheden gevraagd.
   - **Niet geconfigureerd**: gebruikers worden gevraagd om een gebruikersnaam en wachtwoord van een beheerder wanneer het installatiepakket van een toepassing verhoogde bevoegdheden vereist.

- **Vragen om benodigde UIA-bevoegdheden zonder beveiligd bureaublad**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_AllowUIAccessApplicationsToPromptForElevation](https://go.microsoft.com/fwlink/?linkid=867894)  

- **Inschakelen**: UIAccess-apps toestemming geven om te vragen om benodigde bevoegdheden zonder het beveiligde bureaublad te gebruiken.  
- **Niet geconfigureerd**: de vragen om de benodigde bevoegdheden worden naar een beveiligd bureaublad geleid.  

#### <a name="admin-approval-mode"></a>Modus Door administrator goedkeuren  

- **Modus Door administrator goedkeuren voor geïntegreerde beheerder**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_UseAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867902)  

  - **Ingeschakeld**: het ingebouwde Administrator-account kan de modus Door administrator goedkeuren gebruiken. Voor elke bewerking waarvoor uitbreiding van toegangsrechten is vereist, wordt de gebruiker gevraagd de bewerking goed te keuren.  
  - **Niet geconfigureerd**: alle apps worden met volledige beheerdersbevoegdheden uitgevoerd.  

- **Alle beheerders uitvoeren in de modus Door administrator goedkeuren**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [UserAccountControl_RunAllAdministratorsInAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=867898)  


  - **Ingeschakeld**: de modus Door administrator goedkeuren inschakelen.  
  - **Niet geconfigureerd**: de modus Door administrator goedkeuren en alle gerelateerde UAC-beleidsinstellingen uitschakelen.  

### <a name="microsoft-network-client"></a>Microsoft Network Client  

- **Clientcommunicatie digitaal ondertekenen (indien mogelijk)**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [MicrosoftNetworkClient_DigitallySignCommunicationsIfServerAgrees](https://go.microsoft.com/fwlink/?linkid=868423)  

  Hiermee wordt bepaald of de SMB-client onderhandelt over SMB-pakketondertekening.  
  - **Blokkeren**: de SMB-client onderhandelt nooit over SMB-pakketondertekening.
  - **Niet geconfigureerd**: de Microsoft-netwerkclient vraagt de server om SMB-pakketondertekening uit te voeren bij het opzetten van een sessie. Als pakketondertekening is ingeschakeld op de server, wordt over ondertekening van pakketten onderhandeld.  

- **Niet-versleuteld wachtwoord verzenden om verbinding te kunnen maken met niet-Microsoft SMB-servers**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [MicrosoftNetworkClient_SendUnencryptedPasswordToThirdPartySMBServers](https://go.microsoft.com/fwlink/?linkid=868426)  


  - **Blokkeren**: de SMB-redirector (Server Message Block) kan ongecodeerde wachtwoorden verzenden naar niet-Microsoft SMB-servers die geen ondersteuning voor wachtwoordversleuteling bieden tijdens verificatie.  
  - **Niet geconfigureerd**: blokkeer het verzenden van niet-gecodeerde wachtwoorden. De wachtwoorden zijn versleuteld.  

- **Communicatie digitaal ondertekenen (altijd)**  
  **Standaardinstelling**: Niet geconfigureerd  
  LocalPoliciesSecurityOptions-CSP: [MicrosoftNetworkClient_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868425)  


  - **Inschakelen**: de Microsoft-netwerkclient communiceert niet met een Microsoft-netwerkserver, tenzij die server akkoord gaat met SMB-pakketondertekening.  
  - **Niet geconfigureerd**: het ondertekenen van SMB-pakketten wordt onderhandeld door de client en de server.  

### <a name="microsoft-network-server"></a>Microsoft Network Server  
  
- **Communicatie digitaal ondertekenen (bij akkoord van client)**  
  **Standaardinstelling**: Niet geconfigureerd  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsIfClientAgrees](https://go.microsoft.com/fwlink/?linkid=868429)  

  - **Inschakelen**: de Microsoft-netwerkserver onderhandelt over SMB-pakketondertekening zoals aangevraagd door de client. Ofwel, als pakketondertekening is ingeschakeld op de client, wordt over ondertekening van pakketten onderhandeld.  
  - **Niet geconfigureerd**: de SMB-client onderhandelt nooit over SMB-pakketondertekening.  

- **Communicatie digitaal ondertekenen (altijd)**  
  **Standaardinstelling**: Niet geconfigureerd  
  CSP: [MicrosoftNetworkServer_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=868428)  

  - **Inschakelen**: de Microsoft-netwerkserver communiceert niet met een Microsoft-netwerkclient, tenzij die client akkoord gaat met SMB-pakketondertekening.  
  - **Niet geconfigureerd**: het ondertekenen van SMB-pakketten wordt onderhandeld door de client en de server.  

## <a name="xbox-services"></a>Xbox-services

- **Xbox Game Save Task**  
  **Standaardinstelling**: Niet geconfigureerd  
  CSP: [TaskScheduler/EnableXboxGameSaveTask](https://go.microsoft.com/fwlink/?linkid=875480)  
   
  Met deze instelling wordt bepaald of de Xbox Game Save Task is Ingeschakeld of Uitgeschakeld.  
  - **Ingeschakeld**
  - **Niet geconfigureerd**

- **Xbox Accessory Management-service**  
  **Standaardinstelling**: Handmatig  
  CSP: [SystemServices/ConfigureXboxAccessoryManagementServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875481)  

  Met deze instelling bepaalt u het starttype van de Accessory Management-service.  
  - **Handmatig**
  - **Automatisch**
  - **Uitgeschakeld**

- **Xbox Live Auth Manager-service**  
  **Standaardinstelling**: Handmatig  
  CSP: [SystemServices/ConfigureXboxLiveAuthManagerServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875482)  
 
  Met deze instelling bepaalt u het starttype van de Live Auth Manager-service.  
  - **Handmatig**
  - **Automatisch**
  - **Uitgeschakeld**
 
- **Xbox Live Game Save-service**  
  **Standaardinstelling**: Handmatig  
  CSP: [SystemServices/ConfigureXboxLiveGameSaveServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875483)  

  Met deze instelling bepaalt u het starttype van de Live Game Save-service.  
  - **Handmatig**
  - **Automatisch**
  - **Uitgeschakeld**

- **Xbox Live-netwerkservice**  
  **Standaardinstelling**: Handmatig  
  CSP: [SystemServices/ConfigureXboxLiveNetworkingServiceStartupMode](https://go.microsoft.com/fwlink/?linkid=875484)  

  Met deze instelling bepaalt u het starttype van de netwerkservice.  
  - **Handmatig**
  - **Automatisch**
  - **Uitgeschakeld**

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt nog niets. Vervolgens moet u [het profiel toewijzen](../configuration/device-profile-assign.md) en [de status ervan controleren](../configuration/device-profile-monitor.md).  

Instellingen voor eindpuntbescherming configureren op [macOS](endpoint-protection-macos.md)-apparaten.  
