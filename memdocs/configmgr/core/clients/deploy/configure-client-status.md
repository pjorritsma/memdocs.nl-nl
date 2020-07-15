---
title: Client status configureren
titleSuffix: Configuration Manager
description: Selecteer client status instellingen in Configuration Manager.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a352e53a672f7fb47416214884fe7adf0fb829cc
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384907"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>De client status in Configuration Manager configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Configureer de client status instellingen van de site voordat u Configuration Manager-clients kunt bewaken en problemen wilt oplossen. Met deze instellingen geeft u de para meters op die de site gebruikt om-clients als inactief te markeren. Configureer ook opties om u te waarschuwen als client activiteit onder een opgegeven drempel waarde valt.

## <a name="configure-client-status"></a>Client status configureren

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer het knoop punt **client status** . Op het tabblad **Start** van het lint selecteert u **client status instellingen**in de groep **client status** .

1. Configureer de volgende instellingen:

    > [!NOTE]
    > Als een client niet voldoet aan een van de instellingen, markeert de site deze als inactief.

    - **Client beleids aanvragen gedurende de volgende dagen:** Geef op hoeveel dagen sinds de client beleid heeft aangevraagd van de site. De standaard waarde is `7` dagen.

      Vergelijk deze waarde met de instelling voor het **polling interval voor client beleid** in de **client beleids** groep van client instellingen. De standaard waarde is 60 minuten. Met andere woorden, een client moet elk uur de site controleren op beleid. Als er na een week geen beleid wordt aangevraagd, markeert de site dit als inactief.

    - **Heartbeat-detectie gedurende de volgende dagen:** Geef op hoeveel dagen geleden de client een heartbeat-detectie record naar de site heeft verzonden. De standaard waarde is `7` dagen.

      Vergelijk deze waarde met de planning voor de [heartbeat-detectie methode](../../servers/deploy/configure/about-discovery-methods.md). De site voert standaard eenmaal per week heartbeat-detectie uit.

    - **Hardware-inventarisatie gedurende de volgende dagen:** Geef het aantal dagen op sinds de client een hardware-inventarisatie record naar de site heeft verzonden. De standaard waarde is `7` dagen.

      Vergelijk deze waarde met de instelling voor de **Hardware-inventarisatie planning** in de **Hardware-inventarisatie** groep van client instellingen. De standaard waarde is zeven dagen.

    - **Software-inventarisatie gedurende de volgende dagen:** Geef het aantal dagen op sinds de client een software-inventarisatie record naar de site heeft verzonden. De standaard waarde is `7` dagen.

      Vergelijk deze waarde met de instelling **software-inventarisatie en bestands verzameling** in de **software-inventarisatie** groep van client instellingen. De standaard waarde is zeven dagen.

    - **Status berichten gedurende de volgende dagen:** Geef op hoeveel dagen geleden de client status berichten naar de site heeft verzonden. De standaard waarde is `7` dagen. De client kan status berichten verzenden voor verschillende soorten activiteiten, zoals het uitvoeren van een taken reeks. De site verwijdert oude status berichten als onderdeel van de onderhouds taak en **verwijdert verouderde status berichten**.

1. Geef de volgende waarde op om te bepalen hoelang de site geschiedenis gegevens van de client status houdt:

    - **Geschiedenis van client status bewaren gedurende het volgende aantal dagen:** De site houdt standaard informatie over de client status voor `31` dagen. Deze instelling heeft geen invloed op het gedrag van de client of de site. Dit is vergelijkbaar met een onderhouds taak voor de geschiedenis van de client status.

## <a name="configure-the-schedule"></a>De planning configureren

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** en selecteer het knoop punt **client status** . Selecteer op het tabblad **Start** van het lint in de groep **client status** de optie **Schedule client status update**.

1. Configureer het interval waarmee de client status moet worden bijgewerkt.

    > [!NOTE]
    > Wanneer u het schema voor client status updates wijzigt, wordt dit pas van kracht nadat de volgende geplande client status is bijgewerkt volgens het vorige schema.

## <a name="configure-alerts"></a>Waarschuwingen configureren

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **Apparaatsets** .

1. Selecteer de verzameling waarvoor u waarschuwingen wilt configureren. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.

    > [!NOTE]
    > U kunt geen waarschuwingen voor gebruikers verzamelingen configureren.

1. Ga naar het tabblad **waarschuwingen** en selecteer **toevoegen**.

   > [!TIP]
   > U kunt het tabblad **waarschuwingen** alleen weer geven als uw beveiligingsrol machtigingen heeft voor waarschuwingen.

    Kies de waarschuwingen die de site moet genereren voor de drempel waarden voor de client status en selecteer **OK**.

1. Selecteer elke client status waarschuwing in de lijst **voor waarden** van het tabblad **waarschuwingen** en geef vervolgens de volgende gegevens op:

    - **Naam van waarschuwing**: accepteer de standaard naam of voer een nieuwe naam in voor de waarschuwing.

    - **Ernst van waarschuwing**: Kies het waarschuwings niveau dat door de Configuration Manager-console wordt weer gegeven.

    - **Waarschuwing activeren**: Geef het drempel percentage voor de waarschuwing op.

## <a name="automatic-remediation-exclusion"></a>Uitsluiting van automatisch herstel

1. Open de REGI ster-editor op de client computer waarop u automatisch herstel wilt uitschakelen.

    > [!WARNING]
    > Als u de REGI ster-editor onjuist gebruikt, kunt u ernstige problemen veroorzaken waardoor u Windows opnieuw moet installeren. Micro soft kan niet garanderen dat u problemen kunt oplossen die het gevolg zijn van een onjuist gebruik van de REGI ster-editor. Gebruik het op eigen risico.

1. Navigeer naar de register sleutel **HKEY_LOCAL_MACHINE \software\microsoft\ccm\ccmeval**.

1. Wijzig de waarde voor de vermelding **NotifyOnly** :

    - `TRUE`: De client herstelt geen problemen die worden gevonden. De site waarschuwt u nog steeds in de werk ruimte **bewaking** over eventuele problemen met deze client.

    - `FALSE`: Dit is de standaard instelling. De client herstelt problemen automatisch wanneer deze worden gevonden en de site waarschuwt u in de werk ruimte **bewaking** .

Wanneer u clients installeert, kunt u deze uitsluiten van automatisch herstel met de **NotifyOnly** -installatie-eigenschap. Zie [over eigenschappen van client installatie](about-client-installation-properties.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Clients bewaken](../manage/monitor-clients.md)
