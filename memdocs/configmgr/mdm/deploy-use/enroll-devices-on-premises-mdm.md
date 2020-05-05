---
title: Apparaten inschrijven voor on-premises MDM
titleSuffix: Configuration Manager
description: Meer informatie over methoden voor het inschrijven van apparaten voor on-premises Mobile Device Management (MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720672"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Apparaten inschrijven voor on-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u apparaten wilt beheren met Configuration Manager on-premises Mobile Device Management (MDM), moet u deze eerst registreren. Vervolgens kunnen Configuration Manager met de apparaten communiceren voor beheer taken. Configuration Manager biedt twee methoden voor het inschrijven van apparaten:

- **Gebruikers registratie**: gebruikers starten het inschrijvings proces op hun apparaat. Voor een geslaagde gebruikers registratie installeert u het vertrouwde basis certificaat op het apparaat en richt u de gebruiker in voor inschrijving in client instellingen. De gebruiker hoeft alleen hun referenties in te voeren om een apparaat in te schrijven.

    Zie [hoe gebruikers apparaten inschrijven](user-enroll-devices-on-premises-mdm.md)voor meer informatie.

- **Bulk inschrijving**: de gebruiker van het apparaat start de inschrijving niet. U maakt een pakket voor bulk inschrijving in Configuration Manager. Wanneer u het opent op het apparaat, bevat het pakket de vereiste informatie voor het inschrijven van het apparaat.

    Zie [apparaten bulksgewijs inschrijven](bulk-enroll-devices-on-premises-mdm.md)voor meer informatie.

Zie [ondersteunde configuraties](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)voor meer informatie over de versies van het besturings systeem die Configuration Manager ondersteunt voor het inschrijven van apparaten in on-premises MDM.
