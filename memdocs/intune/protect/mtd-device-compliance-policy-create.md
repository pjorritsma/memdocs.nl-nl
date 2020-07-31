---
title: Een MTD-nalevingsbeleid (Mobile Threat Defense) voor apparaten maken met Microsoft Intune
titleSuffix: Microsoft Intune
description: Maak een Intune-nalevingsbeleid voor apparaten waarbij gebruik wordt gemaakt van de bedreigingsniveaus van uw MTD-partner om te bepalen of een mobiel apparaat toegang mag hebben tot bedrijfsresources.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88f8a2ff04f536370f613341170e7fae0a808ff6
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365522"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>MTD-nalevingsbeleid (Mobile Threat Defense) voor apparaten maken met Intune

Intune met MTD helpt u bij het detecteren van bedreigingen en het beoordelen van risico op mobiele apparaten. U kunt een Intune-nalevingsbeleidsregel maken voor een risicoanalyse waarmee wordt bepaald of het apparaat compatibel is. Vervolgens kunt u [beleid voor voorwaardelijke toegang](create-conditional-access-intune.md) gebruiken om toegang tot services te blokkeren op basis van de apparaatnaleving.

> [!NOTE]
> Deze informatie is van toepassing op alle Mobile Threat Defense-partners.

## <a name="before-you-begin"></a>Voordat u begint

Als onderdeel van de configuratie van MTD in de MTD-partnerconsole, hebt u een beleid gemaakt waarmee verschillende bedreigingen in de categorieën Hoog, Gemiddeld en Laag worden ingedeeld. U gaat nu het MTD-niveau instellen in het nalevingsbeleid van Intune voor apparaten.

Vereisten voor apparaatnalevingsbeleid met MTD:

- De integratie van MTD met Intune instellen

## <a name="to-create-an-mtd-device-compliance-policy"></a>Nalevingsbeleid voor MTD-apparaten maken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** > **Apparaatcompatibiliteit** > **Beleid maken**.

3. Selecteer de gewenste optie bij **Platform** en klik vervolgens op **Maken**.

4. Geef bij **Basisinformatie** een **Naam** en **Beschrijving** (optioneel) voor het nalevingsbeleid voor apparaten op. Selecteer **Volgende** om door te gaan.


5. In **Instellingen voor naleving** vouwt u **Apparaatstatus** uit en configureert u deze. Kies het Mobile Threat-niveau uit de vervolgkeuzelijst bij **Vereisen dat het apparaat het apparaatbedreigingsniveau niet overschrijdt**.

   - **Beveiligd**: Dit is het veiligste niveau. Het apparaat kan geen enkele bedreiging hebben en heeft nog altijd toegang tot bedrijfsbronnen. Als er bedreigingen worden gevonden, wordt het apparaat geëvalueerd als niet-compatibel.

   - **Laag**: het apparaat is conform als er alleen bedreigingen van een laag niveau aanwezig zijn. Als een hoger niveau wordt aangetroffen, krijgt het apparaat de status niet-compatibel.

   - **Gemiddeld**: het apparaat is conform als de bedreigingen op het apparaat van laag of gemiddeld niveau zijn. Als er bedreigingen van hoog niveau worden aangetroffen, wordt het apparaat als niet-compatibel beoordeeld.

   - **Hoog**: Dit bedreigingsniveau is het minst veilig; hiermee worden alle bedreigingsniveaus toegestaan en wordt Mobile Threat Defense uitsluitend gebruikt voor rapportagedoeleinden. Op apparaten moet de MTD-app met deze instelling zijn geactiveerd.

6. Selecteer **Volgende** om door te gaan naar **Toewijzingen**. Selecteer de groepen die dit profiel zullen ontvangen. Zie [Gebruikers- en apparaatprofielen toewijzen](../configuration/device-profile-assign.md) voor meer informatie over het toewijzen van profielen.

   Selecteer **Volgende**.

7. Kies op de pagina **Controleren en maken** de optie **Maken** zodra u klaar bent. Het nieuwe profiel wordt weergegeven in de lijst wanneer u het beleidstype selecteert voor het profiel dat u hebt gemaakt.

> [!IMPORTANT]
> Als u beleid voor voorwaardelijke toegang voor Office 365 of andere services maakt, wordt de compatibiliteitsevaluatie van het apparaat bekeken en wordt niet-compatibele apparaten de toegang tot bedrijfsresources geweigerd tot de bedreiging op het apparaat is opgelost.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>Nalevingsbeleid voor MTD-apparaten toewijzen

U kunt een nalevingsbeleid voor apparaten als volgt toewijzen of de toewijzing wijzigen:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Selecteer **Eindpuntbeveiliging** > **Apparaatcompatibiliteit**.

3. Selecteer het beleid dat u aan gebruikers wilt toewijzen en kies vervolgens **Eigenschappen**.

4. Selecteer **Bewerken** voor Toewijzingen en gebruik de beschikbare opties *Opnemen* en *Uitsluiten* als u wilt dat groepen dit beleid al dan niet ontvangen.  

5. Selecteer **Beoordelen en opslaan** om de toewijzing te voltooien. Wanneer u de toewijzing opslaat, wordt het beleid naar de geselecteerde gebruikers geïmplementeerd en worden hun apparaten geëvalueerd op naleving.

## <a name="next-steps"></a>Volgende stappen

[MTD met Intune inschakelen](mtd-connector-enable.md)
