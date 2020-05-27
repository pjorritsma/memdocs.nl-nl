---
title: Instellingen voor voorkeursbestand toevoegen aan macOS-apparaten in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Voeg een XML- of PLIST-bestand toe dat belangrijke informatie over uw app bevat. Gebruik een apparaatconfiguratieprofiel voor het voorkeursbestand om belangrijke informatie in het eigenschappenlijstbestand te wijzigen en dit toe te wijzen aan uw macOS-apparaten.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebf65ecc6dbe5059adbd6fec70833bf2fcab9de7
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988669"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Een eigenschappenlijstbestand toevoegen aan macOS-apparaten met behulp van Microsoft Intune

Met Microsoft Intune kunt u een eigenschappenlijstbestand (.plist) toevoegen voor macOS-apparaten of apps op macOS-apparaten.

Deze functie is van toepassing op:

- macOS 10.7 en hoger

Eigenschappenlijstbestanden bevatten informatie over macOS-apps. Zie [Over gegevenseigenschappenlijstbestanden](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Apple-website) en [Aangepaste payloadinstellingen](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1) voor meer informatie.

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen voor eigenschappenlijstbestanden die u aan macOS-apparaten kunt toevoegen. Gebruik deze instellingen als onderdeel van de MDM-oplossing (Mobile Device Management) om de app-bundel-id (`com.company.application`) en het PLIST-bestand van de app toe te voegen.

Deze instellingen worden toegevoegd aan een apparaatconfiguratieprofiel in Intune en vervolgens toegewezen aan of geïmplementeerd op uw macOS-apparaten.

## <a name="what-you-need-to-know"></a>Wat u dient te weten

- Deze instellingen worden niet gevalideerd. Zorg ervoor dat u de wijzigingen test voordat u het profiel aan uw apparaten toewijst.
- Als u niet zeker weet hoe u een app-sleutel moet invoeren, wijzigt u de instelling in de app. Controleer vervolgens het voorkeursbestand van de app met behulp van [Xcode](https://developer.apple.com/xcode/) om te zien hoe de instelling is geconfigureerd. Apple raadt aan om niet-beheerbare instellingen te verwijderen met Xcode voordat u het bestand importeert.
- Alleen in bepaalde apps kunnen beheerde voorkeuren worden gebruikt en in deze apps kunt u mogelijk niet alle instellingen beheren.
- Upload eigenschappenlijstbestanden die worden toegepast op apparaatkanaalinstellingen, en niet op gebruikerskanaalinstellingen. Eigenschappenlijstbestanden worden toegepast op het hele apparaat.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: **macOS** selecteren
    - **Profiel**: Selecteer **Voorkeursbestand**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het beleid. Geef uw beleid een naam zodat u het later eenvoudig kunt identificeren. Een goede beleidsnaam is bijvoorbeeld **macOS: Voeg een voorkeursbestand toe waarmee op apparaten Microsoft Defender ATP wordt geconfigureerd**.
    - **Beschrijving**: Voer een beschrijving in voor het beleid. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.

7. Configureer in **Configuratie-instellingen** uw instellingen:

    - **Naam van voorkeursdomein**: Voer de bundel-id in, bijvoorbeeld `com.company.application`. Voer bijvoorbeeld `com.Contoso.applicationName`, `com.Microsoft.Edge` of `com.microsoft.wdav` in.

      Eigenschappenlijstbestanden worden meestal gebruikt voor webbrowsers (Microsoft Edge), [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) en aangepaste apps. Wanneer u een voorkeursdomein maakt, wordt er ook een bundel-id gemaakt.

    - **Eigenschappenlijstbestand**: Selecteer het eigenschappenlijstbestand dat aan uw app is gekoppeld. Controleer of het een `.plist`- of `.xml`-bestand is. Upload bijvoorbeeld het bestand `YourApp-Manifest.plist` of het bestand `YourApp-Manifest.xml`.

      De belangrijkste informatie in het eigenschappenlijstbestand wordt weergegeven. Als u de sleutelgegevens wilt wijzigen, opent u het lijstbestand in een andere editor en uploadt u het bestand opnieuw in Intune.

    Zorg ervoor dat het bestand juist is opgemaakt. Het bestand mag alleen sleutel-waardeparen bevatten en mag niet tussen `<dict>`-, `<plist>`- of `<xml>`-tags staan. Het eigenschappenlijstbestand moet er ongeveer uitzien als het volgende bestand:

    ```xml
    <key>SomeKey</key>
    <string>someString</string>
    <key>AnotherKey</key>
    <false/>
    ...
    ```

8. Selecteer **Volgende**.
9. Wijs in **Bereiktags** (optioneel) een tag toe om het profiel te filteren op specifieke IT-groepen, zoals `US-NC IT Team` of `JohnGlenn_ITDepartment`. Zie [RBAC en bereiktags gebruiken voor gedistribueerde IT](../fundamentals/scope-tags.md) voor meer informatie over bereiktags.

    Selecteer **Volgende**.

10. Selecteer in **Toewijzingen** de gebruikers of groepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

11. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

Zie [Microsoft Edge-beleidsinstellingen voor macOS configureren](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac) voor meer informatie over voorkeursbestanden voor Microsoft Edge.
