---
title: Installatiescenario 's
titleSuffix: Configuration Manager
description: Leer technieken voor het installeren van een nieuwe Configuration Manager-hiërarchie wanneer u een site bijwerkt of upgradet.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a63667faf9590f647c01565f1425081e53bdfc97
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718096"
---
# <a name="scenarios-to-streamline-your-installation-of-configuration-manager"></a>Scenario's voor het stroom lijnen van uw installatie van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met de release van update versies voor Configuration Manager current branch zijn er nieuwe scenario's beschikbaar om de installatie van een nieuwe hiërarchie naar een update versie (zoals update 1610) te stroom lijnen en een upgrade uit te brengen van micro soft System Center 2012 Configuration Manager.

Ondersteunde scenario's omvatten:  

**Installeer een nieuwe Configuration Manager huidige vertakkings hiërarchie** waarop een update versie wordt uitgevoerd.  

-   Installeer alleen de site op het hoogste niveau en installeer onmiddellijk een update om die site actueel te maken met de update versie die u wilt gebruiken. Vervolgens kunt u aanvullende sites rechtstreeks op die update versie installeren.  
-   In dit scenario slaat u het proces voor het installeren van extra sites op een basislijn niveau over en werkt u deze vervolgens bij naar de update versie die u wilt gebruiken.  
-   In dit scenario slaat u het proces voor het installeren van clients naar een basislijn versie over en installeert u deze opnieuw wanneer u een nieuwere versie bijwerkt.  

Voer **een upgrade uit van een micro soft System Center 2012 Configuration Manager** -infra structuur naar een update versie van Configuration Manager.  

-   Voer hand matig een upgrade uit van uw centrale beheer site en elke primaire site naar een basislijn versie (zoals versie 1606) voordat u een update versie installeert (zoals versie 1610).  
-   Voer geen upgrade uit van secundaire sites van micro soft System Center 2012 Configuration Manager totdat de update versie die u wilt gebruiken wordt uitgevoerd op uw primaire sites.  
-   Voer geen upgrade uit van de clients van micro soft System Center 2012 Configuration Manager totdat de update versie die u wilt gebruiken wordt uitgevoerd op uw primaire sites.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Scenario: een nieuwe hiërarchie installeren op een update versie  
In dit voorbeeld scenario installeert u de eerste site van een hiërarchie met behulp van een basis versie van Configuration Manager, zoals versie 1610. Installeer vervolgens de 1610-update voordat u extra sites of clients implementeert.  

-   Omdat u van plan bent een update versie (zoals versie 1610) te gebruiken en niet op een basislijn versie (zoals versie 1606), hoeft u geen extra sites te installeren en deze vervolgens bij te werken. Dit geldt ook voor clients.  
-   Installeer geen secundaire sites met versie 1606 en werk deze vervolgens bij naar versie 1610. Installeer in plaats daarvan secundaire sites nadat op uw primaire sites versie 1610 is uitgevoerd.  

Volg deze volg orde:  

1. **Installeer een site op het hoogste niveau voor de nieuwe hiërarchie** met behulp van de basislijn media.  

   -   U kunt basislijn media alleen gebruiken om de eerste site van een nieuwe hiërarchie te installeren.  
   -   Installeer bijvoorbeeld een site op het hoogste niveau met behulp van de basislijn versie van 1606. Zie [de installatie wizard gebruiken om sites te installeren](use-the-setup-wizard-to-install-sites.md)voor meer informatie.  

   Na deze stap wordt op de site op het hoogste niveau versie 1606 uitgevoerd.  

2. **Gebruik in-console updates om de site op het hoogste niveau bij te werken naar een nieuwere versie.**  

   -   Voordat u onderliggende sites of clients installeert, moet u de site op het hoogste niveau bijwerken naar de update versie die u wilt gebruiken.  
   -   U kunt bijvoorbeeld de site op het hoogste niveau waarop versie 1606 wordt uitgevoerd, bijwerken naar versie 1610. Zie [updates voor Configuration Manager](../../../../core/servers/manage/updates.md)voor meer informatie.  

   Na deze stap wordt op de site op het hoogste niveau versie 1610 uitgevoerd.  

3. **Installeer nieuwe onderliggende primaire sites onder een centrale beheersite.**  

   - Installeer nieuwe onderliggende primaire sites met behulp van de installatiemedia in de map CD.Latest op de server van de centrale beheersite. Zie de CD voor meer informatie [. Meest recente map voor Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

     Deze bronmedia zijn vereist om te zorgen dat de versie van de nieuwe onderliggende primaire sites overeenkomt met de versie van de centrale beheersite.  

   Na deze stap voert de nieuwe onderliggende primaire sites versie 1610.  

4. **Gebruik op elke primaire site de optie in de console om nieuwe secundaire sites te installeren.**  

   -   Omdat u geen secundaire sites hebt geïnstalleerd terwijl op de primaire sites versie 1606 werd uitgevoerd, hoeft u geen upgrade uit te voeren van secundaire sites.  
   -   Installeer in plaats daarvan nieuwe secundaire sites waarop versie 1610 wordt uitgevoerd. Zie voor meer informatie [Een secundaire site installeren](use-the-setup-wizard-to-install-sites.md#bkmk_secondary) in het onderwerp [De installatiewizard gebruiken om sites te installeren](use-the-setup-wizard-to-install-sites.md) .  

   Na deze stap zijn nieuwe secundaire sites geïnstalleerd en wordt versie 1610 uitgevoerd.  

5. **Installeer nieuwe clients op de primaire site.**  

   -   Omdat u geen clients hebt geïnstalleerd terwijl op de primaire sites versie 1606 werd uitgevoerd, hoeft u geen upgrade van clients van versie 1606 naar versie 1610 uit te voeren.  
   -   Installeer in plaats daarvan nieuwe clients waarop versie 1610 wordt uitgevoerd. Zie [clients implementeren](../../../clients/deploy/deploy-clients-to-windows-computers.md)voor meer informatie.  

   Na deze stap worden nieuwe clients geïnstalleerd waarop versie 1610 wordt uitgevoerd.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-configuration-manager-current-branch"></a>Scenario: upgrade System Center 2012 Configuration Manager naar een update versie van Configuration Manager, current branch  

In dit voorbeeld scenario werkt u uw System Center 2012-Configuration Manager-infra structuur bij naar een update versie van Configuration Manager current branch, zoals versie 1610.  

-   De centrale beheer site en elke primaire site moeten worden bijgewerkt naar de basislijn versie 1606 voordat u de update voor versie 1610 installeert.  
-   Secundaire sites en clients worden niet bijgewerkt of installeren versie 1606. In plaats daarvan gaat u rechtstreeks vanuit System Center 2012 Configuration Manager naar Configuration Manager huidige branch-versie 1610.  

Volg deze volg orde:  

1. Voer op het **hoogste niveau System Center 2012 Configuration Manager site uit** naar een basislijn versie van de huidige vertakking met behulp van de bron media voor Configuration Manager (zoals versie 1606). Zie [upgrade naar Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)voor meer informatie.  

   -   Net als bij traditionele upgrade scenario's voert u eerst altijd een upgrade uit van de site op het hoogste niveau van een hiërarchie, waarna u de onderliggende sites bijwerkt.  

   Na deze stap wordt op de site op het hoogste niveau versie 1606 uitgevoerd.  

2. **Voer een upgrade uit van alle onderliggende primaire sites in uw hiërarchie** naar dezelfde basislijnversie.  

   -   Wanneer u een upgrade uitvoert van micro soft System Center 2012 Configuration Manager, moet u elke primaire site hand matig bijwerken naar een basislijn versie van de huidige vertakking.  
   -   U gaat op dit punt niet upgraden naar secundaire sites.  

   Na deze stap wordt op elke primaire site versie 1606 uitgevoerd.  

3. **Stel onderhouds Vensters in op de onderliggende primaire sites.** Nadat u de upgrade van alle primaire sites naar de basislijn versie hebt uitgevoerd, plant u het configureren van onderhouds Vensters om te bepalen wanneer deze sites infrastructuur updates installeren. Zie [onderhouds Vensters gebruiken](../../../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie.  (Onderhouds Vensters worden *service vensters* genoemd in versie 1606.)  

   -   Met een onderliggende primaire site worden automatisch dezelfde updates geïnstalleerd die u op een centrale beheersite installeert.  
   -   Bij secundaire sites worden niet automatisch nieuwe versies geïnstalleerd. U moet deze hand matig upgraden vanuit de-console.  

   Als u na deze stap updates op de centrale beheersite installeert, wordt deze update alleen op onderliggende primaire sites geïnstalleerd als het onderhoudsvenster voor een site dat toestaat.  

4. **Installeer de update versie op uw site op het hoogste niveau.** Hiermee werkt u de site op het hoogste niveau bij. Nadat de update versie door een centrale beheer site is geïnstalleerd, wordt de update automatisch geïnstalleerd door elke onderliggende primaire site, tenzij de installatie wordt geblokkeerd door een onderhouds venster.  

   -   U kunt bijvoorbeeld de site op het hoogste niveau bijwerken van versie 1606 naar versie 1610. Zie [updates voor Configuration Manager](../../../../core/servers/manage/updates.md)voor meer informatie.  

   Na deze stap wordt op uw centrale beheer site en op elke primaire site versie 1610 uitgevoerd.  

5. **Voer een upgrade van de secundaire sites uit.** Nadat de update is geïnstalleerd op een primaire site en versie 1610 wordt uitgevoerd, gebruikt u de optie in de console om secundaire sites bij te werken.  

   -   Hiermee worden secundaire sites rechtstreeks vanuit micro soft System Center 2012 Configuration Manager naar de update versie die u hebt geïnstalleerd op de primaire site.  
   -   Voor informatie over het upgraden van een secundaire site, Zie [sites bijwerken](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) in het onderwerp [upgraden naar Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) .  

6. **Clients bijwerken.** Als u clients wilt bijwerken, gebruikt u de informatie in de [clients voor Windows-computers bijwerken](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

   -   Hiermee worden clients rechtstreeks vanuit micro soft System Center 2012 Configuration Manager bijgewerkt naar de update versie die u hebt geïnstalleerd op de primaire site.  

   Na deze stap worden clients bijgewerkt naar versie 1610 zonder eerst te upgraden naar versie 1606.
