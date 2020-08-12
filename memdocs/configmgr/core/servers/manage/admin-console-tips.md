---
title: Wijzigingen en tips van Configuration Manager-console
titleSuffix: Configuration Manager
description: Meer informatie over wijzigingen in de Configuration Manager-console en tips voor het gebruik ervan.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7f46c283bd533d67387ab0abac35e7625438addc
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129646"
---
# <a name="configuration-manager-console-changes-and-tips"></a>Wijzigingen en tips van Configuration Manager-console

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik de onderstaande informatie om te ontdekken over wijzigingen in de Configuration Manager-console en tips voor het gebruik van de-console:

## <a name="general-tips"></a>Algemene tips

### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a>Verbeteringen in zoeken in de console
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

### <a name="role-based-administration-for-folders"></a>Beheer op basis van rollen voor mappen
<!--3600867-->
*(Geïntroduceerd in versie 1906)*

U kunt beveiligingsbereiken instellen voor mappen. Als u toegang hebt tot een object in de map, maar u geen toegang hebt tot de map, kunt u het object niet zien. En als u toegang hebt tot een map, maar geen object daarin, ziet u dat object niet. Klik met de rechter muisknop op een map, kies **Beveiligingsbereiken instellen**en kies vervolgens de beveiligingsbereiken die u wilt Toep assen.

### <a name="views-sort-by-integer-values"></a>Weer gaven worden gesorteerd op gehele waarden

*(Geïntroduceerd in versie 1902)*

We hebben verbeteringen aangebracht in de manier waarop verschillende weer gaven gegevens sorteren. Bijvoorbeeld, in het knoop punt **implementaties** van de werk ruimte **bewaking** , de volgende kolommen worden nu gesorteerd als getallen in plaats van teken reeks waarden:  

- Aantal fouten
- Nummer wordt uitgevoerd
- Aantal andere
- Aantal geslaagde pogingen
- Onbekend nummer  

### <a name="move-the-warning-for-a-large-number-of-results"></a>De waarschuwing voor een groot aantal resultaten verplaatsen

*(Geïntroduceerd in versie 1902)*

Wanneer u een knoop punt in de-console selecteert dat meer dan 1.000 resultaten retourneert, wordt in Configuration Manager de volgende waarschuwing weer gegeven:

> Configuration Manager heeft een groot aantal resultaten geretourneerd. U kunt de resultaten verfijnen met behulp van zoeken. Of klik hier om Maxi maal 100000 resultaten weer te geven.

Er is nu nog lege ruimte tussen deze waarschuwing en het zoek veld. Met deze stap wordt voor komen dat u per ongeluk de waarschuwing selecteert om meer resultaten weer te geven.

### <a name="send-feedback"></a>Feedback verzenden

*(Geïntroduceerd in versie 1806)*
<!--1357542-->

Feedback over het product verzenden vanaf de-console.  

- **Glim lach verzenden**: feedback verzenden over wat u leuk vindt  

- **Frons verzenden**: feedback verzenden over wat u niet bevalt  

- **Een suggestie verzenden**: gaat u naar UserVoice om uw idee te delen  

Zie [product feedback](../../understand/find-help.md#BKMK_1806Feedback)voor meer informatie.


## <a name="assets-and-compliance-workspace"></a>Werk ruimte activa en naleving

### <a name="real-time-actions-from-device-lists"></a>Acties in realtime van apparaten lijsten
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Er zijn verschillende manieren om een lijst met apparaten weer te geven onder het knoop punt **apparaten** in de werk ruimte **activa en naleving** .

- Selecteer in de werk ruimte **activa en naleving** het knoop punt **device Collections** . Selecteer een verzameling apparaten en kies de actie om **leden weer te geven**. Met deze actie wordt een subknooppunt van het knoop punt **apparaten** geopend met een lijst met apparaten voor die verzameling.  

  - Wanneer u het subknooppunt verzameling selecteert, kunt u nu **CMPivot** starten vanuit de verzamelings groep van het lint.  

- Selecteer in de werk ruimte **bewaking** het knoop punt **implementaties** . Selecteer een implementatie en kies de actie **status weer geven** in het lint. Dubbel klik in het deel venster implementatie status op het totale aantal assets dat u wilt inzoomen op een apparaten lijst.  

  - Wanneer u een apparaat in deze lijst selecteert, kunt u nu **CMPivot** starten en **scripts uitvoeren** vanuit de apparaatgroep van het lint.  


### <a name="collections-tab-in-devices-node"></a>Het tabblad verzamelingen in het knoop punt apparaten
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Ga in de werk ruimte **activa en naleving** naar het knoop punt **apparaten** en selecteer een apparaat. Ga in het detail venster naar het tabblad nieuwe **verzamelingen** . Dit tabblad bevat de verzamelingen die dit apparaat bevatten. 

> [!Note]  
> - Dit tabblad is momenteel niet beschikbaar vanuit een subknooppunt apparaten onder het knoop punt **apparaats verzameling** . Wanneer u bijvoorbeeld de optie selecteert om leden op een verzameling **weer te geven** .
> - Dit tabblad wordt mogelijk niet zoals verwacht ingevuld voor sommige gebruikers. Voor een overzicht van de volledige lijst met verzamelingen waarvan een apparaat deel uitmaakt, moet u de beveiligingsrol **volledige beheerder** hebben. Dit is een bekend probleem. <!--5107309--> <!--5107309-->


### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>SMBIOS GUID-kolom toevoegen aan de knoop punten apparaat-en apparaat-verzameling

*(Geïntroduceerd in versie 1906)*

<!--4526580-->
In zowel de **apparaten** als de **apparaat verzameling** knoop punten kunt u nu een nieuwe kolom toevoegen voor de **SMBIOS-GUID**. Deze waarde is hetzelfde als de **BIOS GUID** -eigenschap van de systeem bron klasse. Het is een unieke id voor de hardware van het apparaat.

### <a name="search-device-views-using-mac-address"></a>Apparaatbeheer doorzoeken met MAC-adres

<!--3600878-->
*(Geïntroduceerd in versie 1902)*

U kunt zoeken naar een MAC-adres in een apparaat weergave van de Configuration Manager-console. Deze eigenschap is handig voor beheerders van besturingssysteem implementaties bij het oplossen van problemen met PXE-implementaties. Wanneer u een lijst met apparaten bekijkt, voegt u de kolom **MAC-adres** toe aan de weer gave. Gebruik het zoek veld om de **MAC-adres** zoek criteria toe te voegen.

### <a name="view-users-for-a-device"></a>Gebruikers voor een apparaat weer geven

Vanaf versie 1806 zijn de volgende kolommen beschikbaar in het knoop punt **apparaten** :  

- **Primaire gebruiker (s)** <!--1357280-->  

- **Gebruiker die momenteel is aangemeld** <!--1358202-->  

    > [!NOTE]  
    > Voor het weer geven van de gebruiker die momenteel is aangemeld, is gebruikers [affiniteit met apparaat](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md) [detectie](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) en gebruiker vereist.  

Zie [How to use the admin console](admin-console.md#columns)(Engelstalig) voor meer informatie over het weer geven van een niet-standaard kolom.

### <a name="improvement-to-device-search-performance"></a>Verbetering van de prestaties van het zoeken naar apparaten

<!-- 3614690 -->
Vanaf versie 1806 wordt het tref woord niet doorzocht op alle object eigenschappen bij het zoeken in een apparaat. Wanneer u niet specifiek weet wat u moet zoeken, wordt gezocht in de volgende vier eigenschappen:

- Naam
- Primaire gebruiker (s)
- Gebruiker die momenteel is aangemeld
- Gebruikers naam van recentste aanmelding

Dit gedrag verbetert de tijd die nodig is om op naam te zoeken, met name in een grote omgeving. Aangepaste zoek acties op specifieke criteria worden niet beïnvloed door deze wijziging.


## <a name="software-library-workspace"></a>Werk ruimte software bibliotheek

### <a name="order-by-program-name-in-task-sequence"></a>Order by-programma naam in taken reeks
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer het knoop punt **taken reeksen** . Bewerk een taken reeks en selecteer of Voeg de stap [pakket installeren](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) toe. Als een pakket meer dan één programma heeft, worden de Program ma's nu alfabetisch gesorteerd met de vervolg keuzelijst.

### <a name="task-sequences-tab-in-applications-node"></a>Het tabblad taken reeksen in het knoop punt toepassingen
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

In de werk ruimte **software bibliotheek** vouwt u **toepassings beheer**uit, gaat u naar het knoop punt **toepassingen** en selecteert u een toepassing. Schakel in het detail venster over naar het tabblad nieuwe **taken reeksen** . Dit tabblad bevat de taken reeksen die verwijzen naar deze toepassing.

### <a name="drill-through-required-updates"></a>Bekijk de vereiste updates
<!--4224414-->
*(Geïntroduceerd in versie 1906)*

1. Ga naar een van de volgende locaties in de Configuration Manager-console:

   - **Software bibliotheek**  >  **Software-updates**  >  **Alle software-updates**
   - **Software bibliotheek**  >  Onderhoud van Windows **10**  >  **Alle Windows 10-updates**
   - **Software bibliotheek**  >  **Office 365-client beheer**  >  **Office 365-updates**

1. Selecteer een update die vereist is voor ten minste één apparaat.
1. Ga naar het tabblad **samen vatting** en zoek het cirkel diagram onder **Statistieken**.
1. Selecteer de **weer gave vereiste** Hyper link naast het cirkel diagram om in te zoomen op de apparaten lijst.
1. Met deze actie gaat u naar een tijdelijk knoop punt onder **apparaten** waar u de apparaten kunt zien waarvoor de update is vereist. U kunt ook acties uitvoeren voor het knoop punt, zoals het maken van een nieuwe verzameling in de lijst.

> [!NOTE]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds verwijzingen naar de oude naam in de Configuration Manager-console en de ondersteunende documentatie terwijl de-console wordt bijgewerkt.

### <a name="maximize-the-browse-registry-window"></a>Het Blader register venster maximaliseren

<!--3594151 includes all MMS 1902 console changes-->
*(Geïntroduceerd in versie 1902)*

1. Vouw in de werk ruimte **software bibliotheek** de optie **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .
1. Selecteer een toepassing die een implementatie type heeft met een detectie methode. Bijvoorbeeld een Windows Installer-detectie methode.
1. Ga in het detail venster naar het tabblad **implementatie typen** .
1. Open de eigenschappen van een implementatie type en schakel over naar het tabblad **detectie methode** . Selecteer **component toevoegen**.
1. Wijzig het **instellings type** in **REGI ster** en selecteer **Bladeren** om het venster **Bladeren in REGI ster** te openen. U kunt dit venster nu maximaliseren.  

### <a name="edit-a-task-sequence-by-default"></a>Standaard een taken reeks bewerken

*(Geïntroduceerd in versie 1902)*

Vouw in de werk ruimte **software bibliotheek** **besturings systemen**uit en selecteer het knoop punt **taken reeksen** . **Bewerken** is nu de standaard actie bij het openen van een taken reeks. Voorheen was de standaard actie **Eigenschappen**.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Ga naar de verzameling vanuit een toepassings implementatie

*(Geïntroduceerd in versie 1902)*

1. Vouw in de werk ruimte **software bibliotheek** de optie **toepassings beheer**uit en selecteer het knoop punt **toepassingen** .
1. Selecteer een toepassing. Ga in het detail venster naar het tabblad **implementaties** .
1. Selecteer een implementatie en kies vervolgens de optie nieuwe **verzameling** in het lint op het tabblad implementatie. Met deze actie wordt de weer gave overgeschakeld naar de verzameling die het doel van de implementatie is.
   - Deze actie is ook beschikbaar via het context menu met de rechter muisknop op de implementatie in deze weer gave.


## <a name="monitoring-workspace"></a>Bewakings werkruimte

### <a name="correct-names-for-client-operations"></a>Juiste namen voor client bewerkingen
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Selecteer **client bewerkingen**in de werk ruimte **bewaking** . De bewerking om **over te scha kelen naar het volgende software-update punt** heeft nu de juiste naam.

### <a name="show-collection-name-for-scripts"></a>De naam van de verzameling voor scripts weer geven
<!--4616810-->
*(Geïntroduceerd in versie 1906)*

Selecteer in de werk ruimte **bewaking** het knoop punt **script status** . De naam van de **verzameling** wordt nu naast de id weer gegeven.

### <a name="remove-content-from-monitoring-status"></a>Inhoud verwijderen uit bewakings status

*(Geïntroduceerd in versie 1902)*

1. Vouw in **Monitoring** de werk ruimte bewaking **distributie status**uit en selecteer **inhouds status**.
1. Selecteer een item in de lijst en kies de optie **weergave status** in het lint.
1. Klik in het deel venster activum gegevens met de rechter muisknop op een distributie punt en selecteer de nieuwe optie **verwijderen**. Deze actie verwijdert deze inhoud van het geselecteerde distributie punt.

### <a name="copy-details-in-monitoring-views"></a>Details kopiëren in controle weergaven

*(Geïntroduceerd in versie 1806)*
<!--1357856-->
Gegevens uit het deel venster **activum gegevens** kopiëren voor de volgende bewakings knooppunten:  

- **Status van inhouds distributie**  

- **Implementatie status**  

![Status weergave van de implementatie, Details van activum kopiëren](media/1810-deployment-status.PNG)

## <a name="administration-workspace"></a>Werk ruimte beheer

<!--4223683-->
Vanaf versie 1906 kunt u enkele knoop punten inschakelen onder het knoop punt **beveiliging** om de beheer service te gebruiken. Met deze wijziging kan de console communiceren met de SMS-provider via HTTPS in plaats van via WMI. Zie [de beheer service instellen](../../../develop/adminservice/set-up.md#bkmk_console)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

- [De console gebruiken](admin-console.md)
- [Console meldingen](admin-console-notifications.md)
- [Toegankelijkheidsfuncties](../../understand/accessibility-features.md)