1.  Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** en selecteer het knoop punt **software-updates** .  

2.  Gebruik een van de volgende methoden om de gewenste software-update te kiezen:  

    -   Selecteer een of meer software-update groepen in het knoop punt **Software-Update groepen** . Klik vervolgens op **downloaden** op het lint.  

    -   Selecteer een of meer software-updates van het knoop punt **software-updates** . Klik vervolgens op **downloaden** op het lint.  

        > [!NOTE]  
        >  In het knoop punt **alle software-updates** worden met Configuration Manager alleen software-updates weer gegeven met een **essentiële** en **beveiligings** classificatie die in de afgelopen 30 dagen zijn uitgebracht.  

        > [!TIP]  
        >  Klik op **criteria toevoegen** om de software-updates te filteren die worden weer gegeven in het knoop punt **alle software-updates** . Sla zoek criteria die u vaak gebruikt op en beheer opgeslagen Zoek opdrachten op het tabblad **zoeken** .  


3.  Configureer op de pagina **implementatie pakket** van de wizard software-updates downloaden de volgende instellingen:  

    -  **Implementatiepakket selecteren**: kies deze instelling om een bestaand implementatiepakket te selecteren voor de software-updates in de implementatie.  

        > [!NOTE]  
        >  Software-updates die door de site al naar het geselecteerde implementatie pakket zijn gedownload, worden niet opnieuw gedownload.  

    -  **Nieuw implementatiepakket maken**: selecteer deze instelling als u een nieuw implementatiepakket wilt maken voor de software-updates in de implementatie. Configureer de volgende instellingen:  

        -   **Naam**: hiermee geeft u de naam van het implementatiepakket op. Dit moet een unieke naam zijn die de pakketinhoud kort beschrijft. Het is beperkt tot 50 tekens.  

        -   **Beschrijving**: geef een beschrijving op die informatie biedt over het implementatiepakket. De optionele beschrijving is beperkt tot 127 tekens.    

        -   **Pakketbron**: hiermee geeft u de locatie op van de bronbestanden van de software-update. Typ een netwerkpad voor de bron locatie, bijvoorbeeld `\\server\sharename\path`, of klik op **Bladeren** om de netwerk locatie te zoeken. Maak de gedeelde map voor de bron bestanden van het implementatie pakket voordat u doorgaat naar de volgende pagina.  

             - U kunt de opgegeven locatie niet gebruiken als de bron van een ander software-implementatie pakket.  

             - U kunt de pakket bron locatie wijzigen in de eigenschappen van het implementatie pakket nadat Configuration Manager het implementatie pakket hebt gemaakt. Als dit het geval is, kopieert u eerst de inhoud van de oorspronkelijke pakket bron naar de nieuwe pakket bron locatie.  

             -  De computer account van de SMS-provider en de gebruiker die de wizard uitvoert om de software-updates te downloaden, moeten beide **Schrijf** machtigingen hebben voor de download locatie. Beperk de toegang tot de download locatie. Deze beperking vermindert het risico van aanvallers die knoeien met de bron bestanden van de software-update.  

        - **Binary Differential Replication inschakelen**: Schakel deze instelling in om netwerk verkeer tussen sites te minimaliseren. Met binaire Differentiële replicatie (BDR) wordt alleen de inhoud bijgewerkt die is gewijzigd in het pakket, in plaats van de hele pakket inhoud bij te werken. Zie [binaire Differentiële replicatie](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication)voor meer informatie.  

4.  Geef op de pagina **distributie punten** de distributie punten of distributiepunten groepen op om de software-update bestanden te hosten. Zie [Configuraties van het distributiepunt](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)voor meer informatie over distributiepunten. Deze pagina is alleen beschikbaar wanneer u een nieuw implementatiepakket voor software-updates maakt.  

5.  De pagina **distributie-instellingen** is alleen beschikbaar wanneer u een nieuw implementatie pakket voor software-updates maakt. Geef de volgende instellingen op:  

    -   **Distributieprioriteit**: met deze instelling geeft u de distributieprioriteit voor het implementatiepakket op. De distributieprioriteit is van toepassing wanneer het implementatiepakket naar distributiepunten op onderliggende sites wordt verzonden. Implementatie pakketten worden in volg orde van prioriteit verzonden: hoog, gemiddeld of laag. Pakketten met een identieke prioriteit worden verzonden in de volgorde waarin deze zijn gemaakt. Als er geen achterstand is, wordt het pakket onmiddellijk verwerkt, ongeacht de prioriteit. Standaard verzendt de site pakketten met een **gemiddelde** prioriteit.  

    -   **Inschakelen voor distributie op aanvraag**: gebruik deze instelling om inhouds distributie op aanvraag in te scha kelen naar distributie punten die zijn geconfigureerd voor deze functie en in de huidige grens groep van de client. Wanneer u deze instelling inschakelt, maakt het beheer punt een trigger voor de distributie beheerder om de inhoud naar al deze distributie punten te distribueren wanneer een client de inhoud voor het pakket aanvraagt en de inhoud niet beschikbaar is. Zie [inhoud distribueren op aanvraag](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)voor meer informatie.  

    -   **Instellingen voorbereid distributiepunt**: met deze instelling geeft u op hoe u inhoud naar voorbereide distributiepunten wilt distribueren. Kies een van de volgende opties:  

        -   **Automatisch inhoud downloaden wanneer pakketten worden toegewezen aan distributiepunten**: met deze instelling negeert u de voorbereide instellingen en distribueert u inhoud naar het distributiepunt.   

        -   **Alleen inhoudswijzigingen downloaden naar het distributiepunt**: gebruik deze instelling om de initiële inhoud voor het distributiepunt voor te bereiden en vervolgens inhoudswijzigingen naar het distributiepunt te distribueren.  

        -   **De inhoud in dit pakket handmatig kopiëren naar het distributiepunt**: gebruik deze instelling om inhoud altijd voor te bereiden op het distributiepunt. Dit is de standaardoptie.  

        Zie [Vooraf geplaatste inhoud gebruiken](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)voor meer informatie over het vooraf plaatsen van inhoud op distributiepunten.  


6.  Geef op de pagina **Download locatie** de locatie op die Configuration Manager gebruikt voor het downloaden van de bron bestanden van de software-update. Gebruik een van de volgende opties:  

    -   **Software-updates downloaden van Internet**: Selecteer deze instelling om de software-updates te downloaden vanaf de locatie op internet. Dit is de standaardoptie.  

    -   **Software-updates downloaden van een locatie op mijn netwerk**: Selecteer deze instelling om de software-updates te downloaden uit een lokale map of een gedeelde map. Deze instelling is nuttig wanneer de computer waarop de wizard wordt uitgevoerd, geen toegang tot internet heeft. Elke computer met Internet toegang kan tijdig downloaden van de software-updates. Sla ze vervolgens op in een locatie op het lokale netwerk die toegankelijk is vanaf de computer waarop de wizard wordt uitgevoerd.  


7.  Selecteer op de pagina **taal** selecteren de talen waarvoor de site de geselecteerde software-updates downloadt. De site downloadt deze updates alleen als deze beschikbaar zijn in de geselecteerde talen. Software-updates die niet taalspecifiek zijn, worden altijd gedownload. De wizard selecteert standaard de talen die u hebt geconfigureerd in de eigenschappen van het software-update punt. Er moet ten minste één taal worden geselecteerd voordat u doorgaat naar de volgende pagina. Wanneer u alleen talen selecteert die niet door een software-update worden ondersteund, mislukt het downloaden van de update.  

8. Controleer op de pagina **samen vatting** de instellingen die u in de wizard hebt geselecteerd en klik vervolgens op **volgende** om de software-updates te downloaden.  

9. Controleer op de pagina **voltooiing** of de software-updates zijn gedownload en klik vervolgens op **sluiten**.  
