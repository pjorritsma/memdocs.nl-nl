---
title: Client migratie plannen
titleSuffix: Configuration Manager
description: Meer informatie over de taken waarmee clients van een bron hiërarchie worden gemigreerd naar een Configuration Manager huidige vertakkings doel hiërarchie.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c0885cab43deacf7e7f487e5c20e171f6475b302
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720910"
---
# <a name="plan-a-client-migration-strategy-in-configuration-manager"></a>Een strategie voor client migratie plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u clients wilt migreren van de bron hiërarchie naar een Configuration Manager huidige vertakkings doel hiërarchie, moet u twee taken uitvoeren. U dient de objecten te migreren die aan de client zijn gekoppeld en vervolgens de clients opnieuw installeren of toewijzen van de bronhiërarchie aan de doelhiërarchie. U migreert eerst de objecten zodat ze beschikbaar zijn wanneer de clients worden gemigreerd. De objecten die aan de client zijn gekoppeld worden gemigreerd met behulp van migratietaken. Zie [een strategie voor migratie taken plannen](../../core/migration/planning-a-migration-job-strategy.md)voor meer informatie over het migreren van de objecten die aan de client zijn gekoppeld.  

 Gebruik de volgende rubrieken om de migratie van clients naar de doelhiërarchie te plannen.  

-   [De migratie van clients naar de doel hiërarchie plannen](#Planning_for_Client_Agent_Migration)  

-   [De verwerking van gegevens die op de clients achterblijven tijdens de migratie plannen](#Planning_for_Client_Data_Migration)  

-   [De inventaris-en compatibiliteits gegevens tijdens de migratie plannen](#Planning_for_Inventory_data_migration)  

##  <a name="plan-to-migrate-clients-to-the-destination-hierarchy"></a><a name="Planning_for_Client_Agent_Migration"></a> De migratie van clients naar de doelhiërarchie plannen  
 Wanneer u clients migreert vanaf een-bron hiërarchie, wordt de client software op de client computer bijgewerkt zodat deze overeenkomt met de product versie van de doel hiërarchie.  

-   **Een Configuration Manager 2007-bron hiërarchie:** Wanneer u clients migreert vanaf een bron hiërarchie waarop een ondersteunde versie van Configuration Manager wordt uitgevoerd, wordt de client software bijgewerkt naar de client versie voor de doel hiërarchie.  

-   **Een bron hiërarchie van System Center 2012 Configuration Manager of hoger:** Wanneer u clients migreert tussen hiërarchieën die dezelfde product versie hebben, wordt de client software niet gewijzigd of bijgewerkt. In plaats daarvan gebeurt toewijzing van de client van de bronhiërarchie naar een site in de doelhiërarchie.  

    > [!NOTE]  
    >  Als de productversie van een hiërarchie niet wordt ondersteund voor migratie naar uw doelhiërarchie, upgrade alle sites en clients in de bronhiërarchie naar een compatibele productversie. Na het upgraden van de doelhiërarchie naar een ondersteunde productversie, kunt u tussen de hiërarchieën migreren. Zie voor meer informatie [versies van Configuration Manager die worden ondersteund voor migratie](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) in [vereisten voor migratie](../../core/migration/prerequisites-for-migration.md).  

Gebruik de volgende informatie bij het plannen van de clientmigratie:  

-   Voor het upgraden of opnieuw toewijzen van clients van een bronsite naar een doelsite, kunt u iedere implementatiemethode voor clients gebruiken die wordt ondersteund voor het implementeren van clients in de doelhiërarchie. Typische implementatiemethodes voor clients zijn onder andere clientpushinstallaties, softwaredistributie, groepsbeleid en clientinstallaties gebaseerd op softwareupdates. Zie [client installatie methoden](../../core/clients/deploy/plan/client-installation-methods.md)voor meer informatie.  

-   Zorg ervoor dat het apparaat dat de client software uitvoert in de bron hiërarchie voldoet aan de minimale hardwarevereisten en dat er een besturings systeem wordt uitgevoerd dat wordt ondersteund door de versie van Configuration Manager in de doel hiërarchie.  

-   Voordat u een client migreert, voert u een migratie taak uit om de informatie te migreren die de client gaat gebruiken in de doel hiërarchie.  

-   Clients die upgraden, behouden hun uitvoerings geschiedenis voor implementaties. Zo voor komt u dat implementaties onnodig opnieuw worden uitgevoerd in de doel hiërarchie.  

    -   Voor Configuration Manager 2007-clients wordt de geschiedenis van de aankondigings uitvoering bewaard.  

    -   Voor clients van System Center 2012 Configuration Manager of Configuration Manager huidige branch, wordt de implementatie-uitvoerings geschiedenis bewaard.  

-   U kunt clients migreren van sites in de bronhiërarchie in iedere gewenste volgorde. U kunt echter wel een beperkt aantal clients in fasen migreren in plaats van een groot aantal clients tegelijk te migreren. Een gefaseerde migratie legt minder beslag op de netwerkbandbreedte en serververwerking wanneer iedere pas bijgewerkte client zijn initiële inventaris- en compatibiliteitsgegevens naar de toegewezen site verzendt.  

-   Wanneer u Configuration Manager 2007-clients migreert, wordt de bestaande client software verwijderd van de client computer en wordt de nieuwe client software geïnstalleerd.  

-   Configuration Manager kunt een Configuration Manager 2007-client waarop de app-V-client is geïnstalleerd, alleen migreren als de versie van de app-V-client 4,6 SP1 of hoger is.  

U kunt het client migratie proces bewaken in het knoop punt **migratie** van de werk ruimte **beheer** in de Configuration Manager-console.  

Nadat u de client naar de doel hiërarchie hebt gemigreerd, kunt u dat apparaat niet meer beheren met behulp van de bron hiërarchie en kunt u overwegen om de client uit de bron hiërarchie te verwijderen. Hoewel het niet vereist is bij het migreren van hiërarchieën, kan dit helpen bij het voorkomen van de identificatie van een gemigreerde client in een bronhiërarchierapport of een onjuiste telling van bronnen tussen de twee hiërarchieën tijdens de migratie. Wanneer bijvoorbeeld een gemigreerde client achterblijft in de database van de bronsite, kunt u een softwareupdaterapport uitvoeren dat de computer mogelijk onjuist identificeert als een onbeheerde bron wanneer het nu wordt beheerd door de doelhiërarchie.  

##  <a name="plan-to-handle-data-maintained-on-clients-during-migration"></a><a name="Planning_for_Client_Data_Migration"></a>De verwerking van gegevens die op clients worden onderhouden tijdens de migratie plannen  
Bij de migratie van een client van de bronhiërarchie naar de doelhiërarchie, blijven er sommige gegevens achter op het apparaat, terwijl andere informatie niet beschikbaar is op het apparaat na migratie.  

De volgende informatie wordt behouden op het clientapparaat:  

-   De unieke id (GUID) die een client koppelt aan de informatie in de Configuration Manager-Data Base.  

-   De advertentie- of implementatiegeschiedenis, die voorkomt dat clients onnodig advertenties of implementaties opnieuw uitvoeren in de doelhiërarchie.  

De volgende informatie wordt niet behouden op het clientapparaat:  

-   De bestanden in de clientcache. Als de client deze bestanden nodig heeft om software te installeren, downloadt de client deze nogmaals vanaf de doelhiërarchie.  

-   Informatie van de bronhiërarchie over eventuele advertenties of implementaties die nog niet zijn uitgevoerd. Als u wilt dat de client de advertenties of implementaties uitvoert na de migratie, moet u deze opnieuw implementeren op de client in de doelhiërarchie.  

-   Informatie over de inventarisatie. De client zendt deze informatie opnieuw naar de toegewezen site in de doel hiërarchie nadat de client is gemigreerd en de nieuwe client gegevens zijn gegenereerd.  

-   Compatibiliteitsgegevens. De client zendt deze informatie opnieuw naar de toegewezen site in de doel hiërarchie nadat de client is gemigreerd en de nieuwe client gegevens zijn gegenereerd.  

Wanneer een client wordt gemigreerd, wordt de informatie die is opgeslagen in het REGI ster van de Configuration Manager-client en het bestandspad niet behouden. Pas na de migratie deze instellingen opnieuw toe. Standaardinstellingen zijn onder andere:  

-   Energiebeheerschema's  

-   Instellingen voor logboekregistratie  

-   Lokale beleidsinstellingen  

Mogelijk moet u bovendien sommige toepassingen opnieuw installeren.  

##  <a name="plan-for--inventory-and-compliance-data-during-migration"></a><a name="Planning_for_Inventory_data_migration"></a> Planning maken voor de inventaris- en compatibiliteitsgegevens tijdens de migratie  
Clientinventaris- en compatibiliteitsgegevens worden niet opgeslagen wanneer u een client migreert naar de doelhiërarchie. Deze informatie wordt opnieuw gemaakt in de doelhiërarchie wanneer een client zijn informatie voor de eerste keer verzendt naar de toegewezen site. Voor minder belasting op de netwerkbandbreedte en serververwerking is het aan te raden een beperkt aantal clients gefaseerd te migreren in plaats van een groot aantal clients tegelijkertijd.  

 U kunt bovendien geen aanpassingen migreren voor hardware-inventaris van een bronhiërarchie. U moet deze apart van de migratie aanbrengen in de doelhiërarchie. Zie [hardware-inventaris configureren](../../core/clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over het uitbreiden van de hardware-inventarisatie.  
