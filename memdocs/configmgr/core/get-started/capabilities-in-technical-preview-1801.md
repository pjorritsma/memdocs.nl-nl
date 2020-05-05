---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1801 voor Configuration Manager.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e1e83126748596d9d631caa85506f7b236bf4a76
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074211"
---
# <a name="capabilities-in-technical-preview-1801-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1801 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1801. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. 

Bekijk de [technische preview voor Configuration Manager](technical-preview.md) voordat u deze versie van de Technical Preview installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Bekende problemen in deze technische preview:**
- **Bijwerken naar een nieuwe preview-versie mislukt wanneer u een site server in de passieve modus hebt**. Als u een [primaire site server in de passieve modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)hebt, moet u de site server van de passieve modus verwijderen voordat u de nieuwe preview-versie bijwerkt. U kunt de site server van de passieve modus opnieuw installeren nadat de update door de site is voltooid.

  De site server van de passieve modus verwijderen:
  1. Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **site configuratie** > **servers en site systeem rollen**en selecteer vervolgens de site server passieve modus.
  2. Klik in het deel venster **site systeem rollen** met de rechter muisknop op de **site** serverrol en kies vervolgens **rol verwijderen**.
  3. Klik met de rechter muisknop op de site server in de passieve modus en kies **verwijderen**.
  4. Nadat de installatie van de site server ongedaan is gemaakt, start u de service **CONFIGURATION_MANAGER_UPDATE**opnieuw op de actieve primaire site server.
  <!--sms 489412-->


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Gefaseerde implementaties maken
<!-- 1357405 -->
Met gefaseerde implementaties wordt een gecoördineerde, geordende implementatie van software geautomatiseerd zonder dat er meerdere implementaties worden gemaakt. In deze Technical Preview-versie kan de gefaseerde implementatie wizard worden uitgevoerd voor taken reeksen in de-beheer console. Implementaties worden echter niet gemaakt. 

### <a name="try-it-out"></a>Probeer het nu!  
  Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.
 
**Een gefaseerde implementatie voor een takenreeks maken** </br>
1. Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer **taken reeksen**.
2. Klik met de rechter muisknop op een bestaande taken reeks en selecteer **gefaseerde implementatie maken**. 
3. Geef op het tabblad **Algemeen** de gefaseerde implementatie een naam, beschrijving (optioneel) en selecteer **automatisch standaard pilot-en productie fasen maken**. 
4. Vul de velden **test verzameling** en **productie verzameling** in. Selecteer **Volgende**.
5. Kies op het tabblad **instellingen** één optie voor elk van de plannings instellingen en selecteer **volgende** als u klaar bent. 
6. Bewerk op het tabblad **fasen** de gewenste fasen en klik vervolgens op **volgende**.
7. Bevestig uw selecties op het tabblad **samen vatting** en klik vervolgens op **volgende** om door te gaan.

## <a name="co-management-reporting"></a>Rapportage voor co-beheer
<!-- 1356648 -->
Als u de mogelijkheden voor [co-beheer](../../comanage/overview.md) gebruikt, kunt u nu een dash board weer geven met informatie over co-beheer in uw omgeving. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw **Upgradegereedheid**uit en selecteer het dash board voor **co-beheer** . Het dash board bevat de volgende tegels:
- **Gezamenlijk beheerde apparaten**: het percentage apparaten in uw omgeving dat u hebt ingeschakeld voor co-beheer
- **OS-distributie**: de uitsplitsing van besturings systemen (OS) op versie. In deze grafiek wordt gebruikgemaakt van de volgende groeperingen:
  - Windows 7 & 8. x
  - Windows 10 lager dan 1709
  - Windows 10 1709 en hoger
    > [!NOTE] 
    > Windows 10, versie 1709 en hoger is een vereiste voor co-beheer
- **Status van co-beheer**: de uitsplitsing van het slagen of mislukken van het apparaat in de volgende categorieën:
   - Geslaagd, hybride Azure AD toegevoegd
   - Geslaagd, lid van Azure AD
   - Fout: de automatische inschrijving is mislukt
- **Werkbelasting overgang**: een staaf diagram met het aantal apparaten dat u hebt overgezet naar Microsoft intune voor de drie beschik bare werk belastingen: 
   - Nalevingsbeleid
   - Toegang tot bronnen
   - Windows Update voor Bedrijven

### <a name="prerequisites"></a>Vereisten
- Op de computer waarop de Configuration Manager-console wordt uitgevoerd, is Internet Explorer 9 of hoger vereist.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Evaluatie planning van verbeteringen in automatische implementatie regel
<!-- 1357133 -->
Op basis van uw [feedback voor gebruikers Voice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling)kunt u nu de evaluatie van de automatische implementatie regel (ADR) plannen om te worden gecompenseerd vanaf een basis dag. Bijvoorbeeld: een verschuiving van twee dagen na de tweede dinsdag van de maand evalueert de regel op donderdag. 

### <a name="try-it-out"></a>Probeer het nu!  
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt. <br/>

**Een aangepaste planning maken waarbij de offset wordt geëvalueerd en afgeleid van een basis dag** </br>
1.  Vouw in de werk ruimte **software bibliotheek** het knoop punt **software-updates**uit en selecteer **regels voor automatische implementatie**.
2. Klik met de rechter muisknop op **regels voor automatische implementatie** en kies **regel voor automatische implementatie maken**. 
3. Volg de aanwijzingen om de tabbladen **Algemeen**, **implementatie-instellingen**en **software-updates** te volt ooien. 
4. Op het tabblad **evaluatie schema** selecteert u **de regel volgens een schema uitvoeren** en **aanpassen**.
5. Voor het aangepaste schema selecteert u **maandelijks** en plaatst u de basis op een dag, bijvoorbeeld de tweede dinsdag. 
6. Controleer de **Offset (dagen)** en het aantal dagen voor de offset en klik vervolgens op **OK** .  
7. Voltooi de rest van de **wizard regel voor automatische implementatie maken**. 



## <a name="reassign-distribution-point"></a>Distributie punt opnieuw toewijzen
<!-- 1306937 -->
Veel klanten hebben grote Configuration Manager-infra structuren en verlaagt de primaire of secundaire sites om hun omgeving te vereenvoudigen. Ze moeten nog steeds distributie punten op filiaal locaties bewaren voor het leveren van inhoud aan beheerde clients. Deze distributie punten bevatten vaak meerdere terabytes of meer inhoud. Deze inhoud is in bepaalde tijd en netwerk bandbreedte gedistribueerd om naar deze externe servers te distribueren. 

Met deze functie kunt u een distributie punt opnieuw toewijzen aan een andere primaire site zonder de inhoud opnieuw te distribueren. Met deze actie wordt de site systeem toewijzing bijgewerkt en wordt alle inhoud op de server bewaard. Als u meerdere distributie punten opnieuw wilt toewijzen, voert u deze actie eerst op één distributie punt uit en gaat u door met de extra servers een voor een.

> [!IMPORTANT]
> De site systeem server kan alleen de distributiepuntrol hosten. Als de site systeem server als host fungeert voor een andere Configuration Manager serverrol, zoals het status migratie punt, kunt u het distributie punt niet opnieuw toewijzen. U kunt een Cloud distributiepunt niet opnieuw toewijzen. 

Deze optie werkt niet met deze release vanwege de technische preview-limiet van één primaire site. Bekijk het scenario en verzend vervolgens **feedback** vanuit het tabblad **Start** van het lint, met betrekking tot de mogelijkheden van deze actie.
1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **distributie punten** .
2. Klik met de rechter muisknop op het doel distributiepunt en selecteer **distributie punt opnieuw toewijzen**. 
  ![Distributie punt opnieuw toewijzen](media/1306937-reassign-dp.png)
3. Selecteer de site server en de site code waaraan u dit distributie punt opnieuw wilt toewijzen. 
  ![Een site server selecteren](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Verbeteringen in de hardware-inventarisatie
<!-- 1357389 -->
Voor nieuwe klassen kunnen teken reeks lengten groter dan 255 tekens worden opgegeven voor hardware-inventarisatie-eigenschappen die geen sleutels zijn.

### <a name="try-it-out"></a>Probeer het nu!  
Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.<br/>

1. Klik in de werk ruimte **beheer** op **client instellingen** en selecteer een instelling voor het client apparaat om te bewerken. Klik met de rechter muisknop op **Eigenschappen**. 
2. Selecteer **hardware-inventaris**, vervolgens **klassen instellen**en **toevoegen**.
3. Klik op de knop **verbinding maken** .
4. Vul de **computer naam**, de **WMI-naam ruimte**, het selectie vakje **recursief** in als dat nodig is. Geef indien nodig referenties op om verbinding te maken. Klik op **verbinding maken** om de naam ruimte klassen weer te geven.
5. Selecteer een nieuwe klasse en klik vervolgens op **bewerken**.
6. Wijzig de **lengte** van ten minste één eigenschap die een teken reeks is, behalve de sleutel, die groter is dan 255. Klik op **OK**. 
7. Zorg ervoor dat de bewerkte eigenschap is geselecteerd voor **hardware-inventaris klasse toevoegen** en klik op **OK**. 
8. Verzamel hardware-inventaris met de zojuist toegevoegde klasse met een eigenschap die groter is dan 255 tekens. 



## <a name="improvements-to-client-settings-for-software-center"></a>Verbeteringen aan client instellingen voor Software Center
<!-- 1351224 & 1355146 -->
In deze versie van de Technical Preview zijn er verbeteringen aangebracht in de aanpassing van software Center in de client instellingen. 

1. De client instellingen voor Software Center hebben nu een knop **aanpassen** .
2. Er is een voor beeld toegevoegd om te laten zien hoe de banner van het Software Center eruit ziet.<!--1351224-->
    - Als er geen logo is geselecteerd, worden in het voor beeld de tekst en kleur van het bedrijfs naam weer gegeven.
    - Als er een logo is geselecteerd, toont het voor beeld de tekst van het logo en de bedrijfs naam.  
3.  Niet- **goedgekeurde toepassingen verbergen in Software Center** is een nieuwe instelling voor Software Center. Wanneer deze optie is ingeschakeld, worden gebruikers beschik bare toepassingen die goed keuring vereisen, verborgen in Software Center.<!--1355146-->

### <a name="try-it-out"></a>Probeer het nu!  
 Probeer de taken uit te voeren. Vervolgens verzendt u **feedback** vanaf het tabblad **Start** van het lint zodat wij weten hoe dit werkt.

1. Klik op **client instellingen**in de werk ruimte **beheer** . Selecteer een instelling voor het client apparaat die u wilt bewerken. Klik er met de rechter muisknop op en selecteer vervolgens **Eigenschappen** en vervolgens **Software Center**.
2.  Klik op de knop **aanpassen** . Probeer de verschillende aanpassings instellingen, inclusief de preview-versie.
3. Schakel de instelling niet- **goedgekeurde toepassingen verbergen in Software Center in**. Bekijk de wijzigingen in Software Center. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Nieuwe instellingen voor Windows Defender Application Guard
<!-- 1356256 -->
Voor apparaten met Windows 10 versie 1709 en hoger zijn er twee nieuwe instellingen voor de interactie van hosts voor [Windows Defender Application Guard](../../protect/deploy-use/create-deploy-application-guard-policy.md). 
1. Websites kunnen toegang krijgen tot de virtuele grafische processor van de host. 
2. Bestanden die in de container worden gedownload, kunnen op de host worden bewaard. </br>



## <a name="improvements-to-run-scripts"></a>Verbeteringen voor het uitvoeren van scripts
<!-- 1236459 -->
Met de [functie **scripts uitvoeren** ](../../apps/deploy-use/create-deploy-scripts.md) hebt u nu de mogelijkheid om ondertekende Power shell-scripts te importeren en uit te voeren. 
- Om de script integriteit te hand haven, moeten ondertekende scripts worden geïmporteerd in plaats van kopiëren/plakken te gebruiken. 
- Geïmporteerde ondertekende scripts kunnen niet worden bewerkt na het importeren.
    
>[!IMPORTANT]
>In deze Technical Preview zijn er twee tijdelijke beperkingen.
>- Scripts kunnen alleen worden geïmporteerd in de functie scripts uitvoeren en kunnen niet rechtstreeks vanuit de-console worden bewerkt.
>- Scripts die zijn geïmporteerd met een niet-Unicode-code ring, worden mogelijk niet correct weer gegeven in de console. Het script wordt nog steeds uitgevoerd zoals oorspronkelijk is geschreven.





## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    
