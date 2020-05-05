---
title: Nieuwe versie 1802
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1802 van Configuration Manager.
ms.date: 10/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 11066470347db0f3ffbfadda9897aed92baa645b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073599"
---
# <a name="whats-new-in-version-1802-of-configuration-manager"></a>Wat is er nieuw in versie 1802 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1802 voor Configuration Manager current branch is beschikbaar als een update in de console. Deze update Toep assen op sites waarop versie 1702, 1706 of 1710 wordt uitgevoerd. <!-- baseline only statement: -->Wanneer u een nieuwe site installeert, is deze ook beschikbaar als basislijn versie.

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 1802](https://support.microsoft.com/help/4101375)voor meer informatie.

De volgende aanvullende updates voor deze versie zijn nu ook beschikbaar:
- [Update pakket voor Configuration Manager current branch, versie 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Als u een nieuwe site wilt installeren, moet u een basislijn versie van Configuration Manager gebruiken.  
>
> Meer informatie over:    
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Updates installeren op sites](../../servers/manage/updates.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)

De volgende secties bevatten informatie over de wijzigingen en nieuwe mogelijkheden in versie 1802 van Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Site-infra structuur

### <a name="reassign-distribution-point"></a>Distributie punt opnieuw toewijzen
<!-- 1306937 -->
Veel klanten hebben grote Configuration Manager-infra structuren en verlaagt de primaire of secundaire sites om hun omgeving te vereenvoudigen. Ze moeten nog steeds distributie punten op filiaal locaties bewaren voor het leveren van inhoud aan beheerde clients. Deze distributie punten bevatten vaak meerdere terabytes of meer inhoud. Deze inhoud is in bepaalde tijd en netwerk bandbreedte gedistribueerd om naar deze externe servers te distribueren. Met deze functie kunt u een distributie punt opnieuw toewijzen aan een andere primaire site zonder de inhoud opnieuw te distribueren. Met deze actie wordt de site systeem toewijzing bijgewerkt en wordt alle inhoud op de server bewaard. Zie [een distributie punt opnieuw toewijzen](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_reassign)voor meer informatie.

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Windows Delivery Optimization configureren om Configuration Manager grens groepen te gebruiken
<!-- 1324696 -->
U gebruikt Configuration Manager grens groepen om de distributie van inhoud in uw bedrijfs netwerk en externe kant oren te definiëren en te reguleren. [Windows Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) is een op de cloud gebaseerde peer-to-peer-technologie voor het delen van inhoud tussen Windows 10-apparaten. Vanaf deze release configureert u Delivery Optimization om uw grens groepen te gebruiken bij het delen van inhoud tussen peers. Een nieuwe client instelling past de grens groep-ID toe als de id van de leverings optimalisatie groep op de client. Wanneer de client communiceert met de Delivery Optimization-Cloud service, wordt deze id gebruikt om peers met de gewenste inhoud te vinden. Zie [basis concepten voor inhouds beheer](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)voor meer informatie.

### <a name="support-for-windows-10-arm64-devices"></a>Ondersteuning voor Windows 10 ARM64-apparaten
<!-- 1353704 -->
Vanaf deze release wordt de Configuration Manager-client ondersteund op Windows 10 ARM64-apparaten. Bestaande client beheer functies moeten samen werken met deze nieuwe apparaten. Bijvoorbeeld hardware-en software-inventaris, software-updates en toepassings beheer. Implementatie van besturings systeem wordt momenteel niet ondersteund. 

### <a name="improved-support-for-cng-certificates"></a>Verbeterde ondersteuning voor CNG-certificaten
<!-- 1357314 -->
Configuration Manager (current branch) versie 1710 ondersteunt [crypto grafie: Next Generation (CNG)-certificaten](../network/cng-certificates-overview.md). Versie 1710 beperkt de ondersteuning voor client certificaten in verschillende scenario's. 

Vanaf deze release gebruikt u CNG-certificaten voor de volgende HTTPS-server functies:
- Beheerpunt
- Distributiepunt
- Software-updatepunt
- Statusmigratiepunt  


### <a name="boundary-group-fallback-for-management-points"></a>Terugval van grens groep voor beheer punten
<!-- 1324594 -->
Terugval relaties configureren voor beheer punten tussen [grens groepen](../../servers/deploy/configure/boundary-groups.md). Dit gedrag biedt meer controle over de beheer punten die clients gebruiken. Zie [grens groepen configureren](../../servers/deploy/configure/boundary-groups.md#management-points)voor meer informatie.


### <a name="cloud-distribution-point-site-affinity"></a>Site affiniteit van Cloud distributiepunt
<!--503719-->
Met deze functie kunnen klanten profiteren van een geografisch verspreide hiërarchie met meerdere locaties, met behulp van Cloud distributiepunten. Wanneer een client op internet zoekt naar inhoud, was er al een volg orde voor de lijst met Cloud distributiepunten die door de client zijn ontvangen. Dit gedrag kan ertoe leiden dat clients die inhoud ontvangen van de gegevens van de Cloud distributiepunten in het internet. Het downloaden van inhoud van een dergelijke server op afstand is doorgaans trager dan een dichter server.
 
Met site affiniteit van het Cloud distributiepunt ontvangt een client op internet een geordende lijst. Deze lijst geeft een prioriteit voor Cloud distributiepunten van de toegewezen site van de client. Dit gedrag stelt de beheerder in staat om hun ontwerp intentie te bewaren voor het downloaden van inhoud van site bronnen.
 

## <a name="management-insights"></a>Beheerinzichten
<!-- 1353967 -->
Beheer inzichten in Configuration Manager bieden informatie over de huidige status van uw omgeving. De informatie is gebaseerd op de analyse van gegevens uit de site database. Inzichten helpt u uw omgeving beter te begrijpen en actie te ondernemen op basis van het inzicht. Zie [Management Insights](../../servers/manage/management-insights.md) voor meer informatie.

In Configuration Manager 1802 zijn de volgende inzichten beschikbaar:
- Toepassingen:
    - Toepassingen zonder implementaties
- Cloud Services: <!--1356412-->
    - Gereedheid voor co-beheer beoordelen 
    - Uw apparaten hybride Azure Active Directory-lid maken
    - Uw identiteits-en toegangs infrastructuur moderniseren
    -  Upgrade uw clients naar Windows 10, versie 1709 of hoger 
- Reeksen
    - Lege verzamelingen
- Vereenvoudigd beheer:  <!--1355148-->
    - Verouderde client versies  
- Software Center: 
    - Gebruikers naar Software Center leiden in plaats van toepassingscatalogus  
    - De nieuwe versie van software Center gebruiken 
- Windows 10: <!--1357421-->
    - Windows-telemetrie en commerciële ID-sleutel configureren 
    - Configuration Manager verbinden met Upgradegereedheid 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Clientbeheer

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Cloud Management gateway-ondersteuning voor Azure Resource Manager
<!-- 1324735 -->
Bij het maken van een exemplaar van de [Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md) (CMG) biedt de wizard nu de mogelijkheid om een **Azure Resource Manager-implementatie**te maken. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is een modern platform voor het beheren van alle oplossings resources als één entiteit, een zogenaamde [resource groep](/azure/azure-resource-manager/resource-group-overview#resource-groups). Bij het implementeren van CMG met Azure Resource Manager gebruikt de site Azure Active Directory (Azure AD) om de benodigde cloud resources te verifiëren en te maken. Het klassieke Azure-beheer certificaat is niet vereist voor deze moderne implementatie. Zie [CMG-topologie ontwerpen](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)voor meer informatie.

> [!IMPORTANT]
> Deze mogelijkheid biedt geen ondersteuning voor Azure Cloud service providers (CSP). De CMG-implementatie met Azure Resource Manager blijft de klassieke Cloud service gebruiken, die niet wordt ondersteund door de CSP. Zie [beschik bare Azure-Services in azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services)voor meer informatie.  

### <a name="improvements-to-cloud-management-gateway"></a>Verbeteringen in de Cloud beheer gateway  

- Vanaf deze release is de **Cloud beheer gateway** geen functie meer voor de evaluatie versie.  

- De functie documentatie is gereviseerd en uitgebreid. Raadpleeg voor meer informatie de volgende artikelen:
    - [Plan voor de Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)
    - [Grootte en schaal van de Cloud beheer gateway](../configs/size-and-scale-numbers.md#bkmk_cmg)
    - [Beveiliging en privacy voor cloudbeheergateway](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md)
    - [Veelgestelde vragen over de Cloud beheer gateway](../../clients/manage/cmg/cloud-management-gateway-faq.md)
    - [Certificaten voor cloudbeheergateway](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md)
    - [Een cloudbeheergateway instellen](../../clients/manage/cmg/setup-cloud-management-gateway.md)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Hardware-inventaris configureren voor het verzamelen van teken reeksen die groter zijn dan 255 tekens
<!-- 1357389 -->
U kunt de lengte van teken reeksen configureren zodat deze groter is dan 255 tekens voor hardware-inventarisatie-eigenschappen. Deze wijziging is alleen van toepassing op nieuw toegevoegde klassen en voor hardware-inventarisatie-eigenschappen die geen sleutels zijn. Zie het artikel hardware- [inventaris uitbreiden](../../clients/manage/inventory/extend-hardware-inventory.md#bkmk_GreaterThan255) voor meer informatie. 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Aankondiging van afschaffing voor ondersteuning voor Linux-en UNIX-clients
 <!--510139-->
Micro soft zal de Linux-en UNIX-client ondersteuning in Configuration Manager ongeveer één jaar van nu afnemen, zodat de clients niet worden opgenomen in versie 1902 van vroege kalender 2019. De Configuration Manager 1810-release, in late kalender 2018, is de laatste release om de Linux-en UNIX-clients op te halen en ze worden ondersteund voor de volledige levens cyclus van Configuration Manager 1810. Na Configuration Manager 1810 moeten klanten Microsoft Azure beheer voor het beheer van Linux-servers overwegen. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

### <a name="surface-device-dashboard"></a>Surface Device-dashboard
<!--1355788-->
Het Surface Device-dash board bevat informatie over de Surface-apparaten die in uw omgeving zijn gevonden. Ga in de-console naar **bewakings** > **oppervlak apparaten**. U kunt de items bekijken:
- Percentage van Opper vlakken
- Percentage Surface-modellen
- Top vijf van firmware versies

Zie het [Surface dash board](../../clients/manage/surface-device-dashboard.md) -artikel voor meer informatie.

### <a name="change-in-the-configuration-manager-client-install"></a>Wijziging in de installatie van de Configuration Manager-client
<!--1356195-->
Vanaf deze release wordt Silverlight niet meer automatisch op client apparaten geïnstalleerd. Zie [vereisten voor het implementeren van clients op Windows-computers](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_ExternalDependencies) voor meer informatie.

## <a name="co-management"></a>Co-beheer

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Overgang Endpoint Protection werk belasting naar intune met behulp van co-beheer
<!-- 1357365 -->
 De werk belasting van Endpoint Protection kan worden overgezet naar intune nadat co-beheer is ingeschakeld. Als u de Endpoint Protection workload wilt door lopen, gaat u naar de pagina met eigenschappen voor co-beheer en verplaatst u de schuif regelaar van Configuration Manager naar **pilot** of **alle**. Zie [workloads voor co-beheer](../../../comanage/workloads.md)voor meer informatie over de werk belastingen. Voor meer informatie over co-beheer raadpleegt u [co-beheer voor Windows 10-apparaten](../../../comanage/overview.md).
 
### <a name="co-management-dashboard-in-configuration-manager"></a>Het dash board voor co-beheer in Configuration Manager
<!--1356648-->
Vanaf deze release kunt u een dash board weer geven met informatie over co-beheer. Met het dash board kunt u computers bekijken die in uw omgeving worden beheerd. De grafieken kunnen helpen bij het identificeren van apparaten die mogelijk aandacht vereisen. Zie het artikel over het [co-beheer dashboard](../../../comanage/how-to-monitor.md#co-management-dashboard) voor meer informatie. 


## <a name="compliance-settings"></a>Instellingen voor naleving

### <a name="microsoft-edge-browser-policies"></a>Micro soft Edge-browser beleid
<!-- 1357310 -->
Voor klanten die de [micro soft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) -webbrowser op Windows 10-clients gebruiken, maakt u een Configuration Manager beleid voor nalevings instellingen om verschillende micro soft Edge-instellingen te configureren. Zie [micro soft Edge-browser profiel maken](../../../compliance/deploy-use/browser-profiles.md)voor meer informatie. 



## <a name="application-management"></a>Beheer van toepassingen

### <a name="allow-user-interaction-when-installing-an-application"></a>Gebruikers interactie toestaan bij het installeren van een toepassing
<!-- 1356976 -->
Hiermee staat u toe dat een eind gebruiker met een toepassings installatie communiceert tijdens het uitvoeren van de taken reeks. Voer bijvoorbeeld een installatie proces uit dat de eind gebruiker vraagt om verschillende opties. Sommige installatie Programma's van toepassingen kunnen geen stilte van gebruikers vragen of het installatie proces vereist mogelijk specifieke configuratie waarden die alleen voor de gebruiker bekend zijn. Met deze functie kunt u deze installatie scenario's afhandelen. Zie [Opties voor gebruikers ervaring opgeven voor het implementatie type](../../../apps/deploy-use/create-applications.md#bkmk_dt-ux)voor meer informatie.

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Vervangen toepassingen niet automatisch bijwerken
<!-- 1351266 -->
Configureer een toepassings implementatie om vervangen versie niet automatisch bij te werken. Wanneer u de implementatie hebt gemaakt, kunt u op de pagina **implementatie-instellingen** van de **wizard software implementeren**voor het **beschik bare** installatie doel de optie in-of uitschakelen om **vervangen versies van deze toepassing automatisch**bij te werken. Zie [implementatie-instellingen opgeven](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)voor meer informatie.

### <a name="approve-application-requests-for-users-per-device"></a>Toepassings aanvragen voor gebruikers per apparaat goed keuren
<!-- 1357015 -->
Vanaf deze release, wanneer een gebruiker een toepassing aanvraagt die goed keuring vereist, is de specifieke apparaatnaam nu deel uit van de aanvraag. Als de beheerder de aanvraag goedkeurt, kan de gebruiker de toepassing alleen op dat apparaat installeren. De gebruiker moet een andere aanvraag indienen om de toepassing op een ander apparaat te installeren. Zie [implementatie-instellingen opgeven](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)voor meer informatie.

 > [!Note]  
 > Dit is een optionele functie. Zie voor meer informatie [Enable optional features from updates](../../servers/manage/install-in-console-updates.md#bkmk_options).  


### <a name="run-scripts-improvements"></a>Verbeteringen in scripts uitvoeren 
<!-- 1236459 -->
 Vanaf deze release is het **uitvoeren van scripts** niet langer een voorlopige functie. De script uitvoer wordt nu weer gegeven in JSON-indeling. Zie [Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console](../../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie.


## <a name="operating-system-deployment"></a>Implementatie van besturingssystemen

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Windows 10 in-place upgrade taken reeks via de Cloud beheer gateway
<!-- 1357149 -->
De [taken reeks](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md) Windows 10 in-place upgrade ondersteunt nu implementatie voor clients op Internet die worden beheerd via de [Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md). Met deze mogelijkheid kunnen externe gebruikers eenvoudiger een upgrade uitvoeren naar Windows 10 zonder dat ze verbinding hoeven te maken met het bedrijfs netwerk. Zie [Een takenreeks implementeren](../../../osd/deploy-use/deploy-a-task-sequence.md)voor meer informatie.

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Taken reeks voor verbeteringen in Windows 10 in-place upgrade
<!-- 1357425 -->
De standaard taken reeks sjabloon voor Windows 10 in-place upgrade bevat nu extra groepen met aanbevolen acties om toe te voegen voor en na het upgrade proces. Deze acties zijn gebruikelijk voor veel klanten die apparaten met succes upgraden naar Windows 10. Zie [een taken reeks maken om een besturings systeem bij te werken](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-to-prepare-for-upgrade)voor meer informatie.

### <a name="improvements-to-operating-system-deployment"></a>Verbeteringen in de implementatie van besturings systemen
Deze release bevat de volgende verbeteringen voor de implementatie van besturings systemen:
- Bij het starten van cmtrace. exe in Windows PE wordt u niet meer gevraagd om te kiezen of u dit programma wilt instellen als de standaard viewer voor logboek bestanden. <!-- SMS 500897 -->
- Installatie kopieën toevoegen aan de taken reeks stap [pakket inhoud downloaden](../../../osd/understand/task-sequence-steps.md#BKMK_DownloadPackageContent) .
- Verbeteringen in de stap [taken reeks uitvoeren](../../../osd/understand/task-sequence-steps.md#child-task-sequence) : <!-- 1261338 -->   
  - Ondersteuning voor alle implementatie scenario's voor besturings systemen vanuit software Center, PXE en media.
  - Verbeteringen aan console acties, zoals kopiëren, importeren, exporteren en waarschuwen tijdens het verwijderen van een object.
  - Ondersteuning voor de wizard voor [bereid inhouds bestand maken](../hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) .
  - Integratie met verificatie op basis van implementatie. Zie [taken reeks implementaties met een hoog risico](../../../osd/deploy-use/deploy-a-task-sequence.md)voor meer informatie. 
  - De stap taken reeks uitvoeren kan nu worden gebruikt op meerdere niveaus van taken reeksen, niet alleen voor één bovenliggende/onderliggende relatie. Relaties met meerdere niveaus verg Roten de complexiteit, dus wees voorzichtig. Deze relaties worden nog steeds gecontroleerd op kring verwijzingen.

### <a name="deployment-templates-for-task-sequences"></a>Implementatie sjablonen voor taken reeksen
<!-- 1357391 -->
De [implementatie wizard voor taken reeksen](../../../osd/deploy-use/deploy-a-task-sequence.md) kan nu een implementatie sjabloon maken. De implementatie sjabloon kan worden opgeslagen en toegepast op een bestaande of nieuwe taken reeks voor het maken van een implementatie. 

### <a name="phased-deployments-for-task-sequences"></a>Gefaseerde implementaties voor taken reeksen
<!--1356837-->
 Gefaseerde implementaties is een [functie van een evaluatie versie](../../servers/manage/pre-release-features.md). Gefaseerde implementaties automatiseren een gecoördineerde, geordende implementatie van een taken reeks over meerdere verzamelingen. U kunt [gefaseerde implementaties maken](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) met de standaard twee fasen of hand matig meerdere fasen configureren. Gefaseerde implementatie van taken reeksen biedt geen ondersteuning voor de installatie van PXE of media.




## <a name="software-center"></a>Software Center

### <a name="install-multiple-applications-in-software-center"></a>Meerdere toepassingen installeren in Software Center
<!-- 1357126 -->
Als een eind gebruiker of een desktop technicus meerdere toepassingen op een apparaat moet installeren, ondersteunt Software Center nu het installeren van meerdere geselecteerde toepassingen. Dit gedrag zorgt ervoor dat de gebruiker efficiënter en niet wacht totdat de ene installatie is voltooid voordat de volgende wordt gestart. Zie voor meer informatie [meerdere toepassingen installeren](../../understand/software-center.md#install-multiple-applications) in de gebruikers handleiding van het nieuwe software Center.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Software Center gebruiken om door gebruikers beschik bare toepassingen te bladeren en te installeren op apparaten die zijn toegevoegd aan Azure AD
<!-- 1322613 -->
Als u toepassingen implementeert als beschikbaar voor gebruikers, kunnen ze deze nu bekijken en installeren via Software Center op Azure Active Directory Azure AD-apparaten. Zie voor meer informatie [gebruikers beschik bare toepassingen implementeren op apparaten die zijn toegevoegd aan Azure AD](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Geïnstalleerde toepassingen verbergen in Software Center
<!--1357592-->
Geïnstalleerde toepassingen kunnen nu worden verborgen in Software Center. Toepassingen die al zijn geïnstalleerd, worden niet meer weer gegeven op het tabblad toepassingen wanneer deze optie is ingeschakeld onder client instellingen. Deze optie is ingesteld als de standaard waarde bij het installeren of upgraden van Configuration Manager 1802.  Geïnstalleerde toepassingen zijn nog steeds beschikbaar voor controle op het tabblad installatie status. [geïnstalleerde toepassingen verbergen in Software Center](../../clients/deploy/about-client-settings.md#bkmk_HideInstalled) bevat aanvullende informatie.   

### <a name="hide-unapproved-applications-in-software-center"></a>Niet-goedgekeurde toepassingen verbergen in Software Center
 <!--1355146-->
Als deze optie voor client instelling is ingeschakeld, worden beschik bare toepassingen die goed keuring vereisen, verborgen in Software Center.  Niet- [goedgekeurde toepassingen in Software Center verbergen](../../clients/deploy/about-client-settings.md#bkmk_HideUnapproved) bevat aanvullende informatie.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Software Center toont aanvullende informatie over gebruikers compatibiliteit
<!-- 1235616 -->
 Wanneer u Apparaatstatusverklaring status als nalevings beleids regel gebruikt voor voorwaardelijke toegang tot bedrijfs resources, toont Software Center nu de gebruiker Apparaatstatusverklaring instelling die niet aan het beleid voldoet.


 ## <a name="software-updates"></a>Software-updates 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>De evaluatie regel voor automatische implementatie plannen die moet worden gecompenseerd van een basis dag. 
<!--1357133-->
Regels voor automatische implementatie kunnen worden gepland om de offset van een basis dag te evalueren. Als patch-dinsdag echt woensdag voor u is, kan de evaluatie planning worden ingesteld voor de tweede dinsdag van de maand met één dag. Zie [software-updates automatisch implementeren](../../../sum/deploy-use/automatically-deploy-software-updates.md#BKMK_CreateAutomaticDeploymentRule)voor meer informatie. 



## <a name="reporting"></a>Rapporten

### <a name="report-for-default-browser-counts"></a>Rapport voor standaard aantal browsers
<!-- 1357830 -->
Er is nu een nieuw rapport om het aantal clients met een specifieke webbrowser weer te geven als de Windows-standaard versie. Zie het rapport **standaard browser aantallen** in de groep **software-bedrijven en producten** . Zie de [lijst met rapporten](../../servers/manage/list-of-reports.md#software---companies-and-products)voor meer informatie.

### <a name="report-on-windows-autopilot-device-information"></a>Gegevens over Windows auto pilot-apparaten rapporteren
<!-- 1351442 -->
Windows auto pilot is een oplossing voor het voorbereiden en configureren van nieuwe Windows 10-apparaten op een moderne manier. Zie voor meer informatie een [overzicht van Windows auto pilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Eén methode voor het registreren van bestaande apparaten met Windows auto pilot is het uploaden van apparaatgegevens naar het Microsoft Store voor bedrijven en onderwijs. Deze informatie omvat het serie nummer van het apparaat, de Windows-product-id en een hardware-id. Gebruik Configuration Manager om deze apparaatgegevens te verzamelen en te rapporteren met het nieuwe rapport, **Windows auto pilot-apparaatgegevens**, in het knoop punt **Hardware-algemeen** rapporten. Zie voor meer informatie [over het voorbereiden van op internet gebaseerde apparaten voor co-beheer bij het](../../../comanage/how-to-prepare-Win10.md#windows-autopilot) voorbereiden van co-beheer.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Rapport over Windows 10-onderhouds Details voor een specifieke verzameling
<!--1357653-->
In de **Windows 10-onderhouds Details voor een specifiek verzamelings** rapport wordt algemene informatie weer gegeven over Windows 10-onderhoud voor een bepaalde verzameling. Dit rapport bevat de resource-ID, de NetBIOS-naam, de naam van het besturings systeem, de naam van de besturingssysteem release, de build, de besturingssysteem vertakking en de onderhouds status voor Windows 10-apparaten. Zie de [lijst met rapporten](../../servers/manage/list-of-reports.md#operating-system) voor meer informatie.



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Apparaten beveiligen

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Verbeteringen aan Configuration Manager-beleid voor Windows Defender exploit Guard
<!-- 1356220 -->
Er zijn aanvullende beleids instellingen voor de onderdelen [kwets](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_ASR) baarheid voor aanvallen en [Controlled folder access](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md#bkmk_CFA) toegevoegd in Configuration Manager voor [Windows Defender exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-attack-surface-reduction).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Nieuwe instellingen voor interactie met de host voor Windows Defender Application Guard
<!-- 1356256 -->
Voor apparaten met Windows 10 versie 1709 en hoger zijn er twee nieuwe instellingen voor de interactie van hosts voor [Windows Defender Application Guard](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_HIS): 
- Websites kunnen toegang krijgen tot de virtuele grafische processor van de host. 
- Bestanden die in de container worden gedownload, kunnen op de host worden bewaard. 




## <a name="configuration-manager-console"></a>Configuration Manager-console

### <a name="improvements-to-the-configuration-manager-console"></a>Verbeteringen in de Configuration Manager-console 
Deze release bevat de volgende verbeteringen voor de Configuration Manager-console.
- Apparaat lijsten onder activa en naleving, apparaten, nu standaard de primaire gebruiker weer geven. Deze kolom wordt alleen weer gegeven in het knoop punt apparaten. De laatst aangemelde gebruiker kan ook worden toegevoegd als een optionele kolom.<!-- 1357280 --> Schakel client instellingen voor [gebruikers-en apparaat-affiniteit](../../clients/deploy/about-client-settings.md#user-and-device-affinity) in voor de site om een primaire gebruiker te koppelen aan een apparaat.
- Als een verzameling lid is van een andere verzameling en de naam ervan wordt gewijzigd, wordt de nieuwe naam bijgewerkt onder de lidmaatschaps regels.<!--1357282--> 
- Wanneer u extern beheer gebruikt op een client met meerdere monitors bij verschillende DPI-schaling, wordt de muis aanwijzer nu correct gekoppeld. <!--433170-->
- Het [Office 365-dash board voor client beheer](../../../sum/deploy-use/office-365-dashboard.md) geeft een lijst van relevante apparaten weer wanneer secties van de grafiek worden geselecteerd. <!--1357281 --> 



## <a name="next-steps"></a>Volgende stappen
Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md).
