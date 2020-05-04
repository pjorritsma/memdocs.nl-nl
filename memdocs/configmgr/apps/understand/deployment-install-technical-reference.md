---
title: Technische Naslag informatie over de installatie van de toepassing
titleSuffix: Configuration Manager
description: Problemen met toepassings installaties oplossen technische Naslag informatie voor Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c96e9ad4f0608084d87bed3973221730cb2d5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709780"
---
# <a name="application-installation"></a>Installatie van toepassing

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u doorgaat, moet u de [client onderdelen voor toepassings implementatie](client-components-technical-reference.md) bekijken om de taak verwerking van DCM en CI-agent te begrijpen.

De installatie van de toepassing wordt uitgevoerd door DCM-agent-en CI-agent onderdelen wanneer de implementatie wordt afgedwongen. De afdwingings tijd verschilt voor beschik bare en vereiste implementaties. Als u wilt weten wanneer de toewijzing wordt afgedwongen, raadpleegt u de artikelen [toepassings implementatie naar apparaat verzamelingen](device-deployment-technical-reference.md) of [toepassings implementatie naar gebruikers verzamelingen](user-deployment-technical-reference.md) .

## <a name="enforcement-initiation"></a>Initiatie van afdwinging

De installatie van de toepassing wordt gestart door het CI-agent onderdeel op de client tijdens de **StateEnforcingCIs** -fase. Dit proces is hetzelfde, ongeacht of de toepassing wordt geïmplementeerd in een apparaat-of gebruikers verzameling.

- Voor **beschik bare** implementaties wordt de toepassing geïnstalleerd wanneer de gebruiker de installatie van de toepassing start vanuit software Center.
- Voor **vereiste** implementaties wordt de toepassing tijdens de implementatie deadline geïnstalleerd. De gebruiker kan de installatie echter vóór de deadline initiëren vanuit software Center.

Wanneer CI agent de installatie van de toepassing initieert, wordt er een taak gemaakt die wordt verwerkt door het onderdeel CI taak beheer. CI Task Manager initieert vervolgens de installatie. Deze activiteit kan worden gevolgd in het **CITaskMgr. log** met de unieke implementatie type-id.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Toepassing afdwingen

Nadat het afdwingen van de toepassing is gestart, voert de client de detectie van de toepassing opnieuw uit om ervoor te zorgen dat de toepassing nog niet is geïnstalleerd. Als is vastgesteld dat de toepassing niet is geïnstalleerd, wordt de installatie van de toepassing gestart. Deze activiteit kan worden gevolgd in de **AppEnforce. log** op de client met de unieke implementatie type-id.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Installatie verificatie

Nadat de toepassing is geïnstalleerd, wordt de detectie methode van de toepassing opnieuw gebruikt om ervoor te zorgen dat de toepassing is gedetecteerd als geïnstalleerd.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Ten slotte ontvangt de CI-agent na voltooiing van de afdwinging de melding voltooid taak en wordt de CI agent-taak verplaatst naar de volgende fase.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Volgende stappen

[Problemen met toepassings implementaties oplossen](../deploy-use/troubleshoot-application-deployment.md)
