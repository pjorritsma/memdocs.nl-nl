---
title: Wijzigingen in CMPivot
titleSuffix: Configuration Manager
description: Meer informatie over de wijzigingen die zijn aangebracht in CMPivot tussen Configuration Manager versies.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: a49a9564-0863-44c3-991e-a8e271fed586
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 20b23cec74ae3d201bc81fe1834e87e7eb8fcc13
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129644"
---
# <a name="changes-to-cmpivot"></a>Wijzigingen in CMPivot

Gebruik de volgende informatie voor meer informatie over de wijzigingen die zijn aangebracht in [CMPivot](cmpivot.md) tussen Configuration Manager-versies:

## <a name="cmpivot-changes-for-version-2006"></a><a name="bkmk_2006"></a>CMPivot wijzigingen voor versie 2006
<!--6518631-->

Vanaf versie 2006 zijn de volgende verbeteringen aangebracht in CMPivot:

- [CMPivot standalone](cmpivot.md#bkmk_standalone) en CMPivot gestart vanuit de beheer console zijn geconvergeerd. Wanneer u CMPivot start vanuit de-beheer console, gebruikt deze dezelfde onderliggende technologie als CMPivot standalone om u een scenario pariteit te geven.

- Verbeteringen voor toetsenbord navigatie in CMPivot.

- U kunt CMPivot uitvoeren vanaf een afzonderlijk apparaat of meerdere apparaten vanaf het knoop punt apparaten zonder dat u een verzameling apparaten hoeft te selecteren. Deze verbetering maakt het gemakkelijker voor mensen, zoals degenen die werken als de helpdesk medewerker, voor het maken van CMPivot-query's voor specifieke apparaten buiten een vooraf gemaakte verzameling.
   - Selecteer een afzonderlijk apparaat of meerdere apparaten in een apparaat-verzameling of selecteer **Start CMPivot**.

- Wanneer apparaten in een query lijst weergave worden geretourneerd, kunt u de optie voor het selecteren van het **apparaat** op een of meer apparaten en vervolgens draaiing en query op deze apparaten op dezelfde manier om in te zoomen. Met deze wijziging kunt u inzoomen zonder de grotere set apparaten uit de oorspronkelijke verzameling te doorzoeken. De draai tabel van **het** **apparaat** is vervangen door.
   - In een bestaande CMPivot-bewerking selecteert u een afzonderlijk apparaat of meerdere apparaten selecteren in de uitvoer. Klik met de rechter muisknop en draai het diagram met de optie voor het selecteren van **apparaten** . Met deze actie wordt een afzonderlijk exemplaar van de CMPivot-instantie gestart, alleen voor de apparaten die u hebt geselecteerd. Zo kunt u eenvoudig draaien en alleen query's uitvoeren op apparaten die zijn gewenst zonder dat u hiervoor een verzameling hoeft te maken.

- Wanneer u CMPivot uitvoert voor een afzonderlijk apparaat, wordt de naam van het apparaat bovenaan het venster weer gegeven. Voor meerdere apparaten wordt het aantal geselecteerde apparaten bovenaan het venster weer gegeven.
- De optie **verzameling maken** op het tabblad Query samenvatting is verwijderd omdat voor CMPivot niet meer query's hoeven te worden uitgevoerd op een verzameling. Voer een **draai tabel** van het apparaat uit om een nieuw exemplaar van CMPivot scoped te openen voor alleen de apparaten waarop u een query wilt uitvoeren. De **verzameling maken** is nog steeds beschikbaar in het hoofd menu.

![De draai tabel van het apparaat voor meerdere apparaten met behulp van CMPivot](./media/6518631-cmpivot-multi-select.png)


## <a name="cmpivot-changes-for-version-2002"></a><a name="bkmk_2002"></a>CMPivot wijzigingen voor versie 2002
<!--5870934-->
We hebben het eenvoudiger gemaakt om te navigeren in CMPivot-entiteiten. Vanaf Configuration Manager versie 2002 kunt u CMPivot-entiteiten zoeken. Er zijn ook nieuwe pictogrammen toegevoegd om de entiteiten en de object typen van de entiteit eenvoudig te onderscheiden.

![Zoeken in CMPivot-entiteiten](./media/5870934-search-cmpivot-entities.png)


## <a name="cmpivot-changes-for-version-1910"></a><a name="bkmk_cmpivot1910"></a>CMPivot wijzigingen voor versie 1910
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

### <a name="wineventlognametimespan"></a><a name="bkmk_WinEvent"></a>Wine vent ( \<logname> , [ \<timespan> ])

Deze entiteit wordt gebruikt voor het ophalen van gebeurtenissen uit gebeurtenis logboeken en logboek bestanden voor gebeurtenis tracering. De entiteit haalt gegevens op uit gebeurtenis logboeken die worden gegenereerd door de Windows-gebeurtenis logboek technologie. De entiteit haalt ook gebeurtenissen op in logboek bestanden die zijn gegenereerd door Event Tracing for Windows (ETW). Wine vent bekijkt de gebeurtenissen die standaard in de afgelopen 24 uur zijn opgetreden. De standaard instelling voor 24 uur kan echter worden overschreven door een time span op te nemen.

``` Kusto
WinEvent('Microsoft-Windows-HelloForBusiness/Operational', 1d)
| where LevelDisplayName =='Error'
| summarize count() by Device
```

### <a name="filecontentfilename"></a><a name="bkmk_File"></a>FileContent ( \<filename> )

FileContent wordt gebruikt om de inhoud van een tekst bestand op te halen.

``` Kusto
FileContent('c:\\windows\\SMSCFG.ini')
| where Content startswith  'SMS Unique Identifier='
| project Device, SMSId= substring(Content,22)
```

### <a name="processmoduleprocessname"></a><a name="bkmk_ProcessModule"></a>ProcessModule ( \<processname> )  

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
Wanneer u CMPivot gebruikt buiten de Configuration Manager-console, kunt u alleen een query uitvoeren op het lokale apparaat zonder dat de Configuration Manager-infra structuur nodig is. U kunt nu gebruikmaken van de CMPivot Azure Log Analytics-query's om snel WMI-gegevens op het lokale apparaat weer te geven. Hiermee wordt ook de validatie en verfijning van CMPivot-query's ingeschakeld voordat deze in een grotere omgeving worden uitgevoerd. Zelfstandige CMPivot is alleen beschikbaar in het Engels. Zie [CMPivot standalone](#bkmk_standalone)voor meer informatie over CMPivot standalone.

#### <a name="known-issues-for-local-device-query-evaluation"></a>Bekende problemen met de evaluatie van query's van lokale apparaten

 - Als u op **deze PC** een query uitvoert voor een WMI-entiteit waartoe u geen toegang hebt, zoals een VERGRENDELDE WMI-klasse, ziet u mogelijk een crash in CMPivot. Voer CMPivot uit met een account met verhoogde bevoegdheden voor het opvragen van deze entiteiten. <!--5753242-->
- Als u op **deze PC**niet-WMI-entiteiten opvraagt, ziet u een **Ongeldige naam ruimte** of een niet-eenduidige uitzonde ring.
- Voer CMPivot standalone uit vanuit de snelkoppeling in het menu Start, niet rechtstreeks vanuit het pad van het uitvoer bare bestand. <!--5787962-->

### <a name="other-enhancements"></a><a name="bkmk_Other"></a>Andere verbeteringen

- U kunt reguliere expressie type query's uitvoeren met behulp van de `like` operator new. Bijvoorbeeld:<!--3056858-->
  
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
    > [Installeer CMPivot standalone](#bkmk_standalone)om deze koppeling te laten werken.

- Als het apparaat is inge schreven in micro soft Defender Advanced Threat Protection (ATP), klikt u met de rechter muisknop op het apparaat om de **micro soft defender Security Center** Online-Portal te starten.

### <a name="known-issues-for-cmpivot-in-version-1910"></a>Bekende problemen voor CMPivot in versie 1910

- De banner voor het maximum aantal resultaten kan niet worden weer gegeven wanneer de limiet is bereikt. <!--5431427-->
  - Elke client is beperkt tot 128 KB aan gegevens per query.
  - Resultaten kunnen worden afgekapt als de resultaten van de query groter zijn dan 128 KB.

## <a name="cmpivot-changes-for-version-1906"></a><a name="bkmk_cmpivot1906"></a>CMPivot wijzigingen voor versie 1906

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

[!INCLUDE [CMPivot standalone](includes/cmpivot-standalone.md)] 

## <a name="cmpivot-changes-for-version-1902"></a><a name="bkmk_cmpivot1902"></a>CMPivot wijzigingen voor versie 1902
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


## <a name="cmpivot-changes-for-version-1810"></a><a name="bkmk_cmpivot"></a>CMPivot wijzigingen voor versie 1810
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
   - Deze optie is verwijderd in versie 2006, omdat voor CMPivot niet meer query's moeten worden uitgevoerd op een verzameling.
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

Vanaf versie 1810, wanneer u CMPivot uitvoert, wordt een controle status bericht gemaakt met **MessageID 40805**. U kunt de status berichten weer geven door naar **bewaking**  >  **systeem status**  >  **status bericht query's**te gaan. U kunt **alle controle status berichten voor een specifieke gebruiker**uitvoeren, **alle controle status berichten voor een specifieke site**of uw eigen status bericht query maken.

De volgende indeling wordt gebruikt voor het bericht:

MessageId 40805: gebruiker &lt; gebruikers naam> script &lt; script-GUID> met hash &lt; -script-hash-> in verzamelings &lt; verzameling-id> wordt uitgevoerd.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 is de script-GUID voor CMPivot.
- De script-hash kan worden weer gegeven in het logboek bestand van de client.
- U kunt ook de hash zien die is opgeslagen in het script archief van de client. De bestands naam op de client is &lt; script-Guid>_ &lt; script-Hash->.
    - Voor beeld van bestands naam: C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123. PS
   

![Voor beeld van CMPivot-controle status bericht](media/cmpivot-audit-status-message.png)

## <a name="next-steps"></a>Volgende stappen
 
[Problemen met CMPivot oplossen](cmpivot-tsg.md)
