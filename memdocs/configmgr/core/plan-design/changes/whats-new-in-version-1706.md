---
title: Nieuwe versie 1706
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1706 van Configuration Manager.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 2e823aad8fcf69861d21a99f0e65dcf8aaa40dcd
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993383"
---
# <a name="what39s-new-in-version-1706-of-configuration-manager"></a>Wat&#39;s nieuw in versie 1706 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1706 voor Configuration Manager current branch is beschikbaar als een update in de console voor eerder geïnstalleerde sites waarop versie 1606, 1610 of 1702 wordt uitgevoerd.

> [!TIP]  
> Als u een nieuwe site wilt installeren, moet u een basislijn versie van Configuration Manager gebruiken.  
>
> Meer informatie over:    
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Updates installeren op sites](../../servers/manage/updates.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)  

De volgende secties bevatten informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1706 van Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Site-infra structuur

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-microsoft-365"></a>Ondersteuning voor client-peer-cache voor snelle installatie bestanden voor Windows 10 en Microsoft 365  
<!-- 1352486 -->
Vanaf deze release ondersteunt peer-cache distributie van bestanden voor snelle installatie van inhoud voor Windows 10 en van update bestanden voor Microsoft 365. Er zijn geen aanvullende configuraties vereist ter ondersteuning van deze wijziging.

### <a name="updates-for-the-data-warehouse"></a>Updates voor het Data Warehouse
<!-- 1277922 -->
Het Data Warehouse is niet langer een functie van de voorlopige versie. We hebben ook de vereisten bijgewerkt om ondersteuning te bieden voor de Data Base op SQL Server AlwaysOn-beschikbaarheids groepen en-failoverclusters. Zie [het Data Warehouse-service punt](../../servers/manage/data-warehouse.md)voor meer informatie.

### <a name="accessibility-improvements"></a>Verbeterde toegankelijkheid
<!-- 1253000 -->
Er zijn extra verbeteringen toegevoegd aan toegankelijkheid voor de Configuration Manager-console. Zie [toegankelijkheids functies](../../understand/accessibility-features.md)voor meer informatie.

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Verbeteringen voor SQL Server AlwaysOn-beschikbaarheids groepen
<!-- 1352094 -->
Met deze versie kunt u nu asynchrone doorvoer replica's gebruiken in de SQL Server AlwaysOn-beschikbaarheids groepen die u gebruikt met Configuration Manager. Dit betekent dat u extra replica's aan uw beschikbaarheids groepen kunt toevoegen om te gebruiken als externe back-ups, en ze vervolgens te gebruiken in een nood herstel scenario.  
- Configuration Manager ondersteunt het gebruik van de asynchrone doorvoer replica om uw synchrone replica te herstellen. Zie [Opties voor herstel van de site database](../../servers/manage/recover-sites.md#site-database-recovery-options) in het onderwerp back-up en herstel voor informatie over hoe u dit kunt doen.
- Deze release biedt geen ondersteuning voor failover voor het gebruik van de asynchrone doorvoer replica als uw site database.
Zie voor meer informatie voor [bereiding voor het gebruik van](../../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)AlwaysOn-beschikbaarheids groepen.

### <a name="update-reset-tool"></a>Hulpprogramma voor het opnieuw instellen van updates
<!-- 1324589 -->
Vanaf versie 1706, Configuration Manager primaire sites en centrale beheer sites bevatten het hulp programma Configuration Manager Update reset **CMUpdateReset.exe**. Gebruik dit hulp programma met een wille keurige versie van de huidige vertakking die nog niet wordt ondersteund, om problemen op te lossen wanneer er problemen zijn met het downloaden of repliceren van updates in de console. Zie het [hulp programma voor het opnieuw instellen van updates](../../servers/manage/update-reset-tool.md)voor meer informatie.

### <a name="high-dpi-console-support"></a>Ondersteuning voor hoge DPI-console  
<!-- 1353476 -->
In deze release moeten problemen worden opgelost met de manier waarop de Configuration Manager-console wordt geschaald en de verschillende onderdelen van de gebruikers interface worden weer gegeven wanneer deze worden weer gegeven op hoge DPI-apparaten (zoals een Surface Book).

### <a name="improved-boundary-groups-for-software-update-points"></a>Verbeterde grens groepen voor software-update punten
<!-- 1324591 -->
Deze release bevat verbeteringen voor de werking van software-update punten met grens groepen. Hieronder vindt u een overzicht van het nieuwe terugval gedrag:
- Terugval voor software-update punten gebruikt nu een Configureer bare tijd voor terugval naar grens groepen in de buur.
- Onafhankelijk van de terugval configuratie probeert een client het laatste software-update punt te bereiken dat gedurende 120 minuten wordt gebruikt. Wanneer de server gedurende 120 minuten niet kan worden bereikt, controleert de client de groep beschik bare software-update punten, zodat er een nieuwe kan worden gevonden.
- Als de oorspronkelijke server gedurende twee uur niet kan worden bereikt, schakelt de client over naar een kortere cyclus voor het maken van contact met een nieuw software-update punt. Dit betekent dat als een client geen verbinding kan maken met een nieuwe server, de volgende server snel wordt geselecteerd uit de groep beschik bare servers en er wordt geprobeerd contact op te nemen.

Zie [Software-update punten](../../servers/deploy/configure/boundary-groups.md#bkmk_sup) in het onderwerp grens groepen voor de current branch voor meer informatie.

### <a name="azure-ad-integration-with-configuration-manager"></a>Azure AD-integratie met Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
In deze release hebben we de integratie van Configuration Manager en Azure Active Directory (Azure AD) verbeterd.  Deze verbeteringen stroom lijnen het configureren van de Azure-Services die u gebruikt met Configuration Manager en helpt u bij het beheren van clients en gebruikers die zich verifiëren als Azure AD.

De verbeterde integratie biedt de volgende mogelijkheden:  
- Wizard Azure-Services: deze wizard biedt een algemene configuratie-ervaring waarmee de afzonderlijke werk stromen worden vervangen voor het instellen van de volgende Azure-Services die u gebruikt met Configuration Manager.
  - **Cloud beheer** Clients toestaan om te verifiëren met behulp van Azure Active Directory (Azure AD). U kunt ook Azure AD-gebruikers detectie configureren.
  - **Log Analytics-connector** Verbinding maken met Azure Log Analytics en verzamelings gegevens synchroniseren.
  - **Upgradegereedheid** Verbinding maken met Upgradegereedheid en de client upgrade weer geven-compatibiliteits gegevens.
  - **Windows Store voor bedrijven** Maak verbinding met de online winkel voor Windows Store voor bedrijven en ontvang apps voor uw organisatie die u kunt implementeren met Configuration Manager.


  Dit doet u door een [Azure server web app](/azure/app-service/app-service-authentication-overview) te gebruiken om het abonnement en de configuratie gegevens op te geven die u op een andere manier invoert, telkens wanneer u een nieuw Configuration Manager onderdeel of service met Azure instelt. Zie de [wizard Azure-Services](../../servers/deploy/configure/azure-services-wizard.md)voor meer informatie.

- Gebruik Azure AD om clients op internet te verifiëren om toegang te krijgen tot uw Configuration Manager-sites. Azure AD vervangt de nood zaak voor het configureren en gebruiken van certificaten voor client verificatie. Hiervoor is de site systeemrol voor de Cloud beheer gateway vereist. Zie voor meer informatie [Configuration Manager-clients installeren en toewijzen van het Internet met behulp van Azure AD voor verificatie](../../clients/deploy/deploy-clients-cmg-azure.md).

- De Configuration Manager-client installeren en beheren op computers die zich op internet bevinden. Hiervoor moet de site systeemrol van de Cloud beheer gateway worden gebruikt. Zie voor meer informatie [Configuration Manager-clients installeren en toewijzen van het Internet met behulp van Azure AD voor verificatie](../../clients/deploy/deploy-clients-cmg-azure.md).

- Configureer Azure AD-gebruikers detectie.  Gebruik de wizard voor Azure-Services om deze nieuwe detectie methode te configureren. Met deze nieuwe methode wordt een query uitgevoerd op uw Azure AD voor gebruikers gegevens, en kunt u vervolgens traditionele, gebruikelijke detectie gegevens gebruiken.  Zowel volledige als Delta synchronisatie wordt ondersteund.  Zie [Azure AD-gebruikers detectie](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)voor meer informatie.

### <a name="peer-cache-improvements"></a>Verbeteringen in de peer-cache
<!-- 1252345 -->
Peer-cache maakt geen gebruik meer van het netwerk toegangs account voor het verifiëren van download aanvragen van peers. Er is een voor behoud van dit item wanneer het account voor clients vereist blijft. Dit blijft een vereiste voor clients die opstarten in WinPE en vervolgens toegang krijgen tot inhoud van een peer-cache bron. Zie [vereisten en overwegingen voor peer-cache](../hierarchy/client-peer-cache.md#requirements)voor meer informatie.


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Instellingen voor naleving

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Nieuwe configuratie-instellingen voor Windows 10-apparaten die niet worden beheerd met de Configuration Manager-client
<!-- 1354715 -->
In deze release hebben we nieuwe instellingen voor configuratie-items toegevoegd voor Windows 10-apparaten die zijn Inge schreven bij intune, of die op locatie worden beheerd door Configuration Manager. De instellingen zijn:

- **Wachtwoord**
  - Apparaatversleuteling
- **Apparaat**
  - Regio-instellingen aanpassen (alleen Desktop)
  - Instellingen voor in-/uitschakelen en slaap stand wijzigen
  - Taal instellingen wijzigen
  - Systeem tijd wijzigen
  - Apparaatnaam wijzigen
- **Opslaan**
  - Apps uit de Store automatisch bijwerken
  - Alleen persoonlijke Store gebruiken
  - Door store afkomstige app starten
- **Microsoft Edge**
  - Toegang tot about: Flags blok keren
  - SmartScreen-prompt negeren
  - SmartScreen-prompt voor bestanden negeren
  - WebRTC localhost IP-adres
  - Standaard zoekmachine
  - URL van OpenSearch XML
  - Start pagina's (alleen Desktop)

Zie [configuratie-items maken voor windows 8,1-en Windows 10-apparaten die worden beheerd zonder de Configuration Manager-client](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)voor meer informatie over alle instellingen van Windows 10.

### <a name="new-device-compliance-policy-rules"></a>Nieuwe regels voor nalevings beleid voor apparaten

* **Vereist wachtwoord type**. Geef op of de gebruiker een alfanumeriek wacht woord of een numeriek wacht woord moet maken. Voor alfanumerieke wacht woorden geeft u ook het minimum aantal teken sets op waaruit het wacht woord moet bestaan. De vier teken sets zijn: hoofd letters, kleine letters, symbolen en cijfers.

  **Ondersteund in:**
  * Windows Phone 8+
  * Windows 8.1 +
  * iOS 6+
  <br></br>
* **USB-fout opsporing blok keren op apparaat**. U hoeft deze instellingen niet te configureren, omdat USB-fout opsporing al is uitgeschakeld op Android for work-apparaten.

  **Ondersteund in:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Apps van onbekende bronnen blok keren**. Vereisen dat de installatie van apps van onbekende bronnen wordt voor komen. U hoeft deze instelling niet te configureren, omdat de installatie van onbekende bronnen altijd wordt beperkt door Android for work-apparaten.

  **Ondersteund in:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Dreigingen moeten worden gescand op apps**. Met deze instelling geeft u op dat de functie apps controleren is ingeschakeld op het apparaat.

  **Ondersteund in:**
  * Android 4,2 tot en met 4,4
  * Samsung KNOX Standard 4.0+


## <a name="application-management"></a>Toepassingsbeheer

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Power shell-scripts uitvoeren vanuit de Configuration Manager-console
<!-- 1236459 -->

In Configuration Manager kunt u scripts implementeren op client apparaten met behulp van pakketten en Program ma's. In deze release hebben we nieuwe functionaliteit toegevoegd waarmee u de volgende acties kunt uitvoeren:

- Power shell-scripts importeren in Configuration Manager
- De scripts bewerken vanuit de Configuration Manager-console (alleen voor niet-ondertekende scripts)
- Scripts markeren als goedgekeurd of geweigerd, ter verbetering van de beveiliging
- Scripts uitvoeren op verzamelingen van Windows-client-Pc's en on-premises beheerde Windows-Pc's. U kunt in plaats daarvan geen scripts implementeren. deze worden in bijna realtime uitgevoerd op client apparaten.
- Bekijk de resultaten die door het script worden geretourneerd in de Configuration Manager-console.

Zie [Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console](../../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie.

### <a name="new-mobile-application-management-policy-settings"></a>Nieuwe Mobile Application Management-beleids instellingen    
<!--1324760-->
Vanaf deze release kunt u drie nieuwe Mobile Application Management-beleids instellingen (MAM) gebruiken:

- **Scherm opname blok keren (alleen Android-apparaten):** Hiermee geeft u op dat de mogelijkheden voor scherm opname van het apparaat worden geblokkeerd wanneer deze app wordt gebruikt.


## <a name="operating-system-deployment"></a>Implementatie van besturingssystemen

### <a name="hardware-inventory-collects-secure-boot-information"></a>Hardware-inventaris verzamelt informatie over beveiligd opstarten
Met de hardware-inventarisatie wordt nu informatie verzameld over of beveiligd opstarten is ingeschakeld op clients. Deze informatie wordt opgeslagen in de klasse **SMS_Firmware** (geïntroduceerd in versie 1702) en is standaard ingeschakeld in hardware-inventaris. Zie  [hardware-inventaris configureren](../../clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over hardware-inventarisatie.

### <a name="collapsible-task-sequence-groups"></a>Samenvouw bare taken reeks groepen
Deze versie introduceert de mogelijkheid om taken reeks groepen uit te vouwen en samen te vouwen. U kunt afzonderlijke groepen uitvouwen of samen vouwen of alle groepen in één keer uitvouwen of samen vouwen.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Opstart installatie kopieën opnieuw laden met de huidige versie van Windows PE
Wanneer u **Update distributie punten** op een geselecteerde opstart installatie kopie uitvoert, kunt u nu de nieuwste versie van Windows PE (uit de installatiemap van Windows ADk) in de opstart installatie kopie opnieuw laden. Zie [distributie punten bijwerken met de opstart installatie kopie](../../../osd/get-started/manage-boot-images.md#update-distribution-points-with-the-boot-image)voor meer informatie.

## <a name="software-updates"></a>Software-updates

### <a name="improvements-to-express-update-download-time"></a>Verbeteringen in download tijd van snelle updates
In deze release hebben we de download tijd voor snelle updates aanzienlijk verbeterd. Zie voor meer informatie [bestanden voor snelle installatie beheren voor Windows 10-updates](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

### <a name="manage-microsoft-surface-driver-updates"></a>Updates voor micro soft Surface drivers beheren
<!-- 1098490 -->
U kunt nu Configuration Manager gebruiken om updates van micro soft Surface-Stuur Programma's te beheren.    


#### <a name="prerequisites"></a>Vereisten
- Alle software-update punten moeten Windows Server 2016 uitvoeren.    
- Dit is een voorlopige functie die u moet inschakelen om deze beschikbaar te maken. Zie [Use pre-release features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease) (Functies van evaluatieversies gebruiken) voor meer informatie.

#### <a name="to-manage-surface-driver-updates"></a>Updates voor Surface drivers beheren

1. Synchronisatie inschakelen voor micro soft Surface-Stuur Programma's. Gebruik de procedure in [classificatie en producten configureren](../../../sum/get-started/configure-classifications-and-products.md) en schakel het selectie vakje **micro soft Surface-Stuur Programma's en firmware-updates toevoegen** op het tabblad **classificaties** in om Surface-Stuur Programma's in te scha kelen.
2. [Synchroniseer de micro soft Surface-Stuur Programma's](../../../sum/get-started/synchronize-software-updates.md).
3. [Gesynchroniseerde Stuur Programma's van micro soft Surface implementeren](../../../sum/deploy-use/deploy-software-updates.md)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Windows Update voor beleid voor bedrijfs uitstel configureren
<!-- 1290890 -->
U kunt nu uitstel beleid configureren voor Windows 10-onderdelen updates of kwaliteits updates voor Windows 10-apparaten die rechtstreeks worden beheerd door Windows Update voor bedrijven. U kunt het uitstel beleid beheren in het knoop punt nieuwe **Windows Update voor bedrijfs beleid** onder **software bibliotheek**  >  **Windows 10 Servicing**.

Zie [integratie met Windows Update voor bedrijven in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md#configure-windows-update-for-business-deferral-policies)voor meer informatie.

### <a name="improved-user-notifications-for-microsoft-365-updates"></a>Verbeterde gebruikers meldingen voor Microsoft 365 updates
Er zijn verbeteringen aangebracht voor het gebruik van de Office-klik-en-klaar-gebruikers ervaring wanneer een client een Microsoft 365 update installeert. Dit omvat pop-up-en in-app-meldingen en een aftellings ervaring. Zie voor meer informatie [gedrag voor opnieuw opstarten en client meldingen voor Microsoft 365 updates](../../../sum/deploy-use/manage-office-365-proplus-updates.md)

## <a name="reporting"></a>Rapportage

### <a name="use-windows-analytics-with-configuration-manager"></a>Gebruik Windows Analytics met Configuration Manager
<!-- 1318608 -->
Windows Analytics is een set oplossingen waarmee u inzicht kunt krijgen in de huidige status van uw omgeving. Apparaten in uw omgeving rapporteren Windows telemetriegegevens. De gegevens kunnen worden geopend via de Azure Portal. In het geval van Upgradegereedheid zijn de gegevens rechtstreeks beschikbaar in het knoop punt controle van de Configuration Manager-console.


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Beheer van mobiele apparaten

### <a name="updates-to-android-for-work-sharing-configuration"></a>Updates voor de configuratie van het delen van Android for work
<!-- 1338403 -->
In deze release zijn de waarden voor de instelling **gegevens delen tussen werk en persoonlijk profiel** in de instellings groep voor **werk profielen** bijgewerkt. Er is ook een aangepaste instelling voor het blok keren van kopiëren/plakken tussen het werk profiel en persoonlijke profielen toegevoegd.


### <a name="android-and-ios-enrollment-restrictions"></a>Inschrijvings beperkingen voor Android-en iOS-apparaten
<!-- 1290826 -->
Met deze versie kunt u nu opgeven dat gebruikers geen persoonlijke Android-of iOS-apparaten kunnen inschrijven. Met de instellingen voor nieuwe apparaatinstellingen kunt u de registratie van Android-apparaten beperken tot vooraf gedeclareerde apparaten. Voor iOS-apparaten kunt u de inschrijving van alle apparaten blok keren, behalve die die zijn Inge schreven bij de Device Enrollment Program van Apple, Apple Configurator of het intune-account voor apparaatinschrijvingsmanager.

## <a name="protect-devices"></a>Apparaten beveiligen

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Vertrouwens relatie voor specifieke bestanden en mappen in een Device Guard-beleid toevoegen
<!--1324676-->
In deze release hebben we meer mogelijkheden toegevoegd aan het beheer van het Device Guard-beleid.

U kunt nu desgewenst vertrouwen toevoegen voor specifieke bestanden voor mappen in een Device Guard-beleid. Hiermee kunt u het volgende doen:

- Problemen oplossen met het gedrag van beheerde installatie Programma's
- Regel-of-Business-Apps vertrouwen die niet met Configuration Manager kunnen worden geïmplementeerd
- Apps vertrouwen die zijn opgenomen in een installatie kopie van een besturings systeem

Zie [device Guard Management with Configuration Manager](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)voor meer informatie.