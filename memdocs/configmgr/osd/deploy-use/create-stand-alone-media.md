---
title: Zelfstandige media maken
titleSuffix: Configuration Manager
description: Zelfstandige media gebruiken om het besturings systeem te implementeren op een computer zonder een netwerk verbinding.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e477d08ed97fe46bbe51b62a0ed024d437c2626
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711005"
---
# <a name="create-stand-alone-media"></a>Zelfstandige media maken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Zelfstandige media in Configuration Manager bevatten alles wat u nodig hebt om het besturings systeem op een computer te implementeren zonder een netwerk verbinding.

Gebruik zelfstandige media met de volgende implementatie scenario's voor besturings systemen:  

- [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)  

- [Windows bijwerken naar de laatste versie](upgrade-windows-to-the-latest-version.md)  


## <a name="usage"></a>Gebruik

Zelfstandige media bevatten de taken reeks waarmee de stappen voor het installeren van het besturings systeem en alle andere vereiste inhoud worden geautomatiseerd. Deze inhoud bevat de opstart installatie kopie, de installatie kopie van het besturings systeem en de apparaatstuurprogramma's. Omdat de zelfstandige media alles opslaat om het besturings systeem te implementeren, hebt u meer schijf ruimte nodig dan is vereist voor andere media typen.

Wanneer u zelfstandige media op een centrale beheer site maakt, haalt de client de toegewezen site code op uit Active Directory. Zelfstandige media die worden gemaakt op onderliggende sites, worden automatisch toegewezen aan de client de site code voor die site.  


## <a name="prerequisites"></a>Vereisten

Voordat u zelfstandige media maakt met behulp van de wizard taken reeks media maken, moet u ervoor zorgen dat aan alle voor waarden wordt voldaan.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Een taken reeks maken om een besturings systeem te implementeren

Geef als onderdeel van de zelfstandige media de taken reeks op om een besturings systeem te implementeren. Zie [een taken reeks maken om een besturings systeem te installeren](create-a-task-sequence-to-install-an-operating-system.md)voor meer informatie.

#### <a name="unsupported-actions-for-stand-alone-media"></a>Niet-ondersteunde acties voor zelfstandige media

De volgende acties worden niet ondersteund voor zelfstandige media:

- De stap [Stuur Programma's automatisch Toep assen](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) in de taken reeks. Zelfstandige media bieden geen ondersteuning voor automatische toepassing van apparaatstuurprogramma's uit de stuurprogrammacatalogus. Gebruik de stap [Stuur programmapakket Toep assen](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) om een opgegeven set stuur Programma's beschikbaar te maken voor Windows Setup.  

- De stap [pakket inhoud downloaden](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) in de taken reeks. De informatie van het beheer punt is niet beschikbaar op zelfstandige media, waardoor de stap mislukt met het opsommen van inhouds locaties.  

- Installatie van software-updates.  

- Software installeren voordat het besturings systeem wordt geïmplementeerd.  

- Aangepaste taken reeksen voor niet-besturingssysteem implementaties.  

- Koppelen van gebruikers aan de doelcomputer ter ondersteuning van de gebruikersaffiniteit van apparaten.  

- Dynamisch pakket wordt geïnstalleerd via de stap [pakketten installeren](../understand/task-sequence-steps.md#BKMK_InstallPackage) .  

- Dynamische toepassing wordt geïnstalleerd via de stap [toepassing installeren](../understand/task-sequence-steps.md#BKMK_InstallApplication) .

- Het **client pakket pre-production gebruiken wanneer beschikbaar** in de taken reeks stap **Windows en ConfigMgr installeren** . Zie [Setup Windows and ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)voor meer informatie over deze instelling.  

> [!NOTE]  
> Als uw taken reeks de stap [pakket installeren](../understand/task-sequence-steps.md#BKMK_InstallPackage) bevat en u de zelfstandige media op een centrale beheer site maakt, kan er een fout optreden. De centrale beheer site beschikt niet over de benodigde client configuratie beleidsregels. Deze beleids regels zijn vereist voor het inschakelen van de agent voor software distributie wanneer de taken reeks wordt uitgevoerd. De volgende fout kan worden weer gegeven in het bestand **CreateTsMedia. log** :  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> Voor zelfstandige media met de stap **pakket installeren** maakt u de zelfstandige media op een primaire site waarop de agent voor software distributie is ingeschakeld.
>
> U kunt ook een aangepaste [Run-opdracht regel](../understand/task-sequence-steps.md#BKMK_RunCommandLine) stap gebruiken. Voeg deze toe na de stap [Windows en ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) installeren en voor de eerste stap **pakket installatie** . Met de stap **opdracht regel uitvoeren** voert u de volgende WMIC-opdracht uit om de agent voor software distributie in te scha kelen vóór de eerste stap pakket installeren:  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Alle aan de takenreeks gekoppeld inhoud distribueren

Alle inhoud distribueren die de taken reeks nodig heeft tot ten minste één distributie punt. Deze inhoud bevat de opstart installatie kopie, de installatie kopie van het besturings systeem en andere gekoppelde bestanden. De wizard verzamelt de inhoud van het distributie punt wanneer het de media maakt.

Uw gebruikers account moet ten minste **Lees** rechten hebben voor de inhouds bibliotheek op dat distributie punt. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Het verwisselbare USB-station voorbereiden

Als u een verwisselbaar USB-station gebruikt, verbindt u het met de computer waarop u de wizard taken reeks media maken uitvoert. Het USB-station moet detecteerbaar zijn door Windows als een Verwijder apparaat. De wizard schrijft rechtstreeks naar het USB-station wanneer deze het medium maakt.

Zelfstandige media maakt gebruik van een FAT32-bestandssysteem. U kunt geen zelfstandige media maken op een verwisselbaar USB-station waarvan de inhoud een bestand bevat dat groter is dan 4 GB.

### <a name="create-an-output-folder"></a>Een uitvoermap maken

Voordat u de wizard taken reeks media maken uitvoert voor het maken van media voor een CD-of DVD-set, moet u een map maken voor de uitvoer bestanden die worden gemaakt. Media die worden gemaakt voor een CD-of DVD-set, worden geschreven als een. ISO-bestand rechtstreeks in de map.


## <a name="process"></a>Proces

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer het knoop punt **taken reeksen** .  

2. Klik op het tabblad **Start** van het lint in de groep **maken** op **taken reeks media maken**. Met deze actie wordt de wizard taken reeks media maken gestart.  

3. Geef op de pagina **media type selecteren** de volgende opties op:  

    - Selecteer **Zelfstandige media**.  

    - Als u alleen wilt toestaan dat het besturings systeem wordt geïmplementeerd zonder dat er gebruikers invoer is vereist, selecteert u **implementatie van besturings systeem zonder toezicht toestaan**.  

        > [!IMPORTANT]  
        > Wanneer u deze optie selecteert, wordt de gebruiker niet gevraagd om informatie over de netwerk configuratie of voor optionele taken reeksen. Als u de media voor wachtwoord beveiliging configureert, wordt de gebruiker nog steeds gevraagd om een wacht woord.  

4. Geef op de pagina **medium type** op of het medium een **verwisselbaar USB-station** of een **cd/dvd-set**is. Configureer vervolgens de volgende opties:  

    > [!IMPORTANT]  
    > Media maakt gebruik van een FAT32-bestands systeem. U kunt geen media maken op een USB-station waarvan de inhoud een bestand bevat dat groter is dan 4 GB.  

    - Als u **verwisselbaar USB-station**selecteert, selecteert u het station waar u de inhoud wilt opslaan.  

        - **Verwisselbaar USB-station Format teren (FAT32) en maak een opstart bare**: standaard laat Configuration Manager het USB-station voorbereiden. Veel nieuwere UEFI-apparaten vereisen een opstart bare FAT32-partitie. Met deze indeling wordt echter ook de grootte van bestanden en de totale capaciteit van het station beperkt. Als u het Verwissel bare station al hebt geformatteerd en geconfigureerd, schakelt u deze optie uit.

    - Als u **cd/dvd-set**selecteert, geeft u de capaciteit van de media (**Media grootte**) en de naam en het pad op van het uitvoer bestand (**Media bestand**). De wizard schrijft de uitvoerbestanden naar deze locatie. Bijvoorbeeld: `\\servername\folder\outputfile.iso`  

        Als de capaciteit van de media te klein is om de volledige inhoud op te slaan, worden er meerdere bestanden gemaakt. Vervolgens moet u de inhoud op meerdere cd's of Dvd's opslaan. Als er meerdere media bestanden zijn vereist, Configuration Manager een Volg nummer toevoegen aan de naam van elk uitvoer bestand dat wordt gemaakt.  

        Als u een toepassing implementeert in combi natie met het besturings systeem en de toepassing niet op één medium past, slaat Configuration Manager de toepassing op in meerdere media. Wanneer de zelfstandige media worden uitgevoerd, wordt de gebruiker door Configuration Manager gevraagd naar de volgende media waar de toepassing is opgeslagen.  

        > [!IMPORTANT]  
        > Als u een bestaande .iso-afbeelding selecteert, verwijdert de wizard voor het maken van takenreeksmedia die afbeelding uit het station of de share wanneer u doorgaat naar de volgende pagina van de wizard. De bestaande installatiekopie wordt gewist, zelfs als u de wizard annuleert.  

    - **Tijdelijke map**<!--1359388-->: Voor het maken van media kan veel tijdelijke schijf ruimte nodig zijn. Deze locatie is standaard vergelijkbaar met het volgende pad: `%UserProfile%\AppData\Local\Temp`. Vanaf versie 1902, om u meer flexibiliteit te bieden bij het opslaan van deze tijdelijke bestanden, wijzigt u deze waarde in een ander station en pad.  

    - **Media label**<!--1359388-->: Vanaf versie 1902 voegt u een label toe aan de taken reeks media. Dit label helpt u de media beter te identificeren nadat u deze hebt gemaakt. De standaardwaarde is `Configuration Manager`. Dit tekst veld wordt weer gegeven op de volgende locaties:  

        - Als u een ISO-bestand koppelt, geeft Windows dit label weer als de naam van het gekoppelde station  

        - Als u een USB-station formatteert, worden de eerste elf tekens van het label als naam gebruikt  

        - Configuration Manager schrijft een tekst bestand met `MediaLabel.txt` de naam naar de hoofdmap van de media. Het bestand bevat standaard één tekst regel: `label=Configuration Manager`. Als u het label voor media aanpast, gebruikt deze lijn uw aangepaste label in plaats van de standaard waarde.  

    - **Autorun. inf-bestand op media toevoegen**<!-- 4090666 -->: Vanaf versie 1906 wordt Configuration Manager standaard geen autorun. inf-bestand toegevoegd. Dit bestand wordt doorgaans geblokkeerd door antimalware-producten. Zie [een cd-rom-toepassing](https://docs.microsoft.com/windows/desktop/shell/autoplay)voor automatisch aanmelden maken voor meer informatie over de autorun-functie van Windows. Als het scenario nog steeds nodig is, selecteert u deze optie om het bestand op te laten voegen.  

5. Geef op de pagina **beveiliging** de volgende opties op:

    - **Media beveiligen met een wacht woord**: Voer een sterk wacht woord in om de media te beveiligen tegen onbevoegde toegang. Wanneer u een wacht woord opgeeft, moet de gebruiker dat wacht woord opgeven om de media te gebruiken.  

        > [!IMPORTANT]  
        > Wijs als beveiligings best practice altijd een wacht woord toe om de media te beveiligen.  
        >
        > Op zelfstandige media worden alleen de taken reeks stappen en hun variabelen versleuteld. De resterende inhoud van de media wordt niet versleuteld. Neem geen gevoelige informatie op in taken reeks scripts. U kunt alle gevoelige informatie opslaan en implementeren met behulp van takenreeksvariabelen.  

    - **Selecteer een geldig datum bereik voor deze zelfstandige media**: stel optionele begin-en verval datums in op het medium. Deze instelling is standaard uitgeschakeld. De datums worden vergeleken met de systeem tijd op de computer voordat de zelfstandige media worden uitgevoerd. Wanneer de systeem tijd eerder is dan de begin tijd of later dan de verloop tijd, wordt de zelfstandige media niet gestart. Deze opties zijn ook beschikbaar met de Power shell [-cmdlet New-CMStandaloneMedia](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps) .  

6. Selecteer op de pagina **zelfstandige CD/DVD** de taken reeks die het besturings systeem implementeert. U kunt alleen die taken reeksen selecteren die aan een opstart installatie kopie zijn gekoppeld. Controleer de lijst met inhoud waarnaar wordt verwezen door de taken reeks.  

    - **Gekoppelde toepassings afhankelijkheden detecteren en toevoegen aan deze media**: Voeg ook inhoud toe aan de media voor toepassings afhankelijkheden.  

        > [!TIP]  
        > Als de verwachte toepassings afhankelijkheden niet worden weer geven, schakelt u deze optie uit om de lijst te vernieuwen.  

7. Geef op de pagina **toepassing selecteren** aanvullende toepassings inhoud op die moet worden opgenomen als onderdeel van het Media bestand.  

8. Geef op de pagina **pakket selecteren** de aanvullende pakket inhoud op die moet worden opgenomen als onderdeel van het Media bestand.  

9. Geef op de pagina **Stuur programmapakket selecteren** aanvullende inhoud voor het stuur programmapakket op die moet worden opgenomen als onderdeel van het Media bestand.  

10. Geef op de pagina **distributie punten** de distributie punten op die de vereiste inhoud bevatten.  

    Configuration Manager worden alleen distributie punten met de inhoud weer gegeven. Distribueer alle inhoud die is gekoppeld aan de taken reeks naar ten minste één distributie punt voordat u doorgaat. Nadat u de inhoud hebt gedistribueerd, vernieuwt u de lijst met distributie punten. Verwijder alle distributie punten die u al op deze pagina hebt geselecteerd, gaat u naar de vorige pagina en vervolgens weer terug naar de pagina **distributie punten** . U kunt ook de wizard opnieuw starten. Zie [inhoud distribueren waarnaar wordt verwezen door een taken reeks](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) en [inhoud en infra structuur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor inhoud beheren voor meer informatie.  

11. Geef op de pagina **aanpassing** de volgende opties op:  

    - Voeg alle variabelen toe die door de taken reeks worden gebruikt.  

    - **Prestart-opdracht inschakelen**: Geef eventuele prestart-opdrachten op die u wilt uitvoeren voordat de taken reeks wordt uitgevoerd. Prestart-opdrachten bestaan uit een script of een uitvoerbaar bestand dat kan communiceren met de gebruiker in Windows PE voordat de taken reeks wordt uitgevoerd. Zie [prestart-opdrachten voor taken reeks media](../understand/prestart-commands-for-task-sequence-media.md)voor meer informatie.  

        > [!TIP]  
        > Tijdens het maken van de media schrijft de taken reeks de pakket-ID en prestart-opdracht regel, inclusief de waarde voor eventuele taken reeks variabelen, naar het bestand **CreateTSMedia. log** op de computer waarop de Configuration Manager-console wordt uitgevoerd. U kunt dit logboekbestand controleren om de waarde voor de takenreeksvariabelen te verifiëren.  

        Als de prestart-opdracht inhoud vereist, selecteert u de optie voor **het toevoegen van bestanden voor de prestart-opdracht**.  

12. Voltooi de wizard.  

De zelfstandige media bestanden (. ISO) worden in de doelmap gemaakt. Als u **cd/dvd-set**hebt geselecteerd, kopieert u de uitvoer bestanden naar een set cd's of dvd's.


## <a name="next-steps"></a>Volgende stappen

[Zelfstandige media gebruiken om Windows te implementeren zonder gebruik van het netwerk](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
