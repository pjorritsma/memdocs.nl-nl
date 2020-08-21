---
title: Nieuwe versie 1702
titleSuffix: Configuration Manager
description: Krijg informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1702 van Configuration Manager.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: a947b332addbc3404617abdbbe199ede4e74dc63
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692788"
---
# <a name="what39s-new-in-version-1702-of-configuration-manager"></a>Wat&#39;s nieuw in versie 1702 van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Update 1702 voor Configuration Manager current branch is beschikbaar als een update in de console voor eerder geïnstalleerde sites waarop versie 1602, 1606 of 1610 wordt uitgevoerd. Het is ook beschikbaar als basislijn versie die u kunt gebruiken bij het installeren van een nieuwe implementatie.

> [!TIP]  
> Als u een nieuwe site wilt installeren, moet u een basislijn versie van Configuration Manager gebruiken.  
>
> Meer informatie over:    
> - [Nieuwe sites installeren](../../servers/deploy/install/installing-sites.md)  
> - [Updates installeren op sites](../../servers/manage/updates.md)  
> - [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)

De volgende secties bevatten informatie over wijzigingen en nieuwe mogelijkheden die zijn geïntroduceerd in versie 1702 van Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Afgeschafte functies en besturings systemen
Meer informatie over ondersteunings wijzigingen voordat ze worden geïmplementeerd in [verwijderde en afgeschafte items](deprecated/removed-and-deprecated.md).

Versie 1702 daalt ondersteuning voor de volgende producten:
- **SQL Server 2008 R2**, voor site database servers. Afschaffing van de ondersteuning werd voor het [eerst aangekondigd](deprecated/removed-and-deprecated-server.md#sql-server) op 10 juli 2015. Deze versie van SQL Server blijft ondersteund wanneer u een Configuration Manager versie van vóór versie 1702 gebruikt.
- **Windows Server 2008 R2**, voor site systeem servers en de meeste site systeem rollen. Afschaffing van de ondersteuning werd voor het [eerst aangekondigd](deprecated/removed-and-deprecated-server.md#server-os) op 10 juli 2015. Deze versie van Windows wordt ondersteund wanneer u een Configuration Manager versie van vóór versie 1702 gebruikt.  
- **Windows Server 2008**, voor site systeem servers en de meeste site systeem rollen. Afschaffing van de ondersteuning werd voor het [eerst aangekondigd](deprecated/removed-and-deprecated-server.md#server-os) op 10 juli 2015.
- **Windows XP Embedded**, als besturings systeem van de client. De afschaffing werd voor het [eerst aangekondigd](deprecated/removed-and-deprecated-client.md#deprecated-client-operating-systems) op 10 juli 2015. Deze versie van Windows wordt ondersteund wanneer u een Configuration Manager versie van vóór versie 1702 gebruikt.




## <a name="site-infrastructure"></a>Site-infra structuur

### <a name="improvements-for-in-console-search"></a>Verbeteringen voor zoeken in console
Hieronder vindt u verbeteringen in het gebruik van zoeken in de Configuration Manager-console:
- **Objectpad:**  
  Veel objecten bieden nu ondersteuning voor een kolom met de naam **Objectpad**.  Wanneer u deze kolom zoekt en opneemt in uw weergave resultaten, kunt u het pad naar elk object weer geven. Als u bijvoorbeeld een zoek opdracht naar apps uitvoert in het knoop punt toepassingen en ook subknooppunten zoekt, wordt in de kolom *Objectpad* in het deel venster met resultaten het pad weer gegeven naar elk object dat wordt geretourneerd.   

- **Behoud van Zoek tekst:**  
  Wanneer u tekst in het zoekvak invoert en vervolgens omschakelt tussen het doorzoeken van een subknooppunt en het huidige knoop punt, blijft de tekst die u hebt getypt nu behouden en blijft deze beschikbaar voor een nieuwe zoek opdracht zonder deze opnieuw in te voeren.

- **Behoud van uw besluit om subknooppunten te doorzoeken:**  
  De optie die u kiest voor het zoeken in het *huidige knoop punt* of *alle subknooppunten* , blijft behouden wanneer u het knoop punt wijzigt waarin u werkt. Dit nieuwe gedrag houdt in dat u deze beslissing niet telkens opnieuw hoeft in te stellen wanneer u over de-console gaat. Wanneer u de-console opent, is de optie standaard alleen van het huidige knoop punt te doorzoeken.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Feedback verzenden vanuit de Configuration Manager-console

U kunt de feedback opties in de console gebruiken om feedback rechtstreeks naar het ontwikkel team te verzenden.

U kunt de volgende **feedback** optie vinden:
- In het lint helemaal links op het tabblad Start van elk knoop punt.  
  ![Vaandel](./media/feedback-home.png)

- Wanneer u met de rechter muisknop op een object in de-console klikt.   
   ![Recht: Klik op optie](./media/feedback-option.png)   

  Als u **feedback** kiest, wordt uw browser geopend op de [website van Configuration Manager UserVoice-feedback](https://configurationmanager.uservoice.com/forums/300492-ideas).


###  <a name="changes-for-updates-and-servicing"></a>Wijzigingen voor updates en onderhoud
De volgende wijzigingen zijn van invloed op updates en onderhoud:

- **Knooppunt locatie**   
  Na de installatie van versie 1702 wordt het knoop punt **updates en onderhoud** weer gegeven als een knoop punt op het hoogste niveau onder **beheer**. Het is niet langer een onderliggend knoop punt onder **Cloud Services**.

- **Nieuwe update statussen**  
  Wanneer u beschik bare updates in de-console bekijkt, zijn er twee nieuwe statussen:  
  - **Beschikbaar voor installatie** -dit is een update die is gedownload en gereed is voor installatie.
  - **Gereed voor downloaden**  : deze update is beschikbaar, maar is niet gedownload. U kunt ervoor kiezen om deze update te downloaden, maar deze is vervangen door een meer recente update.


- **Eenvoudigere Update opties**  
  De volgende keer dat uw infra structuur in aanmerking komt voor twee of meer updates, wordt alleen de meest recente update gedownload. Als uw huidige site versie bijvoorbeeld twee of meer ouder is dan de meest recente versie die beschikbaar is, wordt alleen de meest recente update versie automatisch gedownload.  

  U kunt ervoor kiezen om de andere beschik bare updates te downloaden en te installeren, zelfs als dit niet de meest recente versie is. Als u een oudere Update downloadt, wordt een waarschuwing weer gegeven dat de update is vervangen door een nieuwere versie. Als u een update wilt downloaden die *beschikbaar is om te downloaden*, selecteert u de update in de-console en klikt u vervolgens op **downloaden**.

- **Verbeterde opschoning van oudere updates**   
  We hebben een automatische opschoon functie toegevoegd waarmee overbodige down loads uit de map ' EasySetupPayload ' op de site server worden verwijderd. Omdat dit is geïntroduceerd in versie 1702, begint het opschonen na de installatie van een volgende update, zoals een update pakket of toekomstige update versie.  


### <a name="data-warehouse-service-point"></a>Data Warehouse-service punt
Gebruik het Data Warehouse-service punt om historische gegevens over lange termijn voor uw Configuration Manager-implementatie op te slaan en te rapporteren.

Het Data Warehouse ondersteunt Maxi maal 2 TB aan gegevens, met tijds tempels voor het bijhouden van wijzigingen. De opslag van gegevens wordt uitgevoerd door automatische synchronisaties van de Configuration Manager-site database naar de Data Warehouse-data base. Deze informatie is vervolgens toegankelijk vanaf uw Reporting Services-punt.

Zie [het Data Warehouse-service punt](../../servers/manage/data-warehouse.md)voor meer informatie.


### <a name="peer-cache-improvements"></a>Verbeteringen in de peer-cache
Vanaf versie 1702 wordt een aanvraag voor inhoud geweigerd wanneer de bron computer van de peer-cache aan een van de volgende voor waarden voldoet:  
-  Bevindt zich in de modus voor laag accu niveau.
-  CPU-belasting overschrijdt 80% op het moment dat de inhoud wordt aangevraagd.
-  Schijf-I/O heeft een *AvgDiskQueueLength* die groter is dan 10.
-  Er zijn geen meer beschik bare verbindingen met de computer.   
Zie **beperkte toegang tot een peer-cache bron** in [peer-cache voor Configuration Manager-clients](../hierarchy/client-peer-cache.md)voor meer informatie.   

Daarnaast worden er drie nieuwe rapporten toegevoegd aan het rapportage punt. U kunt deze rapporten gebruiken om meer informatie te krijgen over geweigerde inhouds aanvragen, waaronder welke grens groep, computer en inhoud is betrokken. Zie [bewaking](../hierarchy/client-peer-cache.md#monitoring) in het onderwerp peer-cache.

### <a name="content-library-cleanup-tool"></a>Hulpprogramma voor het opschonen van de inhoudsbibliotheek
Gebruik het [hulp programma voor opruimen van inhouds bibliotheken](../hierarchy/content-library-cleanup-tool.md) om inhoud te verwijderen van distributie punten wanneer die inhoud niet langer aan een toepassing is gekoppeld.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>De OMS-connector gebruiken met de Azure Government Cloud
U kunt de OMS-connector gebruiken om verbinding te maken met OMS-Log Analytics in Microsoft Azure Government Cloud. Hiervoor moet u een configuratie bestand wijzigen voordat u de OMS-connector installeert, zodat de connector kan samen werken met de Government Cloud. Zie [de OMS-connector gebruiken met de Azure Government-Cloud](/azure/azure-monitor/platform/collect-sccm)voor meer informatie.

### <a name="software-update-points-are-added-to-boundary-groups"></a>Software-update punten worden toegevoegd aan grens groepen
Vanaf versie 1702 gebruiken de-clients grens groepen om een nieuw software-update punt te zoeken en om een nieuw software-update punt te vinden als het huidige item niet langer toegankelijk is. U kunt afzonderlijke software-update punten toevoegen aan verschillende grens groepen om te bepalen welke servers een client kan vinden. Zie [Software-update punten](../../servers/deploy/configure/boundary-groups.md#bkmk_sup) in het onderwerp [grens groepen configureren](../../servers/deploy/configure/boundary-groups.md) voor meer informatie.


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Instellingen voor naleving

### <a name="new-compliance-settings-for-ios"></a>Nieuwe instellingen voor naleving voor iOS

Er zijn veel nieuwe instellingen voor iOS-apparaten toegevoegd zodat deze overeenkomen met die van Microsoft Intune.


## <a name="application-management"></a>Toepassingsbeheer

### <a name="improved-support-for-windows-store-for-business-apps"></a>Verbeterde ondersteuning voor Windows Store voor bedrijven-apps

U kunt nu online gelicentieerde Apps implementeren vanuit de Windows Store voor bedrijven naar Windows 10-Pc's die u beheert met behulp van de Configuration Manager-client.
Zie [apps beheren vanuit Windows Store voor bedrijven](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)voor meer informatie.

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Controleren of uitvoer bare bestanden worden uitgevoerd voordat een toepassing wordt geïnstalleerd

In het dialoog venster **Eigenschappen** van een implementatie type op het tabblad **installatie gedrag** kunt u nu een van de meer uitvoer bare bestanden opgeven die, indien actief, de installatie van het implementatie type blokkeert. De gebruiker moet het uitgevoerde uitvoer bare bestand sluiten (of het kan automatisch worden gesloten voor implementaties met een vereist doel) voordat het implementatie type kan worden geïnstalleerd.

Als de toepassing is geïmplementeerd als **beschikbaar**en een eind gebruiker probeert een toepassing te installeren, wordt u gevraagd of u de door u opgegeven uitvoer bare bestanden wilt sluiten voordat de installatie kan worden voortgezet.

Als de toepassing is geïmplementeerd als **vereist**en de optie **voor het automatisch sluiten van uitvoer bare bestanden die u hebt opgegeven op het tabblad installatie gedrag van het dialoog venster Eigenschappen van implementatie type** , wordt een dialoog venster weer gegeven waarin wordt gemeld dat de uitvoer bare bestanden die u hebt opgegeven automatisch worden gesloten wanneer de deadline voor de installatie van de toepassing wordt bereikt.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Verbeteringen in het beheer van apps voor hybride MDM

- [Door het volume gekochte iOS-Apps implementeren in apparaat verzamelingen](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Ondersteuning voor het iOS-volume-aanschaf programma voor onderwijs](#support-for-ios-volume-purchase-program-for-education)
- [Ondersteuning voor meerdere volume-aankoop programma tokens](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Implementatie van besturingssystemen

### <a name="expire-stand-alone-media"></a>Zelfstandige media laten verlopen
Wanneer u zelfstandige media maakt, zijn er nieuwe opties voor het instellen van optionele begin-en verval datums op de media. Deze instellingen zijn standaard uitgeschakeld. De datums worden vergeleken met de systeem tijd op de computer voordat de zelfstandige media worden uitgevoerd. Wanneer de systeem tijd eerder is dan de begin tijd of later dan de verloop tijd, wordt de zelfstandige media niet gestart. Deze opties zijn ook beschikbaar met de Power shell-cmdlet New-CMStandaloneMedia. Zie voor meer informatie [maken van zelfstandige media](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="package-id-displayed-in-task-sequence-steps"></a>Pakket-ID weer gegeven in taken reeks stappen
Elke taken reeks stap die verwijst naar een pakket, stuur programmapakket, installatie kopie van het besturings systeem, installatie kopie of besturings systeem, geeft nu de pakket-ID weer van het object waarnaar wordt verwezen. Wanneer een taken reeks stap naar een toepassing verwijst, wordt de object-ID weer gegeven.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Ondersteuning voor extra inhoud op zelfstandige media
Aanvullende inhoud wordt nu ondersteund op zelfstandige media. U kunt extra pakketten, stuur programmapakketten en toepassingen selecteren die moeten worden klaargezet op de media, samen met de andere inhoud waarnaar wordt verwezen in de taken reeks. Voorheen werd alleen inhoud waarnaar wordt verwezen in de taken reeks, klaargezet op zelfstandige media. Zie voor meer informatie [maken van zelfstandige media](../../../osd/deploy-use/create-stand-alone-media.md).

### <a name="hardware-inventory-collects-uefi-information"></a>De hardware-inventaris verzamelt UEFI-gegevens
Er is een nieuwe hardware-inventaris klasse (**SMS_Firmware**) en-eigenschap (**UEFI**) beschikbaar om u te helpen bepalen of een computer in de UEFI-modus wordt gestart. Wanneer een computer in de UEFI-modus wordt gestart, wordt de eigenschap **UEFI** ingesteld op **True**. Dit is standaard ingeschakeld in Hardware-inventarisatie. Zie [hardware-inventaris configureren](../../clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over hardware-inventarisatie.

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Verbeteringen aan software Center-waarschuwings berichten voor taken reeksen met een hoge impact
Deze release bevat de volgende verbeteringen voor waarschuwings berichten van software Center voor taken reeksen met een hoge impact van de implementatie:

- In de eigenschappen voor de taken reeks kunt u nu elke taken reeks configureren, inclusief niet-besturings systeem taken reeksen, als een implementatie met een hoog risico. Elke taken reeks die aan bepaalde voor waarden voldoet, wordt automatisch gedefinieerd als hoge impact. Zie [implementaties met een hoog risico beheren](../../servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.
- In de eigenschappen voor de taken reeks kunt u kiezen of u het standaard meldings bericht wilt gebruiken of uw eigen aangepaste meldings bericht wilt maken voor implementaties met hoge impact.
- In de eigenschappen voor de taken reeks kunt u eigenschappen van software Center configureren, zoals het opnieuw opstarten vereist, de download grootte van de taken reeks en de geschatte uitvoerings tijd.
- In het standaard bericht van hoge impact voor in-place upgrades wordt nu aangegeven dat uw apps, gegevens en instellingen automatisch worden gemigreerd. Voorheen werd het standaard bericht voor een installatie van het besturings systeem aangegeven dat alle apps, gegevens en instellingen verloren zouden zijn gegaan. Dit is niet waar voor een in-place upgrade.

Zie [Configure high-effect Task sequence Settings](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#set-a-task-sequence-as-a-high-impact-task-sequence) (Engelstalig) voor meer informatie.

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Terugkeren naar de vorige pagina wanneer een taken reeks mislukt
U kunt nu teruggaan naar een vorige pagina wanneer u een taken reeks uitvoert en er een fout optreedt. Vóór deze release moest u de taken reeks opnieuw opstarten als er een fout is opgetreden. U kunt bijvoorbeeld de **vorige** knop in de volgende scenario's gebruiken:

- Wanneer een computer wordt opgestart in Windows PE, wordt het dialoog venster Boots trap van taken reeks mogelijk weer gegeven voordat de taken reeks beschikbaar is. Als u in dit scenario op Volgende klikt, wordt de laatste pagina van de taken reeks weer gegeven met een bericht dat er geen taken reeksen beschikbaar zijn. U kunt nu op **vorige** klikken om opnieuw te zoeken naar beschik bare taken reeksen. U kunt dit proces herhalen totdat de taken reeks beschikbaar is.
- Wanneer u een taken reeks uitvoert, maar afhankelijke inhouds pakketten zijn nog niet beschikbaar op distributie punten, mislukt de taken reeks. U kunt nu de ontbrekende inhoud distribueren (als deze nog niet is gedistribueerd) of wachten tot de inhoud beschikbaar is op distributie punten, en klik vervolgens op **vorige** om de taken reeks opnieuw te laten zoeken naar de inhoud.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Inhoud vooraf in cache opslaan voor beschik bare implementaties en taken reeksen
Vanaf versie 1702, voor beschik bare implementaties van taken reeksen, kunt u ervoor kiezen om inhoud in de cache te gebruiken. Inhoud vooraf-cache biedt u de mogelijkheid om de client toe te staan de toepasselijke inhoud te downloaden zodra deze de implementatie ontvangt. Als de gebruiker klikt op **installeren** in Software Center, is de inhoud daarom gereed en wordt de installatie snel gestart, omdat de inhoud zich op de lokale harde schijf bevindt. Zie [inhoud vooraf in cache configureren](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#configure-pre-cache-content)voor meer informatie.

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Conversie van BIOS naar UEFI tijdens een in-place upgrade
In de update voor Windows 10 Crea tors wordt een eenvoudig conversie programma geïntroduceerd waarmee het proces voor het opnieuw partitioneren van de harde schijf voor UEFI-hardware wordt geautomatiseerd en het conversie programma wordt geïntegreerd in het Windows 7-in-place upgrade proces. Wanneer u dit hulp programma combineert met de taken reeks voor de upgrade van het besturings systeem en het OEM-hulp programma dat de firmware converteert van BIOS naar UEFI, kunt u uw computers converteren van BIOS naar UEFI tijdens een in-place upgrade naar de update voor Windows 10 Crea tors. Zie [taken reeks stappen voor het beheren van de conversie van BIOS naar UEFI](../../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)voor meer informatie.

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Verbeteringen in de taken reeks stap toepassingen installeren
Deze versie heeft de volgende verbeteringen geïntroduceerd:
- Het maximum aantal toepassingen dat u kunt installeren op 99 in de taken reeks stap **toepassingen installeren** is verhoogd. Het vorige maximum aantal was 9 toepassingen.
- Wanneer u toepassingen toevoegt aan de taken reeks stap **toepassingen installeren** in de taken reeks editor, kunt u nu meerdere toepassingen selecteren in het deel venster **Selecteer de toepassing die u wilt installeren** .

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Verbeteringen in de taken reeks voor het automatisch Toep assen van Stuur Programma's
Er zijn nu nieuwe taken reeks variabelen beschikbaar voor het configureren van de time-outwaarde voor de taken reeks stap stuur programma automatisch Toep assen bij het maken van aanvragen voor HTTP-catalogi. De volgende variabelen en standaard waarden (in seconden) zijn beschikbaar:
- SMSTSDriverRequestResolveTimeOut  
  Standaardinstelling: 60
- SMSTSDriverRequestConnectTimeOut  
  Standaardinstelling: 60
- SMSTSDriverRequestSendTimeOut  
  Standaardinstelling: 60
- SMSTSDriverRequestReceiveTimeOut  
  Standaard: 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Windows 10 ADK getraceerd op build-versie
De Windows 10 ADK wordt nu gevolgd door een build-versie om te zorgen voor een meer ondersteunde ervaring bij het aanpassen van Windows 10-opstart installatie kopieën. Als de site bijvoorbeeld gebruikmaakt van de Windows ADK voor Windows 10 versie 1607, kunnen alleen opstart installatie kopieën met versie 10.0.14393 worden aangepast in de-console. Zie [opstart installatie kopieën aanpassen](../../../osd/get-started/customize-boot-images.md)voor meer informatie over het aanpassen van WinPE-versies.

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Het bronpad van de standaard installatie kopie kan niet meer worden gewijzigd
Standaard installatie kopieën worden beheerd door Configuration Manager en het bronpad van de standaard installatie kopie kan niet meer worden gewijzigd in de Configuration Manager-console of door gebruik te maken van de Configuration Manager SDK. U kunt door gaan met het configureren van een aangepast bronpad voor aangepaste opstart installatie kopieën.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Standaard installatie kopieën worden opnieuw gegenereerd na het upgraden van Configuration Manager naar een nieuwe versie
Vanaf deze release, wanneer u de Windows ADK-versie bijwerkt en vervolgens updates en onderhoud gebruikt om de nieuwste versie van Configuration Manager te installeren, Configuration Manager de standaard installatie kopieën opnieuw genereren. Dit omvat de nieuwe Window PE-versie van de bijgewerkte Windows ADK, de nieuwe versie van de Configuration Manager-client, stuur Programma's, aanpassingen, enzovoort. Aangepaste opstart installatie kopieën worden niet gewijzigd. Zie [opstart installatie kopieën beheren](../../../osd/get-started/manage-boot-images.md#BKMK_BootImageDefault)voor meer informatie.

## <a name="software-updates"></a>Software-updates

### <a name="deploy-office-365-apps-to-clients"></a>Office 365-Apps implementeren op clients
Vanaf versie 1702 kunt u vanuit het Office 365 client management-dash board het Office 365-installatie programma starten waarmee u de installatie-instellingen van Office 365 kunt configureren, bestanden van Office Content Delivery Networks (Cdn's) downloadt en de bestanden als een toepassing implementeert in Configuration Manager. Zie [Office 365 ProPlus-updates beheren](../../../sum/deploy-use/manage-office-365-proplus-updates.md#bkmk_deploy)voor meer informatie.

> [!IMPORTANT]
> De Office 365-app die u maakt en implementeert met behulp van de wizard Office 365-toepassing in Configuration Manager wordt niet automatisch beheerd door Configuration Manager totdat u de instelling **beheer van de Office 365-client opnieuw inschakelen** hebt ingeschakeld. Zie [over client instellingen](../../clients/deploy/about-client-settings.md)voor meer informatie.

### <a name="manage-express-installation-files-for-windows-10-updates"></a>De bestanden voor snelle installatie van Windows 10-updates beheren
Vanaf versie 1702 ondersteunt Configuration Manager snelle installatie bestanden voor Windows 10-updates. Wanneer u een ondersteunde versie van Windows 10 gebruikt, kunt u de Configuration Manager-instellingen gebruiken om alleen de wijzigingen te downloaden tussen de cumulatieve update voor Windows 10 van de huidige maand en de update van de vorige maand. Zonder bestanden voor snelle installatie wordt Configuration Manager de volledige cumulatieve update van Windows 10 (inclusief alle updates van de vorige maanden) elke maand gedownload. Het gebruik van bestanden voor snelle installatie biedt kleinere down loads en snellere installatie tijden op clients. Zie voor meer informatie [bestanden voor snelle installatie beheren voor Windows 10-updates](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Beheer van mobiele apparaten

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Android-en iOS-versies zijn niet meer doelwitbaar in wizards voor het maken van hybride MDM

Vanaf versie 1702 voor hybride Mobile Device Management (MDM) hoeft u niet langer specifieke versies van Android en iOS te richten bij het maken van nieuwe beleids regels en profielen voor apparaten die door intune worden beheerd. In plaats daarvan kiest u een van de volgende typen apparaten:

- Android
- Samsung KNOX Standard 4,0 en hoger
- iPhone
- iPad

Deze wijziging is van invloed op de wizards voor het maken van de volgende items:

- Configuratie-items
- Nalevingsbeleid
- Certificaatprofielen
- E-mailprofielen
- VPN-profielen
- Wi-Fi-profielen

Met deze wijziging kunnen hybride implementaties sneller ondersteuning bieden voor nieuwe Android-en iOS-versies, zonder dat er een nieuwe Configuration Manager versie of uitbrei ding nodig is. Wanneer een nieuwe versie wordt ondersteund in intune standalone, kunnen gebruikers hun mobiele apparaten upgraden naar die versie.

Om problemen te voor komen bij het uitvoeren van een upgrade van eerdere versies van Configuration Manager, zijn de versies van het mobiele besturings systeem nog steeds beschikbaar op de pagina eigenschappen van deze items. Als u nog steeds een specifieke versie nodig hebt, kunt u het nieuwe item maken en vervolgens de doel versie opgeven op de pagina eigenschappen van het zojuist gemaakte item. 

> [!NOTE]
> De laatste versie van het mobiele besturings systeem die beschikbaar is op de eigenschappen pagina's, is van toepassing op die versie en alle latere versies. Eigenschappen pagina's bieden de volgende opties voor het richten van besturings systemen die later zijn dan Android 7 en iOS 10: 
> - **Android 7 en hoger**
> - **Alle iPhone-of iPod Touch-apparaten met iOS 10 en hoger**
> - **Alle iPad-apparaten met iOS 10 en hoger**

### <a name="android-for-work-support"></a>Ondersteuning van Android for Work
Vanaf 1702, hybride Mobile Device Management met Microsoft Intune ondersteunt nu de registratie en het beheer van Android for work-apparaten.

### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Door het volume gekochte iOS-Apps implementeren in apparaat verzamelingen

U kunt nu gelicentieerde Apps implementeren op apparaten en gebruikers. Afhankelijk van de mogelijkheden van de apps om de ondersteuning van een apparaat te ondersteunen, wordt een geschikte licentie gevraagd wanneer u deze implementeert, als volgt:

| Configuration Manager versie | App ondersteunt apparaat-licenties? | Type implementatie verzameling | Geclaimde licentie |
| ----------------------------- | ------------------------------ | -------------------------- | --------------- |
|Ouder dan 1702|Ja|Gebruiker|Gebruikers licentie|
|Ouder dan 1702|Nee|Gebruiker|Gebruikers licentie|
|Ouder dan 1702|Ja|Apparaat|Gebruikers licentie|
|Ouder dan 1702|Nee|Apparaat|Gebruikers licentie|
|1702 en hoger|Ja|Gebruiker|Gebruikers licentie|
|1702 en hoger|Nee|Gebruiker|Gebruikers licentie|
|1702 en hoger|Ja|Apparaat|Apparaatlicentie|
|1702 en hoger|Nee|Apparaat|Gebruikers licentie|

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Ondersteuning voor het iOS-volume-aanschaf programma voor onderwijs

U kunt nu ook apps implementeren en volgen die u hebt aangeschaft via het iOS volume Purchase Program voor onderwijs.

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Ondersteuning voor meerdere volume-aankoop programma tokens

U kunt nu meerdere Apple volume Purchase Program-tokens koppelen aan Configuration Manager.

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Ondersteuning voor line-of-Business-apps in Windows Store voor bedrijven

U kunt nu aangepaste line-of-Business-Apps synchroniseren vanuit Windows Store voor bedrijven.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Verbeteringen in nalevings beleid voor voorwaardelijke toegang

Een nieuwe regel voor nalevings beleid voor apparaten is beschikbaar om u te helpen bij het blok keren van de toegang tot bedrijfs bronnen die ondersteuning bieden voor voorwaardelijke toegang, wanneer gebruikers apps gebruiken die deel uitmaken van een niet-compatibele lijst met apps. De lijst met niet-compatibele apps kan worden gedefinieerd door de beheerder bij het toevoegen van de nieuwe compatibele regel- **apps die niet kunnen worden geïnstalleerd**. Voor deze regel moet de beheerder de naam van de **app**, de **App-ID**en de uitgever van de **app** (optioneel) invoeren bij het toevoegen van een app aan de lijst die niet aan de vereisten voldoet. Deze instelling is alleen van toepassing op iOS-en Android-apparaten.

Dit helpt organisaties bovendien bij het beperken van gegevens die worden gelekt via onbeveiligde apps en om te voor komen dat er veel gegevens worden verbruikt via bepaalde apps.


### <a name="new-mobile-threat-defense-monitoring-tools"></a>Nieuwe hulpprogram ma's voor de bewaking van mobiele bedreigingen

Vanaf versie 1702 hebt u nieuwe manieren om de nalevings status te controleren met uw provider voor de bescherming van mobiele bedreigingen.


## <a name="protect-devices"></a>Apparaten beveiligen

### <a name="detect-outdated-antimalware-client-versions"></a>Verouderde antimalware-client versies detecteren
Vanaf versie 1702 kunt u een waarschuwing configureren om ervoor te zorgen dat Endpoint Protection-clients niet verouderd zijn. Zie [waarschuwing voor verouderde malware-client](../../../protect/deploy-use/endpoint-configure-alerts.md#alert-for-outdated-malware-client)voor meer informatie.

### <a name="device-health-attestation-updates"></a>Apparaatstatusverklaring-updates
Apparaatstatusverklaring-service voor on-premises clients kan nu worden geconfigureerd en beheerd vanaf het beheer punt. Zie [Health Attestation](../../servers/manage/health-attestation.md)voor meer informatie.

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Certificaat profielen voor Windows hello voor bedrijven

Als u certificaat profielen wilt opslaan in de sleutel container van Windows hello voor bedrijven en het certificaat profiel de EKU voor smartcard aanmelding gebruikt, moet u machtigingen voor sleutel registratie configureren om ervoor te zorgen dat het certificaat correct wordt gevalideerd.
Zie [Windows hello voor bedrijven-instellingen](../../../protect/deploy-use/windows-hello-for-business-settings.md)voor meer informatie.

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nieuwe melding voor Windows hello voor bedrijven voor eind gebruikers
Een nieuwe melding van Windows 10 informeert de eind gebruikers dat ze aanvullende acties moeten ondernemen om de installatie van Windows hello voor bedrijven te volt ooien (bijvoorbeeld het instellen van een pincode).