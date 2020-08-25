---
title: Tenant koppelen/Endpoint Security-antivirus beleid implementeren vanuit het micro soft Endpoint Manager-beheer centrum (preview)
titleSuffix: Configuration Manager
description: " Micro soft Defender anti virus-beleid maken en implementeren vanuit de micro soft Endpoint Manager-console en voor Configuration Manager-verzamelingen."
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 07379821-02b3-4c61-af03-329c782e10d6
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d09b519bfc116afd397d455c6a03a8748f9303cd
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88827019"
---
# <a name="tenant-attach-create-and-deploy-endpoint-security-antivirus-policy-from-the-admin-center-preview"></a><a name="bkmk_atp"></a> Tenant bijvoegen: beveiligings beleid voor Endpoint Security maken en implementeren vanuit het beheer centrum (preview-versie)
<!--5691658-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]
> Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt. 

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen in één console met de naam **micro soft Endpoint Manager-beheer centrum**. Maak micro soft Defender anti virus-beleid in de micro soft Endpoint Manager-console en implementeer deze in Configuration Manager-verzamelingen.


## <a name="prerequisites"></a>Vereisten

- Toegang tot het [micro soft Endpoint Manager-beheer centrum](https://endpoint.microsoft.com/).
- Een E5-licentie voor [micro soft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).
- Een omgeving waaraan een [Tenant is gekoppeld met geüploade apparaten](device-sync-actions.md).
- Mini maal Configuration Manager versie 2006 en de bijbehorende versie van de console zijn geïnstalleerd.
   - Voer een upgrade uit voor de doel apparaten naar de nieuwste versie van de Configuration Manager-client.
- Ten minste één Configuration Manager verzameling die [beschikbaar is voor het toewijzen van endpoint-beveiligings beleid](atp-onboard.md#bkmk_collections)

## <a name="supported-antivirus-profile-for-tenant-attached-devices"></a>Ondersteund antivirus profiel voor aan tenants gekoppelde apparaten

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](../../intune/protect/includes/configmgr-antivirus-profiles.md)]

## <a name="assign-antivirus-policies-to-a-collection"></a>Antivirus beleid toewijzen aan een verzameling

1. Ga in een browser naar [https://aka.ms/MDAVTenantAttachPreview](https://aka.ms/MDAVTenantAttachPreview) .
1. Selecteer **Endpoint Security** en vervolgens **anti virus**.
1. Selecteer **beleid maken**.
1. Voor het **platform**selecteert u **Windows 10 en Windows Server (ConfigMgr)**.
1. Voor het **profiel**selecteert u **micro soft Defender anti virus (preview)** en vervolgens **maken**.
1. Wijs een **naam** en eventueel een **Beschrijving** toe op de pagina **basis beginselen** .
1. Configureer op de pagina **Configuratie-instellingen** de instellingen die u met dit profiel wilt beheren. Wanneer u klaar bent met het configureren van instellingen, selecteert u **Volgende**. Zie [antivirus beleids instellingen voor aan tenants gekoppelde apparaten](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)voor meer informatie over het beschik bare beleid.
1. Wijs het beleid toe aan een Configuration Manager verzameling op de pagina **toewijzingen** .

## <a name="next-steps"></a>Volgende stappen

[Antivirus beleids instellingen voor aan de Tenant gekoppelde apparaten](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)