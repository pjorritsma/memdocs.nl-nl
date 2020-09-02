---
title: Apparaten beheren met Microsoft Intune - Azure | Microsoft Docs
description: Bekijk de apparaten die u met Microsoft Intune beheert, exporteer een lijst met apparaten naar de CSV-indeling, bekijk apparaten die zijn gekoppeld aan Azure Active Directory, bekijk een wijzigingenlogboek van acties op het apparaat, gebruik TeamViewer-Connector waarmee IT-beheerders op afstand problemen met Android-apparaten kunnen oplossen en bekijk alle acties die u op uw apparaten kunt uitvoeren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/14/2018
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d2412418-d91a-4767-a3d6-bc88bb29caa2
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0814fd11b2597c2a78dda70ba560e17fe2b742a1
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914358"
---
# <a name="what-is-microsoft-intune-device-management"></a>Wat is Microsoft Intune-apparaatbeheer?

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Als IT-beheerder moet u ervoor zorgen dat de beheerde apparaten de resources leveren waarmee uw gebruikers hun werk kunnen doen, terwijl u de gegevens beveiligt tegen risico's.

De workload **Apparaten** biedt inzicht in de apparaten die u beheert en biedt u de mogelijkheid om taken op afstand voor deze apparaten te activeren.

## <a name="get-to-your-devices"></a>Uw apparaten ophalen

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Selecteer **Apparaten**. Deze weergave bevat gedetailleerde informatie over de afzonderlijke apparaten en wat u kunt ermee kunt doen, inclusief:

   - **Overzicht** bevat een visuele momentopname van de ingeschreven apparaten waarin onder andere wordt getoond hoeveel apparaten de verschillende platformen gebruiken.
   - **Alle apparaten** geeft een lijst weer met de ingeschreven apparaten die u beheert.

     Met de functie **Exporteren** maakt u een .zip-lijst van alle apparaten in stappen van 10.000 (Internet Explorer) of 30.000 (Microsoft Edge, Chrome).

     Selecteer een apparaat om [meer informatie over dat apparaat weer te geven](device-inventory.md), zoals hardwaregegevens, geïnstalleerde apps en beleid.

   - **Azure AD-apparaten** geeft een lijst weer met apparaten die zijn ingeschreven bij, of deel uitmaken van Azure Active Directory (Azure AD). Meer informatie over [Azure AD-apparaatbeheer](/azure/active-directory/device-management-introduction).
   - **Apparaatacties** bevat een geschiedenis van de acties op afstand die zijn uitgevoerd op verschillende apparaten, waarbij de actie, de status ervan, de persoon die de actie heeft gestart en het tijdstip worden vermeld.

     ![Schermafbeelding van acties voor het bewaken van apparaten](./media/device-management/monitor-device-actions.png)

   - **Auditlogboeken** bevatten een lijst met activiteiten die een wijziging in Intune genereren. [Auditlogboeken](../fundamentals/monitor-audit-logs.md) bevatten meer details.
   - **TeamViewer-connector** is een service waarmee gebruikers van met Intune beheerde Android-apparaten hulp op afstand kunnen krijgen van hun IT-beheerder. Meer informatie over [TeamViewer](teamviewer-support.md).
   - **Help en ondersteuning** bevat een snelkoppeling naar tips voor probleemoplossing of het controleren van de status van Intune.

## <a name="available-device-actions"></a>Beschikbare apparaatbedreigingen
De beschikbaarheid van de acties is afhankelijk van het apparaatplatform en de configuratie van het apparaat.

- [Inventaris van apparaten weergeven](device-inventory.md)
- Externe apparaatacties uitvoeren:
  - [Autopilot opnieuw instellen](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
  - [BitLocker-sleutelrotatie](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) (alleen Windows)
  - [Verwijderen](devices-wipe.md#delete-devices-from-the-intune-portal)
  - [Activeringsvergrendeling uitschakelen](device-activation-lock-disable.md) (alleen iOS)
  - [Nieuwe start](device-fresh-start.md) (alleen Windows)
  - [Volledige scan](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (alleen Windows 10)
  - [Apparaat zoeken](device-locate.md) (alleen iOS)
  - [Modus Apparaat verloren](device-lost-mode.md) (alleen iOS)
  - [Snelle scan](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) (alleen Windows 10)
  - [Beheer op afstand voor Android](teamviewer-support.md)
  - [Vergrendelen op afstand](device-remote-lock.md)
  - [Naam van apparaat wijzigen](device-rename.md)
  - [Wachtwoordcode opnieuw instellen](device-passcode-reset.md)
  - [Opnieuw starten](device-restart.md) (alleen Windows)
  - [Buiten gebruik stellen](devices-wipe.md#retire)
  - [Beveiligingsinformatie van Windows Defender bijwerken](/windows/security/threat-protection/windows-defender-antivirus/manage-protection-updates-windows-defender-antivirus)
  - [Windows 10-pincode opnieuw instellen](device-windows-pin-reset.md)
  - [Wissen](devices-wipe.md#wipe)
  - [Aangepaste meldingen verzenden](custom-notifications.md#send-a-custom-notification-to-a-single-device) (Android, iOS/iPadOS)
  - [Apparaat synchroniseren](device-sync.md)
- [Apparaatacties bulksgewijs uitvoeren](bulk-device-actions.md)

## <a name="next-steps"></a>Volgende stappen

- Selecteer in **Alle apparaten** een apparaat om meer informatie over het apparaat weer te geven.
- Kies **Apparaatacties** om de status te zien van acties die zijn uitgevoerd op apparaten die u beheert.