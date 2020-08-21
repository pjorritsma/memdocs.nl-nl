---
title: Software-updates implementeren
titleSuffix: Configuration Manager
description: Meer informatie over het hand matig of automatisch implementeren van software-updates in de Configuration Manager-console.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: a6e27e2d03983fdf627016d0e3b41aaa378afe29
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693468"
---
# <a name="deploy-software-updates"></a>Software-updates implementeren  

*Van toepassing op: Configuration Manager (huidige vertakking)*

De software-update-implementatie fase is het proces van het implementeren van software-updates. Ongeacht hoe u software-updates implementeert, de site:
- Voegt de updates toe aan een software-update groep
- Distribueert de update-inhoud naar distributie punten
- Hiermee wordt de update groep geïmplementeerd op clients  

Nadat u de implementatie hebt gemaakt, stuurt de site een bijbehorend software-update beleid naar doel clients. De-clients downloaden de software-update-inhouds bestanden van een inhouds bron naar hun lokale cache. Clients op internet downloaden altijd inhoud van de Microsoft Update-Cloud service. De software-updates zijn vervolgens beschikbaar voor installatie door de client.   

> [!Tip]  
>  Als een distributie punt niet beschikbaar is, kunnen clients op het intranet software-updates ook downloaden van Microsoft Update.  

> [!NOTE]  
>  In tegens telling tot andere implementatie types worden software-updates allemaal gedownload naar de client cache. Dit is ongeacht de maximale cache grootte-instelling op de client. Zie [de client cache voor Configuration Manager-clients configureren](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)voor meer informatie over de client cache-instelling.  

Als u een vereiste software-update-implementatie configureert, worden de software-updates automatisch geïnstalleerd tegen de geplande deadline. De gebruiker op de clientcomputer kan de installatie van de software-updates ook plannen of starten vóór de deadline. Na een geprobeerde installatie versturen clientcomputers statusberichten terug naar de siteserver om te rapporteren of de installatie van de software-update geslaagd was. Zie [Implementatiewerkstromen van software-updates](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows)voor meer informatie over de implementatie van software-updates.  

Er zijn drie belang rijke scenario's voor het implementeren van software-updates: 
- [Handmatige implementatie](#BKMK_ManualDeployment)  
- [Automatische implementatie](#bkmk_auto)  
- [Gefaseerde implementatie](#bkmk_phased)  

Normaal gesp roken begint u met het hand matig implementeren van software-updates om een basis lijn voor uw clients te maken. vervolgens beheert u software-updates op clients met behulp van een automatische of gefaseerde implementatie.  

> [!Note]  
> U kunt geen automatische implementatie regel gebruiken met een gefaseerde implementatie.



## <a name="manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Software-updates hand matig implementeren
Selecteer software-updates in de Configuration Manager-console en start het implementatie proces hand matig. Normaal gesp roken gebruikt u deze implementatie methode voor het volgende:  

- Clients up-to-date ophalen met vereiste software-updates voordat u automatische implementatie regels maakt voor het beheren van maandelijkse implementaties  

- Out-of-band-software-updates implementeren  


De volgende lijst geeft de algemene werkstroom voor handmatige implementatie van software-updates:  

1. Filter voor software-updates die gebruikmaken van specifieke vereisten. U kunt bijvoorbeeld criteria opgeven die alle beveiligings-of kritieke software-updates ophalen die op meer dan 50 clients zijn vereist.  

2. Maak een software-updategroep die de software-updates bevat.  

3. Downloadt de inhoud voor software-updates in de software-updategroep.  

4. De software-updategroep handmatig implementeren.  

Zie [software-updates hand matig implementeren](manually-deploy-software-updates.md)voor meer informatie en gedetailleerde stappen.

> [!Note]
> - Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds verwijzingen naar de oude naam in de Configuration Manager-console en de ondersteunende documentatie terwijl de-console wordt bijgewerkt.
> - Wanneer u Microsoft 365 apps-client updates hand matig implementeert, kunt u deze vinden in het knoop punt **office 365-updates** onder **Office 365 client management** van de werk ruimte **software bibliotheek** . 

## <a name="automatically-deploy-software-updates"></a><a name="bkmk_auto"></a> Software-updates automatisch implementeren

Automatische implementatie van software-updates configureren met behulp van een regel voor automatische implementatie (ADR). Deze implementatie methode is gebruikelijk voor maandelijkse software-updates (meestal ' patch dinsdag ' genoemd) en voor het beheren van definitie-updates. U definieert de criteria voor een ADR om het implementatie proces te automatiseren. De volgende lijst bevat de algemene werk stroom voor het automatisch implementeren van software-updates:  

1.  Maak een ADR waarmee implementatie-instellingen worden opgegeven.  

2.  De-site voegt de software-updates toe aan een software-update groep.  

3.  De site implementeert de software-update groep voor de clients in de doel verzameling.  

Bepaal eerst uw automatische implementatie strategie voor software-updates. Maak bijvoorbeeld de ADR om in eerste instantie een verzameling test-clients te richten. Nadat u hebt gecontroleerd of de test groep de software-updates heeft geïnstalleerd, voegt u een nieuwe implementatie aan de regel toe. U kunt ook de doel verzameling in de bestaande implementatie wijzigen in een die een grotere set clients bevat. Houd rekening met het volgende gedrag bij het bepalen van de te gebruiken strategie:  

- U kunt de eigenschappen van de software-update objecten die door de ADR worden gemaakt, wijzigen.   

- De ADR implementeert automatisch software-updates naar clients wanneer u deze toevoegt aan de doel verzameling.  

- Wanneer u of de ADR nieuwe software-updates toevoegt aan de software-update groep, implementeert de site deze automatisch naar de clients in de doel verzameling.  

- Implementaties op elk gewenst moment in-of uitschakelen voor de ADR.  


Nadat u een ADR hebt gemaakt, kunt u aanvullende implementaties aan de regel toevoegen. Deze actie helpt u bij het beheren van de complexiteit van het implementeren van verschillende updates voor verschillende verzamelingen. Elke nieuwe implementatie heeft alle functionaliteit en biedt de volledige implementatiebewakingservaring.  

Elke nieuwe implementatie die u toevoegt:  

- Maakt gebruik van dezelfde update groep en hetzelfde pakket, die door de ADR wordt gemaakt wanneer deze voor het eerst wordt uitgevoerd  
- Kan een andere verzameling bereiken  
- Ondersteunt unieke implementatie-eigenschappen, waaronder:  
  -   Activeringstijd  
  -   Deadline  
  -   Gebruikerservaring  
  -   Afzonderlijke waarschuwingen voor elke implementatie  


Zie [software-updates automatisch implementeren](automatically-deploy-software-updates.md) voor meer informatie en gedetailleerde stappen.



## <a name="deploy-software-updates-in-phases"></a><a name="bkmk_phased"></a> Software-updates implementeren in fasen

<!--1358146-->
Vanaf versie 1810 maakt u gefaseerde implementaties voor software-updates. Met gefaseerde implementaties kunt u een gecoördineerde, geordende implementatie van software organiseren op basis van aanpas bare criteria en groepen.

Zie voor meer informatie [gefaseerde implementaties maken](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).

