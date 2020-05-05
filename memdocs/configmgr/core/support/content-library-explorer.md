---
title: Verkenner van inhoudsbibliotheek
titleSuffix: Configuration Manager
description: Met de inhouds bibliotheek Verkenner kunt u de inhouds bibliotheek op een Configuration Manager distributie punt bekijken en problemen oplossen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aa92fb143815faf693f6c2629c3f6436546c5080
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078529"
---
# <a name="content-library-explorer"></a>Verkenner van inhoudsbibliotheek

*Van toepassing op: Configuration Manager (huidige vertakking)*

Inhouds bibliotheek Verkenner is een van de [Configuration Manager-hulpprogram ma's](tools.md). Gebruik het hulp programma voor de volgende activiteiten:  

- De inhouds bibliotheek op een specifiek distributie punt verkennen  

- Problemen met de inhouds bibliotheek oplossen  

- Pakketten, inhoud, mappen en bestanden uit de inhouds bibliotheek kopiëren  

- Pakketten opnieuw distribueren naar het distributie punt  

- Pakketten op externe distributie punten valideren  



## <a name="requirements"></a>Vereisten

- Voer het hulp programma uit met behulp van een account met beheerders toegang tot:  

    - Het doel distributiepunt  

    - De WMI-provider op de site server  

    - De Configuration Manager provider  

- Alleen de rollen **volledige beheerder** en **alleen-lezen analist** hebben voldoende rechten om alle informatie van dit hulp programma weer te geven.  

    - Andere rollen, zoals **toepassings beheerder**, kunnen gedeeltelijke gegevens weer geven. Zie [Uitgeschakelde pakketten](#bkmk_disabled-packages)voor meer informatie.  

    - De **alleen-lezen analist** kan pakketten van dit hulp programma niet opnieuw distribueren.  

- Voer het hulp programma uit vanaf elke computer, zolang er verbinding mee kan worden gemaakt:  

    - Het doel distributiepunt  

    - De primaire site server  

    - De Configuration Manager provider  

- Als het distributie punt zich op de site server bevindt, is het nog steeds nodig om beheerders toegang te hebben tot de site server.  



## <a name="usage"></a>Gebruik 

Wanneer u **ContentLibraryExplorer. exe**start, voert u de Fully QUALIFIED domain name (FQDN) van het doel distributiepunt in. Vervolgens wordt er verbinding gemaakt met het distributie punt. Als het distributie punt deel uitmaakt van een secundaire site, wordt u gevraagd om de FQDN van de primaire site server en de code van de primaire site.

Bekijk in het linkerdeel venster de pakketten die worden gedistribueerd naar dit distributie punt. Vouw de pakketten uit en verken de mapstructuur. Deze structuur komt overeen met de mappen structuur van waaruit u het pakket hebt gemaakt.

Wanneer u een map selecteert, wordt deze weer gegeven in het rechterdeel venster van alle bestanden in de map. Deze weer gave bevat de volgende informatie: 
- Bestandsnaam
- Bestandsgrootte
- Welk station is ingeschakeld
- Andere pakketten die gebruikmaken van hetzelfde bestand op het station
- Wanneer het bestand voor het laatst is gewijzigd op het distributie punt

Het hulp programma maakt ook verbinding met de Configuration Manager-provider. Deze verbinding is om te bepalen welke pakketten naar het distributie punt worden gedistribueerd en of ze daad werkelijk zijn opgenomen in de inhouds bibliotheek van het distributie punt. Het is bijvoorbeeld mogelijk dat de distributie van een pakket dat in behandeling is, nog niet aanwezig is in de inhouds bibliotheek. Een dergelijk pakket wordt weer gegeven als ' in behandeling ' in het hulp programma en er zijn geen acties ingeschakeld voor dit pakket.


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a>Uitgeschakelde pakketten

Sommige pakketten zijn aanwezig op het distributie punt, maar zijn niet zichtbaar in de Configuration Manager-console. Deze pakketten zijn gemarkeerd met een asterisk (\*). Er kunnen geen acties worden uitgevoerd op deze pakketten. Andere pakketten kunnen ook worden gemarkeerd met een sterretje en acties zijn uitgeschakeld. 

Er zijn drie belang rijke redenen voor uitgeschakelde pakketten:  

- Het pakket is de Configuration Manager client upgrade. Dit pakket bevat ' ccmsetup. exe '.  

- Uw gebruikers account heeft geen toegang tot het pakket, waarschijnlijk vanwege op rollen gebaseerd beheer. De rol van de **Auteur** van de toepassing kan bijvoorbeeld geen stuur programmapakketten zien in de-console, zodat Stuur programmapakketten op het distributie punt zijn gemarkeerd als uitgeschakeld.  

- Het pakket is zwevend op het distributie punt.  


### <a name="validate-packages"></a>Pakketten valideren

Pakketten valideren met behulp van **package** > **Validate** op de werk balk. Selecteer eerst een pakket knooppunt in het linkerdeel venster om geen inhoud of map te selecteren. Het hulp programma maakt verbinding met de WMI-provider op het distributie punt voor deze actie. Wanneer het hulp programma wordt gestart, worden pakketten waarvoor een of meer inhoud ontbreekt, als ongeldig gemarkeerd. Als u het pakket valideert, wordt de inhoud niet meer gevonden. Als alle inhoud aanwezig is, maar de gegevens beschadigd zijn, detecteert validatie de beschadiging.


### <a name="redistribute-packages"></a>Pakketten opnieuw distribueren

Pakketten opnieuw distribueren met **package** > **redistribute** op de werk balk. Selecteer eerst een pakket knooppunt in het linkerdeel venster. Deze actie vereist machtigingen voor het opnieuw distribueren van pakketten.


### <a name="other-actions"></a>Overige acties

Gebruik **Edit** > **copy** om pakketten, inhoud, mappen en bestanden uit de inhouds bibliotheek naar een opgegeven map te kopiëren. U kunt de inhouds bibliotheek zelf niet kopiëren. Selecteer meer dan één bestand, maar u kunt niet meerdere mappen selecteren.

Pakketten zoeken met behulp van **Edit** > -**package**. Met deze actie wordt gezocht naar uw query in de pakket naam en pakket-ID.



## <a name="limitations"></a>Beperkingen

- Het hulp programma kan de inhouds bibliotheek niet rechtstreeks op enigerlei wijze bewerken. Wijzigingen in de inhouds bibliotheek kunnen leiden tot storingen.  

- Het hulp programma kan pakketten opnieuw distribueren, maar alleen naar het doel distributiepunt.  

- Wanneer u het distributie punt naar de site server doorzoekt, kunt u geen pakket gegevens valideren. Gebruik in plaats daarvan de Configuration Manager-console. Het hulp programma inspecteert het pakket nog steeds om ervoor te zorgen dat alle inhoud aanwezig is, maar niet noodzakelijkerwijs intact is.  

- U kunt inhoud met dit hulp programma niet verwijderen.



## <a name="see-also"></a>Zie tevens

- [Basisconcepten voor inhoudsbeheer](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [De inhoudsbibliotheek](../plan-design/hierarchy/the-content-library.md)
