---
title: Nieuw in versie 1606
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1606 van Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3817551c75557a275c98e8c62faef46185438a25
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993604"
---
# <a name="what39s-new-in-version-1606-of-configuration-manager"></a>Wat&#39;s nieuw in versie 1606 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1606 voor Configuration Manager is beschikbaar als een update in de console voor eerder geïnstalleerde sites waarop versie 1511 of 1602 wordt uitgevoerd. Versie 1511 is de oorspronkelijke basislijn versie die u gebruikt om nieuwe Configuration Manager-sites te installeren.
> [!TIP]  
> Meer informatie over:  
>   
> - [Nieuwe sites installeren](../../servers/deploy/install/prepare-to-install-sites.md) (met een basislijn versie zoals 1511)  
> - [Updates installeren op sites](../../servers/manage/updates.md) (zoals update 1602 en 1606)  

 De volgende secties bevatten informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1606 van Configuration Manager.  



## <a name="updates-and-servicing"></a><a name="updatesandservicing"></a>Updates en onderhoud

### <a name="changes-for-the-updates-and-servicing-node"></a>Wijzigingen voor het knoop punt updates en onderhoud
De volgende wijzigingen zijn aangebracht in het knoop punt updates en onderhoud in de Configuration Manager-console:
> [!NOTE]
> Deze wijzigingen zijn pas beschikbaar nadat u versie 1606 hebt geïnstalleerd.

- **Wijziging van knooppunt naam:**

    In de werk ruimte **bewaking** is de naam van het knoop punt voor **site onderhoud** gewijzigd in de **status updates en onderhoud**.
- **Meer details over de installatie status:**

    Wanneer u de update-installatie status voor een site bekijkt, worden in de console nu afzonderlijke details weer gegeven voor de volgende acties:
    - **Downloaden** (dit is alleen van toepassing op de site op het hoogste niveau waar de site systeemrol voor het service aansluitpunt is geïnstalleerd.)
    - **Replicatie**
    - **Controle op vereisten**
    - **Installatie**

  Daarnaast vindt u hier meer gedetailleerde informatie over elke stap, waaronder het logboek bestand dat u kunt weer geven voor meer informatie.  
-   **Nieuwe optie voor het opnieuw proberen van vereiste fouten:**

    In de werk ruimten **beheer** en **bewaking** bevat het knoop punt **updates en onderhoud** een nieuwe knop op het lint met de naam **waarschuwingen over vereisten negeren**.

    Wanneer u updates installeert zonder gebruik te maken van de optie voor het negeren van waarschuwingen over vereisten (vanuit de wizard updates) en de installatie van de update stopt vanwege een waarschuwing, kunt u de **waarschuwingen voor vereisten negeren** selecteren op het lint. Dit leidt tot een automatische voortzetting van de installatie van de update.  



- **Overzichtelijke weer gave van updates:**

    In het knoop punt **updates en onderhoud** ziet u nu alleen de meest recent geïnstalleerde update en eventuele nieuwe updates die beschikbaar zijn voor installatie. Als u eerder geïnstalleerde updates wilt weer geven, klikt u op de knop nieuw **geschiedenis** die wordt weer gegeven op het lint.  

-   **De naam van de optie is gewijzigd voor de pre-productie:**

    De knop **client opties** in het knoop punt **updates en onderhoud** wordt nu de client voor de **pre-productie verhogen**genoemd.


###  <a name="pre-release-features"></a>Pre-release functies
Vanaf 1606 moet u toestemming geven voor het gebruik van functies van de voorlopige versie in Configuration Manager voordat u het gebruik ervan kunt selecteren en inschakelen. Zie [Use pre-release features from updates](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Functies van evaluatieversies gebruiken) voor meer informatie.

### <a name="new-distribution-point-update-behavior"></a>Gedrag nieuwe update van distributie punt
Update 1606 introduceert wijzigingen die de beschik baarheid van distributie punten verbeteren wanneer u toekomstige updates installeert.

Wanneer u na de installatie van update 1606 een update installeert op die site waarvoor de automatische herinstallatie van de site systeem rollen van het standaard-en pull-distributie punt vereist is, gaan alle distributie punten niet meer offline om op hetzelfde moment te worden bijgewerkt. In plaats daarvan gebruikt de site server de inhouds distributie-instellingen van de site om de update op een bepaald moment te distribueren naar een subset van distributie punten. Het resultaat is dat slechts enkele distributie punten offline gaan om de update te installeren. Hierdoor kunnen distributie punten die nog niet zijn begonnen met bijwerken of die de update hebben voltooid, online blijven en inhoud aan clients kunnen leveren.



## <a name="accessibility"></a><a name="accessibility"></a> Toegankelijkheids
Als u wilt navigeren tussen de verschillende knoop punten van een werk ruimte, kunt u nu de eerste letter van de naam van een knoop punt invoeren. Bij elke toets wordt de cursor verplaatst naar het volgende knoop punt dat begint met die letter. Voor gebruikers met een scherm lezer leest de lezer de naam van het knoop punt. Zie [toegankelijkheids functies](../../../core/understand/accessibility-features.md)voor meer informatie over toegankelijkheids opties.

## <a name="administration"></a><a name="administration"></a>Beheer
De volgende wijzigingen zijn aangebracht in beheer in de Configuration Manager-console:
### <a name="oms-connector"></a>OMS-connector

U kunt Configuration Manager nu als verzamelingen verbinden van Configuration Manager aan de [Microsoft Operations Management Suite (OMS)](/azure/azure-monitor/overview). Dit maakt gegevens zoals verzamelingen uit uw Configuration Manager-implementatie zichtbaar in OMS. Zie [gegevens van Configuration Manager naar het Microsoft Operations Management Suite synchroniseren voor](/azure/azure-monitor/platform/collect-sccm)meer informatie.

De OMS-connector is een voorlopige versie-functie. Zie [functies van voorlopige versies van updates gebruiken](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)om de functie in te scha kelen.

### <a name="support-for-cache-size-in-client-settings"></a>Ondersteuning voor cache grootte in client instellingen

U kunt nu de grootte van de cachemap configureren op client computers met **client instellingen** in de Configuration Manager-console. U kunt de client cache pas eerder instellen tijdens het installeren of opnieuw installeren van de-client software. U kunt nu de cache grootte opgeven als een client instelling (standaard of aangepast) en vervolgens deze instellingen Toep assen met de volgende beleids update op de client, zonder dat een client opnieuw hoeft te worden geïnstalleerd. Zie [De clientcache configureren voor Configuration Manager-clients](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache)voor meer informatie.

## <a name="on-premises-mobile-device-management"></a>On-premises Mobile Device Management

### <a name="support-for-multiple-device-management-points"></a>Ondersteuning voor meerdere Apparaatbeheer punten

On-premises Mobile Device Management (MDM) biedt nu ondersteuning voor een nieuwe mogelijkheid in Windows 10 jubileum update waarmee automatisch een geregistreerd apparaat wordt geconfigureerd om meer dan één apparaatbeheerpunt beschikbaar te maken voor gebruik. Met deze functie kan het apparaat terugvallen op een ander apparaatbeheerpunt wanneer het normaal gesp roken niet beschikbaar is. Deze functie werkt alleen voor Pc's en apparaten waarop de Windows 10 jubileum update is geïnstalleerd.


## <a name="application-management"></a>Toepassingsbeheer

### <a name="manage-apps-from-the-windows-store-for-business"></a>Apps beheren via de Windows Store voor Bedrijven

[Windows Store voor bedrijven](https://www.microsoft.com/business-store) is waar u Windows-apps voor uw organisatie kunt vinden en aanschaffen, hetzij afzonderlijk of op volume. Als u de Store verbindt met Configuration Manager, kunt u de lijst met apps die u hebt aangeschaft met Configuration Manager synchroniseren, deze weer geven in de Configuration Manager-console en deze implementeren zoals elke andere app.

Zie [apps beheren in de Windows Store voor bedrijven met Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)voor meer informatie.

### <a name="manage-ios-volume-purchased-apps"></a>iOS-apps beheren die zijn gekocht via het volume-aankoopprogramma

De werk stroom voor het beheren van iOS-apps die zijn gekocht via het volume en het implementeren van deze met Configuration Manager, is verbeterd.


### <a name="software-center-user-interface"></a>Gebruikers interface van software Center

De gebruikers interface van software Center is gestroomlijnd voor een eenvoudiger detectie.
*  De tabbladen **installatie status** en **geïnstalleerde software** zijn gecombineerd tot één tabblad **installatie status** .
*  **Updates**, **besturings systemen**en **toepassingen** zijn onderverdeeld in drie afzonderlijke tabbladen.
* U kunt nu meerdere updates tegelijk selecteren voor installatie, of alle updates kunnen tegelijk worden geïnstalleerd door te klikken op **Alles installeren**.

### <a name="content-status-links"></a>Inhouds status koppelingen
Voor de eigenschappen van een toepassing of pakket is er nu een koppeling waarmee u naar de status van dat object gaat.

## <a name="software-updates"></a>Software-updates

### <a name="client-setting-to-manage-the-microsoft-365-client-agent"></a>Client instelling voor het beheren van de Microsoft 365-client agent
U kunt nu een Configuration Manager client instelling gebruiken om de Microsoft 365-client agent te beheren. Nadat u dit hebt ingesteld en Microsoft 365 updates hebt geïmplementeerd, werkt de Configuration Manager-client agent met de Microsoft 365-client agent om Microsoft 365 updates te downloaden en te installeren vanaf een distributie punt.

Zie [updates van Microsoft 365-apps beheren met Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie.

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Clients hand matig overschakelen naar een nieuw software-update punt
U kunt nu een optie inschakelen waarmee Configuration Manager-clients overschakelen naar een nieuw software-update punt wanneer er problemen zijn met het actieve software-update punt. Nadat deze optie is ingeschakeld, zoeken de clients naar een ander software-updatepunt bij de volgende scan.

Zie [software-updates plannen in Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs)voor meer informatie.

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Opties voor het opnieuw opstarten van Windows 10-clients na de installatie van een software-update
Wanneer een software-update waarvoor opnieuw opstarten is vereist, wordt geïmplementeerd met behulp van Configuration Manager en is geïnstalleerd op een computer, wordt een wacht tijd opnieuw opstarten gepland. Er wordt ook een dialoog venster voor opnieuw opstarten weer gegeven. Vanaf Configuration Manager versie 1606 zijn de opties **bijwerken en opnieuw opstarten** en **bijwerken en afsluiten** beschikbaar wanneer het opnieuw opstarten in behandeling is voor een Configuration Manager software-update. Deze zijn beschikbaar in de Windows-energie opties van Windows 10-computers. Nadat u een van deze opties hebt gebruikt, wordt het dialoog venster opnieuw opstarten niet weer gegeven nadat de computer opnieuw is opgestart.

Zie [software-updates plannen](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions)voor meer informatie.

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Compatibiliteits scan voor software-updates uitvoeren onmiddellijk nadat een client software-updates heeft geïnstalleerd en opnieuw is opgestart
U kunt nu een compatibiliteits scan uitvoeren direct nadat een client software-updates heeft geïnstalleerd en opnieuw is opgestart. Als u dit voor een implementatie wilt instellen, selecteert u op de pagina **gebruikers ervaring** van de wizard software-updates implementeren of voor een **Update in deze implementatie een herstart van het systeem vereist is, voert u de evaluatie cyclus voor de implementatie van updates uit na het opnieuw opstarten**. Hierdoor kan de client controleren op aanvullende software-updates die van toepassing zijn nadat de client opnieuw is opgestart, en deze vervolgens installeren (en voldoen aan de voor waarden) tijdens hetzelfde onderhouds venster. Zie [software-updates automatisch implementeren](../../../sum/deploy-use/automatically-deploy-software-updates.md) of software- [updates hand matig implementeren](../../../sum/deploy-use/manually-deploy-software-updates.md)voor meer informatie.

## <a name="operating-system-deployment"></a>Implementatie van besturingssystemen

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Verbeteringen in de taken reeks stap: software-updates installeren
Een nieuwe instelling, **evalueren van software-updates uit scan resultaten**in de cache, biedt u de mogelijkheid om een volledige scan uit te voeren voor software-updates, in plaats van de scan resultaten in de cache te gebruiken. Zie [taken reeks stappen](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)voor meer informatie.

Daarnaast is er een nieuwe taken reeks variabele, **SMSTSSoftwareUpdateScanTimeout**, beschikbaar. Met deze variabele kunt u de time-out voor de scan van software-updates beheren tijdens de taken reeks stap software-updates installeren. De standaardwaarde is 30 minuten. Zie [ingebouwde variabelen voor de taken reeks](../../../osd/understand/task-sequence-variables.md)voor meer informatie.

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>De taken reeks variabele OSDPreserveDriveLetter is afgeschaft
De taken reeks variabele OSDPreserveDriveLetter is afgeschaft. Vanaf Configuration Manager versie 1606 bepaalt Windows Setup de beste stationsletter die moet worden gebruikt (meestal C:) tijdens de implementatie van een besturings systeem standaard.

Zie [ingebouwde variabelen voor de taken reeks](../../../osd/understand/task-sequence-variables.md)voor meer informatie.

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>De grootte van het RamDisk TFTP-venster aanpassen voor distributie punten met PXE-functionaliteit
U kunt nu de grootte van het RamDisk-venster aanpassen voor distributie punten met PXE-functionaliteit. Als u uw netwerk hebt aangepast, kan dit ertoe leiden dat het downloaden van de opstart installatie kopie mislukt met een time-outfout, omdat de grootte van het venster te groot is. Met de aanpassing van de venster grootte van RamDisk Trivial File Transfer Protocol (TFTP) kunt u TFTP-verkeer optimaliseren wanneer u PXE gebruikt om te voldoen aan uw specifieke netwerk vereisten.

Zie [site systeem rollen voorbereiden voor implementaties van besturings systemen met Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)voor meer informatie.

## <a name="compliance-settings"></a>Instellingen voor naleving

### <a name="smart-lock-setting-for-android-devices"></a>Smart Lock-instelling voor Android-apparaten
Een nieuwe instelling, **toestaan Smart Lock en andere vertrouwde agents**, zijn toegevoegd aan het Android-en Samsung KNOX Standard-configuratie-item.

Met deze instelling kunt u de Smart Lock-functie op compatibele Android-apparaten beheren. Met deze telefoon mogelijkheid, ook wel ' vertrouwde agents ' genoemd, kunt u het vergrendelings scherm van het apparaat uitschakelen of overs Laan als het apparaat zich op een vertrouwde locatie bevindt. Een vertrouwde locatie kan bijvoorbeeld zijn wanneer deze is verbonden met een specifiek Bluetooth-apparaat, of wanneer het zich in de buurt van een NFC-tag bevindt. U kunt deze instelling gebruiken om te voorkomen dat gebruikers Smart Lock configureren.


## <a name="device-configuration-and-protection"></a>Apparaatconfiguratie en-beveiliging

### <a name="product-name-changes"></a>Wijzigingen in de product naam

* Microsoft Passport for Work is nu bekend als **Windows hello voor bedrijven**.
* Ondernemingsgegevensbescherming is nu bekend als **Windows Information Protection**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Implementatie van Windows hello voor bedrijven (Pass Port for work)

U kunt nu Windows hello voor bedrijven-beleid implementeren voor Windows 10-apparaten die zijn toegevoegd aan een domein en die worden beheerd door de Configuration Manager-client.

De Configuration Manager-console is bijgewerkt om deze wijzigingen weer te geven.

### <a name="ios-activation-lock"></a>iOS-Activeringsslot
Configuration Manager kan u helpen bij het beheren van iOS-Activeringsslot, een functie van de app zoek mijn iPhone voor iOS 7,1 en hoger. Nadat de activeringsvergrendeling is ingeschakeld, moeten de Apple ID en het wachtwoord van de gebruiker worden ingevoerd voordat een van de volgende handelingen kan worden verricht:
* Zoek mijn iPhone uitschakelen.
* Het apparaat wissen.
* Activeer het apparaat opnieuw.

Configuration Manager kan u op twee manieren helpen met het beheer van de activeringsvergrendeling:

- Door activeringsvergrendeling op apparaten met supervisie in te schakelen.
- Door bypass van activeringsvergrendeling op apparaten met supervisie in te schakelen.


### <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

Endpoint Protection kunt micro soft Defender Advanced Threat Protection (ATP) beheren en bewaken. Micro soft Defender ATP is een nieuwe service waarmee bedrijven geavanceerde aanvallen op hun netwerken kunnen detecteren, onderzoeken en hierop reageren. Met Configuration Manager-beleid kunt u beheerde computers met Windows 10, versie 1607 (build 14328) of hoger op de bewaken en controleren.

Zie [micro soft Defender Advanced Threat Protection](../../../protect/deploy-use/defender-advanced-threat-protection.md)(Engelstalig) voor meer informatie.

### <a name="device-categories"></a>Apparaatcategorieën
U kunt apparaatcategorieën maken. deze kunnen worden gebruikt om apparaten automatisch in verzamelingen te plaatsen wanneer u Configuration Manager gebruikt met Microsoft Intune. Gebruikers moeten dan een apparaatcategorie kiezen wanneer ze een apparaat registreren bij intune. Daarnaast kunt u de categorie van een apparaat wijzigen vanuit de Configuration Manager-console.

Zie [apparaten automatisch categoriseren in verzamelingen met Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md)voor meer informatie.

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Apparaten vooraf declareren met IMEI-of iOS-serie nummers

U kunt apparaten in bedrijfs eigendom identificeren door de IMEI-nummers (International Station Mobile Equipment Identity) of iOS-serie nummers te importeren. U kunt een bestand met door komma's gescheiden waarden (. CSV) met IMEI-nummers uploaden of u kunt de apparaatgegevens hand matig invoeren. Geïmporteerde informatie stelt het eigendom in van de apparaten die zijn Inge schreven als ' zakelijk ' in een lijst met apparaten. Er is nog steeds een intune-licentie vereist voor elke gebruiker die toegang heeft tot de service.

### <a name="on-premises-health-attestation-service-communication"></a>Communicatie van on-premises Health Attestation-service

U kunt nu Health Attestation Services-bewaking inschakelen voor Windows 10-Pc's door alleen een lokale infra structuur te gebruiken, zodat computers zonder Internet toegang Apparaatstatusverklaring (DHA) kunnen rapporteren.

Zie [Health Attestation voor Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers)voor meer informatie.  

## <a name="remote-control"></a>Afstandsbediening
Gebruikers toestaan om bestands overdrachten te accepteren of te weigeren voordat ze inhoud van het gedeelde klem bord overbrengen in een sessie voor beheer op afstand. Gebruikers hoeven maar één keer per sessie toestemming te geven en de viewer heeft niet de mogelijkheid om zelf toestemming te geven om door te gaan met de bestands overdracht. U kunt deze nieuwe instelling vinden in de werk ruimte **beheer** . Ga naar **client instellingen**en open het deel venster **externe hulpprogram Ma's** in de **standaard instellingen**.