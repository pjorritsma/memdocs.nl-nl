---
title: Ondersteunde clients en apparaten
titleSuffix: Configuration Manager
description: Meer informatie over de versies van het besturings systeem Configuration Manager worden ondersteund voor clients en apparaten.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e9e0ec6df5f80b318cb78ed8cddc986b613230e1
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904537"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Ondersteunde versies van besturings systemen voor clients en apparaten voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager ondersteunt het installeren van client software op Windows-en macOS-computers.  

## <a name="general-requirements-and-limitations"></a>Algemene vereisten en beperkingen

Bekijk de volgende vereisten en beperkingen voor alle clients:

- Het wijzigen van het opstart type of **Aanmelden als** instellingen voor een Configuration Manager-service wordt niet ondersteund. Deze wijziging kan verhinderen dat Key services correct worden uitgevoerd.

## <a name="windows-computers"></a>Windows-computers  

Als u de volgende versies van het Windows-besturings systeem wilt beheren, gebruikt u de-client die is opgenomen in Configuration Manager. Zie [clients implementeren op Windows-computers](../../clients/deploy/deploy-clients-to-windows-computers.md)voor meer informatie.  

### <a name="supported-client-os-versions"></a>Ondersteunde versies van client besturingssysteem

- **Windows 10**  

    Zie [ondersteuning voor Windows 10](support-for-windows-10.md)voor meer informatie.  

- **Windows 8,1** (x86, x64): Professional, Enter prise

#### <a name="windows-virtual-desktop"></a>Windows Virtual Desktop

<!--3556025-->
[Virtueel bureau blad van Windows](https://docs.microsoft.com/azure/virtual-desktop/) is een desktop-en app Virtualization-service die wordt uitgevoerd op Microsoft Azure. Vanaf versie 1906 gebruikt u Configuration Manager voor het beheren van deze virtuele apparaten waarop Windows wordt uitgevoerd in Azure.

Net als bij een Terminal Server, kunnen sommige van deze virtuele apparaten meerdere gelijktijdige actieve gebruikers sessies toestaan. Als u de client prestaties wilt helpen, schakelt Configuration Manager nu het gebruikers beleid uit op elk apparaat dat deze sessies met meerdere gebruikers mogelijk maakt. Zelfs als u gebruikers beleid inschakelt, schakelt de client deze standaard uit op deze apparaten, waaronder Windows 10 Enter prise-meerdere sessies en Terminal servers.

De client schakelt het gebruikers beleid alleen uit wanneer dit type apparaat wordt gedetecteerd tijdens een nieuwe installatie. Het vorige gedrag blijft bestaan voor een bestaande client van dit type die u bijwerkt naar deze versie. Op een bestaand apparaat wordt de instelling voor gebruikers beleid geconfigureerd, zelfs als deze detecteert dat het apparaat meerdere gebruikers sessies toestaat.

Als u in dit scenario gebruikers beleid nodig hebt en mogelijke prestatie problemen wilt accepteren, gebruikt u een van de volgende methoden om gebruikers beleid in te scha kelen:

- Gebruik [client instellingen](../../clients/deploy/configure-client-settings.md)In versie 1910 en hoger. Configureer in de **client beleids** groep de volgende instelling: **gebruikers beleid inschakelen voor meerdere gebruikers sessies**.<!-- 4737447 -->

- Gebruik in versie 1906 de Configuration Manager SDK met de [WMI-klasse SMS_PolicyAgentConfig-server](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md). Stel de nieuwe `PolicyEnableUserPolicyOnTS` eigenschap in op `true` .

> [!Note]  
> U kunt geen co-beheer gebruiken met een client met Windows 10 Enter prise multi-session. <!-- SCCMDocs-pr#3950 -->

### <a name="supported-server-os-versions"></a>Ondersteunde versies van het besturings systeem van de server

- **Windows Server 2019**: Standard, Data Center <sup> [notitie 1](#bkmk_note1)</sup>  
    (Vanaf Configuration Manager versie 1806.)

- **Windows Server 2016**: Standard, Data Center <sup> [notitie 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**: werk groep, standaard  

- **Windows Server 2012 R2** (x64): Standard, Data Center <sup> [notitie 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Data Center <sup> [notitie 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

De volgende versies verwijzen specifiek naar de Server Core-installatie van het besturings systeem. <sup>[Opmerking 3](#bkmk_note3)</sup>  

Windows Server Semi-Annual-kanaal versies zijn Server Core-installaties, zoals Windows Server, versie 1809. Als Configuration Manager-client worden ze ondersteund als de bijbehorende Windows 10 Semi-Annual-kanaal versie. Zie [ondersteuning voor Windows 10](support-for-windows-10.md)voor meer informatie.

- **Windows Server 2019** (x64) <sup> [Opmerking 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup> [Opmerking 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup> [Opmerking 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup> [Opmerking 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a>Opmerking 1

Configuration Manager tests en ondersteunt Windows Server Data Center Editions, maar is niet officieel gecertificeerd voor Windows Server. Configuration Manager hotfix-ondersteuning wordt niet aangeboden voor problemen die specifiek zijn voor Windows Server Data Center Edition. Zie [Windows Server Catalog](https://www.windowsservercatalog.com/)(Engelstalig) voor meer informatie over het Windows Server-certificerings programma.

#### <a name="note-2"></a><a name="bkmk_note2"></a>Opmerking 2

Als u [client push installatie](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)wilt ondersteunen, voegt u de bestands Server-service van de server functie bestands-en opslag Services toe. Zie [functies, functie Services en onderdelen installeren met behulp van Windows Power shell-cmdlets](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets)voor meer informatie over het installeren van Windows-onderdelen op Server Core.  

#### <a name="note-3"></a><a name="bkmk_note3"></a>Opmerking 3

De nieuwe software Center-app wordt niet ondersteund op een versie van Windows Server Core.<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Windows Embedded-computers  

Windows Embedded-apparaten beheren door de Configuration Manager-client op het apparaat te installeren. Zie [planning voor client implementatie op Windows Embedded-apparaten](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)voor meer informatie.  

### <a name="requirements-and-limitations"></a>Vereisten en beperkingen

- Alle client functies worden ondersteund op Windows Embedded-systemen waarvoor geen schrijf filters zijn ingeschakeld.  

- Clients die gebruikmaken van een van de volgende worden ondersteund voor alle functies behalve energie beheer:  

  - Verbeterde schrijf filters (EWF)

  - Op bestanden gebaseerde schrijf filters op basis van een RAM (FBWF)

  - Unified write filters (UWF)  

- De toepassings catalogus wordt niet ondersteund voor Windows Embedded-apparaten.  

### <a name="supported-os-versions"></a>Ondersteunde versies van besturings systemen  

- **Windows 10 Enter prise** (x86, x64)  

- **Windows 10 IOT Enter prise** (x86, x64)  
    Deze versie bevat het Long-term Servicing Channel (LTSC). Zie [overzicht van Windows 10 IOT Enter prise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise)(Engelstalig) voor meer informatie.<!--SCCMDocs issue 560-->  

- **Windows Embedded 8,1 Industry** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows THIN PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 met SP1** (x86, x64)

## <a name="windows-ce-computers"></a>Windows CE computers

Beheer Windows CE apparaten met de Configuration Manager verouderde client van mobiele apparaten die deel uitmaakt van Configuration Manager.  

### <a name="requirements-and-limitations"></a>Vereisten en beperkingen

- Voor de client voor mobiele apparaten is 0,78 MB aan opslag ruimte vereist voor de installatie. Aanmelden kan Maxi maal 256 KB aan extra opslag ruimte vereisen.

- De functies voor deze mobiele apparaten variëren per platform-en client type. Zie [een oplossing voor Apparaatbeheer kiezen](../choose-a-device-management-solution.md)voor meer informatie over welke beheer functies worden ondersteund.  

### <a name="supported-os-versions"></a>Ondersteunde versies van besturings systemen

- Windows CE 7,0 (ARM-en x86-processors)  

    > [!Note]
    > Ondersteuning is afgeschaft voor Windows CE 7,0 in Configuration Manager. Zie [verwijderde en afgeschafte items voor Configuration Manager-clients](../changes/deprecated/removed-and-deprecated-client.md)voor meer informatie.

#### <a name="supported-languages-include"></a>Ondersteunde talen zijn

- Chinees (vereenvoudigd en traditioneel)

- Engels (VS)

- Frans (Frankrijk)

- Duits

- Italiaans

- Japans  

- Koreaans  

- Portugees (Brazilië)  

- Russisch  

- Spaans (Spanje)  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a>Uitgebreide beveiligings updates en Configuration Manager

Het [ESU-programma (Extended Security updates)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) is een laatste redmiddel-optie voor klanten die bepaalde verouderde micro soft-producten na het einde van de ondersteuning moeten uitvoeren. Bijvoorbeeld Windows 7. Het bevat essentiële en/of belang rijke beveiligings updates (zoals gedefinieerd door het [micro soft Security Response Center (MSRC)](https://www.microsoft.com/msrc)) voor een maximum van drie jaar na het einde van de uitgebreide ondersteunings datum van het product.

Producten die niet langer zijn dan hun ondersteunings levenscyclus, worden niet ondersteund voor gebruik met Configuration Manager. Dit omvat alle producten die onder het ESU-programma vallen. Beveiligings updates die zijn uitgebracht onder het ESU-programma, worden gepubliceerd op Windows Server Update Services (WSUS). Deze updates worden weer gegeven in de Configuration Manager-console. Hoewel producten die onder het programma ESU vallen, niet langer worden ondersteund voor gebruik met Configuration Manager, kan de [meest recente versie van Configuration Manager current branch](../../servers/manage/updates.md#version-details) worden gebruikt voor het implementeren en installeren van Windows-beveiligings updates die zijn uitgebracht onder het programma. De nieuwste versie van de release kan ook worden gebruikt om Windows 10 te implementeren op apparaten met Windows 7.

Client beheer functies die geen verband houden met het beheer van software-updates of implementatie van het besturings systeem, worden niet meer getest op de besturings systemen die onder het ESU-programma vallen en wij garanderen niet dat ze blijven functioneren. Het wordt ten zeerste aanbevolen om de huidige versie van de besturings systemen zo snel mogelijk te upgraden of te migreren om client beheer ondersteuning te ontvangen.

## <a name="mac-computers"></a>Mac-computers  

Apple Mac-computers beheren met de Configuration Manager-client voor macOS.  

Het macOS-client installatie pakket wordt niet geleverd met de Configuration Manager media. Down load het vanuit het micro soft Download centrum, [micro soft Endpoint Configuration Manager-MacOS client (64-bits)](https://www.microsoft.com/download/details.aspx?id=100850).  

Zie [clients implementeren op Macs](../../clients/deploy/deploy-clients-to-macs.md)voor meer informatie.  

### <a name="requirements-and-limitations"></a>Vereisten en beperkingen

- Het installeren of uitvoeren van de Configuration Manager-client voor macOS op computers onder een ander account dan root wordt niet ondersteund. Dit kan ervoor zorgen dat Key Services niet goed kan worden uitgevoerd.  

### <a name="supported-versions"></a>Ondersteunde versies

- **MacOS Catalina (10,15)** (vereist Configuration Manager site versie 1910 of hoger en Configuration Manager client voor macOS versie 5.0.8742.1000 of hoger)

- **macOS Mojave (10,14)**

- **macOS High Sierra (10,13)**

## <a name="linux-and-unix-servers"></a>Linux-en UNIX-servers  

> [!Important]  
> Configuration Manager versie 1902 daalt ondersteuning voor Linux en UNIX als een-client. De afschaffing werd aangekondigd met [versie 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

De Linux-en UNIX-client installatie pakketten worden niet geleverd met de Configuration Manager media. Down load de **clients voor aanvullende besturings systemen** via het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=47719). Naast client installatie pakketten bevat de client Download het script waarmee de installatie van de client op elke computer wordt beheerd.  

### <a name="requirements-and-limitations"></a>Vereisten en beperkingen

- Zie [vereisten voor client implementatie op Linux-en UNIX-servers](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU)voor het controleren van afhankelijkheden van besturingssysteem bestanden voor de client voor Linux en UNIX.  

- Zie [clients implementeren op UNIX-en Linux-servers](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)voor een overzicht van ondersteunde beheer mogelijkheden voor Linux of UNIX.  

- Voor ondersteunde versies van Linux en UNIX bevat de vermelde versie alle volgende secundaire versies. CentOS versie 6 bevat bijvoorbeeld CentOS 6,3. Daarnaast bevat ondersteuning voor een besturings systeem dat gebruikmaakt van service packs (zoals SUSE Linux Enterprise Server 11 SP1) volgende service packs voor die versie van het besturings systeem.  

- Zie [clients implementeren op UNIX-en Linux-servers](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)voor meer informatie over client installatie pakketten en de universele agent.  

### <a name="supported-versions"></a>Ondersteunde versies

De volgende versies worden ondersteund door het aangegeven. tar-bestand te gebruiken.  

#### <a name="aix"></a>AIX  

|Versie|TAR-bestand|  
|-|-|  
|Versie 6,1 (voeding)|CCM-Aix61ppc. &lt; Build \> . tar|  
|Versie 7,1 (voeding)|CCM-Aix71ppc. &lt; Build \> . tar|  

#### <a name="centos"></a>CentOS  

|Versie|TAR-bestand|  
|-|-|  
|Versie 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="debian"></a>Debian  

|Versie|TAR-bestand|  
|-|-|  
|Versie 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 7 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 7 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 8 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 8 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="hp-ux"></a>HP-UX  

|Versie|TAR-bestand|  
|-|-|  
|Versie 11iv3 IA64|CCM-HpuxB. 11.31 i64. &lt; Build \> . tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Versie|TAR-bestand|  
|-|-|  
|Versie 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versie|TAR-bestand|  
|-|-|  
|Versie 5 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 5 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 6 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 6 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 7 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="solaris"></a>Sun  

|Versie|TAR-bestand|  
|-|-|  
|Versie 10 x86|CCM-Sol10x86. &lt; Build \> . tar|  
|Versie 10 SPARC|CCM-Sol10sparc. &lt; Build \> . tar|  
|Versie 11 x86|CCM-Sol11x86. &lt; Build \> . tar|  
|Versie 11 SPARC|CCM-Sol11sparc. &lt; Build \> . tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versie|TAR-bestand|  
|-|-|  
|Versie 10 SP1 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 10 SP1 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 11 SP1 x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 11 SP1 x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 12 x64|CCM-Universalx64. &lt; Build \> . tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Versie|TAR-bestand|  
|-|-|  
|Versie 10,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 10,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 12,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 12,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 14,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 14,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  
|Versie 16,04 LTS x86|CCM-Universalx86. &lt; Build \> . tar|  
|Versie 16,04 LTS x64|CCM-Universalx64. &lt; Build \> . tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a>On-premises MDM

Configuration Manager heeft ingebouwde mogelijkheden voor het beheren van mobiele apparaten die on-premises zijn, zonder client software te installeren. Zie [mobiele apparaten beheren met on-premises infra structuur](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)voor meer informatie.  

### <a name="supported-operating-systems"></a>Ondersteunde besturingssystemen

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enter prise** (x86, x64)  

- **Windows 10 IOT Enter prise** (x86, x64)  
    Deze versie bevat het Long-term Servicing Channel (LTSC). Zie [overzicht van Windows 10 IOT Enter prise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise)(Engelstalig) voor meer informatie.<!--SCCMDocs issue 560-->  

- **Windows 10 IoT Mobile Enterprise**  

- **Windows 10 team voor Surface Hub**  

- **Windows 10 Mobile**  

- **Windows 10 Mobile Enterprise**  

    > [!Note]
    > Ondersteuning is afgeschaft voor Windows 10 Mobile en Windows 10 Mobile Enter prise in Configuration Manager. Zie [verwijderde en afgeschafte items voor Configuration Manager-clients](../changes/deprecated/removed-and-deprecated-client.md)voor meer informatie.


## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a>Exchange Server-connector  

Configuration Manager ondersteunt beperkt beheer van apparaten die verbinding maken met uw Exchange-server zonder de Configuration Manager-client te installeren. Zie [mobiele apparaten beheren met Configuration Manager en Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)voor meer informatie.  

### <a name="supported-versions-of-exchange-server"></a>Ondersteunde versies van Exchange Server

- **Exchange Online (Office 365)**: deze versie bevat Business Productivity Online Standard Suite  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange server 2010 SP1** of **Exchange Server 2010 SP2**
