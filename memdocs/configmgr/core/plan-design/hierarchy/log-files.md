---
title: Verwijzing naar logboekbestand
titleSuffix: Configuration Manager
description: Een verwijzing naar alle logboek bestanden voor Configuration Manager-client, server en afhankelijke onderdelen.
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11efada9eaf7e16a68902d7d6d78fb6708916d05
ms.sourcegitcommit: e618ea7cb864635c838b672bc71a1e926bf7c047
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/05/2020
ms.locfileid: "84458131"
---
# <a name="log-file-reference"></a>Verwijzing naar logboekbestand

*Van toepassing op: Configuration Manager (huidige vertakking)*

In Configuration Manager worden proces gegevens in afzonderlijke logboek bestanden vastgelegd in de client-en Site Server onderdelen. U kunt de informatie in deze logboek bestanden gebruiken om problemen op te lossen die zich kunnen voordoen. Configuration Manager maakt logboek registratie voor client-en Server onderdelen standaard mogelijk.

Zie [over logboek bestanden](about-log-files.md)voor meer algemene informatie over logboek bestanden in Configuration Manager. Dit artikel bevat informatie over de hulpprogram ma's die u moet gebruiken, het configureren van de logboeken en waar u ze kunt vinden.

De volgende secties bevatten informatie over de verschillende logboek bestanden die voor u beschikbaar zijn. Bewaak Configuration Manager client-en server logboeken voor bewerkings gegevens en Bekijk fout gegevens om problemen op te lossen.  

- [Client logboek bestanden](#BKMK_ClientLogs)  

  - [Client bewerkingen](#BKMK_ClientOpLogs)  

  - [Clientinstallatie](#BKMK_ClientInstallLog)  

  - [Client voor Linux en UNIX](#BKMK_LogFilesforLnU)  

  - [Client voor Mac-computers](#BKMK_LogfilesforMac)  

- [Server-logboek bestanden](#BKMK_ServerLogs)  

  - [Siteserver en sitesystemen](#BKMK_SiteSiteServerLog)  

  - [Installatie van de site server](#BKMK_SiteInstallLog)

  - [Data Warehouse-service punt](#BKMK_DataWarehouse)

  - [Terugvalstatuspunt](#BKMK_FSPLog)  

  - [Beheer punt](#BKMK_MPLog)  

  - [Serviceverbindingspunt](#BKMK_WITLog)  

  - [Software-updatepunt](#BKMK_SUPLog)  

- [Logboek bestanden op functionaliteit](#BKMK_FunctionLogs)  

  - [Toepassingsbeheer](#BKMK_AppManageLog)  

  - [Asset Intelligence](#BKMK_AILog)  

  - [Back-ups maken en herstellen](#BKMK_BnRLog)  

  - [Certificaat inschrijving](#BKMK_CertificateEnrollment)

  - [Clientmeldingen](#BKMK_BGB)

  - [Cloudbeheergateway](#cloud-management-gateway)

  - [Instellingen voor naleving en toegang tot bedrijfs bronnen](#BKMK_CompSettingsLog)  

  - [Configuration Manager-console](#BKMK_ConsoleLog)  

  - [Inhoudsbeheer](#BKMK_ContentLog)  

  - [Desktop Analytics](#desktop-analytics)

  - [Detectie](#BKMK_DiscoveryLog)  

  - [Endpoint Protection](#BKMK_EPLog)  

  - [Extensies](#BKMK_Extensions)  

  - [Inventaris](#BKMK_InventoryLog)  

  - [Migratie](#BKMK_MigrationLog)  

  - [Mobiele apparaten](#BKMK_MDMLog)  

  - [Besturingssysteemimplementatie](#BKMK_OSDLog)  

  - [Energiebeheer](#BKMK_PowerMgmtLog)  

  - [Extern beheer](#BKMK_RCLog)  

  - [Rapportage](#BKMK_ReportLog)  

  - [Op rollen gebaseerd beheer](#BKMK_RBALog)  

  - [Software licentie controle](#BKMK_MeteringLog)  

  - [Software-updates](#BKMK_SU_NAPLog)  

  - [Wake On LAN](#BKMK_WOLLog)  

  - [Onderhoud van Windows 10](#BKMK_WindowsServicingLog)

  - [Windows Update-agent](#BKMK_WULog)  

  - [WSUS-server](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a>Client logboek bestanden

De volgende secties geven een lijst van de logboek bestanden met betrekking tot client bewerkingen en client installatie.  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a>Client bewerkingen

De volgende tabel geeft een lijst van de logboek bestanden die zich op de Configuration Manager-client bevinden.  

|Logboeknaam|Beschrijving|  
|--------------|-----------------|  
|ADALOperationProvider. log|Informatie over client verificatie token aanvragen met de Azure Active Directory (Azure AD) verificatie bibliotheek (ADAL).|
|BitLockerManagementHandler. log|Registreert informatie over beleid voor BitLocker-beheer.|
|CAS.log|De content Access-service. Behoudt de cache van het lokale pakket op de client.|  
|Ccm32BitLauncher.log|Registreert acties voor het starten van toepassingen op de client *, gemarkeerd als 32-bits*.|  
|CcmEval.log|Registreert Configuration Manager evaluatie activiteiten van de client status en Details voor onderdelen die vereist zijn voor de Configuration Manager-client.|  
|CcmEvalTask.log|Registreert de Configuration Manager client status evaluatie activiteiten die worden geïnitieerd door de geplande taak voor de evaluatie.|  
|CcmExec.log|Registreert activiteiten van de client en de SMS Agent Host-service. Dit logboekbestand bevat informatie over het in- en uitschakelen van wake-up proxy.|  
|CcmMessaging.log|Registreert activiteiten met betrekking tot communicatie tussen de client en beheer punten.|  
|CCMNotificationAgent.log|Registreert activiteiten die betrekking hebben op de bewerkingen van clientmelding.|  
|Ccmperf.log|Registreert activiteiten die betrekking hebben op het onderhoud en vastleggen van gegeven met betrekking tot clientprestatietellers.|  
|CcmRestart.log|Registreert herstartactiviteit van de client-service.|  
|CCMSDKProvider.log|Registreert activiteiten voor de client SDK-interfaces.|  
|ccmsqlce. log|Registreert activiteiten voor de SQL Compact Edition die de-client gebruikt. Dit logboek wordt doorgaans alleen gebruikt wanneer u logboek registratie van fout opsporing inschakelt, of er is een probleem met het onderdeel. De client status taak (ccmeval) corrigeert doorgaans problemen met dit onderdeel.|
|CertificateMaintenance.log|Onderhoudt certificaten voor Active Directory Domain Services en beheerpunten.|  
|CIDownloader.log|Registreert details over downloads van configuratie-itemdefinitie.|  
|CITaskMgr.log|Registreert taken voor elk toepassings-en implementatie type, zoals het downloaden van inhoud en het installeren of verwijderen van acties.|  
|ClientAuth.log|Registreert ondertekening en verificatie activiteit voor de client.|  
|ClientIDManagerStartup.log|Maakt en onderhoudt de client-GUID en identificeert taken tijdens de registratie en toewijzing van de client.|  
|ClientLocation.log|Registreert taken die aan de sitetoewijzing van de client gerelateerd zijn.|  
|CMHttpsReadiness.log|Registreert de resultaten van het uitvoeren van het Configuration Manager HTTPS-gereedheids beoordelings programma. Dit hulp programma controleert of computers een PKI-client verificatie certificaat (Public Key Infrastructure) hebben dat kan worden gebruikt met Configuration Manager.|  
|CmRcService.log|Registreert informatie voor de control-service op afstand.|  
|CoManagementHandler. log|Gebruiken voor het oplossen van co-beheer op de client.|
|ContentTransferManager.log|Hiermee plant u de Background Intelligent Transfer Service (BITS) of SMB (Server Message Block) voor het downloaden of openen van pakketten.|  
|DataTransferService.log|Registreert alle BITS-communicatie voor beleids- of pakkettoegang.|  
|DeltaDownload. log|Registreert informatie over het downloaden van snelle updates en updates die zijn gedownload met behulp van leverings optimalisatie.|  
|Diagnostics. log|Registreert de status van client diagnose acties.|
|EndpointProtectionAgent|Registreert informatie over de installatie van de System Center Endpoint Protection-client en de toepassing van het antimalwarebeleid op die client.|  
|execmgr.log|Registreert details over pakketten en takenreeksen die worden uitgevoerd op de client.|  
|ExpressionSolver.log|Registreert gegevens over verbeterde detectie methoden die worden gebruikt wanneer uitgebreide of debug-logboek registratie is ingeschakeld.|  
|ExternalEventAgent.log|Registreert de geschiedenis van de Endpoint Protection-malware-detectie en gebeurtenissen met betrekking tot clientstatus.|  
|FileBITS.log|Registreert alle SMB-pakket-toegangstaken.|  
|FileSystemFile.log|Registreert de activiteit van de Windows Management Instrumentation (WMI) aanbieder voor software-inventaris en bestandsverzameling.|  
|FSPStateMessage.log|Registreert de activiteit voor statusberichten die gezonden worden naar het terugvalstatuspunt door de client.|  
|InternetProxy.log|Registreert de netwerk proxy configuratie en gebruik activiteit voor de client.|  
|InventoryAgent.log|Registreert activiteiten van hardware-inventaris, software-inventaris en heartbeat-detectieacties op de client.|  
|LocationCache.log|Registreert de activiteit voor locatie cache gebruik en onderhoud voor de client.|  
|LocationServices.log|Registreert de activiteit van de client voor het lokaliseren van beheerpunten, software-updatepunten en distributiepunten.|  
|M365AHandler. log|Informatie over het instellingen beleid voor desktop Analytics|
|MaintenanceCoordinator.log|Registreert de activiteit voor algemene onderhouds taken voor de client.|  
|Mifprovider.log|Registreert de activiteit van de WMI-provider voor MIF-bestanden (Management Information Format).|  
|mtrmgr.log|Bewaakt alle softwarelicentiecontroleprocessen.|  
|PolicyAgent.log|Registreert aanvragen voor beleids regels die zijn gemaakt met behulp van de Gegevensoverdracht-service.|  
|PolicyAgentProvider.log|Registreert beleidswijzigingen.|  
|PolicyEvaluator.log|Registreert gegevens over de beoordeling van beleid op clientcomputer, met inbegrip van beleid vanaf software-updates.|  
|PolicyPlatformClient.log|Registreert het proces van herstel en naleving voor alle providers in \Program Files\Microsoft Policy platform, met uitzonde ring van de bestands provider.|  
|PolicySdk.log|Registreert activiteiten voor beleidsysteem SDK interfaces.|  
|Pwrmgmt.log|Registreert informatie over in- en schakelen en configureren van de wake-up proxy clientinstellingen.|  
|PwrProvider.log|Registreert de activiteiten van de energiebeheer provider (PWRInvProvider) die in de WMI-service wordt gehost. Op alle ondersteunde versies van Windows somt de provider de huidige instellingen op de computers tijdens hardware-inventaris op en past de energiebeheerinstellingen toe.|  
|SCClient_ &lt; *domein* \> @ &lt; *gebruikers naam* \> _1. log|Registreert de activiteit in Software Center voor de opgegeven gebruiker op de clientcomputer.|  
|SCClient_ &lt; *domein* \> @ &lt; *gebruikers naam* \> _2. log|Registreert de historische activiteit in Software Center voor de gespecificeerde gebruiker op de clientcomputer.|  
|Scheduler.log|Registreert activiteiten van geplande taken voor alle clientbewerkingen.|  
|SCNotify_ &lt; *domein* \> @ &lt; *gebruikers naam* \> _1. log|Registreert de activiteit voor het verwittigen van gebruikers met betrekking tot software voor de opgegeven gebruiker.|  
|SCNotify_ &lt; *domein* \> @ &lt; *gebruikers naam* \> _1- &lt; *Date_Time*>. log|Registreert de historische activiteit voor het verwittigen van gebruikers met betrekking tot software voor de opgegeven gebruiker.|  
|setuppolicyevaluator.log|Registreert configuratie- en inventarisbeleid maken in WMI.|  
|SleepAgent_ &lt; *domein*\>@SYSTEM_0.log|Het hoofd logboek bestand voor wake-up proxy.|  
|smscliui.log|Registreert het gebruik van de Configuration Manager-client in het configuratie scherm.|  
|SrcUpdateMgr.log|Registreert activiteit voor geïnstalleerde Windows installertoepassingen die geüpdatet zijn met de huidige bronlocaties van distributiepunten.|  
|StatusAgent.log|Registreert statusberichten die zijn gemaakt door de clientonderdelen.|  
|SWMTRReportGen.log|Hiermee wordt een rapport met gebruiks gegevens gegenereerd dat wordt verzameld door de agent voor licentie controle. Deze gegevens worden geregistreerd in Mtrmgr.log.|  
|UserAffinity.log|Registreert gegevens over gebruikersaffiniteit apparaat.|  
|VirtualApp.log|Registreert informatie die specifiek is voor de evaluatie van implementatie typen van Application Virtualization (app-V).|  
|Wedmtrace.log|Registreert bewerkingen die betrekking hebben op het schrijven van filters op Windows Embedded-clients.|  
|wakeprxy-install.log|Registreert installatie-informatie wanneer clients de optie voor client instelling ontvangen om wake-up proxy in te scha kelen.|  
|wakeprxy-uninstall.log|Registreert informatie over het verwijderen van Wake-up proxy wanneer clients de optie client instelling ontvangen om wake-up proxy uit te scha kelen, als Wake-up proxy eerder is ingeschakeld.|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a>Client installatie

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot de installatie van de Configuration Manager-client.  

|Logboeknaam|Beschrijving|  
|--------------|-----------------|  
|ccmsetup.log|Registreert ccmsetup. exe-taken voor client installatie, client upgrade en client verwijdering. Kan worden gebruikt voor het oplossen van problemen tijdens de installatie van de client.|  
|ccmsetup-ccmeval.log|Registreert ccmsetup. exe-taken voor client status en herstel bewerkingen.|  
|CcmRepair.log|Registreert de herstelactiviteiten van de clientagent.|  
|client.msi.log|Registreert installatie taken uitgevoerd door client. msi. Kan worden gebruikt voor het oplossen van problemen tijdens de installatie van de client.|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a>Client voor Linux en UNIX

> [!Important]  
> Vanaf versie 1902 biedt Configuration Manager geen ondersteuning voor Linux-of UNIX-clients.
>
> Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.

De Configuration Manager-client voor Linux en UNIX registreert informatie in de volgende logboek bestanden:  

> [!TIP]
> Gebruik CMTrace om de logboek bestanden voor de client voor Linux en UNIX weer te geven.

|Logboeknaam|Details|
|-------------------|-----------------------------------------------------------------|
|Scxcm. log| Het logboek bestand voor de kern service van de Configuration Manager-client voor Linux en UNIX (ccmexec. bin). Dit logboekbestand bevat informatie over de installatie en voortgaande operaties van ccmexec.bin. Dit logboek bestand bevindt zich standaard op **/var/opt/Microsoft/scxcm.log**. Bewerk **/opt/microsoft/configmgr/etc/scxcm.conf** en wijzig het veld **PAD** om de locatie van het logboekbestand te wijzigen. U hoeft de client computer of-service niet opnieuw op te starten om de wijziging door te voeren. U kunt het logboek niveau instellen op een van de vier verschillende instellingen. |
| Scxcmprovider. log |Het logboek bestand voor de CIM-service van de Configuration Manager-client voor Linux en UNIX (omiserver. bin). Dit logboekbestand bevat informatie over de lopende processen van nwserver.bin. Dit logboek bevindt zich op `/var/opt/microsoft/configmgr/scxcmprovider.log` . Als u de locatie van het logboekbestand wilt wijzigen, bewerkt u **/opt/microsoft/omi/etc/scxcmprovider.conf** en wijzigt u het veld **PAD**. U hoeft de client computer of-service niet opnieuw op te starten om de wijziging door te voeren. U kunt het logboek niveau instellen op een van de drie instellingen.|

Beide logboekbestanden bieden ondersteuning voor verschillende niveaus van logboekregistratie:  

- **scxcm. log**. Als u het logboek niveau wilt wijzigen, bewerkt u **/opt/Microsoft/ConfigMgr/etc/scxcm.conf** en wijzigt u elk exemplaar van de **module** -tag naar het gewenste logboek niveau:  

  - FOUT: geeft aan dat er problemen zijn die aandacht vereisen  

  - Waarschuwing: geeft mogelijke problemen aan voor client bewerkingen  

  - INFO: meer gedetailleerde logboek registratie die de status van de verschillende gebeurtenissen op de client aangeeft  

  - TRACERing: uitgebreide logboek registratie die meestal wordt gebruikt voor het vaststellen van problemen  

- **scxcmprovider. log**. Als u het logboek niveau wilt wijzigen, bewerkt u **u/opt/Microsoft/Omi/etc/scxcmprovider.conf** en wijzigt u elk exemplaar van de **module** -tag naar het gewenste logboek niveau:  

  - FOUT: geeft aan dat er problemen zijn die aandacht vereisen  

  - Waarschuwing: geeft mogelijke problemen aan voor client bewerkingen

  - INFO: meer gedetailleerde logboek registratie die de status van de verschillende gebeurtenissen op de client aangeeft  

Gebruik onder normale bedrijfs omstandigheden het niveau van het fouten logboek. Dit logboek niveau maakt het kleinste logboek bestand. Naarmate het logboek niveau wordt verhoogd van fout naar waarschuwing, aan informatie en vervolgens om te TRACERen, wordt er een groter logboek bestand gemaakt, omdat er meer gegevens naar het bestand worden geschreven.  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a>Logboek bestanden voor de Linux-en UNIX-client beheren

De client voor Linux en UNIX beperkt de maximum grootte van de client logboek bestanden niet. Ook wordt de inhoud van de. log-bestanden niet automatisch gekopieerd naar een ander bestand, bijvoorbeeld naar een. lo_-bestand. Als u de maximale grootte van logboek bestanden wilt bepalen, implementeert u een proces voor het beheren van de logboek bestanden onafhankelijk van de Configuration Manager-client voor Linux en UNIX.  

U kunt bijvoorbeeld de standaard Linux-en UNIX-opdracht **logrotate** gebruiken om de grootte en de rotatie van de logboek bestanden van de client te beheren. De Configuration Manager-client voor Linux en UNIX heeft een **interface waarmee de client kan worden** gesignaleerd wanneer de draaiing van het logboek is voltooid, zodat de client de logboek registratie in het logboek bestand kan hervatten.  

Zie de documentatie voor de Linux- en UNIX-distributies die u gebruikt voor meer informatie over **logrotate**.  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a>Client voor Mac-computers

De Configuration Manager-client voor Mac-computers registreert informatie in de volgende logboek bestanden op de Mac-computer:  

|Logboeknaam|Details|Locatie|
|--------------|-------------|-------------|
|CCMClient- &lt; *Date_Time*>. log|Registreert activiteiten die betrekking hebben op de bewerkingen van de Mac-client, waaronder toepassings beheer, inventaris en logboek registratie van fouten.| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent- &lt; *Date_Time*>. log|Registreert informatie die betrekking heeft op client bewerkingen, waaronder aanmeldings-en afmeldings bewerkingen van gebruikers en de activiteit van een Mac-computer.| `~/Library/Logs`|  
|CCMNotifications- &lt; *Date_Time*>. log|Registreert activiteiten die gerelateerd zijn aan Configuration Manager meldingen die worden weer gegeven op de Mac-computer.| `~/Library/Logs`|  
|CCMPrefPane- &lt; *Date_Time*>. log|Registreert activiteiten die betrekking hebben op het dialoog venster Configuration Manager voor keuren op de Mac-computer, waaronder algemene status-en fouten registratie.| `~/Library/Logs`|  

Het logboek bestand **SMS_DM. log** op de site systeem server registreert ook communicatie tussen Mac-computers en het beheer punt dat is ingesteld voor mobiele apparaten en Mac-computers.  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a>Server-logboek bestanden

De volgende secties bevatten een lijst met logboek bestanden die op de site server staan of die gerelateerd zijn aan specifieke site systeem rollen.  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a>Site server en site systemen

De volgende tabel geeft een lijst van de logboek bestanden op de Configuration Manager site server en site systeem servers.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Registreert de activiteit van de inschrijvingsverwerking|Siteserver|  
|ADForestDisc.log|Registreert detectieacties Active Directory-forest.|Siteserver|  
|adminservice. log|Registreert acties voor de SMS-provider beheer service REST API|Computer met de SMS-provider|
|ADService.log|Registreert details van accountaanmaking en beveiligingsgroepen in Active Directory.|Siteserver|  
|adsgdis.log|Registreert detectie-acties van Active Directory-groepen.|Siteserver|  
|adsysdis.log|Registreert detectieacties Active Directory-systeem.|Siteserver|  
|adusrdis.log|Registreert detectieacties Active Directory-gebruiker.|Siteserver|  
|BusinessAppProcessWorker. log|Record verwerking voor Microsoft Store voor zakelijke apps.|Siteserver|
|ccm.log|Registreert activiteiten voor client push installatie.|Siteserver|  
|CertMgr.log|Registreert certificaat activiteiten voor intra site communicatie.|Sitesysteemserver|  
|chmgr.log|Registreert activiteiten van de client health manager.|Siteserver|  
|Cidm.log|Registreert wijzigingen aan de clientinstellingen door de Client Install Data Manager (CIDM).|Siteserver|  
|CollectionAADGroupSyncWorker. log | Vanaf versie 2002 wordt het logboek bestand voor synchronisatie van de resultaten van het lidmaatschap van de verzameling Azure Active Directory. In versie 1910 en eerder is logboek registratie voor deze functie gecombineerd in SMS_AZUREAD_DISCOVERY_AGENT. log. | Siteserver|
|colleval.log|Registreert gegevens over wanneer verzamelingen worden gemaakt, gewijzigd en verwijderd door de Verzamelingevaluator.|Siteserver|  
|compmon.log|Registreert de status van component-threads die worden bewaakt voor de siteserver.|Sitesysteemserver|  
|compsumm.log|Registreert taken van het component-statussamenvattingsprogramma.|Siteserver|  
|ComRegSetup.log|Registreert de initiële installatie van COM-registratieresultaten voor een siteserver.|Sitesysteemserver|  
|dataldr.log|Registreert informatie over de verwerking van MIF-bestanden en hardware-inventaris in de Configuration Manager-Data Base.|Siteserver|  
|ddm.log|Registreert activiteiten van de Discovery Data Manager.|Siteserver|  
|despool.log|Registreert inkomende overdrachten van communicatie tussen sites.|Siteserver|  
|distmgr.log|Registreert details over pakketcreatie, compressie, deltareplicatie en informatie-updates. Het kan ook andere activiteiten van het Distribution Manager-onderdeel omvatten. U kunt bijvoorbeeld een distributie punt, Verbindings pogingen en onderdelen installeren. Zie [service verbindings punt](#BKMK_WITLog) en implementatie van het [besturings systeem](#BKMK_OSDLog)voor meer informatie over andere functies die gebruikmaken van dit logboek.|Siteserver|  
|EPCtrlMgr.log|Registreert informatie over de synchronisatie van informatie over malware-bedreiging van de Endpoint Protection-site systeemrol server met de Configuration Manager-Data Base.|Siteserver|  
|EPMgr.log|Registreert de status van de Endpoint Protection-sitesysteemrol.|Sitesysteemserver|  
|EPSetup.log|Geeft informatie over de installatie van de Endpoint Protection-sitesysteemrol.|Sitesysteemserver|  
|EnrollSrv.log|Registreert activiteiten van het proces van de inschrijvingsservice.|Sitesysteemserver|  
|EnrollWeb.log|Registreert activiteiten van het proces van de inschrijvingswebsite.|Sitesysteemserver|  
|fspmgr.log|Registreert activiteiten van de sitesysteemrol terugvalstatuspunt.|Sitesysteemserver|  
|hman.log|Registreert informatie over site configuratie wijzigingen en over het publiceren van site-informatie in Active Directory Domain Services.|Siteserver|  
|Inboxast.log|Registreert de bestanden die verplaatst worden van het beheerpunt naar de corresponderende POSTVAKKEN IN-map op de siteserver.|Siteserver|  
|inboxmgr.log|Registreert activiteiten van bestandsoverdracht tussen Postvak in-mappen.|Siteserver|  
|inboxmon.log|Registreert de verwerking van updates van Postvak in-bestanden en prestatiemeteritems.|Siteserver|  
|invproc.log|Registreert het doorsturen van MIF-bestanden van een secundaire site naar de daarboven liggende site.|Siteserver|  
|migmctrl.log|Registreert informatie voor migratie-acties met migratie taken, gedeelde distributie punten en upgrades van distributie punten.|Site op het hoogste niveau in de hiërarchie van de Configuration Manager en elke onderliggende primaire site. Gebruik in een hiërarchie met meerdere primaire sites het logboek bestand dat is gemaakt op de centrale beheer site.|  
|mpcontrol.log|Registreert de registratie van het beheer punt met Windows Internet Name Service (WINS). Registreert elke 10 minuten de beschikbaarheid van het beheerpunt.|Sitesysteemserver|  
|mpfdm.log|Registreert de acties van de beheerpuntcomponent die clientbestanden verplaatst naar de corresponderende POSTVAKKEN IN-map op de siteserver.|Sitesysteemserver|  
|mpMSI.log|Registreert gegevens over de installatie van het beheer punt.|Siteserver|  
|MPSetup.log|Registreert het wrapperproces van de beheerpuntinstallatie.|Siteserver|  
|netdisc.log|Registreert netwerkdetectieacties.|Siteserver|  
|NotiCtrl. log|Meldingen over toepassings aanvragen.|Siteserver|  
|ntsvrdis.log|Registreert de detectie-activiteit van sitesysteemservers.|Siteserver|  
|Objreplmgr|Registreert de verwerking van objectwijzigingsmeldingen voor replicatie.|Siteserver|  
|offermgr.log|Registreert advertentie-updates.|Siteserver|  
|offersum.log|Registreert de samenvatting van statusberichten voor implementatie.|Siteserver|  
|OfflineServicingMgr.log|Registreert de activiteiten van het toepassen van updates in afbeeldingsbestanden van het besturingssysteem.|Siteserver|  
|outboxmon.log|Registreert de verwerking van updates van Postvak uit-bestanden en prestatiemeteritems.|Siteserver|  
|PerfSetup.log|Registreert de resultaten van de installatie van prestatiemeteritems.|Sitesysteemserver|  
|PkgXferMgr.log|Registreert de acties van het SMS_Executive onderdeel dat verantwoordelijk is voor het verzenden van inhoud van een primaire site naar een extern distributie punt.|Siteserver|  
|policypv.log|Registreert updates van de clientbeleidsregels die nodig zijn na wijzigingen aan clientinstellingen of implementaties.|Primaire siteserver|  
|rcmctrl.log|Registreert de activiteiten van databasereplicatie tussen sites binnen de hiërarchie.|Siteserver|  
|replmgr.log|Registreert de replicatie van bestanden tussen de siteservercomponenten en de Scheduler-component.|Siteserver|  
|ResourceExplorer.log|Registreert fouten, waarschuwingen en informatie over het uitvoeren van resource Explorer.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  
|RESTPROVIDERSetup. log|Installatie van de SMS-provider beheer service REST API|Computer met de SMS-provider|
|ruleengine.log|Registreert details over automatische implementatieregels voor de identificatie, het downloaden van software, en maken van software-updategroepen en implementaties.|Siteserver|  
|schedule.log|Registreert details over de replicatie tussen sites van taken en bestanden.|Siteserver|  
|sender.log|Registreert de bestanden die worden overgezet door middel van bestandsgebaseerde replicatie tussen sites.|Siteserver|  
|sinvproc.log|Registreert informatie over het verwerking van software-inventarisgegevens naar de sitedatabase.|Siteserver|  
|sitecomp.log|Registreert details over het onderhoud van de geïnstalleerde sitecomponenten op alle sitesysteemservers in de site.|Siteserver|  
|sitectrl.log|Registreert site-instellingswijzigingen die zijn aangebracht aan site-controleobjecten in de database.|Siteserver|  
|sitestat.log|Registreert het bewakingsproces van beschikbaarheid en schijfruimte voor alle sitesystemen.|Siteserver|
|SMS_AZUREAD_DISCOVERY_AGENT. log| Logboek bestand voor de detectie van gebruikers en gebruikers groepen voor Azure Active Directory (Azure AD). In versie 1910 en eerder is ook de synchronisatie van de verzamelings lidmaatschaps resultaten opgenomen in azure AD.| Siteserver|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Het logboek bestand voor het onderdeel dat apps synchroniseert vanuit de Microsoft Store voor bedrijven.|Siteserver|
|SMS_ISVUPDATES_SYNCAGENT. log| Logboek bestand voor synchronisatie van software-updates van derden.| Software-update punt op het hoogste niveau in de hiërarchie van de Configuration Manager.|
|SMS_OrchestrationGroup. log| Logboek bestand voor Orchestration-groepen|Siteserver|
|SMS_PhasedDeployment. log| Logboek bestand voor gefaseerde implementaties|Site op het hoogste niveau in de hiërarchie van de Configuration Manager|
|SMS_REST_PROVIDER. log|Service status voor de REST API van de SMS-provider beheer service, met inbegrip van certificaat gegevens|Computer met de SMS-provider|
|SmsAdminUI.log|Registreert Configuration Manager-console activiteit.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  
|SMSAWEBSVCSetup.log|Registreert de installatieactiviteiten van de Application Catalog-webservice.|Sitesysteemserver|  
|smsbkup.log|Registreert output van het back-upproces van de site.|Siteserver|  
|smsdbmon.log|Registreert wijzigingen van de database.|Siteserver|  
|SMSENROLLSRVSetup.log|Registreert de installatieactiviteiten van de inschrijvingswebservice.|Sitesysteemserver|  
|SMSENROLLWEBSetup.log|Registreert de installatieactiviteiten van de inschrijvingswebsite.|Sitesysteemserver|  
|smsexec.log|Registreert de verwerking van alle component-threads van siteservers.|Siteserver of sitesysteemserver|  
|SMSFSPSetup.log|Registreert berichten die gegenereerd worden door de installatie van een terugvalstatuspunt.|Sitesysteemserver|  
|SMSPORTALWEBSetup.log|Registreert de installatieactiviteiten van de Application Catalog-website.|Sitesysteemserver|  
|SMSProv.log|Registreert toegang van de WMI-provider tot de sitedatabase.|Computer met de SMS-provider|  
|srsrpMSI.log|Registreert gedetailleerde resultaten van het installatieproces van het rapportagepunt uit de MSI-output.|Sitesysteemserver|  
|srsrpsetup.log|Registreert resultaten van het installatieproces van het rapportagepunt.|Sitesysteemserver|  
|statesys.log|Registreert de verwerking van statussysteemberichten.|Siteserver|  
|statmgr.log|Registreert het schrijven van alle statusberichten naar de database.|Siteserver|  
|swmproc.log|Registreert de verwerking van meterbestanden en instellingen.|Siteserver|  

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a>Installatie van de site server

De volgende tabel bevat de logboekbestanden die informatie bevatten over de site-installatie.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Registreert vereiste onderdelen voor evaluatie en installatie van componenten.|Siteserver|  
|ConfigMgrSetup.log|Registreert gedetailleerde uitvoer van de installatie van de site server.|Siteserver|  
|ConfigMgrSetupWizard.log|Registreert informatie met betrekking tot de activiteit in de installatie wizard.|Siteserver|  
|SMS_BOOTSTRAP.log|Registreert informatie over de voortgang van de lancering van het installatieproces voor de secundaire site. Details van het werkelijke installatieproces zijn opgenomen in ConfigMgrSetup.log.|Siteserver|  
|smstsvc.log|Registreert informatie over de installatie, het gebruik en de verwijdering van een Windows-service. Windows gebruikt deze service om de netwerk verbinding en machtigingen tussen servers te testen. Het computer account van de server die de verbinding maakt, wordt gebruikt.|Site server en site systeem server|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a>Data Warehouse-service punt

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot het Data Warehouse-service punt.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|DWSSMSI. log|Registreert berichten die zijn gegenereerd door de installatie van een Data Warehouse-service punt.|Sitesysteemserver|  
|DWSSSetup. log|Registreert berichten die zijn gegenereerd door de installatie van een Data Warehouse-service punt.|Sitesysteemserver|  
|Micro soft. ConfigMgrDataWarehouse. log|Registreert informatie over gegevens synchronisatie tussen de site database en de Data Warehouse-data base.|Sitesysteemserver|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a>Terugval status punt

De volgende tabel bevat de logboekbestanden die informatie bevatten over het terugvalstatuspunt.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Registreert gegevens over communicatie naar een terugvalstatuspunt van verouderde clients van mobiele apparaten en clientcomputers.|Sitesysteemserver|  
|fspMSI.log|Registreert berichten die gegenereerd worden door de installatie van een terugvalstatuspunt.|Sitesysteemserver|  
|fspmgr.log|Registreert activiteiten van de sitesysteemrol terugvalstatuspunt.|Sitesysteemserver|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a> Beheerpunt

De volgende tabel bevat de logboekbestanden die informatie bevatten over het beheerpunt.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Registreert activiteiten met betrekking tot clientberichten op het eindpunt.|Sitesysteemserver|  
|MP_CliReg.log|Registreert activiteiten met betrekking tot clientregistratie, verwerkt door het beheerpunt.|Sitesysteemserver|  
|MP_Ddr.log|Registreert de conversie van XML. DDR-records van clients en kopieert deze vervolgens naar de site server.|Sitesysteemserver|  
|MP_Framework.log|Registreert de activiteiten van het kernbeheerpunt en componenten van het clientframework.|Sitesysteemserver|  
|MP_GetAuth.log|Registreert activiteiten met betrekking tot clientautorisatie.|Sitesysteemserver|  
|MP_GetPolicy.log|Registreert activiteiten met betrekking tot beleidsaanvragen van clientcomputers.|Sitesysteemserver|  
|MP_Hinv.log|Registreert details over de conversie van XML hardware-inventarisrecords van clients en de kopie van die bestanden naar de siteserver.|Sitesysteemserver|  
|MP_Location.log|Registreert activiteiten met betrekking tot locatieaanvragen en antwoorden van clients.|Sitesysteemserver|  
|MP_OOBMgr.log|Registreert de beheer punt activiteiten met betrekking tot het ontvangen van een OTP van een client.|Sitesysteemserver|  
|MP_Policy.log|Registreert beleidcommunicatie.|Sitesysteemserver|  
|MP_Relay.log|Registreert het overdragen van bestanden die worden opgehaald van de client.|Sitesysteemserver|  
|MP_Retry.log|Registreert processen voor nieuwe pogingen voor hardware-inventarisatie.|Sitesysteemserver|  
|MP_Sinv.log|Registreert details over de conversie van XML software-inventarisrecords van clients en de kopie van die bestanden naar de siteserver.|Sitesysteemserver|  
|MP_SinvCollFile.log|Registreert details over bestandsverzameling.|Sitesysteemserver|  
|MP_Status.log|Registreert details over de conversie van XML.svf statusberichtbestanden van clients en de kopie van die bestanden naar de siteserver.|Sitesysteemserver|
|mpcontrol.log|Registreert de registratie van het beheerpunt met WINS. Registreert elke 10 minuten de beschikbaarheid van het beheerpunt.|Siteserver|  
|mpfdm.log|Registreert de acties van de beheerpuntcomponent die clientbestanden verplaatst naar de corresponderende POSTVAKKEN IN-map op de siteserver.|Sitesysteemserver|  
|mpMSI.log|Registreert gegevens over de installatie van het beheer punt.|Siteserver|  
|MPSetup.log|Registreert het wrapperproces van de beheerpuntinstallatie.|Siteserver|  
|UserService. log|Registreert gebruikers aanvragen van software Center, waarbij gebruikers beschik bare toepassingen worden opgehaald van de server.|Sitesysteemserver|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a>Service verbindings punt

In de volgende tabel worden de logboekbestanden vermeld die gegevens bevatten die betrekking hebben op het serviceverbindingspunt.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Registreert certificaat- en proxy-accountgegevens.|Siteserver|  
|CollEval.log|Registreert gegevens over wanneer verzamelingen worden gemaakt, gewijzigd en verwijderd door de Verzamelingevaluator.|Primaire site en centrale beheersite|  
|Cloudusersync.log|Registreert inschakelen van licensies voor gebruikers.|Computer met het serviceverbindingspunt|  
|Dataldr.log|Registreert gegevens over de verwerking van MIF-bestanden.|Siteserver|  
|ddm.log|Registreert activiteiten van de Discovery Data Manager.|Siteserver|  
|Distmgr.log|Registreert gegevens over aanvragen voor distributie van inhoud.|Siteserver op het hoogste niveau|  
|Dmpdownloader.log|Registreert gegevens over down loads van Microsoft Intune.|Computer met het serviceverbindingspunt|  
|Dmpuploader.log|Registreert Details met betrekking tot het uploaden van database wijzigingen naar Microsoft Intune.|Computer met het serviceverbindingspunt|  
|hman.log|Registreert informatie over het doorsturen van berichten.|Siteserver|  
|MSfBSyncWorker. log|Registreert informatie over de communicatie met de Microsoft Store voor bedrijven.|Computer met het serviceverbindingspunt|
|objreplmgr.log|Registreert de verwerking van beleid en toewijzing.|Primaire siteserver|  
|PolicyPV.log|Registreert het beleid van het genereren van alle beleidsregels.|Siteserver|  
|outgoingcontentmanager.log|Registreert inhoud die is geüpload naar Microsoft Intune.|Computer met het serviceverbindingspunt|  
|Sitecomp.log|Hierin worden de gegevens over de installatie van het serviceverbindingspunt vastgelegd.|Siteserver|  
|SmsAdminUI.log|Registreert Configuration Manager-console activiteit.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  
|SMS_CLOUDCONNECTION. log|Registreert informatie over Cloud Services.|Computer met het serviceverbindingspunt|
|Smsprov.log|Registreert activiteiten van de SMS-provider. Configuration Manager-console activiteiten gebruiken de SMS-provider.|Computer met de SMS-provider|  
|SrvBoot.log|Hierin worden de gegevens over de service met het installatieprogramma voor het serviceverbindingspunt vastgelegd.|Computer met het serviceverbindingspunt|  
|Statesys.log|Registreert de verwerking van berichten voor het beheer van mobiele apparaten.|Primaire site en centrale beheersite|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a> Software-updatepunt

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot het software-update punt.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Registreert gegevens over de replicatie van meldings bestanden voor software-updates van een bovenliggende site naar onderliggende sites.|Siteserver|  
|PatchDownloader.log|Registreert gegevens over het proces van downloaden van software-updates van de updatebron naar de downloadbestemming op de siteserver.|Wanneer u updates hand matig downloadt, bevindt dit bestand zich in de `%temp%` map op de computer waarop u de-console gebruikt. Voor automatische implementatie regels geldt dat als de Configuration Manager-client op de site server is geïnstalleerd, dit bestand zich op de site server in bevindt `%windir%\CCM\Logs` .|  
|ruleengine.log|Registreert details over automatische implementatieregels voor de identificatie, het downloaden van software, en maken van software-updategroepen en implementaties.|Siteserver|
|SMS_ISVUPDATES_SYNCAGENT. log| Logboek bestand voor synchronisatie van software-updates van derden.| Software-update punt op het hoogste niveau in de hiërarchie van de Configuration Manager.|
|SUPSetup.log|Registreert gegevens over de installatie van het software-updatepunt. Wanneer de installatie van het software-updatepunt is voltooid, wordt **Installatie is geslaagd** geschreven naar dit logboekbestand.|Sitesysteemserver|  
|WCM.log|Registreert gegevens over de configuratie van het software-update punt en verbindingen met de WSUS-server voor geabonneerde update categorieën, classificaties en talen.|Site server die verbinding maakt met de WSUS-server|  
|WSUSCtrl.log|Registreert gegevens over de configuratie, databaseconnectiviteit en status van de WUS-server voor de site.|Sitesysteemserver|  
|wsyncmgr.log|Registreert gegevens over het synchronisatie proces van software-updates.|Sitesysteemserver|  
|WUSSyncXML.log|Registreert gegevens over het inventarisatie hulpprogramma voor het micro soft updates-synchronisatie proces.|Client computer die is geconfigureerd als de synchronisatieclient voor het inventarisatie hulpprogramma voor micro soft updates|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a>Logboek bestanden op functionaliteit

De volgende secties bevatten een lijst met logboek bestanden met betrekking tot Configuration Manager-functies.  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a>Toepassings beheer

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot toepassings beheer.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Registreert gegevens over de huidige en beoogde status van toepassingen, hun toepasbaarheid, of voldaan werd aan de vereisten, implementatietypes en afhankelijkheden.|Client|  
|AppDiscovery.log|Registreert de gegevens over de gevonden of gedetecteerde toepassingen op clientcomputers.|Client|  
|AppEnforce.log|Registreert gegevens over afdwingacties (installeren en verwijderen) die genomen werden voor toepassingen op de client.|Client|  
|AppGroupHandler. log|Starten met versie 1906, informatie over detectie en afdwinging voor toepassings groepen|Client|
|awebsctl.log|Registreert bewakings activiteiten voor de site systeemrol toepassingscatalogus-webservicepunt.|Sitesysteemserver|  
|awebsvcMSI.log|Registreert gedetailleerde informatie voor de sitesysteemrol van het Application Catalog-webservicepunt.|Sitesysteemserver|  
|BusinessAppProcessWorker. log|Record verwerking voor Microsoft Store voor zakelijke apps.|Siteserver|
|Ccmsdkprovider.log|Registreert de activiteiten van het toepassingsbeheer SDK.|Client|  
|colleval.log|Registreert gegevens over wanneer verzamelingen worden gemaakt, gewijzigd en verwijderd door de Verzamelingevaluator.|Sitesysteemserver|  
|ConfigMgrSoftwareCatalog.log|Registreert de activiteit van de Application Catalog, wat zijn gebruik van Silverlight bevat.|Client|  
|MSfBSyncWorker. log|Registreert informatie over de communicatie met de Microsoft Store voor bedrijven.|Computer met het serviceverbindingspunt|
|NotiCtrl. log|Meldingen over toepassings aanvragen.|Siteserver|  
|portlctl.log|Registreert de bewakingsactiviteiten voor de sitesysteemrol van het Application Catalog-websitepunt.|Sitesysteemserver|  
|portlwebMSI.log|Registreert de MSI installatieactiviteit voor de Application Catalog-website.|Sitesysteemserver|  
|PrestageContent.log|Registreert gegevens over het gebruik van het hulp programma Extract content. exe op een extern, vooraf geplaatst distributie punt. Dit hulpprogramma extraheert inhoud die werd geëxporteerd naar een bestand.|Sitesysteemserver|  
|ServicePortalWebService.log|Registreert de activiteit van de Application Catalog-webservice.|Sitesysteemserver|  
|ServicePortalWebSite.log|Registreert de activiteit van de Application Catalog-website.|Sitesysteemserver|  
|SettingsAgent. log|Afdwinging van specifieke toepassingen, registratie van de evaluatie van de toepassings groep en Details van het beleid voor co-beheer.|Client|
|SMS_BUSINESS_APP_PROCESS_MANAGER. log|Het logboek bestand voor het onderdeel dat apps synchroniseert vanuit de Microsoft Store voor bedrijven.|Siteserver|
|SMS_CLOUDCONNECTION. log|Registreert informatie over Cloud Services.|Computer met het serviceverbindingspunt|
|SMSdpmon.log|Registreert gegevens over de geplande taak van statusbewaking van het distributiepunt, dat op een distributiepunt geconfigureerd is.|Siteserver|  
|SoftwareCatalogUpdateEndpoint.log|Registreert activiteiten voor het beheren van de URL voor de toepassingscatalogus weer gegeven in Software Center.|Client|  
|SoftwareCenterSystemTasks.log|Registreert activiteiten die betrekking hebben op de validatie van vereiste onderdelen voor Software Center.|Client|  
|TSDTHandler. log|Voor het implementatie type van de taken reeks. Het proces wordt geregistreerd bij het afdwingen van de app (installeren of verwijderen) voor het starten van de taken reeks. Gebruik het met AppEnforce. log en bestand smsts. log.|Client|<!-- MEMDocs#336 -->

#### <a name="packages-and-programs"></a>Pakketten en programma's

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot het implementeren van pakketten en programma's.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|colleval.log|Registreert gegevens over wanneer verzamelingen worden gemaakt, gewijzigd en verwijderd door de Verzamelingevaluator.|Siteserver|  
|execmgr.log|Registreert gegevens over pakketten en takenreeksen die worden uitgevoerd.|Client|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a>Asset Intelligence

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot asset intelligence.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Registreert de activiteiten van Asset Intelligence-inventarisatie-acties.|Client|  
|aikbmgr.log|Registreert gegevens over de verwerking van XML-bestanden van het postvak IN voor het updaten van de asset intelligence-catalogus.|Siteserver|  
|AIUpdateSvc.log|Registreert de interactie van het Asset Intelligence synchronisatie punt met de Cloud service.|Sitesysteemserver|  
|AIUSMSI.log|Registreert gegevens over de installatie van de site systeemrol Asset Intelligence synchronisatie punt.|Sitesysteemserver|  
|AIUSSetup.log|Registreert gegevens over de installatie van de site systeemrol Asset Intelligence synchronisatie punt.|Sitesysteemserver|  
|ManagedProvider.log|Registreert gegevens over detectie van software met een gekoppelde software-identificatietag. Registreert ook activiteiten met betrekking tot de hardware-inventarisatie.|Sitesysteemserver|  
|MVLSImport.log|Registreert gegevens over de verwerking van de geïmporteerde licentiegegevens bestanden.|Sitesysteemserver|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a>Back-up en herstel

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot back-up-en herstel acties, waaronder site resets en wijzigingen aan de SMS-provider.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Registreert informatie over installatie-en herstel taken wanneer Configuration Manager een site herstelt vanuit een back-up.|Siteserver|  
|Smsbkup.log|Registreert gegevens over de site back-up van de activiteit.|Siteserver|  
|smssqlbkup.log|Registreert uitvoer van het back-upproces van de site database wanneer SQL Server is geïnstalleerd op een server die niet de site server is.|Sitedatabaseserver|  
|Smswriter.log|Registreert informatie over de status van de Configuration Manager VSS Writer die wordt gebruikt door het back-upproces.|Siteserver|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a>Certificaat inschrijving

De volgende tabel bevat de Configuration Manager-logboek bestanden die informatie bevatten met betrekking tot certificaat inschrijving. Certificaat inschrijving maakt gebruik van het certificaat registratiepunt en de Configuration Manager-beleids module op de server waarop de registratie service voor netwerk apparaten (NDES) wordt uitgevoerd.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|CRP.log|Registreert inschrijvings activiteiten.|Certificaatregistratiepunt|  
|Crpctrl.log|Registreert de operationele status van het registratiepunt van het certificaat.|Certificaatregistratiepunt|  
|Crpsetup.log|Registreert gegevens over de installatie en configuratie van het certificaatregistratiepunt.|Certificaatregistratiepunt|  
|Crpmsi.log|Registreert gegevens over de installatie en configuratie van het certificaatregistratiepunt.|Certificaatregistratiepunt|  
|NDESPlugin.log|Registreert vraag verificatie en activiteiten voor het inschrijven van certificaten.|Configuration Manager-beleids module en registratie service voor netwerk apparaten|  

Controleer, samen met de Configuration Manager-logboek bestanden, de Windows-toepassings Logboeken in Logboeken op de server waarop de registratie service voor netwerk apparaten wordt uitgevoerd en de server die het certificaat registratiepunt host. Zoek bijvoorbeeld naar berichten van de bron **NetworkDeviceEnrollmentService**.

U kunt ook de volgende logboekbestanden gebruiken:  

- IIS-logboek bestanden voor registratie service voor netwerk apparaten: **%systemdrive%\inetpub\logs\LogFiles\W3SVC1**  

- IIS-logboek bestanden voor het certificaat registratiepunt: **%systemdrive%\inetpub\logs\LogFiles\W3SVC1**  

- Logboekbestand voor Registratiebeleid voor netwerkapparaten: **mscep.log**  

    > [!NOTE]  
    > Dit bestand bevindt zich in de map voor het NDES-account profiel, bijvoorbeeld in C:\Users\SCEPSvc. Zie de sectie [logboek registratie inschakelen](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging) van de NDES-wiki voor meer informatie over het inschakelen van NDES-logboek registratie.  

### <a name="client-notification"></a><a name="BKMK_BGB"></a>Client melding

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot clientmelding.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Registreert gegevens over site server activiteiten met betrekking tot client meldings taken en het verwerken van online-en taak status bestanden.|Siteserver|  
|BGBServer.log|Registreert de activiteiten van de meldings server, zoals client-server communicatie en het pushen van taken naar clients. Registreert ook informatie over het genereren van online-en taak status bestanden die moeten worden verzonden naar de site server.|Beheerpunt|  
|BgbSetup.log|Registreert de activiteiten van het proces voor de installatie van de meldingen server tijdens installatie en verwijdering.|Beheerpunt|  
|bgbisapiMSI.log|Registreert gegevens over de installatie en verwijdering van de meldings server.|Beheerpunt|  
|BgbHttpProxy.log|Registreert de activiteiten van de HTTP-meldingsproxy zoals het de berichten van clients die HTTP gebruiken, overdraagt naar en van de meldingsserver.|Client|  
|CcmNotificationAgent.log|Registreert de activiteiten van de meldings agent, zoals client-server communicatie en informatie over taken die zijn ontvangen en verzonden naar andere client agenten.|Client|  

### <a name="cloud-management-gateway"></a>Cloudbeheergateway

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot de Cloud beheer gateway.

|Logboeknaam|Beschrijving|Computer met logboekbestand|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Registreert gegevens over de implementatie van de Cloud beheer Gateway-Service, de status van de actieve service en het gebruik van gegevens die aan de service zijn gekoppeld. Als u het logboek registratie niveau wilt configureren, bewerkt u de waarde voor het **registratie niveau** in de volgende register sleutel:`HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|De map *InstallDir* op de primaire site server of de certificerings instantie.|
|CMGSetup. log <sup> [Opmerking 1](#bkmk_note1)</sup>|Registreert gegevens over de tweede fase van de implementatie van de Cloud beheer gateway (lokale implementatie in Azure). Als u het logboek registratie niveau wilt configureren, gebruikt u het **tracerings niveau** instellen (**gegevens** (standaard), **verbose**, **fout**) op het tabblad **configuratie van Azure portal\Cloud Services** .|De **%AppRoot%\logs** op uw Azure-server, of de map SMS/logs op de site systeem server|
|CMGService. log <sup> [Opmerking 1](#bkmk_note1)</sup>|Registreert gegevens over het kern onderdeel van de Cloud Management Gateway-Service in Azure. Als u het logboek registratie niveau wilt configureren, gebruikt u het **tracerings niveau** instellen (**gegevens** (standaard), **verbose**, **fout**) op het tabblad **configuratie van Azure portal\Cloud Services** .|De **%AppRoot%\logs** op uw Azure-server, of de map SMS/logs op de site systeem server|
|SMS_Cloud_ProxyConnector. log|Registreert gegevens over het instellen van verbindingen tussen de Cloud beheer Gateway-Service en het verbindings punt van de Cloud beheer gateway.|Sitesysteemserver|
|CMGContentService. log <sup> [Opmerking 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->Wanneer u een CMG inschakelt om ook inhoud van Azure Storage te verwerken, worden in dit logboek de details van die service vastgelegd.|De **%AppRoot%\logs** op uw Azure-server, of de map SMS/logs op de site systeem server|

- Gebruik **CloudMgr. log** en **CMGSetup. log** voor het oplossen van problemen met implementaties.
- Gebruik **CMGService. log** en **SMS_Cloud_ProxyConnector. log**voor het oplossen van problemen met de service status.
- Voor het oplossen van problemen met client verkeer gebruikt u **CMGHttpHandler. log**, **CMGService. log**en **SMS_Cloud_ProxyConnector. log**.

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a>Opmerking 1: logboeken die zijn gesynchroniseerd vanuit Azure

Dit zijn lokale Configuration Manager-logboek bestanden die Cloud Service Manager elke vijf minuten synchroniseert vanuit Azure Storage. De Cloud beheer gateway pusht elke vijf minuten logboeken naar Azure Storage. De maximale vertraging is 10 minuten. Uitgebreide switches beïnvloeden zowel lokale als externe logboeken. De daad werkelijke bestands namen bevatten de service naam en de instantie-id van de rol. Bijvoorbeeld CMG-*servicenaam* - *RoleInstanceID*-CMGSetup. log

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a>Instellingen voor naleving en toegang tot bedrijfs bronnen

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot nalevingsinstellingen en toegang tot bedrijfsbronnen.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Registreert gegevens over het proces van herstel en naleving voor nalevingsinstellingen, software-updates en replicatiebeheer.|Client|  
|CITaskManager.log|Registreert informatie over de taakplanning voor configuratie-item.|Client|  
|DCMAgent.log|Registreert informatie op hoog niveau over de beoordeling, rapportage van conflicten en herstel van configuratie-items en -toepassingen.|Client|  
|DCMReporting.log|Registreert informatie over rapportagebeleid van platformresultaten in statusberichten voor configuratie-items.|Client|  
|DcmWmiProvider.log|Registreert informatie over het lezen van configuratie-item synclets van WMI.|Client|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a>Configuration Manager-console

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot de Configuration Manager-console.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Registreert de installatie van de Configuration Manager-console.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  
|SmsAdminUI.log|Registreert informatie over de werking van de Configuration Manager-console.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  
|Smsprov.log|Registreert activiteiten van de SMS-provider. Configuration Manager-console activiteiten gebruiken de SMS-provider.|Siteserver of sitesysteemserver|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a>Inhouds beheer

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot inhoudbeheer.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|CloudDP- &lt; GUID \> . log|Registreert gegevens voor een specifiek clouddistributiepunt, inclusief informatie over opslag en toegang tot inhoud.|Sitesysteemserver|  
|CloudMgr.log|Registreert gegevens over het inrichten van inhoud, verzamelen van opslag-en bandbreedte statistieken en door de beheerder geïnitieerde acties om de Cloud service die een cloud-gebaseerd distributie punt uitvoert, te stoppen of te starten.|Sitesysteemserver|  
|DataTransferService.log|Registreert alle BITS-communicatie voor beleids- of pakkettoegang. Dit logboek wordt ook gebruikt voor inhouds beheer door pull-distributie punten.|Computer die is geconfigureerd als een pull-distributie punt|  
|PullDP.log|Registreert gegevens over inhoud die het pull-distributiepunt overdraagt van brondistributiepunten.|Computer die is geconfigureerd als een pull-distributie punt|  
|PrestageContent.log|Registreert de details over het gebruik van het hulp programma Extract content. exe op een extern, vooraf geplaatst distributie punt. Dit hulpprogramma extraheert inhoud die werd geëxporteerd naar een bestand.|Sitesysteemrol|  
|SMSdpmon.log|Registreert gegevens over geplande taken voor status controle van distributie punten die zijn geconfigureerd op een distributie punt.|Sitesysteemrol|  
|smsdpprov.log|Registreert gegevens over de extractie van gecomprimeerde bestanden die ontvangen worden van een primaire site. Dit logboek wordt gegenereerd door de WMI-provider van het externe distributie punt.|Distributiepunt computer die zich niet op de site server bevindt|  
|smsdpusage. log|Registreert Details over de smsdpusage. exe die gegevens uitvoert en verzamelt voor het overzichts rapport over het gebruik van distributie punten.|Sitesysteemrol|  

### <a name="desktop-analytics"></a>Desktop Analytics

Gebruik de volgende logboek bestanden voor hulp bij het oplossen van problemen met Desktop Analytics die is geïntegreerd met Configuration Manager.

De logboek bestanden op het service verbindings punt bevinden zich in de volgende map: `%ProgramFiles%\Configuration Manager\Logs\M365A` .
De logboek bestanden op de Configuration Manager-client bevinden zich in de volgende map: `%WinDir%\CCM\logs` .

| Logboek | Beschrijving |Computer met logboekbestand|
|---------|---------|---------|
| M365ADeploymentPlanWorker. log | Informatie over het implementatie plan synchronisatie van de Cloud service van Desktop Analytics naar een on-premises Configuration Manager |Serviceverbindingspunt|
| M365ADeviceHealthWorker. log | Informatie over het uploaden van apparaatstatus van Configuration Manager naar micro soft Cloud |Serviceverbindingspunt|
| M365AHandler. log | Informatie over het instellingen beleid voor desktop Analytics |Client|
| M365AUploadWorker. log | Informatie over de verzameling en het uploaden van apparaten van Configuration Manager naar micro soft Cloud |Serviceverbindingspunt|
| SmsAdminUI.log | Informatie over Configuration Manager-console activiteit, zoals het configureren van de Azure Cloud Services  |Serviceverbindingspunt|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a>Detectie

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot detectie.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Registreert detectieacties Active Directory-beveiligingsgroep.|Siteserver|  
|adsysdis.log|Registreert detectieacties Active Directory-systeem.|Siteserver|  
|adusrdis.log|Registreert detectieacties Active Directory-gebruiker.|Siteserver|  
|ADForestDisc.Log|Registreert detectieacties Active Directory-forest.|Siteserver|  
|ddm.log|Registreert activiteiten van de Discovery Data Manager.|Siteserver|  
|InventoryAgent.log|Registreert activiteiten van hardware-inventaris, software-inventaris en heartbeat-detectieacties op de client.|Client|  
|netdisc.log|Registreert netwerkdetectieacties.|Siteserver|  

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a>Endpoint Protection

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot Endpoint Protection.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Registreert gegevens over de installatie van de Endpoint Protection-client en de toepassing van anti-malware-beleid voor deze client.|Client|  
|EPCtrlMgr.log|Registreert gegevens over de synchronisatie van informatie over malware-bedreiging van de Endpoint Protection-functie server met de Configuration Manager-Data Base.|Sitesysteemserver|  
|EPMgr.log|Bewaakt de status van de Endpoint Protection-sitesysteemrol.|Sitesysteemserver|  
|EPSetup.log|Geeft informatie over de installatie van de Endpoint Protection-sitesysteemrol.|Sitesysteemserver|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a>Extensions

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot uitbrei dingen.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Registreert informatie over het downloaden van uitbreidingen van Microsoft en de installatie en verwijdering van alle uitbreidingen.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  
|FeatureExtensionInstaller.log|Registreert informatie over het installeren en verwijderen van afzonderlijke uitbrei dingen wanneer deze zijn in-of uitgeschakeld in de Configuration Manager-console.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  
|SmsAdminUI.log|Registreert Configuration Manager-console activiteit.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a>Tell

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot het verwerken van inventarisgegevens.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Registreert informatie over de verwerking van MIF-bestanden en hardware-inventaris in de Configuration Manager-Data Base.|Siteserver|  
|invproc.log|Registreert het doorsturen van MIF-bestanden van een secundaire site naar de daarboven liggende site.|Secundaire siteserver|  
|sinvproc.log|Registreert informatie over het verwerking van software-inventarisgegevens naar de sitedatabase.|Siteserver|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a>Licentie controle

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot meting.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Bewaakt alle softwarelicentiecontroleprocessen.|Client|  
|SWMTRReportGen.log|Hiermee wordt een rapport met gebruiks gegevens gegenereerd dat wordt verzameld door de agent voor licentie controle. Deze gegevens worden geregistreerd in Mtrmgr.log.|Client|
|swmproc.log|Registreert de verwerking van meterbestanden en instellingen.|Siteserver|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a>Virtuelemachinemigratie

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot migratie.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Registreert informatie over migratieacties die migratietaken, gedeelde distributiepunten en distributiepuntupdates bevatten.|Site op het hoogste niveau in de hiërarchie van de Configuration Manager en elke onderliggende primaire site. Gebruik, in een sitehiërarchie met meerdere primaire sites, het logboekbestand gemaakt in de centrale beheersite.|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a>Mobiele apparaten

De volgende secties geven een lijst van de logboek bestanden die informatie bevatten met betrekking tot het beheren van mobiele apparaten.  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a>Inschrijving

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot registratie van mobiele apparaten.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Registreert communicatie tussen beheerpunten die ingeschakeld zijn voor mobiele apparaten en de eindpunten van beheerpunten.|Sitesysteemserver|  
|dmpmsi.log|Registreert de Windows installergegevens voor de configuratie van een beheerpunt dat is ingeschakeld voor mobiele apparaten.|Sitesysteemserver|  
|DMPSetup.log|Registreert de configuratie van het beheer punt wanneer deze is ingeschakeld voor mobiele apparaten.|Sitesysteemserver|  
|enrollsrvMSI.log|Registreert de Windows Installer-gegevens voor de configuratie van een registratiepunt.|Sitesysteemserver|  
|enrollmentweb.log|Registreert communicatie tussen mobiele apparaten en het proxypunt voor registratie.|Sitesysteemserver|  
|enrollwebMSI.log|Registreert de Windows Installer-gegevens voor de configuratie van een registratieproxypunt.|Sitesysteemserver|  
|enrollmentservice.log|Registreert communicatie tussen het registratieproxypunt en het registratiepunt.|Sitesysteemserver|  
|SMS_DM.log|Registreert communicatie tussen mobiele apparaten, Mac-computers en het beheer punt dat is ingeschakeld voor mobiele apparaten en Mac-computers.|Sitesysteemserver|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a>Exchange Server-connector

De volgende logboeken bevatten informatie met betrekking tot de Exchange Server-connector.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Registreert de activiteiten en de status van de Exchange Server-connector.|Siteserver|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a>Mobiel apparaat verouderd

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot verouderde clients van mobiele apparaten.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Registreert gegevens over certificaatregistratiegegevens op verouderde clients van mobiele apparaten.|Client|  
|DMCertResp.htm|Registreert het HTML-antwoord van de certificaatserver wanneer het enroller-programma van de verouderde client van mobiele apparaten een PKI-certificaat vraagt.|Client|  
|DmClientHealth.log|Registreert de GUID'S van alle verouderde clients van mobiele apparaten die communiceren met het beheer punt dat voor mobiele apparaten is ingeschakeld.|Sitesysteemserver|  
|DmClientRegistration.log|Registreert registratieverzoeken en antwoorden naar en van verouderde clients van mobiele apparaten.|Sitesysteemserver|  
|DmClientSetup.log|Registreert clientinstellingsgegevens voor verouderde clients voor mobiele apparaten.|Client|  
|DmClientXfer.log|Registreert overdrachtgegevens voor verouderde clients van mobiele apparaten en ActiveSync-implementaties.|Client|  
|DmCommonInstaller.log|Registreert installatie van overdrachtsbestand van client voor het configureren van overdrachtsbestanden voor verouderde clients van mobiele apparaten.|Client|  
|DmInstaller.log|Registreert of DMInstaller een juiste oproep dat naar DmClientSetup en of DmClientSetup met succes afsluit of integendeel faalt voor verouderde clients van mobiele apparaten.|Client|  
|DmpDatastore.log|Registreert alle databaseverbindingen en -query's die gemaakt worden door het distributiepunt dat ingeschakeld is voor mobiele apparaten.|Sitesysteemserver|  
|DmpDiscovery.log|Registreert alle detectiegegevens van de verouderde clients van mobiele apparaten op het beheerpunt dat ingeschakeld is voor mobiele apparaten.|Sitesysteemserver|  
|DmpHardware.log|Registreert hardware-inventarisgegevens van verouderde clients van mobiele apparaten op het beheerpunt dat voor mobiele apparaten is ingeschakeld.|Sitesysteemserver|  
|DmpIsapi.log|Registreert communicatie van verouderde clients van mobiele met een beheerpunt dat is ingeschakeld voor mobiele apparaten.|Sitesysteemserver|  
|dmpmsi.log|Registreert de Windows installergegevens voor de configuratie van een beheerpunt dat is ingeschakeld voor mobiele apparaten.|Sitesysteemserver|  
|DMPSetup.log|Registreert de configuratie van het beheer punt wanneer deze is ingeschakeld voor mobiele apparaten.|Sitesysteemserver|  
|DmpSoftware.log|Registreert software-distributiegegevens van verouderde clients van mobiele apparaten op een beheerpunt dat voor mobiele apparaten is ingeschakeld.|Sitesysteemserver|  
|DmpStatus.log|Registreert statusberichten van clients van mobiele apparaten op een beheerpunt dat voor mobiele apparaten is ingeschakeld.|Sitesysteemserver|  
|DmSvc.log|Registreert clientcommunicatie van verouderde clients van mobiele apparaten met een beheerpunt dat is ingeschakeld voor mobiele apparaten.|Client|  
|FspIsapi.log|Registreert gegevens over communicatie naar een terugvalstatuspunt van verouderde clients van mobiele apparaten en clientcomputers.|Sitesysteemserver|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a>Implementatie van besturings systeem

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot de implementatie van het besturings systeem.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|CAS.log|Registreert gegevens van de records wanneer distributiepunten zijn gevonden voor inhoud waarnaar wordt verwezen.|Client|  
|ccmsetup.log|Registreert ccmsetup-taken voor clientinstallatie, clientupgrade en clientverwijdering. Kan worden gebruikt voor het oplossen van problemen tijdens de installatie van de client.|Client|  
|CreateTSMedia.log|Registreert gegevens voor de taak mediacreatie sequentiëren.|Computer waarop de Configuration Manager-console wordt uitgevoerd|  
|DISM.log|Registreert installatie acties voor Stuur Programma's of werk toepassings acties bij voor offline onderhoud.|Sitesysteemserver|  
|Distmgr.log|Registreert gegevens over de configuratie van het inschakelen van een distributie punt voor Preboot Execution Environment (PXE).|Sitesysteemserver|  
|DriverCatalog.log|Registreert gegevens over stuurprogramma's voor apparaten die in de stuurprogrammacatalogus werden geïmporteerd.|Sitesysteemserver|  
|mcsisapi.log|Legt Informatie vast voor multicast-pakketoverdracht en antwoorden op client-vragen.|Sitesysteemserver|  
|mcsexec.log|Registreert de status controle, de naam ruimte, het maken van sessies en de acties voor certificaat controles.|Sitesysteemserver|  
|mcsmgr.log|Registreert wijzigingen in de configuratie, beveiligings modus en beschik baarheid.|Sitesysteemserver|  
|mcsprv.log|Legt multicast-provider interactie vast met Windows Deployment Services (WDS).|Sitesysteemserver|  
|MCSSetup.log|Registreert gegevens over de installatie van de rol multicastserver.|Sitesysteemserver|  
|MCSMSI.log|Registreert gegevens over de installatie van de rol multicastserver.|Sitesysteemserver|  
|Mcsperf.log|Registreert gegevens over de prestaties van multicast-prestatiemeter-updates.|Sitesysteemserver|  
|MP_ClientIDManager.log|Registreert beheer punt antwoorden op client-ID-aanvragen die door taken reeksen worden gestart vanaf PXE-of opstart media.|Sitesysteemserver|  
|MP_DriverManager.log|Registreert beheerpuntantwoorden op actieverzoeken van automatisch toepassen-takenreeksen.|Sitesysteemserver|  
|OfflineServicingMgr.log|Registreert gegevens van offline-onderhouds planningen en werk acties Toep assen op WIM-bestanden (Windows Imaging Format) van het besturings systeem.|Sitesysteemserver|  
|Setupact.log|Registreert gegevens over Windows Sysprep en installatielogboeken. Zie [logboek bestanden](https://docs.microsoft.com/windows/deployment/upgrade/log-files)voor meer informatie.|Client|  
|Setupapi.log|Registreert gegevens over Windows Sysprep en installatielogboeken.|Client|  
|Setuperr.log|Registreert gegevens over Windows Sysprep en installatielogboeken.|Client|  
|smpisapi.log|Registreert gegevens over de acties van vastleggen en herstellen van de clientstatus en drempelinformatie.|Client|  
|Smpmgr.log|Registreert gegevens over de resultaten van statuscontroles van statusmigratiepunt en configuratiewijzigingen.|Sitesysteemserver|  
|smpmsi.log|Registreert installatie- en configuratiegegevens over het statusmigratiepunt.|Sitesysteemserver|  
|smpperf.log|Registreert de tellerupdates van de prestatie van het statusmigratiepunt.|Sitesysteemserver|  
|smspxe.log|Registreert gegevens over de antwoorden op clients die PXE-opstart procedure gebruiken en gedetailleerde informatie over de uitbrei ding van opstart installatie kopieën en opstart bestanden.|Sitesysteemserver|  
|smssmpsetup.log|Registreert installatie- en configuratiegegevens over het statusmigratiepunt.|Sitesysteemserver|
| SMS_PhasedDeployment. log| Logboek bestand voor gefaseerde implementaties|Site op het hoogste niveau in de hiërarchie van de Configuration Manager|
|Smsts.log|Registreert takenreeksactiviteiten.|Client|  
|TSAgent.log|Registreert het resultaat van afhankelijkheden van takenreeks vóór een takenreeks gestart wordt.|Client|  
|TaskSequenceProvider.log|Registreert gegevens over taken reeksen wanneer ze worden geïmporteerd, geëxporteerd of bewerkt.|Sitesysteemserver|  
|Loadstate.log|Registreert gegevens over het hulpprogramma voor de migratie van gebruikersstatus (USMT) en het herstellen van gebruikerstatusgegevens.|Client|  
|Scanstate.log|Registreert gegevens over het hulpprogramma voor de migratie van gebruikersstatus (USMT) en het vastleggen van gebruikerstatusgegevens.|Client|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a>Energie beheer

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot energiebeheer.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|Registreert gegevens over energiebeheer activiteiten op de client computer, met inbegrip van bewaking en het afdwingen van instellingen door de client agent voor energie beheer.|Client|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a>Beheer op afstand

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot controle op afstand.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Registreert gegevens over de activiteit van beheer op afstand viewer.|Op de computer waarop de viewer voor beheer op afstand wordt uitgevoerd, in de map% Temp%.|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a>Rapporteren

De volgende tabel bevat de Configuration Manager-logboek bestanden die informatie bevatten met betrekking tot rapportage.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Registreert informatie over de activiteit en status van het rapportageservicepunt.|Sitesysteemserver|  
|srsrpMSI.log|Registreert gedetailleerde resultaten van het installatieproces van het rapportageservicepunt vanuit de MSI-output.|Sitesysteemserver|  
|srsrpsetup.log|Registreert resultaten van het installatieproces van Reporting Services-punt.|Sitesysteemserver|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a>Op rollen gebaseerd beheer

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot het beheren van beheer op basis van rollen.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|hman.log|Registreert informatie over site configuratie wijzigingen en het publiceren van site-informatie naar Active Directory Domain Services.|Siteserver|  
|SMSProv.log|Registreert toegang van de WMI-provider tot de sitedatabase.|Computer met de SMS-provider|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a>Software licentie controle

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot software licentie controle.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Bewaakt alle softwarelicentiecontroleprocessen.|Siteserver|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a>Software-updates

In de volgende tabel worden de logboekbestanden vermeld die gegevens bevatten die betrekking hebben op software-updates.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|AlternateHandler. log|Registreert gegevens wanneer de client de klik-en-klaar-COM-interface van Office aanroept om Microsoft 365-apps te downloaden en te installeren voor Enter prise-client updates. Het is vergelijkbaar met het gebruik van WuaHandler wanneer het de API van Windows Update Agent oproept om Windows-updates te downloaden en te installeren.<!-- SCCMDocs#888 -->|Client|
|ccmperf.log|Registreert activiteiten die betrekking hebben op het onderhoud en vastleggen van gegeven met betrekking tot clientprestatietellers.|Client|
|DeltaDownload. log|Registreert informatie over het downloaden van snelle updates en updates die zijn gedownload met behulp van leverings optimalisatie.|Client|  
|PatchDownloader.log|Registreert gegevens over het proces van downloaden van software-updates van de updatebron naar de downloadbestemming op de siteserver.|Wanneer updates hand matig worden gedownload, bevindt dit logboek bestand zich in de map% Temp% van de gebruiker die de-console uitvoert op de computer waarop de-console wordt uitgevoerd. Voor regels voor automatische implementatie bevindt dit logboek bestand zich op de site server in%windir%\CCM\Logs, als de ConfigMgr-client is geïnstalleerd op de site server.|  
|PolicyEvaluator.log|Registreert gegevens over de beoordeling van beleid op clientcomputer, met inbegrip van beleid vanaf software-updates.|Client|  
|RebootCoordinator.log|Registreert gegevens over de coördinatie van het herstarten van systemen op de clientcomputers na de installaties van de software-update.|Client|  
|ScanAgent.log|Registreert gegevens over scanverzoeken voor software-updates, de WSUS-locatie en gerelateerde acties.|Client|  
|SdmAgent.log|Registreert gegevens over het bijhouden van herstel en naleving. Het logboek bestand voor software-updates, Updatehandler. log, bevat echter meer informatie over het installeren van de software-updates die vereist zijn voor naleving. Dit logboekbestand wordt gedeeld met instellingen voor naleving.|Client|  
|ServiceWindowManager.log|Registreert gegevens over de evaluatie van onderhoudsvensters.|Client|
|SMS_ISVUPDATES_SYNCAGENT. log| Logboek bestand voor synchronisatie van software-updates van derden.| Software-update punt op het hoogste niveau in de hiërarchie van de Configuration Manager.|
|SMS_OrchestrationGroup. log| Logboek bestand voor Orchestration-groepen|Siteserver|
|SmsWusHandler.log|Registreert gegevens over het scanproces voor het inventarishulpprogramma voor Microsoft-updates.|Client|  
|StateMessage.log|Registreert gegevens over software-update status berichten die worden gemaakt en verzonden naar het beheer punt.|Client|  
|SUPSetup.log|Registreert gegevens over de installatie van het software-updatepunt. Wanneer de installatie van het software-updatepunt is voltooid, wordt **Installatie is geslaagd** geschreven naar dit logboekbestand.|Sitesysteemserver|  
|UpdatesDeployment.log|Registreert gegevens over implementaties op de client, met inbegrip van software-updateactiviteit, beoordeling en gedwongen uitvoering. Uitgebreide logboekregistratie toont bijkomende informatie over de interactie de clientgebruikersinterface.|Client|  
|UpdatesHandler.log|Registreert gegevens over scannen van naleving van software-update en over het downloaden en de installatie van software-updates op de client.|Client|  
|UpdatesStore.log|Registreert gegevens over nalevingsstatus voor de software-updates die beoordeeld werden tijdens de cyclus van de nalevingsscan.|Client|  
|WCM.log|Registreert gegevens over configuraties van software-update punten en verbindingen met de WSUS-server voor geabonneerde update categorieën, classificaties en talen.|Siteserver|  
|WSUSCtrl.log|Registreert gegevens over de configuratie, databaseconnectiviteit en status van de WUS-server voor de site.|Sitesysteemserver|  
|wsyncmgr.log|Registreert gegevens over het synchronisatie proces van de software-update.|Siteserver|  
|WUAHandler.log|Registreert gegevens over de Windows Update-agent op de client wanneer hij zoekt naar software-updates.|Client|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a>Wake On LAN

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot het gebruik van Wake On LAN.  

> [!NOTE]  
> Wanneer u Wake On LAN aanvullen met behulp van Wake-up proxy, wordt deze activiteit geregistreerd op de client. Zie bijvoorbeeld CcmExec. log en SleepAgent_<*domein* \> @SYSTEM_0.log in het gedeelte [client bewerkingen](#BKMK_ClientOpLogs) van dit artikel.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Registreert gegevens over welke clients ontwaakpakketten moeten toegestuurd krijgen, het aantal te zenden ontwaakpakketten en het aantal van opnieuw geprobeerde ontwaakpakketten.|Siteserver|  
|wolmgr.log|Registreert gegevens over ontwaakprocedures, zoals wanneer implementaties te activeren die geconfigureerd zijn voor Wake On LAN.|Siteserver|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a>Onderhoud van Windows 10

De volgende tabel geeft een lijst van de logboek bestanden die informatie bevatten met betrekking tot Windows 10-onderhoud.  
Onderhoud maakt gebruik van dezelfde infra structuur en hetzelfde proces als software-updates. Zie [software-updates](#BKMK_SU_NAPLog)voor andere logboeken die van toepassing zijn op het onderhouds scenario.

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|CBS. log|Registreert onderhouds fouten met betrekking tot wijzigingen voor Windows-updates of-rollen en-functies.|Client|
|DISM. log|Registreert alle acties met behulp van DISM. Als dat nodig is, verwijst DISM. log naar CBS. log voor meer informatie.|Client|
|bestand Setupact. log|Primair logboek bestand voor de meeste fouten die optreden tijdens het installatie proces van Windows. Het logboek bestand bevindt zich in de map% windir% \$ Windows. ~ BT\sources\panther.|Client|

Zie [logboek bestanden met betrekking tot online onderhoud](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files)voor meer informatie.

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a>Windows Update-Agent

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot de Windows Update-agent.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Registreert gegevens over wanneer de Windows Update Agent verbinding maakt met de WSUS-server en de software-updates voor de nalevings beoordeling ophaalt, en of er updates zijn voor de agent onderdelen.|Client|  

Zie [Windows Update-logboek bestanden](https://docs.microsoft.com/windows/deployment/update/windows-update-logs)voor meer informatie.

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a>WSUS-server

De volgende tabel geeft een lijst van de logboekbestanden die informatie bevatten met betrekking tot de WSUS-server.  

|Logboeknaam|Beschrijving|Computer met logboekbestand|  
|--------------|-----------------|----------------------------|  
|Change.log|Registreert gegevens over informatie over de WSUS-Server database die is gewijzigd.|WSUS-server|  
|SoftwareDistribution.log|Registreert gegevens over de software-updates die zijn gesynchroniseerd vanuit de geconfigureerde update bron naar de WSUS-Server database.|WSUS-server|  

Deze logboek bestanden bevinden zich in de `%ProgramFiles%\Update Services\LogFiles` map.

## <a name="see-also"></a>Zie ook

- [Logboekbestanden](about-log-files.md)

- [Ondersteunings centrum OneTrace](../../support/support-center-onetrace.md)

- [Logboek bestand viewer voor ondersteunings centrum](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)
