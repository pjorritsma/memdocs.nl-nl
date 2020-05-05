---
title: Windows PE-Peer-Cache voorbereiden om WAN-verkeer te beperken
titleSuffix: Configuration Manager
description: De Windows PE-peer-cache werkt in de Windows PE om inhoud van een lokale peer op te halen en WAN-verkeer te minimaliseren wanneer er geen lokaal distributie punt is.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd622c1a54c1dd3cd3b5071cc62d1b6860a118e3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724039"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-configuration-manager"></a>Windows PE-peer-cache voorbereiden om WAN-verkeer in Configuration Manager te verminderen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u een nieuw besturings systeem implementeert in Configuration Manager, kunnen computers waarop de taken reeks wordt uitgevoerd, Windows PE-peer-cache gebruiken om inhoud te verkrijgen van een lokale peer (een peer-cache bron) in plaats van inhoud te downloaden vanaf een distributie punt. Dit helpt het Wide Area Network-verkeer (WAN) te beperken indien er sprake is van meerdere filialen terwijl er geen lokaal distributiepunt bestaat.  

 Windows PE-peer-cache is vergelijkbaar met [Windows BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache), maar werkt in de Windows Preinstallation Environment (Windows PE). De volgende termen worden gebruikt om de clients te beschrijven die Windows PE-Peer-Cache gebruiken:  

-   Een **peer-cacheclient** is een computer die is geconfigureerd voor het gebruik van Windows PE-Peer-Cache.  

-   Een **peer-cachebron** is een client die is geconfigureerd voor peer-cache en die inhoud beschikbaar stelt aan andere peer-cacheclients die deze inhoud opvragen.  

Gebruik de volgende secties om peer-cache te beheren.

##  <a name="objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a>Objecten die zijn opgeslagen in een peer-cache-bron  
 Een takenreeks die is geconfigureerd voor het gebruik van Windows PE-Peer-Cache kan de volgende inhoudobjecten ophalen tijdens het uitvoeren van Windows PE:  

- Installatiekopie van besturingssysteem  

- Stuurprogrammapakket  

- Pakketten en Program Ma's (als de client de taken reeks blijft uitvoeren in het volledige besturings systeem, haalt de client deze inhoud op van een peer-cache bron als de taken reeks oorspronkelijk is geconfigureerd voor peer-cache bij het uitvoeren in Windows PE.)  

- Aanvullende installatiekopieën  

  De volgende inhoudobjecten worden nooit overgedragen met behulp van Peer-Cache. Deze worden in plaats daarvan overgedragen via een distributiepunt of via Windows BranchCache als u Windows BranchCache hebt geconfigureerd in uw omgeving:  

- Toepassingen  

- Software-updates  

##  <a name="how-does--windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a>Hoe werkt Windows PE-peer-cache?  
 Stelt u zich een scenario voor met een filiaal dat geen distributiepunt heeft, maar wel enkele clients heeft waarvoor gebruik van Windows PE-Peer-Cache is ingeschakeld. U implementeert de takenreeks die is geconfigureerd om Peer-Cache te gebruiken op verschillende clients die zijn geconfigureerd om onderdeel te vormen van de Peer-Cache-bron. De eerste client die de takenreeks uitvoert, zendt een verzoek uit voor een peer met de inhoud. Deze peer wordt niet gevonden en de inhoud wordt daarom opgehaald van een distributiepunt via het WAN. De client installeert de nieuwe installatie kopie en slaat vervolgens de inhoud op in de Configuration Manager-client cache zodat deze kan worden gebruikt als peer-cache bron voor andere clients. Wanneer de volgende client de takenreeks uitvoert, wordt er via het subnet een aanvraag verstuurd voor een peer-cachebron. De eerste client reageert dan en maakt de inhoud in de cache beschikbaar.  

##  <a name="determine-what--clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a>Bepalen welke clients deel uitmaken van de Windows PE-peer-cache-bron  
 Als u wilt bepalen welke computers u moet selecteren als Windows PE-Peer-Cache-bron, zijn er verschillende dingen die u moet overwegen:  

-   De Windows PE-Peer-Cache-bron moet een desktopcomputer zijn die altijd is ingeschakeld en beschikbaar is voor Peer-Cache-clients.  

-   De Windows PE-Peer-Cache moet een clientcache hebben die groot genoeg is om de installatiekopieën op te slaan.  

##  <a name="requirements-for-a-client-to-use-a--windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a>Vereisten voor een client voor het gebruik van een Windows PE-peer-cache-bron  
 Clients waarop een Windows PE-Peer-Cache-bron moet worden gebruikt, moeten voldoen aan de volgende vereisten:  

-   De Configuration Manager-client moet kunnen communiceren via de volgende poorten op het netwerk:  

    -   Poort voor de eerste netwerkuitzending om een peer-cachebron te vinden. Dit is standaard UDP-poort 8004.  

    -   Poort voor het downloaden van inhoud via een peer-cache bron (HTTP en HTTPS). Dit is standaard TCP-poort 8003.  
    
        Zie [poorten die worden gebruikt voor verbindingen](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp)voor meer informatie.  

        > [!TIP]  
        >  Clients gebruiken HTTPS om inhoud te downloaden wanneer deze beschikbaar is. Hetzelfde poortnummer wordt echter voor HTTP of HTTPS gebruikt.  

-   [Configureer de Client Cache voor Configuration Manager-clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) op clients om ervoor te zorgen dat er genoeg ruimte is voor het bewaren van de installatiekopieën die u implementeert. Windows PE-Peer-Cache heeft geen invloed op de configuratie of het gedrag van de clientcache.  

-   De implementatieopties voor de takenreeksimplementatie moeten worden geconfigureerd als Inhoud lokaal downloaden wanneer deze nodig is door de takenreeks.  

##  <a name="configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a>Windows PE-peer-cache configureren  
 Met de volgende methoden kunt u een client inrichten met Peer-Cache-inhoud zodat deze kan dienen als Peer-Cache-bron:  

- Een peer-cacheclient die geen peer-cachebron kan vinden met de gewenste inhoud, downloadt de inhoud van een distributiepunt.  Als de client clientinstellingen ontvangt waardoor peer-cache wordt ingeschakeld en de takenreeks zodanig wordt geconfigureerd dat de inhoud in de cache wordt bewaard, wordt de client een peer-cachebron.  

- Een peer-cache-client kan inhoud ophalen van een andere peer-cache client (een peer-cache bron).  Omdat de client is geconfigureerd voor peer-cache, wordt de client een peer-cachebron wanneer deze een takenreeks uitvoert op basis waarvan de inhoud in de cache moet worden bewaard.  

- Een client voert een takenreeks uit die de optionele stap [Pakketinhoud downloaden](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)bevat. Deze wordt gebruikt om de relevante inhoud die is opgenomen in de Windows PE-Peer-Cache-takenreeks voor te bereiden. Wanneer u deze methode gebruikt:  

  -   De client hoeft de installatiekopie die wordt geïmplementeerd niet te installeren.  

  -   Naast de optie **Pakketinhoud downloaden** moet de takenreeks ook de optie **Configuration Manager-clientcache** gebruiken. U kunt deze optie gebruiken om de inhoud op te slaan in de cache van de client, zodat de client kan dienen als peer-cachebron voor andere peer-cacheclients.  

  Op basis van de volgende procedures kunt u Windows PE-Peer-Cache configureren op clients en takenreeksen configureren die ondersteuning bieden voor peer-cache.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>De Windows PE-Peer-Cache-broncomputers configureren  

1. Ga in de Configuration Manager-console naar **beheer** > **client instellingen**en maak een nieuwe aangepaste instellingen voor **client apparaten** of bewerk een bestaand instellingen object. U kunt dit ook configureren voor het object **Standaardclientinstellingen** .  

   > [!TIP]  
   >  Gebruik een object met aangepaste instellingen om te beheren welke clients deze configuratie ontvangen. Het kan bijvoorbeeld zijn dat u wilt voorkomen dat dit wordt geconfigureerd op de laptops van gebruikers die vaak onderweg zijn. Een uiterst mobiel systeem kan een slechte bron zijn voor het leveren van inhoud aan andere peer-cacheclients.  
   >   
   >  Onthoud dat ook als u deze instelling als onderdeel configureert van de **Standaardclientinstellingen**, de configuratie van toepassing op is alle clients in uw omgeving.  

2. Stel onder **client cache-instellingen**de **optie inschakelen Configuration Manager client in volledig besturings systeem in om inhoud te delen in** **Ja**.  

   -   Standaard is alleen HTTP ingeschakeld. Als u clients in staat wilt stellen om inhoud via HTTPS te downloaden, stelt u **HTTPS inschakelen voor clientpeercommunicatie** in op **Ja**.  

   -   De poort voor uitzendingen is standaard ingesteld op 8004 en de poort voor het downloaden van inhoud is ingesteld op 8003. U kunt beide wijzigen.  

3. Sla de clientinstellingen op en implementeer deze voor de clients die u selecteert als Peer-Cache-bron.  

   Wanneer een apparaat is geconfigureerd met dit instellingenobject, wordt het apparaat geconfigureerd als peer-cachebron. Deze instellingen moeten worden geïmplementeerd op mogelijke peer-cacheclients om de vereiste poorten en protocollen te configureren.  

###  <a name="configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a> Een takenreeks configureren voor Windows PE-Peer-Cache  
 Als u de takenreeks configureert, gebruikt u de volgende takenreeksvariabelen als Verzamelingsvariabelen voor de verzameling waarop de takenreeks wordt geïmplementeerd:  

- **SMSTSPeerDownload**  

   Waarde = TRUE  

   Hiermee kan de client Windows PE-Peer-Cache gebruiken.  

- **SMSTSPeerRequestPort**  

   Waarde: <poort nummer\>  

   Wanneer u niet de standaard poort gebruikt die is geconfigureerd in de client instellingen (8004), moet u deze variabele configureren met een aangepaste waarde van de netwerk poort die moet worden gebruikt voor de eerste uitzending.  

- **SMSTSPreserveContent**  

   Waarde: TRUE  

   Hiermee wordt de inhoud in de taken reeks gemarkeerd die na de implementatie moet worden bewaard in de Configuration Manager-client cache. Dit wijkt af van het gebruik van SMSTSPersisContent waarbij alleen de inhoud voor de duur van de taken reeks wordt behouden en de taken reeks cache wordt gebruikt, niet de Configuration Manager-client cache.  

  Zie [taken reeks variabelen](../understand/task-sequence-variables.md)voor meer informatie.  

###  <a name="validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a> Het succes van het gebruik van Windows PE-Peer-Cache valideren  
 Nadat u met Windows PE-peer-cache een takenreeks voor opstartmedia hebt geïmplementeerd en geïnstalleerd, kunt u controleren of het proces peer-cache heeft gebruikt door de **smsts.log** te bekijken op de client die de takenreeks heeft uitgevoerd.  

 Zoek in het logboek een vermelding die lijkt op het volgende, waarbij <*bron server naam*> de computer identificeert van waaruit de client de inhoud heeft verkregen. Deze computer moet een peer-cachebron zijn, en geen distributiepuntserver. Andere details zijn afhankelijk van uw lokale omgeving en configuraties.  

-   *<! [LOG [down loaded file from http://\><bron server naam: 8003/SCCM_BranchCache $/SS10000C/SCCM?/install.Wim to\\C: _SMSTaskSequence \packages\ss10000c\install.Wim] log]! ><time = "14:24:33.329 + 420" date = "06-26-2015" component = "ApplyOperatingSystem" context = "" type = "1" thread = "1256" file = "downloadcontent. cpp: 1626" >*  
