---
title: Onderhoud van software-updates
titleSuffix: Configuration Manager
description: Als u updates in Configuration Manager wilt behouden, kunt u de WSUS-opschoon taak plannen of u kunt deze hand matig uitvoeren.
author: mestew
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 560b432bb90f99207fd15bc07e7aff98ffd59ebf
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719783"
---
# <a name="software-updates-maintenance"></a>Onderhoud van software-updates

*Van toepassing op: Configuration Manager (huidige vertakking)*

U kunt de WSUS-opschoon taken plannen en uitvoeren vanuit de Configuration Manager-console vanuit de eigenschappen van de software-update punt component. Wanneer u voor het eerst selecteert om de WSUS-opschoon taak uit te voeren, wordt deze uitgevoerd na de volgende synchronisatie van de software-updates.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Een WSUS-opschoontaak plannen en uitvoeren

Voer de volgende stappen uit om de WSUS-opschoon taak te plannen:

1. Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **site configuratie** > **sites**.
2. Selecteer de site boven aan uw Configuration Manager-hiërarchie.

3. Klik op **Siteonderdelen configureren** in de groep **Instellingen** . Klik vervolgens op **Software-updatepunt** om Eigenschappen van software-updatepuntcomponent te openen.  

4. Bekijk het **vervangings gedrag**. Wijzig het gedrag als dat nodig is.

   ![scherm opname van vervangings gedrag](media/supersedence-behavior.png)

5. Klik op het tabblad **vervangings regels** , selecteer **wizard WSUS-opschoning uitvoeren**. In versie 1806 wordt de naam van de optie gewijzigd om **WSUS-opschoning uit te voeren na de synchronisatie**.

6. Klik op **OK** (Klik op **sluiten** als u versie 1806).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Gedrag van WSUS-opschoning in versie 1802 en lager

Vóór Configuration Manager versie 1806 wordt met de optie WSUS Cleanup het volgende item uitgevoerd:

- De optie **verlopen updates** van de WSUS-opschoon wizard op de WSUS-server op het hoogste niveau.

  ![Scherm opname van verlopen WSUS-update opruimen](media/wsus-cleanup-expired.PNG)

- Een opschoon bewerking voor de configuratie-items van software-updates in de Configuration Manager-Data Base wordt elke zeven dagen uitgevoerd en verwijdert overbodige updates van de-console.
  - Met deze opschoning worden verlopen updates van de Configuration Manager-console niet verwijderd als deze momenteel worden geïmplementeerd.

Er is nog steeds extra onderhoud nodig op de WSUS-Data Base op het hoogste niveau en alle andere WSUS-data bases in de omgeving. Zie voor meer informatie en instructies [de volledige hand leiding voor het blog bericht over micro soft WSUS en Configuration Manager sup-onderhoud](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) .

## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Gedrag van WSUS-opschoning vanaf versie 1806

Start versie 1806, de optie WSUS Cleanup vindt plaats na elke synchronisatie en voert de volgende opschoon items uit:
<!--1357898 -->

- De optie **verlopen updates** voor WSUS-servers op ca's en primaire sites.
  - WSUS-servers voor secundaire sites voeren geen WSUS-opschoning uit voor verlopen updates.
- Configuration Manager bouwt een lijst van vervangen updates vanuit de data base. De lijst is gebaseerd op het vervangings gedrag in de eigenschappen van de software-update punt component.
  - De update-configuratie-items die voldoen aan de criteria voor het vervangings gedrag zijn verlopen in de Configuration Manager-console.
  - De updates worden in WSUS afgewezen voor CA'S en primaire sites, maar niet voor secundaire sites.
- Een opschoon bewerking voor de configuratie-items van software-updates in de Configuration Manager-Data Base wordt elke zeven dagen uitgevoerd en verwijdert overbodige updates van de-console.
  - Met deze opschoning worden verlopen updates van de Configuration Manager-console niet verwijderd als deze momenteel worden geïmplementeerd.

> [!NOTE]
> De "maanden dat moet worden gewacht voordat een vervangen update is verlopen" is gebaseerd op de aanmaak datum van de vervangende update. Als u bijvoorbeeld 2 maanden gebruikt voor deze instelling, worden updates die zijn vervangen, geweigerd in WSUS en verlopen in Configuration Manager wanneer de superceding-update 2 maanden oud is.

Alle WSUS-onderhoud moet hand matig worden uitgevoerd op de WSUS-data bases van de secundaire site. De volgende opties voor de **wizard WSUS-server opruimen** worden niet uitgevoerd op de ca's en primaire sites:

- Ongebruikte updates en update revisies
- Computers die geen verbinding maken met de server
- Overbodige update bestanden

  Zie voor meer informatie en instructies [de volledige hand leiding voor het blog bericht over micro soft WSUS en Configuration Manager sup-onderhoud](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) .

## <a name="wsus-cleanup-behavior-starting-in-version-1810"></a>Gedrag van WSUS-opschoning vanaf versie 1810

Vanaf versie 1810 kunt u vervangings regels voor onderdeel updates afzonderlijk opgeven van updates zonder onderdelen in de eigenschappen van de software-update punt component. De optie WSUS Cleanup vindt plaats na elke synchronisatie en voert de volgende opschoon items uit:
<!--2839349,3098809, 2977644-->

- De optie **verlopen updates** voor WSUS-servers op CAS-, primaire en secundaire sites.
- Configuration Manager bouwt een lijst van vervangen updates vanuit de data base. De lijst is gebaseerd op het vervangings gedrag in de eigenschappen van de software-update punt component.
  - De update-configuratie-items die voldoen aan de criteria voor het vervangings gedrag zijn verlopen in de Configuration Manager-console.
  - De updates worden in WSUS afgewezen voor CA'S, primaire en secundaire sites.
- Een opschoon bewerking voor de configuratie-items van software-updates in de Configuration Manager-Data Base wordt elke zeven dagen uitgevoerd en verwijdert overbodige updates van de-console.
  - Met deze opschoning worden verlopen updates van de Configuration Manager-console niet verwijderd als deze momenteel worden geïmplementeerd.

> [!NOTE]
> De "maanden dat moet worden gewacht voordat een vervangen update is verlopen" is gebaseerd op de aanmaak datum van de vervangende update. Als u bijvoorbeeld 2 maanden gebruikt voor deze instelling, worden updates die zijn vervangen, geweigerd in WSUS en verlopen in Configuration Manager wanneer de superceding-update 2 maanden oud is.

De volgende opties voor de **wizard WSUS-server opruimen** worden niet uitgevoerd op de ca's, de primaire en de secundaire site:

- Ongebruikte updates en update revisies
- Computers die geen verbinding maken met de server
- Overbodige update bestanden

  Zie voor meer informatie en instructies [de volledige hand leiding voor het blog bericht over micro soft WSUS en Configuration Manager sup-onderhoud](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) .

## <a name="wsus-cleanup-starting-in-version-1906"></a>WSUS-opschoning wordt gestart in versie 1906
<!--41101009-->

 U hebt extra WSUS-onderhouds taken die Configuration Manager kunnen uitvoeren om software-update punten goed te onderhouden. Naast het weigeren van verlopen updates in WSUS, kunt Configuration Manager niet-geclusterde indexen toevoegen aan de WSUS-data bases en verouderde updates verwijderen uit de WSUS-data bases. Het WSUS-onderhoud vindt plaats na elke synchronisatie.

### <a name="decline-expired-updates-in-wsus-according-to-supersedence-rules"></a>Verlopen updates in WSUS afwijzen volgens vervangings regels

Het weigeren van updates in WSUS verbetert de prestaties door deze updates te verwijderen uit de catalogussen die naar clients worden verzonden. Als u updates afwijst die Configuration Manager markeren als vervangen, minimaliseert u de catalogussen en verbetert u de prestaties.

1. Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **site configuratie** > **sites**.
2. Selecteer de site boven aan uw Configuration Manager-hiërarchie.
3. Klik op **Siteonderdelen configureren** in de groep Instellingen . Klik vervolgens op **Software-updatepunt** om Eigenschappen van software-updatepuntcomponent te openen.
4. Op het tabblad **onderhoud van WSUS** selecteert u **verlopen updates in WSUS afwijzen volgens de vervangings regels**.

### <a name="add-non-clustered-indexes-to-the-wsus-database-to-improve-wsus-cleanup-performance"></a>Niet-geclusterde indexen toevoegen aan de WSUS-Data Base voor het verbeteren van de prestaties van WSUS-opschoning

Het toevoegen van niet-geclusterde indexen verbetert de prestaties van de WSUS-opschoning die Configuration Manager.

1. Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **site configuratie** > **sites**.
2. Selecteer de site boven aan uw Configuration Manager-hiërarchie.
3. Klik op **Siteonderdelen configureren** in de groep Instellingen . Klik vervolgens op **Software-updatepunt** om Eigenschappen van software-updatepuntcomponent te openen.
4. Op het tabblad **onderhoud van WSUS** selecteert **u niet-geclusterde indexen toevoegen aan de WSUS-data base**.
5. Op elke SUSDB die wordt gebruikt door Configuration Manager worden indexen toegevoegd aan de volgende tabellen:
   - tbLocalizedPropertyForRevision
   - tbRevisionSupersedesUpdate

#### <a name="sql-permissions-for-creating-indexes"></a>SQL-machtigingen voor het maken van indexen

Wanneer de WSUS-data base zich op een externe SQL-Server bevindt, moet u mogelijk machtigingen toevoegen in SQL om indexen te maken. Het account dat wordt gebruikt voor verbinding met de WSUS-data base en het maken van de indexen kan variëren. Als u een [WSUS-server verbindings account opgeeft in de eigenschappen van het software-update punt](../get-started/install-a-software-update-point.md#wsus-server-connection-account), moet u ervoor zorgen dat het verbindings account de SQL-machtigingen heeft. Als u geen WSUS-server verbindings account opgeeft, moeten de SQL-machtigingen voor het computer account van de site server zijn vereist.

- Voor het maken van `ALTER` een index is machtiging vereist voor de tabel of weer gave. Het account moet lid zijn van de `sysadmin` vaste serverrol of de `db_ddladmin` en `db_owner` vaste database rollen. Zie [Create Index (Transact-SQL) (Engelstalig)](https://docs.microsoft.com/sql/t-sql/statements/create-index-transact-sql?view=sql-server-2017#permissions)voor meer informatie over het maken en indexeren van machtigingen.
- De `CONNECT SQL` Server machtiging moet aan het account worden verleend. Zie [granting server permissions (Transact-SQL) (Engelstalig)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017)voor meer informatie.

> [!NOTE]  
>  Als de WSUS-data base zich op een externe SQL-Server bevindt met een niet-standaard poort, worden er mogelijk geen indexen toegevoegd. U kunt een [server alias maken met behulp van SQL Server Configuration Manager](https://docs.microsoft.com/sql/database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client?view=sql-server-2017) voor dit scenario. Zodra de alias is toegevoegd en Configuration Manager een verbinding met de WSUS-Data Base kunt maken, worden er indexen toegevoegd.

### <a name="remove-obsolete-updates-from-the-wsus-database"></a>Verouderde updates verwijderen uit de WSUS-data base

Verouderde updates zijn niet-gebruikte updates en update revisies in de WSUS-data base. Over het algemeen wordt een update als verouderd beschouwd als deze niet meer in de [Microsoft Update catalogus](https://www.catalog.update.microsoft.com/) staat en niet als vereisten of afhankelijkheid nodig is voor andere updates.

1. Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **site configuratie** > **sites**.
2. Selecteer de site boven aan uw Configuration Manager-hiërarchie.
3. Klik op **Siteonderdelen configureren** in de groep Instellingen . Klik vervolgens op **Software-updatepunt** om Eigenschappen van software-updatepuntcomponent te openen.
4. Op het tabblad **onderhoud van WSUS** selecteert u **verouderde updates verwijderen uit de WSUS-data base**.
   - De verouderde update verwijdering mag Maxi maal 30 minuten worden uitgevoerd voordat deze wordt gestopt. Het wordt opnieuw opgestart nadat de volgende synchronisatie is uitgevoerd.  

#### <a name="sql-permissions-for-removing-obsolete-updates"></a>SQL-machtigingen voor het verwijderen van verouderde updates

Wanneer de WSUS-data base zich op een externe SQL-Server bevindt, heeft het computer account van de site server de volgende SQL-machtigingen nodig:

- De `db_datareader` en `db_datawriter` de vaste database rollen. Zie [functies op database niveau](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles?view=sql-server-2017#fixed-database-roles)voor meer informatie.
- De `CONNECT SQL` Server machtiging moet worden verleend aan het computer account van de site server. Zie [granting server permissions (Transact-SQL) (Engelstalig)](https://docs.microsoft.com/sql/t-sql/statements/grant-server-permissions-transact-sql?view=sql-server-2017)voor meer informatie.

#### <a name="wsus-cleanup-wizard"></a>Wizard WSUS opruimen

Vanaf versie 1906 worden de volgende opties voor de **wizard WSUS-server opruimen** niet uitgevoerd op de ca's, de primaire en de secundaire site:

- Computers die geen verbinding maken met de server
- Overbodige update bestanden

  Zie voor meer informatie en instructies [de volledige hand leiding voor het blog bericht over micro soft WSUS en Configuration Manager sup-onderhoud](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint/) .


### <a name="known-issues-for-version-1906"></a>Bekende problemen met versie 1906

Denkt u zich het volgende scenario eens in:
<!--5418148-->
- U gebruikt Configuration Manager versie 1906
- U hebt externe software-update punten die gebruikmaken van een interne Windows-Data Base
- In de **Eigenschappen van de software-update punt component**hebt u een van de volgende geselecteerde opties onder het tabblad **WSUS-onderhoud** :
   - Niet-geclusterde indexen toevoegen aan de WSUS-data base
   - Verouderde updates verwijderen uit de WSUS-data base

In dit scenario kan Configuration Manager de bovenstaande WSUS-onderhouds taken voor de externe software-update punten niet uitvoeren met een interne data base van Windows. Dit probleem doet zich voor omdat de interne data base van Windows geen externe verbindingen toestaat. U ziet de volgende fouten in de `WSyncMgr.log` op de site server:

```text
Indexing Failed. Could not connect to SUSDB.
SqlException thrown while connect to SUSDB in Server: <SUP.CONTOSO.COM>. Error Message: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server)
...
Could not Delete Obselete Updates because ConfigManager could not connect to SUSDB: A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections. (provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) UpdateServer: <SUP.CONTOSO.COM>
```

U kunt het probleem omzeilen door het WSUS-onderhoud voor de externe software-update punten te automatiseren met behulp van een interne data base van Windows. Zie [de volledige hand leiding voor micro soft WSUS en het onderhoud van Configuration Manager sup](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint)voor meer informatie en gedetailleerde stappen.

## <a name="updates-cleanup-log-entries"></a>Logboek vermeldingen voor het opschonen van updates

U kunt deze opschoning controleren door de bestand Wsyncmgr. log te bekijken voor de volgende vermeldingen:

- De weigering van vervangen updates in WSUS is voltooid wanneer u deze logboek vermelding ziet:`Cleanup processed <number> total updates and declined <number>`
- De WSUS-opschoning wordt gestart wanneer u deze vermelding ziet:`Calling WSUS Cleanup.`
- De WSUS-opruiming voor verlopen updates is voltooid wanneer u dit item ziet:`Successfully completed WSUS Cleanup.`
- Het opruimen van de Configuration Manager configuratie-items voor verlopen updates wordt gestart wanneer u deze vermelding ziet:`Deleting old expired updates...`
- Het opruimen van de Configuration Manager configuratie-items voor verlopen updates is voltooid wanneer u deze vermelding ziet:`Deleted <number> expired updates total`
