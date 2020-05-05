---
title: Site systeem rollen plannen
titleSuffix: Configuration Manager
description: Overweeg site systeem servers en site systeem rollen bij het plannen van uw Configuration Manager-hiërarchie.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3fb8c54920c10f8d3601a939c3c7b442c95e1dcf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722443"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Plannen voor site systeem servers en site systeem rollen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Elke Configuration Manager-site die u installeert, bevat een site server die een **site systeem server**is. De site kan ook extra sitesysteemservers bevatten op computers die zich op afstand van de siteserver bevinden. Sitesysteemservers (de siteserver of een externe sitesysteemserver) bieden ondersteuning voor **sitesysteemrollen**.  

## <a name="site-system-servers"></a><a name="bkmk_siteservers"></a>Site systeem servers  

Wanneer u een site systeemrol installeert op een computer, wordt die computer een site systeem server. U kunt op elke site een of meer extra site systeem servers installeren. U hoeft geen extra site systeem servers te installeren en kunt ervoor kiezen om alle site systeem rollen rechtstreeks op de site Server computer uit te voeren. Elke site systeem server ondersteunt een of meer site systeem rollen. Extra servers kunnen u helpen de mogelijkheden en capaciteit van een site uit te breiden door de verwerkings belasting te delen die door de site systeem rollen op een server wordt uitgevoerd.  

Wanneer u overweegt een site systeem server toe te voegen, moet u ervoor zorgen dat de server voldoet aan de vereisten voor het beoogde gebruik. Voeg het ook toe op een netwerk locatie die voldoende band breedte heeft om te communiceren met de verwachte eind punten. Deze eind punten omvatten de site server, domein resources, een Cloud locatie, site systeem servers en clients.  


## <a name="site-system-roles"></a><a name="bkmk_planroles"></a>Site systeem rollen  

Installeer site systeem rollen op een server om extra mogelijkheden te bieden aan de site. Voorbeelden zijn:  

- Extra beheer punten zodat de site meer apparaten kan ondersteunen, tot aan de ondersteunde capaciteit van de site.  

- Extra distributie punten om uw inhouds infrastructuur uit te breiden, waardoor de prestaties van inhouds distributies naar apparaten worden verbeterd.  

- Een of meer functie-specifieke site systeem rollen. Met een software-update punt kunt u bijvoorbeeld software-updates beheren voor beheerde apparaten. Met een Reporting Services-punt kunt u rapporten uitvoeren om informatie over uw omgeving te bewaken, te begrijpen en te delen.  

Verschillende Configuration Manager-sites kunnen verschillende sets van site systeem rollen ondersteunen. De ondersteunde set site systeem rollen is afhankelijk van het type site. (De typen sites bevatten een centrale beheer site, primaire sites of secundaire sites.) De topologie van uw hiërarchie kan de plaatsing van sommige rollen bij bepaalde site typen beperken. Het service verbindings punt wordt bijvoorbeeld alleen ondersteund op de site op het hoogste niveau van de hiërarchie. De site op het hoogste niveau kan een centrale beheer site of een zelfstandige primaire site zijn. Deze rol wordt niet ondersteund op een onderliggende primaire site of op secundaire sites.  

Nadat een site is geïnstalleerd, kunt u de locatie van sommige site systeem rollen van de standaard locatie op de site server naar een andere server verplaatsen. Zo worden de rollen beheer punt of distributie punt standaard geïnstalleerd op een primaire of secundaire site server. Installeer ook extra exemplaren van sommige site systeem rollen om de mogelijkheden van uw site uit te breiden en te voldoen aan uw bedrijfs vereisten. Sommige rollen zijn vereist, terwijl andere optioneel zijn.  

### <a name="configuration-manager-site-server"></a>Site Server Configuration Manager

Deze rol identificeert de server waarop Configuration Manager-installatie wordt uitgevoerd om een site te installeren, of de server waarop u een secundaire site installeert. U kunt deze rol pas verplaatsen of verwijderen als de site is verwijderd.  

### <a name="configuration-manager-site-system"></a>Configuration Manager site systeem

Deze rol wordt toegewezen aan een computer waarop u een site installeert of een site systeemrol installeert. U kunt deze rol pas verplaatsen of verwijderen als u de laatste site systeemrol van de computer verwijdert.  

### <a name="configuration-manager-component-site-system-role"></a>Site systeemrol Configuration Manager-onderdeel

Deze rol identificeert een site systeem waarop een exemplaar van de **SMS Executive** -service wordt uitgevoerd. Het is vereist voor ondersteuning van andere rollen, zoals beheer punten. U kunt deze functie pas verplaatsen of verwijderen als u de laatst toepasselijke site systeemrol van de computer hebt verwijderd.  

### <a name="configuration-manager-site-database-server"></a>Site database server Configuration Manager

De site wijst deze rol toe aan site systeem servers die een exemplaar van de site database bevatten. Verplaats deze rol alleen naar een nieuwe server door Setup uit te voeren om de site te wijzigen voor het gebruik van een ander exemplaar van SQL Server om de site database te hosten.  

### <a name="sms-provider"></a>SMS-provider

De site wijst deze rol toe aan elke computer die als host fungeert voor een exemplaar van de SMS-provider. De provider is de interface tussen een Configuration Manager-console en de site database. Standaard wordt deze rol automatisch geïnstalleerd op de site server van een centrale beheer site en primaire sites. Installeer extra exemplaren op elke site om toegang te bieden tot extra gebruikers met beheerders rechten of voor redundantie.  

Als u extra providers wilt installeren, voert u Configuration Manager Setup uit om [de SMS-provider te beheren](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Installeer vervolgens extra providers op extra computers. Installeer slechts één exemplaar van de SMS-provider op een computer. Deze computer moet zich in hetzelfde domein als de site server bestaan.  

### <a name="application-catalog-web-service-point"></a>Application Catalog-webservicepunt

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Een site systeemrol die software-informatie verstrekt aan de Application catalog-website vanuit de software bibliotheek. Hoewel deze rol alleen op primaire sites wordt ondersteund, kunt u meerdere exemplaren van deze rol op een site of op meerdere sites in dezelfde hiërarchie installeren.  

### <a name="application-catalog-website-point"></a>Application catalog-website punt

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Een site systeemrol die gebruikers een lijst met beschik bare software uit de toepassings catalogus verschaft. Hoewel deze rol alleen op primaire sites wordt ondersteund, kunt u meerdere exemplaren van deze rol op een site of op meerdere sites in dezelfde hiërarchie installeren.  

### <a name="asset-intelligence-synchronization-point"></a>Asset Intelligence-synchronisatiepunt

Een site systeemrol die verbinding maakt met micro soft voor het downloaden van informatie voor de Asset Intelligence catalogus. Deze rol uploadt ook gecategoriseerde titels, zodat micro soft deze kan overwegen voor toekomstige opname in de catalogus. Een hiërarchie ondersteunt slechts één exemplaar van deze rol op de site op het hoogste niveau van uw hiërarchie. Als u een zelfstandige primaire site uitbreidt naar een grotere hiërarchie, verwijdert u deze rol van de primaire site. Installeer deze vervolgens op de centrale beheer site.

Zie [Asset Intelligence in Configuration Manager](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)voor meer informatie.  

### <a name="certificate-registration-point"></a>Certificaatregistratiepunt

Een site systeemrol die communiceert met een server waarop de registratie service voor netwerk apparaten (NDES) wordt uitgevoerd. Deze rol beheert certificaat aanvragen voor apparaten die gebruikmaken van de Simple Certificate Enrollment Protocol (SCEP). Deze rol wordt alleen op primaire sites en op de centrale beheersite ondersteund.

Hoewel een enkel certificaat registratiepunt functionaliteit kan bieden voor een gehele hiërarchie, kunt u meerdere exemplaren van deze rol op een site en op meerdere sites in dezelfde hiërarchie installeren. Dit ontwerp helpt bij de taak verdeling. Als er meerdere exemplaren bestaan in een hiërarchie, worden clients willekeurig toegewezen aan een certificaatregistratiepunt.  

Elk certificaat registratiepunt vereist toegang tot een afzonderlijk NDES-exemplaar. U kunt niet twee of meer certificaat registratiepunt configureren voor het gebruik van hetzelfde NDES-exemplaar. Installeer het certificaat registratiepunt bovendien niet op dezelfde server waarop NDES wordt uitgevoerd.  

### <a name="cloud-management-gateway-connection-point"></a>Verbindings punt van de Cloud beheer gateway

Een site systeemrol voor het communiceren met de [Cloud beheer gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md).  

### <a name="data-warehouse-service-point"></a>Data Warehouse-service punt

Gebruik het Data Warehouse-service punt om historische gegevens op lange termijn in uw Configuration Manager omgeving op te slaan en te rapporteren. Zie [Data Warehouse](../../servers/manage/data-warehouse.md)voor meer informatie.  

### <a name="distribution-point"></a>Distributiepunt

Een site systeemrol die bron bestanden bevat die clients kunnen downloaden, bijvoorbeeld:

- Toepassings inhoud
- Software pakketten
- Software-updates
- Installatiekopieën van het besturingssysteem
- Installatiekopieën  

Deze functie wordt standaard op de site server geïnstalleerd wanneer u een nieuwe primaire of secundaire site installeert. Deze rol wordt niet ondersteund op een centrale beheer site. Meerdere exemplaren van deze rol op een ondersteunde site en op meerdere sites in dezelfde hiërarchie installeren. Zie [basis concepten voor inhouds beheer](fundamental-concepts-for-content-management.md)en [inhoud en infra structuur](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)voor inhoud beheren voor meer informatie.  

### <a name="endpoint-protection-point"></a>Endpoint Protection-punt

Een site systeemrol die Configuration Manager gebruikt voor het accepteren van de Endpoint Protection licentie voorwaarden en het configureren van het standaard lidmaatschap voor Cloud Protection Service. Een hiërarchie ondersteunt slechts één exemplaar van deze rol, en die moet zich op de site op het hoogste niveau bevindt. Als u een zelfstandige primaire site uitbreidt naar een grotere hiërarchie, verwijdert u deze rol van de primaire site en installeert u deze op de centrale beheer site. Zie [Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-protection.md)voor meer informatie.  

### <a name="enrollment-point"></a>Inschrijvingspunt

Een site systeemrol die PKI-certificaten gebruikt voor Configuration Manager voor het inschrijven van mobiele apparaten en macOS-computers. Hoewel deze rol alleen op primaire sites wordt ondersteund, kunt u meerdere exemplaren van deze rol op een site of op meerdere sites in dezelfde hiërarchie installeren.  

Als een gebruiker mobiele apparaten inschrijft met behulp van Configuration Manager en het Active Directory account van de gebruiker zich in een forest bevindt dat niet wordt vertrouwd door het forest van de site server, installeert u een inschrijvings punt in het forest van de gebruiker. Vervolgens kan Configuration Manager de gebruiker verifiëren.  

### <a name="enrollment-proxy-point"></a>Proxypunt voor inschrijving

Een site systeemrol die Configuration Manager inschrijvings aanvragen van mobiele apparaten en macOS-computers beheert. Hoewel deze rol alleen op primaire sites wordt ondersteund, kunt u meerdere exemplaren van deze rol op een site of op meerdere sites in dezelfde hiërarchie installeren.  

Wanneer u mobiele apparaten op het internet ondersteunt, installeert u een proxy punt voor inschrijving in een perimeter netwerk en installeert u er een op het intranet.

### <a name="exchange-server-connector"></a>Exchange Server-connector

Zie [mobiele apparaten beheren met Configuration Manager en Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)voor meer informatie over deze functie.  

### <a name="fallback-status-point"></a>Terugvalstatuspunt

Een site systeemrol waarmee u de client installatie kunt controleren. Hiermee worden clients geïdentificeerd die niet beheerd zijn omdat ze niet kunnen communiceren met hun beheer punt. Hoewel deze rol alleen op primaire sites wordt ondersteund, kunt u meerdere exemplaren van deze rol op een site en op meerdere sites in dezelfde hiërarchie installeren.

### <a name="management-point"></a>Beheerpunt

Een site systeemrol die beleid en service locatie-informatie biedt aan clients. Er worden ook configuratie gegevens van clients ontvangen.  

Deze functie wordt standaard op de site server geïnstalleerd wanneer u een nieuwe primaire of secundaire site installeert. Primaire sites ondersteunen meerdere exemplaren van deze rol. Secundaire sites ondersteunen één beheer punt. Deze functie wordt ook wel een proxy beheer punt genoemd en biedt een lokaal contact punt voor clients om computer-en gebruikers beleid te verkrijgen.  

Stel beheer punten in voor de ondersteuning van HTTP of HTTPs. Ze kunnen ook mobiele apparaten ondersteunen die u beheert met Configuration Manager on-premises Mobile Device Management (MDM). Gebruik [database replica's voor beheer punten](../../servers/deploy/configure/database-replicas-for-management-points.md)om te voor komen dat de verwerkings belasting op de site database server wordt gereduceerd door beheer punten als service aanvragen van clients.  

### <a name="reporting-services-point"></a>Reporting Services-punt

Een site systeemrol die met SQL Server Reporting Services kan worden geïntegreerd om rapporten voor Configuration Manager te maken en te beheren. Deze rol wordt ondersteund op primaire sites en de centrale beheer site, en u kunt meerdere exemplaren van deze rol op een ondersteunde site installeren. Zie [planning for reporting](../../servers/manage/planning-for-reporting.md)(Engelstalig) voor meer informatie.  

### <a name="service-connection-point"></a>Serviceverbindingspunt

Een site systeemrol die gebruiks gegevens van uw site uploadt en is vereist om updates voor Configuration Manager beschikbaar te maken in de-console. Een hiërarchie ondersteunt slechts één exemplaar van deze rol, en die moet zich op de bovenste site van uw hiërarchie bevindt. Als u een zelfstandige primaire site uitbreidt naar een grotere hiërarchie, verwijdert u deze rol van de primaire site en installeert u deze op de centrale beheer site. Zie [about the Service Connection Point](../../servers/deploy/configure/about-the-service-connection-point.md)(Engelstalig) voor meer informatie.  

### <a name="software-update-point"></a>Software-updatepunt

Een site systeemrol die met Windows Server Update Services (WSUS) integreert om software-updates te leveren aan Configuration Manager-clients. Deze rol wordt ondersteund op alle sites:  

- Installeer dit site systeem op de centrale beheer site om te synchroniseren met WSUS.  

- Stel elk exemplaar van deze rol in op onderliggende primaire sites om te synchroniseren met de centrale beheer site.  

- Wanneer gegevens overdracht over het netwerk traag is, kunt u een software-update punt installeren op secundaire sites.  

Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md)voor meer informatie.  

### <a name="state-migration-point"></a>Statusmigratiepunt

Wanneer u een computer naar een nieuw besturings systeem migreert, slaat deze site systeemrol gebruikers status gegevens op. Deze rol wordt ondersteund op primaire sites en op secundaire sites. Meerdere exemplaren van deze rol op een site en op meerdere sites in dezelfde hiërarchie installeren. Zie [gebruikers status beheren](../../../osd/get-started/manage-user-state.md)voor meer informatie over het opslaan van de gebruikers status bij het implementeren van een besturings systeem.  


## <a name="next-steps"></a>Volgende stappen

Sommige Configuration Manager site systeem rollen vereisen verbindingen met het internet. Als uw omgeving Internet verkeer vereist voor het gebruik van een proxy server, configureert u deze site systeem rollen om de proxy te gebruiken. Zie [ondersteuning voor proxy server](../network/proxy-server-support.md)voor meer informatie.  
