---
title: Configuration Manager-console
titleSuffix: Configuration Manager
description: Meer informatie over het navigeren via de Configuration Manager-console.
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 58b66639094a602206114cd75a724504618ad38c
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110029"
---
# <a name="how-to-use-the-configuration-manager-console"></a>De Configuration Manager-console gebruiken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Beheerders gebruiken de Configuration Manager-console voor het beheren van de Configuration Manager omgeving. In dit artikel worden de basis principes beschreven van het navigeren door de console.  

## <a name="open-the-console"></a><a name="bkmk_open"></a>Open de-console

De Configuration Manager-console wordt altijd op elke site server geïnstalleerd. U kunt deze ook op andere computers installeren. Zie [de Configuration Manager-console installeren](../deploy/install/install-consoles.md)voor meer informatie.

De eenvoudigste methode om de-console te openen op een Windows 10- **Start** computer, klikt u `Configuration Manager console`op Start en typt u. Mogelijk hoeft u niet de volledige teken reeks voor Windows te typen om het beste resultaat te vinden.

Als u door het menu Start bladert, zoekt u het pictogram **Configuration Manager-console** in de groep **micro soft Endpoint Manager** .

![Pictogrammen start menu van micro soft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> Het pad van het menu Start is gewijzigd in versie 1910. In versie 1906 en eerder is de mapnaam **System Center**. Wanneer u Configuration Manager bijwerkt naar versie 1910 of hoger, moet u ervoor zorgen dat u de interne documentatie die u onderhoudt, bijwerkt om deze nieuwe locatie op te nemen.

## <a name="connect-to-a-site-server"></a>Verbinding maken met een site server

De console maakt verbinding met de server van de centrale beheer site of van uw primaire site servers. U kunt een Configuration Manager-console niet verbinden met een secundaire site. Tijdens de installatie hebt u de Fully Qualified Domain Name (FQDN) opgegeven van de site server waarmee de-console verbinding maakt.

Gebruik de volgende stappen om verbinding te maken met een andere site server:

1. Selecteer de pijl boven aan het [lint](#ribbon)en kies **verbinding maken met een nieuwe site**.  

    ![De console verbinden met een nieuwe site](media/connect-to-a-new-site.png)  

2. Typ de FQDN-naam van de site server. Als u eerder verbinding hebt gemaakt met de site server, selecteert u de server in de vervolg keuzelijst.  

    ![Het venster site verbinding typt u de FQDN-naam van de site server](media/site-server-fqdn.png)  

3. Selecteer **Verbinden**.  

Vanaf versie 1810 kunt u het minimale verificatie niveau voor beheerders opgeven om toegang te krijgen tot Configuration Manager-sites. Deze functie dwingt beheerders af om zich aan te melden bij Windows met het vereiste niveau. Zie [de SMS-provider plannen](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)voor meer informatie. <!--1357013-->  

## <a name="navigation"></a>Navigatie

Sommige onderdelen van de console zijn mogelijk niet zichtbaar, afhankelijk van de toegewezen beveiligingsrol. Zie [basis principes van beheer op basis van rollen](../../understand/fundamentals-of-role-based-administration.md)voor meer informatie over rollen.

### <a name="workspaces"></a>Workspaces

De Configuration Manager-console heeft vier **werk ruimten**:  

- **Activa en naleving**  

- **Software bibliotheek**  

- **Bewaking**  

- **Beheer**  

![Configuration Manager werk ruimten met context menu](media/configuration-manager-workspaces.png)  

Volg orde van de knoppen voor de werk ruimte wijzigen door de pijl-omlaag te selecteren en de opties van het **Navigatie deel venster** Selecteer een item om **omhoog** of **omlaag**te gaan. Selecteer **opnieuw instellen** om de standaard knop volgorde te herstellen.  

![Venster Opties navigatie deel venster voor het opnieuw ordenen van werk ruimten](media/navigation-pane-options.png)  

Minimaliseer een werkruimte knop door **minder knoppen weer geven**te selecteren. De laatste werk ruimte in de lijst wordt eerst geminimaliseerd. Selecteer een geminimaliseerde knop en kies **meer knoppen weer geven** om de oorspronkelijke grootte van de knop te herstellen.

![Geminimaliseerde werk ruimten in de Configuration Manager-console](media/workspace-buttons.png)  

### <a name="nodes"></a>Knooppunten

Werk ruimten zijn een verzameling **knoop punten**. Een voor beeld van een knoop punt is het knoop punt **Software-Update groepen** in de werk ruimte **software bibliotheek** .

Zodra u zich in het knoop punt bevindt, kunt u de pijl selecteren om het navigatie deel venster te minimaliseren.  

![Voorbeeld knooppunt en markeer pijl minimaliseren](media/software-update-groups-node.png)  

Gebruik de **navigatie balk** om door de console te navigeren wanneer u het navigatie deel venster minimaliseert.  

![Geminimaliseerd navigatie deel venster Configuration Manager](media/minimized-navigation-pane.png)  

In de-console worden knoop punten soms ingedeeld in mappen. Wanneer u de map selecteert, wordt meestal een **Navigatie-index** of een **dash board**weer gegeven.  

![Navigatie-index Configuration Manager software-updates](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Vaandel

Het lint bevindt zich boven aan de Configuration Manager-console. Het lint kan meer dan één tabblad hebben en kan worden geminimaliseerd met behulp van de pijl aan de rechter kant. De knoppen op het lint worden gewijzigd op basis van het knoop punt. De meeste knoppen in het lint zijn ook beschikbaar in context menu's.  

![Voorbeeld lint, meerdere tabbladen markeren en pijl minimaliseren](media/ribbon.png)

### <a name="details-pane"></a>Detail venster

U kunt aanvullende informatie over items krijgen door het deel venster Details te bekijken. Het deel venster Details kan een of meer tabbladen bevatten. De tabbladen variëren, afhankelijk van het knoop punt.  

![Configuration Manager deel venster met voorbeeld Details](media/details-pane.png)

### <a name="columns"></a>Kolommen

U kunt kolommen toevoegen, verwijderen, opnieuw rangschikken en het formaat ervan wijzigen. Met deze acties kunt u de gewenste gegevens weer geven. Beschik bare kolommen kunnen variëren, afhankelijk van het knoop punt. Als u een kolom wilt toevoegen aan of verwijderen uit de weer gave, klikt u met de rechter muisknop op een bestaande kolomkop en selecteert u een item. U kunt de volg orde van de kolommen wijzigen door de kolomkop naar wens te slepen.  

![Kolom toevoegen door Configuration Manager](media/add-columns.png)  

Onder in het context menu van de kolom kunt u sorteren of groeperen op een kolom. Daarnaast kunt u sorteren op een kolom door de koptekst ervan te selecteren.  

![Groeperen op kolom Configuration Manager](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a>Vergren deling voor het bewerken van objecten claimen

<!--4786915-->

Als de Configuration Manager-console niet meer reageert, kunt u de vergren deling vergren delen om verdere wijzigingen aan te brengen tot de vergrendeling na 30 minuten verloopt. Deze vergren deling maakt deel uit van de Configuration Manager SEDO (geserialiseerd editing of Distributed Objects). Zie [Configuration Manager Sedo](../../../develop/core/understand/sedo.md)voor meer informatie.

Vanaf de [huidige branch-versie 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences)kunt u de vergren deling van een taken reeks wissen. Vanaf versie 1910 kunt u de vergren deling van een object in de Configuration Manager-console wissen.

Deze actie is alleen van toepassing op uw gebruikers account met de vergren deling en op hetzelfde apparaat waarvan de site de vergren deling heeft gekregen. Wanneer u probeert een vergrendeld object te openen, kunt u nu de **wijzigingen negeren**en door gaan met het bewerken van het object. Deze wijzigingen zijn toch verloren gegaan wanneer de vergren deling is verlopen.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a>Recent verbonden consoles weer geven

<!--3699367-->
Vanaf versie 1902 kunt u de meest recente verbindingen voor de Configuration Manager-console bekijken. De weer gave bevat actieve verbindingen en de verbindingen die recent zijn verbonden. U ziet altijd uw huidige console verbinding in de lijst en u ziet alleen verbindingen van de Configuration Manager-console. Power shell of andere op SDK gebaseerde verbindingen met de SMS-provider worden niet weer geven. De site verwijdert instanties uit de lijst die ouder zijn dan 30 dagen.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a>Vereisten voor het weer geven van verbonden consoles

- Uw account heeft de machtiging **lezen** nodig voor het object **SMS_Site**

- De beheer service configureren REST API. Zie [Wat is de beheer service?](../../../develop/adminservice/overview.md) voor meer informatie.

### <a name="view-connected-consoles"></a>Verbonden consoles weer geven

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** .  

2. Vouw **beveiliging** uit en selecteer het knoop punt **console verbindingen** .  

3. Bekijk de recente verbindingen met de volgende eigenschappen:  

    - Gebruikersnaam
    - Computer naam
    - Code van verbonden site
    - Console versie
    - Tijdstip laatste verbinding: wanneer de gebruiker de console voor het laatst heeft *geopend*
    - Vanaf versie 1910 is de **laatste console-heartbeat** -kolom vervangen door de laatste **verbonden tijd** kolom. <!--4923997-->
       - Een geopende console op de voor grond stuurt elke 10 minuten een heartbeat.

![Configuration Manager-console verbindingen weer geven](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a>Micro soft teams chat starten vanuit console verbindingen
<!--4923997-->
*(Geïntroduceerd in versie 1910)*

Vanaf versie 1910 kunt u andere beheerders van het knoop punt van de **console verbinding** met micro soft-Teams bericht Configuration Manager. Wanneer u ervoor kiest om **micro soft teams-chat te starten** met een beheerder, worden micro soft-teams gestart en wordt een chat sessie geopend met de gebruiker.

### <a name="prerequisites"></a>Vereisten

- Voor het starten van een chat met een beheerder moet het account waarmee u wilt chatten, zijn gedetecteerd met [Azure AD of AD-gebruikers detectie](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Micro soft-teams geïnstalleerd op het apparaat van waaruit u de-console uitvoert.
opmerking
- Alle [vereisten voor het weer geven van verbonden consoles](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Micro soft teams chat starten

1. Ga naar **beheer** > **beveiligings** > **console verbindingen**.
1. Klik met de rechter muisknop op de console verbinding van een gebruiker en selecteer **Start micro soft teams chat**.
    - Als de principal-naam van de gebruiker niet is gevonden voor de geselecteerde beheerder, start u de **Chat functie van micro soft teams** is grijs weer gegeven.
    - Er wordt een fout bericht weer gegeven, inclusief een download koppeling, wanneer micro soft teams niet is geïnstalleerd op het apparaat van waaruit u de-console uitvoert.
    - Als micro soft teams is geïnstalleerd op het apparaat van waaruit u de-console uitvoert, wordt er een chat sessie met de gebruiker geopend.

### <a name="known-issues"></a>Bekende problemen

Het fout bericht dat micro soft-teams niet zijn geïnstalleerd, worden niet weer gegeven als de volgende register sleutel niet bestaat:

Computer \ HKEY_CURRENT_USER \SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

U kunt het probleem omzeilen door de register sleutel hand matig te maken.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a>Meldingen over Configuration Manager-console

<!--3556016, fka 1318035-->
Vanaf Configuration Manager versie 1902 geeft de console u een melding over de volgende gebeurtenissen:

- Wanneer er een update beschikbaar is voor Configuration Manager zichzelf
- Wanneer er levens cyclus-en onderhouds gebeurtenissen optreden in de omgeving

Deze melding is een balk boven aan het console venster onder het lint. De vorige ervaring wordt vervangen wanneer Configuration Manager updates beschikbaar zijn. In deze meldingen in de console worden nog steeds essentiële gegevens weer gegeven, maar uw werk in de console wordt niet verstoord. U kunt geen kritieke meldingen negeren. In de-console worden alle meldingen in een nieuw systeemvak van de titel balk weer gegeven.

![Meldings balk en vlag in console](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Een site configureren voor het weer geven van niet-kritieke meldingen

U kunt elke site zo configureren dat niet-kritieke meldingen worden weer gegeven in de eigenschappen van de site.

1. Vouw **site configuratie**uit in de werk ruimte **beheer** en selecteer vervolgens het knoop punt **sites** .
1. Selecteer de site die u wilt configureren voor niet-kritieke meldingen.
1. Selecteer **Eigenschappen**in het lint.
1. Selecteer op het tabblad **waarschuwingen** de optie om **console meldingen in te scha kelen voor niet-kritieke status wijzigingen van de site**.
   - Als u deze instelling inschakelt, zien alle console gebruikers essentiële, waarschuwings-en informatie meldingen. Deze instelling is standaard ingeschakeld.  
   - Als u deze instelling uitschakelt, bekijken console gebruikers alleen kritieke meldingen.  

De meeste console meldingen zijn per sessie. Query's worden geëvalueerd wanneer een gebruiker de console start. Start de console opnieuw om de wijzigingen in de meldingen te bekijken. Als een gebruiker een niet-kritieke melding heeft gesloten, wordt deze opnieuw weer gemeld wanneer de console opnieuw wordt opgestart als deze nog steeds van toepassing is.

De volgende meldingen worden elke vijf minuten opnieuw geëvalueerd:

- Site bevindt zich in onderhouds modus  
- Site bevindt zich in de herstel modus  
- De site bevindt zich in de upgrade modus  

Meldingen volgen de machtigingen voor beheer op basis van rollen. Als een gebruiker bijvoorbeeld geen machtigingen heeft om Configuration Manager updates te zien, worden deze meldingen niet weer geven.

Sommige meldingen hebben een gerelateerde actie. Als de-console versie bijvoorbeeld niet overeenkomt met de versie van de-site, selecteert u **de nieuwe console versie installeren**. Met deze actie wordt het installatie programma van de-console gestart.

De volgende meldingen zijn het meest van toepassing op de Technical Preview-vertakking:  

- De evaluatie versie ligt binnen 30 dagen na verloop van tijd (waarschuwing): de huidige datum valt binnen 30 dagen na de verval datum van de evaluatie versie  
- De evaluatie versie is verlopen (kritiek): de huidige datum valt na de verval datum van de evaluatie versie  
- Niet-overeenkomende console versies (kritiek): de versie van de console komt niet overeen met de site versie  
- Site-upgrade is beschikbaar (waarschuwing): er is een nieuw update pakket beschikbaar  

Zie het bestand **SmsAdminUI. log** op de-console computer voor meer informatie en hulp bij het oplossen van problemen. Dit logboek bestand bevindt zich standaard op het volgende pad `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`:.


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a>Dash board documentatie in de console

<!--3556019 FKA 1357546-->
Vanaf Configuration Manager versie 1902 is er een **documentatie** knooppunt in de nieuwe werk ruimte van de **Community** . Dit knoop punt bevat actuele informatie over Configuration Manager documentatie en ondersteunings artikelen. De sectie bevat de volgende secties:  

### <a name="product-documentation-library"></a>Bibliotheek met product documentatie

- **Aanbevolen**: een hand matig gecuratore lijst met belang rijke artikelen.
- **Trending**: de populairste artikelen van de afgelopen maand.
- **Recent bijgewerkt**: artikelen die in de afgelopen maand zijn gereviseerd.

### <a name="support-articles"></a>Ondersteuningsartikelen

- **Problemen oplossen met artikelen**: begeleide scenario's voor hulp bij het oplossen van problemen Configuration Manager onderdelen en functies.
- **Nieuwe en bijgewerkte artikel ondersteuning**: artikelen die in de afgelopen twee maanden nieuw of bijgewerkt zijn.

### <a name="troubleshooting-connection-errors"></a>Verbindings fouten oplossen
Het **documentatie** knooppunt heeft geen expliciete proxy configuratie. Het maakt gebruik van een door het besturings systeem gedefinieerde proxy in het onderdeel **Internet opties** van het configuratie scherm. Vernieuw het **documentatie** knooppunt om het opnieuw te proberen na een verbindings fout.


## <a name="command-line-options"></a>Opdrachtregelopties

De Configuration Manager-console heeft de volgende opdracht regel opties:

|Optie|Beschrijving|  
|------------|-----------------|  
|`/sms:debugview=1`|Een DebugView is opgenomen in alle ResultViews die een weer gave opgeven. DebugView toont onbewerkte eigenschappen (namen en waarden).|  
|`/sms:NamespaceView=1`|Geeft de naam ruimte weergave weer in de-console.|  
|`/sms:ResetSettings`|De-console negeert de door de gebruiker blijvende verbinding en weer gave status. De venster grootte wordt niet opnieuw ingesteld.|  
|`/sms:IgnoreExtensions`|Hiermee schakelt u alle Configuration Manager extensies uit.|  
|`/sms:NoRestore`|De vorige permanente navigatie van knoop punten wordt door de console genegeerd.|  


## <a name="tips"></a>Tips

### <a name="general"></a>Algemeen

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a>Verbeteringen in zoeken in de console
<!--4640570-->
*(Geïntroduceerd in versie 1910)*

- U kunt de zoek optie **alle submappen** gebruiken van de knoop punten **Stuur programmapakketten** en **query's** .<!--2841181,5424892--> Vanaf versie 2002 gebruikt u deze optie ook van de knoop punten **configuratie-items** en **configuratie basislijnen** .<!--5891241-->

- Wanneer een zoek opdracht meer dan 1.000 resultaten retourneert, selecteert u de knop **OK** op de mededelingen balk om meer resultaten weer te geven.<!--4640570-->

    ![Scherm afbeelding van de kennisgevings balk voor te veel Zoek resultaten](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > De standaard limiet voor de zoek resultaten is 1.000. U kunt deze standaard waarde wijzigen. Ga in de Configuration Manager-console naar het tabblad **zoeken** van het lint. Selecteer in de groep **Opties** de optie **Zoek instellingen**. Wijzig de waarde van de **Zoek resultaten** . Een groter aantal Zoek resultaten kan langer duren om weer te geven.
    >
    > Standaard is de maximum limiet van 100.000. Als u deze limiet wilt wijzigen, stelt u de DWORD-waarde **QueryResultCountMaximum** in de volgende register sleutel in:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > De instelling in de console komt overeen met de **QueryResultCountLimit** -waarde in dezelfde sleutel. Een beheerder kan deze waarden in de HKLM-component configureren voor alle gebruikers van het apparaat. De HKCU-waarde overschrijft de HKLM-instelling.

#### <a name="role-based-administration-for-folders"></a>Beheer op basis van rollen voor mappen
<!--3600867-->
*(Geïntroduceerd in versie 1906)*

U kunt beveiligingsbereiken instellen voor mappen. Als u toegang hebt tot een object in de map, maar u geen toegang hebt tot de map, kunt u het object niet zien. En als u toegang hebt tot een map, maar geen object daarin, ziet u dat object niet. Klik met de rechter muisknop op een map, kies **Beveiligingsbereiken instellen**en kies vervolgens de beveiligingsbereiken die u wilt Toep assen.

#### <a name="views-sort-by-integer-values"></a>Weer gaven worden gesorteerd op gehele waarden

*(Geïntroduceerd in versie 1902)*

We hebben verbeteringen aangebracht in de manier waarop verschillende weer gaven gegevens sorteren. Bijvoorbeeld, in het knoop punt **implementaties** van de werk ruimte **bewaking** , de volgende kolommen worden nu gesorteerd als getallen in plaats van teken reeks waarden:  

- Aantal fouten
- Nummer wordt uitgevoerd
- Aantal andere
- Aantal geslaagde pogingen
- Onbekend nummer  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>De waarschuwing voor een groot aantal resultaten verplaatsen

*(Geïntroduceerd in versie 1902)*

Wanneer u een knoop punt in de-console selecteert dat meer dan 1.000 resultaten retourneert, wordt in Configuration Manager de volgende waarschuwing weer gegeven:

> Configuration Manager heeft een groot aantal resultaten geretourneerd. U kunt de resultaten verfijnen met behulp van zoeken. Of klik hier om Maxi maal 100000 resultaten weer te geven.

Er is nu nog lege ruimte tussen deze waarschuwing en het zoek veld. Met deze stap wordt voor komen dat u per ongeluk de waarschuwing selecteert om meer resultaten weer te geven.

#### <a name="send-feedback"></a>Feedback verzenden

*(Geïntroduceerd in versie 1806)*
<!--1357542-->

Feedback over het product verzenden vanaf de-console.  

- **Glim lach verzenden**: feedback verzenden over wat u leuk vindt  

- **Frons verzenden**: feedback verzenden over wat u niet bevalt  

- **Een suggestie verzenden**: gaat u naar UserVoice om uw idee te delen  

Zie [product feedback](../../understand/find-help.md#BKMK_1806Feedback)voor meer informatie.


### <a name="assets-and-compliance-workspace"></a>Werk ruimte activa en naleving

#### <a name="real-time-actions-from-device-lists"></a>Acties in realtime van apparaten lijsten
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Er zijn verschillende manieren om een lijst met apparaten weer te geven onder het knoop punt **apparaten** in de werk ruimte **activa en naleving** .

- Selecteer in de werk ruimte **activa en naleving** het knoop punt **device Collections** . Selecteer een verzameling apparaten en kies de actie om **leden weer te geven**. Met deze actie wordt een subknooppunt van het knoop punt **apparaten** geopend met een lijst met apparaten voor die verzameling.  

  - Wanneer u het subknooppunt verzameling selecteert, kunt u nu **CMPivot** starten vanuit de verzamelings groep van het lint.  

- Selecteer in de werk ruimte **bewaking** het knoop punt **implementaties** . Selecteer een implementatie en kies de actie **status weer geven** in het lint. Dubbel klik in het deel venster implementatie status op het totale aantal assets dat u wilt inzoomen op een apparaten lijst.  

  - Wanneer u een apparaat in deze lijst selecteert, kunt u nu **CMPivot** starten en **scripts uitvoeren** vanuit de apparaatgroep van het lint.  


#### <a name="collections-tab-in-devices-node"></a>Het tabblad verzamelingen in het knoop punt apparaten
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Ga in de werk ruimte **activa en naleving** naar het knoop punt **apparaten** en selecteer een apparaat. Ga in het detail venster naar het tabblad nieuwe **verzamelingen** . Dit tabblad bevat de verzamelingen die dit apparaat bevatten. 

> [!Note]  
> - Dit tabblad is momenteel niet beschikbaar vanuit een subknooppunt apparaten onder het knoop punt **apparaats verzameling** . Wanneer u bijvoorbeeld de optie selecteert om leden op een verzameling **weer te geven** .
> - Dit tabblad wordt mogelijk niet zoals verwacht ingevuld voor sommige gebruikers. Voor een overzicht van de volledige lijst met verzamelingen waarvan een apparaat deel uitmaakt, moet u de beveiligingsrol **volledige beheerder** hebben. Dit is een bekend probleem. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>SMBIOS GUID-kolom toevoegen aan de knoop punten apparaat-en apparaat-verzameling

*(Geïntroduceerd in versie 1906)*

<!--4526580-->
In zowel de **apparaten** als de **apparaat verzameling** knoop punten kunt u nu een nieuwe kolom toevoegen voor de **SMBIOS-GUID**. Deze waarde is hetzelfde als de **BIOS GUID** -eigenschap van de systeem bron klasse. Het is een unieke id voor de hardware van het apparaat.

#### <a name="search-device-views-using-mac-address"></a>Apparaatbeheer doorzoeken met MAC-adres

<!--3600878-->
*(Geïntroduceerd in versie 1902)*

U kunt zoeken naar een MAC-adres in een apparaat weergave van de Configuration Manager-console. Deze eigenschap is handig voor beheerders van besturingssysteem implementaties bij het oplossen van problemen met PXE-implementaties. Wanneer u een lijst met apparaten bekijkt, voegt u de kolom **MAC-adres** toe aan de weer gave. Gebruik het zoek veld om de **MAC-adres** zoek criteria toe te voegen.

#### <a name="view-users-for-a-device"></a>Gebruikers voor een apparaat weer geven

Vanaf versie 1806 zijn de volgende kolommen beschikbaar in het knoop punt **apparaten** :  

- **Primaire gebruiker (s)** <!--1357280-->  

- **Gebruiker die momenteel is aangemeld** <!--1358202-->  

    > [!NOTE]  
    > Voor het weer geven van de gebruiker die momenteel is aangemeld, is gebruikers [affiniteit met apparaat](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) [detectie](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) en gebruiker vereist.  

Zie [Columns (kolommen](#columns)) voor meer informatie over het weer geven van een niet-standaard kolom.

#### <a name="improvement-to-device-search-performance"></a>Verbetering van de prestaties van het zoeken naar apparaten

<!-- 3614690 -->
Vanaf versie 1806 wordt het tref woord niet doorzocht op alle object eigenschappen bij het zoeken in een apparaat. Wanneer u niet specifiek weet wat u moet zoeken, wordt gezocht in de volgende vier eigenschappen:

- Naam
- Primaire gebruiker (s)
- Gebruiker die momenteel is aangemeld
- Gebruikers naam van recentste aanmelding

Dit gedrag verbetert de tijd die nodig is om op naam te zoeken, met name in een grote omgeving. Aangepaste zoek acties op specifieke criteria worden niet beïnvloed door deze wijziging.


### <a name="software-library-workspace"></a>Werk ruimte software bibliotheek

#### <a name="order-by-program-name-in-task-sequence"></a>Order by-programma naam in taken reeks
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer het knoop punt **taken reeksen** . Bewerk een taken reeks en selecteer of Voeg de stap [pakket installeren](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) toe. Als een pakket meer dan één programma heeft, worden de Program ma's nu alfabetisch gesorteerd met de vervolg keuzelijst.

#### <a name="task-sequences-tab-in-applications-node"></a>Het tabblad taken reeksen in het knoop punt toepassingen
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

In de werk ruimte **software bibliotheek** vouwt u **toepassings beheer**uit, gaat u naar het knoop punt **toepassingen** en selecteert u een toepassing. Schakel in het detail venster over naar het tabblad nieuwe **taken reeksen** . Dit tabblad bevat de taken reeksen die verwijzen naar deze toepassing.

#### <a name="drill-through-required-updates"></a>Bekijk de vereiste updates
<!--4224414-->
*(Geïntroduceerd in versie 1906)*

1. Ga naar een van de volgende locaties in de Configuration Manager-console:

   - **Software Library** > **software werkt** > **alle software-updates** bij
   - **Software bibliotheek** > **Windows 10 onderhoud** > **alle Windows 10-updates**
   - **Software bibliotheek** > **Office 365 client management** > **Office 365 updates**

1. Selecteer een update die vereist is voor ten minste één apparaat.
1. Ga naar het tabblad **samen vatting** en zoek het cirkel diagram onder **Statistieken**.
1. Selecteer de **weer gave vereiste** Hyper link naast het cirkel diagram om in te zoomen op de apparaten lijst.
1. Met deze actie gaat u naar een tijdelijk knoop punt onder **apparaten** waar u de apparaten kunt zien waarvoor de update is vereist. U kunt ook acties uitvoeren voor het knoop punt, zoals het maken van een nieuwe verzameling in de lijst.

> [!NOTE]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds verwijzingen naar de oude naam in de Configuration Manager-console en de ondersteunende documentatie terwijl de-console wordt bijgewerkt.

#### <a name="maximize-the-browse-registry-window"></a>Het Blader register venster maximaliseren

<!--3594151 includes all MMS 1902 console changes-->
*(Geïntroduceerd in versie 1902)*

1. Vouw in de werk ruimte **software bibliotheek** de optie **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .
1. Selecteer een toepassing die een implementatie type heeft met een detectie methode. Bijvoorbeeld een Windows Installer-detectie methode.
1. Ga in het detail venster naar het tabblad **implementatie typen** .
1. Open de eigenschappen van een implementatie type en schakel over naar het tabblad **detectie methode** . Selecteer **component toevoegen**.
1. Wijzig het **instellings type** in **REGI ster** en selecteer **Bladeren** om het venster **Bladeren in REGI ster** te openen. U kunt dit venster nu maximaliseren.  

#### <a name="edit-a-task-sequence-by-default"></a>Standaard een taken reeks bewerken

*(Geïntroduceerd in versie 1902)*

Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer het knoop punt **taken reeksen** . **Bewerken** is nu de standaard actie bij het openen van een taken reeks. Voorheen was de standaard actie **Eigenschappen**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Ga naar de verzameling vanuit een toepassings implementatie

*(Geïntroduceerd in versie 1902)*

1. Vouw in de werk ruimte **software bibliotheek** de optie **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .
1. Selecteer een toepassing. Ga in het detail venster naar het tabblad **implementaties** .
1. Selecteer een implementatie en kies vervolgens de optie nieuwe **verzameling** in het lint op het tabblad implementatie. Met deze actie wordt de weer gave overgeschakeld naar de verzameling die het doel van de implementatie is.
   - Deze actie is ook beschikbaar via het context menu met de rechter muisknop op de implementatie in deze weer gave.


### <a name="monitoring-workspace"></a>Bewakings werkruimte

#### <a name="correct-names-for-client-operations"></a>Juiste namen voor client bewerkingen
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Selecteer **client bewerkingen**in de werk ruimte **bewaking** . De bewerking om **over te scha kelen naar het volgende software-update punt** heeft nu de juiste naam.

#### <a name="show-collection-name-for-scripts"></a>De naam van de verzameling voor scripts weer geven
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Selecteer in de werk ruimte **bewaking** het knoop punt **script status** . De naam van de **verzameling** wordt nu naast de id weer gegeven.

#### <a name="remove-content-from-monitoring-status"></a>Inhoud verwijderen uit bewakings status

*(Geïntroduceerd in versie 1902)*

1. Vouw in **Monitoring** de werk ruimte bewaking **distributie status**uit en selecteer **inhouds status**.
1. Selecteer een item in de lijst en kies de optie **weergave status** in het lint.
1. Klik in het deel venster activum gegevens met de rechter muisknop op een distributie punt en selecteer de nieuwe optie **verwijderen**. Deze actie verwijdert deze inhoud van het geselecteerde distributie punt.

#### <a name="copy-details-in-monitoring-views"></a>Details kopiëren in controle weergaven

*(Geïntroduceerd in versie 1806)*
<!--1357856-->
Gegevens uit het deel venster **activum gegevens** kopiëren voor de volgende bewakings knooppunten:  

- **Status van inhouds distributie**  

- **Implementatie status**  

![Status weergave van de implementatie, Details van activum kopiëren](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Werk ruimte beheer

<!--4223683-->
Vanaf versie 1906 kunt u enkele knoop punten inschakelen onder het knoop punt **beveiliging** om de beheer service te gebruiken. Met deze wijziging kan de console communiceren met de SMS-provider via HTTPS in plaats van via WMI. Zie [de beheer service instellen](../../../develop/adminservice/set-up.md#bkmk_console)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Toegankelijkheidsfuncties](../../understand/accessibility-features.md)

[Taken reeks editor](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
