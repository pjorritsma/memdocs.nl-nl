---
title: CMPivot voor realtime gegevens
titleSuffix: Configuration Manager
description: Meer informatie over hoe u CMPivot in Configuration Manager kunt gebruiken om clients in realtime te doorzoeken.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 11b5a58a6d9501b0368fcb0b47bf31df1bd8a6af
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700579"
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

- CMPivot en [micro soft Edge](../../../apps/deploy-use/deploy-edge.md) Installer zijn ondertekend met het **micro soft** -certificaat voor ondertekening van programma code. Als dat certificaat niet in het archief **vertrouwde uitgevers** wordt vermeld, moet u het toevoegen. Anders worden CMPivot en micro soft Edge Installer niet uitgevoerd wanneer het Power shell-uitvoerings beleid is ingesteld op **Alles ondertekend**. <!--7585106-->

## <a name="permissions"></a>Machtigingen

De volgende machtigingen zijn nodig voor CMPivot:

- **Lees** machtiging voor het object **SMS-scripts**
- De machtiging **scripts uitvoeren** voor de **verzameling**
   - Vanaf versie 1906 kunt u ook **Run CMPivot** gebruiken voor de **verzameling**.
- **Lees** machtiging voor **inventaris rapporten**
- Het standaard bereik.

> [!NOTE]
> - **Run scripts** is een superset van de machtiging **Run CMPivot** .
> - Vanaf versie 1906 zijn de [machtigingen voor CMPivot toegevoegd](cmpivot-changes.md#bkmk_cmpivot_secadmin1906) aan de ingebouwde rol **beveiligings beheerder** van Configuration Manager.
 
## <a name="limitations"></a>Beperkingen

- Verbind de Configuration Manager-console in een-hiërarchie met een *primaire site* om CMPivot uit te voeren. De actie **CMPivot starten** wordt niet weer gegeven in de-console wanneer deze is verbonden met een centrale beheer site (CAS).
  - Vanaf Configuration Manager versie 1902 kunt u CMPivot uitvoeren vanuit een certificerings instantie. In sommige omgevingen zijn extra machtigingen nodig. Zie [CMPivot changes for versie 1902](cmpivot-changes.md#bkmk_cmpivot1902)(Engelstalig) voor meer informatie.

- CMPivot retourneert alleen gegevens voor clients die zijn verbonden met de huidige site.  

- Als een verzameling apparaten van een andere site bevat, zijn de CMPivot-resultaten alleen van apparaten op de huidige site.  

- U kunt geen Entiteits eigenschappen, kolommen voor resultaten of acties op apparaten aanpassen.  

- Er kan slechts één exemplaar van CMPivot tegelijkertijd worden uitgevoerd op een computer waarop de Configuration Manager-console wordt uitgevoerd.  

- In versie 1806 werkt de query voor de entiteit **Administrators** alleen als de groep ' Administrators ' is. Het werkt niet als de groeps naam is gelokaliseerd. Bijvoorbeeld ' administrateurs ' in het Frans.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>CMPivot starten

1. Maak in de Configuration Manager-console verbinding met de primaire site. Ga naar de werk ruimte **activa en naleving** en selecteer het knoop punt **device Collections** . Selecteer een doel verzameling en klik in het lint op **CMPivot starten** om het hulp programma te starten. Als u deze optie niet ziet, controleert u de volgende configuraties:  
   - Bevestig met een site beheerder dat uw account de vereiste machtigingen heeft. Zie [vereisten](#prerequisites)voor meer informatie.  
   - Verbind de console met een *primaire site*.  

2. De interface biedt meer informatie over het gebruik van het hulp programma.  

     - Voer de query reeksen boven hand matig in of klik op de koppelingen in de online documentatie.  

     - Klik op een van de **entiteiten** om deze toe te voegen aan de query reeks.  

     - De koppelingen voor **tabel operators**, **aggregatie functies**en **scalaire functies** openen taal referentie documentatie in de webbrowser. CMPivot maakt gebruik van de [Kusto query language (KQL)](/azure/kusto/query/).  

3. Houd het venster CMPivot geopend om de resultaten van clients te bekijken. Wanneer u het venster CMPivot sluit, wordt de sessie voltooid.
   - Als de query is verzonden, verzenden clients nog steeds een antwoord op een status bericht naar de server.  



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

    - CMPivot maakt gebruik van een subset van de [Kusto query language (KQL)](/azure/kusto/query/).  

    - Inhoud knippen, kopiëren of plakken in het query venster.  
    <!-- markdownlint-disable MD038 -->
    - Dit deel venster maakt standaard gebruik van IntelliSense. Als u bijvoorbeeld begint te typen `D` , worden alle entiteiten voorgesteld die met die letter beginnen. Selecteer een optie en druk op TAB om deze in te voegen. Typ een sluis teken en een spatie `| ` en vervolgens worden alle tabel operators voorgesteld door IntelliSense. Voeg `summarize` een spatie in en typ een ruimte. IntelliSense stelt alle aggregatie functies voor. Klik op het tabblad **Start** in CMPivot voor meer informatie over deze opera tors en functies.  

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
         - Vanaf versie 2006 is de **draai tabel** vervangen door de **draai tabel**van het apparaat. Zie [CMPivot changes for versie 2006](cmpivot-changes.md#bkmk_2006)(Engelstalig) voor meer informatie.

      - **Script uitvoeren**: Hiermee start u de wizard script uitvoeren om een bestaand Power shell-script uit te voeren op dit apparaat. Zie [een script uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md#run-a-script)voor meer informatie.  

      - **Beheer op afstand**: start een Configuration Manager sessie voor beheer op afstand op dit apparaat. Zie [een Windows-client computer op afstand beheren](../../clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)voor meer informatie.  

      - **Resource Explorer**: start Configuration Manager resource Verkenner voor dit apparaat. Zie [hardware-inventaris weer geven](../../clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) of software- [inventaris weer geven](../../clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)voor meer informatie.  

   - Klik met de rechter muisknop op een andere cel dan een apparaat om de volgende aanvullende acties uit te voeren:  

     - **Kopiëren**: Kopieer de tekst van de cel naar het klem bord.  

     - **Apparaten weer geven met**: een query voor apparaten met deze waarde voor deze eigenschap. Selecteer bijvoorbeeld in de resultaten van de `OS` query deze optie in een cel in de rij versie: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Apparaten weer geven zonder**deze waarde voor deze eigenschap. Selecteer bijvoorbeeld in de resultaten van de `OS` query deze optie in een cel in de rij versie: `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

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



## <a name="example-scenarios"></a>Voorbeeldscenario's

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

Als u proactief met operationeel onderhoud wilt maken, kunt u één keer per week CMPivot uitvoeren op een verzameling van servers die u beheert en selecteert u **query all** op de entiteit **AppCrash** . Klik met de rechter muisknop op de kolom **filename** en selecteer **Oplopend sorteren**. Eén apparaat retourneert zeven resultaten voor sqlsqm.exe met een tijds tempel van ongeveer 03:00 elke dag. Selecteer de bestands naam in een van de rijen, klik er met de rechter muisknop op en selecteer **Bing it**. Door de zoek resultaten in de webbrowser bladeren, vindt u een micro soft-ondersteunings artikel voor dit probleem met meer informatie en oplossingen. 


### <a name="example-3-bios-version"></a>Voor beeld 3: BIOS-versie

Een van de vereisten is het bijwerken van het systeem-BIOS om [beveiligings problemen met speculatieve uitvoeringen](https://techcommunity.microsoft.com/t5/configuration-manager-blog/additional-guidance-to-mitigate-speculative-execution-side/ba-p/274974)op te lossen. U begint met een query voor de **BIOS** -entiteit. Vervolgens **groepeert u op** de eigenschap **Version** . Klik vervolgens met de rechter muisknop op een specifieke waarde, zoals "LENOVO-1140", en selecteer **apparaten weer geven met**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Voor beeld 4: beschik bare schijf ruimte

U moet tijdelijk een groot bestand opslaan op een netwerk Bestands server, maar niet zeker dat er voldoende capaciteit is. Start CMPivot op een verzameling bestands servers en zoek de entiteit **schijf** op. Wijzig de query voor CMPivot om snel een lijst met actieve servers met realtime-opslag gegevens te retour neren:  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="cmpivot-standalone"></a><a name="bkmk_standalone"></a> Zelfstandige CMPivot

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)]


 
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

- [Wijzigingen in CMPivot](cmpivot-changes.md)
- [Problemen met CMPivot oplossen](cmpivot-tsg.md)
- [PowerShell-scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md)