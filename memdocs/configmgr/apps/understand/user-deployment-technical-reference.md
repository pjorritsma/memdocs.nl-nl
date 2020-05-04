---
title: Technische Naslag informatie over app-implementatie naar gebruikers
titleSuffix: Configuration Manager
description: Probleem oplossing voor toepassings implementaties naar technische Naslag informatie voor gebruikers over Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: b8e9dbfe-a046-4e06-8dec-cf0bc41ba095
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b44aad1db96b4191b9c9537acea4e64b1d30fde6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710795"
---
# <a name="application-deployment-policy-for-users"></a>Toepassings implementatie beleid voor gebruikers

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer een toepassing wordt geïmplementeerd naar een gebruikers verzameling, wordt het beleid voor de implementatie alleen voor vereiste implementaties gemaakt. Voor beschik bare implementaties wordt het beleid gemaakt wanneer de gebruiker probeert de toepassing te installeren vanuit het Software Center. In dit artikel wordt het implementatie proces voor vereist en de beschik bare implementaties uitgelegd.

> [!TIP]
> Alle informatie die nodig is om de client logboeken te controleren, kan worden verkregen door de SQL-query uit te voeren waarnaar wordt verwezen in de sectie [voordat u begint](app-deployment-technical-reference.md#before-you-begin) .

## <a name="required-deployments"></a>Vereiste implementaties

Het beleid voor een vereiste toepassings implementatie voor een gebruikers verzameling is gericht op alle gebruikers in de verzameling wanneer de implementatie wordt gemaakt. Verwerking aan de client zijde voor deze implementaties is vergelijkbaar met een vereiste implementatie voor een verzameling apparaten. De activering van de implementatie vindt plaats op de gedefinieerde beschik bare tijd en het afdwingen vindt plaats op de opgegeven deadline tijd. Zie [toepassings implementaties naar Apparaatsets](device-deployment-technical-reference.md)voor meer informatie.

## <a name="available-deployments"></a>Beschik bare implementaties

Toepassingen die zijn geïmplementeerd voor een gebruikers verzameling, werken anders. Met deze gedrags wijziging kan de beheerder toepassingen beschikbaar stellen aan de gebruikers zonder dat bron conflicten voor het beleid worden veroorzaakt. Wanneer een gebruiker het Software Center start, wordt een lijst met toepassingen die beschikbaar zijn voor de gebruiker, in real-time opgevraagd van het beheer punt. Deze aanvraag wordt verzonden naar de `CMUserService_WindowsAuth` virtuele map op het beheer punt en kan worden weer gegeven in de **SCClient_ [username]. log** op de client.

```text
Using endpoint Url: https://MP.CONTOSO.COM:443/CMUserService_WindowsAuth, Windows authentication
```

Wanneer het beheer punt deze aanvraag ontvangt, wordt een query uitgevoerd op de lijst met toepassingen die beschikbaar zijn voor `usp_GetApplicationPropertyValuesFiltered` de gebruiker door de opgeslagen procedure uit te voeren. Deze activiteit kan worden gevolgd in het **UserService. log** op het beheer punt.

```text
GetFilteredApplications, startItem = 0, max rows = 60, search text = '', filter = '', user = CONTOSO\UserName, api = 4.0, source = UserService_WinAuth_SoftwareCenter, platform = <OSPlatform>
GetFilteredApplications: returned 1 rows out of 1 total
```

Software Center ontvangt de lijst en geeft de toepassingen weer die de gebruiker kan installeren. Wanneer de gebruiker op de toepassing klikt, wordt aanvullende informatie over de toepassing opgevraagd bij het beheer punt. Dit omvat het uitvoeren van opgeslagen procedures, zoals usp_GetApplicationInfo, usp_GetAppModelApplicationSupersedence, usp_GetDeploymentTypeForAnApp, enzovoort.

De implementatie wordt geactiveerd wanneer de gebruiker de toepassing selecteert en klikt op de knop **installeren** . er wordt een DCM agent-taak gemaakt om de toepassing te evalueren. Als de toepassing van toepassing is, wordt er een andere taak van een DCM-agent gemaakt om de toepassing te downloaden en af te dwingen. Deze activiteit kan worden gevolgd in de **DCMAgent. log** op de client.

## <a name="next-steps"></a>Volgende stappen

- [Informatie over client onderdelen voor toepassings implementatie](client-components-technical-reference.md)
