---
title: Lokale infrastructuur bijwerken
titleSuffix: Configuration Manager
description: Meer informatie over het bijwerken van de infra structuur, zoals SQL Server en het besturings systeem van site systemen.
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7efc775199a34a66a8cd4a83b85baccd4a3ab5cb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699480"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>On-premises infra structuur bijwerken die ondersteuning biedt voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de informatie in dit artikel om u te helpen bij het bijwerken van de server infrastructuur die Configuration Manager uitvoert.  

- Als u een *upgrade wilt uitvoeren* van een eerdere versie naar Configuration Manager, current branch, raadpleegt u [upgrade to Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md).  

- Zie [updates voor Configuration Manager](updates.md)als u uw Configuration Manager, de huidige branch, de infra structuur naar een nieuwe versie wilt *bijwerken* .  


## <a name="upgrade-the-os-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Het besturings systeem van site systemen bijwerken  

Configuration Manager ondersteunt de in-place upgrade van het besturings systeem van de server die als host fungeert voor een site server en een site systeemrol, in de volgende situaties:  

- Als Configuration Manager nog steeds het resulterende Service Pack-niveau van Windows ondersteunt, wordt in-place upgrade naar een later Windows Server-Service Pack ondersteund.  

- In-place upgrade vanaf:  

    - Windows Server 2016 naar Windows Server 2019  

    - Windows Server 2012 R2 naar Windows Server 2019  

    - Windows Server 2012 R2 naar Windows Server 2016  

    - Windows Server 2012 naar Windows Server 2016  

    - Windows Server 2012 naar Windows Server 2012 R2  

    - Windows Server 2008 R2 naar Windows Server 2012 R2  

Als u een server wilt bijwerken, gebruikt u de upgrade procedures van het besturings systeem waarnaar u een upgrade uitvoert. Zie de volgende artikelen:  

- [Windows Server Upgrade Center](https://aka.ms/upgradecenter)  

- [Upgrade-en conversie opties voor Windows Server 2016](/windows-server/get-started/supported-upgrade-paths)  

- [Upgrade opties voor Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="upgrade-to-windows-server-2016-or-2019"></a><a name="bkmk_2016-2019"></a> Voer een upgrade uit naar Windows Server 2016 of 2019

Volg de stappen in deze sectie voor een van de volgende upgrade scenario's:  

- Een upgrade uitvoeren van Windows Server 2012 R2 of Windows Server 2016 naar Windows Server 2019  

- Een upgrade uitvoeren van Windows Server 2012 of Windows Server 2012 R2 naar Windows Server 2016  

#### <a name="before-upgrade"></a>Vóór de upgrade

- (Windows Server 2012 of Windows Server 2012 R2): Verwijder de SCEP-client (System Center Endpoint Protection). Voor Windows Server is nu Windows Defender builend, waardoor de SCEP-client wordt vervangen. De aanwezigheid van de SCEP-client kan verhinderen dat een upgrade naar Windows Server wordt uitgevoerd.  

- Verwijder de WSUS-functie van de server als deze is geïnstalleerd. U kunt de SUSDB hand haven en opnieuw koppelen zodra WSUS opnieuw is geïnstalleerd.  

- Als u het besturings systeem van de site server bijwerkt, moet u ervoor zorgen dat [replicatie op basis van bestanden](../../plan-design/hierarchy/file-based-replication.md) in orde is voor de site. Controleer alle post vakken voor een achterstand op zowel verzendende als ontvangende sites. Als er veel vastgelopen of wachtende replicatie taken zijn, wacht u totdat ze zijn uitgeschakeld.<!-- SCCMDocs#1792 -->
    - Controleer op de verzendende site de **afzender. log**.
    - Controleer het logboek van de **wachtrij**op de ontvangende site.

#### <a name="after-upgrade"></a>Na de upgrade

- Zorg ervoor dat Windows Defender is ingeschakeld, stel in op automatisch starten en uitvoeren.  

- Zorg ervoor dat de volgende Configuration Manager services worden uitgevoerd:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Zorg ervoor dat de **Windows Process-activering** en **www/W3SVC-** Services zijn ingeschakeld en stel deze in op automatisch starten. Met het upgrade proces worden deze services uitgeschakeld, dus zorg ervoor dat ze worden uitgevoerd voor de volgende site systeem rollen:  

    - Siteserver  

    - Beheerpunt  

    - Application Catalog-webservicepunt  

    - Application Catalog-websitepunt  

- Zorg ervoor dat elke server die als host fungeert voor een site systeemrol blijft voldoen aan alle [vereisten](../../plan-design/configs/site-and-site-system-prerequisites.md). U moet bijvoorbeeld BITS of WSUS opnieuw installeren of specifieke instellingen configureren voor IIS.  

- Nadat de ontbrekende vereiste onderdelen zijn hersteld, start u de server nog een keer opnieuw op om te controleren of de services gestart en operationeel zijn.  

- Als u een upgrade uitvoert van de primaire site server, [voert u een site opnieuw](modify-your-infrastructure.md#bkmk_reset)in.  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Bekend probleem voor externe Configuration Manager-consoles

Nadat u de site server of een exemplaar van de SMS-provider hebt bijgewerkt, kunt u geen verbinding maken met de Configuration Manager-console. U kunt dit probleem omzeilen door de machtigingen voor de **SMS admins** -groep hand matig te herstellen in WMI. Machtigingen moeten worden ingesteld op de site server en op elke externe server die als host fungeert voor een exemplaar van de SMS-provider:

1. Open de micro soft Management Console (MMC) op de toepasselijke servers en voeg de module voor  **WMI-beheer**toe en selecteer vervolgens **lokale computer**.  

2. Open in de MMC de **Eigenschappen** van **WMI-beheer (lokaal)** en selecteer het tabblad **beveiliging** .  

3. Vouw de structuur onder hoofdmap uit, selecteer het **SMS** -knoop punt en kies vervolgens **beveiliging**.  Zorg ervoor dat de **SMS admins** -groep de volgende machtigingen heeft:  

    - Account inschakelen  

    - Op afstand inschakelen  

4. Selecteer op het **tabblad Beveiliging** onder het knoop punt **SMS** het knoop punt **site_ &lt; site** code> en kies vervolgens **beveiliging**. Zorg ervoor dat de **SMS admins** -groep de volgende machtigingen heeft:  

    - Methoden uitvoeren  

    - Provider schrijven  

    - Account inschakelen  

    - Op afstand inschakelen  

5. Sla de machtigingen voor het herstellen van de toegang voor de Configuration Manager-console op.  

#### <a name="known-issue-for-remote-site-systems"></a>Bekend probleem voor externe site systemen

Nadat u een server hebt bijgewerkt die als host fungeert voor een site systeemrol, ontbreekt de waarde `Software\Microsoft\SMS` mogelijk in de volgende register sleutel: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

Als deze waarde ontbreekt nadat u Windows op de server hebt bijgewerkt, voegt u deze hand matig toe. Anders kunnen site systeem rollen problemen hebben met het uploaden van bestanden naar de post vakken van de site server.

### <a name="upgrade-to-windows-server-2012-r2"></a><a name="bkmk_2012r2"></a> Upgrade uitvoeren naar Windows Server 2012 R2

Wanneer u een upgrade uitvoert van Windows Server 2008 R2 of Windows Server 2012 naar Windows Server 2012 R2, gelden de volgende voor waarden:

#### <a name="before-upgrade"></a>Vóór de upgrade

- Op Windows Server 2012: Verwijder de WSUS-functie van de server als deze is geïnstalleerd. U kunt de SUSDB hand haven en opnieuw koppelen zodra WSUS opnieuw is geïnstalleerd.  

- In Windows Server 2008 R2: voordat u een upgrade naar Windows Server 2012 R2 uitvoert, moet u WSUS 3,2 van de server verwijderen. U kunt de SUSDB hand haven en opnieuw koppelen zodra WSUS opnieuw is geïnstalleerd. Zie [Windows Server Update Services Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality)voor meer informatie.  

- Als u het besturings systeem van de site server bijwerkt, moet u ervoor zorgen dat [replicatie op basis van bestanden](../../plan-design/hierarchy/file-based-replication.md) in orde is voor de site. Controleer alle post vakken voor een achterstand op zowel verzendende als ontvangende sites. Als er veel vastgelopen of wachtende replicatie taken zijn, wacht u totdat ze zijn uitgeschakeld.<!-- SCCMDocs#1792 -->
    - Controleer op de verzendende site de **afzender. log**.
    - Controleer het logboek van de **wachtrij**op de ontvangende site.

#### <a name="after-upgrade"></a>Na de upgrade

- Het upgrade proces schakelt de Windows Deployment Services uit. Zorg ervoor dat deze service wordt gestart en wordt uitgevoerd voor de volgende site systeem rollen:  

    - Siteserver  

    - Beheerpunt  

    - Application Catalog-webservicepunt  

    - Application Catalog-websitepunt  

- Zorg ervoor dat de **Windows Process-activering** en **www/W3SVC-** Services zijn ingeschakeld en stel deze in op automatisch starten. Met het upgrade proces worden deze services uitgeschakeld, dus zorg ervoor dat ze worden uitgevoerd voor de volgende site systeem rollen:  

    - Siteserver  

    - Beheerpunt  

    - Application Catalog-webservicepunt  

    - Application Catalog-websitepunt  

- Zorg ervoor dat elke server die als host fungeert voor een site systeemrol blijft voldoen aan alle [vereisten](../../plan-design/configs/site-and-site-system-prerequisites.md). U moet bijvoorbeeld BITS of WSUS opnieuw installeren of specifieke instellingen configureren voor IIS.  

    Nadat de ontbrekende vereiste onderdelen zijn hersteld, start u de server nog een keer opnieuw op om te controleren of de services gestart en operationeel zijn.  

### <a name="unsupported-upgrade-scenarios"></a>Niet-ondersteunde upgrade scenario's

De volgende scenario's voor Windows Server-upgrades worden meestal gevraagd, maar worden niet ondersteund door Configuration Manager:  

- Windows Server 2008 naar Windows Server 2012 of hoger  

- Windows Server 2008 R2 naar Windows Server 2012  


## <a name="upgrade-the-os-of-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Het besturings systeem van clients bijwerken  

Configuration Manager ondersteunt een in-place upgrade van het besturings systeem voor Configuration Manager-clients in de volgende situaties:  

- Als Configuration Manager het resulterende Service Pack-niveau ondersteunt, wordt in-place upgrade naar een hoger Windows-Service Pack ondersteund.  

- In-place upgrade van Windows vanuit een ondersteunde versie naar Windows 10. Zie [Windows upgraden naar de nieuwste versie](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)voor meer informatie.  

- Build-to-build-onderhouds upgrades van Windows 10. Zie [Windows als een service beheren](../../../osd/deploy-use/manage-windows-as-a-service.md)voor meer informatie.  


## <a name="upgrade-sql-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> SQL Server bijwerken  

Configuration Manager ondersteunt een in-place upgrade van SQL Server op de site database server.

Zie [ondersteuning voor SQL Server versies](../../plan-design/configs/support-for-sql-server-versions.md)voor informatie over de versies van SQL Server die door Configuration Manager worden ondersteund.  

### <a name="upgrade-the-service-pack-version-of-sql-server"></a>De servicepackversie van SQL Server bijwerken

Als Configuration Manager nog steeds het SQL Server Service Pack-niveau ondersteunt, wordt het in-place upgrade van SQL Server naar een later service pack ondersteund.

Wanneer u meer dan een Configuration Manager site in een hiërarchie hebt, kan elke site een andere Service Pack versie van SQL Server uitvoeren. Er is geen beperking voor de volg orde waarin de Service Pack versie van SQL Server wordt bijgewerkt met sites.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Upgrade uitvoeren naar een nieuwe versie van SQL Server

Configuration Manager ondersteunt de in-place upgrade van SQL Server tot de volgende versies:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Dit omvat de upgrade van SQL Server Express naar een nieuwere versie van SQL Server Express op secundaire sites.

Wanneer u een upgrade uitvoert van de versie van SQL Server die als host fungeert voor de site database, moet u de SQL Server versie die op de sites wordt gebruikt, in de volgende volg orde bijwerken:

1. Voer eerst een upgrade uit van SQL Server op de centrale beheer site  

2. Upgrade secundaire sites voordat u een upgrade uitvoert van de bovenliggende primaire site van een secundaire site  

3. Voer het laatst een upgrade uit voor bovenliggende primaire sites. Deze sites omvatten zowel onderliggende primaire sites die rapporteren aan een centrale beheer site als zelfstandige primaire sites die de site op het hoogste niveau van een hiërarchie zijn.  

### <a name="sql-server-cardinality-estimation-level"></a>Schattings niveau SQL Server kardinaliteit

Wanneer u een upgrade uitvoert van een site database van een eerdere versie van SQL Server, behoudt de data base het bestaande schattings niveau van SQL-kardinaliteit, als dit ten minste is toegestaan voor dat exemplaar van SQL Server. Als u een upgrade uitvoert van SQL Server met een Data Base op een lager compatibiliteits niveau dan het toegestane niveau, wordt de data base automatisch ingesteld op het laagste compatibiliteits niveau dat is toegestaan door SQL Server.

De volgende tabel bevat de aanbevolen compatibiliteits niveaus voor Configuration Manager site databases:

|SQL Server-versie | Ondersteunde compatibiliteits niveaus | Aanbevolen niveau |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Voer de volgende SQL-query uit op de site database server om het compatibiliteits niveau voor de SQL Server-kardinaliteit te identificeren dat in gebruik is voor uw site database:  

```SQL
SELECT name, compatibility_level FROM sys.databases
```

Zie [ALTER data base Compatibility Level (Transact-SQL) (Engelstalig)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017)voor meer informatie over compatibiliteits niveaus voor SQL CE en hoe u deze kunt instellen.

Raadpleeg de volgende SQL Server artikelen voor meer informatie over het upgraden van SQL Server:  

- [Voer een upgrade uit naar SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Voer een upgrade uit naar SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Upgrade naar SQL Server 2014](/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  

### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Een upgrade uitvoeren voor SQL Server op de sitedatabaseserver  

1. Alle Configuration Manager-services op de site stoppen  

2. SQL Server upgraden naar een ondersteunde versie  

3. De Configuration Manager services opnieuw starten  

> [!NOTE]  
> Wanneer u de SQL Server editie die in gebruik is op de centrale beheer site wijzigt van standaard in een Data Center of onderneming, wordt de database partitie niet gewijzigd. Deze database partitie beperkt het aantal clients dat door de hiërarchie wordt ondersteund.