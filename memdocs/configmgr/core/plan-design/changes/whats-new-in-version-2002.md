---
title: Wat is er nieuw in versie 2002
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 2002 van Configuration Manager current branch.
ms.date: 07/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: de718cdc-d0a9-47e2-9c99-8fa2cb25b5f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4a9eac25de66eb4fb94ea1c5b4b8d0d46caa05d7
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110712"
---
# <a name="whats-new-in-version-2002-of-configuration-manager-current-branch"></a>Wat is er nieuw in versie 2002 van Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 2002 voor Configuration Manager current branch is beschikbaar als een update in de console. Deze update Toep assen op sites waarop versie 1810 of hoger wordt uitgevoerd. <!-- baseline only statement:-->Wanneer u een nieuwe site installeert, is deze ook beschikbaar als basislijn versie. In dit artikel vindt u een overzicht van de wijzigingen en nieuwe functies in Configuration Manager, versie 2002.

Bekijk altijd de laatste controle lijst voor het installeren van deze update. Zie [Check List for Install update 2002](../../servers/manage/checklist-for-installing-update-2002.md)(Engelstalig) voor meer informatie. Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).

Als u optimaal wilt profiteren van de nieuwe functies van Configuration Manager, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

> [!TIP]
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+2002+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-manager-tenant-attach"></a><a name="bkmk_tenant"></a>Micro soft Endpoint Manager-Tenant koppelen

### <a name="device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Synchronisatie van apparaten en acties van apparaten
<!--3555758-->
Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen in één console met de naam **micro soft Endpoint Manager-beheer centrum**. Vanaf deze release kunt u uw Configuration Manager-apparaten uploaden naar de Cloud service en acties uitvoeren op de Blade **apparaten** in het beheer centrum.

Zie voor meer informatie [micro soft Endpoint Manager-Tenant koppelen](../../../tenant-attach/device-sync-actions.md).

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Site-infra structuur

### <a name="remove-a-central-administration-site"></a>Een centrale beheer site verwijderen
<!-- 3607277 -->

Als uw hiërarchie bestaat uit een centrale beheer site (CA'S) en één onderliggende primaire site, kunt u nu de certificerings instanties verwijderen. Met deze actie wordt uw Configuration Manager-infra structuur vereenvoudigd tot één zelfstandige primaire site. Het verwijdert de complexiteit van site-naar-site-replicatie en richt zich op de beheer taken voor één primaire site.

Zie [de certificerings instanties verwijderen](../../servers/deploy/install/remove-central-administration-site.md)voor meer informatie.

### <a name="new-management-insight-rules"></a>Nieuwe management Insight-regels

Deze release bevat de volgende beheer Insight-regels:

- Negen regels in de **Configuration Manager evaluatie** groep van micro soft premier field engineering. Deze regels zijn een voor beeld van de vele meer controles die micro soft Premier biedt in de services hub.<!-- 3607758 -->

  - Active Directory detectie van beveiligings groepen is zo geconfigureerd dat deze te vaak wordt uitgevoerd
  - Active Directory systeem detectie is zo geconfigureerd dat het te vaak wordt uitgevoerd
  - Active Directory gebruikers detectie is zo geconfigureerd dat ze te vaak worden uitgevoerd
  - Verzamelingen beperkt tot alle systemen of alle gebruikers
  - Heartbeat-detectie is uitgeschakeld
  - Langlopende verzamelings query's die zijn ingeschakeld voor incrementele updates
  - Verminder het aantal toepassingen en pakketten op distributie punten
  - Problemen met de installatie van secundaire sites
  - Alle sites bijwerken naar dezelfde versie

- Er zijn twee extra regels in de **Cloud Services** groep die u helpen bij het configureren van uw site voor het toevoegen van beveiligde HTTPS-communicatie:<!-- 6268489 -->

  - Sites waarvoor geen geldige HTTPS-configuratie is
  - Apparaten die niet zijn geüpload naar Azure AD

Zie [Management Insights](../../servers/manage/management-insights.md)voor meer informatie.

### <a name="improvements-to-administration-service"></a>Verbeteringen in de beheer service

<!-- 5728365 -->

De beheer service is een REST API voor de SMS-provider. Voorheen moest u een van de volgende afhankelijkheden implementeren:

- Uitgebreide HTTP inschakelen voor de hele site
- Hand matig een PKI-certificaat binden aan IIS op de server die als host fungeert voor de functie SMS-provider

Vanaf deze release gebruikt de beheer service automatisch het zelfondertekende certificaat van de site. Deze wijziging helpt de wrijving te verminderen voor eenvoudiger gebruik van de beheer service. Dit certificaat wordt altijd door de site gegenereerd. De verbeterde HTTP-site-instelling voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen** bepaalt alleen of site systemen deze gebruiken. De beheer service negeert deze site-instelling, omdat deze altijd het certificaat van de site gebruikt, zelfs als er geen ander site systeem is die verbeterde HTTP gebruikt. U kunt nog steeds een op PKI gebaseerd certificaat voor Server verificatie gebruiken.

Zie de volgende nieuwe artikelen voor meer informatie:

- [Wat is de beheerservice?](../../../develop/adminservice/overview.md)
- [De beheer service instellen](../../../develop/adminservice/set-up.md)

### <a name="proxy-support-for-azure-active-directory-discovery-and-group-sync"></a>Proxy ondersteuning voor detectie van Azure Active Directory en groeps synchronisatie

<!-- 5913817 -->

De proxy-instellingen van het site systeem, inclusief verificatie, worden nu gebruikt door:

- Gebruikers detectie van Azure Active Directory (Azure AD)
- Detectie van Azure AD-gebruikers groepen
- De resultaten van het verzamelings lidmaatschap synchroniseren met Azure Active Directory groepen

Zie [ondersteuning voor proxy server](../network/proxy-server-support.md#bkmk_other)voor meer informatie.

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a>Cloud-gekoppeld beheer

### <a name="critical-status-message-shows-server-connection-errors-to-required-endpoints"></a>Kritiek status bericht toont server verbindings fouten aan vereiste eind punten

<!-- 5566763 -->

Als de Configuration Manager-site server geen verbinding kan maken met de vereiste eind punten voor een Cloud service, wordt een status bericht met de ID 11488 gegenereerd. Wanneer de site server geen verbinding kan maken met de service, wordt de status van de SMS_SERVICE_CONNECTOR onderdeel gewijzigd in kritiek. Bekijk de gedetailleerde status in het knoop punt onderdeel status van de Configuration Manager-console.

### <a name="token-based-authentication-for-cloud-management-gateway"></a>Verificatie op basis van tokens voor Cloud beheer gateway

<!-- 5686290 -->

De Cloud Management Gateway (CMG) ondersteunt veel soorten clients, maar zelfs met verbeterde HTTP, hebben deze clients een certificaat voor client verificatie nodig. Deze certificaat vereiste kan lastig zijn om in te richten op Internet-clients die niet vaak verbinding maken met het interne netwerk, geen lid kunnen worden van Azure Active Directory (Azure AD) en geen methode hebben voor het installeren van een door PKI uitgegeven certificaat.

Configuration Manager breidt de ondersteuning van het apparaat uit met de volgende methoden:

- Registreer u voor een uniek token op het interne netwerk
- Een token voor bulk registratie maken voor apparaten op Internet

Zie [verificatie op basis van tokens voor CMG](../../clients/deploy/deploy-clients-cmg-token.md)voor meer informatie.

### <a name="microsoft-endpoint-configuration-manager-cloud-features"></a>Cloud functies van micro soft endpoint Configuration Manager

<!--5834830-->

Wanneer er nieuwe Cloud functies beschikbaar zijn in het beheer centrum van micro soft Endpoint Manager of door andere gekoppelde cloud services voor uw on-premises Configuration Manager-installatie, kunt u zich nu aanmelden bij deze nieuwe functies in de Configuration Manager-console. Zie [optionele functies van updates inschakelen](../../servers/manage/install-in-console-updates.md#bkmk_options)voor meer informatie over het inschakelen van functies in de Configuration Manager-console.

## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Desktop Analytics

Zie [what's New in Desktop Analytics](../../../desktop-analytics/whats-new.md)(Engelstalig) voor meer informatie over de maandelijkse wijzigingen in de Cloud service van Desktop Analytics.

### <a name="connection-health-dashboard-shows-client-connection-issues"></a>Dash board verbindings status toont problemen met de client verbinding

Gebruik het dash board verbindings status van de bureau blad Analytics in Configuration Manager om de verbindings status van de clients te controleren. U kunt nu gemakkelijker problemen met de configuratie van client proxy op twee gebieden identificeren:

- **Controle van eind punten**: als clients geen vereist eind punt kunnen bereiken, ziet u een configuratie waarschuwing in het dash board. Inzoomen om de eind punten weer te geven waarmee clients geen verbinding kunnen maken vanwege problemen met de proxy configuratie.<!-- 4963230 -->

- **Connectiviteits status**: als uw clients een proxy server gebruiken voor toegang tot de Cloud service van Desktop Analytics, worden in Configuration Manager nu problemen met de proxy verificatie van clients weer gegeven. Inzoomen op de weer gave van clients die niet kunnen worden inge schreven vanwege proxy verificatie.<!-- 4963383 -->

Zie [verbindings status controleren](../../../desktop-analytics/monitor-connection-health.md)voor meer informatie.

## <a name="real-time-management"></a><a name="bkmk_real"></a>Real-time beheer

### <a name="improvements-to-cmpivot"></a>Verbeteringen in CMPivot

<!-- 5870934 -->

We hebben het eenvoudiger gemaakt om te navigeren in CMPivot-entiteiten. U kunt nu CMPivot-entiteiten zoeken. Er zijn ook nieuwe pictogrammen toegevoegd om de entiteiten en de object typen van de entiteit eenvoudig te onderscheiden.

Zie [CMPivot](../../servers/manage/cmpivot.md#bkmk_2002)voor meer informatie.

## <a name="content-management"></a><a name="bkmk_content"></a>Inhouds beheer

### <a name="exclude-certain-subnets-for-peer-content-download"></a>Bepaalde subnetten uitsluiten voor het downloaden van inhoud van peer

<!-- 3555777 -->

Grens groepen bevatten de volgende optie voor peer downloads: **tijdens het downloaden van peers worden alleen peers binnen hetzelfde subnet gebruikt**. Als u deze optie inschakelt, omvat de lijst met inhouds locaties van het beheer punt alleen peer bronnen die zich in dezelfde subnet-en grens groep bevinden als de client. Afhankelijk van de configuratie van uw netwerk, kunt u nu bepaalde subnetten uitsluiten voor overeenkomende treffers. U wilt bijvoorbeeld een grens opnemen, maar een specifiek VPN-subnet uitsluiten.

Zie [Opties voor grens groepen](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions)voor meer informatie.

### <a name="proxy-support-for-microsoft-connected-cache"></a>Proxy-ondersteuning voor micro soft Connected cache

<!-- 5856396 -->

Als uw omgeving een niet-geverifieerde proxy server gebruikt voor Internet toegang, kunt u nu wanneer u een Configuration Manager distributie punt voor micro soft Connected cache inschakelt, communiceren via de proxy. Zie [micro soft Connected cache](../hierarchy/microsoft-connected-cache.md)(Engelstalig) voor meer informatie.

## <a name="client-management"></a><a name="bkmk_client"></a>Client beheer

### <a name="client-log-collection"></a>Client logboek verzameling

<!-- 4226618 -->

U kunt nu een client apparaat activeren om de client logboeken te uploaden naar de site server door een actie voor client meldingen te verzenden vanuit de Configuration Manager-console.

Zie [client notification](../../clients/manage/client-notification.md#client-diagnostics)(Engelstalig) voor meer informatie.

### <a name="wake-up-a-device-from-the-central-administration-site"></a>Een apparaat activeren vanaf de centrale beheer site

<!-- 6030715 -->

Vanuit de centrale beheer site (CAS), in het knoop punt apparaten of apparaten, kunt u nu de actie voor client meldingen gebruiken om apparaten te activeren. Deze actie was eerder alleen beschikbaar op een primaire site.

Zie [Wake on LAN configureren](../../clients/deploy/configure-wake-on-lan.md#bkmk_wol-1810)voor meer informatie.

### <a name="improvements-to-support-for-arm64-devices"></a>Verbeteringen voor de ondersteuning van ARM64-apparaten

<!--5954175-->

Het **alle Windows 10-platform (ARM64)** is beschikbaar in de lijst met ondersteunde versies van besturings systemen voor objecten met vereisten regels of toepasings lijsten.

> [!NOTE]
> Als u eerder het **Windows 10** -platform van het hoogste niveau hebt geselecteerd, wordt met deze actie automatisch zowel **alle Windows 10-(64-bits)** als **alle Windows 10 (32-bits)** geselecteerd. Dit nieuwe platform wordt niet automatisch geselecteerd. Als u **alle Windows 10 (ARM64)** wilt toevoegen, selecteert u deze hand matig in de lijst.

Zie [Windows 10 on ARM64](../configs/support-for-windows-10.md#bkmk_arm64)voor meer informatie over de ondersteuning van Configuration Manager voor ARM64-apparaten.

### <a name="track-configuration-item-remediations"></a>Herbemiddelingen van configuratie-items bijhouden
<!--4261411-->
U kunt nu de **herstel geschiedenis traceren wanneer** deze worden ondersteund in de nalevings regels van uw configuratie-item. Wanneer deze optie is ingeschakeld, genereert een herstel dat zich voordoet op de client voor het configuratie-item een status bericht. De geschiedenis wordt opgeslagen in de Configuration Manager-Data Base.

Zie [aangepaste configuratie-items maken voor Windows-bureau blad en Server computers die worden beheerd met de Configuration Manager-client](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md#bkmk_track)voor meer informatie over deze instelling.

<!-- ## <a name="bkmk_comgmt"></a> Co-management -->

## <a name="application-management"></a><a name="bkmk_app"></a>Toepassings beheer

### <a name="microsoft-edge-management-dashboard"></a>Micro soft Edge Management dash board

<!-- 3871913 -->

Het micro soft Edge Management-dash board biedt inzicht in het gebruik van micro soft Edge en andere browsers. In dit dash board kunt u het volgende doen:

- Bekijk hoeveel van uw apparaten micro soft Edge hebben geïnstalleerd
- Bekijk hoeveel clients verschillende versies van micro soft Edge hebben geïnstalleerd
- Een weer gave hebben van de geïnstalleerde browsers op verschillende apparaten
- Een weer gave van de voorkeurs browser per apparaat

Klik in de werk ruimte software bibliotheek op micro soft Edge management om het dash board weer te geven. Wijzig de verzameling voor de grafiek gegevens door te klikken op Bladeren en een andere verzameling te kiezen. Uw vijf grootste verzamelingen bevinden zich standaard in de vervolg keuzelijst. Wanneer u een verzameling selecteert die zich niet in de lijst bevindt, neemt de zojuist geselecteerde verzameling de onderste plaats in de vervolg keuzelijst.

Zie [micro soft Edge Management](../../../apps/deploy-use/deploy-edge.md#bkmk_edge-dash)(Engelstalig) voor meer informatie.

### <a name="improvements-to-microsoft-edge-management"></a>Verbeteringen in het beheer van micro soft Edge

<!-- 4561024 -->

U kunt nu een micro soft Edge-toepassing maken die is ingesteld voor het ontvangen van automatische updates in plaats van dat automatische updates zijn uitgeschakeld. Met deze wijziging kunt u ervoor kiezen om updates voor micro soft Edge te beheren met Configuration Manager of micro soft Edge automatisch te laten bijwerken. Wanneer u de toepassing maakt, selecteert u micro soft Edge toestaan de versie van de client op het apparaat van de eind gebruiker automatisch bij te werken op de pagina micro soft Edge-instellingen.

Zie [micro soft Edge Management](../../../apps/deploy-use/deploy-edge.md#bkmk_autoupdate)(Engelstalig) voor meer informatie.

### <a name="task-sequence-as-an-app-model-deployment-type"></a>Taken reeks als een app-model implementatie type

<!-- 3555953 -->

U kunt nu complexe toepassingen installeren met behulp van taken reeksen via het toepassings model. Voeg een implementatie type toe aan een app die een taken reeks is, ofwel om de app te installeren of te verwijderen. Deze functie biedt het volgende gedrag:

- De taken reeks van de app weer geven met een pictogram in Software Center. Een pictogram maakt het gemakkelijker voor gebruikers om de taken reeks van de app te vinden en te identificeren.

- Aanvullende meta gegevens definiëren voor de taken reeks van de app, inclusief gelokaliseerde informatie

Zie [Windows-toepassingen maken](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)voor meer informatie.

## <a name="os-deployment"></a><a name="bkmk_osd"></a>Implementatie van besturings systeem

### <a name="bootstrap-a-task-sequence-immediately-after-client-registration"></a>Een taken reeks onmiddellijk Boots trappen na client registratie

<!-- 5526972 -->

Wanneer u een nieuwe Configuration Manager-client installeert en registreert en er ook een taken reeks naar implementeert, is het moeilijk om te bepalen hoe snel na de registratie de taken reeks wordt uitgevoerd. Deze release introduceert een nieuwe client installatie-eigenschap die u kunt gebruiken om een taken reeks op een client te starten nadat deze is geregistreerd bij de site.

Zie [over eigenschappen van client installatie-PROVISIONTS](../../clients/deploy/about-client-installation-properties.md#provisionts)voor meer informatie.

### <a name="improvements-to-check-readiness-task-sequence-step"></a>Verbeteringen voor het controleren van de gereedheids taken reeks stap

<!-- 6005561 -->

U kunt nu meer apparaateigenschappen controleren in de taken reeks stap **gereedheids controleren** . Gebruik deze stap in een taken reeks om te controleren of de doel computer voldoet aan uw vereisten.

- Architectuur van het huidige besturings systeem
- Minimale versie van het besturingssysteem
- Maximale versie van het besturingssysteem
- Minimale client versie
- Taal van het huidige besturings systeem
- Netstroom aangesloten
- Netwerk adapter is verbonden en niet draadloos

Zie [taken reeks stappen-gereedheid controleren](../../../osd/understand/task-sequence-steps.md#BKMK_CheckReadiness)voor meer informatie.

### <a name="improvements-to-task-sequence-progress"></a>Verbeteringen in de voortgang van taken reeksen

<!-- 5932692 -->

Het venster voortgang van taken reeks bevat nu de volgende verbeteringen:

- U kunt deze inschakelen om het huidige stap nummer, het totale aantal stappen en het voltooiings percentage weer te geven
- De breedte van het venster verg root zodat u meer ruimte krijgt om de naam van de organisatie in één regel weer te geven

Zie [gebruikers ervaringen voor implementatie van besturings systemen](../../../osd/understand/user-experience.md#task-sequence-progress)voor meer informatie.

### <a name="improvements-to-os-deployment"></a>Verbeteringen in de implementatie van het besturings systeem

Deze release bevat de volgende verbeteringen voor de implementatie van het besturings systeem:

- De taken reeks omgeving bevat een nieuwe alleen-lezen variabele `_TSSecureBoot` .<!--5842295--> Gebruik deze variabele om de status van beveiligd opstarten op een apparaat met UEFI-functionaliteit te bepalen. Zie [_TSSecureBoot](../../../osd/understand/task-sequence-variables.md#TSSecureBoot)voor meer informatie.

- Stel taken reeks variabelen in om de gebruikers context te configureren voor de **opdracht regel uitvoeren** en **Power shell-script** tappen uit te voeren.<!-- 5573175 --> Zie [SMSTSRunCommandLineAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunCommandLineAsUser) en [SMSTSRunPowerShellAsUser](../../../osd/understand/task-sequence-variables.md#SMSTSRunPowerShellAsUser)voor meer informatie.

- In de stap **Power shell-script uitvoeren** kunt u nu de eigenschap **para meters** instellen op een variabele.<!-- 5690481 --> Zie [Power shell-script uitvoeren](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)voor meer informatie.

- De Configuration Manager PXE-responder verzendt nu status berichten naar de site server. Met deze wijziging kunt u de implementaties van besturings systemen die gebruikmaken van deze service eenvoudiger maken.<!-- 5568051 -->

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>Software-updates

### <a name="orchestration-groups"></a>Orchestration-groepen

<!-- 3098816 -->

Maak een Orchestration-groep om de implementatie van software-updates op apparaten beter te beheren. Veel server beheerders moeten updates voor specifieke werk belastingen zorgvuldig beheren en het gedrag tussen automatiseren.

Een Orchestration-groep biedt u de flexibiliteit om apparaten bij te werken op basis van een percentage, een specifiek getal of een expliciete volg orde. U kunt ook een Power shell-script uitvoeren voor en nadat de update-implementatie op de apparaten is uitgevoerd.

Leden van een Orchestration-groep kunnen elk Configuration Manager-client zijn, niet alleen servers. De groeps beleidsregels zijn van toepassing op de apparaten voor alle software-update-implementaties voor een verzameling die een groeps groepslid bevat. Andere implementatie gedragingen zijn nog steeds van toepassing. Voor beeld: onderhouds Vensters en implementatie planningen.

Zie [Orchestration-groepen](../../../sum/deploy-use/orchestration-groups.md)voor meer informatie.

### <a name="evaluate-software-updates-after-a-servicing-stack-update"></a>Software-updates evalueren na een onderhouds stack-update

<!-- 4639943 -->

Configuration Manager detecteert nu of een onderhouds stack-update (SSU) deel uitmaakt van een installatie voor meerdere updates. Wanneer een SSU wordt gedetecteerd, wordt het eerst geïnstalleerd. Na de installatie van de SSU wordt een evaluatie cyclus voor software-updates uitgevoerd om de resterende updates te installeren. Met deze wijziging kan een afhankelijke cumulatieve update worden geïnstalleerd na de onderhouds stack-update. Het apparaat hoeft niet opnieuw te worden opgestart tussen installaties en u hoeft geen extra onderhouds venster te maken. SSUs worden eerst alleen geïnstalleerd voor installaties die niet door de gebruiker zijn gestart. Als een gebruiker bijvoorbeeld een installatie voor meerdere updates vanuit software Center initieert, wordt de SSU mogelijk niet eerst geïnstalleerd.

Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md#bkmk_ssu)voor meer informatie.

### <a name="office-365-updates-for-disconnected-software-update-points"></a>Office 365-updates voor niet-verbonden software-update punten

<!-- 4065163 -->

U kunt een nieuw hulp programma gebruiken om Office 365-updates te importeren van een met internet verbonden WSUS-server in een niet-verbonden Configuration Manager omgeving. Als u eerder meta gegevens voor software die is bijgewerkt in omgevingen zonder verbinding hebt geëxporteerd en geïmporteerd, kunt u geen Office 365-updates implementeren. Office 365-updates vereisen aanvullende meta gegevens die zijn gedownload van een Office-API en het Office CDN, wat niet mogelijk is met niet-verbonden omgevingen.

Zie voor meer informatie [Office 365-updates synchroniseren vanaf een niet-verbonden software-update punt](../../../sum/get-started/synchronize-office-updates-disconnected.md).

<!-- ## <a name="bkmk_o365"></a> Office management -->

## <a name="protection"></a><a name="bkmk_protect"></a>Kantel

### <a name="expand-microsoft-defender-advanced-threat-protection-atp-onboarding"></a>Vouw het voorbereidings proces van micro soft Defender Advanced Threat Protection (ATP) uit
 
<!-- 5229962 -->
Configuration Manager heeft de ondersteuning voor onboarding-apparaten uitgebreid naar micro soft Defender ATP. Zie [micro soft Defender Advanced Threat Protection](../../../protect/deploy-use/defender-advanced-threat-protection.md)(Engelstalig) voor meer informatie.

### <a name="onboard-configuration-manager-clients-to-microsoft-defender-atp-via-the-microsoft-endpoint-manager-admin-center"></a><a name="bkmk_atp"></a>Configuration Manager-clients onboarden naar micro soft Defender ATP via het beheer centrum van micro soft Endpoint Manager
<!--5691658-->
U kunt nu het voorbereidings beleid voor micro soft Defender ATP-eindpunt detectie en-antwoorden (EDR) implementeren voor het Configuration Manager van beheerde clients. Voor deze clients is Azure AD of MDM-inschrijving niet vereist en het beleid is gericht op ConfigMgr-verzamelingen in plaats van met Azure AD-groepen.

Met deze mogelijkheid kunnen klanten zowel intune MDM als Configuration Manager client EDR/ATP onboarding beheren vanuit één beheer ervaring-het micro soft Endpoint Manager-beheer centrum. Zie voor meer informatie [eindpunt detectie en reactie beleid voor eindpunt beveiliging in intune](../../../../intune/protect/endpoint-security-edr-policy.md).

> [!Important]
> U hebt de hotfix Rollup, [KB4563473](https://support.microsoft.com/help/4563473), geïnstalleerd in uw omgeving voor deze functie.

### <a name="improvements-to-bitlocker-management"></a>Verbeteringen aan BitLocker-beheer

- Het BitLocker-beheer beleid bevat nu aanvullende instellingen, waaronder beleids regels voor vaste en verwissel bare stations.<!-- 5925683 --> Zie referentie voor BitLocker- [instellingen](../../../protect/tech-ref/bitlocker/settings.md)voor meer informatie.

- In Configuration Manager huidige branch versie 1910 om de BitLocker Recovery-service te integreren, moet u een beheer punt inschakelen. De HTTPS-verbinding is nodig voor het versleutelen van de herstel sleutels in het netwerk van de Configuration Manager-client naar het beheer punt. Het configureren van het beheer punt en alle clients voor HTTPS kunnen veel klanten lastig zijn.

    Vanaf deze versie is de HTTPS-vereiste voor de IIS-website die als host fungeert voor de Recovery-service, niet de volledige rol van het beheer punt. Met deze wijziging worden de certificaat vereisten versoepeld en worden de herstel sleutels tijdens de overdracht nog steeds versleuteld.<!-- 5925660 --> Zie [herstel gegevens versleutelen](../../../protect/deploy-use/bitlocker/encrypt-recovery-data.md)voor meer informatie.

## <a name="reporting"></a><a name="bkmk_report"></a>Rapporteren

### <a name="integrate-with-power-bi-report-server"></a>Integreren met Power BI Report Server

<!-- 3721603 -->

U kunt Power BI Report Server nu integreren met Configuration Manager-rapportage. Deze integratie biedt u moderne visualisaties en betere prestaties. Het voegt console ondersteuning toe voor Power BI rapporten die vergelijkbaar zijn met wat er al bestaat met SQL Server Reporting Services.

Zie [integreren met Power bi Report Server](../../servers/manage/powerbi-report-server.md)voor meer informatie.

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Configuration Manager-console

### <a name="show-boundary-groups-for-devices"></a>Grens groepen voor apparaten weer geven

<!--6521835-->

U kunt nu de grens groepen voor specifieke apparaten weer geven om u te helpen bij het oplossen van problemen met het gedrag van apparaten met grens groepen. Voeg de kolom nieuwe **grens groep (en)** toe aan de lijst weergave van het knoop punt **apparaten** of wanneer u de leden van een **apparaat verzameling**weergeeft.

Zie [grens groepen](../../servers/deploy/configure/boundary-groups.md#bkmk_show-boundary)voor meer informatie.

### <a name="send-a-smile-improvements"></a>Een glim lach-verbeteringen verzenden

<!-- 5891852 -->

Wanneer u een glim lach verzendt of een frons verzendt, wordt een status bericht gemaakt wanneer de feedback wordt verzonden. Deze verbetering bevat een overzicht van:

- Wanneer de feedback is verzonden
- Die de feedback heeft verzonden
- De feedback-ID
- Als het verzenden van de feedback is geslaagd of niet

Een status bericht met de ID 53900 is een geslaagde indiening en 53901 is een mislukte verzen ding.

Zie [product feedback](../../understand/find-help.md#BKMK_1806Feedback)voor meer informatie.

### <a name="search-all-subfolders-for-configuration-items-and-configuration-baselines"></a>Alle submappen doorzoeken op configuratie-items en configuratie basislijnen

<!--5891241-->

Net als bij verbeteringen in eerdere versies kunt u nu de zoek optie **alle submappen** gebruiken van de knoop punten **configuratie-items** en **configuratie basislijnen** .

### <a name="community-hub"></a>Community Hub

<!--3555935, 3555936-->

_Eerste geïntroduceerd in juni 2020_

De IT-beheerder heeft een schat aan kennis ontwikkeld over de jaren. In plaats van items zoals scripts en rapporten helemaal opnieuw te hoeven maken, hebben we een Configuration Manager **Community-hub** gemaakt waar u met elkaar kunt delen. Door gebruik te maken van anderen, kunt u uren werk besparen. De Community-hub bevordert creativiteit door te bouwen op het werk van anderen en andere mensen op uw bedrijf te bouwen. GitHub heeft al branchespecifieke processen en hulpprogram ma's die zijn ontworpen voor delen. De Community-hub maakt nu gebruik van deze hulpprogram ma's rechtstreeks in de Configuration Manager-console als basis onderdelen voor het aansturen van deze nieuwe community.

Zie [Community hub en github](../../servers/manage/community-hub.md)voor meer informatie.

## <a name="tools"></a><a name="bkmk_tools"></a>Software

### <a name="onetrace-log-groups"></a>OneTrace-logboek groepen

<!-- 5559993 -->

OneTrace biedt nu ondersteuning voor aanpas bare logboek groepen, vergelijkbaar met de functie in het ondersteunings centrum. Met logboek groepen kunt u alle logboek bestanden openen voor één scenario. OneTrace bevat momenteel groepen voor de volgende scenario's:

- Toepassingsbeheer
- Instellingen voor naleving (ook wel gewenst configuratie beheer genoemd)
- Software-updates

Zie [ondersteunings centrum OneTrace](../../support/support-center-onetrace.md)voor meer informatie.

### <a name="improvements-to-extend-and-migrate-on-premises-site-to-microsoft-azure"></a><a name="bkmk_extend"></a>Verbeteringen voor het uitbreiden en migreren van een on-premises site naar Microsoft Azure
<!--5665775, 6307931-->
Het hulp programma voor het uitbreiden en migreren van een on-premises site naar Microsoft Azure ondersteunt nu het inrichten van meerdere site systeem rollen op één virtuele Azure-machine. U kunt site systeem rollen toevoegen nadat de eerste implementatie van de virtuele Azure-machine is voltooid.

Zie [on-premises site uitbreiden en migreren naar Microsoft Azure](../../support/azure-migration-tool.md#bkmk_add_role)voor meer informatie.

## <a name="other-updates"></a>Andere Updates

Vanaf deze versie zijn de volgende functies niet meer [voorlopige versie](../../servers/manage/pre-release-features.md):

- [Detectie van gebruikers groepen Azure Active Directory](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)<!--3611956-->
- [Resultaten van verzamelings lidmaatschap synchroniseren met Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)<!--3607475-->
- [Zelfstandige CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone)<!--3555890/4692885-->
- [Client-apps voor gezamenlijk beheerde apparaten](../../../comanage/workloads.md#client-apps) (voorheen bekend als *mobiele apps voor gezamenlijk beheerde apparaten*)<!-- 1357892/3600959 -->

Zie [release opmerkingen voor Power shell versie 2002](https://docs.microsoft.com/powershell/sccm/2002-release-notes?view=sccm-ps)voor meer informatie over wijzigingen in de Windows Power shell-cmdlets voor Configuration Manager.

Zie [release opmerkingen voor de beheer service](../../../develop/adminservice/release-notes.md#bkmk_2002)voor meer informatie over wijzigingen in de beheer service rest API.

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 2002](https://support.microsoft.com/help/4556203)voor meer informatie.

Het volgende update pakket (4560496) is beschikbaar in de-console vanaf 15 juli 2020: [Update pakket voor micro soft Endpoint Configuration Manager versie 2002](https://support.microsoft.com/help/4560496).

### <a name="hotfixes"></a>Hotfixes

De volgende aanvullende hotfixes zijn beschikbaar om specifieke problemen op te lossen:

| Id | Titel | Date | In-console |
|---------|---------|---------|---------|
| [4575339](https://support.microsoft.com/help/4575339) | Apparaten worden twee keer weer gegeven in micro soft endpoint Configuration Manager beheer centrum | 23 juli 2020 | Nee |
| [4575774](https://support.microsoft.com/help/4575774) | De cmdlet New-CMTSStepPrestartCheck mislukt in Configuration Manager, versie 2002 | 24 juli 2020 | Nee |
| [4576782](https://support.microsoft.com/help/4576782) | Time-out voor toepassings blad in micro soft Endpoint Manager-beheer centrum | 11 augustus 2020 | Nee |

<!--
> [!NOTE]
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Volgende stappen

<!-- At this time, version 2002 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2002.md#early-update-ring). -->

Vanaf 11 mei 2020 is versie 2002 wereld wijd beschikbaar voor alle klanten die moeten worden geïnstalleerd.

Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md) en [controle lijst voor het installeren van update 2002](../../servers/manage/checklist-for-installing-update-2002.md).

> [!TIP]
> Als u een nieuwe site wilt installeren, gebruikt u een basislijn versie van Configuration Manager.
>
> Meer informatie over:
>
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)

Zie de opmerkingen bij de [release](../../servers/deploy/install/release-notes.md)voor bekende belang rijke problemen.

Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-2002.md#post-update-checklist).
