---
title: Een takenreeks maken voor het vastleggen van een besturingssysteem
titleSuffix: Configuration Manager
description: Een taken reeks voor bouwen en vastleggen bouwt een referentie computer die specifieke Stuur Programma's en software-updates naast het besturings systeem kan bevatten.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ceb63560c6000b1a76116d0791c98219a66066b8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723066"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>Een takenreeks maken voor het vastleggen van een besturingssysteem

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u een taken reeks gebruikt om een besturings systeem te implementeren op een computer in Configuration Manager, installeert de computer de installatie kopie van het besturings systeem die u opgeeft in de taken reeks. U kunt de installatie kopie van het besturings systeem aanpassen zodat deze specifieke Stuur Programma's, toepassingen en software-updates bevat. Gebruik eerst een taken reeks voor bouwen en vastleggen om een referentie computer te bouwen. Leg vervolgens de installatie kopie van het besturings systeem vast van die referentie computer. Als u al een referentie computer beschikbaar hebt om vast te leggen, maakt u een aangepaste taken reeks om het besturings systeem vast te leggen.

## <a name="about-the-build-and-capture-task-sequence"></a><a name="BKMK_BuildCaptureTS"></a>Over de taken reeks voor samen stellen en vastleggen

De taken reeks voor samen stellen en vastleggen:

- De referentie computer partitioneren en Format teren
- Installeert het besturings systeem
- Installeert de Configuration Manager-client
- Installeert toepassingen
- Hiermee worden software-updates toegepast
- Hiermee wordt het besturings systeem van de referentie computer vastgelegd

De pakketten die zijn gekoppeld aan de taken reeks, zoals toepassingen, moeten beschikbaar zijn op distributie punten voordat u de taken reeks bouwen en vastleggen implementeert.

## <a name="requirements"></a><a name="BKMK_CreatePackages"></a>Vereiste

Voordat u een taken reeks maakt om een besturings systeem te installeren, moet u ervoor zorgen dat de volgende onderdelen aanwezig zijn:  

### <a name="required"></a>Vereist

- [Opstartinstallatiekopie](../get-started/manage-boot-images.md)

- [Installatie kopie van besturings systeem](../get-started/manage-operating-system-images.md)

### <a name="required-if-used"></a>Vereist (indien gebruikt)

- [Stuur programmapakketten](../get-started/manage-drivers.md) die de benodigde Windows-Stuur Programma's bevatten voor de ondersteuning van hardware op de referentie computer. Zie [Use task sequences to install device drivers](../get-started/manage-drivers.md#BKMK_TSDrivers)voor meer informatie over takenreeksstappen om stuurprogramma’s te beheren.

- [Software-updates](../../sum/get-started/synchronize-software-updates.md)

- [Toepassingen](../../apps/deploy-use/create-applications.md)

## <a name="create-a-build-and-capture-task-sequence"></a><a name="BKMK_CreateBuildCaptureTS"></a> Een takenreeks voor bouwen en vastleggen maken

Gebruik de volgende procedure om een taken reeks te gebruiken om een referentie computer te bouwen en het besturings systeem vast te leggen.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

1. Klik op het tabblad **Start** van het lint in de groep **maken** op **taken reeks maken** om de wizard taken reeks maken te starten.  

1. Selecteer **Referentie-installatiekopie voor besturingssysteem samenstellen** op de pagina **Nieuwe takenreeks maken**.  

1. Geef op de pagina **taken reeks informatie** de volgende instellingen op:  

    - **Takenreeksnaam**: geef een naam op die de takenreeks identificeert.  

    - **Beschrijving**: Geef een optionele beschrijving op voor de taken reeks. Beschrijf bijvoorbeeld het besturings systeem dat door de taken reeks wordt gemaakt.

    - **Opstart installatie**kopie: Geef de opstart installatie kopie op die moet worden gebruikt met deze taken reeks.  

        > [!IMPORTANT]  
        > De architectuur van de opstartinstallatiekopie moet compatibel zijn met de hardware-architectuur van de doelcomputer.  

1. Geef op de pagina **Windows installeren** de volgende instellingen op:  

    - **Installatie kopie pakket**: Geef het installatie kopie pakket van het besturings systeem op dat de vereiste bestanden bevat om het besturings systeem te installeren.  

    - **Installatie kopie-index**: Geef de index op van het besturings systeem dat in de installatie kopie moet worden geïnstalleerd. Als de installatie kopie van het besturings systeem meerdere versies bevat, selecteert u de versie die u wilt installeren.  

    - **Product code**: geef, indien nodig, de product code op voor het Windows-besturings systeem dat u wilt installeren. U kunt gecodeerde volumelicentiesleutels en standaardproductsleutels opgeven. Als u een niet-gecodeerde product code gebruikt, scheidt u elke groep van vijf tekens met een`-`streepje (). Bijvoorbeeld: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Server licentie modus**: als dat nodig is, geeft u op of de server licentie **per seat**of **per server**is of dat er geen licentie is opgegeven. Als de serverlicentie **Per server**is, geef dan ook het maximum aantal serververbindingen op.  

    - Geef op hoe het beheerders account moet worden geconfigureerd voor het geïmplementeerde besturings systeem:  

        - **Wille keurig het lokale beheerders wachtwoord genereren en het account uitschakelen op alle ondersteunde platforms**: Maak een wille keurig wacht woord voor het lokale beheerders account. Schakel het account uit wanneer de Windows is ingesteld.

        - **Het account inschakelen en het wacht woord van de lokale beheerder opgeven**: gebruik hetzelfde wacht woord voor het lokale beheerders account op alle computers waarop u dit besturings systeem implementeert.

1. Geef op de pagina **netwerk configureren** de volgende instellingen op:

    - **Lid worden van een werk groep**: Geef op of de doel computer aan een werk groep moet worden toegevoegd wanneer het besturings systeem wordt geïmplementeerd.  

    - **Lid worden van een domein**: Geef op of de doel computer aan een domein moet worden toegevoegd wanneer het besturings systeem wordt geïmplementeerd. Geef in **Domein**de naam op van het domein.  

        > [!IMPORTANT]  
        > U kunt bladeren om domeinen te zoeken in het lokale forest. Geef de domein naam op voor een extern forest.

        U kunt ook een organisatie-eenheid (OE) opgeven. Deze instelling is optioneel en geeft de DN-naam van LDAP X. 500 van de organisatie-eenheid waarin het computer account moet worden gemaakt, als deze nog niet bestaat.  

    - **Account**: geef de gebruikersnaam en het wachtwoord op voor het account dat machtigingen heeft om lid te worden van het opgegeven domein. Bijvoorbeeld: `domain\user` of `%variable%`.  

        > [!IMPORTANT]  
        > Als u de instellingen van het domein of de werk groep tijdens de implementatie wilt migreren, moet u de juiste domein referenties invoeren.  

1. Geef op de pagina **installeer Configuration Manager** het Configuration Manager-client pakket op. Dit pakket bevat de bron bestanden voor de installatie van de Configuration Manager-client. Geef ook aanvullende eigenschappen op die nodig zijn om de client te installeren.  

    Zie [over eigenschappen van client installatie](../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie.

1. Geef op de pagina **updates toevoegen** op of de vereiste software-updates, alle software-updates of geen software-updates moeten worden geïnstalleerd. Als u opgeeft om software-updates te installeren, installeert Configuration Manager alleen de software-updates die zijn gericht op de verzamelingen waarvan de doel computer lid is.  

1. Geef op de pagina **toepassingen installeren** de toepassingen op die moeten worden geïnstalleerd op de doel computer. Als u meerdere toepassingen opgeeft, kunt u opgeven dat de takenreeks wordt voortgezet als de installatie van een bepaalde toepassing mislukt.  

    > [!NOTE]
    > De pagina **systeem voorbereiding** wordt weer gegeven naast de wizard, maar deze wordt niet meer gebruikt. Selecteer **Volgende** om door te gaan.

1. Geef op de pagina **Eigenschappen van installatie kopieën** de volgende instellingen op voor de installatie kopie van het besturings systeem:

    - **Gemaakt door**: Geef de naam op van de gebruiker die als maker van de installatie kopie van het besturings systeem moet worden genoteerd.  

    - **Versie**: Geef uw versie nummer op dat is gekoppeld aan de installatie kopie van het besturings systeem. Dit kenmerk hoeft niet de versie van het besturings systeem te zijn, omdat de site deze waarde afzonderlijk opslaat.

    - **Beschrijving**: Geef een beschrijving op van de installatie kopie van het besturings systeem.  

1. Geef op de pagina **installatie kopie vastleggen** de volgende instellingen op:

    - **Pad**: Geef een gedeelde netwerkmap op waarin Configuration Manager het uitvoer kopie bestand (. Wim) moet opslaan. Dit bestand bevat de installatie kopie van het besturings systeem die is gebaseerd op de instellingen die u in deze wizard opgeeft. Als u een map opgeeft die een bestaande bevat. WIM-bestand worden overschreven.  

    - **Account**: geef het Windows-account op met de machtigingen voor de netwerkshare waarin de installatiekopie wordt opgeslagen.  

1. Voltooi de wizard.  

Als u extra stappen wilt toevoegen aan de taken reeks, selecteert u deze en kiest u **bewerken**. Zie [de taken reeks editor gebruiken](../understand/task-sequence-editor.md)voor meer informatie over het bewerken van een taken reeks.  

Implementeer op een van de volgende manieren de takenreeks op een referentiecomputer:  

- Als de referentie computer al een Configuration Manager-client is, implementeert u de taken reeks voor bouwen en vastleggen in een verzameling die de referentie computer bevat. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.

- Als de referentie computer geen Configuration Manager-client is, of als u de taken reeks hand matig wilt uitvoeren op de referentie computer, gebruikt u de **wizard taken reeks media maken** om opstart bare media te maken. Zie [opstart bare media maken](create-bootable-media.md)voor meer informatie.  

Nadat u de installatie kopie hebt vastgelegd, kunt u deze implementeren op andere computers. Zie [een taken reeks maken om een besturings systeem te installeren](create-a-task-sequence-to-install-an-operating-system.md)voor meer informatie over het implementeren van de vastgelegde installatie kopie van het besturings systeem.  

## <a name="capture-from-an-existing-reference-computer"></a><a name="BKMK_CaptureExistingRefComputer"></a>Vastleggen vanaf een bestaande referentie computer

Wanneer u al een referentie computer hebt die gereed is voor vastleggen, maakt u een taken reeks die alleen het besturings systeem van de referentie computer vastlegt. Gebruik de taken reeks stap **besturingssysteem installatie kopie vastleggen** om een of meer installatie kopieën van een referentie computer vast te leggen en op te slaan in een installatie kopie bestand (. Wim) op de opgegeven netwerk share. Start de referentie computer in Windows PE met een opstart installatie kopie. De taken reeks legt elke harde schijf op de referentie computer vast als een afzonderlijke installatie kopie binnen het WIM-bestand. Als de computer waarnaar wordt verwezen meerdere stations heeft, bevat het resulterende. WIM-bestand een afzonderlijke installatie kopie voor elk volume. Alleen volumes die zijn geformatteerd als NTFS of FAT32 worden vastgelegd. Volumes met andere indelingen of USB-volumes worden overgeslagen.  

Gebruik de volgende procedure om een installatie kopie van een besturings systeem vast te leggen vanaf een bestaande referentie computer:

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **taken reeksen** .  

1. Selecteer **taken reeks maken**op het tabblad **Start** van het lint in de groep **maken** . Met deze actie wordt de wizard taken reeks maken gestart.  

1. Selecteer **Nieuwe aangepaste takenreeks maken** op de pagina **Nieuwe takenreeks maken**.  

1. Geef op de pagina **taken reeks informatie** een naam op voor de taken reeks. Voeg eventueel een beschrijving voor de taken reeks toe.  

1. Geef een opstartinstallatiekopie op voor de takenreeks. Configuration Manager gebruikt deze opstart installatie kopie om de referentie computer te starten met Windows PE. Zie [opstart installatie kopieën beheren](../get-started/manage-boot-images.md)voor meer informatie.  

1. Voltooi de wizard.  

1. Selecteer in het knoop punt **taken reeksen** de nieuwe taken reeks. Selecteer vervolgens op het tabblad **Start** van het lint in de groep **taken reeks** de optie **bewerken**. Met deze actie wordt de taken reeks editor geopend.  

1. Als de Configuration Manager-client op de referentie computer is geïnstalleerd:

    Ga naar het menu **toevoegen** , selecteer **afbeeldingen**en kies vervolgens [ConfigMgr-client voorbereiden voor vastleggen](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Met deze stap wordt de Configuration Manager-client op de referentie computer gegeneraliseerd.

    > [!Note]  
    > De taken reeks biedt geen ondersteuning voor het verwijderen van de Configuration Manager-client.

1. Ga naar het menu **toevoegen** , selecteer **installatie kopieën**en kies [Windows voorbereiden voor vastleggen](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Met deze stap wordt Sysprep uitgevoerd en wordt de computer opnieuw opgestart naar de opstart installatie kopie voor Windows PE die is opgegeven voor de taken reeks. Deze actie kan alleen worden voltooid als de referentie computer niet aan een domein is toegevoegd.

1. Ga naar het menu **toevoegen** , selecteer **installatie kopieën**en kies [installatie kopie van het besturings systeem vastleggen](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage). Deze stap wordt alleen uitgevoerd vanuit Windows PE om de vaste schijven op de referentie computer vast te leggen. Configureer de volgende instellingen:

    - **Naam** en **Beschrijving**: u kunt desgewenst de naam van de takenreeksstap wijzigen en een beschrijving verschaffen.  

    - **Bestemming**: geef een gedeelde netwerkmap op waarin het WIM-uitvoerbestand moet worden opgeslagen. Dit bestand bevat de installatie kopie van het besturings systeem op basis van de instellingen die u opgeeft met behulp van deze wizard. Als u een map opgeeft die een bestaande bevat. WIM-bestand worden overschreven.  

    - **Beschrijving**, **versie**en **gemaakt door**: Geef desgewenst Details op over de installatie kopie die moet worden vastgelegd.  

    - **Account voor het vastleggen van een besturingssysteeminstallatiekopie**: geef het Windows-account op met de machtigingen voor de netwerkshare die u hebt opgegeven. Selecteer **instellen** om de naam van het Windows-account op te geven.  

Selecteer **OK** om uw wijzigingen op te slaan en de taken reeks editor te sluiten.  

Implementeer op een van de volgende manieren de takenreeks op een referentiecomputer:  

- Als de referentie computer al een Configuration Manager-client is, implementeert u de taken reeks voor vastleggen in een verzameling die de referentie computer bevat. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.

- Als de referentie computer geen Configuration Manager-client is, of als u de taken reeks hand matig wilt uitvoeren op de referentie computer, gebruikt u de **wizard taken reeks media maken** om vastleg media te maken. Zie [Capture-media maken](create-capture-media.md)voor meer informatie.  

Nadat u de installatie kopie hebt vastgelegd, kunt u deze implementeren op andere computers. Zie [een taken reeks maken om een besturings systeem te installeren](create-a-task-sequence-to-install-an-operating-system.md)voor meer informatie over het implementeren van de vastgelegde installatie kopie van het besturings systeem.

## <a name="example-task-sequence"></a><a name="BKMK_BuildandCaptureTSExample"></a>Voor beeld van taken reeks

Gebruik de volgende tabel als richt lijn bij het maken van een taken reeks die een installatie kopie van een besturings systeem bouwt en vastlegt. De tabel helpt u bij het bepalen van de algemene volg orde voor uw taken reeks stappen en het organiseren en structureren van die stappen in logische groepen. De taken reeks die u maakt, kan afwijken van dit voor beeld. Het kan meer of minder stappen en groepen bevatten.

> [!NOTE]  
> Gebruik altijd de wizard Takenreeks maken om een takenreeks van dit type te maken.
>
> De wizard voegt stappen toe aan de taken reeks met iets andere namen die u zou zien als u de stappen hand matig toevoegt.

### <a name="group-build-the-reference-machine"></a>Groep: de referentie computer bouwen

Deze groep bevat de acties die nodig zijn om een referentiecomputer te bouwen.

|Takenreeksstap|Beschrijving|  
|-------------------------------|---------------|  
|**Opnieuw opstarten in Windows PE**|Start de doel computer opnieuw op naar de opstart installatie kopie die is toegewezen aan de taken reeks. In deze stap wordt een bericht voor de gebruiker weer gegeven dat de computer opnieuw wordt opgestart, zodat de installatie kan worden voortgezet.<br /><br />Deze stap maakt gebruik van de alleen `_SMSTSInWinPE` -lezen taken reeks variabele. Als de gekoppelde waarde gelijk is `false`aan, wordt de taken reeks stap voortgezet.|
|**Schijf 0 - BIOS partitioneren**|Partitioneer en Format teer de vaste schijf op de doel computer in de BIOS-modus. Het standaard nummer van de `0`schijf is.<br /><br />Deze stap maakt gebruik van verschillende alleen-lezen taken reeks variabelen. Dit wordt bijvoorbeeld alleen uitgevoerd als de Configuration Manager-client cache niet bestaat en niet wordt uitgevoerd als de computer is geconfigureerd voor UEFI.|
|**Schijf 0 - UEFI partitioneren**|Partitioneer en Format teer de vaste schijf op de doel computer in UEFI-modus. Het standaard nummer van de `0`schijf is.<br /><br />Deze stap maakt gebruik van verschillende alleen-lezen taken reeks variabelen. Dit wordt bijvoorbeeld alleen uitgevoerd als de Configuration Manager-client cache niet bestaat en alleen wordt uitgevoerd als de computer is geconfigureerd voor UEFI.|
|**Besturingssysteem toepassen**|Installeer de opgegeven installatie kopie van het besturings systeem op de doel computer. Met deze stap worden eerst alle bestanden op het volume verwijderd, met uitzonde ring van Configuration Manager-specifieke besturings bestanden. Vervolgens worden alle volume kopieën in het WIM-bestand toegepast op het bijbehorende sequentiële schijf volume op de doel computer.|
|**Windows-instellingen toepassen**|Configureer de Windows-instellingen voor de doel computer.|
|**Netwerkinstellingen toepassen**|Geef de configuratie gegevens voor het netwerk of de werk groep op voor de doel computer.|
|**Apparaatstuurprogramma's toepassen**|Zoek en installeer Stuur Programma's als onderdeel van deze implementatie van het besturings systeem. Zie voor meer informatie [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).<br /><br />Deze stap maakt gebruik van de alleen `_SMSTSMediaType` -lezen taken reeks variabele. Als de gekoppelde waarde niet gelijk `FullMedia`is, wordt deze stap niet uitgevoerd.|
|**Windows en Configuration Manager instellen**|Installeer de Configuration Manager-client software. Configuration Manager installeert en registreert de Configuration Manager-client-GUID. Neem de benodigde **installatie-eigenschappen**op.|
|**Updates installeren**|Geef op hoe software-updates worden geïnstalleerd op de doel computer. De doel computer wordt pas geëvalueerd voor toepasselijke software-updates als deze stap wordt uitgevoerd. Op dat moment is de evaluatie vergelijkbaar met andere door Configuration Manager beheerde clients. Zie [software-updates installeren](../understand/install-software-updates.md)voor meer informatie.<br /><br />Deze stap maakt gebruik van de alleen `_SMSTSMediaType` -lezen taken reeks variabele. Als de gekoppelde waarde niet gelijk `FullMedia`is, wordt deze stap niet uitgevoerd.|
|**Toepassingen installeren**|Hiermee geeft u de toepassingen op die moeten worden geïnstalleerd op de referentie computer.|

### <a name="group-capture-the-reference-machine"></a>Groep: de referentie computer vastleggen

Deze groep bevat de benodigde stappen om een referentiecomputer voor te bereiden en vast te leggen.

|Takenreeksstap|Beschrijving|  
|-------------------------------|---------------|  
|**Configuration Manager-client voorbereiden**|Generaliseer de Configuration Manager-client op de referentie computer.|
|**Besturings systeem voorbereiden**|Voert Sysprep uit om Windows te generaliseren. Vervolgens wordt de computer opnieuw opgestart naar de opstart installatie kopie voor Windows PE die is opgegeven voor de taken reeks.|
|**Referentiecomputer vastleggen**|Hiermee legt u de installatie kopie vast op de opgegeven netwerk share en. WIM-bestand.|

> [!IMPORTANT]
> Nadat u een installatie kopie van een referentie computer hebt vastgelegd, moet u geen andere installatie kopie van het besturings systeem van de referentie computer vastleggen. Register vermeldingen worden gemaakt tijdens de initiële configuratie. Maak telkens wanneer u de installatie kopie van het besturings systeem vastlegt een nieuwe referentie computer. Als u van plan bent om dezelfde referentie computer te gebruiken om toekomstige installatie kopieën van het besturings systeem te maken, moet u eerst de Configuration Manager-client verwijderen en opnieuw installeren.

## <a name="next-steps"></a>Volgende stappen

[Methoden om enterprise-besturingssystemen te implementeren](methods-to-deploy-enterprise-operating-systems.md)
