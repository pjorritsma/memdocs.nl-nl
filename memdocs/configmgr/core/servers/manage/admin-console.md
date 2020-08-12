---
title: Configuration Manager-console
titleSuffix: Configuration Manager
description: Meer informatie over het navigeren via de Configuration Manager-console.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bcc1f8e93f4fb312b74fd7e5746928182b05710f
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126491"
---
# <a name="how-to-use-the-configuration-manager-console"></a>De Configuration Manager-console gebruiken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Beheerders gebruiken de Configuration Manager-console voor het beheren van de Configuration Manager omgeving. In dit artikel worden de basis principes beschreven van het navigeren door de console.  

## <a name="open-the-console"></a><a name="bkmk_open"></a>Open de-console

De Configuration Manager-console wordt altijd op elke site server geïnstalleerd. U kunt deze ook op andere computers installeren. Zie [de Configuration Manager-console installeren](../deploy/install/install-consoles.md)voor meer informatie.

De eenvoudigste methode om de-console te openen op een Windows 10-computer, klikt u op **Start** en typt u `Configuration Manager console` . Mogelijk hoeft u niet de volledige teken reeks voor Windows te typen om het beste resultaat te vinden.

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

3. Selecteer **Verbinding maken**.  

Vanaf versie 1810 kunt u het minimale verificatie niveau voor beheerders opgeven om toegang te krijgen tot Configuration Manager-sites. Deze functie dwingt beheerders af om zich aan te melden bij Windows met het vereiste niveau. Zie [de SMS-provider plannen](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth)voor meer informatie. <!--1357013-->  

## <a name="navigation"></a>Navigatie

Sommige onderdelen van de console zijn mogelijk niet zichtbaar, afhankelijk van de toegewezen beveiligingsrol. Zie [basis principes van beheer op basis van rollen](../../understand/fundamentals-of-role-based-administration.md)voor meer informatie over rollen.

### <a name="workspaces"></a>Werkruimten

De Configuration Manager-console heeft vier **werk ruimten**:  

- **Activa en naleving**  

- **Software bibliotheek**  

- **Controle**  

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

1. Ga naar **beheer**  >  **beveiligings**  >  **console verbindingen**.
1. Klik met de rechter muisknop op de console verbinding van een gebruiker en selecteer **Start micro soft teams chat**.
    - Als de principal-naam van de gebruiker niet is gevonden voor de geselecteerde beheerder, start u de **Chat functie van micro soft teams** is grijs weer gegeven.
    - Er wordt een fout bericht weer gegeven, inclusief een download koppeling, wanneer micro soft teams niet is geïnstalleerd op het apparaat van waaruit u de-console uitvoert.
    - Als micro soft teams is geïnstalleerd op het apparaat van waaruit u de-console uitvoert, wordt er een chat sessie met de gebruiker geopend.

### <a name="known-issues"></a>Bekende problemen

Het fout bericht dat micro soft-teams niet zijn geïnstalleerd, worden niet weer gegeven als de volgende register sleutel niet bestaat:

Computer \ HKEY_CURRENT_USER \SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

U kunt het probleem omzeilen door de register sleutel hand matig te maken.

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


## <a name="next-steps"></a>Volgende stappen

- [Console meldingen](admin-console-notifications.md)
- [Console tips](admin-console-tips.md)
- [Toegankelijkheidsfuncties](../../understand/accessibility-features.md)
- [Taken reeks editor](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
