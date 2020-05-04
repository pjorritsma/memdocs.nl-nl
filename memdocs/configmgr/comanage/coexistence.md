---
title: Co-existentie met een MDM-service van derden
titleSuffix: Configuration Manager
description: Meer informatie over het gebruik van een MDM-service van derden met Configuration Manager
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f22ba6f29e0c85e19ab66d1b052085db5303cc2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710823"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>MDM-samen werking van derden met Configuration Manager

Wanneer u Windows 10-apparaten gelijktijdig beheert met zowel Configuration Manager als Microsoft Intune, wordt deze functionaliteit [gezamenlijk](overview.md)beheerd. Wanneer u apparaten beheert met Configuration Manager en zich registreert bij een MDM-service van derden, wordt deze *functionaliteit naast elkaar genoemd.* Twee beheer instanties voor één apparaat kunnen lastig zijn als ze niet op de juiste wijze zijn verdeeld tussen de twee. Met co-beheer, Configuration Manager en intune balanceert u de [werk belastingen](workloads.md) om te controleren of er geen conflicten zijn. Deze interactie bestaat niet met services van derden, waardoor er beperkingen zijn met de beheer mogelijkheden van samen werking.

De Configuration Manager-client kan worden gecombineerd met een MDM-service van derden op een apparaat met Windows 10 versie 1709 of hoger, en dat is gekoppeld aan Azure Active Directory. Het apparaat kan een van de volgende typen zijn:

- Alleen [lid van Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) . (Dit type wordt soms aangeduid als lid van een Cloud domein)  

- [Hybride domein](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), waarbij het apparaat wordt gekoppeld aan uw on-premises Active Directory en is geregistreerd bij uw Azure Active Directory.  

> [!Note]  
> Het biedt geen ondersteuning voor [apparaten die persoonlijk eigendom zijn](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device).  

Wanneer de Configuration Manager-client detecteert dat een MDM-service van derden ook het apparaat beheert, worden bepaalde werk belastingen in Configuration Manager automatisch gedeactiveerd. Dit gedrag zorgt ervoor dat de MDM-service deze functies kan overnemen. Ook wordt voor komen dat er conflicterende instellingen op de client optreden die de gebruikers ervaring van het apparaat en de gebruiker mogelijk nadelig beïnvloeden. In dit geval worden de volgende werk belastingen in Configuration Manager gedeactiveerd:

- Toegangs beleid voor bronnen voor VPN-, Wi-Fi-, e-mail-en certificaat instellingen
- Toepassings beheer, inclusief verouderde pakketten
- Scans en installatie van software-updates
- Endpoint Protection, de Windows Defender-suite van antimalware Protection-functies
- Nalevings beleid voor voorwaardelijke toegang
- Apparaatconfiguratie
- Office klik-en-klaar beheer

De Configuration Manager-client voor komt conflicten met de beheer instantie van derden door door te gaan met de volgende alleen-lezen bewerkingen:

- Hardware- en software-inventaris
- Asset Intelligence
- Softwarelicentiecontrole
- Rapportage van energie beheer

Zie voor [delen van co-beheer](overview.md#benefits)voor meer informatie over de voor delen van co-beheer met Configuration Manager en intune.
