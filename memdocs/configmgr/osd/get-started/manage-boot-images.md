---
title: Opstartinstallatiekopieën beheren
titleSuffix: Configuration Manager
description: In Configuration Manager leert u hoe u de Windows PE-opstart installatie kopieën kunt beheren die u tijdens de implementatie van een besturings systeem gebruikt.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 74b8b0f29172140a19c402c79b7ea9b7339cf3e5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697633"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Opstart installatie kopieën beheren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Een opstart installatie kopie in Configuration Manager is een [Windows PE](/windows-hardware/manufacture/desktop/winpe-intro) -installatie kopie (WinPE) die wordt gebruikt tijdens de implementatie van een besturings systeem. Opstart installatie kopieën worden gebruikt om een computer te starten in WinPE. Dit minimale besturings systeem bevat beperkte onderdelen en services. Configuration Manager gebruikt WinPE om de doel computer voor te bereiden voor de installatie van Windows.

## <a name="default-boot-images"></a><a name="BKMK_BootImageDefault"></a> Standaard installatie kopieën

Configuration Manager biedt twee standaard opstart installatie kopieën: één ter ondersteuning van x86-platformen en één ter ondersteuning van x64-platformen. Deze installatie kopieën worden opgeslagen in de *x64* -of *i386* -mappen in de volgende share op de site server: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\` . De standaard installatie kopieën worden bijgewerkt of opnieuw gegenereerd, afhankelijk van de actie die u uitvoert.

Houd rekening met het volgende gedrag voor elk van de acties die worden beschreven voor standaard installatie kopieën:

- De bron stuur programma-objecten moeten geldig zijn. Deze objecten bevatten de bron bestanden van het stuur programma. Als de objecten niet geldig zijn, voegt de-site de Stuur Programma's niet toe aan de installatie kopieën.  

- Opstart installatie kopieën die niet zijn gebaseerd op de standaard installatie kopieën, zelfs als ze dezelfde Windows PE-versie gebruiken, worden niet gewijzigd.  

- De aangepaste opstart installatie kopieën opnieuw distribueren naar distributie punten.  

- Maak opnieuw een medium dat gebruikmaakt van de gewijzigde installatie kopieën.  

- Als u niet wilt dat uw aangepaste/standaard installatie kopieën automatisch worden bijgewerkt, slaat u ze niet op in de standaard locatie.  

> [!NOTE]
> Het hulp programma Configuration Manager logboek (**CMTrace**) wordt toegevoegd aan alle opstart installatie kopieën in de **software bibliotheek**. Wanneer u Windows PE gebruikt, start u het hulp programma door te typen `cmtrace` vanaf de opdracht prompt.
>
> CMTrace is de standaard viewer voor logboek bestanden in Windows PE.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Updates en onderhoud gebruiken om de meest recente versie van Configuration Manager te installeren

Wanneer u de versie van de Windows Assessment and Deployment Kit (ADK) bijwerkt en vervolgens updates en onderhoud gebruikt om de meest recente versie van Configuration Manager te installeren, genereert de site de standaard installatie kopieën opnieuw. Deze update bevat de nieuwe versie van WinPE van de bijgewerkte Windows ADK, de nieuwe versie van de Configuration Manager-client, stuur Programma's en aanpassingen. De site wijzigt geen aangepaste opstart installatie kopieën.

### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Upgrade van Configuration Manager 2012 naar current branch

Wanneer u Configuration Manager 2012 bijwerkt naar de huidige vertakking, genereert de site de standaard installatie kopieën opnieuw. Deze update bevat de nieuwe versie van WinPE van de bijgewerkte Windows ADK en de nieuwe versie van de Configuration Manager-client. Alle aanpassingen van de opstart installatie kopie blijven ongewijzigd. De site wijzigt geen aangepaste opstart installatie kopieën.

### <a name="update-distribution-points-with-the-boot-image"></a>Distributie punten bijwerken met de installatie kopie

Wanneer u de actie **distributie punten bijwerken** gebruikt vanuit het knoop punt **opstart installatie kopieën** in de-console, werkt de site de opstart installatie kopie van het doel bij met de client onderdelen, stuur Programma's en aanpassingen.

U kunt de opstart installatie kopie opnieuw laden met de meest recente versie van WinPE vanuit de installatiemap van Windows ADK. De pagina **Algemeen** van de wizard distributie punten bijwerken bevat de volgende informatie:

- De huidige Windows ADK-versie die is geïnstalleerd op de site server
- De huidige productie client versie
- De Windows ADK-versie van WinPE in de opstart installatie kopie
- De versie van de Configuration Manager-client in de opstart installatie kopie

Als de versies in de opstart installatie kopie verouderd zijn, gebruikt u de optie om **deze opstart installatie kopie opnieuw te laden met de huidige Windows PE-versie van de Windows ADk**.

> [!Important]  
> Deze actie is beschikbaar voor standaard-en aangepaste opstart installatie kopieën. Tijdens dit proces voor het opnieuw laden van de opstart installatie kopie, behoudt de site geen hand matige aanpassingen die buiten Configuration Manager zijn aangebracht. Deze aanpassingen zijn onder andere uitbrei dingen van derden. Met deze optie wordt de opstart installatie kopie opnieuw opgebouwd met de nieuwste versie van WinPE en de meest recente client versie. Alleen de configuraties die u opgeeft in de eigenschappen van de opstart installatie kopie worden opnieuw toegepast. <!--SCCMDocs issue #1283-->

Het knoop punt **opstart installatie kopieën** bevat ook een nieuwe kolom voor (**client versie**). Gebruik deze kolom om snel de versie van de Configuration Manager-client in elke opstart installatie kopie weer te geven.

## <a name="customize-a-boot-image"></a><a name="BKMK_BootImageCustom"></a> Een opstart installatie kopie aanpassen  

Wanneer een opstart installatie kopie is gebaseerd op de WinPE-versie van de ondersteunde versie van Windows ADK, kunt u [een opstart installatie kopie](#BKMK_ModifyBootImages) aanpassen of aanpassen via de-console. Wanneer u een site bijwerkt en een nieuwe versie van Windows ADK installeert, worden aangepaste opstart installatie kopieën niet bijgewerkt met de nieuwe versie van Windows ADK. Als dat gebeurt, kunt u de opstart installatie kopieën niet aanpassen in de Configuration Manager-console. Ze blijven echter werken zoals voor de upgrade.  

Wanneer een opstart installatie kopie is gebaseerd op een andere versie van Windows ADK die op een site is geïnstalleerd, moet u de opstart installatie kopieën aanpassen. Gebruik een andere methode voor het aanpassen van deze opstart installatie kopieën, zoals het gebruik van het opdracht regel programma Deployment Image Servicing and Management (DISM). DISM maakt deel uit van de Windows ADK. Zie [opstart installatie kopieën aanpassen](customize-boot-images.md)voor meer informatie.  

## <a name="add-a-boot-image"></a><a name="BKMK_AddBootImages"></a> Een opstart installatie kopie toevoegen  

Tijdens de installatie van de site voegt Configuration Manager automatisch opstart installatie kopieën toe die zijn gebaseerd op een WinPE-versie van de ondersteunde versie van Windows ADK. Afhankelijk van de versie van Configuration Manager, kunt u opstart installatie kopieën toevoegen op basis van een andere WinPE-versie dan de ondersteunde versie van de Windows ADK. Er treedt een fout op wanneer u een opstart installatie kopie probeert toe te voegen die een niet-ondersteunde versie van WinPE bevat. De volgende lijst bevat de momenteel ondersteunde Windows ADK-en WinPE-versies:

- Windows ADK-versie: Windows ADK voor Windows 10

- Windows PE-versies voor installatie kopieën die aanpasbaar zijn via de Configuration Manager-console: Windows PE 10

- Ondersteunde Windows PE-versies voor installatie kopieën die *niet aanpasbaar* zijn via de Configuration Manager-console

  - Windows PE 3,1<sup>[Opmerking 1](#bkmk_note1)</sup>

  - Windows PE 5

Gebruik bijvoorbeeld de Configuration Manager-console om opstart installatie kopieën op basis van Windows PE 10 van Windows ADK voor Windows 10 aan te passen. Voor een opstart installatie kopie die is gebaseerd op Windows PE 5, past u deze aan op een andere computer met behulp van de versie van DISM van Windows ADK voor Windows 8. Voeg vervolgens de aangepaste opstart installatie kopie toe aan de Configuration Manager-console. Raadpleeg voor meer informatie de volgende artikelen:

- [Opstartinstallatiekopieën aanpassen](customize-boot-images.md)
- [Ondersteuning voor Windows 10 ADK](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk)
- [Door DISM ondersteunde platforms](/windows-hardware/manufacture/desktop/dism-supported-platforms)

<a name="bkmk_note1"></a>

> [!NOTE]
> **Opmerking 1: ondersteuning voor Windows PE 3,1**
>
> Voeg alleen een installatie kopie toe aan Configuration Manager op basis van Windows PE *versie 3,1*. Voer een upgrade uit voor Windows AIK voor Windows 7 (gebaseerd op Windows PE 3,0) met Windows AIK supplement voor Windows 7 SP1 (gebaseerd op Windows PE 3,1). Down load Windows AIK supplement voor Windows 7 SP1 via het [micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=5188).  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **opstart installatie kopieën** .  

2. Klik op het tabblad **Start** van het lint in de groep **maken** op installatie **kopie toevoegen**. Met deze actie wordt de wizard opstart installatie kopie toevoegen gestart.  

3. Geef op de pagina **gegevens bron** de volgende opties op:  

    - Geef in het vakje **Pad** het pad op naar het WIM-bestand van de opstartinstallatiekopie. Het opgegeven pad moet een geldig netwerkpad zijn in UNC-indeling. Bijvoorbeeld: `\\ServerName\ShareName\BootImageName.wim`

    - Selecteer de installatiekopie in de vervolgkeuzelijst **Installatiekopie**. Als het WIM-bestand meerdere opstart installatie kopieën bevat, selecteert u de juiste installatie kopie.  

4. Geef op de pagina **Algemeen** de volgende opties op:  

    - Geef in het venster **Naam** een unieke naam op voor de installatiekopie.  

    - Geef in het venster **Versie** een uniek versienummer op voor de installatiekopie.  

    - Geef in het vak **Opmerking** een korte beschrijving op van de manier waarop u de opstart installatie kopie gebruikt.  

5. Voltooi de wizard.  

De opstart installatie kopie wordt nu weer gegeven in het knoop punt **opstart installatie kopie** . Voordat u de opstart installatie kopie gebruikt om een besturings systeem te implementeren, distribueert u de opstart installatie kopie naar distributie punten.

> [!Tip]  
> In het knoop punt **opstart installatie kopie** van de-console wordt in de kolom **grootte (KB)** de gedecomprimeerde grootte voor elke opstart installatie kopie weer gegeven. Wanneer de site een opstart installatie kopie via het netwerk verzendt, wordt een gecomprimeerde kopie verzonden. Deze kopie is doorgaans kleiner dan de grootte die wordt weer gegeven in de kolom **grootte (KB)** .  

## <a name="distribute-boot-images"></a><a name="BKMK_DistributeBootImages"></a> Opstart installatie kopieën distribueren  

Opstartinstallatiekopieën worden op dezelfde manier naar distributiepunten gedistribueerd als bij het distribueren van andere inhoud. Voordat u een besturings systeem implementeert of media maakt, distribueert u de opstart installatie kopie naar ten minste één distributie punt.

Zie voor meer informatie over het distribueren van een opstart installatie kopie [inhoud distribueren](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

Als u PXE wilt gebruiken om een besturings systeem te implementeren, moet u rekening houden met de volgende punten voordat u de opstart installatie kopie distribueert:  

- Configureer het distributie punt om PXE-aanvragen te accepteren.  
- Distribueer zowel een x86-als een x64-opstart installatie kopie met PXE-functionaliteit naar ten minste één distributie punt met PXE-functionaliteit.  
- Configuration Manager distribueert de opstart installatie kopieën naar de map **map RemoteInstall** op het distributie punt met PXE-functionaliteit.  
  
Zie [PXE gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie over het gebruik van PXE voor het implementeren van besturings systemen.  

## <a name="modify-a-boot-image"></a><a name="BKMK_ModifyBootImages"></a> Een opstart installatie kopie wijzigen  

Stuur Programma's aan de installatie kopie toevoegen of eruit verwijderen of bewerk de eigenschappen van de opstart installatie kopie. De Stuur Programma's die u toevoegt of verwijdert, kunnen netwerk-of opslag Stuur Programma's zijn. Houd rekening met de volgende factoren wanneer u opstartinstallatiekopieën wijzigt:  

- Voordat u stuur Programma's toevoegt aan de opstart installatie kopie, moet u deze importeren en inschakelen in de catalogus van het apparaatstuurprogramma.  

- Wanneer u een opstart installatie kopie wijzigt, wijzigt de opstart installatie kopie geen van de gekoppelde pakketten waarnaar de opstart installatie kopie verwijst.  

- Nadat u wijzigingen in een installatie kopie hebt aangebracht, **werkt** u de opstart installatie kopie bij op de distributie punten die het al hebben. Dit proces zorgt ervoor dat de meest recente versie van de opstart installatie kopie beschikbaar is voor clients. Zie [inhoud beheren die u hebt gedistribueerd](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage)voor meer informatie.  

### <a name="modify-the-properties-of-a-boot-image"></a>De eigenschappen van een opstart installatie kopie wijzigen  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **opstart installatie kopieën** .  

2. Selecteer de opstartinstallatiekopie die u wilt wijzigen.  

3. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.  

4. Stel één van de volgende instellingen in om het gedrag van de opstartinstallatiekopie te wijzigen:  

#### <a name="images"></a>Installatiekopieën

Selecteer **opnieuw laden**op het tabblad **installatie kopieën** als u de eigenschappen van de opstart installatie kopie wijzigt met behulp van een extern hulp programma.  

#### <a name="drivers"></a>Stuurprogramma's

Voeg op het tabblad **Stuur Programma's** de Windows-apparaatstuurprogramma's toe die door WinPE moeten worden opgestart. Houd rekening met de volgende punten wanneer u apparaatstuurprogramma's toevoegt:  

- Zorg ervoor dat de Stuur Programma's die u toevoegt aan de opstart installatie kopie overeenkomen met de architectuur van de opstart installatie kopie.  

- Als u alleen stuur Programma's voor de architectuur van de opstart installatie kopie wilt weer geven, selecteert u **Stuur Programma's verbergen die niet overeenkomen met de architectuur van de opstart installatie kopie**. De architectuur van het stuur programma is gebaseerd op de architectuur die wordt vermeld in het INF-rapport van de fabrikant.  

- WinPE is al voorzien van een groot aantal ingebouwde Stuur Programma's. Voeg alleen netwerk-en opslag Stuur Programma's toe die geen deel uitmaken van WinPE.  

- Voeg alleen netwerk-en opslag Stuur Programma's toe aan de opstart installatie kopie, tenzij er vereisten gelden voor andere Stuur Programma's in WinPE.  

- Als u alleen opslag-en netwerk Stuur Programma's wilt weer geven, selecteert u **Stuur Programma's verbergen die zich niet in een opslag-of netwerk klasse (voor installatie kopieën) bevinden**. Met deze optie verbergt u ook andere Stuur Programma's die doorgaans niet nodig zijn voor installatie kopieën, zoals video-of modem Stuur Programma's.  

- Als u stuur Programma's wilt verbergen die geen geldige digitale hand tekening hebben, selecteert u **Stuur Programma's die niet digitaal zijn ondertekend verbergen**.  

> [!NOTE]  
> Importeer apparaatstuurprogramma's in de catalogus met stuur Programma's voordat u ze aan een installatie kopie toevoegt. Zie [Stuur Programma's beheren](manage-drivers.md)voor meer informatie over het importeren van apparaatstuurprogramma's.  

#### <a name="customization"></a>Aanpassing

Selecteer op het tabblad **Aanpassen** één van de volgende instellingen:  

- Selecteer de optie voor het **inschakelen van prestart-opdrachten** om een opdracht op te geven die moet worden uitgevoerd voordat de taken reeks wordt uitgevoerd. Wanneer u deze optie inschakelt, geeft u ook de opdracht regel op die moet worden uitgevoerd en de ondersteunings bestanden die vereist zijn voor de opdracht.  

    > [!WARNING]  
    > Toevoegen `cmd /c` aan het begin van de opdracht regel. Als u niet opgeeft `cmd /c` , wordt de opdracht niet afgesloten nadat deze is uitgevoerd. De implementatie blijft wachten tot de opdracht is voltooid en er worden geen andere geconfigureerde opdrachten of acties gestart.  

    > [!TIP]  
    > Tijdens het maken van de taken reeks media schrijft de wizard de pakket-ID en prestart-opdracht regel naar het bestand **CreateTSMedia. log** . Deze informatie bevat de waarde voor alle taken reeks variabelen. Dit logboek bevindt zich op de computer waarop de Configuration Manager-console wordt uitgevoerd. Bekijk dit logboek bestand om de waarden voor de taken reeks variabelen te controleren.  

- Stel bij **Windows PE-achtergrond** in of u de standaardachtergrond van WindowsPE of een aangepaste achtergrond wilt gebruiken.  

- Configureer de **Windows PE-Scratch ruimte (MB)**, de tijdelijke opslag (RAM-station) die wordt gebruikt door WinPE. Wanneer er bijvoorbeeld een toepassing wordt uitgevoerd in WinPE en er tijdelijke bestanden moet worden geschreven, stuurt WindPE de bestanden naar de scratchruimte in het geheugen om de aanwezigheid van een harde schijf te simuleren. Dit aantal is standaard 512 MB voor apparaten met meer dan 1 GB RAM-geheugen, anders is de standaard waarde 32 MB.  

- Schakel het selectievakje **Opdrachtondersteuning inschakelen (alleen testen)** in om tijdens het implementeren van de opstartinstallatiekopie een opdrachtprompt met toets **F8** te openen. Deze optie is handig voor het oplossen van problemen tijdens het testen van uw implementatie. Het gebruik van deze instelling in een productie-implementatie wordt niet aanbevolen vanwege beveiligings problemen.  

- **Standaard toetsenbord indeling instellen in WinPE**: <!--4910348-->Configureer vanaf versie 1910 de standaardtoetsen bord indeling voor een opstart installatie kopie. Als u een andere taal dan en-US selecteert, bevat Configuration Manager nog steeds en-us in de beschik bare land instellingen voor invoer. Op het apparaat is de oorspronkelijke toetsenbord indeling de geselecteerde land instelling, maar de gebruiker kan het apparaat overschakelen naar en-US als dat nodig is.

> [!Tip]
> Gebruik de Power shell [-cmdlet Set-CMBootImage](/powershell/module/configurationmanager/set-cmbootimage?view=sccm-ps) om deze instellingen te configureren van een script.

#### <a name="optional-components"></a>Optionele onderdelen

Geef op het tabblad **optionele onderdelen** de onderdelen op die zijn toegevoegd aan Windows PE voor gebruik met Configuration Manager. Zie [Een Windows PE-installatiekopie bouwen met optionele onderdelen](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference) voor meer informatie over beschikbare optionele onderdelen.  

De volgende onderdelen zijn vereist voor Configuration Manager en worden altijd toegevoegd aan installatie kopieën:

- Scripting (WinPE-scripting)
- Opstarten (WinPE-SecureStartup)
- Netwerk (WinPE-WDS-Hulpprogram Ma's)
- Scripting (WinPE-WMI)

De lijst **onderdelen** bevat extra items die worden toegevoegd aan deze opstart installatie kopie. Als u meer onderdelen wilt toevoegen, selecteert u het gouden sterretje. Als u een onderdeel wilt verwijderen, selecteert u dit in de lijst en selecteert u vervolgens de rode X.

De volgende onderdelen worden vaak gebruikt door klanten:

- Microsoft .NET (WinPE-NetFX): dit onderdeel is een vereiste voor Power shell. Het is een van de grotere optionele onderdelen.  
- Windows Power shell (WinPE-Power shell): voor dit onderdeel is .NET vereist en wordt beperkte ondersteuning voor Power shell toegevoegd. Als u aangepaste Power shell-scripts uitvoert tijdens de WinPE-fase van uw taken reeks, voegt u dit onderdeel toe. Er zijn andere onderdelen die mogelijk vereist zijn voor andere Power shell-cmdlets.
- HTML (WinPE-HTA): als u aangepaste HTML-toepassingen uitvoert tijdens de WinPE-fase van uw taken reeks, voegt u dit onderdeel toe.

Zie [meerdere talen configureren](#BKMK_BootImageLanguage)voor meer informatie over het toevoegen van talen.

#### <a name="data-source"></a>Gegevensbron

Update één van de volgende instellingen op het tabblad **Gegevensbron**:  

- Als u het bron bestand van de opstart installatie kopie wilt wijzigen, stelt u het **pad naar de afbeelding** en de **installatie kopie-index**in.  

- Als u een planning wilt maken voor wanneer de installatie kopie van de site wordt bijgewerkt, selecteert u **distributie punten bijwerken volgens een schema**.  

- Als u niet wilt dat de inhoud van dit pakket uit de client cache wordt geleeftijd om ruimte te maken voor andere inhoud, selecteert u **inhoud in client cache behouden**.  

- Als u wilt opgeven dat de site alleen gewijzigde bestanden distribueert wanneer het opstart installatie kopie pakket wordt bijgewerkt op het distributie punt, selecteert u **binary Differential Replication inschakelen** (BDR). Deze instelling minimaliseert het netwerk verkeer tussen sites. BDR is vooral nuttig wanneer het pakket met de opstart installatie kopie groot is en de wijzigingen relatief klein zijn.  

- Als u de opstart installatie kopie in een implementatie met PXE-functionaliteit gebruikt, selecteert u de optie **deze opstart installatie kopie implementeren vanaf het distributie punt met PXE-functionaliteit**. Zie [PXE gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie.  

#### <a name="data-access"></a>Gegevens toegang

Op het tabblad **gegevens toegang** kunt u instellingen voor de pakket share configureren. Stel, indien nodig in uw omgeving, de optie in om **de inhoud in dit pakket te kopiëren naar een pakket share op distributie punten**. U hebt vervolgens de extra optie om **een aangepaste naam te gebruiken voor de pakket share** en de aangepaste **share naam**op te geven. Wanneer u deze optie inschakelt, is er extra schijf ruimte vereist op distributie punten. Dit is van toepassing op alle distributie punten die deze opstart installatie kopie ontvangen.

#### <a name="distribution-settings"></a>Distributie-instellingen

Selecteer één van de volgende instellingen op het tabblad **Distributie-instellingen**:  

- Geef in de lijst **distributie prioriteit** het prioriteits niveau op. Configuration Manager gebruikt deze lijst met prioriteiten wanneer de site meerdere pakketten distribueert naar hetzelfde distributie punt.  

- Als u inhouds distributie op aanvraag naar voorkeurs distributiepunten wilt inschakelen, selecteert u **inschakelen voor distributie op aanvraag**. Wanneer u deze instelling inschakelt en een client de inhoud voor het pakket opvraagt en de inhoud niet beschikbaar is op een distributie punt, distribueert het beheer punt de inhoud. Zie [inhoud distribueren op aanvraag](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution)voor meer informatie.  

- Als u wilt opgeven hoe de installatie kopie van de site moet worden gedistribueerd naar distributie punten die zijn ingeschakeld voor voor bereide inhoud, stelt u de **instellingen voor bereid distributie punt**in. Zie [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) (Voorbereide inhoud) voor meer informatie over voorbereide inhoud.  

#### <a name="content-locations"></a>Inhouds locaties

Selecteer op het tabblad **inhouds locaties** het distributie punt of distributiepunt groep en gebruik de volgende acties:  

- **Valideren**: Controleer de integriteit van het opstart installatie kopie pakket op het geselecteerde distributie punt of distributiepunt groep.  

- Opnieuw **distribueren**: Distribueer de opstart installatie kopie opnieuw naar het geselecteerde distributie punt of distributiepunt groep.  

- **Verwijderen**: de opstart installatie kopie van het geselecteerde distributie punt of distributiepunt groep verwijderen.  

#### <a name="security"></a>Beveiliging

Bekijk op het tabblad **beveiliging** de gebruikers met beheerders rechten die machtigingen hebben voor dit object.

## <a name="configure-a-boot-image-for-pxe"></a><a name="BKMK_BootImagePXE"></a> Een opstart installatie kopie configureren voor PXE  

Voordat u een opstart installatie kopie kunt gebruiken voor een implementatie op basis van PXE, moet u de opstart installatie kopie configureren voor implementatie vanaf een distributie punt met PXE-functionaliteit.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **opstart installatie kopieën** .  

2. Selecteer de opstartinstallatiekopie die u wilt wijzigen.  

3. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.  

4. Selecteer op het tabblad **Gegevensbron** de optie **Deze opstartinstallatiekopie implementeren vanaf het PXE-distributiepunt**. Zie [PXE gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie.  

## <a name="configure-multiple-languages"></a><a name="BKMK_BootImageLanguage"></a> Meerdere talen configureren

> [!TIP]
> Vanaf versie 1910 configureert u de standaardtoetsen bord-indeling voor de eigenschappen van een opstart installatie kopie. Zie [aanpassing](#customization)voor meer informatie.<!--4910348-->

Opstartinstallatiekopieën zijn taalonafhankelijk. Met deze functie kunt u één opstart installatie kopie gebruiken om de tekst van de taken reeks in meerdere talen weer te geven in WinPE. Neem de juiste taal ondersteuning op op het tabblad **optionele onderdelen** van de opstart installatie kopie. Stel vervolgens de juiste taken reeks variabele in om aan te geven welke taal moet worden weer gegeven. De taal van het geïmplementeerde besturings systeem is onafhankelijk van de taal in WinPE. De taal die door WinPE wordt weer gegeven voor de gebruiker, wordt als volgt bepaald:  

- Wanneer een gebruiker de taken reeks uitvoert vanuit een bestaand besturings systeem, wordt in Configuration Manager automatisch de taal gebruikt die voor de gebruiker is geconfigureerd. Wanneer de taken reeks automatisch wordt uitgevoerd als gevolg van een verplichte implementatie deadline, gebruikt Configuration Manager de taal van het besturings systeem.  

- Voor implementaties van besturings systemen die PXE of media gebruiken, stelt u de waarde taal-ID in de variabele **SMSTSLanguageFolder** in als onderdeel van een prestart-opdracht. Wanneer de computer wordt opgestart in WinPE, worden berichten weergegeven in de taal die u hebt opgegeven in de variabele. Als er een fout optreedt bij het openen van het bron bestand voor de taal in de opgegeven map of als u de variabele niet instelt, worden berichten weer gegeven in de standaard taal van WinPE.  

    > [!NOTE]  
    > Wanneer u Media beveiligt met een wacht woord, wordt de tekst waarin de gebruiker om het wacht woord wordt gevraagd, altijd weer gegeven in de WinPE-taal.  

Gebruik de volgende procedure om de WinPE-taal in te stellen voor met PXE of media geïnitieerde besturingssysteem implementaties.  

### <a name="set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>De Windows PE-taal instellen voor een door PXE of media geïnitieerde besturingssysteem implementatie  

1. Voordat u de opstart installatie kopie bijwerkt, controleert u of het juiste resource bestand (tsres.dll) voor de taken reeks zich in de bijbehorende taalmap op de site server bevindt. Het Engelse bron bestand bevindt zich bijvoorbeeld op de volgende locatie: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Als onderdeel van de prestart-opdracht stelt u de omgevings variabele **SMSTSLanguageFolder** in op de juiste taal-id. De taal-ID moet worden opgegeven met decimale en niet-hexadecimale notatie. Als u bijvoorbeeld de taal-ID op Engels wilt instellen, geeft u de decimale waarde **1033**op, niet de hexadecimale waarde 00000409 van de mapnaam.