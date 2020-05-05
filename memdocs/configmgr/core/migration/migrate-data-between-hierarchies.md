---
title: Gegevens migreren
titleSuffix: Configuration Manager
description: Meer informatie over het overdragen van gegevens van een bron hiërarchie naar een Configuration Manager-doel hiërarchie.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a3771011f2822bb93a9569ec534b77259e2e8dc3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718901"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Gegevens migreren tussen hiërarchieën in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik migratie om gegevens over te dragen van een ondersteunde bron hiërarchie naar uw Configuration Manager-doel hiërarchie (current branch). Wanneer u gegevens migreert vanuit een-bron hiërarchie:  

- U opent gegevens van de site databases in de bron infrastructuur en brengt deze gegevens vervolgens over naar uw huidige omgeving.  

- Bij de migratie worden de gegevens in de bron hiërarchie niet gewijzigd. In plaats daarvan worden de gegevens gedetecteerd en wordt er een kopie opgeslagen in de data base van de doel hiërarchie.  

Houd rekening met de volgende punten wanneer u uw migratie strategie plant:  

- U kunt een bestaande Configuration Manager 2007 SP2-infra structuur migreren naar Configuration Manager (current branch).  

- U kunt bepaalde of alle ondersteunde gegevens van een bronsite migreren.  

- U kunt de gegevens van één bronsite migreren naar verschillende sites in de doelhiërarchie.  

- U kunt gegevens van meerdere bronsites verplaatsen naar één site in de doelhiërarchie.  


In de volgende video worden twee algemene [migratie scenario's](#BKMK_MigrationScenarios)besproken en gedemonstreerd. Het bevat ook opties voor het opnemen van Microsoft Azure in migratie plannen.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="concepts"></a><a name="BKMK_MigrationConcepts"></a>Concept  

 Configuration Manager maakt gebruik van de volgende concepten en termen tijdens de migratie.  

#### <a name="source-hierarchy"></a>Bronhiërarchie
Een hiërarchie waarop een ondersteunde versie van Configuration Manager wordt uitgevoerd en die gegevens bevat die u wilt migreren. Wanneer u de migratie instelt, identificeert u de bron hiërarchie wanneer u de site op het hoogste niveau van een bron hiërarchie opgeeft. Nadat u een bronhiërarchie hebt opgegeven, verzamelt de site op het hoogste niveau van de doelhiërarchie gegevens uit de database van de opgegeven bronsite om te bepalen welke gegevens u kunt migreren. 

Zie [bron hiërarchieën](planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies)voor meer informatie.

#### <a name="source-sites"></a>Bronsites
De sites in de bronhiërarchie die gegevens bevatten die u kunt migreren naar uw doelhiërarchie. 

Zie [bron sites](planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites)voor meer informatie.

#### <a name="destination-hierarchy"></a>Doelhiërarchie
Een Configuration Manager-hiërarchie (current branch) waarin de migratie wordt uitgevoerd om gegevens te importeren vanuit een bron hiërarchie.

#### <a name="data-gathering"></a>Gegevens verzamelen
Het continue proces om te ontdekken welke informatie in de bronhiërarchie u kunt migreren naar de doelhiërarchie. Configuration Manager controleert de bron hiërarchie volgens een planning. Dit proces identificeert eventuele wijzigingen in gegevens in de bron hiërarchie die u eerder hebt gemigreerd en die u mogelijk wilt bijwerken in de doel hiërarchie.

Zie [gegevens verzameling](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)voor meer informatie.

#### <a name="migration-jobs"></a>Migratietaken
Het proces waarbij wordt geconfigureerd welke specifieke objecten moeten worden gemigreerd, gevolgd door het beheer van de migratie van die objecten naar de doelhiërarchie.

Zie [een strategie voor migratie taken plannen](planning-a-migration-job-strategy.md)voor meer informatie.

#### <a name="client-migration"></a>Clientmigratie
Het proces waarbij informatie die clients gebruiken, wordt overgedragen van de database van de bronsite naar de database van de doelhiërarchie. Deze migratie van gegevens wordt gevolgd door een upgrade van client software op apparaten naar de client software versie van de doel hiërarchie.

Zie [een strategie voor client migratie plannen](planning-a-client-migration-strategy.md)voor meer informatie.

#### <a name="shared-distribution-points"></a>Gedeelde distributiepunten
De distributie punten van de bron hiërarchie die tijdens de migratie periode Configuration Manager gedeeld met de doel hiërarchie.

Tijdens de migratie periode kunnen clients die zijn toegewezen aan sites in de doel hiërarchie inhoud ophalen van gedeelde distributie punten.

Zie [distributie punten delen tussen de bron-en doel hiërarchieën](planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)voor meer informatie.

#### <a name="monitoring-migration"></a>Migratiebewaking
Het proces waarbij migratieactiviteiten worden bewaakt. U controleert de voortgang van de migratie en het succes van het knoop punt **migratie** in de werk ruimte **beheer** .

Zie [plannen voor het bewaken van migratie activiteiten](planning-to-monitor-migration-activity.md)voor meer informatie.

#### <a name="stop-gathering-data"></a>Gegevens verzamelen stoppen
Het proces waarbij het verzamelen van gegevens vanaf bronsites wordt gestopt. Wanneer u niet langer gegevens hebt om te migreren vanaf een bron hiërarchie, of als u migratie activiteiten wilt onderbreken, kunt u de doel hiërarchie configureren om te stoppen met het verzamelen van gegevens uit de bron hiërarchie.

Zie [gegevens verzameling](planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)voor meer informatie.

#### <a name="clean-up-migration-data"></a>Migratiegegevens opruimen
Het proces waarbij de migratie vanuit een bronhiërarchie wordt voltooid door informatie over de migratie te verwijderen uit de database van de doelhiërarchie.

Zie [plannen voor het volt ooien](planning-to-complete-migration.md)van de migratie voor meer informatie.



## <a name="typical-workflow"></a>Standaardwerkstroom  

Een werk stroom voor migratie instellen:

1.  Geef een ondersteunde bronhiërarchie op.  

2.  Het verzamelen van gegevens instellen. Met het verzamelen van gegevens kan Configuration Manager informatie verzamelen over gegevens die kunnen worden gemigreerd van de bron hiërarchie.  

     Configuration Manager wordt het proces voor het verzamelen van gegevens op basis van een eenvoudig schema automatisch herhaald, totdat u het proces voor het verzamelen van gegevens stopt. Het proces voor het verzamelen van gegevens wordt standaard elke vier uur herhaald, zodat Configuration Manager wijzigingen in de gegevens in de bron hiërarchie kan identificeren. Het verzamelen van gegevens is ook nodig om distributie punten te delen.  

3.  Maak migratietaken om gegevens te migreren tussen de bron- en doelhiërarchie.  

4.  U kunt het proces voor het verzamelen van gegevens op elk gewenst moment stoppen met behulp van de actie voor het **verzamelen van gegevens stoppen** . Wanneer u het verzamelen van gegevens stopt, worden de wijzigingen aan gegevens in de bron hiërarchie niet meer door Configuration Manager geïdentificeerd en kunnen er geen distributie punten meer worden gedeeld. Meestal gebruikt u deze actie wanneer u niet langer van plan bent om gegevens te migreren of distributiepunten van de bronhiërarchie te delen.  

5.  Nadat het verzamelen van gegevens op alle sites voor de bron hiërarchie is gestopt, kunt u de migratie gegevens eventueel opschonen met de actie **migratie gegevens opschonen** . Met deze actie worden de historische gegevens over de migratie van een bron hiërarchie verwijderd uit de data base van de doel hiërarchie.  

Nadat u gegevens hebt gemigreerd en u de bron hiërarchie niet meer nodig hebt voor het beheren van apparaten in uw omgeving, kunt u die bron hiërarchie en-infra structuur buiten gebruik stellen.  



##  <a name="scenarios"></a><a name="BKMK_MigrationScenarios"></a>Denkbaar  

 Configuration Manager ondersteunt de volgende migratie scenario's:
- [Migreren vanuit Configuration Manager 2007-hiërarchieën](#bkmk_2007)  
- [Migratie van Configuration Manager 2012 of een andere Configuration Manager-hiërarchie](#bkmk_2012)

> [!NOTE]  
>  De uitbrei ding van een hiërarchie met een zelfstandige site in een hiërarchie die een centrale beheer site heeft, wordt niet gecategoriseerd als een migratie. Zie [een zelfstandige primaire site uitbreiden](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)voor meer informatie over hiërarchie-uitbrei ding.  


### <a name="migration-from-configuration-manager-2007-hierarchies"></a><a name="bkmk_2007"></a>Migratie van Configuration Manager 2007-hiërarchieën  

 Wanneer u migratie gebruikt om gegevens te migreren van Configuration Manager 2007, kunt u uw investering in uw bestaande site-infra structuur behouden en profiteren van de volgende voor delen:  

#### <a name="site-database-improvements"></a>Verbeteringen aan de sitedatabase
De Configuration Manager-Data Base (current branch) ondersteunt volledige Unicode.

#### <a name="database-replication-between-sites"></a>Databasereplicatie tussen sites
Replicatie in Configuration Manager (current branch) is gebaseerd op Microsoft SQL Server. Dit gedrag verbetert de prestaties van site-naar-site-gegevens overdracht.

#### <a name="user-centric-management"></a>Op de gebruiker gericht beheer
Gebruikers zijn de focus van beheer taken in Configuration Manager (current branch). U kunt bijvoorbeeld software distribueren naar een gebruiker, zelfs als u de naam van het apparaat niet weet voor die gebruiker. Daarnaast geeft Configuration Manager gebruikers veel meer controle over de software die op hun apparaten wordt geïnstalleerd en wanneer die software wordt geïnstalleerd.

#### <a name="hierarchy-simplification"></a>Vereenvoudiging van de hiërarchie
Met Configuration Manager (current branch) kunt u een eenvoudigere site hiërarchie bouwen. Deze verbetering wordt veroorzaakt door de introductie van het type centrale beheer site en wijzigingen in het gedrag van de primaire en secundaire sites. Configuration Manager (current branch) maakt gebruik van minder netwerk bandbreedte en vereist minder servers dan eerdere versies.

#### <a name="role-based-administration"></a>Op rollen gebaseerd beheer
Dit centrale beveiligings model in Configuration Manager (current branch) biedt de beveiliging en het beheer van de gehele hiërarchie die overeenkomt met uw beheer-en bedrijfs vereisten.

> [!NOTE]  
>  Vanwege ontwerp wijzigingen die voor het eerst in System Center 2012 Configuration Manager zijn geïntroduceerd, kunt u Configuration Manager 2007 niet upgraden naar Configuration Manager (current branch). In-place upgrade wordt ondersteund van System Center 2012 Configuration Manager naar Configuration Manager (current branch).  


### <a name="migration-from-configuration-manager-2012-or-another-configuration-manager-hierarchy"></a><a name="bkmk_2012"></a>Migratie van Configuration Manager 2012 of een andere Configuration Manager-hiërarchie  
 Het proces voor het migreren van gegevens van een System Center 2012-Configuration Manager of Configuration Manager-hiërarchie is hetzelfde. Dit proces omvat het migreren van gegevens van meerdere bron hiërarchieën naar één enkele doel hiërarchie. U kunt dit proces gebruiken wanneer uw bedrijf aanvullende bronnen krijgt die al worden beheerd door Configuration Manager. Daarnaast kunt u gegevens migreren van een test omgeving naar uw Configuration Manager-productie omgeving. Met dit proces kunt u uw investering in de Configuration Manager test omgeving onderhouden.  



## <a name="see-also"></a>Zie ook  

-   [Migratie naar Configuration Manager plannen](planning-for-migration.md)  

-   [Bron hiërarchieën en bron sites configureren voor migratie](configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Bewerkingen voor migratie](operations-for-migration.md)  

-   [Beveiliging en privacy voor migratie](security-and-privacy-for-migration.md)  

-   [Aan de slag met Configuration Manager](../servers/deploy/start-using.md)
