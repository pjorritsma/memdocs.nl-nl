---
title: Eindgebruikers accepteren door middel van voorwaardelijke toegang
titleSuffix: Microsoft Intune
description: Lees hoe u voorwaardelijke toegang gebruikt om het inschrijven in Microsoft Intune aan te sturen.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c2d7ce3f-fe97-4044-ad9e-25ac8fa301c9
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4998dab72196d904e2530e85481b0498c8e23c21
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022208"
---
# <a name="drive-end-user-adoption-with-conditional-access-in-microsoft-intune"></a>Eindgebruikers accepteren door middel van voorwaardelijke toegang in Microsoft Intune

Wanneer u functies voor voorwaardelijke toegang bij Intune inschakelt, zoals het blokkeren van e-mail voor niet-ingeschreven apparaten, kan dat helpen bij de registratie en naleving. Functies voor voorwaardelijke toegang zijn echter geen voorwaarde voor een geslaagde migratie. Uw acceptatiedoelstellingen en beveiligingsvereisten voor de migratie moeten bepalend zijn voor het slagen van de migratie.

## <a name="migration-campaign-with-conditional-access"></a>Migratiecampagne met voorwaardelijke toegang

Hier volgt een gebruikelijke benadering voor het uitbreiden van de migratiecampagne met voorwaardelijke toegang:

1. Stel regels voor voorwaardelijke toegang in die moeten worden doorgevoerd voor alle gebruikers. Sluit echter de gebruikers uit die moeten migreren vanuit een voorgaande MDM-provider. U kunt een Azure AD-gebruikersgroep maken met daarin alle gebruikers die zijn uitgesloten van voorwaardelijke toegang.

2. Wanneer gebruikers migreren, verwijdert u ze uit de groep van gebruikers die zijn uitgesloten van voorwaardelijke toegang.

3. Nadat de migratie is voltooid, configureert u alle beleidsregels voor voorwaardelijke toegang om gebruikers standaard te blokkeren, tenzij Intune toegang verleent.

### <a name="advantages"></a>Voordelen

- Het biedt toegangsbeheer voor nieuwe gebruikersaccounts of gebruikersaccounts die niet werden beheerd door de voorgaande oplossing.

- Het biedt een respijtperiode voor gebruikers van een voorgaande oplossing tot aan de migratie.

- Het minimaliseert het verlies aan productiviteit.

### <a name="disadvantages"></a>Nadelen

- Gebruikers van een voorgaande oplossing zouden met niet-beheerde apparaten toegang tot resources kunnen krijgen totdat voorwaardelijke toegang voor die gebruikers is ingeschakeld.


Dit is een van de vele benaderingen. U kunt een eenvoudigere procedure hanteren waarbij alle beleidsregels voor voorwaardelijke toegang worden uitgesteld totdat elke fase de instructie heeft gekregen om de apparaten in te schrijven. U kunt ook een striktere procedure hanteren waarbij vanaf het begin voorwaardelijke toegang wordt toegepast en volledige naleving voor alle toegang is vereist.

- Meer informatie over [voorwaardelijke toegang](../protect/conditional-access.md).

## <a name="task-list-for-conditional-access"></a>Lijst met taken voor voorwaardelijke toegang

### <a name="task-1-decide-how-you-are-going-to-implement-conditional-access"></a>Taak 1: beslissen hoe u voorwaardelijke toegang wilt implementeren

[Gebruikelijke manieren om voorwaardelijke toegang te gebruiken](../protect/conditional-access-intune-common-ways-use.md).

### <a name="task-2-set-up-intune-conditional-access"></a>Taak 2: voorwaardelijke toegang van Intune instellen

Kies een van de volgende opties:

- [Voorwaardelijke toegang in Azure Active Directory configureren](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)

- [De on-premises Exchange-connector installeren met Intune](../protect/exchange-connector-install.md)

- [Beleid voor voorwaardelijke toegang op basis van een app instellen voor Exchange Online](../protect/app-based-conditional-access-intune-create.md)

- [Beleid voor voorwaardelijke toegang op basis van apps instellen voor SharePoint Online](../protect/app-based-conditional-access-intune-create.md)

- [Apps die geen gebruik maken van moderne verificatie blokkeren (ADAL of MSAL)](../protect/app-modern-authentication-block.md) 

## <a name="next-steps"></a>Volgende stappen

Meer informatie over de [standaardmigratiecyclus](migration-guide-cycle.md).
