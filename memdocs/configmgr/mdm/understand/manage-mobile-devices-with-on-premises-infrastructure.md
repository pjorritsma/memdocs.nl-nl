---
title: On-premises MDM
titleSuffix: Configuration Manager
description: Meer informatie over on-premises Mobile Device Management (MDM) in Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721834"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>On-premises MDM in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager on-premises Mobile Device Management (MDM) is een oplossing voor Apparaatbeheer die afhankelijk is van de ingebouwde beheer mogelijkheden van Windows. Deze functie is gebaseerd op de Open Mobile Alliance (OMA) Device Management (DM)-standaard. De Configuration Manager-infra structuur van uw organisatie wordt gebruikt om de apparaten te beheren en te onderhouden. Uw organisatie vereist Microsoft Intune-licenties om deze functie te gebruiken, maar er is geen verbinding met de Cloud vereist. Configuration Manager slaat alle gegevens over uw apparaten op in uw on-premises site-data base.

On-premises MDM wijkt af van Microsoft Intune, die ook afhankelijk zijn van ingebouwde OMA DM-mogelijkheden. Alle beheer functies in intune worden geleverd via Cloud Services. On-premises MDM verschilt ook van de op client gebaseerde beheer oplossing die traditioneel door Configuration Manager wordt aangeboden. Het is gebaseerd op vergelijk bare infra structuur, maar gebruikt geen afzonderlijk geïnstalleerde client software op de apparaten die worden beheerd.  

## <a name="comparison"></a>Vergelijking

De volgende secties bevatten een overzicht van de voor-en nadelen van on-premises MDM, vergeleken met traditionele beheer op basis van clients:  

### <a name="advantages"></a>Voordelen

- **Vereenvoudigde infra structuur**: minder site systeem rollen vereist.

- **Eenvoudiger te onderhouden**: omdat de beheer functionaliteit is ingebouwd in het besturings systeem van het apparaat, zijn nieuwe versies van de Configuration Manager-client niet vereist wanneer er nieuwe beheer functies op de site worden geïntroduceerd.

- **On-premises**:-alle beheer en gegevens worden on-premises bewaard.

### <a name="disadvantages"></a>Nadelen

**Minder client beheer functionaliteit**: geen Orchestration, software meter, integratie van derden, taken Sequentiëren of software Center-ondersteuning.

- **Beperkte ondersteuning voor apparaten**: on-PREMISes MDM biedt geen ondersteuning voor zoveel versies van het besturings systeem als de Configuration Manager-client. Zie [ondersteunde versies van besturings systemen voor clients en apparaten](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)voor meer informatie.

## <a name="next-step"></a>Volgende stap

Meer informatie over wat u moet overwegen bij het instellen van de Configuration Manager-infra structuur en het plannen van de registratie van apparaten in on-premises MDM.

> [!div class="nextstepaction"]
> [On-premises MDM plannen](../plan-design/plan-on-premises-mdm.md)  
