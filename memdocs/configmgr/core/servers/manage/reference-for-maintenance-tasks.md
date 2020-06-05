---
title: Naslaginformatie voor onderhoudstaken
titleSuffix: Configuration Manager
description: Details voor elk van de Configuration Manager site-onderhouds taken
ms.date: 06/04/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e989de5acab778374c233862d0ab4d7077899d28
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428587"
---
# <a name="reference-for-maintenance-tasks-in-configuration-manager"></a>Verwijzing voor onderhouds taken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u de Details voor elk van de Configuration Manager site-onderhouds taken. Elk item bevat de site typen waar de taak beschikbaar is en of deze standaard is ingeschakeld.

Zie [onderhouds taken instellen](maintenance-tasks.md#set-up-maintenance-tasks)voor meer informatie.  

## <a name="tasks"></a>Taken

### <a name="backup-site-server"></a>Back-upserver van site

Gebruik deze taak om een back-up te maken van uw essentiële informatie om een site en de Configuration Manager Data Base te herstellen. Zie [een back-up maken van een Configuration Manager-site](backup-and-recovery.md)voor meer informatie.  

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Niet ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="check-application-title-with-inventory-information"></a>Titel van toepassing controleren met inventaris informatie

Gebruik deze taak om de consistentie van software titels tussen de software-inventaris en de Asset Intelligence catalogus te behouden. Zie [Inleiding tot Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)voor meer informatie.  

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|Primaire site|Niet beschikbaar|
|Secundaire site|Niet beschikbaar|

### <a name="clear-undiscovered-clients"></a>Niet-gedetecteerde clients wissen

> [!Tip]
> Deze taak wordt mogelijk ook weer geven in de console met de naam **duidelijke installatie vlag**.

Gebruik deze taak om de geïnstalleerde vlag te verwijderen voor clients die geen heartbeat-detectie record verzenden tijdens de **herdetectie** periode van de client. De geïnstalleerde vlag voor komt automatische Push-client installatie naar een computer die mogelijk een actieve Configuration Manager-client heeft.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Niet ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-application-request-data"></a>Verouderde gegevens van toepassings aanvraag verwijderen

Gebruik deze taak om verouderde toepassings aanvragen uit de data base te verwijderen. Zie [een toepassing maken en implementeren](../../../apps/get-started/create-and-deploy-an-application.md)voor meer informatie.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-application-revisions"></a>Verouderde toepassings revisies verwijderen

Gebruik deze taak om toepassings revisies te verwijderen waarnaar niet meer wordt verwezen. Zie [toepassingen herzien en vervangen](../../../apps/deploy-use/revise-and-supersede-applications.md)voor meer informatie.

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-client-download-history"></a>Verouderde geschiedenis van client downloaden verwijderen

Gebruik deze taak om historische gegevens over de Download bron die door clients worden gebruikt, te verwijderen. De site gebruikt Download Bron gegevens om het [dash board client gegevens bronnen](../deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)in te vullen.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-client-operations"></a>Verouderde clientbewerkingen verwijderen

Gebruik deze taak om alle verouderde gegevens voor client bewerkingen uit de site database te verwijderen. Deze gegevens omvatten bijvoorbeeld de volgende bewerkingen:

- Verouderde of verlopen client meldingen, zoals Download aanvragen voor computer-of gebruikers beleid
- Endpoint Protection, zoals aanvragen van een gebruiker met beheerders rechten voor clients om een scan uit te voeren of bijgewerkte definities te downloaden
- Resultaten van de uitvoering van scripts

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-client-presence-history"></a>Verouderde geschiedenis van client aanwezigheid verwijderen
<!-- not listed in dogfood for either primary or CAS, was it renamed? -->
Gebruik deze taak om geschiedenis informatie over de online status van clients die zijn vastgelegd door client meldingen te verwijderen. Hiermee verwijdert u informatie voor clients met een status die ouder is dan de opgegeven tijd. Zie [clients controleren](../../clients/manage/monitor-clients.md)voor meer informatie.

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-cloud-management-gateway-traffic-data"></a>Verouderde gegevens van cloudbeheergateway verkeer verwijderen

Gebruik deze taak om alle verouderde gegevens over het verkeer dat door de [Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)wordt door gegeven, uit de site database te verwijderen. Deze gegevens omvatten:

- Het aantal aanvragen
- Totaal aantal aanvraag bytes
- Totaal aantal antwoord bytes
- Aantal mislukte aanvragen
- Maximum aantal gelijktijdige aanvragen

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-cmpivot-results"></a>Verouderde CMPivot-resultaten verwijderen

Gebruik deze taak om verouderde informatie van de site database te verwijderen van clients in CMPivot-query's. Zie [CMPivot voor realtime gegevens](cmpivot.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-collected-files"></a>Verouderde verzamelde bestanden verwijderen

Gebruik deze taak om de verouderde informatie over verzamelde bestanden uit de data base te verwijderen. Deze taak verwijdert tevens de verzamelde bestanden uit de siteservermapstructuur op de geselecteerde site. De vijf meest recente kopieën van verzamelde bestanden worden standaard opgeslagen op de site server in de **map inboxes\sinv.box\filecol** -map. Zie [Inleiding tot software-inventarisatie](../../clients/manage/inventory/introduction-to-software-inventory.md)voor meer informatie.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-computer-association-data"></a>Verouderde gegevens van computer koppeling verwijderen

Gebruik deze taak om de verouderde gegevens van de besturingssysteem implementatie computer koppeling te verwijderen uit de data base. Deze informatie wordt gebruikt bij het herstellen van de gebruikers status tijdens een taken reeks. Zie [gebruikers status beheren](../../../osd/get-started/manage-user-state.md)voor meer informatie.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-console-connection-data"></a>Verouderde console verbindings gegevens verwijderen

Met deze taak worden gegevens uit de site database verwijderd over console verbindingen met de site.<!-- SCCMDocs#528 -->

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-delete-detection-data"></a>Verouderde detectie gegevens verwijderen

Gebruik deze taak om verouderde gegevens uit de data base te verwijderen die door extractie weergaven zijn gemaakt. Hiermee wordt oude gegevens wijzigings informatie verwijderd die wordt gebruikt door externe systemen die gegevens uit de data base ophalen.<!--SCCMDocs#1590--><!--By default, Extraction Views are disabled. You only enable them by using the Configuration Manager SDK. Unless Extraction Views are enabled, there is no data for this task to delete.-->

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-device-wipe-record"></a>Verouderd record van apparaat wissen verwijderen

Gebruik deze taak om te verwijderen uit de data base verouderde gegevens over acties voor wissen van mobiele apparaten. Zie [gegevens beveiligen met wissen op afstand, vergren delen of wachtwoord code opnieuw instellen](../../../mdm/deploy-use/wipe-lock-reset-devices.md)voor meer informatie.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-discovery-data"></a>Verouderde detectiegegevens verwijderen

Gebruik deze taak om verouderde detectie gegevens uit de data base te verwijderen. Deze gegevens kunnen records bevatten van:

- Heartbeat-detectie
- Netwerkdetectie
- Detectie methoden Active Directory: systeem, gebruiker en groep

Met deze taak worden ook verouderde apparaten die zijn gemarkeerd als uit bedrijf genomen, verwijderd. Gegevens die zijn gekoppeld aan een site worden verwijderd wanneer deze taak wordt uitgevoerd op die site, en deze wijzigingen worden gerepliceerd naar andere sites. Zie [detectie uitvoeren](../deploy/configure/run-discovery.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-distribution-point-usage-stats"></a>Verouderde statistieken over gebruik van distributie punten verwijderen

Met deze taak kunt u verouderde gegevens uit de data base verwijderen voor distributie punten die langer dan een opgegeven periode zijn opgeslagen.  

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-enrolled-devices"></a>Verouderde geregistreerde apparaten verwijderen

Gebruik deze taak om de verouderde gegevens over mobiele apparaten te verwijderen uit de site database die gedurende een opgegeven periode geen informatie hebben gerapporteerd aan de site.

Deze taak is van toepassing op apparaten die zijn Inge schreven bij Configuration Manager [on-premises MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md). Zie [ondersteunde besturings systemen voor clients en apparaten](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)voor meer informatie over deze apparaten.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Niet ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-ep-health-status-history-data"></a>Verouderde geschiedenis gegevens van EP-status verwijderen

Gebruik deze taak om de verouderde status informatie voor Endpoint Protection (EP) te verwijderen uit de data base. Zie [Endpoint Protection bewaken](../../../protect/deploy-use/monitor-endpoint-protection.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-exchange-partnership"></a>Verouderde Exchange-partnership verwijderen

> [!Tip]
> > Deze taak wordt mogelijk ook weer geven in de console met de naam **verouderde apparaten verwijderen die worden beheerd door de Exchange Server-connector**.

Gebruik deze taak om verouderde gegevens over mobiele apparaten te verwijderen die worden beheerd door de Exchange Server-connector. Op de site worden deze gegevens verwijderd op basis van de instelling **mobiele apparaten negeren die langer inactief zijn dan (dagen)** op het tabblad **detectie** van de eigenschappen van de Exchange Server-connector. Zie [mobiele apparaten beheren met Configuration Manager en Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-inventory-history"></a>Verouderde inventaris geschiedenis verwijderen

Gebruik deze taak om de inventaris gegevens van de data base te verwijderen die langer dan een opgegeven periode zijn opgeslagen. Zie [resource Explorer gebruiken om de hardware-inventaris te bekijken](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-log-data"></a>Verouderde logboek gegevens verwijderen

Gebruik deze taak om de verouderde logboek gegevens uit de data base te verwijderen die worden gebruikt voor het oplossen van problemen. Deze gegevens zijn niet gerelateerd aan Configuration Manager-onderdeel bewerkingen.  

> [!IMPORTANT]  
> Deze taak wordt standaard dagelijks op elke site uitgevoerd. Op een centrale beheer site en primaire sites verwijdert de taak gegevens die ouder zijn dan 30 dagen. Wanneer u SQL Server Express op een secundaire site gebruikt, moet u ervoor zorgen dat deze taak dagelijks wordt uitgevoerd en de gegevens die gedurende zeven dagen inactief zijn, worden verwijderd.  

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|**Secundaire site**|Ingeschakeld|

### <a name="delete-aged-metering-data"></a>Verouderde meet gegevens verwijderen

Met deze taak kunt u verouderde gegevens uit de data base verwijderen die langer dan een opgegeven periode zijn opgeslagen. Zie [software licentie controle](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-metering-summary-data"></a>Verouderde samenvattings gegevens van meting verwijderen

Gebruik deze taak om de verouderde samenvattings gegevens van de data base te verwijderen voor software meters die langer dan een opgegeven periode zijn opgeslagen. Zie [software licentie controle](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-notification-server-history"></a>Verouderde meldings server geschiedenis verwijderen

Met deze taak wordt de verouderde geschiedenis van client aanwezigheid verwijderd.

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-notification-task-history"></a>Verouderde meldings taken geschiedenis verwijderen

Gebruik deze taak om te verwijderen uit de site database gegevens over client meldings taken. Deze taak is van toepassing op gegevens die gedurende een opgegeven periode niet zijn bijgewerkt. Zie [client meldingen](../../clients/manage/client-notification.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-passcode-records"></a>Verouderde wachtwoord code records verwijderen

Gebruik deze taak op de site op het hoogste niveau van uw hiërarchie om verouderde wachtwoord code voor Windows Phone apparaten opnieuw instellen te verwijderen. De wachtwoord code voor het opnieuw instellen van gegevens is versleuteld, maar bevat de pincode voor apparaten. Standaard is deze taak ingeschakeld en worden gegevens die ouder zijn dan één dag verwijderd.  

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-replication-data"></a>Verouderde replicatie gegevens verwijderen

Gebruik deze taak om de verouderde gegevens over database replicatie tussen Configuration Manager sites uit de data base te verwijderen. Wanneer u de configuratie van deze onderhoudstaak wijzigt, geldt de configuratie voor elke toepasselijke site in de hiërarchie. Zie [Data Base-replicatie bewaken](monitor-replication.md)voor meer informatie.  

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|**Secundaire site**|Ingeschakeld|

### <a name="delete-aged-replication-summary-data"></a>Verouderde gegevens van replicatie samenvatting verwijderen

Gebruik deze taak om de overzichts gegevens van de site database verouderde replicatie te verwijderen wanneer deze gedurende een opgegeven periode niet is bijgewerkt. Zie [Data Base-replicatie bewaken](monitor-replication.md)voor meer informatie.  

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|**Secundaire site**|Ingeschakeld|

### <a name="delete-aged-status-messages"></a>Verouderde status berichten verwijderen

Gebruik deze taak om de verouderde status bericht gegevens uit de data base te verwijderen zoals geconfigureerd in status filter regels. Zie [het status systeem van Configuration Manager bewaken](use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus)voor meer informatie.

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-threat-data"></a>Verouderde bedreigings gegevens verwijderen

Gebruik deze taak om te verwijderen uit de data base verouderde Endpoint Protection bedreigings gegevens die langer dan een opgegeven periode zijn opgeslagen. Zie [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-unknown-computers"></a>Verouderde onbekende computers verwijderen

Gebruik deze taak om informatie over onbekende computers uit de site database te verwijderen wanneer deze gedurende een opgegeven periode niet is bijgewerkt. Zie [voor bereidingen voor onbekende computer implementaties](../../../osd/get-started/prepare-for-unknown-computer-deployments.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-aged-user-device-affinity-data"></a>Verouderde gegevens van affiniteit van gebruiker met apparaat verwijderen

Gebruik deze taak om verouderde gegevens van affiniteit tussen gebruikers en apparaten uit de data base te verwijderen. Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-duplicate-system-discovery-data"></a>Dubbele systeem detectie gegevens verwijderen

Gebruik deze taak om alle dubbele records die door systeem detectie zijn gegenereerd uit de site database te verwijderen.<!-- SCCMDocs#1339 -->

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|Primaire site|Niet beschikbaar|
|Secundaire site|Niet beschikbaar|

### <a name="delete-expired-mdm-bulk-enroll-package-records"></a>Verlopen records voor MDM-inschrijvings pakketten verwijderen

Gebruik deze taak om oude certificaten voor bulk inschrijving en de bijbehorende profielen te verwijderen nadat het certificaat voor inschrijving is verlopen. Zie [certificaat profielen maken](../../../protect/deploy-use/create-certificate-profiles.md)voor meer informatie.

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-inactive-client-discovery-data"></a>Niet-actieve client detectie gegevens verwijderen

Gebruik deze taak om te verwijderen uit de data base-detectie gegevens voor inactieve clients. De site markeert clients als inactief wanneer de client wordt gemarkeerd als verouderd en door configuraties die worden gemaakt voor de client status.

Deze taak werkt alleen op resources die worden Configuration Manager-clients. Dit wijkt af van de taak **verouderde detectie gegevens verwijderen** , waarmee verouderde detectie gegevens records worden verwijderd. Wanneer deze taak op één site wordt uitgevoerd, verwijdert deze gegevens uit de database op alle sites in een hiërarchie. Zie [How to configure client status](../../clients/deploy/configure-client-status.md)voor meer informatie.

> [!IMPORTANT]  
> Wanneer deze is ingeschakeld, configureert u deze taak zodanig dat deze wordt uitgevoerd met een interval dat groter is dan het **heartbeat-detectie** schema. Met deze configuratie kunnen actieve clients een heartbeat-detectie record verzenden om hun client record als actief te markeren zodat deze taak ze niet verwijdert.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Niet ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-obsolete-alerts"></a>Verouderde waarschuwingen verwijderen

Gebruik deze taak om de verlopen waarschuwingen uit de data base te verwijderen die langer dan een opgegeven periode zijn opgeslagen. Zie [waarschuwingen en het status systeem gebruiken](use-alerts-and-the-status-system.md)voor meer informatie.

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-obsolete-client-discovery-data"></a>Verouderde client detectie gegevens verwijderen

Gebruik deze taak om verouderde client records uit de data base te verwijderen. Een record die als verouderd is gemarkeerd, is gewoonlijk vervangen door een nieuwere record voor dezelfde client. De nieuwe record wordt de huidige record van de client. Zie [detectie uitvoeren](../deploy/configure/run-discovery.md)voor meer informatie over detectie.

> [!IMPORTANT]  
> Wanneer deze is ingeschakeld, configureert u deze taak zodanig dat deze wordt uitgevoerd met een interval dat groter is dan het heartbeat-detectie schema. Met deze configuratie kan de client een heartbeat-detectie record verzenden waarmee de status verouderd correct wordt ingesteld.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Niet ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-obsolete-forest-discovery-sites-and-subnets"></a>Verouderde forest-detectie sites en-subnetten verwijderen

Gebruik deze taak om gegevens over Active Directory sites, subnetten en domeinen te verwijderen. Er worden gegevens verwijderd die de site niet heeft gedetecteerd door de Active Directory-forest-detectie methode in de afgelopen 30 dagen. Deze taak verwijdert de detectie gegevens, maar heeft geen invloed op de grenzen die u maakt op basis van deze detectie gegevens. Zie [detectie uitvoeren](../deploy/configure/run-discovery.md)voor meer informatie.

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="delete-orphaned-client-deployment-state-records"></a>Zwevende status records voor client implementatie verwijderen

Gebruik deze taak om regel matig de tabel met informatie over de status van client implementaties op te schonen. Met deze taak worden de records opgeschoond die zijn gekoppeld aan verouderde of buiten gebruik gestelde apparaten.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="evaluate-collection-members"></a>Verzamelings leden evalueren

U configureert de evaluatie van het verzamelings lidmaatschap als een site onderdeel. Zie [site onderdelen](../deploy/configure/site-components.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="monitor-keys"></a>Sleutels bewaken

Gebruik deze taak om de integriteit van de primaire sleutels van de Configuration Manager-Data Base te controleren. Een primaire sleutel is een kolom of een combi natie van kolommen die een unieke identificatie vormen voor één rij. De sleutel onderscheidt de rij van een andere rij in een Microsoft SQL Server database tabel.

|||
|---------|---------|
|**Centrale beheersite**|Ingeschakeld|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="rebuild-indexes"></a>Indexen opnieuw samen stellen

Gebruik deze taak om de Configuration Manager database indexen opnieuw samen te stellen. Een index is een database structuur die op een database tabel is gemaakt om het ophalen van gegevens te versnellen. Het doorzoeken van een geïndexeerde kolom is bijvoorbeeld vaak veel sneller dan het doorzoeken van een kolom die niet is geïndexeerd.

Om de prestaties te verbeteren, worden de Configuration Manager database indexen regel matig bijgewerkt om gesynchroniseerd te blijven met de voortdurend veranderende gegevens die in de Data Base zijn opgeslagen. Deze taak:

- Maakt indexen voor database kolommen die ten minste 50 procent uniek zijn
- Verwijdert indexen voor kolommen die kleiner zijn dan 50 procent uniek
- Alle bestaande indexen opnieuw samen stellen die voldoen aan de criteria voor de uniekheid van gegevens

|||
|---------|---------|
|**Centrale beheersite**|Niet ingeschakeld|
|**Primaire site**|Niet ingeschakeld|
|**Secundaire site**|Niet ingeschakeld|

### <a name="summarize-file-usage-metering-data"></a>Meet gegevens voor bestands gebruik samenvatten

Met deze taak kunt u de gegevens van meerdere records voor het gebruik van software licentie controle bestand samenvatten in één algemeen record. Met gegevens samenvatting kunt u de hoeveelheid gegevens die is opgeslagen in de Configuration Manager Data Base comprimeren.

Als u gegevens van software meter wilt samenvatten en schijf ruimte wilt besparen in de-data base, gebruikt u deze taak met de taak de **maandelijkse gebruiks gegevens van software licentie controle samenvatten** . Zie [software licentie controle](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="summarize-installed-software-data"></a>Geïnstalleerde software gegevens samenvatten

Met deze taak kunt u de gegevens van verzamelde Asset Intelligence-software gegevens via de hardware-inventaris samenvatten om meerdere records samen te voegen in één algemeen record. Met gegevens samenvatting kunt u de hoeveelheid gegevens die is opgeslagen in de Configuration Manager Data Base comprimeren. Zie [Asset Intelligence-onderhouds taken configureren](../../clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_ConfigureMaintenanceTasks)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="summarize-monthly-usage-metering-data"></a>Maandelijkse gebruiks meet gegevens samenvatten

Met deze taak kunt u de gegevens van meerdere records voor het maandelijkse gebruik van software licentie controle in één algemeen record samenvatten. Met gegevens samenvatting kunt u de hoeveelheid gegevens die is opgeslagen in de Configuration Manager Data Base comprimeren.

Gebruik deze taak met de taak **gebruiks gegevens van software meter bestand** samenvatten om gegevens van software meter samenvatten en ruimte te besparen in de-data base. Zie [software licentie controle](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)voor meer informatie.

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="update-application-available-targeting"></a>Beschik bare doel items voor toepassing bijwerken

Gebruik deze taak om de toewijzing van beleid en toepassings implementaties aan resources in verzamelingen Configuration Manager herberekenen. Wanneer u beleid of toepassingen implementeert voor een verzameling, maakt Configuration Manager een initiële toewijzing tussen de objecten die u implementeert en de leden van de verzameling.

Deze toewijzingen worden opgeslagen in een tabel zodat u deze eenvoudig kunt raadplegen. Wanneer een lidmaatschap van een verzameling wordt gewijzigd, werkt de site deze opgeslagen toewijzingen bij om deze wijzigingen door te voeren. Het is echter mogelijk dat deze toewijzingen niet worden gesynchroniseerd. Als de site bijvoorbeeld een meldings bestand niet goed kan verwerken, wordt die wijziging mogelijk niet weer spie geld in een wijziging in de toewijzingen. Met deze taak wordt de toewijzing vernieuwd op basis van het huidige verzamelings lidmaatschap.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|

### <a name="update-application-catalog-tables"></a>toepassingscatalogus tabellen bijwerken

Gebruik deze taak om de toepassingscatalogus website database cache te synchroniseren met de nieuwste toepassings gegevens. Wanneer u de configuratie van deze onderhouds taak wijzigt, is dit van toepassing op alle primaire sites in de hiërarchie.  

|||
|---------|---------|
|Centrale beheersite|Niet beschikbaar|
|**Primaire site**|Ingeschakeld|
|Secundaire site|Niet beschikbaar|


## <a name="see-also"></a>Zie ook

[Onderhoudstaken](maintenance-tasks.md)
