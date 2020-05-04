---
title: Site systeem rollen voor clients
titleSuffix: Configuration Manager
description: Bepaal de site systeem rollen voor clients in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713245"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>De site systeem rollen voor Configuration Manager clients bepalen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Aan de hand van dit artikel kunt u bepalen welke site systeem rollen u nodig hebt om Configuration Manager-clients te implementeren.

Zie [een hiërarchie van sites ontwerpen](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md)voor meer informatie over waar u deze rollen in de hiërarchie kunt installeren.  

Zie [site systeem rollen installeren](../../../servers/deploy/configure/install-site-system-roles.md)voor meer informatie over het installeren en configureren van deze rollen.  

## <a name="management-point"></a>Beheerpunt

Standaard gebruiken alle Windows-client computers een distributie punt om de Configuration Manager-client te installeren. Ze kunnen terugvallen op een beheer punt wanneer een distributie punt niet beschikbaar is. U kunt echter Windows-clients op computers vanaf een andere bron installeren wanneer u de CCMSetup-opdracht regel eigenschap `/source:<Path>`gebruikt. U kunt deze actie bijvoorbeeld uitvoeren als u clients installeert op internet. Een ander scenario is wanneer u wilt voor komen dat er netwerk pakketten worden verzonden tussen de computer en het beheer punt tijdens de client installatie. Dit scenario is omdat een firewall de vereiste poorten blokkeert of omdat u een verbinding met een lage band breedte hebt. Alle clients moeten echter communiceren met een beheer punt om aan een site toe te wijzen en door Configuration Manager te worden beheerd.  

Zie [over eigenschappen van client installatie](../about-client-installation-properties.md)voor meer informatie over de opdracht regel eigenschappen van de client.  

Wanneer u meer dan één beheer punt in de-hiërarchie installeert, maken clients automatisch verbinding met één punt op basis van hun Forest-lidmaatschap en netwerk locatie. U kunt niet meer dan één beheer punt op een secundaire site installeren.  

Clients voor Mac-computers en mobiele apparaten die u registreert met Configuration Manager, vereisen altijd een beheer punt voor client installatie. Dit beheer punt moet zich in een primaire site betreden, moet worden geconfigureerd voor de ondersteuning van mobiele apparaten en moet client verbindingen van het Internet accepteren. Deze clients kunnen geen beheer punten gebruiken in secundaire sites of verbinding maken met beheer punten in andere primaire sites.  

## <a name="distribution-point"></a>Distributiepunt

U hebt geen distributie punt nodig om Configuration Manager-clients op Windows-computers te installeren. Configuration Manager maakt standaard gebruik van een distributie punt om de client bron bestanden op Windows-computers te installeren. Dit kan terugvallen op het downloaden van deze bestanden vanaf een beheer punt. Distributie punten worden niet gebruikt voor het installeren van clients voor mobiele apparaten die zijn Inge schreven door Configuration Manager, maar worden gebruikt als u de verouderde client voor mobiele apparaten installeert. Als u de Configuration Manager-client installeert als onderdeel van een besturingssysteem implementatie, wordt de installatie kopie van het besturings systeem opgeslagen en opgehaald van een distributie punt.

Hoewel u mogelijk geen distributie punten nodig hebt om de meeste Configuration Manager-clients te installeren, moet u de software installeren, zoals toepassingen en software-updates op de clients.  

## <a name="fallback-status-point"></a>Terugvalstatuspunt

U kunt een terugval status punt gebruiken voor het bewaken van client implementatie voor Windows-computers. U kunt ook de Windows-computer clients identificeren die niet-beheerd zijn omdat ze niet kunnen communiceren met een beheer punt.

De volgende client typen gebruiken geen terugval status punt:

- Mac-computers
- Mobiele apparaten die zijn Inge schreven door Configuration Manager
- Mobiele apparaten die worden beheerd met behulp van de Exchange Server-connector

Een terugval status punt is niet vereist voor het bewaken van client activiteiten en client status.  

Het terugval status punt communiceert altijd met clients via HTTP, waarbij niet-geverifieerde verbindingen worden gebruikt en gegevens worden verzonden als ongecodeerde tekst. Dit gedrag zorgt ervoor dat het terugval status punt kwetsbaar is voor aanvallen, met name wanneer het wordt gebruikt met client beheer op internet. U kunt de kwets baarheid verminderen door altijd een server toe te wijzen voor het uitvoeren van het terugval status punt. Installeer geen andere site systeem rollen op dezelfde server in een productie omgeving.  

Installeer een terugval status punt als aan alle volgende voor waarden wordt voldaan:  

- U wilt dat client communicatie fouten van Windows-computers worden verzonden naar de site, zelfs als deze client computers niet kunnen communiceren met een beheer punt.  

- U wilt de Configuration Manager client implementatie rapporten gebruiken, waarin de gegevens worden weer gegeven die worden verzonden met het terugval status punt.  

- U hebt een dedicated server voor deze site systeemrol en u hebt aanvullende beveiligings maatregelen om de server te beschermen tegen aanvallen.  

- De voor delen van het gebruik van een terugval status punt wegen alle beveiligings Risico's die zijn gekoppeld aan niet-geverifieerde verbindingen en duidelijke tekst overdracht via HTTP-verkeer.  

Installeer geen terugval status punt als de beveiligings Risico's van het uitvoeren van een website met niet-geverifieerde verbindingen en heldere tekst overdracht zwaarder zijn dan de voor delen van het identificeren van client communicatie problemen.  

## <a name="reporting-services-point"></a>Reporting Services-punt

Configuration Manager biedt veel rapporten waarmee u de installatie, toewijzing en het beheer van clients in de Configuration Manager-console kunt bewaken. Voor sommige client implementatie rapporten moeten clients zijn toegewezen aan een terugval status punt.  

De rapporten zijn niet nodig voor het implementeren van-clients. U kunt bepaalde implementatie gegevens bekijken in de Configuration Manager-console of de logboek bestanden van de client gebruiken voor gedetailleerde informatie. De client rapporten bieden echter waardevolle informatie voor het bewaken en oplossen van problemen met de client implementatie.  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>Registratiepunt en proxypunt voor registratie

Configuration Manager vereist het inschrijvings punt en het inschrijvings proxy punt om mobiele apparaten in te schrijven en om certificaten voor Mac-computers in te schrijven. U hebt deze site systeem rollen niet nodig in de volgende situaties:

- U van plan bent mobiele apparaten te beheren met de Exchange Server-connector
- U installeert de verouderde client voor mobiele apparaten, bijvoorbeeld voor Windows CE
- U vraagt en installeert het client certificaat op Mac-computers onafhankelijk van Configuration Manager

## <a name="application-catalog"></a>Toepassings catalogus

> [!Important]  
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>Cloud beheer gateway-connector punt

U hebt een verbindings punt voor de Cloud beheer gateway nodig als u een [Cloud beheer gateway](../../manage/cmg/plan-cloud-management-gateway.md) instelt voor [het beheren van clients op Internet](../../manage/manage-clients-internet.md).
