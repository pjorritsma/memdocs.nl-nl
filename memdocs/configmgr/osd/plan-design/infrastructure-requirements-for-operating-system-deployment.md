---
title: Vereisten voor OSD-infra structuur
titleSuffix: Configuration Manager
description: Meer informatie over de externe en product afhankelijkheden en vereisten voor de implementatie van besturings systemen in Configuration Manager
ms.date: 07/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9bb07bd2b82a9411bc527d04a9a64a0bb6e12f8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697667"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Vereisten voor de infra structuur voor de implementatie van besturings systemen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De besturingssysteem implementatie in Configuration Manager heeft externe afhankelijkheden en afhankelijkheden binnen het product. Gebruik dit artikel om u te helpen de infra structuur voor te bereiden voor implementatie van het besturings systeem.  

##  <a name="dependencies-external-to-configuration-manager"></a><a name="BKMK_ExternalDependencies"></a> Externe afhankelijkheden voor Configuration Manager  

Deze sectie bevat informatie over externe hulpprogram ma's, installatie kits en besturingssysteem versies die vereist zijn voor het implementeren van besturings systemen in Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK voor Windows 10  

De Windows Assessment and Deployment Kit (ADK) is een set hulpprogram ma's en documentatie die ondersteuning biedt voor de configuratie en implementatie van Windows. Configuration Manager maakt gebruik van Windows ADK om acties te automatiseren, zoals het installeren van Windows, het vastleggen van installatie kopieën en het migreren van gebruikers profielen en-gegevens.  

Raadpleeg voor meer informatie de volgende artikelen:  

- [Windows ADK voor Windows 10-scenario's voor IT-professionals](/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Download Windows ADK voor Windows 10](/windows-hardware/get-started/adk-install)  

    > [!IMPORTANT]
    > Zorg ervoor dat u de **Windows ADk voor Windows 10** en de **Windows PE-invoeg toepassing voor de ADk**downloadt.

- [Ondersteuning voor Windows 10](../../core/plan-design/configs/support-for-windows-10.md)  

#### <a name="site-systems"></a>Sitesystemen
Windows ADK is een vereiste voor de volgende site systeem servers:

- De site server van de site op het hoogste niveau in de hiërarchie  

- De site server van elke primaire site in de hiërarchie  

- Elk exemplaar van de SMS-provider  


> [!NOTE]  
> Installeer de Windows ADK hand matig op elke site server voordat u de Configuration Manager-site installeert.  

#### <a name="windows-adk-features"></a>Windows ADK-functies
Installeer de volgende functies van Windows ADK:  

-   Hulpprogramma voor migratie van gebruikersstatus (USMT)  

    > [!Note]  
    > USMT is niet vereist voor de SMS-provider.

-   Windows-hulpprogramma's  

-   Windows Voorinstallatieomgeving (Windows PE)  

    > [!Important]  
    > Vanaf Windows 10 versie 1809 is Windows PE een afzonderlijk installatie programma. Anders is er geen functioneel verschil.<!--SCCMDocs-pr issue 2908-->  

Zie [ondersteuning voor Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)voor een lijst met de versies van Windows 10 ADk die u met verschillende versies van Configuration Manager kunt gebruiken.


### <a name="user-state-migration-tool-usmt"></a>Hulpprogramma voor migratie van gebruikersstatus (USMT)  

Configuration Manager gebruikt een USMT-pakket dat de USMT 10-bron bestanden bevat om de gebruikers status vast te leggen en te herstellen als onderdeel van de implementatie van uw besturings systeem. Het USMT-pakket wordt automatisch gemaakt door Configuration Manager-installatie op de site op het hoogste niveau. USMT 10 legt de gebruikers status vast van Windows 7, Windows 8, Windows 8,1 en Windows 10.  

Raadpleeg voor meer informatie de volgende artikelen:  

- [Algemene migratiescenario's voor USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [De gebruikersstatus beheren](../get-started/manage-user-state.md)  


### <a name="windows-pe"></a>Windows PE  

Windows PE wordt gebruikt om een computer met een installatiekopie op te starten. Het is een Windows-versie met beperkte services die wordt gebruikt tijdens de pre-installatie en implementatie van Windows. De volgende lijst bevat de ondersteunde versies van Windows ADK voor Configuration Manager, current branch:  

#### <a name="windows-adk-version"></a>Windows ADK-versie  
Windows ADK voor Windows 10. Zie [ondersteuning voor Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)voor meer informatie.

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Windows PE-versies voor installatie kopieën die aanpasbaar zijn via de Configuration Manager-console  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Ondersteunde Windows PE-versies voor installatie kopieën die niet aanpasbaar zijn via de Configuration Manager-console  
Windows PE 3.1<sup>1</sup> en Windows PE 5  

<sup>1</sup> u kunt alleen een opstart installatie kopie toevoegen aan Configuration Manager wanneer deze is gebaseerd op Windows PE 3,1. Installeer Windows AIK Supplement voor Windows 7 SP1 om een upgrade van Windows AIK voor Windows 7 (gebaseerd op Windows PE 3) naar Windows AIK Supplement voor Windows 7 SP1 (gebaseerd op Windows PE 3.1) uit te voeren. Down load Windows AIK supplement voor Windows 7 SP1 via het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=5188).  

Wanneer u bijvoorbeeld Configuration Manager hebt, kunt u opstart installatie kopieën van Windows ADK voor Windows 10 (gebaseerd op Windows PE 10) aanpassen via de Configuration Manager-console. Hoewel installatie kopieën die zijn gebaseerd op Windows PE 5, echter worden ondersteund, moet u ze aanpassen vanaf een andere computer en de versie van DISM gebruiken die is geïnstalleerd met Windows ADK voor Windows 8. Voeg vervolgens de opstart installatie kopie toe aan de Configuration Manager-console. Zie [opstart installatie kopieën aanpassen](../get-started/customize-boot-images.md)voor meer informatie over de stappen voor het aanpassen van een installatie kopie (toevoegen van optionele componenten en stuur Programma's), het inschakelen van opdracht ondersteuning aan de opstart installatie kopie, het toevoegen van de installatie kopie aan de Configuration Manager-console en het bijwerken van distributie punten met de installatie kopie. Zie [Opstartinstallatiekopieën beheren met System Center Configuration Manager](../get-started/manage-boot-images.md) voor meer informatie over opstartinstallatiekopieën.  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

WSUS is vereist voor het software-update punt, dat vereist is voor het installeren van software-updates tijdens de implementatie van het besturings systeem. Zie een [Software-update punt configureren](../../sum/get-started/install-a-software-update-point.md)voor meer informatie.


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>IIS (Internet Information Services) op de sitesysteemservers  

IIS is vereist voor het distributie punt, het status migratie punt en het beheer punt. Zie voor meer informatie [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).  


### <a name="windows-deployment-services-wds"></a>Windows Deployment Services (WDS)  

In versie 1802 en eerder is WDS vereist voor PXE-implementaties. Vanaf versie 1806 kunt u PXE inschakelen op een distributie punt zonder WDS. Zie [Windows Deployment Services](#BKMK_WDS) in dit artikel voor meer informatie. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration Protocol (DHCP)  

DHCP is vereist voor PXE-implementaties. U moet een werkende DHCP-server hebben met een actieve host om besturingssystemen te implementeren door gebruik te maken van PXE. Zie [PXE gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie over PXE-implementaties.  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Ondersteunde besturingssystemen en vaste-schijfconfiguraties  

Zie [ondersteunde besturings systemen](#BKMK_SupportedOS) en [ondersteunde schijf configuraties](#BKMK_SupportedDiskConfig)voor meer informatie over de besturingssysteem versies en harde-schijf configuraties die door Configuration Manager worden ondersteund wanneer u besturings systemen implementeert.  


### <a name="windows-device-drivers"></a>Windows-apparaatstuurprogramma 's  

Windows-apparaatstuurprogramma's kunnen worden gebruikt wanneer u het besturings systeem installeert op de doel computer. Ze worden ook gebruikt wanneer u Windows PE in een opstart installatie kopie uitvoert. Zie [Stuur Programma's beheren](../get-started/manage-drivers.md)voor meer informatie.  



##  <a name="configuration-manager-dependencies"></a><a name="BKMK_InternalDependencies"></a> Configuration Manager afhankelijkheden  

Deze sectie bevat informatie over Configuration Manager vereisten voor de implementatie van besturings systemen.  


### <a name="os-image"></a>Installatie kopie van besturings systeem  

Installatie kopieën van besturings systemen in Configuration Manager worden opgeslagen in de WIM-bestands indeling (Windows Imaging). Ze vertegenwoordigen een gecomprimeerde verzameling referentie bestanden en-mappen. Deze installatie kopieën zijn vereist voor een geslaagde installatie en configuratie van een besturings systeem op een computer. Zie [installatie kopieën van besturings systemen beheren](../get-started/manage-operating-system-images.md)voor meer informatie.  


### <a name="driver-catalog"></a>Stuurprogrammacatalogus  

Als u een apparaatstuurprogramma wilt implementeren, moet u het apparaatstuurprogramma importeren, inschakelen en het beschikbaar maken op een distributie punt waartoe de Configuration Manager-client toegang heeft. Zie [Stuur Programma's beheren](../get-started/manage-drivers.md)voor meer informatie over de stuurprogrammacatalogus.  


### <a name="management-point"></a>Beheerpunt  

Beheer punten wisselen informatie over tussen clients en de Configuration Manager-site. De client gebruikt een beheer punt om de taken reeks uit te voeren voor het volt ooien van de implementatie van het besturings systeem. Zie [plannings overwegingen voor het automatiseren van taken](planning-considerations-for-automating-tasks.md)voor meer informatie over taken reeksen.  


### <a name="distribution-point"></a>Distributiepunt  

Distributie punten worden in de meeste implementaties gebruikt om de gegevens op te slaan die worden gebruikt voor het implementeren van een besturings systeem, zoals de installatie kopie of stuur programmapakketten. Met taken reeksen worden meestal gegevens opgehaald van een distributie punt om het besturings systeem te implementeren. Zie [inhoud en infra structuur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor inhoud beheren voor meer informatie over het installeren van distributie punten en het beheren van inhoud.  


### <a name="pxe-enabled-distribution-point"></a>Distributiepunt met PXE-functionaliteit  

Om PXE-geïnitieerde implementaties te implementeren, moet u een distributie punt configureren voor het accepteren van PXE-aanvragen van clients. Zie [Configure a Distribution Point (een distributie punt configureren](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)) voor meer informatie.


### <a name="multicast-enabled-distribution-point"></a>Multicast-distributiepunt  

Als u de implementaties van het besturings systeem wilt optimaliseren met behulp van multi cast, configureert u een distributie punt ter ondersteuning van multi cast. Zie [Configure a Distribution Point (een distributie punt configureren](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)) voor meer informatie.   


### <a name="state-migration-point"></a>Statusmigratiepunt  

Wanneer u gegevens over de gebruikers status vastlegt en herstelt voor gelijktijdige implementaties en voor het vernieuwen, kunt u een status migratie punt configureren om de gebruikers status gegevens op een andere computer op te slaan.  

Zie [Statusmigratiepunt](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)voor meer informatie over hoe het configureren van een statusmigratiepunt.  

Zie [gebruikers status beheren](../get-started/manage-user-state.md)voor meer informatie over het vastleggen en herstellen van de gebruikers status.  


### <a name="reporting-services-point"></a>Reporting Services-punt  

Als u Configuration Manager-rapporten wilt gebruiken voor implementaties van besturings systemen, moet u een rapportage punt installeren en configureren. Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.  


### <a name="security-permissions-for-os-deployments"></a>Beveiligings machtigingen voor besturingssysteem implementaties  

Het **besturings systeem Deployment Manager** beveiligingsrol is een ingebouwde rol die u niet kunt wijzigen. U kunt evenwel de rol kopiëren, wijzigingen maken en dan deze wijzigingen opslaan als een nieuwe aangepaste beveiligingsrol. Hier volgen enkele van de machtigingen die rechtstreeks van toepassing zijn op besturingssysteem implementaties:  

- **Installatiekopiepakket**: Maken, Verwijderen, Wijzigen, Map wijzigen, Object verplaatsen, Lezen, Beveiligingsbereik instellen  

- **Apparaatstuurprogramma's**: Maken, Verwijderen, Wijzigen, Map wijzigen, Rapport wijzigen, Object verplaatsen, Lezen, Rapport uitvoeren  

- **Stuurprogrammapakket**: Maken, Verwijderen, Wijzigen, Map wijzigen, Object verplaatsen, Lezen, Beveiligingsbereik instellen  

- **Installatiekopie van het besturingssysteem**: Maken, Verwijderen, Wijzigen, Map wijzigen, Object verplaatsen, Lezen, Beveiligingsbereik instellen  

- **Upgrade pakket voor het besturings systeem**: maken, verwijderen, wijzigen, map wijzigen, object verplaatsen, lezen, beveiligings bereik instellen  

- **Taakvolgordepakket**: Maken, Takenreeksmedia maken, Verwijderen, Wijzigen, Map wijzigen, Rapport wijzigen, Object verplaatsen, Lezen, Rapport uitvoeren, Veiligheidsbereik instellen  

Zie [aangepaste beveiligings rollen maken](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)voor meer informatie.  


### <a name="security-scopes-for-os-deployments"></a>Beveiligingsbereiken voor implementaties van besturings systemen  

Gebruik beveiligingsbereiken om gebruikers met beheerders rechten toegang te geven tot de Beveilig bare objecten die worden gebruikt in implementaties van besturings systemen, zoals besturings systeem-en opstart installatie kopieën, stuur programmapakketten en taken reeks pakketten. Zie [Beveiligingsbereiken](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)voor meer informatie.  



##  <a name="windows-deployment-services"></a><a name="BKMK_WDS"></a> Windows Deployment Services  

In versie 1802 en eerder, Windows Deployment Services (WDS) moet zijn geïnstalleerd op dezelfde server als de distributie punten die u configureert om PXE of multi cast te ondersteunen. WDS is opgenomen in het besturings systeem van de server. Voor PXE-implementaties is WDS de service die het opstarten van PXE uitvoert. Wanneer het distributie punt is geïnstalleerd en ingeschakeld voor PXE, wordt door Configuration Manager een provider in WDS geïnstalleerd die gebruikmaakt van de WDS PXE-opstart functies.  

Vanaf versie 1806 kunt u PXE inschakelen op een distributie punt zonder WDS. Zie de optie **een PXE-Responder inschakelen zonder Windows Deployment service** in [distributie punten installeren en configureren](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)voor meer informatie.


> [!NOTE]  
>  Als de server opnieuw moet worden opgestart, kan de installatie van WDS mislukken. 


### <a name="wds-requirements"></a>WDS-vereisten  

-   De WDS-installatie op de server vereist dat de beheerder lid is van de lokale groep Administrators.  

-   De WDS-server moet lid zijn van een Active Directory-domein of een domeinbeheerder voor een Active Directory-domein. Alle Windows-domein- en forestconfiguraties ondersteunen WDS.  

-   Als de provider is geïnstalleerd op een externe server, moet u WDS installeren op de site server en de externe provider.  


###  <a name="considerations-when-you-have-wds-and-dhcp-on-the-same-server"></a><a name="BKMK_WDSandDHCP"></a> Overwegingen wanneer u WDS en DHCP op dezelfde server hebt  

Als u van plan bent het distributie punt te hosten op een server waarop DHCP wordt uitgevoerd, moet u rekening houden met de volgende configuratie problemen:  

-   U moet beschikken over een werkende DHCP-server met een actief bereik. WDS maakt gebruik van PXE, waarvoor een DHCP-server vereist is.  

-   Er is een DNS-server vereist om WDS uit te voeren.  

-   De volgende UDP-poorten moeten geopend zijn op de WDS-server:  

    -   Poort 67 (DHCP)  

    -   Poort 69 (TFTP)  

    -   Poort 4011 (PXE)  

    > [!NOTE]  
    >  Als DHCP-autorisatie vereist is op de server, moet de DHCP-client poort 68 geopend zijn op de server.  

-   Voor DHCP en WDS is poort nummer 67 vereist. Als u WDS en DHCP co-host, kunt u DHCP of het distributie punt dat is geconfigureerd voor PXE, verplaatsen naar een afzonderlijke server. U kunt ook de volgende procedure gebruiken om de WDS-server te configureren om op een andere poort te Luis teren.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>De WDS-server zo configureren dat deze luistert op een andere poort  

1.  Wijzig de volgende registersleutel:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Stel de register waarde **UseDHCPPorts** in op **0**.  

3.  Voer de volgende opdracht uit op de server om de nieuwe configuratie van kracht te laten worden:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

> [!NOTE]
> In versie 1810 en lager wordt het niet ondersteund om de PXE-responder te gebruiken zonder WDS op servers waarop ook een DHCP-server wordt uitgevoerd.
>
> Vanaf versie 1902, wanneer u een PXE-responder inschakelt op een distributie punt zonder Windows Deployment-service, kan het zich nu op dezelfde server bevinden als de DHCP-service. Zie [Configure ten minste één distributie punt voor het accepteren van PXE-aanvragen](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure)voor meer informatie.


##  <a name="supported-operating-systems"></a><a name="BKMK_SupportedOS"></a> Ondersteunde besturings systemen  

Alle Windows-besturings systemen die worden vermeld als ondersteunde clients in [ondersteunde besturings systemen voor clients en apparaten](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) , worden ondersteund voor de implementatie van het besturings systeem.  



##  <a name="supported-disk-configurations"></a><a name="BKMK_SupportedDiskConfig"></a> Ondersteunde schijf configuraties  

De combi Naties van de harde-schijf configuratie op de referentie-en doel computers die worden ondersteund voor Configuration Manager besturingssysteem implementatie worden weer gegeven in de volgende tabel:  

|Harde-schijfconfiguratie van referentiecomputer|Harde-schijfconfiguratie van doelcomputer|  
|------------------------------------------------|--------------------------------------------------|  
|Standaardschijf|Standaardschijf|  
|Eenvoudig volume op een dynamische schijf|Eenvoudig volume op een dynamische schijf|  

Configuration Manager biedt alleen ondersteuning voor het vastleggen van een installatie kopie van een besturings systeem op computers die zijn geconfigureerd met eenvoudige volumes. Er wordt geen ondersteuning geboden voor de volgende harde-schijf configuraties:  

-   Spanned volumes  

-   Striped volumes (RAID 0)  

-   Gespiegelde volumes (RAID-1)  

-   Pariteitsvolumes (RAID-5)  

In de volgende tabel ziet u een aanvullende configuratie van de harde schijf op de referentie-en doel computers die niet worden ondersteund met Configuration Manager implementatie van het besturings systeem.  

|Harde-schijfconfiguratie van referentiecomputer|Harde-schijfconfiguratie van doelcomputer|  
|------------------------------------------------|--------------------------------------------------|  
|Standaardschijf|Dynamische schijf|  



## <a name="next-steps"></a>Volgende stappen

- [Sitesysteemrollen voor besturingssysteemimplementaties voorbereiden](../get-started/prepare-site-system-roles-for-operating-system-deployments.md)
- [Voorbereidingen voor besturingssysteemimplementatie](../get-started/prepare-for-operating-system-deployment.md)