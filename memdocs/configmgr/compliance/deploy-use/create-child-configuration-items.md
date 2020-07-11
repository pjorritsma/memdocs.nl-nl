---
title: Onderliggende configuratie-items maken
titleSuffix: Configuration Manager
description: Onderliggende configuratie-items maken in Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 319f673200244d4451b957dcb778ce378f9569fa
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240317"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Onderliggend configuratie-items maken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Onderliggende configuratie-items in Configuration Manager zijn kopieën van configuratie-items die een relatie met het oorspronkelijke configuratie-item behouden, zodat ze de oorspronkelijke configuratie overnemen van het bovenliggende configuratie-item.  

Wanneer u de eigenschappen van een onderliggend configuratie-item in de Configuration Manager-console bekijkt, kunt u de overgenomen objecten en instellingen met hun validatie criteria niet bewerken. U kunt echter wel aanvullende validatiecriteria toevoegen aan het onderliggende configuratie-item en criteria vervolgens bewerken. U kunt ook nieuwe objecten en instellingen toevoegen aan het onderliggende configuratie-item.
Een voor beeld voor het maken en bewerken van een onderliggend configuratie-item is het oorspronkelijke configuratie-item verfijnen om te voldoen aan uw bedrijfs vereisten.  

> [!NOTE]  
>  U kunt alleen onderliggende configuratie-items maken van configuratie-items van het type **Windows-desktops en -servers (aangepast)**.  

## <a name="to-create-a-child-configuration-item"></a>Een onderliggend configuratie-item maken  

1.  Klik in de Configuration Manager-console op **assets en**  >  **Compliance Settings**  >  **configuratie-items**voor nalevings instellingen voor naleving.  

3.  Selecteer in de lijst **Configuratie-items** het configuratie-item waarvoor u een onderliggend configuratie-item wilt maken en klik op het tabblad **Start** in de groep **Configuratie-item** op **Onderliggend configuratie-item maken**.  

4.  Op de pagina **Algemeen** van de wizard **Onderliggend configuratie-item maken**kunt u een specifieke revisie van het bovenliggende configuratie-item kiezen die moet worden gebruikt voor het maken van het onderliggende object. De andere stappen in deze wizard zijn gelijk aan de stappen die u gebruikt als u een standaardconfiguratie-item maakt. Zie voor meer informatie [aangepaste configuratie-items maken voor Windows Desktop-en Server computers](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Voltooi de wizard. Het nieuwe onderliggende configuratie-item wordt weergegeven in de lijst **Configuratie-items** .  
