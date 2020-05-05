---
title: Hoe gebruikers apparaten inschrijven
titleSuffix: Configuration Manager
description: Begrijp hoe gebruikers apparaten inschrijven met on-premises Mobile Device Management (MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722331"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Hoe gebruikers apparaten inschrijven met on-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met Configuration Manager on-premises Mobile Device Management (MDM) kunnen gebruikers hun apparaten inschrijven. Er zijn twee vereisten:

- Met client instellingen verleent u de gebruiker toestemming om zich in te schrijven.

- U installeert het vereiste vertrouwde basis certificaat op het apparaat.

Zie [apparaatregistratie instellen voor on-premises MDM](../get-started/set-up-device-enrollment-on-premises-mdm.md)voor meer informatie over het instellen van de inschrijving.

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>Windows 10 registreren

1. Ga op een computer met Windows 10 naar **Instellingen**.

1. Selecteer **accounts**en selecteer vervolgens **toegang tot werk of school**.

1. Selecteer **verbinding maken**, voer uw User Principal Name (UPN) in en selecteer **door gaan**. De UPN kan hetzelfde zijn als uw e-mail adres, bijvoorbeeld jdoe@contoso.com.

1. Voer de Fully Qualified Domain Name (FQDN) van het inschrijvings proxy punt in en selecteer **door gaan**.

1. Voer uw wacht woord in en selecteer **Aanmelden**.

1. Windows hoeft de aanmeldings gegevens voor deze actie niet te onthouden, dus Selecteer **overs Laan**.

Na een korte periode wordt het apparaat Inge schreven bij Configuration Manager.

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>Windows 10 Mobile inschrijven

1. Ga op een apparaat met Windows 10 Mobile naar **Instellingen**.

1. Selecteer **accounts**en selecteer vervolgens **toegang via het werk netwerk**.

1. Selecteer **Verbinden**.

1. Voer uw UPN en de FQDN van het inschrijvings proxy punt in. Selecteer vervolgens **Verbinding maken**.

1. Voer op het volgende scherm uw UPN en wacht woord in en selecteer vervolgens **Aanmelden**.

Na een korte periode wordt het apparaat Inge schreven bij Configuration Manager. Selecteer **Done**.

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>Inschrijving verifiëren

Gebruik de Configuration Manager-console om te controleren of de apparaten zijn Inge schreven. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer **apparaten**. Blader of zoek naar het geregistreerde apparaat in de lijst met apparaten.
