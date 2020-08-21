---
title: Software-updates automatisch implementeren
titleSuffix: Configuration Manager
description: Software-updates automatisch implementeren met behulp van automatische implementatie regels (ADR).
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 3f49d7d001de07a7d3d6a7bdbb5f9ff90de018c9
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699871"
---
#  <a name="automatically-deploy-software-updates"></a>Software-updates automatisch implementeren  

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik een regel voor automatische implementatie (ADR) in plaats van nieuwe updates aan een bestaande software-update groep toe te voegen. Normaal gesp roken gebruikt u Adr's om maandelijkse software-updates te implementeren (ook wel ' patch dinsdag-updates ' genoemd) en voor het beheren van Endpoint Protection definitie-updates. Zie [software-updates implementeren](deploy-software-updates.md)als u hulp nodig hebt om te bepalen welke implementatie methode het meest geschikt is voor u.


##  <a name="create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Een regel voor automatische implementatie (ADR) maken  
Automatisch goed keuren en implementeren van software-updates met behulp van een ADR. De regel kan software-updates toevoegen aan een nieuwe software-update groep elke keer dat de regel wordt uitgevoerd, of software-updates toevoegen aan een bestaande groep. Wanneer een regel wordt uitgevoerd en software-updates worden toegevoegd aan een bestaande groep, verwijdert de regel alle updates uit de groep. Vervolgens wordt aan de groep de updates toegevoegd die voldoen aan de criteria die u definieert. 

> [!WARNING]  
>  Voordat u voor de eerste keer een ADR maakt, moet u controleren of de site de synchronisatie van software-updates heeft voltooid. Deze stap is belang rijk wanneer u Configuration Manager uitvoert met een niet-Engelse taal. Software-update classificaties worden weer gegeven in het Engels vóór de eerste synchronisatie en worden vervolgens weer gegeven in de gelokaliseerde talen nadat de software-update synchronisatie is voltooid. Regels die u maakt voordat u software-updates synchroniseert, werken mogelijk niet goed na synchronisatie, omdat de tekst teken reeks mogelijk niet overeenkomt.  


### <a name="process-to-create-an-adr"></a><a name="bkmk_adr-process"></a> Proces voor het maken van een ADR  

1.  Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **software-updates**uit en selecteer het knoop punt regels voor **automatische implementatie** .  

2.  Klik op het lint op **regel voor automatische implementatie maken**.  

3.  Configureer op de pagina **Algemeen** van de wizard regel voor automatische implementatie maken de volgende instellingen:  

    -   **Naam**: geef de naam voor de ADR op. De naam moet uniek zijn, het doel van de regel beschrijven en deze identificeren van anderen op de Configuration Manager-site.  

    -   **Beschrijving**: geef een beschrijving op voor de ADR op. De beschrijving moet een overzicht bieden van de implementatie regel en andere relevante informatie waarmee de regel van anderen kan worden onderscheiden. Het beschrijvingsveld is optioneel en kent een limiet van 256 tekens. Het veld is standaard leeg.  

    -   **Sjabloon**: Selecteer een implementatie sjabloon om op te geven of eerder opgeslagen ADR-configuraties moeten worden toegepast. Configureer een implementatie sjabloon met meerdere algemene eigenschappen voor update-implementaties die u kunt gebruiken bij het maken van extra Adr's. Deze sjablonen besparen tijd en helpen consistentie te garanderen tussen soort gelijke implementaties. Selecteer een van de volgende ingebouwde implementatie sjablonen voor software-updates:  

         - De sjabloon **Patch Tuesday** biedt algemene instellingen die u kunt gebruiken wanneer u software-updates implementeert op basis van een maandelijkse cyclus.  

         - De sjabloon **Office 365-client updates** biedt algemene instellingen die u kunt gebruiken wanneer u updates implementeert voor Microsoft 365 apps-clients.
             > [!Note]
             > Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Als uw Adr's afhankelijk is van de eigenschap ' title ', moet u deze bewerken vanaf 9 juni 2020. `Microsoft 365 Apps Update - Semi-annual Channel Version 1908 for x64 based Edition (Build 11929.50000)` is een voor beeld van de nieuwe titel. Zie voor meer informatie over het wijzigen van uw Adr's voor de titel wijziging [kanalen voor Microsoft 365 apps bijwerken](manage-office-365-proplus-updates.md#bkmk_channel). Zie voor meer informatie over de naamswijziging naam [wijzigen voor Office 365 ProPlus](/deployoffice/name-change).

         - De sjabloon **SCEP-en Windows Defender anti virus-updates** biedt algemene instellingen die u kunt gebruiken wanneer u Endpoint Protection definitie-updates implementeert.  

    -   **Verzameling**: hiermee geeft u de doelverzameling op die moet worden gebruikt voor de implementatie. Leden van de verzameling ontvangen de software-updates die in de implementatie zijn gedefinieerd.  

    -   Bepaal of u software-updates toevoegt aan een nieuwe of een bestaande software-updategroep. In de meeste gevallen kiest u voor het maken van een nieuwe software-update groep wanneer de ADR wordt uitgevoerd. Als de regel op een agressieve planning wordt uitgevoerd, kunt u ervoor kiezen om een bestaande groep te gebruiken. Als u de regel bijvoorbeeld dagelijks uitvoert voor definitie-updates, kunt u de software-updates toevoegen aan een bestaande software-update groep.  

    -   **De implementatie inschakelen nadat deze regel is uitgevoerd**: geef op of de implementatie van de software-update moet worden ingeschakeld nadat de ADR is uitgevoerd. Houd rekening met de volgende opties voor deze instelling:  

        -   Wanneer u de implementatie inschakelt, worden de updates die voldoen aan de gedefinieerde criteria van de regel, toegevoegd aan een software-update groep. De inhoud van de software-update wordt indien nodig gedownload. De inhoud wordt gekopieerd naar de opgegeven distributie punten en de updates worden geïmplementeerd naar de clients in de doel verzameling.  

        -   Wanneer u de implementatie niet inschakelt, worden de updates die voldoen aan de gedefinieerde criteria van de regel, toegevoegd aan een software-update groep. De inhoud van de software-update-implementatie wordt zo nodig gedownload en gedistribueerd naar de opgegeven distributie punten. De site maakt een uitgeschakelde implementatie in de software-update groep om te voor komen dat de updates worden geïmplementeerd op clients. Deze optie biedt tijd om u voor te bereiden op de implementatie van de updates, te controleren of de updates die voldoen aan de criteria voldoende zijn en vervolgens de implementatie in te scha kelen.  

4.  Configureer de volgende instellingen op de pagina **implementatie-instellingen** :  

    -   **Wake-on-LAN gebruiken om clients te laten ontwaken voor vereiste implementaties**: Hiermee geeft u op of Wake on LAN op de deadline moet worden ingeschakeld. Wake On LAN verzendt Ontwaak pakketten naar computers waarvoor een of meer software-updates in de implementatie zijn vereist. De site ontwaakt alle computers die zich in de slaap stand bevinden tijdens de deadline van de installatie, zodat de installatie kan worden gestart. Clients die zich in de slaap stand bevinden en geen software-updates nodig hebben in de implementatie, worden niet gestart. Deze instelling is standaard niet ingeschakeld. Voordat u deze optie gebruikt, configureert u computers en netwerken voor Wake On LAN. Zie [Wake on LAN configureren](../../core/clients/deploy/configure-wake-on-lan.md)voor meer informatie.  

    -   **Detail niveau**: Geef het detail niveau op voor de status berichten van de update afdwinging die door clients worden gerapporteerd.  

        > [!IMPORTANT]  
        >  Wanneer u definitie-updates implementeert, stelt u het detail niveau in op **alleen fout** zodat de client alleen een status bericht rapporteert wanneer een definitie-update mislukt. Anders rapporteert de client een groot aantal status berichten dat van invloed kan zijn op de prestaties van de site server.  
        
        > [!NOTE]  
        > Het detail niveau **alleen fout** verzendt de afdwingings status berichten die zijn vereist voor het bijhouden van wachtende herstarts.

    -   **Instelling voor licentiebepalingen**: geef op of software-updates waaraan licentiebepalingen zijn gekoppeld, automatisch moeten worden geïmplementeerd. Sommige software-updates bevatten licentie voorwaarden. Wanneer u software-updates automatisch implementeert, worden de licentie voorwaarden niet weer gegeven en is er geen optie om de licentie voorwaarden te accepteren. Kies deze optie om alle software-updates automatisch te implementeren, ongeacht een gekoppelde licentie voorwaarde of alleen updates te implementeren waaraan geen licentie voorwaarden zijn gekoppeld.  

         - Als u de licentie voorwaarden voor een software-update wilt controleren, selecteert u de software-update in het knoop punt **alle software-updates** van de werk ruimte **software bibliotheek** . Klik in het lint op **licentie weer geven**.    

         - Als u wilt zoeken naar software-updates met bijbehorende licentie voorwaarden, voegt u de kolom **licentie voorwaarden** toe aan het deel venster met resultaten in het knoop punt **alle software-updates** . Klik op de kolomkop om de kolom te sorteren op software-updates met licentie voorwaarden.  

5.  Configureer op de pagina **software-updates** de criteria voor de software-updates die door de ADR worden opgehaald en toegevoegd aan de software-update groep.  

     - De limiet voor software-updates in de ADR is 1000 software-updates.  

     - Als dat nodig is, filtert u op de inhouds grootte voor software-updates in de regels voor automatische implementatie. Zie [Configuration Manager en vereenvoudigd Windows-onderhoud op besturings systemen van lagere niveaus](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056)voor meer informatie.  

     - Met ingang van versie 1910 kunt u **geïmplementeerd** als een update filter voor uw regels voor automatische implementatie. Dit filter helpt bij het identificeren van nieuwe updates die mogelijk moeten worden geïmplementeerd voor uw pilot-of test verzamelingen. Het software-update filter kan er ook voor zorgen dat oudere updates niet opnieuw worden geïmplementeerd. 
         - Als u **geïmplementeerd** als een filter gebruikt, moet u mindful zijn dat u de update mogelijk al hebt geïmplementeerd voor een andere verzameling, zoals een pilot-of test verzameling. <!--4852033-->
     - Vanaf versie 1806 is er nu een eigenschappen Filter voor **architectuur** beschikbaar. Gebruik dit filter om architecturen zoals Itanium en ARM64 uit te sluiten die minder gangbaar zijn. Houd er rekening mee dat er 32-bits (x86) toepassingen en onderdelen op 64-bits (x64)-systemen worden uitgevoerd. Tenzij u er zeker van bent dat u geen x86 nodig hebt, schakelt u deze in en selecteert u x64.<!--1322266-->  

    > [!NOTE]  
    > **Windows 10, versie 1903 en hoger** is toegevoegd aan Microsoft Update als een eigen product in plaats van dat ze deel uitmaken van het **Windows 10**  -product zoals eerdere versies. Als gevolg van deze wijziging hebt u een aantal hand matige stappen uitgevoerd om ervoor te zorgen dat uw clients deze updates zien. We hebben geholpen het aantal hand matige stappen te verminderen dat u moet ondernemen voor het nieuwe product in Configuration Manager versie 1906. Zie voor meer informatie [producten configureren voor versies van Windows 10](../get-started/configure-classifications-and-products.md#windows-10-version-1903-and-later) <!--4682946-->


6. Geef op de pagina **evaluatie planning** op of de ADR moet worden ingeschakeld voor uitvoering volgens een schema. Wanneer dit is ingeschakeld, klikt u op **Aanpassen** om de terugkerende planning in te schakelen.  

    - De configuratie van de start tijd voor de planning is gebaseerd op de lokale tijd van de computer waarop de Configuration Manager-console wordt uitgevoerd.  

    - De ADR-evaluatie kan twee tot drie keer per dag worden uitgevoerd.  

    - Stel het evaluatie schema nooit in met een frequentie die de synchronisatie planning voor software-updates overschrijdt. Op deze pagina wordt het synchronisatie schema van het software-update punt weer gegeven om u te helpen de frequentie van de evaluatie planning te bepalen.  

    - Als u de ADR hand matig wilt uitvoeren, selecteert u de regel in het knoop punt **automatische implementatie regel** van de-console en klikt u vervolgens op **nu uitvoeren** op het lint.  

    - Vanaf versie 1802 kan Adr's worden gepland om de offset van een basis dag te evalueren. Als patch-dinsdag bijvoorbeeld werkelijk op woensdag voor u valt, stelt u de evaluatie planning voor de tweede dinsdag van de maand met één dag in.<!--1357133-->  
        - Bij het plannen van een evaluatie met een verschuiving in de laatste week van de maand, als u een offset kiest die in de volgende maand blijft, wordt de evaluatie van de site gepland voor de laatste dag van de maand.<!--506731-->  
        ![Verschuiving aangepaste evaluatie planning ADR van basis dag](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Configureer de volgende instellingen op de pagina **implementatie planning** :  

    -   **Evaluatie van planning**: Geef de tijd op die Configuration Manager de beschik bare tijd en deadline van de installatie wilt evalueren. Kies voor het gebruik van UTC (Coordinated Universal Time) of de lokale tijd van de computer waarop de Configuration Manager-console wordt uitgevoerd.  

          - Wanneer u hier **client lokale tijd** selecteert en vervolgens **zo spoedig mogelijk** selecteert voor de tijd waarop de **software beschikbaar**is, wordt de huidige tijd op de computer waarop de Configuration Manager-console wordt uitgevoerd, gebruikt om te evalueren wanneer er updates beschikbaar zijn. Dit gedrag is hetzelfde als de **installatie deadline** en de tijd waarop updates worden geïnstalleerd op een client. Als de client zich in een andere tijd zone bevindt, worden deze acties uitgevoerd wanneer de tijd van de client de evaluatie tijd heeft bereikt.  

    -   **Tijd waarop de software beschikbaar is**: selecteer een van de volgende instellingen om op te geven wanneer de software-updates beschikbaar worden gemaakt voor clients:  

        -   **Zo spoedig mogelijk**: maakt de software-updates in de implementatie zo spoedig mogelijk beschikbaar voor clients. Wanneer u de implementatie maakt terwijl deze instelling is geselecteerd, wordt het client beleid door Configuration Manager bijgewerkt. Bij de volgende polling cyclus van het client beleid worden clients op de hoogte van de implementatie en kunnen de software-updates beschikbaar zijn voor installatie.  

        -   **Specifiek tijdstip**: Hiermee worden software-updates die zijn opgenomen in de implementatie beschikbaar voor clients op een specifieke datum en tijd. Wanneer u de implementatie maakt terwijl deze instelling is ingeschakeld, wordt het client beleid door Configuration Manager bijgewerkt. Bij de volgende polling cyclus van het client beleid worden clients op de hoogte van de implementatie. De software-updates in de implementatie zijn echter pas na de geconfigureerde datum en tijd beschikbaar voor installatie.  

    -   **Installatie deadline**: Selecteer een van de volgende instellingen om de installatie deadline op te geven voor de software-updates in de implementatie:  

        -   **Zo spoedig mogelijk**: selecteer deze instelling als u wilt dat de software-updates in de implementatie zo spoedig mogelijk automatisch worden geïnstalleerd.  

        -   **Specifiek tijdstip**: selecteer deze instelling als u wilt dat de software-updates in de implementatie automatisch worden geïnstalleerd op een specifieke datum en tijd. Configuration Manager bepaalt de deadline voor het installeren van software-updates door het geconfigureerde **specifieke tijds** interval toe te voegen aan de **beschik bare tijd**van de software.  

             - De werkelijke duur van de installatie deadline is de weer gegeven deadline tijd plus een wille keurige hoeveelheid tijd tot twee uur. Met deze wille keuring vermindert u de potentiële impact van clients in de verzameling die tegelijkertijd updates in de implementatie installeren.  

             - Als u de vertraging voor wille keurige installatie wilt uitschakelen voor vereiste software-updates, configureert u de client instelling voor het **uitschakelen van deadline wille keurigheid** in de groep **computer agent** . Zie [client instellingen voor computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent)voor meer informatie.  

    -  **Het afdwingen van deze implementatie op basis van gebruikers voorkeuren uitstellen tot de respijt periode die in de client instellingen is gedefinieerd**: Schakel deze instelling in om gebruikers meer tijd te geven om de vereiste software-updates na de deadline te installeren.  

        - Dit gedrag is doorgaans vereist wanneer een computer gedurende een lange periode wordt uitgeschakeld en veel software-updates of toepassingen moeten worden geïnstalleerd. Wanneer een gebruiker bijvoorbeeld een vakantie retourneert, moet deze gedurende een lange periode worden gewacht wanneer de client achterstallige implementaties installeert.  

        - Deze respijt periode configureren met de **respijt periode van de eigenschap voor afdwinging na de deadline van de implementatie (uren)** in de client instellingen. Zie de sectie [computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) voor meer informatie. De respijt periode voor afdwinging is van toepassing op alle implementaties waarbij deze optie is ingeschakeld en is gericht op apparaten waarop u ook de client instelling hebt geïmplementeerd.  

        - Na de deadline installeert de client de software-updates in het eerste niet-zakelijke venster, dat door de gebruiker is geconfigureerd, tot deze respijt periode. De gebruiker kan echter nog steeds Software Center openen en de software-updates op elk gewenst moment installeren. Zodra de respijt periode is verlopen, wordt de afdwinging hersteld naar het normale gedrag voor achterstallige implementaties.  

8. Configureer op de pagina **gebruikers ervaring** de volgende instellingen:  

    -   **Meldingen voor gebruikers**: Geef op of meldingen in Software Center moeten worden weer gegeven op de geconfigureerde **tijd waarop de software beschikbaar is**. Deze instelling bepaalt ook of gebruikers op de clients moeten worden gewaarschuwd.  

    -   **Deadline gedrag**: Geef het gedrag op wanneer de implementatie van de software-update de deadline bereikt buiten de gedefinieerde onderhouds Vensters. De opties omvatten of de software-updates moeten worden geïnstalleerd en of het systeem na de installatie opnieuw moet worden opgestart. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.  
        
        > [!Note]
        > Dit geldt alleen wanneer het onderhouds venster is geconfigureerd voor het client apparaat. Als er geen onderhouds venster is gedefinieerd op het apparaat, wordt de update van de installatie en opnieuw opstarten altijd na de deadline uitgevoerd.

    -   **Gedrag voor opnieuw opstarten van apparaat**: Geef op of opnieuw opstarten van servers en werk stations moet worden onderdrukt als opnieuw opstarten is vereist om de installatie van de update te volt ooien.  

        > [!WARNING]  
        >  Het onderdrukken van het opnieuw opstarten van het systeem kan nuttig zijn in Server omgevingen of wanneer u niet wilt dat de doel computers standaard opnieuw worden opgestart. Hierdoor kunnen computers echter een onveilige status achterlaten. Het toestaan van een geforceerde herstart zorgt ervoor dat de installatie van de software-update onmiddellijk kan worden voltooid.  

    -   **Verwerking van schrijf filters voor Windows Embedded-apparaten**: met deze instelling bepaalt u het installatie gedrag op Windows Embedded-apparaten waarvoor een schrijf filter is ingeschakeld. Kies de optie om wijzigingen door te voeren bij de deadline van de installatie of tijdens een onderhouds venster. Wanneer u deze optie selecteert, moet de computer opnieuw worden opgestart en worden de wijzigingen op het apparaat bewaard. Anders wordt de update geïnstalleerd, toegepast op de tijdelijke overlay en later vastgelegd.  

           -  Wanneer u een software-update implementeert op een Windows Embedded-apparaat, moet u ervoor zorgen dat het apparaat lid is van een verzameling met een geconfigureerd onderhouds venster.  

    - **Gedrag van nieuwe evaluatie van software-updates bij opnieuw opstarten**: Selecteer deze instelling om implementaties van software-updates te configureren zodat clients onmiddellijk na de installatie van software-updates een scan voor de compatibiliteit van software-updates uitvoeren. Met deze instelling kan de client controleren op aanvullende updates die van toepassing zijn nadat de client opnieuw is opgestart. vervolgens worden ze geïnstalleerd tijdens hetzelfde onderhouds venster.  

9. Configureer op de pagina **waarschuwingen** hoe Configuration Manager waarschuwingen genereert voor deze implementatie. Bekijk de recente waarschuwingen voor software-updates van Configuration Manager in het knoop punt **software-updates** van de werk ruimte **software bibliotheek** . Als u ook System Center Operations Manager gebruikt, moet u de waarschuwingen ook configureren.  

10. Configureer de volgende instellingen op de pagina **Download instellingen** :  

    - Geef op of clients de updates moeten downloaden en installeren wanneer ze een distributie punt van een neighbor of de standaard site grens groepen gebruiken.  

    - Geef op of clients de updates moeten downloaden en installeren vanaf een distributie punt in de standaard grens groep van de site, wanneer de inhoud voor de software-updates niet beschikbaar is vanaf een distributie punt in de huidige of grens groepen van de buur.  

    - **Clients toestaan inhoud te delen met andere clients in hetzelfde subnet**: hier kunt u aangeven of het gebruik van BranchCache moet worden ingeschakeld voor het downloaden van inhoud. Zie [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)voor meer informatie. Vanaf versie 1802 is BranchCache altijd ingeschakeld op clients. Deze instelling wordt verwijderd omdat clients BranchCache gebruiken als het distributie punt deze ondersteunt.  

    - **Als er geen software-updates beschikbaar zijn op het distributie punt in de huidige, naburige of site grens groepen, downloadt u inhoud van micro soft-updates**: Selecteer deze instelling als u wilt dat clients met een intranet software-updates downloaden van Microsoft Update als er geen updates beschikbaar zijn op distributie punten. Clients op Internet gaan altijd naar Microsoft Update voor inhoud van software-updates.  

    - Geef op of clients mogen downloaden na een installatie deadline wanneer deze Internet verbindingen met een Data limiet gebruiken. Internet providers worden soms kosten in rekening gebracht op basis van de hoeveelheid gegevens die u verzendt en ontvangt wanneer u gebruikmaakt van een verbinding met een Data limiet.  

    > [!NOTE]  
    >  Clients vragen de inhoudlocatie aan bij het beheerpunt voor de software-updates in een implementatie. Het Download gedrag is afhankelijk van hoe u het distributie punt, het implementatie pakket en de instellingen op deze pagina hebt geconfigureerd.   

11. Selecteer op de pagina **implementatie pakket** een van de volgende opties:  

    - **Een implementatie pakket selecteren**: Voeg deze updates toe aan een bestaand implementatie pakket.  

    - **Een nieuw implementatie pakket maken**: Voeg deze updates toe aan een nieuw implementatie pakket. Configureer de volgende aanvullende instellingen:  

        -  **Naam**: geef de naam op van het implementatiepakket. Gebruik een unieke naam die de pakket inhoud beschrijft. Het is beperkt tot 50 tekens.  

        -  **Beschrijving**: geef een beschrijving op die informatie biedt over het implementatiepakket. De optionele beschrijving is beperkt tot 127 tekens.  

        -  **Pakketbron**: hiermee geeft u de locatie op van de bronbestanden van de software-update. Typ een netwerkpad voor de bron locatie, bijvoorbeeld, `\\server\sharename\path` of klik op **Bladeren** om de netwerk locatie te zoeken. Maak de gedeelde map voor de bron bestanden van het implementatie pakket voordat u doorgaat naar de volgende pagina.  

            - U kunt de opgegeven locatie niet gebruiken als de bron van een ander software-implementatie pakket.  

            - U kunt de pakket bron locatie wijzigen in de eigenschappen van het implementatie pakket nadat Configuration Manager het implementatie pakket hebt gemaakt. Als dit het geval is, kopieert u eerst de inhoud van de oorspronkelijke pakket bron naar de nieuwe pakket bron locatie.  

            -  De computer account van de SMS-provider en de gebruiker die de wizard uitvoert om de software-updates te downloaden, moeten beide **Schrijf** machtigingen hebben voor de download locatie. Beperk de toegang tot de download locatie. Deze beperking vermindert het risico van aanvallers die knoeien met de bron bestanden van de software-update.  

        -  **Prioriteit voor verzenden**: geef de prioriteit op voor verzenden van het implementatiepakket. Configuration Manager gebruikt deze prioriteit wanneer het pakket naar distributie punten wordt verzonden. Implementatie pakketten worden in volg orde van prioriteit verzonden: hoog, gemiddeld of laag. Pakketten met een identieke prioriteit worden verzonden in de volgorde waarin deze zijn gemaakt. Als er geen achterstand is, wordt het pakket onmiddellijk verwerkt, ongeacht de prioriteit.  

        - **Binary Differential Replication inschakelen**: Schakel deze instelling in om binary Differential Replication te gebruiken voor het implementatie pakket. Zie [binaire Differentiële replicatie](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication)voor meer informatie.  

    - **Geen implementatie pakket**: vanaf versie 1806 kunt u software-updates implementeren op apparaten zonder eerst inhoud te downloaden en te distribueren naar distributie punten. Deze instelling is nuttig bij het verwerken van extreem grote update-inhoud. Gebruik dit ook wanneer u altijd wilt dat clients inhoud ophalen van de Microsoft Update Cloud service. Clients in dit scenario kunnen ook inhoud downloaden van peers die al over de benodigde inhoud beschikken. De Configuration Manager-client blijft het downloaden van de inhoud blijven beheren, maar kan ook gebruikmaken van de functie voor Configuration Manager peer-cache of andere technologieën zoals Delivery Optimization. Deze functie ondersteunt elk update type dat wordt ondersteund door Configuration Manager beheer van software-updates, waaronder updates van Windows-en Microsoft 365-apps.<!--1357933-->  

        > [!Note]  
        > Wanneer u deze optie selecteert en de instellingen toepast, kan deze niet meer worden gewijzigd. De andere opties worden grijs weer gegeven.<!--SCCMDocs-pr issue 3003-->  

12. Geef op de pagina **distributie punten** de distributie punten of distributiepunten groepen op om de software-update bestanden te hosten. Zie [Configuraties van het distributiepunt](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)voor meer informatie over distributiepunten. Deze pagina is alleen beschikbaar wanneer u een nieuw implementatiepakket voor software-updates maakt.  
  

13. Geef op de pagina **Download locatie** op of de software-update bestanden moeten worden gedownload vanaf internet of vanaf uw lokale netwerk. Configureer de volgende instellingen:  

    -   **Software-updates downloaden van Internet**: Selecteer deze instelling om de software-updates te downloaden vanaf een opgegeven locatie op internet. Deze instelling is standaard ingeschakeld.  

    -   **Software-updates downloaden vanaf een locatie op het lokale netwerk**: selecteer deze instelling als u wilt dat de software-updates worden gedownload vanuit een lokale map of een gedeelde map. Deze instelling is nuttig wanneer de computer waarop de wizard wordt uitgevoerd, geen toegang tot internet heeft. Elke computer met Internet toegang kan tijdig downloaden van de software-updates. Sla ze vervolgens op in een locatie op het lokale netwerk die toegankelijk is vanaf de computer waarop de wizard wordt uitgevoerd. Een ander scenario kan zijn wanneer u inhoud downloadt die is gepubliceerd via System Center Updates Publisher of een patch oplossing van derden. De WSUS-inhouds share op het software-update punt op het hoogste niveau kan worden ingevoerd als de netwerk locatie die moet worden gedownload, zoals `\\server\WsusContent` . <!--memdocs-issue-211-->

14. Selecteer op de pagina **taal** selecteren de talen waarvoor de site de geselecteerde software-updates downloadt. De site downloadt deze updates alleen als deze beschikbaar zijn in de geselecteerde talen. Software-updates die niet taalspecifiek zijn, worden altijd gedownload. De wizard selecteert standaard de talen die u hebt geconfigureerd in de eigenschappen van het software-update punt. Er moet ten minste één taal worden geselecteerd voordat u doorgaat naar de volgende pagina. Wanneer u alleen talen selecteert die niet door een software-update worden ondersteund, mislukt het downloaden van de update.  

15. Bekijk de instellingen op de pagina **Samenvatting** . Klik op **Opslaan als sjabloon**om de instellingen op te slaan in een implementatie sjabloon. Voer een naam in en selecteer de instellingen die u in de sjabloon wilt gebruiken en klik vervolgens op **Opslaan**. Als u een geconfigureerde instelling wilt wijzigen, klikt u op de gekoppelde wizardpagina en wijzigt u de instelling.  

    -  De sjabloon naam kan bestaan uit alfanumerieke ASCII-tekens en `\` (backslash) of `'` (enkele aanhalings tekens).  

16. Klik op **Volgende** om de ADR te maken.  

Nadat u de wizard hebt voltooid, wordt de ADR uitgevoerd. De software-updates die aan de opgegeven criteria voldoen, worden toegevoegd aan een software-update groep. Vervolgens worden de updates gedownload naar de inhouds bibliotheek op de site server en gedistribueerd naar de geconfigureerde distributie punten. De ADR implementeert vervolgens de software-update groep voor clients in de doel verzameling.  



##  <a name="add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a> Nieuwe implementaties aan een bestaande ADR toevoegen  

Nadat u een ADR hebt gemaakt, kunt u aanvullende implementaties aan de regel toevoegen. Deze actie helpt u bij het beheren van de complexiteit van het implementeren van verschillende updates voor verschillende verzamelingen. Elke nieuwe implementatie heeft alle functionaliteit en biedt de volledige implementatiebewakingservaring.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Proces voor het toevoegen van een nieuwe implementatie aan een bestaande ADR  

1.  In de Configuration Manager-console gaat u naar de werk ruimte **software bibliotheek** , vouwt u **software-updates**uit, selecteert u het knoop punt **automatische implementatie regels** en selecteert u vervolgens de gewenste regel.  

2.  Klik op het lint op **implementatie toevoegen**.   

3.  Configureer op de pagina **verzameling** van de wizard implementatie toevoegen de beschik bare instellingen op dezelfde manier als de pagina **Algemeen** van de wizard regel voor automatische implementatie maken. Zie de vorige sectie in het proces voor het [maken van een ADR](#bkmk_adr-process)voor meer informatie. De rest van de wizard implementatie toevoegen bevat de volgende pagina's, die ook overeenkomen met gedetailleerde beschrijvingen hierboven:  

     - Implementatie-instellingen
     - Implementatie planning
     - Gebruikerservaring
     - Waarschuwingen
     - Downloadinstellingen  

Implementaties kunnen ook programmatisch worden toegevoegd met behulp van Windows Power shell-cmdlets. Zie [New-CMSoftwareUpdateDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment) voor een volledige beschrijving van het gebruik van deze methode.

Zie [Implementatieproces voor software-updates](../understand/software-updates-introduction.md#BKMK_DeploymentProcess)voor meer informatie over het implementatieproces.


## <a name="next-steps"></a>Volgende stappen
[Software-updates controleren](monitor-software-updates.md)