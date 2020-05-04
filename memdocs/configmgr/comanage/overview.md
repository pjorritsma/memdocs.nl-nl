---
title: Co-beheer voor Windows 10-apparaten
titleSuffix: Configuration Manager
description: Informatie over het gelijktijdig beheren van Windows 10-apparaten met behulp van zowel Configuration Manager als Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/24/2020
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: e06dc0d40eb6359d11ef31045989d7ed398b3687
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711320"
---
# <a name="what-is-co-management"></a>Wat is co-beheer?

<!-- 1350871 -->
Co-beheer is een van de belangrijkste manieren om uw bestaande Configuration Manager-implementatie aan de Microsoft 365 Cloud te koppelen. Het helpt u extra Cloud mogelijkheden te ontgrendelen, zoals voorwaardelijke toegang.

Beheer co-beheer kunt u Windows 10-apparaten tegelijkertijd beheren door zowel Configuration Manager als Microsoft Intune te gebruiken. Het biedt u de mogelijkheid om uw bestaande investering in Configuration Manager te koppelen door nieuwe functionaliteit toe te voegen. Als u co-beheer gebruikt, hebt u de flexibiliteit om de technologie oplossing te gebruiken die voor uw organisatie het meest geschikt is.

Wanneer een Windows 10-apparaat de Configuration Manager-client heeft en is inge schreven bij intune, krijgt u de voor delen van beide services. U bepaalt welke workloads, indien van toepassing, u de instantie overschakelt van Configuration Manager naar intune. Configuration Manager blijft alle andere workloads beheren, met inbegrip van de werk belastingen die u niet overschakelt naar intune en alle andere functies van Configuration Manager die niet door co-beheer worden ondersteund.

U kunt ook een werk belasting testen met een afzonderlijke verzameling apparaten. Met piloten kunt u de intune-functionaliteit testen met een subset van apparaten voordat u een grotere groep wijzigt.

![Overzichts diagram van co-beheer](media/co-management-overview.svg)

[Het diagram op volledige grootte weer geven](media/co-management-overview.svg)

> [!Note]  
> Wanneer u Windows 10-apparaten gelijktijdig beheert met zowel Configuration Manager als Microsoft Intune, wordt deze configuratie *co-beheer*genoemd. Wanneer u apparaten beheert met Configuration Manager en zich registreert bij een MDM-service van derden, wordt deze *configuratie naast elkaar genoemd.* Twee beheer instanties voor één apparaat kunnen lastig zijn als ze niet op de juiste wijze zijn verdeeld tussen de twee. Met co-beheer, Configuration Manager en intune balanceert u de [werk belastingen](#workloads) om te controleren of er geen conflicten zijn. Deze interactie bestaat niet met services van derden, waardoor er beperkingen zijn met de beheer mogelijkheden van samen werking. Zie [MDM-samen werking van derden met Configuration Manager](coexistence.md)voor meer informatie.

## <a name="paths-to-co-management"></a>Paden naar co-beheer

Er zijn twee hoofd paden om te kunnen bereiken voor co-beheer:  

- **Bestaande Configuration Manager-clients**: u hebt Windows 10-apparaten die al Configuration Manager-clients zijn. U stelt hybride Azure AD in en registreert ze bij intune.  

- **Nieuwe apparaten op Internet**: u hebt nieuwe Windows 10-apparaten die deel nemen aan Azure AD en automatisch worden inge schreven bij intune. U installeert de Configuration Manager-client om een co-beheer status te bereiken.  

Zie voor meer informatie over de paden [paden naar co-beheer](quickstart-paths.md).

## <a name="benefits"></a>Voordelen

Wanneer u bestaande Configuration Manager-clients in co-beheer inschrijft, krijgt u de volgende onmiddellijke waarde:  

- Voorwaardelijke toegang met apparaatcompatibiliteit  

- Externe acties op basis van intune, bijvoorbeeld: opnieuw opstarten, extern beheer of fabrieks instellingen terugzetten

- Gecentraliseerde zicht baarheid van apparaatstatus  

- Gebruikers, apparaten en apps koppelen met Azure Active Directory (Azure AD)  

- Modern inrichten met Windows auto pilot  

- Externe acties

Voor meer informatie over deze onmiddellijke waarde van co-beheer raadpleegt u de Quick Start-serie in de [Cloud verbinding maken met co-beheer](quickstarts.md).

Met co-beheer kunt u ook intune organiseren voor verschillende werk belastingen. Zie de sectie [workloads](#workloads) voor meer informatie.

## <a name="prerequisites"></a>Vereisten

Co-beheer heeft deze vereisten op de volgende gebieden:

- [Licentieverlening](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Machtigingen en rollen](#permissions-and-roles)  

### <a name="licensing"></a>Licentieverlening

- Azure AD Premium

    > [!Note]  
    > Een Enterprise Mobility + Security EMS-abonnement omvat zowel Azure Active Directory Premium als Microsoft Intune.

- Ten minste één intune-licentie voor u als beheerder voor toegang tot de intune-Portal.

    > [!Tip]
    > Zorg ervoor dat u een intune-licentie toewijst aan het account dat u gebruikt om u aan te melden bij uw Tenant. Als dat niet het geval is, mislukt de fout melding ' de gebruiker wordt niet herkend '.
    >
    > U hoeft geen afzonderlijke intune-of EMS-licenties meer aan uw gebruikers te kopen en toe te wijzen. Zie [Veelgestelde vragen over producten en licenties](../core/understand/product-and-licensing-faq.md#bkmk_mem)voor meer informatie.

### <a name="configuration-manager"></a>Configuration Manager

Co-beheer vereist Configuration Manager versie 1710 of hoger.

Vanaf Configuration Manager versie 1806 kunt u meerdere exemplaren van Configuration Manager koppelen aan één intune-Tenant. <!--1357944-->  

Als u co-beheer zelf inschakelt, hoeft u uw site niet vrij te maken met Azure AD. Voor het [tweede pad-scenario](#paths-to-co-management)is Configuration Manager-clients op internet gebaseerd op CMG ( [Cloud Management Gateway](../core/clients/manage/cmg/plan-cloud-management-gateway.md) ). De CMG vereist dat de site [onboarded is voor Azure AD voor Cloud beheer](../core/servers/deploy/configure/azure-services-wizard.md).

### <a name="azure-ad"></a>Azure AD

- Windows 10-apparaten moeten lid zijn van Azure AD. Dit kan een van de volgende typen zijn:  

  - [Hybride Azure Ad-lid](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), waarbij het apparaat wordt gekoppeld aan uw on-premises Active Directory en deel uitmaakt van uw Azure Active Directory.  

  - Alleen [lid van Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) . (Dit type wordt soms aangeduid als lid van een Cloud domein)<!--SCCMDocs issue 605-->  

### <a name="intune"></a>Intune

- [Intune instellen](https://docs.microsoft.com/intune/setup-steps)  

- [Automatische inschrijving voor Windows 10 inschakelen](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

### <a name="windows-10"></a>Windows 10

Werk uw apparaten bij naar Windows 10, versie 1709 of hoger. Zie [Windows als een service aannemen](../core/understand/configuration-manager-and-windows-as-service.md#key-articles-about-adopting-windows-as-a-service)voor meer informatie.

> [!IMPORTANT]
> Windows 10 Mobile-apparaten bieden geen ondersteuning voor co-beheer.

### <a name="permissions-and-roles"></a>Machtigingen en rollen

<!--SCCMDocs issue #667-->
| Bewerking | Rol vereist |
|----|----|
| Een Cloud beheer gateway instellen in Configuration Manager | Azure- **abonnements beheerder** |
| Azure AD-apps maken op basis van Configuration Manager | **Globale beheerder** van Azure AD |
| Azure-apps importeren in Configuration Manager | **Volledige beheerder** Configuration Manager<br>Er zijn geen extra Azure-rollen nodig |
| Co-beheer inschakelen in Configuration Manager | Een Azure AD-gebruiker<br>Configuration Manager **volledige beheerder** met **alle** bereik rechten.<!--SCCMDoc issue 626--> |

Zie [inzicht in de verschillende rollen](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles)voor meer informatie over Azure-rollen.

Zie de [basis principes van beheer op basis van rollen](../core/understand/fundamentals-of-role-based-administration.md)voor meer informatie over Configuration Manager rollen.

## <a name="workloads"></a>Workloads

U hoeft de werk belastingen niet te scha kelen of u kunt ze individueel doen wanneer u klaar bent. Configuration Manager blijft alle andere workloads beheren, met inbegrip van de werk belastingen die u niet overschakelt naar intune en alle andere functies van Configuration Manager die niet door co-beheer worden ondersteund.

Co-beheer ondersteunt de volgende werk belastingen:

- Compliance beleidsregels  

- Windows Update beleid  

- Toegangs beleid voor bronnen  

- Endpoint Protection  

- Apparaatconfiguratie  

- Office klik-en-klaar-apps  

- Client-apps  

Zie [workloads](workloads.md)voor meer informatie.

## <a name="monitor-co-management"></a>Co-beheer bewaken

Het dash board voor co-beheer helpt u bij het controleren van computers die in uw omgeving worden beheerd. De grafieken kunnen helpen bij het identificeren van apparaten die mogelijk aandacht vereisen.

![Scherm opname van het dash board voor co-beheer](media/co-management-dashboard.png)

Zie [co-beheer controleren](how-to-monitor.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over de onmiddellijke waarde en aan de slag met co-beheer](quickstarts.md)  

- [Zelf studie: co-beheer inschakelen voor bestaande Configuration Manager-clients](tutorial-co-manage-clients.md)  
