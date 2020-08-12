---
title: Community-hub en GitHub
titleSuffix: Configuration Manager
description: Community hub inschakelen en gebruiken in Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ae0abdd4a159759037768c8f27d5643bdf612f6e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128168"
---
# <a name="community-hub-and-github"></a>Community-hub en GitHub
<!--3555935, 3555936-->

De IT-beheerder heeft een schat aan kennis ontwikkeld over de jaren. In plaats van items zoals scripts en rapporten helemaal opnieuw te hoeven maken, hebben we een **Configuration Manager Community-hub** gebouwd waar IT-beheerders met elkaar kunnen delen. Door gebruik te maken van anderen, kunt u uren werk besparen. De Community hub bevordert creativiteit door anderen aan het werk te bouwen en anderen te laten bouwen. GitHub heeft al branchespecifieke processen en hulpprogram ma's die zijn ontworpen voor delen. De Community-hub maakt nu gebruik van deze hulpprogram ma's rechtstreeks in de Configuration Manager-console als basis onderdelen voor het aansturen van deze nieuwe community. Voor de eerste release wordt de inhoud die beschikbaar is in de Community hub alleen geüpload door micro soft. De IT-beheerder kan in de toekomst inhoud uploaden met behulp van hun eigen GitHub-account.

> [!Note]  
> Community hub is een optioneel Cloud onderdeel. Het is voor het eerst geïntroduceerd in juni 2020. Zie [optionele functies](install-in-console-updates.md#bkmk_options)voor meer informatie over het kiezen van een Community-hub.

## <a name="about-community-hub"></a>Over Community hub

Community hub ondersteunt de volgende objecten:

- CMPivot query's
- Toepassingen
- Takenreeksen
- Configuratie-items
- PowerShell-scripts
- Rapporten

## <a name="prerequisites"></a>Vereisten

- Op het apparaat waarop de Configuration Manager-console wordt uitgevoerd om toegang te krijgen tot de Community-hub, moeten de volgende items worden gebruikt:
   - .NET Framework versie 4,6 of hoger
   - Windows 10 build 17110 of hoger
      - Windows Server wordt niet ondersteund, dus de Configuration Manager-console moet worden geïnstalleerd op een Windows 10-apparaat dat gescheiden is van de site server.
   - Het aangemelde gebruikers account kan niet het ingebouwde Administrator account zijn

- De [beheer service](../../../develop/adminservice/set-up.md) in Configuration Manager moet worden ingesteld en werkt.

- Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u de Configuration Manager-console toestaan om toegang te krijgen tot internet-eind punten. Zie [vereisten voor Internet toegang](../../plan-design/network/internet-endpoints.md#community-hub)voor meer informatie.

## <a name="permissions"></a>Machtigingen

- Een script importeren: machtiging **maken** voor **SMS_Scripts** klasse.
- Een rapport importeren: volledige beheerder beveiligingsrol.


## <a name="use-the-community-hub"></a>De Community-hub gebruiken

1. Ga naar het knoop punt **Community-hub** in de werk ruimte **Community** .
1. Selecteer een item om te downloaden.
1. U hebt de juiste machtigingen op uw Configuration Manager-site nodig om objecten van de hub te downloaden en te importeren in de-site.
    - Een script importeren: machtiging **maken** voor SMS_Scripts klasse.
    - Een rapport importeren: volledige beheerder beveiligingsrol.
1. Gedownloade rapporten worden geïmplementeerd naar een rapportmap met de naam **hub** op het Reporting Services-punt. Gedownloade scripts kunnen worden weer gegeven in het knoop punt **Run scripts** .
1. Bekijk alle items die zijn gedownload van de hub door uw organisatie door te klikken op **uw down loads** in het knoop punt **Community hub** .

[![Alle items die zijn gedownload van de Community-hub](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)


## <a name="direct-links-to-community-hub-items"></a><a name="bkmk_deeplink"></a>Directe koppelingen naar Community-hub-items
<!--4224406-->
*(Geïntroduceerd in versie 2006)* U kunt eenvoudig navigeren naar en verwijzen naar items in het knoop punt van de Configuration Manager console-hub met een directe koppeling. De bedoeling van deze functie is voor een eenvoudiger samen werking en het delen van koppelingen naar Community-hub-items met uw collega's. Deze diepe koppelingen zijn momenteel alleen voor items in het knoop punt Community-hub van de-console.

### <a name="prerequisites-for-direct-links"></a>Vereisten voor directe koppelingen

- Configuration Manager-console versie 2006 of hoger
- U kunt het lokale ingebouwde Administrator-account niet gebruiken bij het volgen van een Community-hub-koppeling.

### <a name="sharing-and-opening-direct-links"></a>Direct koppelingen delen en openen

Een item delen:
1. Ga naar het item in de hub en selecteer **delen**.
1. Plak de gekopieerde koppeling en deel deze met anderen.

Een gedeelde koppeling openen:
1. Klik op de koppeling van een computer waarop de Configuration Manager-console is geïnstalleerd.
   - U kunt deze koppeling bijvoorbeeld gebruiken om het [script voor automatische updates van de rand configureren](https://communityhub.microsoft.com/item/7200) () te delen `https://communityhub.microsoft.com/item/7200` .
1. Selecteer **de hub van de Community starten** wanneer u hierom wordt gevraagd.
1. De console wordt rechtstreeks naar het script in de Community-hub geopend.

## <a name="known-issues"></a><a name="bkmk_known"></a>Bekende problemen

### <a name="unable-to-access-community-hub-node-when-running-console-as-a-different-user"></a>Kan geen toegang krijgen tot het hub-knoop punt van de Community wanneer de console wordt uitgevoerd als een andere gebruiker
<!--7826897-->
Als u bent aangemeld als een gebruiker met lagere rechten en vervolgens **uitvoeren als** een andere gebruiker kiest om de Configuration Manager-console te openen, hebt u mogelijk geen toegang tot het knoop punt **Community hub** .

### <a name="downloaded-reports-dont-get-removed-from-your-downloads-page"></a>Gedownloade rapporten worden niet verwijderd van de pagina down loads
<!--7851305-->
Als u een gedownload rapport verwijdert uit het knoop punt **bewakings**  >  **rapporten** , wordt het rapport niet verwijderd uit de **Community-hub**op  >  uw pagina met**down loads** en kunt u het rapport niet opnieuw downloaden. 

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het maken en gebruiken van de volgende objecten:

- [PowerShell-scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md)
- [Inleiding op rapportage](introduction-to-reporting.md)
- [Taken reeksen maken en beheren](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Een toepassing maken en implementeren](../../../apps/get-started/create-and-deploy-an-application.md)
- [Configuratie-items maken](../../../compliance/deploy-use/create-configuration-items.md)