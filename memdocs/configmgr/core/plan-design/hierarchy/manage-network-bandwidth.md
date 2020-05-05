---
title: Netwerk bandbreedte voor inhoud beheren
titleSuffix: Configuration Manager
description: Planning, beperking en voor bereide inhoud configureren voor Configuration Manager.
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8ee7d00f3b5c98528d9999b83b07aa393b72e36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720588"
---
# <a name="manage-network-bandwidth-for-content"></a>Netwerk bandbreedte voor inhoud beheren
Om u te helpen bij het beheren van de netwerk bandbreedte die wordt gebruikt voor het inhouds beheerproces van Configuration Manager, kunt u ingebouwde besturings elementen gebruiken voor het plannen en beperken. U kunt ook voor bereide inhoud gebruiken. In de volgende secties worden deze scenario's gedetailleerd beschreven.

##  <a name="scheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Plannen en beperken  

 Wanneer u een pakket maakt, het bronpad voor de inhoud wijzigt of inhoud op het distributie punt bijwerkt, worden de bestanden gekopieerd van het bronpad naar de inhouds bibliotheek op de site server. Vervolgens wordt de inhoud van de inhouds bibliotheek op de site server gekopieerd naar de inhouds bibliotheek op de distributie punten. Wanneer inhouds bron bestanden worden bijgewerkt en de bron bestanden al zijn gedistribueerd, Configuration Manager haalt alleen de nieuwe of bijgewerkte bestanden op en verzendt deze vervolgens naar het distributie punt.

 U kunt plannings-en beperkings opties gebruiken voor site-naar-site-communicatie en voor communicatie tussen een site server en een extern distributie punt. Als de netwerk bandbreedte is beperkt zelfs nadat u de plannings-en beperkings opties hebt ingesteld, kunt u overwegen om de inhoud op het distributie punt voor te bereiden.  

 In Configuration Manager kunt u een planning instellen en beperkings instellingen opgeven op externe distributie punten die bepalen wanneer en hoe inhouds distributie wordt uitgevoerd. Elk extern distributie punt kan verschillende configuraties hebben die de netwerk bandbreedte beperkingen van de site server naar het externe distributie punt helpen aanpakken. De besturings elementen voor het plannen en beperken van het externe distributie punt zijn vergelijkbaar met de instellingen voor een standaard adres van de afzender. In dit geval worden de instellingen gebruikt door een nieuw onderdeel, ook wel package overdracht Manager genoemd.

 Package overdracht Manager distribueert inhoud van een site server, als een primaire site of secundaire site, naar een distributie punt dat op een site systeem is geïnstalleerd. De beperkings instellingen zijn opgegeven op het tabblad **frequentie limieten** en de plannings instellingen worden opgegeven op het tabblad **planning** voor een distributie punt dat zich niet op een site server bevindt. De tijd instellingen zijn gebaseerd op de tijd zone van de verzendende site, niet het distributie punt.  

> [!IMPORTANT]  
>  De tabbladen **frequentie limieten** en **planning** worden alleen weer gegeven in de eigenschappen voor distributie punten die niet op een site server zijn geïnstalleerd.  

Zie [distributie punten voor Configuration Manager installeren en configureren](../../servers/deploy/configure/install-and-configure-distribution-points.md)voor meer informatie.  

##  <a name="prestaged-content"></a><a name="BKMK_PrestagingContent"></a>Voor bereide inhoud  
 U kunt inhoud voorbereiden om de inhouds bestanden toe te voegen aan de inhouds bibliotheek op een site server of distributie punt voordat u de inhoud distribueert. Omdat de inhouds bestanden al in de inhouds bibliotheek staan, worden ze niet via het netwerk overgedragen wanneer u de inhoud distribueert. U kunt inhouds bestanden voor toepassingen en pakketten vooraf plaatsen.  

Selecteer in de Configuration Manager-console de inhoud die u wilt voorbereiden en gebruik vervolgens de **wizard voor bereid inhouds bestand maken**. Hiermee maakt u een gecomprimeerd, voor bereid inhouds bestand dat de bestanden en gekoppelde meta gegevens voor de inhoud bevat. Vervolgens kunt u de inhoud hand matig importeren op een site server of distributie punt. Houd rekening met de volgende punten:  

-   Wanneer u het voor bereide inhouds bestand op een site server importeert, worden de inhouds bestanden toegevoegd aan de inhouds bibliotheek op de site server en vervolgens geregistreerd in de site Server database.  

-   Wanneer u het voor bereide inhouds bestand op een distributie punt importeert, worden de inhouds bestanden toegevoegd aan de inhouds bibliotheek op het distributie punt. Er wordt een status bericht verzonden naar de site server die de site informeert dat de inhoud beschikbaar is op het distributie punt.  

U kunt eventueel het distributie punt als voor **bereid** configureren om de distributie van inhoud te helpen beheren. Wanneer u inhoud distribueert, kunt u kiezen of u het volgende wilt doen:  

-   De inhoud op het distributie punt altijd vooraf plaatsen.  

-   Bereid de oorspronkelijke inhoud voor het pakket voor, en gebruik vervolgens het standaard distributie proces voor inhoud wanneer er updates voor de inhoud zijn.  

-   Gebruik altijd het standaard distributie proces voor inhoud voor de inhoud in het pakket.  

###  <a name="determine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Bepalen of inhoud moet worden voor bereid  
 Denk na over het voorbereiden van inhoud voor toepassingen en pakketten in de volgende scenario's:  

-   **Voor het oplossen van het probleem met beperkte netwerk bandbreedte van de site server naar een distributie punt.** Als het plannen en beperken niet voldoende is om te voldoen aan de band breedte, kunt u overwegen om de inhoud van het distributie punt voor te bereiden. Elk distributie punt heeft de instelling **Dit distributie punt inschakelen voor voor bereide inhoud** die u kunt kiezen in de eigenschappen van het distributie punt. Wanneer u deze optie inschakelt, wordt het distributie punt geïdentificeerd als een voor bereid distributie punt, en kunt u kiezen hoe de inhoud per pakket moet worden beheerd.  

    De volgende instellingen zijn beschikbaar in de eigenschappen voor een toepassing, pakket, stuur programmapakket, opstart installatie kopie, installatie programma voor het besturings systeem en installatie kopie. Met deze instellingen kunt u kiezen hoe inhouds distributie wordt beheerd op externe distributie punten die zijn geïdentificeerd als voor bereid:  

    -   **Automatisch inhoud downloaden wanneer pakketten worden toegewezen aan distributie punten**: gebruik deze optie wanneer u kleinere pakketten hebt, en de plannings-en bandbreedte beperkings instellingen bieden voldoende controle voor inhouds distributie.  

    -   **Alleen inhouds wijzigingen downloaden naar het distributie punt**: gebruik deze optie wanneer u verwacht dat de inhoud in het pakket in de toekomst doorgaans kleiner is dan het oorspronkelijke pakket. U kunt bijvoorbeeld een toepassing voorbereiden zoals Microsoft Office, omdat de initiële pakket grootte groter is dan 700 MB en te groot is om over het netwerk te verzenden. Het bijwerken van inhoud naar dit pakket kan echter minder zijn dan 10 MB en kan worden gedistribueerd via het netwerk. Een ander voor beeld is mogelijk stuur programmapakketten, waarbij de oorspronkelijke grootte van het pakket groot is, maar incrementele Stuur Programma's kunnen klein zijn.  

    -   **De inhoud in dit pakket hand matig kopiëren naar het distributie punt**: gebruik deze optie wanneer u grote pakketten hebt, met inhoud zoals een besturings systeem, en u nooit het netwerk wilt gebruiken om de inhoud naar het distributie punt te distribueren. Wanneer u deze optie selecteert, moet u de inhoud op het distributie punt voorbereiden.  

    > [!IMPORTANT]  
    >  De voor gaande opties zijn van toepassing op elk pakket en worden alleen gebruikt wanneer een distributie punt wordt geïdentificeerd als voor bereid. Distributie punten die niet zijn geïdentificeerd als voor bereid, negeren deze instellingen. In dit geval wordt inhoud altijd via het netwerk gedistribueerd van de site server naar de distributie punten.  

-   **De inhouds bibliotheek op een site server herstellen.** Wanneer een site server uitvalt, wordt informatie over pakketten en toepassingen die is opgenomen in de inhouds bibliotheek, teruggezet naar de site database als onderdeel van het herstel proces, maar de inhouds bibliotheek bestanden worden niet teruggezet als onderdeel van het proces. Als u geen back-up van het bestands systeem hebt om de inhouds bibliotheek te herstellen, kunt u een voor bereid inhouds bestand maken op basis van een andere site die de pakketten en toepassingen bevat die u nodig hebt. Vervolgens kunt u het voor bereide inhouds bestand op de herstelde site server uitpakken. Zie [back-up en herstel voor Configuration Manager](../../servers/manage/backup-and-recovery.md)voor meer informatie over back-up en herstel van de site server.  
