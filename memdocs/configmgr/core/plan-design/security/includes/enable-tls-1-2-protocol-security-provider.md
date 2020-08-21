---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: f14713431c71c1f3625d13ea4be1d919b072e273
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704227"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1,2 is standaard ingeschakeld. Daarom is er geen wijziging aan deze sleutels nodig om deze in te scha kelen. U kunt wijzigingen aanbrengen in het `Protocols` uitschakelen van tls 1,0 en tls 1,1 nadat u de overige instructies in deze artikelen hebt gevolgd en u hebt gecontroleerd of de omgeving werkt als alleen TLS 1,2 is ingeschakeld.

Controleer de `\SecurityProviders\SCHANNEL\Protocols` instelling van de registersubsleutel, zoals wordt weer gegeven in [Aanbevolen procedures voor trans port Layer Security (TLS) met de .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).