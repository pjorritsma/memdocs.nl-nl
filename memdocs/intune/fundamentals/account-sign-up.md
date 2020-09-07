---
title: Registreren of aanmelden bij Microsoft Intune
description: Zo kunt u zich registreren voor een Microsoft Intune-abonnement of u aanmelden om met uw abonnement aan de slag te gaan.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0f3ce07a-b718-42a9-bace-f99a8b8abd94
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae034699d3a07311ca6a51557cbbc673916569bf
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88994273"
---
# <a name="sign-up-or-sign-in-to-microsoft-intune"></a>Registreren of aanmelden bij Microsoft Intune

In dit onderwerp wordt aan systeembeheerders uitgelegd hoe u zich kunt aanmelden voor een Intune-account.

Voordat u zich voor Intune aanmeldt, moet u bepalen of u al een Microsoft Online Services-account, Enterprise Agreement of equivalente volumelicentieovereenkomst hebt. Een Microsoft-volumelicentieovereenkomst of ander abonnement op Microsoft-cloudservices, zoals Microsoft 365, omvat gewoonlijk een werk- of schoolaccount.

Als u al een werk- of schoolaccount hebt **meld u dan aan** met dat account en voeg Intune toe aan uw abonnement. Anders kunt u zich **registreren** voor een nieuw account om Intune te gebruiken voor uw organisatie.

>[!WARNING]
>U kunt een bestaand werk- of schoolaccount niet combineren nadat u zich hebt aangemeld voor een nieuw account.

## <a name="how-to-sign-up-for-intune"></a>Aanmelden voor Intune

1. Ga naar de [Registratiepagina van Intune](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20).

   ![Schermafbeelding van de registratiewebpagina van de evaluatieversie van het Microsoft Intune-account](./media/account-sign-up/account-sign-up-site.png)

2. Op de Registratiepagina kunt u zich aanmelden of registreren om een nieuw abonnement van Intune te beheren.

## <a name="post-sign-up-considerations"></a>Overwegingen voor na uw registratie

Nadat u zich hebt geregistreerd voor een nieuw abonnement, ontvangt u een e-mailbericht met gegevens over uw account op het e-mailadres dat u hebt opgegeven tijdens het registratieproces. In deze e-mail wordt bevestigd dat uw abonnement actief is.

Wanneer het registratieproces is voltooid, wordt u omgeleid naar het Microsoft 365-beheercentrum waarin u gebruikers kunt toevoegen en hen licenties kunt toewijzen. Als u alleen cloudgebaseerde accounts hebt met de standaarddomeinnaam onmicrosoft.com, kunt u direct verder gaan om gebruikers toe te voegen en licenties toe te wijzen. Als u echter van plan bent de [aangepaste domeinnaam](custom-domain-name-configure.md) van uw organisatie te gebruiken of [gebruikersaccountgegevens](users-add.md#sync-active-directory-and-add-users-to-intune) vanuit on-premises Active Directory wilt synchroniseren, kunt u dat browservenster sluiten.

## <a name="sign-in-to-microsoft-intune"></a>Aanmelden bij Microsoft Intune

Zodra u zich hebt aangemeld voor Intune, kunt u elk apparaat met een [ondersteunde browser](supported-devices-browsers.md#intune-supported-web-browsers) gebruiken om u aan te melden bij [Intune](https://go.microsoft.com/fwlink/?linkid=2090973) om de service te beheren.

Standaard moet uw account een van de volgende machtigingen hebben in Azure AD:

- Hoofdbeheerder
- Intune-servicebeheerder (ook wel bekend als Intune-beheerder)

Als u toegang wilt verlenen tot het beheer van de service voor gebruikers met andere machtigingen, raadpleegt u [Op rollen gebaseerd toegangsbeheer](role-based-access-control.md)

### <a name="intune-admin-portal-url"></a>URL van de Intune-beheerportal

Beheercentrum voor Microsoft Endpoint Manager: https://endpoint.microsoft.com

Intune Azure-portal: https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade

Intune voor onderwijs: https://intuneeducation.portal.azure.com

Klassieke Intune-portal: https://manage.microsoft.com De klassieke Intune-portal wordt alleen gebruikt voor het beheren van apparaten die zijn ingeschreven bij de Intune-softwareclient voor pc's

### <a name="urls-for-intune-services-provided-by-microsoft-365"></a>URL's voor Intune-services van Microsoft 365

Microsoft 365 Business: https://portal.microsoft.com/adminportal

Microsoft 365 Mobile Device Management: https://admin.microsoft.com/adminportal/home#/MifoDevices

## <a name="see-also"></a>Zie tevens

[U kunt zich niet aanmelden bij Microsoft 365, Azure of Intune](https://support.microsoft.com/help/2412085)
