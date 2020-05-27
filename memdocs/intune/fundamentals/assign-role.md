---
title: Een rol aan een Intune-gebruiker toewijzen
description: Meer informatie over het toewijzen van ingebouwde of aangepaste rollen aan gebruikers in Microsoft Intune.
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
ms.openlocfilehash: 31e73bd1c3ebed40865ea6c13952b91c3a672852
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988853"
---
# <a name="assign-a-role-to-an-intune-user"></a>Een rol aan een Intune-gebruiker toewijzen

U kunt een [ingebouwde](role-based-access-control.md#built-in-roles) of [aangepaste](create-custom-role.md) rol toewijzen aan een Intune-gebruiker.

Als u rollen wilt maken, bewerken of toewijzen, moet uw account een van de volgende machtigingen hebben in Azure AD:
- **Globale beheerder**
- **Intune-servicebeheerder**

1. Kies in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Tenantbeheer** > **Rollen** > **Alle rollen**.

2. Kies op de blade **Intune-rollen - Alle rollen** de ingebouwde rol die u wilt toewijzen > **Toewijzingen** > **Toewijzen**.

5. Voer op de pagina **Basisinstellingen** een **Toewijzingsnaam** en desgewenst een **Beschrijving van toewijzing** in en kies **Volgende**.

6. Selecteer op de pagina **Beheergroepen** de groep die de gebruiker bevat aan wie u de machtigingen wilt verlenen. Kies **Volgende**

7. Kies op de pagina **Bereik (groepen)** de groep die de gebruikers/apparaten bevat die het hierboven genoemde lid mag beheren. Kies **Volgende**.

8. Kies op de pagina **Bereik (tags)** de tags waarop deze roltoewijzing moet worden toegepast. Kies **Volgende**.

9. Kies zodra u klaar bent op de pagina **Controleren en maken** de optie **Maken**. De nieuwe toewijzing wordt in de lijst met toewijzingen weergegeven.

## <a name="next-steps"></a>Volgende stappen
- [Meer informatie over op rollen gebaseerd toegangsbeheer in Intune](role-based-access-control.md)
- [Een aangepaste rol maken](create-custom-role.md)


