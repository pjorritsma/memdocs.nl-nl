---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 98e3dd75316acfeaf88715b8f80762b1d6c587c6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128326"
---
<!--This file is shared by the cmpivot.md file and the cmpivot-changes.md file and contains information on how to run CMPivot standalone. H2s or HJ3s are determined by the article for which the include file is used.-->
<!--3555890, 4619340, 4683130 -->

Vanaf versie 1906 kunt u CMPivot als zelfstandige app gebruiken. Zelfstandige CMPivot is alleen beschikbaar in het Engels. Voer CMPivot buiten de Configuration Manager-console uit om de real-time status van apparaten in uw omgeving weer te geven. Met deze wijziging kunt u CMPivot gebruiken op een apparaat zonder eerst de-console te installeren.

> [!Tip]  
> Deze functie werd voor het eerst in versie 1906 geïntroduceerd als een [voorlopige functie](../pre-release-features.md). Vanaf versie 2002 is het niet langer een functie van de voorlopige versie.  

U kunt de kracht van CMPivot delen met andere personen, zoals helpdesk medewerkers of beveiligings beheerders, die de-console niet op hun computer hebben geïnstalleerd. Deze andere personen kunnen met behulp van CMPivot query's uitvoeren op Configuration Manager naast de andere hulp middelen die ze traditioneel gebruiken. Door deze uitgebreide beheer gegevens te delen, kunt u samen werken om zakelijke problemen met meerdere rollen proactief op te lossen.

#### <a name="install-cmpivot-standalone"></a>Zelfstandige installatie van CMPivot

1. Stel de machtigingen in die nodig zijn om CMPivot uit te voeren. Zie [vereisten](../cmpivot.md#prerequisites)voor meer informatie. U kunt ook de [rol beveiligings beheerder](../cmpivot-changes.md#bkmk_cmpivot_secadmin1906) gebruiken als de machtigingen geschikt zijn voor de gebruiker.
2. Zoek het installatie programma van de CMPivot-app op het volgende pad: `<site install path>\tools\CMPivot\CMPivot.msi` . U kunt het vanuit dat pad uitvoeren of het naar een andere locatie kopiëren.
3. Wanneer u de zelfstandige CMPivot-app uitvoert, wordt u gevraagd verbinding te maken met een site. Geef de naam van de Fully Qualified Domain Name of computer op van de server voor Centraal beheer of de primaire site.
   - Telkens wanneer u CMPivot standalone opent, wordt u gevraagd verbinding te maken met een site server.
4. Blader naar de verzameling waarop u CMPivot wilt uitvoeren en voer de query uit.

   ![Blader naar de verzameling waarvoor u de query wilt uitvoeren](../media/3555890-cmpivot-standalone-browse-collection.png)

> [!NOTE]
> - Met de rechter muisknop op acties, zoals **Run scripts**, **resource Explorer**en webzoekopdracht, zijn niet beschikbaar in de zelfstandige CMPivot. Het primaire gebruik van CMPivot-zelfstandige query's is onafhankelijk van de Configuration Manager-infra structuur. Ter ondersteuning van beveiligings beheerders biedt CMPivot standalone de mogelijkheid om verbinding te maken met micro soft Defender Security Center. <!--5605358-->
> - Vanaf versie 1910 kunt u de evaluatie van de [lokale query uitvoeren met behulp van CMPivot standalone](../cmpivot-changes.md#bkmk_local-eval). <!--3197353--> 