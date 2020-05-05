---
title: Transport Layer Security (TLS) 1,2 inschakelen op de site servers en externe site systemen
titleSuffix: Configuration Manager
description: Informatie over het inschakelen van TLS 1,2 voor Configuration Manager-site servers.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720546"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>TLS 1,2 inschakelen op de site servers en externe site systemen

*Van toepassing op: Configuration Manager (Current Branch)*

Wanneer u TLS 1,2 inschakelt voor uw Configuration Manager-omgeving, moet u eerst [tls 1,2 inschakelen voor de clients](enable-tls-1-2-client.md) . Schakel vervolgens TLS 1,2 in op de site servers en externe site systemen. Test tot slot de communicatie van de client naar site systeem voordat u de oudere protocollen aan de server zijde mogelijk uitschakelt. De volgende taken zijn nodig om TLS 1,2 in te scha kelen op de site servers en externe site systemen:

- Zorg ervoor dat TLS 1,2 is ingeschakeld als een protocol voor SChannel op het niveau van het besturings systeem
- De .NET Framework bijwerken en configureren ter ondersteuning van TLS 1,2
- SQL Server-en client onderdelen bijwerken
- Windows Server Update Services bijwerken (WSUS)

Zie [about TLS 1,2](enable-tls-1-2.md)(Engelstalig) voor meer informatie over afhankelijkheden voor specifieke Configuration Manager-functies en-scenario's. 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a>Zorg ervoor dat TLS 1,2 is ingeschakeld als een protocol voor SChannel op het niveau van het besturings systeem

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a>De .NET Framework bijwerken en configureren ter ondersteuning van TLS 1,2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a>SQL Server-en client onderdelen bijwerken

Microsoft SQL Server 2016 en hoger ondersteunen TLS 1,1 en TLS 1,2. Voor eerdere versies en afhankelijke bibliotheken zijn mogelijk updates vereist. Zie [KB 3135244: TLS 1,2-ondersteuning voor Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)voor meer informatie.

Secundaire site servers moeten ten minste SQL Server 2016 Express met Service Pack 2 (13.2.50.26) of hoger gebruiken.

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a>SQL Server Native Client

> [!NOTE]
> In [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) worden ook de vereisten voor SQL Server-client onderdelen beschreven.

Zorg ervoor dat u de SQL Server Native Client ook bijwerkt naar ten minste versie SQL 2012 SP4 (11. *. 7001.0). Vanaf versie 1810 is deze vereiste een controle op [vereisten (waarschuwing)](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client).

Configuration Manager gebruikt SQL Server Native Client op de volgende site systeem rollen:

- Sitedatabaseserver
- Site Server: centrale beheer site, primaire site of secundaire site
- Beheerpunt
- Apparaatbeheerpunt
- Statusmigratiepunt
- SMS-provider
- Software-updatepunt
- Multicast-distributiepunt
- Asset Intelligence Service punt bijwerken
- Reporting Services-punt
- Application Catalog-webservice
- Inschrijvingspunt
- Endpoint Protection-punt
- Serviceverbindingspunt
- Certificaatregistratiepunt
- Data Warehouse-service punt


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a>Windows Server Update Services bijwerken (WSUS)

Als u TLS 1,2 wilt ondersteunen in eerdere versies van WSUS, installeert u de volgende update op de WSUS-server:

- Voor WSUS-server met Windows Server 2012 installeert u [update 4022721](https://support.microsoft.com/help/4022721) of een update van een later pakket.
- Voor WSUS-server met Windows Server 2012 R2 installeert u [update 4022720](https://support.microsoft.com/help/4022720) of een update van een later pakket.

Vanaf Windows Server 2016 wordt TLS 1,2 standaard ondersteund voor WSUS.  TLS 1,2-updates zijn alleen nodig voor Windows Server 2012-en Windows Server 2012 R2 WSUS-servers.

## <a name="next-steps"></a>Volgende stappen

- [Algemene problemen bij het inschakelen van TLS 1.2](enable-tls-1-2-troubleshoot.md)
