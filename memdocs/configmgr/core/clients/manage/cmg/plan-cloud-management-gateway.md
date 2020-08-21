---
title: Een cloudbeheergateway plannen
titleSuffix: Configuration Manager
description: Plan en ontwerp de Cloud beheer gateway (CMG) om het beheer van clients op internet te vereenvoudigen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d5b9a65b768d02d02084d778fd36255341a808b2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692839"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Het plannen van de Cloud beheer gateway in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1101764-->
De Cloud Management Gateway (CMG) biedt een eenvoudige manier om Configuration Manager-clients op internet te beheren. Door de CMG te implementeren als een Cloud service in Microsoft Azure, kunt u traditionele clients beheren die op Internet zwerven zonder extra on-premises infra structuur. U hoeft uw on-premises infra structuur ook niet zichtbaar te maken op internet.

> [!NOTE]
> Configuration Manager schakelt deze optionele functie standaard niet in. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../../servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Nadat de vereisten zijn ingesteld, bestaat het maken van de CMG uit de volgende drie stappen in de Configuration Manager-console:

1. Implementeer de CMG-Cloud service in Azure.
2. Voeg de rol CMG-verbindings punt toe.
3. Configureer de site-en site rollen voor de service.
Zodra clients eenmaal zijn geïmplementeerd en geconfigureerd, kunnen ze naadloos toegang krijgen tot on-premises site rollen, ongeacht of ze zich op het intranet of Internet bevinden.

Dit artikel bevat de basis kennis voor meer informatie over het CMG, het ontwerpen van de implementatie van de app in uw omgeving en het plannen van de uitvoering.

## <a name="scenarios"></a>Scenario's

Er zijn verschillende scenario's waarvoor een CMG nuttig is. De volgende scenario's zijn een aantal van de meest voorkomende:  

- Traditionele Windows-clients beheren met Active Directory identiteit die lid is van een domein. Deze clients bevatten Windows 8,1 en Windows 10. Het gebruikt PKI-certificaten om het communicatie kanaal te beveiligen. Beheer activiteiten zijn onder andere:  

  - Software-updates en Endpoint Protection
  - Status van inventarisatie en client
  - Instellingen voor naleving
  - Software distributie naar het apparaat
  - Taken reeks Windows 10 in-place upgrade

- Traditionele Windows 10-clients beheren met moderne identiteit, ofwel hybride of zuivere Cloud domein, gekoppeld aan Azure Active Directory (Azure AD). Clients gebruiken Azure AD voor de verificatie in plaats van PKI-certificaten. Het gebruik van Azure AD is eenvoudiger om meer complexe PKI-systemen in te stellen, te configureren en te onderhouden. Beheer activiteiten zijn hetzelfde als het eerste scenario, evenals:  

  - Software distributie naar de gebruiker  

- Installeer de Configuration Manager-client op Windows 10-apparaten via internet. Met behulp van Azure AD kan het apparaat worden geverifieerd bij de CMG voor registratie en toewijzing van de client. U kunt de client hand matig installeren of een andere methode voor software distributie gebruiken, zoals Microsoft Intune.  

- Nieuwe apparaten inrichten met co-beheer. Bij het automatisch inschrijven van bestaande clients is CMG niet vereist voor co-beheer. Het is vereist voor nieuwe apparaten met Windows auto pilot, Azure AD, Microsoft Intune en Configuration Manager. Zie [paden naar co-beheer](../../../../comanage/quickstart-paths.md)voor meer informatie.

### <a name="specific-use-cases"></a>Specifieke use cases

In deze scenario's kunnen de volgende specifieke gebruiks voorbeelden van apparaten van toepassing zijn:

- Zwervende apparaten, zoals laptops  

- Externe/filiaal apparaten die minder kostbaar en efficiënter zijn om te beheren via internet dan via een WAN of via een VPN.  

- Fusies en acquisities, waar het eenvoudig is om apparaten te koppelen aan Azure AD en te beheren via een CMG.  

- Clients voor werk groep. Voor deze apparaten is mogelijk aanvullende configuratie vereist, zoals certificaten.<!-- SCCMDocs#1925 -->

    Vanaf versie 2002 ondersteunt Configuration Manager verificatie op basis van tokens, wat kan helpen bij het beheer van clients voor externe werk groepen. Zie [verificatie op basis van tokens voor CMG](../../deploy/deploy-clients-cmg-token.md)voor meer informatie.

> [!Important]
> Standaard ontvangen alle clients beleid voor een CMG en gaan ze gebruiken wanneer ze op internet worden gebaseerd. Afhankelijk van het scenario en de use-case die van toepassing zijn op uw organisatie, moet u mogelijk het bereik van het gebruik van de CMG. Zie de client instelling [clients inschakelen voor het gebruik van een Cloud beheer gateway](../../deploy/about-client-settings.md#enable-clients-to-use-a-cloud-management-gateway) voor meer informatie.

## <a name="topology-design"></a>Topologie ontwerp

### <a name="cmg-components"></a>CMG-onderdelen

De implementatie en het gebruik van de CMG omvat de volgende onderdelen:  

- De **CMG-Cloud service** in azure verifieert en stuurt Configuration Manager client aanvragen naar het CMG-verbindings punt.  

- De site systeemrol **CMG-verbindings punt** maakt een consistente en snelle verbinding van het on-premises netwerk naar de CMG-service in azure mogelijk. Er worden ook instellingen gepubliceerd naar de CMG, met inbegrip van verbindings gegevens en beveiligings instellingen. Het CMG-verbindings punt stuurt client aanvragen van de CMG door naar on-premises rollen volgens URL-toewijzingen.

- De site systeemrol [**service aansluitpunt**](../../../servers/deploy/configure/about-the-service-connection-point.md) voert het onderdeel Cloud Service Manager uit, dat alle CMG-implementatie taken verwerkt. Daarnaast worden service status-en logboek gegevens vanuit Azure AD gecontroleerd en gerapporteerd. Zorg ervoor dat uw service verbindings punt zich in de [online modus](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)bevindt.  

- De client aanvragen van de site systeemrol van het **beheer punt** per normaal.

- De site systeemrol Services-client aanvragen van het **Software-update punt** per normaal.

    > [!NOTE]
    > Aanpassings richtlijnen voor beheer punten en software-update punten worden niet gewijzigd of ze on-premises of op internet gebaseerde clients onderhouden. Zie [grootte en schaal getallen](../../../plan-design/configs/size-and-scale-numbers.md#management-point)voor meer informatie.

- Op **Internet gebaseerde clients** maken verbinding met de CMG om toegang te krijgen tot on-premises Configuration Manager onderdelen.

- De CMG gebruikt een **op certificaten gebaseerde https** -webservice om de netwerk communicatie met clients te beveiligen.  

- Op internet gebaseerde clients gebruiken **PKI-certificaten of Azure AD** voor identiteit en authenticatie.  

- Een [**Cloud distributiepunt**](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) biedt zo nodig inhoud aan internetclients op internet.  

  - Een CMG kan ook inhoud leveren aan clients. Deze functionaliteit vermindert de vereiste certificaten en kosten van virtuele Azure-machines. Zie [een CMG wijzigen](setup-cloud-management-gateway.md#modify-a-cmg)voor meer informatie.<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
Maak de CMG met behulp van een **Azure Resource Manager-implementatie**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is een modern platform voor het beheren van alle oplossings resources als één entiteit, een zogenaamde [resource groep](/azure/azure-resource-manager/resource-group-overview#resource-groups). Bij het implementeren van CMG met Azure Resource Manager gebruikt de site Azure Active Directory (Azure AD) om de benodigde cloud resources te verifiëren en te maken. Het klassieke Azure-beheer certificaat is niet vereist voor deze moderne implementatie.  

> [!NOTE]
> Deze mogelijkheid biedt geen ondersteuning voor Azure Cloud service providers (CSP). De CMG-implementatie met Azure Resource Manager blijft de klassieke Cloud service gebruiken, die niet wordt ondersteund door de CSP. Zie [beschik bare Azure-Services in azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)voor meer informatie.

Vanaf Configuration Manager versie 1902 is Azure Resource Manager het enige implementatie mechanisme voor nieuwe exemplaren van de Cloud beheer gateway. Bestaande implementaties blijven werken.<!-- 3605704 -->

In Configuration Manager versie 1810 en eerder biedt de wizard CMG nog steeds de optie voor een **klassieke service-implementatie** met behulp van een Azure-beheer certificaat. Voor het vereenvoudigen van de implementatie en het beheer van resources, wordt het Azure Resource Manager-implementatie model aanbevolen voor alle nieuwe CMG-instanties. Implementeer, indien mogelijk, bestaande CMG-exemplaren opnieuw via Resource Manager. Zie [een CMG wijzigen](setup-cloud-management-gateway.md#modify-a-cmg)voor meer informatie.

> [!IMPORTANT]
> De klassieke service-implementatie in Azure is afgeschaft voor gebruik in Configuration Manager. Versie 1810 is de laatste ter ondersteuning van het maken van deze Azure-implementaties. Deze functionaliteit wordt in een toekomstige versie van Configuration Manager verwijderd.<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>Hiërarchie ontwerp

Maak het CMG op de site op het hoogste niveau van uw hiërarchie. Als dat een centrale beheer site is, maakt u vervolgens CMG-verbindings punten op onderliggende primaire sites. Het onderdeel Cloud Service Manager bevindt zich op het service aansluitpunt, dat zich ook op de centrale beheer site bevindt. Dit ontwerp kan de service delen op verschillende primaire sites, indien nodig.

U kunt meerdere CMG-Services maken in Azure en u kunt meerdere CMG-verbindings punten maken. Meerdere CMG-verbindings punten bieden taak verdeling van client verkeer van de CMG naar de on-premises rollen.

Vanaf versie 1902 kunt u een CMG koppelen aan een grens groep. Met deze configuratie kunnen clients standaard of terugvallen op de CMG voor client communicatie, afhankelijk van de [relaties tussen grens groepen](../../../servers/deploy/configure/boundary-groups.md). Dit gedrag is vooral nuttig in Branch-Office en VPN-scenario's. U kunt client verkeer door sturen naar dure en trage WAN-koppelingen om in plaats daarvan snellere services te gebruiken in Microsoft Azure.<!--3640932-->

Vanaf versie 2006 hebben intranet-clients toegang tot een CMG-software-update punt wanneer het wordt toegewezen aan een grens groep. Zie [grens groepen configureren](../../../servers/deploy/configure/boundary-groups.md#bkmk_cmg-sup)voor meer informatie. <!--7102873-->

> [!NOTE]
> Clients op Internet vallen niet in een grens groep.
>
> In Configuration Manager versie 1810 en eerder wordt de CMG niet in een grens groep ingedeeld.

Andere factoren, zoals het aantal te beheren clients, zijn ook van invloed op uw CMG-ontwerp. Zie [prestaties en schalen](#performance-and-scale)voor meer informatie.

#### <a name="example-1-standalone-primary-site"></a>Voor beeld 1: zelfstandige primaire site

Contoso heeft een zelfstandige primaire site in een on-premises Data Center op hun hoofd kantoor in New York City.

- Ze maken een CMG in de regio VS Oost Azure om de netwerk latentie te verminderen.
- Ze maken twee CMG-verbindings punten die beide zijn gekoppeld aan de single CMG-service.  

Wanneer clients op Internet zwerven, communiceren ze met de CMG in de regio VS Oost Azure. De CMG stuurt deze communicatie door via beide verbindings punten van CMG.

#### <a name="example-2-hierarchy"></a>Voor beeld 2: hiërarchie

Fourth Coffee heeft een centrale beheer site in een on-premises Data Center op hun hoofd kantoor in Seattle. Eén primaire site bevindt zich in hetzelfde Data Center en de andere primaire site bevindt zich in het hoofd-Europese kantoor van Parijs.

- Op de centrale beheer site maken ze een CMG-service in de regio vs West Azure. Ze schalen het aantal Vm's voor de verwachte belasting van zwervende clients in de gehele hiërarchie.
- Op de primaire site op Seattle maken ze een CMG-verbindings punt dat is gekoppeld aan één CMG.
- Op de primaire site op basis van Parijs maken ze een CMG-verbindings punt dat is gekoppeld aan één CMG.

Wanneer clients op Internet zwerven, communiceren ze met de CMG in de Azure-regio West. De CMG stuurt deze communicatie door naar het CMG-verbindings punt in de toegewezen primaire site van de client.

> [!TIP]
> U hoeft niet meer dan één Cloud beheer gateway te implementeren met het oog op geolocatie. De Configuration Manager-client is doorgaans niet van invloed op de geringe latentie die kan optreden bij de Cloud service, zelfs wanneer het geografisch uitvalt.

### <a name="test-environments"></a>Test omgevingen
<!-- SCCMDocs#1225 -->
Veel organisaties hebben afzonderlijke omgevingen voor productie, testen, ontwikkeling of kwaliteits bewaking. Houd bij het plannen van uw CMG-implementatie rekening met de volgende vragen:

- Hoeveel Azure AD-tenants heeft uw organisatie?
  - Is er een afzonderlijke Tenant voor het testen?
  - Zijn de id's van gebruikers en apparaten in dezelfde Tenant?

- Hoeveel abonnementen bevinden zich in elke Tenant?
  - Zijn er abonnementen die specifiek zijn voor het testen?

De Azure-service van Configuration Manager voor **Cloud beheer** ondersteunt meerdere tenants. Meerdere Configuration Manager-sites kunnen verbinding maken met dezelfde Tenant. Eén site kan meerdere CMG services implementeren in verschillende abonnementen. Meerdere sites kunnen CMG-services implementeren in hetzelfde abonnement. Configuration Manager biedt flexibiliteit, afhankelijk van uw omgeving en bedrijfs vereisten.

Zie de volgende veelgestelde vragen voor meer informatie: [de gebruikers accounts moeten zich in dezelfde Azure AD-Tenant bevinden als de Tenant die is gekoppeld aan het abonnement dat als host fungeert voor de CMG-Cloud service?](cloud-management-gateway-faq.md#bkmk_tenant)

## <a name="requirements"></a>Vereisten

- Een **Azure-abonnement** om de CMG te hosten.

    > [!IMPORTANT]
    > CMG biedt geen ondersteuning voor abonnementen met een Azure Cloud service provider (CSP).<!-- MEMDocs#320 -->

- Uw gebruikers account moet een **volledige beheerder** of **infrastructuur beheerder** zijn in Configuration Manager.<!-- SCCMDocs#2146 -->

- Een **Azure-beheerder** moet deel nemen aan het eerste maken van bepaalde onderdelen, afhankelijk van uw ontwerp. Deze persoon kan hetzelfde zijn als de Configuration Manager beheerder of afzonderlijk. Als dit afzonderlijk is, zijn er geen machtigingen vereist in Configuration Manager.

  - Als u de CMG wilt implementeren, hebt u een **abonnements eigenaar** nodig
  - Als u de site wilt integreren met Azure AD om de CMG te implementeren met behulp van Azure Resource Manager, hebt u een **globale beheerder** nodig

- Ten minste één on-premises Windows-Server voor het hosten van het **CMG-verbindings punt**. U kunt deze rol met andere Configuration Manager-site systeem rollen vinden.  

- Het **service verbindings punt** moet zich in de [online modus](../../../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes)bevindt.  

- Integratie met **Azure AD** voor het implementeren van de service met Azure Resource Manager. Zie [Azure-Services configureren](../../../servers/deploy/configure/azure-services-wizard.md)voor meer informatie.  

- Een [**Server verificatie certificaat**](certificates-for-cloud-management-gateway.md#bkmk_serverauth) voor de CMG.  

- **Andere certificaten** zijn mogelijk vereist, afhankelijk van de versie van het besturings systeem van de client en het verificatie model. Zie [CMG-certificaten](certificates-for-cloud-management-gateway.md)voor meer informatie.  

    Wanneer u de site optie gebruikt om door **Configuration Manager gegenereerde certificaten voor HTTP-site systemen te gebruiken**, kan het beheer punt http zijn. Zie [Enhanced http](../../../plan-design/hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie.

- In Configuration Manager versie 1810 of eerder, als u de klassieke Azure-implementatie methode gebruikt, moet u een [**Azure-beheer certificaat**](certificates-for-cloud-management-gateway.md#bkmk_azuremgmt)gebruiken.  

    > [!TIP]  
    > Gebruik het **Azure Resource Manager** -implementatie model. Dit beheer certificaat is niet vereist.
    >
    > De klassieke implementatie methode is afgeschaft vanaf versie 1810.  

- Clients moeten **IPv4**gebruiken.  

## <a name="specifications"></a>Specificaties

- Alle Windows-versies die worden vermeld in [ondersteunde besturings systemen voor clients en apparaten](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) , worden ondersteund voor CMG.  

- CMG ondersteunt alleen de rollen beheer punt en software-update punt.  

- CMG biedt geen ondersteuning voor clients die alleen communiceren met IPv6-adressen.<!--495606-->  

- Software-update punten die gebruikmaken van een netwerk load balancer werken niet met CMG. <!--505311-->  

- CMG-implementaties die gebruikmaken van het Azure-resource model, bieden geen ondersteuning voor Azure Cloud service providers (CSP). De CMG-implementatie met Azure Resource Manager blijft de klassieke Cloud service gebruiken, die niet wordt ondersteund door de CSP. Zie [Azure-Services die beschikbaar zijn in het Azure CSP-programma](/partner-center/azure-plan-available)voor meer informatie.

### <a name="support-for-configuration-manager-features"></a>Ondersteuning voor Configuration Manager-functies

De volgende tabel geeft een overzicht van de CMG-ondersteuning voor Configuration Manager-functies:

|Functie  |Ondersteuning  |
|---------|---------|
| Software-updates     | ![Ondersteund](media/green_check.png) |
| Endpoint Protection     | ![Ondersteunde ](media/green_check.png) <sup> [Opmerking &nbsp; 1](#bkmk_note1)</sup> |
| Hardware- en software-inventaris     | ![Ondersteund](media/green_check.png) |
| Client status en meldingen     | ![Ondersteund](media/green_check.png) |
| Scripts uitvoeren     | ![Ondersteund](media/green_check.png) |
| CMPivot     | ![Ondersteund](media/green_check.png) |
| Instellingen voor naleving     | ![Ondersteund](media/green_check.png) |
| Client installeren<br>(met [Azure AD-integratie](../../deploy/deploy-clients-cmg-azure.md)) | ![Ondersteund](media/green_check.png) |
| Client installeren<br>(met [token verificatie](../../deploy/deploy-clients-cmg-token.md)) | ![Ondersteund](media/green_check.png) (2002) |
| Software distributie (apparaat-doel)     | ![Ondersteund](media/green_check.png) |
| Software distributie (op de gebruiker gericht, vereist)<br>(met Azure AD-integratie)     | ![Ondersteund](media/green_check.png) |
| Software distributie (door de gebruiker gerichte, beschik bare)<br>([alle vereisten](../../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)) | ![Ondersteund](media/green_check.png) |
| [Taken reeks](../../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md) Windows 10 in-place upgrade | ![Ondersteund](media/green_check.png) |
| Taken reeks zonder opstart installatie kopie, geïmplementeerd met de optie om **alle inhoud lokaal te downloaden voordat de taken reeks wordt gestart** | ![Ondersteund](media/green_check.png) |
| Taken reeks zonder installatie kopie, geïmplementeerd met [een van beide download opties](../../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg) | ![Ondersteund](media/green_check.png) (1910) |
| Taken reeks met een opstart installatie kopie, gestart vanuit software Center | ![Ondersteund](media/green_check.png) (2006) |
| Een ander taken reeks scenario     | ![Niet ondersteund](media/Red_X.png) |
| Client-push     | ![Niet ondersteund](media/Red_X.png) |
| Automatische sitetoewijzing     | ![Niet ondersteund](media/Red_X.png) |
| Aanvragen voor software goedkeuring     | ![Niet ondersteund](media/Red_X.png) |
| Configuration Manager-console     | ![Niet ondersteund](media/Red_X.png) |
| Externe hulpprogramma's     | ![Niet ondersteund](media/Red_X.png) |
| Website voor rapporten     | ![Niet ondersteund](media/Red_X.png) |
| Wake on LAN     | ![Niet ondersteund](media/Red_X.png) |
| Mac-, Linux-en UNIX-clients     | ![Niet ondersteund](media/Red_X.png) |
| Peer-cache     | ![Niet ondersteund](media/Red_X.png) |
| On-premises MDM     | ![Niet ondersteund](media/Red_X.png) |
| BitLocker-beheer     | ![Niet ondersteund](media/Red_X.png) |

|Sleutel|
|--|
|![Ondersteund](media/green_check.png) = Deze functie wordt ondersteund met CMG door alle ondersteunde versies van Configuration Manager  |
|![Ondersteund ](media/green_check.png) (*YYMM*) = deze functie wordt ondersteund met CMG vanaf versie *YYMM* van Configuration Manager  |
|![Niet ondersteund](media/Red_X.png) = Deze functie wordt niet ondersteund met CMG |

#### <a name="note-1-support-for-endpoint-protection"></a><a name="bkmk_note1"></a> Opmerking 1: ondersteuning voor Endpoint Protection

Vanaf versie 2006 kunnen clients die via een CMG communiceren, direct Endpoint Protection-beleids regels Toep assen zonder een actieve verbinding met Active Directory.<!--4773948-->

<!-- 4350561 -->
In versie 2002 en eerder, voor apparaten die lid zijn van een domein om Endpoint Protection-beleid toe te passen, is toegang tot het domein vereist. Apparaten met niet-frequente toegang tot het interne netwerk kunnen vertragingen ondervinden bij het Toep assen van Endpoint Protection-beleid. Als u wilt dat apparaten het Endpoint Protection-beleid direct Toep assen nadat ze het hebben ontvangen, moet u rekening houden met een van de volgende opties:

- Werk de site en clients bij naar versie 2006.

- Gebruik co-beheer en schakel de [Endpoint Protection workload](../../../../comanage/workloads.md#endpoint-protection) naar intune en beheer [micro soft Defender anti virus](../../../../../intune/configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) vanuit de Cloud.

- Gebruik [configuratie-items](../../../../compliance/deploy-use/create-configuration-items.md) in plaats van de functie systeem eigen [antimalware policies](../../../../protect/deploy-use/endpoint-antimalware-policies.md) om Endpoint Protection-beleid toe te passen.


## <a name="cost"></a>Kosten

> [!IMPORTANT]  
> De volgende kosten informatie is alleen bedoeld voor de schatting. Uw omgeving kan andere variabelen hebben die van invloed zijn op de totale kosten van het gebruik van CMG.

CMG maakt gebruik van de volgende Azure-onderdelen, die kosten in rekening worden gebracht voor het account van het Azure-abonnement:

### <a name="virtual-machine"></a>Virtuele machine

- CMG maakt gebruik van Azure Cloud Services als platform as a Service (PaaS). Deze service maakt gebruik van virtuele machines (Vm's) die reken kosten oplopen.  

- CMG maakt gebruik van een standaard-a2 v2-VM.  

- U selecteert hoeveel VM-instanties de CMG ondersteunen. De enige is de standaard waarde, en 16 is het maximum. Dit aantal wordt ingesteld bij het maken van de CMG en kan later worden gewijzigd om de service naar behoefte te schalen.

- Zie [prestaties en schalen](#performance-and-scale)voor meer informatie over het aantal vm's dat u nodig hebt om uw clients te ondersteunen.

- Raadpleeg de [Azure-prijs calculator](https://azure.microsoft.com/pricing/calculator/) om mogelijke kosten te bepalen.

    > [!NOTE]  
    > De kosten van de virtuele machine variëren per regio.

### <a name="outbound-data-transfer"></a>Uitgaande gegevens overdracht

- Kosten zijn gebaseerd op gegevens die zijn afgelopen van Azure (uitgang of downloaden). Gegevens stromen in azure zijn gratis (binnenkomend of uploaden). CMG-gegevens stromen buiten Azure include-beleid naar de client, client meldingen en client reacties die door de CMG zijn doorgestuurd naar de site. Deze antwoorden zijn onder andere inventaris rapporten, status berichten en nalevings status.  

- Zelfs zonder clients die communiceren met een CMG, veroorzaakt een bepaalde achtergrond communicatie netwerk verkeer tussen de CMG en de on-premises site.  

- Bekijk de **uitgaande gegevens overdracht (GB)** in de Configuration Manager-console. Zie [clients controleren op CMG](monitor-clients-cloud-management-gateway.md)voor meer informatie.  

- Bekijk de [prijs informatie voor Azure-band breedte](https://azure.microsoft.com/pricing/details/bandwidth/) om mogelijke kosten te bepalen. De prijzen voor gegevens overdracht zijn trapsgewijs gelaagd. Hoe meer u gebruikt, hoe minder u per Gigabyte betaalt.  

- *Voor het schatten van de doel stellingen*, verwacht u ongeveer 100-300 MB per client per maand voor clients op internet. De lagere schatting is voor een standaard client configuratie. De bovenste schatting is voor een agressieve client configuratie. Het daad werkelijke gebruik kan variëren, afhankelijk van de configuratie van client instellingen.  

    > [!NOTE]  
    > Door andere acties uit te voeren, zoals het implementeren van software-updates of-toepassingen, wordt de hoeveelheid uitgaande gegevens overdracht van Azure verhoogd.

- Op internet gebaseerde clients ontvangen inhoud van de micro soft-software-update van Windows Update gratis. Distribueer geen update pakketten met inhoud van micro soft update naar een Cloud distributiepunt, anders kunt u kosten voor opslag en uitvoer van gegevens opleveren.  

- Onjuiste configuratie van de CMG-optie om het **intrekken van client certificaten te controleren** , kan extra verkeer van clients naar de CMG veroorzaken. Dit extra verkeer kan de Azure-uitvoerige gegevens verhogen, waardoor uw Azure-kosten kunnen worden verhoogd.<!-- SCCMDocs#1434 --> Zie voor meer informatie [de certificaatintrekkingslijst publiceren](security-and-privacy-for-cloud-management-gateway.md#bkmk_crl).  

### <a name="content-storage"></a>Inhouds opslag

- Op internet gebaseerde clients ontvangen inhoud van de micro soft-software-update van Windows Update gratis. Distribueer geen update pakketten met inhoud van micro soft update naar een Cloud distributiepunt, anders kunt u kosten voor opslag en uitvoer van gegevens opleveren.  

- Voor alle andere nood zakelijke inhoud, zoals toepassingen of software-updates van derden, moet u distribueren naar een Cloud distributiepunt. Op dit moment ondersteunt de CMG alleen het Cloud distributiepunt voor het verzenden van inhoud naar clients.
   - Wanneer u een CMG gebruikt voor de opslag van inhoud, worden de inhoud voor updates van derden niet gedownload naar clients als de instelling **Delta-inhoud downloaden wanneer de beschik bare** [client](../../deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is ingeschakeld. <!--6598587--> 

- Zie de kosten van het gebruik van [Cloud distributiepunten](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost)voor meer informatie.  

- Een CMG kan ook een Cloud distributiepunt zijn voor het leveren van inhoud aan clients. Deze functionaliteit vermindert de vereiste certificaten en kosten van virtuele Azure-machines. Zie [een CMG wijzigen](setup-cloud-management-gateway.md#modify-a-cmg)voor meer informatie.<!--1358651-->  

- CMG maakt gebruik van lokaal redundante opslag (LRS) van Azure. Zie [lokaal redundante opslag](/azure/storage/common/storage-redundancy-lrs)voor meer informatie.  

### <a name="other-costs"></a>Andere kosten

- Elke Cloud service heeft een dynamisch IP-adres. Elke afzonderlijke CMG maakt gebruik van een nieuw dynamisch IP-adres. Door extra Vm's per CMG toe te voegen, worden deze adressen niet verhoogd.  

## <a name="performance-and-scale"></a>Prestaties en schaal

Zie [grootte en schaal getallen](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)voor meer informatie over de schaal van CMG.

De volgende aanbevelingen kunnen u helpen de prestaties van CMG te verbeteren:

- De verbinding tussen de Configuration Manager-client en de CMG is geen regio-bewust. Client communicatie wordt grotendeels niet beïnvloed door latentie/geografische schei ding. Het is niet nodig om meerdere CMG te implementeren voor geografische nabijheid. Implementeer het CMG op de site op het hoogste niveau in uw hiërarchie en voeg instanties toe om de schaal te verg Roten.

- Voor een hoge Beschik baarheid van de service maakt u een CMG met ten minste twee CMG-instanties en twee CMG-verbindings punten per site.  

- Schaal de CMG om meer clients te ondersteunen door meer VM-instanties toe te voegen. De Azure-load balancer beheert client verbindingen met de service.  

- Maak meer CMG-verbindings punten om de belasting hiertussen te verdelen. De CMG distribueert het verkeer naar de gekoppelde CMG-verbindings punten op een Round-Robin manier.  

- Wanneer de CMG een hoge belasting heeft met meer dan het ondersteunde aantal clients, worden er nog steeds aanvragen verwerkt, maar er kan een vertraging optreden.  

> [!NOTE]
> Hoewel Configuration Manager geen vaste limiet heeft voor het aantal clients voor een CMG-verbindings punt, heeft Windows Server een standaard maximum voor TCP dynamisch poort bereik van 16.384. Als een Configuration Manager-site meer dan 16.384 clients met één CMG-verbindings punt beheert, moet u de limiet voor Windows Server verhogen. Alle clients onderhouden een kanaal voor client meldingen, waarbij een poort is geopend op het CMG-verbindings punt. Zie [Microsoft ondersteuning artikel 929851](https://support.microsoft.com/help/929851)voor meer informatie over het gebruik van de Netsh-opdracht om deze limiet te verg Roten.

## <a name="ports-and-data-flow"></a>Poorten en gegevens stroom

U hoeft geen binnenkomende poorten te openen voor uw on-premises netwerk. Het service aansluitpunt en het CMG-verbindings punt initiëren alle communicatie met Azure en de CMG. Deze twee site systeem rollen moeten uitgaande verbindingen maken met de micro soft-Cloud. Het service aansluitpunt implementeert en bewaakt de service in azure, dus moet de online modus zijn. Het CMG-verbindings punt maakt verbinding met de CMG om de communicatie tussen de CMG-en on-premises site systeem rollen te beheren.

Het volgende diagram is een eenvoudige, conceptuele gegevens stroom voor de CMG:

[![CMG-gegevens stroom](media/cmg-data-flow.png)](media/cmg-data-flow.png#lightbox)

1. Het service verbindings punt maakt verbinding met Azure via HTTPS-poort 443. Het wordt geverifieerd met behulp van Azure AD of het Azure-beheer certificaat. Het service verbindings punt implementeert de CMG in Azure. De CMG maakt de HTTPS-Cloud service met het certificaat voor Server verificatie.  

2. Het CMG-verbindings punt maakt verbinding met de CMG in azure via TCP-TLS of HTTPS. Het houdt de verbinding open en bouwt het kanaal voor toekomstige communicatie in twee richtingen.  

3. De client maakt verbinding met de CMG via HTTPS-poort 443. De verificatie wordt geverifieerd met behulp van Azure AD of het certificaat voor client verificatie.  

    > [!NOTE]
    > Als u de CMG inschakelt voor het leveren van inhoud of het gebruik van een Cloud distributiepunt, maakt de client rechtstreeks verbinding met Azure Blob Storage via HTTPS-poort 443. Zie [een cloud-gebaseerd distributie punt gebruiken](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow)voor meer informatie.<!-- SCCMDocs#2332 -->

4. De CMG stuurt de client communicatie via de bestaande verbinding naar het on-premises CMG-verbindings punt. U hoeft geen binnenkomende firewall poorten te openen.  

5. Het CMG-verbindings punt stuurt de client communicatie door naar het on-premises beheer punt en het software-update punt.  

Zie [een cloud-gebaseerd distributie punt gebruiken](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_dataflow)voor meer informatie over het hosten van inhoud in Azure.

### <a name="required-ports"></a>Vereiste poorten

Deze tabel geeft een lijst van de vereiste netwerk poorten en protocollen. De *client* is het apparaat waarmee de verbinding wordt gestart en waarvoor een uitgaande poort nodig is. De- *Server* is het apparaat dat de verbinding accepteert, waarbij een binnenkomende poort is vereist.

| Client | Protocol | Poort | Server | Beschrijving |
|--------|----------|------|--------|-------------|
| Serviceverbindingspunt | HTTPS | 443 | Azure | CMG-implementatie |
| CMG-verbindings punt | TCP-TLS | 10140-10155 | CMG-service | Voorkeurs protocol voor het maken van CMG-kanaal <sup> [Opmerking 1](#bkmk_port-note1)</sup> |
| CMG-verbindings punt | HTTPS | 443 | CMG-service | Terugval protocol voor het bouwen van een CMG-kanaal aan slechts één VM-instantie <sup> [Opmerking 2](#bkmk_port-note2)</sup> |
| CMG-verbindings punt | HTTPS | 10124-10139 | CMG-service | Terugval protocol voor het bouwen van een CMG-kanaal aan twee of meer VM-exemplaren <sup> [Opmerking 3](#bkmk_port-note3)</sup> |
| Client | HTTPS | 443 | CMG | Algemene client communicatie |
| Client | HTTPS | 443 | Blob Storage | Op de cloud gebaseerde inhoud downloaden |
| CMG-verbindings punt | HTTPS of HTTP | 443 of 80 | Beheerpunt | On-premises verkeer, poort is afhankelijk van de configuratie van het beheer punt |
| CMG-verbindings punt | HTTPS of HTTP | 443 of 80 | Software-updatepunt | On-premises verkeer, poort is afhankelijk van de configuratie van het software-update punt |

#### <a name="note-1-cmg-connection-point-tcp-tls-ports"></a><a name="bkmk_port-note1"></a> Opmerking 1: TCP-TLS-poorten van CMG-verbindings punt

Het CMG-verbindings punt probeert eerst een langdurige TCP-TLS-verbinding tot stand te brengen met elk CMG VM-exemplaar. Er wordt verbinding gemaakt met het eerste VM-exemplaar op poort 10140. De tweede VM-instantie gebruikt poort 10141, tot de 16de op poort 10155. Een TCP-TLS-verbinding voert het beste uit, maar biedt geen ondersteuning voor de Internet proxy. Als het CMG-verbindings punt geen verbinding kan maken via TCP-TLS, terugvallen op de HTTPS-<sup>[Opmerking 2](#bkmk_port-note2)</sup>.

#### <a name="note-2-cmg-connection-point-https-ports-for-one-vm"></a><a name="bkmk_port-note2"></a> Opmerking 2: HTTPS-poorten van CMG-verbindings punt voor één VM

Als het CMG-verbindings punt geen verbinding kan maken met de CMG via TCP-TLS-<sup>[Opmerking 1](#bkmk_port-note1)</sup>, wordt er verbinding gemaakt met het Azure-netwerk Load Balancer meer dan HTTPS 443 voor één VM-exemplaar.  

#### <a name="note-3-cmg-connection-point-https-ports-for-two-or-more-vms"></a><a name="bkmk_port-note3"></a> Opmerking 3: HTTPS-poorten van CMG-verbindings punt voor twee of meer virtuele machines

Als er twee of meer VM-exemplaren zijn, gebruikt het CMG-verbindings punt HTTPS 10124 naar de eerste VM-instantie, niet HTTPS 443. Er wordt verbinding gemaakt met het tweede VM-exemplaar op HTTPS 10125, tot de 16de op HTTPS-poort 10139.

### <a name="internet-access-requirements"></a>Vereisten voor internettoegang

Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u CMG-verbindings punt en service verbindings punt toestaan om toegang te krijgen tot internet-eind punten.

Zie [vereisten voor Internet toegang](../../../plan-design/network/internet-endpoints.md#bkmk_cloud)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- [Certificaten voor cloudbeheergateway](certificates-for-cloud-management-gateway.md)
- [Beveiliging en privacy voor cloudbeheergateway](security-and-privacy-for-cloud-management-gateway.md)
- [Grootte en schaal van de Cloud beheer gateway](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
- [Veelgestelde vragen over de Cloud beheer gateway](cloud-management-gateway-faq.md)
- [Een cloudbeheergateway instellen](setup-cloud-management-gateway.md)