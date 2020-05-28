---
title: Inhoud implementeren
titleSuffix: Configuration Manager
description: Nadat u distributie punten voor Configuration Manager hebt geïnstalleerd, kunt u aan de slag gaan met het implementeren van inhoud.
ms.date: 05/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df26fe91f009a1a4f5d3c5a4f4adb5fe45bbd245
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343147"
---
# <a name="deploy-and-manage-content-for-configuration-manager"></a>Inhoud implementeren en beheren voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u distributie punten voor Configuration Manager hebt geïnstalleerd, kunt u beginnen met het implementeren van inhoud. Doorgaans worden inhouds overdrachten naar distributie punten via het netwerk, maar er zijn ook andere opties voor het ophalen van inhoud aan de distributie punten. Na de overdracht van inhoud naar een distributie punt, kunt u die inhoud op distributie punten bijwerken, opnieuw distribueren, verwijderen en valideren.  

##  <a name="distribute-content"></a><a name="bkmk_distribute"></a>Inhoud distribueren  
Doorgaans distribueert u inhoud naar distributie punten zodat deze beschikbaar is voor client computers. (De uitzonde ring hierop is wanneer u inhouds distributie op aanvraag gebruikt voor een specifieke implementatie.) Wanneer u inhoud distribueert, Configuration Manager inhouds bestanden in een pakket opslaat en vervolgens het pakket distribueert naar het distributie punt. De inhoud voor het pakket wordt opgehaald uit de inhouds bibliotheek van de site server. De typen inhoud die u kunt distribueren, zijn:  

- Implementatie typen van toepassing  

- Pakketten  

- Implementatiepakketten  

- Driverpakketten  

- Installatiekopieën van besturingssysteem  

- Installatie Programma's voor besturings systemen  

- Installatiekopieën  

- Takenreeksen  

Wanneer u een pakket met bron bestanden maakt, zoals een type toepassings implementatie of implementatie pakket, wordt de site waarop het pakket wordt gemaakt de site-eigenaar voor de pakket inhouds bron. Configuration Manager kopieert de bron bestanden van het bron bestand dat u opgeeft voor het object naar de inhouds bibliotheek op de site server die eigenaar is van de bron van de pakket inhoud.  Configuration Manager repliceert vervolgens de gegevens naar extra sites. (Zie [de inhouds bibliotheek](../../../../core/plan-design/hierarchy/the-content-library.md) voor meer informatie.)  

Gebruik de volgende procedure om inhoud te distribueren naar distributie punten.  

#### <a name="to-distribute-content-on-distribution-points"></a>Inhoud op distributie punten distribueren  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Selecteer in de werk ruimte **software bibliotheek** een van de volgende stappen voor het type inhoud dat u wilt distribueren:  

    - **Toepassingen**: Vouw toepassingen voor **toepassings beheer**uit  >  **Applications**en selecteer vervolgens de toepassingen die u wilt distribueren.  

    - **Pakketten**: Vouw **toepassings beheer**  >   **pakketten**uit en selecteer vervolgens de pakketten die u wilt distribueren.  

    - **Implementatie pakketten**: Vouw **Software**  >   -Update-**implementatie pakketten**uit en selecteer vervolgens de implementatie pakketten die u wilt distribueren.  

    - **Stuur programmapakketten**: Vouw **besturings systemen**  >   **Stuur programmapakketten**uit en selecteer vervolgens de Stuur programmapakketten die u wilt distribueren.  

    - **Installatie kopieën van besturings systeem**: Vouw **besturingssysteem**  >   **installatie kopieën**van besturings systemen uit en selecteer vervolgens de installatie kopieën van het besturings systeem die u wilt distribueren.  

    - **Installatie Programma's**van het besturings systeem: Vouw besturings **systemen**  >  **installatie Programma's besturings systeem**en selecteer vervolgens de installatie Programma's van het besturings systeem die u wilt distribueren.  

    - **Opstart installatie**kopieën: Vouw installatie kopieën van **besturings systemen**uit  >   **Boot Images**en selecteer vervolgens de opstart installatie kopieën die u wilt distribueren.  

    - **Taken reeksen**: Vouw taken reeksen van **besturings systemen**uit  >   **Task Sequences**en selecteer vervolgens de taken reeks die u wilt distribueren. Hoewel taken reeksen geen inhoud bevatten, hebben ze gekoppelde inhouds afhankelijkheden die worden gedistribueerd.  

      > [!NOTE]  
      > Als u de taken reeks wijzigt, moet u de inhoud opnieuw distribueren.  

3.  Klik op het tabblad **Start** in de groep **Implementatie** op **Inhoud distribueren**. De wizard inhoud distribueren wordt geopend.  

4.  Controleer op de pagina **Algemeen** of de vermelde inhoud de inhoud is die u wilt distribueren, kies of u wilt dat Configuration Manager inhouds afhankelijkheden detecteert die zijn gekoppeld aan de geselecteerde inhoud en voeg de afhankelijkheden toe aan de distributie. Klik vervolgens op **volgende**.  

    > [!NOTE]  
    > U kunt de **afhankelijkheden van gekoppelde inhoud detecteren configureren en deze alleen toevoegen aan deze distributie** -instelling voor het inhouds type van de toepassing. Configuration Manager configureert deze instelling automatisch voor taken reeksen en kan niet worden gewijzigd.  

5.  Controleer op het tabblad **inhoud** of de vermelde inhoud de inhoud is die u wilt distribueren en klik vervolgens op **volgende**.  

    > [!NOTE]  
    > De pagina **inhoud** wordt alleen weer gegeven als de **afhankelijkheden van gekoppelde inhoud detecteren en toevoegen aan deze distributie** -instelling is geselecteerd op de pagina **Algemeen** van de wizard.  

6.  Klik op de pagina **doel van inhoud** op **toevoegen**, kies een van de volgende opties en volg de bijbehorende stap:  

    - **Verzamelingen**: Selecteer **gebruikers verzamelingen** of **apparaat verzamelingen**, klik op de verzameling die is gekoppeld aan een of meer distributiepunten groepen en klik vervolgens op **OK**.  

        > [!NOTE]  
        > Alleen de verzamelingen die aan een distributiepunten groep zijn gekoppeld, worden weer gegeven. Zie [distributiepunt groepen beheren](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) in het onderwerp [distributie punten installeren en configureren voor Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) voor meer informatie over het koppelen van verzamelingen aan distributiepunten groepen.  

    - **Distributie punt**: Selecteer een bestaand distributie punt en klik vervolgens op **OK**. Distributie punten die de inhoud eerder hebben ontvangen, worden niet weer gegeven.  

    - **Distributiepunten groep**: Selecteer een bestaande distributiepunten groep en klik vervolgens op **OK**. Distributiepunt groepen die de inhoud eerder hebben ontvangen, worden niet weer gegeven.  

    Klik op **volgende**als u klaar bent met het toevoegen van inhouds bestemmingen.  

7.  Controleer op de pagina **samen vatting** de instellingen voor de distributie voordat u doorgaat. Klik op **volgende**om de inhoud naar de geselecteerde bestemmingen te distribueren.  

8.  Op de pagina **voortgang** wordt de voortgang van de distributie weer gegeven.  

9. Op de **bevestigings** pagina wordt weer gegeven of de inhoud aan de punten is toegewezen. Zie [inhoud bewaken die u hebt gedistribueerd met Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)voor het controleren van de inhouds distributie.  

##  <a name="use-prestaged-content"></a><a name="bkmk_prestage"></a>Voor bereide inhoud gebruiken  
U kunt voor bereide inhouds bestanden voor toepassingen en pakket typen:  

- Selecteer in de Configuration Manager-console de inhoud die u nodig hebt en gebruik vervolgens de **wizard voor bereid inhouds bestand maken** om een gecomprimeerd, voor bereid inhouds bestand te maken dat de bestanden en gekoppelde meta gegevens bevat voor de inhoud die u hebt geselecteerd.  

- U kunt de inhoud vervolgens hand matig importeren op een site server, secundaire site of distributie punt.  

- Wanneer u het voor bereide inhouds bestand op een site server importeert, worden de inhouds bestanden toegevoegd aan de inhouds bibliotheek op de site server en vervolgens geregistreerd in de site Server database.  

- Wanneer u het voor bereide inhouds bestand op een distributie punt importeert, worden de inhouds bestanden toegevoegd aan de inhouds bibliotheek op het distributie punt en wordt er een status bericht verzonden naar de site server die de site informeert dat de inhoud beschikbaar is op het distributie punt.  

**Beperkingen en overwegingen voor voor bereide inhoud:**  

- **Wanneer het distributie punt zich op de site server bevindt**, moet u het distributie punt niet inschakelen voor voor bereide inhoud. Gebruik in plaats daarvan de procedure in de voor [bereiding van inhoud op een distributie punt op een site server](#bkmk_dpsiteserver).  

- **Wanneer het distributie punt is geconfigureerd als een pull-distributie punt**, moet u het distributie punt niet inschakelen voor voor bereide inhoud. De configuratie voor het vooraf plaatsen van inhoud voor een distributie punt overschrijft de configuratie van het pull-distributie punt. Een pull-distributie punt dat is geconfigureerd voor voor bereide inhoud haalt geen inhoud op uit het bron distributiepunt en ontvangt geen inhoud van de site server.  

- **De inhouds bibliotheek moet op het distributie punt worden gemaakt voordat u inhoud vooraf op het distributie punt kunt**plaatsen. Distribueer ten minste één keer inhoud over het netwerk, voordat u inhoud vooraf op het distributie punt plaatst.  

- **Wanneer u inhoud voorbereidt voor een pakket met een bronpad van een lang pakket** (bijvoorbeeld meer dan 140 tekens), kan het opdracht regel programma voor het uitpakken van inhoud de inhoud voor dat pakket mogelijk niet extra heren naar de inhouds bibliotheek.  

Zie voor *bereide inhoud* in het onderwerp [netwerk bandbreedte voor inhouds beheer beheren](../../../plan-design/hierarchy/manage-network-bandwidth.md) voor meer informatie over het voorbereiden van inhouds bestanden.  

Gebruik de volgende secties om inhoud voor te bereiden.  

###  <a name="step-1-create-a-prestaged-content-file"></a><a name="BKMK_CreatePrestagedContentFile"></a>Stap 1: een voor bereid inhouds bestand maken  
U kunt een gecomprimeerd, voor bereid inhouds bestand maken dat de bestanden en gekoppelde meta gegevens bevat voor de inhoud die u in de Configuration Manager-console selecteert. Gebruik de volgende procedure om een voor bereid inhouds bestand te maken.  

##### <a name="to-create-a-prestaged-content-file"></a>Een voor bereid inhouds bestand maken  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Selecteer in de werk ruimte **software bibliotheek** een van de volgende stappen voor het type inhoud dat u wilt voorbereiden:  

    - **Toepassingen**: Vouw **toepassings beheer**uit, klik op **toepassingen**en selecteer vervolgens de toepassingen die u wilt voorbereiden.  

    - **Pakketten**: Vouw **toepassings beheer**uit, klik op **pakketten**en selecteer vervolgens de pakketten die u wilt voorbereiden.  

    - **Stuur programmapakketten**: Vouw **besturings systemen**uit, klik op **Stuur programmapakketten**en selecteer vervolgens de Stuur programmapakketten die u wilt voorbereiden.  

    - **Installatie kopieën van besturings systeem**: Vouw **besturings systemen**uit, klik op **installatie kopieën van besturings systeem**en selecteer vervolgens de installatie kopieën van het besturings systeem die u wilt voorbereiden.  

    - **Installatie Programma's van besturings systeem**: Vouw **besturings systemen**uit, klik op **installatie Programma's van besturings systeem**en selecteer vervolgens de installatie Programma's van het besturings systeem die u wilt voorbereiden.  

    - **Opstart installatie kopieën**: Vouw **besturings systemen**uit, klik op installatie **kopieën**en selecteer vervolgens de opstart installatie kopieën die u vooraf wilt plaatsen.  

    - **Taken reeksen**: Vouw **besturings systemen**uit, klik op **taken reeksen**en selecteer vervolgens de taken reeks die u vooraf wilt plaatsen.  

3.  Klik op het tabblad **Start** in de groep **implementatie** op **inhouds bestand voor bereiding maken**. De wizard voor bereid inhouds bestand maken wordt geopend.  

    > [!NOTE]  
    > **Voor toepassingen:** Klik op het tabblad **Start** in de groep **toepassing** op voor **bereid inhouds bestand maken**.  
    >   
    > **Voor pakketten:** Klik op het tabblad **Start** in de &lt; groep *pakketnaam*> op voor **bereid inhouds bestand maken**.  

4.  Klik op de pagina **Algemeen** op **Bladeren**, kies de locatie voor het voor bereide inhouds bestand, geef een naam op voor het bestand en klik vervolgens op **Opslaan**. U gebruikt dit vooraf geplaatste inhouds bestand op primaire site servers, secundaire site servers of distributie punten om de inhoud en meta gegevens te importeren.  

5.  Selecteer voor toepassingen **alle afhankelijkheden exporteren** om Configuration Manager de afhankelijkheden die zijn gekoppeld aan de toepassing te detecteren en toe te voegen aan het voor bereide inhouds bestand. Deze instelling is standaard geselecteerd.  

6.  Voer in **Administrator opmerkingen**optionele opmerkingen over het voor bereide inhouds bestand in en klik op **volgende**.  

7.  Controleer op de pagina **inhoud** of de vermelde inhoud de inhoud is die u wilt toevoegen aan het voor bereide inhouds bestand en klik vervolgens op **volgende**.  

8.  Geef op de pagina **inhouds locaties** de distributie punten op waarvan u de inhouds bestanden voor het voor bereide inhouds bestand wilt ophalen. U kunt meer dan één distributie punt selecteren om de inhoud op te halen. De distributie punten worden weer gegeven in de sectie inhouds locaties. In de kolom **inhoud** wordt weer gegeven hoeveel van de geselecteerde pakketten of toepassingen beschikbaar zijn op elk distributie punt. Configuration Manager begint met het eerste distributie punt in de lijst om de geselecteerde inhoud op te halen. vervolgens wordt de lijst omlaag geplaatst om de resterende vereiste inhoud voor het voor bereide inhouds bestand op te halen. Klik op **omhoog** of **omlaag** om de prioriteits volgorde van de distributie punten te wijzigen. Wanneer de distributie punten in de lijst niet alle geselecteerde inhoud bevatten, moet u distributie punten toevoegen aan de lijst die de inhoud bevat of de wizard afsluiten, de inhoud naar ten minste één distributie punt distribueren en vervolgens de wizard opnieuw starten.  

9. Bevestig de details op de pagina **samen vatting** . U kunt teruggaan naar de vorige pagina's en wijzigingen aanbrengen. Klik op **volgende** om het voor bereide inhouds bestand te maken.  

10. Op de pagina **voortgang** wordt de inhoud weer gegeven die wordt toegevoegd aan het voor bereide inhouds bestand.  

11. Controleer op de pagina **voltooiing** of het voor bereide inhouds bestand is gemaakt en klik vervolgens op **sluiten**.  

###  <a name="step-2-assign-the-content-to-distribution-points"></a><a name="BKMK_AssignContentToDistributionPoint"></a>Stap 2: de inhoud toewijzen aan distributie punten  
 Nadat u het inhouds bestand hebt voor bereid, wijst u de inhoud toe aan distributie punten.  

> [!NOTE]  
> Wanneer u een voor bereid inhouds bestand gebruikt om de inhouds bibliotheek op een site server te herstellen en u de inhouds bestanden niet op een distributie punt hoeft voor te bereiden, kunt u deze procedure overs Laan.  

 Gebruik de volgende procedure om de inhoud in het voor bereide inhouds bestand toe te wijzen aan distributie punten.  

> [!IMPORTANT]  
> Controleer of de distributie punten die u wilt voorbereiden, worden geconfigureerd als voor bereide distributie punten of dat de inhoud wordt gedistribueerd naar de distributie punten met behulp van het netwerk.  

##### <a name="to-assign-the-content-to-distribution-points"></a>De inhoud toewijzen aan distributie punten  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Selecteer in de werk ruimte **software bibliotheek** een van de volgende stappen voor het type inhoud dat u hebt geselecteerd tijdens het maken van het voor bereide inhouds bestand:  

    - **Toepassingen**: Vouw **toepassings beheer**uit, klik op **toepassingen**en selecteer vervolgens de toepassingen die u hebt voor bereid.  

    - **Pakketten**: Vouw **toepassings beheer**uit, klik op **pakketten**en selecteer vervolgens de pakketten die u hebt voor bereid.  

    - **Implementatie pakketten**: Vouw **software-updates**uit, klik op **implementatie pakketten**en selecteer vervolgens de implementatie pakketten die u vooraf hebt geplaatst.  

    - **Stuur programmapakketten**: Vouw **besturings systemen**uit, klik op **Stuur programmapakketten**en selecteer vervolgens de Stuur programmapakketten die u vooraf hebt geplaatst.  

    - **Installatie kopieën van besturings systeem**: Vouw **besturings systemen**uit, klik op **installatie kopieën van besturings systeem**en selecteer vervolgens de installatie kopieën van het besturings systeem die u hebt voor bereid.  

    - **Installatie Programma's van besturings systeem**: Vouw **besturings systemen**uit, klik op **installatie Programma's van besturings systeem**en selecteer vervolgens de installatie Programma's van het besturings systeem die u hebt voor bereid.  

    - **Opstart installatie kopieën**: Vouw **besturings systemen**uit, klik op installatie **kopieën**en selecteer vervolgens de opstart installatie kopieën die u hebt voor bereid.  

3.  Klik op het tabblad **Start** in de groep **Implementatie** op **Inhoud distribueren**. De wizard inhoud distribueren wordt geopend.  

4.  Controleer op de pagina **Algemeen** of de vermelde inhoud de inhoud is die u hebt voor bereid, kies of u wilt dat Configuration Manager inhouds afhankelijkheden detecteert die zijn gekoppeld aan de geselecteerde inhoud en voeg de afhankelijkheden toe aan de distributie. Klik vervolgens op **volgende**.  

    > [!NOTE]  
    > U kunt de **afhankelijkheden van gekoppelde inhoud detecteren configureren en deze alleen toevoegen aan deze distributie** -instelling voor het inhouds type van de toepassing. Configuration Manager configureert deze instelling automatisch voor taken reeksen en kan niet worden gewijzigd.  

5.  Controleer op de pagina **inhoud** , indien weer gegeven, of de vermelde inhoud de inhoud is die u wilt distribueren en klik vervolgens op **volgende**.  

    > [!NOTE]  
    > De pagina **inhoud** wordt alleen weer gegeven als de **afhankelijkheden van gekoppelde inhoud detecteren en toevoegen aan deze distributie** -instelling is geselecteerd op de pagina **Algemeen** van de wizard.  

6.  Klik op de pagina **doel van inhoud** op **toevoegen**, kies een van de volgende opties die de distributie punten bevat die moeten worden voor bereid en volg de bijbehorende stap:  

    - **Verzamelingen**: Selecteer **gebruikers verzamelingen** of **apparaat verzamelingen**, klik op de verzameling die is gekoppeld aan een of meer distributiepunten groepen en klik vervolgens op **OK**.  

      > [!NOTE]  
      > Alleen de verzamelingen die aan een distributiepunten groep zijn gekoppeld, worden weer gegeven.  Zie [distributiepunt groepen beheren](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) in het onderwerp [distributie punten installeren en configureren voor Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) voor meer informatie.  

    - **Distributie punt**: Selecteer een bestaand distributie punt en klik vervolgens op **OK**. Distributie punten die de inhoud eerder hebben ontvangen, worden niet weer gegeven.  

    - **Distributiepunten groep**: Selecteer een bestaande distributiepunten groep en klik vervolgens op **OK**. Distributiepunt groepen die de inhoud eerder hebben ontvangen, worden niet weer gegeven.  

    Klik op **volgende**als u klaar bent met het toevoegen van inhouds bestemmingen.  

7.  Controleer op de pagina **samen vatting** de instellingen voor de distributie voordat u doorgaat. Klik op **volgende**om de inhoud naar de geselecteerde bestemmingen te distribueren.  

8.  Op de pagina **voortgang** wordt de voortgang van de distributie weer gegeven.  

9. Op de **bevestigings** pagina wordt weer gegeven of de inhoud is toegewezen aan de distributie punten. Zie [inhoud bewaken die u hebt gedistribueerd met Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)voor het controleren van de inhouds distributie.  

###  <a name="step-3-extract-the-content-from-the-prestaged-content-file"></a><a name="BKMK_ExportContentFromPrestagedContentFile"></a>Stap 3: de inhoud van het voor bereide inhouds bestand extra heren  
Nadat u het voor bereide inhouds bestand hebt gemaakt en de inhoud aan distributie punten hebt toegewezen, kunt u de inhouds bestanden uitpakken naar de inhouds bibliotheek op een site server of distributie punt. Normaal gesp roken hebt u het voor bereide inhouds bestand naar een draag bare schijf gekopieerd, zoals een USB-station, of hebt u inhoud gebrand op media zoals een DVD en deze beschikbaar op de locatie van de site server of het distributie punt waarvoor de inhoud is vereist.  

Gebruik de volgende procedure om de inhouds bestanden hand matig vanuit het voor bereide inhouds bestand te exporteren met behulp van het opdracht regel programma voor het uitpakken van inhoud.  

> [!IMPORTANT]  
> Wanneer u het opdracht regel programma voor het uitpakken van inhoud uitvoert, maakt het hulp programma een tijdelijk bestand bij het maken van het voor bereide inhouds bestand. Het bestand wordt vervolgens gekopieerd naar de doelmap en het tijdelijke bestand wordt verwijderd. U moet over voldoende schijf ruimte beschikken voor dit tijdelijke bestand of het proces mislukt. Het tijdelijke bestand wordt gemaakt op de volgende locatie:  
>   
> - Het tijdelijke bestand wordt gemaakt in dezelfde map die u opgeeft als de doelmap voor het voor bereide inhouds bestand.  

> [!IMPORTANT]  
> De gebruiker die het opdracht regel programma voor het uitpakken van inhoud uitvoert, moet over **beheerders** rechten beschikken voor de computer van waaruit u de voor bereide inhoud uitpakt.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>De inhouds bestanden uit het voor bereide inhouds bestand extra heren  

1.  Kopieer het voor bereide inhouds bestand naar de computer waarvan u de inhoud wilt extra heren.  

2.  Kopieer het opdracht regel programma voor het uitpakken van inhoud vanuit &lt; *ConfigMgrInstallationPath*> \Bin \\ &lt; *platform*> naar de computer van waaruit u het voor bereide inhouds bestand wilt extra heren.  

3.  Open de opdracht prompt en navigeer naar de maplocatie van het voor bereide inhouds bestand en het hulp programma voor het uitpakken van inhoud.  

    > [!NOTE]  
    > U kunt een of meer voor bereide inhouds bestanden ophalen op een site server, secundaire site server of distributie punt.  

4.  Typ **extract content/p:** &lt; *PrestagedFileLocation* > **\\** &lt; *PrestagedFileName* >  **/s** om één bestand te importeren.  

    Typ **extract content/p:** &lt; *PrestagedFileLocation* >  **/s** om alle voor bereide bestanden in de opgegeven map te importeren.  

    Typ bijvoorbeeld **extract content/p: D:\PrestagedFiles\MyPrestagedFile.pkgx/s** waarbij `D:\PrestagedFiles\` de PrestagedFileLocation is, de voor `MyPrestagedFile.pkgx` bereide bestands naam is en `/S` informeert Configuration Manager om alleen inhouds bestanden uit te pakken die nieuwer zijn dan het distributie punt.  

    Wanneer u het voor bereide inhouds bestand op een site server uitpakt, worden de inhouds bestanden toegevoegd aan de inhouds bibliotheek op de site server en vervolgens wordt de beschik baarheid van de inhoud geregistreerd in de site Server database. Wanneer u het voor bereide inhouds bestand op een distributie punt exporteert, worden de inhouds bestanden toegevoegd aan de inhouds bibliotheek op het distributie punt. het distributie punt verzendt een status bericht naar de bovenliggende primaire site server en vervolgens wordt de beschik baarheid van de inhoud geregistreerd in de site database.  

    > [!IMPORTANT]  
    > In het volgende scenario moet u de inhoud bijwerken die u hebt geëxtraheerd uit een voor bereid inhouds bestand wanneer de inhoud wordt bijgewerkt naar een nieuwe versie:  
    >   
    >  1.  U maakt een voor bereid inhouds bestand voor versie 1 van een pakket.  
    >  2.  U werkt de bron bestanden voor het pakket bij met versie 2.  
    >  3.  U extraheert het voor bereide inhouds bestand (versie 1 van het pakket) op een distributie punt.  
    >   
    > Het pakket versie 2 wordt door Configuration Manager niet automatisch naar het distributie punt gedistribueerd. U moet een nieuw voor bereid inhouds bestand maken met de nieuwe bestands versie en vervolgens de inhoud extra heren, het distributie punt bijwerken voor het distribueren van de bestanden die zijn gewijzigd of alle bestanden in het pakket opnieuw distribueren.  

###  <a name="how-to-prestage-content-on-a-distribution-point-on-a-site-server"></a><a name="bkmk_dpsiteserver"></a>Inhoud vooraf plaatsen op een distributie punt op een site server  
Wanneer een distributie punt op een site server is geïnstalleerd, moet u de volgende procedure gebruiken om inhoud voor te bereiden. Dit komt doordat de inhouds bestanden al in de inhouds bibliotheek staan.  

Wanneer het distributie punt niet is ingeschakeld voor de voor bereide inhoud of wanneer het distributie punt zich niet op een site server bevindt, raadpleegt u de sectie voor [bereide inhoud gebruiken](#bkmk_prestage) in dit onderwerp.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Inhoud voorbereiden op distributie punten die zich op een site server bevinden  

1.  Gebruik de volgende stappen om te controleren of het distributie punt niet is ingeschakeld voor voor bereide inhoud.  

    1.  Klik op **Beheer**in de Configuration Manager-console.  

    2.  Klik in de werk ruimte **beheer** op **distributie punten**en selecteer vervolgens het distributie punt dat zich op de site server bevindt.  

    3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

    4.  Controleer op het tabblad **Algemeen** of het selectie vakje **Dit distributie punt inschakelen voor voor bereide inhoud** niet is ingeschakeld.  

2.  Maak het voor bereide inhouds bestand met behulp van de sectie [stap 1: een voor bereid inhouds bestand maken](#BKMK_CreatePrestagedContentFile) in dit onderwerp.  

3.  Wijs de inhoud toe aan het distributie punt met behulp van de sectie [stap 2: de inhoud toewijzen aan distributie punten](#BKMK_AssignContentToDistributionPoint) in dit onderwerp.  

4.  Pak de inhoud van het voor bereide inhouds bestand op de site server uit met behulp van de [stap 3: de inhoud van het voor bereide inhouds bestand extra heren](#BKMK_ExportContentFromPrestagedContentFile) in dit onderwerp.  

    > [!NOTE]  
    > Wanneer het distributie punt zich op een secundaire site bevindt, wacht u ten minste 10 minuten en vervolgens met behulp van een Configuration Manager-console die is verbonden met de bovenliggende primaire site, wijst u de inhoud toe aan het distributie punt op de secundaire site.  

##  <a name="manage-the-content-you-have-distributed"></a><a name="bkmk_manage"></a>De inhoud beheren die u hebt gedistribueerd  
U hebt de volgende opties voor het beheren van inhoud:  
- [Inhoud bijwerken](#update-content)
- [Inhoud opnieuw distribueren](#redistribute-content)
- [Inhoud verwijderen](#remove-content)
- [inhoud valideren](#validate-content)

### <a name="update-content"></a>Inhoud bijwerken
Wanneer de locatie van het bron bestand voor een implementatie wordt bijgewerkt door nieuwe bestanden toe te voegen of bestaande bestanden te vervangen door een nieuwere versie, kunt u de inhouds bestanden op distributie punten bijwerken met behulp van de actie **distributie punten bijwerken** of **inhoud bijwerken** :  
- De inhouds bestanden worden gekopieerd van de oorspronkelijke pakket bron locatie naar de inhouds bibliotheek op de site die eigenaar is van de pakket inhouds bron
- De pakket versie wordt verhoogd  
- Elk exemplaar van de inhouds bibliotheek op site servers en op distributie punten werkt alleen met de bestanden die zijn gewijzigd  

> [!WARNING]  
> De pakket versie voor toepassingen is altijd 1. Wanneer u de inhoud voor een toepassings implementatie type bijwerkt, maakt Configuration Manager een nieuwe inhouds-ID voor het implementatie type en verwijst het pakket naar de nieuwe inhouds-ID.  

#### <a name="to-update-content-on-distribution-points"></a>Inhoud op distributie punten bijwerken  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Selecteer in de werk ruimte **software bibliotheek** een van de volgende stappen voor het type inhoud dat u wilt distribueren:  

    - **Toepassingen**: Vouw toepassingen voor **toepassings beheer**uit  >  **Applications**en selecteer vervolgens de toepassingen die u wilt distribueren. Klik op het tabblad **implementatie typen** en selecteer vervolgens het implementatie type dat u wilt bijwerken.  

    - **Pakketten**: Vouw **toepassings beheer**  >  **pakketten**uit en selecteer vervolgens de pakketten die u wilt bijwerken.  

    - **Implementatie pakketten**: Vouw **Software**  >  -Update-**implementatie pakketten**uit en selecteer vervolgens de implementatie pakketten die u wilt bijwerken.  

    - **Stuur programmapakketten**: Vouw **besturings systemen**  >  **Stuur programmapakketten**uit en selecteer vervolgens de Stuur programmapakketten die u wilt bijwerken.  

    - **Installatie kopieën van besturings systeem**: Vouw besturingssysteem installatie kopieën van besturings **systemen**uit  >  **Operating System Images**en selecteer vervolgens de installatie kopieën van het besturings systeem die u wilt bijwerken.  

    - **Installatie Programma's**van het besturings systeem: Vouw besturings **systemen**  >  **installatie Programma's besturings systeem**uit en selecteer vervolgens de installatie Programma's van het besturings systeem die u wilt bijwerken.  

    - **Opstart installatie**kopieën: Vouw installatie kopieën van **besturings systemen**uit  >   **Boot Images**en selecteer vervolgens de opstart installatie kopieën die u wilt bijwerken.  

3.  Klik op het tabblad **Start** in de groep **implementatie** op **distributie punten bijwerken**en klik vervolgens op **OK** om te bevestigen dat u de inhoud wilt bijwerken.  

    > [!NOTE]  
    > Als u inhoud voor toepassingen wilt bijwerken, klikt u op het tabblad **implementatie typen** , klikt u met de rechter muisknop op het implementatie type, klikt u op **inhoud bijwerken**en klikt u vervolgens op **OK** om te bevestigen dat u de inhoud wilt vernieuwen.  

    > [!NOTE]  
    > Wanneer u inhoud voor opstart installatie kopieën bijwerkt, wordt de wizard distributie punt beheren geopend. Bekijk de informatie op de pagina **samen vatting** en voltooi vervolgens de wizard om de inhoud bij te werken.  

### <a name="redistribute-content"></a>Inhoud opnieuw distribueren
U kunt een pakket opnieuw distribueren om alle inhouds bestanden in het pakket naar distributie punten of distributiepunten groepen te kopiëren en zodoende de bestaande bestanden te overschrijven.  

Gebruik deze bewerking om inhouds bestanden in het pakket te herstellen of de inhoud opnieuw te verzenden wanneer de initiële distributie mislukt. U kunt een pakket opnieuw distribueren vanuit:  

- Pakket eigenschappen  
- Eigenschappen van distributie punt  
- Eigenschappen van distributiepunten groep.  


#### <a name="to-redistribute-content-from-package-properties"></a>Inhoud opnieuw distribueren vanuit pakket eigenschappen  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Selecteer in de werk ruimte **software bibliotheek** een van de volgende stappen voor het type inhoud dat u wilt distribueren:  

    - **Toepassingen**: Vouw toepassingen voor **toepassings beheer**uit  >   **Applications**en selecteer vervolgens de toepassing die u opnieuw wilt distribueren.  

    - **Pakketten**: Vouw **toepassings beheer**  >  **pakketten**uit en selecteer vervolgens het pakket dat u opnieuw wilt distribueren.  

    - **Implementatie pakketten**: Vouw **Software-update**  >   -**implementatie pakketten**uit en selecteer vervolgens het implementatie pakket dat u opnieuw wilt distribueren.  

    - **Stuur programmapakketten**: Vouw **besturings systemen**  >  **Stuur programmapakketten**uit en selecteer vervolgens het stuur programmapakket dat u opnieuw wilt distribueren.  

    - **Installatie kopieën van besturings systeem**: Vouw besturingssysteem installatie kopieën van besturings **systemen**uit  >  **Operating System Images**en selecteer vervolgens de installatie kopie van het besturings systeem die u opnieuw wilt distribueren.  

    - **Installatie Programma's voor besturings** **systemen**: Vouw besturingssysteem installatie Programma's van besturings systeem uit  >  **Operating System Installers**en selecteer vervolgens het installatie programma van het besturings systeem dat u opnieuw wilt distribueren.  

    - **Opstart installatie**kopieën: Vouw installatie kopieën van **besturings systemen**uit  >   **Boot Images**en selecteer vervolgens de opstart installatie kopie die u opnieuw wilt distribueren.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Klik op het tabblad **inhouds locaties** , selecteer het distributie punt of distributiepunt groep waarin u de inhoud opnieuw wilt distribueren, klik op opnieuw **distribueren**en klik vervolgens op **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Inhoud opnieuw distribueren vanuit eigenschappen van distributie punt  

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  Klik in de werk ruimte **beheer** op **distributie punten**en selecteer vervolgens het distributie punt waarvoor u inhoud opnieuw wilt distribueren.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Klik op het tabblad **inhoud** , selecteer de inhoud die u opnieuw wilt distribueren, klik op opnieuw **distribueren**en klik vervolgens op **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Inhoud opnieuw distribueren vanuit de eigenschappen van een distributiepunten groep  

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  Klik in de werk ruimte **beheer** op **distributiepunten groepen**en selecteer vervolgens de distributiepunten groep waarvan u de inhoud opnieuw wilt distribueren.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Klik op het tabblad **inhoud** , selecteer de inhoud die u opnieuw wilt distribueren, klik op opnieuw **distribueren**en klik vervolgens op **OK**.  

    > [!IMPORTANT]  
    > De inhoud van het pakket wordt opnieuw gedistribueerd naar alle distributie punten in de distributiepunten groep.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>De SDK gebruiken om de replicatie van inhoud af te dwingen
U kunt de **RetryContentReplication** Windows Management INSTRUMENTATION (WMI)-klasse methode van de Configuration Manager SDK gebruiken om te forceren dat Distribution Manager inhoud van de bron locatie naar de inhouds bibliotheek kopieert.  

Gebruik deze methode alleen voor het afdwingen van replicatie wanneer u inhoud opnieuw moet distribueren nadat er problemen zijn met de normale replicatie van inhoud (meestal bevestigd door het knoop punt controle van de-console).   

Zie [methode RetryContentReplication in klasse SMS_CM_UpdatePackages](../../../../develop/reference/sum/retrycontentreplication-method-in-class-sms_cm_updatepackages.md)voor meer informatie over deze SDK-optie.

### <a name="remove-content"></a>Inhoud verwijderen
Wanneer u niet langer inhoud op uw distributie punten nodig hebt, kunt u de inhouds bestanden op het distributie punt verwijderen.  

- Pakket eigenschappen  
- Eigenschappen van distributie punt  
- Eigenschappen van distributiepunten groep.  

Als de inhoud echter is gekoppeld aan een ander pakket dat naar hetzelfde distributie punt is gedistribueerd, kunt u de inhoud niet verwijderen.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Pakket inhouds bestanden verwijderen van distributie punten  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Selecteer in de werk ruimte **software bibliotheek** een van de volgende stappen voor het type inhoud dat u wilt verwijderen:  

    - **Toepassingen**: Vouw toepassingen voor **toepassings beheer**uit  >  **Applications**en selecteer vervolgens de toepassing die u wilt verwijderen.  

    - **Pakketten**: Vouw **toepassings beheer**  >  **pakketten**uit en selecteer vervolgens het pakket dat u wilt verwijderen.  

    - **Implementatie pakketten**: Vouw **Software**  >  -Update-**implementatie pakketten**uit en selecteer vervolgens het implementatie pakket dat u wilt verwijderen.  

    - **Stuur programmapakketten**: Vouw **besturings systemen**  >  **Stuur programmapakketten**uit en selecteer vervolgens het stuur programmapakket dat u wilt verwijderen.  

    - **Installatie kopieën van besturings systeem**: Vouw **besturingssysteem**  >  **installatie kopieën**van besturings systemen uit en selecteer vervolgens de installatie kopie van het besturings systeem die u wilt verwijderen.  

    - **Installatie Programma's voor besturings**systemen: Vouw **besturingssysteem**  >  **installatie Programma's**van besturings systeem uit en selecteer vervolgens het installatie programma van het besturings systeem dat u wilt verwijderen.  

    - **Opstart installatie**kopieën: Vouw installatie kopieën van **besturings systemen**uit  >  **Boot Images**en selecteer vervolgens de opstart installatie kopie die u wilt verwijderen.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Klik op het tabblad **inhouds locaties** , selecteer het distributie punt of distributiepunt groep waarvan u de inhoud wilt verwijderen, klik op **verwijderen**en klik vervolgens op **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Pakket inhoud verwijderen uit eigenschappen van distributie punt  

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  Klik in de werk ruimte **beheer** op **distributie punten**en selecteer vervolgens het distributie punt waarin u de inhoud wilt verwijderen.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Klik op het tabblad **inhoud** , selecteer de inhoud die u wilt verwijderen, klik op **verwijderen**en klik vervolgens op **OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Inhoud verwijderen uit de eigenschappen van een distributiepunten groep  

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  Klik in de werk ruimte **beheer** op **distributiepunten groepen**en selecteer vervolgens de distributiepunten groep waarvan u de inhoud wilt verwijderen.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Klik op het tabblad **inhoud** , selecteer de inhoud die u wilt verwijderen, klik op **verwijderen**en klik vervolgens op **OK**.  


### <a name="validate-content"></a>Inhoud valideren
Het validatie proces voor inhoud verifieert de integriteit van inhouds bestanden op distributie punten. U kunt inhouds validatie op basis van een schema inschakelen of hand matig de inhouds validatie initiëren vanuit de eigenschappen van distributie punten en pakketten.  

Wanneer het proces voor inhouds validatie wordt gestart, controleert Configuration Manager de inhouds bestanden op distributie punten en als de bestands-hash onverwacht is voor de bestanden op het distributie punt, Configuration Manager een status bericht maken dat u kunt bekijken in de werk ruimte **bewaking** .  

Zie [distributiepunt configuraties](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) in het onderwerp [distributie punten installeren en configureren voor Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md) voor meer informatie over het configureren van de planning voor inhouds validatie.  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Inhouds validatie initiëren voor alle inhoud op een distributie punt  

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  Klik in de werk ruimte **beheer** op **distributie punten**en selecteer vervolgens het distributie punt waarvoor u inhoud wilt valideren.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Selecteer op het tabblad **inhoud** het pakket waarin u de inhoud wilt valideren, klik op **valideren**, klik op **OK**en klik vervolgens op **OK**. Het inhouds validatie proces wordt gestart voor het pakket op het distributie punt.  

5.  Als u de resultaten van het proces voor het valideren van inhoud wilt weer geven, vouwt u in de werk ruimte **bewaking** **distributie status**uit en klikt u op het knoop punt **inhouds status** . De inhoud voor elk pakket type (bijvoorbeeld toepassing, software-update pakket en opstart installatie kopie) wordt weer gegeven. Zie [inhoud bewaken die u hebt gedistribueerd met Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)voor meer informatie over het controleren van de inhouds status.  

#### <a name="to-initiate-content-validation-for-a-package"></a>Validatie van inhoud initiëren voor een pakket  

1.  Klik in de Configuration Manager-console op **Softwarebibliotheek**.  

2.  Selecteer in de werk ruimte **software bibliotheek** een van de volgende stappen voor het type inhoud dat u wilt valideren:  

    - **Toepassingen**: Vouw toepassingen voor **toepassings beheer**uit  >  **Applications**en selecteer vervolgens de toepassing die u wilt valideren.  

    - **Pakketten**: Vouw **toepassings beheer**  >  **pakketten**uit en selecteer vervolgens het pakket dat u wilt valideren.  

    - **Implementatie pakketten**: Vouw **Software**  >  -Update-**implementatie pakketten**uit en selecteer vervolgens het implementatie pakket dat u wilt valideren.  

    - **Stuur programmapakketten**: Vouw **besturings systemen**  >  **Stuur programmapakketten**uit en selecteer vervolgens het stuur programmapakket dat u wilt valideren.  

    - **Installatie kopieën van besturings systeem**: Vouw besturingssysteem installatie kopieën van besturings **systemen**uit  >  **Operating System Images**en selecteer vervolgens de installatie kopie van het besturings systeem die u wilt valideren.  

    - **Installatie Programma's voor besturings**systemen: Vouw **besturingssysteem**  >   **installatie Programma's**van besturings systeem uit en selecteer vervolgens het installatie programma van het besturings systeem dat u wilt valideren.  

    - **Opstart installatie**kopieën: Vouw installatie kopieën van **besturings systemen**uit  >  **Boot Images**en selecteer vervolgens de opstart installatie kopie die u vooraf wilt plaatsen.  

3.  Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  

4.  Selecteer op het tabblad **inhouds locaties** het distributie punt of distributiepunt groep waarin u de inhoud wilt valideren, klik op **valideren**, klik op **OK**en klik vervolgens op **OK**. Het inhouds validatie proces wordt gestart voor de inhoud van het geselecteerde distributie punt of distributiepunt groep.  

5.  Als u de resultaten van het proces voor het valideren van inhoud wilt weer geven, vouwt u in de werk ruimte **bewaking** **distributie status**uit en klikt u op het knoop punt **inhouds status** . De inhoud voor elk pakket type (bijvoorbeeld toepassing, software-update pakket en opstart installatie kopie) wordt weer gegeven. Zie [inhoud bewaken die u hebt gedistribueerd met Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)voor meer informatie over het controleren van de status van de inhoud.  
