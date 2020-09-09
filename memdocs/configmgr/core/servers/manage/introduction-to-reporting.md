---
title: Inleiding op rapportage
titleSuffix: Configuration Manager
description: Meer informatie over de set hulpprogram ma's en bronnen die beschikbaar zijn voor het beheren van rapportage in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bfed31b820ac1f09b240122207b5bf27e432b10a
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607530"
---
# <a name="introduction-to-reporting-in-configuration-manager"></a>Inleiding tot rapportage in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Rapportage in Configuration Manager voorziet in een set hulpprogram ma's en bronnen waarmee u de geavanceerde rapportage mogelijkheden van SQL Server Reporting Services (SSRS) en Power BI Report Server kunt gebruiken. Beide rapportage platforms bieden uitgebreide ontwerp functies voor aangepaste rapporten. Rapportage helpt u bij het verzamelen, organiseren en presen teren van informatie over de schat van Configuration Manager gegevens in uw organisatie. Configuration Manager biedt veel vooraf gedefinieerde rapporten in Reporting Services die u zonder wijzigingen kunt gebruiken. U kunt de standaard rapporten dupliceren en aanpassen om te voldoen aan uw vereisten, of u kunt aangepaste rapporten maken.

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

SQL Server Reporting Services biedt een volledig aanbod aan gebruiks klare hulpprogram ma's en services om u te helpen bij het maken, implementeren en beheren van rapporten voor uw organisatie. Het bevat ook programmeer functies waarmee u uw rapportage functionaliteit kunt uitbreiden en aanpassen. Reporting Services is een server rapportage platform dat uitgebreide rapportage functionaliteit biedt voor verschillende soorten gegevens bronnen.

Configuration Manager gebruikt SQL Server Reporting Services als de primaire rapportage oplossing. Integratie met Reporting Services biedt de volgende voordelen:  

- Maakt gebruik van een systeem voor de industrie standaard rapportage om de Configuration Manager-Data Base op te vragen.  

- Geeft rapporten weer door gebruik te maken van de Configuration Manager rapport Viewer of door gebruik te maken van Report Manager, een Webverbinding die is gebaseerd op het rapport.  

- Biedt hoge prestaties, beschikbaarheid en schaalbaarheid.  

- Biedt abonnementen op rapporten waarmee gebruikers zich kunnen abonneren. Een manager abonneert bijvoorbeeld elke dag op een e-mail rapport met informatie over de status van een software-update-implementatie.

- Exporteert rapporten in verschillende soorten populaire indelingen.  

Zie [Wat is SQL Server Reporting Services (SSRS)?](/sql/reporting-services/create-deploy-and-manage-mobile-and-paginated-reports) voor meer informatie.

## <a name="power-bi-report-server"></a>Power BI Report Server

<!-- 3721603 -->

Met ingang van versie 2002 integreert u Power BI Report Server met Configuration Manager-rapportage. Deze integratie biedt u moderne visualisaties en betere prestaties. Het voegt console ondersteuning toe voor Power BI rapporten die vergelijkbaar zijn met wat er al bestaat met SQL Server Reporting Services. Zie [integreren met Power bi Report Server](powerbi-report-server.md)voor meer informatie.

Power BI Report Server is een on-premises rapport server met een webportal waarin u rapporten kunt weer geven en beheren. Het bevat hulpprogram ma's voor het maken van Power BI rapporten, gepagineerde rapporten, mobiele rapporten en Kpi's. Zie [Wat is Power bi Report Server?](/power-bi/report-server/get-started)voor meer informatie.

## <a name="reporting-services-point"></a>Reporting Services-punt

Het Reporting Services-punt is een site systeemrol die u toevoegt op een server waarop Microsoft SQL Server Reporting Services wordt uitgevoerd. Het Reporting Services-punt voert de volgende functies uit:

- Hiermee worden de Configuration Manager rapport definities naar Reporting Services gekopieerd
- Maakt rapport mappen op basis van rapport Categorieën
- Hiermee stelt u het beveiligings beleid in op de rapport mappen en-rapporten. Deze beleids regels zijn gebaseerd op de op rollen gebaseerde machtigingen voor Configuration Manager gebruikers met beheerders rechten. In een interval van 10 minuten maakt het Reporting Services-punt verbinding met Reporting Services om het beveiligings beleid opnieuw toe te passen als u dit hebt gewijzigd.

Zie de volgende artikelen voor meer informatie over het plannen en installeren van een Reporting Services-punt:

- [Rapportage plannen](planning-for-reporting.md)

- [Rapportage configureren](configuring-reporting.md)

## <a name="configuration-manager-reports"></a>Configuration Manager-rapporten

Configuration Manager biedt rapport definities voor meer dan 400 rapporten in meer dan 50 rapport mappen. Tijdens het installatie proces van het Reporting Services-punt worden ze gekopieerd naar de map met het hoofd rapport in SQL Server Reporting Services. De Configuration Manager-console toont de rapporten en organiseert deze in submappen op basis van de rapport categorie.

Rapporten geven de Configuration Manager hiërarchie niet omhoog of omlaag. Ze worden alleen uitgevoerd voor de data base van de site waarin u ze maakt. Omdat Configuration Manager globale gegevens repliceert in de hele hiërarchie, hebt u toegang tot de hiërarchie-brede informatie in rapporten. Wanneer een rapport gegevens ophaalt van een sitedatabase, heeft het toegang tot sitegegevens voor de actuele site en onderliggende sites, en tot globale gegevens voor elke site in de hiërarchie.

Net als andere Configuration Manager objecten moet een gebruiker met beheerders rechten de juiste machtigingen hebben om rapporten uit te voeren of te wijzigen. Een gebruiker met beheerdersrechten moet, om een rapport uit te voeren, beschikken over de machtiging **Rapport uitvoeren** voor het object. Een gebruiker met beheerdersrechten moet, om een rapport te maken of te wijzigen, beschikken over de machtiging **Rapport wijzigen** voor het object.

### <a name="create-and-modify-reports"></a>Rapporten maken en wijzigen

Voor rapporten op basis van Reporting Services gebruikt Configuration Manager Microsoft SQL Server Report Builder als exclusief ontwerp-en bewerkings programma voor rapporten op basis van modellen en op basis van SQL. Wanneer u een rapport maakt of bewerkt in de Configuration Manager-console, wordt Report Builder geopend. Zie [bewerkingen en onderhoud voor rapportage](operations-and-maintenance-for-reporting.md)voor meer informatie.

Met ingang van versie 2002 om Power BI-rapporten te maken of te bewerken, kan de console worden geïntegreerd met Power BI Desktop. Zie [Power bi-rapporten maken](powerbi-report-server.md#create-power-bi-reports)voor meer informatie.

### <a name="run-reports"></a>Rapporten uitvoeren

Wanneer u een rapport op basis van Reporting Services in de Configuration Manager-console uitvoert, wordt de rapport viewer geopend en wordt er verbinding gemaakt met Reporting Services. Als u vereiste rapportparameters opgeeft, haalt Reporting Services deze gegevens op en geeft de resultaten weer in de viewer. U kunt ook verbinding maken met de SQL Services Reporting Services, verbinden met de gegevensbron voor de site en rapporten uitvoeren.

Vanaf versie 2002, wanneer u een rapport op basis van Power BI uitvoert, wordt het in de webbrowser geopend.

### <a name="report-prompts"></a>Rapportprompts

U kunt een rapport prompt of para meter configureren wanneer u een rapport maakt of wijzigt. Maak rapport prompts om de gegevens die een rapport ophaalt te beperken of te richten. Een rapport kan meer dan één prompt bevatten. Zorg ervoor dat de prompt namen uniek zijn en alleen alfanumerieke tekens bevatten die voldoen aan de SQL Server regels voor id's.

Wanneer u een rapport uitvoert, vraagt de prompt een waarde voor een vereiste para meter. Op basis van de parameter waarde worden de rapport gegevens opgehaald. De **computer informatie voor een specifieke computer** rapport vraagt bijvoorbeeld om een computer naam. Reporting Services geeft de opgegeven waarde door aan een variabele die in de SQL-instructie van het rapport is gedefinieerd.

### <a name="report-links"></a>Rapportkoppelingen

Rapport koppelingen in Configuration Manager worden gebruikt in een bron rapport om eenvoudig toegang te bieden tot aanvullende gegevens. Het kan bijvoorbeeld worden gekoppeld aan meer gedetailleerde informatie over elk van de items in het bron rapport. Als er voor het doelrapport één of meer prompts nodig zijn om uit te voeren, moet het bronrapport een kolom bevatten met de juiste waarden voor elke prompt.

De koppeling moet het kolom nummer opgeven met de waarde voor de prompt. Bijvoorbeeld:

- Er is één rapport met een lijst met computers die de site onlangs heeft gedetecteerd.
- U kunt een koppeling maken naar een rapport met de laatste berichten die door de site worden ontvangen voor een specifieke computer.
- U maakt de koppeling en geeft aan dat de kolom `2` in het bron rapport de computer naam bevat. Deze waarde is een vereiste prompt voor het doel rapport.
- U voert het bron rapport uit en er wordt links van elke rij met gegevens een koppelings pictogram weer gegeven.
- U selecteert het pictogram op een rij, en rapport Viewer geeft de waarde in de opgegeven kolom voor die rij als de prompt waarde voor het doel rapport door.

U kunt slechts één koppeling voor een rapport configureren en die koppeling kan alleen verbinding maken met één doel rapport.

> [!WARNING]  
> Als u de doelmap naar een andere rapportmap verplaatst, verandert de locatie voor het doelrapport. Configuration Manager de rapport koppeling in het bron rapport wordt niet automatisch bijgewerkt met de nieuwe locatie en de koppeling werkt niet in het bron rapport.

## <a name="report-folders"></a>Rapportmappen

Rapport mappen bieden een methode om rapporten te sorteren en filteren die Configuration Manager opgeslagen in Reporting Services. Rapport mappen zijn handig wanneer er veel rapporten zijn om te beheren. Wanneer u een Reporting Services-punt installeert, worden rapporten naar Reporting Services gekopieerd en in meer dan 50 rapport mappen ingedeeld. De rapportmappen zijn alleen-lezen. U kunt ze niet wijzigen in de Configuration Manager-console.

## <a name="report-subscriptions"></a>Rapportabonnementen

Een rapport abonnement in Reporting Services is een terugkerende aanvraag om een rapport te leveren op een specifiek tijdstip of als reactie op een gebeurtenis. U geeft de bestands indeling van een toepassing op in het abonnement. Abonnementen bevatten een alternatief voor het uitvoeren van een rapport op aanvraag. Voor rapporten op aanvraag dient u het rapport actief te selecteren telkens u het wilt weergeven. Abonnementen kunnen daarentegen worden gebruikt om de levering van een rapport te plannen en vervolgens te automatiseren.

U kunt rapport abonnementen beheren in de Configuration Manager-console. De rapport server verwerkt de abonnementen. Ze worden gedistribueerd met behulp van leverings extensies die op de server zijn geïmplementeerd. Standaard kunt u abonnementen maken die rapporten verzenden naar een gedeelde map of naar een e-mailadres.

Zie [Manage Report abonnementen](operations-and-maintenance-for-reporting.md#bkmk_subscription)(Engelstalig) voor meer informatie.

## <a name="report-builder"></a>Report Builder

Voor rapporten op basis van Reporting Services gebruikt Configuration Manager Microsoft SQL Server Report Builder als exclusief ontwerp-en bewerkings programma voor rapporten op basis van modellen en SQL. Als u een rapport maakt of bewerkt in de Configuration Manager-console, wordt Report Builder geopend. Wanneer u een rapport voor de eerste keer maakt of wijzigt, wordt Report Builder automatisch geïnstalleerd. De versie van Report Builder die aan de geïnstalleerde versie van SQL Server is gekoppeld, wordt geopend wanneer u rapporten uitvoert of bewerkt.  

 De installatie van de Report Builder voegt ondersteuning toe voor meer dan 20 talen. Wanneer u Report Builder uitvoert, worden de gegevens weer gegeven in de taal van het besturings systeem van de lokale computer. Als Report Builder de taal niet ondersteunt, worden de gegevens in het Engels weer gegeven. Report Builder ondersteunt de volledige mogelijkheden van SQL Server Reporting Services. Dit omvat de volgende mogelijkheden:

- Biedt een intuïtieve ontwerp omgeving voor rapporten met een vormgeving die vergelijkbaar is met Microsoft 365-apps.  

- Biedt de flexibele rapport indeling van SQL Server Report Definition Language (RDL).  

- Biedt verschillende vormen van gegevensvisualisatie waaronder grafieken en meters.  

- Biedt tekstvakken met opmaak.  

- Exporteert naar Microsoft Word-indeling.  

U kunt Report Builder ook rechtstreeks openen vanuit SQL Server Reporting Services.

## <a name="report-models-in-sql-server-reporting-services"></a>Rapportmodellen in SQL Server Reporting Services

SQL Reporting Services gebruikt rapport modellen om u te helpen bij het selecteren van items uit de Configuration Manager-Data Base voor opname in op modellen gebaseerde rapporten. Wanneer u een rapport bouwt, worden alleen opgegeven weer gaven en items beschikbaar gemaakt in rapport modellen waaruit u kunt kiezen. Er moet er minstens één rapportmodel beschikbaar zijn om op modellen gebaseerde rapporten te maken.

Rapportmodellen hebben de volgende functies:

- Geef logische bedrijfs namen op in database velden en-weer gaven. Als u rapporten wilt maken, hebt u geen kennis nodig van de structuur van de Configuration Manager-Data Base.

- Items logisch groeperen.  

- Relaties tussen items definiëren.  

- Beveilig model elementen zodat gebruikers met beheerders rechten alleen de gegevens kunnen zien die ze mogen zien.

Hoewel Configuration Manager voorbeeld rapport modellen biedt, kunt u ook rapport modellen definiëren om te voldoen aan uw eigen zakelijke behoeften. Zie [aangepaste rapport modellen maken](creating-custom-report-models-in-sql-server-reporting-services.md)voor meer informatie over het maken van rapport modellen.

## <a name="next-steps"></a>Volgende stappen

[Rapportage plannen](planning-for-reporting.md)