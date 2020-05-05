---
title: Inrichtingsmodus
titleSuffix: Configuration Manager
description: Meer informatie over de inrichtings modus van de client tijdens de taken reeks Configuration Manager.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 815b32ecf7e9cd315c2365cb5ed73004b2a48718
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723948"
---
# <a name="provisioning-mode"></a>Inrichtingsmodus

*Van toepassing op: Configuration Manager (huidige vertakking)*

Tijdens een taken reeks voor implementatie van een besturings systeem Configuration Manager de client in de inrichtings modus plaatsen. (Een taken reeks voor de implementatie van een besturings systeem bevat in-place upgrade voor Windows 10.) In deze status verwerkt de client het beleid niet van de site. Dit gedrag zorgt ervoor dat de taken reeks zonder risico van extra implementaties wordt uitgevoerd op de client. Wanneer de taken reeks is voltooid, een geslaagde of verwerkte fout is, wordt de client inrichtings modus afgesloten.

Als de taken reeks onverwacht mislukt, kan de client in de inrichtings modus blijven. Als het apparaat bijvoorbeeld wordt opgestart in het midden van de taken reeks verwerking, en dit niet kan worden hersteld. Een beheerder moet clients in deze status hand matig identificeren en oplossen.


## <a name="manually-remove-provisioning-mode"></a>Inrichtings modus hand matig verwijderen

Als een client in de inrichtings modus blijft, moet u dit hand matig proces gebruiken om de client te herstellen naar een normale werking.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Een van de wijzigingen die door deze WMI-methode zijn aangebracht, is het instellen van een register waarde, maar er zijn ook andere wijzigingen aangebracht. Als u alleen de register waarde wijzigt, wordt de client niet volledig uit de inrichtings modus halen. Als u het REGI ster hand matig bewerkt, kan de client onverwacht gedrag vertonen.  


## <a name="client-provisioning-mode-timeout"></a>Time-out voor client inrichtings modus

Vanaf versie 1902 stelt de taken reeks een tijds tempel in wanneer de client in de inrichtings modus wordt gezet. Elke 60 minuten controleert een client in de inrichtings modus de duur van de tijd sinds de tijds tempel. Als de inrichtings modus langer is dan 48 uur, wordt de inrichtings modus door de client automatisch afgesloten en wordt het proces opnieuw gestart.

48 uur is de standaard time-outwaarde voor de inrichtings modus. U kunt deze timer aanpassen op een apparaat door de waarde **ProvisioningMaxMinutes** in de volgende register sleutel in te `HKLM\Software\Microsoft\CCM\CcmExec`stellen:. Als deze waarde niet bestaat of is `0`, gebruikt de client de standaard 48 uur.

De tijds tempel **ProvisioningEnabledTime** bevindt zich in de volgende `HKLM\Software\Microsoft\CCM\CcmExec`register sleutel:. De time stamp heeft een waarde van de laatste keer dat de computer de inrichtings modus heeft opgegeven. De indeling is epoche (UNIX-tijds tempel) en is in UTC.

Deze tijds tempel wordt ook opnieuw ingesteld op de huidige tijd wanneer u de computer hand matig in de inrichtings modus plaatst met behulp van de volgende opdracht:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>Proces stroomdiagrammen

In deze diagrammen wordt de proces stroom voor de taken reeks en de client weer gegeven.

### <a name="task-sequence"></a>Takenreeks

In het volgende diagram ziet u hoe de inrichtings modus in de taken reeks wordt ingesteld:

![Stroom diagram van inrichtings modus voor het instellen van taken reeksen](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Client herstel

In het volgende diagram ziet u hoe de client de inrichtings modus verlaat:

![Stroom diagram van de client voor het afsluiten van de inrichtings modus](media/3197824-client-flow.png)


## <a name="see-also"></a>Zie ook

[Windows en ConfigMgr installeren](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[Besturingssysteem bijwerken](task-sequence-steps.md#BKMK_UpgradeOS)
