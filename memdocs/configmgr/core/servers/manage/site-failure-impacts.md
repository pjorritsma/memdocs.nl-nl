---
title: Gevolgen van sitefouten
titleSuffix: Configuration Manager
description: Inzicht in de effecten van verschillende storingen in een Configuration Manager-site.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf56aee2e9f73ea8c3c69737c749f2a599e1ac37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723892"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Gevolgen voor de site storingen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De site server en een van de andere site systemen kunnen mislukken en een verlies veroorzaken van de services die ze regel matig aanbieden. Als u meerdere site systemen op dezelfde computer installeert en deze computer uitvalt, zijn alle services die regel matig door deze site systemen worden door gegeven, niet meer beschikbaar.

Een deel van uw plannings proces moet weten wat de gevolgen zijn van de service die u voor uw organisatie hebt. Omdat elk site systeem op de site verschillende functionaliteit biedt, verschilt de impact van een storing op de site, afhankelijk van de rol van het site systeem dat is mislukt. 

Gebruik [Opties voor hoge Beschik baarheid](../deploy/configure/high-availability-options.md) om de storing van één systeem te verhelpen. Plan en oefen ook een strategie voor [back-up en herstel](backup-and-recovery.md) om de hoeveelheid tijd die de service niet beschikbaar is, te verminderen.

In de volgende secties wordt de impact beschreven wanneer het opgegeven site systeem niet operationeel is:


### <a name="site-server"></a>Siteserver

- Er is geen site beheer mogelijk. U kunt de-console niet verbinden met de-site.  

- Het beheer punt verzamelt client gegevens en slaat de cache op totdat de site server weer online is.  

- Gebruikers kunnen bestaande implementaties uitvoeren en clients kunnen inhoud downloaden vanaf distributie punten.  


### <a name="site-database"></a>Sitedatabase

- Er is geen site beheer mogelijk.  

- Als de Configuration Manager-client al een beleids toewijzing met nieuwe beleids regels heeft en als het beheer punt heeft de beleids tekst in de cache geplaatst, kan de client een aanvraag voor een beleids tekst maken en het antwoord op het hoofd bericht van het beleid ontvangen. De site kan echter geen nieuwe aanvragen voor beleids toewijzingen verwerken.  

- Clients kunnen implementaties uitvoeren, alleen als ze het beleid al hebben ontvangen en de gekoppelde bron bestanden al lokaal in de cache zijn opgeslagen op de client.  


### <a name="management-point"></a>Beheerpunt

- Hoewel u nieuwe implementaties kunt maken, ontvangen clients geen beheer punt online.  

- Clients verzamelen nog steeds inventaris, software licentie controle en status informatie. Ze slaan deze gegevens lokaal op totdat het beheer punt beschikbaar is.  

- Clients kunnen implementaties uitvoeren, alleen als ze het beleid al hebben ontvangen en de gekoppelde bron bestanden al lokaal in de cache zijn opgeslagen op de client.  


### <a name="distribution-point"></a>Distributiepunt

- Configuration Manager-clients kunnen implementaties uitvoeren, alleen als de gekoppelde bron bestanden al lokaal zijn gedownload of beschikbaar zijn op een peer bron.

