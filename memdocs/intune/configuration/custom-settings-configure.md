---
title: Aangepaste apparaatinstellingen gebruiken in Microsoft Intune - Azure | Microsoft Docs
description: Maak een profiel of voeg een profiel toe om aangepaste instellingen te gebruiken voor apparaten met Windows 10 en hoger en Windows Phone-, Windows 8.1-, Android-apparaatbeheer-, Android Enterprise-, macOS- en iOS-/iPadOS-apparaten met Microsoft Intune.
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
ms.openlocfilehash: feb211b1de15aa0400e9ff71b428e2db02ef4b03
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80551371"
---
# <a name="create-a-profile-with-custom-settings-in-intune"></a>Een profiel maken met aangepaste instellingen in Intune

Microsoft Intune bevat veel ingebouwde instellingen om verschillende functies op een apparaat te beheren. U kunt ook aangepaste profielen maken, die vergelijkbaar zijn met ingebouwde profielen. Aangepaste profielen zijn ideaal wanneer u apparaatinstellingen en -functies wilt gebruiken die niet in Intune zijn ingebouwd. Deze profielen bevatten functies en instellingen die u op apparaten in uw organisatie kunt beheren. U kunt bijvoorbeeld een aangepast profiel maken waarmee u dezelfde functie voor elk iOS-/iPadOS-apparaat instelt.

Aangepaste instellingen worden voor elk platform anders geconfigureerd. Om bijvoorbeeld functies op Android- en Windows-apparaten te beheren, kunt u OMA-URI-waarden (Open Mobile Alliance Uniform Resource Identifier) opgeven. Voor Apple-apparaten kunt u een bestand importeren dat u met [Apple Configurator](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?mt=12) of [Apple Profile Manager](https://support.apple.com/profile-manager) hebt gemaakt.

Zie [Wat zijn Microsoft Intune-apparaatprofielen?](device-profiles.md) voor meer informatie over configuratieprofielen.

In dit artikel wordt beschreven hoe u een aangepast profiel maakt voor Android-apparaatbeheer, Android Enterprise, iOS/iPadOS, macOS en Windows. U kunt ook alle beschikbare instellingen voor de verschillende platformen zien.

> [!NOTE]
> De Intune-gebruikersinterface wordt bijgewerkt naar een versie voor volledig scherm. Dit kan enkele weken duren. Totdat de tenant deze update ontvangt, hebt u een enigszins afwijkende werkstroom wanneer u instellingen maakt of bewerkt zoals beschreven in dit artikel.

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
        - **Windows Phone 8.1**

    - **Profiel**: Selecteer **Aangepast**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **Windows 10: Aangepast profiel waarmee aangepaste AllowVPNOverCellular OMA-URI** wordt ingeschakeld.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Kies uw platform voor gedetailleerde instellingen:

    - [Android-apparaatbeheerder](custom-settings-android.md)
    - [Android Enterprise](custom-settings-android-for-work.md)
    - [iOS/iPadOS](custom-settings-ios.md)
    - [macOS](custom-settings-macos.md)
    - [Windows 10](custom-settings-windows-10.md)
    - [Windows Holographic for Business](custom-settings-windows-holographic.md)
    - [Windows Phone 8.1](custom-settings-windows-phone-8-1.md)

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="example"></a>Voorbeeld

In het volgende voorbeeld wordt de instelling **Connectivity/AllowVPNOverCellular** ingeschakeld. Met deze instelling kan met een Windows-10-apparaat een VPN-verbinding worden gemaakt in een mobiel netwerk.

> [!div class="mx-imgBorder"]
> ![Voorbeeld van een aangepast beleid met VPN-instellingen in Intune en Eindpuntbeheer](./media/custom-settings-configure/custom-policy-example.png)

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt mogelijk nog niets. Vervolgens kunt u [het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).
