---
title: BitLocker Self-Service Portal
titleSuffix: Configuration Manager
description: De Self-Service Portal voor gebruikers gebruiken in Configuration Manager voor BitLocker-herstel
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ad1f79bb439e0a426229680960092a5f0d8fb3c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129236"
---
# <a name="bitlocker-self-service-portal"></a>BitLocker Self-Service Portal

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

Nadat u [de BitLocker Self-Service Portal hebt geïnstalleerd](setup-websites.md)en BitLocker het apparaat van een gebruiker vergrendelt, kunnen ze onafhankelijk toegang krijgen tot hun computers. De Self-Service Portal heeft geen hulp nodig van helpdesk medewerkers.

[![Scherm afbeelding van standaard-BitLocker Self-Service Portal](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> Als u een herstel sleutel van de Self-Service Portal wilt ophalen, moet een gebruiker ten minste één keer zijn aangemeld bij de computer. Deze aanmelding moet lokaal zijn voor het apparaat, niet in een externe sessie. Als dat niet het geval is, moet u contact opnemen met de Help Desk voor sleutel herstel. Een helpdesk beheerder kan de [website beheer en controle](helpdesk-portal.md) gebruiken om de herstel sleutel aan te vragen.

Met BitLocker kan het apparaat in de volgende situaties worden vergrendeld:

- De gebruiker heeft het wacht woord of de pincode van BitLocker verg eten

- Er is een wijziging in de besturingssysteem bestanden, het BIOS of de Trusted Platform Module (TPM) van het apparaat

De BitLocker-herstel sleutel aanvragen bij de Self-Service Portal:

1. Wanneer BitLocker een apparaat vergrendelt, wordt het BitLocker-herstel scherm tijdens het opstarten weer gegeven. Noteer de BitLocker-herstel sleutel-ID van 32 cijfers.

1. Ga op een andere computer naar de Self-Service Portal in de webbrowser, bijvoorbeeld `https://webserver.contoso.com/SelfService` .

1. Lees en accepteer de kennisgeving.

1. Voer in het veld **herstel sleutel-id** de eerste acht cijfers van de BitLocker-herstel sleutel-id in. Als deze overeenkomt met meerdere sleutels, voert u alle 32 cijfers in.

1. Kies een van de volgende opties voor de **reden** voor deze aanvraag:

    - BIOS/TPM gewijzigd
    - Het besturings systeem is gewijzigd
    - Verloren pincode/wachtwoordzin

1. Selecteer **sleutel ophalen**. In de Self-Service Portal wordt de BitLocker- **herstel sleutel**van 48 cijfers weer gegeven.

1. Voer deze code van 48 cijfers in het scherm BitLocker-herstel op uw computer in.

> [!NOTE]
> De BitLocker Self-Service Portal kan een time-out hebben na een periode van inactiviteit. Zo kan na vijf minuten een waarschuwing met een time-out worden weer gegeven met een teller van 60 seconden.
>
> ![Waarschuwing time-out voor BitLocker Self-Service Portal](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Als u niet op de aftelling reageert, verloopt de sessie.
>
> ![Pagina met verlopen van BitLocker Self-Service Portal-sessie](media/bitlocker-self-service-portal-session-expired.png)
