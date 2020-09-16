---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 27436e7cd782ca910049007d52f37e2d7945f01e
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606848"
---
- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742-->

- `https://dc.services.visualstudio.com` <!--7541816-->

Het service verbindings punt maakt een lange permanente uitgaande verbinding met de meldings service die wordt gehost op `https://*.manage.microsoft.com` . Controleer of de proxy die wordt gebruikt voor het service aansluitpunt niet langer uitgaande verbindingen te snel verloopt. We raden 3 minuten aan voor uitgaande verbindingen met dit Internet-eind punt. <!--7820969-->