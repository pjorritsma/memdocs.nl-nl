---
title: Basisconfiguratie van Microsoft Intune
description: In dit artikel wordt beschreven wat de benodigde stappen zijn voor het instellen van Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60cfa440-0723-4ea0-bacf-3c5d26f9a1d3
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: c39174dded9fae0055786b6132b3f964f187b1b1
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992705"
---
# <a name="basic-setup"></a>Basisconfiguratie

Nadat u uw omgeving hebt geëvalueerd, is het tijd om Microsoft Intune in te stellen.

## <a name="external-dependencies-for-an-intune-deployment"></a>Externe afhankelijkheden voor een Intune-implementatie

### <a name="identity"></a>Identiteit

Voor Intune is Azure Active Directory (Azure AD) vereist als id- en gebruikersgroepprovider. Meer informatie over:

- [Identiteitsvereisten](/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview#design-considerations-overview)

- [Adreslijstsynchronisatie](/azure/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements)

- [Multi-factor authentication (MFA)](/azure/active-directory/authentication/concept-mfa-howitworks)

- [Gebruikers- en apparaatgroepen plannen](users-add.md)

- [Gebruikers- en apparaatgroepen maken](groups-get-started.md)

Als uw organisatie al met Microsoft 365 werkt, moet Intune van dezelfde Azure Active Directory-omgeving gebruikmaken.

### <a name="pki-optional"></a>PKI (optioneel)

Als u van plan bent om bij Intune verificatie op basis van certificaten te gebruiken voor VPN-, Wi-Fi- of e-mailprofielen, moet u ervoor zorgen dat u over een ondersteunde [PKI-infrastructuur](../protect/certificates-configure.md) beschikt waarmee certificaatprofielen kunnen worden gemaakt en geïmplementeerd. Meer informatie over het configureren van certificaten in Intune:

- [De certificaatinfrastructuur voor SCEP configureren](/intune/certificates-scep-configure)

- [De certificaatinfrastructuur voor PFX configureren](/intune/certficates-pfx-configure).

## <a name="task-list-for-an-intune-setup"></a>Lijst met taken voor een Intune-configuratie

### <a name="task-1-intune-subscription"></a>Taak 1: Intune-abonnement

Voordat u naar Intune kunt migreren, moet u eerst beschikken over een [Intune-abonnement](account-sign-up.md).

### <a name="task-2-assign-intune-user-licenses"></a>Stap 2: Intune-gebruikerslicenties toewijzen

- Meer informatie over het [toewijzen van Intune-gebruikerslicenties](licenses-assign.md).

- Als u een nieuwe AAD-tenant hebt gemaakt, lees dan [hoe u nieuwe gebruikers maakt of gebruikers uit uw on-premises Active Directory (AD) synchroniseert.](/azure/active-directory/connect/active-directory-aadconnect)

### <a name="task-3-set-your-mdm-authority-to-intune"></a>Taak 3: de MDM-instantie instellen op Intune

U wordt aangeraden Intune te beheren met behulp van het [Beheercentrum voor Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Stel uw MDM-instantie in op **Intune**. Door het gebruik van een andere MDM-instantie kan Intune het MDM-beheer overdragen aan andere Microsoft-beheerconsoles. Deze gevallen zijn niet gebruikelijk.

> [!IMPORTANT]
> Als u het beheer van mobiele apparaten voor het eerst overdraagt aan Intune, moet u de MDM-instantie instellen op Intune.

Meer informatie over [het instellen van de instantie voor het beheer van mobiele apparaten](mdm-authority-set.md).

## <a name="next-step"></a>Volgende stap

[Beheerbeleid voor apparaten en apps configureren](migration-guide-configure-policies.md).