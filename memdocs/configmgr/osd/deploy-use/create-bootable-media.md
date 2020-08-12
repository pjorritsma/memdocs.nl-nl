---
title: Opstartbare media maken
titleSuffix: Configuration Manager
description: Gebruik opstart bare media in Configuration Manager om een nieuwe versie van Windows te installeren of een computer te vervangen.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e18c5e9e029900e10cebfb8e7bcdee29fd928ba
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125403"
---
# <a name="create-bootable-media"></a>Opstartbare media maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Opstart bare media in Configuration Manager bevatten de opstart installatie kopie, optionele prestart-opdrachten en bijbehorende bestanden en Configuration Manager bestanden. Opstart bare media gebruiken voor de volgende implementatie scenario's voor besturings systemen:

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)

- [Een bestaande computer vervangen en de instellingen overzetten](replace-an-existing-computer-and-transfer-settings.md)

## <a name="usage"></a>Gebruik

Het volgende proces treedt op wanneer opstart bare media worden opgestart:

1. De doel computer wordt gestart

1. Er wordt verbinding gemaakt met het netwerk

1. Hiermee wordt de volgende inhoud opgehaald van de site:

    - De opgegeven taken reeks

    - Installatie kopie van besturings systeem

    - Alle andere vereiste inhoud

Omdat de taken reeks zich niet op de media bevindt, kunt u de taken reeks of de inhoud wijzigen zonder dat u de media opnieuw hoeft te maken.

De pakketten op opstart bare media zijn niet versleuteld. Om ervoor te zorgen dat de pakket inhoud beveiligd is tegen onbevoegde gebruikers, neemt u de juiste beveiligings maatregelen. U kunt bijvoorbeeld een wacht woord toevoegen aan de media.

Vanaf versie 2006 kunnen opstart bare media op basis van de Cloud inhoud downloaden. Het apparaat heeft nog steeds een intranet verbinding met het beheer punt nodig. Dit kan inhoud ophalen van een CMG (Cloud Management Gateway) of een Cloud distributiepunt.<!--6209223--> Zie [ondersteuning voor Cloud inhoud](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content)voor meer informatie.

## <a name="prerequisites"></a>Vereisten

Voordat u opstart bare media maakt met behulp van de wizard taken reeks media maken, moet u ervoor zorgen dat aan alle voor waarden wordt voldaan.

### <a name="boot-image"></a>Opstartinstallatiekopie

Houd rekening met de volgende punten over de opstart installatie kopie die u in de taken reeks gebruikt om het besturings systeem te implementeren:

- De architectuur van de opstart installatie kopie moet geschikt zijn voor de architectuur van de doel computer. Op een x64-doelcomputer kan een x86- of x64-opstartinstallatiekopie worden opgestart en uitgevoerd. Op een x86-doelcomputer kan echter alleen een x86-opstartinstallatiekopie worden opgestart en uitgevoerd.
- Zorg ervoor dat de opstart installatie kopie de netwerk-en opslag Stuur Programma's bevat die nodig zijn om de doel computer in te richten.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Een taken reeks maken om een besturings systeem te implementeren

Geef als onderdeel van de opstart bare media de taken reeks op om het besturings systeem te implementeren. Zie [een taken reeks maken om een besturings systeem te installeren](create-a-task-sequence-to-install-an-operating-system.md)voor meer informatie.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Alle aan de takenreeks gekoppeld inhoud distribueren

Alle inhoud distribueren die de taken reeks nodig heeft tot ten minste één distributie punt. Deze inhoud bevat de opstart installatie kopie en andere bijbehorende prestart-bestanden. De wizard verzamelt de inhoud van het distributie punt wanneer het de opstart bare media maakt.

Uw gebruikers account moet ten minste **Lees** rechten hebben voor de inhouds bibliotheek op dat distributie punt. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Het verwisselbare USB-station voorbereiden

Als u een verwisselbaar USB-station gebruikt, verbindt u het met de computer waarop u de wizard taken reeks media maken uitvoert. Het USB-station moet detecteerbaar zijn door Windows als een Verwijder apparaat. De wizard schrijft rechtstreeks naar het USB-station wanneer deze het medium maakt.

### <a name="create-an-output-folder"></a>Een uitvoermap maken

Voordat u de wizard taken reeks media maken uitvoert voor het maken van media voor een CD-of DVD-set, moet u een map maken voor de uitvoer bestanden die worden gemaakt. Media die worden gemaakt voor een CD-of DVD-set, worden geschreven als een. ISO-bestand rechtstreeks in de map.

## <a name="process"></a>Proces

> [!NOTE]
> Aangezien u voor PKI-omgevingen de basis certificerings instantie (CA) op de primaire site opgeeft, moet u ervoor zorgen dat u de opstart bare media maakt op de primaire site. De centrale beheer site (CAS) beschikt niet over de gegevens van de basis certificerings instantie om de opstart bare media te maken.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer het knoop punt **taken reeksen** .

1. Klik op het tabblad **Start** van het lint in de groep **maken** op **taken reeks media maken**. Met deze actie wordt de wizard taken reeks media maken gestart.

1. Geef op de pagina **media type selecteren** de volgende opties op:

    - Selecteer **opstartbare media**.

    - Als u alleen wilt toestaan dat het besturings systeem wordt geïmplementeerd zonder dat er gebruikers invoer is vereist, selecteert u **implementatie van besturings systeem zonder toezicht toestaan**.

        > [!IMPORTANT]
        > Wanneer u deze optie selecteert, wordt de gebruiker niet gevraagd om informatie over de netwerk configuratie of voor optionele taken reeksen. Als u de media voor wachtwoord beveiliging configureert, wordt de gebruiker nog steeds gevraagd om een wacht woord.

1. Geef op de pagina **Media beheer** een van de volgende opties op:

    - **Dynamische media**: Hiermee staat u toe dat een beheer punt de media omleidt naar een ander beheer punt op basis van de client locatie in de grenzen van de site.

    - **Op site gebaseerde media**: de media nemen alleen contact op met het opgegeven beheer punt.

1. Geef op de pagina **medium type** op of het medium een **verwisselbaar USB-station** of een **cd/dvd-set**is. Configureer vervolgens de volgende opties:

    > [!IMPORTANT]
    > Media maakt gebruik van een FAT32-bestands systeem. U kunt geen media maken op een USB-station waarvan de inhoud een bestand bevat dat groter is dan 4 GB.

    - Als u **verwisselbaar USB-station**selecteert, selecteert u het station waar u de inhoud wilt opslaan.

        - **Verwisselbaar USB-station Format teren (FAT32) en maak een opstart bare**: standaard laat Configuration Manager het USB-station voorbereiden. Veel nieuwere UEFI-apparaten vereisen een opstart bare FAT32-partitie. Met deze indeling wordt echter ook de grootte van bestanden en de totale capaciteit van het station beperkt. Als u het Verwissel bare station al hebt geformatteerd en geconfigureerd, schakelt u deze optie uit.

    - Als u **cd/dvd-set**selecteert, geeft u de capaciteit van de media (**Media grootte**) en de naam en het pad op van het uitvoer bestand (**Media bestand**). De wizard schrijft de uitvoerbestanden naar deze locatie. Bijvoorbeeld: `\\servername\folder\outputfile.iso`

        Als de capaciteit van de media te klein is om de volledige inhoud op te slaan, worden er meerdere bestanden gemaakt. Vervolgens moet u de inhoud op meerdere cd's of Dvd's opslaan. Als er meerdere media bestanden zijn vereist, Configuration Manager een Volg nummer toevoegen aan de naam van elk uitvoer bestand dat wordt gemaakt.

        > [!IMPORTANT]
        > Als u een bestaande .iso-afbeelding selecteert, verwijdert de wizard voor het maken van takenreeksmedia die afbeelding uit het station of de share wanneer u doorgaat naar de volgende pagina van de wizard. De bestaande installatiekopie wordt gewist, zelfs als u de wizard annuleert.

    - **Tijdelijke map**<!--1359388-->: Voor het maken van media kan veel tijdelijke schijf ruimte nodig zijn. Deze locatie is standaard vergelijkbaar met het volgende pad: `%UserProfile%\AppData\Local\Temp` . Om u meer flexibiliteit te bieden bij het opslaan van deze tijdelijke bestanden, kunt u deze waarde wijzigen in een ander station en pad.

    - **Media label**<!--1359388-->: Voeg een label toe aan de taken reeks media. Dit label helpt u de media beter te identificeren nadat u deze hebt gemaakt. De standaardwaarde is `Configuration Manager`. Dit tekst veld wordt weer gegeven op de volgende locaties:

        - Als u een ISO-bestand koppelt, geeft Windows dit label weer als de naam van het gekoppelde station.

        - Als u een USB-station formatteert, worden de eerste elf tekens van het label als naam gebruikt.

        - Configuration Manager schrijft een tekst bestand `MediaLabel.txt` met de naam naar de hoofdmap van de media. Het bestand bevat standaard één tekst regel: `label=Configuration Manager` . Als u het label voor media aanpast, gebruikt deze lijn uw aangepaste label in plaats van de standaard waarde.

    - **Autorun. inf-bestand op media toevoegen**<!-- 4090666 -->: Vanaf versie 1906 wordt Configuration Manager standaard geen autorun. inf-bestand toegevoegd. Dit bestand wordt doorgaans geblokkeerd door antimalware-producten. Zie [een cd-rom-toepassing](https://docs.microsoft.com/windows/desktop/shell/autoplay)voor automatisch aanmelden maken voor meer informatie over de autorun-functie van Windows. Als het scenario nog steeds nodig is, selecteert u deze optie om het bestand op te laten voegen.

1. Geef op de pagina **beveiliging** de volgende opties op:

    - **Ondersteuning van onbekende computers inschakelen**: de media toestaan om een besturings systeem te implementeren op een computer die niet wordt beheerd door Configuration Manager. Er is geen record van deze computers in de Configuration Manager-Data Base. Zie [voor bereidingen voor onbekende computer implementaties](../get-started/prepare-for-unknown-computer-deployments.md)voor meer informatie.

    - **Media beveiligen met een wacht woord**: Voer een sterk wacht woord in om de media te beveiligen tegen onbevoegde toegang. Wanneer u een wachtwoord opgeeft, moet de gebruiker dat wachtwoord leveren om de opstartbare media te gebruiken.

        > [!IMPORTANT]
        > Wijs, als een best practice op vlak van beveiliging, altijd een wachtwoord toe om te helpen de opstartbare media te beschermen.

    - Voor HTTP-communicatie selecteert u **zelfondertekend certificaat maken**. Geef vervolgens de begin-en verval datum voor het certificaat op.

        > [!NOTE]
        > Als u deze optie selecteert, kunt u geen HTTPS-beheer punt selecteren op de pagina **opstart installatie kopie** van deze wizard.

    - Selecteer **PKI-certificaat importeren**voor HTTPS-communicatie. Geef vervolgens het certificaat op dat u wilt importeren en het bijbehorende wacht woord.

        Zie [PKI-certificaat vereisten](../../core/plan-design/network/pki-certificate-requirements.md)voor meer informatie over dit client certificaat dat wordt gebruikt voor opstart installatie kopieën.

    - **Affiniteit**Configuration Manager van gebruiker met apparaat: Geef op hoe u wilt dat de media gebruikers aan de doel computer koppelen. Zie [gebruikers koppelen aan een doel computer](../get-started/associate-users-with-a-destination-computer.md)voor meer informatie over hoe de besturingssysteem implementatie de gebruikers affiniteit van het apparaat ondersteunt.

        - **Affiniteit tussen gebruikers en apparaten toestaan met automatische goed keuring**: de media koppelt automatisch gebruikers aan de doel computer. Deze functionaliteit is gebaseerd op de acties van de taken reeks waarmee het besturings systeem wordt geïmplementeerd. In dit scenario maakt de taken reeks een relatie tussen de opgegeven gebruikers en de doel computer wanneer deze het besturings systeem implementeert op de doel computer.

        - **Gebruikers affiniteit met apparaat in afwachting van goed keuring van beheerder toestaan**: de media koppelt gebruikers aan de doel computer nadat goed keuring is verleend. Deze functionaliteit is gebaseerd op het bereik van de taken reeks die het besturings systeem implementeert. In dit scenario maakt de taken reeks een relatie tussen de opgegeven gebruikers en de doel computer. Vervolgens wordt gewacht op goed keuring van een gebruiker met beheerders rechten voordat het besturings systeem wordt geïmplementeerd.

        - **Gebruikers affiniteit met apparaat niet toestaan**: de media koppelt geen gebruikers aan de doel computer. In dit scenario koppelt de taken reeks geen gebruikers aan de doel computer wanneer deze het besturings systeem implementeert.

1. Geef op de pagina **opstart installatie kopie** de volgende opties op:

    > [!IMPORTANT]
    > De architectuur van de opstart installatie kopie die u distribueert, moet geschikt zijn voor de architectuur van de doel computer. Op een x64-doelcomputer kan een x86- of x64-opstartinstallatiekopie worden opgestart en uitgevoerd. Op een x86-doel computer kan echter alleen een x86-opstart installatie kopie worden opgestart en uitgevoerd.

    - **Opstart installatie kopie**: Selecteer de opstart installatie kopie om de doel computer te starten.

    - **Distributie punt**: Selecteer het distributie punt met de opstart installatie kopie. De wizard haalt de opstartinstallatiekopie op van het distributiepunt en schrijft deze naar de media.

        > [!NOTE]
        > Uw gebruikers account heeft mini maal **Lees** machtigingen nodig voor de inhouds bibliotheek op het distributie punt.

    - **Beheer punt**: alleen voor *site-gebaseerde media*selecteert u een beheer punt van een primaire site.

    - **Gekoppelde beheer punten**: alleen voor *dynamische media*, selecteer de beheer punten van de primaire site die moeten worden gebruikt en een prioriteits volgorde voor de eerste communicatie.

        > [!NOTE]
        > Wanneer u een PKI-certificaat opgeeft op de pagina **beveiliging** van deze wizard, worden alleen beheer punten met https-functionaliteit weer gegeven op deze pagina.

1. Geef op de pagina **aanpassing** de volgende opties op:

    - Voeg alle variabelen toe die door de taken reeks worden gebruikt.

    - **Prestart-opdracht inschakelen**: Geef eventuele prestart-opdrachten op die u wilt uitvoeren voordat de taken reeks wordt uitgevoerd. Prestart-opdrachten bestaan uit een script of een uitvoerbaar bestand dat kan communiceren met de gebruiker in Windows PE voordat de taken reeks wordt uitgevoerd. Zie [prestart-opdrachten voor taken reeks media](../understand/prestart-commands-for-task-sequence-media.md)voor meer informatie.

        > [!TIP]
        > Tijdens het maken van de media schrijft de taken reeks de pakket-ID en prestart-opdracht regel, inclusief de waarde voor eventuele taken reeks variabelen, naar het bestand **CreateTSMedia. log** op de computer waarop de Configuration Manager-console wordt uitgevoerd. U kunt dit logboekbestand controleren om de waarde voor de takenreeksvariabelen te verifiëren.

        Als de prestart-opdracht inhoud vereist, selecteert u de optie voor **het toevoegen van bestanden voor de prestart-opdracht**.

1. Voltooi de wizard.

## <a name="alternate-method"></a>Alternatieve methode

U kunt opstart bare media maken op een verwisselbaar USB-station wanneer het station niet is verbonden met de computer waarop de Configuration Manager-console wordt uitgevoerd.

1. [Maak de opstart media voor de taken reeks](#process). Selecteer op de pagina **media type** de optie **cd/dvd-set**. De wizard schrijft de uitvoer bestanden naar de locatie die u opgeeft. Bijvoorbeeld: `\\servername\folder\outputfile.iso`.  

1. Bereid het Verwissel bare USB-station voor. Het station moet geformatteerd, leeg en opstart bare zijn.

1. Koppel de ISO van de share locatie en zet de bestanden over van de ISO naar het USB-station.

## <a name="next-steps"></a>Volgende stappen

[Opstartbare media gebruiken om Windows te implementeren via het netwerk](use-bootable-media-to-deploy-windows-over-the-network.md)  
