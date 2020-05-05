---
title: Stuurprogramma's beheren
titleSuffix: Configuration Manager
description: Gebruik de Configuration Manager-stuurprogrammacatalogus om apparaatstuurprogramma's te importeren, stuur Programma's te groeperen in pakketten en deze pakketten te distribueren naar distributie punten.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8fffa72e45f2f9e063fb0072882c2a5278694cee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724123"
---
# <a name="manage-drivers-in-configuration-manager"></a>Stuur Programma's beheren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager biedt een stuurprogrammacatalogus die u kunt gebruiken om de Windows-apparaatstuurprogramma's in uw Configuration Manager omgeving te beheren. Gebruik de stuurprogrammacatalogus om apparaatstuurprogramma's te importeren in Configuration Manager, om ze te groeperen in pakketten en om die pakketten te distribueren naar distributie punten. Apparaatstuurprogramma's kunnen worden gebruikt wanneer u het volledige besturings systeem op de doel computer installeert en wanneer u Windows PE in een opstart installatie kopie gebruikt. Windows-apparaatstuurprogramma's bestaan uit een Setup-informatie bestand (INF) en eventuele aanvullende bestanden die vereist zijn voor de ondersteuning van het apparaat. Wanneer u een besturings systeem implementeert, verkrijgt Configuration Manager de hardware-en platform informatie voor het apparaat uit het bijbehorende INF-bestand. 



## <a name="driver-categories"></a><a name="BKMK_DriverCategories"></a>Categorieën van Stuur Programma's

Wanneer u apparaatstuurprogramma's importeert, kunt u ze toewijzen aan een categorie. Met categorieën voor apparaatstuurprogramma's kunnen apparaatstuurprogramma's die op vergelijkbare wijze worden gebruikt, samen worden gegroepeerd in de stuurprogrammacatalogus. Stel bijvoorbeeld alle apparaatstuurprogramma's voor netwerk adapters in op een specifieke categorie. Wanneer u vervolgens een taken reeks maakt die de stap [Stuur Programma's automatisch Toep assen](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) bevat, geeft u een categorie apparaatstuurprogramma's op. Configuration Manager scant vervolgens de hardware en selecteert de toepasselijke Stuur Programma's uit die categorie in de fase van het systeem om te gebruiken Windows Setup.  



## <a name="driver-packages"></a><a name="BKMK_ManagingDriverPackages"></a> Driverpakketten

Groepeert vergelijk bare apparaatstuurprogramma's in pakketten om besturingssysteem implementaties te stroom lijnen. U kunt bijvoorbeeld een stuur programmapakket maken voor elke computer fabrikant in uw netwerk. U kunt een stuur programmapakket maken wanneer u stuur Programma's rechtstreeks in de stuurprogrammacatalogus importeert in het knoop punt **Stuur programmapakketten** . Nadat u een stuur programmapakket hebt gemaakt, distribueert u het naar distributie punten. Vervolgens kunnen Configuration Manager client computers de Stuur Programma's installeren als dat nodig is. 

Houd rekening met de volgende punten:  

- Wanneer u een stuur programmapakket maakt, moet de bron locatie van het pakket verwijzen naar een lege netwerk share die niet door een ander Stuur programmapakket wordt gebruikt. De SMS-provider moet machtigingen voor **volledig beheer** voor die locatie hebben.  

- Wanneer u apparaatstuurprogramma's toevoegt aan een stuur programmapakket, Configuration Manager deze kopiëren naar de bron locatie van het pakket. U kunt toevoegen aan een stuur programmapakket alleen apparaatstuurprogramma's die u hebt geïmporteerd en die zijn ingeschakeld in de stuurprogrammacatalogus.  

- U kunt een subset van de apparaatstuurprogramma's uit een bestaand Stuur programmapakket kopiëren. Maak eerst een nieuw Stuur programmapakket. Vervolgens voegt u de subset met apparaatstuurprogramma's toe aan het nieuwe pakket en distribueert u vervolgens het nieuwe pakket naar een distributie punt.  

- Wanneer u takenreeksen gebruikt om stuurprogramma's te installeren, moet u stuurprogrammapakketten met minder dan 500 apparaatstuurprogramma's maken.


### <a name="create-a-driver-package"></a><a name="BKMK_CreatingDriverPackages"></a>Een stuur programmapakket maken  

> [!IMPORTANT]  
> Als u een stuur programmapakket wilt maken, moet u een lege netwerkmap hebben die niet door een ander Stuur programmapakket wordt gebruikt. In de meeste gevallen moet u een nieuwe map maken voordat u deze procedure start.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **Stuur programmapakketten** .  

2. Selecteer **Stuur programmapakket maken**op het tabblad **Start** van het lint in de groep **maken** .  

3. Geef een beschrijvende **naam** op voor het stuur programmapakket.  

4. Voer een optionele **Opmerking** in voor het stuur programmapakket. Gebruik deze beschrijving om informatie te geven over de inhoud of het doel van het stuur programmapakket.  

5. Geef in het vak **Pad** een lege bronmap op voor het stuurprogrammapakket. Elk stuurprogrammapakket moet een unieke map gebruiken. Dit pad is vereist als netwerk locatie.  

   > [!IMPORTANT]  
   > Het site Server account moet machtigingen voor **volledig beheer** hebben voor de opgegeven bronmap.  

Het nieuwe Stuur programmapakket bevat geen stuur Programma's. In de volgende stap worden Stuur Programma's toegevoegd aan het pakket.  

Als het knooppunt **Stuurprogrammapakketten** verschillende pakketten bevat, kunt u mappen toevoegen aan het knooppunt om de pakketten onder te verdelen in logische groepen.  


### <a name="additional-actions-for-driver-packages"></a><a name="BKMK_PackageActions"></a> Aanvullende acties voor stuurprogrammapakketten  

U kunt extra acties uitvoeren om stuur programmapakketten te beheren wanneer u een of meer Stuur programmapakketten selecteert in het knoop punt **Stuur programmapakketten** . 


#### <a name="create-prestage-content-file"></a>Voorbereid inhoudsbestand maken
Hiermee maakt u bestanden die u kunt gebruiken om hand matig inhoud en bijbehorende meta gegevens te importeren. Gebruik voorbereide inhoud wanneer u lage netwerkbandbreedte hebt tussen de siteserver en de distributiepunten waar het stuurprogrammapakket wordt opgeslagen.

#### <a name="delete"></a>Verwijderen
Hiermee verwijdert u het stuurprogrammapakket uit het knooppunt **Stuurprogrammapakketten** .

#### <a name="distribute-content"></a>Inhoud distribueren
Distribueert het stuurprogrammapakket naar distributiepunten, distributiepuntgroepen en distributiepuntgroepen die zijn gekoppeld aan verzamelingen.

#### <a name="manage-access-accounts"></a>Toegangsaccounts beheren
Hiermee worden toegangsaccounts voor het stuurprogrammapakket toegevoegd, gewijzigd of verwijderd.

Zie [accounts die worden gebruikt in Configuration Manager](../../core/plan-design/hierarchy/accounts.md)voor meer informatie over pakket toegangs accounts.

#### <a name="move"></a>Verplaatsen
Verplaatst het stuurprogrammapakket naar een andere map in het knooppunt **Stuurprogrammapakketten** .

#### <a name="update-distribution-points"></a>Distributiepunten bijwerken
Werkt het apparaatstuurprogrammapakket bij op alle distributiepunten waar het pakket wordt opgeslagen. Deze bewerking kopieert alleen de inhoud die is gewijzigd sinds de laatste keer het werd gedistribueerd.

#### <a name="properties"></a>Eigenschappen
Hiermee opent u het dialoog venster **Eigenschappen** . Bekijk en wijzig de inhoud en eigenschappen van het stuur programma. Wijzig bijvoorbeeld de naam en beschrijving van het stuur programma, schakel het in of uit en geef op welke platformen kunnen worden uitgevoerd. 

<!--3607716, fka 1358270-->
Vanaf versie 1810 bevatten de Stuur programmapakketten meta gegevens velden voor de **fabrikant** en het **model**. Gebruik deze velden voor het labelen van Stuur programmapakketten met informatie om te helpen bij algemene housekeeping, of om oude en dubbele Stuur Programma's te identificeren die u kunt verwijderen. Op het tabblad **Algemeen** selecteert u een bestaande waarde in de vervolg keuzelijst of voert u een teken reeks in om een nieuwe vermelding te maken.

In het knoop punt **Stuur programmapakketten** worden deze velden weer gegeven in de lijst met de kolommen **fabrikant** **en stuurprogrammamodel van** het stuur programma. Ze kunnen ook worden gebruikt als Zoek criterium.

Vanaf versie 1906 kunt u deze kenmerken gebruiken om inhoud vooraf in de cache op te slaan op een client. Zie [inhoud vooraf in cache configureren](../deploy-use/configure-precache-content.md)voor meer informatie.<!--4224642-->  




## <a name="device-drivers"></a><a name="BKMK_DeviceDrivers"></a>Apparaatstuurprogramma's

U kunt Stuur Programma's installeren op doel computers zonder ze op te nemen in de installatie kopie van het besturings systeem die is geïmplementeerd. Configuration Manager biedt een stuurprogrammacatalogus die verwijzingen bevat naar alle Stuur Programma's die u in Configuration Manager importeert. De stuurprogrammacatalogus bevindt zich in de werkruimte **Softwarebibliotheek** en bestaat uit twee knooppunten: **Stuurprogramma's** en **Stuurprogrammapakketten**. Het knoop punt **Stuur Programma's** geeft een lijst van alle Stuur Programma's die u in de stuurprogrammacatalogus hebt geïmporteerd.  


### <a name="import-device-drivers-into-the-driver-catalog"></a><a name="BKMK_ImportDrivers"></a> Apparaatstuurprogramma's in de stuurprogrammacatalogus importeren  

Voordat u een stuur programma kunt gebruiken wanneer u een besturings systeem implementeert, importeert u het in de stuurprogrammacatalogus. Importeer alleen de Stuur Programma's die u wilt installeren als onderdeel van de implementaties van het besturings systeem om ze beter te beheren. Sla meerdere versies van Stuur Programma's op in de catalogus om een eenvoudige manier te bieden om bestaande Stuur Programma's bij te werken wanneer de vereisten voor hardware-apparaten worden gewijzigd in uw netwerk.  

Als onderdeel van het import proces voor het apparaatstuurprogramma, Configuration Manager leest de volgende eigenschappen over het stuur programma:
- Provider
- Klasse
- Versie
- Handtekening
- Ondersteunde hardware
- Ondersteunde platform gegevens

Standaard krijgt het stuur programma de naam van het eerste hardware-apparaat dat het ondersteunt. U kunt de naam van het apparaatstuurprogramma later wijzigen. De lijst met ondersteunde platformen is gebaseerd op de informatie in het INF-bestand van het stuurprogramma. Omdat de nauw keurigheid van deze informatie kan variëren, moet u hand matig controleren of het stuur programma wordt ondersteund nadat u het in de catalogus hebt geïmporteerd.  

Nadat u apparaatstuurprogramma's in de catalogus hebt geïmporteerd, voegt u deze toe aan de pakketten met stuur programmapakketten of opstart installatie kopieën.  

> [!IMPORTANT]  
> U kunt geen apparaatstuurprogramma's rechtstreeks importeren in een submap van het knoop punt **Stuur Programma's** . U kunt een apparaatstuurprogramma importeren in een submap door het apparaatstuurprogramma eerst te importeren in het knooppunt **Stuurprogramma's** en het stuurprogramma vervolgens te verplaatsen naar de submap.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Proces om Windows-apparaatstuurprogramma's te importeren in de stuurprogrammacatalogus  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **besturings systemen**uit en selecteer het knoop punt **Stuur Programma's** .  

2. Selecteer op het tabblad **Start** van het lint in de groep **maken** de optie **stuur programma importeren** om de **wizard Nieuw stuur programma importeren**te starten.  

3. Geef op de pagina **stuur programma zoeken** de volgende opties op:  

    - **Alle Stuur Programma's importeren in het volgende netwerkpad (UNC)**: Geef het netwerkpad op om alle apparaatstuurprogramma's in een specifieke map te importeren. Bijvoorbeeld: `\\servername\share\folder`.  

        > [!NOTE]  
        > Als er veel submappen en een groot aantal INF-bestanden voor Stuur Programma's zijn, kan dit proces enige tijd duren.  

    - **Een specifiek stuur programma importeren**: Geef het netwerkpad naar het inf-bestand van het Windows-apparaatstuurprogramma op om een specifiek stuur programma te importeren uit een map.  

    - **Geef de optie op voor dubbele Stuur Programma's**: Selecteer hoe u wilt dat Configuration Manager de stuurprogrammagroepen beheert wanneer u een dubbel apparaatstuurprogramma importeert  
        - **Het stuur programma importeren en een nieuwe categorie toevoegen aan de bestaande categorieën**  
        - **Het stuur programma importeren en de bestaande categorieën blijven gebruiken**  
        - **Het stuur programma importeren en de bestaande categorieën overschrijven**  
        - **Het stuur programma niet importeren**  

    > [!IMPORTANT]  
    > Als u stuurprogramma's importeert, moet de siteserver over de machtiging **Lezen** beschikken voor de map. Het importeren mislukt als dit niet het geval is.  

4. Geef op de pagina **Stuur programmagegevens** de volgende opties op:  

    - **Stuur Programma's die niet voor komen in een opslag-of netwerk klasse verbergen (voor installatie kopieën)**: gebruik deze instelling om alleen opslag-en netwerk Stuur Programma's weer te geven. Met deze optie worden andere Stuur Programma's verborgen die doorgaans niet nodig zijn voor installatie kopieën, zoals een video stuur programma of modem stuur programma.  

    - **Stuur Programma's die niet digitaal zijn ondertekend verbergen**: micro soft adviseert alleen stuur Programma's te gebruiken die digitaal zijn ondertekend  

    - Selecteer in de lijst met stuurprogramma's de stuurprogramma's die u wilt importeren naar de stuurprogrammacatalogus.  

    - **Deze stuurprogramma's inschakelen en computers toestaan ze te installeren**: selecteer deze instelling om computers toestemming te geven de apparaatstuurprogramma's te installeren. Deze optie is standaard ingeschakeld.  

        > [!IMPORTANT]  
        > Als een apparaatstuurprogramma een probleem veroorzaakt of als u de installatie van een apparaatstuurprogramma wilt onderbreken, schakelt u dit tijdens het importeren uit. U kunt ook Stuur Programma's uitschakelen nadat u ze hebt geïmporteerd.  

    - Selecteer **Categorieën**om de apparaatstuurprogramma's toe te wijzen aan een beheer categorie voor filter doeleinden, zoals "Desk Tops" of "notebooks". Kies vervolgens een bestaande categorie of maak een nieuwe categorie. Gebruik categorieën om te bepalen welke Stuur Programma's worden toegepast door de taken reeks stap [Stuur Programma's automatisch Toep assen](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) .  

5. Kies op de pagina **stuur programma toevoegen aan pakketten** of u de Stuur Programma's aan een pakket wilt toevoegen.  

    - Selecteer de stuurprogrammapakketten die worden gebruikt om de apparaatstuurprogramma's te distribueren.  

        Selecteer, indien nodig, **nieuw pakket** om een nieuw Stuur programmapakket te maken. Wanneer u een nieuw Stuur programmapakket maakt, moet u een netwerk share opgeven die niet wordt gebruikt door andere Stuur programmapakketten.  

    - Als het pakket al is gedistribueerd naar distributie punten, selecteert u **Ja** in het dialoog venster om de opstart installatie kopieën op distributie punten bij te werken. U kunt geen apparaatstuurprogramma's gebruiken totdat ze naar distributie punten worden gedistribueerd. Als u **Nee**selecteert, voert u de actie **distributie punt bijwerken** uit voordat u de opstart installatie kopie gebruikt. Als het stuur programmapakket nog nooit is gedistribueerd, moet u de actie **inhoud distribueren** gebruiken in het knoop punt **Stuur programmapakketten** .  

6. Kies op de pagina **stuur programma toevoegen aan opstart installatie kopieën** of u de apparaatstuurprogramma's wilt toevoegen aan bestaande opstart installatie kopieën.  

    > [!NOTE]  
    > Voeg alleen opslag-en netwerk Stuur Programma's toe aan de installatie kopieën.  

    - Selecteer **Ja** in het dialoog venster om de opstart installatie kopieën op distributie punten bij te werken. U kunt geen apparaatstuurprogramma's gebruiken totdat ze naar distributie punten worden gedistribueerd. Als u **Nee**selecteert, voert u de actie **distributie punt bijwerken** uit voordat u de opstart installatie kopie gebruikt. Als het stuur programmapakket nog nooit is gedistribueerd, moet u de actie **inhoud distribueren** gebruiken in het knoop punt **Stuur programmapakketten** .  

    - Configuration Manager waarschuwt u als de architectuur van een of meer Stuur Programma's niet overeenkomt met de architectuur van de opstart installatie kopieën die u hebt geselecteerd. Als ze niet overeenkomen, selecteert u **OK**. Ga terug naar de pagina **Stuur programmagegevens** en wis de Stuur Programma's die niet overeenkomen met de architectuur van de geselecteerde opstart installatie kopie. Als u bijvoorbeeld een x64- en x86-installatiekopie selecteert, moeten alle stuurprogramma's beide architecturen ondersteunen. Als u een x64-installatiekopie selecteert, moeten alle stuurprogramma's de x64-architectuur ondersteunen.  

        > [!NOTE]  
        > - De architectuur is gebaseerd op de architectuur die is gerapporteerd in het INF-rapport van de fabrikant.  
        > - Als een stuur programma meldt dat het beide architecturen ondersteunt, kunt u het importeren in een van de opstart installatie kopieën.  

    - Configuration Manager waarschuwt u als u apparaatstuurprogramma's toevoegt die geen netwerk-of opslag Stuur Programma's zijn voor een opstart installatie kopie. In de meeste gevallen zijn ze niet nodig voor de opstart installatie kopie. Selecteer **Ja** om de Stuur Programma's toe te voegen aan de opstart installatie kopie of op **Nee** om terug te gaan en de selectie van het stuur programma te wijzigen.  

    - Configuration Manager waarschuwt u als een of meer van de geselecteerde Stuur Programma's niet goed zijn ondertekend. Selecteer **Ja** om door te gaan en selecteer **Nee** om terug te gaan en wijzigingen aan te brengen in de selectie van het stuur programma.  

7. Voltooi de wizard.  


### <a name="manage-device-drivers-in-a-driver-package"></a><a name="BKMK_ModifyDriverPackage"></a> Beheren van apparaatstuurprogramma's in een stuurprogrammapakket  

Gebruik de volgende procedures om de stuurprogrammapakketten en opstartinstallatiekopieën te wijzigen. Als u een stuur programma wilt toevoegen of verwijderen, moet u het eerst vinden in het knoop punt **Stuur Programma's** . Bewerk vervolgens de pakketten of opstart installatie kopieën waaraan het geselecteerde stuur programma is gekoppeld.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **Stuur Programma's** .  

2. Selecteer de apparaatstuurprogramma's die u wilt toevoegen aan een stuur programmapakket.  

3. Selecteer **bewerken**op het tabblad **Start** van het lint in de groep **stuur programma** en kies **Stuur programmapakketten**.  

4. Selecteer het selectievakje van de stuurprogrammapakketten waaraan u de apparaatstuurprogramma's wilt toevoegen om een apparaatstuurprogramma toe te voegen. Deselecteer het selectievakje van de stuurprogrammapakketten waaraan u de apparaatstuurprogramma's wilt toevoegen om een apparaatstuurprogramma te verwijderen.  

    Als u apparaatstuurprogramma's toevoegt die zijn gekoppeld aan Stuur programmapakketten, kunt u eventueel ook een nieuw pakket maken. Selecteer **nieuw pakket**, waarmee het dialoog venster **Nieuw Stuur programmapakket** wordt geopend.  

5. Als het pakket al is gedistribueerd naar distributie punten, selecteert u **Ja** in het dialoog venster om de opstart installatie kopieën op distributie punten bij te werken. U kunt geen apparaatstuurprogramma's gebruiken totdat ze naar distributie punten worden gedistribueerd. Als u **Nee**selecteert, voert u de actie **distributie punt bijwerken** uit voordat u de opstart installatie kopie gebruikt. Als het stuur programmapakket nog nooit is gedistribueerd, moet u de actie **inhoud distribueren** gebruiken in het knoop punt **Stuur programmapakketten** . Voordat de stuurprogramma's beschikbaar worden, moet u het stuurprogrammapakket op de distributiepunten bijwerken.  

    Selecteer **OK** wanneer u klaar bent.  


### <a name="manage-device-drivers-in-a-boot-image"></a><a name="BKMK_ManageDriversBootImage"></a> Apparaatstuurprogramma's in een opstartinstallatiekopie beheren  

U kunt toevoegen aan opstart installatie kopieën Windows-apparaatstuurprogramma's die zijn geïmporteerd in de catalogus. Gebruik de volgende richtlijnen wanneer u apparaatstuurprogramma's toevoegt aan een opstartinstallatiekopie:  

- Voeg alleen opslag-en netwerk Stuur Programma's toe aan installatie kopieën. Andere typen Stuur Programma's zijn doorgaans niet vereist in Windows PE. Stuur Programma's die niet vereist zijn, nemen de grootte van de opstart installatie kopie onnodig toe.  

- Voeg alleen apparaatstuurprogramma's voor Windows 10 toe aan een opstart installatie kopie. De vereiste versie van Windows PE is gebaseerd op Windows 10.  

- Zorg ervoor dat u het juiste apparaatstuurprogramma gebruikt voor de architectuur van de opstart installatie kopie. Voeg geen x86-apparaatstuurprogramma toe aan een x64-opstart installatie kopie.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Proces voor het wijzigen van de apparaatstuurprogramma's die zijn gekoppeld aan een opstart installatie kopie  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **Stuur Programma's** .  

2. Selecteer de apparaatstuurprogramma's die u wilt toevoegen aan het stuur programmapakket.  

3. Selecteer **bewerken**op het tabblad **Start** van het lint in de groep **stuur programma** en kies vervolgens **opstart installatie kopieën**.  

4. Selecteer het selectievakje van de installatiekopie waaraan u de apparaatstuurprogramma's wilt toevoegen om een apparaatstuurprogramma toe te voegen. Deselecteer het selectievakje van de installatiekopie waaraan u de apparaatstuurprogramma's wilt toevoegen om een apparaatstuurprogramma te verwijderen.  

5. Als u de distributie punten waarop de opstart installatie kopie wordt opgeslagen niet wilt bijwerken, wist u het selectie vakje **distributie punten bijwerken na voltooiing** . Standaard worden de distributiepunten bijgewerkt wanneer de installatiekopie wordt bijgewerkt.  

    - Selecteer **Ja** in het dialoog venster om de opstart installatie kopieën op distributie punten bij te werken. U kunt geen apparaatstuurprogramma's gebruiken totdat ze naar distributie punten worden gedistribueerd. Als u **Nee**selecteert, voert u de actie **distributie punt bijwerken** uit voordat u de opstart installatie kopie gebruikt. Als het stuur programmapakket nog nooit is gedistribueerd, moet u de actie **inhoud distribueren** gebruiken in het knoop punt **Stuur programmapakketten** .  

    - Configuration Manager waarschuwt u als de architectuur van een of meer Stuur Programma's niet overeenkomt met de architectuur van de opstart installatie kopieën die u hebt geselecteerd. Als ze niet overeenkomen, selecteert u **OK**. Ga terug naar de detail pagina van het **stuur programma** en wis de Stuur Programma's die niet overeenkomen met de architectuur van de geselecteerde opstart installatie kopie. Als u bijvoorbeeld een x64- en x86-installatiekopie selecteert, moeten alle stuurprogramma's beide architecturen ondersteunen. Als u een x64-installatiekopie selecteert, moeten alle stuurprogramma's de x64-architectuur ondersteunen.  

        > [!NOTE]
        > - De architectuur is gebaseerd op de architectuur die is gerapporteerd in het INF-rapport van de fabrikant.  
        > - Als een stuurprogramma aangeeft dat beide architecturen worden ondersteund, kunt u het naar een van beide installatiekopieën importeren.  

    - Configuration Manager waarschuwt u als u apparaatstuurprogramma's toevoegt die geen netwerk-of opslag Stuur Programma's zijn voor een opstart installatie kopie. In de meeste gevallen zijn ze niet nodig voor de opstart installatie kopie. Selecteer **Ja** om de Stuur Programma's toe te voegen aan de opstart installatie kopie of **Nee** om terug te gaan en de selectie van het stuur programma te wijzigen.  

    - Configuration Manager waarschuwt u als een of meer van de geselecteerde Stuur Programma's niet goed zijn ondertekend. Selecteer **Ja** om door te gaan of selecteer **Nee** om terug te gaan en wijzigingen aan te brengen in de selectie van het stuur programma.  


### <a name="additional-actions-for-device-drivers"></a><a name="BKMK_DriverActions"></a>Aanvullende acties voor apparaatstuurprogramma's  

U kunt extra acties uitvoeren om stuur Programma's te beheren wanneer u deze selecteert in het knoop punt **Stuur Programma's** .  

#### <a name="categorize"></a>Categoriseren
Wist, beheert of stelt een beheer categorie voor de geselecteerde Stuur Programma's in.

#### <a name="delete"></a>Verwijderen
Hiermee verwijdert u het stuur programma uit het knoop punt **Stuur Programma's** en verwijdert u het stuur programma ook uit de bijbehorende distributie punten.

#### <a name="disable"></a>Uitschakelen
Verhindert dat het stuur programma wordt geïnstalleerd. Met deze actie wordt het stuur programma tijdelijk uitgeschakeld. De taken reeks kan geen uitgeschakeld stuur programma installeren wanneer u een besturings systeem implementeert. 

> [!Note]  
> Met deze actie wordt alleen voor komen dat stuur Programma's worden geïnstalleerd met behulp van de taken reeks stap **stuur programma automatisch Toep assen** .

#### <a name="enable"></a>Inschakelen
Hiermee kunnen Configuration Manager-client computers en-taken reeksen het apparaatstuurprogramma installeren wanneer u het besturings systeem implementeert.

#### <a name="move"></a>Verplaatsen
Verplaatst het apparaatstuurprogramma naar een andere map in het knooppunt **Stuurprogramma's** .

#### <a name="properties"></a>Eigenschappen
Hiermee opent u het dialoog venster **Eigenschappen** . Bekijk en wijzig de eigenschappen van het stuur programma. U kunt bijvoorbeeld de naam en beschrijving wijzigen, het apparaat in-of uitschakelen en opgeven op welke platformen het kan worden uitgevoerd.



## <a name="use-task-sequences-to-install-drivers"></a><a name="BKMK_TSDrivers"></a>Taken reeksen gebruiken om stuur Programma's te installeren  

Gebruik taken reeksen om de manier waarop het besturings systeem wordt geïmplementeerd, te automatiseren. Elke stap in de taken reeks kan een specifieke actie uitvoeren, zoals het installeren van een stuur programma. U kunt de volgende twee taken reeks stappen gebruiken om apparaatstuurprogramma's te installeren wanneer u een besturings systeem implementeert:  

- [Stuurprogramma's automatisch toepassen](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): in deze stap kunt u apparaatstuurprogramma's automatisch vergelijken en installeren als onderdeel van de implementatie van een besturingssysteem. U kunt de taken reeks stap zodanig configureren dat alleen het meest overeenkomende stuur programma voor elk gedetecteerd apparaat wordt geïnstalleerd. U kunt ook opgeven dat met de stap alle compatibele Stuur Programma's voor elk gedetecteerd hardwareapparaat worden geïnstalleerd. vervolgens kunt Windows Setup het beste stuur programma kiezen. U kunt ook een categorie van een stuur programma opgeven om de Stuur Programma's te beperken die beschikbaar zijn voor deze stap.  

- [Stuurprogrammapakket toepassen](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): in deze stap kunt u alle apparaatstuurprogramma's in een specifiek stuurprogrammapakket beschikbaar maken voor Windows Setup. Windows Setup zoekt in de opgegeven stuurprogrammapakketten naar de vereiste apparaatstuurprogramma's. Wanneer u zelfstandige media maakt, moet u deze stap gebruiken om apparaatstuurprogramma's te installeren.  

Wanneer u deze taken reeks stappen gebruikt, kunt u ook opgeven hoe de Stuur Programma's worden geïnstalleerd op de computer waarop u het besturings systeem implementeert. Raadpleeg taken [reeksen beheren om taken te automatiseren](../deploy-use/manage-task-sequences-to-automate-tasks.md)voor meer informatie.  



## <a name="driver-reports"></a><a name="BKMK_DriverReports"></a>Rapporten van Stuur Programma's  

U kunt diverse rapporten in de rapportencategorie **Stuurprogrammabeheer** gebruiken om algemene informatie over de apparaatstuurprogramma's in de stuurprogrammacatalogus te bepalen. Zie [Introduction to Reporting](../../core/servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over rapporten.

