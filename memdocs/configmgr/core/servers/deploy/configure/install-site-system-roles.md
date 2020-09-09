---
title: Sitesysteemrollen installeren
titleSuffix: Configuration Manager
description: Voeg site systeem rollen toe aan een bestaande of nieuwe site systeem server in de site.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8cb16b6fd703142e0c3c6400403207976b4208f5
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607572"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Site systeem rollen voor Configuration Manager installeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

De Configuration Manager-console bevat twee methoden voor het installeren van site systeem rollen:

- **Site systeem rollen toevoegen**: Voeg site systeem rollen toe aan een bestaande site systeem server in de site.

- **Site systeem server maken**: Geef een nieuwe server op als een site systeem server en installeer vervolgens een of meer rollen. Deze methode is hetzelfde als de **site systeem rollen toevoegen**, met uitzonde ring van de eerste pagina. U geeft eerst de naam op van de server en de site waarop u deze wilt installeren.

> [!TIP]
> Wanneer u een functie op een externe computer installeert, voegt Configuration Manager het computer account van de externe computer toe aan een lokale groep op de site server.
>
> Wanneer u de site op een domein controller installeert, is de groep op de site server een domein groep in plaats van een lokale groep. In dit geval werkt de externe site systeemrol niet meteen. De site systeem server moet opnieuw worden opgestart of u kunt het Kerberos-ticket voor het computer account van de externe server vernieuwen. Zie [accounts used](../../../plan-design/hierarchy/accounts.md)(Engelstalig) voor meer informatie.

Voordat de site systeemrol wordt geïnstalleerd, controleert Configuration Manager de doel computer om te controleren of deze voldoet aan de vereisten voor de geselecteerde rollen.

Wanneer Configuration Manager een site systeemrol installeert, worden de bestanden standaard geïnstalleerd op het eerste beschik bare schijf station met NTFS-indeling dat de meeste beschik bare vrije schijf ruimte heeft. Om te voor komen dat Configuration Manager op specifieke stations installeert voordat u de site systeem server installeert, maakt u een leeg bestand met de naam **no_sms_on_drive. SMS** in de hoofdmap van het station.

Configuration Manager gebruikt het **installatie account van het site systeem** om functies te installeren. U geeft dit account op wanneer u de functie installeert. Dit account is standaard het lokale systeem account van de site Server computer. U kunt een domein gebruikers account opgeven als installatie account voor het site systeem. Zie [accounts-site systeem installatie account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)voor meer informatie.

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> Rollen installeren op een bestaande site systeem server

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer het knoop punt **servers en site systeem rollen** . Selecteer de bestaande site systeem server waarop u nieuwe site systeem rollen wilt installeren.

1. Selecteer op het lint op het tabblad **Start** in de groep **Server** de optie **site systeem rollen toevoegen**.

1. Controleer de instellingen op de pagina **Algemeen** .

    > [!TIP]
    >  Als u de site systeemrol van Internet wilt openen, moet u een Internet Fully Qualified Domain Name (FQDN) opgeven.

1. Als op de pagina **proxy** de functies op deze server een Internet proxy vereisen, geeft u instellingen voor een proxy server op. Zie [ondersteuning voor proxy server](../../../plan-design/network/proxy-server-support.md)voor meer informatie.

1. Selecteer op de pagina **selectie van systeem** rollen de site systeem rollen die u wilt toevoegen.

1. Voltooi de wizard. Er kunnen extra pagina's voor specifieke rollen worden weer gegeven. Zie [configuratie opties voor site systeem rollen](configuration-options-for-site-system-roles.md)voor meer informatie.

> [!TIP]
> De Windows Power shell-cmdlet **New-CMSiteSystemServer**voert dezelfde functie uit als deze procedure. Zie [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver)voor meer informatie.

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> Rollen installeren op een nieuwe site systeem server

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer het knoop punt **servers en site systeem rollen** .

1. Selecteer in het lint op het tabblad **Start** in de groep **maken** de optie **site systeem server maken**.

1. Geef op de pagina **Algemeen** de algemene instellingen voor het site systeem op.

    > [!TIP]
    > Zorg ervoor dat u een Internet-FQDN opgeeft om toegang te krijgen tot de nieuwe site systeemrol van het internet.

1. Als op de pagina **proxy** de functies op deze server een Internet proxy vereisen, geeft u instellingen voor een proxy server op. Zie [ondersteuning voor proxy server](../../../plan-design/network/proxy-server-support.md)voor meer informatie.

1. Selecteer op de pagina **selectie van systeem** rollen de site systeem rollen die u wilt toevoegen.

1. Voltooi de wizard. Er kunnen extra pagina's voor specifieke rollen worden weer gegeven. Zie [configuratie opties voor site systeem rollen](configuration-options-for-site-system-roles.md)voor meer informatie.

> [!TIP]
> De Windows Power shell-cmdlet **New-CMSiteSystemServer**voert dezelfde functie uit als deze procedure. Zie [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- [Configuratieopties voor sitesysteemrollen](configuration-options-for-site-system-roles.md)

- [Rol verwijderen](../install/uninstall-sites-and-hierarchies.md#bkmk_role)