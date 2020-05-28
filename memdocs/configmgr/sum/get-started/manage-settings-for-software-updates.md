---
title: Instellingen voor software-updates beheren
titleSuffix: Configuration Manager
description: Meer informatie over de client instellingen die van toepassing zijn op software-updates op uw site nadat u het software-update punt hebt geïnstalleerd.
ms.date: 03/30/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0a2a45ff866ea02aacc83c42109c8cba4020ed4e
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906804"
---
#  <a name="manage-settings-for-software-updates"></a><a name="BKMK_ManageSUSettings"></a>Instellingen voor software-updates beheren  

*Van toepassing op: Configuration Manager (huidige vertakking)*

Nadat u software-updates in Configuration Manager hebt gesynchroniseerd, configureert en verifieert u de instellingen in de volgende secties.

##  <a name="client-settings-for-software-updates"></a><a name="BKMK_ClientSettings"></a>Client instellingen voor software-updates  
Wanneer u het software-updatepunt installeert, worden standaard software-updates ingeschakeld op clients en hebben de instellingen op de pagina **Software-updates** in de clientinstellingen de standaardwaarden. De client instellingen worden gebruikt voor de hele site en beïnvloeden wanneer software-updates worden gescand op naleving, en hoe en wanneer software-updates worden geïnstalleerd op client computers. Voordat u software-updates implementeert, controleert u of de client instellingen geschikt zijn voor software-updates op uw site.  

> [!IMPORTANT]  
>  De instelling **Software-updates op clients inschakelen** wordt standaard ingeschakeld. Als u deze instelling uitschakelt, verwijdert Configuration Manager de bestaande implementatie beleidsregels van de client.  

Zie [client instellingen configureren](../../core/clients/deploy/configure-client-settings.md)voor meer informatie over het configureren van client instellingen.  

Zie [over client instellingen](../../core/clients/deploy/about-client-settings.md)voor meer informatie over de client instellingen.  

##  <a name="group-policy-settings-for-software-updates"></a><a name="BKMK_GroupPolicy"></a>Groeps beleids instellingen voor software-updates  
Er zijn specifieke door Windows Update Agent (WUA) gebruikte groepsbeleidinstellingen op clientcomputers om verbinding te maken met WSUS die op het software-updatespunt wordt gebruikt. U kunt met deze groepsbeleidinstellingen ook de naleving van software-updates scannen en automatisch de software-updates en WUA bijwerken.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Lokaal beleid voor Locatie van Microsoft-updateservice in intranet  
Wanneer er een software-updatepunt voor een site is gemaakt, ontvangen clients een machinebeleid dat de servernaam van het software-updatepunt verstrekt en het lokale beleid **Locatie van Microsoft-updateservice in intranet opgeven** op de computer configureert. De WUA haalt de in de instelling **De updateservice in intranet instellen voor het detecteren van updates** opgegeven servernaam op, waarna deze verbinding maakt met deze server wanneer de scan voor compatibiliteit van software-updates wordt uitgevoerd. Wanneer het domeinbeleid voor de instelling **Locatie van Microsoft-updateservice in intranet** wordt gemaakt, wordt het lokale beleid overschreven en maakt de WUA mogelijk verbinding met een andere server dan die van het software-updatepunt. Wanneer dit gebeurt, scant de client mogelijk voor compatibiliteit van software-updates op basis van andere producten, classificaties en talen. Daarom dient u het Active Directory-beleid voor clientcomputers niet te configureren.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Ondertekende inhoud vanaf de locatie van de Microsoft-updateservice op een intranet toestaan  
U moet de groepsbeleidinstelling **Ondertekende inhoud toestaan van groepsbeleid voor locatie van Microsoft-updateservice in intranet** inschakelen voordat de WUA computers gaat scannen op software-updates die door System Center Updates Publisher zijn gemaakt en gepubliceerd. Wanneer de beleidinstelling is ingeschakeld, accepteert WUA via een intranetlocatie ontvangen software-updates, als de software-updates zijn ondertekend in het certificaatarchief **Vertrouwde uitgevers** op de lokale computer. Zie de [documentatiebibliotheek van Updates Publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10))voor meer informatie over de voor Updates Publisher 2011 vereiste groepsbeleidinstellingen.  

### <a name="automatic-updates-configuration"></a>Automatische updates configureren  
Met automatische updates kunt u beveiligingsupdates en andere belangrijke downloads ontvangen op clientcomputers. Automatische updates wordt geconfigureerd via de groepsbeleidinstelling **Automatische updates configureren** of via het configuratiescherm op de lokale computer. Wanneer Automatische updates is ingeschakeld, ontvangen clientcomputers updatemeldingen en downloaden en installeren de clientcomputers de vereiste updates, afhankelijk van de geconfigureerde instellingen, Wanneer Automatische updates tegelijk met software-updates wordt gebruikt, geeft elke clientcomputer mogelijk meldingspictogrammen en pop-upweergavemeldingen weer voor dezelfde update. Wanneer opnieuw opstarten is vereist, geeft elke clientcomputer mogelijk een dialoogvenster voor opnieuw opstarten weer voor dezelfde update.  

### <a name="self-update"></a>Automatische update  
Wanneer automatische updates is ingeschakeld op clientcomputers, voert de WUA een automatische update uit wanneer een nieuwere versie beschikbaar komt of wanneer er problemen zijn met een WUA-component. Wanneer Automatische updates niet is geconfigureerd of is uitgeschakeld en clientcomputers een eerdere versie van de WUA hebben, moeten de clientcomputers het WUA-installatiebestand uitvoeren.  

## <a name="software-updates-properties"></a>Eigenschappen van software-updates
De eigenschappen van software-updates bieden informatie over software-updates en gekoppelde inhoud. U kunt deze eigenschappen ook gebruiken om instellingen voor software-updates te configureren. Wanneer u de eigenschappen voor meerdere software-updates opent, worden alleen de tabbladen **Maximale uitvoeringstijd** en **Aangepaste ernst** weergegeven.   

Gebruik de volgende procedure om eigenschappen van software-updates te openen.  

#### <a name="to-open-software-update-properties"></a>Eigenschappen van software-updates openen  

1. Klik in de Configuration Manager-console op **Softwarebibliotheek**.  
2. Vouw in de werkruimte Softwarebibliotheek het knooppunt **Software-updates**uit en klik op **Alle software-updates**.  
3. Selecteer een of meer software-updates en klik vervolgens op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen** .  

   > [!NOTE]  
   >  In het knoop punt **alle software-updates** geeft Configuration Manager alleen de software-updates weer die de classificatie **kritiek** en **beveiliging** hebben en die in de afgelopen 30 dagen zijn uitgebracht.  

###  <a name="review-software-updates-information"></a><a name="BKMK_SoftwareUpdatesInformation"></a> Informatie over software-updates weergeven  
U kunt in de eigenschappen van software-updates gedetailleerde informatie over een software-update controleren. De gedetailleerde informatie wordt niet weergegeven wanneer u meer dan één software-update selecteert. In de volgende secties is de informatie beschreven die beschikbaar is voor de geselecteerde software-update.  

####  <a name="software-update-details"></a><a name="BKMK_SoftwareUpdateDetails"></a>Details van software-update  
Op het tabblad met **updatedetails** wordt de volgende overzichtsinformatie over de geselecteerde software-update weergegeven:  

- **Bulletin-id**: bevat de bulletin-id die aan beveiligingsupdates is gekoppeld. U kunt de details van het beveiligings Bulletin vinden door te zoeken op de Bulletin-ID op de webpagina [micro soft Security Response Center](https://portal.msrc.microsoft.com/) .  

> [!NOTE]
> De manier waarop micro soft documenten beveiligings updates wijzigt. Het vorige model gebruikte webpaginas van beveiligings bulletins en bijgevoegde beveiligings Bulletin-ID-nummers (bijvoorbeeld MS16-XXX) als een draai punt. Deze vorm van documentatie voor beveiligings updates, inclusief Bulletin-ID-nummers, wordt buiten gebruik gesteld en vervangen door de hand leiding voor beveiligings updates. In plaats van bulletin-Id's draait de nieuwe hand leiding naar ID-nummers voor het beveiligingslek en KB-artikel-id's. Zie [Veelgestelde vragen over de hand leiding voor beveiligings updates](https://www.microsoft.com/msrc/faqs-security-update-guide)voor meer informatie.


- **Artikel-id**: bevat de artikel-id voor de software-update. Het artikel waarnaar wordt verwezen biedt gedetailleerde informatie over de software-update en het probleem dat de software-update corrigeert of verbetert.  

- **Revisiedatum**: bevat de datum waarop de software-update voor het laatst is gewijzigd.  

- **Maximale ernstclassificatie**: bevat de ernstclassificatie die de leverancier voor de software-update heeft gedefinieerd.  

- **Beschrijving**: biedt een overzicht van de problemen die met de software-update worden verholpen of waarvan de ernst wordt verminderd.  

- **Toepasselijke talen**: biedt een lijst met de talen waarvoor de software-update van toepassing is.  

- **Betrokken producten**: biedt een lijst met de producten waarvoor de software-update van toepassing is.  

####  <a name="content-information"></a><a name="BKMK_ContentInformation"></a> Informatie over inhoud  
Op het tabblad **Informatie over inhoud** wordt de volgende informatie weergegeven over de inhoud die aan de geselecteerde software-update is gekoppeld:  

-   **Id van inhoud**: hier wordt de inhouds-id voor de software-update aangegeven.  

-   **Gedownload**: Hiermee wordt aangegeven of de software-update bestanden door Configuration Manager zijn gedownload.  

-   **Taal**: hier worden de talen voor de software-update vermeld.  

-   **Bronpad**: hier wordt het pad naar de bronbestanden voor de software-update aangegeven.  

-   **Grootte (MB)**: hier wordt de grootte van de bronbestanden voor de software-update aangegeven.  

####  <a name="custom-bundle-information"></a><a name="BKMK_CustomBundleInformation"></a> Aangepaste bundelgegevens  
Op het tabblad **Aangepaste bundelgegevens** wordt informatie over aangepaste bundels voor de software-update weergegeven. Wanneer de geselecteerde software-update gebundelde software-updates bevat die in het software-updatebestand zijn opgenomen, worden deze weergegeven in de sectie **Bundelgegevens** . Op dit tabblad worden geen gebundelde software-updates weergegeven die worden weergegeven op het tabblad **Informatie over inhoud** , zoals updatebestanden voor verschillende talen.  

####  <a name="supersedence-information"></a><a name="BKMK_SupersedenceInformation"></a> Vervangingsinformatie  
Op het tabblad **Vervangingsinformatie** wordt vervangingsinformatie weergegeven die op de software-update van toepassing is:  

- **Deze software-update is vervangen door een andere software-update**: hier worden de software-updates vermeld die deze update vervangen. Dit betekent dat de vermelde updates nieuwer zijn. In de meeste gevallen implementeert u een van de software-updates die de software-update vervangt. De software-updates die in de lijst worden weergegeven, bevatten hyperlinks naar webpagina's met meer informatie over de software-updates. Wanneer deze update niet wordt vervangen, wordt de waarde **Geen** weergegeven.  

- **Deze software-update vervangt de volgende software-updates**: hier worden de software-updates vermeld die door deze software-update worden vervangen. Dit betekent dat deze software-update nieuwer is. In de meeste gevallen implementeert u deze software-update om de software-updates te vervangen. De software-updates die in de lijst worden weergegeven, bevatten hyperlinks naar webpagina's met meer informatie over de software-updates. Wanneer deze update geen enkele andere update vervang, wordt de waarde **Geen** weergegeven.  

###  <a name="configure-software-updates-settings"></a><a name="BKMK_SoftwareUpdatesSettings"></a> Instellingen voor software-updates configureren  
In de eigenschappen kunt u instellingen configureren voor een of meer software-updates. U kunt de meeste instellingen voor software-updates alleen configureren op de centrale beheersite of een zelfstandige primaire site. De volgende secties helpen u om instellingen voor software-updates te configureren.  

####  <a name="set-maximum-run-time"></a><a name="BKMK_SetMaxRunTime"></a> De maximale uitvoeringstijd instellen  
Stel op het tabblad **Maximale uitvoeringstijd** de maximale hoeveelheid tijd in die aan een software-update wordt toegewezen om op clientcomputers te worden voltooid. Als de update langer duurt dan de waarde voor de maximale uitvoerings tijd, Configuration Manager maakt een status bericht en stopt de bewaking van de implementatie voor de installatie van software-updates. U kunt deze instelling alleen configureren op de centrale beheersite of een zelfstandige primaire site.  

Configuration Manager gebruikt deze instelling ook om te bepalen of de installatie van de software-update in een geconfigureerd onderhouds venster moet worden gestart. Als de waarde voor de maximale uitvoeringsduur groter is dan de hoeveelheid resterende tijd binnen het onderhoudsvenster, wordt de installatie van software-updates uitgesteld tot het volgende onderhoudsvenster. Wanneer er meerdere software-updates moeten worden geïnstalleerd op een clientcomputer met een geconfigureerd onderhoudsvenster (tijdsbestek), wordt de software-update met de geringste maximale uitvoeringsduur als eerste geïnstalleerd . Vervolgens wordt de software-update met de volgende geringste maximale uitvoeringsduur geïnstalleerd, enzovoort. Voordat elke software-update wordt geïnstalleerd, controleert de client of het beschikbare onderhoudsvenster voldoende tijd biedt voor het installeren van de software-update. Nadat het installeren van de software-update is gestart; wordt de installatie zelfs voortgezet als deze zich verder uitstrekt dan het einde van het onderhoudsvenster. Zie het gebruik van onderhouds [Vensters](../../core/clients/manage/collections/use-maintenance-windows.md)voor meer informatie over onderhouds Vensters.  

U kunt op het tabblad **Maximale uitvoeringstijd** de volgende instellingen weergeven en configureren:  

- **Maximale uitvoerings tijd**: Hiermee geeft u het maximale aantal minuten op dat aan de installatie van een software-update moet worden toegewezen om te volt ooien voordat de installatie niet meer wordt bewaakt door Configuration Manager. Deze instelling wordt gebruikt om te bepalen of er voldoende beschikbare tijd resteert om de update voor het einde van een onderhoudsvenster te installeren. De standaard instelling is 60 minuten voor service packs. Voor andere software-update typen is de standaard waarde 10 minuten als u een nieuwe installatie van Configuration Manager versie 1511 of hoger en vijf minuten hebt uitgevoerd bij een upgrade van een eerdere versie. Waarden kunnen uiteenlopen van 5 tot 9999 minuten.  

> [!IMPORTANT]  
>  Stel de waarde voor de maximale uitvoerings tijd in op een waarde die kleiner is dan het geconfigureerde onderhouds venster tijd of verg root de tijd van het onderhouds venster tot een groter dan de maximale uitvoerings tijd. Anders wordt de installatie van de software-update nooit gestart.  

####  <a name="set-custom-severity"></a><a name="BKMK_SetCustomSeverity"></a> Aangepaste ernst instellen  
In de eigenschappen voor een software-update kunt u het tabblad **Aangepaste ernst** gebruiken om waarden voor aangepaste ernst voor de software-updates te configureren. Dit kan noodzakelijk zijn als de vooraf gedefinieerde ernstwaarden niet voldoen aan uw behoeften. De aangepaste waarden worden weer gegeven in de kolom **aangepaste Ernst** in de Configuration Manager-console. U kunt de software-updates sorteren volgens de gedefinieerde waarden voor aangepaste ernst en u kunt ook query's en rapporten maken die op deze waarden kunnen worden gefilterd. U kunt deze instelling enkel configureren op de centrale beheersite of zelfstandige primaire site.  

U kunt de volgende instellingen configureren op het tabblad **Aangepaste ernst** .  

- **Aangepaste ernst**: hiermee stelt u een waarde in voor de aangepaste ernst voor de software-updates. Selecteer **Kritiek**, **Belangrijk**, **Gemiddeld**of **Laag** uit de lijst. De waarde voor aangepaste ernst is standaard leeg.

## <a name="crl-checking-for-software-updates"></a>CRL-controle voor software-updates
Standaard wordt de certificaatintrekkingslijst (CRL) niet gecontroleerd bij het verifiëren van de hand tekening op Configuration Manager software-updates. Door de CRL te raadplegen elke keer dat er een certificaat wordt gebruikt, bent u beter beschermd tegen het gebruik van een ingetrokken certificaat. Hierdoor ontstaat echter ook een vertraging in de verbinding en vinden er extra verwerkingsactiviteiten plaats op de computer die de CRL-controle uitvoert.  

Als u deze optie gebruikt, moet u CRL-controle inschakelen op de Configuration Manager-consoles die software-updates verwerken.  

#### <a name="to-enable-crl-checking"></a>Controle van certificaatintrekkingslijst inschakelen  
Op de computer die de CRL-controle uitvoert, voert u vanaf de product-DVD het volgende uit vanaf een opdracht prompt: **\SMSSETUP\BIN\X64 \\ ** < *Language* > **\UpdDwnldCfg.exe/checkrevocation**.  

Voor Engels (Verenigde Staten) voert u bijvoorbeeld **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe/checkrevocation** uit  
