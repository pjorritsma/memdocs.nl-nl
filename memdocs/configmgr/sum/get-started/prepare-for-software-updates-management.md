---
title: Beheer van software-updates voorbereiden
titleSuffix: Configuration Manager
description: Als u wilt voorbereiden op het beheer van updates, voltooit u deze taken om gegevens van de nalevings beoordeling weer te geven in de Configuration Manager-console.
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: ab22fdcacf7574884f7cfd21859cb4b1aeb8e23f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717270"
---
# <a name="prepare-for-software-updates-management"></a>Beheer van software-updates voorbereiden

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat de gegevens voor de nalevings beoordeling van de software-update worden weer gegeven in de Configuration Manager-console en voordat u software-updates op client computers kunt implementeren, moet u de stappen in de volgende secties volt ooien.

## <a name="step-1-install-a-software-update-point"></a>Stap 1: een software-update punt installeren  
Het software-update punt is vereist op de centrale beheer site of op een zelfstandige primaire site, en op primaire sites om de beoordeling van de naleving van software-updates in te scha kelen en software-updates te implementeren op clients. Het software-updatepunt is optioneel op secundaire sites. Zie [een software-update punt installeren](install-a-software-update-point.md) voor meer informatie.  

## <a name="step-2-synchronize-software-updates"></a>Stap 2: software-updates synchroniseren
Synchronisatie van software-updates is het proces van het ophalen van de meta gegevens van software-updates die voldoen aan de criteria die u configureert. Software-updates worden pas weer gegeven in de Configuration Manager-console als u software-updates synchroniseert. Zie [software-updates synchroniseren](synchronize-software-updates.md)voor meer informatie.   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Stap 3: classificaties en producten configureren voor synchronisatie
Voer deze configuratie uit op de centrale beheersite of de zelfstandige primaire site. Wanneer u software-updates de eerste keer synchroniseert, wordt Configuration Manager een bijgewerkte lijst met classificaties en producten opgehaald. U kunt nu kiezen uit de nieuwe opties in de eigenschappen van de software-update punt component. Nadat u de nieuwe classificaties en producten hebt geconfigureerd, herhaalt u stap 2 om de synchronisatie van software-updates te starten om meta gegevens van software-updates voor de nieuwe criteria op te halen. Zie [classificaties en producten configureren voor synchronisatie](configure-classifications-and-products.md)voor meer informatie.

## <a name="step-4-manage-settings-for-software-updates"></a>Stap 4: instellingen voor software-updates beheren
Nadat u software-updates hebt gesynchroniseerd, controleert u Configuration Manager client instellingen, groeps beleids configuraties en instellingen voor software-updates voordat u software-updates implementeert. Zie [instellingen voor software-updates beheren](manage-settings-for-software-updates.md)voor meer informatie.
