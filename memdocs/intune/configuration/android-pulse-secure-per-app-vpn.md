---
title: Aangepast VPN-profiel per app voor Android in Microsoft Intune - Azure | Microsoft Docs
description: Meer informatie over het maken van een VPN-profiel per app maken voor Android-apparaatbeheer-apparaten die worden beheerd met Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d035ebf5-85f4-4001-a249-75d24325061a
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 367ac927650ebf08c245b1ff554ad01db3bf3792
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990157"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Een aangepast Microsoft Intune-profiel gebruiken voor het maken van een VPN-profiel per app voor Android-apparaten

U kunt een VPN-profiel per app maken voor apparaten met Android 5.0 en hoger die worden beheerd met Intune. Maak eerst een VPN-profiel met het verbindingstype Pulse Secure of Citrix. Maak vervolgens een aangepast configuratiebeleid dat het VPN-profiel aan specifieke apps koppelt.

> [!NOTE]
> Als u VPN per app wilt gebruiken op Android Enterprise-apparaten, kunt u deze stappen ook gebruiken. Het is echter raadzaam een [app-configuratiebeleid te gebruiken](../apps/app-configuration-policies-use-android.md) voor uw VPN-client-app.

Nadat u het beleid aan uw Android-apparaat of gebruikersgroepen hebt toegewezen, moeten gebruikers de Pulse Secure- of Citrix-VPN-client starten. De VPN-client staat vervolgens alleen verkeer van de opgegeven apps toe om gebruik te maken van de open VPN-verbinding.

> [!NOTE]
>
> Alleen de verbindingstypen Pulse Secure en Citrix worden ondersteund voor dit profiel.

## <a name="step-1-create-a-vpn-profile"></a>Stap 1: Een VPN-profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Selecteer **Android-apparaatbeheer**.
    - **Profiel**: Selecteer **VPN**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **Android-apparaatbeheer VPN-profiel per app voor apps voor hele bedrijf**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Configureer in **configuratie-instellingen**de gewenste instellingen in het profiel:

    - [VPN-instellingen voor Android-apparaatbeheer-apparaten](vpn-settings-android.md).

    Noteer de waarde die u voor **Naam van de verbinding** invoert wanneer u het VPN-profiel maakt. Deze naam is nodig tijdens de volgend stap. In dit voorbeeld is de naam van de verbinding **MyAppVpnProfile**.

8. Selecteer **Volgende**en ga door met het maken van uw profiel. Zie [Een VPN-profiel maken](vpn-settings-configure.md#create-the-profile) voor meer informatie.

## <a name="step-2-create-a-custom-configuration-policy"></a>Stap 2: Een aangepast configuratiebeleid maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het aangepaste profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **Aangepast OMA-URI Android VPN-profiel voor hele bedrijf**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Selecteer **Android-apparaatbeheer**.
    - **Profieltype**: Selecteer **Aangepast**.

4. Kies **Instellingen** > **Configureren**.
5. Kies **Toevoegen** in het deelvenster **Aangepaste OMA-URI-instellingen**.
    - **Naam**: Voer een naam voor de instelling in.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
    - **OMA-URI**: Voer `./Vendor/MSFT/VPN/Profile/*Name*/PackageList` in, waarbij *Naam* de naam is van de verbinding die u in stap 1 hebt genoteerd. In dit voorbeeld is de tekenreeks `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/PackageList`.
    - **Gegevenstype**: Voer **Tekenreeks** in.
    - **Waarde**: Voer een lijst met door puntkomma's gescheiden pakketten in om aan het profiel te koppelen. Als u bijvoorbeeld wilt dat Excel en de Google Chrome-browser de VPN-verbinding gebruiken, voert u `com.microsoft.office.excel;com.android.chrome` in.

    > [!div class="mx-imgBorder"]
    >![Voorbeeld van een aangepast VPN-beleid per app voor Android-apparaatbeheer](./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png)

### <a name="set-your-app-list-to-blacklist-or-whitelist-optional"></a>Uw lijst met apps instellen als een blacklist of whitelist (optioneel)

Gebruik de waarde **BLACKLIST** om een lijst met apps in te voeren die de VPN-verbinding *niet* mogen gebruiken. Alle andere apps kunnen verbinding maken via de VPN. Of gebruik de waarde **WHITELIST** om een lijst met apps in te voeren die de VPN-verbinding *wel* mogen gebruiken. Apps die niet in de lijst staan, kunnen geen verbinding via de VPN maken.

1. Kies **Toevoegen** in het deelvenster **Aangepaste OMA-URI-instellingen**.
2. Geef een naam op voor de instelling.
3. Voer in **OMA-URI-** `./Vendor/MSFT/VPN/Profile/*Name*/Mode` in, waarbij *Naam* de naam is van het VPN-profiel dat u in stap 1 hebt genoteerd. In dit voorbeeld is de tekenreeks `./Vendor/MSFT/VPN/Profile/MyAppVpnProfile/Mode`.
4. Voer in **Gegevenstype** **Tekenreeks** in.
5. Geef voor **Waarde** **BLACKLIST** of **WHITELIST** op.

## <a name="step-3-assign-both-policies"></a>Stap 3: Beide beleidsregels toewijzen

[Wijs beide apparaatprofielen toe](device-profile-assign.md) aan de vereiste gebruikers of apparaten.

## <a name="next-steps"></a>Volgende stappen

- Zie [Android device settings to configure VPN](vpn-settings-android.md) (Android-apparaatinstellingen voor het configureren van VPN) voor een lijst met alle VPN-instellingen voor Android-apparaatbeheer.
- Zie [VPN-instellingen configureren in Microsoft Intune](vpn-settings-configure.md) voor meer informatie over VPN-instellingen en Intune.
