---
title: Mogelijkheden die Intune biedt per inschrijvingsmethode voor Windows-apparaten
titleSuffix: Microsoft Intune
description: Mogelijkheden per inschrijvingsmethode voor Windows-apparaten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/21/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 701794ba476f87aaf079e39c834f3e8e3f2c280d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88913882"
---
# <a name="intune-enrollment-method-capabilities-for-windows-devices"></a>Mogelijkheden die Intune biedt per inschrijvingsmethode voor Windows-apparaten
[!INCLUDE[azure_portal](../includes/azure_portal.md)]

Er zijn verschillende methoden om de apparaten van uw werknemers in te schrijven bij Intune. Voor elke methode gelden andere aanbevolen procedures en mogelijkheden, zoals wordt weergegeven in de onderstaande tabellen.

## <a name="best-practices-by-enrollment-method"></a>Aanbevolen procedures per inschrijvingsmethode
| **Best practices** | **[Neemt deel aan Azure AD](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Neemt deel aan Azure AD via Autopilot (Gebruikersmodus)](../../autopilot/enrollment-autopilot.md)** |**[Neemt deel aan Azure AD via Autopilot (Zelf-implementatiemodus)](../../autopilot/enrollment-autopilot.md)** |**[Bulk](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Co-beheer](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Veel gebruikt in EDU|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Apparaten kunnen worden gebruikt als gedeelde apparaten|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Persoonlijke apparaten moeten toegang hebben tot bedrijfsresources|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Self-service voor apps|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>Mogelijkheden per inschrijvingsmethode

| **Mogelijkheden** | **[Neemt deel aan Azure AD](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Neemt deel aan Azure AD via Autopilot (Gebruikersmodus)](../../autopilot/enrollment-autopilot.md)** |**[Neemt deel aan Azure AD via Autopilot (Zelf-implementatiemodus)](../../autopilot/enrollment-autopilot.md)** |**[Bulk](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[Co-beheer](/configmgr/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Voorwaardelijke toegang                                      |![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)\*\*|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|
|Gebruikers worden gekoppeld aan apparaten                    |![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|
|Azure AD Premium is vereist                               |![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|
|Apparaten krijgen toegang tot resources met CA-beveiliging             |![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|
|Gebruikers mogen geen beheerder zijn op hun apparaat               |![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Mogelijkheid om de apparaatconfiguratie-ervaring te wijzigen        |![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|
|Mogelijkheid om apparaten in te schrijven zonder tussenkomst van de gebruiker      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|
|Mogelijkheid om PowerShell-scripts uit te voeren                       |![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/checkmark.png)\*| 
|Biedt ondersteuning voor automatische inschrijving na AD-domeindeelname      |![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|
|Biedt ondersteuning voor automatische inschrijving na hybride Azure AD-deelname|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|
|Biedt ondersteuning voor automatische inschrijving na Azure AD-deelname       |![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![Vinkje](./media/enrollment-method-capab/checkmark.png)|![X](./media/enrollment-method-capab/xmark.png)|![X](./media/enrollment-method-capab/xmark.png)|

\* Workloads Client-app in Configuration Manager moeten worden verplaatst naar Intune Pilot of Intune.

\** [Apparaten worden geblokkeerd voor Voorwaardelijke toegang, met uitzondering van Windows 10 1803+.](device-enrollment-manager-enroll.md)

## <a name="next-steps"></a>Volgende stappen

[Inschrijving instellen voor Windows](windows-enroll.md)