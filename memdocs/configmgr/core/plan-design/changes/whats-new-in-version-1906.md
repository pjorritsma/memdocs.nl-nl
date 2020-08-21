---
title: Wat is er nieuw in versie 1906
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1906 van Configuration Manager current branch.
ms.date: 10/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 97e23075-549c-4e45-ab1e-0671027edacf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0401207ec98331c33e87a0ac03b5cd7f750c17e7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698711"
---
# <a name="whats-new-in-version-1906-of-configuration-manager-current-branch"></a>Wat is er nieuw in versie 1906 van Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1906 voor Configuration Manager current branch is beschikbaar als een update in de console. Deze update Toep assen op sites waarop versie 1802 of hoger wordt uitgevoerd. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> In dit artikel vindt u een overzicht van de wijzigingen en nieuwe functies in Configuration Manager, versie 1906.  

Bekijk altijd de laatste controle lijst voor het installeren van deze update. Zie [Check List for Install update 1906](../../servers/manage/checklist-for-installing-update-1906.md)(Engelstalig) voor meer informatie. Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).

Als u optimaal wilt profiteren van de nieuwe functies van Configuration Manager, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

> [!Tip]  
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1906+-+Configuration+Manager%22&locale=en-us`


## <a name="requirement-changes"></a>Vereiste wijzigingen

### <a name="version-1906-client-requires-sha-2-code-signing-support"></a>Versie 1906-client vereist ondersteuning voor SHA-2-ondertekening van programma code

<!--SCCMDocs-pr#3404-->
Vanwege de nadelen van het algoritme SHA-1 en om af te stemmen op industrie standaarden, wordt micro soft nu alleen gebruikgemaakt van Configuration Manager binaire bestanden met het algoritme voor meer beveiliging SHA-2. De volgende versies van Windows-besturings systemen vereisen een update voor de ondersteuning van SHA-2-code ondertekening:

- Windows 7 SP1
- Windows Server 2008 R2 SP1
- Windows Server 2008 SP2

Zie [vereisten voor Windows-clients](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#bkmk_sha2)voor meer informatie.


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site-infra structuur

### <a name="site-server-maintenance-task-improvements"></a>Verbeteringen in de onderhouds taak van de site server

<!--3555894-->
Onderhouds taken voor site servers kunnen nu worden weer gegeven en bewerkt op hun eigen tabblad in de weer gave Details van een site server. Op het tabblad nieuwe **onderhouds taken** vindt u informatie zoals:

- Als de taak is ingeschakeld
- Het taak schema
- Laatste start tijd
- Tijdstip van de laatste voltooiing
- Als de taak is voltooid

![Nieuw tabblad voor onderhouds taken in de detail weergave van een site server](./media/3555894-maintenance-tasks.png)

Zie [onderhouds taken](../../servers/manage/maintenance-tasks.md#bkmk_MTs1906)voor meer informatie.

### <a name="configuration-manager-update-database-upgrade-monitoring"></a>Bewaking van data base-upgrade Configuration Manager bijwerken

<!--4200581-->
Wanneer u een Configuration Manager update toepast, kunt u nu de status van de taak **ConfigMgr-data base bijwerken** in het venster installatie status zien.

- Als de upgrade van de data base is geblokkeerd, krijgt u de waarschuwing dat deze wordt **uitgevoerd**.
   - De naam van het programma en de SessionID van SQL die de data base-upgrade blokkeert, worden door cmupdate. log geregistreerd.
- Wanneer de upgrade van de data base niet meer wordt geblokkeerd, wordt de status opnieuw ingesteld op **actief** of **voltooid**.
   - Wanneer de data base-upgrade is geblokkeerd, wordt elke vijf minuten een controle uitgevoerd om te zien of deze nog steeds wordt geblokkeerd.

   ![Data base-upgrade bewaking tijdens de installatie](./media/4200581-database-upgrade-monitoring.png)

Zie [updates binnen de console installeren](../../servers/manage/install-in-console-updates.md#3-monitor-the-progress-of-updates-as-they-install)voor meer informatie.

### <a name="management-insights-rule-for-ntlm-fallback"></a>Beheer Insights regel voor NTLM-terugval

<!--4572953-->
Management Insights bevat een nieuwe regel die detecteert of u de terugval methode voor minder veilige NTLM-authenticatie voor de site hebt ingeschakeld: **NTLM terugval is ingeschakeld**.

Zie [Management Insights](../../servers/manage/management-insights.md#security)voor meer informatie.

### <a name="improvements-to-support-for-sql-always-on"></a>Verbeterde ondersteuning voor SQL always on

- Een nieuwe synchrone replica toevoegen vanuit Setup<!--3127336-->: U kunt nu een nieuw secundair replica-knoop punt toevoegen aan een bestaande SQL always on-beschikbaarheids groep. Gebruik Configuration Manager Setup om deze wijziging door te voeren in plaats van een hand matig proces. Zie SQL Server AlwaysOn- [beschikbaarheids groepen configureren](../../servers/deploy/configure/configure-aoag.md#bkmk_sync)voor meer informatie.

- Failover met meerdere subnetten<!-- SCCMDocs-pr#3734 -->: U kunt het [sleutel woord MultiSubnetFailover Connection String](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) nu inschakelen in SQL Server. U moet de site server ook hand matig configureren. Zie voor meer informatie de [failover-vereiste voor meerdere subnetten](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#multi-subnet-failover) .

- Ondersteuning voor gedistribueerde weer gaven<!-- SCCMDocs-pr#3792 -->: De site database kan worden gehost op een SQL Server AlwaysOn-beschikbaarheids groep, en u kunt database replicatie koppelingen inschakelen om [gedistribueerde weer gaven](../hierarchy/data-transfers-between-sites.md#bkmk_dbrep)te gebruiken.

    > [!Note]  
    > Deze wijziging is niet van toepassing op SQL Server clusters.

- Site Recovery kan de data base opnieuw maken op een SQL always on-groep. Dit proces werkt met zowel hand matige als automatische seeding.<!-- SCCMDocs-pr#3846 -->

- Controles op vereisten voor nieuwe installatie:<!-- SCCMDocs-pr#3899 -->  

    - Replica's van de SQL-beschikbaarheids groep moeten allemaal dezelfde seeding-modus hebben
    - Replica's van de SQL-beschikbaarheids groep moeten in orde zijn

## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Cloud-gekoppeld beheer

### <a name="azure-active-directory-user-group-discovery"></a>Detectie van gebruikers groepen Azure Active Directory

<!--3611956-->

U kunt nu gebruikers groepen en leden van deze groepen ontdekken vanuit Azure Active Directory (Azure AD). Gebruikers die zijn gevonden in azure AD-groepen die de site nog niet eerder hebben gedetecteerd, worden toegevoegd als gebruikers resources in Configuration Manager. Er wordt een resource record voor een gebruikers groep gemaakt wanneer de groep een beveiligings groep is. Deze functie is een [voorlopige versie](../../servers/manage/pre-release-features.md) en moet worden ingeschakeld.

Zie [detectie methoden configureren](../../servers/deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco)voor meer informatie.

### <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a>Resultaten van verzamelings lidmaatschap synchroniseren met Azure Active Directory groepen

<!--3607475-->

U kunt nu de synchronisatie van verzamelings lidmaatschappen inschakelen voor een groep Azure Active Directory (Azure AD). Deze synchronisatie is een evaluatie versie. Zie [functies van voorlopige versies](../../servers/manage/pre-release-features.md)om deze functie in te scha kelen.

Met de synchronisatie kunt u uw bestaande on-premises groeperings regels in de Cloud gebruiken door Azure AD-groepslid maatschappen te maken op basis van de resultaten van het verzamelings lidmaatschap. Alleen apparaten met een Azure Active Directory record worden weer gegeven in de Azure AD-groep. Zowel hybride Azure AD join-als Azure Active Directory gekoppelde apparaten worden ondersteund.

Zie [verzamelingen maken](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)voor meer informatie.


## <a name="desktop-analytics"></a><a name="bkmk_da"></a> Desktop Analytics

### <a name="readiness-insights-for-desktop-apps"></a>Gereedheids inzichten voor desktop-apps

<!-- 4021225 -->

U kunt nu meer gedetailleerde inzichten krijgen voor uw desktop toepassingen, waaronder line-of-Business-Apps. De voormalige app Health Analyzer Toolkit is nu geïntegreerd met de Configuration Manager-client. Deze integratie vereenvoudigt de implementatie en beheer baarheid van app Readiness Insights in de Desktop Analytics-Portal.

Zie [compatibiliteits beoordeling in Desktop Analytics](../../../desktop-analytics/compat-assessment.md#advanced-insights)voor meer informatie.


### <a name="dalogscollector-tool"></a>Hulp programma DALogsCollector

<!--4622989-->
Gebruik het DesktopAnalyticsLogsCollector.ps1-hulp programma vanuit de Configuration Manager installatiemap om te helpen bij het oplossen van problemen met Desktop Analytics. Er worden enkele basis stappen voor probleem oplossing uitgevoerd en de relevante logboeken worden in één werkmap verzameld.

Zie [Logboeken](../../../desktop-analytics/log-collector.md)voor meer informatie.


## <a name="real-time-management"></a><a name="bkmk_real"></a> Real-time beheer

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a>Voeg koppelingen, extra Opera tors en aggregators toe in CMPivot

<!--4054074-->

Voor CMPivot hebt u nu extra reken kundige Opera Tors, aggregators en de mogelijkheid om query's toe te voegen, zoals het gebruik van het REGI ster en het bestand samen.

Zie [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1906)voor meer informatie.

### <a name="cmpivot-standalone"></a>Zelfstandige CMPivot

<!--3555890, 4619340, 4692885 -->

U kunt CMPivot nu als een zelfstandige app gebruiken. CMPivot standalone is een **voorlopige functie** en is alleen beschikbaar in het Engels. Voer CMPivot buiten de Configuration Manager-console uit om de real-time status van apparaten in uw omgeving weer te geven. Met deze wijziging kunt u CMPivot gebruiken op een apparaat zonder eerst de-console te installeren.

U kunt de kracht van CMPivot delen met andere personen, zoals helpdesk medewerkers of beveiligings beheerders, die de-console niet op hun computer hebben geïnstalleerd. Deze andere personen kunnen met behulp van CMPivot query's uitvoeren op Configuration Manager naast de andere hulp middelen die ze traditioneel gebruiken. Door deze uitgebreide beheer gegevens te delen, kunt u samen werken om zakelijke problemen met meerdere rollen proactief op te lossen.

Zie [CMPivot](../../servers/manage/cmpivot.md#bkmk_standalone) en functies van de [voorlopige versie](../../servers/manage/pre-release-features.md#bkmk_table)voor meer informatie.

### <a name="added-permissions-to-the-security-administrator-role"></a>Er zijn machtigingen toegevoegd aan de rol beveiligings beheerder

<!--4683130-->

De volgende machtigingen zijn toegevoegd aan de ingebouwde rol [**beveiligings beheerder**](../../understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) van Configuration Manager:

- SMS-script lezen
- CMPivot uitvoeren op verzameling
- Lezen op inventaris rapport

Zie [CMPivot](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot_secadmin1906)voor meer informatie.


## <a name="content-management"></a><a name="bkmk_content"></a> Inhouds beheer

### <a name="delivery-optimization-download-data-in-client-data-sources-dashboard"></a>Bezorgings optimalisatie gegevens downloaden in het dash board client gegevens bronnen

<!--3555759-->
Het dash board client gegevens bronnen bevat nu gegevens voor [leverings optimalisatie](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) . Dit dash board helpt u te begrijpen van waar clients inhoud in uw omgeving ophalen.

Zie [dash board client gegevens bronnen](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)voor meer informatie.

### <a name="use-your-distribution-point-as-an-in-network-cache-server-for-delivery-optimization"></a>Gebruik uw distributie punt als een cache server in het netwerk voor de optimalisatie van de levering

<!--3555764-->
U kunt nu Delivery Optimization in-Network cache server installeren op uw distributie punten. Door deze inhoud on-premises in de cache te plaatsen, kunnen uw clients profiteren van de functie voor Delivery Optimization, maar kunt u WAN-koppelingen helpen beveiligen.

Deze cache server fungeert als transparante cache op aanvraag voor inhoud die wordt gedownload door Delivery Optimization. Gebruik client instellingen om te controleren of deze server alleen wordt aangeboden aan de leden van de lokale Configuration Manager grens groep.

Zie [Delivery Optimization in-Network cache in Configuration Manager](../hierarchy/microsoft-connected-cache.md)voor meer informatie.


## <a name="client-management"></a><a name="bkmk_client"></a> Client beheer

### <a name="support-for-windows-virtual-desktop"></a>Ondersteuning voor virtueel bureau blad van Windows

<!--3556025-->
[Virtueel bureau blad van Windows](/azure/virtual-desktop/) is een preview-functie van Microsoft Azure en Microsoft 365. U kunt nu Configuration Manager gebruiken voor het beheren van deze virtuele apparaten waarop Windows wordt uitgevoerd in Azure.

Net als bij een Terminal Server kunnen deze virtuele apparaten meerdere gelijktijdige actieve gebruikers sessies. Als u de client prestaties wilt helpen, schakelt Configuration Manager nu het gebruikers beleid uit op elk apparaat dat deze sessies met meerdere gebruikers mogelijk maakt. Zelfs als u gebruikers beleid inschakelt, schakelt de client deze standaard uit op deze apparaten, waaronder Windows Virtual Desktop en Terminal servers.

Zie [ondersteunde versies van besturings systemen voor clients en apparaten](../configs/supported-operating-systems-for-clients-and-devices.md#windows-computers)voor meer informatie.

### <a name="support-center-onetrace-preview"></a>Ondersteuningscentrum OneTrace (preview)

<!--3555962-->
OneTrace is een nieuwe logboek weergave met het ondersteunings centrum. Het werkt op dezelfde manier als CMTrace, met de volgende verbeteringen:

- Een weer gave met tabbladen
- Dockable Windows
- Verbeterde zoek mogelijkheden
- Mogelijkheid om filters in te scha kelen zonder de logboek weergave te verlaten
- Schuif balk hints om snel cluster fouten te identificeren
- Snel logboek openen voor grote bestanden

![Scherm opname van OneTrace log viewer](./media/3555962-onetrace.png)

Zie [ondersteunings centrum OneTrace](../../support/support-center-onetrace.md)voor meer informatie.

### <a name="configure-client-cache-minimum-retention-period"></a>Minimale Bewaar periode voor de client cache configureren

<!--4485509-->
U kunt nu de minimale tijd opgeven waarop de Configuration Manager-client de inhoud in de cache moet blijven gebruiken. Deze client instelling definieert de minimale hoeveelheid tijd Configuration Manager agent moet wachten voordat de inhoud uit de cache kan worden verwijderd in het geval dat er meer ruimte nodig is. Configureer de volgende instelling in de groep **client cache-instellingen** van client instellingen: **minimale duur voordat inhoud in cache kan worden verwijderd (minuten)**.

> [!Note]  
> In dezelfde client instellings groep wordt de naam van de bestaande instelling voor het **inschakelen van Configuration Manager client in het volledige besturings systeem om inhoud te delen** , nu hernoemd zodat deze **als peer-cache bron**kan worden ingesteld. Het gedrag van de instelling verandert niet.  

Zie [client cache-instellingen](../../clients/deploy/about-client-settings.md#client-cache-settings)voor meer informatie.


## <a name="co-management"></a><a name="bkmk_comgmt"></a> Co-beheer

### <a name="improvements-to-co-management-auto-enrollment"></a>Verbeteringen in de automatische inschrijving van co-beheer

- Een nieuw, door co beheerd apparaat wordt nu automatisch Inge schreven bij de Microsoft Intune-service op basis van het *apparaat* -token van Azure Active Directory (Azure AD). U hoeft niet te wachten totdat een gebruiker zich bij het apparaat aanmeldt voor het starten van de automatische inschrijving. Deze wijziging helpt bij het verminderen van het aantal apparaten met de [inschrijvings status](../../../comanage/how-to-monitor.md#co-management-enrollment-status) *wacht op gebruiker aanmelden*.<!-- 4454491 -->

- Voor klanten die al apparaten hebben Inge schreven voor gezamenlijk beheer, worden nieuwe apparaten nu onmiddellijk geregistreerd zodra ze aan de vereisten voldoen. Als het apparaat bijvoorbeeld is gekoppeld aan Azure AD en de Configuration Manager-client is geïnstalleerd.<!--4321130-->

Zie [co-beheer inschakelen](../../../comanage/how-to-enable.md)voor meer informatie.

### <a name="multiple-pilot-groups-for-co-management-workloads"></a>Meerdere Pilot groepen voor werk belastingen voor co-beheer

<!--3555750-->
U kunt nu verschillende pilot verzamelingen configureren voor elk van de werk belastingen voor co-beheer. Door gebruik te maken van verschillende pilot verzamelingen kunt u een nauw keurigere benadering gebruiken bij het verschuiven van werk belastingen.

- Op het tabblad **Activering** kunt u nu een verzameling voor **automatische inschrijving van intune** opgeven.
    - De **intune** -verzameling voor automatische inschrijving moet alle clients bevatten die u wilt onboarden naar co-beheer. Het is in feite een superset van alle andere staging-verzamelingen.

- Op het tabblad **tijdelijke bestanden** , in plaats van één pilot verzameling te gebruiken voor alle werk belastingen, kunt u nu een afzonderlijke verzameling kiezen voor elke werk belasting.

    ![Met het tabblad staging op co-beheer kunt u voor elke werk belasting een verzameling kiezen](./media/3555750-co-management-staging-tab.png)

Deze opties zijn ook beschikbaar wanneer u co-beheer voor het eerst inschakelt.

Zie [co-beheer inschakelen](../../../comanage/how-to-enable.md)voor meer informatie.

### <a name="co-management-support-for-government-cloud"></a>Ondersteuning voor co-beheer voor Government Cloud

<!--4075452-->
Klanten van de Amerikaanse overheid kunnen nu co-beheer gebruiken met de Azure-Cloud voor de Amerikaanse overheid (portal.azure.us). Zie [co-beheer inschakelen](../../../comanage/how-to-enable.md)voor meer informatie.


## <a name="application-management"></a><a name="bkmk_app"></a> Toepassings beheer

### <a name="filter-applications-deployed-to-devices"></a>Toepassingen die zijn geïmplementeerd op apparaten filteren

<!--4451056-->
Gebruikers categorieën voor toepassings implementaties van apparaten worden nu weer gegeven als filters in Software Center. Geef een **gebruikers categorie** op voor een toepassing op de pagina **Software Center** van de bijbehorende eigenschappen. Open vervolgens de app in Software Center en Bekijk de beschik bare filters.

Zie [hand matig toepassings gegevens opgeven](../../../apps/deploy-use/create-applications.md#bkmk_manual-app)voor meer informatie.

### <a name="application-groups"></a>Toepassings groepen

<!--3555907-->
Een groep toepassingen maken die u kunt verzenden naar een gebruiker of apparaat als één implementatie. De meta gegevens die u opgeeft over de app-groep worden gezien in Software Center als één entiteit. U kunt de apps in de groep ordenen, zodat de client deze in een specifieke volg orde installeert.

Deze functie is voorlopige versie. Zie [functies van voorlopige versies](../../servers/manage/pre-release-features.md)om deze functie in te scha kelen.

Zie [toepassings groepen maken](../../../apps/deploy-use/create-app-groups.md)voor meer informatie.

### <a name="retry-the-install-of-pre-approved-applications"></a>De installatie van vooraf goedgekeurde toepassingen opnieuw uitvoeren

<!--4336307-->
U kunt nu de installatie van een app die u eerder hebt goedgekeurd voor een gebruiker of apparaat opnieuw proberen. De goedkeurings optie is alleen voor beschik bare implementaties. Als de gebruiker de app verwijdert of als het eerste installatie proces mislukt, Configuration Manager de status ervan niet opnieuw evalueren en opnieuw installeren. Met deze functie kan een ondersteunings medewerker snel de installatie van de app opnieuw proberen voor een gebruiker die hulp aanroept.

Zie [toepassingen goed keuren](../../../apps/deploy-use/app-approval.md)voor meer informatie.

### <a name="install-an-application-for-a-device"></a>Een toepassing voor een apparaat installeren

<!--4402180-->
Vanuit de Configuration Manager-console kunt u nu in realtime toepassingen op een apparaat installeren. Met deze functie kunt u de nood zaak van afzonderlijke verzamelingen voor elke toepassing verminderen.

Zie [toepassingen voor een apparaat installeren](../../../apps/deploy-use/install-app-for-device.md)voor meer informatie.

### <a name="improvements-to-app-approvals"></a>Verbeteringen aan app-goed keuringen

<!--4224910-->
Deze release bevat de volgende verbeteringen voor het goed keuren van apps:

- Als u een aanvraag voor een app goedkeurt in de-console en deze vervolgens weigert, kunt u deze nu opnieuw goed keuren. Nadat u het hebt goedgekeurd, wordt de app opnieuw op de client geïnstalleerd.  

- In de Configuration Manager-console, de werk ruimte **software bibliotheek** onder **toepassings beheer**, wordt het knoop punt **goedkeurings aanvragen** hernoemd **toepassings aanvragen**.<!-- SCCMDocs-pr#4028 -->

- Er is een nieuwe WMI-methode, **DeleteInstance** voor het verwijderen van een aanvraag voor het goed keuren van apps. Met deze actie wordt de app op het apparaat niet verwijderd. Als dit nog niet is gebeurd, kan de gebruiker de app niet installeren vanuit software Center.

- Aanroepen van de **CreateApprovedRequest** -API om een vooraf goedgekeurde aanvraag voor een app op een apparaat te maken. Stel de para meter voor automatische **installatie** in op om te voor komen dat de app automatisch wordt geïnstalleerd op de client `FALSE` . De gebruiker ziet de app in Software Center, maar wordt niet automatisch geïnstalleerd.

Zie [toepassingen goed keuren](../../../apps/deploy-use/app-approval.md)voor meer informatie.


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementatie van besturings systeem

### <a name="task-sequence-debugger"></a>Fout opsporing voor taken reeksen

<!--3612274-->
Het fout opsporingsprogramma voor taken reeksen is een nieuw hulp programma voor probleem oplossing. U implementeert een taken reeks in foutopsporingsmodus op een verzameling van één apparaat. Zo kunt u de taken reeks op een gecontroleerde manier door lopen om het oplossen van problemen en onderzoek te helpen.

![Scherm afbeelding van het fout opsporingsprogramma voor taken reeksen](./media/3612274-tsdebug.png)

Deze functie is voorlopige versie. Zie [functies van voorlopige versies](../../servers/manage/pre-release-features.md)om deze functie in te scha kelen.

Zie [debug a task sequence](../../../osd/deploy-use/debug-task-sequence.md)voor meer informatie.

### <a name="clear-app-content-from-client-cache-during-task-sequence"></a>App-inhoud uit de client cache wissen tijdens de taken reeks

<!--4485675-->
In de taken reeks stap **toepassing installeren** kunt u nu de app-inhoud uit de client cache verwijderen nadat de stap is uitgevoerd.

Zie [over taken reeks stappen](../../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication)voor meer informatie.

> [!Important]  
> Werk de doel-client bij naar de meest recente versie ter ondersteuning van deze nieuwe functie.

### <a name="reclaim-sedo-lock-for-task-sequences"></a>SEDO-vergren deling voor taken reeksen vrijmaken

<!--3699337-->
Als de Configuration Manager-console niet meer reageert, kunt u de taken reeks vergren delen om verdere wijzigingen aan te brengen. Wanneer u nu probeert toegang te krijgen tot een vergrendelde taken reeks, kunt u nu de **wijzigingen negeren**en door gaan met het bewerken van het object.

Zie [de taken reeks editor gebruiken](../../../osd/understand/task-sequence-editor.md#bkmk_sedo)voor meer informatie.

### <a name="pre-cache-driver-packages-and-os-images"></a>Stuur programmapakketten en OS-installatie kopieën vooraf in cache plaatsen

<!--4224642-->
De vooraf-cache taken reeks bevat nu aanvullende inhouds typen. Inhoud van vóór de cache is eerder alleen toegepast op OS-upgrade pakketten. U kunt nu caching gebruiken om het bandbreedte verbruik van te verminderen:

- Installatiekopieën van het besturingssysteem
- Driverpakketten
- Pakketten

Zie [inhoud vooraf in cache configureren](../../../osd/deploy-use/configure-precache-content.md)voor meer informatie.

### <a name="improvements-to-os-deployment"></a>Verbeteringen in de implementatie van het besturings systeem

Deze release bevat de volgende verbeteringen voor de implementatie van het besturings systeem:

- Gebruik de volgende twee Power shell-cmdlets om de [taken reeks stap uitvoeren](../../../osd/understand/task-sequence-steps.md#child-task-sequence) te maken en te bewerken:<!--2839943-->

    - **New-CMTSStepRunTaskSequence**

    - **Set-CMTSStepRunTaskSequence**

- Het is nu eenvoudiger om variabelen te bewerken wanneer u een taken reeks uitvoert. Nadat u een taken reeks hebt geselecteerd in het venster Wizard taken reeks, bevat de pagina voor het bewerken van taken reeks variabelen een knop **bewerken** .<!-- 4668846 --> Zie [How to use Task sequence Varia bles](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-tswiz)(Engelstalig) voor meer informatie.

- De taken reeks stap **BitLocker uitschakelen** heeft een nieuwe teller voor opnieuw opstarten. Gebruik deze optie om het aantal herstartingen op te geven dat BitLocker moet worden uitgeschakeld. Deze wijziging helpt u bij het vereenvoudigen van uw taken reeks. U kunt één stap gebruiken in plaats van meerdere exemplaren van deze stap toe te voegen. <!--4512937--> Zie voor meer informatie [Disable BitLocker](../../../osd/understand/task-sequence-steps.md#BKMK_DisableBitLocker).

- Gebruik de nieuwe taken reeks variabele **SMSTSRebootDelayNext** met de bestaande [SMSTSRebootDelay](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelay) -variabele. Als u later opnieuw wilt opstarten met een andere time-out dan de eerste, stelt u deze nieuwe variabele in op een andere waarde in seconden. <!--4447680--> Zie [SMSTSRebootDelayNext](../../../osd/understand/task-sequence-variables.md#SMSTSRebootDelayNext)voor meer informatie.

- De taken reeks stelt een nieuwe variabele met het kenmerk alleen-lezen **_SMSTSLastContentDownloadLocation**in. Deze variabele bevat de laatste locatie waar de taken reeks is gedownload of probeerde inhoud te downloaden. Inspecteer deze variabele in plaats van de client logboeken te parseren.<!-- 2840337 -->

- Wanneer u taken reeks media maakt, voegt Configuration Manager geen autorun. inf-bestand toe. Dit bestand wordt doorgaans geblokkeerd door antimalware-producten. U kunt het bestand nog steeds toevoegen als dat nodig is voor uw scenario.<!-- 4090666 -->

### <a name="improvements-to-pxe"></a>Verbeteringen aan PXE

De optie 82 tijdens de PXE DHCP-Handshake wordt nu ondersteund met de PXE-responder zonder WDS. De optie 82 wordt niet ondersteund met WDS.


## <a name="software-center"></a><a name="bkmk_userxp"></a> Software Center

### <a name="improvements-to-software-center-tab-customizations"></a>Verbeteringen aan het tabblad aanpassingen in het Software Center

<!--4063773-->
U kunt nu Maxi maal vijf aangepaste tabbladen toevoegen in Software Center. U kunt ook de volg orde wijzigen waarin deze tabbladen worden weer gegeven in Software Center.

Zie [client instellingen voor Software Center](../../clients/deploy/about-client-settings.md#software-center)voor meer informatie.

### <a name="software-center-infrastructure-improvements"></a>Verbeteringen in de Software Center-infra structuur

<!--3555950-->

Deze release bevat de volgende infrastructuur verbeteringen voor Software Center:

- Software Center communiceert nu met een beheer punt voor apps die als beschikbaar zijn gericht op gebruikers. De toepassings catalogus wordt niet meer gebruikt. Met deze wijziging wordt het voor u eenvoudiger om de toepassings catalogus uit de site te verwijderen.

- Voorheen heeft het Software Center het eerste beheer punt gekozen uit de lijst met beschik bare servers. Vanaf deze release maakt het gebruik van hetzelfde beheer punt dat de client gebruikt. Met deze wijziging kan software center hetzelfde beheer punt van de toegewezen primaire site gebruiken als de client.

> [!Important]  
> Deze herhaalde verbeteringen voor Software Center en het beheer punt zijn het buiten gebruik stellen van de functies van de toepassings catalogus.
>
> - De Silverlight-gebruikers ervaring wordt niet ondersteund op de huidige branch-versie 1806.
> - Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren.
> - Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  

Zie [de Application Catalog verwijderen](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat) en [Software Center plannen](../../../apps/plan-design/plan-for-software-center.md)voor meer informatie.

### <a name="redesigned-notification-for-newly-available-software"></a>Opnieuw ontworpen melding voor nieuwe beschik bare software

<!--3555904-->
De **nieuwe software is beschikbaar** melding slechts eenmaal weer gegeven voor een gebruiker voor een bepaalde toepassing en revisie. De gebruiker krijgt de melding niet meer te zien wanneer deze zich aanmeldt. Er wordt alleen een andere melding voor een toepassing weer geven als deze is gewijzigd of opnieuw is geïmplementeerd.

Zie [een toepassing maken en implementeren](../../../apps/get-started/create-and-deploy-an-application.md#end-user-experience)voor meer informatie.

### <a name="more-frequent-countdown-notifications-for-restarts"></a>Vaker voorkomende aftellings meldingen voor opnieuw opstarten

<!--3976435-->

Eind gebruikers worden nu vaker gevraagd met een herstart die opnieuw moet worden gestart, waarbij periodieke aftellings meldingen worden uitgevoerd. U kunt het interval voor de onregelmatige meldingen in **client instellingen** definiëren op de pagina voor het **opnieuw opstarten** van de computer. Wijzig de waarde voor **de uitstel duur voor het opnieuw starten van de computer (minuten)** om te configureren hoe vaak een gebruiker wordt gewaarschuwd voor een wacht tijd die opnieuw moet worden opgestart totdat de uiteindelijke melding over het aftellen wordt weer gegeven.

Daarnaast wordt de maximum waarde voor **een tijdelijke melding weer gegeven aan de gebruiker die het interval aangeeft voordat de gebruiker wordt afgemeld of de computer opnieuw wordt opgestart (minuten)** van 1440 minuten (24 uur) tot 20160 minuten (twee weken).

Zie meldingen voor het [opnieuw opstarten van apparaten](../../clients/deploy/device-restart-notifications.md) en [client instellingen](../../clients/deploy/about-client-settings.md#computer-restart)voor meer informatie.

### <a name="direct-link-to-custom-tabs-in-software-center"></a>Directe koppeling naar aangepaste tabbladen in Software Center

<!--4655176-->

U kunt gebruikers nu een rechtstreekse koppeling geven naar een [aangepast tabblad](../../clients/deploy/about-client-settings.md#software-center-tab-visibility) in Software Center.

Gebruik de volgende URL-indeling om software Center te openen op een bepaald tabblad:

`softwarecenter:page=CustomTab1`

De teken reeks `CustomTab1` is het eerste aangepaste tabblad in de juiste volg orde.

Typ bijvoorbeeld deze URL in het venster Windows **uitvoeren** .

U kunt deze syntaxis ook gebruiken om standaard tabbladen in Software Center te openen:

|Opdrachtregel  |Tabblad  |
|---------|---------|
|`AvailableSoftware`|Toepassingen|
|`Updates`|Updates|
|`OSD`|Besturingssystemen|
|`InstallationStatus`|Installatie status|
|`Compliance`|Apparaatcompatibiliteit|
|`Options`|Opties|

Zie het [tabblad Software Center](../../clients/deploy/about-client-settings.md#software-center-tab-visibility)voor meer informatie.

## <a name="software-updates"></a><a name="bkmk_sum"></a> Software-updates

### <a name="additional-options-for-wsus-maintenance"></a>Aanvullende opties voor WSUS-onderhoud

<!--4110109-->
U hebt nu aanvullende WSUS-onderhouds taken die Configuration Manager kunnen worden uitgevoerd om software-update punten goed te onderhouden. Het WSUS-onderhoud vindt plaats na elke synchronisatie. Naast het weigeren van verlopen updates in WSUS, kunt Configuration Manager nu het volgende doen:

- Verouderde updates verwijderen uit de WSUS-data base.
- Voeg niet-geclusterde indexen toe aan de WSUS-data base om de prestaties van WSUS-opschoning te verbeteren.

Zie onderhoud van software- [updates](../../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-starting-in-version-1906)voor meer informatie.

### <a name="configure-the-default-maximum-run-time-for-software-updates"></a>De standaard maximale uitvoerings tijd voor software-updates configureren

<!--3734426-->

U kunt nu de maximale hoeveelheid tijd opgeven dat de installatie van een software-update moet worden voltooid. U kunt de volgende items opgeven op het tabblad **maximale uitvoerings tijd** op het software-update punt:

- **Maximale uitvoerings tijd voor updates van Windows-onderdelen (minuten)**
- **Maximale uitvoerings tijd voor updates van Office 365 en niet-onderdelen voor Windows (minuten)**

Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md#bkmk_maxruntime)voor meer informatie.

### <a name="configure-dynamic-update-during-feature-updates"></a>Dynamische updates configureren tijdens onderdeel updates

<!--4062619-->

Gebruik een nieuwe client instelling voor het configureren van [dynamische updates](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847) tijdens de installatie van de Windows 10-functie-updates. Met de dynamische update worden taal pakketten, onderdelen op aanvraag, stuur Programma's en cumulatieve updates geïnstalleerd tijdens de installatie van Windows door de client te sturen om deze updates via internet te downloaden.

Zie [client instellingen voor software-updates](../../clients/deploy/about-client-settings.md#software-updates) en [Windows als een service beheren](../../../osd/deploy-use/manage-windows-as-a-service.md)voor meer informatie.

### <a name="new-windows-10-version-1903-and-later-product-category"></a>Nieuwe product categorie voor Windows 10, versie 1903 en hoger

<!--4682946-->

**Windows 10, versie 1903 en hoger** is toegevoegd aan Microsoft Update als een eigen product in plaats van dat ze deel uitmaken van het **Windows 10**  -product zoals eerdere versies. Als gevolg van deze wijziging hebt u een aantal hand matige stappen uitgevoerd om ervoor te zorgen dat uw clients deze updates zien. We hebben geholpen het aantal hand matige stappen te verminderen dat u voor het nieuwe product moet uitvoeren.

Wanneer u bijwerkt naar Configuration Manager versie 1906 en het **Windows 10** -product hebt geselecteerd voor synchronisatie, worden de volgende acties automatisch uitgevoerd:

- Het product **Windows 10, versie 1903 en hoger** wordt toegevoegd voor synchronisatie.
- Regels voor automatische implementatie die het **Windows 10** -product bevatten, worden bijgewerkt met **windows 10 versie 1903 en hoger**.
- Onderhouds plannen worden bijgewerkt met het product **Windows 10, versie 1903 en hoger** .

Zie voor meer informatie [classificaties en producten configureren voor synchronisatie](../../../sum/get-started/configure-classifications-and-products.md), [onderhouds plannen](../../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow)en [regels voor automatische implementatie](../../../sum/deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process).

### <a name="drill-through-required-updates"></a>Bekijk de vereiste updates

<!--4224414-->
U kunt nu inzoomen op nalevings statistieken om te zien voor welke apparaten een specifieke software-update is vereist. Als u de lijst met apparaten wilt weer geven, hebt u machtigingen nodig voor het weer geven van updates en de verzamelingen waartoe de apparaten behoren. Als u wilt inzoomen op de apparaten lijst, selecteert u in het tabblad **samen vatting** voor een update de optie **vereiste** Hyper link naast het cirkel diagram. Als u op de Hyper link klikt, gaat u naar een tijdelijk knoop punt onder **apparaten** waar u de apparaten kunt zien waarvoor de update is vereist.

De **weer gave** die is vereist, is beschikbaar op de volgende locaties:

   - **Software bibliotheek**  >  **Software-updates**  >  **Alle software-updates**
   - **Software bibliotheek**  >  Onderhoud van Windows **10**  >  **Alle Windows 10-updates**
   - **Software bibliotheek**  >  **Office 365-client beheer**  >  **Office 365-updates**

Zie [software-updates bewaken](../../../sum/deploy-use/monitor-software-updates.md#drill-through-required-updates), [Windows als een service beheren](../../../osd/deploy-use/manage-windows-as-a-service.md#drill-through-required-updates)en [Office 365 ProPlus-updates beheren](../../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie.


## <a name="office-management"></a><a name="bkmk_o365"></a> Office-beheer

### <a name="office-365-proplus-upgrade-readiness-dashboard"></a>Office 365 ProPlus upgrade gereedheids dashboard

<!--4021125-->

Om te bepalen welke apparaten klaar zijn om te upgraden naar Office 365 ProPlus, is er een nieuw dash board voor gereedheid. Het bevat de **Office 365 ProPlus upgrade Readiness** -tegel die is uitgebracht in Configuration Manager huidige branch versie 1902. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **Office 365 client management**uit en selecteer het knoop punt **Office 365 ProPlus Upgradegereedheid** .

Zie voor meer informatie over het dash board, vereisten en het gebruik van deze gegevens [integratie voor Office 365 ProPlus-gereedheid](../../../sum/deploy-use/office-365-dashboard.md#bkmk_readiness-dash).


## <a name="protection"></a><a name="bkmk_protect"></a> Kantel

### <a name="windows-defender-application-guard-file-trust-criteria"></a>Vertrouwens criteria voor Windows Defender Application Guard-bestanden

<!--3555858-->

Er is een nieuwe beleids instelling waarmee gebruikers bestanden kunnen vertrouwen die normaal worden geopend in Windows Defender Application Guard (WDAG). Wanneer de uitvoering is voltooid, worden de bestanden geopend op het hostapparaat in plaats van in WDAG.

Zie [Windows Defender Application Guard-beleid maken en implementeren](../../../protect/deploy-use/create-deploy-application-guard-policy.md#bkmk_FM)voor meer informatie.


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-console

### <a name="role-based-access-for-folders"></a>Op rollen gebaseerde toegang voor mappen

<!--3600867-->

U kunt nu beveiligingsbereiken instellen voor mappen. Als u toegang hebt tot een object in de map, maar u geen toegang hebt tot de map, kunt u het object niet zien. En als u toegang hebt tot een map, maar geen object daarin, ziet u dat object niet. Klik met de rechter muisknop op een map, kies **Beveiligingsbereiken instellen**en kies vervolgens de beveiligingsbereiken die u wilt Toep assen.

Zie [Configuration Manager console tips](../../servers/manage/admin-console-tips.md) en [op rollen gebaseerd beheer configureren](../../servers/deploy/configure/configure-role-based-administration.md#bkmk_config-folder)voor meer informatie.

### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>SMBIOS GUID-kolom toevoegen aan de knoop punten apparaat-en apparaat-verzameling

<!--4526580-->
In zowel de **apparaten** als de **apparaat verzameling** knoop punten kunt u nu een nieuwe kolom toevoegen voor de **SMBIOS-GUID**. Deze waarde is hetzelfde als de **BIOS GUID** -eigenschap van de systeem bron klasse. Het is een unieke id voor de hardware van het apparaat.

### <a name="administration-service-support-for-security-nodes"></a>Ondersteuning voor beheer Services voor beveiligings knooppunten

<!--4223683-->
U kunt nu enkele knoop punten van de Configuration Manager-console inschakelen om de beheer service te gebruiken. Met deze wijziging kan de console communiceren met de SMS-provider via HTTPS in plaats van via WMI.

Zie [beheer service](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)voor meer informatie.

> [!Note]
> Vanaf versie 1906 wordt het tabblad **communicatie van client computers** op de site-eigenschappen nu **communicatie beveiliging**genoemd.<!-- SCCMDocs#1645 -->  

### <a name="collections-tab-in-devices-node"></a>Het tabblad verzamelingen in het knoop punt apparaten

<!--4616810-->
Ga in de werk ruimte **activa en naleving** naar het knoop punt **apparaten** en selecteer een apparaat. Ga in het detail venster naar het tabblad nieuwe **verzamelingen** . Dit tabblad bevat de verzamelingen die dit apparaat bevatten.

> [!Note]  
> - Dit tabblad is momenteel niet beschikbaar vanuit een subknooppunt apparaten onder het knoop punt **apparaats verzameling** . Wanneer u bijvoorbeeld de optie selecteert om leden op een verzameling **weer te geven** .
> - Dit tabblad wordt mogelijk niet zoals verwacht ingevuld voor sommige gebruikers. Voor een overzicht van de volledige lijst met verzamelingen waarvan een apparaat deel uitmaakt, moet u de beveiligingsrol **volledige beheerder** hebben. Dit is een bekend probleem. <!--5107309-->

### <a name="task-sequences-tab-in-applications-node"></a>Het tabblad taken reeksen in het knoop punt toepassingen

<!--4616810-->
In de werk ruimte **software bibliotheek** vouwt u **toepassings beheer**uit, gaat u naar het knoop punt **toepassingen** en selecteert u een toepassing. Schakel in het detail venster over naar het tabblad nieuwe **taken reeksen** . Dit tabblad bevat de taken reeksen die verwijzen naar deze toepassing.

### <a name="show-collection-name-for-scripts"></a>De naam van de verzameling voor scripts weer geven

<!--4616810-->
Selecteer in de werk ruimte **bewaking** het knoop punt **script status** . De naam van de **verzameling** wordt nu naast de id weer gegeven.

### <a name="real-time-actions-from-device-lists"></a>Acties in realtime van apparaten lijsten

<!--4616810-->
Er zijn verschillende manieren om een lijst met apparaten weer te geven onder het knoop punt **apparaten** in de werk ruimte **activa en naleving** .

- Selecteer in de werk ruimte **activa en naleving** het knoop punt **device Collections** . Selecteer een verzameling apparaten en kies de actie om **leden weer te geven**. Met deze actie wordt een subknooppunt van het knoop punt **apparaten** geopend met een lijst met apparaten voor die verzameling.  

  - Wanneer u het subknooppunt verzameling selecteert, kunt u nu **CMPivot** starten vanuit de verzamelings groep van het lint.  

- Selecteer in de werk ruimte **bewaking** het knoop punt **implementaties** . Selecteer een implementatie en kies de actie **status weer geven** in het lint. Dubbel klik in het deel venster implementatie status op het totale aantal assets dat u wilt inzoomen op een apparaten lijst.  

  - Wanneer u een apparaat in deze lijst selecteert, kunt u nu **CMPivot** starten en **scripts uitvoeren** vanuit de apparaatgroep van het lint.  

### <a name="order-by-program-name-in-task-sequence"></a>Order by-programma naam in taken reeks

<!--4616810-->
Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer het knoop punt **taken reeksen** . Bewerk een taken reeks en selecteer of Voeg de stap [pakket installeren](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) toe. Als een pakket meer dan één programma heeft, worden de Program ma's nu alfabetisch gesorteerd met de vervolg keuzelijst.

### <a name="correct-names-for-client-operations"></a>Juiste namen voor client bewerkingen

<!--4616810-->
Selecteer **client bewerkingen**in de werk ruimte **bewaking** . De bewerking om **over te scha kelen naar het volgende software-update punt** heeft nu de juiste naam.


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Afgeschafte functies en besturings systemen

Meer informatie over ondersteunings wijzigingen voordat ze worden geïmplementeerd in [verwijderde en afgeschafte items](deprecated/removed-and-deprecated.md).

Versie 1906 wordt niet ondersteund voor de volgende functies:  

- U kunt geen nieuwe functies van de toepassings catalogus installeren. Bijgewerkte clients gebruiken automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. Zie [plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)(Engelstalig) voor meer informatie.

Versie 1906 reafschaffing ondersteunt de volgende producten:  

- Windows CE 7,0
- Windows 10 Mobile
- Windows 10 Mobile Enterprise


## <a name="other-updates"></a>Andere Updates

Vanaf deze versie zijn de volgende functies niet meer voorlopige versie:

- [Beheer service SMS-provider](../hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service)
- [Beheer van Windows Defender-toepassingsbeheer](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 1906](https://support.microsoft.com/help/4514258)voor meer informatie.

Zie [release opmerkingen voor Power shell versie 1906](/powershell/sccm/1906-release-notes?view=sccm-ps)voor meer informatie over wijzigingen in de Windows Power shell-cmdlets voor Configuration Manager.

Het volgende update pakket (4517869) is beschikbaar in de-console vanaf 1 oktober 2019: [Update pakket voor Configuration Manager current branch, versie 1906](https://support.microsoft.com/help/4517869).

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](../../servers/manage/updates.md#bkmk_supersede).
-->


## <a name="next-steps"></a>Volgende stappen

<!--At this time, version 1906 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-1906.md#early-update-ring). -->
Vanaf 16 augustus 2019 is versie 1906 wereld wijd beschikbaar voor alle klanten die moeten worden geïnstalleerd.

Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md) en [controle lijst voor het installeren van update 1906](../../servers/manage/checklist-for-installing-update-1906.md).

> [!TIP]  
> Als u een nieuwe site wilt installeren, gebruikt u een basislijn versie van Configuration Manager.  
>
> Meer informatie over:
>
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)  

Zie de [release opmerkingen](../../servers/deploy/install/release-notes.md)voor bekende, belang rijke problemen.

Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1906.md#post-update-checklist).