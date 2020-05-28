---
title: Implementatie plannen maken
titleSuffix: Configuration Manager
description: Een hand leiding voor het maken van implementatie plannen in Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ac9b5ddd85904c90709a9450d6d2a9ffd379ddb9
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268756"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Implementatie plannen maken in Desktop Analytics

In dit artikel worden de stappen beschreven voor het maken van een implementatie plan in Desktop Analytics. Voordat u begint, moet u eerst [meer informatie over implementatie plannen](about-deployment-plans.md).

## <a name="create-a-plan-for-windows-10"></a>Een plan maken voor Windows 10

Volg de stappen in deze sectie om met Desktop Analytics een plan te maken voor de implementatie van Windows 10.

1. Open de [Desktop Analytics-Portal](https://aka.ms/desktopanalytics). Gebruik referenties met ten minste machtigingen voor **werk ruimte-inzenders** .  

2. Selecteer **implementatie plannen** in de groep beheren.  

3. Selecteer **maken**in het deel venster **implementatie plannen** .  

4. Configureer de volgende instellingen in het deel venster **implementatie plan maken** :  

    - **Naam**: een unieke naam voor het implementatie plan  

    - **Producten en versies**: Kies de versie van Windows 10 die u wilt implementeren. Micro soft raadt aan om implementatie plannen te maken die gebruikmaken van de meest recente versie.  

    - **Apparaatgroepen**: Selecteer een of meer groepen in dezelfde hiërarchie. Deze groepen zijn [apparaat verzamelingen](connect-configmgr.md#bkmk_Collections) gesynchroniseerd vanuit Configuration Manager.

        Als u meerdere Configuration Manager-hiërarchieën verbindt met hetzelfde bureau blad Analytics-exemplaar, wordt in een weergave naam voor de hiërarchie de naam van de verzameling voor voegsels in de globale pilot configuratie. Deze naam is de **weergave naam** eigenschap in de verbinding met de bureau blad Analytics in de Configuration Manager-console.<!-- 4814075 -->

        > [!NOTE]
        > Ondersteuning voor meerdere hiërarchieën vereist Configuration Manager versie 1910 of hoger.
        >
        > Als u verzamelingen voor meerdere hiërarchieën selecteert, wordt er een waarschuwing weer gegeven in de portal. U kunt het implementatie plan niet maken met verzamelingen uit meerdere hiërarchieën.<!-- 4814075 -->

    - **Gereedheids regels**: deze regels helpen om te bepalen welke apparaten in aanmerking komen voor een upgrade. Zie [gereedheids regels](#readiness-rules)voor meer informatie.  

    - **Voltooiings datum**: Kies de datum waarop Windows volledig moet worden geïmplementeerd op alle doel apparaten.  

5. Selecteer **Maken**. Het nieuwe plan wordt weer gegeven in de lijst met implementatie plannen terwijl het wordt verwerkt. Als u de verwerking wilt versnellen, moet u een gegevens vernieuwing op aanvraag aanvragen. Zie [Veelgestelde vragen over desktop Analytics](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal)voor meer informatie.  

6. Open het implementatie plan door de naam ervan te selecteren.  

7. Selecteer in het menu voor het implementatie plan in de groep **voorbereiden** de optie **belang rijkheid identificeren**.  

    1. Selecteer op het tabblad **apps** de optie om alleen **niet-gecontroleerde** assets weer te geven.  

    2. Selecteer elke app en selecteer vervolgens **bewerken**. U kunt meer dan één app selecteren om tegelijkertijd te bewerken.  

    3. Kies een urgentie niveau in de lijst **urgentie** . Als u wilt dat Desktop Analytics de app tijdens de test valideert, selecteert u **kritiek** of **belang rijk**. Apps die zijn gemarkeerd als **niet belang rijk**, worden niet gevalideerd. Evalueer de [compatibiliteit](compat-assessment.md) en andere plan inzichten bij het toewijzen van urgentie niveaus.  

        Bij het toewijzen van urgentie niveaus kunt u ook kiezen voor de upgrade beslissing.  

    4. Selecteer **Opslaan** wanneer u klaar bent.  

8. Selecteer in het menu voor het implementatie plan in de groep **voorbereiden** de optie **pilot identificeren**.  

    1. Bekijk de aanbevolen apparaten voor de test.  

    2. Selecteer elk apparaat en selecteer **toevoegen aan pilot**. Als u niet akkoord gaat met de aanbeveling, selecteert u **vervangen**.  

        Voor meer informatie over hoe Desktop Analytics deze aanbevelingen doet, selecteert u het informatie pictogram in de rechter bovenhoek van het deel venster **prototype identificeren** .

## <a name="readiness-rules"></a>Gereedheids regels

Met deze regels kunt u bepalen welke apparaten in aanmerking komen voor in-place upgrade. U kunt deze regels instellen wanneer u het implementatie plan maakt of ze later bewerken.

De gereedheids regels wijzigen:

1. Selecteer in de portal voor desktop Analytics het implementatie plan.
1. Selecteer vervolgens **bewerken**naast de naam.
1. Selecteer **gereedheids regels**.
1. Selecteer **Windows-besturings systeem**.
1. Breng de gewenste wijzigingen aan en selecteer **Opslaan**.

Voor upgrades van het **Windows-besturings systeem** zijn er twee regels beschikbaar: Apparaatstuurprogramma's en Windows-toepassingen.

### <a name="device-drivers"></a>Apparaatstuurprogramma 's

Configureer of uw apparaten Stuur Programma's van Windows Update ophalen. Deze waarde is standaard **uitgeschakeld** . Schakel deze regel in wanneer u Windows Update voor bedrijven gebruikt om updates te beheren, met inbegrip van Stuur Programma's. Als u gebruikmaakt van Configuration Manager voor het beheren van software-updates, stelt u deze regel in op **uit**.

### <a name="windows-applications"></a>Windows-toepassingen

De apps die door Desktop *Analytics worden weer gegeven, zijn* gebaseerd op de drempel waarde voor aantal kleine installaties. Stel deze drempel in voor de gereedheids regels voor het implementatie plan. Deze drempel waarde is standaard **2,0%**. U kunt de waarde wijzigen van `0.0` in `10.0` .


## <a name="next-steps"></a>Volgende stappen

Ga naar het volgende artikel om te implementeren op pilot-apparaten.
> [!div class="nextstepaction"]  
> [Implementeren voor testdoeleinden](deploy-pilot.md)  
