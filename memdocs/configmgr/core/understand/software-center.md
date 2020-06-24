---
title: Gebruikershandleiding van Software Center
titleSuffix: Configuration Manager
description: Meer informatie over de functies en functionaliteit van software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715424"
---
# <a name="software-center-user-guide"></a>Gebruikershandleiding van Software Center

*Van toepassing op: Configuration Manager (huidige vertakking)*

De IT-beheerder van uw organisatie gebruikt software Center voor het installeren van toepassingen, software-updates en het upgraden van Windows. In deze gebruikers handleiding wordt de functionaliteit van software Center uitgelegd voor gebruikers van de computer.

Software Center wordt automatisch geïnstalleerd op Windows-apparaten die worden beheerd door uw IT-organisatie. Zie [Software Center openen](#bkmk_open)om aan de slag te gaan.

Algemene opmerkingen over Software Center-functionaliteit:

- In dit artikel worden de nieuwste functies van software Center beschreven. Als uw organisatie een oudere, maar nog steeds ondersteunde versie van software Center gebruikt, zijn niet alle functies beschikbaar. Neem contact op met uw IT-beheerder voor meer informatie.

- De IT-beheerder kan sommige aspecten van software Center uitschakelen. Uw specifieke ervaring kan variëren.

- Als meerdere gebruikers tegelijkertijd een apparaat gebruiken, is de gebruiker met de laagste sessie-ID de enige voor het weer geven van alle beschik bare implementaties in Software Center. Bijvoorbeeld meerdere gebruikers in een extern bureau blad-omgeving. Gebruikers met een hogere sessie-id kunnen sommige implementaties niet zien in Software Center. Gebruikers met een hogere sessie-id kunnen bijvoorbeeld geïmplementeerde toepassingen zien, maar niet geïmplementeerde pakketten of taken reeksen. Ondertussen wordt de gebruiker met de laagste sessie-ID alle geïmplementeerde toepassingen, pakketten en taken reeksen weer geven. Op het tabblad **gebruikers** van Windows taak beheer worden alle gebruikers en hun sessie-id's weer gegeven.

- Uw IT-beheerder kan de kleur van software Center wijzigen en het logo van uw organisatie toevoegen.

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Software Center openen

Software Center wordt automatisch geïnstalleerd op Windows-apparaten die worden beheerd door uw IT-organisatie. Voor de eenvoudigste methode om software Center te starten op een Windows 10-computer, drukt u op **Start** en typt u `Software Center` . Mogelijk hoeft u niet de volledige teken reeks voor Windows te typen om het beste resultaat te vinden.

:::image type="content" source="media/start-menu-software-center.png" alt-text="Beste overeenkomst Software Center in het menu Start":::

Als u wilt navigeren in het menu Start, gaat u naar de groep **micro soft Endpoint Manager** voor het pictogram **Software Center** .

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Pictogrammen start menu van micro soft Endpoint Manager":::

> [!NOTE]
> Het bovenstaande pad naar het start menu is voor versies van november 2019 (versie 1910) of hoger. In eerdere versies is de mapnaam **micro soft System Center**.

Als u Software Center niet kunt vinden in het menu Start, neemt u contact op met uw IT-beheerder.

## <a name="applications"></a>Toepassingen

:::image type="content" source="media/software-center-apps.png" alt-text="Tabblad Software Center-toepassingen" lightbox="media/software-center-apps.png":::

Selecteer het tabblad **toepassingen** (1) om toepassingen te zoeken en te installeren die uw IT-beheerder voor u of op deze computer implementeert.

- **Alle** (2): hier worden alle beschik bare toepassingen weer gegeven die u kunt installeren.

- **Vereist** (3): uw IT-beheerder dwingt deze toepassingen af. Als u een van deze toepassingen verwijdert, wordt dit door Software Center opnieuw geïnstalleerd.

- **Filters** (4): uw IT-beheerder kan categorieën van toepassingen maken. Indien beschikbaar selecteert u de vervolg keuzelijst om de weer gave te filteren op alleen de toepassingen in een specifieke categorie. Selecteer **Alles** om alle toepassingen weer te geven.

- **Sorteren op** (5): de lijst met toepassingen opnieuw rangschikken. Deze lijst wordt standaard gesorteerd op de **meest recente**. Recent beschik bare toepassingen worden weer gegeven met een **nieuwe** banner die zeven dagen zichtbaar is.

- **Search** (6): u kunt nog steeds niet vinden wat u zoekt? Voer tref woorden in het zoekvak in om te zoeken naar!

- Scha kelen tussen de weer gave (7): Selecteer de pictogrammen om de weer gave te scha kelen tussen de lijst weergave en de tegel weergave. De lijst toepassingen wordt standaard weer gegeven als grafische tegels.

|Pictogram|Weergave|Beschrijving|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|**Modus voor meervoudige selectie**|Installeer meer dan één toepassing per keer. Zie voor meer informatie [installeren van meerdere toepassingen](#install-multiple-applications).|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|**Lijstweergave**|In deze weer gave worden het toepassings pictogram, de naam, de uitgever, de versie en de status weer gegeven.|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|**Tegel weergave**|De IT-beheerder kan de pictogrammen aanpassen. Onder elke tegel worden de toepassings naam, de uitgever en de versie weer gegeven.|

### <a name="install-an-application"></a>Een toepassing installeren

Selecteer een toepassing in de lijst om er meer informatie over te zien. Selecteer **installeren** om deze te installeren. Als er al een app is geïnstalleerd, kunt u de optie **verwijderen**.

Voor sommige apps is mogelijk goed keuring vereist voordat ze worden geïnstalleerd.

- Wanneer u het probeert te installeren, kunt u een opmerking invoeren en de app vervolgens **aanvragen** .

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="Aanvraag voor installatie van software Center-app voor goed keuring":::

- Software Center toont de aanvraag geschiedenis en u kunt de aanvraag annuleren.

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="Installatie van software Center-app aangevraagd":::

- Wanneer een beheerder uw aanvraag goedkeurt, kunt u de app installeren. Als u een ogen blik geduld, installeert software Center de app automatisch tijdens uw niet-kantoor uren.

  :::image type="content" source="media/software-center-app-approved.png" alt-text="Installatie van software Center-App goedgekeurd":::

### <a name="install-multiple-applications"></a>Meerdere toepassingen installeren

<!-- 1357126 -->
U kunt meer dan één toepassing tegelijk installeren in plaats van te wachten totdat deze is voltooid voordat u begint met de volgende. De geselecteerde apps moeten worden gekwalificeerd:

- De app is zichtbaar voor u
- De app wordt niet al gedownload of geïnstalleerd
- Uw IT-beheerder heeft geen goed keuring nodig om de app te installeren

Meer dan één toepassing tegelijk installeren:

1. Selecteer het pictogram voor meervoudige selectie in de rechter bovenhoek::::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::

2. Selecteer twee of meer apps die u wilt installeren. Schakel het selectie vakje links van elke app in de lijst in.

3. Selecteer de knop **geselecteerde installatie** om te starten.

De apps worden zo normaal geïnstalleerd, maar nu na elkaar.

### <a name="share-an-application"></a>Een toepassing delen

Als u een koppeling naar een specifieke app wilt delen, selecteert u in de rechter bovenhoek het pictogram voor **delen** nadat u de app hebt geselecteerd::::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="Een app delen vanuit software Center":::

**Kopieer** de teken reeks en plak elders, zoals een e-mail bericht. Bijvoorbeeld `softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a`. Iemand anders in uw organisatie met Software Center kan de koppeling gebruiken om dezelfde toepassing te openen.

## <a name="updates"></a>Updates

:::image type="content" source="media/software-center-updates.png" alt-text="Tabblad Software Center-updates" lightbox="media/software-center-updates.png":::

Selecteer het tabblad **updates** (1) om software-updates te bekijken en te installeren die uw IT-beheerder op deze computer implementeert.  

- **Alle** (2): hier worden alle updates weer gegeven die u kunt installeren

- **Vereist** (3): uw IT-beheerder dwingt deze updates af.

- **Sorteren op** (4): de lijst met updates opnieuw rangschikken. Deze lijst wordt standaard gesorteerd op **toepassings naam: A tot Z**.

- **Zoeken** (5): u kunt nog steeds niet vinden wat u zoekt? Voer tref woorden in het zoekvak in om te zoeken naar!

Als u updates wilt installeren, selecteert u **Alles installeren** (6).

Als u alleen specifieke updates wilt installeren, selecteert u het pictogram om de modus voor meervoudige selectie in te voeren (7)::::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
Controleer de updates die moeten worden geïnstalleerd en selecteer vervolgens **installeren geselecteerd**.

## <a name="operating-systems"></a>Besturingssystemen

:::image type="content" source="media/software-center-os.png" alt-text="Tabblad Software Center-besturings systemen" lightbox="media/software-center-os.png":::

Selecteer het tabblad **besturings systemen** (1) om versies van Windows die door uw IT-beheerder op deze computer worden geïmplementeerd, weer te geven en te installeren.  

- **Alle** (2): toont alle Windows-versies die u kunt installeren

- **Vereist** (3): uw IT-beheerder dwingt deze upgrades af.

- **Sorteren op** (4): de lijst met updates opnieuw rangschikken. Deze lijst wordt standaard gesorteerd op **toepassings naam: A tot Z**.

- **Zoeken** (5): u kunt nog steeds niet vinden wat u zoekt? Voer tref woorden in het zoekvak in om te zoeken naar!

## <a name="installation-status"></a>Installatie status

Selecteer het tabblad **installatie status** om de status van toepassingen weer te geven. Mogelijk ziet u de volgende statussen:

- **Geïnstalleerd**: Software Center heeft deze toepassing al geïnstalleerd op deze computer.

- **Downloaden**: Software Center downloadt de software die op deze computer moet worden geïnstalleerd.

- **Mislukt**: Software Center kan de software niet installeren.

- **Gepland voor installatie na**: hier ziet u de datum en tijd van het volgende onderhouds venster van het apparaat om aanstaande software te installeren. Onderhouds Vensters worden gedefinieerd door de IT-beheerder.<!--1358131-->

  - De status kan worden weer gegeven op het tabblad **alle** en **gepland** .

  - U kunt vóór de tijd van het onderhouds venster installeren door de knop **nu installeren** te selecteren.

## <a name="device-compliance"></a>Apparaatcompatibiliteit

Selecteer het **tabblad apparaatcompatibiliteit om de** nalevings status van deze computer weer te geven.

Selecteer **naleving controleren** om de instellingen van dit apparaat te evalueren op basis van het beveiligings beleid dat door uw IT-beheerder is gedefinieerd.

## <a name="options"></a>Opties

Selecteer het tabblad **Opties** om aanvullende instellingen voor deze computer weer te geven.

### <a name="work-information"></a>Werk gegevens

Geef het aantal uren dat u normaal gesp roken werk op. Uw IT-beheerder kan software-installaties buiten uw kantoor uren plannen. Laat elke dag ten minste vier uur voor systeem onderhouds taken. Uw IT-beheerder kan nog steeds essentiële toepassingen en software-updates installeren tijdens kantoor uren.

- Selecteer het eerste en laatste uur dat u deze computer gebruikt. Deze waarden zijn standaard van **5:00 uur** tot **10:00 uur**.

- Selecteer de dagen van de week waarop u deze computer doorgaans gebruikt. Standaard selecteert Software Center alleen de week dagen.

Geef op of u deze computer regel matig gebruikt om uw werk uit te voeren. De beheerder kan automatisch toepassingen installeren of aanvullende toepassingen beschikbaar maken op primaire computers.<!--3485366--> Als de computer die u gebruikt een primaire computer is, selecteert **u deze computer regel matig gebruiken om mijn werk uit te voeren**.

### <a name="power-management"></a>Energiebeheer

De IT-beheerder kan beleids regels voor energie beheer instellen. Deze beleids regels helpen uw organisatie bij het besparen van de elektriciteit wanneer deze computer niet in gebruik is.

Als u deze computer wilt uitsluiten van dit beleid, selecteert u **geen energie-instellingen van mijn IT-afdeling op deze computer Toep assen**. Standaard is deze instelling uitgeschakeld en worden energie-instellingen toegepast op de computer.

### <a name="computer-maintenance"></a>Computer onderhoud

Geef op hoe software Center wijzigingen in software vóór de deadline moet Toep assen.

- **Vereiste software automatisch installeren of verwijderen en de computer opnieuw opstarten buiten de opgegeven kantoor uren**: deze instelling is standaard uitgeschakeld.

- **Software Center-activiteiten onderbreken wanneer mijn computer zich in de presentatie modus bevindt**: deze instelling is standaard ingeschakeld.

Wanneer u de IT-beheerder opdracht geeft, selecteert u **synchronisatie beleid**. Deze computer controleert de servers op alle nieuwe, zoals toepassingen, software-updates of besturings systemen.

### <a name="remote-control"></a>Afstandsbediening

Geef de instellingen voor externe toegang en beheer op afstand voor uw computer op.

**Instellingen voor externe toegang van uw IT-afdeling gebruiken**: uw IT-afdeling definieert standaard de instellingen om u op afstand te helpen. De andere instellingen in deze sectie tonen de status van de instellingen die uw IT-afdeling definieert. Als u instellingen wilt wijzigen, schakelt u eerst deze optie uit.

- **Toegestaan niveau voor externe toegang**
  - **Externe toegang niet toestaan**: IT-beheerders kunnen niet op afstand toegang krijgen tot deze computer om u te helpen.
  - **Alleen weer geven**: een IT-beheerder kan uw scherm alleen op afstand weer geven.
  - **Volledig**: een IT-beheerder kan deze computer op afstand beheren. Deze instelling is de standaard optie.

- **Beheer op afstand van deze computer door beheerders toestaan wanneer ik afwezig ben**. Deze instelling is standaard **Ja** .

- **Wanneer een beheerder deze computer op afstand probeert te beheren**
  - **Elke keer om toestemming vragen**: deze instelling is de standaard optie.
  - **Niet om toestemming vragen**

- **Het volgende weer geven tijdens beheer op afstand**: deze visuele meldingen zijn standaard ingeschakeld om u te laten weten dat een beheerder op afstand toegang heeft tot het apparaat.
  - **Status pictogram in het systeemvak**
  - **Een sessie verbindings balk op het bureau blad**

- **Geluid afspelen**: deze hoorbare melding laat u weten dat een beheerder op afstand toegang heeft tot het apparaat.
  - **Wanneer de sessie begint en eindigt**: deze instelling is de standaard optie.
  - **Herhaaldelijk tijdens sessie**
  - **Nooit**

## <a name="custom-tabs"></a>Aangepaste tabbladen

De IT-beheerder kan de standaard tabbladen verwijderen of extra tabbladen toevoegen aan software Center. Aangepaste tabbladen worden benoemd door uw beheerder en ze openen een website die door de beheerder is opgegeven. Het is bijvoorbeeld mogelijk dat u een tabblad met de naam ' Help Desk ' hebt waarmee de website van de Help Desk van uw IT-organisatie wordt geopend. <!--1358132-->

## <a name="more-information-for-it-administrators"></a>Meer informatie voor IT-beheerders

Meer informatie is beschikbaar voor IT-beheerders bij het plannen en configureren van software Center in de volgende artikelen:

- [Software Center plannen](../../apps/plan-design/plan-for-software-center.md)
- [Client instellingen voor Software Center](../clients/deploy/about-client-settings.md#software-center)
- [Meldingen over opnieuw starten van apparaat](../clients/deploy/device-restart-notifications.md)
- [Inleiding op beheer op afstand](../clients/manage/remote-control/introduction-to-remote-control.md)
