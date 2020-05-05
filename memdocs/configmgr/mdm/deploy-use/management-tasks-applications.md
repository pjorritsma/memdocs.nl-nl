---
title: Apps beheren voor on-premises MDM
titleSuffix: Configuration Manager
description: Toepassingen beheren voor on-premises Mobile Device Management (MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 693f661f2a2db59335ec8e463842a0ad03c977f3
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721911"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Apps beheren voor on-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u apparaten beheert met Configuration Manager on-premises Mobile Device Management (MDM), kunt u de volgende toepassings typen beheren:

- Windows Phone-app-pakket (XAP-bestand)
- Windows Phone-app-pakket (in de Windows Phone Store)
- Windows Installer via MDM
- Webtoepassing

Zie [Beheer taken voor Configuration Manager toepassingen](../../apps/deploy-use/management-tasks-applications.md)voor meer algemene informatie over het beheren van Configuration Manager toepassingen en implementatie typen.

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>Windows Phone-toepassing maken

Een Configuration Manager toepassing heeft een of meer implementatie typen. Het implementatie type bevat de installatie bestanden en informatie die nodig is voor het implementeren van software op een apparaat. Een implementatie type bevat ook regels die aangeven wanneer en hoe de software wordt geïmplementeerd.

Zie [een toepassing maken](../../apps/deploy-use/create-applications.md#bkmk_create)voor de algemene stappen voor het maken van een app en implementatie typen.

Configuration Manager ondersteunt de volgende app-bestands typen voor Windows Mobile-apparaten:

|Apparaattype|Ondersteunde bestandstypen|
|-----------------|---------------------|
|Windows Phone 8|XAP|
|Windows Phone 8.1|XAP, appx, appxbundle|
|Windows 10 Mobile|XAP, appx, appxbundle|

Implementeer Windows Phone-apps als **beschikbaar** of **vereist**. Gebruik ook implementaties om apps te verwijderen.

## <a name="deploy-and-monitor-apps"></a>Apps implementeren en bewaken

Toepassingen voor mobiele apparaten implementeren en bewaken in Configuration Manager hetzelfde als voor andere apparaten, zoals Desk tops en servers. Raadpleeg voor meer informatie de volgende artikelen:

- [Toepassingen implementeren](../../apps/deploy-use/deploy-applications.md)
- [Toepassingen bewaken](../../apps/deploy-use/monitor-applications-from-the-console.md)

Bekijk de volgende beperkingen die specifiek zijn voor mobiele apparaten:

- Door MDM Inge schreven apparaten bieden geen ondersteuning voor gesimuleerde implementaties, gebruikers ervaring of plannings instellingen.

- Voeg niet meer dan 100 land instellingen toe aan één app. Met deze actie wordt voor komen dat de app op het apparaat wordt geïnstalleerd.

## <a name="next-step"></a>Volgende stap

Als u wijzigingen wilt aanbrengen, een geïmplementeerde toepassing wilt verwijderen of vervangen door een nieuwe toepassing, kunt u deze hetzelfde beheren als elke app in Configuration Manager. Zie [toepassingen bijwerken en buiten gebruik stellen](../../apps/deploy-use/update-and-retire-applications.md)voor meer informatie.
