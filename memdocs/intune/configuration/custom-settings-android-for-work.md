---
title: Aangepaste instellingen toevoegen aan Android Enterprise-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Een aangepast profiel voor Android Enterprise-apparaten toevoegen of maken om aangepaste instellingen te maken in Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4724d6e5-05e5-496c-9af3-b74f083141f8
ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 827b5eb8b65aa59212b9ef990def3c5f191baf7c
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "79334428"
---
# <a name="use-custom-settings-for-android-enterprise-devices-in-microsoft-intune"></a>Aangepaste instellingen gebruiken voor Android Enterprise-apparaten in Microsoft Intune

Met Microsoft Intune kunt u met behulp van een 'aangepast profiel' aangepaste instellingen toevoegen of maken voor uw apparaten met een Android Enterprise-werkprofiel. Aangepaste profielen zijn een functie in Intune. Ze zijn ontworpen om apparaatinstellingen en -functies toe te voegen die niet in Intune zijn ingebouwd.

In aangepaste profielen voor Android Enterprise worden OMA-URI-instellingen (Open Mobile Alliance Uniform Resource Identifier) gebruikt om functies op Android Enterprise-apparaten te beheren. Deze instellingen worden doorgaans gebruikt door fabrikanten van mobiele apparaten om deze functies te beheren.

Intune biedt ondersteuning voor het volgende beperkte aantal aangepaste Android Enterprise-profielen:

- ./Vendor/MSFT/WiFi/Profile/SSID/Settings: In [Een Wi-Fi-profiel maken met een vooraf gedeelde sleutel](wi-fi-profile-shared-key.md) vindt u enkele voorbeelden.
- ./Vendor/MSFT/VPN/Profile/Name/PackageList: In [Een profiel voor VPN per app maken](android-pulse-secure-per-app-vpn.md) vindt u enkele voorbeelden.
- ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste: Zie het [voorbeeld](#example) in dit artikel. Deze instelling is ook beschikbaar in de gebruikersinterface. Zie [Android Enterprise-apparaatinstellingen voor beheer van functies](device-restrictions-android-for-work.md) voor meer informatie.

Raadpleeg [OEMConfig voor Android Enterprise](android-oem-configuration-overview.md) als u aanvullende instellingen nodig hebt.

In dit artikel wordt beschreven hoe u een aangepast profiel maakt voor Android Enterprise-apparaten. Het bevat ook een voorbeeld van een aangepast profiel waarmee kopieer- en plakbewerkingen worden geblokkeerd.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende instellingen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **aangepast Android Enterprise-profiel**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Selecteer **Android Enterprise**.
    - **Profieltype**: Selecteer **Aangepast**.

4. Selecteer in **Aangepaste OMA-URI-instellingen** de optie **Toevoegen**. Voer de volgende instellingen in:

    - **Naam**: Voer een unieke naam in voor de OMA-URI-instelling, zodat u deze gemakkelijk kunt vinden.
    - **Beschrijving**: Voer een beschrijving in met een overzicht van de instelling en eventuele andere belangrijke details.
    - **OMA-URI**: Voer de OMA-URI in die u als instelling wilt gebruiken.
    - **Gegevenstype**: Selecteer het gegevenstype dat u voor deze OMA-URI-instelling gaat gebruiken. Uw opties zijn:

      - Tekenreeks
      - Tekenreeks (XML-bestand)
      - Datum en tijd
      - Geheel getal
      - Drijvende komma
      - Boolean-waarde
      - Base64 (bestand)

    - **Waarde**: Voer de gegevenswaarde in die moet worden gekoppeld aan de OMA-URI die u hebt ingevoerd. De waarde is afhankelijk van het gegevenstype dat u hebt geselecteerd. Als u bijvoorbeeld **Datum en tijd** selecteert, selecteert u de waarde in een datumkiezer.

    Nadat u een aantal instellingen hebt toegevoegd, kunt u **Exporteren** selecteren. Met **Exporteren** maakt u een lijst met alle waarden die u hebt toegevoegd in een bestand met door komma's gescheiden waarden (.csv).

5. Selecteer **OK** om uw wijzigingen op te slaan. Blijf, indien nodig, meer instellingen toevoegen.
6. Wanneer u klaar bent, selecteert u **OK** > **Maken** om het Intune-profiel te maken. Wanneer het profiel is gemaakt, wordt dit weergegeven in de lijst **Apparaten - Configuratieprofielen**.

## <a name="example"></a>Voorbeeld

In dit voorbeeld maakt u een aangepast profiel waarmee kopieer- en plakbewerkingen tussen werk-apps en persoonlijke apps op Android Enterprise-apparaten worden beperkt.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende instellingen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Voer bijvoorbeeld **android ent block copy paste custom profile** in.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Selecteer **Android Enterprise**.
    - **Profieltype**: Selecteer **Aangepast**.

4. Selecteer in **Aangepaste OMA-URI-instellingen** de optie **Toevoegen**. Voer de volgende instellingen in:

    - **Naam**: Voer iets in als `Block copy and paste`.
    - **Beschrijving**: Voer iets in als `Blocks copy/paste between work and personal apps`.
    - **OMA-URI**: Voer `./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste` in.
    - **Gegevenstype**: Selecteer **Booleaans**, zodat de waarde voor deze OMA-URI **Waar** of **Onwaar** is.
    - **Waarde**: Selecteer **Waar**.

5. Nadat u de instellingen hebt ingevoerd, moet uw omgeving ongeveer zijn zoals in de volgende afbeelding:

    ![Blokkeer kopiëren en plakken voor een Android-werkprofiel.](./media/custom-settings-android-for-work/custom-policy-afw-copy-paste.png)

Als u dit profiel toewijst aan Android Enterprise-apparaten die u beheert, wordt het kopiëren en plakken tussen apps in het werkprofiel en persoonlijke profiel geblokkeerd.

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt nog niets. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

Maak een [aangepast profiel op Android-apparaten](custom-settings-android.md).
