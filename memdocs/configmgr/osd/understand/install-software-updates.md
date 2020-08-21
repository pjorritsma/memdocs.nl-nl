---
title: Software-updates installeren
titleSuffix: Configuration Manager
description: Aanbevelingen voor het gebruik van de taken reeks stap software-updates installeren in Configuration Manager.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 73acd43ef9d7924682de9df66487c5a04297e640
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697497"
---
# <a name="install-software-updates"></a>Software-updates installeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

De stap **software-updates installeren** wordt meestal gebruikt in Configuration Manager taken reeksen. Wanneer u het besturings systeem installeert of bijwerkt, worden de onderdelen van software-updates geactiveerd voor het scannen en implementeren van updates. Deze stap kan een grote uitdaging veroorzaken voor sommige klanten, zoals vertragingen bij lange time-outs of gemiste updates. Gebruik de informatie in dit artikel om veelvoorkomende problemen met deze stap te verhelpen en voor betere probleem oplossing wanneer er problemen optreden.

Zie [software-updates installeren](task-sequence-steps.md#BKMK_InstallSoftwareUpdates) voor meer informatie over de stap



## <a name="recommendations"></a>Aanbevelingen

Gebruik de volgende aanbevelingen om dit proces te volt ooien:

- [Offline onderhoud gebruiken](#use-offline-servicing)
- [Enkele index](#single-index)
- [Afbeeldings grootte reduceren](#bkmk_resetbase)

### <a name="use-offline-servicing"></a>Offline onderhoud gebruiken

Gebruik Configuration Manager om regel matig toepasselijke software-updates te installeren in uw installatie kopie bestanden. Deze procedure vermindert vervolgens het aantal updates dat u tijdens de taken reeks moet installeren.

Zie [software-updates Toep assen op een installatie kopie](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)voor meer informatie.

### <a name="single-index"></a>Enkele index

Veel afbeeldings bestanden bevatten meerdere indexen, zoals voor verschillende versies van Windows. Verminder het afbeeldings bestand naar een enkele index die u nodig hebt. Deze werk wijze reduceert de hoeveelheid tijd om software-updates toe te passen op de installatie kopie. Het biedt ook de volgende aanbeveling om de grootte van de afbeelding te reduceren.

Vanaf versie 1902 kunt u dit proces automatiseren wanneer u een installatie kopie van een besturings systeem toevoegt aan de site. Zie [een installatie kopie van een besturings systeem toevoegen](../get-started/manage-operating-system-images.md#BKMK_AddOSImages)voor meer informatie.<!--3719699-->

### <a name="reduce-image-size"></a><a name="bkmk_resetbase"></a> Afbeeldings grootte reduceren

Wanneer u software-updates op de installatie kopie toepast, optimaliseert u de uitvoer door vervangen updates te verwijderen. Gebruik het opdracht regel programma DISM, bijvoorbeeld:

``` Command
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```

Vanaf versie 1902 is er een nieuwe optie om dit proces te automatiseren. Zie [geoptimaliseerde installatie kopie onderhoud](../get-started/manage-operating-system-images.md#bkmk_resetbase)voor meer informatie.<!--3555951-->


## <a name="image-engineering-decisions"></a>Technische beslissingen over image

Wanneer u uw imaging-proces ontwerpt, zijn er verschillende opties die van invloed kunnen zijn op de installatie van software-updates:

- [De installatie kopie periodiek opnieuw vastleggen](#bkmk_goldimage)  
- [Offline onderhoud gebruiken](#bkmk_offline)  
- [Alleen de standaard installatie kopie gebruiken](#bkmk_installwim)

### <a name="periodically-recapture-the-image"></a><a name="bkmk_goldimage"></a> De installatie kopie periodiek opnieuw vastleggen

U hebt een geautomatiseerd proces om een aangepaste installatie kopie van het besturings systeem vast te leggen volgens een regel matig schema. Met deze taken reeks voor vastleggen worden de nieuwste software-updates geïnstalleerd. Deze updates kunnen cumulatieve, niet-cumulatieve en andere essentiële updates omvatten, zoals het onderhouds stack-updates (SSU). Met de taken reeks implementatie worden na het vastleggen extra updates geïnstalleerd.

Zie [een taken reeks maken voor het vastleggen van een besturings systeem](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)voor meer informatie over dit proces.

#### <a name="advantages"></a>Voordelen

- Minder updates die moeten worden toegepast tijdens de implementatie tijd per client, waardoor tijd en band breedte tijdens de implementatie worden bespaard
- Minder updates voor het uitvoeren van een herstart
- Aangepaste afbeelding voor de organisatie
- Minder variabelen tijdens de implementatie

#### <a name="disadvantages"></a>Nadelen

- Tijd om een installatie kopie te maken en vast te leggen, zelfs als deze voornamelijk is geautomatiseerd
- Verhoogde tijd voor het distribueren van de installatie kopie naar distributie punten, die kan worden gezien als storing voor actieve implementaties
- De tijd die nodig is om te testen via pre-productie omgevingen is langer dan de besturingssysteem patch cyclus, waardoor de bijgewerkte installatie kopie irrelevant kan worden


### <a name="use-offline-servicing"></a><a name="bkmk_offline"></a> Offline onderhoud gebruiken

Plan Configuration Manager om software-updates toe te passen op uw installatie kopieën.

Zie [software-updates Toep assen op een installatie kopie](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates)voor meer informatie.

#### <a name="advantages"></a>Voordelen

- Minder updates die moeten worden toegepast tijdens de implementatie tijd per client, waardoor tijd en band breedte tijdens de implementatie worden bespaard
- Minder updates voor het uitvoeren van een herstart
- U kunt het onderhouds proces plannen op de site

#### <a name="disadvantages"></a>Nadelen

- Hand matige selectie van updates
- Verhoogde tijd om de installatie kopie naar distributie punten te distribueren
- Ondersteunt alleen op CBS gebaseerde updates. Er kunnen geen updates van Microsoft 365 apps worden toegepast

> [!Tip]  
> U kunt de selectie van software-updates automatiseren met behulp van Power shell. Gebruik de cmdlet [Get-CMSoftwareUpdate](/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) om een lijst met updates op te halen. Gebruik vervolgens de cmdlet [New-CMOperatingSystemImageUpdateSchedule](/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) om het offline-onderhouds schema te maken. In het volgende voor beeld ziet u een methode om deze actie te automatiseren:
>
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
>
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
>
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True
> ```


### <a name="use-default-image-only"></a><a name="bkmk_installwim"></a> Alleen de standaard installatie kopie gebruiken

Gebruik het standaard installatie kopie bestand voor Windows Install. Wim in de taken reeksen van uw implementatie.

#### <a name="advantages"></a>Voordelen

- Een bekende goede bron, waardoor het risico van beschadiging van de afbeelding als een mogelijk probleem wordt verkleind
- Elimineert wijzigingen in de afbeelding als een mogelijk probleem

#### <a name="disadvantages"></a>Nadelen

- Mogelijk voor grote hoeveel heden updates tijdens de implementatie
- Verhoogde implementatie tijd voor elk apparaat
- Mogelijk zijn er geen aanpassingen nodig, moeten aanvullende taken reeks stappen worden aangepast



## <a name="flowchart"></a>Shape

Dit stroom diagram toont het proces wanneer u de stap software-updates installeren in een taken reeks opneemt.

[Het diagram op volledige grootte weer geven](media/ts-step-install-software-updates.svg)

![Stroom diagram voor de taken reeks stap software-updates installeren](media/ts-step-install-software-updates.svg)  

1. **Het proces wordt gestart op de client**: een taken reeks die wordt uitgevoerd op een client bevat de stap software-updates installeren.
2. **Beleid compileren en evalueren**: de client compileert alle software-update beleidsregels in de WMI RequestedConfigs-naam ruimte. (CIAgent. log)
3. *Is dit exemplaar de eerste keer dat het wordt aangeroepen?*  
    1. **Ja**: naar **volledige scan**  
    2. **Nee**: *is de stap geconfigureerd met de optie om [software-updates te evalueren vanuit scan resultaten in het cache geheugen](task-sequence-steps.md#evaluate-software-updates-from-cached-scan-results)?*
        1. **Ja**: naar de **Scan gaan vanuit de resultaten in de cache**
        2. **Nee**: naar **volledige scan**
4. Scan proces: een volledige scan of scan van resultaten in de cache, met bewakings proces parallel.
    1. **Volledige scan**: met de taken reeks engine wordt de Software-Update Agent via de API voor Update Scan aangeroepen om een *volledige* scan uit te voeren. (WUAHandler. log, ScanAgent. log)  
        1. **Sum agent scan-Full**: normaal scan proces via Windows Update Agent (WUA), dat communiceert met het software-update punt waarop WSUS wordt uitgevoerd. Alle toepasselijke updates worden toegevoegd aan de lokale update opslag. (WindowsUpdate. log, update Store. log)
    2. **Scannen vanuit cache resultaten**: de taken reeks engine roept via de API voor Update Scan de Software-Update Agent aan om te scannen op meta gegevens in de cache. (WUAHandler. log, ScanAgent. log)
        1. **Sum agent scan-in cache opgeslagen**: de WUA-controles (Windows Update Agent) controleren op updates die al in de cache zijn opgeslagen in de lokale update Store. (WindowsUpdate. log, update Store. log)
    3. **Scan timer starten**: de taken reeks Engine start een timer en wacht. (Dit proces gebeurt parallel met de volledige scan of scan uit het resultaat van een cache.)
        1. **Bewaking**: de taak reeks engine bewaakt de sum-agent voor de status.
        2. *Wat is de reactie van de SUM-agent?*
            - Wordt **uitgevoerd**: de timer heeft de waarde in de taken reeks variabele [SMSTSSoftwareUpdateScanTimeout](task-sequence-variables.md#SMSTSSoftwareUpdateScanTimeout)bereikt? (Standaard 1 uur)
                - **Ja**: de stap is mislukt.
                - **Nee**: naar **bewaking** gaan
            - **Mislukt**: de stap is mislukt.
            - **Volt ooien**: Ga naar **lijst met opsommings updates**
5. **Update lijst opsommen**: de sum-agent somt de lijst met updates op die zijn geretourneerd door de scan, waardoor wordt bepaald welke of verplicht is.
6. *Zijn er updates in de lijst met scan resultaten?*
    - **Ja**: Ga naar **updates installeren**
    - **Nee**: niets te installeren, de stap is voltooid.
7. Implementatie proces: het proces voor het installeren van updates gebeurt parallel met het bewakings proces voor de implementatie.
    1. **Updates installeren**: met de taken reeks engine wordt de sum-agent via update-implementatie-API aangeroepen om alle beschik bare of alleen verplichte updates te installeren. Dit gedrag is gebaseerd op de configuratie van de stap, ongeacht of u **vereist hebt geselecteerd voor installatie-verplichte software-updates of alleen** **beschikbaar voor installatie-alle software-updates**. U kunt dit gedrag ook opgeven met behulp van de [SMSInstallUpdateTarget](task-sequence-variables.md#SMSInstallUpdateTarget) -variabele.
        1. **Sum-agent installatie**: normaal installatie proces met behulp van de bestaande lijst met updates in de cache met standaard inhoud downloaden. Installeer update via Windows Update Agent (WUA). (UpdatesDeployment. log, Updatehandler. log, WuaHandler. log, WindowsUpdate. log)
    2. **Implementatie timer starten en voortgang weer geven**: met de taken reeks-engine wordt een installatie Timer gestart, wordt de subvoortgang van 10% intervallen in de gebruikers interface van TS uitgevoerd en wordt gewacht.
        1. **Bewaking**: de taken reeks engine vraagt de sum-agent op status.
        2. *Wat is de reactie van de SUM-agent?*
            - Wordt **uitgevoerd**: *heeft het installatie proces 8 uur inactief?*
                - **Ja**: de stap is mislukt.
                - **Nee**: naar **bewaking** gaan
            - **Mislukt**: de stap is mislukt.
            - **Volt ooien**: Ga naar *is de stap die is geconfigureerd met de optie om **software-updates te evalueren vanuit scan resultaten in het cache geheugen**?*


### <a name="timeouts"></a>Time-outs

Het diagram bevat twee van de time-outvaria bles die van toepassing zijn op deze stap. Er zijn andere standaard timers van andere onderdelen die van invloed kunnen zijn op dit proces.

- Time-out van Update Scan: 1 uur (bestand smsts. log)  
- Locatie aanvraag time-out: 1 uur (bestand locationservices. log, CAS. log)  
- Time-out bij downloaden van inhoud: 1 uur (DTS. log)  
- Time-out van inactieve distributie punt: 1 uur (bestand locationservices. log, CAS. log)  
- Totale inactieve time-out bij installatie: 8 uur (bestand smsts. log)  



## <a name="troubleshooting"></a>Problemen oplossen

Gebruik de volgende bronnen en aanvullende informatie om u te helpen bij het oplossen van problemen met deze stap:

- Zorg ervoor dat u uw software-update-implementaties naar dezelfde verzameling richt als de taken reeks implementatie.  

- Zorg ervoor dat u software-update punten in grens groepen opneemt. Zie dit [Microsoft ondersteuning artikel](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager)voor meer informatie.  

- Zie [Software Update Management Troubleshooting](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager)(Engelstalig) voor informatie over het oplossen van problemen met het software-update beheer proces.  

- Om de algehele prestaties te verbeteren, vermindert u de omvang van de Software-Update catalogus. Bijvoorbeeld:  

    - Verwijder overbodige classificaties, producten en talen. Zie voor meer informatie [classificaties en producten configureren om te synchroniseren](../../sum/get-started/configure-classifications-and-products.md).  

    - De site database opnieuw indexeren en statistieken opnieuw samen stellen. Zie voor meer informatie het document [Configuration Manager perf en schaal richtlijnen](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).  

    - Weiger overbodige updates, bijvoorbeeld:
        - Vervangen (vanaf versie 1810 wordt deze actie door Configuration Manager uitgevoerd. Zie voor meer informatie het [opruimen van WSUS vanaf versie 1810](../../sum/deploy-use/software-updates-maintenance.md#wsus-cleanup-behavior-starting-in-version-1810).)
        - Intel
        - Bèta
        - Volgende versie
        - ARM
        - Versies van Windows die u niet implementeert