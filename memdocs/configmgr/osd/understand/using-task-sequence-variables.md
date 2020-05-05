---
title: Takenreeksvariabelen gebruiken
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van de variabelen in een Configuration Manager taken reeks.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c043cfabc411dbd5ae4984110fc2904d37669300
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717823"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Taken reeks variabelen gebruiken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

 De taken reeks engine in de implementatie functie van het besturings systeem van Configuration Manager gebruikt veel variabelen om het gedrag ervan te bepalen. Gebruik deze variabelen voor het volgende:

- Voor waarden instellen voor stappen  
- Gedrag voor specifieke stappen wijzigen  
- Gebruiken in scripts voor complexere acties  

Zie [taken reeks variabelen](task-sequence-variables.md)voor een overzicht van alle beschik bare taken reeks variabelen.

## <a name="types-of-variables"></a><a name="bkmk_types"></a>Typen variabelen

Er zijn verschillende typen variabelen:  

- [Ingebouwd](#bkmk_built-in)  
- [Actie](#bkmk_action)  
- [Aangepast](#bkmk_custom)  
- [Alleen-lezen](#bkmk_read-only)  
- [Array](#bkmk_array)  

### <a name="built-in-variables"></a><a name="bkmk_built-in"></a>Ingebouwde variabelen

Ingebouwde variabelen bieden informatie over de omgeving waarin de taken reeks wordt uitgevoerd. Hun waarden zijn beschikbaar in de hele taken reeks. De taken reeks engine initialiseert doorgaans ingebouwde variabelen voordat de stappen worden uitgevoerd.

`_SMSTSLogPath` Is bijvoorbeeld een omgevings variabele die het pad specificeert naar Configuration Manager-onderdelen logboek bestanden schrijven. Elke taken reeks stap heeft toegang tot deze omgevings variabele.

De taken reeks evalueert enkele variabelen voor elke stap. Een voor beeld `_SMSTSCurrentActionName` bevat een lijst met de naam van de huidige stap.

### <a name="action-variables"></a><a name="bkmk_action"></a>Actie variabelen

Variabelen voor taken reeks acties geven configuratie-instellingen op die door één taken reeks stap worden gebruikt. Standaard worden de instellingen van de stap geïnitialiseerd voordat deze wordt uitgevoerd. Deze instellingen zijn alleen beschikbaar wanneer de gekoppelde taken reeks stap wordt uitgevoerd. De taken reeks voegt de waarde van de actie variabele toe aan de omgeving voordat de stap wordt uitgevoerd. Daarna wordt de waarde uit de omgeving verwijderd nadat de stap is uitgevoerd.

U kunt bijvoorbeeld de stap **opdracht regel uitvoeren** toevoegen aan een taken reeks. Deze stap bevat een **Start in** -eigenschap. De taken reeks slaat een standaard waarde voor deze eigenschap op als `WorkingDirectory` de variabele. De taken reeks initialiseert deze waarde voordat de stap **opdracht regel uitvoeren** wordt uitgevoerd. Terwijl deze stap wordt uitgevoerd, opent u de waarde van de eigenschap **begin in** van de `WorkingDirectory` waarde. Nadat de stap is voltooid, verwijdert de taken reeks de waarde van de `WorkingDirectory` variabele uit de omgeving. Als de taken reeks een andere stap **opdracht regel uitvoeren** bevat, wordt een nieuwe `WorkingDirectory` variabele geïnitialiseerd. Op dat moment stelt de taken reeks de variabele in op de begin waarde voor de huidige stap. Zie [variabele workingdirectory](task-sequence-variables.md#WorkingDirectory)voor meer informatie.  

De *standaard* waarde voor een actie variabele is aanwezig wanneer de stap wordt uitgevoerd. Als u een *nieuwe* waarde instelt, is deze beschikbaar voor meerdere stappen in de taken reeks. Als u een standaard waarde overschrijft, blijft de nieuwe waarde in de omgeving. Deze nieuwe waarde overschrijft de standaard waarde voor de overige stappen in de taken reeks. U kunt bijvoorbeeld een set variabele-stap voor **taken reeks** toevoegen als de eerste stap van de taken reeks. Met deze stap stelt `WorkingDirectory` u de `C:\`variabele in op. Elke **uitvoerings opdracht regel** stap in de taken reeks maakt gebruik van de nieuwe waarde voor het starten van de map.  

Sommige taken reeks stappen markeren bepaalde actie variabelen als *uitvoer*. Stappen verderop in de taken reeks lezen deze uitvoer variabelen.

> [!Note]  
> Niet alle taken reeks stappen hebben actie variabelen. Hoewel er bijvoorbeeld variabelen zijn gekoppeld aan de actie **BitLocker inschakelen** , zijn er geen variabelen gekoppeld aan de actie **BitLocker uitschakelen** .  

### <a name="custom-variables"></a><a name="bkmk_custom"></a>Aangepaste variabelen

Deze variabelen zijn die Configuration Manager niet worden gemaakt. Initialiseer uw eigen variabelen om te gebruiken als voor waarden, in opdracht regels of in scripts.

Wanneer u een naam voor een nieuwe taken reeks variabele opgeeft, volgt u deze richt lijnen:  

- De naam van de taken reeks variabele kan letters, cijfers, het onderstrepings`_`teken () en een koppel`-`teken () bevatten.  

- Namen van taken reeks variabelen hebben een minimum lengte van één teken en een maximale lengte van 256 tekens.  

- Door de gebruiker gedefinieerde variabelen moeten beginnen met een letter`A-Z` ( `a-z`of).  

- Namen van door de gebruiker gedefinieerde variabelen mogen niet beginnen met een onderstrepings teken. Alleen alleen-lezen taken reeks variabelen worden voorafgegaan door het onderstrepings teken.  

- Namen van taken reeks variabelen zijn niet hoofdletter gevoelig. `OSDVAR` En `osdvar` zijn bijvoorbeeld dezelfde taken reeks variabele.  

- Namen van taken reeks variabelen kunnen niet beginnen of eindigen met een spatie. Ze kunnen ook geen Inge sloten spaties bevatten. Alle spaties aan het begin of het einde van de naam van een variabele worden door de taken reeks genegeerd.  

Er is geen limiet ingesteld voor het aantal taken reeks variabelen dat u kunt maken. Het maximale aantal variabelen is echter wel beperkt door de grootte van de takenreeksomgeving. De limiet voor de totale grootte van de takenreeksomgeving is 32 MB.  

### <a name="read-only-variables"></a><a name="bkmk_read-only"></a>Alleen-lezen variabelen

U kunt de waarde van sommige variabelen niet wijzigen, wat alleen-lezen is. Meestal begint de naam met een onderstrepings teken`_`(). De taken reeks gebruikt deze voor de bewerkingen ervan. Alleen-lezen variabelen zijn zichtbaar in de taken reeks omgeving.

Deze variabelen zijn handig in scripts of op opdracht regels. U kunt bijvoorbeeld een opdracht regel uitvoeren en de uitvoer naar een logboek bestand in `_SMSTSLogPath` met de andere logboek bestanden belichten.

> [!NOTE]  
> Alleen-lezen taken reeks variabelen kunnen worden gelezen door stappen in een taken reeks, maar ze kunnen niet worden ingesteld. Gebruik bijvoorbeeld een alleen-lezen variabele als onderdeel van de opdracht regel voor de stap **opdracht regel uitvoeren** . U kunt geen alleen-lezen variabele instellen met behulp van de stap **taken reeks variabele instellen** .  

### <a name="array-variables"></a><a name="bkmk_array"></a>Matrix variabelen

De taken reeks slaat enkele variabelen op als een matrix. Elk element in de matrix staat voor de instellingen voor één object. Gebruik deze variabelen wanneer een apparaat meer dan één object heeft om te configureren. De volgende taken reeks stappen gebruiken matrix variabelen:

- [Netwerkinstellingen toepassen](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

- [Schijf formatteren en partitioneren](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  

## <a name="how-to-set-variables"></a><a name="bkmk_set"></a>Variabelen instellen

Voor aangepaste variabelen of variabelen die niet alleen-lezen zijn, zijn er verschillende methoden om de waarde van de variabele te initialiseren en in te stellen:  

- Stap van [taken reeks variabele instellen](#bkmk_set-ts-step)
- Stap [dynamische variabelen instellen](#bkmk_set-dyn-step)
- [Power shell-script stap uitvoeren](#bkmk_run-ps)
- [Verzamelings-en apparaat-variabelen](#bkmk_set-coll-var)  
- [COM-object TSEnvironment](#bkmk_set-com)  
- [Prestart-opdracht](#bkmk_set-prestart)  
- [Wizard taken reeks](#bkmk_set-tswiz)
- [Wizard taken reeks media](#bkmk_set-media)  

Verwijder een variabele uit de omgeving door dezelfde methoden te gebruiken als voor het maken van een variabele. Als u een variabele wilt verwijderen, stelt u de waarde van de variabele in op een lege teken reeks.  

U kunt methoden combi neren om een taken reeks variabele in te stellen op verschillende waarden voor dezelfde reeks. Stel bijvoorbeeld de standaard waarden in met behulp van de taken reeks editor en stel vervolgens aangepaste waarden in met behulp van een script.

Als u dezelfde variabele op verschillende manieren instelt, gebruikt de taken reeks engine de volgende volg orde:  

1. Eerst worden verzamelings variabelen geëvalueerd.  

2. Apparaatspecifieke variabelen overschrijven dezelfde variabele die is ingesteld voor een verzameling.  

3. Variabelen die worden ingesteld door een wille keurige methode tijdens de taken reeks, hebben voor rang op verzamelings-of apparaat-variabelen.  

### <a name="general-limitations-for-task-sequence-variable-values"></a>Algemene beperkingen voor waarden van taken reeks variabelen

- Waarden van taken reeks variabelen mogen niet langer zijn dan 4.000 tekens.  

- U kunt een alleen-lezen taken reeks variabele niet wijzigen. Alleen-lezen variabelen hebben namen die beginnen met een onderstrepings teken`_`().  

- Waarden van taken reeks variabelen kunnen hoofdletter gevoelig zijn, afhankelijk van het gebruik van de waarde. In de meeste gevallen zijn de waarden van taken reeks variabelen niet hoofdletter gevoelig. Een variabele met een wacht woord is hoofdletter gevoelig.  

### <a name="set-task-sequence-variable"></a><a name="bkmk_set-ts-step"></a>Taken reeks variabele instellen

Gebruik deze stap in de taken reeks om één variabele in te stellen op een enkele waarde.

Zie [set-variabele taken reeks](task-sequence-steps.md#BKMK_SetTaskSequenceVariable)voor meer informatie.

### <a name="set-dynamic-variables"></a><a name="bkmk_set-dyn-step"></a>Dynamische variabelen instellen

Gebruik deze stap in de taken reeks om een of meer taken reeks variabelen in te stellen. U definieert regels in deze stap om te bepalen welke variabelen en waarden u moet gebruiken.

Zie [set Dynamic Varia bles](task-sequence-steps.md#BKMK_SetDynamicVariables)voor meer informatie.

### <a name="run-powershell-script"></a><a name="bkmk_run-ps"></a>Power shell-script uitvoeren

<!-- 6315548 -->

Gebruik deze stap in de taken reeks om een Power shell-script te gebruiken om een taken reeks variabele in te stellen.

U kunt een script naam uit een pakket opgeven, of rechtstreeks een Power shell-script invoeren in de stap. Gebruik vervolgens de stap eigenschap om **naar de taken reeks variabele** uit te voeren om de script uitvoer op te slaan in een aangepaste taken reeks variabele.

Zie [Power shell-script uitvoeren](task-sequence-steps.md#BKMK_RunPowerShellScript)voor meer informatie over deze stap.

> [!NOTE]
> U kunt ook een Power shell-script gebruiken om een of meer variabelen in te stellen met het **TSEnvironment** -object. Zie [variabelen gebruiken in een taken reeks die wordt uitgevoerd](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) in de Configuration Manager SDK voor meer informatie.

#### <a name="example-scenario-with-run-powershell-script-step"></a>Voorbeeld scenario met de stap Power shell-script uitvoeren

Uw omgeving heeft gebruikers in meerdere landen, dus u wilt een query uitvoeren op de taal van het besturings systeem om in te stellen als voor waarde voor meerdere taalspecifieke stappen voor het **besturings systeem** .

1. Voeg een exemplaar van het **Power shell-script uitvoeren** toe aan de taken reeks vóór de stappen voor het **Toep assen van het besturings systeem** .

1. Gebruik de optie om **een Power shell-script** in te voeren om de volgende opdracht op te geven:

    ```powershell
    (Get-Culture).TwoLetterISOLanguageName
    ```

    Zie [Get-Culture](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/get-culture)voor meer informatie over de cmdlet. Zie [lijst met iso 639-1-codes](https://wikipedia.org/wiki/List_of_ISO_639-1_codes)voor meer informatie over de ISO-taal namen van twee letters.

1. Geef `CurrentOSLanguage`voor de optie voor **uitvoer naar de taken reeks variabele**op.

    ![Scherm afbeelding van voor beeld van Power shell-script stap uitvoeren](media/run-powershell-script-example-language.png)

1. Maak in de stap **besturings systeem Toep assen** voor de installatie kopie van de Engelse taal de volgende voor waarde:`Task Sequence Variable CurrentOSLanguage equals "en"`

    ![Scherm afbeelding van voor waarde voor beeld in de stap besturings systeem Toep assen](media/condition-custom-task-sequence-variable.png)

    > [!TIP]
    > Zie voor meer informatie over het maken van een voor waarde voor een stap voor [het openen van variabelen-stap voorwaarde](#bkmk_access-condition).

1. Sla de taken reeks op en implementeer deze.

Wanneer de stap **Power shell-script uitvoeren** op een apparaat met de Engelse taal versie van Windows wordt uitgevoerd, retourneert de `en`opdracht de waarde. Vervolgens wordt die waarde opgeslagen in de aangepaste variabele. Wanneer de stap **besturings systeem Toep assen** voor de Engelse taal op hetzelfde apparaat wordt uitgevoerd, wordt de voor waarde geëvalueerd als waar. Als u meerdere exemplaren van de stap **besturings systeem Toep assen** voor verschillende talen hebt, voert de taken reeks de stap die overeenkomt met de taal van het besturings systeem, dynamisch uit.

### <a name="collection-and-device-variables"></a><a name="bkmk_set-coll-var"></a>Verzamelings-en apparaat-variabelen

U kunt aangepaste taken reeks variabelen definiëren voor apparaten en verzamelingen. Variabelen die u voor een apparaat definieert, worden taken reeks variabelen per apparaat genoemd. Naar variabelen die voor een verzameling zijn gedefinieerd, wordt verwezen als verzamelingtakenreeksvariabelen. Als er sprake is van een conflict, hebben variabelen per apparaat voor rang op variabelen van het verzamelings niveau. Dit gedrag houdt in dat taken reeks variabelen die aan een specifiek apparaat zijn toegewezen automatisch een hogere prioriteit hebben dan variabelen die zijn toegewezen aan de verzameling die het apparaat bevat.  

Bijvoorbeeld, apparaat XYZ is lid van verzameling ABC. U wijst MyVariable toe aan verzameling ABC met de waarde 1. U wijst ook MyVariable toe aan het apparaat XYZ met de waarde 2. De variabele die is toegewezen aan XYZ heeft een hogere prioriteit dan de variabele die is toegewezen aan verzameling ABC. Wanneer een taken reeks met deze variabele wordt uitgevoerd op XYZ, heeft MyVariable de waarde 2.

U kunt de variabelen per apparaat en per verzameling verbergen, zodat deze niet zichtbaar zijn in de Configuration Manager-console. Wanneer u de optie **deze waarde niet weer geven in de Configuration Manager-console**gebruikt, wordt de waarde van de variabele niet weer gegeven in de console. De variabele kan nog steeds worden gebruikt door de taken reeks wanneer deze wordt uitgevoerd. Als u deze variabelen niet meer wilt verbergen, verwijdert u deze eerst. Definieer de variabelen vervolgens opnieuw zonder de optie te selecteren om ze te verbergen.  

> [!WARNING]  
> De instelling om **deze waarde niet weer te geven in de Configuration Manager-console** is alleen van toepassing op de Configuration Manager-console. De waarden voor de variabelen worden nog steeds weer gegeven in het logboek bestand van de taken reeks (**bestand smsts. log**).

U kunt per apparaat variabelen op een primaire site of op een centrale beheer site beheren. Configuration Manager ondersteunt niet meer dan 1.000 toegewezen variabelen voor een apparaat.  

> [!IMPORTANT]  
> Wanneer u per-verzameling-variabelen voor taken reeksen gebruikt, moet u rekening houden met het volgende gedrag:  
>
> - Wijzigingen in verzamelingen worden altijd gerepliceerd in de hele hiërarchie. Wijzigingen die u aanbrengt in verzamelings variabelen zijn niet alleen van toepassing op leden van de huidige site, maar op alle leden van de verzameling in de gehele hiërarchie.  
>  
> - Wanneer u een verzameling verwijdert, worden met deze actie ook de taken reeks variabelen verwijderd die u voor de verzameling hebt geconfigureerd.  

#### <a name="create-task-sequence-variables-for-a-device"></a>Taken reeks variabelen voor een *apparaat* maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **apparaten** .  

2. Selecteer het doel apparaat en selecteer **Eigenschappen**.  

3. Ga in het dialoog venster **Eigenschappen** naar het tabblad **variabelen** .  

4. Voor elke variabele die u wilt maken, selecteert u het pictogram **Nieuw** . Geef de **naam** en **waarde** van de taken reeks variabele op. Als u de variabele wilt verbergen zodat deze niet zichtbaar is in de Configuration Manager-console, selecteert u de optie **deze waarde niet weer geven in de Configuration Manager-console**.  

5. Wanneer u alle variabelen aan de apparaateigenschappen hebt toegevoegd, selecteert u **OK**.  

#### <a name="create-task-sequence-variables-for-a-collection"></a>Taken reeks variabelen voor een *verzameling* maken

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **Apparaatsets** . Selecteer de doel verzameling en kies **Eigenschappen**.  

2. Ga in het dialoog venster **Eigenschappen** naar het tabblad **verzamelings variabelen** .  

3. Voor elke variabele die u wilt maken, selecteert u het pictogram **Nieuw** . Geef de **naam** en **waarde** van de taken reeks variabele op. Als u de variabele wilt verbergen zodat deze niet zichtbaar is in de Configuration Manager-console, selecteert u de optie **deze waarde niet weer geven in de Configuration Manager-console**.  

4. Geef eventueel de prioriteit voor Configuration Manager op die moet worden gebruikt wanneer de taken reeks variabelen worden geëvalueerd.  

5. Wanneer u alle variabelen aan de verzamelings eigenschappen hebt toegevoegd, selecteert u **OK**.  

### <a name="tsenvironment-com-object"></a><a name="bkmk_set-com"></a>COM-object TSEnvironment

Als u wilt werken met variabelen uit een script, gebruikt u het **TSEnvironment** -object.

Zie [variabelen gebruiken in een taken reeks die wordt uitgevoerd](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md) in de Configuration Manager SDK voor meer informatie.

### <a name="prestart-command"></a><a name="bkmk_set-prestart"></a>Prestart-opdracht

De prestart-opdracht is een script of een uitvoerbaar bestand dat wordt uitgevoerd in Windows PE voordat de gebruiker de taken reeks selecteert. De prestart-opdracht kan een query uitvoeren op een variabele of de gebruiker vragen om informatie en deze vervolgens opslaan in de omgeving. Gebruik het COM-object [TSEnvironment](#bkmk_set-com) om variabelen van de prestart-opdracht te lezen en te schrijven.

Zie [prestart-opdrachten voor taken reeks media](prestart-commands-for-task-sequence-media.md)voor meer informatie.

### <a name="task-sequence-wizard"></a><a name="bkmk_set-tswiz"></a>Wizard taken reeks

Vanaf versie 1906, nadat u een taken reeks in het venster taken reeks hebt geselecteerd, bevat de pagina voor het bewerken van taken reeks variabelen een knop **bewerken** . U kunt toegankelijke sneltoetsen gebruiken om de variabelen te bewerken. Deze wijziging helpt in gevallen waarin een muis niet beschikbaar is.<!-- 4668846 -->

### <a name="task-sequence-media-wizard"></a><a name="bkmk_set-media"></a>Wizard taken reeks media

Variabelen opgeven voor taken reeksen die vanaf media worden uitgevoerd. Wanneer u media gebruikt om het besturings systeem te implementeren, voegt u de taken reeks variabelen toe en geeft u hun waarden op wanneer u de media maakt. De variabelen en hun waarden worden opgeslagen op de media.  

> [!NOTE]  
> Taken reeksen worden opgeslagen op zelfstandige media. Alle andere typen media, zoals voor bereide media, halen de taken reeks op uit een beheer punt.  

Wanneer u een taken reeks uit media uitvoert, kunt u een variabele toevoegen op de pagina **aanpassing** van de wizard.

Gebruik de mediavariabelen in plaats van per-verzameling- of per-computer-variabelen. Als de taken reeks wordt uitgevoerd vanaf media, zijn de variabelen per computer en per verzameling niet van toepassing en worden ze niet gebruikt.  

> [!TIP]  
> De taken reeks schrijft de pakket-ID en prestart-opdracht regel naar het bestand **CreateTSMedia. log** op de computer waarop de Configuration Manager-console wordt uitgevoerd. Dit logboek bestand bevat de waarde voor alle taken reeks variabelen. Bekijk dit logboek bestand om de waarde voor de taken reeks variabelen te controleren.  

Zie [taken reeks media maken](../deploy-use/create-task-sequence-media.md)voor meer informatie.

## <a name="how-to-access-variables"></a><a name="bkmk_access"></a>Toegang tot variabelen

Nadat u de variabele en de waarde ervan hebt opgegeven met behulp van een van de methoden uit de vorige sectie, gebruikt u deze in uw taken reeksen. U kunt bijvoorbeeld de standaard waarden voor ingebouwde taken reeks variabelen openen, of een stap voorwaardelijk maken op basis van de waarde van een variabele.  

Gebruik de volgende methoden voor toegang tot variabelen waarden in de taken reeks omgeving:

- [Gebruiken in een stap](#bkmk_access-step)  
- [Stap voorwaarde](#bkmk_access-condition)  
- [Aangepast script](#bkmk_access-script)  
- [Antwoord bestand voor Windows Setup](#bkmk_access-answer)  
  
### <a name="use-in-a-step"></a><a name="bkmk_access-step"></a>Gebruiken in een stap

Geef een waarde voor de variabele op voor een instelling in een taken reeks stap. Bewerk de stap in de taken reeks editor en geef de naam van de variabele op als de veld waarde. Plaats de naam van de variabele tussen procent`%`tekens ().

Gebruik bijvoorbeeld de naam van de variabele als onderdeel van het veld **opdracht regel** van de stap **opdracht regel uitvoeren** . De volgende opdracht regel schrijft de naam van de computer naar een tekst bestand.

`cmd.exe /c %_SMSTSMachineName% > C:\File.txt`

### <a name="step-condition"></a><a name="bkmk_access-condition"></a>Stap voorwaarde

Ingebouwde of aangepaste taken reeks variabelen gebruiken als onderdeel van een voor waarde voor een stap of groep. De taken reeks evalueert de waarde van de variabele voordat de stap of groep wordt uitgevoerd.

Voer de volgende stappen uit om een voor waarde toe te voegen waarmee een variabele waarde wordt geëvalueerd:  

1. Selecteer in de taken reeks editor de stap of groep waaraan u de voor waarde wilt toevoegen.  

2. Schakel over naar het tabblad **Opties** voor de stap of groep. Klik op **voor waarde toevoegen**en selecteer **taken reeks variabele**.  

3. Geef in het dialoog venster **taken reeks variabele** de volgende instellingen op:  

    - **Variabele**: de naam van de variabele. Bijvoorbeeld `_SMSTSInWinPE`.  

    - **Voor waarde**: de voor waarde om de waarde van de variabele te evalueren. **Is bijvoorbeeld gelijk aan**.  

    - **Waarde**: de waarde van de variabele die moet worden gecontroleerd. Bijvoorbeeld `false`.  

De drie voor beelden hierboven vormen een gemeen schappelijke voor waarde om te testen of de taken reeks wordt uitgevoerd vanuit een opstart installatie kopie in Windows PE:

> **Taken reeks variabele**`_SMSTSInWinPE equals "false"`

Zie deze voor waarde in de groep **bestanden en instellingen vastleggen** van de standaard taken reeks sjabloon voor het installeren van een bestaande installatie kopie van het besturings systeem.

Zie [taken reeks editor-voor waarden](task-sequence-editor.md#bkmk_conditions)voor meer informatie over voor waarden.

### <a name="custom-script"></a><a name="bkmk_access-script"></a>Aangepast script

Lees en schrijf variabelen met behulp van het COM-object **Microsoft. SMS. TSEnvironment** terwijl de taken reeks wordt uitgevoerd.

In het volgende Windows Power shell-voor beeld wordt de variabele **_SMSTSLogPath** opgevraagd om de huidige logboek locatie op te halen. Met het script wordt ook een aangepaste variabele ingesteld.

```PowerShell
# Create an object to access the task sequence environment
$tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment

# Query the environment to get an existing variable
# Set a variable for the task sequence log path
$LogPath = $tsenv.Value("_SMSTSLogPath")

# Or, convert all of the variables currently in the environment to PowerShell variables
$tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

# Write a message to a log file
Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append

# Set a custom variable "startTime" to the current time
$tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
```

### <a name="windows-setup-answer-file"></a><a name="bkmk_access-answer"></a>Antwoord bestand voor Windows Setup

Het Windows Setup-antwoord bestand dat u opgeeft, kan Inge sloten taken reeks variabelen bevatten. Gebruik het formulier `%varname%`, waarbij *varnaam* de naam van de variabele is. De stap **Windows en ConfigMgr installeren** vervangt de teken reeks met de variabelenaam voor de werkelijke waarde van de variabele. Deze Inge sloten taken reeks variabelen kunnen niet worden gebruikt in velden die alleen numeriek zijn in het antwoord bestand Unattend. XML.

Zie [Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)voor meer informatie.

## <a name="see-also"></a>Zie ook

- [Stappen voor takenreeksen](task-sequence-steps.md)

- [Takenreeksvariabelen](task-sequence-variables.md)

- [Planningsoverwegingen voor het automatiseren van taken](../plan-design/planning-considerations-for-automating-tasks.md)

- [Taken reeks editor](task-sequence-editor.md)
