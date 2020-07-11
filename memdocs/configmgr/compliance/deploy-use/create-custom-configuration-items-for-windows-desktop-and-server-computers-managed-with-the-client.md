---
title: Aangepaste configuratie-items maken
titleSuffix: Configuration Manager
description: Instellingen voor Windows-computers en-servers beheren met een aangepast configuratie-item voor Windows-Desk tops en-servers
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 24637862326b029f974843c18ccba835ee5501ba
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240419"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Aangepaste configuratie-items maken voor Windows Desktop-en Server computers die worden beheerd met de Configuration Manager-client

*Van toepassing op: Configuration Manager (huidige vertakking)*


Gebruik het aangepaste configuratie-item Configuration Manager **Windows-Bureau bladen en-servers** om instellingen te beheren voor Windows-computers en-servers die worden beheerd door de Configuration Manager-client.  



## <a name="start-the-wizard"></a>De wizard starten

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** , vouw **instellingen voor naleving**uit en selecteer het knoop punt configuratie- **items** .  

2. Selecteer **configuratie-item maken**op het tabblad **Start** van het lint in de groep **maken** .  

3. Geef op de pagina **Algemeen** van de **Wizard Configuratie-item maken** een naam en een optionele beschrijving voor het configuratie-item op.  

4. Selecteer onder **Geef het type configuratie-item op dat u wilt maken** de optie **Windows-desktops en -servers (aangepast)**.  

    > [!TIP]  
    > Als u instellingen voor de detectiemethode wilt opgeven om te controleren op het bestaan van een toepassing, selecteert u **Dit configuratie-item bevat toepassingsinstellingen**.  

5. Selecteer **Categorieën** voor het maken en toewijzen van categorieën om configuratie-items te zoeken en te filteren in de Configuration Manager-console.  



## <a name="detection-methods"></a>Detectie methoden  

Gebruik deze procedure om gegevens voor de detectiemethode op te geven voor het configuratie-item.  

> [!NOTE]  
> Deze informatie is alleen van toepassing als u **dit configuratie-item bevat toepassings instellingen** op de pagina **Algemeen** van de wizard.  

Een detectie methode in Configuration Manager bevat regels die worden gebruikt om te detecteren of een toepassing op een computer is geïnstalleerd. Deze detectie vindt plaats voordat de client de naleving van het configuratie-item evalueert. Als u wilt verifiëren of een toepassing is geïnstalleerd, kunt u controleren of er een Windows Installer-bestand aanwezig is voor de toepassing, een aangepast script gebruiken of **Altijd aannemen dat de toepassing is geïnstalleerd** selecteren om het configuratie-item op naleving te controleren, ongeacht of de toepassing is geïnstalleerd.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Een installatie van een toepassing detecteren met behulp van het Windows Installer-bestand  

1. Selecteer op de pagina **detectie methoden** van de **wizard Configuratie-item maken**de optie voor het **gebruik van Windows Installer detectie**.  

2. Selecteer **openen**, blader naar het Windows Installer bestand (. msi) dat u wilt detecteren en selecteer vervolgens **openen**.  

3. In het veld **versie** wordt automatisch het versie nummer van het Windows Installer bestand ingevuld. Als de weer gegeven waarde onjuist is, voert u hier een nieuw versie nummer in.  

4. Als u elk gebruikers profiel op de computer wilt detecteren, selecteert u **deze toepassing is geïnstalleerd voor een of meer gebruikers**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Een bepaalde toepassing en een implementatietype detecteren  

1. Selecteer op de pagina **detectie methoden** van de **wizard Configuratie-item maken**voor het **detecteren van een specifieke toepassing en een implementatie type**. Kies **Selecteren**.   

2. Selecteer in het dialoogvenster **Toepassing opgeven** de toepassing en een bijbehorend implementatietype dat u wilt detecteren.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>De installatie van een toepassing detecteren met een aangepast script  

1. Selecteer op de pagina **detectie methoden** van de **wizard Configuratie-item maken**de optie om **een aangepast script te gebruiken om deze toepassing te detecteren**.  

2. Selecteer in de lijst de taal van het script. Kies uit de volgende indelingen:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > Vanaf versie 1810, wanneer een Windows Power shell-script wordt uitgevoerd als detectie methode, roept de Configuration Manager-client Power shell aan met de `-NoProfile` para meter. Met deze optie wordt Power shell zonder profielen gestart. Een Power shell-profiel is een script dat wordt uitgevoerd wanneer Power shell wordt gestart. <!--3607762-->  

3. Selecteer **openen**, blader naar het script dat u wilt gebruiken en selecteer vervolgens **openen**.  



## <a name="specify-supported-platforms"></a>Ondersteunde platforms opgeven  

Selecteer op de pagina **ondersteunde platforms** van de **wizard Configuratie-item maken**de Windows-versies waarop u wilt dat het configuratie-item wordt beoordeeld op naleving, of kies **Alles selecteren**.

U kunt **de versie van Windows ook hand matig opgeven**. Selecteer **toevoegen** en geef elk deel van het Windows-buildnummer op.

> [!NOTE]
> Wanneer u Windows Server 2016 opgeeft, bevat de selectie voor `All Windows Server 2016 and higher 64-bit)` ook Windows server 2019. Als u alleen Windows Server 2016 wilt opgeven, gebruikt u de optie om **de versie van Windows hand matig**op te geven. <!--5866480-->



##  <a name="configure-settings"></a>Instellingen configureren  

Gebruik deze procedure om de instellingen in het configuratie-item te configureren.  

Instellingen vertegenwoordigen de zakelijke of technische voorwaarden die worden gebruikt voor het evalueren van naleving op clientapparaten. U kunt een nieuwe instelling configureren of naar een bestaande instelling op een referentiecomputer bladeren.  

1. Selecteer op de pagina **instellingen** van de **wizard Configuratie-item maken**de optie **Nieuw**.  

2. Op het tabblad **Algemeen** van het dialoogvenster **Instellingen maken** geeft u de volgende gegevens op:  

    - **Naam**: Voer een unieke naam in voor de instelling. U kunt maximaal 256 tekens gebruiken.  

    - **Beschrijving**: Voer een beschrijving in voor de instelling. U kunt maximaal 256 tekens gebruiken.  

    - **Instellings type**: Kies in de lijst een van de volgende instellings typen voor deze instelling:  
        - [Active Directory-query](#bkmk_adquery)
        - [Assembly](#bkmk_assembly)
        - [Bestandssysteem](#bkmk_file)
        - [IIS Metabase](#bkmk_iis)
        - [Register sleutel](#bkmk_regkey)
        - [Register waarde](#bkmk_regval)
        - [Script](#bkmk_script)
        - [SQL-query](#bkmk_sql)
        - [WQL-query](#bkmk_wql)
        - [XPath-query](#bkmk_xpath)

    - **Gegevens type**: Kies de indeling waarin de voor waarde de gegevens retourneert voordat deze wordt gebruikt om de instelling te beoordelen. De lijst **gegevens type** wordt niet voor alle instellings typen weer gegeven.  

        > [!Tip]  
        > Het gegevens type **drijvende** komma ondersteunt slechts drie cijfers na het decimaal teken.  

3. Configureer aanvullende informatie over deze instelling onder de lijst **Instellingstype**. De items die u kunt configureren variëren afhankelijk van het instellings type dat u hebt geselecteerd.  

4. Selecteer **OK** om de instelling op te slaan en het dialoog venster **instelling maken** te sluiten.  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a>Active Directory query

- **LDAP-voor voegsel**: Geef een geldig voor voegsel op voor de Active Directory Domain Services query om naleving op client computers te beoordelen. Als u een globale catalogus wilt zoeken, gebruikt u `LDAP://` of `GC://` .  

- **Distinguished name (DN)**: Geef de DN-naam op van het Active Directory Domain Services-object dat wordt beoordeeld op naleving op client computers.  

- **Zoek filter**: Geef een optioneel LDAP-filter op om de resultaten van de Active Directory Domain Services query te verfijnen om de compatibiliteit op client computers te beoordelen. Als u alle resultaten van de query wilt retour neren, voert u in `(objectclass=*)` .  

- **Zoek bereik**: Geef het zoek bereik op in Active Directory Domain Services  

    - **Base**: alleen query's uitvoeren op het opgegeven object  

    - **Eén niveau**: deze optie wordt niet gebruikt in deze versie van Configuration Manager  

    - **Substructuur**: query's uitvoeren op het opgegeven object en de volledige substructuur in de Directory  

- **Eigenschap**: Geef de eigenschap op van het Active Directory Domain Services-object dat wordt gebruikt om de naleving op client computers te beoordelen.  

    Als u bijvoorbeeld een query wilt uitvoeren op de eigenschap Active Directory waarmee het aantal keren dat een gebruiker onjuist een wacht woord invoert, invoert, voert u `badPwdCount` in dit veld in.  

- **Query**: geeft de query weer die is samengesteld op basis van de vermeldingen in **LDAP-voor voegsel**, **DN-naam**, **Zoek filter** (indien opgegeven) en **eigenschap**.  


### <a name="assembly"></a><a name="bkmk_assembly"></a>Assemblage

Een assembly is een stuk code dat tussen toepassingen kan worden gedeeld. Assembly's kunnen de bestandsnaamextensie .dll of .exe hebben. De Global Assembly Cache is de map `%SystemRoot%\Assembly` op client computers. Deze cache is de plek waar Windows alle gedeelde assembly's opslaat.  

- **Naam van assembly**: hier geeft u de naam op van het assembly-object waarnaar u wilt zoeken. De naam kan niet hetzelfde zijn als andere assembly-objecten van hetzelfde type. Registreer deze eerst in de Global Assembly Cache. De assembly-naam mag maximaal 256 tekens lang zijn.  


### <a name="file-system"></a><a name="bkmk_file"></a>Bestands systeem

- **Type**: Selecteer in de lijst of u wilt zoeken naar een **bestand** of een **map**.  

- **Pad**: Geef het pad op naar het opgegeven bestand of de map op client computers. U kunt in het pad systeem omgevingsvariabelen en de `%USERPROFILE%` omgevings variabele opgeven.  

    > [!NOTE]  
    > Als u de `%USERPROFILE%` omgevings variabele gebruikt in het vak **pad** of **bestand of mapnaam** , zoekt de Configuration Manager-client alle gebruikers profielen op de client computer. Dit gedrag kan ertoe leiden dat er meerdere exemplaren van het bestand of de map worden gevonden.  
    >   
    > Als nalevings instellingen geen toegang tot het opgegeven pad hebben, wordt er een detectie fout gegenereerd. Er wordt ook een detectiefout gegenereerd als het bestand dat u zoekt momenteel in gebruik is.  

    > [!Tip]  
    > Selecteer **Bladeren** om de instelling te configureren op basis van waarden op een referentie computer.   

- **Bestands-of mapnaam**: Geef de naam op van het bestand of het mapobject waarnaar moet worden gezocht. U kunt systeem omgevingsvariabelen en de `%USERPROFILE%` omgevings variabele opgeven in de naam van het bestand of de map. U kunt ook de joker tekens `*` en `?` de naam van het bestand gebruiken.  

    > [!NOTE]  
    > Als u de naam van een bestand of map opgeeft en Joker tekens gebruikt, kan deze combi natie een groot aantal resultaten opleveren. Het kan ook leiden tot een hoog bron gebruik op de client computer en veel netwerk verkeer wanneer de resultaten worden gerapporteerd aan Configuration Manager.  

- **Inclusief submappen**: Doorzoek ook submappen onder het opgegeven pad.  

- **Dit bestand of deze map is gekoppeld aan een 64-bits toepassing**: als deze functie is ingeschakeld, worden alleen op 64-bits bestands locaties gezocht, zoals `%ProgramFiles%` op 64-bits computers. Als deze optie niet is ingeschakeld, zoekt u in zowel 64-bits als op 32-bits locatie, zoals `%ProgramFiles(x86)%` .  

    > [!NOTE]  
    > Als hetzelfde bestand of dezelfde map zowel op de 64-bits als op de 32-bits systeembestandslocatie van dezelfde 64-bits computer bestaat, worden meerdere bestanden gedetecteerd door de globale voorwaarde.  

    Het instellings type **Bestands systeem** biedt geen ondersteuning voor het opgeven van een UNC-pad naar een netwerk share in het vak **pad** .  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a>IIS-meta base

- **Metabasepad**: Geef een geldig pad op naar de meta base van de Internet Information Services (IIS). Bijvoorbeeld `/LM/W3SVC/`.  

- **Eigenschaps-id**: Geef de numerieke eigenschap van de IIS-meta base-instelling op.  


### <a name="registry-key"></a><a name="bkmk_regkey"></a>Register sleutel

- **Hive**: Selecteer de register component waarin u wilt zoeken

    > [!Tip]  
    > Selecteer **Bladeren** om de instelling te configureren op basis van waarden op een referentie computer. Als u wilt bladeren naar een register sleutel op een externe computer, schakelt u de **externe register** service op de externe computer in.  

- **Sleutel**: Geef de naam op van de register sleutel waarnaar u wilt zoeken. Gebruik de indeling `key\subkey`.  

- **Deze register sleutel is gekoppeld aan een 64-bits toepassing**: zoek in 64-bits register sleutels naast de 32-bits register sleutels op clients met een 64-bits versie van Windows.  

    > [!NOTE]  
    > Als dezelfde registersleutel zowel op de 64-bits als op de 32-bits registerlocatie van dezelfde 64-bits computer bestaat, worden beide registersleutels gedetecteerd door de globale voorwaarde.  


### <a name="registry-value"></a><a name="bkmk_regval"></a>Register waarde

- **Hive**: Selecteer het register onderdeel dat u wilt zoeken.  

    > [!Tip]  
    > Selecteer **Bladeren** om de instelling te configureren op basis van waarden op een referentie computer. Als u wilt bladeren naar een register waarde op een externe computer, schakelt u de **externe register** service op de externe computer in. U hebt ook beheerders machtigingen nodig voor toegang tot de externe computer.  

- **Sleutel**: Geef de naam op van de register sleutel waarnaar moet worden gezocht. Gebruik de indeling `key\subkey`.  

- **Waarde**: Geef de waarde op die moet worden opgenomen in de opgegeven register sleutel.  

- **Deze register sleutel is gekoppeld aan een 64-bits toepassing**: Zoek in de 64-bits register sleutels naast de 32-bits register sleutels op clients met een 64-bits versie van Windows.  

    > [!NOTE]  
    > Als dezelfde registersleutel zowel op de 64-bits als op de 32-bits registerlocatie van dezelfde 64-bits computer bestaat, worden beide registersleutels gedetecteerd door de globale voorwaarde.  


### <a name="script"></a><a name="bkmk_script"></a>Schriften

De geretourneerde waarde door het script wordt gebruikt om de naleving van de globale voorwaarde vast te stellen. Wanneer u bijvoorbeeld VBScript gebruikt, kunt u de opdracht **WScript.Echo Result** gebruiken om de variabele waarde *Result* te retourneren naar de globale voorwaarde.  

- **Detectie script**: Selecteer **script toevoegen**en voer of blader naar een script. Dit script wordt gebruikt om de waarde te vinden. U kunt Windows PowerShell-, VBScript- of Microsoft JScript-scripts gebruiken.  

- **Herstel script (optioneel)**: Selecteer **script toevoegen**en voer of blader naar een script. Dit script wordt gebruikt om niet-compatibele instellings waarden te herstellen. U kunt Windows PowerShell-, VBScript- of Microsoft JScript-scripts gebruiken.  

- **Scripts uitvoeren met de referenties van de aangemelde gebruiker**: als u deze optie inschakelt, wordt het script uitgevoerd op client computers die gebruikmaken van de referenties van de aangemelde gebruiker.  

> [!Note]  
> Vanaf versie 1810, wanneer u Windows Power shell als een script voor detectie of herstel gebruikt, roept de Configuration Manager-client Power shell aan met de `-NoProfile` para meter. Met deze optie wordt Power shell zonder profielen gestart. Een Power shell-profiel is een script dat wordt uitgevoerd wanneer Power shell wordt gestart. <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a>SQL-query

- **SQL Server exemplaar**: Kies of u de SQL-query wilt uitvoeren op het standaard exemplaar, alle exemplaren of een opgegeven naam van een Data Base-exemplaar.  

    > [!NOTE]  
    > De naam van het exemplaar moet verwijzen naar een lokaal exemplaar van de SQL Server. Gebruik een scriptinstelling om te verwijzen naar een geclusterd SQL server-exemplaar.  

- **Data Base**: Geef de naam op van de Microsoft SQL Server Data Base waarvoor u de SQL-query wilt uitvoeren.  

- **Kolom**: Geef de naam op van de kolom die wordt geretourneerd door de Transact-SQL-instructie die wordt gebruikt om de compatibiliteit van de globale voor waarde vast te stellen.  

- **Transact-SQL-instructie**: Geef de volledige SQL-query op die u wilt gebruiken voor de globale voor waarde. Selecteer **openen**om een bestaande SQL-query te gebruiken.  

    > [!IMPORTANT]  
    > SQL-query-instellingen bieden geen ondersteuning voor SQL-opdrachten waarmee de data base wordt gewijzigd. U kunt alleen SQL-opdrachten gebruiken waarmee gegevens uit de database worden gelezen.  


### <a name="wql-query"></a><a name="bkmk_wql"></a>WQL-query

- **Naam ruimte**: Geef de WMI-naam ruimte op die wordt beoordeeld op naleving op client computers. De standaardwaarde is `root\cimv2`.  

- **Klasse**: Geef de WMI-doel klasse op in de bovenstaande naam ruimte.  

- **Eigenschap**: Geef de WMI-doel eigenschap in de bovenstaande klasse op.  

- **WHERE-component van WQL-query**: Geef een component kwalificeren op om de resultaten te verminderen. Als u bijvoorbeeld alleen de DHCP-service in de klasse Win32_Service wilt opvragen, zou de component WHERE kunnen zijn `Name = 'DHCP' and StartMode = 'Auto'` .   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a>XPath-query

- **Pad**: Geef het pad op naar het XML-bestand op client computers die wordt gebruikt om naleving te beoordelen. Configuration Manager ondersteunt het gebruik van alle Windows-systeem omgevingsvariabelen en de `%USERPROFILE%` gebruikers variabele in de naam van het pad.  

- **XML-bestands naam**: Geef de naam van het bestand op dat de XML-query bevat in het bovenstaande pad.  

- **Inclusief submappen**: Schakel deze optie in om submappen onder het opgegeven pad te doorzoeken.  

- **Dit bestand is gekoppeld aan een 64-bits toepassing**: zoeken naar de bestands locatie van het 64-bits systeem, `%Windir%\System32` naast de locatie van het 32-bits systeem bestand `%Windir%\Syswow64` op Configuration Manager clients met een 64-bits versie van Windows.  

- **XPath-query**: Geef een geldige volledige XML Path-taal (XPath)-query op.  

- **Naam ruimten**: Identificeer naam ruimten en voor voegsels die moeten worden gebruikt tijdens de XPath-query.  

Als u een versleuteld XML-bestand probeert te detecteren, vinden de instellingen voor naleving het bestand, maar levert de XPath-query geen resultaten op. De Configuration Manager-client genereert geen fout.  

Als de XPath-query ongeldig is, wordt de instelling geëvalueerd als niet-compatibel op client computers.  



##  <a name="configure-compliance-rules"></a>Compliantieregels configureren  

Met compliantieregels geeft u de voorwaarden voor naleving van een configuratie-item op. Voordat een instelling kan worden beoordeeld op naleving, moet de instelling minimaal één compliantieregel hebben. Met WMI-, register- en scriptinstellingen kunt u waarden herstellen die niet compliant zijn. U kunt nieuwe regels maken of naar een bestaande instelling in een configuratie-item bladeren om regels hierin te selecteren.  


### <a name="to-create-a-compliance-rule"></a>Een compliantieregel maken  

1. Selecteer op de pagina **compliantie regels** van de **wizard Configuratie-item maken**de optie **Nieuw**.  

2. Geef in het dialoogvenster **Regel maken** de volgende informatie op:  

    - **Naam**: Voer een naam in voor de nalevings regel.  

    - **Beschrijving**: Voer een beschrijving in voor de nalevings regel.  

    - **Geselecteerde instelling**: Selecteer **Bladeren** om het dialoog venster **instelling selecteren** te openen. Selecteer de instelling waarvoor u een regel wilt definiëren of selecteer **nieuwe instelling**. Wanneer u klaar bent, kiest u **selecteren**.  

        > [!Tip]  
        > Als u informatie over de geselecteerde instelling wilt weer geven, selecteert u **Eigenschappen**.  

    - **Regel type**: Selecteer het type nalevings regel dat u wilt gebruiken:  

        - **Waarde**: Maak een regel waarmee de waarde die door het configuratie-item wordt geretourneerd, wordt vergeleken met een waarde die u opgeeft. Zie [Value Rules](#bkmk_value)(Engelstalig) voor meer informatie over de aanvullende instellingen.  

        - **Existentieel**: Maak een regel die de instelling evalueert, afhankelijk van of deze op een client apparaat bestaat of op basis van het aantal keren dat deze wordt gevonden. Zie [existentieel-regels](#bkmk_exist)voor meer informatie over de aanvullende instellingen.  

3. Selecteer **OK** om het dialoog venster **regel maken** te sluiten.  




### <a name="value-rules"></a><a name="bkmk_value"></a>Waarde-regels  

- **Eigenschap**: de eigenschap van het object dat moet worden gecontroleerd, is afhankelijk van de geselecteerde instelling. De beschik bare eigenschappen variëren afhankelijk van het type instelling. 

- **De instelling moet voldoen aan het volgende...**: de beschik bare regels of machtigingen variëren op basis van het type instelling.

- **Regels die niet compliant zijn herstellen, indien ondersteund**: Selecteer deze optie voor Configuration Manager om niet-compatibele regels automatisch te herstellen. Configuration Manager ondersteunt deze actie met de volgende regel typen:  

    - **Register waarde**: als het niet-compatibel is, stelt de client de register waarde in. Als deze niet bestaat, wordt de waarde door de client gemaakt.  

    - **Script**: de client gebruikt het herstel script dat u hebt opgegeven bij de instelling.  

    - **WQL-query**  

    > [!IMPORTANT]  
    > U kunt niet-compatibele regels alleen herstellen als de regeloperator is ingesteld op **Is gelijk aan**.  

- **Niet-naleving melden als dit instellings exemplaar niet wordt gevonden**: als deze instelling niet op client computers wordt gevonden, schakelt u deze optie in voor het configuratie-item om niet-naleving te rapporteren.  

- **Ernst van niet-compliantie voor rapporten**: Geef de ernst op die in Configuration Manager rapporten wordt gerapporteerd als deze compliantie regel mislukt. De volgende Ernst niveaus zijn beschikbaar:  
    - **Geen**  
    - **Informatie**  
    - **Waarschuwing**  
    - **Kritiek**  
    - **Kritiek met gebeurtenis**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek**gerapporteerd. Dit ernstniveau wordt ook vastgelegd als een Windows-gebeurtenis in het logboek voor toepassingsgebeurtenissen.  


### <a name="existential-rules"></a><a name="bkmk_exist"></a>Existentieel-regels 

> [!NOTE]  
> De weer gegeven opties kunnen variëren afhankelijk van het instellings type waarvoor u een regel configureert.  

- **De instelling moet bestaan op clientapparaten**  

- **De instelling mag niet bestaan op clientapparaten**  

- **De instelling komt het volgende aantal keren voor:**  

- **Ernst van niet-compliantie voor rapporten**: Geef de ernst op die in Configuration Manager rapporten wordt gerapporteerd als deze compliantie regel mislukt. De volgende Ernst niveaus zijn beschikbaar:  
    - **Geen**  
    - **Informatie**  
    - **Waarschuwing**  
    - **Kritiek**  
    - **Kritiek met gebeurtenis**: voor computers die niet voldoen aan deze compliantie regel wordt de fout Ernst **kritiek**gerapporteerd. Dit ernstniveau wordt ook vastgelegd als een Windows-gebeurtenis in het logboek voor toepassingsgebeurtenissen.  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a>Herbemiddelingen van configuratie-items bijhouden
<!--4261411-->
*(Geïntroduceerd in versie 2002)*

Vanaf Configuration Manager versie 2002 kunt u de **herstel geschiedenis volgen wanneer** deze wordt ondersteund in de nalevings regels van uw configuratie-item. Wanneer deze optie is ingeschakeld, genereert een herstel dat zich voordoet op de client voor het configuratie-item een status bericht. De geschiedenis wordt opgeslagen in de Configuration Manager-Data Base.

Aangepaste rapporten bouwen om de herstel geschiedenis weer te geven met behulp van de open bare weer gave **v_CIRemediationHistory**. De `RemediationDate` kolom is de tijd, in UTC, die door de client is uitgevoerd. `ResourceID`Hiermee wordt het apparaat geïdentificeerd. Door aangepaste rapporten te bouwen met de **v_CIRemediationHistory** weer gave kunt u het volgende doen:

- Mogelijke problemen met uw herstel scripts identificeren
- Vind trends in herbemiddelingen, zoals een-client, die consistent niet-naleving van elke evaluatie cyclus zijn.

### <a name="enable-the-track-remediation-history-when-supported-option"></a>Schakel de optie herstel geschiedenis bijhouden wanneer ondersteund

- Voor nieuwe configuratie-items, voegt u de optie **herstel geschiedenis bijhouden wanneer ondersteund** op het tabblad **nalevings regels** wanneer u een nieuwe instelling op de pagina **instellingen** van de wizard maakt.
- Voor bestaande configuratie-items, voegt u de optie **herstel geschiedenis bijhouden wanneer ondersteund** op het tabblad **nalevings regels** in de **Eigenschappen**van het configuratie-item.
[![Herstel geschiedenis bijhouden wanneer ondersteund in versie 2002](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>Volgende stappen

[Configuratiebasislijnen maken](create-configuration-baselines.md)
