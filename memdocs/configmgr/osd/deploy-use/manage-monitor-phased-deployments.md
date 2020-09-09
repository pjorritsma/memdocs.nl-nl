---
title: Gefaseerde implementaties van & controle beheren
titleSuffix: Configuration Manager
description: Meer informatie over het beheren en bewaken van gefaseerde implementaties voor software in Configuration Manager.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 631a2fc3cb7df01eed1a5a6af80dd87f84455bdc
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606339"
---
# <a name="manage-and-monitor-phased-deployments"></a>Gefaseerde implementaties beheren en bewaken

In dit artikel wordt beschreven hoe u gefaseerde implementaties kunt beheren en bewaken. Beheer taken zijn het hand matig starten van de volgende fase en het onderbreken of hervatten van een-fase.

Eerst moet u een gefaseerde implementatie maken:

- [App](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/apps/toc.json&bc=/mem/configmgr/apps/breadcrumb/toc.json)  
- [Software-update](create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json)  
- [Takenreeks](create-phased-deployment-for-task-sequence.md)  

## <a name="move-to-the-next-phase"></a><a name="bkmk_move"></a> Naar de volgende fase gaan

Wanneer u de instelling selecteert, **begint hand matig met de tweede fase van de implementatie**, wordt de volgende fase niet automatisch door de site gestart op basis van de criteria voor geslaagde pogingen. U moet de gefaseerde implementatie naar de volgende fase verplaatsen.  

1. Hoe u deze actie start, is afhankelijk van het type geïmplementeerde software:  

    - **Toepassing**: Ga naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer **toepassingen**.

    - **Software-update**: Ga naar de werk ruimte **software bibliotheek** en selecteer een van de volgende knoop punten:
        - Software-updates  
            - **Alle software-updates**  
            - **Software-update groepen**
        - Windows 10-onderhoud, **alle Windows 10-updates**  
        - Office 365-client beheer, **office 365-updates**  

    - **Taken reeks**: Ga naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer **taken reeksen**.

2. Selecteer de software met de gefaseerde implementatie.  

3. Ga in het detail venster naar het tabblad **gefaseerde implementaties** .  

4. Selecteer de gefaseerde implementatie en klik op **verplaatsen naar volgende fase** in het lint.  

    ![Snelmenu met acties voor een gefaseerde implementatie](media/Suspend-phased-deployment.PNG)

Gebruik vanaf versie 2002 de volgende Windows Power shell-cmdlet voor deze taak: [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext).

## <a name="suspend-and-resume-phases"></a><a name="bkmk_suspend"></a> Fasen onderbreken en hervatten

U kunt een gefaseerde implementatie hand matig onderbreken of hervatten. U kunt bijvoorbeeld een gefaseerde implementatie voor een taken reeks maken. Tijdens het bewaken van de fase voor uw test groep ziet u een groot aantal fouten. U onderbreekt de gefaseerde implementatie om te voor komen dat verdere apparaten de taken reeks uitvoeren. Nadat u het probleem hebt opgelost, kunt u de gefaseerde implementatie hervatten om de implementatie voort te zetten.

1. Hoe u deze actie start, is afhankelijk van het type geïmplementeerde software:  

    - **Toepassing**: Ga naar de werk ruimte **software bibliotheek** , vouw **toepassings beheer**uit en selecteer **toepassingen**.

    - **Software-update**: Ga naar de werk ruimte **software bibliotheek** en selecteer een van de volgende knoop punten:
        - Software-updates  
            - **Alle software-updates**  
            - **Software-update groepen**
        - Windows 10-onderhoud, **alle Windows 10-updates**  
        - Office 365-client beheer, **office 365-updates**  

    - **Taken reeks**: Ga naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer **taken reeksen**. Selecteer een bestaande taken reeks en klik vervolgens in het lint op **gefaseerde implementatie maken** .  

2. Selecteer de software met de gefaseerde implementatie.  

3. Ga in het detail venster naar het tabblad **gefaseerde implementaties** .  

4. Selecteer de gefaseerde implementatie en klik op **onderbreken** of **hervatten** in het lint.

> [!NOTE]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds de oude naam in het Configuration Manager product en de documentatie terwijl de-console wordt bijgewerkt.

Vanaf versie 2002 gebruikt u de volgende Windows Power shell-cmdlets voor deze taak:

- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)

## <a name="monitor"></a><a name="bkmk_monitor"></a> Monitoren
<!--1358577-->

Gefaseerde implementaties hebben hun eigen specifieke bewakings knooppunt, waardoor het gemakkelijker wordt om gefaseerde implementaties te identificeren die u hebt gemaakt en naar de bewakings weergave met gefaseerde implementatie te navigeren. Selecteer in de werk ruimte **bewaking** de optie **gefaseerde implementaties**en dubbel klik vervolgens op een van de gefaseerde implementaties om de status weer te geven. <!--3555949-->

![Dash board voor de fase van de implementatie status met de status van twee fasen](media/1358577-phased-deployment-status.png)

Dit dash board bevat de volgende informatie voor elke fase in de implementatie:  

- **Totaal aantal apparaten** of **Totaal aantal resources**: hoeveel apparaten zijn gericht op deze fase.  

- **Status**: de huidige status van deze fase. Elke fase kan een van de volgende statussen hebben:  

  - **Implementatie gemaakt**: de gefaseerde implementatie heeft een implementatie van de software voor deze fase gemaakt. Clients zijn actief gericht op deze software.  

  - **Wachten**: de vorige fase heeft nog niet de criteria voor het slagen van de implementatie bereikt om door te gaan naar deze fase.  

  - **Onderbroken**: een beheerder heeft de implementatie onderbroken.  

- **Voortgang**: de implementatie statussen met kleur code van clients. Bijvoorbeeld: geslaagd, in voortgang, fout, niet voldaan aan vereisten en onbekend.

### <a name="success-criteria-tile"></a>Tegel criteria voor succes

Gebruik de vervolg keuzelijst **fase selecteren** om de weer gave van de tegel **criteria voor succes** te wijzigen. In deze tegel wordt het **doel** van de fase vergeleken met de huidige compatibiliteit van de implementatie. Met de standaard instellingen is het Phase-doel 95%. Deze waarde betekent dat de implementatie een naleving van 95% nodig heeft om over te stappen op de volgende fase.

In het voor beeld is het doel van de fase 65% en de huidige naleving is 66,7%. De gefaseerde implementatie wordt automatisch verplaatst naar de tweede fase, omdat de eerste fase voldeed aan de criteria voor geslaagde pogingen.  

   ![Voor beeld van een tegel met succes criteria vanuit de Faseve implementatie status waarbij het doel 65% is](media/pod-status-success-criteria-tile.png)

Het doel van de fase is hetzelfde als het **voltooiings percentage** van de implementatie van de fase-instellingen voor de *volgende* fase. Voor de gefaseerde implementatie om de volgende fase te starten, definieert die tweede fase de criteria voor het slagen van de eerste fase. Als u deze instelling wilt weer geven:

1. Ga naar het gefaseerde implementatie object op de software en open de gefaseerde implementatie-eigenschappen.  

2. Ga naar het tabblad **fasen** . Selecteer **fase 2** en klik op **weer geven**.  

3. Ga in de fase venster Eigenschappen naar het tabblad **fase-instellingen** .  

4. Bekijk de waarde voor het **percentage geslaagde implementaties** in de *criteria voor het slagen van de vorige fase* groep.  

De volgende eigenschappen zijn bijvoorbeeld voor dezelfde fase als de tegel criteria die hierboven wordt weer gegeven, waarbij de criteria 65% zijn:  

![Tabblad fase-instellingen op de fase-eigenschappen](media/phase-properties-phase-settings.png)

## <a name="powershell"></a>PowerShell

Gebruik de volgende Windows Power shell-cmdlets voor het beheren van gefaseerde implementaties:

### <a name="automatically-create-phased-deployments"></a>Automatisch gefaseerde implementaties maken

- [New-CMApplicationAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmapplicationautophaseddeployment)
- [New-CMSoftwareUpdateAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdateautophaseddeployment)
- [New-CMTaskSequenceAutoPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequenceautophaseddeployment)

### <a name="manually-create-phased-deployments"></a>Hand matig gefaseerde implementaties maken

- [New-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/new-cmsoftwareupdatephase)
- [New-CMSoftwareUpdateManualPhasedDeployment](/powershell/module/configurationmanager/new-cmsoftwareupdatemanualphaseddeployment)
- [New-CMTaskSequencePhase](/powershell/module/configurationmanager/new-cmtasksequencephase)
- [New-CMTaskSequenceManualPhasedDeployment](/powershell/module/configurationmanager/new-cmtasksequencemanualphaseddeployment)

### <a name="get-existing-phased-deployment-objects"></a>Bestaande gefaseerde implementatie objecten ophalen

- [Get-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/get-cmapplicationphaseddeployment)
- [Get-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/get-cmsoftwareupdatephaseddeployment)
- [Get-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/get-cmtasksequencephaseddeployment)
- [Get-CMPhase](/powershell/module/configurationmanager/get-cmphase)

### <a name="monitor-phased-deployment-status"></a>Status van gefaseerde implementatie bewaken

- [Get-CMPhasedDeploymentStatus](/powershell/module/configurationmanager/get-cmphaseddeploymentstatus)

### <a name="manage-existing-phased-deployments"></a>Bestaande gefaseerde implementaties beheren

- [Move-CMPhasedDeploymentToNext](/powershell/module/configurationmanager/move-cmphaseddeploymenttonext)
- [Resume-CMPhasedDeployment](/powershell/module/configurationmanager/resume-cmphaseddeployment)
- [Suspend-CMPhasedDeployment](/powershell/module/configurationmanager/suspend-cmphaseddeployment)

### <a name="modify-existing-phased-deployments"></a>Bestaande gefaseerde implementaties wijzigen

- [Set-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/set-cmapplicationphaseddeployment)
- [Set-CMSoftwareUpdatePhase](/powershell/module/configurationmanager/set-cmsoftwareupdatephase)
- [Set-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/set-cmsoftwareupdatephaseddeployment)
- [Set-CMTaskSequencePhase](/powershell/module/configurationmanager/set-cmtasksequencephase)
- [Set-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/set-cmtasksequencephaseddeployment)
- [Remove-CMApplicationPhasedDeployment](/powershell/module/configurationmanager/remove-cmapplicationphaseddeployment)
- [Remove-CMSoftwareUpdatePhasedDeployment](/powershell/module/configurationmanager/remove-cmsoftwareupdatephaseddeployment)
- [Remove-CMTaskSequencePhasedDeployment](/powershell/module/configurationmanager/remove-cmtasksequencephaseddeployment)
