---
title: Richtlijnen voor grootte en prestaties van sites
titleSuffix: Configuration Manager
description: Site grootte-gerelateerde prestatie test resultaten, methodologie en richt lijnen.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 9e5cc21e4fef60f64576a7b578b3616a7e37756d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073497"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Richt lijnen voor site grootte en-prestaties Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager leidt de branche in de schaal baarheid en prestaties. Andere documentatie heeft betrekking op [Maxi maal ondersteunde schaalbaarheids limieten](size-and-scale-numbers.md) en [Hardware-richt lijnen](recommended-hardware.md) voor het uitvoeren van sites in de grootste omgevings grootten. Dit artikel biedt aanvullende prestatie richtlijnen voor omgevingen van elke omvang. Deze richt lijnen kunnen u helpen om de hardware die u nodig hebt om Configuration Manager te implementeren nauw keuriger te ramen.

Dit artikel is gericht op de grootste bijdrager aan Configuration Manager prestatie knelpunten: het subsysteem voor de invoer/uitvoer van schijven of IOPS. Het artikel:

- Geeft details weer en test resultaten die zijn gericht op IOPS
- Documenten over het reproduceren van de tests met uw eigen omgevingen en hardware
- Voorst Ellen voor schijf-IOPS-vereisten voor verschillende grootte omgevingen 

## <a name="performance-test-methodology"></a>Methodologie voor prestatie testen

U kunt Configuration Manager op tal van unieke manieren implementeren, maar het is belang rijk dat u een aantal variabelen in een bepaalde formaat discussie begrijpt. Een variabele is een *functie-interval*, zoals een inventarisatie cyclus. Een andere variabele is het aantal gebruikers, software-implementaties of andere *objecten* waarnaar het systeem verwijst of implementeert. Bij het testen van de prestaties worden deze variabelen toegepast als onderdeel van een *belasting*. De belasting genereert objecten met een typische snelheid voor zakelijke klanten die gebruikmaken van productie-implementaties in verschillende grootte omgevingen.

> [!NOTE] 
> Met telemetrie van de klant kunnen huidige branch-builds worden getest met de meest voorkomende scenario's, configuraties en instellingen voor de meeste klanten. De aanbevelingen in dit artikel zijn gebaseerd op deze gemiddelden. Uw ervaringen kunnen variëren afhankelijk van de grootte en configuratie van uw omgeving. Over het algemeen is Configuration Manager gemeen schappelijke betekenis wanneer het gaat om objecten en intervallen. Net omdat u elk bestand op een systeem kunt verzamelen of het interval voor een cyclus instelt op één minuut, betekent dat niet.

In de volgende secties worden enkele belang rijke instellingen en configuraties gemarkeerd die moeten worden gebruikt bij het testen en model leren van verwerkings behoeften voor grote ondernemingen. Deze richt lijnen helpen u bij het instellen van basis verwachtingen voor systeem prestaties voor de voorgestelde hardware-grootten.

### <a name="feature-intervals-settings"></a>Instellingen voor functie-intervallen 
Voor de meeste tests moet u gebruikmaken van de standaard intervallen voor de belangrijkste cycli in het systeem. Bijvoorbeeld: de hardware-inventarisatie test vindt één keer per week plaats met een groter bestand dan default *. MOF* . Sommige terugkerende functie-intervallen, met name hardware-en software-inventarisatie cycli, kunnen aanzienlijke gevolgen hebben voor de prestatie kenmerken van een omgeving. Omgevingen die agressieve standaard intervallen voor het verzamelen van gegevens nodig hebben, hebben de hardware in direct verhouding tot de toename van de activiteit. Stel bijvoorbeeld dat u 25.000 desktop-clients hebt en de hardware-inventaris twee keer sneller wilt verzamelen dan het standaard interval. U moet eerst de hardware van uw site aanpassen alsof u 50.000-clients had.

### <a name="objects"></a>Objecten 
Tests moeten gebruikmaken van het *bovenste gemiddelde* van de objecten die grote ondernemingen vaak gebruiken voor het systeem. Typische waarden zijn duizenden verzamelingen en toepassingen, die worden geïmplementeerd op honderd duizenden gebruikers of systemen. Tests moeten tegelijkertijd op *alle* objecten in het systeem worden uitgevoerd. Veel klanten maken gebruik van verschillende functies, maar gebruiken doorgaans niet alle functies van het product op deze hoogste limieten. Testen met alle product functies helpt de best mogelijke prestaties op het hele systeem te garanderen en biedt een buffer voor functies die sommige klanten het bovenstaande gemiddelde kunnen gebruiken. 

### <a name="loads"></a>Laden 
Testen moeten ook worden uitgevoerd op een waarde die groter is dan de standaard *gemiddelde dag* , door simulaties uit te voeren die een piek gebruiks vereisten op het systeem genereren. Een voor beeld is het simuleren van patch-dinsdag implementaties, om ervoor te zorgen dat het systeem onmiddellijk update nalevings gegevens kan retour neren tijdens deze dagen van piek activiteit. Een ander voor beeld is het simuleren van site activiteiten tijdens een wijde uitvallende malware, om ervoor te zorgen dat er tijdig meldingen en reacties mogelijk zijn. Hoewel geïmplementeerde machines van de aanbevolen grootte op een bepaalde dag kunnen worden gebruikt, is voor de meest extreme situaties een verwerkings buffer vereist.

### <a name="configurations"></a>Configuraties
Voer tests uit op een bereik van fysieke, Hyper-V-en Azure-hardware, met een combi natie van ondersteunde besturings systemen en SQL Server versies. Valideer altijd de slechtste gevallen voor de ondersteunde configuratie. Over het algemeen retour neren Hyper-V en Azure vergelijk bare prestatie resultaten naar gelijkwaardige fysieke hardware wanneer ze op dezelfde manier zijn geconfigureerd. Nieuwere besturings systemen van de server werken vaak gelijk of beter dan oudere, ondersteunde besturings systemen van de server. Hoewel alle ondersteunde platforms voldoen aan de minimale vereisten, hebben de nieuwste versies van ondersteunende producten, zoals Windows en SQL, zelfs betere prestaties. 

De grootste variatie is afkomstig uit de SQL Server versies die in gebruik zijn. Zie voor meer informatie over SQL Server versies [welke versie van SQL moet ik uitvoeren?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run). 

## <a name="key-performance-determinants"></a>Belangrijkste prestatie determinanten

U kunt de prestaties van Configuration Manager testen en meten met diverse instellingen, op verschillende manieren en op verschillende site grootten. De volgende instellingen en objecten kunnen aanzienlijk van invloed zijn op de prestaties. Houd er rekening mee dat u ze overweegt bij het testen en model leren van de prestaties in uw omgeving.

> [!CAUTION]
> Hoewel weinig aspecten van Configuration Manager officiële maximum waarden of beperkingen van de gebruikers interface hebben waardoor overmatig gebruik wordt voor komen, kunnen de richt lijnen een aanzienlijke nadelige invloed hebben op de prestaties van een site. Het overschrijden van de aanbevolen niveaus of het negeren van de richt lijnen vereist meestal grotere hardware, waardoor uw omgeving mogelijk niet kan worden onderhouden totdat u de frequentie of het aantal verschillende objecten verlaagt.

### <a name="hardware-inventory"></a>Hardware-inventaris
Als u de basislijn prestaties wilt testen, stelt u de hardware-inventaris verzameling in op één keer per week, met de standaard grootte van het *MOF* -bestand plus ongeveer 20% extra eigenschappen. Schakel niet alle eigenschappen in en verzamel alleen de eigenschappen die u daad werkelijk nodig hebt. Let op het verzamelen van eigenschappen, zoals het beschik bare virtuele geheugen, die *altijd* worden gewijzigd bij *elke* inventarisatie cyclus. Het verzamelen van deze eigenschappen kan te wijten zijn aan een buitensporig verloop op elke inventarisatie cyclus van elke client.

### <a name="software-inventory"></a>Software-inventaris
Als u de basislijn prestaties wilt testen, stelt u software-inventaris verzameling in op één keer per week, met alleen details van *product* . Het verzamelen van veel bestanden kan een belang rijke stam op het inventaris subsysteem plaatsen. Vermijd het opgeven van filters die het verzamelen van duizenden bestanden in veel clients, zoals * \*. exe* of * \*. dll*, kunnen beëindigen.

### <a name="collections"></a>Verzamelingen
Basislijn prestaties kunnen bestaan uit meerdere duizenden verzamelingen met verschillende bereik-, grootte-, complexiteits-en update-instellingen. Site prestaties is geen directe functie van het Sheer aantal verzamelingen op een site. Prestaties zijn ook een cross-product van de verzameling query's, volledige en incrementele updates en wijzigings frequentie, afhankelijkheden tussen verzamelingen en aantal clients in de verzamelingen.

Minimaliseer zo mogelijk verzamelingen met dure of gecompliceerde dynamische regel query's. Voor verzamelingen waarvoor deze typen regels zijn vereist, stelt u de juiste update-intervallen en update tijden in om de impact van de herevaluatie van de verzameling op het systeem te minimaliseren. Bijvoorbeeld: update om middernacht in plaats van 8:00 uur.

Het inschakelen van incrementele updates voor verzamelingen zorgt voor snelle en tijdige updates voor verzamelings lidmaatschap. Maar hoewel incrementele updates efficiënt zijn, worden ze nog steeds geladen op het systeem. Bewaak de wijzigings frequentie die u verwacht met de behoefte aan bijna realtime updates voor het lidmaatschap. Stel bijvoorbeeld dat u een zware verloop verwacht bij de verzamelings leden, maar u geen bijna realtime lidmaatschaps updates nodig hebt. Het is efficiënter en levert minder belasting op het systeem om de verzameling bij een bepaald interval bij te werken met een geplande volledige update dan om incrementele updates in te scha kelen. 

Wanneer u incrementele updates inschakelt, moet u alle geplande volledige updates op dezelfde verzamelingen verlagen. Ze zijn slechts een back-upmethode voor evaluatie, omdat bij incrementele updates het lidmaatschap van de verzameling bijna in realtime moet worden bijgewerkt. [Best Practices for collections](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental) raadt een maximum aantal verzamelingen aan voor incrementele updates, maar naarmate het artikel uitvalt, kan uw ervaring variëren op basis van een groot aantal factoren.

Verzamelingen met alleen regels voor direct lidmaatschap en een beperkende verzameling die geen incrementele updates uitvoert, hebben geen geplande volledige updates nodig. Schakel de update planningen voor deze typen verzamelingen uit om onnodige belasting van het systeem te voor komen. Als de beperkende verzameling incrementele updates gebruikt, mogen verzamelingen met alleen directe lidmaatschaps regels Maxi maal 24 uur worden bijgewerkt, of totdat een geplande vernieuwing plaatsvindt.

Hoewel er geen best practice zijn, maken sommige organisaties honderden of zelfs duizenden verzamelingen als onderdeel van verschillende bedrijfs processen. Als u Automation gebruikt om verzamelingen te maken, is het belang rijk om de nood zakelijke incrementele updates correct in te scha kelen. Minimaliseer en verspreid eventuele volledige update schema's om te voor komen dat er hot spots worden geëvalueerd tijdens één tijds periode. Stel een normaal opschonings proces in voor het verwijderen van ongebruikte verzamelingen, met name als u automatisch verzamelingen maakt die u niet meer nodig hebt na enige tijd.

Houd er rekening mee dat Configuration Manager beleids regels maakt voor alle objecten in uw verzamelingen wanneer u taken zoals implementaties op de doel groep aanwijst. Wijzigingen in het lidmaatschap, hetzij via geplande vernieuwing of incrementele updates, kunnen veel andere werk voor het hele systeem maken. De nieuwste huidige branch-builds hebben speciale beleids optimalisaties voor de verzamelingen alle systemen en alle gebruikers. Bij het richten op uw hele onderneming gebruikt u de ingebouwde verzamelingen in plaats van een kloon van deze ingebouwde verzamelingen.

Als u de prestaties van de verzameling nog verder wilt onderzoeken, kunt u de verzamelings evaluatie Viewer (CEViewer) in de [Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012)gebruiken.

### <a name="discovery-methods"></a>Detectie methoden
Voor het testen van de basislijn prestaties voert u eenmaal per week detectie methoden op server uit en schakelt u de detectie van verschillen in, zodat de gegevens tijdens de week vernieuwd blijven. De tests moeten een object hoeveelheid in verhouding tot de gesimuleerde bedrijfs grootte detecteren. De prestatie basislijn test voor heartbeat-detectie moet ook eenmaal per week worden uitgevoerd.

De detectie gegevens zijn algemene gegevens. Een veelvoorkomend probleem met de prestaties is het configureren van op servers gebaseerde detectie methoden in een hiërarchie, waardoor duplicaten detectie van dezelfde bronnen vanuit meerdere primaire sites wordt voor komen. Configureer de detectie methoden zorgvuldig voor het optimaliseren van de communicatie met de doel service, zoals Active Directory domein controllers, terwijl het dupliceren van hetzelfde detectie bereik op meerdere primaire sites wordt voor komen.

## <a name="general-sizing-guidelines"></a>Algemene richt lijnen voor aanpassing 

Op basis van de voor gaande [prestatie test methodologie](#performance-test-methodology)bevat de volgende tabel algemene richt lijnen *voor hardwarevereisten voor* specifieke aantallen beheerde clients. Deze waarden moeten de meeste klanten met het opgegeven aantal clients in staat stellen snel genoeg objecten te verwerken om de opgegeven site te beheren. Reken kracht blijft elk jaar dalen, en enkele van de onderstaande vereisten zijn klein in het kader van moderne hardwareconfiguraties voor servers. Hardware die de volgende richt lijnen overschrijdt, verhoogt de prestaties voor sites waarvoor extra verwerkings kracht is vereist of die speciale product gebruiks patronen hebben. 

| Desktop-clients  | Site type/-rol  | Kernen<sup>1</sup>   | Geheugen (GB)   | Toewijzing van SQL-geheugen  | IOPS: Postvak in<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Vereiste opslag ruimte (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25k  | Primaire of certificerings instantie met database siterol op dezelfde server   | 6   | 24  | 65% | 600  | 1700 | 350  |
| 25k  | Primair of CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | Externe SQL                                                  | 4   | 16  | 70% |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50.000  | Primaire of certificerings instantie met database siterol op dezelfde server   | 8   | 32  | 70% | 1200 | 2800 | 600  |
| 50.000  | Primair of CAS                                              | 4   | 8   |     | 1200 |      | 200  |
|      | Externe SQL                                                  | 8   | 24  | 70% |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100.000 | Primaire of certificerings instantie met database siterol op dezelfde server   | 12  | 64  | 70% | 1200 | 5000 | 1100 |
| 100.000 | Primair of CAS                                              | 6   | 12  |     | 1200 |      | 300  |
|      | Externe SQL                                                  | 12  | 48  | 80% |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150k | Primaire of certificerings instantie met database siterol op dezelfde server   | 16  | 96  | 70% | 1800 | 7400 | 1600 |
| 150k | Primair of CAS                                   | 8   | 16   |     | 1800  |         | 400   |
|      | Externe SQL                                       | 16  | 72   | 90% |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700k | CA'S met de database siterol op dezelfde server   | 20+ | 128 en | 80% | 1800 + | 9000 +   | 5000 + |
| 700k | CAS                                              | 8 +  | 16+  |     | 1800 + |         | 500 +  |
|      | Externe SQL                                       | 16+ | 96 +  | 90% |       | 9000 +   | 4500 + |
|      |                                                             |     |     |     |      |      |      |
| 5k   | Secundaire site                                   | 4   | 8    |     | 500   | -       | 200   |
| rpm  | Secundaire site                                   | 8   | 16   |     | 500   | -       | 300   |

**Opmerkingen**

1. **Kernen**: Configuration Manager voert een groot aantal gelijktijdige processen uit, dus vereist een bepaald minimum aan CPU-kernen voor diverse site grootten. Hoewel kernen elk jaar sneller worden, is het belang rijk om ervoor te zorgen dat een bepaald minimum aantal kernen parallel werkt. Over het algemeen is een CPU op server niveau die is geproduceerd na 2015 voldoet aan de basis prestatie behoeften voor de kernen die zijn opgegeven in de tabel. Configuration Manager profiteert van extra kernen naast de aanbevelingen, maar in het algemeen geldt dat als u de minimale aanbevolen kernen hebt, u de prioriteit van CPU-resource investeringen moet bepalen om de snelheid van bestaande kernen te verhogen, en niet meer, langzamere kernen toe te voegen. Configuration Manager werkt bijvoorbeeld beter bij belang rijke verwerkings taken met 16 snelle kernen dan met 24 langzame kernen, ervan uitgaande dat er voldoende andere systeem bronnen zijn, zoals schijf-IOPS.
   
   De relatie tussen kernen en geheugen is ook belang rijk. Over het algemeen vermindert de totale verwerkings capaciteit van uw SQL-servers ten minste 3-4 GB RAM per kern. U hebt meer RAM per kern nodig als SQL met de site Server onderdelen wordt geplaatst.
   
   > [!NOTE]
   > Alle tests stellen machine energiebeheer schema's in staat om Maxi maal CPU-energie verbruik en prestaties toe te staan.
   
2. **IOPS: post vakken en IOPS: SQL** verwijzen naar de IOPS-behoeften voor de Configuration Manager en logische SQL-stations. De kolom **IOPS: Postvak** in bevat de IOPS-vereisten voor het logische station waar de Configuration Manager mappen in het postvak in zich bevinden. In de kolom **IOPS: SQL** wordt het totale aantal IOPS-behoeften weer gegeven voor de logische stations die door verschillende SQL-bestanden worden gebruikt. Deze kolommen verschillen, omdat de twee stations een andere indeling moeten hebben. Zie de [Veelgestelde vragen over de site grootte en-prestaties](../../understand/site-size-performance-faq.md)voor meer informatie en voor beelden over voorgestelde SQL-schijf configuraties en aanbevolen procedures voor bestanden, inclusief informatie over het splitsen van bestanden op meerdere volumes.
   
   Beide IOPS-kolommen gebruiken gegevens uit het industrie-standaard hulp programma, *Diskspd*. Zie [schijf prestaties meten](#how-to-measure-disk-performance) voor instructies voor het dupliceren van deze metingen. Over het algemeen beschikt het opslag subsysteem over de grootste invloed op de prestaties van de site, en biedt de verbeteringen de meeste gevolgen voor de berekenings capaciteit.
   
3.  **Vereiste opslag ruimte:** Deze reële waarden kunnen afwijken van andere gedocumenteerde aanbevelingen. We geven deze cijfers alleen als algemene richt lijnen. de afzonderlijke vereisten kunnen aanzienlijk verschillen. Plan zorgvuldig de benodigde schijf ruimte voor de site-installatie. Stel dat een deel van deze opslag de meeste vrije schijf ruimte blijft. U kunt deze buffer ruimte in een herstel scenario gebruiken, of voor upgrade scenario's die vrije schijf ruimte nodig hebben voor het instellen van het pakket uitbrei ding. Uw site vereist mogelijk extra opslag voor grote hoeveel heden gegevens verzameling, langere Peri Oden van gegevens retentie en grote hoeveel heden software distributie-inhoud. U kunt deze items ook opslaan op afzonderlijke volumes met een lage door voer.

## <a name="how-to-measure-disk-performance"></a>Schijf prestaties meten 

U kunt het *Diskspd* -hulp programma gebruiken om gestandaardiseerde suggesties te bieden voor de IOPS die voor verschillende afmetingen Configuration Manager omgevingen nodig zijn. De volgende test stappen en opdracht regels zijn niet volledig, maar bieden een eenvoudige en reproduceer bare manier om de door Voer van het schijf subsysteem van de servers te ramen. U kunt de resultaten vergelijken met de minimale aanbevolen IOPS in de tabel [algemene richt lijnen](#general-sizing-guidelines) voor het aanpassen van de grootte. 

Zie [voor beelden van schijf configuraties](#example-disk-configurations) voor test resultaten van een groot aantal hardwareconfiguraties in test omgevingen. U kunt de gegevens voor een ruw begin punt gebruiken bij het ontwerpen van het opslag subsysteem voor een nieuwe omgeving.

### <a name="to-test-disk-iops"></a>Schijf-IOPS testen  
1. Down load hier het *Diskspd* - [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62)hulp programma:.
   
1. Zorg ervoor dat er ten minste 100 GB vrije schijf ruimte beschikbaar is. Schakel alle apps uit die de schijf kunnen verstoren of extra belasting veroorzaken, zoals het actief scannen van virussen van de Directory, SQL of SMSExec.
   
1. Voer *Diskspd* uit vanaf een opdracht prompt met verhoogde bevoegdheid. 
   
   Voer twee uitvoeringen van het hulp programma uit voor het volume dat u wilt testen. De eerste test voert 64 KB-grootte, wille keurige schrijf bewerkingen voor één minuut uit. Deze test garandeert het laden van de Controller cache en de toewijzing van de schijf ruimte voor het geval het volume dynamisch kan worden uitgebreid. De resultaten van de eerste test negeren. De tweede test moet *onmiddellijk* volgen op de eerste test en dezelfde belasting gedurende vijf minuten uitvoeren.
   
   Gebruik bijvoorbeeld de volgende opdracht regels om het volume G:\\ te testen.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Bekijk de uitvoer van de tweede test om de totale IOPS in de kolom **I/O per s** te vinden. In het volgende voor beeld is het totale aantal IOPS **3929,18**.

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Voor beeld van schijf configuraties

In de volgende tabellen ziet u de resultaten van het uitvoeren van de test stappen in het [meten van schijf prestaties](#how-to-measure-disk-performance) met verschillende testlab-configuraties. Gebruik deze gegevens voor een *ruw* begin punt bij het ontwerpen van het opslag subsysteem voor een nieuwe omgeving. 

### <a name="physical-machines-and-hyper-v"></a>Fysieke machines en Hyper-V 
Hardware wordt altijd verbeterd. U verwacht nieuwere generaties hardware en verschillende combi Naties van hardware, zoals Ssd's en San's, om de hieronder vermelde prestaties te overschrijden. Deze resultaten vormen een basis uitgangs punt om te overwegen bij het ontwerpen van een server of het bespreken van de hardwareleverancier.

In de volgende tabel ziet u de test resultaten op verschillende subsystemen van de schijf, met inbegrip van de harde schijven van de spindle en SSD, in verschillende testlab-configuraties. Alle configuraties Format teren de schijven met 64 KB-clusters en voeg ze toe aan een schijf controller voor bedrijfs klassen. Naast het aantal schijven van de RAID-matrix, hebben ze elk ten minste één reserve schijf.

| Schijftype   | Aantal schijven, niet inclusief + 1 reserve schijf | RAID     | Gemeten IOPS  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15.000 SAS          | 2                                                  |           1   | 620           |
| 15.000 SAS          | 4                                                  |           10  | 1206          |
| 15.000 SAS          | 6                                                  |           10  | 1751          |
| 15.000 SAS          | 8                                                  |           10  | 2322          |
| 15.000 SAS          | 10                                                 |           10  | 2882          |
| 15.000 SAS          | 12                                                 |           10  | 3476          |
| 15.000 SAS          | 16                                                 |           10  | 4236          |
| 15.000 SAS          | 20                                                 |           10  | 5148          |
| 15.000 SAS          | 30                                                 |           10  | 7398          |
| 15.000 SAS          | 40                                                 |           10  | 9913          |
| SSD-SATA         | 2                                                  |           1   | 3300          |
| SSD-SATA         | 4                                                  |           10  | 5542          |
| SSD-SATA         | 6                                                  |           10  | 7201          |
| SAS VAN SSD          | 2                                                  |           1   | 7539          |
| SAS VAN SSD          | 4                                                  |           10  | 14346         |
| SAS VAN SSD          | 6                                                  |           10  | 15607         |

Dit zijn de apparaten die het voor beeld gebruikt. Deze informatie is niet een aanbeveling voor een specifiek hardware model of een specifieke fabrikant. 

| Schijftype    | Model      | RAID-controller | Cache geheugen en-configuratie |
|-------------------|-----------------|----------------------|-------------------------------------|
| SAS HD van 15.000 RPM    | HP EH0300JDYTH  | P822 slimme matrix     | 2 GB, 20% lezen/80% schrijven           |
| SSD-SATA          | ATA-MK0200GCTYV | P420i slimme matrix    | 1 GB, 20% lezen/80% schrijven           |
| SAS VAN SSD           | HP MO0800 JEFPB | P420i slimme matrix    | 1 GB, 20% lezen/80% schrijven           |

### <a name="azure-machine-and-disk-performance"></a>Prestaties van Azure-machine en-schijf 
De prestaties van de Azure-schijf zijn afhankelijk van verschillende factoren, zoals de grootte van de virtuele machine van Azure en het aantal en het type schijven dat wordt gebruikt. Azure voegt ook voortdurend nieuwe machine typen en schijf snelheden toe die afwijken van het volgende diagram. Zie [Configuration Manager op veelgestelde vragen over Azure](../../understand/configuration-manager-on-azure.md)voor meer informatie over Configuration Manager die worden uitgevoerd op Azure en aanvullende informatie over de schijf-I/O op Azure.

Alle schijven zijn opgemaakt als NTFS 64 KB cluster grootte en rijen met meer dan één schijf worden geconfigureerd als striped volumes via het hulp programma voor schijf beheer van Windows.

| Azure VM| Azure-schijf| Aantal schijven | Beschik bare ruimte | Gemeten IOPS   | Beperkings factor   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Azure VM-grootte   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Azure VM-grootte   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Azure VM-grootte   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Azure VM-grootte   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 MB                    | 1994  | Azure VM-grootte   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1024 MB                   | 1992  | Azure VM-grootte   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1024 MB                   | 1993  | Azure VM-grootte   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2048 MB                   | 1992  | Azure VM-grootte   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 MB                    | 2334  | P20-schijf        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1024 MB                   | 3984  | Azure VM-grootte   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1536 MB                   | 3984  | Azure VM-grootte   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1024 MB                   | 3112  | P30-schijf        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2048 MB                   | 3984  | Azure VM-grootte   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3072 MB                   | 3996  | Azure VM-grootte   |
| **DS5 HEEFT/DS14/F16S**                         | P20                     | 1                   | 512 MB                    | 2335  | P20-schijf        |
| **DS5 HEEFT/DS14/F16S**                         | P20                     | 2                   | 1024 MB                   | 4639  | P20-schijf        |
| **DS5 HEEFT/DS14/F16S**                         | P20                     | 3                   | 1536 MB                   | 6913  | P20-schijf        |
| **DS5 HEEFT/DS14/F16S**                         | P20                     | 4                   | 2048 MB                   | 7966  | Azure VM-grootte   |
| **DS5 HEEFT/DS14/F16S**                         | P30                     | 1                   | 1024 MB                   | 3112  | P30-schijf        |
| **DS5 HEEFT/DS14/F16S**                         | P30                     | 2                   | 2048 MB                   | 6182  | P30-schijf        |
| **DS5 HEEFT/DS14/F16S**                         | P30                     | 3                   | 3072 MB                   | 7963  | Azure VM-grootte   |
| **DS5 HEEFT/DS14/F16S**                         | P30                     | 4                   | 4096 MB                   | 7968  | Azure VM-grootte   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | P30-schijf        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | P30-schijf        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | P30-schijf        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Azure VM-grootte   |

## <a name="see-also"></a>Zie tevens

- [Veelgestelde vragen over site formaat en-prestaties](../../understand/site-size-performance-faq.md)
- [Veelgestelde vragen over Azure Configuration Manager](../../understand/configuration-manager-on-azure.md)
- [Grootte en schaalgetallen](size-and-scale-numbers.md)
- [Aanbevolen hardware](recommended-hardware.md)

