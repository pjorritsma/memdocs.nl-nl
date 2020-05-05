---
title: CMPivot voor realtime gegevens
titleSuffix: Configuration Manager
description: Meer informatie over hoe u CMPivot in Configuration Manager kunt gebruiken om clients in realtime te doorzoeken.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dcd441c7f35748f42adc8824c68ec703291a13e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719139"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot voor realtime gegevens in Configuration Manager

<!--1358456-->

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager heeft altijd een grote centrale opslag van apparaatgegevens verschaft, die klanten gebruiken voor rapportage doeleinden. De site verzamelt deze gegevens doorgaans wekelijks. Vanaf versie 1806 is CMPivot een nieuw hulp programma in de console dat nu toegang biedt tot de real-time status van apparaten in uw omgeving. Er wordt onmiddellijk een query uitgevoerd op alle apparaten die momenteel zijn verbonden in de doel verzameling en de resultaten worden geretourneerd. Filter en groepeer vervolgens deze gegevens in het hulp programma. Door real-time gegevens op te geven van online-clients, kunt u sneller zakelijke vragen beantwoorden, problemen oplossen en reageren op beveiligings incidenten.

Een van de vereisten is bijvoorbeeld het bijwerken van het systeem-BIOS bij het [beperken van beveiligings problemen van speculatieve uitvoeringen](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974). U kunt CMPivot gebruiken om snel gegevens over het systeem-BIOS op te vragen en clients te zoeken die niet voldoen aan het beleid.

 > [!IMPORTANT]  
 > - Bepaalde beveiligings software blokkeert mogelijk scripts die worden uitgevoerd vanaf c:\windows\ccm\scriptstore. Dit kan leiden tot een geslaagde uitvoering van CMPivot-query's. Bepaalde beveiligings software kan ook controle gebeurtenissen of waarschuwingen genereren bij het uitvoeren van CMPivot Power shell.
 > - Bepaalde anti-malware-software kan per ongeluk gebeurtenissen activeren op basis van de Configuration Manager scripts uitvoeren of CMPivot-functies. Het is raadzaam om%windir%\CCM\ScriptStore uit te sluiten, zodat de anti-malware-software deze functies zonder interferentie kan uitvoeren.


## <a name="prerequisites"></a>Vereisten

De volgende onderdelen zijn vereist voor het gebruik van CMPivot:

- Voer een upgrade uit voor de doel apparaten naar de nieuwste versie van de Configuration Manager-client.  

- Voor doel-clients is mini maal Power shell-versie 4 vereist.

- Voor het verzamelen van gegevens voor de volgende entiteiten vereist de doel-clients Power shell-versie 5,0:  
  - Beheerders
  - Verbinding
  - IP
  - SMBConfig


- Machtigingen voor CMPivot:
  - **Lees** machtiging voor het object **SMS-scripts**
  - De machtiging **scripts uitvoeren** voor de **verzameling**
    - Vanaf versie 1906 kunt u ook **Run CMPivot** gebruiken voor de **verzameling**.
  - **Lees** machtiging voor **inventaris rapporten**
  - Het standaard bereik.

>[!NOTE]
> **Run scripts** is een superset van de machtiging **Run CMPivot** .
 
## <a name="limitations"></a>Beperkingen

- Verbind de Configuration Manager-console in een-hiërarchie met een *primaire site* om CMPivot uit te voeren. De actie **CMPivot starten** wordt niet weer gegeven in de-console wanneer deze is verbonden met een centrale beheer site (CAS).
  - Vanaf Configuration Manager versie 1902 kunt u CMPivot uitvoeren vanuit een certificerings instantie. In sommige omgevingen zijn extra machtigingen nodig. Zie [CMPivot vanaf versie 1902](#bkmk_cmpivot1902)voor meer informatie.

- CMPivot retourneert alleen gegevens voor clients die zijn verbonden met de huidige site.  

- Als een verzameling apparaten van een andere site bevat, zijn de CMPivot-resultaten alleen van apparaten op de huidige site.  

- U kunt geen Entiteits eigenschappen, kolommen voor resultaten of acties op apparaten aanpassen.  

- Er kan slechts één exemplaar van CMPivot tegelijkertijd worden uitgevoerd op een computer waarop de Configuration Manager-console wordt uitgevoerd.  

- In versie 1806 werkt de query voor de entiteit **Administrators** alleen als de groep ' Administrators ' is. Het werkt niet als de groeps naam is gelokaliseerd. Bijvoorbeeld ' administrateurs ' in het Frans.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>CMPivot starten

1. Maak in de Configuration Manager-console verbinding met de primaire site. Ga naar de werk ruimte **activa en naleving** en selecteer het knoop punt **device Collections** . Selecteer een doel verzameling en klik in het lint op **CMPivot starten** om het hulp programma te starten.  

    > [!Tip]  
    > Als u deze optie niet ziet, controleert u de volgende configuraties:  
    > 
    > - Bevestig met een site beheerder dat uw account de vereiste machtigingen heeft. Zie [vereisten](#prerequisites)voor meer informatie.  
    > 
    > - Verbind de console met een *primaire site*.  

2. De interface biedt meer informatie over het gebruik van het hulp programma.  

     - Voer de query reeksen boven hand matig in of klik op de koppelingen in de online documentatie.  

     - Klik op een van de **entiteiten** om deze toe te voegen aan de query reeks.  

     - De koppelingen voor **tabel operators**, **aggregatie functies**en **scalaire functies** openen taal referentie documentatie in de webbrowser. CMPivot maakt gebruik van de [Kusto query language (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

3. Houd het venster CMPivot geopend om de resultaten van clients te bekijken. Wanneer u het venster CMPivot sluit, wordt de sessie voltooid.  

    > [!Note]  
    > Als de query is verzonden, verzenden clients nog steeds een antwoord op een status bericht naar de server.  



## <a name="how-to-use-cmpivot"></a>CMPivot gebruiken

![CMPivot-venster voorbeeld](media/1358456-cmpivot-sample.png)

Het venster CMPivot bevat de volgende elementen:  

1. De verzameling met CMPivot momenteel bevindt zich in de titel balk bovenin en de status balk onder aan het venster. Bijvoorbeeld ' PM_Team_Machines ' in de bovenstaande scherm afbeelding.  

2. In het deel venster aan de linkerkant worden de **entiteiten** vermeld die beschikbaar zijn op clients. Sommige entiteiten zijn afhankelijk van WMI, terwijl andere Power shell gebruiken voor het ophalen van gegevens van clients.   

    - Klik met de rechter muisknop op een entiteit voor de volgende acties:  

       - **Invoegen**: Voeg de entiteit toe aan de query op de huidige cursor positie. De query wordt niet automatisch uitgevoerd. Deze actie is de standaard waarde wanneer u dubbelklikt op een entiteit. Gebruik deze actie bij het maken van een query.  

       - **Query alle**: Voer een query uit voor deze entiteit, inclusief alle eigenschappen. Gebruik deze actie om snel een query uit te zoeken voor één entiteit.  

       - **Query op apparaat**: Voer een query uit voor deze entiteit en groepeer de resultaten. Bijvoorbeeld: `Disk | summarize dcount( Device ) by Name`  

    - Vouw een entiteit uit om specifieke eigenschappen weer te geven die beschikbaar zijn voor elke entiteit. Dubbel klik op een eigenschap om deze toe te voegen aan de query op de huidige cursor positie.  

3. Het tabblad **Start** bevat algemene informatie over CMPivot, waaronder koppelingen naar voorbeeld query's en ondersteunende documentatie.  

4. Op het tabblad **query** worden het query deel venster, het deel venster met resultaten en de status balk weer gegeven. Het tabblad Query is geselecteerd in het bovenstaande voor beeld van de scherm afbeelding.  

5. In het query deel venster maakt of typt u een query die u wilt uitvoeren op clients in de verzameling.  

    - CMPivot maakt gebruik van een subset van de [Kusto query language (KQL)](https://docs.microsoft.com/azure/kusto/query/).  

    - Inhoud knippen, kopiëren of plakken in het query venster.  
    <!-- markdownlint-disable MD038 -->
    - Dit deel venster maakt standaard gebruik van IntelliSense. Als u bijvoorbeeld begint te typen `D`, worden alle entiteiten voorgesteld die met die letter beginnen. Selecteer een optie en druk op TAB om deze in te voegen. Typ een sluis teken en een spatie `| `en vervolgens worden alle tabel operators voorgesteld door IntelliSense. Voeg `summarize` een spatie in en typ een ruimte. IntelliSense stelt alle aggregatie functies voor. Klik op het tabblad **Start** in CMPivot voor meer informatie over deze opera tors en functies.  

    - Het query deel venster bevat ook de volgende opties:  

        - Voer de query uit.  

        - Verplaats achterwaartse en doorstuur servers in de geschiedenis lijst met query's.  

        - Maak een directe lidmaatschaps verzameling.  

        - De query resultaten exporteren naar CSV of het klem bord.  

6. In het deel venster met resultaten worden de gegevens weer gegeven die door actieve clients voor de query worden geretourneerd.  

   - De beschik bare kolommen variëren op basis van de entiteit en de query.  

   - Klik op de naam van een kolom om de resultaten te sorteren op die eigenschap.  

   - Klik met de rechter muisknop op de naam van een kolom om de resultaten te groeperen op dezelfde gegevens in die kolom, of de resultaten te sorteren.  

   - Klik met de rechter muisknop op de naam van een apparaat om de volgende aanvullende acties op het apparaat uit te voeren:  

      - **Draaien naar**: een query uitvoeren op een andere entiteit op dit apparaat.  

      - **Script uitvoeren**: Hiermee start u de wizard script uitvoeren om een bestaand Power shell-script uit te voeren op dit apparaat. Zie [een script uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script)voor meer informatie.  

      - **Beheer op afstand**: start een Configuration Manager sessie voor beheer op afstand op dit apparaat. Zie [een Windows-client computer op afstand beheren](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)voor meer informatie.  

      - **Resource Explorer**: start Configuration Manager resource Verkenner voor dit apparaat. Zie [hardware-inventaris weer geven](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) of software- [inventaris weer geven](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)voor meer informatie.  

   - Klik met de rechter muisknop op een andere cel dan een apparaat om de volgende aanvullende acties uit te voeren:  

     - **Kopiëren**: Kopieer de tekst van de cel naar het klem bord.  

     - **Apparaten weer geven met**: een query voor apparaten met deze waarde voor deze eigenschap. Selecteer bijvoorbeeld in de resultaten van de `OS` query deze optie in een cel in de rij versie:`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Apparaten weer geven zonder**deze waarde voor deze eigenschap. Selecteer bijvoorbeeld in de resultaten van de `OS` query deze optie in een cel in de rij versie:`OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Bing it**: Start de standaard webbrowser naar https://www.bing.com met deze waarde als de query reeks.  

   - Klik op een tekst met Hyper links om de weer gave te draaien op die specifieke informatie.  

   - In het deel venster met resultaten worden niet meer dan 20.000 rijen weer gegeven. Pas de query aan om de gegevens verder te filteren of CMPivot opnieuw op te starten in een kleinere verzameling.  

7. Op de status balk wordt de volgende informatie weer gegeven (van links naar rechts):  

   - De status van de huidige query naar de doel verzameling. Deze status omvat:  
     - Het aantal actieve clients dat de query heeft voltooid (3)  
     - Het aantal totale clients (5)  
     - Het aantal offline clients (2)  
     - Clients waarvoor de fout is geretourneerd (0)  

       Bijvoorbeeld: `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - De ID van de client bewerking. Bijvoorbeeld: `id(16780221)`  

   - De huidige verzameling. Bijvoorbeeld: `PM_Team_Machines`  

   - Het totale aantal rijen in het resultaten venster. Bijvoorbeeld: `1 objects`  



## <a name="example-scenarios"></a>Voorbeeldscenario 's

In de volgende secties vindt u voor beelden van hoe u CMPivot in uw omgeving kunt gebruiken:


### <a name="example-1-stop-a-running-service"></a>Voor beeld 1: een actieve service stoppen

Uw beveiligings beheerder vraagt u de computer browser-service zo snel mogelijk te stoppen en uit te scha kelen op alle apparaten in de boekhoud afdeling. U begint CMPivot op een verzameling voor alle apparaten in de groep Accounting en selecteert **alle query's** in de **service** -entiteit. 

`Service`

Wanneer de resultaten worden weer gegeven, klikt u met de rechter muisknop op de kolom **naam** en selecteert u **groeperen op**. 

`Service | summarize dcount( Device ) by Name`

In de rij voor de **browser** -service klikt u op het nummer met de Hyper link in de kolom **dcount_** . 

`Service | where (Name == 'Browser') | summarize count() by Device`

U kunt alle apparaten tegelijk selecteren, met de rechter muisknop op de selectie klikken en **script uitvoeren**kiezen. Met deze actie wordt de wizard script uitvoeren gestart, van waaruit u een bestaand script uitvoert dat u hebt om een service te stoppen en uit te scha kelen. Met CMPivot kunt u snel reageren op het beveiligings incident voor alle actieve computers en de resultaten weer geven in de wizard script uitvoeren. Vervolgens kunt u een configuratie basislijn maken om andere computers in de verzameling te herstellen, omdat deze in de toekomst actief worden. 

![CMPivot-voor beeld voor de browser service en de script actie uitvoeren](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Voor beeld 2: problemen met toepassingen proactief oplossen  

Als u proactief met operationeel onderhoud wilt maken, kunt u één keer per week CMPivot uitvoeren op een verzameling van servers die u beheert en selecteert u **query all** op de entiteit **AppCrash** . Klik met de rechter muisknop op de kolom **filename** en selecteer **Oplopend sorteren**. Eén apparaat retourneert zeven resultaten voor sqlsqm. exe met een tijds tempel van ongeveer 03:00 elke dag. Selecteer de bestands naam in een van de rijen, klik er met de rechter muisknop op en selecteer **Bing it**. Door de zoek resultaten in de webbrowser bladeren, vindt u een micro soft-ondersteunings artikel voor dit probleem met meer informatie en oplossingen. 


### <a name="example-3-bios-version"></a>Voor beeld 3: BIOS-versie

Een van de vereisten is het bijwerken van het systeem-BIOS om [beveiligings problemen met speculatieve uitvoeringen](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)op te lossen. U begint met een query voor de **BIOS** -entiteit. Vervolgens **groepeert u op** de eigenschap **Version** . Klik vervolgens met de rechter muisknop op een specifieke waarde, zoals "LENOVO-1140", en selecteer **apparaten weer geven met**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Voor beeld 4: beschik bare schijf ruimte

U moet tijdelijk een groot bestand opslaan op een netwerk Bestands server, maar niet zeker dat er voldoende capaciteit is. Start CMPivot op een verzameling bestands servers en zoek de entiteit **schijf** op. Wijzig de query voor CMPivot om snel een lijst met actieve servers met realtime-opslag gegevens te retour neren:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-starting-in-version-1810"></a><a name="bkmk_cmpivot"></a>CMPivot vanaf versie 1810
<!--1359068, 3607759-->

CMPivot bevat de volgende verbeteringen vanaf Configuration Manager versie 1810:

- [CMPivot-hulp programma en prestaties](#bkmk_cmpivot-perf)
- [Scalaire functies](#bkmk_cmpivot-functions)  
- [Visualisaties weer geven](#bkmk_cmpivot-charts)  
- [Hardware-inventaris](#bkmk_cmpivot-hinv)  
- [Scalaire operators](#bkmk_cmpivot-operators)  
- [Query samenvatting](#bkmk_cmpivot-summary)  
- [Controle status berichten](#cmpivot-audit-status-messages)

### <a name="cmpivot-utility-and-performance"></a><a name="bkmk_cmpivot-perf"></a>CMPivot-hulp programma en prestaties

- CMPivot retourneert Maxi maal 100.000 cellen in plaats van 20.000 rijen.
  - Als de entiteit 5 eigenschappen heeft, wat betekent 5 kolommen, worden Maxi maal 20.000 rijen weer gegeven.
  - Voor een entiteit met tien eigenschappen worden Maxi maal 10.000 rijen weer gegeven.
  - De totale hoeveelheid weer gegeven gegevens is kleiner dan of gelijk aan 100.000 cellen.
- Op het tabblad Query Samenvatting selecteert u het aantal mislukte of offline apparaten en selecteert u vervolgens de optie voor het **maken**van de verzameling. Met deze optie kunt u gemakkelijk deze apparaten richten met een herstel implementatie.
- Sla **favoriete** query's op door op het mappictogram te klikken.
   ![Voor beeld van het opslaan van een favoriete query in CMPivot](media/cmpivot-favorite.png)

- Clients die zijn bijgewerkt naar de 1810-versie retour neren een uitvoer van minder dan 80 KB aan de site via een snel communicatie kanaal.
  - Deze wijziging verhoogt de prestaties van het weer geven van scripts of uitvoer van query's.
  - Als het script of de query-uitvoer groter is dan 80 KB, verzendt de client de gegevens via een status bericht.
  - Als de client niet is bijgewerkt naar de 1810-client versie, blijven status berichten gebruiken.

- Mogelijk wordt de volgende fout weer geven wanneer u CMPivot start: **u kunt CMPivot nu niet gebruiken vanwege een incompatibele script versie. Dit probleem kan worden veroorzaakt doordat de hiërarchie een upgrade uitvoert voor een site. Wacht tot de upgrade is voltooid en probeer het vervolgens opnieuw.**

  - Als dit bericht wordt weer gegeven, kan dit het volgende betekenen:
    - Het beveiligings bereik is niet juist ingesteld.
    - Er zijn problemen met de upgrade in het proces.
    - Het onderliggende CMPivot-script is incompatibel.


### <a name="scalar-functions"></a><a name="bkmk_cmpivot-functions"></a>Scalaire functies
CMPivot ondersteunt de volgende scalaire functies:
- **geleden ()**: de opgegeven time span aftrekken van de huidige UTC-klok tijd  
- **datetime_diff ()**: berekent het kalender verschil tussen twee datum/tijd-waarden  
- **Now ()**: retourneert de huidige UTC-klok tijd  
- **bin ()**: rondt waarden af naar een geheel getal veelvoud van een bepaalde opslaglocatie grootte  

> [!Note]  
> Het gegevens type datetime vertegenwoordigt een onmiddellijke tijd, meestal uitgedrukt als een datum en tijd van de dag. Tijd waarden worden gemeten in eenheden van 1 seconde. Een datum/tijd-waarde is altijd in de UTC-tijd zone. Altijd datum en tijd letterlijke waarden in ISO 8601-indeling, bijvoorbeeld`yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Voorbeelden
- `datetime(2015-12-31 23:59:59.9)`: Een bepaalde letterlijke datum tijd   
- `now()`: De huidige tijd  
- `ago(1d)`: De huidige tijd min één dag  


### <a name="rendering-visualizations"></a><a name="bkmk_cmpivot-charts"></a>Visualisaties weer geven

CMPivot bevat nu Basic-ondersteuning voor de KQL- [render-operator](https://docs.microsoft.com/azure/kusto/query/renderoperator). Deze ondersteuning omvat de volgende typen:  
- **Barchart**: de eerste kolom is x-as en kan tekst, DateTime of numeric zijn. De tweede kolommen moeten numeriek zijn en worden weer gegeven als een horizontale streep.  
- **columnchart**: like Barchart, met verticale stroken in plaats van horizontale strepen.  
- **piechart**: de eerste kolom is een kleurenas, een tweede kolom is een numerieke waarde.  
- **timechart**: lijn diagram. De eerste kolom is x-as en moet datetime zijn. De tweede kolom is een y-as.  

#### <a name="example-bar-chart"></a>Voor beeld: staaf diagram
Met de volgende query worden de meest recent gebruikte toepassingen als staaf diagram weer gegeven:

``` Kusto
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```

![Voor beeld van een visualisatie van een CMPivot-staaf diagram](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Voor beeld: tijd diagram
Als u tijd grafieken wilt weer geven, gebruikt u de operator new **bin ()** om gebeurtenissen in tijd te groeperen. De volgende query geeft aan wanneer apparaten zijn gestart in de afgelopen zeven dagen:

``` Kusto
OperatingSystem
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```

![Voor beeld van een CMPivot tijd diagram visualisatie](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Voor beeld: cirkel diagram
Met de volgende query worden alle versies van het besturings systeem in een cirkel diagram weer gegeven:

``` Kusto
OperatingSystem
| summarize count() by Caption
| render piechart
```

![Voor beeld van een visualisatie van een CMPivot-cirkel diagram](media/1359068-cmpivot-piechart.png)


### <a name="hardware-inventory"></a><a name="bkmk_cmpivot-hinv"></a>Hardware-inventarisatie
Gebruik CMPivot voor het opvragen van een hardware-inventaris klasse. Deze klassen bevatten alle aangepaste uitbrei dingen die u hebt gemaakt voor de hardware-inventarisatie. CMPivot keert onmiddellijk in de cache resultaten van de laatste scan voor hardware-inventarisatie die is opgeslagen in de site database. Tegelijkertijd worden de resultaten bijgewerkt, indien nodig met Live gegevens van alle online clients.

De kleur verzadiging van de gegevens in de resultaten tabel of-grafiek geeft aan of de gegevens in de cache worden opgeslagen. Donker blauw is bijvoorbeeld real-time gegevens van een online-client. Licht blauw is gegevens in de cache.

#### <a name="example"></a>Voorbeeld

``` Kusto
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```

![Voor beeld van een CMPivot-inventaris query met de visualisatie van een kolom diagram](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Beperkingen
- De volgende hardware-inventaris entiteiten worden niet ondersteund:  
    - Matrix eigenschappen, bijvoorbeeld IP-adres  
    - Real32/Real64 <!--example?-->  
    - Eigenschappen van Inge sloten object <!--example?-->  
- Namen van voorraad entiteiten moeten beginnen met een teken
- U kunt de ingebouwde entiteiten niet overschrijven door een inventaris entiteit met dezelfde naam te maken  


### <a name="scalar-operators"></a><a name="bkmk_cmpivot-operators"></a>Scalaire Opera tors
CMPivot bevat de volgende scalaire Opera tors:  

> [!Note]  
> - LHS: teken reeks links van de operator  
> - RHS: teken reeks rechts van de operator  


|Operator|Beschrijving|Voor beeld (resulteert in ' waar ')|
|--------|-----------|---------------------|
|==|Is gelijk aan|`"aBc" == "aBc"`|
|!=|Niet gelijk aan|`"abc" != "ABC"`|
|zo|LHS bevat een overeenkomst voor RHS|`"FabriKam" like "%Brik%"`|
|! like|LHS bevat geen overeenkomst voor RHS|`"Fabrikam" !like "%xyz%"`|
|bevat|RHS treedt op als een subreeks van LHS|`"FabriKam" contains "BRik"`|
|! bevat|RHS vindt niet plaats in LHS|`"Fabrikam" !contains "xyz"`|
|startsWith|RHS is een initiële subreeks van LHS|`"Fabrikam" startswith "fab"`|
|! startsWith|RHS is geen initiële subreeks van LHS|`"Fabrikam" !startswith "kam"`|
|endswith|RHS is een subreeks van LHS|`"Fabrikam" endswith "Kam"`|
|! endswith|RHS is geen afsluitende subreeks van LHS|`"Fabrikam" !endswith "brik"`|


### <a name="query-summary"></a><a name="bkmk_cmpivot-summary"></a>Query samenvatting

Selecteer het tabblad **query samenvatting** onder aan het venster CMPivot. Deze status helpt u bij het identificeren van clients die offline zijn, of het oplossen van fouten die zich kunnen voordoen. Selecteer een waarde in de kolom aantal om een lijst met specifieke apparaten met die status te openen. 

Selecteer bijvoorbeeld het aantal apparaten met de status mislukt. Zie het specifieke fout bericht en exporteer een lijst van deze apparaten. Als de fout is dat een specifieke cmdlet niet wordt herkend, maakt u een verzameling uit de lijst met geëxporteerde apparaten om een Windows Power shell-update te implementeren.  

### <a name="cmpivot-audit-status-messages"></a>Controle status berichten CMPivot

Vanaf versie 1810, wanneer u CMPivot uitvoert, wordt een controle status bericht gemaakt met **MessageID 40805**. U kunt de status berichten weer geven door naar **bewaking** > **systeem status** > **status bericht query's**te gaan. U kunt **alle controle status berichten voor een specifieke gebruiker**uitvoeren, **alle controle status berichten voor een specifieke site**of uw eigen status bericht query maken.

De volgende indeling wordt gebruikt voor het bericht:

MessageId 40805: gebruiker &lt;gebruikers naam> script &lt;script-GUID> met hash &lt;-script-hash-> &lt;in verzamelings verzameling-id> wordt uitgevoerd.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 is de script-GUID voor CMPivot.
- De script-hash kan worden weer gegeven in het logboek bestand van de client.
- U kunt ook de hash zien die is opgeslagen in het script archief van de client. De bestands naam op de client &lt;is script-GUID&lt;>_ script-hash->.
    - Voor beeld van bestands naam: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123. PS
   

![Voor beeld van CMPivot-controle status bericht](media/cmpivot-audit-status-message.png)

## <a name="cmpivot-starting-in-version-1902"></a><a name="bkmk_cmpivot1902"></a>CMPivot vanaf versie 1902
<!--3610960-->
Vanaf Configuration Manager versie 1902 kunt u CMPivot uitvoeren vanaf de centrale beheer site (CAS) in een-hiërarchie. De primaire site verwerkt nog steeds de communicatie met de client. Wanneer CMPivot vanaf de centrale beheer site wordt uitgevoerd, communiceert deze met de primaire site via het kanaal voor het abonnement op hoge snelheid van berichten. Deze communicatie vertrouwt niet op de standaard SQL-replicatie tussen sites.

Voor het uitvoeren van CMPivot op de CAS zijn extra machtigingen vereist wanneer SQL of de provider zich niet op dezelfde computer bevindt, of in het geval van de configuratie voor SQL always on. Met deze externe configuraties hebt u een ' Double hop scenario ' voor CMPivot.

U kunt beperkte delegering definiëren om CMPivot te laten werken aan de certificerings instanties in een dergelijk scenario met ' dubbele hop '. Lees het artikel [Kerberos-beperkte overdracht](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview) voor meer informatie over de beveiligings implicaties van deze configuratie. Kerberos moet alle hops tussen de computers door lopen.<!--5746133--> Als u meer dan één externe configuratie hebt, zoals SQL of SMS-provider die is gekoppeld aan de CAS of niet of meerdere vertrouwde forests, hebt u mogelijk een combi natie van machtigings instellingen nodig. Hieronder vindt u de stappen die u mogelijk moet uitvoeren:

### <a name="cas-has-a-remote-sql-server"></a>CA'S heeft een externe SQL-Server

1. Ga naar de SQL-Server van elke primaire site.
   1. Voeg de externe SQL Server-CA'S en de CAS-site server toe aan de groep [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) .
   ![Configmgr_DviewAccess groep op de SQL-Server van een primaire site](media/cmpivot-dviewaccess-group.png)
1. Ga naar Active Directory gebruikers en computers.
   1. Voor elke primaire site server klikt u met de rechter muisknop en selecteert u **Eigenschappen**.
      1. Kies op het tabblad delegering de derde optie, **deze computer mag alleen delegeren aan de opgegeven services**. 
      1. Kies **alleen Kerberos gebruiken**.
      1. Voeg de SQL Server-service van CAS toe met de poort en het exemplaar.
      1. Zorg ervoor dat deze wijzigingen worden uitgelijnd met het beveiligings beleid van uw bedrijf.
   1. Klik met de rechter muisknop op de CAS-site en selecteer **Eigenschappen**.
      1. Kies op het tabblad delegering de derde optie, **deze computer mag alleen delegeren aan de opgegeven services**. 
      1. Kies **alleen Kerberos gebruiken**.
      1. Voeg de SQL Server-service van elke primaire site toe met de poort en het exemplaar.
      1. Zorg ervoor dat deze wijzigingen worden uitgelijnd met het beveiligings beleid van uw bedrijf.

   ![Voor beeld van CMPivot AD-overdracht voor dubbele hops](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>CA'S heeft een externe provider

1. Ga naar de SQL-Server van elke primaire site.
   1. Voeg het computer account van de CAS-provider en de CAS-site server toe aan de groep [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) .
1. Ga naar Active Directory gebruikers en computers.
   1. Selecteer de computer van de CAS-provider, klik met de rechter muisknop en selecteer **Eigenschappen**.
      1. Kies op het tabblad delegering de derde optie, **deze computer mag alleen delegeren aan de opgegeven services**. 
      1. Kies **alleen Kerberos gebruiken**.
      1. Voeg de SQL Server-service van elke primaire site toe met de poort en het exemplaar.
      1. Zorg ervoor dat deze wijzigingen worden uitgelijnd met het beveiligings beleid van uw bedrijf.
   1. Selecteer de CAS-site server, klik met de rechter muisknop en selecteer **Eigenschappen**.
      1. Kies op het tabblad delegering de derde optie, **deze computer mag alleen delegeren aan de opgegeven services**. 
      1. Kies **alleen Kerberos gebruiken**.
      1. Voeg de SQL Server-service van elke primaire site toe met de poort en het exemplaar.
      1. Zorg ervoor dat deze wijzigingen worden uitgelijnd met het beveiligings beleid van uw bedrijf.
1. Start de CAS-computer voor externe provider opnieuw op.

### <a name="sql-always-on"></a>SQL always on

1. Ga naar de SQL-Server van elke primaire site.
   1. Voeg de CAS-site server toe aan de groep [Configmgr_DviewAccess](../../plan-design/hierarchy/accounts.md#configmgr_dviewaccess) .
1. Ga naar Active Directory gebruikers en computers.
   1. Voor elke primaire site server klikt u met de rechter muisknop en selecteert u **Eigenschappen**.
      1. Kies op het tabblad delegering de derde optie, **deze computer mag alleen delegeren aan de opgegeven services**. 
      1. Kies **alleen Kerberos gebruiken**.
      1. Voeg de SQL Server-service accounts van de CAS toe voor de SQL-knoop punten met de poort en het exemplaar.
      1. Zorg ervoor dat deze wijzigingen worden uitgelijnd met het beveiligings beleid van uw bedrijf.
   1. Selecteer de CAS-site server, klik met de rechter muisknop en selecteer **Eigenschappen**.
      1. Kies op het tabblad delegering de derde optie, **deze computer mag alleen delegeren aan de opgegeven services**. 
      1. Kies **alleen Kerberos gebruiken**.
      1. Voeg de SQL Server-service van elke primaire site toe met de poort en het exemplaar.
      1. Zorg ervoor dat deze wijzigingen worden uitgelijnd met het beveiligings beleid van uw bedrijf.
1. Zorg ervoor dat de [SPN wordt gepubliceerd](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) voor de naam van de SQL-LISTENER van CAS en elke naam van de primaire SQL-listener.
1. Start de primaire SQL-servers opnieuw op.
1. Start de CAS-site server en de CAS SQL-servers opnieuw op.

## <a name="cmpivot-starting-in-version-1906"></a><a name="bkmk_cmpivot1906"></a>CMPivot vanaf versie 1906

Vanaf versie 1906 zijn de volgende items toegevoegd aan CMPivot:

- [Samen voegingen, extra Opera tors en aggregators](#bkmk_cmpivot_joins)
- [De CMPivot-machtigingen zijn toegevoegd aan de rol beveiligings beheerder](#bkmk_cmpivot_secadmin1906)
- [Zelfstandige CMPivot](#bkmk_standalone)

### <a name="add-joins-additional-operators-and-aggregators-in-cmpivot"></a><a name="bkmk_cmpivot_joins"></a>Voeg koppelingen, extra Opera tors en aggregators toe in CMPivot
<!--4054074-->
U hebt nu extra reken kundige Opera Tors, aggregators en de mogelijkheid om toevoeg query's toe te voegen, zoals het gebruik van het REGI ster en het bestand samen. De volgende items zijn toegevoegd:

#### <a name="table-operators"></a>Tabel operators

|Tabel operators| Beschrijving|
|-----|-----|
| [Jointypen](https://docs.microsoft.com/azure/kusto/query/joinoperator)| De rijen van twee tabellen samen voegen om een nieuwe tabel te vormen door overeenkomende rij voor hetzelfde apparaat te zoeken|
|waardoor|Hiermee worden resultaten weer gegeven als grafische uitvoer|

De render-operator bestaat al in CMPivot. Er is ondersteuning voor meerdere reeksen en de instructie **with** toegevoegd. Zie voor meer informatie de sectie [voor beelden](#bkmk_cmpivot_examples1906) en het artikel [deelname operator](https://docs.microsoft.com/azure/kusto/query/joinoperator) Kusto.

#### <a name="limitations-for-joins"></a>Beperkingen voor samen voegingen

1. De samenvoegings kolom wordt altijd impliciet uitgevoerd op het veld **apparaat** .
1. U kunt Maxi maal 5 koppelingen per query gebruiken.
1. U kunt Maxi maal 64 gecombineerde kolommen gebruiken.

#### <a name="scalar-operators"></a>Scalaire operators

|Operator| Beschrijving|Voorbeeld|
|-----|-----|-----|
| + | Toevoegen| `2 + 1, now() + 1d`|
| - |  Aftrekken| `2 - 1, now() - 1d`|
| * | Vermenigvuldigen| `2 * 2`|
| / | Delen | `2 / 1`|
| % | Modulo | `2 % 1`

#### <a name="aggregation-functions"></a>Aggregatiefuncties

|Functie| Beschrijving|
|-----|-----|
| percentiel ()| Retourneert een schatting voor het opgegeven dichtstbijzijnde-positie percentiel van de populatie die is gedefinieerd met expr|
| sumif() | Retourneert een som van de expr waarvoor het predicaat resulteert in waar|

#### <a name="scalar-functions"></a>Scalaire functies

|Functie| Beschrijving|
|-----|-----|
| case()| Evalueert een lijst met predikaten en retourneert de eerste resultaat expressie waarvan het predicaat is voldaan |
| IFF () | Evalueert het eerste argument en retourneert de waarde van de tweede of derde argumenten, afhankelijk van het feit of het predicaat is geëvalueerd als waar (seconde) of ONWAAR (derde)|
 | indexof() | Functie rapporteert de op nul gebaseerde index van het eerste exemplaar van een opgegeven teken reeks in de invoer teken reeks|
| strcat() | Voegt de argumenten tussen 1 en 64 |
| strlen()| Retourneert de lengte in tekens van de invoer teken reeks|
| substring() | Hiermee wordt een subtekenreeks geëxtraheerd van een bron teken reeks, beginnend bij een index naar het einde van de teken reeks |
| tostring() | Converteert invoer naar een teken reeks bewerking |

#### <a name="examples"></a><a name="bkmk_cmpivot_examples1906"></a>Vindt

- Apparaat, fabrikant, model en niet weer geven:

   ``` Kusto
   ComputerSystem
   | project Device, Manufacturer, Model
   | join (OperatingSystem | project Device, OSVersion=Caption)
   ```

- De grafiek van opstart tijden voor een apparaat weer geven:

   ``` Kusto
   SystemBootData
   | where Device == 'MyDevice'
   | project SystemStartTime, BootDuration, OSStart=EventLogStart, GPDuration, UpdateDuration
   | order by SystemStartTime desc
   | render barchart with (kind=stacked, title='Boot times for MyDevice', ytitle='Time (ms)')
   ```

   ![Gestapeld staaf diagram met opstart tijden voor een apparaat in MS](./media/4054074-render-using-with-statement.png)

### <a name="added-cmpivot-permissions-to-the-security-administrator-role"></a><a name="bkmk_cmpivot_secadmin1906"></a>De CMPivot-machtigingen zijn toegevoegd aan de rol beveiligings beheerder
<!--4683130-->

Vanaf versie 1906 zijn de volgende machtigingen toegevoegd aan de ingebouwde rol **beveiligings beheerder** van Configuration Manager:

 - SMS-script **lezen**
 - **CMPivot uitvoeren** op verzameling
 - **Lezen** op inventaris rapport

>[!NOTE]
> **Run scripts** is een superset van de machtiging **Run CMPivot** .
 

### <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a>Zelfstandige CMPivot
<!--3555890, 4619340, 4683130 -->

Vanaf versie 1906 kunt u CMPivot als zelfstandige app gebruiken. Zelfstandige CMPivot is alleen beschikbaar in het Engels. Voer CMPivot buiten de Configuration Manager-console uit om de real-time status van apparaten in uw omgeving weer te geven. Met deze wijziging kunt u CMPivot gebruiken op een apparaat zonder eerst de-console te installeren.

> [!Tip]  
> Deze functie werd voor het eerst in versie 1906 geïntroduceerd als een [voorlopige functie](pre-release-features.md). Vanaf versie 2002 is het niet langer een functie van de voorlopige versie.  

U kunt de kracht van CMPivot delen met andere personen, zoals helpdesk medewerkers of beveiligings beheerders, die de-console niet op hun computer hebben geïnstalleerd. Deze andere personen kunnen met behulp van CMPivot query's uitvoeren op Configuration Manager naast de andere hulp middelen die ze traditioneel gebruiken. Door deze uitgebreide beheer gegevens te delen, kunt u samen werken om zakelijke problemen met meerdere rollen proactief op te lossen.

#### <a name="install-cmpivot-standalone"></a>Zelfstandige installatie van CMPivot

1. Stel de machtigingen in die nodig zijn om CMPivot uit te voeren. Zie [vereisten](#prerequisites)voor meer informatie. U kunt ook de [rol beveiligings beheerder](#bkmk_cmpivot_secadmin1906) gebruiken als de machtigingen geschikt zijn voor de gebruiker.
2. Zoek het installatie programma van de CMPivot-app op `<site install path>\tools\CMPivot\CMPivot.msi`het volgende pad:. U kunt het vanuit dat pad uitvoeren of het naar een andere locatie kopiëren.
3. Wanneer u de zelfstandige CMPivot-app uitvoert, wordt u gevraagd verbinding te maken met een site. Geef de naam van de Fully Qualified Domain Name of computer op van de server voor Centraal beheer of de primaire site.
   - Telkens wanneer u CMPivot standalone opent, wordt u gevraagd verbinding te maken met een site server.
4. Blader naar de verzameling waarop u CMPivot wilt uitvoeren en voer de query uit.

   ![Blader naar de verzameling waarvoor u de query wilt uitvoeren](./media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> Met de rechter muisknop op acties, zoals **Run scripts**, **resource Explorer**en webzoekopdracht, zijn niet beschikbaar in de zelfstandige CMPivot. Het primaire gebruik van CMPivot-zelfstandige query's is onafhankelijk van de Configuration Manager-infra structuur. Ter ondersteuning van beveiligings beheerders biedt CMpivot standalone de mogelijkheid om verbinding te maken met micro soft Defender Security Center. <!--5605358-->

## <a name="cmpivot-starting-in-version-1910"></a><a name="bkmk_cmpivot1910"></a>CMPivot vanaf versie 1910
<!--5410930, 3197353-->
Vanaf versie 1910 werd CMPivot aanzienlijk geoptimaliseerd om het netwerk verkeer en de belasting van uw servers te verminderen. Daarnaast zijn er een aantal entiteiten en entiteits verbeteringen toegevoegd aan de hulp bij het oplossen van problemen en jacht. De volgende wijzigingen zijn geïntroduceerd voor CMPivot in versie 1910:

- [Optimalisaties voor de CMPivot-engine](#bkmk_optimization)
- Extra entiteiten en entiteits verbeteringen:
  - Windows-gebeurtenis Logboeken ([Wine vent](#bkmk_WinEvent))
  - Bestands inhoud ([FileContent](#bkmk_File))
  - Door processen geladen dll's ([ProcessModule](#bkmk_ProcessModule))
  - Azure Active Directory informatie ([AADStatus](#bkmk_AadStatus))
  - Endpoint Protection-status ([EPStatus](#bkmk_EPStatus))
- [Query-evaluatie van lokale apparaten met behulp van CMPivot standalone](#bkmk_local-eval)
- [Andere verbeteringen in CMPivot](#bkmk_Other)


### <a name="optimizations-to-the-cmpivot-engine"></a><a name="bkmk_optimization"></a>Optimalisaties voor de CMPivot-engine
<!--3197353-->
CMPivot is geoptimaliseerd in 1910 om het netwerk verkeer en de belasting van uw servers te verminderen. Veel query bewerkingen worden nu direct uitgevoerd op de client in plaats van op de servers. Deze wijziging betekent ook dat sommige CMPivot-bewerkingen minimale gegevens retour neren van de eerste query. Als u wilt inzoomen op de gegevens voor meer informatie, kan een nieuwe query worden uitgevoerd om de aanvullende gegevens van de client op te halen. Voorheen werd bijvoorbeeld een grote gegevensset naar de server geretourneerd toen u de query ' aantal ' overzichten ' had uitgevoerd.  Tijdens het retour neren van een grote gegevensset wordt direct inzoomen aangeboden, maar vaak is alleen het aantal samenvattingen nodig. In 1910 wanneer u ervoor kiest om in te zoomen op een specifieke client, wordt een andere verzameling van de gegevens uitgevoerd om de aanvullende gegevens die u hebt aangevraagd, te retour neren. Met deze wijziging worden de prestaties en schaal baarheid van query's op een groot aantal clients verbeterd. <!--3197353, 5458337-->

#### <a name="examples"></a>Voorbeelden

De CMPivot-optimalisaties verlagen het netwerk en de CPU-belasting van de server die nodig is om CMPivot-query's uit te voeren. Met deze optimalisaties kunnen we nu Maxi maal gigabytes aan client gegevens in realtime door lopen. De volgende query's illustreren deze optimalisaties:

- Zoek in alle gebeurtenis logboeken op alle clients in uw onderneming naar mislukte verificaties.

   ``` Kusto
   EventLog('Security')
   | where  EventID == 4673
   | summarize count() by Device
   | order by count_ desc
   ```

- Zoek naar een bestand op hash.

   ``` Kusto
   Device
   | join kind=leftouter ( File('%windir%\\system32\\*.exe')
   | where SHA256Hash == 'A92056D772260B39A876D01552496B2F8B4610A0B1E084952FE1176784E2CE77')
   | project Device, MalwareFound = iif( isnull(FileName), 'No', 'Yes')
   ```

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a>Wine vent (\<logname>, [\<time span>])

Deze entiteit wordt gebruikt voor het ophalen van gebeurtenissen uit gebeurtenis logboeken en logboek bestanden voor gebeurtenis tracering. De entiteit haalt gegevens op uit gebeurtenis logboeken die worden gegenereerd door de Windows-gebeurtenis logboek technologie. De entiteit haalt ook gebeurtenissen op in logboek bestanden die zijn gegenereerd door Event Tracing for Windows (ETW). Wine vent bekijkt de gebeurtenissen die standaard in de afgelopen 24 uur zijn opgetreden. De standaard instelling voor 24 uur kan echter worden overschreven door een time span op te nemen.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a>FileContent (\<bestands naam>)

FileContent wordt gebruikt om de inhoud van een tekst bestand op te halen.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a>ProcessModule (\<verwerkings>)  

Deze entiteit wordt gebruikt voor het inventariseren van de modules (dll's) die door een bepaald proces zijn geladen. ProcessModule is handig bij het zoeken naar malware die in legitieme processen wordt verborgen.  

``` Kusto
ProcessModule('powershell')
| summarize count() by ModuleName
| order by count_ desc
```

### <a name="aadstatus"></a><a name="bkmk_AadStatus"></a>AadStatus

Deze entiteit kan worden gebruikt om de huidige Azure Active Directory identiteits gegevens van een apparaat op te halen.

``` Kusto
AadStatus
| project Device, IsAADJoined=iif( isnull(DeviceId),'No','Yes')
| summarize DeviceCount=count() by IsAADJoined
| render piechart
```

### <a name="epstatus"></a><a name="bkmk_EPStatus"></a>EPStatus

EPStatus wordt gebruikt voor het ophalen van de status van de antimalware-software die op de computer is geïnstalleerd.

``` Kusto
EPStatus
| project Device, QuickScanAge=datetime_diff('day',now(),QuickScanEndTime)
| summarize DeviceCount=count() by QuickScanAge
| order by QuickScanAge
| render barchart
```

### <a name="local-device-query-evaluation-using-cmpivot-standalone"></a><a name="bkmk_local-eval"></a>Query-evaluatie van lokale apparaten met behulp van CMPivot standalone
<!--3197353-->
Wanneer u CMPivot gebruikt buiten de Configuration Manager-console, kunt u alleen een query uitvoeren op het lokale apparaat zonder dat de Configuration Manager-infra structuur nodig is. U kunt nu gebruikmaken van de CMPivot Azure Log Analytics-query's om snel WMI-gegevens op het lokale apparaat weer te geven. Hiermee wordt ook de validatie en verfijning van CMPivot-query's ingeschakeld voordat deze in een grotere omgeving worden uitgevoerd. Zelfstandige CMPivot is alleen beschikbaar in het Engels. Zie [install CMPivot zelfstandige](#install-cmpivot-standalone)voor meer informatie over het installeren van CMPivot standalone.

#### <a name="known-issues-for-local-device-query-evaluation"></a>Bekende problemen met de evaluatie van query's van lokale apparaten

 - Als u op **deze PC** een query uitvoert voor een WMI-entiteit waartoe u geen toegang hebt, zoals een VERGRENDELDE WMI-klasse, ziet u mogelijk een crash in CMPivot. Voer CMPivot uit met een account met verhoogde bevoegdheden voor het opvragen van deze entiteiten. <!--5753242-->
- Als u op **deze PC**niet-WMI-entiteiten opvraagt, ziet u een **Ongeldige naam ruimte** of een niet-eenduidige uitzonde ring.
- Voer CMPivot standalone uit vanuit de snelkoppeling in het menu Start, niet rechtstreeks vanuit het pad van het uitvoer bare bestand. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a>Andere verbeteringen

- U kunt reguliere expressie type query's uitvoeren met behulp `like` van de operator new. Bijvoorbeeld:<!--3056858-->
  
   ```kusto
   //Find BIOS manufacture that contains any word like Micro, such as Microsoft
   Bios
   | where Manufacturer like '%Micro%'
   ```

- We hebben de **CcmLog ()** en **Eventlog ()** -entiteiten bijgewerkt zodat ze alleen in de afgelopen 24 uur berichten kunnen bekijken. Dit gedrag kan worden overschreven door een optionele time span door te geven. De volgende query bekijkt bijvoorbeeld gebeurtenissen in het afgelopen uur:

   ```kusto
   CcmLog('Scripts',1h)
   ```

- De entiteit **File ()** is bijgewerkt met informatie over verborgen en systeem bestanden en bevat de MD5-hash. Hoewel een MD5-hash niet zo nauw keurig is als de SHA256-hash, is het doorgaans de gebruikelijke gerapporteerde hash in de meeste malware-bulletins.  

- U kunt opmerkingen toevoegen in query's.<!-- 5431463 --> Dit gedrag is handig bij het delen van query's. Bijvoorbeeld:

    ``` Kusto
    //Get the top ten devices sorted by user
    Device
    | top 10 by UserName
    ```

- CMPivot maakt automatisch verbinding met de laatste site.<!-- 5420395 --> Nadat u CMPivot hebt gestart, kunt u, indien nodig, verbinding maken met een nieuwe site.

- Selecteer in het menu **exporteren** de optie Nieuw om een **koppeling naar het klem bord te**maken.<!-- 5431577 --> Met deze actie wordt een koppeling naar het klem bord gekopieerd die u met anderen kunt delen. Bijvoorbeeld:

    `cmpivot:Ly8gU2FtcGxlIHF1ZXJ5DQpPcGVyYXRpbmdTeXN0ZW0NCnwgc3VtbWFyaXplIGNvdW50KCkgYnkgQ2FwdGlvbg0KfCBvcmRlciBieSBjb3VudF8gYXNjDQp8IHJlbmRlciBiYXJjaGFydA==`

    Met deze koppeling opent u CMPivot standalone met de volgende query:

    ``` Kusto
    // Sample query
    OperatingSystem
    | summarize count() by Caption
    | order by count_ asc
    | render barchart
    ```

    > [!TIP]
    > [Installeer CMPivot standalone](#install-cmpivot-standalone)om deze koppeling te laten werken.

- Als het apparaat is inge schreven in micro soft Defender Advanced Threat Protection (ATP), klikt u met de rechter muisknop op het apparaat om de **micro soft defender Security Center** Online-Portal te starten.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Bekende problemen voor CMPivot in versie 1910

- De banner voor het maximum aantal resultaten kan niet worden weer gegeven wanneer de limiet is bereikt. <!--5431427-->
  - Elke client is beperkt tot 128 KB aan gegevens per query.
  - Resultaten kunnen worden afgekapt als de resultaten van de query groter zijn dan 128 KB.
  
## <a name="cmpivot-starting-in-version-2002"></a><a name="bkmk_2002"></a>CMPivot vanaf versie 2002
<!--5870934-->
We hebben het eenvoudiger gemaakt om te navigeren in CMPivot-entiteiten. Vanaf Configuration Manager versie 2002 kunt u CMPivot-entiteiten zoeken. Er zijn ook nieuwe pictogrammen toegevoegd om de entiteiten en de object typen van de entiteit eenvoudig te onderscheiden.

![Zoeken in CMPivot-entiteiten](./media/5870934-search-cmpivot-entities.png)

 
## <a name="inside-cmpivot"></a>Binnen CMPivot

CMPivot verzendt query's naar clients met behulp van de Configuration Manager "Fast Channel". Dit communicatie kanaal van de server naar de client wordt ook gebruikt door andere functies, zoals client meldings acties, client status en Endpoint Protection. Clients retour neren resultaten via het vergelijk bare bericht systeem voor snelle status. Status berichten worden tijdelijk opgeslagen in de-data base. Zie het artikel over de [poorten](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-MP) voor meer informatie over de poorten die worden gebruikt voor client meldingen.

De query's en de resultaten zijn allemaal alleen tekst. De entiteiten **InstallSoftware** en **process** retour neren een aantal van de grootste resultaten sets. Tijdens prestatie tests is de bestands grootte van het grootste bericht van de ene client voor deze query's kleiner dan **1 KB**. Deze eenmalige query kan worden geschaald naar een grote omgeving met 50.000 actieve clients en genereert minder dan 50 MB aan gegevens in het netwerk. Alle items op de welkomst pagina die onderstreept zijn, retour neren minder dan 1 KB aan gegevens per client.

![Voor beeld van CMPivot onderstreepte entiteiten](media/cmpivot-underlined-entities.png)

Met ingang van Configuration Manager 1810 kan CMPivot query's uitvoeren op hardware-inventaris gegevens, met inbegrip van uitgebreide hardware-inventaris klassen. Deze nieuwe entiteiten (entiteiten die niet op de welkomst pagina zijn onderstreept) kunnen veel grotere gegevens sets retour neren, afhankelijk van de hoeveelheid gegevens die voor een bepaalde hardware-inventaris eigenschap is gedefinieerd. De entiteit ' InstalledExecutable ' kan bijvoorbeeld meerdere MB aan gegevens per client retour neren, afhankelijk van de specifieke gegevens waarop u een query uitvoert. Zorg dat u de prestaties en schaal baarheid van uw systemen mindful wanneer u grotere gegevens sets voor hardware-inventarisatie van grotere verzamelingen wilt retour neren met behulp van CMPivot.

Een query verkeert na één uur naar een time-out. Een verzameling heeft bijvoorbeeld 500 apparaten en 450 van de clients zijn momenteel online. Deze actieve apparaten ontvangen de query en retour neren de resultaten bijna onmiddellijk. Als u het CMPivot-venster geopend laten, omdat de andere 50-clients online zijn, ontvangen ze ook de query en retour neren ze resultaten. 

## <a name="log-files"></a>Logboekbestanden

 CMPivot-interacties worden vastgelegd in de volgende logboek bestanden:

**Server zijde:**
- SmsProv. log
- BgbServer. log
- StateSys. log

**Aan de client zijde:**
- CcmNotificationAgent.log
- Scripts. log
- StateMessage.log

Zie [logboek bestanden](../../plan-design/hierarchy/log-files.md) en [probleemoplossings CMPivot](cmpivot-tsg.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen
 
[Problemen met CMPivot oplossen](cmpivot-tsg.md)

[PowerShell-scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md)


