---
title: Stappen voor takenreeksen
titleSuffix: Configuration Manager
description: Meer informatie over de stappen die u kunt toevoegen aan een Configuration Manager taken reeks.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: reference
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 37abb7cba84c8e2479e59070e47c3f09b3b2b8d9
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606971"
---
# <a name="task-sequence-steps"></a>Stappen voor takenreeksen

*Van toepassing op: Configuration Manager (huidige vertakking)*

De volgende taken reeks stappen kunnen worden toegevoegd aan een Configuration Manager taken reeks. Zie [de taken reeks editor gebruiken](task-sequence-editor.md)voor meer informatie.  

## <a name="common-settings"></a>Algemene instellingen

De volgende instellingen gelden voor alle taken reeks stappen:

### <a name="properties-for-all-steps"></a>Eigenschappen voor alle stappen

- **Naam**: in de taken reeks editor moet u een korte naam opgeven om deze stap te beschrijven. Wanneer u een nieuwe stap toevoegt, stelt de taken reeks editor de naam standaard in op het type. De **naam** mag maxi maal 50 tekens lang zijn.  

- **Beschrijving**: Geef desgewenst meer gedetailleerde informatie op over deze stap. De lengte van de **Beschrijving** mag niet langer zijn dan 256 tekens.  

In de rest van dit artikel worden de andere instellingen beschreven op het tabblad **Eigenschappen** voor elke taken reeks stap.

### <a name="options-for-all-steps"></a>Opties voor alle stappen

- **Deze stap uitschakelen**: de taken reeks slaat deze stap over wanneer deze wordt uitgevoerd op een computer. Het pictogram voor deze stap is grijs weer gegeven in de taken reeks editor.  

- **Door gaan bij fout**: als er een fout optreedt tijdens het uitvoeren van de stap, wordt de taken reeks voortgezet. Zie [plannings overwegingen voor het automatiseren van taken](../plan-design/planning-considerations-for-automating-tasks.md#BKMK_TSGroups)voor meer informatie.  

- **Voor waarde toevoegen**: de taken reeks evalueert deze voorwaardelijke instructies om te bepalen of de stap wordt uitgevoerd. Zie [How to use Task sequence Varia bles](using-task-sequence-variables.md#bkmk_access-condition)(Engelstalig) voor een voor beeld van het gebruik van een taken reeks variabele als voor waarde. Zie [taken reeks editor-voor waarden](task-sequence-editor.md#bkmk_conditions)voor meer informatie over voor waarden.

In de volgende secties voor specifieke taken reeks stappen worden de andere mogelijke instellingen op het tabblad **Opties** beschreven.



## <a name="apply-data-image"></a><a name="BKMK_ApplyDataImage"></a> Gegevens installatie kopie Toep assen

Gebruik deze stap om de gegevens installatie kopie te kopiëren naar de opgegeven doel partitie.  

Deze stap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **installatie kopieën**en selecteert u **gegevens installatie kopie Toep assen**.

### <a name="variables-for-apply-data-image"></a>Variabelen voor het Toep assen van gegevens installatie kopie

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDDataImageIndex](task-sequence-variables.md#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](task-sequence-variables.md#OSDWipeDestinationPartition)  

### <a name="cmdlets-for-apply-data-image"></a>Cmdlets voor het Toep assen van gegevens installatie kopie

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Get-CMTSStepApplyDataImage)
- [New-CMTSStepApplyDataImage](/powershell/module/configurationmanager/New-CMTSStepApplyDataImage)
- [Remove-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDataImage)
- [Set-CMTSStepApplyDataImage](/powershell/module/configurationmanager/Set-CMTSStepApplyDataImage)

### <a name="properties-for-apply-data-image"></a>Eigenschappen voor de installatie kopie van de gegevens Toep assen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="image-package"></a>Installatiekopiepakket

Selecteer **Bladeren** om het **installatie kopie pakket** op te geven dat wordt gebruikt door deze taken reeks. Selecteer het pakket dat u wilt installeren in het dialoogvenster **Pakket selecteren**. Onder in het dialoog venster worden de bijbehorende eigenschaps informatie voor elk bestaand installatie kopie pakket weer gegeven. Gebruik de vervolgkeuzelijst om de **Installatiekopie** te selecteren die u wilt installeren via het geselecteerde **Installatiekopiepakket**.  

> [!NOTE]  
> Met deze taken reeks actie wordt de installatie kopie beschouwd als een gegevens bestand. Deze actie voert geen Setup uit om de installatie kopie op te starten als een besturings systeem.  

#### <a name="destination"></a>Doel

Configureer een van de volgende opties:

- **Volgende beschik bare partitie**: gebruik de volgende sequentiële partitie waarvoor een installatie kopie van een **besturings systeem** of de stap voor het **Toep assen van gegevens** in deze taken reeks niet al is gericht.  

- **Specifieke schijf en partitie**: Selecteer het **schijf** nummer (te beginnen met 0) en het **partitie** nummer (te beginnen met 1).  

- **Specifieke logische stationsletter**: Geef **de stationsletter op die door** Windows PE wordt toegewezen aan de partitie. Deze stationsletter kan afwijken van de stationsletter die is toegewezen door het zojuist geïmplementeerde besturings systeem.  

- **Logische stationsletter opgeslagen in een variabele**: Geef de taken reeks variabele op die de stationsletter bevat die is toegewezen aan de partitie door Windows PE. Deze variabele wordt meestal ingesteld in de sectie Geavanceerd van het dialoog venster **partitie-eigenschappen** voor de taken reeks stap **schijf Format teren en partitioneren** .  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Alle inhoud op de partitie verwijderen alvorens de installatiekopie toe te passen  

Hiermee geeft u op dat de taken reeks alle bestanden op de doel partitie verwijdert voordat de installatie kopie wordt geïnstalleerd. Door de inhoud van de partitie niet te verwijderen, kan deze actie worden gebruikt om aanvullende inhoud toe te passen op een eerder beoogde partitie.  



## <a name="apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> Stuur programmapakket Toep assen  

Gebruik deze stap om alle Stuur Programma's in het stuur programmapakket te downloaden en te installeren op het Windows-besturings systeem.

Met de takenreeksstap **Stuurprogrammapakket toepassen** worden alle apparaatstuurprogramma's in een stuurprogrammapakket beschikbaar gemaakt voor gebruik door Windows. Voeg deze stap toe tussen de stappen **besturings systeem Toep assen** en **installatie van Windows en ConfigMgr** om de Stuur Programma's in het pakket beschikbaar te maken voor Windows. De takenreeksstap **Stuurprogrammapakket toepassen** is ook nuttig bij scenario's met implementatie van zelfstandige media.  

Plaats vergelijk bare apparaatstuurprogramma's in een stuur programmapakket en distribueer deze naar de juiste distributie punten. Plaats bijvoorbeeld alle Stuur Programma's van een fabrikant in een stuur programmapakket. Distribueer vervolgens het pakket naar distributie punten waar de bijbehorende computers toegang tot hebben.

De stap **Stuur programmapakket Toep assen** is handig voor zelfstandige media. Deze stap is ook handig voor het installeren van een specifieke set stuur Programma's. Deze typen Stuur Programma's zijn onder andere apparaten die niet door Windows Plug en Play worden gedetecteerd, zoals netwerk printers.  

Deze takenreeksstap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Stuur Programma's**en selecteert u **Stuur programmapakket Toep assen**.

> [!TIP]
> Zie [taken reeksen gebruiken om stuur Programma's te installeren](../get-started/manage-drivers.md#BKMK_TSDrivers)voor een overzicht van de Stuur programma's in Configuration Manager.
>
> Inhoud vooraf in cache opslaan gebruiken om een toepasselijk Stuur programmapakket te downloaden voordat een gebruiker de taken reeks installeert. Zie [inhoud vooraf in cache configureren](../deploy-use/configure-precache-content.md)voor meer informatie.

### <a name="variables-for-apply-driver-package"></a>Variabelen voor het Toep assen van Stuur programmapakket

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDApplyDriverBootCriticalContentUniqueID](task-sequence-variables.md#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](task-sequence-variables.md#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](task-sequence-variables.md#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](task-sequence-variables.md#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions)<!--516679/2840016-->

### <a name="cmdlets-for-apply-driver-package"></a>Cmdlets voor het Toep assen van Stuur programmapakket

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Get-CMTSStepApplyDriverPackage)
- [New-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/New-CMTSStepApplyDriverPackage)
- [Remove-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Remove-CMTSStepApplyDriverPackage)
- [Set-CMTSStepApplyDriverPackage](/powershell/module/configurationmanager/Set-CMTSStepApplyDriverPackage)

### <a name="properties-for-apply-driver-package"></a>Eigenschappen voor Stuur programmapakket Toep assen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="driver-package"></a>Stuurprogrammapakket

Geef het stuur programmapakket op dat de benodigde apparaatstuurprogramma's bevat. Selecteer **Bladeren** om het dialoog venster **pakket selecteren** te openen. Selecteer een bestaand Stuur programmapakket dat u wilt Toep assen. Onder in het dialoog venster worden de bijbehorende pakket eigenschappen weer gegeven.  

#### <a name="install-driver-package-via-running-dism-with-recurse-option"></a>Stuur programmapakket installeren door DISM uit te voeren met de optie recursief

Selecteer deze optie om de `/recurse` para meter toe te voegen aan de DISM-opdracht regel wanneer het stuur programmapakket door Windows wordt toegepast.

Wanneer u deze optie inschakelt, kunt u ook aanvullende DISM-opdracht regel parameters opgeven. Gebruik de taken reeks variabele [OSDInstallDriversAdditionalOptions](task-sequence-variables.md#OSDInstallDriversAdditionalOptions) om meer opties toe te voegen. Zie [opdracht regel opties voor Windows 10 DISM](/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options)voor meer informatie.<!-- SCCMDocs#2125 -->

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Selecteer het stuurprogramma voor massaopslag in het pakket dat moet worden geïnstalleerd vóór de installatie op besturingssystemen ouder dan Windows Vista.

Geef alle Stuur Programma's voor massa opslag op die nodig zijn om een klassiek besturings systeem te installeren.  

##### <a name="driver"></a>Stuurprogramma

Selecteer het stuur programma voor massa opslag dat moet worden geïnstalleerd vóór de installatie van een klassiek besturings systeem. De vervolg keuzelijst wordt gevuld vanuit het opgegeven pakket.  

##### <a name="model"></a>Model

Geef het apparaat op dat essentieel is voor het opstarten dat nodig is voor implementaties van besturings systemen van vóór Windows Vista.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Installatie zonder toezicht van niet-ondertekende stuurprogramma's uitvoeren op versie van Windows wanneer dit is toegestaan

Met deze optie kan Windows Stuur Programma's zonder digitale hand tekening installeren.  



## <a name="apply-network-settings"></a><a name="BKMK_ApplyNetworkSettings"></a> Netwerk instellingen Toep assen  

Gebruik deze stap om de configuratie gegevens van het netwerk of de werk groep op te geven voor de doel computer. De taken reeks slaat deze waarden op in het juiste antwoord bestand. Windows Setup gebruikt dit antwoord bestand tijdens de **installatie van Windows en ConfigMgr** .  

Deze takenreeksstap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **instellingen**en selecteert u **netwerk instellingen Toep assen**.

> [!NOTE]
> Als u meerdere exemplaren van deze stap in een taken reeks opneemt, zijn de voor waarden niet van toepassing. De instellingen van de laatste instantie van deze stap in de taken reeks worden toegepast op het apparaat. U kunt dit probleem omzeilen door elke stap in een afzonderlijke groep met voor waarden voor de groep op te lossen.

### <a name="variables-for-apply-network-settings"></a>Variabelen voor het Toep assen van netwerk instellingen

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDAdapter](task-sequence-variables.md#OSDAdapter)  
- [OSDAdapterCount](task-sequence-variables.md#OSDAdapterCount)  
- [OSDDNSDomain](task-sequence-variables.md#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](task-sequence-variables.md#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](task-sequence-variables.md#OSDDomainName)  
- [OSDDomainOUName](task-sequence-variables.md#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](task-sequence-variables.md#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDWorkgroupName](task-sequence-variables.md#OSDWorkgroupName)  

### <a name="cmdlets-for-apply-network-settings"></a>Cmdlets voor het Toep assen van netwerk instellingen

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyNetworkSetting)
- [New-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/New-CMTSStepApplyNetworkSetting)
- [Remove-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyNetworkSetting)
- [Set-CMTSStepApplyNetworkSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyNetworkSetting)

### <a name="properties-for-apply-network-settings"></a>Eigenschappen voor netwerk instellingen Toep assen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="join-a-workgroup"></a>Lid worden van een werkgroep

Selecteer deze optie om de doelcomputer toe te voegen aan de opgegeven werkgroep. Voer de naam van de werkgroep in op de regel **Werkgroep**. De waarde die wordt vastgelegd door de taken reeks stap **netwerk instellingen vastleggen** kan deze waarde overschrijven.

#### <a name="join-a-domain"></a>Lid worden van een domein

Selecteer deze optie om de doelcomputer toe te voegen aan het opgegeven domein. Geef op of blader naar het domein, zoals `fabricam.com` . Geef een LDAP-pad (Lightweight Directory Access Protocol) op of blader naar een organisatie-eenheid. Bijvoorbeeld: `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

> [!NOTE]
> Wanneer een client die lid is van een Azure Active Directory (Azure AD) een taken reeks voor besturingssysteem implementatie uitvoert, wordt de client in het nieuwe besturings systeem niet automatisch toegevoegd aan Azure AD. Hoewel het geen lid is van Azure AD, wordt de client nog steeds beheerd.

#### <a name="account"></a>Account

Selecteer **instellen** om een account op te geven met de vereiste machtigingen om de computer aan het domein toe te voegen. Voer in het dialoog venster **Windows-gebruikers account** de gebruikers naam in met de volgende indeling: `Domain\User` . Zie voor meer informatie [domein deelname aan account](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account).

#### <a name="adapter-settings"></a>Adapterinstellingen

Netwerkconfiguraties opgeven voor elke netwerkadapter in de computer. Selecteer **Nieuw** om het dialoog venster **netwerk instellingen** te openen en geef vervolgens de netwerk instellingen op.

- Als u ook de stap **netwerk instellingen vastleggen** gebruikt, past de taken reeks de eerder vastgelegde instellingen toe op de netwerk adapter.
- Als de taken reeks niet eerder netwerk instellingen heeft vastgelegd, worden de instellingen toegepast die u in deze stap opgeeft.
- De taken reeks past deze instellingen toe op netwerk adapters in volg orde van Windows-apparaatinventarisatie.  
- In de taken reeks worden de instellingen die u in deze stap opgeeft, niet onmiddellijk toegepast op de computer.



## <a name="apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> Installatie kopie van besturings systeem Toep assen  

Gebruik deze stap om een besturings systeem te installeren op de doel computer.

Nadat de actie **besturings systeem Toep assen** is uitgevoerd, wordt de variabele **OSDTargetSystemDrive** ingesteld op de stationsletter van de partitie die de besturingssysteem bestanden bevat.  

Deze takenreeksstap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **installatie kopieën**en selecteert u **installatie kopie van besturings systeem Toep assen**.

> [!TIP]
> Vanaf Windows 10, versie 1709, media bevat meerdere edities. Wanneer u een taken reeks configureert voor het gebruik van een upgrade pakket voor een besturings systeem of installatie kopie van een besturings systeem, moet u een [ondersteunde versie](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)selecteren.  
>
> Inhoud vooraf in cache opslaan gebruiken om een toepasselijk upgrade pakket voor het besturings systeem te downloaden voordat een gebruiker de taken reeks installeert. Zie [inhoud vooraf in cache configureren](../deploy-use/configure-precache-content.md)voor meer informatie.
>
> Met de stap **Windows en ConfigMgr installeren** wordt de installatie van Windows gestart.

### <a name="variables-for-apply-os-image"></a>Variabelen voor installatie kopie van besturings systeem Toep assen

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDConfigFileName](task-sequence-variables.md#OSDConfigFileName)  
- [OSDImageIndex](task-sequence-variables.md#OSDImageIndex)  
- [OSDTargetSystemDrive](task-sequence-variables.md#OSDTargetSystemDrive)  

### <a name="cmdlets-for-apply-os-image"></a>Cmdlets voor installatie kopie van besturings systeem Toep assen

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepApplyOperatingSystem)
- [New-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepApplyOperatingSystem)
- [Remove-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepApplyOperatingSystem)
- [Set-CMTSStepApplyOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepApplyOperatingSystem)

### <a name="behaviors-for-apply-os-image"></a>Gedrag voor installatie kopie van besturings systeem Toep assen

Met deze stap worden verschillende acties uitgevoerd, afhankelijk van of het een installatie kopie van een besturings systeem of een upgrade pakket voor het besturings systeem gebruikt.  

#### <a name="os-image-actions"></a>Acties van besturings systeem installatie kopieën

Met de stap **besturingssysteem installatie kopie Toep assen** worden de volgende acties uitgevoerd wanneer u een installatie kopie van een besturings systeem gebruikt:  

1. Verwijder alle inhoud op het doel volume, met uitzonde ring van de bestanden in de map die is opgegeven door de variabele ** \_ SMSTSUserStatePath** .  

2. Pak de inhoud van het opgegeven Wim-bestand uit naar de opgegeven doel partitie.  

3. Het antwoord bestand voorbereiden:  

    1. Maak een nieuw standaard Windows Setup antwoord bestand (Sysprep. inf of unattend.xml) voor het geïmplementeerde besturings systeem.  

    2. Alle waarden van het door de gebruiker opgegeven antwoord bestand samen voegen.  

4. Kopieer Windows-opstart laad Programma's naar de actieve partitie.  

5. Stel de boot.ini of de Boot Configuration Data Base (BCD) in om te verwijzen naar het zojuist geïnstalleerde besturings systeem.  

#### <a name="os-upgrade-package-actions"></a>Acties voor het upgrade pakket van het besturings systeem

Met de stap **besturingssysteem installatie kopie Toep assen** worden de volgende acties uitgevoerd wanneer u een upgrade pakket voor het besturings systeem gebruikt:  

1. Verwijder alle inhoud op het doel volume, met uitzonde ring van de bestanden in de map die is opgegeven door de variabele ** \_ SMSTSUserStatePath** .  

2. Het antwoord bestand voorbereiden:  

    1. Maak een nieuw antwoord bestand met standaard waarden die zijn gemaakt door Configuration Manager.  

    2. Alle waarden van het door de gebruiker opgegeven antwoord bestand samen voegen.  

### <a name="properties-for-apply-os-image"></a>Eigenschappen voor installatie kopie van besturings systeem Toep assen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Besturingssysteem toepassen vanuit een vastgelegd beeld

Hiermee installeert u een installatie kopie van het besturings systeem die u hebt vastgelegd. Selecteer **Bladeren** om het dialoog venster **pakket selecteren** te openen. Selecteer vervolgens het bestaande installatie kopie pakket dat u wilt installeren. Als er meerdere installatie kopieën zijn gekoppeld aan het opgegeven **installatie kopie pakket**, selecteert u in de vervolg keuzelijst de bijbehorende installatie kopie die u voor deze implementatie wilt gebruiken. U kunt basis informatie over elke bestaande installatie kopie weer geven door deze te selecteren.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Installatiekopie van besturingssysteem toepassen van een oorspronkelijke installatiebron

Installeert een besturings systeem met behulp van een upgrade pakket voor het besturings systeem, dat ook een originele installatie bron is. Selecteer **Bladeren** om het dialoog venster **een upgrade pakket voor het besturings systeem selecteren** te openen. Selecteer vervolgens het bestaande upgrade pakket voor het besturings systeem dat u wilt gebruiken. U kunt basis informatie over elke bestaande installatie kopie bron weer geven door deze te selecteren. In het resultaten venster onder in het dialoog venster worden de bijbehorende eigenschappen van de afbeeldings bron weer gegeven. Als er meerdere edities zijn gekoppeld aan het opgegeven pakket, gebruikt u de vervolg keuzelijst om de **editie** te selecteren die u wilt gebruiken.  

> [!NOTE]  
> **Upgrade pakketten voor besturings systemen** zijn voornamelijk bedoeld voor gebruik met in-place Upgrades en niet voor nieuwe installaties van Windows. Bij het implementeren van nieuwe installaties van Windows, gebruikt u de optie **besturings systeem Toep assen vanaf een vastgelegde installatie kopie** en **installeert u. Wim** vanuit de bron bestanden voor de installatie.
>
> Het implementeren van nieuwe installaties van Windows via **upgrade pakketten voor besturings systemen** wordt nog steeds ondersteund, maar is afhankelijk van Stuur Programma's die compatibel zijn met deze methode. Wanneer u Windows installeert vanuit een upgrade pakket voor het besturings systeem, worden er Stuur Programma's geïnstalleerd terwijl Windows PE nog steeds wordt toegevoegd in Windows PE. Sommige Stuur Programma's zijn niet compatibel met geïnstalleerd tijdens de installatie van Windows PE.
>
> Als Stuur Programma's niet compatibel zijn met die worden geïnstalleerd in Windows PE, maakt u een **installatie kopie van een besturings systeem** met de **install. Wim** vanaf de oorspronkelijke installatie bron bestanden. Implementeer vervolgens met behulp van de optie **besturings systeem Toep assen vanaf een vastgelegde installatie kopie** .

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Installatie zonder toezicht of Sysprep-antwoordbestand gebruiken voor aangepaste installatie

Gebruik deze optie om een Windows Setup-antwoord bestand (**unattend.xml**, **unattend.txt**of **Sysprep. inf**) te bieden, afhankelijk van de versie van het besturings systeem en de installatie methode. Het opgegeven bestand kan de standaardconfiguratieopties bevatten die worden ondersteund voor Windows-antwoordbestanden. Bijvoorbeeld: u kunt hiermee de standaardstartpagina voor Internet Explorer opgeven. Geef het pakket op dat het antwoord bestand bevat en het bijbehorende pad naar het bestand in het pakket.  

> [!NOTE]  
> Het Windows Setup-antwoord bestand dat u opgeeft kan Inge sloten taken reeks variabelen van het formulier bevatten `%varname%` , waarbij *varnaam* de naam van de variabele is. In de stap **Windows en ConfigMgr installeren** wordt de variabele String vervangen door de werkelijke waarde van de variabele. U kunt deze Inge sloten taken reeks variabelen niet gebruiken in velden die alleen numeriek zijn in een unattend.xml antwoord bestand.  

Als u geen Windows Setup-antwoord bestand opgeeft, genereert de taken reeks automatisch een antwoord bestand.  

#### <a name="destination"></a>Doel

Configureer een van de volgende opties:  

- **Volgende beschik bare partitie**: gebruik de volgende sequentiële partitie die niet al is gericht op de stap **besturings systeem Toep assen** of **gegevens installatie kopie** Toep assen in deze taken reeks.  

- **Specifieke schijf en partitie**: Selecteer het **schijf** nummer (te beginnen met 0) en het **partitie** nummer (te beginnen met 1).  

- **Specifieke logische stationsletter**: Geef de stationsletter op die door Windows PE **is toegewezen aan** de partitie. Deze stationsletter kan afwijken van de stationsletter die is toegewezen door het zojuist geïmplementeerde besturings systeem.  

- **Logische stationsletter opgeslagen in een variabele**: Geef de taken reeks variabele op met de stationsletter die door Windows PE is toegewezen aan de partitie. Deze variabele wordt meestal ingesteld in de sectie Geavanceerd van het dialoog venster **partitie-eigenschappen** voor de taken reeks stap **schijf Format teren en partitioneren** .  

### <a name="options-for-apply-os-image"></a>Opties voor installatie kopie van besturings systeem Toep assen

Naast de standaard opties configureert u de volgende extra instellingen op het tabblad **Opties** van deze taken reeks stap:  

#### <a name="access-content-directly-from-the-distribution-point"></a>Rechtstreeks vanaf het distributie punt toegang tot inhoud

Configureer de taken reeks voor toegang tot de installatie kopie van het besturings systeem rechtstreeks vanaf het distributie punt. Gebruik deze optie bijvoorbeeld wanneer u besturings systemen implementeert op Inge sloten apparaten met beperkte opslag capaciteit. Wanneer u deze optie selecteert, moet u ook de instellingen voor de pakket share configureren op het tabblad **gegevens toegang** van de eigenschappen van de installatie kopie van het besturings systeem.  

> [!NOTE]  
> Deze instelling overschrijft de implementatie optie die u configureert op de pagina **distributie punten** van de **wizard software implementeren**. Deze onderdrukking is alleen voor de installatie kopie van het besturings systeem die met deze stap wordt opgegeven, niet voor alle inhoud van de taken reeks.  

> [!IMPORTANT]  
> Voor de beste beveiliging is het raadzaam deze optie niet te selecteren. Deze optie is hoofd zakelijk ontworpen voor gebruik op apparaten met beperkte opslag capaciteit. Deze optie is niet bedoeld om de snelheid van de taken reeks te verg Roten. Als deze optie is geselecteerd, wordt de pakket-hash niet geverifieerd voor het besturingssysteem pakket. De pakket integriteit kan daarom niet worden gegarandeerd omdat gebruikers met beheerders rechten kunnen wijzigen of knoeien met de inhoud van het pakket.



## <a name="apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Windows-instellingen Toep assen

Gebruik deze stap om de Windows-instellingen voor de doel computer te configureren. De taken reeks slaat deze waarden op in het juiste antwoord bestand. Windows Setup gebruikt dit antwoord bestand tijdens de stap **Windows en ConfigMgr installeren** .  

Deze takenreeksstap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **instellingen**en selecteert u **Windows-instellingen Toep assen**.

### <a name="variables-for-apply-windows-settings"></a>Variabelen voor het Toep assen van Windows-instellingen

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-input)  
- [OSDLocalAdminPassword](task-sequence-variables.md#OSDLocalAdminPassword)  
- [OSDProductKey](task-sequence-variables.md#OSDProductKey)  
- [OSDRandomAdminPassword](task-sequence-variables.md#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](task-sequence-variables.md#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](task-sequence-variables.md#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](task-sequence-variables.md#OSDServerLicenseMode)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-input)  
- [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale)
- [OSDWindowsSettingsSystemLocale](task-sequence-variables.md#OSDWindowsSettingsSystemLocale)
- [OSDWindowsSettingsUILanguage](task-sequence-variables.md#OSDWindowsSettingsUILanguage)
- [OSDWindowsSettingsUILanguageFallback](task-sequence-variables.md#OSDWindowsSettingsUILanguageFallback)
- [OSDWindowsSettingsUserLocale](task-sequence-variables.md#OSDWindowsSettingsUserLocale)

### <a name="cmdlets-for-apply-windows-settings"></a>Cmdlets voor het Toep assen van Windows-instellingen

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [New-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Get-CMTSStepApplyWindowsSetting)
- [Remove-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Remove-CMTSStepApplyWindowsSetting)
- [Set-CMTSStepApplyWindowsSetting](/powershell/module/configurationmanager/Set-CMTSStepApplyWindowsSetting)

### <a name="properties-for-apply-windows-settings"></a>Eigenschappen voor het Toep assen van Windows-instellingen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="user-name"></a>Gebruikersnaam

Geef de geregistreerde gebruikers naam op die u wilt koppelen aan de doel computer. De waarde die wordt vastgelegd door de taken reeks stap **Windows-instellingen vastleggen** kan deze waarde overschrijven.  

#### <a name="organization-name"></a>Organisatienaam

Geef de naam van de geregistreerde organisatie op die u wilt koppelen aan de doel computer. De waarde die wordt vastgelegd door de taken reeks stap **Windows-instellingen vastleggen** kan deze waarde overschrijven.  

#### <a name="product-key"></a>Productcode  

Geef de product code op die moet worden gebruikt voor de installatie van Windows op de doel computer.  

#### <a name="server-licensing"></a>Serverlicentieverlening

Geef de serverlicentiemodus op.

- Selecteer **per server** of **per gebruiker** als de licentie modus.  
- Als u **per server**selecteert, geeft u ook het maximum aantal toegestane verbindingen op dat is toegestaan volgens uw licentie overeenkomst.  
- Als de doel computer geen server is of als u de licentie modus niet wilt opgeven, selecteert u **niet opgeven**.  

#### <a name="maximum-connections"></a>Maximum aantal verbindingen

> [!NOTE]
> Deze instelling is alleen van toepassing op oudere versies van Windows die niet meer worden ondersteund.<!-- #4833 -->

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Willekeurig wachtwoord genereren voor lokale beheerder en het account uitschakelen op alle ondersteunde platforms (aanbevolen)  

Selecteer deze optie om het wacht woord van de lokale beheerder in te stellen op een wille keurig gegenereerde teken reeks. Met deze optie wordt ook het lokale beheerders account uitgeschakeld op platforms die deze mogelijkheid ondersteunen.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Het account inschakelen en lokaal beheerderswachtwoord instellen  

Selecteer deze optie om het lokale beheerders account in te scha kelen met het opgegeven wacht woord. Voer het wachtwoord in op de regel **Wachtwoord** en bevestig het wachtwoord op de regel **Wachtwoord bevestigen**.  

#### <a name="time-zone"></a>Tijdzone

Geef de tijdzone op die u wilt configureren op de doelcomputer. De waarde die wordt vastgelegd door de taken reeks stap **Windows-instellingen vastleggen** kan deze waarde overschrijven.  

#### <a name="language-settings"></a>Taalinstellingen

<!--5411057, 5138936-->

Vanaf versie 1910 beheert u de taal configuratie tijdens de besturingssysteem implementatie. Als u deze taal instellingen al toepast, kan deze wijziging u helpen de taken reeks van de besturingssysteem implementatie te vereenvoudigen. In plaats van meerdere stappen per taal of afzonderlijke scripts te gebruiken, gebruikt u één exemplaar per taal van deze stap met een voor waarde voor die taal.

Configureer de volgende instellingen:

- Land instellingen voor invoer (standaard toetsenbord indeling)
- Systeem land instelling
- Taal van gebruikers interface
- Terugval taal gebruikers interface
- Land instellingen voor gebruiker

Zie [micro soft-Windows-International-core](/windows-hardware/customize/desktop/unattend/microsoft-windows-international-core)(Engelstalig) voor meer informatie over deze waarden voor Windows Setup-antwoord bestanden.

> [!NOTE]
> Als u een aangepast Windows Setup-antwoord bestand (unattend.xml) maakt, overschrijft deze stap alle bestaande waarden. Als u een dynamisch proces voor deze instellingen wilt automatiseren, gebruikt u de gerelateerde taken reeks variabelen. Bijvoorbeeld [OSDWindowsSettingsInputLocale](task-sequence-variables.md#OSDWindowsSettingsInputLocale). 

## <a name="auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> Stuur Programma's automatisch Toep assen

Gebruik deze stap om stuur Programma's te zoeken en te installeren als onderdeel van de implementatie van het besturings systeem.  

> [!IMPORTANT]  
> De stap **Stuur Programma's automatisch Toep assen** kan niet worden gebruikt voor zelfstandige media. De taken reeks heeft in dit scenario geen verbinding met de Configuration Manager-site.  

Deze takenreeksstap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Stuur**Programma's en selecteert u **Stuur Programma's automatisch Toep assen**.

> [!TIP]
> Zie [taken reeksen gebruiken om stuur Programma's te installeren](../get-started/manage-drivers.md#BKMK_TSDrivers)voor een overzicht van de Stuur programma's in Configuration Manager.

### <a name="behaviors-for-auto-apply-drivers"></a>Gedrag voor het automatisch Toep assen van Stuur Programma's

Met de takenreeksactie **Stuurprogramma's automatisch toepassen** worden de volgende acties uitgevoerd:  

1. Scan de hardware en zoek de Plug en Play-Id's van alle apparaten die aanwezig zijn op het systeem.  

2. De lijst met apparaten en hun Plug en Play-Id's verzenden naar het beheer punt. Het beheer punt retourneert een lijst met compatibele Stuur Programma's van de stuurprogrammacatalogus voor elk hardwareapparaat. De lijst bevat alle ingeschakelde Stuur Programma's, ongeacht het stuur programmapakket waarin ze zich bevinden en de Stuur Programma's die zijn gelabeld met de opgegeven categorie van het stuur programma.  

3. Voor elk hardwareapparaat kiest de taken reeks het beste stuur programma. Dit stuur programma is geschikt voor het geïmplementeerde besturings systeem en bevindt zich op een toegankelijk distributie punt.  

4. De taken reeks downloadt de geselecteerde Stuur Programma's van een distributie punt en de Stuur Programma's in het doel besturingssysteem.  

    1. Wanneer u een installatie kopie van een besturings systeem gebruikt, plaatst de taken reeks de Stuur Programma's in het stuur programma-archief van het besturings systeem.  

    2. Wanneer u een upgrade pakket voor het besturings systeem gebruikt als een oorspronkelijke installatie bron, configureert de taken reeks Windows Setup met de locatie van de Stuur Programma's.  

5. Tijdens de stap **Windows en ConfigMgr** in de taken reeks wordt Windows Setup de Stuur Programma's gevonden die door deze stap worden klaargezet.  

### <a name="variables-for-auto-apply-drivers"></a>Variabelen voor het automatisch Toep assen van Stuur Programma's

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDAutoApplyDriverBestMatch](task-sequence-variables.md#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](task-sequence-variables.md#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](task-sequence-variables.md#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](task-sequence-variables.md#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](task-sequence-variables.md#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](task-sequence-variables.md#SMSTSDriverRequestSendTimeOut)  

### <a name="cmdlets-for-auto-apply-drivers"></a>Cmdlets voor het automatisch Toep assen van Stuur Programma's

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Get-CMTSStepAutoApplyDriver)
- [New-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/New-CMTSStepAutoApplyDriver)
- [Remove-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Remove-CMTSStepAutoApplyDriver)
- [Set-CMTSStepAutoApplyDriver](/powershell/module/configurationmanager/Set-CMTSStepAutoApplyDriver)

### <a name="properties-for-auto-apply-drivers"></a>Eigenschappen voor Stuur Programma's automatisch Toep assen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Alleen de best overeenkomende compatibele stuurprogramma's installeren

Hiermee geeft u aan dat met de takenreeksstap alleen het beste overeenkomende stuurprogramma voor elk gedetecteerd apparaat wordt geïnstalleerd.  

#### <a name="install-all-compatible-drivers"></a>Alle compatibele stuurprogramma's installeren

De taken reeks installeert alle Stuur Programma's die compatibel zijn voor elk gedetecteerd hardwareapparaat. Windows Setup kiest vervolgens het beste stuur programma. Deze optie neemt meer netwerk bandbreedte en schijf ruimte in beslag. Met de taken reeks worden meer Stuur Programma's gedownload, maar Windows kan een beter stuur programma selecteren.  

#### <a name="consider-drivers-from-all-categories"></a>Stuurprogramma's uit alle categorieën overwegen

De taken reeks doorzoekt alle beschik bare categorieën van Stuur Programma's voor de juiste apparaatstuurprogramma's.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Zoeken naar passende stuurprogramma's beperken tot bepaalde categorieën

De taken reeks zoekt in de opgegeven Stuur Programma's naar de juiste apparaatstuurprogramma's.  

Als u meerdere categorieën selecteert, worden alle overeenkomende Stuur Programma's geretourneerd die in een van de categorieën aanwezig zijn. Het is gelijk aan een `OR` bewerking.<!-- SCCMDocs issue 851 -->

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Installatie zonder toezicht van niet-ondertekende stuurprogramma's uitvoeren in Windows-versies waar dit is toegestaan

Met deze optie kan Windows Stuur Programma's zonder digitale hand tekening installeren.  

> [!IMPORTANT]  
> Deze optie is niet van toepassing op besturings systemen waarop u het beleid voor ondertekening van Stuur Programma's niet kunt configureren.  



## <a name="capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> Netwerk instellingen vastleggen

Gebruik deze stap om de micro soft-netwerk instellingen vast te leggen van de computer waarop de taken reeks wordt uitgevoerd. De taken reeks slaat deze instellingen op in taken reeks variabelen. Deze instellingen overschrijven de standaard instellingen die u configureert in de stap **netwerk instellingen Toep assen** .  

Deze taken reeks stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **instellingen**en selecteert u **netwerk instellingen vastleggen**.

### <a name="variables-for-capture-network-settings"></a>Variabelen voor het vastleggen van netwerk instellingen

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDMigrateAdapterSettings](task-sequence-variables.md#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](task-sequence-variables.md#OSDMigrateNetworkMembership)  

### <a name="cmdlets-for-capture-network-settings"></a>Cmdlets voor het vastleggen van netwerk instellingen

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureNetworkSettings)
- [New-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureNetworkSettings)
- [Remove-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureNetworkSettings)
- [Set-CMTSStepCaptureNetworkSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureNetworkSettings)

### <a name="properties-for-capture-network-settings"></a>Eigenschappen voor het vastleggen van netwerk instellingen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Lidmaatschap van domein en werkgroep migreren

Hiermee worden de lidmaatschapsgegevens van het domein en de werkgroep van de doelcomputer vastgelegd.  

#### <a name="migrate-network-adapter-configuration"></a>Configuratie netwerkadapter migreren

Hiermee wordt de netwerkadapterconfiguratie van de doelcomputer vastgelegd. De volgende informatie wordt vastgelegd:

- Globale netwerk instellingen  
- Aantal adapters  
- De volgende netwerk instellingen die zijn gekoppeld aan elke adapter: DNS, WINS, IP en poort filters



## <a name="capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Installatie kopie van het besturings systeem vastleggen

In deze stap worden een of meer installatie kopieën van een referentie computer vastgelegd. De taken reeks maakt een Windows-installatie kopie bestand (. Wim) op de opgegeven netwerk share. Gebruik vervolgens de wizard **installatie kopie pakket van besturings systeem toevoegen** om deze installatie kopie te importeren in Configuration Manager voor besturingssysteem implementaties op basis van een installatie kopie.  

Configuration Manager elk volume (station) van de referentie computer wordt vastgelegd naar een afzonderlijke installatie kopie binnen het WIM-bestand. Als de computer waarnaar wordt verwezen meerdere volumes heeft, bevat het resulterende. WIM-bestand een afzonderlijke installatie kopie voor elk volume. Met deze stap worden alleen volumes vastgelegd die zijn geformatteerd als NTFS of FAT32. Volumes met andere indelingen en USB-volumes worden overgeslagen.  

Het geïnstalleerde besturings systeem op de referentie computer moet een versie van Windows zijn die Configuration Manager ondersteunt. Gebruik het hulp programma SysPrep om het besturings systeem op de referentie computer voor te bereiden. Het geïnstalleerde besturingssysteem volume en het opstart volume moeten hetzelfde volume zijn.  

Geef een account op met schrijf machtigingen voor de geselecteerde netwerk share. Zie [accounts](../../core/plan-design/hierarchy/accounts.md#capture-os-image-account)voor meer informatie over de installatie kopie van het besturings systeem.

Deze takenreeksstap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **installatie kopieën**en selecteert u **installatie kopie van het besturings systeem vastleggen**.

### <a name="variables-for-capture-os-image"></a>Variabelen voor het vastleggen van installatie kopie van het besturings systeem

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDCaptureAccount](task-sequence-variables.md#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](task-sequence-variables.md#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](task-sequence-variables.md#OSDCaptureDestination)  
- [OSDImageCreator](task-sequence-variables.md#OSDImageCreator)  
- [OSDImageDescription](task-sequence-variables.md#OSDImageDescription)  
- [OSDImageVersion](task-sequence-variables.md#OSDImageVersion)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-input)  

### <a name="cmdlets-for-capture-os-image"></a>Cmdlets voor het vastleggen van de installatie kopie van het besturings systeem

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Get-CMTSStepCaptureSystemImage)
- [New-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/New-CMTSStepCaptureSystemImage)
- [Remove-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Remove-CMTSStepCaptureSystemImage)
- [Set-CMTSStepCaptureSystemImage](/powershell/module/configurationmanager/Set-CMTSStepCaptureSystemImage)

### <a name="properties-for-capture-os-image"></a>Eigenschappen voor de installatie kopie van het besturings systeem vastleggen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="target"></a>Doel  

Bestandssysteempad naar de locatie die Configuration Manager gebruikt bij het opslaan van de vastgelegde installatie kopie van het besturings systeem.  

#### <a name="description"></a>Beschrijving  

Een optionele, door de gebruiker gedefinieerde beschrijving van de vastgelegde installatie kopie van het besturings systeem die is opgeslagen in het installatie kopie bestand.  

#### <a name="version"></a>Versie  

Een optioneel, door de gebruiker gedefinieerd versie nummer om toe te wijzen aan de vastgelegde installatie kopie van het besturings systeem. Deze waarde kan een wille keurige combi natie van letters en cijfers zijn. Deze wordt opgeslagen in het afbeeldings bestand.  

#### <a name="created-by"></a>Gemaakt door  

De optionele naam van de gebruiker die de installatie kopie van het besturings systeem heeft gemaakt. Deze wordt opgeslagen in het afbeeldings bestand.  

#### <a name="capture-operating-system-image-account"></a>Account voor het vastleggen van een besturingssysteeminstallatiekopie  

Geef het Windows-account op dat machtigingen heeft voor de opgegeven netwerk share. Selecteer **instellen** om de naam van het Windows-account op te geven.  



## <a name="capture-user-state"></a><a name="BKMK_CaptureUserState"></a> Gebruikers status vastleggen

Deze stap maakt gebruik van de Hulpprogramma voor migratie van gebruikersstatus (USMT) om de gebruikers status en instellingen vast te leggen van de computer waarop de taken reeks wordt uitgevoerd. Deze takenreeksstap wordt gebruikt in combinatie met de takenreeksstap **Gebruikersstatus herstellen**. Met deze stap wordt altijd de USMT-status opslag versleuteld met behulp van een versleutelings sleutel die Configuration Manager gegenereerd en beheerd.  

Zie [gebruikers status beheren](../get-started/manage-user-state.md)voor meer informatie over het beheren van de gebruikers status bij het implementeren van besturings systemen.  

Als u de instellingen voor de gebruikers status van een status migratie punt wilt opslaan en herstellen, gebruikt u deze stap met de stappen status **opslag opvragen** en **status opslag vrijgeven** .  

Deze stap biedt controle over een beperkte subset van de meest gebruikte USMT-opties. Geef aanvullende opdracht regel opties op met behulp van de taken reeks variabele **taken osdmigrateadditionalcaptureoptions** .  

Deze takenreeksstap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **gebruikers status**en selecteert u **gebruikers status vastleggen**.

### <a name="variables-for-capture-user-state"></a>Variabelen voor het vastleggen van de gebruikers status

Gebruik de volgende taken reeks variabelen met deze stap:  

- [_OSDMigrateUsmtPackageID](task-sequence-variables.md#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](task-sequence-variables.md#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](task-sequence-variables.md#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](task-sequence-variables.md#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](task-sequence-variables.md#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](task-sequence-variables.md#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-capture-user-state"></a>Cmdlets voor het vastleggen van de gebruikers status

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Get-CMTSStepCaptureUserState)
- [New-CMTSStepCaptureUserState](/powershell/module/configurationmanager/New-CMTSStepCaptureUserState)
- [Remove-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Remove-CMTSStepCaptureUserState)
- [Set-CMTSStepCaptureUserState](/powershell/module/configurationmanager/Set-CMTSStepCaptureUserState)

### <a name="properties-for-capture-user-state"></a>Eigenschappen voor het vastleggen van de gebruikers status

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="user-state-migration-tool-package"></a>Pakket migratieprogramma gebruikersstatus

Geef het pakket op dat de Hulpprogramma voor migratie van gebruikersstatus bevat (USMT). De taken reeks gebruikt deze versie van USMT om de gebruikers status en instellingen vast te leggen. Voor dit pakket is geen programma vereist. Geef een pakket op dat de 32-bits of 64-bits versie van USMT bevat. De architectuur van USMT is afhankelijk van de architectuur van het besturings systeem van waaruit de taken reeks wordt vastgelegd.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Alle gebruikersprofielen vastleggen met standaardopties

Alle gebruikers profiel gegevens migreren. Dit is de standaardoptie.  

Als u deze optie selecteert, maar niet selecteert **gebruikers profielen lokale computer herstellen** in de stap **gebruikers status herstellen** , mislukt de taken reeks. Configuration Manager kunt de nieuwe accounts niet migreren zonder dat ze een wacht woord hoeven toe te wijzen.

Wanneer u de optie **een bestaand installatie kopie pakket installeren** van de wizard **nieuwe taken reeks** gebruikt, wordt de resulterende taken reeks standaard ingesteld op **alle gebruikers profielen vastleggen met standaard opties**. Deze standaard taken reeks selecteert de optie voor het **herstellen van gebruikers profielen voor lokale computers**of niet-domein gebruikers accounts.  

Selecteer **gebruikers profielen lokale computer herstellen** en geef een wacht woord op voor het account dat moet worden gemigreerd. In een hand matig gemaakte taken reeks is deze instelling te vinden onder de stap **gebruikers status herstellen** . In een takenreeks die is gemaakt door de wizard **Nieuwe takenreeks maken** is deze instelling te vinden op de wizardpagina voor de stap **Gebruikersbestanden en -instellingen herstellen**.  

Als u geen lokale gebruikers accounts hebt, is deze instelling niet van toepassing.  

#### <a name="customize-how-user-profiles-are-captured"></a>Vastleggen van gebruikersprofielen aanpassen

Selecteer deze optie om een aangepast profiel bestand op te geven voor migratie. Selecteer **bestanden** om de configuratie bestanden voor USMT te selecteren die met deze stap moeten worden gebruikt. Geef een aangepast. XML-bestand op dat regels bevat waarmee de gebruikers status bestanden worden gedefinieerd die moeten worden gemigreerd.  

#### <a name="click-here-to-select-configuration-files"></a>Klik hier om configuratie bestanden te selecteren

Selecteer deze optie om de configuratiebestanden in het USMT-pakket te selecteren die u wilt gebruiken voor het vastleggen van gebruikersprofielen. Selecteer de knop **bestanden** om het dialoog venster **configuratie bestanden** te openen. Als u een configuratie bestand wilt opgeven, voert u de naam van het bestand op de regel **Bestands** naam in en selecteert u de knop **toevoegen** .  

#### <a name="enable-verbose-logging"></a>Uitgebreide logboekregistratie inschakelen

Schakel deze optie in om meer gedetailleerde informatie in het logboekbestand te genereren. Bij het vastleggen van de status genereert de taken reeks standaard **Scan State. log** in de map taken reeks logboek `%WinDir%\ccm\logs` .  

#### <a name="skip-files-using-encrypted-file-system"></a>Bestanden met Encrypted File System overslaan

Schakel deze optie in om het vastleggen van bestanden die zijn versleuteld met het versleutelde bestands systeem (EFS) over te slaan. Deze bestanden bevatten gebruikers profiel bestanden. Afhankelijk van het besturings systeem en de USMT-versie zijn versleutelde bestanden mogelijk niet leesbaar na het herstellen. Zie de USMT-documentatie voor meer informatie.  

#### <a name="copy-by-using-file-system-access"></a>Kopiëren door toegang tot bestandssysteem

Schakel deze optie in om een van de volgende instellingen op te geven:  

- **Door gaan als sommige bestanden niet kunnen worden vastgelegd**: Schakel deze instelling in om verder te gaan met het migratie proces, zelfs als er geen bestanden kunnen worden vastgelegd. Als u deze optie uitschakelt en een bestand niet kan worden vastgelegd, mislukt deze stap. Deze optie is standaard ingeschakeld.  

- **Lokaal vastleggen met koppelingen in plaats van door bestanden te kopiëren**: schakel deze instelling in om bestanden met vaste NTFS-koppelingen vast te leggen.  

    Zie [hard link Migration Store (Engelstalig](/windows/deployment/usmt/usmt-hard-link-migration-store)) voor meer informatie over het migreren van gegevens met behulp van vaste koppelingen.  

- **Vastleggen in offline modus (alleen Windows PE)**: Schakel deze instelling in om de gebruikers status vast te leggen in Windows PE in plaats van het volledige besturings systeem.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Vastleggen met behulp van Volume Copy Shadow Service (VSS)

Met deze optie kunt u bestanden vastleggen, zelfs als deze zijn vergrendeld voor bewerking door een andere toepassing.  



## <a name="capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Windows-instellingen vastleggen

Gebruik deze stap om de Windows-instellingen vast te leggen van de computer waarop de taken reeks wordt uitgevoerd. De taken reeks slaat deze instellingen op in taken reeks variabelen. Deze vastgelegde instellingen overschrijven de standaard instellingen die u configureert in de stap **Windows-instellingen Toep assen** .  

Deze taken reeks stap wordt uitgevoerd in Windows PE of het volledige besturings systeem.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **instellingen**en selecteert u **Windows-instellingen vastleggen**.

### <a name="variables-for-capture-windows-settings"></a>Variabelen voor het vastleggen van Windows-instellingen

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDComputerName](task-sequence-variables.md#OSDComputerName-output)  
- [OSDMigrateComputerName](task-sequence-variables.md#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](task-sequence-variables.md#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](task-sequence-variables.md#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](task-sequence-variables.md#OSDRegisteredOrgName-output)  
- [OSDTimeZone](task-sequence-variables.md#OSDTimeZone-output)  

### <a name="cmdlets-for-capture-windows-settings"></a>Cmdlets voor het vastleggen van Windows-instellingen

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Get-CMTSStepCaptureWindowsSettings)
- [New-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/New-CMTSStepCaptureWindowsSettings)
- [Remove-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Remove-CMTSStepCaptureWindowsSettings)
- [Set-CMTSStepCaptureWindowsSettings](/powershell/module/configurationmanager/Set-CMTSStepCaptureWindowsSettings)

### <a name="properties-for-capture-windows-settings"></a>Eigenschappen voor het vastleggen van Windows-instellingen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="migrate-computer-name"></a>Computernaam migreren

Leg de NetBIOS-computer naam van de computer vast.  

#### <a name="migrate-registered-user-and-organization-names"></a>Geregistreerde namen van gebruikers en organisaties migreren

Leg de geregistreerde namen van de gebruiker en organisatie vast van de computer.  

#### <a name="migrate-time-zone"></a>Tijdzone migreren

Leg de tijd zone-instelling op de computer vast.  


## <a name="check-readiness"></a><a name="BKMK_CheckReadiness"></a> Gereedheid controleren

Gebruik deze stap om te controleren of de doel computer voldoet aan de opgegeven voor waarden voor de implementatie vereisten.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert u **gereedheid controleren**.

Vanaf versie 2002 bevat deze stap acht nieuwe controles. Geen van deze nieuwe controles wordt standaard geselecteerd in nieuwe of bestaande exemplaren van de stap.<!--6005561--> Zie de specifieke secties hieronder voor meer informatie over elke controle.

- **Architectuur van het huidige besturings systeem**
- **Minimale versie van het besturingssysteem**
- **Maximale versie van het besturingssysteem**
- **Minimale client versie**
- **Taal van het huidige besturings systeem**
- **Netstroom aangesloten**
- **Netwerk adapter verbonden**
  - **Netwerk adapter is niet draadloos**

Vanaf versie 2006 is deze stap inclusief een controle om te bepalen of het apparaat gebruikmaakt van UEFI, de **computer bevindt zich in de UEFI-modus**.<!--6452769-->

> [!IMPORTANT]
> Als u deze nieuwe functie Configuration Manager wilt gebruiken, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

Het **bestand smsts. log** bevat het resultaat van alle controles. Als één controle mislukt, blijft de taken reeks engine de andere controles evalueren. De stap mislukt totdat alle controles zijn voltooid. Als ten minste één controle mislukt, wordt de stap mislukt en wordt fout code **4316**geretourneerd. Deze fout code wordt omgezet in ' de resource die vereist is voor deze bewerking bestaat niet. '

### <a name="variables-for-check-readiness"></a>Variabelen voor de gereedheid controleren

Gebruik de volgende taken reeks variabelen met deze stap:  

- [_TS_CRMEMORY](task-sequence-variables.md#TSCRMEMORY)
- [_TS_CRSPEED](task-sequence-variables.md#TSCRSPEED)
- [_TS_CRDISK](task-sequence-variables.md#TSCRDISK)
- [_TS_CROSTYPE](task-sequence-variables.md#TSCROSTYPE)
- [_TS_CRARCH](task-sequence-variables.md#TSCRARCH) (vanaf versie 2002)
- [_TS_CRMINOSVER](task-sequence-variables.md#TSCRMINOSVER) (vanaf versie 2002)
- [_TS_CRMAXOSVER](task-sequence-variables.md#TSCRMAXOSVER) (vanaf versie 2002)
- [_TS_CRCLIENTMINVER](task-sequence-variables.md#TSCRCLIENTMINVER) (vanaf versie 2002)
- [_TS_CROSLANGUAGE](task-sequence-variables.md#TSCROSLANGUAGE) (vanaf versie 2002)
- [_TS_CRACPOWER](task-sequence-variables.md#TSCRACPOWER) (vanaf versie 2002)
- [_TS_CRNETWORK](task-sequence-variables.md#TSCRNETWORK) (vanaf versie 2002)
- [_TS_CRUEFI](task-sequence-variables.md#TSCRUEFI) (vanaf versie 2006)
- [_TS_CRWIRED](task-sequence-variables.md#TSCRWIRED) (vanaf versie 2002)

### <a name="cmdlets-for-check-readiness"></a>Cmdlets voor de gereedheid controleren

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Get-CMTSStepPrestartCheck)
- [New-CMTSStepPrestartCheck](/powershell/module/configurationmanager/New-CMTSStepPrestartCheck)
- [Remove-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Remove-CMTSStepPrestartCheck)
- [Set-CMTSStepPrestartCheck](/powershell/module/configurationmanager/Set-CMTSStepPrestartCheck)

### <a name="properties-for-check-readiness"></a>Eigenschappen voor de gereedheid controleren

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="minimum-memory-mb"></a>Mini maal geheugen (MB)

Controleer of de hoeveelheid geheugen, in mega bytes (MB), voldoet aan of groter is dan de opgegeven hoeveelheid. Met deze stap wordt deze instelling standaard ingeschakeld.  

#### <a name="minimum-processor-speed-mhz"></a>Minimale processor snelheid (MHz)  

Controleer of de snelheid van de processor, in Mega Hertz (MHz), voldoet aan of groter is dan de opgegeven hoeveelheid. Met deze stap wordt deze instelling standaard ingeschakeld.  

#### <a name="minimum-free-disk-space-mb"></a>Minimale vrije schijf ruimte (MB)

Controleer of de hoeveelheid beschik bare schijf ruimte, in mega bytes (MB), voldoet aan of groter is dan de opgegeven hoeveelheid.  

#### <a name="current-os-to-be-refreshed-is"></a>Het huidige besturings systeem dat moet worden vernieuwd, is

Controleer of het besturings systeem dat is geïnstalleerd op de doel computer voldoet aan de opgegeven vereiste. De stap stelt deze instelling standaard in op **client** .  

#### <a name="architecture-of-current-os"></a>Architectuur van het huidige besturings systeem

Controleer vanaf versie 2002 of het huidige besturings systeem **32-bits** of **64-bits**is.

#### <a name="minimum-os-version"></a>Minimale versie van het besturingssysteem

Controleer vanaf versie 2002 of op het huidige besturings systeem een versie wordt uitgevoerd die hoger is dan is opgegeven. Geef de versie op met de primaire versie, de secundaire versie en het buildnummer. Bijvoorbeeld `10.0.16299`.

#### <a name="maximum-os-version"></a>Maximale versie van het besturingssysteem

Controleer vanaf versie 2002 of op het huidige besturings systeem een eerdere versie wordt uitgevoerd dan is opgegeven. Geef de versie op met de primaire versie, de secundaire versie en het buildnummer. Bijvoorbeeld `10.0.18356`.

#### <a name="minimum-client-version"></a>Minimale client versie

Controleer vanaf versie 2002 of de versie van de Configuration Manager-client ten minste de opgegeven versie is. Geef de client versie op in de volgende indeling: `5.00.8913.1005` .

#### <a name="language-of-current-os"></a>Taal van het huidige besturings systeem

Start in versie 2002, Controleer of de huidige taal van het besturings systeem overeenkomt met wat u opgeeft. Selecteer de naam van de taal en de stap vergelijkt de bijbehorende taal code. Met deze controle vergelijkt u de taal die u hebt geselecteerd voor de eigenschap **OSLanguage** van de WMI-klasse **Win32_OperatingSystem** op de client.

#### <a name="ac-power-plugged-in"></a>Netstroom aangesloten

Start in versie 2002, Controleer of het apparaat is aangesloten op en niet op accu.

#### <a name="network-adapter-connected"></a>Netwerk adapter verbonden

Controleer vanaf versie 2002 of het apparaat een netwerk adapter heeft die is verbonden met het netwerk. U kunt ook de afhankelijke controle selecteren om te controleren of de **netwerk adapter niet draadloos is**.

#### <a name="computer-is-in-uefi-mode"></a>Computer bevindt zich in de UEFI-modus

Bepaal vanaf versie 2006 of het apparaat is geconfigureerd voor UEFI of BIOS.

### <a name="options-for-check-readiness"></a>Opties voor de gereedheid controleren

> [!NOTE]  
> Als u de instelling **door gaan bij fout** op het tabblad **Opties** van deze stap inschakelt, worden alleen de resultaten van de gereedheids controle vastgelegd. Als een controle mislukt, wordt de taken reeks niet gestopt.  



## <a name="connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> Verbinding maken met netwerkmap

Gebruik deze stap om een verbinding te maken met een gedeelde netwerkmap.  

Deze taken reeks stap wordt uitgevoerd in het volledige besturings systeem of Windows PE.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert **u verbinding maken met netwerkmap**.

### <a name="variables-for-connect-to-network-folder"></a>Variabelen voor verbinding maken met netwerkmap

Gebruik de volgende taken reeks variabelen met deze stap:  

- [SMSConnectNetworkFolderAccount](task-sequence-variables.md#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](task-sequence-variables.md#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](task-sequence-variables.md#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](task-sequence-variables.md#SMSConnectNetworkFolderPath)  

### <a name="cmdlets-for-connect-to-network-folder"></a>Cmdlets voor verbinding maken met netwerkmap

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Get-CMTSStepConnectNetworkFolder)
- [New-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/New-CMTSStepConnectNetworkFolder)
- [Remove-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Remove-CMTSStepConnectNetworkFolder)
- [Set-CMTSStepConnectNetworkFolder](/powershell/module/configurationmanager/Set-CMTSStepConnectNetworkFolder)

### <a name="properties-for-connect-to-network-folder"></a>Eigenschappen voor verbinding maken met netwerkmap

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="path"></a>Pad  

Selecteer **Bladeren** om het pad naar de netwerkmap op te geven. Gebruik de indeling `\\server\share`.

#### <a name="drive"></a>Station  

Selecteer de stationsletter van het lokale station die u wilt toewijzen voor deze verbinding.

#### <a name="account"></a>Account

Selecteer **instellen** om het gebruikers account op te geven met machtigingen om verbinding te maken met deze netwerkmap. Zie [accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-network-folder-connection-account)voor meer informatie over het verbindings account voor de taken reeks netwerkmap.



## <a name="disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> BitLocker uitschakelen

Gebruik deze stap om BitLocker-versleuteling uit te scha kelen op het huidige besturingssysteem station of op een specifiek station. Met deze actie blijven de sleutel beveiligingen zichtbaar in Lees bare tekst op de vaste schijf. De inhoud van het station wordt niet ontsleuteld. Deze actie is bijna onmiddellijk voltooid.  

> [!NOTE]  
> BitLocker-stationsversleuteling biedt versleuteling op laag niveau van de inhoud van een schijfvolume.  

Als u meerdere versleutelde stations hebt, moet u BitLocker uitschakelen op alle gegevens stations voordat u BitLocker uitschakelt op het station van het besturings systeem.  

Deze stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **schijven**en selecteert u **BitLocker uitschakelen**.

### <a name="variables-for-disable-bitlocker"></a>Variabelen voor uitschakelen van BitLocker

Met ingang van versie 1906 gebruikt u de volgende taken reeks variabelen met deze stap:  

- [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount)  
- [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride)  

### <a name="cmdlets-for-disable-bitlocker"></a>Cmdlets voor het uitschakelen van BitLocker

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepDisableBitLocker)
- [New-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/New-CMTSStepDisableBitLocker)
- [Remove-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepDisableBitLocker)
- [Set-CMTSStepDisableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepDisableBitLocker)

### <a name="properties-for-disable-bitlocker"></a>Eigenschappen voor uitschakelen van BitLocker

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="current-operating-system-drive"></a>Huidig besturingssysteemstation

BitLocker wordt uitgeschakeld op het huidige station van het besturings systeem.  

#### <a name="specific-drive"></a>Specifiek station  

Hiermee wordt BitLocker uitgeschakeld op een specifiek station. Gebruik de vervolgkeuzelijst om het station op te geven waarop BitLocker wordt uitgeschakeld.  

#### <a name="resume-protection-after-windows-has-been-restarted-the-specified-number-of-times"></a>De beveiliging hervatten nadat Windows het opgegeven aantal keren opnieuw is opgestart

<!-- 4512937 -->
Met ingang van versie 1906, gebruikt u deze optie om het aantal herstartingen op te geven dat BitLocker moet blijven uitschakelen. In plaats van meerdere exemplaren van deze stap toe te voegen, stelt u een waarde in tussen 1 (standaard) en 15.

U kunt dit gedrag instellen en wijzigen met behulp van de taken reeks variabelen [OSDBitLockerRebootCount](task-sequence-variables.md#OSDBitLockerRebootCount) en [OSDBitLockerRebootCountOverride](task-sequence-variables.md#OSDBitLockerRebootCountOverride).


## <a name="download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> Pakket inhoud downloaden

Gebruik deze stap om een van de volgende pakket typen te downloaden:  

- Installatiekopieën van het besturingssysteem  
- OS-upgrade pakketten  
- Driverpakketten  
- Pakketten  
- Installatie kopieën <sup> [Opmerking 1](#bkmk_note1)</sup>  

Deze stap werkt goed in een taken reeks om een besturings systeem bij te werken in de volgende scenario's:  

- Een enkele takenreeks gebruiken voor een upgrade die voor zowel x86- als x64-platforms werkt. Voeg twee stappen **pakket inhoud downloaden** toe aan de groep **voor bereiding van de upgrade** . Geef voor waarden op het tabblad **Opties** op om de client architectuur te detecteren en down load alleen het juiste upgrade pakket voor het besturings systeem. Configureer elke stap **pakket inhoud downloaden** om dezelfde variabele te gebruiken. Gebruik de variabele voor het mediapad in de stap **besturings systeem bijwerken** .  

- Als u een geschikt stuurprogrammapakket wilt downloaden, gebruikt u twee **Pakketinhoud downloaden**-stappen op voorwaarde dat het juiste hardwaretype wordt gedetecteerd voor elk stuurprogrammapakket. Configureer elke stap **pakket inhoud downloaden** om dezelfde variabele te gebruiken. Gebruik de variabele voor de waarde voor **gefaseerde inhoud** in het gedeelte Stuur Programma's van de stap **besturings systeem bijwerken** .  

> [!NOTE]  
> Wanneer u een taken reeks implementeert die deze stap bevat, selecteert u niet **alle inhoud lokaal downloaden voordat u de taken reeks start** of **rechtstreeks vanuit een distributie punt toegang tot inhoud** **op de** pagina **distributie punten** van de wizard software implementeren.  

Deze stap wordt uitgevoerd in het volledige besturings systeem of in Windows PE. De optie om het pakket op te slaan in de cache van de Configuration Manager-client wordt niet ondersteund in Windows PE.

> [!NOTE]  
> De taak **pakket inhoud downloaden** wordt niet ondersteund voor gebruik met zelfstandige media. Zie [niet-ondersteunde acties voor zelfstandige media](../deploy-use/create-stand-alone-media.md#unsupported-actions-for-stand-alone-media)voor meer informatie.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Software**en selecteert u **pakket inhoud downloaden**.

### <a name="cmdlets-for-download-package-content"></a>Cmdlets voor het downloaden van pakket inhoud

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Get-CMTSStepDownloadPackageContent)
- [New-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/New-CMTSStepDownloadPackageContent)
- [Remove-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Remove-CMTSStepDownloadPackageContent)
- [Set-CMTSStepDownloadPackageContent](/powershell/module/configurationmanager/Set-CMTSStepDownloadPackageContent)

### <a name="properties-for-download-package-content"></a>Eigenschappen voor pakket inhoud downloaden

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="select-package"></a>Pakket selecteren  

Selecteer het pictogram om het pakket te kiezen dat u wilt downloaden. Nadat u een pakket hebt gekozen, selecteert u het pictogram opnieuw om een ander pakket te kiezen.  

#### <a name="place-into-the-following-location"></a>Op de volgende locatie plaatsen

Kies ervoor om het pakket op te slaan op een van de volgende locaties:  

- **Werkmap voor taken reeksen**: deze locatie wordt ook wel de taken reeks cache genoemd.  

- **Configuration Manager-client cache**: gebruik deze optie om de inhoud in de client cache op te slaan. Dit pad is standaard `%WinDir%\ccmcache` .  

- **Aangepast pad**: de taken reeks engine downloadt eerst het pakket naar de werkmap van de taken reeks. Vervolgens wordt de inhoud verplaatst naar dit pad dat u opgeeft. De taken reeks engine voegt het pad toe met de pakket-ID.  

#### <a name="save-path-as-a-variable"></a>Pad opslaan als een variabele

Sla het pad van het pakket op in een aangepaste taken reeks variabele. Gebruik deze variabele vervolgens in een andere taken reeks stap.

Configuration Manager voegt een numeriek achtervoegsel toe aan de naam van de variabele. U kunt bijvoorbeeld een variabele opgeven `%MyContent%` als een aangepaste variabele. Het is de hoofdmap waar de taken reeks alle inhoud waarnaar wordt verwezen voor deze stap opslaat. Deze inhoud kan meerdere pakketten bevatten. Wanneer u naar de variabele verwijst, voegt u een numeriek achtervoegsel toe. Raadpleeg voor het eerste pakket `%MyContent01%` . Wanneer u in de volgende stappen naar de variabele verwijst, zoals **besturings systeem bijwerken**, gebruikt u `%MyContent02%` of `%MyContent03%` , waarbij het nummer overeenkomt met de volg orde waarin de pakketten worden weer gegeven in de stap **pakket inhoud downloaden** .  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>Als het downloaden van een pakket mislukt, ga dan door met het downloaden van andere pakketten in de lijst

Als de taken reeks een pakket niet kan downloaden, begint het met het downloaden van het volgende pakket in de lijst.  

### <a name="note-1-use-of-boot-images-in-the-download-package-content-step"></a><a name="bkmk_note1"></a> Opmerking 1: het gebruik van opstart installatie kopieën in de stap pakket inhoud downloaden

*Van toepassing op versie 1910 en hoger*<!-- SCCMDocs-pr #4202 -->

Als u de [taken reeks eigenschappen](../deploy-use/manage-task-sequences-to-automate-tasks.md#bkmk_prop-advanced) configureert om **een opstart installatie kopie te gebruiken**, is het toevoegen van een opstart installatie kopie aan deze stap overbodig. Voeg alleen een installatie kopie toe aan deze stap als deze niet is opgegeven in de eigenschappen van de taken reeks.

#### <a name="example-use-case"></a>Voorbeeld van een toepassing

- Een enkele taken reeks voor het vooraf downloaden van inhoud:
  - Geen gekoppelde opstart installatie kopie.
  - Wordt alleen uitgevoerd in het volledige besturings systeem, waarschijnlijk zonder tussen komst van de gebruiker.
  - Maakt gebruik van meerdere stappen voor het **downloaden van pakket inhoud** met voor waarden. Afhankelijk van de specifieke taal en architectuur, downloadt de inhoud naar de client cache om voor te bereiden voor de taken reeks voor de implementatie van het besturings systeem.
  - Er is slechts één exemplaar van deze taken reeks met alle mogelijke inhouds opties.

- Meerdere taken reeksen voor de implementatie van besturings systemen:
  - Een normale taken reeks voor de implementatie van besturings systemen.
  - Er wordt in de eigenschappen van een opstart installatie kopie verwezen.
  - Er zijn meerdere exemplaren van deze taken reeks, met verschillende installatie kopieën die nodig zijn voor de architectuur en taal

## <a name="enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> BitLocker inschakelen

BitLocker-stationsversleuteling biedt versleuteling op laag niveau van de inhoud van een schijfvolume. Gebruik deze stap om BitLocker-versleuteling in te scha kelen op ten minste twee partities op de harde schijf. De eerste actieve partitie bevat de Windows-bootstrapcode. Een andere partitie bevat het besturings systeem. De bootstrappartitie moet onversleuteld blijven.  

Gebruik de stap [BitLocker vooraf inrichten](#BKMK_PreProvisionBitLocker) om BitLocker in te scha kelen op een station in Windows PE.

Deze stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **schijven**en selecteert u **BitLocker inschakelen**.

Wanneer u **alleen TPM**, **TPM en opstart sleutel op USB**of **TPM en pincode**OPGEEFT, moet de Trusted Platform Module (TPM) de volgende status hebben voordat u de stap **BitLocker inschakelen** kunt uitvoeren:  

- Ingeschakeld  
- Geactiveerd  
- Eigendom toegestaan  

Vanaf versie 2006 kunt u deze stap overs laan voor computers die geen TPM hebben of wanneer de TPM niet is ingeschakeld. Met een nieuwe instelling kunt u het gedrag van taken reeksen eenvoudiger beheren op apparaten die BitLocker niet volledig ondersteunen.<!--6995601-->

Met deze stap wordt de resterende TPM-initialisatie voltooid. Voor de resterende acties is geen fysieke aanwezigheid of opnieuw opstarten vereist. Met de stap **BitLocker inschakelen** wordt de volgende resterende TPM-initialisatie acties op transparante wijze voltooid, indien nodig:

- Goedkeuringssleutelpaar maken  
- Eigenaarautorisatiewaarde en escrow maken voor Active Directory, dat moet zijn uitgebreid ter ondersteuning van deze waarde  
- Eigenaar worden  
- De opslaghoofdsleutel maken of opnieuw instellen als deze al aanwezig maar niet-compatibel is  

Als u wilt dat de taken reeks op de stap **BitLocker inschakelen** wordt gewacht om het versleutelings proces voor stationsversleuteling te volt ooien, selecteert u de optie **wachten** . Als u de optie **wachten** niet selecteert, wordt het versleutelings proces op de achtergrond uitgevoerd. De taken reeks loopt onmiddellijk door naar de volgende stap.  

BitLocker kan worden gebruikt voor het versleutelen van meerdere stations op een computer systeem, zowel het besturings systeem als de gegevens stations. Voor het versleutelen van een gegevens station versleutelt u eerst het OS-station en voltooit u het versleutelings proces. Deze vereiste is omdat het besturingssysteem station de sleutel beveiligingen voor de gegevens stations opslaat. Als u het besturings systeem en de gegevens stations in dezelfde taken reeks versleutelt, selecteert u de optie **wachten** op de stap **BitLocker inschakelen** voor het station van het besturings systeem.  

Als de harde schijf al is versleuteld, maar BitLocker is uitgeschakeld, schakelt u met de stap **BitLocker inschakelen** de sleutel beveiligingen opnieuw in en voert u deze snel uit. In dit geval is het niet nodig om de vaste schijf opnieuw te versleutelen.  

### <a name="variables-for-enable-bitlocker"></a>Variabelen voor het inschakelen van BitLocker

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDBitLockerRecoveryPassword](task-sequence-variables.md#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](task-sequence-variables.md#OSDBitLockerStartupKey)  

### <a name="cmdlets-for-enable-bitlocker"></a>Cmdlets voor het inschakelen van BitLocker

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepEnableBitLocker)
- [New-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepEnableBitLocker)
- [Remove-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepEnableBitLocker)
- [Set-CMTSStepEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepEnableBitLocker)

### <a name="properties-for-enable-bitlocker"></a>Eigenschappen voor inschakelen van BitLocker

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="choose-the-drive-to-encrypt"></a>Kies het station dat moet worden gecodeerd

Hiermee geeft u het te versleutelen station op. Selecteer het **huidige besturingssysteem station**om het huidige besturingssysteem station te versleutelen. Configureer vervolgens een van de volgende opties voor sleutel beheer:  

- **Alleen TPM**: selecteer deze optie om alleen Trusted Platform Module (Trusted) te gebruiken.  

- **Alleen opstartsleutel op USB**: selecteer deze optie om een opstartsleutel te gebruiken die op een USB-flashstation is opgeslagen. Wanneer u deze optie selecteert, wordt de normale opstartprocedure door BitLocker vergrendeld totdat een USB-apparaat met een BitLocker-opstartsleutel wordt aangesloten op de computer.  

- **TPM en opstartsleutel op USB**: selecteer deze optie om TPM en een opstartsleutel te gebruiken die op een USB-flashstation is opgeslagen. Wanneer u deze optie selecteert, wordt de normale opstartprocedure door BitLocker vergrendeld totdat een USB-apparaat met een BitLocker-opstartsleutel wordt aangesloten op de computer.  

- **TPM en pincode**: Selecteer deze optie om TPM en een pincode (Personal Identification Number) te gebruiken. Wanneer u deze optie selecteert, wordt de normale opstartprocedure door BitLocker vergrendeld totdat de pincode is ingevoerd.  

Als u een specifieke niet-OS-gegevens schijf wilt versleutelen, selecteert u **specifieke schijf**. Selecteer vervolgens het station in de lijst.  

#### <a name="disk-encryption-mode"></a>Schijf versleutelings modus

<!--6995601-->
Selecteer vanaf versie 2006 een van de volgende versleutelings algoritmen:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Standaard of als dit niet is opgegeven, blijft de stap de standaard versleutelings methode voor de versie van het besturings systeem gebruiken. Als de stap wordt uitgevoerd op een versie van Windows die het opgegeven algoritme niet ondersteunt, wordt de standaard instelling van het besturings systeem hersteld. In dit geval verzendt de taken reeks engine status bericht 11911.

#### <a name="use-full-disk-encryption"></a>Volledige schijf versleuteling gebruiken

<!--SCCMDocs-pr issue 2671-->
Met deze stap wordt standaard alleen de gebruikte ruimte op het station versleuteld. Dit standaard gedrag wordt aanbevolen, omdat het sneller en efficiënter is. Als voor uw organisatie het hele station moet worden versleuteld tijdens de installatie, schakelt u deze optie in. Windows Setup wacht tot het hele station versleuteld is, wat veel tijd in beslag neemt, met name op grote stations.

> [!TIP]
> Vanaf versie 1910 kunt u een beleid voor BitLocker-beheer maken en implementeren, dat gebruikmaakt van de *volledige schijf* versleuteling. Schakel deze optie in als u BitLocker op apparaten wilt beheren nadat het besturings systeem door de taken reeks is geïmplementeerd. Zie voor meer informatie [plannen voor BitLocker-beheer](../../protect/plan-design/bitlocker-management.md).

#### <a name="choose-where-to-create-the-recovery-key"></a>Kies waar de herstel sleutel moet worden gemaakt

Als u wilt opgeven dat BitLocker het herstel wachtwoord moet maken en dit in Active Directory wilt borgen, selecteert u **in Active Directory**. Deze optie vereist dat u Active Directory uitbreidt voor BitLocker-sleutel. BitLocker kan de bijbehorende herstel gegevens vervolgens opslaan in Active Directory. Selecteer geen **herstel sleutel maken** om geen wacht woord te maken. Het maken van een wacht woord is de aanbevolen optie.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Wacht totdat BitLocker het stationscoderingsproces op alle stations heeft voltooid voordat Configuration Manager doorgaat met het uitvoeren van de takenreeks 

Selecteer deze optie als u wilt dat BitLocker-stationsversleuteling is voltooid voordat de volgende stap in de taken reeks wordt uitgevoerd. Als u deze optie selecteert, versleutelt BitLocker het hele schijf volume voordat de gebruiker zich kan aanmelden bij de computer.  

Het versleutelings proces kan uren duren wanneer een grote harde schijf wordt versleuteld. Als u deze optie niet selecteert, kan de taken reeks onmiddellijk worden voortgezet.  

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Deze stap overslaan voor computers die geen TMP hebben of wanneer TMP niet is ingeschakeld

<!--6995601-->
Selecteer met ingang van versie 2006 deze optie om stationsversleuteling over te slaan op een computer die geen ondersteunde of ingeschakelde TPM bevat. Gebruik deze optie bijvoorbeeld wanneer u een besturings systeem implementeert op een virtuele machine. Deze instelling is standaard uitgeschakeld voor de stap **BitLocker inschakelen** . Als u deze instelling inschakelt en het apparaat heeft geen functionele TPM, registreert de taken reeks engine een fout in bestand smsts. log en verzendt status bericht 11912. De taken reeks gaat verder dan deze stap.


## <a name="format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> Schijf Format teren en partitioneren

Gebruik deze stap om een opgegeven schijf op de doel computer te Format teren en te partitioneren.  

> [!IMPORTANT]  
> Elke instelling die u voor deze stap opgeeft, geldt voor één opgegeven schijf. Als u een andere schijf op de doel computer wilt Format teren en partitioneren, voegt u een extra **indeling en partitie schijf** stap toe aan de taken reeks.  

Deze stap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **schijven**en selecteert u **schijf Format teren en partitioneren**.

### <a name="variables-for-format-and-partition-disk"></a>Variabelen voor Format teren en partitioneren schijf

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDDiskIndex](task-sequence-variables.md#OSDDiskIndex)  
- [OSDGPTBootDisk](task-sequence-variables.md#OSDGPTBootDisk)  
- [OSDPartitions](task-sequence-variables.md#OSDPartitions)  
- [OSDPartitionStyle](task-sequence-variables.md#OSDPartitionStyle)  

### <a name="cmdlets-for-format-and-partition-disk"></a>-Cmdlets voor schijf Format teren en partitioneren

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPartitionDisk](/powershell/module/configurationmanager/get-cmtssteppartitiondisk)
- [New-CMTSStepPartitionDisk](/powershell/module/configurationmanager/new-cmtssteppartitiondisk)
- [Remove-CMTSStepPartitionDisk](/powershell/module/configurationmanager/remove-cmtssteppartitiondisk)
- [Set-CMTSStepPartitionDisk](/powershell/module/configurationmanager/set-cmtssteppartitiondisk)

### <a name="properties-for-format-and-partition-disk"></a>Eigenschappen voor Format teren en partitioneren schijf

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="disk-number"></a>Schijfnummer

Het fysieke schijf nummer van de schijf die moet worden geformatteerd. Het nummer is gebaseerd op de rangschikking van Windows-schijfinventarisatie.  

#### <a name="variable-name-to-store-disk-number"></a>Naam van de variabele voor het opslaan van het schijf nummer

<!--6610288-->

Vanaf versie 2006, gebruikt u een taken reeks variabele om de doel schijf op te geven die moet worden geformatteerd. Deze variabele-optie ondersteunt complexere taken reeksen met dynamische gedragingen. Een aangepast script kan bijvoorbeeld de schijf detecteren en de variabele instellen op basis van het hardwaretype. Vervolgens kunt u meerdere exemplaren van deze stap gebruiken om verschillende typen hardware en partities te configureren.

Als u deze eigenschap selecteert, voert u een naam in voor de aangepaste variabele. Voeg een eerdere stap toe aan de taken reeks om de waarde van deze aangepaste variabele in te stellen op een geheel getal voor de fysieke schijf.

In de volgende model stappen ziet u een voor beeld:

- **Power shell-script uitvoeren**: een aangepast script voor het verzamelen van doel schijven
  - Sets `myOSDisk` op `1`
  - Sets `myDataDisk` op `2`

- **Schijf Format teren en partitioneren** voor besturingssysteem schijf: `myOSDisk` variabele opgeven
  - Schijf 1 als de systeem schijf configureren

- **Schijf Format teren en partitioneren** voor gegevens schijf: `myDataDisk` variabele opgeven
  - Hiermee wordt schijf 2 voor onbewerkte opslag geconfigureerd

Een variant van dit voor beeld maakt gebruik van schijf nummers en partitielay-abonnementen voor verschillende typen hardware.

> [!NOTE]
> U kunt nog steeds de bestaande taken reeks variabele **OSDDiskIndex**gebruiken. Elk exemplaar van de schijf voor **Format teren en partitioneren** maakt echter gebruik van dezelfde index waarde. Als u het schijf nummer voor meerdere exemplaren van deze stap programmatisch wilt instellen, gebruikt u deze variabele-eigenschap.

#### <a name="disk-type"></a>Schijftype

Het type schijf dat moet worden geformatteerd. Er zijn twee opties die u kunt selecteren in de vervolgkeuzelijst:

- **Standaard (MBR)**: Master boot record  
- **GPT**: GUID-partitie tabel  

> [!NOTE]  
> Als u het schijf type wijzigt van **standaard (MBR)** in **GPT**en de partitie-indeling een uitgebreide partitie bevat, verwijdert de taken reeks alle uitgebreide en logische partities uit de lay-out. De taken reeks editor vraagt u deze actie te bevestigen voordat u het schijf type wijzigt.  

#### <a name="volume"></a>Volume

Specifieke informatie over de partitie of het volume dat door de taken reeks wordt gemaakt, met inbegrip van de volgende kenmerken:  

- Naam  
- Resterende schijfruimte  

Als u een nieuwe partitie wilt maken, selecteert u **Nieuw** om het dialoog venster **partitie-eigenschappen** te openen. Geef het partitie type en de grootte op en als het een opstart partitie is. Als u een bestaande partitie wilt wijzigen, selecteert u de te wijzigen partitie en selecteert u vervolgens de **Eigenschappen** knop. Zie een van de volgende artikelen voor meer informatie over het configureren van partities voor harde schijven:  

- [Partities op basis van UEFI/GPT-schijven](/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [Partities op basis van BIOS/MBR-schijven](/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Als u een partitie wilt verwijderen, kiest u de partitie en selecteert u vervolgens **verwijderen**.  



## <a name="install-application"></a><a name="BKMK_InstallApplication"></a> Toepassing installeren

Met deze stap worden de opgegeven toepassingen geïnstalleerd, of een set toepassingen die is gedefinieerd door een dynamische lijst met taken reeks variabelen. Wanneer de taken reeks deze stap uitvoert, begint de installatie van de toepassing onmiddellijk zonder te wachten op een polling-interval voor beleid.  

De toepassingen moeten voldoen aan de volgende criteria:  

- De toepassing moet een implementatie type van **Windows Installer** of **script** installatie programma hebben. Implementatie typen voor Windows-app-pakketten (appx-bestand) worden niet ondersteund.  

- Het moet worden uitgevoerd onder het lokale systeem account en niet op het gebruikers account.  

- De toepassing mag geen interactie hebben met het bureaublad. Het programma moet stil of zonder toezicht worden uitgevoerd.  

- De toepassing mag zelf geen herstart initiëren. De toepassing moet een herstart aanvragen via de standaard herstart code, 3010. Dit gedrag zorgt ervoor dat bij deze stap de herstart correct wordt afgehandeld. Als de toepassing een afsluit code van 3010 retourneert, start de taken reeks engine de computer opnieuw op. Na het opnieuw opstarten wordt de takenreeks automatisch voortgezet.  

> [!Note]
> Als met de toepassing wordt [gecontroleerd of uitvoer bare bestanden worden uitgevoerd](../../apps/deploy-use/deploy-applications.md#bkmk_exe-check), kan de taken reeks deze niet installeren. Als u deze stap niet configureert om door te gaan met de fout, mislukt de hele taken reeks.

Wanneer deze stap wordt uitgevoerd, controleert de toepassing de toepas baarheid van de regels voor vereisten en de detectie methode voor de implementatie typen. Op basis van de resultaten van deze controle installeert de toepassing het toepasselijke implementatietype. Als een implementatie type afhankelijkheden bevat, wordt het afhankelijke implementatie type geëvalueerd en geïnstalleerd als onderdeel van deze stap. Toepassings afhankelijkheden worden niet ondersteund voor zelfstandige media.  

> [!NOTE]  
> Voor het installeren van een toepassing die een andere toepassing vervangt, moeten de inhouds bestanden voor de vervangen toepassing beschikbaar zijn. Anders mislukt deze taken reeks stap. Bijvoorbeeld: Microsoft Visio 2010 is geïnstalleerd in een client of in een vastgelegde installatiekopie. Wanneer u de stap **toepassing installeren** installeert micro soft Visio 2013, moeten de inhouds bestanden voor micro soft Visio 2010 (de vervangen toepassing) beschikbaar zijn op een distributie punt. Als micro soft Visio helemaal niet is geïnstalleerd op een client of vastgelegde installatie kopie, installeert de taken reeks micro soft Visio 2013 zonder te controleren op de micro soft Visio 2010-inhouds bestanden.  
>
> Als u een vervangen app buiten gebruik stelt en er in een taken reeks naar de nieuwe app wordt verwezen, kan de taken reeks niet worden gestart.
Dit gedrag is inherent aan het ontwerp: de taken reeks vereist alle app-verwijzingen.<!-- SCCMDocs 1711 -->  

Deze taken reeks stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Software**en selecteert u **toepassing installeren**.

### <a name="variables-for-install-application"></a>Variabelen voor installatie toepassing

Gebruik de volgende taken reeks variabelen met deze stap:  

- [_TSAppInstallStatus](task-sequence-variables.md#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](task-sequence-variables.md#TSErrorOnWarning)  

> [!NOTE]  
> Als de client de lijst met beheer punten niet kan ophalen van locatie Services, gebruikt u de taken reeks variabelen **SMSTSMPListRequestTimeoutEnabled** en **SMSTSMPListRequestTimeout** . Deze variabelen geven aan hoeveel milliseconden een taken reeks wacht voordat deze opnieuw probeert een toepassing te installeren. Zie [taken reeks variabelen](task-sequence-variables.md)voor meer informatie.

### <a name="cmdlets-for-install-application"></a>Cmdlets voor de installatie toepassing

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallApplication](/powershell/module/configurationmanager/get-cmtsstepinstallapplication)
- [New-CMTSStepInstallApplication](/powershell/module/configurationmanager/new-cmtsstepinstallapplication)
- [Remove-CMTSStepInstallApplication](/powershell/module/configurationmanager/remove-cmtsstepinstallapplication)
- [Set-CMTSStepInstallApplication](/powershell/module/configurationmanager/set-cmtsstepinstallapplication)

### <a name="properties-for-install-application"></a>Eigenschappen voor installatie toepassing

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="install-the-following-applications"></a>De volgende toepassingen installeren

De taken reeks installeert deze toepassingen in de opgegeven volg orde.  

Configuration Manager uitgeschakelde toepassingen of toepassingen met de volgende instellingen worden gefilterd:  

- Alleen als er een gebruiker is aangemeld  
- Uitvoeren met gebruikersrechten  

Deze toepassingen worden niet weer gegeven in het dialoog venster **Selecteer de te installeren toepassing** .

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Toepassingen installeren volgens dynamische variabelenlijst

Met de taken reeks worden toepassingen geïnstalleerd met behulp van deze basis variabelenaam. De naam van de basis variabele is voor een set taken reeks variabelen die zijn gedefinieerd voor een verzameling of computer. Met deze variabelen worden de toepassingen opgegeven die door de taken reeks voor die verzameling of computer worden geïnstalleerd. De naam van elke variabele bestaat uit de gemeenschappelijke basisnaam plus een numeriek achtervoegsel dat begint bij 01. De waarde voor elke variabele moet de naam van de toepassing en niets anders bevatten.  

Als u wilt dat de taken reeks toepassingen installeert met behulp van een dynamische variabelen lijst, schakelt u de volgende instelling in op het tabblad **Algemeen** van de **Eigenschappen**van de toepassing: **toestaan dat deze toepassing wordt geïnstalleerd vanuit de taken reeks actie toepassing installeren in plaats van hand matig implementeren**.  

> [!NOTE]  
> U kunt toepassingen niet installeren met behulp van een dynamische variabelen lijst voor zelfstandige media-implementaties.  

Als u bijvoorbeeld één toepassing wilt installeren met behulp van een taken reeks variabele met de naam AA01, geeft u de volgende variabele op:  

|Naam variabele|Waarde variabele|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Als u twee toepassingen wilt installeren, geeft u de volgende variabelen op:  

|Naam variabele|Waarde variabele|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

De volgende voor waarden zijn van invloed op de toepassingen die door de taken reeks zijn geïnstalleerd:  

- Als de waarde van een variabele andere informatie bevat dan de naam van de toepassing, Met de taken reeks wordt de toepassing niet geïnstalleerd en wordt de taken reeks voortgezet.  

- Als de taken reeks geen variabele met de opgegeven basis naam en het achtervoegsel ' 01 ' vindt, worden door de taken reeks geen toepassingen geïnstalleerd.  

> [!Important]  
> Deze waarden zijn hoofdletter gevoelig. Bijvoorbeeld ' install ' is niet hetzelfde als ' installeren '. Als u de waarde moet wijzigen, detecteert de taken reeks editor geen hoofdletter wijziging. U kunt op hetzelfde moment nog een andere bewerking maken, bijvoorbeeld de stap beschrijving wijzigen.<!--509714-->

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Als de installatie van een toepassing mislukt, doorgaan met installatie van de andere toepassingen op de lijst

Met deze instelling geeft u op dat de stap wordt voortgezet wanneer de installatie van een afzonderlijke toepassing mislukt. Als u deze instelling opgeeft, wordt de taken reeks voortgezet ongeacht eventuele installatie fouten. Als u deze instelling niet opgeeft en de installatie mislukt, wordt de stap onmiddellijk beëindigd.  

#### <a name="clear-application-content-from-cache-after-installing"></a>Toepassings inhoud uit cache wissen na installatie

<!--4485675-->
Vanaf versie 1906 verwijdert u de app-inhoud uit de client cache nadat de stap is uitgevoerd. Dit gedrag is nuttig op apparaten met kleine harde schijven of bij het installeren van veel grote apps achter elkaar.


### <a name="options-for-install-application"></a>Opties voor installatie toepassing

> [!NOTE]  
> Wanneer u **door gaan bij fout** selecteert op het tabblad **Opties** van deze stap, wordt de taken reeks voortgezet als een toepassing niet kan worden geïnstalleerd. Wanneer u deze optie niet inschakelt, mislukt de taken reeks en worden resterende toepassingen niet geïnstalleerd.  

Naast de standaard opties configureert u de volgende extra instellingen op het tabblad **Opties** van deze taken reeks stap:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Probeer deze stap opnieuw uit te voeren als de computer onverwacht opnieuw wordt opgestart

Als de computer onverwacht opnieuw wordt opgestart door een van de toepassings installaties, voert u deze stap opnieuw uit. Met deze stap wordt deze instelling standaard ingeschakeld met twee nieuwe pogingen. U kunt een tot vijf nieuwe pogingen opgeven.  



## <a name="install-package"></a><a name="BKMK_InstallPackage"></a> Pakket installeren

Gebruik deze stap om een software pakket te installeren als onderdeel van de taken reeks. Wanneer deze stap wordt uitgevoerd, begint de installatie onmiddellijk zonder te wachten op een polling-interval voor beleid.  

Het pakket moet voldoen aan de volgende criteria:  

- Het moet worden uitgevoerd onder het lokale systeem account en niet op een gebruikers account.  

- Het mag niet communiceren met het bureau blad. Het programma moet stil of zonder toezicht worden uitgevoerd.  

- De toepassing mag zelf geen herstart initiëren. De software moet een herstart aanvragen via de standaard herstart code, 3010. Dit gedrag zorgt ervoor dat de taken reeks de herstart correct afhandelt. Als de software een afsluit code van 3010 retourneert, start de taken reeks engine de computer opnieuw op. Na het opnieuw opstarten wordt de takenreeks automatisch voortgezet.  

Program ma's die gebruikmaken van de optie **eerst een ander programma uitvoeren** voor het installeren van een afhankelijk programma, worden niet ondersteund bij het implementeren van een besturings systeem. Als u de pakket optie inschakelt **eerst een ander programma uitvoeren**en het afhankelijke programma al is uitgevoerd op de doel computer, wordt het afhankelijke programma uitgevoerd en wordt de taken reeks voortgezet. Als het afhankelijke programma echter nog niet is uitgevoerd op de doel computer, mislukt de taken reeks stap.  

> [!NOTE]  
> De centrale beheer site beschikt niet over het vereiste beleid voor client configuratie om de Software Distribution agent tijdens de taken reeks in te scha kelen. Wanneer u op de centrale beheersite zelfstandige media maakt voor een takenreeks en de takenreeks de stap **Pakket installeren** bevat, wordt mogelijk de volgende fout weergegeven in het bestand CreateTsMedia.log:  
>
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>
> Voor zelfstandige media met de stap **pakket installeren** maakt u de zelfstandige media op een primaire site waarop de agent voor software distributie is ingeschakeld. U kunt ook de stap **opdracht regel uitvoeren** toevoegen na de stap **Windows en ConfigMgr** installeren en vóór de eerste stap **pakket installatie** . Met de stap **opdracht regel uitvoeren** wordt een WMIC-opdracht uitgevoerd om de agent voor software distributie in te scha kelen vóór de eerste stap **pakket installeren** . Gebruik de volgende opdracht in de stap **opdracht regel uitvoeren** :  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>
> Zie voor meer informatie over het maken van zelfstandige media [zelfstandige media maken](../deploy-use/create-stand-alone-media.md).  

Deze taken reeks stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Software**en selecteert u **pakket installeren**.

### <a name="variables-for-install-package"></a>Variabelen voor installatie pakket

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) <!--1358493-->  

### <a name="cmdlets-for-install-package"></a>Cmdlets voor het installatie pakket

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallSoftware](/powershell/module/configurationmanager/get-cmtsstepinstallsoftware)
- [New-CMTSStepInstallSoftware](/powershell/module/configurationmanager/new-cmtsstepinstallsoftware)
- [Remove-CMTSStepInstallSoftware](/powershell/module/configurationmanager/remove-cmtsstepinstallsoftware)
- [Set-CMTSStepInstallSoftware](/powershell/module/configurationmanager/set-cmtsstepinstallsoftware)

> [!TIP]
> Inhoud vooraf in cache opslaan gebruiken om een toepasselijk upgrade pakket voor het besturings systeem te downloaden voordat een gebruiker de taken reeks installeert. Zie [inhoud vooraf in cache configureren](../deploy-use/configure-precache-content.md)voor meer informatie.

### <a name="properties-for-install-package"></a>Eigenschappen voor installatie pakket

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="install-a-single-software-package"></a>Een enkel softwarepakket installeren

Met deze instelling geeft u een Configuration Manager software pakket op. De stap wacht totdat de installatie is voltooid.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Softwarepakketten installeren volgens dynamische variabelenlijst

Met de taken reeks worden pakketten geïnstalleerd met behulp van deze basis variabelenaam. De naam van de basis variabele is voor een set taken reeks variabelen die zijn gedefinieerd voor een verzameling of computer. Met deze variabelen worden de pakketten opgegeven die de taken reeks voor die verzameling of computer installeert. De naam van elke variabele bestaat uit de gemeenschappelijke basisnaam plus een numeriek achtervoegsel dat begint bij 001. De waarde voor elke variabele moet een pakket-id en de naam van de software bevatten en deze moeten zijn gescheiden door een dubbele punt.  

Voor de taken reeks om software te installeren met behulp van een dynamische variabelen lijst, schakelt u de volgende instelling in op het tabblad **Geavanceerd** van de **Eigenschappen**van het pakket: **toestaan dat dit programma wordt geïnstalleerd vanuit de taken reeks pakket installeren zonder te worden geïmplementeerd**.  

> [!NOTE]  
> U kunt software pakketten niet installeren met behulp van een dynamische variabelen lijst voor zelfstandige media-implementaties.  

Bijvoorbeeld: als u één softwarepakket wilt installeren met behulp van de takenreeksvariabele AA001, geeft u de volgende variabele op:  

|Naam variabele|Waarde variabele|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

Als u drie softwarepakketten wilt installeren, geeft u de volgende variabelen op:  

|Naam variabele|Waarde variabele|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

De volgende voor waarden zijn van invloed op de pakketten die worden geïnstalleerd door de taken reeks:  

- Als u de waarde van een variabele niet in de juiste indeling maakt of als deze geen geldige pakket-ID en naam opgeeft, mislukt de software-installatie.  

- Als de pakket-ID kleine letters bevat, mislukt de installatie van de software.  

- Als de taken reeks geen variabele met de opgegeven basis naam en het achtervoegsel ' 001 ' vindt, worden door de taken reeks geen pakketten geïnstalleerd. De taken reeks wordt verder uitgevoerd.  

> [!Important]  
> Deze waarden zijn hoofdletter gevoelig. Bijvoorbeeld ' install ' is niet hetzelfde als ' installeren '. Als u de waarde moet wijzigen, detecteert de taken reeks editor geen hoofdletter wijziging. U kunt op hetzelfde moment nog een andere bewerking maken, bijvoorbeeld de stap beschrijving wijzigen.<!--509714-->

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Als de installatie van een softwarepakket mislukt, doorgaan met installatie van andere pakketten in de lijst

Deze instelling geeft aan dat de stap wordt voorgezet als de installatie van een afzonderlijk softwarepakket mislukt. Als u deze instelling opgeeft, wordt de taken reeks voortgezet ongeacht eventuele installatie fouten. Als u deze instelling niet opgeeft en de installatie mislukt, wordt de stap onmiddellijk beëindigd.  



## <a name="install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> Software-updates installeren

Gebruik deze stap om software-updates te installeren op de doel computer. De doel computer wordt pas geëvalueerd voor toepasselijke software-updates als deze taken reeks stap wordt uitgevoerd. Op dat moment wordt de doel computer geëvalueerd voor software-updates zoals elke andere Configuration Manager-client. Voor deze stap om software-updates te installeren, moet u eerst de updates implementeren op een verzameling waarvan de doel computer lid is.  

> [!IMPORTANT]  
> Installeer de meest recente versie van de Windows Update-Agent voor de beste prestaties.  

Deze taken reeks stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Software**en selecteert u **software-updates installeren**.

### <a name="variables-for-install-software-updates"></a>Variabelen voor het installeren van software-updates

Gebruik de volgende taken reeks variabelen met deze stap:  

- [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](task-sequence-variables.md#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](task-sequence-variables.md#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](task-sequence-variables.md#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> Als de client de lijst met beheer punten niet kan ophalen van locatie Services, gebruikt u de variabelen **SMSTSMPListRequestTimeoutEnabled** en **SMSTSMPListRequestTimeout** . Deze variabelen geven aan hoeveel milliseconden een taken reeks wacht voordat deze opnieuw probeert een toepassing of software-update te installeren. Zie [taken reeks variabelen](task-sequence-variables.md)voor meer informatie.  

### <a name="cmdlets-for-install-software-updates"></a>Cmdlets voor het installeren van software-updates

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepInstallUpdate](/powershell/module/configurationmanager/get-cmtsstepinstallupdate)
- [New-CMTSStepInstallUpdate](/powershell/module/configurationmanager/new-cmtsstepinstallupdate)
- [Remove-CMTSStepInstallUpdate](/powershell/module/configurationmanager/remove-cmtsstepinstallupdate)
- [Set-CMTSStepInstallUpdate](/powershell/module/configurationmanager/set-cmtsstepinstallupdate)

Zie [software-updates installeren](install-software-updates.md)voor meer aanbevelingen en een technisch stroom diagram voor deze stap.

### <a name="properties-for-install-software-updates"></a>Eigenschappen voor het installeren van software-updates

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Vereist voor installatie - alleen verplichte software-updates

Selecteer deze optie om alle verplichte software-updates te installeren met door de beheerder gedefinieerde installatie deadlines.  

#### <a name="available-for-installation---all-software-updates"></a>Beschikbaar voor installatie - alle software-updates

Selecteer deze optie om alle beschik bare software-updates te installeren. Implementeer deze updates eerst op een verzameling waarvan de computer lid is. De taken reeks installeert alle beschik bare software-updates op de doel computers.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Software-updates van scanresultaten in het cachegeheugen evalueren

Deze stap maakt standaard gebruik van scan resultaten in de cache van de Windows Update-Agent. Schakel deze optie uit om de Windows Update-Agent te instrueren de nieuwste catalogus te downloaden van het software-update punt. Schakel deze optie in als u een taken reeks gebruikt om [een installatie kopie van een besturings systeem vast te leggen en te bouwen](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). Een groot aantal software-updates is waarschijnlijk in dit scenario.

Veel van deze updates hebben afhankelijkheden. Installeer bijvoorbeeld update ABC voordat update XYZ wordt weer gegeven zoals van toepassing. Wanneer u deze instelling uitschakelt en de taken reeks implementeert voor een groot aantal clients, maken ze allemaal gelijktijdig verbinding met het software-update punt. Dit gedrag resulteert in prestatie problemen tijdens het proces en het downloaden van de Update catalogus.

In de meeste gevallen gebruikt u de standaard instelling voor het gebruik van scan resultaten in het cache geheugen.

De variabele **SMSTSSoftwareUpdateScanTimeout** regelt de time-out voor de scan van software-updates tijdens deze stap. De standaard waarde is 60 minuten. Zie [taken reeks variabelen](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)voor meer informatie.

### <a name="options-for-install-software-updates"></a>Opties voor het installeren van software-updates

Naast de standaard opties configureert u de volgende extra instellingen op het tabblad **Opties** van deze taken reeks stap:  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Probeer deze stap opnieuw uit te voeren als de computer onverwacht opnieuw wordt opgestart

Als een van de updates de computer onverwacht opnieuw opstart, voert u deze stap opnieuw uit. Met deze stap wordt deze instelling standaard ingeschakeld met twee nieuwe pogingen. U kunt een tot vijf nieuwe pogingen opgeven.  

> [!NOTE]  
> Configureer de **SMSTSWaitForSecondReboot** -variabele om op te geven hoeveel seconden de taken reeks moet worden onderbroken nadat de computer opnieuw is opgestart in dit scenario. Zie [taken reeks variabelen](task-sequence-variables.md#SMSTSWaitForSecondReboot)voor meer informatie.  



## <a name="join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> Lid worden van domein of werk groep

Gebruik deze stap om de doel computer toe te voegen aan een werk groep of domein.  

> [!NOTE]
> Wanneer een client die lid is van een Azure Active Directory (Azure AD) een taken reeks voor besturingssysteem implementatie uitvoert, wordt de client in het nieuwe besturings systeem niet automatisch toegevoegd aan Azure AD. Hoewel het geen lid is van Azure AD, wordt de client nog steeds beheerd.

Deze taken reeks stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert u **lid worden van domein of werk groep**.

### <a name="variables-for-join-domain-or-workgroup"></a>Variabelen voor lid worden van domein of werk groep

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDJoinAccount](task-sequence-variables.md#OSDJoinAccount)  
- [OSDJoinDomainName](task-sequence-variables.md#OSDJoinDomainName)  
- [OSDJoinDomainOUName](task-sequence-variables.md#OSDJoinDomainOUName)  
- [OSDJoinPassword](task-sequence-variables.md#OSDJoinPassword)  
- [OSDJoinSkipReboot](task-sequence-variables.md#OSDJoinSkipReboot)  
- [OSDJoinType](task-sequence-variables.md#OSDJoinType)  
- [OSDJoinWorkgroupName](task-sequence-variables.md#OSDJoinWorkgroupName)  

### <a name="cmdlets-for-join-domain-or-workgroup"></a>Cmdlets voor lid worden van domein of werk groep

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Get-CMTSStepJoinDomainWorkgroup)
- [New-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/New-CMTSStepJoinDomainWorkgroup)
- [Remove-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Remove-CMTSStepJoinDomainWorkgroup)
- [Set-CMTSStepJoinDomainWorkgroup](/powershell/module/configurationmanager/Set-CMTSStepJoinDomainWorkgroup)

### <a name="properties-for-join-domain-or-workgroup"></a>Eigenschappen voor lid van domein of werk groep

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="join-a-workgroup"></a>Lid worden van een werkgroep

Selecteer deze optie om de doelcomputer toe te voegen aan de opgegeven werkgroep. Als de computer momenteel lid is van een domein en u deze optie selecteert, wordt de computer opnieuw opgestart.  

#### <a name="join-a-domain"></a>Lid worden van een domein

Selecteer deze optie om de doelcomputer toe te voegen aan het opgegeven domein.  

Typ optioneel een organisatie-eenheid (OE) of blader ernaartoe in het opgegeven domein waarvan u de computer lid wilt maken. Als de computer momenteel lid is van een ander domein of een werk groep, zorgt deze optie ervoor dat de computer opnieuw wordt opgestart. Als de computer al lid is van een andere organisatie-eenheid, omdat Active Directory Domain Services de OE niet mag wijzigen via deze methode, wordt deze instelling door Windows Setup genegeerd.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Voer het account in dat is gemachtigd om lid te worden van het domein.

Selecteer **instellen** om de gebruikers naam en het wacht woord in te voeren voor een account met machtigingen om lid te worden van het domein. Voer het account in met de volgende indeling:  `Domain\account` . Zie [accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-domain-join-account)voor meer informatie over het domein voor het samen voegen van taken reeksen.  



## <a name="prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> ConfigMgr-client voorbereiden voor vastleggen

Met deze stap kunt u de Configuration Manager-client op de referentie computer verwijderen of configureren. Met deze actie wordt de computer voor bereid voor vastleggen als onderdeel van het installatie kopie proces.

Met deze stap wordt de Configuration Manager-client volledig verwijderd, in plaats van alleen de sleutel gegevens te verwijderen. Wanneer de vastgelegde installatie kopie van het besturings systeem door de taken reeks wordt geïmplementeerd, wordt elke keer een nieuwe Configuration Manager-client geïnstalleerd.  

> [!Note]  
> De taken reeks engine verwijdert de client alleen tijdens het **bouwen en vastleggen van een referentie-installatie kopie van het besturings systeem** . De taken reeks engine verwijdert de client niet tijdens andere vastleg methoden, zoals vastleg media of een aangepaste taken reeks.  

Deze taken reeks stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **installatie kopieën**en selecteert u **ConfigMgr-client voorbereiden voor vastleggen**.

### <a name="cmdlets-for-prepare-configmgr-client-for-capture"></a>Cmdlets voor het voorbereiden van ConfigMgr-client voor vastleggen

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Get-CMTSStepPrepareConfigMgrClient)
- [New-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/New-CMTSStepPrepareConfigMgrClient)
- [Remove-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Remove-CMTSStepPrepareConfigMgrClient)
- [Set-CMTSStepPrepareConfigMgrClient](/powershell/module/configurationmanager/Set-CMTSStepPrepareConfigMgrClient)



## <a name="prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Windows voorbereiden voor vastleggen

Gebruik deze stap om de Sysprep-opties op te geven bij het vastleggen van een installatie kopie van een besturings systeem op de referentie computer. Met deze stap wordt Sysprep uitgevoerd en wordt de computer opnieuw opgestart naar de opstart installatie kopie voor Windows PE die is opgegeven voor de taken reeks. Deze actie mislukt als de referentie computer lid is van een domein.  

Deze stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **installatie kopieën**en selecteert u **Windows voorbereiden voor vastleggen**.

### <a name="variables-for-prepare-windows-for-capture"></a>Variabelen voor het voorbereiden van Windows voor vastleggen

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDKeepActivation](task-sequence-variables.md#OSDKeepActivation)  
- [OSDTargetSystemRoot](task-sequence-variables.md#OSDTargetSystemRoot-output)  

### <a name="cmdlets-for-prepare-windows-for-capture"></a>Cmdlets voor het voorbereiden van Windows voor vastleggen

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Get-CMTSStepPrepareWindows)
- [New-CMTSStepPrepareWindows](/powershell/module/configurationmanager/New-CMTSStepPrepareWindows)
- [Remove-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Remove-CMTSStepPrepareWindows)
- [Set-CMTSStepPrepareWindows](/powershell/module/configurationmanager/Set-CMTSStepPrepareWindows)

### <a name="properties-for-prepare-windows-for-capture"></a>Eigenschappen voor het voorbereiden van Windows voor vastleggen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Lijst van stuurprogramma's voor massaopslag automatisch samenstellen

Selecteer deze optie om automatisch een lijst met stuurprogramma's voor massaopslag van de referentiecomputer te laten samenstellen door Sysprep. Met deze optie wordt de optie Build Mass Storage Drivers in het bestand sysprep.inf op de referentiecomputer ingeschakeld. Raadpleeg de documentatie van Sysprep voor meer informatie over deze instelling.  

#### <a name="do-not-reset-activation-flag"></a>Activatiemarkering niet resetten

Selecteer deze optie om te voorkomen dat Sysprep de markering voor productactivering opnieuw instelt.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>De computer afsluiten nadat deze actie is uitgevoerd

<!--SCCMDocs-pr issue 2695-->
Met deze optie geeft u aan dat Sysprep de computer moet afsluiten in plaats van het standaard gedrag voor opnieuw opstarten.

De taken reeks [Windows auto pilot voor bestaande apparaten](../../../autopilot/existing-devices.md) gebruikt deze stap met deze optie.

- Als u wilt dat de taken reeks het apparaat vernieuwt en vervolgens de OOBE voor auto pilot onmiddellijk start, moet u deze optie uitschakelen.  

- Schakel deze optie in om het apparaat na de installatie af te afsluiten. Vervolgens kunt u het apparaat aan een gebruiker leveren dat OOBE start met auto pilot wanneer ze het voor de eerste keer inschakelt.  



## <a name="pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> BitLocker vooraf inrichten

Gebruik deze stap om BitLocker in te scha kelen op een station in Windows PE. Standaard wordt alleen de gebruikte schijf ruimte versleuteld, zodat de versleutelings tijden veel sneller zijn. U past de sleutel beheer opties toe met behulp van de stap [BitLocker inschakelen](#BKMK_EnableBitLocker) nadat het besturings systeem is geïnstalleerd.

> [!IMPORTANT]
> Voor het vooraf inrichten van BitLocker moet de computer een ondersteunde en ingeschakelde Trusted Platform Module (TPM) hebben.

Deze stap kan alleen in Windows PE worden uitgevoerd. Deze wordt niet uitgevoerd in het volledige besturings systeem.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **schijven**en selecteert u **BitLocker vooraf inrichten**.

### <a name="cmdlets-for-pre-provision-bitlocker"></a>Cmdlets voor het vooraf inrichten van BitLocker

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Get-CMTSStepOfflineEnableBitLocker)
- [New-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/New-CMTSStepOfflineEnableBitLocker)
- [Remove-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Remove-CMTSStepOfflineEnableBitLocker)
- [Set-CMTSStepOfflineEnableBitLocker](/powershell/module/configurationmanager/Set-CMTSStepOfflineEnableBitLocker)

### <a name="properties-for-pre-provision-bitlocker"></a>Eigenschappen voor BitLocker vooraf inrichten

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>BitLocker toepassen op het opgegeven station

Geef het station op waarvoor u BitLocker wilt inschakelen. BitLocker versleutelt alleen de gebruikte ruimte op het station.  

#### <a name="disk-encryption-mode"></a>Schijf versleutelings modus

<!--6995601-->
Selecteer vanaf versie 2006 een van de volgende versleutelings algoritmen:

- AES_128
- AES_256
- XTS_AES256
- XTS_AES128

Standaard of als dit niet is opgegeven, blijft de stap de standaard versleutelings methode voor de versie van het besturings systeem gebruiken. Als de stap wordt uitgevoerd op een versie van Windows die het opgegeven algoritme niet ondersteunt, wordt de standaard instelling van het besturings systeem hersteld. In dit geval verzendt de taken reeks engine status bericht 11911.

#### <a name="use-full-disk-encryption"></a>Volledige schijf versleuteling gebruiken

<!--SCCMDocs-pr issue 2671-->
Met deze stap wordt standaard alleen de gebruikte ruimte op het station versleuteld. Dit standaard gedrag wordt aanbevolen, omdat het sneller en efficiënter is. Als voor uw organisatie het hele station moet worden versleuteld tijdens de installatie, schakelt u deze optie in. Windows Setup wacht tot het hele station versleuteld is, wat veel tijd in beslag neemt, met name op grote stations.

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Deze stap overslaan voor computers die geen TMP hebben of wanneer TMP niet is ingeschakeld

Selecteer deze optie om stationsversleuteling over te slaan op een computer die geen ondersteunde of ingeschakelde TPM bevat. Gebruik deze optie bijvoorbeeld wanneer u een besturings systeem implementeert op een virtuele machine. Deze instelling is standaard ingeschakeld voor de **BitLocker-stap vooraf inrichten** . De stap mislukt op een apparaat zonder TPM of een TPM die niet kan worden geïnitialiseerd. Vanaf versie 2006, wanneer het apparaat geen functionele TPM heeft, registreert de taken reeks engine een waarschuwing in bestand smsts. log en verzendt het status bericht 11912.



## <a name="release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> Status opslag vrijgeven

Gebruik deze stap om het status migratie punt te informeren dat de vastleg-of herstel actie is voltooid. Gebruik deze stap in combi natie met de stappen **status opslag opvragen**, **gebruikers toestand vastleggen**en **gebruikers status herstellen** . U kunt deze stappen gebruiken om gebruikers status gegevens te migreren met behulp van een status migratie punt en de Hulpprogramma voor migratie van gebruikersstatus (USMT).  

Zie [gebruikers status beheren](../get-started/manage-user-state.md)voor meer informatie over het beheren van de gebruikers status bij het implementeren van besturings systemen.  

Als u de stap **status opslag opvragen** gebruikt om toegang aan te vragen tot een status migratie punt om de gebruikers status vast te *leggen* , wordt met deze stap aan het status migratie punt gewaarschuwd dat het vastleg proces is voltooid. Het status migratie punt markeert vervolgens de gebruikers status gegevens die beschikbaar zijn voor herstel. Het status migratie punt stelt de toegangs beheer machtigingen voor de gebruikers status gegevens in, zodat alleen de herstel computer alleen-lezen toegang heeft.  

Als u de stap **status opslag opvragen** gebruikt om toegang aan te vragen tot een status migratie punt om gebruikers status te *herstellen* , wordt met deze stap aan het status migratie punt gewaarschuwd dat het herstel proces is voltooid. Het status migratie punt activeert vervolgens de instellingen voor het bewaren van de geconfigureerde gegevens.  

> [!IMPORTANT]  
> Stel de optie **door gaan bij fout in** voor alle stappen tussen de stappen **status opslag opvragen** en **status opslag vrijgeven** . Elke stap voor de **status opslag** van een aanvraag moet een overeenkomende stap voor het vrijgeven van de **status opslag** hebben.  

Deze stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **gebruikers status**en selecteert u **release status opslag**.

### <a name="variables-for-release-state-store"></a>Variabelen voor status opslag vrijgeven

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-release-state-store"></a>Cmdlets voor status opslag vrijgeven

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Get-CMTSStepReleaseStateStore)
- [New-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/New-CMTSStepReleaseStateStore)
- [Remove-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Remove-CMTSStepReleaseStateStore)
- [Set-CMTSStepReleaseStateStore](/powershell/module/configurationmanager/Set-CMTSStepReleaseStateStore)

### <a name="properties-for-release-state-store"></a>Eigenschappen voor status opslag vrijgeven

Voor deze stap zijn geen instellingen vereist op het tabblad **Eigenschappen** .



## <a name="request-state-store"></a><a name="BKMK_RequestStateStore"></a> Status opslag opvragen

Gebruik deze stap om toegang aan te vragen tot een status migratie punt bij het vastleggen of herstellen van de status.  

Zie [gebruikers status beheren](../get-started/manage-user-state.md)voor meer informatie over het beheren van de gebruikers status bij het implementeren van besturings systemen.  

Gebruik deze stap in combi natie met het **release status archief**, de **gebruikers status vastleggen**en de stappen voor het **herstellen van gebruikers status** . U kunt deze stappen gebruiken om computer status te migreren met behulp van een status migratie punt en de Hulpprogramma voor migratie van gebruikersstatus (USMT).  

> [!NOTE]  
> Wanneer u een nieuw status migratie punt maakt, is de opslag van de gebruikers status niet Maxi maal één uur beschikbaar. Als u de beschik baarheid wilt versnellen, past u de instellingen van de eigenschappen op het status migratie punt aan om een update van het site besturings bestand te activeren.  

Deze stap wordt uitgevoerd in het volledige besturings systeem en in Windows PE voor offline USMT.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **gebruikers status**en selecteert u **status opslag opvragen**.

### <a name="variables-for-request-state-store"></a>Variabelen voor aanvraag status opslag

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDStateFallbackToNAA](task-sequence-variables.md#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](task-sequence-variables.md#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](task-sequence-variables.md#OSDStateSMPRetryTime)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-request-state-store"></a>Cmdlets voor aanvraag status opslag

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Get-CMTSStepRequestStateStore)
- [New-CMTSStepRequestStateStore](/powershell/module/configurationmanager/New-CMTSStepRequestStateStore)
- [Remove-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Remove-CMTSStepRequestStateStore)
- [Set-CMTSStepRequestStateStore](/powershell/module/configurationmanager/Set-CMTSStepRequestStateStore)

### <a name="properties-for-request-state-store"></a>Eigenschappen voor aanvraag status opslag

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="capture-state-from-the-computer"></a>Status vastleggen vanaf de computer

Zoek een status migratie punt dat voldoet aan de minimum vereisten zoals geconfigureerd in de instellingen van het status migratie punt. Bijvoorbeeld **maximum aantal clients** en **minimale hoeveelheid vrije schijf ruimte**. Met deze optie wordt niet gegarandeerd dat er voldoende ruimte beschikbaar is op het moment van de status migratie. Deze optie vraagt toegang tot het status migratie punt om de gebruikers status en instellingen van een computer vast te leggen.  

Als de Configuration Manager-site meerdere actieve status migratie punten heeft, zoekt deze stap een status migratie punt met beschik bare schijf ruimte. De taken reeks voert een query uit op het beheer punt voor een lijst met status migratie punten en evalueert elke totdat er een wordt gevonden die voldoet aan de minimale vereisten.  

#### <a name="restore-state-from-another-computer"></a>Status herstellen vanaf een andere computer

Vraag toegang aan een status migratie punt om eerder vastgelegde gebruikers status en-instellingen naar een doel computer te herstellen.  

Als er meerdere status migratie punten zijn, zoekt deze stap het status migratie punt met de status voor de doel computer.  

#### <a name="number-of-retries"></a>Aantal keer opnieuw geprobeerd

Het aantal keren dat deze stap een geschikt status migratie punt probeert te vinden voordat dit mislukt.  

#### <a name="retry-delay-in-seconds"></a>Wachttijd nieuwe poging (seconden)

De hoeveelheid tijd in seconden dat de takenreeksstap moet wachten tussen nieuwe pogingen.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Als het computer account geen verbinding kan maken met een status opslag, gebruikt u het netwerk toegangs account

Als de taken reeks geen toegang heeft tot het status migratie punt met behulp van het computer account, worden de referenties van het netwerk toegangs account gebruikt om verbinding te maken. Deze optie is minder veilig, omdat andere computers het netwerk toegangs account kunnen gebruiken om toegang te krijgen tot de opgeslagen status. Deze optie kan nodig zijn als de doel computer niet lid is van een domein.  



## <a name="restart-computer"></a><a name="BKMK_RestartComputer"></a> Computer opnieuw opstarten

Gebruik deze stap om de computer waarop de taken reeks wordt uitgevoerd opnieuw op te starten. Na het opnieuw opstarten gaat de computer automatisch door met de volgende stap in de taken reeks.  

Deze stap kan worden uitgevoerd in het volledige besturings systeem of in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert u **computer opnieuw opstarten**.

### <a name="variables-for-restart-computer"></a>Variabelen voor computer opnieuw opstarten

Gebruik de volgende taken reeks variabelen met deze stap:  

- [SMSRebootMessage](task-sequence-variables.md#SMSRebootMessage)  
- [SMSRebootTimeout](task-sequence-variables.md#SMSRebootTimeout)  

### <a name="cmdlets-for-restart-computer"></a>Cmdlets voor het opnieuw opstarten van de computer

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepReboot](/powershell/module/configurationmanager/get-cmtsstepreboot)
- [New-CMTSStepReboot](/powershell/module/configurationmanager/new-cmtsstepreboot)
- [Remove-CMTSStepReboot](/powershell/module/configurationmanager/remove-cmtsstepreboot)
- [Set-CMTSStepReboot](/powershell/module/configurationmanager/set-cmtsstepreboot)

### <a name="properties-for-restart-computer"></a>Eigenschappen voor computer opnieuw opstarten

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>De opstartinstallatiekopie toegewezen aan deze takenreeks

Selecteer deze optie voor de doel computer om de opstart installatie kopie te gebruiken die is toegewezen aan de taken reeks. De taken reeks gebruikt de opstart installatie kopie om de volgende stappen uit te voeren in Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>Het momenteel geïnstalleerde standaard besturingssysteem

Selecteer deze optie om de doel computer opnieuw op te starten in het geïnstalleerde besturings systeem.  

#### <a name="notify-the-user-before-restarting"></a>Waarschuwing aan gebruiker voor herstart

Selecteer deze optie om een melding weer te geven voor de gebruiker voordat de doel computer opnieuw wordt opgestart. De stap selecteert standaard deze optie.  

#### <a name="notification-message"></a>Melding

Voer een meldings bericht in dat wordt weer gegeven aan de gebruiker voordat de doel computer opnieuw wordt opgestart.  

#### <a name="message-display-time-out"></a>Time-out voor weergave melding

Geef de hoeveelheid tijd in seconden op waarna de doel computer opnieuw wordt opgestart. De standaard waarde is 60 seconden.  



## <a name="restore-user-state"></a><a name="BKMK_RestoreUserState"></a> Gebruikers status herstellen

Gebruik deze stap om de Hulpprogramma voor migratie van gebruikersstatus (USMT) te initiëren voor het herstellen van de gebruikers status en-instellingen naar de doel computer. U gebruikt deze stap in combi natie met de stap **gebruikers status vastleggen** .  

Zie [gebruikers status beheren](../get-started/manage-user-state.md)voor meer informatie over het beheren van de gebruikers status bij het implementeren van besturings systemen.  

Gebruik deze stap met de stappen voor de status **opslag opvragen** en **status opslag vrijgeven** om de status instellingen op te slaan of te herstellen met een status migratie punt. Met deze optie wordt het USMT-status archief altijd ontsleuteld met behulp van een versleutelings sleutel die Configuration Manager gegenereerd en beheerd.  

De stap **gebruikers status herstellen** biedt controle over een beperkte subset van de meest gebruikte USMT-opties. Geef aanvullende opdracht regel opties op met de variabele **taken osdmigrateadditionalrestoreoptions** .  

> [!IMPORTANT]  
> Als u deze stap gebruikt voor een doel dat geen verband houdt met een implementatie scenario voor een besturings systeem, voegt u de stap [computer opnieuw opstarten](#BKMK_RestartComputer) onmiddellijk uit na de stap **gebruikers status herstellen** .  

Deze stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **gebruikers status**en selecteert u **gebruikers status herstellen**.

### <a name="variables-for-restore-user-state"></a>Variabelen voor het herstellen van de gebruikers status

Gebruik de volgende taken reeks variabelen met deze stap:  

- [_OSDMigrateUsmtRestorePackageID](task-sequence-variables.md#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](task-sequence-variables.md#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](task-sequence-variables.md#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](task-sequence-variables.md#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](task-sequence-variables.md#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](task-sequence-variables.md#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](task-sequence-variables.md#OSDStateStorePath)  

### <a name="cmdlets-for-restore-user-state"></a>Cmdlets voor het herstellen van de gebruikers status

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Get-CMTSStepRestoreUserState)
- [New-CMTSStepRestoreUserState](/powershell/module/configurationmanager/New-CMTSStepRestoreUserState)
- [Remove-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Remove-CMTSStepRestoreUserState)
- [Set-CMTSStepRestoreUserState](/powershell/module/configurationmanager/Set-CMTSStepRestoreUserState)

### <a name="properties-for-restore-user-state"></a>Eigenschappen voor Restore User State

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="user-state-migration-tool-package"></a>Pakket migratieprogramma gebruikersstatus

Geef het pakket op dat de versie van USMT bevat voor deze stap die moet worden gebruikt. Voor dit pakket is geen programma vereist. Wanneer de stap wordt uitgevoerd, gebruikt de taken reeks de versie van USMT in het opgegeven pakket. Geef een pakket op dat de 32-bits of 64-bits versie van USMT bevat. De architectuur van USMT is afhankelijk van de architectuur van het besturings systeem waarop de taken reeks wordt teruggezet.

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Alle vastgelegde gebruikersprofielen herstellen met standaardopties

Hiermee worden de vastgelegde gebruikersprofielen hersteld met de standaardopties. Als u de opties die USMT herstelt, wilt aanpassen, selecteert u **gebruikers profiel vastleggen aanpassen**.  

#### <a name="customize-how-user-profiles-are-restored"></a>Herstellen van gebruikersprofielen aanpassen

Hiermee kunt u de bestanden aanpassen die u wilt herstellen naar de doelcomputer. Selecteer **bestanden** om de configuratie bestanden op te geven in het USMT-pakket dat u wilt gebruiken voor het herstellen van de gebruikers profielen. Als u een configuratie bestand wilt toevoegen, voert u de naam van het bestand in het vak **Bestands naam** in en selecteert u vervolgens **toevoegen**. Het deel venster bestanden geeft een lijst van de configuratie bestanden die USMT gebruikt. Het. XML-bestand dat u opgeeft, definieert welk gebruikers bestand USMT herstelt.  

#### <a name="restore-local-computer-user-profiles"></a>Gebruikersprofielen lokale computer herstellen

Hiermee worden de gebruikers profielen van de lokale computer hersteld. Deze profielen zijn niet voor domein gebruikers. Nieuwe wacht woorden toewijzen aan de herstelde lokale gebruikers accounts. USMT kan de oorspronkelijke wacht woorden niet migreren. Voer het nieuwe wachtwoord in het vak **Wachtwoord** in en bevestig het wachtwoord in het vak **Wachtwoord bevestigen**.  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Doorgaan als sommige bestanden niet kunnen worden hersteld

Gaat verder met het herstellen van de gebruikers status en-instellingen, zelfs als USMT sommige bestanden niet kan herstellen. Met deze stap wordt deze optie standaard ingeschakeld. Als u deze optie uitschakelt en USMT fouten ondervindt tijdens het herstellen van bestanden, mislukt deze stap onmiddellijk. USMT herstelt niet alle bestanden.

#### <a name="enable-verbose-logging"></a>Uitgebreide logboekregistratie inschakelen

Schakel deze optie in om meer gedetailleerde informatie in het logboekbestand te genereren. Bij het herstellen van de status genereert de taken reeks standaard **Load State. log** in de map met de taken reeks logboeken `%WinDir%\ccm\logs` .  



## <a name="run-command-line"></a><a name="BKMK_RunCommandLine"></a> Opdracht regel uitvoeren

Gebruik deze stap om de opgegeven opdracht regel uit te voeren.  

De opdracht die wordt uitgevoerd, moet voldoen aan de volgende criteria:  

- Het mag niet communiceren met het bureau blad. De opdracht moet op de achtergrond of in een modus zonder toezicht worden uitgevoerd.  

- De toepassing mag zelf geen herstart initiëren. De opdracht moet een herstart aanvragen via de standaard herstart code, 3010. Dit gedrag zorgt ervoor dat de taken reeks de herstart correct afhandelt. Als de opdracht een afsluit code van 3010 retourneert, start de taken reeks engine de computer opnieuw op. Na het opnieuw opstarten wordt de takenreeks automatisch voortgezet.

Deze stap kan worden uitgevoerd in het volledige besturings systeem of in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert u **opdracht regel uitvoeren**.

### <a name="variables-for-run-command-line"></a>Variabelen voor opdracht regel uitvoeren

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDDoNotLogCommand](task-sequence-variables.md#OSDDoNotLogCommand) (vanaf versie 1902)<!--3654172-->  
- [SMSTSDisableWow64Redirection](task-sequence-variables.md#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](task-sequence-variables.md#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLineUserPassword](task-sequence-variables.md#SMSTSRunCommandLineUserPassword)  
- [SMSTSRunCommandLineAsUser](task-sequence-variables.md#SMSTSRunCommandLineAsUser) (vanaf versie 2002)<!-- 5573175 -->
- [WorkingDirectory](task-sequence-variables.md#WorkingDirectory)  

### <a name="cmdlets-for-run-command-line"></a>Cmdlets voor de opdracht regel uitvoeren

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunCommandLine](/powershell/module/configurationmanager/get-cmtsstepruncommandline)
- [New-CMTSStepRunCommandLine](/powershell/module/configurationmanager/new-cmtsstepruncommandline)
- [Remove-CMTSStepRunCommandLine](/powershell/module/configurationmanager/remove-cmtsstepruncommandline)
- [Set-CMTSStepRunCommandLine](/powershell/module/configurationmanager/set-cmtsstepruncommandline)

### <a name="properties-for-run-command-line"></a>Eigenschappen voor opdracht regel uitvoeren

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="command-line"></a>Opdrachtregel

Hiermee geeft u de opdracht regel op die door de taken reeks wordt uitgevoerd. Dit veld is vereist. Bestandsnaam extensies toevoegen, bijvoorbeeld. vbs en. exe. Neem alle vereiste instellingen bestanden en opdracht regel opties op.  

Als u de bestandsnaam extensie niet opgeeft, Configuration Manager probeert. com,. exe en. bat. Als de bestands naam een extensie heeft die geen uitvoerbaar type is, Configuration Manager probeert een lokale koppeling toe te passen. Als de opdracht regel bijvoorbeeld readme.gif is, start Configuration Manager de toepassing die is opgegeven op de doel computer voor het openen van. GIF-bestanden.  

Voorbeelden:  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> Als u wilt uitvoeren, moet u voorafgaand aan opdracht regel acties met de opdracht **cmd.exe/c** . Voor beelden van deze acties zijn uitvoer omleiding, pijpleiding en kopieer opdrachten.  

#### <a name="output-to-task-sequence-variable"></a>De variabele output to task sequence

<!--user story 4977616/bug 4798352-->

Vanaf versie 1910, sla de uitvoer van de opdracht op in een aangepaste taken reeks variabele.

> [!Note]  
> Configuration Manager beperkt deze uitvoer tot de laatste 1000 tekens.

#### <a name="disable-64-bit-file-system-redirection"></a>64-bits bestandssysteemomleiding uitschakelen 

64-bits besturings systemen gebruiken standaard de WOW64 bestands systeem-redirector om opdracht regels uit te voeren. Dit gedrag is het correct vinden van 32-bits versies van uitvoer bare bestanden van het besturings systeem en bibliotheken. Selecteer deze optie om het gebruik van de WOW64-bestandssysteem redirector uit te scha kelen. Windows voert de opdracht uit met systeem eigen 64-bits versies van uitvoer bare bestanden en bibliotheken van het besturings systeem. Deze optie heeft geen effect als deze wordt uitgevoerd op een 32-bits besturings systeem.  

#### <a name="start-in"></a>Beginnen in

Hiermee geeft u de uitvoerbare map op voor het programma, in maximaal 127 tekens. Deze map kan een absoluut pad op de doelcomputer betreffen of een relatief pad ten opzichte van de distributiepuntmap die het pakket bevat. Dit veld is optioneel.  

Voorbeelden:  

`c:\officexp`  

`i386`  

> [!NOTE]  
> Met de knop **Bladeren** wordt gebladerd naar de lokale computer voor bestanden en mappen. Alles wat u selecteert, moet ook bestaan op de doel computer. Deze moet zich op dezelfde locatie en met dezelfde bestands-en mapnamen bevinden.  

#### <a name="package"></a>Pakket

Wanneer u bestanden of Program ma's op de opdracht regel opgeeft die nog niet aanwezig zijn op de doel computer, selecteert u deze optie om het Configuration Manager-pakket op te geven dat de benodigde bestanden bevat. Voor het pakket is geen programma vereist. Als de opgegeven bestanden bestaan op de doel computer, is deze optie niet vereist.  

#### <a name="time-out"></a>Time-out

Hiermee geeft u een waarde op die aangeeft hoe lang Configuration Manager de uitvoering van de opdracht regel toestaat. Deze waarde kan een minuut tot 999 minuten zijn. De standaardwaarde is 15 minuten. Deze optie is standaard uitgeschakeld.  

> [!IMPORTANT]  
> Als u een waarde opgeeft die onvoldoende tijd heeft voor het volt ooien van de opgegeven opdracht, mislukt deze stap. De gehele taken reeks kan mislukken afhankelijk van stap-of groeps voorwaarden. Als de time-out is verlopen, Configuration Manager het opdracht regel proces beëindigen.  

#### <a name="run-this-step-as-the-following-account"></a>Deze stap uitvoeren als de volgende account

Hiermee geeft u op dat de opdracht regel wordt uitgevoerd als een Windows-gebruikers account dan het lokale systeem account.  

> [!NOTE]  
> Als u eenvoudige scripts of opdrachten met een ander account wilt uitvoeren nadat het besturings systeem is geïnstalleerd, voegt u het account eerst toe aan de computer. Het is ook mogelijk dat u Windows-gebruikers profielen moet herstellen om complexere Program ma's, zoals een Windows Installer, uit te voeren.  

#### <a name="account"></a>Account

Hiermee geeft u het Windows-gebruikers account op dat wordt gebruikt om de opdracht regel uit te voeren. De opdracht regel wordt uitgevoerd met de machtigingen van het opgegeven account. Selecteer **instellen** om het lokale gebruikers-of domein account op te geven. Zie [accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)voor meer informatie over het run as-account van de taken reeks.

> [!IMPORTANT]  
> Als met deze stap een gebruikers account wordt opgegeven en wordt uitgevoerd in Windows PE, mislukt de actie. U kunt Windows PE niet toevoegen aan een domein. In het bestand **bestand smsts. log** wordt deze fout vastgelegd.  

### <a name="options-for-run-command-line"></a>Opties voor opdracht regel uitvoeren

Naast de standaard opties configureert u de volgende extra instellingen op het tabblad **Opties** van deze taken reeks stap:  

#### <a name="success-codes"></a>Geslaagde codes

Neem andere afsluit codes op uit het script dat door de stap als geslaagd moet worden geëvalueerd.



## <a name="run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> Power shell-script uitvoeren

Gebruik deze stap om het opgegeven Windows Power shell-script uit te voeren.  

Het script moet voldoen aan de volgende criteria:  

- Het mag niet communiceren met het bureau blad. Het script moet op de achtergrond of in een modus zonder toezicht worden uitgevoerd.  

- De toepassing mag zelf geen herstart initiëren. De sscript moet een herstart aanvragen via de standaard herstart code, 3010. Dit gedrag zorgt ervoor dat de taken reeks de herstart correct afhandelt. Als het script een afsluit code van 3010 retourneert, start de taken reeks engine de computer opnieuw op. Na het opnieuw opstarten wordt de takenreeks automatisch voortgezet.

Deze stap kan worden uitgevoerd in het volledige besturings systeem of in Windows PE. Als u deze stap wilt uitvoeren in Windows PE, schakelt u Power shell in de opstart installatie kopie in. Schakel het onderdeel WinPE-Power shell in op het tabblad **optionele onderdelen** in de eigenschappen voor de opstart installatie kopie. Zie [opstart installatie kopieën beheren](../get-started/manage-boot-images.md)voor meer informatie over het wijzigen van een opstart installatie kopie.  

> [!NOTE]  
> Power shell is niet standaard ingeschakeld op Windows Embedded-besturings systemen.  

> [!WARNING]
> Bepaalde anti-malware-software kan per ongeluk gebeurtenissen activeren op basis van de taken reeks stap Configuration Manager Power shell-script uitvoeren. Het is raadzaam om%windir%\temp\smstspowershellscripts uit te sluiten, zodat deze scripts zonder storing kunnen worden uitgevoerd door de anti-malware-software.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert u **Power shell-script uitvoeren**.

### <a name="variables-for-run-powershell-script"></a>Variabelen voor het uitvoeren van Power shell-script

Gebruik de volgende taken reeks variabelen met deze stap:  

- [OSDLogPowerShellParameters](task-sequence-variables.md#OSDLogPowerShellParameters) (vanaf versie 1902)<!--3556028-->  
- [SMSTSRunPowerShellAsUser](task-sequence-variables.md#SMSTSRunPowerShellAsUser) (vanaf versie 2002)<!-- 5573175 -->
- [SMSTSRunPowerShellUserName](task-sequence-variables.md#SMSTSRunPowerShellUserName)  
- [SMSTSRunPowerShellUserPassword](task-sequence-variables.md#SMSTSRunPowerShellUserPassword)  

### <a name="cmdlets-for-run-powershell-script"></a>Cmdlets voor het uitvoeren van Power shell-script

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/get-cmtssteprunpowershellscript)
- [New-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/new-cmtssteprunpowershellscript)
- [Remove-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/remove-cmtssteprunpowershellscript)
- [Set-CMTSStepRunPowerShellScript](/powershell/module/configurationmanager/set-cmtssteprunpowershellscript)

> [!Note]  
> Ondertekende Power shell-scripts gebruiken in Unicode-indeling. De ANSI-indeling, de standaard instelling, werkt niet met deze stap.

### <a name="properties-for-run-powershell-script"></a>Eigenschappen voor Power shell-script uitvoeren

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="package"></a>Pakket

Geef het Configuration Manager-pakket op dat het Power shell-script bevat. Eén pakket kan meerdere PowerShell-scripts bevatten.  

#### <a name="script-name"></a>Scriptnaam

Hiermee geeft u de naam van het uit te voeren PowerShell-script op. Dit veld is vereist.  

#### <a name="enter-a-powershell-script"></a>Voer een Power shell-script in

<!-- 3556028 -->
Vanaf versie 1902 voert u rechtstreeks Windows Power shell-code in in deze stap. Met deze functie kunt u Power shell-opdrachten uitvoeren tijdens een taken reeks zonder eerst een pakket te maken en te distribueren met het script.

Wanneer u een script toevoegt of bewerkt, biedt het Power shell-script venster de volgende acties:  

- Het script rechtstreeks bewerken  

- Een bestaand script openen vanuit een bestand  

- Naar een bestaand goedgekeurd [script](../../apps/deploy-use/create-deploy-scripts.md) in Configuration Manager bladeren

> [!Important]  
> Als u deze nieuwe functie Configuration Manager wilt gebruiken, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Wanneer u de-site en-console bijwerkt terwijl er nieuwe functionaliteit wordt weer gegeven in de Configuration Manager-console, is het volledige scenario niet functioneel totdat de client versie ook het meest recent is.

#### <a name="parameters"></a>Parameters

Hiermee geeft u de para meters door gegeven aan het Power shell-script. Deze para meters zijn hetzelfde als de Power shell-script parameters op de opdracht regel.  

Geef parameters op die worden gebruikt door het script, niet voor de Windows PowerShell-opdrachtregel.  
Het volgende voorbeeld bevat geldige parameters:  

`-MyParameter1 MyValue1 -MyParameter2 MyValue2`  

Het volgende voorbeeld bevat ongeldige parameters. De eerste twee items zijn Windows Power shell-opdracht regel parameters (**-logo** en **-ExecutionPolicy unrestricted**). De para meters worden niet gebruikt door het script.  

`-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`

<!-- SCCMDocs-pr issue 3561 -->
Als een parameter waarde een speciaal teken bevat, gebruikt u enkele aanhalings tekens ( `'` ) rond de waarde. Het gebruik van dubbele aanhalings tekens ( `"` ) kan ertoe leiden dat de para meter in de taken reeks stap onjuist wordt verwerkt.

Bijvoorbeeld: `-Arg1 '%TSVar1%' -Arg2 '%TSVar2%'`

Met ingang van versie 2002 stelt u deze eigenschap in op een variabele.<!-- 5690481 --> Als u bijvoorbeeld opgeeft `%MyScriptVariable%` , wanneer het script door de taken reeks wordt uitgevoerd, wordt de waarde van deze aangepaste variabele toegevoegd aan de Power shell-opdracht regel.

#### <a name="powershell-execution-policy"></a>PowerShell-uitvoeringsbeleid

Bepaal welke Power shell-scripts (indien van toepassing) u wilt uitvoeren op de computer. Kies een van de volgende uitvoeringsbeleidsregels:  

- **Alles ondertekend**: alleen scripts uitvoeren die zijn ondertekend door een vertrouwde uitgever  

- Niet **gedefinieerd**: er is geen uitvoerings beleid gedefinieerd  

- **Overs Laan**: alle configuratie bestanden laden en alle scripts uitvoeren. Als u een niet-ondertekend script van internet downloadt, wordt door Windows Power shell niet om toestemming gevraagd voordat het script wordt uitgevoerd.  

> [!IMPORTANT]  
> Power shell 1,0 biedt geen ondersteuning voor het uitvoerings beleid undefined en bypass.  

#### <a name="output-to-task-sequence-variable"></a>De variabele output to task sequence

<!-- 3556028 -->
Met ingang van versie 1902 slaat u de script uitvoer op in een aangepaste taken reeks variabele.

> [!Note]  
> Vanaf versie 1910 wordt deze uitvoer door Configuration Manager beperkt tot de laatste 1000 tekens.

Zie [variabelen instellen](using-task-sequence-variables.md#bkmk_run-ps)voor een voor beeld van het gebruik van deze stap eigenschap.

#### <a name="start-in"></a>Beginnen in

<!-- 3556028 -->
Geef vanaf versie 1902 de startmap voor het script op, Maxi maal 127 tekens. Deze map kan een absoluut pad op de doelcomputer betreffen of een relatief pad ten opzichte van de distributiepuntmap die het pakket bevat. Dit veld is optioneel.  

> [!NOTE]  
> Met de knop **Bladeren** wordt gebladerd naar de lokale computer voor bestanden en mappen. Alles wat u selecteert, moet ook bestaan op de doel computer. Deze moet zich op dezelfde locatie en met dezelfde bestands-en mapnamen bevinden.  

#### <a name="time-out"></a>Time-out

<!-- 3556028 -->
Geef vanaf versie 1902 een waarde op die aangeeft hoe lang Configuration Manager het Power shell-script mag uitvoeren. Deze waarde kan een minuut tot 999 minuten zijn. De standaardwaarde is 15 minuten. Deze optie is standaard uitgeschakeld.  

> [!IMPORTANT]  
> Als u een waarde opgeeft die onvoldoende tijd heeft voor het volt ooien van het opgegeven script, mislukt deze stap. De gehele taken reeks kan mislukken afhankelijk van stap-of groeps voorwaarden. Als de time-out is verlopen, Configuration Manager het Power Shell-proces beëindigen.  

#### <a name="run-this-step-as-the-following-account"></a>Deze stap uitvoeren als de volgende account

<!-- 3556028 -->
Vanaf versie 1902 geeft u op dat het Power shell-script wordt uitgevoerd als een Windows-gebruikers account dan het lokale systeem account.  

> [!NOTE]  
> Als u eenvoudige scripts of opdrachten met een ander account wilt uitvoeren nadat het besturings systeem is geïnstalleerd, voegt u het account eerst toe aan de computer. Het is ook mogelijk dat u Windows-gebruikers profielen moet herstellen om complexere acties uit te voeren.  

#### <a name="account"></a>Account

<!-- 3556028 -->
Geef met ingang van versie 1902 het Windows-gebruikers account op dat wordt gebruikt om het Power shell-script uit te voeren. Het opgegeven account moet een lokale beheerder zijn op het systeem en het script wordt uitgevoerd met de machtigingen van dit account. Selecteer **instellen** om het lokale gebruikers-of domein account op te geven. Zie [accounts](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)voor meer informatie over het run as-account van de taken reeks.

> [!IMPORTANT]  
> Als met deze stap een gebruikers account wordt opgegeven en wordt uitgevoerd in Windows PE, mislukt de actie. U kunt Windows PE niet toevoegen aan een domein. In het bestand **bestand smsts. log** wordt deze fout vastgelegd.  

### <a name="options-for-run-powershell-script"></a>Opties voor het uitvoeren van Power shell-script

Naast de standaard opties configureert u de volgende extra instellingen op het tabblad **Opties** van deze taken reeks stap:  

#### <a name="success-codes"></a>Geslaagde codes

<!-- 3556028 -->
Vanaf versie 1902 neemt u andere afsluit codes op uit het script dat door de stap als geslaagd moet worden geëvalueerd.



## <a name="run-task-sequence"></a><a name="child-task-sequence"></a> Taken reeks uitvoeren

> [!Note]  
> In versie 1910 Configuration Manager deze functie standaard ingeschakeld. In versie 1906 of eerder is Configuration Manager deze optionele functie standaard niet ingeschakeld. Schakel deze functie in voordat u deze gebruikt. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).

In deze stap wordt een andere taken reeks uitgevoerd. Hiermee maakt u een relatie tussen een bovenliggend/onderliggend item tussen de taken reeksen. Met onderliggende taken reeksen kunt u meer modulaire, herbruikbare taken reeksen maken.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert u **taken reeks uitvoeren**.

### <a name="specifications-and-limitations-for-run-task-sequence"></a>Specificaties en beperkingen voor de taken reeks uitvoeren

Houd rekening met de volgende punten wanneer u een onderliggende taken reeks toevoegt aan een taken reeks:  

- De bovenliggende en onderliggende taken reeks worden effectief gecombineerd tot één beleid dat door de client wordt uitgevoerd.  

- De omgeving is wereld wijd. Als de bovenliggende taken reeks een variabele instelt en vervolgens de onderliggende taken reeks de variabele wijzigt, blijft de meest recente waarde behouden. Als de onderliggende taken reeks een nieuwe variabele maakt, is deze beschikbaar voor de rest van de bovenliggende taken reeks.  

- Status berichten worden per normale verzen ding verzonden voor een enkele taken reeks bewerking.  

- De taken reeks schrijft vermeldingen naar het bestand **bestand smsts. log** , met nieuwe logboek vermeldingen die duidelijk worden gemaakt wanneer een onderliggende taken reeks wordt gestart.  

<!--the following points are from SCCMdocs issue #1079-->

- U kunt een taken reeks met een verwijzing naar de opstart installatie kopie niet selecteren. Voor elke implementatie waarvoor een opstart installatie kopie is vereist, geeft u deze op in de bovenliggende taken reeks.  

- Als een onderliggende taken reeks is uitgeschakeld, mislukt de implementatie. U kunt de optie **door gaan** met niet gebruiken om deze beperking te omzeilen.  

- Als een onderliggende taken reeks stappen bevat die als *hoge impact*worden beschouwd, detecteert Software Center deze niet en wordt de melding met hoge impact weer gegeven. Wijzig de eigenschappen van de bovenliggende taken reeks op het tabblad gebruikers melding om aan te geven dat **dit een hoge impact is van de taken reeks**.  

- Als een onderliggende taken reeks een ontbrekende pakket verwijzing heeft, kan deze status niet worden gedetecteerd door de bovenliggende taken reeks te bekijken. Als u de bovenliggende taken reeks bewerkt, detecteert deze ontbrekende verwijzingen in onderliggende taken reeksen wanneer u wijzigingen aanbrengt in het bovenliggende item.  

### <a name="cmdlets-for-run-task-sequence"></a>Cmdlets voor taken reeks uitvoeren

Met ingang van versie 1906 beheert u deze stap met de volgende Power shell-cmdlets:<!-- 2839943, SCCMDocs#1118 -->

- [Get-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/get-cmtsstepruntasksequence)
- [New-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/new-cmtsstepruntasksequence)
- [Remove-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/remove-cmtsstepruntasksequence)
- [Set-CMTSStepRunTaskSequence](/powershell/module/configurationmanager/set-cmtsstepruntasksequence)

Zie [1906 release opmerkingen-nieuwe cmdlets](/powershell/sccm/1906-release-notes#new-cmdlets)voor meer informatie.

### <a name="properties-for-run-task-sequence"></a>Eigenschappen voor taken reeks uitvoeren

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="select-task-sequence-to-run"></a>Uit te voeren taken reeks selecteren

Selecteer **Bladeren** om de onderliggende taken reeks te selecteren. In het dialoog venster **een taken reeks selecteren** wordt de bovenliggende taken reeks niet weer gegeven.



## <a name="set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> Dynamische variabelen instellen

Gebruik deze stap om de volgende acties uit te voeren:  

1. Informatie verzamelen van de computer en de omgeving. Stel vervolgens de opgegeven taken reeks variabelen in met de informatie.  

2. Gedefinieerde regels evalueren. Stel taken reeks variabelen in op basis van de regels die bij waar worden geëvalueerd.  

Deze stap kan worden uitgevoerd in het volledige besturings systeem of in Windows PE.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert u **dynamische variabelen instellen**.

### <a name="variables-for-set-dynamic-variables"></a>Variabelen voor set Dynamic Varia bles

De taakvolgorde stelt automatisch de volgende alleen-lezen takenreeksvariabelen in:  

- [\_SMSTSMake](task-sequence-variables.md#SMSTSMake)  
- [\_SMSTSModel](task-sequence-variables.md#SMSTSModel)  
- [\_SMSTSMacAddresses](task-sequence-variables.md#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](task-sequence-variables.md#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](task-sequence-variables.md#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](task-sequence-variables.md#SMSTSAssetTag)  
- [\_SMSTSUUID](task-sequence-variables.md#SMSTSUUID)  

### <a name="cmdlets-for-set-dynamic-variables"></a>Cmdlets voor het instellen van dynamische variabelen

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/get-cmtsstepsetdynamicvariable)
- [New-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/new-cmtsstepsetdynamicvariable)
- [Remove-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/remove-cmtsstepsetdynamicvariable)
- [Set-CMTSStepSetDynamicVariable](/powershell/module/configurationmanager/set-cmtsstepsetdynamicvariable)

### <a name="properties-for-set-dynamic-variables"></a>Eigenschappen voor dynamische variabelen instellen

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="dynamic-rules-and-variables"></a>Dynamische regels en variabelen

Als u een dynamische variabele voor gebruik in de taken reeks wilt instellen, voegt u een regel toe. Stel vervolgens een waarde in voor elke variabele die in de regel is opgegeven. Voeg daarnaast een of meer variabelen toe zonder een regel toe te voegen. Wanneer u een regel toevoegt, kunt u kiezen uit de volgende categorieën:  

- **Computer**: waarden voor de code van de Hardware-Asset, uuid, serie nummer of Mac-adres evalueren. Stel meerdere waarden in als dat nodig is. Als een wille keurige waarde waar is, evalueert de regel als waar. De volgende regel evalueert bijvoorbeeld als waar als het serie nummer van het apparaat 5892087 is en het MAC-adres 22-A4-5A-13-78-26:  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Locatie**: waarden voor de standaard netwerk gateway evalueren  

- **Merk en model**: Beoordeel waarden voor het merk en model van een computer. Zowel het merk als het model moet resulteren in waar om de regel te laten resulteren in waar.

    Geef een asterisk ( `*` ) en een vraag teken ( `?` ) op als joker tekens. Het sterretje komt overeen met meerdere tekens en het vraag teken komt overeen met één teken. De teken reeks komt bijvoorbeeld `DELL*900?` overeen met zowel `DELL-ABC-9001` als `DELL9009` .  

- **Taken reeks variabele**: Voeg een taken reeks variabele, voor waarde en waarde toe om te evalueren. Deze regel resulteert in waar wanneer de ingestelde waarde voor de variabele voldoet aan de opgegeven voorwaarde.  

    Geef een of meer variabelen op die moeten worden ingesteld voor een regel die resulteert in waar, of stel variabelen in zonder een regel te gebruiken. Selecteer een bestaande variabele of maak een aangepaste variabele.  

  - **Bestaande taken reeks variabelen**: Selecteer een of meer variabelen uit een lijst met bestaande taken reeks variabelen. Matrix variabelen zijn niet beschikbaar om te selecteren.  

  - **Aangepaste taken reeks variabelen**: Definieer een aangepaste taken reeks variabele. U kunt ook een bestaande takenreeksvariabele opgeven. Deze instelling is handig om een bestaande variabelen matrix op te geven, zoals **OSDAdapter**, omdat variabelen matrices niet voor komen in de lijst met bestaande taken reeks variabelen.  

Nadat u de variabelen voor een regel hebt geselecteerd, geeft u een waarde op voor elke variabele. De variabele wordt ingesteld op de opgegeven waarde wanneer de regel resulteert in waar. Voor elke variabele kunt u **deze waarde niet weer geven** selecteren om de waarde van de variabele te verbergen. Standaard verbergen sommige bestaande variabelen waarden, zoals de variabele **OSDCaptureAccountPassword** .  

> [!IMPORTANT]  
> Wanneer u een taken reeks importeert met de stap **dynamische variabelen instellen** , verwijdert Configuration Manager alle variabelen waarden die zijn gemarkeerd als **deze waarde niet weer geven**. Nadat u de taken reeks hebt geïmporteerd, voert u de waarde voor de dynamische variabele opnieuw in.

Wanneer u de optie **deze waarde niet weer geven**gebruikt, wordt de waarde van de variabele niet weer gegeven in de editor voor taken reeksen. De waarde van de variabele wordt niet weer gegeven in het logboek bestand van de taken reeks (**bestand smsts. log**) of het fout opsporingsprogramma voor de taken reeks. De variabele kan nog steeds worden gebruikt door de taken reeks wanneer deze wordt uitgevoerd. Als u deze variabelen niet meer wilt verbergen, verwijdert u deze eerst. Definieer de variabelen vervolgens opnieuw zonder de optie te selecteren om ze te verbergen.  

> [!WARNING]  
> Als u variabelen opneemt in de stap **opdracht regel uitvoeren** , wordt in het logboek bestand van de taken reeks de volledige opdracht regel weer gegeven, inclusief de waarden van de variabele. Als u wilt voor komen dat mogelijk gevoelige gegevens in het logboek bestand worden weer gegeven, stelt u de taken reeks variabele **OSDDoNotLogCommand** in op `TRUE` .


## <a name="set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> Taken reeks variabele instellen

Gebruik deze stap om de waarde in te stellen van een variabele die wordt gebruikt in combi natie met de taken reeks.  

Deze stap kan worden uitgevoerd in het volledige besturings systeem of in Windows PE.

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **Algemeen**en selecteert u **taken reeks variabele instellen**.

### <a name="variables-for-set-task-sequence-variable"></a>Variabelen voor het instellen van een taken reeks variabele

Takenreeksvariabelen worden gelezen door takenreeksacties en bepalen het gedrag van deze acties. Raadpleeg de volgende artikelen voor meer informatie over specifieke taken reeks variabelen en hoe u deze kunt gebruiken:  

- [Takenreeksvariabelen gebruiken](using-task-sequence-variables.md)  
- [Takenreeksvariabelen](task-sequence-variables.md)  

### <a name="cmdlets-for-set-task-sequence-variable"></a>Cmdlets voor het instellen van een taken reeks variabele

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetVariable](/powershell/module/configurationmanager/get-cmtsstepsetvariable)
- [New-CMTSStepSetVariable](/powershell/module/configurationmanager/new-cmtsstepsetvariable)
- [Remove-CMTSStepSetVariable](/powershell/module/configurationmanager/remove-cmtsstepsetvariable)
- [Set-CMTSStepSetVariable](/powershell/module/configurationmanager/set-cmtsstepsetvariable)

### <a name="properties-for-set-task-sequence-variable"></a>Eigenschappen voor set-taken reeks variabele

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="task-sequence-variable"></a>Takenreeksvariabele

Geef de naam op van een ingebouwde taken reeks of actie variabele, of geef uw eigen naam op voor de door de gebruiker gedefinieerde variabele.  

#### <a name="do-not-display-this-value"></a>Deze waarde niet weer geven

<!--1358330-->
Schakel deze optie in om gevoelige gegevens te maskeren die zijn opgeslagen in taken reeks variabelen. Bijvoorbeeld wanneer u een wacht woord opgeeft.

> [!NOTE]
> Schakel deze optie in en stel vervolgens de waarde van de taken reeks variabele in. Anders is de waarde van de variabele niet ingesteld zoals u dat wilt, wat kan leiden tot onverwacht gedrag wanneer de taken reeks wordt uitgevoerd.<!--SCCMdocs issue #800-->

Wanneer u de optie **deze waarde niet weer geven**gebruikt, wordt de waarde van de variabele niet weer gegeven in de editor voor taken reeksen. De waarde van de variabele wordt niet weer gegeven in het logboek bestand van de taken reeks (**bestand smsts. log**) of het fout opsporingsprogramma voor de taken reeks. De variabele kan nog steeds worden gebruikt door de taken reeks wanneer deze wordt uitgevoerd. Als u deze variabele niet meer wilt verbergen, verwijdert u deze eerst. Definieer de variabele vervolgens opnieuw, zonder de optie te selecteren om deze te verbergen.

> [!WARNING]
> Als u variabelen opneemt in de stap **opdracht regel uitvoeren** , wordt in het logboek bestand van de taken reeks de volledige opdracht regel weer gegeven, inclusief de waarden van de variabele. Als u wilt voor komen dat mogelijk gevoelige gegevens in het logboek bestand worden weer gegeven, stelt u de taken reeks variabele **OSDDoNotLogCommand** in op `TRUE` .<!-- 6963278 -->

#### <a name="value"></a>Waarde  

De taken reeks stelt de variabele in op deze waarde. Stel deze taken reeks variabele in op de waarde van een andere taken reeks variabele met de syntaxis `%varname%` .  



## <a name="setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Windows en ConfigMgr installeren

Gebruik deze stap om de overgang van Windows PE naar het nieuwe besturings systeem uit te voeren. Deze taken reeks stap is een vereist onderdeel van de implementatie van een besturings systeem. De Configuration Manager-client wordt in het nieuwe besturings systeem geïnstalleerd en bereidt de taken reeks voor om de uitvoering in het nieuwe besturings systeem voort te zetten.  

Deze stap is verantwoordelijk voor het overstappen van de taken reeks van Windows PE naar het volledige besturings systeem. De stap wordt in Windows PE en het volledige besturings systeem uitgevoerd door deze overgang. Omdat de overgang echter wordt gestart in Windows PE, kan deze alleen worden toegevoegd tijdens het Windows PE-gedeelte van de taken reeks.  

Deze stap vervangt Sysprep. inf-of unattend.xml Directory-variabelen, zoals `%WINDIR%` en `%ProgramFiles%` , met de installatiemap van Windows PE `X:\Windows` . De taken reeks negeert variabelen die zijn opgegeven met behulp van deze omgevings variabelen.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **installatie kopieën**en selecteert u **Windows en ConfigMgr installeren**.

### <a name="behaviors-for-setup-windows-and-configmgr"></a>Gedrag voor het instellen van Windows en ConfigMgr

Met deze stap worden de volgende acties uitgevoerd:  

#### <a name="preliminaries-windows-pe"></a>Voor bereidingen: Windows PE  

1. Vervang taken reeks variabelen in het unattend.xml bestand.  

2. Down load het pakket dat de Configuration Manager-client bevat. Voeg het pakket toe aan de geïmplementeerde installatie kopie.  

#### <a name="set-up-windows"></a>Windows installeren  

- Installatie op basis van een installatie kopie  

    1. Schakel de Configuration Manager-client uit in de installatie kopie, als deze bestaat. Met andere woorden, Schakel automatisch starten uit voor de Configuration Manager-client service.  

    2. Werk het REGI ster in de geïmplementeerde installatie kopie bij zodat het geïmplementeerde besturings systeem wordt gestart met dezelfde stationsletter als de referentie computer.  

    3. Start opnieuw op in het geïmplementeerde besturings systeem.  

    4. Windows Mini-Setup wordt uitgevoerd met behulp van het eerder opgegeven bestand Sysprep. inf of unattend.xml, waarbij alle interactie van de eind gebruiker wordt onderdrukt. Als u de stap **netwerk instellingen Toep assen** gebruikt om lid te worden van een domein, bevindt die informatie zich in het antwoord bestand. Windows Mini-Setup voegt de computer toe aan het domein.  

- Installatie op basis van setup.exe. Voert Setup.exe uit, die de standaard Windows-installatieprocedure volgt:  

    1. Kopieer het OS-upgrade pakket dat is opgegeven in de stap **besturings systeem Toep assen** op de vaste schijf.  

    2. Start opnieuw op naar het nieuw geïmplementeerde besturings systeem.  

    3. Windows Mini-Setup wordt uitgevoerd met behulp van het eerder opgegeven Sysprep. inf-of unattend.xml antwoord bestand met alle gebruikers interface-instellingen onderdrukt. Als u de stap  **netwerk instellingen Toep assen** gebruikt om lid te worden van een domein, bevindt die informatie zich in het antwoord bestand. Windows Mini-Setup voegt de computer toe aan het domein.  

#### <a name="set-up-the-configuration-manager-client"></a>De Configuration Manager-client instellen  

1. Nadat Windows Mini-Setup is voltooid, wordt de takenreeks hervat met behulp van setupcomplete.cmd. Zie [een script uitvoeren nadat de installatie is voltooid (SetupComplete. cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd)voor meer informatie.  

2. Schakel het lokale beheerders account in of uit op basis van de geselecteerde optie in de stap **Windows-instellingen Toep assen** .  

3. Installeer de Configuration Manager-client met behulp van het eerder gedownloade pakket en de installatie-eigenschappen die in deze stap zijn opgegeven. De client wordt geïnstalleerd in ' inrichtings modus '. Deze modus voor komt dat de client nieuwe beleids aanvragen verwerkt totdat de taken reeks is voltooid. Zie [inrichtings modus](provisioning-mode.md)voor meer informatie.  

4. Wacht tot de client volledig operationeel is.  

#### <a name="the-step-completes"></a>De stap is voltooid

De taken reeks gaat verder met de volgende stap.  

> [!Note]  
> Windows-groeps beleid wordt normaal pas verwerkt nadat de taken reeks is voltooid. Dit gedrag is consistent in verschillende versies van Windows. Andere aangepaste acties tijdens de taken reeks kunnen de evaluatie van groeps beleid activeren. Zie [een script uitvoeren nadat de installatie is voltooid (SetupComplete. cmd)](/windows-hardware/manufacture/desktop/add-a-custom-script-to-windows-setup#run-a-script-after-setup-is-complete-setupcompletecmd)voor meer informatie over de volg orde van de bewerkingen. <!-- 2841304 -->


### <a name="variables-for-setup-windows-and-configmgr"></a>Variabelen voor het instellen van Windows en ConfigMgr

Gebruik de volgende taken reeks variabelen met deze stap:  

- [SMSClientInstallProperties](task-sequence-variables.md#SMSClientInstallProperties)  

### <a name="cmdlets-for-setup-windows-and-configmgr"></a>Cmdlets voor het installeren van Windows en ConfigMgr

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/get-cmtsstepsetupwindowsandconfigmgr)
- [New-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/new-cmtsstepsetupwindowsandconfigmgr)
- [Remove-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/remove-cmtsstepsetupwindowsandconfigmgr)
- [Set-CMTSStepSetupWindowsAndConfigMgr](/powershell/module/configurationmanager/set-cmtsstepsetupwindowsandconfigmgr)

### <a name="properties-for-setup-windows-and-configmgr"></a>Eigenschappen voor het installeren van Windows en ConfigMgr

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="client-package"></a>Clientpakket

Selecteer **Bladeren**en kies vervolgens het Configuration Manager-client installatie pakket dat u bij deze stap wilt gebruiken.  

#### <a name="use-pre-production-client-package-when-available"></a>Gebruik een pre-productieclientpakket indien beschikbaar

Als er een pre-production-client pakket beschikbaar is en de computer lid is van de verzameling Piloting, gebruikt de taken reeks dit pakket in plaats van het productie-client pakket. De pre-productie client is een nieuwere versie voor testen in de productie omgeving. Selecteer **Bladeren**en kies vervolgens het pre-production client-installatie pakket dat u bij deze stap wilt gebruiken.  

#### <a name="installation-properties"></a>Installatie-eigenschappen

In de taken reeks stap worden automatisch site toewijzing en de standaard configuratie opgegeven. Gebruik dit veld om eventuele aanvullende installatie-eigenschappen op te geven die moeten worden gebruikt wanneer u de-client installeert. Als u meerdere installatie-eigenschappen wilt invoeren, scheidt u deze met een spatie.  

Geef opdracht regel opties op die moeten worden gebruikt tijdens de client installatie. Voer bijvoorbeeld `/skipprereq: silverlight.exe` in om aan CCMSetup.exe te informeren dat de micro soft Silverlight-vereiste niet moet worden geïnstalleerd. Zie [over de eigenschappen van client installatie](../../core/clients/deploy/about-client-installation-properties.md)voor meer informatie over de beschik bare opdracht regel opties voor CCMSetup.exe.  

Wanneer u een taken reeks voor implementatie van een besturings systeem uitvoert op een client op het Internet, die deel uitmaakt van Azure AD of gebruikmaakt van op tokens gebaseerde verificatie, moet u de eigenschap [CCMHOSTNAME](../../core/clients/deploy/about-client-installation-properties.md#ccmhostname) opgeven in de stap **Windows en ConfigMgr van Setup** . Bijvoorbeeld `CCMHOSTNAME=OTTERFALLS.CLOUDAPP.NET/CCM_Proxy_MutualAuth/12345678907927939`.

### <a name="options-for-setup-windows-and-configmgr"></a>Opties voor het instellen van Windows en ConfigMgr

> [!NOTE]  
> Schakel **door gaan bij fout** niet in op het tabblad **Opties** . Als er tijdens deze stap een fout optreedt, mislukt de taken reeks, ongeacht of u deze instelling inschakelt.  



## <a name="upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> Besturings systeem bijwerken

Gebruik deze stap om een oudere versie van Windows bij te werken naar een nieuwere versie van Windows 10.  

Deze taken reeks stap kan alleen in het volledige besturings systeem worden uitgevoerd. Deze wordt niet uitgevoerd in Windows PE.  

Als u deze stap wilt toevoegen in de taken reeks editor, selecteert u **toevoegen**, selecteert u **installatie kopieën**en selecteert u **besturings systeem bijwerken**.

> [!TIP]
> Vanaf Windows 10, versie 1709, media bevat meerdere edities. Wanneer u een taken reeks configureert voor het gebruik van een upgrade pakket voor een besturings systeem of installatie kopie van een besturings systeem, moet u een [ondersteunde versie](../../core/plan-design/configs/support-for-windows-10.md#windows-10-as-a-client)selecteren.  
>
> Inhoud vooraf in cache opslaan gebruiken om een toepasselijk upgrade pakket voor het besturings systeem te downloaden voordat een gebruiker de taken reeks installeert. Zie [inhoud vooraf in cache configureren](../deploy-use/configure-precache-content.md)voor meer informatie.

### <a name="variables-for-upgrade-os"></a>Variabelen voor het upgraden van het besturings systeem

Gebruik de volgende taken reeks variabelen met deze stap:  

- [_SMSTSOSUpgradeActionReturnCode](task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)  
- [SetupCompletePause](task-sequence-variables.md#SetupCompletePause)
- [OSDSetupAdditionalUpgradeOptions](task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions)  

### <a name="cmdlets-for-upgrade-os"></a>Cmdlets voor het upgraden van het besturings systeem

Beheer deze stap met de volgende Power shell-cmdlets:<!-- SCCMDocs #1118 -->

- [Get-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Get-CMTSStepUpgradeOperatingSystem)
- [New-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/New-CMTSStepUpgradeOperatingSystem)
- [Remove-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Remove-CMTSStepUpgradeOperatingSystem)
- [Set-CMTSStepUpgradeOperatingSystem](/powershell/module/configurationmanager/Set-CMTSStepUpgradeOperatingSystem)

### <a name="properties-for-upgrade-os"></a>Eigenschappen voor upgrade-besturings systeem

Configureer op het tabblad **Eigenschappen** voor deze stap de instellingen die in deze sectie worden beschreven.  

#### <a name="upgrade-package"></a>Upgradepakket

Selecteer deze optie om het Windows 10 OS-upgrade pakket op te geven dat moet worden gebruikt voor de upgrade.  

#### <a name="source-path"></a>Bronpad

Hiermee geeft u een lokaal pad of netwerkpad naar de Windows 10-media die Windows Setup gebruikt. Deze instelling komt overeen met de Windows Setup opdracht regel optie `/InstallFrom` .

U kunt ook een variabele opgeven, zoals `%MyContentPath%` of `%DPC01%` . Wanneer u een variabele voor het bronpad gebruikt, stelt u de waarde ervan eerder in de taken reeks in. Gebruik bijvoorbeeld de stap [pakket inhoud downloaden](#BKMK_DownloadPackageContent) om een variabele op te geven voor de locatie van het upgrade pakket van het besturings systeem. Vervolgens gebruikt u deze variabele voor het bronpad voor deze stap.  

#### <a name="edition"></a>Editie

Geef de editie in het besturingssysteem medium op die moet worden gebruikt voor de upgrade.  

#### <a name="product-key"></a>Productcode

Geef de product code op die u wilt Toep assen op het upgrade proces.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Geef de volgende stuurprogramma-inhoud op aan Windows Setup tijdens de upgrade

Stuur Programma's toevoegen aan de doel computer tijdens het upgrade proces. De stuurprogramma's moeten compatibel zijn met Windows 10. Deze instelling komt overeen met de Windows Setup opdracht regel optie `/InstallDriver` . Zie [Windows Setup opdracht regel opties](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#installdrivers)voor meer informatie.

Geef een van de volgende opties op:  

- **Stuur programmapakket**: Selecteer **Bladeren** en kies een bestaand Stuur programmapakket in de lijst.

- **Gefaseerde inhoud**: Selecteer deze optie om de locatie voor de inhoud van het stuur programma op te geven. U kunt een lokale map, netwerkpad of een takenreeksvariabele opgeven. Wanneer u een variabele voor het bronpad gebruikt, stelt u de waarde ervan eerder in de taken reeks in. U kunt bijvoorbeeld de stap [pakket inhoud downloaden](task-sequence-steps.md#BKMK_DownloadPackageContent) gebruiken.  

> [!TIP]
> Als u dynamische inhoud wilt hebben voor meerdere typen hardware:
>
> - Gebruik meerdere exemplaren van deze stap met voor waarden voor de typen hardware en afzonderlijke stuur programma-inhoud.
>
> - Gebruik meerdere exemplaren van de stap [pakket inhoud downloaden](task-sequence-steps.md#BKMK_DownloadPackageContent) . Plaats de inhoud op een algemene locatie en gebruik vervolgens de optie **gefaseerde inhoud** . Het voor deel van deze methode is dat de taken reeks één stap voor een upgrade van het **besturings systeem** bevat.

#### <a name="time-out-minutes"></a>Time-out (minuten)

Geef het aantal minuten op waarna Configuration Manager deze stap mislukt. Deze optie is handig als Windows Setup verwerking stopt, maar niet wordt beëindigd.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Windows-installatiecompatibiliteitsscan uitvoeren zonder dat de upgrade wordt gestart

Voer de Windows Setup compatibiliteits scan uit zonder het upgrade proces te starten. Deze instelling komt overeen met de Windows Setup opdracht regel optie `/Compat ScanOnly` . Implementeer het hele OS-upgrade pakket met deze optie.

<!--SCCMDocs-pr issue 2812-->
Wanneer u deze optie inschakelt, wordt de Configuration Manager-client niet in de inrichtings modus geplaatst. Windows Setup wordt op de achtergrond uitgevoerd en de client blijft normaal functioneren. Zie [inrichtings modus](provisioning-mode.md)voor meer informatie.

Setup retourneert een afsluitcode als resultaat van de scan. De volgende tabel bevat enkele van de meest voorkomende afsluit codes:  

|Afsluitcode|Details|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Geen compatibiliteitsproblemen (gelukt).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Compatibiliteits problemen met actie-items.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|De geselecteerde migratie keuze is niet beschikbaar. Bijvoorbeeld een upgrade van Enterprise naar Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Komt niet in aanmerking voor Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Onvoldoende vrije schijfruimte.|  

Zie [Windows Setup opdracht regel opties](/windows-hardware/manufacture/desktop/windows-setup-command-line-options#compat)voor meer informatie over deze para meter.  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Verwijder compatibiliteitsberichten die kunnen worden genegeerd

Hiermee geeft u op dat de installatie door Setup wordt voltooid en dat er dismissible-compatibiliteits berichten worden genegeerd. Deze instelling komt overeen met de Windows Setup opdracht regel optie `/Compat IgnoreWarning` .  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Installatie van Windows dynamisch bijwerken met Windows Update

Schakel Setup in om dynamische update bewerkingen uit te voeren, zoals zoeken, downloaden en installeren van updates. Deze instelling komt overeen met de Windows Setup opdracht regel optie `/DynamicUpdate` . Deze instelling is niet compatibel met Configuration Manager software-updates. Schakel deze optie in als u updates beheert met zelfstandige Windows Server Update Services (WSUS) of Windows Update voor bedrijven.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Beleid negeren en standaard Microsoft Update gebruiken

Overschrijf het lokale beleid tijdelijk in realtime om dynamische update bewerkingen uit te voeren. De computer ontvangt updates van Windows Update.