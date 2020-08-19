---
title: E-mailinstellingen voor Windows Phone 8.1 in Microsoft Intune
titleSuffix: ''
description: Meer informatie over de Intune-instellingen die u kunt gebruiken om e-mailverbindingen op apparaten met Windows Phone 8.1 te configureren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5bd00f12ab0f015c6408e2bbc934e1320c7540e
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146135"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>E-mailprofielinstellingen in Microsoft Intune voor apparaten met Windows Phone 8.1

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

In dit artikel ziet u de e-mailprofielinstellingen die u kunt configureren voor uw apparaten met Windows Phone 8.1.

>[!IMPORTANT]
>Windows Phone 8.1-e-mailprofielen worden ook toegepast op Windows 10-apparaten.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een e-mailprofiel voor Windows Phone 8.1](email-settings-configure.md).

## <a name="email-settings"></a>E-mailinstellingen

- **E-mailserver**: Voer de hostnaam van uw Exchange-server in. Voer bijvoorbeeld `outlook.office365.com` in.
- **Accountnaam**: Voer de weergavenaam voor het e-mailaccount in. Deze naam zien gebruikers op hun apparaat.
- **Het kenmerk Gebruikersnaam van AAD**: Deze naam is het kenmerk dat Intune uit Azure Active Directory (AAD) ophaalt. In Intune wordt de gebruikersnaam die wordt gebruikt door dit profiel dynamisch gegenereerd. Uw opties zijn:
  - **User Principal Name**: Hiermee wordt de naam opgehaald, zoals `user1` of `user1@contoso.com`.
  - **Primair SMTP-adres**: Hiermee haalt u de naam op in e-mailadresindeling, zoals `user1@contoso.com`.
  - **sAM-accountnaam**: Hiervoor is het domein vereist, zoals `domain\user1`. Voer ook in:
    - **Bron van gebruikersdomeinnaam**: Uw opties zijn:
      - **AAD** (Azure Active Directory): Voer **Kenmerk voor gebruikersdomeinnaam uit AAD** in. Kies de optie om de **Volledige domeinnaam** of het kenmerk **NetBIOS-naam** van de gebruiker op te halen.
      - **Aangepast**: Voer de **Te gebruiken aangepaste domeinnaam** in. Voer een waarde in die voor de domeinnaam wordt gebruikt in Intune, zoals `contoso.com` of `contoso`.

- **Kenmerk van het e-mailadres van AAD**: Intune haalt dit kenmerk op uit Azure Active Directory (AAD). Kies op welke manier het e-mailadres voor de gebruiker wordt gegenereerd. Uw opties zijn:
  - **User Principal Name**: De volledige principal-naam wordt gebruikt als het e-mailadres, zoals `user1@contoso.com` of `user1`.
  - **Primair SMTP-adres**: Het primaire SMTP-adres voor aanmelding bij Exchange wordt gebruikt, zoals `user1@contoso.com`.

## <a name="security-settings"></a>Beveiligingsinstellingen

- **SSL**: U kunt deze optie **inschakelen** om SSL-communicatie (Secure Sockets Layer) te gebruiken wanneer u e-mailberichten verzendt, e-mailberichten ontvangt en communiceert met de Exchange-server. Voor **Uitschakelen** is SSL niet vereist.

## <a name="synchronization-settings"></a>Synchronisatie-instellingen

- **Aantal dagen e-mail voor synchronisatie**: Kies het aantal dagen waarvoor u e-mail wilt synchroniseren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Selecteer **Onbeperkt** om alle beschikbare e-mail te synchroniseren.
- **Synchronisatieschema**: Selecteer het schema dat voor apparaten wordt gebruikt om gegevens van de Exchange-server te synchroniseren. U kunt ook **Wanneer berichten binnenkomen** selecteren, zodat gegevens worden gesynchroniseerd zodra ze binnenkomen. Of selecteer **Handmatig** om de synchronisatie te laten starten door de gebruiker van het apparaat.

## <a name="content-sync-settings"></a>Instellingen voor inhoudssynchronisatie

- **Inhoudstype voor synchronisatie**: Selecteer de inhoudstypen die u wilt synchroniseren met apparaten:
  - **Contactpersonen**: Met **Aan** worden de contactpersonen gesynchroniseerd. Met **Uit** worden de contactpersonen niet automatisch gesynchroniseerd. Gebruikers synchroniseren handmatig.
  - **Agenda**: Met **Aan** wordt de agenda gesynchroniseerd. Met **Uit** worden de contactpersonen niet automatisch gesynchroniseerd. Gebruikers synchroniseren handmatig.
  - **Taken**: Met **Aan** worden de taken gesynchroniseerd. Met **Uit** worden de taken niet automatisch gesynchroniseerd. Gebruikers synchroniseren handmatig.

## <a name="next-steps"></a>Volgende stappen

U kunt de e-mailinstellingen ook configureren op [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), [iOS/iPadOS](email-settings-ios.md) en [Windows 10](email-settings-windows-10.md).

[E-mailinstellingen configureren in Intune](email-settings-configure.md).
