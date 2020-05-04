---
title: Pakketdefinitiebestanden
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van pakket definitie bestanden voor het maken van pakketten en Program ma's in Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710137"
---
# <a name="package-definition-files"></a>Pakketdefinitiebestanden

*Van toepassing op: Configuration Manager (huidige vertakking)*

Pakket definitie bestanden zijn scripts die u helpen bij het automatiseren van het maken van [pakketten en Program ma's](packages-and-programs.md) in Configuration Manager. Ze bieden alle informatie die Configuration Manager nodig heeft om een pakket en programma te maken, met uitzonde ring van de locatie van pakket bron bestanden.

## <a name="about-the-package-definition-file-format"></a>Over de Package Definition File-indeling

Elk Package Definition File is een ASCII-of UTF-8-tekst bestand dat de ini-bestands indeling gebruikt. Het bevat de volgende secties:  

### <a name="pdf"></a>[PDF]

Deze sectie geeft het bestand aan als een pakketdefinitiebestand. De sectie bevat de volgende informatie:  

- **Versie**: Geef de versie op van de Package Definition File indeling die het bestand gebruikt. Deze versie komt overeen met de versie van Configuration Manager waarvoor deze is geschreven. Dit item is vereist.  

### <a name="package-definition"></a>[Package Definition]

Geef de eigenschappen van het pakket en programma op. Het rapport bevat de volgende informatie:  

- **Name**: de naam van het pakket, maximaal 50 tekens.  

- **Versie** (optioneel): de versie van het pakket, maxi maal 32 tekens.  

- **Pictogram** (optioneel): het bestand dat het pictogram bevat dat voor dit pakket moet worden gebruikt. Indien opgegeven, vervangt dit pictogram het standaard pakket pictogram in de Configuration Manager-console.

- **Publisher**: de uitgever van het pakket, maximaal 32 tekens.

- **Language**: de taalversie van het pakket, maximaal 32 tekens.

- **Opmerking** (optioneel): een opmerking over het pakket, maxi maal 127 tekens.

- **ContainsNoFiles**: deze vermelding geeft aan of het pakket bron bestanden bevat.  

- **Program ma's**: de Program ma's die u voor dit pakket definieert. Elke programmanaam komt overeen met een sectie **[Program]** in dit pakketdefinitiebestand.  

    Voorbeeld:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: de naam van het MIF-bestand (Management Information Format) dat de pakketstatus bevat, maximaal 50 tekens.  

- **MIFName**: de naam van het pakket voor MIF dat overeenkomt met maxi maal 50 tekens.  

- **MIFVersion**: het versie nummer van het pakket voor MIF dat overeenkomt met maxi maal 32 tekens.  

- **MIFPublisher**: de software-uitgever van het pakket voor MIF dat overeenkomt met maxi maal 32 tekens.  

### <a name="program"></a>[Program]

Neem een sectie [Program] op voor elk programma dat u opgeeft in het item **Program ma's** in de sectie **[Package Definition]** . In deze sectie wordt elk programma gedefinieerd. Elk programma sectie bevat de volgende informatie:  

- **Name**: de naam van het programma, maximaal 50 tekens. Dit item moet uniek zijn binnen een pakket.  

- **Pictogram** (optioneel): Geef het bestand op dat het pictogram bevat dat moet worden gebruikt voor dit programma. Dit pictogram vervangt het standaard programma pictogram in de Configuration Manager-console. De client geeft ook dit pictogram weer wanneer u het programma implementeert in een verzameling.

- **Opmerking** (optioneel): een opmerking over het programma, maxi maal 127 tekens.

- **Commandline**: Geef de opdracht regel voor het programma op, maxi maal 127 tekens. De opdracht is relatief ten opzichte van de pakketbronmap.

- **StartIn**: Geef de werkmap voor het programma op, maxi maal 127 tekens. Dit item kan een absoluut pad op de client computer zijn of een pad dat relatief is ten opzichte van de bronmap van het pakket.

- **Uitvoeren**: Geef de programma modus op waarin het programma wordt uitgevoerd. U kunt **Minimized** (Geminimaliseerd), **Maximized** (Gemaximaliseerd) of **Hidden** (Verborgen) opgeven. Als u dit item niet opneemt, wordt het programma in de normale modus uitgevoerd.  

- **AfterRunning**: Geef een speciale actie op die plaatsvindt nadat het programma is voltooid. Beschikbare opties zijn **SMSRestart**, **ProgramRestart** en **SMSLogoff**. Als u deze vermelding niet opneemt, voert het programma geen speciale actie uit.  

- **EstimatedDiskSpace**: Geef de hoeveelheid schijf ruimte op die het software programma nodig heeft om op de computer te worden uitgevoerd. De standaard waarde is **onbekend**. U kunt de waarde instellen als een geheel getal dat groter is dan of gelijk is aan nul. Als u een waarde opgeeft, neemt u ook de eenheden voor de waarde op.  

    Voorbeeld:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**: Geef de geschatte duur in minuten op die u verwacht dat het programma wordt uitgevoerd op de client computer. De standaard waarde is **120**. U kunt de waarde instellen als een geheel getal groter dan nul of **onbekend**.  

    Voorbeeld:  

    `EstimatedRunTime=25`  

- **SupportedClients**: Geef de processors en besturings systemen op waarop dit programma wordt uitgevoerd. Scheid de platforms van elkaar door komma's. Als u deze vermelding niet opneemt, controleert de client niet de ondersteunde platforms voor dit programma.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Geef het begin-tot-eind bereik op voor de versie nummers van de besturings systemen die zijn opgegeven in de **SupportedClients** -vermelding.  

    Voorbeeld:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (optioneel): Geef alle andere informatie of vereisten voor client computers op, maxi maal 127 tekens.

- **CanRunWhen**: Geef de gebruikers status op die het programma nodig heeft om op de client computer te worden uitgevoerd. Beschikbare waarden zijn **UserLoggedOn**, **NoUserLoggedOn** en **AnyUserStatus**. De standaardwaarde is **UserLoggedOn**.  

- **UserInputRequired**: Geef op of het programma interactie met de gebruiker vereist. Beschikbare waarden zijn **True** (Waar) of **False** (Onwaar). De standaard waarde is **True**. Deze vermelding is ingesteld op **False** als **CanRunWhen** niet is ingesteld op **UserLoggedOn**.  

- **AdminRightsRequired**: Geef op of het programma beheerders referenties nodig heeft om de computer uit te voeren. Beschikbare waarden zijn **True** (Waar) of **False** (Onwaar). De standaard waarde is **False**. Deze vermelding is ingesteld op **True** als **CanRunWhen** niet is ingesteld op **UserLoggedOn**.  

- **UseInstallAccount**: Geef op of het programma het installatie account van de client software gebruikt wanneer dit wordt uitgevoerd op client computers. Deze waarde is standaard **False** (Onwaar). Deze waarde is ook **False** (Onwaar) als **CanRunWhen** is ingesteld op **UserLoggedOn**.  

- **DriveLetterConnection**: Geef op of het programma een stationsletter verbinding moet hebben met de pakket bestanden op het distributie punt. U kunt **True** (Waar) of **False** (Onwaar) opgeven. De standaard waarde is **False**, waardoor het programma een UNC-verbinding (Universal Naming Convention) kan gebruiken. Als deze waarde is ingesteld op **True**, gebruikt de client de volgende beschik bare stationsletter, beginnend met Z: en gaat achteruit.  

- **SpecifyDrive** (optioneel): Geef een stationsletter op die het programma nodig heeft om verbinding te maken met de pakket bestanden op het distributie punt. Deze instelling dwingt het gebruik van de opgegeven stationsletter af voor client verbindingen met distributie punten.

- **ReconnectDriveAtLogon**: Geef op of de computer opnieuw verbinding met het distributie punt maakt wanneer de gebruiker zich aanmeldt. Beschikbare waarden zijn **True** (Waar) of **False** (Onwaar). De standaard waarde is **False**.  

- **DependentProgram**: Geef een programma in dit pakket op dat moet worden uitgevoerd vóór het huidige programma. Voor deze vermelding wordt gebruikgemaakt van de notatie `DependentProgram=<ProgramName>`, waarbij `<ProgramName>` de **naam** voor dat programma wordt vermeld in de Package Definition File. Als er geen afhankelijke programma's zijn, laat u dit item leeg.  

    Voorbeelden:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Toewijzing**: Geef op hoe het programma wordt toegewezen aan gebruikers. Deze waarde kan zijn:

    - **FirstUser**: alleen de eerste gebruiker die zich aanmeldt bij de client, voert het programma uit
    - **EveryUser**: elke gebruiker die zich aanmeldt, voert het programma uit

    Wanneer **CanRunWhen** niet is ingesteld op **UserLoggedOn**, wordt dit item ingesteld op **FirstUser**.  

- **Uitgeschakeld**: Geef op of u dit programma kunt implementeren op clients. Beschikbare waarden zijn **True** (Waar) of **False** (Onwaar). De standaard waarde is **False**.  


## <a name="use-a-package-definition-file"></a>Een Package Definition File gebruiken  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer het knoop punt **pakketten** .  

2. Kies op het tabblad **Start** van het lint in de groep **maken** de optie **pakket maken van definitie**.  

3. Kies op de pagina **pakket definitie** van de **wizard pakket maken van definitie**een bestaand Package Definition File. Als u een nieuwe Package Definition File wilt openen, kiest u **Bladeren**. Nadat u een nieuwe Package Definition File hebt opgegeven, selecteert u deze in de lijst **pakket definitie** .

4. Geef op de pagina **bron bestanden** informatie op over de vereiste bron bestanden voor het pakket en programma.  

5. Als voor het pakket bron bestanden zijn vereist, geeft u op de pagina **bron map** de locatie op van waaruit de site de bron bestanden kan ophalen.  

6. Voltooi de wizard.  


## <a name="see-also"></a>Zie ook

[Pakketten en programma's](packages-and-programs.md)
