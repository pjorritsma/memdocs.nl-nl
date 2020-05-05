---
title: Vereisten voor internettoegang
titleSuffix: Configuration Manager
description: Meer informatie over de Internet-eind punten zodat u de volledige functionaliteit van Configuration Manager-functies kunt toestaan.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58afaf564a8afaba4569755575fcc7c1757c5529
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110131"
---
# <a name="internet-access-requirements"></a>Vereisten voor internettoegang

Sommige Configuration Manager functies zijn afhankelijk van Internet connectiviteit voor volledige functionaliteit. Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u ervoor zorgen dat deze eind punten zijn toegestaan.

<!-- SCCMDocs-pr #3403 -->

## <a name="service-connection-point"></a><a name="bkmk_scp"></a>Service verbindings punt

Deze configuraties zijn van toepassing op de computer die het service aansluitpunt host en eventuele firewalls tussen die computer en Internet. Beide moeten communicatie toestaan via uitgaande poort **tcp 443** voor HTTPS en uitgaande poort **TCP 80** voor http naar de onderstaande Internet locaties.

Het service aansluitpunt ondersteunt het gebruik van een webproxy (met of zonder verificatie) voor het gebruik van deze locaties. Zie [ondersteuning voor proxy server](proxy-server-support.md)voor meer informatie.

Zie [over het service verbindings punt](../../servers/deploy/configure/about-the-service-connection-point.md)voor meer informatie over het service aansluitpunt.

Andere Configuration Manager-functies vereisen mogelijk extra eind punten van het service verbindings punt. Zie de overige secties in dit artikel voor meer informatie.

> [!TIP]  
> Het service aansluitpunt gebruikt de Microsoft Intune-service wanneer deze `go.microsoft.com` verbinding `manage.microsoft.com`maakt met of. Er is een bekend probleem waarbij de intune-connector verbindings problemen ondervindt als het basis certificaat van de Baltimore Cyber Trust niet is geïnstalleerd, is verlopen of beschadigd is op het service verbindings punt. Voor meer informatie, Zie [KB 3187516: Service verbindings punt downloadt geen updates](https://support.microsoft.com/help/3187516).  

Vanaf versie 2002, als de Configuration Manager-site geen verbinding kan maken met de vereiste eind punten voor een Cloud service, wordt een kritieke status bericht-ID 11488 gegenereerd. Wanneer er geen verbinding kan worden gemaakt met de service, wordt de status van het SMS_SERVICE_CONNECTOR onderdeel gewijzigd in kritiek. Bekijk de gedetailleerde status in het knoop punt [onderdeel status](../../servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) van de Configuration Manager-console.<!-- 5566763 -->

### <a name="updates-and-servicing"></a><a name="bkmk_scp-updates"/>Updates en onderhoud

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

- `management.azure.com`  

## <a name="co-management"></a>Co-beheer

Als u Windows 10-apparaten inschrijft voor Microsoft Intune voor co-beheer, moet u ervoor zorgen dat deze apparaten toegang hebben tot de eind punten die vereist zijn voor intune. Zie [Network-eind punten voor Microsoft intune](https://docs.microsoft.com/intune/intune-endpoints)voor meer informatie.

## <a name="microsoft-store-for-business"></a>Microsoft Store voor bedrijven

Als u Configuration Manager integreert met de [Microsoft Store voor bedrijven](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md), moet u ervoor zorgen dat het service aansluitpunt en de doel apparaten toegang hebben tot de Cloud service. Zie [Microsoft Store voor Business proxy configureren](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration)voor meer informatie.

## <a name="cloud-services"></a><a name="bkmk_cloud"></a>Cloud Services

<!-- SCCMDocs-pr #3402 -->

In deze sectie komen de volgende functies aan bod:

- Cloud beheer gateway (CMG)
- Cloud distributiepunt (CDP)
- Integratie van Azure Active Directory (Azure AD)
- Detectie op basis van Azure AD

Voor de implementatie van CMG/CDP-Services moet het **service aansluitpunt** toegang hebben tot:

- Specifieke Azure-eind punten zijn per omgeving verschillend, afhankelijk van de configuratie. Configuration Manager worden deze eind punten opgeslagen in de site database. Query's uitvoeren op de **AzureEnvironments** -tabel in SQL Server voor de lijst met Azure-eind punten.  

Het **CMG-verbindings punt** moet toegang hebben tot de volgende service-eind punten:

- Service Management-eind punt:`https://management.core.windows.net/`  

- Opslag eindpunt: `<name>.blob.core.windows.net` en`<name>.table.core.windows.net`

    Waar `<name>` de naam is van de Cloud service van uw CMG of CDP. Als uw CMG bijvoorbeeld is `GraniteFalls.CloudApp.Net`, dan is het eerste opslag eindpunt dat is `GraniteFalls.blob.core.windows.net`toegestaan.<!-- SCCMDocs#2288 -->

Voor het ophalen van Azure AD-tokens door de **Configuration Manager-console** en- **client**:

- ActiveDirectoryEndpoint`https://login.microsoftonline.com/`  

Voor Azure AD-gebruikers detectie moet het **service verbindings punt** toegang hebben tot:

- Versie 1810 en eerder: Azure AD Graph-eind punt`https://graph.windows.net/`  

- Versie 1902 en hoger: Microsoft Graph eind punt`https://graph.microsoft.com/`

Het site systeem van het CMG-verbindings punt (Cloud Management Point) ondersteunt het gebruik van een webproxy. Zie [ondersteuning voor proxy server](proxy-server-support.md#configure-the-proxy-for-a-site-system-server)voor meer informatie over het configureren van deze rol voor een proxy. Het CMG-verbindings punt hoeft alleen verbinding te maken met de CMG-service-eind punten. De service heeft geen toegang nodig tot andere Azure-eind punten.

Zie [plan for CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md)voor meer informatie over de CMG.

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

## <a name="configuration-manager-console"></a>Configuration Manager-console

Computers met de Configuration Manager-console moeten toegang hebben tot de volgende Internet eindpunten voor specifieke functies:

### <a name="in-console-feedback"></a>Feedback in de console

- `http://petrol.office.microsoft.com`

Zie [product feedback](../../understand/find-help.md#product-feedback)voor meer informatie over deze functie.

### <a name="community-workspace-documentation-node"></a>Community-werk ruimte, documentatie knooppunt

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Zie [de Configuration Manager-console gebruiken](../../servers/manage/admin-console.md)voor meer informatie over dit console knooppunt.

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Bewakings werkruimte, knoop punt site hiërarchie

Als u de **geografische weer gave**gebruikt, verleent u toegang tot het volgende eind punt:

- `http://maps.bing.com`

## <a name="desktop-analytics"></a>Desktop Analytics

Zie voor meer informatie over de vereiste eind punten voor de Cloud service van Desktop Analytics de optie voor het [delen van gegevens](../../../desktop-analytics/enable-data-sharing.md#endpoints).

## <a name="microsoft-public-ip-addresses"></a>Open bare IP-adressen van micro soft

Zie [open bare IP-adres ruimte van micro soft](https://www.microsoft.com/download/details.aspx?id=53602)voor meer informatie over de IP-adresbereiken van micro soft. Deze adressen worden regel matig bijgewerkt. Er is geen granulatie per service, elk IP-adres in deze bereiken kan worden gebruikt.

## <a name="see-also"></a>Zie ook

- [Poorten die worden gebruikt in Configuration Manager](../hierarchy/ports.md)

- [Ondersteuning van proxy server in Configuration Manager](proxy-server-support.md)
