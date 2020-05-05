---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720532"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

TLS 1,2 is standaard ingeschakeld. Daarom is er geen wijziging aan deze sleutels nodig om deze in te scha kelen. U kunt wijzigingen aanbrengen `Protocols` in het uitschakelen van TLS 1,0 en TLS 1,1 nadat u de overige instructies in deze artikelen hebt gevolgd en u hebt gecontroleerd of de omgeving werkt als alleen TLS 1,2 is ingeschakeld.

Controleer de `\SecurityProviders\SCHANNEL\Protocols` instelling van de registersubsleutel, zoals wordt weer gegeven in [Aanbevolen procedures voor trans port Layer Security (TLS) met de .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

