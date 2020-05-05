---
title: De map CD.Latest
titleSuffix: Configuration Manager
description: Meer informatie over het proces dat updates levert aan het product in de Configuration Manager-console.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720511"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>De CD. Meest recente map voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager heeft een proces voor het leveren van updates voor het product vanuit de Configuration Manager-console. Ter ondersteuning van deze nieuwe methode voor het bijwerken van Configuration Manager, wordt een nieuwe map gemaakt met de naam **cd. Meest recente**. Deze map bevat een kopie van de Configuration Manager-installatie bestanden voor de bijgewerkte versie van uw site.  

De CD. De meest recente map bevat een map met de naam **redist**, die de herdistribueerbare bestanden bevat die door Setup worden gedownload en gebruikt. Deze bestanden zijn afgestemd op de versie van de Configuration Manager-bestanden die te vinden zijn in de map CD.Latest. Wanneer u Setup uitvoert vanuit de map CD.Latest, dient u de bestanden te gebruiken die zijn afgestemd op die versie van Setup. U kunt direct instellen om nieuwe en huidige bestanden van micro soft te downloaden, of rechtstreeks instellen om de bestanden te gebruiken uit de map Redist die is opgenomen in de CD. Meest recente map.

Basislijn media bevatten geen **redist** -map. De site maakt geen redist-map tot u een update in de console installeert. In de tussen tijd gebruikt u de map Redist die u hebt gebruikt bij het installeren van sites vanaf de basislijn media.  

> [!TIP]  
> Zorg ervoor dat de herdistribueerbare bestanden die u gebruikt, actueel zijn. Als u nog niet recentelijk herdistribueerbare bestanden hebt gedownload, moet u de installatie van micro soft toestaan.   

In de volgende scenario's wordt de CD gemaakt of bijgewerkt. Meest recente map op een centrale beheer site of primaire site server:  

- Wanneer u een update of hotfix installeert vanuit de Configuration Manager-console, wordt de map gemaakt of bijgewerkt in de installatiemap van Configuration Manager.  

- Wanneer u de ingebouwde Configuration Manager back-uptaak uitvoert, maakt of werkt de site de map onder de aangewezen locatie van de back-upmap.  

- Wanneer u een nieuwe site installeert met behulp van basislijn media, maakt de site de CD. Meest recente map.


## <a name="supported-scenarios"></a>Ondersteunde scenario's

De bron bestanden van de CD. De meest recente map wordt ondersteund voor de volgende scenario's:  

### <a name="backup-and-recovery"></a>Back-ups maken en herstellen
Als u een site wilt herstellen, gebruikt u de bron bestanden vanaf een CD. De meest recente map die overeenkomt met uw site. Wanneer u een site back-up uitvoert met behulp van de ingebouwde site back-uptaak, de CD. De meest recente map is opgenomen als onderdeel van de back-up.

- Wanneer u een site opnieuw installeert als onderdeel van een siteherstel , installeert u de site vanuit de map CD.Latest in uw back-up. Met deze actie wordt de site geïnstalleerd met de bestands versies die overeenkomen met uw site back-up en site database.  

    - Als u geen toegang hebt tot de juiste CD. Meest recente versie van de map, de CD ophalen. Laatste map met de juiste bestands versie door een site te installeren in een test omgeving. Werk vervolgens die site bij zodat deze overeenkomt met de versie die u wilt herstellen.  

    - Als u niet de juiste CD hebt. De meest recente map en de inhoud beschikbaar zijn, kunt u een site niet herstellen. In dit geval moet u de site opnieuw installeren.  

- Wanneer u geen CD hebt. Meest recente map, maar wel een werkende onderliggende primaire site of centrale beheer site, kunt u die site gebruiken als referentie site voor een site herstel.  

### <a name="install-a-child-primary-site"></a>Een onderliggende primaire site installeren
Wanneer u een nieuwe onderliggende primaire site wilt installeren onder een centrale beheer site waarop een of meer console-updates zijn geïnstalleerd, gebruikt u Setup en de bron bestanden van de CD. Meest recente map van de centrale beheer site. Dit proces maakt gebruik van bron bestanden voor installatie die overeenkomen met de versie van de centrale beheer site. Zie [de installatie wizard gebruiken om sites te installeren](../deploy/install/use-the-setup-wizard-to-install-sites.md)voor meer informatie.  

### <a name="expand-a-stand-alone-primary-site"></a>Een zelfstandige primaire site uitbreiden
Wanneer u een zelfstandige primaire site uitbreidt door een nieuwe centrale beheer site te installeren, gebruikt u Setup en de bron bestanden van de CD. Meest recente map van de primaire site. Dit proces maakt gebruik van bron bestanden voor installatie die overeenkomen met de versie van de primaire site. Zie [een zelfstandige primaire site uitbreiden](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)voor meer informatie.

### <a name="install-a-secondary-site"></a>Een secundaire site installeren
<!-- SCCMDocs-pr issue #3164 -->
Als u een nieuwe secundaire site wilt installeren onder een primaire site waarop een of meer console-updates zijn geïnstalleerd, gebruikt u de bron bestanden van de CD. Meest recente map van de primaire site. 

Zie [een secundaire site installeren](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary)voor meer informatie. 


## <a name="unsupported-scenarios"></a>Niet-ondersteunde scenario's

De bijgewerkte CD. De meest recente bron bestanden worden niet ondersteund voor:  

- Installatie van een nieuwe site voor een nieuwe hiërarchie  
- Een upgrade uitvoeren van een micro soft System Center 2012 Configuration Manager-site naar Configuration Manager current branch
- Configuration Manager-clients installeren
- Configuration Manager-consoles installeren
