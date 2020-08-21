---
title: Updates van derden inschakelen
titleSuffix: Configuration Manager
description: Updates van derden inschakelen in Configuration Manager
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3192cd8177075542ffc86ab236b817db5befca1d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696885"
---
# <a name="enable-third-party-updates"></a>Updates van derden inschakelen 

*Van toepassing op: Configuration Manager (huidige vertakking)*

Vanaf versie 1806 kunt u met het knoop punt **Software-update catalogi** van derden in de Configuration Manager-console een abonnement nemen op catalogi van derden, hun updates publiceren op uw software-update punt (SUP) en deze vervolgens implementeren op clients.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> Configuration Manager schakelt deze functie standaard niet in. Voordat u het gebruikt, schakelt u de optionele functie **ondersteuning voor updates van derden op clients in**. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).


## <a name="prerequisites"></a>Vereisten 
- Er is voldoende schijf ruimte op de WSUSContent-map van het hoogste niveau voor het opslaan van de binaire bron inhoud voor software-updates van derden.
    - De hoeveelheid vereiste opslag is afhankelijk van de leverancier, typen updates en specifieke updates die u voor implementatie publiceert.
    - Als u de map WSUSContent naar een ander station met meer vrije ruimte wilt verplaatsen, raadpleegt u de [locatie wijzigen waar de update lokaal](/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally) blog bericht wordt opgeslagen in WSUS.
- De synchronisatie service voor software-updates van derden vereist Internet toegang.
    - Voor de lijst met partner catalogi is download.microsoft.com via HTTPS-poort 443 vereist. 
    -  Internet toegang tot catalogi van derden en het bijwerken van inhouds bestanden. Andere andere poorten dan 443 zijn mogelijk nodig.
    - Updates van derden gebruiken dezelfde proxy instellingen als de SUP.
- Voor Configuration Manager versies voorafgaand aan 1910 kan de beveiligingsrol **Software-update beheer** geen catalogi van derden synchroniseren. U hebt de beveiligingsrol **volledige beheerder** nodig om de catalogussen te synchroniseren.


## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Aanvullende vereisten wanneer het SUP op afstand van de site server op het hoogste niveau is 

1. SSL moet zijn ingeschakeld op de SUP als deze extern is. Hiervoor is een certificaat voor Server verificatie gegenereerd van een interne certificerings instantie of via een open bare provider.
    - [SSL configureren op WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - Wanneer u SSL op WSUS configureert, noteert u enkele van de webservices en de virtuele mappen altijd HTTP en niet HTTPS. 
        - Configuration Manager downloaden van inhoud van derden voor software-update pakketten vanuit uw WSUS-inhoudsmap via HTTP.   
    - [SSL configureren voor het SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Wanneer u de configuratie van het WSUS-handtekening certificaat van derden instelt op **Configuration Manager het certificaat beheert** in de eigenschappen van de software-update punt component, zijn de volgende configuraties vereist voor het maken van het zelfondertekende WSUS-handtekening certificaat: 
   - Extern REGI ster moet zijn ingeschakeld op de SUP-server.
   -  Het **account voor de WSUS-server verbinding** moet externe register machtigingen hebben op de sup/WSUS-server. 


3. Maak de volgende register sleutel op de site server Configuration Manager: 
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`maakt u een nieuwe DWORD met de naam **EnableSelfSignedCertificates** met de waarde `1` . 

4. Het installeren van het zelfondertekende WSUS-handtekening certificaat voor vertrouwde uitgevers en vertrouwde basis archieven op de externe SUP-server inschakelen:
   - Het **account voor de WSUS-server verbinding** moet machtigingen voor extern beheer op de sup-server hebben.

     Als dit item niet mogelijk is, exporteert u het certificaat van de WSUS-archief van de lokale computer naar de vertrouwde uitgever en de vertrouwde basis archieven. 

> [!NOTE] 
>Het **account voor de WSUS-server verbinding** kan worden geïdentificeerd door het tabblad **proxy-en account instellingen** te bekijken in de eigenschappen van de site systeemrol van het sup. Als er geen account is opgegeven, wordt het computer account van de site server gebruikt.

## <a name="enable-third-party-updates-on-the-sup"></a>Updates van derden inschakelen voor het SUP
Als u deze optie inschakelt, kunt u zich abonneren op update catalogussen van derden in de Configuration Manager-console. U kunt deze updates vervolgens publiceren naar WSUS en deze implementeren op clients. De volgende stappen moeten eenmaal per hiërarchie worden uitgevoerd om de functie voor gebruik in te scha kelen en in te stellen. De stappen moeten mogelijk opnieuw worden uitgevoerd als u ooit de WSUS-server op het hoogste niveau vervangt. 

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer het knoop punt **sites** .
2. Selecteer de site op het hoogste niveau in de hiërarchie. Klik in het lint op **site onderdelen configureren**en selecteer **Software-update punt**.
3. Schakel over naar het tabblad **updates** van derden. Selecteer de optie **software-updates van derden inschakelen**.

    ![Scherm afbeelding van SUP-eigenschappen van derden](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Het WSUS-handtekening certificaat configureren
U moet beslissen of u wilt dat Configuration Manager het WSUS-handtekening certificaat van derden automatisch beheert met behulp van een zelfondertekend certificaat, of dat u het certificaat hand matig moet configureren. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Het WSUS-handtekening certificaat automatisch beheren
Als u geen PKI-certificaten nodig hebt, kunt u ervoor kiezen om de handtekening certificaten voor updates van derden automatisch te beheren. Het WSUS-certificaat beheer wordt uitgevoerd als onderdeel van de synchronisatie cyclus en wordt geregistreerd in de `wsyncmgr.log` . 

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer het knoop punt **sites** .
2. Selecteer de site op het hoogste niveau in de hiërarchie. Klik in het lint op **site onderdelen configureren**en selecteer **Software-update punt**.
3. Schakel over naar het tabblad **updates** van derden. Selecteer de optie **Configuration Manager het certificaat beheert**. 
4. Er wordt een nieuw certificaat van het type **WSUS-ondertekening** van derden gemaakt in het knoop punt **certificaten** onder **beveiliging** in de werk ruimte **beheer** .  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Het WSUS-handtekening certificaat hand matig beheren
Als u het certificaat hand matig moet configureren, bijvoorbeeld als u een PKI-certificaat wilt gebruiken, moet u [System Center updates Publisher](../tools/updates-publisher-options.md#update-server) of een ander hulp programma gebruiken.  

1. Configureer het handtekening certificaat met behulp van [System Center updates Publisher](../tools/updates-publisher-options.md#update-server).
2. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer het knoop punt **sites** .
3. Selecteer de site op het hoogste niveau in de hiërarchie. Klik in het lint op **site onderdelen configureren**en selecteer **Software-update punt**.
4. Schakel over naar het tabblad **updates** van derden. Selecteer de optie voor **het hand matig beheren van het certificaat**.


## <a name="enable-third-party-updates-on-the-clients"></a>Updates van derden op de clients inschakelen
Schakel updates van derden in op de clients in de client instellingen. Met deze instelling wordt het beleid voor Windows Update Agent ingesteld voor het [toestaan van ondertekende updates voor een intranet locatie van micro soft-Update service](/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location). Deze client instelling installeert ook het WSUS-handtekening certificaat in het archief met vertrouwde uitgevers van de client. De logboek registratie van certificaat beheer is te zien in `updatesdeployment.log` op de-clients.  Voer deze stappen uit voor elke aangepaste client instelling die u wilt gebruiken voor updates van derden. Zie het artikel [over client instellingen](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) voor meer informatie.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **client instellingen** .
2. Selecteer een bestaande aangepaste client instelling of maak een nieuwe. 
3. Selecteer het tabblad **software-updates** aan de linkerkant. Als u dit tabblad niet hebt, moet u ervoor zorgen dat het selectie vakje **software-updates** is ingeschakeld.
4. Stel **software-updates van derden** in op **Ja**. 


## <a name="add-a-custom-catalog"></a>Een aangepaste catalogus toevoegen
*Partner Catalogs* zijn software leveranciers catalogi waarvan de informatie al is geregistreerd bij micro soft. Met partner catalogi kunt u zich abonneren zonder dat u aanvullende informatie hoeft op te geven. Catalogi die u toevoegt, worden *aangepaste catalogi*genoemd. U kunt een aangepaste catalogus toevoegen van een update leverancier van derden aan Configuration Manager. Aangepaste catalogi moeten https gebruiken en de updates moeten digitaal zijn ondertekend. 

1. Ga naar de werk ruimte **software-updates bibliotheek** , vouw **software-updates**uit en selecteer het knoop punt **Software-update catalogi van derden** . 
   
     ![Scherm afbeelding van het knoop punt voor updates van derden](media/third-party-updates-node.PNG)
2. Klik op **aangepaste catalogus toevoegen** op het lint. 

     ![Updates van derden Voeg aangepaste catalogus toe](media/third-party-updates-custom-catalog.png)
1. Geef op de pagina **Algemeen** de volgende items op: 
    - **Download-URL**: een geldig https-adres van de aangepaste catalogus.
    - **Uitgever**: de naam van de organisatie die de catalogus publiceert. 
    - **Naam**: de naam van de catalogus die in de Configuration Manager-console moet worden weer gegeven. 
    - **Beschrijving**: een beschrijving van de catalogus. 
    - **Ondersteunings-URL** (optioneel): een geldig https-adres van een website om hulp te krijgen bij de catalogus. 
    - **Ondersteunings contact** (optioneel): Neem contact op met informatie om hulp te krijgen bij de catalogus. 
2. Klik op **volgende** om het catalogus overzicht te bekijken en te gaan met het volt ooien van de **wizard software-updates**van derden.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>Abonneren op een catalogus van derden en updates synchroniseren
Wanneer u zich abonneert op een catalogus van derden in de Configuration Manager-console, worden de meta gegevens voor elke update in de catalogus gesynchroniseerd met de WSUS-servers voor uw punten. Met de synchronisatie van de meta gegevens kunnen de clients bepalen of een van de updates van toepassing is. Voer de volgende stappen uit voor elke catalogus van derden waarop u zich wilt abonneren:  

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **software-updates** uit en selecteer het knoop punt **Software-update catalogi van derden** .  
2. Selecteer de catalogus waarop u zich wilt abonneren en klik op **Abonneren op catalogus** op het lint. 
    ![Updates van derden Voeg aangepaste catalogus toe](media/third-party-updates-subscribe.png)
3. Het catalogus certificaat controleren en goed keuren.  
   > [!NOTE]
   > 
   > Wanneer u zich abonneert op een Software-Update catalogus van derden, wordt het certificaat dat u in de wizard hebt gecontroleerd en goedgekeurd, aan de site toegevoegd. Dit certificaat is van het type **catalogus met software-updates**van derden. U kunt deze beheren via het knoop punt **certificaten** onder **beveiliging** in de werk ruimte **beheer** .  
4. Voltooi de wizard. Na het eerste abonnement moet de catalogus binnen een paar minuten worden gedownload. 
    - De catalogus synchroniseert automatisch elke 7 dagen.
    - Klik op **Nu synchroniseren** in het lint om een synchronisatie af te dwingen.
5. Nadat de catalogus is gedownload, moeten de meta gegevens van het product worden gesynchroniseerd vanuit de WSUS-Data Base naar de Configuration Manager-Data Base. [Start de synchronisatie van software-updates hand matig](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) om de product informatie te synchroniseren.
6. Zodra de product informatie is gesynchroniseerd, [moet u het sup configureren om het gewenste product te synchroniseren met](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) Configuration Manager.  
7. [Start de synchronisatie van software-updates hand matig](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) om de updates van het nieuwe product te synchroniseren met Configuration Manager.  
8. Wanneer de synchronisatie is voltooid, kunt u de updates van derden in het knoop punt **alle updates** bekijken. Deze updates worden gepubliceerd als updates **met alleen meta gegevens** totdat u ze publiceert. 
     - Het pictogram met de blauwe pijl duidt op een software-update waarbij alleen de metagegevens worden bijgewerkt. ![Pictogram Software-update alleen meta gegevens](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Software-updates van derden publiceren en implementeren 
Zodra de updates van derden zich in het knoop punt **alle updates** bevinden, kunt u kiezen welke updates voor implementatie moeten worden gepubliceerd. Wanneer u een update publiceert, worden de binaire bestanden van de leverancier gedownload en in de WSUSContent-map op het hoogste niveau geplaatst. 

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **software-updates** uit en selecteer het knoop punt **alle software-updates** .
2. Klik op **criteria toevoegen** om de lijst met updates te filteren. Voeg bijvoorbeeld **leverancier** toe voor **HP**. om alle updates van HP weer te geven.  
3. Selecteer de updates die voor uw organisatie zijn vereist. Klik op **inhoud van software-update**van derden publiceren.
    - Met deze actie worden de binaire update bestanden van de leverancier gedownload en opgeslagen in de map WSUSContent op het software-update punt op het hoogste niveau. 
4. [Start de synchronisatie van software-updates hand matig](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) om de status van de gepubliceerde updates van meta gegevens te wijzigen in Implementeer bare updates met inhoud. 
    >[!NOTE]
    >Wanneer u inhoud van software-updates van derden publiceert, worden alle certificaten die worden gebruikt voor het ondertekenen van de inhoud toegevoegd aan de site. Deze certificaten zijn van **het type inhoud van software-updates**van derden. U kunt deze beheren via het knoop punt **certificaten** onder **beveiliging** in de werk ruimte **beheer** .  

5. Controleer de voortgang in het SMS_ISVUPDATES_SYNCAGENT. log. Het logboek bevindt zich op het hoogste niveau van het software-update punt in de map site systeem logs.
6. Implementeer de updates met het proces voor het [implementeren van software-updates](../deploy-use/deploy-software-updates.md) . 
7. Selecteer op de pagina **Download locaties** van de **wizard software-updates implementeren**de standaard optie om **software-updates van Internet te downloaden**. In dit scenario wordt de inhoud al gepubliceerd naar het software-update punt, dat wordt gebruikt voor het downloaden van de inhoud voor het implementatie pakket.
8. Clients moeten een scan uitvoeren en updates evalueren voordat u de nalevings resultaten kunt zien.  U kunt deze cyclus hand matig activeren vanuit het Configuration Manager configuratie scherm op een client door de actie **Scan cyclus voor software-updates** uit te voeren.


## <a name="improvements-for-third-party-updates-starting-in-1910"></a><a name="bkmk_1910"></a> Verbeteringen voor updates van derden vanaf 1910
<!--4469002-->
U hebt nu meer gedetailleerde controle over de synchronisatie van catalogussen met updates van derden. Vanaf Configuration Manager versie 1910 kunt u de synchronisatie planning voor elke afzonderlijke catalogus afzonderlijk configureren. Wanneer u catalogi gebruikt die gecategoriseerde updates bevatten, kunt u synchronisatie zo configureren dat er alleen specifieke categorieën updates worden toegevoegd om te voor komen dat u de volledige catalogus synchroniseert. Als u zeker weet dat u een categorie wilt implementeren met gecategoriseerde catalogi, kunt u deze zo configureren dat deze automatisch wordt gedownload en gepubliceerd in WSUS.

### <a name="set-the-schedule-for-a-catalog-in-a-new-catalog-subscription"></a>Het schema voor een catalogus in een nieuw catalogus abonnement instellen

1. Ga naar de werk ruimte **software bibliotheek** , vouw **software-updates**uit en selecteer het knoop punt **Software-update catalogi** van derden.
1. Selecteer de catalogus waarop u zich wilt abonneren en klik op **Abonneren op catalogus** op het lint.
1. Kies de gewenste opties op de pagina **planning** als u het standaard synchronisatie schema wilt overschrijven:
   - **Eenvoudig schema**: Kies het interval voor uur, dag of maand.
   - **Aangepast schema**: Stel een complex schema in.

### <a name="update-the-schedule-per-catalog"></a>Het schema per catalogus bijwerken

1. Ga naar de werk ruimte **software bibliotheek** , vouw **software-updates**uit en selecteer het knoop punt **Software-update catalogi** van derden.
1. Klik met de rechter muisknop op de catalogus en selecteer **Eigenschappen**.
1. Kies uw opties op het tabblad Planning: 
   - **Eenvoudig schema**: Kies het interval voor uur, dag of maand.
   - **Aangepast schema**: Stel een complex schema in.

### <a name="new-subscription-to-a-third-party-v3-catalog"></a>Nieuw abonnement op een v3-catalogus van een derde partij

> [!IMPORTANT]
> Deze optie is alleen beschikbaar voor v3 update catalogi van derden, die ondersteuning bieden voor categorieën voor updates. Deze opties zijn uitgeschakeld voor catalogi die niet worden gepubliceerd in de nieuwe v3-indeling.


1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **software-updates** uit en selecteer het knoop punt **Software-update catalogi van derden** .
1. Selecteer de catalogus waarop u zich wilt abonneren en klik op **Abonneren op catalogus** op het lint.
1. Kies uw opties op de pagina **categorieën selecteren** :

   - **Alle update Categorieën synchroniseren** (standaard)
       - Synchroniseert alle updates in de Update catalogus van derden in Configuration Manager.
   -  **Categorieën voor synchronisatie selecteren**
       - Kies welke categorieën en onderliggende categorieën u wilt synchroniseren in Configuration Manager.

      ![Update categorieën selecteren voor synchronisatie in Configuration Manager](./media/4469002-select-categories-for-sync.png)
1. Kies of u de inhoud van de catalogus wilt **bijwerken** . Wanneer u de inhoud faseert, worden alle updates in de geselecteerde categorieën automatisch gedownload naar het software-update punt op het hoogste niveau. Dit betekent dat u niet hoeft te controleren of deze al zijn gedownload voordat u de implementatie uitvoert. U moet alleen inhoud voor updates die u waarschijnlijk gaat implementeren, automatisch in de fase plaatsen om buitensporige band breedte en opslag vereisten te voor komen.

   - **Inhoud niet klaarzetten, alleen synchroniseren voor scannen (aanbevolen)**
     - Down load geen inhoud voor updates in de catalogus van derden
   - **De inhoud voor geselecteerde categorieën automatisch faseren**
     - Kies de update categorieën waarmee automatisch inhoud wordt gedownload.
     - De inhoud voor updates in geselecteerde categorieën wordt gedownload naar de WSUS-inhoudsmap van het hoogste niveau van het software-update punt.
      ![Update categorieën selecteren om inhoud te stage](./media/4469002-stage-content.png)
1. Stel uw **planning** in voor catalogus synchronisatie en voltooi vervolgens de wizard.

 

### <a name="edit-an-existing-subscription"></a>Een bestaand abonnement bewerken

> [!IMPORTANT]
> Deze optie is alleen beschikbaar voor v3 update catalogi van derden, die ondersteuning bieden voor categorieën voor updates. Deze opties zijn uitgeschakeld voor catalogi die niet worden gepubliceerd in de nieuwe v3-indeling.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** . Vouw **software-updates** uit en selecteer het knoop punt **Software-update catalogi van derden** .
1. Klik met de rechter muisknop op de catalogus en selecteer **Eigenschappen**.
1. Kies uw opties op het tabblad **categorieën selecteren** .
   - **Alle update Categorieën synchroniseren** (standaard)
       - Synchroniseert alle updates in de Update catalogus van derden in Configuration Manager.
   -  **Categorieën voor synchronisatie selecteren**
       - Kies welke categorieën en onderliggende categorieën u wilt synchroniseren in Configuration Manager.
1. Kies uw opties voor het tabblad **update-inhoud** van het stadium.
   - **Inhoud niet klaarzetten, alleen synchroniseren voor scannen (aanbevolen)**
     - Down load geen inhoud voor updates in de catalogus van derden
   - **De inhoud voor geselecteerde categorieën automatisch faseren**
     - Kies de update categorieën waarmee automatisch inhoud wordt gedownload.
     - De inhoud voor updates in geselecteerde categorieën wordt gedownload naar de WSUS-inhoudsmap van het hoogste niveau van het software-update punt. 

## <a name="monitoring-progress-of-third-party-software-updates"></a>De voortgang van software-updates van derden bewaken 

Synchronisatie van software-updates van derden wordt afgehandeld door het SMS_ISVUPDATES_SYNCAGENT onderdeel op het standaard software-update punt op het hoogste niveau. U kunt status berichten van dit onderdeel weer geven of meer gedetailleerde statussen bekijken in het SMS_ISVUPDATES_SYNCAGENT. log. Dit logboek bevindt zich op het hoogste niveau van het software-update punt in de map site systeem logs. Dit pad is standaard C:\Program Files\Microsoft Configuration Manager\Logs. Zie [software-updates bewaken](../deploy-use/monitor-software-updates.md) voor meer informatie over het bewaken van het algemene software-update beheer proces 

## <a name="known-issues"></a>Bekende problemen

- De computer waarop de-console wordt uitgevoerd, wordt gebruikt om de updates te downloaden van WSUS en toe te voegen aan het update pakket. Het WSUS-handtekening certificaat moet worden vertrouwd op de computer met de console. Als dat niet het geval is, ziet u mogelijk problemen met de handtekening controle tijdens het downloaden van updates van derden. 
- De synchronisatie service voor software-updates van derden kan geen inhoud publiceren naar updates met meta gegevens die zijn toegevoegd aan WSUS door een andere toepassing, hulp programma of script, zoals SCUP gemaakt. De actie **inhoud van software-update publiceren** van derden mislukt bij deze updates. Als u updates van derden wilt implementeren die door deze functie nog niet worden ondersteund, moet u uw bestaande proces volledig gebruiken om deze updates te implementeren.  
-  Configuration Manager heeft een nieuwe versie voor de indeling van het CAB-bestand in de catalogus. De nieuwe versie bevat de certificaten voor de binaire bestanden van de leverancier. Deze certificaten worden toegevoegd aan het knoop punt **certificaten** onder **beveiliging** in de werk ruimte **beheer** zodra u de catalogus goed keurt en vertrouwt.  
     - U kunt nog steeds de oudere versie van het CAB-bestand voor de catalogus gebruiken zolang de download-URL https is en de updates worden ondertekend. De inhoud kan niet worden gepubliceerd omdat de certificaten voor de binaire bestanden niet aanwezig zijn in het CAB-bestand en al zijn goedgekeurd. U kunt dit probleem omzeilen door het certificaat in het knoop punt **certificaten** te zoeken, de blok kering ervan op te heffen en vervolgens de update opnieuw te publiceren. Als u meerdere updates publiceert die zijn ondertekend met verschillende certificaten, moet u elk certificaat dat wordt gebruikt, deblokkeren.
     - Zie status berichten 11523 en 11524 in de onderstaande status bericht tabel voor meer informatie.
-  Wanneer de synchronisatie service voor software-updates van derden op het software-update punt op het hoogste niveau een proxy server voor Internet toegang vereist, kunnen controles van digitale hand tekeningen mislukken. U kunt dit probleem oplossen door de WinHTTP-proxy-instellingen te configureren op het site systeem. Zie [Netsh Commands for WinHTTP](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731131(v=ws.10))(Engelstalig) voor meer informatie.
- Wanneer u een CMG gebruikt voor de opslag van inhoud, worden de inhoud voor updates van derden niet gedownload naar clients als de instelling **Delta-inhoud downloaden wanneer de beschik bare** [client](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is ingeschakeld. <!--6598587-->

## <a name="status-messages"></a>Statusberichten

| MessageID       | Ernst           | Beschrijving | Mogelijke oorzaak| Mogelijke oplossing
| ------------- |-------------| -----|----|----|
| 11516     | Fout |Kan inhoud niet publiceren voor update-ID omdat de inhoud niet is ondertekend.  Alleen inhoud met geldige hand tekeningen kan worden gepubliceerd.  |Configuration Manager staat niet toe dat niet-ondertekende updates worden gepubliceerd.| Publiceer de update op een andere manier. </br></br>Controleer of er een ondertekende update beschikbaar is van de leverancier.|
| 11523  | Waarschuwing |  De catalogus "X" bevat geen certificaten voor het ondertekenen van inhoud, maar pogingen tot het publiceren van update-inhoud voor updates vanuit deze catalogus zijn mogelijk pas mislukt nadat de certificaten voor het ondertekenen van inhoud zijn toegevoegd en goedgekeurd. | Dit bericht kan optreden wanneer u een catalogus importeert die een oudere versie van de cab-bestands indeling gebruikt.|Neem contact op met de provider van de catalogus om een bijgewerkte catalogus te verkrijgen die de certificaten voor het ondertekenen van inhoud bevat. </br> </br> De certificaten voor de binaire bestanden worden niet opgenomen in het CAB-bestand, zodat de inhoud niet kan worden gepubliceerd. U kunt dit probleem omzeilen door het certificaat in het knoop punt **certificaten** te zoeken, de blok kering ervan op te heffen en vervolgens de update opnieuw te publiceren. Als u meerdere updates publiceert die zijn ondertekend met verschillende certificaten, moet u elk certificaat dat wordt gebruikt, deblokkeren.|
| 11524| Fout  | Kan update-ID niet publiceren vanwege ontbrekende meta gegevens van de update. | De update is mogelijk gesynchroniseerd met WSUS buiten Configuration Manager.| Synchroniseer de update met Configuration Manager voordat u de inhoud probeert te publiceren.  </br> </br>Als een extern hulp programma is gebruikt voor het publiceren van de update als **alleen meta gegevens**, gebruikt u hetzelfde hulp programma voor het publiceren van de update-inhoud.|



## <a name="working-with-third-party-updates-video"></a>Werken met video over updates van derden
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Volgende stap
> [!div class="nextstepaction"]
> [Software-updates implementeren](./deploy-software-updates.md)