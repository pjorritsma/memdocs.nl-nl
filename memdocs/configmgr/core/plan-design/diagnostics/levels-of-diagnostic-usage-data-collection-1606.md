---
title: Diagnostische gegevens voor 1606
titleSuffix: Configuration Manager
description: Meer informatie over de niveaus van diagnostische en gebruiks gegevens die Configuration Manager versie 1606 verzamelt.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: cd58fb2ad105d3fb94fcc1d2fe56f0ae64f766f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715569"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-configuration-manager"></a>Niveaus van het verzamelen van diagnostische gebruiks gegevens voor versie 1606 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configuration Manager versie 1606 verzamelt drie niveaus van diagnostische gegevens en gebruik: **basis**, **uitgebreid**en **volledig**. Deze functie is standaard ingesteld op het niveau Uitgebreid. In de volgende secties vindt u meer informatie over de gegevens die op elk niveau worden verzameld.

Wijzigingen ten opzichte van vorige versies worden aangegeven met ***[New]***, ***[updated]***, ***[dismoved]*** of ***[dismoved]***.


> [!IMPORTANT]
>  Configuration Manager verzamelt geen site codes, namen van sites, IP-adressen, gebruikers namen, computer namen, fysieke adressen of e-mail adressen op het niveau basis of uitgebreid. Een verzameling van deze informatie op het niveau volledig is niet doel gericht, die mogelijk is opgenomen in geavanceerde diagnostische gegevens, zoals logboek bestanden of moment opnamen van het geheugen. Micro soft gebruikt deze informatie niet om u te identificeren, contact met u op te nemen of reclame te ontwikkelen.

##  <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Niveau wijzigen
 Beheerders met een op rollen gebaseerd administratief bereik met **wijzigings** machtigingen voor de object klasse **site** kunnen het niveau wijzigen van de gegevens die zijn verzameld in de instellingen voor diagnostische gegevens en gebruik in de Configuration Manager-console.

   Hiertoe gaat u in de-console naar het tabblad Back stage (het tabblad linksboven met de vervolg keuze pijl), selecteert u **gebruiks gegevens**en selecteert u vervolgens het gegevens niveau dat u wilt gebruiken.  

##  <a name="level-1---basic"></a><a name="bkmk_level1"></a> Niveau 1 - Basis
 Het niveau basis omvat gegevens over uw hiërarchie, gegevens die nodig zijn om uw installatie-of upgrade-ervaring te verbeteren en gegevens die u helpen bij het bepalen van de Configuration Manager updates die van toepassing zijn voor uw hiërarchie.

 Vanaf Configuration Manager versie 1606 omvat dit niveau het volgende:


-   Setup-informatie:
      - Bouwen, type installatie, taal pakketten, functies die u hebt ingeschakeld  

      -   Implementatie status en fouten van update pakket, download voortgang en vereiste fouten 

      -  Versie van script na de upgrade

      -  Gebruik van snelle ring van updates

-   Metrische database prestaties (informatie over replicatie verwerking, de belangrijkste SQL Server opgeslagen procedures per processor en schijf gebruik)

-   Basis database configuratie (processors, cluster configuratie en configuratie van gedistribueerde weer gaven)

-   Configuration Manager-database schema (hash van alle object definities)

-   Aantal Configuration Manager client versies en besturingssysteem versies

-   Aantal besturings systemen voor beheerde apparaten en beleids regels die zijn ingesteld door de Exchange connector

-   Aantal client talen en land instellingen

-   Aantal Windows 10-apparaten per branch en build

-   Basis gegevens van Configuration Manager site hiërarchie (site lijst, type, versie, status, aantal clients en tijd zone)

-   Basis informatie over de site systeem server (gebruikte site systeem rollen, Internet-en SSL-status, besturings systeem, processors en fysieke of virtuele machine)

-   Basis statistieken voor gebruikers detectie (aantal gebruikers detectie en minimale/maximale/gemiddelde groeps grootten)

-   Basis Endpoint Protection informatie (client versies voor antimalware)

-   Het aantal basis toepassingen en implementatie typen (totaal aantal apps, totaal aantal apps met meerdere implementatie typen, totaal aantal apps met afhankelijkheden, totaal aantal vervangen apps en het aantal implementatie technologieën dat in gebruik is)

-   Basis aantallen van het besturings systeem (OSD) (installatie kopieën)

-   Distributie punt-en beheer punt typen en elementaire informatie over de configuratie (beveiligd, voor bereid, PXE, multi cast, SSL-status, pull/peer-distributie punten, MDM-functionaliteit, SSL-functionaliteit, enzovoort)

-   Telemetrie-statistieken (bij uitvoering, Runtime en fouten)

-  Geconfigureerde telemetrie-niveau, modus (online of offline) en configuratie van snelle updates

-  Gebruik van netwerk detectie (ingeschakeld of uitgeschakeld)
-  Beheer console:

    -  Statistieken over console verbindingen (versie van het besturings systeem, de taal, de SKU en de architectuur, het systeem geheugen, het aantal logische processors, de verbinding van de site-ID, de geïnstalleerde .NET-versies en console taal pakketten)    


- ***[Nieuw]*** SQL-versie, service pack level, Edition, collatie-ID en tekenset


##  <a name="level-2---enhanced"></a><a name="bkmk_level2"></a> Niveau 2 - Uitgebreid
Het niveau uitgebreid is de standaard instelling nadat de installatie is voltooid. Dit niveau omvat gegevens die worden verzameld op het niveau basis, de functie-specifieke gegevens (frequentie en duur van gebruik), Configuration Manager client instellingen (onderdeel naam, status en bepaalde instellingen zoals polling-intervallen) en basis informatie over software-updates.

Dit niveau wordt aanbevolen omdat micro soft de minimale gegevens biedt die nodig zijn om nuttige verbeteringen aan te brengen in toekomstige versies van producten en services. Dit niveau verzamelt geen object namen (sites, gebruikers, computers of objecten), Details over beveiligings objecten of beveiligings problemen zoals het aantal systemen waarvoor software-updates zijn vereist.

Vanaf Configuration Manager versie 1606 omvat dit niveau het volgende:

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

    - ***[Nieuw]*** Aantal Windows Store voor bedrijven-apps en synchronisatie statistieken (inclusief samenvatte typen apps)  

    - ***[Nieuw]*** Statistieken over grens groepen (hoeveel snelle, aantal trage en aantal per groep)

    - ***[Nieuw]*** MSI-configuratie opties en-tellingen

    - ***[Nieuw]*** App-vereisten (aantal ingebouwde voor waarden wordt verwezen door de implementatie technologie)

    - ***[Nieuw]*** Vervanging van app, maximum diepte van keten

    - ***[Nieuw]*** Gebruik van Universal Data Access (UDA) en hoe gemaakt



-   **Serviceclient**  

    -   Lijst met en aantal ingeschakelde clientagents  

    -   Aantal clientinstallaties vanaf elk bronlocatietype  

    -   Aantal mislukte clientinstallaties  

    -  ***[Nieuw]*** Implementatie configuratie voor automatische upgrade van client, inclusief client Piloting

    -  ***[Nieuw]*** Client status statistieken en samen vatting van belangrijkste problemen

    - ***[Nieuw]*** BIOS-leeftijd in jaren

    - ***[Nieuw]*** Leeftijd van het besturings systeem in maanden

    - ***[Nieuw]*** Aantal software Center-acties

    - ***[Nieuw]*** De AMT-client versie (Active Management Technology)

    - ***[Nieuw]*** Download fouten client implementatie

    - ***[Nieuw]*** Status van bewerkings actie client melding (aantal keer dat elk wordt uitgevoerd, maximum aantal beoogde clients en gemiddeld succes percentage)

    - ***[Nieuw]*** Implementatie methoden die worden gebruikt voor de client en het aantal clients per implementatie methode

    - ***[Nieuw]*** Configuratie van client cache grootte



- ***[Nieuw]*** **Cloud Services:**

  - ***[Nieuw]*** Aantal verzamelingen dat is gesynchroniseerd met Operations Management Suite

  - ***[Nieuw]***  Of de Cloud connector van Operations Management Suite is ingeschakeld



- ***Ander Reeksen***

    -  ***[Verplaatst]*** Statistieken verzamelings evaluatie (query tijd, toegewezen versus niet-toegewezen aantallen, tellingen op type, ID-rollover en regel gebruik)

    - ***[Nieuw]*** Verzamelingen zonder een implementatie

    - ***[Nieuw]*** Gebruik van verzamelings-ID (niet-uitgevoerde Id's)



-   **Instellingen voor naleving:**  

    -   Aantal configuratie-items per type  

    -   Basislijninformatie over basisconfiguratie (aantal, aantal implementaties en aantal verwijzingen)  

    -   ***[Bijgewerkt]*** Aantal implementaties die verwijzen naar ingebouwde instellingen (nu vastleggen van herstel instelling)  

    -   ***[Bijgewerkt]*** Aantal regels en implementaties die voor aangepaste instellingen zijn gemaakt (nu vastleggen van herstel instelling)  
    -   Aantal geïmplementeerde Simple Certificate Enrollment Protocol (SCEP), VPN, Wi-Fi, certificaat (. pfx) en nalevings beleids sjablonen

    -  Aantal SCEP-certificaten, VPN-, Wi-Fi-, certificaat-en nalevings beleid-implementaties per platform

    - ***[Nieuw]*** Pass Port for Work-beleid (gemaakt, geïmplementeerd)



-   **Inhoud:**  

    -   Aantal grenzen per type  

    -   Informatie over grens groepen (aantal grenzen en site systemen dat is toegewezen aan elke grens groep)  

    -   Informatie over distributiepunten groepen (aantal pakketten en distributie punten die zijn toegewezen aan elke distributiepunten groep)  

    -   Configuratie-informatie over distributie punten (gebruik van Branch-cache en distributiepunt bewaking)  

    -   Configuratie-informatie over Distribution Manager (threads, vertraging bij nieuwe pogingen, aantal nieuwe pogingen en pull-distributiepunt instellingen)  


-   **Endpoint Protection:**  

    -   Endpoint Protection antimalware en Windows Firewall gebruik van beleid (aantal unieke beleids regels toegewezen aan groep)<br /><br /> Dit omvat geen informatie over de instellingen die zijn opgenomen in het beleid.  

    -   Endpoint Protection implementatie fouten (aantal Endpoint Protection beleids implementatie fout codes)  

    -   Aantal verzamelingen dat is geselecteerd om te worden weer gegeven in het dash board van Endpoint Protection  

    -   Aantal waarschuwingen dat is geconfigureerd voor de functie Endpoint Protection  

    - ***[Nieuw]*** Beleid voor Advanced Threat Protection (ATP) (aantal beleids regels en of beleids regels worden geïmplementeerd)


-   ***[Verwijderd]*** **Mobile Application Management (mam):**  

    -   ***[Verwijderd]*** Aantal Office-toepassingen voor MAM, line-of-business-toepassingen en beleids regels per besturings systeem  

    -   ***[Verwijderd]*** Aantal MAM-toepassingen/beleids implementaties  

    -   ***[Verwijderd]*** Aantal regels dat per MAM-instelling is gemaakt  


- ***[Nieuwe]*** **migratie:**

  -  ***[Nieuw]***  Aantal gemigreerde objecten (gebruik van de wizard Migratie)



-   **Beheer van mobiele apparaten (MDM):**  

    -   Aantal uitgegeven acties voor mobiele apparaten: vergren delen, opdrachten vastmaken, wissen en buiten gebruik stellen  

    -   Aantal mobiele apparaten dat wordt beheerd door Configuration Manager en Microsoft Intune en hoe deze zijn Inge schreven (bulk of op basis van gebruikers)  

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

    -   ***[Nieuw]*** Aantallen van het gebruik van taken reeks stappen



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

    -   ***[Nieuw]*** Taakverdelings statistieken voor software-update punten



-   **SQL/prestatiegegevens:**  

    -   Aantal van de grootste databasetabellen  

    -   Informatie over SQL Always-On-replica  

    -  Bewaar periode voor het bijhouden van SQL-wijzigingen

    - ***[Nieuw]*** Detectie typen, ingeschakeld en plannen (volledig, incrementeel)

    - ***[Nieuw]*** Operationele statistieken voor detectie (aantal gevonden objecten)

    - ***[Nieuw]*** Prestatie problemen met het bijhouden van SQL-wijzigingen, de Bewaar periode en de status van automatisch opschonen



- ***[Nieuw]*** **Diversen**

    - ***[Nieuw]*** Aantal sites met Wake on LAN (WOL)



##  <a name="level-3---full"></a><a name="bkmk_level3"></a> Niveau 3 - Volledig
Het niveau volledig omvat alle gegevens in de niveaus basis en uitgebreid. Het omvat ook aanvullende informatie over Endpoint Protection, percentages van updatenaleving en informatie over software-updates. Dit niveau kan ook geavanceerde diagnostische gegevens bevatten, zoals systeem bestanden en moment opnamen van het geheugen, die persoonlijke gegevens kunnen bevatten die in het geheugen of logboek bestanden aanwezig zijn op het moment van vastleggen.

Vanaf Configuration Manager versie 1606 omvat dit niveau het volgende:

-   Evaluatie van verzamelingen en vernieuwingsstatistieken

-   Samenvatting van Endpoint Protection-status (waaronder het aantal beveiligde clients, risicoclients, onbekende clients en niet-ondersteunde clients)

-   Endpoint Protection-beleidsconfiguratie

-   Informatie over implementatie van software-updates (percentage van implementaties die zijn gericht op client versus UTC-tijd, vereist versus optioneel versus stil en onderdrukking opnieuw opstarten)

-   Algemene naleving van software-update-implementaties

-   Informatie over de evaluatieplanning voor regels voor automatische implementatie

-   ***[Verwijderd]*** Aantal clients met beleids regels voor netwerk toegangs beveiliging

-   Aantal fouten en foutcodes voor software-update-implementaties

-   Minimaal/maximaal/gemiddeld aantal inactieve clients in verzamelingen voor software-update-implementaties

-   Aantal groepen met verlopen software-updates

-   Minimaal/maximaal/gemiddeld aantal software-updates per pakket

-   Percentage van geslaagde software-updatescans

-   Minimaal/maximaal/gemiddeld aantal uren sinds de vorige software-updatescan

-    Software-update producten gesynchroniseerd door software-update punt
-    Instellingen voor naleving: SCEP-, VPN-, Wi-Fi-en nalevings beleid sjabloon configuratie Details

-    Type EAS-beleid voor voorwaardelijke toegang (blok of quarantaine) voor apparaten die door intune worden beheerd

-   ***[Nieuw]*** Top 50 Cpu's in de omgeving

-   ***[Nieuw]*** DCM-configuratie pakket voor Configuration Manager gebruik

-   ***[Nieuw]*** MSI-product code (algemene apps die door klanten worden geïmplementeerd)

-   ***[Nieuw]*** ATP-status samenvatting

-   ***[Nieuw]*** Gedetailleerde installatie fouten voor client implementatie
