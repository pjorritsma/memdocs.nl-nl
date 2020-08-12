---
title: Een takenreeks maken voor niet-besturingssysteemimplementaties
titleSuffix: Configuration Manager
description: Taken reeksen maken die geen besturings systeem implementeren, zoals het distribueren van software of het automatiseren van taken
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fcae4d520b1e81d0ef3470cd12ee68488b4f589
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125523"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Een takenreeks maken voor niet-besturingssysteemimplementaties

*Van toepassing op: Configuration Manager (huidige vertakking)*

Taken reeksen in Configuration Manager worden gebruikt voor het automatiseren van verschillende soorten taken in uw omgeving. Deze taken zijn voornamelijk ontworpen en getest voor het implementeren van besturingssystemen. Configuration Manager heeft vele andere functies die de primaire technologie moeten zijn die u gebruikt voor de volgende scenario's:

- [Toepassing installeren](../../apps/understand/introduction-to-application-management.md)

    > [!NOTE]
    > Vanaf versie 2002 kunt u complexe toepassingen installeren met behulp van taken reeksen via het toepassings model. Voeg een implementatie type toe aan een app die een taken reeks is, ofwel om de app te installeren of te verwijderen. Zie [Windows-toepassingen maken](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)voor meer informatie.<!-- 3555953 -->

- [Installatie van software-updates](../../sum/understand/software-updates-introduction.md)

- [Configuratie instellen](../../compliance/understand/ensure-device-compliance.md)

Denk ook aan andere micro soft System Center-automatiserings technologieën, zoals [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) en [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

De kracht van taken reeksen ligt in hun flexibiliteit en hoe u ze gebruikt. Ze kunnen client instellingen configureren, software distribueren, stuur Programma's bijwerken, gebruikers statussen bewerken en andere taken uitvoeren, onafhankelijk van de implementatie van het besturings systeem. U kunt een aangepaste takenreeks maken om elk gewenst aantal taken toe te voegen. Het gebruik van aangepaste taken reeksen voor niet-besturingssysteem implementatie wordt ondersteund in Configuration Manager. Als een taken reeks echter resulteert in ongewenste of inconsistente resultaten, kijkt u naar manieren om de bewerking te vereenvoudigen:

- Eenvoudigere stappen gebruiken
- De acties verdelen over meerdere taken reeksen
- Maak een gefaseerde benadering van het maken en testen van de taken reeks

## <a name="supported-steps"></a>Ondersteunde stappen

De volgende stappen worden ondersteund voor gebruik in een aangepaste taken reeks die geen besturings systeem is voor implementatie:  

- [Gereedheid controleren](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

- [Verbinding maken met netwerkmap](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

- [Pakketinhoud downloaden](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

- [Toepassing installeren](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

- [Pakket installeren](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

- [Software-updates installeren](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

- [Computer opnieuw opstarten](../understand/task-sequence-steps.md#BKMK_RestartComputer)  

- [Opdrachtregel uitvoeren](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

- [PowerShell-script uitvoeren](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

- [Taken reeks uitvoeren](../understand/task-sequence-steps.md#child-task-sequence)  

- [Dynamische variabelen instellen](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

- [Takenreeksvariabele instellen](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Volgende stappen

[Een aangepaste takenreeks maken](create-a-custom-task-sequence.md)