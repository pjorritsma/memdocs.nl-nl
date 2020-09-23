---
title: Aangepaste instellingen toevoegen aan Android-apparaten Microsoft Intune - Azure | Microsoft Docs
description: Een aangepast profiel toevoegen voor Android-apparaten om een Wi-Fi-profiel te maken met een vooraf gedeelde sleutel, per app een VPN-profiel maken of apps toestemming geven/blokkeren voor Samsung Knox Standard-apparaten in Microsoft Intune
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/16/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 494b3892-916e-4b40-9b67-61adec889bdf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b5f08f4ce77bf068ac67e6a83e4e15e9a11f6e2d
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814855"
---
# <a name="use-custom-settings-for-android-devices-in-microsoft-intune"></a>Aangepaste instellingen gebruiken voor Android-apparaten in Microsoft Intune

Met Microsoft Intune kunt u aangepaste instellingen voor uw Android-apparaten toevoegen of maken met behulp van een 'aangepast profiel'. Aangepaste profielen zijn een functie in Intune. Ze zijn ontworpen om apparaatinstellingen en -functies toe te voegen die niet in Intune zijn ingebouwd.

Aangepaste profielen voor Android gebruiken OMA-URI-instellingen (Open Mobile Alliance Uniform Resource Identifier) om verschillende functies op Android-apparaten te configureren. Deze instellingen worden doorgaans gebruikt door fabrikanten van mobiele apparaten om deze functies te beheren.

Door een aangepast profiel te gebruiken, kunt u de volgende Android-instellingen configureren en toewijzen. De volgende instellingen zijn niet ingebouwd in Intune:

- [Een Wi-Fi-profiel maken met een vooraf gedeelde sleutel](/intune/wi-fi-profile-shared-key)
- [Een VPN per app-profiel maken](/intune/android-pulse-secure-per-app-vpn)
- [Apps toestaan of blokkeren voor Samsung KNOX Standard-apparaten](/intune/samsung-knox-apps-allow-block)
- [ in Microsoft Defender Advanced Threat Protection voor Android](../protect/advanced-threat-protection-manage-android.md)

>[!IMPORTANT]
> Alleen de hierboven genoemde instellingen kunnen worden geconfigureerd in een aangepast profiel. Android-apparaten geven geen volledige lijst weer met OMA-URI-instellingen die u kunt configureren. Als u meer instellingen wilt bekijken, stemt u voor meer instellingen op de [Intune Uservoice-site](https://microsoftintune.uservoice.com/forums/291681-ideas).

In dit artikel wordt beschreven hoe u een aangepast profiel maakt voor Android-apparaten.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende instellingen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **aangepast Android-profiel**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.
    - **Platform**: Selecteer **Android-apparaatbeheer**.
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

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt nog niets. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

Maak een [aangepast profiel op Android Enterprise-apparaten](custom-settings-android-for-work.md).
