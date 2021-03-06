---
title: Een aangepaste rol in Intune maken
description: Leer hoe u een aangepaste rol maakt in Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 51c8ce62d27efa72b6c974f10364e33fb7e6da76
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988013"
---
# <a name="create-a-custom-role-in-intune"></a>Een aangepaste rol in Intune maken

U kunt een aangepaste Intune-rol maken die alle machtigingen bevat die vereist zijn voor een bepaalde taakfunctie. Als een groep van de IT-afdeling bijvoorbeeld toepassingen, beleidsregels en configuratieprofielen beheert, kunt u al deze machtigingen samenvoegen tot één aangepaste rol. Nadat u een aangepaste rol hebt gemaakt, kunt u deze [toewijzen](assign-role.md) aan elke gebruiker die die machtigingen nodig heeft.

Als u rollen wilt maken, bewerken of toewijzen, moet uw account een van de volgende machtigingen hebben in Azure AD:
- **Globale beheerder**
- **Intune-servicebeheerder**

## <a name="to-create-a-custom-role"></a>Een aangepaste rol maken

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Tenantbeheer** > **Rollen** > **Alle rollen** > **Maken**.

2. Voer op de pagina **Basisinformatie** een naam en een beschrijving in voor de nieuwe rol en selecteer dan **Volgende**.

3. Kies op de pagina **Machtigingen** de machtigingen die u voor deze rol wilt gebruiken.

4. Kies op de pagina **Bereik (tags)** de tags voor deze rol. Wanneer deze rol wordt toegewezen aan een gebruiker, heeft die gebruiker toegang tot resources die ook deze tags hebben. Kies **Volgende**.

5. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. De nieuwe rol wordt weergegeven in de lijst op de blade **Intune-rollen - Alle rollen**.

## <a name="copy-a-role"></a>Een rol kopiëren

U kunt ook een bestaande rol kopiëren.

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Tenantbeheer** > **Rollen** > **Alle rollen** > schakel het selectievakje in bij een rol in de lijst > **Dupliceren**.

2. Voer op de pagina **Basisinformatie** een naam in. Zorg ervoor dat u een unieke naam gebruikt.

3. Alle machtigingen en bereiktags van de oorspronkelijke rol zijn al geselecteerd. U kunt vervolgens de **naam**, **beschrijving**, **machtigingen** en **bereik(tags)** van de dubbele rol wijzigen.

4. Nadat u alle gewenste wijzigingen hebt aangebracht, kiest u **Volgende** om naar de pagina **Controleren en maken** te gaan. Selecteer **Maken**. 

## <a name="next-steps"></a>Volgende stappen
- [Een rol toewijzen aan een gebruiker](assign-role.md)
- [Meer informatie over op rollen gebaseerd toegangsbeheer in Intune](role-based-access-control.md)


