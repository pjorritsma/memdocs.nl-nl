---
title: Controles van vereisten
titleSuffix: Configuration Manager
description: Verwijzing naar de specifieke controles van de vereisten voor Configuration Manager updates.
ms.date: 05/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2dd722ddcf0e5ea6e944a76366204ac83ede05ec
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698953"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Lijst met vereisten controles voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel worden de vereisten voor controles beschreven die worden uitgevoerd wanneer u Configuration Manager installeert of bijwerkt. Zie [prerequisite Checker](prerequisite-checker.md)voor meer informatie.  



## <a name="errors"></a>Fouten

### <a name="active-migration-mappings-on-the-target-primary-site"></a>Actieve migratietoewijzingen op de primaire doelsite

*Van toepassing op: centrale beheer site*

Er zijn geen actieve migratie toewijzingen naar primaire sites.

### <a name="active-replica-mp"></a>Actieve replica-MP

*Van toepassing op: primaire site*

Er is een actieve beheer punt replica.

### <a name="administrative-rights-on-expand-primary-site"></a>Beheer rechten op uit te breiden primaire site

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site naar een hiërarchie uitbreidt, heeft het gebruikers account dat Setup uitvoert, **beheerders** rechten op de zelfstandige primaire site server.

### <a name="administrative-rights-on-site-system"></a>Beheer rechten op site systeem

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Het gebruikers account dat Configuration Manager Setup uitvoert, heeft **beheerders** rechten op de site server.

### <a name="administrator-rights-on-central-administration-site"></a>Beheerders rechten op de centrale beheer site

*Van toepassing op: primaire site*

Het gebruikers account dat Configuration Manager Setup uitvoert, heeft **beheerders** rechten op de server van de centrale beheer site.

### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Asset Intelligence synchronisatie punt op de uitgebreide primaire site

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site uitbreidt naar een hiërarchie, wordt de rol Asset Intelligence synchronisatie punt niet geïnstalleerd op de zelfstandige primaire site.

### <a name="bits-enabled"></a>BITS ingeschakeld

*Van toepassing op: beheer punt*

Background Intelligent Transfer Service (BITS) is geïnstalleerd op het beheer punt. Deze controle kan om een van de volgende redenen mislukken:

- BITS is niet geïnstalleerd  

- Het IIS 6,0 WMI Compatibility-onderdeel voor IIS 7,0 niet is geïnstalleerd op de server of de externe IIS-host  

- Setup kan de externe IIS-instellingen niet controleren. Algemene IIS-onderdelen zijn niet geïnstalleerd op de site server.  

### <a name="case-insensitive-collation-on-sql-server"></a>Hoofdletter gevoelige sortering op SQL Server

*Van toepassing op: site database server*

De SQL Server-installatie maakt gebruik van een niet-hoofdletter gevoelige sortering, zoals **SQL_Latin1_General_CP1_CI_AS**.

### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Beheer rechten van de centrale beheer site voor de uit te breiden primaire site

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site naar een hiërarchie uitbreidt, heeft het computer account van de server van de centrale beheer site **beheerders** rechten op de zelfstandige primaire site server.

### <a name="client-version-on-management-point-computer"></a>Client versie op beheer punt computer

*Van toepassing op: beheer punt*

U installeert het beheer punt op een server waarop geen andere versie van de Configuration Manager-client is geïnstalleerd.

### <a name="cloud-management-gateway-on-the-expanded-primary-site"></a>Cloud beheer gateway op de uitgebreide primaire site

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site uitbreidt naar een hiërarchie, wordt de functie Cloud beheer gateway niet geïnstalleerd op de zelfstandige primaire site.

### <a name="connection-to-sql-server-on-central-administration-site"></a>Verbinding met SQL Server op de centrale beheer site

*Van toepassing op: primaire site*

Het gebruikers account dat Configuration Manager Setup uitvoert op de primaire site om lid te worden van een bestaande hiërarchie, heeft de rol **sysadmin** op het SQL Server-exemplaar voor de centrale beheer site.

### <a name="custom-client-agent-settings-have-nap-enabled"></a>NAP is ingeschakeld voor de aangepaste instellingen van de client agent

*Van toepassing op: centrale beheer site, primaire site*

Er zijn geen aangepaste client instellingen waarmee NAP (Network Access Protection) is ingeschakeld.

### <a name="data-warehouse-service-point-on-the-expanded-primary-site"></a>Data Warehouse-service punt op de uitgebreide primaire site

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site uitbreidt naar een hiërarchie, wordt de rol Data Warehouse-service punt niet geïnstalleerd op de zelfstandige primaire site.

### <a name="dedicated-sql-server-instance"></a>Toegewezen SQL Server exemplaar

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

U hebt een toegewezen exemplaar van SQL Server geconfigureerd om de Configuration Manager-site database te hosten.

Als de instantie door een andere site wordt gebruikt, moet u een andere instantie voor de nieuwe site selecteren. U kunt de andere site ook verwijderen of de data base ervan verplaatsen naar een andere instantie voor de SQL-Server.

### <a name="default-client-agent-settings-have-nap-enabled"></a>Voor de standaard instellingen van de client agent is NAP ingeschakeld

*Van toepassing op: centrale beheer site, primaire site*

Netwerk toegangs beveiliging (NAP) is niet ingeschakeld voor de standaard client instellingen.

### <a name="domain-membership-error"></a>Domein lidmaatschap (fout)

*Van toepassing op: centrale beheer site, primaire site, secundaire site, SMS-provider, SQL Server*

De Configuration Manager computer is lid van een Windows-domein.

### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Endpoint Protection punt op de uitgebreide primaire site

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site uitbreidt naar een hiërarchie, wordt de rol Endpoint Protection punt niet geïnstalleerd op de zelfstandige primaire site.

### <a name="existing-configuration-manager-server-components-on-server"></a>Bestaande Configuration Manager server-onderdelen op server

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Een site server of site systeemrol is niet al geïnstalleerd op de server die is geselecteerd voor site-installatie.

### <a name="existing-stand-alone-primary-site-for-version-and-site-code"></a>Bestaande zelfstandige primaire site voor versie-en site code

*Van toepassing op: centrale beheer site, primaire site*

De primaire site die u wilt uitbreiden, is een zelfstandige primaire site. Deze heeft dezelfde versie van Configuration Manager, maar een andere site code dan de centrale beheer site die moet worden geïnstalleerd.

### <a name="firewall-exception-for-sql-server"></a>Firewall-uitzonde ring voor SQL Server

*Van toepassing op: centrale beheer site, primaire site, secundaire site, beheer punt*

De Windows Firewall is uitgeschakeld of er bestaat een relevante uitzonde ring Windows Firewall voor SQL Server.

Toestaan dat Sqlservr.exe of de vereiste TCP-poorten extern toegankelijk zijn. SQL Server luistert standaard op TCP-poort 1433 en gebruikt de SQL Server Service Broker (SSB) TCP-poort 4022.

### <a name="free-disk-space-on-site-server"></a>Beschik bare schijf ruimte op site server

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Voor het installeren van de site server moet er ten minste 15 GB vrije schijf ruimte zijn. Als u de SMS-provider op dezelfde server installeert, heeft deze een extra beschik bare ruimte van 1 GB nodig.

### <a name="iis-service-running"></a>IIS-service wordt uitgevoerd

*Van toepassing op: beheer punt, distributie punt*

IIS is geïnstalleerd en wordt uitgevoerd op de server voor het beheer punt of distributie punt.

### <a name="incompatible-collection-references"></a>Niet-compatibele verzamelings verwijzingen

*Van toepassing op: centrale beheer site*

Tijdens een upgrade verwijzen verzamelingen alleen naar andere verzamelingen van hetzelfde type.

### <a name="match-collation-of-expand-primary-site"></a>Sortering van de uit te breiden primaire site vergelijken

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site naar een hiërarchie uitbreidt, heeft de site database voor de zelfstandige primaire site dezelfde sortering als de site database op de centrale beheer site.

### <a name="maximum-text-replication-size-for-sql-server-always-on-availability-groups"></a>Maximale grootte van tekst replicatie voor SQL Server AlwaysOn-beschikbaarheids groepen

*Van toepassing op: site database server*

Wanneer u SQL Server always on gebruikt, moet de instelling voor de **maximale tekst replicatie grootte** op de juiste wijze zijn geconfigureerd. Zie voor meer informatie [voorbereiden op het gebruik van SQL Server AlwaysOn-beschikbaarheids groepen met Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Microsoft Intune connector op de uitgebreide primaire site

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site uitbreidt naar een hiërarchie, wordt de rol van Microsoft Intune-connector niet geïnstalleerd op de zelfstandige primaire site.

### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>Micro soft Remote Differential Compression (RDC)-bibliotheek geregistreerd

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

De RDC-bibliotheek is geregistreerd op de Configuration Manager site server.

### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Hiermee wordt de Windows Installer versie gecontroleerd.

Wanneer deze controle mislukt, kan Setup de versie niet controleren of de geïnstalleerde versie voldoet niet aan de minimum vereiste van Windows Installer 4,5.

### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Minimale .NET Framework versie voor Configuration Manager-console

*Van toepassing op: Configuration Manager-console*

Microsoft .NET Framework 4,0 is geïnstalleerd op de computer met de Configuration Manager-console.

### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Minimale .NET Framework versie voor Configuration Manager site server

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

.NET Framework 3,5 is geïnstalleerd of ingeschakeld op de Configuration Manager site server.

### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Minimale .NET Framework versie voor de installatie van de SQL Server Express Edition voor Configuration Manager secundaire site

*Van toepassing op: secundaire site*

.NET Framework 4,0 is geïnstalleerd of ingeschakeld op de Configuration Manager secundaire site server. Deze versie is vereist door SQL Server Express.

### <a name="parent-database-collation"></a>Sortering van bovenliggende data base

*Van toepassing op: primaire site, secundaire site*

De collatie van de site database komt overeen met de sortering van de data base van de bovenliggende site. Alle sites binnen een hiërarchie moeten dezelfde databasecollatie gebruiken.

### <a name="parent-site-replication-status"></a>Replicatie status van bovenliggende site

*Van toepassing op: centrale beheer site, primaire site*

De replicatie status van de bovenliggende site is **replicatie actief** (status **125**).

### <a name="pending-system-restart"></a>Opnieuw starten van systeem in behandeling

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Voordat u het installatie programma uitvoert, moet de server opnieuw worden opgestart.

Vanaf versie 1810 is deze controle robuuster. Controleer de volgende register locaties om te controleren of de computer opnieuw wordt opgestart:<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="primary-fqdn"></a>Primaire FQDN

*Van toepassing op: centrale beheer site, primaire site, secundaire site, site database server*

De NetBIOS-naam van de computer komt overeen met de lokale hostnaam in de Fully Qualified Domain Name (FQDN).

### <a name="read-only-domain-controller"></a>Alleen-lezen domeincontroller

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Site database servers en secundaire site servers worden niet ondersteund op een alleen-lezen domein controller (RODC).

Zie het Microsoft Ondersteuning-artikel over [problemen bij het installeren van SQL Server op een domein controller](https://support.microsoft.com/help/2032911)voor meer informatie.

### <a name="required-sql-server-collation"></a>Vereiste SQL Server sortering

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Het exemplaar voor SQL Server is geconfigureerd voor het gebruik van de **SQL_Latin1_General_CP1_CI_AS** collatie.

Als de Configuration Manager-site database al is geïnstalleerd, is deze controle ook van toepassing op de data base. Zie [ondersteuning voor SQL-sortering en Unicode](/sql/relational-databases/collations/collation-and-unicode-support)voor meer informatie over het wijzigen van de SQL Server exemplaar-en database sorteringen.

Als u een Chinees besturings systeem gebruikt en ondersteuning voor GB18030 vereist, is deze controle niet van toepassing. Zie [internationale ondersteuning](../../../plan-design/hierarchy/international-support.md)voor meer informatie over het inschakelen van GB18030-ondersteuning.

### <a name="server-service-is-running"></a>De Server-service wordt uitgevoerd

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

De Server-service is gestart en wordt uitgevoerd.

### <a name="setup-source-folder"></a>Bronmap van installatie

*Van toepassing op: secundaire site*

Het computer account voor de secundaire site heeft de volgende machtigingen voor de bronmap en share van de installatie:

- **Lezen** Machtigingen voor het NTFS-bestands systeem  

- Machtigingen voor **lezen** share  

> [!Note]  
> Als u beheer shares gebruikt, bijvoorbeeld C $ en D $, moet het computer account van de secundaire site een **beheerder** op de server zijn.  

### <a name="setup-source-version"></a>Versie van installatie bron

*Van toepassing op: secundaire site*

De Configuration Manager versie in de opgegeven bronmap voor de installatie van de secundaire site komt overeen met de Configuration Manager versie van de primaire site.

### <a name="site-code-in-use"></a>Site code in gebruik

*Van toepassing op: primaire site*

De opgegeven site code wordt niet al gebruikt in de Configuration Manager-hiërarchie. Geef een unieke site code op voor deze site.

### <a name="site-server-computer-account-administrative-rights"></a>Beheer rechten computer account site server

*Van toepassing op: primaire site, site database server*

Het computer account van de site server heeft **beheerders** rechten op de SQL-Server en het beheer punt.

### <a name="site-server-fqdn-length"></a>Lengte van site server-FQDN

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

De lengte van de FQDN-naam van de site server.

### <a name="site-server-in-passive-mode-on-the-expanded-primary-site"></a>Site server in de passieve modus op de uitgebreide primaire site

*Van toepassing op: centrale beheer site*

Wanneer u een primaire site uitbreidt naar een hiërarchie, wordt de site server in de passieve modus functie niet geïnstalleerd op de zelfstandige primaire site.

### <a name="sms-provider-in-same-domain-as-site-server"></a>SMS-provider in hetzelfde domein als de site server

*Van toepassing op: SMS-provider*

Elk exemplaar van de SMS-provider bevindt zich in hetzelfde domein als de site server.

### <a name="software-update-point-in-nlb-configuration"></a>Software-update punt in NLB-configuratie

*Van toepassing op: software-update punt*

De site maakt geen gebruik van Network Load Balancing (NLB) met virtuele locaties voor actieve software-update punten.

### <a name="software-update-point-using-a-load-balancer"></a>Software-update punt met behulp van een load balancer

*Van toepassing op: software-update punt*

Configuration Manager biedt geen ondersteuning voor software-update punten op netwerk (NLB) of load balancers (HLB).

### <a name="sql-server-always-on-availability-groups"></a>SQL Server AlwaysOn-beschikbaarheidsgroepen

*Van toepassing op: site database server*

Als SQL Server always on wordt gebruikt, moet deze voldoen aan de minimum vereisten voor het hosten van een beschikbaarheids groep. Zie voor meer informatie [voorbereiden op het gebruik van SQL Server AlwaysOn-beschikbaarheids groepen met Configuration Manager](../configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="sql-server-availability-group-configured-for-readable-secondaries"></a>SQL Server beschikbaarheids groep die is geconfigureerd voor lees bare secundaire zones

*Van toepassing op: site database server*

Als SQL Server always on gebruikt, controleert u de secundaire Lees status van replica's van beschikbaarheids groepen.

### <a name="sql-server-availability-group-configured-for-manual-failover"></a>SQL Server beschikbaarheids groep is geconfigureerd voor hand matige failover

*Van toepassing op: site database server*

Wanneer u SQL Server always on gebruikt, worden de replica's van beschikbaarheids groepen geconfigureerd voor hand matige failover.

### <a name="sql-server-availability-group-replicas-on-default-instance"></a>Replica's van de beschikbaarheids groep SQL Server op het standaard exemplaar

*Van toepassing op: site database server*

Wanneer u SQL Server always on gebruikt, zijn de replica's van de beschikbaarheids groep op het standaard exemplaar.

### <a name="sql-availability-group-replicas-must-all-have-the-same-seeding-mode"></a>Replica's van de SQL-beschikbaarheids groep moeten allemaal dezelfde seeding-modus hebben

<!-- SCCMDocs-pr#3899 -->
*Van toepassing op: site database server*

Vanaf versie 1906, wanneer u SQL Server always on gebruikt, moet u replica's van beschikbaarheids groepen configureren met dezelfde [seeding-modus](/sql/database-engine/availability-groups/windows/automatic-seeding-secondary-replicas).

### <a name="sql-availability-group-replicas-must-be-healthy"></a>Replica's van de SQL-beschikbaarheids groep moeten in orde zijn

<!-- SCCMDocs-pr#3899 -->
*Van toepassing op: site database server*

Vanaf versie 1906 is de status van de beschikbaarheids groep in orde wanneer u SQL Server always on gebruikt.

### <a name="sql-server-configuration-for-site-upgrade"></a>SQL Server configuratie voor site-upgrade

*Van toepassing op: site database server*

De SQL Server voldoet aan de minimale vereisten voor site-upgrade. Zie [ondersteunde versies van SQL Server](../../../plan-design/configs/support-for-sql-server-versions.md)voor meer informatie.

### <a name="sql-server-edition"></a>SQL Server-editie

*Van toepassing op: site database server*

SQL Server op de site is niet SQL Server Express.

### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express op secundaire site

*Van toepassing op: secundaire site*

SQL Server Express kan worden geïnstalleerd op de secundaire site server.

### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server op de secundaire site server

*Van toepassing op: secundaire site*

SQL Server is geïnstalleerd op de secundaire site server. U kunt SQL Server niet installeren op een extern site systeem voor een secundaire site.

> [!Warning]  
> Deze controle is alleen van toepassing wanneer u ervoor kiest om een bestaand exemplaar van SQL Server te gebruiken.  

### <a name="sql-server-service-running-account"></a>SQL Server service-account wordt uitgevoerd

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Het aanmeldings account voor de SQL Server-service is geen lokaal gebruikers account of **lokale service**.

Configureer de SQL Server-service om een geldig domein account, **netwerk service**of **lokaal systeem**te gebruiken.

### <a name="sql-server-site-database-consistency"></a>Consistentie van de site database SQL Server

*Van toepassing op: site database server*

Controleer de consistentie van de data base.

### <a name="sql-server-sysadmin-rights"></a>SQL Server sysadmin-rechten

*Van toepassing op: site database server*

Het gebruikers account dat wordt uitgevoerd Configuration Manager Setup heeft de rol **sysadmin** op het SQL Server exemplaar dat u hebt geselecteerd voor de installatie van de site database. Deze controle mislukt ook wanneer het installatie programma geen toegang kan krijgen tot het exemplaar voor de SQL Server om machtigingen te controleren.

### <a name="sql-server-sysadmin-rights-for-reference-site"></a>SQL Server sysadmin-rechten voor referentie site

*Van toepassing op: site database server*

Het gebruikers account dat wordt uitgevoerd Configuration Manager Setup heeft de rol **sysadmin** op het SQL Server rolinstantie dat u hebt geselecteerd als referentie-site database. SQL Server **sysadmin** -rolmachtigingen zijn vereist voor het wijzigen van de site database.

### <a name="sql-server-tcp-port"></a>SQL Server TCP-poort

*Van toepassing op: site database server*

TCP is ingeschakeld voor het SQL Server-exemplaar en is ingesteld op het gebruik van een statische poort.

### <a name="sql-server-version"></a>SQL Server-versie

*Van toepassing op: site database server*

Er is een ondersteunde versie van SQL Server geïnstalleerd op de opgegeven site database server.

Zie [ondersteuning voor SQL Server-versies](../../../plan-design/configs/support-for-sql-server-versions.md)voor meer informatie.

### <a name="unsupported-os-for-configuration-manager-console"></a>Niet-ondersteund besturings systeem voor Configuration Manager-console

*Van toepassing op: Configuration Manager-console*

Installeer de Configuration Manager-console op computers die een ondersteunde versie van het besturings systeem uitvoeren.

Zie de [ondersteunde versies van het besturings systeem voor de Configuration Manager-console](../../../plan-design/configs/supported-operating-systems-consoles.md)voor meer informatie.

### <a name="unsupported-os-for-site-server"></a>Niet-ondersteund besturings systeem voor site server

*Van toepassing op: centrale beheer site, primaire site, secundaire site, Configuration Manager-console, beheer punt, distributie punt*

Op de server wordt een ondersteunde versie van het besturings systeem uitgevoerd.

Zie [ondersteunde versies van besturings systemen voor Configuration Manager-site systeem servers](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)voor meer informatie.

### <a name="unsupported-site-system-role-out-of-band-service-point"></a>Niet-ondersteunde site systeemrol: buiten-band servicepunt

*Van toepassing op: primaire site*

De site systeemrol van het buiten-band servicepunt is niet geïnstalleerd.

### <a name="unsupported-site-system-role-system-health-validation-point"></a>Niet-ondersteunde site systeemrol: systeem status validatie punt

*Van toepassing op: primaire site*

De site systeemrol System Health Validator-punt is niet geïnstalleerd.

### <a name="unsupported-upgrade-path"></a>Niet-ondersteund upgradepad

*Van toepassing op: centrale beheer site, primaire site*

Alle site servers in de hiërarchie voldoen aan de Configuration Manager minimale versie die vereist is voor de upgrade.

### <a name="usmt-installed"></a>USMT geïnstalleerd

*Van toepassing op: centrale beheer site, primaire site (alleen zelfstandig)*

Het onderdeel Hulpprogramma voor migratie van gebruikersstatus (USMT) van de Windows Assessment and Deployment Kit (ADK) voor Windows is geïnstalleerd.

### <a name="validate-fqdn-of-sql-server"></a>FQDN van SQL Server valideren

*Van toepassing op: site database server*

U hebt een geldige FQDN opgegeven voor de SQL Server computer.

### <a name="verify-central-administration-site-version"></a>De versie van de centrale beheer site controleren

*Van toepassing op: primaire site*

De centrale beheer site heeft dezelfde versie van Configuration Manager.

### <a name="verify-database-consistency"></a>Database consistentie controleren

*Van toepassing op: centrale beheer site, primaire site*

Hiermee wordt de consistentie van de site database in SQL Server gecontroleerd.  

### <a name="windows-deployment-tools-installed"></a>Windows-implementatie Hulpprogramma's geïnstalleerd

*Van toepassing op: SMS-provider*

Het onderdeel Windows-Hulpprogram Ma's voor installatie van Windows ADK is geïnstalleerd.

### <a name="windows-failover-cluster"></a>Windows-failovercluster

*Van toepassing op: site server, beheer punt, distributie punt*

De server met de rollen site server, beheer punt of distributie punt maakt geen deel uit van een Windows-cluster.

Vanaf versie 1810 wordt de installatie van de site serverrol op een computer met de Windows-functie voor failover clustering niet meer geblokkeerd door het installatie proces Configuration Manager. Voor SQL always on is deze rol vereist, zodat u de site database niet kunt vinden op de site server. Met deze wijziging kunt u een Maxi maal beschik bare site met minder servers maken met behulp van SQL always on en een site server in de passieve modus. Zie [Opties voor hoge Beschik baarheid](../configure/high-availability-options.md)voor meer informatie. <!--1359132-->  

### <a name="windows-pe-installed"></a>Windows PE geïnstalleerd

*Van toepassing op: SMS-provider*

Het onderdeel Windows Preinstallation Environment (PE) van Windows ADK is geïnstalleerd.



## <a name="warnings"></a>Waarschuwingen

### <a name="active-directory-domain-functional-level"></a>Functionaliteits niveau van Active Directory domein

*Van toepassing op: centrale beheer site, primaire site*

Het functionaliteits niveau van het Active Directory domein en het forest is mini maal Windows Server 2008 R2. Zie [ondersteuning voor Active Directory domeinen](../../../plan-design/configs/support-for-active-directory-domains.md)voor meer informatie.

### <a name="administrative-rights-on-distribution-point"></a>Beheer rechten op distributie punt

*Van toepassing op: distributie punt*

Het gebruikers account waarmee de installatie wordt uitgevoerd, heeft **beheerders** rechten op het distributie punt.

### <a name="administrative-rights-on-management-point"></a>Beheer rechten op beheer punt

*Van toepassing op: beheer punt, distributie punt*

Het computer account van de site server heeft **beheerders** rechten op het beheer punt en distributie punt.

### <a name="administrative-share-site-system"></a>Beheer share (site systeem)

*Van toepassing op: beheer punt*

De vereiste beheer shares zijn aanwezig op de site systeem computer.

### <a name="application-compatibility"></a>Compatibiliteit van toepassingen

*Van toepassing op: centrale beheer site, primaire site*

Huidige toepassingen zijn compatibel met het toepassings schema.

### <a name="backlogged-inboxes"></a>Post vakken voor achterstand

*Van toepassing op: centrale beheer site, primaire site*

De site server verwerkt de kritieke post vakken op tijd. Post vakken bevatten geen bestanden die ouder zijn dan één dag.

Hiermee worden de volgende mappen in het postvak in gecontroleerd:

- `despoolr.box\receive\*.i??`

- `despoolr.box\receive\*.s??`

- `despoolr.box\receive\*.nil`

- `schedule.box\requests\*.sr?`

Om deze waarschuwing op te lossen, controleert u of de site systeem onderdelen van despooler en scheduler worden uitgevoerd.

### <a name="bits-installed"></a>BITS geïnstalleerd

*Van toepassing op: beheer punt*

De Background Intelligent Transfer Service (BITS) is geïnstalleerd en ingeschakeld in IIS.

### <a name="check-if-the-site-uses-upgrade-readiness-cloud-service-connector"></a>Controleren of de site gebruikmaakt van Upgradegereedheid-Cloud service-connector

*Van toepassing op: centrale beheer site, primaire site*

De Upgradegereedheid-service wordt vanaf 31 januari 2020 buiten gebruik gesteld. Zie [KB 4521815: Windows Analytics is buiten gebruik gesteld op 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement)voor meer informatie.

Desktop Analytics is de ontwikkeling van Windows Analytics. Zie [Wat is Desktop Analytics](../../../../desktop-analytics/overview.md)? voor meer informatie.

Als uw Configuration Manager-site verbinding heeft met Upgradegereedheid, moet u deze verwijderen en clients opnieuw configureren. Zie [Upgradegereedheid-verbinding verwijderen](../../../clients/manage/upgrade-readiness.md#bkmk_remove)voor meer informatie.

Als u deze waarschuwing over de vereiste negeert, wordt de Upgradegereedheid-connector automatisch door Configuration Manager Setup verwijderd.<!-- #4898 -->

### <a name="cloud-management-gateway-requires-either-token-based-authentication-or-an-https-management-point"></a>Voor Cloud beheer gateway is verificatie op basis van tokens of een HTTPS-beheer punt vereist

*Van toepassing op: Cloud beheer gateway*

Met sommige versies van Configuration Manager kunt u geen HTTP-beheer punt gebruiken met de CMG (Cloud Management Gateway). Configureer de CMG voor HTTPS of configureer de site voor verbeterde HTTP. Zie voor meer informatie [plannen voor Cloud beheer gateway](../../../clients/manage/cmg/plan-cloud-management-gateway.md).

### <a name="configuration-for-sql-server-memory-usage"></a>Configuratie voor het gebruik van SQL Server geheugen

*Van toepassing op: site database server*

SQL Server is geconfigureerd voor onbeperkt geheugen gebruik. Configureer SQL Server geheugen voor een maximum limiet.

### <a name="distribution-point-package-version"></a>Pakket versie distributie punt

*Van toepassing op: distributie punten*

Alle distributie punten op de site hebben de nieuwste versie van software distribution packages.

### <a name="domain-membership-warning"></a>Domein lidmaatschap (waarschuwing)

*Van toepassing op: beheer punt, distributie punt*

De Configuration Manager computer is lid van een Windows-domein.

### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Firewall-uitzonde ring voor SQL Server (zelfstandige primaire site)

*Van toepassing op: primaire site (alleen zelfstandig)*

De Windows Firewall is uitgeschakeld of er bestaat een relevante Windows Firewall uitzonde ring voor SQL Server.

Toestaan dat Sqlservr.exe of de vereiste TCP-poorten extern toegankelijk zijn. SQL Server luistert standaard op TCP-poort 1433 en maakt gebruik van TCP-poort 4022 op de Server Service Broker (SSB).

### <a name="firewall-exception-for-sql-server-for-management-point"></a>Firewall-uitzonde ring voor SQL Server voor beheer punt

*Van toepassing op: beheer punt*

De Windows Firewall is uitgeschakeld of er bestaat een relevante Windows Firewall uitzonde ring voor SQL Server.

### <a name="iis-https-configuration"></a>IIS HTTPS-configuratie

*Van toepassing op: beheer punt, distributie punt*

De IIS-website heeft bindingen voor het HTTPS-communicatie protocol.

Wanneer u site rollen installeert die HTTPS vereisen, configureert u IIS-site bindingen op de opgegeven server met een geldig PKI-certificaat (Public Key Infrastructure).

### <a name="invalid-discovery-records"></a>Ongeldige detectie records

*Van toepassing op: centrale beheer site*

Er zijn detectie records die niet meer geldig zijn. Deze records worden gemarkeerd voor verwijdering.

### <a name="microsoft-xml-core-services-60-msxml60"></a>Micro soft XML Core Services 6,0 (MSXML60)

*Van toepassing op de centrale beheer site, primaire site, secundaire site, Configuration Manager-console, beheer punt, distributie punt*

Controleert of MSXML 6,0 of een latere versie is geïnstalleerd.

### <a name="network-access-protection-nap-is-no-longer-supported"></a>Netwerk toegangs beveiliging (NAP) wordt niet meer ondersteund

*Van toepassing op: primaire site*

Er zijn geen software-updates die zijn ingeschakeld voor NAP.

### <a name="ntfs-drive-on-site-server"></a>NTFS-station op site server

*Van toepassing op: primaire site*

Het schijf station is geformatteerd met het NTFS-bestands systeem. Voor betere beveiliging installeert u Site Server onderdelen op schijf stations die zijn geformatteerd met het NTFS-bestands systeem.

### <a name="pending-configuration-item-policy-updates"></a><a name="bkmk_pending-policy"></a> Updates van beleid voor configuratie-items in behandeling

<!--SCCMDocs-pr issue 2814-->

*Van toepassing op: primaire site*

Vanaf versie 1806, als u een update uitvoert van versie 1706 of hoger, ziet u mogelijk deze waarschuwing als u veel toepassings implementaties hebt en ten minste één van de toepassingen moet worden goedgekeurd.

U hebt hiervoor twee opties:  

- Negeer de waarschuwing en ga door met de update. Deze actie veroorzaakt een hogere verwerking op de site server tijdens de update tijdens het verwerken van het beleid. Na de update ziet u mogelijk ook meer processor belasting op het beheer punt.  

- Herzie een van de toepassingen die geen vereisten of een specifieke vereiste voor het besturings systeem hebben. Verwerk een deel van de belasting op de site server op dat moment vooraf. Controleer **objreplmgr. log**en controleer de processor op het beheer punt. Wanneer de verwerking is voltooid, werkt u de site bij. Na de update is er nog steeds extra verwerking mogelijk, maar minder dan wanneer u de waarschuwing met de eerste optie negeert.  

### <a name="pending-system-restart-on-the-remote-sql-server"></a>Opnieuw opstarten van systeem in behandeling op de externe SQL Server

*Van toepassing op: versie 1902 en hoger, externe SQL Server*

Voordat u het installatie programma uitvoert, moet de server opnieuw worden opgestart.

Controleer de volgende register locaties om te controleren of de computer opnieuw wordt opgestart:<!--SCCMDocs-pr issue 3377-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  

- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  

- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  

- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

### <a name="powershell-20-on-site-server"></a>Power Shell 2,0 op site server

*Van toepassing op: primaire site met Exchange connector*

Windows Power Shell 2,0 of een latere versie is geïnstalleerd op de site server voor de Configuration Manager Exchange-connector.

### <a name="remote-connection-to-wmi-on-secondary-site"></a>Externe verbinding naar WMI op secundaire site

*Van toepassing op: secundaire site*

Setup kan een externe verbinding tot stand brengen met WMI op de secundaire site server.

### <a name="schema-extensions"></a>Schema-uitbreidingen

*Van toepassing op: centrale beheer site, primaire site*

Het Active Directory schema is uitgebreid. Als deze is uitgebreid, is dit de versie van de schema-uitbrei dingen die zijn gebruikt.

Configuration Manager vereist geen Active Directory schema-uitbrei dingen voor de installatie van de site server. Micro soft raadt hen aan om alle Configuration Manager functies volledig te gebruiken. Zie [Active Directory voorbereiden voor het publiceren van sites](../../../plan-design/network/extend-the-active-directory-schema.md)voor meer informatie over de voor delen van het schema.

### <a name="share-name-in-package"></a>Share naam in pakket

*Van toepassing op: centrale beheer site, primaire site*

Pakketten bevatten ongeldige tekens in de share naam, zoals `#` .

### <a name="site-system-to-sql-server-communication"></a>Communicatie tussen site systeem en SQL Server

*Van toepassing op: secundaire site, beheer punt*

Het account dat u hebt geconfigureerd voor het uitvoeren van de SQL Server-service voor het exemplaar van de site database, heeft een geldige Service Principal Name (SPN) in Active Directory Domain Services. Registreer een geldige SPN in Active Directory ter ondersteuning van Kerberos-verificatie.

### <a name="sql-server-change-tracking-cleanup"></a><a name="bkmk_changetracking"></a> SQL Server opschonen van wijzigingen bijhouden

*Van toepassing op: site database server*

Start in versie 1810, Controleer of de site database een achterstand heeft voor het bijhouden van SQL-wijzigingen.<!--SCCMDocs-pr issue 3023-->  

U moet deze controle hand matig controleren door een opgeslagen diagnostische procedure uit te voeren in de site database. Maak eerst een [Diagnostische verbinding](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) met uw site database. De eenvoudigste methode is om de query-editor van de data base engine van SQL Server Management Studio te gebruiken en verbinding te maken met `admin:<instance name>` .

Voer de volgende opdrachten uit in een exclusieve beheerders verbindings venster:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

Afhankelijk van de grootte van uw data base en de grootte van de achterstand, kan deze opgeslagen procedure binnen enkele minuten of enkele uren worden uitgevoerd. Wanneer de query is voltooid, ziet u twee delen van gegevens met betrekking tot de achterstand. Kijk eerst naar **CT_Days_Old**. Met deze waarde krijgt u de leeftijd (dagen) van de oudste vermelding in uw syscommittab-tabel. Deze moet vijf dagen zijn. Dit is de Configuration Manager standaard waarde. Wijzig deze standaard waarde niet. Bij een zware gegevens verwerking of-replicatie kan de oudste vermelding in syscommittab langer zijn dan vijf dagen. Als deze waarde hoger is dan zeven dagen, voert u een hand matige opschoning van de gegevens voor het bijhouden van wijzigingen uit.  

Als u de gegevens voor het bijhouden van wijzigingen wilt opschonen, voert u de volgende opdracht uit in de toegewezen beheer verbinding:

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Met deze opdracht start u een opschoning van syscommittab en alle bijbehorende tabellen. Het kan in enkele minuten of enkele uren worden uitgevoerd. Als u de voortgang wilt bewaken, moet u de weer gave van de **Vlogs** opvragen. Voer de volgende query uit om de huidige voortgang te bekijken:

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

### <a name="sql-server-native-client"></a>SQL Server Native Client

<!--SCCMDocs-pr issue 3094-->

Wanneer u een nieuwe site installeert, installeert Configuration Manager automatisch SQL Server Native Client als een herdistribueerbaar onderdeel. Nadat de site is geïnstalleerd, wordt Configuration Manager SQL Server Native Client niet bijgewerkt. Het bijwerken van de SQL Server Native Client moet mogelijk opnieuw worden opgestart, wat van invloed kan zijn op het installatie proces van de site.

Met deze controle wordt gecontroleerd of de site server een ondersteunde versie van de SQL Native Client heeft. Met de controle van vereisten wordt niet gecontroleerd of de versie van de SQL Native Client op externe site systemen.

De minimale versie is SQL 2012 SP4 ( `11.*.7001.0` ). Deze SQL Native Client-versie ondersteunt TLS 1,2. Raadpleeg voor meer informatie de volgende artikelen:

- [TLS 1,2-ondersteuning voor Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)  

- [TLS 1,2 inschakelen voor Configuration Manager](../../../plan-design/security/enable-tls-1-2.md)  

Configuration Manager gebruikt SQL Server Native Client op de volgende site systeem rollen:<!-- SCCMDocs issue 1150 -->

- Sitedatabaseserver
- Site Server: centrale beheer site, primaire site of secundaire site
- Beheerpunt
- Apparaatbeheerpunt
- Statusmigratiepunt
- SMS-provider
- Software-updatepunt
- Multicast-distributiepunt
- Asset Intelligence Service punt bijwerken
- Reporting Services-punt
- Application Catalog-webservice
- Inschrijvingspunt
- Endpoint Protection-punt
- Serviceverbindingspunt
- Certificaatregistratiepunt
- Data Warehouse-service punt

### <a name="sql-server-process-memory-allocation"></a>Geheugen toewijzing SQL Server proces

*Van toepassing op: site database server*

SQL Server reserveert mini maal 8 GB aan geheugen voor de centrale beheer site en primaire site, en mini maal 4 GB geheugen voor de secundaire site.

Zie [geheugen opties configureren met SQL Server Management Studio](/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-)voor meer informatie.

> [!NOTE]  
> Deze controle is niet van toepassing op SQL Server Express op een secundaire site. Deze editie is beperkt tot 1 GB gereserveerd geheugen.  

### <a name="sql-server-security-mode"></a>Beveiligings modus SQL Server

*Van toepassing op: site database server*

SQL Server is geconfigureerd voor Windows-verificatie beveiliging.

### <a name="unsupported-site-system-os-version-for-upgrade"></a>Niet-ondersteunde besturingssysteem versie van het site systeem voor upgrade

*Van toepassing op: primaire site, secundaire site*

Site systeem rollen, met uitzonde ring van distributie punten, worden geïnstalleerd op servers met Windows Server 2012 of hoger.

Zie [ondersteunde besturings systemen voor Configuration Manager-site systeem servers](../../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)voor meer informatie.

> [!NOTE]  
> Deze controle kan de status niet omzetten van de site systeem rollen die zijn geïnstalleerd in azure of voor de Cloud opslag die wordt gebruikt door Microsoft Intune. Waarschuwingen voor deze rollen negeren als fout-positief.

### <a name="upgrade-assessment-toolkit-is-unsupported"></a>Upgrade Assessment Toolkit wordt niet ondersteund

*Van toepassing op: centrale beheer site, primaire site*

De upgrade Assessment Toolkit is niet geïnstalleerd. Zie [verwijderde en afgeschafte functies](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.

### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Site Server machtigingen voor publiceren naar Active Directory controleren

*Van toepassing op: centrale beheer site, primaire site, secundaire site*

Het computer account voor de site server heeft machtigingen voor **volledig beheer** voor de **System Management** -container in het Active Directory domein.

Zie [Active Directory voorbereiden voor het publiceren van sites](../../../plan-design/network/extend-the-active-directory-schema.md)voor meer informatie.

> [!NOTE]  
> Als u de machtigingen hand matig verifieert, kunt u deze waarschuwing negeren.

### <a name="windows-remote-management-winrm-v11"></a>Windows Remote Management (WinRM) v 1.1

*Van toepassing op: primaire site, Configuration Manager-console*

WinRM 1,1 is geïnstalleerd op de primaire site server of de Configuration Manager-console computer om de out-of-band-beheer console uit te voeren.

WinRM wordt automatisch geïnstalleerd met alle versies van Windows die momenteel worden ondersteund. Zie [installatie en configuratie voor Windows Remote Management](/windows/win32/winrm/installation-and-configuration-for-windows-remote-management)voor meer informatie.

### <a name="wsus-on-site-server"></a>WSUS op site server

*Van toepassing op: centrale beheer site, primaire site*

Er is een ondersteunde versie van Windows Server Update Services (WSUS) geïnstalleerd op de site server.

Wanneer u een software-update punt op een andere server dan de site server gebruikt, moet u de WSUS-beheer console op de site server installeren. Zie [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus)voor meer informatie over WSUS.