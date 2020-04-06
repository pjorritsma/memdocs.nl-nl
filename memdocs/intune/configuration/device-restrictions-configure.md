---
title: Apparaatfuncties beperken met behulp van beleid in Microsoft Intune - Azure | Microsoft Docs
description: Voeg een apparaatprofiel toe om functies op Android-apparaatbeheer-, Android Enterprise-, macOS-, iOS-, iPadOS-, Windows Phone- en Windows 10-apparaten in Microsoft Intune te beperken.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 470ca47aa92b30acacc8a251c6d7d1741513bdf1
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359219"
---
# <a name="configure-device-restriction-settings-in-microsoft-intune"></a>Apparaatbeperkingsinstellingen configureren in Microsoft Intune

Intune bevat beleidsregels voor apparaatbeperkingen waarmee beheerders Android-, iOS-/iPadOS-, macOS-en Windows-apparaten kunnen beheren. Met deze beperkingen kunt u een breed scala aan instellingen en functies beheren voor het beveiligen van de resources van uw organisatie. Beheerders kunnen bijvoorbeeld het volgende:

- Hiermee kunt u het gebruik van de camera van het apparaat toestaan of blokkeren.
- Toegang beheren tot Google Play, app-stores, documenten weergeven en gamen.
- Ingebouwde apps blokkeren of een lijst maken met apps die zijn toegestaan of verboden.
- Het maken van een back-up van bestanden naar cloud- en opslagaccounts toestaan of voorkomen.
- De minimale wachtwoordlengte instellen en eenvoudige wachtwoorden blokkeren.

Deze functies zijn beschikbaar in Intune en kunnen worden geconfigureerd door de beheerder. Intune maakt gebruik van configuratieprofielen om deze instellingen te maken voor en af te stemmen op de behoeften van uw organisatie. Nadat u deze functies aan een profiel hebt toegevoegd, kunt u het profiel pushen naar en implementeren op apparaten in uw organisatie.

In dit artikel wordt beschreven hoe u een apparaatbeperkingsprofiel maakt. U kunt ook alle beschikbare instellingen voor de verschillende platformen zien.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Kies het platform van uw apparaten. Uw opties zijn:  

        - **Android-apparaatbeheerder**
        - **Android Enterprise**
        - **iOS/iPadOS**
        - **macOS**
        - **Windows 10 en hoger**
        - **Windows 8.1 en hoger**
        - **Windows Phone 8.1**

    - **Profiel**: Selecteer **Apparaatbeperkingen**.

        Als u een apparaatbeperkingsprofiel wilt maken voor Windows 10 Team-apparaten, zoals Surface Hub, kiest u **Apparaatbeperkingen (Windows 10 Team)** .

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **iOS/iPadOS: Camera op apparaten blokkeren**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Kies uw platform voor gedetailleerde instellingen:

    - [Android-apparaatbeheerder](device-restrictions-android.md)
    - [Android Enterprise](device-restrictions-android-for-work.md)
    - [iOS/iPadOS](device-restrictions-ios.md)
    - [macOS](device-restrictions-macos.md)
    - [Windows Phone 8.1](device-restrictions-windows-phone-8-1.md)
    - [Windows 8.1](device-restrictions-windows-8-1.md)
    - [Windows 10 en nieuwer](device-restrictions-windows-10.md)
    - [Windows 10 Team](device-restrictions-windows-10-teams.md)
    - [Windows Holographic for Business](device-restrictions-windows-holographic.md)

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="next-steps"></a>Volgende stappen

Nadat het profiel is gemaakt, is het klaar om te worden toegewezen. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/device-restrictions-configure/disable-android-camera.png)

-->
