---
title: Query's maken
titleSuffix: Configuration Manager
description: Ontdek hoe u query's maakt en importeert in Configuration Manager. Bevat voorbeeld query's en tips.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05b77fa181da67858c30f48fc8045c20384953ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720091"
---
# <a name="create-queries-in-configuration-manager"></a>Query's maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel wordt beschreven hoe u query's maakt en importeert in Configuration Manager.  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a>Een query maken  
 Gebruik deze procedure voor het maken van een query in Configuration Manager.  

1.  Selecteer **bewaking**In de Configuration Manager-console.  

2.  Selecteer in de werk ruimte **bewaking** de optie **query's**. Klik op het tabblad **Start** in de groep **maken** op **query maken**.  

3.  Geef op het tabblad **Algemeen** van de **wizard query maken**een unieke naam en eventueel een opmerking voor de query op.  

4.  Als u een bestaande query wilt importeren om te gebruiken als basis voor de nieuwe query, selecteert u **query-instructie importeren**. Selecteer in het dialoog venster **Blader query** een query die u wilt importeren en selecteer vervolgens **OK**.  

5.  Selecteer in de lijst **object type** het type object dat u wilt dat de query retourneert. In deze tabel worden enkele voor beelden van de typen objecten beschreven waarnaar u kunt zoeken:  

    |Objecttype|Beschrijving|  
    |-----------------|-----------------|  
    |**Systeembron**|Gebruik dit om te zoeken naar typische systeem kenmerken, zoals de NetBIOS-naam van een apparaat, de client versie, het IP-adres van de client en Active Directory Domain Services informatie.|  
    |**Gebruikersresource**|Gebruik dit om te zoeken naar typische gebruikers informatie, zoals gebruikers namen, namen van gebruikers groepen en namen van beveiligings groepen.|  
    |**Implementatie**|Gebruik dit om te zoeken naar typische kenmerken van een implementatie, zoals de implementatie naam, het schema en de verzameling waarin deze is geïmplementeerd.|  

6.  Selecteer **query-instructie bewerken** om het &lt;dialoog venster\> **Eigenschappen** van query naam overzicht te openen.  

7.  Geef op het tabblad **Algemeen** van &lt;het dialoog\> venster Eigenschappen van query naam **instructie** de kenmerken op die de query retourneert en hoe deze moeten worden weer gegeven. Selecteer het pictogram **Nieuw** om een nieuw kenmerk toe te voegen. U kunt ook **query taal weer geven** selecteren om de query rechtstreeks in WMI Query Language (WQL) in te voeren of te bewerken. Voor voor beelden van WMI-query's raadpleegt u de sectie [voor beeld WQL-query's](#BKMK_Example) in dit artikel.  

    > [!TIP]  
    > U kunt de volgende referentie documentatie gebruiken om u te helpen bij het bouwen van uw eigen WQL-query's:  
    >   
    > -   [WQL (SQL voor WMI)](https://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [WHERE-component](https://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [WQL-operators](https://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Op het tabblad **criteria** van het &lt;dialoog venster\> **Eigenschappen** van query naam instructie geeft u criteria op die worden gebruikt om de resultaten van de query te verfijnen. U kunt bijvoorbeeld alleen resources met de site code **xyz**retour neren. U kunt meerdere criteria voor een query configureren.  

    > [!IMPORTANT]  
    > Als u een query zonder criteria maakt, retourneert de query alle apparaten in de verzameling **Alle systemen** .  

9. Op het tabblad **samen voegingen** van &lt;het dialoog\> venster Eigenschappen van query naam **instructie** kunt u gegevens van twee verschillende kenmerken combi neren in de query resultaten. Hoewel Configuration Manager automatisch query-samen voegen maakt wanneer u verschillende kenmerken voor het query resultaat kiest, biedt het tabblad **samen voegingen** meer geavanceerde opties. Configuration Manager ondersteunt deze kenmerk klassen:  

    |Relatietype|Beschrijving|  
    |---------------|-----------------|  
    |Binnen|Alleen overeenkomende resultaten weer gegeven. Wordt altijd gebruikt door samen voegingen die automatisch worden gemaakt.|  
    |Links|Geeft alle resultaten voor het basiskenmerk weer en alleen de overeenkomende resultaten voor het samenvoegingskenmerk.|  
    |Rechts|Geeft alle resultaten voor het samenvoegings kenmerk en alleen de overeenkomende resultaten voor het basis kenmerk.|  
    |Volledig|Geeft alle resultaten weer voor zowel het basis kenmerk als het samenvoegings kenmerk.|  

     Zie de SQL Server-documentatie voor meer informatie over het gebruik van koppelings bewerkingen.  

10. Selecteer **OK** om het dialoog &lt;venster Eigenschappen\> van de query naam **instructie** te sluiten.  

11. Op het tabblad **Algemeen** van de **wizard query maken**geeft u op dat de resultaten van de query niet beperkt zijn tot de leden van een verzameling, dat ze beperkt zijn tot de leden van een opgegeven verzameling of dat een prompt voor een verzameling wordt weer gegeven telkens wanneer de query wordt uitgevoerd.  

12. Voltooi de wizard om de query te maken. De nieuwe query wordt weer gegeven in het knoop punt **query's** in de werk ruimte **bewaking** .  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a>Een query importeren  
 Gebruik deze procedure voor het importeren van een query in Configuration Manager. Zie [query's beheren](../../../core/servers/manage/manage-queries.md)voor meer informatie over het exporteren van query's.  

1.  Selecteer **bewaking**In de Configuration Manager-console.  

2.  Selecteer in de werk ruimte **bewaking** de optie **query's**. Selecteer op het tabblad **Start** in de groep **maken** de optie **objecten importeren**.  

3.  Selecteer op de pagina **MOF-bestands naam** van de **wizard objecten importeren**de optie **Bladeren** om het MOF-bestand (Managed Object Format) te selecteren dat de query bevat die u wilt importeren.  

4.  Bekijk de informatie over de query die u wilt importeren en voltooi vervolgens de wizard. De nieuwe query wordt weer gegeven in het knoop punt **query's** in de werk ruimte **bewaking** .  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries

Deze sectie bevat voor beelden van WQL-query's die u kunt gebruiken in uw hiërarchie of voor andere doel einden wijzigen. Als u deze query's wilt gebruiken, selecteert u **query taal weer geven** in het dialoog venster **Eigenschappen query-instructie** . Kopieer en plak de query vervolgens in het veld **query-instructie** .  

> [!TIP]  
> Gebruik het jokerteken `%` om willekeurige tekenreeks aan te geven. `%Visio%` Retourneert bijvoorbeeld Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-10"></a>Computers met Windows 10

Gebruik de volgende query om de NetBIOS-naam en besturingssysteemversie te retourneren van alle computers met Windows 7.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computers met een specifiek softwarepakket geïnstalleerd  

Gebruik de volgende query om de NetBIOS-naam en softwarepakketnaam te retourneren van alle computers waarop een specifiek softwarepakket is geïnstalleerd. In dit voor beeld worden alle computers weer gegeven waarop een versie van micro soft Visio is geïnstalleerd. Vervang `Microsoft%Visio%` door het software pakket waarvoor u een query wilt uitvoeren.  

> [!TIP]  
> Deze query zoekt naar het softwarepakket op basis van de namen die worden weergegeven in de lijst met programma's in het Configuratiescherm.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Computers in een specifieke Active Directory Domain Services organisatie-eenheid

Gebruik de volgende query om de NetBIOS-naam en de naam van de organisatie-eenheid (OE) te retour neren van alle computers in een opgegeven organisatie-eenheid. Vervang de tekst `OU Name` door de naam van de organisatie-eenheid waarvoor u een query wilt uitvoeren.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computers met een specifieke NetBIOS-naam

Gebruik de volgende query om de NetBIOS-naam te retourneren van alle computers die met een specifieke tekenreeks beginnen. In dit voor beeld retourneert de query alle computers met een NetBIOS-naam die begint `ABC`met.  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Apparaten van een bepaald type

Apparaattypen worden opgeslagen in de Configuration Manager-Data Base onder de resource klasse **SMS_R_System** en de kenmerk naam **AgentEdition**. Gebruik deze query om alleen de apparaten op te halen die overeenkomen met de agent editie van het apparaattype dat u opgeeft:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Gebruik een van de volgende waarden &lt;voor de\>apparaat-id:  

|Apparaattype|Waarde van AgentEdition|  
|-----------------|---------------------------|  
|Windows-bureau blad of laptop computer|0|  
|Windows ARM-apparaat (waarop Windows RT wordt uitgevoerd)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac-computer|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Intel-systeem op een chip|12|  
|UNIX- en Linux-servers|13|  
|Micro soft HoloLens (MDM)|15|
|Micro soft Surface Hub (MDM)|16|

> [!NOTE]
> Waarden die niet in deze tabel worden vermeld, zijn gekoppeld aan apparaten die niet meer worden ondersteund.

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

Als u bijvoorbeeld alleen Mac-computers wilt retour neren, gebruikt u deze query:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Volgende stappen

[Query's beheren](manage-queries.md)
