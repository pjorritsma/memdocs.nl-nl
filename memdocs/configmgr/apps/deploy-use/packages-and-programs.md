---
title: Pakketten en programma's
titleSuffix: Configuration Manager
description: Ondersteunings implementaties die gebruikmaken van verouderde pakketten en Program ma's met Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2c125212a13790e196d001f53411633d1e42d4f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710109"
---
# <a name="packages-and-programs-in-configuration-manager"></a>Pakketten en Program ma's in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager blijft ondersteuning bieden voor pakketten en Program ma's die in Configuration Manager 2007 zijn gebruikt. Een implementatie waarbij pakketten en Program ma's worden gebruikt, is mogelijk meer geschikt voor een toepassing wanneer u een van de volgende hulpprogram ma's of scripts implementeert:  

- Beheer Programma's die geen toepassing op een computer installeren
- ' Eenmalige ' scripts die niet voortdurend hoeven te worden bewaakt  
- Scripts die worden uitgevoerd volgens een terugkerend schema en geen globale evaluatie kunnen gebruiken

> [!TIP]  
> U kunt de functie [scripts](create-deploy-scripts.md) gebruiken in de Configuration Manager-console. Scripts zijn mogelijk een betere oplossing voor enkele van de voor gaande scenario's in plaats van het gebruik van pakketten en Program ma's.

Wanneer u pakketten migreert vanuit een eerdere versie van Configuration Manager, kunt u deze implementeren in uw Configuration Manager-hiërarchie. Zodra de migratie is voltooid, worden de pakketten weergegeven onder het knooppunt **Pakketten** in de werkruimte **Softwarebibliotheek**.

U kunt deze pakketten wijzigen en implementeren op dezelfde manier als u hebt gedaan met behulp van software distributie. De **wizard pakket importeren van definitie** blijft in Configuration Manager om verouderde pakketten te importeren. Aankondigingen worden geconverteerd naar implementaties wanneer u migreert van Configuration Manager 2007 naar een Configuration Manager-hiërarchie.  

> [!NOTE]  
> Pakket conversie beheer gebruiken om pakketten en Program ma's te converteren naar Configuration Manager-toepassingen.  
>
> Vanaf versie 1806 is pakket conversie beheer geïntegreerd met Configuration Manager. Zie [package Conversion Manager](../pcm/package-conversion-manager.md)voor meer informatie.  

Pakketten kunnen enkele nieuwe functies van Configuration Manager gebruiken, waaronder distributiepunten groepen en bewaking. U kunt geen toepassingen van micro soft Application Virtualization (app-V) implementeren met pakketten en Program ma's in Configuration Manager. Als u virtuele toepassingen wilt distribueren, maakt u deze als Configuration Manager-toepassingen. Zie [virtuele toepassingen van app-V implementeren](../get-started/deploying-app-v-virtual-applications.md)voor meer informatie.  


## <a name="create-a-package-and-program"></a>Een pakket en programma maken

### <a name="use-the-create-package-and-program-wizard"></a>Gebruik de wizard pakket en programma maken

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **pakketten** .  

2. Klik op het tabblad **Start** van het lint in de groep **maken** op **pakket maken**.  

3. Geef op de pagina **pakket** van de **wizard pakket en programma maken**de volgende informatie op:  

    - **Naam**: Geef een naam op voor het pakket met een maximum van 50 tekens.  

    - **Beschrijving**: Geef een beschrijving op voor dit pakket met een maximum van 128 tekens.  

    - **Fabrikant** (optioneel): Geef de naam van een fabrikant op om het pakket te identificeren in de Configuration Manager-console. Deze naam mag maximaal 32 tekens lang zijn.

    - **Taal** (optioneel): Geef de taal versie van het pakket op met een maximum van 32 tekens.  

    - **Versie** (optioneel): Geef een versie nummer op voor het pakket met een maximum van 32 tekens.

    - **Dit pakket bevat bron bestanden**: deze instelling geeft aan of het pakket vereist dat bron bestanden aanwezig zijn op client apparaten. Standaard wordt deze optie niet door de wizard ingeschakeld en Configuration Manager geen distributie punten voor het pakket gebruikt. Wanneer u deze optie selecteert, geeft u de pakket inhoud op die moet worden gedistribueerd naar distributie punten.  

    - **Bronmap**: als het pakket bron bestanden bevat, kiest u **Bladeren** om het dialoog venster **bronmap instellen** te openen en geeft u de locatie van de bron bestanden voor het pakket op.  

        > [!NOTE]  
        > Het computeraccount van de siteserver moet leesrechten voor de door u opgegeven bronmap hebben.  

    - Vanaf versie 1906 kunt u de **architectuur** en **taal** van het pakket opgeven als u inhoud vooraf in de cache wilt opslaan op een client. Zie [inhoud vooraf in cache configureren](../../osd/deploy-use/configure-precache-content.md)voor meer informatie.<!--4224642-->  

4. Selecteer op de pagina **programma type** van de **wizard pakket en programma maken**het type programma dat u wilt maken en kies vervolgens **volgende**. U kunt een programma voor een [computer](#create-a-standard-program) of [apparaat](#create-a-device-program)maken of u kunt deze stap overs Laan en later een programma maken.  

    > [!TIP]  
    > Als u een nieuw programma voor een bestaand pakket wilt maken, selecteert u eerst het pakket. Klik vervolgens op het tabblad **Start** in de groep **pakket** op **programma maken** om de **wizard programma maken**te openen.  

#### <a name="create-a-standard-program"></a>Een standaard programma maken

1. Kies op de pagina **programma type** van de **wizard pakket en programma maken**de optie **standaard programma**en klik vervolgens op **volgende**.  

2. Geef op de pagina **standaard programma** de volgende informatie op:  

    - **Naam**geef een naam voor het programma op met een maximum van 50 tekens.  

        > [!NOTE]  
        > De naam van het programma moet uniek zijn binnen een pakket. Nadat u een programma hebt gemaakt, kunt u de naam niet meer wijzigen.  

    - **Opdracht regel**: Geef de opdracht regel op die moet worden gebruikt om dit programma te starten of kies **Bladeren** om naar de locatie van het bestand te bladeren.  

        Als u geen extensie opgeeft voor een bestands naam, Configuration Manager probeert. com,. exe en. bat te gebruiken als mogelijke uitbrei dingen.  

        Wanneer de client het programma uitvoert, zoekt Configuration Manager naar het bestand op de volgende locaties:

        - Binnen het pakket
        - De lokale Windows-map
        - Het lokale *% pad%*

        Als het bestand niet kan worden gevonden, mislukt het programma.  

    - **Opstartmap** (optioneel): Geef de map op waarin het programma wordt uitgevoerd, maxi maal 127 tekens. Deze map kan een absoluut pad op de client zijn. Het kan ook een pad zijn dat relatief is ten opzichte van de map met het distributie punt waarin het pakket zich bevindt.

    - **Uitvoeren**: Geef de modus op waarin het programma wordt uitgevoerd op client computers. Selecteer één van de volgende opties:  

        - **Normaal**: het programma wordt in de normale modus uitgevoerd op basis van standaard instellingen van het systeem en Program ma's. Deze modus is de standaardinstelling.  

        - **Geminimaliseerd**: het programma wordt geminimaliseerd uitgevoerd op client apparaten. Gebruikers zien de installatie activiteit mogelijk in het systeemvak of op de taak balk.  

        - **Gemaximaliseerd**: het programma wordt gemaximaliseerd uitgevoerd op client apparaten. Gebruikers zien alle installatie activiteiten.  

        - **Verborgen**: het programma wordt verborgen op client apparaten. Gebruikers zien geen installatie activiteiten.  

    - Het **programma kan worden uitgevoerd**: Geef op of het programma alleen wordt uitgevoerd wanneer een gebruiker is aangemeld, alleen wanneer er geen gebruiker is aangemeld, of ongeacht of een gebruiker is aangemeld bij de client computer.  

    - **Uitvoerings modus**: Geef op of het programma wordt uitgevoerd met beheerders machtigingen of met de machtigingen van de gebruiker die op dat moment is aangemeld.  

    - **Gebruikers toestaan de programma-installatie te bekijken en ermee te werken**: gebruik deze instelling, indien beschikbaar, om op te geven of gebruikers de programma-installatie mogen gebruiken. Deze optie is alleen beschikbaar als aan de volgende voor waarden wordt voldaan:

        - De instelling **kan** alleen worden uitgevoerd **als er geen gebruiker is aangemeld of als er** geen gebruiker **is aangemeld**
        - De **uitvoerings modus** moet worden **uitgevoerd met beheerders rechten**  

    - **Schijf modus**: Geef informatie op over hoe dit programma wordt uitgevoerd op het netwerk. Kies een van de volgende opties:  

        - **Wordt uitgevoerd met UNC-naam**: Hiermee geeft u op dat het programma wordt uitgevoerd met een UNC-naam (Universal Naming Convention). Dit is de standaardinstelling.  

        - **Vereist stationsletter**: Geef op dat voor het programma een stationsletter is vereist om de locatie volledig te kwalificeren. Voor deze instelling kan Configuration Manager alle beschik bare stationsletters op de client gebruiken.  

        - **Vereist specifieke**stationsletter: Geef op dat het programma een specifieke stationsletter vereist die u opgeeft om de locatie volledig te kwalificeren. Bijvoorbeeld **Z:**. Als de client de opgegeven stationsletter al gebruikt, wordt het programma niet uitgevoerd.  

    - **Opnieuw verbinding maken met distributie punt bij aanmelding**: Geef aan of de client opnieuw verbinding maakt met het distributie punt wanneer de gebruiker zich aanmeldt. Deze optie wordt standaard niet door de wizard ingeschakeld.

3. Geef op de pagina **vereisten** van de **wizard pakket en programma maken** de volgende informatie op:  

    - **Eerst een ander programma uitvoeren**: Identificeer een pakket en programma dat wordt uitgevoerd voordat dit pakket en programma wordt uitgevoerd.  

    - **Platform vereisten**: Selecteer **dit programma kan op elk platform worden uitgevoerd** of **dit programma kan alleen op de opgegeven platforms worden uitgevoerd**. Kies vervolgens de versies van het besturings systeem die clients moeten hebben om dit pakket en programma te installeren.  

    - **Geschatte schijf ruimte**: Geef de hoeveelheid schijf ruimte op die het programma nodig heeft om op de computer te worden uitgevoerd. De standaard instelling is **onbekend**. Geef indien nodig een geheel getal op dat groter is dan of gelijk is aan nul. Als u een waarde instelt, selecteert u ook eenheden voor de waarde.  

    - **Maxi maal toegestane uitvoerings tijd (minuten)**: Geef de maximale duur op voor het uitvoeren van het programma op de client computer. De standaard waarde is **120** minuten. Gebruik alleen gehele getallen die groter zijn dan nul.  

        > [!IMPORTANT]  
        > Als u onderhouds Vensters gebruikt in dezelfde verzameling als waarin u dit programma implementeert, kan er een conflict optreden als de **maximale toegestane uitvoerings tijd** langer is dan het geplande onderhouds venster. Als u de maximale uitvoerings tijd instelt op **onbekend**, wordt het programma gestart tijdens het onderhouds venster. Het wordt vervolgens naar behoefte uitgevoerd nadat het onderhouds venster is gesloten. Als u de maximale uitvoerings tijd instelt op een specifieke periode die groter is dan de lengte van een beschikbaar onderhouds venster, wordt het programma niet uitgevoerd op de client.  

        Als u deze waarde instelt op **onbekend**, stelt Configuration Manager de Maxi maal toegestane uitvoerings tijd in op 12 uur (720 minuten).  

        > [!NOTE]  
        > Als het programma de maximale uitvoerings tijd overschrijdt, wordt Configuration Manager gestopt als aan de volgende voor waarden wordt voldaan:
        >
        > - U kunt de optie **uitvoeren met beheerders rechten**
        > - U kunt de optie niet inschakelen om **gebruikers toe te staan de programma-installatie te bekijken en te gebruiken**  

#### <a name="create-a-device-program"></a>Een apparaatprogramma maken  

1. Op de pagina **programma type** van de **wizard pakket en programma maken**selecteert u **programma voor apparaat**en klikt u vervolgens op **volgende**.  

2. Geef op de pagina **programma voor apparaat** de volgende instellingen op:  

    - **Naam**: Geef een naam voor het programma op met een maximum van 50 tekens.  

        > [!NOTE]  
        > De naam van het programma moet uniek zijn binnen een pakket. Nadat u een programma hebt gemaakt, kunt u de naam niet meer wijzigen.  

    - **Opmerking** (optioneel): Geef een opmerking op voor dit apparaat met een maximum van 127 tekens.  

    - **Downloadmap**: Geef de naam op van de map op het apparaat waarin de bron bestanden van het pakket worden opgeslagen. De standaardwaarde is `\Temp\`.  

    - **Opdracht regel**: Geef de opdracht regel op die moet worden gebruikt om dit programma te starten. Klik op **Bladeren**om naar de locatie van het bestand te bladeren.  

    - **Opdracht regel uitvoeren in downloadmap**: Selecteer deze optie om het programma uit te voeren vanuit de downloadmap.  

    - **Opdracht regel uitvoeren vanuit deze map**: Selecteer deze optie om een andere map op te geven waaruit u het programma wilt uitvoeren.  

3. Geef op de pagina **vereisten** de volgende instellingen op:  

    - **Geschatte schijf ruimte**: Geef de hoeveelheid schijf ruimte op die vereist is voor de software. De client geeft deze waarde weer aan gebruikers van mobiele apparaten voordat ze het programma installeren.  

    - **Programma downloaden**: Geef informatie op over wanneer dit programma door het mobiele apparaat kan worden gedownload. U kunt **Zo snel mogelijk**, **Alleen via een snel netwerk** of **Alleen wanneer het apparaat is vastgezet** opgeven.  

    - **Aanvullende vereisten**: Geef eventuele aanvullende vereisten voor dit programma op. Gebruikers zien deze vereisten voordat ze de software installeren. U kunt gebruikers bijvoorbeeld waarschuwen dat ze alle andere toepassingen moeten sluiten voordat ze het programma uitvoeren.  

## <a name="deploy-packages-and-programs"></a>Pakketten en Program ma's implementeren  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **pakketten** .  

2. Selecteer het pakket dat u wilt implementeren. Klik op het tabblad **Start** van het lint in de groep **implementatie** op **implementeren**.  

3. Geef op de pagina **Algemeen** van de **wizard software implementeren**de naam op van het pakket en programma dat u wilt implementeren. Selecteer de verzameling waarvoor u het pakket en programma wilt implementeren en eventuele optionele opmerkingen.  

    Als u de pakket inhoud wilt opslaan op de standaard distributiepunten groep van de verzameling, selecteert u de optie voor het **gebruik van standaard distributiepunten groepen die zijn gekoppeld aan deze verzameling**. Als u deze verzameling niet hebt gekoppeld aan een distributiepunten groep, is deze optie niet beschikbaar.  

4. Kies op de pagina **inhoud** **toevoegen**. Selecteer de distributie punten of distributiepunten groepen waarnaar u de inhoud voor dit pakket en programma wilt distribueren.  

5. Configureer de volgende instellingen op de pagina **implementatie-instellingen** :  

    - **Doel**: Kies een van de volgende opties:

        - **Beschikbaar**: de gebruiker ziet het gepubliceerde pakket en programma in Software Center en kan het op aanvraag installeren.  

        - **Vereist**: het pakket en programma worden automatisch geïmplementeerd volgens de geconfigureerde planning. In Software Center kunt u de implementatie status volgen en deze installeren vóór de deadline.  

        > [!NOTE]
        > Als meerdere gebruikers zijn aangemeld bij het apparaat, worden er mogelijk geen pakket-en taken reeks implementaties weer gegeven in Software Center.

    - **Ontwaak pakketten verzenden**: als u het implementatie doel instelt op **vereist** en deze optie selecteert, verzendt de site eerst een Ontwaak pakket naar computers bij de deadline van de installatie. Voordat u deze optie kunt gebruiken, moet u computers configureren voor Wake On LAN. Zie [Wake on LAN configureren](../../core/clients/deploy/configure-wake-on-lan.md)voor meer informatie.  

    - **Clients met een Internet verbinding naar gebruik toestaan inhoud te downloaden na de installatie deadline, waarvoor extra kosten in rekening kunnen worden gebracht**  

    > [!NOTE]  
    > Wanneer u een pakket en programma implementeert, is de optie om **software vooraf te implementeren op het primaire apparaat van de gebruiker** niet beschikbaar.  

6. Configureer op de pagina **planning** wanneer u dit pakket en programma wilt implementeren op client apparaten.  

    De opties op deze pagina variëren, afhankelijk van het feit of u de implementatie actie instelt op **beschikbaar** of **vereist**.  

    Voor **vereiste** implementaties configureert u het gedrag voor opnieuw uitvoeren voor het programma in de vervolg keuzelijst **gedrag voor opnieuw uitvoeren** . Kies uit de volgende opties:  

    | Gedrag voor opnieuw uitvoeren | Beschrijving |
    |----------------|-------------|
    | **Geïmplementeerd programma nooit opnieuw uitvoeren** | De client voert het programma niet opnieuw uit. Dit gedrag treedt zelfs op als het programma oorspronkelijk is mislukt of als de programma bestanden zijn gewijzigd. |
    | **Programma altijd opnieuw uitvoeren** | De client voert het programma altijd opnieuw uit wanneer de implementatie is gepland. Dit gebeurt zelfs als het programma al is uitgevoerd. Het is handig bij terugkerende implementaties wanneer u het programma bijwerkt. |
    | **Opnieuw uitvoeren als de vorige poging is mislukt** | De client voert het programma opnieuw uit wanneer de implementatie is gepland, alleen als dit tijdens de vorige uitvoerings poging is mislukt. |
    | **Opnieuw uitvoeren als de vorige poging is gelukt** | De client voert het programma alleen opnieuw uit als dit eerder is uitgevoerd op de client. Dit gedrag is handig bij terugkerende implementaties wanneer u het programma regel matig bijwerkt en voor elke update moet de vorige update zijn geïnstalleerd. |

7. Geef op de pagina **Gebruikerservaring** de volgende informatie:  

    - **Gebruikers toestaan het programma onafhankelijk van toewijzingen uit te voeren**: gebruikers kunnen deze software installeren vanuit software Center, ongeacht het geplande installatie tijdstip.  

    - **Software-installatie**: hierdoor kan de software worden geïnstalleerd buiten de geconfigureerde onderhoudsvensters.  

    - **Systeem opnieuw opstarten (indien dit is vereist om de installatie te volt ooien)**: als de software-installatie vereist dat het apparaat opnieuw wordt opgestart, mag deze actie buiten de geconfigureerde onderhouds Vensters plaatsvinden.  

    - **Inge sloten apparaten**: wanneer u pakketten en Program ma's implementeert op Windows Embedded-apparaten waarop schrijf filter is ingeschakeld, kunt u opgeven dat ze pakketten en Program ma's op de tijdelijke overlay installeren en later wijzigingen door voeren. U kunt ook de wijzigingen door voeren op de deadline van de installatie of tijdens een onderhouds venster. Wanneer u wijzigingen doorvoert voor de installatie deadline of tijdens een onderhouds venster, is opnieuw opstarten vereist en blijven de wijzigingen op het apparaat behouden.  

        > [!NOTE]  
        > Wanneer u een pakket of programma implementeert op een Windows Embedded-apparaat, moet u ervoor zorgen dat het apparaat lid is van een verzameling met een geconfigureerd onderhoudsvenster. Zie [Windows Embedded-toepassingen maken](../get-started/creating-windows-embedded-applications.md)voor meer informatie over het gebruik van onderhouds Vensters wanneer u pakketten en Program ma's implementeert op Windows Embedded-apparaten.  

8. Geef op de pagina **Distributiepunten** de volgende informatie:  

    - **Implementatie opties**: Geef de actie op die een client gebruikt voor een distributie punt in de huidige grens groep. Selecteer ook de actie voor de client wanneer deze gebruikmaakt van een distributie punt van een grens groep in de nabijheid of de standaard site grens groep.

        > [!IMPORTANT]  
        > Als u de implementatie optie configureert om het **programma uit te voeren vanaf het distributie punt**, moet u ervoor zorgen dat de optie voor het **kopiëren van de inhoud in dit pakket naar een pakket share op distributie punten** is ingeschakeld op het tabblad **gegevens toegang** van de pakket eigenschappen. Anders is het pakket niet beschikbaar voor uitvoering vanaf distributie punten.  

    - **Clients toestaan distributie punten van de standaard site grens groep te gebruiken**: als deze inhoud niet beschikbaar is vanaf een distributie punt in de huidige of grens groepen van de grenzen, schakelt u deze optie in om de distributie punten in de standaard grens groep van de site te laten proberen.

9. Voltooi de wizard.  

Bekijk de implementatie in het knoop punt **implementaties** van de werk ruimte **bewaking** en in het detail venster van het tabblad pakket implementatie wanneer u de implementatie selecteert. Zie [pakketten en Program ma's bewaken](#monitor-packages-and-programs)voor meer informatie.  


## <a name="monitor-packages-and-programs"></a>Pakketten en Program ma's bewaken

Voor het bewaken van pakket-en programma-implementaties, gebruikt u dezelfde procedures die u ook gebruikt voor het bewaken van toepassingen zoals beschreven in [toepassingen bewaken](monitor-applications-from-the-console.md).  

Pakketten en Program ma's bevatten ook een aantal ingebouwde rapporten waarmee u informatie kunt controleren over de implementatie status van pakketten en Program ma's. Deze rapporten hebben de rapportcategorie **Softwaredistributie – Pakketten en programma's** en **Softwaredistributie – Status van pakket- en programma-implementatie**.  

Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over het configureren van rapportage in Configuration Manager.  


## <a name="manage-packages-and-programs"></a>Pakketten en Program ma's beheren

Vouw in de werk ruimte **software bibliotheek** de optie **toepassings beheer**uit en selecteer het knoop punt **pakketten** . Selecteer het pakket dat u wilt beheren en kies vervolgens een beheer taak.  

### <a name="create-prestage-content-file"></a>Voorbereid inhoudsbestand maken

Hiermee opent u de **wizard voor bereid inhouds bestand maken**om een bestand te maken dat de pakket inhoud bevat. Gebruik dit bestand om het pakket hand matig te importeren naar een extern distributie punt. Deze actie is handig als u een lage netwerk bandbreedte hebt tussen de site server en het distributie punt.

### <a name="create-program"></a>Programma maken

Hiermee opent u de **wizard programma maken**, waarmee u een nieuw programma voor dit pakket kunt maken.

### <a name="export"></a>Exporteren

Hiermee opent u de **wizard pakket exporteren**, waarmee u het geselecteerde pakket en de inhoud ervan naar een bestand kunt exporteren. Gebruik dit bestand om het bestand te importeren in een andere hiërarchie.

Zie [pakketten en Program Ma's maken](#create-a-package-and-program)voor meer informatie over het importeren van pakketten en Program ma's.

### <a name="deploy"></a>Implementeren

Hiermee opent u de **wizard software implementeren**, waarmee u het geselecteerde pakket en programma kunt implementeren voor een verzameling. Zie [pakketten en Program Ma's implementeren](#deploy-packages-and-programs)voor meer informatie.

### <a name="distribute-content"></a>Inhoud distribueren

Hiermee opent u de **wizard inhoud distribueren**om de inhoud voor een pakket en programma te verzenden naar geselecteerde distributie punten of distributiepunten groepen.

### <a name="update-distribution-points"></a>Distributie punten bijwerken

Hiermee worden distributiepunten bijwerkt met de meest recente inhoud voor het geselecteerde pakket en programma.


## <a name="see-also"></a>Zie ook

- [Scripts](create-deploy-scripts.md)

- [Package Conversion Manager](../pcm/package-conversion-manager.md)

- [Pakketdefinitiebestanden](package-definition-files.md)
