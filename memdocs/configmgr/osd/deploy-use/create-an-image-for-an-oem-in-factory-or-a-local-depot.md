---
title: Een installatiekopie voor een OEM in de fabriek of bij een lokaal depot maken
titleSuffix: Configuration Manager
description: Gebruik voorgefaseerde media-implementaties om het netwerk verkeer te verminderen terwijl u een besturings systeem implementeert op een computer die niet volledig is ingericht.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125437"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Een installatie kopie voor een OEM in de fabriek of een lokaal depot maken met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met voor bereide media-implementaties in Configuration Manager kunt u een besturings systeem implementeren op een computer die niet volledig is ingericht. De voorgefaseerde media zijn een Windows-installatie kopie (WIM)-bestand. De fabrikant (OEM) kan deze installeren op een bare-metal computer of u kunt deze gebruiken in een faserings centrum dat gescheiden is van uw productie omgeving.

Deze implementatie methode kan het netwerk verkeer verminderen omdat de opstart installatie kopie en de installatie kopie van het besturings systeem zich al op de doel computer bevinden. U kunt toepassingen, pakketten en stuur programmapakketten opgeven die ook moeten worden toegevoegd aan de voorgefaseerde media. Nadat het besturings systeem op de computer is geïnstalleerd, controleert de taken reeks eerst de voor bereide cache op toepassingen, pakketten of stuur programmapakketten. Als de benodigde inhoud niet kan worden gevonden of als er een nieuwere revisie beschikbaar is, downloadt de taken reeks de inhoud van een distributie punt.

Gebruik voorgefaseerde media in de volgende implementatie scenario's voor besturings systemen:

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)

- [Een bestaande computer vervangen en de instellingen overzetten](replace-an-existing-computer-and-transfer-settings.md)

Voer de stappen in een van deze scenario's voor implementatie van het besturings systeem uit. Gebruik vervolgens de volgende secties om de voorgefaseerde media voor te bereiden en te maken.

## <a name="configure-deployment-settings"></a>Implementatie-instellingen configureren

Selecteer op de pagina **implementatie-instellingen** van de implementatie een van de volgende opties voor de instelling **beschikbaar maken voor de volgende** :

- Configuration Manager-clients, media en PXE

- Alleen media en PXE

- Alleen media en PXE (verborgen)

## <a name="create-the-prestaged-media"></a>Voorbereide media maken

Maak de voorbereide media die naar de OEM of uw lokale depot moet worden verzonden. Zie voor [bereide media maken met Configuration Manager](create-prestaged-media.md)voor meer informatie.

## <a name="send-the-prestaged-media-file"></a>Het voor bereide Media bestand verzenden

Verzend de media naar de OEM of uw lokale depot om de computers voor te bereiden. Het installatie kopie bestand wordt toegepast op een geformatteerde vaste schijf op de computer.

## <a name="deliver-the-computer"></a>De computer leveren

Wanneer u de computer aan een gebruiker levert en deze voor de eerste keer inschakelt:

1. De computer begint met de voor bereide opstart installatie kopie.

1. Er wordt een hash op de voor bereide media gecontroleerd om er zeker van te zijn dat deze geldig is.

1. De computer maakt verbinding met het beheer punt voor beschik bare taken reeksen om het proces te volt ooien.

## <a name="next-steps"></a>Volgende stappen

[Gebruikerservaring voor implementatie van besturingssysteem](../understand/user-experience.md)
