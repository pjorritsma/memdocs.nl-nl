---
title: Locatie van de inhouds bron
titleSuffix: Configuration Manager
description: Meer informatie over de Configuration Manager instellingen waarmee clients inhoud kunnen vinden op een traag netwerk.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58138380263a7e7c3305ab2ad663a5246098b4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720238"
---
# <a name="content-source-location-scenarios-in-configuration-manager"></a>Scenario's voor de locatie van inhouds bronnen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voorafgaand aan versie 1610, Configuration Manager verschillende instellingen ondersteund die zijn gecombineerd om te definiëren hoe en waar clients inhoud vinden wanneer ze zich op een traag netwerk voordoen. De mogelijke combi Naties zijn van invloed op de inhouds locatie die clients gebruiken en of ze een terugval locatie kunnen gebruiken wanneer er geen voorkeurs bron voor inhoud beschikbaar is.  

> [!IMPORTANT]  
> **Als uw sites versie 1511, 1602 of 1606 uitvoeren**, is de informatie in dit onderwerp van toepassing op uw infra structuur. Zie ook [grens groepen voor versies 1511, 1602 en 1606](../../servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md) voor informatie die specifiek is voor grens groepen met deze versies van Configuration Manager.
>
> **Als op uw sites versie 1610 of hoger wordt uitgevoerd**, gebruikt u de informatie in [site grenzen en grens groepen definiëren voor Configuration Manager](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md) om inzicht te krijgen in hoe uw clients distributie punten vinden die beschik bare inhoud hebben.





**De volgende drie instellingen bepalen het gedrag wanneer clients inhoud opvragen:**

- **Terugval bron locatie voor inhoud toestaan** (ingeschakeld of niet ingeschakeld): dit is een optie die u kunt inschakelen op het tabblad **grens groepen** van een distributie punt. Hierdoor kan de client een distributie punt gebruiken dat is geconfigureerd als een terugval locatie wanneer inhoud niet beschikbaar is op een voorkeurs distributiepunt.  

  - **Implementatie gedrag voor netwerk verbindings snelheid**: elke implementatie is geconfigureerd met een van de volgende gedragingen voor gebruik wanneer de verbinding met het distributie punt traag is:  

    -   **Inhoud downloaden van het distributie punt en lokaal uitvoeren**  

    -   **Geen inhoud downloaden**: deze optie wordt alleen gebruikt wanneer een client een terugval locatie gebruikt om inhoud te verkrijgen.  

    De verbindings snelheid voor een distributie punt wordt geconfigureerd op het tabblad **verwijzingen** van een grens groep en is specifiek voor die grens groep.  

  - **Pakket distributie op aanvraag** (naar voorkeurs distributiepunten): dit is ingeschakeld wanneer u de optie de **inhoud voor dit pakket distribueren naar voorkeurs distributiepunten** selecteert op het tabblad distributie- **instellingen** van de eigenschappen van een pakket of toepassing. Wanneer deze optie is ingeschakeld, wordt Configuration Manager de inhoud automatisch gekopieerd naar een voorkeurs distributiepunt dat de inhoud nog niet heeft nadat een client die inhoud van dat distributie punt heeft aangevraagd.  


 **De volgende vereisten zijn van toepassing op alle scenario's:**


-   Inhoud is beschikbaar op een terugval distributiepunt  

-   Distributie punten zijn online en toegankelijk  


## <a name="scenario-1"></a>Scenario 1  
 Van toepassing wanneer de volgende configuraties bestaan:  

-   **Inhoud is beschikbaar op een voorkeurs distributiepunt**  

-   **Terugval toestaan**: niet ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: elke configuratie  


**Details:** (de configuratie voor pakket distributie op aanvraag is niet relevant in dit scenario.)  

1.  De client zendt een inhouds aanvraag naar het beheer punt.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten die de inhoud bevatten.  

3.  De-client downloadt de inhoud van een voorkeurs distributiepunt in de lijst.  

## <a name="scenario-2"></a>Scenario 2  
 De volgende configuraties bestaan:  

-   **Inhoud is beschikbaar op een voorkeurs distributiepunt**  

-   **Terugval toestaan**: ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: inhoud niet downloaden  


**Details:** (de configuratie voor pakket distributie op aanvraag is niet relevant in dit scenario.)  

1.  De client zendt een inhouds aanvraag naar het beheer punt. De client bevat een vlag met de aanvraag die aangeeft dat terugval distributie punten zijn toegestaan.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten en de terugval distributie punten die de inhoud bevatten.  

3.  De-client downloadt de inhoud van een voorkeurs distributiepunt in de lijst.  

## <a name="scenario-3"></a>Scenario 3  
 De volgende configuraties bestaan:  

-   **Inhoud is beschikbaar op een voorkeurs distributiepunt**  

-   **Terugval toestaan**: ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: inhoud downloaden en installeren  


**Details:** (de configuratie voor pakket distributie op aanvraag is niet relevant in dit scenario.)  

1.  De client zendt een inhouds aanvraag naar het beheer punt. De client bevat een vlag met de aanvraag die aangeeft dat terugval distributie punten zijn toegestaan.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten en de terugval distributie punten die de inhoud bevatten.  

3.  De-client downloadt de inhoud van een voorkeurs distributiepunt in de lijst.  

## <a name="scenario-4"></a>Scenario 4  
 De volgende configuraties bestaan:  

-   **Inhoud is niet beschikbaar op een voorkeurs distributiepunt**  

-   **De inhoud voor dit pakket distribueren naar voorkeurs distributiepunten** is niet ingeschakeld  

-   **Terugval toestaan**: niet ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: elke configuratie  


**Nadere**  

1.  De client zendt een inhouds aanvraag naar het beheer punt.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten die de inhoud hebben. Er zijn geen voorkeurs distributiepunten in de lijst.  

3.  De client mislukt met de inhoud van het bericht **is niet beschikbaar** en gaat in de modus voor opnieuw proberen. Elk uur wordt een nieuwe inhouds aanvraag gestart.  

## <a name="scenario-5"></a>Scenario 5  
 De volgende configuraties bestaan:  

-   **Inhoud is niet beschikbaar op een voorkeurs distributiepunt**  

-   **De inhoud voor dit pakket distribueren naar voorkeurs distributiepunten** is niet ingeschakeld  

-   **Terugval toestaan**: ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: inhoud niet downloaden  


**Nadere**  

1.  De client zendt een inhouds aanvraag naar het beheer punt. De client bevat een vlag met de aanvraag die aangeeft dat terugval distributie punten zijn toegestaan.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten en de terugval distributie punten die de inhoud bevatten. Er zijn geen voorkeurs distributiepunten met de inhoud, maar ten minste één terugval distributiepunt heeft de inhoud.  

3.  De inhoud wordt niet gedownload omdat de implementatie-eigenschap voor het gebruik van een terugval distributiepunt door de client wordt ingesteld op **inhoud niet downloaden** (die wordt gebruikt wanneer clients terugvallen om de inhoud op te halen). De client mislukt met de inhoud van het bericht **is niet beschikbaar** en gaat in de modus voor opnieuw proberen. De client maakt elk uur een nieuwe inhouds aanvraag.  

## <a name="scenario-6"></a>Scenario 6  
 De volgende configuraties bestaan:  

-   **Inhoud is niet beschikbaar op een voorkeurs distributiepunt**  

-   **De inhoud voor dit pakket distribueren naar voorkeurs distributiepunten** is niet ingeschakeld  

-   **Terugval toestaan**: ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: inhoud downloaden en installeren  


**Nadere**  

1.  De client zendt een inhouds aanvraag naar het beheer punt. De client bevat een vlag met de aanvraag die aangeeft dat terugval distributie punten zijn ingeschakeld.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten en de terugval distributie punten die de inhoud bevatten. Er zijn geen voorkeurs distributiepunten met de inhoud, maar ten minste één terugval distributiepunt met de inhoud.  

3.  De inhoud wordt gedownload van een terugval distributiepunt in de lijst omdat de implementatie-eigenschap voor het gebruik van een terugval distributiepunt door de client is ingesteld om **de inhoud te downloaden en te installeren**.  

## <a name="scenario-7"></a>Scenario 7  
 De volgende configuraties bestaan:  

-   **Inhoud is niet beschikbaar op een voorkeurs distributiepunt**  

-   **De inhoud voor dit pakket distribueren naar voorkeurs distributiepunten** is ingeschakeld  

-   **Terugval toestaan**: niet ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: elke configuratie  


**Nadere**  

1.  De client zendt een inhouds aanvraag naar het beheer punt.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten die de inhoud hebben. Er zijn geen voorkeurs distributiepunten die de inhoud hebben.  

3.  De client mislukt met de inhoud van het bericht **is niet beschikbaar** en gaat in de modus voor opnieuw proberen. Elk uur wordt een nieuwe inhouds aanvraag gemaakt.  

4.  Het beheer punt maakt een trigger voor Distribution Manager om de inhoud naar alle voorkeurs distributiepunten te distribueren voor de client die de inhouds aanvraag heeft ingediend.  

5.  Distribution Manager distribueert de inhoud naar alle voorkeurs distributiepunten. In de meeste gevallen wordt de inhoud binnen een uur gedistribueerd naar de voorkeurs distributiepunten.  

6.  Er wordt een nieuwe inhouds aanvraag geïnitieerd door de client naar het beheer punt.  

7.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten die de inhoud hebben. De-client downloadt de inhoud van een voorkeurs distributiepunt in de lijst.  

## <a name="scenario-8"></a>Scenario 8  
 De volgende configuraties bestaan:  

-   **Inhoud is niet beschikbaar op een voorkeurs distributiepunt**  

-   **De inhoud voor dit pakket distribueren naar voorkeurs distributiepunten** is ingeschakeld  

-   **Terugval toestaan**: ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: inhoud niet downloaden  


**Nadere**  

1.  De client zendt een inhouds aanvraag naar het beheer punt. De client bevat een vlag met de aanvraag die aangeeft dat terugval distributie punten zijn toegestaan.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten en de terugval distributie punten die de inhoud bevatten. Er zijn geen voorkeurs distributiepunten met de inhoud, maar ten minste één terugval distributiepunt heeft de inhoud.  

3.  De inhoud wordt niet gedownload omdat de implementatie-eigenschap voor het gebruik van een terugval distributiepunt door de client is ingesteld op **niet downloaden**. De client mislukt met de inhoud van het bericht **is niet beschikbaar** en gaat in de modus voor opnieuw proberen. De client maakt elk uur een nieuwe inhouds aanvraag.  

4.  Het beheer punt maakt een trigger voor Distribution Manager om de inhoud naar alle voorkeurs distributiepunten te distribueren voor de client die de inhouds aanvraag heeft ingediend.  

5.  Distribution Manager distribueert de inhoud naar alle voorkeurs distributiepunten. In de meeste gevallen wordt de inhoud binnen een uur gedistribueerd naar de voorkeurs distributiepunten.  

6.  Er wordt een nieuwe inhouds aanvraag geïnitieerd door de client naar het beheer punt.  

7.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten die de inhoud hebben.  

8.  De-client downloadt de inhoud van een voorkeurs distributiepunt in de lijst.  

## <a name="scenario-9"></a>Scenario 9  
 De volgende configuraties bestaan:  

-   **Inhoud is niet beschikbaar op een voorkeurs distributiepunt**  

-   **De inhoud voor dit pakket distribueren naar voorkeurs distributiepunten** is ingeschakeld  

-   **Terugval toestaan**: ingeschakeld  

-   **Implementatie gedrag voor een langzaam netwerk**: inhoud downloaden en installeren  


**Nadere**  

1.  De client zendt een inhouds aanvraag naar het beheer punt. De client bevat een vlag met de aanvraag die aangeeft dat terugval distributie punten zijn toegestaan.  

2.  Een inhouds locatie lijst wordt geretourneerd naar de client vanaf het beheer punt met de voorkeurs distributiepunten en de terugval distributie punten die de inhoud bevatten. Er zijn geen voorkeurs distributiepunten met de inhoud, maar ten minste één terugval distributiepunt heeft de inhoud.  

3.  De inhoud wordt gedownload van een terugval distributiepunt in de lijst omdat de implementatie-eigenschap voor het gebruik van een terugval distributiepunt door de client is ingesteld om **de inhoud te downloaden en te installeren**. Met deze implementatie-instelling kan een client die een terugval locatie voor inhoud moet gebruiken om de inhoud van die locatie op te halen.  

4.  Het beheer punt maakt een trigger voor Distribution Manager om de inhoud naar alle voorkeurs distributiepunten te distribueren voor de client die de inhouds aanvraag heeft ingediend.  

5.  Distribution Manager distribueert de inhoud naar alle voorkeurs distributiepunten, waardoor extra clients de inhoud kunnen verkrijgen zonder een terugval distributiepunt te gebruiken.  
