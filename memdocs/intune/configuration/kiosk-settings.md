---
title: Kioskinstellingen voor Windows- en Holographic-apparaten in Microsoft Intune - Azure | Microsoft Docs
description: Configureer uw Windows 10-apparaten (en hoger) en Windows Holographic for Business-apparaten als kiosken voor één app en voor meerdere apps, pas het menu Start aan, voeg apps toe, geef de taakbalk weer, en configureer een webbrowser in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: a9be644a47a361cf29e7b7132b2c87a4921553ea
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989425"
---
# <a name="windows-10-and-windows-holographic-for-business-device-settings-to-run-as-a-dedicated-kiosk-using-intune"></a>Instellingen voor Windows 10- en Windows Holographic for Business-apparaten om ze als toegewezen kiosk uit te voeren via Intune

Op Windows 10-apparaten kunt u Intune gebruiken om apparaten als kiosk uit te voeren; dit worden ook wel toegewezen apparaten genoemd. Met een apparaat in de kioskmodus kan er één app of kunnen er veel apps worden uitgevoerd. U kunt een startmenu weergeven en aanpassen, diverse apps toevoegen, waaronder Win32-apps, een specifieke startpagina aan een webbrowser toevoegen en meer. 

Deze functie is van toepassing op:

- Windows 10 en hoger
- Windows Holographic for Business

Als u kioskprofielen voor andere platforms wilt maken, raadpleegt u [Android-apparaatbeheerder](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices) en [iOS/iPadOS](device-restrictions-ios.md#kiosk).

Intune biedt ondersteuning voor één kioskprofiel per apparaat. Als u meerdere kioskprofielen op één apparaat nodig hebt, kunt u een [aangepaste OMA URI gebruiken](custom-settings-windows-10.md).

Intune maakt gebruik van configuratieprofielen om deze instellingen te maken voor en af te stemmen op de behoeften van uw organisatie. Voeg deze functies aan een profiel toe en push of implementeer deze instellingen vervolgens naar groepen binnen de organisatie.

In dit artikel wordt beschreven hoe u een apparaatconfiguratieprofiel maakt. Zie [Kioskinstellingen voor Windows 10](kiosk-settings-windows.md) en [Kioskinstellingen voor Windows Holographic for Business](kiosk-settings-holographic.md) voor een lijst met alle instellingen en wat ze doen.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

   - **Platform**: Kies **Windows 10 en hoger**.
   - **Profiel**: Selecteer **Kiosk**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

   - **Naam**: Voer een beschrijvende naam in voor het nieuwe profiel.
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Kies in **Configuratie-instellingen** > **Selecteer een kioskmodus** het type kioskmodus dat door het beleid wordt ondersteund. Opties zijn onder andere:

    - **Niet geconfigureerd** (standaardinstelling): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt door het beleid geen kioskmodus ingeschakeld.
    - **Kiosk met één app, in volledige schermweergave**: Het apparaat wordt uitgevoerd als een enkel gebruikersaccount en wordt vastgemaakt aan een enkele Store-app. Dus wanneer de gebruiker zich aanmeldt, wordt een specifieke app gestart. Deze modus voorkomt ook dat de gebruiker nieuwe apps kan openen of de actieve app kan wijzigen.
    - **Kiosk voor meerdere apps**: Op het apparaat worden meerdere Store-apps, Win32-apps of Postvak IN-apps voor Windows uitgevoerd met behulp van de model-id van de toepassingsgebruiker (AUMID). Alleen de apps die u toevoegt, zijn op het apparaat beschikbaar.

        Het voordeel van een kiosk voor meerdere apps, of apparaat voor een bepaald doeleinde, is dat het eenvoudig is in het gebruik omdat de gebruikers alleen toegang krijgen tot de apps die ze nodig hebben. Daarnaast worden de apps die de gebruikers niet nodig hebben niet weergegeven.

    Voor een lijst van alle instellingen en wat ze doen raadpleegt u:

      - [Kioskinstellingen voor Windows 10](kiosk-settings-windows.md)
      - [Kioskinstellingen voor Windows Holographic for Business](kiosk-settings-holographic.md)

8. Selecteer **Volgende**.

9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of gebruikersgroep die uw profiel ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

De volgende keer dat elk apparaat incheckt, wordt het beleid toegepast.

## <a name="next-steps"></a>Volgende stappen

Wanneer het [profiel is toegewezen](device-profile-assign.md), moet u [de status ervan controleren](device-profile-monitor.md).

U kunt kioskprofielen maken voor apparaten met de volgende platforms:

- [Android-apparaatbeheerder](device-restrictions-android.md#kiosk)
- [Android Enterprise](device-restrictions-android-for-work.md#dedicated-devices)
- [Windows 10 en hoger](kiosk-settings-windows.md)
- [Windows Holographic for Business](kiosk-settings-holographic.md)
