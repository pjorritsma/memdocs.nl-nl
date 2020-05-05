---
title: De grondbeginselen van sites en hiërarchieën
titleSuffix: Configuration Manager
description: Algemene informatie over Configuration Manager-sites en-hiërarchieën ophalen.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed22436d750572fed8ce898c5ed3a23b71f239
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722814"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-configuration-manager"></a>De grond beginselen van sites en hiërarchieën voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Een Configuration Manager implementatie moet in een Active Directory domein worden geïnstalleerd. De basis van deze implementatie bevat een of meer Configuration Manager sites die een site hiërarchie vormen. Voor een hiërarchie die uit een enkele site bestaat en voor een hiërarchie die uit meerdere sites bestaat, geldt dat het type en de locatie van sites die u installeert, u de mogelijkheid bieden om uw implementatie indien nodig omhoog te schalen (uit te breiden) en om belangrijke services te leveren aan beheerde gebruikers en apparaten.

## <a name="hierarchies-of-sites"></a>Sitehiërarchieën
Wanneer u Configuration Manager voor de eerste keer installeert, bepaalt de eerste Configuration Manager-site die u installeert, het bereik van uw hiërarchie. De eerste Configuration Manager site is de basis van waaruit u apparaten en gebruikers in uw onderneming gaat beheren. Deze eerste site moet een centrale beheer site of een zelfstandige primaire site zijn.  

 Een *centrale beheer site* is geschikt voor grootschalige implementaties en biedt een centraal punt van beheer en biedt de flexibiliteit om apparaten te ondersteunen die worden gedistribueerd via een globale netwerk infrastructuur. Nadat u een centrale beheer site hebt geïnstalleerd, moet u een of meer primaire sites installeren als onderliggende sites. Deze configuratie is nood zakelijk omdat een centrale beheer site het beheer van apparaten niet rechtstreeks ondersteunt. Dit is de functie van een primaire site. Een centrale beheer site ondersteunt meerdere onderliggende primaire sites. De onderliggende primaire sites worden gebruikt voor het direct beheren van apparaten, en voor het beheren van de netwerk bandbreedte wanneer de beheerde apparaten zich op verschillende geografische locaties bevinden.  

 Een *zelfstandige primaire site* is geschikt voor kleinere implementaties en kan worden gebruikt voor het beheren van apparaten zonder dat hiervoor extra sites hoeven te worden geïnstalleerd. Hoewel een zelfstandige primaire site de omvang van uw implementatie kan beperken, wordt een scenario ondersteund om uw hiërarchie op een later tijdstip uit te breiden door een nieuwe centrale beheer site te installeren. Met dit scenario voor site-uitbrei ding wordt uw zelfstandige primaire site een onderliggende primaire site en kunt u extra onderliggende primaire sites onder de nieuwe centrale beheer site installeren. U kunt de eerste implementatie uitbreiden voor toekomstige groei van uw onderneming.  

> [!TIP]  
>  Een zelfstandige primaire site en een onderliggende primaire site zijn in feite hetzelfde type site: een primaire site. Het naamsverschil is gebaseerd op de hiërarchische relatie die wordt gemaakt wanneer u ook een centrale beheersite gebruikt. Deze hiërarchie relatie kan ook de installatie van bepaalde site systeem rollen beperken die Configuration Manager-functionaliteit uitbreiden. Deze beperking van rollen treedt op omdat bepaalde site systeem rollen alleen kunnen worden geïnstalleerd op de site op het hoogste niveau van de hiërarchie, een centrale beheer site of een zelfstandige primaire site.  

 Nadat u uw eerste site hebt geïnstalleerd, kunt u aanvullende sites installeren. Als uw eerste site een centrale beheer site was, kunt u een of meer onderliggende primaire sites installeren. Nadat u een primaire site (zelfstandig of onderliggend-primair) hebt geïnstalleerd, kunt u vervolgens een of meer secundaire sites installeren.  

 Een *secundaire site* kan alleen worden geïnstalleerd als een onderliggende site onder een primaire site. Dit type site kan het bereik van een primaire site uitbreiden voor het beheer van apparaten op locaties die een trage netwerkverbinding hebben met de primaire site. Hoewel een secundaire site de primaire site uitbreidt, beheert de primaire site alle clients. De secundaire site biedt ondersteuning voor apparaten op de externe locatie. Het biedt ondersteuning voor het comprimeren en beheren van de overdracht van gegevens in uw netwerk die u verzendt (implementeert) naar clients en die clients terugsturen naar de site.  

 De volgende diagrammen geven voorbeelden van siteontwerpen weer.  

 ![Voor beelden van hiërarchieën](media/Hierarchy_examples.png)  

 Zie de volgende onderwerpen voor meer informatie:  

-   [Inleiding tot Configuration Manager](../../core/understand/introduction.md)  

-   [Een hiërarchie van sites ontwerpen voor Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Configuration Manager-sites installeren](../servers/deploy/install/installing-sites.md)  

## <a name="site-system-servers-and-site-system-roles"></a>Sitesysteemservers en sitesysteemrollen  
 Elke Configuration Manager-site installeert *site systeem rollen* die beheer bewerkingen ondersteunen. De volgende rollen worden standaard geïnstalleerd wanneer u een-site installeert:

-   De site serverrol wordt toegewezen aan de computer waarop u de site installeert.

-   De server functie site database is toegewezen aan de SQL Server die als host fungeert voor de site database.

Andere site systeem rollen zijn optioneel en worden alleen gebruikt wanneer u de functionaliteit wilt gebruiken die actief is in een site systeemrol. Elke computer die als host fungeert voor een sitesysteemrol wordt een sitesysteemserver genoemd.  

 Voor een kleinere implementatie van Configuration Manager kunt u eerst al uw site systeem rollen rechtstreeks op de site Server computer uitvoeren. Als uw beheerde omgeving en behoeften groeien, kunt u extra site systeem servers installeren om extra site systeem rollen te hosten om de efficiëntie van de site te verbeteren bij het leveren van services aan meer apparaten.  

 Zie [site systeem rollen](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) in [plan voor site systeem servers en site systeem rollen voor Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)voor meer informatie over de verschillende site systeem rollen.

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Sitegegevens publiceren naar Active Directory Domain Services  
 Als u het beheer van Configuration Manager wilt vereenvoudigen, kunt u het Active Directory-schema uitbreiden voor de ondersteuning van gegevens die worden gebruikt door Configuration Manager en dat de sites hun sleutel gegevens vervolgens naar Active Directory Domain Services (AD DS) publiceren. De computers die u wilt beheren, kunnen veilig site-gerelateerde gegevens ophalen van de vertrouwde bron van AD DS. De informatie die clients kunnen ophalen identificeert de beschikbare sites, sitesysteemservers en services die deze sitesysteemservers bieden.  

 *Uitbrei ding van het Active Directory schema* wordt slechts één keer uitgevoerd voor elk forest en kan worden uitgevoerd vóór of na de installatie van Configuration Manager.   Wanneer u het schema uitbreidt, moet u een nieuwe Active Directory container met de naam System Management maken in elk domein. De container bevat een Configuration Manager-site die gegevens publiceert zodat clients deze kunnen vinden. Zie [Active Directory voorbereiden voor het publiceren van sites](../../core/plan-design/network/extend-the-active-directory-schema.md)voor meer informatie.  

 Het *publiceren van site gegevens* verbetert de beveiliging van uw Configuration Manager-hiërarchie en vermindert de administratieve overhead, maar is niet vereist voor de basis functionaliteit van Configuration Manager.  
