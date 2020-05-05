---
title: Mogelijkheden van Technical Preview 1701
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1701.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: f100d28b3fd4ce0d310ddb2f0b4e777c72f72881
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076200"
---
# <a name="capabilities-in-technical-preview-1701-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1701 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*



Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1701. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Verbeteringen voor grens groepen voor software-update punten
Met deze preview-versie kunt u nu grens groepen gebruiken om clients te koppelen aan software-update punten. Dit maakt deel uit van het voortgezette werk om de wijzigingen voor grens groepen uit te breiden om aanvullende site systeem rollen te beheren.  Wijzigingen voor grens groepen werden voor het eerst geïntroduceerd in Technical Preview 1609 en de Current Branch in versie 1610.  

Met deze preview-versie gebruikt u het nieuwe gedrag grens groep om te beheren welke software-update punten een client kan gebruiken, vergelijkbaar met de manier waarop u beheert welk distributie punt een client kan gebruiken:  

- U kunt grens groepen configureren om een of meer servers te koppelen die als host fungeren voor een software-update punt.
- Clients die een nieuw software-update punt zoeken, proberen een te gebruiken dat is gekoppeld aan de huidige grens groep.
- Wanneer de client het huidige software-update punt niet kan bereiken en er geen kan worden gevonden vanuit de huidige grens groep, gebruikt de client terugval gedrag om de beschik bare groep software-update punten die het kan gebruiken, uit te breiden.    

Zie [grens groepen](../servers/deploy/configure/boundary-groups.md) in de inhoud voor de current branch voor meer informatie over grens groepen.

Met deze preview-versie worden grens groepen voor software-update punten echter slechts gedeeltelijk geïmplementeerd. U kunt software-update punten toevoegen en neighbor-grens groepen configureren die software-update punten bevatten, maar de terugval tijd voor software-update punten wordt nog niet ondersteund en clients wachten twee uur voordat de terugval wordt gestart.

Hieronder vindt u een beschrijving van het gedrag van software-update punten met deze technische preview:  

- **Nieuwe clients gebruiken grens groepen om software-update punten te selecteren** Een client die u na de installatie van versie 1701 installeert, selecteert een software-update punt van die gekoppeld aan de grens groep van de client.

  Dit vervangt het vorige gedrag waarbij clients wille keurig een software-update punt selecteren uit een lijst met gebruikers die het forest clients delen.   

- **Eerder geïnstalleerde clients blijven hun huidige software-update punt gebruiken totdat ze een nieuwe hebben gevonden.**
  Clients die eerder zijn geïnstalleerd en die al een software-update punt hebben, blijven dat software-update punt gebruiken totdat ze terugval zijn. Dit zijn onder andere software-update punten die niet zijn gekoppeld aan de huidige grens groep van de client. Er wordt niet onmiddellijk geprobeerd een software-update punt te vinden en te gebruiken van de huidige grens groep.

  Een client die al een software-update punt heeft, begint met het gebruik van deze nieuwe grens groep gedrag alleen wanneer het huidige software-update punt door de client niet is bereikt en terugval wordt gestart.
  Deze vertraging bij het overschakelen naar het nieuwe gedrag is opzettelijk. Dit komt doordat een wijziging van het software-update punt kan leiden tot een groot gebruik van netwerk bandbreedte wanneer de client gegevens synchroniseert met het nieuwe software-update punt. De vertraging in de overgang kan helpen om te voor komen dat uw netwerk verzadigd is voor al uw clients om tegelijkertijd over te scha kelen naar nieuwe software-update punten.

- **Configuraties voor terugval tijd:** Configuraties voor wanneer clients terugval starten om te zoeken naar een nieuw software-update punt, worden niet ondersteund in deze technische preview-versie. Dit omvat configuraties voor **terugval tijden (in minuten)** en **nooit terugval**, die u kunt configureren voor verschillende relaties met grens groepen.

  Clients behouden in plaats daarvan hun huidige gedrag waarbij een client gedurende twee uur verbinding probeert te maken met het huidige software-update punt om een nieuw software-update punt te vinden dat kan worden gebruikt.

  Wanneer een client terugval gebruikt, worden de configuratie van de grens groep gebruikt voor terugval om een groep beschik bare software-update punten te maken. Deze groep bevat alle software-update punten van de *huidige grens groep*van de client, grens groepen in de *grenzen*en de *standaard grens groep*van de clients-site.

- **De standaard site grens groep configureren:**  
  Overweeg een software-update punt toe te voegen aan de *standaard-site&lt;-Boundary-Group>*. Dit zorgt ervoor dat clients die geen deel uitmaken van een andere grens groep, een software-update punt kunnen vinden.


Als u software-update punten voor grens groepen wilt beheren, gebruikt u de [procedures in de current branch-documentatie](../servers/deploy/configure/boundary-group-procedures.md), maar vergeet niet dat u de door u geconfigureerde terugval tijden nog niet gebruikt voor software-update punten.


## <a name="hardware-inventory-collects-uefi-information"></a>De hardware-inventaris verzamelt UEFI-gegevens
Er is een nieuwe hardware-inventaris klasse (**SMS_Firmware**) en-eigenschap (**UEFI**) beschikbaar om u te helpen bepalen of een computer in de UEFI-modus wordt gestart. Wanneer een computer in de UEFI-modus wordt gestart, wordt de eigenschap **UEFI** ingesteld op **True**. Dit is standaard ingeschakeld in Hardware-inventarisatie. Zie [hardware-inventaris configureren](../clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over hardware-inventarisatie.

## <a name="improvements-to-operating-system-deployment"></a>Verbeteringen in de implementatie van besturings systemen
We hebben de volgende verbeteringen aangebracht in de implementatie van het besturings systeem. veel hiervan zijn het resultaat van de feedback van uw gebruikers stem.
- [**Ondersteuning voor meer toepassingen voor de taken reeks stap toepassingen installeren**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t): we hebben het maximum aantal toepassingen dat u in de taken reeks stap voor het installeren van **toepassingen** kunt installeren, uitgebreid naar 99. Het vorige maximum aantal was 9 toepassingen.
- [**Meerdere apps selecteren in de taken reeks stap app installeren**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step): wanneer u toepassingen toevoegt aan de taken reeks stap toepassing installeren in de taken reeks editor, kunt u nu meerdere toepassingen selecteren in het deel venster **Selecteer de toepassing die u wilt installeren** .
- [**Zelfstandige media laten verlopen**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media): wanneer u zelfstandige media maakt, zijn er nieuwe opties voor het instellen van optionele begin-en verval datums op de media. Deze instellingen zijn standaard uitgeschakeld. De datums worden vergeleken met de systeem tijd op de computer voordat de zelfstandige media worden uitgevoerd. Wanneer de systeem tijd eerder is dan de begin tijd of later dan de verloop tijd, wordt de zelfstandige media niet gestart. Deze opties zijn ook beschikbaar met de Power shell-cmdlet New-CMStandaloneMedia.
- [**Ondersteuning voor aanvullende inhoud in zelfstandige media**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic): extra inhoud wordt nu ondersteund op zelfstandige media. U kunt extra pakketten, stuur programmapakketten en toepassingen selecteren die moeten worden klaargezet op de media, samen met de andere inhoud waarnaar wordt verwezen in de taken reeks. Voorheen werd alleen inhoud waarnaar wordt verwezen in de taken reeks, klaargezet op zelfstandige media.
- [**Configureer bare time-out voor de taken reeks stap Stuur Programma's automatisch Toep assen**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout): er zijn nu nieuwe taken reeks variabelen beschikbaar voor het configureren van de time-outwaarde voor de taken reeks stap stuur programma automatisch Toep assen bij het maken van aanvragen voor http-catalogi. De volgende variabelen en standaard waarden (in seconden) zijn beschikbaar:
   - SMSTSDriverRequestResolveTimeOut standaard: 60
   - SMSTSDriverRequestConnectTimeOut standaard: 60
   - SMSTSDriverRequestSendTimeOut standaard: 60
   - SMSTSDriverRequestReceiveTimeOut standaard: 480
- [**Pakket-id wordt nu weer gegeven in taken reeks stappen**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste): elke taken reeks stap die verwijst naar een pakket, stuur programmapakket, installatie kopie van het besturings systeem, opstart installatie kopie of besturings systeem, geeft nu de pakket-id weer van het object waarnaar wordt verwezen. Wanneer een taken reeks stap naar een toepassing verwijst, wordt de object-ID weer gegeven.
- **Windows 10 ADk getraceerd door build-versie**: de Windows 10 ADk wordt nu gevolgd door build-versie om te zorgen voor een meer ondersteunde ervaring bij het aanpassen van Windows 10-opstart installatie kopieën. Als de site bijvoorbeeld gebruikmaakt van de Windows ADK voor Windows 10 versie 1607, kunnen alleen opstart installatie kopieën met versie 10.0.14393 worden aangepast in de-console. Zie [opstart installatie kopieën aanpassen](../../osd/get-started/customize-boot-images.md)voor meer informatie over het aanpassen van WinPE-versies.
- Het bronpad van de **standaard installatie kopie kan niet meer worden gewijzigd**: standaard installatie kopieën worden beheerd door Configuration Manager en het bronpad van de standaard opstart installatie kopie kan niet meer worden gewijzigd in de Configuration Manager-console of met behulp van de Configuration Manager SDK. U kunt door gaan met het configureren van een aangepast bronpad voor aangepaste opstart installatie kopieën.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Software-updates hosten op distributie punten in de Cloud
Vanaf deze preview-versie kunt u een distributie punt in de Cloud gebruiken voor het hosten van een software-update pakket. Omdat u echter clients zodanig kunt configureren dat software-updates rechtstreeks vanuit Microsoft Update worden gedownload, moet u rekening houden met de extra kosten voor het implementeren van een software-update pakket voor een distributie punt in de Cloud.

Zie voor meer informatie over het gebruik van cloud-gebaseerde distributie punten [een distributie punt in de Cloud gebruiken](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) in de inhoud voor de Current Branch van Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Gegevens van apparaatstatusverklaring valideren via beheer punten

Met ingang van deze preview-versie kunt u beheer punten configureren om rapportage gegevens van Health Attestation te valideren voor de Cloud of on-premises Health Attestation-service. Op het tabblad nieuwe **Geavanceerde opties** in het dialoog venster **Eigenschappen van beheer punt componenten** kunt u de **URL van de on-premises**apparaatstatusverklaring-service **toevoegen**, **bewerken**of **verwijderen** . U kunt ook **aangepaste apparaatinstellingen** opgeven voor de client agent voor het **gebruik van de on-premises Health Attestation-service**.  Als **Ja** voor deze instelling is ingesteld, wordt rapportage op het on-premises beheer punt in plaats van de Cloud service ingeschakeld.

### <a name="try-it-out"></a>Uitproberen

- **On-premises apparaatstatusverklaring inschakelen op een beheer punt**<br>  Navigeer in de Configuration Manager-console naar de eigenschappen van het beheer punt en open **beheer punt componenten** en klik vervolgens op het tabblad **Geavanceerde opties** . Klik op **toevoegen** en geef de on-premises https://10.10.10.10) URL op (bijvoorbeeld voor de **url's van on-premises**apparaatstatusverklaring-service).
- **On-premises rapportage van de status verklaring van het beheer punt inschakelen voor de client agent**<br>Kies in de Configuration Manager-console **Administration** > **instellingen voor client** beheer en dubbel klik of maak een nieuwe **aangepaste apparaatinstellingen**. Selecteer **computer agent** en stel **on-premises Health Attestation-service gebruiken** in op **Ja**. Als de **optie communicatie met Apparaatstatusverklaring-service inschakelen** is ingesteld op **Ja** en **on-premises status verklaring gebruiken** is ingesteld op **Nee**, wordt het beheer punt gebruikt de Cloud service voor apparaatstatusverklaring.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>De OMS-connector gebruiken voor Microsoft Azure Government Cloud
Met deze technische preview kunt u nu de Microsoft Operations Management Suite (OMS)-connector gebruiken om verbinding te maken met een OMS-werk ruimte die zich op Microsoft Azure Government Cloud bevindt.  

Als u dit wilt doen, wijzigt u een configuratie bestand zodat dit verwijst naar de Government Cloud en installeert u de OMS-connector.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Een OMS-connector instellen voor Microsoft Azure Government Cloud
1. Op elke computer waarop de Configuration Manager-console is geïnstalleerd, bewerkt u het volgende configuratie bestand zodat dit verwijst naar de Government Cloud: *** &lt;cm-installatiepad> \adminconsole\bin\microsoft.configurationmanagmenet.exe.config***

   **Bewerkingen**

   Wijzig de waarde voor de naam van de instelling *FairFaxArmResourceID* gelijk is aan '<https://management.usgovcloudapi.net/">

   - **Origineel:** &lt;setting name = "FairFaxArmResourceId" serializeAs = "string" >   
     &lt;waarde>&lt;/value>   
     &lt;/setting>

   - **Aangepast**     
     &lt;setting name = "FairFaxArmResourceId" serializeAs = "string" > &lt;waarde><https://management.usgovcloudapi.net/&lt;/value>>  
     &lt;/setting>

   Wijzig de waarde voor de naam van de instelling *FairFaxAuthorityResource* gelijk<https://login.microsoftonline.com/>is aan

   - **Origineel:** &lt;setting name = "FairFaxAuthorityResource" serializeAs = "string" >   
     &lt;waarde>&lt;/value>

   - **Bewerkt:** &lt;setting name = "FairFaxAuthorityResource" serializeAs = "string" >   
     &lt;waarde><https://login.microsoftonline.com/&lt;/value>>

2. Nadat u het bestand met de twee wijzigingen hebt opgeslagen, start u de Configuration Manager-console op dezelfde computer opnieuw op en gebruikt u die console om de OMS-connector te installeren. Als u de connector wilt installeren, gebruikt u de gegevens in [synchronisatie gegevens van Configuration Manager naar de Microsoft Operations Management Suite](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm)en selecteert u de **Operations Management Suite-werk ruimte** die zich op de Microsoft Azure Government Cloud bevindt.

3. Nadat de OMS-connector is geïnstalleerd, is de verbinding met de Government Cloud beschikbaar wanneer u een console gebruikt die verbinding maakt met de site.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Android-en iOS-versies zijn niet meer doelwitbaar in wizards voor het maken van hybride MDM

Vanaf deze Technical Preview voor hybride Mobile Device Management (MDM) hoeft u niet langer specifieke versies van Android en iOS te richten bij het maken van nieuwe beleids regels en profielen voor apparaten die door intune worden beheerd. In plaats daarvan kiest u een van de volgende typen apparaten:

- Android
- Samsung KNOX Standard 4,0 en hoger
- iPhone
- iPad

Deze wijziging is van invloed op de wizards voor het maken van de volgende items:

- Configuratie-items
- Compliance beleidsregels
- Certificaatprofielen
- E-mailprofielen
- VPN-profielen
- Wi-Fi-profielen

Met deze wijziging kunnen hybride implementaties sneller ondersteuning bieden voor nieuwe Android-en iOS-versies, zonder dat er een nieuwe Configuration Manager versie of uitbrei ding nodig is. Wanneer een nieuwe versie wordt ondersteund in intune standalone, kunnen gebruikers hun mobiele apparaten upgraden naar die versie.

Om problemen te voor komen bij het uitvoeren van een upgrade van eerdere versies van Configuration Manager, zijn de versies van het mobiele besturings systeem nog steeds beschikbaar op de pagina eigenschappen van deze items. Als u nog steeds een specifieke versie nodig hebt, kunt u het nieuwe item maken en vervolgens de doel versie opgeven op de pagina eigenschappen van het zojuist gemaakte item.
