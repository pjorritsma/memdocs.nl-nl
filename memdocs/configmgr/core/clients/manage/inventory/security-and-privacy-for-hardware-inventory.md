---
title: Privacy voor hardware-inventaris
titleSuffix: Configuration Manager
description: Informatie over beveiliging en privacy voor hardware-inventaris in Configuration Manager ophalen.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a5989c80818ac45bb8dd6a4f768595dbd56b846d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710683"
---
# <a name="security-and-privacy-for-hardware-inventory-in-configuration-manager"></a>Beveiliging en privacy voor hardware-inventarisatie in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat beveiligings-en privacy-informatie voor hardware-inventarisatie in Configuration Manager.  

##  <a name="security-best-practices-for-hardware-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Aanbevolen beveiligingsprocedures voor hardware-inventarisatie  
 Gebruik de volgende aanbevolen beveiligingsprocedures wanneer u hardware-inventarisgegevens bij clients verzamelt:  

|Aanbevolen beveiligingsprocedure|Meer informatie|  
|----------------------------|----------------------|  
|Inventarisgegevens ondertekenen en versleutelen|Wanneer clients via HTTPS communiceren met beheerpunten, worden alle gegevens die ze verzenden met behulp van SSL versleuteld. Wanneer clientcomputers echter op het intranet via HTTP met beheerpunten communiceren, kunnen clientinventarisgegevens en verzamelde bestanden niet-ondertekend en niet-versleuteld worden verzonden. Zorg ervoor dat de site zodanig is geconfigureerd dat ondertekening is vereist en versleuteling wordt gebruikt. Bovendien, als clients het SHA-256-algoritme kunnen ondersteunen, selecteer dan de optie die SHA-256 vereist.|  
|Verzamel geen IDMIF- en NOIDMIF-bestanden in sterk beveiligde omgevingen|U kunt verzamelen van IDMIF- en NOIDMIF-bestanden gebruiken om het verzamelen voor hardware-inventarisatie uit te breiden. Configuration Manager maakt zo nodig nieuwe tabellen of wijzigt bestaande tabellen in de Configuration Manager-Data Base om de eigenschappen in IDMIF-en NOIDMIF-bestanden aan te passen. Configuration Manager maakt echter geen gebruik van IDMIF-en NOIDMIF-bestanden, zodat deze bestanden kunnen worden gebruikt om tabellen te wijzigen waarvan u niet wilt dat ze worden gewijzigd. Geldige gegevens kunnen worden overschreven door ongeldige gegevens. Bovendien kunnen grote hoeveel heden gegevens worden toegevoegd en kan de verwerking van deze gegevens vertragingen veroorzaken in alle Configuration Manager-functies. Configureer de clientinstelling voor hardware-inventarisatie **MIF-bestanden verzamelen** als **Geen**om deze risico's te beperken.|  

### <a name="security-issues-for-hardware-inventory"></a>Beveiligingsproblemen voor hardware-inventarisatie  
 Bij het verzamelen van inventaris komen potentiële beveiligingslekken naar voren. Kwaadwillende personen kunnen het volgende doen:  

- Ongeldige gegevens verzenden, die door het beheerpunt worden geaccepteerd, zelfs wanneer de clientinstelling voor software-inventaris is uitgeschakeld en bestandsverzameling niet is ingeschakeld.  

- Uitzonderlijk grote hoeveelheden gegevens verzenden in een enkel bestand en in heel veel bestanden, wat kan leiden tot een denial-of-service.  

- Toegang krijgen tot inventaris gegevens wanneer deze worden overgedragen naar Configuration Manager.  

  Omdat een gebruiker met lokale beheerders bevoegdheden informatie als inventaris gegevens kan verzenden, moet u de inventaris gegevens die door Configuration Manager worden verzameld, niet beschouwen als gezaghebbend.  

  Hardware-inventarisatie is standaard ingeschakeld als een clientinstelling.  

##  <a name="privacy-information-for-hardware-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Privacy-informatie voor hardware-inventarisatie  
 Met de hardware-inventarisatie kunt u gegevens ophalen die zijn opgeslagen in het REGI ster en in WMI op Configuration Manager-clients. Met een software-inventarisatie kunt u alle bestanden van een bepaald type ontdekken of alle bestanden van een bepaald type bij clients verzamelen. Asset Intelligence verbetert de inventarisatiefuncties door hardware- en software-inventarisatie uit te breiden en nieuwe licentiebeheerfunctionaliteit toe te voegen.  

 Hardware-inventarisatie is standaard ingeschakeld als een clientinstelling en welke WMI-gegevens worden verzameld, wordt bepaald door de opties die u selecteert. Software-inventarisatie is standaard ingeschakeld, maar er worden standaard geen bestanden verzameld. Asset Intelligence-gegevensverzameling is automatisch ingeschakeld, maar u kunt selecteren welke hardware-inventarisrapportageklassen u wilt inschakelen.  

 Er wordt geen inventarisinformatie naar Microsoft verzonden. Inventarisatie gegevens worden opgeslagen in de Configuration Manager-Data Base. Wanneer clients HTTPS gebruiken om verbinding te maken met beheerpunten, worden de inventarisatiegegevens die ze naar de site verzenden tijdens de overdracht versleuteld. Als clients HTTP gebruiken om verbinding te maken met beheerpunten, hebt u de mogelijkheid versleuteling voor het inventarisatieproces in te schakelen. De inventarisatiegegevens worden niet in een versleutelde indeling in de database opgeslagen. Informatie wordt bewaard in de database tot deze om de 90 dagen wordt verwijderd door de siteonderhoudstaak **Verouderde inventarisgeschiedenis verwijderen** of **Verouderde verzamelde bestanden verwijderen** . U kunt het verwijderingsinterval configureren.  

 Bedenk wat uw privacyvereisten zijn voordat u hardware-inventarisatie, software-inventarisatie, het verzamelen van bestanden of het verzamelen van Asset Intelligence-gegevens configureert.  
