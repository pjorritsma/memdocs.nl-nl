---
title: Controle lijst voor 1606
titleSuffix: Configuration Manager
description: Meer informatie over de acties die u moet uitvoeren voordat u een update van Configuration Manager versie 1511 of 1602 naar versie 1606 uitvoert.
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 95da730a6978c235fcae6a1d05b7984486abdaeb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723080"
---
# <a name="checklist-for-installing-update-1606-for-configuration-manager"></a>Controle lijst voor het installeren van update 1606 voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Versie 1606 voor Configuration Manager huidige branch is een update die u kunt gebruiken om bij te werken vanaf versie 1511 of 1602.

Voordat u versie 1606 als update installeert, raadpleegt u de volgende informatie en controle lijst voor acties die u moet uitvoeren voordat u de update start.

Zie voor meer informatie over basislijn versies [basis lijn-en update versies](../../../core/servers/manage/updates.md#bkmk_Baselines) in [updates voor Configuration Manager](../../../core/servers/manage/updates.md).

## <a name="about-installing-update-1606"></a>Over het installeren van update 1606

Als *Update*kan 1606 alleen worden geïnstalleerd op de site op het hoogste niveau van uw hiërarchie. Dit betekent dat u de installatie start vanaf uw centrale beheer site als u er een hebt of van uw zelfstandige primaire site.  

- De update wordt automatisch geïnstalleerd op onderliggende primaire sites nadat de centrale beheer site de installatie van de update heeft voltooid. U kunt service Windows gebruiken om te controleren wanneer een site updates installeert. Vóór versie 1606 werden service Windows onderhouds Vensters genoemd. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.  

- U moet secundaire sites hand matig bijwerken vanuit de Configuration Manager-console nadat de primaire bovenliggende site is voltooid met het installeren van de update. Het automatisch bijwerken van secundaire siteservers wordt niet ondersteund.  

Wanneer de update wordt geïnstalleerd door de site server, worden site systeem rollen die zijn geïnstalleerd op de site server en die op externe computers zijn geïnstalleerd, automatisch bijgewerkt. Zorg er daarom voordat u de update installeert voor dat elke site systeem server voldoet aan eventuele nieuwe vereisten voor bewerkingen met de nieuwe update versie.  

De eerste keer dat u een Configuration Manager-console gebruikt nadat de update is geïnstalleerd, wordt u gevraagd die console bij te werken.  Hiertoe moet u Configuration Manager Setup uitvoeren op de computer die als host fungeert voor de-console en vervolgens de optie kiezen om de-console bij te werken. U kunt installeren van de update naar de console beter niet uitstellen.

**Bekende problemen voor deze update**   
De volgende problemen zijn van toepassing wanneer u de installatie status van het update pakket bekijkt:
- Bij het bijwerken van versie 1602 naar 1606 wordt met de stap **Update pakket payload** de status **niet gestart**weer gegeven, zelfs als de down load is voltooid.
- Bij het bijwerken van versie 1511 naar 1606, worden in sommige stappen de status **voltooid** weer gegeven, maar wordt er geen waarde voor de tijd van de **laatste update**weer geven.


## <a name="checklist"></a>Controlelijst  

**Zorg ervoor dat op alle sites een ondersteunde versie van Configuration Manager wordt uitgevoerd:**  Voordat u begint met de installatie van update 1606, moet op elke site server in de hiërarchie dezelfde versie van Configuration Manager worden uitgevoerd: versie 1511 of 1602.

**Geïnstalleerde Microsoft.NET-versies controleren op site systeem servers:** Wanneer een site update 1606 installeert, installeert Configuration Manager automatisch .NET Framework 4.5.2 op elke computer die als host fungeert voor een van de volgende site systeem rollen (als .NET Framework 4,5 of hoger nog niet is geïnstalleerd):  

- Proxypunt voor inschrijving  

- Inschrijvingspunt  

- Beheerpunt  

- Serviceverbindingspunt  

Met deze installatie kan de site systeem server de status opnieuw opstarten in behandeling hebben en fouten melden aan de Configuration Manager onderdeel status viewer. Bovendien kunnen .NET-toepassingen op de server mogelijk willekeurig mislukken totdat de server opnieuw is gestart.  

Zie [site-en site systeem vereisten](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)voor meer informatie.  

**De site- en hiërarchiestatus bekijken en controleren of er geen onopgeloste problemen zijn:** voordat u een site bijwerkt, dient u alle operationele problemen voor de siteserver, de sitedatabaseserver, en sitesysteemrollen die op externe computers zijn geïnstalleerd, op te lossen. De update van een site kan mislukken door bestaande operationele problemen.

Zie [waarschuwingen en het status systeem voor Configuration Manager gebruiken](../../../core/servers/manage/use-alerts-and-the-status-system.md)voor meer informatie.  

**Bestands- en databasereplicatie tussen sites controleren:**  zorg ervoor dat bestands- en databasereplicatie tussen sites operationeel en actueel is. Vertragingen of achterstanden in een van beide kunnen leiden tot een soepele, geslaagde update.    

Voor databasereplicatie kunt u Replication Link Analyzer gebruiken om u te helpen bij het oplossen van problemen voordat u de update start. Zie [over de Replication link Analyzer](monitor-replication.md#BKMK_RLA)voor meer informatie.  


**Installeer alle toepasselijke kritieke updates voor besturings systemen op computers die de site, de site database server en externe site systeem rollen hosten:** Installeer alle essentiële updates voor elk toepasselijk site systeem voordat u een update voor Configuration Manager installeert. Als een update die u installeert, vereist dat de computer opnieuw wordt opgestart, start de desbetreffende computers dan opnieuw op voordat u de upgrade start.  

**Database Replica's uitschakelen voor beheer punten op primaire sites:** Configuration Manager een primaire site met een database replica voor beheer punten is ingeschakeld, kan niet worden bijgewerkt. Schakel database replicatie uit voordat u een update voor Configuration Manager installeert.  

Zie [database replica's voor beheer punten voor Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)voor meer informatie.  

**Stel SQL Server AlwaysOn-beschikbaarheids groepen in op hand matige failover:**  
Voordat u updates installeert, zoals versie 1606, moet u ervoor zorgen dat de beschikbaarheids groep is ingesteld op hand matige failover. Nadat de site is bijgewerkt, kunt u de failover herstellen naar automatisch. Zie [SQL Server AlwaysOn voor een site database](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie.

**Configureer software-update punten die gebruikmaken van nlb's:** Configuration Manager kan geen site bijwerken die gebruikmaakt van een NLB-cluster (Network Load Balancing) om software-update punten te hosten.  

Als u NLB-clusters voor software-update punten gebruikt, moet u Windows Power shell gebruiken om het NLB-cluster te verwijderen.    

Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md)voor meer informatie.  

**Alle site-onderhouds taken op elke site uitschakelen gedurende de duur van de installatie van de update op die site:** Voordat u de update installeert, schakelt u site-onderhouds taken uit die mogelijk worden uitgevoerd op het moment dat het update proces actief is. Dit omvat, maar is niet beperkt tot het volgende:  

- Back-upserver van site  

- Verouderde clientbewerkingen verwijderen  

- Verouderde detectiegegevens verwijderen  

Wanneer een onderhoudstaak van de sitedatabase wordt uitgevoerd tijdens de installatie van updates, kan de installatie van de update mislukken. Voordat u een taak uitschakelt, registreert u het schema van de taak zodat u de configuratie ervan kunt herstellen nadat de update is geïnstalleerd.  

Zie [onderhouds taken voor Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) en [referentie voor onderhouds taken voor Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md)voor meer informatie. 

**Antivirus software op de Configuration Manager servers tijdelijk stoppen:** Voordat u een site bijwerkt, moet u ervoor zorgen dat u de antivirus software op de Configuration Manager-servers hebt gestopt. <!--SMS.503481--> 

**Een back-up maken van de sitedatabase op de centrale beheersite en de primaire site:** maak een back-up van de sitedatabase voordat u de site bijwerkt, om ervoor te zorgen dat u over een goede back-up beschikt voor herstel na noodgevallen.   

Zie [back-up en herstel voor Configuration Manager](backup-and-recovery.md)voor meer informatie.  

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

- You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

- Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

- A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

- Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

- If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**Plan voor het testen van de client:** Wanneer u een update installeert die de-client bijwerkt, kunt u de nieuwe client update in de pre-productie testen voordat u deze implementeert en een upgrade uitvoert voor al uw actieve clients.   

Als u wilt profiteren van deze optie, moet u uw site configureren voor ondersteuning van automatische upgrades voor pre-productie voordat u de installatie van de update start. Zie voor meer informatie [clients upgraden](../../../core/clients/manage/upgrade/upgrade-clients.md) en   
[Client upgrades testen in een pre-productie verzameling](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**Het gebruik van service Windows plannen om te bepalen wanneer site servers updates installeren:** U kunt service Windows gebruiken om een periode te definiëren gedurende welke updates op een site server kunnen worden geïnstalleerd.

Hiermee kunt u bepalen wanneer de sites in uw hiërarchie de update installeren.
Vóór versie 1606 werden service Windows onderhouds Vensters genoemd. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.  

**Prerequisite Checker uitvoeren:**  Voordat u update 1606 installeert, kunt u de prerequisite Checker onafhankelijk van de installatie van de update uitvoeren. Wanneer u de update op de site installeert, wordt prerequisite Checker opnieuw uitgevoerd.  

Zie **stap 3: de prerequisite Checker uitvoeren voordat u een update installeert** in het onderwerp [updates voor Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) voor meer informatie.  

> [!IMPORTANT]  
> Wanneer de prerequisite Checker onafhankelijk wordt uitgevoerd of als onderdeel van een update-installatie, werkt het proces een aantal product bron bestanden bij die worden gebruikt voor site-onderhouds taken. Daarom moet u na het uitvoeren van de prerequisite Checker, maar voordat u de 1606-update installeert, **Setupwpf. exe** (Configuration Manager Setup) uitvoeren vanaf de cd. Meest recente map op de site server.  

**Sites bijwerken:** u kunt nu de installatie van de update voor uw hiërarchie starten.  
U wordt aangeraden de update voor elke site buiten kantoor uren te installeren, wanneer het installatie proces van de update en de bijbehorende acties voor het opnieuw installeren van site onderdelen en site systeem rollen het minste effect heeft op uw zakelijke activiteiten.

Zie [updates voor Configuration Manager](../../../core/servers/manage/updates.md)voor meer informatie.  
