---
title: Aangepast VPN per app-profiel voor Android-apparaatbeheerder in Microsoft Intune - Azure | Microsoft Docs
description: Een aangepast profiel voor VPN per app-profielen gebruiken voor Android-apparaatbeheerder met het VPN-verbindingstype Pulse Secure of Citrix in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/22/2020
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
ms.openlocfilehash: 3c8e09b6010f7fc846fd81281053eaaa722e5ef4
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262792"
---
# <a name="use-a-microsoft-intune-custom-profile-to-create-a-per-app-vpn-profile-for-android-devices"></a>Een aangepast Microsoft Intune-profiel gebruiken voor het maken van een VPN-profiel per app voor Android-apparaten

U kunt een VPN-profiel per app maken voor apparaten met Android 5.0 en hoger die worden beheerd met Intune. Maak eerst een VPN-profiel met het verbindingstype Pulse Secure of Citrix. Maak vervolgens een aangepast configuratiebeleid dat het VPN-profiel aan specifieke apps koppelt.

Deze functie is van toepassing op:

- Android-apparaatbeheerder

Als u VPN per app wilt gebruiken op Android Enterprise-apparaten, gebruikt u een [app-configuratiebeleid](../apps/app-configuration-vpn-ae.md). App-configuratiebeleid biedt ondersteuning voor meer VPN-client-apps. Op Android Enterprise-apparaten kunt u de stappen in dit artikel gebruiken. Maar dit wordt niet aangeraden en u bent beperkt tot alleen de VPN-verbindingen Pulse Secure en Citrix.

Nadat u het beleid aan uw Android-apparaat of gebruikersgroepen hebt toegewezen, moeten gebruikers de Pulse Secure- of Citrix-VPN-client starten. De VPN-client staat vervolgens alleen verkeer van de opgegeven apps toe om gebruik te maken van de open VPN-verbinding.

> [!NOTE]
>
> Alleen de verbindingstypen Pulse Secure en Citrix worden ondersteund voor Android-apparaatbeheerders. Gebruik op Android Enterprise-apparaten een [app-configuratiebeleid](../apps/app-configuration-vpn-ae.md).

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

    :::image type="content" source="./media/android-pulse-secure-per-app-vpn/android_per_app_vpn_oma_uri.png" alt-text="Aangepast VPN-beleid per app voor Android-apparaatbeheer in Microsoft Intune":::

### <a name="set-your-blocked-and-allowed-app-list-optional"></a>De lijst met geblokkeerde en toegestane apps instellen (optioneel)

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
