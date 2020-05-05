---
title: Controle lijst voor 1602
titleSuffix: Configuration Manager
description: Meer informatie over de acties die u moet uitvoeren voordat u een update uitvoert van Configuration Manager versie 1511 naar versie 1602.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: b330c4049dce06b1e47d1088993b09ec16e724a8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717858"
---
# <a name="checklist-for-installing-update-1602-for-configuration-manager"></a>Controle lijst voor het installeren van update 1602 voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u bijwerkt van Configuration Manager versie 1511 naar versie 1602, raadpleegt u de volgende informatie en controle lijst voor acties die u moet uitvoeren voordat u de update start.  

 **Over het installeren van update 1602:**  

 Update 1602 kan alleen op de site op het hoogste niveau van uw hiërarchie worden opgegeven. Dit betekent dat u de installatie start vanaf uw centrale beheer site als u er een hebt of van uw zelfstandige primaire site.  

-   De update wordt automatisch geïnstalleerd op onderliggende primaire sites nadat de centrale beheer site de installatie van de update heeft voltooid. U kunt onderhouds Vensters gebruiken om te controleren wanneer een site updates installeert. Vanaf de release van de 1602-update hebben onderhouds Vensters de naam van de *service Windows*gewijzigd. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.  

-   U moet secundaire sites hand matig bijwerken vanuit de Configuration Manager-console nadat de primaire bovenliggende site is voltooid met het installeren van de update. Automatische updates van secundaire site servers worden niet ondersteund.  

Wanneer de update wordt geïnstalleerd door de site server, worden site systeem rollen die zijn geïnstalleerd op de site server en die op externe computers zijn geïnstalleerd automatisch bijgewerkt. Zorg er daarom voordat u de update installeert voor dat elke site systeem server voldoet aan eventuele nieuwe vereisten voor bewerkingen met de nieuwe update versie.  

De eerste keer dat u een Configuration Manager-console gebruikt nadat de update is voltooid, wordt u gevraagd die console bij te werken. Hiertoe moet u Configuration Manager Setup uitvoeren op de computer die als host fungeert voor de-console en kiest u de optie om de-console bij te werken. U kunt installeren van de update naar de console beter niet uitstellen.  

 **Besproken**  

 **Zorg ervoor dat op alle sites een ondersteunde versie van Configuration Manager wordt uitgevoerd:**  Op elke site server in de hiërarchie moet Configuration Manager versie 1511 worden uitgevoerd voordat u de installatie van update 1602 kunt starten.  

 **Geïnstalleerde Microsoft .NET versies controleren op site systeem servers:** Wanneer een site update 1602 installeert, installeert Configuration Manager automatisch .NET Framework 4.5.2 op elke computer die als host fungeert voor een van de volgende site systeem rollen (als .NET Framework 4,5 of hoger nog niet is geïnstalleerd):  

-   Proxypunt voor inschrijving  

-   Inschrijvingspunt  

-   Beheerpunt  

-   Serviceverbindingspunt  

Met deze installatie kan de site systeem server de status opnieuw opstarten in behandeling hebben en fouten melden aan de viewer van de Configuration Manager onderdeel status. Daarnaast kunnen de .NET-toepassingen op de server wille keurige fouten ondervinden totdat de server opnieuw is opgestart.  

 Zie voor meer informatie [Site and site system prerequisites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).  

 **De site- en hiërarchiestatus bekijken en controleren of er geen onopgeloste problemen zijn:** voordat u een site bijwerkt, dient u alle operationele problemen voor de siteserver, de sitedatabaseserver, en sitesysteemrollen die op externe computers zijn geïnstalleerd, op te lossen. De update van een site kan mislukken door bestaande operationele problemen.  

Zie [waarschuwingen en het status systeem voor Configuration Manager gebruiken](../../../core/servers/manage/use-alerts-and-the-status-system.md)voor meer informatie.  

 **Bestands- en databasereplicatie tussen sites controleren:**  zorg ervoor dat bestands- en databasereplicatie tussen sites operationeel en actueel is. Vertragingen of achterstanden in een van beide kunnen leiden tot een soepele, geslaagde update.    

Voor databasereplicatie kunt u Replication Link Analyzer gebruiken om u te helpen bij het oplossen van problemen voordat u de update start.    

 Zie [over de Replication link Analyzer](monitor-replication.md#BKMK_RLA)voor meer informatie.  

 **Installeer alle toepasselijke kritieke updates voor besturings systemen op computers die de site, de site database server en externe site systeem rollen hosten:** Installeer alle essentiële updates voor elk toepasselijk site systeem voordat u een update voor Configuration Manager installeert. Als een update die u installeert, vereist dat de computer opnieuw wordt opgestart, start de desbetreffende computers dan opnieuw op voordat u de upgrade start.  

 **Database Replica's uitschakelen voor beheer punten op primaire sites:** Configuration Manager een primaire site met een database replica voor beheer punten is ingeschakeld, kan niet worden bijgewerkt. Schakel databasereplicatie uit voordat u:  

-   Maak een back-up van de site database om de upgrade van de data base te testen.  

-   Installeer een update voor Configuration Manager.  

Zie [database replica's voor beheer punten voor Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)voor meer informatie.  

 **Configureer software-update punten die gebruikmaken van nlb's:** Configuration Manager kan geen site bijwerken die gebruikmaakt van een NLB-cluster (Network Load Balancing) om software-update punten te hosten.  Als u NLB-clusters voor software-update punten gebruikt, moet u Windows Power shell gebruiken om het NLB-cluster te verwijderen.    

 Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md)voor meer informatie.  

 **Alle site-onderhouds taken op elke site uitschakelen gedurende de duur van de installatie van de update op die site:** Voordat u updates installeert, moet u de onderhouds taak van de site uitschakelen die kan worden uitgevoerd op het moment dat het update proces actief is. Deze taken omvatten (maar zijn niet beperkt) tot het volgende:  

-   Back-upserver van site  

-   Verouderde clientbewerkingen verwijderen  

-   Verouderde detectiegegevens verwijderen  

Wanneer een onderhoudstaak van de sitedatabase wordt uitgevoerd tijdens de installatie van updates, kan de installatie van de update mislukken. Voordat u een taak uitschakelt, registreert u het schema van de taak zodat u de configuratie ervan kunt herstellen nadat de update is geïnstalleerd.  

 Zie [onderhouds taken voor Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) en [referentie voor onderhouds taken voor Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md)voor meer informatie. 

**Antivirus software op de Configuration Manager servers tijdelijk stoppen:** Voordat u een site bijwerkt, moet u ervoor zorgen dat u de antivirus software op de Configuration Manager-servers hebt gestopt. <!--SMS.503481--> 

 **Maak een back-up van de site database op de centrale beheer site en primaire sites:** Voordat u een site bijwerkt, maakt u een back-up van de site database om ervoor te zorgen dat u een geslaagde back-up hebt voor herstel na nood gevallen.   

Zie [back-up en herstel voor Configuration Manager](backup-and-recovery.md)voor meer informatie.  

 **Back-up maken van een aangepast configuratie. MOF-bestand:** Als u een aangepast configuratie. MOF-bestand gebruikt voor het definiëren van gegevens klassen die u gebruikt met de hardware-inventaris, maakt u een back-up van dit bestand voordat u de site bijwerkt. Nadat de update is bijgewerkt, herstelt u dit bestand naar uw versie 1602-site. Wanneer u een site bijwerkt, wordt het huidige bestand overschreven met de oorspronkelijke (standaard) versie van het bestand. Zie [Hardware-inventarisatie uitbreiden](../../../core/clients/manage/inventory/extend-hardware-inventory.md)voor meer informatie over het gebruik van dit bestand.  

 **De data base-upgrade testen op een kopie van de meest recente back-up van de site database:** Voordat u een Configuration Manager centrale beheer site of primaire site bijwerkt, moet u het upgrade proces van de site database testen op een kopie van de site database.  

-   U moet het upgrade proces van de site database testen omdat wanneer u een site bijwerkt, de site database mogelijk wordt gewijzigd.  

-   Hoewel een upgrade test van de data base niet is vereist, kan hiermee problemen voor de upgrade worden geïdentificeerd voordat de productie database wordt beïnvloed.  

-   Een mislukte upgrade van de sitedatabase kan leiden tot een onbruikbare sitedatabase, waardoor u mogelijk een site recovery moet uitvoeren om de functionaliteit te herstellen.  

-   Hoewel de site database tussen sites in een hiërarchie wordt gedeeld, moet u de Data Base op elke toepasselijke site testen voordat u die site bijwerkt.  

-   Als u database replica's gebruikt voor beheer punten op een primaire site, schakelt u replicatie uit voordat u de back-up van de site database maakt.  

Configuration Manager biedt geen ondersteuning voor het maken van back-ups van secundaire sites en biedt geen ondersteuning voor de test upgrade van een secundaire site database.   
Voer geen test database-upgrade uit op de data base van de productie site. Dit leidt tot een update van de sitedatabase en kan tot gevolg hebben dat uw site onbruikbaar wordt. Zie voor meer informatie [stap 2: de upgrade van de data base testen voordat u een update installeert](install-in-console-updates.md#bkmk_step2) van **voordat u een update in de console installeert**.  

 **Plan voor het testen van de client:** Wanneer u een update installeert die de-client bijwerkt, kunt u de nieuwe client update in de pre-productie testen voordat u deze implementeert en een upgrade uitvoert voor al uw actieve clients.   

 Als u deze optie wilt gebruiken, moet u uw site configureren voor ondersteuning van automatische upgrades voor pre-productie voordat u begint met de installatie van de update. Zie voor meer informatie [clients upgraden](../../../core/clients/manage/upgrade/upgrade-clients.md) en   
[Client upgrades testen in een pre-productie verzameling](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Plannen van het gebruik van onderhouds Vensters om te bepalen wanneer site servers updates installeren:** U kunt de onderhouds Vensters gebruiken om een periode te definiëren gedurende welke updates van de site server kunnen worden geïnstalleerd. Hiermee kunt u bepalen wanneer de sites in uw hiërarchie de update installeren.   

Vanaf de release van de 1602-update hebben onderhouds Vensters de naam van de *service Windows*gewijzigd. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.  

 **Prerequisite Checker uitvoeren:**  Voordat u update 1602 installeert, kunt u de prerequisite Checker onafhankelijk van de installatie van de update uitvoeren. Wanneer u de update op de site installeert, wordt prerequisite Checker opnieuw uitgevoerd.  

Zie **stap 3: de prerequisite Checker uitvoeren voordat u een update installeert** in het onderwerp [updates voor Configuration Manager](../../../core/servers/manage/updates.md) voor meer informatie.  

> [!IMPORTANT]  
>  Wanneer de prerequisite Checker onafhankelijk wordt uitgevoerd of als onderdeel van een update-installatie, werkt het proces een aantal product bron bestanden bij die worden gebruikt voor site-onderhouds taken. Daarom moet u na het uitvoeren van de prerequisite Checker, maar voordat u de 1602-update installeert, **Setupwfe. exe** (Configuration Manager Setup) uitvoeren vanaf de cd. Meest recente map op de site server.  

 **Sites bijwerken:** u kunt nu de installatie van de update voor uw hiërarchie starten. U wordt aangeraden de update voor elke site buiten kantoor uren te installeren, wanneer het installatie proces van de update en de bijbehorende acties voor het opnieuw installeren van site onderdelen en site systeem rollen het minste effect heeft op uw zakelijke activiteiten.

Zie [updates voor Configuration Manager](../../../core/servers/manage/updates.md)voor meer informatie.  

## <a name="see-also"></a>Zie ook  
 [Updates voor Configuration Manager](../../../core/servers/manage/updates.md)
