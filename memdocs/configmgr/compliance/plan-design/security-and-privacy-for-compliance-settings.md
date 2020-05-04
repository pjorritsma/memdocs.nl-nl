---
title: Beveiliging en privacy voor instellingen voor naleving
titleSuffix: Configuration Manager
description: Meer informatie over de aanbevolen beveiligings procedures voor nalevings instellingen in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1c409244-6778-4970-a99c-d2508c9cf62b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: eae705b97add7515403549eb668e68f1489d6756
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712146"
---
# <a name="security-and-privacy-for-compliance-settings-in-configuration-manager"></a>Beveiliging en privacy voor instellingen voor naleving in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*


## <a name="security-best-practices-for-compliance-settings"></a>Aanbevolen beveiligingsprocedures voor nalevingsinstellingen  

|Aanbevolen beveiligingsprocedure|Meer informatie|  
|----------------------------|----------------------|  
|Bewaak gevoelige gegevens niet.|Als u wilt voorkomen dat mogelijk gevoelige gegevens openbaar worden gemaakt, moet u configuratie-items niet zo configureren dat deze gegevens worden bewaakt.|  
|Configureer geen compatibiliteitsregels die gegevens gebruiken die door eindgebruikers kunnen worden gewijzigd.|Als u een nalevingsregel maakt op basis van gegevens die gebruikers kunnen wijzigen, zoals registerinstellingen voor configuratieopties, zijn de nalevingsresultaten niet betrouwbaar.|  
|Importeer Microsoft System Center-configuratiepakketten en andere configuratiegegevens alleen uit externe bronnen als deze beschikken over een geldige digitale handtekening van een vertrouwde uitgever.|Gepubliceerde configuratiegegevens kunnen digitaal worden ondertekend zodat u de uitgiftebron kunt verifiëren en er zeker van kunt zijn dat er niet is geknoeid met de gegevens. Als de verificatiecontrole van de digitale handtekening mislukt, ontvangt u een waarschuwing en wordt u gevraagd of u wilt doorgaan met importeren. Importeer geen niet-ondertekende gegevens als de bron en de integriteit van de gegevens niet kunnen worden geverifieerd.|  
|Toegangsbeheer implementeren om referentiecomputers te beveiligen.|Wanneer een gebruiker met beheerdersrechten een register- of bestandssysteeminstelling wil configureren door te bladeren naar een referentiecomputer, moet u ervoor zorgen dat er niet is geknoeid met de referentiecomputer.|  
|Beveilig het communicatiekanaal wanneer u naar een referentiecomputer bladert.|Gebruik Internet Protocol-beveiliging (IPsec) of Server Message Block (SMB) tussen de computer waarop de Configuration Manager-console en de referentie computer worden uitgevoerd om te voor komen dat de gegevens worden geknoeid wanneer deze via het netwerk worden overgedragen.|  
|Beperk en bewaak de gebruikers met beheerdersrechten die de rol van beheerder van nalevingsinstellingen krijgen|Gebruikers met beheerdersrechten die de rol **Beheerder van instellingen voor naleving** krijgen, kunnen configuratie-items voor alle apparaten en gebruikers in de hiërarchie implementeren. Configuratie-items kunnen zeer krachtig zijn en kunnen bijvoorbeeld scripts en registerconfiguraties bevatten.|  

## <a name="privacy-information-for-compliance-settings"></a>Privacygegevens voor nalevingsinstellingen  
 U kunt nalevingsinstellingen gebruiken om te evalueren of uw clientapparaten compliant zijn met configuratie-items die u in configuratiebasislijnen implementeert. Sommige instellingen kunnen automatisch worden hersteld als deze niet compliant zijn. Compatibiliteitsinformatie wordt naar de siteserver verzonden door het beheerpunt en wordt opgeslagen in de sitedatabase. De informatie wordt versleuteld wanneer apparaten deze naar het beheerpunt verzenden, maar deze wordt niet in een versleutelde indeling opgeslagen in de sitedatabase. Informatie wordt bewaard in de database en wordt na negentig dagen verwijderd door de siteonderhoudstaak **Verouderde gegevens van Configuration Manager verwijderen** . U kunt het verwijderingsinterval configureren. Er wordt geen compatibiliteitsinformatie naar Microsoft verzonden.  

 Standaard worden nalevingsinstellingen niet door apparaten geëvalueerd. Bovendien moet u de configuratie-items en configuratiebasislijnen configureren en vervolgens implementeren voor apparaten.  
