---
title: Instellingen voor gedeelde apparaten en apparaten met meerdere gebruikers in Microsoft Intune - Azure | Microsoft Docs
description: Voeg in Microsoft Intune Windows 10- en Windows Holographic for Business-apparaten toe die worden gedeeld of door meerdere gebruikers worden gebruikt, en gebruik deze. Bekijk een lijst met alle instellingen en wat deze betekenen op de apparaten, inclusief Microsoft HoloLens. Beheer gastaccounts, beheer accounts, verwijder inactieve accounts, geef toestemming voor of blokkeer opslaan in lokale opslag, stel energie- en slaapopties in, kies wanneer updates worden geïnstalleerd en gebruik apparaten in onderwijsomgevingen in een apparaatconfiguratieprofiel.
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
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4f85c30c9472849d26802c8cdccd7a95006a3e4a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984004"
---
# <a name="control-access-accounts-and-power-features-on-shared-pc-or-multi-user-devices-using-intune"></a>Toegang, accounts en energiefuncties op gedeelde pc's en apparaten met meerdere gebruikers beheren met Intune

Apparaten met meerdere gebruikers worden ook wel gedeelde apparaten genoemd. Deze maken meestal deel uit van MDM-oplossingen (Mobile Device Management). Met Microsoft Intune kunt u gedeelde apparaten met de volgende platformen aanpassen:

- Windows 10 Professional en hoger
- Windows 10 Enterprise en hoger
- Windows Holographic for Business, zoals de HoloLens

Scholen beschikken bijvoorbeeld over apparaten die door veel leerlingen of studenten worden gebruikt. Met deze instelling kan de Intune-beheerder op school de functie voor gedeelde pc's inschakelen zodat er slechts één gebruiker tegelijk een apparaat kan gebruiken. Studenten kunnen op apparaten niet wisselen tussen verschillende accounts waarbij is aangemeld. Wanneer de student zich heeft afgemeld, worden indien gewenst alle gebruikersspecifieke instellingen verwijderd.

Eindgebruikers kunnen zich met een gastaccount aanmelden op deze gedeelde apparaten. Wanneer een gebruiker zich heeft aangemeld, worden de referenties in de cache opgeslagen. Tijdens het gebruik van het apparaat hebben eindgebruikers alleen toegang tot de functies die u inschakelt. U bepaalt bijvoorbeeld wanneer de slaapstand op apparaten wordt ingeschakeld, of gebruikers lokale bestanden kunnen zien en bestanden kunnen opslaan, energiebeheerinstellingen kunnen in- of uitschakelen en meer. U bepaalt ook of het gastaccount wordt verwijderd nadat de gebruiker zich heeft afgemeld en of inactieve accounts worden verwijderd als er een bepaalde drempelwaarde wordt bereikt.

In dit artikel ziet u hoe u een configuratieprofiel maakt. Er staan ook koppelingen in naar de beschikbare instellingen (inclusief beschrijving).

Wanneer het profiel in Intune is gemaakt, implementeert u het of wijst u het toe aan apparaatgroepen in uw organisatie. U kunt dit profiel ook toewijzen aan apparaatgroepen met verschillende typen apparaten en besturingssysteemversies.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

   - **Platform**: Kies **Windows 10 en hoger**.
   - **Profiel**: Selecteer **Gedeelde apparaat voor meerdere gebruikers**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

   - **Naam**: Voer een beschrijvende naam in voor het nieuwe profiel.
   - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Welke instellingen u kunt configureren in **Configuratie-instellingen**, is afhankelijk van het platform dat u hebt gekozen. Kies uw platform voor gedetailleerde instellingen:

    - [Windows 10 en hoger](shared-user-device-settings-windows.md)
    - [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)

8. Selecteer **Volgende**.

9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de apparaatgroep die uw profiel zal ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

    > [!NOTE]
    > Wijs het profiel toe aan apparaatgroepen in uw organisatie.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

De volgende keer dat elk apparaat incheckt, wordt het beleid toegepast.

## <a name="next-steps"></a>Volgende stappen

- Zie alle instellingen voor [Windows 10 en hoger](shared-user-device-settings-windows.md) of [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md).
- Wanneer het [profiel is toegewezen](device-profile-assign.md), moet u [de status ervan controleren](device-profile-monitor.md).
