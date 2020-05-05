---
title: Taalpakketten
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare taal ondersteuning in Configuration Manager.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ec5581567925ee57300274e50288058e06d80ec0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718187"
---
# <a name="language-packs-in-configuration-manager"></a>Taal pakketten in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel vindt u technische gegevens over taal ondersteuning in Configuration Manager. Configuration Manager site servers en-clients worden beschouwd als taal onafhankelijk. Voeg ondersteuning toe voor weergave talen door **server taal pakketten** of **client taal pakketten** te installeren op een centrale beheer site en op primaire sites. U selecteert de server-en client talen voor ondersteuning op een site vanuit de beschik bare taal pakket bestanden tijdens het installatie proces van de site.
 
Installeer meerdere talen op elke site. U hoeft alleen de talen te installeren die u gebruikt.  

- Elke-site ondersteunt meerdere talen voor Configuration Manager-consoles.  

- Voeg alleen ondersteuning toe voor de client talen die u wilt ondersteunen door afzonderlijke client taal pakketten te installeren op elke site.  

Wanneer u ondersteuning installeert voor een taal die overeenkomt met de volgende onderdelen:  

- De weergave taal van een computer: zowel de Configuration Manager-console als de gebruikers interface van de client die op die computer wordt uitgevoerd, geven informatie weer in die taal.  

- De taal voorkeur die wordt gebruikt door de webbrowser van een computer: verbindingen met webgebaseerde informatie, waaronder de toepassingscatalogus of SQL Server Reporting Services, worden weer gegeven in die taal.  


Wanneer u Configuration Manager Setup uitvoert, worden taal pakket bestanden gedownload als onderdeel van de vereisten en herdistribueerbare bestanden. U kunt ook het Download [programma](setup-downloader.md) voor de installatie gebruiken om deze bestanden te downloaden voordat u het installatie programma uitvoert.   



## <a name="server-languages"></a>Server talen  

Gebruik de volgende tabel om een land instellingen-ID toe te wijzen aan een taal die u op servers wilt ondersteunen. Zie [locale-id's die door micro soft zijn toegewezen](https://go.microsoft.com/fwlink/p/?LinkId=252609)voor meer informatie over land instellingen-id's.  

|Servertaal|Landinstellingen-id (LCID)|Code van drie letters|  
|---------------------|------------------------|-----------------------|  
|Engels (standaard)|0409|ENU|  
|Chinees (Vereenvoudigd)|0804|CHS|  
|Chinees (Traditioneel, Taiwan)|0404|CHT|  
|Tsjechisch|0405|CSY|  
|Nederlands - Nederland|0413|NLD|  
|Frans|040c|FRA|  
|Duits|0407|DEU|  
|Hongaars|040e|HUN|  
|Italiaans - Italië|0410|ITA|  
|Japans|0411|JPN|  
|Koreaans|0412|KOR|  
|Pools|0415|PLK|  
|Portuguese - Brazil|0416|PTB|  
|Portugees - Portugal|0816|PTG|  
|Russisch|0419|RUS|  
|Spaans – Spanje|0c0a|ESN|  
|Zweeds|041d|SVE|  
|Turks|041f|TRK|  



## <a name="client-languages"></a>Client talen  

Gebruik de volgende tabel om een land instellingen-ID toe te wijzen aan een taal die u wilt ondersteunen op client computers. Zie [locale-id's die door micro soft zijn toegewezen](https://go.microsoft.com/fwlink/p/?LinkId=252609)voor meer informatie over land instellingen-id's.  

|Clienttaal|Landinstellingen-id (LCID)|Code van drie letters|  
|---------------------|------------------------|-----------------------|  
|Engels (standaard)|0409|NL|  
|Chinees - Vereenvoudigd|0804|CHS|  
|Chinees (Traditioneel, Taiwan)|0404|CHT|  
|Tsjechisch|0405|CSY|  
|Deens|0406|DAN|  
|Nederlands - Nederland|0413|NLD|  
|Fins|040b|FIN|  
|Frans|040c|FRA|  
|Duits|0407|DEU|  
|Grieks|0408|ELL|  
|Hongaars|040e|HUN|  
|Italiaans - Italië|0410|ITA|  
|Japans|0411|JPN|  
|Koreaans|0412|KOR|  
|Norwegian|0414|NOR|  
|Pools|0415|PLK|  
|Portugees (Brazilië)|0416|PTB|  
|Portugees (Portugal)|0816|PTG|  
|Russisch|0419|RUS|  
|Spaans – Spanje|0c0a|ESN|  
|Zweeds|041d|SVE|  
|Turks|041f|TRK|  


### <a name="mobile-device-client-languages"></a>Client talen voor mobiele apparaten  
Wanneer u ondersteuning voor talen voor mobiele apparaten toevoegt, worden alle ondersteunde client talen voor mobiele apparaten opgenomen. U kunt geen afzonderlijke taal pakketten selecteren voor ondersteuning van mobiele apparaten.  



## <a name="identify-installed-language-packs"></a>Geïnstalleerde taal pakketten identificeren  
Zoek naar de land instellingen-ID (LCID) van de geïnstalleerde taal pakketten in het REGI ster van de computer om de taal pakketten te identificeren die zijn geïnstalleerd op een computer waarop de Configuration Manager-client wordt uitgevoerd. Deze informatie is beschikbaar op het volgende registerpad:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

De hardware-inventaris aanpassen om deze informatie te verzamelen. Maak vervolgens een aangepast rapport om de taal details te bekijken. Zie [hardware-inventaris configureren](../../../clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over het verzamelen van aangepaste hardware-inventarisatie. Zie [rapporten maken](../../manage/operations-and-maintenance-for-reporting.md#create-reports)voor meer informatie.
