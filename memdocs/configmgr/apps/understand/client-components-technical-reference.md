---
title: Technische documentatie voor client onderdelen voor toepassings implementatie
titleSuffix: Configuration Manager
description: Client onderdelen die worden gebruikt voor het oplossen van problemen met de implementatie van toepassingen in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35b54bd5868197d607a15ab1d4759d03968b9892
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709801"
---
# <a name="understanding-application-deployment-client-components"></a>Informatie over client onderdelen voor toepassings implementatie

*Van toepassing op: Configuration Manager (huidige vertakking)*

Evaluatie-en afdwingings bewerkingen voor toepassings implementatie worden verwerkt door de DCM-agent en CI-agent onderdelen op de client. In dit artikel wordt uitgelegd hoe een typische DCM-en CI-agent taak werkt.

## <a name="dcm-agent"></a>DCM-agent

DCM-agent is het client onderdeel op hoog niveau dat verantwoordelijk is voor de evaluatie van configuratie-items, waaronder toepassingen. Wanneer een implementatie wordt geactiveerd of afgedwongen, wordt een DCM-agent taak gemaakt die het toewijzings beleid leest en de acties bepaalt die moeten worden uitgevoerd. Deze activiteit kan worden gevolgd in de **DCMAgent. log** op de client met de taak-id van de DCM-agent, die kan worden geïdentificeerd door te zoeken naar de unieke id van de toepassing.

### <a name="device-deployments"></a>Implementaties van apparaten

- Voor **vereiste** implementaties worden in DCMAgent. log de toepasselijke acties weer gegeven. Deze acties kunnen verschillen, afhankelijk van of de implementatie deadline al is verstreken.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Voor **beschik bare** implementaties wordt in DCMAgent. log aangegeven `is not mandatory`dat de implementatie. Voor deze implementaties wordt de evaluatie van de toepassing uitgevoerd, maar afdwinging wordt overgeslagen, tenzij de gebruiker de installatie heeft gestart.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Gebruikers implementaties

- Voor **vereiste** implementaties worden in DCMAgent. log de toepasselijke acties weer gegeven. Deze acties kunnen verschillen, afhankelijk van of de implementatie deadline al is verstreken.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Voor **beschik bare** implementaties worden DCM-Agent taken voor evaluatie en afdwinging gemaakt wanneer de installatie van de toepassing door de gebruiker wordt gestart.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>CI-agent

CI-agent is het client onderdeel dat verantwoordelijk is voor de evaluatie en het herstel van configuratie-items. DCM-agent leest het toewijzings beleid en maakt een taak voor het onderdeel CI agent om de gevraagde acties uit te voeren. In **DCMAgent. log** wordt de CI-agent taak-id vastgelegd. Dit is handig voor het bijhouden van de activiteit van de CI-agent in de **CIAgent. log** op de client.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Een typische CI-agent taak doorloopt meerdere fasen, die kunnen worden geïdentificeerd door **CIAgent. log** te filteren op de CI agent-taak-id `TransitionState`en vervolgens naar te zoeken. Enkele belang rijke fasen voor een CI-agent taak voor een implementatie van een toepassing zijn:

- **DownloadingCIs**
  - Tijdens deze fase worden de toepassings-meta gegevens die zijn vereist om te evalueren van de toepassing gedownload. De meta gegevens bevatten de detectie methode, regels voor vereisten, globale voor waarden enzovoort. Deze activiteit kan worden gevolgd in **CIDownloader. log** en **bestand datatransferservice. log**. Voor **beschik bare** implementaties vindt dit proces plaats tijdens de eerste evaluatie van de toepassing. Voor **vereiste** implementaties wordt dit proces echter onmiddellijk uitgevoerd nadat het beleid is gedownload.

- **InvokingSdmMethod**
  - Tijdens deze fase wordt de detectie methode van de toepassing gebruikt om te controleren of de toepassing is geïnstalleerd en of de gewenste status wordt bepaald. Deze activiteit kan worden gevolgd in **AppDiscovery. log** en **AppIntentEval. log**. Zie voor meer informatie over deze fase [toepassings evaluatie](deployment-evaluation-technical-reference.md).

- **StateDownloadingContents**
  - Tijdens deze fase wordt de inhoud van de toepassing gedownload, indien nodig. Deze activiteit kan worden gevolgd in **CAS. log**, **ContentTransferManager. log**, **bestand locationservices. log**en **bestand datatransferservice. log**. Zie [toepassingen downloaden](deployment-download-technical-reference.md)voor meer informatie over deze fase.

- **StateEnforcingCIs**
  - Tijdens deze fase wordt de installatie van de toepassing gestart. Deze activiteit kan worden gevolgd in **AppEnforce. log**. Zie voor meer informatie over deze fase installatie van de [toepassing](deployment-install-technical-reference.md).

- **StateEnforcementReporting**
  - Tijdens deze fase wordt de installatie status van de toepassing vastgelegd voor rapportage aan het beheer punt. Deze activiteit kan worden gevolgd in **StateMessage. log**.

Hoewel de CI agent-taak alle fasen doorloopt, slaat deze de fase over als deze niet vereist is. Voor beelden van de **beschik bare** implementaties StateDownloadingContents en StateEnforcingCIs worden overgeslagen totdat de gebruiker de toepassing probeert te installeren vanuit software Center. Voor **vereiste** implementaties downloadt de StateDownloadingContents-fase echter de inhoud van de toepassing (indien nodig) wanneer de toewijzing wordt geactiveerd, maar de StateEnforcingCIs-fase wordt overgeslagen als de deadline in de toekomst ligt. Dit gedrag kan worden waargenomen in de CIAgent. log door te filteren op de CI-agent taak-ID `Skipping policy`en op zoek naar.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Volgende stappen

- [Toepassings evaluatie](deployment-evaluation-technical-reference.md)
- [Toepassing downloaden](deployment-download-technical-reference.md)
- [Installatie van toepassing](deployment-install-technical-reference.md)
