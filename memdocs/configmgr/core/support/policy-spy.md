---
title: Policy Spy
titleSuffix: Configuration Manager
description: Gebruik Policy Spy om het beleids systeem op Configuration Manager-clients weer te geven en problemen op te lossen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6038a3332c63a58d1f3c423491b1aa17aa28b080
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723178"
---
# <a name="policy-spy"></a>Policy Spy

*Van toepassing op: Configuration Manager (huidige vertakking)*

Policy Spy is een van de [Configuration Manager-hulpprogram ma's](tools.md). Het is een hulp programma voor het weer geven en oplossen van problemen met het beleids systeem op Configuration Manager-clients. Voer **PolicySpy. exe** uit om de gebruikers interface te openen. Zie [opdracht regel syntaxis](#bkmk_policyspy-syntax)voor meer informatie over het gebruik van de opdracht regel.

> [!Important]  
> Voer beleid Spy uit als beheerder. Als u niet **als Administrator uitvoert**, ziet u de volgende fout in client informatie:  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="command-line-syntax"></a><a name="bkmk_policyspy-syntax"></a>Opdracht regel syntaxis

Beleids Spy is voornamelijk bedoeld voor gebruik via de gebruikers interface. Het biedt beperkte opdracht regel opties voor het ondersteunen van automatisering en batch verwerking.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Selecteert`/export`
Met deze optie wordt het beleid van de lokale of externe computer op de achtergrond geëxporteerd. `<ExportFilename>`is de naam van het bestand waarmee het geëxporteerde XML-beleid wordt opgeslagen. Als u de `<computername>` optie opgeeft, exporteert Policy Spy het beleid van die computer in plaats van de lokale computer.

> [!Note]  
> Deze opdracht regel optie biedt geen manier om gebruikers referenties op te geven. Als u alternatieve referenties wilt gebruiken om toegang te krijgen tot een externe computer, gebruikt u de opdracht **runas** om een nieuwe opdracht prompt te openen met de vereiste beveiligings referenties.  


## <a name="usage"></a>Gebruik

### <a name="tools-menu"></a>Menu Extra

De volgende acties zijn beschikbaar in het menu **extra** :  

- **Open extern**: Hiermee maakt u verbinding met het Configuration Manager-client beleid op een externe computer. Gebruik het dialoog venster verbinding maken om de naam van de externe computer en optionele gebruikers referenties op te halen. Als de verbinding mislukt, wordt de fout informatie weer gegeven in het deel venster client gegevens. Als de verbinding opnieuw mislukt, probeert u verbinding te maken door **vernieuwen** te selecteren in het menu **bewerken** of door op F5 te drukken.  

- **Bestand openen**: Hiermee opent u een export bestand (XML) voor beleid dat is gemaakt met de optie **beleid exporteren** . Het hulp programma geeft het geëxporteerde beleid precies hetzelfde als een actief beleid. Sommige functies die alleen van toepassing zijn wanneer u verbinding maakt met een echte client, worden uitgeschakeld.  

- **Machine toewijzingen aanvragen**: Hiermee wordt een aanvraag voor computer beleids toewijzingen op de doel computer geactiveerd. Deze functie is uitgeschakeld wanneer het geëxporteerde beleid wordt weer gegeven.  

- **Machine beleid evalueren**: activeert een evaluatie van het computer beleid op de doel computer. Deze functie is uitgeschakeld bij het weer geven van een geëxporteerd beleid.  

- **Gebruikers toewijzingen aanvragen**: Hiermee wordt een aanvraag voor gebruikers beleids toewijzingen geactiveerd voor de gebruiker die momenteel is aangemeld. Deze functie is alleen beschikbaar wanneer een beleid op de lokale computer wordt weer gegeven.  

- **Gebruikers beleid evalueren**: Hiermee wordt een gebruikers beleids evaluatie geactiveerd voor de gebruiker die momenteel is aangemeld. Deze functie is alleen beschikbaar wanneer een beleid op de lokale computer wordt weer gegeven.  

- **Beleid opnieuw instellen**: verwijdert alle niet-standaard beleids regels en stelt de beleids cookies voor de site opnieuw in. Vervolgens wordt een aanvraag voor machine beleids toewijzingen geactiveerd. Deze functie is uitgeschakeld bij het weer geven van een geëxporteerd beleid.  

- **Beleid exporteren**: exporteert het beleid van de doel computer naar een XML-bestand. Bekijk dit bestand op elke computer met policy Spy. Als u het export bestand wilt openen, selecteert u **bestand openen** in het menu **extra** . Deze functie is uitgeschakeld bij het weer geven van een geëxporteerd beleid.  


### <a name="edit-menu"></a>Menu bewerken

De volgende acties zijn beschikbaar in het menu **bewerken** :  

- **Verwijderen**: Hiermee verwijdert u het geselecteerde exemplaar in het resultaten venster. Deze actie wordt alleen ondersteund voor beleids exemplaren. Als u probeert iets anders dan beleids exemplaren te verwijderen, wordt er een fout bericht weer gegeven. Deze functie is uitgeschakeld bij het weer geven van een geëxporteerd beleid.  

- **Vernieuwen**: Hiermee worden alle resultaten vernieuwd om de meest recente informatie weer te geven. Alle structuur knooppunten die zijn uitgevouwen voordat ze worden vernieuwd, worden later automatisch uitgebreid. Als beleids Spy geen verbinding heeft gemaakt met het beleid van de doel computer, probeert het opnieuw verbinding te maken. Deze functie is uitgeschakeld bij het weer geven van een geëxporteerd beleid.  

- **Gebeurtenissen wissen**: Hiermee wist u alle items van het tabblad gebeurtenissen.  



## <a name="results-pane"></a>Resultaten deel venster

In het deel venster met resultaten worden verschillende weer gaven van het beleids systeem op de doel computer weer gegeven. U opent deze weer gaven door op een van de volgende vier tabbladen te klikken: 
- [Werkelijk](#bkmk_policyspy-actual)
- [Aangevraagd](#bkmk_policyspy-requested)
- [Standaard](#bkmk_policyspy-default)
- [Gebeurtenissen](#bkmk_policyspy-events)


### <a name="actual"></a><a name="bkmk_policyspy-actual"></a>Effectief

Op dit tabblad wordt het huidige beleid van de client weer gegeven. Het huidige beleid bepaalt het gedrag van een client en het gedrag van de client agenten, zoals software distributie en-inventarisatie. Op het tabblad worden resultaten weer gegeven in een structuur indeling met een hoofd knooppunt voor de computer naam ruimte en elke gebruikersspecifieke naam ruimte. Vouw een naam ruimte knooppunt uit om een lijst met klassen weer te geven. Vouw een klasse uit om een lijst met exemplaren weer te geven. De lijst met klassen bevat alleen klassen met exemplaren.


### <a name="requested"></a><a name="bkmk_policyspy-requested"></a>Aangevraagde

Op dit tabblad worden de beleids toewijzingen weer gegeven die de client heeft opgehaald van de toegewezen site. Op het tabblad worden de resultaten weer gegeven in structuur indeling met een hoofd knooppunt voor de naam ruimte van de computer en elke gebruikersspecifieke naam ruimte. Voor het uitbreiden van een naam ruimte knooppunt worden de volgende knoop punten weer gegeven:  

- **Configuratie**: geeft een lijst weer van configuratie klassen die zijn afgeleid van CCM_Policy_Config, waaronder beleids object, toewijzingen en anderen.  

- **Instellingen**: geeft alle actieve instellingen weer die door het beleid worden gegenereerd. De instellingen worden weer gegeven onder het knoop punt configuratie. 

> [!Note]   
> Er kunnen meerdere exemplaren zijn met dezelfde naam omdat de client deze instellingen niet heeft samengevoegd in een uiteindelijke resulterende set. In Policy Spy worden instanties onder dit knoop punt weer gegeven met behulp van de RealKey-eigenschappen in plaats van de echte beleids sleutels. Correleer deze instanties met de resulterende set die wordt weer gegeven op het tabblad werkelijk.  


### <a name="default"></a><a name="bkmk_policyspy-default"></a>Prijs

Op dit tabblad wordt dezelfde informatie weer gegeven als het **aangevraagde** tabblad. Het bevat ook inhoud van de naam ruimten DefaultMachine en DefaultUser.


### <a name="events"></a><a name="bkmk_policyspy-events"></a>Evenementen

Op dit tabblad worden de gebeurtenissen van de beleids agent weer gegeven wanneer deze plaatsvinden. De weer gave maakt een WMI-gebeurtenis abonnement voor alle gebeurtenissen die zijn afgeleid van CCM_PolicyAgent_Event. De weer gave bevat een maximum van 200 gebeurtenissen. De oudste gebeurtenissen worden zo nodig boven aan de lijst verwijderd. Als u het laatste item in de lijst selecteert, schuift de lijst automatisch omlaag wanneer er nieuwe gebeurtenissen worden toegevoegd. Als dat niet het geval is, behoudt de weer gave de huidige positie en u moet omlaag of omlaag schuiven om nieuwe gebeurtenissen weer te geven. Deze weer gave is altijd leeg bij het weer geven van een geëxporteerd beleid.



## <a name="client-info-pane"></a>Deel venster client informatie
In het deel venster client informatie wordt een lijst met eigenschappen voor de doel computer weer gegeven. De volgende eigenschappen worden weer gegeven, indien beschikbaar:  
- Naam
- Id
- Versie
- Site
- Toegewezen MP
- Resident MP
- Proxy-MP
- Proxy status



## <a name="details-pane"></a>Detail venster
In het detail venster wordt gedetailleerde informatie weer gegeven over de huidige selectie. Als er geen selectie actief is, wordt er informatie weer gegeven over het beleid Spy zelf, met inbegrip van de versie. Anders wordt een MOF-representatie (manage object Format) van het geselecteerde item weer gegeven.

In beleids Spy wordt een eigen code voor het genereren van MOF gebruikt voor het maken van een gebruiks vriendelijker HTML-weer gave dan de MOF voor onbewerkte tekst die door WMI is gegenereerd. Dit gedrag stelt beleids Spy in staat om de volgende functies toe te voegen om de MOF beter leesbaar te maken:  

- Syntaxis markering  

- Inge sprongen objecten en matrices  

- Eigenschappen worden gerangschikt in systeem, overgenomen en lokale groepen. Standaard worden de systeem-en overgenomen groepen samengevouwen. U kunt meteen zien welke eigenschappen het exemplaar daad werkelijk gebruikt.  

- Kopieer MOF of kopieer onbewerkte tekst-MOF naar het klem bord. Deze functie is handig voor het plakken van de MOF in andere toepassingen door het hulp programma MofComp rechtstreeks aan te roepen.  

Voor exemplaren van beleids objecten die zijn afgeleid van CCM_Policy_Policy, wordt in het detail venster de beleids tekst weer gegeven onder de MOF die wordt weer gegeven. Als de client de beleids tekst niet heeft gedownload, wordt in Policy Spy een Hyper link weer gegeven. Klik op de koppeling om de beleids tekst rechtstreeks vanuit het beheer punt van de client te downloaden. Als het hulp programma de beleids tekst van het beleid downloadt, wordt de Hyper Link vervangen door de inhoud van het antwoord. Anders werkt Policy Spy de weer gave bij die aangeeft dat de aanvraag is mislukt.

