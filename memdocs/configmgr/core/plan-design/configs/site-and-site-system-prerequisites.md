---
title: Sitevereisten
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van een Windows-computer als een Configuration Manager-site systeem server.
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce3420a6e229b5987616c5c0c1c41d50cdc499c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700347"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Site-en site systeem vereisten voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Op Windows-computers zijn specifieke configuraties vereist ter ondersteuning van hun gebruik als Configuration Manager-site systeem servers.

Voor sommige producten, zoals Windows Server Update Services (WSUS) voor het software-update punt, moet u de product documentatie raadplegen om aanvullende vereisten en beperkingen voor gebruik te bepalen. Hier vindt u alleen configuraties die rechtstreeks van toepassing zijn op gebruik met Configuration Manager.

Zie voor meer informatie over .NET Framework [levenscyclus Veelgestelde vragen-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a> Algemene vereisten en beperkingen

De volgende vereisten zijn van toepassing op alle site systeem servers:

- Elke site systeem server moet een 64-bits besturings systeem gebruiken. De enige uitzonde ring hierop is de site systeemrol van het distributie punt, die u op sommige 32-bits besturings systemen kunt installeren.  

- Site systemen worden niet ondersteund op Server Core-installaties van elk besturings systeem. Een uitzonde ring hierop is dat Server Core-installaties worden ondersteund voor de site systeemrol van het distributie punt. Zie [ondersteunde besturings systemen voor Configuration Manager-site systeem servers](supported-operating-systems-for-site-system-servers.md)voor meer informatie.  

- Nadat een site systeem server is geïnstalleerd, wordt deze niet meer ondersteund:  

    - De domein naam van het domein waarin de site systeem computer zich bevindt (ook wel **domein naam wijzigen**genoemd).  

    - Het domein lidmaatschap van de computer.  

    - De naam van de computer.  

    Als u een van deze items wilt wijzigen, moet u eerst de site systeemrol van de computer verwijderen. Installeer de functie vervolgens opnieuw nadat de wijziging is voltooid. Voor wijzigingen die van invloed zijn op de site server, moet u eerst de site verwijderen. Installeer de site vervolgens opnieuw nadat de wijziging is voltooid.  

- Site systeem rollen worden niet ondersteund op een exemplaar van een Windows Server-cluster. De enige uitzonde ring hierop is de site database server. Zie [een SQL Server cluster gebruiken voor de Configuration Manager-site database](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)voor meer informatie.  

    Vanaf versie 1810 wordt de installatie van de site serverrol op een computer met de Windows-functie voor failover clustering niet meer geblokkeerd door het installatie proces Configuration Manager. Voor SQL always on is deze rol vereist, zodat u de site database niet kunt vinden op de site server. Met deze wijziging kunt u een Maxi maal beschik bare site met minder servers maken met behulp van SQL always on en een site server in de passieve modus. Zie [Opties voor hoge Beschik baarheid](../../servers/deploy/configure/high-availability-options.md)voor meer informatie. <!--3607761, fka 1359132-->  

- Het wordt niet ondersteund om het opstart type of de instellingen voor aanmelden als voor een Configuration Manager-service te wijzigen. Als u dat wel doet, kan het voor komen dat Key Services goed worden uitgevoerd.  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Vereisten voor Windows Server 2012 en latere besturings systemen  

Zie de belangrijkste secties in dit artikel voor de specifieke vereisten voor site systeem servers en-rollen op Windows Server 2012 en hoger:

- [Centrale beheer site en primaire site servers](#bkmk_2012sspreq)
- [Secundaire siteserver](#bkmk_2012secpreq)
- [Databaseserver](#bkmk_2012dbpreq)
- [Server van SMS-provider](#bkmk_2012smsprovpreq)
- [Application Catalog-websitepunt](#bkmk_2012acwspreq)
- [Application Catalog-webservicepunt](#bkmk_2012ACwsitepreq)
- [Synchronisatie punt Asset Intelligence](#bkmk_2012AIpreq)
- [Certificaatregistratiepunt](#bkmk_2012crppreq)
- [Distributiepunt](#bkmk_2012dppreq)
- [Endpoint Protection-punt](#bkmk_2012EPPpreq)
- [Inschrijvingspunt](#bkmk_2012Enrollpreq)
- [Proxypunt voor inschrijving](#bkmk_2012EnrollProxpreq)
- [Terugvalstatuspunt](#bkmk_2012FSPpreq)
- [Beheer punt](#bkmk_2012MPpreq)
- [Reporting Services-punt](#bkmk_2012RSpoint)
- [Serviceverbindingspunt](#bkmk_SCPpreq)
- [Software-updatepunt](#bkmk_2012SUPpreq)
- [Status migratie punt](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a> Centrale beheer site en primaire site servers

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework 3.5

- Remote Differential Compression  

- Wanneer u een software-update punt op een andere server dan de site server gebruikt, installeert u de WSUS-beheer console op de site server.

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- Voordat u een centrale beheer site of primaire site installeert of bijwerkt, moet u de versie van de Windows Assessment and Deployment Kit (ADK) installeren die vereist is voor de versie van Configuration Manager u installeert of een upgrade naar uitvoert. Zie [Windows 10 ADk](support-for-windows-10.md#windows-10-adk)(Engelstalig) voor meer informatie.  

- Zie [vereisten voor de infra structuur voor implementatie van het besturings systeem](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)voor meer informatie over deze vereiste.  

### <a name="visual-c-redistributable"></a>Te distribueren pakket Visual C++  

- Configuration Manager installeert het Herdistribueerbaar pakket voor micro soft Visual C++ 2013 op elke computer die een site server installeert.  

- Voor centrale beheer sites en primaire sites zijn zowel de x86-als de x64-versie van het betreffende herdistribueerbare bestand vereist.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a> Secundaire site server

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework 3.5

- Remote Differential Compression  

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Te distribueren pakket Visual C++

- Configuration Manager installeert het Herdistribueerbaar pakket voor micro soft Visual C++ 2013 op elke computer die een site server installeert.  

- Voor secundaire sites is alleen de x64-versie vereist.  

### <a name="default-site-system-roles"></a>Standaard site systeem rollen  

- Een secundaire site installeert standaard een **beheer punt** en een **distributie punt**.  

- Zorg ervoor dat de secundaire site server voldoet aan de vereisten voor deze site systeem rollen.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a> Database server  

### <a name="remote-registry-service"></a>Remote Registry-service  

- Schakel tijdens de installatie van de Configuration Manager-site de **Remote Registry** -service in op de computer die als host fungeert voor de site database.  

### <a name="sql-server"></a>SQL Server  

- Voordat u een centrale beheer site of primaire site installeert, moet u een ondersteunde versie van SQL Server installeren om de site database te hosten. Zie [ondersteunde versies van SQL Server](support-for-sql-server-versions.md)voor meer informatie.  

- Voordat u een secundaire site installeert, kunt u een ondersteunde versie van SQL Server installeren.  

- Als u ervoor kiest om SQL Server Express Configuration Manager te installeren als onderdeel van de installatie van de secundaire site, moet u ervoor zorgen dat de computer voldoet aan de vereisten om SQL Server Express uit te voeren.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> Server van SMS-provider  

### <a name="windows-adk"></a>Windows ADK

- Op de computer waarop u een exemplaar van de SMS-provider installeert, moet de vereiste versie van Windows ADK zijn geïnstalleerd. de versie van Configuration Manager die u installeert of waarmee u een upgrade uitvoert, is vereist. Zie [Windows 10 ADk](support-for-windows-10.md#windows-10-adk)(Engelstalig) voor meer informatie.  

- Zie [vereisten voor de infra structuur voor de implementatie van besturings systemen](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)voor meer informatie over deze vereiste.  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- Als u de [beheer service](../../../develop/adminservice/overview.md)gebruikt, is voor de server die als host fungeert voor de functie SMS-Provider .net 4,5 of hoger vereist  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Voor Configuration Manager versie 1810 is .NET 4.5.2 of later vereist.

- Webserver (IIS): elke provider probeert de [beheer service](../../../develop/adminservice/overview.md)te installeren. Deze service heeft een afhankelijkheid van IIS om een certificaat te binden aan HTTPS-poort 443. Configuration Manager gebruikt IIS Api's om deze certificaat configuratie te controleren. Als u de site configureert voor [verbeterde http](../hierarchy/enhanced-http.md), gebruikt Configuration Manager IIS api's om het door de site gegenereerde certificaat te koppelen. Vanaf versie 2002 gebruikt de site automatisch het zelfondertekende certificaat van de site.

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> Application catalog-website punt  

> [!Important]  
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-configuratie  

- Veelvoorkomende HTTP-functies:  

    - Standaarddocument  

    - Statische inhoud  

- Toepassings ontwikkeling:  

    - ASP.NET 3,5 (en automatisch geselecteerde opties)  

    - ASP.NET 4,5 (en automatisch geselecteerde opties)  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- Beveiligingsprincipal  

    - Windows-verificatie  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> Application Catalog-webservicepunt  

> [!Important]  
> De Silverlight-gebruikers ervaring van de toepassings catalogus wordt niet ondersteund vanaf de huidige branch-versie 1806. Vanaf versie 1906 gebruiken bijgewerkte clients automatisch het beheer punt voor toepassings implementaties die beschikbaar zijn voor gebruikers. U kunt ook geen nieuwe functies van de toepassings catalogus installeren. Ondersteuning voor de functies van de toepassings catalogus wordt beëindigd met versie 1910.  
>
> Raadpleeg voor meer informatie de volgende artikelen:
>
> - [Software Center configureren](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Verwijderde en afgeschafte functies](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework 3.5

- ASP.NET 4,5:  

    - HTTP-activering (en automatisch geselecteerde opties)  

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-configuratie

- Veelvoorkomende HTTP-functies:  

    - Standaarddocument  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  

- Toepassings ontwikkeling:  

    - ASP.NET 3,5 (en automatisch geselecteerde opties)  

    - .NET Extensibility 3.5  

    - ASP.NET 4,5 (en automatisch geselecteerde opties)  

    - .NET Extensibility 4.5  

### <a name="computer-memory"></a>Computer geheugen  

- De computer die als host fungeert voor deze site systeemrol moet mini maal 5% van het beschik bare geheugen van de computer hebben om de site systeemrol in staat te stellen aanvragen te verwerken.  

- Als deze site systeemrol is gekoppeld aan een andere site systeemrol die dezelfde vereiste heeft, neemt dit geheugen vereiste voor de computer niet toe, maar blijft het mini maal 5%.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a> Synchronisatie punt Asset Intelligence  

### <a name="net-framework"></a>.NET Framework

Installeer een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a> Certificaat registratiepunt  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework

    - HTTP-activering  

### <a name="net-framework"></a>.NET Framework

Installeer een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-configuratie

- Toepassings ontwikkeling:  

    - ASP.NET 3,5 (en automatisch geselecteerde opties)  

    - ASP.NET 4,5 (en automatisch geselecteerde opties)  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  

    - Compatibiliteit met IIS 6 WMI  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a> Distributiepunt  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- Remote Differential Compression  

#### <a name="iis-configuration"></a>IIS-configuratie

- Toepassings ontwikkeling:  

    - ISAPI-uitbreidingen  

- Beveiligingsprincipal  

    - Windows-verificatie  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  

    - Compatibiliteit met IIS 6 WMI  

### <a name="powershell"></a>PowerShell  

- In Windows Server 2012 of hoger is Power Shell 3,0 of 4,0 vereist voordat u het distributie punt installeert.  

### <a name="visual-c-redistributable"></a>Te distribueren pakket Visual C++

- Configuration Manager installeert het Herdistribueerbaar pakket voor micro soft Visual C++ 2013 op elke computer die als host fungeert voor een distributie punt.  

- De versie die wordt geïnstalleerd, is afhankelijk van het computer platform (x86 of x64).  

### <a name="microsoft-azure"></a>Microsoft Azure  

- U kunt een Cloud service in Microsoft Azure gebruiken om een distributie punt te hosten.  

### <a name="to-support-pxe-or-multicast"></a>Voor de ondersteuning van PXE of multi cast  

- Een PXE-Responder inschakelen op een distributie punt zonder Windows Deployment-service.  

- Installeer en configureer de Windows Server-functie Windows Deployment Services (WDS).  

    > [!NOTE]  
    > WDS wordt automatisch geïnstalleerd en geconfigureerd wanneer u een distributie punt configureert voor de ondersteuning van PXE of multi cast op een server waarop Windows Server 2012 of hoger wordt uitgevoerd.  

- Controleer voor een multi cast-distributie punt of de SQL Server Native Client is geïnstalleerd en up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.

Zie [distributie punten installeren en configureren](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)voor meer informatie.

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Wanneer het distributie punt inhoud overdraagt, wordt dit overgedragen met behulp van de **Background Intelligent Transfer service** (bits) die in Windows zijn ingebouwd. De functie van het distributie punt vereist niet dat de optionele BITS IIS-server uitbreiding wordt geïnstalleerd, omdat de client geen informatie naar de rol uploadt.  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection punt  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen  

- .NET Framework 3.5

- Windows Defender-functies (Windows Server 2016 of hoger)  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a> Inschrijvingspunt  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework 3.5

    - HTTP-activering (en automatisch geselecteerde opties)  

    - ASP.NET 4.5  

    - Windows Communication Foundation-Services (WCF)<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

> [!Note]
> Wanneer deze site systeemrol wordt geïnstalleerd, installeert Configuration Manager automatisch de .NET Framework 4.5.2. Met deze installatie kan de server de status opnieuw opstarten in behandeling hebben. Als opnieuw opstarten in behandeling is voor de .NET Framework, kunnen .NET-toepassingen mislukken totdat de server opnieuw is opgestart en de installatie is voltooid.  

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-configuratie

- Veelvoorkomende HTTP-functies:  

    - Standaarddocument  

- Toepassings ontwikkeling:  

    - ASP.NET 3,5 (en automatisch geselecteerde opties)  

    - .NET Extensibility 3.5  

    - ASP.NET 4,5 (en automatisch geselecteerde opties)  

    - .NET Extensibility 4.5  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  

### <a name="computer-memory"></a>Computer geheugen

- De computer die als host fungeert voor deze site systeemrol moet mini maal 5% van het beschik bare geheugen van de computer hebben om de site systeemrol in staat te stellen aanvragen te verwerken.  

- Als deze site systeemrol is gekoppeld aan een andere site systeemrol die dezelfde vereiste heeft, neemt dit geheugen vereiste voor de computer niet toe, maar blijft het mini maal 5%.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a> Proxypunt voor inschrijving  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

> [!Note]
> Wanneer deze site systeemrol wordt geïnstalleerd, installeert Configuration Manager automatisch de .NET Framework 4.5.2. Met deze installatie kan de server de status opnieuw opstarten in behandeling hebben. Als opnieuw opstarten in behandeling is voor de .NET Framework, kunnen .NET-toepassingen mislukken totdat de server opnieuw is opgestart en de installatie is voltooid.  

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-configuratie

- Veelvoorkomende HTTP-functies:  

    - Standaarddocument  

    - Statische inhoud  

- Toepassings ontwikkeling:  

    - ASP.NET 3,5 (en automatisch geselecteerde opties)  

    - ASP.NET 4,5 (en automatisch geselecteerde opties)  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- Beveiligingsprincipal  

    - Windows-verificatie  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  

### <a name="computer-memory"></a>Computer geheugen

- De computer die als host fungeert voor deze site systeemrol moet mini maal 5% van het beschik bare geheugen van de computer hebben om de site systeemrol in staat te stellen aanvragen te verwerken.  

- Als deze site systeemrol is gekoppeld aan een andere site systeemrol die dezelfde vereiste heeft, neemt dit geheugen vereiste voor de computer niet toe, maar blijft het mini maal 5%.  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a> Terugval status punt

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- BITS-server uitbreidingen (en automatisch geselecteerde opties) of BITS (Background Intelligent trans Services) (en automatisch geselecteerde opties)

#### <a name="iis-configuration"></a>IIS-configuratie

De standaard IIS-configuratie is vereist met de volgende toevoegingen:  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a> Beheerpunt  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- BITS-server uitbreidingen (en automatisch geselecteerde opties) of BITS (Background Intelligent trans Services) (en automatisch geselecteerde opties)  

### <a name="net-framework"></a>.NET Framework

Installeer een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-configuratie

- Toepassings ontwikkeling:  

    - ISAPI-uitbreidingen  

- Beveiligingsprincipal  

    - Windows-verificatie  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  

    - Compatibiliteit met IIS 6 WMI  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Reporting Services-punt  

### <a name="net-framework"></a>.NET Framework

Installeer een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- Installeer en configureer ten minste één exemplaar van SQL Server ter ondersteuning van SQL Server Reporting Services voordat u het rapportage punt installeert.  

- Het exemplaar dat u voor SQL Server Reporting Services gebruikt, kan hetzelfde exemplaar zijn dat u voor de site database gebruikt.  

- Bovendien kan het exemplaar dat u gebruikt met andere System Center-producten worden gedeeld, zolang de andere System Center-producten geen beperkingen hebben voor het delen van het exemplaar van SQL Server.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a> Service verbindings punt  

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

> [!Note]
> Wanneer deze site systeemrol wordt geïnstalleerd, installeert Configuration Manager automatisch de .NET Framework 4.5.2. Met deze installatie kan de server de status opnieuw opstarten in behandeling hebben. Als opnieuw opstarten in behandeling is voor de .NET Framework, kunnen .NET-toepassingen mislukken totdat de server opnieuw is opgestart en de installatie is voltooid.  

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Te distribueren pakket Visual C++

- Configuration Manager installeert het Herdistribueerbaar pakket voor micro soft Visual C++ 2013 op elke computer die als host fungeert voor een distributie punt.  

- De-site systeemrol vereist de x64-versie.  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a> Software-updatepunt  

### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework 3.5

De standaard IIS-configuratie is vereist.

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server Update Services  

- Installeer de Windows Server-functie Windows Server Update Services op een computer voordat u een software-update punt installeert.  

- Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md)voor meer informatie.  

> [!NOTE]  
> Wanneer u een software-update punt op een andere server dan de site server gebruikt, moet u de WSUS-beheer console op de site server installeren.

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> Statusmigratiepunt

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Windows Server-functies en-onderdelen

- .NET Framework 3.5

    - HTTP-activering (en automatisch geselecteerde opties)  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

Schakel de Windows-functie in voor .NET Framework 3,5.

Installeer ook een ondersteunde versie van de .NET Framework versie 4,5 of hoger. Vanaf versie 1906 ondersteunt Configuration Manager .NET Framework 4,8.

> [!Note]
> Wanneer deze site systeemrol wordt geïnstalleerd, installeert Configuration Manager automatisch de .NET Framework 4.5.2. Met deze installatie kan de server de status opnieuw opstarten in behandeling hebben. Als opnieuw opstarten in behandeling is voor de .NET Framework, kunnen .NET-toepassingen mislukken totdat de server opnieuw is opgestart en de installatie is voltooid.  

Raadpleeg de volgende artikelen voor meer informatie over .NET Framework versies:

- [Versies en afhankelijkheden .NET Framework](/dotnet/framework/migration-guide/versions-and-dependencies)
- [Veelgestelde vragen over levens cyclus-.NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS-configuratie

- Veelvoorkomende HTTP-functies:  

    - Standaarddocument  

- Toepassings ontwikkeling:  

    - ASP.NET 3,5 (en automatisch geselecteerde opties)  

    - .NET Extensibility 3.5  

    - ASP.NET 4,5 (en automatisch geselecteerde opties)  

    - .NET Extensibility 4.5  

- Compatibiliteit met IIS 6-beheer:  

    - Compatibiliteit met IIS 6-metabase  

### <a name="sql-server-native-client"></a>SQL Server Native Client

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Zorg ervoor dat dit onderdeel up-to-date is. Zie [prerequisite checks-SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)voor meer informatie.