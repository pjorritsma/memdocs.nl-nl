---
title: Controle lijst voor 1610
titleSuffix: Configuration Manager
description: Meer informatie over de acties die u moet uitvoeren voordat u bijwerkt naar Configuration Manager versie 1610.
ms.date: 06/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 25d0302c4c35f2c66ce06febde63809b4a11116c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709752"
---
# <a name="checklist-for-installing-update-1610-for-configuration-manager"></a>Controle lijst voor het installeren van update 1610 voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u de huidige vertakking van Configuration Manager gebruikt, kunt u de update in de console installeren voor versie 1610 om uw hiërarchie bij te werken vanuit versie 1606. Als uw hiërarchie versie 1511, 1602 of 1606 uitvoert, kunt u bijwerken naar versie 1610.

Als u de update voor versie 1610 wilt downloaden, moet u een site systeemrol voor het service verbindings punt gebruiken op de site op het hoogste niveau van uw hiërarchie. Dit kan in de online-of offline modus zijn. Nadat uw hiërarchie het update pakket van micro soft heeft gedownload, kunt u het vinden in de **console &gt; onder &gt; beheer &gt; overzicht Cloud Services updates en onderhoud**.

-   Wanneer de update wordt weer gegeven als **beschikbaar**, is de update gereed voor installatie. Voordat u versie 1610 installeert, raadpleegt u de volgende informatie [over het installeren van update 1610](#about-installing-update-1610) en de [controle lijst](#checklist) voor configuraties die moeten worden gemaakt voordat de update wordt gestart.

-   Als de update wordt weer gegeven als **downloaden** en niet wordt gewijzigd, controleert u de **hman. log** en **dmpdownloader. log** op fouten.

    -   Normaal gesp roken kunt u de **SMS_Executive** -service op de site server ook opnieuw starten om het downloaden van de herdistributie bestanden van de update opnieuw te starten.

    -   Een ander algemeen Download probleem doet zich voor wanneer de instellingen van `silverlight.dlservice.microsoft.com` de `download.microsoft.com`proxy server downloaden van en niet verhinderen.

Zie [updates en onderhoud in de console](updates.md#bkmk_inconsole)voor meer informatie over het installeren van updates.

Voor informatie over de versies van de Current Branch, Zie [basis lijn-en update versies](updates.md#bkmk_Baselines) in [updates voor Configuration Manager](updates.md).

## <a name="about-installing-update-1610"></a>Over het installeren van update 1610

**Sites**  
Update 1610 kan alleen worden geïnstalleerd op de site op het hoogste niveau van uw hiërarchie. Dit betekent dat u de installatie start vanaf uw centrale beheer site als u er een hebt of van uw zelfstandige primaire site. Nadat de update is geïnstalleerd op de site op het hoogste niveau, hebben onderliggende sites het volgende gedrag van de update:

-   De update wordt automatisch geïnstalleerd op onderliggende primaire sites nadat de installatie van de update is voltooid op de centrale beheer site. U kunt service Windows gebruiken om te controleren wanneer een site updates installeert. Vóór versie 1606 werden service Windows onderhouds Vensters genoemd. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.

-   U moet secundaire sites hand matig bijwerken vanuit de Configuration Manager-console nadat de primaire bovenliggende site de installatie van de update heeft voltooid. Het automatisch bijwerken van secundaire siteservers wordt niet ondersteund.

**Sitesysteemrollen:**  
Wanneer de update wordt geïnstalleerd op de site server, worden de site systeem rollen die zijn geïnstalleerd op de site server en die die zijn geïnstalleerd op externe computers automatisch bijgewerkt. Voordat u de update installeert, moet u ervoor zorgen dat elke site systeem server voldoet aan eventuele nieuwe vereisten voor de bewerking met de nieuwe update versie.

**Configuration Manager-consoles:**   
De eerste keer dat u een Configuration Manager-console gebruikt nadat de update is voltooid, wordt u gevraagd die console bij te werken. Hiertoe moet u Configuration Manager Setup uitvoeren op de computer die als host fungeert voor de-console en vervolgens de optie kiezen om de-console bij te werken. U kunt installeren van de update naar de console beter niet uitstellen.



## <a name="checklist"></a>Controlelijst

**Zorg ervoor dat op alle sites een ondersteunde versie van Configuration Manager wordt uitgevoerd:** Voordat u begint met de installatie van update 1610, moet op elke site in de hiërarchie dezelfde versie van Configuration Manager worden uitgevoerd: versie 1511, 1602 of 1606.

**Bekijk de status van uw Software Assurance-of gelijkwaardige abonnements rechten:**   
U moet beschikken over een overeenkomst voor actieve Software Assurance (SA) om update 1610 te installeren. Wanneer u versie 1610 installeert, hebt u de optie op het tabblad **licenties** om de **verval datum van uw Software Assurance**te bevestigen.

Dit is een optionele waarde die u kunt opgeven als een handige herinnering voor de verval datum van uw licentie, die wordt weer gegeven wanneer u toekomstige updates installeert. Als u Configuration Manager hebt geïnstalleerd vanaf de baseline media van versie 1606, hebt u deze waarde mogelijk eerder tijdens de installatie opgegeven of op het tabblad **licenties** van de **hiërarchie-instellingen** na de installatie van de site.

Zie [Licentiëring en vertakkingen voor Configuration Manager](../../understand/learn-more-editions.md)voor meer informatie.

**Geïnstalleerde Microsoft .NET versies controleren op site systeem servers:** Wanneer een site update 1610 installeert, installeert Configuration Manager automatisch .NET Framework 4.5.2 op elke computer die als host fungeert voor een van de volgende site systeem rollen wanneer .NET Framework 4,5 of hoger nog niet is geïnstalleerd:

-   Proxypunt voor inschrijving
-   Inschrijvingspunt
-   Beheerpunt
-   Serviceverbindingspunt

Met deze installatie kan de site systeem server de status opnieuw opstarten in behandeling hebben en fouten melden aan de Configuration Manager onderdeel status viewer. Daarnaast kunnen de .NET-toepassingen op de server wille keurige fouten ondervinden totdat de server opnieuw is opgestart.

Zie voor meer informatie [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).

**De site- en hiërarchiestatus bekijken en controleren of er geen onopgeloste problemen zijn:** voordat u een site bijwerkt, dient u alle operationele problemen voor de siteserver, de sitedatabaseserver, en sitesysteemrollen die op externe computers zijn geïnstalleerd, op te lossen. De update van een site kan mislukken door bestaande operationele problemen.

Zie [waarschuwingen en het status systeem voor Configuration Manager gebruiken](use-alerts-and-the-status-system.md)voor meer informatie.

**Bestands-en gegevens replicatie tussen sites controleren:** Zorg ervoor dat bestands-en database replicatie tussen sites operationeel en actueel is. Vertragingen of achterstanden in een van beide kunnen leiden tot een soepele, geslaagde update.
Voor databasereplicatie kunt u Replication Link Analyzer gebruiken om u te helpen bij het oplossen van problemen voordat u de update start.

Zie [Replication link Analyzer](monitor-replication.md#BKMK_RLA) in het onderwerp [database replicatie bewaken](monitor-replication.md) voor meer informatie.

**Installeer alle toepasselijke kritieke updates voor besturings systemen op computers die de site, de site database server en externe site systeem rollen hosten:** Installeer alle essentiële updates voor elk toepasselijk site systeem voordat u een update voor Configuration Manager installeert. Als voor een update die u installeert, opnieuw moet worden opgestart, start u de betreffende computers opnieuw op voordat u de Configuration Manager Update start.

**Database replica's uitschakelen voor beheer punten op primaire sites:**   
Configuration Manager een primaire site met een database replica voor beheer punten is ingeschakeld, kan niet worden bijgewerkt. Schakel database replicatie uit voordat u een update voor Configuration Manager installeert.

Zie [database replica's voor beheer punten voor Configuration Manager](../deploy/configure/database-replicas-for-management-points.md)voor meer informatie.

**Stel SQL Server AlwaysOn-beschikbaarheids groepen in op hand matige failover:**   
Voordat u updates installeert, zoals versie 1610, moet u ervoor zorgen dat de beschikbaarheids groep is ingesteld op hand matige failover. Nadat de site is bijgewerkt, kunt u de failover herstellen naar automatisch. Zie [SQL Server AlwaysOn voor een site database](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie.

**Configureer software-update punten die gebruikmaken van Nlb's:**   
Configuration Manager kan geen site bijwerken die gebruikmaakt van een NLB-cluster (Network Load Balancing) om software-update punten te hosten.

Als u NLB-clusters voor software-update punten gebruikt, moet u Windows Power shell gebruiken om het NLB-cluster te verwijderen.
Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md)voor meer informatie.

**Alle site-onderhouds taken op elke site uitschakelen gedurende de duur van de installatie van de update op die site:**   
Voordat u de update installeert, moet u de onderhouds taak van de site uitschakelen die kan worden uitgevoerd op het moment dat het update proces actief is. Dit omvat, maar is niet beperkt tot het volgende:

-   Back-upserver van site
-   Verouderde clientbewerkingen verwijderen
-   Verouderde detectiegegevens verwijderen

Wanneer een onderhoudstaak van de sitedatabase wordt uitgevoerd tijdens de installatie van updates, kan de installatie van de update mislukken. Voordat u een taak uitschakelt, registreert u het schema van de taak zodat u de configuratie ervan kunt herstellen nadat de update is geïnstalleerd.

Zie [onderhouds taken voor Configuration Manager](maintenance-tasks.md) en [referentie voor onderhouds taken voor Configuration Manager](reference-for-maintenance-tasks.md)voor meer informatie.

**Antivirus software op de Configuration Manager servers tijdelijk stoppen:** Voordat u een site bijwerkt, moet u ervoor zorgen dat u de antivirus software op de Configuration Manager-servers hebt gestopt. <!--SMS.503481-->

**Een back-up maken van de sitedatabase op de centrale beheersite en de primaire site:** maak een back-up van de sitedatabase voordat u de site bijwerkt, om ervoor te zorgen dat u over een goede back-up beschikt voor herstel na noodgevallen.

Zie [back-up en herstel voor Configuration Manager](backup-and-recovery.md)voor meer informatie.

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](install-in-console-updates.md#bkmk_step2) from **Before you install an in-console update**.
-->

**Plan voor het testen van de client:**   
Wanneer u een update installeert die de-client bijwerkt, kunt u de nieuwe client update in de pre-productie testen voordat u deze implementeert en een upgrade uitvoert voor al uw actieve clients.

Als u deze optie wilt gebruiken, moet u uw site configureren voor ondersteuning van automatische upgrades voor pre-productie voordat u begint met de installatie van de update.

Zie [clients bijwerken](../../clients/manage/upgrade/upgrade-clients.md) en [Client upgrades testen in een pre-productie verzameling](../../clients/manage/upgrade/test-client-upgrades.md)voor meer informatie.

**Het gebruik van service Windows plannen om te bepalen wanneer site servers updates installeren:**   
U kunt service Windows gebruiken om een periode te definiëren gedurende welke updates op een site server kunnen worden geïnstalleerd.

Hiermee kunt u bepalen wanneer de sites in uw hiërarchie de update installeren. Vóór versie 1606 werden service Windows onderhouds Vensters genoemd. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.

**Voer de prerequisite Checker voor Setup uit:**   
Wanneer de update in de-console wordt weer gegeven als **beschikbaar,** kunt u de prerequisite Checker onafhankelijk uitvoeren voordat u de update installeert. (Wanneer u de update op de site installeert, wordt prerequisite Checker opnieuw uitgevoerd.)

Als u een controle op vereisten wilt uitvoeren vanuit de-console, gaat u naar **beheer > overzicht > Cloud Services > updates en onderhoud.** Klik vervolgens met de rechter muisknop op **Configuration Manager Update pakket 1610**en kies vervolgens **controle op vereisten uitvoeren**.

Zie **stap 3: de prerequisite Checker uitvoeren voordat u een update installeert** in het onderwerp [updates in de console installeren voor Configuration Manager](install-in-console-updates.md)voor meer informatie over het starten en vervolgens controleren van de controle op vereisten.

> [!IMPORTANT]  
> Wanneer de prerequisite Checker onafhankelijk wordt uitgevoerd of als onderdeel van een update-installatie, werkt het proces een aantal product bron bestanden bij die worden gebruikt voor site-onderhouds taken. Daarom moet u na het uitvoeren van de prerequisite Checker, maar voordat u de 1610-update installeert, **Setupwpf. exe** (Configuration Manager Setup) uitvoeren vanaf de cd. Meest recente map op de site server.

**Sites bijwerken:** u kunt nu de installatie van de update voor uw hiërarchie starten. Zie [updates in de console installeren](install-in-console-updates.md#bkmk_install) voor meer informatie over het installeren van de update.

U wordt aangeraden de update voor elke site buiten kantoor uren te installeren, wanneer het installatie proces van de update en de bijbehorende acties voor het opnieuw installeren van site onderdelen en site systeem rollen het minste effect heeft op uw zakelijke activiteiten.

Zie [updates voor Configuration Manager](updates.md)voor meer informatie.
