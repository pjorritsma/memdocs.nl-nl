---
title: CMTrace
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van het hulp programma CMTrace om logboek bestanden voor Configuration Manager weer te geven.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8c9c42dcd1e6a6a4ca064953f0513157f5ebb228
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723423"
---
# <a name="cmtrace"></a>CMTrace

*Van toepassing op: Configuration Manager (huidige vertakking)*

CMTrace is een van de [Configuration Manager-hulpprogram ma's](tools.md). Hiermee kunt u logboek bestanden weer geven en bewaken, met inbegrip van de volgende typen:  

- Logboek bestanden in de Configuration Manager-of CCM-indeling (client component Manager)  

- Platte ASCII-of Unicode-tekst bestanden, zoals Windows Installer logboeken  

Het hulp programma helpt bij het analyseren van logboek bestanden door te markeren, filteren en fout zoeken.

Vanaf versie 1806 wordt het hulp programma logboek weergave van CMTrace automatisch geïnstalleerd samen met de Configuration Manager-client. Deze wordt toegevoegd aan de installatiemap van de client. Dit is `%WinDir%\CCM\CMTrace.exe`standaard.<!--1357971-->

> [!Note]  
> CMTrace wordt niet automatisch bij Windows geregistreerd om de bestands extensie. log te openen. Zie [Bestands koppelingen](#file-associations)voor meer informatie.  

Vanaf versie 1906 is **OneTrace** een nieuwe logboek weergave met het ondersteunings centrum. Het werkt op dezelfde manier als CMTrace, met verbeteringen. Zie [ondersteunings centrum OneTrace](support-center-onetrace.md)voor meer informatie.

## <a name="usage"></a>Gebruik

Voer **CMTrace. exe**uit. De eerste keer dat u het hulp programma uitvoert, ziet u een prompt voor bestands koppeling. Zie [Bestands koppelingen](#file-associations)voor meer informatie.

U neemt de meeste acties in CMTrace uit de volgende menu's:

- [Bestand](#file-menu)
- [Hulpprogramma's](#tools-menu)

### <a name="file-menu"></a>Menu Bestand

De volgende acties zijn beschikbaar in het menu **bestand** :  

- [Openen](#open)
- [Openen op server](#open-on-server)
- [Afdrukken](#print)
- [Voorkeuren](#preferences)

Het menu bestand bevat ook de laatste acht recente bestanden. U kunt een van deze logboeken snel opnieuw openen door deze te selecteren in het menu bestand.

#### <a name="open"></a>Geopend

Hiermee wordt het dialoog venster openen weer gegeven om te bladeren naar een logboek bestand.

Filter de weer gave voor bestanden van de volgende typen:

- Logboek bestanden (\*. log)  
- Oude logboek bestanden (\*. lo_)
- Alle bestanden (\*.\*)

De volgende twee opties zijn standaard niet geselecteerd:  

- **Bestaande regels negeren**: als u deze selecteert, wordt de bestaande inhoud van het geselecteerde logboek bestand genegeerd en worden alleen nieuwe regels weer gegeven wanneer ze worden toegevoegd. Gebruik deze optie om alleen nieuwe acties te controleren wanneer u niet de volledige geschiedenis van het logboek bestand nodig hebt.  

- **Geselecteerde bestanden samen voegen**: als u deze optie inschakelt en meer dan één logboek bestand selecteert, voegt CMTrace de geselecteerde Logboeken in de weer gave samen. Ze worden weer gegeven alsof ze een enkel logboek bestand zijn. Het samengevoegde logboek werkt hetzelfde en ondersteunt alle andere CMTrace-functies alsof het een enkel logboek bestand is.  

#### <a name="open-on-server"></a>Openen op server

Blader in de map Configuration Manager logs op een site systeem computer met het standaard dialoogvenster Bladeren. U kunt ook bladeren in het netwerk voor een externe computer.

Wanneer u een externe computer selecteert om te bladeren, controleert CMTrace of de Configuration Manager share. Als een share met Configuration Manager-logboek bestanden niet kan worden gevonden, wordt er een fout bericht weer gegeven.  

Als u rechtstreeks verbinding wilt maken met een bekende computer zonder te bladeren, gebruikt u de actie [openen](#open) . Voer vervolgens de naam en share van de server in met de UNC-indeling.

#### <a name="print"></a>Afdrukken

Het standaard Windows-dialoog venster afdrukken weer geven. Met deze actie wordt het huidige logboek bestand naar een printer verzonden. De uitvoer wordt opgemaakt op basis van de instellingen op het tabblad afdrukken van CMTrace-voor keuren.

#### <a name="preferences"></a>Voorkeuren

Configureer instellingen voor CMTrace. De volgende opties zijn beschikbaar:  

- Tabblad **Algemeen**  

    - **Update-interval**: bepaalt hoe vaak CMTrace controleert op wijzigingen in logboek bestanden en nieuwe regels laadt. Deze waarde is standaard 500 milliseconden.  

    - **Highlight**: Hiermee stelt u de kleur in die CMTrace gebruikt voor het markeren van logboek regels die u kiest. Standaard is deze kleur basis geel (rood: 255, groen: 255, blauw: 0).  

    - **Columns**: Hiermee configureert u de kolommen die zichtbaar zijn in de logboek weergave en de volg orde waarin ze worden weer gegeven. Standaard worden de logboek tekst, het onderdeel, de datum/tijd en de thread weer gegeven.  

- Tabblad **afdrukken**  

    - **Columns**: Configureer welke kolommen worden gebruikt bij het afdrukken van logboek bestanden en de volg orde waarin ze worden weer gegeven. Standaard worden dezelfde kolommen afgedrukt als wordt weer gegeven.  

    - **Orientation**: Hiermee stelt u de standaard afdruk stand in bij het afdrukken van logboek bestanden. Vervang deze instelling in het dialoog venster afdrukken. Standaard wordt de afdruk stand staand gebruikt.  

- Tabblad **Geavanceerd**  

    - **Vernieuwings interval**: forceert CMTrace om de logboek weergave bij te werken met een opgegeven interval bij het laden van een groot aantal regels. Deze optie is standaard uitgeschakeld met de waarde nul.  

        > [!Note]  
        > In het algemeen moet u het **Vernieuwings interval**niet wijzigen. Het kan aanzienlijk verhogen hoe lang het duurt om grote logboek bestanden te openen.

### <a name="tools-menu"></a>Menu Extra

De volgende acties zijn beschikbaar in het menu **extra** :

- [Moeilijk](#find)
- [Volgende zoeken](#find-next)
- [Naar klembord kopiëren](#copy-to-clipboard)
- [Markeren](#highlight)
- [Filter](#filter)
- [Fout bij zoeken](#error-lookup)
- [Onderbreken](#pause)
- [Details weer geven/verbergen](#showhide-details)
- [Info venster weer geven/verbergen](#showhide-info-pane)

#### <a name="find"></a>Find

Zoek in het geopende logboek bestand naar een opgegeven teken reeks.  

#### <a name="find-next"></a>Volgende zoeken

Hiermee zoekt u de volgende overeenkomende teken reeks, zoals u eerder hebt opgegeven in het dialoog venster zoeken.  

#### <a name="copy-to-clipboard"></a>Naar klembord kopiëren

Hiermee worden de geselecteerde regels als tekst zonder opmaak naar het Windows-klem bord gekopieerd. Als u Configuration Manager en CCM-logboek bestanden bekijkt, worden de kolommen in dezelfde volg orde als de weer gave gekopieerd. Elke kolom wordt gescheiden door een tabteken. Gebruik deze actie bij het kopiëren van logboeken naar e-mail berichten of andere documenten.  

#### <a name="highlight"></a>Markeren

Voer een teken reeks in die door CMTrace wordt gebruikt om de tekst van elk logboek item te doorzoeken. Vervolgens wordt de logboek tekst gemarkeerd die overeenkomt met de teken reeks die u invoert.  

- De markering gebruikt de kleur die u hebt opgegeven in voor keuren.  

- Als u markeren wilt uitschakelen, verwijdert u de teken reeks uit dit veld.  

- Als u een decimaal of hexadecimaal getal opgeeft, probeert CMTrace de waarde te vergelijken met de thread kolom. U kunt dit gedrag gebruiken om de verwerking van één thread te markeren, zonder dat er andere threads worden gefilterd die er mogelijk mee kunnen communiceren.  

- Als u teken reeksen wilt vergelijken per case, schakelt u de optie voor **hoofdletter gevoelig**in.  

#### <a name="filter"></a>Filteren

Logboek regels weer geven of verbergen op basis van de opgegeven criteria. Filters toep assen op een van de vier kolommen, ongeacht of ze zichtbaar zijn. Deze instellingen zijn van toepassing op elk geopend logboek bestand.

Voorbeelden:
<!--SCCMDocs issue #603-->

- Filter **bestand smsts. log** op invoer tekst met de actie of de groep.
- Filter **InventoryAgent. log** waarbij de invoer tekst ' Destination ' bevat.

#### <a name="error-lookup"></a>Fout bij zoeken

Typ of plak een fout code in een decimale of hexadecimale notatie om een beschrijving weer te geven. Mogelijke fout bronnen zijn: Windows, WMI of WinHTTP.

#### <a name="pause"></a>Onderbreken

Logboek bewaking onderbreken of opnieuw starten. De volgende use cases zijn een aantal van de mogelijke redenen om deze actie te gebruiken:  

- Wanneer CMTrace de gegevens van het logboek bestand te snel weergeeft  

- Wanneer u de logboek bewaking onderbreekt, gaan de gegevens die CMTrace worden weer gegeven niet verloren als het huidige bestand wordt overgeschakeld naar een nieuw logboek  

- Wanneer u wilt voor komen dat CMTrace de nieuwe gegevens weergeeft terwijl u het logboek bestand bekijkt  

#### <a name="showhide-details"></a>Details weer geven/verbergen

Alle kolommen behalve de logboek tekst weer geven of verbergen. Ook wordt de kolom logboek tekst uitgebreid naar de breedte van het venster. Gebruik deze actie wanneer u logboeken bekijkt op een computer met een lage weergave resolutie. Meer van de logboek tekst wordt weer gegeven.  

> [!Note]  
> Bij het weer geven van onbewerkte-tekst bestanden worden de details in CMTrace automatisch verborgen omdat ze altijd leeg zijn.  

#### <a name="showhide-info-pane"></a>Info venster weer geven/verbergen

Het deel venster Info weer geven of verbergen. Gebruik deze actie wanneer u logboeken bekijkt op een computer met een lage weergave resolutie. Meer logboek Details worden weer gegeven.  


## <a name="log-pane"></a>Deel venster Logboek

Het deel venster logboek bevindt zich boven aan het CMTrace-venster. Hiermee worden regels uit logboek bestanden weer gegeven.

Wanneer u een regel selecteert, wordt deze tijdelijk gemarkeerd met het Windows-selectie kleuren schema.

De gemarkeerde regels voldoen aan de criteria die u definieert met de optie **markeren** in het menu **extra** . De markering gebruikt de kleur die u opgeeft in **voor keuren**.

CMTrace worden regels met fouten weer gegeven met een rode achtergrond en een gele tekst kleur. In CCM: logboek vermeldingen hebben een expliciete type waarde die de vermelding als een fout aanduidt. Voor andere logboek indelingen heeft CMTrace een hoofdletter gevoelige zoek opdracht in elk item voor elke teken reeks die overeenkomt met "Error".

Er worden regels met waarschuwingen weer gegeven met een gele achtergrond. In CCM: logboek vermeldingen hebben een expliciete type waarde die de vermelding als een waarschuwing aanduidt. Voor andere logboek indelingen heeft CMTrace een niet-hoofdletter gevoelige zoek opdracht in elk item voor elke teken reeks die overeenkomt met ' warn '.


## <a name="info-pane"></a>Informatie venster

Het deel venster Info bevindt zich onder aan het CMTrace-venster. Het bevat de volgende functies:

- Details over de momenteel geselecteerde logboek vermelding  

- Een tekstvak waarin de logboek tekst wordt weer gegeven  

- Er worden regel terugloop tekens weer gegeven zodat opgemaakte tekst gemakkelijker te lezen is  

- Lange vermeldingen die niet volledig zichtbaar zijn in het deel venster Logboeken zijn gemakkelijker te lezen.  

Het deel venster Info weer geven of verbergen met de optie **info deel venster weer geven/verbergen** in het menu **extra** . Als het deel venster info meer dan de helft van het logboek venster inneemt, wordt het in CMTrace automatisch verborgen.

### <a name="progress-bar"></a>Voortgangs balk

Wanneer u een logboek bestand voor het eerst opent, vervangt CMTrace het deel venster Info door een voortgangs balk. Deze voortgang geeft aan hoeveel van de bestaande bestands inhoud wordt geladen. De voortgang bereikt 100 procent, CMTrace verwijdert de voortgangs balk en vervangt deze door het deel venster Info. Wanneer u grote bestanden laadt, geeft dit gedrag u een indicatie van hoe lang de belasting kan duren.

### <a name="status-bar"></a>Status balk

Op de status balk van Configuration Manager-indeling en CCM-indelings logboek bestanden wordt de verstreken tijd voor de geselecteerde logboek vermeldingen weer gegeven. Als u één item selecteert, wordt in het hulp programma de tijd weer gegeven van de eerste logboek vermelding tot het geselecteerde item. Als u meerdere vermeldingen selecteert, wordt de tijd van de bovenste geselecteerde vermelding berekend naar het onderste geselecteerde item. CMTrace maakt deze informatie als volgt:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`


## <a name="windows-shell-integration"></a>Integratie met Windows-shell

CMTrace ondersteunt [Bestands koppelingen](#file-associations) en [slepen en neerzetten](#drag-and-drop).

### <a name="file-associations"></a>Bestands koppelingen

CMTrace kan zichzelf koppelen aan. log-en. lo_ bestandsnaam extensies. Wanneer het programma wordt gestart, wordt het REGI ster gecontroleerd om te bepalen of het al is gekoppeld aan deze bestandsnaam extensies. Als CMTrace nog niet is gekoppeld aan bestandsnaam extensies, wordt u gevraagd om de bestandsnaam extensies te koppelen aan CMTrace. Als u **deze optie niet opnieuw vragen**selecteert, slaat CMTrace deze controle over wanneer deze wordt uitgevoerd op deze computer.

### <a name="drag-and-drop"></a>Slepen en neerzetten

CMTrace biedt ondersteuning voor eenvoudige functionaliteit voor slepen en neerzetten. Sleep een logboek bestand van Windows Verkenner naar CMTrace om het te openen.


## <a name="other-tips"></a>Andere tips

### <a name="last-directory-registry-key"></a>Register sleutel voor de laatste map

<!--511280-->
Standaard slaat CMTrace de laatste logboek locatie op die u hebt geopend. Dit gedrag is nuttig op de site server, omdat het standaard wordt ingesteld op het pad logs.

De eerste keer dat u deze op een-client start, wordt standaard de actieve werkmap gebruikt. Deze locatie kan het pad zijn waar u CMTrace hebt opgeslagen, of een pad `%userprofile%\Desktop`zoals.

De **laatste map** -waarde in de register `HKEY_CURRENT_USER\Software\Microsoft\Trace32` sleutel bepaalt deze standaard locatie. Als u deze waarde instelt `%windir%\CCM\Logs` op uw clients, opent CMTrace bestanden in de logboek locatie van de client de eerste keer dat u deze uitvoert.


## <a name="see-also"></a>Zie ook

- [Logboekbestanden](../plan-design/hierarchy/log-files.md)

- [Logboek bestand viewer voor ondersteunings centrum](support-center.md#support-center-log-file-viewer)

- [Ondersteunings centrum OneTrace](support-center-onetrace.md)
