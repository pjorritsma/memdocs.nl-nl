---
title: Education-instellingen toevoegen of configureren in Microsoft Intune - Azure | Microsoft Docs
description: Gebruik de app Take a test in een apparaatconfiguratieprofiel op apparaten met Windows 10 en hoger in Microsoft Intune. Maak een configuratieprofiel met behulp van de Education-instellingen, voer een test-app-URL in, kies hoe gebruikers zich aanmelden, bewaak het scherm tijdens de test en sta tekstsuggesties al dan niet toe tijdens de test.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52eae65e6735ad655c2e8db53e34383ccc5e3b30
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988399"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Gebruik de app Take a test op Windows 10-apparaten in Microsoft Intune

Education-profielen in Intune zijn bedoeld voor studenten die een test of examen op apparaten afleggen. Deze functie omvat de app **Take a test** en instellingen om een test-URL toe te voegen, te bepalen hoe eindgebruikers zich voor de test aanmelden en meer. Deze functie ondersteunt het volgende platform:

- Windows 10 en hoger

Wanneer de gebruiker zich aanmeldt, wordt de app Take a test automatisch geopend met de test die u hebt ingevoerd. Er kunnen geen andere apps op het apparaat worden uitgevoerd als de test bezig is. Meer informatie over de app Take a test vindt u in [Take tests in Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) (Testen afleggen in Windows 10).

Dit artikel vermeldt de stappen voor het maken van een configuratieprofiel voor een apparaat in Microsoft Intune. Het artikel bevat tevens informatie over de beschikbare education-instellingen voor uw Windows 10-apparaten.

## <a name="create-a-device-profile"></a>Een apparaatprofiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: Kies **Windows 10 en hoger**.
    - **Profiel**: Selecteer **Veilige evaluatie (onderwijs)** .

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het nieuwe profiel.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Voer in **Configuratie-instellingen** de instellingen in die u wilt configureren:

    - [Windows 10 en hoger](education-settings-windows.md)

8. Selecteer **Volgende**.

9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of gebruikersgroep die uw profiel ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

De volgende keer dat elk apparaat incheckt, wordt het beleid toegepast.

## <a name="next-steps"></a>Volgende stappen

Bekijk een overzicht van de [Windows 10 Education-instellingen](education-settings-windows.md) en de bijbehorende beschrijvingen.

Nadat het [profiel is toegewezen](device-profile-assign.md), [moet u de status ervan controleren](device-profile-monitor.md).
