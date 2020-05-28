---
title: Externe acties met co-beheer
titleSuffix: Configuration Manager
description: Externe acties uitvoeren vanuit intune voor gezamenlijk beheerde apparaten
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075316"
---
# <a name="remote-actions-with-co-management"></a>Externe acties met co-beheer

U moet ervoor zorgen dat elk apparaat dat u beheert bereikbaar is, ongeacht waar het is, wanneer het verbinding maakt. U moet ook elke gebruiker een alles bieden wat ze nodig hebben om productief te blijven, terwijl u de apps en gegevens beveiligt. Met de acties die door intune worden ondersteund, kunt u deze kritieke functies op afstand oplossen.

In de volgende video worden de belangrijkste Program ma's voor Heidi Cheng en Senior Program Manager Danny Guillory voor het bespreken en uitvoeren van externe acties met co-beheer beschreven.

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Voordelen

Acties voor externe apparaten bieden u beheer besturings elementen op het apparaat zonder dat dit van invloed is op persoonlijke gegevens. Met deze acties voor externe apparaten kunt u het volgende doen: 
- Bedrijfs gegevens op verloren of gestolen apparaten verwijderen  
- De naam van een apparaat wijzigen  
- Apparaten opnieuw opstarten  
- Inventaris van apparaten controleren  
- Een apparaat op afstand beheren  
- Vooraf geïnstalleerde OEM-apps wissen met een nieuwe start opnieuw opstarten  
- Fabrieks instellingen terugzetten op een apparaat met Windows 10  

Deze functies zijn een belang rijke en eenvoudige manier om bedrijfs gegevens te beveiligen die op deze apparaten zijn opgeslagen, ongeacht of ze zich in een e-mail of OneDrive bevinden.

Zie [beschik bare externe acties](#available-remote-actions)voor meer informatie over deze acties. 



## <a name="case-studies"></a>Casestudy's

De Global Consulting Fiat Avanade maakt regel matig gebruik van externe acties voor het beheren van de apparaten die worden gebruikt door hun 30.000-werk nemers. In een [recente blog post](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/)is de CIO van Avanade de volgende genoteerd:

> *Onze onmiddellijke win van het gebruik van de intune-functionaliteit is de mogelijkheid om Windows op een computer op afstand opnieuw in te stellen. Dit is belang rijk voor het oplossen van verloren of gestolen computers, wat gebruikelijk is in onze uiterst mobiele* mede werkers. 
>  *Dit is de functionaliteit die anders in een aangepast ConfigMgr-pakket zou moeten worden gemaakt en onderhouden.*

Zie [beschik bare acties voor apparaten](../../intune/remote-actions/device-management.md#available-device-actions)voor meer informatie over het gebruik van deze externe acties.


## <a name="value-proposition"></a>Toegevoegde waarde

Wanneer een Configuration Manager-apparaat wordt beheerd door co-beheer, voegt het direct deze functies toe die Configuration Manager niet systeem eigen zijn. Nu kunt u een externe actie uitvoeren die wordt ondersteund door intune. 

Met co-beheer zijn de Configuration Manager-apparaten nu net zo hetzelfde als andere door intune beheerd apparaat. Ze hebben bijvoorbeeld een volledige aanwezigheid in de Cloud en u kunt deze bereiken zolang ze toegang hebben tot internet. U kunt al deze acties uitvoeren zonder dat u verder hoeft te doen om co-beheer in te scha kelen.

Omdat het proces voor automatische inschrijving transparant is voor de gebruiker, zijn er geen gevolgen voor de productiviteit. De gebruiker hoeft niets te doen.


### <a name="available-remote-actions"></a>Beschik bare externe acties

Gebruik deze externe acties van intune als u [co-beheer hebt ingeschakeld](how-to-enable.md) in Configuration Manager.

#### <a name="remove-devices"></a>Apparaten verwijderen
- **Buiten gebruik stellen**: met deze actie worden beheerde apps en gegevens (indien van toepassing), instellingen en e-mail profielen verwijderd die aan dat apparaat zijn toegewezen. Het apparaat wordt vervolgens verwijderd uit intune-beheer. Dit proces vindt plaats de volgende keer dat het apparaat wordt ingecheckt en ontvangt de actie extern buiten gebruik stellen. Met de functie buiten gebruik stellen blijven de persoonlijke gegevens van de gebruiker op het apparaat.  

- **Wissen**: met deze actie worden de fabrieks instellingen van een apparaat hersteld. Als u de optie voor het **behouden van de inschrijvings status en gebruikers account**kiest, worden de gebruikers gegevens bewaard. Anders wordt het station veilig gewist.  

- **Verwijderen**: als u apparaten wilt verwijderen uit intune op Azure Portal, verwijdert u deze uit het deel venster specifieke apparaten. De volgende keer dat het apparaat wordt ingecheckt, worden alle organisatie gegevens die erop zijn opgeslagen, verwijderd.  

Zie [apparaten verwijderen met wissen, buiten gebruik stellen of de registratie van het apparaat hand matig ongedaan maken](../../intune/remote-actions/devices-wipe.md)voor meer informatie.

#### <a name="selective-wipe"></a>Selectief wissen
<!--SCCMDocs issue 973-->
Wanneer u **selectief wissen**kiest voor apps, worden de app-gegevens van het bedrijf verwijderd zonder dat er persoonlijke gegevens worden verwijderd. Gebruik deze actie wanneer een apparaat wordt gerapporteerd als verloren of gestolen. 

Zie [informatie over het wissen van Bedrijfs gegevens uit door intune beheerde apps] (.. /.. /intune/apps/apps-selective-wipe.md.

#### <a name="sync"></a>Synchroniseren
Met apparaatactie **Synchroniseren** wordt het geselecteerde apparaat direct ingecheckt bij Intune. Wanneer een apparaat wordt ingecheckt, ontvangt het direct alle in behandeling zijnde acties of beleids regels die u hieraan hebt toegewezen.

Met deze functie kunt u toegewezen beleid meteen controleren en in het geval van problemen direct aanpassen, zonder dat u hoeft te wachten op de volgende geplande check-in.

Zie [apparaten synchroniseren voor het meest recente beleid en acties voor intune](../../intune/remote-actions/device-sync.md)voor meer informatie.

#### <a name="restart"></a>Opnieuw starten
De actie apparaat **opnieuw starten** veroorzaakt het apparaat dat u opnieuw wilt opstarten. Deze actie is handig wanneer het opnieuw opstarten in behandeling is, maar de gebruiker niet beschikbaar is.

Zie [apparaten op afstand opnieuw opstarten met intune](../../intune/remote-actions/device-restart.md)voor meer informatie.

#### <a name="fresh-start"></a>Nieuwe start
Met de actie **Nieuw start** apparaat worden alle apps verwijderd die zijn geïnstalleerd op een apparaat met Windows 10, versie 1703 of hoger. Nieuwe start helpt bij het verwijderen van vooraf geïnstalleerde (OEM) apps die doorgaans worden geïnstalleerd met een nieuw apparaat.

Als u ervoor kiest geen gebruikers gegevens te bewaren, herstelt het apparaat de out-of-Box-status. De registratie van Azure AD en MDM wordt ongedaan gemaakt.

Als u vooraf vastgestelde normen hebt met betrekking tot de apps die op het apparaat moeten zijn geïnstalleerd, elimineert deze actie de voor waarden die niet aan uw criteria voldoen.

Zie [Fresh Start gebruiken om Windows 10-apparaten opnieuw in te stellen met intune](../../intune/remote-actions/device-fresh-start.md)voor meer informatie. 

#### <a name="remote-control"></a>Extern beheer
Apparaten die worden beheerd door Intune kunnen extern worden beheerd met [TeamViewer](https://www.teamviewer.com/). Team Viewer is een programma van derden dat u afzonderlijk aanschaft.

Zie [Team Viewer gebruiken om intune-apparaten op afstand te beheren](../../intune/remote-actions/teamviewer-support.md)voor meer informatie.



## <a name="configure"></a>Configureren

Met uitzonde ring van beheer op afstand via Team Viewer, om te beginnen met het gebruik van deze acties voor externe apparaten in intune, hoeft u geen aanvullende instellingen te installeren nadat u [co-beheer hebt ingeschakeld](how-to-enable.md).

Zie [Team Viewer gebruiken voor het extern beheren van intune-apparaten](../../intune/remote-actions/teamviewer-support.md)voor meer informatie over het gebruik van Team Viewer voor beheer op afstand.
