---
title: Installatiekopieën van besturingssysteem beheren
titleSuffix: Configuration Manager
description: Meer informatie over de methoden voor het beheren van besturingssysteem installatie kopieën die zijn opgeslagen in WIM-bestanden (Windows-installatie kopie).
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2f8b8a45ff83ce903f5737c94144e6ca5ab50826
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697650"
---
# <a name="manage-os-images-with-configuration-manager"></a>Installatie kopieën van besturings systemen beheren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Installatie kopieën van besturings systemen in Configuration Manager worden opgeslagen in de WIM-bestands indeling (Windows-installatie kopie). Deze installatie kopieën zijn een gecomprimeerde verzameling referentie bestanden en mappen gebruiken om een nieuw besturings systeem op een computer te installeren en te configureren. Bij veel implementatie scenario's voor besturings systemen is een installatie kopie van het besturings systeem vereist.


## <a name="os-image-types"></a>Typen installatie kopieën van besturings systemen

U kunt een [standaard installatie kopie van het besturings systeem](#default-image)gebruiken of de installatie kopie van het besturings systeem bouwen op een [referentie computer](#bkmk_capture) die u configureert. Wanneer u de referentie computer bouwt, voegt u besturingssysteem bestanden, stuur Programma's, ondersteunings bestanden, software-updates, hulpprogram ma's en toepassingen toe aan het besturings systeem. Vervolgens legt u deze vast om het installatie kopie bestand te maken.

### <a name="default-image"></a>Standaardinstallatiekopie

De Windows-installatie bestanden bevatten de standaard installatie kopie van het besturings systeem. Deze installatie kopie is een basis installatie kopie van het besturings systeem die een standaardset Stuur Programma's bevat. Wanneer u de standaard installatie kopie van het besturings systeem gebruikt, kunt u met taken reeks stappen apps installeren en andere configuraties uitvoeren nadat het besturings systeem op een apparaat is geïnstalleerd. Zoek de standaard installatie kopie van het besturings systeem in de Windows-bron bestanden: `\Sources\install.wim` .  

#### <a name="default-image-advantages"></a>Voor delen standaard afbeelding

- De grootte van de installatiekopie is kleiner dan die van een vastgelegde installatiekopie.  

- Het installeren van apps en configuraties met taken reeks stappen is dynamischer. Wijzig bijvoorbeeld de configuraties en apps die in de taken reeks worden geïnstalleerd, zonder dat u de installatie kopie van het apparaat hoeft te wijzigen.  

#### <a name="default-image-disadvantages"></a>Nadelen van standaard afbeelding

- De installatie van het besturings systeem kan meer tijd in beslag nemen. De installatie van de toepassing en andere configuraties worden uitgevoerd nadat de installatie van het besturings systeem is voltooid.  


### <a name="captured-image-from-a-reference-computer"></a><a name="bkmk_capture"></a> Vastgelegde installatie kopie van een referentie computer

Als u een aangepaste installatie kopie van het besturings systeem wilt maken, bouwt u een referentie computer met het gewenste besturings systeem. Installeer vervolgens toepassingen en Configureer instellingen. Leg de installatie kopie van het besturings systeem van de referentie computer vast om het WIM-bestand te maken. Bouw de referentie computer hand matig op of gebruik een taken reeks om enkele of alle stappen van de build te automatiseren. Zie [installatie kopieën van besturings systemen aanpassen](customize-operating-system-images.md)voor meer informatie.  

#### <a name="captured-image-advantages"></a>Voor delen van vastgelegde afbeelding

- De installatie verloopt waarschijnlijk sneller dan wanneer u de standaardinstallatiekopie gebruikt. Toepassingen kunnen bijvoorbeeld vooraf worden geïnstalleerd met de vastgelegde installatie kopie van het besturings systeem. Vervolgens hoeft u deze toepassingen niet later te installeren met behulp van taken reeks stappen.  

#### <a name="captured-image-disadvantages"></a>Nadelen van vastgelegde afbeelding

- De grootte van de installatie kopie is mogelijk groter dan de standaard installatie kopie.  

- U moet een nieuwe installatie kopie maken wanneer u updates voor toepassingen en hulpprogram ma's nodig hebt.  


## <a name="add-an-os-image"></a><a name="BKMK_AddOSImages"></a> Een installatie kopie van een besturings systeem toevoegen  

Voordat u een installatie kopie van het besturings systeem kunt gebruiken, moet u deze toevoegen aan uw Configuration Manager-site.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **installatie kopieën van het besturings systeem** .  

2. Klik op het tabblad **Start** van het lint in de groep **maken** op **installatie kopie van besturings systeem toevoegen**. Met deze actie wordt de wizard Installatie kopie van besturings systeem toevoegen gestart.  

3. Geef op de pagina **gegevens bron** de volgende informatie op:

    - Netwerkpad **naar het** installatie kopie bestand van het besturings systeem. Bijvoorbeeld `\\server\share\path\image.wim`.

    - **Extraheer een specifieke installatie kopie-index uit het opgegeven Wim-bestand** en selecteer vervolgens een installatie kopie-index in de lijst.<!--3719699--> Vanaf versie 1902 wordt met deze optie automatisch één index geïmporteerd in plaats van alle afbeeldings indexen in het bestand. Als u deze optie gebruikt, resulteert dit in een kleiner afbeeldings bestand en snellere offline onderhoud. Het ondersteunt ook het proces voor het [optimaliseren van installatie kopieën](#bkmk_resetbase)voor een kleiner installatie kopie bestand na het Toep assen van software-updates.  

        > [!Note]  
        > Configuration Manager wijzigt het bron installatie kopie bestand niet. Er wordt een nieuw afbeeldings bestand gemaakt in dezelfde bron directory.
        >
        > Dit uitpak proces kan mislukken voor extreem grote afbeeldings bestanden, bijvoorbeeld meer dan 60 GB. De DISM-fout is `Not enough storage is available to process this command.` de opdracht regel die Configuration Manager gebruikt, bevindt zich in de smsprov. log en DISM. log. Voer dezelfde opdracht hand matig uit en importeer vervolgens de installatie kopie.<!-- SCCMDocs-pr issue 3502 -->  

    - Vanaf versie 1906 kunt u de **architectuur** en **taal** van de installatie kopie opgeven als u inhoud vooraf in de cache wilt opslaan op een client. Zie [inhoud vooraf in cache configureren](../deploy-use/configure-precache-content.md)voor meer informatie.<!--4224642-->  

4. Geef op de pagina **Algemeen** de volgende informatie op. Deze informatie is nuttig voor identificatie doeleinden wanneer u meer dan één installatie kopie van het besturings systeem hebt.  

    - **Naam**: een unieke naam voor de installatie kopie. De naam is standaard afkomstig uit de naam van het WIM-bestand.  

    - **Versie**: een optionele versie-id. Deze eigenschap hoeft niet de versie van het besturings systeem van de installatie kopie te zijn. Het is vaak de versie van uw organisatie voor het pakket.  

    - **Opmerking**: een optionele korte beschrijving.  

5. Voltooi de wizard.  

Zie [New-CMOperatingSystemImage](/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps)voor het equivalent van de Power shell-cmdlet van deze console wizard.

Distribueer vervolgens de installatie kopie van het besturings systeem naar distributie punten.  


## <a name="distribute-content-to-distribution-points"></a><a name="BKMK_DistributeBootImages"></a> Inhoud distribueren naar distributie punten  

Distribueer installatie kopieën van het besturings systeem naar distributie punten die hetzelfde zijn als andere inhoud. Voordat u de taken reeks implementeert, distribueert u de installatie kopie van het besturings systeem naar ten minste één distributie punt. Zie voor meer informatie [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  


[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]


## <a name="prepare-the-os-image-for-multicast-deployments"></a><a name="BKMK_OSImageMulticast"></a> De installatie kopie van het besturings systeem voorbereiden voor multi cast-implementaties  

Multi cast-implementaties gebruiken om ervoor te zorgen dat meerdere computers tegelijkertijd een installatie kopie van het besturings systeem downloaden. De installatie kopie is multi cast naar clients op het distributie punt, in plaats van dat elke client een kopie van de installatie kopie downloadt van het distributie punt over een afzonderlijke verbinding. Wanneer u de implementatie methode voor het besturings systeem kiest voor het [gebruik van multi cast om Windows via het netwerk te implementeren](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), moet u de installatie kopie van het besturings systeem configureren voor multi cast. Distribueer de installatie kopie vervolgens naar een multi cast-distributie punt.

1. Ga in de Configuration Manager-console naar de werk ruimte **software bibliotheek** , vouw **besturings systemen**uit en selecteer vervolgens het knoop punt **installatie kopieën van het besturings systeem** .  

2. Selecteer de installatie kopie van het besturings systeem die u wilt distribueren naar een multi cast-distributie punt.  

3. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.  

4. Ga naar het tabblad **distributie-instellingen** en configureer de volgende opties:  

    - **Toestaan dat dit pakket kan worden overgedragen via multi cast (alleen WinPE)**: Selecteer deze optie om de installatie kopieën van het besturings systeem tegelijkertijd te implementeren met behulp Configuration Manager van multi cast.  

    - **Multi cast-pakketten versleutelen**: Hiermee geeft u op of de site de installatie kopie versleutelt voordat deze wordt verzonden naar het distributie punt. Als de installatie kopie gevoelige informatie bevat, gebruikt u deze optie. Als de installatie kopie niet is versleuteld, is de inhoud ervan zichtbaar in ongecodeerde tekst in het netwerk. Vervolgens kan een niet-gemachtigde gebruiker de inhoud van de installatie kopie onderscheppen en weer geven.  

    - **Dit pakket alleen overdragen via multicast**: hiermee geeft u aan dat de installatiekopie alleen tijdens een multicastsessie door het distributiepunt mag worden geïmplementeerd.  

         Als u **Dit pakket alleen overdragen via multi cast**selecteert, moet u ook de optie voor de implementatie van taken reeksen opgeven om **inhoud lokaal te downloaden wanneer dit nodig is voor de taken reeks die wordt uitgevoerd**. Zie [Een takenreeks implementeren](../deploy-use/deploy-a-task-sequence.md)voor meer informatie.  

5. Selecteer **OK** om de instellingen op te slaan en de eigenschappen van de installatie kopie te sluiten.