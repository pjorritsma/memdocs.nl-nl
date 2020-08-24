---
title: VPN-instellingen gebruiken voor Android-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk alle instellingen voor het maken van VPN-verbindingen op Android-apparaten in Microsoft Intune. Voer de verbindingsnaam, het IP-adres of de FQDN van de VPN-server in, kies de gewenste gebruikersverificatie en kies verbindingstypen voor Citrix, SonicWall, Check Point Capsule en Pulse Secure.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 13d1f65ab9164c20923fa7293b19bc707718d6a7
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146385"
---
# <a name="android-device-settings-to-configure-vpn-in-intune"></a>Instellingen voor Android-apparaten voor het configureren van VPN in Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen die u voor VPN-verbindingen kunt beheren op Android-apparaten. U kunt deze instellingen onder meer gebruiken als onderdeel van uw MDM-oplossing (Mobile Device Management) om een VPN-verbinding te maken, de VPN-verificatiemethode te kiezen en een VPN-servertype te selecteren.

Als Intune-beheerder kunt u VPN-instellingen maken en toewijzen aan Android-apparaten. 

Zie [VPN-profielen](vpn-settings-configure.md) voor meer informatie over VPN-profielen in Intune.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een apparaatconfiguratieprofiel](vpn-settings-configure.md) en kies **Android-apparaatbeheer**.

## <a name="base-vpn"></a>Basis-VPN

- **Verbindingsnaam**: voer een naam voor deze verbinding in. Eindgebruikers zien deze naam wanneer ze op hun apparaat de beschikbare VPN-verbindingen zoeken. Voer bijvoorbeeld `Contoso VPN` in.
- **IP-adres of FQDN**: geef het IP-adres of de FQDN (Fully Qualified Domain Name) op van de VPN-server waarmee apparaten verbinding maken. Voer bijvoorbeeld **192.168.1.1** of **vpn.contoso.com** in.

  - **Verificatiemethode**: kies hoe apparaten worden geverifieerd bij de VPN-server. Uw opties zijn:

    - **Certificaten**: selecteer een bestaand SCEP- of PKCS-certificaatprofiel om de verbinding te verifiëren. [Certificaten configureren](../protect/certificates-configure.md) bevat de stappen voor het maken van een certificaatprofiel.
    - **Gebruikersnaam en wachtwoord**: tijdens het aanmelden bij de VPN-server moeten eindgebruikers hun gebruikersnaam en wachtwoord invoeren.

- **Verbindingstype**: selecteer het type VPN-verbinding. Uw opties zijn:

  - **Check Point Capsule VPN**
  - **Cisco AnyConnect**
  - **SonicWall Mobile Connect**
  - **F5-toegang**
  - **Pulse Secure**
  - **Citrix SSO**

- **Vingerafdruk** (alleen voor VPN Check Point Capsule): geef een tekenreeks op (bijvoorbeeld **Contoso-vingerafdrukcode**) om te verifiëren dat de VPN-server kan worden vertrouwd. Er wordt een vingerafdruk verzonden naar de client zodat deze alle servers vertrouwt die over dezelfde vingerafdruk beschikken. Als het apparaat niet over de vingerafdruk beschikt, wordt de gebruiker gevraagd om de VPN-server te vertrouwen terwijl de vingerafdruk wordt weergegeven. De gebruiker controleert de vingerafdruk handmatig en kiest ervoor om de verbinding te vertrouwen.
- **Sleutel- en waardeparen voor de kenmerken van de Citrix VPN invoeren** (alleen voor Citrix): voer sleutel- en waardeparen in, afkomstig van Citrix. Met deze waarden configureert u de eigenschappen van de VPN-verbinding. 

  U kunt ook een bestand met door komma's gescheiden waarden (.csv) met sleutel- en waardeparen **importeren**. Controleer de eigenschappen **Mijn gegevens bevatten kopteksten** en **Sleutel**.

  Nadat u de sleutel- en waardeparen hebt toegevoegd, gebruikt u **Exporteren** om een back-up van uw gegevens te maken in de vorm van een CSV-bestand.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook VPN-profielen maken voor apparaten met [Android Enterprise](vpn-settings-android-enterprise.md), [iOS/iPadOS](vpn-settings-ios.md), [macOS](vpn-settings-macos.md), [Windows 10 en hoger](vpn-settings-windows-10.md) en [Windows 8.1](vpn-settings-windows-8-1.md).
