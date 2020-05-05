---
title: Mogelijkheden van Technical Preview 1605
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1605.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: c38230b44f7f18e3f60cb4c88b31a03e10a37d30
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721638"
---
# <a name="capabilities-in-technical-preview-1605-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1605 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1605. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site.      Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.  

 **Bekende problemen in deze technische preview:**  

- Met Technical Preview 1605, als u de eigenschappen van een beheer punt bijwerkt nadat dit is geïnstalleerd, ziet u mogelijk een console fout waardoor de console wordt gesloten.  Als dit het geval is, kunt u het beheer punt verwijderen en het beheer punt vervolgens opnieuw installeren met de gewenste instellingen. U kunt het beheer punt ook wijzigen voordat u Technical Preview 1605 installeert.  

- Wanneer u de functie Windows Store voor bedrijven gebruikt met de Technical Preview 1604 en vervolgens bijwerkt naar Technical Preview 1605, kunt u de onboarding-gegevens niet meer weer geven. Alle andere functies blijven werken. Als u het technisch voor beeld 1604 hebt uitgevoerd, blijft u onboarded nadat u Technical Preview 1605 hebt geïnstalleerd en hoeft u geen verdere actie te ondernemen.  

  **Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

##  <a name="per-app-vpn-for-windows-10-devices"></a><a name="BKMK_PerAppVPN"></a>VPN per app voor Windows 10-apparaten  
 Voor Windows 10-apparaten die worden beheerd met Configuration Manager met intune, kunt u een lijst met apps toevoegen die automatisch een VPN-verbinding openen die u hebt geconfigureerd via de Configuration Manager-beheer console. U hebt de mogelijkheid om VPN-verkeer naar deze apps te beperken of u kunt al het verkeer via de VPN-verbinding blijven toestaan.  

 **Vereisten**:  

-   Configuration Manager met intune  

-   Een Windows 10-VPN-profiel dat is geïmplementeerd op ten minste één apparaat  

##  <a name="improvements-to-the-install-software-updates-task-sequence"></a><a name="BKMK_InstallSU"></a>Verbeteringen in de taken reeks software-updates installeren  
 De volgende verbeteringen zijn aangebracht in de taken reeks software-updates installeren:  

-   Er is een nieuwe taken reeks variabele, SMSTSSoftwareUpdateScanTimeout, beschikbaar om u de mogelijkheid te bieden de time-out voor de scan van software-updates te beheren tijdens de taken reeks stap software-updates installeren. De standaardwaarde is 30 minuten.  

-   Er zijn verbeteringen aangebracht in de logboek registratie. Het logboek bestand bestand smsts. log bevat nieuwe logboek vermeldingen die verwijzen naar andere logboek bestanden die u kunnen helpen bij het oplossen van problemen tijdens het installatie proces van software-updates.  

##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a><a name="BKMK_PrepareConfigMgrClient"></a>Verbeteringen aan de taken reeks stap ConfigMgr-client voorbereiden voor vastleggen  
 Met de stap ConfigMgr-client voorbereiden wordt de Configuration Manager-client nu volledig verwijderd, in plaats van alleen de sleutel gegevens te verwijderen. Wanneer de taken reeks de vastgelegde installatie kopie van het besturings systeem implementeert, wordt elke keer een nieuwe Configuration Manager-client geïnstalleerd.  

##  <a name="grace-period-for-required-application-deployments"></a><a name="BKMK_Grace"></a>Respijt periode voor vereiste toepassings implementaties  
 In sommige gevallen kunt u gebruikers meer tijd geven om vereiste toepassings implementaties te installeren na eventuele deadlines die u hebt geconfigureerd. Als een eind gebruiker bijvoorbeeld slechts een vakantie heeft geretourneerd, kan het zijn dat ze lang moeten wachten terwijl er achterstallige toepassings implementaties zijn geïnstalleerd. Ze kunnen de toepassing echter altijd direct op elk gewenst moment installeren.  

 Om dit probleem op te lossen, kunt u nu een **respijt periode** definiëren door Configuration Manager client instellingen te implementeren voor een verzameling.  

 Voer de volgende acties uit om de respijt periode te configureren:  

1. Configureer op de pagina **computer agent** van client instellingen de nieuwe eigenschap **respijt periode voor afdwingen na de deadline van de implementatie (uren)** met een waarde tussen **1** en **120** uur.  

2. In een nieuwe toepassings implementatie, of in de eigenschappen van een bestaande implementatie, op de pagina **planning** , selecteert u het selectie vakje **vertraging afdwingen van deze implementatie op basis van gebruikers voorkeuren**tot de respijt periode die in de client instellingen is gedefinieerd.  

    Alle implementaties waarvoor dit selectie vakje is ingeschakeld en die zijn gericht op apparaten waarop u ook de client instelling implementeert, gebruiken de respijt periode.  

   In deze release wordt de door u geconfigureerde respijt periode niet gebruikt door client apparaten. Als u een respijt periode configureert en het selectie vakje inschakelt, wordt de toepassing geïnstalleerd in het eerste niet-zakelijke venster dat de gebruiker na de deadline hebt geconfigureerd.  

   Er zijn Vergelijk bare opties toegevoegd aan de wizard software-updates implementeren, de wizard regels voor automatische implementatie en eigenschappen pagina's. Deze worden momenteel echter niet geïmplementeerd in deze Technical Preview.  

##  <a name="new-experience-for-remote-device-actions"></a><a name="BKMK_Remote"></a>Nieuwe ervaring voor acties van externe apparaten  
 De ervaring voor het uitvoeren van acties voor externe apparaten vanuit de Configuration Manager-console is verbeterd.  
Veelvoorkomende acties, zoals **buiten gebruik stellen/wissen**, **opnieuw instellen, wachtwoord code**, **extern vergren delen**en **bypass Activeringsslot** , kunnen nu worden gevonden in het menu **acties van extern apparaat** dat wordt geopend vanuit de werk ruimte **activa en naleving** .  

 ![Scherm afbeelding nieuwe acties op afstand](media/New-Remote-Device-Actions.png)  

 U kunt de status voor elk van deze bewerkingen vinden op de volgende locaties:  

- In het detail venster, wanneer u een apparaat selecteert in het knoop punt **apparaten** .  

- Op de pagina **Eigenschappen** voor een apparaat.  

- Op de hoofd pagina van het knoop punt **apparaten** (niet alle kolommen kunnen standaard worden weer gegeven).  

##  <a name="windows-store-for-business-apps"></a><a name="BKMK_WSFB"></a>Windows Store voor bedrijven-apps  
 In de [Windows Store voor bedrijven](https://www.microsoft.com/business-store) kunt u apps zoeken en kopen voor uw organisatie, afzonderlijk of op volume. Als u de Store verbindt met Configuration Manager, kunt u apps die zijn gekocht via het volume-aankoop programma beheren via de Configuration Manager-console, bijvoorbeeld:  

- U kunt de lijst met aangeschafte apps synchroniseren met Configuration Manager  

- Apps die zijn gesynchroniseerd, worden weer gegeven in de Configuration Manager-console en u kunt deze op dezelfde manier implementeren als andere apps  

- Elke 24 uur, Configuration Manager app-licentie gegevens uit de Store downloaden en u kunt dit bekijken in de Configuration Manager-console  

  In de 1604 Technical Preview-versie kunt u apps in de Windows Store voor bedrijven synchroniseren en weer geven in de Configuration Manager-console. In deze release hebben we de mogelijkheid toegevoegd om Configuration Manager-toepassingen te maken en te implementeren vanuit gesynchroniseerde Store-apps.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Synchronisatie van Windows Store voor bedrijven instellen  

1.  Registreer Configuration Manager in Azure Active Directory als een hulp programma voor het beheer van webtoepassingen en/of Web-API. Hiermee krijgt u een client-ID die u later nodig hebt.  

    1.  Selecteer uw Azure Active Directory in het [https://manage.windowsazure.com](https://manage.windowsazure.com)knoop punt Active Directory van en klik vervolgens op **toepassingen** > **toevoegen**.  

    2.  Klik op **een toepassing toevoegen die mijn organisatie ontwikkelt**.  

    3.  Voer een naam in voor de toepassing, selecteer **Webtoepassing** en/of **Web-API**en klik op de pijl **volgende** .  

    4.  Voer dezelfde URL in voor zowel de **aanmeldings-URL** als de **URI van de App-ID**. De URL kan iets zijn en hoeft niet te worden omgezet naar een echt adres. U kunt bijvoorbeeld **https://e&lt;domein eigen>/SCCM**invoeren.  

    5.  Voltooi de wizard.  

2.  In Azure Active Directory maakt u een client sleutel voor het geregistreerde beheer programma.  

    1.  Markeer de toepassing die u zojuist hebt gemaakt en klik op **configureren**.  

    2.  Onder **sleutels**selecteert u een duur in de lijst en klikt u op **Opslaan**. Hiermee wordt een nieuwe client sleutel gemaakt. Verlaat deze pagina pas als u Windows Store voor bedrijven hebt gerepareerd naar Configuration Manager.  

3.  Configureer in de Windows Store voor bedrijven Configuration Manager als het hulp programma voor het beheer van opslag.  

    1.  Open [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) en meld u aan als u hierom wordt gevraagd.  

    2.  Accepteer de gebruiks voorwaarden, indien nodig.  

    3.  Klik onder **beheer hulpprogramma's**op **een beheer programma toevoegen**.  

    4.  Typ in **zoeken naar het hulp programma op naam**de naam van de toepassing die u eerder hebt gemaakt in Aad en klik vervolgens op **toevoegen**.  

    5.  Klik op **activeren** naast de toepassing die u zojuist hebt geïmporteerd.  

    6.  Klik in de wizard **apps met offline licenties weer geven** op **Ja** als u wilt toestaan dat toepassingen met een offline licentie worden gekocht.  

4.  Koop ten minste één app vanuit Windows Store voor bedrijven.  

5.  Vouw in de werk ruimte **beheer** van de Configuration Manager-console **Cloud Services**uit en klik vervolgens op **Windows Store voor bedrijven.**  

6.  Klik op het tabblad **Start** in de groep **maken** op **Windows Store voor bedrijven-account toevoegen**.  

7.  Voeg uw Tenant-ID, client-id en client sleutel van Azure Active Directory toe en voltooi vervolgens de wizard.  

8.  Wanneer u klaar bent, ziet u het account dat u hebt geconfigureerd in de lijst met **Windows Store voor bedrijven-accounts** in de Configuration Manager-console.  

### <a name="try-it-out"></a>Probeer het nu!  
 Voer de volgende taak uit en laat ons weten hoe het werkt met behulp van ons feedback formulier op de pagina [Configuration Manager feedback programma](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) op de micro soft Connect-site:  

 Een Configuration Manager-toepassing maken en implementeren vanuit een Windows Store voor bedrijven-app met een offline licentie.  

1. Vouw in de werk ruimte **software bibliotheek** van de Configuration Manager-console het knoop punt **toepassings beheer**uit en klik vervolgens op **licentie-informatie voor Store-apps**.  

2. Kies de app die u wilt implementeren en klik vervolgens op het tabblad **Start** in de groep **maken** op **toepassing maken**.  

   Er wordt een Configuration Manager-toepassing gemaakt met daarin de app Windows Store voor bedrijven. U kunt deze toepassing vervolgens implementeren en bewaken op dezelfde manier als andere Configuration Manager-toepassingen.  

> [!IMPORTANT]  
>  Wanneer u een Configuration Manager toepassing maakt met één implementatie type van een offline gelicentieerde app, kan dit worden geïmplementeerd voor apparaten die worden beheerd met MDM en ook worden beheerd met de Configuration Manager-client. Als u probeert een app te implementeren met meerdere implementatie typen, mislukt de installatie.  
>   
>  U kunt momenteel geen apps met een online licentie implementeren met Configuration Manager.  

##  <a name="general-improvements-for-volume-purchased-apps"></a><a name="BKMK_VPP2"></a>Algemene verbeteringen voor apps die zijn gekocht via het volume-aankoop programma  

-   In deze release zijn apps die zijn gekocht via het volume van de Windows Store voor bedrijven en de iOS-App Store samengevoegd in dezelfde weer gave, **licentie gegevens voor Store-apps**.  

-   Voor iOS-apps die zijn gekocht via het volume-aankoop programma, is het tabblad Apple Volume Purchase Program verwijderd uit het dialoog venster **app-pakket voor IOS-browser** in de wizard toepassing maken. Voer de volgende stappen uit om een app die is gekocht via het volume-aankoop programma voor iOS te maken:  

    1.  1.  Vouw in de werk ruimte **software bibliotheek** van de Configuration Manager-console het knoop punt **toepassings beheer**uit en klik vervolgens op **licentie-informatie voor Store-apps**.  

    2.  2.  Kies de app die u wilt implementeren en klik vervolgens op het tabblad **Start** in de groep **maken** op **toepassing maken**.  

-   De locatie die u gebruikt om een Apple VPP-token op te halen en te uploaden voor apps die zijn gekocht via het volume-aankoop programma in de Configuration Manager-console is gewijzigd. U kunt dit nu doen in de werk ruimte **beheer** onder het knoop punt **Cloud Services** > **Apple volume Purchase Program tokens** .  

##  <a name="enterprise-data-protection-edp"></a><a name="BKMK_VPP"></a>Ondernemings gegevens bescherming (EDP)  
 U kunt configuratie-items maken waarmee u uw beleid voor ondernemings gegevens bescherming (EDP) implementeert, met inbegrip van uw beveiligde apps, uw EDP-beschermings niveau en het vinden van Bedrijfs gegevens in het netwerk. Zie de volgende onderwerpen voor meer informatie over EDP:  

- [Uw bedrijfs gegevens beveiligen met behulp van Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Een beleid voor Windows Information Protection (WIP) maken en implementeren met behulp van Configuration Manager](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)


##  <a name="end-users-can-install-apps-from-the-company-portal"></a><a name="BKMK_End"></a>Eind gebruikers kunnen apps installeren vanuit de Bedrijfsportal  
 On-premises MDM werd geïntroduceerd in de Configuration Manager versie 1511. In eerdere versies kon u toepassingen implementeren op door MDM beheerde Windows 10-apparaten met een implementatie doel van **vereiste** installatie voor on-PREMISes MDM-beheerde apparaten.  

 In deze release kunt u nu apps implementeren met het implementatie doel **beschikbaar** voor gebruikers van on-premises MDM-beheerde Windows 10-computers, en gebruikers kunnen deze apps nu zelf installeren vanaf de bedrijfsportal.
Als de Bedrijfsportal langer dan 15 minuten open is, wordt in deze technische preview-versie een fout bericht weer gegeven. U kunt het probleem omzeilen door de Bedrijfsportal opnieuw te starten.  

### <a name="before-you-start"></a>Voordat u begint  

#### <a name="server-prerequisites"></a>Server vereisten  

-   .NET 4,5 of hoger (opnieuw opstarten nood zakelijk)  

-   Power Shell 3,0 voor configuratie script (opnieuw opstarten nood zakelijk)  

#### <a name="client-prerequisites"></a>Client vereisten  

-   Windows 10 Desktop 1511 (OS Build 10586,218) of hoger  

#### <a name="general-prerequisites"></a>Algemene vereisten  

-   Zorg ervoor dat u de [voorbereidings stappen voor on-premises Mobile Device Management](https://technet.microsoft.com/library/mt613153.aspx) hebt voltooid en [uw apparaten hebt geregistreerd](https://technet.microsoft.com/library/mt627870.aspx).  

-   Voor de beste ervaring bij het installeren van toepassingen bij gebruik van de Bedrijfsportal, moet u ervoor zorgen dat Configuration Manager een actieve verbinding met Microsoft Intune heeft.  

-   Als u kiest voor de optie voor bulk registratie, configureert u de affiniteit tussen gebruikers en apparaten voor het Inge schreven apparaat voordat u dit scenario probeert.  

### <a name="configuration-steps"></a>Configuratiestappen  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>De toepassingscatalogus-rollen installeren en ondersteuning voor het beheer van mobiele apparaten inschakelen  

1.  De rollen van de toepassingscatalogus-webservice en de website toevoegen  

    1.  Selecteer **https-modus** en de optie **mobiele apparaten toestaan deze Toepassingscatalogus-webservicepunt te gebruiken** .  

    2.  Beperkingen in deze technische preview:  

        -   U moet bestaande toepassingscatalogus rollen verwijderen voordat u de optie selecteert om mobiele apparaten verbinding te laten maken.  

        -   Zorg ervoor dat er slechts één set toepassingscatalogus rollen en de rollen zich op hetzelfde site systeem bevinden als de rollen inschrijvings punt en inschrijvings proxy punt.  

2.  Controleer of de volgende onderdelen operationeel zijn vanuit het knoop punt onderdeel status in de Configuration Manager-console:  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Grenzen configureren  
 Configureer de vereiste grenzen voor distributie punten op intranet.  

> [!NOTE]  
>  Er worden op dit moment alleen grenzen van IPv4-bereiken ondersteund voor Mobile Device Management.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>De Bedrijfsportal-toepassing en-configuratie implementeren  

1. Gebruik het configuratie script dat is opgenomen in de Technical Preview om de Bedrijfsportal-implementatie en-configuratie voor te bereiden:  

   1. Open een Power shell-opdracht venster met verhoogde bevoegdheden.  

   2. Run **Set-ExecutionPolicy RemoteSigned**  

   3. Vanuit de map ** &lt;SCCM Installation Directory\>\Cd.latest\SMSSETUP\TOOLS\MDM** run **.\ConfigurationScript.ps1**  

      Het configuratie script doet het volgende:  

   4. Hiermee maakt u een Configuration Manager-toepassing met een implementatie type voor een Windows-app-pakket met behulp van **CompanyPortalOnPremisesMDM. appx** in dezelfde map.  

   5. Hiermee maakt u een configuratie-item en configuratie basislijn waarmee de Bedrijfsportal worden geconfigureerd.  

   6. Hiermee implementeert u de configuratie basislijn en de toepassing en voegt u de toepassing toe aan alle distributie punten.  

   > [!NOTE]
   >  Als de toepassingscatalogus rollen zich niet op dezelfde locatie bevinden als de primaire site, voert u de volgende acties uit:  
   > 
   > - Zoek in de werk ruimte **activa en naleving** het configuratie-item **ONPREMMDM Portal Configuration CI-server url's**  
   >   -   Wijzig de waarde van de **compliantie regels** in de volledig gekwalificeerde domein naam van het site systeem waar de toepassingscatalogus rollen zich bevinden.  

2. Nadat de Bedrijfsportal toepassing en de bijbehorende configuratie zijn geïmplementeerd, controleert u of de toepassings-en configuratie basislijn compatibel zijn met de sectie **implementaties** van de Configuration Manager-console. De Bedrijfsportal wordt weer gegeven als **bedrijfsportal (Technical Preview)** in het menu Start op het apparaat.  

### <a name="try-it-out"></a>Probeer het nu!  
 Voer de volgende taken uit en laat ons weten hoe het werkt met behulp van ons feedback formulier op de pagina [Configuration Manager feedback programma](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) op de micro soft Connect-site:  

1.  Implementeer verschillende toepassingen met ondersteunde implementatie typen voor een gebruikers verzameling met het implementatie doel **beschikbaar**. Voor deze technische preview worden toepassingen waarvoor goed keuring door de beheerder is vereist, niet ondersteund en worden ze niet weer gegeven in de Bedrijfsportal.  

2.  Gebruikers kunnen vervolgens apps zoeken en installeren vanuit de Bedrijfsportal.  

     Nadat u Bedrijfsportal hebt geopend, ziet u een dialoog venster voor verificatie met de naam **Configuration Manager** de Active Directory referenties van de gebruiker opgeven (in user@domain de vorm van of domein\gebruiker) om u aan te melden.  

##  <a name="new-tabs-for-updates-and-operating-systems-in-software-center"></a><a name="BKMK_SW1"></a>Nieuwe tabbladen voor updates en besturings systemen in Software Center  
 In deze release zijn de volgende wijzigingen aangebracht om de lay-out van de Software Center-toepassing te verbeteren:  

-   Het tabblad **toepassingen** is opgesplitst in drie afzonderlijke tabbladen **voor updates**, **besturings systemen** (die eerder zijn gevonden in de lijst met **filters** ) en **toepassingen**.  

##  <a name="service-a--server-group"></a><a name="BKMK_ServerGroups"></a>Een server groep onderhouden  
 Technical Preview voor Configuration Manager, versie 1511, bevat de mogelijkheid om een verzameling te maken waarbij alle apparaten in de verzameling een server groep vormen. Vervolgens kunt u de instellingen van de Server groep zodanig configureren dat deze worden gebruikt wanneer u software-updates implementeert voor de Server groep, het percentage van de computers die op een bepaald moment worden bijgewerkt, beheren en Power shell-scripts na de implementatie configureren om aangepaste acties uit te voeren.  

 Technical Preview voor Configuration Manager, versie 1605, voegt de mogelijkheid toe om de computers in de Server groep bij te werken in een opgegeven volg orde die u definieert, voegt uitgebreide bewaking toe om de status van de computers in de Server groep weer te geven en biedt de mogelijkheid om de implementatie vergrendelingen te wissen die handig zijn wanneer clients de software-updates niet konden installeren en ervoor zorgen dat andere clients de software-  

### <a name="try-it-out"></a>Probeer het nu!  
 Voer de volgende taken uit en laat ons weten hoe het werkt met behulp van ons feedback formulier op de pagina [Configuration Manager feedback programma](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) op de micro soft Connect-site:  

-   Ik kan een verzameling maken die een server groep vertegenwoordigt. Voor deze test kunt u de regels voor het verzamelen van lidmaatschap configureren om 2 computers in deze verzameling te hebben.   

-   Ik kan opgeven dat computers in de Server groep software-updates in een specifieke volg orde installeren op basis van de instellingen van de Server groep voor de verzameling. Gebruik de voorbeeld scripts in de procedure om de scripts voor de pre-implementatie en na de implementatie op te geven.  

-   Ik kan een software-update implementeren voor deze verzameling. Controleer de bestanden start. txt en end. txt (die zijn gemaakt op basis van de voorbeeld scripts) in C:\Temp en controleer de begin-en eind tijden voor de implementatie op de computers in de Server groep. Raadpleeg het bestand UpdatesDeployment. log voor meer informatie.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Een verzameling voor een server groep maken  

1.  [Maak een verzameling apparaten](https://technet.microsoft.com/library/gg712295.aspx) die de computers in de Server groep bevat.  

2.  Klik in de werk ruimte **activa en naleving** op **apparaten verzamelingen**, klik met de rechter muisknop op de verzameling met de computers in de Server groep en klik vervolgens op **Eigenschappen**.  

3.  Selecteer op het tabblad **Algemeen** de optie **alle apparaten zijn onderdeel van dezelfde server groep**en klik vervolgens op **instellingen**.  

4.  Geef op de pagina **instellingen voor Server groep** een van de volgende instellingen op:  

    -   **Toestaan dat een percentage van de machines tegelijk wordt bijgewerkt**: Hiermee geeft u op dat alleen een bepaald percentage van clients tegelijk wordt bijgewerkt. Als de verzameling bijvoorbeeld 10 clients heeft en de verzameling zodanig is geconfigureerd dat 30% van de clients tegelijkertijd wordt bijgewerkt, worden er door slechts drie clients software-updates op een bepaald moment geïnstalleerd.  

    -   **Toestaan dat een aantal machines tegelijk wordt bijgewerkt**: Hiermee geeft u op dat slechts een bepaald aantal clients tegelijk wordt bijgewerkt.  

    -   **De onderhouds volgorde opgeven**: Hiermee geeft u op dat de clients in de verzameling op één keer worden bijgewerkt in de volg orde die u configureert. Een client installeert alleen software-updates nadat de installatie van de software-updates is voltooid door de client die zich voordoet in de lijst.  

5.  Geef aan of u een script voor het uitvoeren van een voor bereiding (knooppunt afvoer) of na de implementatie (knoop punt voor het hervatten) wilt gebruiken.  

    > [!TIP]  
    >  Hier volgen enkele voor beelden die u kunt gebruiken bij het testen van scripts voor vóór de implementatie en na de implementatie die de huidige tijd naar een tekst bestand schrijven:  
    >   
    >  **Pre-implementatie**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Na de implementatie**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Software-updates implementeren in de Server groep en de status van de monitor  

1.  [Software-updates implementeren](https://technet.microsoft.com/library/gg712304.aspx) in de verzameling van Server groepen.  

2.  [Controleer de implementatie van de software-update](https://technet.microsoft.com/library/gg712304.aspx). Naast de standaard weergave weergaven voor de implementatie van software-updates, wordt een nieuwe status beschrijving weer gegeven wanneer een client op zijn beurt wacht om de software-updates te installeren. **Wachten op vergren deling** wordt weer gegeven voor deze nieuwe status.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>De implementatie vergrendelingen wissen voor computers in een server groep  

1.  Klik in de werk ruimte **activa en naleving** op **apparaten verzamelingen**en klik op de verzameling om de implementatie vergrendelingen te wissen.  

2.  Klik op het tabblad **Start** , in de groep **implementatie** , op **Server groep implementatie vergrendelingen wissen**. De implementatie vergrendelingen kunnen hand matig worden gewist wanneer clients de software-updates niet hebben geïnstalleerd en de software-updates niet worden geïnstalleerd door andere clients.  

##  <a name="support-for-microsoft-defender-advanced-threat-protection-service"></a><a name="BKMK_ATP"></a>Ondersteuning voor micro soft Defender Advanced Threat Protection-Service  
 Micro soft Defender Advanced Threat Protection (ATP) is een service waarmee bedrijven geavanceerde aanvallen op hun netwerken kunnen detecteren, onderzoeken en hierop reageren. Micro soft Defender ATP is voorheen bekend als Windows Defender ATP. Meer informatie over [micro soft Defender ATP](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Configuration Manager kunt u helpen bij het bewaken en controleren van beheerde Windows 10 jubileum Edition-client apparaten.  

### <a name="try-it-now"></a>Probeer het nu!  
 Voer de volgende taken uit en laat ons weten hoe het werkt met behulp van ons feedback formulier op de pagina [Configuration Manager feedback programma](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) op de micro soft Connect-site:  

- Apparaten onboarden naar de online service micro soft Defender Advanced Threat Protection (ATP)  

- Micro soft Defender ATP-implementatie bewaken op beheerde apparaten  

  **Vereisten**  

- Abonnement op de micro soft Defender Advanced Threat Protection-online service  

- Clients met Windows 10, jubileum Edition (build 14328 en hoger)  

- Een configuratie bestand voor de onboarding van de client maken  

  ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Een onboarding-configuratie bestand maken  

  1.  Aanmelden bij de micro soft Defender ATP online-service  

  2.  Klik op de **client on-board** menu opdracht  

  3.  Selecteer **Configuration Manager** en klik op **pakket downloaden**.  

  4.  Down load het gecomprimeerde archief bestand (. zip) en pak de inhoud uit.  


##### <a name="onboard-devices-for-microsoft-defender-atp"></a>Onboarding-apparaten voor micro soft Defender ATP  

1. Ga in de Configuration Manager-console **naar activa en naleving** > **overzicht** > **Endpoint Protection** > **Windows Defender ATP-beleid** en klik op **Windows Defender ATP-beleid maken**. De wizard micro soft Defender ATP-beleid wordt geopend.  

2. Typ de **naam** en **Beschrijving** voor het micro soft Defender ATP-beleid en selecteer **onboarding**. Klik op Volgende.  

3. **Blader** naar het configuratie bestand dat is opgenomen in de micro soft Defender ATP Cloud service-Tenant van uw organisatie. Klik op **Volgende**.  

4. Geef de bestands voorbeelden op die worden verzameld en gedeeld met beheerde apparaten voor analyse.  

   - **Geen** : er worden geen voorbeeld bestanden verzameld voor analyse  

   - **Draag bare uitvoer bare bestanden** : bestanden zoals programma bestanden (. exe), dynamische bibliotheek koppelings bestanden (. dll), lettertype bestanden en vergelijk bare bestanden die kunnen worden misbruikt in Cyber aanvallen, worden verzameld en gedeeld voor analyse  

     Klik op **Volgende**.  

5. Bekijk de samen vatting en voltooi de wizard.  

6. U kunt het micro soft Defender ATP-beleid nu implementeren op beheerde client computers door te klikken op **implementeren**.  

##### <a name="monitor-microsoft-defender-atp"></a>Micro soft Defender ATP bewaken  

1.  Navigeer in de Configuration Manager-console naar **bewakings** > **overzicht** > **beveiliging** en klik vervolgens op **Windows Defender ATP**.  

2.  Bekijk het micro soft Defender Advanced Threat Protection-dash board.  

    -   **Implementatie status van de Windows Defender-agent** : het aantal en percentage van de in aanmerking komende beheerde client computers met actief micro soft Defender ATP-beleid, onboarded  

    -   **Windows Defender atp status van agent** : percentage van de rapportage status van client computers voor de micro soft Defender ATP-agent  

        -   **Healthy** Goed werkt correct  

        -   **Inactief** : er zijn geen gegevens naar de service verzonden tijdens de tijds periode  

        -   **Agent status** : de systeem service voor de agent in Windows is niet actief  

        -   **Er is geen onboarding** -beleid toegepast, maar de agent heeft geen beleid voor de onboarding gemeld  

##  <a name="on-premises-device-health-attestation"></a><a name="BKMK_DHA"></a>On-premises Apparaatstatusverklaring  
 Health Attestation voor Windows 10-apparaten kan nu worden geconfigureerd om te communiceren met behulp van de on-premises infra structuur. Beheerders kunnen opgeven of rapportage plaatsvindt via de Cloud of on-premises resources. Als on-premises is geselecteerd voor Health Attestation-rapportage, kan een URL worden opgegeven voor de service. Hierdoor kunnen client-Pc's zonder Internet toegang apparaten inschakelen en beheren met Health Attestation.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Status verklaring inschakelen voor on-premises apparaten  
 In 1605 hebben we enkele fouten opgelost die zijn gedetecteerd in 1604 Technical Preview.  Als u dit wilt uitproberen, configureert u de on-premises Health Attestation-service met de instellingen van de client agent.  

1.  Ga in de Configuration Manager-console naar **beheer** > **overzicht** > **client instellingen**en stel **on-premises Health Attestation-service gebruiken** in op **Ja**.  

2.  Geef de **URL op voor de on-premises statusverklaringsservice**en klik op **OK**.  

##  <a name="new-restart-options-for-windows-10-clients-after-software-update-installation"></a><a name="BKMK_RestartOptions"></a>Nieuwe opties voor opnieuw opstarten voor Windows 10-clients na de installatie van de software-update  
 Wanneer een software-update waarvoor opnieuw opstarten is vereist, wordt geïmplementeerd met Configuration Manager en op een computer is geïnstalleerd, wordt het opnieuw opstarten in behandeling gepland en wordt een dialoog venster voor opnieuw opstarten weer gegeven. Op dit moment kunt u voor Windows 8 en hoger als u de computer afsluit of opnieuw opstarten met behulp van de Windows-energie opties (in plaats van vanuit het dialoog venster voor opnieuw opstarten), het dialoog venster voor opnieuw opstarten blijft staan nadat de computer opnieuw is opgestart en de computer opnieuw moet worden opgestart om de ingestelde deadline te configureren. In deze technische preview-versie is de optie **bijwerken en opnieuw opstarten** en **bijwerken en afsluiten** beschikbaar op Windows 10-computers in de Windows-energie beheer wanneer het opnieuw opstarten in behandeling is voor een Configuration Manager software-update. Nadat u een van deze opties hebt gebruikt, wordt het dialoogvenster voor opnieuw opstarten niet weergegeven nadat de computer opnieuw wordt opgestart.  

##  <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a><a name="BKMK_IMEI"></a>Apparaten in bedrijfs eigendom vooraf declareren met IMEI of iOS-serie nummer  
 U kunt nu apparaten in bedrijfs eigendom identificeren door de IMEI-nummers (International Station Mobile Equipment Identity) te importeren. U kunt een bestand met door komma's gescheiden waarden (. CSV) met IMEI-nummers van het apparaat uploaden of u kunt de apparaatgegevens hand matig invoeren.  U kunt ook serie nummers importeren voor iOS-apparaten.  Met geïmporteerde gegevens wordt het eigendom van de apparaten ingesteld die zijn Inge schreven als ' zakelijk '.  Er is nog steeds een intune-licentie vereist voor elke gebruiker die toegang heeft tot de service.  

### <a name="try-it-out"></a>Probeer het nu!  
 Voer de volgende taken uit en laat ons weten hoe het werkt met behulp van ons feedback formulier op de pagina [Configuration Manager feedback programma](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) op de micro soft Connect-site:  

-   Importeer een set IMEI-nummers in een CSV-bestand. Elke rij kan het IMEI-nummer bevatten, gevolgd door een detail veld.  

-   Importeer IMEI-nummers hand matig vanuit de Configuration Manager-console.  

-   Een set iOS-serie nummers importeren in een CSV-bestand. Elke rij bevat een getal gevolgd door eventuele Details van het apparaat.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Vooraf declareren van apparaten in bedrijfseigendom met IMEI-nummer of iOS-serienummer  

1. Ga in de Configuration Manager-console naar **activa en naleving** > **overzicht** > **van alle apparaten** > die eigendom zijn van het bedrijf en klik vervolgens op **vooraf gedeclareerde apparaten maken**.**Pre-declared Devices** De wizard vooraf gedeclareerde apparaten wordt geopend.  

2. Geef op hoe u apparaatgegevens wilt toevoegen:  

   -   **Een CSV-bestand met IMEI-nummers en details uploaden** : als u een lijst met getallen wilt uploaden, raadpleegt u stap #3.  

   -   **IMEI-nummers en Details hand matig toevoegen** : als u de informatie hand matig wilt invoeren, typt u het IMEI-nummer of IOS-serie nummer en de gegevens voor de apparaten en gaat u verder met stap #4.  

3. Voor geüploade bestanden, bladert u naar het. CSV-bestand met informatie voor het vooraf declareren van apparaten in bedrijfs eigendom. Het bestand moet de volgende indeling hebben, met uitzonde ring van de bovenste rij (alleen voor de richt lijnen):  

   |**IMEI #**|**iOS-serieel**|**Besturingssysteem**|**Details**|
   |---|---|---|---|
   |123456789012345||WINDOWS|Windows-apparaat dat eigendom is van het bedrijf|
   |123456789012|A0BCD0EFGH0J|iOS|iOS-apparaten die bedrijfseigendom zijn|
   |123456789012346||ANDROID|Android-apparaat dat eigendom is van het bedrijf|

    **Kolommen**  

   - Kolom 1: IMEI-nummer: een IMEI-nummer of iOS-serie nummer is vereist voor elke rij  

   - Kolom 2: iOS-serie nummer: alleen iOS-serie nummers kunnen vooraf worden gedeclareerd. IMEI-nummer gebruiken voor andere platformen  

   - Kolom 3: besturings systeem van het apparaat (vereist hoofdletter gebruik):  

     -   IOS: alle iOS-apparaten  

     -   WINDOWS: bevat Windows Phone, Window 10 Mobile en Windows-Pc's  

     -   ANDROID: alle Android-apparaten  

   - Kolom 4: Details: aanvullende informatie over apparaten die wordt weer gegeven in de Configuration Manager-console  

     Klik op **Volgende**.  

4. Bekijk de resultaten van het importeren van het bestand. De details van eerder geïmporteerde IMEI-of serie nummers worden bijgewerkt met nieuwe gegevens.  Klik op **volgende** om door te gaan of op **terug** om de bijgewerkte gegevens op te slaan en de wizard te volt ooien.  
