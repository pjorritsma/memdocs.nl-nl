---
title: Software-updates controleren
titleSuffix: Configuration Manager
description: De Configuration Manager-console bevat waarschuwingen en statussen voor het bewaken van updates en naleving.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110369"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>Software-updates controleren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager biedt veel manieren om u te helpen bij het bewaken van software-update objecten, processen en compatibiliteits informatie. Gebruik de volgende secties om software-updates te controleren.

## <a name="software-updates-dashboard"></a>Dash board voor software-updates

*(Geïntroduceerd in versie 1610)*

Vanaf Configuration Manager versie 1610 kunt u het dash board voor software-updates gebruiken om de huidige nalevings status van apparaten in uw organisatie weer te geven en snel de gegevens te analyseren om te zien welke apparaten risico lopen. Als u het dash board wilt weer geven, gaat u naar **bewaking** > **overzicht** > **Security** > **software updates dash board**.

## <a name="drill-through-required-updates"></a>Bekijk de vereiste updates
<!--4224414-->
*(Geïntroduceerd in versie 1906)*

U kunt inzoomen op nalevings statistieken om te zien welke apparaten een specifieke Microsoft 365 apps software-update nodig hebben. Als u de lijst met apparaten wilt weer geven, hebt u machtigingen nodig voor het weer geven van updates en de verzamelingen waartoe de apparaten behoren. Inzoomen op de apparaten lijst:

1. Ga naar **Software Library** > **software updates** > **alle software-updates**.
1. Selecteer een update die vereist is voor ten minste één apparaat.
1. Ga naar het tabblad **samen vatting** en zoek het cirkel diagram onder **Statistieken**.
1. Selecteer de **weer gave vereiste** Hyper link naast het cirkel diagram om in te zoomen op de apparaten lijst.
1. Met deze actie gaat u naar een tijdelijk knoop punt onder **apparaten** waar u de apparaten kunt zien waarvoor de update is vereist. U kunt ook acties uitvoeren voor het knoop punt, zoals het maken van een nieuwe verzameling in de lijst.


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> Waarschuwingen voor software-updates  
 U kunt waarschuwingen voor software-updates configureren om gebruikers met beheerdersrechten te waarschuwen wanneer compatibiliteitsniveaus voor implementaties van software-updates onder het geconfigureerde percentage uitkomen. U kunt op de volgende locaties waarschuwingen voor implementaties van software-updates configureren:  

-   ADR-instelling: u kunt de instellingen voor waarschuwingen configureren in de wizard Regel voor automatische implementatie en in de eigenschappen voor de regel voor automatische implementatie.  

-   Implementatie-instelling: u kunt de instellingen voor waarschuwingen configureren in de wizard Software-updates implementeren en in de implementatie-eigenschappen.  

Nadat u de waarschuwings instellingen hebt geconfigureerd, wordt door Configuration Manager een waarschuwing gegenereerd als de opgegeven voor waarden zich voordoen. U kunt de waarschuwingen voor software-updates op de volgende locaties weergeven:  

1.  U kunt recente waarschuwingen weergeven in het knooppunt **Software-updates** in de werkruimte **Softwarebibliotheek** .  

2.  U kunt de geconfigureerde waarschuwingen beheren in het knooppunt **Waarschuwingen** in de werkruimte **Controle** .  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a>Synchronisatie status van software-updates  
 Nadat u het synchronisatie proces hebt gestart, kunt u het synchronisatie proces bewaken vanuit de Configuration Manager-console voor alle software-update punten in uw hiërarchie. Gebruik de volgende procedure om het synchronisatieproces voor software-updates te controleren.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Het synchronisatieproces voor software-updates controleren  

- Ga in de Configuration Manager-console naar **bewaking** > **overzicht** > **synchronisatie status van software-update punten**.  

    De software-update punten in uw Configuration Manager-hiërarchie worden weer gegeven in het deel venster met resultaten. In deze weergave kunt u de synchronisatiestatus van alle software-updatepunten controleren. Als u meer gedetailleerde informatie over het synchronisatie proces wilt zien, kunt u het bestand bestand Wsyncmgr. log bekijken, dat zich bevindt in <*ConfigMgrInstallationPath*> \logs op elke site server.  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> Implementatiestatus van software-updates  
 Nadat u de software-updates in een software-updategroep hebt geïmplementeerd of nadat u een afzonderlijke software-updates hebt geïmplementeerd, kunt u de implementatiestatus controleren. Gebruik de volgende procedure om de implementatiestatus van een software-updategroep of software-update te controleren.  

#### <a name="to-monitor-deployment-status"></a>De implementatiestatus controleren  

1.  Ga in de Configuration Manager-console naar **bewakings** > **overzicht** > **implementaties**.  

2.  Klik op de software-updategroep of software-update waarvan u de implementatiestatus wilt controleren.  

3.  Klik op het tabblad **Starten** in de groep **Implementatie** op **Status weergeven**.  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> Rapporten van software-updates  
 De statusberichten voor software-updates bieden informatie over de compatibiliteit van software-updates en over de evaluatie en afdwingingsstatus van implementaties van software-updates. U kunt software-updaterapporten uitvoeren om deze statusberichten weer te geven. Er zijn meer dan 30 vooraf gedefinieerde software-updaterapporten beschikbaar. Ze zijn ingedeeld in verschillende categorieën en kunnen worden gebruikt voor het rapporteren van specifieke informatie over software-updates en implementaties. U kunt naast deze vooraf geconfigureerde rapporten ook aangepaste software-updaterapporten maken op basis van de behoeften van uw bedrijf. Zie [bewerkingen en onderhoud voor rapportage](../../core/servers/manage/operations-and-maintenance-for-reporting.md)voor meer informatie.  

### <a name="recommended-software-updates-reports"></a>Aanbevolen rapporten voor software-updates
Hier volgen enkele van de rapporten die u kunt gebruiken om potentiële problemen te identificeren: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Naleving 9: algehele status en naleving (vanaf versie 1806)
Het rapport bevat de volgende onderdelen:

- **Goede clients versus totaal aantal clients**: dit staaf diagram vergelijkt de "gezonde" clients die in de opgegeven tijds periode hebben gecommuniceerd met de site ten opzichte van het totale aantal clients in de opgegeven verzameling.
- **Overzicht van naleving**: in dit cirkel diagram wordt de algemene compatibiliteits status weer gegeven voor de specifieke software-update groep op actieve clients in de opgegeven verzameling.
- **Top 5 niet-compatibel met artikel-id**: in dit staaf diagram worden de vijf meest voorkomende software-updates in de opgegeven groep weer gegeven die niet compatibel zijn op actieve clients in de opgegeven verzameling.
- De onderkant van het rapport is een tabel met meer details, waarin de software-updates in de opgegeven groep worden weer gegeven.

#### <a name="management-2---updates-required-but-not-deployed"></a>Beheer 2 - Updates vereist maar niet geïmplementeerd

In dit rapport worden leverancierspecifieke software-updates weer gegeven in een specifieke update classificatie die is gedetecteerd als vereist op clients, maar die niet zijn geïmplementeerd voor een specifieke verzameling. 

#### <a name="troubleshooting-2---deployment-errors"></a>Problemen oplossen 2-implementatie fouten

Dit rapport retourneert de implementatie fouten op de site en een telling van de computers waarbij elke fout optreedt. 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a>Inhoud bewaken  
 U kunt inhoud bewaken in de Configuration Manager-console om de status van alle pakket typen in relatie tot de gekoppelde distributie punten te controleren. Dit kan het volgende omvatten: de validatiestatus voor de inhoud in het pakket, de status van inhoud die is toegewezen aan een specifieke distributiepuntengroep, de status van inhoud die is toegewezen aan een distributiepunt en de status van optionele functies voor de afzonderlijke distributiepunten (inhoudvalidatie, PXE en multicast).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Controle van de status van inhoud  
 Het knooppunt **Status van inhoud** in de werkruimte **Controle** biedt informatie over inhoudspakketten. U kunt algemene informatie over het pakket, de distributiestatus voor het pakket en gedetailleerde statusinformatie over het pakket weergeven. Gebruik de volgende procedure om de status van inhoud weer te geven.  

#### <a name="to-monitor-content-status"></a>De status van inhoud controleren  

1.  Ga in de Configuration Manager-console naar **bewaking** > **overzicht** > **distributie status** > van de**inhouds status**. De pakketten worden weergegeven.  

2.  Selecteer het pakket waarvoor u gedetailleerde statusinformatie wilt weergeven.  

3.  Klik op het tabblad **Start** op **Status weergeven**. De gedetailleerde statusinformatie voor het pakket wordt weergegeven.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a>Status van distributiepunten groep  
 Het knooppunt **Status van distributiepuntengroep** in de werkruimte **Controle** biedt informatie over distributiepuntengroepen. U kunt algemene informatie weergeven over de distributiepuntengroep, zoals de status van de distributiepuntengroep en het compatibiliteitspercentage, evenals gedetailleerde statusinformatie voor de distributiepuntengroep. Gebruik de volgende procedure om de status van een distributiepuntengroep weer te geven.  

#### <a name="to-monitor-distribution-point-group-status"></a>De status van een distributiepuntengroep bewaken  

1.  Ga in de Configuration Manager-console naar **bewaking** > **overzicht** > **distributie status** > distributiepunt**groep status**. De distributiepuntengroepen worden weergegeven.  

2.  Selecteer de distributiepuntengroep waarvoor u gedetailleerde statusinformatie wilt weergeven.  

3.  Klik op het tabblad **Start** op **Status weergeven**. Er wordt gedetailleerde statusinformatie voor de distributiepuntengroep weergegeven.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> Configuratiestatus van distributiepunt  
 Het knooppunt **Configuratiestatus van distributiepunt** in de werkruimte **Controle** biedt informatie over de distributiepuntengroep. U kunt weergeven welke kenmerken voor het distributiepunt zijn ingeschakeld, zoals PXE, multicast en validatie van inhoud. U kunt tevens gedetailleerde statusinformatie voor het distributiepunt weergeven. Gebruik de volgende procedure om de configuratiestatus van een distributiepuntengroep weer te geven.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Bewaken van de configuratiestatus van distributiepunten  

1.  Ga in de Configuration Manager-console naar **bewaking** > **overzicht** > **distributie status** > distributiepunt**configuratie status**. De distributiepunten worden weergegeven.  

2.  Selecteer het distributiepunt waarvoor u de statusinformatie wilt weergeven.  

3.  Klik op het tabblad **Details** in het resultaten venster. de status informatie voor het distributie punt wordt weer gegeven.  

## <a name="next-steps"></a>Volgende stappen

- [Logboek bestanden voor software-updates](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Technisch document van software-updates](https://www.microsoft.com/download/confirmation.aspx?id=44578)
