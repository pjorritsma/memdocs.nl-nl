---
title: Technical Preview 1806
titleSuffix: Configuration Manager
description: Meer informatie over nieuwe functies die beschikbaar zijn in de Configuration Manager Technical Preview versie 1806.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 01c482700b56a1835e46cf5d48da75710f380496
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995395"
---
# <a name="capabilities-in-technical-preview-1806-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1806 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1806. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Technical Preview-site. 

Raadpleeg het artikel [Technical Preview](technical-preview.md) voordat u deze update installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Bekende problemen in deze Technical Preview

### <a name="site-fails-to-upgrade-with-remote-content-library"></a><a name="ki_contentlib"></a> Site kan niet worden bijgewerkt met externe inhouds bibliotheek
<!--514642-->
De site kan niet worden bijgewerkt met de volgende fouten in **cmupdate. log**:  

``` Log
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Dit probleem doet zich voor in deze release wanneer de inhouds bibliotheek zich op een externe locatie bevindt.

#### <a name="workaround"></a>Tijdelijke oplossing
Verplaats de inhouds bibliotheek naar een lokaal station op de site server. Zie [een externe inhouds bibliotheek voor de site server configureren](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)voor meer informatie. 



</br>

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  



## <a name="third-party-software-updates"></a><a name="bkmk-3pupdate"></a> Software-updates van derden
<!--1352101-->
In deze release wordt de ondersteuning voor software-updates van derden verder herhaald als gevolg van uw [UserVoice-feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co). U hebt het gebruik van System Center Updates Publisher (SCUP gemaakt) niet meer nodig voor een aantal algemene scenario's. Met het nieuwe knoop punt **Software-update catalogussen** van derden in de Configuration Manager-console kunt u zich abonneren op catalogi van derden, hun updates publiceren op uw software-update punt en deze vervolgens implementeren op clients. 

De volgende software-update catalogussen van derden zijn beschikbaar in deze release:

 | Publisher | Catalogus naam |
 |--------|---------------------|
 | HP | Catalogus met HP client-updates |

SCUP gemaakt blijft ondersteuning bieden voor andere catalogussen en scenario's. De lijst met catalogi in het knoop punt software-update catalogi van derden van de Configuration Manager-console is dynamisch en wordt bijgewerkt als er aanvullende catalogi beschikbaar en ondersteund zijn.


### <a name="prerequisites"></a>Vereisten
- Stel het beheer van software-updates in met een software-update punt met HTTPS-functionaliteit. Zie voor meer informatie [voor bereiding op het beheer van software-updates](../../sum/get-started/prepare-for-software-updates-management.md).  
  - Het software-update punt moet zich op de site server voor deze functie in deze release bestaan. <!--515810--> 

    > [!Tip]  
    > Het software-update punt vereist HTTPS omdat het een vereiste is voor de WSUS-Api's die worden gebruikt voor het afhandelen van handtekening certificaten. Clients hoeven ook geen HTTPS-functionaliteit te hebben. Raadpleeg de volgende artikelen voor hulp voor meer informatie over het inschakelen van HTTPS op WSUS:  
    > - [Beveiligde WSUS met het Secure Sockets Layer-protocol](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 
    > - [Blog bericht over WSUS-ondersteuning](/archive/blogs/sus/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names)

- Er voldoende schijf ruimte op het software-update punt, WSUSContent-map, om de binaire bron inhoud op te slaan voor software-updates van derden. De hoeveelheid vereiste opslag is afhankelijk van de leverancier, typen updates en specifieke updates die u voor implementatie publiceert. Als u de map WSUSContent naar een ander station met meer vrije ruimte wilt verplaatsen, raadpleegt u het blog bericht van het WSUS-ondersteunings team [hoe u de locatie wijzigt waar WSUS lokaal updates opslaat](/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally).  

- Inschakelen en implementeren van de client instelling [software-updates](../clients/deploy/about-client-settings.md#enable-third-party-software-updates) van derden inschakelen in de groep met software- **updates** .  

- De site server vereist Internet toegang tot download.microsoft.com via HTTPS-poort 443. De synchronisatie service voor software-updates van derden wordt momenteel uitgevoerd op de site server. Met deze service wordt de lijst met beschik bare catalogi van derden bijgewerkt, worden de catalogussen gedownload wanneer u zich abonneert en worden de updates gedownload wanneer deze worden gepubliceerd. Configureer de Internet proxy instellingen, indien nodig, op het tabblad **proxy** van de eigenschappen van de site systeemrol van de site Server computer.  


### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Fase 1: de functie inschakelen en instellen
Voer de volgende stappen *eenmaal per hiërarchie* uit om de functie in te scha kelen en in te stellen voor gebruik:  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer het knoop punt **sites** .  

2. Selecteer de site op het hoogste niveau in de hiërarchie. Klik in het lint op **site onderdelen configureren**en selecteer **Software-update punt**.  

3. Schakel over naar het tabblad **updates van derden** . Selecteer de optie om **software-updates van derden in te scha kelen**. Zie [verbeteringen voor het inschakelen van ondersteuning voor software-updates van derden](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)voor meer informatie over de certificaat opties.  

   > [!Note]  
   > Als u de standaard optie voor Configuration Manager gebruikt voor het beheren van dit certificaat, wordt er een nieuw certificaat van het type **WSUS-ondertekening** van derden gemaakt in het knoop punt **certificaten** onder **beveiliging** in de werk ruimte **beheer** .  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Fase 2: abonneren op een catalogus van derden en updates synchroniseren
Voer de volgende stappen uit voor *elke catalogus* van derden waarop u zich wilt abonneren:  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **software-updates** uit en selecteer het knoop punt **Software-update catalogi van derden** .  

2. Selecteer de catalogus waarvoor u zich wilt abonneren en klik op **Abonneren op catalogus** op het lint.   

3. Het catalogus certificaat controleren en goed keuren.  

   > [!Note]  
   > Wanneer u zich abonneert op een Software-Update catalogus van derden, wordt het certificaat dat u in de wizard hebt gecontroleerd en goedgekeurd, aan de site toegevoegd. Dit certificaat is van het type **catalogus met software-updates**van derden. U kunt deze beheren via het knoop punt **certificaten** onder **beveiliging** in de werk ruimte **beheer** .  

4. Voltooi de wizard.  

   > [!Tip]  
   > Na het eerste abonnement moet de catalogus onmiddellijk worden gedownload. Vervolgens wordt elke 24 uur opnieuw gesynchroniseerd in deze release. Als u niet wilt wachten totdat de catalogus automatisch wordt gedownload, klikt u op **Nu synchroniseren** op het lint.  
   > 
   > Nadat de catalogus is gedownload, moeten de meta gegevens van het product worden gesynchroniseerd met het software-update punt. Zie [software-updates synchroniseren](../../sum/get-started/synchronize-software-updates.md)voor meer informatie over dit proces en hoe hand matig moet worden gestart. Op dit moment kunt u de updates van derden in het knoop punt **alle updates** bekijken. 

5. Configureer vervolgens de software-update punt **producten** voor de catalogus van derden waarop u bent geabonneerd. Zie voor meer informatie [classificaties en producten configureren om te synchroniseren](../../sum/get-started/configure-classifications-and-products.md). Nadat de product criteria zijn gewijzigd, moet de software-update synchronisatie opnieuw worden uitgevoerd.

Voordat u de nalevings resultaten van clients kunt zien, moeten ze updates scannen en evalueren. U kunt deze cyclus hand matig activeren vanuit het Configuration Manager configuratie scherm op een client door de actie **Scan cyclus voor software-updates** uit te voeren. Zie [Inleiding tot software-updates](../../sum/understand/software-updates-introduction.md)voor meer informatie over het proces.


#### <a name="phase-3-deploy-third-party-software-updates"></a>Fase 3: software-updates van derden implementeren
Voer de volgende stappen uit voor *software-updates* van derden die u wilt implementeren op clients:  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **software-updates** uit en selecteer het knoop punt **alle software-updates** .  

   > [!Tip]  
   > Klik op **criteria toevoegen** om de lijst met updates te filteren. Voeg bijvoorbeeld **leverancier** toe voor **Adobe Systems, Inc.** om alle updates van Adobe weer te geven.  

2. Selecteer de updates die vereist zijn voor clients. Klik op **inhoud van software-update** van derden publiceren en controleer de voortgang in het SMS_ISVUPDATES_SYNCAGENT. log. Met deze actie worden de binaire update bestanden van de leverancier gedownload en opgeslagen in de map WSUSContent op het software-update punt. Ook wordt de status van de update gewijzigd van meta gegevens in met inhoud en implementeerbaar.  

   > [!Note]  
   > Wanneer u inhoud van software-updates van derden publiceert, worden alle certificaten die worden gebruikt voor het ondertekenen van de inhoud toegevoegd aan de site. Deze certificaten zijn van **het type inhoud van software-updates**van derden. U kunt deze beheren via het knoop punt **certificaten** onder **beveiliging** in de werk ruimte **beheer** .  

3. Implementeer de updates met behulp van het bestaande beheer proces voor software-updates. Zie [software-updates implementeren](../../sum/deploy-use/deploy-software-updates.md)voor meer informatie. Selecteer op de pagina **Download locaties** van de wizard software-updates implementeren de standaard optie om **software-updates van Internet te downloaden**. In dit scenario wordt de inhoud al gepubliceerd naar het software-update punt, dat wordt gebruikt voor het downloaden van de inhoud voor het implementatie pakket.


### <a name="monitoring-progress-of-third-party-software-updates"></a>De voortgang van software-updates van derden bewaken
Synchronisatie van software-updates van derden wordt afgehandeld door het onderdeel SMS_ISVUPDATES_SYNCAGENT op de site server. U kunt status berichten van dit onderdeel weer geven of meer gedetailleerde statussen bekijken in het SMS_ISVUPDATES_SYNCAGENT. log. Dit logboek bevindt zich op de site server in de submap **logs** van de installatiemap van de site. Dit pad is standaard `C:\Program Files\Microsoft Configuration Manager\Logs` . Zie [software-updates bewaken](../../sum/deploy-use/monitor-software-updates.md)voor meer informatie over het controleren van het algemene proces voor software-update beheer.


### <a name="known-issues"></a>Bekende problemen
- De synchronisatie service van de software-update van derden biedt geen ondersteuning voor het software-update punt dat is geconfigureerd voor het gebruik van een **WSUS-server verbindings account**. Als dit account is geconfigureerd op het tabblad **proxy-en account instellingen** van de eigenschappen pagina van het software-update punt, ziet u de volgende fout in het SMS_ISVUPDATES_SYNCAGENT. log:  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Zie [verbindings account software-update punt](../plan-design/hierarchy/accounts.md#software-update-point-connection-account)voor meer informatie over dit account.<!--515492-->  

- Combi neer niet het gebruik van andere hulpprogram ma's, zoals SCUP gemaakt, met deze nieuwe geïntegreerde software-update functie van derden. De synchronisatie service voor software-updates van derden kan geen inhoud publiceren naar updates met meta gegevens die zijn toegevoegd aan WSUS door een andere toepassing, hulp programma of script, zoals SCUP gemaakt. De actie **inhoud van software-update publiceren** van derden mislukt bij deze updates. Als u updates van derden wilt implementeren die door deze functie nog niet worden ondersteund, moet u uw bestaande proces volledig gebruiken om deze updates te implementeren.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Windows Defender SmartScreen-instellingen voor micro soft Edge configureren
<!--1353701-->
Deze release voegt drie instellingen voor [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) toe aan het [beleid voor nalevings instellingen van micro soft Edge-browser](../../compliance/deploy-use/browser-profiles.md). Het beleid bevat nu de volgende aanvullende instellingen op de pagina **SmartScreen-instellingen** :
- **SmartScreen toestaan**: Hiermee geeft u op of Windows Defender SmartScreen is toegestaan. Zie het [AllowSmartScreen-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)voor meer informatie.
- **Gebruikers kunnen SmartScreen-prompts voor sites overschrijven**: Hiermee geeft u op of gebruikers de waarschuwingen van het Windows Defender SmartScreen-filter kunnen negeren over mogelijk schadelijke websites. Zie het [PreventSmartScreenPromptOverride-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)voor meer informatie.
- **Gebruikers kunnen SmartScreen-prompts negeren voor bestanden**: Hiermee geeft u aan of gebruikers de waarschuwingen van het Windows Defender SmartScreen-filter kunnen negeren over het downloaden van niet-geverifieerde bestanden. Zie het [PreventSmartScreenPromptOverrideForFiles-browser beleid](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)voor meer informatie.



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>MDM-beleid van Microsoft Intune voor een gezamenlijk beheerd apparaat synchroniseren
<!--1357377-->
In deze release wordt het MDM-beleid automatisch gesynchroniseerd op basis van Microsoft Intune als u [een werk belasting voor co-beheer verwisselt](../../comanage/how-to-switch-workloads.md). Deze synchronisatie treedt ook op wanneer u de actie **computer beleid downloaden** van client meldingen in de Configuration Manager-console start. Zie [het ophalen van client beleid initiëren met client meldingen](../clients/manage/manage-clients.md#BKMK_PolicyRetrieval)voor meer informatie.



## <a name="transition-microsoft-365-workload-to-intune-using-co-management"></a>Overgang Microsoft 365 werk belasting naar intune met behulp van co-beheer
<!--1357841-->
U kunt de Microsoft 365 workload nu overzetten van Configuration Manager naar Microsoft Intune na het inschakelen van co-beheer. Als u deze werk belasting wilt door lopen, gaat u naar de pagina met eigenschappen voor co-beheer en verplaatst u de schuif regelaar van Configuration Manager naar pilot of alle. Zie voor meer informatie [co-beheer voor Windows 10-apparaten](../../comanage/overview.md).

Er is ook een nieuwe globale voor waarde, **zijn Office 365-toepassingen die worden beheerd door intune op het apparaat**. Deze voor waarde wordt standaard toegevoegd als vereiste voor nieuwe Microsoft 365-toepassingen. Wanneer u deze werk belasting overdraagt, voldoen gezamenlijk beheerde clients niet aan de vereiste voor de toepassing. Installeer daarom niet Microsoft 365 geïmplementeerd via Configuration Manager.

### <a name="known-issue"></a>Bekend probleem

- Deze werkbelasting overgang is momenteel alleen van toepassing op Microsoft 365-implementaties. Configuration Manager blijft Microsoft 365-updates beheren.<!--510876--> Voor meer informatie, waaronder een mogelijke tijdelijke oplossing, raadpleegt u de Configuration Manager versie 1802 Release Opmerking het [wijzigen van Microsoft 365 client instelling is niet van toepassing](../servers/deploy/install/release-notes.md).



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Pakket conversie beheer is nu een geïntegreerd hulp programma waarmee u verouderde Configuration Manager 2007-pakketten kunt converteren naar Configuration Manager huidige branch-toepassingen. Vervolgens kunt u de functies van toepassingen gebruiken, zoals afhankelijkheden, vereisten regels en gebruikers affiniteit met apparaat.

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

> [!Important]  
> Als u eerder een oudere versie van package Conversion Manager hebt geïnstalleerd, moet u deze eerst verwijderen voordat u de site bijwerkt. De nieuwe geïntegreerde versie hoeft niet te worden geïnstalleerd, maar kan conflicteren met bestaande versies.  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **toepassings beheer** uit en selecteer **pakketten**.  
2. Selecteer een pakket. De volgende drie opties zijn beschikbaar in de **pakket conversie** groep van het lint:  
     - **Pakket analyseren**: start het conversie proces door het pakket te analyseren.
     - **Pakket converteren**: sommige pakketten kunnen eenvoudig worden geconverteerd in toepassingen met deze actie.
     - **Herstellen en converteren**: voor sommige pakketten moeten problemen worden opgelost voordat deze naar toepassingen worden geconverteerd.  


3. Ga naar de werk ruimte **bewaking** en selecteer **pakket conversie status**. Dit nieuwe dash board toont de algemene analyse-en conversie status van de pakketten in de-site. Met een nieuwe achtergrond taak worden automatisch de analyse gegevens samenvatten.  

   > [!Tip]  
   > Voor package Conversion Manager is het niet nodig om de analyse van pakketten te plannen. Deze actie wordt nu verwerkt door de taak Integrated samenvatting.  

![Scherm opname van het dash board voor pakket conversie status](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Software-updates zonder inhoud implementeren
<!--1357933-->
U kunt nu software-updates implementeren op apparaten zonder eerst software-update-inhoud te downloaden en distribueren naar distributie punten. Deze functie is handig bij het verwerken van extreem grote update-inhoud of wanneer u altijd wilt dat clients inhoud ophalen van de Microsoft Update Cloud service. Clients in dit scenario kunnen ook inhoud downloaden van peers die al over de benodigde inhoud beschikken. De Configuration Manager-client blijft het downloaden van de inhoud blijven beheren, maar kan ook gebruikmaken van de functie voor Configuration Manager peer-cache of andere technologieën zoals Delivery Optimization. Deze functie ondersteunt elk update type dat wordt ondersteund door Configuration Manager beheer van software-updates, waaronder Windows-en Office-updates. 

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Start een software-update-implementatie per normaal. Zie [software-updates implementeren](../../sum/deploy-use/deploy-software-updates.md)voor meer informatie.
2. Selecteer in de wizard software-updates implementeren op de pagina **implementatie pakket** de optie Nieuw voor **geen implementatie pakket**.

### <a name="known-issues"></a>Bekende problemen
- Het pictogram voor een update die met deze instelling wordt geïmplementeerd, wordt onjuist weer gegeven met een rode X alsof de update ongeldig is. Zie [pictogrammen die worden gebruikt voor software-updates](../../sum/understand/software-updates-icons.md)voor meer informatie. <!--515556-->  
- Deze instelling is alleen geïntegreerd met de wizard software-updates implementeren. Deze functie is momenteel niet beschikbaar voor regels voor automatische implementatie. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Integratie van Office Customization Tool met Office 365 Installer
<!--1358149-->
Het hulp programma voor het aanpassen van Office is nu geïntegreerd met het installatie programma van Office 365 in de Configuration Manager-console. Bij het maken van een implementatie voor Office 365 kunt u nu de meest recente Office-beheer baarheid-instellingen dynamisch configureren. Het hulp programma voor het aanpassen van Office wordt op hetzelfde moment bijgewerkt als de release van de nieuwe builds van Office 365. U kunt nu profiteren van nieuwe beheer instellingen in Office 365 zodra deze beschikbaar zijn. 

### <a name="prerequisites"></a>Vereisten
- De computer waarop de Configuration Manager-console wordt uitgevoerd, heeft Internet toegang nodig via HTTPS-poort 443. De Office 365-client installatie wizard gebruikt een Windows standaard webbrowser-API om te openen https://config.office.com . Als er een Internet proxy wordt gebruikt, moet de gebruiker toegang hebben tot deze URL.

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** en selecteer het knoop punt **Office 365-client beheer** .
2. Klik op de tegel **office 365-installatie programma** in het dash board om de Wizard Office 365-client installatie te starten. Zie [Microsoft 365-Apps implementeren](../../sum/deploy-use/manage-office-365-proplus-updates.md)voor meer informatie.
3. Klik op de pagina **Office-instellingen** op **Go to Office Web page**. Gebruik het hulp programma voor het aanpassen van het online kantoor om instellingen voor deze implementatie op te geven. 
4. Klik op **verzenden** in de rechter bovenhoek wanneer dit is voltooid. Voltooi de wizard Office 365-client installatie.



## <a name="improvements-to-cloud-management-gateway"></a>Verbeteringen in de Cloud beheer gateway
Deze release bevat de volgende verbeteringen voor de Cloud Management Gateway (CMG):

### <a name="simplified-client-bootstrap-command-line"></a>Vereenvoudigde client opdracht regel voor Boots trap
<!--1358215-->
Wanneer u de Configuration Manager-client op Internet installeert via een CMG, zijn er minder opdracht regel eigenschappen vereist. Voor meer informatie over een voor beeld van dit scenario raadpleegt [u de opdracht regel om Configuration Manager-client te installeren](../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) tijdens de voor bereiding op co-beheer. 

De volgende opdracht regel eigenschappen zijn vereist in alle scenario's:
- CCMHOSTNAME  
- SMSSITECODE  

De volgende eigenschappen zijn vereist wanneer u Azure AD gebruikt voor client verificatie in plaats van client verificatie certificaten op basis van PKI:
- AADCLIENTAPPID  
- AADRESOURCEURI  

De volgende eigenschap is vereist als de client terugkeert naar het intranet:
- SMSMP  

In het volgende voor beeld worden alle bovenstaande eigenschappen opgenomen:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Zie [Eigenschappen van client installatie](../clients/deploy/about-client-installation-properties.md)voor meer informatie.

### <a name="download-content-from-a-cmg"></a>Inhoud downloaden van een CMG
<!--1358651-->
Voorheen moest u een Cloud distributiepunt en CMG implementeren als afzonderlijke rollen. In deze release kan een CMG ook inhoud aan clients aanbieden. Deze functionaliteit vermindert de vereiste certificaten en kosten van virtuele Azure-machines. Als u deze functie wilt inschakelen, schakelt u de optie Nieuw in om **CMG te laten functioneren als een Cloud distributiepunt en inhoud te bezorgen bij Azure Storage** op het tabblad **instellingen** van de CMG eigenschappen. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Het vertrouwde basis certificaat is niet vereist voor Azure AD
<!--503899-->
Wanneer u een CMG maakt, hoeft u niet langer een [vertrouwd basis certificaat](../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_cmgroot) op te geven op de pagina instellingen. Dit certificaat is niet vereist wanneer u Azure Active Directory (Azure AD) gebruikt voor client verificatie, maar dat in de wizard vereist is.

> [!Important]  
> Als u certificaten voor PKI-client verificatie gebruikt, moet u nog steeds een vertrouwd basis certificaat toevoegen aan de CMG.



## <a name="improvements-to-secure-client-communications"></a>Verbeteringen voor het beveiligen van client communicatie
<!--1358278,1358279-->
Deze release blijft de [verbeterde beveiligde client communicatie](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) herhalen door extra afhankelijkheden van het netwerk toegangs account te verwijderen. Wanneer u de optie nieuwe site inschakelt voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen**, is voor de volgende scenario's geen netwerk toegangs account vereist om inhoud te downloaden vanaf een distributie punt:  

- Taken reeksen die worden uitgevoerd vanaf opstart media of PXE
- Taken reeksen die worden uitgevoerd vanuit software Center  

Deze taken reeksen kunnen voor de implementatie van het besturings systeem of aangepast zijn. Het wordt ook ondersteund voor werkgroepcomputers.



## <a name="software-center-infrastructure-improvements"></a>Verbeteringen in de Software Center-infra structuur
<!--1358309-->
De functies van de toepassings catalogus zijn niet langer vereist voor het weer geven van gebruikers beschik bare toepassingen in Software Center. Met deze wijziging kunt u de server infrastructuur verminderen die nodig is voor het leveren van toepassingen aan gebruikers. Software Center is nu afhankelijk van het beheer punt om deze informatie te verkrijgen, waardoor grotere omgevingen beter kunnen worden geschaald door ze toe te wijzen aan [grens groepen](../servers/deploy/configure/boundary-groups.md#management-points).

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Verwijder alle Application Catalog-rollen van de site. Deze rollen zijn onder andere het Application Catalog-webservicepunt en het Application catalog-website punt.
2. Implementeer een toepassing als beschikbaar voor een gebruikers verzameling.
3. Gebruik Software Center als doel gebruiker om de toepassing te zoeken, te vragen en te installeren.

### <a name="known-issue"></a>Bekend probleem
- Als u met deze functie een Azure Active Directory-client gebruikt, moet u de site niet configureren voor het **gebruik van door Configuration Manager gegenereerde certificaten voor HTTP-site systemen**. Er is momenteel een conflict met deze functie.<!--515846--> Zie [verbeterde beveiligde client communicatie](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)voor meer informatie over deze instelling.



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Windows-app-pakketten inrichten voor alle gebruikers op een apparaat
<!--1358310-->
U kunt nu een toepassing inrichten met een Windows-app-pakket voor alle gebruikers op het apparaat. Een veelvoorkomend voor beeld van dit scenario is het inrichten van een app van de Microsoft Store for Business en Education, zoals Minecraft: Education Edition, op alle apparaten die worden gebruikt door studenten op school. Voorheen Configuration Manager alleen de installatie van deze toepassingen per gebruiker ondersteund. Nadat u zich hebt aangemeld bij een nieuw apparaat, moet een student wachten op toegang tot een app. Wanneer de app nu voor alle gebruikers op het apparaat wordt ingericht, kunnen ze sneller productief zijn.

> [!Important]  
> Wees voorzichtig met het installeren, inrichten en bijwerken van verschillende versies van hetzelfde Windows-app-pakket op een apparaat. Dit kan leiden tot onverwachte resultaten. Dit gedrag kan optreden wanneer Configuration Manager wordt gebruikt om de app in te richten, maar vervolgens gebruikers toestaan om de app vanuit de Microsoft Store bij te werken. Zie de volgende richt lijnen voor meer informatie over het [beheren van apps vanuit de Microsoft Store voor bedrijven](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Bij het inrichten van een offline gelicentieerde app, kunt Configuration Manager deze niet automatisch bijwerken vanuit de Microsoft Store.  

### <a name="try-it-out"></a>Probeer het nu!
 Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) en laat ons weten hoe het heeft gewerkt.

1. Een nieuwe toepassing maken. Deze app moet afkomstig zijn uit een Windows-app-pakket of een app met een offline licentie die u hebt gesynchroniseerd vanuit het Microsoft Store voor bedrijven en onderwijs.  

2. Schakel op de pagina **algemene informatie** van de wizard toepassing maken de optie in om **deze toepassing in te richten voor alle gebruikers op het apparaat**.  

   > [!Tip]  
   > Als u een bestaande toepassing wijzigt, bevindt deze instelling zich op het tabblad **gebruikers ervaring** van de eigenschappen van de toepassing.  

3. Implementeer de toepassing in een verzameling apparaten.  

4. Meld u aan bij een doel apparaat met verschillende gebruikers accounts en start de toepassing.  

> [!Note]  
> Als u een ingerichte toepassing moet verwijderen van apparaten waarop gebruikers al zijn aangemeld, moet u twee implementaties voor verwijderen maken. Richt de eerste implementatie voor het verwijderen naar een verzameling apparaten die de apparaten bevat. Richt de tweede implementatie voor verwijderen uit voor een gebruikers verzameling die de gebruikers bevat die al zijn aangemeld bij apparaten met de ingerichte toepassing. Wanneer u een ingerichte app op een apparaat verwijdert, wordt die app momenteel niet door Windows verwijderd voor gebruikers. 



## <a name="improvements-to-the-surface-dashboard"></a>Verbeteringen aan het Surface-dash board
<!--1358654-->
Deze release bevat de volgende verbeteringen aan het [Surface-dash board](../clients/manage/surface-device-dashboard.md):
- Het Surface-dash board geeft nu een lijst met relevante apparaten weer wanneer secties van de grafiek worden geselecteerd.
   - Als u op de tegel **percentage van Opper vlakken** klikt, wordt een lijst met Surface-apparaten geopend.
   - Als u op een balk in de **bovenste vijf firmware versies** tegel klikt, wordt er een lijst met Surface-apparaten met die specifieke firmware versie geopend.
- Wanneer u deze apparaten uit het Surface-dash board bekijkt, kunt u met de rechter muisknop op een apparaat klikken en algemene acties uitvoeren.



## <a name="hardware-inventory-default-unit-revision"></a>Revisie van standaard eenheid voor hardware-inventaris
<!--514442-->
In [Configuration Manager versie 1710](../plan-design/changes/whats-new-in-version-1710.md#site-infrastructure)is de standaard eenheid die in veel rapport weergaven wordt gebruikt, gewijzigd van mega bytes (MB) in GIGABYTES (GB). Als gevolg van [verbeteringen in de hardware-inventaris voor grote integerwaarden](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)en op basis van feedback van klanten, is deze standaard eenheid nu MB opnieuw.



## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.