---
title: Migratie vereisten
titleSuffix: Configuration Manager
description: Meer informatie over de ondersteunde versies van Configuration Manager, ondersteunde talen voor de bron site en de vereiste configuraties voor migratie.
ms.date: 05/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 229a8c7980933480a243278b2679d55f012490ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713014"
---
# <a name="prerequisites-for-migration-in-configuration-manager"></a>Vereisten voor migratie in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u wilt migreren vanaf een ondersteunde bron hiërarchie, moet u toegang hebben tot elke toepasselijke Configuration Manager-bron site en machtigingen binnen de Configuration Manager doel site om migratie bewerkingen te configureren en uit te voeren.  

 Gebruik de informatie in de volgende secties om inzicht te krijgen in de versies van Configuration Manager die worden ondersteund voor migratie en de vereiste configuraties.  

-   [Versies van Configuration Manager die worden ondersteund voor migratie](#BKMK_SupportedMigrationVersions)  

-   [Bron site talen die worden ondersteund voor migratie](#BKMK_SorceSiteLanguage)  

-   [Vereiste configuraties voor migratie](#BKMK_Required_Configurations)  

##  <a name="versions-of-configuration-manager-that-are-supported-for-migration"></a><a name="BKMK_SupportedMigrationVersions"></a>Versies van Configuration Manager die worden ondersteund voor migratie  
 U kunt gegevens migreren vanaf een bron hiërarchie waarop een van de volgende versies van Configuration Manager worden uitgevoerd:  

- Configuration Manager 2007 SP2 (met het oog op de migratie is Configuration Manager 2007 R2 of R3 op de bron site niet in aanmerking genomen. Zolang op de bron site SP2 wordt uitgevoerd, worden sites met de R2-of R3-invoeg toepassing ondersteund voor migratie naar Configuration Manager current branch).  

- System Center 2012 Configuration Manager SP2 of System Center 2012 R2 Configuration Manager SP1.  

  > [!TIP]  
  >  Naast de migratie kunt u een in-place upgrade van sites met System Center 2012 Configuration Manager gebruiken om de huidige vertakking te Configuration Manager.  

- Een Configuration Manager-hiërarchie met dezelfde of een lagere versie van Configuration Manager.  

  Als u bijvoorbeeld een doel hiërarchie hebt waarop Configuration Manager huidige branch 1606 wordt uitgevoerd, kunt u migratie gebruiken om gegevens te kopiëren van een bron hiërarchie waarop versie 1606 of 1602 wordt uitgevoerd. U kunt echter geen gegevens migreren van een bron hiërarchie waarop 1610 wordt uitgevoerd.  


##  <a name="source-site-languages-that-are-supported-for-migration"></a><a name="BKMK_SorceSiteLanguage"></a> Bronsitetalen die worden ondersteund voor migratie  
 Wanneer u gegevens migreert tussen Configuration Manager hiërarchieën, worden de gegevens in de doel hiërarchie opgeslagen in de taalneutrale indeling voor Configuration Manager. Omdat Configuration Manager 2007 geen gegevens opslaat in een taalneutrale indeling, moet het migratie proces objecten converteren naar deze indeling tijdens de migratie van Configuration Manager 2007. Daarom worden alleen Configuration Manager 2007-bron sites die met de volgende talen worden geïnstalleerd, ondersteund voor migratie:  

-   Engels  

-   Frans  

-   Duits  

-   Japans  

-   Koreaans  

-   Russisch  

-   Vereenvoudigd Chinees  

-   Traditioneel Chinees  

Wanneer u gegevens migreert van een System Center 2012-Configuration Manager of Configuration Manager huidige branch-hiërarchie, zijn er geen taal beperkingen voor de bron site. Objecten in de database van de bronsite hebben al een taalneutrale indeling.  

##  <a name="required-configurations-for-migration"></a><a name="BKMK_Required_Configurations"></a>Vereiste configuraties voor migratie  
Hieronder vindt u de vereiste configuraties voor het gebruik van migratie-en migratie bewerkingen:  

- **Migratie configureren, uitvoeren en bewaken in de Configuration Manager-console:**  

   Op de doelsite moet aan uw account de op rollen gebaseerde beheerbeveiligingsrol van **Infrastructuurbeheerder**worden toegewezen. Met deze beveiligingsrol worden machtigingen verleend om alle migratiebewerkingen te beheren, inclusief maken van migratietaken, opruimen, bewaken en de actie om distributiepunten te delen en bij te werken.  

- **Gegevens verzamelen:**  

   Om ervoor te zorgen dat de doelsite gegevens kan verzamelen, moet u de volgende twee toegangaccounts op de bronsite configureren voor gebruik met elke bronsite:  

  -   **Bronsiteaccount:** dit account wordt gebruikt om toegang te krijgen tot de SMS-provider van de bronsite.  

      -   Voor een Configuration Manager 2007 SP2-bron site heeft dit account de machtiging **lezen** nodig voor alle bron site objecten.  

      -   Voor een System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron site heeft dit account de machtiging **lezen** nodig voor alle bron site objecten. u verleent deze machtiging aan het account door gebruik te maken van beheer op basis van rollen. Zie [basis principes van op rollen gebaseerd beheer voor Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)voor meer informatie over het gebruik van op rollen gebaseerd beheer.  

  -   **Bronsitedatabaseaccount:** dit account wordt gebruikt om toegang te krijgen tot de SQL Server-database van de bronsite. Hiervoor zijn de machtigingen **Verbinden**, **Uitvoeren**en **Selecteren** vereist voor de database van de bronsite.  

  U kunt deze accounts configureren wanneer u een nieuwe bronhiërarchie of het verzamelen van gegevens voor een aanvullende bronsite configureert, of wanneer u de referenties voor een bronsite opnieuw configureert. Deze accounts kunnen gebruikmaken van een domeingebruikersaccount of u kunt het computeraccount van de site op het hoogste niveau van de doelhiërarchie opgeven.  

  > [!IMPORTANT]  
  >  Als u de Configuration Manager computer account gebruikt voor een van beide toegangs accounts, moet u ervoor zorgen dat dit account lid is van de beveiligings groep **DCOM-gebruikers** in het domein waar de bron site zich bevindt.  

  Wanneer u gegevens verzamelt, worden de volgende netwerkprotocollen en -poorten gebruikt:  

  -   NetBIOS/SMB-445 (TCP)  

  -   RPC (WMI) - 135 (TCP)  

  -   SQL Server - De TCP-poorten die worden gebruikt door de databases van zowel de bron- als de doelsite.  

- **Software-updates migreren:**  

   Voordat u software-updates migreert, moet u de doelhiërarchie configureren met een software-updatepunt. Zie [De migratie van software-updates plannen](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates)voor meer informatie.  

- **Distributiepunten delen:**  

   Als u distributiepunten van een bronsite correct wilt delen, moet minstens één primaire site of de centrale beheersite in de doelhiërarchie dezelfde poortnummers voor clientaanvragen gebruiken als de bronsite. Zie [client communicatie poorten configureren](../../core/clients/deploy/configure-client-communication-ports.md) voor meer informatie over poorten voor client aanvragen.  

   Voor elke bronsite worden alleen de distributiepunten gedeeld die zijn geïnstalleerd op sitesysteemservers die zijn geconfigureerd met een FQDN.  

   Om een distributie punt te delen van een System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron site, moet het **bron site account** (waarmee toegang wordt gezocht tot de SMS-provider voor de bron site server) bovendien de machtiging **wijzigen** hebben voor het object **site** op de bron site. U verleent deze machtiging aan het account door gebruik te maken van beheer op basis van rollen. Zie [basis principes van op rollen gebaseerd beheer voor Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)voor meer informatie over het gebruik van op rollen gebaseerd beheer.  


- **Distributiepunten bijwerken of opnieuw toewijzen:**  

   Het **Toegangsaccount voor de bronsite** dat is geconfigureerd om gegevens te verzamelen vanaf de SMS-provider van de bronsite, moet beschikken over de volgende machtigingen:  

  - Als u een upgrade van een Configuration Manager 2007-distributie punt wilt uitvoeren, heeft het account de machtigingen **lezen**, **uitvoeren**en **verwijderen** voor de klasse **site** op de site server van de configuratie Manager2007 nodig om het distributie punt te verwijderen uit de bron site van de configuratie Manager2007.  

  - Als u een System Center 2012 Configuration Manager of Configuration Manager huidige Branch-distributie punt opnieuw wilt toewijzen, moet het account de machtiging **wijzigen** hebben voor het object **site** op de bron site. U verleent deze machtiging aan het account door gebruik te maken van beheer op basis van rollen. Zie [basis principes van op rollen gebaseerd beheer voor Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md)voor meer informatie over het gebruik van op rollen gebaseerd beheer.  

    Als u een distributiepunt correct wilt bijwerken of toewijzen aan een nieuwe hiërarchie, moeten de poorten die zijn geconfigureerd voor clientaanvragen op de site waar het distributiepunt in de bronhiërarchie wordt beheerd, overeenkomen met de poorten die zijn geconfigureerd voor clientaanvragen op de doelsite waar het distributiepunt wordt beheerd. Zie [client communicatie poorten configureren](../../core/clients/deploy/configure-client-communication-ports.md)voor meer informatie over poorten voor client aanvragen.  
