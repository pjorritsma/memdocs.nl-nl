---
title: Software-updates handmatig implementeren
titleSuffix: Configuration Manager
description: Hand matig software-implementaties maken om uw clients up-to-date te krijgen met de vereiste software-updates of om out-of-band-updates te implementeren.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: b7d6640beb9353d5c613cf38e3f880e7fd76b393
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717088"
---
# <a name="manually-deploy-software-updates"></a>Software-updates handmatig implementeren  

*Van toepassing op: Configuration Manager (huidige vertakking)*

Een hand matige implementatie van software-updates is het proces van het selecteren van software-update in de Configuration Manager-console en het hand matig starten van het implementatie proces. U kunt ook de geselecteerde software-updates toevoegen aan een update groep en de update groep vervolgens hand matig implementeren. Normaal gesp roken gebruikt u hand matige implementaties om uw clients up-to-date te krijgen met de vereiste software-updates. Vervolgens gebruikt u de regels voor automatische implementatie (ADR) om lopende maandelijkse software-update-implementaties te beheren. Gebruik deze hand matige methode ook om out-of-band-software-updates te implementeren. Zie [software-updates implementeren](deploy-software-updates.md)voor meer informatie over welke implementatie methode het meest geschikt is voor u.



##  <a name="step-1-specify-search-criteria-for-software-updates"></a><a name="BKMK_1SearchCriteria"></a> Stap 1: zoekcriteria voor software-updates opgeven  

Afhankelijk van de combi Naties van producten en classificaties die uw site synchroniseert, zijn er mogelijk duizenden software-updates weer gegeven in de Configuration Manager-console. De eerste stap in de werkstroom voor het handmatig implementeren van software-updates is het identificeren van de software-updates die u wilt implementeren. U kunt bijvoorbeeld alle software-updates weer geven die vereist zijn op meer dan 50 client apparaten met een **beveiligings** -of **kritieke** classificatie.  

> [!IMPORTANT]  
>  Voor een implementatie van één software-update geldt een limiet van 1000 software-updates.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Proces voor het opgeven van zoek criteria voor software-updates  

1.  Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **software-updates**uit en klik op **alle software-updates**. Dit knoop punt geeft alle gesynchroniseerde software-updates weer.  

    > [!NOTE]  
    >  Het knoop punt **alle software-updates** geeft alleen software-updates weer met een **essentiële** en **beveiligings** classificatie die in de afgelopen 30 dagen zijn uitgebracht.  

2.  Filter in het zoek venster om de software-updates te identificeren die u nodig hebt. Gebruik een of beide van de volgende opties:  

    -   Typ in het zoekvak een zoek reeks die de software-updates filtert. Typ bijvoorbeeld het artikel of de Bulletin-ID voor een specifieke software-update. Of voer een teken reeks in die wordt weer gegeven in de titel van verschillende software-updates.  

    -   Klik op **criteria toevoegen**en selecteer de criteria om software-updates te filteren. Klik op **toevoegen**en geef de waarden voor de criteria op.  

3.  Klik op **Zoeken** om de software-updates te filteren.  

    > [!TIP]  
    >  Veelgebruikte filter criteria opslaan. Klik op het lint op de optie om de **huidige zoek opdracht**op te slaan. U haalt vorige Zoek opdrachten op door te klikken op **opgeslagen Zoek opdrachten**.   



##  <a name="step-2-create-a-software-update-group-that-contains-the-software-updates"></a><a name="BKMK_2UpdateGroup"></a> Stap 2: een software-updategroep maken die de software-updates bevat   

Met software-update groepen kunt u software-updates organiseren die worden voor bereid voor implementatie. Gebruik de volgende procedure om software-updates hand matig toe te voegen aan een nieuwe software-update groep.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Proces om software-updates hand matig toe te voegen aan een nieuwe software-update groep  

1.  Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** en selecteer **software-updates**. Selecteer de gewenste software-updates.  

2.  Klik op **Software-update groep maken** op het lint.  

3.  Geef de naam voor de software-updategroep en geef optioneel een beschrijving. Gebruik een naam en beschrijving die voldoende informatie bieden voor u om te bepalen welk type updates er in de software-update groep staan. Klik op **maken**.  

4.  Selecteer het knoop punt **Software-Update groepen** en selecteer de nieuwe software-update groep. Als u de lijst met updates in de groep wilt weer geven, klikt u op **leden weer geven** in het lint.  



##  <a name="step-3-download-the-content-for-the-software-update-group"></a><a name="BKMK_3DownloadContent"></a> Stap 3: de inhoud voor de software-updategroep downloaden  

Voordat u de software-updates implementeert, moet u de inhoud voor de software-updates in de software-update groep downloaden. Met deze stap kunt u controleren of de inhoud beschikbaar is op de distributie punten voordat u de software-updates implementeert. U kunt er ook voor zorgen dat er onverwachte problemen met de inhouds distributie optreden. Als u deze stap overs laat, wordt de-site als onderdeel van het implementatie proces de inhoud gedownload en gedistribueerd naar de distributie punten. Gebruik de volgende procedure om de inhoud voor software-updates in de software-updategroep te downloaden.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Het proces voor het downloaden van inhoud voor de software-update groep
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Proces voor het bewaken van de status van inhoud
1. Als u de status van de inhoud voor de software-updates wilt controleren, gaat u naar de werk ruimte **bewaking** in de Configuration Manager-console. Vouw **distributie status**uit en selecteer vervolgens het knoop punt **inhouds status** .  

2. Selecteer het software-updatepakket dat u eerder voor het downloaden van software-updates hebt geïdentificeerd in de software-updategroep.  

3. Klik op het lint op **status weer geven** .  



##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_4DeployUpdateGroup"></a>Stap 4: de software-update groep implementeren  

Nadat u hebt vastgesteld welke updates u wilt implementeren en deze aan een software-update groep wilt toevoegen, moet u de software-update groep hand matig implementeren.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Proces voor het hand matig implementeren van de software-updates in een software-update groep  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **software-updates**uit en selecteer het knoop punt software- **Update groepen** .  

2. Selecteer de software-update groep die u wilt implementeren. Klik op **implementeren** in het lint.   

3. Configureer de volgende instellingen op de pagina **Algemeen** van de wizard software-updates implementeren:  

   -   **Naam**: hier geeft u de naam op voor de implementatie. De implementatie moet een unieke naam hebben die het doel beschrijft en deze onderscheidt van andere implementaties in de-site. Dit naam veld heeft een limiet van 256 tekens. Standaard geeft Configuration Manager automatisch een naam voor de implementatie in de volgende indeling:`Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Beschrijving**: hier geeft u een beschrijving op voor de implementatie. De beschrijving is optioneel, maar biedt een overzicht van de implementatie. Neem eventuele andere relevante informatie op die u helpt om deze te identificeren en te onderscheiden van andere in de-site. Het beschrijvings veld heeft een limiet van 256 tekens en heeft standaard een lege waarde.  

   -   **Software-Update/software-update groep**: Controleer of de weer gegeven software-update groep of software-update juist is.  

   -   **Implementatie sjabloon selecteren**: hier geeft u op of een eerder opgeslagen implementatiesjabloon moet worden toegepast. Configureer een implementatie sjabloon om algemene eigenschappen van software-update-implementaties op te slaan. Pas vervolgens de sjabloon toe wanneer u in de toekomst software-updates implementeert. Deze sjablonen besparen tijd en helpen consistentie te garanderen tussen soort gelijke implementaties.  

   -   **Verzameling**: Geef de verzameling op voor de implementatie. Apparaten in de verzameling ontvangen de software-updates in deze implementatie.  

4. Configureer de volgende instellingen op de pagina **implementatie-instellingen** :  

   -   **Type implementatie**: hier geeft u het implementatietype voor de implementatie van de software-update op.  

       > [!IMPORTANT]  
       >  Nadat u de software-update-implementatie hebt gemaakt, kunt u het implementatie type niet wijzigen.  

        - Selecteer **vereist** om een verplichte software-update-implementatie te maken. De software-updates worden automatisch geïnstalleerd op clients vóór de installatie deadline die u configureert.  

        - Selecteer **beschikbaar** om een optionele software-update-implementatie te maken. Deze implementatie is beschikbaar voor gebruikers om te installeren vanuit software Center.  

       > [!NOTE]  
       >  Wanneer u een software-update groep implementeert zoals **vereist**, downloaden clients de inhoud op de achtergrond en voldoen de bits-instellingen, indien geconfigureerd.  
       > 
       > Voor software-update groepen die worden geïmplementeerd als **beschikbaar**, downloaden clients de inhoud op de voor grond en worden bits-instellingen genegeerd.  

   -   **Wake-on-LAN gebruiken om clients te laten ontwaken voor vereiste implementaties**: Hiermee geeft u op of Wake on LAN op de deadline moet worden ingeschakeld. Wake On LAN verzendt Ontwaak pakketten naar computers waarvoor een of meer software-updates in de implementatie zijn vereist. De site ontwaakt alle computers die zich in de slaap stand bevinden tijdens de deadline van de installatie, zodat de installatie kan worden gestart. Clients die zich in de slaap stand bevinden en geen software-updates nodig hebben in de implementatie, worden niet gestart. Deze instelling is standaard niet ingeschakeld. Het is alleen beschikbaar voor **vereiste** implementaties. Voordat u deze optie gebruikt, configureert u computers en netwerken voor Wake On LAN. Zie [Wake on LAN configureren](../../core/clients/deploy/configure-wake-on-lan.md)voor meer informatie.  

   -   **Detail niveau**: Geef het detail niveau op voor de status berichten die clients rapporteren aan de site.  

5. Configureer op de pagina **planning** de volgende instellingen:  

   -   **Evaluatie van planning**: Geef de tijd op die Configuration Manager de beschik bare tijd en deadline van de installatie wilt evalueren. Kies voor het gebruik van UTC (Coordinated Universal Time) of de lokale tijd van de computer waarop de Configuration Manager-console wordt uitgevoerd.  

       - Wanneer u hier **client lokale tijd** selecteert en vervolgens **zo spoedig mogelijk** selecteert voor de tijd waarop de **software beschikbaar**is, wordt de huidige tijd op de computer waarop de Configuration Manager-console wordt uitgevoerd, gebruikt om te evalueren wanneer er updates beschikbaar zijn. Dit gedrag is hetzelfde als de **installatie deadline** en de tijd waarop updates worden geïnstalleerd op een client. Als de client zich in een andere tijd zone bevindt, worden deze acties uitgevoerd wanneer de tijd van de client de evaluatie tijd heeft bereikt.  

   -   **Tijd waarop de software beschikbaar is**: selecteer een van de volgende instellingen om op te geven wanneer de software-updates beschikbaar worden gemaakt voor clients:  

       -   **Zo spoedig mogelijk**: maakt de software-updates in de implementatie zo spoedig mogelijk beschikbaar voor clients. Wanneer u de implementatie maakt terwijl deze instelling is geselecteerd, wordt het client beleid door Configuration Manager bijgewerkt. Bij de volgende polling cyclus van het client beleid worden clients op de hoogte van de implementatie en kunnen de software-updates beschikbaar zijn voor installatie.  

       -   **Specifiek tijdstip**: Hiermee worden software-updates die zijn opgenomen in de implementatie beschikbaar voor clients op een specifieke datum en tijd. Wanneer u de implementatie maakt terwijl deze instelling is ingeschakeld, wordt het client beleid door Configuration Manager bijgewerkt. Bij de volgende polling cyclus van het client beleid worden clients op de hoogte van de implementatie. De software-updates in de implementatie zijn echter pas na de geconfigureerde datum en tijd beschikbaar voor installatie.  

   -   **Installatie deadline**: deze opties zijn alleen beschikbaar voor **vereiste** implementaties. Selecteer een van de volgende instellingen om de installatie deadline op te geven voor de software-updates in de implementatie  

       -   **Zo spoedig mogelijk**: selecteer deze instelling als u wilt dat de software-updates in de implementatie zo spoedig mogelijk automatisch worden geïnstalleerd.  

       -   **Specifiek tijdstip**: selecteer deze instelling als u wilt dat de software-updates in de implementatie automatisch worden geïnstalleerd op een specifieke datum en tijd.  

           - De werkelijke duur van de installatie deadline is de weer gegeven deadline tijd plus een wille keurige hoeveelheid tijd tot twee uur. Met deze wille keuring vermindert u de potentiële impact van clients in de verzameling die tegelijkertijd updates in de implementatie installeren.   

           - Als u de vertraging voor wille keurige installatie wilt uitschakelen voor vereiste software-updates, configureert u de client instelling voor het **uitschakelen van deadline wille keurigheid** in de groep **computer agent** . Zie [client instellingen voor computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent)voor meer informatie.  

   -  **Het afdwingen van deze implementatie op basis van gebruikers voorkeuren uitstellen tot de respijt periode die in de client instellingen is gedefinieerd**: Schakel deze instelling in om gebruikers meer tijd te geven om de vereiste software-updates na de deadline te installeren.  

       - Dit gedrag is doorgaans vereist wanneer een computer gedurende een lange periode wordt uitgeschakeld en veel software-updates of toepassingen moeten worden geïnstalleerd. Wanneer een gebruiker bijvoorbeeld een vakantie retourneert, moet deze gedurende een lange periode worden gewacht wanneer de client achterstallige implementaties installeert.  

       - Deze respijt periode configureren met de **respijt periode van de eigenschap voor afdwinging na de deadline van de implementatie (uren)** in de client instellingen. Zie de sectie [computer agent](../../core/clients/deploy/about-client-settings.md#computer-agent) voor meer informatie. De respijt periode voor afdwinging is van toepassing op alle implementaties waarbij deze optie is ingeschakeld en is gericht op apparaten waarop u ook de client instelling hebt geïmplementeerd.  

       - Na de deadline installeert de client de software-updates in het eerste niet-zakelijke venster, dat door de gebruiker is geconfigureerd, tot deze respijt periode. De gebruiker kan echter nog steeds Software Center openen en de software-updates op elk gewenst moment installeren. Zodra de respijt periode is verlopen, wordt de afdwinging hersteld naar het normale gedrag voor achterstallige implementaties.  

6. Configureer op de pagina **gebruikers ervaring** de volgende instellingen:  

   -   **Meldingen voor gebruikers**: Geef op of meldingen in Software Center moeten worden weer gegeven op de geconfigureerde **tijd waarop de software beschikbaar is**. Met deze instelling bepaalt u ook of gebruikers op de client computers moeten worden gewaarschuwd. Voor **beschik bare** implementaties kunt u de optie om te **verbergen in Software Center en alle meldingen**niet selecteren.  

   -   **Deadline gedrag**: deze instelling kan alleen worden geconfigureerd voor **vereiste** implementaties. Geef het gedrag op wanneer de implementatie van de software-update de deadline bereikt buiten de gedefinieerde onderhouds Vensters. De opties omvatten of de software-updates moeten worden geïnstalleerd en of het systeem na de installatie opnieuw moet worden opgestart. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters. 
  
       > [!Note]
       > Dit geldt alleen wanneer het onderhouds venster is geconfigureerd voor het client apparaat. Als er geen onderhouds venster is gedefinieerd op het apparaat, wordt de update van de installatie en opnieuw opstarten altijd na de deadline uitgevoerd.

   -   **Gedrag voor opnieuw opstarten van apparaat**: deze instelling kan alleen worden geconfigureerd voor **vereiste** implementaties. Opgeven of opnieuw opstarten van het systeem op servers en werk stations moet worden onderdrukt als opnieuw opstarten is vereist om de installatie van de update te volt ooien.  

       > [!WARNING]  
       >  Het onderdrukken van het opnieuw opstarten van het systeem kan nuttig zijn in Server omgevingen of wanneer u niet wilt dat de doel computers standaard opnieuw worden opgestart. Hierdoor kunnen computers echter een onveilige status achterlaten. Het toestaan van een geforceerde herstart zorgt ervoor dat de installatie van de software-update onmiddellijk kan worden voltooid.  

   -   **Verwerking van schrijf filters voor Windows Embedded-apparaten**: met deze instelling bepaalt u het installatie gedrag op Windows Embedded-apparaten waarvoor een schrijf filter is ingeschakeld. Kies de optie om wijzigingen door te voeren bij de deadline van de installatie of tijdens een onderhouds venster. Wanneer u deze optie selecteert, moet de computer opnieuw worden opgestart en worden de wijzigingen op het apparaat bewaard. Anders wordt de update geïnstalleerd, toegepast op de tijdelijke overlay en later vastgelegd.  

       -  Wanneer u een software-update implementeert op een Windows Embedded-apparaat, moet u ervoor zorgen dat het apparaat lid is van een verzameling met een geconfigureerd onderhouds venster.  

   - **Gedrag van nieuwe evaluatie van software-updates bij opnieuw opstarten**: Selecteer deze instelling om implementaties van software-updates te configureren zodat clients onmiddellijk na de installatie van software-updates een scan voor de compatibiliteit van software-updates uitvoeren. Met deze instelling kan de client controleren op aanvullende updates die van toepassing zijn nadat de client opnieuw is opgestart. vervolgens worden ze geïnstalleerd tijdens hetzelfde onderhouds venster.  

7. Configureer op de pagina **waarschuwingen** hoe Configuration Manager waarschuwingen genereert voor deze implementatie. Bekijk de recente waarschuwingen voor software-updates van Configuration Manager in het knoop punt **software-updates** van de werk ruimte **software bibliotheek** . Als u ook System Center Operations Manager gebruikt, moet u de waarschuwingen ook configureren. Configureer alleen waarschuwingen voor **vereiste** implementaties.  

8. Configureer de volgende instellingen op de pagina **Download instellingen** :  

    > [!NOTE]  
    >  Clients vragen de inhoudlocatie aan bij het beheerpunt voor de software-updates in een implementatie. Het Download gedrag is afhankelijk van hoe u het distributie punt, het implementatie pakket en de instellingen op deze pagina hebt geconfigureerd.  

    - Geef op of clients de updates moeten downloaden en installeren wanneer ze een distributie punt van een neighbor of de standaard site grens groepen gebruiken.  

    - Geef op of clients de updates moeten downloaden en installeren vanaf een distributie punt in de standaard grens groep van de site, wanneer de inhoud voor de software-updates niet beschikbaar is vanaf een distributie punt in de huidige of grens groepen van de buur.  

    - **Clients toestaan inhoud te delen met andere clients in hetzelfde subnet**: hier kunt u aangeven of het gebruik van BranchCache moet worden ingeschakeld voor het downloaden van inhoud. Zie [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)voor meer informatie. Vanaf versie 1802 is BranchCache altijd ingeschakeld op clients. Deze instelling wordt verwijderd omdat clients BranchCache gebruiken als het distributie punt deze ondersteunt.  

    - **Als er geen software-updates beschikbaar zijn op het distributie punt in de huidige, naburige of site grens groepen, downloadt u inhoud van micro soft-updates**: Selecteer deze instelling als u wilt dat clients met een intranet software-updates downloaden van Microsoft Update als er geen updates beschikbaar zijn op distributie punten. Clients op Internet gaan altijd naar Microsoft Update voor inhoud van software-updates.

    - Geef op of clients mogen downloaden na een installatie deadline wanneer deze Internet verbindingen met een Data limiet gebruiken. Internet providers worden soms kosten in rekening gebracht op basis van de hoeveelheid gegevens die u verzendt en ontvangt wanneer u gebruikmaakt van een verbinding met een Data limiet.  

9. Selecteer op de pagina **implementatie pakket** een van de volgende opties:  

    > [!Note]  
    > Als u stap 3 al hebt uitgevoerd [: de inhoud voor de software-update groep downloaden](#BKMK_3DownloadContent), worden de pagina's **implementatie pakket**, **distributie punten**en **taal selectie** niet weer gegeven in de wizard. Ga naar de pagina [samen vatting](#bkmk_summary) van de wizard.  
    > 
    >  Software-updates die eerder naar de inhouds bibliotheek op de site server zijn gedownload, worden niet opnieuw gedownload. Dit gedrag geldt ook wanneer u een nieuw implementatie pakket voor de software-updates maakt. Als alle software-updates al zijn gedownload, slaat de wizard over naar de pagina [samen vatting](#bkmk_summary) .  

    - **Een implementatie pakket selecteren**: Voeg deze updates toe aan een bestaand implementatie pakket.  

    - **Een nieuw implementatie pakket maken**: Voeg deze updates toe aan een nieuw implementatie pakket. Configureer de volgende aanvullende instellingen:  

        -  **Naam**: geef de naam op van het implementatiepakket. Gebruik een unieke naam die de pakket inhoud beschrijft. Het is beperkt tot 50 tekens.  

        -  **Beschrijving**: geef een beschrijving op die informatie biedt over het implementatiepakket. De optionele beschrijving is beperkt tot 127 tekens.  

        -  **Pakketbron**: geef de locatie op van de bronbestanden van de software-update. Typ een netwerkpad voor de bron locatie, bijvoorbeeld `\\server\sharename\path`, of klik op **Bladeren** om de netwerk locatie te zoeken. Maak de gedeelde map voor de bron bestanden van het implementatie pakket voordat u doorgaat naar de volgende pagina.  

            - U kunt de opgegeven locatie niet gebruiken als de bron van een ander software-implementatie pakket.  

            - U kunt de pakket bron locatie wijzigen in de eigenschappen van het implementatie pakket nadat Configuration Manager het implementatie pakket hebt gemaakt. Als dit het geval is, kopieert u eerst de inhoud van de oorspronkelijke pakket bron naar de nieuwe pakket bron locatie.  

            -  De computer account van de SMS-provider en de gebruiker die de wizard uitvoert om de software-updates te downloaden, moeten beide **Schrijf** machtigingen hebben voor de download locatie. Beperk de toegang tot de download locatie. Deze beperking vermindert het risico van aanvallers die knoeien met de bron bestanden van de software-update.  

        -  **Prioriteit voor verzenden**: geef de prioriteit op voor verzenden van het implementatiepakket. Configuration Manager gebruikt deze prioriteit wanneer het pakket naar distributie punten wordt verzonden. Implementatie pakketten worden in volg orde van prioriteit verzonden: hoog, gemiddeld of laag. Pakketten met een identieke prioriteit worden verzonden in de volgorde waarin deze zijn gemaakt. Als er geen achterstand is, wordt het pakket onmiddellijk verwerkt, ongeacht de prioriteit.  

        - **Binary Differential Replication inschakelen**: Schakel deze instelling in om netwerk verkeer tussen sites te minimaliseren. Met binaire Differentiële replicatie (BDR) wordt alleen de inhoud bijgewerkt die is gewijzigd in het pakket, in plaats van de hele pakket inhoud bij te werken. Zie [binaire Differentiële replicatie](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication)voor meer informatie.  

    - **Geen implementatie pakket**: vanaf versie 1806 kunt u software-updates implementeren op apparaten zonder eerst inhoud te downloaden en te distribueren naar distributie punten. Deze instelling is nuttig bij het verwerken van extreem grote update-inhoud. Gebruik dit ook wanneer u altijd wilt dat clients inhoud ophalen van de Microsoft Update Cloud service. Clients in dit scenario kunnen ook inhoud downloaden van peers die al over de benodigde inhoud beschikken. De Configuration Manager-client blijft het downloaden van de inhoud blijven beheren, maar kan ook gebruikmaken van de functie voor Configuration Manager peer-cache of andere technologieën zoals Delivery Optimization. Deze functie ondersteunt elk update type dat wordt ondersteund door Configuration Manager beheer van software-updates, waaronder Windows-en Office-updates.<!--1357933-->  

10. Geef op de pagina **distributie punten** de distributie punten of distributiepunten groepen op om de software-update bestanden te hosten. Zie [Configuraties van het distributiepunt](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)voor meer informatie over distributiepunten.  

    > [!Note]  
    > Als u stap 3 al hebt uitgevoerd [: de inhoud voor de software-update groep downloaden](#BKMK_3DownloadContent), worden de pagina's **implementatie pakket**, **distributie punten**en **taal selectie** niet weer gegeven in de wizard. Ga naar de pagina [samen vatting](#bkmk_summary) van de wizard.  

11. Geef op de pagina **Download locatie** op of de software-update bestanden moeten worden gedownload vanaf internet of vanaf uw lokale netwerk. Configureer de volgende instellingen:  

    -   **Software-updates downloaden van Internet**: Selecteer deze instelling om de software-updates te downloaden vanaf een opgegeven locatie op internet. Deze instelling is standaard ingeschakeld.  

    -   **Software-updates downloaden vanaf een locatie op het lokale netwerk**: selecteer deze instelling als u wilt dat de software-updates worden gedownload vanuit een lokale map of een gedeelde map. Deze instelling is nuttig wanneer de computer waarop de wizard wordt uitgevoerd, geen toegang tot internet heeft. Elke computer met Internet toegang kan tijdig downloaden van de software-updates. Sla ze vervolgens op in een locatie op het lokale netwerk die toegankelijk is vanaf de computer waarop de wizard wordt uitgevoerd.  

12. Selecteer op de pagina **taal** selecteren de talen waarvoor de site de geselecteerde software-updates downloadt. De site downloadt deze updates alleen als deze beschikbaar zijn in de geselecteerde talen. Software-updates die niet taalspecifiek zijn, worden altijd gedownload. De wizard selecteert standaard de talen die u hebt geconfigureerd in de eigenschappen van het software-update punt. Er moet ten minste één taal worden geselecteerd voordat u doorgaat naar de volgende pagina. Wanneer u alleen talen selecteert die niet door een software-update worden ondersteund, mislukt het downloaden van de update.  

    > [!Note]  
    > Als u stap 3 al hebt uitgevoerd [: de inhoud voor de software-update groep downloaden](#BKMK_3DownloadContent), worden de pagina's **implementatie pakket**, **distributie punten**en **taal selectie** niet weer gegeven in de wizard. Ga naar de pagina [samen vatting](#bkmk_summary) van de wizard.  

13. <a name="bkmk_summary"></a>Controleer de instellingen op de pagina **samen vatting** . Klik op **Opslaan als sjabloon**om de instellingen op te slaan in een implementatie sjabloon. Voer een naam in en selecteer de instellingen die u in de sjabloon wilt gebruiken en klik vervolgens op **Opslaan**. Als u een geconfigureerde instelling wilt wijzigen, klikt u op de gekoppelde wizardpagina en wijzigt u de instelling.  

    -  De sjabloon naam kan bestaan uit alfanumerieke ASCII-tekens en `\` (backslash) of `'` (enkele aanhalings tekens).  

14. Klik op **Volgende** om de software-update te implementeren.  

    Nadat u de wizard hebt voltooid, worden de software-updates door Configuration Manager gedownload naar de inhouds bibliotheek op de site server. Vervolgens wordt de inhoud gedistribueerd naar de geconfigureerde distributie punten en wordt de software-update groep geïmplementeerd voor clients in de doel verzameling. Zie [Implementatieproces voor software-updates](../understand/software-updates-introduction.md#BKMK_DeploymentProcess)voor meer informatie over het implementatieproces.  



## <a name="next-steps"></a>Volgende stappen
[Software-updates controleren](monitor-software-updates.md)
