---
title: Wat is er nieuw in versie 1902
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1902 van Configuration Manager current branch.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 950146c694addc5be0b351278a381ff4839e7bca
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607781"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Wat is er nieuw in versie 1902 van Configuration Manager current branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1902 voor Configuration Manager current branch is beschikbaar als een update in de console. Deze update Toep assen op sites waarop versie 1802, 1806 of 1810 wordt uitgevoerd. <!-- baseline only statement:-->Wanneer u een nieuwe site installeert, is deze ook beschikbaar als basislijn versie. In dit artikel vindt u een overzicht van de wijzigingen en nieuwe functies in Configuration Manager, versie 1902.  

Bekijk altijd de laatste controle lijst voor het installeren van deze update. Zie [Check List for Install update 1902](../../servers/manage/checklist-for-installing-update-1902.md)(Engelstalig) voor meer informatie. Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).

Als u optimaal wilt profiteren van de nieuwe functies van Configuration Manager, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

<!-- > [!Note]  
> This article currently lists all significant features in this version. However, not all sections yet link to updated content with further information on the new features. Keep checking this page regularly for updates. Changes are noted with the ***[Updated]*** tag. This note will be removed when the content is finalized.  
 -->

> [!Tip]  
> Als u een melding wilt ontvangen wanneer deze pagina wordt bijgewerkt, kopieert en plakt u de volgende URL in uw RSS feed-lezer: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`


## <a name="deprecated-features-and-operating-systems"></a><a name="bkmk_deprecated"></a> Afgeschafte functies en besturings systemen

Meer informatie over ondersteunings wijzigingen voordat ze worden geïmplementeerd in [verwijderde en afgeschafte items](deprecated/removed-and-deprecated.md).

- De implementatie voor het delen van inhoud van Azure is gewijzigd. Gebruik een Cloud beheer gateway die is ingeschakeld voor inhoud door de optie in te scha kelen om **CMG te laten functioneren als een Cloud distributiepunt en inhoud te bezorgen bij Azure Storage**. U kunt in de toekomst geen traditioneel Cloud distributiepunt maken.

Versie 1902 daalt ondersteuning voor de volgende producten:  

- Linux en UNIX als een-client. De afschaffing werd aangekondigd met [versie 1802](whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support). Overweeg Microsoft Azure beheer voor het beheer van Linux-servers. Azure-oplossingen hebben uitgebreide Linux-ondersteuning die in de meeste gevallen de functionaliteit van Configuration Manager overschrijden, waaronder end-to-end patch management voor Linux.


## <a name="site-infrastructure"></a><a name="bkmk_infra"></a> Site-infra structuur

### <a name="client-health-dashboard"></a>Client status dashboard

<!--3599209-->
U implementeert software-updates en andere apps om uw omgeving te beveiligen, maar deze implementaties bereiken alleen gezonde clients. Slechte Configuration Manager-clients hebben een negatieve invloed op de algehele naleving. Het bepalen van de status van de client kan lastig zijn, afhankelijk van de noemer: hoeveel apparaten in totaal moeten worden beheerd? Als u bijvoorbeeld alle systemen van Active Directory ontdekt, zelfs als sommige van deze records voor buiten gebruik gestelde machines zijn, neemt dit proces uw noemer toe.

U kunt nu een dash board weer geven met informatie over de status van Configuration Manager-clients in uw omgeving. Bekijk de status van uw client, scenario status en veelvoorkomende fouten. Filter de weer gave op diverse kenmerken om potentiële problemen per OS en client versies te bekijken.

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** . Vouw **client status**uit en selecteer het knoop punt **client status dashboard** .

![Scherm opname van het dash board voor client status](media/3599209-client-health-dashboard.png)

Zie [clients controleren](../../clients/manage/monitor-clients.md#bkmk_health)voor meer informatie.

### <a name="new-management-insight-rules"></a>Nieuwe management Insight-regels

De functie Management Insights heeft de volgende nieuwe regels:

- Meerdere regels met aanbevelingen voor het beheren van verzamelingen. Gebruik deze inzichten om het beheer te vereenvoudigen en de prestaties te verbeteren. Bekijk deze nieuwe regels in de groep **verzamelingen** .<!--3555752-->  

- **Clients bijwerken naar een ondersteunde versie regel van Windows 10** in de **vereenvoudigde beheer** groep. Deze regel rapporteert op clients met een versie van Windows 10 die niet meer wordt ondersteund. Het bevat ook clients met een Windows 10-versie die bijna op het einde van de service (drie maanden) ligt.<!--3897268-->  

Zie [Management Insights](../../servers/manage/management-insights.md)voor meer informatie.

### <a name="improvement-to-enhanced-http"></a>Verbetering van verbeterde HTTP

<!--3798957-->

U kunt nu verbeterde HTTP inschakelen per primaire site of voor de centrale beheer site.

Selecteer op de eigenschappen van de centrale beheer site de optie voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen**. Deze instelling geldt alleen voor site systeem rollen op de centrale beheer site. Het is geen globale instelling voor de hiërarchie.

Zie [Enhanced http](../hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie.

### <a name="improvement-to-setup-prerequisites"></a>Verbetering van de vereisten voor installatie

Wanneer u installeert of bijwerkt naar versie 1902, bevat Configuration Manager Setup nu de volgende controle van vereisten:

- **Opnieuw opstarten van systeem in behandeling op de externe SQL Server**: deze controle op vereisten is vergelijkbaar met de regel voor het **opnieuw opstarten** van het systeem, maar controleert een externe SQL Server. Zie [lijst met vereisten controles](../../servers/deploy/install/list-of-prerequisite-checks.md#pending-system-restart-on-the-remote-sql-server)voor meer informatie. <!--SCCMDocs-pr issue 3377-->  


## <a name="cloud-attached-management"></a><a name="bkmk_cloud"></a> Cloud-gekoppeld beheer

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Cloud service stoppen als deze de drempel waarde overschrijdt

<!--3735092-->
Configuration Manager kunt nu een CMG-service (Cloud Management Gateway) stoppen als de totale gegevens overdracht meer dan uw limiet overschrijdt. De CMG heeft altijd waarschuwingen over het activeren van meldingen wanneer het gebruik van de waarschuwing of kritiek niveau is bereikt. Om onverwachte Azure-kosten te verminderen vanwege een piek in het gebruik, wordt met deze nieuwe optie de Cloud service uitgeschakeld.

Zie [Stop CMG als de drempel waarde wordt overschreden](../../clients/manage/cmg/monitor-clients-cloud-management-gateway.md#bkmk_stop)voor meer informatie.

### <a name="use-azure-resource-manager-for-cloud-services"></a>Azure Resource Manager gebruiken voor Cloud Services

<!--3605704-->
Vanaf versie 1810 is de klassieke service-implementatie in azure afgeschaft voor gebruik in Configuration Manager. Deze versie is de laatste ter ondersteuning van het maken van deze Azure-implementaties.

Bestaande implementaties blijven werken. Met ingang van deze huidige branch-versie is Azure Resource Manager het enige implementatie mechanisme voor nieuwe exemplaren van de Cloud beheer gateway en het Cloud distributiepunt.

Zie [Azure Resource Manager voor de Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager)voor meer informatie.

### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Cloud beheer gateway toevoegen aan grens groepen

<!--3640932-->
U kunt nu een CMG (Cloud Management Gateway) koppelen aan een grens groep. Met deze configuratie kunnen clients standaard of terugvallen op de CMG voor client communicatie, afhankelijk van de relaties tussen grens groepen. Dit gedrag is vooral nuttig in Branch-Office en VPN-scenario's. U kunt client verkeer door sturen naar dure en trage WAN-koppelingen om in plaats daarvan sneller Internet koppelingen naar Microsoft Azure te gebruiken.

Zie [CMG Hierarchy design](../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design) (Engelstalig) en [Stel CMG](../../clients/manage/cmg/setup-cloud-management-gateway.md#configure-boundary-groups)in voor meer informatie.


## <a name="real-time-management"></a><a name="bkmk_real"></a> Real-time beheer

### <a name="run-cmpivot-from-the-central-administration-site"></a>CMPivot uitvoeren vanaf de centrale beheer site

<!--3610960-->
Configuration Manager ondersteunt nu het uitvoeren van CMPivot vanaf de centrale beheer site in een hiërarchie. De primaire site verwerkt nog steeds de communicatie met de client. Wanneer CMPivot vanaf de centrale beheer site wordt uitgevoerd, communiceert deze met de primaire site via het kanaal voor het abonnement op hoge snelheid van berichten. Deze communicatie vertrouwt niet op de standaard SQL-replicatie tussen sites.

Zie [CMPivot voor realtime gegevens](../../servers/manage/cmpivot-changes.md#bkmk_cmpivot1902)voor meer informatie.

### <a name="edit-or-copy-powershell-scripts"></a>Power shell-scripts bewerken of kopiëren

<!--3705507-->
U kunt nu een bestaand Power shell-script **bewerken** of **kopiëren** dat wordt gebruikt met de functie scripts uitvoeren. In plaats van een script opnieuw te maken dat u moet wijzigen, kunt u dit nu rechtstreeks bewerken. Beide acties gebruiken dezelfde wizard-ervaring als wanneer u een nieuw script maakt. Wanneer u een script bewerkt of kopieert, wordt Configuration Manager de goedkeurings status niet behouden.

Zie [scripts uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md#bkmk_psedit)voor meer informatie.


## <a name="content-management"></a><a name="bkmk_content"></a> Inhouds beheer

### <a name="distribution-point-maintenance-mode"></a>Onderhouds modus van distributie punt

<!--3555754-->

U kunt nu een distributie punt instellen in de onderhouds modus. Schakel de onderhouds modus in wanneer u software-updates installeert of wijzigingen aanbrengt aan de server.

Terwijl het distributie punt zich in de onderhouds modus bevindt, heeft het het volgende gedrag:

- Er wordt geen inhoud naar de site gedistribueerd.  

- Beheer punten retour neren niet de locatie van dit distributie punt naar clients.

- Wanneer u de site bijwerkt, wordt er nog een distributie punt in de onderhouds modus bijgewerkt.

- De eigenschappen van het distributie punt zijn alleen-lezen. Het is bijvoorbeeld niet mogelijk om het certificaat te wijzigen of grens groepen toe te voegen.  

- Alle geplande taken, zoals inhouds validatie, worden nog steeds uitgevoerd volgens hetzelfde schema.

Zie [onderhouds modus](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_maint)voor meer informatie over deze functie.

Zie [methode SetDPMaintenanceMode in klasse SMS_DistributionPointInfo](../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md)voor meer informatie over het automatiseren van dit proces met de SDK van Configuration Manager.


## <a name="client-management"></a><a name="bkmk_client"></a> Client beheer

### <a name="client-provisioning-mode-timeout"></a>Time-out voor client inrichtings modus

<!--3197824-->
De taken reeks stelt een tijds tempel in wanneer de client in de inrichtings modus wordt geplaatst. Een client in de inrichtings modus controleert elke 60 minuten de tijds duur sinds de tijds tempel. Als de inrichtings modus langer is dan 48 uur, wordt de inrichtings modus door de client automatisch afgesloten en wordt het proces opnieuw gestart.

Zie [inrichtings modus](../../../osd/understand/provisioning-mode.md)voor meer informatie.

### <a name="view-first-screen-only-during-remote-control"></a>Eerste scherm alleen weer geven tijdens beheer op afstand

<!--3231732-->
Wanneer u verbinding maakt met een client met twee of meer monitors, kan het lastig zijn deze allemaal weer te geven in de Configuration Manager viewer voor beheer op afstand. Een operator voor externe hulpprogram ma's kan nu kiezen tussen het weer geven van **alle schermen** of het **eerste scherm** .

Zie [een Windows-client computer op afstand beheren](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)voor meer informatie.

### <a name="specify-a-custom-port-for-peer-wakeup"></a>Geef een aangepaste poort op voor het opstarten van de peer

<!--3605925-->
U kunt nu een aangepast poort nummer opgeven voor wake-up proxy. Configureer in client instellingen in de groep **energie beheer** de instelling voor **Wake on LAN poort nummer (UDP)**.  

Zie [Wake on LAN configureren](../../clients/deploy/configure-wake-on-lan.md)voor meer informatie.


## <a name="application-management"></a><a name="bkmk_app"></a> Toepassings beheer

### <a name="improvements-to-application-approvals-via-email"></a>Verbeteringen in het goed keuren van toepassingen via e-mail

<!--3594063-->
Deze versie heeft verbeteringen in de functie voor het ontvangen van e-mail meldingen voor toepassings aanvragen. Gebruikers kunnen altijd een opmerking toevoegen aan de aanvraag vanuit software Center. Deze opmerking wordt weer gegeven in de toepassings aanvraag in de Configuration Manager-console. Nu wordt de opmerking ook in het e-mail bericht weer gegeven. Met deze opmerking in het e-mail bericht kunnen goed keurders een betere beslissing nemen om de aanvraag goed te keuren of te weigeren.

Zie [e-mail meldingen](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)voor meer informatie.

### <a name="improvements-to-package-conversion-manager"></a>Verbeteringen in pakket conversie beheer

<!-- SCCMDocs-pr issue #3357 -->
Deze versie bevat de volgende verbeteringen voor [package Conversion Manager](../../../apps/pcm/package-conversion-manager.md):

- Geplande pakket analyse wordt standaard elke 7 dagen uitgevoerd
- Power shell-cmdlets voor het analyseren en converteren van pakketten
- Algemene oplossingen voor fouten en verbeteringen


## <a name="os-deployment"></a><a name="bkmk_osd"></a> Implementatie van besturings systeem

### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Voortgangs status tijdens in-place upgrade taken reeks

<!--3747129-->
Er wordt nu een gedetailleerde voortgangs balk weer geven tijdens een Windows 10-in-place upgrade taken reeks. Deze balk toont de voortgang van de installatie van Windows, die op een andere manier tijdens de taken reeks op de achtergrond wordt uitgevoerd. Gebruikers hebben nu inzicht in de onderliggende voortgang. Het helpt om te zorgen dat het upgrade proces wordt onderbroken vanwege een gebrek aan voortgangs indicatie.  

![Voor beeld van voortgang van taken reeks met voortgang van Windows-upgrade](media/3747129-installation-progress.png)

Deze functie werkt met alle ondersteunde versies van Windows 10 en alleen met de taken reeks in-place upgrade.

### <a name="improvements-to-task-sequence-media-creation"></a>Verbeteringen in het maken van taken reeks media

<!--3556027, fka 1359388-->
Deze versie bevat verschillende verbeteringen voor het verbeteren van het maken en beheren van taken reeks media. Voor meer informatie raadpleegt u de volgende artikelen voor specifieke media typen:

- [Zelfstandige media maken](../../../osd/deploy-use/create-stand-alone-media.md)
- [Voorbereide media maken](../../../osd/deploy-use/create-prestaged-media.md)
- [Opstartbare media maken](../../../osd/deploy-use/create-bootable-media.md)
- [Vastelegmedia maken](../../../osd/deploy-use/create-capture-media.md)

#### <a name="specify-temporary-storage"></a>Tijdelijke opslag opgeven

Wanneer u taken reeks media maakt, past u nu de locatie aan die de site gebruikt voor tijdelijke opslag van gegevens. Dit proces kan veel tijdelijke schijf ruimte vergen. Met deze wijziging hebt u meer flexibiliteit om te kiezen waar deze tijdelijke bestanden moeten worden opgeslagen.

Geef in de **wizard taken reeks media maken**een locatie op voor de **map voor gefaseerde installatie**. Deze locatie is standaard vergelijkbaar met het volgende pad: `%UserProfile%\AppData\Local\Temp` .

#### <a name="add-a-label-to-the-media"></a>Een label toevoegen aan de media

U kunt nu een label toevoegen aan taken reeks media. Dit label helpt u de media beter te identificeren nadat u deze hebt gemaakt. Geef in de **wizard taken reeks media maken**een **medium label**op.

### <a name="import-a-single-index-of-an-os-image"></a>Eén index van een installatie kopie van het besturings systeem importeren

<!--3719699-->
Wanneer u een Windows-installatie kopie bestand (WIM) importeert naar Configuration Manager, kunt u nu een enkelvoudige index importeren in plaats van alle afbeeldings indexen in het bestand. Deze optie biedt de volgende voor delen:

- Kleiner afbeeldings bestand  
- Snellere offline onderhoud  
- Installatie kopie-onderhoud optimaliseren voor een kleiner afbeeldings bestand na offline onderhoud

Wanneer u een installatie kopie van een besturings systeem importeert, selecteert u de optie voor het **extra heren van een specifieke installatie kopie-index uit het opgegeven Wim-bestand**. Selecteer vervolgens de afbeeldings index in de lijst.  

Zie [een installatie kopie van een besturings systeem toevoegen](../../../osd/get-started/manage-operating-system-images.md#BKMK_AddOSImages)voor meer informatie.

### <a name="optimized-image-servicing"></a>Geoptimaliseerde installatie kopie onderhoud

<!--3555951-->
Wanneer u software-updates toepast op een installatie kopie van een besturings systeem, is er een nieuwe optie voor het optimaliseren van de uitvoer door vervangen updates te verwijderen. De optimalisatie van offline onderhoud is alleen van toepassing op installatie kopieën met één index.

Wanneer u een planning maakt voor het bijwerken van een installatie kopie van een besturings systeem, selecteert u de optie om **vervangen updates te verwijderen nadat de installatie kopie is bijgewerkt**.

Zie [software-updates Toep assen op een installatie kopie](../../../osd/get-started/manage-operating-system-images.md#bkmk_resetbase)voor meer informatie.

### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Verbeteringen voor het uitvoeren van de taken reeks stap Power shell-script

<!--3556028, fka 1359389-->
De taken reeks stap **Power shell-script uitvoeren** bevat nu de volgende verbeteringen:  

- U kunt nu direct Windows Power shell-code invoeren in deze stap. Met deze wijziging kunt u Power shell-opdrachten uitvoeren tijdens een taken reeks zonder eerst een pakket te maken en te distribueren met het script.

- Wanneer u de optie **een Power shell-script opgeven** kiest, selecteert u **script bewerken**. Het nieuwe Power shell-script venster bevat de volgende acties:  

    - Het script rechtstreeks bewerken  

    - Een bestaand script openen vanuit een bestand  

    - Naar een bestaand goedgekeurd script in Configuration Manager bladeren

- De script uitvoer opslaan naar een aangepaste taken reeks variabele  

- Als u de script parameters in het taken reeks logboek wilt toevoegen, stelt u de taken reeks variabele **OSDLogPowerShellParameters** in op **waar**. De para meters worden standaard niet in het logboek geregistreerd.  

- Andere verbeteringen die vergelijk bare functionaliteit bieden als de stap [opdracht regel uitvoeren](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) . Geef bijvoorbeeld alternatieve gebruikers referenties op of geef een time-out op.

> [!Important]  
> Als u deze nieuwe functie Configuration Manager wilt gebruiken, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

Zie [Power shell-script uitvoeren](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript)voor meer informatie.

### <a name="other-improvements-to-os-deployment"></a>Andere verbeteringen voor de implementatie van besturings systemen

<!--3633146,3641475,3654172,3734270-->
Deze versie bevat de volgende verbeteringen voor de implementatie van besturings systemen:

- Er is een nieuwe standaard actie voor de **weer gave** van taken reeksen. <!--3633146-->  

- In het dialoog venster fout in taken reeks wordt nu meer informatie weer gegeven. Hier wordt de naam weer gegeven van de taken reeks stap die is mislukt. <!--3641475-->  

- Wanneer u de taken reeks variabele **OSDDoNotLogCommand** instelt op True, wordt de opdracht regel ook verborgen met de stap opdracht regel uitvoeren in het logboek bestand. Voorheen werd alleen de programma naam gemaskeerd uit de stap pakket installeren in bestand smsts. log.<!--3654172-->  

- Wanneer u een PXE-responder inschakelt op een distributie punt zonder Windows Deployment-service, kan dit nu zich op dezelfde server bevinden als de DHCP-service. <!--3734270--> Zie [Configure ten minste één distributie punt voor het accepteren van PXE-aanvragen](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md#BKMK_Configure)voor meer informatie.


## <a name="software-center"></a><a name="bkmk_userxp"></a> Software Center

### <a name="replace-toast-notifications-with-dialog-window"></a>Pop-upmeldingen vervangen door dialoog venster

<!--3555947-->
Soms zien gebruikers de Windows-pop-upmelding over het opnieuw opstarten of de vereiste implementatie niet. De ervaring wordt dan niet weer geven om de herinnering af te stellen. Dit gedrag kan leiden tot een slechte gebruikers ervaring wanneer de client een deadline bereikt.

Wanneer implementaties nu opnieuw moeten worden opgestart of als er software wijzigingen nodig zijn, hebt u de mogelijkheid om een meer opvallend dialoog venster te gebruiken.

Zie [plan for Software Center](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact) (Engelstalig) voor meer informatie.

### <a name="configure-user-device-affinity-in-software-center"></a>Affiniteit tussen gebruikers en apparaten configureren in Software Center

<!--3485366-->
Met het verbeteren van de [infra structuur van software Center](whats-new-in-version-1806.md#software-center-infrastructure-improvements) vanaf versie 1806 zijn de site Server functies van de Application Catalog niet meer vereist voor de meeste scenario's. Sommige klanten zijn nog steeds afhankelijk van de toepassings catalogus om gebruikers toe te staan hun primaire apparaat in te stellen voor affiniteit tussen gebruikers en apparaten.

Gebruikers kunnen nu hun primaire apparaat instellen in Software Center. Met deze actie wordt de primaire gebruiker van het apparaat in Configuration Manager.

Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.

### <a name="configure-default-views-in-software-center"></a>Standaard weergaven in Software Center configureren

<!--3612112-->
Deze versie van Configuration Manager wordt verder herhaald over hoe u Software Center kunt aanpassen:

- De standaard indeling van toepassingen instellen, ofwel tegels of een lijst  

    - Als een gebruiker deze configuratie wijzigt, wordt de voor keur van de gebruiker in de toekomst persistent gemaakt door Software Center  

- Het standaard toepassings filter configureren, ofwel alle of alleen vereiste apps  

    - Software Center gebruikt altijd de standaard instelling. Gebruikers kunnen dit filter wijzigen, maar Software Center blijft de voor keur niet behouden.

Geef deze instellingen op in de **Software Center** -groep van client instellingen.

Zie [over client instellingen](../../clients/deploy/about-client-settings.md#bkmk_swctr_defaults)voor meer informatie.


## <a name="software-updates"></a><a name="bkmk_sum"></a> Software-updates

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Prioriteit voor functie-updates opgeven in Windows 10 Servicing

<!--3734525-->
Pas de prioriteit aan waarmee clients een onderdeel Update installeren via [Windows 10 Servicing](../../../osd/deploy-use/manage-windows-as-a-service.md). Standaard installeren clients nu onderdelen updates met een hogere verwerkings prioriteit.

Gebruik client instellingen om deze optie te configureren. Configureer in de groep **software-updates** de volgende instelling: **Geef de thread prioriteit op voor functie-updates**.

Zie [over client instellingen](../../clients/deploy/about-client-settings.md#software-updates)voor meer informatie.


## <a name="office-management"></a><a name="bkmk_o365"></a> Office-beheer

### <a name="redirect-windows-known-folders-to-onedrive"></a>Windows-bekende mappen omleiden naar OneDrive

<!--3556021-->
Gebruik Configuration Manager om bekende mappen van Windows te verplaatsen naar OneDrive voor bedrijven. Deze mappen omvatten bureau blad, documenten en afbeeldingen. Als u uw Windows 10-upgrades wilt vereenvoudigen, implementeert u deze instellingen voor Windows 7-clients voordat u een taken reeks implementeert.

Zie [Windows bekende mappen omleiden en verplaatsen naar OneDrive](/onedrive/redirect-known-folders)voor meer informatie over deze functie van OneDrive voor bedrijven.

Zoek eerst [de Tenant-id van Microsoft 365](/onedrive/find-your-office-365-tenant-id). Implementeer vervolgens de OneDrive Sync Client versie 18.111.0603.0004 of hoger. Zie voor meer informatie [OneDrive-Apps implementeren met behulp van Configuration Manager](/onedrive/deploy-on-windows).  

Als u een OneDrive voor bedrijven-profiel wilt maken en implementeren, gaat u in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Vouw **instellingen voor naleving**uit en selecteer het knoop punt **voor OneDrive voor bedrijven-profielen** .  

Zie de sectie Windows bekende mappen omleiden naar OneDrive in het artikel in de [OneDrive voor bedrijven-profielen](../../../compliance/deploy-use/onedrive-profile.md) voor meer informatie.

### <a name="integration-for-microsoft-365-apps-for-enterprise-readiness"></a>Integratie voor Microsoft 365 apps voor de gereedheid van het bedrijf

<!--3735402-->
Gebruik Configuration Manager om apparaten met hoge betrouw baarheid te identificeren die gereed zijn om te upgraden naar Microsoft 365 apps voor bedrijven. De integratie biedt inzicht in mogelijke compatibiliteits problemen met Office-invoeg toepassingen en macro's die in uw omgeving worden gebruikt. Gebruik vervolgens Configuration Manager om Office te implementeren op apparaten die klaar zijn voor gebruik.

Het bestaande Microsoft 365-client beheer Dashboard bevat nu een nieuwe tegel, **Office 365 ProPlus Upgradegereedheid**.

Zie [Microsoft 365 dash board voor client beheer](../../../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) voor meer informatie.

### <a name="additional-languages-for-microsoft-365-updates"></a>Aanvullende talen voor Microsoft 365 updates

<!--3555955-->
Configuration Manager ondersteunt nu alle ondersteunde talen voor Microsoft 365-client updates. De werk stroom voor updates scheidt nu de 38 talen voor **Windows Update** van de talloze talen voor **Office 365 client update**.

Zie [Manage Microsoft 365 updates](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_o365_lang) (Engelstalig) voor meer informatie

### <a name="office-products-on-lifecycle-dashboard"></a>Dash board Office-producten op levens cyclus

<!--3556026-->
Het dash board voor product levenscyclus bevat nu informatie over geïnstalleerde versies van Office 2003 tot en met Office 2016. De gegevens worden weer gegeven nadat de taak levenscyclus overzicht op de site wordt uitgevoerd. Dit is elke 24 uur.

Zie [het dash board product levenscyclus gebruiken](../../clients/manage/asset-intelligence/product-lifecycle-dashboard.md)voor meer informatie.


## <a name="phased-deployments"></a><a name="bkmk_pod"></a> Gefaseerde implementaties

### <a name="dedicated-monitoring-for-phased-deployments"></a>Specifieke bewaking voor gefaseerde implementaties

<!--3555949-->
Gefaseerde implementaties hebben nu hun eigen specifieke bewakings knooppunt. Dit knoop punt maakt het gemakkelijker om gefaseerde implementaties te identificeren die u hebt gemaakt en vervolgens naar de bewakings weergave met gefaseerde implementatie te gaan. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer het knoop punt **gefaseerde implementaties** . De lijst met gefaseerde implementaties wordt weer gegeven.

Zie de [weer gave van de gefaseerde implementatie bewaking](../../../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_monitor)voor meer informatie.

### <a name="improvement-to-phased-deployment-success-criteria"></a>Verbetering van geslaagde criteria voor implementatie

<!--3555946-->
Aanvullende criteria opgeven voor het slagen van een fase in een gefaseerde implementatie. In plaats van alleen een percentage kunnen deze criteria nu ook het aantal apparaten zijn dat is geïmplementeerd. Deze optie is handig als de grootte van de verzameling variabel is en u een specifiek aantal apparaten hebt om het succes weer te geven voordat u verdergaat met de volgende fase.

Een gefaseerde implementatie voor een taken reeks, software-update of toepassing maken. Selecteer vervolgens op de pagina instellingen van de wizard de volgende optie als de criteria voor het slagen van de eerste fase: het **aantal apparaten dat is geïmplementeerd**.

Zie voor meer informatie [gefaseerde implementaties maken](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md).


## <a name="configuration-manager-console"></a><a name="bkmk_admin"></a> Configuration Manager-console

### <a name="improvements-to-configuration-manager-console"></a><a name="bkmk_console"></a> Verbeteringen aan Configuration Manager-console

<!--3594151-->
Op basis van feedback van klanten op het gebied van de-versie 2018 van de Midwest Management Summit (MMS), bevat de volgende verbeteringen voor de Configuration Manager-console:

- Maximaliseer het Blader register venster voor toepassings detectie methoden
- Ga naar de verzameling vanuit een toepassings implementatie
- Inhoud verwijderen uit bewakings status
- Weer gaven worden gesorteerd op gehele waarden in het knoop punt **implementaties** van de werk ruimte **bewaking**
- De waarschuwing voor een groot aantal resultaten verplaatsen

Zie [Configuration Manager-console tips](../../servers/manage/admin-console-tips.md)voor meer informatie.

### <a name="configuration-manager-console-notifications"></a>Meldingen over Configuration Manager-console

<!--3556016, fka 1318035-->
Om u beter op de hoogte te houden, zodat u de juiste actie kunt ondernemen, wordt de Configuration Manager-console nu op de hoogte gesteld van de volgende gebeurtenissen:

- Wanneer er een update beschikbaar is voor Configuration Manager zichzelf
- Wanneer er levens cyclus-en onderhouds gebeurtenissen optreden in de omgeving

Deze melding is een balk boven aan het console venster onder het lint. De vorige ervaring wordt vervangen wanneer Configuration Manager updates beschikbaar zijn. In deze meldingen in de console worden nog steeds essentiële gegevens weer gegeven, maar uw werk in de console wordt niet verstoord. U kunt geen kritieke meldingen negeren. In de-console worden alle meldingen in een nieuw systeemvak van de titel balk weer gegeven.

Zie [Configuration Manager-console meldingen](../../servers/manage/admin-console-notifications.md)voor meer informatie.

### <a name="confirmation-of-console-feedback"></a>Bevestiging van console feedback

<!--3556010-->
Wanneer u [feedback](../../understand/find-help.md#product-feedback) verzendt in de Configuration Manager-console, wordt er nu een bevestigings bericht weer gegeven. Dit bericht bevat een **feedback-id**, die u aan micro soft kunt geven als tracking-ID.

Zie [product feedback](../../understand/find-help.md#bkmk_feedbackid)voor meer informatie.

### <a name="view-recently-connected-consoles"></a>Recent verbonden consoles weer geven

<!--3699367-->
U kunt nu de meest recente verbindingen voor de Configuration Manager-console weer geven. De weer gave bevat actieve verbindingen en de consoles die recent zijn verbonden. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **beveiliging**uit en selecteer het knoop punt **console verbindingen** .

Zie [de Configuration Manager-console gebruiken](../../servers/manage/admin-console.md#bkmk_viewconnected)voor meer informatie.

### <a name="in-console-documentation-dashboard"></a>Dash board documentatie in de console

<!--3556019, fka 1357546-->
Er is een nieuw **documentatie** knooppunt in de nieuwe werk ruimte van de **Community** . Dit knoop punt bevat actuele informatie over Configuration Manager documentatie en ondersteunings artikelen.

Zie [de Configuration Manager-console gebruiken](../../servers/manage/admin-console.md#bkmk_doc-dashboard)voor meer informatie.

### <a name="search-device-views-using-mac-address"></a>Apparaatbeheer doorzoeken met MAC-adres

<!--3600878-->
U kunt nu zoeken naar een MAC-adres in een apparaat weergave van de Configuration Manager-console. Deze eigenschap is handig voor beheerders van besturingssysteem implementaties bij het oplossen van problemen met PXE-implementaties. Wanneer u een lijst met apparaten bekijkt, voegt u de kolom **MAC-adres** toe aan de weer gave. Gebruik het zoek veld om de **MAC-adres** zoek criteria toe te voegen.

Zie [Configuration Manager-console tips](../../servers/manage/admin-console-tips.md)voor meer informatie.

### <a name="use-net-47-for-improved-console-accessibility"></a>.NET 4,7 gebruiken voor verbeterde console toegankelijkheid

<!-- SCCMDocs-pr issue #3228 -->
Als u de toegankelijkheids functies van de Configuration Manager-console wilt verbeteren, werkt u .NET bij naar versie 4,7 of hoger op de computer waarop de-console wordt uitgevoerd.

Zie [toegankelijkheids functies in Configuration Manager](../../understand/accessibility-features.md)voor meer informatie.

### <a name="changes-to-console-setup-process"></a>Wijzigingen in het installatie proces van de console

<!-- 3612513 -->
Er zijn nieuwe onderdelen vereist bij het installeren van de Configuration Manager-console. Als u een pakket maakt voor het installeren van de-console op andere computers, moet u ervoor zorgen dat het pakket de volgende bestanden bevat:

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

Wanneer u een site server installeert of bijwerkt, worden deze installatie bestanden en ondersteunde taal pakketten voor de site naar de submap **Tools\ConsoleSetup** gekopieerd. Zie [de Configuration Manager-console installeren](../../servers/deploy/install/install-consoles.md)voor meer informatie.


## <a name="other-updates"></a>Andere Updates

Afgezien van nieuwe functies bevat deze release ook aanvullende wijzigingen, zoals oplossingen voor problemen. Zie [overzicht van wijzigingen in Configuration Manager current branch, versie 1902](https://support.microsoft.com/help/4498910)voor meer informatie.

Zie [release opmerkingen voor Power shell versie 1902](/powershell/sccm/1902-release-notes)voor meer informatie over wijzigingen in de Windows Power shell-cmdlets voor Configuration Manager.

Het volgende update pakket (4500571) is beschikbaar in de-console vanaf 17 juni 2019: [Update pakket voor Configuration Manager current branch, versie 1902](https://support.microsoft.com/help/4500571).

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

Wanneer u klaar bent om deze versie te installeren, raadpleegt u [updates voor Configuration Manager](../../servers/manage/updates.md) en [controle lijst voor het installeren van update 1902](../../servers/manage/checklist-for-installing-update-1902.md).

> [!TIP]  
> Als u een nieuwe site wilt installeren, gebruikt u een basislijn versie van Configuration Manager.  
>
> Meer informatie over:    
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)  

Zie de [release opmerkingen](../../servers/deploy/install/release-notes.md)voor bekende, belang rijke problemen.

Nadat u een site hebt bijgewerkt, raadpleegt u ook de [controle lijst na de update](../../servers/manage/checklist-for-installing-update-1902.md#post-update-checklist).