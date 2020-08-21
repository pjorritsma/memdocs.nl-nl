---
title: Gebruikte accounts
titleSuffix: Configuration Manager
description: De Windows-groepen,-accounts en SQL-objecten identificeren en beheren die worden gebruikt in Configuration Manager.
ms.date: 05/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 17c22027ffc28f2e04e95b8223de27b8f26489fd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698483"
---
# <a name="accounts-used-in-configuration-manager"></a>Accounts die worden gebruikt in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de volgende informatie om de Windows-groepen, accounts en SQL-objecten te identificeren die worden gebruikt in Configuration Manager, hoe ze worden gebruikt en eventuele vereisten.  

- [Windows-groepen die worden gemaakt en gebruikt met Configuration Manager](#bkmk_groups)  
  - [Configuratie Manager_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [Configuratie Manager_DViewAccess](#configmgr_dviewaccess)  
  - [Gebruikers met beheer op afstand Configuration Manager](#configmgr_rcusers)  
  - [SMS Admins](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_ &lt; site code\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_ &lt; site code\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_ &lt; site code\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_ &lt; site code\>](#bkmk_filerepl)  

- [Accounts die worden gebruikt met Configuration Manager](#bkmk_accounts)
  - [Account voor detectie van Active Directory-groep](#active-directory-group-discovery-account)  
  - [Account voor Active Directory systeem detectie](#active-directory-system-discovery-account)  
  - [Gebruikers detectie account Active Directory](#active-directory-user-discovery-account)  
  - [Active Directory-forest-account](#active-directory-forest-account)  
  - [Account voor het certificaat registratiepunt](#certificate-registration-point-account)  
  - [Account voor installatie kopie van besturings systeem vastleggen](#capture-os-image-account)  
  - [Account voor push-client installatie](#client-push-installation-account)  
  - [Verbindings account voor inschrijvings punt](#enrollment-point-connection-account)  
  - [Exchange Server-verbindings account](#exchange-server-connection-account)  
  - [Verbindings account beheer punt](#management-point-connection-account)  
  - [Multicast verbindings account](#multicast-connection-account)  
  - [Netwerktoegangsaccount](#network-access-account)  
  - [Pakket toegangs account](#package-access-account)  
  - [Account van Reporting Services-punt](#reporting-services-point-account)  
  - [Toegestane Viewer accounts voor externe hulpprogram ma's](#remote-tools-permitted-viewer-accounts)  
  - [Site-installatie account](#site-installation-account)
  - [Installatie account site systeem](#site-system-installation-account)  
  - [Proxy Server account van site systeem](#site-system-proxy-server-account)  
  - [SMTP-server verbindings account](#smtp-server-connection-account)  
  - [Verbindings account software-update punt](#software-update-point-connection-account)  
  - [Bron site account](#source-site-account)  
  - [Bron site database account](#source-site-database-account)  
  - [Lidmaatschaps account voor taken reeks domein](#task-sequence-domain-join-account)  
  - [Verbindings account voor taken reeks netwerk mappen](#task-sequence-network-folder-connection-account)  
  - [Uitvoeren als-account voor taken reeks](#task-sequence-run-as-account)  

- [Gebruikers objecten die door Configuration Manager worden gebruikt in SQL](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Database rollen die door Configuration Manager worden gebruikt in SQL](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a> Windows-groepen die Configuration Manager maken en gebruiken  

Configuration Manager maakt automatisch en in veel gevallen worden de volgende Windows-groepen automatisch bijgehouden:  

> [!NOTE]  
> Wanneer Configuration Manager een groep maakt op een computer die lid is van een domein, is de groep een lokale beveiligings groep. Als de computer een domein controller is, is de groep een domeingebonden groep. Dit type groep wordt gedeeld tussen alle domein controllers in het domein.  


### <a name="configuration-manager_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a> Configuratie Manager_CollectedFilesAccess

Configuration Manager gebruikt deze groep om toegang te verlenen voor het weer geven van bestanden die zijn verzameld door software-inventarisatie.  

Zie [Inleiding tot software-inventarisatie](../../clients/manage/inventory/introduction-to-software-inventory.md)voor meer informatie.

#### <a name="type-and-location"></a>Type en locatie
Deze groep is een lokale beveiligingsgroep die op de primaire siteserver is gemaakt.

Wanneer u een site verwijdert, wordt deze groep niet automatisch verwijderd. Verwijder deze hand matig nadat u een site hebt verwijderd.

#### <a name="membership"></a>Lidmaatschap
Configuration Manager beheert automatisch het groepslid maatschap. De leden zijn onder andere beheerders aan wie de machtiging **Verzamelde bestanden weergeven** is verleend op het beveiligbare object **Verzameling** van een toegewezen beveiligingsrol.

#### <a name="permissions"></a>Machtigingen
Deze groep heeft standaard **Lees** machtiging voor de volgende map op de site server: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configuration-manager_dviewaccess"></a><a name="configmgr_dviewaccess"></a>Configuratie Manager_DViewAccess  

Deze groep is een lokale beveiligings groep die Configuration Manager maakt op de site database server of de data base-replica server voor een onderliggende primaire site. De site maakt deze wanneer u gedistribueerde weer gaven gebruikt voor database replicatie tussen sites in een hiërarchie. Het bevat de site server en SQL Server computer accounts van de centrale beheer site.

Zie [gegevens overdracht tussen sites](data-transfers-between-sites.md)voor meer informatie.


### <a name="configuration-manager-remote-control-users"></a><a name="configmgr_rcusers"></a> Gebruikers met beheer op afstand Configuration Manager  

Configuration Manager externe hulpprogram ma's deze groep gebruiken om de accounts en groepen op te slaan die u hebt ingesteld in de lijst met **toegestane viewers** . De site wijst deze lijst toe aan elke client.  

Zie [Inleiding tot beheer op afstand](../../clients/manage/remote-control/introduction-to-remote-control.md)voor meer informatie.

#### <a name="type-and-location"></a>Type en locatie
Deze groep is een lokale beveiligings groep die is gemaakt op de Configuration Manager-client wanneer de client een beleid ontvangt dat externe hulpprogram ma's mogelijk maakt.

Nadat u externe hulpprogram ma's voor een client hebt uitgeschakeld, wordt deze groep niet automatisch verwijderd. Verwijder deze hand matig nadat u externe hulpprogram ma's hebt uitgeschakeld.

#### <a name="membership"></a>Lidmaatschap
Standaard behoren er geen leden tot deze groep. Wanneer u gebruikers aan de lijst met **toegestane viewers** toevoegt, worden ze automatisch aan deze groep toegevoegd.

U kunt de lijst met **toegestane viewers** gebruiken om het lidmaatschap van deze groep te beheren in plaats van gebruikers of groepen rechtstreeks aan deze groep toe te voegen.

Een gebruiker met beheerders rechten heeft niet alleen een toegestane viewer, maar moet beschikken over de machtiging beheer op **afstand** voor het object **verzameling** . Wijs deze machtiging toe met behulp van de beveiligingsrol **operator voor externe Hulpprogram ma's** .  

#### <a name="permissions"></a>Machtigingen
Deze groep heeft standaard geen machtigingen voor locaties op de computer. Deze wordt alleen gebruikt om de lijst met **toegestane viewers** te bewaren.  


### <a name="sms-admins"></a>SMS Admins  

Configuration Manager gebruikt deze groep om toegang te verlenen tot de SMS-provider via WMI. Toegang tot de SMS-provider is vereist om objecten in de Configuration Manager-console weer te geven en te wijzigen.  

> [!NOTE]  
> De op rollen gebaseerde beheer configuratie van een gebruiker met beheerders rechten bepaalt welke objecten ze kunnen bekijken en beheren wanneer ze de Configuration Manager-console gebruiken.  

Zie [de SMS-provider plannen](plan-for-the-sms-provider.md)voor meer informatie.

#### <a name="type-and-location"></a>Type en locatie
Deze groep is een lokale beveiligings groep die is gemaakt op elke computer met een SMS-provider. 

Wanneer u een site verwijdert, wordt deze groep niet automatisch verwijderd. Verwijder deze hand matig nadat u een site hebt verwijderd.

#### <a name="membership"></a>Lidmaatschap
Configuration Manager beheert automatisch het groepslid maatschap. Elke gebruiker met beheerders rechten in een hiërarchie en het computer account van de site server is standaard lid van de **SMS admins** -groep op elke SMS-provider computer in een-site.

#### <a name="permissions"></a>Machtigingen
U kunt de rechten en machtigingen voor de SMS admins-groep weer geven in de MMC-module voor **WMI-beheer** . Aan deze groep wordt standaard de **optie account inschakelen** en **Extern inschakelen** op de `Root\SMS` WMI-naam ruimte toegekend. Geverifieerde gebruikers hebben **uitvoerings methoden**, een **provider schrijven**en **account inschakelen**.

Wanneer u een externe Configuration Manager-console gebruikt, configureert u de DCOM-machtigingen voor **externe activering** op zowel de site Server computer als de SMS-provider. Ken deze rechten toe aan de **SMS admins** -groep. Deze actie vereenvoudigt het beheer in plaats van deze rechten rechtstreeks aan gebruikers of groepen toe te kennen. Zie [DCOM-machtigingen voor externe Configuration Manager-consoles configureren](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole)voor meer informatie. 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_ &lt; site code\>  
 
Beheer punten die zich op afstand van de site server bevinden, gebruiken deze groep om verbinding te maken met de site database. Deze groep biedt een beheerpunt toegang tot het Postvak IN op de siteserver en de sitedatabase.  

#### <a name="type-and-location"></a>Type en locatie
Deze groep is een lokale beveiligings groep die is gemaakt op elke computer met een SMS-provider.

Wanneer u een site verwijdert, wordt deze groep niet automatisch verwijderd. Verwijder deze hand matig nadat u een site hebt verwijderd.

#### <a name="membership"></a>Lidmaatschap
Configuration Manager beheert automatisch het groepslid maatschap. Lidmaatschap omvat standaard de computeraccounts van externe computers die een beheerpunt voor de site hebben.

#### <a name="permissions"></a>Machtigingen
Deze groep heeft standaard de machtiging **lezen**, **lezen & uitvoeren**en Mapinhoud **weer geven** voor de volgende map op de site server: `C:\Program Files\Microsoft Configuration Manager\inboxes` . Deze groep heeft de extra machtiging **schrijven** naar submappen onder **Postvak**in, waarnaar het beheer punt client gegevens schrijft.


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_ &lt; site code\>  
 
Externe SMS-provider computers gebruiken deze groep om verbinding te maken met de site server.  

#### <a name="type-and-location"></a>Type en locatie
Deze groep is een lokale beveiligingsgroep die op de siteserver is gemaakt.

Wanneer u een site verwijdert, wordt deze groep niet automatisch verwijderd. Verwijder deze hand matig nadat u een site hebt verwijderd.

#### <a name="membership"></a>Lidmaatschap
Configuration Manager beheert automatisch het groepslid maatschap. Lidmaatschap omvat standaard het computer account of een domein gebruikers account. Deze account wordt gebruikt om verbinding te maken met de site server van elke externe SMS-provider.

#### <a name="permissions"></a>Machtigingen
Deze groep heeft standaard de machtiging **lezen**, **lezen & uitvoeren**en Mapinhoud **weer geven** voor de volgende map op de site server: `C:\Program Files\Microsoft Configuration Manager\inboxes` . Deze groep heeft de extra machtigingen **schrijven** en **wijzigen** in submappen onder de post vakken. De SMS-provider vereist toegang tot deze mappen.

Deze groep heeft ook **Lees** machtigingen voor de submappen op de onderstaande site server `C:\Program Files\Microsoft Configuration Manager\OSD\Bin` . 

Het bevat ook de volgende machtigingen voor de submappen hieronder `C:\Program Files\Microsoft Configuration Manager\OSD\boot` :
- **Lezen**  
- **Lezen & uitvoeren**  
- **Mapinhoud weer geven**  
- **Schrijven**  
- **Wijzigen**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_ &lt; site code\>  

Het onderdeel Bestands verzendings beheer op Configuration Manager externe site systeem computers maakt gebruik van deze groep om verbinding te maken met de site server.  

#### <a name="type-and-location"></a>Type en locatie
Deze groep is een lokale beveiligingsgroep die op de siteserver is gemaakt.

Wanneer u een site verwijdert, wordt deze groep niet automatisch verwijderd. Verwijder deze hand matig nadat u een site hebt verwijderd.

#### <a name="membership"></a>Lidmaatschap
Configuration Manager beheert automatisch het groepslid maatschap. Lidmaatschap omvat standaard het computer account of het domein gebruikers account. Dit account wordt gebruikt om verbinding te maken met de site server van elk extern site systeem dat het File Dispatch Manager uitvoert.

#### <a name="permissions"></a>Machtigingen
Deze groep beschikt standaard over de machtigingen **lezen**, **lezen & uitvoeren**en Mapinhoud **weer geven** voor de volgende map en de bijbehorende submappen op de site server: `C:\Program Files\Microsoft Configuration Manager\inboxes` . 

Deze groep heeft de extra machtigingen **schrijven** en **wijzigen** in de volgende map op de site server: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box` .


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_ &lt; site code\>  
Configuration Manager gebruikt deze groep om op bestanden gebaseerde replicatie tussen sites in een hiërarchie in te scha kelen. Voor elke externe site die rechtstreeks bestanden overbrengt naar deze site, bevat deze groep accounts die zijn ingesteld als een **account voor bestands replicatie**.  

#### <a name="type-and-location"></a>Type en locatie
Deze groep is een lokale beveiligingsgroep die op de siteserver is gemaakt.

#### <a name="membership"></a>Lidmaatschap
Wanneer u een nieuwe site installeert als een onderliggend element van een andere site, voegt Configuration Manager automatisch het computer account van de nieuwe site server toe aan deze groep op de bovenliggende site server. Configuration Manager voegt ook het computer account van de bovenliggende site toe aan de groep op de nieuwe site server. Als u een ander account opgeeft voor overdracht op basis van bestanden, voegt u dit account dan toe aan deze groep op de doel site server.

Wanneer u een site verwijdert, wordt deze groep niet automatisch verwijderd. Verwijder deze hand matig nadat u een site hebt verwijderd.

#### <a name="permissions"></a>Machtigingen
Deze groep heeft standaard de **volledige controle** over de volgende map: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive` .



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a> Accounts die Configuration Manager gebruikt  

U kunt de volgende accounts instellen voor Configuration Manager.  

> [!TIP]
> Gebruik niet het procent teken ( `%` ) in het wacht woord voor accounts die u opgeeft in de Configuration Manager-console. Het account kan niet worden geverifieerd.<!-- SCCMDocs#1032 -->

### <a name="active-directory-group-discovery-account"></a>Account voor detectie van Active Directory-groep  

De site maakt gebruik van het **detectie account Active Directory groep** om de volgende objecten te detecteren vanaf de locaties in Active Directory Domain Services die u opgeeft:
- Lokale, globale en universele beveiligings groepen
- Het lidmaatschap van deze groepen
- Het lidmaatschap binnen distributie groepen
  - Distributie groepen worden niet als groeps bronnen gedetecteerd

Dit account kan een computeraccount van de siteserver zijn dat detectie uitvoert of een Windows-gebruikersaccount. De machtiging moet **Lees** toegang hebben tot de Active Directory locaties die u voor detectie opgeeft.  

Zie voor meer informatie [Active Directory groeps detectie](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Account voor Active Directory systeem detectie  

De site gebruikt het **Active Directory systeem detectie account** om computers te detecteren vanaf de locaties in Active Directory Domain Services die u opgeeft.  

Dit account kan een computeraccount van de siteserver zijn dat detectie uitvoert of een Windows-gebruikersaccount. De machtiging moet **Lees** toegang hebben tot de Active Directory locaties die u voor detectie opgeeft.  

Zie [Active Directory-systeem detectie](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem)voor meer informatie.


### <a name="active-directory-user-discovery-account"></a>Gebruikers detectie account Active Directory  
 
De site gebruikt het **Active Directory detectie account** van de gebruiker om gebruikers accounts te detecteren vanaf de locaties in Active Directory Domain Services die u opgeeft.  

Dit account kan een computeraccount van de siteserver zijn dat detectie uitvoert of een Windows-gebruikersaccount. De machtiging moet **Lees** toegang hebben tot de Active Directory locaties die u voor detectie opgeeft.  

Zie [Active Directory gebruikers detectie](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)voor meer informatie. 


### <a name="active-directory-forest-account"></a>Active Directory-forest-account  

De site gebruikt het **Active Directory-forest-account** om de netwerk infrastructuur van Active Directory forests te detecteren. Centrale beheer sites en primaire sites gebruiken IT ook om site gegevens te publiceren naar Active Directory Domain Services voor een forest.  

> [!NOTE]  
> Secundaire sites gebruiken steeds het computeraccount van de secundaire siteserver om naar Active Directory te publiceren.  

Om niet-vertrouwde forests te detecteren en te publiceren, moet het Active Directory forest-account een globaal account zijn. Als u het computer account van de site server niet gebruikt, kunt u alleen een globaal account selecteren.  

Dit account moet **Lezen**-machtigingen hebben voor elk Active Directory-forest waar u de netwerkinfrastructuur wilt detecteren.  

Dit account moet machtigingen voor **volledig beheer** hebben voor de **System Management** -container en alle onderliggende objecten in elk Active Directory forest waar u site gegevens wilt publiceren. Zie [Active Directory voorbereiden voor het publiceren van sites](../network/extend-the-active-directory-schema.md)voor meer informatie.  

Zie [Active Directory forest Discovery](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)(Engelstalig) voor meer informatie.


### <a name="certificate-registration-point-account"></a>Account voor het certificaat registratiepunt  

Het certificaat registratiepunt gebruikt het **account voor het certificaat registratiepunt** om verbinding te maken met de Configuration Manager-Data Base. Het computer account wordt standaard gebruikt, maar u kunt in plaats daarvan een gebruikers account configureren. Wanneer het certificaat registratiepunt zich in een niet-vertrouwd domein van de site server bevindt, moet u een gebruikers account opgeven. Dit account heeft alleen **Lees** toegang tot de site database nodig omdat het status bericht systeem schrijf taken verwerkt.  

Zie [Inleiding tot certificaat profielen](../../../protect/deploy-use/introduction-to-certificate-profiles.md)voor meer informatie.


### <a name="capture-os-image-account"></a>Account voor installatie kopie van besturings systeem vastleggen  

Wanneer u een installatie kopie van een besturings systeem vastlegt, gebruikt Configuration Manager het Capture-account van het **installatie kopie** bestand voor toegang tot de map waarin u de vastgelegde installatie kopieën opslaat. Als u de stap **installatie kopie van besturings systeem vastleggen** toevoegt aan een taken reeks, is dit account vereist.  

Het account moet de machtigingen **lezen** en **schrijven** hebben op de netwerk share waar u vastgelegde installatie kopieën opslaat.  

Als u het wacht woord voor het account in Windows wijzigt, werkt u de taken reeks bij met het nieuwe wacht woord. De Configuration Manager-client ontvangt het nieuwe wacht woord wanneer het de volgende keer het client beleid downloadt.  

Als u dit account wilt gebruiken, maakt u één domein gebruikers account. Verleen het minimale machtigingen voor toegang tot de vereiste netwerk bronnen en gebruik dit voor alle Capture-taken reeksen.  

> [!IMPORTANT]  
> Wijs geen interactieve aanmeldings machtigingen toe aan dit account.  
>   
> Gebruik niet het netwerk toegangs account voor dit account.  

Zie [een taken reeks maken voor het vastleggen van een besturings systeem](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)voor meer informatie.


### <a name="client-push-installation-account"></a>Account voor push-client installatie  

Wanneer u clients implementeert met behulp van de Push-client installatie methode, gebruikt de site het **account voor push-client installatie** om verbinding te maken met computers en de Configuration Manager-client software te installeren. Als u dit account niet opgeeft, probeert de site server het computer account te gebruiken.  

Dit account moet lid zijn van de lokale groep **Administrators** op de doel-client computers. Voor dit account zijn geen beheerders rechten voor het **domein** vereist.  

U kunt meer dan één client push installatie account opgeven. Configuration Manager probeert elke keer elke keer, totdat er een slaagt.  

> [!TIP]  
> Als u een grote Active Directory omgeving hebt en dit account moet wijzigen, gebruikt u het volgende proces om deze account update effectiever te coördineren: 
> 1. Een nieuw account met een andere naam maken   
> 2. Voeg het nieuwe account toe aan de lijst met accounts voor push-installatie van de client in Configuration Manager  
> 3. Voldoende tijd toestaan dat Active Directory Domain Services het nieuwe account repliceert  
> 4. Verwijder vervolgens het oude account uit Configuration Manager en Active Directory Domain Services  

> [!IMPORTANT]  
> Verleen dit account niet het recht om lokaal aan te melden.  

Zie [client push Installation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)(Engelstalig) voor meer informatie.


### <a name="enrollment-point-connection-account"></a>Verbindings account voor inschrijvings punt  

Het inschrijvings punt gebruikt het account voor de **inschrijvings punt verbinding** om verbinding te maken met de Configuration Manager-site database. Het computer account wordt standaard gebruikt, maar u kunt in plaats daarvan een gebruikers account configureren. Wanneer het inschrijvings punt zich in een niet-vertrouwd domein van de site server bevindt, moet u een gebruikers account opgeven. Dit account vereist **Lees** -en **Schrijf** toegang tot de site database.  

Zie [site systeem rollen installeren voor on-premises MDM](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)voor meer informatie.


### <a name="exchange-server-connection-account"></a>Exchange Server-verbindings account  

De site server gebruikt het **Exchange Server-verbindings account** om verbinding te maken met de opgegeven Exchange-Server. Deze verbinding wordt gebruikt voor het zoeken en beheren van mobiele apparaten die verbinding maken met Exchange Server. Dit account vereist Exchange PowerShell-cmdlets die de vereiste machtigingen op de Exchange Server-computer bieden. Zie [de Exchange-connector installeren en configureren](../../../mdm/deploy-use/install-configure-exchange-connector.md)voor meer informatie over de cmdlets.  


### <a name="management-point-connection-account"></a>Verbindings account beheer punt  

Het beheer punt gebruikt het **verbindings account van het beheer punt** om verbinding te maken met de Configuration Manager-site database. Deze verbinding wordt gebruikt voor het verzenden en ophalen van informatie voor clients. Het computer account van het beheer punt wordt standaard gebruikt, maar u kunt in plaats daarvan een gebruikers account configureren. Wanneer het beheer punt zich in een niet-vertrouwd domein van de site server bevindt, moet u een gebruikers account opgeven.  

Maak het account als een lokaal account met beperkte rechten op de computer waarop Microsoft SQL Server wordt uitgevoerd.  

> [!IMPORTANT]  
> Ken geen interactieve aanmeldings rechten toe aan dit account.  


### <a name="multicast-connection-account"></a>Multicast verbindings account  

Multi cast-distributie punten gebruiken het **multi cast-verbindings account** om informatie uit de site database te lezen. De server maakt standaard gebruik van het computer account, maar u kunt in plaats daarvan een gebruikers account configureren. Wanneer de site database zich in een niet-vertrouwd forest bevindt, moet u een gebruikers account opgeven. Als uw data centrum bijvoorbeeld een perimeter netwerk heeft in een ander forest dan de site server en site database, gebruikt u dit account om de multicast informatie uit de site database te lezen.  

Als u dit account nodig hebt, maakt u dit als een lokaal account met beperkte rechten op de computer waarop Microsoft SQL Server wordt uitgevoerd.  

> [!IMPORTANT]  
> Ken geen interactieve aanmeldings rechten toe aan dit account.  

Zie [multi cast gebruiken om Windows via het netwerk te implementeren](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)voor meer informatie.


### <a name="network-access-account"></a>Netwerktoegangsaccount  

Client computers gebruiken het **netwerk toegangs account** wanneer ze hun lokale computer account niet kunnen gebruiken voor toegang tot inhoud op distributie punten. Dit geldt voornamelijk voor werkgroepcomputers en computers uit niet-vertrouwde domeinen. Dit account wordt ook gebruikt tijdens de implementatie van het besturings systeem, wanneer de computer die het besturings systeem installeert nog niet over een computer account voor het domein beschikt.  

> [!Important]  
> Het netwerk toegangs account wordt nooit gebruikt als de beveiligings context om Program ma's uit te voeren, software-updates te installeren of taken reeksen uit te voeren. Het wordt alleen gebruikt voor toegang tot bronnen op het netwerk.  

Een Configuration Manager client probeert eerst het computer account te gebruiken om de inhoud te downloaden. Als dit mislukt, probeert het automatisch het netwerk toegangs account.  

Als u de site configureert voor HTTPS of [verbeterde http](enhanced-http.md), kan een werk groep of Azure AD-client veilig toegang krijgen tot inhoud vanaf distributie punten zonder dat hiervoor een netwerk toegangs account nodig is. Dit gedrag omvat implementatie scenario's voor besturings systemen met een taken reeks die wordt uitgevoerd vanaf opstart media, PXE of software Center.<!--1358228,1358278--> Zie [communicatie tussen clients en beheer punten](communications-between-endpoints.md#bkmk_client2mp)voor meer informatie.<!-- SCCMDocs#1345 -->

> [!Note]  
> Als u **Enhanced http** inschakelt om het netwerk toegangs account niet te vereisen, moet op het distributie punt Windows Server 2012 of hoger worden uitgevoerd. <!--SCCMDocs-pr issue #2696-->
>  
> Upgrade clients naar ten minste versie 1806 voordat u deze functie inschakelt. Als u alleen **uitgebreide HTTP-** verbindingen toestaat, kunnen oudere clients niet met deze methode verifiëren, dus kan het client upgrade pakket niet downloaden van een distributie punt. <!--vso2841213-->   

#### <a name="permissions"></a>Machtigingen

Verleen aan dit account de minimum geschikte machtigingen op de inhoud die de client nodig heeft voor toegang tot de software. Het account moet de **toegang tot deze computer vanaf het netwerk** hebben op het distributie punt. U kunt Maxi maal 10 netwerk toegangs accounts per site configureren.  

Maak het account in elk domein dat de benodigde toegang tot bronnen biedt. Het netwerk toegangs account moet altijd een domein naam bevatten. Pass-Through-beveiliging wordt niet ondersteund voor dit account. Als u over distributiepunten in meerdere domeinen beschikt, maakt u het account in een vertrouwd domein.  

> [!TIP]  
> Wijzig het wacht woord van een bestaand netwerk toegangs account niet om account vergrendelingen te voor komen. Maak in plaats daarvan een nieuw account en stel het nieuwe account in Configuration Manager. Wanneer er voldoende tijd is verstreken waarbinnen alle clients de nieuwe accountgegevens hebben ontvangen, verwijdert u het account uit de gedeelde netwerkmappen en verwijdert u het account.  

> [!IMPORTANT]  
> Ken geen interactieve aanmeldings rechten toe aan dit account.  
>   
> Verleen dit account niet het recht om computers aan het domein toe te voegen. Als u tijdens een taken reeks computers moet toevoegen aan het domein, gebruikt u het [account voor taken reeks domein deelname](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Het netwerk toegangs account configureren  

1.  Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Selecteer vervolgens de site.  

2.  Selecteer in de groep **instellingen** van het lint de optie **site onderdelen configureren**en kies **software distributie**.  

3.  Kies het tabblad **netwerk toegangs account** . Stel een of meer accounts in en klik vervolgens op **OK**.  


### <a name="package-access-account"></a>Pakket toegangs account  

Met een **pakket toegangs account** kunt u NTFS-machtigingen instellen om de gebruikers en gebruikers groepen op te geven die toegang hebben tot pakket inhoud op distributie punten. Configuration Manager verleent standaard alleen toegang tot de algemene toegangs accounts **gebruiker** en **beheerder**. U kunt de toegang voor client computers beheren via aanvullende Windows-accounts of-groepen. Mobiele apparaten halen pakket inhoud altijd anoniem op, zodat ze geen pakket toegangs account gebruiken.  

Wanneer Configuration Manager de inhouds bestanden naar een distributie punt kopieert, wordt standaard **Lees** toegang verleend aan de groep lokale **gebruikers** en **volledig beheer** aan de lokale groep **Administrators** . De daad werkelijke machtigingen die vereist zijn, zijn afhankelijk van het pakket. Als u clients in werk groepen of in niet-vertrouwde forests hebt, gebruiken die clients het netwerk toegangs account om toegang te krijgen tot de pakket inhoud. Zorg ervoor dat het netwerk toegangs account machtigingen heeft voor het pakket door gebruik te maken van de gedefinieerde pakket toegangs accounts.  

Gebruik accounts in een domein dat toegang heeft tot de distributiepunten. Als u het account maakt of wijzigt nadat u het pakket hebt gemaakt, moet u het pakket opnieuw distribueren. Het bijwerken van het pakket heeft geen invloed op de NTFS-machtigingen op het pakket.  

U hoeft het netwerk toegangs account niet toe te voegen als een pakket toegangs account omdat het lidmaatschap van de groep **gebruikers** dit automatisch toevoegt. Als u het pakket toegangs account beperkt tot het netwerk toegangs account, kunnen clients geen toegang krijgen tot het pakket.  

#### <a name="manage-package-access-accounts"></a>Pakket toegangs accounts beheren  

1.  Kies in de Configuration Manager-console de optie **software bibliotheek**.  

2.  Bepaal in de werk ruimte **software bibliotheek** het type inhoud waarvoor u toegangs accounts wilt beheren en volg de stappen die worden beschreven:  

    - **Toepassing**: Vouw **toepassings beheer**uit, kies **toepassingen**en selecteer vervolgens de toepassing waarvoor u toegangs accounts wilt beheren.  

    - **Pakket**: Vouw **toepassings beheer**uit, kies **pakketten**en selecteer vervolgens het pakket waarvoor u toegangs accounts wilt beheren.  

    - **Software-update-implementatie pakket**: Vouw **software-updates**uit, kies **implementatie pakketten**en selecteer vervolgens het implementatie pakket waarvoor u toegangs accounts wilt beheren.  

    - **Stuur programmapakket**: Vouw **besturings systemen**uit, kies **Stuur programmapakketten**en selecteer vervolgens het stuur programmapakket waarvoor u toegangs accounts wilt beheren.  

    - **OS-installatie kopie**: Vouw **besturings systemen**uit, kies **installatie kopieën van besturings systeem**en selecteer vervolgens de installatie kopie van het besturings systeem waarvoor u toegangs accounts wilt beheren.  

    - **OS-upgrade pakket**: Vouw **besturings systemen**uit, kies **besturingssysteem upgrade pakketten**en selecteer vervolgens het upgrade pakket voor het besturings systeem waarvoor u toegangs accounts wilt beheren.  

    - **Opstart installatie kopie**: Vouw **besturings systemen**uit, kies **opstart installatie kopieën**en selecteer vervolgens de opstart installatie kopie waarvoor u toegangs accounts wilt beheren.  

3.  Klik met de rechter muisknop op het geselecteerde object en kies **toegangs accounts beheren**.  

4.  Geef in het dialoog venster **account toevoegen** het account type op waaraan toegang tot de inhoud wordt verleend en geef vervolgens de toegangs rechten op die aan het account zijn gekoppeld.  

    > [!NOTE]  
    > Wanneer u een gebruikers naam voor het account toevoegt en Configuration Manager een lokaal gebruikers account en een domein gebruikers account met die naam vindt, worden door Configuration Manager toegangs rechten ingesteld voor het domein gebruikers account.  


### <a name="reporting-services-point-account"></a>Account van Reporting Services-punt  
 
SQL Server Reporting Services gebruikt het **account van het Reporting Services-punt** om de gegevens voor Configuration Manager rapporten op te halen uit de site database. Het Windows-gebruikersaccount en wachtwoord die u opgeeft, worden versleuteld en opgeslagen in de SQL Server Reporting Services-database.  

> [!NOTE]  
> Het account dat u opgeeft moet de machtiging **lokaal aanmelden** hebben op de computer die als host fungeert voor de SQL Reporting Services-Data Base.

> [!NOTE]  
> Aan het account worden automatisch alle benodigde rechten verleend door toe te voegen aan de smsschm_users SQL Database rol van de Configuration Manager-Data Base.

Zie [Introduction to Reporting](../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.


### <a name="remote-tools-permitted-viewer-accounts"></a>Toegestane Viewer accounts voor externe hulpprogram ma's  

De accounts die u opgeeft als **toegestane viewers** voor extern beheer zijn een lijst van gebruikers die zijn gemachtigd externe hulpprogramma's te gebruiken op clients.  

Zie [Inleiding tot beheer op afstand](../../clients/manage/remote-control/introduction-to-remote-control.md)voor meer informatie.


### <a name="site-installation-account"></a>Site-installatie account
<!--SCCMDocs issue #572-->
Gebruik een domein gebruikers account om u aan te melden bij de server waarop u Configuration Manager Setup uitvoert en een nieuwe site installeert.

Voor dit account zijn de volgende rechten vereist:  

- **Beheerder** op de volgende servers:
    - De site server  
    - Elke server die als host fungeert voor de site database  
    - Elk exemplaar van de SMS-provider voor de site  

- **Sysadmin** op het exemplaar van SQL Server dat als host fungeert voor de site database  

Configuration Manager Setup voegt dit account automatisch toe aan de groep [SMS admins](#sms-admins) .

Na de installatie is dit account de enige gebruiker met rechten voor de Configuration Manager-console. Als u dit account wilt verwijderen, moet u ervoor zorgen dat u eerst de rechten aan een andere gebruiker toevoegt.

Bij het uitbreiden van een zelfstandige site om een centrale beheer site op te halen, vereist dit account volledige beheer rechten op basis van de rol **beheerder** of **infrastructuur beheerder** op de zelfstandige primaire site.


### <a name="site-system-installation-account"></a>Installatie account site systeem  

De site server gebruikt het **installatie account van het site systeem** om site systemen te installeren, opnieuw te installeren, te verwijderen en in te stellen. Als u het site systeem zo instelt dat de site server verbindingen met dit site systeem moet initiëren, gebruikt Configuration Manager dit account ook om gegevens van het site systeem op te halen nadat het site systeem en alle rollen zijn geïnstalleerd. Elk site systeem kan een ander installatie account hebben, maar u kunt slechts één installatie account instellen om alle rollen op dat site systeem te beheren.  

Voor dit account zijn lokale beheerders machtigingen vereist op de doel site systemen. Daarnaast moet dit account toegang hebben **tot deze computer vanaf het netwerk** in het beveiligings beleid op de doel site systemen.  

> [!TIP]  
> Als u veel domein controllers hebt en deze accounts worden gebruikt in meerdere domeinen, moet u voordat u het site systeem instelt, controleren of Active Directory deze accounts heeft gerepliceerd.  
>   
> Wanneer u een lokaal account opgeeft op elk site systeem dat moet worden beheerd, is deze configuratie veiliger dan met behulp van domein accounts. Het beperkt de schade die aanvallers kunnen uitvoeren als het account is aangetast. Domein accounts zijn echter gemakkelijker te beheren. Houd rekening met de afweging tussen beveiliging en effectief beheer.  


### <a name="site-system-proxy-server-account"></a>Proxy Server account van site systeem
<!--SCCMDocs issue #648-->
De volgende site systeem rollen gebruiken het **site systeem proxyserver account** voor toegang tot internet via een proxy server of firewall die geverifieerde toegang vereist:

- Asset Intelligence-synchronisatiepunt
- Exchange Server-connector
- Serviceverbindingspunt
- Software-updatepunt

> [!IMPORTANT]  
> Geef een account op dat over de geringst mogelijke machtigingen voor de vereiste proxyserver of firewall beschikt.  

Zie [ondersteuning voor proxy server](../network/proxy-server-support.md)voor meer informatie.


### <a name="smtp-server-connection-account"></a>SMTP-server verbindings account  

De site server gebruikt het **SMTP-server verbindings account** om e-mail waarschuwingen te verzenden wanneer de SMTP-server geverifieerde toegang vereist.  

> [!IMPORTANT]  
> Geef een account die de geringst mogelijke machtigingen heeft om e-mails te verzenden.  

Zie [waarschuwingen en het status systeem gebruiken](../../servers/manage/use-alerts-and-the-status-system.md)voor meer informatie.


### <a name="software-update-point-connection-account"></a>Verbindings account software-update punt  

De site server maakt gebruik van het **verbindings account van het software-update punt** voor de volgende twee Software-Update Services:  

- Windows Server Update Services (WSUS), waarmee instellingen worden ingesteld, zoals product definities, classificaties en upstream-instellingen.  

- WSUS Synchronization Manager, dat synchronisatie vraagt met een upstream WSUS-server of Microsoft Update.  

Het [installatie account van het site systeem](#site-system-installation-account) kan onderdelen voor software-updates installeren, maar kan geen software-update-specifieke functies uitvoeren op het software-update punt. Als u het computer account van de site server voor deze functionaliteit niet kunt gebruiken omdat het software-update punt zich in een niet-vertrouwd forest bevindt, moet u dit account opgeven naast het installatie account van het site systeem.  

Dit account moet een lokale beheerder zijn op de computer waarop u WSUS installeert. Het moet ook deel uitmaken van de lokale groep **WSUS-Administrators** .  

Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md)voor meer informatie.


### <a name="source-site-account"></a>Bron site account  

Het migratie proces gebruikt het **bron site account** om toegang te krijgen tot de SMS-provider van de bron site. Dit account vereist **Lezen**-machtigingen op siteobjecten in de bronsite om gegevens voor migratiejobs te verzamelen.  

Als u beschikt over Configuration Manager 2007-distributie punten of secundaire sites met een distributie punt op basis van een upgrade naar Configuration Manager (current branch)-distributie punten, moet dit account ook **verwijderings** machtigingen hebben voor de klasse **site** . Deze machtiging is om het distributie punt tijdens de upgrade van de Configuration Manager 2007-site te verwijderen.  

> [!NOTE]  
> Zowel het bron site account als het [bron site database account](#source-site-database-account) worden als **migratie beheer** aangeduid in het knoop punt **accounts** van de werk ruimte **beheer** in de Configuration Manager-console.  

Zie voor meer informatie [migreren van gegevens tussen hiërarchieën](/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Bron site database account  

Het migratie proces maakt gebruik van het **bron site database account** om toegang te krijgen tot de SQL Server Data Base voor de bron site. Als u gegevens wilt verzamelen uit de SQL Server Data Base van de bron site, moet het bron site database account de machtigingen **lezen** en **uitvoeren** hebben voor de SQL Server-Data Base van de bron site.  

Als u het computer account Configuration Manager (current branch) gebruikt, moet u ervoor zorgen dat alle volgende voor dit account waar zijn:  
  
- Het is lid van de beveiligings groep **gedistribueerde COM-gebruikers** in hetzelfde domein als de Configuration Manager 2007-site  
- Het is lid van de beveiligings groep **SMS admins**  
- Het beschikt over de machtiging **lezen** voor alle Configuration Manager 2007-objecten  

> [!NOTE]  
> Zowel het bron site account als het [bron site database account](#source-site-database-account) worden als **migratie beheer** aangeduid in het knoop punt **accounts** van de werk ruimte **beheer** in de Configuration Manager-console.  

Zie voor meer informatie [migreren van gegevens tussen hiërarchieën](/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Lidmaatschaps account voor taken reeks domein 

Windows Setup gebruikt het **account voor taken reeks domein deelname** om een computer met een nieuwe installatie kopie toe te voegen aan een domein. Dit account is vereist voor de taken reeks stap lid maken van [domein of werk groep](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) met de optie **lid worden van een domein** . Dit account kan ook worden ingesteld met de stap [netwerk instellingen Toep assen](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings) , maar dit is niet vereist.  

Voor dit account is het recht **domein toevoegen** vereist in het doel domein.  

> [!TIP]  
> Maak één domein gebruikers account met de minimale machtigingen om lid te worden van het domein en gebruik dit voor alle taken reeksen.  

> [!IMPORTANT]  
> Wijs geen interactieve aanmeldings machtigingen toe aan dit account.  
>   
> Gebruik niet het netwerk toegangs account voor dit account.  


### <a name="task-sequence-network-folder-connection-account"></a>Verbindings account voor taken reeks netwerk mappen  

De taken reeks engine gebruikt het **verbindings account van de taken reeks** netwerkmap om verbinding te maken met een gedeelde map in het netwerk. Dit account is vereist voor de taken reeks stap [verbinding maken met](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) netwerkmap.  

Dit account vereist machtigingen voor toegang tot de opgegeven gedeelde map. Dit moet een domein gebruikers account zijn.  

> [!TIP]  
> Maak één domein gebruikers account met minimale machtigingen voor toegang tot de vereiste netwerk bronnen en gebruik dit voor alle taken reeksen.  

> [!IMPORTANT]  
> Wijs geen interactieve aanmeldings machtigingen toe aan dit account.  
>   
> Gebruik niet het netwerk toegangs account voor dit account.  


### <a name="task-sequence-run-as-account"></a>Uitvoeren als-account voor taken reeks  

De taken reeks engine gebruikt het **Run as-account van de taken reeks** om opdracht regels of Power shell-scripts uit te voeren met andere referenties dan het lokale systeem account. Dit account is vereist door de [opdracht regel uitvoeren](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) en [Power shell-script](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) taken reeks stappen uitvoeren met de optie **deze stap uitvoeren als het volgende account** is geselecteerd.  

Stel het account in op de minimale machtigingen die zijn vereist voor het uitvoeren van de opdracht regel die u opgeeft in de taken reeks. Het account vereist interactieve aanmeldings rechten. Normaal gesp roken is de mogelijkheid om software te installeren en netwerk bronnen te openen. Voor de taak Power shell-script uitvoeren is voor dit account lokale beheerders machtigingen vereist. 

> [!IMPORTANT]  
> Gebruik niet het netwerk toegangs account voor dit account.  
>   
> Maak het account nooit een domein beheerder.  
>   
> Stel nooit zwervende profielen in voor dit account. Wanneer de taken reeks wordt uitgevoerd, wordt het zwervende profiel voor het account gedownload. Hierdoor blijft het profiel kwetsbaar voor toegang op de lokale computer.  
>   
> Beperk het bereik van het account. Maak bijvoorbeeld verschillende run as-accounts voor taken reeksen voor elke taken reeks. Als er vervolgens één account wordt aangetast, zijn alleen de client computers waarvoor dat account toegang heeft, aangetast.  
>   
> Als de opdracht regel beheerders toegang op de computer vereist, kunt u overwegen om voor dit account een lokaal beheerders account te maken op alle computers waarop de taken reeks wordt uitgevoerd. Verwijder het account wanneer u het niet meer nodig hebt.  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a> Gebruikers objecten die door Configuration Manager worden gebruikt in SQL 
<!--SCCMDocs issue #1160-->
Configuration Manager maakt en onderhoudt automatisch de volgende gebruikers objecten in SQL.  Deze objecten bevinden zich in de Configuration Manager-Data Base onder beveiliging/gebruikers.  

> [!IMPORTANT]  
>  Als u deze objecten wijzigt of verwijdert, kan dit leiden tot ingrijpende problemen binnen een Configuration Manager omgeving.  U kunt het beste geen wijzigingen aanbrengen in deze objecten.


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

Dit object wordt gebruikt om query's uit te voeren onder de alleen-lezen context.  Dit object wordt gebruikt met verschillende opgeslagen procedures.


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

Dit object wordt gebruikt om machtigingen op te geven voor dynamische SQL-instructies.


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

Dit object wordt gebruikt om SQL Reporting uitvoeringen uit te voeren.  De volgende opgeslagen procedure wordt gebruikt met deze functie: spSRExecQuery.


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Database rollen die door Configuration Manager worden gebruikt in SQL
<!--SCCMDocs issue #1160-->
Configuration Manager maakt en onderhoudt automatisch de volgende functie objecten in SQL. Deze rollen bieden toegang tot specifieke opgeslagen procedures, tabellen, weer gaven en functies om de benodigde acties van elke rol uit te voeren om gegevens op te halen of gegevens in te voegen van en van de Configuration Manager Data Base. Deze objecten bevinden zich in de Configuration Manager-Data Base onder beveiliging/rollen/database rollen.

> [!IMPORTANT]  
> Als u deze objecten wijzigt of verwijdert, kan dit leiden tot ingrijpende problemen binnen een Configuration Manager omgeving. Wijzig deze objecten niet. De volgende lijst is alleen ter informatie bedoeld.

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Asset Intelligence volume licenties importeren. Configuration Manager verleent deze machtiging aan gebruikers accounts op basis van RBA-toegang om de volume licentie te kunnen importeren die moet worden gebruikt met Asset Intelligence.  Dit account kan worden toegevoegd door een volledige beheerdersrol of een Asset Manager-rol.

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Asset Intelligence Update synchronisatie. Configuration Manager verleent het computer account dat als host van het Asset Intelligence synchronisatie punt-account toegang krijgt tot Asset Intelligence-proxy gegevens en om de in behandeling zijnde AI-gegevens weer te geven voor het uploaden.

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

Buiten-band beheer. Deze rol wordt gebruikt door Configuration Manager AMT-rol om gegevens op te halen op apparaten die ondersteunde Intel AMT.

> [!NOTE]  
> Deze rol is afgeschaft in nieuwere releases van Configuration Manager.

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

Certificaat registratiepunt ter ondersteuning van Simple Certificate Enrollment Protocol (SCEP). Configuration Manager verleent machtigingen aan het computer account van het site systeem dat ondersteuning biedt voor het certificaat registratiepunt voor SCEP-ondersteuning voor ondertekening en verlenging van certificaten.

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

PFX-ondersteuning van het certificaat registratiepunt. Configuration Manager verleent machtigingen aan het computer account van het site systeem dat ondersteuning biedt voor het certificaat registratiepunt dat is geconfigureerd voor PFX-ondersteuning voor ondertekening en verlenging.

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

Apparaatbeheerpunt. Configuration Manager verleent deze machtiging aan het computer account voor een beheer punt met de optie ' mobiele apparaten en Mac-computer toestaan dit beheer punt te gebruiken ', de mogelijkheid om ondersteuning te bieden voor door MDM Inge schreven apparaten.

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

Service verbindings punt. Configuration Manager verleent deze machtiging aan het computer account dat het service aansluitpunt host om telemetriegegevens op te halen en te verstrekken, Cloud Services te beheren en service-updates te verkrijgen.

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

Gedistribueerde weer gaven. Configuration Manager verleent deze machtiging aan het computer account van de primaire site servers op de CAS wanneer de optie SQL Server gedistribueerde weer gaven is geselecteerd in de eigenschappen van de replicatie koppeling.

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

Data Warehouse. Configuration Manager verleent deze machtiging aan het computer account dat als host voor de Data Warehouse-rol wordt gehost.

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 Inschrijvings punt. Configuration Manager verleent deze machtiging aan het computer account dat het inschrijvings punt host om apparaatregistratie via MDM toe te staan.

### <a name="smsdbrole_extract"></a>smsdbrole_extract

Biedt toegang tot alle uitgebreide schema weergaven.

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

Hiërarchie Manager-service. Configuration Manager verleent machtigingen aan dit account voor het beheren van failover-status berichten en SQL Server Broker-trans acties tussen sites in een hiërarchie.

> [!NOTE]  
> De functie smdbrole_WebPortal is standaard lid van deze rol.

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

Multi cast-service. Configuration Manager verleent deze machtiging aan het computer account van het distributie punt dat multi cast ondersteunt.

### <a name="smsdbrole_mp"></a>smsdbrole_MP

Beheer punt. Configuration Manager verleent deze machtiging aan het computer account dat de rol beheer punt host om ondersteuning te bieden voor de Configuration Manager-clients.

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

Beheer punt micro soft BitLocker Administration and monitoring. Configuration Manager verleent deze machtiging aan het computer account dat het beheer punt host dat MBAM beheert voor een omgeving.

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

Toepassings aanvraag beheer punt. Configuration Manager verleent deze machtiging aan het computer account dat het beheer punt host om toepassings aanvragen op basis van gebruikers te ondersteunen.

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

SMS-provider. Configuration Manager verleent deze machtiging aan het computer account dat als host voor de functie van een SMS-provider wordt gehost.  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

Site server. Configuration Manager verleent deze machtiging aan het computer account dat de primaire of CAS-site host.

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

Software-update punt. Configuration Manager verleent deze machtiging aan het computer account dat het software-update punt host voor het werken met updates van derden.

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

Website punt van toepassingscatalogus. Configuration Manager verleent machtigingen aan het computer account dat het toepassingscatalogus website punt host om toepassings implementatie op basis van gebruikers te bieden.

### <a name="smsschm_users"></a>smsschm_users

Toegang voor gebruikers rapportage. Configuration Manager verleent toegang tot het account dat wordt gebruikt voor het Reporting Services-account om toegang te krijgen tot de SMS-rapportage weergaven om de Configuration Manager rapportage gegevens weer te geven.  De gegevens worden verder beperkt door het gebruik van RBA.

## <a name="elevated-permissions"></a>Verhoogde machtigingen

<!-- SCCMDocs#405 -->

Voor Configuration Manager moeten sommige accounts verhoogde machtigingen hebben voor on-continue bewerkingen. Zie bijvoorbeeld [vereisten voor het installeren van een primaire site](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_PrereqPri). De volgende lijst bevat een overzicht van deze machtigingen en de redenen waarom ze nodig zijn.

- Het computer account van de server van de primaire site server en de centrale beheer site vereist:

  - Lokale beheerders rechten op alle site systeem servers. Deze machtiging is om systeem services te beheren, te installeren en te verwijderen. De site server werkt ook lokale groepen op het site systeem bij wanneer u rollen toevoegt of verwijdert.

  - Sysadmin toegang tot het SQL-exemplaar voor de site database. Deze machtiging is voor het configureren en beheren van SQL voor de site. Configuration Manager nauw geïntegreerd met SQL, is het niet alleen een Data Base.

- Gebruikers accounts in de rol volledige beheerder vereisen:

  - Lokale beheerders rechten op alle site servers. Deze machtiging is om systeem services, register sleutels en-waarden en WMI-objecten weer te geven, te bewerken, te verwijderen en te installeren.

  - Sysadmin toegang tot het SQL-exemplaar voor de site database. Deze machtiging is om de data base te installeren en bij te werken tijdens de installatie of het herstel. Het is ook vereist voor SQL-onderhoud en-bewerkingen. U kunt bijvoorbeeld statistieken opnieuw indexeren en bijwerken.

    > [!NOTE]
    > Sommige organisaties kunnen ervoor kiezen om sysadmin-toegang te verwijderen en deze alleen te verlenen wanneer dit nodig is. Dit gedrag wordt soms aangeduid als just-in-time (JIT)-toegang. In dit geval moeten gebruikers met de rol volledige beheerder nog steeds toegang hebben tot opgeslagen procedures voor lezen, bijwerken en uitvoeren van de Configuration Manager Data Base. Deze machtigingen maken het mogelijk om de meeste problemen op te lossen zonder volledige sysadmin-toegang.