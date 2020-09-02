---
title: Wijzigingen en gebeurtenissen in Microsoft Intune controleren - Azure | Microsoft Docs
description: Meer informatie over het bekijken van auditlogboeken waarin Microsoft Intune-activiteiten worden opgenomen.
keywords: ''
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 03/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1808743685c6907c11da23f92c5e263860098bea
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909683"
---
# <a name="use-audit-logs-to-track-and-monitor-events-in-microsoft-intune"></a>Gebruik auditlogboeken om gebeurtenissen in Microsoft Intune te volgen en te controleren

Auditlogboeken bevatten een lijst met activiteiten die een wijziging in Microsoft Intune genereren. De acties maken, bijwerken (bewerken), verwijderen, toewijzen en externe acties zorgen voor controlegebeurtenissen die beheerders voor de meeste werkbelastingen van Intune kunnen bekijken. Standaard is controle ingeschakeld voor alle klanten. De functie kan niet worden uitgeschakeld.

> [!NOTE]
> Het vastleggen van controlegebeurtenissen is gestart bij de functierelease van december 2017. Eerdere gebeurtenissen zijn niet beschikbaar.

## <a name="who-can-access-the-data"></a>Wie hebben er toegang tot de gegevens?

Gebruikers met de volgende machtigingen kunnen auditlogboeken bekijken:

- Hoofdbeheerder
- Intune-servicebeheerder
- Beheerders die zijn toegewezen aan een Intune-rol met **Auditgegevens** - **Lezen**-machtigingen

## <a name="audit-logs-for-intune-workloads"></a>Auditlogboeken voor Intune-werkbelastingen

U kunt auditlogboeken in de controlegroep voor elke Intune-workload bekijken:

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Tenantbeheer** > **Auditlogboeken**.
3. Als u de resultaten wilt filteren, selecteert u **Filteren** en verfijnt u de resultaten met behulp van de volgende opties.
    - **Categorie**: bijvoorbeeld **Compliance**, **Apparaat** en **Rol**.
    - **Activiteit**: de opties die hier worden weergegeven, worden beperkt door de optie die u hebt gekozen bij **Categorie**.
    - **Datumbereik**: u kunt logboeken van de vorige maand, week of dag kiezen.
4. Kies **Toepassen**.
4. Selecteer een item in de lijst om de activiteitsdetails weer te geven.

## <a name="route-logs-to-azure-monitor"></a>Logboeken routeren naar Azure Monitor

Auditlogboeken en operationele logboeken kunnen ook naar Azure Monitor worden gerouteerd. Selecteer in **Auditlogboeken** **Gegevensinstellingen exporteren**:

![Logboekgegevens exporteren naar Azure Monitor door Gegevensinstellingen exporteren in Intune te selecteren](./media/monitor-audit-logs/audit-logs-export-data-settings.png)

> [!NOTE]
> Zie [Logboekgegevens verzenden naar opslag, Event Hubs of Log Analytics](review-logs-using-azure-monitor.md) voor meer informatie over deze functie en om de vereisten voor het gebruik te bekijken.

> [!NOTE]
> **Gestart door (actor)** bevat informatie over wie de taak heeft uitgevoerd en waar deze is uitgevoerd. Als u de activiteit bijvoorbeeld in Intune in de Azure-portal uitvoert, vermeldt **Toepassing** altijd **Uitbreiding voor Microsoft Intune-portal** en maakt de **Toepassings-id** altijd gebruik van dezelfde GUID.
>
> In de sectie **Doel(en)** worden mogelijk meerdere doelen vermeld, samen met de eigenschappen die zijn gewijzigd.  

## <a name="use-graph-api-to-retrieve-audit-events"></a>Graph API gebruiken om auditgebeurtenissen op te halen

Zie [List auditEvents](/graph/api/intune-auditing-auditevent-list?view=graph-rest-1.0) (Auditgebeurtenissen weergeven) voor meer informatie over het gebruik van de Graph API voor het ophalen van één jaar aan auditgebeurtenissen.

## <a name="next-steps"></a>Volgende stappen

[Logboekgegevens verzenden naar opslag, Event Hubs of Log Analytics](review-logs-using-azure-monitor.md).

[Logboeken voor beveiliging van de client-app controleren](../apps/app-protection-policy-settings-log.md).