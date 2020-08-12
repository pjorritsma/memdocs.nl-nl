---
title: Windows met Software Center via het netwerk implementeren
titleSuffix: Configuration Manager
description: Implementeer een besturings systeem vanuit software Center om een bestaande computer te vernieuwen met een nieuwe versie van Windows of om Windows bij te werken naar de nieuwste versie.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6bd10240ebc7ec478efe122bf7f8a45d3afe9f10
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124598"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Software Center gebruiken om Windows via het netwerk te implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt een taken reeks maken voor het installeren van een besturings systeem dat beschikbaar is in Software Center. Een gebruiker kan een taken reeks uitvoeren vanuit software Center voor de volgende implementatie scenario's voor besturings systemen:

- [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Windows bijwerken naar de laatste versie](upgrade-windows-to-the-latest-version.md)

- [Een takenreeks maken voor niet-besturingssysteemimplementaties](create-a-task-sequence-for-non-operating-system-deployments.md)

Voer de stappen in een van deze scenario's voor implementatie van het besturings systeem uit. Gebruik vervolgens de volgende secties om voor te bereiden voor implementaties die beschikbaar zijn in Software Center.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> De takenreeks implementeren

Implementeer de taken reeks op een doel verzameling. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.

Selecteer op de pagina **implementatie-instellingen** van de implementatie een van de volgende opties voor de instelling **beschikbaar maken voor de volgende** :

- Alleen Configuration Manager-clients

- Configuration Manager-clients, media en PXE

Configureer ook of de implementatie vereist of beschikbaar is:

- Vereiste implementatie: bij vereiste implementaties wordt de taken reeks beschikbaar gemaakt in Software Center. Het wordt automatisch gestart op de geconfigureerde deadline.

- Beschik bare implementatie: de taken reeks is beschikbaar in Software Center en een gebruiker kan deze op aanvraag installeren.

Nadat u de implementatie hebt gemaakt, wordt de taken reeks in Software Center weer gegeven voor clients in de doel verzameling.

## <a name="next-steps"></a>Volgende stappen

[Gebruikerservaring voor implementatie van besturingssysteem](../understand/user-experience.md#software-center)
