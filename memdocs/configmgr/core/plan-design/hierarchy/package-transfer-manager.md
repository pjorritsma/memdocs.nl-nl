---
title: Package Transfer Manager
titleSuffix: Configuration Manager
description: Begrijpen hoe package Transfer Manager in Configuration Manager inhoud overdraagt van een site server naar externe distributie punten.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b450c45342793b89d41a2d96b8a7340939899093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722450"
---
# <a name="package-transfer-manager-in-configuration-manager"></a>Package overdracht manager in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In een Configuration Manager-site is package overdracht Manager een onderdeel van de SMS_Executive-service waarmee de overdracht van inhoud van een site Server computer naar externe distributie punten in een site wordt beheerd. (Een extern distributie punt dat zich niet op de site Server computer bevindt.) Package overdracht Manager biedt geen ondersteuning voor configuraties door de beheerder, maar met een uitleg over hoe het wordt uitgevoerd, kunt u uw infra structuur voor inhouds beheer plannen. Het kan ook helpen bij het oplossen van problemen met de inhouds distributie.


Wanneer u inhoud distribueert naar een of meer externe distributie punten op een site, wordt door **Distribution Manager** een taak voor inhouds overdracht gemaakt. Vervolgens wordt de package overdracht Manager op de primaire en secundaire site servers op de hoogte gebracht om de inhoud over te dragen naar de externe distributie punten.

 Package overdracht Manager registreert de acties in het bestand **pkgxfermgr. log** op de site server. Het logboek bestand is de enige locatie waar u de activiteiten van de package overboeking Manager kunt bekijken.  

> [!NOTE]  
>  In eerdere versies van Configuration Manager beheert Distribution Manager de overdracht van inhoud naar een extern distributie punt. Distribution Manager beheert ook de overdracht van inhoud tussen sites. Met de Configuration Manager blijft Distribution Manager de overdracht van inhoud tussen twee sites blijven beheren. De package overdracht Manager beheert nu echter de overdracht van inhoud naar een groot aantal distributie punten. Dit helpt bij het verhogen van de algehele prestaties van inhouds implementatie tussen sites en tot distributie punten binnen een site.  

Als u inhoud wilt overdragen naar een standaard distributiepunt, werkt package overdracht Manager hetzelfde als de Distribution Manager werkt in eerdere versies van Configuration Manager. Dat wil zeggen dat het de overdracht van bestanden naar elk extern distributie punt actief beheert. Voor het distribueren van inhoud naar een pull-distributie punt, wordt het pull-distributie punt dat de inhoud beschikbaar is, door de package overdrachts Manager op de hoogte gebracht. Het pull-distributie punt neemt vervolgens het overdrachts proces over.  

De volgende informatie beschrijft hoe package overdracht Manager de overdracht van inhoud beheert naar standaard distributie punten en naar distributie punten die zijn geconfigureerd als pull-distributie punten:
1.  **De beheerder implementeert inhoud op een of meer distributie punten op een site.**  

    -   **Standaard distributie punt:** Distribution Manager maakt een taak voor inhouds overdracht voor die inhoud.  

    -   **Pull-distributie punt:** Distribution Manager maakt een taak voor inhouds overdracht voor die inhoud.  

2.  **Distribution Manager voert voorlopige controles uit.**  

    -   **Standaard distributie punt:** Distribution Manager voert een basis controle uit om te bevestigen dat elk distributie punt klaar is om de inhoud te ontvangen. Na deze controle waarschuwt Distribution Manager package overdracht Manager om de overdracht van inhoud naar het distributie punt te starten.  

    -   **Pull-distributie punt:** Distribution Manager start package overdracht Manager, waarna het pull-distributie punt wordt gewaarschuwd dat er een nieuwe taak voor inhouds overdracht is. Distribution Manager controleert niet de status van externe distributie punten die pull-distributie punten zijn, omdat elk pull-distributie punt zijn eigen inhouds overdrachten beheert.  

3.  **Package overdracht Manager bereidt het overdragen van inhoud voor.**  

    -   **Standaard distributie punt:** Package overboeking Manager onderzoekt de single instance Content Store van elk opgegeven extern distributie punt. Het doel hiervan is het identificeren van bestanden die zich al op dat distributie punt bevinden. Pakket overdracht Manager-wacht rijen voor overdracht alleen die bestanden die nog niet aanwezig zijn.  

        > [!NOTE]  
        >  Als u wilt dat elk bestand in de distributie naar het distributie punt kopieert, zelfs als de bestanden al aanwezig zijn in de Single Instance Store van het distributie punt, gebruikt u de actie opnieuw **distribueren** voor inhoud.  

    -   **Pull-distributie punt:** Voor elk pull-distributie punt in de distributie controleert package overboeking Manager de bron distributiepunten voor pull-distributie punten om te bevestigen of de inhoud beschikbaar is.  

        -   Wanneer de inhoud beschikbaar is op ten minste één bron distributiepunt, stuurt package overdracht Manager een melding naar het pull-distributie punt. De melding leidt dat distributie punt om te beginnen met het proces van het overdragen van inhoud. De melding bevat bestands namen en grootten, kenmerken en hash-waarden.  

        -   Wanneer de inhoud nog niet beschikbaar is, verzendt package overdracht Manager geen melding naar het distributie punt. In plaats daarvan wordt de controle om de 20 minuten herhaald, totdat de inhoud beschikbaar is. Wanneer de inhoud beschikbaar is, verzendt package overdracht Manager de melding naar het pull-distributie punt.  

        > [!NOTE]  
        >  Voor het pull-distributie punt voor het kopiëren van elk bestand in de distributie naar het distributie punt, zelfs als de bestanden al aanwezig zijn in de Single Instance Store van het pull-distributie punt, gebruikt u de actie opnieuw **distribueren** voor inhoud.  

4.  **De inhoud begint te worden overgedragen.**  

    -   **Standaard distributie punt:** Package overdracht Manager kopieert bestanden naar elk extern distributie punt. Tijdens de overdracht naar een standaard distributiepunt:  

        -   Package overdracht Manager kan standaard drie unieke pakketten verwerken en deze gelijktijdig distribueren naar vijf distributie punten. Gezamenlijk worden deze **instellingen voor gelijktijdige distributie**genoemd. Als u gelijktijdige distributie wilt instellen, gaat u naar het tabblad **Algemeen** in de eigenschappen voor de **software distributie onderdelen** van elke site.  

        -   Package Transfer Manager maakt gebruik van de plannings-en netwerk bandbreedte configuraties van elk distributie punt bij het overdragen van inhoud naar dat distributie punt. Als u deze instellingen wilt configureren, gaat u naar de tabbladen **schema** en **frequentie limieten** in de **Eigenschappen** van elk extern distributie punt. Zie [inhoud en infra structuur voor inhoud beheren voor Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor meer informatie.  

    -   **Pull-distributie punt:** Wanneer een pull-distributie punt een meldings bestand ontvangt, begint het distributie punt het proces om de inhoud over te dragen. Het overdrachts proces wordt onafhankelijk uitgevoerd op elk pull-distributie punt:  

        1.   De pull-distributie identificeert de bestanden in de inhouds distributie die deze nog niet heeft in zijn Single Instance Store en bereidt het downloaden van die inhoud vanaf een van de bron distributiepunten voor.  

        2.   Vervolgens controleert het pull-distributie punt met elk van de bron distributiepunten, in de juiste volg orde, totdat er een bron distributiepunt wordt gevonden dat de inhoud beschikbaar heeft. Wanneer het pull-distributie punt een bron distributiepunt met de inhoud identificeert, wordt het downloaden van die inhoud gestart.  

        > [!NOTE]  
        >  Het proces voor het downloaden van inhoud door het pull-distributie punt is hetzelfde als die welke wordt gebruikt door Configuration Manager-clients. Voor de overdracht van inhoud door het pull-distributie punt worden geen instellingen voor gelijktijdige overdracht gebruikt. Plannings-en bandbreedte opties die u configureert voor standaard distributie punten, worden niet gebruikt.  

5.  **De inhouds overdracht is voltooid.**  

    -   **Standaard distributie punt:** Nadat de package Transfer Manager klaar is met het overbrengen van bestanden naar elk aangewezen extern distributie punt, wordt de hash van de inhoud op het distributie punt gecontroleerd. Vervolgens wordt Distribution Manager op de hoogte gebracht dat de distributie is voltooid.  

    -   **Pull-distributie punt:** Nadat het pull-distributie punt de inhoud downloadt, controleert het distributie punt de hash van de inhoud. Vervolgens wordt er een status bericht verzonden naar het site beheer punt om aan te geven dat dit is geslaagd. Als na 60 minuten deze status niet wordt ontvangen, wordt de package overboeking Manager opnieuw geactiveerd. Het pull-distributie punt wordt gecontroleerd om te bevestigen of het pull-distributie punt de inhoud heeft gedownload. Als het downloaden van de inhoud wordt uitgevoerd, verschuift de package overdracht Manager gedurende een andere 60 minuten voordat deze het pull-distributie punt opnieuw controleert. De cyclus gaat door totdat het pull-distributiepunt de inhoudstransfer voltooit.  
