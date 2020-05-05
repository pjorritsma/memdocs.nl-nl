---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Meer informatie over nieuwe functies die beschikbaar zijn in de Configuration Manager Technical Preview versie 1803.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719041"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1803 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1803. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Technical Preview-site. 

Raadpleeg het artikel [Technical Preview](technical-preview.md) voordat u deze update installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Pull-distributie punten ondersteunen Cloud distributiepunten als bron  
<!--1321554-->
Veel klanten gebruiken [pull-distributie punten](../plan-design/hierarchy/use-a-pull-distribution-point.md) in externe of filialen, die inhoud van een bron distributiepunt downloaden via het WAN. Als uw externe kant oren een betere verbinding met internet hebben of als u de belasting van uw WAN-koppelingen wilt verkorten, kunt u nu een [Cloud distributiepunt](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) in Microsoft Azure als bron gebruiken. Wanneer u een bron toevoegt op het **pull-distributie punt** tabblad van de eigenschappen van het distributie punt, wordt een Cloud distributiepunt in de site nu vermeld als beschikbaar distributie punt. Het gedrag van beide site systeem rollen blijft anders. 

### <a name="prerequisites"></a>Vereisten
- Het pull-distributie punt heeft Internet toegang nodig om te kunnen communiceren met Microsoft Azure.
- De inhoud moet worden gedistribueerd naar het bron-Cloud distributiepunt.

> [!Note]  
> Met deze functie worden kosten in rekening gebracht voor uw Azure-abonnement voor gegevens opslag en netwerk uitgaand verkeer. Zie de kosten voor het [gebruik van Cloud distributie](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost)voor meer informatie.



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Gedeeltelijke download ondersteuning in client-peer-cache om WAN-gebruik te verminderen
<!--1357346-->
Client-peer-cache bronnen kunnen nu inhoud in delen delen. Deze onderdelen minimaliseren de netwerk overdracht om WAN-gebruik te verminderen. Het beheer punt biedt gedetailleerdere tracking van de inhouds onderdelen. Er wordt geprobeerd om meer dan één down load van dezelfde inhoud per grens groep te verwijderen. 

### <a name="example-scenario"></a>Voorbeeldscenario
Contoso heeft één primaire site met twee grens groepen: hoofd kantoor (hoofd kantoor) en filialen. Er is een terugval relatie van 30 minuten tussen de grens groepen. Het beheer punt en distributie punt voor de site bevinden zich alleen in de hoofd kantoor-grens. De vestiging van het filiaal heeft geen lokaal distributie punt. Twee van de vier clients in het filiaal worden geconfigureerd als peer-cache bronnen. 

![Diagram van de netwerk configuratie zoals beschreven in het voorbeeld scenario](media/1357346-peer-cache-source-parts.png)

1. U richt een implementatie met inhoud op alle vier clients in het filiaal. U distribueert de inhoud alleen naar het distributie punt.
2. Client3 en Client4 hebben geen lokale bron voor de implementatie. Het beheer punt zorgt ervoor dat clients 30 minuten wachten voordat ze terugvallen op de externe grens groep.
3. CLIENT1 (PCS1) is de eerste peer-cache bron voor het vernieuwen van het beleid met het beheer punt. Omdat deze client als bron van een peer-cache is ingeschakeld, geeft het beheer punt aan dat het downloaden van onderdeel A onmiddellijk vanaf het distributie punt wordt gestart.  
4. Wanneer CLIENT2 (PCS2) contact opneemt met het beheer punt, wordt door het beheer punt automatisch het downloaden van deel B vanaf het distributie punt in de huidige staat uitgevoerd, maar nog niet voltooid.
5. PCS1 voltooit deel A en brengt onmiddellijk op de hoogte van het beheer punt. Als deel B wordt al uitgevoerd, maar nog niet is voltooid, geeft het beheer punt aan dat deel C vanaf het distributie punt moet worden gedownload.
6. PCS2 voltooit deel B en waarschuwt onmiddellijk het beheer punt. Het beheer punt geeft aan dat het downloaden van deel D van het distributie punt begint. 
7. PCS1 voltooit het downloaden van deel C en brengt onmiddellijk op de hoogte van het beheer punt. Het beheer punt informeert dat er geen onderdelen meer beschikbaar zijn vanaf het externe distributie punt. Het beheer punt geeft aan dat deel B kan worden gedownload van de lokale peer, PCS2.
8. Dit proces wordt voortgezet totdat beide client peer-cache bronnen alle onderdelen van elkaar hebben. Het beheer punt prioriteert onderdelen van het externe distributie punt voordat de peer-cache bronnen worden geïnstrueerd om onderdelen van lokale peers te downloaden. 
9. Client3 is de eerste keer dat u het beleid vernieuwt nadat de terugval periode van 30 minuten is verlopen. Er wordt nu weer gecontroleerd op het beheer punt, waarmee de client van nieuwe lokale bronnen wordt geïnformeerd. In plaats van de inhoud volledig te downloaden van het distributie punt via het WAN, wordt de inhoud volledig gedownload van een van de peer-cache bronnen van de client. Clients geven prioriteit aan lokale peer bronnen. 

> [!Note]  
> Als het aantal cache bronnen van de client peer groter is dan het aantal inhouds onderdelen, geeft het beheer punt de extra peer-cache bronnen de opdracht om te wachten op terugval, zoals een normale client. 


### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

1. Stel [grens groepen](../servers/deploy/configure/boundary-groups.md) en [peer-cache bronnen](../plan-design/hierarchy/client-peer-cache.md) per normaal in.
2. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer **sites**. Klik op **hiërarchie-instellingen** in het lint. 
3. Schakel op het tabblad **Algemeen** de optie voor het **configureren van cache bronnen voor client peer in om inhoud in delen te verdelen**. 
4. Maak een vereiste implementatie met inhoud.  

   > [!Note]  
   > Deze functie werkt alleen wanneer de client inhoud op de achtergrond downloadt, bijvoorbeeld met een vereiste implementatie. Down loads op aanvraag, bijvoorbeeld wanneer de gebruiker een beschik bare implementatie in Software Center installeert, gedraagt zich op de gebruikelijke manier.  

1. Als u wilt zien hoe het downloaden van inhoud in delen wordt verwerkt, bekijkt u de **ContentTransferManager. log** op de client peer-cache bron en het **MP_Location. log** op het beheer punt.  
 



## <a name="maintenance-windows-in-software-center"></a>Onderhouds Vensters in Software Center
<!--1358131-->
In Software Center wordt nu het volgende geplande onderhouds venster weer gegeven. Schakel op het tabblad installatie status de optie weer gave van alles naar gepland. Het tijds bereik en de lijst met geplande implementaties worden weer gegeven. De lijst is leeg als er geen toekomstige onderhouds Vensters zijn. 

![Software Center met de lijst met aanstaande implementaties op het tabblad installatie status](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Aangepast tabblad voor webpagina in Software Center
<!--1358132-->
U kunt nu een aangepast tabblad maken om een webpagina te openen in Software Center. Met deze functie kunt u inhoud op een consistente, betrouw bare manier weer geven aan uw eind gebruikers. De volgende lijst bevat enkele voor beelden:
- Neem contact op met IT: informatie over hoe u contact kunt opnemen met de IT-afdeling van uw organisatie
- IT-ondersteunings centrum: IT-self-service acties, zoals zoeken in een Knowledge Base of het openen van een ondersteunings ticket.
- Documentatie voor eind gebruikers: artikelen voor gebruikers in uw organisatie op diverse IT-onderwerpen, zoals toepassingen gebruiken of een upgrade uitvoeren naar Windows 10.


### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

1. Open in de Configuration Manager-console, werk ruimte **beheer** , knoop punt **client instellingen** het standaard beleid voor **client instellingen** .
2. Selecteer de **Software Center** -groep.
3. Klik voor **Software Center-instellingen**op **aanpassen**.
4. Ga naar het tabblad **Tabs** .
5. Schakel de optie in om **een aangepast tabblad voor Software Center**op te geven.
    1. Geef een naam op in het tekst veld **naam van tabblad** . Deze naam wordt weer gegeven aan de gebruiker in Software Center.
    2. Voer een geldige URL in het tekst veld voor de **inhouds-URL** in. Deze URL is de inhoud die door Software Center wordt weer gegeven wanneer gebruikers op dit tabblad klikken.

> [!Tip]  
> Software Center maakt gebruik van Internet Explorer-onderdelen voor het weer geven van de webpagina.

## <a name="enable-third-party-software-update-support-on-clients"></a>Ondersteuning van software-updates van derden op clients inschakelen

U kunt nu de configuratie inschakelen van Configuration Manager-clients voor software-updates van derden. Wanneer u **software-updates van derden inschakelt** voor de eigenschappen van het sup-onderdeel, downloadt het sup het handtekening certificaat dat door WSUS wordt gebruikt voor updates van derden. <!--1357605-->

Als u **software-updates** van derden inschakelen selecteert in client instellingen, gebeurt het volgende: 
- Op de client wordt het beleid ingesteld op ' ondertekende updates toestaan voor een micro soft-Update service-locatie op een intranet ' 
- Installeert het handtekening certificaat in het archief met vertrouwde uitgevers op de client. 

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

1. Ga op de bovenste site in de Configuration Manager-hiërarchie naar het knoop punt **beheer** , vouw **site configuratie**uit en klik vervolgens op **sites**.
2. Klik met de rechter muisknop op de bovenste site server en selecteer **site onderdelen configureren** en vervolgens **Software-update punt**.
3. Klik op het tabblad **updates** van derden en Schakel **software-updates**van derden inschakelen in.
4. Open **client instellingen** en ga naar de instellingen voor **software-updates**.
5. Zorg ervoor dat **software-updates** van derden inschakelen is ingesteld op **Ja**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Kopiëren/plakken van activum gegevens in controle weergaven inschakelen
Als gevolg van de feedback van uw [gebruiker](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det) kunt u nu de functionaliteit voor kopiëren/plakken inschakelen in het deel venster activum gegevens in de weer gaven implementatie en distributie status controle.  <!--1357552-->

## <a name="scap-extensions"></a>SCAP-extensies
De voorlopige versie van SCAP-uitbrei dingen is beschikbaar in de map cd. latest onder SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Deze voorlopige versie van de SCAP-uitbrei dingen kan worden geïnstalleerd op alle momenteel ondersteunde versies van Configuration Manager current branch en LTSB 1606.



## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    
