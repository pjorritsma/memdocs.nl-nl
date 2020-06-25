---
title: Instellingen voor 802.1x bekabeld netwerk configureren voor macOS-apparaten in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Lees hoe u een configuratieprofiel voor een bekabeld netwerkapparaat kunt toevoegen of maken voor macOS-desktopcomputers. Zie de verschillende instellingen, voeg certificaten toe, kies een EAP-type en het selecteer een verificatiemethode in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095771"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>Bekabeld netwerkinstellingen toevoegen en gebruiken op uw macOs-apparaten in Microsoft Intune

Bekabelde netwerken worden door veel organisaties gebruikt om netwerktoegang te geven tot desktopcomputers. Microsoft Intune omvat ingebouwde instellingen die kunnen worden geïmplementeerd voor macOs-gebruikers en apparaten in uw organisatie. Deze groep instellingen wordt een "profiel" genoemd. In uw profiel kunt u algemene instellingen, zoals de netwerkinterface, geaccepteerde EAP-typen en vertrouwensinstellingen voor servers, toevoegen.

Wanneer het profiel gereed is, kan het worden toegewezen aan verschillende gebruikers en groepen. Wanneer het profiel is toegewezen, krijgen uw gebruikers toegang tot het bekabeld netwerk van uw organisatie zonder dat zij dit zelf hoeven te configureren.

Gebruik deze functie als onderdeel van uw Mobile Device Management-oplossing (MDM) om 802.1 x-profielen te maken voor het beheren van bekabelde netwerken. Implementeer vervolgens deze bekabelde netwerken op uw macOS-apparaten.

Deze functie is van toepassing op:

- macOS

U hebt bijvoorbeeld een bekabeld netwerk met de naam **bekabelde netwerk Contoso**. U wilt alle macOS-desktops instellen om verbinding te maken met dit netwerk. Dit is het proces:

1. Maak een bekabeld netwerkprofiel met daarin de instellingen voor de verbinding met het **bekabelde netwerk Contoso**.
2. Wijs het profiel toe aan een groep die alle gebruikers van macOs-desktopcomputers omvat. Zie [Gebruikersgroepen versus apparaatgroepen](device-profile-assign.md#user-groups-vs-device-groups) voor aanbevelingen voor het gebruik van groepstypen.
3. Op hun desktops vinden gebruikers het **bekabelde netwerk Contoso** in de lijst met netwerken. Ze kunnen dan verbinding maken met het netwerk via de door u gekozen verificatiemethode.

In dit artikel worden de stappen vermeld voor het maken van een bekabeld netwerkprofiel. Het bevat ook een koppeling met een beschrijving van de verschillende instellingen.

## <a name="create-the-profile"></a>Het profiel maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > **Configuratieprofielen** > **Profiel maken**.
3. Voer de volgende eigenschappen in:

    - **Platform**: **macOS** selecteren.
    - **Profiel**: Selecteer **Bekabeld netwerk**.

4. Selecteer **Maken**.
5. Voer in **Basisinformatie** de volgende eigenschappen in:

    - **Naam**: Voer een beschrijvende naam in voor het profiel. Geef uw profielen een naam zodat u ze later eenvoudig kunt identificeren. Een goede profielnaam is bijvoorbeeld **bekabeld netwerkprofiel voor hele bedrijf op macOS-apparaten**.
    - **Beschrijving**: Voer een beschrijving in voor het profiel. Deze instelling is optioneel, maar wordt aanbevolen.

6. Selecteer **Volgende**.
7. Selecteer in **Configuratie-instellingen** de netwerkinterface van het netwerk en kies het type Extensible Authentication Protocol (EAP). Voor een lijst van alle instellingen en wat ze doen raadpleegt u:

    - [macOS](wired-network-settings-macos.md)

8. Selecteer **Volgende**.
9. Selecteer in **Toewijzingen** de gebruikersgroepen of apparaatgroepen die uw profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

    Selecteer **Volgende**.

10. Controleer uw instellingen in **Beoordelen en maken**. Wanneer u **Maken**selecteert, worden uw wijzigingen opgeslagen en wordt het profiel toegewezen. Het beleid wordt ook weergegeven in de lijst met profielen.

> [!TIP]
> Als u gebruikmaakt van verificatie op basis van certificaten voor uw bekabeld netwerkprofiel, implementeert u het bekabeld netwerkprofiel, het certificaatprofiel en het vertrouwde basisprofiel in dezelfde groepen. Door deze implementatie kan elk apparaat de geldigheid van uw certificeringsinstantie herkennen. Zie [Certificaten configureren met Microsoft Intune](../protect/certificates-configure.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

Het profiel is gemaakt, maar er gebeurt mogelijk niets. Zorg ervoor dat u [dit profiel toewijst](device-profile-assign.md) en[de status ervan bewaakt](device-profile-monitor.md).
