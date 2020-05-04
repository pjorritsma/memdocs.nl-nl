---
title: Inleiding op energiebeheer
titleSuffix: Configuration Manager
description: Krijg een inleiding tot energie beheer in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 400fe3113207217504317eeb8ef8bbce4ab6a298
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715219"
---
# <a name="introduction-to-power-management-in-configuration-manager"></a>Inleiding tot energie beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Energie beheer in Configuration Manager is de nood zaak van veel organisaties om het energie verbruik van hun computers te controleren en te verminderen. Hierbij wordt gebruikgemaakt van de ingebouwde Windows-functies voor energiebeheer om relevante en consistente instellingen op computers in de organisatie toe te passen. U kunt tijdens kantooruren en buiten kantooruren verschillende energie-instellingen toepassen op computers. Het is bijvoorbeeld mogelijk dat u buiten kantooruren een meer beperkend energiebeheerschema op computers wilt toepassen. Wanneer computers altijd ingeschakeld moeten blijven, kunt u voorkomen dat energiebeheerinstellingen worden toegepast.  

 Energie beheer in Configuration Manager bevat verschillende rapporten waarmee u het energie verbruik en de energie-instellingen van computers in uw organisatie kunt analyseren. U kunt de rapporten ook gebruiken om problemen met energiebeheer op te lossen.  

 Zie [controle lijst voor beheerders voor energie beheer](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md)voor een gedetailleerde werk stroom over het configureren en gebruiken van energie beheer.  

> [!IMPORTANT]  
>  Configuration Manager energie beheer wordt niet ondersteund op virtuele machines. U kunt geen energiebeheerschema's toepassen op virtuele machines en u kunt hiervoor geen energiegegevens rapporteren.  

## <a name="the-power-management-workflow"></a>De werkstroom voor energiebeheer  
 Gebruik de volgende drie fasen om energie beheer te plannen en te implementeren in Configuration Manager.  

### <a name="monitoring-and-planning-phase"></a>Bewaking- en planningsfase  
 Energie beheer maakt gebruik van Configuration Manager hardware-inventaris voor het verzamelen van gegevens over computer gebruik en energie-instellingen voor computers in de site. U kunt verschillende rapporten gebruiken om deze gegevens te analyseren en de optimale energiebeheerinstellingen voor computers te bepalen. Tijdens de bewakings- en planningsfase van de werkstroom voor energiebeheer kunt u bijvoorbeeld verzamelingen maken die zijn gebaseerd op de gegevens die zijn opgenomen in het rapport **Stroomvoorzieningsmogelijkheden** en die gegevens gebruiken om de computers te identificeren die niet geschikt zijn voor energiebeheer. Vervolgens kunt u deze computers uitsluiten van energiebeheer.  

> [!IMPORTANT]  
>  Pas geen energiebeheerschema's op uw computers toe voordat u de energiegegevens van clientcomputers hebt verzameld en geanalyseerd. Als u nieuwe energiebeheerinstellingen op computers toepast zonder eerst de bestaande instellingen te controleren, kan dit leiden tot een toename van het energieverbruik.  

### <a name="enforcement-phase"></a>Afdwingingsfase  
 Met energiebeheer kunt u energiebeheerschema's maken die u op verzamelingen computers in uw site kunt toepassen. Met deze energiebeheerschema's worden Windows-instellingen voor energiebeheer geconfigureerd op computers. U kunt de energiebeheer schema's gebruiken die deel uitmaken van Configuration Manager, maar u kunt ook uw eigen aangepaste energiebeheer schema's configureren. U kunt de energiegegevens die tijdens de bewakings- en planningsfase zijn verzameld, gebruiken als basislijn om energiebesparingen te evalueren nadat u een energiebeheerschema op computers hebt toegepast. Zie [controle lijst voor beheerders voor energie beheer](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md)voor meer informatie.  

### <a name="compliance-phase"></a>Nalevingsfase  
 In de nalevingsfase kunt u rapporten uitvoeren om het energieverbruik en energiebesparingskosten in uw organisatie te evalueren. U kunt ook rapporten uitvoeren waarin de verbeteringen worden beschreven in de hoeveelheid CO2 gegenereerd door computers. Er zijn ook rapporten beschikbaar waarmee u kunt controleren of energie-instellingen correct zijn toegepast op computers en u problemen kunt oplossen met de functie voor energiebeheer.  
