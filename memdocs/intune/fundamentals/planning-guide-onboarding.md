---
title: Intune-onboarding
titleSuffix: Microsoft Intune
description: Dit artikel helpt u bij het bepalen van alle aspecten die moeten worden overwogen bij de onboarding van een cloudoplossing met Microsoft Intune in uw omgeving.
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
ms.assetid: ac7bd764-5365-4920-8fd0-ea57d5ebe039
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b479f770053051e580a68aa810a60c35d745ac5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996347"
---
# <a name="implement-your-microsoft-intune-plan"></a>Uw Microsoft Intune-abonnement implementeren

Tijdens de onboardingfase implementeert u Intune in uw productieomgeving. Het implementatieproces bestaat uit het installeren en configureren van Intune en externe afhankelijkheden (indien nodig) op basis van uw [use-casevereisten](planning-guide-requirements.md).

De volgende sectie biedt een overzicht van het implementatieproces voor Intune met vereisten en taken op hoog niveau.

## <a name="intune-requirements"></a>Vereisten voor Intune

De belangrijkste vereisten voor de zelfstandige versie van Intune zijn:

- Enterprise Mobility + Security (EMS)/Intune-abonnement

- Microsoft 365-abonnement (voor Office-apps en door beveiligingsbeleid voor apps beheerde apps)

- Apple APNs-certificaat (voor het beheer van het iOS/iPadOS-apparaatplatform)

- Azure AD Connect (voor adreslijstsynchronisatie)

- Intune On-Premises Connector voor Exchange (voor voorwaardelijke toegang voor Exchange On-Premises, indien nodig)

- Intune Certificate Connector (voor implementatie van SCEP-certificaten, indien nodig)

>[!TIP]
> Overzicht van de [ondersteunde apparaten](supported-devices-browsers.md) voor een volledige lijst met apparaten die u met Intune kunt beheren.

## <a name="intune-implementation-process"></a>Proces van Intune-implementatie

We hebben 13 verschillende taken voor het implementeren van een Intune-implementatie geïdentificeerd. Afhankelijk van uw zakelijke vereisten, de bestaande infrastructuur en de strategie voor het beheer van apparaten, zijn sommige van deze taken mogelijk al voltooid. Anderen zijn mogelijk niet van toepassing op uw abonnement.

### <a name="task-1-get-an-intune-subscription"></a>Taak 1: een Intune-abonnement kopen

Zoals hierboven aangegeven in de sectie met Intune-vereisten, moet u een EMS- of Intune-abonnement hebben. Als uw organisatie dat niet heeft, kunt u contact opnemen met Microsoft of uw Microsoft-accountteam om aan te geven dat u de aanschaf van Enterprise Mobility + Security (EMS) of Intune overweegt.

- Meer informatie over [het kopen van Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune-pricing).

### <a name="task-2-add-microsoft-365-subscription"></a>Taak 2: Microsoft 365-abonnement toevoegen

Deze stap is optioneel. U moet een Microsoft 365-abonnement hebben als u van plan bent Exchange Online te gebruiken en mobiele Office-apps te beheren met app-beveiligingsbeleid. Als uw organisatie geen Microsoft 365-abonnement heeft, kunt u contact opnemen met Microsoft of uw Microsoft-accountteam om aan te geven dat u de aanschaf van Microsoft 365 overweegt.

- Meer informatie over [het kopen van Microsoft 365](https://products.office.com/business/compare-office-365-for-business-plans).

### <a name="task-3-add-users-groups-in-azure-ad"></a>Taak 3: gebruikersgroepen toevoegen in Azure AD

Wellicht moet u gebruikers of beveiligingsgroepen toevoegen in Active Directory of Azure Active Directory op basis van de use-casescenario's en -vereisten voor uw Intune-implementatie. Controleer uw huidige gebruikers en beveiligingsgroepen in Active Directory of Azure Active Directory om te bepalen of ze volledig voldoen aan uw behoeften. Wanneer u nieuwe gebruikers en beveiligingsgroepen toevoegt, raden we aan deze toe te voegen in Active Directory en te synchroniseren met Azure Active Directory met behulp van Azure AD Connect.

- Meer informatie over [gebruikers/groepen toevoegen aan Intune](users-add.md).
<!---why not send them to the AAD connect topic? Question out to Andre: https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect--->


### <a name="task-4-assign-intune-and-microsoft-365-user-licenses"></a>Taak 4: Intune- en Microsoft 365-gebruikerslicenties toewijzen

Alle gebruikers voor wie de implementatie van EMS/Intune en Microsoft 365 is bedoeld, moeten beschikken over een licentie die aan hen is toegewezen. U kunt EMS/Intune- en Microsoft 365-licenties toewijzen in het Microsoft 365-beheercentrum.

- Meer informatie over [het toewijzen van Intune-licenties](licenses-assign.md).

### <a name="task-5-set-mobile-device-management-authority-to-intune"></a>Taak 5: de instantie voor het beheer van mobiele apparaten instellen op Intune

Voordat u apparaten kunt installeren, configureren, beheren en registreren met behulp van Intune, moet u de instantie voor het beheer van mobiele apparaten instellen op Intune.

- Meer informatie over [de instantie voor het beheer van mobiele apparaten instellen op Intune](mdm-authority-set.md).

### <a name="task-6-enable-device-platforms"></a>Taak 6: platformen voor apparaten inschakelen

De meeste apparaatplatformen zijn standaard ingeschakeld, met uitzondering van Apple-apparaten (iOS/iPadOS en Mac). Voordat iOS/iPadOS-apparaten kunnen worden geregistreerd en beheerd in Intune, moet u het apparaatplatform inschakelen. Om dit te doen, moet u een Push-MDM-certificaat maken en dit toevoegen aan Intune.

- Meer informatie over [registratie voor Apple-apparaten inschakelen](../enrollment/apple-mdm-push-certificate-get.md).

### <a name="task-7-add-and-deploy-terms-and-conditions-policies"></a>Taak 7: voorwaardenbeleid toevoegen en implementeren

Intune ondersteunt beleidsregels voor voorwaarden. Voeg waar nodig voorwaardenbeleid toe en implementeer dit voor doelgroepen op basis van de use cases en vereisten van uw Intune-implementatie.

- Meer informatie over [het toevoegen en implementeren van voorwaardenbeleid](../enrollment/terms-and-conditions-create.md).

### <a name="task-8-add-and-deploy-configuration-policies"></a>Taak 8: configuratiebeleid toevoegen en implementeren

Intune ondersteunt twee typen configuratiebeleid: algemeen en aangepast. Voeg waar nodig configuratiebeleid toe en implementeer dit voor doelgroepen op basis van de use cases en vereisten van uw Intune-implementatie.

- Meer informatie over [het toevoegen en implementeren van configuratiebeleid](../configuration/device-profiles.md).

### <a name="task-9-add-and-deploy-resource-profiles"></a>Taak 9: resourceprofielen toevoegen en implementeren

Intune biedt ondersteuning voor e-mail, wifi en VPN-profielen. Voeg waar nodig deze profielen toe en implementeer deze voor doelgroepen op basis van de use cases en vereisten van uw Intune-implementatie.

- Meer informatie over [toegang tot bedrijfsbronnen inschakelen met Intune](../configuration/device-profiles.md).

### <a name="task-10-add-and-deploy-apps"></a>Taak 10: Apps maken en implementeren

Intune biedt ondersteuning voor de implementatie van web-, bedrijfstakgerichte en openbare store-apps. U kunt ook apps beheren waarin de Intune SDK is geïntegreerd door deze te koppelen aan beveiligingsbeleid voor apps. Voeg waar nodig apps toe en implementeer deze voor doelgroepen op basis van de use cases en vereisten van uw Intune-implementatie.

- Meer informatie over [apps toevoegen en implementeren](../apps/app-management.md).

### <a name="task-11-add-and-deploy-compliance-policies"></a>Taak 11: nalevingsbeleid toevoegen en implementeren

Intune ondersteunt nalevingsbeleid. Voeg waar nodig nalevingsbeleid toe en implementeer dit voor doelgroepen op basis van de use cases en vereisten van uw Intune-implementatie.

- Meer informatie over [nalevingsbeleid](../protect/device-compliance-get-started.md).

### <a name="task-12-enable-conditional-access-policies"></a>Taak 12: beleid voor voorwaardelijke toegang inschakelen

Intune biedt ondersteuning voor voorwaardelijke toegang voor Exchange Online, Exchange on-premises, SharePoint Online, Skype voor Bedrijven Online en Dynamics CRM Online. U kunt voorwaardelijke toegang inschakelen en configureren op basis van de use cases en vereisten van uw Intune-implementatie.

- Meer informatie over [voorwaardelijke toegang](../protect/conditional-access.md).

### <a name="task-13-enroll-devices"></a>Taak 13: Apparaten inschrijven

Intune ondersteunt platformen voor iOS/iPadOS-, macOS-, Android- en Windows-desktopapparaten. Registreer platformen voor mobiele apparaten waar nodig op basis van de use cases en vereisten van uw Intune-implementatie.

- Meer informatie over [het registreren van apparaten](../enrollment/device-enrollment.md).


## <a name="next-steps"></a>Volgende stappen
Meer informatie over het [testen en valideren van uw Intune-implementatie](planning-guide-test-validation.md).
