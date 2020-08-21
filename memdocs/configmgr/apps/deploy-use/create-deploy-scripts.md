---
title: Scripts maken en uitvoeren
titleSuffix: Configuration Manager
description: Power shell-scripts maken en uitvoeren op client apparaten.
ms.date: 04/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: db3a673d99efc40bd6fa0da7930c66c648136e03
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695354"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1236459-->
Configuration Manager heeft een geïntegreerde mogelijkheid om Power shell-scripts uit te voeren. Power shell biedt het voor deel van het maken van geavanceerde, geautomatiseerde scripts die worden begrepen en gedeeld met een grotere community. Met de scripts kunt u aangepaste hulp middelen bouwen om software te beheren en kunt u zodanig scripten taken snel uitvoeren, zodat u gemakkelijk en consistent grote taken kunt doen.  

> [!Note]  
> Configuration Manager schakelt deze optionele functie standaard niet in. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  


Met deze integratie in Configuration Manager kunt u de functionaliteit voor het *uitvoeren van scripts* gebruiken om de volgende handelingen uit te voeren:

- Scripts maken en bewerken voor gebruik met Configuration Manager.
- Het gebruik van het script beheren via rollen en beveiligingsbereiken. 
- Scripts uitvoeren op verzamelingen of afzonderlijke on-premises beheerde Windows-Pc's.
- Ontvang snelle geaggregeerde script resultaten van client apparaten.
- Uitvoering van het script bewaken en rapportage resultaten weer geven van script uitvoer.

> [!WARNING]
> - Gezien de kracht van scripts, wordt u geadviseerd om opzettelijk en voorzichtig te zijn met het gebruik ervan. We hebben extra beveiligingen ontwikkeld om u te helpen. gescheiden rollen en bereiken. Zorg ervoor dat u de nauw keurigheid van scripts valideert voordat u ze uitvoert en bevestig dat ze afkomstig zijn van een vertrouwde bron om te voor komen dat onbedoelde script uitvoering wordt uitgevoerd. Wees mindful met uitgebreide tekens of andere tinten en leer hoe u scripts beveiligt. [Meer informatie over Power shell-script beveiliging](learn-script-security.md)
> - Bepaalde anti-malware-software kan per ongeluk gebeurtenissen activeren op basis van de Configuration Manager scripts uitvoeren of CMPivot-functies. Het is raadzaam om%windir%\CCM\ScriptStore uit te sluiten, zodat de anti-malware-software deze functies zonder interferentie kan uitvoeren.

## <a name="prerequisites"></a>Vereisten

- Voor het uitvoeren van Power shell-scripts moet Power shell-versie 3,0 of hoger worden uitgevoerd op de client. Als een script dat u uitvoert echter functionaliteit bevat van een nieuwere versie van Power shell, moet op de client waarop u het script uitvoert, die versie van Power shell worden uitgevoerd.
- Configuration Manager-clients moeten de-client uitvoeren vanuit de 1706-versie of later om scripts uit te voeren.
- Als u scripts wilt gebruiken, moet u lid zijn van de juiste Configuration Manager beveiligingsrol.
- Voor het importeren en ontwerpen van scripts moet uw account over **Create** -machtigingen voor **SMS-scripts**beschikken.
- Voor het goed keuren of weigeren van scripts-uw account moet machtigingen voor het **goed keuren** hebben voor **SMS-scripts**.
- Als u scripts wilt uitvoeren, moet uw account machtigingen voor het uitvoeren van het **script** hebben voor **verzamelingen**.

Voor meer informatie over Configuration Manager beveiligings rollen:</br>
[Beveiligingsbereiken voor uitvoer scripts](#security-scopes)</br>
[Beveiligings rollen voor uitvoer scripts](#bkmk_ScriptRoles)</br>
De [basis principes van beheer op basis van rollen](../../core/understand/fundamentals-of-role-based-administration.md).

## <a name="limitations"></a>Beperkingen

Scripts uitvoeren die op dit moment worden ondersteund:

- Script talen: Power shell
- Parameter typen: geheel getal, teken reeks en lijst.


>[!WARNING]
>Houd er rekening mee dat bij het gebruik van para meters een surface area wordt geopend voor potentieel risico op Power shell-injectie aanvallen. Er zijn verschillende manieren om het probleem op te lossen en te verhelpen, zoals het gebruik van reguliere expressies voor het valideren van parameter invoer of het gebruik van vooraf gedefinieerde para meters. Gemeen schappelijk best practice bevat geen geheimen in uw Power shell-scripts (geen wacht woorden, enz.). [Meer informatie over Power shell-script beveiliging](learn-script-security.md) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Auteurs en goed keurders van het script uitvoeren

Scripts uitvoeren gebruikt het concept *script auteurs* en *script-goed keurders* als afzonderlijke rollen voor de implementatie en uitvoering van een script. Als de rollen auteur en goed keurder zijn gescheiden, is het mogelijk dat er een belang rijk proces wordt gecontroleerd op het krachtige hulp programma voor het uitvoeren van scripts. Er is *een extra rol waarbij scripts kunnen* worden uitgevoerd, maar geen scripts worden gemaakt of goedgekeurd. Zie [beveiligings rollen maken voor scripts](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Besturings element voor script rollen

Standaard kunnen gebruikers geen script goed keuren dat ze hebben gemaakt. Omdat scripts krachtig, veelzijdig en mogelijk op veel apparaten kunnen worden geïmplementeerd, kunt u de rollen scheiden tussen de persoon die het script en de persoon die het script goedkeurt. Deze rollen bieden een extra beveiligings niveau voor het uitvoeren van een script zonder toezicht. U kunt secundaire goed keuring uitschakelen voor het eenvoudig testen van de tests.

### <a name="approve-or-deny-a-script"></a>Een script goed keuren of weigeren

Scripts moeten worden goedgekeurd door de rol van de *script fiatteur* voordat ze kunnen worden uitgevoerd. Een script goed keuren:

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.
2. Klik in de werk ruimte **software bibliotheek** op **scripts**.
3. Kies in de lijst **script** het script dat u wilt goed keuren of weigeren, en klik vervolgens op het tabblad **Start** in de groep **script** op **goed keuren/weigeren**.
4. In het dialoog venster **script goed keuren of** weigeren selecteert u **goed keuren**of **weigeren** voor het script. Voer eventueel een opmerking in over uw beslissing.  Als u een script weigert, kan het niet worden uitgevoerd op client apparaten. <br>
![Script-goed keuring](./media/run-scripts/RS-approval.png)
1. Voltooi de wizard. In de lijst met **scripts** ziet u de kolom wijziging **goedkeurings status** , afhankelijk van de actie die u hebt ondernomen.

### <a name="allow-users-to-approve-their-own-scripts"></a>Gebruikers toestaan hun eigen scripts goed te keuren

Deze goed keuring wordt hoofd zakelijk gebruikt voor de test fase van het ontwikkelen van scripts.

1. Klik op **Beheer**in de Configuration Manager-console.
2. Vouw in de werkruimte **Beheer****Siteconfiguratie**uit en klik vervolgens op **Sites**.
3. Kies uw site in de lijst met sites en klik vervolgens op het tabblad **Start** in de groep **sites** op **hiërarchie-instellingen**.
4. Schakel op het tabblad **Algemeen** van het dialoog venster **Eigenschappen van hiërarchie-instellingen** het selectie vakje **script auteurs vereisen extra script goed keurder**.

>[!IMPORTANT]
>Als best practice moet u geen script Auteur toestaan om hun eigen scripts goed te keuren. Het mag alleen worden toegestaan in een Lab-instelling. Overweeg zorgvuldig de mogelijke gevolgen van het wijzigen van deze instelling in een productie omgeving.

## <a name="security-scopes"></a>Beveiligingsbereiken
  
Run scripts gebruiken beveiligingsbereiken, een bestaande functie van Configuration Manager, om scripts te ontwerpen en uit te voeren via het toewijzen van labels die gebruikers groepen vertegenwoordigen. Zie op [rollen gebaseerd beheer configureren voor Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)voor meer informatie over het gebruik van beveiligingsbereiken.

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a> Beveiligings rollen maken voor scripts
De drie beveiligings rollen die worden gebruikt voor het uitvoeren van scripts, worden niet standaard in Configuration Manager gemaakt. Volg de stappen in het overzicht om de rollen script lopers, script auteurs en script-fiatteurs te maken.

1. Ga in de Configuration Manager-console naar **Administration**  > **beveiligings**  > **rollen** voor beheer beveiliging
2. Klik met de rechter muisknop op een rol en klik op **kopiëren**. Aan de rol die u hebt gekopieerd, zijn machtigingen al toegewezen. Zorg ervoor dat u alleen de gewenste machtigingen neemt. 
3. Geef een **naam** en **Beschrijving**voor de aangepaste rol op. 
4. Wijs aan de beveiligingsrol de machtigingen toe die hieronder worden beschreven.  

### <a name="security-role-permissions"></a>Machtigingen voor beveiligings rollen  

**Rolnaam**: script lopers  
- **Beschrijving**: met deze machtigingen kan deze rol alleen scripts uitvoeren die eerder zijn gemaakt en goedgekeurd door andere rollen.  
- **Machtigingen:** Zorg ervoor dat het volgende is ingesteld op **Ja**.  

|Categorie|Machtiging|Status|
|---|---|---|
|Verzameling|Script uitvoeren|Ja|
|Site|Lezen|Ja|
|SMS-scripts|Lezen|Ja|


**Rolnaam**: auteurs van scripts  
- **Beschrijving**: deze machtigingen maken het mogelijk om met deze rol scripts te schrijven, maar ze kunnen ze niet goed keuren of uitvoeren.  
- **Machtigingen**: Zorg ervoor dat de volgende machtigingen zijn ingesteld.
 
|Categorie|Machtiging|Status|
|---|---|---|
|Verzameling|Script uitvoeren|Nee|
|Site|Lezen|Ja|
|SMS-scripts|Maken|Ja|
|SMS-scripts|Lezen|Ja|
|SMS-scripts|Verwijderen|Ja|
|SMS-scripts|Wijzigen|Ja|


**Rolnaam**: goed keurders van het script  
- **Beschrijving**: deze machtigingen maken deze rol het goed keuren van scripts, maar ze kunnen ze niet maken of uitvoeren.  
- **Machtigingen:** Zorg ervoor dat de volgende machtigingen zijn ingesteld.  

|Categorie|Machtiging|Status|
|---|---|---|
|Verzameling|Script uitvoeren|Nee|
|Site|Lezen|Ja|
|SMS-scripts|Lezen|Ja|
|SMS-scripts|Goedkeuren|Ja|
|SMS-scripts|Wijzigen|Ja|

     
**Voor beeld van SMS-script machtigingen voor de rol script auteurs**  

 ![Voor beeld van SMS-script machtigingen voor de rol script auteurs](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Een script maken

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.
2. Klik in de werk ruimte **software bibliotheek** op **scripts**.
3. Klik op het tabblad **Start** in de groep **maken** op **script maken**.
4. Configureer op de pagina **script** van de wizard **script** maken de volgende instellingen:
    - **Script naam** : Voer een naam in voor het script. Hoewel u meerdere scripts met dezelfde naam kunt maken met behulp van dubbele namen, is het voor u moeilijker om het script te vinden dat u nodig hebt in de Configuration Manager-console.
    - **Script taal** -momenteel worden alleen Power shell-scripts ondersteund.
    - **Importeer** een Power shell-script in de-console. Het script wordt weer gegeven in het veld **script** .
    - **Clear** : Hiermee verwijdert u het huidige script uit het veld script.
    - **Script** : het momenteel geïmporteerde script wordt weer gegeven. U kunt het script in dit veld indien nodig bewerken.
5. Voltooi de wizard. Het nieuwe script wordt weer gegeven in **de lijst met de status** van **wachten op goed keuring**. Voordat u dit script op client apparaten kunt uitvoeren, moet u het goed keuren. 

> [!IMPORTANT]
> Vermijd het uitvoeren van scripts voor het opnieuw opstarten van een apparaat of het opnieuw opstarten van de Configuration Manager-agent wanneer u de functie scripts gebruiken uitvoert. Dit kan leiden tot een doorlopende status van het opnieuw opstarten. Als dat nodig is, zijn er verbeteringen aangebracht in de functie voor client meldingen die het opnieuw opstarten van apparaten mogelijk maakt. De [kolom wachtend op opnieuw starten](../../core/clients/manage/manage-clients.md#restart-clients) kan helpen bij het identificeren van apparaten waarvoor opnieuw moet worden opgestart. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Scriptparameters

Het toevoegen van para meters aan een script biedt meer flexibiliteit voor uw werk. U kunt Maxi maal 10 para meters toevoegen. Hieronder vindt u een overzicht van de huidige mogelijkheden van de functie scripts uitvoeren met script parameters voor; *Teken reeks*, gegevens typen *geheel getal* . Er zijn ook lijsten met vooraf gedefinieerde waarden beschikbaar. Als uw script niet-ondersteunde gegevens typen bevat, wordt er een waarschuwing weer gegeven.

Klik in het dialoog venster **script maken** op **script parameters** onder **script**.

Elk van de para meters van uw script heeft een eigen dialoog venster voor het toevoegen van meer details en validatie. Als er een standaard parameter is in het script, wordt deze in de gebruikers interface van de para meter geïnventariseerd en kunt u deze instellen. Configuration Manager overschrijft de standaard waarde niet, omdat het script nooit rechtstreeks wordt gewijzigd. U kunt dit nadenken als ' vooraf gevulde voorgestelde waarden ' zijn beschikbaar in de gebruikers interface, maar Configuration Manager biedt geen toegang tot de ' standaard-waarden ' tijdens runtime. Dit kan worden omzeild door het script te bewerken zodat de juiste standaard waarden worden gebruikt. <!--17694323-->

>[!IMPORTANT]
> Parameter waarden mogen geen enkele aanhalings tekens bevatten. </br></br>
> Er is een bekend probleem waarbij parameter waarden die zijn Inge sloten in enkele aanhalings tekens, niet naar behoren worden door gegeven aan het script. Gebruik in plaats daarvan dubbele aanhalings tekens wanneer u standaard parameter waarden met een spatie in een script opgeeft. Wanneer u standaard parameter waarden opgeeft tijdens het maken of uitvoeren van een **script**, is de standaard waarde in dubbele of enkele aanhalings tekens niet nodig, ongeacht of de waarde een spatie bevat of niet.

### <a name="parameter-validation"></a>Validatie van de para meter

Elke para meter in het script bevat een dialoog venster **Eigenschappen van script parameter** waarmee u validatie voor die para meter kunt toevoegen. Nadat u validatie hebt toegevoegd, moet u fouten ontvangen als u een waarde invoert voor een para meter die niet aan de validatie voldoet.

#### <a name="example-firstname"></a>Voor beeld: *FirstName*

In dit voor beeld kunt u de eigenschappen van de teken reeks parameter, voor *naam*, instellen.

![Script parameters: teken reeks](./media/run-scripts/RS-parameters-string.png)


De sectie validatie van het dialoog venster **Eigenschappen van script parameter** bevat de volgende velden voor uw gebruik:

- **Minimale lengte** : minimum aantal tekens van het veld voor *naam* .
- **Maximale lengte**: maximum aantal tekens van het veld voor *naam*
- **Regex** -short voor *reguliere expressie*. Zie de volgende sectie, *using reguliere expressies valideren*, voor meer informatie over het gebruik van de reguliere expressie.
- **Aangepaste fout** -nuttig voor het toevoegen van uw eigen aangepaste fout bericht dat alle systeem validatie fout berichten vervangt.

#### <a name="using-regular-expression-validation"></a>Reguliere expressie validatie gebruiken

Een reguliere expressie is een compacte vorm van programmering voor het controleren van een reeks tekens op basis van een gecodeerde validatie. U kunt bijvoorbeeld controleren op het ontbreken van een hoofdletter alfabet in het veld voor *naam* door het `[^A-Z]` in het veld *regex* te plaatsen.

De normale expressie verwerking voor dit dialoog venster wordt ondersteund door de .NET Framework. Voor hulp bij het gebruik van reguliere expressies raadpleegt u de [reguliere .net-expressie](/dotnet/standard/base-types/regular-expressions) en de taal van de [reguliere expressie](/dotnet/standard/base-types/regular-expression-language-quick-reference).


## <a name="script-examples"></a>Voorbeeldscripts

Hier volgen enkele voor beelden van scripts die u mogelijk wilt gebruiken met deze mogelijkheid.

### <a name="create-a-new-folder-and-file"></a>Een nieuwe map en een nieuw bestand maken

Met dit script maakt u een nieuwe map en een bestand in de map, op basis van uw naamgevings invoer.

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Versie van besturings systeem ophalen

Dit script maakt gebruik van WMI om de computer te doorzoeken op de versie van het besturings systeem.

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a> Power shell-scripts bewerken of kopiëren
<!--3705507-->
*(Geïntroduceerd bij versie 1902)*  
U kunt een bestaand Power shell-script **bewerken** of **kopiëren** dat wordt gebruikt met de functie **scripts uitvoeren** . In plaats van een script opnieuw te maken dat u moet wijzigen, kunt u dit nu rechtstreeks bewerken. Beide acties gebruiken dezelfde wizard-ervaring als wanneer u een nieuw script maakt. Wanneer u een script bewerkt of kopieert, wordt Configuration Manager de goedkeurings status niet behouden.

> [!Tip]  
> Bewerk geen scripts die actief worden uitgevoerd op clients. Het uitvoeren van het oorspronkelijke script wordt niet voltooid en u krijgt mogelijk niet de beoogde resultaten van deze clients.  

### <a name="edit-a-script"></a>Een script bewerken

1. Ga naar het knoop punt **scripts** onder de werk ruimte **software bibliotheek** .
1. Selecteer het script dat u wilt bewerken en klik vervolgens op **bewerken** in het lint. 
1. Wijzig of importeer het script opnieuw op de pagina met **script Details** .
1. Klik op **volgende** om de **samen vatting** te bekijken en vervolgens te **sluiten** wanneer u klaar bent met het bewerken van.

### <a name="copy-a-script"></a>Een script kopiëren

1. Ga naar het knoop punt **scripts** onder de werk ruimte **software bibliotheek** .
1. Selecteer het script dat u wilt kopiëren en klik vervolgens op **kopiëren** in het lint.
1. Wijzig de naam van het script in het veld **script naam** en breng eventueel extra wijzigingen aan.
1. Klik op **volgende** om de **samen vatting** te bekijken en vervolgens te **sluiten** wanneer u klaar bent met het bewerken van.


## <a name="run-a-script"></a>Een script uitvoeren

Nadat een script is goedgekeurd, kan het worden uitgevoerd op één apparaat of op een verzameling. Zodra de uitvoering van het script is gestart, wordt het snel gestart via een systeem met hoge prioriteit dat een time-out van één uur heeft. De resultaten van het script worden vervolgens geretourneerd met behulp van een status bericht systeem.

Een verzameling doelen selecteren voor uw script:

1. Klik op **Activa en naleving**op de Configuration Manager-console.
2. Klik op Apparaatverzamelingen in de werkruimte **Activa en naleving**.
3. Klik in de lijst **apparaat Collections** op de verzameling apparaten waarop u het script wilt uitvoeren.
4. Selecteer een verzameling van uw keuze en klik op **script uitvoeren**.
5. Kies op de pagina **script** van de wizard **script uitvoeren** een script uit de lijst. Alleen goedgekeurde scripts worden weer gegeven.
6. Klik op **volgende**en voltooi de wizard.

> [!IMPORTANT]
> Als een script niet wordt uitgevoerd, bijvoorbeeld omdat een doel apparaat wordt uitgeschakeld tijdens de periode van één uur, moet u het opnieuw uitvoeren.

### <a name="target-machine-execution"></a>Doel computer uitvoeren

Het script wordt uitgevoerd als het *systeem* -of *computer* account op de beoogde client (s). Dit account heeft beperkte netwerk toegang. Toegang tot externe systemen en locaties door het script moet dienovereenkomstig worden ingericht.

## <a name="script-monitoring"></a>Script bewaking

Nadat u het uitvoeren van een script op een verzameling apparaten hebt gestart, gebruikt u de volgende procedure om de bewerking te controleren. U kunt een script in realtime bewaken terwijl het wordt uitgevoerd, en later terugkeren naar de status en resultaten voor een bepaalde uitvoering van het script. De script status gegevens worden opgeschoond als onderdeel van de [taak verouderde onderhouds taken verwijderen](../../core/servers/manage/reference-for-maintenance-tasks.md) of verwijderen van het script.<br>

![Script monitor-uitvoerings status van script](./media/run-scripts/RS-monitoring-three-bar.png)

1. Klik in de Configuration Manager-console op **bewaking**.
2. Klik in de werk ruimte **bewaking** op **script status**.
3. In de lijst **script status** ziet u de resultaten voor elk script dat u hebt uitgevoerd op client apparaten. Een afsluit code van het script van **0** geeft doorgaans aan dat het script met succes is uitgevoerd.

 
   ![Script monitor-afgekapt script](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output"></a>Script uitvoer

De uitvoer van het retour script van de client met behulp van JSON-indeling door de resultaten van het script te sluizen naar de [ConvertTo-JSON-](/powershell/module/microsoft.powershell.utility/convertto-json) cmdlet. De JSON-indeling retourneert consequent Lees bare script uitvoer. Voor scripts die geen objecten retour neren als uitvoer, converteert de ConvertTo-JSON-cmdlet de uitvoer naar een eenvoudige teken reeks die door de client wordt geretourneerd in plaats van JSON.  

- Scripts die een onbekend resultaat krijgen of waarbij de client offline was, worden niet weer gegeven in de grafieken of gegevensset. <!--507179-->
- Vermijd het retour neren van een grote script uitvoer omdat deze is afgekapt tot 4 KB. <!--508488-->
- Converteer een Enum-object naar een teken reeks waarde in scripts zodat deze op de juiste wijze wordt weer gegeven in JSON-indeling. <!--508377-->

   ![Enum-object converteren naar een Sting-waarde](./media/run-scripts/enum-tostring-JSON.png)

U kunt gedetailleerde script uitvoer weer geven in de RAW-of Structured JSON-indeling. Met deze opmaak wordt de uitvoer eenvoudiger te lezen en te analyseren. Als het script geldige tekst in JSON-indeling retourneert of de uitvoer kan worden geconverteerd naar JSON met behulp van de [ConvertTo-JSON](/powershell/module/microsoft.powershell.utility/convertto-json) Power shell-cmdlet, bekijkt u de gedetailleerde uitvoer als **JSON-uitvoer** of **onbewerkte uitvoer**. Anders is de enige optie **script uitvoer**.

### <a name="example-script-output-is-convertible-to-valid-json"></a>Voor beeld: script uitvoer is converteerbaar naar een geldige JSON

Cmd `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Voor beeld: script uitvoer is geen geldige JSON

Cmd `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

## <a name="log-files"></a>Logboekbestanden

- Op de client standaard in C:\Windows\CCM\logs:  
  - **Scripts. log**  
  - **CcmMessaging.log**  

- Op het MP, standaard in C:\ SMS_CCM \Logs:
  - **MP_RelayMsgMgr. log**  

- Op de site server, standaard in C:\Program Files\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine. log**

## <a name="see-also"></a>Zie ook

- [Op rollen gebaseerd beheer configureren voor Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Basisprincipes voor beheer op basis van rollen](../../core/understand/fundamentals-of-role-based-administration.md)