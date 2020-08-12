---
title: Websites voor site systemen
titleSuffix: Configuration Manager
description: Meer informatie over standaard-en aangepaste websites voor site systeem servers in Configuration Manager.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8091ecf4abc113d41f053c1152152262131a4bb
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146079"
---
# <a name="websites-for-site-system-servers-in-configuration-manager"></a>Websites voor site systeem servers in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Verschillende Configuration Manager site systeem rollen vereisen het gebruik van micro soft Internet Information Services (IIS) en gebruiken de standaard IIS-website om site systeem services te hosten. Wanneer u andere webtoepassingen moet uitvoeren op dezelfde server en de instellingen niet compatibel zijn met Configuration Manager, kunt u een aangepaste website gebruiken voor Configuration Manager.  

> [!TIP]  
>  Een beveiligings best practice is het reserveren van een server voor de Configuration Manager-site systemen waarvoor IIS is vereist. Wanneer u andere toepassingen uitvoert op een Configuration Manager site systeem, verhoogt u de kwets baarheid van de computer.  




##  <a name="what-to-know-before-choosing-to-use-custom-websites"></a><a name="BKMK_What2Know"></a> Wat u moet weten voordat u aangepaste websites gaat gebruiken  
 Sitesysteemrollen gebruiken standaard de **standaardwebsite** in IIS. Dit wordt automatisch ingesteld wanneer de site systeemrol wordt geïnstalleerd. Op primaire sites kunt u in plaats daarvan echter kiezen voor het gebruik van aangepaste websites. Wanneer u aangepaste websites gebruikt, geldt het volgende:  

-   Aangepaste websites zijn ingeschakeld voor de hele site in plaats van voor afzonderlijke site systeem servers of-rollen.  

-   Op primaire sites moet elke computer die als host fungeert voor een site systeemrol, worden ingesteld met een aangepaste website met de naam **SMSWEB**. Clients kunnen mogelijk niet communiceren met site systeem rollen op die computer totdat u deze website maakt en site systeem rollen op die computer instelt voor het gebruik van de aangepaste website.  

-   Omdat secundaire sites automatisch worden ingesteld voor het gebruik van een aangepaste website wanneer de primaire bovenliggende site hiervoor is ingesteld, moet u ook aangepaste websites in IIS maken op elke secundaire site systeem server waarvoor IIS vereist is.  


  **Vereisten voor het gebruik van aangepaste websites:**  

 Voordat u de optie voor gebruik van aangepaste websites op een site inschakelt, moet u het volgende doen:  

-   Maak een aangepaste website met de naam **SMSWEB** in IIS op elke sitesysteemserver waarvoor IIS is vereist. Doe dat op de primaire site en op alle onderliggende secundaire sites.  

-   Stel de aangepaste website zo in dat deze reageert op dezelfde poort die u hebt ingesteld voor Configuration Manager client communicatie (poort voor client aanvragen).  

-   Plaats voor elke aangepaste of standaard website die gebruikmaakt van een aangepaste map, een kopie van het standaard document type dat u gebruikt in de hoofdmap waarin de website wordt gehost. Een voor beeld: op een Windows Server 2008 R2-computer met standaard configuraties is **iisstart.htm** een van de volgende beschik bare standaard document typen. U vindt dit bestand in de hoofdmap van de standaard website en plaatst vervolgens een kopie van dit bestand (of een kopie van het standaard document type dat u gebruikt) in de hoofdmap die als host fungeert voor de aangepaste SMSWEB-website. Zie [Standaard document &lt; DEFAULTDOCUMENT \> voor IIS](https://www.iis.net/configreference/system.webserver/defaultdocument)voor meer informatie over standaard document typen.  

**Over IIS-vereisten:** 
 **Voor de volgende site systeem rollen zijn IIS en een website vereist om de site systeem services te hosten:**  

-   Application Catalog-webservicepunt  

-   Application Catalog-websitepunt  

-   Distributiepunt  

-   Inschrijvingspunt  

-   Proxypunt voor inschrijving  

-   Terugvalstatuspunt  

-   Beheerpunt  

-   Software-updatepunt  

-   Statusmigratiepunt  

Aanvullende overwegingen:  

-   Wanneer op een primaire site aangepaste websites zijn ingeschakeld, worden clients die aan die site zijn toegewezen, omgeleid om te communiceren met de aangepaste websites in plaats van de standaard websites op de betreffende site systeem servers  

-   Als u aangepaste websites gebruikt voor één primaire site, kunt u overwegen om aangepaste websites te gebruiken voor alle primaire sites in uw hiërarchie om ervoor te zorgen dat clients kunnen zwerven binnen de hiërarchie. (Bij roaming wordt een clientcomputer verplaatst naar een nieuw netwerksegment dat wordt beheerd door een andere site. Roaming kan invloed hebben op bronnen waartoe een client lokaal toegang heeft in plaats van via een WAN-koppeling).  

-   Site systeem rollen die gebruikmaken van IIS, maar geen client verbindingen accepteren, zoals het Reporting Services-punt, gebruiken ook de SMSWEB-website in plaats van de standaard website.  

-   Voor aangepaste websites moet u poort nummers toewijzen die afwijken van de poorten die door de standaard website van de computer worden gebruikt. Een standaardwebsite en een aangepaste website kunnen niet tegelijkertijd worden uitgevoerd als beide sites proberen dezelfde TCP/IP-poorten te gebruiken.  

-   De TCP/IP-poorten die u in IIS voor de aangepaste website instelt, moeten overeenkomen met de client aanvraag poorten voor de site.  

## <a name="switch-between-default-and-custom-websites"></a>Scha kelen tussen standaard-en aangepaste websites  
Hoewel u het selectie vakje voor het gebruik van aangepaste websites op een primaire site op elk gewenst moment kunt in-of uitschakelen (het vak bevindt zich op het tabblad poorten van de eigenschappen van de site), moet u zorgvuldig plannen voordat u deze wijziging aanbrengt. Wanneer deze configuratie wordt gewijzigd, moeten alle toepasselijke site systeem rollen op de primaire site en de onderliggende secundaire sites worden verwijderd en opnieuw worden geïnstalleerd:  

De volgende rollen **worden automatisch opnieuw geïnstalleerd**:  

-   Beheerpunt  

-   Distributiepunt  

-   Software-updatepunt  

-   Terugvalstatuspunt  

-   Statusmigratiepunt  

De volgende rollen moeten **handmatig opnieuw worden geïnstalleerd**:  

-   Application Catalog-webservicepunt  

-   Application Catalog-websitepunt  

-   Inschrijvingspunt  

-   Proxypunt voor inschrijving  

Aanvullend:  

-   Wanneer u overschakelt van de standaard website naar een aangepaste website, Configuration Manager verwijdert de oude virtuele mappen niet. Als u de bestanden die Configuration Manager gebruikt, wilt verwijderen, moet u de virtuele mappen die zijn gemaakt op de standaard website hand matig verwijderen.  

-   Als u de site voor het gebruik van aangepaste websites wijzigt, moeten de clients die al aan de site zijn toegewezen, vervolgens opnieuw worden geconfigureerd om de nieuwe client aanvragen voor de aangepaste websites te gebruiken. Zie [client communicatie poorten configureren](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Aangepaste websites instellen  
De stappen voor het maken van een aangepaste website verschillen per besturingssysteem. Raadpleeg voor de exacte stappen de documentatie voor de besturingssysteemversie, maar gebruik de volgende informatie wanneer dit van toepassing is:  

-   De naam van de website moet zijn: **SMSWEB**.  

-   Wanneer u HTTPS hebt ingesteld, moet u een SSL-certificaat opgeven voordat u de configuratie kunt opslaan.  

-   Nadat u de aangepaste website hebt gemaakt, verwijdert u de aangepaste website poorten die u gebruikt van andere websites in IIS:  

    1.  Bewerk de **bindingen** van de andere websites om poorten te verwijderen die overeenkomen met de verbindingen die zijn toegewezen aan de **SMSWEB** -website.  

    2.  Start de **SMSWEB** -website.  

    3.  Start de service **SMS_SITE_COMPONENT_MANAGER** op de siteserver van de site opnieuw op.  
