---
title: Technische Naslag informatie voor de evaluatie van de toepassing
titleSuffix: Configuration Manager
description: Probleem oplossing voor technische Naslag informatie over toepassings evaluatie voor Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdeec54489adfc0d2a5cceb99c7e7587ce1a41ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709794"
---
# <a name="application-deployment-evaluation"></a>Evaluatie van toepassings implementatie

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u doorgaat, moet u de [client onderdelen voor toepassings implementatie](client-components-technical-reference.md) bekijken om de taak verwerking van DCM en CI-agent te begrijpen.

De evaluatie van de toepassing wordt uitgevoerd door de DCM-agent en CI-agent onderdelen wanneer de implementatie wordt geactiveerd. Als u wilt weten wanneer de toewijzing is geactiveerd, raadpleegt u de artikelen [toepassings implementatie naar apparaten verzamelingen](device-deployment-technical-reference.md) of [toepassing implementeren naar gebruikers verzamelingen](user-deployment-technical-reference.md) .

## <a name="application-detection-and-evaluation"></a>Detectie en evaluatie van toepassingen

De evaluatie van de toepassing wordt uitgevoerd tijdens de **InvokingSdmMethod** -fase van een CI-agent taak. In deze fase evalueert de client de detectie methode die is gedefinieerd voor de toepassing om te bepalen of de toepassing op het apparaat is geïnstalleerd. Deze activiteit kan worden gevolgd in **AppDiscovery. log** met de unieke implementatie type-id of implementatie type naam.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> Hierboven vindt u een voor beeld van detectie voor een MSI-toepassing waarbij de detectie wordt uitgevoerd door te controleren of de MSI-product code op het apparaat is geïnstalleerd. Voor toepassingen die gebruikmaken van alternatieve detectie methoden, wordt de juiste detectie methode gebruikt om te controleren of de toepassing is geïnstalleerd.

Vervolgens evalueert de client de gewenste status van de toepassing op basis van het implementatie doel. Deze stap omvat ook het detecteren van de vraag of de toepassing afhankelijkheden of vervangings regels heeft die moeten worden uitgevoerd voor de toepassing. Deze activiteit kan worden gevolgd in **AppIntentEval. log** met de unieke id voor de toepassing en het implementatie type.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

In de bovenstaande logboek vermelding geeft de **huidige status** aan of de toepassing momenteel op het apparaat is geïnstalleerd. **Toepas baarheid** geeft aan of de toepassing van toepassing is op basis van gedefinieerde regels voor vereisten. **ResolvedState** geeft de gewenste status van de toepassing aan op basis van het implementatie doel.

> [!TIP]
> Gebruik het [hulp programma voor implementatie bewaking](../../core/support/deployment-monitoring-tool.md) om de toepassings status, de status van de toepasselijkheid en de schendingen van vereisten weer te geven.

## <a name="next-steps"></a>Volgende stappen

- [Toepassing downloaden](deployment-download-technical-reference.md)
