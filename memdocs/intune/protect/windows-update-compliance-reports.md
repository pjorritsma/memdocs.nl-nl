---
title: Updatenalevingsrapporten voor Windows-updates gebruiken in Microsoft Intune
titleSuffix: Microsoft Intune
description: Gebruik OMS-updatenaleving om rapportgegevens weer te geven voor de Windows-updates die u met Intune implementeert.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/01/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 297707da0afb03650eaab91b26abad9947c6a951
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286149"
---
# <a name="intune-compliance-reports-for-updates"></a>Intune-nalevingsrapporten voor updates

Wanneer u Intune gebruikt om Windows-updates te implementeren op Windows 10-apparaten, bekijkt u details over updatenaleving met behulp van Intune of de gratis oplossing *Updatenaleving*. Updatenaleving is onderdeel van de Microsoft Operations Management Suite (OMS).

## <a name="use-intune"></a>Intune gebruiken

U kunt als volgt een beleidsrapport weergeven met de implementatiestatus voor de Windows 10-update-ringen die u hebt geconfigureerd:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Apparaten** > **Overzicht** > **Status van software-update**. Hier wordt algemene informatie weergegeven over de status van de update-ringen die u hebt toegewezen.

3. Als u meer details wilt zien, selecteert u **Bewaken**. Selecteer onder **Software-updates** de optie **Implementatiestatus per updatering** en kies de implementatiering die u wilt controleren.

   Kies in de sectie **Bewaken** een van de volgende rapporten om meer gedetailleerde informatie over de implementatiering weer te geven:

   - **Apparaatstatus**: hier wordt de configuratiestatus van het apparaat weergegeven. Zie [Update deviceConfigurationDeviceStatus]( /graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0) voor meer details.

   - **Gebruikersstatus**: hier wordt de gebruikersnaam, de status en de laatste rapportagedatum weergegeven. Zie [List deviceConfigurationUserStatuses](/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0) voor meer details.

   - **Updatestatus van de eindgebruiker**: hier wordt de updatestatus van het Windows-apparaat weergegeven. Zie [windowsUpdateState](/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta) voor meer details.

## <a name="use-update-compliance"></a>Updatenaleving gebruiken

Met [Updatenaleving](/windows/deployment/update/update-compliance-monitor) kunt u de Windows 10-update-implementaties bewaken. Updatenaleving wordt u aangeboden via Azure Portal en is gratis beschikbaar voor apparaten die aan de [voorwaarden](/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites) voldoen.  

Wanneer u deze oplossing gebruikt, kunt u een commerciële id implementeren op elk van uw door Intune beheerde Windows 10-apparaten waarvoor u over de naleving van updates wilt rapporteren.  

In Intune worden de OMA-URI-instellingen van een aangepast beleid gebruikt om de commerciële id te configureren. Zie [Aangepaste instellingen gebruiken voor Windows 10-apparaten in Intune](../configuration/custom-settings-windows-10.md).

Het pad voor de OMA-URI (hoofdlettergevoelig) voor het configureren van de commerciële id is: *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*

U kunt bijvoorbeeld de volgende waarden gebruiken in **OMA-URI-instelling toevoegen of bewerken**:

- **Naam van instelling**: Commerciële id voor Windows Analytics
- **Beschrijving van instelling**: Commerciële id voor Windows Analytics-oplossingen configureren
- **OMA-URI** (hoofdlettergevoelig): *./Vendor/MSFT/DMClient/Provider/ProviderID/CommercialID*
- **Gegevenstype**: Tekenreeks
- **Waarde**: \<Use the GUID shown on the Windows Telemetry tab in your OMS workspace>

> [!NOTE]
> Zie [DMClient configuratieserviceprovider (CSP)]( /windows/client-management/mdm/dmclient-csp) voor meer informatie over MS DM Server.

## <a name="next-steps"></a>Volgende stappen

[Software-updates beheren in Intune](windows-update-for-business-configure.md)
