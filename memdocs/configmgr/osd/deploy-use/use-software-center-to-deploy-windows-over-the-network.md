---
title: Windows met Software Center via het netwerk implementeren
titleSuffix: Configuration Manager
description: U kunt een besturings systeem implementeren naar Software Center om een bestaande computer te vernieuwen met een nieuwe versie van Windows of om Windows bij te werken naar de nieuwste versie.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4b9946f6204c2e95645c932cd4e9aab691f1d95d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724214"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Software Center gebruiken om Windows via het netwerk te implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt de taken reeks voor het installeren van een besturings systeem in Configuration Manager beschikbaar maken in Software Center. U kunt een besturings systeem implementeren naar Software Center met de volgende implementatie scenario's voor besturings systemen:

-   [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Windows bijwerken naar de laatste versie](upgrade-windows-to-the-latest-version.md)

Voer de stappen in een van de implementatie scenario's voor besturings systemen uit. Gebruik vervolgens de volgende secties om voor te bereiden voor implementaties die beschikbaar zijn in Software Center.

## <a name="configure-deployment-settings"></a>Implementatie-instellingen configureren  
Configureer de implementatie om ervoor te zorgen dat de implementatie van het besturings systeem beschikbaar is in het Software Center. U kunt de implementatie configureren op de pagina **implementatie-instellingen** van de wizard software implementeren of het tabblad implementatie- **instellingen** in de eigenschappen voor de implementatie. Voor de instelling **Toegankelijk maken voor de volgende** configureert u **Alleen Configuration Manager-clients** of **Configuration Manager-clients, media en PXE**. Nadat het besturings systeem is geïmplementeerd door het systeem, wordt het besturings systeem in Software Center weer gegeven voor leden van de doel verzameling.

##  <a name="deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a>De taken reeks implementeren op computers  
Implementeer het besturingssysteem in een doelverzameling. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie. Wanneer u besturings systemen voor Software Center implementeert, kunt u configureren of de implementatie vereist of beschikbaar is.

-   **Vereiste implementatie**: bij vereiste implementaties wordt het besturingssysteem beschikbaar gesteld in Software Center, maar wordt het automatisch gestart volgens de geconfigureerde toewijzingsplanning.

-   **Beschikbare implementatie**: het besturingssysteem wordt beschikbaar gesteld in Software Center en de gebruiker kan het op aanvraag installeren.
