---
title: Een installatiekopie voor een OEM in de fabriek of bij een lokaal depot maken
titleSuffix: Configuration Manager
description: Gebruik voorgefaseerde media-implementaties om het netwerk verkeer te verminderen terwijl u een besturings systeem implementeert op een computer die nog niet volledig is ingericht.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c4d445d18b9e239ace673199f6a7d0f26d10a42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722996"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Een installatie kopie voor een OEM in de fabriek of een lokaal depot maken met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met voor bereide media-implementaties in Configuration Manager kunt u een besturings systeem implementeren op een computer die nog niet volledig is ingericht. De voorgefaseerde media is een WIM-bestand (Windows Imaging Format) dat door de fabrikant (OEM) kan worden geïnstalleerd op een bare-metal computer of in een Enter prise staging Center dat geen verbinding heeft met de Configuration Manager omgeving. Later in de Configuration Manager omgeving wordt de computer gestart met de opstart installatie kopie van de media, wordt er een hash-controle op de voor bereide media uitgevoerd om er zeker van te zijn dat deze geldig is, en maakt de computer vervolgens verbinding met het site beheer punt voor beschik bare taken reeksen die het download proces volt ooien.


Deze implementatiemethode kan het netwerkverkeer verminderen omdat de opstartinstallatiekopie en de installatiekopie van het besturingssysteem zich al op de doelcomputer bevinden. U kunt toepassingen, pakketten en stuurprogrammapakketten opgeven die in de voorbereide media moeten worden opgenomen. Nadat het besturingssysteem is geïnstalleerd op de computer, wordt de lokale takenreekscache eerst gecontroleerd op toepassingen, pakketten en stuurprogrammapakketten, en als de inhoud niet kan worden gevonden of is gewijzigd, wordt de inhoud gedownload vanaf een distributiepunt dat is geconfigureerd in de voorbereide media, en vervolgens geïnstalleerd.  

 U kunt voor bereide media gebruiken in de volgende implementatie scenario's voor besturings systemen:  

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)  

- [Een bestaande computer vervangen en de instellingen overzetten](replace-an-existing-computer-and-transfer-settings.md)  

  Voer de stappen in een van de implementatiescenario’s voor besturingssystemen en gebruik de volgende secties om de voorbereide media voor te bereiden en te maken.  

## <a name="configure-deployment-settings"></a>Implementatie-instellingen configureren  
 Als u het implementatieproces voor een besturingssysteem wilt starten vanaf vooraf geplaatste media, moet u de implementatie configureren om het besturingssysteem beschikbaar te stellen voor media. U kunt dit configureren op de pagina **Implementatie-instellingen** van de wizard Software implementeren of op het tabblad **Implementatie-instellingen** in de eigenschappen voor de implementatie.  Configureer een van de volgende waarden voor de instelling **Toegankelijk maken voor de volgende** :  

-   **Configuration Manager-clients, media en PXE**  

-   **Alleen media en PXE**  

-   **Alleen media en PXE (verborgen)**  

## <a name="create-the-prestaged-media"></a>Voorbereide media maken  
 Maak de voorbereide media die naar de OEM of uw lokale depot moet worden verzonden. Zie voor [bereide media maken met Configuration Manager](create-prestaged-media.md)voor meer informatie.  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Het voorbereide mediabestand naar de OEM of het lokale depot verzenden  
 Verzend de media naar de OEM of uw lokale depot om de computers voor te bereiden. Het voorbereide mediabestand wordt toegepast op een geformatteerde vaste schijf op de computer.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Start de computer om het besturingssysteem te installeren  
 Het voorbereide mediabestand wordt toegepast op alle computers. Zodra de computer voor het eerst wordt gestart, start het installatieproces van het besturingssysteem.  
