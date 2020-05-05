---
title: Upgrade van evaluatie-installaties
titleSuffix: Configuration Manager
description: Meer informatie over het bijwerken van een evaluatie-installatie naar een volledige installatie van Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8a42b2538ff1baaceb6895d371081ac2a444c5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717998"
---
# <a name="upgrade-an-evaluation-installation-of-configuration-manager-to-a-full-installation"></a>Een evaluatie-installatie van Configuration Manager upgraden naar een volledige installatie

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u Configuration Manager als een evaluatie versie hebt geïnstalleerd, wordt de Configuration Manager-console na 180 dagen alleen-lezen, totdat u het product via de pagina **site onderhoud** in Setup activeert. U kunt op elk moment vóór of na de periode van 180 dagen een upgrade uitvoeren van een evaluatie-installatie naar een volledige installatie.  

> [!NOTE]  
>  Wanneer u een Configuration Manager-console verbindt met een evaluatie-installatie van Configuration Manager, wordt in de titel balk van de console het aantal dagen weer gegeven dat overblijft totdat de evaluatie-installatie verloopt. Het aantal dagen wordt niet automatisch vernieuwd en wordt alleen bijgewerkt wanneer u een nieuwe verbinding maakt met een site.  

 U kunt de volgende sites waarop een evaluatie-installatie wordt uitgevoerd, upgraden:  

-   Centrale beheersite  
-   Primaire site  

Omdat secundaire sites niet worden behandeld als evaluatie-installaties, hoeft u geen secundaire site te wijzigen nadat de primaire bovenliggende site is bijgewerkt naar een volledige installatie.  

Vereisten voor het bijwerken van een evaluatie versie naar een versie met licentie:  

-   U moet een geldig product hebben om te kunnen gebruiken tijdens de upgrade.  
-   Uw account moet beschikken over **beheerders** rechten op de computer waarop de site is geïnstalleerd.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Een evaluatie versie van Configuration Manager bijwerken naar een versie met licentie  

1.  Voer **Setup. exe** (Configuration Manager Setup) uit in de Configuration Manager installatiemap (**%Path%\BIN\X64**) op de site server. U moet de kopie van Setup uitvoeren die zich op de site server in de map Configuration Manager bevindt, omdat er geen site-onderhouds opties beschikbaar zijn wanneer u Setup uitvoert vanaf de installatie media.  
2.  Selecteer op de pagina **voordat u begint** de optie **volgende**.  
3.  Selecteer op de pagina **aan** de slag **de optie site onderhoud uitvoeren of de site opnieuw instellen**, en selecteer vervolgens **volgende**.  
4.  Selecteer op de pagina **site onderhoud** **de optie upgrade van de evaluatie versie naar een gelicentieerde versie**, voer een geldige product code in en selecteer **volgende**.  
5.  Lees en accepteer de licentie voorwaarden op de pagina **licentie voorwaarden voor micro soft-software** en selecteer **volgende**.  
6.  Op de pagina **configuratie** selecteert u **sluiten** om de wizard te volt ooien.  

    > [!NOTE]  
    >  De titel balk van een Configuration Manager-console die verbonden blijft met de site die u bijwerkt, geeft mogelijk aan dat de site nog steeds een evaluatie versie is totdat u de-console opnieuw verbindt met de-site.  
