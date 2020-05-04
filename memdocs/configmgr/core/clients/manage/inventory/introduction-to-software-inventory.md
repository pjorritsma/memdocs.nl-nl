---
title: Software-inventaris
titleSuffix: Configuration Manager
description: Krijg kennis met de software-inventarisatie in Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 07b6f0108125c97128ddc88b663b0af4dabadbe7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714393"
---
# <a name="introduction-to-software-inventory-in-configuration-manager"></a>Inleiding tot software-inventarisatie in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Software-inventaris gebruiken om informatie te verzamelen over bestanden op client apparaten. Software-inventaris kan ook bestanden van client apparaten verzamelen en deze op de site server opslaan. De software-inventarisatie wordt verzameld wanneer u de instelling **software-inventaris op clients inschakelen** in de client instellingen selecteert. U kunt ook de bewerking in client instellingen plannen.  

Nadat u software-inventarisatie hebt ingeschakeld en de clients een software-inventarisatie cyclus hebben uitgevoerd, stuurt de client de gegevens naar een beheer punt in de site van de client. Het beheer punt stuurt de inventarisatie gegevens vervolgens door naar de Configuration Manager-site server, die de informatie in de site database opslaat.

 Er zijn enkele manieren om software-inventaris gegevens weer te geven:  

- [Query's maken](../../../../core/servers/manage/create-queries.md) die apparaten met opgegeven bestanden retour neren.   

- [Op query's gebaseerde verzamelingen](../../../../core/clients/manage/collections/introduction-to-collections.md) maken die apparaten met opgegeven bestanden bevatten.   

- [Rapporten uitvoeren](../../../servers/manage/introduction-to-reporting.md) met details over bestanden op apparaten.

- [Resource Explorer](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) gebruiken om gedetailleerde informatie over de bestanden te onderzoeken die zijn geïnventariseerd en verzameld van client apparaten.   

 Wanneer software-inventarisatie op een client apparaat wordt uitgevoerd, is het eerste rapport een volledige inventarisatie. Volgende rapporten bevatten alleen informatie over Delta-inventarisatie. De site server verwerkt de Delta-informatie in de ontvangen bestelling. Als er geen Delta gegevens voor een client ontbreken, wordt door de site server meer Delta gegevens geweigerd en wordt de client doorgestuurd om een volledige inventarisatie uit te voeren.  

 Configuration Manager kan dual-boot-computers detecteren, maar retourneert alleen inventarisatie gegevens van het besturings systeem dat actief is op het moment van de inventarisatie.  
