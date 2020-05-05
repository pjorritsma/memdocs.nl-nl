---
title: Niet-nalevingscodes
titleSuffix: Configuration Manager
description: Een technische Naslag informatie voor de mogelijke codes van een Configuration Manager-client die niet compatibel is met het BitLocker-beleid
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6c28fa29-fc97-49ef-9fc3-cb062bdba908
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e8ee130929605f8087eb7fbef55e8a27618c3aed
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722051"
---
# <a name="non-compliance-codes"></a>Niet-nalevingscodes

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3601034-->

WMI op de client biedt de volgende niet-nalevings codes. Ook worden de redenen beschreven waarom een bepaald apparaat rapporteert als niet-compatibel.

Er zijn verschillende methoden om WMI weer te geven. Gebruik bijvoorbeeld de volgende Power shell-opdracht:

``` PowerShell
(Get-WmiObject -Class mbam_Volume -Namespace root\microsoft\mbam).ReasonsForNoncompliance
```

> [!TIP]
> Als het apparaat compatibel is, retourneert deze opdracht niets.
>
> U kunt ook het `Compliant` kenmerk van deze klasse controleren. Dit is `1` het geval als het apparaat compatibel is.

|Niet-nalevings code|Reden voor niet-naleving|
|--- |--- |
|0|Codeer sterkte niet AES 256.|
|1|Voor het BitLocker-beleid moet dit volume worden versleuteld, maar dit is niet het geval.|
|2|Voor het BitLocker-beleid moet dit volume *niet* worden versleuteld, maar het is.|
|3|Voor het BitLocker-beleid moet dit volume een TPM-beveiliging gebruiken, maar dit is niet het geval.|
|4|Voor het BitLocker-beleid moet dit volume gebruikmaken van een TPM + pincode-Protector, maar dit is niet het geval.|
|5|Het BitLocker-beleid staat niet toe dat niet-TPM-computers als compatibel rapporteren.|
|6|Het volume heeft een TPM-beveiliging, maar de TPM is niet zichtbaar.|
|7|Voor het BitLocker-beleid is vereist dat dit volume een wachtwoord beveiliging gebruikt, maar er is er geen.|
|8|Het BitLocker-beleid vereist dat dit volume *geen* wachtwoord beveiliging gebruikt, maar heeft er een.|
|9|Voor het BitLocker-beleid is vereist dat dit volume een automatische ontgrendelings beveiliging gebruikt, maar het is niet een.|
|10|Voor het BitLocker-beleid is vereist dat dit volume *geen* automatische Ontgrendel beveiliging gebruikt, maar het is er een.|
|11|BitLocker detecteert een beleids conflict, waardoor dit volume niet kan worden gerapporteerd als compatibel.|
|12|Er is een systeem volume nodig om het volume van het besturings systeem te versleutelen, maar dit is niet aanwezig.|
|13|De beveiliging is onderbroken voor het volume.|
|14|Beveiliging voor automatisch ontgrendelen is onveilig tenzij het volume van het besturings systeem is versleuteld.|
|15|Het beleid vereist een minimale coderings-sterkte is XTS-AES-128 bits, de werkelijke coderings-sterkte is zwakker.|
|16|Het beleid vereist een minimale coderings-sterkte is XTS-AES-256 bits, de werkelijke coderings-sterkte is zwakker.|
