---
title: Takenreeksen beheren
titleSuffix: Configuration Manager
description: Maken, bewerken, implementeren, importeren en exporteren van taken reeksen om ze te beheren en taken in uw omgeving te automatiseren.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b38b0c8f28645fa0aae66058b0c93bd8beffc470
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078478"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Takenreeksen beheren om taken te automatiseren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik taken reeksen om stappen in uw Configuration Manager omgeving te automatiseren. Met deze stappen kunt u een installatie kopie van een besturings systeem implementeren op een doel computer, een installatie kopie van een besturings systeem bouwen en vastleggen vanuit een reeks installatie bestanden van het besturings systeem, en gebruikers status informatie vastleggen en herstellen. Taken reeksen bevinden zich in de Configuration Manager-console. Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer **taken reeksen**. Het knoop punt **taken reeksen** , inclusief de submappen die u maakt, wordt gerepliceerd in de Configuration Manager hiërarchie. Zie [plannings overwegingen voor het automatiseren van taken](../plan-design/planning-considerations-for-automating-tasks.md)voor plannings informatie.  

## <a name="create"></a><a name="BKMK_CreateTaskSequence"></a>Creëren

Maak takenreeksen via de wizard Takenreeks maken. Met deze wizard kunt u de volgende typen takenreeksen maken:  

- [Taken reeks voor het installeren van een besturings systeem](create-a-task-sequence-to-install-an-operating-system.md): Maak de stappen voor het installeren van een besturings systeem. Het bevat ook opties voor het migreren van gebruikers gegevens, het opnemen van software-updates en het installeren van toepassingen.

- [Taken reeks voor het upgraden van een besturings systeem](create-a-task-sequence-to-upgrade-an-operating-system.md): Maak de stappen om een besturings systeem bij te werken. Het bevat ook opties voor het opnemen van software-updates en het installeren van toepassingen.

- [Taken reeks voor het vastleggen van een besturings systeem](create-a-task-sequence-to-capture-an-operating-system.md): Maak de stappen voor het bouwen en vastleggen van een besturings systeem vanaf een referentie computer. U kunt software-updates opnemen en toepassingen installeren op de referentie computer voordat u de installatie kopie vastlegt.

- [Taken reeks voor het vastleggen en herstellen van de gebruikers status](create-a-task-sequence-to-capture-and-restore-user-state.md): Voeg stappen toe aan een bestaande taken reeks om gebruikers status gegevens vast te leggen en te herstellen.

- [Aangepaste taken reeks](create-a-custom-task-sequence.md): dit type voegt geen stappen toe aan de taken reeks. Nadat u deze taken reeks hebt gemaakt, bewerkt u deze en voegt u stappen toe.

## <a name="edit"></a><a name="BKMK_ModifyTaskSequence"></a>Wijzigt  

U kunt een taken reeks wijzigen door stappen toe te voegen of te verwijderen, groepen toe te voegen of te verwijderen of door de volg orde van de stappen te wijzigen. Zie [de taken reeks editor gebruiken](../understand/task-sequence-editor.md)voor meer informatie.

## <a name="software-center-properties"></a><a name="bkmk_prop-general"></a>Eigenschappen van software Center

Gebruik de volgende procedure om de details te configureren voor de taken reeks die wordt weer gegeven in Software Center. Deze details zijn alleen ter informatie.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer **taken reeksen**.  

2. Selecteer de taken reeks die u wilt bewerken en selecteer **Eigenschappen**.  

3. Op het tabblad **Algemeen** zijn de volgende instellingen voor Software Center beschikbaar:  

    - **Opnieuw opstarten vereist**: Hiermee geeft u aan dat de gebruiker weet of opnieuw opstarten is vereist tijdens de installatie.  

    - **Download grootte (MB)**: Hiermee geeft u op hoeveel mega bytes in Software Center voor de taken reeks worden weer gegeven.  

    - **Geschatte uitvoerings tijd (minuten)**: Hiermee geeft u de geschatte uitvoerings tijd in minuten op die wordt weer gegeven in Software Center voor de taken reeks.  

## <a name="advanced-settings"></a><a name="bkmk_prop-advanced"></a>Geavanceerde instellingen

Gebruik de volgende procedure om het gedrag van de taken reeks op de Configuration Manager-client te configureren.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer **taken reeksen**.  

2. Selecteer de taken reeks die u wilt bewerken en selecteer **Eigenschappen**.  

3. Op het tabblad **Geavanceerd** zijn de volgende instellingen beschikbaar:  

    - **Eerst een ander programma uitvoeren**: Selecteer deze optie als u een programma in een ander pakket wilt uitvoeren voordat de taken reeks wordt uitgevoerd. Standaard is dit selectievakje niet geselecteerd. U hoeft het door u opgegeven programma niet afzonderlijk te implementeren om het eerst uit te voeren.  

        > [!IMPORTANT]
        > Deze instelling geldt alleen voor taken reeksen die in het volledige besturings systeem worden uitgevoerd. Als u de taken reeks start met behulp van PXE-of opstart media, wordt deze instelling door Configuration Manager genegeerd.  

        - **Pakket**: Blader naar het pakket dat het programma bevat dat moet worden uitgevoerd vóór deze taken reeks.  

        - **Programma**: Selecteer het programma dat moet worden uitgevoerd vóór deze taken reeks.  

        > [!NOTE]  
        > Als het geselecteerde programma niet kan worden uitgevoerd op een client, wordt de taken reeks niet uitgevoerd. Als het geselecteerde programma correct wordt uitgevoerd, wordt het niet opnieuw uitgevoerd, zelfs niet als de taken reeks opnieuw op dezelfde client wordt gestart.  

    - **Taken reeks meldingen onderdrukken**: Selecteer deze optie om de **nieuwe software** te verbergen pop-upmelding. Het pictogram **nieuwe software** wordt nog steeds weer geven in Software Center in het systeemvak. Deze optie is standaard uitgeschakeld.  

    - **Deze taken reeks uitschakelen op computers waarop deze wordt geïmplementeerd**: als u deze optie selecteert, schakelt Configuration Manager alle implementaties die deze taken reeks bevatten, tijdelijk uit. Ook wordt de taken reeks verwijderd uit de lijst met implementaties die kunnen worden uitgevoerd. De taken reeks wordt niet uitgevoerd totdat u deze inschakelt. Deze optie is standaard uitgeschakeld.  

    - **Maxi maal toegestane uitvoerings tijd**: Hiermee geeft u de maximale tijd in minuten op dat de taken reeks op de doel computer wordt uitgevoerd. Gebruik een geheel getal dat gelijk is aan of groter is dan nul. Deze waarde is standaard 120 minuten.  

        > [!IMPORTANT]  
        > Als u onderhouds Vensters gebruikt voor de verzameling waarnaar u deze taken reeks implementeert, kan er een conflict optreden als de **maximale toegestane uitvoerings tijd** langer is dan het geplande onderhouds venster. Als u de maximale uitvoerings tijd instelt op **0**, wordt de taken reeks gestart tijdens het onderhouds venster. Het proces blijft actief totdat het is voltooid of mislukt nadat het onderhouds venster is gesloten. Als gevolg hiervan kunnen taken reeksen met een maximale uitvoerings tijd die is ingesteld op **0** , na het einde van hun onderhouds Vensters worden uitgevoerd. Als u de maximale uitvoerings tijd instelt op een specifieke periode (niet-nul) die de lengte van een beschikbaar onderhouds venster overschrijdt, wordt die taken reeks niet uitgevoerd. Zie [onderhouds Vensters gebruiken](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie.  

        Als u de waarde instelt op **0**, Configuration Manager evalueert de Maxi maal toegestane uitvoerings tijd van **12** uur (720 minuten) voor de voortgang van de bewaking. De taken reeks begint echter als de aftel tijd niet groter is dan de waarde van het onderhouds venster.  

        > [!NOTE]
        > Als u de maximale uitvoerings tijd bereikt en u niet toestaat dat gebruikers met een vereiste implementatie werken, wordt de taken reeks door Configuration Manager gestopt. Als de taken reeks zelf niet is gestopt, wordt de bewaking van de taken reeks door Configuration Manager gestopt na het bereiken van de Maxi maal toegestane uitvoerings tijd.

    - **Een opstart installatie kopie gebruiken**: de geselecteerde opstart installatie kopie gebruiken wanneer de taken reeks wordt uitgevoerd. Selecteer **Bladeren** om een andere opstart installatie kopie te selecteren. Schakel deze optie uit als u het gebruik van de geselecteerde opstart installatie kopie wilt uitschakelen wanneer de taken reeks wordt uitgevoerd.  

    - **Deze taken reeks kan op elk platform worden uitgevoerd**: als u deze optie selecteert, wordt het platform type van de doel computer niet door Configuration Manager gecontroleerd wanneer de taken reeks wordt uitgevoerd. Deze optie is standaard ingeschakeld.  

    - **Deze taken reeks kan alleen worden uitgevoerd op de opgegeven client platforms**: met deze optie geeft u de processors, versies van besturings systemen en service packs op waarop deze taken reeks kan worden uitgevoerd. Wanneer u deze optie selecteert, selecteert u ten minste één platform in de lijst. Standaard zijn er geen platformen geselecteerd. Configuration Manager gebruikt deze informatie wanneer wordt geëvalueerd welke doel computers in een verzameling de geïmplementeerde taken reeks ontvangen.  

        > [!NOTE]  
        > Wanneer u een taken reeks uitvoert vanuit opstart media of PXE, Configuration Manager deze optie genegeerd. De taken reeks wordt uitgevoerd alsof de optie **dit programma kan worden uitgevoerd op elk platform** is geselecteerd.  

## <a name="high-impact-settings"></a>Instellingen met hoge impact

Configureer een taken reeks als hoge impact en pas de berichten aan die gebruikers ontvangen wanneer ze de taken reeks uitvoeren.

> [!WARNING]
> Als u PXE-implementaties gebruikt en de hardware van het apparaat configureert met de netwerk adapter als het eerste opstart apparaat, kunnen deze apparaten automatisch een taken reeks voor besturingssysteem implementatie starten zonder tussen komst van de gebruiker. Deze configuratie wordt niet beheerd door implementatie verificatie. Hoewel deze configuratie het proces kan vereenvoudigen en de gebruikers interactie vermindert, wordt het apparaat voor een groter risico voor onbedoelde herinstallatie kopieën geplaatst.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Een taken reeks instellen als een taken reeks met hoge impact

Gebruik de volgende procedure om een taken reeks als hoge impact in te stellen.

> [!NOTE]  
> Elke taken reeks die aan bepaalde voor waarden voldoet, wordt automatisch gedefinieerd als hoge impact. Zie [implementaties met een hoog risico beheren](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer **taken reeksen**.  

2. Selecteer de taken reeks die u wilt bewerken en selecteer **Eigenschappen**.  

3. Op het tabblad **gebruikers melding** selecteert u **Dit is een taken reeks met hoge impact**.  

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Een aangepaste melding maken voor implementaties met een hoog risico

Gebruik de volgende procedure om een aangepaste melding te maken voor implementaties met hoge impact.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer **taken reeksen**.  

2. Selecteer de taken reeks die u wilt bewerken en selecteer **Eigenschappen**.  

3. Op het tabblad **gebruikers melding** selecteert **u aangepaste tekst gebruiken**.  

    > [!NOTE]
    > U kunt alleen tekst van de gebruikers melding instellen wanneer u de optie selecteert. **Dit is een zeer grote taak reeks**.  

4. Configureer de volgende instellingen:  

    > [!Note]  
    > Elk tekstvak heeft een maximum limiet van 255 tekens.  

    - **Kopregel tekst van gebruikers melding**: Hiermee geeft u de blauwe tekst op die wordt weer gegeven op de gebruikers melding van het Software Center. In de standaard gebruikers melding bevat deze sectie bijvoorbeeld "Bevestig dat u het besturings systeem op deze computer wilt upgraden."  

    - **Bericht tekst van gebruikers melding**: er zijn drie tekst vakken die de hoofd tekst van de aangepaste melding geven. Voor alle tekst vakken moet u tekst toevoegen.  

        - Eerste tekstvak: Hiermee geeft u de hoofd tekst op, meestal met instructies voor de gebruiker. In de standaard gebruikers melding bevat deze sectie bijvoorbeeld ' upgrade van het besturings systeem uitvoeren en kan uw computer enkele keren opnieuw worden opgestart '.  

        - Tweede tekstvak: Hiermee wordt de vetgedrukte tekst onder de hoofd tekst weer gegeven. In de standaard gebruikers melding bevat deze sectie bijvoorbeeld ' this in-place upgrade het nieuwe besturings systeem installeert en worden uw apps, gegevens en instellingen automatisch gemigreerd. '  

        - Derde tekstvak: Hiermee geeft u de laatste regel tekst onder de vetgedrukte tekst op. In de standaard gebruikers melding bevat deze sectie bijvoorbeeld ' Klik op installeren om te beginnen. Klik anders op Annuleren.  

#### <a name="example"></a>Voorbeeld

Stel dat u de volgende aangepaste melding wilt configureren in eigenschappen.

![Tabblad Aangepaste gebruikers melding van taken reeks eigenschappen](../media/user-notification.png)

Het volgende meldings bericht wordt weer gegeven wanneer de eind gebruiker de installatie opent vanuit software Center.

![Aangepaste taken reeks melding voor de eind gebruiker vanuit software Center](../media/user-notification-enduser.png)

## <a name="performance-improvements-for-power-plans"></a><a name="bkmk_perf"></a>Prestatie verbeteringen voor energiebeheer schema's

<!--3555926-->

Vanaf versie 1910 kunt u nu een taken reeks uitvoeren met het energiebeheer schema voor hoge prestaties. Met deze optie wordt de totale snelheid van de taken reeks verbeterd. Windows wordt geconfigureerd voor het gebruik van het ingebouwde energiebeheer schema voor hoge prestaties, dat maximale prestaties levert voor de kosten van een hoger energie verbruik. Deze optie is standaard ingeschakeld voor nieuwe taken reeksen.

Wanneer de taken reeks wordt gestart, wordt in de meeste scenario's het ingeschakelde energiebeheer schema vastgelegd. Vervolgens wordt het actieve energiebeheer schema overgeschakeld naar het Windows-standaard abonnement voor **hoge prestaties** . Als de taken reeks de computer opnieuw opstart, wordt dit proces herhaald. Aan het einde van de taken reeks wordt het energiebeheer schema opnieuw ingesteld op de opgeslagen waarde. Deze functionaliteit werkt in Windows en Windows PE, maar heeft geen invloed op virtuele machines.

- Als de taken reeks wordt gestart in Windows PE, registreert de taken reeks niet het energiebeheer schema dat momenteel is ingeschakeld voor later gebruik.

- Met een besturingssysteem implementatie taken reeks waarmee de installatie kopie van de computer (wissen en laden) wordt verwijderd, blijft de instelling voor het energiebeheer schema van het oude besturings systeem niet behouden. Aan het einde van de taken reeks wordt het standaard schema voor **evenwichtige** energie hersteld.

> [!Important]
> Als u wilt profiteren van deze nieuwe Configuration Manager functie, moet u na het bijwerken van de site de clients bijwerken naar de nieuwste versie. Werk installatie kopieën ook bij om de nieuwste client onderdelen op te kunnen gebruiken. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **besturings systemen**uit en selecteer het knoop punt **taken reeksen** .

1. Maak of kies een bestaande taken reeks en selecteer vervolgens **Eigenschappen**.

1. Ga naar het tabblad **prestaties** .

1. Schakel de optie in om uit te **voeren als energiebeheer schema met hoge prestaties**.

> [!Warning]
> Wees voorzichtig met deze instelling op hardware met lage prestaties. Het uitvoeren van intensieve systeem bewerkingen gedurende lange tijd kan een lage hoeveelheid hardware zijn. Neem contact op met de hardwarefabrikant voor specifieke richt lijnen.

### <a name="known-issue"></a>Bekend probleem

<!-- 5554928 -->

U moet een nieuwe taken reeks implementatie maken om deze instelling in of uit te scha kelen voor hoge prestaties. De nieuwe instelling wordt weer gegeven op bestaande implementaties, maar is niet van toepassing.<!-- SCCMDocs#2107 -->

## <a name="distribute-referenced-content"></a><a name="BKMK_DistributeTS"></a>Inhoud waarnaar wordt verwezen distribueren  

Voordat clients een taken reeks uitvoeren die naar inhoud verwijst, distribueert u die inhoud naar distributie punten. U kunt op elk gewenst moment de takenreeks selecteren en de bijbehorende inhoud distribueren om een nieuwe lijst met referentiepakketten voor distributie te bouwen. Als u wijzigingen aanbrengt in de taken reeks met bijgewerkte inhoud, moet u de inhoud opnieuw distribueren voordat deze beschikbaar is voor clients. Gebruik de volgende procedure om de inhoud te distribueren waarnaar een takenreeks verwijst.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Proces voor het distribueren van inhoud waarnaar wordt verwezen naar distributie punten  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

2. Selecteer in de lijst **Takenreeks** de takenreeks die u wilt distribueren.  

3. Klik op het tabblad **Start** van het lint in de groep **implementatie** op **inhoud distribueren**. Met deze actie wordt de wizard inhoud distribueren gestart.  

4. Controleer op de pagina **Algemeen** of de juiste taken reeks is geselecteerd voor distributie.  

5. Controleer op de pagina **inhoud** de inhoud die moet worden gedistribueerd, zoals de opstart installatie kopie waarnaar wordt verwezen door de taken reeks.  

6. Geef op de pagina **doel van inhoud** de verzamelingen, het distributie punt of de distributiepunt groep op waarnaar u de inhoud van de taken reeks wilt distribueren.  

    > [!IMPORTANT]  
    > Als de taken reeks die u hebt geselecteerd, verwijst naar inhoud die al is gedistribueerd naar een specifiek distributie punt, wordt dat distributie punt niet vermeld in de wizard.  

7. Voltooi de wizard.  

U kunt ook de inhoud voorbereiden waarnaar in de taken reeks wordt verwezen. Configuration Manager maakt een gecomprimeerd, voor bereid inhouds bestand dat de bestanden, gekoppelde afhankelijkheden en gekoppelde meta gegevens bevat voor de inhoud die u selecteert. Vervolgens importeert u de inhoud hand matig op een site server, secundaire site of distributie punt. Zie [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)voor meer informatie over het voorbereiden van inhoudsbestanden.  

## <a name="deploy"></a><a name="BKMK_DeployTS"></a>Zetten  

Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.

## <a name="export-and-import"></a><a name="BKMK_ExportImport"></a>Exporteren en importeren  

Taken reeksen met of zonder bijbehorende objecten exporteren en importeren. Deze inhoud waarnaar wordt verwezen, omvat de volgende objecten:  

- Installatiekopieën van het besturingssysteem  
- Installatiekopieën  
- Pakketten zoals het client installatie pakket  
- Driverpakketten  
- Toepassingen met afhankelijkheden  

Houd rekening met de volgende punten wanneer u taken reeksen exporteert en importeert:  

- Configuration Manager exporteert geen wacht woorden in de taken reeks. Als u een taken reeks exporteert en importeert die wacht woorden bevat, moet u de geïmporteerde taken reeks bewerken om wacht woorden opnieuw in te voeren. Bekijk de volgende stappen die een wacht woord kunnen bevatten:  

  - [Lid worden van domein of werkgroep](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  
  - [Verbinding maken met netwerkmap](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  
  - [Opdrachtregel uitvoeren](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- Wanneer u een taken reeks exporteert met de stap **dynamische variabelen instellen** , exporteert Configuration Manager geen waarden voor variabelen die u configureert met de instelling **geheime waarde** . Voer de waarden voor deze variabelen opnieuw in nadat u de taken reeks hebt geïmporteerd.  

- Wanneer u meerdere primaire sites hebt, importeert u taken reeksen op de centrale beheer site.  

### <a name="process-to-export-task-sequences"></a>Proces voor het exporteren van taken reeksen  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

2. Selecteer in de lijst **Takenreeks** de takenreeks die u wilt exporteren. Als u meer dan één taken reeks selecteert, worden deze allemaal opgeslagen in één export bestand.  

3. Klik op het tabblad **Start** van het lint in de groep **taken reeks** op **exporteren**. Met deze actie wordt de wizard taken reeks exporteren gestart.  

4. Geef op het tabblad **Algemeen** de volgende instellingen op:  

    - **Bestand**: Geef de locatie en de naam van het export bestand op. Als u de bestandsnaam rechtstreeks invoert, moet u de extensie (.zip) opnemen in de bestandsnaam. Als u naar het exportbestand bladert, wordt de extensie door de wizard automatisch aan deze bestandsnaam toegevoegd.  

    - Als u de afhankelijkheden van taken reeksen niet wilt exporteren, schakelt u de optie voor het **exporteren van alle afhankelijkheden van taken reeksen**uit. De wizard scant standaard op alle bijbehorende objecten en exporteert deze met de takenreeks. Deze afhankelijkheden zijn voor toepassingen.  

    - Als u de inhoud van de pakket bron niet naar de export locatie wilt kopiëren, schakelt u de optie voor het **exporteren van alle inhoud voor de geselecteerde taken reeksen en afhankelijkheden**uit. Als u deze optie selecteert, gebruikt de wizard taken reeks importeren het pad importeren als de nieuwe pakket bron locatie.  

    - **Opmerkingen beheerder**: Voeg een beschrijving toe van de taken reeksen die u wilt exporteren.  

5. Voltooi de wizard.  

De wizard maakt de volgende uitvoerbestanden:  

- Als u geen inhoud exporteert: een zip-bestand.  

- Als u inhoud exporteert: een ZIP-bestand en een map met de naam *export*_files, waarbij *export* de naam is van het ZIP-bestand dat de geëxporteerde inhoud bevat.  

Als u inhoud opneemt wanneer u een taken reeks exporteert, moet u ervoor zorgen dat u het zip-bestand en de map *export*_FILES kopieert, anders mislukt het importeren.  

### <a name="process-to-import-task-sequences"></a>Proces voor het importeren van taken reeksen  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

2. Selecteer **taken reeks importeren**op het tabblad **Start** van het lint in de groep **maken** . Met deze actie wordt de wizard taken reeks importeren gestart.  

3. Geef op de pagina **Algemeen** van het lint het geëxporteerde zip-bestand op.  

4. Selecteer op de pagina **Bestandsinhoud** de actie die u nodig hebt voor elk object dat u importeert. Op deze pagina worden alle objecten weer gegeven die Configuration Manager te importeren hebben gevonden.  

    - Selecteer **Nieuw**, als het object nog nooit is geïmporteerd.  

    - Selecteer een van de volgende acties, als het object al eerder is geïmporteerd:  

        - **Dubbele negeren** (standaard): met deze actie wordt het object niet geïmporteerd. In plaats daarvan koppelt de wizard het bestaande object aan de takenreeks.  

        - **Overschrijven**: met deze actie wordt het bestaande object overschreven door het geïmporteerde object. Voor toepassingen kunt u een revisie toevoegen om de bestaande toepassing bij te werken of een nieuwe toepassing te maken.  

5. Voltooi de wizard.  

Wanneer u de takenreeks hebt geïmporteerd, bewerkt u de takenreeks zo, dat deze wachtwoorden opgeeft die geldig waren in de oorspronkelijke takenreeks. Uit veiligheids overwegingen worden wacht woorden niet geëxporteerd.  

## <a name="return-to-previous-page-on-failure"></a>Terug naar vorige pagina bij fout

Wanneer u een taken reeks uitvoert en er een fout is opgetreden, kunt u teruggaan naar een vorige pagina van de wizard taken reeks. In eerdere versies van Configuration Manager moest u de taken reeks opnieuw opstarten als er een fout is opgetreden. Gebruik de knop **vorige** in de volgende scenario's:

- Wanneer een computer wordt opgestart in Windows PE, wordt het dialoog venster Boots trap van taken reeks mogelijk weer gegeven voordat de taken reeks beschikbaar is. Wanneer u volgende in dit scenario selecteert, wordt de laatste pagina van de taken reeks weer gegeven met een bericht dat er geen taken reeksen beschikbaar zijn. Nu kunt u **vorige** selecteren om opnieuw te zoeken naar beschik bare taken reeksen. U kunt dit proces herhalen totdat de taken reeks beschikbaar is.  

- Wanneer u een taken reeks uitvoert, maar afhankelijke inhouds pakketten nog niet beschikbaar zijn op distributie punten, mislukt de taken reeks. Als de ontbrekende inhoud nog niet is gedistribueerd, distribueer deze dan nu. Of wacht tot de inhoud beschikbaar is op distributie punten. Selecteer **vorige** om de taken reeks opnieuw te laten zoeken naar de inhoud.

## <a name="collection-and-device-variables"></a><a name="BKMK_CreateTSVariables"></a>Verzamelings-en apparaat-variabelen

U kunt takenreeksvariabelen definiëren voor computers en verzamelingen. Variabelen die u definieert voor een computer worden taken reeks variabelen per computer genoemd. Naar variabelen die voor een verzameling zijn gedefinieerd, wordt verwezen als verzamelingtakenreeksvariabelen. Zie [verzameling en apparaat variabelen](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)voor meer informatie.

## <a name="additional-actions"></a><a name="BKMK_AdditionalActionsTS"></a>Aanvullende acties  

U kunt taken reeksen beheren door gebruik te maken van aanvullende acties wanneer u een taken reeks selecteert.  

### <a name="edit"></a>Bewerken

Zie [de taken reeks editor gebruiken](../understand/task-sequence-editor.md#bkmk_edit)voor meer informatie.

### <a name="enable"></a>Inschakelen

Hiermee wordt de taken reeks ingeschakeld zodat clients deze kunnen uitvoeren. U hoeft een taken reeks niet opnieuw te implementeren nadat deze is ingeschakeld.  

### <a name="disable"></a>Uitschakelen

Hiermee wordt de taken reeks uitgeschakeld, zodat deze niet op computers kan worden uitgevoerd. U kunt een uitgeschakelde taken reeks implementeren, maar computers voeren de taken reeks pas uit nadat u deze hebt ingeschakeld.  

### <a name="export"></a>Exporteren

Zie [taken reeksen exporteren en importeren](#BKMK_ExportImport)voor meer informatie.

### <a name="copy"></a>Exemplaar

Hiermee wordt een kopie gemaakt van de geselecteerde takenreeks. Deze actie is handig als u een nieuwe taken reeks wilt maken die is gebaseerd op een bestaande taken reeks.

Wanneer u een kopie maakt van een takenreeks in een map, wordt de kopie in die map vermeld tot u het takenreeksknooppunt vernieuwt. Na het vernieuwen, wordt de kopie weergegeven in de hoofdmap.  

### <a name="refresh"></a>Vernieuwen

Hiermee vernieuwt u de Details voor de geselecteerde taken reeks.

### <a name="delete"></a>Verwijderen

Hiermee verwijdert u de geselecteerde taken reeks.

### <a name="create-phased-deployment"></a>Gefaseerde implementatie maken

Zie voor meer informatie [gefaseerde implementaties maken](create-phased-deployment-for-task-sequence.md).

### <a name="deploy"></a>Implementeren

Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.

### <a name="distribute-content"></a>Inhoud distribueren

Hiermee wordt de wizard inhoud distribueren gestart om de inhoud waarnaar wordt verwezen, naar distributie punten te verzenden.

### <a name="create-prestaged-content-file"></a>Voorbereid inhoudsbestand maken

Hiermee wordt de wizard Voorbereid inhoudsbestand maken gestart om de inhoud van de takenreeks voor te bereiden. Zie [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)voor informatie over het maken van een voorbereid inhoudsbestand.

### <a name="move"></a>Verplaatsen

Hiermee wordt de geselecteerde taken reeks verplaatst naar een andere map in het knoop punt **taken reeksen** .

### <a name="set-security-scopes"></a>Beveiligingsbereiken instellen

Selecteer de beveiligingsbereiken voor de geselecteerde taken reeks. Zie [Beveiligingsbereiken](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)voor meer informatie.

### <a name="properties"></a>Eigenschappen

Zie [Eigenschappen van software Center configureren](#bkmk_prop-general) en [geavanceerde taken reeks instellingen configureren](#bkmk_prop-advanced)voor meer informatie.

### <a name="view"></a>Weergave

<!--3633146-->
Vanaf versie 1902 is de **weergave** actie voor taken reeksen de standaard instelling. Met deze actie kunt u de stappen van de taken reeks zien zonder deze te vergren delen voor bewerken. Zie [de taken reeks editor gebruiken](../understand/task-sequence-editor.md#bkmk_view)voor meer informatie.

## <a name="see-also"></a>Zie ook

- [Scenario's voor het implementeren van enterprise-besturingssystemen](scenarios-to-deploy-enterprise-operating-systems.md)

- [De takenreekseditor gebruiken](../understand/task-sequence-editor.md)

- [Een takenreeks implementeren](deploy-a-task-sequence.md)

- [Stappen voor takenreeksen](../understand/task-sequence-steps.md)

- [Verzamelings-en apparaat-variabelen](../understand/using-task-sequence-variables.md#bkmk_set-coll-var)

- [Gefaseerde implementaties maken](create-phased-deployment-for-task-sequence.md)
