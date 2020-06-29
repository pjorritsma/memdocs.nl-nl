---
title: iOS-/iPadOS-apparaten inschrijven bij Intune
titleSuffix: Microsoft Intune
description: Lees hoe u het inschrijven van iOS-/iPadOS-apparaten in Microsoft Intune kunt instellen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/23/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 439c33a6-e80c-4da9-ba09-a51fc36f62ad
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba44cca323dd2a3fbf756b86743dea403ce0b156
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093059"
---
# <a name="enroll-iosipados-devices-in-intune"></a>iOS-/iPadOS-apparaten inschrijven bij Intune

Intune maakt Mobile Device Management (MDM) mogelijk voor iPads en iPhones en geeft gebruikers beveiligde toegang tot zakelijke e-mail, gegevens en apps.

Als Intune-beheerder kunt u de registratie voor iOS-/iPadOS- en iPadOS-apparaten instellen voor toegang tot bedrijfsbronnen. U kunt gebruikers toestaan apparaten in persoonlijk eigendom in te schrijven. Dit wordt ook wel BYOD-inschrijving (Bring Your Own Device) genoemd. U kunt ook de inschrijving van apparaten in bedrijfseigendom inschakelen.

## <a name="prerequisites-for-iosipados-enrollment"></a>Vereisten voor iOS-/iPadOS-inschrijving

Voordat u de inschrijving van iOS-/iPadOS-apparaten kunt inschakelen, moet u de volgende stappen uitvoeren:

- [Controleren of uw apparaten worden ondersteund](../fundamentals/supported-devices-browsers.md).
- [Intune instellen](../fundamentals/setup-steps.md): hiermee stelt u de Intune-infrastructuur in. Voor apparaatinschrijving is met name het [instellen van uw MDM-instantie](../fundamentals/mdm-authority-set.md) van belang.
- [Een Apple MDM-pushcertificaat ophalen](apple-mdm-push-certificate-get.md): Apple vereist een certificaat voor het inschakelen van het beheer van iOS-/iPadOS- en macOS-apparaten.

## <a name="user-owned-iosipados-and-ipados-devices-byod"></a>iOS-/iPadOS- en iPadOS-apparaten die het eigendom van gebruikers zijn (BYOD)

U kunt gebruikers hun persoonlijke apparaten laten inschrijven voor Intune-beheer, wat 'Bring Your Own Device' of BYOD wordt genoemd. Er zijn drie opties voor het inschrijven van gebruikers:
- Beveiligingsbeleid voor apps biedt u de lichtste BYOD-ervaring, met alleen beheer op app-niveau. Als u het apparaat echter ook wilt beveiligen met een complexere 6-cijferige pincode, kunt u dit beleid gebruiken in combinatie met gebruikersinschrijving.
- Apparaatinschrijving is een veelgebruikte vorm van BYOD-inschrijving. Het biedt beheerders een breed scala aan beheeropties.
- Gebruikersinschrijving is een meer gestroomlijnd inschrijvingsproces en biedt beheerders een subset aan apparaatbeheeropties. Deze functie is momenteel in preview. 

Zodra u aan de vereisten hebt voldaan en gebruikerslicenties hebt toegewezen, kunnen gebruikers in de App Store de Intune-bedrijfsportal-app downloaden en in de app de inschrijvingsinstructies volgen. U kunt de privacyverklaring van Bedrijfsportal op iOS-iPadOS aanpassen, zoals wordt uitgelegd in [De app Microsoft Intune-bedrijfsportal configureren](../apps/company-portal-app.md#configuration).

## <a name="company-owned-iosipados-devices"></a>iOS-/iPadOS-apparaten die bedrijfseigendom zijn

Voor organisaties die apparaten voor hun gebruikers aanschaffen, ondersteunt Intune de volgende inschrijvingsmethoden voor iOS-/iPadOS-apparaten die bedrijfseigendom zijn:

- Automatische apparaatinschrijving (Automated Device Enrollment of ADE) van Apple
- Apple School Manager
- Inschrijving via Apple Configurator Setup Assistant
- Directe inschrijving via Apple Configurator

U kunt iOS-/iPadOS-apparaten die bedrijfseigendom zijn ook inschrijven met een [Device Enrollment Manager](device-enrollment-manager-enroll.md)-account.

## <a name="automated-device-enrollment"></a>Automatische apparaatinschrijving

Organisaties kunnen nu iOS-/iPadOS-apparaten aanschaffen via de automatische apparaatinschrijving (ADE) van Apple. Met ADE kunt u een inschrijvingsprofiel draadloos implementeren om apparaten voor beheer in te schrijven. Zie [iOS/iPadOS-apparaten automatisch inschrijven met Automated Device Enrollment van Apple](device-enrollment-program-enroll-ios.md).

## <a name="user-enrollment"></a>Gebruikersinschrijving
Gebruikersinschrijving biedt beheerders een subset van beheeropties vergeleken met andere inschrijvingsmethoden. Zie [Ondersteunde acties, wachtwoorden en andere opties voor gebruikersinschrijving](ios-user-enrollment-supported-actions.md) en [iOS-/iPadOS- en iPadOS-gebruikersinschrijving instellen](ios-user-enrollment.md) voor meer informatie.

## <a name="apple-school-manager"></a>Apple School Manager

Apple School Manager is een programma voor het aanschaffen en inschrijven van apparaten voor scholen. Net als bij ADE kunt u een profiel implementeren om apparaten in te schrijven voor beheer. Meer informatie over [Apple School Manager](apple-school-manager-set-up-ios.md).

## <a name="apple-configurator"></a>Apple Configurator

U kunt iOS-/iPadOS-apparaten inschrijven met Apple Configurator op een Mac-computer. Ter voorbereiding daarop sluit u de apparaten aan via USB en installeert u een inschrijvingsprofiel. U kunt apparaten op twee manieren inschrijven met Apple Configurator:

- Inschrijving met Configuratieassistent: hierbij wordt het apparaat gewist, wordt het apparaat voorbereid voor uitvoering van Configuratieassistent en worden de bedrijfsbeleidsregels voor de nieuwe gebruiker van het apparaat geïnstalleerd.
- Directe registratie: met dit proces wordt het apparaat niet gewist en wordt het apparaat met een vooraf gedefinieerd beleid geregistreerd. Deze methode is geschikt voor apparaten zonder gebruikersaffiniteit.

Meer informatie over [Apple Configurator-inschrijving](apple-configurator-enroll-ios.md).

## <a name="use-the-company-portal-on-ade-enrolled-or-apple-configurator-enrolled-devices"></a>De bedrijfsportal gebruiken op apparaten die bij ADE of Apple Configurator zijn geschreven

Op apparaten die zijn geconfigureerd met gebruikersaffiniteit kan de bedrijfsportal-app worden geïnstalleerd en uitgevoerd om apps te downloaden en apparaten te beheren. Nadat gebruikers hun apparaten hebben ontvangen, moeten zij een aantal extra stappen uitvoeren om de Configuratieassistent te voltooien en de bedrijfsportal-app te installeren.

Gebruikersaffiniteit is vereist voor de ondersteuning van het volgende:

- MAM-apps (Mobile Application Management)
- Voorwaardelijke toegang tot e-mail en bedrijfsgegevens
- Bedrijfsportal-app

### <a name="how-users-enroll-corporate-owned-iosipados-devices-with-user-affinity"></a>iOS-/iPadOS-apparaten in bedrijfseigendom inschrijven met gebruikersaffiniteit

1. Wanneer gebruikers hun apparaat inschakelen, wordt ze gevraagd de Configuratieassistent te voltooien.
2. Na het voltooien van de installatie wordt er naar de Apple ID van de gebruikers gevraagd. Er moet een Apple ID worden opgegeven zodat de bedrijfsportal op het apparaat kan worden geïnstalleerd.
3. Op het iOS-/iPadOS-apparaat wordt de bedrijfsportal-app automatisch via de App Store geïnstalleerd.
4. Gebruikers moeten de bedrijfsportal-app openen en zich aanmelden met de referenties (zoals hun unieke gebruikersnaam of UPN) die zijn gekoppeld aan hun abonnement in Intune.
5. Na het aanmelden is de inschrijving voltooid. Gebruikers kunnen dit apparaat nu gebruiken met de volledige set mogelijkheden.

### <a name="about-corporate-owned-managed-devices-with-no-user-affinity"></a>Over beheerde bedrijfsapparaten zonder gebruikersaffiniteit

Apparaten die zijn geconfigureerd zonder gebruikersaffiniteit bieden geen ondersteuning voor de bedrijfsportal. De app moet niet op deze apparaten worden geïnstalleerd. De bedrijfsportal is bedoeld voor gebruikers met zakelijke referenties die toegang tot persoonlijke bedrijfsresources (bijvoorbeeld e-mail) nodig hebben. Apparaten die zijn ingeschreven zonder gebruikersaffiniteit zijn niet bedoeld voor gebruik met een specifieke gebruikersaanmelding. Kiosks, verkooppunten (POS) of apparaten met gedeelde hulpmiddelen zijn typische gebruiksvoorbeelden van apparaten die zonder gebruikersaffiniteit worden ingeschreven.

Als gebruikersaffiniteit vereist is, moet **Gebruikersaffiniteit** in het inschrijvingsprofiel van het apparaat zijn geselecteerd voordat het apparaat wordt ingeschreven. Als u de status van de affiniteit op een apparaat wilt wijzigen, moet u het apparaat buiten gebruik stellen en opnieuw inschrijven.

## <a name="see-also"></a>Zie tevens

[Problemen met inschrijving van iOS-/iPadOS-apparaten in Microsoft Intune oplossen](https://support.microsoft.com/help/4039809)
