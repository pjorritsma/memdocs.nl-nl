---
title: Lijst met rapporten
titleSuffix: Configuration Manager
description: Bekijk een lijst met rapporten die worden geleverd met Configuration Manager. De rapporten worden in verschillende categorieën weergegeven.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49fe5b5b94b29d93d29108660e2b76db2f87ddf9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713763"
---
# <a name="list-of-reports-in-configuration-manager"></a>Lijst met rapporten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager biedt veel ingebouwde rapporten voor veel van de rapportage taken die u mogelijk wilt uitvoeren. U kunt ook de SQL-instructies in deze rapporten gebruiken om u te helpen uw eigen rapporten schrijven.   

De volgende rapporten zijn opgenomen in Configuration Manager. De rapporten worden in verschillende categorieën weergegeven.  



## <a name="administrative-security"></a>Administratieve beveiliging  

De volgende zes rapporten worden vermeld in de categorie **administratieve beveiliging** .  

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Activiteitenlogboek van beheer**|Geeft een record weer van administratieve wijzigingen die zijn aangebracht voor gebruikers met beheerders rechten, beveiligings rollen, beveiligingsbereiken en verzamelingen.|  
|**Beveiligingstaken voor beheergebruiker**|Geeft beheergebruikers, de bijbehorende beveiligingsrollen en de beveiligingsbereiken die zijn gekoppeld aan elke rol voor elke gebruiker weer.|  
|**Objecten die zijn beveiligd door één beveiligingsbereik**|Geeft objecten weer die een beheerder heeft toegewezen aan het opgegeven beveiligings bereik. Dit rapport geeft geen objecten weer die een beheerder aan meer dan één beveiligings bereik koppelt.|  
|**Beveiliging voor een bepaald of meerdere Configuration Manager-objecten**|Bevat objecten die kunnen worden beveiligd, de beveiligingsbereiken die aan deze objecten zijn gekoppeld en welke beheerdergebruikers rechten hebben voor de objecten.|  
|**Samenvatting beveiligingsrollen**|Geeft beveiligings rollen en de Configuration Manager beheerders die aan elke rol zijn gekoppeld.|  
|**Samenvatting beveiligingsbereiken**|Hiermee worden beveiligingsbereiken en de Configuration Manager gebruikers met beheerders rechten en beveiligings groepen die zijn gekoppeld aan elk bereik weer gegeven.|  



## <a name="alerts"></a>Waarschuwingen  

De volgende twee rapporten worden vermeld in de categorie **waarschuwingen** .  

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Waarschuwingsscorecard**|Geeft een samenvatting weer van alle uitgestelde waarschuwingen die zijn gegenereerd tussen de opgegeven begindatum en einddatum.|  
|**Meest gegenereerde waarschuwingen**|Geeft een samenvatting weer van de waarschuwingen die het meest zijn gegenereerd vanaf de opgegeven datum voor het opgegeven functiegebied tot dit moment.|  



## <a name="asset-intelligence"></a>Asset Intelligence  

De volgende 67-rapporten worden vermeld in de categorie **Asset Intelligence** .  

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Hardware 01A - Samenvatting van computers in een opgegeven verzameling**|Geeft een Asset Intelligence-samenvatting weer van computers in een verzameling die u opgeeft.|  
|**Hardware 03A - Primaire computergebruikers**|Geeft gebruikers weer en het aantal computers waarop ze de primaire gebruiker zijn.|  
|**Hardware 03B - Computers voor een specifieke primaire console-gebruiker**|Geeft alle computers weer waarvoor een opgegeven gebruiker de primaire console-gebruikers is.|  
|**Hardware 04A - Computers met meerdere gebruikers (gedeeld)**|Geeft computers weer die geen primaire gebruiker hebben omdat geen enkele gebruiker een ingelogde tijd heeft die groter is dan 66%.|  
|**Hardware 05A - Consolegebruikers op een opgegeven computer**|Bevat alle consolegebruikers op een opgegeven computer.|  
|**Hardware 06A - Computers waarvoor geen consolegebruikers kunnen worden vastgesteld**|Helpt beheerdergebruikers bij de identificatie van computers waarvoor het vastleggen van gebeurtenissen in het beveiligingslogboek moet worden ingeschakeld.|  
|**Hardware 07A - USB-apparaten op fabrikant**|Geeft de USB-apparaten weer, gegroepeerd op fabrikant.|  
|**Hardware 07A - USB-apparaten op fabrikant en omschrijving**|Geeft de USB-apparaten weer, gegroepeerd op fabrikant en omschrijving.|  
|**Hardware 07C - Computers met een bepaald USB-apparaat**|Geeft alle computers weer met een opgegeven USB-apparaat|  
|**Hardware 07D - USB-apparaten op een bepaalde computer**|Geeft alle USB-apparaten op een opgegeven computer weer.|  
|**Hardware 08A - Hardware die niet gereed is voor een software-upgrade**|Geeft hardware weer die niet voldoet aan de minimale hardwarevereisten.|  
|**Hardware 09A - Zoeken naar computers**|Geeft een samen vatting weer van computers die overeenkomen met trefwoord filters. Deze filters zijn computer naam, Configuration Manager site, domein, bovenste console gebruiker, besturings systeem, fabrikant of model.|  
|**Hardware 10A - Computers in een opgegeven verzameling die zijn gewijzigd tijdens een opgegeven periode**|Geeft een samenvatting weer van computers in een opgegeven collectie waarbij een hardwareklasse is gewijzigd gedurende een opgegeven periode.|  
|**Hardware 10B - Wijzigingen op een opgegeven computer in een opgegeven periode**|Geeft de klassen weer die zijn gewijzigd op een opgegeven computer in een opgegeven periode.|  
|**Licentie 01A - Microsoft Volume License-grootboek voor Microsoft-licentieverklaringen**|Geeft een inventarisatie weer van alle Microsoft-softwaretitels die beschikbaar zijn in het Microsoft Volume Licensing-programma|  
|**Licentie 01B - Microsoft Volume License-grootboekitem per verkoopkanaal**|Identificeert en toont verkoopkanaal voor geïnventariseerde Microsoft Volume License-software.|  
|**Licentie 01C - Computers met een specifiek Microsoft Volume License-grootboekitem en verkoopkanaal**|Identificeert en toont computers die een opgegeven item bevatten uit het Microsoft Volume License-grootboek.|  
|**Licentie 01D - Microsoft Volume License-grootboekproducten op een specifieke computer**|Identificeert en toont alle Microsoft-Volume License-grootboekitems op een opgegeven computer.|  
|**Licentie 02A - Aantal licenties die binnenkort aflopen op tijdperiode**|Geeft het aantal licenties weer dat binnenkort verloopt op basis van een opgegeven tijdperiode. De weer gegeven producten hebben hun licenties die worden beheerd door de Software Licensing-service.|  
|**Licentie 02B - Computers met licenties die binnenkort verlopen**|Geeft de opgegeven computers weer met licenties die binnenkort verlopen.|  
|**Licentie 02C - Licentie-informatie op een specifieke computer**|Geeft producten weer op een computer waarvan de licenties worden beheerd door de Software Licensing-service.|  
|**Licentie 03A - Aantal licenties op licentiestatus**|Geeft producten weer, op licentiestatus, waarvan de licenties worden beheerd door de Software Licensing-service.|  
|**Licentie 03B - Computers met een specifieke licentiestatus**|Geeft producten weer, met een opgegeven licentiestatus, waarvan de licenties worden beheerd door de Software Licensing-service.|  
|**Licentie 04A - Aantal producten dat worden beheerd door softwarelicenties**|Geeft het aantal producten weer waarvan de licenties worden beheerd door de Software Licensing-service.|  
|**Licentie 04B - Computers met een specifiek product dat wordt beheerd door de Software Licensing-service**|Geeft computers weer die worden beheerd door de Software Licensing-service en die een opgegeven product bevatten.|  
|**Licentie 05A - Computers die Sleutelbeheerserver bieden**|Geeft computers weer die als sleutelbeheerserver fungeren.|  
|**Licentie 06A - Processortellingen voor producten die per processor zijn gelicentieerd**|Geeft het aantal processoren weer op computers die Microsoft-producten gebruiken die licentieverlening per processor ondersteunen.|  
|**Licentie 06B - Computers met een specifiek product dat per licentieverlening per processor ondersteunt**|Geeft een lijst weer van computers waarop een opgegeven Microsoft-product is geïnstalleerd dat licentieverlening per processor ondersteunt.|  
|**Licentie 14A - Microsoft Volume Licensing-afstemmingsrapport**|Geeft afstemming weer voor software licenties die zijn verkregen via micro soft Volume License Agreement en de werkelijke inventarisatie telling.|  
|**Licentie 14B - Lijst van Microsoft software-inventarisatie die niet is gevonden in MVLS**|Dit rapport geeft de micro soft-software titels weer die in gebruik zijn en die niet zijn gevonden in de micro soft-volume licentie overeenkomst.|  
|**Licentie 15A - Algemeen rapport licentie-afstemming**|Geeft afstemming weer op algemene software licenties die zijn verkregen en de werkelijke inventarisatie telling.|  
|**Licentie 15B - Algemeen rapport licentie-afstemming per computer**|Geeft computers weer waarop het gelicentieerde product is geïnstalleerd met een opgegeven versie.|  
|**Software 01A - Samenvatting van geïnstalleerde software in een specifieke verzameling**|Geeft samenvatting weer van geïnstalleerde software die is besteld op het aantal exemplaren dat in de inventarisatie is gevonden.|  
|**Software 02A - Productfamilies voor een specifieke verzameling**|Geeft de productfamilies en de telling van software in de familie voor een specifieke verzameling weer.|  
|**Software 02B - Productcategorieën voor een specifieke productfamilie**|Geeft opsomming weer van de productcategorieën in een opgegeven productfamilie en de telling van software binnen de categorie.|  
|**Software 02C - Software in a bepaalde productfamilie en -categorie**|Geeft alle software weer in een opgegeven productfamilie en -categorie.|  
|**Software 02D - Computers waarop bepaalde software is geïnstalleerd**|Geeft alle computers weer waarop opgegeven software is geïnstalleerd.|  
|**Software 02E - Geïnstalleerde software op een specifieke computer**|Geeft alle software weer die op een opgegeven computer is geïnstalleerd.|  
|**Software 03A - Niet-gecategoriseerde software**|Geeft de software weer die is ingedeeld als onbekend of die geen indeling heeft.|  
|**Software 04A - Software die is geconfigureerd om automatisch te worden uitgevoerd op computers**|Geeft een lijst weer van software die is geconfigureerd om automatisch te worden uitgevoerd op computers.|  
|**Software 04B - Computers met software die is geconfigureerd om automatisch te worden uitgevoerd**|Geeft alle computers weer met opgegeven software die is geconfigureerd om automatisch te worden uitgevoerd|  
|**Software 04C - Software die is geconfigureerd om automatisch te worden uitgevoerd op een bepaalde computer**|Geeft geïnstalleerde software weer die is geconfigureerd om automatisch te worden uitgevoerd op een opgegeven computer|  
|**Software 05A - Browserhelperobjecten**|Geeft de browserhelperobjecten weer die zijn geïnstalleerd op computers in een opgegeven verzameling.|  
|**Software 05B - Computers met een specifiek browserhelperobject**|Geeft alle computers weer met een opgegeven browser helper-object.|  
|**Software 05C - Browserhelperobjecten op een specifieke computer**|Geeft alle browserhelperobjecten op de opgegeven computer weer.|  
|**Software 06A - Zoeken naar geïnstalleerde software**|Dit rapport bevat een samen vatting van geïnstalleerde software. Er wordt gezocht op basis van de volgende criteria: product naam, uitgever of versie.|  
|**Software 06B - Software op productnaam**|Geeft een samen vatting weer van geïnstalleerde software op basis van een opgegeven product naam.|  
|**Software 07A - Recent gebruikte uitvoerbare programma's op de telling van computers**|Geeft uitvoer bare Program ma's weer die gebruikers recent hebben gebruikt. Het bevat ook het aantal computers waarop gebruikers het programma hebben gebruikt. Softwarelicentiecontrole moet zijn ingeschakeld voor deze site om dit rapport te kunnen weergeven.|  
|**Software 07B - Computers die recent een opgegeven uitvoerbaar programma hebben gebruikt**|Geeft de computers weer waarop gebruikers recent een opgegeven uitvoerbaar programma hebben gebruikt. Dit rapport vereist dat u de client instelling voor software licentie controle inschakelt.|  
|**Software 07C - Recent gebruikte uitvoerbare programma's op een opgegeven computer**|Geeft de uitvoer bare bestanden weer die gebruikers recent op een opgegeven computer hebben gebruikt. Dit rapport vereist dat u de client instelling voor software licentie controle inschakelt.|  
|**Software 08A - Recent gebruikte uitvoerbare programma's op telling van gebruikers**|Geeft uitvoer bare Program ma's weer die gebruikers recent hebben gebruikt. Het bevat ook een telling van de gebruikers die het programma het meest recent hebben gebruikt. Dit rapport vereist dat u de client instelling voor software licentie controle inschakelt.|  
|**Software 08B - Gebruikers die recent een opgegeven uitvoerbaar programma hebben gebruikt**|Geeft de gebruikers weer die het meest recent een opgegeven uitvoerbaar programma hebben gebruikt. Dit rapport vereist dat u de client instelling voor software licentie controle inschakelt.|  
|**Software 08C - Recent gebruikte uitvoerbare programma's door een opgegeven gebruiker**|Geeft uitvoer bare Program ma's weer die de opgegeven gebruiker onlangs heeft gebruikt. Dit rapport vereist dat u de client instelling voor software licentie controle inschakelt.|  
|**Software 09A - Zelden gebruikte software**|Geeft software titels weer die gebruikers gedurende een opgegeven periode niet hebben gebruikt.|  
|**Software 09B - Computers waarop zelden gebruikte software is geïnstalleerd**|Geeft computers weer met geïnstalleerde software die gebruikers gedurende een opgegeven periode niet hebben gebruikt. De opgegeven periode is gebaseerd op de waarde die is opgegeven in het rapport 'Software 09A - Zelden gebruikte software'.|  
|**Software 10A - Softwaretitels waarvoor specifieke meerdere aangepaste etiketten zijn gedefinieerd**|Geeft softwaretitels weer op basis van overeenkomst met alle opgegeven criteria voor aangepaste etiketten. Er kunnen maximaal drie aangepaste etiketten worden geselecteerd om een softwaretitelzoekopdracht te verfijnen.|  
|**Software 10B - Computers waarvoor een specifieke softwaretitel met aangepast etiket is geïnstalleerd**|Geeft alle computers in deze verzameling weer waarvoor de opgegeven softwaretitel met aangepast etiket is geïnstalleerd.|  
|**Software 11A - Softwaretitels waarvoor een specifiek aangepast etiket is gedefinieerd**|Geeft softwaretitels weer op basis van overeenkomst met ten minste een van de opgegeven criteria voor aangepaste etiketten.|  
|**Software 12A - Softwaretitels zonder aangepast etiket**|Geeft alle software titels weer waarvoor geen aangepast etiket is gedefinieerd.|  
|**Software 14A - Zoeken naar software waarbij een softwaretag is geactiveerd**|Geeft de telling weer van geïnstalleerde software waarbij een softwaretag is geactiveerd.|  
|**Software 14B -Computers met geïnstalleerde software waarbij een bepaalde software-id-tag is geactiveerd**|Geeft een opsomming weer van alle computers die geïnstalleerde software hebben waarbij een opgegeven software-id-tag is geactiveerd.|  
|**Software 14C - Geïnstalleerde software waarbij een bepaalde software-id-tag is geactiveerd op een computer**|Geeft een opsomming weer van alle geïnstalleerde software waarbij een opgegeven software-id-tag is geactiveerd op een opgegeven computer.|  
|**Levens cyclus 01A-computers met een specifiek software product**|Een lijst weer geven met computers waarop een opgegeven product is gedetecteerd.|
|**Levenscyclus 02A: lijst met computers met verlopen producten in de organisatie**|Computers weer geven die verlopen producten hierop hebben. U kunt dit rapport filteren op product naam.|
|**Levenscyclus 03A: lijst met verlopen producten die in de organisatie zijn gevonden**|Details weer geven voor producten in uw omgeving met verlopen levenscyclus datums.|
|**Levenscyclus 04A-algemeen overzicht van product levenscyclus**|Een lijst met product levenscyclussen weer geven. De lijst filteren op product naam en dagen tot verval datum.|
|**Levenscyclus 05A-dash board product levenscyclus**|Vanaf versie 1810 bevat dit rapport soort gelijke informatie als het dash board in de console.|



## <a name="client-push"></a>Client-push  

De volgende vier rapporten worden vermeld in de categorie **client push** .  

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Details van de status van de clientpushinstallatie**|Geeft informatie weer over het clientpushinstallatieproces voor alle sites.|  
|**Details van de status van de clientpushinstallatie voor een opgegeven site**|Geeft informatie weer over het clientpushinstallatieproces voor een opgegeven site.|  
|**Samenvatting van de status van de clientpushinstallatie**|Geeft samenvatting weer over het clientpushinstallatieproces voor alle sites.|  
|**Samenvatting van de status van de clientpushinstallatie voor een opgegeven site**|Geeft samenvatting weer over het clientpushinstallatieproces voor een opgegeven site.|  



## <a name="client-status"></a>Clientstatus  

De volgende zeven rapporten worden vermeld in de categorie **client status** .  

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Details over clientherstel**|Geeft details weer over clientherstelacties voor een verzameling die u opgeeft.|  
|**Samenvatting van clientherstel**|Geeft een samenvatting weer over clientherstelacties voor een opgegeven verzameling.|  
|**Geschiedenis van clientstatus**|Geeft een historisch overzicht weer van de algemene clientstatus in de site.|  
|**Samenvatting van clientstatus**|Geeft de clientcontroleresultaten weer van actieve clients voor een opgegeven verzameling.|  
|**Clienttijd voor aanvraag beleid**|Geeft het percentage clients weer dat in de afgelopen 30 dagen ten minste één maal beleid heeft aangevraagd. Elke dag staat voor een percentage van het totaal aantal clients dat beleid heeft aangevraagd sinds de eerste dag in de cyclus.|  
|**Details van fouten clientcontrole**|Geeft details weer over clients waarbij de clientcontrole is mislukt voor een opgegeven verzameling.|  
|**Details van niet-actieve clients**|Geeft een gedetailleerde lijst weer van inactieve clients voor een bepaalde verzameling.|  



## <a name="company-resource-access"></a>Toegang tot bedrijfsbronnen  

De volgende drie rapporten worden vermeld in de categorie **toegang tot bedrijfs resources** . 

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Geschiedenis van certificaatuitgifte**|Hier wordt de geschiedenis weer gegeven van certificaten die zijn uitgegeven door het certificaat registratiepunt voor gebruikers en apparaten voor het opgegeven datum bereik.|  
|**Lijst met activa per certificaatuitgiftestatus**|Geeft een lijst weer van apparaten of gebruikers in een opgegeven certificaatuitgiftestatus na de evaluatie van een opgegeven certificaatprofiel.|  
|**Lijst met activa met certificaten die de vervaldatum bijna hebben bereikt**|Geeft de apparaten of gebruikers weer met certificaten die op of voor de opgegeven datum vervallen.|  



## <a name="compliance-and-settings-management"></a>Naleving en instellingen beheren  

De volgende 22 rapporten worden vermeld in de categorie **naleving en instellingen beheer** . 

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Compatibiliteitsgeschiedenis van een configuratiebasislijn**|Geeft de geschiedenis weer van de wijzigingen in compatibiliteit van een configuratiebasislijn voor het opgegeven datumbereik.|  
|**Compatibiliteitsgeschiedenis van een configuratie-item**|Geeft de geschiedenis weer van de wijzigingen in compatibiliteit van een configuratie-item voor het opgegeven datumbereik.|  
|**Details van compatibele regels van configuratie-items in een configuratiebasislijn voor een asset**|Geeft informatie weer over de regels die als compatibel zijn geëvalueerd voor een opgegeven configuratie-item voor een opgegeven apparaat of gebruiker.|  
|**Details van conflicterende regels van configuratie-items in een configuratiebasislijn voor een asset**|Geeft informatie weer over regels in een geïmplementeerd configuratie-item die conflicteren met andere regels. Neem de andere regels op in hetzelfde of een ander geïmplementeerd configuratie-item.|  
|**Details van fouten van configuratie-items in een configuratiebasislijn voor een asset**|Geeft informatie weer over fouten die zijn gegenereerd door een opgegeven configuratie-item voor een opgegeven apparaat of gebruiker.|  
|**Details van niet-compatibele regels van configuratie-items in een configuratiebasislijn voor een asset**|Geeft informatie weer over regels die niet compatibel zijn bevonden voor een opgegeven configuratie-item voor een opgegeven apparaat of gebruiker.|  
|**Details van herstelde regels van configuratie-items in een configuratiebasislijn voor een asset**|Geeft informatie weer over regels die zijn hersteld door een opgegeven configuratie-item voor een opgegeven apparaat of gebruiker.|  
|**Lijst van assets op compatibiliteitsstatus voor een configuratiebasislijn**|Geeft de apparaten of gebruikers weer in een opgegeven compatibiliteitsstatus na de evaluatie van een opgegeven configuratiebasislijn.|  
|**Lijst van assets op compatibiliteitsstatus voor een configuratie-item in een configuratiebasislijn**|Geeft de apparaten of gebruikers weer in een opgegeven compatibiliteitsstatus na de evaluatie van een opgegeven configuratie-item.|  
|**Lijst met niet-compatibele apps en apparaten voor een opgegeven gebruiker**|Geeft informatie weer over gebruikers en apparaten die apps hebben geïnstalleerd die niet compatibel zijn met een beleid dat u hebt opgegeven.|  
|**Lijst met regels die conflicteren met een opgegeven regel voor een asset**|Geeft een lijst weer van regels die conflicteren met een opgegeven regel voor een geïmplementeerd configuratie-item.|  
|**Lijst met onbekende assets voor een configuratiebasislijn**|Geeft een lijst weer van apparaten of gebruikers die nog geen compatibiliteits gegevens hebben gerapporteerd voor een opgegeven configuratie basislijn.|  
|**Lijst met onbekende assets voor een configuratie-item**|Geeft een lijst weer van apparaten of gebruikers die nog geen compatibiliteits gegevens hebben gerapporteerd voor een opgegeven configuratie-item.|  
|**Samenvatting van regels en fouten van configuratie-items in een configuratiebasislijn voor een asset**|Geeft een samen vatting weer van de compatibiliteits status van de regels en eventuele instellings fouten voor een opgegeven configuratie-item. Het configuratie-item moet worden geïmplementeerd op een apparaat of gebruiker.|  
|**Samenvatting van compatibiliteit op configuratiebasislijn**|Geeft een samenvatting weer van de algemene compatibiliteit van geïmplementeerde configuratiebasislijnen in de hiërarchie.|  
|**Samenvatting van compatibiliteit op configuratie-items voor een configuratiebasislijn**|Geeft een samenvatting weer van de compatibiliteit van configuratie-items in een opgegeven configuratiebasislijn.|  
|**Samenvatting van naleving per configuratiebeleid**|Geeft een samenvatting van de naleving van configuratiebeleid.|  
|**Samenvatting van compatibiliteit voor een configuratiebasislijn voor een verzameling**|Geeft een samen vatting weer van de algemene compatibiliteit van een opgegeven configuratie basislijn. Het configuratie-item moet worden geïmplementeerd in de opgegeven verzameling.|  
|**Overzicht van gebruikers met niet-compatibele apps**|Geeft informatie weer over gebruikers die apps hebben geïnstalleerd die niet compatibel zijn met een beleid dat u hebt opgegeven.|  
|**Acceptatie van voorwaarden**|Geeft de voorwaarden weer en de versie die door elke gebruiker is geaccepteerd.|  



## <a name="data-warehouse"></a>Datawarehouse  

De volgende zeven rapporten worden vermeld in de categorie **Data Warehouse** . 

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Toepassingsimplementatie**|Historisch: Details voor toepassings implementaties voor een specifieke toepassing en computer weer geven.|
|**Endpoint Protection en software Updatenaleving**|Historisch: computers weer geven waarop software-updates ontbreken.|
|**Algemene Hardware-inventarisatie**|Historisch: alle hardware-inventarisatie voor een specifieke computer weer geven.|
|**Algemene software-inventarisatie**|Historisch: alle software-inventaris voor een specifieke computer weer geven.|
|**Overzicht van infrastructuur status**|Historisch: hier wordt een overzicht weer gegeven van de status van uw Configuration Manager-infra structuur.|
|**Lijst met gedetecteerde malware**|Historisch: schadelijke software weer geven die in de organisatie is gedetecteerd.|
|**Samen vatting van software distributie**|Historisch: een samen vatting van software distributie voor een specifieke advertentie en computer.|


## <a name="device-management"></a>Apparaatbeheer  

De volgende 37-rapporten worden vermeld in de categorie **Apparaatbeheer** . 

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle mobiele apparaten in bedrijfs eigendom**|Geeft alle mobiele apparaten weer die eigendom zijn van het bedrijf.|
|**Clients voor alle mobiele apparaten**|Geeft informatie weer over clients voor alle mobiele apparaten Apparaten die worden beheerd door de Exchange Server-connector, zijn niet opgenomen.|  
|**Certificaat problemen op mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE en die niet in orde zijn**|Geeft gedetailleerde informatie weer over certificaat problemen op mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE.|  
|**Mislukte client implementaties voor mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE**|Geeft gedetailleerde informatie weer over mislukte implementaties voor mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE.|  
|**Details van client implementatie status voor mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE**|Geeft informatie weer over de status van mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE.|  
|**Geslaagde clientimplementaties voor mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE**|Geeft gedetailleerde informatie weer over geslaagde implementaties voor mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE.|  
|**Communicatieproblemen op mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE en die zijn beschadigd**|Dit rapport bevat gedetailleerde informatie over communicatie problemen op mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE.|  
|**Nalevings status van het standaard ActiveSync-postvak beleid voor de mobiele apparaten die worden beheerd door de Exchange Server-connector**|Geeft een samen vatting weer van de compatibiliteits status met het standaard Exchange ActiveSync-postvak beleid voor de mobiele apparaten die worden beheerd door de Exchange Server-connector.|  
|**Aantal mobiele apparaten op weergave-instellingen**|Dit rapport bevat het aantal van mobiele apparaten op weergave-instellingen.|  
|**Aantal mobiele apparaten op besturingssysteem**|Geeft het aantal mobiele apparaten weer op het besturingssysteem.|  
|**Aantal mobiele apparaten op programmageheugen**|Geeft het aantal mobiele apparaten weer op programmageheugen.|  
|**Aantal mobiele apparaten op opslaggeheugenconfiguraties**|Aantal mobiele apparaten op opslaggeheugenconfiguraties|  
|**Statusinformatie voor mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE**|Geeft gedetailleerde status informatie weer voor mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE.|  
|**Statussamenvatting voor mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE**|Geeft informatie weer over de status van mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE.|  
|**Inactieve apparaten die worden beheerd door de Exchange Server-connector**|Geeft de mobiele apparaten weer die worden beheerd door de Exchange Server-connector en die geen verbinding hebben gemaakt met een Exchange-server in een opgegeven aantal dagen.|  
|**Lijst met apparaten op Health Attestation-status**|Geeft een lijst weer van apparaten met kenmerken die zijn gerapporteerd door de Health Attestation-service|
|**Lijst met apparaten die per gebruiker zijn ingeschreven bij Microsoft Intune**|Geeft alle apparaten weer die een gebruiker heeft inge schreven bij Microsoft Intune.|  
|**Lijst met apparaten in een specifieke apparaatcategorie**|Geeft informatie weer voor alle apparaten in een specifieke apparaatcategorie.|
|**Problemen met lokale clients op mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE en die zijn beschadigd**|Dit rapport bevat gedetailleerde informatie over problemen met lokale clients op mobiele apparaten die worden beheerd door de Configuration Manager-client voor Windows CE.|  
|**Informatie over mobiele-apparaatclient**|Geeft informatie weer over de mobiele apparaten waarop de Configuration Manager-client is geïnstalleerd. U kunt dit rapport gebruiken om te controleren welke mobiele apparaten kunnen communiceren met een beheerpunt.|  
|**Compatibiliteitsdetails voor mobiele apparaten voor de Exchange Server-connector**|Geeft compatibiliteitsdetails voor mobiele apparaten voor een standaard Exchange ActiveSync-postvakbeleid dat is geconfigureerd met behulp van de Exchange Server-connector.|  
|**Mobiele apparaten op besturingssysteem**|Geeft de mobiele apparaten weer op besturingssysteem.|  
|**Mobiele apparaten die zijn opengebroken of geroot**|Geeft de mobiele apparaten weer die zijn opengebroken of geroot.|  
|**Mobiele apparaten die niet beheerd zijn omdat ze zijn geregistreerd maar niet aan een site zijn toegewezen**|Geeft de mobiele apparaten weer die de registratie met Configuration Manager hebben voltooid, een certificaat hebben, maar de site toewijzing niet volt ooien.|  
|**Mobiele apparaten met een specifieke hoeveelheid vrij programmageheugen**|Geeft alle mobiele apparaten weer met een specifieke hoeveelheid vrij programmageheugen.|  
|**Mobiele apparaten met een specifieke hoeveelheid vrij verwisselbaar geheugen**|Geeft alle mobiele apparaten weer met een specifieke hoeveelheid vrij verwijderbaar geheugen.|  
|**Mobiele apparaten met problemen bij het verlengen van het certificaat**|Geeft de geregistreerde apparaten weer waarvan het verlengen van het certificaat is mislukt. Als u het certificaat niet vóór de verloop periode verlengt, worden de mobiele apparaten onbeheerd.|  
|**Mobiele apparaten met weinig vrij programmageheugen (minder dan opgegeven aantal KB vrij)**|Geeft de mobiele apparaten weer waarvoor het programmageheugen lager is dan een opgegeven grootte in KB.|  
|**Mobiele apparaten met weinig vrij verwijderbaar geheugen (minder dan opgegeven aantal KB vrij)**|Geeft de mobiele apparaten weer waarvoor het verwijderbare geheugen lager is dan een opgegeven grootte in KB.|  
|**Aantal apparaten dat per gebruiker is inge schreven bij Microsoft Intune**|Hier worden de gebruikers weer gegeven die zijn ingeschakeld voor het Microsoft Intune-abonnement. Ook wordt het totale aantal apparaten weer gegeven dat voor elke gebruiker is inge schreven.|  
|**Aanvraag voor buiten gebruiks telling en wissen voor mobiele apparaten**|Geeft de verzoeken om te wissen weer die in behandeling zijn voor mobiele apparaten.|  
|**Recent geregistreerde en toegewezen mobiele apparaten**|Geeft mobiele apparaten weer die recent zijn geregistreerd bij Configuration Manager en die aan een site zijn toegewezen.|  
|**Recent gewiste mobiele apparaten**|Geeft de mobiele apparaten weer die zijn recent zijn gewist.|  
|**Samenvatting van instellingen voor mobiele apparaten die worden beheerd door de Exchange Server-connector**|Geeft het aantal mobiele apparaten weer dat de instellingen toepast voor elk standaard Exchange ActiveSync-postvak beleid dat wordt beheerd door de Exchange Server-connector.|  
|**Gedetailleerde status van Windows RT-sideloading-codes**|Geeft gedetailleerde statusinformatie weer voor een opgegeven Windows RT-sideloading-code|  
|**Samenvatting van Windows RT-sideloading-codes**|Geeft de status weer van Windows RT sideloading-codes.|  



## <a name="driver-management"></a>Stuurprogrammabeheer  

De volgende 13 rapporten worden vermeld in de categorie **stuurprogrammabeheer** . 

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle stuurprogramma's**|Geeft een lijst van alle stuurprogramma’s weer.|  
|**Alle stuurprogramma's voor een specifiek platform**|Geeft alle stuurprogramma's voor een opgegeven platform weer.|  
|**Alle stuurprogramma's in een specifieke installatiekopie**|Geeft alle stuurprogramma's in een opgegeven installatiekopie weer.|  
|**Alle stuurprogramma's in een specifieke categorie**|Geeft alle stuurprogramma's in een opgegeven categorie weer.|  
|**Alle stuurprogramma's in een specifiek pakket**|Geeft alle stuurprogramma's in een opgegeven pakket weer.|  
|**Categorieën voor een specifiek stuurprogramma**|Geeft de categorieën voor een opgegeven stuurprogramma weer.|  
|**Computers waarop geen stuurprogramma's konden worden geïnstalleerd voor een specifieke verzameling**|Geeft computers weer waarop geen stuurprogramma's konden worden geïnstalleerd voor een opgegeven verzameling.|  
|**Stuurprogrammacatalogus die overeenkomt met een rapport voor een specifieke verzameling**|Geeft de stuurprogrammacatalogus weer die overeenkomt met een rapport voor een opgegeven verzameling.|  
|**Stuurprogrammacatalogus die overeenkomt met een rapport voor een specifieke computer**|Geeft de stuurprogrammacatalogus weer die overeenkomt met een rapport voor een opgegeven computer.|  
|**Stuurprogrammacatalogus die overeenkomt met een rapport voor een specifiek apparaat op een specifieke computer**|Geeft de stuurprogrammacatalogus weer die overeenkomt met een rapport voor een opgegeven apparaat op een opgegeven computer|  
|**Stuurprogrammacatalogus die overeenkomt met een rapport voor computers in een specifieke verzameling met een specifiek apparaat**|Geeft een stuurprogrammacatalogus weer die overeenkomt met een rapport voor computers in een specifieke verzameling met een specifiek apparaat.|  
|**Stuurprogramma's die niet konden worden geïnstalleerd op een specifieke computer**|Geeft de stuurprogramma's weer die niet konden worden geïnstalleerd op een opgegeven computer.|  
|**Ondersteunde platforms voor een specifiek stuurprogramma**|Geeft ondersteunde platforms weer voor een opgegeven stuurprogramma|  



## <a name="endpoint-protection"></a>Endpoint Protection  

De volgende zes rapporten worden vermeld in de categorie **Endpoint Protection** . 

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Rapport activiteit tegen malware**|Geeft een overzicht van activiteit tegen malware.|  
|**Algemene status en geschiedenis van antimalware**|Geeft de algemene status en geschiedenis weer van antimalware.|  
|**Details van computermalware**|Geeft details weer over een opgegeven computer, en een lijst met de malware die erop is aangetroffen.|  
|**Geïnfecteerde computers**|Geeft een lijst weer van computers waarop een opgegeven bedreiging is gedetecteerd.|  
|**Meest voorkomende gebruikers op bedreigingen**|Geeft de lijst weer met de gebruikers met het hoogste aantal gedetecteerde bedreigingen.|  
|**Lijst met bedreigingen voor gebruiker**|Geeft een lijst met bedreigingen weer voor een opgegeven gebruikersaccount.|  



## <a name="hardware---cd-rom"></a>Hardware-CD-ROM  

De volgende vier rapporten worden vermeld in de categorie **Hardware-cd-rom** . 

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Cd-romstations voor een specifieke computer**|Geeft informatie weer over de cd-romstations op een opgegeven computer.|  
|**Computers voor een specifieke cd-romfabrikant**|Geeft een lijst weer met computers met een cd-romstation van een door u opgegeven fabrikant.|  
|**Aantal cd-romstations per fabrikant**|Geeft het aantal cd-romstations weer dat is geïnventariseerd per fabrikant.|  
|**Geschiedenis-CD-ROMSTATION voor een specifieke computer**|Geeft de geïnventariseerde cd-romgeschiedenis voor een opgegeven computer weer.|  



## <a name="hardware---disk"></a>Hardware-schijf  

De volgende acht rapporten worden vermeld in de categorie **Hardware-Disk** . 

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers met een specifieke vasteschijfgrootte**|Geeft een lijst weer van computers met een opgegeven vasteschijfgrootte.|  
|**Computers met weinig vrije ruimte (minder dan opgegeven percentage vrij)**|Geeft een lijst weer van computers in een opgegeven verzameling die minder dan de opgegeven beschikbare schijfruimte hebben.|  
|**Computers met weinig vrije ruimte (minder dan opgegeven aantal MB vrij)**|Geeft een lijst weer van computers en schijven met weinig schijfruimte. De grootte van de te controleren vrije ruimte is opgegeven in MB.|  
|**Fysieke schijfconfiguraties tellen**|Geeft het aantal harde schijven weer dat is geïnventariseerd op schijfcapaciteit.|  
|**Schijf informatie voor een specifieke computer-logische schijven**|Geeft een samenvatting weer van informatie over logische schijven op een opgegeven computer.|  
|**Schijfinformatie voor een specifieke computer - Partities**|Geeft een samenvatting weer van informatie over schijfpartities op een opgegeven computer.|  
|**Schijfinformatie voor een specifieke computer - Fysieke schijven**|Geeft een samenvatting weer van informatie over fysieke schijven op een opgegeven computer.|  
|**Geschiedenis - Geschiedenis van logischeschijfruimte voor een specifieke computer**|Geeft de inventarisgeschiedenis weer voor logischeschijfstations op een opgegeven computer.|  



## <a name="hardware---general"></a>Hardware-algemeen  

De volgende vijf rapporten worden vermeld in de categorie **Hardware-algemeen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computerinformatie voor een specifieke computer**|Geeft de computerinformatie weer voor een opgegeven computer|  
|**Computers in een specifieke werkgroep of een specifiek domein**|Geeft een lijst weer van computers in een opgegeven werkgroep of domein.|  
|**Inventarisatieklassen die zijn toegewezen aan een specifieke verzameling**|Geeft een lijst weer van de inventarisatieklassen die zijn toegewezen aan een opgegeven verzameling.|  
|**Inventarisatieklassen die zijn ingeschakeld op een specifieke computer**|Geeft de inventarisatieklassen weer die zijn ingeschakeld op een opgegeven computer.|  
|**Gegevens van Windows auto pilot-apparaat**|Geeft informatie weer over het client apparaat dat nodig is voor de registratie van Windows auto pilot.|



## <a name="hardware---memory"></a>Hardware-geheugen  

De volgende vijf rapporten worden vermeld in de categorie **Hardware-geheugen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers waarbij het fysieke geheugen is gewijzigd**|Geeft een lijst met computers weer waarbij de hoeveelheid RAM is gewijzigd sinds de laatste inventarisatiecyclus.|  
|**Computers met een specifieke hoeveelheid geheugen**|Geeft een lijst weer met computers met een opgegeven hoeveelheid RAM (totaal fysiek geheugen afgerond naar het dichtstbijzijnde aantal MB).|  
|**Computers met weinig geheugen (minder dan of gelijk aan opgegeven aantal MB)**|Geeft een lijst met computers weer die weinig geheugen hebben  De hoeveelheid te controleren geheugen is opgegeven in MB.|  
|**Geheugenconfiguraties tellen**|Geeft het aantal computers weer dat is geïnventariseerd op hoeveelheid RAM.|  
|**Geheugeninformatie voor een specifieke computer**|Geeft een samenvatting weer van informatie over het geheugen op een opgegeven computer.|  



## <a name="hardware---modem"></a>Hardware-modem  

De volgende drie rapporten worden vermeld in de categorie **hardware-modem** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers voor een specifieke modemfabrikant**|Geeft een lijst weer van computers met een modem van een opgegeven fabrikant.|  
|**Modems tellen op fabrikant**|Geeft het aantal modems weer dat is geïnventariseerd voor elke modemfabrikant.|  
|**Modeminformatie voor een specifieke computer**|Geeft samenvattingsinformatie weer over het modem op een opgegeven computer.|  



## <a name="hardware---network-adapter"></a>Hardware-netwerk adapter  

De volgende drie rapporten worden vermeld in de categorie **hardware-netwerk adapter** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers met een specifieke netwerkadapter**|Geeft een lijst weer van computers met een opgegeven netwerkadapter.|  
|**Netwerkadapters tellen op type**|Geeft het aantal geïnventariseerde netwerkadapterkaarten weer van elk type.|  
|**Netwerkadapterinformatie voor een specifieke computer**|Geeft informatie weer over de netwerkadapters die zijn geïnstalleerd op een opgegeven computer.|  



## <a name="hardware---processor"></a>Hardware-processor  

De volgende vijf rapporten worden vermeld in de categorie **Hardware-processor** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers voor een specifieke processorsnelheid**|Geeft een lijst weer van computers met een processor met een opgegeven snelheid.|  
|**Computers met een snelle processor (even snel als of sneller dan een opgegeven kloksnelheid)**|Geeft een lijst weer met computers met een processor die sneller is dan de opgegeven snelheid.|  
|**Computers met een trage processor (even snel als of trager dan een opgegeven kloksnelheid)**|Geeft een lijst weer van computers met een processor die even snel als of trager dan een opgegeven kloksnelheid zijn.|  
|**Processorsnelheden tellen**|Geeft het aantal computers weer dat is geïnventariseerd op processorsnelheid.|  
|**Processorinformatie voor een specifieke computer**|Geeft informatie weer over de processors die zijn geïnstalleerd op een opgegeven computer.|  



## <a name="hardware---scsi"></a>Hardware-SCSI  

De volgende vijf rapporten worden vermeld in de categorie **Hardware-SCSI** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers met een specifiek type SCSI-kaart**|Geeft een lijst weer van computers met een opgegeven type SCSI-kaart.|  
|**SCSI-kaarttypen tellen**|Geeft het aantal geïnventariseerde SCSI-kaarten weer op kaarttype.|  
|**SCSI-kaartinformatie voor een specifieke computer**|Geeft informatie weer over de SCSI-kaarten die zijn geïnstalleerd op een opgegeven computer.|  



## <a name="hardware---security"></a>Hardware-beveiliging

De volgende twee rapporten worden vermeld in de categorie **Hardware-beveiliging** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Details van de status van de firmware op apparaten**|Geeft de details weer van de statussen van UEFI, SecureBoot en TPM. **Opmerking**: dit rapport is niet in versie 1810.<!--SCCMDocs issue #1189-->|  



## <a name="hardware---sound-card"></a>Hardware-geluids kaart  

De volgende drie rapporten worden vermeld in de categorie **Hardware-SCSI** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers met een specifieke geluidskaart**|Geeft een lijst weer van computers met een opgegeven geluidskaart.|  
|**Geluidskaarten tellen**|Geeft het aantal computers weer dat is geïnventariseerd op elk type geluidskaart.|  
|**Geluidskaartinformatie voor een specifieke computer**|Geeft samenvattingsinformatie weer over de geluidskaarten op een opgegeven computer.|  



## <a name="hardware---video-card"></a>Hardware-video kaart  

De volgende drie rapporten worden vermeld in de categorie **hardware-video kaart** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers met een specifieke geluidskaart**|Geeft een lijst weer van computers met een opgegeven videokaart.|  
|**Videokaarten op type tellen**|Geeft een lijst weer van alle video kaarten die op computers zijn geïnstalleerd. Het bevat ook het aantal van elk type video kaart.|  
|**Videokaartinformatie voor een specifieke computer**|Geeft samenvattingsinformatie weer over de videokaarten die zijn geïnstalleerd op een opgegeven computer.|  



## <a name="migration"></a>Migratie  

De volgende vijf rapporten worden vermeld in de categorie **migratie** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Clients in uitsluitingslijst**|Geeft clients weer die zijn uitgesloten van migratie.|  
|**Afhankelijkheid van een Configuration Manager-verzameling**|Geeft de objecten weer die afhankelijk zijn van een verzameling van de bronhiërarchie|  
|**Eigenschappen migratietaak**|In dit rapport wordt de inhoud weer van de opgegeven migratietaak weergegeven.|  
|**Migratietaken**|In dit rapport wordt de lijst met migratietaken weergegeven.|  
|**Objecten die niet konden migreren**|Geeft een lijst weer met objecten die niet konden migreren tijdens de laatste poging.|  



## <a name="network"></a>Netwerk  

De volgende zes rapporten worden vermeld in de categorie **netwerk** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**IP-adressen per subnet tellen**|Geeft het aantal IP-adressen weer dat voor elk IP-subnet is geïnventariseerd.|  
|**IP-alle subnetten op subnetmasker**|Geeft een lijst weer met IP-subnetten en subnetmaskers.|  
|**IP-computers in een specifiek subnet**|Geeft een lijst weer van computers en IP-informatie voor een opgegeven IP-subnet.|  
|**IP-informatie voor een specifieke computer**|Geeft samenvattingsinformatie weer over het IP op een opgegeven computer.|  
|**IP-informatie voor een specifiek IP-adres**|Geeft samenvattingsinformatie weer over een opgegeven IP-adres.|  
|**MAC-computers voor een specifiek MAC-adres**|Geeft de computernaam en het IP-adres weer van computers dat het opgegeven MAC-adres hebben.|  



## <a name="operating-system"></a>Besturingssysteem  

De volgende 10 rapporten worden vermeld in de categorie **besturings systeem** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Versiegeschiedenis besturingssysteem van computer**|Geeft de inventarisgeschiedenis weer voor het besturingssysteem op een opgegeven computer.|  
|**Computers met een specifiek besturingssysteem**|Geeft computers weer met een opgegeven besturingssysteem.|  
|**Computers met een specifiek besturingssysteem en servicepack**|Geeft computers weer met een specifiek besturingssysteem en servicepack.|  
|**Versies besturingssystemen tellen**|Geeft het aantal computers weer dat is geïnventariseerd op besturingssysteem.|  
|**Besturingssystemen en servicepacks tellen**|Geeft het aantal computers weer dat is geïnventariseerd op combinaties van besturingssysteem en service pack.|  
|**Services - Computers waarop een specifieke service wordt uitgevoerd**|Geeft een lijst weer van computers waarop een opgegeven service wordt uitgevoerd.|  
|**Services - Computers waarop Remote Access Server wordt uitgevoerd**|Geeft een lijst weer van computers waarop Remote Access Server wordt uitgevoerd.|  
|**Service - Services voor een specifieke computer**|Geeft samenvattingsinformatie weer over de services op een opgegeven computer.|  
|**Windows 10-onderhouds Details voor een specifieke verzameling**|Geeft algemene informatie over Windows 10-onderhoud voor een bepaalde verzameling weer.|
|**Windows Server-computers**|Geeft een lijst met computers weer waarop Windows Server-besturingssystemen worden uitgevoerd.|  


## <a name="power-management"></a>Energiebeheer  

De volgende 18 rapporten worden vermeld in de categorie **energie beheer** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Energie beheer-computer activiteit**|Geeft een grafiek weer met monitor-, computer-en gebruikers activiteit voor een opgegeven verzameling gedurende een opgegeven periode.|  
|**Energie beheer-computer activiteit per computer**|Geeft een grafiek weer met monitor-, computer-en gebruikers activiteit voor een opgegeven computer op een opgegeven datum.|  
|**Energie beheer-Details van computer activiteit**|Geeft een lijst weer van de slaapstandmogelijkheden van computers in de opgegeven verzameling voor een opgegeven datum en tijd.|  
|**Energie beheer-computer Details**|Geeft gedetailleerde informatie weer over de energie mogelijkheden, energie-instellingen en energiebeheer schema's die worden toegepast op een opgegeven computer.|  
|**Energie beheer-computer meldt geen Details**|Geeft een lijst weer van computers waar waarvoor op een opgegeven datum en tijdstip geen stroomactiviteit is gerapporteerd.|  
|**Energie beheer-uitgesloten computers**|Geef een lijst weer van computers die zijn uitgesloten van het energiebeheerschema.|  
|**Energie beheer-computers met meerdere energiebeheer schema's**|Geeft een lijst weer van computers waarop meerdere, conflicterende energiebeheerschema’s zijn toegepast.|  
|**Energie beheer-energie verbruik**|Geeft het totale maandelijkse energieverbruik weer (in kWh) voor een opgegeven verzameling gedurende een opgegeven periode.|  
|**Energie beheer-energie verbruik per dag**|Geeft het totale energieverbruik weer (in kWh) voor de afgelopen 31 dagen voor een opgegeven verzameling.|  
|**Energie beheer-energie kosten**|Geeft de kosten van het totale maandelijkse energieverbruik weer voor een opgegeven verzameling gedurende een opgegeven periode.|  
|**Energie beheer-energie kosten per dag**|Geeft de kosten van het totale energieverbruik weer voor een opgegeven verzameling gedurende de afgelopen 31 dagen.|  
|**Energie beheer-gevolgen voor het milieu**|Geeft een grafiek weer met CO2-uitstoot die wordt gegenereerd door een specifieke verzameling gedurende een specifieke periode.|  
|**Energie beheer-gevolgen voor het milieu per dag**|Geeft een grafiek weer met CO2-uitstoot die wordt gegenereerd door een specifieke verzameling gedurende de afgelopen 31 dagen.|  
|**Energie beheer-Details van slapeloosheid computer**|Geeft gedetailleerde informatie weer over computers die niet in de slaap-of sluimer stand staan binnen een opgegeven periode.|  
|**Energie beheer-slapeloosheid-rapport**|Geeft een lijst met algemene oorzaken weer die verhinderen dat computers in de slaap-of sluimer stand worden gezet. Het bevat ook het aantal computers waarop elke oorzaak van toepassing is gedurende een opgegeven periode.|  
|**Energie beheer-energie mogelijkheden**|Geeft de mogelijkheden voor energiebeheer weer van computers in de opgegeven verzameling.|  
|**Energie beheer-energie-instellingen**|Geeft een samengevoegde lijst energie-instellingen weer die worden gebruikt door computers in een opgegeven verzameling.|  
|**Energie beheer-Details van energie-instellingen**|Wordt gebruikt om meer informatie weer te geven over computers die zijn opgegeven in het rapport **energie beheer-energie-instellingen** .|  



## <a name="replication-traffic"></a>Replicatie verkeer  

De volgende 10 rapporten worden vermeld in de categorie **replicatie verkeer** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Replicatieverkeer van globale gegevens per koppeling (lijndiagram)**|Geeft het totale replicatieverkeer van globale gegevens weer voor een opgegeven koppeling gedurende een opgegeven aantal dagen|  
|**Replicatieverkeer van globale gegevens per koppeling (cirkeldiagram)**|Geeft het totale replicatieverkeer van globale gegevens weer voor een opgegeven koppeling gedurende een opgegeven aantal dagen|  
|**Hiërarchie van replicatieverkeer per koppeling**|Geeft het totale replicatieverkeer weer voor elke koppeling in de hiërarchie gedurende een opgegeven aantal dagen.|  
|**Top tien van de replicatiegroepen in de gehele hiërarchie per koppeling (cirkeldiagram)**|Geeft het replicatie verkeer weer voor de Top 10 van replicatie groepen in de gehele hiërarchie geïdentificeerd door de koppeling.|  
|**Replicatiekoppelingsverkeer**|Geeft het totale replicatieverkeer weer voor alle gegevens gedurende een opgegeven aantal dagen.|  
|**Verkeer van de replicatiegroep per koppeling**|Geeft het netwerkverkeer van de replicatiegroep weer via een opgegeven replicatiekoppeling in de database, gedurende een opgegeven aantal dagen.|  
|**Replicatieverkeer van sitegegevens per koppeling (lijndiagram)**|Geeft het totale replicatieverkeer van sitegegevens weer voor een opgegeven koppeling gedurende een opgegeven aantal dagen|  
|**Replicatieverkeer van sitegegevens per koppeling (cirkeldiagram)**|Geeft het totale replicatieverkeer van sitegegevens weer voor een opgegeven koppeling gedurende een opgegeven aantal dagen|  
|**Totale hiërarchie van replicatieverkeer (lijndiagram)**|Geeft de verzamelde globale gegevens in de hiërarchie en gegevensreplicatie van de site weer voor elke richting van elke koppeling gedurende een opgegeven aantal dagen.|  
|**Totale hiërarchie van replicatieverkeer (cirkeldiagram)**|Geeft de verzamelde globale gegevens in de hiërarchie en gegevensreplicatie van de site weer voor elke richting van elke koppeling gedurende een opgegeven aantal dagen.|  



## <a name="site---client-information"></a>Site-client informatie  

De volgende 19 rapporten worden vermeld in de categorie **site-client informatie** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Gedetailleerd rapport van clienttoewijzing**|Geeft gedetailleerde informatie weer over de status van clienttoewijzingen.|  
|**Foutdetails van clienttoewijzing**|Geeft gedetailleerde informatie weer over mislukte clienttoewijzingen.|  
|**Statusdetails van clienttoewijzing**|Geeft overzichtsinformatie weer over de status van clienttoewijzingen.|  
|**Details van slagen van clienttoewijzing**|Geeft gedetailleerde informatie weer over geslaagde clienttoewijzingen.|  
|**Rapport over fouten clientimplementatie**|Geeft gedetailleerde informatie weer voor clients die niet kunnen worden geïmplementeerd.|  
|**Statusdetails clientimplementatie**|Geeft samenvattingsinformatie weer voor de status van clientinstallaties.|  
|**Rapport over geslaagde clientimplementatie**|Geeft gedetailleerde informatie weer voor clients waarvan de implementatie is geslaagd.|  
|**Clients waarvoor HTTPS-communicatie niet mogelijk is**|Geeft gedetailleerde informatie weer over elke client die de HTTPS Communication Readiness Tool uitvoert en rapporten die niet kunnen communiceren via HTTPS.|  
|**   Computers die zijn toegewezen maar niet geïnstalleerd voor een bepaalde site **|Geeft een lijst weer van computers die zijn toegewezen aan een opgegeven site, maar die niet aan die site rapporteren.|  
|**Computers met een specifieke Configuration Manager-clientversie**|Geeft een lijst weer van computers waarop een opgegeven versie van de Configuration Manager-client software wordt uitgevoerd.|  
|**Telling van clients en protocol gebruikt voor communicatie**|Geeft een samenvatting weer van de communicatiemethoden die door clients worden gebruikt (HTTP of HTTPS).|  
|**Telling van clients die zijn toegewezen en geïnstalleerd voor elke site**|Geeft het aantal computers weer dat is toegewezen en geïnstalleerd voor elke site Clients met een netwerk locatie die is gekoppeld aan meerdere sites, worden alleen geteld als geïnstalleerd als ze aan die site rapporteren.|  
|**Aantal clients waarvoor HTTPS-communicatie mogelijk is**|Geeft gedetailleerde informatie weer over elke client die de HTTPS Communication Readiness Tool uitvoert, en rapporten die geschikt of niet kunnen communiceren via HTTPS.|  
|**Telling van clients voor elke site**|Geeft het aantal Configuration Manager-clients weer dat door site code is geïnstalleerd.|  
|**Telling van Configuration Manager-clients op clientversies**|Geeft het aantal computers weer dat is gedetecteerd door de Configuration Manager-client versie.|  
|**Details van probleem gerapporteerd aan het terugvalstatuspunt voor een opgegeven verzameling**|Geeft gedetailleerde informatie weer voor problemen die worden gerapporteerd door clients in een opgegeven verzameling. Deze clients moeten een toegewezen terugval status punt hebben.|  
|**Details van probleem gerapporteerd aan het terugvalstatuspunt voor een opgegeven site**|Geeft gedetailleerde informatie weer over problemen die worden gerapporteerd door clients in een opgegeven site. Deze clients moeten een toegewezen terugval status punt hebben.|  
|**Samenvatting van problemen die worden gerapporteerd aan het terugvalstatuspunt**|Geeft informatie weer over alle problemen die door clients worden gerapporteerd. Deze clients moeten een toegewezen terugval status punt hebben.|  
|**Samenvatting van problemen die zijn gerapporteerd aan het terugvalstatuspunt voor een opgegeven verzameling**|Geeft samenvattings informatie weer voor problemen die worden gerapporteerd door clients in een opgegeven verzameling. Deze clients moeten een toegewezen terugval status punt hebben.|  



## <a name="site---discovery-and-inventory-information"></a>Site-informatie over detectie en inventaris  

De volgende 10 rapporten worden vermeld in de categorie **site-detectie en inventarisatie-informatie** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Clients die recent niets hebben gerapporteerd (gedurende een opgegeven aantal dagen)**|Geeft een lijst weer van clients die gedurende een opgegeven aantal dagen geen detectie gegevens, Hardware-inventarisatie of software-inventarisatie hebben gerapporteerd.|  
|**Computers die door een specifieke site zijn gedetecteerd**|Geeft een lijst weer van alle computers die de opgegeven site heeft gedetecteerd. Ook de datum van de meest recente detectie wordt weer gegeven.|  
|**Computers die recent zijn gedetecteerd op detectiemethode**|Geeft een lijst weer van computers die de site heeft gedetecteerd binnen het opgegeven aantal dagen. Er wordt ook een lijst weer gegeven met de agents die ze hebben gedetecteerd. Als meerdere agents een computer hebben gedetecteerd, kan deze meer dan één keer in de lijst worden weer gegeven.|  
|**Computers niet recent gedetecteerd (in een opgegeven aantal dagen)**|Geeft een lijst weer van computers die de site niet recent heeft gedetecteerd. Ook wordt het aantal dagen weer gegeven sinds de site de computer heeft gedetecteerd.|  
|**Computers niet recent geïnventariseerd (in een opgegeven aantal dagen)**|Geeft een lijst weer van computers die niet recent zijn geïnventariseerd op de site. Het toont ook de laatste keer dat de client de computer heeft geïnventariseerd.|  
|**Computers die mogelijk dezelfde unieke Configuration Manager-id delen**|Geeft een lijst weer van computers waarvan de naam is veranderd. Een wijziging in naam is een mogelijk symptoom dat een computer een Configuration Manager unieke id deelt met een andere computer.|  
|**Computers met dubbele MAC-adressen**|Geeft computers weer die een MAC-adres delen.|  
|**Computers in resourcedomeinen of werkgroepen tellen**|Geeft het aantal computers in elk resourcedomein of elke werkgroep weer|  
|**Detectie-informatie voor een specifieke computer**|Geeft een lijst weer van de agents en sites die een opgegeven computer hebben gedetecteerd.|  
|**Inventarisatiedatums voor een specifieke computer**|Geeft de datum en tijd weer waarop voor het laatst een inventarisatie op een opgegeven computer is uitgevoerd.|  



## <a name="site---general"></a>Site - Algemeen  

De volgende drie rapporten worden vermeld in de categorie **site-algemeen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers in een specifieke site**|Geeft een lijst weer van clientcomputers in een opgegeven site.|  
|**Sitestatus voor de hiërarchie**|Geeft de lijst weer van sites in de hiërarchie met siteversie en informatie over de sitestatus.|  
|**Status van Configuration Manager-update in de hiërarchie.**|Geeft informatie weer over Configuration Manager site-updates voor de hiërarchie.|  



## <a name="site---server-information"></a>Site-server informatie  

De volgende rapporten worden vermeld in de categorie **site-server informatie** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Sitesysteemrollen en sitesysteemservers voor een specifieke site**|Geeft een lijst weer voor de sitesysteemserver en de bijbehorende sitesysteemrollen voor een opgegeven site.|  



## <a name="software---companies-and-products"></a>Software-bedrijven en producten  

De volgende 15 rapporten worden vermeld in de categorie **software-bedrijven en producten** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle geïnventariseerde producten voor een specifiek softwarebedrijf**|Geeft een lijst weer met de geïnventariseerde softwareproducten en versies van een opgegeven bedrijf.|  
|**Alle softwarebedrijven**|Geeft een lijst weer van alle bedrijven die geïnventariseerde software produceren.|  
|**Alle Windows-apps**|Geeft een samen vatting weer van geïnstalleerde Windows-apps. De zoek opdracht zoekt aan de hand van de volgende criteria: toepassings naam,-architectuur of-uitgever.|  
|**Computers met een specifiek product**|Geeft een lijst weer van de computers waarop een opgegeven product is geïnventariseerd, en van de versies van dat product.|  
|**Computers met een specifieke productnaam en -versie**|Geeft een lijst weer van de computers waarop een opgegeven versie van een product is geïnventariseerd.|  
|**Computers met specifieke software die is geregistreerd in Software**|Geeft een samenvatting weer van alle computers met opgegeven software die is geregistreerd in Software of Programma’s en onderdelen.|  
|**Alle geïnventariseerde producten en versies tellen**|Geeft een lijst weer van de geïnventariseerde softwareproducten en versies en van het aantal computers waar deze op zijn geïnstalleerd.|  
|**Geïnventariseerde producten en versies voor een specifiek product**|Geeft een lijst weer van de geïnventariseerde versies van een opgegeven product en van het aantal computers waar deze op zijn geïnstalleerd.|  
|**Telling van alle exemplaren van software die is geregistreerd met Software**|Geeft een samenvatting weer van alle exemplaren van software die is geïnstalleerd en geregistreerd met Software of Programma’s en onderdelen op computers binnen de opgegeven verzameling.|  
|**Telling van exemplaren van specifieke software die is geregistreerd met Software**|Geeft een telling weer van exemplaren voor opgegeven softwarepakketten die zijn geïnstalleerd en geregistreerd in Software of Programma’s en onderdelen.|  
|**Aantal standaard browsers**|Hiermee wordt het aantal clients met een specifieke webbrowser weer gegeven als de Windows-standaard instelling. <br>Gebruik de volgende referentie voor algemene BrowserProgIDs:<br> -AppXq0fevzme2pys62n3e0fbqa7peapykr8v: micro soft Edge<br> IE. HTTP: micro soft Internet Explorer<br> -ChromeHTML: Google Chrome<br> -OperaStable: Opera Software<br> -FirefoxURL-308046B0AF4A39CB: Mozilla Firefox<br> -Onbekend: het besturings systeem van de client biedt geen ondersteuning voor de query, de query is niet uitgevoerd of de gebruiker is niet aangemeld|
|**Installaties van opgegeven Windows-apps**|Dit rapport geeft een lijst weer van alle computers met een opgegeven Windows-app.|  
|**Producten op een specifieke computer**|Geeft een samenvatting weer van de geïnventariseerde softwareproducten en de fabrikanten daarvan op een opgegeven computer.|  
|**Software die is geregistreerd in Software op een specifieke computer**|Geeft een samenvatting weer van de software die is geïnstalleerd op een opgegeven computer en die is geregistreerd in Software of Programma’s en onderdelen.|  
|**Windows-apps geïnstalleerd voor de opgegeven gebruiker**|Bevat alle Windows-apps die zijn geïnstalleerd voor de opgegeven gebruiker|  



## <a name="software---files"></a>Software - Bestanden  

De volgende vijf rapporten worden vermeld in de categorie **software-bestanden** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle geïnventariseerde bestanden voor een specifiek product**|Geeft een samenvatting weer van de geïnventariseerde bestanden die zijn gekoppeld aan een opgegeven softwareproduct.|  
|**Alle geïnventariseerde bestanden op een specifieke computer**|Geeft een samenvatting weer van alle bestanden die zijn geïnventariseerd op een opgegeven computer.|  
|**Software-inventarisatie op twee computers weergeven**|Geeft de verschillen weer tussen de software-inventarisatie die is gerapporteerd op twee opgegeven computers.|  
|**Computers met een specifiek bestand**|Geeft een lijst weer van computers met een verzamelde software-inventarisatie voor een opgegeven bestandsnaam. Als een computer meerdere kopieën van het bestand bevat, kan deze meer dan één keer in de lijst worden weer gegeven.|  
|**Computers met een specifieke bestandsnaam tellen**|Geeft het aantal computers weer met een verzamelde software-inventarisatie voor een opgegeven bestand.|  



## <a name="software-distribution---application-monitoring"></a>Software distributie-toepassings bewaking  

De volgende 10 rapporten worden vermeld in de categorie **software distributie-toepassings bewaking** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle toepassingsimplementaties (geavanceerd)**|Geeft gedetailleerde samenvattingsinformatie weer voor alle software-implementaties.|  
|**Alle toepassingsimplementaties (basis)**|Geeft samenvattingsinformatie weer voor alle software-implementaties.|  
|**Toepassingscompatibiliteit**|Geeft gedetailleerde informatie weer over de compatibiliteit van de opgegeven toepassing binnen de opgegeven verzameling.|  
|**Toepassingsimplementaties per asset**|Geeft toepassingen weer die zijn geïmplementeerd naar een opgegeven apparaat of gebruiker.|  
|**Fouten in toepassingsinfrastructuur**|Geeft de fouten in de toepassingsinfrastructuur weer. Deze fouten zijn onder andere interne infrastructuur problemen of fouten die voortkomen uit ongeldige regels voor vereisten.|  
|**Gedetailleerde status toepassingsgebruik**|Geeft gebruiksdetails weer voor geïnstalleerde toepassingen.|  
|**Status van samenvatting van toepassingsgebruik**|Geeft een gebruikssamenvatting weer voor geïnstalleerde toepassingen.|  
|**Implementaties van takenreeksen met toepassingen**|Geeft de takenreeksimplementaties weer die een opgegeven toepassing installeren.|  


## <a name="software-distribution---collections"></a>Software distributie-verzamelingen  

De volgende drie rapporten worden vermeld in de categorie **software distributie-verzamelingen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle verzamelingen**|Geeft alle verzamelingen in de hiërarchie weer.|  
|**Alle resources in een specifieke verzameling**|Geeft resources weer in een opgegeven verzameling.|  
|**Onderhoudsvensters die beschikbaar zijn voor een opgegeven client**|Geeft alle onderhoudsvensters weer die van toepassing zijn voor een opgegeven client.|  



## <a name="software-distribution---content"></a>Software distributie-inhoud  

De volgende 16 rapporten worden vermeld in de categorie **software distributie-inhoud** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle actieve inhoudsdistributies**|Geeft alle distributiepunten weer waarop op dit moment inhoud wordt geïnstalleerd of verwijderd.|  
|**Alle inhoud**|Geeft alle toepassingen en pakketten op een site weer.|  
|**Alle inhoud op een specifiek distributiepunt**|Geeft alle inhoud weer die momenteel is geïnstalleerd op een opgegeven distributiepunt.|  
|**Alle distributiepunten**|Geeft informatie weer over de distributiepunten voor elke site.|  
|**Alle statusberichten voor een specifiek pakket op een specifiek distributiepunt**|Geeft alle statusberichten weer voor een opgegeven pakket op een opgegeven distributiepunt.|  
|**Distributiestatus van toepassingsinhoud**|Geeft informatie weer over de distributiestatus voor de toepassingsinhoud.|  
|**Toepassingen die op een distributiepuntengroep zijn gericht**|Geeft informatie weer over de toepassingsinhoud die is geïmplementeerd naar een opgegeven distributiepuntengroep.|  
|**Toepassingen die niet zijn gesynchroniseerd op een opgegeven distributiepuntengroep**|Geeft de toepassingen weer waarvoor gekoppelde inhouds bestanden niet zijn bijgewerkt met de laatste versie op een opgegeven distributiepunten groep.|  
|**Distributiepuntengroep**|Geeft informatie weer over een opgegeven distributiepuntengroep.|  
|**Samenvatting van gebruik van distributiepunt**|Geeft een samenvatting weer van het distributiepuntgebruik per distributiepunt.|  
|**Distributiestatus van specifiek pakket**|Geeft de distributiestatus weer voor opgegeven pakketinhoud op elk distributiepunt.|  
|**Pakketten die op een distributiepuntengroep zijn gericht**|Geeft informatie weer over pakketten die zijn gericht op een opgegeven distributiepuntengroep.|  
|**Pakketten die niet zijn gesynchroniseerd op een opgegeven distributiepuntengroep**|Geeft pakketten weer waarvoor gekoppelde inhouds bestanden niet zijn bijgewerkt met de laatste versie op een opgegeven distributiepunten groep.|  
|**Afwijzing van bron inhoud van peer-cache**|Hiermee wordt het aantal geweigerde peer-cache-bron afwijzingen per grens groep weer gegeven.|
|**Afwijzing van bron inhoud peer-cache per voor waarde**|Hiermee worden de peer-cache bronnen weer gegeven die de inhoud van een voor waarde hebben afgewezen.|
|**Details afwijzing van bron inhoud peer-cache**|Hier wordt de naam weer gegeven van de inhoud die is geweigerd door een peer bron.|



## <a name="software-distribution---package-and-program-deployment"></a>Software distributie-implementatie van pakket en programma 

De volgende vijf rapporten worden vermeld in de categorie **software distributie-implementatie van pakket en programma** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle implementaties voor een specifiek pakket en programma**|Geeft informatie weer over alle implementaties van een opgegeven pakket en programma.|  
|**Alle pakket- en programma-implementaties**|Geeft alle pakket- en programma-implementaties op deze site weer.|  
|**Alle pakket- en programma-implementaties voor een opgegeven verzameling**|Geeft alle pakket- en programma-implementaties weer voor een opgeven verzameling.|  
|**Alle pakket- en programma-implementaties voor een opgegeven computer**|Geeft alle pakket- en programma-implementaties weer die van toepassing zijn op een opgegeven computer.|  
|**Alle pakket- en programma-implementaties voor een opgegeven gebruiker**|Geeft alle pakket- en programma-implementaties weer voor een opgegeven gebruiker.|  



## <a name="software-distribution---package-and-program-deployment-status"></a>Software distributie-status van pakket-en programma-implementatie  

De volgende vijf rapporten worden vermeld in de categorie **software distributie-status van pakket-en programma-implementatie** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle systeemresourcepakket- en programma-implementaties met status**|Geeft alle pakket- en programma-implementaties voor de site weer met een samenvattingsstatus van elke implementatie.|  
|**Alle systeemresources voor een specifieke pakket- en programma-implementatie in een opgegeven status**|Geeft een lijst weer van alle resources die een opgegeven status hebben voor een opgegeven pakket- en programma-implementatie.|  
|**Grafiek-voltooiings status van pakket-en programma-implementatie per uur**|Geeft het percentage computers weer waarop het pakket is geïnstalleerd. De lijst organiseert elke uur nadat een beheerder het pakket en de programma-implementatie heeft gemaakt. Dit kan worden gebruikt om de gemiddelde tijd bij te houden voor een implementatie van pakket en programma.|  
|**Status van pakket- en programma-implementatie voor een opgegeven client en implementatie**|Geeft de statusberichten weer die zijn gerapporteerd voor een opgegeven computer en pakket- en programma-implementatie.|  
|**Status van een opgegeven pakket- en programma-implementatie**|Geeft een samenvatting weer voor een opgegeven pakket- en programma-implementatie.|  



## <a name="software-metering"></a>Softwarelicentiecontrole  

De volgende 13 rapporten worden vermeld in de categorie **Software meter** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle software-licentiecontroleregels die worden toegepast op deze site**|Geeft een lijst weer met alle regels voor softwarelicentiecontrole op de site.|  
|**Computers waarop een programma met gecontroleerde licentie is geïnstalleerd, maar die het programma sinds een opgegeven datum niet hebben uitgevoerd**|Geeft alle computers weer met de opgegeven toepassing met data limiet, maar de gebruiker heeft het programma niet uitgevoerd sinds de opgegeven datum.|  
|**Computers waarop een specifiek programma met gecontroleerde licenties is uitgevoerd**|Geeft een lijst weer van computers waarop programma’s zijn uitgevoerd die overeenkomen met de opgegeven softwaremeterregel binnen de opgegeven maand en het opgegeven jaar.|  
|**Gelijktijdig gebruik voor alle programma's met gecontroleerde licentie**|Geeft het maximum aantal gebruikers weer die elk programma met gecontroleerde licenties tegelijkertijd hebben uitgevoerd tijdens de opgegeven maand en het opgegeven jaar.|  
|**Trendgrafiek van gelijktijdig gebruik van een specifiek programma met gecontroleerde licenties**|Geeft het maximum aantal gebruikers weer die het opgegeven programma met gecontroleerde licenties tegelijkertijd hebben uitgevoerd gedurende elke maand van het afgelopen jaar.|  
|**Installatiebasis voor alle programma's met gecontroleerde licentie**|Geeft het aantal computers weer waarop programma's met gecontroleerde licenties zijn geïnstalleerd, zoals gerapporteerd door de software-inventarisatie. Dit rapport vereist dat de computer software-inventaris verzamelt.|  
|**Voortgang van samenvatting softwarelicentiecontrole**|Geeft de tijd weer waarop de recentst samengevatte licentiecontrolegegevens zijn verwerkt op de siteserver. De software licentie controle rapporten geven alleen meet gegevens weer die zijn verwerkt vóór deze datums.|  
|**Samenvatting van gebruik op tijdstip voor een specifiek programma met gecontroleerde licentie**|Geeft het gemiddelde gebruik van een bepaald programma weer in de afgelopen negentig dagen, opgedeeld per uur en dag.|  
|**Totaal gebruik voor alle programma's met gecontroleerde licentie**|Geeft het aantal gebruikers weer die Program ma's hebben uitgevoerd binnen de opgegeven maand en het jaar en die overeenkomen met elke software meter regel. Deze regels zijn voor lokaal geïnstalleerde software of het gebruik van Terminal Services.|  
|**Totaal gebruik voor alle programma's met gecontroleerde licenties op Windows Terminal Servers**|Geeft het aantal gebruikers weer die programma's hebben uitgevoerd die overeenkomen met elke softwarelicentiecontroleregel met behulp van Terminal Services binnen de opgegeven maand en het opgegeven jaar.|  
|**Trendgrafiek van het totale gebruik voor een specifiek programma met gecontroleerde licenties**|Geeft het aantal gebruikers weer die gedurende de afgelopen jaar Program ma's hebben uitgevoerd en die overeenkomen met de opgegeven software meter regel. Deze regels zijn voor lokaal geïnstalleerde software of het gebruik van Terminal Services.|  
|**Trendgrafiek van het totale gebruik voor een specifiek programma met gecontroleerde licenties op Windows Terminal-servers**|Geeft het aantal gebruikers weer die gedurende de afgelopen jaar Program ma's hebben uitgevoerd en die overeenkomen met de opgegeven software meter regel. Deze regels zijn van het gebruik van Terminal Services.|  
|**Gebruikers die een specifiek programma met gecontroleerde licenties hebben uitgevoerd**|Geeft een lijst weer van gebruikers die Program ma's hebben uitgevoerd binnen de opgegeven maand en het jaar en die overeenkomen met de opgegeven software meter regel.|  



## <a name="software-updates---a-compliance"></a>Software-updates-A compatibiliteit  

De volgende acht rapporten worden vermeld in de categorie **software-updates-een naleving** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Compatibiliteit 1 - Algemene compatibiliteit**|Geeft de algemene compatibiliteitsgegevens weer voor een software-updategroep.|  
|**Compatibiliteit 2 - Specifieke software-update**|Geeft de compatibiliteitsgegevens weer voor een opgegeven software-update.|  
|**Compatibiliteit 3 - Updategroep (per update)**|Geeft de compatibiliteitsgegevens weer voor software-updates die zijn gedefinieerd in een software-updategroep.|  
|**Compatibiliteit 4 - Updates per leverancier maand jaar**|Geeft de compatibiliteitsgegevens weer voor software-updates die gedurende een specifieke maand en een specifiek jaar zijn uitgegeven door een leverancier.|  
|**Compatibiliteit 5 - Specifieke computer**|Dit rapport retourneert de compatibiliteitgegevens van een software-update voor een opgegeven computer. Als u de hoeveelheid geretourneerde informatie wilt beperken, kunt u de leverancier en software-updateclassificatie opgeven.|  
|**Compatibiliteit 6 - Specifieke software-updatestatussen (secundair)**|Geeft de telling en het percentage computers weer in elke compatibiliteitsstatus voor de opgegeven software-update.|  
|**Compatibiliteit 7 - Computers in een specifieke compatibiliteitsstatus voor een updategroep (secundair)**|Geeft alle computers weer in een verzameling die een opgegeven algemene compatibiliteitsstatus hebben ten opzichte van een software-updategroep.|  
|**Compatibiliteit 8 - Computers in een specifieke compatibiliteitstatus voor een update (secundair)**|Geeft alle computers weer in een verzameling die een opgegeven compatibiliteitsstatus hebben voor een software-update.|  
|**Naleving 9: algehele status en naleving**|Geeft de algemene status-en compatibiliteits gegevens weer voor een software-update groep. (vanaf versie 1806)| 


## <a name="software-updates---b-deployment-management"></a>Software-updates-B implementatie beheer  

De volgende acht rapporten worden vermeld in de categorie **software-updates-B implementatie beheer** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Beheer 1 - Implementaties van een updategroep**|Geeft alle implementaties weer die alle software-updates bevatten die zijn gedefinieerd in een opgegeven software-update groep.|  
|**Beheer 2 - Updates vereist maar niet geïmplementeerd**|Geeft alle leverancierspecifieke software-updates weer die clients detecteren als vereist, maar een beheerder heeft niet geïmplementeerd voor een opgegeven verzameling.|  
|**Beheer 3 - Updates in een implementatie**|Geeft de software-updates weer die zijn opgenomen in een opgegeven implementatie.|  
|**Beheer 4 - Implementaties die zijn gericht op een verzameling**|Geeft alle software-update-implementaties weer die zijn gericht op een opgegeven verzameling.|  
|**Beheer 5 - Implementaties die zijn gericht op een computer**|Geeft alle software-update-implementaties weer die zijn geïmplementeerd op een opgegeven computer.|  
|**Beheer 6 - Implementaties die een specifieke update bevatten**|Geeft alle implementaties weer die een opgegeven software-update en de gekoppelde doel verzameling voor de implementatie bevatten.|  
|**Beheer 7 - Updates in een implementatie waarbij inhoud ontbreekt**|Geeft de software-updates in een opgegeven implementatie weer waarvoor niet alle gekoppelde inhoud is opgehaald. Deze status voor komt dat clients de update installeren, waardoor de implementatie geen naleving van 100% kan bereiken.|  
|**Beheer 8 - Computers waarbij inhoud ontbreekt (secundair)**|Geeft alle computers weer waarvoor de opgegeven software-update is vereist, maar de gekoppelde inhoud is nog niet gedistribueerd naar een distributie punt.|  



## <a name="software-updates---c-deployment-states"></a>Software-updates-C implementatie statussen  

De volgende zes rapporten worden vermeld in de categorie **software-updates-C implementatie status** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Statussen 1 - Afdwingingsstatussen voor een implementatie**|Geeft de afdwingingsstatussen weer voor een opgegeven software-update-implementatie, die normaal gesproken de tweede fase vormt in een implementatie-evaluatie.|  
|**Statussen 2 - Evaluatiestatussen voor een implementatie**|Geeft de evaluatiestatus weer voor een opgegeven software-update-implementatie, die normaal gesproken de eerste fase vormt in een implementatie-evaluatie.|  
|**Statussen 3 - Statussen voor een implementatie en computer**|Geeft de statussen weer voor alle software-updates in de opgegeven implementatie voor een opgegeven computer.|  
|**Statussen 4 - Computers in een specifieke status voor een implementatie (secundair)**|Geeft alle computers weer in een opgegeven status voor een software-update-implementatie.|  
|**Statussen 5 - Statussen voor een update in een implementatie (secundair)**|Geeft een samenvatting weer van statussen voor een opgegeven software-update waarop een opgegeven implementatie is gericht.|  
|**Statussen 6 - Computers in een specifieke afdwingingsstatus voor een update (secundair)**|Geeft alle computers weer in een opgegeven afdwingingsstatus voor een opgegeven software-update.|  



## <a name="software-updates---d-scan"></a>Software-updates-D controleren  

De volgende vier rapporten worden vermeld in de categorie **software-updates-D scannen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Controle 1 - Laatste controlestatussen op verzameling**|Geef een verzameling op om het aantal computers in elke compatibiliteits controle status weer te geven. De clients retour neren de status tijdens de laatste compatibiliteits controle.|  
|**Controle 2 - Laatste controlestatussen op site**|Geef een site op om het aantal computers in elke compatibiliteits controle status weer te geven. De clients retour neren de status tijdens de laatste compatibiliteits controle.|  
|**Controle 3 - Clients van een verzameling die een specifieke status rapporteren (secundair)**|Geeft alle computers weer voor een opgegeven verzameling en een opgegeven compatibiliteitscontrolestatus hebben geretourneerd tijdens de laatste compatibiliteitscontrole.|  
|**Controle 4 - Clients van een site die een specifieke status rapporteert (secundair)**|Geef een site op om alle computers met een opgegeven compatibiliteits controle status weer te geven. De clients retour neren de status tijdens de laatste compatibiliteits controle.|  



## <a name="software-updates---e-troubleshooting"></a>Software-updates-E problemen oplossen  

De volgende vier rapporten worden vermeld in de categorie **software-updates-E probleem oplossing** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Problemen oplossen 1-controle fouten**|Geeft controlefouten op de site en een telling van de computers waarbij elke fout optreedt weer.|  
|**Problemen oplossen 2-implementatie fouten**|Geeft de implementatiefouten op de site en een telling van de computers waarbij elke fout optreedt weer.|  
|**Problemen oplossen 3-computers waarbij een specifieke controle fout optreedt (secundair)**|Geeft een lijst weer van de computers die niet konden worden gescand vanwege een opgegeven fout.|  
|**Problemen oplossen 4 - Computers waarbij een specifieke implementatiefout optreedt (secundair)**|Geeft een lijst weer van de computers waarop de implementatie van een update mislukt vanwege een opgegeven fout.|  



## <a name="state-migration"></a>Status migratie  

De volgende drie rapporten worden vermeld in de categorie **status migratie** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Statusmigratie-informatie voor een specifieke broncomputer**|Geeft de statusmigratie-informatie weer voor een opgegeven broncomputer.|  
|**Statusmigratie-informatie voor een specifiek statusmigratiepunt**|Geeft de statusmigratie-informatie weer voor een opgegeven migratiepunt.|  
|**Statusmigratiepunten voor een specifieke site**|Geeft de statusmigratiepunten weer voor een opgegeven site.|  



## <a name="status-messages"></a>Statusberichten  

De volgende 12 rapporten worden vermeld in de categorie **status berichten** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle berichten voor een specifieke bericht-id**|Geeft een lijst weer van statusberichten met een opgegeven bericht-id|  
|**Clients die de afgelopen 12 uur fouten hebben gerapporteerd voor een specifieke site**|Geeft een lijst weer van computers aan onderdelen die de afgelopen 12 uur fouten hebben gerapporteerd, en het aantal gerapporteerde fouten.|  
|**Onderdeelberichten voor de afgelopen 12 uur**|Geeft een lijst weer van onderdelenberichten voor de afgelopen 12 uur voor een opgegeven sitecode, computer en onderdeel.|  
|**Onderdeelberichten voor het afgelopen uur**|Geeft een lijst weer van de status berichten die het afgelopen uur zijn gemaakt door een opgegeven onderdeel op een opgegeven computer op een opgegeven site.|  
|**Onderdeelberichten voor het afgelopen uur voor een specifieke site**|Geeft het aantal en de ernst weer van statusberichten die zijn gerapporteerd in het afgelopen uur op een opgegeven site, per onderdeel.|  
|**Fouten in de afgelopen 12 uur tellen**|Geeft het aantal serveronderdeelberichten in de afgelopen 12 uur weer.|  
|**Fatale fouten (per onderdeel)**|Geeft een lijst weer met computers die fatale fouten rapporteren, per onderdeel.|  
|**Fatale fouten (op computernaam)**|Geeft een lijst weer met computers die fatale fouten rapporteren, per computernaam.|  
|**Laatste 1000 berichten voor een specifieke computer (fouten en waarschuwingen)**|Geeft een samenvatting weer van de laatste 1000 fout- en waarschuwingsberichten voor onderdeelstatus voor een opgegeven computer.|  
|**Laatste 1000 berichten voor een specifieke computer (fouten waarschuwingen en informatie)**|Geeft een samenvatting weer van de laatste 1000 fout-, waarschuwings- en informatieberichten voor onderdeelstatus voor een opgegeven computer.|  
|**Laatste 1000 berichten voor een specifieke computer (fouten)**|Geeft een samenvatting weer van de laatste 1000 foutstatusberichten voor serveronderdeel voor een opgegeven computer.|  
|**Laatste 1000 berichten voor een specifiek serveronderdeel**|Geeft een samenvatting weer van de recentste 1000 statusberichten voor een opgegeven serveronderdeel.|  



## <a name="status-messages---audit"></a>Status berichten-audit  

De volgende drie rapporten worden vermeld in de categorie **status berichten-audit** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle controleberichten voor een specifieke gebruiker**|Geeft een samenvatting weer van alle controlestatusberichten voor een opgegeven gebruiker. Controle berichten beschrijven acties die zijn uitgevoerd in de Configuration Manager-console waarmee objecten in Configuration Manager worden toegevoegd, gewijzigd of verwijderd.|  
|**Extern beheer-alle computers die extern worden beheerd door een specifieke gebruiker**|Geeft een samenvatting weer van statusberichten die extern beheer van clientcomputers door een opgegeven gebruiker aangeven.|  
|**Extern beheer-alle informatie over extern beheer**|Geeft een samenvatting weer van statusberichten die zijn gerelateerd aan het beheer op afstand van clientcomputers.|  



## <a name="task-sequence---deployment-status"></a>Taken reeks-implementatie status  

De volgende elf rapporten worden vermeld onder de categorie **taken reeks-implementatie status** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle systeemresources voor een takenreeksimplementatie in een bepaalde status**|Geeft een lijst weer van de doelcomputers voor de opgegeven takenreeksimplementatie in de opgegeven implementatiestatus.|  
|**Alle systeemresources voor een takenreeksimplementatie in een specifieke status en die beschikbaar is voor onbekende computers**|Geeft een lijst weer van de doelcomputers voor de opgegeven takenreeksimplementatie in de opgegeven implementatiestatus.|  
|**Telling van systeemresources waaraan takenreeksimplementaties zijn toegewezen maar die deze nog niet heeft uitgevoerd**|Geeft het aantal computers weer dat taken reeksen heeft geaccepteerd, maar de taken reeks nog niet heeft uitgevoerd.|  
|**Geschiedenis van een takenreeksimplementatie op een computer**|Geeft de status weer van elke stap van de opgegeven takenreeksimplementatie op de opgegeven doelcomputer. Als er geen record wordt geretourneerd, is de taken reeks niet gestart op de computer.|  
|**Lijst van computers die een specifieke tijdsduur hebben overschreden voor het uitvoeren van een takenreeksimplementatie**|Geeft de lijst weer van doelcomputers die de opgegeven tijdsduur hebben overschreden voor het uitvoeren van een takenreeks.|  
|**Uitvoeringstijd voor een specifieke takenreeksimplementatie op een specifieke doelcomputer**|Geeft de totale tijdsduur weer die nodig was voor het voltooien van een opgegeven takenreeks op een opgegeven computer.|  
|**Uitvoeringstijd voor elke stap van een takenreeksimplementatie op een specifieke doelcomputer**|Geeft de tijdsduur weer die nodig was voor het voltooien van elke stap van de opgegeven takenreeksimplementatie op een opgegeven doelcomputer.|  
|**Status van een specifieke takenreeksimplementatie voor een specifieke computer**|Geeft de statussamenvatting weer voor een opgegeven takenreeksimplementatie op een opgegeven computer.|  
|**Status van een takenreeksimplementatie op een onbekende doelcomputer**|Geeft de status weer van de opgegeven takenreeksimplementatie op de opgegeven onbekende doelcomputer.|  
|**Statussamenvatting van een specifieke takenreeksimplementatie**|Geeft een statussamenvatting weer van alle resources waarop een implementatie is gericht.|  
|**Statussamenvatting van een specifieke takenreeksimplementatie op onbekende computers**|Geeft de status samenvatting weer van alle resources die zijn gericht op de opgegeven implementatie en die beschikbaar is voor een verzameling die onbekende computers bevat.|  



## <a name="task-sequence---deployments"></a>Taken reeks-implementaties  

De volgende elf rapporten worden vermeld in de categorie **taken reeks-implementaties** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle systeemresources die zich op dit moment in een specifieke groep of fase van een specifieke takenreeksimplementatie bevinden**|Geeft een lijst weer van computers die zich momenteel in een opgegeven groep of fase van een opgegeven takenreeksimplementatie bevinden.|  
|**Alle systeemresources waarbij een takenreeksimplementatie is mislukt binnen een specifieke groep of fase**|Geeft een lijst weer van computers waarbij een fout is opgetreden binnen een opgegeven groep of fase van de opgegeven takenreeksimplementatie.|  
|**Alle takenreeksimplementaties**|Geeft details weer van alle takenreeksimplementaties die vanaf deze site zijn gestart.|  
|**Alle takenreeksimplementaties die beschikbaar zijn voor onbekende computers**|Geeft details weer van alle taken reeks implementaties die vanaf de site zijn gestart en die zijn geïmplementeerd op verzamelingen die onbekende computers bevatten.|  
|**Telling van fouten in elke fase of groep van een specifieke takenreeks**|Geeft het aantal fouten weer in elke fase of groep van een opgegeven takenreeks.|  
|**Telling van fouten in elke fase of groep van een specifieke takenreeksimplementatie**|Geeft het aantal fouten weer in elke fase of groep van een opgegeven takenreeksimplementatie.|  
|**Implementatiestatus van alle takenreeksimplementaties**|Geeft de algemene voortgang weer van alle takenreeksimplementaties.|  
|**Voortgang van een actieve takenreeks**|Geeft de voortgang weer van de opgegeven takenreeks.|  
|**Voortgang van een actieve takenreeksimplementatie**|Geeft de samenvattingsinformatie weer voor de opgegeven takenreeksimplementatie.|  
|**Voortgang van alle implementaties voor een specifieke takenreeks**|Geeft de voortgang weer van alle implementaties voor de opgegeven takenreeks.|  
|**Samenvattingsrapport voor een opgegeven takenreeksimplementatie**|Geeft de samenvattingsinformatie weer voor de opgegeven takenreeksimplementatie.|  



## <a name="task-sequence---progress"></a>Taken reeks-voortgang  

De volgende vijf rapporten worden vermeld in de categorie **taken reeks voortgang** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Grafiek-wekelijkse voortgang van een taken reeks**|Geeft de wekelijkse voortgang weer van een takenreeks vanaf de datum van implementatie.|  
|**Voortgang van een takenreeks**|Geeft de voortgang weer van de opgegeven takenreeks.|  
|**Voortgang van alle takenreeksen**|Geeft een samenvatting weer van de voortgang van alle takenreeksen.|  
|**Voortgang van takenreeksen voor de implementatie van besturingssystemen**|Geeft de voortgang weer van alle takenreeksen die besturingssystemen implementeren.|  
|**Status van alle onbekende computers**|Geeft een lijst weer van computers die onbekend waren op het moment dat ze een taken reeks implementatie hebben uitgevoerd en of ze nu bekende computers zijn.|  



## <a name="task-sequences---references"></a>Taken reeksen-verwijzingen  

Het volgende rapport wordt vermeld onder de categorie **taken reeksen-verwijzingen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Inhoud waarnaar wordt verwezen door een specifieke taakreeks**|Geeft inhoud weer waarnaar wordt verwezen door een opgegeven takenreeks.|  



<!--
## Upgrade Assessment  
The following 11 reports are listed under the **Upgrade Assessment** category.

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## <a name="user---device-affinity"></a>Gebruiker-affiniteit met apparaat  

De volgende twee rapporten worden vermeld in de categorie **gebruiker-apparaat-affiniteit** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Affiniteitskoppelingen per verzameling van gebruikersapparaat in afwachting**|Geeft alle in behandeling zijnde gebruikersapparaat-affiniteit-toewijzingen op basis van gebruiksgegevens weer voor leden van een verzameling.|  
|**Affiniteitskoppelingen van gebruikersapparaat per verzameling**|Geeft alle koppelingen van gebruikers apparaten weer voor de opgegeven verzameling en groepeert de resultaten per type verzameling (bijvoorbeeld gebruiker of apparaat).|  



## <a name="user-data-and-profiles-health"></a>Status van gebruikers gegevens en-profielen  

De volgende vier rapporten worden vermeld in de categorie **status van gebruikers gegevens en-profielen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Statusrapport mapomleiding - details**|Hiermee worden de status Details van Mapomleiding voor elk van de omgeleide mappen voor een bepaalde gebruiker weer gegeven.|  
|**Statusrapport van gebruikersprofielen voor roaming - details**|Geeft de details weer van de status van het zwervende gebruikers profiel voor een opgegeven gebruiker.|  
|**Statusrapport van gebruikersgegevens en -profielen - details**|Geeft de fout-of waarschuwings details weer van Mapomleiding of zwervende gebruikers profielen. Dit rapport is het doel van de details van het samenvattings rapport.|  
|**Statusrapport van gebruikersgegevens en -profielen - samenvatting**|Geeft de samenvatting weer van de status van mapomleiding en gebruikersprofielen voor roaming.|  



## <a name="users"></a>Gebruikers  

De volgende drie rapporten worden vermeld in de categorie **gebruikers** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Computers voor een specifieke gebruikersnaam**|Geeft een lijst weer van de computers die zijn gebruikt door een opgegeven gebruiker.|  
|**Gebruikers per domein tellen**|Geeft het aantal gebruikers weer in elk domein.|  
|**Gebruikers in een specifiek domein**|Geeft een overzicht van gebruikers en hun computers in een opgegeven domein.|  



## <a name="virtual-applications"></a>Virtuele toepassingen  

De volgende zeven rapporten worden vermeld in de categorie **virtuele toepassingen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Resultaten virtuele omgeving App-V**|Geeft informatie weer over een opgegeven virtuele omgeving met een opgegeven status voor een opgegeven verzameling.|  
|**Resultaten virtuele omgeving App-V voor activa**|Geeft informatie weer over een opgegeven virtuele omgeving voor een opgegeven Asset. Het bevat ook een implementatie type voor de opgegeven virtuele omgeving.|  
|**Status virtuele omgeving App-V**|Geeft compatibiliteitsinformatie weer voor een opgegeven virtuele omgeving voor een opgegeven verzameling.|  
|**Computers met een specifieke virtuele toepassing**|Geeft een samenvatting weer van computers die de opgegeven App-V-toepassingssnelkoppeling hebben zoals gemaakt met behulp van de Application Virtualization Management Sequencer.|  
|**Computers met een specifiek virtuele-toepassingspakket**|Geeft een samen vatting weer van computers die het opgegeven app-V-toepassings pakket hebben.|  
|**Alle virtuele toepassingspakketten tellen**|Geef een telling weer van aantal gedetecteerde App-V-toepassingspakketten.|  
|**Telling van alle exemplaren van virtuele toepassingen**|Geef een telling weer van gedetecteerde App-V-toepassingen.|  



## <a name="vulnerability-assessment"></a>Evaluatie van beveiligingsproblemen

De volgende rapporten worden vermeld in de categorie met de **evaluatie van beveiligings problemen** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Algemeen rapport evaluatie van beveiligings problemen**|Identificeert beveiligings-, beheer-en nalevings problemen voor een specifieke computer|  



## <a name="wake-on-lan"></a>Wake on LAN  

De volgende zeven rapporten worden vermeld in de categorie **Wake on LAN** .

|Rapportnaam|Beschrijving|  
|-----------------|-----------------|  
|**Alle computers waarop Wake On LAN-activiteit is gericht**|Geef het type implementatie op om een lijst weer te geven met computers waarop Wake on LAN-activiteit is gericht.|  
|**Alle objecten in afwachting van ontwaakactiviteit**|Geeft objecten weer die zijn ingepland voor ontwaken.|  
|**Alle sites in de hiërarchie die beschikbaar zijn voor Wake On LAN**|Geeft een lijst met alle sites in de hiërarchie weer die beschikbaar zijn voor Wake On LAN.|  
|**Fouten die zijn ontvangen tijdens het verzenden van ontwaakpakketten voor een opgegeven periode**|Geeft de fouten weer die zijn ontvangen tijdens het verzenden van ontwaakpakketten naar computers voor een opgegeven periode|  
|**Geschiedenis van Wake On LAN-activiteit**|Geeft een geschiedenis weer van de ontwaakactiviteit sinds een bepaalde periode.|  
|**Details van implementatiestatus van Wake-up proxy**|Geeft informatie weer over de implementatiestatus van Wake-up proxy voor elk apparaat in een opgegeven verzameling.|  
|**Samenvatting van implementatiestatus van Wake-up proxy**|Geeft een samenvatting weer van de implementatiestatus van Wake-up proxy voor een opgegeven verzameling.|  
