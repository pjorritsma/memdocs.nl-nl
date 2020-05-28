---
title: Migratie beveiliging en privacy
titleSuffix: Configuration Manager
description: Lees de aanbevolen procedures voor beveiliging en privacy-informatie voor migratie naar uw Configuration Manager huidige branch-omgeving.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad92e4906c45b5c720ab35efc055449a27cc0850
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906221"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>Beveiliging en privacy voor migratie naar Configuration Manager huidige branch

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit onderwerp bevat aanbevolen procedures voor beveiliging en privacy-informatie voor migratie naar uw Configuration Manager huidige branch-omgeving.  

## <a name="security-best-practices-for-migration"></a>Aanbevolen beveiligings procedures voor migratie  
 Gebruik de volgende beveiligings best practice voor migratie.  

|Aanbevolen beveiligingsprocedure|Meer informatie|  
|----------------------------|----------------------|  
|Gebruik het computer account voor het SMS-provider account van de bron site en de bron site SQL Server account in plaats van een gebruikers account.|Als u een gebruikers account moet gebruiken voor migratie, verwijdert u de account gegevens wanneer de migratie is voltooid.|  
|Gebruik IPsec wanneer u inhoud migreert van een distributie punt in een bron site naar een distributie punt in de doel site.|Hoewel de gemigreerde inhoud wordt gehasht om knoeien te detecteren, mislukt de migratie als de gegevens worden gewijzigd.|  
|Beperk en bewaak de gebruikers met beheerders rechten die migratie taken kunnen maken.|De integriteit van de data base van de doel hiërarchie is afhankelijk van de integriteit van gegevens die de gebruiker met beheerders rechten wil importeren uit de bron hiërarchie. Daarnaast kan deze gebruiker met beheerders rechten alle gegevens lezen uit de bron hiërarchie.|  

### <a name="security-issues-for-migration"></a>Beveiligings problemen voor migratie  
Migratie heeft de volgende beveiligings problemen:  

-   Clients die zijn geblokkeerd vanaf een bron site, kunnen worden toegewezen aan de doel hiërarchie voordat hun client record wordt gemigreerd.  

     Hoewel Configuration Manager de geblokkeerde status behoudt van clients die u migreert, kan de client worden toegewezen aan de doel hiërarchie als de toewijzing plaatsvindt voordat de migratie van de client record is voltooid.  

-   Controle berichten worden niet gemigreerd.  

Wanneer u gegevens migreert van een bron site naar een doel site, verliest u de controle gegevens van de bron hiërarchie.  

## <a name="privacy-information-for-migration"></a>Privacy-informatie voor migratie  
 Migratie detecteert gegevens van de site databases die u identificeert in een bron infrastructuur en slaat deze gegevens op in de data base in de doel hiërarchie. De informatie die Configuration Manager van een bron site of-hiërarchie kan detecteren, is afhankelijk van de functies die zijn ingeschakeld in de bron omgeving, evenals de beheer bewerkingen die zijn uitgevoerd in die bron omgeving.  

 Zie een van de volgende onderwerpen voor meer informatie over beveiligings-en privacy-informatie:  

-   Zie [beveiliging en privacy voor Configuration Manager 2007](https://docs.microsoft.com/previous-versions/system-center/configuration-manager-2007/bb680768(v=technet.10)) in de documentatie bibliotheek van Configuration Manager 2007 voor meer informatie over de privacy-informatie voor Configuration Manager 2007.  

-   Zie [beveiliging en privacy voor System center 2012 Configuration Manager](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/gg682033(v=technet.10)) in de documentatie bibliotheek van system center 2012 Configuration Manager voor meer informatie over de privacy-informatie voor system center 2012 Configuration Manager.  

-   Zie voor meer informatie over de privacy-informatie voor Configuration Manager [beveiliging en privacy voor Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

U kunt enkele of alle ondersteunde gegevens van een bron site naar een doel hiërarchie migreren.  

Migratie is niet standaard ingeschakeld en vereist verschillende configuratie stappen. Migratie gegevens worden niet naar micro soft verzonden.  

Voordat u gegevens migreert vanuit een-bron hiërarchie, moet u rekening houden met uw privacy-vereisten.  
