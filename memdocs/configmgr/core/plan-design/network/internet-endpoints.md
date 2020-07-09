---
title: Vereisten voor internettoegang
titleSuffix: Configuration Manager
description: Meer informatie over de Internet-eind punten zodat u de volledige functionaliteit van Configuration Manager-functies kunt toestaan.
ms.date: 07/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 71f2a75d59af6f8d5c77e96d780e6d02352e5045
ms.sourcegitcommit: 678104677ad36b789630befdc5e0f1efc572c14b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/08/2020
ms.locfileid: "86137359"
---
# <a name="internet-access-requirements"></a>Vereisten voor internettoegang

Sommige Configuration Manager functies zijn afhankelijk van Internet connectiviteit voor volledige functionaliteit. Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u ervoor zorgen dat deze eind punten zijn toegestaan.

<!-- SCCMDocs-pr #3403 -->

Configuration Manager gebruikt de volgende micro soft URL Forwarding services in het hele product:

- `https://aka.ms`
- `https://go.microsoft.com`

Zelfs als ze niet expliciet worden vermeld in de onderstaande secties, moet u deze eind punten altijd toestaan.

## <a name="service-connection-point"></a><a name="bkmk_scp"></a>Service verbindings punt

Deze configuraties zijn van toepassing op de computer die het service aansluitpunt host en eventuele firewalls tussen die computer en Internet. Beide moeten communicatie toestaan via uitgaande poort **tcp 443** voor HTTPS en uitgaande poort **TCP 80** voor http naar de onderstaande Internet locaties.

Het service aansluitpunt ondersteunt het gebruik van een webproxy (met of zonder verificatie) voor het gebruik van deze locaties. Zie [ondersteuning voor proxy server](proxy-server-support.md)voor meer informatie.

Zie [over het service verbindings punt](../../servers/deploy/configure/about-the-service-connection-point.md)voor meer informatie over het service aansluitpunt.

Andere Configuration Manager-functies vereisen mogelijk extra eind punten van het service verbindings punt. Zie de overige secties in dit artikel voor meer informatie.

> [!TIP]  
> Het service aansluitpunt gebruikt de Microsoft Intune-service wanneer deze verbinding maakt met `go.microsoft.com` of `manage.microsoft.com` . Er is een bekend probleem waarbij de intune-connector verbindings problemen ondervindt als het basis certificaat van de Baltimore Cyber Trust niet is geïnstalleerd, is verlopen of beschadigd is op het service verbindings punt. Voor meer informatie, Zie [KB 3187516: Service verbindings punt downloadt geen updates](https://support.microsoft.com/help/3187516).  

Vanaf versie 2002, als de Configuration Manager-site geen verbinding kan maken met de vereiste eind punten voor een Cloud service, wordt een kritieke status bericht-ID 11488 gegenereerd. Wanneer er geen verbinding kan worden gemaakt met de service, wordt de status van het SMS_SERVICE_CONNECTOR onderdeel gewijzigd in kritiek. Bekijk de gedetailleerde status in het knoop punt [onderdeel status](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) van de Configuration Manager-console.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"></a>Updates en onderhoud

Zie [updates en onderhoud voor Configuration Manager](../../servers/manage/updates.md)voor meer informatie over deze functie.

> [!Tip]  
> Schakel deze eind punten in voor de [Management Insight](../../servers/manage/management-insights.md) -regel, **Verbind de site met de micro soft-Cloud voor Configuration Manager updates**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="windows-10-servicing"></a>Onderhoud van Windows 10

Zie [Windows als een service beheren](../../../osd/deploy-use/manage-windows-as-a-service.md)voor meer informatie over deze functie.

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Azure-services

Zie [Azure-Services configureren voor gebruik met Configuration Manager](../../servers/deploy/configure/azure-services-wizard.md)voor meer informatie over deze functie.

- `management.azure.com`(Open bare Azure-Cloud)
- `management.usgovcloudapi.net`(Azure-Cloud voor de Amerikaanse overheid)

## <a name="co-management"></a>Co-beheer

Als u Windows 10-apparaten inschrijft voor Microsoft Intune voor co-beheer, moet u ervoor zorgen dat deze apparaten toegang hebben tot de eind punten die vereist zijn voor intune. Zie [Network-eind punten voor Microsoft intune](https://docs.microsoft.com/intune/intune-endpoints)voor meer informatie.

## <a name="microsoft-store-for-business"></a>Microsoft Store voor bedrijven

Als u Configuration Manager integreert met de [Microsoft Store voor bedrijven](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md), moet u ervoor zorgen dat het service aansluitpunt en de doel apparaten toegang hebben tot de Cloud service. Zie [Microsoft Store voor Business proxy configureren](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration)voor meer informatie.

## <a name="delivery-optimization"></a>Delivery Optimization

Als u Delivery Optimization gebruikt, moeten clients communiceren met de Cloud service:`*.do.dsp.mp.microsoft.com`

Distributie punten die ondersteuning bieden voor micro soft Connected cache vereisen ook deze eind punten.

Raadpleeg voor meer informatie de volgende artikelen:

- [Veelgestelde vragen over Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)
- [Basis concepten voor inhouds beheer in Configuration Manager](../hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)
- [Met micro soft verbonden cache in Configuration Manager](../hierarchy/microsoft-connected-cache.md)

## <a name="cloud-services"></a><a name="bkmk_cloud"></a>Cloud Services

<!-- SCCMDocs-pr #3402 -->

In deze sectie komen de volgende functies aan bod:

- Cloud beheer gateway (CMG)
- Cloud distributiepunt (CDP)
- Integratie van Azure Active Directory (Azure AD)
- Detectie op basis van Azure AD

Zie [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md)voor meer informatie over de CMG.

De volgende secties geven een lijst van de eind punten op rol. Sommige eind punten verwijzen naar een service op `<name>` . Dit is de naam van de Cloud service van de CMG of CDP. Als uw CMG bijvoorbeeld is `GraniteFalls.CloudApp.Net` , is het werkelijke opslag eindpunt `GraniteFalls.blob.core.windows.net` .<!-- SCCMDocs#2288 -->

### <a name="service-connection-point"></a>Serviceverbindingspunt

Voor de implementatie van CMG/CDP-Services moet het service aansluitpunt toegang hebben tot:

- Specifieke Azure-eind punten zijn per omgeving verschillend, afhankelijk van de configuratie. Configuration Manager worden deze eind punten opgeslagen in de site database. Query's uitvoeren op de **AzureEnvironments** -tabel in SQL Server voor de lijst met Azure-eind punten.

- [Azure-services](#azure-services)

- Voor Azure AD-gebruikers detectie:

  - Versie 1902 en hoger: Microsoft Graph eind punt`https://graph.microsoft.com/`

  - Versie 1810 en eerder: Azure AD Graph-eind punt`https://graph.windows.net/`  

### <a name="cmg-connection-point"></a>CMG-verbindings punt

Het CMG-verbindings punt moet toegang hebben tot de volgende service-eind punten:

- Naam van Cloud service (voor CMG of CDP):
  - `<name>.cloudapp.net`(Open bare Azure-Cloud)
  - `<name>.usgovcloudapp.net`(Azure-Cloud voor de Amerikaanse overheid)

- Service Management-eind punt:`https://management.core.windows.net/`  

- Opslag eindpunt (voor CMG of CDP met ingeschakelde inhoud):
  - `<name>.blob.core.windows.net`(Open bare Azure-Cloud)
  - `<name>.blob.core.usgovcloudapi.net`(Azure-Cloud voor de Amerikaanse overheid)
<!--  and `<name>.table.core.windows.net` per DC, only used internally -->

Het site systeem van het CMG-verbindings punt ondersteunt het gebruik van een webproxy. Zie [ondersteuning voor proxy server](proxy-server-support.md#configure-the-proxy-for-a-site-system-server)voor meer informatie over het configureren van deze rol voor een proxy. Het CMG-verbindings punt hoeft alleen verbinding te maken met de CMG-service-eind punten. De service heeft geen toegang nodig tot andere Azure-eind punten.

### <a name="configuration-manager-client"></a>Configuration Manager-client

- Naam van Cloud service (voor CMG of CDP):
  - `<name>.cloudapp.net`(Open bare Azure-Cloud)
  - `<name>.usgovcloudapp.net`(Azure-Cloud voor de Amerikaanse overheid)

- Opslag eindpunt (voor CMG of CDP met ingeschakelde inhoud):
  - `<name>.blob.core.windows.net`(Open bare Azure-Cloud)
  - `<name>.blob.core.usgovcloudapi.net`(Azure-Cloud voor de Amerikaanse overheid)

- Voor het ophalen van Azure AD-tokens, het Azure AD-eind punt:
  - `login.microsoftonline.com`(Open bare Azure-Cloud)
  - `login.microsoftonline.us`(Azure-Cloud voor de Amerikaanse overheid)

### <a name="configuration-manager-console"></a>Configuration Manager-console

- Voor het ophalen van Azure AD-tokens, het Azure AD-eind punt:

  - Openbare Azure-cloud
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Azure-Cloud voor de Amerikaanse overheid
    - `login.microsoftonline.us`

## <a name="software-updates"></a><a name="bkmk_sum"></a>Software-updates

Het actieve software-update punt toestaan om toegang te krijgen tot de volgende eind punten zodat WSUS en Automatische updates kunnen communiceren met de Microsoft Update-Cloud service:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md)voor meer informatie over software-updates.

### <a name="intranet-firewall"></a>Intranet firewall

Mogelijk moet u eind punten toevoegen aan een firewall tussen twee site systemen in de volgende gevallen:

- Als onderliggende sites een software-update punt hebben
- Als er een extern actief op internet gebaseerd software-update punt op een site is

#### <a name="software-update-point-on-the-child-site"></a>Software-updatepunt op de onderliggende site

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  

## <a name="manage-office-365"></a>Office 365 beheren

> [!NOTE]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds verwijzingen naar de oude naam in de Configuration Manager-console en de ondersteunende documentatie terwijl de-console wordt bijgewerkt.

Als u Configuration Manager gebruikt voor het implementeren en bijwerken van Microsoft 365-apps voor bedrijven, moet u de volgende eind punten toestaan:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com`het software-update punt voor Microsoft 365 apps voor Enter prise-client updates synchroniseren

- `config.office.com`aangepaste configuraties voor Microsoft 365-apps maken voor bedrijfs implementaties

- `contentstorage.osi.office.net`ter ondersteuning van de evaluatie van de gereedheid voor Office-invoeg toepassingen<!-- MEMDocs#410 -->

## <a name="configuration-manager-console"></a>Configuration Manager-console

Computers met de Configuration Manager-console moeten toegang hebben tot de volgende Internet eindpunten voor specifieke functies:

### <a name="in-console-feedback"></a>Feedback in de console

- `http://petrol.office.microsoft.com`

Zie [product feedback](../../understand/find-help.md#product-feedback)voor meer informatie over deze functie.

### <a name="community-workspace"></a>Community-werk ruimte

#### <a name="documentation-node"></a>Documentatie knooppunt

Zie [de Configuration Manager-console gebruiken](../../servers/manage/admin-console.md)voor meer informatie over dit console knooppunt.

- `https://aka.ms`

- `https://raw.githubusercontent.com`

#### <a name="community-hub"></a>Community Hub

Zie [Community hub](../../servers/manage/community-hub.md)voor meer informatie over deze functie.

- `https://github.com`

- `https://communityhub.microsoft.com`

### <a name="monitoring-workspace-site-hierarchy-node"></a>Bewakings werkruimte, knoop punt site hiërarchie

Als u de **geografische weer gave**gebruikt, verleent u toegang tot het volgende eind punt:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Zie voor meer informatie over de vereiste eind punten voor de Cloud service van Desktop Analytics de optie voor het [delen van gegevens](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="tenant-attach"></a>Tenantkoppeling

Zie [Tenant koppelen inschakelen](../../../tenant-attach/device-sync-actions.md#internet-endpoints)voor meer informatie over de vereiste eind punten voor Tenant koppelings functies.

## <a name="endpoint-analytics"></a>Eindpuntanalyse

Zie voor meer informatie over de vereiste eind punten voor endpoint Analytics configuratie van de [endpoint Analytics-proxy](../../../../analytics/troubleshoot.md#bkmk_endpoints).

## <a name="asset-intelligence"></a>Asset Intelligence

<!-- memdocs#470 -->
Als u [Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)gebruikt, verleent u de volgende eind punten voor het synchroniseren van de service:

- `https://sc.microsoft.com`
- `https://ssu2.manage.microsoft.com`

## <a name="microsoft-public-ip-addresses"></a>Open bare IP-adressen van micro soft

Zie [open bare IP-adres ruimte van micro soft](https://www.microsoft.com/download/details.aspx?id=53602)voor meer informatie over de IP-adresbereiken van micro soft. Deze adressen worden regel matig bijgewerkt. Er is geen granulatie per service, elk IP-adres in deze bereiken kan worden gebruikt.

## <a name="see-also"></a>Zie ook

- [Poorten die worden gebruikt in Configuration Manager](../hierarchy/ports.md)

- [Ondersteuning van proxy server in Configuration Manager](proxy-server-support.md)
