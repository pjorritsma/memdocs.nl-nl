---
title: Client status met co-beheer
titleSuffix: Configuration Manager
description: Zicht baarheid van de Configuration Manager client status van intune op Azure Portal onderhouden
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711194"
---
# <a name="client-health-with-co-management"></a>Client status met co-beheer

De status van uw netwerk is rechtstreeks verbonden met de status van de apparaten die in en uit het verplaatsen. InTune kan communiceren met een slechte client, zelfs wanneer deze zich niet in uw netwerk bevindt. Gebruik co-beheer om deze functie te combi neren met de mogelijkheden van Configuration Manager om 98% van bekende clients te melden. Vervolgens kunt u alle clients in realtime detecteren, evalueren en er zicht op geven. InTune voegt ook de ondersteuning toe die nodig is voor het bijwerken van de naleving op alle verbonden clients.

In de volgende video is Senior Program Manager Rob York en de Ainley-vergren deling en de client status van de product marketing manager met co-beheer uitgebreid:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Voordelen

Het beoordelen van de client status is een topprioriteit. System Center 2012 Configuration Manager **CCMeval**toegevoegd. Dit hulp programma is extern voor de Configuration Manager-client. Het biedt client status controle en automatisch herstel. Deze rapportage is echter afhankelijk van een fysiek of virtueel netwerk apparaat. Co-beheer helpt dit probleem op te lossen.

Met co-beheer kan intune rapporteren over de status van de client. Het bevat informatie over de tijds tempel voor de geldigheid van de gegevens. Deze informatie geeft aan of uw apparaten in orde zijn, verbinding kunnen maken, apps kunnen installeren of kunnen bijwerken naar de vereiste OS-builds. 

Voor een gedetailleerd overzicht van deze functie raadpleegt u deze video van de [What's New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) -sessie op Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Wanneer Configuration Manager de status van het apparaat levert dat de-client is geïnstalleerd, maar dit niet het geval is, kan intune meer informatie geven zonder dat er verbinding hoeft te worden gemaakt met de client. De status informatie voor het apparaat in intune is eenvoudig te begrijpen. Als de status iets anders is dan **in orde**, geeft het aanbevelingen en de volgende stappen om het probleem op te lossen en op te lossen.

> [!Note]  
> De volgende voor delen zijn gepland voor een toekomstige versie:
> - Configuration Manager bevat extra functionaliteit in CCMeval  
> - Het is eenvoudiger om mogelijk slechte computers te identificeren in zowel Configuration Manager als intune  
> - U kunt de client status gegevens groeperen in intune  



## <a name="value-proposition"></a>Toegevoegde waarde

Met deze functie hebt u nu een externe gegevens bron met intune. Hiermee kunt u de volgende stappen voor het oplossen van problemen met een groot aantal client problemen bepalen. U hoeft nu geen aanvullende rapporten te maken of andere hulpprogram ma's te gebruiken om client gegevens terug te halen.

Wanneer u goede clients hebt, hebt u de compatibiliteit van patches direct bijgewerkt. Betere naleving van patches betekent betere beveiliging.



## <a name="configure"></a>Configureren

Gebruik de volgende stappen om aan de slag te gaan met deze functie:

- Apparaten bijwerken naar Windows 10, versie 1709 of hoger  

- [Co-beheer inschakelen](how-to-enable.md)  
    - U hoeft geen workload over te scha kelen naar intune  

- Uw Configuration Manager-site en-clients bijwerken naar *versie 1806* of hoger  


### <a name="review-configuration-manager-client-health-in-intune"></a>Status van Configuration Manager-client controleren in intune

1. Meld u aan bij de [Azure Portal](https://portal.azure.com/).  

2. Kies **alle services** > **intune**. Intune bevindt zich in de sectie **Bewaking en beheer**.  

3. Zodra u het deel venster **Microsoft intune** hebt geopend, gaat u in het menu onder **Help en ondersteuning**naar de pagina **problemen oplossen** .  

4. Gebruik de optie **gebruiker selecteren** , zoek het specifieke apparaat in de lijst met **apparaten** en selecteer dit om de pagina apparaat te openen.  

5. Informatie over co-beheer wordt weer gegeven aan de onderkant van de pagina apparaat. Deze informatie omvat de volgende velden voor client status:  
    - **Status van Configuration Manager agent**  
    - **Tijd waarop de laatste Configuration Manager-agent is ingecheckt**  

> [!Tip]  
> InTune-geregistreerde apparaten maken drie keer per dag een verbinding met de Cloud service, ongeveer om de acht uur. 
