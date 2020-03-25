---
title: VPN-instellingen gebruiken voor Android Enterprise in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk alle instellingen voor het maken van VPN-verbindingen op Android Enterprise-apparaten in Microsoft Intune. Voer de verbindingsnaam, het IP-adres of de FQDN van de VPN-server in, kies de gewenste gebruikersverificatie en kies verbindingstypen voor Citrix, SonicWall, Check Point Capsule en Pulse Secure.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8bc627e7b9efb68e8d5cb777b5d8e659b06cab92
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086810"
---
# <a name="android-enterprise-device-settings-to-configure-vpn-in-intune"></a>Instellingen voor Android Enterprise-apparaten voor het configureren van VPN in Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen die u voor VPN-verbindingen kunt beheren op Android Enterprise-apparaten. U kunt deze instellingen onder meer gebruiken als onderdeel van uw MDM-oplossing (Mobile Device Management) om een VPN-verbinding te maken, de VPN-verificatiemethode te kiezen en een VPN-servertype te selecteren.

Als Intune-beheerder kunt u VPN-instellingen maken en toewijzen aan Android Enterprise-apparaten. 

Zie [VPN-profielen](vpn-settings-configure.md) voor meer informatie over VPN-profielen in Intune.

> [!NOTE]
> Als u VPN altijd ingeschakeld wilt configureren, moet u een VPN-profiel maken en ook een profiel voor [apparaatbeperkingen](device-restrictions-android-for-work.md#connectivity) waarvoor de instelling VPN altijd ingeschakeld is geconfigureerd.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een apparaatconfiguratieprofiel](vpn-settings-configure.md) en kies **Android Enterprise**.

## <a name="device-owner-only"></a>Alleen eigenaar van het apparaat

- **Verbindingsnaam**: Voer een naam in voor deze verbinding. Eindgebruikers zien deze naam wanneer ze op hun apparaat de beschikbare VPN-verbindingen zoeken. Voer bijvoorbeeld `Contoso VPN` in.
- **IP-adres of FQDN**: geef het IP-adres of de FQDN (Fully Qualified Domain Name) op van de VPN-server waarmee apparaten verbinding maken. Voer bijvoorbeeld **192.168.1.1** of **vpn.contoso.com** in.

  - **Verificatiemethode**: kies hoe apparaten worden geverifieerd bij de VPN-server. Uw opties zijn:
  
    - **Certificaten**: selecteer een bestaand SCEP- of PKCS-certificaatprofiel om de verbinding te verifiëren. [Certificaten configureren](../protect/certificates-configure.md) bevat de stappen voor het maken van een certificaatprofiel.
    - **Gebruikersnaam en wachtwoord**: Tijdens het aanmelden bij de VPN-server wordt de eindgebruikers gevraagd hun gebruikersnaam en wachtwoord in te voeren.

- **Type verbinding**: selecteer het type van de VPN-verbinding. Uw opties zijn:

  - **Cisco AnyConnect**
  - **F5-toegang**
  - **Pulse Secure**

## <a name="work-profile-only"></a>Alleen werkprofiel

- **Verbindingsnaam**: Voer een naam in voor deze verbinding. Eindgebruikers zien deze naam wanneer ze op hun apparaat de beschikbare VPN-verbindingen zoeken. Voer bijvoorbeeld `Contoso VPN` in.
- **IP-adres of FQDN**: geef het IP-adres of de FQDN (Fully Qualified Domain Name) op van de VPN-server waarmee apparaten verbinding maken. Voer bijvoorbeeld **192.168.1.1** of **vpn.contoso.com** in.

  - **Verificatiemethode**: kies hoe apparaten worden geverifieerd bij de VPN-server. Uw opties zijn:
  
    - **Certificaten**: selecteer een bestaand SCEP- of PKCS-certificaatprofiel om de verbinding te verifiëren. [Certificaten configureren](../protect/certificates-configure.md) bevat de stappen voor het maken van een certificaatprofiel.
    - **Gebruikersnaam en wachtwoord**: Tijdens het aanmelden bij de VPN-server wordt de eindgebruikers gevraagd hun gebruikersnaam en wachtwoord in te voeren.

- **Type verbinding**: selecteer het type van de VPN-verbinding. Uw opties zijn:

  - **Cisco AnyConnect**
  - **F5-toegang**
  - **Pulse Secure**
  - **SonicWall Mobile Connect**
  - **Check Point Capsule VPN**

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook VPN-profielen maken voor apparaten met [Android](vpn-settings-android.md), [iOS/iPadOS](vpn-settings-ios.md), [macOS](vpn-settings-macos.md), [Windows 10 en hoger](vpn-settings-windows-10.md), [Windows 8.1](vpn-settings-windows-8-1.md) en [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md).
