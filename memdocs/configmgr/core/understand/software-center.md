---
title: Gebruikershandleiding van Software Center
titleSuffix: Configuration Manager
description: Meer informatie over de functies en functionaliteit van software Center
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: c4fa0819bf6427d93adf44a7b6284a8266e3a6a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722660"
---
# <a name="software-center-user-guide"></a>Gebruikershandleiding van Software Center

*Van toepassing op: Configuration Manager (huidige vertakking)*

De IT-beheerder van uw organisatie gebruikt software Center voor het installeren van toepassingen, software-updates en het upgraden van Windows. In deze gebruikers handleiding wordt de functionaliteit van software Center uitgelegd voor gebruikers van de computer.

Algemene opmerkingen over Software Center-functionaliteit:

- In dit artikel worden de nieuwste functies van software Center beschreven. Als uw organisatie een oudere, maar nog steeds ondersteunde versie van software Center gebruikt, zijn niet alle functies beschikbaar. Neem contact op met uw IT-beheerder voor meer informatie.

- De IT-beheerder kan sommige aspecten van software Center uitschakelen. Uw specifieke ervaring kan variëren.

- Als meerdere gebruikers tegelijkertijd gebruikmaken van een apparaat, kunt u via meerdere extern bureau blad-sessies zeggen dat de gebruiker met de laagste sessie-ID het enige is dat alle beschik bare implementaties in Software Center worden weer geven. Gebruikers met een hogere sessie-id kunnen sommige implementaties niet zien in Software Center. Gebruikers met een hogere sessie-id kunnen bijvoorbeeld geïmplementeerde toepassingen zien, maar niet geïmplementeerde pakketten of taken reeksen. Ondertussen wordt de gebruiker met de laagste sessie-ID alle geïmplementeerde toepassingen, pakketten en taken reeksen weer geven.

<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a>Software Center openen

Voor de eenvoudigste methode om software Center te starten op een Windows 10-computer **Start** , drukt u `Software Center`op Start en typt u. Mogelijk hoeft u niet de volledige teken reeks voor Windows te typen om het beste resultaat te vinden.

Als u navigeert naar het menu Start, gaat u naar de groep **micro soft Endpoint Manager** voor het pictogram **Software Center** .

![Pictogrammen start menu van micro soft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Het pad van het menu Start is gewijzigd in versie 1910. In versie 1906 en eerder is de mapnaam **micro soft System Center**. Wanneer u Configuration Manager bijwerkt naar versie 1910 of hoger, moet u ervoor zorgen dat u de interne documentatie die u onderhoudt, bijwerkt om deze nieuwe locatie op te nemen.

## <a name="applications"></a>Toepassingen

Selecteer het tabblad **toepassingen** om toepassingen te zoeken en te installeren die uw IT-beheerder voor u of op deze computer implementeert.

- **Alle**: hier worden alle toepassingen weer gegeven die u kunt installeren
- **Vereist**: uw IT-beheerder dwingt deze toepassingen af. Als u een van deze toepassingen verwijdert, wordt dit door Software Center opnieuw geïnstalleerd.
- **Filters**: uw IT-beheerder kan categorieën toepassingen maken. Indien beschikbaar selecteert u de vervolg keuzelijst om de weer gave te filteren op alleen de toepassingen in een specifieke categorie. Selecteer **Alles** om alle toepassingen weer te geven.
- **Sorteren op**: de lijst met toepassingen opnieuw rangschikken. Deze lijst wordt standaard gesorteerd op de **meest recente**. Recent beschik bare toepassingen worden weer gegeven met een **nieuwe** tag die 7 dagen zichtbaar is.
- **Zoeken**: u kunt nog steeds niet vinden wat u zoekt? Voer tref woorden in het zoekvak in om te zoeken naar!
- **De weer gave wijzigen**: Selecteer de pictogrammen om de weer gave te scha kelen tussen de lijst weergave en de tegel weergave. De lijst toepassingen wordt standaard weer gegeven als grafische tegels.
    - Tegel weergave: uw IT-beheerder kan de pictogrammen aanpassen. Onder elke tegel worden de toepassings naam, de uitgever en de versie weer gegeven.
    - Lijst weergave: in deze weer gave worden het toepassings pictogram, de naam, de uitgever, de versie en de status weer gegeven.

### <a name="install-multiple-applications"></a>Meerdere toepassingen installeren

<!-- 1357126 -->
U kunt meer dan één toepassing tegelijk installeren in plaats van te wachten totdat deze is voltooid voordat u begint met de volgende. Niet alle toepassingen komen in aanmerking:

- De app is zichtbaar voor u
- De app wordt niet al gedownload of geïnstalleerd
- Uw IT-beheerder heeft geen goed keuring nodig om de app te installeren

Meer dan één toepassing tegelijk installeren:

1. Als u de modus voor meervoudige selectie in de lijst weergave wilt invoeren, selecteert u het pictogram voor meervoudige selectie ![Pictogram Software Center multi-select](media/software-center-multi-select-apps.png) in de rechter bovenhoek.
2. Selecteer twee of meer apps die u wilt installeren door het selectie vakje links van de apps in de lijst in te scha kelen.
3. Selecteer de knop **geselecteerde installatie** .

De apps worden zo normaal geïnstalleerd, maar nu na elkaar.


## <a name="updates"></a>Updates

Selecteer het tabblad **updates** om software-updates te bekijken en te installeren die uw IT-beheerder op deze computer implementeert.  

- **Alle**: hier worden alle updates weer gegeven die u kunt installeren
- **Vereist**: uw IT-beheerder dwingt deze updates af.
- **Sorteren op**: rang Schik de lijst met updates opnieuw. Deze lijst wordt standaard gesorteerd op **toepassings naam: A tot Z**.

Als u updates wilt installeren, selecteert u **Alles installeren**.

Als u alleen specifieke updates wilt installeren, selecteert u het pictogram om de modus voor meervoudige selectie in te voeren. Controleer de updates die moeten worden geïnstalleerd en selecteer vervolgens **installeren geselecteerd**.


## <a name="operating-systems"></a>Besturingssystemen

Selecteer het tabblad **besturings systemen** om versies van Windows weer te geven en te installeren die door uw IT-beheerder op deze computer worden geïmplementeerd.  

- **Alle**: hier worden alle Windows-versies weer gegeven die u kunt installeren
- **Vereist**: uw IT-beheerder dwingt deze upgrades af.
- **Sorteren op**: rang Schik de lijst met updates opnieuw. Deze lijst wordt standaard gesorteerd op **toepassings naam: A tot Z**.


## <a name="installation-status"></a>Installatie status

Selecteer het tabblad **installatie status** om de status van toepassingen weer te geven. Mogelijk ziet u de volgende statussen:

- **Geïnstalleerd**: Software Center heeft deze toepassing al geïnstalleerd op deze computer.
- **Downloaden**: Software Center downloadt de software die op deze computer moet worden geïnstalleerd.
- **Mislukt**: er is een fout opgetreden in Software Center tijdens het installeren van de software.
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

- Selecteer de vervolg keuzelijst om de eerste en laatste uren te selecteren die u op deze computer gebruikt. Deze waarden zijn standaard van **5** tot **10 uur**

- Schakel het selectie vakje in naast de dagen van de week waarop u deze computer doorgaans gebruikt. Software Center selecteert standaard alleen de werk dagen.  

Geef op of u deze computer regel matig gebruikt om uw werk uit te voeren. De beheerder kan automatisch toepassingen installeren of aanvullende toepassingen beschikbaar maken op primaire computers. <!--3485366-->

- Selecteer **Ik wil deze computer regel matig gebruiken om mijn werk uit te voeren** als de computer die u gebruikt een primaire computer is.

### <a name="power-management"></a>Energiebeheer

De IT-beheerder kan beleids regels voor energie beheer instellen. Deze beleids regels helpen uw organisatie bij het besparen van de elektriciteit wanneer deze computer niet in gebruik is.

Als u deze computer wilt uitsluiten van dit beleid, schakelt u het selectie vakje **energie-instellingen van mijn IT-afdeling op deze computer niet Toep assen**. Deze instelling is standaard uitgeschakeld. de computer past energie-instellingen toe.

### <a name="computer-maintenance"></a>Computer onderhoud

Opgeven hoe software Center wijzigingen in software toepast vóór de deadline

- **Vereiste software automatisch installeren of verwijderen en de computer opnieuw opstarten buiten de opgegeven kantoor uren**: deze instelling is standaard uitgeschakeld.
- **Software Center-activiteiten onderbreken wanneer mijn computer zich in de presentatie modus bevindt**: deze instelling is standaard ingeschakeld.
- **Synchronisatie beleid**: Selecteer deze knop als u de IT-beheerder hierom vraagt. Deze computer controleert de servers op alle nieuwe, zoals toepassingen, software-updates of besturings systemen.

### <a name="remote-control"></a>Afstandsbediening

Instellingen voor externe toegang en beheer op afstand opgeven voor uw computer

- **Instellingen voor externe toegang van uw IT-afdeling gebruiken**: dit selectie vakje is standaard ingeschakeld.
- **Toegestaan niveau voor externe toegang**: Selecteer een van de volgende drie opties
    - **Externe toegang niet toestaan**
    - **Alleen weergeven**
    - **Volledig**: dit niveau is standaard ingeschakeld.
- **Beheer op afstand van deze computer door beheerders toestaan wanneer ik afwezig ben**. Deze instelling is standaard ingesteld op **Ja** .
- **Wanneer een beheerder deze computer op afstand probeert te beheren**: deze instelling heeft twee opties
    - **Elke keer om toestemming vragen**: deze optie is standaard geselecteerd.
    - **Niet om toestemming vragen**
- **Het volgende weer geven tijdens beheer op afstand**: beide opties zijn standaard geselecteerd
    - **Status pictogram in het systeemvak**
    - **Een sessie verbindings balk op het bureau blad**
- **Geluid afspelen**: deze instelling heeft drie opties
    - **Wanneer de sessie begint en eindigt**: deze instelling is standaard geselecteerd.
    - **Herhaaldelijk tijdens sessie**
    - **Nooit**

    Zie [Inleiding tot beheer op afstand](../clients/manage/remote-control/introduction-to-remote-control.md) voor meer informatie
    

## <a name="custom-tab-in-software-center"></a>Aangepast tabblad in Software Center

De IT-beheerder heeft mogelijk een extra tabblad toegevoegd aan software Center. Dit tabblad wordt door uw beheerder aangeduid en leidt naar een website die ze opgeven. Het is bijvoorbeeld mogelijk dat u een tabblad met de naam ' Help Desk ' hebt die leidt naar de website van de Help Desk van uw organisatie. <!--1358132-->
