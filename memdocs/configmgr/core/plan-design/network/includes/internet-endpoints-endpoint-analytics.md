---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126450"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Vereiste eind punten voor door Configuration Manager beheerde apparaten

Configuration Manager-beheerde apparaten verzenden gegevens naar intune via de connector van de Configuration Manager-rol en ze hebben geen directe toegang nodig tot de open bare cloud van micro soft.

| Eindpunt  | Functie  |
|-----------|-----------|
| `https://graph.windows.net` | Wordt gebruikt om automatisch instellingen op te halen wanneer u uw hiërarchie koppelt aan endpoint Analytics op Configuration Manager serverrol. Zie [Configure the proxy for a site System server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)(Engelstalig) voor meer informatie. |
| `https://*.manage.microsoft.com` | Wordt gebruikt voor het synchroniseren van apparaten verzameling en apparaten met endpoint Analytics op Configuration Manager server functie. Zie [Configure the proxy for a site System server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)(Engelstalig) voor meer informatie. |

### <a name="endpoints-required-for-intune-managed-devices"></a>Vereiste eind punten voor door intune beheerde apparaten

Als u apparaten wilt registreren bij Endpoint Analytics, moeten ze de vereiste functionele gegevens verzenden naar de open bare cloud van micro soft. Endpoint Analytics maakt gebruik van de met Windows 10 en Windows Server verbonden gebruikers ervaringen en telemetrie-onderdelen (DiagTrack) voor het verzamelen van de gegevens van door intune beheerde apparaten. Zorg ervoor dat de **verbonden gebruikers ervaring en telemetrie** -service op het apparaat wordt uitgevoerd.

| Eindpunt  | Functie  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Wordt gebruikt door door intune beheerde apparaten om [vereiste functionele gegevens](../../../../../analytics/data-collection.md#bkmk_datacollection) te verzenden naar het eind punt van de intune-gegevens verzameling. |
