---
title: Siteonderdelen
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van site onderdelen om het gedrag van site systeem rollen en site status rapportage te wijzigen.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a3447e6ac71e9c5441a9e82034ee41eabda59374
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718327"
---
# <a name="site-components-for-configuration-manager"></a>Site onderdelen voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor elke Configuration Manager-site kunt u site onderdelen configureren om het gedrag van site systeem rollen en site status rapportage te wijzigen. Site onderdeel configuraties zijn van toepassing op een site en op elk exemplaar van een geschikte site systeemrol op de site.  

Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer een site. Klik in de groep **instellingen** van het lint op **site onderdelen configureren**. Selecteer één van de volgende opties:

- [Software distributie](#software-distribution)  
- [Software-updatepunt](#software-update-point) 
- [Implementatie van besturingssystemen](#operating-system-deployment)
- [Beheer punt](#management-point)  
- [Status rapportage](#status-reporting)  
- [E-mail melding](#email-notification)
- [Evaluatie lidmaatschap verzameling](#bkmk_colleval)


## <a name="about-site-components"></a>Siteonderdelen  

 De meeste opties voor de verschillende site onderdelen zijn zelf uitleg wanneer ze worden weer gegeven in de Configuration Manager-console. Met de volgende gegevens kunt u echter enkele van de complexere configuraties uitleggen of naar aanvullende inhoud verwijzen.  

> [!Note]  
> De beschik bare opties voor sommige onderdelen zijn afhankelijk van het feit of u de centrale beheer site, een primaire site of een secundaire site selecteert. Sommige onderdelen zijn alleen beschikbaar voor bepaalde typen sites.  



### <a name="software-distribution"></a>Softwaredistributie  

#### <a name="content-distribution-settings"></a>Instellingen voor inhouds distributie
Geef op het tabblad **Algemeen** de instellingen op waarmee wordt gewijzigd hoe de site server inhoud overdraagt naar de distributie punten. Als u de waarden voor instellingen voor gelijktijdige distributie verhoogt, kan de inhoudsdistributie meer netwerkbandbreedte gebruiken.  

#### <a name="pull-distribution-point"></a>Pull-distributie punt
Zie [een pull-distributie punt gebruiken](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)voor meer informatie.

#### <a name="network-access-account"></a>Netwerktoegangsaccount
Zie [netwerk toegangs account](../../../plan-design/hierarchy/accounts.md#network-access-account)voor meer informatie.  


### <a name="software-update-point"></a>Software-updatepunt  

Zie [Software-update punten installeren](../../../../sum/get-started/install-a-software-update-point.md)voor meer informatie.  


### <a name="operating-system-deployment"></a>Implementatie van besturingssystemen

Zie [het station opgeven voor offline-installatie kopieën van besturings systemen](../../../../osd/get-started/manage-operating-system-images.md#bkmk_servicing-drive)voor meer informatie.


### <a name="management-point"></a>Beheerpunt  

Stel op het tabblad **Algemeen** de site in om informatie over de bijbehorende beheer punten te publiceren naar Active Directory Domain Services.  

Configuration Manager-clients gebruiken beheer punten om services te zoeken, en om site-informatie te vinden, zoals lidmaatschap van grens groepen en opties voor het selecteren van PKI-certificaten. Clients gebruiken ook beheer punten om andere beheer punten in de site en distributie punten te vinden van waaruit software kan worden gedownload. Met beheer punten kunnen clients ook de site toewijzing volt ooien en client beleid downloaden en client gegevens uploaden.  

De veiligste methode voor clients om beheer punten te vinden is door deze te publiceren in Active Directory Domain Services. Voor deze service locatie methode moet het volgende waar zijn:

- Het schema wordt uitgebreid voor Configuration Manager.
- Er is een **System Management** -container met de juiste beveiligings machtigingen voor de site server om deze te publiceren naar deze container.
- De Configuration Manager-site is ingesteld om naar Active Directory Domain Services te publiceren.
- Clients behoren tot hetzelfde Active Directory forest als het forest van de site server.  

Gebruik [DNS-publicatie](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns)als clients op het intranet geen gebruik kunnen kunnen Active Directory Domain Services om beheer punten te vinden.  

Zie [begrijpen hoe clients site resources en-services vinden](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)voor algemene informatie over service locatie.  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Geselecteerde intranet beheer punten publiceren in DNS
Geef deze optie op wanneer clients op het intranet geen beheer punten kunnen vinden van Active Directory Domain Services. In plaats daarvan kunnen ze een bron record voor een DNS-service locatie (SRV RR) gebruiken om een beheer punt te vinden in hun toegewezen site.  

Voor Configuration Manager om intranet beheer punten te publiceren naar DNS, moeten aan alle volgende voor waarden worden voldaan:  

-   Uw DNS-servers hebben een versie van BIND die versie 8.1.2 of hoger is.  

-   Uw DNS-servers worden ingesteld voor automatische updates en de service locatie bron records worden ondersteund.  

-   De opgegeven FQDN-namen (FULLy Qualified Domain Name) voor de beheer punten in Configuration Manager hebben host-items (A-of AAA-records) in DNS.  

> [!WARNING]  
>  Voor clients om beheer punten te vinden die in DNS zijn gepubliceerd, moet u de clients toewijzen aan een specifieke site (in plaats van automatische site toewijzing te gebruiken). Stel deze clients in om de site code te gebruiken met het domein achtervoegsel van hun beheer punt. Zie [zoeken naar beheer punten](../../../clients/deploy/assign-clients-to-a-site.md#locating-management-points)voor meer informatie.  

Als Configuration Manager-clients Active Directory Domain Services of DNS niet kunnen gebruiken om beheer punten op het intranet te vinden, gebruiken ze [WINS](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). Het eerste beheer punt dat voor de site is geïnstalleerd, wordt automatisch naar WINS gepubliceerd wanneer het is ingesteld op het accepteren van HTTP-client verbindingen op het intranet.  


### <a name="status-reporting"></a>Status rapportage  

Deze instellingen stellen direct het detail niveau in dat is opgenomen in status rapporten van sites en clients.  


### <a name="email-notification"></a>E-mailmelding  

Geef account-en e-mailserver gegevens op om in te scha kelen Configuration Manager e-mail meldingen voor waarschuwingen te sturen.  

Zie [waarschuwingen en het status systeem gebruiken](../../manage/use-alerts-and-the-status-system.md)voor meer informatie.


### <a name="collection-membership-evaluation"></a><a name="bkmk_colleval"></a>Evaluatie lidmaatschap verzameling  

Gebruik dit onderdeel om in te stellen hoe vaak het verzamelings lidmaatschap stapsgewijs wordt geëvalueerd. Via stapsgewijze evaluatie werkt u een verzamelingslidmaatschap bij met uitsluitend nieuwe of gewijzigde bronnen.  

Zie [Aanbevolen procedures voor verzamelingen](../../../clients/manage/collections/best-practices-for-collections.md)voor meer informatie.



##  <a name="use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Configuration Manager Service Manager gebruiken om siteonderdelen te beheren  

U kunt de Configuration Manager Service Manager gebruiken om Configuration Manager-services te beheren en om de status van een Configuration Manager service of werk thread weer te geven. Deze services en threads worden gezamenlijk aangeduid als Configuration Manager onderdelen. Meer informatie over de volgende instructies over Configuration Manager-onderdelen:  

-   Onderdelen kunnen worden uitgevoerd op elk site systeem.  

-   Onderdelen worden op dezelfde manier beheerd als u services in Windows beheert. U kunt Configuration Manager onderdelen starten, stoppen, onderbreken, hervatten of opvragen.  

Een Configuration Manager-service wordt uitgevoerd wanneer er iets is om te doen. Deze actie wordt doorgaans uitgevoerd wanneer een configuratie bestand wordt geschreven naar het postvak in van een onderdeel. 


### <a name="use-the-configuration-manager-service-manager"></a>De Configuration Manager gebruiken Service Manager  

1.  Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **systeem status**uit en selecteer het knoop punt **onderdeel status** .  

2.  Selecteer in de **onderdeel** groep van het lint **Start**en kies vervolgens **Configuration Manager Service Manager**.  

3.  Wanneer het Configuration Manager-servicebeheer opent, verbindt dan met de site die u wilt beheren.  

     Als u de site die u wilt beheren niet ziet, gaat u naar het menu **site** en selecteert u **verbinding maken**. Voer vervolgens de naam van de site server van de juiste site in.  

4.  Vouw de site uit en navigeer naar **Onderdelen** of **Servers**, afhankelijk van waar de onderdelen zich bevinden die u wilt beheren.  

5.  Selecteer één of meer onderdelen in het rechterpaneel. Selecteer vervolgens in het menu **onderdeel** **query** om de status van uw selectie bij te werken.  

6.  Nadat de status van het onderdeel is bijgewerkt, gebruikt u een van de vier op actie gebaseerde opties in het menu **onderdeel** om de bewerking van het onderdeel te wijzigen. Nadat u een actie vraagt, moet u het onderdeel opvragen om de nieuwe status van het onderdeel weer te geven.  

7.  Sluit de Configuration Manager Service Manager wanneer u klaar bent met het wijzigen van de operationele status van onderdelen.  
