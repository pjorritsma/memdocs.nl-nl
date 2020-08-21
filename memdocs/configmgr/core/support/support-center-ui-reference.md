---
title: Naslag informatie voor ondersteunings centrum-gebruikers interface
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van de hulpprogram ma's van het ondersteunings centrum.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 79d483f95c12c1da1e34ca556836a1f42bbffbef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699446"
---
# <a name="support-center-user-interface-reference"></a>Naslag informatie voor de gebruikers interface van ondersteunings centrum

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u een beschrijving van de gebruikers interfaces (UI) van de hulpprogram ma's van het ondersteunings centrum:
- Ondersteuningscentrum
- Logboek viewer voor ondersteunings centrum
- Viewer voor ondersteunings centrum



## <a name="support-center-reference"></a>Naslag informatie over ondersteunings centrum

In deze sectie wordt de gebruikers interface voor het hulp programma **ondersteunings centrum** beschreven. 
- [Venster menu](#bkmk_support-window)  
- [Tabblad Start](#bkmk_support-home)  
- [Tabblad client](#bkmk_support-client)  
- [Tabblad beleid](#bkmk_support-policy)  
- [Tabblad inhoud](#bkmk_support-content)  
- [Tabblad voor Raad](#bkmk_support-inventory)  
- [Tabblad probleem oplossing](#bkmk_support-troubleshoot)  
- [Tabblad logboeken](#bkmk_support-logs)  


### <a name="window-menu"></a><a name="bkmk_support-window"></a> Venster menu

Selecteer in de linkerbovenhoek van het venster van het ondersteunings centrum de pijl in het blauwe vak om dit menu te openen.

#### <a name="local-machine-connection"></a>Verbinding met lokale machine
Het ondersteunings centrum verzamelt logboek bestanden en voert probleem oplossing uit op de client waarop het ondersteunings centrum wordt uitgevoerd.

#### <a name="remote-connection"></a>Externe verbinding
Een externe verbinding met een andere Configuration Manager-client tot stand brengen. Nadat de verbinding tot stand is gebracht, verzamelt het ondersteunings centrum logboek bestanden en voert het probleem op te lossen op de client waarmee de verbinding is gemaakt.

#### <a name="about"></a>Over
Bevat informatie over het ondersteunings centrum.

#### <a name="options"></a>Opties
In het dialoog venster **Opties** kunt u het volgende doen:
- Verminder de verplaatsing van elementen van de gebruikers interface met animatie  
- De standaard opslaglocatie voor gegevens bundel bestanden wijzigen  
- De locatie van tijdelijke bestanden wijzigen    
- Waarschuwingen opnieuw instellen. Eventuele waarschuwings berichten die u eerder hebt onderdrukt, worden opnieuw weer gegeven wanneer de trigger wordt geactiveerd.  
- Het tijdelijke bestandspad opnieuw instellen op de standaard waarde, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Afsluiten
Sluit ondersteunings centrum.



### <a name="home-tab"></a><a name="bkmk_support-home"></a> Tabblad Start

#### <a name="collect-selected-data"></a>Geselecteerde gegevens verzamelen
Ondersteunings centrum verzamelt gegevens van de Configuration Manager-client. Standaard worden de volgende typen verzameld:
- Logboekbestanden
- Client configuratie verzamelaar
- Besturingssysteem

Als u andere typen gegevens wilt verzamelen, selecteert u het selectie vakje naast de naam van dat type.

Selecteer de vervolg keuzelijst onder aan de knop **geselecteerde gegevens verzamelen** in het lint en selecteer **alle gegevens verzamelen**. Met deze actie wordt de volledige set met client status gegevens verzameld.

Terwijl ondersteunings centrum gegevens verzamelt, selecteert u **verzameling annuleren** om deze te stoppen.

#### <a name="data-types"></a>Gegevenstypen
Wanneer u het selectie vakje voor een optie selecteert, verzamelt het ondersteunings centrum dat type gegevens de volgende keer dat u **geselecteerde gegevens verzamelen**selecteert. De volgende typen zijn beschikbaar:  

- **Logboek bestanden**: client-logboek bestanden, inclusief Setup-logboeken  

- **Beleid**: client beleids verzameling  

- **Certificaten**: informatie over de open bare sleutel voor client certificaten. Het ondersteunings centrum verzamelt geen persoonlijke sleutel van het certificaat.  

- **Client configuratie verzamelaar**: Configuration Manager-client gegevens. U kunt dit gegevens type niet uitschakelen.  

- **Client register**: verzamelt client configuratie gegevens uit het REGI ster. Ondersteunings centrum verzamelt alleen Configuration Manager register gegevens.  

- **Client-WMI**: client configuratie gegevens van WMI. Het ondersteunings centrum verzamelt geen client beleid.  

- **Problemen oplossen**: realtime-probleemoplossings gegevens om veelvoorkomende client problemen met Active Directory, beheer punten, netwerken, beleids toewijzingen en registratie te helpen vaststellen.  

    > [!NOTE]  
    > Dit gegevens type wordt niet ondersteund wanneer u een externe verbinding met een andere client maakt.  

- **Debug-dumps**: Voer debug dump van client en gerelateerde processen uit. De dump van de fout opsporing kan groot zijn. Schakel deze optie alleen in bij het oplossen van problemen met client prestaties.  

    > [!WARNING]  
    > Het verzamelen van dump bestanden voor fout opsporing zorgt ervoor dat gegevens bundels zeer groot worden (in sommige gevallen honderd MB).  
    >  
    > Debug dumps bevatten mogelijk gevoelige informatie, zoals wacht woorden, cryptografische geheimen of gebruikers gegevens. Dumps voor fout opsporing mogen alleen worden verzameld voor de aanbeveling van Microsoft Ondersteuning personeel. Gegevens bundels die dumps voor fout opsporing bevatten, moeten zorgvuldig worden verwerkt om ze te beschermen tegen onbevoegde toegang.  
    >  
    > Dit gegevens type wordt niet ondersteund wanneer u een externe verbinding met een andere client maakt.  

- **Besturings systeem**: verzamelt configuratie-informatie over de lokale machine. Deze gegevens bevatten informatie over de Windows-installatie, netwerk adapters en de configuratie van systeem services. U kunt dit gegevens type niet uitschakelen.  



### <a name="client-tab"></a><a name="bkmk_support-client"></a> Tabblad client

#### <a name="load-or-refresh"></a>Laden of vernieuwen
In ondersteunings centrum worden Details voor de Configuration Manager-client geladen of vernieuwd.

#### <a name="control-client-agent-service"></a>Client Agent-service beheren
Voer een van de volgende acties uit op de Configuration Manager client agent-service (ccmexec) op de verbonden client:  

- **Client opnieuw starten**  

    > [!IMPORTANT]  
    > Als de client agent-service niet correct opnieuw wordt gestart, kan de client niet worden beheerd door Configuration Manager totdat de service wordt gestart.  

- **Client starten**  

- **Client stoppen**  

    > [!IMPORTANT]  
    > De client kan niet worden beheerd door Configuration Manager totdat de service wordt gestart.  

#### <a name="properties"></a>Eigenschappen
Wanneer u client Details laadt, worden in ondersteunings centrum de volgende eigenschappen weer gegeven:  

- **Client-id**: een unieke id die Configuration Manager gebruikt om de client te identificeren  

- **Hardware-id**: een unieke id die Configuration Manager gebruikt voor het identificeren van de client-hardware  

- **Goedgekeurd**: geeft aan of de client is goedgekeurd in Configuration Manager  

- **Registratie status**: geeft aan of de client is geregistreerd bij Configuration Manager  

- **Internet gerichte**: geeft aan of de client op internet is  

- **Versie**: het versie nummer van de geïnstalleerde Configuration Manager-client  

- **Site code**: de site code voor de primaire site waaraan de client is toegewezen  

- **Toegewezen MP**: de Fully QUALIFIED domain name (FQDN) van het momenteel toegewezen beheer punt van de client  

- **Residente MP**: de FQDN van het residente beheer punt  

- **Proxy-MP**: de HOSTNAAM of FQDN van het proxy beheer punt (indien aanwezig)  

- **Proxy site code**: de site code voor de secundaire site (indien aanwezig)  

- **Proxy status**: de status van het proxy beheer punt van de Configuration Manager-client. Bijvoorbeeld **actief** of **in behandeling**.  



### <a name="policy-tab"></a><a name="bkmk_support-policy"></a> Tabblad beleid

Gebruik de acties op dit tabblad in plaats van het oudere [PolicySpy](policy-spy.md) -hulp programma.

#### <a name="load-policy"></a>Beleid laden
Deze optie is afhankelijk van de weer gave:

- **Werkelijke waarde van het beleid laden**: Selecteer **werkelijk** in de weergave groep en selecteer deze optie in de beleids groep. Het ondersteunings centrum laadt het client beleid dat u momenteel hebt geselecteerd.  

- **Aangevraagde beleid laden**: Selecteer **aangevraagd** in de weergave groep en selecteer deze optie in de beleids groep. Ondersteunings centrum laadt het aangevraagde client beleid van de client.  

- **Standaard beleid laden**: Selecteer **standaard** in de weer gave groep en selecteer deze optie in de beleids groep. Ondersteunings centrum laadt het standaard beleid voor deze client.  

Selecteer de vervolg keuzelijst onder aan deze knop voor extra opties:

- **Laden of vernieuwen alles**: Hiermee wordt het werkelijke, gevraagde en standaard beleid op hetzelfde moment geladen of vernieuwd.  

#### <a name="actual-view"></a>Werkelijke weer gave
Hiermee opent u de werkelijke beleids weergave

#### <a name="requested-view"></a>Aangevraagde weer gave
Hiermee opent u de aangevraagde beleids weergave

#### <a name="default-view"></a>Standaard weergave
Hiermee opent u de standaard beleids weergave. (Dit beleid is welke apparaten worden ontvangen wanneer u de Configuration Manager-client installeert.)

#### <a name="request-and-evaluate-policy"></a>Beleid aanvragen en evalueren
Het ondersteunings centrum vraagt het client beleid aan bij het beheer punt en evalueert dat beleid op de client.

Selecteer de vervolg keuzelijst onder aan deze knop voor extra opties:  

- **Aanvraag beleid**: het ondersteunings centrum vraagt het client beleid aan bij het beheer punt.  

- **Beleid evalueren**: ondersteunings centrum evalueert het client beleid op de client.  

- **Beleid opnieuw instellen op standaard waarden**: ondersteunings centrum vertelt de Configuration Manager-client om het standaard beleid opnieuw toe te passen. Hiermee verwijdert u alle computer-en gebruikers beleid op de client.  

#### <a name="listen-for-policy-events"></a>Luis teren naar beleids gebeurtenissen
Ondersteunings centrum luistert naar beleids gebeurtenissen. Selecteer deze optie opnieuw om het Luis teren naar beleids gebeurtenissen uit te scha kelen. Selecteer de pijl onder aan dit tabblad om **beleids gebeurtenissen**weer te geven. 

#### <a name="clear-events"></a>Gebeurtenissen wissen
In het ondersteunings centrum worden alle beleids gebeurtenissen gewist.



### <a name="content-tab"></a><a name="bkmk_support-content"></a> Tabblad inhoud

Inhoud op de client weer geven, met inbegrip van inhoud in de cache. Bewaak de voortgang van software-update-en toepassings implementaties. 

#### <a name="load-or-refresh"></a>Laden of vernieuwen
*Is van toepassing op de inhoud en cache weergaven*

In het ondersteunings centrum wordt de lijst met inhoud die momenteel op de client staat, geladen of vernieuwd.

#### <a name="invoke-trigger"></a>Trigger activeren
Met de volgende items in dit menu kunt u een client actie aanvragen met betrekking tot inhoud:  

- **Locatie Services**  

    - **Inhouds locaties vernieuwen**: Hiermee vernieuwt u de distributie punten die worden gebruikt door actieve inhouds downloads.  

    - **Beheer punten vernieuwen**: werkt de interne lijst bij van beheer punten die door de client worden gebruikt.  

    - **Time-outaanvragen voor inhoud**: als de aanvragen voor de inhouds locatie te lang zijn uitgevoerd, wordt de aanvraag door deze actie gestopt.  

- **Evaluatie**van de implementatie van de toepassing: Hiermee wordt een taak gestart waarmee geïmplementeerde toepassingen worden geëvalueerd.  

- **Evaluatie**van de implementatie van software-updates: Hiermee wordt een taak gestart waarmee geïmplementeerde software-updates worden geëvalueerd.  

- **Bron scan voor software-updates**: Hiermee wordt een taak gestart die de bron locaties voor updates scant.  

- **Windows Installer update van de bron lijst**: Hiermee wordt een taak gestart die de bron locatie voor Windows Installer (MSI)-installaties bijwerkt.  

#### <a name="content-view"></a>Inhouds weergave
Bekijk toepassingen, pakketten en updates die zijn geladen op de client. Wanneer u een toepassing, pakket of update selecteert, kunt u de details van die inhoud weer geven. Voor sommige toepassingen kunt u ook de volgende acties uitvoeren:  

- **Vernieuwen**: de weer gave Details vernieuwen  

- **Controleren of downloaden**: controleren of een toepassing beschikbaar is voor downloaden  

- **Installeren**: de toepassing installeren  

- **Verwijderen**: de toepassing verwijderen  

#### <a name="cache-view"></a>Cache weergave
De configuratie van de client cache en Details over de cache-inhoud weer geven. Wanneer u het ondersteunings centrum verbindt met een lokale client, voert u ook de volgende acties uit:  

- Selecteer **wijzigen** naast het veld **cache locatie** om de cache locatie te wijzigen.  

- Selecteer **wijzigen** naast het veld **cache grootte** om de grootte van de cache aan te passen.  

- Selecteer **wissen** naast het veld **cache in gebruik** om de client cache te wissen.  

In deze weer gave worden de volgende eigenschappen weer gegeven:  

- **Locatie**: de locatie van elke cachemap. Selecteer de koppeling om de map te openen in Windows Verkenner.   
- **Inhoud-ID**  
- **Cache-ID**  
- **Grootte**  
- **Laatst verwezen**: deze eigenschap is de datum waarop de client de laatste keer heeft gelezen van of geschreven naar dit item in de cache.  

#### <a name="monitoring-view"></a>Bewakings weergave
Selecteer **monitor** om de actieve voortgang van software-update-en toepassings update-implementaties weer te geven. In deze weer gave worden status berichten weer gegeven die van toepassing zijn op gebeurtenis-en software-updates Event WMI-berichten.

Voor elke gebeurtenis worden de volgende eigenschappen weer gegeven:  

- **Tijd**: de tijd waarop de client de gebeurtenis heeft gegenereerd  
- **Type onderwerp**: het status bericht type  
- **Onderwerp-id**: id van het status bericht dat wordt gebruikt om toe te wijzen aan gebeurtenissen in logboek bestanden  
- **Onderwerp-ID type**: het subtype van het status bericht  
- **Status-ID**: het resultaat van de actie die u wilt bewaken  
- **Details** en **gebeurtenis gegevens**: meer informatie over de status berichten die in deze weer gave worden weer gegeven. De status gegevens kunnen soms leeg zijn.  



### <a name="inventory-tab"></a><a name="bkmk_support-inventory"></a> Tabblad voor Raad

#### <a name="load-or-refresh"></a>Laden of vernieuwen
Ondersteunings centrum laadt of vernieuwt de client inventarisatie lijst voor de momenteel geselecteerde weer gave.

#### <a name="invoke-trigger"></a>Trigger activeren

> [!Note]  
> Voor andere taken dan de **rapport cyclus voor software licentie controle**:  
> - Als u de taak aanvraagt wanneer er al een andere inventarisatie taak wordt uitgevoerd, wacht de client de nieuwe taak die wordt uitgevoerd nadat de huidige taak en andere taken in de wachtrij zijn voltooid.  
> - De voortgang van de taak in **InventoryAgent. log**volgen.  

De volgende items in dit menu aanvragen client actie gerelateerd aan de inventarisatie:  

- **Verzamel fase detectie gegevens (heartbeat)**: Hiermee wordt de client taak geactiveerd die wordt gebruikt voor het verzamelen van detectie gegevens van apparaten  

- **Verzamel fase bestanden**: de client taak die wordt gebruikt voor het verzamelen van lokale bestanden wordt geactiveerd  

- **Hardware-inventarisatie fase**: activeert de client taak die wordt gebruikt voor het verzamelen van hardware-inventaris gegevens  

- **IDMIF-verzamelings cyclus**: activeert de client taak die wordt gebruikt voor het verzamelen van IDMIF-gegevens  

- **Software-inventarisatie fase**: activeert de client taak die wordt gebruikt voor het verzamelen van software-inventaris gegevens  

- **Rapport cyclus voor software licentie controle**: activeert de client taak die wordt gebruikt om een software licentie controle rapport samen te stellen en te verzenden naar het beheer punt. Volg de voortgang van deze taak in **SWMTRReportGen. log**.

- Niet- **verzonden status berichten verzenden in wachtrij**: activeert de client taak voor het leegmaken van de wachtrij met status berichten.

- **Geavanceerd**  
    - **Hardware-inventarisatie fase (volledige hersynchronisatie)**  
    - **Software-inventarisatie cyclus (volledige hersynchronisatie)**  


#### <a name="views"></a>Weergaven
Als een functie niet is ingeschakeld, worden in de weer gave geen gegevens weer gegeven. 

- **Status**: de inventarisatie gegevens sets weer geven die de client heeft verzameld  

- **DDR**: informatie over de client detectie gegevens die van de client zijn verzameld  

- **HINV**: informatie over de hardware-inventarisatie gegevens die van de client zijn verzameld  

- **SINV**: informatie over de software-inventarisatie gegevens die van de client zijn verzameld  

- **Bestands verzameling**: informatie over de bestanden die van de client zijn verzameld  

- **IDMIF**: informatie over de IDMIF-en NOIDMIF-gegevens die van de client zijn verzameld  

- **Meting**: informatie over de software licentie controle gegevens die zijn verzameld van de client  



### <a name="troubleshooting-tab"></a><a name="bkmk_support-troubleshoot"></a> Tabblad probleem oplossing

Los enkele van de meest voorkomende problemen met Configuration Manager-clients op:  
- Problemen met Active Directory  
- Windows-netwerken  
- Configuration Manager   
    - Beheer punten  
    - Beleidstoewijzing  
    - Registratie  


> [!NOTE]  
> Dit tabblad is niet beschikbaar wanneer u verbinding maakt met een externe Configuration Manager-client.


#### <a name="start"></a>Starten
Hiermee wordt het oplossen van problemen met de client gestart

- **Active Directory**: query's Active Directory om gepubliceerde Configuration Manager-site gegevens op te halen  
- **MPCERTIFICATE**: Hiermee worden beheer punt certificaten opgehaald  
- **MPLIST**: Hiermee wordt een lijst met beheer punten opgehaald  
- **MPKEYINFORMATION**: Hiermee wordt informatie over de cryptografische sleutel van het beheer punt opgehaald  
- **Netwerken**: problemen met netwerken oplossen  
- **Beleids toewijzingen**: Hiermee worden beleids toewijzingen opgehaald  
- **Registratie**: controleert of de client is geregistreerd bij de site  

#### <a name="view-selected-log"></a>Geselecteerd logboek weer geven
Nadat u een rij op het tabblad probleem oplossing hebt geselecteerd, selecteert u deze actie om het logboek bestand weer te geven.

#### <a name="keep-previous-results"></a>Eerdere resultaten blijven
Als u de client problemen oplost en vervolgens opnieuw wilt proberen om het probleem op te lossen, kiest u deze optie om de resultaten van uw eerste poging te bewaren. Als dat niet het geval is, overschrijft het ondersteunings centrum vorige logboek bestanden voor probleem oplossing.



### <a name="logs-tab"></a><a name="bkmk_support-logs"></a> Tabblad logboeken

In deze sectie vindt u de items op het tabblad **Logboeken** van het hulp programma ondersteunings centrum. 

Dit tabblad is bijna identiek aan de **log viewer** -tool. Het hulp programma voor **logboek weergave** bevat geen functies voor het **configureren van client logboek registratie** en **logboek groepen** die in deze sectie worden beschreven. In het [ondersteunings centrum voor logboeken wordt](#bkmk_log-viewer) een overzicht van de andere beschik bare opties op dit tabblad beschreven.

#### <a name="configure-client-logging"></a>Client logboek registratie configureren

Stel de volgende opties in: 
- **Client logboek niveau**: uitgebreid logboek bestand en bestands grootte  
- **Maximum aantal bestanden**: meerdere logboek bestanden van een bepaald type toestaan  
- **Maximale bestands grootte**: de grootte in bytes van een gegeven logboek bestand voordat de client een nieuw logboek maakt  

> [!NOTE]  
> Als u deze waarden te laag instelt, kan de client geen bruikbare informatie in het logboek registreren. Als u deze waarden te hoog instelt, kunnen de client logboeken grote hoeveel heden opslag ruimte gebruiken.  

#### <a name="log-groups"></a>Logboek groepen

In plaats van hand matig logboek bestanden te selecteren met behulp van de knop **Logboeken openen** , gebruikt u deze vervolg keuzelijst om alle logboek bestanden te openen die zijn gekoppeld aan de volgende onderdelen gebieden: 
- **Gewenst configuratie beheer**
- **Inventaris**
- **Software distributie**
- **Software-updates**
- **Toepassings beheer**
- **Beleid**
- **Client registratie**
- **Implementatie van besturingssystemen**


## <a name="support-center-log-viewer-reference"></a><a name="bkmk_log-viewer"></a> Naslag informatie over Logboeken in ondersteunings centrum

In deze sectie wordt de gebruikers interface voor het hulp programma voor **logboek weergave van ondersteunings centrum** beschreven. 

- [Venster menu](#bkmk_log-window)  
- [Tabblad Start](#bkmk_log-home)  

Het hulp programma **logboeken viewer** is bijna identiek aan het tabblad **Logboeken** van het **ondersteunings centrum**. Het hulp programma voor **logboek weergave** bevat geen opties voor het **configureren van client logboek registratie** en **logboek groepen**.


### <a name="window-menu"></a><a name="bkmk_log-window"></a> Venster menu

Selecteer in de linkerbovenhoek van het venster met de logboek weergave van de ondersteunings centrum de pijl in het blauwe vak om dit menu te openen.

#### <a name="open-logs"></a>Logboeken openen
Blader naar de locatie van de logboek bestanden die u wilt openen. 

#### <a name="options"></a>Opties
In het dialoog venster **Opties** kunt u het volgende doen:
- Verminder de verplaatsing van elementen van de gebruikers interface met animatie  
- Log viewer registreren als de standaard-app voor logboek bestanden met de bestands extensies. log en. lo_  
- Waarschuwingen opnieuw instellen. Eventuele waarschuwings berichten die u eerder hebt onderdrukt, worden opnieuw weer gegeven wanneer de trigger wordt geactiveerd.  

#### <a name="about"></a>Over
Geeft informatie weer over de logboek weergave van ondersteunings centrum

#### <a name="close"></a>Sluiten
Hiermee sluit u de logboek viewer van ondersteunings centrum


### <a name="home-tab"></a><a name="bkmk_log-home"></a> Tabblad Start

#### <a name="open-logs"></a>Logboeken openen 
In het ondersteunings centrum wordt u gevraagd om een of meer logboek bestanden te selecteren die u wilt openen.

Selecteer de vervolg keuzelijst onder aan de knop **Logboeken openen** in het lint en selecteer een van de volgende extra opties: 
- **Logboeken openen in huidige weer gave**: Hiermee opent u de geselecteerde logboek bestanden in de huidige weer gave  
- **Logboeken openen in nieuw venster**: Hiermee opent u de geselecteerde logboek bestanden in een nieuw venster van de **logboeken viewer**  

#### <a name="close-and-clear-logs"></a>Logboeken sluiten en wissen
Hiermee sluit u alle geopende logboek bestanden. Hiermee worden ook alle weer gegeven logboek vermeldingen uit het venster gewist. Deze vermeldingen worden in de toekomst niet meer weer gegeven in het ondersteunings centrum.

Selecteer de vervolg keuzelijst onder aan de knop **logs sluiten en logboeken wissen** in het lint en selecteer een van de volgende extra opties: 
- **Alle vermeldingen wissen**: Hiermee wist u de vermeldingen in het logboek bestand uit het venster. Deze vermeldingen worden in de toekomst niet meer weer gegeven in het ondersteunings centrum.  
- **Alle logboeken sluiten**: Hiermee sluit u alle geopende logboek bestanden  

#### <a name="find"></a>Find
Hiermee opent u het dialoog venster **zoeken** . Geef een teken reeks op waarnaar u wilt zoeken. Om te voor komen dat er wordt gezocht op korte teken reeksen in andere teken reeksen, kunt u ervoor kiezen om te zoeken naar hele woorden. U kunt er ook voor kiezen om een hoofdletter gevoelige overeenkomst voor de teken reeks uit te voeren.

#### <a name="find-next"></a>Volgende zoeken
Wanneer u een overeenkomst hebt gevonden voor de teken reeks die u zoekt, gaat u met deze optie naar de volgende overeenkomst.

#### <a name="find-previous"></a>Vorige zoeken
Wanneer u twee of meer overeenkomsten hebt gevonden voor de teken reeks die u zoekt, gaat u met deze optie naar de vorige overeenkomst.

#### <a name="options"></a>Opties

- **Live bijwerken**: een logboek bestand dat momenteel is geopend controleren op wijzigingen. Deze functie werkt niet wanneer er meerdere logboek bestanden zijn geopend. Deze optie is standaard ingeschakeld.  

- **Automatisch schuiven**: als u ook de optie **Live-Update** hebt gekozen, schuift deze optie automatisch door de weer gave logboek om nieuwe vermeldingen weer te geven. Deze functie werkt niet wanneer er meerdere logboek bestanden zijn geopend. Deze optie is standaard ingeschakeld.  

- **Details weer geven**: wanneer u een bericht van een logboek bestand selecteert, worden in het tabblad **Logboeken** de details van het bericht van het logboek bestand weer gegeven. Deze optie is standaard ingeschakeld.  

- **Snelfilter**: de berichten van het logboek bestand filteren op alle geopende logboek bestanden om een specifieke teken reeks te zoeken. U kunt filteren op logboek tekst, onderdeel naam en thread-ID. Als u vergelijk bare logboek berichten wilt zoeken, klikt u met de rechter muisknop op een logboek bericht en selecteert u **snel filter** op logboek tekst.  

- **Tekst terugloop logboek**: lange en meerdere regels berichten laten teruglopen in één kolom. Dit gedrag zorgt ervoor dat deze berichten gemakkelijker te lezen zijn. Deze optie is standaard ingeschakeld.  

- **Weer gave onbewerkte logboek vermelding**: geeft niet-verwerkte logboek regels weer.  

- **Geavanceerde filters**: Open het dialoog venster **Geavanceerde filters** . Zie [Geavanceerde logboek bestand filters](#bkmk_adv-filters)voor meer informatie.  

- **Fout code koppelingen**: fout codes in logboek tekst zijn gemarkeerd en klikbaar. Deze optie is standaard ingeschakeld.  

#### <a name="error-lookup"></a>Fout bij zoeken
Voer een fout code in om te zoeken naar de fout code in de logboek bestanden die momenteel zijn geopend. Gebruik de volgende fout code notaties:
- **32-bits geheel getal (ondertekend)**: bijvoorbeeld `-2147024891`  
- **32-bits geheel getal (niet-ondertekend)**: bijvoorbeeld `2147942405`  
- **32-bits hexadecimaal**: bijvoorbeeld `0x80070005`  

#### <a name="decode-certificate"></a>Certificaat decoderen
Plak in het dialoog venster **certificaat decoderen** de geserialiseerde certificaat waarde voor een certificaat op de client. Zoek deze waarde in het REGI ster, in logboek bestanden of in WMI. Selecteer **proces** om algemene informatie en Details over het certificaat weer te geven. Deze informatie omvat het certificeringspad. Selecteer **exporteren** om het certificaat te exporteren als een **. CER** -bestand.



## <a name="advanced-log-file-filters"></a><a name="bkmk_adv-filters"></a> Geavanceerde filters voor logboek bestanden

Met geavanceerde filters voor logboek bestanden kunt u specifieke teken reeksen opnemen, uitsluiten of markeren. Deze teken reeksen kunnen zich voordoen in een logboek bestand of logboek bestand groep bij het zoeken naar logboek bestand vermeldingen. Zoek opdrachten met Joker tekens gebruiken bij het maken van een filter. Wanneer u een handige combi natie van filters hebt, slaat u ze op als een *Filterset*. 

Geavanceerde filters voor logboek bestanden vervangen snelle filters. Beide tegelijk gebruiken, maar snelle filters zijn alleen van toepassing op de weer gegeven logboek gegevens. Geavanceerde filters bepalen welke gegevens in eerste instantie worden weer gegeven voordat een snelle filters worden toegepast.

In het dialoog venster Geavanceerde filters kunt u complexe filter sets maken. Deze filter sets zoeken naar teken reeksen in veel logboek bestand onderdelen. Deze onderdelen zijn onder andere berichten, threads, logboek registratie niveaus en onderdelen. Een Filterset bevat meerdere filter instructies die u gebruikt om logboek bestand berichten op te nemen, uit te sluiten of te markeren. Een filter definieert een kolom van een logboek bestand om te zoeken in, een operator en een waarde. De waarde kan reguliere expressies bevatten, zoals het *Joker* teken `*` .


### <a name="add-a-filter"></a>Een filter toevoegen

1. In het venster van de **logboeken viewer** of op het tabblad **Logboeken** van het ondersteunings centrum selecteert u **Geavanceerde filters**.  

2. Selecteer in het dialoog venster Geavanceerde filters de optie **toevoegen**. Selecteer vervolgens een van de volgende opties om te reageren op logboek vermeldingen die overeenkomen met uw filter:  
    - **Opnemen**  
    - **Weekend**  
    - **Markeren**  

3. Kies in het dialoog venster **Geavanceerde filter configuratie** een kolom en een operator:  

    - **Kolom**: Kies waar u wilt zoeken naar teken reeksen die overeenkomen met uw filter:  

         - **Logboek tekst**: zoeken in de tekst van een logboek bestand  

         - **Ernst**van het logboek: zoek naar Logboeken met een specifiek Ernst niveau. Stel deze Ernst niveaus in het veld **waarde** in.  

         - **Onderdeel**: zoeken naar een specifiek onderdeel op naam  

         - **Thread-id**: zoeken naar logboek berichten met een specifieke thread-id  

         - **Bron bestand**: zoeken naar logboek berichten die in een specifiek logboek bestand plaatsvinden  

    - **Operator**: Kies een operator voor uw filter  

4. Voer in het veld **waarde** een waarde in waarop u wilt filteren. Als uw waarde reguliere expressies bevat, selecteert u **reguliere expressie-overeenkomsten inschakelen**.  


### <a name="manage-filter-sets"></a>Filter sets beheren

- Als u een filter wilt bewerken, selecteert u het filter en selecteert u vervolgens **bewerken**.  

- Als u een filter wilt verwijderen, selecteert u het filter en selecteert u vervolgens **verwijderen**.  

- Als u alle filters wilt wissen, selecteert u **wissen**.  

- Selecteer **filters opslaan**om de huidige Filterset op te slaan. Sla vervolgens de Filterset op als een **. Filterset** -bestand.  

- Selecteer **filters laden**om een opgeslagen Filterset te laden. Ga vervolgens naar een eerder opgeslagen **. Filterset** -bestand.  



## <a name="support-center-viewer-reference"></a><a name="bkmk_viewer"></a> Naslag informatie over ondersteunings centrum

In deze sectie wordt de gebruikers interface (UI) voor het Viewer hulpprogramma van het Configuration Manager- **ondersteunings centrum** beschreven. De beschik bare tabbladen variëren op basis van de inhoud van de bundel probleem oplossing. Het [menu venster](#bkmk_viewer-window) en het [tabblad Start](#bkmk_viewer-home) worden standaard weer gegeven.
- [Venster menu](#bkmk_viewer-window)
- [Tabblad Start](#bkmk_viewer-home)
- [Tabblad Configuratie](#bkmk_viewer-config)
- [Tabblad logboeken](#bkmk_viewer-logs)
- [Tabblad debug dumps](#bkmk_viewer-debug)
- [Tabblad WMI](#bkmk_viewer-wmi)
- [Tabblad REGI ster](#bkmk_viewer-registry)
- [Tabblad beleid](#bkmk_viewer-policy)
- [Tabblad Certificaten](#bkmk_viewer-certs)
- [Tabblad probleem oplossing](#bkmk_viewer-troubleshoot)


### <a name="window-menu"></a><a name="bkmk_viewer-window"></a> Venster menu

Selecteer in de linkerbovenhoek van het viewer venster van de ondersteunings centrum de pijl in het blauwe vak om dit menu te openen.

#### <a name="open-bundle"></a>Bundel openen
Blader naar de locatie van een gegevens bundel die is gemaakt met het ondersteunings centrum.

#### <a name="about"></a>Over
Geeft informatie weer over de viewer van ondersteunings centrum.

#### <a name="options"></a>Opties
In het dialoog venster **Opties** kunt u het volgende doen:
- Verminder de verplaatsing van elementen van de gebruikers interface met animatie  
- De locatie van tijdelijke bestanden wijzigen    
- Waarschuwingen opnieuw instellen. Eventuele waarschuwings berichten die u eerder hebt onderdrukt, worden opnieuw weer gegeven wanneer de trigger wordt geactiveerd.  
- Het tijdelijke bestandspad opnieuw instellen op de standaard waarde, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Afsluiten
Viewer voor ondersteunings centrum afsluiten


### <a name="home-tab"></a><a name="bkmk_viewer-home"></a> Tabblad Start

#### <a name="open-bundle"></a>Bundel openen
Blader naar de locatie van een gegevens bundel die is gemaakt met het ondersteunings centrum.

#### <a name="open-log-file"></a>Logboek bestand openen
Selecteer een of meer logboek bestanden om te openen.

#### <a name="decode-certificate"></a>Certificaat decoderen
Plak in het dialoog venster **certificaat decoderen** de geserialiseerde certificaat waarde voor een certificaat op de client. Zoek deze waarde in het REGI ster, in logboek bestanden of in WMI. Selecteer **proces** om algemene informatie en Details over het certificaat weer te geven. Deze informatie omvat het certificeringspad. Selecteer **exporteren** om het certificaat te exporteren als een **. CER** -bestand.


### <a name="configuration-tab"></a><a name="bkmk_viewer-config"></a> Tabblad Configuratie

Het tabblad **configuratie** van het hulp programma ondersteunings centrum biedt de volgende weer gaven met behulp van gegevens die zijn opgehaald van de WMI-providers:

#### <a name="client"></a>Client
In deze weer gave wordt dezelfde informatie weer gegeven op het tabblad **client** van het ondersteunings centrum.

#### <a name="operating-system"></a>Besturingssysteem
Details van het besturings systeem van de client. Er wordt gebruikgemaakt van de [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem) -klasse.

#### <a name="computer"></a>Computer
Details voor de client computer. Er wordt gebruikgemaakt van de [Win32_OperatingSystem](/windows/desktop/CIMWin32Prov/win32-operatingsystem) -klasse.

#### <a name="services"></a>Services
Details voor services die worden uitgevoerd op de client computer. Er wordt gebruikgemaakt van de [Win32_Service](/windows/desktop/CIMWin32Prov/win32-service) -klasse.

#### <a name="network-adapters"></a>Netwerkadapters
Details voor netwerk adapters die zijn geïnstalleerd op de client computer. Er wordt gebruikgemaakt van de [Win32_NetworkAdapterConfiguration](/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration) -klasse.


### <a name="logs-tab"></a><a name="bkmk_viewer-logs"></a> Tabblad logboeken

Op het tabblad **Logboeken** ziet u een lijst van de logboek bestanden die in de bundel zijn opgenomen. Elke rij op dit tabblad bevat het pad, de naam en de grootte van het logboek bestand. 

#### <a name="open"></a>Open
Klik na het selecteren van een logboek bestand op deze knop om **Logboeken**te openen. Het bevat een subset van de functionaliteit die wordt weer gegeven op het tabblad logboeken van het ondersteunings centrum.

#### <a name="decode-certificate"></a>Certificaat decoderen
Plak in het dialoog venster **certificaat decoderen** de geserialiseerde certificaat waarde voor een certificaat op de client. Zoek deze waarde in het REGI ster, in logboek bestanden of in WMI. Selecteer **proces** om algemene informatie en Details over het certificaat weer te geven. Deze informatie omvat het certificeringspad. Selecteer **exporteren** om het certificaat te exporteren als een **. CER** -bestand.


### <a name="debug-dumps-tab"></a><a name="bkmk_viewer-debug"></a> Tabblad debug dumps

Elke rij op dit tabblad bevat details over de dump bestanden voor fout opsporing die kunnen worden geëxporteerd. Op dit tabblad kunt u dump bestanden voor fout opsporing (. dmp) exporteren voor verdere analyse. Deze analyse maakt gebruik van een hulp programma voor fout opsporing, zoals WinDbg. 

> [!WARNING]  
> Debug-dumps kunnen gevoelige informatie bevatten, waaronder wacht woorden, cryptografische geheimen of gebruikers gegevens. Verzamel alleen debug-dumps op aanbeveling van Microsoft Ondersteuning personeel. Gegevens bundels die dumps voor fout opsporing bevatten, moeten zorgvuldig worden verwerkt om ze te beschermen tegen onbevoegde toegang.  

#### <a name="export"></a>Exporteren
Sla een kopie op van het geselecteerde dump bestand voor fout opsporing.


### <a name="wmi-tab"></a><a name="bkmk_viewer-wmi"></a> Tabblad WMI

Dit tabblad bevat de set WMI-gegevens van de Configuration Manager-client die de gegevens bundel bevat. 

#### <a name="find"></a>Find
Hiermee opent u het dialoog venster zoeken, met de volgende functies:  

- **Zoek naar: Geef**een teken reeks op waarnaar u wilt zoeken in de WMI-gegevensset. Joker tekens worden ondersteund.  

- **Kijken**naar: Kies of u wilt zoeken in de WMI-gegevensset voor een overeenkomende **klasse-of exemplaar naam**, **eigenschap**of **waarde**.  

- **Hele teken reeks**: standaard zoekt het dialoog venster zoeken naar teken reeksen die de teken reeks bevatten waarnaar u op zoek bent. Kies dit selectie vakje om alleen teken reeksen te vinden die exact overeenkomen met de teken reeks die u hebt opgegeven.  

#### <a name="find-next"></a>Volgende zoeken
Met deze knop opent u het volgende exemplaar van de teken reeks die u hebt opgegeven in het dialoog venster zoeken in de WMI-gegevensset.

#### <a name="decode-certificate"></a>Certificaat decoderen
Plak in het dialoog venster **certificaat decoderen** de geserialiseerde certificaat waarde voor een certificaat op de client. Zoek deze waarde in het REGI ster, in logboek bestanden of in WMI. Selecteer **proces** om algemene informatie en Details over het certificaat weer te geven. Deze informatie omvat het certificeringspad. Selecteer **exporteren** om het certificaat te exporteren als een **. CER** -bestand.


### <a name="registry-tab"></a><a name="bkmk_viewer-registry"></a> Tabblad REGI ster

Gebruik het tabblad **REGI ster** om register gegevens weer te geven die zijn opgenomen in de gegevens bundel en om die gegevens te exporteren voor verdere analyse.

#### <a name="export"></a>Exporteren
Sla een kopie van de register sleutel en subsleutels op die u als een register bestand (. reg) selecteert.

#### <a name="find"></a>Find
Hiermee opent u het dialoog venster zoeken, met de volgende functies:  

- **Zoek naar: Geef**een teken reeks op waarnaar u wilt zoeken in de WMI-gegevensset. Joker tekens worden ondersteund.  

- **Kijken**naar: Kies of u wilt zoeken in de WMI-gegevensset voor een overeenkomende **klasse-of exemplaar naam**, **eigenschap**of **waarde**.  

- **Hele teken reeks**: standaard zoekt het dialoog venster zoeken naar teken reeksen die de teken reeks bevatten waarnaar u op zoek bent. Kies dit selectie vakje om alleen teken reeksen te vinden die exact overeenkomen met de teken reeks die u hebt opgegeven.  

#### <a name="find-next"></a>Volgende zoeken
Met deze knop opent u het volgende exemplaar van de teken reeks die u hebt opgegeven in het dialoog venster zoeken in de WMI-gegevensset.

#### <a name="decode-certificate"></a>Certificaat decoderen
Plak in het dialoog venster **certificaat decoderen** de geserialiseerde certificaat waarde voor een certificaat op de client. Zoek deze waarde in het REGI ster, in logboek bestanden of in WMI. Selecteer **proces** om algemene informatie en Details over het certificaat weer te geven. Deze informatie omvat het certificeringspad. Selecteer **exporteren** om het certificaat te exporteren als een **. CER** -bestand.


### <a name="policy-tab"></a><a name="bkmk_viewer-policy"></a> Tabblad beleid

Het tabblad **beleid** wordt gebruikt voor het weer geven van beleids gegevens die zijn opgenomen in de gegevens bundel. 

#### <a name="find"></a>Find
Hiermee opent u het dialoog venster zoeken, met de volgende functies:  

- **Zoek naar: Geef**een teken reeks op waarnaar u wilt zoeken in de WMI-gegevensset. Joker tekens worden ondersteund.  

- **Kijken**naar: Kies of u wilt zoeken in de WMI-gegevensset voor een overeenkomende **klasse-of exemplaar naam**, **eigenschap**of **waarde**.  

- **Hele teken reeks**: standaard zoekt het dialoog venster zoeken naar teken reeksen die de teken reeks bevatten waarnaar u op zoek bent. Kies dit selectie vakje om alleen teken reeksen te vinden die exact overeenkomen met de teken reeks die u hebt opgegeven.  

#### <a name="find-next"></a>Volgende zoeken
Met deze knop opent u het volgende exemplaar van de teken reeks die u hebt opgegeven in het dialoog venster zoeken in de WMI-gegevensset.

#### <a name="decode-certificate"></a>Certificaat decoderen
Plak in het dialoog venster **certificaat decoderen** de geserialiseerde certificaat waarde voor een certificaat op de client. Zoek deze waarde in het REGI ster, in logboek bestanden of in WMI. Selecteer **proces** om algemene informatie en Details over het certificaat weer te geven. Deze informatie omvat het certificeringspad. Selecteer **exporteren** om het certificaat te exporteren als een **. CER** -bestand.


### <a name="certificates-tab"></a><a name="bkmk_viewer-certs"></a> Tabblad Certificaten

Het tabblad **certificaten** wordt gebruikt voor het weer geven van certificaten die zijn opgenomen in de gegevens bundel en om deze te exporteren.

#### <a name="view-certificate"></a>Certificaat weer geven
Geeft informatie weer over een geselecteerd certificaat.

#### <a name="export"></a>Exporteren
Hiermee opent u een dialoog venster **Opslaan als** om een kopie op te slaan van het certificaat dat u selecteert.


### <a name="troubleshooting-tab"></a><a name="bkmk_viewer-troubleshoot"></a> Tabblad probleem oplossing

Gebruik het tabblad **probleem oplossing** om de logboek bestanden weer te geven die zijn gemaakt met het tabblad probleem oplossing van het ondersteunings centrum.

#### <a name="view-log"></a>Logboek weer geven
Nadat u een rij op het tabblad **probleem oplossing** hebt geselecteerd, selecteert u deze optie om het logboek bestand met log viewer weer te geven.