---
title: Dash board voor product levenscyclus
titleSuffix: Configuration Manager
description: Bekijk het micro soft Lifecycle-beleid met het dash board product levenscyclus in Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714239"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Micro soft Lifecycle-beleid beheren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Vanaf versie 1806 kunt u het dash board van de Configuration Manager product levenscyclus gebruiken om het micro soft Lifecycle-beleid weer te geven. Het dash board toont de status van het micro soft Lifecycle-beleid voor micro soft-producten geïnstalleerd op apparaten die worden beheerd met Configuration Manager. Ook vindt u hier informatie over de micro soft-producten in uw omgeving, de ondersteunings status en de ondersteuning voor eind datums. Gebruik het dash board om inzicht te krijgen in de beschik baarheid van de ondersteuning voor elk product. Deze informatie helpt u bij het bijwerken van de micro soft-producten die u gebruikt voordat het huidige einde van de ondersteuning wordt bereikt.  

Zie het [micro soft Lifecycle-beleid](https://support.microsoft.com/lifecycle)voor meer informatie.

Vanaf versie 1810 bevat het dash board informatie over System Center 2012 Configuration Manager en hoger.<!--1358702-->  



## <a name="prerequisites"></a>Vereisten 

 Voor het weer geven van gegevens in het dash board voor product levenscyclus zijn de volgende onderdelen vereist:  

- Internet Explorer 9 of hoger moet zijn geïnstalleerd op de computer waarop de Configuration Manager-console wordt uitgevoerd.  

- De rol van een service aansluitpunt moet zijn geïnstalleerd en geconfigureerd. Als u updates wilt ophalen voor de gegevens op dit dash board, moet het service verbindings punt online zijn of regel matig worden gesynchroniseerd als het offline is. Zie [about the Service Connection Point](../../../servers/deploy/configure/about-the-service-connection-point.md)(Engelstalig) voor meer informatie.

- Een Reporting Services-punt is vereist voor hyperlink functionaliteit in het dash board. De dashboard koppelingen naar rapporten van SQL Server Reporting Services (SSRS). Zie [Introduction to Reporting](../../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.  

- Het Asset Intelligence-synchronisatie punt moet worden geconfigureerd en gesynchroniseerd. Het dash board gebruikt de Asset Intelligence-catalogus als meta gegevens voor product titels. De meta gegevens worden vergeleken met de inventarisatie gegevens in uw hiërarchie. Zie [Asset Intelligence configureren in Configuration Manager](configuring-asset-intelligence.md)voor meer informatie.  
  - Als u het Asset Intelligence-Service punt voor de eerste keer configureert, zorg er dan voor dat [Asset Intelligence-hardware-inventaris klassen worden ingeschakeld](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence). Het levenscyclus dashboard is afhankelijk van de hardware-inventaris klassen van Asset Intelligence. In het dash board worden geen gegevens weer gegeven totdat clients hebben gescand op hardware-inventaris en deze hebben geretourneerd.  
  - Als u informatie over Extended Security updates (ESU) in dit dash board wilt weer geven, schakelt u de hardware-inventaris klasse **Software Licensing product-Asset Intelligence (SoftwareLicensingProduct)** in. Zie [Asset Intelligence-hardware-inventaris klassen inschakelen](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)voor meer informatie. <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>Het dash board voor product levenscyclus gebruiken

Op basis van de inventarisatie gegevens die door de site worden verzameld van beheerde apparaten, wordt in het dash board informatie over alle huidige producten weer gegeven. De informatie die wordt weer gegeven voor besturings systemen en SQL Server, is echter beperkt tot de volgende versies:

- Windows Server 2008 en hoger
- Windows XP en hoger
- SQL Server 2008 en hoger

Als u het dash board levenscyclus wilt openen in de Configuration Manager-console, gaat u naar de werk ruimte **activa en naleving** , vouwt u **Asset Intelligence**uit en selecteert u het knoop punt **product levenscyclus** .

> [!NOTE]  
> De gegevens in het dash board zijn gebaseerd op de site waarmee de Configuration Manager-console verbinding maakt. Als de-console verbinding maakt met uw site op het hoogste niveau, ziet u de gegevens voor de volledige hiërarchie. Wanneer er verbinding wordt gemaakt met een onderliggende primaire site, worden alleen gegevens van die site weer gegeven.

### <a name="product-lifecycle-dashboard"></a>Dash board voor product levenscyclus

![Scherm afbeelding van het dash board product levenscyclus in de-console](media/product-lifecycle-dashboard.png)

Wijzig de weer gave door een van de volgende opties te selecteren in de lijst **product categorie** :  
- **Alle**: alle producten samen weer geven  
- **Windows-client**: versies van Windows client-besturings systeem weer geven  
- **Windows Server**: versies van Windows Server-besturings systeem weer geven  
- **Data Base**: SQL Server versies weer geven  
- **Configuration Manager**: vanaf versie 1810 kunt u Configuration Manager versies weer geven 
- **Microsoft Office**: vanaf versie 1902 kunt u informatie weer geven voor geïnstalleerde versies van Office 2003 tot en met Office 2016 <!--3556026-->

Het dashboard bevat de volgende tegels:  

- **Top 5 van producten die het einde van de levens duur**hebben bereikt: deze tegel is een geconsolideerde gegevens weergave van producten die in uw omgeving zijn gevonden, voorbij hun einde van de levens duur. De grafiek toont de geïnstalleerde software die is verlopen in vergelijking met de ondersteunings levenscyclus van besturings systemen en SQL Server-producten.  

- **Top 5 van producten die het einde van de levens duur bijna hebben bereikt**: deze tegel is een geconsolideerde gegevens weergave van producten die in uw omgeving worden gevonden en die in de komende 18 maanden het einde van de levens duur bijna zijn. In de grafiek ziet u de geïnstalleerde software binnen 18 maanden aan einde van de levens duur in vergelijking met de ondersteunings levenscyclus van besturings systemen en SQL Server-producten.  

- **Levenscyclus gegevens voor geïnstalleerde producten**: deze tegel geeft u een algemeen idee wanneer een product overschakelt van ondersteuning naar de verlopen status. De grafiek bevat een uitsplitsing van het aantal clients waarop het product is geïnstalleerd, de beschik baarheid van de ondersteunings status en een koppeling voor meer informatie over de volgende stappen die u moet uitvoeren. De volgende informatie is opgenomen in de grafiek:     
    - Resterende ondersteunings tijd
    - Aantal in omgeving 
    - Eind datum voor algemene ondersteuning
    - Eind datum voor uitgebreide ondersteuning
    - Volgende stappen  

> [!IMPORTANT]  
> De gegevens die in dit dash board worden weer gegeven, zijn voor uw gemak en alleen voor intern gebruik binnen uw bedrijf. U moet niet alleen vertrouwen op deze informatie om de naleving te bevestigen. Zorg ervoor dat u de nauw keurigheid controleert van de informatie die u hebt ontvangen, samen met de beschik baarheid van ondersteunings informatie, door naar het [micro soft Lifecycle-beleid](https://support.microsoft.com/lifecycle)te gaan.  



## <a name="reporting"></a>Rapporten

Er zijn ook aanvullende rapporten beschikbaar. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **rapportage**uit en vouw **rapporten**uit. De volgende nieuwe rapporten worden toegevoegd onder de categorie **Asset Intelligence**:  

- **Levens cyclus 01A-computers met een specifiek software product**: een lijst weer geven met computers waarop een opgegeven product is gedetecteerd.  

- **Levenscyclus 02a-lijst met computers met verlopen producten in de organisatie**: computers weer geven waarop de producten zijn verlopen. U kunt dit rapport filteren op product naam.

- **Levenscyclus 03A-lijst met verlopen producten die in de organisatie zijn gevonden**: Details weer geven voor producten in uw omgeving die datums met een verstreken levens duur hebben.  

- **Levenscyclus 04a-algemeen overzicht van product levenscyclus**: een lijst met product levenscyclussen weer geven. De lijst filteren op product naam en dagen tot verval datum.  

- **Levenscyclus 05A-dash board voor product levenscyclus**: vanaf versie 1810 bevat dit rapport soort gelijke informatie als het dash board in de console. Selecteer een categorie om het aantal producten in uw omgeving weer te geven en Bekijk de dagen van de resterende ondersteuning.  

Zie [lijst met rapporten](../../../servers/manage/list-of-reports.md#asset-intelligence)voor meer informatie.<!--SCCMDocs issue 997-->  
