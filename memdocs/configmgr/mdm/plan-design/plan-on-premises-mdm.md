---
title: On-premises MDM plannen
titleSuffix: Configuration Manager
description: On-premises Mobile Device Management plannen voor het beheren van mobiele apparaten in Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 60139e3e26195f2feb8b5533c1d26e3e8fb8c3d0
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693740"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>On-premises MDM plannen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Er zijn verschillende belang rijke gebieden die u kunt controleren wanneer u van plan bent om on-premises Mobile Device Management (MDM) in Configuration Manager te implementeren:

- Ondersteunde apparaten en versies van besturings systemen
- Vereiste sitesysteemrollen
- Beveiligde communicatie
- Apparaatinschrijving

> [!IMPORTANT]
> Terwijl de site of een mobiel apparaat geen verbinding maakt met Microsoft Intune, heeft uw organisatie nog steeds intune-licenties nodig om deze functie te gebruiken. Zie [Microsoft intune Licensing](/intune/fundamentals/licenses)voor meer informatie.

Houd rekening met de volgende vereisten voordat u de Configuration Manager-infra structuur voorbereidt op het verwerken van on-premises MDM.

## <a name="supported-devices"></a><a name="bkmk_devices"></a> Ondersteunde apparaten  

De huidige vertakking van Configuration Manager ondersteunt inschrijving in on-premises Mobile Device Management voor apparaten met Windows 10. Deze apparaattypen bevatten voornamelijk laptops, IoT en Surface Hub. Zie [ondersteunde versies van besturings systemen voor clients en apparaten](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)voor meer informatie en de lijst met specifieke edities.

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Site systeem rollen

On-premises MDM vereist ten minste één van de volgende site systeem rollen:

- **Proxypunt voor inschrijving** voor de ondersteuning van inschrijvingsaanvragen.

- **Inschrijvingspunt** voor de ondersteuning van apparaatinschrijving.

- **Apparaatbeheerpunt** voor de levering van het beleid. Deze rol is een variant van het beheer punt, maar staat Mobile Device Management toe.

- **Distributiepunt** voor de levering van inhoud.

Afhankelijk van de behoeften van uw organisatie, kunt u deze rollen op de enkele server of afzonderlijk op verschillende servers installeren.

> [!NOTE]
> U moet elke rol configureren die wordt gebruikt voor on-premises MDM als een HTTPS-eind punt voor communicatie met vertrouwde apparaten. Zie [Vereiste vertrouwde communicatie](#bkmk_trustedComs) voor meer informatie.

Zie voor meer algemene informatie [plannen voor site systeem servers en-rollen](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a> Vertrouwde communicatie

Voor on-premises MDM moet u site systeem rollen inschakelen voor HTTPS-communicatie. Afhankelijk van uw behoeften kunt u de certificerings instantie (CA) van uw organisatie gebruiken om de vertrouwde verbindingen tussen servers en apparaten tot stand te brengen. U kunt ook een openbaar beschik bare CA gebruiken als vertrouwde instantie. In beide gevallen moet u de volgende certificaten configureren:

- Een **webserver certificaat** in IIS op de servers die als host fungeren voor de vereiste site systeem rollen. Als één server als host fungeert voor meerdere site systeem rollen, hebt u slechts één certificaat voor die server nodig. Als elke rol zich op een afzonderlijke server bevindt, moet elke server een afzonderlijk certificaat hebben.

- Het **vertrouwde basis certificaat** van de certificerings instantie die de webserver certificaten uitgeeft. Installeer dit basis certificaat op alle apparaten die verbinding moeten maken met de site systeem rollen.

Zie [certificaten voor vertrouwde communicatie instellen in on-premises MDM](../get-started/set-up-certificates-on-premises-mdm.md)voor meer informatie.

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a> Registratie van apparaten

Apparaatregistratie inschakelen voor on-premises MDM:

- Gebruikers toestemming geven om zich te registreren via client instellingen

- Apparaten configureren voor vertrouwde communicatie met de site systeem servers die als host fungeren voor de vereiste rollen

Als alternatief voor door de gebruiker geïnitieerde registratie kunt u een pakket voor bulk inschrijving instellen. Met dit pakket kan het apparaat worden inge schreven zonder tussen komst van de gebruiker. Levering van het pakket aan het apparaat voordat het is ingericht voor gebruik of nadat het het OOBE-proces heeft door lopen.

Zie [registratie van apparaten instellen voor on-premises MDM](../get-started/set-up-device-enrollment-on-premises-mdm.md)voor meer informatie.

## <a name="next-step"></a>Volgende stap

> [!div class="nextstepaction"]
> [Sitesysteemrollen installeren](../get-started/install-site-system-roles-for-on-premises-mdm.md)