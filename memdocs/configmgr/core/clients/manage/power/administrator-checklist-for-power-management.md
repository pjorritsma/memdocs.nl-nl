---
title: Controlelijst voor beheerders voor energiebeheer
titleSuffix: Configuration Manager
description: Gebruik de controle lijst voor beheerders om energie beheer te plannen en te implementeren in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 039ebf73fba9850b8479bfabab6ab928b7d6f2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715282"
---
# <a name="administrator-checklist-for-power-management-in-configuration-manager"></a>Controle lijst voor beheerders voor energie beheer in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Deze controle lijst voor beheerders biedt de aanbevolen stappen voor het gebruik van Configuration Manager energie beheer in uw organisatie.  

## <a name="configuring-power-management"></a>Energiebeheer configureren  
 Volg deze stappen om uw hiërarchie te configureren om energiebeheerinformatie te verzamelen bij clientcomputers.  

> [!IMPORTANT]  
>  Pas geen energiebeheerschema's toe op computers in uw hiërarchie tot u gegevens van energiebeheer van clientcomputers hebt verzameld en geanalyseerd. Als u nieuwe energiebeheerinstellingen op computers toepast zonder eerst de bestaande instellingen te controleren, kan dit leiden tot een toename van het energieverbruik.  

|Taak|Details|  
|----------|-------------|  
|Bekijk de energiebeheer concepten in de documentatie bibliotheek van Configuration Manager.|Zie [Inleiding tot energie beheer](introduction-to-power-management.md).|  
|Controleer de vereisten voor energie beheer in de documentatie bibliotheek van Configuration Manager.|Zie [vereisten voor energie beheer](prerequisites-for-power-management.md).|  
|Bekijk de informatie over de aanbevolen procedures voor energiebeheer.|Zie [Aanbevolen procedures voor energie beheer](best-practices-for-power-management.md).|  
|Configureer uw verzamelingen voor het beheren van het energie verbruik van computers in uw omgeving.|Gebruik de **verzameling voor de rapportage van basislijn gegevens**, het verzamelen van de **basis gegevens**, het verzamelen van computers die niet geschikt zijn voor **energie beheer**, **verzamelingen van computers waarop energie schema's worden toegepast**, verzamelingen van computers waarop **energie schema's worden toegepast**en **verzamelingen computers waarop Windows Server wordt uitgevoerd** om u te helpen bij het beheren van energie-instellingen voor computers in uw hiërarchie. U kunt meerdere verzamelingen maken en verschillende energiebeheerschema's toepassen op elke verzameling.|  
|Energiebeheer inschakelen.|Voordat u energiebeheer kunt gaan gebruiken, moet u dit inschakelen en de vereiste clientinstellingen configureren. Zie [energie beheer configureren](configuring-power-management.md)voor meer informatie.|  
|Energiebeheerinformatie verzamelen bij clientcomputers.|Energie beheer gegevens worden door clients gerapporteerd via Configuration Manager Hardware-inventarisatie. Afhankelijk van de hardware-inventarisplanning die u hebt geconfigureerd, kan het enige tijd duren om inventarisgegevens bij alle clientcomputers op te vragen.|  

## <a name="monitoring-and-planning-phase"></a>Bewaking- en planningsfase  

|Taak|Details|  
|----------|-------------|  
|Voer het rapport **Computeractiviteit**uit.|In het rapport **Computeractiviteit** wordt een grafiek weergegeven met bewakings-, computer- en gebruikersactiviteit voor een opgegeven verzameling gedurende een opgegeven periode. Dit rapport is gekoppeld aan het rapport **Details van computeractiviteit** waarin de slaap- en waakmogelijkheden van computers in de opgegeven verzameling worden weergegeven. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Voer het rapport **Energieverbruik** of **Energieverbruik per dag**uit.|In het rapport **Energieverbruik** en het rapport **Energieverbruik per dag** worden het totale maandelijkse energieverbruik in kilowatt per uur (kWh) weergegeven voor een opgegeven verzameling gedurende een opgegeven periode. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Voer het rapport **milieu impact** of **impact op het milieu op dag**uit.|In de rapporten **Uitwerking op milieu** en **Uitwerking op milieu op dag** wordt een grafiek met kooldioxide-uitstoot (CO2) weergegeven die wordt bespaard door een opgegeven verzameling van computers gedurende een opgegeven periode. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Voer het rapport **Energiekosten** of **Energiekosten op dag**uit.|In de rapporten **Energiekosten** en **Energiekosten op dag** worden de totale energieverbruikskosten weergegeven voor een opgegeven periode. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Voer het rapport **Stroomvoorzieningsmogelijkheden**uit.|Het rapport **Stroomvoorzieningsmogelijkheden** geeft de energiebeheermogelijkheden van computers in de opgegeven verzameling weer. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Voer het rapport **Energie-instellingen**uit.|Het rapport **Energie-instellingen** bevat een samengevoegde lijst met de huidige energie-instellingen die door computers in een opgegeven verzameling worden gebruikt. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Alle vereiste verzamelingen van computers uitsluiten van energiebeheer.|Zie [energie beheer configureren](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Zorg ervoor dat u de rapporten met energiebeheergegevens opslaat die tijdens de bewakings- en planningsfase zijn gegenereerd. U kunt deze gegevens vergelijken met energiebeheergegevens die zijn gegenereerd tijdens de afdwingings- en nalevingsfase, zodat u het energieverbruik, de energiekosten en milieubesparingen kunt beoordelen die horen bij het toepassen van een energieplan op computers in uw hiërarchie.  

## <a name="enforcement-phase"></a>Afdwingingsfase  

|Taak|Details|  
|----------|-------------|  
|Bestaande energiebeheerschema's selecteren of nieuwe energiebeheerschema's maken voor verzamelingen van computers in uw organisatie.|Zie [Energiebeheer schema's maken en Toep assen](create-and-apply-power-plans.md).|  
|Deze energiebeheerschema's toepassen op computers.|Zie [Energiebeheer schema's maken en Toep assen](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Nalevingsfase  

|Taak|Details|  
|----------|-------------|  
|Voer het rapport **Computeractiviteit**uit.|In het rapport **Computeractiviteit** wordt een grafiek weergegeven met bewakings-, computer- en gebruikersactiviteit voor een opgegeven verzameling gedurende een opgegeven periode. Dit rapport is gekoppeld aan het rapport **Details van computeractiviteit** waarin de slaap- en waakmogelijkheden van computers in de opgegeven verzameling worden weergegeven. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Voer het rapport **Energieverbruik** of **Energieverbruik per dag**uit.|In het rapport **Energieverbruik** en het rapport **Energieverbruik per dag** worden het totale maandelijkse energieverbruik in kilowatt per uur (kWh) weergegeven voor een opgegeven verzameling gedurende een opgegeven periode. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Voer het rapport **Uitwerking op milieu** of **Uitwerking op het milieu op dag**uit.|In de rapporten **Uitwerking op milieu** en **Uitwerking op milieu op dag** wordt een grafiek met kooldioxide-uitstoot (CO2) weergegeven die wordt bespaard door een opgegeven verzameling van computers gedurende een opgegeven periode. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Voer het rapport **Energiekosten** of **Energiekosten op dag**uit.|In de rapporten **Energiekosten** en **Energiekosten op dag** worden de totale energieverbruikskosten weergegeven voor een opgegeven periode. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  

## <a name="troubleshooting"></a>Problemen oplossen  

|Taak|Details|  
|----------|-------------|  
|Als de computers in uw hiërarchie niet zijn overgeschakeld op de slaapstand of sluimerstand, voert u het **slapeloosheidsrapport** uit om mogelijke oorzaken weer te geven.|Het **Slapeloosheidsrapport** geeft een lijst met algemene oorzaken weer die voorkomen dat computers overschakelen naar de slaapstand of sluimerstand, evenals het aantal computers dat hierdoor gedurende een bepaalde periode is getroffen. Zie [energie beheer bewaken en plannen voor](monitor-and-plan-for-power-management.md)meer informatie.|  
|Als er meerdere energiebeheerschema's worden toegepast op een computer, wordt het minst beperkende energiebeheerschema toegepast. Voer het rapport **Computers met meerdere energiebeheerschema's** uit om de computers te zien waarop meerdere energiebeheerschema's worden toegepast.|Zie **computers met meerdere** energiebeheer schema's [voor energie beheer bewaken en plannen](monitor-and-plan-for-power-management.md).|  
