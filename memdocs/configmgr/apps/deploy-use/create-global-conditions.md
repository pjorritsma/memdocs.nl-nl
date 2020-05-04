---
title: Globale voorwaarden maken
titleSuffix: Configuration Manager
description: Globale voor waarden maken om op te geven hoe een toepassing wordt opgegeven en geïmplementeerd op client apparaten.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ae27e50e5093d7443c35df33b1757caec6086627
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710284"
---
# <a name="how-to-create-global-conditions-in-configuration-manager"></a>Globale voor waarden maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In Configuration Manager zijn globale voor waarden regels die zakelijke of technische voor waarden Voorst Ellen die u kunt gebruiken om op te geven hoe een toepassing wordt opgegeven en geïmplementeerd op client apparaten. Globale voorwaarden worden geopend via de pagina **Vereisten** van de wizard Implementatietype maken.  

> [!NOTE]  
>  U kunt globale voor waarden alleen bewerken op de site waar ze zijn gemaakt.  

 Gebruik de volgende procedures om Configuration Manager globale voor waarden te maken.  

## <a name="provide-basic-information-about-the-global-condition"></a>Algemene gegevens over de globale voorwaarde opgeven  
 Verschillende soorten globale voorwaarden zijn beschikbaar. Verschillende opties zijn gekoppeld aan de verschillende typen globale voorwaarden. Wanneer u een specifiek type globale voor waarde selecteert, worden in Configuration Manager de opties weer gegeven die op uw selectie van toepassing zijn.  

1.  Kies **software bibliotheek** > **toepassings beheer** > **globale voor waarden**in de Configuration Manager-console.  

3.  Kies op het tabblad **Start** in de groep **maken** de optie **globale voor waarde maken**.  

4.  Geef in het dialoogvenster **Globale voorwaarde maken** een naam op en een optionele beschrijving voor de globale voorwaarde.  

5.  Kies in de vervolg keuzelijst **Apparaattype** of de globale voor waarde geldt voor een **Windows** -computer of een **Windows Mobile** -apparaat.  

6.  Kies in het vervolgkeuzemenu **Voorwaardetype** een van de volgende opties:  

    -   **Instelling** – Met deze optie kunt u controleren of er sprake is van een of meerdere items op clientapparaten. U kunt bijvoorbeeld controleren of een bestand, map of register sleutel waarde bestaat op een client apparaat.  

    -   **Expressie** – met deze optie kunt u complexere regels instellen om te controleren of aan de voor waarde is voldaan op client apparaten. U kunt bijvoorbeeld controleren of het fysieke geheugen op een computer tussen 2 GB en 4 GB ligt, of dat een mobiel apparaat invoer met een aanraak scherm gebruikt.  

## <a name="set-up-rules-for-the-global-condition"></a>Regels instellen voor de globale voor waarde  
 De procedure voor het definiëren van de regels voor globale voor waarden is anders, afhankelijk van of u een instelling of een expressie configureert. Gebruik de toepasselijke procedure om een instelling of een expressie in te stellen voor de globale voor waarde.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Instellen van een instelling voor de globale voor waarde  

1. Kies in het vervolgkeuzemenu **Voorwaardetype****Instelling**.  

2. Kies in het vervolgkeuzemenu **Instellingstype** het item dat u wilt gebruiken als de voorwaarde waarvoor u vereisten wilt controleren. De volgende instellings typen en configuraties zijn beschikbaar.  

   - **Active Directory-query**  

     -   **LDAP-voorvoegsel** - Geef een geldig LDAP-voorvoegsel op in de Active Directory Domain Services-query om de compatibiliteit vast te stellen op clientcomputers. U kunt **LDAP://** of **GC://** gebruiken.  

     -   **Distinguished name (DN)** : Geef de DN-naam op van het Active Directory Domain Services-object dat wordt beoordeeld op naleving op client computers.  

     -   **Zoekfilter**: Geef een optionele LDAP-filter op om de resultaten van de Active Directory Domain Services-query te verfijnen om de compatibiliteit vast te stellen op clientcomputers.  

     -   **Zoekbereik** - Geef het zoekbereik op in Active Directory Domain Services:  

         -   **Base** -alleen query's uitvoeren op het opgegeven object.  

         -   **Eén niveau** : deze optie wordt niet gebruikt in deze versie van Configuration Manager.  

         -   **Substructuur** : Hiermee vraagt u het opgegeven object en de volledige substructuur in de directory op.  

     -   **Eigenschap** - Hier specificeert u de eigenschap van een Active Directory Domain Services-object dat wordt gebruikt om de compatibiliteit vast te stellen op clientcomputers.  

     -   **Query** -geeft de LDAP-query weer die is samengesteld op basis van de vermeldingen in **LDAP-voor voegsel**, **DN (Distinguished Name)**, **Zoek filter** indien opgegeven en **eigenschap**. Deze query wordt gebruikt om de compatibiliteit vast te stellen op clientcomputers.  

   - **Assembly**  

     -   **Naam van assembly** - Hier geeft u de naam op van het assembly-object waarnaar u wilt zoeken. De naam kan niet hetzelfde zijn als een ander Assembly-object van hetzelfde type en de naam moet zijn geregistreerd in de globale assembly-cache. De assembly naam mag Maxi maal 256 tekens lang zijn.  

     > [!NOTE]  
     >  Een assembly is een stuk code dat tussen toepassingen kan worden gedeeld. Assembly's kunnen de bestandsnaam extensie. dll of. exe hebben. De Global Assembly-cache is een map met de naam *%systemroot%\assembly* op clientcomputers waarin alle gedeelde assembly's zijn opgeslagen.  

   - **Bestands systeem**  

     - **Type** : Kies in de vervolg keuzelijst of u wilt zoeken naar een **bestand** of een **map**.  

     - **Pad** - Geef het pad op naar het gespecificeerde bestand of de map op clientcomputers. U kunt in het pad systeemomgevingsvariabelen specificeren en de *%USERPROFILE%*-omgevingsvariabele.  

       > [!NOTE]  
       >  Als u de *%USERPROFILE%* -omgevingsvariabele gebruikt in het **Pad** of in de velden **Bestands- of mapnaam** , wordt in alle gebruikersprofielen op de clientcomputer gezocht. Dit kan leiden tot het vinden van meerdere exemplaren van het bestand of de map.  

     - **Bestands- of mapnaam** - Geef de naam op van het bestand of het mapobject waarnaar moet worden gezocht. U kunt in de bestands- of map naam systeemomgevingsvariabelen specificeren en de *%USERPROFILE%*-omgevingsvariabele. U kunt ook de * en gebruiken? Joker tekens in de bestands naam.  

       > [!NOTE]  
       >  Als u een bestands- of mapnaam opgeeft en hierbij jokertekens gebruikt, kunt u een groot aantal resultaten krijgen. Dit kan leiden tot een hoog bron gebruik op de client computer en veel netwerk verkeer wanneer de resultaten worden gerapporteerd aan Configuration Manager.  

     - **Inclusief submappen**: schakel deze optie in als u in submappen wilt zoeken onder het opgegeven pad.  

     - **Dit bestand of deze map is gekoppeld aan een 64-bits toepassing** : Kies of de 64-bits systeem bestands locatie (*% windir%* \System32) moet worden doorzocht naast de 32-bits systeem bestands locatie (*% windir%* \syswow64) op Configuration Manager clients waarop een 64-bits versie van Windows wordt uitgevoerd.  

       > [!NOTE]  
       >  Als hetzelfde bestand of dezelfde map bestaat in zowel de 64-bits als de 32-bits systeembestandslocatie op dezelfde 64-bits computer, worden door de globale voorwaarde meerdere bestanden gevonden.  

       Het instellingstype **Bestandssysteem** ondersteunt geen specificatie van een UNC-pad naar een netwerkshare in het veld **Pad** .  

   - **IIS Metabase**  

     -   **Metabasepad** - Geef een geldig pad op naar de IIS Metabase.  

     -   **Eigenschaps-id** - Geef de numerieke eigenschap op van de IIS Metabase-instelling.  

   - **Registersleutel**  

     -   **Hive** : Kies in de vervolg keuzelijst de register component waarin u wilt zoeken.  

     -   **Sleutel**: specificeer de naam van de registersleutel waarnaar u wilt zoeken. De gebruikte indeling moet *sleutel\subsleutel*zijn.  

     -   **Deze registersleutel is gekoppeld aan een 64-bits toepassing** - Hiermee geeft u op of de 64-bits registersleutels moeten worden doorzocht naast de 32-bits registersleutels op clients die worden uitgevoerd op een 64-bits versie van Windows.  

         > [!NOTE]  
         >  Als hetzelfde bestand of dezelfde map bestaat in zowel de 64-bits als de 32-bits systeembestandslocatie op dezelfde 64-bits computer, worden door de globale voorwaarde meerdere bestanden gevonden.  

   - **Register waarde**  

     -   **Component** - Selecteer in de vervolgkeuzelijst de registercomponent waarin u wilt zoeken.  

     -   **Sleutel**: specificeer de naam van de registersleutel waarnaar u wilt zoeken. De gebruikte indeling moet *sleutel\subsleutel*zijn.  

     -   **Waarde**: specificeer de waarde die moet zijn opgenomen in de opgegeven registersleutel.  

     -   **Deze registersleutel is gekoppeld aan een 64-bits toepassing** - Hiermee geeft u op of de 64-bits registersleutels moeten worden doorzocht naast de 32-bits registersleutels op clients die worden uitgevoerd op een 64-bits versie van Windows.  

         > [!NOTE]  
         >  Als hetzelfde bestand of dezelfde map bestaat in zowel de 64-bits als de 32-bits systeembestandslocatie op dezelfde 64-bits computer, worden door de globale voorwaarde meerdere bestanden gevonden.  

   - **Schriften**  

     -   **Detectie script** : Kies **toevoegen** om in te voeren of blader naar het script dat u wilt gebruiken. U kunt Windows Power shell-, VBScript-of JScript-scripts gebruiken.  

     -   **Scripts uitvoeren met de referenties van de aangemelde gebruiker** – als u deze optie inschakelt, wordt het script uitgevoerd op client computers met behulp van de referenties van de gebruiker die is aangemeld.  

         > [!NOTE]  
         >  De waarde die het script heeft geretourneerd wordt gebruikt om de compatibiliteit vast te stellen van de globale voorwaarde. Wanneer u bijvoorbeeld VBScript gebruikt, kunt u de opdracht **WScript. echo result** gebruiken om de variabele waarde resultaat te retour neren naar de globale voor waarde.  
         >   
         >  Als uw script meerdere waarden retourneert, moeten deze waarden op één regel staan, gescheiden door een punt komma. Als iedere waarde op een afzonderlijke regel staat, mislukt de evaluatie.  

   - **SQL-query**  

     -   **SQL Server-exemplaar** – Kies of u de SQL-query wilt uitvoeren op het standaardexemplaar, alle exemplaren of op de naam van een specifiek database-exemplaar.  

         > [!NOTE]  
         >  De naam van het exemplaar moet verwijzen naar een lokaal exemplaar van de SQL Server. Gebruik een scriptinstelling om te verwijzen naar een geclusterd SQL server-exemplaar.  

     -   **Database** - Geef de naam op van de Microsoft SQL Server-database waarvoor u de SQL query wilt uitvoeren.  

     -   **Kolom** - Geef de naam van de kolom op die door de Transact-SQL-instructie is geretourneerd om de compatibiliteit vast te stellen van de globale voorwaarde.  

     -   **Transact-SQL-instructie** – Geef de volledige SQL-query op die u wilt gebruiken voor de globale voorwaarde. U kunt ook **openen** selecteren om een bestaande SQL-query te openen.  

   - **WQL-query**  

     -   **Naamruimte** - Specificeer de WMI-naamruimte die wordt gebruikt om een WQL-query samen te stellen waarvoor de compatibiliteit op clientcomputers wordt vastgesteld. De standaardwaarde is Root\cimv2.  

     -   **Klasse** - Hier geeft u de WMI-klasse op die wordt gebruikt om een WQL-query samen te stellen waarvoor de compatibiliteit op clientcomputers wordt vastgesteld.  

     -   **Eigenschap** - Hier geeft u de WMI-eigenschap op die wordt gebruikt om een WQL-query samen te stellen waarvoor de compatibiliteit op clientcomputers wordt vastgesteld.  

     -   **WHERE-component van WQL-query** - U kunt het item **WHERE-component van WQL-query** gebruiken om een WHERE-component te specificeren die moet worden toegepast op de opgegeven naamruimte en de eigenschap op clientcomputers.  

   - **XPath-query**  

     -   **Pad** - Geef het pad op naar het XML-bestand op clientcomputers die worden gebruikt om compatibiliteit te beoordelen. Configuration Manager ondersteunt het gebruik van alle Windows-systeem omgevingsvariabelen en de *% userprofile%* -gebruikers variabele in de naam van het pad.  

     -   **XML-bestands naam** : Geef de naam van het bestand op dat de XML-query bevat die moet worden gebruikt om de naleving op client computers te beoordelen.  

     -   **Inclusief submappen** : Schakel deze optie in als u ook in submappen wilt zoeken onder het opgegeven pad.  

     -   **Dit bestand is gekoppeld aan een 64-bits toepassing** : Kies of de 64-bits systeem bestands locatie (*% windir%* \System32) moet worden doorzocht naast de 32-bits systeem bestands locatie (*% windir%* \syswow64) op Configuration Manager clients waarop een 64-bits versie van Windows wordt uitgevoerd.  

     -   **XPath-query** - Geef een geldig volledige XML Path-taal (XPath)-query om de compatibiliteit op clientcomputers vast te stellen.  

     -   **Naamruimten** - Hiermee opent u het dialoogvenster **XML-naamruimten** om naamruimten en voorvoegsels te identificeren voor gebruik tijdens de XPath-query.  

3. Kies in de vervolgkeuzelijst **Gegevenstype** de indeling waarin de gegevens worden geretourneerd door de voorwaarde voordat deze wordt gebruikt om vereisten te controleren.  

   > [!NOTE]  
   >  De vervolg keuzelijst **gegevens type** wordt niet voor alle instellings typen weer gegeven.  

4. Stel meer informatie in over deze instelling onder de vervolg keuzelijst **instellings type** . De items die u kunt instellen, variëren afhankelijk van het instellings type dat u hebt geselecteerd.  

5. Kies **OK** om de regel op te slaan en het dialoog venster **globale voor waarde maken** te sluiten.  

### <a name="set-up-an-expression-for-the-global-condition"></a>Een expressie voor de globale voor waarde instellen  

1.  Kies in de vervolgkeuzelijst **Voorwaardetype****Instelling**.  

2.  Kies **component toevoegen** om het dialoog venster **component toevoegen** te openen.  

3.  Selecteer in de vervolgkeuzelijst **Categorie selecteren** of deze expressie voor een apparaat of voor een gebruiker is bedoeld. U kunt ook **Aangepast** selecteren om een vooraf geconfigureerde globale voorwaarde te gebruiken.  

4.  Selecteer in de vervolgkeuzelijst **Selecteer een voorwaarde** de voorwaarde die moet worden gebruikt om vast te stellen of de gebruiker of het apparaat voldoet aan de regelvereisten. De inhoud van deze lijst varieert op basis van de geselecteerde categorie.  

5.  Selecteer in de vervolgkeuzelijst **Operator kiezen** de operator die wordt gebruikt om de geselecteerde voorwaarde te vergelijken met de opgegeven waarde om vast te stellen of de gebruiker of het apparaat aan de regelvereisten voldoet. De beschikbare operators variëren op basis van de geselecteerde voorwaarde.  

6.  Voer in het veld **Waarde** de waarden in die worden gebruikt met de geselecteerde voorwaarde en operator om vast te stellen of de gebruiker of het apparaat voldoet aan de regelvereisten. De beschikbare waarden variëren op basis van de geselecteerde voorwaarde en de geselecteerde operator.  

7.  Kies **OK** om de expressie op te slaan en het dialoog venster **component toevoegen** te sluiten.  

8.  Wanneer u klaar bent met het toevoegen van componenten aan de globale voor waarde, klikt u op **OK** om het dialoog venster **globale voor waarde maken** te sluiten en de globale voor waarde op te slaan.  
