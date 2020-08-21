---
title: Wat is er nieuw in versie 1810
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1810 van Configuration Manager current branch.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 04630815b3d10a232d7fc0eea50296062c823194
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699837"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Wat is er nieuw in versie 1810 van Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1810 voor Configuration Manager current branch is beschikbaar als een update in de console. Deze update Toep assen op sites waarop versie 1710, 1802 of 1806 wordt uitgevoerd. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.--> In dit artikel vindt u een overzicht van de wijzigingen en nieuwe functies in Configuration Manager, versie 1810.  

Bekijk altijd de laatste controle lijst voor het installeren van deze update. Zie [Check List for Install update 1810](../../servers/manage/checklist-for-installing-update-1810.md)(Engelstalig) voor meer informatie. Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).

Als u gebruik wilt maken van nieuwe Configuration Manager functies, moet u clients eerst bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

<!--
> [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized. 
-->  

> [!Tip]  
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1810+-+Configuration+Manager%22&locale=en-us`



## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Afgeschafte functies en besturings systemen

Meer informatie over ondersteunings wijzigingen voordat ze worden geïmplementeerd in [verwijderde en afgeschafte items](deprecated/removed-and-deprecated.md).

Vanaf 14 augustus 2018 wordt de functie hybride Mobile Device Management afgeschaft. Zie [Wat is er gebeurd met hybride MDM](../../../mdm/understand/what-happened-to-hybrid.md)voor meer informatie.<!--Intune feature 2683117-->  

Ondersteuning voor System Center Endpoint Protection (SCEP) voor Mac en Linux (alle versies) eindigt op 31 december 2018. De beschik baarheid van nieuwe virus definities voor SCEP voor Mac en SCEP voor Linux kan na het einde van de ondersteuning worden stopgezet. Zie [End of support blog post](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257)voor meer informatie.

Klassieke service-implementaties in azure zijn nu afgeschaft in Configuration Manager. Begin met het gebruik van Azure Resource Manager-implementaties voor de Cloud beheer gateway en het Cloud distributiepunt. Zie [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)voor meer informatie.



## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site-infra structuur

### <a name="support-for-windows-server-2019"></a>Ondersteuning voor Windows Server 2019

<!--1359195-->
Configuration Manager ondersteunt nu Windows Server 2019 en Windows Server, versie 1809, als site systemen.

Zie [ondersteunde besturings systemen voor site systeem servers](../configs/supported-operating-systems-for-site-system-servers.md)voor meer informatie.


### <a name="hierarchy-support-for-site-server-high-availability"></a>Hiërarchie-ondersteuning voor hoge Beschik baarheid van site server

<!--3607755, fka 1358224-->
Centrale beheer sites en onderliggende primaire sites kunnen nu een extra site server in de passieve modus hebben.

Zie [hoge Beschik baarheid van site server](../../servers/deploy/configure/site-server-high-availability.md)voor meer informatie.


### <a name="improvements-to-setup-prerequisites"></a>Verbeteringen aan installatie vereisten

Wanneer u installeert of bijwerkt naar versie 1810, wordt in Configuration Manager Setup nu de volgende controles voor vereisten opgenomen of verbeterd:

- **Opnieuw opstarten van systeem in behandeling**: deze controle op vereisten is nu robuuster. Er worden aanvullende register sleutels voor Windows-onderdelen gecontroleerd. Zie [wachten op opnieuw opstarten](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart)van het systeem voor meer informatie. <!--SCCMDocs-pr issue 3010-->  

- **Opschonen van SQL-wijzigingen bijhouden**: een nieuwe controle of de site database een achterstand heeft voor het bijhouden van SQL-wijzigingen. Zie voor meer informatie, inclusief een procedure om deze achterstand te controleren en te wissen, het [opschonen van SQL-wijzigingen bijhouden](../../servers/deploy/install/list-of-prerequisite-checks.md#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **SQL Native Client versie**: deze controle op vereisten is bijgewerkt voor versies van SQL Native Client die TLS 1,2 ondersteunen. De minimale versie is [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Zie [SQL Native Client-versie](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie. <!--SCCMDocs-pr issue 3094-->  

- **Site systeem op het Windows-cluster knooppunt**: het installatie proces van Configuration Manager blokkeert niet langer de installatie van de site serverrol op een computer met de Windows-functie voor failover clustering. Voor SQL always on is deze rol vereist, zodat u de site database niet kunt vinden op de site server. Met deze wijziging kunt u een Maxi maal beschik bare site met minder servers maken met behulp van SQL always on en een site server in de passieve modus. Zie [Windows-failovercluster](../../servers/deploy/install/list-of-prerequisite-checks.md#windows-failover-cluster)voor meer informatie. <!--1359132-->  


### <a name="new-permission-for-client-notification-actions"></a>Nieuwe machtiging voor client meldings acties

<!--SCCMDocs-pr issue #2972-->
Voor client meldings acties is nu de machtiging **resource waarschuwen** voor de klasse SMS_Collection vereist. De volgende ingebouwde rollen hebben standaard deze machtiging:

- Volledige beheerder  
- Infrastructuurbeheerder  

Voeg deze machtiging toe aan aangepaste rollen die client meldings acties moeten gebruiken.

Zie [client meldingen](../../clients/manage/client-notification.md)voor meer informatie.



## <a name="content-management"></a><a name="bkmk_content"></a> Inhouds beheer

### <a name="new-boundary-group-options"></a>Nieuwe opties voor grens groepen

<!--1358749-->
Grens groepen bevatten nu de volgende aanvullende instellingen om u meer controle te geven over de distributie van inhoud in uw omgeving:

- Geef de voor **keur aan distributie punten over peers met hetzelfde subnet**: standaard prioriteiten van het beheer punt zijn de peer-cache bronnen boven aan de lijst met inhouds locaties. Deze instelling omkeert die prioriteit voor clients die zich in hetzelfde subnet bevinden als de peer-cache bron.  

- Bekijk de voor **keur boven distributie punten voor Cloud distributiepunt**: als u een filiaal met een snellere Internet koppeling hebt, kunt u nu een prioriteit geven aan Cloud inhoud.  

Zie voor meer informatie [Opties voor grens groepen voor het downloaden van peers](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Beheer Insights regel voor de client versie van de peer-cache

<!-- 1358008 -->
Het **Management Insights** -knoop punt heeft een nieuwe regel om clients te identificeren die als peer-cache bron fungeren, maar die niet zijn bijgewerkt van een pre-1806-client versie. De nieuwe regel is het **upgraden van peer-cache bronnen naar de nieuwste versie van de Configuration Manager-client**en maakt deel uit van de nieuwe **proactieve onderhouds** regel groep. Pre-1806-clients kunnen niet worden gebruikt als peer-cache bron voor clients waarop versie 1806 of hoger wordt uitgevoerd. Selecteer **actie ondernemen** om een weer gave apparaat te openen waarin de lijst met clients wordt weer gegeven.

Zie [Management Insights](../../servers/manage/management-insights.md)voor meer informatie.



## <a name="client-management"></a><a name="bkmk_client"></a> Client beheer

### <a name="new-client-notification-action-to-wake-up-device"></a>Nieuwe client meldings actie voor het activeren van het apparaat

<!--1317364-->
U kunt nu clients uit de Configuration Manager-console ontwaken, zelfs als de client zich niet in hetzelfde subnet bevindt als de site server. Als u onderhoud of query apparaten wilt uitvoeren, bent u niet beperkt door externe clients die in de slaap stand zijn. De site server maakt gebruik van het kanaal voor client meldingen om een andere client aan te duiden die zich in hetzelfde externe subnet bevindt. De aanwakkerde client verzendt vervolgens een Wake on LAN-aanvraag (Magic-pakket).

Zie [Wake on LAN configureren](../../clients/deploy/configure-wake-on-lan.md) en [clients activeren](../../clients/deploy/plan/plan-wake-up-clients.md)voor meer informatie.

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Nieuwe optie voor het uitvoeren van client melding van het knoop punt apparaten

<!--1317364-->
Tot 1810, de optie **client melding** is alleen beschikbaar via het knoop punt van de verzameling apparaten of wanneer u het lidmaatschap van een verzameling apparaten hebt bekeken. Het is nu mogelijk om rechtstreeks een **client melding** van het knoop punt **apparaten** uit te voeren. Het is niet meer nodig om binnen de weer gave van het verzamelings lidmaatschap te vallen.

Zie [client meldingen](../../clients/manage/client-notification.md)voor meer informatie.


### <a name="improvements-to-collection-evaluation"></a>Verbeteringen in de verzamelings evaluatie

<!--3607726, fka 1358981-->
De volgende wijzigingen in het verzamelings evaluatie gedrag kunnen de prestaties van de site verbeteren:  

- Wanneer u eerder een planning voor een op query's gebaseerde verzameling hebt geconfigureerd, zal de site de query toch gaan evalueren, ongeacht of u de instelling voor het verzamelen **van een volledige update voor deze verzameling**hebt ingeschakeld. Als u het schema volledig wilt uitschakelen, moet u het schema wijzigen in **geen**. De site wist nu het schema wanneer u deze instelling uitschakelt. Als u een planning voor het verzamelen van de verzameling wilt opgeven, schakelt u de optie voor het **plannen van een volledige update voor deze verzameling**in.  

- U kunt de evaluatie van ingebouwde verzamelingen, zoals **alle systemen**, niet uitschakelen, maar de planning kan nu worden geconfigureerd. Dit gedrag stelt u in staat om deze actie aan te passen op een moment dat voldoet aan uw bedrijfs vereisten.

Zie [verzamelingen maken](../../clients/manage/collections/create-collections.md#bkmk_create)voor meer informatie.


### <a name="improvement-to-client-installation"></a>Verbetering van client installatie

<!--1358840-->
Bij de installatie van de Configuration Manager-client neemt het ccmsetup-proces contact op met het beheer punt om de benodigde inhoud te vinden. Eerder in dit proces retourneert het beheer punt alleen distributie punten in de huidige grens groep van de client. Als er geen inhoud beschikbaar is, wordt het installatie proces teruggezet om de inhoud van het beheer punt te downloaden. Er is geen optie om terug te vallen op distributie punten in andere grens groepen die mogelijk de benodigde inhoud hebben. Het beheer punt retourneert nu distributie punten op basis van de configuratie van de grens groep.

Zie [grens groepen configureren](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)voor meer informatie.



## <a name="co-management"></a><a name="bkmk_comgmt"></a> Co-beheer

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Vereist app-nalevings beleid voor gezamenlijk beheerde apparaten

<!--1358196-->
Regels voor nalevings beleid definiëren in Configuration Manager voor vereiste toepassingen. Deze app-evaluatie maakt deel uit van de algemene nalevings status die is verzonden naar Microsoft Intune voor door co beheerde apparaten.

Zie [werk belastingen voor co-beheer](../../../comanage/workloads.md)voor meer informatie.


### <a name="improvement-to-co-management-dashboard"></a>Verbetering van het dash board voor co-beheer

<!--1358980-->
Het dash board voor co-beheer is verbeterd met de volgende gedetailleerde informatie:  

- De tegel **inschrijvings status van co-beheer** bevat aanvullende statussen

- Een nieuwe tegel voor **co-beheer status** met een trechter diagram toont de statussen van het registratie proces

- Een nieuwe tegel met aantallen **inschrijvings fouten**

![Scherm opname van het dash board voor co-beheer met de vier beste tegels](media/1358980-comgmt-dashboard.png)

Zie het [dash board voor co-beheer](../../../comanage/how-to-monitor.md#co-management-dashboard)voor meer informatie.


### <a name="improvements-to-internet-based-client-setup"></a>Verbeteringen in client installatie op Internet

<!--3607731, fka 1359181-->
Deze versie vereenvoudigt het Configuration Manager client installatie proces voor clients op internet. De site publiceert aanvullende informatie over Azure Active Directory (Azure AD) naar de Cloud Management Gateway (CMG). Een client die lid is van Azure AD, haalt deze informatie op uit de CMG tijdens het ccmsetup-proces, waarbij dezelfde Tenant wordt gebruikt waaraan deze is gekoppeld. Dit gedrag vereenvoudigt het inschrijven van apparaten op co-beheer in een omgeving met meer dan één Azure AD-Tenant. Nu zijn de enige twee vereiste ccmsetup-eigenschappen **CCMHOSTNAME** en **SMSSiteCode**.

Zie [hoe u op internet gebaseerde apparaten voorbereidt voor co-beheer](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client)voor meer informatie.



## <a name="application-management"></a><a name="bkmk_app"></a> Toepassings beheer

### <a name="convert-applications-to-msix"></a>Toepassingen converteren naar MSIX

<!--3607729, fka 1359029-->
Vanaf versie 1806 ondersteunt Configuration Manager de implementatie van de nieuwe Windows 10 app pakket-indeling (. msix). U kunt uw bestaande Windows Installer-toepassingen (. msi) nu converteren naar de MSIX-indeling.

Zie [Windows-toepassingen maken](../../../apps/get-started/creating-windows-applications.md#bkmk_msix)voor meer informatie.  


### <a name="repair-applications"></a>Toepassingen herstellen

<!--1357866-->
Geef een herstel opdracht regel op voor de implementatie typen Windows Installer en script installatie. Als u de optie voor de implementatie inschakelt, is er in Software Center een nieuwe knop beschikbaar om de toepassing te **herstellen** . Wanneer u een toepassing met een herstel programma configureert, kunnen gebruikers de opdracht starten vanuit software Center.

Zie [toepassingen maken](../../../apps/deploy-use/create-applications.md#bkmk_dt-content) en [toepassingen implementeren](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings)voor meer informatie.


### <a name="approve-application-requests-via-email"></a>Toepassings aanvragen via e-mail goed keuren

<!--1321550-->
E-mail meldingen configureren voor aanvragen voor het goed keuren van toepassingen. Wanneer een gebruiker een toepassing aanvraagt, ontvangt u een e-mail bericht. Klik op koppelingen in het e-mail bericht om de aanvraag goed te keuren of te weigeren zonder dat de Configuration Manager-console is vereist.

Zie [toepassingen goed keuren](../../../apps/deploy-use/app-approval.md)voor meer informatie.


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Windows Power shell-profielen worden niet geladen door detectie methoden

<!--3607762, fka 1359239-->
U kunt Windows Power shell-scripts gebruiken voor detectie methoden voor toepassingen en instellingen in configuratie-items. Wanneer deze scripts worden uitgevoerd op clients, roept de Configuration Manager-client nu Power shell aan met de `-NoProfile` para meter. Met deze optie wordt Power shell zonder profielen gestart.

Een Power shell-profiel is een script dat wordt uitgevoerd wanneer Power shell wordt gestart. U kunt een Power shell-profiel maken om uw omgeving aan te passen en om sessie-specifieke elementen toe te voegen aan elke Power shell-sessie die u start.

> [!Note]  
> Deze wijziging in gedrag is niet van toepassing op [scripts](../../../apps/deploy-use/create-deploy-scripts.md) of [CMPivot](../../servers/manage/cmpivot.md). Deze beide functies gebruiken al deze Power shell-para meter.  

Zie [toepassingen maken](../../../apps/deploy-use/create-applications.md) en [aangepaste configuratie-items maken](../../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)voor meer informatie.



## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementatie van besturings systeem

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Ondersteuning voor taken reeksen van Windows auto pilot voor bestaande apparaten

<!--3607717, fka 1358333-->
[Windows auto pilot voor bestaande apparaten](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) is nu beschikbaar in Windows 10 versie 1809 of hoger. Met deze nieuwe functie kunt u de installatie kopie van een Windows 7-apparaat voor de door de [gebruiker gestuurde Windows-modus voor automatische prototypen](/windows/deployment/windows-autopilot/user-driven) opnieuw maken en inrichten met één systeem eigen Configuration Manager taken reeks.

Zie [Windows Autopilot voor bestaande apparaten](../../../../autopilot/existing-devices.md) voor meer informatie.


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Het station opgeven voor offline-installatie kopie onderhoud van besturings systemen

<!--1358924-->
Geef nu het station op dat Configuration Manager gebruikt om software-updates toe te voegen aan installatie kopieën van het besturings systeem en upgrade pakketten van het besturings systeem. Dit proces kan een grote hoeveelheid schijf ruimte in beslag nemen met tijdelijke bestanden, zodat u met deze optie de mogelijkheid hebt om het te gebruiken station te selecteren.

Zie [installatie kopieën van besturings systemen beheren](../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive) of [OS-upgrade pakketten beheren](../../../osd/get-started/manage-operating-system-upgrade-packages.md#bkmk_servicing-drive)voor meer informatie.


### <a name="task-sequence-support-for-boundary-groups"></a>Ondersteuning van taken reeksen voor grens groepen

<!--1359025-->
Wanneer een apparaat een taken reeks uitvoert en inhoud moet verkrijgen, worden er nu gedrag voor grens groepen gebruikt die vergelijkbaar zijn met de Configuration Manager-client.

Zie [grens groepen](../../servers/deploy/configure/boundary-groups.md#bkmk_bgr-osd)voor meer informatie.


### <a name="improvements-to-driver-maintenance"></a>Verbeteringen in het onderhoud van Stuur Programma's

<!--3607716, fka 1358270-->
Stuur programmapakketten hebben nu aanvullende meta gegevens velden voor de **fabrikant** en het **model**. Gebruik deze velden voor het labelen van Stuur programmapakketten met informatie om te helpen bij algemene housekeeping, of om oude en dubbele Stuur Programma's te identificeren die u kunt verwijderen.

Zie [Stuur Programma's beheren](../../../osd/get-started/manage-drivers.md)voor meer informatie.

### <a name="improvements-to-windows-10-servicing-plan-filters"></a>Verbeteringen in de filters voor het onderhouds plan voor Windows 10

<!--3098809, 3113836, 3204570 -->
Er zijn extra filters toegevoegd aan onderhouds plannen voor Windows 10. U kunt nu filteren op **architectuur**, **product categorie**en als de upgrade is **vervangen**.

Zie [Windows 10-onderhouds plan](../../../osd/deploy-use/manage-windows-as-a-service.md#BKMK_ServicingPlan)voor meer informatie.

### <a name="new-task-sequence-variable-for-last-action-name"></a>Nieuwe taken reeks variabele voor de naam van de laatste actie

<!--SCCMDocs-pr issue #2964-->
Naast de taken reeks variabele _SMSTSLastActionRetCode, stelt de taken reeks ook een nieuwe variabele in **_SMSTSLastActionName**. Deze waarde wordt ook geregistreerd in het bestand bestand smsts. log. Deze nieuwe variabele is handig bij het oplossen van problemen met een taken reeks. Wanneer een stap mislukt, kan een aangepast script de naam van de stap en de retour code bevatten.

Zie [taken reeks variabelen](../../../osd/understand/task-sequence-variables.md#SMSTSLastActionName)voor meer informatie.



## <a name="software-updates"></a><a name="bkmk_sum"></a> Software-updates

### <a name="phased-deployment-of-software-updates"></a>Gefaseerde implementatie van software-updates

<!--1358146-->
Gefaseerde implementaties maken voor software-updates. Met gefaseerde implementaties kunt u een gecoördineerde, geordende implementatie van software organiseren op basis van aanpas bare criteria en groepen.

Zie voor meer informatie [gefaseerde implementaties maken](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Verbetering van onderhouds Vensters voor software-updates

<!--vso2839307-->
De volgende client instelling bevindt zich in de groep met **software-updates** om het installatie gedrag van software-updates in onderhouds Vensters te beheren: **installatie van updates inschakelen in het onderhouds venster van ' alle implementaties ' wanneer het onderhouds venster Software-update beschikbaar is**

Deze optie is standaard **niet** nodig om consistent te blijven met het bestaande gedrag. Wijzig deze in **Ja** zodat clients andere beschik bare onderhouds Vensters kunnen gebruiken om software-updates te installeren.

Zie [client instellingen voor software-updates](../../clients/deploy/about-client-settings.md#bkmk_SUMMaint)voor meer informatie.


### <a name="improvement-to-software-updates-maintenance"></a>Verbetering van onderhoud van software-updates

<!--2839349-->
WSUS-opschoon taken worden nu uitgevoerd op secundaire sites. WSUS Cleanup voor verlopen updates wordt uitgevoerd en vervangen updates worden in WSUS afgewezen voor secundaire sites.

Zie voor meer informatie het [opruimen van WSUS vanaf versie 1810](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810)

### <a name="improvement-to-software-update-supersedence-rules"></a>Verbetering van de vervangings regels voor software-updates

<!--3098809, 2977644-->
U kunt nu vervangings regels voor onderdeel updates afzonderlijk van updates zonder onderdelen opgeven. Dit betekent dat uw upgrades niet uit Configuration Manager worden verwijderd voordat u uw Windows 10-clients hebt geïnstalleerd.

Zie [Supersedence rules](../../../sum/get-started/install-a-software-update-point.md#supersedence-rules)voor meer informatie.

## <a name="reporting"></a><a name="bkmk_report"></a> Rapporteren

### <a name="improvement-to-lifecycle-dashboard"></a>Dash board voor verbetering van levens cyclus

<!--1358702-->
Het dash board voor product levenscyclus bevat nu informatie over **System Center 2012 Configuration Manager en hoger**.

Er is ook een nieuw rapport, **levenscyclus 05A-product levenscyclus-dash board**. Het bevat soort gelijke informatie als het dash board in de console.

Zie [het dash board product levenscyclus gebruiken](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)voor meer informatie over dit dash board.


### <a name="improvement-to-data-warehouse"></a>Verbetering van het Data Warehouse

<!--1358870-->
U kunt nu meer tabellen van de site database synchroniseren naar het Data Warehouse. Met deze wijziging kunt u meer rapporten maken op basis van uw bedrijfs vereisten.

Zie [Data Warehouse](../../servers/manage/data-warehouse.md)voor meer informatie.



## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-console

### <a name="configuration-manager-administrator-authentication"></a>Beheerders verificatie Configuration Manager

<!--1357013-->
U kunt nu het minimale verificatie niveau voor beheerders opgeven om toegang te krijgen tot Configuration Manager-sites. Deze functie dwingt beheerders af om zich aan te melden bij Windows met het vereiste niveau. Als u deze instelling wilt configureren, gaat u naar het tabblad **verificatie** in **hiërarchie-instellingen**.

Zie [de SMS-provider plannen](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth)voor meer informatie.


### <a name="support-center"></a>Ondersteuningscentrum

<!--1357489-->
Gebruik het ondersteunings centrum voor het oplossen van problemen met clients, het weer geven van real-time Logboeken of het vastleggen van de status van een Configuration Manager-client computer voor latere analyse. Ondersteunings centrum is één hulp programma waarmee u veel hulpprogram ma's voor probleem oplossing kunt combi neren. Zoek het installatie programma voor het ondersteunings centrum op de site server in de map **cd. latest\SMSSETUP\Tools\SupportCenter** .

Zie het [ondersteunings centrum](../../support/support-center.md)voor meer informatie.


### <a name="management-insights-dashboard"></a>Management Insights-dash board

<!--1357979-->
Het **Management Insights** -knoop punt bevat nu een grafisch dash board. Dit dash board geeft een overzicht van de statussen van de regel, waardoor u uw voortgang gemakkelijker kunt weer geven. Het dash board bevat de volgende tegels:

- **Management Insights-index**: houdt de algehele voortgang bij van beheer Insights-regels. De index is een gewogen gemiddelde. Kritieke regels zijn het meest. Deze index geeft het minste gewicht aan optionele regels.  

- **Beheer Insights-groepen**: Hiermee wordt het percentage van de regels in elke groep weer gegeven.  

- **Prioriteit van management Insights**: geeft het percentage van de regels op prioriteit weer.  

- **Alle inzichten**: een tabel met inzichten, waaronder prioriteit en status.  

![Scherm opname van het management Insights-dash board](media/1357979-management-insights-dashboard.png)

Zie [Management Insights](../../servers/manage/management-insights.md)voor meer informatie.


### <a name="improvements-to-cmpivot"></a>Verbeteringen in CMPivot

<!--1359068-->
CMPivot bevat de volgende verbeteringen:

- **Favoriete** query's opslaan  

- Op het tabblad Query Samenvatting selecteert u het aantal mislukte of offline apparaten en selecteert u vervolgens de optie voor het **maken**van de verzameling.

Zie [verbeteringen in scripts](#bkmk_scripts)voor meer informatie over aanvullende prestaties en verbeteringen in CMPivot.

Zie [CMPivot](../../servers/manage/cmpivot.md)voor meer informatie over CMPivot.


### <a name="improvements-to-scripts"></a><a name="bkmk_scripts"></a> Verbeteringen in scripts

<!--1358239-->
U kunt nu gedetailleerde script uitvoer weer geven in de RAW-of Structured JSON-indeling. Met deze opmaak wordt de uitvoer eenvoudiger te lezen en te analyseren.

De volgende verbeteringen op het gebied van prestaties en probleem oplossing zijn van toepassing op zowel CMPivot als scripts:

- Bijgewerkte clients retour neren een uitvoer van minder dan 80 KB aan de site via een snel communicatie kanaal. Deze wijziging verhoogt de prestaties van het weer geven van scripts of uitvoer van query's.  

- Aanvullende logboeken voor het oplossen van problemen  

Raadpleeg voor meer informatie de volgende artikelen:  

- [Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console](../../../apps/deploy-use/create-deploy-scripts.md)  

- [Problemen met CMPivot oplossen](../../servers/manage/cmpivot-tsg.md)


### <a name="sms-provider-api"></a>API SMS-provider

<!--3607711, fka 1321523-->
De SMS-provider biedt nu alleen-lezen API-interoperabiliteits toegang tot WMI via HTTPS, de **beheer service**genoemd. Deze REST API kan worden gebruikt in plaats van een aangepaste webservice om toegang te krijgen tot informatie van de site.

De **SMS-provider** wordt weer gegeven als een functie met een optie om communicatie via de Cloud beheer gateway toe te staan. Het huidige gebruik van deze instelling is om goed keuringen van toepassingen via e-mail van een extern apparaat in te scha kelen.

Zie [de SMS-provider plannen](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)voor meer informatie.



## <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> On-premises MDM

### <a name="an-intune-connection-is-no-longer-required-for-new-on-premises-mdm-deployments"></a>Er is geen intune-verbinding meer vereist voor nieuwe on-premises MDM-implementaties

<!--1359124-->
De on-premises MDM-vereiste voor het configureren van een Microsoft Intune-abonnement is niet langer vereist voor nieuwe implementaties. Uw organisatie heeft nog steeds intune-licenties nodig om deze functie te gebruiken. U kunt de intune-verbinding op dit moment niet verwijderen uit bestaande on-premises MDM-implementaties. Zie het [blog bericht intune-ondersteuning](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150)voor meer informatie.



## <a name="other-updates"></a>Andere Updates

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 1810](https://support.microsoft.com/help/4482169)voor meer informatie.

Zie [release opmerkingen voor Power shell versie 1810](/powershell/sccm/1810-release-notes?view=sccm-ps)voor meer informatie over wijzigingen in de Windows Power shell-cmdlets voor Configuration Manager.

Het volgende update pakket (4488598) is beschikbaar in de-console vanaf 25 maart 2019: [Update pakket 2 voor Configuration Manager current branch, versie 1810](https://support.microsoft.com/help/4488598). Dit vervangt het vorige update pakket KB 4486457.


### <a name="hotfixes"></a>Hotfixes

De volgende aanvullende hotfixes zijn beschikbaar om specifieke problemen op te lossen:

| Id | Titel | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificaat wordt niet vernieuwd in Configuration Manager | 18 januari 2019 | Ja |
| [4490434](https://support.microsoft.com/help/4490434) | Er worden dubbele kolommen voor gebruikers detectie gemaakt in Configuration Manager | 22 februari 2019 | Ja |
| [4490575](https://support.microsoft.com/help/4490575) | Update-installaties reageren niet meer of worden nooit voltooid weer gegeven in Configuration Manager, versie 1810 | 22 februari 2019 | Ja |


## <a name="next-steps"></a>Volgende stappen

Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md) en [controle lijst voor het installeren van update 1810](../../servers/manage/checklist-for-installing-update-1810.md).

> [!TIP]  
> Als u een nieuwe site wilt installeren, gebruikt u een basislijn versie van Configuration Manager.  
>
> Meer informatie over:
>
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)  

Zie de [release opmerkingen](../../servers/deploy/install/release-notes.md)voor bekende, belang rijke problemen.

Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1810.md#post-update-checklist).