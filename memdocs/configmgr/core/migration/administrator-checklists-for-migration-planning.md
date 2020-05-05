---
title: Controle lijsten voor migratie
titleSuffix: Configuration Manager
description: Gebruik de controle lijsten voor beheerders voor het plannen van een migratie strategie voor het Configuration Manager van de huidige vertakking.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e406a2b7674815bb3313200ba850baa249f17ebc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718943"
---
# <a name="administrator-checklists-for-migration-planning-in-configuration-manager"></a>Controle lijsten voor beheerders voor migratie planning in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de volgende controle lijsten voor beheerders om u te helpen bij het plannen van de migratie strategie voor Configuration Manager huidige branch.

##  <a name="administrator-checklist-for-migration-planning"></a><a name="Checklist_Migraiton_Planning"></a>Controle lijst voor beheerders voor migratie planning  
 Gebruik de volgende controle lijst voor de plannings stappen voorafgaand aan de migratie.  

-   **Evalueer de huidige omgeving:**  

     Bepaal de bestaande bedrijfsvereisten waaraan de bronhiërarchie voldoet en stel plannen op om in de doelhiërarchie te blijven voldoen aan die vereisten.  

-   **Bekijk de functionaliteit en wijzigingen die beschikbaar zijn in de versie van Configuration Manager die u gebruikt, en gebruik deze informatie om u te helpen bij het ontwerpen van uw doel hiërarchie:**  

    Zie [Fundamentals of Configuration Manager](../../core/understand/fundamentals.md) en [what's New](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)(Engelstalig) voor meer informatie.  


-   **Bepaal het administratieve beveiligings model dat moet worden gebruikt voor beheer op basis van rollen:**  

    Zie de [basis principes van beheer op basis van rollen voor Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)voor meer informatie.  

-   **Uw netwerk-en Active Directory topologie evalueren:** Bekijk uw bestaande domein structuur en netwerk topologie en bedenk hoe dit van invloed is op uw hiërarchie ontwerp en migratie taken.  

-   **Voltooi het ontwerp van de doelhiërarchie:**  

    Neem beslissingen over de plaatsing van een centrale beheersite, primaire sites, secundaire sites en opties voor inhoudsdistributie.  

-   **Wijs de hiërarchie toe aan de computers die u gebruikt voor sites en siteservers in de doelhiërarchie:**  

    Identificeer de computers die sites en site systeem servers gebruiken in de doel hiërarchie en zorg ervoor dat ze voldoende capaciteit hebben om te voldoen aan bestaande en toekomstige operationele vereisten.  

-   **Plan de strategie voor objectmigratie:**  

    Plan het gebruik van de beschik bare migratie taken om verschillende objecten te migreren, waaronder site grenzen, verzamelingen, advertenties en implementaties. Zie [typen migratie taken](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) in [een strategie voor een migratie taak plannen](../../core/migration/planning-a-migration-job-strategy.md) voor meer informatie  

    Configuration Manager migreert alleen de objecten die u selecteert. Objecten die niet worden gemigreerd en die vereist zijn in de doel hiërarchie, moeten opnieuw worden gemaakt in de doel hiërarchie.  

    Objecten die kunnen worden gemigreerd worden weergegeven wanneer u migratietaken configureert.  

-   **Plan de strategie voor clientmigratie:**  

    Plan de migratie van clients aan de hand van een gecontroleerde benadering waarmee de netwerkbandbreedte en serververwerkingsvereisten worden beperkt wanneer u clients migreert naar de doelhiërarchie. Zie [een strategie voor client migratie plannen](../../core/migration/planning-a-client-migration-strategy.md)voor meer informatie over het plannen van een strategie voor client migratie.  

-   **Plan de inventaris- en compatibiliteitsgegevens:**  

    Configuration Manager biedt geen ondersteuning voor het migreren van de hardware-inventaris, software-inventaris of Desired Configuration Management compatibiliteits gegevens voor software-updates of clients.  

    Nadat de client is gemigreerd naar de nieuwe site in de doelhiërarchie en een beleid heeft ontvangen voor deze configuraties, verzendt de client deze informatie naar de toegewezen site. Door deze actie wordt de database van de doelsite gevuld met actuele inventaris- en compatibiliteitsgegevens.  

-   **Plan de voltooiing van de migratie vanaf de bronhiërarchie:**  

    Beslis wanneer objecten en clients worden gemigreerd. Nadat de migratie is voltooid, kunt u een planning maken om de siteservers in de bronhiërarchie buiten gebruik te stellen.  

##  <a name="administrator-checklist-for-hierarchy-migration"></a><a name="Checklist_Hierarchy_for_migration"></a>Controle lijst voor beheerders voor hiërarchie migratie  
Gebruik de volgende controlelijst om een doelhiërarchie te plannen voordat u de migratie start.  

-   **Bepaal welke computers moeten worden gebruikt in de doelhiërarchie:**  

    Configuration Manager biedt geen ondersteuning voor een in-place upgrade van de Configuration Manager 2007-infra structuur. In plaats daarvan gebruikt u migratie om gegevens te verplaatsen van Configuration Manager 2007 naar Configuration Manager huidige vertakking. Hiervoor moet u een side-by-side-implementatie gebruiken en Configuration Manager op nieuwe computers installeren.  

    Op dezelfde manier moet u, wanneer u migreert vanuit een andere Configuration Manager-hiërarchie, een nieuwe doel hiërarchie installeren die een side-by-side-implementatie is voor uw bron hiërarchie.  

-   **Maak de doelhiërarchie:**  

    Installeer en configureer een Configuration Manager-doel hiërarchie die een primaire site bevat om de migratie voor te bereiden. Bijvoorbeeld:  

    -   Installeer een centrale beheer site en installeer ten minste één onderliggend primair item.  

    -   Installeer een zelfstandige primaire locatie als u niet van plan bent om een centrale beheer site te gebruiken.  

-   **Als u informatie wilt migreren die gerelateerd is aan software-updates, configureert u een software-updatepunt in de doelhiërarchie en synchroniseert u software-updates:**  

    U moet software-updates in de doelhiërarchie configureren en synchroniseren voordat u informatie over software-updates kunt migreren vanaf de bronhiërarchie.  


-   **Installeer en configureer aanvullende sitesysteemrollen in de doelhiërarchie:**  

    Configureer aanvullende site systeem rollen en site systemen die u nodig hebt.  

-   **Controleer de operationele functionaliteit in de doel hiërarchie:**  

    Controleer het volgende:  

    -   Als de doelhiërarchie bestaat uit meerdere sites, bevestigt u dat databasereplicatie tussen de sites werkt. Database replicatie is niet van toepassing op zelfstandige primaire sites.  

    -   Controleer of alle geïnstalleerde site systeem rollen operationeel zijn.  

    -   Controleer of de Configuration Manager-clients die u installeert op de doel hiërarchie, kunnen communiceren met hun toegewezen site.  


##  <a name="administrator-checklist-for-migration"></a><a name="Checklisit_Migration"></a>Controle lijst voor beheerders voor migratie  
Gebruik de volgende controlelijsten om gegevens te migreren van de bronhiërarchie naar de doelhiërarchie.  

-   **Schakel migratie in binnen de doelhiërarchie:**  

    Configureer een bron hiërarchie door de site op het hoogste niveau van de bron hiërarchie op te geven. Zie [een strategie voor een bron hiërarchie plannen](../../core/migration/planning-a-source-hierarchy-strategy.md)voor meer informatie over het opgeven van de bron site.  

-   **Wanneer de bron hiërarchie Configuration Manager 2007 SP2 wordt uitgevoerd, selecteert en configureert u aanvullende sites in de bron hiërarchie:**  

    Voor elke aanvullende site in de Configuration Manager 2007 SP2-bron hiërarchie waarvan u gegevens wilt verzamelen, moet u referenties voor het verzamelen van gegevens configureren. Wanneer u elke bron site configureert, wordt het proces voor gegevens verzameling onmiddellijk gestart en doorloopt de migratie periode totdat u het verzamelen van gegevens voor die site stopt. Het verzamelen van gegevens zorgt ervoor dat u objecten van de bron hiërarchie kunt migreren die zijn bijgewerkt of toegevoegd na een eerder proces voor het verzamelen van gegevens.

    > [!NOTE]  
    >  Wanneer de bron hiërarchie System Center 2012 Configuration Manager of hoger uitvoert, hoeft u geen aanvullende bron sites te configureren.  

-   **Configureer het delen van distributiepunten:**  

    U kunt distributiepunten delen tussen de twee hiërarchieën om zodoende inhoudt voor objecten die u migreert, beschikbaar te stellen voor clients in de doelhiërarchie. Dit zorgt ervoor dat dezelfde inhoud beschikbaar blijft voor clients in beide hiërarchieën en dat u deze inhoud kunt onderhouden totdat u stopt met het verzamelen van gegevens en de migratie voltooit.  

    Zie [distributie punten tussen bron-en doel hiërarchieën delen](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [planning a Content Deployment Migration strategie](../../core/migration/planning-a-content-deployment-migration-strategy.md)(Engelstalig) voor meer informatie over gedeelde distributie punten.  

-   **Maak migratietaken en voer deze uit om objecten te migreren die zijn gekoppeld aan de clients in de bronhiërarchie:**  

    Maak migratietaken om objecten te migreren tussen hiërarchieën. De vereiste configuraties voor elke migratietaak kunnen verschillen, afhankelijk van de gegevens die met de taak worden gemigreerd.  

    Wanneer u bijvoorbeeld inhoud migreert (ongeacht de migratietaak die u gebruikt), moet u een site in de doelhiërarchie toewijzen om die inhoud te kunnen beheren. De toegewezen site krijgt toegang tot de locatie van het originele bronbestand voor de inhoud en is verantwoordelijk voor het distribueren van die inhoud naar distributiepunten in de doelhiërarchie.  

    Zie voor meer informatie [migratie taken maken en bewerken voor Configuration Manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) in [bewerkingen voor de migratie naar Configuration Manager huidige vertakking](../../core/migration/operations-for-migration.md).  

-   **Migreer clients naar de doelhiërarchie:**  

    Het proces voor het migreren van clients is afhankelijk van het migratiescenario:  

    -   Wanneer u clients migreert met een client versie die niet dezelfde is als de doel hiërarchie, moet u de client software bijwerken. Voor de upgrade moet u de huidige Configuration Manager-client verwijderen, gevolgd door de installatie van de nieuwe client versie die overeenkomt met de doel site.  

    -   Wanneer u clients migreert met een clientversie die overeenkomt met de versie van de doelhiërarchie, hoeft de client niet te worden bijgewerkt of opnieuw geïnstalleerd. In plaats daarvan wordt de client opnieuw toegewezen aan een primaire site in de doelhiërarchie.  

    Wanneer u een client migreert naar de doelhiërarchie, wordt de client gekoppeld aan de bijbehorende gegevens die u eerder hebt gemigreerd naar die doelhiërarchie.  

    Zie [een strategie voor client migratie plannen](../../core/migration/planning-a-client-migration-strategy.md)voor meer informatie.  

-   **Werk gedeelde distributiepunten bij of wijs ze opnieuw toe:**  

    Wanneer u clients in de bron hiërarchie niet langer hoeft te ondersteunen, kunt u gedeelde distributie punten van een Configuration Manager 2007-bron site bijwerken of gedeelde distributie punten van een System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron site opnieuw toewijzen. Wanneer u een distributiepunt bijwerkt of opnieuw toewijst, wordt de sitesysteemrol overgedragen naar een primaire site in de doelhiërarchie en wordt het distributiepunt verwijderd van de bronsite in de bronhiërarchie. Wanneer u een gedeeld distributie punt bijwerkt of opnieuw toewijst, blijft de inhoud op de distributiepunt computer en hoeft u de inhoud niet opnieuw te implementeren naar nieuwe distributie punten in de doel hiërarchie.  

    U kunt ook een distributie punt bijwerken dat zich op een co-locatie op een Configuration Manager 2007 secundaire site server bevindt. Hierbij worden de secundaire site en resultaten alleen verwijderd van een distributiepunt in de doelhiërarchie.  

    Zie [distributie punten tussen bron-en doel hiërarchieën delen](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [planning a Content Deployment Migration strategie](../../core/migration/planning-a-content-deployment-migration-strategy.md)(Engelstalig) voor meer informatie over gedeelde distributie punten.  

-   **Migratie volt ooien:**  

    Nadat u gegevens en clients hebt gemigreerd van alle sites in de bron hiërarchie en u de juiste distributie punten hebt bijgewerkt, kunt u de migratie volt ooien. Als u de migratie wilt volt ooien, stopt u met het verzamelen van gegevens voor elke bron site in de bron hiërarchie. Daarna kunt u migratiegegevens verwijderen die u niet nodig hebt, en de infrastructuur van de bronhiërarchie buiten bedrijf stellen. Zie [plannen voor het volt ooien](../../core/migration/planning-to-complete-migration.md)van de migratie voor meer informatie.  
