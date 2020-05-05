---
title: Detectiemethoden selecteren
titleSuffix: Configuration Manager
description: Bekijk de overwegingen voor de methoden die u wilt gebruiken en op welke sites ze moeten worden uitgevoerd.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f08ab44a11b48b4446a372c4f6065ea0d7c63e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718348"
---
# <a name="select-discovery-methods-to-use-for-configuration-manager"></a>Detectie methoden selecteren om te gebruiken voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor een succes volle en efficiënt gebruik van detectie voor Configuration Manager, moet u overwegen welke methoden u wilt gebruiken en op welke sites ze moeten worden uitgevoerd.  

 Omdat detectie een grote hoeveelheid netwerk verkeer kan genereren en de resulterende detectie gegevens records (Ddr's) aanzienlijke CPU-bronnen kunnen gebruiken tijdens de verwerking, kunt u alleen die detectie methoden gebruiken die u nodig hebt om te voldoen aan uw doelen. U kunt beginnen met slechts één of twee detectie methoden en later extra methoden op een gecontroleerde manier inschakelen om het detectie niveau in uw omgeving uit te breiden. Aan de hand van de informatie in dit onderwerp kunt u weloverwogen beslissingen nemen.  

 Zie [over detectie methoden voor Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)voor meer informatie over de verschillende detectie methoden.  

## <a name="select-methods-to-discover-different-things"></a>Methoden selecteren om verschillende dingen te ontdekken  
 Als u potentiële Configuration Manager-client computers of gebruikers bronnen wilt detecteren, moet u de juiste detectie methoden inschakelen. U kunt verschillende combi Naties van detectie methoden gebruiken om verschillende bronnen te vinden en om aanvullende informatie over die bronnen te ontdekken. De detectie methoden die u gebruikt bepalen het type resources dat wordt gedetecteerd en welke Configuration Manager services en agents worden gebruikt in het detectie proces. Ze bepalen ook het type informatie over de bronnen die u kunt detecteren.  

### <a name="discover-computers"></a>Computers detecteren   
Wanneer u computers wilt detecteren, kunt u **Active Directory systeem detectie** of **netwerk detectie**gebruiken.  

 Als u bijvoorbeeld resources wilt detecteren die de Configuration Manager-client kunnen installeren voordat u client push installatie gebruikt, kunt u Active Directory systeem detectie uitvoeren. Met deze methode detecteert u de resource niet alleen en detecteert u ook basis informatie, zelfs uitgebreide informatie over de bron van Active Directory Domain Services. Deze informatie kan nuttig zijn bij het bouwen van complexe query's en verzamelingen die moeten worden gebruikt voor de toewijzing van client instellingen of inhouds implementatie.

U kunt ook netwerk detectie uitvoeren en de bijbehorende opties gebruiken om het besturings systeem van bronnen te detecteren (vereist om later client push installatie te gebruiken). Netwerk detectie biedt informatie over uw netwerk topologie die u niet kunt verkrijgen met andere detectie methoden. Deze methode biedt echter geen informatie over uw Active Directory omgeving.

 Er is ook een methode met de naam **heartbeat-detectie**. Het is mogelijk alleen heartbeat-detectie te gebruiken om de detectie van clients die u hebt geïnstalleerd door andere methoden dan client push installatie af te dwingen. Maar in tegens telling tot andere detectie methoden kan heartbeat-detectie geen computers detecteren die geen actieve Configuration Manager-client hebben. Het retourneert een beperkte set informatie, bedoeld om een bestaande database record te onderhouden en niet de basis van die record te zijn. Gegevens die door heartbeat-detectie worden verzonden, zijn mogelijk niet voldoende om complexe query's of verzamelingen te bouwen.  

 Als u **Active Directory groeps detectie** gebruikt om het lidmaatschap van een opgegeven groep te detecteren, kunt u beperkte systeem-of computer informatie ontdekken. Dit vervangt geen volledige detectie van computers, maar kan basis informatie geven. Deze informatie is onvoldoende voor client push installatie.  

### <a name="discover-users"></a>Gebruikers detecteren   
Als u informatie over gebruikers wilt detecteren, gebruikt u **Active Directory gebruikers detectie**. Net als bij Active Directory systeem detectie detecteert deze methode gebruikers van Active Directory. Het bevat algemene informatie, naast uitgebreide Active Directory informatie. U kunt deze informatie gebruiken om complexe query's en verzamelingen op te bouwen die vergelijkbaar zijn met die voor computers.  

### <a name="discover-group-information"></a>Groeps informatie detecteren   
Als u informatie over groepen en groepslid maatschappen wilt detecteren, gebruikt u **Active Directory groeps detectie**. Deze detectie methode maakt bron records voor beveiligings groepen.  

 U kunt deze methode gebruiken om te zoeken naar een specifieke Active Directory groep om de leden van die groep te identificeren, naast alle geneste groepen binnen die groep. U kunt deze methode ook gebruiken om te zoeken op een Active Directory locatie voor groepen, en doorzoeken recursief elke onderliggende container van die locatie in Active Directory Domain Services.  

 Deze detectie methode kan ook het lidmaatschap van distributie groepen doorzoeken. Dit kan de groeps relaties van zowel gebruikers als computers identificeren.  

 Wanneer u een groep detecteert, kunt u ook beperkte informatie over de leden ontdekken. Hierdoor worden de Active Directory systeem-of gebruikers detectie methoden echter niet vervangen. Normaal gesp roken is het niet voldoende om complexe query's en verzamelingen te bouwen, of als basis voor een Push-client installatie.  

### <a name="discover-infrastructure"></a>Infra structuur detecteren   
Er zijn twee methoden die u kunt gebruiken om de netwerk infrastructuur te detecteren, **Active Directory forest-detectie** en **netwerk detectie**.  

 Gebruik Active Directory forest-detectie om een Active Directory forest te doorzoeken op informatie over subnetten en Active Directory site configuraties. Deze configuraties kunnen vervolgens automatisch worden ingevoerd in Configuration Manager als grens locaties.  

 Wanneer u uw netwerk topologie wilt detecteren, gebruikt u netwerk detectie. Hoewel andere detectie methoden informatie retour neren met betrekking tot Active Directory Domain Services en de huidige netwerk locatie van een client kunnen identificeren, bieden ze geen infrastructuur gegevens op basis van de subnetten en router topologie van uw netwerk.  

##  <a name="discovery-data-is-shared-among-sites"></a><a name="bkmk_shared"></a>Detectie gegevens worden gedeeld tussen sites  
 Nadat Configuration Manager detectie gegevens toevoegt aan een Data Base, wordt deze snel gedeeld tussen alle sites in de hiërarchie. Omdat er doorgaans geen voor deel is dat dezelfde gegevens op meerdere sites in uw hiërarchie wordt gedetecteerd, kunt u een enkele instantie van elke detectie methode instellen die u gebruikt om op één site uit te voeren. Het is een goed idee om dit te doen in plaats van meerdere exemplaren van één methode op verschillende sites uit te voeren.  

 Voor sommige omgevingen kan het echter handig zijn om dezelfde detectie methode toe te wijzen voor uitvoering op meerdere sites, elk met een afzonderlijke configuratie en planning. Wanneer u bijvoorbeeld netwerk detectie gebruikt, wilt u mogelijk elke site om het lokale netwerk te detecteren, in plaats van alle netwerk locaties in een WAN te detecteren.

Als u meerdere exemplaren van dezelfde detectie methoden wilt configureren om uit te voeren op verschillende sites, moet u de configuratie van elke site zorgvuldig plannen. U wilt voor komen dat twee of meer sites dezelfde resources van uw netwerk of Active Directory ontdekken. Dit kan extra netwerk bandbreedte verbruiken en dubbele Ddr's maken.

De volgende tabel geeft aan op welke sites u de verschillende detectie methoden kunt instellen.  

|Detectie methode|Ondersteunde locaties|  
|----------------------|-------------------------|  
|Detectie van Active Directory-forests|Centrale beheersite<br /><br /> Primaire site|  
|Active Directory-groepdetectie|Primaire site|  
|Active Directory-systeemdetectie|Primaire site|  
|Detectie Active Directory-gebruiker|Primaire site|  
|Heartbeat-detectie<sup>1</sup>|Primaire site|  
|Netwerkdetectie|Primaire site<br /><br /> Secundaire site|  

 <sup>1</sup> secundaire sites kunnen geen heartbeat-detectie configureren, maar kunnen de heartbeat-DDR van een client ontvangen.  

 Wanneer secundaire sites netwerk detectie uitvoeren of heartbeat-detectie-Ddr's ontvangen, overdragen ze de DDR door op bestanden gebaseerde replicatie naar hun bovenliggende primaire site. Dit komt doordat alleen de primaire sites en centrale beheer sites Ddr's kunnen verwerken. Zie [info over detectie gegevens records](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs)voor meer informatie over hoe ddr's worden verwerkt.  

## <a name="considerations-for-different-discovery-methods"></a>Overwegingen voor verschillende detectie methoden  
 Omdat elke site server en netwerk omgeving afwijkt, is het een goed idee om de initiële configuraties voor detectie te beperken. Bewaak vervolgens elke site server voor de mogelijkheid om de gegenereerde detectie gegevens te verwerken.  

Wanneer u een **Active Directory** detectie methode gebruikt voor systemen, gebruikers of groepen:  

-   Voer detectie uit op een site die een snelle netwerk verbinding met uw domein controllers heeft.  

-   Denk na over de Active Directory replicatie topologie om te controleren of de detectie toegang tot de meest recente gegevens heeft.  

-   Denk na over het bereik van de detectie configuratie en beperk de detectie tot alleen de Active Directory locaties en groepen die u moet detecteren.  

Als u **netwerk detectie**gebruikt:  

-   Gebruik een beperkte initiële configuratie om uw netwerk topografie te identificeren.  

-   Nadat u de netwerk-topografie hebt geïdentificeerd, stelt u netwerk detectie in om uit te voeren op specifieke sites die centraal zijn voor de netwerk gebieden die u vollediger wilt detecteren.  

Omdat **heartbeat-detectie** niet wordt uitgevoerd op een specifieke site, hoeft u dit niet te overwegen in algemene planning voor het uitvoeren van detectie.  

##  <a name="best-practices-for-discovery"></a><a name="bkmk_best"></a>Aanbevolen procedures voor detectie  
Voor de beste resultaten met detectie raden we het volgende aan:

- **Voer Active Directory systeem detectie uit en Active Directory gebruikers detectie voordat u Active Directory groeps detectie uitvoert.**  

  Wanneer Active Directory groeps detectie een eerder niet-gedetecteerde gebruiker of computer identificeert als lid van een groep, wordt geprobeerd de basis gegevens voor de gebruiker of computer te detecteren. Omdat de detectie van Active Directory groepen niet is geoptimaliseerd voor dit type detectie, kan dit proces ertoe leiden dat het langzaam wordt uitgevoerd. Daarnaast identificeert Active Directory groeps detectie alleen de basis gegevens over de gebruikers en computers die deze detecteert en maakt geen volledige detectie record voor de gebruiker of computer. Wanneer u Active Directory systeem detectie uitvoert en gebruikers detectie Active Directory, zijn de aanvullende Active Directory kenmerken voor elk object type beschikbaar. Als gevolg hiervan wordt Active Directory groeps detectie efficiënter uitgevoerd.  

- **Wanneer u Active Directory groeps detectie instelt, geeft u alleen groepen op die u gebruikt met Configuration Manager.**  

  Als u het gebruik van resources door Active Directory groeps detectie wilt beheren, geeft u alleen de groepen op die u gebruikt met Configuration Manager. Dit komt omdat Active Directory groeps detectie recursief zoekt in elke groep die wordt gedetecteerd voor gebruikers, computers en geneste groepen. De zoek opdracht van elke geneste groep kan het bereik van Active Directory groeps detectie uitbreiden en de prestaties verminderen. Wanneer u detectie van verschillen voor Active Directory groeps detectie instelt, wordt door de detectie methode elke groep gecontroleerd op wijzigingen. Dit vermindert de prestaties verder wanneer de methode overbodige groepen moet doorzoeken.  

- **Stel detectie methoden in met een langer interval tussen volledige detectie en een frequentere periode voor detectie van verschillen.**  

  Omdat Delta detectie gebruikmaakt van minder bronnen dan een volledige detectie cyclus en kan nieuwe of gewijzigde resources in Active Directory identificeren, kunt u de frequentie van volledige detectie cycli verlagen om wekelijks (of minder) uit te voeren. Detectie van verschillen voor Active Directory systeem detectie Active Directory gebruikers detectie en Active Directory groeps detectie identificeert bijna alle wijzigingen van Active Directory-objecten en kan nauw keurige detectie gegevens voor resources behouden.  

- **Voer Active Directory detectie methoden uit op een primaire site met een netwerk locatie die zich het dichtst bij uw Active Directory domein controller bevindt.**  

  Voor het verbeteren van de prestaties van Active Directory detectie, is het een goed idee om Discover uit te voeren op een primaire site die een snelle netwerk verbinding heeft met uw domein controllers. Als u dezelfde Active Directory detectie methode op meerdere sites uitvoert, stelt u elke detectie methode in om overlap ping te voor komen. In tegens telling tot eerdere versies van Configuration Manager, worden detectie gegevens gedeeld tussen sites. Daarom is het niet nodig dezelfde informatie te detecteren op meerdere sites. Zie [detectie gegevens worden gedeeld tussen sites](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared)voor meer informatie.  

- **Voer Active Directory forest-detectie uit op slechts één site wanneer u van plan bent om automatisch grenzen te maken op basis van de detectie gegevens.**  

  Als u Active Directory forest-detectie uitvoert op meer dan één site in een hiërarchie, is het een goed idee om alleen opties in te scha kelen om automatisch grenzen te maken op één site. Dit komt doordat wanneer Active Directory forest-detectie wordt uitgevoerd op elke site en grenzen maakt, Configuration Manager deze grenzen niet samen voegen tot één grens object. Wanneer u Active Directory forest-detectie configureert om automatisch grenzen te maken op meerdere sites, kan het resultaat dubbele grens objecten zijn in de Configuration Manager-console.  
