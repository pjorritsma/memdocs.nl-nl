---
title: Zimperium MTD integreren met Microsoft Intune
titleSuffix: Microsoft Intune
description: Meer informatie over hoe u de Zimperium Mobile Threat Defense-oplossing (MTD) instelt met Microsoft Intune om toegang tot uw bedrijfsresources met mobiele apparaten te beheren.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 889706a0fcf0d84abcbdb70b429e507233159254
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915939"
---
# <a name="integrate-zimperium-with-intune"></a>Zimperium integreren met Intune

Voer de volgende stappen uit om de Zimperium Mobile Threat Defense-oplossing te integreren met Intune.

## <a name="before-you-begin"></a>Voordat u begint

De volgende stappen worden uitgevoerd in de [Zimperium MTD-console](https://www.zimperium.com/platform) en maken een verbinding mogelijk met de service van Zimperium voor zowel Intune-ingeschreven apparaten (via apparaatcompatibiliteit) als niet-geregistreerde apparaten (via app-beveiligingsbeleid).

Zorg ervoor dat u de volgende abonnementen en referenties bij de hand hebt voordat u begint met de integratie van Zimperium met Intune:

- Microsoft Intune-abonnement

- Globale Azure Active Directory-beheerdersreferenties om de volgende machtigingen te verlenen:

  - Aanmelden en gebruikersprofiel lezen

  - Toegang tot de map als de aangemelde gebruiker

  - Mapgegevens lezen

  - Gegevens van een apparaat verzenden naar Intune

- Administrator-referenties voor toegang tot Zimperium MTD-console.

### <a name="zimperium-app-authorization"></a>Zimperium-app-autorisatie

Het autorisatieproces van de Zimperium-app is als volgt:

- Verleen de Zimperium-service machtigingen om informatie met betrekking tot de status van apparaten naar Intune te communiceren. Hiertoe moet u globale beheerdersreferenties gebruiken. Het verlenen van machtigingen is een eenmalige bewerking. Nadat de machtigingen zijn verleend, zijn de referenties van de globale beheerder niet meer nodig voor dagelijkse bewerkingen.

- Zimperium wordt gesynchroniseerd met het Azure Active Directory (AD) Enrollment-groepslidmaatschap om de database van het apparaat te vullen.

- Toestaan dat Zimperium-beheerconsole Azure AD-enkelvoudige aanmelding (SSO) gebruikt.

- De app Zimperium toestaan zich aan te melden met behulp van Azure AD-eenmalige aanmelding.

Zie voor meer informatie over toestemming en Azure Active Directory-toepassingen [De machtigingen aanvragen bij een directory-beheerder](/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin) in het Azure Active Directory-artikel *Machtigingen en toestemming in het Azure Active Directory v2.0-eindpunt*.


## <a name="to-set-up-zimperium-integration"></a>Instellen van Zimperium-integratie

1. Ga naar [Zimperium MTD-console](https://www.zimperium.com/platform) en meld u aan met uw referenties. Om het installatieproces van de Zimperium-integratie uit te voeren, moet u zich aanmelden als een Azure Active Directory-gebruiker die de rol Globale beheerder heeft. Bij deze eenmalige installatiebewerking worden de globale beheerdersrechten gebruikt om de Zimperium-apps in uw organisatie toestemming te verlenen om te communiceren met Intune. 

2. Kies **Beheer** in het menu links.

3. Kies het tabblad **MDM-instellingen**.

4. Kies **MDM toevoegen** selecteer dan **Microsoft Intune** in de lijst **MDM-provider**.

5. Nadat u Microsoft Intune als MDM-service hebt ingesteld, verschijnt het venster **Configuratie van Microsoft Intune**, kies **Azure Active Directory toevoegen** voor elke volgende optie: **Zimperium zConsole**, **zIPS iOS- en Android-apps** om Zimperium te autoriseren te communiceren met Intune en Azure AD via Azure AD eenmalige aanmelding.

    > [!IMPORTANT]  
    > U moet de Zimperium zConsole-, zIPS iOS- en Android-apps toevoegen om het integratieproces met Intune te voltooien.

6. Kies **Accepteren** om de Zimperium-app te autoriseren te communiceren met Intune en Azure Active Directory.

7. Nadat u de **Zimperium-zConsole**- en de **zIPS iOS- en Android**-apps aan Azure AD hebt toegevoegd, voegt u de Azure AD-beveiligingsgroepen toe. Op die manier kan Zimperium de Azure AD-beveiligingsgroep synchroniseren met de eigen service.

8. Kies **Voltooien** om de configuratie op te slaan en de eerste synchronisatie met Azure AD-beveiligingsgroepen te starten.

9. Afmelden bij de Zimperium MTD-console.

## <a name="next-steps"></a>Volgende stappen

- [Zimperium-apps instellen voor ingeschreven apparaten](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Zimperium-apps instellen voor niet-ingeschreven apparaten](mtd-add-apps-unenrolled-devices.md)