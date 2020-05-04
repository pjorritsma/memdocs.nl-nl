---
title: Software-inventaris beveiliging privacy
titleSuffix: Configuration Manager
description: Informatie over beveiliging en privacy voor software-inventaris in Configuration Manager ophalen.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d64fd2ac98996a6a1ccadae78e5f9cc576b55444
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710669"
---
# <a name="security-and-privacy-for-software-inventory-in-configuration-manager"></a>Beveiliging en privacy voor software-inventarisatie in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat beveiligings-en privacy-informatie voor software-inventarisatie in Configuration Manager.  

##  <a name="security-best-practices-for-software-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Aanbevolen beveiligingsprocedures voor software-inventaris  
 Gebruik de volgende aanbevolen beveiligingsprocedures voor wanneer u software-inventarisgegevens bij clients verzamelt:  

|Aanbevolen beveiligingsprocedure|Meer informatie|  
|----------------------------|----------------------|  
|Inventarisgegevens ondertekenen en versleutelen|Wanneer clients via HTTPS communiceren met beheerpunten, worden alle gegevens die ze verzenden met behulp van SSL versleuteld. Wanneer clientcomputers echter op het intranet via HTTP met beheerpunten communiceren, kunnen clientinventarisgegevens en verzamelde bestanden niet-ondertekend en niet-versleuteld worden verzonden. Zorg ervoor dat de site zodanig is geconfigureerd dat ondertekening is vereist en versleuteling wordt gebruikt. Bovendien, als clients het SHA-256-algoritme kunnen ondersteunen, selecteer dan de optie die SHA-256 vereist.|  
|Gebruik bestandsverzameling niet om essentiële bestanden of gevoelige gegevens te verzamelen|Configuration Manager software-inventaris gebruikt alle rechten van de LocalSystem-account, die de mogelijkheid heeft om kopieën van essentiële systeem bestanden te verzamelen, zoals het REGI ster of de data base van het beveiligings account. Wanneer deze bestanden beschikbaar zijn op de siteserver, kan iemand met het recht Bron lezen of het recht NTFS op de opgeslagen locatie de inhoud analyseren en mogelijk belangrijke informatie achterhalen over de client om vervolgens de beveiliging ervan in gevaar te brengen.|  
|Beperk lokale beheerrechten op clientcomputers|Een gebruiker met lokale beheerdersrechten kan ongeldige gegevens als inventarisatie-informatie verzenden.|  

### <a name="security-issues-for-software-inventory"></a>Beveiligingsproblemen voor software-inventaris  
 Bij het verzamelen van inventaris komen potentiële beveiligingslekken naar voren. Kwaadwillende personen kunnen het volgende doen:  

- Ongeldige gegevens verzenden, die door het beheerpunt worden geaccepteerd, zelfs wanneer de clientinstelling voor software-inventaris is uitgeschakeld en bestandsverzameling niet is ingeschakeld.  

- Uitzonderlijk grote hoeveelheden gegevens verzenden in een enkel bestand en in heel veel bestanden, wat kan leiden tot een denial-of-service.  

- Toegang krijgen tot inventaris gegevens wanneer deze worden overgedragen naar Configuration Manager.  

  Als gebruikers weten dat ze een verborgen bestand kunnen maken met de naam **Skpswi.dat** en dit in de hoofdmap op de harde schijf van een client kunnen plaatsen om dit uit te sluiten van software-inventaris, kunt u geen software-inventarisatiegegevens bij die computer verzamelen.  

  Omdat een gebruiker met lokale beheerders bevoegdheden informatie als inventaris gegevens kan verzenden, moet u de inventaris gegevens die door Configuration Manager worden verzameld, niet beschouwen als gezaghebbend.  

  Software-inventarisatie is standaard ingeschakeld als een clientinstelling.  

##  <a name="privacy-information-for-software-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Privacy-informatie voor software-inventarisatie  
 Met de hardware-inventarisatie kunt u gegevens ophalen die zijn opgeslagen in het REGI ster en in WMI op Configuration Manager-clients. Met een software-inventarisatie kunt u alle bestanden van een bepaald type ontdekken of alle bestanden van een bepaald type bij clients verzamelen. Asset Intelligence verbetert de inventarisatiefuncties door hardware- en software-inventarisatie uit te breiden en nieuwe licentiebeheerfunctionaliteit toe te voegen.  

 Hardware-inventarisatie is standaard ingeschakeld als een clientinstelling en welke WMI-gegevens worden verzameld, wordt bepaald door de opties die u selecteert. Software-inventarisatie is standaard ingeschakeld, maar er worden standaard geen bestanden verzameld. Asset Intelligence-gegevensverzameling is automatisch ingeschakeld, maar u kunt selecteren welke hardware-inventarisrapportageklassen u wilt inschakelen.  

 Er wordt geen inventarisinformatie naar Microsoft verzonden. Inventarisatie gegevens worden opgeslagen in de Configuration Manager-Data Base. Wanneer clients HTTPS gebruiken om verbinding te maken met beheerpunten, worden de inventarisatiegegevens die ze naar de site verzenden tijdens de overdracht versleuteld. Als clients HTTP gebruiken om verbinding te maken met beheerpunten, hebt u de mogelijkheid versleuteling voor het inventarisatieproces in te schakelen. De inventarisatiegegevens worden niet in een versleutelde indeling in de database opgeslagen. Informatie wordt bewaard in de database tot deze om de 90 dagen wordt verwijderd door de siteonderhoudstaak **Verouderde inventarisgeschiedenis verwijderen** of **Verouderde verzamelde bestanden verwijderen** . U kunt het verwijderingsinterval configureren.  

 Bedenk wat uw privacyvereisten zijn voordat u hardware-inventarisatie, software-inventarisatie, het verzamelen van bestanden of het verzamelen van Asset Intelligence-gegevens configureert.  
