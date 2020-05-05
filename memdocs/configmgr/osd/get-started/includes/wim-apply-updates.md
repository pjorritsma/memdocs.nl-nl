---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 05/28/2019
ms.openlocfilehash: e5c15556a7a8dd91db3ae2c4aa4f9830abc8e430
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724109"
---
## <a name="apply-software-updates-to-an-image"></a><a name="BKMK_OSImagesApplyUpdates"></a>Software-updates Toep assen op een installatie kopie

> [!Note]  
> Deze sectie is van toepassing op **installatie kopieën van het besturings systeem** en upgrade pakketten van het **besturings systeem**. De algemene term ' afbeelding ' wordt gebruikt om te verwijzen naar het Windows-installatie kopie bestand (WIM). Beide objecten hebben een WIM-bestand, dat installatie bestanden van Windows bevat. Software-updates zijn in beide objecten van toepassing op deze bestanden. Het gedrag van dit proces is hetzelfde voor beide objecten.  

Elke maand zijn er nieuwe software-updates die van toepassing zijn op de installatie kopie. Voordat u software-updates kunt Toep assen, moet u aan de volgende vereisten voldoen:

- Een infra structuur voor software-updates  
- De software-updates zijn gesynchroniseerd  
- De software-updates zijn gedownload naar de inhouds bibliotheek op de site server  

Zie [software-updates implementeren](../../../sum/deploy-use/deploy-software-updates.md)voor meer informatie.  

Toepasselijke software-updates Toep assen op een installatie kopie volgens een opgegeven planning. Dit proces wordt ook wel *offline onderhoud*genoemd. In dit schema past Configuration Manager de geselecteerde software-updates toe op de installatie kopie. De bijgewerkte installatie kopie kan vervolgens ook opnieuw worden gedistribueerd naar distributie punten.

> [!Important]  
> Hoewel u alle software-updates kunt selecteren die van toepassing zijn op de installatie kopie op basis van versie, kan DISM alleen bepaalde typen updates Toep assen op de installatie kopie. In het bestand **OfflineServicingMgr. log** wordt de volgende vermelding `Not applying this update binary, it is not supported`weer gegeven:.<!-- SCCMDocs issue 1324 -->

De site database bevat informatie over de installatie kopie, inclusief de software-updates die zijn toegepast op het moment van de import. Software-updates die u op de installatie kopie toepast sinds deze voor het eerst werd toegevoegd, worden ook opgeslagen in de-site database. Wanneer u de wizard start om software-updates toe te passen, wordt er een lijst opgehaald met de toepasselijke software-updates die op de site nog niet op de installatie kopie zijn toegepast. Configuration Manager kopieert de software-updates die u selecteert uit de inhouds bibliotheek op de site server. Vervolgens worden de software-updates toegepast op de installatie kopie.  

### <a name="servicing-process"></a>Onderhouds proces

1. In de Configuration Manager-console gaat u naar de werk ruimte **software bibliotheek** , vouwt u **besturings systemen**uit en selecteert u **installatie kopieën van besturings** systemen of **upgrade pakketten voor besturings systemen**.  

2. Selecteer het object waarop u software-updates wilt Toep assen.  

3. Selecteer op het lint **updates plannen** om de wizard te starten.  

4. Selecteer op de pagina **updates kiezen** de software-updates die op de installatie kopie moeten worden toegepast. Het kan enige tijd duren voordat de lijst met updates wordt weer gegeven in de wizard. Gebruik het **filter** om naar teken reeksen in de meta gegevens te zoeken. Gebruik de vervolg keuzelijst **systeem architectuur** om te filteren op **x86**, **x64**of **alle**. U kunt één, veel of alle updates in de lijst selecteren. Wanneer u klaar bent met het selecteren van updates, selecteert u **volgende**.  

5. Geef, op de pagina **Schema instellen** , de volgende instellingen op, en klik vervolgens op **Volgende**.  

    1. **Schema**: Geef de planning op voor wanneer de site de software-updates op de installatie kopie toepast.  

    2. **Door gaan bij fout**: Selecteer deze optie om software-updates te blijven Toep assen op de installatie kopie, zelfs wanneer er een fout is opgetreden.  

    3. **Distributie punten bijwerken met de installatie kopie**: Selecteer deze optie om de installatie kopie op distributie punten bij te werken nadat de site de software-updates heeft toegepast.  

6. Voltooi de wizard updates plannen.  

> [!NOTE]  
> Om de payload-grootte te minimaliseren, wordt de oudere versie verwijderd door het onderhoud van besturingssysteem upgrade pakketten en installatie kopieën van besturings systemen.  

### <a name="servicing-operations"></a>Onderhouds bewerkingen

Voeg in de Configuration Manager-console in het knoop punt **installatie kopieën van besturings systeem** of **OS-upgrade pakketten** de volgende kolommen toe aan de weer gave:

- **Datum van geplande updates**: met deze eigenschap wordt het volgende schema weer gegeven dat u hebt gedefinieerd.  
- **Status van geplande updates**: met deze eigenschap wordt de status weer gegeven. Bijvoorbeeld **geslaagd** of **in verwerking**.  

Selecteer een specifiek afbeeldings object en schakel vervolgens over naar het tabblad **update status** in het detail venster. Op dit tabblad wordt de lijst met updates in de installatie kopie weer gegeven.

Selecteer een specifiek afbeeldings object en selecteer **Eigenschappen** in het lint. Op het tabblad **geïnstalleerde updates** wordt de lijst met updates in de installatie kopie weer gegeven. Het tabblad **onderhoud** is een alleen-lezen weer gave van de huidige onderhouds planning en de updates die u wilt Toep assen.

Wanneer de status wordt **uitgevoerd**, kunt u **geplande updates annuleren** selecteren op het lint. Met deze actie wordt het actieve onderhouds proces geannuleerd.

Als u dit proces wilt oplossen, bekijkt u de bestanden **OfflineServicingMgr. log** en **DISM. log** op de site server. Zie [logboek bestanden](../../../core/plan-design/hierarchy/log-files.md)voor meer informatie.

### <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_servicing-drive"></a>Het station opgeven voor offline-installatie kopie onderhoud van besturings systemen

<!--1358924-->

Geef vanaf versie 1810 het station op dat Configuration Manager gebruikt tijdens het offline onderhoud van installatie kopieën van het besturings systeem. Dit proces kan een grote hoeveelheid schijf ruimte in beslag nemen met tijdelijke bestanden. Deze optie geeft u de flexibiliteit om het te gebruiken station te selecteren.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer het knoop punt **sites** . Klik in het lint op **site onderdelen configureren** en selecteer **implementatie van besturings systeem**.  

2. Geef op het tabblad **offline onderhoud** de optie op voor **een lokaal station dat moet worden gebruikt door offline onderhoud van installatie kopieën**.  

Deze instelling is standaard **automatisch**. Met deze waarde Configuration Manager selecteert u het station waarop het is geïnstalleerd.

Als u een station selecteert dat niet bestaat op de site server, Configuration Manager zich hetzelfde als wanneer u **automatisch**selecteert.

Tijdens offline onderhoud slaat Configuration Manager tijdelijke bestanden op in de map `<drive>:\ConfigMgr_OfflineImageServicing`. Ook wordt de installatie kopie van het besturings systeem in deze map gekoppeld.

### <a name="optimized-image-servicing"></a><a name="bkmk_resetbase"></a>Geoptimaliseerde installatie kopie onderhoud

<!--3555951-->

Vanaf versie 1902, wanneer u software-updates toepast op een installatie kopie van het besturings systeem, is er een nieuwe optie voor het optimaliseren van de uitvoer door vervangen updates te verwijderen. De optimalisatie van offline onderhoud is alleen van toepassing op installatie kopieën met één index.

Wanneer u de site plant om software-updates toe te passen op een installatie kopie van een besturings systeem, wordt het opdracht regel programma Windows Deployment Image Servicing and Management (DISM) gebruikt. Tijdens het onderhouds proces worden de volgende twee extra stappen door deze wijziging geïntroduceerd:  

- DISM wordt uitgevoerd op basis van de gekoppelde offline-installatie `/Cleanup-Image /StartComponentCleanup /ResetBase`kopie met de para meters. Als deze opdracht mislukt, mislukt het huidige onderhouds proces. Wijzigingen in de installatie kopie worden niet doorgevoerd.  

- Nadat Configuration Manager wijzigingen in de installatie kopie heeft doorgevoerd en deze ontkoppelt van het bestands systeem, wordt de installatie kopie naar een ander bestand geëxporteerd. Deze stap maakt gebruik van de `/Export-Image`DISM-para meter. Hiermee verwijdert u overbodige bestanden van de installatie kopie, waardoor de grootte wordt verminderd.  

Micro soft raadt u aan om regel matig updates toe te passen op uw offline-installatie kopieën. U hoeft deze optie niet altijd te gebruiken wanneer u een installatie kopie service. Wanneer u dit proces elke maand doet, kunt u met deze nieuwe optie het beste profiteren van het voor deel van de tijd. Zie voor meer informatie [aanbevelingen voor de stap software-updates installeren](../../understand/install-software-updates.md#recommendations).

Deze optie helpt de totale grootte van de service kopie te reduceren. het duurt langer om het proces te volt ooien. Gebruik de wizard om onderhoud te plannen tijdens handige tijden. Daarnaast is extra opslag ruimte op de site server vereist. U kunt de site aanpassen voor het gebruik van een alternatieve locatie. Zie [het station opgeven voor offline-installatie kopieën van besturings systemen](#bkmk_servicing-drive)voor meer informatie.

#### <a name="process-to-optimize-image-servicing"></a>Proces voor het optimaliseren van installatie kopie onderhoud

1. Start het [onderhouds proces](#servicing-process).  

2. Selecteer op de pagina **schema instellen** de optie om **vervangen updates te verwijderen nadat de installatie kopie is bijgewerkt**. Deze optie is niet automatisch ingeschakeld. Als de afbeelding meer dan één index heeft, kunt u deze optie niet gebruiken.  

3. Voltooi de wizard om de installatie kopie te onderhoud te plannen.  

Valideer en controleer het proces met behulp van **OfflineServicing. log**.
