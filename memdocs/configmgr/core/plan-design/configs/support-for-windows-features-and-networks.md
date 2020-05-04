---
title: Ondersteuning voor Windows-onderdelen
titleSuffix: Configuration Manager
description: Meer informatie over de Windows-en netwerk functies die Configuration Manager ondersteunt.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7e8e65571a3902661176ca3840690c159faef416
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709619"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Ondersteuning voor Windows-onderdelen en-netwerken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel wordt Configuration Manager ondersteuning voor algemene Windows-en netwerk functies aangeduid.  

## <a name="branchcache"></a><a name="bkmk_branchcache"></a>BranchCache  

Gebruik Windows BranchCache met Configuration Manager wanneer u deze inschakelt op distributie punten en configureer clients voor gebruik in de gedistribueerde-cache modus.

Configureer de BranchCache-instellingen voor een implementatie type voor toepassingen, voor de implementatie van een pakket en voor taken reeksen. Vanaf versie 1802 is BranchCache standaard ingeschakeld.

Wanneer aan de vereisten voor BranchCache wordt voldaan, kan deze functie clients op externe locaties gebruiken om inhoud te verkrijgen van lokale clients die een huidige cache van de inhoud hebben.  

Wanneer de eerste client voor BranchCache-ondersteuning bijvoorbeeld inhoud aanvraagt van een distributie punt dat is geconfigureerd als een BranchCache-server, wordt de inhoud door de client gedownload en opgeslagen in de cache. Deze inhoud wordt vervolgens beschikbaar gesteld voor clients op hetzelfde subnet die deze inhoud hebben aangevraagd.

Deze clients slaan ook de inhoud op in de cache. Andere clients in hetzelfde subnet hoeven geen inhoud te downloaden van het distributie punt. De inhoud wordt gedistribueerd over meerdere clients voor toekomstige overdrachten.  

### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Vereisten voor de ondersteuning van BranchCache met Configuration Manager

#### <a name="configure-distribution-points"></a>Distributie punten configureren

Voeg de functie **Windows BranchCache** toe aan de site systeem server die is geconfigureerd als een distributie punt.

- Distributie punten op servers die zijn geconfigureerd voor ondersteuning van BranchCache, hebben geen aanvullende configuratie nodig.
- U kunt Windows BranchCache niet toevoegen aan een cloud-gebaseerd distributie punt. Distributie punten in de Cloud bieden ondersteuning voor het downloaden van inhoud door clients die zijn geconfigureerd voor Windows BranchCache.  

#### <a name="configure-clients"></a>Clients configureren

- De clients die BranchCache kunnen ondersteunen, moeten zijn geconfigureerd voor de modus gedistribueerde cache van BranchCache.  
- De besturingssysteem instelling voor BITS-client instellingen moet zijn ingeschakeld voor de ondersteuning van BranchCache.  

Zie [Configure clients for BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) in de Windows-documentatie voor meer informatie.

Alle Configuration Manager ondersteunde versies van Windows ondersteunen BranchCache standaard.

Zie [BranchCache voor Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) in de Windows Server-documentatie voor meer informatie.  

## <a name="computers-in-workgroups"></a><a name="bkmk_Workgroups"></a>Computers in werk groepen  

Configuration Manager biedt ondersteuning voor clients in werk groepen.  

- Configuration Manager ondersteunt het verplaatsen van een client van een werk groep naar een domein of van een domein naar een werk groep. Zie [Configuration Manager-clients installeren op computers in werk groepen](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)voor meer informatie.  

> [!NOTE]
> Hoewel clients in werk groepen worden ondersteund, moeten alle site systemen lid zijn van een ondersteund Active Directory domein.  

## <a name="data-deduplication"></a><a name="bkmmk_datadedup"></a>Gegevensontdubbeling

Configuration Manager ondersteunt het gebruik van gegevensontdubbeling met distributie punten in Windows Server 2012 of hoger.

> [!IMPORTANT]  
> Het volume dat als host fungeert voor pakket bron bestanden kan niet worden gemarkeerd voor gegevensontdubbeling. Deze beperking is omdat gegevensontdubbeling reparse-punten gebruikt. Configuration Manager biedt geen ondersteuning voor het gebruik van een inhouds bron locatie met bestanden die op reparsepunten zijn opgeslagen.  

Voor meer informatie raadpleegt u de volgende berichten:

- [Configuration Manager distributie punten en Windows Server 2012-gegevensontdubbeling](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-distribution-points-and-windows-server/ba-p/273385) op het Configuration Manager team blog

- [Overzicht van gegevensontdubbeling](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) in de Windows Server-documentatie

## <a name="directaccess"></a><a name="bkmk_DA"></a>-  

Configuration Manager ondersteunt de DirectAccess-functie voor communicatie tussen clients en site server systemen.  

- Wanneer aan alle vereisten voor DirectAccess is voldaan, kunnen Configuration Manager clients op Internet communiceren met hun toegewezen site alsof ze op het intranet zijn.  

- Voor door de server geïnitieerde acties, zoals beheer op afstand en Push-client installatie, moet op de initiërende computer IPv6 worden uitgevoerd. Dit protocol moet worden ondersteund op alle tussenliggende netwerk apparaten.  

Configuration Manager biedt geen ondersteuning voor de volgende functionaliteit ten opzichte van DirectAccess:  

- Besturingssysteemimplementatie

- Communicatie tussen Configuration Manager sites  

- Communicatie tussen Configuration Manager-site systeem servers binnen een site  

## <a name="dual-boot-computers"></a><a name="bkmk_dualboot"></a>Dual-boot computers  

Configuration Manager kunt niet meer dan één besturings systeem op één computer beheren. Als er meer dan één besturings systeem op een computer wordt beheerd, past u de detectie-en client installatie methoden van de site aan om ervoor te zorgen dat de Configuration Manager-client alleen wordt geïnstalleerd op het besturings systeem dat moet worden beheerd.  

## <a name="ipv6"></a><a name="bkmk_IPv6"></a>Ipconfiguration  

Naast Internet Protocol versie 4 (IPv4) ondersteunt Configuration Manager Internet Protocol versie 6 (IPv6), met de volgende uitzonde ringen:  

|Functie| Uitzondering op IPv6-ondersteuning|  
|--------------|-------------------------------|  
|Clouddistributiepunten|IPv4 is vereist voor de ondersteuning van Microsoft Azure en clouddistributiepunten.|  
|Cloudbeheergateway|IPv4 is vereist voor de ondersteuning van Microsoft Azure en de Cloud beheer gateway.|  
|Mobiele apparaten die zijn geregistreerd door Microsoft Intune en de micro soft-service connector|IPv4 is vereist voor de ondersteuning van mobiele apparaten die zijn Inge schreven door Microsoft Intune en de micro soft-service connector.|  
|Netwerkdetectie|IPv4 is vereist als u een DHCP-server configureert om in Netwerkdetectie te zoeken.|  
|Besturingssysteemimplementatie|In versie 1802 en eerder is IPv4 vereist voor de ondersteuning van de implementatie van besturings systemen.  </br> </br> Vanaf versie 1806 kunt u een PXE-Responder inschakelen op een distributie punt zonder Windows Deployment service. Deze nieuwe PXE-responder-service biedt ondersteuning voor IPv6. Andere aspecten van de implementatie functie van het besturings systeem, zoals het vastleggen of instellen van vaste IP-adressen tijdens de taken reeks, blijven IPv4 vereisen. |  
|Communicatie van de wake-up proxy|IPv4 is vereist voor de ondersteuning van de pakketten voor de wake-up proxy van clients.|  
|Windows CE|IPv4 is vereist voor de ondersteuning van de Configuration Manager-client op Windows CE apparaten.|  

## <a name="network-address-translation"></a><a name="bkmk_NAT"></a>Netwerkadresomzetting  

Netwerkadresomzetting (NAT) wordt niet ondersteund in Configuration Manager, tenzij de site ondersteuning biedt voor clients op internet en de client detecteert dat deze verbinding heeft met internet. Zie voor meer informatie over het op internet gebaseerde client beheer [plannen voor het beheren van clients op Internet](../../clients/manage/plan-internet-based-client-management.md).  

## <a name="specialized-storage-technology"></a><a name="bkmk_storage"></a>Gespecialiseerde opslag technologie  

Configuration Manager werkt met alle hardware die is gecertificeerd in de lijst met compatibele Windows-hardware voor de versie van het besturings systeem waarop het Configuration Manager-onderdeel is geïnstalleerd.

Voor Site Server functies is NTFS vereist, zodat Configuration Manager Directory-en bestands machtigingen kunt instellen. Configuration Manager ervan uit dat het eigendom van een logisch station volledig is. Site systemen die op afzonderlijke computers worden uitgevoerd, kunnen geen logische partitie op opslag technologie delen. Elke computer kan echter een afzonderlijke logische partitie gebruiken op dezelfde fysieke partitie van een gedeeld opslagapparaat.  

### <a name="support-considerations"></a>Ondersteunings overwegingen

- **Storage Area Network**: een Storage Area Network (San) wordt ondersteund wanneer een ondersteunde Windows-Server rechtstreeks wordt gekoppeld aan het volume dat wordt gehost door het San.  

- **Single Instance Storage**: Configuration Manager ondersteunt geen configuratie van mappen voor distributiepunt pakketten en hand tekeningen op een SIS-volume (Single Instance Storage).  

     Daarnaast wordt de cache van een Configuration Manager-client niet ondersteund op een SIS-volume.  

- **Verwissel bare schijf**: Configuration Manager biedt geen ondersteuning voor de installatie van Configuration Manager-site systemen of-clients op een verwisselbaar schijf station.  
