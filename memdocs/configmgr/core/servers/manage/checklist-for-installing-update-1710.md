---
title: Controle lijst voor 1710 | Configuration Manager
titleSuffix: Configuration Manager
description: Meer informatie over de acties die u moet uitvoeren voordat u bijwerkt naar Configuration Manager versie 1710.
ms.date: 12/19/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e8ab8ca-41ef-467a-943b-a115d88cafe0
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fd3e067577a7f89c02727ccd490ef6d1eb26ca98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723318"
---
# <a name="checklist-for-installing-update-1710-for-configuration-manager"></a>Controle lijst voor het installeren van update 1710 voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u de huidige vertakking van Configuration Manager gebruikt, kunt u de update voor de console van versie 1710 installeren om uw hiërarchie van een vorige versie bij te werken.

Als u de update voor versie 1710 wilt downloaden, moet u een site systeemrol voor het service verbindings punt gebruiken op de site op het hoogste niveau van uw hiërarchie. Dit kan in de online-of offline modus zijn. Nadat uw hiërarchie het update pakket van micro soft heeft gedownload, kunt u het vinden in de **console &gt; onder &gt; beheer &gt; overzicht Cloud Services updates en onderhoud**.

-   Wanneer de update wordt weer gegeven als **beschikbaar**, is de update gereed voor installatie. Voordat u versie 1710 installeert, raadpleegt u de volgende informatie [over het installeren van update 1710](#about-installing-update-1710) en de [controle lijst](#checklist) voor configuraties die moeten worden gemaakt voordat de update wordt gestart.

-   Als de update wordt weer gegeven als **downloaden** en niet wordt gewijzigd, controleert u de **hman. log** en **dmpdownloader. log** op fouten.

    -   Als in het dmpdownloader. log wordt aangegeven dat het dmpdownloader-proces in de slaap stand staat en wacht op een interval voordat op updates wordt gecontroleerd, kunt u de **SMS_Executive** -service opnieuw starten op de site server om het downloaden van de herdistributies bestanden van de update opnieuw te starten.

    -   Een ander algemeen Download probleem doet zich voor wanneer de instellingen van `silverlight.dlservice.microsoft.com` de `download.microsoft.com`proxy server downloaden van en niet verhinderen.

Zie [updates en onderhoud in de console](updates.md#bkmk_inconsole)voor meer informatie over het installeren van updates.

Voor informatie over de versies van de Current Branch, Zie [basis lijn-en update versies](updates.md#bkmk_Baselines) in [updates voor Configuration Manager](updates.md).

## <a name="about-installing-update-1710"></a>Over het installeren van update 1710

**Sites**  
U installeert Update 1710 op de site op het hoogste niveau van uw hiërarchie. Dit betekent dat u de installatie start vanaf uw centrale beheer site als u er een hebt of van uw zelfstandige primaire site. Nadat de update is geïnstalleerd op de site op het hoogste niveau, hebben onderliggende sites het volgende gedrag van de update:

-   De update wordt automatisch geïnstalleerd op onderliggende primaire sites nadat de installatie van de update is voltooid op de centrale beheer site. U kunt service Windows gebruiken om te bepalen wanneer een site de update installeert. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.

-   U moet elke secundaire site hand matig bijwerken vanuit de Configuration Manager-console nadat de primaire bovenliggende site de installatie van de update heeft voltooid. Het automatisch bijwerken van secundaire siteservers wordt niet ondersteund.

**Sitesysteemrollen:**  
Wanneer een site server de update installeert, worden de site systeem rollen die zijn geïnstalleerd op de site Server computer en die op externe computers zijn geïnstalleerd, automatisch bijgewerkt. Voordat u de update installeert, moet u ervoor zorgen dat elke site systeem server voldoet aan de vereisten voor de bewerking met de nieuwe update versie.

**Configuration Manager-consoles:**   
De eerste keer dat u een Configuration Manager-console gebruikt nadat de update is voltooid, wordt u gevraagd die console bij te werken. Hiertoe moet u Configuration Manager Setup uitvoeren op de computer die als host fungeert voor de-console en vervolgens de optie kiezen om de-console bij te werken. U kunt installeren van de update naar de console beter niet uitstellen.

> [!IMPORTANT]  
> Wanneer u een update installeert op de centrale beheer site, moet u rekening houden met de volgende beperkingen en vertragingen die bestaan totdat alle onderliggende primaire sites de update-installatie ook volt ooien:    
> - **Client upgrades** worden niet gestart. Dit omvat automatische updates van clients en pre-productie clients. Daarnaast kunt u pas productie clients promo veren naar productie als de laatste site de installatie van de update heeft voltooid. Nadat de installatie van de update is voltooid op de laatste site, worden de client upgrades gestart op basis van uw configuratie keuzes.   
> - **Nieuwe functies** die u met de update inschakelt, zijn niet beschikbaar. Dit is om te voor komen dat de replicatie van gegevens met betrekking tot deze functie wordt verzonden naar een site die nog geen ondersteuning voor die functie heeft geïnstalleerd. Nadat alle primaire sites de update hebben geïnstalleerd, is de functie beschikbaar voor gebruik.   
> - **Replicatie koppelingen** tussen de centrale beheer site en de onderliggende primaire sites worden weer gegeven als niet-bijgewerkt. Hiermee wordt de installatie status van het update pakket weer gegeven als de status voltooid met waarschuwing voor het controleren van de replicatie-initialisatie. In het knoop punt controle van de-console wordt deze weer gegeven als *koppeling wordt geconfigureerd*.


## <a name="checklist"></a>Controlelijst

**Zorg ervoor dat op alle sites een versie van Configuration Manager wordt uitgevoerd die ondersteuning biedt voor update 1710:**   
Op elke site server in de hiërarchie moet dezelfde versie van Configuration Manager worden uitgevoerd voordat u de installatie van update 1710 kunt starten. Als u wilt bijwerken naar 1710, moet u versie 1610, 1702 of 1706 gebruiken.

**Bekijk de status van uw Software Assurance-of gelijkwaardige abonnements rechten:**   
U moet beschikken over een overeenkomst voor actieve Software Assurance (SA) om update 1710 te installeren. Wanneer u deze update installeert, wordt op het tabblad **licenties** de optie weer gegeven om de **verval datum van uw Software Assurance**te bevestigen.

Dit is een optionele waarde die u kunt opgeven als een handige herinnering voor de verval datum van uw licentie. Deze datum is zichtbaar wanneer u toekomstige updates installeert. Mogelijk hebt u deze waarde eerder opgegeven tijdens de installatie of installatie van een update of via het tabblad **licenties** van de **hiërarchie-instellingen**vanuit de Configuration Manager-console.

Zie [Licentiëring en vertakkingen voor Configuration Manager](../../understand/learn-more-editions.md)voor meer informatie.

**Geïnstalleerde Microsoft .NET versies controleren op site systeem servers:** Wanneer deze update wordt geïnstalleerd op een site, installeert Configuration Manager automatisch .NET Framework 4.5.2 op elke computer die als host fungeert voor een van de volgende site systeem rollen wanneer .NET Framework 4,5 of hoger nog niet is geïnstalleerd:

-   Proxypunt voor inschrijving
-   Inschrijvingspunt
-   Beheerpunt
-   Serviceverbindingspunt

Met deze installatie kan de site systeem server de status opnieuw opstarten in behandeling hebben en fouten melden aan de Configuration Manager onderdeel status viewer. Daarnaast kunnen de .NET-toepassingen op de server wille keurige fouten ondervinden totdat de server opnieuw is opgestart.

Zie voor meer informatie [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).

**Controleer de versie van de Windows Assessment and Deployment Kit (ADk) voor Windows 10** De Windows 10 ADK moet versie 1703 of hoger zijn. (Zie [Windows 10 ADk](../../plan-design/configs/support-for-windows-10.md#windows-10-adk)voor meer informatie over ondersteunde versies van Windows ADk.) Als u de Windows ADK moet bijwerken, doet u dit voordat u begint met het bijwerken van Configuration Manager. Dit zorgt ervoor dat de standaard opstart installatie kopieën automatisch worden bijgewerkt naar de meest recente versie van Windows PE. (Aangepaste opstart installatie kopieën moeten hand matig worden bijgewerkt.)

Als u de site bijwerkt voordat u de Windows ADK bijwerkt, raadpleegt u [distributie punten bijwerken met de opstart installatie kopie](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image) voor verbeteringen van dit proces in Configuration Manager versie 1710.

**De site- en hiërarchiestatus bekijken en controleren of er geen onopgeloste problemen zijn:** voordat u een site bijwerkt, dient u alle operationele problemen voor de siteserver, de sitedatabaseserver, en sitesysteemrollen die op externe computers zijn geïnstalleerd, op te lossen. De update van een site kan mislukken door bestaande operationele problemen.

Zie [waarschuwingen en het status systeem voor Configuration Manager gebruiken](use-alerts-and-the-status-system.md)voor meer informatie.

**Bestands-en gegevens replicatie tussen sites controleren:**   
Zorg ervoor dat bestands-en database replicatie tussen sites operationeel en actueel is. Vertragingen of achterstanden in een van beide kunnen leiden tot een soepele, geslaagde update.
Voor databasereplicatie kunt u Replication Link Analyzer gebruiken om u te helpen bij het oplossen van problemen voordat u de update start.

Zie [Replication link Analyzer](monitor-replication.md#BKMK_RLA) in het onderwerp  [database replicatie bewaken](monitor-replication.md#BKMK_RLA)voor meer informatie.

**Installeer alle toepasselijke kritieke updates voor besturings systemen op computers die de site, de site database server en externe site systeem rollen hosten:** Installeer alle essentiële updates voor elk toepasselijk site systeem voordat u een update voor Configuration Manager installeert. Als een update die u installeert, vereist dat de computer opnieuw wordt opgestart, start de desbetreffende computers dan opnieuw op voordat u de upgrade start.

**Database replica's uitschakelen voor beheer punten op primaire sites:**   
Configuration Manager een primaire site met een database replica voor beheer punten is ingeschakeld, kan niet worden bijgewerkt. Schakel database replicatie uit voordat u een update voor Configuration Manager installeert.

Zie [database replica's voor beheer punten voor Configuration Manager](../deploy/configure/database-replicas-for-management-points.md)voor meer informatie.

**Stel SQL Server AlwaysOn-beschikbaarheids groepen in op hand matige failover:**   
Als u een beschikbaarheids groep gebruikt, moet u ervoor zorgen dat de beschikbaarheids groep is ingesteld op hand matige failover voordat u de installatie van de update start. Nadat de site is bijgewerkt, kunt u de failover herstellen naar automatisch. Zie [SQL Server AlwaysOn voor een site database](../deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)voor meer informatie.

**Configureer software-update punten die gebruikmaken van Nlb's:**   
<!-- Support for NLBs is fully removed with 1702. When 1702 is no longer in support, this statement can drop -->
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

**Plan voor het testen van de client:**   
Wanneer u een update installeert die de-client bijwerkt, kunt u de nieuwe client update in de pre-productie testen voordat u deze implementeert en een upgrade uitvoert voor al uw actieve clients.

Als u deze optie wilt gebruiken, moet u uw site configureren voor ondersteuning van automatische upgrades voor pre-productie voordat u begint met de installatie van de update.

Zie [clients bijwerken](../../clients/manage/upgrade/upgrade-clients.md) en [Client upgrades testen in een pre-productie verzameling](../../clients/manage/upgrade/test-client-upgrades.md)voor meer informatie.

**Het gebruik van service Windows plannen om te bepalen wanneer site servers updates installeren:**   
Gebruik service Windows om een periode te definiëren gedurende welke updates op een site server kunnen worden geïnstalleerd.

Hiermee kunt u bepalen wanneer de sites in uw hiërarchie de update installeren. Zie [service Windows for site servers](service-windows.md)(Engelstalig) voor meer informatie.

**Voer de prerequisite Checker voor Setup uit:**   
Wanneer de update in de-console wordt weer gegeven als **beschikbaar,** kunt u de prerequisite Checker onafhankelijk uitvoeren voordat u de update installeert. (Wanneer u de update op de site installeert, wordt prerequisite Checker opnieuw uitgevoerd.)

Als u een controle op vereisten wilt uitvoeren vanuit de-console, gaat u naar **beheer > overzicht > Cloud Services > updates en onderhoud.** Klik vervolgens met de rechter muisknop op **Configuration Manager Update pakket 1710**en kies vervolgens **controle op vereisten uitvoeren**.

Zie **stap 3: de prerequisite Checker uitvoeren voordat u een update installeert** in het onderwerp [updates in de console installeren voor Configuration Manager](install-in-console-updates.md)voor meer informatie over het starten en vervolgens controleren van de controle op vereisten.

> [!IMPORTANT]  
> Wanneer de prerequisite Checker onafhankelijk wordt uitgevoerd of als onderdeel van een update-installatie, werkt het proces een aantal product bron bestanden bij die worden gebruikt voor site-onderhouds taken. Daarom voert u na het uitvoeren van de prerequisite Checker, maar voordat u de update installeert,, als u een site-onderhouds taak moet uitvoeren, **Setupwpf. exe** (Configuration Manager Setup) uit vanaf de cd. Meest recente map op de site server.

**Sites bijwerken:**   
U bent nu klaar om de installatie van de update voor uw hiërarchie te starten. Zie [updates in de console installeren](install-in-console-updates.md#bkmk_install)voor meer informatie over het installeren van de update.

U wordt aangeraden de update voor elke site buiten kantoor uren te installeren, wanneer het installatie proces van de update en de bijbehorende acties voor het opnieuw installeren van site onderdelen en site systeem rollen het minste effect heeft op uw zakelijke activiteiten.

Zie [updates voor Configuration Manager](updates.md)voor meer informatie.

## <a name="post-update-checklist"></a>Controle lijst voor bijwerken berichten
Controleer de volgende acties om uit te voeren nadat de installatie van de update is voltooid.
1. Zorg ervoor dat de replicatie van site-naar-site actief is. In de-console bekijkt u**site hiërarchie** **bewaking** > en **bewaken** > van**database replicatie** voor aanwijzingen van problemen of bevestiging dat replicatie koppelingen actief zijn.
2. Zorg ervoor dat de site server en de site systeemrol zijn bijgewerkt naar versie 1710. In de-console kunt u de optionele kolom **versie** toevoegen aan de weer gave van een aantal knoop punten, inclusief **sites** en **distributie punten**.

   Als dat nodig is, wordt de site systeemrol automatisch opnieuw geïnstalleerd om bij te werken naar de nieuwe versie. Overweeg om externe site systemen die niet zijn bijgewerkt, opnieuw te starten.
3. Configureer database replica's opnieuw voor beheer punten op primaire sites die u hebt uitgeschakeld voordat u de update start.
4. Configureer database onderhouds taken die u hebt uitgeschakeld voordat u de update start.
5. Als u client Piloting hebt geconfigureerd voordat u de update installeert, moet u de upgrade van clients uitvoeren volgens het plan dat u hebt gemaakt.
