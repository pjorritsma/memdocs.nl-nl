---
title: Netwerkinfrastructuur
titleSuffix: Configuration Manager
description: Stel firewalls, poorten en domeinen in om Configuration Manager-communicatie voor te bereiden.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719839"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Aandachtspunten voor de netwerk infrastructuur voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u uw netwerk wilt voorbereiden op de ondersteuning van Configuration Manager, moet u mogelijk enkele infrastructuur onderdelen configureren. U kunt bijvoorbeeld firewall poorten openen om de communicaties door te geven die worden gebruikt door Configuration Manager.  

## <a name="ports-and-protocols"></a>Poorten en protocollen

Verschillende Configuration Manager-functies gebruiken verschillende netwerk poorten. Sommige poorten zijn vereist, wat u kunt aanpassen.

De meeste Configuration Manager Communications gebruiken algemene poorten zoals poort 80 voor HTTP of 443 voor HTTPS. Sommige site systeem rollen bieden ondersteuning voor het gebruik van aangepaste websites en aangepaste poorten. Zie [websites voor site systeem servers](websites-for-site-system-servers.md)voor meer informatie.

Voordat u Configuration Manager implementeert, moet u de poorten identificeren die u wilt gebruiken en zo nodig firewalls instellen.

Wanneer u Configuration Manager hebt geïnstalleerd en u een poort moet wijzigen, vergeet dan niet om firewalls op apparaten en het netwerk bij te werken. Wijzig ook de configuratie van de poort in Configuration Manager.

Raadpleeg voor meer informatie de volgende artikelen:

- [Clientcommunicatiepoorten configureren](../../clients/deploy/configure-client-communication-ports.md)
- [Poorten die worden gebruikt in Configuration Manager](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>Vereisten voor internettoegang

Sommige Configuration Manager functies zijn afhankelijk van Internet connectiviteit voor volledige functionaliteit. Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u ervoor zorgen dat de benodigde eind punten zijn toegestaan.

Zie [vereisten voor Internet toegang](internet-endpoints.md) voor meer informatie.


## <a name="proxy-servers"></a>Proxyservers

U kunt afzonderlijke proxy servers opgeven voor verschillende site systeem servers en clients. U maakt deze configuraties tijdens het installeren van een site systeemrol of client, of u kunt ze later indien nodig wijzigen.

Zie [ondersteuning voor proxy server](proxy-server-support.md)voor meer informatie.
