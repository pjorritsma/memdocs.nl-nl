---
title: Instellingen voor firewall tegen aanvallen beheren met eindpuntbeveiligingsbeleid in Microsoft Intune | Microsoft Docs
description: Configureer en implementeer beleidsregels voor apparaten die u beheert met eindpuntbeveiligingsinstellingen voor firewallbeleid in Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 5b33be56975713c801d2ad3fdea17e6303687274
ms.sourcegitcommit: 03d2331876ad61d0a6bb1efca3aa655b88f73119
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/03/2020
ms.locfileid: "85946909"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Firewallbeleid voor eindpuntbeveiliging in Intune

Gebruik het firewallbeleid voor eindpuntbeveiliging in Intune om een in apparaten ingebouwde firewall te configureren voor apparaten met macOS en Windows 10.

Hoewel u dezelfde firewallinstellingen kunt configureren met behulp van Endpoint Protection-apparaatconfiguratieprofielen, bevatten de apparaatconfiguratieprofielen aanvullende categorieën instellingen. Deze extra instellingen zijn niet gerelateerd aan firewalls en kunnen de taak voor het configureren van alleen firewall-instellingen voor uw omgeving bemoeilijken.

U kunt het eindpuntbeveiligingsbeleid vinden bij firewalls onder *Beheren* in het knooppunt **Eindpuntbeveiliging** van het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

Zie [Instellingen voor Firewall-profielen](../protect/endpoint-security-Firewall-profile-settings.md).

## <a name="prerequisites-for-firewall-profiles"></a>Vereisten voor Firewall-profielen

- Windows 10 of hoger
- Een ondersteunde versie van macOS

## <a name="firewall-profiles"></a>Firewall-profielen

**macOS-profielen**:

- **macOS firewall**: Instellingen inschakelen en configureren voor de ingebouwde firewall op macOS.

**Windows 10-profielen**:

- **Microsoft Defender Firewall**: Configureer instellingen voor Windows Defender Firewall met geavanceerde beveiliging. Windows Defender Firewall voorziet in twee richtingen filteren van netwerk verkeer op basis van hosts voor een apparaat en kan niet-geautoriseerd netwerkverkeer naar of van het lokale apparaat blokkeren.

- **Microsoft Defender Firewall-regels**  *(Preview)* : Definieer beheerders uitgebreide firewallregels, zoals specifieke poorten, protocollen, toepassingen en netwerken en om netwerkverkeer toe te staan of te blokkeren. Elk exemplaar van dit profiel ondersteunt maximaal 150 aangepaste regels.

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>Samenvoegers van firewallregels en beleidsconflicten

Plan voor het toepassen van Firewall-beleid op een apparaat met slechts één beleid. Het gebruik van één beleidsexemplaar en beleidstype helpt te voorkomen dat twee afzonderlijke beleidsregels verschillende configuraties toepassen op dezelfde instelling, waardoor er conflicten ontstaan. Wanneer er sprake is van een conflict tussen twee beleidsexemplaren of typen beleidsregels die dezelfde instelling beheren met verschillende waarden, wordt de instelling niet naar het apparaat verzonden.

- Deze vorm van beleidsconflicten is van toepassing op het **Microsoft Defender Firewall**-profiel, dat strijdig kan zijn met andere profielen van Microsoft Defender Firewall, of een firewallconfiguratie die wordt geleverd door een ander beleidstype, zoals de apparaatconfiguratie.

  *Microsoft Defender Firewall-profielen* zijn niet in conflict met profielen voor *Microsoft Defender Firewall-regels*.

Wanneer u **Microsoft Defender Firewall-regel**profielen gebruikt, kunt u meerdere regelprofielen toepassen op hetzelfde apparaat. Als er echter verschillende regels bestaan voor hetzelfde item met verschillende configuraties, worden beide naar het apparaat verzonden en ontstaat er een conflict op dat apparaat.

- Als de ene regel bijvoorbeeld *Teams.exe* door de firewall blokkeert en een tweede regel *Teams.exe*toestaat, worden beide regels aan de client geleverd. Dit resultaat wijkt af van conflicten die onstaan via andere beleidsregels voor Firewall-instellingen.

Wanneer regels uit meerdere regelprofielen niet conflicteren met elkaar, worden de regels uit elk profiel samengevoegd om een gecombineerde firewallregelconfiguratie op het apparaat te maken. Dit gedrag stelt u in staat om meer dan de 150 regels te implementeren die elk afzonderlijk profiel voor een apparaat ondersteunen.

- U hebt bijvoorbeeld twee Microsoft Defender Firewall-regelprofielen. Het eerste profiel biedt toegang tot *Teams.exe* via de firewall. Het tweede profiel biedt toegang tot *Outlook. exe* via de firewall. Wanneer een apparaat beide profielen ontvangt, wordt het apparaat geconfigureerd om beide apps via de firewall toe te staan.

## <a name="next-steps"></a>Volgende stappen

[Eindpuntbeveiligingsbeleid configureren](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
