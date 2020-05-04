---
title: Aanbevolen procedures voor verzamelingen
titleSuffix: Configuration Manager
description: Aanbevolen procedures voor verzamelingen in Configuration Manager ophalen.
ms.date: 09/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3e7b108ef48b218ee9d6a31064606b40a68fea
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714288"
---
# <a name="best-practices-for-collections-in-configuration-manager"></a>Aanbevolen procedures voor verzamelingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de volgende aanbevolen procedures voor verzamelingen in Configuration Manager.  

## <a name="dont-use-incremental-updates-with-many-collections"></a><a name="bkmk_incremental"></a>Gebruik geen incrementele updates met veel verzamelingen

Als u de optie **Incrementele updates gebruiken voor deze verzameling** activeert, kan deze configuratie beoordelingsvertragingen veroorzaken wanneer u deze voor veel verzamelingen inschakelt. De drempelwaarde is ongeveer 200 verzamelingen in uw hiërarchie. Het exacte aantal is afhankelijk van de volgende factoren:  

- Het totale aantal verzamelingen  

- De frequentie van nieuwe resources die worden toegevoegd en gewijzigd in de hiërarchie  

- Het aantal clients in uw hiërarchie  

- De complexiteit van de lidmaatschapsregels voor de verzamelingen in uw hiërarchie  

## <a name="maintenance-window-size-for-software-updates"></a>Grootte van onderhouds venster voor software-updates

U kunt onderhouds Vensters voor Apparaatsets configureren om de tijden te beperken dat Configuration Manager software op deze apparaten kan installeren. Als u het onderhouds venster te klein configureert, is het mogelijk dat de client essentiële software-updates niet kan installeren. Dit zorgt ervoor dat de client kwetsbaar is voor de aanval die wordt verholpen door de software-update.

> [!Tip]
> Belang rijke overwegingen voor het plannen van uw onderhouds Vensters:
>
> - De standaard waarde voor de maximale uitvoerings tijd van de software-update is 60 minuten.
> - Wanneer Configuration Manager berekent of een update kan worden geïnstalleerd, wordt er vijf minuten aan de maximale uitvoerings tijd toegevoegd om het systeem opnieuw op te starten.
> - De resterende duur van een onderhouds venster moet langer zijn dan de maximale uitvoerings tijd van de software-update plus vijf minuten.
