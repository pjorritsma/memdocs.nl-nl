---
title: VPN-instellingen toevoegen aan apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Gebruik voor Android-apparaatbeheer-, Android Enterprise-, iOS/iPadOS-, macOS- en Windows-apparaten ingebouwde instellingen voor het maken van VPN-verbindingen (virtueel particulier netwerk) in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c72d2f8d9bd6a7235845863000272f605bb41089
ms.sourcegitcommit: 0f02742301e42daaa30e1bde8694653e1b9e5d2a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/08/2020
ms.locfileid: "82943821"
---
# <a name="create-vpn-profiles-to-connect-to-vpn-servers-in-intune"></a>VPN-profielen maken om verbinding te maken met VPN-servers in Intune

Met virtuele particuliere netwerken (VPN's) geeft u gebruikers veilige externe toegang tot het netwerk van uw organisatie. Apparaten gebruiken een VPN-verbindingsprofiel om een verbinding met de VPN-server op te zetten. Met **VPN-profielen** in Microsoft Intune worden VPN-instellingen toegewezen aan gebruikers en apparaten in uw organisatie, zodat deze gemakkelijk en veilig verbinding met het netwerk van uw organisatie kunnen maken.

U wilt bijvoorbeeld alle iOS/iPadOS-apparaten configureren met de instellingen die vereist zijn om verbinding te maken met een bestandsshare in het netwerk van de organisatie. U maakt een VPN-profiel dat deze instellingen bevat. U wijst dit profiel vervolgens toe aan alle gebruikers die over iOS/iPadOS-apparaten beschikken. De gebruikers zien de VPN-verbinding in de lijst met beschikbare netwerken en kunnen moeiteloos verbinding maken.

> [!NOTE]
> U kunt [aangepast Intune-configuratiebeleid](custom-settings-configure.md) gebruiken om VPN-profielen te maken voor de volgende platformen:
>
> * Android 4 en hoger
> * Geregistreerde apparaten met Windows 8.1 en hoger
> * Windows Phone 8.1 en hoger
> * Geregistreerde apparaten met Windows 10 Desktop
> * Windows 10 Mobile
> * Windows Holographic for Business

## <a name="vpn-connection-types"></a>VPN-verbindingstypen

U kunt VPN-profielen met de volgende verbindingstypen maken:

- Automatisch
  - Windows 10

- Check Point Capsule VPN
  - Android-apparaatbeheerder
  - Android Enterprise-werkprofielen
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Cisco AnyConnect
  - Android-apparaatbeheerder
  - Android Enterprise-werkprofielen
  - Android Enterprise-apparaten in zakelijk eigendom (volledig beheerd)
  - iOS/iPadOS
  - macOS

- Cisco (IPsec)
  - iOS/iPadOS

- Citrix SSO
  - Android-apparaatbeheerder
  - Android Enterprise-werkprofielen: [App-configuratiebeleid](../apps/app-configuration-policies-use-android.md) gebruiken
  - Android Enterprise-apparaateigenaar (volledig beheerd): [App-configuratiebeleid](../apps/app-configuration-policies-use-android.md) gebruiken
  - iOS/iPadOS
  - Windows 10

- Aangepaste VPN
  - iOS/iPadOS
  - macOS

  Maak aangepaste VPN-profielen met behulp van URI-instellingen in [Profielen met aangepaste instellingen maken](custom-settings-configure.md).

- F5-toegang
  - Android-apparaatbeheerder
  - Android Enterprise-werkprofielen
  - Android Enterprise-apparaten in zakelijk eigendom (volledig beheerd)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- IKEv2
  - iOS/iPadOS
  - Windows 10

- L2TP
  - Windows 10

- Palo Alto Networks GlobalProtect
  - Android Enterprise-werkprofielen: [App-configuratiebeleid](../apps/app-configuration-policies-use-android.md) gebruiken
  - iOS/iPadOS
  - Windows 10

- PPTP
  - Windows 10

- Pulse Secure
  - Android-apparaatbeheerder
  - Android Enterprise-werkprofielen
  - Android Enterprise-apparaten in zakelijk eigendom (volledig beheerd)
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- SonicWall Mobile Connect
  - Android-apparaatbeheerder
  - Android Enterprise-werkprofielen
  - iOS/iPadOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Zscaler
  - Android Enterprise-werkprofielen: [App-configuratiebeleid](../apps/app-configuration-policies-use-android.md) gebruiken
  - iOS/iPadOS

> [!IMPORTANT]
> U kunt VPN-profielen die zijn toegewezen aan een apparaat pas gebruiken nadat de betreffende VPN-app voor het profiel is geïnstalleerd. Zie [Wat is appbeheer in Microsoft Intune?](../apps/app-management.md) voor hulp bij het toewijzen van de app met behulp van Intune.  

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Kies het platform van uw apparaten. Uw opties zijn:
      - **Android-apparaatbeheerder**
      - **Alleen Android Enterprise** >  **-apparaateigenaar**
      - **Alleen Android Enterprise** >  **-werkprofiel**
      - **iOS/iPadOS**
      - **macOS**
      - **Windows 10 en hoger**
      - **Windows 8.1 en hoger**
      - **Windows Phone 8.1**
    - **Profiel**: Selecteer **VPN**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **VPN-profiel voor hele bedrijf**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Selecteer uw platform voor gedetailleerde instellingen:

    - [Android-apparaatbeheerder](vpn-settings-android.md)
    - [Android Enterprise](vpn-settings-android-enterprise.md)
    - [iOS/iPadOS](vpn-settings-ios.md)
    - [macOS](vpn-settings-macos.md)
    - [Windows 10](vpn-settings-windows-10.md) (inclusief Windows Holographic for Business)
    - [Windows 8.1](vpn-settings-windows-8-1.md)
    - [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md)

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruiker of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="secure-your-vpn-profiles"></a>Uw VPN-profielen beveiligen

Voor VPN-profielen kan een aantal verschillende verbindingstypen en -protocollen van verschillende fabrikanten worden gebruikt. Deze verbindingen zijn doorgaans beveiligd met een of meer van de volgende methoden.

### <a name="certificates"></a>Certificaten

Wanneer u het VPN-profiel maakt, kiest u een SCEP- of PFX-certificaatprofiel dat u eerder hebt gemaakt in Intune. Dit profiel wordt het identiteitscertificaat genoemd. Dit wordt gebruikt voor verificatie aan de hand van een vertrouwd-certificaatprofiel (of *basiscertificaat*) dat u hebt gemaakt om het apparaat van de gebruiker verbinding te laten maken. Het vertrouwde certificaat wordt toegewezen aan de computer die de VPN-verbinding verifieert. Dit is meestal de VPN-server.

Als u gebruikmaakt van verificatie op basis van certificaten voor uw VPN-profiel, implementeert u het VPN-profiel, het certificaatprofiel en het vertrouwde basisprofiel in dezelfde groepen om ervoor te zorgen dat elk apparaat de geldigheid van uw certificeringsinstantie kan herkennen.

Zie [How to configure certificates with Microsoft Intune](../protect/certificates-configure.md) (Certificaten configureren met Microsoft Intune) voor meer informatie over het gebruiken en maken van certificaatprofielen in Intune.

> [!NOTE]
> Certificaten die zijn toegevoegd met behulp van het profieltype voor **geïmporteerde PKCS-certificaten** worden niet ondersteund voor VPN-verificatie. Certificaten die zijn toegevoegd met behulp van profieltype voor **PKCS-certificaten** worden ondersteund voor VPN-verificatie.


### <a name="user-name-and-password"></a>Gebruikersnaam en wachtwoord

De gebruiker wordt geverifieerd op de VPN-server door een gebruikersnaam en wachtwoord op te geven.

## <a name="next-steps"></a>Volgende stappen

Als het profiel is gemaakt, doet het nog niets. Vervolgens moet u [het profiel toewijzen](device-profile-assign.md) aan apparaten en [de status ervan controleren](device-profile-monitor.md).

U kunt ook VPN's per app maken en gebruiken op [Android-apparaatbeheer/Android Enterprise](android-pulse-secure-per-app-vpn.md)-apparaten en [iOS/iPadOS](vpn-setting-configure-per-app.md)-apparaten.
