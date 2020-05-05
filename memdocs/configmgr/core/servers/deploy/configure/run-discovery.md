---
title: Apparaat-en gebruikers bronnen detecteren
titleSuffix: Configuration Manager
description: Lees een overzicht van de records detectie proces en detectie gegevens.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1869c9e6de455b7086a051db91bb26bc00a91a5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718369"
---
# <a name="run-discovery-for-configuration-manager"></a>Detectie uitvoeren voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

U gebruikt een of meer detectie methoden in Configuration Manager om apparaat-en gebruikers bronnen te vinden die u kunt beheren. U kunt ook detectie gebruiken om de netwerk infrastructuur in uw omgeving te identificeren. Er zijn verschillende methoden die u kunt gebruiken om verschillende dingen te ontdekken en elke methode heeft zijn eigen configuraties en beperkingen.  

## <a name="overview-of-discovery"></a>Overzicht van detectie  
 Detectie is het proces waarmee Configuration Manager informatie over de dingen die u kunt beheren. De beschikbare detectiemethoden zijn:  

-   Detectie van Active Directory-forests  

-   Active Directory-groepdetectie  

-   Active Directory-systeemdetectie  

-   Detectie Active Directory-gebruiker  

-   Heartbeat-detectie  

-   Netwerkdetectie  

-   Serverdetectie  

> [!TIP]  
>  Meer informatie over de afzonderlijke detectie methoden vindt u in [informatie over detectie methoden voor Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Zie [detectie methoden selecteren om te gebruiken voor Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)voor hulp bij het selecteren van de te gebruiken methoden en op welke sites in uw hiërarchie.  

 Als u de meeste detectie methoden wilt gebruiken, moet u de methode op een site inschakelen en instellen op zoeken naar specifieke netwerk-of Active Directory locaties. Wanneer de service wordt uitgevoerd, wordt de opgegeven locatie opgevraagd voor informatie over apparaten of gebruikers die Configuration Manager kunnen beheren. Wanneer met een detectie methode informatie over een bron wordt gevonden, wordt die informatie in een bestand met de naam detectie gegevens record (DDR) geplaatst. Dat bestand wordt vervolgens verwerkt door een primaire of centrale beheer site. Als een DDR wordt verwerkt, wordt voor nieuwe gedetecteerde bronnen een nieuw record gemaakt in de sitedatabase. De records van bestaande bronnen worden bijgewerkt met de nieuwe informatie.  

 Sommige detectie methoden kunnen een grote hoeveelheid netwerk verkeer genereren en de Ddr's die ze produceren, kunnen leiden tot een aanzienlijk gebruik van CPU-resources tijdens de verwerking. Plan daarom het gebruik van alleen die detectie methoden die u nodig hebt om te voldoen aan uw doelen. U kunt bijvoorbeeld beginnen met slechts één of twee detectiemethoden en later op een gecontroleerde manier verdere methoden inschakelen om het detectieniveau in uw omgeving uit te breiden.  

 Nadat de detectie gegevens zijn toegevoegd aan de site database, wordt de informatie vervolgens gerepliceerd naar elke site in de hiërarchie, ongeacht waar deze is gedetecteerd of verwerkt. Daarom kunt u verschillende planningen en instellingen voor detectie methoden op verschillende sites instellen, maar kunt u een specifieke detectie methode op slechts één site uitvoeren. Dit vermindert het gebruik van netwerk bandbreedte door dubbele detectie acties en vermindert de verwerking van redundante detectie gegevens op meerdere sites.  

 U kunt detectie gegevens gebruiken voor het maken van aangepaste verzamelingen en query's waarmee resources logisch worden gegroepeerd voor beheer taken. Bijvoorbeeld:  

-   Client installaties pushen of bijwerken.  

-   Inhoud implementeren voor gebruikers of apparaten.  

-   Client instellingen en gerelateerde configuraties implementeren.

##  <a name="about-discovery-data-records"></a><a name="BKMK_DDRs"></a>Informatie over detectie gegevens records  
 Ddr's zijn bestanden die door een detectie methode zijn gemaakt. Ze bevatten informatie over een bron die u kunt beheren in Configuration Manager, zoals computers, gebruikers en in sommige gevallen, netwerk infrastructuur. Ze worden verwerkt op primaire sites of op centrale beheersites. Nadat de bron informatie in de DDR is ingevoerd in de-data base, wordt de DDR verwijderd en worden de gegevens gerepliceerd als globale gegevens naar alle sites in de hiërarchie.  

 De site waarop een DDR wordt verwerkt, hangt af van de informatie die het bevat:  

-   Ddr's voor nieuwe gedetecteerde bronnen die zich niet in de data base bevinden, worden verwerkt op de site op het hoogste niveau van de hiërarchie. De site op het hoogste niveau maakt een nieuwe bron record in de data base en wijst deze toe aan een unieke id. Ddr's overdragen door replicatie op basis van bestanden tot de site op het hoogste niveau is bereikt.  

-   DDR's voor eerder gedetecteerde objecten zijn op primaire sites verwerkt. Onderliggende sites dragen geen DDR's over naar de centrale beheersite, wanneer de DDR informatie bevat over een bron die reeds in de database aanwezig is.  

-   Secundaire sites verwerken geen Ddr's en dragen deze altijd over naar de bovenliggende primaire site van de replicatie op basis van een bestand.  

DDR-bestanden worden geïdentificeerd door de .ddr-extense en hebben een typische grootte van ongeveer 1 KB.  

## <a name="get-started-with-discovery"></a>Aan de slag met detectie:  
 Voordat u de Configuration Manager-console kunt gebruiken om detectie in te stellen, moet u inzicht hebben in de verschillen tussen de methoden, wat ze kunnen doen en wat hun beperkingen zijn.  

De volgende onderwerpen kunnen een basis vormen waarmee u detectie methoden met succes kunt gebruiken:  

-   [Over detectie methoden voor Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Detectie methoden selecteren om te gebruiken voor Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md)  

Wanneer u de methoden die u wilt gebruiken begrijpt, kunt u aan de hand van de richt lijnen [voor het configureren van detectie methoden voor Configuration Manager de hulp middelen voor](../../../../core/servers/deploy/configure/configure-discovery-methods.md)het instellen van een methode zoeken.  
