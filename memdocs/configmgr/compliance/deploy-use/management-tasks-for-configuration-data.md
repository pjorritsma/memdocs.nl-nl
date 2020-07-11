---
title: Configuratiegegevens beheren
titleSuffix: Configuration Manager
description: Nadat u configuratie-items en basis lijnen in Configuration Manager hebt gemaakt, kunt u andere opdrachten gebruiken om verschillende acties uit te voeren.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: c375b5d773775e1be89f1e9dda38ee04e7f9f63f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240249"
---
# <a name="manage-configuration-data-in-configuration-manager"></a>Configuratie gegevens in Configuration Manager beheren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u configuratie-items en configuratie basislijnen hebt gemaakt in Configuration Manager, zijn er meer opdrachten beschikbaar om u te helpen bij het uitvoeren van verschillende acties.  

## <a name="manage-configuration-items"></a>Configuratie-items beheren  

-   Vouw in de werk ruimte **activa en naleving** het knoop punt configuratie-items voor **nalevings instellingen**uit  >  **Configuration Items**, selecteer het configuratie-item dat u wilt beheren en selecteer vervolgens een beheer taak.  

|Beheertaak|Details|  
|---------------------|-------------|  
|**Onderliggend configuratie-item maken**|Hiermee opent u de **Wizard Onderliggend configuratie-item maken** waarmee u een onderliggend configuratie-item kunt maken van het geselecteerde configuratie-item.<br /><br /> U kunt geen onderliggend configuratie-item maken van een configuratie-item voor mobiele apparaten.<br /><br /> Zie [onderliggende configuratie-items maken](../../compliance/deploy-use/create-child-configuration-items.md)voor meer informatie.|  
|**Overzicht van wijzigingen**|Hiermee opent u het dialoogvenster **Overzicht van wijzigingen van configuratie-item** waarin u eerdere versies van het geselecteerde configuratie-item kunt weergeven en beheren.|  
|**XML-definitie weergeven**|Toont de definitie van het XML-bestand voor het geselecteerde configuratie-item in een nieuw venster. Deze informatie kan nuttig zijn wanneer u configuratiegegevens handmatig wilt maken.|  
|**Exporteren**|Exporteert een configuratie-item naar een CAB-bestand-indeling, mits het is gemaakt op die site. U kunt deze vervolgens importeren op dezelfde of een andere Configuration Manager-site. Configuratiegegevens worden geconverteerd naar DCM Digest.|  
|**Kopiëren**|Maakt een kopie van het geselecteerde configuratie-item met een naam die u opgeeft. Het nieuwe configuratie-item behoudt geen relatie met het oorspronkelijke configuratie-item. Dit betekent dat het dubbele configuratie-item geen configuratie-informatie blijft overnemen van het oorspronkelijke configuratie-item.|  
|**Verwijderen**|Hiermee opent u het dialoogvenster **Configuratie-item verwijderen** waarin u alle verwijzingen naar dit configuratie-item kunt bekijken.<br /><br /> U moet alle verwijzingen naar een configuratie-item verwijderen voordat u dit kunt verwijderen.|  

## <a name="manage-configuration-baselines"></a>Configuratie basislijnen beheren  

-   Vouw in de werk ruimte **activa en naleving** het knoop punt **Compliance Settings**  >  **configuratie basislijnen**voor naleving uit, selecteer de configuratie basislijn die u wilt beheren en selecteer vervolgens een beheer taak.  


|Beheertaak|Details|  
|---------------------|-------------|  
|**Leden weergeven**|Geeft alle configuratie-items weer waarnaar wordt verwezen door de configuratiebasislijn.|  
|**Overzicht plannen**|Hiermee configureert u het schema waarmee de gegevens die worden weer gegeven in het knoop punt **configuratie basislijnen** in de Configuration Manager-console worden bijgewerkt met de meest recente gegevens uit de site database.|  
|**Overzicht uitvoeren**|Het maken van een overzicht zorgt ervoor dat de gegevens op het knooppunt **Configuratiebasislijnen** worden vernieuwd met de meest recente gegevens uit de sitedatabase. Deze actie kan enkele minuten duren. Mogelijk moet u op **Vernieuwen** klikken voordat u de meest recente gegevens in de console kunt zien.|  
|**XML-definitie weergeven**|Toont de definitie van het XML-bestand voor de geselecteerde configuratiebasislijn in een nieuw venster. Deze informatie kan nuttig zijn wanneer u configuratiegegevens handmatig wilt maken.|  
|**Inschakelen**|Hiermee wordt een configuratiebasislijn ingeschakeld voor het bewaken van naleving.|  
|**Uitschakelen**|Hiermee wordt een configuratiebasislijn uitgeschakeld zodat deze niet langer wordt geëvalueerd voor naleving op clientcomputers. Configuratiebasislijnen die verwijzen naar deze configuratiebasislijn worden ook uitgeschakeld.|  
|**Exporteren**|Exporteert een configuratiebasislijn naar een CAB-bestand-indeling, mits deze is gemaakt op die site. U kunt deze vervolgens importeren op dezelfde of een andere Configuration Manager-site. Configuratiegegevens worden geconverteerd naar DCM Digest.<br /><br /> Zie [configuratie gegevens importeren](../../compliance/deploy-use/import-configuration-data.md)voor meer informatie over het importeren van configuratie gegevens.|  
|**Kopiëren**|Maakt een kopie van de geselecteerde configuratiebasislijn met een naam die u opgeeft. De nieuwe configuratiebasislijn behoudt geen relatie met de oorspronkelijke configuratiebasislijn.|  
|**Verwijderen**|Hiermee opent u het dialoogvenster **Configuratiebasislijn verwijderen** waarin u alle verwijzingen naar deze configuratiebasislijn kunt bekijken.<br /><br /> U moet alle verwijzingen naar een configuratiebasislijn verwijderen voordat u deze kunt verwijderen.|  
|**Implementeren**|Hiermee opent u het dialoogvenster **Configuratiebasislijn implementeren** waarin u een of meer configuratiebasislijnen kunt implementeren op apparaten in uw hiërarchie.<br /><br /> Zie [configuratie basislijnen implementeren](../../compliance/deploy-use/deploy-configuration-baselines.md)voor meer informatie.|  
