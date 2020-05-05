---
title: Een takenreeks voor een besturingssysteem maken
titleSuffix: Configuration Manager
description: Een taken reeks gebruiken om automatisch bij te werken van Windows 7 of hoger naar Windows 10
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b11e0a1747cb8303c14f5971b98d337ae7b2a834
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723003"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Een taken reeks maken om een besturings systeem in Configuration Manager bij te werken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik taken reeksen in Configuration Manager om automatisch een besturings systeem op een doel computer te upgraden. Deze upgrade kan van Windows 7 of hoger naar Windows 10 of van Windows Server 2012 of hoger naar Windows Server 2016 zijn. Maak een taken reeks die verwijst naar het upgrade pakket van het besturings systeem en eventuele andere inhoud die moet worden geïnstalleerd, zoals toepassingen of software-updates. De taken reeks voor het upgraden van een besturings systeem maakt deel uit van de [upgrade-vensters naar het nieuwste versie](upgrade-windows-to-the-latest-version.md) scenario.  


## <a name="prerequisites"></a>Vereisten

Voordat u de taken reeks maakt, moeten de volgende vereisten aanwezig zijn:

### <a name="required"></a>Vereist

- Het [upgrade pakket voor het besturings systeem](../get-started/manage-operating-system-upgrade-packages.md) moet beschikbaar zijn in de Configuration Manager-console.  

- Als u een upgrade naar Windows Server 2016 wilt uitvoeren, selecteert u de instelling **negeert mogelijke compatibiliteits berichten** in de taken reeks stap besturings systeem bijwerken. Anders mislukt de upgrade.  

### <a name="required-if-used"></a>Vereist (indien gebruikt)  

- [Software-updates](../../sum/get-started/synchronize-software-updates.md) moeten worden gesynchroniseerd in de Configuration Manager-console.  

- [Toepassingen](../../apps/deploy-use/create-applications.md) moeten worden toegevoegd aan de Configuration Manager-console.  


## <a name="create-a-task-sequence-to-upgrade-an-os"></a><a name="BKMK_UpgradeOS"></a>Een taken reeks maken om een besturings systeem bij te werken  

Als u het besturings systeem op clients wilt upgraden, maakt u een taken reeks en selecteert u **een upgrade uitvoeren van een besturingssysteem van upgrade pakket** in de wizard taken reeks maken. De wizard voegt de taken reeks stappen toe om het besturings systeem bij te werken, software-updates toe te passen en toepassingen te installeren.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens **taken reeksen**.  

2. Selecteer **taken reeks maken**op het tabblad **Start** van het lint in de groep **maken** .  

3. Selecteer op de pagina **nieuwe taken reeks maken** van de wizard taken reeks maken de optie **een besturings systeem bijwerken vanuit een upgrade pakket**en selecteer **volgende**.  

4. Geef op de pagina **taken reeks informatie** de volgende instellingen op:  

    - **Takenreeksnaam**: geef een naam op die de takenreeks identificeert.  

    - **Beschrijving**: Geef eventueel een beschrijving op.  

5. Geef op de pagina **Windows-besturings systeem bijwerken** de volgende instellingen op:  

    - **Upgrade pakket**: Geef het upgrade pakket op dat de bron bestanden voor het bijwerken van het besturings systeem bevat. Controleer of u het juiste upgrade pakket hebt geselecteerd door te kijken naar de informatie in het deel venster **Eigenschappen** . Zie [upgrade pakketten voor besturings systemen beheren](../get-started/manage-operating-system-upgrade-packages.md)voor meer informatie.  

    - **Editie-index**: als er meerdere OS Edition-indexen beschikbaar zijn in het pakket, selecteert u de gewenste editie-index. De wizard selecteert standaard de eerste index.  

    - **Product code**: Geef de Windows-product code op voor het besturings systeem dat u wilt installeren. Geef gecodeerde volume licentie sleutels of standaard product codes op. Als u een standaard product code gebruikt, scheidt u elke groep van vijf tekens met een`-`streepje (). Bijvoorbeeld: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`. Wanneer de upgrade is voor een volume licentie-editie, is de product code mogelijk niet vereist.  

        > [!Note]  
        > Deze product code kan een meervoudige activerings code (MAK) of een algemene volume licentie code (GVLK) zijn. Een GVLK wordt ook wel een configuratie sleutel voor de KMS-client (Key Management service) genoemd. Zie [volume activering plannen](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)voor meer informatie. Zie [bijlage a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) van de Windows Server-activerings handleiding voor een lijst met installatie sleutels voor KMS-clients.

    - **Negeer mogelijke compatibiliteits berichten**: Selecteer deze instelling als u een upgrade uitvoert naar Windows Server 2016. Als u deze instelling niet selecteert, kan de taken reeks niet worden voltooid omdat Windows Setup wacht totdat de gebruiker op **bevestigen** klikt in het dialoog venster Windows-app-compatibiliteit.  

6. Geef op de pagina **updates toevoegen** aan of u vereiste, alle of geen software-updates wilt installeren. Selecteer **volgende**. Als u opgeeft om software-updates te installeren, installeert Configuration Manager alleen de updates die zijn gericht op de verzamelingen waarvan de doel computer lid is.  

7. Geef op de pagina **toepassingen installeren** de toepassingen op die moeten worden geïnstalleerd op de doel computer en selecteer **volgende**. Als u meer dan één toepassing selecteert, geeft u ook op of de taken reeks moet worden voortgezet als de installatie van een bepaalde toepassing mislukt.  

8. Voltooi de wizard.  

> [!Important]  
> Wanneer de taken reeks op een apparaat wordt uitgevoerd, maakt de Configuration Manager-client verschillende scripts voor het beheren van het gedrag van de taken reeks in verschillende scenario's. Wanneer de taken reeks is voltooid, worden deze scripts pas verwijderd door de client nadat de computer opnieuw is opgestart. Deze script bestanden bevatten geen gevoelige informatie.  

De standaard taken reeks sjabloon voor Windows 10 in-place upgrade bevat extra groepen met aanbevolen acties die moeten worden toegevoegd voor en na het upgrade proces. Deze acties zijn gebruikelijk voor veel klanten die apparaten met succes upgraden naar Windows 10. Zie Aanbevolen taken reeks stappen voor [het voorbereiden van de upgrade](#recommended-task-sequence-steps-to-prepare-for-upgrade) en voor een [naverwerking](#recommended-task-sequence-steps-for-post-processing)voor meer informatie.

Vanaf versie 1806 bevat deze taken reeks sjabloon ook een groep met aanbevolen acties om toe te voegen in het geval dat het upgrade proces mislukt. Deze acties maken het gemakkelijker om problemen op te lossen. Zie [Aanbevolen taken reeks stappen bij fout](#recommended-task-sequence-steps-on-failure)voor meer informatie.<!--1358500-->  


## <a name="configure-pre-cache-content"></a>Vooraf in cachegeheugen opgeslagen inhoud configureren

<!--1021244-->
Met de functie voor het vooraf opslaan van beschik bare implementaties van taken reeksen kunnen clients relevante inhoud van het OS-upgrade pakket downloaden voordat een gebruiker de taken reeks installeert.  

Zie [inhoud vooraf in cache configureren](configure-precache-content.md)voor meer informatie.


## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Aanbevolen stappen voor de taken reeks om de upgrade voor te bereiden

De standaard taken reeks sjabloon voor Windows 10 in-place upgrade bevat extra groepen met aanbevolen acties om toe te voegen vóór het upgrade proces. Deze acties in de **voor bereiding voor-upgrade** groep zijn gebruikelijk voor veel klanten die apparaten met succes upgraden naar Windows 10. Als u een bestaande taken reeks hebt die deze acties nog niet hebt, voegt u deze hand matig toe aan de taken reeks in de groep **voorbereiden voor upgrade** .  

### <a name="battery-checks"></a>Batterij controles

Voeg stappen in deze groep toe om te controleren of de computer accu of Wired Power gebruikt. Voor deze actie is een aangepast script of hulp programma vereist om deze controle uit te voeren.

#### <a name="battery-check-example"></a>Voor beeld van batterij controle

Gebruik WbemTest en maak verbinding met `root\cimv2` de naam ruimte. Voer vervolgens de volgende query uit:

`Select BatteryStatus From Win32_Battery where BatteryStatus != 2`

Als er resultaten worden geretourneerd, wordt het apparaat op de batterij uitgevoerd. Als dat niet het geval is, is het apparaat verbonden met de bekabelde voeding.  

### <a name="networkwired-connection-checks"></a>Controles van netwerk/bekabelde verbinding

Voeg stappen in deze groep toe om te controleren of de computer is verbonden met een netwerk en geen draadloze verbinding gebruikt. Voor deze actie is een aangepast script of hulp programma vereist om deze controle uit te voeren.

#### <a name="network-check-example"></a>Netwerk controle-voor beeld

Gebruik WbemTest en maak verbinding met `root\cimv2` de naam ruimte. Voer vervolgens de volgende query uit:

`Select * From Win32_NetworkAdapter Where NetConnectionStatus = 2 and PhysicalAdapter = 'True' and NetConnectionID = 'Wi-Fi'`

Als er resultaten worden geretourneerd, wordt het apparaat uitgevoerd op Wi-Fi. Anders is het apparaat verbonden met een bekabelde netwerk verbinding.

### <a name="remove-incompatible-applications"></a>Niet-compatibele toepassingen verwijderen

Voeg stappen voor het verwijderen van alle toepassingen die niet compatibel zijn met deze versie van Windows 10, toe aan deze groep. De methode voor het verwijderen van een toepassing varieert.  

Als de toepassing Windows Installer gebruikt, kopieert u de opdracht regel voor het **Uninstall-programma** van het tabblad **Program ma's** van de Windows Installer implementatie type-eigenschappen van de toepassing. Voeg vervolgens de stap **opdracht regel uitvoeren** in deze groep toe met de opdracht regel voor het verwijderen van het programma. Bijvoorbeeld:

`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`  

### <a name="remove-incompatible-drivers"></a>Niet-compatibele Stuur Programma's verwijderen

Voeg stappen voor het verwijderen van Stuur Programma's die niet compatibel zijn met deze versie van Windows 10, toe aan deze groep.  

### <a name="removesuspend-third-party-security"></a>Beveiliging van derden verwijderen/opschorten

Voeg stappen voor het verwijderen of onderbreken van externe beveiligings Programma's, zoals antivirus software, toe aan deze groep.  

Als u een schijf versleutelings programma van derden gebruikt, geeft u het versleutelings stuur programma `/ReflectDrivers` voor het Windows Setup met de [opdracht regel optie](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#reflectdrivers). Voeg een [set taken reeks variabelen voor sets](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) toe aan de taken reeks in deze groep. Stel de taken reeks variabele in op **OSDSetupAdditionalUpgradeOptions**. Stel de waarde in `/ReflectDrivers` op met het pad naar het stuur programma. Met deze [taken reeks variabele](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) wordt de Windows Setup opdracht regel toegevoegd die wordt gebruikt door de taken reeks. Neem contact op met de software leverancier voor meer informatie over dit proces.  

### <a name="download-package-content-task-sequence-step"></a>De taken reeks stap pakket inhoud downloaden  

Gebruik de stap [pakket inhoud downloaden](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) voor de stap **besturings systeem bijwerken** in de volgende scenario's:  

- U gebruikt één upgrade taken reeks voor zowel x86-als x64-platforms. Voeg twee stappen **pakket inhoud downloaden** toe aan de groep **voor bereiding van de upgrade** . Stel voor waarden in voor elke stap om de client architectuur te detecteren. Dit heeft tot gevolg dat de stap alleen het juiste upgrade pakket voor het besturings systeem downloadt. Configureer elke **Pakketinhoud downloaden**-stap zodanig dat dezelfde variabele wordt gebruikt, en gebruik de variabele voor het mediumpad in de stap **Besturingssysteem bijwerken**.  

- Als u een geschikt stuurprogrammapakket wilt downloaden, gebruikt u twee **Pakketinhoud downloaden**-stappen op voorwaarde dat het juiste hardwaretype wordt gedetecteerd voor elk stuurprogrammapakket. Configureer elke stap **pakket inhoud downloaden** om dezelfde variabele te gebruiken. Gebruik vervolgens die variabele voor de waarde van de **gefaseerde inhoud** in het gedeelte Stuur Programma's van de stap **besturings systeem bijwerken** .  

    > [!NOTE]  
    > Configuration Manager voegt een numeriek achtervoegsel toe aan deze naam van de variabele. Als u bijvoorbeeld een aangepaste variabele `%mycontent%` opgeeft, slaat de client alle inhoud waarnaar wordt verwezen, op op deze locatie. Wanneer u in een volgende stap naar de variabele verwijst, zoals **besturings systeem bijwerken**, gebruikt u de variabele met een numeriek achtervoegsel. In dit voor beeld `%mycontent01%` of `%mycontent02%`, waarbij het nummer overeenkomt met de volg orde waarin de stap **pakket inhoud downloaden** deze specifieke inhoud bevat.  


## <a name="recommended-task-sequence-steps-for-post-processing"></a>Aanbevolen stappen voor de taken reeks voor naverwerking

Nadat u de taken reeks hebt gemaakt, voegt u extra stappen toe aan de **verwerkings** groep van de taken reeks.  

> [!NOTE]  
> Deze taken reeks is niet lineair. Er zijn voor waarden voor de stappen die van invloed kunnen zijn op de resultaten van de taken reeks. Dit gedrag is afhankelijk van het feit of de client computer met succes wordt bijgewerkt of dat de client computer moet worden teruggedraaid naar het oorspronkelijke besturings systeem.  

De standaard taken reeks sjabloon voor Windows 10 in-place upgrade bevat extra groepen met aanbevolen acties om toe te voegen na het upgrade proces. Deze acties in de **verwerkings** groep zijn gebruikelijk voor veel klanten die apparaten met succes upgraden naar Windows 10. Als u een bestaande taken reeks hebt die deze acties nog niet hebt, voegt u deze hand matig toe aan uw taken reeks in de **verwerkings** groep.  

### <a name="apply-setup-based-drivers"></a>Op installatie gebaseerde Stuur programma's toep assen

Voeg stappen voor het installeren van Stuur programma's (. exe) vanuit pakketten toe aan deze groep.  

### <a name="installenable-third-party-security"></a>Beveiliging van derden installeren/inschakelen

Voeg stappen voor het installeren of inschakelen van externe beveiligings Programma's, zoals antivirus software, toe aan deze groep.  

### <a name="set-windows-default-apps-and-associations"></a>Windows-standaard-apps en-koppelingen instellen

Voeg stappen in deze groep toe om Windows-standaard-apps en-bestands koppelingen in te stellen.

1. Bereid een referentie computer voor met de gewenste app-koppelingen.
1. Voer de volgende opdracht regel uit om te exporteren:  
    `dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`  
1. Voeg het XML-bestand toe aan een pakket.
1. Voeg een [Run-opdracht regel](../understand/task-sequence-steps.md#BKMK_RunCommandLine) stap toe aan deze groep. Geef het pakket op dat het XML-bestand bevat en geef vervolgens de volgende opdracht regel op:  
    `dism /online /Import-DefaultAppAssociations:DefaultAppAssociations.xml`  

Zie [standaard toepassings koppelingen exporteren of importeren](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations)voor meer informatie.

### <a name="apply-customizations-and-personalization"></a>Aanpassingen en persoonlijke instellingen Toep assen

Voeg stappen voor het Toep assen van aanpassingen van het start menu, zoals het organiseren van programma groepen, toe aan deze groep. Zie [het Start scherm aanpassen](/windows-hardware/manufacture/desktop/customize-the-start-screen)voor meer informatie.  


## <a name="optional-task-sequence-steps-for-rollback"></a>Optionele taken reeks stappen voor terugdraaien  

Wanneer er iets mis gaat met het upgrade proces nadat de computer opnieuw is opgestart, wordt Windows Setup het systeem teruggedraaid naar het vorige besturings systeem. De taken reeks gaat vervolgens door met de stappen in de groep **terugdraaien** . Nadat u de taken reeks hebt gemaakt, voegt u indien nodig optionele stappen in deze groep toe. U kunt bijvoorbeeld alle wijzigingen die in het systeem zijn aangebracht, terugdraaien in de voor bereiding van de upgrade groep, zoals het verwijderen van incompatibele software.


## <a name="recommended-task-sequence-steps-on-failure"></a>Aanbevolen stappen voor de taken reeks bij een fout

<!--1358500-->
Vanaf versie 1806 is de standaard taken reeks sjabloon voor Windows 10 in-place upgrade een groep bevat voor het **uitvoeren van acties bij een fout**. Deze groep bevat aanbevolen acties om toe te voegen in het geval dat het upgrade proces mislukt. Deze acties maken het gemakkelijker om problemen op te lossen.

### <a name="collect-logs"></a>Logboeken verzamelen

Als u logboeken van de client wilt verzamelen, voegt u de stappen in deze groep toe.  

- Een veelvoorkomende procedure is het kopiëren van de logboek bestanden naar een netwerk share. Gebruik de stap [verbinding maken met](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) netwerkmap om deze verbinding tot stand te brengen.  

- Als u de Kopieer bewerking wilt uitvoeren, gebruikt u een aangepast script of hulp programma met de [opdracht regel uitvoeren](../understand/task-sequence-steps.md#BKMK_RunCommandLine) of [Power shell-script uitvoeren](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript) .  

- Bestanden die moeten worden verzameld, kunnen de volgende logboeken bevatten:  
     `%_SMSTSLogPath%\*.log`  
     `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

- Zie [Windows Setup-logboek bestanden](https://docs.microsoft.com/windows/deployment/upgrade/log-files)voor meer informatie over Setupact. log en andere Windows Setup logboeken.  

- Zie [Configuration Manager client-logboeken](../../core/plan-design/hierarchy/log-files.md#BKMK_ClientLogs)voor meer informatie over Configuration Manager client Logboeken.  

- Zie [taken reeks variabelen](../understand/task-sequence-variables.md)voor meer informatie over **_SMSTSLogPath** en andere nuttige variabelen.  

### <a name="run-diagnostic-tools"></a>Diagnostische hulpprogram ma's uitvoeren

Als u aanvullende diagnostische hulpprogram ma's wilt uitvoeren, voegt u de stappen in deze groep toe. Automatiseer deze hulpprogram ma's voor het verzamelen van aanvullende informatie uit het systeem, direct na de storing.  

Een dergelijk hulp programma is Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Het is een zelfstandig diagnostisch hulp programma voor het verkrijgen van informatie over waarom een Windows 10-upgrade is mislukt.  

- Maak in Configuration Manager [een pakket](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program) voor het hulp programma.  

- Voeg een stap [opdracht regel uitvoeren](../understand/task-sequence-steps.md#BKMK_RunCommandLine) toe aan deze groep van uw taken reeks. Gebruik de **pakket** optie om te verwijzen naar het hulp programma. De volgende teken reeks is een voor beeld van een **opdracht regel**:  
    `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  


## <a name="additional-recommendations"></a>Extra aanbevelingen

### <a name="windows-documentation"></a>Windows-documentatie

Raadpleeg de Windows-documentatie om [Windows 10-upgrade fouten op te lossen](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Dit artikel bevat ook gedetailleerde informatie over het upgrade proces.  

### <a name="check-minimum-disk-space"></a>Controleer de minimale schijf ruimte

Op de standaard stap voor het controleren van de **gereedheid** kunt u **ervoor zorgen dat het minimale aantal beschik bare schijf ruimte (MB)** is. Stel de waarde in op ten minste **16384** (16 GB) voor een 32-bits OS-upgrade pakket, of **20480** (20 GB) voor de 64-bits.  

### <a name="retry-downloading-policy"></a>Het beleid opnieuw downloaden

Gebruik de **SMSTSDownloadRetryCount** [taken reeks variabele](../understand/task-sequence-variables.md#SMSTSDownloadRetryCount) SMSTSDownloadRetryCount om het beleid opnieuw te downloaden. Op dit moment wordt de client standaard twee maal opnieuw geprobeerd. Deze variabele is ingesteld op twee (2). Als uw clients zich niet op een bekabelde intranet netwerk verbinding bevinden, kunnen er extra pogingen worden gedaan om de client beleid te verkrijgen. Het gebruik van deze variabele veroorzaakt geen negatief neven effect, anders dan vertraagd mislukken als het beleid niet kan worden gedownload.<!--501016--> Verhoog ook de **SMSTSDownloadRetryDelay** -variabele van de standaard waarde van 15 seconden.  

### <a name="perform-an-inline-compatibility-assessment"></a>Een inline-compatibiliteits beoordeling uitvoeren

1. Voeg in de groep **voorbereiden voor upgrade** een tweede stap van het **besturings systeem uit** .  

    1. Geef een naam voor de *upgrade beoordeling*op.
    1. Geef hetzelfde upgrade pakket op en schakel vervolgens de optie in om **Windows Setup compatibiliteits scan uit te voeren zonder de upgrade te starten**.
    1. Schakel **door gaan bij fout** in op het tabblad Opties.  

1. Voeg direct na deze stap voor de *upgrade beoordeling* een stap **opdracht regel uitvoeren** toe. Geef de volgende opdracht regel op:

    `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`

1. Voeg op het tabblad **Opties** de volgende voor waarde toe:

    `Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400`

Deze retour code is het decimale equivalent van MOSETUP_E_COMPAT_SCANONLY (0xC1900210). Dit is een geslaagde compatibiliteits scan zonder problemen. Als de stap *upgrade beoordeling* slaagt en deze code retourneert, slaat de taken reeks deze stap over. Als de evaluatie stap een andere retour code retourneert, mislukt deze stap de taken reeks met de retour code van de Windows Setup compatibiliteits scan. Zie [taken reeks variabelen](../understand/task-sequence-variables.md#SMSTSOSUpgradeActionReturnCode)voor meer informatie over **_SMSTSOSUpgradeActionReturnCode**.

Zie [upgrade van besturings systeem](../understand/task-sequence-steps.md#BKMK_UpgradeOS)voor meer informatie.  

### <a name="convert-from-bios-to-uefi"></a>Converteren van BIOS naar UEFI

Als u het apparaat wilt wijzigen van BIOS in UEFI tijdens deze taken reeks, raadpleegt u de [conversie van BIOS naar UEFI tijdens een in-place upgrade](task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).  

### <a name="manage-bitlocker"></a>BitLocker beheren

<!--SCCMDocs issue #494-->
Als u BitLocker-schijf versleuteling gebruikt, wordt de standaard Windows Setup automatisch onderbroken tijdens de upgrade. Vanaf Windows 10 versie 1803 bevat Windows Setup de `/BitLocker` opdracht regel parameter om dit gedrag te bepalen. Als voor uw beveiligings vereisten altijd actieve schijf versleuteling moet worden ingeschakeld, gebruikt u de [taken reeks variabele](../understand/task-sequence-variables.md#OSDSetupAdditionalUpgradeOptions) **OSDSetupAdditionalUpgradeOptions** in de **voor bereiding van de upgrade** groep `/BitLocker TryKeepActive`die u wilt toevoegen. Zie [Windows Setup opdracht regel opties](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#bitlocker)voor meer informatie.

### <a name="remove-default-apps"></a>Standaard-apps verwijderen

<!--SCCMDocs issue #526-->
Sommige klanten verwijderen standaard ingerichte apps in Windows 10. Bijvoorbeeld de Bing weer-app of de micro soft Patience-verzameling. In sommige gevallen retour neren deze apps na het bijwerken van Windows 10. Zie [How to keep apps unmoved from Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update)(Engelstalig) voor meer informatie.

Voeg een stap **opdracht regel uitvoeren** toe aan de taken reeks in de groep **voorbereiden voor upgrade** . Geef een opdracht regel op die vergelijkbaar is met het volgende voor beeld:

`cmd /c reg add "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f`
