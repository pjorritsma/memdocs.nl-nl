---
title: De inhoudsbibliotheek
titleSuffix: Configuration Manager
description: Meer informatie over de inhouds bibliotheek die Configuration Manager gebruikt om de totale grootte van gedistribueerde inhoud te verminderen.
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d7432b3522d5292e2c2afc1dac6b8db3382cca12
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343164"
---
# <a name="the-content-library-in-configuration-manager"></a>De inhouds bibliotheek in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De inhouds bibliotheek is een opslag met één exemplaar van inhoud in Configuration Manager. De site gebruikt IT om de totale omvang van de gecombineerde hoofd tekst van de inhoud die u distribueert te reduceren. De inhouds bibliotheek slaat alle inhouds bestanden op voor software-implementaties, bijvoorbeeld: software-updates, toepassingen en besturingssysteem implementaties.  

- De site maakt en onderhoudt automatisch een kopie van de inhouds bibliotheek op elke site server en elk distributie punt.  

- Voordat Configuration Manager inhouds bestanden toevoegt aan de site server of de bestanden kopieert naar distributie punten, wordt gecontroleerd of elk inhouds bestand al aanwezig is in de inhouds bibliotheek.  

- Als het inhouds bestand beschikbaar is, Configuration Manager het bestand niet kopiëren. In plaats daarvan wordt het bestaande inhouds bestand gekoppeld aan de toepassing of het pakket.  

Configureer op distributiepunt servers de volgende opties:

- Een of meer schijf stations waarop u de inhouds bibliotheek wilt maken.  

- Een prioriteit voor elk station dat u gebruikt.  

Configuration Manager kopieert inhouds bestanden naar het station met de hoogste prioriteit totdat het station minder dan een minimale hoeveelheid beschik bare ruimte bevat die u opgeeft.  

- U configureert de instellingen van het station tijdens de installatie van het distributie punt.  

- U kunt de instellingen van het station in de eigenschappen van het distributie punt niet configureren nadat de installatie is voltooid.  

Zie [inhoud en infra structuur voor inhoud beheren](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)voor meer informatie over het configureren van de stations-instellingen voor het distributie punt.  

> [!IMPORTANT]
> Als u de inhouds bibliotheek na de installatie wilt verplaatsen naar een andere locatie op een distributie punt, gebruikt u het hulp programma voor de **overdracht van inhouds bibliotheken** in de Configuration Manager-hulpprogram ma's. Zie het hulp programma voor de [overdracht van inhouds bibliotheken](../../support/content-library-transfer.md)voor meer informatie.  


## <a name="about-the-content-library-on-the-central-administration-site"></a>Informatie over de inhouds bibliotheek op de centrale beheer site

Configuration Manager maakt standaard een inhouds bibliotheek op de centrale beheer site wanneer de site wordt geïnstalleerd. De inhouds bibliotheek bevindt zich op het station van de site server met de meeste vrije schijf ruimte. Omdat u een distributie punt niet kunt installeren op de centrale beheer site, kunt u geen prioriteit geven aan de stations die worden gebruikt door de inhouds bibliotheek. Net als de inhouds bibliotheek op andere site servers en op distributie punten, wordt de inhouds bibliotheek automatisch gedistribueerd naar het volgende beschik bare station wanneer het station met de inhouds bibliotheek geen beschik bare schijf ruimte meer heeft.  

Configuration Manager maakt gebruik van de inhouds bibliotheek op de centrale beheer site in de volgende scenario's:  

- U maakt inhoud op de centrale beheer site  

- U kunt inhoud migreren vanaf een andere Configuration Manager-site en de centrale beheer site toewijzen als de site die de inhoud beheert  

> [!NOTE]  
> Wanneer u inhoud maakt op een primaire site en deze vervolgens distribueert naar een andere primaire site of een secundaire site onder een andere primaire site, slaat de centrale beheer site die inhoud tijdelijk op in het postvak in van de planner op de centrale beheer site, maar voegt die inhoud niet toe aan de inhouds bibliotheek.  

Gebruik de volgende opties voor het beheren van de inhouds bibliotheek op de centrale beheer site:  

- Als u wilt voor komen dat de inhouds bibliotheek op een specifiek station wordt geïnstalleerd, maakt u een leeg bestand met de naam **no_sms_on_drive. SMS**. Kopieer het naar de hoofdmap van het station voordat de inhouds bibliotheek wordt gemaakt.  

- Nadat de inhouds bibliotheek is gemaakt, gebruikt u het hulp programma voor het overdragen van de **inhouds bibliotheek** van de Configuration Manager-hulpprogram ma's om de locatie van de inhouds bibliotheek te beheren. Zie het hulp programma voor de [overdracht van inhouds bibliotheken](../../support/content-library-transfer.md)voor meer informatie.  

> [!Note]  
> Distributie punten in de Cloud gebruiken geen opslag met één exemplaar. De site versleutelt pakketten voordat deze naar Azure worden verzonden en elk pakket heeft een unieke versleutelde sleutel. Zelfs als twee bestanden identiek waren, zijn de versleutelde versies niet hetzelfde.  


## <a name="configure-a-remote-content-library-for-the-site-server"></a><a name="bkmk_remote"></a>Een externe inhouds bibliotheek voor de site server configureren

<!--1357525-->
Vanaf versie 1806, om de [hoge Beschik baarheid van de site server](../../servers/deploy/configure/site-server-high-availability.md) te configureren of om ruimte op de vaste schijf vrij te maken op uw centrale beheer-of primaire site servers, moet u de inhouds bibliotheek verplaatsen naar een andere opslag locatie. Verplaats de inhouds bibliotheek naar een ander station op de site server, een afzonderlijke server of fout tolerante schijven in een Storage Area Network (SAN). Een SAN wordt aanbevolen omdat het Maxi maal beschikbaar is en een elastische opslag biedt die in de loop van de tijd verg root of verkleint om te voldoen aan de veranderende vereisten voor inhoud. Zie [Opties voor hoge Beschik baarheid](../../servers/deploy/configure/site-server-high-availability.md)voor meer informatie.

Een externe inhouds bibliotheek is een vereiste voor [hoge Beschik baarheid van site server](../../servers/deploy/configure/site-server-high-availability.md).

> [!Note]  
> Met deze actie wordt alleen de inhouds bibliotheek op de site server verplaatst. Dit heeft geen invloed op de locatie van de inhouds bibliotheek op distributie punten. 

> [!Tip]  
> Plan ook het beheer van pakket bron inhoud, die extern is voor de inhouds bibliotheek. Elk software object in Configuration Manager heeft een pakket bron op een netwerk share. Overweeg alle bronnen op één share te centraliseren, maar zorg ervoor dat deze locatie overbodig en Maxi maal beschikbaar is.
>
> Als u de inhouds bibliotheek naar hetzelfde opslag volume als uw pakket bronnen verplaatst, kunt u dit volume niet markeren voor gegevensontdubbeling. Hoewel de inhouds bibliotheek ondersteuning biedt voor gegevensontdubbeling, ondersteunt het pakket bron volume het niet. Zie [gegevensontdubbeling](../configs/support-for-windows-features-and-networks.md#bkmmk_datadedup)voor meer informatie.<!--SCCMDOcs issue #831-->  

### <a name="prerequisites"></a>Vereisten  

- Het computer account van de site server moet machtigingen voor **volledig beheer** hebben voor het netwerkpad waarnaar u de inhouds bibliotheek verplaatst. Deze machtiging is van toepassing op zowel de share als het bestands systeem. Er zijn geen onderdelen geïnstalleerd op het externe systeem.

- De-site server kan geen rol voor distributie punt hebben. Het distributie punt gebruikt ook de inhouds bibliotheek en deze rol biedt geen ondersteuning voor een externe inhouds bibliotheek. Nadat u de inhouds bibliotheek hebt verplaatst, kunt u de distributiepuntrol niet toevoegen aan de site server.  

- Het externe systeem voor de inhouds bibliotheek moet zich in een vertrouwd domein bestaan.

> [!Important]  
> Hergebruik een gedeelde netwerk locatie tussen meerdere sites niet. Gebruik bijvoorbeeld niet hetzelfde pad voor zowel een centrale beheer site als een onderliggende primaire site. Deze configuratie biedt de mogelijkheid om de inhouds bibliotheek te beschadigen en u moet deze opnieuw samen stellen.<!--SCCMDocs-pr issue 2764-->  

### <a name="process-to-manage-the-content-library"></a>Proces voor het beheren van de inhouds bibliotheek

1. Maak een map in een netwerk share als het doel voor de inhouds bibliotheek. Bijvoorbeeld `\\server\share\folder`.  

    > [!Warning]  
    > Gebruik een bestaande map niet opnieuw met inhoud. Gebruik bijvoorbeeld niet dezelfde map als uw pakket bronnen. Voordat u de inhouds bibliotheek kopieert, verwijdert Configuration Manager alle bestaande inhoud van de locatie die u opgeeft.  

2. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit, selecteer het knoop punt **sites** en selecteer de site. Op het tabblad **samen vatting** onder in het detail venster ziet u een nieuwe kolom voor de **inhouds bibliotheek**.  

3. Selecteer **inhouds bibliotheek beheren** op het lint.  

4. In het venster inhouds bibliotheek beheren worden het lokale station en pad weer gegeven in het veld **huidige locatie** . Voer een geldig netwerkpad in voor de **nieuwe locatie**. Dit pad is de locatie waarnaar de site de inhouds bibliotheek verplaatst. De naam moet een mapnaam bevatten die al bestaat op de share, bijvoorbeeld `\\server\share\folder` . Selecteer **OK**.  

5. Noteer de **status** waarde in de kolom inhouds bibliotheek op het tabblad samen vatting van het detail venster. Hiermee wordt de voortgang van de site weer gegeven bij het verplaatsen van de inhouds bibliotheek.  

   - Terwijl **de waarde wordt** **verplaatst** , wordt het percentage voltooid weer gegeven.  

        > [!Note]  
        > Als u een grote inhouds bibliotheek hebt, ziet u mogelijk `0%` een tijdje de voortgang in de console. Als u bijvoorbeeld een bibliotheek van 1 TB hebt, moet deze 10 GB kopiëren voordat deze wordt weer gegeven `1%` . Controleer **distmgr. log**, waarin het aantal bestanden en gekopieerde bytes wordt weer gegeven. Vanaf versie 1810 wordt in het logboek bestand ook een geschatte resterende tijd weer gegeven.

   - Als er een fout optreedt, wordt de fout weer gegeven in de status. Veelvoorkomende fouten zijn onder andere **geweigerde toegang** of de **schijf is vol**.  

   - Als volt ooien wordt weer gegeven, **is voltooid**.  

     Raadpleeg **distmgr. log** voor meer informatie. Zie [Logboeken site server en site systeem server](log-files.md#BKMK_SiteSiteServerLog)voor meer informatie.  

Zie voor meer informatie over dit proces [stroom diagram-inhouds bibliotheek beheren](manage-content-library-flowchart.md).

De site *kopieert* de inhouds bibliotheek bestanden daad werkelijk naar de externe locatie. Dit proces verwijdert de inhouds bibliotheek bestanden niet op de oorspronkelijke locatie op de site server. Om ruimte vrij te maken, moet een beheerder deze oorspronkelijke bestanden hand matig verwijderen.

Als de oorspronkelijke inhouds bibliotheek twee schijven omvat, wordt deze samengevoegd tot één map op de nieuwe bestemming.

Vanaf versie 1810 worden er tijdens het kopieer proces geen nieuwe pakketten verwerkt door de onderdelen **despooler** en **Distribution Manager** . Met deze actie zorgt u ervoor dat de inhoud niet wordt toegevoegd aan de bibliotheek tijdens het verplaatsen. U kunt deze wijziging ook plannen tijdens het onderhoud van het systeem.

Als u de inhouds bibliotheek terug naar de site server wilt verplaatsen, herhaalt u dit proces, maar voert u een lokaal station en pad in voor de **nieuwe locatie**. De naam moet een mapnaam bevatten die al op het station bestaat, bijvoorbeeld `D:\SCCMContentLib` . Wanneer de oorspronkelijke inhoud nog bestaat, verplaatst het proces de configuratie snel naar de lokale locatie van de site server.

> [!Tip]  
> Als u de inhoud naar een ander station op de site server wilt verplaatsen, gebruikt u het hulp programma voor de **overdracht van inhouds bibliotheken** . Zie het hulp programma voor de [overdracht van inhouds bibliotheken](../../support/content-library-transfer.md)voor meer informatie.  


## <a name="inside-the-content-library"></a>In de inhouds bibliotheek

> [!Warning]  
> De volgende sectie is alleen ter informatie bedoeld. U kunt geen bestanden of mappen in de inhouds bibliotheek wijzigen, toevoegen of verwijderen. Dit kan ertoe leiden dat pakketten, inhoud of de inhouds bibliotheek als geheel worden beschadigd. Als u vermoedt dat ontbrekende, beschadigde of anderszins ongeldige gegevens bevatten, gebruikt u de validatie functie in de Configuration Manager-console om dergelijke problemen te detecteren. Distribueer de betrokken inhoud vervolgens opnieuw om de problemen op te lossen.

De inhouds bibliotheek wordt standaard opgeslagen in de hoofdmap van een station in een map met de naam **SCCMContentLib**. Deze map wordt standaard gedeeld als **SCCMContentLib $**. De map en share hebben beperkte machtigingen om onbedoelde schade te voor komen. Alle wijzigingen moeten worden aangebracht vanuit de Configuration Manager-console. In deze map bevinden zich de volgende objecten:  

- De pakket bibliotheek (**PkgLib** -map): informatie over welke pakketten aanwezig zijn op het distributie punt.  

- De gegevens bibliotheek (**DataLib** map): informatie over de oorspronkelijke structuur van de pakketten.  

- De bestands bibliotheek (**FileLib** map): de oorspronkelijke bestanden in het pakket. In deze map wordt meestal het meren deel van de opslag gebruikt.  

![Diagram overzicht van Configuration Manager inhouds bibliotheek](media/content-library-overview.png)

> [!Tip]  
> Gebruik het hulp programma **inhouds bibliotheek Verkenner** van de Configuration Manager-hulpprogram ma's om de inhoud van de inhouds bibliotheek te doorzoeken. U kunt dit hulp programma niet gebruiken om de inhoud te wijzigen. Het biedt inzicht in wat er aanwezig is, en kan validatie en herdistributie toestaan. Zie de [inhouds bibliotheek Verkenner](../../support/content-library-explorer.md)voor meer informatie.  

### <a name="package-library"></a>Pakket bibliotheek

De map pakket bibliotheek, **PkgLib**, bevat één bestand voor elk pakket dat naar het distributie punt wordt gedistribueerd. De bestands naam is de pakket-ID, bijvoorbeeld `ABC00001.INI` . In dit bestand in de `[Packages]` sectie vindt u een lijst met inhouds-id's die deel uitmaken van het pakket, evenals andere informatie, zoals de versie. **ABC00001** is bijvoorbeeld een verouderd pakket op versie **1**. De inhouds-ID in dit bestand is `ABC00001.1` .

### <a name="data-library"></a>Gegevens bibliotheek

De map gegevens bibliotheek, **DataLib**, bevat één bestand en één map voor elk van de inhoud van elk pakket. Dit bestand en deze map hebben bijvoorbeeld de naam `ABC00001.1.INI` en `ABC00001.1` respectievelijk. Het bestand bevat informatie voor validatie. De map maakt opnieuw de mapstructuur van het oorspronkelijke pakket.

De bestanden in de gegevens bibliotheek worden vervangen door INI-bestanden met de naam van het oorspronkelijke bestand in het pakket. Bijvoorbeeld `MyFile.exe.INI`. Deze bestanden bevatten informatie over het oorspronkelijke bestand, zoals de grootte, de tijd die is gewijzigd en de hash. Gebruik de eerste vier tekens van de hash om het oorspronkelijke bestand in de bestands bibliotheek te vinden. De hash in MyFile. exe. INI is bijvoorbeeld **DEF98765**en de eerste vier tekens zijn **DEF9**.

### <a name="file-library"></a>Bestands bibliotheek

Als de inhouds bibliotheek zich op meerdere stations bevindt, kan het zijn dat de pakket bestanden zich in de map met de bestands bibliotheek **FileLib**bevindt op een van deze stations.

Zoek een specifiek bestand aan de hand van de eerste vier tekens in de hash die is gevonden in de gegevens bibliotheek. In de map van de bestands bibliotheek zijn veel mappen, elk met een naam van vier tekens. Zoek de map die overeenkomt met de eerste vier tekens van de hash. Zodra u deze map hebt gevonden, bevat deze een of meer sets van drie bestanden. Deze bestanden delen dezelfde naam, maar de ene heeft de extensie INI, een heeft de extensie SIG en de ene heeft geen bestands extensie. Het oorspronkelijke bestand is de enige zonder extensie waarvan de naam gelijk is aan de hash van de gegevens bibliotheek.

Bijvoorbeeld: map **DEF9** bevat `DEF98765.INI` , `DEF98765.SIG` , en `DEF98765` . `DEF98765`is het origineel `MyFile.exe` . Het INI-bestand bevat een lijst met gebruikers of inhouds-Id's die hetzelfde bestand delen. Op de site wordt een bestand niet verwijderd, tenzij al deze inhoud ook wordt verwijderd.

### <a name="drive-spanning"></a>Station spanning

De inhouds bibliotheek kan worden verspreid over meerdere stations. U kiest deze stations bij het maken van het distributie punt. Configuration Manager kiest standaard automatisch de stations bij het spanningen van de inhouds bibliotheek.

Wanneer u de stations kiest, selecteert u een primair en secundair station. Op de site worden alle meta gegevens op het primaire station opgeslagen. Het omvat alleen de bestands bibliotheek op het secundaire station. De share naam van de map voor secundaire stations bevat de stationsletter. Als bijvoorbeeld D: en E: secundaire stations zijn voor de inhouds bibliotheek, zijn de share namen **SCCMContentLibD $** en **SCCMContentLibE $**.

Als u de **automatische** optie kiest, Configuration Manager selecteert u het station met de meest beschik bare vrije ruimte als primaire schijf. Alle meta gegevens op dit station worden opgeslagen. De site omvat alleen de bestands bibliotheek over secundaire stations.

U geeft een hoeveelheid reserve ruimte op tijdens de configuratie. Configuration Manager probeert een secundaire schijf te gebruiken zodra de beste beschik bare schijf alleen de hoeveelheid gereserveerde ruimte op de reserve heeft. Telkens wanneer een nieuw station wordt geselecteerd voor gebruik, wordt het station met de meeste beschik bare vrije ruimte geselecteerd.

U kunt niet opgeven dat een distributie punt alle stations moet gebruiken behalve voor een specifieke set. U kunt dit gedrag voor komen door een leeg bestand te maken in de hoofdmap van het station met de naam `NO_SMS_ON_DRIVE.SMS` . Plaats dit bestand voordat Configuration Manager het station selecteert voor gebruik. Als Configuration Manager dit bestand in de hoofdmap van het station detecteert, wordt het station niet gebruikt voor de inhouds bibliotheek.


## <a name="troubleshooting"></a>Problemen oplossen

De volgende tips kunnen u helpen bij het oplossen van problemen met de inhouds bibliotheek:  

- Bekijk de logboeken op de site server (**distmgr. log** en **PkgXferMgr. log**) en het distributie punt (**smsdpprov. log**) voor eventuele verwijzingen naar de fouten.  

- Gebruik het hulp programma [inhouds bibliotheek Verkenner](../../support/content-library-explorer.md) .  

- Controleren op bestands vergrendelingen door andere processen, zoals antivirus software. Sluit de inhouds bibliotheek op alle stations van automatische antivirus scans en de tijdelijke faserings Directory **SMS_DP $**, op elk station.  

- Als u wilt zien of er sprake is van hash-verschillen, valideert u het pakket vanuit de Configuration Manager-console.  

- Als laatste optie moet u de inhoud opnieuw distribueren. Met deze actie worden de meeste problemen opgelost.  

Zie informatie [over de distributie van inhoud en problemen oplossen in Configuration Manager](https://support.microsoft.com/help/4482728/understand-troubleshoot-content-distribution-in-configuration-manager)voor meer gedetailleerde informatie.
