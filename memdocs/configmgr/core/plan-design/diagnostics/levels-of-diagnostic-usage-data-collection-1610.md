---
title: Diagnostische gegevens voor 1610
titleSuffix: Configuration Manager
description: Meer informatie over de niveaus van diagnostische en gebruiks gegevens die Configuration Manager versie 1610 verzamelt.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 02b1eb010cc874e75b733b567ce4f41e59eab82e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128794"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-configuration-manager"></a>Niveaus van het verzamelen van diagnostische gebruiks gegevens voor versie 1610 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager versie 1610 verzamelt drie niveaus van diagnostische gegevens en gebruik: **basis**, **uitgebreid**en **volledig**. Deze functie is standaard ingesteld op het niveau Uitgebreid. In de volgende secties vindt u meer informatie over de gegevens die op elk niveau worden verzameld.

Wijzigingen ten opzichte van vorige versies worden aangegeven met ***[New]***, ***[updated]***, ***[dismoved]*** of ***[dismoved]***.


> [!IMPORTANT]
>  Configuration Manager verzamelt geen site codes, namen van sites, IP-adressen, gebruikers namen, computer namen, fysieke adressen of e-mail adressen op het niveau basis of uitgebreid. Een verzameling van deze informatie op het niveau volledig is niet doel gericht, die mogelijk is opgenomen in geavanceerde diagnostische gegevens, zoals logboek bestanden of moment opnamen van het geheugen. Micro soft gebruikt deze informatie niet om u te identificeren, contact met u op te nemen of reclame te ontwikkelen.

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Niveau wijzigen
 Beheerders met een op rollen gebaseerd administratief bereik met **wijzigings** machtigingen voor de object klasse **site** kunnen het niveau wijzigen van de gegevens die zijn verzameld in de instellingen voor diagnostische gegevens en gebruik in de Configuration Manager-console.

Vanaf versie 1610 wijzigt u het niveau van de gegevens verzameling vanuit de-console door te navigeren naar **beheer**  >  **overzicht**  >  **site configuratie**  >  **sites**. Open de instellingen van de **hiërarchie**en selecteer vervolgens het gegevens niveau dat u wilt gebruiken.  

##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Niveau 1 - Basis
 Het niveau basis omvat gegevens over uw hiërarchie, gegevens die nodig zijn om uw installatie-of upgrade-ervaring te verbeteren en gegevens die u helpen bij het bepalen van de Configuration Manager updates die van toepassing zijn voor uw hiërarchie.

 voor Configuration Manager versie 1610 omvat dit niveau het volgende:


- Setup-informatie:
  - Bouwen, type installatie, taal pakketten, functies die u hebt ingeschakeld  

  - Implementatie status en fouten van update pakket, download voortgang en vereiste fouten    

  - Versie van script na de upgrade

  - Gebruik van snelle ring van updates

  - ***[Nieuw]*** Gebruik vóór de release, type installatie media, vertakkings type

  - ***[Nieuw]*** Verval datum Software Assurance

- Meetgegevens over databaseprestaties (informatie over replicatieverwerking, beste in SQL Server opgeslagen procedures op processor- en schijfgebruik)

- Basis database configuratie (processors, cluster configuratie en configuratie van gedistribueerde weer gaven)

- Configuration Manager-database schema (hash van alle object definities)

- Aantal Configuration Manager client versies en besturingssysteem versies

- Aantal besturings systemen voor beheerde apparaten en beleids regels die zijn ingesteld door de Exchange connector

- Aantal client talen en land instellingen

- Aantal Windows 10-apparaten per branch en build

- Basis gegevens van Configuration Manager site hiërarchie (site lijst, type, versie, status, aantal clients en tijd zone)

- Basis informatie over de site systeem server (gebruikte site systeem rollen, Internet-en SSL-status, besturings systeem, processors en fysieke of virtuele machine)

- Basis statistieken voor gebruikers detectie (aantal gebruikers detectie en minimale/maximale/gemiddelde groeps grootten)

- Basis Endpoint Protection informatie (client versies voor antimalware)

- Het aantal basis toepassingen en implementatie typen (totaal aantal apps, totaal aantal apps met meerdere implementatie typen, totaal aantal apps met afhankelijkheden, totaal aantal vervangen apps en het aantal implementatie technologieën dat in gebruik is)

- Basis aantallen van het besturings systeem (OSD) (installatie kopieën)

- Distributie punt-en beheer punt typen en elementaire informatie over de configuratie (beveiligd, voor bereid, PXE, multi cast, SSL-status, pull/peer-distributie punten, MDM-functionaliteit, SSL-functionaliteit, enzovoort)

- Telemetriestatistieken (wanneer uitgevoerd, runtimefouten)

- Geconfigureerde telemetrie-niveau, modus (online of offline) en configuratie van snelle updates

- Gebruik van netwerk detectie (ingeschakeld of uitgeschakeld)
- Beheer console:

  - Statistieken over console verbindingen (versie van het besturings systeem, de taal, de SKU en de architectuur, het systeem geheugen, het aantal logische processors, de verbinding van de site-ID, de geïnstalleerde .NET-versies en console taal pakketten)    

- SQL-versie, service pack level, Edition, collatie-ID en tekenset


##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Niveau 2 - Uitgebreid
Het niveau uitgebreid is de standaard instelling nadat de installatie is voltooid. Dit niveau omvat gegevens die worden verzameld op basis niveau en functie-specifieke gegevens (frequentie en duur van gebruik), Configuration Manager client instellingen (onderdeel naam, status en bepaalde instellingen zoals polling-intervallen) en basis informatie over software-updates.

Dit niveau wordt aanbevolen omdat micro soft de minimale gegevens biedt die nodig zijn om nuttige verbeteringen aan te brengen in toekomstige versies van producten en services. Dit niveau verzamelt geen object namen (sites, gebruikers, computers of objecten), Details van aan beveiliging gerelateerde objecten of beveiligings problemen zoals het aantal systemen waarvoor software-updates zijn vereist.

Voor Configuration Manager versie 1610 omvat dit niveau het volgende:

-   **Toepassings beheer:**  

    -    Elementaire informatie over gebruik/targeting voor implementatie typen die in de organisatie worden gebruikt (gebruiker versus apparaat gericht, vereist versus beschikbaar en universele apps)  

    -   Informatie over de implementatie van toepassingen (installeren/verwijderen, vereist goed keuring, gebruikers interactie ingeschakeld/uitgeschakeld, afhankelijkheid en vervanging)  

    -   Statistieken over beschikbare toepassingsaanvragen  

    -   Aantal pakketten per type  

    -   Aantal van toepassing zijnde toepassingen per besturingssysteem  

    -   Aantal pakket/programma-implementaties  

    -   Aantal App-V-omgevingen en implementatie-eigenschappen  

    -   Aantal toepassingen met een Windows 10-licentie  

    -   Mini maal/Maxi maal/gemiddeld aantal toepassings implementaties per gebruiker/apparaat per tijds periode

    -   Type onderhoudsvenster en duur  

    -  Toepassings beleids grootte en complexiteits statistieken

    - ***[Bijgewerkt]*** Aantal Windows Store voor bedrijven-apps en synchronisatie statistieken (inclusief de samenvatte typen apps, de status van de app met een licentie en het aantal online en offline gelicentieerde apps)  

    - Statistieken over grens groepen (hoeveel snelle, aantal trage en aantal per groep)

    - MSI-configuratie opties en-tellingen

    - App-vereisten (aantal ingebouwde voor waarden wordt verwezen door de implementatie technologie)

    - Vervanging van app, maximum diepte van keten

    - Gebruik van Universal Data Access (UDA), hoe gemaakt

    - ***[Nieuw]*** Toepassings goedkeurings statistieken en gebruiks frequentie



-   **Serviceclient**  

    -   Lijst met en aantal ingeschakelde clientagents  

    -   Aantal clientinstallaties vanaf elk bronlocatietype  

    -   Aantal mislukte clientinstallaties  

    -  ***[Bijgewerkt]*** Automatische client upgrade: implementatie configuratie inclusief client Piloting en uitgesloten gebruik (uitgebreide interoperabiliteits client)

    -  Client status statistieken en samen vatting van belangrijkste problemen

    - BIOS-leeftijd in jaren

    - Leeftijd van het besturings systeem in maanden

    - Aantal software Center-acties

    - De AMT-client versie (Active Management Technology)

    - Download fouten client implementatie

    - Status van bewerkings actie client melding (aantal keer dat elk wordt uitgevoerd, maximum aantal beoogde clients en gemiddeld succes percentage)

    - Implementatie methoden die worden gebruikt voor de client en het aantal clients per implementatie methode

    - Configuratie van client cache grootte

    - ***[Nieuw]***  Aantal hardware-inventaris klassen, software-inventarisatie regels en regels voor bestands verzameling




- **Cloud Services:**

  - Aantal verzamelingen dat is gesynchroniseerd met Operations Management Suite

  -  Of de Cloud connector van Operations Management Suite is ingeschakeld

  - ***[Nieuw]*** Configuratie-en gebruiks statistieken van cloudbeheergateway

  - ***[Nieuw]*** Aantal Upgrade Analytics-connectors




- **Reeksen**

    -  Statistieken verzamelings evaluatie (query tijd, toegewezen versus niet-toegewezen aantallen, tellingen op type, ID-rollover en regel gebruik)

    - Verzamelingen zonder een implementatie

    - Gebruik van verzamelings-ID (niet-uitgevoerde Id's)



-   **Instellingen voor naleving:**  

    -   Aantal configuratie-items per type  

    -   Basislijninformatie over basisconfiguratie (aantal, aantal implementaties en aantal verwijzingen)  

    -   Aantal implementaties die verwijzen naar ingebouwde instellingen (nu vastleggen van herstel instelling)  

    -   Aantal regels en implementaties die voor aangepaste instellingen zijn gemaakt (nu vastleggen van herstel instelling)  
    -   Aantal geïmplementeerde Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, certificaat (. pfx) en nalevings beleids sjablonen

    -  Aantal SCEP-certificaten, VPN-, Wi-Fi-, certificaat-(. pfx)-en nalevings beleid-implementaties per platform

    - Pass Port for Work-beleid (gemaakt, geïmplementeerd)



-   **Inhoudbeheer**  

    -   Aantal grenzen per type  

    -   Informatie over grens groepen (aantal grenzen en site systemen dat is toegewezen aan elke grens groep)  

    - ***[Nieuw]*** Relaties tussen grens groepen en terugval configuratie

    -   Informatie over distributiepunten groepen (aantal pakketten en distributie punten die zijn toegewezen aan elke distributiepunten groep)  

    -   Configuratie-informatie over distributie punten (gebruik van Branch-cache en distributiepunt bewaking)  

    -   Configuratie-informatie over Distribution Manager (threads, vertraging bij nieuwe pogingen, aantal nieuwe pogingen en pull-distributiepunt instellingen)  

    - ***[Nieuw]*** Aantal peer-cache-clients en gebruiks statistieken

    - ***[Nieuw]*** Statistieken voor downloaden van client inhoud


-   **Endpoint Protection:**  

    -   Endpoint Protection antimalware en Windows Firewall gebruik van beleid (aantal unieke beleids regels toegewezen aan groep)<br /><br /> Dit omvat geen informatie over de instellingen die zijn opgenomen in het beleid.  

    -   Endpoint Protection implementatie fouten (aantal Endpoint Protection beleids implementatie fout codes)  

    -   Aantal verzamelingen dat is geselecteerd om te worden weer gegeven in Endpoint Protection dash board  

    -   Aantal waarschuwingen dat is geconfigureerd voor Endpoint Protection functie  

    -   Beleid voor Advanced Threat Protection (ATP) (aantal beleids regels en of beleids regels worden geïmplementeerd)


- **Virtuelemachinemigratie**

  -   Aantal gemigreerde objecten (gebruik van de wizard Migratie)



-   **Beheer van mobiele apparaten (MDM):**  

    -   ***[Bijgewerkt]*** Aantal uitgegeven acties voor mobiele apparaten: de opdrachten vergren delen, rest vastmaken, wissen, buiten gebruik stellen en nu synchroniseren  

    -   Aantal mobiele apparaten dat wordt beheerd door Configuration Manager en Microsoft Intune en hoe deze zijn Inge schreven (bulksgewijs, op basis van gebruikers)  

    -   Polling planning voor mobiele apparaten en statistieken voor de duur van het inchecken van mobiele apparaten  

    -   Aantal beleidsregels voor mobiele apparaten  

    -   Aantal gebruikers met meerdere Inge schreven mobiele apparaten  

-   **Microsoft Intune probleem oplossing:**

    -   Aantal en de grootte van de status, status, inventaris, RDR, DDR, UDX, Tenant status, POL, LOG, CERT, CRP, Resync, CFD, RDO, BEX, ISM en nalevings berichten die worden gedownload van Microsoft Intune

    -   Aantal en grootte van Apparaatinstellingen (wissen, buiten gebruik stellen, vergren delen), telemetrie en gegevens berichten die worden gerepliceerd naar Microsoft Intune

    -   Volledige en Delta statistieken voor gebruikers synchronisatie voor Microsoft Intune


-   **Lokaal Mobile Device Management (MDM)**  

    -   Statistieken over geslaagde/mislukte lokale MDM-toepassingsimplementaties  

    -   Aantal Windows 10-bulkregistratiepakketten en -profielen  



-   **Implementatie van besturings systeem:**  

    -   Aantal opstartinstallatiekopieën, stuurprogramma's, stuurprogrammapakketten, distributiepunten met ingeschakelde multicast, distributiepunten voor PXE-functionaliteit en takenreeksen  

    -   Aantallen van het gebruik van taken reeks stappen

    - ***[Nieuw]*** Aantal editie-upgrade beleid



-   **Site-updates:**

    - Versies van geïnstalleerde Configuration Manager hotfixes




-   **Software-updates:**  

    -   Totaal/gemiddeld aantal verzamelingen met software-update-implementaties en het maximum/gemiddeld aantal geïmplementeerde updates  

    -   Aantal regels voor automatische implementatie dat is gekoppeld aan synchronisatie  

    -   Aantal regels voor automatische implementatie waarmee nieuwe updates worden gemaakt of waarmee updates worden toegevoegd aan een bestaande groep  

    -   Beschik bare en deadline Deltas die worden gebruikt in regels voor automatische implementatie  

    -   Gemiddeld en maximumaantal toewijzingen per update  

    -   Aantal updates dat is gemaakt en geïmplementeerd met System Center update Publisher  

    -   Aantal updategroepen en toewijzingen  

    -   Aantal update pakketten en het maximale/minimale/gemiddelde aantal distributie punten dat is gericht op pakketten  

    -   Aantal updategroepen en minimaal/maximaal/gemiddeld aantal updates per groep  

    -   Aantal updates en het percentage updates dat is geïmplementeerd, verlopen, vervangen, gedownload en gebruiksrecht overeenkomst bevat  

    -   Foutcodes voor updatescans en het aantal computers  

    -   Evaluatie van client-updates en scanplanningen  

    -   Synchronisatieplanning voor software-updatepunten  

    -   Aantal regels voor automatische implementatie met meerdere implementaties  

    -   Configuraties die worden gebruikt voor actieve Windows 10-onderhouds plannen  

    -   Versies van Windows 10-dashboardinhoud  

    -   Aantal Windows 10-clients die gebruikmaken van Windows Update voor bedrijven  

    -   Statistieken over clusterpatching  

    -   Aantal geïmplementeerde Office 365-updates  

    -   Classificaties die worden gesynchroniseerd door software-update punt

    -   Taakverdelings statistieken voor software-update punten

    -  ***[Nieuw]*** Configuratie van updates voor Windows 10 Express




-   **SQL/prestatiegegevens:**  

    -   Aantal van de grootste databasetabellen  

    -   ***[Bijgewerkt]***  Informatie over de SQL AlwaysOn-replica, het gebruik en de integriteits status

    -  Bewaar periode voor het bijhouden van SQL-wijzigingen

    - Detectie typen, ingeschakeld en plannen (volledig, incrementeel)

    - Operationele statistieken voor detectie (aantal gevonden objecten)

    - Prestatie problemen met het bijhouden van SQL-wijzigingen, de Bewaar periode en de status van automatisch opschonen



- **Diversen**

    - Aantal sites met Wake on LAN (WOL)

    - ***[Nieuw]*** Statistieken over gebruik en prestaties rapporteren  



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Niveau 3 - Volledig
Het niveau volledig omvat alle gegevens in de niveaus basis en uitgebreid. Het omvat ook aanvullende informatie over Endpoint Protection, percentages van updatenaleving en informatie over software-updates.  Dit niveau kan ook geavanceerde diagnostische gegevens bevatten, zoals systeem bestanden en moment opnamen van het geheugen, die persoonlijke gegevens kunnen bevatten die in het geheugen of logboek bestanden aanwezig zijn op het moment van vastleggen.

Voor Configuration Manager versie 1610 omvat dit niveau het volgende:

-   Evaluatie van verzamelingen en vernieuwingsstatistieken

-   Samenvatting van Endpoint Protection-status (waaronder het aantal beveiligde clients, risicoclients, onbekende clients en niet-ondersteunde clients)

-   Endpoint Protection-beleidsconfiguratie

-   Informatie over implementatie van software-updates (percentage van implementaties die zijn gericht op client versus UTC-tijd, vereist versus optioneel versus stil en onderdrukking opnieuw opstarten)

-   Algemene naleving van software-update-implementaties

-   Informatie over de evaluatieplanning voor regels voor automatische implementatie

-   Aantal fouten en foutcodes voor software-update-implementaties

-   Minimaal/maximaal/gemiddeld aantal inactieve clients in verzamelingen voor software-update-implementaties

-   Aantal groepen met verlopen software-updates

-   Minimaal/maximaal/gemiddeld aantal software-updates per pakket

-   Percentage van geslaagde software-updatescans

-   Minimaal/maximaal/gemiddeld aantal uren sinds de vorige software-updatescan

-    Software-update producten gesynchroniseerd door software-update punt
-    Instellingen voor naleving: SCEP-, VPN-, Wi-Fi-en nalevings beleid sjabloon configuratie Details

-    Type EAS-beleid voor voorwaardelijke toegang (blok of quarantaine) voor apparaten die door intune worden beheerd

-   Top 50 Cpu's in de omgeving

-   DCM-configuratie pakket voor Configuration Manager gebruik

-   MSI-product code (algemene apps die door klanten worden geïmplementeerd)

-   ATP-status samenvatting

-   Gedetailleerde installatie fouten voor client implementatie

- ***[Nieuw]*** Details van Windows Store voor bedrijven-toepassing (niet-geaggregeerde lijst met gesynchroniseerde toepassingen, waaronder AppID, online status of offline status en totaal aantal aangeschafte licenties)
