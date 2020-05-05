---
title: Update catalogussen beheren
titleSuffix: Configuration Manager
description: Software-update catalogussen voor System Center Updates Publisher beheren
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1314e2b4a6adc21b876e6bdbf8b25aa9e4fd3e9a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717767"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Software-update catalogussen beheren in updates Publisher

*Van toepassing op: System Center Updates Publisher*

Gebruik de **werk ruimte** **catalogussen** om software-update catalogussen te beheren. Dit omvat het toevoegen van nieuwe catalogi, het beheren van bestaande catalogus abonnementen en het importeren van informatie over de updates van een catalogus naar de update-opslag plaats van Publisher.

Software-update cataloguss bevatten informatie over gerelateerde updates die zijn gemaakt door andere organisaties dan micro soft. Andere organisaties omvatten uw eigen organisatie en software leveranciers van derden die hun catalogussen bij micro soft hebben geregistreerd. Geregistreerde catalogi van software leveranciers worden *partner catalogi*genoemd. Catalogi die u maakt en die niet bij micro soft zijn geregistreerd, worden *gebruikers* catalogi genoemd.

## <a name="add-software-update-catalogs"></a>Software-update catalogussen toevoegen
U moet een Update catalogus toevoegen aan updates Publisher voordat u de updates die deze bevat, kunt beheren. Wanneer u een catalogus toevoegt, updates Publisher:
-   Hiermee maakt u een abonnement op die catalogus, zodat deze kan controleren op updates voor die catalogus.
-   Voegt de catalogus toe aan een lijst in het venster **mijn software-update-catalogi** van de **werk ruimte Catalogs**.  

Informatie over elke geabonneerde catalogus is beschikbaar in de-console. De informatie bevat de download-URL of-locatie, de naam van het bedrijf of de organisatie die de catalogus heeft gemaakt en de laatste keer dat deze werd geïmporteerd of gewijzigd.

Updates Publisher kan uw abonnementen automatisch controleren op wijzigingen wanneer het wordt gestart. Dit is geconfigureerd als een [geavanceerde optie](updates-publisher-options.md#advanced). Wanneer updates worden geconfigureerd, wordt in Publisher verwezen naar de download-URL of locatie-informatie voor het abonnement en wordt u gewaarschuwd wanneer er wijzigingen zijn aangebracht in de catalogus die zijn gemaakt sinds de laatste keer dat u deze hebt geïmporteerd in de opslag plaats.

Als u hand matig wilt controleren op een catalogus update, selecteert u de catalogus in de lijst **mijn Software-Update catalogus** en kiest u vervolgens **vernieuwen** in het lint.

Naast het toevoegen van catalogi en het weer geven van informatie over geabonneerde catalogi, kunt u het volgende doen:
-  **Bewerk** de gegevens voor *gebruikers* catalogi.
-  Een catalogus van updates Publisher **verwijderen** (verwijderen).
-  Updates uit een catalogus **importeren** in de update voor de Publisher-opslag plaats. Wanneer u updates importeert, importeert u alle updates die zijn opgenomen in die catalogus. U kunt de updates vervolgens weer geven in de werk ruimte updates, waar u vervolgens updates kunt selecteren en publiceren op de update server.

> [!NOTE]   
> Als u een catalogus verwijdert uit updates, worden de updates in de catalogus verwijderd uit de opslag plaats. Dit heeft geen invloed op de updates die u op de update server hebt gepubliceerd. Zie niet- [referentie software-updates laten verlopen](updates-publisher-options.md#expire-unreferenced-software-updates)om updates te verwijderen van uw update server die zich niet meer in uw opslag plaats bevinden.

## <a name="manage-update-catalogs"></a>Update catalogussen beheren
U kunt de lijst catalogi weer geven die u hebt geïmporteerd in het venster **mijn software-update-catalogi** van de **werk ruimte catalogussen**. In deze werk ruimte kunt u het volgende doen:

-   **Een partner catalogus toevoegen:** Gebruik een van de volgende opties om nieuwe partner catalogi te vinden:

    -   Ga in de-console naar**overzicht**van **updates-werk ruimte** > . In het venster **aan** de slag kiest u **catalogussen met partner software-updates toevoegen**.

    -   Ga in de-console naar **catalogussen werkruimte** > **Mijn catalogi**. Klik vervolgens in het lint op **catalogus toevoegen**.

-   **Een gebruikers catalogus toevoegen:** Ga in de-console naar **catalogussen werkruimte** > **Mijn catalogi**. Klik vervolgens in het lint op **catalogus toevoegen**. Naast de locatie van het CAB-bestand moet u een uitgever, naam en beschrijving opgeven om de catalogus te identificeren.


-   **Controleren op updates voor catalogi:** Selecteer een of meer catalogi en kies vervolgens **vernieuwen** in het lint.

-   **Een gebruikers catalogus bewerken:** Selecteer een *gebruikers* catalogus en kies vervolgens **bewerken** in het lint. U kunt vervolgens de door de gebruiker gedefinieerde eigenschappen wijzigen.

-   **Catalogussen verwijderen:** Selecteer een of meer catalogussen en kies vervolgens **verwijderen** in het lint. Hiermee worden de catalogus, uw abonnement en de updates uit deze catalogussen verwijderd uit de opslag plaats van de uitgever van updates.

-   **Updates van een catalogus toevoegen aan de opslag plaats**: Kies **importeren** in het lint om de wizard **catalogus importeren** te starten. Zie [updates importeren](#import-updates) voor meer informatie

## <a name="import-updates"></a>Updates importeren
Wanneer u een catalogus importeert, worden de updates vanuit die catalogus toegevoegd aan de update-opslag plaats van de uitgever. Nadat de updates zijn geïmporteerd, kunt u ze naar de update server publiceren om ze beschikbaar te maken voor beheerde apparaten.

### <a name="to-import-updates"></a>Updates importeren
1. Als u de wizard **catalogus importeren** wilt starten, kiest u **importeren** in het lint in een van de volgende werk ruimten:

   -   Werk ruimte catalogi

   -   Werk ruimte updates

2. Selecteer op de pagina **type import** een of meer catalogussen die u hebt toegevoegd aan updates Publisher of geef een pad op naar een catalogus die u nog niet hebt toegevoegd als een abonnement. Kies **volgende** om het scherm samen vatting weer te geven en klik als u klaar bent op **volgende** om het importeren te starten.

3. Controleer in het venster **beveiligings waarschuwing – catalogus validatie** het catalogus certificaat en wanneer u klaar bent, op **accepteren** om de updates te importeren.

   > [!CAUTION]
   > Alleen updates accepteren van uitgevers die u vertrouwt. Software-updates van uitgevers die niet worden vertrouwd, kunnen schadelijk zijn voor client computers bij het scannen op updates.
   > 
   >  Als u een uitgever niet meer vertrouwt, verwijdert u deze uitgever uit de lijst met vertrouwde uitgevers. Meer informatie over het accepteren van catalogi vindt u **in het** dialoog venster **beveiligings waarschuwing-catalogus validatie** .

   Als u ervoor kiest om altijd catalogussen van een uitgever te accepteren, wordt die uitgever toegevoegd aan de [lijst met vertrouwde uitgevers](updates-publisher-options.md#trusted-publishers). U kunt deze lijst bekijken en bewerken als update voor de Publisher-optie.

4. Bij het importeren wordt het importeren van een update overgeslagen wanneer de update al in de opslag plaats is en een van de volgende voor waarden waar is:

   -   De update is niet gewijzigd ten opzichte van de laatste keer dat deze is geïmporteerd.

   -   De update is bewerkt en heeft een nieuwe digitale hash. Als u een update bewerkt, voor komt u dat een nieuwe update het origineel overschrijft, waardoor de wijzigingen die u mogelijk hebt geïmplementeerd, worden overschreven.

5. Controleer op de pagina **bevestiging** de resultaten van het importeren.

6. Klik op **sluiten** om de wizard te volt ooien. U kunt nu de updates voor deze catalogus weer geven in de werk ruimte updates.

## <a name="next-steps"></a>Volgende stappen
Nadat u updates hebt geïmporteerd, omvatten algemene acties:
-   [Updates beheren](manage-updates-with-updates-publisher.md) om ze te bundelen, toe te wijzen en te implementeren op de update server.
-   [Regels voor toepasselijkheid maken](updates-publisher-applicability-rules.md) om te helpen bepalen wanneer updates worden geïmplementeerd op de update server.
