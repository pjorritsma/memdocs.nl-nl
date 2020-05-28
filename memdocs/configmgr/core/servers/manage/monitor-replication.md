---
title: Database replicatie bewaken
titleSuffix: Configuration Manager
description: Meer informatie over het bewaken van SQL Server replicatie in uw Configuration Manager-hiërarchie.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 69550b35-bcdb-4b47-bbec-b3c8bc92bb7b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4a9ae791582911f91e5f76b841248ad5085d8170
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83879823"
---
# <a name="monitor-database-replication"></a>Database replicatie bewaken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Bewaak Details voor database replicatie met het knoop punt **database replicatie** in de werk ruimte **bewaking** van de Configuration Manager-console. U kunt de status van replicatie koppelingen tussen sites bewaken. Het bevat ook de initialisatie en replicatie van replicatie groepen voor de site waarmee u verbinding maakt.  

> [!TIP]  
> Hoewel het knoop punt **database replicatie** ook wordt weer gegeven onder het knoop punt **hiërarchie configuratie** in de werk ruimte **beheer** , kunt u de replicatie status voor database replicatie koppelingen vanaf die locatie niet weer geven.  

## <a name="replication-link-status"></a><a name="BKMK_MonitorReplicationLinks"></a> Status replicatiekoppeling  

Database replicatie tussen sites omvat de replicatie van verschillende gegevens sets, ook wel *replicatie groepen*genoemd. Elke replicatie groep verzendt en ontvangt gegevens met verschillende prioriteiten. Standaard kunt u de gegevens in een replicatie groep en de frequentie van replicatie niet wijzigen.  

Wanneer een replicatie koppeling actief is en de status ervan niet is mislukt of gedegradeerd, worden alle groepen snel gerepliceerd. Als een of meer groepen de replicatie in de verwachte periode niet kunnen volt ooien, wordt de koppeling als *gedegradeerd*weer gegeven. Gedegradeerde koppelingen kunnen nog steeds werken, maar u moet ze controleren om er zeker van te zijn dat ze terugkeren naar de status actief. Onderzoek ze om er zeker van te zijn dat er geen extra degradatie of replicatie fouten optreden.  

Geef voor elke replicatie koppeling het aantal keren op dat een niet-geslaagde gerepliceerde groep probeert te maken. Na dit aantal nieuwe pogingen stelt de site de status van de koppeling in op gedegradeerd of mislukt. Zelfs als alle groepen zijn gerepliceerd, stelt de site de status van de koppeling in op gedegradeerd of mislukt. Deze status wordt ingesteld omdat de ene replicatie groep de replicatie niet kan uitvoeren in het opgegeven aantal pogingen. Zie [drempel waarden voor database replicatie](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds)voor meer informatie.  

Gebruik de volgende informatie om de status van replicatie koppelingen te begrijpen die mogelijk verder moeten worden onderzocht:  

### <a name="link-is-active"></a>Koppeling is actief

Er zijn geen problemen gedetecteerd en de communicatie via de koppeling is actueel.

Terwijl een bovenliggende site wordt bijgewerkt naar een nieuwe versie en u de status van de koppeling van de onderliggende site bekijkt, wordt de status van de koppeling als actief weer gegeven. Na de update wordt de status van de koppeling als actief weer gegeven wanneer deze wordt bekeken vanaf de bovenliggende site totdat de onderliggende site zich op dezelfde versie bevindt als de bovenliggende site. Wanneer het wordt weer gegeven op de onderliggende site, wordt het weer gegeven als geconfigureerd.  

### <a name="link-is-degraded"></a>Koppeling is gedegradeerd

Replicatie is functioneel maar minstens een replicatieobject of -groep is vertraagd. Koppelingen in deze status controleren. Controleer de informatie van beide sites op de koppeling voor aanwijzingen dat de koppeling kan mislukken.

Een koppeling kan de status van gedegradeerd ook weergeven wanneer de site die gerepliceerde gegevens ontvangt de gegevens niet snel naar de database kan doorvoeren. Dit gedrag treedt op wanneer grote hoeveel heden gegevens worden gerepliceerd. U implementeert bijvoorbeeld een software-update op een groot aantal computers. De bovenliggende site op de koppeling kan enige tijd duren om dit volume van gerepliceerde gegevens te verwerken. Een verwerkings vertraging op de bovenliggende site resulteert in de status van de koppeling op gedegradeerd totdat de achterstand van gegevens kan worden verwerkt.

### <a name="link-has-failed"></a>Koppeling is mislukt

De replicatie is niet functioneel. Het is mogelijk dat een replicatie koppeling zonder verdere actie kan worden hersteld. Als u de replicatie op deze koppeling wilt onderzoeken en helpen herstellen, gebruikt u de Replication Link Analyzer (RLA).

Deze status kan ook duiden op een probleem met het fysieke netwerk tussen de bovenliggende en onderliggende site op de replicatiekoppeling.


## <a name="monitor-replication-status"></a><a name="BKMK_MonitorReplicationStatus"></a>Replicatie status controleren

Gebruik het knoop punt **database replicatie** in de werk ruimte **bewaking** om de status van een replicatie koppeling te bekijken. Details weer geven over de Data Base op elke site op de replicatie koppeling. U kunt ook details over replicatiegroepen weergeven. Als u deze details wilt weer geven, selecteert u een replicatie koppeling en selecteert u vervolgens het juiste tabblad voor de replicatie status die u wilt weer geven.

De volgende secties bevatten informatie over de verschillende tabbladen voor replicatie status:

### <a name="summary"></a>Samenvatting

Informatie op hoog niveau weer geven over de replicatie van site gegevens en algemene gegevens tussen de twee sites op een koppeling.  

Selecteer **rapporten voor historische verkeers gegevens weer geven** om een rapport weer te geven met informatie over de netwerk bandbreedte die wordt gebruikt door de replicatie over de koppeling.  

### <a name="parent-site"></a>Bovenliggende site

Voor de bovenliggende site op een replicatiekoppeling, gegevens inzake de database weergeven, met inbegrip van:  

- Firewallpoorten voor de SQL Server  

- Vrije schijfruimte  

- Databasebestandslocaties  

- Certificaten  

### <a name="child-site"></a>Onderliggende Site

Voor de onderliggende site op een replicatiekoppeling, gegevens inzake de database weergeven, met inbegrip van:  

- Firewallpoorten voor de SQL Server  

- Vrije schijfruimte  

- Databasebestandslocaties  

- Certificaten  

### <a name="initialization-detail"></a>Initialisatiedetails

De initialisatie status weer geven voor groepen die via de koppeling worden gerepliceerd. Deze informatie kan u helpen bij het identificeren wanneer initialisatie van replicatiegegevens uitgevoerd wordt of mislukt is.  

Gebruik deze informatie om te bepalen wanneer een site zich in de *interoperabiliteits modus*bevindt. De interoperabiliteits modus is wanneer de onderliggende site niet dezelfde versie van Configuration Manager uitvoert als de bovenliggende site.  

### <a name="replication-detail"></a>Replicatiedetails

Bekijk de replicatie status voor elke groep die via de koppeling repliceert. Gebruik deze informatie om te helpen bij het identificeren van problemen of vertragingen bij de replicatie van specifieke gegevens. Hiermee kunt u de juiste drempel waarden voor database replicatie voor deze koppeling bepalen. Zie [drempel waarden voor database replicatie](../../plan-design/hierarchy/database-replication.md#BKMK_DBRepThresholds)voor meer informatie.  

> [!TIP]  
> Replicatiegroepen voor sitegegevens worden enkel gezonden vanaf de onderliggende site naar de bovenliggende site. Replicatiegroepen voor globale gegevens worden gerepliceerd in beide richtingen.  


## <a name="replication-link-analyzer"></a><a name="BKMK_RLA"></a>Replication Link Analyzer

Configuration Manager bevat de **Replication link Analyzer** (RLA), waarmee u replicatie problemen kunt analyseren en herstellen. Gebruik RLA om koppelings fouten te herstellen wanneer de replicatie mislukt. Het is ook handig als de replicatie niet meer werkt, maar de site deze nog niet heeft gerapporteerd als mislukt.

Gebruik RLA voor het oplossen van replicatie problemen tussen de volgende computers in de hiërarchie:  

- Tussen een site server en de site database server  

- Tussen de database server van een site en de database server van een andere site, ook wel intersitereplicatie (intersite-replicatie) genoemd  

> [!Note]  
> De richting van de replicatie fout is niet van belang.

Voer RLA uit in de Configuration Manager-console of vanaf een opdracht prompt:  

- Om uit te voeren in de Configuration Manager-console gaat u naar de werk ruimte **bewaking** en selecteert u het knoop punt **database replicatie** . Selecteer de replicatie koppeling die u wilt analyseren en selecteer vervolgens op het lint **Replication link Analyzer**.  

- Typ de volgende opdracht om uit te voeren vanaf een opdracht prompt:`%ProgramFiles(x86)%\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe <source site server FQDN> <destination site server FQDN>`  

    > [!IMPORTANT]
    > Vanaf versie 1910 is dit pad gewijzigd om de map te gebruiken `Microsoft Endpoint Manager` . Zorg ervoor dat u geen oudere versie van het bestand gebruikt dat in een andere map kan voor komen.

Wanneer u RLA uitvoert, worden er problemen gedetecteerd door gebruik te maken van een reeks diagnostische regels en controles. U ziet de problemen die het hulp programma identificeert. Wanneer deze instructies bevat om een probleem op te lossen, worden ze weer gegeven. Als RLA automatisch een probleem kan oplossen, wordt deze optie weer gegeven.

Wanneer RLA is voltooid, worden de resultaten opgeslagen in het volgende XML-rapport en een logboek bestand op het bureau blad van de gebruiker die het hulp programma uitvoert:  

- ReplicationAnalysis.xml  

- ReplicationLinkAnalysis.log  

RLA stopt de volgende services terwijl er enkele problemen worden opgelost. Deze services worden opnieuw gestart wanneer het herstel is voltooid:  

- SMS_SITE_COMPONENT_MANAGER  

- SMS_EXECUTIVE  

Als RLA het herstel niet kan volt ooien, moet u deze services indien nodig opnieuw opstarten op de site server.  

RLA registreert alle onderzoek-en herstel acties om aanvullende details op te geven die niet worden weer gegeven in de wizard.  

### <a name="rla-prerequisites"></a>Vereisten voor RLA

Het account dat u gebruikt om RLA uit te voeren, moet de volgende machtigingen hebben:

- Lokale beheerders rechten op elke computer die betrokken is bij de replicatie koppeling.

- Sysadmin-rechten voor elke SQL Server-Data Base die betrokken is bij de replicatie koppeling.  

> [!Note]  
> Het account vereist geen specifieke Configuration Manager op rollen gebaseerde beheer beveiligingsrol. Een gebruiker met beheerders rechten met toegang tot het knoop punt **database replicatie** kan het hulp programma uitvoeren in de Configuration Manager-console. Een systeem beheerder met voldoende rechten voor elke computer kan het hulp programma uitvoeren vanaf een opdracht prompt.  

### <a name="rla-known-issue"></a>RLA bekend probleem

RLA genereert SQL Server Service Broker (SSB) certificaat fouten voor primaire sites die zijn bijgewerkt van System Center 2012 Configuration Manager. Dit probleem wordt veroorzaakt door wijzigingen in de namen van de certificaten in Configuration Manager current branch. U kunt deze fouten negeren.  


## <a name="monitoring-database-replication"></a><a name="BKMK_ProcsforMonitoringReplication"></a>Database replicatie bewaken  

### <a name="monitor-high-level-site-to-site-database-replication-status"></a>Replicatie status van site-naar-site-data base op hoog niveau controleren

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** .  

2. Selecteer het knoop punt **site hiërarchie** om de weer gave **hiërarchie diagram** te openen.  

3. Houd de muis aanwijzer op de lijn tussen de twee sites. Bekijk de status van globale en site gegevens replicatie voor deze sites.  

### <a name="monitor-the-status-of-a-replication-link"></a>De status van een replicatie koppeling bewaken

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** .  

2. Selecteer het knoop punt **database replicatie** en selecteer vervolgens de replicatie koppeling die u wilt bewaken. Selecteer vervolgens het juiste tabblad om verschillende details over de replicatie status voor die koppeling weer te geven.  
