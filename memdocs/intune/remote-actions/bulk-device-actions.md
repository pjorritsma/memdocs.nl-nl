---
title: Gebruik bulksgewijze apparaatacties in Microsoft Intune.
titleSuffix: ''
description: Gebruik bulksgewijze apparaatacties voor het externe apparaat.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c00e124c9f2741c3b94b08b51a6d1d897086087
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914409"
---
# <a name="use-bulk-device-actions"></a>Bulksgewijze apparaatacties gebruiken

U kunt bulksgewijze apparaatacties voor de volgende externe acties gebruiken:
- [Autopilot opnieuw instellen](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Aangepaste meldingen](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Verwijderen](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Naam wijzigen](device-rename.md)
- [Opnieuw opstarten](device-restart.md)
- [Synchroniseren](device-sync.md)
- [Wissen](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Een bulksgewijze apparaatactie gebruiken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Kies **Apparaten** > **Alle apparaten** > **Bulksgewijze apparaatacties**.
![Apparaatacties bulksgewijs uitvoeren](./media/bulk-device-actions/bulk-device-actions.png)
3. Selecteer op de pagina **Bulkacties voor apparaat** een **besturingssysteem** en **Apparaatactie**. Voor sommige apparaatacties kunnen extra opties of velden worden ingevuld. Kies **Volgende**.
4. Selecteer op de pagina **Apparaten** 1 tot 100 apparaten > **Volgende**.
5. Selecteer op de pagina **Beoordelen en maken** de optie **Maken**.

## <a name="next-steps"></a>Volgende stappen
[Overzicht van apparaatbeheer.](device-management.md)