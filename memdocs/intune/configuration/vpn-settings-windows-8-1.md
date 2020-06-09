---
title: VPN-instellingen configureren voor Windows 8.1-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Maak een VPN-configuratieprofiel (virtueel particulier netwerk) of voeg dit toe met behulp van VPN-configuratie-instellingen, zoals de verbindingsgegevens en de proxyinstellingen met het IP- of FQDN-adres, en de TCP-poort in Microsoft Intune op apparaten met Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556350"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>VPN-instellingen toevoegen op Windows 8.1-apparaten in Microsoft Intune

In dit artikel leest u meer over de Intune-instellingen die u kunt gebruiken om VPN-verbindingen op apparaten met Windows 8.1. te configureren.

Afhankelijk van de instellingen die u kiest, kunnen niet alle waarden in de volgende lijst worden geconfigureerd.

## <a name="before-you-begin"></a>Voordat u begint

[Een Windows 8.1 VPN-apparaatconfiguratieprofiel maken](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Basis-VPN-instellingen

- **Verbindingsnaam**: Voer een naam in voor deze verbinding. Gebruikers zien deze naam wanneer ze op hun apparaat in de lijst met beschikbare VPN-verbindingen zoeken. Voer bijvoorbeeld `Contoso VPN` in.
- **Servers**: Voeg een of meer VPN-servers toe waarmee de apparaten verbinding maken. Als u een server toevoegt, voert u de volgende gegevens in:
  - **Beschrijving**: Voer een beschrijvende naam in voor de server, zoals **Contoso VPN-server**.
  - **IP-adres of FQDN**: geef het IP-adres of de FQDN (Fully Qualified Domain Name) op van de VPN-server waarmee apparaten verbinding maken. Voer bijvoorbeeld `192.168.1.1` of `vpn.contoso.com` in.
  - **Standaardserver**: met **Waar** wordt deze server ingeschakeld als de standaardserver die apparaten gebruiken om de verbinding te maken. U kunt slechts één server als standaard instellen.
  - **Importeren**: blader naar een bestand met een door komma's gescheiden lijst met servers in de indeling: beschrijving, IP-adres of FQDN, standaardserver. Kies **OK** om deze servers te importeren in de lijst met **servers**.
  - **Exporteren**: Hiermee exporteert u de lijst met servers naar een bestand met door komma's gescheiden waarden (CSV-bestand).

- **Type verbinding**: selecteer het type van de VPN-verbinding. Uw opties zijn:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Aanmeldingsgroep of domein** (alleen SonicWall Mobile Connect): voer de naam in van de aanmeldingsgroep of het aanmeldingsdomein waarmee u verbinding wilt maken.

- **Rol** (alleen Pulse Secure): voer de naam in van de gebruikersrol die toegang tot deze verbinding heeft. Een gebruikersrol definieert persoonlijke instellingen en opties en schakelt bepaalde toegangsfuncties in of uit.

- **Realm** (alleen Pulse Secure): voer de naam in van de verificatierealm die u wilt gebruiken. Een verificatierealm is een groepering van verificatieresources die worden gebruikt door het verbindingstype Pulse Secure.

- **Aangepaste XML**: Geef aangepaste XML-opdrachten op waarmee de VPN-verbinding wordt geconfigureerd.

  **Voorbeeld van Pulse Secure**:

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **Voorbeeld van CheckPoint Mobile VPN**:

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **Voorbeeld van SonicWall Mobile Connect**:

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **Voorbeeld van F5 Edge Client**:

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  Raadpleeg de VPN-documentatie van de fabrikant voor meer informatie over het schrijven van aangepaste XML-opdrachten.

- **Split tunneling**: Met **Inschakelen** bepalen apparaten op basis van het verkeer welke verbinding moet worden gebruikt. Een gebruiker in een hotel gebruikt bijvoorbeeld de VPN-verbinding voor werkbestanden, maar het standaardnetwerk van het hotel om gewoon op het web te surfen. Selecteer **Uitschakelen** als u wilt afdwingen dat al het verkeer de VPN-tunnel gebruikt wanneer de VPN-verbinding actief is.

## <a name="proxy-settings"></a>Proxyinstellingen

- **Script voor automatische configuratie**: Gebruik een bestand om de proxyserver te configureren. Voer de **URL van de proxyserver** in die het configuratiebestand bevat. Voer bijvoorbeeld `http://proxy.contoso.com` in.
- **Adres**: voer het adres van de proxyserver in, zoals een IP-adres of `vpn.contoso.com`.
- **Poortnummer**: voer het TCP-poortnummer in dat wordt gebruikt voor uw proxyserver.
- **Proxy-instellingen automatisch detecteren**: Als de VPN-server een proxyserver voor de verbinding vereist, kiest u of u wilt dat apparaten de verbindingsinstellingen automatisch detecteren. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Inschakelen**: de verbindingsinstellingen worden automatisch gedetecteerd.
  - **Uitschakelen**: de verbindingsinstellingen worden niet automatisch gedetecteerd.
- **Proxy niet gebruiken voor lokale adressen**: bypass instellen voor de proxyserver voor lokale adressen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Inschakelen**: geen proxyserver gebruiken voor lokale adressen.
  - **Uitschakelen**: een proxyserver gebruiken voor lokale adressen.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

Configureer VPN-instellingen op apparaten met [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md) en [Windows 10](vpn-settings-windows-10.md).
