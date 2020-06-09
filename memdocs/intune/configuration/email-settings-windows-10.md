---
title: E-mailinstellingen toevoegen voor Windows 10-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Het e-mailprofiel van een apparaatconfiguratie maken die gebruikmaakt van Exchange-servers en kenmerken ophaalt uit Azure Active Directory. U kunt ook SSL inschakelen en e-mail en schema's synchroniseren op Windows 10-apparaten met behulp van Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0cd3505d0a0067adfe9082d7aa3882f3421a2183
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429608"
---
# <a name="email-profile-settings-for-devices-running-windows-10-in-microsoft-intune"></a>E-mailprofielinstellingen voor apparaten met Windows 10 in Microsoft Intune

U kunt met de e-mailprofielinstellingen de Mail-app op uw apparaten met Windows 10 of later configureren.

## <a name="before-you-begin"></a>Voordat u begint

[Maak het profiel](email-settings-configure.md).

## <a name="email-settings"></a>E-mailinstellingen

- **E-mailserver**: Voer de hostnaam van uw Exchange-server in. Voer bijvoorbeeld `outlook.office365.com` in.
- **Accountnaam**: Voer de weergavenaam voor het e-mailaccount in. Deze naam zien gebruikers op hun apparaat.
- **Het kenmerk Gebruikersnaam van AAD**: Deze naam is het kenmerk dat Intune uit Azure Active Directory (AAD) ophaalt. In Intune wordt de gebruikersnaam die wordt gebruikt door dit profiel dynamisch gegenereerd. Uw opties zijn:
  - **User Principal Name**: Hiermee wordt de naam opgehaald, zoals `user1` of `user1@contoso.com`.
  - **Primair SMTP-adres**: Hiermee haalt u de naam op in e-mailadresindeling, zoals `user1@contoso.com`.
  - **sAM-accountnaam**: Hiervoor is het domein vereist, zoals `domain\user1`. Voer ook in:  
    - **Bron van gebruikersdomeinnaam**: Selecteer **AAD** (Azure Active Directory) of **Aangepast**.

      Wanneer u de kenmerken ophaalt vanuit **AAD**, voert u ook het volgende in:
      - **Het kenmerk Gebruikersdomeinnaam van AAD**: Kies de optie om de **Volledige domeinnaam** of het kenmerk **NetBIOS-naam** van de gebruiker op te halen.

      Wanneer u **aangepaste** kenmerken gebruikt, voert u ook het volgende in:
      - **Te gebruiken aangepaste domeinnaam**: Voer een waarde in die voor de domeinnaam wordt gebruikt in Intune, zoals `contoso.com` of `contoso`.

- **Kenmerk van het e-mailadres van AAD**: Intune haalt dit kenmerk op uit Azure Active Directory (AAD). Kies op welke manier het e-mailadres voor de gebruiker wordt gegenereerd. Uw opties zijn:
  - **User Principal Name**: De volledige principal-naam wordt gebruikt als het e-mailadres, zoals `user1@contoso.com` of `user1`.
  - **Primair SMTP-adres**: Het primaire SMTP-adres voor aanmelding bij Exchange wordt gebruikt, zoals `user1@contoso.com`.

### <a name="security"></a>Beveiliging

- **SSL**: U kunt deze optie **inschakelen** om SSL-communicatie (Secure Sockets Layer) te gebruiken wanneer u e-mailberichten verzendt, e-mailberichten ontvangt en communiceert met de Exchange-server. Voor **Uitschakelen** is SSL niet vereist.

### <a name="synchronization"></a>Synchronisatie

- **Aantal dagen e-mail voor synchronisatie**: Selecteer het aantal dagen waarvoor u e-mail wilt synchroniseren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Selecteer **Onbeperkt** om alle beschikbare e-mail te synchroniseren.
- **Synchronisatieschema**: Selecteer het schema dat voor apparaten wordt gebruikt om gegevens van de Exchange-server te synchroniseren. U kunt ook **Wanneer berichten binnenkomen** selecteren, zodat gegevens worden gesynchroniseerd zodra ze binnenkomen. Of selecteer **Handmatig** om de synchronisatie te laten starten door de gebruiker van het apparaat.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

### <a name="content-sync"></a>Inhoudssynchronisatie

- **Inhoudstype voor synchronisatie**: Selecteer de inhoudstypen die u wilt synchroniseren met apparaten. Uw opties zijn:
  - **Contactpersonen**: Met **Aan** worden de contactpersonen gesynchroniseerd. Met **Uit** worden de contactpersonen niet automatisch gesynchroniseerd. Gebruikers synchroniseren handmatig.
  - **Agenda**: Met **Aan** wordt de agenda gesynchroniseerd. Met **Uit** worden de contactpersonen niet automatisch gesynchroniseerd. Gebruikers synchroniseren handmatig.
  - **Taken**: Met **Aan** worden de taken gesynchroniseerd. Met **Uit** worden de taken niet automatisch gesynchroniseerd. Gebruikers synchroniseren handmatig.

## <a name="next-steps"></a>Volgende stappen

U kunt de e-mailinstellingen ook configureren op [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md)en [iOS/iPadOS](email-settings-ios.md). 

[Meer informatie over de e-mailinstellingen in Intune](email-settings-configure.md).

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).
