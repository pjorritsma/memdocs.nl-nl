---
title: Cloud distributiepunt
titleSuffix: Configuration Manager
description: Plan en ontwerp voor het distribueren van software-inhoud via Microsoft Azure met Cloud distributiepunten in Configuration Manager.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52c2b70d2b094d5a89d80aafa61f1db67a53816f
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83987712"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Een Cloud distributiepunt gebruiken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> De implementatie voor het delen van inhoud van Azure is gewijzigd. Gebruik een Cloud beheer gateway die is ingeschakeld voor inhoud door de optie in te scha kelen om **CMG te laten functioneren als een Cloud distributiepunt en inhoud te bezorgen bij Azure Storage**. Zie [een CMG wijzigen](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg)voor meer informatie.
>
> U kunt in de toekomst geen traditioneel Cloud distributiepunt maken. Zie [verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.

Een Cloud distributiepunt is een Configuration Manager-distributie punt dat wordt gehost als platform-as-a-Service (PaaS) in Microsoft Azure. Deze service ondersteunt de volgende scenario's:  

- Software-inhoud bieden aan clients op internet zonder extra on-premises infra structuur  

- Uw inhouds distributiesysteem inschakelen in de Cloud  

- Verminder de nood zaak van traditionele distributie punten  

In dit artikel vindt u meer informatie over het Cloud distributiepunt, het plannen van het gebruik en het ontwerpen van uw implementatie. De sectie bevat de volgende secties:

- [Functies en voor delen](#bkmk_features)
- [Topologie ontwerp](#bkmk_topology)
- [Vereisten](#bkmk_requirements)
- [Specificaties](#bkmk_spec)
- [Kosten](#bkmk_cost)
- [Prestaties en schaal](#bkmk_perf)
- [Poorten en gegevens stroom](#bkmk_dataflow)
- [Certificaten](#bkmk_certs)
- [Veelgestelde vragen](#bkmk_faq)


## <a name="features-and-benefits"></a><a name="bkmk_features"></a>Functies en voor delen

### <a name="features"></a>Functies

Het Cloud distributiepunt ondersteunt diverse functies die ook worden aangeboden door on-premises distributie punten:  

- Cloud distributiepunten afzonderlijk of als leden van distributiepunt groepen beheren  

- Een Cloud distributiepunt gebruiken als locatie voor terugval inhoud  

- Ondersteunt zowel intranet-als op internet gebaseerde clients  

### <a name="benefits"></a>Voordelen

Het Cloud distributiepunt biedt de volgende extra voor delen:  

- De site versleutelt de inhoud voordat deze wordt verzonden naar het Cloud distributiepunt in Azure.  

- Om te voldoen aan de veranderende vereisten voor inhouds aanvragen door clients, schaalt u de Cloud service hand matig in Azure. Voor deze actie is het niet vereist dat u extra distributie punten installeert en inricht in Configuration Manager.  

- Ondersteunt het downloaden van inhoud van clients die zijn geconfigureerd voor andere inhouds technologieën, zoals Windows BranchCache en alternatieve inhouds providers.  

- Vanaf versie 1806 kunt u Cloud distributiepunten gebruiken als bron locaties voor pull-distributie punten.  


## <a name="topology-design"></a><a name="bkmk_topology"></a>Topologie ontwerp

De implementatie en het gebruik van het Cloud distributiepunt omvat de volgende onderdelen:  

- Een **Cloud service** in Azure. De site distribueert inhoud naar deze service, die deze opslaat in azure-Cloud opslag. Het beheer punt voorziet clients van deze inhouds locatie in de lijst met beschik bare bronnen als dat nodig is.  

- Een **beheer punt** site systeemrol client aanvragen per normaal.  

    - On-premises clients gebruiken meestal een on-premises beheer punt.  

    - Clients op Internet gebruiken een [Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)of een [beheer punt op Internet](../../clients/manage/plan-internet-based-client-management.md).  

- Het Cloud distributiepunt gebruikt een **op een certificaat gebaseerde https** -webservice om de netwerk communicatie met clients te beveiligen. Clients moeten dit certificaat vertrouwen.  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!--1322209-->
Maak vanaf versie 1806 een distributie punt in de Cloud met behulp van een **Azure Resource Manager-implementatie**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) is een modern platform voor het beheren van alle oplossings resources als één entiteit, een zogenaamde [resource groep](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Wanneer u een Cloud distributiepunt implementeert met Azure Resource Manager, gebruikt de site Azure Active Directory (Azure AD) om de benodigde cloud resources te verifiëren en te maken. Het klassieke Azure-beheer certificaat is niet vereist voor deze moderne implementatie.  

> [!Note]  
> Deze functie biedt geen ondersteuning voor Azure Cloud service providers (CSP). De implementatie van het Cloud distributiepunt met Azure Resource Manager blijft de klassieke Cloud service gebruiken, die niet wordt ondersteund door de CSP. Zie [beschik bare Azure-Services in azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)voor meer informatie.  

Vanaf Configuration Manager versie 1902 is Azure Resource Manager het enige implementatie mechanisme voor nieuwe exemplaren van het Cloud distributiepunt. Bestaande implementaties blijven werken.<!-- 3605704 -->

In Configuration Manager versie 1810 en eerder biedt de wizard Cloud distributiepunt nog steeds de optie voor een **klassieke service-implementatie** met behulp van een Azure-beheer certificaat. Gebruik het Azure Resource Manager implementatie model voor alle nieuwe Cloud distributiepunten om de implementatie en het beheer van resources te vereenvoudigen. Implementeer, indien mogelijk, bestaande Cloud distributiepunten opnieuw met behulp van Resource Manager.

> [!Important]  
> Vanaf versie 1810 is de implementatie van de klassieke service in azure afgeschaft voor gebruik in Configuration Manager. Deze versie is de laatste ter ondersteuning van het maken van deze Azure-implementaties. Deze functionaliteit wordt in een toekomstige versie van Configuration Manager verwijderd.<!--SCCMDocs-pr issue #2993-->  

Configuration Manager migreert geen bestaande klassieke Cloud distributiepunten naar het Azure Resource Manager-implementatie model. Nieuwe Cloud distributiepunten maken met Azure Resource Manager-implementaties en vervolgens klassieke Cloud distributiepunten verwijderen.

### <a name="hierarchy-design"></a>Hiërarchie ontwerp

Wanneer u het Cloud distributiepunt maakt, is afhankelijk van welke clients toegang moeten hebben tot de inhoud. Vanaf versie 1806 zijn er drie typen Cloud distributiepunten:  

- Azure Resource Manager implementatie: dit type maken op een primaire site of de centrale beheer site.  

- Implementatie van klassieke service: Maak dit type alleen op een primaire site.  

- De Cloud beheer gateway kan ook inhoud aan clients aanbieden. Deze functionaliteit vermindert de vereiste certificaten en kosten van virtuele Azure-machines. Zie voor meer informatie [plannen voor Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).<!--1358651-->  

Als u wilt bepalen of u Cloud distributiepunten in grens groepen wilt toevoegen, moet u rekening houden met het volgende gedrag:  

- Clients op Internet vertrouwen niet op grens groepen. Ze gebruiken alleen Internet gerichte distributie punten of Cloud distributiepunten. Als u alleen Cloud distributiepunten gebruikt voor het onderhouden van deze typen clients, hoeft u deze niet op te geven in grens groepen.  

- Als u wilt dat clients in uw interne netwerk een Cloud distributiepunt gebruiken, moet deze zich in dezelfde grens groep bevindt als de clients. Clients geven de voor keur aan de Cloud distributiepunten als laatste in hun lijst met inhouds bronnen, omdat er kosten zijn verbonden aan het downloaden van inhoud van Azure. Een Cloud distributiepunt wordt doorgaans gebruikt als een terugval bron voor clients op het intranet. Als u een ontwerp voor de Cloud wilt ontwerpen, ontwerpt u de grens groepen om aan deze zakelijke vereiste te voldoen. Zie [grens groepen configureren](../../servers/deploy/configure/boundary-groups.md)voor meer informatie.  

Hoewel u Cloud distributiepunten in specifieke regio's van Azure installeert, zijn clients niet op de hoogte van de Azure-regio's. Ze selecteren wille keurig een Cloud distributiepunt. Als u Cloud distributiepunten in meerdere regio's installeert en een client meer dan één in de lijst met inhouds locaties ontvangt, gebruikt de client mogelijk geen Cloud distributiepunt uit dezelfde Azure-regio.  

### <a name="backup-and-recovery"></a>Back-ups maken en herstellen  

Wanneer u een Cloud distributiepunt in uw hiërarchie gebruikt, gebruikt u de volgende informatie om u te helpen bij het plannen van back-ups en herstel:  

- Wanneer u de onderhouds taak van de **back-upserver voor site servers** gebruikt, bevat Configuration Manager automatisch de configuraties voor het Cloud distributiepunt.  

- Maak een back-up en sla een kopie van het Server verificatie certificaat op. Als u de klassieke service-implementatie in azure gebruikt, moet u ook een back-up maken en een kopie van het Azure-beheer certificaat opslaan. Wanneer u de Configuration Manager primaire site naar een andere server herstelt, moet u de certificaten opnieuw importeren.  


## <a name="requirements"></a><a name="bkmk_requirements"></a>Vereiste

- U hebt een **Azure-abonnement** nodig om de service te hosten.  

    - Een **Azure-beheerder** moet deel nemen aan het eerste maken van bepaalde onderdelen, afhankelijk van uw ontwerp. Voor deze persoon zijn geen machtigingen vereist in Configuration Manager.  

- De site server vereist **Internet toegang** om de Cloud service te implementeren en te beheren.  

- Wanneer u de implementatie methode **Azure Resource Manager** gebruikt, integreert u Configuration Manager met [Azure AD](../../servers/deploy/configure/azure-services-wizard.md) voor **Cloud beheer**. Azure AD- *gebruikers detectie* is niet vereist.  

- Een **certificaat voor Server verificatie**. Zie de sectie [certificaten](#bkmk_certs) hieronder voor meer informatie.  

    - Gebruik een open bare certificaat provider voor het Server verificatie certificaat om de complexiteit te verminderen. Wanneer u dit doet, moet u ook een **DNS CNAME-alias** voor clients hebben om de naam van de Cloud service op te lossen.  

- In Configuration Manager versie 1810 of eerder, als u de klassieke Azure-implementatie methode gebruikt, hebt u een **Azure-beheer certificaat**nodig. Zie de sectie [certificaten](#bkmk_certs) hieronder voor meer informatie.  

    > [!TIP]  
    > Met ingang van Configuration Manager versie 1806 gebruikt u het **Azure Resource Manager** -implementatie model. Dit beheer certificaat is niet vereist.  
    >
    > De klassieke implementatie methode is afgeschaft vanaf versie 1810.  

- Stel de client instelling in, **sta toegang tot Cloud distributiepunten**toe aan **Ja** in de groep **Cloud Services** . Deze waarde is standaard ingesteld op **Nee**.  

- Client apparaten hebben **Internet verbinding**nodig en moeten **IPv4**gebruiken.  


## <a name="specifications"></a><a name="bkmk_spec"></a>Specificatie

- Het Cloud distributiepunt ondersteunt alle Windows-versies die worden vermeld in [ondersteunde besturings systemen voor clients en apparaten](../configs/supported-operating-systems-for-clients-and-devices.md).  

- Een beheerder distribueert de volgende typen ondersteunde software-inhoud:  
  - Toepassingen
  - Pakketten
  - OS-upgrade pakketten
  - Software-updates van derden  

    > [!Important]  
    > - Hoewel de Configuration Manager-console de distributie van software-updates van micro soft niet blokkeert naar een Cloud distributiepunt, betaalt u Azure-kosten voor het opslaan van inhoud die clients niet gebruiken. Op internet gebaseerde clients ontvangen altijd inhoud van micro soft-software-updates van de Microsoft Update-Cloud service. Distribueer geen micro soft-software-updates naar een Cloud distributiepunt.
    > - Wanneer u een CMG gebruikt voor de opslag van inhoud, worden de inhoud voor updates van derden niet gedownload naar clients als de instelling **Delta-inhoud downloaden wanneer de beschik bare** [client](../../clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is ingeschakeld. <!--6598587--> 

- Vanaf versie 1806 configureert u een pull-distributie punt voor het gebruik van een Cloud distributiepunt als een bron. Zie [informatie over bron distributiepunten](use-a-pull-distribution-point.md#about-source-distribution-points)voor meer informatie.<!--1321554-->  

### <a name="deployment-settings"></a>Implementatie-instellingen

- **Down load de inhoud lokaal wanneer dit nodig is voor de taken reeks die wordt uitgevoerd**. Vanaf versie 1910 kan de engine van de taken reeks pakketten op aanvraag downloaden van een CMG of een Cloud distributiepunt. Deze wijziging biedt extra flexibiliteit met uw Windows 10-in-place upgrade implementaties op apparaten op internet.

- **Alle inhoud lokaal downloaden voordat de taken reeks wordt gestart**. In Configuration Manager versie 1906 en lager, werken andere opties, zoals **het lokaal downloaden van inhoud wanneer dit nodig is voor de taken reeks die wordt uitgevoerd** , niet in dit scenario. De taken reeks engine kan geen inhoud downloaden van een Cloud bron. De Configuration Manager-client moet de inhoud van de Cloud bron downloaden voordat de taken reeks wordt gestart. U kunt deze optie nog steeds gebruiken in versie 1910, indien nodig om aan uw vereisten te voldoen.

- Een Cloud distributiepunt biedt geen ondersteuning voor pakket implementaties met de optie om het **programma uit te voeren vanaf het distributie punt**. Gebruik de implementatie optie om **inhoud te downloaden vanaf een distributie punt en lokaal uit te voeren**.  

### <a name="limitations"></a>Beperkingen  

- U kunt geen Cloud distributiepunt gebruiken voor implementaties met PXE of multi cast.  

- Een Cloud distributiepunt biedt geen ondersteuning voor app-V-streaming-toepassingen.  

- U kunt [inhoud niet vooraf](manage-network-bandwidth.md#BKMK_PrestagingContent) plaatsen op een Cloud distributiepunt. De Distribution Manager van de primaire site die het Cloud distributiepunt beheert, verzendt alle inhoud.  

- U kunt een Cloud distributiepunt niet configureren als een pull-distributie punt.  


## <a name="cost"></a><a name="bkmk_cost"></a>Goedkope

<!--501018-->
> [!IMPORTANT]  
> De volgende kosten informatie is alleen bedoeld voor de schatting. Uw omgeving kan andere variabelen hebben die van invloed zijn op de totale kosten van het gebruik van een Cloud distributiepunt.  

Configuration Manager bevat de volgende opties om de kosten te helpen controleren en gegevens toegang te controleren:  

- De hoeveelheid inhoud die u in een Cloud service opslaat beheren en bewaken. Zie [Cloud distributiepunten bewaken](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor)voor meer informatie.  

- Configureer Configuration Manager om u te waarschuwen wanneer drempel waarden voor client downloads voldoen aan de maandelijkse limieten of overschrijden. Zie [drempel waarschuwingen voor gegevens overdracht](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_alerts)voor meer informatie.

- Om het aantal gegevens overdrachten van Cloud distributiepunten door clients te verminderen, gebruikt u een van de volgende peer-caching-technologieën:  
  - Peer-cache Configuration Manager
  - Windows BranchCache
  - Optimalisatie van Windows 10 Delivery  

    Zie [basis concepten voor inhouds beheer](fundamental-concepts-for-content-management.md)voor meer informatie.  

### <a name="components"></a>Onderdelen

Een Cloud distributiepunt maakt gebruik van de volgende Azure-onderdelen, die kosten in rekening worden gebracht voor het account van het Azure-abonnement:  

> [!Tip]  
> Vanaf versie 1806 kan de Cloud beheer gateway ook inhoud aan clients aanbieden. Deze functionaliteit vermindert de kosten door de Azure-Vm's samen te voegen. Zie [kosten voor Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#cost)voor meer informatie.  

#### <a name="virtual-machine"></a>Virtuele machine

- Het Cloud distributiepunt gebruikt Azure Cloud Services als platform as a Service (PaaS). Deze service maakt gebruik van virtuele machines (Vm's) die reken kosten oplopen.  

- Elke Cloud distributiepunt service gebruikt twee standaard a0-Vm's.  

- Raadpleeg de [Azure-prijs calculator](https://azure.microsoft.com/pricing/calculator/) om mogelijke kosten te bepalen.

    > [!NOTE]  
    > De kosten van de virtuele machine variëren per regio.

#### <a name="outbound-data-transfer"></a>Uitgaande gegevens overdracht

- Gegevens stromen in azure zijn gratis (binnenkomend of uploaden). Het distribueren van inhoud van de site naar het Cloud distributiepunt uploadt naar Azure.  

- Kosten zijn gebaseerd op gegevens die zijn afgelopen van Azure (uitgang of downloaden). Het Cloud distributiepunt gegevens stromen buiten Azure bestaat uit de software-inhoud die clients downloaden.  

- Zie [Cloud distributiepunten bewaken](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#bkmk_monitor)voor meer informatie.  

- Bekijk de [prijs informatie voor Azure-band breedte](https://azure.microsoft.com/pricing/details/bandwidth/) om mogelijke kosten te bepalen. De prijzen voor gegevens overdracht zijn trapsgewijs gelaagd. Hoe meer u gebruikt, hoe minder u per Gigabyte betaalt.  

#### <a name="content-storage"></a>Inhouds opslag

- Op internet gebaseerde clients kunnen inhoud van software-updates van micro soft downloaden van de Microsoft Update Cloud service gratis. Distribueer geen software-update-implementatie pakketten met micro soft-software-updates naar een Cloud distributiepunt. Anders worden er kosten in rekening gebracht voor de opslag van inhoud die clients nooit gebruiken.  

- Cloud distributiepunten gebruiken de volgende standaard-Blob-opslag, afhankelijk van het implementatie model:  

    - Een Azure Resource Manager-implementatie gebruikt Azure lokaal redundante opslag (LRS). Deze wijziging vermindert de kosten van het opslag account. De klassieke implementatie maakt geen gebruik van de aanvullende functies van GRS. Zie [lokaal redundante opslag](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs)voor meer informatie.  

    - Een klassieke implementatie met Configuration Manager versie 1810 of eerder maakt gebruik van Azure geo-redundante opslag (GRS). Zie [geo-redundante opslag](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs)voor meer informatie.  

#### <a name="other-costs"></a>Andere kosten

- Elke Cloud service heeft een dynamisch IP-adres. Elk afzonderlijk Cloud distributiepunt maakt gebruik van een nieuw dynamisch IP-adres. Door extra Vm's per Cloud service toe te voegen, worden deze adressen niet verhoogd.  


## <a name="ports-and-data-flow"></a><a name="bkmk_dataflow"></a>Poorten en gegevens stroom

Er zijn twee primaire gegevens stromen voor het Cloud distributiepunt:  

- De site server maakt verbinding met Azure om de Cloud distributiepunt service in te stellen  

- Een client maakt verbinding met het Cloud distributiepunt voor het downloaden van inhoud  

### <a name="site-server-to-azure"></a>Site server naar Azure

U hoeft geen binnenkomende poorten te openen voor uw on-premises netwerk. De site server initieert alle communicatie met Azure en het Cloud distributiepunt om de Cloud service te implementeren, bij te werken en te beheren. De site server moet uitgaande verbindingen maken met de micro soft-Cloud. Deze actie is gelijk aan het installeren van de sitesysteemrol van distributiepunt op een specifieke site.  

### <a name="client-to-cloud-distribution-point"></a>Client naar Cloud distributiepunt

U hoeft geen binnenkomende poorten te openen voor uw on-premises netwerk. Clients op Internet communiceren rechtstreeks met de Azure-service. Clients in uw interne netwerk die gebruikmaken van een Cloud distributiepunt moeten verbinding maken met de micro soft-Cloud.

Zie [content source Priority](fundamental-concepts-for-content-management.md#content-source-priority)(Engelstalig) voor meer informatie over de prioriteit van inhouds locaties en wanneer clients op intranet basis een Cloud distributiepunt gebruiken.

Wanneer een client een distributie punt in de Cloud gebruikt als een inhouds locatie:  

1. Het beheer punt geeft de client een toegangs token samen met de lijst met inhouds bronnen. Dit token is 24 uur geldig en geeft de client toegang tot het Cloud distributiepunt.  

2. Het beheer punt reageert op de locatie aanvraag van de client met de **service-FQDN** van het Cloud distributiepunt. Deze eigenschap is hetzelfde als de algemene naam van het Server verificatie certificaat.  

    Als u uw domein naam gebruikt, bijvoorbeeld WallaceFalls.contoso.com, probeert de client eerst deze FQDN op te lossen. U hebt een CNAME-alias nodig in de Internet gerichte DNS van uw domein voor clients voor het omzetten van de naam van de Azure-service, bijvoorbeeld: WallaceFalls.cloudapp.net.  

3. De client volgende verhelpt de naam van de Azure-service, bijvoorbeeld WallaceFalls.cloudapp.net, naar een geldig IP-adres. Dit antwoord moet worden verwerkt door de DNS van Azure.  

4. De client maakt verbinding met het Cloud distributiepunt. Met Azure Load wordt de verbinding met een van de VM-exemplaren gebalanceerd. De client verifieert zichzelf met behulp van het toegangs token.  

5. Het Cloud distributiepunt verifieert het toegangs token van de client en geeft de client de exacte inhouds locatie in azure Storage.  

6. Als de client het Server verificatie certificaat van het Cloud distributiepunt vertrouwt, maakt het verbinding met Azure Storage om de inhoud te downloaden.


## <a name="performance-and-scale"></a><a name="bkmk_perf"></a>Prestaties en schaal

<!--494872-->

Net als bij elk ontwerp van een distributie punt, moet u rekening houden met de volgende factoren:  

- Aantal gelijktijdige client verbindingen
- De grootte van de inhoud die clients downloaden
- De tijds duur die nodig is om te voldoen aan uw bedrijfs vereisten

Afhankelijk van het ontwerp van uw [topologie](#bkmk_topology), als clients de mogelijkheid hebben om meer dan één Cloud distributiepunt te hebben voor een bepaalde inhoud, kunnen ze natuurlijk wille keurig zijn in die Cloud Services. Als u slechts een bepaald inhouds fragment distribueert naar één Cloud distributiepunt en een groot aantal clients tegelijkertijd proberen deze inhoud te downloaden, wordt met deze activiteit een hogere belasting voor dat enkele Cloud distributiepunt. Het toevoegen van een extra Cloud distributiepunt omvat ook een afzonderlijke Azure Storage-service. Zie [poorten en gegevens stroom](#bkmk_dataflow)voor meer informatie over de manier waarop de client communiceert met de onderdelen van het Cloud distributiepunt en het downloaden van inhoud.  

Het Cloud distributiepunt gebruikt twee virtuele machines van Azure als front-end naar de Azure-opslag. Deze standaard implementatie voldoet aan de meeste behoeften van de klant. In sommige uitzonderlijke omstandigheden, met een groot aantal gelijktijdige client verbindingen (bijvoorbeeld 150.000-clients), kan de verwerkings capaciteit van de virtuele machines van Azure niet worden bewaard met de client aanvragen. U kunt de grootte van de virtuele Azure-machines die worden gebruikt voor het Cloud distributiepunt niet wijzigen. Hoewel u het aantal VM-exemplaren voor het Cloud distributiepunt in Configuration Manager niet kunt configureren, moet u, indien nodig, de Cloud service opnieuw configureren in de Azure Portal. Voeg hand matig meer VM-exemplaren toe of configureer de service zodanig dat deze automatisch wordt geschaald.

> [!Important]  
> Wanneer u Configuration Manager bijwerkt, implementeert de site de Cloud service opnieuw. Als u de Cloud service hand matig opnieuw configureert in de Azure Portal, wordt het aantal exemplaren opnieuw ingesteld op de standaard waarde van twee.  

De Azure Storage-service ondersteunt per seconde 500 aanvragen voor één bestand. Prestaties testen van één distributie punt in de cloud van een enkele 100-MB-bestand naar 50.000 clients in 24 uur.<!--512106-->  


## <a name="certificates"></a><a name="bkmk_certs"></a>Bewijzen  

Afhankelijk van het ontwerp van het Cloud distributiepunt hebt u een of meer digitale certificaten nodig.  

### <a name="general-information"></a>Algemene informatie

<!--SCCMDocs issue #779-->
Certificaten voor Cloud distributiepunten ondersteunen de volgende configuraties:  

- 4096-bits sleutel lengte

- Certificaten van versie 3. Zie voor meer informatie [overzicht CNG-certificaten](../network/cng-certificates-overview.md).  

- Vanaf versie 1802, wanneer u Windows configureert met het volgende beleid: **systeem cryptografie: gebruik FIPS-compatibele algoritmen voor versleuteling, hashing en ondertekening**  

- Vanaf versie 1802, ondersteuning voor TLS 1,2. Zie [technische documentatie voor cryptografische besturings elementen](../security/cryptographic-controls-technical-reference.md#about-ssl-vulnerabilities)voor meer informatie.  

### <a name="server-authentication-certificate"></a>Certificaat voor serverauthenticatie

*Dit certificaat is vereist voor alle implementaties van Cloud distributiepunt.*

Zie voor meer informatie [CMG Server-verificatie certificaat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_serverauth)en de volgende subsecties, indien nodig:  

- Vertrouwde basis certificaat CMG naar clients
- Certificaat voor Server verificatie dat is uitgegeven door de open bare provider
- Server verificatie certificaat dat is uitgegeven door Enter prise PKI

Het Cloud distributiepunt gebruikt dit type certificaat op dezelfde manier als de Cloud beheer gateway. Clients moeten dit certificaat ook vertrouwen. Om de complexiteit te verminderen, raadt micro soft aan een certificaat te gebruiken dat is uitgegeven door een open bare provider.

Tenzij u een certificaat met Joker tekens gebruikt, moet u hetzelfde certificaat niet opnieuw gebruiken. Voor elk exemplaar van het Cloud distributiepunt en de Cloud beheer gateway is een uniek server authenticatie certificaat vereist.

Zie [het service certificaat voor Cloud distributiepunten implementeren](../network/example-deployment-of-pki-certificates.md#BKMK_clouddp2008_cm2012)voor meer informatie over het maken van dit certificaat van een PKI.  

### <a name="azure-management-certificate"></a>Azure-beheer certificaat

*Dit certificaat is vereist voor klassieke service-implementaties. Het is niet vereist voor de implementatie van Azure Resource Manager.*

> [!Important]  
> Met ingang van Configuration Manager versie 1806 gebruikt u het **Azure Resource Manager** -implementatie model. Dit beheer certificaat is niet vereist.  
>
> De klassieke implementatie methode is afgeschaft vanaf versie 1810.  
>
> Vanaf Configuration Manager versie 1902 is Azure Resource Manager het enige implementatie mechanisme voor nieuwe exemplaren van het Cloud distributiepunt. Dit certificaat is niet vereist in Configuration Manager versie 1902 of hoger.<!-- 3605704 -->

Als u de klassieke Azure-implementatie methode met Configuration Manager versie 1810 of eerder gebruikt, hebt u een **Azure-beheer certificaat**nodig. Zie de sectie [Azure-beheer certificaat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_azuremgmt) in het artikel Cloud Management Gateway-certificaten voor meer informatie. De Configuration Manager-site server gebruikt dit certificaat om te verifiëren bij Azure om de klassieke implementatie te maken en te beheren.  

Gebruik hetzelfde Azure-beheer certificaat voor alle klassieke implementaties van Cloud distributiepunten en Cloud beheer gateways voor alle Azure-abonnementen en alle Configuration Manager-sites om de complexiteit te verminderen.


## <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a>Veelgestelde vragen

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Heeft een client een certificaat nodig om inhoud van een Cloud distributiepunt te downloaden?

Een certificaat voor client verificatie is niet vereist. De client moet het Server verificatie certificaat vertrouwen dat wordt gebruikt door het Cloud distributiepunt. Als dit certificaat is uitgegeven door een open bare certificaat provider, bevatten de meeste Windows-apparaten al vertrouwde basis certificaten voor deze providers. Als u een server verificatie certificaat van de PKI van uw organisatie hebt uitgegeven, moeten uw clients de uitgegeven certificaten in de hele keten vertrouwen. Deze keten bevat de basis certificerings instantie en alle tussenliggende certificerings instanties. Afhankelijk van uw PKI-ontwerp, kan dit certificaat een extra complexiteit van de implementatie van het Cloud distributiepunt veroorzaken. Om deze complexiteit te voor komen, raadt micro soft aan een open bare certificaat provider te gebruiken die uw klanten al vertrouwen.  

### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Kunnen mijn on-premises clients een Cloud distributiepunt gebruiken?

Ja. Als u wilt dat clients in uw interne netwerk een Cloud distributiepunt gebruiken, moet deze zich in dezelfde grens groep bevindt als de clients. Clients geven de voor keur aan de Cloud distributiepunten als laatste in hun lijst met inhouds bronnen, omdat er kosten zijn verbonden aan het downloaden van inhoud van Azure. Daarom wordt een Cloud distributiepunt meestal gebruikt als een terugval bron voor clients op het intranet. Als u een ontwerp voor de Cloud wilt ontwerpen, moet u de grens groepen dienovereenkomstig ontwerpen. Zie [grens groepen configureren](../../servers/deploy/configure/boundary-groups.md)voor meer informatie.  

### <a name="do-i-need-azure-expressroute"></a>Heb ik Azure ExpressRoute nodig?

Met [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) kunt u uw on-premises netwerk uitbreiden naar de micro soft-Cloud. ExpressRoute of andere dergelijke virtuele netwerk verbindingen zijn niet vereist voor het Configuration Manager Cloud distributiepunt.  

Als uw organisatie gebruikmaakt van ExpressRoute, isoleert u het Azure-abonnement voor het Cloud distributiepunt van het abonnement dat gebruikmaakt van ExpressRoute. Deze configuratie zorgt ervoor dat het Cloud distributiepunt niet per ongeluk verbonden is op deze manier.  

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Moet ik de virtuele machines van Azure onderhouden?

Er is geen onderhoud vereist. Het ontwerp van het Cloud distributiepunt maakt gebruik van Azure Platform as a Service (PaaS). Met het abonnement dat u opgeeft, maakt Configuration Manager de benodigde Vm's, opslag en netwerken. De virtuele machines worden beveiligd en bijgewerkt met Azure. Deze Vm's maken geen deel uit van uw on-premises omgeving, evenals het geval van een IaaS (Infrastructure as a Service). Het Cloud distributiepunt is een PaaS die uw Configuration Manager omgeving uitbreidt in de Cloud. Zie [beveiligings voordelen van een Paas-Cloud service model](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model)voor meer informatie.  

### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>Gebruikt het Cloud distributiepunt Azure CDN?

De Azure Content Delivery Network (CDN) is een wereld wijde oplossing voor het snel leveren van inhoud met een hoge band breedte door de inhoud op strategisch geplaatste fysieke knoop punten over de hele wereld in de cache op te plaatsen. Zie [Wat is Azure CDN?](https://docs.microsoft.com/azure/cdn/cdn-overview)voor meer informatie.

Het Configuration Manager Cloud distributiepunt biedt momenteel geen ondersteuning voor Azure CDN.


## <a name="next-steps"></a>Volgende stappen

[Cloud distributiepunten installeren](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)
