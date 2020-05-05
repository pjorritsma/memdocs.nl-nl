---
title: Windows-service
titleSuffix: Configuration Manager
description: Gebruik service Windows om te bepalen wanneer Configuration Manager-sites updates installeren.
ms.date: 01/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 669da2a04fe4e94b08fc426c32e0dbcc804a21d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719111"
---
#  <a name="service-windows-for-site-servers"></a>Servicewindows voor siteservers

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt service Windows op centrale beheer sites en primaire sites configureren om te bepalen wanneer de updates in de console kunnen worden geïnstalleerd.  U kunt meerdere vensters configureren, met het venster dat is toegestaan voor het installeren van updates die wordt bepaald door een combi natie van alle service vensters voor die site server.

Wanneer er geen service venster is geconfigureerd:
- **Op de site op het hoogste niveau** (een centrale beheer site of een zelfstandige primaire site) kunt u kiezen wanneer u de installatie van de update wilt starten.
- **Op een onderliggende primaire site**wordt de update automatisch geïnstalleerd nadat de installatie van de update is voltooid op de centrale beheer site.
- **Op een secundaire site**worden updates nooit automatisch gestart. In plaats daarvan moet u de installatie van de update hand matig starten vanuit de-console nadat de update is geïnstalleerd op de bovenliggende primaire site.

Wanneer een service venster is geconfigureerd:
- **Op de site op de bovenste laag**kunt u de installatie van een nieuwe update niet starten vanuit de Configuration Manager-console. Zelfs als er een service venster is geconfigureerd, worden updates automatisch gedownload door de site, zodat deze gereed zijn om te worden geïnstalleerd.  
- **Op een onderliggende primaire site**worden updates die zijn geïnstalleerd op een centrale beheer site gedownload naar de primaire site, maar niet automatisch gestart. U kunt de installatie van een update niet hand matig starten tijdens een tijd die wordt geblokkeerd door het gebruik van een service venster. Op het moment dat de service Windows de installatie van de update niet langer blokkeert, wordt de installatie van de update automatisch gestart.
- **Secundaire sites** bieden geen ondersteuning voor service vensters en installeren updates niet automatisch. Nadat op de primaire bovenliggende site van een secundaire site een update is geïnstalleerd, kunt u de update van de secundaire site vanuit de-console starten.

## <a name="to-configure-a-service-window"></a>Een service venster configureren

1.  Open **beheer** > **site configuratie** > **sites**in Configuration Manager-console en selecteer vervolgens de site server waarvoor u een service venster wilt configureren.  

2.  Bewerk vervolgens de waarden bij **Eigenschappen** voor de siteservers en selecteer het tabblad **Servicewindow**. Hier kunt u een of meer servicewindows voor de betreffende siteserver instellen.  
