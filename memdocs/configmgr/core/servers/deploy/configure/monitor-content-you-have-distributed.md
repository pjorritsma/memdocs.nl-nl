---
title: Inhoud controleren
titleSuffix: Configuration Manager
description: Meer informatie over het bewaken van gedistribueerde inhoud met behulp van de Configuration Manager-console.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fafcbffe3231af78ae3a079061accc9f112a181c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110012"
---
# <a name="monitor-content-you-distribute-with-configuration-manager"></a>Bewaak inhoud die u distribueert met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de Configuration Manager-console voor het bewaken van gedistribueerde inhoud, waaronder:  

- De status voor alle pakket typen voor de bijbehorende distributie punten.  
- De status van de inhouds validatie voor de inhoud in een pakket.  
- De status van de inhoud die is toegewezen aan een specifieke distributiepunten groep.  
- De status van de inhoud die is toegewezen aan een distributie punt.  
- De status van optionele functies voor elk distributie punt (inhouds validatie, PXE en multi cast).  

> [!NOTE]  
> Configuration Manager bewaakt alleen de inhoud op een distributie punt in de inhouds bibliotheek. Inhoud die op het distributie punt is opgeslagen, wordt niet bewaakt in pakket-of aangepaste shares.  

## <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Controle van de status van inhoud

Het knooppunt **Status van inhoud** in de werkruimte **Controle** biedt informatie over inhoudspakketten. Bekijk in de Configuration Manager-console informatie zoals:  

- Pakket naam, type en ID
- Naar hoeveel distributie punten een pakket is verzonden
- Compatibiliteits frequentie
- Wanneer het pakket is gemaakt
- Bron versie

U vindt hier ook gedetailleerde informatie over de status van alle pakketten, waaronder:  

- Distributie status
- Het aantal fouten
- Distributies in behandeling  
- Het aantal installaties

U kunt ook distributies beheren die worden uitgevoerd naar een distributie punt of die de inhoud niet kan distribueren naar een distributie punt:  

- De optie om inhoud te annuleren of te distribueren is beschikbaar wanneer u het implementatie status bericht van een distributie taak weergeeft naar een distributie punt in het deel venster **activum gegevens** . Dit deel venster vindt u op het tabblad **in uitvoering** of het tabblad **fout** van het knoop punt **inhouds status** .  
- Daarnaast geeft de taak Details het percentage van de taak weer dat is voltooid wanneer u de details van een taak op het tabblad wordt **uitgevoerd** bekijkt. De taak details geven ook het aantal nieuwe pogingen voor een taak weer. Wanneer u de details van een taak op het tabblad **fout** bekijkt, wordt weer gegeven hoe lang het duurt voordat de volgende poging doet.  

Wanneer u een implementatie annuleert die nog niet is voltooid, wordt de distributie taak voor het overdragen van de inhoud gestopt:  

- De status van de implementatie wordt vervolgens bijgewerkt om aan te geven dat de distributie is mislukt en dat deze is geannuleerd door een gebruikers actie.  
- Deze nieuwe status wordt weer gegeven op het tabblad **fout** .  

> [!NOTE]  
> Wanneer een implementatie bijna is voltooid, is het mogelijk dat de actie annuleren die distributie niet kan worden uitgevoerd voordat de distributie naar het distributie punt is voltooid. Als dit gebeurt, wordt de actie voor het annuleren van de implementatie genegeerd en wordt de status van de implementatie weer gegeven als geslaagd.  
>
> Hoewel u de optie kunt selecteren om een distributie te annuleren naar een distributie punt dat zich op een site server bevindt, heeft dit geen effect. Dit gedrag is omdat de site server en het distributie punt op een site server dezelfde single instance Content Store delen. Er is geen werkelijke distributie taak om te annuleren.  

Wanneer u inhoud die eerder niet naar een distributie punt is overgedragen opnieuw distribueert, begint Configuration Manager onmiddellijk met het opnieuw implementeren van die inhoud naar het distributie punt. Configuration Manager werkt de status van de implementatie bij om de huidige status van die herimplementatie weer te geven.  

### <a name="tasks-to-monitor-content"></a>Taken voor het bewaken van inhoud

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **distributie status**uit en selecteer vervolgens het knoop punt **inhouds status** . Dit knoop punt geeft de pakketten weer.  

2. Selecteer het pakket dat u wilt beheren.  

3. Klik op het tabblad **Start** van het lint in de groep **inhoud** op **status weer geven**. De-console bevat gedetailleerde status informatie voor het pakket.

Ga door naar een van de volgende secties voor aanvullende acties:

#### <a name="cancel-a-distribution-that-remains-in-progress"></a>Een distributie annuleren die nog wordt uitgevoerd  

1. Ga naar het tabblad wordt **uitgevoerd** .

2. Klik in het deel venster **activum gegevens** met de rechter muisknop op de vermelding voor de distributie die u wilt annuleren en selecteer **Annuleren**.  

3. Selecteer **Ja** om de actie te bevestigen en de distributie taak te annuleren tot dat distributie punt.  

#### <a name="redistribute-content-that-failed-to-distribute"></a>Inhoud die niet kan worden gedistribueerd, opnieuw distribueren  

1. Schakel over naar het tabblad **fout** .

2. Klik in het deel venster **activum gegevens** met de rechter muisknop op de vermelding voor de distributie die u opnieuw wilt distribueren en selecteer opnieuw **distribueren**.  

3. Selecteer **Ja** om de actie te bevestigen en het opnieuw distribueren van dat distributie punt te starten.  


## <a name="distribution-point-group-status"></a>Status van distributiepuntengroep

Het knooppunt **Status van distributiepuntengroep** in de werkruimte **Controle** biedt informatie over distributiepuntengroepen. U kunt informatie als volgt bekijken:  

- De naam, beschrijving en status van de distributiepunten groep
- Hoeveel distributie punten zijn leden van de distributiepunten groep
- Hoeveel pakketten zijn toegewezen aan de groep
- Het compatibiliteits aantal

U kunt ook de volgende gedetailleerde status informatie bekijken:  

- Fouten voor de distributiepunten groep  
- Hoeveel distributies worden uitgevoerd
- Hoeveel er is gedistribueerd  

### <a name="monitor-distribution-point-group-status"></a>De groeps status van distributie punten bewaken  

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **distributie status**uit en selecteer vervolgens het knoop punt **status van distributiepunten groep** . De distributiepunten groepen worden weer gegeven.  

2. Selecteer de distributiepunten groep waarvoor u gedetailleerde status informatie wilt.  

3. Op het tabblad **Start** van het lint selecteert u **status weer geven**. Er wordt gedetailleerde status informatie voor de distributiepunten groep weer gegeven.  


## <a name="distribution-point-configuration-status"></a> Configuratiestatus van distributiepunt

Het knooppunt **Configuratiestatus van distributiepunt** in de werkruimte **Controle** biedt informatie over de distributiepuntengroep. U kunt controleren welke kenmerken voor het distributie punt zijn ingeschakeld, zoals PXE, multi cast en inhouds validatie. Controleer ook de distributie status van het distributie punt.

> [!WARNING]  
> De configuratie status van het distributie punt is relatief ten opzichte van de afgelopen 24 uur. Als het distributie punt een fout heeft en herstelt, kan de fout status Maxi maal 24 uur na het herstellen van het distributie punt worden weer gegeven.  

### <a name="monitor-distribution-point-configuration-status"></a>Configuratie status van distributie punt bewaken  

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **distributie status**uit en selecteer het knoop punt **configuratie status van distributie punt** .  

2. Selecteer een distributie punt.  

3. Schakel in het resultaten venster over naar het tabblad **Details** . De status informatie voor het distributie punt wordt weer gegeven.  


## <a name="client-data-sources-dashboard"></a>Dash board client gegevens bronnen

Gebruik het dash board **client gegevens bronnen** om beter te begrijpen waar clients inhoud in uw omgeving ophalen. Het dash board begint met het weer geven van gegevens nadat clients inhoud hebben gedownload en deze gegevens weer rapporteren aan de site. Dit proces kan Maxi maal 24 uur duren.

> [!Note]  
> Configuration Manager schakelt deze optionele functie standaard niet in. U moet de functie **client peer cache** inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../manage/install-in-console-updates.md#bkmk_options).  

Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **distributie status**uit en selecteer het knoop punt **client gegevens bronnen** . Selecteer een tijds periode die op het dash board moet worden toegepast. Selecteer vervolgens de grens groep waarvoor u informatie wilt weer geven. U kunt de muis aanwijzer over tegels bewegen om meer informatie over de verschillende inhoud of beleids bronnen weer te geven.

Gebruik ook het rapport **gegevens bronnen-samen vatting**van de client om een samen vatting van de client gegevens bronnen voor elke grens groep weer te geven.

### <a name="dashboard-tiles"></a>Update van dashboardtegels

Het dash board bevat de volgende tegels:  

#### <a name="client-content-sources"></a>Bronnen van client inhoud

Hiermee worden de bronnen weer gegeven waarvan clients inhoud ontvangen:

- Distributiepunt
- [Cloud distributiepunt](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)
- [BranchCache](../../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache)
- [Peer-cache](../../../plan-design/hierarchy/client-peer-cache.md)
- [Delivery Optimization](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization) (vanaf versie 1906)<sup>[Opmerking 1](#bkmk_note1)</sup>
- Microsoft Update: apparaten melden deze bron wanneer de Configuration Manager client software-updates downloadt van micro soft-Cloud Services. Deze services omvatten Microsoft Update en Microsoft 365 apps voor bedrijven.

![Tegel client-inhouds bronnen op het dash board](media/3555759-do-source.png)

<a name="bkmk_note1"></a>

> [!Note]  
> Vanaf versie 1906<!--3555759-->kunt u de volgende acties uitvoeren om de leverings optimalisatie op dit dash board op te treffen:
>
> - De client instelling configureren, de **installatie van snelle updates inschakelen op clients** in de software-update groep
>
> - Windows 10 Express-updates implementeren
>
> Zie voor meer informatie [bestanden voor snelle installatie beheren voor Windows 10-updates](../../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

#### <a name="distribution-points"></a>Distributiepunten

Geeft het aantal distributie punten weer die deel uitmaken van de geselecteerde grens groep.

#### <a name="clients-that-used-a-distribution-point"></a>Clients waarvoor een distributie punt is gebruikt

Van het aantal clients dat zich in de geselecteerde grens groep bevindt, wordt in deze tegel aangegeven hoeveel er een distributie punt is gebruikt om inhoud op te halen.

#### <a name="peer-cache-sources"></a>Peer-cache bronnen

Voor de geselecteerde grens groep ziet u in deze tegel hoeveel peer-cache bronnen Download geschiedenis hebben gerapporteerd.

#### <a name="clients-that-used-a-peer"></a>Clients waarvoor een peer is gebruikt

Van het aantal clients dat zich in de geselecteerde grens groep bevindt, wordt in deze tegel aangegeven hoeveel er een peer-cache bron is gebruikt om inhoud op te halen.

#### <a name="top-distributed-content"></a>Beste gedistribueerde inhoud

De meest gedistribueerde pakketten per bron type
