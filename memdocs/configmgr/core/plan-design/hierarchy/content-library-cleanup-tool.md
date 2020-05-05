---
title: Hulpprogramma voor het opschonen van de inhoudsbibliotheek
titleSuffix: Configuration Manager
description: Gebruik het hulp programma voor opruimen van inhouds bibliotheken om zwevende inhoud te verwijderen die niet meer aan een Configuration Manager-implementatie is gekoppeld.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b1b415d5c24800f003f730426216ac7cf190a4f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720217"
---
# <a name="content-library-cleanup-tool"></a>Hulpprogramma voor het opschonen van de inhoudsbibliotheek

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik het opdracht regel programma voor het opschonen van de inhouds bibliotheek om inhoud te verwijderen die niet meer is gekoppeld aan een pakket of toepassing op een distributie punt. Dit type inhoud heet *zwevende inhoud*. Dit hulp programma vervangt oudere versies van vergelijk bare hulpprogram ma's die zijn uitgebracht voor eerdere Configuration Manager producten.  

Het hulp programma is alleen van invloed op de inhoud van het distributie punt dat u opgeeft wanneer u het hulp programma uitvoert. Het hulp programma kan geen inhoud verwijderen uit de inhouds bibliotheek op de site server.

Zoek **ContentLibraryCleanup. exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` op de site server.



## <a name="requirements"></a>Vereisten  

- Voer het hulp programma alleen uit op één distributie punt tegelijk.  

- Voer de toepassing rechtstreeks uit op de computer waarop het distributie punt wordt gehost, of op afstand vanaf een andere computer.  

- Het gebruikers account dat het hulp programma uitvoert, moet dezelfde machtigingen hebben als de beveiligingsrol **volledige beheerder** in Configuration Manager.  



## <a name="modes-of-operation"></a>Bedrijfsmodi

Voer het hulp programma uit in de volgende twee modi: [What-if](#what-if-mode) en [Delete](#delete-mode).

> [!Tip]  
> Begin met de modus ' *wat als'* '. Wanneer u tevreden bent met de resultaten, voert u het hulp programma uit in de modus *verwijderen* .  


### <a name="what-if-mode"></a>Modus voor ' wat als' '   

Als u de `/delete` para meter niet opgeeft, wordt het hulp programma uitgevoerd in de modus What-if. In deze modus wordt de inhoud geïdentificeerd die uit het distributie punt zou worden verwijderd.

- Wanneer u deze modus uitvoert, worden er door het hulp programma geen gegevens verwijderd.  

- Het hulp programma schrijft naar het logboek bestand informatie over de inhoud die wordt verwijderd. U wordt niet gevraagd om elke mogelijke verwijdering te bevestigen.  


### <a name="delete-mode"></a>Verwijder modus   

Wanneer u het hulp programma uitvoert met `/delete` de para meter, wordt het hulp programma uitgevoerd in de modus verwijderen.

- Wanneer u deze modus uitvoert, kan zwevende inhoud die op het opgegeven distributie punt wordt gevonden, worden verwijderd uit de inhouds bibliotheek van het distributie punt.  

- Voordat u elk bestand verwijdert, controleert u of het hulp programma het moet verwijderen. Selecteer **Y** voor Ja, **N** voor Nee of **Ja op alles** om verdere vragen te overs Laan en alle zwevende inhoud te verwijderen.  


### <a name="log-file"></a>Logboekbestand

Wanneer het hulp programma in een van beide modi wordt uitgevoerd, wordt er automatisch een logboek gemaakt. De naam van het logboek bestand met de volgende informatie: 
- De modus waarin het hulp programma wordt uitgevoerd  
- De naam van het distributie punt  
- De datum en tijd van de bewerking  

Wanneer het hulp programma is voltooid, wordt automatisch het logboek bestand in Windows geopend. 

Het hulp programma schrijft standaard het logboek bestand naar de map Temp van het gebruikers account dat het hulp programma uitvoert. Deze locatie bevindt zich op de computer waarop u het hulp programma uitvoert. Dit is niet altijd het doel van het hulp programma. Gebruik de `/log` para meter om het logboek bestand om te leiden naar een andere locatie, met inbegrip van een netwerk share.



## <a name="run-the-tool"></a>Het hulp programma uitvoeren

Het hulp programma uitvoeren: 

1. Open een opdrachtprompt als beheerder. Wijzig de Directory in de map die **ContentLibraryCleanup. exe**bevat.  

2. Voer een opdracht regel in met de vereiste [opdracht regel parameters](#bkmk_params)en eventuele optionele para meters die u wilt gebruiken.



## <a name="command-line-parameters"></a><a name="bkmk_params"></a>Opdracht regel parameters  

Gebruik deze opdracht regel parameters in een wille keurige volg orde.   

### <a name="required-parameters"></a>Vereiste para meters

|Parameter|Details|
|---------|-------|
| `/dp <distribution point FQDN>`  | Geef de Fully Qualified Domain Name (FQDN) op van het distributie punt dat u wilt opschonen. |
| `/ps <primary site FQDN>` | Alleen *vereist* bij het opschonen van inhoud van een distributie punt op een secundaire site. Het hulp programma maakt verbinding met de bovenliggende primaire site om query's uit te voeren op de SMS-provider. Met deze query's kan het hulp programma bepalen welke inhoud moet worden gedistribueerd op het distributie punt. Vervolgens kan de zwevende inhoud worden geïdentificeerd die moet worden verwijderd. Deze verbinding met de bovenliggende primaire site moet worden gemaakt voor distributie punten op een secundaire site, omdat de vereiste gegevens niet rechtstreeks van de secundaire site beschikbaar zijn.|
| `/sc <primary site code>`  | Alleen *vereist* bij het opschonen van inhoud van een distributie punt op een secundaire site. Geef de site code op van de bovenliggende primaire site. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Voor beeld: de inhoud die wordt verwijderd (What-if) scannen en registreren
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Voor beeld: inhoud scannen en logboeken voor een DP op een secundaire site
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Optionele parameters

|Parameter|Details|
|---------|-------|
|`/delete`| Gebruik deze para meter wanneer u klaar bent om inhoud te verwijderen van het distributie punt. U wordt gevraagd om de inhoud te verwijderen. </br></br> Wanneer u deze para meter niet gebruikt, registreert het hulp programma de resultaten van de inhoud die wordt verwijderd. Zonder deze para meter verwijdert het geen inhoud van het distributie punt. |
| `/q` | Met deze para meter wordt het hulp programma uitgevoerd in een stille modus waarmee alle prompts worden onderdrukt. Deze vragen moeten worden meegenomen wanneer de inhoud wordt verwijderd. Het logboek bestand wordt ook niet automatisch geopend. |
| `/ps <primary site FQDN>` | Optioneel alleen bij het opschonen van inhoud van een distributie punt op een primaire site. Geef de FQDN op van de primaire site waarvan het distributie punt deel uitmaakt. |
| `/sc <primary site code>` | Optioneel alleen bij het opschonen van inhoud van een distributie punt op een primaire site. Geef de site code op van de primaire site waarvan het distributie punt deel uitmaakt. |
| `/log <log file directory>` | Geef de locatie op waar het hulp programma het logboek bestand schrijft. Deze locatie kan een lokaal station of een netwerk share zijn.</br></br> Wanneer u deze para meter niet gebruikt, plaatst het hulp programma het logboek bestand in de map Temp van de gebruiker op de computer waarop het hulp programma wordt uitgevoerd.|

#### <a name="example-delete-content"></a>Voor beeld: inhoud verwijderen 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Voor beeld: inhoud zonder prompts verwijderen
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Voor beeld: aanmelden bij lokaal station
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Voor beeld: aanmelden bij netwerk share
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Bekend probleem

Wanneer een pakket of implementatie mislukt of wordt uitgevoerd, kan het hulp programma de volgende fout retour neren:`System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Er is geen oplossing voor dit probleem. Het hulp programma kan geen zwevende bestanden identificeren wanneer de inhoud wordt uitgevoerd of niet kan worden geïmplementeerd. Met het hulp programma kunt u inhoud pas opschonen als u dit probleem hebt opgelost.
