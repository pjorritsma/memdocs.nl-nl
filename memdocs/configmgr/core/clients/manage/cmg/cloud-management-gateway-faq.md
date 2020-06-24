---
title: VEELGESTELDE VRAGEN CMG
titleSuffix: Configuration Manager
description: In dit artikel vindt u antwoorden op veelgestelde vragen over de Cloud beheer gateway
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: bd846b0155a0baddad76d6027ffbd239d7dbf26f
ms.sourcegitcommit: 5f15a3abf33ce7bfd6855ffeef2ec3cd4cd48a7f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721887"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Veelgestelde vragen over de Cloud beheer gateway

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u antwoorden op uw veelgestelde vragen over de Cloud beheer gateway. Zie voor meer informatie [plannen voor Cloud beheer gateway](plan-cloud-management-gateway.md).

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="what-certificates-do-i-need"></a>Welke certificaten heb ik nodig?

Zie [certificaten voor Cloud beheer gateway](certificates-for-cloud-management-gateway.md)voor meer gedetailleerde informatie.

### <a name="do-i-need-azure-expressroute"></a>Heb ik Azure ExpressRoute nodig?

Nee. Met [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) kunt u uw on-premises netwerk uitbreiden naar de micro soft-Cloud. ExpressRoute of andere dergelijke virtuele netwerk verbindingen zijn niet vereist voor de Configuration Manager Cloud beheer gateway. Het ontwerp van de Cloud beheer gateway maakt het op internet gebaseerde clients mogelijk om via de Azure-service te communiceren met on-premises site systemen zonder extra netwerk configuratie. Zie voor meer informatie [plannen voor Cloud beheer gateway](plan-cloud-management-gateway.md)

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Moet ik de virtuele machines van Azure onderhouden?

Er is geen onderhoud vereist. Het ontwerp van de Cloud beheer gateway maakt gebruik van Azure Platform as a Service (PaaS). Met het abonnement dat u opgeeft, maakt Configuration Manager de benodigde virtuele machines (Vm's), opslag en netwerken. De virtuele machine wordt beveiligd en bijgewerkt door Azure. Deze Vm's maken geen deel uit van uw on-premises omgeving, evenals het geval van een IaaS (Infrastructure as a Service). De Cloud beheer gateway is een PaaS die uw Configuration Manager-omgeving uitbreidt naar de Cloud. Zie [PaaS-implementaties beveiligen](/azure/security/security-paas-deployments)voor meer informatie.

### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Hoe kan ik ervoor zorgen dat de service continuïteit tijdens service-updates?

Door CMG te schalen om twee of meer exemplaren op te halen, profiteert u automatisch van update domeinen in Azure. Bekijk [hoe u een Cloud service bijwerkt](/azure/cloud-services/cloud-services-update-azure-service).

### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Ik gebruik IBCM al. Hoe gedragen clients zich als ik CMG toevoeg?

Als u [op internet gebaseerde client beheer](../plan-internet-based-client-management.md) (IBCM) al hebt geïmplementeerd, kunt u ook de Cloud beheer Gateway implementeren. Clients ontvangen beleid voor beide services. Wanneer ze op Internet roamen, selecteren en gebruiken ze wille keurig een van deze op internet gebaseerde services.

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a>Moeten de gebruikers accounts zich in dezelfde Azure AD-Tenant bevindt als de Tenant die is gekoppeld aan het abonnement dat als host fungeert voor de CMG-Cloud service?
<!--SCCMDocs-pr issue #2873-->
Nee, u kunt CMG implementeren in elk abonnement dat Azure Cloud Services kan hosten.

Voor waarden verduidelijken:

- De _Tenant_ is de map van gebruikers accounts en app-registraties. Een Tenant kan meerdere abonnementen hebben.
- Een _abonnement_ scheidt facturering, resources en services. Deze is gekoppeld aan één Tenant.

Deze vraag is gebruikelijk in de volgende scenario's:  

- Wanneer u een unieke test-en productie Active Directory en Azure AD-omgevingen hebt, maar één gecentraliseerd Azure-hosting abonnement.

- Uw gebruik van Azure is op biologische wijze toegenomen over verschillende teams

Wanneer u een Resource Manager-implementatie gebruikt, moet u de Azure AD-Tenant die is gekoppeld aan het abonnement, onboarden. Met deze verbinding kan Configuration Manager worden geverifieerd bij Azure om de CMG te maken, implementeren en beheren.  

Als u Azure AD-verificatie gebruikt voor de gebruikers en apparaten die worden beheerd via de CMG, kunt u de Azure AD-Tenant onboarden. Zie [Azure-Services configureren](../../../servers/deploy/configure/azure-services-wizard.md)voor meer informatie over Azure-Services voor Cloud beheer. Wanneer u elke Azure AD-Tenant onboardeert, kan één CMG Azure AD-verificatie bieden voor meerdere tenants, ongeacht de hosting locatie.

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>Voor beeld 1: één Tenant met meerdere abonnementen

De gebruikers identiteiten, apparaatregistratie en app-registraties bevinden zich allemaal in dezelfde Tenant. U kunt kiezen welk abonnement door de CMG wordt gebruikt. U kunt meerdere CMG-services van één site implementeren in afzonderlijke abonnementen. De site heeft een een-op-een-relatie met de Tenant. U bepaalt welke abonnementen u moet gebruiken om verschillende redenen, zoals facturering of logische schei ding.

#### <a name="example-2-multiple-tenants"></a>Voor beeld 2: meerdere tenants

Met andere woorden, uw omgeving heeft meer dan één Azure AD. Als u de identiteit van gebruikers en apparaten in beide tenants wilt ondersteunen, moet u de site koppelen aan elke Tenant. Dit proces vereist een beheerders account van elke Tenant om de app-registraties in die Tenant te maken. Eén site kan vervolgens CMG services hosten in meerdere tenants. U kunt in elk beschikbaar abonnement in een van beide tenants een CMG maken. Apparaten die zijn gekoppeld aan of hybride lid zijn van Azure AD, kunnen gebruikmaken van een CMG.

Als de gebruikers-en apparaat-id's zich in één Tenant bevinden, maar het abonnement van de CMG zich in een andere Tenant bevindt, moet u de site koppelen aan beide tenants. Technisch gezien is de client-app niet nodig voor de tweede Tenant die alleen de CMG-service heeft. De client-app biedt alleen gebruikers-en apparaat-authenticatie voor clients die gebruikmaken van de CMG-service.<!-- SCCMDocs#1902 -->

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Wat is de invloed van CMG op mijn clients die zijn verbonden via VPN?

Zwervende clients die via een VPN verbinding maken met uw omgeving, worden doorgaans gedetecteerd als intranet gericht. Ze proberen verbinding te maken met uw on-premises infra structuur, zoals beheer punten en distributie punten. Sommige klanten geven de voor keur aan deze zwervende clients die worden beheerd door Cloud Services, zelfs wanneer ze via VPN verbinding maken. Vanaf versie 1902 koppelt u de CMG aan een grens groep. Deze actie dwingt deze clients om de on-premises site systemen niet te gebruiken. Zie [grens groepen configureren](setup-cloud-management-gateway.md#configure-boundary-groups)voor meer informatie.

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Als ik een CMG inschakel, zullen mijn clients alleen verbinding maken met het beheer punt met CMG wanneer ze zijn verbonden met het intranet?

Als u gevoelig verkeer wilt beveiligen dat via een CMG wordt verzonden, configureert u een HTTPS-beheer punt of gebruikt u Enhanced HTTP.

Als u ervoor kiest om een CMG te implementeren en PKI-certificaten te gebruiken voor HTTPS-communicatie op het beheer punt waarvoor CMG is ingeschakeld, selecteert u de optie voor het **toestaan van clients met alleen Internet toegang** tot de eigenschappen van het beheer punt. Deze instelling zorgt ervoor dat interne clients HTTP-beheer punten blijven gebruiken in uw omgeving.

Als u verbeterde HTTP gebruikt, hoeft u deze instelling niet te configureren. Clients blijven HTTP gebruiken bij het rechtstreeks communiceren met het CMG-beheer punt. Zie [Enhanced http](../../../plan-design/hierarchy/enhanced-http.md)(Engelstalig) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- [Een cloudbeheergateway plannen](plan-cloud-management-gateway.md)
- [Een cloudbeheergateway instellen](setup-cloud-management-gateway.md)
- [Certificaten voor cloudbeheergateway](certificates-for-cloud-management-gateway.md)
- [Beveiliging en privacy voor cloudbeheergateway](security-and-privacy-for-cloud-management-gateway.md)
- [Grootte en schaal van de Cloud beheer gateway](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
