---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1711 voor Configuration Manager.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e6f8ed1562392899b46a082bf8f64872c7e1b67d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721288"
---
# <a name="capabilities-in-technical-preview-1711-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1711 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1711. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md) om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bekende problemen in deze technische preview:**
- **Ondersteuning voor Windows 10, versie 1709 (ook wel bekend als de update voor het najaar van makers)**.  Vanaf deze Windows-versie bevat Windows Media meerdere edities. Bij het configureren van een taken reeks voor het gebruik van een upgrade pakket voor een besturings systeem of een installatie kopie van een besturings systeem, moet u ervoor zorgen dat u een [editie selecteert die wordt ondersteund voor gebruik door Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Bijwerken naar een nieuwe preview-versie mislukt wanneer u een site server in de passieve modus hebt**. Wanneer u een preview-versie met een [primaire site server in de passieve modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)uitvoert, moet u de site server van de passieve modus verwijderen voordat u uw preview-site kunt bijwerken naar deze nieuwe preview-versie. U kunt de site server van de passieve modus opnieuw installeren nadat de update door de site is voltooid.

  De site server van de passieve modus verwijderen:
  1. Ga in de-console naar **beheer** > **overzicht** > **site configuratie** > **servers en site systeem rollen**en selecteer vervolgens de site server passieve modus.
  2. Klik in het deel venster **site systeem rollen** met de rechter muisknop op de **site** serverrol en kies vervolgens **rol verwijderen**.
  3. Klik met de rechter muisknop op de site server in de passieve modus en kies **verwijderen**.
  4. Nadat de installatie van de site server ongedaan is gemaakt, start u de service **CONFIGURATION_MANAGER_UPDATE**opnieuw op de actieve primaire site server.

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Verbeteringen voor het uitvoeren van taken reeks
<!-- 1261338 -->

Met deze technische preview wordt de stap voor het uitvoeren van taken reeksen verbeterd. Verbeteringen zijn onder andere de volgende items:

- Ondersteuning voor alle implementatie scenario's voor besturings systemen vanuit software Center, PXE en media.
- Verbeteringen aan console acties, zoals kopiëren, importeren, exporteren en waarschuwen tijdens het verwijderen van een object.
- Ondersteuning voor de wizard **inhoud maken voor bereiding** .
- Integratie met verificatie op basis van implementatie.
- De stap taken reeks uitvoeren kan nu worden gebruikt op meerdere niveaus van taken reeksen, niet alleen voor één bovenliggende/onderliggende relatie. Relaties met meerdere niveaus verg Roten de complexiteit, dus wees voorzichtig. Deze relaties worden nog steeds gecontroleerd op kring verwijzingen.

### <a name="try-it-out"></a>Probeer het nu!  

Voer de volgende taken uit en stuur ons **feedback** via het tabblad **Start** van het lint om ons te laten weten hoe het werkt:

1. Klik in de taken reeks editor op **toevoegen**, selecteer **Algemeen**en klik op **taken reeks uitvoeren**.
2. Klik op **Bladeren** om de onderliggende taken reeks te selecteren.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Gebruikers interactie toestaan bij het installeren van een toepassing <!-- 1356976 -->

Met deze preview-versie kunt u een eind gebruiker in staat stellen om te communiceren met een installatie van een toepassing tijdens het uitvoeren van de taken reeks. Voer bijvoorbeeld een installatie proces uit dat de eind gebruiker vraagt om verschillende opties. Voor sommige installatie Programma's van toepassingen kunnen geen gebruikers prompts worden gestilte of het installatie proces kan specifieke configuratie waarden vereisen die alleen voor de gebruiker bekend zijn. Met deze functie kunt u deze installatie scenario's afhandelen.

### <a name="try-it-out"></a>Probeer het nu!

Voer de volgende taken uit en verzend vervolgens **feedback** vanaf het tabblad **Start** van het lint om ons te laten weten hoe het werkt:

1.  Een toepassing maken of bewerken. Zie [toepassingen maken met Configuration Manager](../../apps/deploy-use/create-applications.md)voor meer informatie.

    a. Kies het tabblad **gebruikers ervaring** in de **eigenschappen van\*het Windows Installer (MSI-bestand)**.

    b. Selecteer **installeren voor systeem** voor **installatie gedrag**.

    c. Geef aan of **er een gebruiker is aangemeld** voor de **aanmeldings vereiste**.

    d. Selecteer **normaal** voor **zicht baarheid van installatie programma**. U kunt kiezen uit drie opties: **geminimaliseerd**, **normaal**of **gemaximaliseerd**.

    e. Selecteer de optie **gebruikers toestaan om te communiceren met de installatie van het programma** .

2.  Maak of bewerk een taken reeks om de toepassing te installeren met behulp van de stap **toepassing installeren** . Zie voor meer informatie [toepassing installeren](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication) in de [taken reeks stappen](../../osd/understand/task-sequence-steps.md).

    a. De taken reeks Imaging na de stap Windows en Configuration Manager.

    b. In-place upgrade taken reeks in de verwerkings groep.

3.  Implementeer de taken reeks op een-client.
4.  Installeer de taken reeks vanuit software Center.

Tijdens de taken reeks wordt de toepassings installatie-interface weer gegeven op het doel apparaat van de eind gebruiker. De voortgang van de taken reeks wordt onderbroken totdat de eind gebruiker de installatie werk stroom van de toepassing voltooit.

### <a name="install-using-the-wizard"></a>Installeren met behulp van de wizard

U kunt deze functie ook gebruiken bij het implementeren van een app met behulp van de wizard.

1. Een toepassing maken of bewerken.
2. Implementeer de toepassing naar een-client.
3. Installeer de toepassing vanuit software Center. De installatie-interface van de toepassing moet worden weer gegeven. De eind gebruiker moet de wizard voor het installeren van de toepassing volgen en de toepassing wordt geïnstalleerd.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    
