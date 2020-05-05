---
title: Poorten die worden gebruikt voor verbindingen
titleSuffix: Configuration Manager
description: Meer informatie over de vereiste en aanpas bare netwerk poorten die door Configuration Manager worden gebruikt voor verbindingen.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b75ebe7e768080a1239e817c514b634cdcf64179
ms.sourcegitcommit: b7e5b053dfa260e7383a9744558d50245f2bccdc
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/29/2020
ms.locfileid: "82587175"
---
# <a name="ports-used-in-configuration-manager"></a>Poorten die worden gebruikt in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat een lijst met de netwerk poorten die Configuration Manager gebruikt. Sommige verbindingen gebruiken poorten die niet kunnen worden geconfigureerd, en sommige ondersteunde aangepaste poorten die u opgeeft. Als u een technologie voor poort filtering gebruikt, controleert u of de vereiste poorten beschikbaar zijn. Deze technologieën voor poort filtering omvatten firewalls, routers, proxy servers of IPsec.

> [!NOTE]  
> Als u client-clients met behulp van SSL-bridging en poort vereisten ondersteunt, moet u mogelijk ook sommige HTTP-woorden en-headers toestaan om door te gaan met uw firewall.

## <a name="ports-you-can-configure"></a><a name="BKMK_ConfigurablePorts"></a> Poorten die u kunt configureren

Met Configuration Manager kunt u de poorten configureren voor de volgende communicatie typen:  

- toepassingscatalogus website punt naar toepassingscatalogus Web Service Point  

- Registratie-proxypunt naar registratiepunt  

- Client-naar-site-systemen die IIS uitvoeren  

- Client naar Internet (als instellingen voor de proxy server)  

- Software-update punt naar Internet (als instellingen van de proxy server)  

- Software-updatepunt naar WSUS-server  

- Siteserver met sitedatabaseserver  

- Site server naar WSUS-database server

- Reporting Services-punten  

  > [!NOTE]  
  > De poorten die in gebruik zijn voor de site systeemrol van het Reporting Services-punt worden geconfigureerd in SQL Server Reporting Services. Deze poorten worden vervolgens door Configuration Manager gebruikt tijdens de communicatie met het Reporting Services-punt. Zorg ervoor dat u deze poorten bekijkt die de IP-filter gegevens definiëren voor IPsec-beleid of voor het configureren van firewalls.  

Standaard is de HTTP-poort die wordt gebruikt voor client-naar-site systeem communicatie poort 80 en de standaard HTTPS-poort 443. Poorten voor client-naar-site-systeem communicatie via HTTP of HTTPS kunnen worden gewijzigd tijdens de installatie of in de site-eigenschappen voor uw Configuration Manager-site.  

De poorten die in gebruik zijn voor de site systeemrol van het Reporting Services-punt worden geconfigureerd in SQL Server Reporting Services. Deze poorten worden vervolgens door Configuration Manager gebruikt tijdens de communicatie met het Reporting Services-punt. Zorg ervoor dat u deze poorten bekijkt wanneer u de IP-filter informatie definieert voor IPsec-beleid of voor het configureren van firewalls.  

## <a name="non-configurable-ports"></a><a name="BKMK_NonConfigurablePorts"></a> Niet-configureerbare poorten  

Met Configuration Manager kunt u geen poorten configureren voor de volgende communicatie typen:  

- Site-naar-site  

- Siteserver-naar-site-systeem  

- Configuration Manager-console naar SMS-provider  

- Configuration Manager-console op Internet  

- Verbindingen met Cloud Services, zoals Microsoft Intune en Cloud distributiepunten  

## <a name="ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMK_CommunicationPorts"></a> Poorten die door Configuration Manager-clients en sitesystemen worden gebruikt  

De volgende secties beschrijven de poorten die worden gebruikt voor communicatie in Configuration Manager. De pijlen in de sectie titel tonen de richting van de communicatie:  

- --> geeft aan dat de ene computer communicatie start en de andere computer altijd reageert  

- &lt;--> geeft aan dat de computer communicatie kan starten  

### <a name="asset-intelligence-synchronization-point----microsoft"></a><a name="BKMK_PortsAI"></a>Asset Intelligence synchronisatie punt--> micro soft  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="asset-intelligence-synchronization-point----sql-server"></a><a name="BKMK_PortsAI-to-SQL"></a>Asset Intelligence synchronisatie punt--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="application-catalog-web-service-point----sql-server"></a><a name="BKMK_PortsAppCatalogService-SQL"></a>Toepassingscatalogus-webservicepunt--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="application-catalog-website-point----application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a>Toepassingscatalogus website punt: > toepassingscatalogus Web Service Point  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="client----application-catalog-website-point"></a><a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a>Client--> toepassingscatalogus website punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="client----client"></a><a name="BKMK_PortsClient-ClientWakeUp"></a>Client-->-client  

Wake-up proxy gebruikt ook ICMP echo-aanvraag berichten van een client naar een andere client. Clients gebruiken deze communicatie om te bevestigen of de andere client zich in het netwerk bevindt. ICMP wordt soms ook wel ping-opdrachten genoemd. ICMP heeft geen UDP-of TCP-protocol nummer en wordt dus niet weer gegeven in de onderstaande tabel. Evenwel moet elke host-gebaseerde firewall op deze clientcomputers of tussenliggende netwerkapparaten binnen het subnet ICMP-verkeer toelating geven ​​voor wake-up proxy communicatie om te slagen.  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|--|  
|Wake-up proxy|25536 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|--|  
|Windows PE-peer-cache-broadcast|8004|--|  
|Windows PE-peer-cache downloaden|--|8003|  

Zie [Windows PE-peer-cache](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#BKMK_PeerCacheRequirements)voor meer informatie.

### <a name="client----configuration-manager-network-device-enrollment-service-ndes-policy-module"></a><a name="BKMK_PortsClient-PolicyModule"></a>Client--> Configuration Manager NDES-beleids module (registratie service voor netwerk apparaten)

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  

### <a name="client----cloud-distribution-point"></a><a name="BKMK_PortsClient-CloudDP"></a>Client--> Cloud distributiepunt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Zie [poorten en data flow](use-a-cloud-based-distribution-point.md#bkmk_dataflow)voor meer informatie.

### <a name="client----cloud-management-gateway-cmg"></a><a name="bkmk_client-cmg"></a>Client--> Cloud beheer gateway (CMG)  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Zie [CMG ports and data flow](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)(Engelstalig) voor meer informatie.

### <a name="client----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP"></a>Client--> distributie punt, zowel standaard als pull  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|
|Snelle updates|--|8005 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|<!-- SCCMDocs#2091 -->

> [!NOTE]
> Gebruik client instellingen om de alternatieve poort voor snelle updates te configureren. Zie [poort die clients gebruiken om aanvragen voor Delta-inhoud te ontvangen](../../clients/deploy/about-client-settings.md#port-that-clients-use-to-receive-requests-for-delta-content)voor meer informatie.

### <a name="client----distribution-point-configured-for-multicast-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP2"></a>Client--> distributie punt dat is geconfigureerd voor multi cast, zowel standaard als pull  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|Multi Cast-protocol|63000-64000|--|  

### <a name="client----distribution-point-configured-for-pxe-both-standard-and-pull"></a><a name="BKMK_PortsClient-DP3"></a>Client--> distributie punt dat is geconfigureerd voor PXE, zowel standaard als pull  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 en 68|--|  
|TFTP|69 <sup> [Opmerking 4](#bkmk_note4)</sup> |--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

> [!Important]  
> Als u een op een host gebaseerde firewall inschakelt, moet u ervoor zorgen dat de-server toestaat dat deze poorten worden verzonden en ontvangen. Wanneer u een distributie punt voor PXE inschakelt, kunt Configuration Manager de regels voor binnenkomend verkeer (ontvangen) inschakelen op de Windows Firewall. De regels voor uitgaande verbindingen (verzenden) worden niet geconfigureerd.<!--SCCMDocs issue #744-->  

### <a name="client----fallback-status-point"></a><a name="BKMK_PortsClient-FSP"></a>Client--> terugval status punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="client----global-catalog-domain-controller"></a><a name="BKMK_PortsClient-GCDC"></a>Client--> globale catalogus-domein controller

Een Configuration Manager-client neemt geen contact op met een globale catalogus server wanneer het een werkgroepcomputer is of wanneer deze is geconfigureerd voor communicatie via internet.  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Global Catalog LDAP|--|3268|  

### <a name="client----management-point"></a><a name="BKMK_PortsClient-MP"></a>Client--> beheer punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Melding client (standaardcommunicatie vóór terug te vallen op HTTP of HTTPS)|--|10123 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|HTTP|--|80 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="client----software-update-point"></a><a name="BKMK_PortsClient-SUP"></a>Client--> software-update punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 of 8530 <sup> [Opmerking 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 of 8531 <sup> [Opmerking 3](#bkmk_note3)</sup>|  

### <a name="client----state-migration-point"></a><a name="BKMK_PortsClient-SMP"></a>Client--> status migratie punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|Server Message Block (SMB)|--|445|  

### <a name="cmg-connection-point----cmg-cloud-service"></a><a name="bkmk_cmgcp-cmg"></a>CMG-verbindings punt--> CMG-Cloud service  

Configuration Manager maakt gebruik van deze verbindingen om het CMG-kanaal te bouwen. Zie [CMG ports and data flow](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)(Engelstalig) voor meer informatie.

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (voor keur)|--|10140-10155|  
|HTTPS (terugval met één virtuele machine)|--|443|  
|HTTPS (terugval met twee of meer Vm's)|--|10124-10139|  

### <a name="cmg-connection-point----management-point"></a><a name="bkmk_cmgcp-mp"></a>CMG-verbindings punt--> beheer punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Zie [CMG ports and data flow](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)(Engelstalig) voor meer informatie.

### <a name="cmg-connection-point----software-update-point"></a><a name="bkmk_cmgcp-sup"></a>CMG-verbindings punt--> software-update punt  

De specifieke poort is afhankelijk van de configuratie van het software-update punt.

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Zie [CMG ports and data flow](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)(Engelstalig) voor meer informatie.

### <a name="configuration-manager-console----client"></a><a name="BKMK_PortsConsole-Client"></a>Configuration Manager-console-->-client  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Beheer op afstand (controle)|--|2701|  
|Hulp op afstand (RDP en RTC)|--|3389|  

### <a name="configuration-manager-console----internet"></a><a name="BKMK_PortsConsole-Internet"></a>Configuration Manager-console--> Internet  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

De Configuration Manager-console maakt gebruik van Internet toegang voor de volgende acties:

- Downloaden van software-updates van Microsoft Update voor implementatie pakketten.
- Het feedback-item op het lint.
- Koppelingen naar documentatie in de-console.
<!--506823-->

### <a name="configuration-manager-console----reporting-services-point"></a><a name="BKMK_PortsConsole-RSP"></a>Configuration Manager-console--> Reporting Services-punt  

|Beschrijving|UDP|TCP|
|-----------------|---------|---------|
|HTTP|--|80 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="configuration-manager-console----site-server"></a><a name="BKMK_PortsConsole-Site"></a>Configuration Manager-console--> site server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (initiële verbinding naar WMI om providersysteem te vinden)|--|135|  

### <a name="configuration-manager-console----sms-provider"></a><a name="BKMK_PortsConsole-Provider"></a>Configuration Manager-console--> SMS-provider  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="configuration-manager-network-device-enrollment-service-ndes-policy-module----certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a>Configuration Manager beleids module voor de registratie service voor netwerk apparaten (NDES)--> certificaat registratiepunt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="data-warehouse-service-point----sql-server"></a><a name="BKMK_PortsDWSPSQL"></a>Data Warehouse-service punt--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="distribution-point-both-standard-and-pull----management-point"></a><a name="BKMK_PortsDist_MP"></a>Distributie punt, zowel standaard als pull-> beheer punt

Een distributiepunt communiceert met het beheerpunt in de volgende scenario's:  

- De status van voor bereide inhoud rapporteren  

- Samenvattingsgegevens over gebruik rapporteren  

- Inhoudsvalidatie rapporteren  

- De status van pakket downloads melden (alleen voor pull-distributie punten)

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="endpoint-protection-point----internet"></a><a name="BKMK_PortsEndpointProtection_Internet"></a>Endpoint Protection punt--> Internet  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  

### <a name="endpoint-protection-point----sql-server"></a><a name="BKMK_PortsEP-to-SQL"></a>Endpoint Protection punt--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="enrollment-proxy-point----enrollment-point"></a><a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a>Proxy punt voor inschrijving--> inschrijvings punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="enrollment-point----sql-server"></a><a name="BKMK_PortsEnrollmentEnrollmentSQL"></a>Inschrijvings punt--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="exchange-server-connector----exchange-online"></a><a name="BKMK_PortsExchangeConnectorHosted"></a>Exchange Server-connector--> Exchange Online  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Windows Remote Management via HTTPS|--|5986|  

### <a name="exchange-server-connector----on-premises-exchange-server"></a><a name="BKMK_PortsExchangeConnectorOnPrem"></a>Exchange Server-connector--> on-premises Exchange Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Windows Remote Management via HTTP|--|5985|  

### <a name="mac-computer----enrollment-proxy-point"></a><a name="BKMK_PortsMacEnrollmentProxyPoint"></a>Mac-computer--> proxy punt voor inschrijving  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

### <a name="management-point----domain-controller"></a><a name="BKMK_PortsMP-DC"></a>Beheer punt--> domein controller  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|389|389|  
|Secure LDAP (LDAPS, voor ondertekening en binding)|636|636|  
|Global Catalog LDAP|--|3268|  
|RPC-eindpunttoewijzer|--|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="management-point-lt---site-server"></a><a name="BKMK_PortsMP-Site"></a>Beheer punt &lt;--> site server

<sup>[Opmerking 5](#bkmk_note5)</sup>

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-eindpunttoewijzer|--|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  
|Server Message Block (SMB)|--|445|  

### <a name="management-point----sql-server"></a><a name="BKMK_PortsMP-SQL"></a>Beheer punt--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="mobile-device----enrollment-proxy-point"></a><a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a>Mobiel apparaat--> proxy punt voor inschrijving  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

###  <a name="reporting-services-point----sql-server"></a><a name="BKMK_PortsRSP-SQL"></a>Reporting Services-punt--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="service-connection-point----azure-cmg"></a><a name="bkmk_scp-cmg"></a>Service verbindings punt--> Azure (CMG)  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS voor CMG-service-implementatie|--|443|

Zie [CMG ports and data flow](../../clients/manage/cmg/plan-cloud-management-gateway.md#ports-and-data-flow)(Engelstalig) voor meer informatie.

### <a name="site-server-lt---application-catalog-web-service-point"></a><a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a>Site server &lt;--> toepassingscatalogus-webservicepunt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---application-catalog-website-point"></a><a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a>Site server &lt;--> toepassingscatalogus website punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---asset-intelligence-synchronization-point"></a><a name="BKMK_PortsSite-AISP"></a>Site server &lt;--> Asset Intelligence synchronisatie punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server----client"></a><a name="BKMK_PortsSite-Client"></a>Site Server-->-client  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Wake on LAN|9 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|--|  

### <a name="site-server----cloud-distribution-point"></a><a name="BKMK_PortsSiteServer-CloudDP"></a>Site Server--> Cloud distributiepunt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Zie [poorten en data flow](use-a-cloud-based-distribution-point.md#bkmk_dataflow)voor meer informatie.

### <a name="site-server----distribution-point-both-standard-and-pull"></a><a name="BKMK_PortsSite-DP"></a>Site Server--> distributie punt, zowel standaard als pull

<sup>[Opmerking 5](#bkmk_note5)</sup>  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server----domain-controller"></a><a name="BKMK_PortsSite-DC"></a>Site Server--> domein controller  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Lightweight Directory Access Protocol (LDAP)|389|389|
|Secure LDAP (LDAPS, voor ondertekening en binding)|636|636|
|Global Catalog LDAP|--|3268|  
|RPC-eindpunttoewijzer|--|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---certificate-registration-point"></a><a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a>Site server &lt;--> certificaat registratiepunt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---cmg-connection-point"></a><a name="BKMK_CMGCP_SiteServer"></a>Site server &lt;--> CMG-verbindings punt

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---endpoint-protection-point"></a><a name="BKMK_PortsEndpointProtection_SiteServer"></a>Site server &lt;--> Endpoint Protection punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-point"></a><a name="BKMK_EnrollmentPoint_SiteServer"></a>Site server &lt;--> inschrijvings punt  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---enrollment-proxy-point"></a><a name="BKMK_EnrollmentProxyPoint_SiteServer"></a>Site server &lt;--> proxy punt voor inschrijving  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---fallback-status-point"></a><a name="BKMK_PortsSite-FSP"></a>Site server &lt;--> terugval status punt

<sup>[Opmerking 5](#bkmk_note5)</sup>  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server----internet"></a><a name="BKMK_PortSite-Internet"></a>Site Server--> Internet  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Opmerking 1](#bkmk_note1)</sup>|  

### <a name="site-server-lt---issuing-certification-authority-ca"></a><a name="BKMK_PortsIssuingCA_SiteServer"></a>Site server &lt;--> uitgeven van certificerings instantie (CA)

Deze communicatie wordt gebruikt wanneer u certificaatprofielen implementeert door gebruik te maken van het certificaatregistratiepunt. De communicatie wordt niet gebruikt voor elke site server in de hiërarchie. In plaats daarvan wordt deze alleen gebruikt voor de site server bovenaan de hiërarchie.  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|RPC-eindpunttoewijzer|135|135|  
|RPC (DCOM)|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server----server-hosting-remote-content-library-share"></a><a name="BKMK_PortsSite-RCL"></a>Site Server--> server die als host fungeert voor een externe inhouds bibliotheek share

U kunt de inhouds bibliotheek verplaatsen naar een andere opslag locatie om ruimte op de vaste schijf vrij te maken op uw centrale beheer-of primaire site servers. Zie [een externe inhouds bibliotheek voor de site server configureren](the-content-library.md#bkmk_remote)voor meer informatie.

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="site-server-lt---service-connection-point"></a><a name="BKMK_SCP_SiteServer"></a>Site server &lt;--> service verbindings punt

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---reporting-services-point"></a><a name="BKMK_PortsSite-RSP"></a>Site server &lt;--> Reporting Services-punt

<sup>[Opmerking 5](#bkmk_note5)</sup>  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---site-server"></a><a name="BKMK_PortsSite-Site"></a>Site server &lt;-->-site server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="site-server----sql-server"></a><a name="BKMK_PortsSite-SQL"></a>Site Server-> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

Tijdens de installatie van een site die gebruikmaakt van een externe SQL Server om de site database te hosten, opent u de volgende poorten tussen de site server en de SQL Server:  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server----sql-server-for-wsus"></a><a name="BKMK_PortsSite-SQL-WSUS"></a>Site Server--> SQL Server voor WSUS  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 3](#bkmk_note3) alternatieve poort beschikbaar</sup>|  

### <a name="site-server----sms-provider"></a><a name="BKMK_PortsSite-Provider"></a>Site Server--> SMS-provider  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  
|RPC|--|DYNAMISCHE <sup> [Opmerking 6](#bkmk_note6)</sup>|  

### <a name="site-server-lt---software-update-point"></a><a name="BKMK_PortsSite-SUP"></a>Site server &lt;--> software-update punt

<sup>[Opmerking 5](#bkmk_note5)</sup>  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|HTTP|--|80 of 8530 <sup> [Opmerking 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 of 8531 <sup> [Opmerking 3](#bkmk_note3)</sup>|  

### <a name="site-server-lt---state-migration-point"></a><a name="BKMK_PortsSite-SMP"></a>Site server &lt;--> status migratie punt

<sup>[Opmerking 5](#bkmk_note5)</sup>  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  
|RPC-eindpunttoewijzer|135|135|  

### <a name="sms-provider----sql-server"></a><a name="BKMK_PortsProvider-SQL"></a>SMS-provider--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="software-update-point----internet"></a><a name="BKMK_PortsSUP-Internet"></a>Software-update punt--> Internet  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [Opmerking 1](#bkmk_note1)</sup>|  

### <a name="software-update-point----upstream-wsus-server"></a><a name="BKMK_PortsSUP-WSUS"></a>Software-update punt--> upstream-WSUS-server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 of 8530 <sup> [Opmerking 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 of 8531 <sup> [Opmerking 3](#bkmk_note3)</sup>|  

### <a name="sql-server----sql-server"></a><a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server

Replicatie van de intersite-data base vereist dat de SQL Server op één site rechtstreeks communiceert met de SQL Server op de bovenliggende of onderliggende site.  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server-service|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  
|SQL Server Service Broker|--|4022 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

> [!TIP]  
> Voor Configuration Manager is de SQL Server Browser niet vereist, dat gebruikmaakt van poort UDP 1434.  

### <a name="state-migration-point----sql-server"></a><a name="BKMK_PortsStateMigrationPoint-to-SQL"></a>Status migratie punt--> SQL Server  

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|SQL via TCP|--|1433 <sup> [Opmerking 2](#bkmk_note2) alternatieve poort beschikbaar</sup>|  

### <a name="notes-for-ports-used-by-configuration-manager-clients-and-site-systems"></a><a name="BKMY_PortNotes"></a> Opmerkingen voor poorten die door Configuration Manager-clients en sitesystemen worden gebruikt  

#### <a name="note-1-proxy-server-port"></a><a name="bkmk_note1"></a>Opmerking 1: poort van proxy server

Deze poort kan niet worden geconfigureerd, maar kan worden gerouteerd via een geconfigureerde proxy server.  

#### <a name="note-2-alternate-port-available"></a><a name="bkmk_note2"></a>Opmerking 2: alternatieve poort beschikbaar

U kunt voor deze waarde een alternatieve poort definiëren in Configuration Manager. Als u een aangepaste poort definieert, gebruikt u die aangepaste poort in de IP-filter informatie voor IPsec-beleid of voor het configureren van firewalls.  

#### <a name="note-3-windows-server-update-services-wsus"></a><a name="bkmk_note3"></a>Opmerking 3: Windows Server Update Services (WSUS)

WSUS kan worden geïnstalleerd voor het gebruik van poort 80/443 of poorten 8530/8531 voor client communicatie. Wanneer u WSUS uitvoert in Windows Server 2012 of Windows Server 2016, wordt WSUS standaard geconfigureerd voor het gebruik van poort 8530 voor HTTP en poort 8531 voor HTTPS.  

Na de installatie kunt u de poort te wijzigen. U hoeft niet hetzelfde poort nummer te gebruiken in de site hiërarchie.  

- Als de HTTP-poort 80 is, moet de HTTPS-poort 443 zijn.  

- Als de HTTP-poort iets anders is, moet de HTTPS-poort 1 of hoger zijn, bijvoorbeeld 8530 en 8531.

    > [!NOTE]  
    >  Wanneer u het software-updatepunt voor gebruik van HTTPS configureert, moet de HTTP-poort ook zijn geopend. Niet-versleutelde gegevens, zoals de gebruiksrechtovereenkomst voor specifieke updates, gebruiken de HTTP-poort.

- De site server maakt verbinding met de SQL-Server die als host fungeert voor de SUSDB wanneer u de volgende opties voor WSUS-opschoning inschakelt:
  - Niet-geclusterde indexen toevoegen aan de WSUS-Data Base voor het verbeteren van de prestaties van WSUS-opschoning
  - Verouderde updates verwijderen uit de WSUS-data base
  
  Als de standaard SQL Server poort wordt gewijzigd naar een andere poort met SQL Server Configuration Manager, moet u ervoor zorgen dat de site server verbinding kan maken met behulp van de gedefinieerde poort. Configuration Manager biedt geen ondersteuning voor dynamische poorten. SQL Server benoemde instanties gebruiken standaard dynamische poorten voor verbindingen met de data base-engine. Wanneer u een benoemd exemplaar gebruikt, configureert u de statische poort hand matig.

#### <a name="note-4-trivial-ftp-tftp-daemon"></a><a name="bkmk_note4"></a>Opmerking 4: Trivial FTP (TFTP) daemon

De Trivial FTP (TFTP) daemon-systeem service vereist geen gebruikers naam of wacht woord en is een integraal onderdeel van Windows Deployment Services (WDS). De Trivial FTP daemon service implementeert ondersteuning voor het TFTP-protocol dat is gedefinieerd door de volgende Rfc's:  

- RFC 1350: TFTP  

- RFC 2347: optie-uitbrei ding  

- RFC 2348: optie blok grootte  

- RFC 2349: time-outinterval en opties voor overdrachts grootte  

TFTP is ontworpen voor ondersteuning van opstart omgevingen met schijven. TFTP Daemons luisteren op UDP-poort 69 maar antwoorden vanaf een dynamisch toegewezen hoge poort. Als u deze poort inschakelt, kan de TFTP-service binnenkomende TFTP-aanvragen ontvangen, maar de geselecteerde server kan niet op deze aanvragen reageren. U kunt de geselecteerde server niet in staat stellen om te reageren op binnenkomende TFTP-aanvragen tenzij u de TFTP-server zo configureert dat deze reageert op poort 69.  

Het distributie punt met PXE-functionaliteit en de client in Windows PE selecteren dynamisch toegewezen hoge poorten voor TFTP-overdrachten. Deze poorten worden door micro soft gedefinieerd tussen 49152 en 65535. Zie [service-overzicht en vereisten voor de netwerk poort voor Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows) voor meer informatie.

Tijdens de daad werkelijke PXE-opstart optie selecteert de netwerk kaart op het apparaat echter de dynamisch toegewezen hoge poort die wordt gebruikt tijdens de TFTP-overdracht. De netwerk kaart op het apparaat is niet gekoppeld aan de dynamisch toegewezen hoge poorten die door micro soft zijn gedefinieerd. Het is alleen gebonden aan de poorten die zijn gedefinieerd in RFC 1350. Deze poort kan een waarde hebben van 0 tot en met 65535. Neem contact op met de hardwarefabrikant van het apparaat voor meer informatie over de dynamisch toegewezen hoge poorten die door de netwerk kaart worden gebruikt.

#### <a name="note-5-communication-between-the-site-server-and-site-systems"></a><a name="bkmk_note5"></a>Opmerking 5: communicatie tussen de site server en site systemen

De communicatie tussen de site server en site systemen is standaard twee richtings. De site server start communicatie om het site systeem te configureren, waarna de meeste site systemen weer verbinding maken met de site server om status informatie te verzenden. Rapportage service punten en distributie punten verzenden geen status gegevens. Als u **vereisen dat de site server verbindingen met dit site systeem initieert** op de site systeem eigenschappen nadat het site systeem is geïnstalleerd, start het site systeem de communicatie met de site server niet. In plaats daarvan wordt de communicatie met de site server gestart. Het gebruikt het installatie account van het site systeem voor verificatie naar de site systeem server.  

#### <a name="note-6-dynamic-ports"></a><a name="bkmk_note6"></a>Opmerking 6: dynamische poorten

Dynamische poorten gebruiken een bereik van poort nummers die worden gedefinieerd door de versie van het besturings systeem. Deze poorten worden ook wel kortstondige poorten genoemd. Voor meer informatie over de standaardpoortbereiken, zie [Service overview and network port requirements for Windows (Service overzicht en netwerk poortvereisten voor Windows)](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

## <a name="additional-lists-of-ports"></a><a name="BKMK_AdditionalPorts"></a> Aanvullende lijsten met poorten  

In de volgende secties vindt u aanvullende informatie over poorten die door Configuration Manager worden gebruikt.

### <a name="client-to-server-shares"></a><a name="BKMK_ClientShares"></a> Client naar servershares

Clients gebruiken Server Message Block (SMB) wanneer ze verbinden met UNC shares. Bijvoorbeeld:

- Hand matige client installatie waarmee de CCMSetup. exe **/Source:** opdracht regel eigenschap wordt opgegeven  

- Endpoint Protection-clients die definitie bestanden downloaden van een UNC-pad

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB)|--|445|  

### <a name="connections-to-microsoft-sql-server"></a><a name="BKMK_SQLPorts"></a> Verbindingen met Microsoft SQL Server

Voor communicatie met de SQL Server database-engine en voor intersitereplicatie kunt u de standaard SQL Server-poort gebruiken of aangepaste poorten opgeven:  

- Gebruik van de communicatie tussen sites:  

  - SQL Server Service Broker is standaard poort TCP 4022.  

  - SQL Server-service, die wordt ingesteld als poort TCP 1433.  

- Intra site-communicatie tussen de SQL Server data base-engine en verschillende Configuration Manager site systeem rollen wordt standaard ingesteld op poort TCP 1433.  

- Configuration Manager gebruikt dezelfde poorten en protocollen om te communiceren met elke replica van de SQL-beschikbaarheids groep die als host fungeert voor de site database, alsof de replica een zelfstandig SQL Server exemplaar is.

Wanneer u Azure gebruikt en de site database zich achter een interne of externe load balancer bevindt, configureert u de volgende onderdelen:

- Firewall-uitzonde ringen op elke replica
- Taakverdelings regels

Configureer de volgende poorten:

- SQL via TCP: TCP 1433
- SQL Server Service Broker: TCP 4022
- Server Message Block (SMB): TCP 445
- RPC-eindpunttoewijzer: TCP 135

> [!WARNING]  
> Configuration Manager biedt geen ondersteuning voor dynamische poorten. SQL Server benoemde instanties gebruiken standaard dynamische poorten voor verbindingen met de data base-engine. Wanneer u een benoemd exemplaar gebruikt, configureert u de statische poort voor intra site-communicatie hand matig.  

De volgende sitesysteemrollen communiceren direct met de SQL Server database:  

- Application Catalog-webservicepunt  

- Certificaatregistratiepuntrol  

- Servicepunt voor inschrijving  

- Beheerpunt  

- Siteserver  

- Reporting Services-punt  

- SMS-provider  

- SQL Server--> SQL Server  

Wanneer een SQL Server als host fungeert voor een Data Base van meer dan één site, moet elke Data Base een afzonderlijk exemplaar van SQL Server gebruiken. Configureer elk exemplaar met een unieke set poorten.  

Als u een op een host gebaseerde firewall op de SQL-server inschakelt, configureert u deze zodanig dat de juiste poorten zijn toegestaan. Configureer ook netwerk firewalls tussen computers die communiceren met de SQL-Server.  

Zie [een server configureren om te Luis teren naar een specifieke TCP-poort](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)voor een voor beeld van het configureren van SQL Server voor het gebruik van een specifieke poort.  

### <a name="discovery-and-publishing"></a><a name="bkmk_discovery"> </a> Detectie en publicatie

Configuration Manager gebruikt de volgende poorten voor de detectie en publicatie van site-informatie:

- Lightweight Directory Access Protocol (LDAP): 389
- Secure LDAP (LDAPS, voor ondertekening en binding): 636
- Global Catalog LDAP: 3268
- RPC-eindpunttoewijzer: 135
- RPC: dynamisch toegewezen hoge TCP-poorten
- TCP: 1024:5000
- TCP: 49152:65535

### <a name="external-connections-made-by-configuration-manager"></a><a name="BKMK_External"></a> Externe verbindingen gemaakt door Configuration Manager

On-premises Configuration Manager-clients of site systemen kunnen de volgende externe verbindingen maken:  

- [Asset Intelligence synchronisatie punt--&gt; micro soft](#BKMK_PortsAI)  

- [Endpoint Protection punt--&gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

- [Client--&gt; globale catalogus-domein controller](#BKMK_PortsClient-GCDC)  

- [Configuration Manager-console-&gt; -Internet](#BKMK_PortsConsole-Internet)  

- [Beheer punt--&gt; domein controller](#BKMK_PortsMP-DC)  

- [Site server--&gt; domein controller](#BKMK_PortsSite-DC)  

- [Certificerings &lt;  -- &gt; instantie van site server uitgeven](#BKMK_PortsIssuingCA_SiteServer)  

- [Software-update punt-&gt; -Internet](#BKMK_PortsSUP-Internet)  

- [Software-update punt-&gt; -UPstream WSUS-server](#BKMK_PortsSUP-WSUS)  

- [Service verbindings punt--> Azure](#bkmk_scp-cmg)  

- [CMG-verbindings punt--> CMG-Cloud service](#bkmk_cmgcp-cmg)  

### <a name="installation-requirements-for-site-systems-that-support-internet-based-clients"></a><a name="BKMK_IBCMports"></a>Installatie vereisten voor site systemen die ondersteuning bieden voor clients op Internet

> [!Note]  
> Deze sectie is alleen van toepassing op client beheer op internet (IBCM). Het is niet van toepassing op de Cloud beheer gateway. Zie [clients op Internet beheren](../../clients/manage/manage-clients-internet.md)voor meer informatie.  

Beheer punten op internet, distributie punten die ondersteuning bieden voor clients op internet, het software-update punt en het terugval status punt gebruiken de volgende poorten voor installatie en herstel:  

- Site Server--> site systeem: RPC-eindpunt toewijzing via UDP en TCP-poort 135.  

- Site Server--> site systeem: RPC dynamische TCP-poorten  

- Site server &lt; --> site systeem: Server Message Blocks (SMB) via TCP-poort 445

Installaties van toepassingen en pakketten op distributiepunten vereisen de volgende RPC-poorten:  

- Site Server--> distributie punt: RPC-eindpunt toewijzing via UDP en TCP-poort 135

- Site Server-->-distributie punt: RPC dynamische TCP-poorten  

Gebruik IPsec voor verkeer tussen de siteserver en sitesystemen. Als u de dynamische poorten moet beperken die worden gebruikt met RPC, kunt u het micro soft RPC-configuratie programma (RPCCfg. exe) gebruiken. Gebruik het hulp programma om een beperkt aantal poorten te configureren voor deze RPC-pakketten. Zie voor meer informatie [RPC configureren voor het gebruik van bepaalde poorten en hoe u deze poorten kunt beveiligen met behulp van IPSec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]
> Voordat u deze site systemen installeert, moet u ervoor zorgen dat de externe register service wordt uitgevoerd op de site systeem server en dat u een installatie account hebt opgegeven voor het site systeem als het site systeem zich in een andere Active Directory forest bevindt zonder een vertrouwens relatie. De Remote Registry-service wordt bijvoorbeeld gebruikt op servers waarop site systemen worden uitgevoerd, zoals distributie punten (zowel pull als standaard), externe SQL-servers en de toepassingscatalogus.

### <a name="ports-used-by-configuration-manager-client-installation"></a><a name="BKMK_PortsClientInstall"></a> Poorten die worden gebruikt door de Configuration Manager-clientinstallatie

De poorten die Configuration Manager gebruikt tijdens de client installatie, zijn afhankelijk van de implementatie methode.

- Zie [poorten die worden gebruikt tijdens Configuration Manager-client implementatie](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md#ports-used-during-configuration-manager-client-deployment) voor een lijst met poorten voor elke client implementatie methode  

- Zie [Windows Firewall-en poort instellingen voor clients](../../clients/deploy/windows-firewall-and-port-settings-for-clients.md) voor meer informatie over het configureren van Windows Firewall op de client voor client installatie en communicatie na de installatie.  

### <a name="ports-used-by-migration"></a><a name="BKMK_MigrationPorts"></a> Poorten die door de migratie worden gebruikt

De site server die de migratie uitvoert, maakt gebruik van verschillende poorten om verbinding te maken met de toepasselijke sites in de bron hiërarchie. Zie [vereiste configuraties voor migratie](../../migration/prerequisites-for-migration.md#BKMK_Required_Configurations)voor meer informatie.  

### <a name="ports-used-by-windows-server"></a><a name="BKMK_ServerPorts"></a> Poorten die door Windows Server worden gebruikt

De volgende tabel bevat een aantal van de belangrijkste poorten die door Windows Server worden gebruikt.

|Beschrijving|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 en 68|--|  
|NetBIOS-naamomzetting|137|--|  
|NetBIOS Datagram-service|138|--|  
|NetBIOS-sessieservice|--|139|  
|Kerberos-verificatie|--|88|

Raadpleeg voor meer informatie de volgende artikelen:

- [Service overzicht en netwerk poort vereisten voor het Windows Server-systeem](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

- [Een firewall configureren voor domeinen en vertrouwens relaties](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)
