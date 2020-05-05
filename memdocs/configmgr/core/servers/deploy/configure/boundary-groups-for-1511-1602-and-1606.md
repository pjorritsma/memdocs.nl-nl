---
title: Grens groepen voor 1511, 1602 en 1606
titleSuffix: Configuration Manager
description: Gebruik grens groepen met Configuration Manager versies 1511, 1602 en 1606.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09c1b0613d36cd135ff3ac71ac7ec8472ad1e8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721106"
---
# <a name="boundary-groups-for-configuration-manager-version-1511-1602-and-1606"></a>Grens groepen voor Configuration Manager versie 1511, 1602 en 1606

*Van toepassing op: Configuration Manager (huidige vertakking)*
<!-- This topic drops from TOC with the release of version 1706 -->

De informatie in dit onderwerp is specifiek voor het gebruik van grens groepen met versie 1511, 1602 en 1606 van Configuration Manager.
Als u versie 1610 of hoger gebruikt, raadpleegt u [grens groepen configureren](boundary-groups.md) voor informatie over het gebruik van de opnieuw ontworpen grens groepen.  


##  <a name="boundary-groups"></a><a name="BKMK_BoundaryGroups"></a>Grens groepen  
 U maakt grensgroepen om gerelateerde netwerklocaties (grenzen) logisch te groeperen, zodat uw infrastructuur eenvoudiger kan worden beheerd. U moet grenzen eerst toewijzen aan grensgroepen voordat u de grensgroep kunt gebruiken. Clients gebruiken de configuratie van de grensgroep voor:  

-   Automatische sitetoewijzing  

-   Inhoudslocatie  

-   Voorkeurs beheer punten

    Als u voorkeurs beheer punten wilt gebruiken, moet u deze optie inschakelen voor de hiërarchie en niet vanuit de configuratie van de grens groep. Zie de procedure *voor het gebruik van voorkeurs beheer punten inschakelen* verderop in dit onderwerp.  

Wanneer u grens groepen instelt, voegt u een of meer grenzen aan de grens groep toe. Vervolgens configureert u extra instellingen voor gebruik door clients die zich op die grenzen bevinden.  

#### <a name="to-create-a-boundary-group"></a>Een grensgroep maken  

1.  Kies in de Configuration Manager-console de optie **beheer** > **hiërarchie configuratie** >  **grens groepen**.  

2.  Klik op het tabblad **Start** in de groep **maken** op **grens groep maken**.  

3.  Kies in het dialoog venster **grens groep maken** het tabblad **Algemeen** en voer een **naam** in voor deze grens groep.  

4.  Kies **OK** om de nieuwe grens groep op te slaan.  

#### <a name="to-set-up-a-boundary-group"></a>Een grens groep instellen  

1.  Kies in de Configuration Manager-console de optie **beheer** > **hiërarchie configuratie** >  **grens groepen**.  

2.  Kies de grens groep die u wilt wijzigen.  

3.  Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

4.  Kies in het dialoog venster **Eigenschappen** voor de grens groep het tabblad **Algemeen** om de grenzen te wijzigen die lid zijn van deze grens groep:  

    -   Als u grenzen wilt toevoegen, klikt u op **toevoegen**, schakelt u het selectie vakje voor een of meer grenzen in en klikt u vervolgens op **OK**.  

    -   Als u grenzen wilt verwijderen, selecteert u de grens en klikt u vervolgens op **verwijderen**.  

5.  Kies het tabblad **verwijzingen** om de site toewijzing en de bijbehorende configuratie van de site systeem server te wijzigen:  

    -   Als u deze grens groep wilt inschakelen voor gebruik door clients voor site toewijzing, schakelt u het selectie vakje voor **deze grens groep gebruiken voor site toewijzing**in en kiest u een site in de vervolg keuzelijst **toegewezen site** .  

    -   De beschik bare site systeem servers instellen die zijn gekoppeld aan deze grens groep:  

    1.  Kies **toevoegen**en schakel vervolgens het selectie vakje voor een of meer servers in. De servers worden als gekoppelde sitesysteemservers toegevoegd aan deze grensgroep. Alleen servers waarop ondersteunde sitesysteemrollen zijn geïnstalleerd, zijn beschikbaar.  

        > [!NOTE]  
        >  U kunt een combinatie van beschikbare sitesystemen van alle sites in de hiërarchie selecteren. Geselecteerde sitesystemen worden weergegeven op het tabblad **Sitesystemen** in de eigenschappen van elke grens die deel uitmaakt van deze grensgroep.  

    2.  Als u een server uit deze grens groep wilt verwijderen, kiest u de server en kiest u vervolgens **verwijderen**.  

        > [!NOTE]  
        >  Als u deze grens groep niet meer wilt gebruiken voor het koppelen van site systemen, moet u alle servers die worden vermeld als gekoppelde site systeem servers verwijderen.  

    3.  Als u de netwerk verbindings snelheid voor een site systeem server voor deze grens groep wilt wijzigen, kiest u de server en kiest u **verbinding wijzigen**.  

         Standaard is de verbindings snelheid voor elk site systeem **snel**, maar u kunt de snelheid wijzigen in **langzaam**. De netwerkverbindingssnelheid en configuratie van een implementatie bepalen of een client inhoud kan downloaden van de server.  

6.  Kies **OK** om de eigenschappen van de grens groep te sluiten en de configuratie op te slaan.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Een inhoudsimplementatieserver of beheerpunt koppelen aan een grensgroep  

1.  Kies in de Configuration Manager-console de optie **beheer** > **hiërarchie configuratie** >  **grens groepen**.  

2.  Kies de grens groep die u wilt wijzigen.  

3.  Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

4.  Kies in het dialoog venster **Eigenschappen** voor de grens groep het tabblad **verwijzingen** .  

5.  Klik onder **site systeem servers selecteren**op **toevoegen**, schakel het selectie vakje in voor de site systeem servers die u wilt koppelen aan deze grens groep en kies vervolgens **OK**.  

6.  Kies **OK** om het dialoog venster te sluiten en de configuratie van de grens groep op te slaan.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Gebruik van voorkeursbeheerpunten inschakelen  

1.  Klik in de Configuration Manager-console op **beheer** > **site configuratie** > **sites**en kies vervolgens op het tabblad **Start** de optie **hiërarchie-instellingen**.  

2.  Kies op het tabblad **Algemeen** van de **hiërarchie-instellingen**de optie **clients gebruiken liever beheer punten die zijn opgegeven in grens groepen**.  

3.  Kies **OK** om het dialoog venster te sluiten en de configuratie op te slaan.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Een terugval site voor automatische site toewijzing instellen  

1. Klik in de Configuration Manager-console op **beheer** > **site configuratie** >  **sites**.  

2. Klik op het tabblad **Start** in de groep **sites** op **hiërarchie-instellingen**.  

3. Schakel op het tabblad **Algemeen** het selectie vakje voor **een terugval site gebruiken**in en kies vervolgens een site in de vervolg keuzelijst **terugval site** .  

4. Kies **OK** om de configuratie op te slaan.  

   In de volgende secties vindt u meer informatie over de configuratie van grensgroepen.  

###  <a name="about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Sitetoewijzing  
 U kunt elke grens groep instellen met een toegewezen site voor clients.  

-   Een nieuw geïnstalleerde client die gebruikmaakt van automatische site toewijzing, wordt lid van de toegewezen site van een grens groep die de huidige netwerk locatie van de client heeft.  

-   De site toewijzing van een client die is toegewezen aan een site, wordt niet gewijzigd wanneer de client de netwerk locatie wijzigt. Als de client bijvoorbeeld naar een nieuwe netwerk locatie roamt die wordt vertegenwoordigd door een grens in een grens groep met een andere site toewijzing, blijft de toegewezen site van de client ongewijzigd.  

-   Wanneer door Active Directory-systeemdetectie een nieuwe bron wordt gedetecteerd, worden netwerkgegevens voor de gedetecteerde bron geëvalueerd op basis van de grenzen in grensgroepen. In dit proces wordt de nieuwe bron aan een toegewezen site gekoppeld voor de push-clientinstallatie.  

-   Wanneer een grens lid is van meerdere grens groepen met verschillende toegewezen sites, selecteren clients wille keurig een van de sites.  

-   Wijzigingen in de toegewezen site van een grens groep gelden alleen voor nieuwe acties voor site toewijzing. Clients die eerder aan een site zijn toegewezen, evalueren hun site toewijzing niet opnieuw op basis van wijzigingen in de configuratie van een grens groep (of op hun eigen netwerk locatie).  

Zie voor meer informatie over client site toewijzing [automatische site toewijzing gebruiken voor computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [het toewijzen van clients aan een site](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Inhoudslocatie  
 U kunt elke grens groep instellen met een of meer distributie punten en status migratie punten en u kunt dezelfde distributie punten en status migratie punten koppelen aan meerdere grens groepen.  

-   **Tijdens de softwaredistributie**vragen clients een locatie aan voor de implementatie-inhoud. Configuration Manager verzendt de client een lijst met distributie punten die zijn gekoppeld aan elke grens groep die de huidige netwerk locatie van de client bevat.  

-   **Tijdens de implementatie van het besturings systeem**vragen clients een locatie aan voor het verzenden of ontvangen van hun status migratie-informatie. Configuration Manager verzendt de client een lijst met status migratie punten die zijn gekoppeld aan elke grens groep die de huidige netwerk locatie van de client bevat.  

Dit gedrag zorgt ervoor dat de client de dichtstbijzijnde server kan selecteren waarvan de inhoud of status migratie-informatie moet worden overgedragen.  

###  <a name="about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Voorkeursbeheerpunten  
 Met voorkeurs beheer punten kunnen clients een beheer punt identificeren dat is gekoppeld aan de huidige netwerk locatie (grens).  

-   Een client probeert een voorkeurs beheer punt van de toegewezen site te gebruiken voordat het een beheer punt gebruikt van de toegewezen site die niet is ingesteld als voor keur.  

-   Als u deze optie wilt gebruiken, moet u deze voor de hiërarchie inschakelen en grens groepen instellen op afzonderlijke primaire sites, zodat u de beheer punten kunt toevoegen die moeten worden gekoppeld aan de gekoppelde grenzen van de grens groep  

-   Wanneer voorkeurs beheer punten worden ingesteld en een client de lijst van beheer punten ordent, plaatst de client de voorkeurs beheer punten boven aan de lijst met toegewezen beheer punten, inclusief alle beheer punten van de toegewezen site van de client.  

> [!NOTE]  
>  Wanneer een client roamt, bijvoorbeeld wanneer een laptop naar een externe kantoor locatie wordt verplaatst en de netwerk locatie wijzigt, kan deze een beheer punt (of proxy beheer punt) van de lokale site op de nieuwe locatie gebruiken voordat een beheer punt wordt gebruikt vanuit de toegewezen site (inclusief de voorkeurs beheer punten).  Zie [begrijpen hoe clients site bronnen en-services vinden voor Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) voor meer informatie.  

###  <a name="about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Overlappende grenzen  
 Configuration Manager ondersteunt configuraties met overlappende grenzen voor locatie van inhoud:  

-   **Wanneer een client inhoud aanvraagt**en de client netwerk locatie tot meerdere grens groepen behoort, stuurt Configuration Manager de client een lijst met alle distributie punten die de inhoud hebben.  

-   **Wanneer een client een server aanvraagt voor het verzenden of ontvangen van de status migratie gegevens**en de client netwerk locatie tot meerdere grens groepen behoort, verzendt Configuration Manager de client een lijst met alle status migratie punten die zijn gekoppeld aan een grens groep die de huidige netwerk locatie van de client bevat.  

Dit gedrag zorgt ervoor dat de client de dichtstbijzijnde server kan selecteren waarvan de inhoud of status migratie-informatie moet worden overgedragen.  

###  <a name="about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a>Over de snelheid van de netwerk verbinding  
 U kunt de netwerk verbindings snelheid instellen voor elke site systeem server in een grens groep. Deze instelling geldt voor clients die verbinding maken met een site systeem op basis van de configuratie van deze grens groep. Op dezelfde sitesysteemserver kan hiervoor een andere verbindingssnelheid zijn ingesteld in verschillende grensgroepen.  

 De netwerk verbindings snelheid is standaard ingesteld op **snel**, maar u kunt deze wijzigen in **langzaam**. De netwerk verbindings snelheid en de implementatie configuratie controleren of een client inhoud kan downloaden van een distributie punt wanneer de client zich in een gekoppelde grens groep bevindt.  

 Zie scenario's voor de [locatie van inhouds bronnen](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md)voor meer informatie over hoe de configuratie van de netwerk verbindings snelheid van invloed is op hoe clients inhoud ophalen.  
