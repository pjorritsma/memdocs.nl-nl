---
title: VPN-instellingen configureren voor Windows 8.1-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Maak een VPN-configuratieprofiel (virtueel particulier netwerk) of voeg dit toe met behulp van VPN-configuratie-instellingen, zoals de verbindingsgegevens en de proxyinstellingen met het IP- of FQDN-adres, en de TCP-poort in Microsoft Intune op apparaten met Windows 8.1.
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
ms.openlocfilehash: 2c80bf57b195d7e97308ba423c9e5b53f7e29c74
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086475"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>VPN-instellingen toevoegen op Windows 8.1-apparaten in Microsoft Intune

In dit artikel leest u meer over de Intune-instellingen die u kunt gebruiken om VPN-verbindingen op apparaten met Windows 8.1. te configureren.

Afhankelijk van de instellingen die u kiest, kunnen niet alle waarden in de volgende lijst worden geconfigureerd.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een apparaatconfiguratieprofiel](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Basis-VPN-instellingen

- **Alle instellingen alleen toepassen op Windows 8.1**: Configureer deze instelling in de klassieke Intune-portal. In het Microsoft Endpoint Manager-beheercentrum kan deze instelling niet worden gewijzigd. Als de instelling is ingesteld op **Geconfigureerd**, worden de instellingen alleen toegepast op Windows 8.1-apparaten. Als de instelling is ingesteld op **Niet geconfigureerd**, gelden deze instellingen ook voor Windows 10-apparaten.
- **Verbindingsnaam**: Voer een naam in voor deze verbinding. Gebruikers zien deze naam wanneer ze op hun apparaat in de lijst met beschikbare VPN-verbindingen zoeken.
- **Servers**: Voeg een of meer VPN-servers toe waarmee de apparaten verbinding maken.
  - **Toevoegen**: Hiermee opent u het deelvenster **Rij toevoegen** waar u de volgende informatie kunt opgeven:
    - **Beschrijving**: Geef een beschrijvende naam op voor de server, zoals **Contoso VPN-server**.
    - **IP-adres of FQDN**: Geef het IP-adres of de Fully Qualified Domain Name (FQDN) op van de VPN-server waarmee apparaten verbinding maken. Voorbeelden: **192.168.1.1**, **vpn.contoso.com**.
    - **Standaardserver**: Hiermee wordt deze server ingeschakeld als de standaardserver die apparaten gebruiken om de verbinding te maken. U kunt slechts één server als standaard instellen.
  - **Importeren**: Blader naar een bestand met een door komma's gescheiden lijst met servers in de indeling: beschrijving, IP-adres of FQDN, standaardserver. Kies **OK** om deze servers te importeren in de lijst met **servers**.
  - **Exporteren**: Hiermee exporteert u de lijst met servers naar een bestand met door komma's gescheiden waarden (CSV-bestand).

- **Type verbinding**: Selecteer het type VPN-verbinding in de volgende lijst met leveranciers:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Aanmeldingsgroep of domein** (alleen SonicWall Mobile Connect): Geef de naam op van de aanmeldingsgroep of het aanmeldingsdomein waarmee u verbinding wilt maken.

- **Rol** (alleen Pulse Secure): Geef de naam op van de gebruikersrol die toegang tot deze verbinding heeft. Een gebruikersrol definieert persoonlijke instellingen en opties en schakelt bepaalde toegangsfuncties in of uit.

- **Realm** (alleen Pulse Secure): Geef de naam op van de verificatierealm die u wilt gebruiken. Een verificatierealm is een groepering van verificatieresources die worden gebruikt door het verbindingstype Pulse Secure.

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

- **Proxy-instellingen automatisch detecteren**: Als de VPN-server een proxyserver voor de verbinding vereist, geeft u op of u wilt dat apparaten de verbindingsinstellingen automatisch detecteren.
- **Script voor automatische configuratie**: Gebruik een bestand om de proxyserver te configureren. Voer de **URL van de proxyserver** in die het configuratiebestand bevat. Voer bijvoorbeeld `http://proxy.contoso.com` in.
- **Proxyserver gebruiken**: Schakel deze optie in als u de proxyserverinstellingen handmatig wilt invoeren.
  - **Adres**: Voer het adres van de proxyserver in (als een IP-adres).
  - **Poortnummer**: Voer het poortnummer in dat is gekoppeld aan de proxyserver.
- **Proxy niet gebruiken voor lokale adressen**: Als voor de VPN-server een proxyserver voor de verbinding is vereist en u de proxyserver niet wilt gebruiken voor lokale adressen die u opgeeft, selecteert u deze optie.

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt nog niets. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

Configureer VPN-instellingen op apparaten met [Android](vpn-settings-android.md), [Android Enterprise](vpn-settings-android-enterprise.md), [macOS](vpn-settings-macos.md) en [Windows 10](vpn-settings-windows-10.md).
