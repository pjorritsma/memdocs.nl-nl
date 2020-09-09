---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: 8d456185e39df8d76b949baf26de755970a9a89b
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89563995"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-multi-factor-authentication-is-enabled-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Als multi-factor Authentication is ingeschakeld, werken de meeste functies voor Tenant koppeling niet
<!--7986450, 7988266-->
**Scenario:** Als de [SMS-provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) computer die communiceert met het [service aansluitpunt](../../core/servers/deploy/configure/about-the-service-connection-point.md) is geconfigureerd voor het gebruik van multi-factor Authentication, kunt u geen toepassingen installeren, CMPivot query's uitvoeren en andere acties uitvoeren vanuit de beheer console. U ontvangt fout code 403, verboden.  

**Tijdelijke oplossing:** De huidige tijdelijke oplossing is het configureren van de hiërarchie naar het standaard verificatie niveau van **Windows-verificatie**. Zie de [sectie verificatie in het artikel](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)over de SMS-provider voor meer informatie.

