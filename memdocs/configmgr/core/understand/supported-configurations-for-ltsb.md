---
title: 'Ondersteunde configuraties voor de LTSB '
titleSuffix: Configuration Manager
description: Begrijp welke besturings systemen en afhankelijke producten werken met de lange termijn onderhouds vertakking van System Center Configuration Manager.
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7de7d562131f97ac21d1c394b176d3b7f4ce7747
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906440"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Ondersteunde configuraties voor de Long-term Servicing Branch van System Center Configuration Manager

*Van toepassing op: System Center Configuration Manager (onderhouds branche voor de lange termijn)*

Gebruik de informatie in dit onderwerp om te begrijpen welke besturings systemen en product afhankelijkheden worden ondersteund door de Long-term Servicing Branch (LTSB) van Configuration Manager.
Als anders vermeld in deze of de LTSB-specifieke onderwerpen, zijn dezelfde configuraties en beperkingen die van toepassing zijn op de Current Branch versie 1606 van toepassing op de LTSB.  Als er conflicten optreden, gebruikt u de informatie die van toepassing is op de editie die u gebruikt. Normaal gesp roken is de LTSB beperkter dan de Current Branch.

## <a name="general-statement-of-support"></a>Algemene ondersteunings verklaring
De volgende producten en technologieën worden ondersteund door deze vertakking van Configuration Manager. Hun insluiting in deze inhoud geeft echter geen uitbrei ding van ondersteuning voor een product of versie die de individuele ondersteunings levenscyclus van het product nakomt. Producten die niet langer zijn dan hun levens cyclus, worden niet ondersteund voor gebruik met Configuration Manager. Ga voor meer informatie naar de website van [Microsoft ondersteuning Lifecycle](https://support.microsoft.com/lifecycle) en lees de veelgestelde vragen over het Microsoft ondersteuning Lifecycle-beleid.

Producten en product versies die niet in de volgende onderwerpen worden vermeld, worden bovendien niet ondersteund, tenzij ze zijn aangekondigd op de [Enterprise Mobility + Security Blog](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/bg-p/enterprisemobilityandsecurity).

**Beperkingen voor toekomstige ondersteuning:** De LTSB heeft beperkte ondersteuning voor toekomstige server-en client besturingssystemen en product afhankelijkheden. De lijst met platforms voor de LTSB is vast voor de levens duur van de release:

**Windows:**
- Alleen kwaliteits-en beveiligings updates voor Windows worden ondersteund.
- Er is geen ondersteuning toegevoegd voor huidige branches (CB), Current branches for Business (CBB) of LTSB van Windows 10.
- Geen ondersteuning voor nieuwe primaire versies van Windows Server.

**SQL Server:**
- Alleen kwaliteits-en beveiligings updates, of kleine upgrades zoals service packs, worden ondersteund voor SQL Server.
- Geen ondersteuning voor nieuwe primaire versies van SQL Server.  

## <a name="site-systems-and-servers"></a>Site systemen en-servers
De LTSB ondersteunt het gebruik van de volgende Windows-computer besturingssystemen als-site systemen.  Elk besturings systeem heeft dezelfde vereisten en beperkingen als hetzelfde item in [ondersteunde besturings systemen voor site systeem servers](../plan-design/configs/supported-operating-systems-for-site-system-servers.md).  De Server Core-installatie van Windows 2012 R2 moet bijvoorbeeld een x64-versie zijn, wordt alleen ondersteund voor het hosten van een distributie punt en biedt geen ondersteuning voor PXE of multi cast.

**Ondersteunde besturings systemen:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Data Center
- Windows Server 2012 (x64): Standard, Data Center
- Windows 10 Enter prise 2015 LTSB (x86, x64)
- Windows 10 Enter prise 2016 LTSB (x86, x64)
- Windows 8,1 (x86, x64): Professional, Enter prise
- De Server Core-installatie van Windows Server 2012
- De Server Core-installatie van Windows Server 2012 R2

## <a name="client-management"></a>Clientbeheer
In de volgende secties worden de client besturingssystemen geïdentificeerd die u met de LTSB kunt beheren. De LTSB biedt geen ondersteuning voor het toevoegen van nieuwe besturings systemen als ondersteunde clients.

### <a name="windows-computers"></a>Windows-computers
U kunt de LTSB gebruiken om de volgende besturings systemen van Windows-computers te beheren met de Configuration Manager-client software die is opgenomen in Configuration Manager. Zie [clients implementeren op Windows-computers](../clients/deploy/deploy-clients-to-windows-computers.md)voor meer informatie.

**Ondersteunde besturings systemen:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Data Center (Opmerking 1)
- Windows Server 2012 (x64): Standard, Data Center (Opmerking 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows 10 Enter prise 2015 LTSB (x86, x64)
- Windows 10 Enter prise 2016 LTSB (x86, x64)
- Windows 8,1 (x86, x64): Professional, Enter prise
- De Server Core-installatie van Windows Server 2012 R2 (x64) (Opmerking 2)
- De Server Core-installatie van Windows Server 2012 (x64) (Opmerking 2)

**(Opmerking 1)** Data Center-releases worden ondersteund, maar niet gecertificeerd voor Configuration Manager.  
**(Opmerking 2)** Ter ondersteuning van client push installatie moet op de computer waarop deze besturingssysteem versie wordt uitgevoerd, de functie service Bestands server worden uitgevoerd voor de server functie bestands-en opslag Services. Zie [Server functies en-onderdelen installeren op een server core-server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574158(v=ws.11))voor meer informatie over het installeren van Windows-onderdelen op een server core-computer.

### <a name="windows-embedded"></a>Windows Embedded
U kunt de LTSB gebruiken om de volgende Windows Embedded-apparaten te beheren door de-client software op het apparaat te installeren.  Zie [planning voor client implementatie op Windows Embedded-apparaten](../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)voor meer informatie.

**Vereisten en beperkingen:**  

-   Alle client functies worden ondersteund op ondersteunde Windows Embedded-systemen waarvoor geen schrijf filters zijn ingeschakeld.  

-   Clients die gebruikmaken van een van de volgende worden ondersteund voor alle functies behalve energie beheer:  

    -   Verbeterde schrijf filters (EWF)    

    -   Op bestanden gebaseerde schrijf filters op basis van een RAM (FBWF)    

    -   Unified write filters (UWF)  

-   De toepassingscatalogus wordt niet ondersteund voor Windows Embedded-apparaten.  

-   Voordat u gedetecteerde malware op Windows Embedded-apparaten op basis van Windows XP kunt bewaken, moet u het micro soft Windows WMI-script pakket op het Inge sloten apparaat installeren. Gebruik Windows Embedded target Designer om dit pakket te installeren. De *WBEMDISP. DLL* en *WBEMDISP. TLB* -bestanden moeten bestaan en moeten worden geregistreerd in de map%windir%\System32\WBEM op het Inge sloten apparaat om ervoor te zorgen dat gedetecteerde malware wordt gerapporteerd.  

**Ondersteunde besturings systemen:**  
-   Windows 10 Enter prise 2016 LTSB (x86, x64)  
-   Windows 10 Enter prise 2015 LTSB (x86, x64)  
-   Windows Embedded 8,1 Industry (x86, x64)    
-   Windows Thin PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 met SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 U kunt Windows CE apparaten beheren met de Configuration Manager verouderde client van mobiele apparaten die deel uitmaakt van Configuration Manager.  

**Vereisten en beperkingen:**  

-   De client voor mobiele apparaten heeft 0,78 MB aan opslag ruimte nodig om de client te installeren. Een mobiel apparaat kan tot 256 KB aan extra opslag ruimte vereisen om u aan te melden.    

-   De functies voor deze mobiele apparaten variëren per platform-en client type. Zie voor meer informatie over het soort beheer functies dat Configuration Manager ondersteunt voor een verouderde client voor mobiele apparaten, [een oplossing voor het beheer van apparaten kiezen voor Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Ondersteunde besturings systemen:**  

-   Windows CE 7,0 (ARM-en x86-processors)  

**Enkele ondersteunde talen:**  
-   Chinees (vereenvoudigd en traditioneel)    
-   Engels (VS)    
-   Frans (Frankrijk)    
-   Duits    
-   Italiaans    
-   Japans  
-   Koreaans  
-   Portugees (Brazilië)  
-   Russisch  
-   Spaans (Spanje)  

### <a name="mac-computers"></a>Mac-computers  
 U kunt de LTSB gebruiken voor het beheren van Mac OS X-computers met de Configuration Manager-client voor Mac.

Het Mac-client installatie pakket wordt niet geleverd met de Configuration Manager media. U kunt deze downloaden als onderdeel van de down load ' clients voor aanvullende besturings systemen ' in het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=47719).  

Ondersteuning voor Mac-besturings systemen is beperkt tot de apparaten die worden vermeld in deze sectie. Ondersteuning biedt geen aanvullende besturings systemen die mogelijk worden ondersteund door een toekomstige update op Mac client installatie pakketten voor Current Branch.

Zie [clients implementeren op Macs](../clients/deploy/deploy-clients-to-macs.md)voor meer informatie.

**Ondersteunde versies:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Linux-en UNIX-servers
U kunt de LTSB gebruiken voor het beheren van Linux-en UNIX-servers met de Configuration Manager-client voor Linux en UNIX.

De Linux-en UNIX-client installatie pakketten worden niet geleverd met de Configuration Manager media. U kunt deze downloaden als onderdeel van de down load "clients voor aanvullende besturings systemen" in het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=47719). Naast de clientinstallatiepakketten bevat de clientdownload het installatie script waarmee de installatie van de client op elke computer wordt beheerd.

Ondersteuning voor Linux-en UNIX-besturings systemen is beperkt tot die in deze sectie. Ondersteuning omvat geen aanvullende besturings systemen die mogelijk worden ondersteund door een toekomstige update van Linux-en UNIX-client pakketten voor Current Branch.

**Vereisten en beperkingen:**  

-   Zie [vereisten voor client implementatie op Linux-en UNIX-servers](../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU)voor een overzicht van de afhankelijkheden van besturingssysteem bestanden voor de client voor Linux en UNIX.  
-   Zie [clients implementeren op UNIX-en Linux-servers](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)voor een overzicht van de beheer mogelijkheden die worden ondersteund voor computers met Linux of UNIX.  
-   Voor ondersteunde versies van Linux en UNIX bevat de vermelde versie alle volgende secundaire versies. Bijvoorbeeld, waar ondersteuning wordt aangegeven voor CentOS versie 6, bevat dit ook alle volgende secundaire versies van CentOS 6, zoals CentOS 6,3. Op dezelfde manier geldt dat als ondersteuning wordt vermeld voor een besturings systeem dat gebruikmaakt van service packs, zoals SUSE Linux Enterprise Server 11 SP1, de daaropvolgende service packs voor die versie van het besturings systeem.
-   Zie [clients implementeren op UNIX-en Linux-servers](../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)voor meer informatie over client installatie pakketten en de universele agent.


**Ondersteunde versies:**   
De volgende versies worden ondersteund door het aangegeven. tar-bestand te gebruiken.  
### <a name="aix"></a>AIX  

|Versie|File|  
|-|-|  
|Versie 5,3 (voeding)|CCM-Aix53ppc. &lt; Build \> . tar|  
|Versie 6,1 (voeding)|CCM-Aix61ppc. &lt; Build \> . tar|  
|Versie 7,1 (voeding)|CCM-Aix71ppc. &lt; Build \> . tar|  

### <a name="centos"></a>CentOS  

|Versie|File|  
|-|-|  
|Versie 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="debian"></a>Debian  

|Versie|File|    
|-|-|  
|Versie 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 6x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 7 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 7 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 8 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 8 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="hp-ux"></a>HP-UX  

|Versie|File|  
|-|-|  
|Versie 11iv2 IA64|CCM-HpuxB. 11.23 i64. &lt; Build \> . tar|  
|Versie 11iv2 PA-RISC|CCM-HpuxB. 11.23 PA. &lt; Build \> . tar|  
|Versie 11iv3 IA64|CCM-HpuxB. 11.31 i64. &lt; Build \> . tar|  
|Versie 11iv3 PA-RISC|CCM-HpuxB. 11.31 PA. &lt; Build \> . tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Versie|File|    
|-|-|  
|Versie 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versie|File|  
|-|-|  
|Versie 4 x86|CCM-RHEL4x86. &lt; Build \> . tar|  
|Versie 4 x64|CCM-RHEL4x64. &lt; Build \> . tar|  
|Versie 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="solaris"></a>Sun  

|Versie|File|   
|-|-|  
|Versie 9 SPARC|CCM-Sol9sparc. &lt; Build \> . tar|  
|Versie 10 x86|CCM-Sol10x86. &lt; Build \> . tar|  
|Versie 10 SPARC|CCM-Sol10sparc. &lt; Build \> . tar|  
|Versie 11 x86|CCM-Sol11x86. &lt; Build \> . tar|  
|Versie 11 SPARC|CCM-Sol11sparc. &lt; Build \> . tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versie|File|  
|-|-|  
|Versie 9 x86|CCM-SLES9x86. &lt; Build \> . tar|  
|Versie 10 SP1 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 10 SP1 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 11 SP1 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 11 SP1 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 12 x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="ubuntu"></a>Ubuntu  

|Versie|File|    
|-|-|  
|Versie 10,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 10,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 12,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 12,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 14,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 14,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  

### <a name="exchange-server-connector"></a>Exchange Server-connector
 De LTSB ondersteunt beperkt beheer van apparaten die verbinding maken met uw Exchange Server-exemplaar, zonder client software te installeren. Zie [mobiele apparaten beheren met Configuration Manager en Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)voor meer informatie.

 **Vereisten en beperkingen:**  

-   Configuration Manager biedt beperkt beheer voor mobiele apparaten. Beperkt beheer is beschikbaar wanneer u de apparaten met de Exchange Server-connector voor Exchange Active Sync (EAS) gebruikt die verbinding maken met een server met Exchange Server of Exchange Online.  

-   Zie voor meer informatie over de beheer functies die Configuration Manager ondersteunt voor mobiele apparaten die door de Exchange Server-connector worden beheerd, [een oplossing voor het beheer van apparaten kiezen voor Configuration Manager](../plan-design/choose-a-device-management-solution.md).  

**Ondersteunde versies van Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> De LTSB biedt geen ondersteuning voor het beheer van apparaten die verbinding maken via een online service, zoals Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Configuration Manager-console
De LTSB ondersteunt de volgende besturings systemen om de Configuration Manager-console uit te voeren. Elke computer die als host fungeert voor de-console moet mini maal .NET Framework versie 4.5.2 hebben, met uitzonde ring van Windows 10, waarvoor mini maal .NET Framework 4,6 is vereist.

**Ondersteunde besturings systemen:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Data Center
- Windows Server 2012 (x64): Standard, Data Center
- Windows 10 Enter prise 2016 LTSB (x86, x64)
- Windows 10 Enter prise 2015 LTSB (x86, x64)
- Windows 8,1 (x86, x64): Professional, Enter prise


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>SQL Server versies die worden ondersteund voor de site database en het rapportage punt
De LTSB ondersteunt de volgende versies van SQL Server voor het hosten van de site database en het rapportage punt. Voor elke ondersteunde versie gelden dezelfde configuratie vereisten en beperkingen die worden weer gegeven bij de [ondersteuning voor SQL Server versies](../plan-design/configs/support-for-sql-server-versions.md) voor de current branch van toepassing op de LTSB.  Dit omvat het gebruik van een SQL Server cluster of een SQL Server AlwaysOn-beschikbaarheids groep.  

**Ondersteunde versies:**

- SQL Server 2016: Standard, Enter prise
- SQL Server 2014 SP2: Standard, Enter prise
- SQL Server 2014 SP1: Standard, Enter prise
- SQL Server 2012 SP3: Standard, Enter prise
- SQL Server 2008 R2 SP3: Standard, Enter prise, Data Center
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Ondersteuning voor Active Directory-domeinen
Alle LTSB-site systemen moeten lid zijn van een ondersteund Windows Active Directory-domein. Ondersteuning voor Active Directory domeinen heeft dezelfde vereisten en beperkingen als [voor de ondersteuning voor Active Directory domeinen](../plan-design/configs/support-for-active-directory-domains.md), maar is beperkt tot de volgende domein functionaliteits niveaus:

**Ondersteunde niveaus:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Aanvullende ondersteunings onderwerpen die van toepassing zijn op de Long-term Servicing Branch
De informatie in de volgende Current Branch-onderwerpen is van toepassing op de LTSB:
- [Grootte en schaalgetallen](../plan-design/configs/size-and-scale-numbers.md)
- [Vereisten voor sites en sitesystemen](../plan-design/configs/site-and-site-system-prerequisites.md)
- [Opties voor hoge beschikbaarheid](../servers/deploy/configure/high-availability-options.md)
- [Aanbevolen hardware](../plan-design/configs/recommended-hardware.md)
- [Ondersteuning voor Windows-onderdelen en -netwerken](../plan-design/configs/support-for-windows-features-and-networks.md)
- [Ondersteuning voor virtualisatieomgevingen](../plan-design/configs/support-for-virtualization-environments.md)
