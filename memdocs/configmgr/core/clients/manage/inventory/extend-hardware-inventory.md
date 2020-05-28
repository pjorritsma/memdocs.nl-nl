---
title: Hardware-inventaris uitbreiden
titleSuffix: Configuration Manager
description: Leer hoe u hardware-inventaris kunt uitbreiden in Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 39e88debf5c25fb3a033c322e37663549ead29fd
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427758"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>Hardware-inventarisatie uitbreiden in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met de hardware-inventarisatie worden gegevens van Windows-Pc's gelezen met behulp van Windows Management Instrumentation (WMI). WMI is de micro soft-implementatie van web-based Enter prise Management (WBEM), een industrie standaard voor het openen van beheer gegevens in een onderneming. In eerdere versies van Configuration Manager hebt u de hardware-inventarisatie uitgebreid door het bestand sms_def. mof op de site server te wijzigen. Dit bestand bevat een lijst met WMI-klassen die door de hardware-inventaris kunnen worden gelezen. Als u dit bestand bewerkt, kunt u bestaande klassen inschakelen en uitschakelen, en ook nieuwe klassen aan de inventaris maken.  

Het bestand Configuration. mof wordt gebruikt voor het definiëren van de gegevens klassen die moeten worden geïnventariseerd door hardware-inventaris op de client en is ongewijzigd ten opzichte van Configuration Manager 2012. U kunt gegevensklassen maken voor het inventariseren van bestaande of aangepaste gegevensklassen voor WMI-opslagplaatsen of registersleutels aanwezig op clientsystemen.  

 Het bestand Configuration.mof bepaalt en registreert ook de WMI-providers die toegang hebben tot informatie over apparaten tijdens hardware-inventarisatie. Registreren van providers definieert het type provider dat moet worden gebruikt en de klassen die de provider ondersteunt.  

 Als Configuration Manager aanvragen beleid voor clients, wordt de configuratie. MOF gekoppeld aan de beleids tekst. Dit bestand wordt vervolgens gedownload en gecompileerd door clients. Wanneer u gegevensklassen uit het bestand Configuration.mof toevoegt, wijzigt of verwijdert, compileren clients automatisch deze wijzigingen die zijn aangebracht in de gegevensklassen gerelateerd aan inventaris. Er is geen verdere actie nodig voor inventarisatie van nieuwe of gewijzigde gegevens klassen op Configuration Manager-clients. Dit bestand bevindt zich in **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** op primaire siteservers.  

 In Configuration Manager bewerkt u het bestand sms_def. MOF niet meer zoals in Configuration Manager 2007. U kunt in plaats daarvan WMI-klassen inschakelen en uitschakelen, en u kunt nieuwe klassen toevoegen voor het verzamelen van hardware-inventaris met clientinstellingen. Configuration Manager biedt de volgende methoden om de hardware-inventaris uit te breiden.  

> [!NOTE]  
>  Als u het bestand Configuration. MOF hand matig hebt gewijzigd om aangepaste inventaris klassen toe te voegen, worden deze wijzigingen overschreven wanneer u bijwerkt naar versie 1602. Als u aangepaste klassen wilt blijven gebruiken na het bijwerken, moet u deze toevoegen aan de sectie ' extensies toevoegen ' van het bestand Configuration. MOF nadat u hebt bijgewerkt naar 1602.  
> Het is echter niet mogelijk om iets boven deze sectie te wijzigen, omdat deze secties zijn gereserveerd voor wijziging door Configuration Manager. U kunt een back-up van uw aangepaste Configuration.mof-bestand vinden in:  
> **<CM Install dir\>\data\hinvarchive\\**.  

## <a name="methods"></a>Methoden

### <a name="enable-or-disable"></a>In-of uitschakelen

Het in-of uitschakelen van alle kenmerken van een klasse die al bestaat op de client. Deze actie geeft de hardware-inventaris agent opdracht om deze te verzamelen op clients. U kunt deze actie uitvoeren in standaard client instellingen of aangepaste client instellingen voor apparaten. Zie [bestaande inventaris klassen in-of uitschakelen](#BKMK_Enable)voor meer informatie.

### <a name="add"></a>Toevoegen

Als er een WMI-klasse op de client bestaat en bekend is bij de-site, neemt deze actie deze op naar de mogelijke set hardware-inventaris klassen. U kunt een nieuwe inventarisklasse toevoegen via de WMI-naamruimte van een ander apparaat. Deze actie is alleen voor de standaard instellingen van de client. Zie [een nieuwe inventaris klasse toevoegen](#BKMK_Add)voor meer informatie.

### <a name="extend"></a>Verlengen

Voeg een nieuwe WMI-klasse toe aan de client. Als u de hardware-inventaris hand matig wilt uitbreiden, bewerkt u de Configuration. mof op de site op het hoogste niveau.<!-- SCCMDocs#1073 -->

Als de WMI-klasse nog niet bestaat op de client, moet u het WMI-schema uitbreiden:

1. Bewerk de Configuration. mof op de site op het hoogste niveau. Raadpleeg **dataldr. log** om de site toe te voegen.

1. Vernieuw het beleid op een client en wacht totdat de nieuwe klasse is gecompileerd.

1. Standaard client instellingen gebruiken om de nieuwe klasse toe te [voegen](#add) aan de hardware-inventaris. U hoeft deze klasse niet in te scha kelen in de standaard instellingen van de client. Vervolgens kunt u de client instelling inschakelen in een aangepaste apparaatclient.

### <a name="import-and-export"></a>Importeren en exporteren

Gebruik de Configuration Manager-console voor het importeren en exporteren van Managed Object Format (MOF)-bestanden die inventaris klassen bevatten. Zie [hardware-inventaris klassen importeren](#BKMK_Import) en [hardware-inventaris klassen exporteren](#BKMK_Export)voor meer informatie.

### <a name="create-noidmif-files"></a>NOIDMIF-bestanden maken

Gebruik NOIDMIF-bestanden voor het verzamelen van informatie over client apparaten die Configuration Manager niet kan inventariseren. Verzamel bijvoorbeeld informatie over apparaat-assetnummer die alleen bestaat als een label op het apparaat. NOIDMIF-inventarisatie is automatisch gekoppeld aan het clientapparaat waarvan deze is verzameld. Zie [NOIDMIF-bestanden maken](#BKMK_NOIDMIF)voor meer informatie.

### <a name="create-idmif-files"></a>IDMIF-bestanden maken

Gebruik IDMIF-bestanden voor het verzamelen van informatie over assets in uw organisatie die niet zijn gekoppeld aan een Configuration Manager-client. Bijvoorbeeld projectors, Fotokopieer apparaten en netwerk printers. Zie [IDMIF-bestanden maken](#BKMK_IDMIF)voor meer informatie.

## <a name="procedures-to-extend-hardware-inventory"></a>Procedures voor het uitbreiden van hardware-inventaris

Deze procedures helpen u de standaardclientinstellingen voor hardware-inventaris te configureren en ze zijn van toepassing op alle clients in uw hiërarchie. Als u wilt dat deze instellingen alleen van toepassing zijn op sommige clients, maakt u een aangepaste client apparaat-instelling en wijst u deze toe aan een verzameling specifieke clients. Zie [client instellingen configureren](../../../../core/clients/deploy/configure-client-settings.md)voor meer informatie.  

### <a name="enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a>Bestaande inventaris klassen in-of uitschakelen  

1. Kies in de Configuration Manager-console de client instellingen voor **de client instellingen**  >  **Client Settings**  >  **standaard**.  

1. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

1. In het dialoog venster **standaard client instellingen** kiest u **Hardware-inventarisatie**.  

1. Selecteer in de lijst **Apparaatinstellingen** de optie **klassen instellen**.  

1. In het dialoogvenster **Hardware-inventarisklassen** selecteert of wist u de klassen en klasse-eigenschappen die moeten worden verzameld door hardware-inventarisatie. U kunt klassen uitbreiden om afzonderlijke eigenschappen in een klasse te selecteren of te wissen. Gebruik het veld **Zoeken naar inventarisklassen** om te zoeken naar afzonderlijke klassen.  

    > [!IMPORTANT]  
    >  Wanneer u nieuwe klassen toevoegt aan Configuration Manager hardware-inventaris, neemt de grootte van het inventarisatie bestand dat wordt verzameld en verzonden naar de site server toe. Dit kan een negatieve invloed hebben op de prestaties van uw netwerk en Configuration Manager-site. Schakel de inventarisklassen in die u wilt verzamelen.  

### <a name="add-a-new-inventory-class"></a><a name="BKMK_Add"></a>Een nieuwe inventaris klasse toevoegen  

U kunt alleen inventaris klassen toevoegen vanaf de server van het hoogste niveau van de hiërarchie door de standaard client instellingen te wijzigen. Deze optie is niet beschikbaar wanneer u aangepaste apparaatinstellingen maakt.

1. Kies in de Configuration Manager-console de client instellingen voor **de client instellingen**  >  **Client Settings**  >  **standaard**.  

1. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

1. In het dialoog venster **standaard client instellingen** kiest u **Hardware-inventarisatie**.  

1. Kies in de lijst **Apparaatinstellingen** de optie **klassen instellen**.  

1. Kies in het dialoog venster **hardware-inventaris klassen** **toevoegen**.  

1. Selecteer in het dialoog venster **hardware-inventaris klasse toevoegen** de optie **verbinding maken**.  

1. Geef in het dialoog venster **verbinding maken met Windows Management Instrumentation (WMI)** de naam op van de computer waarvandaan u de WMI-klassen en de WMI-naam ruimte ophaalt die u wilt gebruiken voor het ophalen van de klassen. Als u alle klassen wilt ophalen onder de WMI-naam ruimte die u hebt opgegeven, selecteert u **recursief**. Als de computer waarmee u verbinding maakt, niet de lokale computer is, geeft u referenties op voor een account dat toegang heeft tot WMI op de externe computer.

1. Kies **Verbinding maken**.  

1. Selecteer in het dialoog venster **hardware-inventaris klasse toevoegen** in de lijst **inventaris klassen** de WMI-klassen die u wilt toevoegen aan Configuration Manager Hardware-inventarisatie.  

1. Als u informatie over de geselecteerde WMI-klasse wilt bewerken, kiest u **bewerken**en geeft u in het dialoog venster **klassen kwalificaties** de volgende informatie op:  

    - **Weergave naam**: deze naam wordt weer gegeven in resource Explorer.  

    - **Eigenschappen**: Geef de eenheden op waarin elke eigenschap van de WMI-klasse wordt weer gegeven.  

      U kunt ook eigenschappen instellen als sleutel eigenschap om elke instantie van de klasse uniek te identificeren. Als er geen sleutel is gedefinieerd voor de klasse en meerdere exemplaren van de klasse worden gerapporteerd door de client, wordt alleen de laatste gevonden instantie in de database opgeslagen.  

      Wanneer u klaar bent met het configureren van de eigenschappen, selecteert u **OK** om het dialoog venster **klassen kwalificaties** en de andere geopende dialoog vensters te sluiten.

### <a name="import-hardware-inventory-classes"></a><a name="BKMK_Import"></a>Hardware-inventaris klassen importeren

U kunt alleen inventarisklassen importeren wanneer u de standaardclientinstellingen wijzigt. U kunt echter aangepaste client instellingen gebruiken voor het importeren van gegevens die geen schema wijziging bevatten, zoals het wijzigen van de eigenschap van een bestaande klasse van **waar** in **Onwaar**.  

1. Kies in de Configuration Manager-console de client instellingen voor **de client instellingen**  >   **Client Settings**  >  **standaard**.

1. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

1. In het dialoog venster **standaard client instellingen** kiest u **Hardware-inventarisatie**.  

1. Kies in de lijst **Apparaatinstellingen** de optie **klassen instellen**.  

1. Kies in het dialoog venster **hardware-inventaris klassen** **importeren**.  

1. Selecteer in het dialoog venster **importeren** het Managed Object Format MOF-bestand dat u wilt importeren en klik vervolgens op **OK**. Controleer de items die worden geïmporteerd en selecteer vervolgens **importeren**.  

### <a name="export-hardware-inventory-classes"></a><a name="BKMK_Export"></a>Hardware-inventaris klassen exporteren  

1. Kies in de Configuration Manager-console de client instellingen voor **de client instellingen**  >  **Client Settings**  >  **standaard**.  

1. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

1. In het dialoog venster **standaard client instellingen** kiest u **Hardware-inventarisatie**.  

1. Kies in de lijst **Apparaatinstellingen** de optie **klassen instellen**.  

1. Kies in het dialoog venster **hardware-inventaris klassen** **exporteren**.  

    > [!NOTE]  
    > Als u klassen exporteert, worden alle geselecteerde klassen worden geëxporteerd.  

1. Geef in het dialoog venster **exporteren** het Managed Object Format (MOF)-bestand op waarnaar u de klassen wilt exporteren en kies vervolgens **Opslaan**.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>Hardware-inventaris configureren voor het verzamelen van teken reeksen die groter zijn dan 255 tekens

U kunt de lengte van teken reeksen opgeven die groter is dan 255 tekens voor hardware-inventarisatie-eigenschappen. Deze actie is alleen van toepassing op nieuw toegevoegde klassen en voor hardware-inventarisatie-eigenschappen die geen sleutels zijn. <!-- 1357389 -->

1. Selecteer **client instellingen**in de werk ruimte **beheer** . Kies een instelling voor het client apparaat die u wilt bewerken en selecteer vervolgens **Eigenschappen**.

1. Selecteer **hardware-inventaris**, vervolgens **klassen instellen**en **toevoegen**.

1. Selecteer **Verbinding maken**.

1. Vul de **computer naam**, de **WMI-naam ruimte**, het selectie vakje **recursief** in als dat nodig is. Geef indien nodig referenties op om verbinding te maken. Selecteer **verbinding maken** om de naam ruimte klassen weer te geven.

1. Selecteer een nieuwe klasse en selecteer vervolgens **bewerken**.

1. Wijzig de **lengte** van uw eigenschap die een teken reeks is, behalve de sleutel, die groter is dan 255. Selecteer **OK**.

1. Zorg ervoor dat de bewerkte eigenschap is geselecteerd voor **hardware-inventaris klasse toevoegen**en selecteer **OK**.

## <a name="use-mif-files-to-extend-hardware-inventory"></a>MIF-bestanden gebruiken om hardware-inventaris uit te breiden

Gebruik MIF-bestanden (Management Information Format) om informatie over hardware-inventarisatie uit te breiden die door Configuration Manager is verzameld. Tijdens de hardware-inventaris wordt de in MIF-bestanden opgeslagen informatie toegevoegd aan het clientinventarisrapport en opgeslagen in de sitedatabase, waar u de gegevens op dezelfde manier kunt gebruiken als standaard clientinventarisgegevens. Er zijn twee soorten MIF-bestanden: NOIDMIF en IDMIF.

> [!IMPORTANT]  
> Voordat u gegevens van MIF-bestanden kunt toevoegen aan de Configuration Manager-Data Base, moet u hier klassegegevens voor maken of importeren. Zie de secties [een nieuwe inventaris klasse toevoegen](#BKMK_Add) en [hardware-inventaris klassen importeren](#BKMK_Import) in dit artikel voor meer informatie.  

### <a name="create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a>NOIDMIF-bestanden maken

NOIDMIF-bestanden kunnen worden gebruikt om informatie toe te voegen aan een hardware-inventarisatie van de client die normaal gesp roken niet kan worden verzameld door Configuration Manager en is gekoppeld aan een bepaald client apparaat. Bijvoorbeeld: veel bedrijven labelen elke computer in de organisatie met een activum nummer en catalogiseren deze nummers vervolgens hand matig. Wanneer u een NOIDMIF-bestand maakt, kan deze informatie worden toegevoegd aan de Configuration Manager-Data Base en worden gebruikt voor query's en rapportage. Zie de Configuration Manager SDK-documentatie voor meer informatie over het maken van NOIDMIF-bestanden.  

> [!IMPORTANT]  
> Wanneer u een NOIDMIF-bestand maakt, moet dit worden opgeslagen in een indeling met ANSI-code ring. NOIDMIF-bestanden die zijn opgeslagen in een indeling met UTF-8-code ring kunnen niet worden gelezen door Configuration Manager.  

Nadat u een NOIDMIF-bestand hebt gemaakt, slaat u dit op in de `%Windir%\CCM\Inventory\Noidmifs` map op elke client. Tijdens de volgende geplande Hardware-inventarisatie fase verzamelt Configuration Manager gegevens uit NODMIF-bestanden in deze map.  

### <a name="create-idmif-files"></a><a name="BKMK_IDMIF"></a>IDMIF-bestanden maken

IDMIF-bestanden kunnen worden gebruikt om informatie toe te voegen over assets die normaal gesp roken niet kunnen worden geïnventariseerd door Configuration Manager en niet zijn gekoppeld aan een bepaald client apparaat, aan de Configuration Manager-Data Base. U kunt kunt IDMIF gebruiken bijvoorbeeld gebruiken om informatie te verzamelen over projectors, DVD-spelers, fotokopieers of andere apparatuur die geen Configuration Manager-client heeft. Zie de Configuration Manager SDK-documentatie voor meer informatie over het maken van IDMIF-bestanden.  

Nadat u een IDMIF-bestand hebt gemaakt, slaat u dit op in de `%Windir%\CCM\Inventory\Idmifs` map op client computers. Tijdens de volgende geplande Hardware-inventarisatie fase verzamelt Configuration Manager informatie uit dit bestand. Declareer nieuwe klassen voor informatie die is opgenomen in het bestand door deze toe te voegen of te importeren.  

> [!NOTE]
> MIF-bestanden kunnen grote hoeveelheden gegevens bevatten en de verzameling van deze gegevens kan een negatieve invloed hebben op de prestaties van uw site. Schakel de MIF-verzameling alleen in indien nodig en configureer de optie **maximale aangepaste MIF-bestands grootte (KB)** in de hardware-inventaris instellingen. Zie [Inleiding op Hardware-inventarisatie](introduction-to-hardware-inventory.md)voor meer informatie.
