---
title: PXE voor OSD via het netwerk gebruiken
titleSuffix: Configuration Manager
description: Met PXE geïnitieerde besturingssysteem implementaties gebruiken om het besturings systeem van een computer te vernieuwen of een nieuwe versie van Windows op een nieuwe computer te installeren.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d2d467a053689edad1dcf62fa9bb140d5f259d9
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124615"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>PXE gebruiken om Windows via het netwerk te implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met PXE (Preboot Execution Environment) geïnitieerde besturingssysteem implementaties in Configuration Manager kunnen clients besturings systemen via het netwerk aanvragen en implementeren. Voor deze implementatie methode verzendt u de installatie kopie van het besturings systeem en de opstart installatie kopieën naar een distributie punt met PXE-functionaliteit.

> [!NOTE]
> Wanneer u een besturingssysteem implementatie maakt die alleen is gericht op x64 BIOS-computers, moeten zowel de x64-opstart installatie kopie als de x86-opstart installatie kopie beschikbaar zijn op het distributie punt.

U kunt met PXE geïnitieerde besturingssysteem implementaties gebruiken in de volgende scenario's:

- [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)

Voer de stappen in een van de implementatie scenario's voor besturings systemen uit en gebruik de secties in dit artikel om voor te bereiden op door PXE geïnitieerde implementaties.

> [!WARNING]
> Als u PXE-implementaties gebruikt en de hardware van het apparaat configureert met de netwerk adapter als het eerste opstart apparaat, kunnen deze apparaten automatisch een taken reeks voor besturingssysteem implementatie starten zonder tussen komst van de gebruiker. Deze configuratie wordt niet beheerd door [implementatie verificatie](../../core/servers/manage/settings-to-manage-high-risk-deployments.md) . Hoewel deze configuratie het proces kan vereenvoudigen en de gebruikers interactie vermindert, wordt het apparaat voor een groter risico voor onbedoelde herinstallatie kopieën geplaatst.

Met ingang van versie 2006 kunnen op PXE gebaseerde taken reeksen inhoud op basis van de cloud downloaden. Het distributie punt met PXE-functionaliteit vereist nog steeds de opstart installatie kopie en het apparaat heeft een intranet verbinding met het beheer punt nodig. Vervolgens kan er extra inhoud worden ontvangen van een CMG (Cloud Management Gateway) of een Cloud distributiepunt.<!--6209223--> Zie [ondersteuning voor Cloud inhoud](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content)voor meer informatie.

## <a name="configure-distribution-points-for-pxe"></a><a name="BKMK_Configure"></a>Distributie punten voor PXE configureren

Als u besturings systemen wilt implementeren om clients te Configuration Manager die PXE-opstart aanvragen maken, configureert u een of meer distributie punten om PXE-aanvragen te accepteren. Vervolgens reageert het distributie punt op PXE-opstart aanvragen en bepaalt de juiste implementatie actie. Zie voor meer informatie [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).

> [!NOTE]
> Wanneer u één distributie punt met PXE-functionaliteit configureert voor ondersteuning van meerdere subnetten, wordt het niet ondersteund voor het gebruik van DHCP-opties. Configureer IP-helpers op de routers om het netwerk toe te staan PXE-aanvragen van clients naar distributie punten met PXE-functionaliteit door te sturen.

In versie 1810 wordt niet ondersteund voor het gebruik van de PXE-responder zonder WDS op servers waarop ook een DHCP-server wordt uitgevoerd.

Vanaf versie 1902, wanneer u een PXE-responder inschakelt op een distributie punt zonder Windows Deployment-service, kan het zich nu op dezelfde server bevinden als de DHCP-service.<!--3734270, SCCMDocs-pr #3416--> Voeg de volgende instellingen toe ter ondersteuning van deze configuratie:

- Stel de DWord- **DoNotListenOnDhcpPort** waarde DoNotListenOnDhcpPort `1` in op in de volgende register sleutel: `HKLM\Software\Microsoft\SMS\DP` .
- Stel de DHCP-optie 60 in op `PXEClient` .
- Start de SCCMPXE-en DHCP-services op de server opnieuw op.

## <a name="prepare-a-pxe-enabled-boot-image"></a>Een opstartinstallatiekopie die geschikt is voor gebruik met PXE voorbereiden

Als u PXE wilt gebruiken om een besturings systeem te implementeren, distribueert u zowel x86-als x64-opstart installatie kopieën met PXE-functionaliteit naar een of meer distributie punten met PXE-functionaliteit.

- Selecteer **deze opstart installatie kopie implementeren vanaf het distributie punt met PXE-functionaliteit** op het tabblad **gegevens bron** in de eigenschappen van de opstart installatie kopie om PXE in te scha kelen op een opstart installatie kopie.

- Wanneer u de eigenschappen van de opstart installatie kopie wijzigt, moet u de opstart installatie kopie bijwerken en opnieuw distribueren naar distributie punten. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

## <a name="manage-duplicate-hardware-identifiers"></a>Dubbele hardware-id's beheren

Configuration Manager herkent mogelijk meerdere computers als hetzelfde apparaat als ze dubbele SMBIOS-kenmerken hebben of als u een gedeelde netwerk adapter gebruikt. Verminder deze problemen door dubbele hardware-id's in hiërarchie-instellingen te beheren. Zie [dubbele hardware-Id's beheren](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers)voor meer informatie.

## <a name="create-an-exclusion-list-for-pxe-deployments"></a><a name="BKMK_PXEExclusionList"></a> Een uitsluitingslijst voor PXE-implementaties maken

> [!NOTE]
> In sommige gevallen kan het proces voor het [beheren van dubbele hardware-id's](../../core/clients/manage/manage-clients.md#manage-duplicate-hardware-identifiers) eenvoudiger zijn.<!-- SCCMDocs issue 802 -->
>
> Het gedrag van elk kan in sommige scenario's verschillende resultaten veroorzaken. De uitsluitings lijst start nooit een client met het vermelde MAC-adres, ongeacht wat.
>
> De lijst met dubbele ID'S maakt geen gebruik van het MAC-adres om het taken reeks beleid voor een client te vinden. Als deze overeenkomt met de SMBIOS-ID of als er een taken reeks beleid is voor onbekende computers, wordt de client nog steeds opgestart.

Wanneer u besturings systemen met PXE implementeert, kunt u op elk distributie punt een uitsluitings lijst maken. Voeg de MAC-adressen toe aan de uitsluitings lijst van de computers die u door het distributie punt wilt laten negeren. De vermelde computers ontvangen geen implementatie taken reeksen die Configuration Manager gebruikt voor de PXE-implementatie.

1. Maak een tekst bestand op het distributie punt met PXE-functionaliteit. Geef bijvoorbeeld het bestand de naam **pxeExceptions.txt**.

1. Gebruik een tekst editor, zoals Klad blok, om het bestand te bewerken. Voeg de MAC-adressen toe van de computers die door het distributie punt met PXE-functionaliteit moeten worden genegeerd. Scheid de MAC-adressen met een dubbele punt van elkaar en geef elk adres op een aparte regel op. Bijvoorbeeld: `01:23:45:67:89:ab`

1. Sla het tekst bestand op het distributie punt met PXE-functionaliteit op. U kunt deze opslaan op elke locatie op de server.

1. Bewerk het REGI ster op het distributie punt met PXE-functionaliteit. Blader naar het volgende registerpad: `HKLM\Software\Microsoft\SMS\DP` . Maak een teken reeks waarde van **MACIgnoreListFile** . Voeg het volledige pad toe aan het tekst bestand op het distributie punt met PXE-functionaliteit.

    > [!WARNING]
    > Als u de REGI ster-editor onjuist gebruikt, kunt u ernstige problemen veroorzaken waarvoor u mogelijk Windows opnieuw moet installeren. Micro soft kan niet garanderen dat u problemen kunt oplossen die het gevolg zijn van een onjuist gebruik van de REGI ster-editor. Gebruik de Registry Editor op eigen risico.

1. Nadat u deze wijziging in het REGI ster hebt aangebracht, start u de WDS-service of de PXE-responder-service opnieuw. U hoeft de server niet opnieuw op te starten.<!--512129-->

## <a name="ramdisk-tftp-block-size-and-window-size"></a><a name="BKMK_RamDiskTFTP"></a>RamDisk TFTP-blok grootte en venster grootte

U kunt de RamDisk TFTP-blok-en venster grootten aanpassen voor distributie punten met PXE-functionaliteit. Als u uw netwerk hebt aangepast, kan het downloaden van de opstart installatie kopie mislukken met een time-outfout vanwege een grote blok-of venster grootte. Met de aanpassingen van het RamDisk TFTP-blok en de venster grootte kunt u TFTP-verkeer optimaliseren wanneer u PXE gebruikt om te voldoen aan uw specifieke netwerk vereisten. Test de aangepaste instellingen in uw omgeving om te bepalen welke configuratie het meest efficiënt is. Zie voor meer informatie [de ramdisk TFTP-blok grootte en de venster grootte aanpassen op distributie punten met PXE-functionaliteit](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Implementatie-instellingen configureren

Als u een door PXE geïnitieerde besturingssysteem implementatie wilt gebruiken, moet u de implementatie configureren om het besturings systeem beschikbaar te maken voor PXE-opstart aanvragen. Configureer beschik bare besturings systemen op het tabblad **implementatie-instellingen** in de implementatie-eigenschappen. Selecteer een van de volgende opties voor de instelling **beschikbaar maken voor de volgende** :

- Configuration Manager-clients, media en PXE

- Alleen media en PXE

- Alleen media en PXE (verborgen)

## <a name="option-82-during-pxe-dhcp-handshake"></a>Optie 82 tijdens PXE DHCP-Handshake

Vanaf versie 1906 ondersteunt Configuration Manager optie 82 tijdens de PXE DHCP-Handshake met de PXE-responder zonder WDS. Als u optie 82 nodig hebt, moet u ervoor zorgen dat u de PXE-responder zonder WDS gebruikt. Configuration Manager biedt geen ondersteuning voor optie 82 met WDS.

## <a name="deploy-the-task-sequence"></a><a name="BKMK_Deploy"></a> De takenreeks implementeren

Implementeer het besturings systeem in een doel verzameling. Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie. Wanneer u besturingssystemen met PXE implementeert, kunt u configureren of de implementatie vereist of beschikbaar is.

- **Vereiste implementatie**: bij vereiste implementaties wordt PXE gebruikt zonder tussen komst van de gebruiker. De gebruiker kan de PXE-opstart actie niet overs Laan. Als de gebruiker de PXE-opstart bewerking echter annuleert voordat het distributie punt reageert, wordt het besturings systeem niet geïmplementeerd.

- **Beschik bare implementatie**: voor beschik bare implementaties moet de gebruiker aanwezig zijn op de doel computer. Een gebruiker moet op de **F12** -toets drukken om door te gaan met het PXE-opstart proces. Als een gebruiker niet aanwezig is om op **F12**te drukken, wordt de computer opgestart met het huidige besturings systeem of vanaf het volgende beschik bare opstart apparaat.

U kunt een vereiste PXE-implementatie opnieuw implementeren door de status te wissen van de laatste PXE-implementatie die is toegewezen aan een Configuration Manager verzameling of een computer. Zie [clients beheren](../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) of [verzamelingen beheren](../../core/clients/manage/collections/manage-collections.md#bkmk_device)voor meer informatie over de vereiste actie voor het wissen van een **PXE-implementatie** . Met deze actie wordt de status van die implementatie opnieuw ingesteld en worden de meest recente vereiste implementaties opnieuw geïnstalleerd.

> [!IMPORTANT]
> Het PXE-protocol is niet beveiligd. Zorg ervoor dat de PXE-server en de PXE-client zich op een fysiek beveiligd netwerk, zoals in een Data Center, bevinden om onbevoegde toegang tot uw site te voor komen.

## <a name="how-the-boot-image-is-selected-for-pxe"></a>Hoe de opstart installatie kopie wordt geselecteerd voor PXE

Wanneer een client opstart met PXE, biedt Configuration Manager de client een opstart installatie kopie die moet worden gebruikt. Configuration Manager maakt gebruik van een opstart installatie kopie met een exact overeenkomende architectuur. Als er geen opstart installatie kopie met de exacte architectuur beschikbaar is, gebruikt Configuration Manager een opstart installatie kopie met een compatibele architectuur.

De volgende lijst bevat informatie over de manier waarop een opstart installatie kopie wordt geselecteerd voor clients die opstarten met PXE:  

1. Configuration Manager zoekt in de site database naar de systeem record die overeenkomt met het MAC-adres of SMBIOS van de client die probeert op te starten.  

    > [!NOTE]  
    > Als een computer die is toegewezen aan een site wordt opgestart naar PXE voor een andere site, zijn de beleids regels niet zichtbaar voor de computer. Als er bijvoorbeeld al een client is toegewezen aan site A, hebben het beheer punt en distributie punt voor site B geen toegang tot de beleids regels van site A. De client kan niet worden opgestart met een PXE-opstart bewerking.  

2. Configuration Manager zoekt naar taken reeksen die zijn geïmplementeerd in de systeem record die is gevonden in stap 1.  

3. In de lijst met taken reeksen gevonden in stap 2, Configuration Manager zoekt naar een opstart installatie kopie die overeenkomt met de architectuur van de client die probeert op te starten. Als er een opstart installatie kopie met dezelfde architectuur wordt gevonden, wordt die opstart installatie kopie gebruikt.  

    Als er meer dan één opstart installatie kopie wordt gevonden, wordt de *hoogste* of meest recente taken reeks implementatie-id gebruikt. In het geval van een hiërarchie met meerdere sites heeft de site van de *hogere* letter voor rang op de vergelijking van de teken reeks. Als ze bijvoorbeeld beide overeenkomen, wordt een jaar-oud-implementatie vanaf site ZZZ geselecteerd via de implementatie van gisteren van site AAA.<!-- SCCMDocs issue 877 -->  

4. Als er geen opstart installatie kopie met dezelfde architectuur wordt gevonden, zoekt Configuration Manager naar een opstart installatie kopie die compatibel is met de architectuur van de client. Er wordt gezocht in de lijst met taken reeksen die u in stap 2 hebt gevonden. Een 64-bits BIOS/MBR-client is bijvoorbeeld compatibel met 32-bits en 64-bits opstart installatie kopieën. Een 32-bits BIOS/MBR-client is compatibel met alleen 32-bits opstart installatie kopieën. UEFI-clients zijn alleen compatibel met de overeenkomende architectuur. Een 64-bits UEFI-client is compatibel met alleen 64-bits opstart installatie kopieën en een 32-bits UEFI-client is compatibel met alleen 32-bits opstart installatie kopieën.

## <a name="next-steps"></a>Volgende stappen

[Gebruikerservaring voor implementatie van besturingssysteem](../understand/user-experience.md#pxe)
