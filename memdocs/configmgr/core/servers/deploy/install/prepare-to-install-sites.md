---
title: De installatie van sites voorbereiden
titleSuffix: Configuration Manager
description: Als u van plan bent meerdere Configuration Manager-sites te installeren, kunt u deze informatie lezen om tijd te besparen en fouten te voor komen.
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718180"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Voorbereiden om Configuration Manager-sites te installeren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als voor bereiding op een geslaagde implementatie van een of meer Configuration Manager sites, kunt u vertrouwd raken met de informatie in dit artikel. Deze stappen kunnen u tijd besparen tijdens de installatie van meerdere sites en helpen bij het voor komen van niet-verwerkingen die ertoe kunnen leiden dat een of meer sites opnieuw moeten worden geïnstalleerd.

> [!TIP]
> Bij het beheren van Configuration Manager site-en hiërarchie-infra structuur, worden de voor waarden *bijgewerkt*, *bijgewerkt*en *installeren* gebruikt om drie afzonderlijke concepten te beschrijven. Zie voor meer informatie over het gebruik van elke term [over upgrade, update en installatie](../../../understand/upgrade-update-install.md).

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a>Opties voor het installeren van verschillende typen sites
Wanneer u een nieuwe Configuration Manager-site installeert, is de versie van de bron bestanden die u kunt gebruiken afhankelijk van de versie van de sites die zich al in de hiërarchie bevinden (indien van toepassing). De installatie methoden die u kunt gebruiken, zijn afhankelijk van het type site dat u wilt installeren.  

Voordat u een site installeert, moet u ervoor zorgen dat u uw hiërarchie hebt gepland en hebt u inzicht in het type site dat u wilt installeren. Zie [een hiërarchie van sites ontwerpen](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)voor meer informatie.


### <a name="first-site"></a>Eerste site
De eerste-site die u in een-hiërarchie installeert, is een zelfstandige primaire site of een centrale beheer site.

**Installatie media**: als u een centrale beheer site of een zelfstandige primaire site wilt installeren als de eerste site in een nieuwe hiërarchie, moet u [een basislijn versie](../../../../core/servers/manage/updates.md#bkmk_Baselines) van Configuration Manager gebruiken. Installeer de eerste site van een nieuwe hiërarchie niet met behulp van bijgewerkte bron bestanden van de [cd. De meest recente map](../../../../core/servers/manage/the-cd.latest-folder.md) van een site.

**Installatie methode**: u kunt een van beide typen sites installeren met behulp van de [installatie wizard van Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md), of u kunt een script configureren voor gebruik met een [script opdracht regel installatie](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Aanvullende sites
Nadat de eerste site is geïnstalleerd, kunt u op elk gewenst moment meer sites toevoegen. U hebt de volgende opties voor het toevoegen van sites (Maxi maal [ondersteunde limieten](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Site die u hebt|Aanvullend site type dat u kunt installeren|
|---|---|
|Centrale beheersite|Onderliggende primaire site|
|Onderliggende primaire site|Secundaire site|
|Zelfstandige primaire site|Secundaire site (u kunt de primaire site uitbreiden, waarmee de zelfstandige primaire site naar een onderliggende primaire site wordt geconverteerd)|

**Installatie media**: wanneer u een centrale beheer site installeert om een zelfstandige primaire site uit te breiden of als u een nieuwe onderliggende primaire site installeert in een bestaande hiërarchie, moet u installatie media (die bron bestanden bevatten) gebruiken die overeenkomen met de versie van de bestaande site of sites.

> [!IMPORTANT]
> Als u updates in de console hebt geïnstalleerd waarmee de versie van eerder geïnstalleerde sites is gewijzigd, moet u de oorspronkelijke installatie media niet gebruiken. Gebruik in dat geval bron bestanden van de [cd. Meest recente map](../../../../core/servers/manage/the-cd.latest-folder.md) van een bijgewerkte site. Configuration Manager moet u bron bestanden gebruiken die overeenkomen met de versie van de bestaande site waarmee de nieuwe site verbinding maakt.

Een secundaire site moet worden geïnstalleerd vanuit de Configuration Manager-console. Op deze manier worden secundaire sites altijd geïnstalleerd met behulp van bron bestanden van de bovenliggende primaire site.

**Installatie methode**: de methode die u gebruikt voor het installeren van extra sites is afhankelijk van het type site dat u wilt installeren.
- **Een centrale beheer site toevoegen**: u kunt de Configuration Manager installatie wizard of een script opdracht regel gebruiken om de nieuwe centrale beheer site als een bovenliggende site te installeren op uw bestaande zelfstandige primaire site. Zie [een zelfstandige primaire site uitbreiden](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand)voor meer informatie.
- **Een onderliggende primaire site toevoegen**: u kunt de wizard Configuration Manager installatie of een opdracht regel installatie gebruiken om een onderliggende primaire site onder een centrale beheer site toe te voegen.
- **Een secundaire site toevoegen**: gebruik de Configuration Manager-console om een secundaire site te installeren als een onderliggende site onder een primaire site. Andere methoden worden niet ondersteund voor het toevoegen van secundaire sites.

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a>Algemene taken die moeten worden voltooid voordat een installatie wordt gestart
- **Inzicht in de hiërarchie topologie die u voor uw implementatie wilt gebruiken**    
Zie [ontwerp een hiërarchie van sites voor Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)voor meer informatie.  

- **Afzonderlijke servers voorbereiden en configureren om te voldoen aan vereisten en ondersteunde configuraties voor gebruik met Configuration Manager**         
Zie voor meer informatie [Site and site system prerequisites](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Vereisten voor sites en sitesystemen).  

- **SQL Server installeren en configureren voor het hosten van de site database**     
Zie [ondersteuning voor SQL Server-versies voor Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md)voor meer informatie.  

- **Bereid uw netwerk omgeving voor op de ondersteuning van Configuration Manager**      
Zie [firewalls, poorten en domeinen configureren om Configuration Manager voor te bereiden](../../../../core/plan-design/network/configure-firewalls-ports-domains.md)voor meer informatie.  

- **Als u een open bare-sleutel infrastructuur (PKI) wilt gebruiken, moet u uw infra structuur en certificaten voorbereiden**      
Zie [PKI-certificaat vereisten voor Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md)voor meer informatie.

- **Installeer de meest recente beveiligings updates op de computers die u wilt gebruiken als site servers of site systeem servers, en start deze indien nodig opnieuw**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a>Site namen en site codes
Site codes en site namen worden gebruikt om de sites in een Configuration Manager hiërarchie te identificeren en te beheren. In de Configuration Manager-console worden de site code en site naam weer gegeven in &lt;de site *code*\> - &lt;-site*naam* \> indeling. Elke site code die u in uw hiërarchie gebruikt, moet uniek zijn. Als het Active Directory schema wordt uitgebreid voor Configuration Manager en uw sites gegevens publiceren, moeten de site codes die in een Active Directory forest worden gebruikt, uniek zijn, zelfs als ze worden gebruikt in een andere Configuration Manager-hiërarchie of als ze in eerdere Configuration Manager-installaties zijn gebruikt. Zorg ervoor dat u uw site codes en site namen zorgvuldig plant voordat u uw-hiërarchie implementeert.

### <a name="specify-a-site-code-and-site-name"></a>Geef een site code en site naam op
Wanneer u Configuration Manager Setup uitvoert, wordt u gevraagd om een site code en site naam voor de centrale beheer site en voor elke primaire site en installatie van de secundaire site. Een site code moet een unieke identificatie vormen van elke site in de hiërarchie. Omdat de site code in mapnamen wordt gebruikt, moet u nooit de volgende namen voor de site code gebruiken. Dit zijn onder andere de namen die zijn gereserveerd voor Configuration Manager en Windows:
- AUX
- CON
- NUL
- PRN
- Sms
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Configuration Manager-installatie controleert niet of een site code niet al in gebruik is.

Als u de site code voor een site wilt invoeren wanneer u Configuration Manager Setup uitvoert, moet u drie alfanumerieke tekens invoeren. Alleen de letters *A* t/m *Z* en de cijfers *0* t/m *9*, in een wille keurige combi natie, zijn toegestaan in site codes. De reeks letters of cijfers heeft geen invloed op de communicatie tussen sites. Het is bijvoorbeeld niet nodig om een primaire site *ABC* en een *definitie*van een secundaire site te noemen.

De site naam is een beschrijvende naam-id voor de site. U kunt alleen de tekens *a* tot en met *z*, *A* tot en met *z*, *0* t/m *9*en het koppel teken (*-*) in site namen gebruiken.

> [!IMPORTANT]
> Het wijzigen van de site code of site naam na de installatie van de site wordt niet ondersteund.

### <a name="reuse-a-site-code"></a>Een site code opnieuw gebruiken
Site codes kunnen niet meer dan één keer worden gebruikt in een Configuration Manager-hiërarchie voor een centrale beheer site of voor een primaire site, zelfs als de oorspronkelijke site en site code zijn verwijderd. Als u een site code hergebruikt, is het risico dat de object-id's in uw hiërarchie conflicteren. U kunt de site code voor een secundaire site hergebruiken als die secundaire site en de site code niet meer worden gebruikt in uw Configuration Manager-hiërarchie of in het Active Directory-forest.

## <a name="limits-and-restrictions-for-installed-sites"></a>Limieten en beperkingen voor geïnstalleerde sites
Voordat u een site installeert, is het belang rijk om inzicht te krijgen in de volgende beperkingen die van toepassing zijn op sites en site hiërarchieën:
- Na het uitvoeren van de installatie kunt u de volgende site-eigenschappen niet wijzigen zonder de site te verwijderen en vervolgens opnieuw te installeren met behulp van de nieuwe waarden:  
  - Installatiemap van programma bestanden  
  - Site code  
  - Site beschrijving  
- Wanneer uw hiërarchie een centrale beheer site bevat:  
  - Configuration Manager biedt geen ondersteuning voor het verplaatsen van een onderliggende primaire site uit een hiërarchie om een zelfstandige primaire site te maken of om deze aan een andere hiërarchie te koppelen. Verwijder in plaats daarvan de onderliggende primaire site en installeer deze opnieuw als een nieuwe zelfstandige primaire site of als onderliggende site van de centrale beheer site van een andere hiërarchie.  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a>Optionele stappen voorafgaand aan het uitvoeren van Setup
**Het [Download programma](../../../../core/servers/deploy/install/setup-downloader.md) hand matig uitvoeren**

Als u de bijgewerkte installatie bestanden voor Configuration Manager wilt downloaden, kunt u het download programma voor de installatie uitvoeren. Als de computer waarop u Setup wilt uitvoeren, niet is verbonden met internet of als u van plan bent meerdere site servers te installeren, kunt u het download programma voor de installatie gebruiken om de vereiste updates te downloaden. Hier volgt aanvullende informatie:
- Setup maakt standaard verbinding met internet om bijgewerkte Setup-bestanden te downloaden.
- Standaard worden de bestanden opgeslagen in de map Redist.
- U kunt Setup naar een locatie in het netwerk sturen waar u eerder een kopie van deze bestanden hebt opgeslagen.

**[Prerequisite Checker](../../../../core/servers/deploy/install/prerequisite-checker.md) hand matig uitvoeren**

Als u problemen wilt identificeren en oplossen voordat u Setup uitvoert om een site te installeren en voordat u een site systeemrol op een server installeert, kunt u prerequisite Checker uitvoeren. Prerequisite Checker helpt ervoor te zorgen dat de computer voldoet aan de vereisten voor het hosten van de site of site systeemrol. Hier volgt aanvullende informatie:
- De prerequisite checker wordt standaard gecontroleerd.
- Als er fouten zijn, wordt Setup gestopt totdat het probleem is opgelost.

**Optionele poorten identificeren**

U kunt optionele poorten identificeren voor het gebruik van site systemen en clients. Hier volgt aanvullende informatie:
- Site systemen en-clients gebruiken standaard vooraf gedefinieerde poorten om te communiceren.
- Tijdens de installatie kunt u alternatieve poorten configureren.

Zie [poorten die worden gebruikt](../../../../core/plan-design/hierarchy/ports.md)voor meer informatie.
