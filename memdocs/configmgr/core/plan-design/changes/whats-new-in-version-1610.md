---
title: Nieuwe versie 1610
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1610 van Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d23880def99fd12bffe83efffe9768f94481d07e
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993553"
---
# <a name="what39s-new-in-version-1610-of-configuration-manager"></a>Wat&#39;s nieuw in versie 1610 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1610 voor Configuration Manager current branch is beschikbaar als een update in de console voor eerder geïnstalleerde sites waarop versie 1511, 1602 of 1606 wordt uitgevoerd.


> [!TIP]  
> Als u een nieuwe site wilt installeren, moet u een basislijn versie van Configuration Manager gebruiken.  
>
> Meer informatie over:    
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Updates installeren op sites](../../servers/manage/updates.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)

De volgende secties bevatten informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1610 van Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Bewaking in de console van de installatie status van de update  
Vanaf versie 1610, wanneer u een update Pack installeert en de installatie bewaakt in de-console, is er een nieuwe fase: **na de installatie**. Deze fase bevat de status voor taken zoals het opnieuw starten van belang rijke Services en de initialisatie van replicatie bewaking. (Deze fase is pas beschikbaar in de-console nadat de site is bijgewerkt naar versie 1610.) Zie [updates binnen de console installeren](../../servers/manage/install-in-console-updates.md#bkmk_install)voor meer informatie over de installatie status van de update.


## <a name="exclude-clients-from-automatic-upgrade"></a>Clients uitsluiten van automatische upgrade
U kunt Windows-clients uitsluiten van een upgrade naar nieuwe versies van de-client software. Hiertoe neemt u de client computers op in een verzameling die is opgegeven om te worden uitgesloten van de upgrade. Clients in de uitgesloten verzameling negeren aanvragen voor het bijwerken van de client software.  Zie [Windows-clients uitsluiten van upgrades](../../clients/manage/upgrade/exclude-clients-windows.md)voor meer informatie.


## <a name="improvements-for-boundary-groups"></a>Verbeteringen voor grens groepen
Versie 1610 introduceert belang rijke wijzigingen in grens groepen en hoe deze werken met distributie punten. Deze wijzigingen kunnen het ontwerp van uw inhouds infrastructuur vereenvoudigen, terwijl u meer controle hebt over hoe en wanneer clients terugval zoeken naar aanvullende distributie punten als inhouds bron locaties. Dit geldt zowel voor on-premises als in de cloud gebaseerde distributie punten.
Deze verbeteringen vervangen de concepten en gedragingen die u mogelijk kent (zoals het configureren van distributie punten om snel of langzaam te zijn). Het nieuwe model moet eenvoudiger in te stellen en te onderhouden zijn. Deze wijzigingen zijn ook de basis voor toekomstige wijzigingen waarmee andere site systeem rollen die u aan grens groepen koppelt, worden verbeterd.

Wanneer u updatet naar versie 1610, zet de update uw huidige grenzen van de grens groep om in het nieuwe model zodat deze wijzigingen de bestaande distributie configuraties van de inhoud niet storen.

Zie [grens groepen](../../servers/deploy/configure/boundary-groups.md)voor meer informatie.


## <a name="peer-cache-for-content-distribution-to-clients"></a>Peer-cache voor het distribueren van inhoud naar clients
Vanaf versie 1610 kunt u met client- **peer-cache** de implementatie van inhoud naar clients op externe locaties beheren. Peer-cache is een ingebouwde Configuration Manager oplossing waarmee clients inhoud kunnen delen met andere clients, rechtstreeks vanuit hun lokale cache.

Nadat u client instellingen hebt geïmplementeerd waarmee peer-cache voor een verzameling wordt ingeschakeld, kunnen leden van die verzameling fungeren als een peer-inhouds bron voor andere clients in dezelfde grens groep.

U kunt ook het nieuwe dash board **client gegevens bronnen** gebruiken om inzicht te krijgen in het gebruik van inhouds bronnen van peer-cache in uw omgeving.

> [!TIP]  
> Met versie 1610, peer-cache en het dash board client gegevens bronnen zijn functies van de voorlopige versie. Zie [functies van voorlopige versies van updates gebruiken](../../servers/manage/install-in-console-updates.md#bkmk_prerelease)om ze in te scha kelen.

Zie [peer-cache voor Configuration Manager-clients](../hierarchy/client-peer-cache.md)en [dash board client gegevens bronnen](../../servers/deploy/configure/monitor-content-you-have-distributed.md#client-data-sources-dashboard)voor meer informatie.


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Meerdere gedeelde distributie punten tegelijk migreren
U kunt nu de optie gebruiken om een **distributie punt opnieuw** toe te wijzen voor Configuration Manager proces parallel de hertoewijzing van maxi maal 50 gedeelde distributie punten tegelijk. Vóór deze release zijn opnieuw toegewezen distributie punten een voor een verwerkt. Zie [meerdere gedeelde distributie punten tegelijkertijd migreren](../../migration/planning-a-content-deployment-migration-strategy.md#migrate-multiple-shared-distribution-points-at-the-same-time)voor meer informatie.

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Cloud beheer gateway voor het beheren van op internet gebaseerde clients

Cloud beheer gateway biedt een eenvoudige manier om Configuration Manager-clients op het Internet te beheren. De Cloud Management Gateway-Service, die is geïmplementeerd voor Microsoft Azure en waarvoor een Azure-abonnement is vereist, maakt verbinding met uw on-premises Configuration Manager-infra structuur met behulp van een nieuwe functie, het verbindings punt van de Cloud beheer gateway. Zodra het volledig is geïmplementeerd en geconfigureerd, kunnen clients communiceren met on-premises Configuration Manager site systeem rollen en distributie punten in de Cloud, ongeacht of ze zijn verbonden met het interne particuliere netwerk of via internet. Zie [clients op Internet beheren](../../clients/manage/manage-clients-internet.md)voor meer informatie en om te zien hoe de Cloud beheer gateway vergelijkt met client beheer op internet.

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Verbeteringen in het upgradebeleid van de Windows 10-editie
In deze release zijn de volgende verbeteringen aangebracht in dit beleids type:

- U kunt nu het beleid voor editie-upgrades gebruiken met Windows 10-Pc's waarop de Configuration Manager-client wordt uitgevoerd, naast de Windows 10-computers die zijn Inge schreven bij Microsoft Intune.
- U kunt een upgrade uitvoeren van Windows 10 Professional naar een van de platformen in de wizard die compatibel zijn met uw hardware.

## <a name="manage-hardware-identifiers"></a>Hardware-id's beheren
U kunt nu een lijst met hardware-Id's opgeven die Configuration Manager moet negeren voor het opstarten van de PXE-opstart-en client registratie. Er zijn twee veelvoorkomende problemen die kunnen worden opgelost:

1. Veel apparaten, zoals Surface Pro 3, bevatten geen onboard Ethernet-poort. Een USB-naar-Ethernet-adapter wordt doorgaans gebruikt om een bekabelde verbinding tot stand te brengen voor het implementeren van een besturings systeem. Vanwege de kosten en algemene gebruiks vriendelijkheid zijn dit echter vaak gedeelde adapters. Omdat het MAC-adres van deze adapter wordt gebruikt om het apparaat te identificeren, wordt het opnieuw gebruiken van de adapter problematisch zonder extra beheerders acties tussen elke implementatie. Nu in Configuration Manager versie 1610, kunt u het MAC-adres van deze adapter uitsluiten zodat deze eenvoudig opnieuw kan worden gebruikt in dit scenario.
2. De SMBIOS-ID moet een unieke hardware-id zijn, maar sommige gespecialiseerde hardwareapparaten zijn gebouwd met dubbele Id's. Dit probleem is mogelijk niet zo gebruikelijk als het scenario voor USB-to-Ethernet-adapters dat zojuist is beschreven, maar u kunt het adres ook adresseren met behulp van de lijst met uitgesloten hardware-Id's.

Zie [dubbele hardware-Id's beheren](../../clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)voor meer informatie.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Verbeteringen in de integratie van Windows Store voor bedrijven met Configuration Manager
Wijzigingen in deze release:
- Voorheen kon u alleen gratis apps implementeren vanuit Windows Store voor bedrijven. Configuration Manager biedt nu ook ondersteuning voor de implementatie van betaalde online gelicentieerde apps (alleen voor intune Inge schreven apparaten).
- U kunt nu een onmiddellijke synchronisatie initiëren tussen Windows Store voor bedrijven en Configuration Manager.
- U kunt nu de geheime sleutel van de client wijzigen die u hebt verkregen van Azure Active Directory.
- U kunt een abonnement verwijderen uit de Store.

Zie [apps beheren in de Windows Store voor bedrijven met Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)voor meer informatie.


## <a name="policy-sync-for-intune-enrolled-devices"></a>Beleids synchronisatie voor apparaten die zijn Inge schreven bij intune
U kunt nu een beleids synchronisatie aanvragen voor een intune-apparaat dat is inge schreven via de Configuration Manager-console, in plaats van dat u een synchronisatie wilt aanvragen van de Bedrijfsportal-app op het apparaat zelf. Informatie over de status van de synchronisatie aanvraag is beschikbaar als een nieuwe kolom in apparaat weergaven, de **externe synchronisatie status**genoemd. De informatie is ook beschikbaar in de sectie detectie gegevens van het dialoog venster **Eigenschappen** voor elk apparaat.


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Instellingen voor naleving gebruiken voor het configureren van Windows Defender-instellingen
U kunt nu Windows Defender-client instellingen configureren op door intune Inge schreven Windows 10-computers met behulp van configuratie-items in de Configuration Manager-console.
Zie de sectie **Windows Defender** in [configuratie-items maken voor Windows 8,1 en Windows 10-apparaten die worden beheerd zonder de Configuration Manager-client](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)voor meer informatie.



## <a name="general-improvements-to-software-center"></a>Algemene verbeteringen in Software Center
- Gebruikers kunnen nu apps aanvragen via Software Center en de toepassingscatalogus.
- Verbeteringen om gebruikers te helpen begrijpen welke software nieuw en relevant is.

## <a name="new-columns-in-device-collection-views"></a>Nieuwe kolommen in weer gaven voor Apparaatbeheer
U kunt nu kolommen weer geven voor **IMEI** en **serie nummer** (voor IOS-apparaten) in weer gaven voor Apparaatbeheer.

## <a name="customizable-branding-for-software-center-dialogs"></a>Aanpas bare huis stijl voor Software Center-dialoog vensters
Aangepaste huis stijl voor het Software Center werd geïntroduceerd in Configuration Manager versie 1602. In versie 1610 is die branding nu uitgebreid naar alle bijbehorende dialoog vensters om software Center-gebruikers een consistenter ervaring te bieden.

Aangepaste huis stijl voor het Software Center wordt toegepast volgens de volgende regels:

- Als de site serverrol toepassingscatalogus website punt niet is geïnstalleerd, wordt in Software Center de naam van de organisatie weer gegeven die is opgegeven in de **computer agent** -client instelling **organisatie naam weer gegeven in Software Center**. Zie [client instellingen configureren](../../clients/deploy/configure-client-settings.md)voor instructies.

- Als de site serverrol toepassingscatalogus website punt is geïnstalleerd, wordt in Software Center de naam en de kleur van de organisatie weer gegeven die zijn opgegeven in de eigenschappen van de site server functie toepassingscatalogus website punt. Zie [configuratie opties voor toepassingscatalogus website punt](../../servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)voor meer informatie.

- Als een Microsoft Intune-abonnement is geconfigureerd en verbonden met de Configuration Manager omgeving, worden in Software Center de naam van de organisatie, de kleur en het bedrijfs logo weer gegeven die zijn opgegeven in de eigenschappen van het intune-abonnement.


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Respijtperiode afdwingen voor vereiste toepassingen en software-update-implementaties
In sommige gevallen wilt u mogelijk gebruikers meer tijd geven om vereiste toepassings implementaties of software-updates te installeren na eventuele deadlines die u hebt ingesteld. Dit kan bijvoorbeeld nodig zijn wanneer een computer gedurende lange tijd is uitgeschakeld en een groot aantal toepassings-of update-implementaties moet installeren. Als een eind gebruiker bijvoorbeeld slechts een vakantie heeft geretourneerd, kan het zijn dat ze lang moeten wachten terwijl er achterstallige toepassings implementaties zijn geïnstalleerd. Om dit probleem op te lossen, kunt u nu een respijt periode voor afdwinging definiëren door Configuration Manager client instellingen te implementeren voor een verzameling. 

Voer de volgende acties uit om de respijt periode te configureren:
1. Configureer op de pagina **computer agent** van client instellingen de nieuwe eigenschap **respijt periode voor afdwingen na de deadline van de implementatie (uren)** met een waarde tussen **1** en **120** uur.
2. In een nieuwe vereiste toepassings implementatie, of in de eigenschappen van een bestaande implementatie, op de pagina **planning** , selecteert u het selectie vakje **vertraging afdwingen van deze implementatie op basis van gebruikers voorkeuren tot de respijt periode die in de client instellingen is gedefinieerd**. Alle implementaties waarvoor dit selectie vakje is ingeschakeld en die zijn gericht op apparaten waarop u ook de client instelling hebt geïmplementeerd, gebruiken de respijt periode voor afdwinging.

Als u een respijt periode voor afdwinging configureert en het selectie vakje inschakelt, wordt de installatie van de toepassing geïnstalleerd in het eerste niet-zakelijke venster dat de gebruiker heeft geconfigureerd tot die respijt periode. De gebruiker kan echter nog steeds Software Center openen en de toepassing op elk gewenst moment installeren. Zodra de respijt periode is verlopen, wordt de afdwinging hersteld naar het normale gedrag voor achterstallige implementaties. Er zijn Vergelijk bare opties toegevoegd aan de wizard software-updates implementeren, de wizard regels voor automatische implementatie en eigenschappen pagina's.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Verbeterde functionaliteit in dialoog vensters over vereiste software
Wanneer een gebruiker de vereiste software ontvangt, van de instelling **uitstellen en herinneren:** , kunnen ze in de volgende vervolg keuzelijst met waarden selecteren: 
- **Later**. Hiermee geeft u op dat meldingen worden gepland op basis van de instellingen voor meldingen die zijn geconfigureerd in de instellingen van de client agent.
- **Vaste tijd**. Hiermee geeft u op dat de melding wordt gepland om weer te geven na de geselecteerde tijd (bijvoorbeeld in 30 minuten).

![Pagina computer agent in instellingen van client agent](media/client-notification-settings.png)

De maximale uitstel tijd is gebaseerd op meldings waarden die zijn geconfigureerd in de instellingen van de client agent. Als de **implementatie deadline van meer dan 24 uur is, herinnert u gebruikers elke (uur)** instelling op de pagina computer agent is 10 uur geconfigureerd en is deze meer dan 24 uur voor de deadline. de gebruiker ziet dan een aantal opties voor uitstellen, tot maar nooit meer dan 10 uur. Naarmate de deadline aanpakt, zijn er minder opties beschikbaar, in overeenstemming met de relevante instellingen van de client agent voor elk onderdeel van de implementatie tijdlijn.

Voor een implementatie met een hoog risico, zoals een taken reeks die een besturings systeem implementeert, is bovendien de gebruikers meldings ervaring nu nog resterend. In plaats van een waarschuwing op de taak balk wordt elke keer dat de gebruiker wordt gewaarschuwd dat essentieel software onderhoud vereist is, een dialoog venster zoals het volgende wordt weer gegeven op de computer van de gebruiker:

![Dialoog venster vereiste software](media/client-toast-notification.png)


Voor meer informatie:
- [Instellingen voor het beheren van implementaties met een hoog risico](../../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Clientinstellingen configureren](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Dash board voor software-updates
Gebruik het nieuwe dash board voor software-updates om de huidige nalevings status van apparaten in uw organisatie weer te geven en snel de gegevens te analyseren om te zien welke apparaten risico lopen. Als u het dash board wilt weer geven, gaat u naar **bewaking**  >  **overzicht**  >  **Security**  >  **software updates dash board**.

Zie [software-updates bewaken](../../../sum/deploy-use/monitor-software-updates.md)voor meer informatie.


## <a name="improvements-to-the-application-request-process"></a>Verbeteringen in het proces van toepassings aanvragen
Nadat u een toepassing hebt goedgekeurd voor installatie, kunt u de aanvraag vervolgens weigeren door te klikken op **weigeren** in de Configuration Manager-console. Voorheen werd deze knop grijs weer gegeven na goed keuring.

Met deze actie wordt de toepassing niet verwijderd van alle apparaten. Het programma stopt echter met het installeren van nieuwe exemplaren van de toepassing vanuit software Center.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filteren op inhouds grootte in regels voor automatische implementatie
U kunt nu filteren op de inhouds grootte voor software-updates in regels voor automatische implementatie. Als u bijvoorbeeld alleen software-updates wilt downloaden die kleiner zijn dan 2 MB, kunt u het filter voor **inhouds grootte (KB)** instellen op **< 2048**. Met dit filter wordt voor komen dat grote software-updates automatisch worden gedownload, wat een vereenvoudigd Windows-onderhoud op lagere niveaus ondersteunt wanneer de netwerk bandbreedte beperkt is. Zie deze artikelen voor meer informatie:
- [Configuration Manager en vereenvoudigd Windows-onderhoud op besturings systemen van lagere niveaus](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056)
- [Software-updates automatisch implementeren](../../../sum/deploy-use/automatically-deploy-software-updates.md)

Voer een van de volgende handelingen uit om het veld **inhouds grootte (KB)** te configureren:
- Wanneer u een regel voor automatische implementatie maakt, gaat u in de wizard regel voor automatische implementatie maken naar de pagina **software-updates** .
- Ga in de eigenschappen voor een bestaande regel voor automatische implementatie naar het tabblad **software-updates** .

## <a name="office-365-client-management-dashboard"></a>Office 365-dash board voor client beheer
Het Office 365-dash board voor client beheer is nu beschikbaar in de Configuration Manager-console. Als u het dash board wilt weer geven, gaat u naar **software bibliotheek**  >  **Overview**  >  **Office 365 client management**.

In het dash board worden grafieken weer gegeven voor het volgende:

- Aantal Office 365-clients
- Office 365-client versies
- Office 365-client talen
- Office 365-client kanalen

Zie [updates van Microsoft 365-apps beheren](../../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie.

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Takenreeksstappen voor het beheren van de conversie van BIOS naar UEFI
U kunt nu een taken reeks met een implementatie van een besturings systeem aanpassen met een nieuwe variabele, TSUEFIDrive, zodat de stap **computer opnieuw opstarten** een FAT32-partitie op de harde schijf voorbereidt voor overgang naar UEFI. De volgende procedure bevat een voor beeld van hoe u taken reeks stappen kunt maken om de harde schijf voor te bereiden voor de conversie van BIOS naar UEFI. Zie  [taken reeks stappen voor het beheren van de conversie van BIOS naar UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md)voor meer informatie.

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Verbeteringen aan de taken reeks stap: ConfigMgr-client voorbereiden voor vastleggen  
Met de stap ConfigMgr-client voorbereiden wordt de Configuration Manager-client nu volledig verwijderd, in plaats van alleen de sleutel gegevens te verwijderen. Wanneer de taken reeks de vastgelegde installatie kopie van het besturings systeem implementeert, wordt elke keer een nieuwe Configuration Manager-client geïnstalleerd. Zie [taken reeks stappen](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)voor meer informatie.



## <a name="intune-compliance-policy-charts"></a>Diagrammen van intune-nalevings beleid
U kunt nu een snel overzicht krijgen van de algemene compatibiliteit voor apparaten en de belangrijkste redenen voor niet-naleving met behulp van nieuwe grafieken onder de werk ruimte **bewaking** in de Configuration Manager-console. U kunt op een sectie in het diagram klikken om in te zoomen op een lijst met apparaten in die categorie. Zie [het nalevings beleid bewaken](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)voor meer informatie.


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Lookout-integratie voor hybride implementaties om iOS-en Android-apparaten te beveiligen
Micro soft integreert met de oplossing voor beveiliging tegen mobiele bedreigingen van Lookout om mobiele iOS-en Android-apparaten te beveiligen door malware, Risk ante apps en meer op apparaten te detecteren. De oplossing van Lookout helpt u bij het bepalen van het bedreigings niveau dat kan worden geconfigureerd. U kunt een nalevings beleids regel maken in Configuration Manager om de apparaatcompatibiliteit te bepalen op basis van de risico analyse van Lookout. Met behulp van beleid voor voorwaardelijke toegang kunt u toegang tot bedrijfsbronnen toestaan of blokkeren op basis van de apparaatnalevingsstatus.

Gebruikers van niet-compatibele iOS-apparaten wordt gevraagd om in te schrijven. Ze moeten de Lookout for Work-app op hun apparaten installeren, de app activeren en bedreigingen herstellen die zijn gerapporteerd in de Lookout for Work toepassing om toegang te krijgen tot Bedrijfs gegevens.


## <a name="new-compliance-settings-for-configuration-items"></a>Nieuwe instellingen voor naleving voor configuratie-items
Er zijn veel nieuwe instellingen die u in de configuratie-items voor verschillende platformen kunt gebruiken. Dit zijn instellingen die voorheen aanwezig waren in Microsoft Intune in een zelfstandige configuratie en zijn nu beschikbaar wanneer u intune gebruikt met Configuration Manager.
Zie [configuratie-items voor apparaten die worden beheerd zonder de Configuration Manager-client](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)voor meer informatie.

### <a name="new-settings-for-android-devices"></a>Nieuwe instellingen voor Android-apparaten
#### <a name="password-settings"></a>Wachtwoordinstellingen
- **Wachtwoordgeschiedenis onthouden**
- **Vingerafdruk voor ontgrendelen toestaan**

#### <a name="security-settings"></a>Beveiligingsinstellingen
- **Versleuteling vereisen op opslagkaarten**
- **Schermafbeelding toestaan**
- **Verzending van diagnostische gegevens toestaan**

#### <a name="browser-settings"></a>Browserinstellingen
- **Webbrowser toestaan**
- **Automatisch invullen toestaan**
- **Pop-upblokkering toestaan**
- **Cookies toestaan**
- **Active Scripting toestaan**

#### <a name="app-settings"></a>App-instellingen
- **Google Play Store toestaan**

#### <a name="device-capability-settings"></a>Instellingen voor apparaatfuncties
- **Verwisselbare opslag toestaan**
- **Wi-Fi-tethering toestaan**
- **Geolocatie toestaan**
- **NFC toestaan**
- **Bluetooth toestaan**
- **Spraakroaming toestaan**
- **Gegevensroaming toestaan**
- **Sms-/mms-berichten toestaan**
- **Spraakassistent toestaan**
- **Nummer inspreken toestaan**
- **Kopiëren en plakken toestaan**

### <a name="new-settings-for-ios-devices"></a>Nieuwe instellingen voor iOS-apparaten
#### <a name="password-settings"></a>Wachtwoordinstellingen
- **Aantal complexe tekens dat is vereist in wachtwoord**
- **Eenvoudige wachtwoorden toestaan**
- **Minuten inactief voordat wachtwoord is vereist**
- **Wachtwoordgeschiedenis onthouden**

### <a name="new-settings-for-mac-os-x-devices"></a>Nieuwe instellingen voor Mac OS X-apparaten
#### <a name="password-settings"></a>Wachtwoordinstellingen
- **Aantal complexe tekens dat is vereist in wachtwoord**
- **Eenvoudige wachtwoorden toestaan**
- **Wachtwoordgeschiedenis onthouden**
- **Minuten van inactiviteit voordat de schermbeveiliging wordt geactiveerd**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nieuwe instellingen voor Windows 10 Desktop-en Mobile-apparaten
#### <a name="password-settings"></a>Wachtwoordinstellingen
- **Minimum aantal tekensets**
- **Wachtwoordgeschiedenis onthouden**
- **Wacht woord vereisen wanneer het apparaat wordt geactiveerd vanuit een niet-actieve status**

#### <a name="security-settings"></a>Beveiligingsinstellingen
- **Versleuteling vereisen voor mobiel apparaat**
- **Handmatige uitschrijving toestaan**

#### <a name="device-capability-settings"></a>Instellingen voor apparaatfuncties
- **VPN via mobiele verbinding toestaan**
- **VPN-roaming via mobiele verbinding toestaan**
- **Opnieuw instellen van telefoon toestaan**
- **USB-verbinding toestaan**
- **Cortana toestaan**
- **Meldingen van onderhoudscentrum toestaan**

### <a name="new-settings-for-windows-10-team-devices"></a>Nieuwe instellingen voor Windows 10 team-apparaten
#### <a name="device-settings"></a>Apparaatinstellingen
- **Operational Insights van Azure inschakelen**
- **Draadloze Miracast-projectie inschakelen**
- **Kiezen welke vergaderingsinformatie wordt weergegeven op het welkomstscherm**
- **URL naar de achtergrondafbeelding van het vergrendelingsscherm**

### <a name="new-settings-for-windows-81-devices"></a>Nieuwe instellingen voor Windows 8,1-apparaten
#### <a name="applicability-settings"></a>Toepasselijkheidsinstellingen
- **Alle configuraties toepassen op Windows 10**

#### <a name="password-settings"></a>Wachtwoordinstellingen
- **Vereist wachtwoordtype**
- **Minimum aantal tekensets**
- **Minimale wachtwoordlengte**
- **Aantal mislukte aanmeldingen dat is toegestaan voordat het apparaat wordt gewist**
- **Minuten van inactiviteit voordat het scherm wordt uitgeschakeld**
- **Dagen tot wachtwoord verloopt**
- **Wachtwoordgeschiedenis onthouden**
- **Wachtwoorden niet opnieuw gebruiken**
- **Afbeeldingswachtwoord en PIN toestaan**

#### <a name="browser-settings"></a>Browserinstellingen
- **Automatische detectie van een intranetnetwerk toestaan**

### <a name="new-settings-for-windows-phone-81-devices"></a>Nieuwe instellingen voor Windows Phone 8,1-apparaten
#### <a name="applicability-settings"></a>Toepasselijkheidsinstellingen
- **Alle configuraties toepassen op Windows 10**

#### <a name="password-settings"></a>Wachtwoordinstellingen
- **Minimum aantal tekensets**
- **Eenvoudige wachtwoorden toestaan**
- **Wachtwoordgeschiedenis onthouden**

#### <a name="device-capability-settings"></a>Instellingen voor apparaatfuncties
- **Automatische verbinding met gratis Wi-Fi-hotspots toestaan**
