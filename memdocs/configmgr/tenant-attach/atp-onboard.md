---
title: Tenant-onboard-Configuration Manager-clients toevoegen aan micro soft Defender ATP vanuit het micro soft Endpoint Manager-beheer centrum (preview)
titleSuffix: Configuration Manager
description: Implementeer het voorbereidings beleid voor micro soft Defender ATP-eindpunt detectie en-antwoorden (EDR) voor het Configuration Manager van beheerde clients vanuit het beheer centrum.
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 50f8e206-a2af-469a-9f1b-0f7a87166f48
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a2862812145e33a992ceaa346e138606eee5fad0
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/31/2020
ms.locfileid: "89194216"
---
# <a name="tenant-attach-onboard-configuration-manager-clients-to-microsoft-defender-atp-from-the-admin-center-preview"></a><a name="bkmk_atp"></a> Tenant bijvoegen: Configuration Manager-clients onboarden naar micro soft Defender ATP vanuit het beheer centrum (preview-versie)
<!--5691658-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen in één console met de naam **micro soft Endpoint Manager-beheer centrum**. U kunt het voorbereidings beleid voor micro soft Defender ATP-eindpunt detectie en-antwoorden (EDR) implementeren voor het Configuration Manager van beheerde clients. Voor deze clients is Azure AD of MDM-inschrijving niet vereist en het beleid is gericht op ConfigMgr-verzamelingen in plaats van met Azure AD-groepen.

## <a name="prerequisites"></a>Vereisten

- Toegang tot het [micro soft Endpoint Manager-beheer centrum](https://endpoint.microsoft.com/).
- Een E5-licentie voor [micro soft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).
- Een omgeving waaraan een [Tenant is gekoppeld met geüploade apparaten](device-sync-actions.md).
- Mini maal Configuration Manager versie 2006 en de bijbehorende versie van de console zijn geïnstalleerd.
   - Voer een upgrade uit voor de doel apparaten naar de nieuwste versie van de Configuration Manager-client.

## <a name="make-configuration-manager-collections-available-to-assign-endpoint-security-policies"></a><a name="bkmk_collections"></a> Configuration Manager verzamelingen beschikbaar maken voor het toewijzen van endpoint-beveiligings beleidsregels

Als u verzamelingen van apparaten in Intune in staat stelt om met eindpuntbeveiligingsbeleid Intune te werken, configureert u apparaten in die verzamelingen voor onboarding met Microsoft Defender ATP.

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](../../intune/protect/includes/make-configmgr-collection-available-edr.md)]

## <a name="create-microsoft-defender-atp-endpoint-detection-and-response-edr-onboarding-policies"></a><a name="bkmk_onboard"></a> Maak beleids regels voor het voorbereiden van micro soft Defender ATP-eind punten detectie en-antwoorden (EDR)

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://endpoint.microsoft.com).

1. Selecteer **Eindpuntbeveiliging** > **Eindpuntdetectie en -respons** > **Beleid maken**.

1. Selecteer het volgende platform en profiel voor uw beleid:

   - Platform: **Windows 10 en Windows Server (ConfigMgr)**
   - Profiel: **Eindpuntdetectie en -respons (ConfigMgr)**

1. Selecteer **Maken**.

1. Voer op de pagina **Basisinformatie** een naam en een beschrijving in voor het profiel en selecteer dan **Volgende**.

1. Configureer op de pagina **Configuratie-instellingen** de instellingen die u met dit profiel wilt beheren. Het onboardingpakket wordt automatisch opgenomen en kan niet worden geconfigureerd.

   Wanneer u klaar bent met het configureren van instellingen, selecteert u **Volgende**.

1. Selecteer op de pagina **toewijzingen** de verzamelingen die dit beleid zullen ontvangen. Selecteer verzamelingen in Configuration Manager die u hebt gesynchroniseerd met micro soft Endpoint Manager-beheer centrum en ingeschakeld voor micro soft Defender ATP-beleid.

   U kunt ervoor kiezen om op dit moment geen verzamelingen toe te wijzen en het beleid later bewerken om een toewijzing toe te voegen.

   Wanneer u klaar bent om verder te gaan, selecteert u **Volgende**.

1. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent.

   Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

## <a name="next-steps"></a>Volgende stappen

[Endpoint Security-antivirus beleid maken en implementeren op apparaten die aan de Tenant zijn gekoppeld](deploy-antivirus-policy.md)