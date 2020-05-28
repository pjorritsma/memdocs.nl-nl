---
title: Hotfix-installatie programma
titleSuffix: Configuration Manager
description: Ontdek wanneer en hoe u updates installeert via het installatie programma voor hotfixes voor Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a8eed671b723091f2a43350f42ca82d90e0d9da3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906135"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-configuration-manager"></a>Het installatie programma voor hotfixes gebruiken om updates te installeren voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Sommige updates voor Configuration Manager zijn niet beschikbaar in de micro soft-Cloud service en worden alleen out-of-band verkregen. Een voorbeeld is een beperkt uitgegeven hotfix voor een specifiek probleem.   
Wanneer u een update (of hotfix) die u van micro soft ontvangt, moet installeren en die update een bestands naam heeft die eindigt op de extensie **. exe** (niet **Update. exe**), gebruikt u het installatie programma voor hotfixes dat is opgenomen in die hotfix downloaden om de update rechtstreeks op de site server van Configuration Manager te installeren.  

Als het hotfixbestand de bestands extensie **. update. exe** heeft, raadpleegt u [het hulp programma Registratie bijwerken om hotfixes te importeren in Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
> In dit onderwerp vindt u algemene richt lijnen voor het installeren van hotfixes die Configuration Manager bijwerken. Raadpleeg voor meer informatie over specifieke updates het betreffende Knowledge Base-artikel op Microsoft Ondersteuning.  

##  <a name="overview-of-hotfixes-for-configuration-manager"></a><a name="bkmk_Overview"></a>Overzicht van hotfixes voor Configuration Manager  
Hotfixes voor Configuration Manager zijn vergelijkbaar met die voor andere micro soft-producten, zoals SQL Server, bevatten één afzonderlijke correctie of een bundel (een samen stelling van oplossingen) en worden beschreven in een micro soft Knowledge Base-artikel.  

Afzonderlijke updates bevatten één gerichte update voor een specifieke versie van Configuration Manager.  
Update bundels bevatten meerdere updates voor een specifieke versie van Configuration Manager.  
Als een update als bundel wordt aangeboden, kunt u geen afzonderlijke updates uit die bundel installeren.  

Als u echter implementaties wilt maken om updates op extra computers te installeren, moet u de updatebundel installeren op de server van een centrale beheersite of op een primaire siteserver.  

Wanneer u de updatebundel uitvoert, gebeurt het volgende:  

- De updatebestanden voor elk toepasselijk onderdeel van de updatebundel worden uitgepakt.  

- Er wordt een wizard gestart die u door het configuratieproces en de implementatieopties voor de updates leidt.  

- Zodra u de wizard hebt voltooid, worden de updates in de bundel die van toepassing is op siteserver geïnstalleerd op de betreffende siteserver.  

De wizard maakt ook implementaties die u kunt gebruiken voor de installatie van updates op extra computers. U kunt de updates op aanvullende computers implementeren met een ondersteunde implementatiemethode, zoals een software-implementatiepakket of Microsoft System Center Updates Publisher 2011.  

Wanneer de wizard wordt uitgevoerd, wordt een **CAB** -bestand gemaakt op de siteserver dat kan worden gebruikt met Updates Publisher 2011. Eventueel kunt u de wizard ook zodanig configureren dat er één of meer pakketten worden gemaakt voor software-implementatie. U kunt deze implementaties gebruiken om updates te installeren op onderdelen, zoals clients of de Configuration Manager-console. U kunt updates ook hand matig installeren op computers waarop de Configuration Manager-client niet wordt uitgevoerd.  

De volgende drie groepen in Configuration Manager kunnen worden bijgewerkt:  

- Configuration Manager server functies, zoals:  

  - Centrale beheersite  

  - Primaire site  

  - Secundaire site  

  - Externe SMS-provider  

- Configuration Manager-console  

- Configuration Manager-client  

> [!NOTE]  
> **Updates voor sitesysteemrollen** (inclusief updates voor de sitedatabase en de clouddistributiepunten) worden geïnstalleerd als onderdeel van de update voor siteservers en services van de Site Component Manager.  
>   
> Updates voor pull-distributiepunten worden echter afgehandeld door de distributiebeheerder in plaats van de Site Component Manager.  

Elke update bundel voor Configuration Manager is een zelfuitpakkend uitvoerbaar. exe-bestand (SFX) dat de benodigde bestanden bevat voor het installeren van de update op de betreffende onderdelen van Configuration Manager. Het SFX-bestand kan normaal gesproken de volgende bestanden bevatten:  

|File|Details|  
|----------|-------------|  
|&lt;Product versie \> -QFE-KB &lt; KB-artikel-id \> - &lt; platform \> - &lt; taal \> . exe|Dit is het updatebestand. De opdrachtregel voor dit bestand wordt beheerd door Updatesetup.exe.<br /><br /> Bijvoorbeeld:<br />CM1511RTM-QFE-KB123456-X64-ENU. exe|  
|Updatesetup.exe|Deze MSI-wrapper beheert de installatie van de updatebundel.<br /><br /> Wanneer u de update uitvoert, detecteert Updatesetup.exe de weergavetaal van de computer waarop hij wordt uitgevoerd. De gebruikersinterface voor de update is standaard in het Engels. Wanneer de weergavetaal echter wordt ondersteund, geeft de gebruikersinterface inhoud in de lokale taal van de computer weer.|  
|License_&lt;taal\>.rtf|Wanneer van toepassing bevat iedere update een of meerdere licentiebestanden voor ondersteunde talen.|  
|&lt;Product&updatetype>- &lt; product versie \> - &lt; KB-artikel-id \> - &lt; platform \> . msp|Als de update van toepassing is op de Configuration Manager-console of-clients, bevat de update bundel afzonderlijke Windows Installer patch-bestanden (. msp).<br /><br /> Bijvoorbeeld:<br /><br /> **Configuration Manager-console-update:** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Client update:** ConfigMgr1511-client-KB1234567-i386. msp<br />ConfigMgr1511-client-KB1234567-x64. msp|  

De updatebundel registreert standaard zijn bewerkingen in een logboekbestand op de siteserver. Het logboekbestand heeft dezelfde naam als de updatebundel en wordt naar de map **%SystemRoot%/Temp** geschreven.  

Wanneer u de updatebundel uitvoert, pakt deze een bestand uit met dezelfde naam als de updatebundel in een tijdelijke map op de computer en voert Updatesetup.exe uit. Updatesetup. exe start de wizard software-update voor Configuration Manager &lt; product versie \> &lt; KB-nummer \> .  

Afhankelijk van het bereik van de update maakt de wizard een aantal mappen aan onder de installatiemap Configuration Manager op de site server. De mapstructuur lijkt op het volgende:   
** \\ \\ &lt; Server naam \> \ SMS_ &lt; site code \> \Hotfix \\ &lt; KB number \> \\ &lt; Update type \> \\ &lt; platform \> **.  

De volgende tabel biedt details over de mappen in de mapstructuur:  

|Mapnaam|Meer informatie|  
|-----------------|----------------------|  
|&lt;Servernaam\>|Dit is de naam van de siteserver waar u de updatebundel uitvoert.|  
|SMS_- &lt; site code\>|Dit is de share naam van de installatiemap van Configuration Manager.|  
|&lt;KB-nummer\>|Dit is het ID-nummer van het Knowledge Base-artikel voor deze updatebundel.|  
|&lt;Updatetype\>|Dit zijn de soorten updates voor Configuration Manager. De wizard maakt een afzonderlijke map aan voor ieder soort update in de updatebundel. De mapnamen staan voor de update-typen. Dit zijn onder meer de volgende:<br /><br /> **Server**: bevat updates voor site servers, site database servers en computers waarop de SMS-provider wordt uitgevoerd.<br /><br /> **Client**: bevat updates voor de Configuration Manager-client.<br /><br /> **AdminConsole**: bevat updates voor de Configuration Manager-console<br /><br /> Naast de update-typen hierboven wordt met de wizard nog een map met de naam **SCUP** gemaakt. Deze map staat niet voor een type update, maar bevat het CAB-bestand voor Updates Publisher.|  
|&lt;Platform\>|Dit is een platform-specifieke map. Deze bevat update-bestanden die specifiek zijn voor een type processor.  Deze mappen zijn onder andere:<br /><br />-x64<br /><br /> -I386|  

##  <a name="how-to-install-updates"></a><a name="bkmk_Install"></a> Updates installeren  
Voor de installatie van updates moet u eerst de updatebundel installeren op een siteserver. Wanneer u een updatebundel installeert, wordt er een installatiewizard gestart voor die update. Deze wizard doet het volgende:  

- De updatebestanden uitpakken  

- Helpen bij de configuratie van implementaties  

- De betreffende updates op de serveronderdelen van de lokale computer installeren  

Nadat u de update bundel op een site server hebt geïnstalleerd, kunt u aanvullende onderdelen voor Configuration Manager bijwerken. In de volgende tabel staan updatebewerkingen voor deze verschillende onderdelen:  

|Onderdeel|Instructies|  
|---------------|------------------|  
|Siteserver|Implementeer updates op een externe siteserver wanneer u de updatebundel niet direct op die externe siteserver wilt installeren.|  
|Sitedatabase|Implementeer voor externe siteservers die serverupdates die een update bevatten van de sitedatabase als u de updatebundel niet direct op die externe siteserver installeert.|  
|Configuration Manager-console|Na de eerste installatie van de Configuration Manager-console kunt u updates voor de Configuration Manager-console installeren op elke computer waarop de-console wordt uitgevoerd. U kunt de installatie bestanden van de Configuration Manager-console niet wijzigen voor het Toep assen van de updates tijdens de eerste installatie van de-console.|  
|Externe SMS-provider|Installeer updates voor ieder exemplaar van de SMS-provider dat op een computer wordt uitgevoerd die niet de siteserver is waar u de updatebundel hebt geïnstalleerd.|  
|Configuration Manager-clients|Na de eerste installatie van de Configuration Manager-client, kunt u updates voor de Configuration Manager-client installeren op elke computer waarop de-client wordt uitgevoerd.|  

> [!NOTE]  
> U kunt updates alleen implementeren op computers waarop de Configuration Manager-client wordt uitgevoerd.  

Als u een client, Configuration Manager-console of SMS-provider opnieuw installeert, moet u ook de updates voor deze onderdelen opnieuw installeren.  

Gebruik de informatie in de volgende secties om updates te installeren voor elk van de onderdelen voor Configuration Manager.  

###  <a name="update-servers"></a><a name="bkmk_servers"></a> Updateservers  
Updates voor servers kunnen updates zijn voor **sites**, de **site database**en computers waarop een exemplaar van de SMS- **provider**wordt uitgevoerd:  

####  <a name="update-a-site"></a><a name="bkmk_site"></a>Een site bijwerken  
Als u een Configuration Manager site wilt bijwerken, kunt u de update bundel rechtstreeks op de site server installeren of u kunt de updates implementeren op een site server nadat u de update bundel op een andere site hebt geïnstalleerd.  

Als u een update installeert op een siteserver, beheert het update-installatieproces aanvullende bewerkingen die nodig zijn om de update toe te passen, zoals het bijwerken van sitesysteemrollen. De uitzondering hierop is de sitedatabase. De volgende rubrieken bevatten informatie over hoe u de sitedatabase kunt bijwerken.  

####  <a name="update-a-site-database"></a><a name="bkmk_database"></a>Een site database bijwerken  
Voor het bijwerken van de sitedatabase, voert het installatieproces een bestand met de naam **update.sql** uit op de sitedatabase. U kunt het updateproces instellen op het automatisch bijwerken van de sitedatabase of u kunt dit later zelf handmatig doen.  

**Automatische update van de site database**  

Wanneer u de updatebundel op een siteserver installeert, kunt u de sitedatabase automatisch laten bijwerken wanneer de serverupdate wordt geïnstalleerd. U kunt dit alleen doen voor de siteserver waar u de updatebundel installeert en geldt niet voor implementaties voor het installeren van updates op externe siteservers.  

> [!NOTE]  
> Als u ervoor kiest de sitedatabase automatisch te laten bijwerken, werkt het proces een database bij ongeacht of de database zich op de siteserver bevindt of op een externe computer.  

> [!IMPORTANT]  
> Maak voordat u de sitedatabase bijwerkt een back-up van de sitedatabase. U kunt een update van de sitedatabase niet verwijderen. Zie [back-up en herstel voor Configuration Manager](backup-and-recovery.md)voor informatie over het maken van een back-up voor Configuration Manager.  

**Handmatige update van de sitedatabase**  

Als u ervoor kiest de sitedatabase niet automatisch te laten bijwerken wanneer u de updatebundel installeert op de siteserver, wijzigt de serverupdate de database op de siteserver waarop de updatebundel wordt uitgevoerd niet. Bij implementaties waarvoor het pakket wordt gebruikt dat is gemaakt voor software-implementatie of waarmee wordt geïnstalleerd, wordt de sitedatabase altijd bijgewerkt.  

> [!WARNING]  
> Wanneer de update updates bevat voor zowel de siteserver als de sitedatabase, is de update niet functioneel totdat de update is voltooid voor zowel de siteserver als de sitedatabase. De site wordt niet ondersteund totdat de update is toegepast op de sitedatabase.  

**Een site database hand matig bijwerken:**  

1.  Op de siteserver zet u de service SMS_SITE_COMPONENT_MANAGER stop en daarna zet u de service SMS_EXECUTIVE stop.  

2.  Sluit de Configuration Manager-console.  

3.  Voer het updatescript **update.sql** uit op de database van die site. Voor informatie over het uitvoeren van een script om een SQL Server-database bij te werken, raadpleegt u de documentatie voor de SQL Server-versie die u voor de databaseserver van uw site gebruikt.  

4.  Start de services die tijdens de vorige stappen zijn gestopt opnieuw op.  

5.  Wanneer de update bundel wordt geïnstalleerd, wordt **Update. SQL** naar de volgende locatie op de site server geëxtraheerd: ** \\ \\ &lt; Server naam \> \ SMS_ &lt; site code \> \Hotfix KB- \\ &lt; nummer \> \Update.SQL**  

####  <a name="update-a-computer-that-runs-the-sms-provider"></a><a name="bkmk_provider"></a>Een computer bijwerken waarop de SMS-provider wordt uitgevoerd  
Wanneer u een updatebundel installeert met updates voor de SMS-provider, moet u de update voor elke computer implementeren waarop de SMS-provider draait. De enige uitzondering hierop is het exemplaar van de SMS-provider dat voorheen op de siteserver was geïnstalleerd, waarop u de updatebundel installeert. Het lokale exemplaar van de SMS-provider op de siteserver wordt bijgewerkt wanneer u de updatebundel installeert.  

Als u de SMS-provider eerst verwijdert en opnieuw installeert op een computer, moet u de update voor de SMS-provider op die computer opnieuw installeren.  

###  <a name="update-clients"></a><a name="BKMK_clients"></a>Clients bijwerken  
Wanneer u een update installeert die updates bevat voor de Configuration Manager-client, krijgt u de optie om clients automatisch te upgraden met de installatie van de update of om clients op een later tijdstip hand matig bij te werken. Zie [clients voor Windows-computers bijwerken voor](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md)meer informatie over automatische client upgrade.  

U kunt updates implementeren met Updates Publisher of een software-implementatiepakket. Ook kunt u ervoor kiezen om een update handmatig op elke client te installeren. Zie de sectie [Updates implementeren voor Configuration Manager](#BKMK_Deploy) in dit onderwerp voor meer informatie over het gebruik van implementaties voor het installeren van updates.  

> [!IMPORTANT]  
> Zorg ervoor, wanneer u updates installeert voor clients en de updatebundel updates voor servers bevat, dat u de serverupdates tevens op de primaire site installeert waaraan de clients zijn toegewezen.  

Als u de client update hand matig wilt installeren op elke Configuration Manager-client, moet u **Msiexec. exe** uitvoeren en verwijzen naar het platformspecifieke client update. msp-bestand.  

U kunt bijvoorbeeld de volgende opdrachtregel gebruiken voor een clientupdate. Met deze opdracht regel wordt Msiexec op de client computer uitgevoerd en wordt gerefereerd aan het MSP-bestand dat de update bundel op de site server heeft uitgepakt: **Msiexec. exe/p \\ \\ &lt; Server naam \> \ SMS_ &lt; site \> \\ &lt; code \Hotfix KB number \> \Client \\ &lt; platform \> \\ &lt; MSP \> /l \* v &lt; logbestand \> REINSTALLMODE = Mous reinstall = all**  

###  <a name="update-configuration-manager-consoles"></a><a name="BKMK_console"></a>Configuration Manager-consoles bijwerken  
Als u een Configuration Manager-console wilt bijwerken, moet u de update installeren op de computer waarop de-console wordt uitgevoerd nadat de installatie van de console is voltooid.  

> [!IMPORTANT]  
> Zorg ervoor, wanneer u updates installeert voor de Configuration Manager-console en de update bundel updates bevat voor servers, dat u de server updates ook installeert op de site die u gebruikt met de Configuration Manager-console.  

Als de computer die u bijwerkt, de Configuration Manager-client uitvoert:  

- u kunt een implementatie gebruiken om de update te installeren. Zie de sectie [Updates implementeren voor Configuration Manager](#BKMK_Deploy) in dit onderwerp voor meer informatie over het gebruik van implementaties voor het installeren van updates.  

- Als u zich hebt aangemeld op de clientcomputer, kunt u de installatie interactief uitvoeren.  

- U kunt handmatig de update installeren op elke computer. Als u de Configuration Manager-console-update hand matig wilt installeren op elke computer waarop de Configuration Manager-console wordt uitgevoerd, kunt u Msiexec. exe uitvoeren en verwijzen naar het bestand Configuration Manager console update. msp.  

U kunt bijvoorbeeld de volgende opdracht regel gebruiken om een Configuration Manager-console bij te werken. Met deze opdracht regel wordt Msiexec op de computer uitgevoerd en wordt gerefereerd aan het MSP-bestand dat de update bundel op de site server heeft geëxtraheerd: **Msiexec. exe/p \\ \\ &lt; Server naam \> \ SMS_ &lt; site \> \\ &lt; code \Hotfix KB number \> \AdminConsole \\ &lt; platform \> \\ &lt; MSP \> /l \* v &lt; logbestand \> REINSTALLMODE = Mous reinstall = all**  

##  <a name="deploy-updates-for-configuration-manager"></a><a name="BKMK_Deploy"></a> Updates implementeren voor Configuration Manager  
Wanneer u de updatebundel op een siteserver installeert, kunt u een van de volgende drie methoden gebruiken om updates te implementeren op extra computers.  

###  <a name="use-updates-publisher-2011-to-install-updates"></a><a name="BKMK_DeploySCUP"></a>Updates Publisher 2011 gebruiken om updates te installeren  
Wanneer u de updatebundel op een siteserver installeert, maakt de installatiewizard een catalogusbestand aan voor Updates Publisher dat u kunt gebruiken om de updates op de toepasselijke computers te implementeren. De wizard maakt deze catalogus altijd, zelfs wanneer u de optie **pakket en programma gebruiken om deze update te implementeren**selecteert.  

De catalogus voor updates Publisher heet **bestand scupcatalog. cab** en is te vinden op de volgende locatie op de computer waarop de update bundel wordt uitgevoerd: ** \\ \\ &lt; Server naam \> \ SMS_ &lt; site \> code \Hotfix \\ &lt; KB-nummer \> \SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
> Omdat het bestand SCUPCatalog.cab wordt gemaakt door gebruik te maken van paden die specifiek zijn voor de siteserver waarop de updatebundel is geïnstalleerd, kan het niet op andere siteservers worden gebruikt.  

Nadat de wizard is voltooid, kunt u de catalogus importeren in updates Publisher en vervolgens Configuration Manager software-updates gebruiken om de updates te implementeren. Zie [updates publisher 2011](https://docs.microsoft.com/previous-versions/system-center/updates-publisher-2011/hh134742(v=technet.10))voor informatie over updates Publisher.  

Gebruik de volgende procedure om het bestand SCUPCatalog.cab te importeren in Updates Publisher en de updates te publiceren.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>De updates importeren in Updates Publisher 2011  

1.  Start de updates Publisher-console en klik op **importeren**.  

2.  Selecteer op de pagina **Importtype** van de wizard Catalogus software-updates importeren **Het pad opgeven naar de te importeren catalogus**, en geef vervolgens het bestand SCUPCatalog.cab op.  

3.  Klik op **Volgende** en weer op **Volgende**.  

4.  Klik in het dialoogvenster **Beveiligingswaarschuwing - Validatie catalogus** op **Accepteren**. Sluit de wizard nadat deze is voltooid.  

5.  Selecteer in de Updates Publisher-console de update die u wilt implementeren en klik op **Publiceren**.  

6.  Selecteer op de pagina **opties publiceren** van de wizard software-updates publiceren **volledige inhoud**en klik vervolgens op **volgende**.  

7.  Voer de wizard uit om de updates te publiceren.  

###  <a name="use-software-deployment-to-install-updates"></a><a name="BKMK_DeploySWDist"></a>Software-implementatie gebruiken om updates te installeren  
Wanneer u de updatebundel op de siteserver van een primaire site of een centrale beheersite installeert, kunt u de installatiewizard configureren om updatepakketten te maken voor software-implementatie. U kunt vervolgens elk pakket implementeren op een verzameling van computers die u wilt bijwerken.  

Als u een software-implementatiepakket wilt maken, schakelt u op de pagina **Implementatie software-update configureren** van de wizard het selectievakje in voor elk updatepakkettype dat u wilt bijwerken. De beschik bare typen kunnen servers, Configuration Manager-consoles en clients zijn. Er wordt voor elk door u geselecteerde type update een apart pakket gemaakt.  

> [!NOTE]  
> Het pakket voor servers bevat updates voor de volgende onderdelen:  
>   
> - Siteserver  
> - SMS-provider  
> - Sitedatabase  

Daarna selecteert u op de pagina **Implementatiemethode software-updates configureren** van de wizard de optie **Ik gebruik softwaredistributie**. Deze selectie stelt de wizard in om de software-implementatiepakketten te maken.  

Nadat de wizard is voltooid, kunt u de pakketten weer geven die worden gemaakt in de Configuration Manager-console in het knoop punt **pakketten** in de werk ruimte **software bibliotheek** . U kunt vervolgens uw standaard proces gebruiken om software pakketten te implementeren om clients te Configuration Manager. Wanneer een pakket wordt uitgevoerd op een client, worden de updates geïnstalleerd op de toepasselijke onderdelen van Configuration Manager op de client computer.  

Zie [pakketten en Program ma's](../../../apps/deploy-use/packages-and-programs.md)voor meer informatie over het implementeren van pakketten naar Configuration Manager-clients.  

###  <a name="create-collections-for-deploying-updates-to-configuration-manager"></a><a name="BKMK_DeployCollections"></a>Verzamelingen maken voor het implementeren van updates voor Configuration Manager  
U kunt specifieke updates implementeren naar toepasselijke clients. De volgende informatie kan u helpen om verzamelingen te maken voor de verschillende onderdelen voor Configuration Manager.  

|Onderdeel van Configuration Manager|Instructies|  
|----------------------------------------|------------------|  
|Server centrale beheersite|Maak een directe lidmaatschapquery en voeg de servercomputer van de centrale beheersite toe.|  
|Alle primaire siteservers|Maak een directe lidmaatschapquery en voeg de servercomputer van elke primaire site toe.|  
|Alle secundaire siteservers|Maak een directe lidmaatschapquery en voeg de servercomputer van elke secundaire site toe.|  
|Alle x 86-clients|Maak een verzameling met de volgende querycriteria:<br /><br /> **Selecteer \* in SMS_R_System inner join SMS_G_System_SYSTEM op SMS_G_System_SYSTEM. ResourceID = SMS_R_System. ResourceId waarbij SMS_G_System_SYSTEM. System type = "op x86 gebaseerde PC"**|  
|Alle x 64-clients|Maak een verzameling met de volgende querycriteria:<br /><br /> **Selecteer \* in SMS_R_System inner join SMS_G_System_SYSTEM op SMS_G_System_SYSTEM. ResourceID = SMS_R_System. ResourceId waarbij SMS_G_System_SYSTEM. System type = "op x64 gebaseerde PC"**|  
|Alle computers waarop de Configuration Manager-console wordt uitgevoerd|Maak een directe lidmaatschapquery en voeg elke computer toe.|  
|Externe computers waarop een exemplaar van de SMS-provider wordt uitgevoerd|Maak een directe lidmaatschapquery en voeg elke computer toe.|  

> [!NOTE]  
> Implementeer de update op de siteserver van de site voor het bijwerken van een sitedatabase.  

Zie [verzamelingen maken](../../../core/clients/manage/collections/create-collections.md)voor meer informatie over het maken van verzamelingen.  
