---
title: Grootte en schaal
titleSuffix: Configuration Manager
description: Bepaal het aantal site systeem rollen en-sites dat u nodig hebt om de apparaten in uw omgeving te ondersteunen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0861bb73769beb6c7595b896afc8d0e156eef94d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709640"
---
# <a name="size-and-scale-numbers-for-configuration-manager"></a>Grootte en schaalgrootte voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Elke Configuration Manager-implementatie heeft een maximum aantal sites, site systeem rollen en apparaten die kunnen worden ondersteund. Deze aantallen variëren, afhankelijk van uw hiërarchie structuur, de typen en aantallen sites die u gebruikt, en de site systeem rollen die u implementeert. De informatie in dit artikel kan u helpen bij het bepalen van het aantal site systeem rollen en-sites dat u nodig hebt om de apparaten te ondersteunen die u verwacht te beheren.

Raadpleeg voor meer informatie de volgende artikelen:

- [Aanbevolen hardware](recommended-hardware.md)
- [Ondersteunde besturingssystemen voor sitesysteemservers](supported-operating-systems-for-site-system-servers.md)  
- [Ondersteunde besturingssystemen voor clients en apparaten](supported-operating-systems-for-clients-and-devices.md)
- [Vereisten voor sites en sitesystemen](site-and-site-system-prerequisites.md)

Deze ondersteunings nummers zijn gebaseerd op het gebruik van de aanbevolen hardware voor Configuration Manager. Ze zijn ook gebaseerd op de standaard instellingen voor alle beschik bare Configuration Manager-functies. Wanneer u de aanbevolen hardware niet gebruikt of meer agressieve aangepaste instellingen gebruikt, kunnen de prestaties van site systemen afnemen. De site systemen voldoen mogelijk niet aan de vermelde ondersteunings niveaus. (Een voor beeld van een agressieve client instelling voert hardware-of software-inventarisatie vaker uit dan de standaard waarden van een keer per zeven dagen.)

## <a name="site-types"></a><a name="bkmk_SiteSystemScale"></a>Site typen  

### <a name="central-administration-site"></a>Centrale beheersite  

- Een centrale beheer site biedt ondersteuning voor Maxi maal 25 onderliggende primaire sites.  

### <a name="primary-site"></a>Primaire site  

- Elke primaire site ondersteunt Maxi maal 250 secundaire sites.  

- Het aantal secundaire sites per primaire site is gebaseerd op voortdurend verbonden en betrouw bare WAN-verbindingen (Wide Area Network). Voor locaties met minder dan 500 clients kunt u een distributie punt overwegen in plaats van een secundaire site.  

  Zie voor meer informatie over het aantal clients en apparaten dat door een primaire site kan worden ondersteund [client nummers voor sites en hiërarchieën](#bkmk_clientnumbers).  

### <a name="secondary-site"></a>Secundaire site  

- Secundaire sites bieden geen ondersteuning voor onderliggende sites.  

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Site systeem rollen

### <a name="application-catalog-web-service-point"></a>Application Catalog-webservicepunt  

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- U kunt meerdere exemplaren van het toepassingscatalogus-webservicepunt installeren op primaire sites.  

### <a name="application-catalog-website-point"></a>Application catalog-website punt  

> [!Important]
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

- U kunt meerdere exemplaren van het toepassingscatalogus website punt op primaire sites installeren.  

### <a name="cloud-management-gateway"></a><a name="bkmk_cmg"></a>Cloud beheer gateway

- U kunt meerdere exemplaren van de Cloud beheer gateway (CMG) installeren op primaire sites of op de centrale beheer site.  

    > [!Tip]  
    > Maak in een hiërarchie het CMG op de centrale beheer site.  

  - Een CMG ondersteunt één tot 16 virtuele machine-exemplaren (VM) in de Azure-Cloud service.  

  - Elk CMG VM-exemplaar ondersteunt 6.000 gelijktijdige client verbindingen. Wanneer de CMG een hoge belasting heeft wegens meer dan het ondersteunde aantal clients, worden er nog steeds aanvragen verwerkt, maar er kan een vertraging optreden.  

Zie CMG [prestaties en schalen](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) voor meer informatie.

### <a name="cloud-management-gateway-connection-point"></a>Verbindings punt van de Cloud beheer gateway

- U kunt meerdere exemplaren van het CMG-verbindings punt op primaire sites installeren.  

- Een CMG-verbindings punt kan een CMG ondersteunen met Maxi maal vier VM-exemplaren. Als de CMG meer dan vier VM-exemplaren heeft, voegt u een tweede CMG-verbindings punt toe voor taak verdeling. Een CMG met 16 VM-exemplaren moet worden gekoppeld aan vier CMG-verbindings punten.

Zie CMG [prestaties en schalen](../../clients/manage/cmg/plan-cloud-management-gateway.md#performance-and-scale) voor meer informatie.

> [!NOTE]
> Zie [Aanbevolen hardware voor externe site systeem servers](recommended-hardware.md#bkmk_RemoteSiteSystem)wanneer u de hardwarevereisten voor het CMG-verbindings punt overweegt.<!-- SCCMDocs#2276 -->

### <a name="distribution-point"></a>Distributiepunt  

- Distributie punten per site:  

  - Elke primaire en secundaire site ondersteunt Maxi maal 250 distributie punten.  

  - Elke primaire en secundaire site ondersteunt Maxi maal 2000 extra distributie punten die zijn geconfigureerd als pull-distributie punten. Eén primaire site ondersteunt **bijvoorbeeld**2250-distributie punten wanneer 2000 van deze distributie punten zijn geconfigureerd als pull-distributie punten.  

  - Elk distributie punt ondersteunt verbindingen van Maxi maal 4.000 clients.  

  - Een pull-distributie punt fungeert als een-client wanneer het toegang heeft tot inhoud van een bron distributiepunt.  

- Elke primaire site ondersteunt een gecombineerd totaal van Maxi maal 5.000 distributie punten. Dit totaal omvat alle distributie punten op de primaire site en alle distributie punten die deel uitmaken van de onderliggende secundaire sites van de primaire site.  

- Elk distributie punt ondersteunt een gecombineerd totaal van Maxi maal 10.000 pakketten en toepassingen.  

> [!WARNING]  
> Het werkelijke aantal clients dat een distributie punt kan ondersteunen, is afhankelijk van de snelheid van het netwerk en de hardwareconfiguratie van de server.  
>
> Het aantal pull-distributie punten dat door één bron distributiepunt kan worden ondersteund, is afhankelijk van de snelheid van het netwerk en de hardwareconfiguratie van het bron distributiepunt. Dit aantal wordt echter ook beïnvloed door de hoeveelheid inhoud die u hebt geïmplementeerd. Dit komt doordat, in tegens telling tot clients die doorgaans toegang hebben tot inhoud op verschillende momenten tijdens een implementatie, alle pull-distributie punten tegelijkertijd inhoud aanvragen. Pull-distributie punten kunnen alle beschik bare inhoud aanvragen, niet alleen de inhoud die van toepassing is op de gegevens. Wanneer u een hoge verwerkings belasting op een bron distributiepunt plaatst, kunnen er onverwachte vertragingen optreden bij het distribueren van de inhoud naar de doel distributiepunten.  

### <a name="fallback-status-point"></a>Terugvalstatuspunt  

- Elk terugval status punt kan Maxi maal 100.000 clients ondersteunen.  

### <a name="management-point"></a>Beheerpunt  

- Elke primaire site ondersteunt Maxi maal 15 beheer punten.  

    > [!TIP]  
    > Installeer geen beheer punten op servers die zich op een trage verbinding van de primaire site server of de site database server bevinden.  

- Elke secundaire site ondersteunt één beheer punt dat moet worden geïnstalleerd op de secundaire site server.  

Zie de sectie [beheer punten](#bkmk_mp) voor meer informatie over het aantal clients en apparaten dat door een beheer punt kan worden ondersteund.  

### <a name="software-update-point"></a>Software-updatepunt  

Gebruik de volgende aanbevelingen als basis lijn. Deze basis lijn helpt u bij het bepalen van de informatie voor de capaciteits planning voor software-updates die geschikt is voor uw organisatie. De werkelijke capaciteits vereisten kunnen afwijken van de aanbevelingen die in dit artikel worden vermeld, afhankelijk van de volgende criteria:

- Uw specifieke netwerk omgeving
- De hardware die u gebruikt om het site systeem van het software-update punt te hosten
- Het aantal beheerde clients
- De andere site systeem rollen die op de server zijn geïnstalleerd  

#### <a name="capacity-planning-for-the-software-update-point"></a><a name="BKMK_SUMCapacity"></a> Capaciteitsplanning voor het software-updatepunt  

Het aantal ondersteunde clients is afhankelijk van de versie van Windows Server Update Services (WSUS) die op het software-update punt wordt uitgevoerd. Het is ook afhankelijk van of de site systeemrol van het software-update punt naast een andere site systeemrol bestaat:  

- Het software-update punt kan Maxi maal 25.000 clients ondersteunen wanneer WSUS wordt uitgevoerd op de server van het software-update punt en het software-update punt naast een andere site systeemrol bestaat.  

- Het software-update punt kan Maxi maal 150.000 clients ondersteunen wanneer een externe server voldoet aan de WSUS-vereisten, WSUS wordt gebruikt met Configuration Manager en u de volgende instellingen configureert:

  Groepen van IIS-toepassingen:

  - Verhoog de wachtrijlengte voor WsusPool naar 2000
  - Verhoog de WsusPool privé-geheugen limiet X4-tijden of stel deze in op 0 (onbeperkt). Als de standaard limiet bijvoorbeeld 1.843.200 KB is, verhoogt u deze naar 7.372.800. Zie voor meer informatie dit [blog bericht over het ondersteunings team van Configuration Manager](https://www.phoenixtekk.com/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Zie [Aanbevolen hardware voor site systemen](recommended-hardware.md#bkmk_ScaleSieSystems)voor meer informatie over de hardwarevereisten voor het software-update punt.  

#### <a name="capacity-planning-for-software-updates-objects"></a><a name="bkmk_sum-capacity-obj"></a>Capaciteits planning voor software-update objecten  

Gebruik de volgende capaciteits informatie om te plannen voor software-update objecten:  

- **Limiet van 1000 software-updates in een implementatie** : Beperk het aantal software-updates tot 1000 voor elke implementatie van software-updates. Wanneer u een regel voor automatische implementatie (ADR) maakt, geeft u criteria op waarmee het aantal software-updates wordt beperkt. De ADR mislukt wanneer met de opgegeven criteria meer dan 1000 software-updates worden geretourneerd. Controleer de status van de ADR van het knoop punt **automatische implementatie regels** in de Configuration Manager-console. Wanneer u software-updates hand matig implementeert, selecteert u niet meer dan 1000 updates om te implementeren.  

  Beperk ook het aantal software-updates tot 1000 in een configuratie basislijn. Zie [configuratie basislijnen maken](../../../compliance/deploy-use/create-configuration-baselines.md)voor meer informatie.

- **Limiet van 580 beveiligingsbereiken voor regels voor automatische implementatie** -<!--ado 4962928-->
Beperk het aantal beveiligingsbereiken op automatische implementatie regels (Adr's) tot minder dan 580. Wanneer u een ADR maakt, worden de beveiligingsbereiken die toegang hebben tot het moment automatisch toegevoegd. Als er meer dan 580 beveiligingsbereiken zijn ingesteld, wordt de ADR niet uitgevoerd en wordt er een fout geregistreerd in bestand ruleengine. log.

### <a name="sms-provider"></a>SMS-provider

<!-- SCCMDocs#1958 -->

Elk exemplaar van de SMS-provider ondersteunt gelijktijdige verbindingen van meerdere aanvragen. De enige beperkingen met betrekking tot deze verbindingen zijn het aantal server verbindingen dat beschikbaar is voor Windows en de beschik bare bronnen op de server om de verbindings aanvragen te verwerken.

Zie [de SMS-provider plannen](../hierarchy/plan-for-the-sms-provider.md)voor meer informatie.

## <a name="client-numbers-for-sites-and-hierarchies"></a><a name="bkmk_clientnumbers"></a>Client nummers voor sites en hiërarchieën

Gebruik de volgende informatie om te bepalen hoeveel clients en welke typen clients u op een site of in een hiërarchie kunt ondersteunen.  

### <a name="hierarchy-with-a-central-administration-site"></a><a name="bkmk_cas"></a>Hiërarchie met een centrale beheer site

Een centrale beheer site ondersteunt een totaal aantal apparaten dat is opgenomen in het aantal apparaten dat wordt vermeld voor de volgende drie groepen:  

- 700.000 Windows-Desk tops. Zie ook ondersteuning voor [Inge sloten apparaten](#embedded).

- 25.000-apparaten met Mac en Windows CE 7,0  

- 100.000-apparaten die u beheert met behulp van on-premises Mobile Device Management (MDM)

In een-hiërarchie kunt u bijvoorbeeld 700.000-Desk tops ondersteunen, Maxi maal 25.000 Mac en Windows CE 7,0 apparaten, en Maxi maal 100.000 apparaten die worden beheerd door on-premises MDM. Deze hiërarchie ondersteunt een totaal van 825.000 apparaten.

> [!IMPORTANT]  
> In een-hiërarchie waarbij de centrale beheer site gebruikmaakt van een Standard-editie van SQL Server, ondersteunt de hiërarchie Maxi maal 50.000 Desk tops en apparaten. Als u meer dan 50.000 Desk tops en apparaten wilt ondersteunen, moet u een Enter prise-editie van SQL Server gebruiken. Deze vereiste geldt alleen voor een centrale beheer site. Het is niet van toepassing op een zelfstandige primaire site of een onderliggende primaire site. De versie van SQL Server die u voor een primaire site gebruikt, beperkt de capaciteit niet om het vermelde aantal clients te ondersteunen.

De versie van SQL Server die in gebruik is op een zelfstandige primaire site, beperkt de capaciteit van die site niet tot het aantal clients dat wordt ondersteund.  

### <a name="child-primary-site"></a><a name="bkmk_chipri"></a>Onderliggende primaire site

Elke onderliggende primaire site in een hiërarchie met een centrale beheer site ondersteunt het volgende aantal clients:  

- 150.000 totaal aantal clients en apparaten dat niet beperkt is tot een specifieke groep of type, zolang ondersteuning niet groter is dan het aantal dat voor de hiërarchie wordt ondersteund. Zie ook ondersteuning voor [Inge sloten apparaten](#embedded).

Een primaire site ondersteunt bijvoorbeeld 25.000 Mac en Windows CE 7,0-apparaten. Dat aantal is de limiet voor een hiërarchie. Deze primaire site kan vervolgens een extra 125.000 desktop-computer ondersteunen. Het totale aantal ondersteunde apparaten voor de onderliggende primaire site is de ondersteunde maximum limiet van 150.000.

### <a name="stand-alone-primary-site"></a><a name="bkmk_pri"></a>Zelfstandige primaire site

Een zelfstandige primaire site ondersteunt het volgende aantal apparaten:  

- 175.000 totaal aantal clients en apparaten, Maxi maal:  

  - 150.000 Desk tops (computers waarop Windows, Linux en UNIX worden uitgevoerd). Zie ook ondersteuning voor [Inge sloten apparaten](#embedded).

  - 25.000-apparaten met Mac en Windows CE 7,0

  - 50.000-apparaten die u beheert met on-premises MDM  

Een zelfstandige primaire site die 150.000 Desk tops en 10.000 Macs ondersteunt, kan bijvoorbeeld alleen ondersteuning bieden voor een extra 15.000 mobiele apparaten die worden beheerd door on-premises MDM.

### <a name="primary-sites-and-windows-embedded-devices"></a><a name="embedded"></a>Primaire sites en Windows Embedded-apparaten

Primaire sites bieden ondersteuning voor Windows Embedded-apparaten waarvoor schrijf filters op basis van bestanden (FBWF) zijn ingeschakeld. Wanneer op Inge sloten apparaten geen schrijf filters zijn ingeschakeld, kan een primaire site een aantal Inge sloten apparaten ondersteunen tot het toegestane aantal apparaten voor die site. Wanneer FBWF of Unified write filters (UWF) is ingeschakeld op Inge sloten apparaten, kan een primaire site een maximum van 10.000 Windows Embedded-apparaten ondersteunen. Deze apparaten moeten worden geconfigureerd met de uitzonde ringen die worden vermeld in de belang rijke opmerking die is gevonden in de [planning voor client implementatie op Windows Embedded-apparaten](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md). Een primaire site ondersteunt slechts 3.000 Windows Embedded-apparaten waarop EWF is ingeschakeld en die niet zijn geconfigureerd voor de uitzonde ringen.

### <a name="secondary-sites"></a><a name="bkmk_sec"></a>Secundaire sites

Secundaire sites ondersteunen het volgende aantal apparaten:  

- 15.000 Desk tops (computers waarop Windows, Linux en UNIX worden uitgevoerd)  

### <a name="management-points"></a><a name="bkmk_mp"></a>Beheer punten

Elk beheer punt kan het volgende aantal apparaten ondersteunen:  

- 25.000 totaal aantal clients en apparaten, Maxi maal:  

  - 25.000 Desk tops (computers waarop Windows, Linux en UNIX worden uitgevoerd)  

  - Een van de volgende (niet beide):  

    - 10.000-apparaten die worden beheerd met on-premises MDM  

    - 10.000-apparaten met Mac en Windows CE 7,0-clients
