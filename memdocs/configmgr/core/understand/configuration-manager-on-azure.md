---
title: Configuration Manager in Azure
titleSuffix: Configuration Manager
description: Informatie over het gebruik van Configuration Manager in een Azure-omgeving.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c12372325573c6795396ff0832ca60cba68b8c29
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078495"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Configuration Manager op veelgestelde vragen over Azure

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met de volgende vragen en antwoorden krijgt u inzicht in het gebruik en het configureren van Configuration Manager op Microsoft Azure.

## <a name="general-questions"></a>Algemene vragen
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Mijn bedrijf probeert zo veel mogelijk fysieke servers te verplaatsen naar Microsoft Azure, kan ik Configuration Manager servers verplaatsen naar Azure?
Dit is zeker een ondersteund scenario.  Zie [ondersteuning voor de virtualisatie-omgevingen voor Configuration Manager](../plan-design/configs/support-for-virtualization-environments.md).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Goed gedaan. Mijn omgeving vereist meerdere sites. Moeten alle onderliggende primaire sites zich in azure bezien met de centrale beheer site of on-premises? Hoe zit het met secundaire sites?
Site-naar-site-communicatie (op basis van bestanden en database replicatie) is voor delen van de nabijheid van hosten in Azure. Alle client-gerelateerde verkeer zou echter extern van site servers en site systemen zijn. Als u een snelle en betrouw bare netwerk verbinding tussen Azure en uw intranet met een onbeperkt data-abonnement gebruikt, is het hosten van al uw infra structuur in azure een optie.

Als u echter een data-abonnement met data limiet of een beschik bare band breedte gebruikt, of als de netwerk verbinding tussen Azure en uw intranet niet snel is of onbetrouwbaar is, kunt u overwegen om specifieke sites (en site systemen) on-premises te plaatsen en vervolgens de besturings elementen voor band breedte te gebruiken die zijn ingebouwd in Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Heeft Configuration Manager in azure een SaaS-scenario (software als een service)?
Nee, het is een IaaS (Infrastructure as a Service), omdat u uw Configuration Manager infrastructuur servers in azure virtual machines host.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>Op welke gebieden moet ik aandacht schenken wanneer ik een overstap van mijn Configuration Manager-infra structuur naar Azure Overweeg?
Hier vindt u een goede vraag: Hier volgen de gebieden die het belangrijkst zijn bij het nemen van deze beslissing, die allemaal worden besproken in een afzonderlijke sectie van dit onderwerp.
1. Netwerken
2. Beschikbaarheid
3. Prestaties
4. Kosten
5. Gebruikerservaring

## <a name="networking"></a>Netwerken
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>Hoe zit het met de netwerk vereisten, moet ik ExpressRoute of een Azure VPN Gateway gebruiken?
Netwerken zijn een zeer belang rijke beslissing. Netwerk snelheden en latentie kunnen invloed hebben op de functionaliteit tussen de site server en de externe site systemen en eventuele client communicatie met de site systemen. Onze aanbeveling is om ExpressRoute te gebruiken. Maar er is geen beperking Configuration Manager om te voor komen dat u Azure VPN Gateway kunt gebruiken. U moet uw vereisten zorgvuldig door nemen (prestaties, patches, software distributie, implementatie van het besturings systeem) van deze infra structuur en vervolgens uw beslissing nemen. Hieronder vindt u enkele aandachtspunten voor elke oplossing:

- **ExpressRoute** (aanbevolen)
  - Natuurlijke uitbrei ding van uw Data Center (kan meerdere data centers koppelen)
  - Particuliere verbindingen tussen Azure-data centers en uw infra structuur
  - Gaat niet over het open bare Internet
  - Biedt betrouw baarheid, snelle snelheden, lagere latentie, hoge beveiliging
  - Biedt Maxi maal 10 Gbps snelheden en onbeperkte opties voor het gegevens abonnement
- **VPN Gateway**
  - Site-naar-site/punt-naar-site-Vpn's
  - Verkeer verloopt via het open bare Internet
  - Maakt gebruik van Internet Protocol Security (IPsec) en Internet Key Exchange (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute heeft een groot aantal verschillende opties, zoals onbeperkte mogelijkheden, verschillende snelheids opties en Premium-invoeg toepassingen. Welke moet ik kiezen?
De opties die u selecteert, zijn afhankelijk van het scenario dat u implementeert en de hoeveelheid gegevens die u wilt distribueren. De overdracht van Configuration Manager gegevens kan worden beheerd tussen site servers en distributie punten, maar de communicatie van de site server naar site server kan niet worden beheerd.   Wanneer u gebruikmaakt van een data-abonnement met data limiet, het plaatsen van specifieke sites (en site systemen) on-premises en het gebruik van de [ingebouwde bandbreedte regeling van Configuration Manager](../plan-design/hierarchy/fundamental-concepts-for-content-management.md) , kunt u de kosten van het gebruik van Azure helpen bepalen.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Hoe zit het met de installatie vereisten zoals Active Directory domeinen? Moet ik mijn site servers nog steeds toevoegen aan een Active Directory domein?
Ja. Wanneer u naar Azure gaat, blijven de [ondersteunde configuraties](../plan-design/configs/supported-configurations.md) hetzelfde, met inbegrip van Active Directory vereisten voor het installeren van Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Ik begrijp dat ik mijn site servers moet toevoegen aan een Active Directory domein, maar ik kan Azure Active Directory gebruiken?
Nee, Azure Active Directory wordt op dit moment niet ondersteund. De site servers moeten nog lid zijn van een [Windows Active Directory-domein](../plan-design/configs/support-for-active-directory-domains.md).



## <a name="availability"></a>Beschikbaarheid
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>Een van de redenen waarom ik een infra structuur naar Azure Verplaats, is de belofte van hoge Beschik baarheid. Kan ik profiteren van opties voor hoge Beschik baarheid, zoals beschikbaarheids sets van Azure-vm's voor virtuele machines die ik voor Configuration Manager moet gebruiken?
Ja. Beschikbaarheids sets van Azure-VM'S kunnen worden gebruikt voor redundante site systeem rollen zoals distributie punten of beheer punten.

U kunt ze ook gebruiken voor de Configuration Manager-site servers. Centrale beheer sites en primaire sites kunnen bijvoorbeeld allemaal in dezelfde beschikbaarheidsset staan, waarmee u ervoor kunt zorgen dat ze niet op hetzelfde moment opnieuw worden opgestart.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Hoe kan ik mijn data base Maxi maal beschikbaar maken? Kan ik Azure SQL Database gebruiken? Of moet ik Microsoft SQL Server gebruiken in een VM?
U moet Microsoft SQL Server in een VM gebruiken. Configuration Manager biedt geen ondersteuning voor Azure SQL Server op dit moment. Maar u kunt ook gebruikmaken van functies als AlwaysOn-beschikbaarheidsgroepen voor uw SQL-Server. [AlwaysOn-beschikbaarheidsgroepen](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) worden aanbevolen en worden officieel ondersteund vanaf versie 1602 van Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Kan ik Azure load balancers gebruiken met site systeem rollen, zoals beheer punten of software-update punten?
Hoewel Configuration Manager niet wordt getest met Azure load balancers, en als de functionaliteit transparant is voor de toepassing, mag deze geen nadelige gevolgen hebben voor normale bewerkingen.


## <a name="performance"></a>Prestaties
### <a name="what-factors-affect-performance-in-this-scenario"></a>Welke factoren zijn van invloed op de prestaties in dit scenario?
[Azure VM-grootte en-type](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs), virtuele Azure-schijven (Premium-opslag wordt aanbevolen, met name voor SQL Server), netwerk latentie en snelheid zijn de belangrijkste gebieden.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Vertel me meer over Azure virtual machines. welk formaat Vm's moet ik gebruiken?
In het algemeen moet uw reken kracht (CPU en geheugen) voldoen aan de [Aanbevolen hardware voor Configuration Manager](../plan-design/configs/recommended-hardware.md). Maar er zijn enkele verschillen tussen gewone computerhardware en Azure-Vm's, met name wanneer het gaat om de schijven die door deze Vm's worden gebruikt.  Welk formaat Vm's u gebruikt, is afhankelijk van de grootte van uw omgeving, maar hier volgen enkele aanbevelingen:
- Voor productie-implementaties met een aanzienlijke grootte raden we Azure-Vm's voor de klasse '**S**' aan. Dit komt doordat ze Premium Storage schijven kunnen gebruiken.  Niet-S-klasse-Vm's maken gebruik van Blob-opslag en in het algemeen voldoet niet aan de prestatie vereisten die nodig zijn voor een acceptabele productie-ervaring.
- Meerdere Premium Storage schijven moeten worden gebruikt voor een hogere schaal en striped in de Windows-schijf beheer console voor maximale IOPS.  
- U kunt het beste betere of meerdere Premium-schijven gebruiken tijdens de eerste site-implementatie (zoals P30 in plaats van P20 en 2xP30 in een striped volume in plaats van 1xP30). Als uw site later in de VM-grootte moet worden opgevolgd als gevolg van extra belasting, kunt u profiteren van de extra CPU en het geheugen die een grotere VM-grootte biedt. Er zijn ook schijven al aanwezig die kunnen profiteren van de extra IOPS-door Voer die de grotere VM-grootte toestaat.



In de volgende tabellen worden de eerste aanbevolen schijf aantallen weer geven voor het gebruik van primaire en centrale beheer sites voor diverse installaties:

**Site database met co-** locatie: primaire of centrale beheer site met de site database op de site server:

| Desktop-clients    |Aanbevolen VM-grootte|Aanbevolen schijven|
|--------------------|-------------------|-----------------|
|**Maxi maal 25k**       |   DS4_V2          |2xP30 (striped)  |
|**25k naar 50.000**      |   DS13_V2         |2xP30 (striped)  |
|**50.000 naar 100.000**     |   DS14_V2         |3xP30 (striped)  |


**Externe site-data base** -primaire of centrale beheer site met de site database op een externe server:

| Desktop-clients    |Aanbevolen VM-grootte|Aanbevolen schijven |
|--------------------|-------------------|------------------|
|**Maxi maal 25k**       | Site Server: F4S </br>Database server: DS12_V2 | Site Server: 1xP30 </br>Database server: 2xP30 (striped)  |
|**25k naar 50.000**      | Site Server: F4S </br>Database server: DS13_V2 | Site Server: 1xP30 </br>Database server: 2xP30 (striped)   |
|**50.000 naar 100.000**     | Site Server: F8S </br>Database server: DS14_V2 | Site Server: 2xP30 (striped)   </br>Database server: 3xP30 (striped)   |

Hieronder ziet u een voor beeld van een configuratie voor 50.000 naar 100.000-clients op DS14_V2 met 3xP30-schijven in een striped volume met afzonderlijke logische volumes voor de Configuration Manager ![installatie-en database bestanden: VM-schijven)](media/vm_disks.png)  



## <a name="user-experience"></a>Gebruikerservaring
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Waarom is de gebruikers ervaring een van de belangrijkste gebieden, waarom is dat?
De beslissingen die u hebt genomen voor netwerken, Beschik baarheid, prestaties en waar u uw Configuration Manager-site servers rechtstreeks van invloed kunnen zijn op uw gebruikers. We geloven dat een overstap naar Azure transparant moet zijn voor uw gebruikers, zodat ze geen wijziging ondervinden in hun dagelijkse interacties met Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>OK, dat klopt. Ik ben van plan om één zelfstandige primaire site te installeren op een virtuele machine van Azure en ik wil er zeker van zijn dat mijn kosten laag zijn. Moet ik (externe) site systemen (zoals beheer punten, distributie punten en software-update punten) op virtuele machines van Azure (ook wel on-premises) plaatsen?
Met uitzonde ring van de communicatie van de site server naar een distributie punt kunnen deze server-naar-server-communicatie op een site op elk gewenst moment plaatsvinden en geen gebruik maken van mechanismen om het gebruik van netwerk bandbreedte te beheren. Omdat u de communicatie tussen site systemen niet kunt beheren, moet u rekening houden met de kosten van deze communicatie.

Netwerk snelheden en latentie zijn ook andere factoren die u kunt overwegen. Trage of onbetrouwbare netwerken kunnen de functionaliteit beïnvloeden tussen de site server en de externe site systemen, evenals alle client communicatie met de site systemen. Het aantal beheerde clients dat gebruikmaakt van een bepaald site systeem en de functies die u actief gebruikt, moet ook worden overwogen.
Over het algemeen kunt u gebruikmaken van de normale richt lijnen die betrekking hebben op WAN-koppelingen en site systemen als uitgangs punt. In het ideale geval wordt de netwerk doorvoer die u selecteert en ontvangt tussen Azure en uw intranet consistent met een WAN dat goed is verbonden met een snel netwerk.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>Hoe zit het met inhouds distributie en inhouds beheer? Moeten standaard distributie punten zich in azure of on-premises bevindt, en moet ik BranchCache of pull-distributie punten on-premises gebruiken? Of moet ik exclusief gebruik maken van Cloud distributiepunten?
De benadering van inhouds beheer is veel hetzelfde als voor site servers en site systemen.
- Als u een snelle en betrouw bare netwerk verbinding tussen Azure en uw intranet met een onbeperkt data-abonnement gebruikt, kan het hosten van standaard distributie punten in azure een optie zijn.
- Als u gebruikmaakt van een data-abonnement met data limiet en de kosten voor de band breedte van belang zijn of de netwerk verbinding tussen Azure en uw intranet niet snel is of onbetrouwbaar is, kunt u rekening houden met andere benaderingen. Dit geldt ook voor het zoeken naar standaard-of pull-distributie punten op locatie en met behulp van BranchCache. Het gebruik van distributie punten in de Cloud is ook een optie, maar er zijn enkele beperkingen voor de ondersteunde inhouds typen (bijvoorbeeld, geen ondersteuning voor software-update pakketten).

> [!NOTE]
>  Als ondersteuning voor PXE of multi cast is vereist, moet u on-premises distributie punten (standaard of pull) gebruiken om te reageren op opstart aanvragen.


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Ik ben goed met de beperkingen van distributie punten in de Cloud, ik wil mijn beheer punt niet in een DMZ plaatsen, zelfs als dat nodig is voor de ondersteuning van mijn internet-gebaseerde clients. Heb ik andere opties?
Ja. Met de Configuration Manager versie 1610 is de [cloudbeheergateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) geïntroduceerd als een voorlopige functie. (Deze functie is voor het eerst gepubliceerd in de Technical Preview versie 1606 als de [Cloud proxy service](../get-started/capabilities-in-technical-preview-1606.md#cloud_proxy)).

De **cloudbeheergateway** biedt een eenvoudige manier om Configuration Manager-clients op het Internet te beheren. De service, die is geïmplementeerd voor Microsoft Azure en waarvoor een Azure-abonnement is vereist, maakt verbinding met uw on-premises Configuration Manager-infra structuur met behulp van een nieuwe functie genaamd het connector punt van de Cloud beheer gateway. Nadat de implementatie is geïmplementeerd en geconfigureerd, hebben clients toegang tot on-premises Configuration Manager site systeem rollen, ongeacht of ze zijn verbonden met het interne particuliere netwerk of via internet.

U kunt beginnen met het gebruik van de Cloud beheer gateway in uw omgeving en ons feedback geven om dit beter te maken. Zie [functies van voorlopige versies van updates gebruiken](../servers/manage/install-in-console-updates.md#bkmk_prerelease)voor meer informatie over de functies van de voorlopige versie.

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>Ik heb ook gehoord dat u een andere nieuwe functie met de naam peer-cache die is geïntroduceerd als een voorlopige functie in versie 1610. Verschilt van BranchCache? Welke moet ik kiezen?
Ja, geheel verschillend. [Peer-cache](../plan-design/hierarchy/client-peer-cache.md) is een 100% systeem eigen Configuration Manager technologie waarbij BranchCache een functie van Windows is. Beide kunnen nuttig zijn voor u. BranchCache gebruikt een broadcast om de vereiste inhoud te vinden, terwijl peer-cache gebruikmaakt van de normale distributie werk stroom en grens groeps instellingen van Configuration Manager.

U kunt elke client configureren als peer-cache bron. Wanneer beheer punten informatie over de locatie van inhouds bronnen verschaffen, geven ze gegevens over de distributie punten en alle peer-cache bronnen met de inhoud die de client nodig heeft.


## <a name="cost"></a>Kosten
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>Ik weet iets over de kosten. Is dit een kosteneffectieve oplossing voor mij?
Het is moeilijk om te zeggen omdat elke omgeving afwijkt. U kunt het beste uw omgeving kosten met behulp van Microsoft Azure prijs calculator:https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Aanvullende resources
**Fundamentals:**https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Azure VM-computer typen:**
- Grootte van Azure-machines:https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
- VM-prijzen:https://azure.microsoft.com/pricing/details/virtual-machines/  
- Prijzen voor opslag:https://azure.microsoft.com/pricing/details/storage/

**Overwegingen voor schijf prestaties:**    
- Intro Premium-schijf:https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
- Meer informatie over Premium-schijven:https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
- Handige verzameling grafieken voor maximale groottes en prestatie doelen voor opslag:https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
- Een andere intro + enige leuke uber-nerd-gegevens over de werking van Premium Storage achter de kaften:https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Availability**
- SLA voor Azure IaaS uptime:https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
- Uitleg over beschikbaarheids sets:https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Mogelijkheden**
- Express route versus Azure VPN:https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
- Prijzen voor Express route:https://azure.microsoft.com/pricing/details/expressroute/
- Meer informatie over Express route:https://azure.microsoft.com/documentation/articles/expressroute-introduction/
