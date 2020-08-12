---
title: Wat is er nieuw in versie 1910
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1910 van Configuration Manager current branch.
ms.date: 01/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1567531ed83586f47ba2f79372e0b7962c1341dc
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128913"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Wat is er nieuw in versie 1910 van Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1910 voor Configuration Manager current branch is beschikbaar als een update in de console. Deze update Toep assen op sites waarop versie 1806 of hoger wordt uitgevoerd. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> In dit artikel vindt u een overzicht van de wijzigingen en nieuwe functies in Configuration Manager, versie 1910.

Bekijk altijd de laatste controle lijst voor het installeren van deze update. Zie [Check List for Install update 1910](../../servers/manage/checklist-for-installing-update-1910.md)(Engelstalig) voor meer informatie. Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).

Als u optimaal wilt profiteren van de nieuwe functies van Configuration Manager, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

> [!TIP]
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer:`https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="microsoft-endpoint-configuration-manager"></a><a name="bkmk_mem"></a>Micro soft endpoint Configuration Manager

<!--4960084-->

Configuration Manager maakt nu deel uit van micro soft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen met vereenvoudigde licenties. Blijf gebruikmaken van uw bestaande Configuration Manager investeringen, terwijl u profiteert van de kracht van de micro soft-Cloud in uw eigen tempo.

De volgende micro soft-beheer oplossingen maken nu deel uit van het merk van micro soft Endpoint Manager:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Andere functies in de beheer [console voor Apparaatbeheer](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Raadpleeg voor meer informatie de volgende Posts van Mark Anderson, micro soft Corporate Vice President for Microsoft 365:

- [Aankondigings blog post](https://aka.ms/cmannounce)
- [Vision Paper](https://aka.ms/MEMVisionPaper)
- [Video overzicht van aankondiging](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Wat is er veranderd in Configuration Manager met micro soft Endpoint Manager?

In versie 1910, afgezien van de naamswijziging, werkt Configuration Manager nog steeds hetzelfde. Sommige naam wijzigingen kunnen van invloed zijn op uw gebruik van de volgende onderdelen:

- **Configuration Manager-console**: snelkoppelingen naar de-console en de **Viewer voor extern beheer** vindt u in het menu Start van Windows in de map **micro soft Endpoint Manager** .

- **Software Center**: Ga naar de snelkoppeling Software Center onder het menu Start van Windows in de map **micro soft Endpoint Manager** .

![Pictogrammen start menu van micro soft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

Zorg ervoor dat u de interne documentatie die u onderhoudt, bijwerkt om deze nieuwe locaties op te nemen.

> [!TIP]
> Wanneer u in Windows 10 het menu Start opent, typt u de naam om het pictogram te vinden. Voer bijvoorbeeld `Configuration Manager` of `Software Center` in.

## <a name="site-infrastructure"></a><a name="bkmk_infra"></a>Site-infra structuur

### <a name="reclaim-sedo-lock"></a>SEDO-vergren deling vrijmaken

<!--4786915-->

Vanaf de [huidige branch-versie 1906](whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)kunt u de vergren deling van een taken reeks wissen. Nu kunt u de vergren deling van een object in de Configuration Manager-console wissen.

Zie [de Configuration Manager-console gebruiken](../../servers/manage/admin-console.md#bkmk_sedo)voor meer informatie.

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>On-premises site uitbreiden en migreren naar Microsoft Azure
<!--3556022-->

Dit nieuwe hulp programma helpt u bij het programmatisch maken van Azure virtual machines (Vm's) voor Configuration Manager. Het kan worden geïnstalleerd met de standaard instellingen site rollen zoals een passieve site server, beheer punten en distributie punten. Nadat u de nieuwe rollen hebt gevalideerd, gebruikt u deze als aanvullende site systemen voor hoge Beschik baarheid. U kunt ook de on-premises site systeemrol verwijderen en alleen de Azure VM-rol blijven gebruiken.

Zie [on-premises site uitbreiden en migreren naar Microsoft Azure](../../support/azure-migration-tool.md)voor meer informatie.

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="desktop-analytics"></a><a name="bkmk_da"></a>Desktop Analytics

Zie [what's New in Desktop Analytics](../../../desktop-analytics/whats-new.md)(Engelstalig) voor meer informatie over de maandelijkse wijzigingen in de Cloud service van Desktop Analytics.

## <a name="real-time-management"></a><a name="bkmk_real"></a>Real-time beheer

### <a name="optimizations-to-the-cmpivot-engine"></a>Optimalisaties voor de CMPivot-engine
<!--3197353-->
We hebben een aantal belang rijke optimalisaties toegevoegd aan de CMPivot-engine. U kunt nu meer van de verwerking naar de Configuration Manager-client pushen. De optimalisaties verminderen het netwerk en de CPU-belasting van de server die nodig is voor het uitvoeren van CMPivot-query's. Met deze optimalisaties kunt u nu Maxi maal gigabytes aan client gegevens in realtime door lopen. 

Zie [optimalisaties voor de CMPivot-engine](../../servers/manage/cmpivot-changes.md#bkmk_optimization)voor meer informatie.

### <a name="additional-cmpivot-entities-and-enhancements"></a>Aanvullende CMPivot-entiteiten en-verbeteringen
<!--5410930-->
We hebben een aantal nieuwe CMPivot-entiteiten en entiteits uitbreidingen toegevoegd om hulp te bieden bij het oplossen van problemen en jacht. We hebben de volgende entiteiten opgenomen voor het uitvoeren van query's:

- Windows-gebeurtenis Logboeken ([Wine vent](../../servers/manage/cmpivot-changes.md#bkmk_WinEvent))
- Bestands inhoud ([FileContent](../../servers/manage/cmpivot-changes.md#bkmk_File))
- Door processen geladen Dll's ([ProcessModule](../../servers/manage/cmpivot-changes.md#bkmk_ProcessModule))
- Azure Active Directory informatie ([AADStatus](../../servers/manage/cmpivot-changes.md#bkmk_AadStatus))
- Endpoint Protection-status ([EPStatus](../../servers/manage/cmpivot-changes.md#bkmk_EPStatus))

Deze release bevat ook enkele [andere verbeteringen](../../servers/manage/cmpivot-changes.md#bkmk_Other) in CMPivot. Zie [CMPivot vanaf versie 1910](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1910)voor meer informatie.

## <a name="content-management"></a><a name="bkmk_content"></a>Inhouds beheer

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Ondersteuning voor micro soft Connected cache voor intune Win32-apps

<!--5032900-->

Wanneer u micro soft Connected cache op uw Configuration Manager-distributie punten inschakelt, kunnen ze nu Microsoft Intune Win32-apps uitvoeren op clients die gezamenlijk worden beheerd.

Zie voor meer informatie [micro soft Connected cache in Configuration Manager](../hierarchy/microsoft-connected-cache.md#bkmk_intune).

> [!NOTE]
> Configuration Manager huidige branch-versie 1906 opgenomen [Delivery Optimization in-Network cache](../hierarchy/microsoft-connected-cache.md), een toepassing die is geïnstalleerd op Windows Server en nog steeds in ontwikkeling is. Met ingang van huidige versie 1910 van de branch wordt deze functie nu micro soft Connected cache genoemd.
>
> Wanneer u een verbonden cache op een Configuration Manager distributie punt installeert, wordt het verkeer voor de leverings optimalisatie service naar lokale bronnen geoffload. Verbonden cache doet dit gedrag door inhoud op het niveau van byte bereik efficiënt op te slaan in de cache.

## <a name="client-management"></a><a name="bkmk_client"></a>Client beheer

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Aangepaste configuratie basislijnen opnemen als onderdeel van de beoordeling van het nalevings beleid
<!--3608345-->

U kunt nu evaluatie van aangepaste configuratie basislijnen toevoegen als beoordelings regel voor het nalevings beleid. Wanneer u een configuratie basislijn maakt of bewerkt, kunt u nu gebruikmaken van de optie **deze basis lijn evalueren als onderdeel van de beoordeling van het nalevings beleid** . Wanneer u een nalevings beleidsregel toevoegt of bewerkt, hebt u een voor waarde met de naam onder de regel **geconfigureerde basis lijnen in de beoordeling van het nalevings beleid**.

Voor gezamenlijk beheerde apparaten en wanneer u intune configureert om de resultaten van de nalevings beoordeling te Configuration Manager als onderdeel van de algemene nalevings status, wordt deze informatie verzonden naar Azure Active Directory. U kunt dit vervolgens gebruiken voor voorwaardelijke toegang tot uw Office 365-resources.

Zie [aangepaste configuratie basislijnen opnemen als onderdeel van de evaluatie van het nalevings beleid](../../../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)voor meer informatie.

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Gebruikers beleid voor Windows 10 Enter prise meerdere sessies inschakelen

<!--4737447-->

Configuration Manager versie 1906 van de huidige branch is geïntroduceerd in ondersteuning voor [virtueel bureau blad van Windows](../configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop). Deze Microsoft Azure omgeving ondersteunt verschillende versies van besturings systemen, waarvan sommige meerdere gelijktijdige actieve gebruikers sessies toestaan. Zo is Windows 10 Enter prise meerdere sessies een van deze versies van het besturings systeem.

Als u gebruikers beleid nodig hebt voor deze multi-sessie apparaten en mogelijke gevolgen voor de prestaties wilt accepteren, kunt u nu een client instelling configureren om gebruikers beleid in te scha kelen. Configureer in de **client beleids** groep de instelling **gebruikers beleid inschakelen voor meerdere gebruikers sessies** .

Zie [client instellingen configureren](../../clients/deploy/configure-client-settings.md)voor meer informatie.


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="application-management"></a><a name="bkmk_app"></a>Toepassings beheer

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Microsoft Edge versie 77 en hoger implementeren
<!--4561024-->
De alles-nieuwe micro soft Edge is gereed voor bedrijven. U kunt nu micro soft Edge, versie 77 en hoger implementeren voor uw gebruikers. Beheerders kunnen de bèta, het dev of het stabiele kanaal kiezen, samen met een versie van de micro soft Edge-client die moet worden geïmplementeerd.

Zie [Deploying micro soft Edge, versie 77 of hoger](../../../apps/deploy-use/deploy-edge.md)(Engelstalig) voor meer informatie.

### <a name="improvements-to-application-groups"></a>Verbeteringen in toepassings groepen

<!--4760058-->

Vanaf de huidige versie 1906 van de branch kunt u een groep toepassingen maken en deze naar een apparaat verzameling verzenden als één implementatie. Deze versie is verbeterd op deze functie:

- Gebruikers kunnen **verwijderen** selecteren voor de app-groep in Software Center.
- U kunt een app-groep implementeren naar een **gebruikers verzameling**.

Zie [toepassings groepen maken](../../../apps/deploy-use/create-app-groups.md)voor meer algemene informatie.


## <a name="os-deployment"></a><a name="bkmk_osd"></a>Implementatie van besturings systeem

### <a name="improvements-to-the-task-sequence-editor"></a>Verbeteringen in de editor voor taken reeksen

 De editor voor taken reeksen bevat de volgende verbeteringen:

- **De taken reeks editor doorzoeken:**<!--4621085--> Als u een grote taken reeks hebt met veel groepen en stappen, kan het lastig zijn om specifieke stappen te vinden. U kunt nu zoeken in de editor voor taken reeksen. Met deze actie kunt u sneller stappen in de taken reeks vinden.
- **Kopiëren en plakken van de taken reeks voor waarden:**<!--4621098--> Als u de voor waarden van een taken reeks stap naar een andere wilt hergebruiken, kunt u nu voor waarden kopiëren en plakken in de taken reeks editor.

Zie het nieuwe artikel over [het gebruik van de taken reeks editor](../../../osd/understand/task-sequence-editor.md)voor meer informatie.

### <a name="task-sequence-performance-improvements-power-plans"></a>Verbeteringen aan de prestaties van de taken reeks: energiebeheer schema's

<!--3555926-->

U kunt nu een taken reeks uitvoeren met het energiebeheer schema met hoge prestaties. Met deze optie wordt de totale snelheid van de taken reeks verbeterd. Windows wordt geconfigureerd voor het gebruik van het ingebouwde energiebeheer schema met hoge prestaties, dat maximale prestaties levert voor de kosten van een hoger energie verbruik.

Zie [prestatie verbeteringen voor energiebeheer schema's](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_perf)voor meer informatie.

### <a name="task-sequence-download-on-demand-over-the-internet"></a>Taken reeks downloaden op aanvraag via Internet

<!--3601238-->

U kunt de taken reeks gebruiken om een Windows 10-in-place upgrade te implementeren via de Cloud Management Gateway (CMG). Hiervoor moet de implementatie echter alle inhoud lokaal downloaden voordat de taken reeks wordt gestart.

Vanaf deze release kan de taken reeks Engine pakketten op aanvraag downloaden van een CMG of een Cloud distributiepunt. Deze wijziging biedt extra flexibiliteit met uw Windows 10-in-place upgrade implementaties op apparaten op internet.

Zie [Deploying Windows 10 in-place upgrade via CMG](../../../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)voor meer informatie.

### <a name="improvements-to-os-deployment"></a>Verbeteringen in de implementatie van het besturings systeem

Deze release bevat de volgende verbeteringen voor de implementatie van besturings systemen.

#### <a name="boot-image-keyboard-layout"></a>Toetsenbord indeling voor opstart installatie kopie

<!--4910348-->

Configureer de standaardtoetsen bord indeling voor een opstart installatie kopie. Op het tabblad **aanpassing** van een opstart installatie kopie gebruikt u de nieuwe **standaard toetsenbord indeling instellen in** de optie WinPE. Als u een andere taal dan en-US selecteert, bevat Configuration Manager nog steeds en-us in de beschik bare land instellingen voor invoer. Op het apparaat is de oorspronkelijke toetsenbord indeling de geselecteerde land instelling, maar de gebruiker kan het apparaat overschakelen naar en-US als dat nodig is.

Zie [opstart installatie kopieën beheren](../../../osd/get-started/manage-boot-images.md#customization)voor meer informatie.

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Eén index van een OS-upgrade pakket importeren

<!--4931110-->

Wanneer u een upgrade pakket voor het besturings systeem importeert, kunt u de optie **een specifieke installatie kopie-index uit het bestand install. Wim van het geselecteerde upgrade pakket** gebruiken. Dit gedrag is vergelijkbaar met de [installatie kopieën van het besturings systeem](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages), behalve dat de bestaande install. Wim in het upgrade pakket van het besturings systeem wordt overschreven. De afbeeldings index wordt naar een tijdelijke locatie geëxtraheerd en vervolgens verplaatst naar de oorspronkelijke bronmap.

Zie [upgrade pakketten voor besturings systemen beheren](../../../osd/get-started/manage-operating-system-upgrade-packages.md#BKMK_AddOSUpgradePkgs)voor meer informatie.

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>De resultaten van een run-opdracht regel stap uitvoeren naar een variabele tijdens een taken reeks

<!--user story 4977616/bug 4798352-->

De stap **opdracht regel uitvoeren** bevat nu een optie **uitvoer voor taken reeks variabele** . Wanneer u deze optie inschakelt, slaat de taken reeks de uitvoer van de opdracht op in een aangepaste taken reeks variabele die u opgeeft.

Zie [Run Command Line](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine)voor meer informatie.

#### <a name="improvements-to-task-sequence-debugger"></a>Verbeteringen in het fout opsporingsprogramma voor taken reeksen

Deze release bevat de volgende verbeteringen voor het fout opsporingsprogramma voor taken reeksen:

- Gebruik de nieuwe taken reeks variabele **TSDebugOnError** om automatisch het fout opsporingsprogramma te starten als er een fout wordt geretourneerd door de taken reeks.<!-- 5012536 -->
- Als u een onderbrekings punt in het fout opsporingsprogramma maakt en vervolgens de computer opnieuw opstart, worden de onderbrekings punten na het opnieuw opstarten door de taken reeks bewaard.<!-- 5012509 -->

Zie voor meer informatie [taken reeks debugger](../../../osd/deploy-use/debug-task-sequence.md) en [taken reeks variabelen-TSDebugOnError](../../../osd/understand/task-sequence-variables.md#TSDebugOnError).

#### <a name="improved-language-support-in-task-sequence"></a>Verbeterde taal ondersteuning in de taken reeks

<!--5411057, 5138936-->

Deze release voegt controle over de taal configuratie toe tijdens de implementatie van het besturings systeem. Als u deze taal instellingen al toepast, kan deze wijziging u helpen de taken reeks van de besturingssysteem implementatie te vereenvoudigen. In plaats van meerdere stappen per taal of afzonderlijke scripts te gebruiken, gebruikt u één exemplaar per taal van de ingebouwde stap **Windows-instellingen Toep assen** met een voor waarde voor die taal.

Gebruik de taken reeks stap **Windows-instellingen Toep assen** om de volgende nieuwe instellingen te configureren:

- Land instellingen voor invoer (standaard toetsenbord indeling)
- Systeem land instelling
- Taal van gebruikers interface
- Terugval taal gebruikers interface
- Land instellingen voor gebruiker

Zie [Apply Windows Settings](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings)voor meer informatie.

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Nieuwe variabele voor Windows 10-in-place upgrade

<!--4680263-->

Als u problemen met de timing wilt oplossen met het venster 10 in-place upgrade taken reeks op apparaten met hoge prestaties wanneer Windows Setup is voltooid, kunt u nu een nieuwe taken reeks variabele **SetupCompletePause**instellen. Wanneer u een waarde in seconden aan deze variabele toewijst, wordt de hoeveelheid tijd voordat de taken reeks wordt gestart door het Windows-installatie proces vertraagd. Deze time-out zorgt voor de Configuration Manager-client meer tijd om te initialiseren.

Zie [taken reeks variabelen-SetupCompletePause](../../../osd/understand/task-sequence-variables.md#SetupCompletePause)voor meer informatie.

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="software-updates"></a><a name="bkmk_sum"></a>Software-updates

### <a name="additional-options-for-third-party-update-catalogs"></a>Aanvullende opties voor update-catalogi van derden
<!--4469002-->
U hebt nu meer gedetailleerde controle over de synchronisatie van catalogi met updates van derden. Vanaf Configuration Manager versie 1910 kunt u de synchronisatie planning voor elke afzonderlijke catalogus afzonderlijk configureren. Wanneer u catalogi gebruikt die gecategoriseerde updates bevatten, kunt u synchronisatie zo configureren dat deze alleen specifieke categorieën updates bevat om te voor komen dat u de volledige catalogus synchroniseert. Bij gecategoriseerde catalogussen kunt u, wanneer u zeker weet dat u een categorie wilt implementeren, deze zo configureren dat deze automatisch wordt gedownload en gepubliceerd op Windows Server Update Services (WSUS).

Zie updates van derden [inschakelen](../../../sum/deploy-use/third-party-software-updates.md#bkmk_1910)voor meer informatie.

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Delivery Optimization voor alle Windows-updates gebruiken
<!--4699118-->
Voorheen kunt u alleen Delivery Optimization gebruiken voor snelle updates. Met Configuration Manager versie 1910 is het nu mogelijk om Delivery Optimization te gebruiken voor de distributie van alle Windows Update inhoud voor clients met Windows 10 versie 1709 of hoger.

Zie voor meer informatie:
- [Levering van Windows 10-update optimaliseren](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#bkmk_DO-1910)
- [Clientinstellingen voor software-updates](../../clients/deploy/about-client-settings.md#software-updates)
- [Client instellingen voor Delivery Optimization](../../clients/deploy/about-client-settings.md#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>Extra software-update filter voor Adr's
<!--4852033-->
U kunt nu **geïmplementeerd** gebruiken als een update filter voor uw regels voor automatische implementatie (adr's). Dit filter helpt bij het identificeren van nieuwe updates die mogelijk moeten worden geïmplementeerd voor uw pilot-of test verzamelingen.

Zie [software-updates automatisch implementeren](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process)voor meer informatie.

## <a name="office-management"></a><a name="bkmk_o365"></a>Office-beheer


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Office 365 ProPlus pilot-en status dashboard
<!--4488272, 4488301-->

Het Office 365 ProPlus-pilot-en status dashboard helpt u bij het plannen, testen en implementeren van Office 365 ProPlus. Het dash board biedt status inzichten voor apparaten met Office 365 ProPlus om mogelijke problemen te identificeren die van invloed kunnen zijn op uw implementatie plannen. Het Office 365 ProPlus-pilot-en status dashboard biedt een aanbeveling voor pilot-apparaten op basis van de inventaris van invoeg toepassingen.

Zie voor meer informatie [Office 365 ProPlus pilot en Health dash board](../../../sum/deploy-use/office-365-dashboard.md#bkmk_pilot).

## <a name="protection"></a><a name="bkmk_protect"></a>Kantel

### <a name="bitlocker-management"></a>BitLocker-beheer

<!--3601034-->

Configuration Manager biedt nu de volgende beheer mogelijkheden voor BitLocker-stationsversleuteling:

- Implementeer de BitLocker-client op beheerde Windows-apparaten.
- Beleid voor het versleutelen van apparaten beheren.
- Nalevings rapporten genereren.
- Gebruik een website voor beheer en controle voor sleutel herstel.
- Toegang krijgen tot een self-service portal voor gebruikers.

Zie voor meer informatie [plannen voor BitLocker-beheer](../../../protect/plan-design/bitlocker-management.md).

## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a>Configuration Manager-console

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Actieve consoles en bericht beheerders weer geven via console verbindingen
<!--4923997-->
We hebben de volgende verbeteringen aangebracht in **console verbindingen**:

- De mogelijkheid om andere Configuration Manager beheerders te berichten via micro soft-teams.
- De **laatste kolom heartbeat** van de console is vervangen door de **laatste verbonden tijd** kolom.
  - Een geopende console op de voor grond stuurt elke 10 minuten een heartbeat om te helpen bepalen welke console verbindingen momenteel actief zijn.

Zie [recent verbonden consoles](../../servers/manage/admin-console.md#bkmk_viewconnected) en [bericht beheerders](../../servers/manage/admin-console.md#bkmk_message)weer geven voor meer informatie.

### <a name="client-diagnostics-actions"></a>Client diagnose acties

<!--4433455-->

Er zijn nieuwe acties voor **client diagnostiek** in de Configuration Manager-console:

- **Uitgebreide logboek registratie inschakelen:** Wijzig het globale logboek niveau voor het onderdeel CCM in *uitgebreid*en schakel logboek registratie voor fout opsporing in.
- **Uitgebreide logboek registratie uitschakelen:** Wijzig het globale logboek niveau in *standaard*en schakel logboek registratie voor fout opsporing uit.

Zie [client Diagnostics](../../clients/manage/client-notification.md#client-diagnostics)(Engelstalig) voor meer informatie.

### <a name="improvements-to-console-search"></a>Verbeteringen in zoeken in de console
<!--4640570-->

Deze release bevat de volgende verbeteringen voor het zoeken in de Configuration Manager-console:

- U kunt nu de zoek optie **alle submappen** gebruiken van de knoop punten **Stuur programmapakketten** en **query's** .<!--2841181,5424892-->
- Wanneer een zoek opdracht meer dan 1.000 resultaten retourneert, selecteert u **OK** op de mededelingen balk om meer resultaten weer te geven.<!--4640570-->

## <a name="other-updates"></a>Andere Updates

Zie [release opmerkingen voor Power shell versie 1910](https://docs.microsoft.com/powershell/sccm/1910-release-notes?view=sccm-ps)voor meer informatie over wijzigingen in de Windows Power shell-cmdlets voor Configuration Manager.

Zie [release opmerkingen voor de beheer service](../../../develop/adminservice/release-notes.md#bkmk_1910)voor meer informatie over wijzigingen in de beheer service rest API.

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 1910](https://support.microsoft.com/help/4535776)voor meer informatie.

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Device Guard management](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)
-->
Het volgende update pakket (4537079) is beschikbaar in de-console vanaf 18 februari 2020: [Update pakket voor micro soft Endpoint Configuration Manager current branch, versie 1910](https://support.microsoft.com/help/4537079).



<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4552181](https://support.microsoft.com/help/4552181) | Content distribution stalls in Configuration Manager current branch, version 1910 | 16 March 2020 | No |
| [4552430](https://support.microsoft.com/help/4552430) | Third-party update category synchronization resets to default in Configuration Manager | 18 March 2020 | No |

> [!NOTE]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->

## <a name="next-steps"></a>Volgende stappen

<!-- At this time, version 1910 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1910.md#early-update-ring). -->
Vanaf 20 december 2019 is versie 1910 wereld wijd beschikbaar voor alle klanten die moeten worden geïnstalleerd.

Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md) en [controle lijst voor het installeren van update 1910](../../servers/manage/checklist-for-installing-update-1910.md).

> [!TIP]
> Als u een nieuwe site wilt installeren, gebruikt u een basislijn versie van Configuration Manager.
>
> Meer informatie over:
>
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md) 
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines) 

Zie de opmerkingen bij de [release](../../servers/deploy/install/release-notes.md)voor bekende belang rijke problemen.

Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1910.md#post-update-checklist).
