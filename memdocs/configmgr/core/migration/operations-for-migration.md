---
title: Migratie bewerkingen
titleSuffix: Configuration Manager
description: Maak en voer taken uit om gegevens en clients te migreren naar Configuration Manager huidige vertakking.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a93269fc50c7bb39cd47f10e448d30742fc8ab22
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720917"
---
# <a name="operations-for-migrating-to-configuration-manager-current-branch"></a>Bewerkingen voor de migratie naar Configuration Manager huidige vertakking

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor migratie in Configuration Manager kunt u gegevens en clients migreren nadat u gegevens hebt verzameld van een bron site in een ondersteunde bron hiërarchie. Gebruik de informatie in de volgende secties om migratie taken te maken en uit te voeren om gegevens en clients te migreren en het migratie proces te volt ooien.  

-   [Migratietaken maken en bewerken](#Create_Edit_migration_Jobs)  

-   [Migratie taken uitvoeren](#Run_Migration_Jobs)  

-   [Een gedeeld distributiepunt bijwerken of opnieuw toewijzen](#BKMK_ProcUpgrdSS)  

-   [Migratieactiviteiten in de werkruimte Migratie bewaken](#Monitor_MIgration)  

-   [Clients migreren](#BKMK_MigrateClients)  

-   [Migratie volt ooien](#Complete_Migration)  

##  <a name="create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a>Migratie taken maken en bewerken  
 Gebruik de volgende procedures om taken voor gegevens migratie te maken, de uitsluitings lijst te bewerken voor migratie taken op basis van verzamelingen, gedeelde distributie punten in te stellen en planningen voor migratie taken te bewerken.  

> [!NOTE]  
>  De volgende procedure voor het maken van een migratie taak die door verzamelingen wordt gemigreerd, is alleen van toepassing op bron hiërarchieën waarop een ondersteunde versie van Configuration Manager 2007 wordt uitgevoerd. Het type migratie taak op basis van verzameling is niet beschikbaar wanneer u migreert van een System Center 2012-Configuration Manager of Configuration Manager huidige branch-bron hiërarchie.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Een migratie taak maken om te migreren op basis van verzamelingen  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit en kies **migratie taken**.  

3.  Kies op het tabblad **Start** in de groep **maken** de optie **migratie taak maken**.  

4.  Stel op de pagina **Algemeen** van de wizard Migratie taak maken het volgende in en kies vervolgens **OK**:  

    -   Geef een naam op voor de migratietaak.  

    -   Selecteer **Verzamelingmigratie** in de vervolgkeuzelijst **Type taak**.  

5.  Stel op de pagina **verzamelingen selecteren** het volgende in en kies **volgende**:  

    -   Selecteer de verzamelingen die u wilt migreren.  

    -   Als u alleen verzamelingen wilt migreren en niet de objecten die aan deze verzamelingen zijn gekoppeld, schakelt u **objecten migreren die zijn gekoppeld aan de opgegeven verzamelingen**uit. Als u deze optie uitschakelt, worden er geen gekoppelde objecten gemigreerd in deze taak en kunt u stap 6 en 7 overs Laan.  

6.  Schakel op de pagina **objecten selecteren** alle object typen of specifieke beschik bare objecten uit die u niet wilt migreren. Standaard worden alle gekoppelde objecttypen en beschikbare objecten geselecteerd. Kies **Volgende**.  

7.  Wijs op de pagina **inhoud eigendom** het eigendom van de inhoud van elke vermelde bron site toe aan een site in de doel hiërarchie en kies vervolgens **volgende**.  

8.  Selecteer op de pagina **beveiligings bereik** een of meer op rollen gebaseerde beheer beveiligingsbereiken die moeten worden toegewezen aan de objecten die moeten worden gemigreerd in deze migratie taak en klik vervolgens op **volgende**.  

9. Stel op de pagina **beperkende verzameling** een verzameling in van de doel hiërarchie om het bereik van elke vermelde verzameling te beperken en kies vervolgens **volgende**. Als er geen verzamelingen worden weer gegeven, kiest u **volgende**.  

10. Wijs op de pagina **vervanging van site codes** een site code uit de doel hiërarchie toe om de Configuration Manager 2007-site code voor elke vermelde verzameling te vervangen. Klik vervolgens op **volgende**. Als er geen verzamelingen worden weer gegeven, kiest u **volgende**.  

11. Kies op de pagina **gegevens controleren** de optie **opslaan in bestand** om de weer gegeven informatie op te slaan zodat u deze later kunt bekijken. Wanneer u klaar bent om door te gaan, kiest u **volgende**.  

12. Stel op de pagina **instellingen** de optie in wanneer de migratie taak wordt uitgevoerd, kies alle extra instellingen die u nodig hebt voor deze migratie taak en kies vervolgens **volgende**.  

13. Bevestig de instellingen en voltooi de wizard.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Een migratie taak maken om te migreren op basis van objecten  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit en kies **migratie taken**.  

3.  Kies op het tabblad **Start** in de groep **maken** de optie **migratie taak maken**.  

4.  Stel op de pagina **Algemeen** van de wizard Migratie taak maken het volgende in en kies **volgende**:  

    -   Geef een naam op voor de migratietaak.  

    -   Selecteer **Objectmigratie** in de vervolgkeuzelijst **Type taak**.  

5.  Selecteer op de pagina **Objecten selecteren** de objecttypen die u wilt migreren. Standaard worden alle beschikbare objecten geselecteerd voor elk objecttype dat u selecteert.  

6.  Wijs op de pagina **inhoud eigendom** het eigendom van de inhoud van elke vermelde bron site toe aan een site in de doel hiërarchie en kies vervolgens **volgende**. Als er geen bron sites worden weer gegeven, kiest u **volgende**.  

7.  Selecteer op de pagina **beveiligings bereik** een of meer op rollen gebaseerde beheer beveiligingsbereiken die moeten worden toegewezen aan de objecten in deze migratie taak en klik vervolgens op **volgende**.  

8.  Kies op de pagina **gegevens controleren** de optie **opslaan in bestand** om de weer gegeven informatie op te slaan zodat u deze later kunt bekijken. Wanneer u klaar bent om door te gaan, kiest u **volgende**.  

9. Stel in op de pagina **instellingen** wanneer de migratie taak wordt uitgevoerd en kies eventuele aanvullende instellingen die u nodig hebt voor deze migratie taak. Kies vervolgens **volgende**.  

10. Bevestig de instellingen en voltooi de wizard.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Een migratie taak maken om gewijzigde objecten te migreren  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit en kies **migratie taken**.  

3.  Kies op het tabblad **Start** in de groep **maken** de optie **migratie taak maken**.  

4.  Stel op de pagina **Algemeen** van de wizard Migratie taak maken het volgende in en kies **volgende**:  

    -   Geef een naam op voor de migratietaak.  

    -   Selecteer in de vervolg keuzelijst **type taak** de optie **objecten gewijzigd na migratie**.  

5.  Selecteer op de pagina **Objecten selecteren** de objecttypen die u wilt migreren. Standaard worden alle beschikbare objecten geselecteerd voor elk objecttype dat u selecteert.  

6.  Wijs op de pagina **inhoud eigendom** het eigendom van de inhoud van elke vermelde bron site toe aan een site in de doel hiërarchie en kies vervolgens **volgende**. Als er geen bron sites worden weer gegeven, kiest u **volgende**.  

7.  Selecteer op de pagina **beveiligings bereik** een of meer op rollen gebaseerde beheer beveiligingsbereiken die moeten worden toegewezen aan de objecten in deze migratie taak en klik vervolgens op **volgende**.  

8.  Kies op de pagina **gegevens controleren** de optie **opslaan in bestand** om de weer gegeven informatie op te slaan zodat u deze later kunt bekijken. Wanneer u klaar bent om door te gaan, kiest u **volgende**.  

9. Stel in op de pagina **instellingen** wanneer de migratie taak wordt uitgevoerd en kies eventuele aanvullende instellingen die u nodig hebt voor deze migratie taak. In tegens telling tot de andere typen migratie taken moet deze migratie taak de eerder gemigreerde objecten in de Configuration Manager-Data Base overschrijven. Kies **Volgende**.  

10. Bevestig de instellingen en voltooi de wizard.  

###  <a name="modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a>De uitsluitings lijst voor migratie wijzigen  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Kies in de werk ruimte **beheer** de optie **migratie** om toegang te krijgen tot de uitsluitings lijst. U kunt de uitsluitingenlijst ook openen vanuit het knooppunt **Bronhiërarchie** of **Migratietaken** .  

3.  Klik op het tabblad **Start** in de groep **migratie** op **uitsluitingen lijst bewerken**.  

4.  Selecteer in het dialoog venster **uitsluitingen lijst bewerken** het uitgesloten object dat u wilt verwijderen uit de uitsluitings lijst en kies vervolgens **verwijderen**.  

5.  Kies **OK** om de wijzigingen op te slaan en de bewerking te volt ooien. Als u de huidige wijzigingen wilt annuleren en alle objecten wilt herstellen die u hebt verwijderd, kiest u **Annuleren**en kiest u **Nee**. Op deze manier maakt u de verwijdering van de objecten ongedaan en sluit u het dialoogvenster **Uitsluitingenlijst bewerken** .  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Distributie punten delen vanuit de bron hiërarchie  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit, kies **bron hiërarchie**en selecteer de bron site die u wilt instellen.  

3.  Klik op het tabblad **Start** in de groep **bron site** op **configureren**.  

4.  Selecteer in het dialoog venster **bron site referenties** de optie **deling van distributie punt inschakelen voor de server van de bron site**en klik vervolgens op **OK**.  

5.  Wanneer het verzamelen van gegevens is voltooid, kiest u **sluiten**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>De planning van een migratie taak wijzigen  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit en kies **migratie taken**.  

3.  Kies de migratie taak die u wilt wijzigen. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

4.  Selecteer in de eigenschappen van de migratie taak het tabblad **instellingen** , wijzig de uitvoerings tijd voor de migratie taak en klik vervolgens op **OK**.  

##  <a name="run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Migratietaken uitvoeren  
 Gebruik de volgende procedure om een migratietaak uit te voeren die nog niet is gestart.  


1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit en kies **migratie taken**.  

3.  Kies de migratie taak die u wilt uitvoeren. Klik op het tabblad **Start** in de groep **migratie taak** op **starten**.  

4.  Kies **Ja** om de migratie taak te starten.  

##  <a name="upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a>Een gedeeld distributie punt bijwerken of opnieuw toewijzen  
 U kunt een ondersteund distributie punt bijwerken dat wordt gedeeld vanaf een Configuration Manager 2007-bron site (of een ondersteund distributie punt dat wordt gedeeld vanaf een Configuration Manager-bron site opnieuw toewijzen) als een distributie punt in de doel hiërarchie.  

> [!IMPORTANT]  
>  Voordat u een Configuration Manager 2007-vertakkings distributiepunt bijwerkt, moet u de Configuration Manager 2007-client software verwijderen van de computer met het vertakkings distributiepunt. Als de Configuration Manager 2007-client software wordt geïnstalleerd wanneer u het distributie punt probeert bij te werken, mislukt de upgrade en wordt de inhoud die eerder was geïmplementeerd op het vertakkings distributiepunt verwijderd van de computer.  

> [!CAUTION]  
>  Wanneer u een gedeeld distributie punt bijwerkt of opnieuw toewijst, worden de site systeemrol en site systeem computer van het distributie punt verwijderd van de bron site en als een distributie punt toegevoegd aan de site in de doel hiërarchie die u selecteert.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Een gedeeld distributiepunt bijwerken of opnieuw toewijzen  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit en kies vervolgens **bron hiërarchie**.  

3.  Selecteer de site die eigenaar is van het distributie punt dat u wilt bijwerken, kies het tabblad **gedeelde distributie punten** en selecteer het in aanmerking komende distributie punt dat u wilt bijwerken of opnieuw toewijzen.  

4.  Kies op het tabblad **distributie punt** in de groep **distributie punt** de optie **opnieuw toewijzen**.  

5.  Geef de instellingen op in de wizard gedeeld distributie punt opnieuw toewijzen, zoals u een nieuw distributie punt voor de doel hiërarchie installeert, met de volgende toevoeging:  

    -   Bekijk op de pagina **inhouds conversie** de richt lijnen over de benodigde ruimte om de bestaande inhoud te converteren. Controleer vervolgens op de pagina **stations-instellingen** van de wizard of het station van de geselecteerde distributiepunt computer de vereiste hoeveelheid beschik bare schijf ruimte heeft.  

6.  Bevestig de instellingen en voltooi de wizard.  

##  <a name="monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a>Migratie activiteiten in de werk ruimte migratie bewaken  
 Gebruik de Configuration Manager-console om de migratie te bewaken.  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit en kies **migratie taken**.  

3.  Kies de migratie taak die u wilt bewaken.  

4.  Bekijk de details over en status van de geselecteerde migratietaak op de tabbladen voor **Samenvatting** en **Objecten in taak**.  

##  <a name="migrate-clients"></a><a name="BKMK_MigrateClients"></a> Clients migreren  
 Nadat u gegevens voor clients tussen hiërarchieën hebt gemigreerd, maar voordat u de migratie voltooit, moet u de migratie van clients naar de doel hiërarchie plannen. De migratie van clients tussen hiërarchieën omvat het verwijderen van de Configuration Manager-client software van computers die zijn toegewezen aan de bron hiërarchie en het installeren van de Configuration Manager-client software vanuit de doel hiërarchie. Wanneer u de client vanuit de doelhiërarchie installeert, wijst u de client ook aan een primaire site in die hiërarchie toe. Zie [een strategie voor client migratie plannen](../../core/migration/planning-a-client-migration-strategy.md)voor meer informatie over het migreren van clients.  

##  <a name="finish-migration"></a><a name="Complete_Migration"></a>Migratie volt ooien  
 Gebruik deze procedure om de migratie vanuit de bron hiërarchie te volt ooien.  

1.  Klik in de Configuration Manager-console op **beheer**.  

2.  Vouw in de werk ruimte **beheer** het knoop punt **migratie**uit en kies vervolgens **bron hiërarchie**.  

3.  Selecteer voor een Configuration Manager 2007-bron hiërarchie een bron site die zich op het onderste niveau van de bron hiërarchie bevindt. Selecteer de beschik bare bron site voor een System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron hiërarchie.  

4.  Klik op het tabblad **Start** in de groep **opschonen** op geen **gegevens meer verzamelen**.  

5.  Kies **Ja** om de actie te bevestigen.  

6.  Voor een Configuration Manager 2007-bron hiërarchie moet u voordat u verdergaat met de volgende stap, stap 3, 4 en 5 herhalen. Door loop deze stappen op elke site in de hiërarchie, van de onderkant van de hiërarchie naar boven. Ga door naar de volgende stap voor een System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron hiërarchie.  

7.  Klik op het tabblad **Start** in de groep **opschonen** op **migratie gegevens opruimen**.  

8.  Selecteer in het dialoog venster **migratie gegevens opruimen** in de vervolg keuzelijst **bron hiërarchie** de site code en site server van de site op het hoogste niveau van de bron hiërarchie, en kies vervolgens **OK**.  

9. Kies **Ja** om het migratie proces voor de bron hiërarchie te volt ooien.  
