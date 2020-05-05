---
title: Client Spy
titleSuffix: Configuration Manager
description: Gebruik client Spy voor het oplossen van problemen met software distributie, inventarisatie en software licentie controle op Configuration Manager-clients.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723430"
---
# <a name="client-spy"></a>Client Spy

*Van toepassing op: Configuration Manager (huidige vertakking)*

Client Spy is een van de [Configuration Manager-hulpprogram ma's](tools.md). Het is een hulp programma voor het oplossen van problemen met software distributie, inventarisatie en software licentie controle op Configuration Manager-clients. 

De meeste informatie die door het hulp programma wordt opgehaald, is van toepassing op software-implementaties:
- Alle huidige software-implementaties 
- Geschiedenis van software distributie
- De configuratie van de client cache
- Items in cache
- Vereiste implementaties in behandeling
- Beschik bare implementaties  

Ook worden de volgende inventaris gegevens weer gegeven
- De laatste datum van de inventarisatie cyclus
- De laatste rapport datum
- Primaire en secundaire versies van software-inventaris
- Bestands verzameling
- Hardware-inventaris
- IDMIF-verzameling
- Detectie gegevens records (Ddr's) 

De software meter regels worden ook weer gegeven. 

> [!Note]   
> Om de prestaties te verbeteren, verzamelt het hulp programma alleen informatie voor elk tabblad wanneer u het selecteert. Op dezelfde manier kunt u, wanneer u op **vernieuwen**klikt, alleen de informatie vernieuwen voor het tabblad dat momenteel wordt weer gegeven.



## <a name="usage"></a>Gebruik


### <a name="tools-menu"></a>Menu Extra

De volgende acties zijn beschikbaar in het menu **extra** :  

#### <a name="connect"></a>Verbinding maken
Gegevens ophalen van een andere computer.  

- Het hulp programma geeft standaard informatie weer van de huidige computer. 

- Verbinding maken met behulp van de naam van de externe computer, de gebruikers naam en het wacht woord voor het account. Het hulp programma maakt verbinding met de IPC $-share op de externe computer. De verbinding wordt verwijderd als het hulp programma wordt afgesloten of als u verbinding maakt met een andere computer.  

- Er is een account vereist met voldoende referenties om de informatie op te halen.  

- Als u geen gebruikers naam en wacht woord opgeeft, gebruikt client Spy de beveiligings context van de gebruiker die momenteel is aangemeld om de verbinding tot stand te brengen.  

- Wanneer u verbinding maakt met een externe computer, worden alle tabbladen die worden weer gegeven informatie van de externe computer weer gegeven.

#### <a name="software-distribution"></a>Softwaredistributie
Hiermee worden de tabbladen voor [software distributie](#software-distribution) weer gegeven en de andere tabbladen verborgen. Standaard geeft client Spy de tabbladen software distributie.

#### <a name="inventory"></a>Inventaris
Hiermee wordt het tabblad inventarisatie weer gegeven en de andere tabbladen verborgen.

#### <a name="software-metering"></a>Softwaremeter
Hiermee wordt het tabblad software licentie controle weer gegeven en worden de andere tabbladen verborgen.

#### <a name="save-current-tab-to-file"></a>Huidig tabblad Opslaan in bestand
Hiermee slaat u de gegevens op het momenteel weer gegeven tabblad op in een tekst bestand dat u opgeeft. 

#### <a name="save-all-tabs-to-file"></a>Alle tabbladen opslaan in bestand
Hiermee slaat u de informatie op alle tabs op in een tekst bestand dat u opgeeft. Er worden alleen gegevens opgeslagen die uw account kan zien.



## <a name="software-distribution-tab"></a>Tabblad software distributie

Configureer instellingen op de volgende vier tabbladen:
- [Aanvragen voor het uitvoeren van software distributie](#bkmk_exec-requests)
- [Geschiedenis van software distributie](#bkmk_history)
- [Informatie over software distributie cache](#bkmk_cache-info)
- [Uitvoeringen van software distributie in behandeling](#bkmk_pending-exec)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a>Aanvragen voor het uitvoeren van software distributie

Op dit tabblad worden alle bestaande implementaties weer gegeven, met inbegrip van apparaat-en gebruikers gerichte implementaties.

Elk structuur item in het tabblad uitvoerings aanvragen voor software distributie bevat de volgende vier kenmerken:
- Aankondigings-ID. Deze waarde kan leeg zijn, als dit een beschik bare implementatie is. 
- Pakket-id 
- Programmanaam 
- Gebruiker. Dit kan de beoogde gebruikers-SID zijn of de SID van de gebruiker die de aanvraag heeft gestart. Als beide systeem aanvragen zijn, is de weer gegeven gebruiker systeem. 

Voor elk verzoek om te worden uitgevoerd, wordt ook de volgende informatie in een boom structuur weer gegeven:
- Programmanaam 
- Pakket-id 
- Pakketnaam 
- Aanmaak tijd van aanvraag 
- Status 
- Uitvoerings status, als de status wordt uitgevoerd 
- Uitvoerings context (gebruiker of beheerder) 
- Geschiedenis status (geslaagd, mislukt of NotRun) 
- LastRunTime (nooit: als het programma nog niet eerder is uitgevoerd) 
- RetryCount, als de status WaitingRetry is 
- ContentAccess (aantal pogingen, als de status WaitingRetry is) 
- FailureCode, als de status WaitingRetry is 
- FailureReason, als de status WaitingRetry is 

Als de aanvraag inhoud vereist, is de status WaitingContent. Op het tabblad informatie over software distributie cache worden de Details voor deze download aanvraag weer gegeven.

Als de aanvraag voor het uitvoeren van een download aanvraag is, wordt ook het aantal gedownloade bytes weer gegeven.

> [!Note]   
> Er worden verschillende pictogrammen gebruikt voor verschillende statussen van een uitvoerings aanvraag.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a>Geschiedenis van software distributie

Dit tabblad bevat informatie over alle eerder uitgevoerde Program ma's. Deze informatie wordt opgeslagen in het REGI ster.

De belangrijkste vertakkingen van deze boom structuur zijn de verschillende gebruikers geschiedenis, waaronder System. Er wordt een substructuur weer gegeven met de lijst met pakketten waaruit Program ma's voor elke gebruiker zijn uitgevoerd. 

De pakket-ID en pakket naam voor elke pakket substructuur bevat een lijst met Program ma's die zijn uitgevoerd. Hier worden de volgende kenmerken voor elk weer gegeven: 
- Programma naam
- Uitvoerings status
- Laatste uitvoerings tijd
- Fout code
- Reden van fout  

De fout code en fout reden zijn leeg wanneer een programma is uitgevoerd.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a>Informatie over software distributie cache

#### <a name="cache-config"></a>Cache configuratie
Bevat informatie over de Configuration Manager-client cache. Deze informatie omvat de cache locatie, de cache grootte en of deze momenteel in gebruik is. 

#### <a name="cached-items"></a>Items in cache
Bevat een substructuur van alle items die momenteel in de cache zijn opgeslagen. Elk structuur item bevat de volgende informatie over elk item: 
- De locatie (map) van het item in de cache
- Huidige status
- Pakket-id
- Naam van het pakket
- Versie van het pakket
- Pakket grootte
- Huidig aantal verwijzingen
- Tijd van recentste Referentie (UTC)  

#### <a name="downloading-items"></a>Items downloaden
Dit zijn de items die op dit moment door de client worden gedownload. Elk daarvan bevat dezelfde informatie die wordt weer gegeven door de items in de cache en het aantal kilo bytes dat is gedownload. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a>Uitvoeringen van software distributie in behandeling

Dit tabblad bevat informatie over eerdere en toekomstige vereiste implementaties en een lijst met beschik bare implementaties.

Elke vertakking is voor elk gebruikers account met implementaties die beschikbaar zijn, met inbegrip van systeem.

Voor elke gebruiker bevat een substructuur de volgende drie items:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Verplichte advertenties met toekomstige uitvoeringen
Dit zijn verplichte advertisements die nog steeds Program ma's moeten blijven uitvoeren. Dit kunnen terugkerende, eenmalige of meerdere plannings advertenties zijn. Elk geeft de aankondigings-ID, de volgende uitvoerings tijd en het schema weer waarop de advertentie wordt uitgevoerd. 

#### <a name="optional-advertisements"></a>Optionele advertenties
Geeft een lijst weer van alle gepubliceerde advertenties. Er worden ook details weer gegeven, zoals advertentie-ID, programma naam en pakket naam voor elke. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Eerdere verplichte advertenties zonder toekomstige geplande uitvoeringen
Dit is een lijst met advertisements die zich op de client bevinden en waarop geen toekomstige Program ma's zijn gepland om te worden uitgevoerd. De aankondigings-ID, pakket naam en programma naam worden weer gegeven. Een substructuur item wordt weer gegeven voor eventuele advertisements die optioneel zijn.

> [!Note]  
> Pakket naam gegevens zijn alleen beschikbaar voor pakketten waaraan een aangekondigd beleid is gekoppeld op de computer die wordt weer gegeven. Aan pakketten waaraan geen beleid meer is gekoppeld, wordt het bericht ' pakket naam niet meer beschikbaar ' weer gegeven.  



## <a name="inventory-tab"></a>Tabblad voor Raad

Er is slechts één tabblad met inventaris informatie. De hoofd structuur bevat de volgende vijf items:  

- **Software-inventaris**: bevat de datum waarop de laatste cyclus is gestart, de datum van het laatste rapport en de secundaire en primaire versie van het laatste rapport.  

- **Bestands verzameling**: bevat de datum waarop de laatste cyclus is gestart, de datum van het laatste rapport en de secundaire en primaire versie van het laatste rapport.  

- **Hardware-inventarisatie**: bevat de datum waarop de laatste cyclus is gestart, de datum van het laatste rapport en de secundaire en primaire versie van het laatste rapport.  

- **IDMIF-verzameling**: bevat de datum waarop de laatste cyclus is gestart, de datum van het laatste rapport en de secundaire en primaire versie van het laatste rapport.  

- **DDR**: bevat de datum waarop de laatste cyclus is gestart, de datum van het laatste rapport en de secundaire en primaire versie van het laatste rapport. De DDR-informatie wordt ook weer gegeven in een substructuur.



## <a name="software-metering-tab"></a>Het tabblad software meter

Op dit tabblad wordt informatie weer gegeven als een substructuur en alle software meter regels bevat. Elke regel als een knoop punt wordt weer gegeven, die wordt aangeduid met de bestands naam en regel-ID. Vouw elk knoop punt in de structuur uit en Bekijk de volgende informatie:
- Verkenner-bestands naam 
- Oorspronkelijke bestands naam
- Regel-id
- Bestandsversie
- Taal


