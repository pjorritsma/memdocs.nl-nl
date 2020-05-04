---
title: Toepassingen importeren en exporteren
titleSuffix: Configuration Manager
description: Meer informatie over het importeren en exporteren van toepassingen in Configuration Manager om te delen tussen afzonderlijke hiërarchieën.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4ed1c10e23b75dc4478a0409d197015c98aff8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710214"
---
# <a name="import-and-export-applications"></a>Toepassingen importeren en exporteren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik Configuration Manager om toepassingen tussen twee hiërarchieën te importeren en te exporteren. Kopieer bijvoorbeeld een toepassing vanuit een test omgeving naar een productie omgeving.

## <a name="export"></a>Exporteren

1. Selecteer in de Configuration Manager-console het knoop punt **toepassingen** . Kies in de groep maken van het lint de optie **toepassing exporteren**.
1. Geef in het scherm **Algemeen** een pad op naar een nieuw zip-bestand waarnaar u wilt exporteren. Geef desgewenst op of u *afhankelijkheden, vervangings relaties, voor waarden en virtuele omgevingen*wilt exporteren, evenals *de inhoud voor de geselecteerde toepassingen en afhankelijkheden*.  Voer indien gewenst beheerders opmerkingen in en selecteer **volgende**.
1. Controleer of de toepassing en eventuele afhankelijkheden worden weer gegeven op de pagina **Verwante objecten** en selecteer **volgende**.
1. Selecteer **volgende**op de pagina samen vatting.
1. Zodra het proces is voltooid, wordt het ZIP-bestand gemaakt en kunt u de wizard sluiten.

> [!IMPORTANT]
> Als u deze toepassing wilt kopiëren naar een andere omgeving, neemt u het ZIP-bestand en de map op. Het ZIP-bestand moet zich in dezelfde map bevinden als de map gemaakt.

## <a name="import"></a>Importeren

> [!NOTE]
> U kunt alleen toepassingen uit UNC-paden importeren, maar niet rechtstreeks importeren vanaf uw lokale schijf.

1. Selecteer in de Configuration Manager-console het knoop punt **toepassingen** . Kies in de groep maken van het lint de optie **toepassing importeren**.
1. Kies het ZIP-bestand dat u wilt importeren en selecteer **volgende**.
1. In het venster bestands inhoud ziet u wat er gebeurt wanneer u de toepassing importeert. Selecteer **Volgende**.
1. Controleer het scherm samen vatting en selecteer **volgende**.
1. Sluit de wizard. De toepassing is nu beschikbaar in de-site.

## <a name="see-also"></a>Zie ook
 
Automatiseer het importeren en exporteren van toepassingen met behulp van Power shell.

* [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Exporteren-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
