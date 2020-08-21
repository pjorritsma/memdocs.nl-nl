---
title: Paden naar co-beheer
titleSuffix: Configuration Manager
description: Meer informatie over de vereisten voor de twee primaire manieren waarop u co-beheer kunt instellen.
ms.date: 06/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a685e10ecdb2f6fac8d5634fd932facf52fddcb0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694947"
---
# <a name="paths-to-co-management"></a>Paden naar co-beheer

Er zijn twee primaire manieren waarop u co-beheer kunt instellen. Het is belang rijk om inzicht te krijgen in de vereisten voor elk pad. Ze vereisen elk een combi natie van Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune en Windows 10. 

1. [Bestaande door Configuration Manager beheerde apparaten automatisch inschrijven bij intune](#bkmk_path1)  
2. [Boots trap de Configuration Manager-client met moderne inrichting](#bkmk_path2)  

![Diagram van paden voor co-beheer](media/co-management-paths.png)



## <a name="path-1-auto-enroll-existing-clients"></a><a name="bkmk_path1"></a> Pad 1: bestaande clients automatisch inschrijven

Door dit pad op te nemen, kunnen uw bestaande door Configuration Manager beheerde apparaten snel worden inge schreven bij intune. Het beheer van deze apparaten vanaf Configuration Manager verschilt van voordat u co-beheer inschakelt. Nu profiteert u van alle voor delen in de Cloud. Dit pad is transparant voor uw gebruikers.

U moet het volgende instellen:
- Hybride Azure AD
    - Een van de volgende [Opties voor de hybride identiteit van Azure AD](/azure/active-directory/hybrid/plan-connect-user-signin):  
       - [Wachtwoord hash-synchronisatie](/azure/active-directory/hybrid/plan-connect-user-signin#password-hash-synchronization) met [naadloze eenmalige aanmelding (SSO)](/azure/active-directory/hybrid/how-to-connect-sso)
       - [Pass-Through-verificatie](/azure/active-directory/hybrid/how-to-connect-pta) met [naadloze eenmalige aanmelding (SSO)](/azure/active-directory/hybrid/how-to-connect-sso)
       - [Federatieve SSO (met Active Directory Federation Services (AD FS))](/azure/active-directory/hybrid/plan-connect-user-signin#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)
    - Azure AD Connect
    - Een Azure AD Premium-licentie
    - Hybride Azure AD-samen voeging configureren (Kies één optie):
        - Voor beheerde domeinen
        - Voor federatieve domeinen
- Instelling van client agent voor hybride Azure AD-samen voeging
- De automatische inschrijving van apparaten met intune configureren
- Co-beheer inschakelen in Configuration Manager

Zie [zelf studie: co-beheer inschakelen voor bestaande Configuration Manager-clients](tutorial-co-manage-clients.md)voor een zelf studie over dit pad.



## <a name="path-2-bootstrap-with-modern-provisioning"></a><a name="bkmk_path2"></a> Pad 2: Boots trap met moderne inrichting

U moet het volgende instellen:

1. [Verbeterde HTTP-instellingen](../core/plan-design/hierarchy/enhanced-http.md)  
2. [Cloud Services maken in azure](../core/servers/deploy/configure/azure-services-wizard.md)  
3. [Het beheer punt en clients configureren voor het gebruik van de Cloud beheer gateway](../core/clients/manage/cmg/setup-cloud-management-gateway.md)  
4. [InTune gebruiken om de Configuration Manager-client te implementeren](how-to-prepare-Win10.md)  

Zie [zelf studie: co-beheer inschakelen voor nieuwe apparaten op Internet](tutorial-co-manage-new-devices.md)voor een zelf studie over dit pad.