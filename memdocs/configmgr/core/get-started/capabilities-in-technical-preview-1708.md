---
title: Technical Preview 1708
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1708 voor Configuration Manager.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ab5cc83cc8e7bb51477d84a50f18d4f6b73f286d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721330"
---
# <a name="capabilities-in-technical-preview-1708-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1708 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1708. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md) om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bekende problemen in deze technische preview:**
- **Update voor preview versie 1708 mislukt wanneer u een site server in de passieve modus hebt**. Wanneer u de preview-versie 1706 of 1707 uitvoert en een [primaire site server in de passieve modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)hebt, moet u de site server van de passieve modus verwijderen voordat u uw preview-site kunt bijwerken naar versie 1708. U kunt de site server van de passieve modus opnieuw installeren nadat versie 1708 van de site is uitgevoerd.

  De site server van de passieve modus verwijderen:
  1. Ga in de-console naar **beheer** > **overzicht** > **site configuratie** > **servers en site systeem rollen**en selecteer vervolgens de site server passieve modus.
  2. Klik in het deel venster **site systeem rollen** met de rechter muisknop op de **site** serverrol en kies vervolgens **rol verwijderen**.
  3. Klik met de rechter muisknop op de site server in de passieve modus en kies **verwijderen**.
  4. Nadat de installatie van de site server ongedaan is gemaakt, start u de service **CONFIGURATION_MANAGER_UPDATE**opnieuw op de actieve primaire site server.




**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Verbeteringen voor het opgeven van script parameters wanneer u Power shell-scripts van Configuration Manager implementeert
<!-- 1236459 -->

Vanuit Configuration Manager 1706 kunt u [Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console](../../apps/deploy-use/create-deploy-scripts.md).

In [Technical Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)hebben we de mogelijkheid uitgebreid om para meters uit het script te Configuration Manager lezen.

In deze Technical Preview hebben we de mogelijkheid van script parameters uitgebreid om te detecteren welke para meters verplicht zijn en welke optioneel zijn, en wordt u gevraagd deze in te voeren.

### <a name="try-it-out"></a>Probeer het nu!

1. Volg de instructies om [Power shell-scripts te maken en uit te voeren vanuit de Configuration Manager-console](../../apps/deploy-use/create-deploy-scripts.md).
2. Kies op de pagina nieuwe **script parameters** van de **wizard script maken**een para meter en bewerk vervolgens de waarden.
De wizard geeft weer welke para meters verplicht zijn en welke optioneel zijn.
4. Wanneer u klaar bent met het bewerken van de para meters, voltooit u de wizard.

Wanneer het script wordt uitgevoerd, worden alle parameter waarden gebruikt die u hebt geconfigureerd. Als u geen verplichte para meter hebt geconfigureerd, wordt de eind gebruiker gevraagd de para meter op te geven wanneer het script wordt uitgevoerd.

## <a name="management-insights"></a>Beheerinzichten
<!-- 1353967 -->
U kunt nu inzicht krijgen in de huidige status van uw omgeving op basis van de analyse van gegevens in de site database. Inzichten helpt u uw omgeving beter te begrijpen en actie te ondernemen op basis van het inzicht. Bekijk beheer inzichten in de Configuration Manager-console op **beheer** > **beheer inzichten** > **alle inzichten**. In deze release zijn de volgende inzichten nu beschikbaar:

- **Toepassingen zonder implementaties**: hier wordt een lijst weer gegeven met de toepassingen in uw omgeving die geen actieve implementaties hebben. Zo kunt u ongebruikte toepassingen vinden en verwijderen om de lijst met toepassingen die in de-console worden weer gegeven, te vereenvoudigen.
- **Lege verzamelingen**: bevat een lijst met de verzamelingen in uw omgeving die geen leden hebben. U kunt deze verzamelingen verwijderen om de lijst met verzamelingen te vereenvoudigen die worden weer gegeven bij het implementeren van objecten, bijvoorbeeld.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Computers opnieuw opstarten via de Configuration Manager-console   
<!-- 1356283 -->
Vanaf deze release kunt u de Configuration Manager-console gebruiken om client apparaten te identificeren waarvoor opnieuw moet worden opgestart en vervolgens een client meldings actie te gebruiken om ze opnieuw te starten.

Als u apparaten wilt identificeren die opnieuw moeten worden opgestart, gaat u naar **activa en nalevings** > **apparaten** en selecteert u een verzameling met apparaten die mogelijk opnieuw moeten worden opgestart. Nadat u een verzameling hebt geselecteerd, kunt u de status van elk apparaat in het detail venster weer geven in een nieuwe kolom met de naam **opnieuw opstarten in behandeling**. Elk apparaat heeft de waarde **Ja**of **Nee**.

De client melding maken om een apparaat opnieuw op te starten:
1. Zoek het apparaat dat u opnieuw wilt starten in het knoop punt apparaten van de-console.
2. Klik met de rechter muisknop op het apparaat, selecteer **client melding**en selecteer vervolgens **opnieuw opstarten**. Hiermee opent u een informatie venster over het opnieuw opstarten. Klik op **OK** om de aanvraag opnieuw te starten te bevestigen.

Wanneer de melding door een client wordt ontvangen, wordt een meldings venster voor **Software Center** geopend om de gebruiker op de hoogte te stellen van de herstart. Standaard wordt het opnieuw opstarten na 90 minuten uitgevoerd. U kunt de tijd voor opnieuw opstarten wijzigen door [client instellingen](../clients/deploy/configure-client-settings.md)te configureren. Instellingen voor het gedrag voor opnieuw opstarten vindt u op het tabblad [computer opnieuw opstarten](../clients/deploy/about-client-settings.md#computer-restart) van de standaard instellingen.


### <a name="try-it-out"></a>Probeer het nu!
Voer de volgende taken uit en stuur ons **feedback** via het tabblad **Start** van het lint om ons te laten weten hoe het werkt:
1. Een app implementeren of bijwerken op een apparaat dat vereist dat het apparaat opnieuw wordt opgestart om de installatie te volt ooien.
2. Zoek het apparaat in het knoop punt **activa en nalevings** > **apparaten** van de console en bevestig dat **Ja** in de kolom **wachtend op opnieuw opstarten** wordt weer gegeven. Het kan Maxi maal 20 minuten duren voordat de status voor opnieuw opstarten wordt weer gegeven in de console.
3. Controleer het apparaat om te bevestigen dat de melding van het software centrum wordt geopend en of het apparaat opnieuw is opgestart.


## <a name="software-center-customization"></a>Aanpassing van software Center
<!-- 1351224 -->
U kunt huisstijl elementen voor ondernemingen toevoegen en de zicht baarheid van tabbladen in Software Center opgeven. U kunt uw specifieke bedrijfs naam voor Software Center toevoegen, een kleuren thema voor het configureren van software Centers instellen, een bedrijfs logo instellen en de zicht bare tabbladen voor client apparaten instellen.

### <a name="customize-software-center"></a>Software Center aanpassen

Software Center wijzigen:

1. Kies in de **Configuration Manager** -console de optie **beheer** > **client instellingen**. Klik op het exemplaar van de gewenste client instelling.
2. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.
3. Kies in het dialoog venster **standaard instellingen** het onderdeel **Software Center**.
4. Selecteer **Ja** als u de **nieuwe instellingen wilt selecteren om bedrijfs gegevens** op te geven om de aanpassings instellingen voor uw software Center in te scha kelen.
5. Typ de **naam**van uw bedrijf.
6. Selecteer uw **kleuren schema voor Software Center**.
7. Klik op **Bladeren** om naar uw logo voor Software Center te navigeren. Het logo moet een JPEG-of PNG-bestand zijn van 400 x 100 pixels met een maximale grootte van 750 KB.
8. Selecteer **Ja** als u tabbladen zichtbaar wilt maken in het Software Center voor client apparaten. Ten minste één tabblad moet zichtbaar zijn:

    -  Tabblad toepassingen inschakelen
    -  Tabblad updates inschakelen
    -  Tabblad besturings systemen inschakelen
    -  Tabblad installatie status inschakelen
    -  Het tabblad apparaatcompatibiliteit inschakelen
    -  Tabblad Opties inschakelen

### <a name="next-steps"></a>Volgende stappen

Zie [Inleiding tot toepassings beheer](../../apps/understand/introduction-to-application-management.md)voor meer informatie over toepassings beheer in Configuration Manager.
