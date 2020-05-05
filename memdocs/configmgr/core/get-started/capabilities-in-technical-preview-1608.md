---
title: Mogelijkheden van Technical Preview 1608
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1608.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: fd668760a6b5d1a16cfbb8549063da4f7e8a8b7d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074177"
---
# <a name="capabilities-in-technical-preview-1608-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1608 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1608. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site.      Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Verbeteringen in de takenreeksstap ConfigMgr-client voorbereiden voor vastleggen  
Met de stap ConfigMgr-client voorbereiden wordt de Configuration Manager-client nu volledig verwijderd, in plaats van alleen de sleutel gegevens te verwijderen. Wanneer de taken reeks de vastgelegde installatie kopie van het besturings systeem implementeert, wordt elke keer een nieuwe Configuration Manager-client geïnstalleerd.  


## <a name="improvements-to-software-center"></a>Verbeteringen in Software Center
* Op de tabbladen Software Center- **toepassingen**, **updates**en **besturings systemen** wordt nu weer gegeven welke software onlangs is toegevoegd. In het navigatie venster ziet u hoeveel nieuwe software onderdelen op elk tabblad worden weer gegeven.
* Gebruikers kunnen nu goed keuring aanvragen voor toepassingen en vervolgens de aanvraag geschiedenis weer geven in de weer gave **toepassings Details** in Software Center. De knop **aanvraag** in **toepassings Details** wordt niet meer omgeleid naar de webtoepassingscatalogus.

## <a name="improvements-to-asset-intelligence"></a>Verbeteringen in Asset Intelligence
We hebben een veld toegevoegd aan de eigenschappen voor geïnventariseerde software waarmee u een bovenliggende en onderliggende relatie kunt instellen met andere software. In de lijst geïnventariseerde software kunt u vervolgens het bovenliggende onderdeel van alle software weer geven en ook alle onderliggende software verbergen.

### <a name="configure-a-parent-to-child-relationship"></a>Een bovenliggende en onderliggende relatie configureren
  1. Als u de bovenliggende software wilt instellen, klikt u in het knoop punt geïnventariseerde software met de rechter muisknop op een software-item in de lijst **geïnventariseerde software** en kiest u **Eigenschappen**.
  2. In het dialoog venster dat wordt geopend, selecteert u de software die u wilt instellen als de bovenliggende software voor de eerste selectie.

### <a name="filter-the-software-display"></a>De software weergave filteren
Nadat u de bovenliggende en onderliggende relaties hebt gedefinieerd, kunt u de weer gave filteren zodat alleen software wordt weer gegeven die een bovenliggend item is of die geen gedefinieerde relatie heeft. Hiermee wordt alle software verborgen die is ingesteld als onderliggend element van een andere geïnventariseerde software. Dit doet u als volgt:
   1. Kies voor de zoek balk **criteria toevoegen**
   2. Selecteer **bovenliggende software** , wijzig de criterium waarde in **leeg**en klik vervolgens op **zoeken**.

In het scherm worden nu alleen de bovenliggende software-items weer gegeven, of software waarvoor geen relaties zijn gedefinieerd. Alleen software die een onderliggend item van een andere titel is, wordt niet weer gegeven.

## <a name="remote-control-keyboard-translation"></a>Toetsenbord vertaling op afstand beheren
In het verleden heeft Configuration Manager de sleutel positie van de locatie van de viewer naar de locatie van de gedeelde persoon verzonden. Dit was een probleem voor de toetsenbord configuraties die verschillen van de viewer naar de delende map. Een viewer met een Engels toetsen bord zou bijvoorbeeld een ' A ' bevatten, maar het Franse toetsen bord van de delende persoon zou een ' Q ' zijn. Het standaard gedrag wordt gewijzigd, zodat het teken zelf wordt verzonden van het toetsen bord van de viewer naar de delende persoon en de manier waarop de viewer ingaat, arriveert bij de delende functie.

Dit gedrag kan worden uitgeschakeld door de Viewer als deze liever volgens de toetsenbord indeling van de delende persoon. Als u het gedrag wilt wijzigen, kiest u in **Configuration Manager beheer op afstand**de optie **actie**en kiest u **toetsenbord vertaling inschakelen** om de sleutel positie te verzenden.

> [!NOTE]
>
> Speciale sleutels, zoals ~! # @ $%, worden niet correct vertaald.
