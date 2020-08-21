---
title: Vereisten voor rapportage
titleSuffix: Configuration Manager
description: Krijg inzicht in verschillende afhankelijkheden die van invloed zijn op uw gebruik van rapportage in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b082ae578052a92c0afacd3d1f62fdb2e21bd6d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699531"
---
# <a name="prerequisites-for-reporting-in-configuration-manager"></a>Vereisten voor rapportage in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Rapportage in Configuration Manager heeft de volgende afhankelijkheden:

- SQL Server Reporting Services
- Reporting Services-punt
- Power BI Report Server (optioneel, vanaf versie 2002)

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Voordat u rapportage in Configuration Manager kunt gebruiken, moet u SQL Server Reporting Services installeren en configureren.

Zie de [Install SQL Server Reporting Services](/sql/reporting-services/install-windows/install-reporting-services)voor meer informatie over het plannen en implementeren van Reporting Services.

Installeer de Reporting Services-Data Base op het standaard exemplaar of een benoemd exemplaar van een 64-bits SQL Server-installatie. Plaats de SQL Server-instantie met de site systeem server of configureer deze op een externe computer.

Configuration Manager ondersteunt dezelfde versies van SQL Server voor rapportage als voor de site database. Zie [ondersteunde versies van SQL Server](../../plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions)voor meer informatie.

## <a name="reporting-services-point"></a>Reporting Services-punt

Voordat u rapportage in Configuration Manager kunt gebruiken, moet u de site systeemrol van het Reporting Services-punt configureren.

Zie voor meer informatie [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012RSpoint) (Vereisten voor sites en sitesystemen).

## <a name="power-bi-report-server"></a>Power BI Report Server

Vanaf versie 2002 kunt u de rapportage met Power BI Report Server integreren. Zie voor meer informatie, inclusief vereisten, [integreren met Power bi Report Server](powerbi-report-server.md).

## <a name="next-steps"></a>Volgende stappen

[Rapportage configureren](configuring-reporting.md)