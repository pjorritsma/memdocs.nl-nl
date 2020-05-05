---
title: Grond beginselen van client beheer
titleSuffix: Configuration Manager
description: Meer informatie over taken die u uitvoert om Configuration Manager-clients te beheren.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d58a0da25d98089a54694a21d47d1ef8583acb81
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722863"
---
# <a name="fundamentals-of-client-management-tasks-for-configuration-manager"></a>De basis principes van client beheer taken voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u de Configuration Manager-clients hebt geïnstalleerd, zijn er verschillende taken die u kunt uitvoeren om de clients te beheren.  Sommige taken worden uitgevoerd vanuit de Configuration Manager-console. Andere taken worden uitgevoerd vanuit de Configuration Manager-client toepassing. De Configuration Manager-client toepassing wordt geïnstalleerd met de Configuration Manager-client software.

## <a name="configuration-manager-console-tasks"></a>Configuration Manager-console taken
 In de Configuration Manager-console kunt u diverse client beheer taken uitvoeren:  

-   Toepassingen, software-updates, onderhoudsscripts en besturingssystemen implementeren. Configureer de installatie voor een specifieke datum en tijd, maak de software beschikbaar zodat gebruikers deze kunnen installeren wanneer ze worden aangevraagd of Configureer toepassingen die moeten worden verwijderd.  

-   Computers beter beschermen tegen malware en beveiligingsrisico's en u melden wanneer er problemen zijn gedetecteerd.  

-   Configuratie-instellingen van clients definiëren die u wilt controleren en herstellen als deze niet meer compatibel zijn.  

-   Inventarisgegevens van hardware en software verzamelen waaronder het controleren en afstemmen van licentiegegevens van Microsoft.  

-   Computerproblemen oplossen met extern beheer.  

-   Instellingen voor energiebeheer implementeren om het energieverbruik van computers te beheren en controleren.  

In de Configuration Manager-console worden de vorige taken bijna in realtime gecontroleerd. Informatie over meldingen en status van elke taak vindt u in de Configuration Manager-console. Gebruik voor het vastleggen van gegevens en historische trends de geïntegreerde rapportage mogelijkheden van SQL Server Reporting Services. Clients verzenden gegevens als de clientstatus naar de site.  Informatie over de client status biedt gegevens over de status van de client-en client activiteit, en wordt weer gegeven in de console of door gebruik te maken van de ingebouwde rapporten voor Configuration Manager. Met deze gegevens kunnen computers worden geïdentificeerd die niet reageren en in sommige gevallen worden problemen automatisch opgelost.  

 Zie [clients beheren](../../core/clients/manage/manage-clients.md) en [clients beheren voor Linux-en UNIX-servers](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)voor meer informatie over beheer taken voor clients. Voor meer informatie over het gebruik van rapporten gaat u naar   
            [Inleiding tot rapportage](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Client toepassing Configuration Manager  
 Wanneer u de Configuration Manager-client software installeert, wordt de Configuration Manager-client toepassing ook geïnstalleerd. In tegens telling tot software Center is de Configuration Manager-client toepassing ontworpen voor de Help Desk in plaats van voor de eind gebruiker. Voor sommige configuratie opties zijn lokale beheerders machtigingen vereist. de meeste opties vereisen technische kennis over de werking van de Configuration Manager-client toepassing. U kunt met behulp van deze toepassing de volgende taken op een client uitvoeren:  

-   Eigenschappen van de client weer geven, zoals het buildnummer, de toegewezen site, het beheer punt waarmee deze communiceert en of de client een PKI-certificaat (Public Key Infrastructure) of een zelfondertekend certificaat gebruikt.  

-   Controleer of de client een client beleid heeft gedownload nadat de client voor de eerste keer is geïnstalleerd. Controleer ook of de client instellingen op de verwachte wijze zijn in-of uitgeschakeld volgens de client instellingen die zijn geconfigureerd in de Configuration Manager-console.  

-   Client acties starten. U kunt bijvoorbeeld het client beleid downloaden als er een recente configuratie wijziging is opgetreden in de Configuration Manager-console en u niet wilt wachten tot het volgende geplande tijdstip.  

-   Wijs een client hand matig toe aan een Configuration Manager-site of probeer een site te vinden. Geef vervolgens het Domain Name System (DNS)-achtervoegsel op voor beheer punten die naar DNS publiceren.  

-   De client cache configureren die tijdelijk bestanden opslaat. Verwijder vervolgens bestanden in de cache als u meer schijf ruimte nodig hebt om software te installeren.  

-   Instellingen configureren voor clientbeheer via internet.  

-   Configuratiebasislijnen weergeven die op de client zijn geïmplementeerd, een conformiteitsevaluatie starten en conformiteitsrapporten weergeven.  
