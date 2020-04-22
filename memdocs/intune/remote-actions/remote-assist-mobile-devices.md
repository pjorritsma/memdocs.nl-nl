---
title: Extern beheer voor mobiele apparaten die worden beheerd met Intune
description: Er zijn vier verschillende opties om gebruikers op afstand te helpen met hun mobiele apparaten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 548f63dcbd1635c106573fda40f8cc7bf312866e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086647"
---
# <a name="remotely-assist-mobile-devices-managed-by-microsoft-endpoint-manager"></a>Extern beheer voor apparaten die worden beheerd door Microsoft Endpoint Manager

Er zijn vier opties beschikbaar waarmee apparaten die worden beheerd door Microsoft Endpoint Manager op afstand kunnen worden beheerd:

- [Microsoft Teams](https://products.office.com/microsoft-teams/) is de hub voor teamwork waar u kunt chatten, ontmoeten en samenwerken, waar u ook bent.
- [Quick Assist](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) is een Windows 10-toepassing waarmee twee personen een apparaat kunnen delen via een externe verbinding.
- [TeamViewer](https://www.teamviewer.com/) is een programma van derden dat u afzonderlijk aanschaft. Het biedt een uitgebreide set mogelijkheden voor externe toegang en ondersteuning. De integratie van Intune en [TeamViewer](teamviewer-support.md) biedt externe ondersteuning via TeamViewer en de connector wordt rechtstreeks in Intune beheerd.
- [Extern beheer](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) is geïntegreerd in van Microsoft Endpoint Configuration Manager. Het wordt gebruikt om werkgroepcomputers of computers die lid zijn van een domein op afstand te beheren, te ondersteunen of te bekijken.

| Functies, platformen, licenties | **Teams** | Quick Assist | TeamViewer (Intune) | Extern beheer (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Externe weergave en beheer |![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Chat |![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Bestandsoverdracht |![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Beheerderstoegang met verhoogde bevoegdheden |||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Onbeheerde toegang |||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Gelijktijdig extern beheer |![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Ondersteuning voor meerdere gebruikers |||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Externe acties ||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Ondersteuning via internet |![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Auditrapportage |![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Ondersteuning voor alle platformen (Windows, iOS, Android, macOS) |![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Geïntegreerd met Windows 10: er is geen aanvullende app vereist ||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Vereist co-beheer door Configuration Manager en Intune voor het apparaat ||||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Vereist aanvullende licenties\* |![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)||![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|![Vinkje](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Voor Teams zijn O365- of M365-licenties vereist. Het gebruik van TeamViewer en Intune vereist licenties vanuit zowel TeamViewer als Intune. Extern beheer is een functie van Configuration Manager en vereist Configuration Manager-licenties.
