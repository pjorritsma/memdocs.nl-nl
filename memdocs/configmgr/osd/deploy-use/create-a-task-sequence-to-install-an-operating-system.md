---
title: Een takenreeks maken voor het installeren van een besturingssysteem
titleSuffix: Configuration Manager
description: Gebruik taken reeksen in Configuration Manager om automatisch een installatie kopie van het besturings systeem en andere inhoud op een doel computer te installeren.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dae4287b1e4a4a69209672f01f45eeaeb3b540d7
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125471"
---
# <a name="create-a-task-sequence-to-install-an-os"></a>Een takenreeks maken voor het installeren van een besturingssysteem

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik taken reeksen in Configuration Manager om automatisch een installatie kopie van een besturings systeem op een doel computer te installeren. U maakt een taken reeks die verwijst naar een opstart installatie kopie die wordt gebruikt om de doel computer te starten, de installatie kopie van het besturings systeem die u wilt installeren op de doel computer en andere aanvullende inhoud, zoals andere toepassingen of software-updates, die u wilt installeren. Vervolgens implementeert u de takenreeks voor de verzameling die de doelcomputer bevat.  

## <a name="create-a-task-sequence-to-install-an-os"></a><a name="BKMK_InstallOS"></a>Een taken reeks maken om een besturings systeem te installeren

Er zijn meerdere scenario's voor het implementeren van een besturings systeem op computers in uw omgeving. In de meeste gevallen maakt u een taken reeks en selecteert u **een bestaand installatie kopie pakket installeren** in de wizard taken reeks maken. Met deze optie maakt u een taken reeks waarmee het besturings systeem wordt geïnstalleerd, gebruikers instellingen worden gemigreerd, software-updates worden toegepast en toepassingen worden geïnstalleerd.

### <a name="prerequisites"></a>Vereisten

Voordat u een taken reeks maakt om een besturings systeem te installeren, moet aan de volgende vereisten zijn voldaan:

#### <a name="required"></a>Vereist

- Een [opstart installatie kopie](../get-started/manage-boot-images.md)  

- Een [installatie kopie van het besturings systeem](../get-started/manage-operating-system-images.md)  

#### <a name="required-if-used"></a>Vereist (indien gebruikt)

- [Software-updates](../../sum/get-started/synchronize-software-updates.md) synchroniseren  

- [Toepassingen](../../apps/deploy-use/create-applications.md) toevoegen  

### <a name="process-to-create-a-task-sequence-that-installs-an-os"></a>Proces voor het maken van een taken reeks waarmee een besturings systeem wordt geïnstalleerd  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer het knoop punt **taken reeksen** .  

2. Selecteer **taken reeks maken**op het tabblad **Start** van het lint in de groep **maken** . Met deze actie wordt de wizard taken reeks maken gestart.  

3. Selecteer op de pagina **nieuwe taken reeks maken** de optie **een bestaand installatie kopie pakket installeren**en selecteer vervolgens **volgende**.  

4. Geef op de pagina **taken reeks informatie** de volgende instellingen op:  

    - **Takenreeksnaam**: geef een naam op die de takenreeks identificeert.  

    - **Beschrijving**: Geef een beschrijving op van de taken reeks.  

    - **Opstart installatie kopie**: Geef de opstart installatie kopie op die de taken reeks gebruikt om het besturings systeem op de doel computer te installeren. De opstart installatie kopie bevat een versie van Windows PE, plus eventuele aanvullende vereiste apparaatstuurprogramma's. Zie [opstart installatie kopieën beheren](../get-started/manage-boot-images.md)voor meer informatie.  

        > [!IMPORTANT]  
        > De architectuur van de opstartinstallatiekopie moet compatibel zijn met de hardware-architectuur van de doelcomputer.  

5. Geef op de pagina **Windows installeren** de volgende instellingen op:  

    - **Installatie kopie pakket**: Geef het pakket op dat de installatie kopie van het besturings systeem bevat die moet worden geïnstalleerd. Zie [installatie kopieën van besturings systemen beheren](../get-started/manage-operating-system-images.md)voor meer informatie.  

    - **Installatie kopie**: als het installatie kopie pakket van het besturings systeem meerdere installatie kopieën bevat, geeft u de index op van de installatie kopie van het besturings systeem die u wilt  

    - **De doel computer partitioneren en Format teren installeren van het besturings systeem**: Geef op of u de taken reeks wilt partitioneren en Format teren van de doel computer voordat u de OS installeert.  

    - **Product code**: Geef de Windows-product code op, indien nodig. U kunt gecodeerde volumelicentiesleutels en standaardproductsleutels opgeven. Als u een niet-gecodeerde product code gebruikt, moet elke groep van vijf tekens gescheiden worden door een streepje ( `-` ). Bijvoorbeeld: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    - **Serverlicentiemodus**: geef op of de serverlicentie **Per seat**of **Per server**is of dat er geen licentie wordt opgegeven. Als de serverlicentie **Per server**is, geef dan ook het maximum aantal serververbindingen op.  

    - Geef op hoe het beheerders account moet worden afgehandeld voor het nieuwe besturings systeem:  

        - **Wille keurig het wacht woord voor het lokale beheerders account genereren en het account uitschakelen op alle ondersteunde platforms (aanbevolen)**: Windows schakelt het lokale beheerders account uit nadat de taken reeks de installatie kopie van het besturings systeem implementeert.  

        - **Het account inschakelen en het wacht woord van de lokale beheerder opgeven**: Windows gebruikt hetzelfde wacht woord voor het lokale beheerders account op alle computers waarop de taken reeks de installatie kopie van het besturings systeem implementeert.  

6. Geef op de pagina **netwerk configureren** de volgende instellingen op:  

    - **Lid worden van een werk groep**: Voeg de doel computer toe aan een werk groep.  

    - **Lid worden van een domein**: Voeg de doel computer toe aan een domein. Geef in **Domein**de naam op van het domein.  

        > [!IMPORTANT]  
        > U kunt bladeren om domeinen te zoeken in het lokaal forest, maar u moet de domeinnaam opgeven voor een extern forest.  

        U kunt ook een organisatie-eenheid (OE) opgeven in het veld **OE van domein** . Deze instelling is optioneel en geeft de LDAP X. 500-DN-naam van de organisatie-eenheid. Als deze nog niet bestaat, maakt Windows het computer account in deze OE.  

    - **Account**: de gebruikers naam en het wacht woord voor het account dat is gemachtigd om lid te worden van het opgegeven domein. Bijvoorbeeld: *domein\gebruiker* of *%variabele%*.  

        > [!IMPORTANT]  
        > Als u van plan bent de instellingen van het domein of de werk groep te migreren, voert u de juiste domein referenties in.  

7. Geef op de pagina **installeer Configuration Manager** het Configuration Manager-client pakket op dat op de doel computer moet worden geïnstalleerd. U kunt ook installatie-eigenschappen toevoegen.  

8. Geef op de pagina **status migratie** de volgende informatie op:  

    - **Gebruikers instellingen vastleggen**: de taken reeks legt de gebruikers status vast. Zie [gebruikers status beheren](../get-started/manage-user-state.md)voor meer informatie over het vastleggen en herstellen van de gebruikers status.  

    - **Netwerk instellingen vastleggen**: de taken reeks legt netwerk instellingen vast van de doel computer. Hiermee wordt het lidmaatschap van het domein of de werk groep vastgelegd, ook de instellingen van de netwerk adapter.  

    - **Micro soft Windows-instellingen vastleggen**: de taken reeks legt Windows-instellingen vast van de doel computer voordat de installatie kopie van het besturings systeem wordt geïnstalleerd. De computer naam, de naam van de geregistreerde gebruiker en organisatie en de instellingen voor de tijd zone worden vastgelegd.  

9. Geef op de pagina **updates toevoegen** op of de vereiste software-updates, alle software-updates of geen software-updates moeten worden geïnstalleerd. Als u opgeeft om software-updates te installeren, installeert Configuration Manager alleen de software-updates die zijn gericht op de verzamelingen waarvan de doel computer lid is.  

10. Geef op de pagina **toepassingen installeren** de toepassingen op die moeten worden geïnstalleerd op de doel computer. Als u meerdere toepassingen opgeeft, kunt u opgeven dat de takenreeks wordt voortgezet als de installatie van een bepaalde toepassing mislukt.  

11. Voltooi de wizard.  

U kunt nu de takenreeks implementeren voor een verzameling van computers. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.


## <a name="pre-cache-content"></a>Inhoud vooraf in cache opslaan

<!--4224642-->
Vanaf versie 1906 kunt u dit type taken reeks inschakelen om inhoud vooraf in de cache op te slaan. Met de functie voor het vooraf opslaan van beschik bare implementaties van taken reeksen kunnen clients relevante inhoud downloaden voordat een gebruiker de taken reeks installeert.  

Zie [inhoud vooraf in cache configureren](configure-precache-content.md)voor meer informatie.


## <a name="example-task-sequence"></a><a name="BKMK_InstallExistingOSImageTSExample"></a>Voor beeld van taken reeks

Gebruik de volgende tabel als richt lijn bij het maken van een taken reeks die een besturings systeem implementeert met behulp van een bestaande installatie kopie. De tabel helpt u bij het bepalen van de algemene volg orde voor uw taken reeks stappen en hoe u deze taken reeks stappen indeelt in logische groepen. De takenreeks die u maakt, kan afwijken van dit voorbeeld en kan meer of minder takenreeksstappen en groepen bevatten.  

> [!NOTE]  
> Gebruik de wizard taken reeks maken om deze taken reeks te maken.  
>
> Wanneer u de wizard taken reeks maken gebruikt om deze nieuwe taken reeks te maken, zijn sommige namen van de stappen anders dan wanneer u deze taken reeks stappen hand matig toevoegt aan een bestaande taken reeks.

|Takenreeksgroep of -stap|Beschrijving|  
|---------------------------------|-----------------|  
|Bestand en instellingen vastleggen- **(nieuwe taken reeks groep)**|Een takenreeksgroep maken. In een takenreeksgroep houdt u vergelijkbare takenreeksstappen bij elkaar voor betere ordening en foutcontrole.<br /><br /> Deze groep bevat de stappen die nodig zijn voor het vastleggen van bestanden en instellingen van het besturingssysteem van een referentiecomputer.|  
|Windows-instellingen vastleggen|Gebruik deze takenreeksstap om de Microsoft Windows-instellingen op de referentiecomputer te identificeren die moeten worden vastgelegd. U kunt de computernaam, gebruikers- en organisatiegegevens en de instellingen voor de tijdzone vastleggen.|  
|Netwerkinstellingen vastleggen|Gebruik deze takenreeksstap om de netwerkinstellingen van de referentiecomputer vast te leggen. U kunt naast de netwerkadapterinstellingen het lidmaatschap van de referentiecomputer van een domein of werkgroep vastleggen.|  
|Gebruikers bestanden en-instellingen vastleggen- **(nieuwe taken reeks subgroep)**|Maak een takenreeksgroep binnen een takenreeksgroep. Deze subgroep bevat de stappen die nodig zijn om de gebruikersstatus vast te leggen. Net als bij de eerste groep die u hebt toegevoegd, houdt deze subgroep samen met dezelfde taken reeks stappen voor betere organisatie-en fout controle.|  
|Opslag gebruikersstatus aanvragen|Gebruik deze takenreeksstap om toegang aan te vragen tot een statusmigratiepunt waar de gebruikersgegevens worden opgeslagen. U kunt deze takenreeksstap configureren om informatie over de gebruikersstatus vast te leggen of te herstellen.|  
|Gebruikersbestanden en -instellingen vastleggen|Gebruik deze taken reeks stap om de Hulpprogramma voor migratie van gebruikersstatus (USMT) te gebruiken om de gebruikers status en instellingen vast te leggen van de referentie computer die de taken reeks ontvangt die aan deze taak stap is gekoppeld. U kunt de standaard opties vastleggen of configureren welke opties u wilt vastleggen.|  
|Opslag gebruikersstatus vrijgeven|Gebruik deze takenreeksstap om het statusmigratiepunt te informeren dat de vastleg- of herstelactie is voltooid.|  
|Besturings systeem installeren- **(nieuwe taken reeks groep)**|Maak een andere taken reeks subgroep. Deze subgroep bevat de stappen die nodig zijn om de Windows PE-omgeving te installeren en te configureren.|  
|Opnieuw opstarten in Windows PE|In deze takenreeksstap geeft u de opties op voor het opnieuw opstarten van de doelcomputer die deze takenreeks ontvangt. Bij deze stap wordt een bericht voor de gebruiker weergegeven dat de computer opnieuw wordt opgestart zodat de installatie kan doorgaan.<br /><br /> Deze stap maakt gebruik van de alleen-lezen takenreeksvariabele **_SMSTSInWinPE** . Als de gekoppelde waarde gelijk is aan **false**, wordt de takenreeksstap voortgezet.|  
|Schijf 0 partitioneren|Met deze takenreeksstap geeft u de acties op die nodig zijn om de harde schijf op de doelcomputer te formatteren. Het standaardnummer van de schijf is **0**.<br /><br /> Deze stap maakt gebruik van de alleen-lezen takenreeksvariabele **_SMSTSClientCache** . Deze stap wordt uitgevoerd als de Configuration Manager-client cache niet bestaat.|  
|Besturingssysteem toepassen|Met deze takenreeksstap installeert u de installatiekopie van het besturingssysteem op de doelcomputer. Met deze stap worden eerst alle bestanden op het volume verwijderd, met uitzonde ring van Configuration Manager-specifieke besturings bestanden. Vervolgens worden alle volume kopieën in het WIM-bestand toegepast op het bijbehorende sequentiële schijf volume op de doel computer. U kunt een **sysprep** -antwoordbestand opgeven en ook configureren welke schijfpartitie voor de installatie moet worden gebruikt.|  
|Windows-instellingen toepassen|Met deze takenreeksstap configureert u de configuratiegegevens voor de Windows-instellingen voor de doelcomputer. De Windows-instellingen die u kunt toepassen zijn gebruikers- en organisatiegegevens, product- of licentiecodegegevens, de tijdzone en het wachtwoord voor de lokale beheerder.|  
|Netwerkinstellingen toepassen|Met deze takenreeks geeft u de gegevens voor netwerk- of werkgroepconfiguratie op voor de doelcomputer. U kunt ook opgeven of de computer een DHCP-server gebruikt of u kunt de IP-adresgegevens statisch toewijzen.|  
|Apparaatstuurprogramma's toepassen|Met deze takenreeksstap installeert u stuurprogramma's als onderdeel van de implementatie van een besturingssysteem. U kunt Windows Setup toestaan om in alle bestaande categorieën stuurprogramma's te zoeken door **stuurprogramma's uit alle categorieën overwegen** te selecteren of de stuurprogrammacategorieën waarin Windows Setup zoekt beperken door **Zoeken naar passende stuurprogramma's beperken tot bepaalde categorieën**te selecteren.<br /><br /> Deze stap maakt gebruik van de alleen-lezen takenreeksvariabele **_SMSTSMediaType** . Deze taken reeks stap wordt alleen uitgevoerd als de waarde van de variabele niet gelijk is aan **FullMedia**.|  
|Stuurprogrammapakket toepassen|Gebruik deze takenreeksstap om alle apparaatstuurprogramma's in een stuurprogrammapakket beschikbaar te maken voor gebruik door Windows Setup.|  
|Besturings systeem installeren- **(nieuwe taken reeks groep)**|Maak een andere taken reeks subgroep. Deze subgroep bevat de stappen die nodig zijn om het geïnstalleerde besturingssysteem te configureren.|  
|Windows en ConfigMgr installeren|Gebruik deze taken reeks stap om de Configuration Manager-client software te installeren. Configuration Manager installeert en registreert de Configuration Manager-client-GUID. U kunt de vereiste installatieparameters toewijzen in het venster **Installatie-eigenschappen** .|  
|Updates installeren|Met deze takenreeksstap geeft u op hoe software-updates worden geïnstalleerd op de doelcomputer. De doel computer wordt pas geëvalueerd voor toepasselijke software-updates als deze taken reeks stap wordt uitgevoerd. Op dat moment wordt de doel computer geëvalueerd voor software-updates die vergelijkbaar zijn met andere door Configuration Manager beheerde clients.<br /><br /> Deze stap maakt gebruik van de alleen-lezen takenreeksvariabele **_SMSTSMediaType** . Deze taken reeks stap wordt alleen uitgevoerd als de waarde van de variabele niet gelijk is aan **FullMedia**.|  
|Gebruikers bestanden en-instellingen herstellen- **(nieuwe taken reeks subgroep)**|Maak een andere taken reeks subgroep. Deze subgroep bevat de stappen die nodig zijn om de gebruikersbestanden en -instellingen te herstellen.|  
|Opslag gebruikersstatus aanvragen|Gebruik deze takenreeksstap om toegang aan te vragen tot een statusmigratiepunt waar de gebruikersgegevens worden opgeslagen.|  
|Gebruikersbestanden en -instellingen herstellen|Gebruik deze taken reeks stap om de Hulpprogramma voor migratie van gebruikersstatus (USMT) uit te voeren om de gebruikers status en-instellingen naar een doel computer te herstellen.|  
|Opslag gebruikersstatus vrijgeven|Gebruik deze takenreeksstap om het statusmigratiepunt te informeren dat de gebruikersstatusgegevens niet langer nodig zijn.|  
