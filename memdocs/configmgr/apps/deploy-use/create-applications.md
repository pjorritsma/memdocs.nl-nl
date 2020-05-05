---
title: Toepassingen maken
titleSuffix: Configuration Manager
description: Maak toepassingen met implementatie typen, detectie methoden en vereisten voor het installeren van software.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 33a95ae78fdc80c6c08b59cfe5ec5b2e88485a8f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074653"
---
# <a name="create-applications-in-configuration-manager"></a>Toepassingen maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Een Configuration Manager toepassing definieert de meta gegevens over de toepassing. Een toepassing heeft een of meer implementatie typen. Deze implementatie typen bevatten de installatie bestanden en informatie die nodig zijn voor het installeren van software op apparaten. Een implementatie type bevat ook regels, zoals detectie methoden en vereisten. Deze regels bepalen wanneer en hoe de client de software installeert.  

Toepassingen maken met behulp van de volgende methoden:  

- Automatisch een toepassings-en implementatie type maken door de installatie bestanden van de toepassing te lezen:  
  - [Een toepassing maken](#bkmk_create) en [automatisch](#bkmk_auto-app) toepassings gegevens detecteren
  - [Een implementatie type maken](#bkmk_create-dt) en informatie over het implementatie type [automatisch identificeren](#bkmk_auto-dt)

- Maak hand matig een toepassing en voeg later implementatie typen toe:  
  - [Een toepassing maken](#bkmk_create) en [hand matig](#bkmk_manual-app) toepassings gegevens opgeven
  - [Maak een implementatie type](#bkmk_create-dt) en [Geef hand matig](#bkmk_manual-dt) informatie over het implementatie type op

- [Een toepassing importeren](#bkmk_import) uit een bestand  

Dit artikel bevat ook de volgende informatie over het configureren van een implementatie type:  

- [Inhoud](#bkmk_dt-content)
- [Taken reeks](#bkmk_dt-ts)
- [Detectie methode](#bkmk_dt-detect)
- [Gebruikers ervaring](#bkmk_dt-ux)
- [Vereisten](#bkmk_dt-require)
- [Retour codes](#bkmk_dt-return)
- [Afhankelijkheden](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a>Een toepassing maken  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .  

2. Selecteer op het tabblad **Start** van het lint in de groep **maken** de optie **toepassing maken**.  

Vervolgens automatisch detecteren of hand matig informatie over de toepassing opgeven:  

- [Automatisch](#bkmk_auto-app) toepassings gegevens detecteren om een basis toepassing te maken met één implementatie type. Bijvoorbeeld een Windows Installer bestand dat geen afhankelijkheden of vereisten heeft. Nadat u een toepassing hebt gemaakt met behulp van deze procedure, bewerkt u deze indien nodig. U kunt implementatie typen toevoegen of wijzigen en detectie methoden, afhankelijkheden of vereisten toevoegen.  

- [Hand matig](#bkmk_manual-app) toepassings informatie opgeven om complexere toepassingen te maken. Definieer meer dan één implementatie type, afhankelijkheden, detectie methoden of vereisten.  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a>Toepassings gegevens automatisch detecteren  

1. Selecteer op de pagina **Algemeen** van de wizard toepassing maken de optie **automatisch informatie over deze toepassing detecteren uit installatie bestanden**.  

2. Selecteer in de vervolg keuzelijst **type** het installatie bestands type van de toepassing die u wilt gebruiken voor het detecteren van toepassings informatie. Zie [implementatie typen die worden ondersteund door Configuration Manager](create-applications.md#bkmk_deploy-types)voor meer informatie over de beschik bare installatie typen.  

3. Geef in het vak **locatie** het installatie bestand van de toepassing op dat u wilt gebruiken voor het detecteren van toepassings informatie. Deze locatie is een netwerkpad () of`\\server\share\filename`een Store-koppeling. U moet toegang hebben tot het netwerkpad en alle submappen die toepassings inhoud bevatten.  

    > [!IMPORTANT]  
    > Wanneer u **Windows Installer (\*MSI-bestand)** selecteert als een toepassings type, importeert de site alle bestanden in de opgegeven map. Vervolgens worden deze bestanden naar distributie punten verzonden. Zorg ervoor dat de opgegeven map alleen de bestanden bevat die nodig zijn om de toepassing te installeren. Micro soft TESTT Configuration Manager voor de ondersteuning van Maxi maal 20.000 bestanden in het toepassings pakket. Als uw toepassing meer bestanden bevat, kunt u overwegen om meerdere toepassingen met minder bestanden te maken.  

4. Controleer de informatie op de pagina **informatie importeren** van de wizard toepassing maken en selecteer **volgende**. Selecteer indien nodig **vorige** om terug te gaan en eventuele fouten op te lossen.  

5. Geef op de pagina **algemene informatie** van de wizard toepassing maken de volgende informatie op:  

    > [!NOTE]  
    > Als Configuration Manager deze informatie automatisch detecteert van de installatie bestanden van de toepassing, is deze hier al ingevuld. Het kan bovendien zijn dat de weergegeven opties wisselen op basis van het toepassingstype dat u maakt.  

    - Algemene informatie over de toepassing, zoals de toepassings **naam**, de opmerkingen van de **beheerder**, de **Uitgever**en de **Software versie**. Als hulp bij het vinden van de toepassing in de Configuration Manager-console, geeft u een **optionele verwijzing**op of selecteert u **Beheer categorieën**.  

    - **Installatie programma**: Geef het installatie programma en eventueel vereiste eigenschappen op die nodig zijn om het implementatie type van de toepassing te installeren.  

        > [!TIP]  
        > Als het installatie programma niet wordt weer gegeven, kiest u **Bladeren** en bladert u naar de locatie van het installatie programma.  

    - **Installatie gedrag**: Selecteer een van de drie opties voor de manier waarop Configuration Manager dit implementatie type installeert. Zie [gebruikers ervaring](#bkmk_dt-ux)voor meer informatie over deze opties.  

    - **Een automatische VPN-verbinding gebruiken (indien geconfigureerd)**: als u een VPN-profiel hebt geïmplementeerd op het apparaat waarop de gebruiker de app start, koppelt u het VPN wanneer de app wordt gestart. Deze optie is alleen voor Windows 8,1 en Windows Phone 8,1. Als u op Windows Phone 8,1-apparaten meer dan één VPN-profiel op het apparaat implementeert, worden automatische VPN-verbindingen niet ondersteund. Zie [VPN-profielen](../../protect/deploy-use/vpn-profiles.md)voor meer informatie.  

    - **Deze toepassing inrichten voor alle gebruikers op het apparaat**<!--1358310-->: Richt een toepassing in met een Windows-app-pakket voor alle gebruikers op het apparaat. Zie [Windows-toepassingen maken](../get-started/creating-windows-applications.md#bkmk_provision)voor meer informatie.  

       > [!Tip]  
       > Als u een bestaande toepassing wijzigt, bevindt deze instelling zich op het tabblad **gebruikers ervaring** van de implementatie type-eigenschappen van het Windows-app-pakket.  

6. Klik op **volgende**, Controleer de toepassings gegevens op de pagina **samen vatting** en voltooi vervolgens de wizard toepassing maken.  

De nieuwe toepassing wordt nu weer gegeven in het knoop punt **toepassingen** van de Configuration Manager-console. U hebt een toepassing gemaakt.

Zie [implementatie typen voor de toepassing maken](#bkmk_create-dt)als u meer implementatie typen wilt toevoegen of andere instellingen wilt configureren.  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a>Toepassings informatie hand matig opgeven  

1. Selecteer op de pagina **Algemeen** van de wizard toepassing maken **de optie hand matig de toepassings gegevens opgeven**en klik vervolgens op **volgende**.  

2. Geef **algemene informatie** over de toepassing op:  

    - De **naam** van de toepassing is vereist en moet korter zijn dan 256 tekens.  

    - **Opmerkingen**van de beheerder, **Uitgever**en **Software versie** zijn aanvullende meta gegevens om de toepassing verder te beschrijven.  

    - Als hulp bij het vinden van de toepassing in de Configuration Manager-console, geeft u een **optionele verwijzing**op of selecteert u **Beheer categorieën**.  

    - **Publicatie datum**  

    - Selecteer gebruikers of groepen die verantwoordelijk zijn voor deze toepassing als **eigen aren** en **contact personen voor ondersteuning**. Deze waarden worden standaard ingesteld op uw gebruikers naam.  

3. Geef op de pagina **Software Center** van de wizard toepassing maken de volgende informatie op:  

    > [!Note]  
    > In versie 1902 en eerder heette deze pagina de naam **toepassingscatalogus**.

    - **Geselecteerde taal**: in de vervolg keuzelijst selecteert u de taal versie van de toepassing die u wilt instellen. Kies **toevoegen/verwijderen** om meer talen voor deze toepassing in te stellen.  

    - **Gelokaliseerde toepassings naam**: Geef de toepassings naam op in de geselecteerde taal.  

        > [!IMPORTANT]  
        > Een gelokaliseerde toepassings naam is vereist voor elke taal versie die u instelt.  

    - **Gebruikers categorieën**: Kies **bewerken** om toepassings Categorieën op te geven in de geselecteerde taal. Gebruikers van software Center gebruiken deze categorieën om de toepassingen te filteren en te sorteren.  

        > [!Note]  
        > In versie 1902 en eerder zijn gebruikers categorieën alleen van toepassing op beschik bare implementaties voor gebruikers verzamelingen. Als een toepassing wordt geïmplementeerd naar een computer verzameling, worden de gebruikers categorieën genegeerd.
        >
        > Vanaf versie 1906 worden gebruikers categorieën voor toepassings implementaties met een apparaat als filters weer gegeven in Software Center. Deze implementaties kunnen beschikbaar of vereist zijn.
        >
        > <!-- 4726793 -->Het wijzigen van de naam of het verwijderen van een categorie wordt niet automatisch toegepast op apps met deze categorie. Deze wijzigingen zijn van toepassing op de volgende revisie van de app. U kunt dit probleem omzeilen door de naam te wijzigen of te verwijderen:
        >
        > - Schakel eerst het selectie vakje voor de categorie uit voor alle apps die ernaar verwijzen. Pas vervolgens die wijziging toe, die de app wijzigt.
        >     - In plaats van de actie NaamWijzigen, vervolgens maakt u een nieuwe categorie met de nieuwe naam en voegt u de nieuwe categorie toe aan de relevante apps.
        >     - U kunt de categorie verwijderen nadat u de apps hebt gereviseerd.

    - **Gebruikers documentatie**: Geef de locatie op van een bestand waaruit Software Center-gebruikers meer informatie over deze toepassing kunnen krijgen. Deze locatie is een website adres of een netwerkpad en een bestands naam. Zorg ervoor dat gebruikers toegang hebben tot deze locatie.  

    - **Koppelings tekst**: Geef de tekst op die wordt weer gegeven in plaats van ' aanvullende informatie ' wanneer de gebruikers documentatie is opgegeven.  

    - **Privacy-URL**: Geef een website adres op voor de privacyverklaring van de toepassing.  

    - **Gelokaliseerde beschrijving**: Voer een beschrijving in voor deze toepassing in de geselecteerde taal.  

    - **Tref woorden**: Voer een lijst met tref woorden in de geselecteerde taal in. Met deze tref woorden kunnen gebruikers van het Software Center zoeken naar de toepassing.  

    - **Pictogram**: Selecteer **Bladeren** om een pictogram voor deze toepassing te selecteren. Als u geen pictogram opgeeft, wordt Configuration Manager een standaard pictogram gebruikt. Pictogrammen kunnen pixel dimensies hebben van Maxi maal 512 x 512.  

4. Klik op de pagina **implementatie typen** van de wizard toepassing maken op **toevoegen** om een nieuw implementatie type te maken. Zie [implementatie typen voor de toepassing maken](#bkmk_create-dt)voor meer informatie.  

5. Klik op **volgende**, Controleer de toepassings gegevens op de pagina **samen vatting** en voltooi vervolgens de wizard toepassing maken.  

De nieuwe toepassing wordt nu weer gegeven in het knoop punt **toepassingen** van de Configuration Manager-console.  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a>Implementatie typen voor de toepassing maken  

Als u [automatisch toepassings gegevens detecteert](#bkmk_auto-app), hoeft u de stappen in deze sectie mogelijk niet te volt ooien.  

> [!Note]  
> Wanneer u de eigenschappen van een bestaand implementatie type bekijkt, komen de volgende secties overeen met de tabbladen van het venster Eigenschappen van implementatie type:  
>
> - [Inhoud](#bkmk_dt-content)
> - [Taken reeks](#bkmk_dt-ts)
> - [Detectie methode](#bkmk_dt-detect)
> - [Gebruikers ervaring](#bkmk_dt-ux)
> - [Vereisten](#bkmk_dt-require)
> - [Retour codes](#bkmk_dt-return)
> - [Afhankelijkheden](#bkmk_dt-depend)
>  
> Zie [controleren op actieve uitvoer bare bestanden](deploy-applications.md#bkmk_exe-check)voor meer informatie over het tabblad **installatie gedrag** van de eigenschappen van een implementatie type.  

### <a name="start-the-create-deployment-type-wizard"></a>De wizard implementatie type maken starten  

Er zijn drie manieren om de wizard implementatie type maken te starten:

- Ga **in het knoop punt toepassingen**naar de werk ruimte **software bibliotheek** in de Configuration Manager-console, vouw **toepassings beheer**uit en selecteer het knoop punt **toepassingen** . Selecteer een toepassing en selecteer vervolgens **implementatie type maken** in het lint.  

- **Bij het maken van een toepassing**: wanneer u [hand matig toepassings informatie opgeeft](#bkmk_manual-app) in de wizard toepassing maken, selecteert u **toevoegen** op de pagina implementatie typen.  

- **Van toepassings eigenschappen**: Selecteer een bestaande toepassing in het knoop punt **toepassingen** en selecteer **Eigenschappen**. Ga naar het tabblad **implementatie typen** en selecteer **toevoegen**.

Gebruik vervolgens een van de volgende procedures om informatie over het implementatie type [automatisch te identificeren](#bkmk_auto-dt) of [hand matig](#bkmk_manual-dt) op te geven.  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a>Informatie over het implementatie type automatisch identificeren  

1. Op de pagina **Algemeen** van de wizard implementatie type maken:  

    1. Selecteer het bestands **type** voor de installatie van de toepassing om de informatie over het implementatie type te detecteren.  

    2. Selecteer **automatisch informatie identificeren over dit implementatie type vanuit installatie bestanden**.  

    3. Geef in het vak **locatie** het installatie bestand van de toepassing op dat u wilt gebruiken voor het detecteren van de implementatie type-informatie. Deze locatie is een netwerkpad () of`\\server\share\filename`een Store-koppeling. U moet toegang hebben tot het netwerkpad en alle submappen die toepassings inhoud bevatten.  

2. Controleer de informatie op de pagina **informatie importeren** van de wizard implementatie type maken en selecteer **volgende**. Selecteer indien nodig **vorige** om terug te gaan en eventuele fouten op te lossen.  

3. Geef op de pagina **algemene informatie** van de wizard implementatie type maken de volgende informatie op:  

    > [!NOTE]  
    > Sommige implementatietype-informatie is mogelijk al ingevuld als deze automatisch is opgehaald uit de installatiebestanden van de toepassing. Daarnaast kunnen de weer gegeven opties verschillen, afhankelijk van het implementatie type dat u maakt.  

    - **Algemene informatie** over het implementatie type:  
        - De **naam** is vereist  

        - **Opmerkingen** van de beheerder om deze verder te beschrijven  

        - Beschik bare **talen**  

    - **Installatie programma**: Geef het installatie programma en alle eigenschappen op die u nodig hebt om het implementatie type te installeren.  

    - **Installatie gedrag**: Selecteer een van de drie opties voor de manier waarop Configuration Manager dit implementatie type installeert. Zie [gebruikers ervaring](#bkmk_dt-ux)voor meer informatie over deze opties.  

    - **Een automatische VPN-verbinding gebruiken (indien geconfigureerd)**: als u een VPN-profiel hebt geïmplementeerd op het apparaat waarop de gebruiker de app start, koppelt u het VPN wanneer de app wordt gestart. Deze optie is alleen voor Windows 8,1 en Windows Phone 8,1. Als u op Windows Phone 8,1-apparaten meer dan één VPN-profiel op het apparaat implementeert, worden automatische VPN-verbindingen niet ondersteund. Zie [VPN-profielen](../../protect/deploy-use/vpn-profiles.md)voor meer informatie.  

4. Klik op **volgende**en ga vervolgens verder met de [inhouds opties voor het implementatie type](#bkmk_dt-content).  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a>Hand matig de implementatie type-informatie opgeven  

1. Kies op de pagina **Algemeen** van de wizard implementatie type maken in de vervolg keuzelijst **type** het installatie bestands type van de toepassing voor dit implementatie type.

2. Selecteer **hand matig de implementatie type-informatie opgeven**en selecteer **volgende**.

3. Geef op de pagina **algemene informatie** van de wizard implementatie type maken een **naam** op voor het implementatie type. Geef desgewenst **beheerders opmerkingen**op, selecteer de **talen** voor dit implementatie type en selecteer vervolgens **volgende**.  

4. Ga door naar de [inhouds opties voor het implementatie type](#bkmk_dt-content).  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a>**Inhouds** opties implementatie type  

Geef op de pagina **inhoud** de volgende informatie op:  

> [!Note]  
> Wanneer u de eigenschappen van een bestaand implementatie type bekijkt, worden enkele van deze opties weer gegeven op het tabblad **inhoud** en op het tabblad **Program ma's** .  

- **Locatie van inhoud**: Geef de locatie van de inhoud voor dit implementatie type op of selecteer **Bladeren** om de map van het implementatie type te kiezen.  

    > [!IMPORTANT]  
    > Het systeem account van de site Server computer moet machtigingen hebben voor de opgegeven inhouds locatie.  

  - **Inhoud in de client cache behouden**: de Configuration Manager-client bewaart de inhoud van het implementatie type oneindig in de cache. De-client persistente inhoud, zelfs als de app al is geïnstalleerd. Deze optie is nuttig bij sommige implementaties, zoals Windows Installer-gebaseerde software. Windows Installer hebt een lokale kopie van de bron inhoud nodig voor het Toep assen van updates. Met deze optie wordt de beschik bare cache ruimte verminderd. Als u deze optie selecteert, kan dit ertoe leiden dat een grote implementatie op een later tijdstip mislukt als er onvoldoende ruimte beschikbaar is in de cache.  

- **Installatie programma**: Geef de naam op van het installatie programma en eventueel vereiste installatie parameters.  

  - **Installatie start over**: Geef eventueel de map op die het installatie programma voor het implementatie type heeft. Deze map kan een absoluut pad op de client zijn of een pad naar de map van het distributie punt met de installatie bestanden.  

- **Programma verwijderen**: Geef desgewenst de naam van het Uninstall-programma en eventueel vereiste para meters op.  

  - **Verwijderen start over**: Geef eventueel de map op die het Uninstall-programma voor het implementatie type heeft. Deze map kan een absoluut pad op de client zijn. Het kan ook een relatief pad zijn op een distributie punt van de map met het pakket.  

- **Reparatie programma**: voor de implementatie typen Windows Installer en script kunt u eventueel de naam van het reparatie programma en eventuele vereiste para meters opgeven.<!--1357866-->  

  - **Herstellen gestart in**: Geef eventueel de map op die het reparatie programma voor het implementatie type heeft. Deze map kan een absoluut pad op de client zijn. Het kan ook een relatief pad zijn op een distributie punt van de map met het pakket.  

- **Programma voor installeren en verwijderen uitvoeren als 32-bits proces op 64-bits-clients**: gebruik het 32-bits bestand en register locaties op Windows-computers om het installatie programma voor het implementatie type uit te voeren.  

#### <a name="deployment-type-properties-content-options"></a>**Inhouds** opties voor eigenschappen van implementatie type

Wanneer u de eigenschappen van een implementatie type bekijkt, worden de volgende opties alleen weer gegeven op het tabblad **inhoud** :

- **Instellingen voor inhoud verwijderen**:  

  - **Hetzelfde als de installatie-inhoud**: Selecteer deze optie als de inhoud voor installeren en verwijderen hetzelfde is. Dit is de standaardoptie.  

  - **Geen uninstall-inhoud**: Selecteer deze optie als u niet wilt dat de inhoud van de toepassing wordt verwijderd.  

  - **Verschilt van de installatie-inhoud**: Selecteer deze optie als de uninstall-inhoud afwijkt van de installatie-inhoud.  

    - **Locatie van installatie van inhoud**: Geef het netwerkpad op naar de inhoud die wordt gebruikt voor het verwijderen van de toepassing.  

- **Clients toestaan distributie punten van de standaard site grens groep te gebruiken**: Geef op of clients de software van een distributie punt in de standaard grens groep van de site moeten downloaden en installeren wanneer de inhoud niet beschikbaar is vanaf een distributie punt in de huidige of grens groepen van de groep.  

- **Implementatie opties**: Geef op of clients de toepassing moeten downloaden wanneer ze een distributie punt van een neighbor of de standaard site grens groepen gebruiken.  

- **Clients toestaan inhoud te delen met andere clients in hetzelfde subnet**: hier kunt u aangeven of het gebruik van BranchCache moet worden ingeschakeld voor het downloaden van inhoud. Zie [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)voor meer informatie. BranchCache is altijd ingeschakeld op clients. Deze instelling is verwijderd in versie 1802, omdat clients BranchCache gebruiken als het distributie punt deze ondersteunt.  

### <a name="deployment-type-task-sequence-options"></a><a name="bkmk_dt-ts"></a>Opties voor de **taken reeks** implementatie type

<!--3555953-->

Zie [implementatie type voor taken reeksen](../get-started/creating-windows-applications.md#bkmk_tsdt)voor meer informatie over het implementatie type voor taken reeksen, te beginnen met versie 2002.

Geef op de pagina **taken reeks** de volgende informatie op:

- **Taken reeks installeren**: Selecteer een taken reeks die het installatie proces voor deze app uitvoert.

- **Taken reeks verwijderen** (optioneel): Selecteer een taken reeks waarmee deze app wordt verwijderd.

> [!TIP]  
> Als uw taken reeks niet in de lijst wordt weer gegeven, controleert u of deze geen besturingssysteem implementatie of upgrade stappen voor het besturings systeem bevat. Zorg er ook voor dat deze niet is gemarkeerd als een taken reeks met een hoge impact. Raadpleeg voor meer informatie de vereisten voor het [implementatie type van de taken reeks](../get-started/creating-windows-applications.md#bkmk_tsdt).

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a>Opties voor de **detectie methode** voor het implementatie type

Met deze procedure wordt een detectie methode ingesteld die de aanwezigheid van het implementatie type aangeeft. Met andere woorden, of op het Windows-apparaat al de toepassing is geïnstalleerd. Gebruik een van de volgende twee methoden om een detectie methode te maken:

- [Regels configureren voor het detecteren van de aanwezigheid van dit implementatie type](#bkmk_detect-rule)
- [Een aangepast script gebruiken om de aanwezigheid van dit implementatie type te detecteren](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a>Regels configureren voor het detecteren van de aanwezigheid van dit implementatie type

1. Op de pagina **detectie methode** is de optie voor het **configureren van regels voor het detecteren van de aanwezigheid van dit implementatie type** standaard geselecteerd. Selecteer **component toevoegen**.  

2. Selecteer in het dialoog venster **detectie regel** het **type instelling** om de aanwezigheid van het implementatie type te detecteren:  

    - **Bestands systeem**: detecteren of een opgegeven bestand of map op een apparaat bestaat. Deze detectie geeft aan dat de toepassing is geïnstalleerd. Geef de volgende aanvullende informatie op:  

        - **Type**: Selecteer of het een bestand of map is.  

        - **Pad** (vereist): Typ of blader naar het lokale pad op het apparaat dat het bestand of de map bevat. Bijvoorbeeld `C:\Program Files`. U kunt geen gedeeld netwerkpad opgeven. Als u **Bladeren**selecteert, bladert u naar het lokale bestands systeem of maakt u verbinding met een representatieve client om te bladeren.  

        - **Naam van bestand of map** (vereist): Geef de naam op van het specifieke bestand of de map die moet worden gedetecteerd in het bovenstaande pad. Als de client dit bestand of deze map op het apparaat detecteert, beschouwt deze de toepassing als geïnstalleerd op het apparaat.  

        - **Dit bestand of deze map is gekoppeld aan een 32-bits toepassing op 64-bits systemen**: deze optie is standaard geselecteerd. De client controleert eerst 32-bits bestands locaties voor het bestand of de map die is opgegeven. Als het bestand of de map niet wordt gevonden, zoekt de client vervolgens naar 64-bits locaties.  

    - **REGI ster**: detecteert of een opgegeven register sleutel of register waarde bestaat op een client apparaat. Deze detectie geeft aan dat de toepassing is geïnstalleerd. Geef de volgende aanvullende informatie op:  

        - **Hive** (vereist): Kies een register component in de vervolg keuzelijst. Bijvoorbeeld `HKEY_LOCAL_MACHINE`.  

        - **Sleutel** (vereist): Geef de register sleutel op waarnaar moet worden gezocht in de bovenstaande component. Bijvoorbeeld `SOFTWARE\Microsoft\Office`.  

        - **Waarde** (optioneel): Voer een specifieke waarde in die moet worden gedetecteerd in de bovenstaande sleutel. Als u wilt dat de client de (standaard) waarde detecteert, schakelt u de optie voor het **gebruik van de register sleutel waarde (standaard) voor detectie**in. Wanneer u een waarde invoert of deze optie inschakelt, moet u een **gegevens type**selecteren.  

        - **Deze register sleutel is gekoppeld aan een 32-bits toepassing op 64-bits systemen**: Selecteer deze optie om eerst 32-bits register locaties te controleren voor de opgegeven register sleutel. Als de register sleutel niet wordt gevonden, zoekt de client naar 64-bits locaties.  

    - **Windows Installer**: detecteert of een opgegeven Windows Installer bestand bestaat op een client apparaat. Deze detectie geeft aan dat de toepassing is geïnstalleerd. Geef de MSI- **product code** op die op de client moet worden gedetecteerd. Als u **Bladeren**selecteert, kiest u het MSI-bestand waaruit u de product code wilt lezen.

3. Geef aan de onderkant van het venster detectie regel op of het item moet bestaan of voldoen aan een regel. Als u bijvoorbeeld een bestand detecteert, is de volgende optie standaard geselecteerd: **de bestandssysteem instelling moet op het doel systeem bestaan om de aanwezigheid van deze toepassing te kunnen aangeven**. Selecteer de andere optie om een regel voor detectie te maken op basis van eigenschappen van bestanden of mappen. Deze eigenschappen zijn onder andere datum gewijzigd, datum gemaakt, versie of grootte. Deze regel criteria verschillen voor elk instellings type.  

4. Selecteer **OK** om het dialoog venster **detectie regel** te sluiten.  

Wanneer u meer dan één detectie methode voor een implementatie type maakt, kunt u componenten groeperen om complexere logica te maken.  

#### <a name="group-detection-clauses-optional"></a>Groeps detectie componenten *(optioneel)*

1. Maak drie of meer clausules voor detectie methoden voor een implementatie type.  

2. Selecteer twee of meer opeenvolgende componenten en selecteer vervolgens **groep**. U ziet dat de haakjes worden toegevoegd aan de gekoppelde kolommen, die laten zien waar de groep begint en eindigt.  

    Voorbeeld:

    | Connector  |  ( | Component           |  )  |
    |------------|----|------------------|-----|
    |            |    | MSI-product code |     |
    | of         | (  | bestand1. Text bestaat|     |
    | And        |    | bestand2. txt bestaat al | )   |

3. Als u de groep wilt verwijderen, selecteert u de gegroepeerde componenten en selecteert u **groep opheffen**.  

*Ga door* naar de volgende sectie over het gebruik van een aangepast script als detectie methode. Of *Ga* door naar de opties voor de [gebruikers ervaring](#bkmk_dt-ux) voor het implementatie type.

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a>Een aangepast script gebruiken om te controleren op de aanwezigheid van een implementatie type  

1. Schakel op de pagina **detectie methode** het selectie vakje **een aangepast script gebruiken om de aanwezigheid van dit implementatie type op te sporen** . Selecteer vervolgens **Edit**.  

2. Selecteer in het dialoog venster **Script Editor** een **script type** om het implementatie type te detecteren: Power shell, VBScript of JScript.  

    > [!Note]  
    > Wanneer een Windows Power shell-script wordt uitgevoerd als een app-detectie methode, roept de Configuration Manager `-NoProfile` -client Power shell aan met de para meter. Met deze optie wordt Power shell zonder profielen gestart. Een Power shell-profiel is een script dat wordt uitgevoerd wanneer Power shell wordt gestart. <!--3607762-->  

3. Voer in het vak **script inhoud** het script in dat u wilt gebruiken of plak de inhoud van een bestaand script. Kies **openen** om naar een bestaand opgeslagen script te bladeren. Selecteer **wissen** om de tekst in het veld script inhoud te verwijderen. Schakel, indien nodig, de optie voor het **uitvoeren van een script als 32-bits proces op 64-bits-clients**.  

    > [!NOTE]  
    > De maximale grootte voor een script is 32 KB.  

4. Selecteer **OK** om het script op te slaan en het dialoog venster **Script Editor** te sluiten. Met de wizard implementatie type maken worden de velden van het **type script** en de **script lengte** bijgewerkt met details over uw script.

#### <a name="about-custom-script-detection-methods"></a>Over aangepaste script detectie methoden  

Configuration Manager controleert de resultaten van het script. Het leest de waarden die door het script zijn geschreven naar de standaard uitvoerstroom (STDOUT), de standaardfoutstroom (STDERR) en de afsluitcode. Als het script wordt afgesloten met een andere waarde dan nul, mislukt het script en is de detectie status van de toepassing *onbekend*. Als de afsluit code nul is en STDOUT gegevens bevat, wordt de detectie status van de toepassing *geïnstalleerd*.

> [!TIP]
> Bij het schrijven van een detectie script als u een afsluit code van nul retourneert, maar geen uitvoer retourneert (gegevens in STDOUT), wordt de toepassing niet gedetecteerd als geïnstalleerd. Zie de volgende voor beelden voor meer informatie.

Gebruik de volgende tabellen om te controleren of een toepassing wordt geïnstalleerd vanuit de uitvoer van een script:  

##### <a name="zero-exit-code"></a>Geen afsluit code

|STDOUT|STDERR|Script resultaat|Detectie status van toepassing|
|---------|---------|---------|---------|
|Leeg|Leeg|Geslaagd|Niet geïnstalleerd|
|Leeg|Niet leeg|Fout|Onbekend|
|Niet leeg|Leeg|Geslaagd|Geïnstalleerd|
|Niet leeg|Niet leeg|Geslaagd|Geïnstalleerd|

##### <a name="non-zero-exit-code"></a>Niet-nul afsluit code

|STDOUT|STDERR|Script resultaat|Detectie status van toepassing|
|---------|---------|---------|---------|
|Leeg|Leeg|Fout|Onbekend|
|Leeg|Niet leeg|Fout|Onbekend|
|Niet leeg|Leeg|Fout|Onbekend|
|Niet leeg|Niet leeg|Fout|Onbekend|

##### <a name="examples"></a>Voorbeelden

Gebruik de volgende Power shell/VBScript-voor beelden om uw eigen toepassings detectie scripts te schrijven:  

**Voor beeld 1**: het script retourneert een afsluit code die niet gelijk is aan nul. Deze code geeft aan dat het script niet kan worden uitgevoerd. In dit geval is de status van de detectie van de toepassing onbekend.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Voor beeld 2**: het script retourneert een afsluit code nul, maar de waarde van stderr is niet leeg. Dit resultaat geeft aan dat het script niet kan worden uitgevoerd. In dit geval is de status van de detectie van de toepassing onbekend.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Voor beeld 3**: het script retourneert een afsluit code nul, wat aangeeft dat het is uitgevoerd. De waarde voor STDOUT is echter leeg, wat aangeeft dat de toepassing niet is geïnstalleerd.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Voor beeld 4**: het script retourneert een afsluit code nul, wat aangeeft dat het is uitgevoerd. De waarde voor STDOUT is niet leeg, wat aangeeft dat de toepassing is geïnstalleerd.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Voor beeld 5**: het script retourneert een afsluit code nul, wat aangeeft dat het is uitgevoerd. De waarden voor STDOUT en STDERR zijn niet leeg, wat aangeeft dat de toepassing is geïnstalleerd.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a>Opties voor **gebruikers ervaring** implementatie type

Met deze instellingen geeft u op hoe de-client de toepassing installeert op apparaten en wat de gebruiker ziet.  

Geef op de pagina **Gebruikerservaring** de volgende informatie:  

- **Installatie gedrag**: Selecteer een van de volgende opties in de vervolg keuzelijst:  

  - **Installeren voor gebruiker**: de-client installeert de toepassing alleen voor de gebruiker voor wie u de toepassing implementeert.  

  - **Installeren voor systeem**: de-client installeert de toepassing slechts één keer. Het is beschikbaar voor alle gebruikers.  

  - **Installeren voor systeem indien de resource een apparaat is; anders installeren voor gebruiker**: als u de toepassing implementeert op een apparaat, installeert de client deze voor alle gebruikers. Als u de toepassing implementeert voor een gebruiker, installeert de client deze alleen voor die gebruiker.  

- **Aanmeldings vereiste**: Selecteer een van de volgende opties:  

  - **Alleen als er een gebruiker is aangemeld**  

  - **Ongeacht of er een gebruiker is aangemeld of niet**  

  - **Alleen als er geen gebruiker is aangemeld**  

    > [!NOTE]  
    > Deze optie wordt alleen standaard ingesteld op **Wanneer een gebruiker is aangemeld**. Als u **installeren voor gebruiker** selecteert in de vervolg keuzelijst **installatie gedrag** , kunt u deze optie niet wijzigen.  

- **Zicht baarheid installatie programma**: Geef de modus op waarin het implementatie type op client apparaten wordt uitgevoerd. Selecteer één van de volgende opties:  

  - **Gemaximaliseerd**: het implementatie type wordt gemaximaliseerd uitgevoerd op client apparaten. Gebruikers zien alle installatie activiteiten.  

  - **Normaal**: het implementatie type wordt in de normale modus uitgevoerd op basis van standaard instellingen van het systeem en Program ma's. Deze modus is de standaardinstelling.  

  - **Geminimaliseerd**: het implementatie type wordt geminimaliseerd uitgevoerd op client apparaten. Gebruikers zien de installatie activiteit mogelijk in het systeemvak of de taak balk.  

  - **Verborgen**: het implementatie type wordt verborgen op client apparaten. Gebruikers zien geen installatie-activiteiten.  

- **Gebruikers toestaan de programma-installatie te bekijken en ermee te werken**: Geef op of een gebruiker kan communiceren met de implementatie type-installatie om de installatie opties in te stellen.  

    Als u de optie **installeren voor gebruiker** hebt geselecteerd in de vervolg keuzelijst **installatie gedrag** , wordt deze optie standaard ingeschakeld.  

    > [!IMPORTANT]  
    > Wanneer u de **installatie voor systeem** gedrag selecteert, is deze instelling optioneel. Deze wijziging is voornamelijk bedoeld om een eind gebruiker in staat te stellen te communiceren met de installatie tijdens een taken reeks. Als u bijvoorbeeld een installatie proces wilt uitvoeren dat de eind gebruiker vraagt om verschillende opties. Voor sommige toepassings installatie Programma's kunnen geen gebruikers prompts worden gestilte of het installatie proces kan specifieke configuratie waarden vereisen die alleen voor de gebruiker bekend zijn. <!--1356976-->  
    >  
    > Installeren in systeem context en toestaan dat gebruikers de installatie kunnen gebruiken, is geen veilige configuratie. Zie [beveiliging en privacy voor toepassings beheer](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact)voor meer informatie.  

- **Maxi maal toegestane uitvoerings tijd (minuten)**: Geef de maximale tijd in minuten op waarvoor het implementatie type op de client computer verwacht. Geef deze instelling op als een geheel getal dat groter is dan nul. De standaard waarde is 120 minuten (twee uur).  

    Gebruik deze waarde voor de volgende acties:  

  - De resultaten van het implementatie type bewaken.  

  - Om te controleren of een implementatie type wordt geïnstalleerd wanneer u onderhouds Vensters op client apparaten definieert. Wanneer er een onderhouds venster aanwezig is, wordt een implementatie type alleen gestart als er voldoende tijd beschikbaar is in het onderhouds venster om de **maximale toegestane uitvoerings tijd** te kunnen instellen.  

    > [!IMPORTANT]  
    > Er kan een conflict optreden als de **maximale toegestane uitvoerings tijd** langer is dan het geplande onderhouds venster. Als de gebruiker de maximale uitvoerings tijd instelt op een periode die groter is dan de lengte van een beschikbaar onderhouds venster, wordt het implementatie type niet uitgevoerd.  

- **Geschatte installatie tijd (minuten)**: Geef de geschatte installatie tijd van het implementatie type op. Gebruikers zien deze tijd in Software Center.  

#### <a name="deployment-type-properties-user-experience-options"></a>Opties voor eigenschappen van implementatie type **gebruikers ervaring**

Wanneer u de eigenschappen van een implementatie type bekijkt, worden de volgende opties alleen weer gegeven op het tabblad **gebruikers ervaring** :

Specifiek gedrag na installatie afdwingen. Selecteer één van de volgende opties:  

- **Gedrag bepalen op basis van retour codes**: afhandelings bewerkingen op basis van de codes die zijn geconfigureerd op het tabblad [retour codes](#bkmk_dt-return) . Software Center geeft **mogelijk een herstart opnieuw**op. Als een gebruiker is aangemeld tijdens de installatie, wordt deze gevraagd, afhankelijk van de configuratie *van* de gebruikers ervaring voor de implementatie.  

- **Geen specifieke actie**: opnieuw opstarten is niet vereist na installatie. Software Center-rapporten die niet opnieuw moeten worden opgestart.  

- **Het software-installatie programma forceert mogelijk een herstart van het apparaat**: Configuration Manager beheert of start geen opnieuw opstarten, maar de daad werkelijke installatie kan zonder waarschuwing worden uitgevoerd. Gebruik deze instelling om te voor komen dat Configuration Manager een melding over de installatie mislukt wanneer het installatie programma de computer opnieuw opstart. Software Center **moet mogelijk opnieuw worden opgestart**.  

- **Configuration Manager client dwingt het opnieuw opstarten van het apparaat**af: Configuration Manager geforceerd opnieuw opstarten nadat de installatie is voltooid. Software Center meldt dat opnieuw opstarten is vereist. Als een gebruiker is aangemeld tijdens de installatie, wordt deze gevraagd, afhankelijk van de configuratie *van* de gebruikers ervaring voor de implementatie.  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a>**Vereisten voor** implementatie type

Configuration Manager controleert deze vereisten op apparaten voordat het implementatie type wordt geïnstalleerd. Gebruik vereisten om de apparaten of gebruikers die deze toepassing ontvangen, verder te verfijnen en te beheren. Als u de toepassing bijvoorbeeld in een gebruikers verzameling implementeert, geeft u hier de hardwarevereisten voor de app op.

1. Selecteer op de pagina **vereisten** de optie **toevoegen** om het dialoog venster **vereiste maken** te openen.  

2. Selecteer in de vervolg keuzelijst **categorie** of deze vereiste geldt voor een **apparaat** of een **gebruiker**.  

    Selecteer **aangepast** als u een eerder gemaakte globale voor waarde wilt gebruiken. Wanneer u **aangepast**selecteert, kunt u ook **maken** kiezen om een nieuwe globale voor waarde te maken. Zie [globale voor waarden maken](create-global-conditions.md)voor meer informatie over globale voor waarden.  

    > [!IMPORTANT]  
    > Als u de toepassing implementeert in een verzameling apparaten, negeert de client een vereiste van de categorie **gebruiker** en het **primaire apparaat**van de voor waarde.  

3. Selecteer in de vervolg keuzelijst **voor waarde** de voor waarde om te beoordelen of de gebruiker of het apparaat voldoet aan de installatie vereisten. De inhoud van deze lijst varieert, afhankelijk van de geselecteerde categorie.  

4. Selecteer in de vervolg keuzelijst **operator** de operator die u wilt gebruiken. Met deze operator wordt de geselecteerde voor waarde vergeleken met de opgegeven waarde. Hiermee wordt beoordeeld of de gebruiker of het apparaat voldoet aan de installatie vereiste. De beschik bare Opera tors variëren afhankelijk van de geselecteerde voor waarde.  

    > [!Note]  
    > De beschik bare vereisten variëren, afhankelijk van het apparaattype dat door het implementatie type wordt gebruikt.  

5. Geef in het vak **waarde** de waarden op die moeten worden gebruikt voor de vergelijking. Deze waarden, samen met de geselecteerde voor waarde en operator, evalueren of de gebruiker of het apparaat voldoet aan de installatie vereisten. De beschik bare waarden variëren, afhankelijk van de geselecteerde voor waarde en de geselecteerde operator.  

6. Kies **OK** om de vereiste op te slaan en het dialoog venster **vereiste maken** te sluiten.  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a>**Afhankelijkheden** implementatie type  

Afhankelijkheden definiëren een of meer implementatie typen van een andere toepassing die de client moet installeren voordat dit implementatie type wordt geïnstalleerd.

> [!IMPORTANT]  
> In sommige gevallen is een implementatie type afhankelijk van een implementatie type dat ook afhankelijkheden heeft. Het maximum aantal ondersteunde afhankelijkheden in de keten is vijf.  

1. Selecteer op de pagina **afhankelijkheden** de optie **toevoegen**.  

2. Voer de naam van de **afhankelijkheids groep**in het venster afhankelijkheid toevoegen in. Deze naam verwijst naar deze groep toepassings afhankelijkheden.  

3. Selecteer in het venster afhankelijkheid toevoegen de optie **toevoegen**.  

4. Selecteer in het venster **vereiste toepassing opgeven** een beschik bare toepassing en ten minste één van de implementatie typen die u als afhankelijkheid wilt gebruiken.  

    > [!TIP]  
    > Selecteer **weer gave** om de eigenschappen van de geselecteerde toepassing of dit implementatie type weer te geven.  

5. Selecteer **OK** om het venster **Geef de vereiste toepassing** op te sluiten.  

6. Als u wilt dat de client de afhankelijke toepassing automatisch installeert, selecteert u **automatisch installeren** naast de afhankelijkheid.  

    > [!NOTE]  
    > U hoeft geen afhankelijke toepassing voor de client te implementeren om deze automatisch te installeren.  

7. Als u meer dan één afhankelijkheid toevoegt, gebruikt u de knoppen **prioriteit verhogen** en **prioriteit verlagen** . Met deze acties wijzigt u de volg orde waarin de client elke afhankelijkheid evalueert.  

8. Selecteer **OK** om het venster **afhankelijkheid toevoegen** te sluiten.  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a>**Retour codes** implementatie type

> [!Note]  
> Deze pagina bevindt zich niet in de wizard implementatie type maken. Het is slechts een tabblad op de eigenschappen van een bestaand implementatie type.  

Geef retour codes op voor het beheren van gedrag nadat het implementatie type is voltooid. Bijvoorbeeld, signaal dat het opnieuw opstarten is vereist, de installatie is voltooid.

1. Selecteer **toevoegen**op het tabblad **retour codes** van het venster Eigenschappen van implementatie type.  

2. Geef in het venster retour code toevoegen de **retour code waarde** op die u verwacht van dit implementatie type. Deze waarde is een positief of negatief geheel getal `-2147483648` tussen `2147483647`en.  

3. Selecteer een **code type** in de vervolg keuzelijst. Met deze instelling definieert u hoe Configuration Manager de opgegeven retour code van dit implementatie type interpreteert. De beschik bare typen variëren op basis van de technologie van het implementatie type.  

    - **Geslaagd (niet opnieuw opgestart)**: het implementatie type is geïnstalleerd en het systeem hoeft niet opnieuw te worden opgestart.  

    - **Mislukt (niet opnieuw opstarten)**: het implementatie type is niet geïnstalleerd.  

    - **Hard opstarten**: het implementatie type is geïnstalleerd, maar vereist dat het apparaat opnieuw wordt opgestart. Niets anders kan worden geïnstalleerd totdat het apparaat opnieuw wordt opgestart.  

    - **Zacht opnieuw opstarten**: het implementatie type is geïnstalleerd, maar vraagt het apparaat opnieuw op te starten. Andere installaties kunnen zich voordoen voordat het apparaat opnieuw wordt opgestart.  

    - **Snel opnieuw proberen**: er wordt al een andere installatie uitgevoerd op het apparaat. De client probeert om de twee uur, voor een totaal van tien keer.  

4. Voer eventueel een **naam** en **Beschrijving** in voor deze retour code.

5. Selecteer **OK** om het venster retour code toevoegen te sluiten.  

#### <a name="example-non-zero-success"></a>Voor beeld: niet-nul geslaagd

U implementeert een toepassing die een afsluit code retourneert van `1` het moment waarop de installatie wordt uitgevoerd. Configuration Manager detecteert deze niet-nul retour code standaard als fout. Geef de retour code waarde van `1`op en selecteer het code type **geslaagd (niet opnieuw opstarten)**. Nu Configuration Manager interpreteert dat de retour code als een succes is voor dit implementatie type.

#### <a name="default-return-codes"></a>Standaard retour codes

Wanneer u een aantal implementatie typen maakt, voegt Configuration Manager automatisch de volgende retour codes toe die gemeen schappelijk zijn voor die technologie:  

##### <a name="windows-installer-msi-file"></a>Windows Installer (\*MSI-bestand)

|Waarde    |Code type|
|---------|---------|
|0        |Geslaagd (niet opnieuw opgestart)|
|1707     |Geslaagd (niet opnieuw opgestart)|
|3010     |Zacht opnieuw opstarten|
|1641     |Hard opstarten|
|1618     |Snel opnieuw proberen|

##### <a name="script-installer"></a>Script Installer

|Waarde    |Code type|
|---------|---------|
|0        |Geslaagd (niet opnieuw opgestart)|
|1641     |Hard opstarten|
|3010     |Zacht opnieuw opstarten|
|1618     |Snel opnieuw proberen|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Windows-app-\*pakket (. \*appx,. \*appxbundle,. \*msix,. msixbundle)

|Waarde    |Code type|
|---------|---------|
|15605    |Snel opnieuw proberen|
|15618    |Snel opnieuw proberen|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a>Aanvullende opties voor app-V-implementatie typen  

Configureer aanvullende opties die uniek zijn voor implementatie typen voor virtuele toepassingen (app-V).  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a>**Inhouds** opties voor het implementatie type app-V  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .  

2. Selecteer een toepassing met een app-V-implementatie type en selecteer **Eigenschappen**.  

3. Ga in de eigenschappen van de toepassing naar het tabblad **implementatie typen** , selecteer het implementatie type app-V en selecteer **bewerken**.  

4. In de eigenschappen van het implementatie type gaat u naar het tabblad **inhoud** . Configureer zo nodig de volgende opties:  

    - **Inhoud in de client cache behouden**: de Configuration Manager-client verwijdert de inhoud voor dit implementatie type niet uit de cache.  

    - **Inhoud vóór starten laden in App-v-cache**: voordat de toepassing wordt gestart, laadt de Configuration Manager-client in de App-v-cache alle inhoud voor dit implementatie type. De-client maakt geen pincode voor de inhoud in de cache. De inhoud wordt verwijderd als dat nodig is.  

5. Selecteer **OK** om de implementatie type-eigenschappen te sluiten. Selecteer **OK** om de toepassings eigenschappen te sluiten.  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a>**Publicatie** opties voor het implementatie type app-V

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .  

2. Selecteer een toepassing met een app-V-implementatie type en selecteer **Eigenschappen**.  

3. Ga in de eigenschappen van de toepassing naar het tabblad **implementatie typen** , selecteer het implementatie type app-V en selecteer **bewerken**.  

4. Ga in de eigenschappen van het implementatie type naar het tabblad **publiceren** . Selecteer de items in de virtuele toepassing die u wilt publiceren.  

5. Selecteer **OK** om de implementatie type-eigenschappen te sluiten. Selecteer **OK** om de toepassings eigenschappen te sluiten.  

## <a name="import-an-application"></a><a name="bkmk_import"></a>Een toepassing importeren  

Gebruik de volgende procedure om een toepassing in Configuration Manager te importeren:

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .  

2. Selecteer in het lint op het tabblad **Start** en de groep **maken** de optie **toepassing importeren**.  

3. Geef op de pagina **Algemeen** van de wizard toepassing importeren het netwerkpad op naar het **bestand** dat u wilt importeren. Bijvoorbeeld `\\server\share\file.zip`. Dit bestand is een geldig gecomprimeerd archief (ZIP-indeling) van een geëxporteerde Configuration Manager-toepassing.  

4. Selecteer op de pagina **Bestands inhoud** de actie die moet worden uitgevoerd als deze toepassing een duplicaat is van een bestaande toepassing. Een nieuwe toepassing maken of het duplicaat negeren en een nieuwe revisie toevoegen aan de bestaande toepassing.  

5. Controleer de acties op de pagina **samen vatting** en voltooi vervolgens de wizard.  

De nieuwe toepassing wordt weergegeven in het knooppunt **Toepassingen**.  

> [!TIP]  
> De Windows Power shell **-cmdlet Import-CMApplication** heeft dezelfde functie als deze procedure. Zie [import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps)voor meer informatie.  

Zie [management tasks for Applications](management-tasks-applications.md)(Engelstalig) voor meer informatie over het exporteren van een toepassing.

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a>Ondersteunde implementatie typen  

Configuration Manager ondersteunt de volgende implementatie typen voor toepassingen:

| Naam van implementatietype | Beschrijving |
|--------------------------|----------------------|  
| **Windows Installer (\*MSI-bestand)** | Een Windows Installer-bestand. |  
| **Windows-app-\*pakket (. \*appx,. \*appxbundle,. \*msix,. msixbundle)** | Een Windows-app-pakket bestand (. appx), een Windows-app-bundel pakket (. appxbundle), een Windows 10-app-pakket (. msix) of Windows 10 app-bundel (. msixbundle).<!--1357427--> |  
| **Windows-app-pakket (in de Windows Store)** | Geef een koppeling op naar de app in de Windows Store of blader door de Store om de app te selecteren.<sup>[Opmerking 1](#bkmk_note1)</sup> |  
| **Script Installer** | Geef een script of programma op dat wordt uitgevoerd op Windows-clients om inhoud te installeren of om een actie uit te voeren. Gebruik dit implementatie type voor Setup. exe-installatie Programma's of script wrappers. |  
| **Microsoft Application Virtualization 4** | Een micro soft app-V v4-manifest. |  
| **Microsoft Application Virtualization 5** | Een micro soft app-V V5-pakket bestand. |  
| **Windows Phone-app-\*pakket (XAP-bestand)** | Een Windows Phone-app-pakket bestand. |  
| **Windows Phone-app-pakket (in de Windows Phone Store)** | Geef een koppeling op naar de app in de Windows Store. |  
| **Mac OS X** | Voor macOS-computers waarop de Configuration Manager-client wordt uitgevoerd. Maak een. cmmac-bestand met het **CMAppUtil** -hulp programma. |  
| **Webtoepassing** | Geef een koppeling op naar een webtoepassing. Met dit implementatie type wordt een snelkoppeling naar de webtoepassing op het apparaat van de gebruiker geïnstalleerd. |  
| **Windows Installer via MDM (\*. msi)** | Op Windows Installer gebaseerde apps maken en implementeren op Windows 10-apparaten. Zie [Windows Installer-apps implementeren op MDM-geregistreerde Windows 10-apparaten](../get-started/creating-windows-applications.md#bkmk_mdm-msi)voor meer informatie. |
| **Takenreeks** | Met ingang van versie 2002 kunt u complexe toepassingen installeren of verwijderen met taken reeksen. Zie [implementatie type voor taken reeksen](../get-started/creating-windows-applications.md#bkmk_tsdt)voor meer informatie. <!--3555953--> |

> [!NOTE]
> De Configuration Manager-console kan andere implementatie typen weer geven, maar ze zijn voor platforms die niet meer worden ondersteund. Zie [Wat is er gebeurd met hybride?](../../mdm/understand/what-happened-to-hybrid.md)voor meer informatie.

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a>Opmerking 1: Windows-app-pakket (in de Windows Store)

Als u de app als een koppeling naar de Windows Store wilt implementeren, configureert u het groeps beleid **de toepassing Store uit te scha kelen**. Stel dit beleid in op **uitgeschakeld** of **niet geconfigureerd**. Als u deze instelling inschakelt, kunnen clients geen verbinding maken met de Windows Store om toepassingen te downloaden en te installeren.

Windows-clients evalueren altijd implementatie typen die een koppeling naar een archief gebruiken vóór andere implementatie typen. Vervolgens evalueert de client implementatie typen op prioriteit.

> [!TIP]
> Sommige archief koppelingen kunnen de volgende fout veroorzaken in de wizard toepassing maken: ' ongeldige toepassings koppeling '. Sommige *apps* in Store kunnen bijvoorbeeld deze fout veroorzaken. U kunt nog steeds de **volgende** selecteren op de pagina **Algemeen** van de wizard. Configuration Manager de app hebt gemaakt, kunt u deze implementeren.<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>Volgende stappen

Nadat u een toepassing hebt gemaakt in Configuration Manager, is de volgende stap het [implementeren van de toepassing](deploy-applications.md).

Met ingang van versie 1906 maakt u een groep toepassingen die u kunt verzenden naar een gebruiker of een apparaat-verzameling als één implementatie. Zie [toepassings groepen maken](create-app-groups.md)voor meer informatie.

Raadpleeg de volgende artikelen voor meer informatie over het maken van toepassingen op verschillende besturingssysteem platforms:  

- [Windows-toepassingen maken](../get-started/creating-windows-applications.md)
- [Mac-toepassingen maken](../get-started/creating-mac-computer-applications.md)
- [Linux- en UNIX-servertoepassingen maken](../get-started/creating-linux-and-unix-server-applications.md)
- [Windows Embedded-toepassingen maken](../get-started/creating-windows-embedded-applications.md)
