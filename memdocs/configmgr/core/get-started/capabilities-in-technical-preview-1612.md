---
title: Mogelijkheden van Technical Preview 1612
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1612.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 0c2464bfba05d640868af7d5c8be7c32c0999946
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721505"
---
# <a name="capabilities-in-technical-preview-1612-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1612 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*



Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1612. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="the-data-warehouse-service-point"></a>Het Data Warehouse-service punt
Vanaf de Technical Preview-versie 1612 kunt u met het Data Warehouse-service punt historische gegevens over lange termijn opslaan en rapporteren voor uw Configuration Manager-implementatie. Dit wordt bereikt door automatische synchronisaties van de Configuration Manager-site database naar een Data Warehouse-data base. Deze informatie is vervolgens toegankelijk vanaf uw Reporting Services-punt.

Wanneer u de nieuwe site systeemrol installeert, maakt Configuration Manager standaard de Data Warehouse database voor u op een SQL Server-exemplaar dat u opgeeft. Het Data Warehouse ondersteunt Maxi maal 2 TB aan gegevens, met tijds tempels voor het bijhouden van wijzigingen.  De gegevens die worden gesynchroniseerd vanuit de site database, bevatten standaard de gegevens groepen voor globale gegevens, site gegevens, Global_Proxy, Cloud gegevens en database weergaven. U kunt ook wijzigen wat er is gesynchroniseerd met aanvullende tabellen, of specifieke tabellen uitsluiten van de standaard-replicatie sets.
De standaard gegevens die worden gesynchroniseerd, bevatten informatie over:
- Status van infra structuur
- Beveiliging
- Naleving
- Malware   
- Software-implementatie
- Inventarisatie Details (er is echter geen synchronisatie van de inventarisatie geschiedenis)

Naast het installeren en configureren van de Data Warehouse database, worden er diverse nieuwe rapporten geïnstalleerd, zodat u deze gegevens eenvoudig kunt zoeken en rapporteren.

### <a name="data-warehouse-dataflow"></a>Gegevens stroom van Data Warehouse   
![Datawarehouse_flow](./media/datawarehouse.png)

| Stap         | Details  |
|:------:|-----------|  
| **1** | De site server verzendt en slaat gegevens op in de site database.  |  
| **2** | Op basis van het schema en de configuratie haalt het Data Warehouse-service punt gegevens op uit de site database.  |  
| **3** | Het Data Warehouse-service punt brengt een kopie van de gesynchroniseerde gegevens in de Data Warehouse-Data Base over en slaat deze op. |  
| **A** | Met behulp van ingebouwde rapporten wordt een aanvraag voor gegevens gemaakt die wordt door gegeven aan het Reporting Services-punt met behulp van SQL Server Reporting Services. |  
| **B** | De meeste rapporten zijn voor actuele informatie en deze aanvragen worden uitgevoerd op basis van de site database. |  
| **C** | Wanneer een rapport historische gegevens opvraagt met behulp van een van de rapporten in een *categorie* **Data Warehouse**, wordt de aanvraag uitgevoerd voor de Data Warehouse-data base.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Vereisten voor het Data Warehouse-service punt en de-data base
- Voor uw hiërarchie moet een site systeemrol van het Reporting Services-punt zijn geïnstalleerd.
- De computer waarop u de site systeemrol installeert, vereist .NET Framework 4.5.2 of hoger.
- Het computer account van de computer waarop u de site systeemrol installeert, moet lokale beheerders machtigingen hebben voor de computer die als host fungeert voor de Data Warehouse-data base.
- Het beheerders account dat u gebruikt voor het installeren van de site systeemrol, moet een DBO zijn op het exemplaar van SQL Server dat als host fungeert voor de Data Warehouse-data base.  
- De data base wordt ondersteund:
  - Met SQL Server 2012 of hoger, Enter prise of Data Center Edition.
  - Op een standaard-of benoemd exemplaar
  - Op een *SQL Server-cluster*. Hoewel deze configuratie zou moeten werken, is deze niet getest en wordt de ondersteuning het beste.
  - Als er een co-locatie met de data base van de site database of het Reporting Services-punt is. We raden u echter aan de installatie op een afzonderlijke server uit te voeren.  
- Het account dat wordt gebruikt als account van het *Reporting Services-punt* moet de **db_datareader** machtiging voor de Data Warehouse-data base hebben.  
- De data base wordt niet ondersteund in een *SQL Server AlwaysOn-beschikbaarheids groep*.

### <a name="install-the-data-warehouse"></a>Het Data Warehouse installeren
U installeert de-site systeemrol van het Data Warehouse op een centrale beheer site of primaire site met behulp van de **wizard site systeem rollen toevoegen** of de **wizard site systeem server maken**. Zie [site systeem rollen installeren](../servers/deploy/configure/install-site-system-roles.md) voor meer informatie. Een hiërarchie ondersteunt meerdere exemplaren van deze rol, maar er wordt slechts één instantie ondersteund op elke site.  

Wanneer u de functie installeert, maakt Configuration Manager de Data Warehouse database voor u op het door u opgegeven exemplaar van SQL Server. Als u de naam van een bestaande data base opgeeft (zoals u zou doen als u [de Data Warehouse-data base verplaatst naar een nieuw SQL Server](#move-the-data-warehouse-database)), wordt in Configuration Manager geen nieuwe data base gemaakt, maar wordt het door u opgegeven.

#### <a name="configurations-used-during-installation"></a>Configuraties die worden gebruikt tijdens de installatie
Gebruik de volgende informatie voor het volt ooien van de installatie van de site systeemrol:

**Selectie** pagina van de systeemrol:  
Voordat de wizard een optie geeft om het Data Warehouse-service punt te selecteren en te installeren, moet u een Reporting Services-punt hebben geïnstalleerd.

Pagina **Algemeen** : de volgende algemene informatie is vereist:
- **Configuration Manager Data Base-instellingen:**   
  - **Server naam** : Geef de FQDN op van de server die als host fungeert voor de site database. Als u geen standaard exemplaar van SQL Server gebruikt, moet u het exemplaar opgeven na de FQDN in de volgende notatie: *** &lt;Sqlserver_FQDN>\&lt; Instance_name>***
  - **Database naam** : Geef de naam op van de site database.
  - **Controleer of** de verbinding met de site database is geslaagd en klik op **verifiëren** .
</br></br>
- **Data Warehouse-database instellingen:**
  - **Server naam** : Geef de FQDN op van de server die als host fungeert voor het Data Warehouse-service punt en de data base. Als u geen standaard exemplaar van SQL Server gebruikt, moet u het exemplaar opgeven na de FQDN in de volgende notatie: *** &lt;Sqlserver_FQDN>\&lt; Instance_name>***
  - **Database naam** : Geef de FQDN op voor de Data Warehouse-data base.  Configuration Manager wordt de data base met deze naam gemaakt. Als u een database naam opgeeft die al bestaat op het exemplaar van SQL Server, zal Configuration Manager die data base gebruiken.
  - **Controleer of** de verbinding met de site database is geslaagd en klik op **verifiëren** .

Pagina **synchronisatie-instellingen** :   
- **Gegevens instellingen:**
  - **Replicatie groepen voor synchronisatie** : Selecteer de gegevens groepen die u wilt synchroniseren. Zie [database replicatie](../plan-design/hierarchy/data-transfers-between-sites.md#bkmk_dbrep) en **gedistribueerde weer gaven** in [gegevens overdracht tussen sites](../plan-design/hierarchy/data-transfers-between-sites.md)voor meer informatie over de verschillende typen gegevens groepen.
  - **Tabellen die zijn opgenomen in de synchronisatie** : Geef de naam op van elke aanvullende tabel die u wilt synchroniseren. Meerdere tabellen scheiden met een komma. Deze tabellen worden naast de door u geselecteerde replicatie groepen gesynchroniseerd vanuit de site database.
  - **Tabellen die zijn uitgesloten voor synchronisatie** : Geef de naam op van de afzonderlijke tabellen van de replicatie groepen die u synchroniseert. De tabellen die u opgeeft, worden uitgesloten van. Meerdere tabellen scheiden met een komma.
- **Synchronisatie-instellingen:**
  - **Synchronisatie-interval (minuten)** : Geef een waarde op in minuten. Nadat het interval is bereikt, wordt er een nieuwe synchronisatie gestart. Dit ondersteunt een bereik van 60 tot 1440 minuten (24 uur).
  - **Schema** : Geef de dagen op die u wilt dat de synchronisatie wordt uitgevoerd.

**Toegang tot rapportage punt**:   
Nadat de Data Warehouse-rol is geïnstalleerd, zorgt u ervoor dat het account dat wordt gebruikt als *Reporting Services-account* de **db_datareader** machtiging heeft voor de Data Warehouse-data base.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Problemen met de installatie en gegevens synchronisatie oplossen
Gebruik de volgende logboeken om problemen met de installatie van het Data Warehouse-service punt of de synchronisatie van gegevens te onderzoeken:
- **DWSSMSI. log** en **DWSSSetup. log** : gebruik deze logboeken om fouten te onderzoeken bij het installeren van het Data Warehouse-service punt.
- **Micro soft. ConfigMgrDataWarehouse. log** : dit logboek gebruiken om de gegevens synchronisatie tussen de site database naar de Data Warehouse-data base te onderzoeken.

### <a name="reporting"></a>Rapporten
Nadat u een Data Warehouse-site systeemrol hebt geïnstalleerd, zijn de volgende rapporten beschikbaar op uw Reporting Services-punt met een *categorie* **Data Warehouse:**

|Rapport                   | Details                                  |
|-------------------------|------------------------------------------|
| **Rapport over toepassings implementatie** | Details weer geven voor toepassings implementatie voor een specifieke toepassing en computer.|
| **Endpoint Protection en software Updatenaleving rapport**   | Computers weer geven waarop software-updates ontbreken.|
| **Algemene hardware-inventaris rapport**  | Bekijk alle hardware-inventarisatie voor een specifieke computer.|
| **Algemeen rapport van software-inventaris**  | Bekijk alle software-inventarisatie voor een specifieke computer.|
| **Overzicht van infrastructuur status**  |Geeft een overzicht van de status van uw Configuration Manager-infra structuur.|
| **Lijst met gedetecteerde malware**  |Schadelijke software weer geven die in de organisatie is gedetecteerd.|
| **Overzichts rapport software distributie** | Een samen vatting van software distributie voor een specifieke advertentie en computer.|

### <a name="move-the-data-warehouse-database"></a>De Data Warehouse-data base verplaatsen
Gebruik de volgende stappen om de Data Warehouse-data base te verplaatsen naar een nieuwe SQL Server:

1. Controleer de huidige database configuratie en noteer de configuratie gegevens, waaronder:  
   - De gegevens groepen die u synchroniseert
   - Tabellen die u wilt opnemen of uitsluiten van synchronisatie       

   U kunt deze gegevens groepen en tabellen opnieuw configureren nadat u de Data Base naar een nieuwe server hebt hersteld en de site systeemrol opnieuw hebt geïnstalleerd.  

2. Gebruik SQL Server Management Studio om een back-up van de Data Warehouse database te maken en herstel de data base vervolgens opnieuw naar een SQL-Server op de nieuwe computer die als host zal fungeren voor het Data Warehouse.

   Nadat u de Data Base naar de nieuwe server hebt hersteld, moet u ervoor zorgen dat de toegangs machtigingen voor de data base in de nieuwe Data Warehouse-data base gelijk zijn aan die van de oorspronkelijke Data Warehouse-data base.

3. Gebruik de Configuration Manager-console om de site systeemrol van het Data Warehouse-service punt te verwijderen van de huidige server.

4. Installeer een nieuw data warehouse-service punt en geef de naam op van de nieuwe SQL Server en het exemplaar dat als host fungeert voor de Data Warehouse-data base die u hebt hersteld.

5. Wanneer de site systeemrol wordt geïnstalleerd, is de verplaatsing voltooid.

U kunt de volgende Configuration Manager-logboeken bekijken om te bevestigen dat de site systeemrol opnieuw is geïnstalleerd:  
- **DWSSMSI. log** en **DWSSSetup. log** : gebruik deze logboeken om fouten te onderzoeken bij het installeren van het Data Warehouse-service punt.
- **Micro soft. ConfigMgrDataWarehouse. log** : dit logboek gebruiken om de gegevens synchronisatie tussen de site database naar de Data Warehouse-data base te onderzoeken.


## <a name="content-library-cleanup-tool"></a>Hulp programma inhouds bibliotheek opruimen
Vanaf Technical Preview versie 1612 kunt u een nieuw opdracht regel programma (**ContentLibraryCleanup. exe**) gebruiken om inhoud te verwijderen die niet meer is gekoppeld aan een pakket of toepassing van een distributie punt (zwevende inhoud). Dit hulp programma wordt het hulp programma voor het opschonen van inhouds bibliotheken genoemd.

Dit hulp programma is alleen van invloed op de inhoud van het distributie punt dat u opgeeft wanneer u het hulp programma uitvoert en kan inhoud niet verwijderen uit de inhouds bibliotheek op de site server.

Nadat u Technical Preview 1612 hebt geïnstalleerd, kunt u **ContentLibraryCleanup. exe** vinden in de map *% CM_Installation_Path% \ cd\* . latest\SMSSETUP\TOOLS\ContentLibraryCleanup op de site Server Technical Preview.

Het hulp programma dat bij deze Technical Preview is uitgebracht, is bedoeld ter vervanging van oudere versies van vergelijk bare hulpprogram ma's die zijn uitgebracht voor eerdere Configuration Manager producten. Hoewel deze versie van het hulp programma niet meer werkt na 1 maart, 2017, zullen nieuwe versies worden vrijgegeven met toekomstige technische previews totdat dit hulp programma wordt uitgebracht als onderdeel van de Current Branch of een kant-en-klare release van productie.

### <a name="requirements"></a>Vereisten  
- Het hulp programma kan rechtstreeks worden uitgevoerd op de computer waarop het distributie punt wordt gehost of op afstand vanaf een andere server. Het hulp programma kan slechts op één distributie punt tegelijk worden uitgevoerd.
- Het gebruikers account dat het hulp programma uitvoert, moet rechtstreeks beheer machtigingen op basis van rollen hebben die gelijk zijn aan een volledige beheerder op de Configuration Manager hiërarchie.  Het hulp programma werkt niet wanneer aan het gebruikers account machtigingen worden verleend als lid van een Windows-beveiligings groep met de volledige beheerders machtigingen.

### <a name="modes-of-operation"></a>Bedrijfsmodi
Het hulp programma kan in twee modi worden uitgevoerd:
1. **Modus voor ' wat als'**:   
   Wanneer u de schakel optie **/Delete** niet opgeeft, wordt het hulp programma uitgevoerd in de modus What-if en wordt de inhoud geïdentificeerd die zou worden verwijderd uit het distributie punt, maar worden er geen gegevens verwijderd.

   - Wanneer het hulp programma in deze modus wordt uitgevoerd, wordt informatie over de inhoud die wordt verwijderd automatisch naar het logboek bestand van de hulpprogram ma's geschreven. De gebruiker wordt niet gevraagd om elke mogelijke verwijdering te bevestigen.
   - Standaard wordt het logboek bestand geschreven naar de tijdelijke map van gebruikers op de computer waarop u het hulp programma uitvoert, maar u kunt de optie/log gebruiken om het logboek bestand om te leiden naar een andere locatie.  
   </br>

   We raden u aan het hulp programma uit te voeren in deze modus en het resulterende logboek bestand te bekijken voordat u het hulp programma uitvoert met de schakel optie/delete.  

2. **Verwijder modus**: wanneer u het hulp programma uitvoert met de schakel optie **/Delete** , wordt het hulp programma uitgevoerd in de modus verwijderen.

   - Wanneer het hulp programma wordt uitgevoerd in deze modus, kan zwevende inhoud die is gevonden op het opgegeven distributie punt, worden verwijderd uit de inhouds bibliotheek van het distributie punt.
   -  Voordat u elk bestand verwijdert, wordt de gebruiker gevraagd om te bevestigen dat het bestand moet worden verwijderd.  U kunt, **j** voor Ja, **N** voor Nee of **Ja op alles** selecteren om verdere vragen over te slaan en alle zwevende inhoud te verwijderen.  
   </br>

   We raden u aan het hulp programma uit te voeren in de modus ' wat Als' ' en het resulterende logboek bestand te controleren voordat u het hulp programma uitvoert met de schakel optie/delete.  

Wanneer het hulp programma voor het opschonen van de inhouds bibliotheek in een van beide modi wordt uitgevoerd, wordt er automatisch een logboek gemaakt met een naam die de modus bevat waarin het hulp programma wordt uitgevoerd, de naam van het distributie punt, de datum en het tijdstip van de bewerking. Het logboek bestand wordt automatisch geopend wanneer het hulp programma is voltooid. Standaard wordt dit logboek geschreven naar de **tijdelijke** map van gebruikers op de computer waarop u het hulp programma uitvoert. u kunt echter een opdracht regel parameter gebruiken om het logboek bestand om te leiden naar een andere locatie, inclusief een netwerk share.   


### <a name="run-the-tool"></a>Het hulp programma uitvoeren
Het hulp programma uitvoeren:
1. Open een opdracht prompt met beheerders rechten naar een map met **ContentLibraryCleanup. exe**.  
2. Voer vervolgens een opdracht regel in met de vereiste opdracht regel parameters en optionele Schakel opties die u wilt gebruiken.

**Bekend probleem** Wanneer het hulp programma wordt uitgevoerd, kan er een fout melding als het volgende worden geretourneerd wanneer een pakket of implementatie mislukt of wordt uitgevoerd:
-  *System. InvalidOperationException: deze inhouds bibliotheek kan nu niet worden opgeruimd omdat pakket \<packageID> niet volledig is geïnstalleerd.*

**Tijdelijke oplossing:** geen. Het hulp programma kan geen zwevende bestanden identificeren wanneer de inhoud wordt uitgevoerd of niet kan worden geïmplementeerd. Daarom is het hulp programma niet in staat om inhoud op te schonen totdat het probleem is opgelost.



### <a name="command-line-switches"></a>Opdracht regel opties  
De volgende opdracht regel parameters kunnen in een wille keurige volg orde worden gebruikt.   

|Switch|Details|
|---------|-------|
|**/Delete**  |**Beschrijving** </br> Gebruik deze schakel optie als u inhoud wilt verwijderen van het distributie punt. U wordt gevraagd om de inhoud te verwijderen. </br></br> Als deze schakel optie niet wordt gebruikt, registreert het hulp programma de resultaten van welke inhoud zou worden verwijderd, maar verwijdert geen inhoud van het distributie punt. </br></br> Voor beeld: ***ContentLibraryCleanup. exe/dp server1.contoso.com/delete*** |
| **q**       |**Beschrijving** </br> Voer het hulp programma uit in de Stille modus dat alle prompts onderdrukt (zoals vragen wanneer u inhoud verwijdert) en open het logboek bestand niet automatisch. </br></br> Voor beeld: ***ContentLibraryCleanup. exe/q/dp server1.contoso.com*** |
| **/DP &lt;-distributie punt FQDN->**  | **Vereist** </br> Geef de Fully Qualified Domain Name (FQDN) op van het distributie punt dat u wilt opschonen. </br></br> Voor beeld: ***ContentLibraryCleanup. exe/dp server1.contoso.com***|
| **FQDN &lt;->van primaire site/PS**       | **Optioneel** bij het opschonen van inhoud van een distributie punt op een primaire site.</br>**Vereist** bij het opschonen van inhoud van een distributie punt op een secundaire site. </br></br> Geef de FQDN op van de primaire site waarvan het distributie punt deel uitmaakt, of van het bovenliggende primaire bovenliggend element wanneer het distributie punt zich op een secundaire site bevindt. </br></br> Voor beeld: ***ContentLibraryCleanup. exe/dp server1.contoso.com/ps siteserver1.contoso.com*** |
| **/SC &lt;Primary site code>**  | **Optioneel** bij het opschonen van inhoud van een distributie punt op een primaire site.</br>**Vereist** bij het opschonen van inhoud van een distributie punt op een secundaire site. </br></br> Geef de site code op van de primaire site waarvan het distributie punt deel uitmaakt, of van de bovenliggende primaire site wanneer het distributie punt zich op een secundaire site bevindt.</br></br> Voor beeld: ***ContentLibraryCleanup. exe/dp server1.contoso.com/SC ABC*** |
| **/Log \<logboek bestand map>**       |**Beschrijving** </br> Geef een map op waarin de logboek bestanden moeten worden geplaatst. Dit kan een lokaal station of een netwerk share zijn.</br></br> Als deze schakel optie niet wordt gebruikt, worden logboek bestanden automatisch in de map Temp van de gebruiker geplaatst.</br></br> Voor beeld van een lokaal station: ***ContentLibraryCleanup. exe/dp server1.contoso.com/log C:\Users\Administrator\Desktop*** </br></br>Voor beeld van een netwerk share: ***ContentLibraryCleanup. exe/DP \\ &lt;server1.contoso.com/Log \&share>lt; map>***|


## <a name="improvements-for-in-console-search"></a>Verbeteringen voor zoeken in console
Op basis van feedback van gebruikers spraak hebben we de volgende verbeteringen toegevoegd aan de zoek opdracht in de console:
- **Objectpad:**  
  Veel objecten ondersteunen nu een nieuwe kolom met de naam **Objectpad**.  Wanneer u deze kolom zoekt en opneemt in uw weergave resultaten, kunt u het pad naar elk object weer geven. Als u bijvoorbeeld een zoek opdracht uitvoert voor apps in het knoop punt toepassingen en ook subknooppunten zoekt, wordt in de kolom *Objectpad* in het deel venster met resultaten het pad weer gegeven naar elk object dat wordt geretourneerd.   

- **Behoud van Zoek tekst:**  
  Wanneer u tekst in het zoekvak invoert en vervolgens omschakelt tussen het doorzoeken van een subknooppunt en het huidige knoop punt, blijft de tekst die u hebt getypt nu behouden en blijft deze beschikbaar voor een nieuwe zoek opdracht zonder dat u deze opnieuw hoeft te typen.

- **Behoud van uw besluit om subknooppunten te doorzoeken:**  
  De optie die u selecteert voor het zoeken naar het *huidige knoop punt* of *alle subknooppunten* , blijft behouden wanneer u het knoop punt wijzigt waarin u werkt.   Dit betekent dat u de beslissing niet voortdurend opnieuw moet instellen wanneer u over de console gaat.  Wanneer u de console opent, is de optie standaard alleen van het huidige knoop punt te doorzoeken.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Installatie van een toepassing voor komen als een opgegeven programma wordt uitgevoerd.
U kunt nu een lijst met uitvoer bare bestanden (met de extensie. exe) configureren in de implementatie type-eigenschappen, zodat de installatie van een toepassing wordt geblokkeerd als deze wordt uitgevoerd. Nadat de installatie is uitgevoerd, krijgen gebruikers een dialoog venster te zien waarin wordt gevraagd om de processen te sluiten die de installatie blok keren.

### <a name="try-it-out"></a>Uitproberen
Een lijst met uitvoer bare bestanden configureren
1. Kies op de pagina eigenschappen van een implementatie type het tabblad **afhandeling van het installatie programma** .
2. Klik op **toevoegen**om een of meer uitvoer bare bestanden toe te voegen aan de lijst (bijvoorbeeld **Edge. exe**)
3. Klik op **OK** om het dialoog venster Eigenschappen van implementatie type te sluiten.

Wanneer u deze toepassing nu implementeert voor een gebruiker of een apparaat en een van de uitvoer bare bestanden die u hebt toegevoegd, wordt het dialoog venster Software Center weer gegeven waarin wordt vermeld dat de installatie is mislukt omdat er een toepassing wordt uitgevoerd.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nieuwe melding voor Windows hello voor bedrijven voor eind gebruikers

Een nieuwe melding van Windows 10 informeert de eind gebruikers dat ze aanvullende acties moeten ondernemen om de installatie van Windows hello voor bedrijven te volt ooien (bijvoorbeeld het instellen van een pincode).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Ondersteuning voor Windows Store voor bedrijven in Configuration Manager

U kunt nu online gelicentieerde Apps implementeren met het implementatie doel **beschikbaar** van de Windows Store voor bedrijven naar pc's met de Configuration Manager-client.
Zie [apps beheren in de Windows Store voor bedrijven met Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)voor meer informatie.

Ondersteuning voor deze functie is momenteel alleen beschikbaar voor Pc's met de preview-versie van Windows 10 RS2.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Terugkeren naar de vorige pagina wanneer een taken reeks mislukt
U kunt nu teruggaan naar een vorige pagina wanneer u een taken reeks uitvoert en er een fout optreedt. Vóór deze release moest u de taken reeks opnieuw opstarten als er een fout is opgetreden. U kunt bijvoorbeeld de **vorige** knop in de volgende scenario's gebruiken:

- Wanneer een computer wordt opgestart in Windows PE, wordt het dialoog venster Boots trap van taken reeks mogelijk weer gegeven voordat de taken reeks beschikbaar is. Als u in dit scenario op Volgende klikt, wordt de laatste pagina van de taken reeks weer gegeven met een bericht dat er geen taken reeksen beschikbaar zijn. U kunt nu op **vorige** klikken om opnieuw te zoeken naar beschik bare taken reeksen. U kunt dit proces herhalen totdat de taken reeks beschikbaar is.
- Wanneer u een taken reeks uitvoert, maar afhankelijke inhouds pakketten zijn nog niet beschikbaar op distributie punten, mislukt de taken reeks. U kunt nu de ontbrekende inhoud distribueren (als deze nog niet is gedistribueerd) of wachten tot de inhoud beschikbaar is op distributie punten, en klik vervolgens op **vorige** om de taken reeks opnieuw te laten zoeken naar de inhoud.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Ondersteuning voor snelle installatie bestanden voor Windows 10-updates
We hebben ondersteuning voor snelle installatie bestanden toegevoegd in Configuration Manager voor Windows 10-updates. Wanneer u een ondersteunde versie van Windows 10 gebruikt, kunt u nu Configuration Manager-instellingen gebruiken om alleen de verschillen te downloaden tussen de cumulatieve update voor Windows 10 van de huidige maand en de update van de vorige maand. In Configuration Manager Current Branch wordt de volledige cumulatieve update van Windows 10 (inclusief alle updates van de vorige maanden) elke maand gedownload. Het gebruik van bestanden voor snelle installatie biedt kleinere down loads en snellere installatie tijden op clients.

> [!IMPORTANT]
> Hoewel de instellingen voor de ondersteuning van het gebruik van bestanden voor snelle installatie in Configuration Manager beschikbaar zijn, wordt deze functionaliteit alleen ondersteund in Windows 10 versie 1607 met een Windows Update Agent update die is opgenomen in de updates die zijn uitgebracht op 10 januari 2017 (patch-dinsdag). Zie [ondersteuning voor artikel 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693)voor meer informatie over deze updates. U kunt profiteren van de bestanden voor snelle installatie wanneer de volgende set updates wordt uitgebracht op 14 februari 2017. Windows 10 versie 1607 zonder de update en eerdere versies bieden geen ondersteuning voor bestanden voor snelle installatie.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Downloaden van bestanden voor snelle installatie voor Windows 10-updates op de server inschakelen
Als u wilt beginnen met het synchroniseren van de meta gegevens voor Windows 10 Express-installatie bestanden, moet u deze inschakelen in de eigenschappen van het software-update punt.
1. Ga in de Configuration Manager-console naar **beheer** > **site configuratie** > **sites**.
2. Selecteer de centrale beheer site of de zelfstandige primaire site.
3. Klik op het tabblad **Start** in de groep **Instellingen** op **Sitecomponenten configureren** en klik op **Software-updatepunt**. Op het tabblad **Update bestanden** selecteert u **volledige bestanden downloaden voor alle goedgekeurde updates en bestanden voor snelle installatie voor Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Ondersteuning inschakelen voor clients voor het downloaden en installeren van bestanden voor snelle installatie
Als u ondersteuning voor bestanden voor snelle installatie op clients wilt inschakelen, moet u bestanden voor snelle installatie op clients inschakelen in de sectie Software-updates van client instellingen. Hiermee wordt een nieuwe HTTP-listener gemaakt waarmee wordt geluisterd naar aanvragen voor het downloaden van snelle installatie bestanden op de poort die u opgeeft. Zodra u client instellingen hebt geïmplementeerd om deze functionaliteit op de client in te scha kelen, wordt geprobeerd de verschillen tussen de cumulatieve update van Windows 10 van de huidige maand en de update van de vorige maand te downloaden (clients moeten een versie van Windows 10 uitvoeren die snelle installatie bestanden ondersteunt).
1. Schakel ondersteuning voor snelle installatie bestanden in de eigenschappen van software-update punt componenten in (vorige procedure).
2. Ga in de Configuration Manager-console naar **beheer** > **client instellingen**.
3. Selecteer de juiste client instellingen en klik vervolgens op het tabblad **Start** op **Eigenschappen**.
4. Selecteer de **pagina software-updates** , Configureer **Ja** voor de instelling de **installatie van snelle updates op clients inschakelen** en configureer de poort die wordt gebruikt door de HTTP-listener op de client voor de **poort die wordt gebruikt voor het downloaden van inhoud voor de instelling voor snelle updates** .


## <a name="odata-endpoint-data-access"></a>Toegang tot gegevens van OData-eind punt

 Configuration Manager biedt nu een REST OData-eind punt voor toegang tot Configuration Manager gegevens. Het eind punt is compatibel met Odata versie 4, waarmee hulp middelen zoals Excel en Power BI eenvoudig toegang krijgen tot Configuration Manager gegevens via een enkel eind punt. Technical Preview 1612 ondersteunt alleen lees toegang tot objecten in Configuration Manager.  

Gegevens die momenteel beschikbaar zijn in de [WMI-provider van Configuration Manager](../../develop/reference/configuration-manager-reference.md) zijn nu ook toegankelijk met het nieuwe OData-eind punt. Met de entiteit sets die door het OData-eind punt worden weer gegeven, kunt u de gegevens die u met de WMI-provider wilt opvragen, opsommen.

### <a name="try-it-out"></a>Uitproberen

Voordat u het OData-eind punt kunt gebruiken, moet u het inschakelen voor de site.

1.  Ga naar **beheer** > **site configuratie** > **sites**.
2.  Selecteer de primaire site en klik op **Eigenschappen**.
3.  Klik op het tabblad Algemeen van het eigenschappen venster van de primaire site op **rest-eind punt inschakelen voor alle providers op deze site**en klik vervolgens op **OK**.

Probeer in uw favoriete OData-query-Viewer query's die vergelijkbaar zijn met de volgende voor beelden om verschillende objecten in Configuration Manager te retour neren:

| Doel | OData-query |
|---|---|
| Alle verzamelingen ophalen | `http://localhost/CMRestProvider/Collection` |
| Een verzameling ophalen | `http://localhost/CMRestProvider/Collection('SMS00001')`
| De Top 100-apparaten in de verzameling ophalen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Een apparaat met een resource-ID in de verzameling ophalen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Besturings systeem van het apparaat in de verzameling ophalen | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Gebruikers in de verzameling ophalen | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> De voorbeeld query's die in de tabel worden weer gegeven, gebruiken *localhost* als de hostnaam in de URL en kunnen worden gebruikt op de computer waarop de SMS-provider wordt uitgevoerd. Als u uw query's uitvoert vanaf een andere computer, vervangt u localhost door de FQDN van de server waarop de SMS-provider is geïnstalleerd.

## <a name="azure-active-directory-onboarding"></a>Azure Active Directory onboarding

Met Azure Active Directory (AD) onboarding wordt een verbinding gemaakt tussen Configuration Manager en Azure Active Directory die door andere Cloud Services kunnen worden gebruikt. Dit kan momenteel worden gebruikt voor het maken van de verbinding die nodig is voor de cloudbeheergateway.

Voer deze taak uit met een Azure-beheerder, omdat u Azure-beheerders referenties nodig hebt.

#### <a name="to-create-the-connection"></a>De verbinding maken:

2. Kies in de werk ruimte **beheer** de optie **Cloud Services** > **Azure Active Directory** > **Azure Active Directory toevoegen**.
2. Klik op **Aanmelden** om de verbinding met Azure ad te maken.

#### <a name="configuration-manager-client-requirements"></a>Client vereisten Configuration Manager

Er zijn verschillende vereisten voor het inschakelen van het maken van gebruikers beleid in de cloudbeheergateway.

- Het Azure AD-voorbereidings proces moet zijn voltooid en de client moet eerst verbonden zijn met het bedrijfs netwerk om de verbindings gegevens op te halen.
- Clients moeten beide lid zijn van een domein (geregistreerd in Active Directory) en lid zijn van de Cloud domein (geregistreerd in azure AD).
- U moet [Active Directory gebruikers detectie](../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)uitvoeren.
- U moet de Configuration Manager-client wijzigen om aanvragen voor gebruikers beleid via Internet toe te staan en de wijziging op de client te implementeren. Omdat deze wijziging in de client plaatsvindt *op het client apparaat*, kan deze worden geïmplementeerd via de cloudbeheergateway, hoewel u de configuratie wijzigingen die nodig zijn voor het gebruikers beleid nog niet hebt voltooid.
- Uw beheer punt moet worden geconfigureerd om HTTPS te gebruiken voor het beveiligen van het token in het netwerk en .net 4,5 moet zijn geïnstalleerd.

Nadat u deze configuratie wijzigingen hebt aangebracht, kunt u een gebruikers beleid maken en clients naar Internet verplaatsen om het beleid te testen. Aanvragen voor gebruikers beleid via de cloudbeheergateway worden geverifieerd met Azure AD-verificatie op basis van tokens.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Wijziging in het configureren van multi-factor Authentication voor apparaatregistratie

Nu u multi-factor Authentication (MFA) voor apparaatregistratie kunt instellen in de Azure Portal, is de optie MFA verwijderd in de Configuration Manager-console. [In dit onderwerp](/mem/intune/enrollment/multi-factor-authentication)vindt u meer informatie over Microsoft intune het instellen van MFA voor inschrijving.
