---
title: Clients bewaken
titleSuffix: Configuration Manager
description: Gedetailleerde richt lijnen voor het controleren van clients in Configuration Manager
ms.date: 09/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8094db944a1430311f0c3bb8c94bc7043b12c5ae
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574610"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Clients controleren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u de Configuration Manager-client op de Windows-apparaten in uw site hebt geïnstalleerd, controleert u de status en activiteit in de Configuration Manager-console.  


## <a name="about-client-status"></a><a name="bkmk_about"></a> Over de client status

Configuration Manager biedt de volgende soorten informatie als client status:  

- **Online status van client**: op de site wordt een apparaat als **online** beschouwd als het is verbonden met het toegewezen beheer punt. Om aan te geven dat de client online is, verzendt deze ping-achtige berichten naar het beheer punt. Als het beheer punt binnen vijf minuten geen bericht ontvangt, beschouwt de site de client als **offline**.  

- **Client activiteit**: de site beschouwt de client als **actief** als deze in de afgelopen zeven dagen is gecommuniceerd met Configuration Manager. De site beschouwt de client **inactief** als de volgende acties in zeven dagen niet zijn uitgevoerd:  

    - Aangevraagde beleids update  
    - Er is een heartbeat-bericht verzonden  
    - Verzonden hardware-inventaris  

- **Client controle**: de status van de periodieke evaluatie dat de Configuration Manager-client op het apparaat wordt uitgevoerd. De evaluatie controleert het apparaat en kan enkele van de gevonden problemen oplossen. Zie [client status controles](#BKMK_ClientHealth)voor meer informatie.  

     Op apparaten waarop Windows 7 wordt uitgevoerd, wordt de client controle uitgevoerd als een geplande taak. Bij latere versies van het besturings systeem wordt de client controle automatisch uitgevoerd tijdens het Windows-onderhouds venster.  

     U kunt herstel configureren om niet te worden uitgevoerd op specifieke apparaten, bijvoorbeeld een bedrijfs kritieke server. Als er extra items zijn die u wilt evalueren, gebruikt u Configuration Manager instellingen voor naleving om aanvullende configuraties te controleren. Zie [instellingen voor naleving plannen en configureren](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)voor meer informatie over nalevings instellingen.  

- **Buiten gebruik gesteld**: de site heeft de record van het apparaat gemarkeerd voor verwijdering. Dit gedrag kan optreden wanneer een nieuwe registratie voor hetzelfde apparaat wordt toegewezen aan dezelfde of een andere primaire site in een hiërarchie. De site verwijdert deze apparaten de volgende keer dat de onderhouds taak van de site **verouderde detectie gegevens verwijderen**.<!-- SCCMDocs issue #1418 -->  

- **Verouderd**: de site heeft een nieuwe apparaat-record gevonden met dezelfde hardware-id, zodat de oude record als verouderd wordt gemarkeerd. Rapporten tellen geen verouderde records van hetzelfde apparaat meerdere keren. U kunt nog steeds beleid bereiken voor verouderde apparaten. Als de site geen heartbeat voor een verouderde record krijgt na 90 dagen van inactiviteit, wordt het verouderde apparaat verwijderd tijdens het uitvoeren van de site onderhoud taak **verouderde client detectie gegevens verwijderen**.


## <a name="monitor-individual-clients"></a><a name="bkmk_indStatus"></a> Afzonderlijke clients bewaken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** . Selecteer het knoop punt **apparaten** of kies een verzameling onder **apparaten verzamelingen**.  

    De pictogrammen aan het begin van elke rij geven de online status van het apparaat aan:  

    | Pictogram | Beschrijving |
    | ---- | ----------- |  
    |![online-statuspictogram voor clients](../../../core/clients/manage/media/online-status-icon.png)|Apparaat is online|  
    |![offline-statuspictogram voor clients](../../../core/clients/manage/media/offline-status-icon.png)|Het apparaat is offline|  
    |![onbekende-statuspictogram voor clients](../../../core/clients/manage/media/unknown-status-icon.png)|Online status is onbekend|  
    |![client niet geïnstalleerd](../../../core/clients/manage/media/client-not-installed.png)|De client is niet geïnstalleerd op het apparaat|  

2. Voor een gedetailleerde online status voegt u de online status gegevens van de client toe aan de weer gave apparaat. Klik met de rechter muisknop op de kolomkop en selecteer de online status velden die u wilt toevoegen:

    - **Online status**van het apparaat: geeft aan of de client op dit moment online of offline is. (Deze status is dezelfde informatie die door de pictogrammen wordt gegeven.)  

    - **Tijdstip van de laatste online**: geeft aan wanneer de online status van de client is gewijzigd in online  

    - **Laatste tijdstip offline** geeft aan wanneer de status is gewijzigd in offline  

3. Selecteer een afzonderlijke client in het lijst deel venster om meer statussen in het detail venster weer te geven. Deze informatie omvat client activiteit en client controle status.  


## <a name="client-health-dashboard"></a><a name="bkmk_health"></a> Client status dashboard

<!--3599209-->
U implementeert software-updates en andere apps om uw omgeving te beveiligen, maar deze implementaties bereiken alleen gezonde clients. Slechte Configuration Manager-clients hebben een negatieve invloed op de algehele naleving. Het bepalen van de status van de client kan lastig zijn, afhankelijk van de noemer: hoeveel apparaten in totaal moeten worden beheerd? Als u bijvoorbeeld alle systemen van Active Directory ontdekt, zelfs als sommige van deze records voor buiten gebruik gestelde machines zijn, neemt dit proces uw noemer toe.

Configuration Manager biedt een dash board met informatie over de status van clients in uw omgeving. Bekijk de status van uw client, scenario status en veelvoorkomende fouten. Filter de weer gave op diverse kenmerken om potentiële problemen per OS en client versies te bekijken.

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** . Vouw **client status**uit en selecteer het knoop punt **client status dashboard** .

:::image type="content" source="media/3599209-client-health-dashboard.png" alt-text="Scherm afbeelding client status dashboard" lightbox="media/3599209-client-health-dashboard.png":::

> [!Tip]  
> Er zijn geen wijzigingen in ccmeval.  

Standaard worden in het dash board van de client status online-clients en-clients weer gegeven die in de afgelopen drie dagen actief zijn. Daarom ziet u mogelijk verschillende getallen in dit dash board dan in andere historische bronnen van client status. Bijvoorbeeld andere knoop punten onder **client status**of rapporten in de categorie client status.

### <a name="filters"></a>Filters

Boven aan het dash board bevindt zich een set filters voor het aanpassen van de gegevens die in het dash board worden weer gegeven.

- **Client status voor clients in de volgende verzamelingen**: in het dash board worden standaard apparaten weer gegeven in de verzameling **alle systemen** . Selecteer een apparaat verzameling om de weer gave te beperken tot een subset van apparaten in een bepaalde verzameling.  

- **Client actief in het afgelopen aantal dagen**: standaard geeft het dash board clients weer die in de afgelopen drie dagen actief zijn.  

- **Client status voor offline clients toevoegen**: standaard worden alleen online clients weer gegeven in het dash board. Deze status is afkomstig van het kanaal voor client meldingen dat elke vijf minuten de status van een client bijwerkt. Zie [about client status](monitor-clients.md#bkmk_about)voor meer informatie.  

- **Alleen details van de status van de client weer geven**: bereik de weer gave alleen voor apparaten die een client status fout rapporteren.  

    > [!Tip]  
    > Gebruik dit filter samen met de tegels van de client versie en de besturingssysteem versie. Zie [versie tegels](#version-tiles)voor meer informatie.

### <a name="overall-client-health"></a>Algehele client status

Deze tegel toont de algehele client status in uw hiërarchie.

Een gezonde Configuration Manager client heeft de volgende eigenschappen:

- Online  
- Gegevens actief verzenden  
- Alle evaluatie controles voor de client status door lopen  

Zie [about client status](monitor-clients.md#bkmk_about)voor meer informatie.

Een gezonde client communiceert met de site. Alle gegevens op basis van de gedefinieerde schema's in de client instellingen worden gerapporteerd.

Selecteer een segment van dit diagram om in te zoomen op een weer gave met apparaten lijsten.

### <a name="version-tiles"></a>Versie tegels

Er zijn twee tegels die de client status weer geven op Configuration Manager client versie en de versie van het besturings systeem. Deze tegels zijn nuttig wanneer u wijzigingen aanbrengt in de filters, zoals **alleen fout**. Ze kunnen u helpen om te benadrukken of er problemen zijn in een specifieke versie. Gebruik deze informatie om u te helpen bij het maken van upgrade beslissingen.

Selecteer een segment van deze grafieken om in te zoomen op een weer gave met apparaten lijsten.

### <a name="scenario-health"></a>Scenario status

Dit staaf diagram toont de algemene status van de volgende kern scenario's:

- Client beleid
- Heartbeat-detectie
- Hardware-inventaris
- Software-inventaris
- Statusberichten

Gebruik de selecters om de focus op specifieke scenario's in de grafiek aan te passen.

De volgende twee balken worden altijd weer gegeven:

- **Gecombineerd (alle)**: de combi natie van alle SCENARIO'S (en)  
- **Gecombineerd (elk)**: ten minste één van de SCENARIO'S (of)

> [!Tip]  
> Scenario status wordt niet gemeten op basis van uw configuratie van client instellingen. Deze waarden kunnen variëren op basis van de resulterende verzameling beleids regels per apparaat. Gebruik de volgende stappen om de evaluatie perioden voor scenario status aan te passen:
>
> - Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer het knoop punt **client status** .  
> - Selecteer in het lint **client status instellingen**.  
>
> Als een client geen scenario-specifieke gegevens in **zeven dagen**verzendt, wordt de status van het scenario standaard in Configuration Manager beschouwd.

### <a name="top-10-client-health-failures"></a>Top 10 van client status fouten

In dit diagram vindt u de meest voorkomende storingen in uw omgeving. Deze fouten zijn afkomstig van Windows of Configuration Manager.

<!-- The following list includes some of the more common failures overall:

#### Failure 1 title
Failure 1 description

Solution for failure 1 -->


## <a name="monitor-the-status-of-all-clients"></a><a name="bkmk_allStatus"></a> De status van alle clients controleren

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer het knoop punt **client status** . Bekijk de algemene statistieken voor client activiteit en client controles op de site. Wijzig het bereik van de informatie door een andere verzameling te kiezen.  

2. Als u details over de gerapporteerde statistieken wilt inzoomen, kiest u de naam van de gerapporteerde informatie. Bijvoorbeeld **actieve clients die de client controle hebben doorstaan of waarvoor geen resultaten zijn opgegeven**. Bekijk vervolgens de informatie over de afzonderlijke clients.  

3. Selecteer **client activiteit** om de grafieken weer te geven met de client activiteit in uw Configuration Manager-site.  

4. Selecteer **client controle** om de grafieken weer te geven met de status van client controles in uw Configuration Manager-site.  

    Waarschuwingen configureren om u te waarschuwen wanneer client controle resultaten of client activiteit onder een opgegeven percentage daalt. De site kan u ook waarschuwen wanneer herbemiddeling mislukt op een opgegeven percentage clients. Zie [How to configure client status](../deploy/configure-client-status.md)voor meer informatie.  


## <a name="client-health-checks"></a><a name="BKMK_ClientHealth"></a> Client status controles

Client controle voert de volgende controles en herstel bewerkingen uit:  

|Clientcontrole|Herstelactie|Meer informatie|  
|------------------|------------------------|----------------------|  
|Controleer of dat de clientcontrole onlangs is uitgevoerd|Clientcontrole uitvoeren|Controleert of de clientcontrole ten minste eenmaal in de voorbije drie dagen is uitgevoerd.|  
|Controleer of vereiste clientonderdelen zijn geïnstalleerd|Installeer de vereiste clientonderdelen|Controleert of vereiste clientonderdelen zijn geïnstalleerd. Leest het bestand ccmsetup.xml in de clientinstallatiemap om te bepalen welke onderdelen vereist zijn.|  
|Integriteitstest WMI-rapportage|De Configuration Manager-client opnieuw installeren|Controleert of Configuration Manager client vermeldingen aanwezig zijn in WMI.|  
|Controleer of de clientservice actief is|Start de clientservice (SMS Agent Host)|Geen aanvullende informatie|  
|Test WMI-gebeurtenis-opvanger.|Start de clientservice opnieuw|Controleer of de Configuration Manager gerelateerde WMI-gebeurtenis sink verloren is gegaan|  
|Controleer of de WMI-service (Windows Management Instrumentation) bestaat|Geen herstel mogelijk|Geen aanvullende informatie|  
|Controleer of de client correct is geïnstalleerd|Installeer de client opnieuw|Geen aanvullende informatie|  
|Controleer of het opstarttype voor de antimalwareservice automatisch is|Stel het opstarttype van de service opnieuw in op automatisch|Geen aanvullende informatie|  
|Controleer of de antimalwareservice actief is|Start de antimalwareservice|Geen aanvullende informatie|  
|Controleer of het opstarttype voor de Windows Update-service automatisch of handmatig is|Stel het opstarttype van de service opnieuw in op automatisch|Geen aanvullende informatie|  
|Controleer of het opstarttype voor de clientservice (SMS Agent Host) automatisch is|Stel het opstarttype van de service opnieuw in op automatisch|Geen aanvullende informatie|  
|Controleer of de WMI-service (Windows Management Instrumentation) actief is.|Start de WMI-service|Geen aanvullende informatie|  
|Controleer de conditie van de Microsoft SQL CE-database|De Configuration Manager-client opnieuw installeren|Geen aanvullende informatie|  
|WMI-integriteitstest van het Microsoft-beleidsplatform|Het Microsoft-beleidsplatform herstellen|Geen aanvullende informatie|  
|Controleer of de service Microsoft-beleidsplatform bestaat|Het Microsoft-beleidsplatform herstellen|Geen aanvullende informatie|  
|Controleer of het opstarttype voor de service Microsoft-beleidsplatform handmatig is.|Stel het opstarttype van de service opnieuw in op handmatig|Geen aanvullende informatie|  
|Controleer of Background Intelligent Transfer Service bestaat|Geen herstel mogelijk|Geen aanvullende informatie|  
|Controleer of het opstarttype voor Background Intelligent Transfer Service automatisch of handmatig is|Stel het opstarttype van de service opnieuw in op automatisch|Geen aanvullende informatie|  
|Controleer of het opstarttype voor de netwerkinspectieservice handmatig is|Stel het opstarttype van de service, indien geïnstalleerd, opnieuw in op handmatig|Geen aanvullende informatie|  
|Controleer of het opstarttype voor de WMI-service (Windows Management Instrumentation) automatisch is.|Stel het opstarttype van de service opnieuw in op automatisch|Geen aanvullende informatie|  
|Controleer of het opstart type voor de Windows Update-service op Windows 8-apparaten automatisch of hand matig is|Stel het opstarttype van de service opnieuw in op handmatig|Geen aanvullende informatie|  
|Controleer of de clientservice (SMS Agent Host) bestaat.|Geen herstel mogelijk|Geen aanvullende informatie|  
|Controleer of het opstarttype voor de Configuration Manager-service voor extern beheer automatisch of handmatig is|Stel het opstarttype van de service opnieuw in op automatisch|Geen aanvullende informatie|  
|Controleer of de Configuration Manager-service voor extern beheer wordt uitgevoerd|Start de service voor extern beheer|Geen aanvullende informatie|  
|Controleer of de service Wake-up proxy wordt uitgevoerd|Start de ConfigMgr-service Wake-up proxy|De clientcontrole wordt alleen uitgevoerd wanneer de clientinstelling **Energiebeheer**: **Wake-up proxy inschakelen** op de ondersteunde clientbesturingssystemen is ingesteld op **Ja** .|  
|Controleer of het opstarttype voor de service Wake-up proxy automatisch is|Stel het opstarttype voor de ConfigMgr-service Wake-up proxy opnieuw in op automatisch|De clientcontrole wordt alleen uitgevoerd wanneer de clientinstelling **Energiebeheer**: **Wake-up proxy inschakelen** op de ondersteunde clientbesturingssystemen is ingesteld op **Ja** .|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Logboek bestanden voor client implementatie

Zie [logboek bestanden](../../plan-design/hierarchy/log-files.md#BKMK_ClientLogs)voor meer informatie over de logboek bestanden die worden gebruikt door client implementatie-en beheer bewerkingen.
