---
title: Problemen met BitLocker oplossen
titleSuffix: Configuration Manager
description: Meer informatie over het oplossen van problemen met BitLocker-beheer in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ed8e464e0ab7c17e87e3de2bf72aa0dfb0acd071
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723920"
---
# <a name="troubleshoot-bitlocker"></a>Problemen met BitLocker oplossen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de informatie in dit artikel voor hulp bij het oplossen van problemen met BitLocker-beheer in Configuration Manager.

## <a name="server-error-in-self-service"></a>Server fout in self-service

Wanneer u de Self-Service Portal (`https://webserver.contoso.com/SelfService`) voor de eerste keer probeert te openen, wordt het volgende fout bericht weer gegeven:

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

Als u dit probleem wilt oplossen, moet u de [vereiste](../../plan-design/bitlocker-management.md#prerequisites) voor **micro soft ASP.NET MVC 4,0** op de webserver installeren.

## <a name="see-also"></a>Zie ook

Zie [BitLocker-gebeurtenis logboeken](about-event-logs.md)voor meer informatie over het gebruik van BitLocker-gebeurtenis Logboeken.

Raadpleeg de volgende artikelen voor een lijst met bekende fouten en mogelijke oorzaken voor gebeurtenis logboek vermeldingen:

- [Clientgebeurtenislogboeken](client-event-logs.md)
- [Servergebeurtenislogboeken](server-event-logs.md)

Zie [niet-nalevings codes](non-compliance-codes.md)voor meer informatie waarom clients rapporteren die niet compatibel zijn met het beheer beleid van BitLocker.
