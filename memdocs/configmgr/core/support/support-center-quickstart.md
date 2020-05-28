---
title: Snelstartgids voor ondersteunings centrum
titleSuffix: Configuration Manager
description: Leg snel de status vast van een Configuration Manager-client voor het oplossen van problemen.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723115"
---
# <a name="support-center-quickstart-guide"></a>Snelstartgids gids voor ondersteunings centrum

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het ondersteunings centrum heeft krachtige mogelijkheden, waaronder probleem oplossing en real-time logboek weergave. Het kan ook in slechts enkele minuten worden gebruikt om de status van een Configuration Manager client computer vast te leggen. Deze mogelijkheid omvat het verkrijgen van toegang tot externe clients.

Maak een volledig *probleemoplossings bundel* bestand (. zip) waarmee de client status wordt vastgelegd. De bundel bevat geen logboek bestanden. Het kan ook andere soorten gegevens bevatten, zoals register instellingen en client configuraties. Geef de bundel door aan een ondersteunings technicus die de viewer voor ondersteunings centrum gebruikt.



## <a name="prerequisites"></a>Vereisten

- Lokale beheerders rechten voor een Configuration Manager-client  

- Het installatie programma van het ondersteunings centrum. Dit bestand bevindt zich op de site server op `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi` . Zie [ondersteunings centrum-installeren](support-center.md#install)voor meer informatie.  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Stap 1: een gegevens bundel maken op een lokale client

1.  Installeer het ondersteunings centrum op de Configuration Manager-client.  

2.  Ga naar het menu **Start** en selecteer in de groep **micro soft System Center** het **ondersteunings centrum**.  

3.  Op het tabblad Start van het lint selecteert u **geselecteerde gegevens verzamelen**. Standaard verzamelt het ondersteunings centrum de minimale gegevensset: logboek bestanden, client configuratie en besturings systeem.  

4.  Sla het bundel bestand voor probleem oplossing (. zip) op naar een map op de computer. De bestands naam is standaard vergelijkbaar met het volgende voor beeld: `Support_c885cdfed3c7482bba4f9e662978ec07.zip` .  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Stap 2: de gegevens bundel weer geven met de viewer van ondersteunings centrum

1.  Start de **Viewer voor ondersteunings centrum**. Deze actie kan zich voordoen op elke computer waarop u het ondersteunings centrum installeert.  

2.  Selecteer **bundel openen**, blader naar het bundel bestand en selecteer **openen**.  

3.  Nadat het bestand door de viewer van het ondersteunings centrum wordt verwerkt, schakelt u over naar elk beschikbaar tabblad. de typen gegevens weer geven die door het ondersteunings centrum standaard worden verzameld:  

    - **Configuratie**  

        - Client configuratie Configuration Manager  

        - Besturingssysteem  

        - Computer  

        - Services  

        - Netwerkadapters  

    - **Logboeken**: Kies een of meer items in de lijst en selecteer **openen**. Met deze actie worden de geselecteerde logboek bestanden geopend in de logboeken viewer. Gebruik deze functie om fout codes op te zoeken en geavanceerde filters te gebruiken om logboek bestanden sneller te analyseren.  



## <a name="collect-more-data"></a>Meer gegevens verzamelen

Naast deze basis mogelijkheden kan het ondersteunings centrum ook een grote verscheidenheid aan andere informatie over de client status verzamelen. Open het **ondersteunings centrum** en selecteer **alle gegevens verzamelen**. Dit proces duurt doorgaans enkele minuten, zelfs op nieuwere computers. Ondersteunings centrum verzamelt de volgende aanvullende gegevens:

- **Beleid**: beleids instellingen voor Configuration Manager, met inbegrip van de aangevraagde beleids configuratie en de daad werkelijke beleids configuratie  

- **Certificaten**: informatie over de open bare sleutel voor client certificaten. Het ondersteunings centrum verzamelt geen persoonlijke sleutel van het certificaat.  

- **Client register**: verzamelt client configuratie gegevens uit het REGI ster. Ondersteunings centrum verzamelt alleen Configuration Manager register gegevens.  

- **Client-WMI**: client configuratie gegevens van WMI. Het ondersteunings centrum verzamelt geen client beleid.  

- **Problemen oplossen**: realtime-probleemoplossings gegevens om veelvoorkomende client problemen met Active Directory, beheer punten, netwerken, beleids toewijzingen en registratie te helpen vaststellen.  

- **Debug-dumps**: Voer debug dump van client en gerelateerde processen uit. De dump van de fout opsporing kan groot zijn. Schakel deze optie alleen in bij het oplossen van problemen met client prestaties.  

