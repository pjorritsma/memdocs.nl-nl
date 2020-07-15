---
title: De grondbeginselen van inhoudsbeheer
titleSuffix: Configuration Manager
description: Gebruik hulpprogram ma's en opties in Configuration Manager voor het beheren van de inhoud die u implementeert.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8f29ed1e3201da139daeaa1fadca739ff44dc8e
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384941"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Basis concepten voor inhouds beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager ondersteunt een robuust systeem van hulpprogram ma's en opties voor het beheren van software-inhoud. Software-implementaties, zoals toepassingen, pakketten, software-updates en implementaties van besturings systemen, hebben inhoud nodig. Configuration Manager slaat de inhoud op op zowel site servers als distributie punten. Deze inhoud vereist een grote hoeveelheid netwerk bandbreedte wanneer deze wordt overgedragen tussen locaties. Als u de infra structuur voor inhouds beheer effectief wilt plannen en gebruiken, moet u eerst de beschik bare opties en configuraties begrijpen. Bedenk vervolgens hoe u deze kunt gebruiken om uw netwerk omgeving en vereisten voor inhouds implementatie optimaal aan te passen.  

> [!TIP]  
> Zie informatie over de [distributie van inhoud en problemen oplossen in micro soft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm)voor meer informatie over het proces van inhouds distributie en het vinden van problemen bij het vaststellen en oplossen van algemene oplossingen voor inhouds distributie.

De volgende secties zijn belang rijke concepten voor inhouds beheer. Wanneer een concept aanvullende of complexe informatie vereist, worden er koppelingen naar de informatie weergegeven.


## <a name="accounts-used-for-content-management"></a>Accounts die worden gebruikt voor inhoudsbeheer

De volgende accounts kunnen worden gebruikt met inhoudsbeheer:  

### <a name="network-access-account"></a>Netwerktoegangsaccount

Wordt gebruikt door clients om verbinding te maken met een distributie punt en om toegang te krijgen tot inhoud. Standaard wordt het computer account eerst geprobeerd.  

Dit account wordt ook gebruikt door pull-distributie punten voor het downloaden van inhoud van een bron distributiepunt in een extern forest.  

Vanaf versie 1806 is voor sommige scenario's geen netwerk toegangs account meer nodig. U kunt de site inschakelen voor het gebruik van verbeterde HTTP met Azure Active Directory-verificatie.<!--1358228-->

Zie [netwerk toegangs account](accounts.md#network-access-account)voor meer informatie.

### <a name="package-access-account"></a>Pakket toegangs account

Configuration Manager verleent standaard toegang tot inhoud op een distributie punt naar de algemene toegangs accounts gebruikers en beheerders. U kunt echter aanvullende machtigingen configureren om de toegang te beperken.

Zie [pakket toegangs account](accounts.md#package-access-account)voor meer informatie.


## <a name="bandwidth-throttling-and-scheduling"></a>Bandbreedtebeperking en planning

Bandbreedtebeperking en planning zijn opties waarmee u kunt bepalen wanneer inhoud van een siteserver naar distributiepunten wordt gedistribueerd. Deze mogelijkheden zijn vergelijkbaar met, maar niet direct gerelateerd aan bandbreedte controles voor site-naar-site-replicatie op basis van een bestand.  

Zie [netwerk bandbreedte beheren](manage-network-bandwidth.md)voor meer informatie.


## <a name="binary-differential-replication"></a>Binaire differentiële replicatie

Configuration Manager gebruikt Binary Differential Replication (BDR) om inhoud bij te werken die u eerder hebt gedistribueerd naar andere sites of naar externe distributie punten. Installeer de functie voor **externe differentiële compressie** op distributie punten om de BDR van het bandbreedte gebruik te ondersteunen. Zie [vereisten voor distributie punten](../configs/site-and-site-system-prerequisites.md#bkmk_2012dppreq)voor meer informatie.

BDR minimaliseert de netwerk bandbreedte die wordt gebruikt om updates te verzenden voor gedistribueerde inhoud. Er wordt alleen de nieuwe of gewijzigde inhoud verzonden in plaats van de volledige set inhouds bron bestanden telkens wanneer u deze bestanden wijzigt.  

Wanneer BDR wordt gebruikt, identificeert Configuration Manager de wijzigingen die worden aangebracht aan de bron bestanden voor elke set inhoud die u eerder hebt gedistribueerd.  

- Wanneer bestanden in de bron inhoud wijzigen, maakt de site een nieuwe incrementele versie van de inhoud. Vervolgens worden alleen de gewijzigde bestanden gerepliceerd naar de doel sites en distributie punten. Een bestand wordt beschouwd als gewijzigd als u de naam ervan wijzigt of verplaatst, of als u de inhoud van het bestand hebt gewijzigd. Als u bijvoorbeeld één stuurprogrammabestand vervangt voor een stuur programmapakket dat u eerder naar verschillende sites hebt gedistribueerd, wordt alleen het gewijzigde stuurprogrammabestand gerepliceerd.  

- Configuration Manager ondersteunt Maxi maal vijf incrementele versies van een inhoudsset voordat de volledige inhoudsset opnieuw wordt verzonden. Na de vijfde update zorgt de volgende wijziging in de inhoudsset ervoor dat de site een nieuwe versie van de inhoudsset maakt. Configuration Manager verdeelt vervolgens de nieuwe versie van de inhoudset om de vorige set en alle incrementele versies te vervangen. Nadat de nieuwe inhoudsset is gedistribueerd, worden latere incrementele wijzigingen aan de bron bestanden opnieuw gerepliceerd door BDR.  

BDR wordt ondersteund tussen elke bovenliggende en onderliggende site in een hiërarchie. BDR wordt ondersteund binnen een site tussen de site server en de bijbehorende reguliere distributie punten. Pull-distributie punten en Cloud distributiepunten bieden echter geen ondersteuning voor BDR om inhoud over te dragen. Pull-distributie punten ondersteunen Deltas op bestands niveau, waarbij nieuwe bestanden worden overgedragen, maar geen blokken binnen een bestand.

Toepassingen gebruiken altijd binaire differentiële replicatie. BDR is optioneel voor pakketten en is standaard niet ingeschakeld. Als u BDR voor pakketten wilt gebruiken, schakelt u deze functie in voor elk pakket. Selecteer de optie **binary Differential Replication inschakelen** wanneer u een pakket maakt of bewerkt.


### <a name="bdr-or-delta-replication"></a>BDR of Delta replicatie

<!-- SCCMDocs#1209 -->
De volgende lijsten geven een overzicht van de verschillen tussen *binary Differential Replication* (BDR) en *Delta replicatie*.

#### <a name="summary-of-binary-differential-replication"></a>Samen vatting van Binary Differential Replication

- Configuration Manager van de term voor **externe differentiële compressie** van Windows
- Verschillen op *blok*niveau
- Altijd ingeschakeld voor apps
- Optioneel voor oudere pakketten
- Als er al een bestand op het distributie punt bestaat en er een wijziging is, gebruikt de site BDR om de wijziging op blok niveau te repliceren in plaats van het hele bestand. Dit gedrag geldt alleen wanneer u het object inschakelt voor het gebruik van BDR.<!-- SCCMDocs#2026 -->

#### <a name="summary-of-delta-replication"></a>Samen vatting van Delta replicatie

- Verschillen op *Bestands*niveau
- Standaard, niet configureerbaar
- Wanneer een pakket wordt gewijzigd, controleert de site op wijzigingen in de afzonderlijke bestanden in plaats van het hele pakket.
    - Als een bestand wordt gewijzigd, gebruikt u BDR om het werk uit te voeren
    - Als er een nieuw bestand is, kopieert u het nieuwe bestand


## <a name="peer-caching-technologies"></a>Cache technologieën op hetzelfde niveau

<!-- SCCMDocs#1044 -->

Configuration Manager ondersteunt diverse opties voor het beheren van inhoud tussen peer apparaten op hetzelfde netwerk:

- [BranchCache](#branchcache)
- [Leverings optimalisatie](#delivery-optimization)
- [Peer-cache Configuration Manager](#peer-cache)

Gebruik de volgende tabel om de belangrijkste functies van deze technologieën te vergelijken:

| Functie  | Peer- &nbsp; cache  | Leverings &nbsp; optimalisatie  | BranchCache  |
|---------|---------|---------|---------|
| Over subnetten | Ja | Ja | Nee |
| Bandbreedte beperken | Ja (BITS) | Ja (systeem eigen) | Ja (BITS) |
| Gedeeltelijke inhoud | Ja | Ja | Ja |
| Grootte van beheer cache op schijf | Ja | Ja | Ja |
| Detectie van peer-bronnen | Hand matig (client instelling) | Automatisch | Automatisch |
| Peer-detectie | Via beheer punt met behulp van grens groepen | Cloud service uitvoeren | Uitzenden |
| Rapportage | Dash board client gegevens bronnen | Dash board client gegevens bronnen | Dash board client gegevens bronnen |
| Besturings element voor WAN-gebruik | Grensgroepen | GroupID | Alleen subnet |
| Ondersteunde inhoud | Alle ConfigMgr-inhoud | Windows-updates, stuur Programma's, Store-apps | Alle ConfigMgr-inhoud |
| Beleidsbeheer | Instellingen voor client agent | Instellingen van client agent (gedeeltelijk) | Instellingen voor client agent |

### <a name="recommendations"></a>Aanbevelingen

- Modern beheer: als u al gebruikmaakt van moderne hulpprogram ma's, zoals intune, implementeert u leverings optimalisatie

- Configuration Manager en co-beheer: gebruik een combi natie van peer-cache en leverings optimalisatie. Gebruik peer-cache met on-premises distributie punten en gebruik Delivery Optimization voor Cloud scenario's.

- Bestaande BranchCache geïmplementeerd: gebruik alle drie de technologieën parallel. Gebruik peer cache en Delivery Optimization voor scenario's die niet worden ondersteund door BranchCache.


## <a name="branchcache"></a>BranchCache

[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) is een Windows-technologie. Clients die BranchCache ondersteunen en een implementatie hebben gedownload die u configureert voor BranchCache en vervolgens als inhouds bron voor andere BranchCache-clients fungeren.  

U hebt bijvoorbeeld een distributie punt waarop Windows Server 2012 of hoger wordt uitgevoerd en dat is geconfigureerd als een BranchCache-server. Wanneer de eerste client voor BranchCache-functionaliteit inhoud van deze server opvraagt, wordt die inhoud door de client gedownload en opgeslagen in de cache.  

- Deze client maakt de inhoud vervolgens beschikbaar voor aanvullende BranchCache-clients op hetzelfde subnet die ook de inhoud in de cache opslaan.  
- Andere clients in hetzelfde subnet hoeven geen inhoud te downloaden van het distributie punt.  
- De inhoud wordt gedistribueerd over meerdere clients voor toekomstige overdrachten.  

Zie [ondersteuning voor Windows BranchCache](../configs/support-for-windows-features-and-networks.md#bkmk_branchcache)voor meer informatie.

## <a name="delivery-optimization"></a>Delivery optimization

<!-- 1324696 -->
U gebruikt Configuration Manager grens groepen om de distributie van inhoud in uw bedrijfs netwerk en externe kant oren te definiëren en te reguleren. [Windows Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) is een op de cloud gebaseerde peer-to-peer-technologie voor het delen van inhoud tussen Windows 10-apparaten. Configureer Delivery Optimization om uw grens groepen te gebruiken bij het delen van inhoud tussen peers. Client instellingen Toep assen de grens groep-ID als de id van de leverings optimalisatie groep op de client. Wanneer de client communiceert met de Delivery Optimization-Cloud service, wordt deze id gebruikt om peers te zoeken met de inhoud. Zie [Delivery Optimization](../../clients/deploy/about-client-settings.md#delivery-optimization) client settings voor meer informatie.

Delivery Optimization is de aanbevolen technologie voor het optimaliseren van Windows 10 update levering van snelle installatie bestanden voor Windows 10-kwaliteits updates. Vanaf Configuration Manager versie 1910 is Internet toegang tot de Cloud Service Delivery Optimization een vereiste om gebruik te maken van de peer-to-peer-functionaliteit. Zie [Veelgestelde vragen over Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)voor meer informatie over de benodigde Internet-eind punten. Optimalisatie kan worden gebruikt voor alle Windows-updates. Zie [Windows 10 update delivery](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)voor meer informatie.


## <a name="microsoft-connected-cache"></a>Microsoft verbonden cache

<!--3555764-->
Vanaf versie 1906 kunt u een micro soft Connected cache-server op uw distributie punten installeren. Door deze inhoud on-premises in de cache te plaatsen, kunnen uw clients profiteren van de functie voor Delivery Optimization, maar kunt u WAN-koppelingen helpen beveiligen.

> [!NOTE]
> Vanaf versie 1910 wordt deze functie nu **micro soft Connected cache**genoemd. Het was voorheen bekend als Delivery Optimization in-Network cache.

Deze cache server fungeert als transparante cache op aanvraag voor inhoud die wordt gedownload door Delivery Optimization. Gebruik client instellingen om te controleren of deze server alleen wordt aangeboden aan de leden van de lokale Configuration Manager grens groep.

Deze cache is gescheiden van de inhoud van het distributie punt van Configuration Manager. Als u hetzelfde station kiest als de distributiepunt rol, wordt de inhoud afzonderlijk opgeslagen.

Zie voor meer informatie [micro soft Connected cache in Configuration Manager](microsoft-connected-cache.md).


## <a name="peer-cache"></a>Peer-cache

Met client-peer-cache kunt u de implementatie van inhoud naar clients op externe locaties beheren. Peer-cache is een ingebouwde Configuration Manager oplossing waarmee clients rechtstreeks vanuit hun lokale cache inhoud met andere clients kunnen delen.

Implementeer eerst de client instellingen waarmee peer-cache voor een verzameling wordt ingeschakeld. Leden van die verzameling kunnen fungeren als een peer-inhouds bron voor andere clients in dezelfde grens groep.

Vanaf versie 1806 kunnen peer-cache bronnen van de client inhoud delen in delen. Deze onderdelen minimaliseren de netwerk overdracht om WAN-gebruik te verminderen. Het beheer punt biedt gedetailleerdere tracking van de inhouds onderdelen. Er wordt geprobeerd om meer dan één down load van dezelfde inhoud per grens groep te verwijderen.<!--1357346-->

Zie [peer-cache voor Configuration Manager-clients](client-peer-cache.md)voor meer informatie.


## <a name="windows-pe-peer-cache"></a>Windows PE-peer-cache

Wanneer u een nieuw besturings systeem met Configuration Manager implementeert, kunnen computers waarop de taken reeks wordt uitgevoerd, Windows PE-peer-cache gebruiken. Ze downloaden inhoud van een peer-cache bron in plaats van vanaf een distributie punt. Dit gedrag zorgt ervoor dat WAN-verkeer in filialen wordt geminimaliseerd wanneer er geen lokaal distributie punt is.

Zie [Windows PE-peer-cache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)voor meer informatie.


## <a name="windows-ledbat"></a>Windows-LEDBAT

<!--1358112-->
Windows-lage extra vertraging achtergrond transport (LEDBAT) is een beheer functie voor netwerk congestie van Windows Server voor het beheren van achtergrond netwerk overdrachten. Voor distributie punten die worden uitgevoerd op ondersteunde versies van Windows Server, kunt u een optie inschakelen om netwerk verkeer aan te passen. Clients gebruiken alleen netwerk bandbreedte wanneer dit beschikbaar is.

Voor meer informatie over Windows LEDBAT in het algemeen raadpleegt u het nieuwe blog bericht over [transport voorschots](https://techcommunity.microsoft.com/t5/Networking-Blog/Announcing-Transport-Features-and-Performance-Advancements-in/ba-p/339726) .

Zie voor meer informatie over het gebruik van Windows LEDBAT met Configuration Manager-distributie punten de instelling voor het **aanpassen van de download snelheid voor het gebruik van de ongebruikte netwerk bandbreedte (Windows LEDBAT)** bij [het configureren van de algemene instellingen van een distributie punt](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-general).


## <a name="client-locations"></a>Clientlocaties

Op de volgende locaties wordt door clients inhoud opgehaald:  

- **Intranet** (on-premises):  

    - Distributie punten kunnen HTTP of HTTPs gebruiken.  

    - Gebruik alleen een Cloud distributiepunt voor terugval wanneer er geen on-premises distributie punten beschikbaar zijn.  

- **Internet**:  

    - Vereist Internet gerichte distributie punten voor het accepteren van HTTPS.  

    - Kan gebruikmaken van een Cloud distributiepunt of CMG (Cloud Management Gateway).  

        Vanaf versie 1806 kan een CMG ook inhoud aan clients aanbieden. Deze functionaliteit vermindert de vereiste certificaten en kosten van virtuele Azure-machines. Zie [een CMG wijzigen](../../clients/manage/cmg/setup-cloud-management-gateway.md)voor meer informatie.

- **Werk groep**:  

    - Vereist dat distributie punten HTTPS accepteren.  

    - Kan een Cloud distributiepunt of CMG gebruiken.  


## <a name="content-source-priority"></a>Prioriteit van inhouds bron

Wanneer een client inhoud nodig heeft, wordt er een aanvraag voor een inhouds locatie naar het beheer punt gemaakt. Het beheer punt retourneert een lijst met bron locaties die geldig zijn voor de aangevraagde inhoud. Deze lijst varieert, afhankelijk van het specifieke scenario, gebruikte technologieën, site ontwerp, grens groepen en implementatie-instellingen. Wanneer bijvoorbeeld een taken reeks wordt uitgevoerd, is de volledige Configuration Manager-client niet altijd actief, waardoor het gedrag kan verschillen.<!-- SCCMDocs#1960 -->

De volgende lijst bevat alle mogelijke inhouds bron locaties die de Configuration Manager-client kan gebruiken, in de volg orde waarin deze de prioriteit krijgt:  

1. Het distributie punt op dezelfde computer als de client
2. Een peer bron in hetzelfde subnet van het netwerk
3. Een distributie punt in hetzelfde subnet van het netwerk
4. Een peer bron in dezelfde grens groep
5. Een distributie punt in de huidige grens groep
6. Een distributie punt in een grens groep in een neighbor dat is geconfigureerd voor terugval
7. Een distributie punt in de standaard site grens groep
8. De Windows Update-Cloud service
9. Een Internet gericht distributie punt
10. Een Cloud distributiepunt in azure

> [!Note]  
> <!-- SCCMDocs#1607 -->Delivery Optimization is niet van toepassing op deze prioriteits aanduiding voor de bron. Deze lijst is de manier waarop de Configuration Manager-client inhoud vindt. De Windows Update-Agent downloadt inhoud voor de optimalisatie van de levering. Als de Windows Update-agent de inhoud niet kan vinden, gebruikt de Configuration Manager-client deze lijst om ernaar te zoeken.

## <a name="content-library"></a>Inhouds bibliotheek

De inhouds bibliotheek is de opslag voor één instantie van inhoud in Configuration Manager. Deze tape wisselaar vermindert de totale omvang van de inhoud die u distribueert.  

- Meer informatie over de [inhouds bibliotheek](the-content-library.md).
- Gebruik het [hulp programma voor opruimen van inhouds bibliotheken](content-library-cleanup-tool.md) om inhoud te verwijderen die niet meer aan een toepassing is gekoppeld.  


## <a name="distribution-points"></a>Distributiepunten

Configuration Manager maakt gebruik van distributie punten voor het opslaan van bestanden die vereist zijn voor het uitvoeren van software op client computers. Clients moeten toegang hebben tot ten minste één distributie punt waarvan ze de bestanden kunnen downloaden voor inhoud die u implementeert.  

Het basis distributie punt (niet-gespecialiseerd) wordt meestal een standaard distributiepunt genoemd. Er zijn twee varianten van het standaarddistributiepunt die speciale aandacht krijgen:  

- **Pull-distributie punt**: een variatie van een distributie punt waar het distributie punt inhoud ophaalt van een ander distributie punt (een bron distributiepunt). Dit proces is vergelijkbaar met de manier waarop clients inhoud van distributie punten downloaden. Pull-distributie punten kunnen u helpen netwerk bandbreedte knelpunten te voor komen die optreden wanneer de site server inhoud rechtstreeks naar elk distributie punt moet distribueren. [Een pull-distributie punt gebruiken](use-a-pull-distribution-point.md).

- **Cloud distributiepunt**: een variant van een distributie punt dat is geïnstalleerd op Microsoft Azure. [Meer informatie over het gebruik van een Cloud distributiepunt](use-a-cloud-based-distribution-point.md).  

Standaard distributie punten bieden ondersteuning voor diverse configuraties en functies:  

- Gebruik besturings elementen zoals **planningen** of **bandbreedte beperking** om deze overdracht te beheren.  

- Gebruik andere opties, waaronder voor **bereide inhoud**, en **pull-distributie punten** om het netwerk gebruik te minimaliseren en te beheren.  

- **BranchCache**, **peer-cache**en **leverings optimalisatie** zijn peer-to-peer-technologieën om de netwerk bandbreedte te beperken die wordt gebruikt wanneer u inhoud implementeert.  

- Er zijn verschillende configuraties voor besturingssysteem implementaties, zoals **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** en **[multi cast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**  

- Opties voor **mobiele apparaten**  
  
Cloud-en pull-distributie punten ondersteunen veel van deze configuraties, maar hebben beperkingen die specifiek zijn voor elk distributie punt.  


## <a name="distribution-point-groups"></a>Distributiepunten groepen

Distributiepunten groepen zijn logische groeperingen van distributie punten die de inhouds distributie kunnen vereenvoudigen.  

Zie [distributiepunt groepen beheren](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)voor meer informatie.


## <a name="distribution-point-priority"></a>Prioriteit van het distributiepunt

De prioriteitswaarde voor het distributiepunt is gebaseerd op het tijdsbestek dat de overdracht van eerdere implementaties naar dat distributiepunt in beslag nam.  

- Deze waarde wordt automatisch afgestemd. Deze is ingesteld op elk distributie punt, Configuration Manager zodat de inhoud sneller kan worden overgedragen naar meer distributie punten.  

- Wanneer u inhoud distribueert naar meerdere distributie punten tegelijkertijd of naar een distributiepunten groep, verzendt de site eerst de inhoud naar de server met de hoogste prioriteit. Vervolgens wordt dezelfde inhoud naar een distributie punt met een lagere prioriteit verzonden.  

- Met de prioriteit van het distributie punt wordt de distributie prioriteit voor pakketten niet vervangen. De pakket prioriteit blijft de beslissende factor van wanneer de site verschillende inhoud verzendt.  

U hebt bijvoorbeeld een pakket met een hoge pakket prioriteit. U distribueert het naar een server met een lage distributiepunt prioriteit. Dit pakket met hoge prioriteit wordt altijd overgedragen vóór een pakket met een lagere prioriteit. De pakket prioriteit is ook van toepassing als de site pakketten met een lagere prioriteit distribueert naar servers met hogere distributiepunt prioriteiten.

De hoge prioriteit van het pakket zorgt ervoor dat Configuration Manager die inhoud naar distributie punten distribueert voordat er pakketten met een lagere prioriteit worden verzonden.  

> [!NOTE]  
> Pull-distributiepunten maken ook gebruik van een prioriteitsconcept om de volgorde van de eigen brondistributiepunten vast te leggen.  
>
> - De distributiepunt prioriteit voor inhouds overdrachten naar de server verschilt van de prioriteit die pull-distributie punten gebruiken. Pull-distributie punten gebruiken hun prioriteit wanneer ze zoeken naar inhoud vanaf een bron distributiepunt.  
> - Zie [een pull-distributie punt gebruiken](use-a-pull-distribution-point.md)voor meer informatie.  


## <a name="fallback"></a>Terugval

Er zijn verschillende dingen gewijzigd met Configuration Manager huidige vertakking in de manier waarop clients een distributie punt vinden dat inhoud bevat, inclusief terugval.

Clients die geen inhoud kunnen vinden van een distributie punt dat is gekoppeld aan de huidige grens groep, vallen terug op het gebruik van inhouds bron locaties die zijn gekoppeld aan grens groepen in de buur. Een grens groep die moet worden gebruikt voor terugval moet een gedefinieerde relatie hebben met de huidige grens groep van de client. Deze relatie bevat een geconfigureerde tijd die moet worden door gegeven voordat een client die inhoud lokaal niet kan vinden, inhouds bronnen uit de grens groep van de naburige bevat als onderdeel van de zoek opdracht.

De concepten van voorkeurs distributiepunten worden niet meer gebruikt en de instellingen voor het **toestaan van terugval bron locaties voor inhoud** zijn niet langer beschikbaar of worden afgedwongen.

Zie [grens groepen](../../servers/deploy/configure/boundary-groups.md)voor meer informatie.


## <a name="network-bandwidth"></a>Netwerkbandbreedte

U kunt de volgende opties gebruiken om de hoeveelheid netwerk bandbreedte te beheren die wordt gebruikt wanneer u inhoud distribueert:  

- Voor **bereide inhoud**: inhoud overbrengen naar een distributie punt zonder de inhoud over het netwerk te distribueren.  

- **Planning en beperking**: configuraties waarmee u kunt bepalen wanneer en hoe inhoud wordt gedistribueerd naar distributie punten.  

Zie [netwerk bandbreedte beheren](manage-network-bandwidth.md)voor meer informatie.


## <a name="network-connection-speed-to-content-source"></a>Netwerkverbindingssnelheid naar de inhoudsbron

Er zijn verschillende dingen gewijzigd met Configuration Manager huidige vertakking in de manier waarop clients een distributie punt vinden dat inhoud bevat. Deze wijzigingen omvatten de netwerk snelheid naar een inhouds bron.

Netwerk verbindings snelheden die een distributie punt definiëren als **snel** of **langzaam** , worden niet meer gebruikt. In plaats daarvan wordt elk site systeem dat is gekoppeld aan een grens groep, op dezelfde manier behandeld.

Zie [grens groepen](../../servers/deploy/configure/boundary-groups.md)voor meer informatie.


## <a name="on-demand-content-distribution"></a>Inhoudsdistributie op aanvraag

Inhouds distributie op aanvraag is een optie voor afzonderlijke implementaties van toepassingen en pakketten. Met deze optie kan inhouds distributie op aanvraag naar voorkeurs servers worden gedistribueerd.  

- Als u deze instelling voor een implementatie wilt inschakelen, schakelt **u: de inhoud voor dit pakket distribueren naar voorkeurs distributiepunten**.  

- Wanneer u deze optie inschakelt voor een implementatie en een client die inhoud aanvraagt, maar de inhoud niet beschikbaar is op een van de voorkeurs distributiepunten van de client, distribueert Configuration Manager die inhoud automatisch naar de voorkeurs distributiepunten van de client.  

- Hoewel deze activeert Configuration Manager om de inhoud automatisch te distribueren naar de voorkeurs distributiepunten van die client, kan de client die inhoud mogelijk verkrijgen van andere distributie punten voordat de voorkeurs distributiepunten voor de client de implementatie ontvangen. Als dit probleem zich voordoet, wordt de inhoud op dat distributie punt weer gegeven voor gebruik door de volgende client die deze implementatie zoekt.  

Zie [grens groepen](../../servers/deploy/configure/boundary-groups.md)voor meer informatie.


## <a name="package-transfer-manager"></a>Package overdrachts Manager

Package Transfer Manager is het site Server onderdeel dat inhoud overdraagt naar distributie punten op andere computers.  

Zie [package overdracht Manager](package-transfer-manager.md)voor meer informatie.  


## <a name="prestage-content"></a>Inhoud vooraf plaatsen

Inhoud van voor bereiding is een proces waarbij inhoud naar een distributie punt wordt overgebracht zonder de inhoud over het netwerk te distribueren.  

Zie [netwerk bandbreedte beheren](manage-network-bandwidth.md)voor meer informatie.
