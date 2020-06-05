---
title: Include-bestand
description: Include-bestand
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347243"
---
## <a name="apple-device-network-information"></a>Netwerkgegevens voor Apple-apparaten

|**Gebruikt voor**|**Hostnaam (IP-adres/subnet)**|**Protocol**|**Poort**|
|------------|-----------|------------|-----------|
|Inhoud van Apple-servers ophalen en weergeven|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|Communicatie met APNS-servers|#-courier.push.apple.com<br># is een willekeurig getal van 0 tot en met 50.|TCP|5223 en 443|
|Verschillende functies waaronder toegang tot internet, de iTunes Store, de macOS App Store, iCloud, berichten, enzovoort.|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 of 443|

Zie voor meer informatie:

- [TCP- en UDP-poorten die door Apple software worden gebruikt](https://support.apple.com/HT202944)
- [macOS, iOS/iPadOS en iTunes-server-hostverbindingen en achtergrondprocessen in iTunes](https://support.apple.com/HT201999)
- [Als u geen Apple pushberichten ontvangt in de macOS- en iOS-/iPadOS-clients](https://support.apple.com/HT203609)