---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: Meer informatie over nieuwe functies die beschikbaar zijn in de Configuration Manager Technical Preview-vertakking versie 1807.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 398f16b8f75d894030d76406807f74bdaa4be9d5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714785"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Mogelijkheden in Configuration Manager Technical Preview-versie 1807 

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1807. Installeer deze versie om nieuwe functies bij te werken en toe te voegen aan uw technische preview-site. 

Raadpleeg het artikel [Technical Preview](technical-preview.md) voordat u deze update installeert. In dit artikel wordt u vertrouwd met de algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Bekende problemen 

### <a name="issues-with-office-365-software-updates"></a><a name="ki_o365"></a>Problemen met Office 365-software-updates
<!--521365-->
Als u updates voor Office 365 beheert met behulp van de branches van Technical Preview versie 1806 en 1806,2, kunnen ze niet worden geïnstalleerd op clients. 

#### <a name="workaround"></a>Tijdelijke oplossing
- Verwijder bestaande implementatie pakketten en software-update groepen voor Office 365.  

- Vanaf 31 juli 2018 synchroniseert u Office 365-software-updates en implementeert u alleen de meest recente updates.  



</br>

**In de volgende secties worden de nieuwe functies beschreven voor het uitproberen van deze versie:**  


## <a name="community-hub"></a><a name="bkmk_hub"></a>Community Hub
<!--1357766-->

De Community Hub is een centrale locatie voor het delen van nuttige Configuration Manager objecten met anderen. Bekijk de nieuwe **Community** -werk ruimte in de Configuration Manager-console en selecteer het knoop punt **hub** . Gebruik de Community Hub om de volgende typen Configuration Manager-objecten te downloaden: 
- Scripts
- Configuratie-items

![Configuration Manager-console, Community-werk ruimte, hub-knoop punt](media/1357766-hub.png)

Als u meer informatie over een beschikbaar item wilt weer geven, klikt u op deze in de hub. Klik op de pagina Details op **downloaden** om het item te verkrijgen. Wanneer u een item downloadt van de hub, wordt het automatisch toegevoegd aan uw site. 

![Configuration Manager-console, Community-werk ruimte, hub-knoop punt, detail pagina](media/1357766-hub-details.png)

De werk ruimte **Community** bevat ook de volgende knoop punten:

- **Documentatie**: de [documentatie bibliotheek](https://docs.microsoft.com/sccm/) van Configuration Manager wordt weer gegeven  

- **Feedback**: de Configuration Manager [UserVoice-site](https://configurationmanager.uservoice.com/) wordt weer gegeven  


### <a name="prerequisites"></a>Vereisten

- Gebruik de Configuration Manager-console op het besturings systeem van de client.  

    - Als alternatief, maar niet aanbevolen: Schakel op een server besturingssysteem [Internet Explorer uit: verbeterde beveiliging](https://go.microsoft.com/fwlink/?LinkId=253461).  

- De computer met de-console vereist Internet toegang en connectiviteit met de volgende sites:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Bekend probleem

Items die bijdragen aan de hub, zijn momenteel niet beschikbaar in deze versie. 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a>Het station opgeven voor offline-installatie kopie onderhoud van besturings systemen  
<!--1358924-->

Op basis van uw [UserVoice-feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive)geeft u nu het station op dat Configuration Manager gebruikt tijdens het offline onderhoud van installatie kopieën van besturings systemen. Dit proces kan een grote hoeveelheid schijf ruimte in beslag nemen met tijdelijke bestanden, zodat u met deze optie de mogelijkheid hebt om het te gebruiken station te selecteren. 


### <a name="try-it-out"></a>Probeer het nu!

Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) met uw mening over de functie.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Klik in het lint op **site onderdelen configureren** en selecteer **Software-update punt**.  

2. Ga naar het tabblad **offline onderhoud** en geef de optie op voor **een lokaal station dat moet worden gebruikt door offline onderhoud van installatie kopieën**.  

Deze instelling is standaard **automatisch**. Met deze waarde Configuration Manager selecteert u het station waarop het is geïnstalleerd. 

Tijdens offline onderhoud slaat Configuration Manager tijdelijke bestanden op in de map `<drive>:\ConfigMgr_OfflineImageServicing`. Ook worden de installatie kopieën van het besturings systeem in deze map gekoppeld. 

Controleer het logboek bestand **OfflineServicingMgr. log** . 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a>Synchronisatie activiteit voor gezamenlijk beheerde apparaten vanuit intune
<!--1358565-->

Weer geven in de Configuration Manager-console of een door co beheerd apparaat actief is met Microsoft Intune. Deze status is gebaseerd op gegevens uit het [intune-Data Warehouse](https://docs.microsoft.com/intune/reports-nav-create-intune-reports). Het dash board **client status** in de Configuration Manager-console bevat **inactieve clients die gebruikmaken van intune**. Deze nieuwe categorie is voor door co beheerde apparaten die inactief zijn en Configuration Manager, maar die in de afgelopen week zijn gesynchroniseerd met de intune-service.


### <a name="try-it-out"></a>Probeer het nu!

Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) met uw mening over de functie.

Als u uw site al hebt ingesteld voor co-beheer: 

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt voor **co-beheer** . Klik op **Eigenschappen** in het lint.  

2. Ga naar het tabblad **rapportage** . Klik op **Aanmelden** en verifiëren. Klik vervolgens op **bijwerken** om Lees machtigingen voor het intune-data warehouse in te scha kelen.  

3. Nadat de site is gesynchroniseerd met intune, gaat u naar de werk ruimte **bewaking** en selecteert u het knoop punt **client status** . In de sectie **algehele client status** raadpleegt u de rij voor **inactieve clients die intune gebruiken**.  

Zie [co-beheer voor Windows 10-apparaten](../../comanage/overview.md)voor meer informatie over het inschakelen van co-beheer.



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a>Toepassingen herstellen
<!--1357866-->

Op basis van uw [UserVoice-feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application)geeft u nu een herstel opdracht regel op voor de implementatie typen Windows Installer en script installatie. 


### <a name="try-it-out"></a>Probeer het nu!

Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) met uw mening over de functie.

1. Open in de Configuration Manager-console de eigenschappen van een Windows Installer of het implementatie type script installatie programma.  

2. Ga naar het tabblad **Program ma's** . Geef de opdracht voor het herstellen van het **programma** op.  

3. Implementeer de app. Schakel op het tabblad **implementatie-instellingen** van de implementatie de optie in om **eind gebruikers toe te staan om deze toepassing te herstellen**.  


### <a name="known-issue"></a>Bekend probleem

De knop Nieuw in Software Center voor gebruikers voor het **herstellen** van de app is niet zichtbaar in deze versie.  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a>Toepassings aanvragen via e-mail goed keuren
<!--1321550-->

E-mail meldingen configureren voor aanvragen voor het goed keuren van toepassingen. Wanneer een gebruiker een toepassing aanvraagt, ontvangt u een e-mail bericht. Klik op koppelingen in het e-mail bericht om de aanvraag goed te keuren of te weigeren zonder dat de Configuration Manager-console is vereist.


### <a name="prerequisites"></a>Vereisten

#### <a name="to-send-email-notifications"></a>E-mail meldingen verzenden
- De [optionele functie](../servers/manage/install-in-console-updates.md#bkmk_options) **voor het goed keuren van toepassings aanvragen voor gebruikers per apparaat**inschakelen.  

- [E-mail meldingen voor waarschuwingen](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts)configureren.  

#### <a name="to-approve-or-deny-requests-from-email"></a>Aanvragen van e-mail goed keuren of weigeren
Als u deze vereisten niet configureert, verzendt de site een e-mail melding voor toepassings aanvragen zonder koppelingen om de aanvraag goed te keuren of te weigeren.  

- Schakel in het gedeelte site-eigenschappen **rest-eind punt in voor alle provider rollen op deze site en sta Configuration Manager verkeer van de Cloud beheer gateway toe**. Zie [OData endpoint Data Access](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)voor meer informatie.  

    - De SMS_EXEC-service opnieuw starten nadat het REST-eind punt is ingeschakeld

- [Cloudbeheergateway](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- De site onboarden naar [Azure-Services](../servers/deploy/configure/azure-services-wizard.md) voor **Cloud beheer**  

    - [Azure AD-gebruikers detectie](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) inschakelen  

    - Configureer de volgende instellingen voor deze systeem eigen app hand matig in azure AD:  

        - **Omleidings-URI**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`. Gebruik de Fully Qualified Domain Name (FQDN) van de CMG-service (Cloud Management Gateway), bijvoorbeeld GraniteFalls.Contoso.com.   

        - **Manifest**: Stel **oauth2AllowImplicitFlow** in op True:`"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Probeer het nu!

Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) met uw mening over de functie.

1. Implementeer in de Configuration Manager-console een toepassing als beschikbaar voor een verzameling gebruikers. Schakel op de pagina **implementatie-instellingen** het in voor goed keuring. Voer vervolgens *één* e-mail adres in om een melding te ontvangen.  

     > [!Note]  
     > Iedereen in uw Azure AD-organisatie die het e-mail bericht ontvangt, kan de aanvraag goed keuren. Stuur het e-mail bericht niet door naar anderen, tenzij u wilt dat ze actie ondernemen.  

2. Als gebruiker vraagt u de toepassing op in Software Center.  

3. U ontvangt een e-mail bericht vergelijkbaar met het volgende voor beeld:  

![Voor beeld van een e-mail melding voor een toepassings goedkeuring](media/1321550-email.png)

> [!Note]  
> De koppeling die u wilt goed keuren of weigeren, is voor eenmalig gebruik. U kunt bijvoorbeeld een groeps alias configureren voor het ontvangen van meldingen. MB keurt de aanvraag goed. Bruce kan de aanvraag nu niet weigeren.  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a>Verbetering van de script uitvoer
<!--1236459-->

U kunt nu gedetailleerde script uitvoer weer geven in de RAW-of Structured JSON-indeling. Met deze opmaak wordt de uitvoer eenvoudiger te lezen en te analyseren. Als het script geldige tekst in JSON-indeling retourneert, bekijkt u de gedetailleerde uitvoer als **JSON-uitvoer** of **onbewerkte uitvoer**. Anders is de enige optie **script uitvoer**. 

#### <a name="example-script-output-is-valid-json"></a>Voor beeld: script uitvoer is een geldige JSON
Cmd`$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Voor beeld: script uitvoer is geen geldige JSON
Cmd`Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Probeer het nu!

Probeer de taken uit te voeren. Stuur vervolgens [feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) met uw mening over de functie.

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **Apparaatsets** . Klik met de rechter muisknop op een verzameling en selecteer **script uitvoeren**. Zie [Power shell-scripts maken en uitvoeren vanuit de Configuration Manager-console](../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie over het maken en gebruiken van scripts.  

2. Voer een script uit op de doel verzameling.  

3. Selecteer op de pagina **controle van script status** van de wizard script uitvoeren het tabblad **samen vatting** onderaan. Wijzig de twee vervolg keuzelijsten bovenaan in **script uitvoer** en **gegevens tabel**. Dubbel klik vervolgens op de rij met resultaten om het dialoog venster **gedetailleerde uitvoer** te openen.  

4. Selecteer op de pagina **controle van script status** van de wizard script uitvoeren het tabblad Details van de **uitvoering** onder. Dubbel klik op een rij met resultaten om het dialoog venster gedetailleerde uitvoer voor dat apparaat te openen.  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a>Verbetering van software-updates van derden
<!--1358714-->

U kunt nu de eigenschappen van aangepaste catalogussen wijzigen.

Zie [ondersteuning voor software-updates van derden voor aangepaste catalogussen](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)voor meer informatie.



## <a name="next-steps"></a>Volgende stappen

Voor meer informatie over het installeren of bijwerken van de technische preview-vertakking raadpleegt u [Technical Preview](technical-preview.md).    

Zie voor meer informatie over de verschillende branches van Configuration Manager [welke vertakking van Configuration Manager moet ik gebruiken?](../understand/which-branch-should-i-use.md)
