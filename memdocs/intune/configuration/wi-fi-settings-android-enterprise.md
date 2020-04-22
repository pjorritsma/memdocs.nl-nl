---
title: Wi-Fi-instellingen voor Android Enterprise- en Kiosk-apparaten - Microsoft Intune | Microsoft Docs
description: Een configuratieprofiel voor een Wi-Fi-apparaat voor Android Enterprise en Android Kiosk maken of toevoegen. Zie de verschillende instellingen, zoals voor het toevoegen van certificaten, voor het kiezen van een EAP-type en het selecteren van een verificatiemethode in Microsoft Intune. Voor Kiosk-apparaten moet u ook de vooraf gedeelde sleutel van uw netwerk opgeven.
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
ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38c3c4adb7029303eaad34b1d5a9fdef774c0f00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086433"
---
# <a name="add-wi-fi-settings-for-android-enterprise-dedicated-and-fully-managed-devices-in-microsoft-intune"></a>Wi-Fi-instellingen toevoegen voor volledig beheerde en toegewezen Android Enterprise-apparaten in Microsoft Intune

U kunt een profiel maken met specifieke wifi-instellingen en dit profiel vervolgens implementeren op uw volledig beheerde en toegewezen Android Enterprise-apparaten. Microsoft Intune bevat veel functies, waaronder het verifiëren bij uw netwerk, het gebruik van een vooraf gedeelde sleutel en meer.

In dit artikel worden deze instellingen beschreven. [Wi-Fi gebruiken op uw apparaten](wi-fi-settings-configure.md) bevat meer informatie over de Wi-Fi-functie in Microsoft Intune.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een apparaatprofiel](wi-fi-settings-configure.md).

## <a name="device-owner-only"></a>Alleen eigenaar van het apparaat

Selecteer deze optie als u implementeert op een volledig beheerd of toegewezen Android Enterprise-apparaat.  Volledig beheerde en toegewezen Android Enterprise-apparaten ondersteunen momenteel de implementatie van SCEP-certificaten, maar niet van PKCS.

### <a name="basic"></a>Basic

- **Wi-Fi-type**: kies **Basic**.
- **Netwerknaam**: voer een naam in voor deze Wi-Fi-verbinding. Eindgebruikers zien deze naam wanneer ze op hun apparaat beschikbare wifi-verbindingen zoeken. Voer bijvoorbeeld **Contoso WiFi** in.
- **SSID**: voer de **serviceset-id** in, wat de echte naam is van het draadloze netwerk waarmee apparaten verbinding maken. Gebruikers zien echter alleen de **netwerknaam** die u hebt geconfigureerd wanneer ze de verbinding kiezen.
- **Verborgen netwerk**: kies **Inschakelen** om te voorkomen dat dit netwerk op het apparaat wordt weergegeven in de lijst met beschikbare netwerken. De SSID wordt niet verzonden. Kies **Uitschakelen** om dit netwerk in de lijst met beschikbare netwerken op het apparaat weer te geven.
- **Wi-Fi-type**: selecteer het beveiligingsprotocol voor de verificatie bij het Wi-Fi-netwerk. Uw opties zijn:

  - **Open (geen verificatie)** : gebruik deze optie alleen als het netwerk niet beveiligd is.
  - **Vooraf gedeelde WEP-sleutel**: typ het wachtwoord bij **Vooraf gedeelde sleutel**. Wanneer het netwerk van uw organisatie is ingesteld of geconfigureerd, wordt er ook een wachtwoord of netwerksleutel geconfigureerd. Voer dit wachtwoord of deze netwerksleutel in voor de PSK-waarde.
  - **Vooraf gedeelde WPA-sleutel**: typ het wachtwoord bij **Vooraf gedeelde sleutel**. Wanneer het netwerk van uw organisatie is ingesteld of geconfigureerd, wordt er ook een wachtwoord of netwerksleutel geconfigureerd. Voer dit wachtwoord of deze netwerksleutel in voor de PSK-waarde.

### <a name="enterprise"></a>Enterprise

- **Wi-Fi-type**: kies **Enterprise**.
- **SSID**: voer de **serviceset-id** in, wat de echte naam is van het draadloze netwerk waarmee apparaten verbinding maken. Gebruikers zien echter alleen de **netwerknaam** die u hebt geconfigureerd wanneer ze de verbinding kiezen.
- **Verborgen netwerk**: kies **Inschakelen** om te voorkomen dat dit netwerk op het apparaat wordt weergegeven in de lijst met beschikbare netwerken. De SSID wordt niet verzonden. Kies **Uitschakelen** om dit netwerk in de lijst met beschikbare netwerken op het apparaat weer te geven.
- **EAP-type**: kies het type Extensible Authentication Protocol (EAP) dat wordt gebruikt om beveiligde draadloze verbindingen te verifiëren. Uw opties zijn:

  - **EAP-TLS**: voer ook het volgende in:

    - **Vertrouwelijke server** - **Basiscertificaat voor servervalidatie**: kies een profiel voor een bestaand vertrouwd basiscertificaat. Wanneer de client verbinding met het netwerk maakt, wordt dit certificaat aan de server aangeboden en gebruikt om de verbinding te verifiëren.

    - **Clientverificatie** - **Clientcertificaat voor clientverificatie (identiteitscertificaat)** : kies het profiel van het SCEP-clientcertificaat dat ook op het apparaat wordt geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.

    - **Identiteitsprivacy (externe identiteit)** : voer de tekst in die wordt verzonden als reactie op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

  - **EAP-TTLS**: voer ook het volgende in:

    - **Vertrouwelijke server** - **Basiscertificaat voor servervalidatie**: kies een profiel voor een bestaand vertrouwd basiscertificaat. Wanneer de client verbinding met het netwerk maakt, wordt dit certificaat aan de server aangeboden en gebruikt om de verbinding te verifiëren.

    - **Clientverificatie**: Kies een **verificatiemethode**. Uw opties zijn:

      - **Gebruikersnaam en wachtwoord**: de gebruiker wordt gevraagd om een gebruikersnaam en wachtwoord om de verbinding te verifiëren. Voer ook in:
        - **Niet-EAP-methode (interne identiteit)** : kies hoe u de verbinding verifieert. Zorg ervoor dat u hetzelfde protocol kiest dat op uw Wi-Fi-netwerk is geconfigureerd. Uw opties zijn:

          - **Niet-versleuteld wachtwoord (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP versie 2 (MS-CHAP v2)**

      - **Certificaten**: kies het profiel van het SCEP-clientcertificaat dat ook op het apparaat is geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.

      - **Identiteitsprivacy (externe identiteit)** : voer de tekst in die wordt verzonden als reactie op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

  - **PEAP**: voer ook het volgende in:

    - **Vertrouwelijke server** - **Basiscertificaat voor servervalidatie**: kies een profiel voor een bestaand vertrouwd basiscertificaat. Wanneer de client verbinding met het netwerk maakt, wordt dit certificaat aan de server aangeboden en gebruikt om de verbinding te verifiëren.

    - **Clientverificatie**: Kies een **verificatiemethode**. Uw opties zijn:

      - **Gebruikersnaam en wachtwoord**: de gebruiker wordt gevraagd om een gebruikersnaam en wachtwoord om de verbinding te verifiëren. Voer ook in:
        - **Niet-EAP-methode voor verificatie (interne identiteit)** : kies hoe u de verbinding verifieert. Zorg ervoor dat u hetzelfde protocol kiest dat op uw Wi-Fi-netwerk is geconfigureerd. Uw opties zijn:

          - **Geen**
          - **Microsoft CHAP versie 2 (MS-CHAP v2)**

      - **Certificaten**: kies het profiel van het SCEP-clientcertificaat dat ook op het apparaat is geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.

      - **Identiteitsprivacy (externe identiteit)** : voer de tekst in die wordt verzonden als reactie op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

## <a name="work-profile-only"></a>Alleen werkprofiel

### <a name="basic"></a>Basic

- **Wi-Fi-type**: kies **Basic**.
- **SSID**: voer de **serviceset-id** in, wat de echte naam is van het draadloze netwerk waarmee apparaten verbinding maken. Gebruikers zien echter alleen de **netwerknaam** die u hebt geconfigureerd wanneer ze de verbinding kiezen.
- **Verborgen netwerk**: kies **Inschakelen** om te voorkomen dat dit netwerk op het apparaat wordt weergegeven in de lijst met beschikbare netwerken. De SSID wordt niet verzonden. Kies **Uitschakelen** om dit netwerk in de lijst met beschikbare netwerken op het apparaat weer te geven.

### <a name="enterprise"></a>Enterprise

- **Wi-Fi-type**: kies **Enterprise**.
- **SSID**: voer de **serviceset-id** in, wat de echte naam is van het draadloze netwerk waarmee apparaten verbinding maken. Gebruikers zien echter alleen de **netwerknaam** die u hebt geconfigureerd wanneer ze de verbinding kiezen.
- **Verborgen netwerk**: kies **Inschakelen** om te voorkomen dat dit netwerk op het apparaat wordt weergegeven in de lijst met beschikbare netwerken. De SSID wordt niet verzonden. Kies **Uitschakelen** om dit netwerk in de lijst met beschikbare netwerken op het apparaat weer te geven.
- **EAP-type**: kies het type Extensible Authentication Protocol (EAP) dat wordt gebruikt om beveiligde draadloze verbindingen te verifiëren. Uw opties zijn:

  - **EAP-TLS**: voer ook het volgende in:

    - **Vertrouwelijke server** - **Basiscertificaat voor servervalidatie**: kies een profiel voor een bestaand vertrouwd basiscertificaat. Wanneer de client verbinding met het netwerk maakt, wordt dit certificaat aan de server aangeboden en gebruikt om de verbinding te verifiëren.

    - **Clientverificatie** - **Clientcertificaat voor clientverificatie (identiteitscertificaat)** : kies het profiel van het SCEP- of PKCS-clientcertificaat dat ook op het apparaat wordt geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.

    - **Identiteitsprivacy (externe identiteit)** : voer de tekst in die wordt verzonden als reactie op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

  - **EAP-TTLS**: voer ook het volgende in:

    - **Vertrouwelijke server** - **Basiscertificaat voor servervalidatie**: kies een profiel voor een bestaand vertrouwd basiscertificaat. Wanneer de client verbinding met het netwerk maakt, wordt dit certificaat aan de server aangeboden en gebruikt om de verbinding te verifiëren.

    - **Clientverificatie**: Kies een **verificatiemethode**. Uw opties zijn:

      - **Gebruikersnaam en wachtwoord**: de gebruiker wordt gevraagd om een gebruikersnaam en wachtwoord om de verbinding te verifiëren. Voer ook in:
        - **Niet-EAP-methode (interne identiteit)** : kies hoe u de verbinding verifieert. Zorg ervoor dat u hetzelfde protocol kiest dat op uw Wi-Fi-netwerk is geconfigureerd. Uw opties zijn:

          - **Niet-versleuteld wachtwoord (PAP)**
          - **Microsoft CHAP (MS-CHAP)**
          - **Microsoft CHAP versie 2 (MS-CHAP v2)**

      - **Certificaten**: kies het profiel van het SCEP- of PKCS-clientcertificaat dat ook op het apparaat is geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.

      - **Identiteitsprivacy (externe identiteit)** : voer de tekst in die wordt verzonden als reactie op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

  - **PEAP**: voer ook het volgende in:

    - **Vertrouwelijke server** - **Basiscertificaat voor servervalidatie**: kies een profiel voor een bestaand vertrouwd basiscertificaat. Wanneer de client verbinding met het netwerk maakt, wordt dit certificaat aan de server aangeboden en gebruikt om de verbinding te verifiëren.

    - **Clientverificatie**: Kies een **verificatiemethode**. Uw opties zijn:

      - **Gebruikersnaam en wachtwoord**: de gebruiker wordt gevraagd om een gebruikersnaam en wachtwoord om de verbinding te verifiëren. Voer ook in:
        - **Niet-EAP-methode voor verificatie (interne identiteit)** : kies hoe u de verbinding verifieert. Zorg ervoor dat u hetzelfde protocol kiest dat op uw Wi-Fi-netwerk is geconfigureerd. Uw opties zijn:

          - **Geen**
          - **Microsoft CHAP versie 2 (MS-CHAP v2)**

      - **Certificaten**: kies het profiel van het SCEP- of PKCS-clientcertificaat dat ook op het apparaat is geïmplementeerd. Dit certificaat is de identiteit die door het apparaat wordt gepresenteerd aan de server om de verbinding te verifiëren.

      - **Identiteitsprivacy (externe identiteit)** : voer de tekst in die wordt verzonden als reactie op een EAP-identiteitsaanvraag. Deze tekst kan elke waarde hebben, zoals `anonymous`. Tijdens verificatie wordt deze anonieme identiteit in eerste instantie verzonden en wordt deze gevolgd door de echte identificatie in een beveiligde tunnel.

- **Proxy-instellingen**: geef de proxyconfiguratie op die door uw organisatie wordt gebruikt. Uw opties zijn:

  - **Geen** : u gebruikt geen proxyserver.
  - **Automatisch**: selecteer deze optie om de instelling *URL van proxyserver* beschikbaar te maken, waarmee u uw proxyserver of een PAC-bestand (Proxy Auto-Configuration) kunt opgeven dat een lijst met uw proxyservers bevat.

- **URL van proxyserver**: deze instelling is beschikbaar wanneer u *Proxyinstellingen* instelt op *Automatisch*. Geef een van de volgende opties op om apparaten naar uw proxyserver te leiden:

  - IP-adres. bijvoorbeeld `10.0.0.11`
  - Een URL. Bijvoorbeeld `http://proxyserver.contoso.com`.
  - De URL van een PAC-bestand (Proxy Auto-Configuration). Bijvoorbeeld: `http://proxy.contoso.com/proxy.pac`.

  Zie [PAC-bestand (Proxy Auto-Configuration)](https://developer.mozilla.org/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file) (hiermee opent u een niet-Microsoft-site) voor meer informatie over PAC-bestanden.

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt niets. Vervolgens moet u [dit profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

U kunt ook Wi-Fi-profielen maken voor apparaten met [Android](wi-fi-settings-android.md), [iOS/iPadOS](wi-fi-settings-ios.md), [macOS](wi-fi-settings-macos.md), [Windows 10](wi-fi-settings-windows.md) en [Windows 8.1](wi-fi-settings-import-windows-8-1.md).
