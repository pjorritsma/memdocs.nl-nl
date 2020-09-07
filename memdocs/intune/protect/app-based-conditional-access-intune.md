---
title: Op apps gebaseerde voorwaardelijke toegang met Intune
titleSuffix: Microsoft Intune
description: Meer informatie over hoe op apps gebaseerde voorwaardelijke toegang werkt met Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: b399fba0-5dd4-4777-bc9b-856af038ec41
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: e1619f3dde57b002ce8884e4af7d4a02e3d71b9f
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992756"
---
# <a name="app-based-conditional-access-with-intune"></a>Op apps gebaseerde voorwaardelijke toegang met Intune

U kunt [beveiligingsbeleid voor apps in Intune](../apps/app-protection-policy.md) gebruiken om te helpen bij het beveiligen van uw bedrijfsgegevens op apparaten die zijn geregistreerd in Intune. U kunt ook beveiligingsbeleid voor apps gebruiken op apparaten die in het bezit zijn van werknemers en die niet zijn geregistreerd voor beheer in Intune. In dit geval moet u, zelfs als u het apparaat niet beheert, er nog steeds voor zorgen dat uw bedrijfsgegevens en -bronnen zijn beveiligd.

Met op apps gebaseerde voorwaardelijke toegang en beheer van client-apps voegt u een beveiligingslaag toe door ervoor te zorgen dat alleen client-apps die app-beveiligingsbeleid van Intune ondersteunen, toegang hebben tot Exchange Online en andere Microsoft 365-services.

> [!NOTE]
> Een beheerde app is een app waarop app-beveiligingsbeleid is toegepast en die door Intune kan worden beheerd.

U kunt de ingebouwde e-mailapps voor iOS/iPadOS en Android blokkeren wanneer u alleen toegang van de Microsoft Outlook-app tot Exchange Online toestaat. Bovendien kunt u de toegang tot SharePoint Online blokkeren voor apps waarvoor geen app-beveiligingsbeleid in Intune is ingesteld.

## <a name="prerequisites"></a>Vereisten

Als u een op apps gebaseerd beleid voor voorwaardelijke toegang wilt maken, moet u over het volgende beschikken:

- **Microsoft Enterprise Mobility + Security (EMS)** of een **Azure Active Directory (AD) Premium-abonnement**
- Gebruikers moeten een licentie hebben voor EMS of Azure AD

Zie [Prijzen van Enterprise Mobility](https://www.microsoft.com/cloud-platform/enterprise-mobility-pricing) of [Prijzen van Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) voor meer informatie.

## <a name="supported-apps"></a>Ondersteunde apps

Een lijst met apps die ondersteuning bieden voor voorwaardelijke toegang op app-basis is beschikbaar in de [technische naslaginformatie over voorwaardelijke toegang voor Azure Active Directory](/azure/active-directory/active-directory-conditional-access-technical-reference).

Op apps gebaseerde voorwaardelijke toegang [biedt ook ondersteuning voor LOB-apps (Line-Of-Business)](app-modern-authentication-block.md), maar als u deze apps wilt gebruiken, moet u gebruikmaken van [moderne Microsoft 365-verificatie](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a). 

## <a name="how-app-based-conditional-access-works"></a>Hoe op apps gebaseerde voorwaardelijke toegang werkt

In dit voorbeeld heeft de beheerder beveiligingsbeleid voor de Outlook-app toegepast, gevolgd door een regel voor voorwaardelijke toegang waarmee de Outlook-app wordt toegevoegd aan een lijst met goedgekeurde apps die kunnen worden gebruikt bij het openen van bedrijfs-e-mail.

> [!NOTE]
> Het volgende stroomdiagram kan worden gebruikt voor andere beheerde apps.

![Op apps gebaseerde voorwaardelijke toegang geïllustreerd in een stroomdiagram](./media/app-based-conditional-access-intune/ca-intune-common-ways-3.png)

1. De gebruiker probeert te verifiëren met Azure AD vanuit de Outlook-app.

2. De gebruiker wordt omgeleid naar de app store om een broker-app te installeren bij de eerste verificatiepoging. De broker-app kan de Microsoft-Authenticator voor iOS of de Microsoft-bedrijfsportal voor Android-apparaten zijn.

   Als gebruikers een systeemeigen e-mailapp willen gebruiken, worden ze omgeleid naar de app store, waarna ze de Outlook-app kunnen installeren.

3. De broker-app wordt op het apparaat geïnstalleerd.

4. Met de broker-app wordt het registratieproces van Azure AD gestart om een apparaatrecord te maken in Azure AD. Dit is niet hetzelfde zijn als het MDM-inschrijvingsproces (Mobile Device Management), maar deze record is nodig om het beleid voor voorwaardelijke toegang te kunnen afdwingen op het apparaat.

5. De broker-app verifieert de identiteit van de app. Er is een beveiligingslaag zodat met de broker-app kan worden gevalideerd of de app is gemachtigd voor gebruik.

6. De broker-app verzendt de client-id van de app naar Azure AD als onderdeel van het verificatieproces voor de gebruiker om te controleren of de app voorkomt in de lijst met goedgekeurde beleidsregels.

7. Met Azure AD kan de gebruiker worden geverifieerd en wordt de app op de lijst met goedkeurde beleidsregels gebruikt. Als de app niet voorkomt op de lijst, wordt de toegang tot de app geweigerd.

8. De Outlook-app communiceert met de Outlook-cloudservice voor communicatie met Exchange Online.

9. De Outlook-cloudservice communiceert met Azure AD om de Exchange Online-toegangstoken voor de gebruiker op te halen.

10. De Outlook-app communiceert met Exchange Online om het bedrijfs-e-mailadres van de gebruiker op te halen.

11. Bedrijfs-e-mail wordt bezorgd in het postvak van de gebruiker.

## <a name="next-steps"></a>Volgende stappen
[Op apps gebaseerd beleid voor voorwaardelijke toegang maken](app-based-conditional-access-intune-create.md)

[Apps die geen gebruik maken van moderne verificatie blokkeren](app-modern-authentication-block.md)