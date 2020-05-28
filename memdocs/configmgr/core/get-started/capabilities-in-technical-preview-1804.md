---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Meer informatie over nieuwe functies die beschikbaar zijn in de Configuration Manager Technical Preview versie 1804.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b709d6ec0c0cda188502c314d945a70e8de71288
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905256"
---
# <a name="capabilities-in-technical-preview-1804-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1804 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1804. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Technical Preview-site. 

Raadpleeg het artikel [Technical Preview](technical-preview.md) voordat u deze update installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Bekende problemen in deze Technical Preview

### <a name="setup-link-to-download-updates-not-working"></a><a name="bkmk_ki-prereqs"></a>Installatie koppeling voor het downloaden van updates werkt niet
<!--514334-->
Als u Setup vanaf het medium uitvoert, bevat de eerste pagina een koppeling met **de titel down load de meest recente Configuration Manager updates**, die niet in deze release werken. Deze koppeling is voor het downloaden van de vereiste bestanden voor Setup.

#### <a name="workaround"></a>Tijdelijke oplossing
Als u de vereiste bestanden voor de installatie wilt downloaden, voert u de wizard Setup uit. Gebruik op de pagina vereiste down loads de optie voor het downloaden van de **vereiste bestanden**. 


### <a name="the-application-catalog-web-service-point-cant-be-https-enabled"></a><a name="bkmk_appcathttps"></a>Het Application Catalog-webservicepunt kan geen HTTPS-functionaliteit hebben
<!--512637-->
Als het Application Catalog-webservicepunt HTTPS-ingeschakeld is:

- Toepassingen die zijn geïmplementeerd als beschikbaar voor gebruikers, worden niet weer gegeven in Software Center  

- De volgende fout wordt weer gegeven in awebsctl. log:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Tijdelijke oplossing
Configureer het Application Catalog-webservicepunt opnieuw om te communiceren met behulp van HTTP-verbindingen.  




</br>

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Een externe inhouds bibliotheek voor de site server configureren  
<!--1357525-->
Als u ruimte op de vaste schijf op de primaire site server wilt vrijmaken, moet u de [inhouds bibliotheek](../plan-design/hierarchy/the-content-library.md) naar een andere opslag locatie verplaatsen. U kunt de inhouds bibliotheek verplaatsen naar een ander station op de site server, een afzonderlijke server of fout tolerante schijven in een Storage Area Network (SAN). We raden u aan een SAN te maken omdat deze elastische opslag biedt die in de loop der tijd groeit of verkleint om te voldoen aan de veranderende vereisten voor inhoud. 

Deze externe inhouds bibliotheek is een nieuwe vereiste voor [hoge Beschik baarheid van de site server functie](capabilities-in-technical-preview-1706.md#site-server-role-high-availability). 

> [!Note]  
> Met deze actie wordt alleen de inhouds bibliotheek op de site server verplaatst. Dit heeft geen invloed op de locatie van de inhouds bibliotheek op distributie punten. 

### <a name="prerequisites"></a>Vereisten  
- Het computer account van de site server moet **Lees** -en **Schrijf** machtigingen hebben voor het netwerkpad waarnaar u de inhouds bibliotheek verplaatst. Er zijn geen onderdelen geïnstalleerd op het externe systeem. 

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie** uit en selecteer **sites**. Op het tabblad **samen vatting** onder in het detail venster ziet u een nieuwe kolom voor de **inhouds bibliotheek**.  

2. Klik op **inhouds bibliotheek beheren** op het lint.  

3. Selecteer **een netwerk share** en voer een geldig netwerkpad in. Dit pad is de locatie waarnaar de site de inhouds bibliotheek verplaatst. Klik op **OK**.  

4. Let op de eigenschap **status** in de kolom inhouds bibliotheek in het deel venster Details. Hiermee wordt de voortgang van de site weer gegeven bij het verplaatsen van de inhouds bibliotheek. Wanneer deze bewerking wordt uitgevoerd, wordt het percentage voltooid weer gegeven. Als er een fout status is, wordt de fout weer gegeven. Veelvoorkomende fouten zijn `access denied` of `disk full` . Wanneer het volt ooien wordt weer gegeven `OK` . Raadpleeg **distmgr. log** voor meer informatie. Zie [Logboeken site server en site systeem server](../plan-design/hierarchy/log-files.md#BKMK_SiteSiteServerLog)voor meer informatie.  

Als u de inhouds bibliotheek terug naar de site server wilt verplaatsen, herhaalt u dit proces en selecteert u de optie **lokaal voor de site server**.  

> [!Tip]  
> Als u de inhoud naar een ander station op de site server wilt verplaatsen, gebruikt u het hulp programma voor de **overdracht van inhouds bibliotheken** . Zie [Configuration Manager Toolkit](#configuration-manager-toolkit)voor meer informatie.  



## <a name="submit-feedback-from-the-configuration-manager-console"></a><a name="bkmk_feedback"></a>Feedback verzenden vanuit de Configuration Manager-console  
<!--1357542-->

Glim lach verzenden U kunt nu direct het Configuration Manager team informeren over uw ervaringen. Het verzenden van feedback is eenvoudig vanuit de Configuration Manager-console. We willen al uw feedback horen: Praise, problemen en suggesties.  

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens **feedback** en laat ons weten hoe het heeft gewerkt.  

1. Klik in de Configuration Manager-console op de knop glim lach in de rechter bovenhoek boven het lint.  

2. Selecteer een van de beschik bare opties in de vervolg keuzelijst:  

   - **Een glim lach verzenden**: u hebt iets echt leuk! Voer de details van uw feedback in voor deze optie. Vervolgens kunt u desgewenst een scherm opname en uw e-mail adres toevoegen.  

   - **Frons verzenden**: er is een probleem opgetreden in de console of er is iets anders dan verwacht. Voor deze optie voert u de details van het potentiële product probleem in. Vervolgens kunt u desgewenst een scherm opname, uw e-mail adres en diagnostische gegevens toevoegen.  

   - **Een suggestie verzenden**: u hebt een idee om Configuration Manager te wijzigen en te verbeteren. Met deze optie wordt de [UserVoice](https://configurationmanager.uservoice.com) -site geopend in uw webbrowser.  

Deze feedback gaat rechtstreeks naar het micro soft-product team voor Configuration Manager. Hoewel de Windows 10 feedback-hub nog steeds wordt ondersteund, wordt u aangeraden het feedback mechanisme in de console te gebruiken.  

De volgende anonieme informatie wordt altijd opgenomen in de feedback voor context:  

- Versie en taal van Configuration Manager-console  

- Configuration Manager-site versie  

- Ondersteunings-ID, ook wel bekend als de hiërarchie-ID  

- BESTURINGSSYSTEEM versie en-taal voor het systeem waarop de-console wordt uitgevoerd  

- De exacte locatie in de console van waaruit u op het glim lach hebt geklikt  

Deze gegevens zijn consistent met de verzameling van onze diagnostische gegevens en gebruiks informatie. Zie [diagnostiek en gebruiks gegevens](../plan-design/diagnostics/diagnostics-and-usage-data.md)voor meer informatie.

### <a name="known-issues"></a>Bekende problemen

Als u probeert feedback te verzenden van een apparaat dat geen toegang heeft tot internet, kan de toepassing onverwacht worden afgesloten. Als u een glim lach of frons wilt verzenden, controleert u of het apparaat toegang heeft tot petrol.office.microsoft.com.



## <a name="support-center"></a>Ondersteuningscentrum
<!--1357489-->

Gebruik het ondersteunings centrum voor het oplossen van problemen met clients, het weer geven van real-time Logboeken of het vastleggen van de status van een Configuration Manager-client computer voor latere analyse. Ondersteunings centrum is één hulp programma voor het consolideren van veel hulpprogram ma's voor probleem oplossing. Een voor beeld van de meest recente versie van het ondersteunings centrum met oplossingen voor fouten, verbeteringen en een preview van de nieuwe log viewer is beschikbaar in de Technical Preview. Zoek het installatie programma voor het ondersteunings centrum op de site server in de map **cd. latest\SMSSETUP\Tools\SupportCenter** .


### <a name="new-support-center-features"></a>Nieuwe functies van het ondersteunings centrum  

- Een nieuwe log viewer, OneTrace. Het werkt op dezelfde manier als CMTrace en bevat verbeteringen zoals een weer gave met tabbladen en dockable Windows.  

- Met een nieuwe functie gegevens verzamelaar worden Diagnostische logboeken van de lokale of een externe Configuration Manager-client verzameld. Het biedt real-time diagnose van de inventaris (vervangt client Spy), beleid (vervangt beleids Spy) en de client cache.  



## <a name="configuration-manager-toolkit"></a>Configuration Manager Toolkit
<!--1357145-->

De Configuration Manager server-en client hulpprogramma's zijn nu opgenomen in de Technical Preview. Zoek ze in de map **cd. latest\SMSSETUP\Tools** op de site server. U hoeft verder niets te installeren.

#### <a name="server-tools"></a>Server hulpprogramma's  

- **DP-taak beheer**: problemen met inhouds distributie taken naar distributie punten oplossen  

- **Verzamelings evaluatie-Viewer**: Details van verzamelings evaluatie weer geven  

- **Inhouds bibliotheek Verkenner**: inhoud van de inhouds bibliotheek Single Instance Store weer geven  

- **Overdracht van inhouds bibliotheek**: inhouds bibliotheek verplaatsen tussen stations  

- **Hulp programma voor eigendom van inhoud**: wijzigt het eigendom van zwevende pakketten. Deze pakketten bevinden zich op de site zonder eigenaar van de site server.  

- **Op rollen gebaseerd beheer en controle programma**: helpt beheerders bij het controleren van de configuratie van rollen  

#### <a name="client-tools"></a>Client hulpprogramma's

- **CMTrace**: logboeken weer geven  

- **Hulp programma voor implementatie bewaking**: problemen met toepassingen, updates en basislijn implementaties oplossen  

- **Beleids spyware**: beleids toewijzingen weer geven  

- **Power Viewer-hulp programma**: de status van de functie voor energie beheer weer geven  

- **Hulp programma**voor het verzenden van plannen: schema's en evaluaties van DCM-basis lijnen activeren  

> [!Important]  
> [Ondersteunings centrum](#support-center) wordt aanbevolen voor de meeste use-cases, omdat het dezelfde of verbeterde functionaliteit voor de volgende hulpprogram ma's bevat:  
> - Client Spy
> - CMTrace<sup>1</sup> 
> - Hulpprogramma voor implementatiebewaking
> - Policy Spy
> - Hulpprogramma voor het verzenden van planningen
> 
> <sup>1</sup> CMTrace is niet afhankelijk van .net of Windows PRESENTATION Foundation (WPF), dus wordt nog steeds gebruikt in Windows PE-opstart installatie kopieën.

### <a name="known-issues"></a>Bekende problemen
Sommige client-en server hulpprogramma's worden onverwacht afgesloten tijdens het starten. Dit probleem wordt veroorzaakt door een ontbrekend bestand op de media. Als tijdelijke oplossing kopieert u het bestand **micro soft. Diagnostics. Tract. Event source. dll** vanuit de AdminConsole\bin-map in zowel SMSSETUP\Tools\ClientTools-als server-hulp directory's. Dit bestand moet dezelfde versie zijn als die wordt gebruikt door de Configuration Manager-console. Andere versies werken mogelijk niet. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Toepassing verwijderen bij het intrekken van de goed keuring
<!--1357891-->

Het gedrag is gewijzigd wanneer u de goed keuring voor een toepassing intrekt. Wanneer u de aanvraag voor de toepassing weigert, verwijdert de client de toepassing van het apparaat van de gebruiker. 

### <a name="prerequisites"></a>Vereisten
- De functie **voor het goed keuren van toepassings aanvragen voor gebruikers per apparaat**inschakelen.

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Implementeer in de Configuration Manager-console voor een gebruiker een toepassing waarvoor goed keuring is vereist. Schakel op het tabblad **implementatie-instellingen** van de implementatie de optie **een beheerder moet een aanvraag voor deze toepassing goed keuren op het apparaat**.  

2. Op de Configuration Manager-client in Software Center vraagt de gebruiker goed keuring aan om de toepassing te installeren.  

3. In de Configuration Manager-console moet u de aanvraag voor deze gebruiker goed keuren om de toepassing op het apparaat te installeren. Aanvragen voor het goed keuren van toepassingen worden weer gegeven in de werk ruimte **software bibliotheek** onder **toepassings beheer**in het knoop punt **goedkeurings aanvragen** .  

4. Op de client in Software Center installeert de gebruiker de toepassing.  

5. Weiger de aanvraag van de gebruiker voor de toepassing op het apparaat in de Configuration Manager-console.  

### <a name="known-issues"></a>Bekende problemen
- Nadat de gebruiker de toepassing op de client heeft geïnstalleerd, werkt u het gebruikers beleid bij. Ga in Software Center naar het tabblad **Opties** , vouw **computer onderhoud** uit en klik op **beleid synchroniseren**.<!--480609-->  

- Het Application Catalog-webservicepunt moet HTTP zijn. Zie [bekende problemen in deze technische preview](#bkmk_appcathttps)voor meer informatie.<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Active Directory containers uitsluiten van detectie
<!--1358143-->
Als u het aantal gedetecteerde objecten wilt verminderen, kunt u nu specifieke containers uitsluiten van Active Directory systeem detectie. Deze functie is een resultaat van uw [UserVoice-feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **hiërarchie configuratie** uit en selecteer **detectie methoden**. Selecteer **Active Directory systeem detectie** en klik op **Eigenschappen** in het lint.  

2. Klik op het pictogram Nieuw om een nieuwe Active Directory-container op te geven.   

3. In het dialoog venster Active Directory container gaat u naar of typt u het **pad** in de sectie locatie om de detectie te starten.  

4. Schakel in de sectie Zoek opties de optie in voor het **recursief zoeken Active Directory onderliggende containers**. Klik vervolgens op **toevoegen** om subcontainers te selecteren die moeten worden uitgesloten van deze detectie.  

5. Selecteer in het dialoog venster nieuwe container selecteren een onderliggende container die u wilt uitsluiten. Klik op **OK** om het dialoog venster nieuwe container selecteren te sluiten.  

6. Klik op **OK** om het dialoog venster Active Directory container te sluiten.  

7. In de venster Eigenschappen Active Directory systeem detectie raadpleegt u het pad van de Active Directory-container waarop de detectie wordt gestart. In de **recursieve** kolom ziet u **Ja**en de nieuwe kolom **bevat uitsluitingen** bevat ook **Ja**. Klik op **OK** om de venster Eigenschappen Active Directory systeem detectie te sluiten.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>De zicht baarheid van de toepassingscatalogus website koppeling in Software Center opgeven
<!--1358214-->

U kunt nu bepalen of de koppeling voor **het openen van de toepassingscatalogus** website wordt weer gegeven in het knoop punt **installatie status** van software Center.  

> [!Note]  
> Ondersteuning voor de gebruikers ervaring van de toepassingscatalogus website eindigt op de eerste update die na 1 juni 2018 is uitgebracht. Zie [verwijderde en afgeschafte functies](../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.  

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Maak in de Configuration Manager-console, werk ruimte **beheer** , knoop punt **client instellingen** een aangepast beleid voor client Apparaatinstellingen.  

2. Selecteer de **Software Center** -groep.  

3. Klik voor **Software Center-instellingen**op **aanpassen**.  

4. Schakel de optie in om **de toepassingscatalogus website koppeling in Software Center te verbergen**.   

Zie [client instellingen configureren](../clients/deploy/configure-client-settings.md)voor meer informatie over client instellingen.




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Regels voor automatische implementatie filteren op software-update architectuur
 <!--1322266-->
U kunt nu regels voor automatische implementatie filteren om architecturen zoals Itanium en ARM64 uit te sluiten.

### <a name="try-it-out"></a>Probeer het nu!
Probeer de taken uit te voeren. Stuur vervolgens [feedback](#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **software-updates** uit en selecteer **regels voor automatische implementatie**. Selecteer op het lint **regel voor automatische implementatie maken**.  

2. Vul de juiste instellingen in voor het tabblad **Algemeen** en het tabblad **implementatie-instellingen** .  

3. Selecteer op het tabblad **software-updates** de optie **architectuur** en klik vervolgens op **items om te zoeken** in de **zoek criteria**.  

4. Selecteer de architecturen die u wilt toevoegen in de regel voor automatische implementatie.  

5. Klik op **volgende** en ga door met het maken van de regel voor automatische implementatie.  

> [!IMPORTANT]  
> Houd er rekening mee dat er 32-bits (x86) toepassingen en onderdelen op 64-bits (x64)-systemen worden uitgevoerd. Tenzij u er zeker van bent dat u geen x86 nodig hebt, schakelt u deze in en selecteert u x64.  

### <a name="known-issues"></a>Bekende problemen
Nadat de architectuur criteria zijn toegevoegd, wordt op de pagina eigenschappen van regel voor automatische implementatie de **titel** weer gegeven in de zoek criteria. De regel voor automatische implementatie werkt nog steeds op de verwachte manier en selecteert de juiste software-updates. U kunt op dit moment echter geen criteria voor de **architectuur** en de **titel** opgeven. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Verbeteringen in de implementatie van het besturings systeem
We hebben de volgende verbeteringen aangebracht in de implementatie van het besturings systeem, wat het resultaat was van de feedback van uw gebruikers stem.  

- [Masker gevoelige gegevens die zijn opgeslagen in taken reeks variabelen](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): Selecteer in de stap [taken reeks variabele instellen](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) de optie nieuwe om **deze waarde niet weer te geven**. Bijvoorbeeld wanneer u een wacht woord opgeeft.<!--1358330--> Wanneer u deze optie inschakelt, geldt het volgende gedrag:
  - De waarde van de variabele wordt niet weer gegeven in bestand smsts. log.
  - De Configuration Manager-console en de SMS-provider verwerken deze waarde hetzelfde als andere geheimen, zoals wacht woorden.
  - De waarde wordt niet opgenomen wanneer u de taken reeks exporteert.
  - De taken reeks editor leest deze waarde niet wanneer u de stap bewerkt. Typ de volledige waarde opnieuw om wijzigingen aan te brengen.

  > [!Important]  
  > Variabelen en hun waarden worden opgeslagen met de taken reeks als XML en verborgen in de-data base. Wanneer de client een taken reeks beleid aanvraagt van het beheer punt, wordt dit tijdens de overdracht versleuteld en wanneer het op de client wordt opgeslagen. Alle variabelen waarden zijn echter onbewerkte tekst in de taken reeks omgeving in het geheugen tijdens runtime op de client. Als de taken reeks een stap bevat voor het uitvoeren van de waarde van de variabele, is deze uitvoer in tekst zonder opmaak. Dit gedrag vereist een expliciete actie van de beheerder voor het toevoegen van een dergelijke stap in de taken reeks. 


- [Naam van masker programma tijdens het uitvoeren van de opdracht stap van een taken reeks](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): als u wilt voor komen dat gevoelige gegevens worden weer gegeven of geregistreerd, stelt u de taken reeks variabele **OSDDoNotLogCommand** in op `TRUE` . Deze variabele maskeert de naam van het programma in bestand smsts. log tijdens de taken reeks stap [opdracht regel uitvoeren](../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) . <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Verbeteringen in de Configuration Manager-console
- De gegevens van de primaire gebruiker zijn nu zichtbaar bij het weer geven van de leden van een verzameling onder **activa en naleving**, **apparaat verzamelingen**.<!--510252-->  



## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    
