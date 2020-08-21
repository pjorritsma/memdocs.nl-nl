---
title: Objecten migreren
titleSuffix: Configuration Manager
description: Meer informatie over het plannen van de migratie van objecten tussen hiërarchieën in een Configuration Manager huidige branch-omgeving.
ms.date: 01/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 996cff4b8b333a59b774afb979bbdd89aae536a1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692890"
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-configuration-manager-current-branch"></a>Plannen voor de migratie van Configuration Manager objecten naar Configuration Manager huidige vertakking

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met Configuration Manager current branch kunt u veel van de verschillende objecten migreren die zijn gekoppeld aan verschillende functies die op een bron site zijn gevonden.

##  <a name="plan-to-migrate-software-updates"></a><a name="Plan_migrate_Software_updates"></a> Migratie van software-updates plannen  
 U kunt software-update objecten migreren, zoals software-update pakketten en software-update-implementaties.  

 Om software-update objecten met succes te migreren, moet u eerst uw doel hiërarchie instellen met configuraties die overeenkomen met uw bron hiërarchie omgeving. Dit vereist de volgende acties:  

-   Een actief software-update punt in de doel hiërarchie implementeren  

-   De catalogus met producten en talen zo instellen dat deze overeenkomt met de configuratie van uw bron hiërarchie  

-   Het software-update punt in de doel hiërarchie synchroniseren met Windows Server Update Services (WSUS)  

Overweeg, als u software-updates migreert, het volgende:  

-   De migratie van software-update objecten kan mislukken wanneer u geen gesynchroniseerde informatie hebt in uw doel hiërarchie zodat deze overeenkomt met de configuratie van uw bron hiërarchie.  

    > [!WARNING]  
    >  Configuration Manager biedt geen ondersteuning voor het gebruik van het hulp programma WSUSutil om gegevens te synchroniseren tussen een bron-en doel hiërarchie.  

-   U kunt geen aangepaste updates migreren die gepubliceerd zijn door gebruik te maken van System Center Updates Publisher. Aangepaste updates moeten in plaats daarvan opnieuw worden gepubliceerd naar de doelhiërarchie.  

Wanneer u migreert vanaf een Configuration Manager 2007-bron hiërarchie, wijzigt het migratie proces sommige software-update objecten in de indeling die wordt gebruikt door de doel hiërarchie. Gebruik de volgende tabel om u te helpen bij het plannen van de migratie van software-update objecten van Configuration Manager 2007.  

|Configuration Manager 2007-object|Objectnaam na migratie|  
|-----------------------------------|---------------------------------|  
|Lijsten met software-updates|Lijsten met software-updates worden geconverteerd naar software-updategroepen.|  
|Software-update-implementaties|Software-update-implementaties worden omgezet in implementaties en groepen bijwerken.<br /><br /> Nadat u een software-update-implementatie van Configuration Manager 2007 hebt gemigreerd, moet u deze inschakelen in de doel hiërarchie voordat u deze kunt implementeren.|  
|Software-updatepakketten|Software-updatepakketten blijven software-updatepakketten.|  
|Software-update-sjablonen|Software-update sjablonen blijven sjablonen voor software-update.<br /><br /> De waarde **duration** in Configuration Manager 2007-implementatie sjablonen wordt niet gemigreerd.|  

Wanneer u objecten migreert vanuit een System Center 2012-Configuration Manager of Configuration Manager huidige branch-bron hiërarchie, worden de software-update objecten niet gewijzigd.  

##  <a name="plan-to-migrate-content"></a><a name="Plan_Migrate_content"></a> Migratie van inhoud plannen  
 U kunt inhoud migreren vanaf een ondersteunde bronhiërarchie naar uw doelhiërarchie. Voor een Configuration Manager 2007-bron hiërarchie omvat deze inhoud software distributie pakketten en Program ma's en virtuele toepassingen, zoals micro soft Application Virtualization (app-V). Voor System Center 2012 Configuration Manager en Configuration Manager huidige branch-bron hiërarchieën bevat deze inhoud toepassingen en app-V virtuele toepassingen. Wanneer u inhoud migreert tussen hiërarchieën, worden de gecomprimeerde bron bestanden gemigreerd naar de doel hiërarchie.  

### <a name="packages-and-programs"></a>Pakketten en programma's  
 Wanneer u pakketten en programma's migreert, worden ze niet gewijzigd door migratie. Voordat u deze migreert, moet u echter elk pakket zo instellen dat een UNC-pad (Universal Naming Convention) wordt gebruikt voor de bron bestands locatie. Als onderdeel van de configuratie van pakketten en programma's, moet u een site toewijzen in de doelhiërarchie om deze inhoud te beheren. De inhoud wordt niet gemigreerd vanaf de toegewezen site, maar na de migratie krijgt de toegewezen site toegang tot de oorspronkelijke bron bestands locatie door gebruik te maken van de UNC-toewijzing.  

 Nadat u een pakket en programma naar de doel hiërarchie hebt gemigreerd en de migratie van de bron hiërarchie actief blijft, kunt u de inhoud beschikbaar maken voor clients in die hiërarchie met behulp van een gedeeld distributie punt. Om een gedeeld distributiepunt te gebruiken, moet de inhoud beschikbaar blijven op het distributiepunt op de bronsite. Zie [distributie punten tussen bron-en doel hiërarchieën delen](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [een strategie voor de migratie van een inhouds implementatie plannen](../../core/migration/planning-a-content-deployment-migration-strategy.md)voor meer informatie over gedeelde distributie punten.  

 Voor inhoud die is gemigreerd, hebben clients geen toegang meer tot de inhoud van het gedeelde distributie punt in de doel hiërarchie als de inhouds versie wordt gewijzigd in de bron hiërarchie of de doel hiërarchie. In dit scenario moet u de inhoud opnieuw migreren om een consistente versie van het pakket te herstellen tussen de bron hiërarchie en de doel hiërarchie. Deze gegevens worden gesynchroniseerd tijdens de gegevens verzamelings cyclus.  

> [!TIP]  
>  Voor elk pakket dat u migreert, werkt u het pakket bij in de doelhiërarchie. Met deze actie kunnen problemen met de implementatie van het pakket op distributiepunten in de doelhiërarchie worden voorkomen. Wanneer u echter een pakket bijwerkt op het distributie punt in de doel hiërarchie, kunnen clients in die hiërarchie dat pakket niet meer ophalen van een gedeeld distributie punt. Als u een pakket wilt bijwerken in de doel hiërarchie, gaat u in de Configuration Manager-console naar de software bibliotheek, klikt u met de rechter muisknop op het pakket en selecteert u vervolgens **distributie punten bijwerken**. Voer deze actie uit voor elk pakket dat u migreert.  

> [!TIP]  
> Pakket conversie beheer gebruiken om pakketten en Program ma's te converteren naar Configuration Manager-toepassingen. Zie [package Conversion Manager](../../apps/pcm/package-conversion-manager.md)voor meer informatie.  

### <a name="virtual-applications"></a>Virtuele toepassingen  
Wanneer u app-V-pakketten migreert vanaf een ondersteunde Configuration Manager 2007-site, worden deze door het migratie proces geconverteerd naar toepassingen in de doel hiërarchie. Daarnaast worden de volgende implementatie typen gemaakt in de doel hiërarchie, gebaseerd op bestaande advertenties voor het app-V-pakket:  

-   Indien er geen advertenties zijn, wordt één implementatietype gecreëerd dat de standaard implementatietype-instellingen gebruikt.  

-   Als er één advertentie bestaat, wordt één implementatie type gemaakt dat dezelfde instellingen gebruikt als de Configuration Manager 2007-aankondiging.  

-   Als er meerdere advertenties bestaan, wordt er voor elke Configuration Manager 2007 advertisement een implementatie type gemaakt met behulp van de instellingen voor die aankondiging.  

> [!IMPORTANT]  
>  Als u een eerder gemigreerd Configuration Manager 2007 app-V-pakket migreert, mislukt de migratie omdat virtuele toepassings pakketten het overschrijvings gedrag van migratie niet ondersteunen. In dit scenario moet u het gemigreerde virtuele toepassingspakket wissen van de doelhiërarchie en dan een nieuwe migratietaak maken om de virtuele toepassing te migreren.  

> [!NOTE]  
>  Nadat u een app-V-pakket hebt gemigreerd, kunt u de wizard inhoud bijwerken gebruiken om het bronpad voor implementatie typen van app-V te wijzigen. Zie implementatie typen beheren in [Beheer taken voor Configuration Manager-toepassingen](../../apps/deploy-use/management-tasks-applications.md)voor meer informatie over het bijwerken van inhoud voor een implementatie type.  

Wanneer u migreert van een System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron hiërarchie, kunt u naast app-V-implementatie typen en-toepassingen objecten migreren voor de virtuele app-V-omgeving. Zie [virtuele toepassingen van App-v implementeren](../../apps/get-started/deploying-app-v-virtual-applications.md)voor meer informatie over app-v-omgevingen.  

### <a name="advertisements"></a>Aankondigingen  
U kunt advertenties migreren vanaf een ondersteunde Configuration Manager 2007-bron site naar de doel hiërarchie door gebruik te maken van migratie op basis van verzamelingen. Indien u een client updatet, behoudt hij de geschiedenis van eerder uitgevoerde advertenties om te voorkomen dat de client opnieuw gemigreerde advertenties uitvoert.  

> [!NOTE]  
>  U kunt advertenties voor virtuele pakketten niet migreren. Dit is een uitzondering voor het migreren van advertenties.  

### <a name="applications"></a>Toepassingen  
 U kunt toepassingen migreren van een ondersteund System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron hiërarchie naar een doel hiërarchie. Indien u een client opnieuw toewijst vanaf een bronhiërarchie naar de doelhiërarchie, behoudt de client de geschiedenis van voordien geïnstalleerde toepassingen om te voorkomen dat de client opnieuw een gemigreerde toepassing uitvoert.  

##  <a name="plan-to-migrate-collections"></a><a name="BKMK_MigrateCollections"></a> Migratie van verzamelingen plannen  
 U kunt de criteria voor verzamelingen migreren vanuit een ondersteund System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron hiërarchie. Hiervoor gebruikt u een migratie taak op basis van een object. Wanneer u een verzameling migreert, migreert u de regels voor de verzameling en niet informatie over de leden van de verzameling of informatie of objecten gerelateerd tot leden van de verzameling.  

 Migratie van het verzamelings object wordt niet ondersteund wanneer u migreert vanaf een Configuration Manager 2007-bron hiërarchie.  

##  <a name="plan-to-migrate-operating-system-deployments"></a><a name="Plan_migrate_OSD"></a> Migratie van implementaties van besturings systemen plannen  
U kunt de volgende implementatieobjecten van besturingssystemen migreren vanaf een ondersteunde bronhiërarchie:  

-   Installatiekopieën van besturingssystemen en pakketten. Het bronpad van opstart installatie kopieën wordt bijgewerkt naar de standaard locatie van de installatie kopie voor de Windows-beheer installatie kit (Windows AIK) op de doel site. Het volgende zijn vereisten en beperking voor het migreren van besturingssystemen en pakketten:  

    -   Om installatie kopie bestanden met succes te migreren, moet het computer account van de server van de SMS-provider voor de site op het hoogste niveau van de doel hiërarchie **Lees** -en **Schrijf** machtigingen hebben voor de installatie kopie bron bestanden van de Windows AIK-locatie van de bron site.  

    -   Wanneer u een installatie pakket voor een besturings systeem migreert, moet u ervoor zorgen dat de configuratie van het pakket op de bron site wijst naar de map die het WIM-bestand bevat en niet naar het WIM-bestand zelf. Indien het installatiepakket wijst naar het WIM-bestand, zal de migratie van het installatiepakket falen.  

    -   Wanneer u een opstart installatie kopie pakket migreert vanaf een Configuration Manager 2007-bron site, wordt de pakket-ID van het pakket niet behouden in de doel site. Het resultaat hiervan is dat clients in de doelhiërarchie geen opstartinstallatiekopieën kunnen gebruiken die beschikbaar zijn op gedeelde distributiepunten.  

-   Takenreeksen. Wanneer u een taken reeks migreert die verwijst naar een client installatie pakket, wordt deze verwijzing vervangen door een verwijzing naar het client installatie pakket van de doel hiërarchie.  

    > [!NOTE]  
    >  Wanneer u een taken reeks migreert, kan Configuration Manager mogelijk objecten migreren die niet vereist zijn in de doel hiërarchie. Deze objecten bevatten opstart installatie kopieën en Configuration Manager 2007-client installatie pakketten.  

-   Stuurprogramma's en stuurprogrammapakketten. Wanneer u stuur programmapakketten migreert, moet het computer account van de SMS-provider in de doel hiërarchie volledig beheer hebben over de pakket bron.

##  <a name="plan-to-migrate-desired-configuration-management"></a><a name="Plan_Migrate_Compliance_settings"></a> Migratie van Desired Configuration Management plannen  
U kunt de configuratie-items en configuratiebasislijnen migreren.  

> [!NOTE]  
>  Niet-geïnterpreteerde configuratie-items van Configuration Manager 2007-bron hiërarchieën worden niet ondersteund voor migratie. U kunt deze configuratie-items niet migreren of importeren naar de doelhiërarchie. Voor meer informatie over niet-geïnterpreteerde configuratie-items raadpleegt u niet-geïnterpreteerde configuratie-items in het onderwerp [over configuratie-items in desired Configuration Management](/previous-versions/system-center/configuration-manager-2007/bb694136(v=technet.10)#uninterpreted-configuration-item) in de documentatie bibliotheek van Configuration Manager 2007.  

U kunt Configuration Manager 2007-configuratie pakketten importeren. Tijdens het import proces worden de configuratie pakketten automatisch geconverteerd zodat deze compatibel zijn met Configuration Manager huidige vertakking.  

##  <a name="plan-to-migrate-boundaries"></a><a name="Plan_migrate_Boundaries"></a> Migratie van grenzen plannen  
 U kunt grenzen tussen hiërarchieën migreren. Wanneer u grenzen migreert vanaf Configuration Manager 2007, wordt elke grens van de bron site tegelijk gemigreerd en wordt deze toegevoegd aan een nieuwe grens groep die in de doel hiërarchie wordt gemaakt. Wanneer u grenzen migreert van een System Center 2012-Configuration Manager of Configuration Manager huidige branch-hiërarchie, wordt elke door u geselecteerde grens toegevoegd aan een nieuwe grens groep in de doel hiërarchie.  

 Voor elke automatisch gemaakte grensgroep is locatie van inhoud ingeschakeld, maar niet sitetoewijzing. Hiermee wordt voorkomen dat grenzen voor sitetoewijzing tussen de bron- en doelhiërarchieën elkaar overlappen. Wanneer u migreert vanaf een Configuration Manager 2007-bron site, kunt u hiermee voor komen dat nieuwe Configuration Manager 2007-clients die worden geïnstalleerd, onjuist worden toegewezen aan de doel hiërarchie. Configuration Manager huidige branch-clients worden standaard niet automatisch toegewezen aan Configuration Manager 2007-sites.  

 Als u tijdens de migratie een distributiepunt deelt met de doelhiërarchie, migreren aan dit distributiepunt gekoppelde grenzen automatisch naar de doelhiërarchie. In de doel hiërarchie maakt migratie een nieuwe alleen-lezen grens groep voor elk gedeeld distributie punt. Als u de grenzen van het distributiepunt in de bronhiërarchie wijzigt, wordt de grensgroep in de doelhiërarchie tijdens de volgende gegevensverzamelingscyclus bijgewerkt met deze wijzigingen.  

##  <a name="plan-to-migrate-reports"></a><a name="Plan_Migrate_reports"></a> De migratie van rapporten plannen  
Configuration Manager biedt geen ondersteuning voor de migratie van rapporten. In plaats daarvan kunt u met SQL Server Reporting Services Report Builder rapporten uit de bronhiërarchie exporteren en vervolgens in de doelhiërarchie importeren.  

> [!NOTE]  
>  Omdat er schema wijzigingen zijn in rapporten tussen Configuration Manager 2007 en Configuration Manager huidige vertakking, test u elk rapport dat u importeert uit een Configuration Manager 2007-hiërarchie, om ervoor te zorgen dat het werkt zoals verwacht.  

Zie [Introduction to Reporting](../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over rapportage.  

##  <a name="plan-to-migrate-organizational-and-search-folders"></a><a name="Plan_Migrate_Org_Folders"></a> De migratie van organisatie-en zoek mappen plannen  
 U kunt organisatorische mappen en zoekmappen vanuit een ondersteunde bronhiërarchie naar een doelhiërarchie migreren. Daarnaast kunt u vanuit een System Center 2012-Configuration Manager of Configuration Manager huidige branch-bron hiërarchie de criteria voor een opgeslagen zoek opdracht naar een doel hiërarchie migreren.  

 Wanneer u migreert, wordt in het migratieproces standaard de structuur van uw zoekmap en beheermap gehandhaafd voor objecten en verzamelingen. U kunt in de wizard Migratie taak maken op de pagina **instellingen** echter een migratie taak instellen om de organisatie structuur voor objecten niet te migreren, door het selectie vakje voor deze optie uit te vinken. De organisatiestructuren van verzamelingen worden altijd gehandhaafd.  

 Een uitzondering hierop is een zoekmap met virtuele toepassingen. Wanneer een app-V-pakket wordt gemigreerd, wordt het app-V-pakket omgezet in een toepassing in Configuration Manager. Na de migratie van de zoekmap zijn alleen de resterende pakketten gevonden. de zoekmap kan geen app-V-pakket vinden vanwege deze conversie naar een toepassing wanneer het app-V-pakket wordt gemigreerd.  

 Wanneer u een opgeslagen zoek opdracht van een System Center 2012-Configuration Manager of Configuration Manager huidige branch-bron hiërarchie migreert, migreert u de criteria voor de zoek opdracht en niet de informatie over de zoek resultaten. De migratie van een opgeslagen zoek opdracht is niet van toepassing op een Configuration Manager 2007-bron site.  

##  <a name="plan-to-migrate-asset-intelligence-customizations"></a><a name="Plan_Migrate_AI"></a> Migratie van Asset Intelligence aanpassingen plannen  
 U kunt aanpassingen voor Asset Intelligence vanuit een ondersteunde bronhiërarchie naar een doelhiërarchie migreren. Er zijn geen belang rijke wijzigingen aangebracht in de structuur van Asset Intelligence aanpassingen tussen Configuration Manager 2007 en Configuration Manager huidige vertakking.  

> [!NOTE]  
> Configuration Manager current branch biedt geen ondersteuning voor de migratie van Asset Intelligence-objecten van een Configuration Manager 2007-site die Asset Intelligence Service 2,0 (AIS 2,0) gebruikt.  

##  <a name="plan-to-migrate-software-metering-rules-customizations"></a><a name="Plan_Migrate_SWM_Rules"></a> Planning voor het migreren van aanpassingen van de software meter regels  
 Er zijn geen belang rijke wijzigingen in software meter tussen Configuration Manager 2007 en Configuration Manager huidige branch. U kunt uw regels voor softwarelicentiecontrole vanuit een ondersteunde bronhiërarchie naar een doelhiërarchie migreren.  

 Standaard worden de door u naar een doelhiërarchie gemigreerde regels voor softwarelicentiecontrole niet aan een specifieke site in de doelhiërarchie gekoppeld en zijn daarentegen van toepassing op alle clients in de hiërarchie. Wanneer u een regel voor softwarelicentiecontrole wilt laten gelden voor clients op een specifieke site, moet u de regel voor softwarelicentiecontrole bewerken na de migratie ervan.