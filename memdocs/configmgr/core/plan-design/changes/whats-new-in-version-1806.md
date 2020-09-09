---
title: Wat is er nieuw in versie 1806
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1806 van Configuration Manager current branch.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: eae605c067094665f2f6866e75fa8f9a94a5df52
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607735"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Wat is er nieuw in versie 1806 van Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1806 voor Configuration Manager current branch is beschikbaar als een update in de console. Deze update Toep assen op sites waarop versie 1706, 1710 of 1802 wordt uitgevoerd. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Bekijk altijd de laatste controle lijst voor het installeren van deze update. Zie [Check List for Install update 1806](../../servers/manage/checklist-for-installing-update-1806.md)(Engelstalig) voor meer informatie. Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).

<!--
> [!Important]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
-->

De volgende secties bevatten informatie over de wijzigingen en nieuwe functies in versie 1806 van Configuration Manager current branch.  



## <a name="deprecated-features-and-operating-systems"></a>Afgeschafte functies en besturings systemen

Meer informatie over ondersteunings wijzigingen voordat ze worden geïmplementeerd in [verwijderde en afgeschafte items](deprecated/removed-and-deprecated.md).

Vanaf 14 augustus 2018 wordt de functie hybride Mobile Device Management afgeschaft. Zie [Wat is er gebeurd met hybride MDM](../../../mdm/understand/what-happened-to-hybrid.md)voor meer informatie.<!--Intune feature 2683117-->  

<!--
Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Site-infra structuur

### <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager heeft altijd een grote centrale opslag van apparaatgegevens verschaft, die klanten gebruiken voor rapportage doeleinden. De site verzamelt deze gegevens doorgaans wekelijks. CMPivot is een nieuw hulp programma in de console dat nu toegang biedt tot de real-time status van apparaten in uw omgeving. Er wordt onmiddellijk een query uitgevoerd op alle apparaten die momenteel zijn verbonden in de doel verzameling en de resultaten worden geretourneerd. U kunt deze gegevens vervolgens filteren en groeperen in het hulp programma. Door real-time gegevens op te geven van online-clients, kunt u sneller zakelijke vragen beantwoorden, problemen oplossen en reageren op beveiligings incidenten. 

Zie [CMPivot](../../servers/manage/cmpivot.md)voor meer informatie.  


### <a name="site-server-high-availability"></a>Siteserver met hoge beschikbaarheid
<!--1128774-->
Hoge Beschik baarheid voor een zelfstandige primaire site serverrol is een op Configuration Manager gebaseerde oplossing voor het installeren van een extra site server in de passieve modus. De site server in de passieve modus is een aanvulling op uw bestaande site server in de actieve modus. Een site server in de passieve modus is beschikbaar voor onmiddellijk gebruik, indien nodig. 

Raadpleeg voor meer informatie de volgende artikelen: 
- [Siteserver met hoge beschikbaarheid](../../servers/deploy/configure/site-server-high-availability.md) 
- [Stroom diagram: een site server instellen in de passieve modus](../../servers/deploy/configure/passive-site-server-flowchart.md)
- [Stroomdiagram: niveau van siteserver verhogen (gepland)](../../servers/deploy/configure/promote-site-server-flowchart.md)
- [Stroomdiagram: niveau van siteserver verhogen (ongepland)](../../servers/deploy/configure/promote-site-server-unplanned-flowchart.md)


### <a name="improvements-to-management-insights"></a>Verbeteringen aan management Insights
Deze release bevat de volgende verbeteringen voor management Insights:  

- Sommige beheer inzichten hebben nu de mogelijkheid om een actie uit te voeren. Deze actie navigeert naar het gekoppelde knoop punt in de-console of toont een gefilterde weer gave op basis van een query.<!--1357930-->  

- Er is een nieuwe groep voor proactieve onderhoud beschikbaar met zes nieuwe regels, waarmee u mogelijke configuratie problemen kunt markeren om te voor komen dat deze regel matig worden bewaard.<!--1352184-->  

Zie [Management Insights](../../servers/manage/management-insights.md)voor meer informatie.


### <a name="configuration-manager-tools"></a>Configuration Manager-hulpprogramma's
<!--1357145-->
De Configuration Manager server-en client hulpprogramma's zijn nu opgenomen op de server. Zoek ze in de `CD.Latest\SMSSETUP\Tools` map op de site server. U hoeft verder niets te installeren. 

Zie [Configuration Manager-hulpprogram ma's](../../support/tools.md)voor meer informatie.


### <a name="exclude-active-directory-containers-from-discovery"></a>Active Directory containers uitsluiten van detectie
<!--1358143-->
Als u het aantal gedetecteerde objecten wilt verminderen, moet u specifieke containers uitsluiten van Active Directory systeem detectie. 

Zie [Active Directory-systeem detectie configureren](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_config-adsd)voor meer informatie.



## <a name="content-management"></a>Inhoudbeheer

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Een externe inhouds bibliotheek voor de site server configureren
<!--1357525-->
Als u de hoge Beschik baarheid van de site server wilt configureren of als u ruimte op de vaste schijf op de centrale beheer-of primaire site servers wilt vrijmaken, moet u de inhouds bibliotheek verplaatsen naar een andere opslag locatie. Verplaats de inhouds bibliotheek naar een ander station op de site server, een afzonderlijke server of fout tolerante schijven in een Storage Area Network (SAN). 

Raadpleeg voor meer informatie de volgende artikelen: 
- [De inhoudsbibliotheek](../hierarchy/the-content-library.md)
- [Stroomdiagram: inhoudsbibliotheek beheren](../hierarchy/manage-content-library-flowchart.md)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Ondersteuning voor Cloud distributiepunt voor Azure Resource Manager
<!--1322209-->
Wanneer u een Cloud distributiepunt maakt, biedt de wizard nu de mogelijkheid om een **Azure Resource Manager-implementatie**te maken. Azure Resource Manager is een modern platform voor het beheren van alle oplossings resources als één entiteit, een zogenaamde resource groep. Wanneer u een Cloud distributiepunt implementeert met Azure Resource Manager, gebruikt de site Azure Active Directory om de benodigde cloud resources te verifiëren en te maken. Het klassieke Azure-beheer certificaat is niet vereist voor deze moderne implementatie. 

De functie documentatie voor het Cloud distributiepunt is ook herzien en verbeterd. Raadpleeg voor meer informatie de volgende artikelen:
- [Een Cloud distributiepunt gebruiken](../hierarchy/use-a-cloud-based-distribution-point.md)   
- [Een Cloud distributiepunt installeren](../../servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Pull-distributie punten ondersteunen Cloud distributiepunten als bron  
<!--1321554-->
Veel klanten gebruiken pull-distributie punten in externe of filialen, die inhoud van een bron distributiepunt downloaden via het WAN. Als uw externe kant oren een betere verbinding met internet hebben of als u de belasting van uw WAN-koppelingen wilt verkorten, kunt u nu een Cloud distributiepunt in Microsoft Azure als bron gebruiken. Wanneer u een bron toevoegt op het **pull-distributie punt** tabblad van de eigenschappen van het distributie punt, wordt een Cloud distributiepunt in de site nu vermeld als beschikbaar distributie punt. Het gedrag van beide site systeem rollen blijft anders. 

Zie [een pull-distributie punt gebruiken](../hierarchy/use-a-pull-distribution-point.md)voor meer informatie.


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Distributie punten inschakelen voor het gebruik van congestie beheer van het netwerk
<!--1358112-->
Windows-lage extra vertraging achtergrond transport (LEDBAT) is een functie van Windows Server voor het beheren van achtergrond netwerk overdrachten. Voor distributie punten die worden uitgevoerd op ondersteunde versies van Windows Server, kunt u een optie inschakelen om netwerk verkeer aan te passen. Clients gebruiken alleen netwerk bandbreedte wanneer dit beschikbaar is. 

Zie [Windows LEDBAT](../hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat)voor meer informatie.


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Gedeeltelijke download ondersteuning in client-peer-cache om WAN-gebruik te verminderen
<!--1357346-->
Client-peer-cache bronnen kunnen nu inhoud in delen delen. Deze onderdelen minimaliseren de netwerk overdracht om WAN-gebruik te verminderen. Het beheer punt biedt gedetailleerdere tracking van de inhouds onderdelen. Er wordt geprobeerd om meer dan één down load van dezelfde inhoud per grens groep te verwijderen. 

Zie [ondersteuning voor gedeeltelijk downloaden](../hierarchy/client-peer-cache.md#bkmk_parts)voor meer informatie. 


### <a name="boundary-group-options-for-peer-downloads"></a>Opties voor grens groepen voor het downloaden van peers
<!--1356193-->
Grens groepen bevatten nu aanvullende instellingen om u meer controle te geven over de distributie van inhoud in uw omgeving. Deze release voegt de volgende opties toe:  

- **Down loads van peers toestaan in deze grens groep**: het beheer punt biedt clients een lijst met inhouds locaties die peer bronnen bevatten. Deze instelling is ook van invloed op het Toep assen van groeps-Id's voor optimalisatie van levering.  

- **Gebruik tijdens het downloaden van peers alleen peers binnen hetzelfde subnet**: het beheer punt bevat alleen in de inhouds locatie lijst peer bronnen die zich in hetzelfde subnet bevinden als de client.  

Zie voor meer informatie [Opties voor grens groepen voor het downloaden van peers](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="improvement-to-peer-cache-source-location-status"></a>Verbetering van de status van de bron locatie van de peer-cache
<!--SCCMDocs issue 850-->
Configuration Manager is efficiënter bij het bepalen of een peer-cache bron is geroamd naar een andere locatie. Dit gedrag zorgt ervoor dat het beheer punt dit als een inhouds bron levert aan clients op de nieuwe locatie en niet op de oude locatie. Als u de functie voor peer-cache gebruikt met zwervende peer-cache bronnen, moet u na het bijwerken van de site naar versie 1806 ook alle peer-cache bronnen bijwerken naar de meest recente client versie. Het beheer punt bevat deze peer-cache bronnen niet in de lijst met inhouds locaties totdat ze zijn bijgewerkt naar ten minste versie 1806.

Zie [vereisten voor peer-cache](../hierarchy/client-peer-cache.md#requirements)voor meer informatie.



<!-- ## Migration  -->



## <a name="client-management"></a>Clientbeheer

### <a name="improvement-to-client-push-security"></a>Verbetering van client push beveiliging
<!--1358204-->
Wanneer u de client push methode voor het installeren van de Configuration Manager-client gebruikt, kan de site nu wederzijdse Kerberos-verificatie vereisen. Deze verbetering helpt bij het beveiligen van de communicatie tussen de server en de client. 

Zie [clients installeren met client push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)voor meer informatie.


### <a name="enhanced-http-site-system"></a><a name="bkmk_ehttp"></a> Verbeterd HTTP-site systeem
<!--1356889,1358228-->
Het gebruik van HTTPS-communicatie wordt aanbevolen voor alle Configuration Manager communicatie paden, maar dit kan lastig zijn voor sommige klanten vanwege de overhead van het beheer van PKI-certificaten.

Deze release bevat verbeteringen in de manier waarop clients communiceren met site systemen. Selecteer op het tabblad site-eigenschappen, **client computer communicatie** de optie voor **https of http**en schakel vervolgens de optie Nieuw in voor het **gebruik van door Configuration Manager gegenereerde certificaten voor http-site systemen**. Deze functie is een [evaluatie versie](../../servers/manage/pre-release-features.md).

Zie [Enhanced http](../hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie.


### <a name="azure-ad-device-identity"></a>Azure AD-apparaat-id 
<!--1358460-->
Een Azure AD-of [Hybrid Azure AD-apparaat](/azure/active-directory/devices/concept-azure-ad-join-hybrid) zonder een aangemelde Azure AD [-](/azure/active-directory/devices/concept-azure-ad-join) gebruiker kan veilig communiceren met de toegewezen site. De identiteit van het apparaat in de Cloud is nu voldoende voor verificatie met de CMG en het beheer punt.  

Zie [Enhanced http](../hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie.


### <a name="cmtrace-installed-with-client"></a>CMTrace geïnstalleerd met client
<!--1357971-->
Het CMTrace-hulp programma voor logboek weergave wordt nu samen met de Configuration Manager-client automatisch geïnstalleerd. Deze wordt toegevoegd aan de installatiemap van de client. Dit is standaard `%WinDir%\ccm\cmtrace.exe` . 

Zie [CMTrace](../../support/cmtrace.md) voor meer informatie.


### <a name="cloud-management-dashboard"></a>Dash board voor Cloud beheer
<!--1358461-->
Het nieuwe dash board voor Cloud beheer biedt een gecentraliseerde weer gave voor CMG-gebruik (Cloud Management Gateway). Wanneer de site is opgebruikt met Azure AD, worden ook gegevens over Cloud gebruikers en-apparaten weer gegeven.   

Deze functie bevat ook de **CMG Connection Analyzer** voor real-time verificatie bij het oplossen van problemen. Het console-hulp programma controleert de huidige status van de service en het communicatie kanaal via het CMG-verbindings punt naar een beheer punt dat CMG-verkeer toestaat. 

Zie voor meer informatie de volgende secties van het artikel [monitor CMG](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md) :  
- [Dash board voor Cloud beheer](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#cloud-management-dashboard)  
- [Connection Analyzer](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#connection-analyzer)  


### <a name="improvements-to-cloud-management-gateway"></a>Verbeteringen in de Cloud beheer gateway

Versie 1806 bevat de volgende verbeteringen voor de Cloud Management Gateway (CMG):

#### <a name="simplified-client-bootstrap-command-line"></a>Vereenvoudigde client opdracht regel voor Boots trap
<!--1358215-->
Wanneer u de Configuration Manager-client op Internet installeert via een CMG, zijn voor de opdracht regel nu minder eigenschappen vereist. Deze verbetering vermindert de grootte van de opdracht regel die wordt gebruikt in Microsoft Intune bij het voorbereiden van co-beheer. 

Zie [hoe u op internet gebaseerde apparaten voorbereidt voor co-beheer](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)voor meer informatie.

#### <a name="download-content-from-a-cmg"></a>Inhoud downloaden van een CMG
<!--1358651-->
Voorheen moest u een Cloud distributiepunt en CMG implementeren als afzonderlijke rollen. Een CMG kan nu ook inhoud leveren aan clients. Deze functionaliteit vermindert de vereiste certificaten en kosten van virtuele Azure-machines. 

Zie [een CMG wijzigen](../../clients/manage/cmg/setup-cloud-management-gateway.md#modify-a-cmg)voor meer informatie.

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Het vertrouwde basis certificaat is niet vereist voor Azure AD
<!--503899-->
Wanneer u een CMG maakt, hoeft u niet langer een [vertrouwd basis certificaat](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) op te geven op de pagina instellingen. Dit certificaat is niet vereist wanneer u Azure Active Directory (Azure AD) gebruikt voor client verificatie, maar dat in de wizard vereist is. Als u certificaten voor PKI-client verificatie gebruikt, moet u nog steeds een vertrouwd basis certificaat toevoegen aan de CMG.



## <a name="co-management"></a>Co-beheer

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>MDM-beleid van Microsoft Intune voor een gezamenlijk beheerd apparaat synchroniseren
<!--1357377-->
Wanneer u een werk belasting voor co-beheer overschakelt, wordt het MDM-beleid automatisch gesynchroniseerd van Microsoft Intune. Deze synchronisatie treedt ook op wanneer u de actie **computer beleid downloaden** van client meldingen in de Configuration Manager-console start. 

Zie [Configuration Manager workloads naar intune overschakelen](../../../comanage/how-to-switch-workloads.md)voor meer informatie.


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Nieuwe workloads overzetten naar intune met behulp van co-beheer
De volgende werk belastingen kunnen nu overstappen van Configuration Manager naar intune nadat co-beheer is ingeschakeld:  

- **Apparaatconfiguratie**<!--1357903-->: Met deze workload kunt u intune gebruiken om MDM-beleid te implementeren, terwijl u Configuration Manager gebruikt voor het implementeren van toepassingen.  

- **Office 365**<!--1357841-->: Apparaten worden niet Microsoft 365 implementaties van Configuration Manager geïnstalleerd.  

- **Mobiele apps**<!--1357892-->: Alle beschik bare apps die zijn geïmplementeerd vanuit intune, zijn beschikbaar in de Bedrijfsportal. Apps die u vanaf Configuration Manager implementeert, zijn beschikbaar in Software Center. Deze functie is een [evaluatie versie](../../servers/manage/pre-release-features.md).  

Als u deze werk belastingen wilt door lopen, gaat u naar de pagina met eigenschappen voor co-beheer en verplaatst u de schuif regelaar werk belasting van Configuration Manager naar **pilot** of **alle**. 

Zie voor meer informatie [co-beheer voor Windows 10-apparaten](../../../comanage/overview.md).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Ondersteuning voor meerdere hiërarchieën naar één intune-Tenant
<!--1357944-->
Sommige klanten hebben verschillende Configuration Manager hiërarchieën en willen in de toekomst samen voegen tot één Tenant voor Azure Active Directory en Microsoft Intune. Co-beheer ondersteunt nu het verbinden van meer dan een Configuration Manager omgeving met dezelfde intune-Tenant.

Zie [vereisten voor co-beheer](../../../comanage/overview.md#prerequisites)voor meer informatie.
 


## <a name="compliance-settings"></a>Instellingen voor naleving

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Windows Defender SmartScreen-instellingen voor micro soft Edge configureren
<!--1353701-->
Het beleid voor nalevings instellingen van de micro soft Edge-browser voegt de volgende drie instellingen toe voor Windows Defender SmartScreen: 
- SmartScreen toestaan
- Gebruikers kunnen SmartScreen-prompts voor sites overschrijven
- Gebruikers kunnen SmartScreen-prompts voor bestanden negeren

Zie [instellingen voor micro soft Edge configureren](../../../compliance/deploy-use/browser-profiles.md)voor meer informatie.


### <a name="scap-extensions"></a>SCAP-extensies
<!--1357552-->
SCAP-inhoud (Security content Automation Protocol) converteren naar de basis lijnen voor nalevings instellingen en SCAP-rapporten genereren met behulp van een console-uitbrei ding. Deze functie omvat ook een nieuw dash board voor het visualiseren van de naleving van de client en de naleving van de XCCDF-regels. 





## <a name="application-management"></a>Toepassingsbeheer

### <a name="phased-deployment-of-applications"></a>Gefaseerde implementatie van toepassingen
<!--1358147-->
Een gefaseerde implementatie maken voor een toepassing. Met gefaseerde implementaties kunt u een gecoördineerde, geordende implementatie van software organiseren op basis van aanpas bare criteria en groepen. U kunt bijvoorbeeld de toepassing implementeren in een pilot verzameling en vervolgens de implementatie automatisch voortzetten op basis van de criteria voor geslaagde pogingen. 

Raadpleeg voor meer informatie de volgende artikelen:  

- [Een gefaseerde implementatie maken](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  

- [Gefaseerde implementaties beheren en bewaken](../../../osd/deploy-use/manage-monitor-phased-deployments.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Windows-app-pakketten inrichten voor alle gebruikers op een apparaat
<!--1358310-->
Richt een toepassing in met een Windows-app-pakket voor alle gebruikers op het apparaat. Een veelvoorkomend voor beeld van dit scenario is het inrichten van een app van de Microsoft Store for Business en Education, zoals Minecraft: Education Edition, op alle apparaten die worden gebruikt door studenten op school. Voorheen Configuration Manager alleen de installatie van deze toepassingen per gebruiker ondersteund. Nadat u zich hebt aangemeld bij een nieuw apparaat, moet een student wachten op toegang tot een app. Wanneer de app nu voor alle gebruikers op het apparaat wordt ingericht, kunnen ze sneller productief zijn. 

Zie [Windows-toepassingen maken](../../../apps/get-started/creating-windows-applications.md#bkmk_provision)voor meer informatie.


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integratie van Office Customization Tool met Office 365 Installer
<!--1358149-->
Het hulp programma voor het aanpassen van Office is nu geïntegreerd met het installatie programma van Office 365 in de Configuration Manager-console. Wanneer u een implementatie voor Microsoft 365 maakt, moet u de meest recente Office-beheer baarheid-instellingen dynamisch configureren. Micro soft werkt het hulp programma voor het aanpassen van Office bij wanneer nieuwe builds van Microsoft 365 worden uitgebracht. Met deze integratie kunt u profiteren van nieuwe beheer instellingen in Microsoft 365 zodra deze beschikbaar zijn. 

Zie [Microsoft 365-Apps implementeren](../../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie.


### <a name="support-for-new-windows-app-package-formats"></a>Ondersteuning voor nieuwe Windows-app-pakket indelingen
<!--1357427-->
Configuration Manager ondersteunt nu de implementatie van nieuwe indelingen van Windows 10 app package (. msix) en app-bundel (. msixbundle). 

Zie [Windows-toepassingen maken](../../../apps/get-started/creating-windows-applications.md#bkmk_msix)voor meer informatie.


### <a name="uninstall-application-on-approval-revocation"></a>Toepassing verwijderen bij het intrekken van de goed keuring
<!--1357891-->
Het gedrag is gewijzigd wanneer u de goed keuring voor een toepassing intrekt. Wanneer u de aanvraag voor de toepassing weigert, verwijdert de client de toepassing van het apparaat van de gebruiker. Voor dit gedrag moet u de [optionele functie](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **voor het goed keuren van toepassings aanvragen voor gebruikers per apparaat**inschakelen. 

Zie [toepassingen implementeren](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)voor meer informatie.


### <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Pakket conversie beheer is nu een geïntegreerd hulp programma waarmee u verouderde pakketten kunt converteren naar Configuration Manager huidige branch-toepassingen. Vervolgens kunt u de functies van toepassingen gebruiken, zoals afhankelijkheden, vereisten regels en gebruikers affiniteit met apparaat.

Zie [package Conversion Manager](../../../apps/pcm/package-conversion-manager.md)voor meer informatie.



## <a name="os-deployment"></a>Besturingssysteemimplementatie

### <a name="improvements-to-phased-deployments"></a>Verbeteringen in gefaseerde implementaties

Deze release bevat de volgende verbeteringen in gefaseerde implementaties:  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Een gefaseerde implementatie met hand matig geconfigureerde fasen maken
<!--1358148-->
Voor een taken reeks configureert u de fasen nu hand matig wanneer u een gefaseerde implementatie maakt. Voeg Maxi maal 10 extra fasen toe op het tabblad **fasen** van de wizard gefaseerde implementatie maken. U kunt nog steeds automatisch een standaard implementatie met twee fasen maken. 

Zie [een gefaseerde implementatie met hand matig geconfigureerde fasen maken](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_manual)voor meer informatie.

#### <a name="phased-deployment-status"></a>Status van gefaseerde implementatie
<!--1358577-->
Gefaseerde implementaties hebben nu een systeem eigen bewakings ervaring. Selecteer een gefaseerde implementatie in het knoop punt **implementaties** in de werk ruimte **bewaking** en klik vervolgens op **status van gefaseerde implementatie** in het lint. 

Zie [gefaseerde implementaties beheren en bewaken](../../../osd/deploy-use/manage-monitor-phased-deployments.md)voor meer informatie.  

#### <a name="gradual-rollout-during-phased-deployments"></a>Geleidelijke implementatie tijdens gefaseerd implementeren
<!--1358578-->
Tijdens een gefaseerde implementatie kan de implementatie in elke fase nu geleidelijk plaatsvinden. Dit gedrag helpt bij het oplossen van problemen met de implementatie en vermindert de belasting van het netwerk, veroorzaakt door de distributie van inhoud naar clients. De site kan geleidelijk de software beschikbaar maken, afhankelijk van de configuratie van elke fase. Elke client in een fase heeft een deadline die relatief is ten opzichte van de tijd dat de software beschikbaar is. Het tijd venster tussen de beschik bare tijd en deadline is hetzelfde voor alle clients in een fase. 

Zie [Phase Settings](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md#bkmk_settings)(Engelstalig) voor meer informatie.  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Taken reeks voor verbeteringen in Windows 10 in-place upgrade
<!--1358500-->
De standaard taken reeks sjabloon voor Windows 10 in-place upgrade bevat nu een andere nieuwe groep met aanbevolen acties om toe te voegen wanneer het upgrade proces mislukt. Deze acties maken het gemakkelijker om problemen op te lossen. Een dergelijk hulp programma is Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). Het is een zelfstandig diagnostisch hulp programma voor het verkrijgen van informatie over waarom een Windows 10-upgrade is mislukt. 

Zie [een taken reeks maken om een besturings systeem bij te werken](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-on-failure)voor meer informatie.


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Verbeteringen van distributie punten met PXE-functionaliteit
<!--1357580-->
Schakel op het tabblad **PXE** van de eigenschappen van het distributie punt het selectie vakje **PXE-Responder inschakelen zonder Windows Deployment service**in. Met deze nieuwe optie wordt een PXE-responder op het distributie punt ingeschakeld, waarvoor Windows Deployment Services (WDS) niet vereist is. Omdat WDS niet vereist is, kan het distributie punt met PXE-functionaliteit een client-of Server besturingssysteem zijn, met inbegrip van Windows Server Core. Deze nieuwe PXE responder-service ondersteunt IPv6 en verbetert ook de flexibiliteit van distributie punten met PXE-functionaliteit in externe kant oren. 

Zie [PXE inschakelen op het distributie punt](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)voor meer informatie.


### <a name="network-access-account-not-required-for-some-scenarios"></a>Netwerk toegangs account niet vereist voor bepaalde scenario's
<!--1358278,1358279-->
De [verbeterde HTTP-site systeem](#bkmk_ehttp) functie verwijdert ook enkele afhankelijkheden van het netwerk toegangs account. Wanneer u de optie nieuwe site inschakelt voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen**, is voor de volgende scenario's geen netwerk toegangs account vereist om inhoud te downloaden vanaf een distributie punt:  

- Taken reeksen die worden uitgevoerd vanaf opstart media of PXE
- Taken reeksen die worden uitgevoerd vanuit software Center  

Deze taken reeksen kunnen voor de implementatie van het besturings systeem of aangepast zijn. Het wordt ook ondersteund voor werkgroepcomputers.

Zie [taken reeksen en het netwerk toegangs account](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount)voor meer informatie.


### <a name="other-improvements-to-os-deployment"></a>Andere verbeteringen voor de implementatie van besturings systemen

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Masker gevoelige gegevens die zijn opgeslagen in taken reeks variabelen
 <!--1358330-->
 Selecteer in de stap **taken reeks variabele instellen** de optie Nieuw om **deze waarde niet weer te geven**. 

 Zie [set-variabele taken reeks](../../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)voor meer informatie. 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>De naam van het masker programma tijdens het uitvoeren van de opdracht stap van een taken reeks
 <!--1358493-->
 Als u wilt voor komen dat mogelijk gevoelige gegevens worden weer gegeven of geregistreerd, configureert u de taken reeks variabele **OSDDoNotLogCommand**.  

 Zie [taken reeks variabelen](../../../osd/understand/task-sequence-variables.md#OSDDoNotLogCommand)voor meer informatie. 

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Taken reeks variabele voor DISM-para meters bij het installeren van Stuur Programma's
 <!--516679/2840016-->
 Als u aanvullende opdracht regel parameters voor DISM wilt opgeven, gebruikt u de nieuwe taken reeks variabele **OSDInstallDriversAdditionalOptions**. 

 Zie [taken reeks variabelen](../../../osd/understand/task-sequence-variables.md#OSDInstallDriversAdditionalOptions)voor meer informatie. 

#### <a name="option-to-use-full-disk-encryption"></a>Optie voor het gebruik van volledige schijf versleuteling
 <!--SCCMDocs-pr issue 2671-->
 Zowel de stap **BitLocker inschakelen** als **BitLocker-stappen vooraf inrichten** bevatten nu een optie voor het gebruik van een **volledige schijf versleuteling**. Met deze stappen wordt standaard gebruikte ruimte op het station versleuteld. Dit standaard gedrag wordt aanbevolen, omdat het sneller en efficiënter is. 

 Zie [BitLocker inschakelen](../../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker) en [BitLocker vooraf inrichten](../../../osd/understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker)voor meer informatie. 

#### <a name="client-provisioning-mode-isnt-enabled-with-windows-10-upgrade-compatibility-scan"></a>De client inrichtings modus is niet ingeschakeld met de upgrade compatibiliteits scan voor Windows 10
 <!--SCCMDocs-pr issue 2812-->
 Wanneer u nu de optie inschakelt om **Windows Setup compatibiliteits scan uit te voeren zonder de upgrade te starten**, wordt de Configuration Manager-client niet in de inrichtings modus geplaatst door de taken reeks stap **besturings systeem bijwerken** .

 Zie [upgrade van besturings systeem](../../../osd/understand/task-sequence-steps.md#BKMK_UpgradeOS)voor meer informatie.

#### <a name="revised-documentation-for-task-sequence-variables"></a>Gereviseerde documentatie voor taken reeks variabelen
Er zijn nu twee nieuwe artikelen beschikbaar voor het leren van taken reeks variabelen:  

- Het [gebruik van taken reeks variabelen](../../../osd/understand/using-task-sequence-variables.md) is een nieuw artikel met een beschrijving van de verschillende typen variabelen, methoden voor het instellen van de variabelen en hoe u deze kunt openen.  

- [Taken reeks variabelen](../../../osd/understand/task-sequence-variables.md) is een verwijzing voor alle beschik bare taken reeks variabelen. In dit artikel worden de vorige artikelen gecombineerd, waarbij ingebouwde variabelen worden gescheiden van actie variabelen. 



## <a name="software-center"></a>Software Center

> [!Important]  
> Als u gebruik wilt maken van nieuwe Configuration Manager functies, moet u clients eerst bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.


### <a name="software-center-infrastructure-improvements"></a>Verbeteringen in de Software Center-infra structuur
<!--1358309-->
De functies van de toepassings catalogus zijn niet langer vereist voor het weer geven van gebruikers beschik bare toepassingen in Software Center. Met deze wijziging kunt u de server infrastructuur verminderen die nodig is voor het leveren van toepassingen aan gebruikers. Software Center is nu afhankelijk van het beheer punt om deze informatie te verkrijgen, waardoor grotere omgevingen beter kunnen worden geschaald door ze toe te wijzen aan [grens groepen](../../servers/deploy/configure/boundary-groups.md#management-points).

Zie [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex) voor meer informatie.  

> [!Note]  
> De rollen Application catalog-website punt en Web Service Point zijn niet meer *vereist* in 1806, maar nog steeds *ondersteunde* rollen. 
> 
> De **Silverlight-gebruikers ervaring** voor het Application catalog-website punt wordt niet meer ondersteund. Zie [verwijderde en afgeschafte functies](deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>De zicht baarheid van de Application catalog-website koppeling in Software Center opgeven
<!--1358214-->
Gebruik client instellingen om te bepalen of de koppeling voor **het openen van de toepassingscatalogus** website wordt weer gegeven in het knoop punt **installatie status** van software Center.  

Zie [client instellingen voor Software Center](../../clients/deploy/about-client-settings.md#software-center)voor meer informatie.

> [!Note]  
> De **Silverlight-gebruikers ervaring** voor het Application catalog-website punt wordt niet meer ondersteund. Zie [verwijderde en afgeschafte functies](deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.  


### <a name="custom-tab-for-webpage-in-software-center"></a>Aangepast tabblad voor webpagina in Software Center
<!--1358132-->
Gebruik client instellingen om een aangepast tabblad te maken om een webpagina te openen in Software Center. Met deze functie kunt u inhoud op een consistente, betrouw bare manier weer geven aan uw eind gebruikers. De volgende lijst bevat enkele voor beelden:  

- Neem contact op met IT: informatie over hoe u contact kunt opnemen met de IT-afdeling van uw organisatie  

- IT-ondersteunings centrum: IT-self-service acties, zoals zoeken in een Knowledge Base of het openen van een ondersteunings ticket.  

- Documentatie voor eind gebruikers: artikelen voor gebruikers in uw organisatie op diverse IT-onderwerpen, zoals toepassingen gebruiken of een upgrade uitvoeren naar Windows 10.  

Zie [client instellingen voor Software Center](../../clients/deploy/about-client-settings.md#software-center) en de [Gebruikers handleiding voor Software Center](../../understand/software-center.md)voor meer informatie.


### <a name="maintenance-windows-in-software-center"></a>Onderhouds Vensters in Software Center
<!--1358131-->
In Software Center wordt nu het volgende geplande onderhouds venster weer gegeven. Schakel op het tabblad installatie status de optie weer gave van alles naar gepland. Het tijds bereik en de lijst met geplande implementaties worden weer gegeven. Als er geen toekomstig onderhouds Vensters zijn, is de lijst leeg. 

Zie het [gebruik van onderhouds Vensters](../../clients/manage/collections/use-maintenance-windows.md) en de [Gebruikers handleiding voor Software Center](../../understand/software-center.md)voor meer informatie.



## <a name="software-updates"></a>Software-updates

### <a name="third-party-software-updates"></a>Software-updates van derden
<!--1357605, 1352101, 1358714-->
Met software-updates van derden kunt u zich abonneren op partner catalogi in de Configuration Manager-console en de updates publiceren naar WSUS. U kunt deze updates vervolgens implementeren met behulp van het bestaande software-update beheer proces. 

Zie updates van derden [inschakelen](../../../sum/deploy-use/third-party-software-updates.md)voor meer informatie.


### <a name="deploy-software-updates-without-content"></a>Software-updates zonder inhoud implementeren
<!--1357933-->
Software-updates implementeren op apparaten zonder eerst inhoud te downloaden en te distribueren naar distributie punten. Deze functie is handig bij het verwerken van extreem grote update-inhoud of wanneer u altijd wilt dat clients inhoud ophalen van de Microsoft Update Cloud service. Clients in dit scenario kunnen ook inhoud downloaden van peers die al over de benodigde inhoud beschikken. De Configuration Manager-client blijft het downloaden van de inhoud blijven beheren, maar kan ook gebruikmaken van de functie voor Configuration Manager peer-cache of andere technologieën zoals Delivery Optimization. Deze functie ondersteunt elk update type dat wordt ondersteund door Configuration Manager beheer van software-updates, waaronder Windows-en Office-updates. 

Zie de optie **geen implementatie pakket** wanneer u [software-updates hand matig implementeert](../../../sum/deploy-use/manually-deploy-software-updates.md) of [automatisch software-updates implementeert](../../../sum/deploy-use/automatically-deploy-software-updates.md)voor meer informatie.


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Regels voor automatische implementatie filteren op software-update architectuur
 <!--1322266-->
U kunt nu de regels voor automatische implementatie (ADR) filteren om architecturen zoals Itanium en ARM64 uit te sluiten. Op de pagina **software-updates** van de wizard regel voor automatische implementatie maken is het eigenschappen Filter voor de **architectuur** nu beschikbaar. 

Zie [software-updates automatisch implementeren](../../../sum/deploy-use/automatically-deploy-software-updates.md)voor meer informatie.


### <a name="improved-wsus-maintenance"></a>Verbeterd WSUS-onderhoud 
<!--1357898-->
De wizard WSUS opschonen wijst nu updates af die zijn verlopen volgens de vervangings regels die zijn gedefinieerd in de eigenschappen van de software-update punt component. 

Zie onderhoud van software- [updates](../../../sum/deploy-use/software-updates-maintenance.md)voor meer informatie.



## <a name="reporting"></a>Rapportage

### <a name="new-software-updates-compliance-report"></a>Rapport voor naleving van nieuwe software-updates
<!--1357775-->
Het weer geven van rapporten voor de compatibiliteit van software-updates bevat traditioneel gegevens van clients die recent geen contact hebben gemaakt met de site. In een nieuw rapport, **naleving 9: algemene status en naleving**, kunt u nalevings resultaten voor een specifieke software-update groep filteren op ' gezonde ' clients. In dit rapport wordt de realistischere compatibiliteits status weer gegeven van de actieve clients in uw omgeving. 

Zie [software-updates rapporten](../../../sum/deploy-use/monitor-software-updates.md#BKMK_SUReports)voor meer informatie.



## <a name="inventory"></a>Inventaris

### <a name="improvement-to-hardware-inventory-for-large-integer-values"></a><a name="bkmk_bigint"></a> Verbetering van de hardware-inventaris voor grote waarden met gehele getallen
<!--1357880-->
Voor hardware-inventarisatie was eerder een limiet voor gehele getallen groter dan 4.294.967.296 (2 ^ 32). Deze limiet kan worden bereikt voor kenmerken zoals de grootte van harde schijven in bytes. Het beheer punt heeft geen gehele waarden verwerkt die hoger zijn dan deze limiet, waardoor er geen waarde is opgeslagen in de data base. Nu in deze release wordt de limiet verhoogd naar 18446744073709551616 (2 ^ 64). 

Zie voor meer informatie [gebruik van grote waarden voor geheel getal](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Revisie van standaard eenheid voor hardware-inventaris
<!--514442-->
In [Configuration Manager versie 1710](whats-new-in-version-1710.md#site-infrastructure)is de standaard eenheid die in veel rapport weergaven wordt gebruikt, gewijzigd van mega bytes (MB) in GIGABYTES (GB). Als gevolg van [verbeteringen in de hardware-inventaris voor grote integerwaarden](#bkmk_bigint)en op basis van feedback van klanten, is deze standaard eenheid nu MB opnieuw.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Configuration Manager-console

### <a name="product-lifecycle-dashboard"></a>Dash board voor product levenscyclus
<!--1319632-->
Het dash board product levenscyclus toont de status van het micro soft Lifecycle-beleid voor micro soft-producten geïnstalleerd op apparaten die worden beheerd met Configuration Manager. Ook vindt u hier informatie over de micro soft-producten in uw omgeving, de ondersteunings status en de ondersteuning voor eind datums. Gebruik het dash board om inzicht te krijgen in de beschik baarheid van de ondersteuning voor elk product. Deze informatie helpt u bij het bijwerken van de micro soft-producten die u gebruikt voordat het huidige einde van de ondersteuning wordt bereikt.   

Zie [dash board voor product levenscyclus](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)voor meer informatie.


### <a name="copy-asset-details-from-monitoring-views"></a>Activum gegevens kopiëren vanuit controle weergaven
<!--1357856-->
De volgende gebieden van de werk ruimte **bewaking** ondersteunen nu het kopiëren van tekst:  

- Selecteer een implementatie in het knoop punt **implementaties** en klik op **status weer geven**. Selecteer een of meer apparaten in het deel venster **activum gegevens** van de weer gave implementatie status.  

- Vouw het knoop punt **distributie status** uit en selecteer **inhouds status**. Selecteer een software pakket en klik op **status weer geven**. Selecteer in het deel venster **activum gegevens** van de weer gave status van inhoud een of meer distributie punten. 

Klik met de rechter muisknop op de Asset en selecteer **kopiëren**. Met deze actie worden de geselecteerde assets als een door komma's gescheiden lijst met de volledige details gekopieerd. De sneltoets **CTRL**  +  **C** werkt ook in deze weer gaven. 

Zie voor meer informatie [console verbeteringen in versie 1806](../../servers/manage/admin-console-tips.md#copy-details-in-monitoring-views).


### <a name="improvements-to-the-surface-dashboard"></a>Verbeteringen aan het Surface-dash board
<!--1358654-->
Deze release bevat de volgende verbeteringen aan het Surface-dash board:  

- Het Surface-dash board geeft nu een lijst met relevante apparaten weer wanneer u specifieke grafiek secties selecteert:  

   - Als u op de tegel **percentage van Opper vlakken** klikt, wordt een lijst met Surface-apparaten geopend.  

   - Als u op een balk in de **bovenste vijf firmware versies** tegel klikt, wordt er een lijst met Surface-apparaten met die specifieke firmware versie geopend.  

- Wanneer u deze apparaten uit het Surface-dash board bekijkt, klikt u met de rechter muisknop op een apparaat om algemene acties uit te voeren.  

Zie [Surface dash board](../../clients/manage/surface-device-dashboard.md)voor meer informatie.


### <a name="view-the-currently-signed-on-user-for-a-device"></a>De momenteel aangemelde gebruiker voor een apparaat weer geven
<!--1358202-->
Het knoop punt **apparaten** van de werk ruimte **activa en naleving** bevat nu standaard een kolom voor de **gebruiker die momenteel is aangemeld**. De lijst wordt ook weer gegeven voor een verzameling apparaten. Deze waarde is als actueel als de [client status](../../clients/manage/monitor-clients.md#bkmk_indStatus). Wanneer de gebruiker zich afmeldt, wordt deze waarde door de client gewist. Als er geen gebruiker is aangemeld, is de waarde leeg. 

Zie voor meer informatie [console verbeteringen in versie 1806](../../servers/manage/admin-console-tips.md#view-users-for-a-device).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Feedback verzenden vanuit de Configuration Manager-console  
<!--1357542-->

Glim lach verzenden U kunt nu direct het Configuration Manager team informeren over uw ervaringen. Het verzenden van feedback is eenvoudig vanuit de Configuration Manager-console. We willen al uw feedback horen: Praise, problemen en suggesties. Klik in de Configuration Manager-console op de knop glim lach in de rechter bovenhoek boven het lint. Deze feedback gaat rechtstreeks naar het micro soft-product team voor Configuration Manager. Hoewel de Windows 10 feedback-hub nog steeds wordt ondersteund, wordt u aangeraden het feedback mechanisme in de console te gebruiken.  

Zie voor meer informatie [console verbeteringen in versie 1806](../../servers/manage/admin-console-tips.md#send-feedback) en [product feedback](../../understand/find-help.md#BKMK_1806Feedback).



## <a name="other-updates"></a>Andere Updates

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 1806](https://support.microsoft.com/help/4459701)voor meer informatie.

Zie [Power shell 1806 Release Notes](/powershell/sccm/1806_release_notes)(Engelstalig) voor meer informatie over wijzigingen in de Windows Power shell-cmdlets voor Configuration Manager.

Het volgende update pakket (4462978) is beschikbaar in de-console vanaf 24 oktober 2018: [Update pakket voor Configuration Manager current branch, versie 1806](https://support.microsoft.com/help/4462978).


### <a name="hotfixes"></a>Hotfixes

De volgende aanvullende hotfixes zijn beschikbaar om specifieke problemen op te lossen:

| Id | Titel | Date | In-console |
|---------|---------|---------|---------|
| [4346645](https://support.microsoft.com/help/4346645) | Update voor Configuration Manager versie 1806, eerste golf | 31 augustus 2018 | Ja |
| [4465865](https://support.microsoft.com/help/4465865) | Software-updates worden niet gedownload in Configuration Manager omgeving als de verbinding met WSUS is verbroken<br><br>Deze update bevindt zich ook in het update pakket (4462978) | 01 oktober 2018 | Ja |
| [4471892](https://support.microsoft.com/help/4471892) | PXE-responder werkt niet in subnetten in Configuration Manager 1806 | 23 november 2018 | Nee |
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificaat wordt niet vernieuwd in Configuration Manager | 18 januari 2019 | Ja |


## <a name="next-steps"></a>Volgende stappen

Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md) en [controle lijst voor het installeren van update 1806](../../servers/manage/checklist-for-installing-update-1806.md).

> [!TIP]  
> Als u een nieuwe site wilt installeren, gebruikt u een basislijn versie van Configuration Manager.  
>
> Meer informatie over:    
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)

Zie de [release opmerkingen](../../servers/deploy/install/release-notes.md)voor bekende, belang rijke problemen.

Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1806.md#post-update-checklist).
