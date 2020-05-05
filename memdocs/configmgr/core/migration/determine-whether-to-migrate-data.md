---
title: Kies wat u wilt migreren
titleSuffix: Configuration Manager
description: Meer informatie over welke gegevens u kunt migreren en welke gegevens u niet naar Configuration Manager huidige vertakking kan migreren.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b697df41490d1709782561cc59b43684fb60d16
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718915"
---
# <a name="determine-whether-to-migrate-data-to-configuration-manager-current-branch"></a>Bepalen of gegevens naar Configuration Manager huidige vertakking moeten worden gemigreerd

*Van toepassing op: Configuration Manager (huidige vertakking)*

In Configuration Manager huidige vertakking levert migratie een proces voor de overdracht van gegevens en configuraties die u hebt gemaakt op basis van ondersteunde versies van Configuration Manager naar uw nieuwe hiërarchie.  U kunt hiermee het volgende doen:  

-   Meerdere hiërarchieën combi neren tot één.  

-   Gegevens en configuraties verplaatsen van een test implementatie naar uw productie-implementatie.

-   Verplaats gegevens en configuratie van een eerdere versie van Configuration Manager, zoals Configuration Manager 2007, die geen upgradepad heeft naar Configuration Manager current branch, of van System Center 2012 Configuration Manager (wat een upgradepad ondersteunt naar Configuration Manager current branch).  

Met uitzondering van de sitesysteemrol van het distributiepunt en de computers waarop distributiepunten worden gehost, kan er geen infrastructuur (die bestaat uit sites, sitesysteemrollen of computers waarop een sitesysteemrol wordt gehost) worden gemigreerd, overgedragen of gedeeld tussen hiërarchieën.  

 Hoewel u een server infrastructuur niet kunt migreren, kunt u Configuration Manager-clients tussen hiërarchieën migreren. Bij een clientmigratie worden de gegevens die clients gebruiken, gemigreerd van de bronhiërarchie naar de doelhiërarchie. Vervolgens wordt de clientsoftware geïnstalleerd of opnieuw toegewezen, zodat de client vervolgens verslag uitbrengt aan de nieuwe hiërarchie.

Nadat u een client hebt geïnstalleerd op de nieuwe hiërarchie en de client de gegevens verzendt, helpt de unieke Configuration Manager-ID Configuration Manager te koppelen van de gegevens die u eerder hebt gemigreerd met elke client computer.  

 De functionaliteit die wordt geleverd door de migratie helpt u bij het onderhouden van investeringen die u hebt gemaakt in configuraties en implementaties, terwijl u optimaal kunt profiteren van belang rijke wijzigingen in het product (dat voor het eerst werd geïntroduceerd in System Center 2012 Configuration Manager en vervolgens in Configuration Manager). Deze wijzigingen omvatten een vereenvoudigde Configuration Manager-hiërarchie waarin minder sites en bronnen worden gebruikt, en de verbeterde verwerking die afkomstig is van het gebruik van systeem eigen 64-bits code die wordt uitgevoerd op 64-bits hardware.  

 Zie [vereisten voor migratie](../../core/migration/prerequisites-for-migration.md)voor informatie over de versies van Configuration Manager die door de migratie worden ondersteund.  

## <a name="data-that-you-can-migrate-to-configuration-manager-current-branch"></a><a name="Can_Migrate"></a>Gegevens die u naar Configuration Manager huidige vertakking kunt migreren

Met migratie kunnen de meeste objecten worden gemigreerd tussen ondersteunde Configuration Manager-hiërarchieën. De gemigreerde exemplaren van sommige objecten van een ondersteunde versie van Configuration Manager 2007 moeten worden gewijzigd om te voldoen aan de System Center 2012 Configuration Manager schema-en object indeling.

Deze wijzigingen zijn niet van invloed op de gegevens in de data base van de bron site. Objecten die worden gemigreerd vanuit een ondersteunde versie van System Center 2012 Configuration Manager of Configuration Manager huidige vertakking, hoeven niet te worden gewijzigd.  

Hieronder vindt u objecten die kunnen worden gemigreerd op basis van de versie van Configuration Manager in de bron hiërarchie. Sommige objecten, zoals query's, kunnen niet worden gemigreerd. Als u deze objecten die niet kunnen worden gemigreerd, wilt blijven gebruiken, moet u ze opnieuw maken in de nieuwe hiërarchie. Andere objecten, waaronder bepaalde client gegevens, worden automatisch opnieuw gemaakt in de nieuwe hiërarchie wanneer u clients in die hiërarchie beheert.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-configuration-manager-current-branch"></a>Objecten die u kunt migreren vanuit System Center 2012 Configuration Manager of Configuration Manager current branch

-   Toepassingen voor System Center 2012 Configuration Manager en latere versies  

-   Virtuele omgeving van app-V van System Center 2012 Configuration Manager en latere versies  

-   Asset Intelligence-aanpassingen  

-   Grenzen  

-   Verzamelingen: als u verzamelingen wilt migreren vanuit een ondersteunde versie van System Center 2012 Configuration Manager of Configuration Manager huidige branch, gebruikt u een object migratie taak.  

-   Instellingen voor naleving:  

    -   Configuratiebasislijn  

    -   Configuratie-items  

-   Implementaties  

-   Implementatie van besturingssysteem:  

    -   Installatiekopieën  

    -   Driverpakketten  

    -   Stuurprogramma's  

    -   Installatiekopieën  

    -   Pakketten  

    -   Takenreeksen  

-   Zoek resultaten: opgeslagen zoek criteria  

-   Software-updates:  

    -   Implementaties  

    -   Implementatiepakketten  

    -   Sjablonen  

    -   Lijsten met software-updates  

-   Softwaredistributiepakketten  

-   Regels voor softwarelicentiecontrole  

-   Virtuele toepassingspakketten  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Objecten die u kunt migreren vanaf Configuration Manager 2007 SP2

-   Aankondigingen  

-   Toepassingen voor System Center 2012 Configuration Manager en latere versies  

-   Virtuele omgeving van app-V van System Center 2012 Configuration Manager en latere versies  

-   Asset Intelligence-aanpassingen  

-   Grenzen  

-   Verzamelingen: u migreert verzamelingen vanuit een ondersteunde versie van Configuration Manager 2007 met behulp van een migratie taak voor verzamelingen.  

-   Instellingen voor naleving (Desired Configuration Management genoemd in Configuration Manager 2007):  

    -   Configuratiebasislijn  

    -   Configuratie-items  

-   Implementatie van besturingssysteem:  

    -   Installatiekopieën  

    -   Driverpakketten  

    -   Stuurprogramma's  

    -   Installatiekopieën  

    -   Pakketten  

    -   Takenreeksen  

-   Zoek resultaten: Zoek mappen  

-   Software-updates:  

    -   Implementaties  

    -   Implementatiepakketten  

    -   Sjablonen  

    -   Lijsten met software-updates  

-   Softwaredistributiepakketten  

-   Regels voor softwarelicentiecontrole  

-   Virtuele toepassingspakketten  

## <a name="data-that-you-cant-migrate-to-configuration-manager-current-branch"></a><a name="Cannot_migrate"></a>Gegevens die u niet kunt migreren naar Configuration Manager huidige vertakking

U kunt de volgende typen objecten niet migreren:  

-   Inrichtingsgegevens voor een AMT-client  

-   Bestanden op clients, waaronder:  

    -   Inventaris- en geschiedenisgegevens van een client  

    -   Bestanden in de clientcache  

-   Query's  

-   Configuration Manager 2007-beveiligings rechten en-exemplaren voor de site en objecten  

-   Configuration Manager 2007-rapporten van SQL Server Reporting Services  

-   Configuration Manager 2007-webrapporten  

-   System Center 2012 Configuration Manager en Configuration Manager huidige branch-rapporten  

-   System Center 2012 Configuration Manager en Configuration Manager het huidige beheer op basis van rollen:  

    -   Beveiligingsrollen  

    -   Beveiligingsbereiken  
