---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 08/14/2020
ms.openlocfilehash: 13a5b771f712420939f87073854faab3c38270c9
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252472"
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="when-the-sms-provider-is-remote-from-the-cas-you-may-encounter-an-internal-server-error-from-the-admin-console"></a><a name="bkmk_dblhop"></a> Wanneer de SMS-provider extern van de certificerings instantie is, kan er een interne server fout optreden in de beheer console

**Fout bericht:** On-premises fout code: 500 interne server fout

**Scenario 1:** Bij het uitvoeren van Configuration Manager versie 2002 en er een externe provider voor de certificerings instantie is, kan er een interne server fout optreden in de beheer console.

**Scenario 2:** Als Configuration Manager versie 2006 wordt uitgevoerd, kan deze fout ook optreden als het service verbindings punt geen verbinding kan maken met de provider op de primaire site en terugvalt op de provider voor de CAS. 

**Scenario 3:** Als de CAS is bijgewerkt naar versie 2006, maar de primaire server nog niet is bijgewerkt, worden de aanvragen doorgestuurd via de CAS-provider. Als de provider extern is, kan er een interne server fout optreden in de beheer console. 

**Tijdelijke oplossing:** Volg de instructies voor de [CAS bevat een scenario voor een externe provider](../../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) in het CMPivot-artikel om dit "dubbele hop"-scenario te omzeilen.

### <a name="when-multi-factor-authentication-is-enabled-most-tenant-attach-features-dont-work"></a><a name="bkmk_mfa"></a> Als multi-factor Authentication is ingeschakeld, werken de meeste functies voor Tenant koppeling niet
<!--7986450, 7988266-->
**Scenario:** Als de [SMS-provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) computer die communiceert met het [service aansluitpunt](../../core/servers/deploy/configure/about-the-service-connection-point.md) is geconfigureerd voor het gebruik van multi-factor Authentication, kunt u geen toepassingen installeren, CMPivot query's uitvoeren en andere acties uitvoeren vanuit de beheer console. U ontvangt fout code 403, verboden.  

**Tijdelijke oplossing:** De huidige tijdelijke oplossing is het configureren van de hiërarchie naar het standaard verificatie niveau van **Windows-verificatie**. Zie de [sectie verificatie in het artikel](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)over de SMS-provider voor meer informatie.

