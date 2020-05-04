---
title: Upgrade uitvoeren voor Windows 10
titleSuffix: Configuration Manager
description: Apparaten upgraden naar Windows 10 versie 1709 of hoger, wat vereist is voor co-beheer
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e11a6130fb9f7d86b7d3377cc4120d4e61c43d2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711460"
---
# <a name="upgrade-windows-10-for-co-management"></a>Windows 10 bijwerken voor co-beheer

Wanneer u uw organisatie naar co-beheer voorbereidt, is de actuele hindernis voor sommige klanten aanzienlijk. Voor co-beheer is [Windows 10 versie 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) of hoger vereist. Nadat u Windows hebt bijgewerkt en automatische inschrijving hebt geconfigureerd, worden uw-clients automatisch Inge schreven voor co-beheer.

In de volgende video is Senior Program Manager Rob York en de vergren deling van productmarketing Manager Locky Ainley bespreken en de demo voor het uitvoeren van een upgrade naar Windows 10 voor co-beheer:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Waarom bijwerken?

Onder andere platform voorschotten biedt Windows 10 versie 1709 en hoger ondersteuning voor automatische inschrijving. Dit gedrag zorgt ervoor dat een apparaat automatisch wordt Inge schreven bij intune wanneer het is toegevoegd Azure Active Directory (Azure AD). 

Zie [automatische inschrijving voor Windows 10 inschakelen](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)voor meer informatie.


## <a name="how-to-do-it"></a>Hoe u dit doet

Hier volgen enkele tips die zijn geleerd van het helpen van duizenden klanten om snel aan de slag te gaan:

- Gebruik gefaseerde implementaties voor het implementeren van deze upgrade naar de juiste personen op het juiste moment. Zie voor meer informatie [gefaseerde implementaties maken](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).  

- Gebruik vooraf-cache om de wacht tijden van gebruikers te verminderen. Zie [inhoud vooraf in cache configureren](../osd/deploy-use/configure-precache-content.md)voor meer informatie.  

- Gebruik de standaard in-place upgrade taken reeks sjabloon. Configureer vervolgens de stappen voor vóór en na de upgrade, en eventuele fout acties. Zie [Aanbevolen taken reeks stappen voor naverwerking](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing)voor meer informatie.  

- Als uw omgeving zeer mobiele mede werkers heeft, ondersteunt Configuration Manager in-place upgrade via de Cloud Management Gateway (CMG). Met deze functie kunt u een upgrade uitvoeren van uw Windows 10-clients wanneer deze op internet zijn gebaseerd. Zie [Deploying Windows 10 in-place upgrade via CMG](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg)voor meer informatie over de CMG.  

- Bied een opt-in voor het co-beheer van gebruikers die vroege klanten willen zijn. Deze aanpak versnelt de eerste acceptatie. Door deze gebruikers vooraf te identificeren, kunt u in de vroege dagen van een implementatie zorgen voor een goede dekking. U ontvangt ook validatie en feedback van gebruikers die blij zijn om te worden gewijzigd en die geïnteresseerd zijn in meer frequente releases. Vroege toepasser-Program ma's genereren belang rijke in de nieuwe technologieën en verg Roten de omvang van de tijd.  


## <a name="case-studies"></a>Casestudy's

Micro soft IT heeft Windows 10 geïmplementeerd op 96.000 gedistribueerde gebruikers van micro soft. De implementatie omvat zowel externe gebruikers als gebruikers in het bedrijfs netwerk. De implementatie is in negen weken voltooid. Zie [Deploying Windows 10 at micro soft as a in-place upgrade](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade)(Engelstalig) voor meer informatie over hun ervaring.  

Een grote Europese software fabrikant gebruikt een early adopter groep. Na de eerste test-en test groepen ontvangen ongeveer 2.000 werk nemers de eerste update, upgrades en software. Deze groep bevat IT-mede werkers en opt-in vrijwilligers. Dit niveau van betrokkenheid bij hun gebruikers geeft hen een grotere mate van vertrouwen bij het testen en meer geloofwaardigheid bij het starten van massale implementaties.



## <a name="contact-fasttrack"></a>Contact opnemen met FastTrack

Als u hulp nodig hebt bij uw Windows 10-upgrade op elk gewenst moment in het proces, gaat u naar [Microsoft FastTrack](https://Microsoft.com/FastTrack/), meldt u zich aan en vraagt u om hulp. 

Zie voor meer informatie [hulp vragen van FastTrack](quickstart-fasttrack.md). 

