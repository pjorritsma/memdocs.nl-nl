---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: e6023808f60d0ac7753745d5882516dda0f85be2
ms.sourcegitcommit: af4fc4f928203c1bfdb27499a56c91fe0ebae854
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/18/2020
ms.locfileid: "90802932"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-the-configuration-manager-site-is-configured-to-require-multi-factor-authentication-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Wanneer de Configuration Manager-site is geconfigureerd om multi-factor Authentication te vereisen, werken de meeste functies voor Tenant koppeling niet
<!--7986450, 7988266-->
**Scenario:** Als de [SMS-provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) computer die communiceert met het [service aansluitpunt](../../core/servers/deploy/configure/about-the-service-connection-point.md) is geconfigureerd voor het gebruik van multi-factor Authentication, kunt u geen toepassingen installeren, CMPivot query's uitvoeren en andere acties uitvoeren vanuit de beheer console. U ontvangt fout code 403, verboden.  

**Tijdelijke oplossing:** De huidige tijdelijke oplossing is het configureren van de on-premises hiërarchie naar het standaard verificatie niveau van **Windows-verificatie**. Zie de [sectie verificatie in het artikel](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)over de SMS-provider voor meer informatie.

