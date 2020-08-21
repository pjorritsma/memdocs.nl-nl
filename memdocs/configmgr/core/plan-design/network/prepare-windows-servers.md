---
title: Windows-servers voorbereiden
titleSuffix: Configuration Manager
description: Zorg ervoor dat een computer voldoet aan de vereisten voor gebruik als een site server of een site systeem server voor Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8585f04e6cedf9cb5158dbebc41b00565eabd989
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692720"
---
# <a name="prepare-windows-servers-to-support-configuration-manager"></a>Windows-servers voorbereiden voor de ondersteuning van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u een Windows-computer als een site systeem server voor Configuration Manager kunt gebruiken, moet de computer voldoen aan de vereisten voor het beoogde gebruik als een site server of site systeem server.  

- Deze vereisten omvatten vaak een of meer Windows-onderdelen of-rollen die worden ingeschakeld met behulp van de computers Serverbeheer.  

- Omdat de methode voor het inschakelen van Windows-onderdelen en-rollen verschilt van de versies van het besturings systeem, raadpleegt u de documentatie voor de versie van het besturings systeem voor gedetailleerde informatie over het instellen van het besturings systeem dat u gebruikt.  

De informatie in dit artikel bevat een overzicht van de typen Windows-configuraties die nodig zijn voor de ondersteuning van Configuration Manager-site systemen. Zie [site-en site systeem vereisten](../configs/site-and-site-system-prerequisites.md)voor meer informatie over de configuratie van specifieke site systeem rollen.

##  <a name="windows-features-and-roles"></a><a name="BKMK_WinFeatures"></a> Windows-onderdelen en-rollen  
Wanneer u Windows-onderdelen en-functies op een computer instelt, moet u mogelijk de computer opnieuw opstarten om deze configuratie te volt ooien. Daarom is het een goed idee om computers te identificeren die specifieke site systeem rollen zullen hosten voordat u een Configuration Manager site of site systeem server installeert.

### <a name="features"></a>Functies  
De volgende Windows-onderdelen zijn vereist op bepaalde site systeem servers en moeten worden ingesteld voordat u een site systeemrol op die computer installeert.  

- **.NET Framework**: inclusief  

    - ASP.NET  
    - HTTP-activering  
    - Niet-HTTP-activering  
    - Windows Communication Foundation-Services (WCF)  

    Verschillende site systeem rollen vereisen verschillende versies van .NET Framework.  

    Omdat .NET Framework 4,0 en hoger niet compatibel is met het vervangen van 3,5 en eerdere versies, kunt u elke versie op dezelfde computer inschakelen als er verschillende versies worden weer gegeven als vereist.  

- **Background Intelligent overboeking Services (bits)**: voor beheer punten zijn bits (en automatisch geselecteerde opties) vereist om communicatie met beheerde apparaten te ondersteunen.  

- **BranchCache**: distributie punten kunnen worden ingesteld met BranchCache ter ondersteuning van clients die BranchCache gebruiken.  

- **Gegevensontdubbeling**: distributie punten kunnen worden ingesteld met en voor deel van gegevensontdubbeling.  

- **Externe differentiële compressie (RDC)**: voor elke computer die als host fungeert voor een site server of een distributie punt is RDC vereist. RDC wordt gebruikt voor het genereren van handtekeningen van pakketten en voor het vergelijken van handtekeningen.  

### <a name="roles"></a>Rollen  
De volgende Windows-rollen zijn vereist ter ondersteuning van specifieke functionaliteit, zoals software-updates en implementaties van besturings systemen, terwijl IIS is vereist voor de meest voorkomende site systeem rollen.  

- **Registratie service voor netwerk apparaten** (onder Active Directory Certificate Services): deze Windows-rol is een vereiste voor het gebruik van certificaat profielen in Configuration Manager.  

- **Webserver (IIS)**: met inbegrip van:  
    - Veelvoorkomende HTTP-functies  
          - HTTP-omleiding  
    - Ontwikkeling van toepassingen  
          - .NET-uitbreidbaarheid  
          - ASP.NET  
          - ISAPI-uitbreidingen  
          - ISAPI-filters  
    - Beheerprogramma's  
          - Compatibiliteit met IIS 6-beheer  
          - Compatibiliteit met IIS 6-metabase  
          - Compatibiliteit met IIS 6 Windows Management Instrumentation (WMI)  
    - Beveiliging  
          - Aanvraagfiltering  
          - Windows-verificatie  

  De volgende site systeem rollen gebruiken een of meer van de vermelde IIS-configuraties:  
  - Application Catalog-webservicepunt  
  - Application Catalog-websitepunt  
  - Distributiepunt  
  - Inschrijvingspunt  
  - Proxypunt voor inschrijving  
  - Terugvalstatuspunt  
  - Beheerpunt  
  - Software-updatepunt  
  - Statusmigratiepunt     

  De minimale versie van IIS die is vereist, is de versie die wordt meegeleverd met het besturings systeem van de site server.  

  Naast deze IIS-configuraties moet u mogelijk [IIS-aanvraag filtering voor distributie punten](#BKMK_IISFiltering)instellen.  

- **Windows Deployment Services**: deze rol wordt gebruikt bij de implementatie van het besturings systeem.  

- **Windows Server Update Services**: deze rol is vereist voor software-updates.  


##  <a name="iis-request-filtering-for-distribution-points"></a><a name="BKMK_IISFiltering"></a> IIS-aanvraag filtering voor distributie punten  
IIS gebruikt standaard aanvraagfiltering om de toegang tot verschillende bestandsnaamextensies en maplocaties voor HTTP- of HTTPS-communicatie te blokkeren. Op een distributie punt wordt hiermee voor komen dat clients pakketten downloaden die geblokkeerde extensies of maplocaties hebben.  

Wanneer de bron bestanden van uw pakket extensies hebben die in IIS worden geblokkeerd door de configuratie van de aanvraag filtering, moet u aanvraag filtering instellen om ze toe te staan. Dit doet u door [de functie voor het filteren van aanvragen te bewerken](/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)) in IIS-beheer op de distributiepunt computers.  

Daarnaast worden de volgende bestandsnaam extensies gebruikt door Configuration Manager voor pakketten en toepassingen. Zorg ervoor dat de configuraties voor het filteren van aanvragen deze bestands extensies niet blok keren:  

- .PCK  
- .PKG  
- .STA  
- .TAR  

Bron bestanden voor een software-implementatie kunnen bijvoorbeeld een map met de naam **bin** bevatten of een bestand hebben met de bestandsnaam extensie **. mdb** .  

- IIS-aanvraag filtering blokkeert standaard de toegang tot deze elementen (de**bin** wordt geblokkeerd als een verborgen segment en **. mdb** wordt geblokkeerd als een bestandsnaam extensie).  

- Wanneer u de standaard IIS-configuratie op een distributie punt gebruikt, kunnen clients die gebruikmaken van BITS deze software-implementatie niet downloaden vanaf het distributie punt en aangeven dat ze wachten op inhoud.  

- Om ervoor te zorgen dat de-clients deze inhoud kunnen downloaden, bewerkt u in IIS-beheer **aanvraag filtering** om toegang te krijgen tot de bestands extensies en mappen in de pakketten en toepassingen die u implementeert.  

> [!IMPORTANT]  
> Wijzigingen in het aanvraag filter kunnen de kwets baarheid van de computer verg Roten.  
> 
> - Wijzigingen die u aanbrengt op server niveau, zijn van toepassing op alle websites op de server.   
>     - Wijzigingen die u aanbrengt in de afzonderlijke websites gelden alleen voor die website.  
> 
> De beveiligings best practice is om Configuration Manager uit te voeren op een speciale webserver. Als u andere toepassingen op de webserver moet uitvoeren, gebruikt u een aangepaste website voor Configuration Manager. Zie [websites voor site systeem servers](websites-for-site-system-servers.md)voor meer informatie.  

## <a name="http-verbs"></a>HTTP-woorden
**Beheer punten:** Om ervoor te zorgen dat clients kunnen communiceren met een beheer punt, moet op de beheer punt server de volgende HTTP-termen worden toegestaan:  
- GET
- POST
- CCM_POST
- HEAD
- PROPFIND

**Distributie punten:** Distributie punten vereisen dat de volgende HTTP-termen worden toegestaan:
- GET
- HEAD
- PROPFIND

Zie [aanvraag filtering configureren in IIS](/previous-versions/orphan-topics/ws.11/hh831621(v=ws.11)#http-verbs)voor meer informatie.