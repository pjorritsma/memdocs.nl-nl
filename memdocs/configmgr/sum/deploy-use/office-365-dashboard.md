---
title: Office 365-dash board voor client beheer
titleSuffix: Configuration Manager
description: Office 365-client gegevens controleren via het Office 365 client management-dash board
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: 7e6ed38d0f4217bfc70d3ddb196527d421e5d7c1
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110386"
---
# <a name="office-365-client-management-dashboard"></a>Office 365-dash board voor client beheer

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Note]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds verwijzingen naar de oude naam in de Configuration Manager-console en de ondersteunende documentatie terwijl de-console wordt bijgewerkt.

Vanaf Configuration Manager versie 1802 kunt u de gegevens van Office 365-clients bekijken via het Office 365-client beheer dash board. Het Office 365-dash board voor client beheer geeft een lijst van relevante apparaten weer wanneer secties van de grafiek worden geselecteerd. <!--1357281 -->

## <a name="prerequisites"></a>Vereisten

### <a name="enable-hardware-inventory"></a>Hardware-inventaris inschakelen

De gegevens die worden weer gegeven in het Office 365-dash board voor client beheer, zijn afkomstig van hardware-inventarisatie. Schakel de hardware-inventarisatie in en selecteer de hardware-inventaris klasse **Office 365 ProPlus-configuraties** voor gegevens die in het dash board moeten worden weer gegeven.
 
1. Hardware-inventaris inschakelen, als deze nog niet is ingeschakeld. Zie [hardware-inventaris configureren](../../core/clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie.
2. Navigeer in de Configuration Manager-console naar **Administration** > **instellingen** > van de client voor beheer clients**standaard instellingen voor clients**.  
3. Klik op **Eigenschappen** in het tabblad **Start**, in de groep **Eigenschappen**.  
4. Klik in het dialoogvenster **Standaardclientinstellingen** op **Hardware-inventarisatie**.  
5. Klik in de lijst **Apparaatinstellingen** op **Klassen instellen**.  
6. Selecteer in het dialoog venster **hardware-inventaris klassen** de optie **Office 365 ProPlus-configuraties**.  
7. Klik op **OK** om uw wijzigingen op te slaan en het dialoogvenster **Hardware-inventarisklassen** te sluiten.

Het Office 365-dash board voor client beheer begint met het weer geven van gegevens als hardware-inventaris wordt gerapporteerd.

### <a name="connectivity-for-top-level-site-server"></a>Connectiviteit voor site server op het hoogste niveau

*(Geïntroduceerd in versie 1906 als een vereiste)*

De site server op het hoogste niveau moet toegang hebben tot het volgende eind punt om het gereedheids bestand te downloaden:

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> Internet connectiviteit is niet vereist voor de client apparaten voor een van deze scenario's.

### <a name="enable-data-collection-for-office-365-proplus"></a>Gegevens verzameling inschakelen voor Office 365 ProPlus

*(Geïntroduceerd in versie 1910 als een vereiste)*

Vanaf versie 1910 moet u het verzamelen van gegevens voor Office 365 ProPlus instellen om informatie in te vullen in het **office 365 ProPlus-prototype en het status dashboard**. De gegevens worden opgeslagen in de site database van Configuration Manager en worden niet naar micro soft verzonden.

Deze gegevens verschillen van de diagnostische gegevens, die worden beschreven in [Diagnostische gegevens die vanuit Office 365 ProPlus naar micro soft worden verzonden](https://docs.microsoft.com/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft).

U kunt het verzamelen van gegevens inschakelen door gebruik te maken van groepsbeleid of door het REGI ster te bewerken.

#### <a name="enable-data-collection-from-group-policy"></a>Gegevens verzameling van groepsbeleid inschakelen

1. Down load de meest recente [beheer sjabloon bestanden van het micro soft Download centrum](https://www.microsoft.com/download/details.aspx?id=49030).
2. Schakel de beleids instelling **telemetrie-gegevens verzameling** inschakelen `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard`in.
    - U kunt ook de beleids instelling Toep assen met de [Office-Cloud beleids service](https://docs.microsoft.com/DeployOffice/overview-office-cloud-policy-service).
    - De beleids instelling wordt ook gebruikt door het Office-telemetrie-dash board, dat u niet hoeft te implementeren voor het verzamelen van gegevens.

#### <a name="enable-data-collection-from-the-registry"></a>Gegevens verzameling inschakelen vanuit het REGI ster

De onderstaande opdracht is een voor beeld van het inschakelen van het verzamelen van gegevens uit het REGI ster:

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Het Office 365-dash board voor client beheer weer geven

Als u het Office 365-dash board voor client beheer wilt weer geven in de Configuration Manager-console, gaat u naar **software bibliotheek** > **Overview** > **Office 365 client management**. Aan de bovenkant van het dash board gebruikt u de vervolg keuzelijst **verzameling** om de dashboard gegevens te filteren op leden van een bepaalde verzameling. Vanaf Configuration Manager versie 1802 wordt in het Office 365 client management-dash board een lijst met relevante apparaten weer gegeven wanneer de secties van de grafiek worden geselecteerd.

Het Office 365-dash board voor client beheer bevat grafieken voor de volgende informatie:

- Aantal Office 365-clients
- Office 365-client versies
- Office 365-client talen
- Office 365-client kanalen Zie [overzicht van update kanalen voor Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus)voor meer informatie.


## <a name="integration-for-office-365-proplus-readiness"></a><a name="bkmk_o365_readiness"></a>Integratie voor Office 365 ProPlus gereedheid
<!--3735402-->
Vanaf Configuration Manager versie 1902 kunt u het dash board gebruiken om apparaten met hoge betrouw baarheid te identificeren die gereed zijn voor een upgrade naar Office 365 ProPlus. Deze integratie biedt inzicht in mogelijke compatibiliteits problemen met Office-invoeg toepassingen en macro's in uw omgeving. Gebruik vervolgens Configuration Manager om Office te implementeren op apparaten die klaar zijn voor gebruik.

Het Office 365-dash board voor client beheer bevat een nieuwe tegel, **Office 365 ProPlus Upgradegereedheid**. Deze tegel is een staaf diagram met apparaten in de volgende statussen:
- Niet beoordeeld
- Gereed voor de upgrade
- Beoordeling vereist

Selecteer een status om in te zoomen naar een lijst met apparaten. Dit gereedheids rapport bevat meer details over apparaten. Het bevat kolommen voor de compatibiliteits status van zowel Office-invoeg toepassingen als macro's.

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Vereisten voor de integratie van Office 365 ProPlus-gereedheid

- Hardware-inventaris in client instellingen inschakelen. Zie de sectie [vereisten](#prerequisites) voor meer informatie.  

- Het apparaat moet zijn verbonden met het Office Content Delivery Network (CDN) om een gereedheids bestand voor invoeg toepassingen te downloaden. Zie [Content Delivery Networks](https://docs.microsoft.com/office365/enterprise/content-delivery-networks)(Engelstalig) voor meer informatie. Als het apparaat dit bestand niet kan downloaden, moet de status van de invoeg toepassingen worden *gecontroleerd*.  

    > [!Note]  
    > Er worden geen gegevens naar micro soft verzonden voor deze functie.  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a>Gedetailleerde macro gereedheid

De scan agent zoekt standaard naar de lijst met recent gebruikte bestanden (MRU) op elk apparaat. Hiermee worden de bestanden in deze lijst geteld die macro's ondersteunen. Deze bestanden bevatten de volgende typen:
- Office-bestands indelingen met macro's, zoals Excel-werkmappen met macro's (. XLSM) of Word-document met macro's (. DOCM)  
- Oudere Office-indelingen die niet aangeven of er macro-inhoud is. Bijvoorbeeld een Excel 97-2003-werkmap (. xls).

Als u meer gedetailleerde informatie over de compatibiliteit van macro's nodig hebt, implementeert u de **Readiness Toolkit voor Office** om de code in de macro bestanden te analyseren. Er wordt gecontroleerd of er mogelijke compatibiliteits problemen zijn. Het bestand maakt bijvoorbeeld gebruik van een functie die is gewijzigd in een recentere versie van Office. Nadat u de Readiness Toolkit voor Office hebt uitgevoerd en de optie hebt geselecteerd voor de **meest recent gebruikte Office-documenten en geïnstalleerde invoeg toepassingen op deze computer**, of `-mru` als u de vlag gebruikt op de opdracht regel, kunnen de resultaten worden opgehaald door de hardware-inventaris agent van Configuration Manager. Deze extra gegevens verbeteren de berekening van de gereedheid van het apparaat. Zie voor meer informatie [de Readiness Toolkit voor Office gebruiken voor het beoordelen van de compatibiliteit van toepassingen voor office 365 ProPlus](https://aka.ms/readinesstoolkit).

Houd er rekening mee dat de Readiness Toolkit niet op elk doel apparaat hoeft te worden geïnstalleerd om de scan uit te voeren. U kunt de voor beeld-opdracht regel optie hieronder gebruiken om elk gewenst apparaat te scannen.  De uitvoer vlag is vereist, maar de bestanden worden niet gebruikt voor het genereren van de resultaten in het dash board, zodat er een geldige locatie kan worden geselecteerd.

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

Zie [gereedheids informatie voor meerdere gebruikers in een onderneming ophalen](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise)voor meer informatie.

## <a name="office-365-proplus-upgrade-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a>Office 365 ProPlus upgrade gereedheids dashboard

*(Geïntroduceerd in versie 1906)*

<!--4021125-->
Om u te helpen bepalen welke apparaten klaar zijn om te upgraden naar Office 365 ProPlus, is er een gereedheids dashboard vanaf versie 1906. Het bevat de **Office 365 ProPlus upgrade Readiness** -tegel die is uitgebracht in Configuration Manager huidige branch versie 1902. De volgende nieuwe tegels in dit dash board helpen u bij het evalueren van de Office-invoeg toepassing en macro gereedheid:

- Implementatie
- Gereedheid van apparaat
- Gereedheid voor invoeg toepassing
- Ondersteunings instructies voor invoeg toepassingen
- Belangrijkste invoeg toepassingen per aantal versies
- Aantal apparaten met macro's
- Gereedheid voor macro's
- Macro-adviseurs

De volgende video is een sessie van Ignite 2019, die meer informatie bevat:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Aanbevolen procedures voor compatibiliteits beoordeling en Microsoft Office 365 ProPlus-upgrades met behulp van Office-gereedheid in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>Het Office 365 ProPlus upgrade Readiness dash board gebruiken

Nadat u hebt gecontroleerd of aan de [vereisten wordt voldaan](#prerequisites), gebruikt u de volgende instructies voor het gebruik van het dash board:
 
1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** en vouw **Office 365 client management**uit.
1. Selecteer het knoop punt **Office 365 ProPlus Upgradegereedheid** .
1. Wijzig de **verzameling** en de **Office-architectuur** van het doel om de gegevens die in het dash board worden doorgestuurd, te wijzigen.

![Office 365 ProPlus upgrade gereedheids dashboard](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Office 365 ProPlus upgrade gereedheids dashboard](./media/4021125-office-365-to-add-ins.png)

![Office 365 ProPlus upgrade gereedheids dashboard](./media/4021125-office-365-macro-advisories.png)

### <a name="device-readiness-information"></a>Informatie over gereedheid van apparaat

Zodra de invoeg toepassing en de macro inventaris op elk apparaat worden geëvalueerd, worden de apparaten gegroepeerd op basis van de informatie. Apparaten waarvan de status is vermeld als **gereed voor de upgrade** , hebben waarschijnlijk geen compatibiliteits problemen.

Als u de categorie **gereed voor upgrades** in de grafiek selecteert, ziet u meer informatie over de apparaten in de beperkende verzameling. U kunt de lijst met apparaten bekijken, selecties maken op basis van uw bedrijfs vereisten en een nieuwe apparaat verzameling maken op basis van uw selectie. Gebruik uw nieuwe verzameling om Office 365 ProPlus met Configuration Manager te implementeren.

Apparaten die mogelijk kwetsbaar zijn voor compatibiliteits problemen, zijn gemarkeerd als **behoeften beoordeling**. Deze apparaten moeten mogelijk actie ondernemen voordat ze worden bijgewerkt naar Office 365 ProPlus. U kunt essentiële invoeg toepassingen bijvoorbeeld bijwerken naar een recentere versie.

### <a name="add-in-information"></a>Informatie van invoeg toepassing

 Op elk apparaat wordt een inventarisatie van alle geïnstalleerde invoeg toepassingen verzameld. De inventarisatie wordt vervolgens vergeleken met de informatie die micro soft heeft over de prestaties van de invoeg toepassing op Office 365 ProPlus. Als er een invoeg toepassing wordt gevonden die waarschijnlijk problemen veroorzaakt na de upgrade, worden alle apparaten met de invoeg toepassing gemarkeerd voor controle.

### <a name="macro-information"></a>Macro gegevens

Configuration Manager op elk apparaat de meest recent gebruikte bestanden bekijkt. Hiermee worden de bestanden in deze lijst geteld die macro's ondersteunen, met inbegrip van de volgende typen:

- Office-bestands indelingen met macro's.
- Oudere Office-indelingen, die niet aangeven of er macro-inhoud is.

Dit rapport kan worden gebruikt om te bepalen welke apparaten recent gebruikte bestanden hebben die macro's kunnen bevatten. De **Readiness Toolkit voor Office** kan vervolgens worden geïmplementeerd met behulp van Configuration Manager om apparaten te scannen waar meer gedetailleerde informatie nodig is, en om te controleren of er mogelijke compatibiliteits problemen zijn. Als het bestand bijvoorbeeld gebruikmaakt van een functie die is gewijzigd in een recentere versie van Office.

Zie voor meer informatie over het uitvoeren van de scan [gedetailleerde macro gereedheid](#bkmk_ort).

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a>Office 365 ProPlus pilot-en status dashboard
<!--4488272, 4488301-->
*(Geïntroduceerd in versie 1910)*

Vanaf versie 1910, het **office 365 ProPlus pilot en het status dashboard** , kunt u uw Office 365 ProPlus-implementatie plannen, testen en uitvoeren. Het dash board biedt status inzichten voor apparaten met Office 365 ProPlus om mogelijke problemen te identificeren die van invloed kunnen zijn op uw implementatie plannen. Het **Office 365 ProPlus-pilot-en status dashboard** biedt een aanbeveling voor pilot-apparaten op basis van de inventaris van invoeg toepassingen. De volgende tegels bevinden zich in het dash board:

- Pilot genereren
- Aanbevolen pilot-apparaten
- Pilot implementeren
- Apparaten die status gegevens verzenden
- Apparaten die niet voldoen aan de gezondheids doelen
- Invoeg toepassingen die niet voldoen aan de status
- Macro's die geen voldoen aan de gezondheids doelen

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>Het Office 365 ProPlus-pilot-en status dashboard gebruiken

Nadat u hebt gecontroleerd of aan de [vereisten wordt voldaan](#prerequisites), gebruikt u de volgende instructies voor het gebruik van het dash board:

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** en vouw **Office 365 client management**uit.
1. Selecteer het knoop punt **Office 365 pilot en Health** .

![Office 365 ProPlus pilot-en status dashboard](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>Pilot genereren

Genereer een test aanbeveling van een beperkende verzameling bij het klikken op een knop. Zodra de actie wordt gestart, wordt het berekenen van uw pilot verzameling door een achtergrond taak gestart. Uw beperkende verzameling moet ten minste één apparaat bevatten met een Office-versie die niet ProPlus is.

### <a name="recommended-pilot-devices"></a>Aanbevolen pilot-apparaten

**Aanbevolen pilot-apparaten** zijn een minimale set apparaten die alle geïnstalleerde invoeg toepassingen voor de beperkende verzameling voor het genereren van de pilot gebruiken. Inzoomen om een lijst met deze apparaten weer te geven. Gebruik vervolgens de Details om eventuele apparaten van de pilot uit te sluiten, indien nodig. Als al uw invoeg toepassingen aanwezig zijn op Office 365 ProPlus-apparaten, worden apparaten met deze invoeg toepassingen niet opgenomen in de berekening. Dit betekent ook dat u geen resultaten krijgt in uw test verzameling omdat al uw invoeg toepassingen zijn gedetecteerd op apparaten waarop Office 365 ProPlus is geïnstalleerd.

### <a name="deploy-pilot"></a>Pilot implementeren

Nadat u uw test apparaten hebt geaccepteerd, implementeert u Office 365 ProPlus naar de pilot verzameling met behulp van de wizard gefaseerde implementatie. Beheerders kunnen de pilot-en beperkende verzameling in de wizard definiëren voor het beheren van implementaties.

### <a name="health-data"></a>Status gegevens

Zodra Office 365 ProPlus is geïnstalleerd, schakelt u status gegevens in op uw test apparaten. Met de status gegevens krijgt u inzicht in welke invoeg toepassingen en macro's niet voldoen aan de status doelen. De **apparaten die gereed zijn voor het implementeren** van de grafiek, identificeren niet-pilot apparaten die gereed zijn voor implementatie met behulp van de status inzichten. Ontvang een telling van apparaten die status gegevens verzenden vanuit het diagram **apparaten verzenden** van de status.

### <a name="devices-not-meeting-health-goals"></a>Apparaten die niet voldoen aan de gezondheids doelen

In deze tegel vindt u een overzicht van apparaten met problemen met invoeg toepassingen, macro's of beide.

### <a name="add-ins-not-meeting-health-goals"></a>Invoeg toepassingen die niet voldoen aan de status

- Laad fouten: de invoeg toepassing is niet gestart.
- Crashes: de invoeg toepassing is mislukt tijdens de uitvoering ervan.
- Fout: er is een fout gerapporteerd door de invoeg toepassing.
- Meerdere problemen: de invoeg toepassing heeft meer dan een van de bovenstaande problemen.

### <a name="macros-not-meeting-health-goals"></a>Macro's die geen voldoen aan de gezondheids doelen

- Laad fouten: het document kan niet worden geladen.
- Runtime-fouten: er is een fout opgetreden tijdens het uitvoeren van de macro. Deze fouten kunnen afhankelijk zijn van de invoer en kunnen daarom niet altijd optreden.
- Compileer fouten: de macro is niet correct gecompileerd, zodat er geen poging wordt gedaan om uit te voeren.
- Meerdere problemen: de macro heeft meer dan een van de bovenstaande problemen.

> [!NOTE]
> De macro-inventarisatie wordt gevuld met gegevens van de Readiness Toolkit voor Office en recent gebruikte gegevens bestanden. De status van de macro wordt ingevuld op basis van de status gegevens. Vanwege de verschillende gegevens bronnen is het mogelijk dat de integriteits status van de macro moet worden **gecontroleerd** wanneer de inventarisatie van de macro **niet wordt gescand**. <!--5922845-->

### <a name="known-issues"></a>Bekende problemen

Er is een bekend probleem met de tegel **pilot implementeren** . Op dit moment kan deze niet worden gebruikt om te implementeren in een pilot. De tijdelijke oplossing is de bestaande werk stroom voor het implementeren van een toepassing met behulp van de wizard gefaseerde implementatie. <!--5525871-->

## <a name="next-steps"></a>Volgende stappen

[Office 365 ProPlus beheren met Configuration Manager](manage-office-365-proplus-updates.md)
