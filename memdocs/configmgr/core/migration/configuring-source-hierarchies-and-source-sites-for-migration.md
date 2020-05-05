---
title: Migratie bron hiërarchieën
titleSuffix: Configuration Manager
description: Configureer een bron hiërarchie en bron sites, zodat u gegevens kunt migreren naar uw Configuration Manager huidige branch-omgeving.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c2e8e2ba57867b3c2a0929cfd670629296fdb9c9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718922"
---
# <a name="configure-source-hierarchies-and-source-sites-for-migration-to-configuration-manager-current-branch"></a>Bron hiërarchieën en bron sites configureren voor migratie naar Configuration Manager huidige vertakking

*Van toepassing op: Configuration Manager (huidige vertakking)*

Als u de migratie van gegevens naar uw Configuration Manager huidige branch-omgeving wilt inschakelen, moet u een ondersteunde Configuration Manager-bron hiërarchie en een of meer bron sites in die hiërarchie configureren die gegevens bevatten die u wilt migreren.  

> [!NOTE]  
>  Bewerkingen voor migratie worden uitgevoerd op de site op het hoogste niveau in de doel hiërarchie. Als u de migratie configureert wanneer u een Configuration Manager-console gebruikt die is verbonden met een primaire onderliggende site, moet u ervoor zorgen dat de configuratie wordt gerepliceerd naar de centrale beheer site, start en vervolgens de status weer repliceert naar de primaire site waarmee u bent verbonden.  

 Gebruik de informatie en procedures in de volgende secties om de bron hiërarchie op te geven en extra bron sites toe te voegen. Nadat u deze procedures hebt voltooid, kunt u migratie taken maken en beginnen met het migreren van gegevens van de bron hiërarchie naar de doel hiërarchie.  

-   [Een bron hiërarchie voor migratie opgeven](#BKBM_ConfigSrcHierarchy)  

-   [Aanvullende bron sites van de bron hiërarchie identificeren](#BKBM_ConfigSrcSites)  

##  <a name="specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a>Een bron hiërarchie voor migratie opgeven  
 Als u gegevens naar uw doel hiërarchie wilt migreren, moet u een ondersteunde bron hiërarchie opgeven die de gegevens bevat die u wilt migreren. Standaard wordt de site op het hoogste niveau van die hiërarchie een bron site van de bron hiërarchie. Als u migreert vanaf een Configuration Manager 2007-hiërarchie, kunt u aanvullende bron sites voor migratie instellen nadat gegevens van de oorspronkelijke bron site zijn verzameld. Als u migreert van een System Center 2012 Configuration Manager of Configuration Manager huidige branch-hiërarchie, hoeft u geen aanvullende bron sites in te stellen om gegevens van de bron hiërarchie te migreren. Dit komt doordat in deze versies van Configuration Manager een gedeelde data base wordt gebruikt die beschikbaar is op de site op het hoogste niveau van de bron hiërarchie. De gedeelde data base bevat alle informatie die u kunt migreren.  

 Gebruik de volgende procedures om een bron hiërarchie voor migratie op te geven en om aanvullende bron sites in een Configuration Manager 2007-hiërarchie te identificeren.  

 Voer deze procedure uit met een Configuration Manager-console die is verbonden met de doel hiërarchie:  

### <a name="to-configure-a-source-hierarchy"></a>Een bron hiërarchie configureren   

1. Klik op **Beheer**in de Configuration Manager-console.  

2. Vouw **Migratie** uit in de werkruimte **Beheer**en klik vervolgens op **Bronhiërarchie**.  

3. Klik op het tabblad **Start** in de groep **migratie** op **bron hiërarchie opgeven**.  

4. Selecteer in het dialoog venster **bron hiërarchie opgeven** , bij **bron hiërarchie**, de optie **nieuwe bron hiërarchie**.  

5. Voor **Configuration Manager site server op het hoogste niveau**voert u de naam of het IP-adres in van de site op het hoogste niveau van een ondersteunde bron hiërarchie.  

6. Geef toegangs accounts voor de bron site op die de volgende machtigingen hebben:  

   - Bron site account: machtiging **lezen** voor de SMS-provider voor de opgegeven site op het hoogste niveau in de bron hiërarchie. Voor het delen van distributie punten en upgrades moeten machtigingen voor **wijzigen** en **verwijderen** voor de site in de bron hiërarchie zijn vereist.

   - Bron site database account: machtiging **lezen** en **uitvoeren** voor de SQL Server Data Base voor de opgegeven site op het hoogste niveau in de bron hiërarchie.  

     Als u het gebruik van het computer account opgeeft, maakt Configuration Manager gebruik van het computer account van de site op het hoogste niveau van de doel hiërarchie. Voor deze optie moet u ervoor zorgen dat dit account lid is van de beveiligings groep **DCOM-gebruikers** in het domein waar de site op het hoogste niveau van de bron hiërarchie zich bevindt.  

7. Als u distributie punten tussen de bron-en doel hiërarchieën wilt delen, schakelt u het selectie vakje **delen van distributie punt voor de bron site server inschakelen** in. Als u het delen van distributie punten op dit moment niet inschakelt, kunt u dit doen door de referenties van de bron site te bewerken nadat het verzamelen van gegevens is voltooid.  

8. Klik op **OK** om de configuratie op te slaan. Hiermee opent u het dialoog venster status van het **verzamelen van gegevens** en wordt het verzamelen van gegevens automatisch gestart.  

9. Wanneer het verzamelen van gegevens is voltooid, klikt u op **sluiten** om het dialoog venster **status gegevens verzamelen** te sluiten en de configuratie te volt ooien.  

##  <a name="identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a>Aanvullende bron sites van de bron hiërarchie identificeren  
 Wanneer u een ondersteunde bron hiërarchie configureert, wordt de site op het hoogste niveau van die hiërarchie automatisch geconfigureerd als een bron site en worden de gegevens automatisch van die site verzameld. De volgende actie die u uitvoert, is afhankelijk van de versie van Configuration Manager die wordt uitgevoerd door de bron hiërarchie:  

-   Voor een Configuration Manager 2007-bron hiërarchie kunt u de migratie vanaf die eerste bron site starten of aanvullende bron sites van de bron hiërarchie instellen nadat het verzamelen van gegevens voor de oorspronkelijke bron site is voltooid. Als u gegevens wilt migreren die alleen beschikbaar zijn vanaf een onderliggende site, stelt u aanvullende bron sites in voor een Configuration Manager 2007-hiërarchie. U kunt bijvoorbeeld extra bron sites configureren voor het verzamelen van gegevens over inhoud die u wilt migreren wanneer deze wordt gemaakt op een onderliggende site in de bron hiërarchie en is niet beschikbaar op de site op het hoogste niveau van de bron hiërarchie.  

-   U hoeft geen aanvullende bron sites te configureren voor een System Center 2012 Configuration Manager of Configuration Manager huidige branch-bron hiërarchie. Dit komt doordat in deze versies van Configuration Manager een gedeelde data base wordt gebruikt die beschikbaar is op de site op het hoogste niveau van de bron hiërarchie. De gedeelde data base bevat alle informatie die u kunt migreren van alle sites in die bron hiërarchie. Dit maakt de gegevens die u kunt migreren beschikbaar op de site op het hoogste niveau van de bron hiërarchie.  

Wanneer u aanvullende bron sites configureert voor een Configuration Manager 2007-bron hiërarchie, moet u de extra bron sites vanaf de bovenkant van de bron hiërarchie naar beneden configureren. U moet een bovenliggende site als een bron site configureren voordat u een van de onderliggende sites als bron sites configureert.  

Gebruik de volgende procedure om aanvullende bron sites te configureren voor Configuration Manager 2007-bron hiërarchieën:  

### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Aanvullende bron sites in de bron hiërarchie identificeren 

1.  Klik op **Beheer**in de Configuration Manager-console.  

2.  Vouw **Migratie** uit in de werkruimte **Beheer**en klik vervolgens op **Bronhiërarchie**.  

3.  Kies de site die u wilt configureren als een bron site.  

4.  Klik op het tabblad **Start** in de groep **Bronsite** op **Configureren**.  

5.  Geef in het dialoog venster **bron site referenties** voor de toegangs accounts van de bron site de accounts op die de volgende machtigingen hebben:  

    -   Bron site account: machtiging **lezen** voor de SMS-provider voor de opgegeven site op het hoogste niveau in de bron hiërarchie. Voor het delen van distributie punten en upgrades moeten machtigingen voor **wijzigen** en **verwijderen** voor de site in de bron hiërarchie zijn vereist.  

    -   Bron site database account: machtiging **lezen** en **uitvoeren** voor de SQL Server Data Base voor de opgegeven site op het hoogste niveau in de bron hiërarchie.  

    Als u het gebruik van het computer account opgeeft, maakt Configuration Manager gebruik van het computer account van de site op het hoogste niveau van de doel hiërarchie. Voor deze optie moet u ervoor zorgen dat dit account lid is van de beveiligings groep **DCOM-gebruikers** in het domein waar de site op het hoogste niveau van de bron hiërarchie zich bevindt.  

6.  Als u distributie punten tussen de bron-en doel hiërarchieën wilt delen, schakelt u het selectie vakje **delen van distributie punt voor de bron site server inschakelen** in. Als u het delen van distributie punten op dit moment niet inschakelt, kunt u dit doen door de referenties voor de bron site te bewerken nadat het verzamelen van gegevens is voltooid.  

7. Klik op **OK** om de configuratie op te slaan. Hiermee opent u het dialoog venster status van het **verzamelen van gegevens** en wordt het verzamelen van gegevens automatisch gestart.  

8.  Wanneer het verzamelen van gegevens is voltooid, klikt u op **sluiten** om de configuratie te volt ooien.  
