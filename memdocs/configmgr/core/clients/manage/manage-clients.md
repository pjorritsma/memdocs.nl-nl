---
title: Clients beheren
titleSuffix: Configuration Manager
description: Meer informatie over het beheren van clients in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d7697f8b5a2017aa732c52512bf31598c070fbc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714876"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Clients beheren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer de Configuration Manager-client op een apparaat wordt geïnstalleerd en is toegewezen aan een-site, wordt het apparaat weer geven in de werk ruimte **activa en naleving** in het knoop punt **apparaten** en in een of meer verzamelingen in het knoop punt **apparaat Collections** . Selecteer het apparaat of een verzameling en voer vervolgens beheer bewerkingen uit. Er zijn echter andere manieren om de client te beheren, die mogelijk andere werk ruimten in de-console omvat, of taken buiten de-console.  

> [!NOTE]  
> Als u de Configuration Manager-client installeert, maar deze nog niet is toegewezen aan een site, wordt deze mogelijk niet weer gegeven in de console. Nadat de client aan een site is toegewezen, het lidmaatschap van de verzameling bij te werken en de weer gave van de console te vernieuwen.  
>
> Een apparaat kan ook worden weer gegeven in de console wanneer de Configuration Manager-client niet is geïnstalleerd. Dit probleem treedt op als de site een apparaat detecteert, maar de-client niet is geïnstalleerd en toegewezen.
>
> Mobiele apparaten die worden beheerd met de [Exchange Server-connector](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) of [on-premises MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) , installeren de Configuration Manager-client niet.  
>
> Als u een apparaat wilt beheren vanaf de-console, gebruikt u de kolom **client** in het knoop punt **apparaten** om te bepalen of de-client is geïnstalleerd.  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a>Clients beheren vanaf het knoop punt **apparaten**  

Afhankelijk van het apparaattype, kunnen sommige van deze opties niet beschikbaar zijn.  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **apparaten** .  

2. Selecteer een of meer apparaten en selecteer vervolgens een van deze client beheer taken op het lint. U kunt ook met de rechter muisknop op het apparaat klikken.)  

### <a name="import-user-device-affinity"></a>Gebruikers affiniteit apparaat importeren

Configureer de koppelingen tussen gebruikers en apparaten, zodat u software efficiënt kunt implementeren voor gebruikers.  

Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.

### <a name="import-computer-information"></a>Computer gegevens importeren

Start de **wizard computer gegevens importeren** om nieuwe computer gegevens in de Configuration Manager-Data Base te importeren. U kunt meerdere computers importeren met behulp van een bestand of informatie opgeven voor één computer.

### <a name="add-selected-items"></a>Geselecteerde items toevoegen

Biedt de volgende opties:

- **Geselecteerde items toevoegen aan de bestaande verzameling apparaten**: Hiermee opent u het dialoog venster **verzameling selecteren** . Selecteer de verzameling waaraan u dit apparaat wilt toevoegen. Het apparaat is opgenomen in deze verzameling met behulp van een regel voor **direct** lidmaatschap.  

- **Geselecteerde items toevoegen aan de nieuwe verzameling apparaten**: Hiermee opent u de **wizard apparaatbesturing maken** , waarin u een nieuwe verzameling kunt maken. De geselecteerde verzameling is opgenomen in deze verzameling met behulp van een regel voor **direct** lidmaatschap.  

Zie [verzamelingen maken](collections/create-collections.md)voor meer informatie.

### <a name="install-client"></a>Client installeren

Hiermee opent u de **wizard Client installeren**. Deze wizard maakt gebruik van client push installatie om de Configuration Manager-client op het geselecteerde apparaat te installeren of opnieuw te installeren.

> [!TIP]  
> Er zijn veel verschillende manieren om de Configuration Manager-client te installeren. Hoewel de wizard Client push een handige client installatie methode van de-console biedt, heeft deze methode veel afhankelijkheden en is deze niet geschikt voor alle omgevingen. Zie [vereisten voor het implementeren van clients op Windows-computers](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation)voor meer informatie over de afhankelijkheden. Zie [client installatie methoden](../deploy/plan/client-installation-methods.md)voor meer informatie over de andere client installatie methoden.

Zie [Configuration Manager-clients installeren met behulp van client push](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)voor meer informatie.

### <a name="run-script"></a>Script uitvoeren

Hiermee opent u de wizard **script uitvoeren** om een Power shell-script uit te voeren op het geselecteerde apparaat.

Zie [Power shell-scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie.

### <a name="install-application"></a>Toepassing installeren

Een toepassing in realtime installeren op een apparaat. Met deze functie kunt u de nood zaak van afzonderlijke verzamelingen voor elke toepassing verminderen.

Zie [toepassingen voor een apparaat installeren](../../../apps/deploy-use/install-app-for-device.md)voor meer informatie.

### <a name="reassign-site"></a>Site opnieuw toewijzen

Wijs één of meerdere klanten, waaronder beheerde mobiele apparaten, toe aan een andere primaire site in de hiërarchie. U kunt afzonderlijke clients opnieuw toewijzen of meerdere selecteren om ze bulksgewijs opnieuw toe te wijzen.  

### <a name="client-settings---resultant-client-settings"></a>Client instellingen-resulterende client instellingen

Wanneer u meerdere client instellingen op hetzelfde apparaat implementeert, zijn de prioriteiten en combi natie van instellingen complex. Gebruik deze optie om de resulterende verzameling client instellingen weer te geven die op dit apparaat zijn geïmplementeerd.

Zie [client instellingen configureren](../deploy/configure-client-settings.md)voor meer informatie.

### <a name="start"></a>Starten

- Voer **resource Explorer** uit om de hardware-en software-inventarisatie gegevens van een Windows-client te bekijken. Raadpleeg voor meer informatie de volgende artikelen:

  - [Resource Explorer gebruiken om hardware-inventaris weer te geven](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [Resource Explorer gebruiken om software-inventaris weer te geven](inventory/use-resource-explorer-to-view-software-inventory.md)

- Beheer het apparaat op afstand met behulp van **extern beheer**, **hulp op afstand**of **extern bureaublad client**. Zie [een Windows-client computer op afstand beheren](remote-control/remotely-administer-a-windows-client-computer.md)voor meer informatie.

### <a name="approve"></a>Goedkeuren

Wanneer de client communiceert met site systemen met behulp van HTTP en een zelfondertekend certificaat, moet u deze clients goed keuren om ze als vertrouwde computers te identificeren. Standaard keurt de site configuratie automatisch clients goed van hetzelfde Active Directory forest en vertrouwde forests. Dit standaard gedrag betekent dat u niet elke client hand matig hoeft goed te keuren. Computers die u vertrouwt hand matig goed keuren en andere niet-goedgekeurde computers die u vertrouwt.

> [!IMPORTANT]  
> Hoewel sommige beheer functies kunnen werken voor niet-goedgekeurde clients, is dit een niet-ondersteund scenario voor Configuration Manager.  

U hoeft geen clients goed te keuren die altijd communiceren met site systemen met behulp van HTTPS, of clients die een PKI-certificaat gebruiken wanneer ze communiceren met site systemen met behulp van HTTP. Deze clients maken vertrouwen met behulp van de PKI-certificaten.

### <a name="block-or-unblock"></a>Blok keren of deblokkeren

Blok keer een client die u niet meer vertrouwt. Als u blokkeert, kan de client geen beleid ontvangen en kunnen site systemen niet communiceren met de client.  

> [!IMPORTANT]  
> Het blok keren van een client voor komt alleen dat communicatie tussen de client en Configuration Manager site systemen. De communicatie met andere apparaten wordt niet voor komen. Wanneer de client communiceert met site systemen door gebruik te maken van HTTP in plaats van HTTPS, zijn er enkele beveiligings beperkingen.  

U kunt ook de blok kering van een geblokkeerde client opheffen.

Zie [bepalen of clients moeten worden geblokkeerd](../deploy/plan/determine-whether-to-block-clients.md)voor meer informatie.

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>Vereiste PXE-implementaties wissen

U kunt een vereiste PXE-implementatie opnieuw implementeren door de status te wissen van de laatste PXE-implementatie die is toegewezen aan een Configuration Manager verzameling of een computer. Met deze actie wordt de status van die implementatie opnieuw ingesteld en worden de meest recente vereiste implementaties opnieuw geïnstalleerd.

Zie [PXE gebruiken om Windows via het netwerk te implementeren](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)voor meer informatie.

### <a name="client-notification"></a>Clientmeldingen

Zie [client meldingen](client-notification.md#client-notification)voor meer informatie.

### <a name="endpoint-protection"></a>Endpoint Protection

Zie [client meldingen](client-notification.md#endpoint-protection)voor meer informatie.

### <a name="edit-primary-users"></a>Primaire gebruikers bewerken

Gebruikers van dit apparaat weer geven in de afgelopen 90 dagen of de primaire gebruikers van dit apparaat opgeven.

Zie [gebruikers en apparaten koppelen met gebruikers affiniteit met apparaat](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)voor meer informatie.

### <a name="wipe-a-mobile-device"></a>Een mobiel apparaat wissen

U kunt mobiele apparaten wissen die de wisopdracht ondersteunen. Met deze actie worden alle gegevens op het mobiele apparaat permanent verwijderd, met inbegrip van persoonlijke instellingen en persoonlijke gegevens. Typisch zet deze actie het mobiele apparaat terug naar zijn fabrieksinstellingen. Een mobiel apparaat wissen wanneer het niet meer wordt vertrouwd. Bijvoorbeeld als het apparaat is vermist of gestolen.  

> [!TIP]  
> Raadpleeg de documentatie van de fabrikant voor meer informatie over hoe het mobiele apparaat een opdracht voor Extern wissen verwerkt.  

Er is vaak een vertraging tot het mobiele apparaat de opdracht wissen ontvangt:  

- Als het mobiele apparaat is geregistreerd door Configuration Manager, ontvangt de client de opdracht wanneer het client beleid wordt gedownload.

- Als het mobiele apparaat wordt beheerd door de Exchange Server-connector, ontvangt het de opdracht als deze wordt gesynchroniseerd met Exchange.  

Als u wilt controleren wanneer het apparaat de opdracht wissen ontvangt, gebruikt u de kolom **status wissen** . U kunt de opdracht wissen annuleren totdat het apparaat een bevestiging van wissen naar Configuration Manager verstuurt.  

### <a name="retire-a-mobile-device"></a>Een mobiel apparaat buiten gebruik stellen

De optie **buiten gebruik stellen** wordt alleen ondersteund door mobiele apparaten die zijn Inge schreven door on-premises MDM.  

Zie [Help uw gegevens beschermen met wissen op afstand, vergren delen op afstand of wachtwoord code opnieuw instellen](../../../mdm/deploy-use/wipe-lock-reset-devices.md)voor meer informatie.

### <a name="change-ownership"></a>Eigendom wijzigen

Als een apparaat niet is toegevoegd aan een domein en de Configuration Manager-client niet is geïnstalleerd, gebruikt u deze optie om het eigendom van het **bedrijf** of **persoonlijk**te wijzigen.  

U kunt deze waarde gebruiken in toepassings vereisten om implementaties te beheren, en om te bepalen hoeveel inventaris wordt verzameld van apparaten van gebruikers.  

Mogelijk moet u de kolom **eigenaar van apparaat** toevoegen aan de weer gave door met de rechter muisknop op een kolomkop te klikken en deze te kiezen.

### <a name="delete"></a>Verwijderen

> [!WARNING]  
> Verwijder een client niet als u de Configuration Manager-client wilt verwijderen of uit een verzameling wilt verwijderen.  

Met de actie **verwijderen** wordt de client record hand matig verwijderd uit de Configuration Manager-Data Base. Gebruik deze actie alleen om een probleem op te lossen. Als u het object verwijdert maar de-client nog steeds is geïnstalleerd en communiceert met de site, maakt heartbeat-detectie de client record opnieuw. Het wordt weer gegeven in de Configuration Manager-console, hoewel de client geschiedenis en eerdere koppelingen verloren zijn gegaan.  
> [!NOTE]  
> Wanneer u een client voor mobiele apparaten verwijdert die is geregistreerd door Configuration Manager, trekt deze actie ook het uitgegeven PKI-certificaat in. Dit certificaat wordt dan geweigerd door het beheer punt, zelfs als IIS de certificaatintrekkingslijst (CRL) niet controleert.
>
> Certificaten op verouderde mobiele apparaten worden niet ingetrokken wanneer u deze clients wist.

Zie [de Configuration Manager-client verwijderen](#BKMK_UninstalClient)als u de client wilt verwijderen.  

Zie [clients toewijzen aan een site](../deploy/assign-clients-to-a-site.md)om de client toe te wijzen aan een nieuwe primaire site.

Configureer, om de client te verwijderen uit een verzameling, opnieuw de eigenschappen van de verzameling. Zie [verzamelingen beheren](collections/manage-collections.md)voor meer informatie.

### <a name="refresh"></a>Vernieuwen

Vernieuw de weer gave van de console met de meest recente gegevens in de data base. Bijvoorbeeld als een apparaat wordt weer gegeven in de lijst van detectie, maar niet wordt weer gegeven als geïnstalleerd. Selecteer **vernieuwen**nadat u de client hebt geïnstalleerd en er zeker van bent dat deze is toegewezen aan de site.

### <a name="properties"></a>Eigenschappen

Bekijk de detectie gegevens en implementaties die zijn gericht op de client.

U kunt ook variabelen configureren die taken reeksen gebruiken om een besturings systeem te implementeren op het apparaat. Voor meer informatie maakt u [taken reeks variabelen voor apparaten en verzamelingen](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a>Clients beheren vanuit het knoop punt **apparaat verzamelingen**

Veel van de taken die beschikbaar zijn voor apparaten in het knoop punt **apparaten** zijn ook beschikbaar in verzamelingen. De-console past de bewerking automatisch toe op alle in aanmerking komende apparaten in de verzameling. Deze actie voor een volledige verzameling genereert extra netwerk pakketten en verhoogt het CPU-gebruik op de site server.  

Houd rekening met de volgende vragen voordat u taken op verzamelings niveau uitvoert. Zodra de taak is gestart, kunt u deze niet meer stoppen vanaf de-console.

- Hoeveel apparaten bevinden zich in de verzameling?
- Zijn de apparaten verbonden met netwerk verbindingen met een lage band breedte?
- Hoe lang moet deze taak worden voltooid voor alle apparaten?

Zie [verzamelingen beheren](collections/manage-collections.md)voor meer informatie.


## <a name="restart-clients"></a>Clients opnieuw opstarten

Gebruik de Configuration Manager-console om clients te identificeren waarvoor opnieuw moet worden opgestart. Gebruik vervolgens de actie voor client meldingen om ze opnieuw te starten.

> [!Tip]
> Schakel automatische client upgrade in om uw clients up-to-date te houden met minder inspanning. Zie [about Automatic client upgrade](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)(Engelstalig) voor meer informatie.

Als u apparaten wilt identificeren die wachten op opnieuw opstarten, gaat u naar de werk ruimte **activa en naleving** in de Configuration Manager-console en selecteert u het knoop punt **apparaten** . Bekijk vervolgens de status voor elk apparaat in het detail venster in een nieuwe kolom met de naam **opnieuw opstarten in behandeling**. Elk apparaat heeft een of meer van de volgende waarden:

- **Nee**: opnieuw opstarten is niet in behandeling
- **Configuration Manager**: deze waarde is afkomstig van het onderdeel client opnieuw opstarten coördinator (RebootCoordinator. log)
- **Bestands naam wijzigen**: deze waarde is afkomstig van Windows Reporting a Pending File Rename Operation (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
- **Windows Update**: deze waarde is afkomstig van de Windows Update agent die het opnieuw opstarten in behandeling heeft gerapporteerd, is vereist voor een of meer updates (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **Functie toevoegen of verwijderen**: deze waarde is afkomstig van de Windows-service voor het op onderdelen gebaseerde onderhoud het toevoegen of verwijderen van een Windows-functie vereist een herstart (op HKLM\Software\Microsoft\Windows\CurrentVersion\Component gebaseerd Servicing\Reboot in behandeling)

### <a name="create-the-client-notification-to-restart-a-device"></a>De client melding maken om een apparaat opnieuw op te starten

1. Selecteer het apparaat dat u opnieuw wilt opstarten binnen een verzameling in het knoop punt **apparaat verzamelingen** van de-console.
2. Selecteer **client melding**op het lint en selecteer vervolgens **opnieuw opstarten**. Er wordt een informatie venster geopend over het opnieuw opstarten. Selecteer **OK** om de aanvraag opnieuw te starten te bevestigen.

Wanneer de melding door een client wordt ontvangen, wordt een meldings venster voor **Software Center** geopend om de gebruiker op de hoogte te stellen van de herstart. Standaard wordt het opnieuw opstarten na 90 minuten uitgevoerd. U kunt de tijd voor opnieuw opstarten wijzigen door [client instellingen](../deploy/configure-client-settings.md)te configureren. Instellingen voor het gedrag voor opnieuw opstarten vindt u op het tabblad [computer opnieuw opstarten](../deploy/about-client-settings.md#computer-restart) van de standaard instellingen.


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a>De client cache configureren

In de cache van de client worden tijdelijke bestanden opgeslagen voor wanneer clients toepassingen en Program ma's installeren. Software-updates gebruiken ook de client cache, maar proberen altijd te downloaden naar de cache, ongeacht de grootte-instelling. Configureer de cache-instellingen, zoals grootte en locatie, wanneer u de-client hand matig installeert, wanneer u client push installatie gebruikt of na de installatie.

U kunt de grootte van de cachemap opgeven met behulp van client instellingen in de Configuration Manager-console. Zie [client cache-instellingen](../deploy/about-client-settings.md#client-cache-settings)voor meer informatie.

De standaard locatie voor de Configuration Manager-client cache `%windir%\ccmcache` is en de standaard schijf ruimte is 5120 MB.  

> [!IMPORTANT]  
> Versleutel de map die wordt gebruikt voor de client cache niet. Configuration Manager kan geen inhoud downloaden naar een versleutelde map.  

### <a name="about-the-client-cache"></a>Over de client cache  

De Configuration Manager-client downloadt de inhoud voor vereiste software kort nadat deze de implementatie heeft ontvangen, maar wacht tot de geplande implementatie tijd. Op het geplande tijdstip controleert de Configuration Manager-client of de inhoud beschikbaar is in de cache. Als de inhoud in de cache is opgeslagen en de juiste versie is, gebruikt de client de inhoud in de cache. Wanneer de vereiste versie van de inhoud verandert, of als de client de inhoud verwijdert om ruimte te maken voor een ander pakket, wordt de inhoud opnieuw door de client naar de cache gedownload.  

Als de client inhoud probeert te downloaden voor een programma of toepassing die groter is dan de grootte van de cache, mislukt de implementatie vanwege onvoldoende cache grootte. De client genereert status bericht 10050 voor onvoldoende cache grootte. Als u later de cache grootte verg root, is dit het resultaat:  

- Voor een vereist programma: de client probeert de inhoud niet automatisch opnieuw te downloaden. Implementeer het pakket en programma opnieuw naar de client.  
- Voor een vereiste toepassing: de client probeert automatisch de inhoud te downloaden wanneer het client beleid wordt gedownload.  

Als de client een pakket probeert te downloaden dat kleiner is dan de grootte van de cache, maar de cache vol is, blijven alle *vereiste* implementaties opnieuw proberen tot:

- De cache ruimte is beschikbaar
- Time-out bij het downloaden
- De limiet voor het aantal pogingen is bereikt

Als u later de cache grootte verg root, probeert de client het pakket opnieuw te downloaden tijdens het volgende interval voor nieuwe pogingen. De client probeert de inhoud elke vier uur te downloaden tot deze 18 keer wordt geprobeerd.  

De inhoud in de cache wordt niet automatisch verwijderd. Het blijft in de cache voor ten minste één dag nadat de client die inhoud gebruikt. Als u de pakket eigenschappen configureert met de optie om inhoud op te slaan in de client cache, wordt deze niet automatisch verwijderd door de client. Als de cache ruimte wordt gebruikt door pakketten die in de afgelopen 24 uur zijn gedownload en de client nieuwe pakketten moet downloaden, verg root u de cache grootte of kiest u de optie voor het verwijderen van blijvende cache-inhoud.  

Gebruik de volgende procedures om de clientcache te configureren tijdens de handmatige clientinstallatie of nadat de client is geïnstalleerd.  

### <a name="configure-the-cache-during-manual-client-installation"></a>De cache configureren tijdens de hand matige client installatie  

Voer de opdracht CCMSetup.exe uit vanaf de installatiebronlocatie en geef de volgende eigenschappen op, indien vereist (gescheiden door spaties):  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > Gebruik de instellingen voor de cache grootte die beschikbaar zijn in **client instellingen** in de Configuration Manager-console in plaats van SMSCACHESIZE. Zie [client cache-instellingen](../deploy/about-client-settings.md#client-cache-settings)voor meer informatie.

Zie [over eigenschappen van client installatie](../deploy/about-client-installation-properties.md)voor meer informatie over het gebruik van deze opdracht regel eigenschappen voor CCMSetup. exe.

### <a name="configure-the-cache-during-client-push-installation"></a>De cache configureren tijdens de Push-client installatie  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer de gewenste site. Klik op het tabblad **Start** van het lint in de groep **instellingen** op **instellingen voor client installatie**en kies **client push installatie**. Ga naar het tabblad **installatie-eigenschappen** .  

3. Geef de volgende eigenschappen op, gescheiden door spaties:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > Gebruik de instellingen voor de cache grootte die beschikbaar zijn in **client instellingen** in de Configuration Manager-console in plaats van SMSCACHESIZE. Zie [client cache-instellingen](../deploy/about-client-settings.md#client-cache-settings)voor meer informatie.

     Zie [over eigenschappen van client installatie](../deploy/about-client-installation-properties.md)voor meer informatie over het gebruik van deze opdracht regel eigenschappen voor CCMSetup. exe.  

### <a name="configure-the-cache-on-the-client-computer"></a>De cache op de client computer configureren  

1. Open op de client computer het onderdeel **Configuration Manager** van het configuratie scherm.  

2. Ga naar het tabblad **cache** . Stel de ruimte-en locatie-eigenschappen in. De standaard locatie is `%windir%\ccmcache`.  

3. Als u de bestanden in de cachemap wilt verwijderen, kiest u **bestanden verwijderen**.  

### <a name="configure-client-cache-size-in-client-settings"></a>Client cache grootte in client instellingen configureren

Pas de grootte van de client cache aan zonder de client opnieuw te hoeven installeren. Gebruik de instellingen voor de cache grootte die beschikbaar zijn in de **client instellingen** in de Configuration Manager-console. Zie [client cache-instellingen](../deploy/about-client-settings.md#client-cache-settings)voor meer informatie.


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a>De client verwijderen

U kunt de Configuration Manager-client software van een computer verwijderen door **CCMSetup. exe** te gebruiken met de eigenschap **/Uninstall** . Voer CCMSetup. exe op een afzonderlijke computer uit vanaf de opdracht prompt of implementeer een pakket om de client te verwijderen voor een verzameling computers.  

> [!NOTE]  
> U kunt de Configuration Manager-client niet verwijderen van een mobiel apparaat. Als u de Configuration Manager-client van een mobiel apparaat moet verwijderen, moet u het apparaat wissen, waardoor alle gegevens op het mobiele apparaat worden verwijderd.  

1. Open een Windows-opdracht prompt als beheerder. Wijzig de map in de locatie waarin CCMSetup. exe zich bevindt, bijvoorbeeld:`cd %windir%\ccmsetup`

2. Voer de volgende opdracht uit:`CCMSetup.exe /uninstall`

> [!TIP]  
> Het verwijderings proces geeft geen resultaten weer op het scherm. Raadpleeg het volgende logboek bestand om te controleren of de client is verwijderd:`%windir%\ccmsetup\logs\CCMSetup.log`  
>
> Als u wilt wachten tot de verwijdering is voltooid voordat u iets anders doet, voert `Wait-Process CCMSetup` u uit in Power shell. Met deze opdracht kan een script worden onderbroken totdat het CCMSetup-proces is voltooid.


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a>Conflicterende records beheren

Configuration Manager gebruikt de hardware-id om clients te identificeren die mogelijk duplicaten zijn en u te waarschuwen voor de conflicterende records. Als u een computer opnieuw installeert, zou de hardware-id bijvoorbeeld hetzelfde zijn, maar de GUID die door Configuration Manager wordt gebruikt, kan worden gewijzigd.  

Configuration Manager lost conflicten automatisch op met behulp van Windows-verificatie van het computer account of een PKI-certificaat van een vertrouwde bron. Als Configuration Manager het conflict met dubbele hardware-id's niet kan oplossen, bepaalt een hiërarchie-instelling het gedrag.

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>De hiërarchie-instelling voor het beheren van conflicterende records wijzigen  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .

1. Selecteer **hiërarchie-instellingen**op het lint.

1. Schakel over naar het tabblad **goed keuring van client en conflicterende records** en selecteer een van de volgende opties:

    - **Conflicterende records automatisch oplossen**
    - **Conflicterende records hand matig oplossen**

### <a name="manually-resolve-conflicting-records"></a>Conflicterende records hand matig oplossen  

1. Ga in de Configuration Manager-console naar de werk ruimte **bewaking** , vouw de **systeem status**uit en selecteer het knoop punt **conflicterende records** .  

1. Selecteer een of meer conflicterende records en kies vervolgens **conflicterende record**.  

1. Selecteer één van de volgende opties:  

    - **Samen voegen**: de nieuw gedetecteerde record combi neren met de bestaande client record.  

    - **Nieuw**: Maak een nieuwe record voor de conflicterende client record.  

    - **Blok keren**: Maak een nieuwe record voor de conflicterende client record, maar Markeer deze als geblokkeerd.  


## <a name="manage-duplicate-hardware-identifiers"></a>Dubbele hardware-id's beheren

U kunt een lijst opgeven met hardware-id's die Configuration Manager worden genegeerd voor PXE-opstart-en client registratie. Deze lijst helpt bij het oplossen van twee veelvoorkomende problemen:

1. Veel nieuwe apparaten bevatten geen onboard Ethernet-poort. Technici gebruiken een USB-naar-Ethernet-adapter om een bekabelde verbinding tot stand te brengen voor de implementatie van het besturings systeem. Deze adapters worden vaak gedeeld vanwege kosten en algemene gebruiks gemak. De site maakt gebruik van het MAC-adres van deze adapter om het apparaat te identificeren. Het opnieuw gebruiken van de adapter wordt problematisch zonder extra beheerders acties tussen elke implementatie. Als u de adapter in dit scenario opnieuw wilt gebruiken, moet u het MAC-adres ervan uitsluiten.

2. Hoewel het SMBIOS-kenmerk uniek moet zijn, hebben sommige gespecialiseerde hardwareapparaten dubbele id's. Sluit deze dubbele id en vertrouw op het unieke MAC-adres van elk apparaat.

Gebruik het volgende proces om hardware-id's toe te voegen voor het Configuration Manager negeren:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** .

2. Klik op het tabblad **Start** van het lint in de groep **sites** op **hiërarchie-instellingen**.

3. Schakel over naar het tabblad **goed keuring van client en conflicterende records** . Als u nieuwe hardware-id's wilt toevoegen, klikt u op **toevoegen** in de sectie **dubbele hardware-id's** .

> [!TIP]
> Met ingang van versie 1910 kunt u de volgende Power shell-cmdlets gebruiken om het beheer van dubbele hardware-id's te automatiseren:<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a>Ophalen van beleid starten

Een Configuration Manager-client downloadt het client beleid op een schema dat u configureert als een client instelling. U kunt ook het ophalen van beleid op aanvraag van de client starten. Bijvoorbeeld voor het oplossen van problemen of het testen van situaties.  

- [Clientmeldingen](#bkmk_policy-notify)
- [Het configuratie scherm van de client](#bkmk_policy-manual)
- [Ondersteuningscentrum](#bkmk_policy-support)
- [Een script](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a>Ophalen van client beleid starten met client melding  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer **apparaten**.  

1. Selecteer het apparaat dat u wilt downloaden. Selecteer op het tabblad **Start** van het lint in de groep **apparaat** de optie **client melding**en kies vervolgens **computer beleid downloaden**.  

    > [!NOTE]  
    > U kunt ook client melding gebruiken om het beleid op te halen voor alle apparaten in een verzameling.  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a>Het ophalen van client beleid starten vanuit het configuratie scherm van Configuration Manager-client

1. Open het configuratie scherm van **Configuration Manager** op de computer.  

2. Ga naar het tabblad **acties** . Selecteer **& evaluatie cyclus machine beleid ophalen** om het computer beleid te starten en selecteer **nu uitvoeren**.  

3. Selecteer **OK** om de prompt te bevestigen.  

4. Herhaal de vorige stappen voor andere acties. Bijvoorbeeld **het ophalen van gebruikers beleid & evaluatie cyclus** voor client instellingen voor gebruikers.  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a>Het ophalen van client beleid starten met het ondersteunings centrum

Gebruik het ondersteunings centrum om het client beleid aan te vragen en weer te geven. Zie [Naslag Gids voor ondersteunings centrum](../../support/support-center-ui-reference.md#bkmk_support-policy)voor meer informatie.

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a>Client beleid ophalen op basis van script starten  

1. Open een script editor, zoals Klad blok of Windows PowerShell ISE.  

2. Kopieer de volgende Power shell-voorbeeld code en voeg deze in<!-- SCCMDocs#1591 --> in het bestand:  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > Zie [bericht-id's](../../support/send-schedule-tool.md#bkmk_sendschedule-guids)voor meer informatie over de schema-id's.

3. Sla het bestand op met de extensie. ps1.  

4. Voer het script uit op de client.
