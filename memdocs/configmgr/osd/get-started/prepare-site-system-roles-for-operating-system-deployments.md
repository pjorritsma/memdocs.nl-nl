---
title: Site systeem rollen voorbereiden voor OSD
titleSuffix: Configuration Manager
description: Configureer de site systeem rollen voordat u besturings systemen implementeert in Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1beec2f5ef7b6da9f1f093300ec6c2b239e7396e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724053"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Site systeem rollen voorbereiden voor besturingssysteem implementaties met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voor het implementeren van besturings systemen in Configuration Manager moet u eerst de volgende site systeem rollen voorbereiden die specifieke configuraties en overwegingen vereisen.



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a>Distributie punten  

De site systeemrol van het distributie punt bevat bron bestanden die clients kunnen downloaden. Deze inhoud is voor toepassingen, software-updates, installatie kopieën van besturings systemen, opstart installatie kopieën en stuur programmapakketten. Distributie van inhoud beheren door gebruik te maken van band breedte, bandbreedte beperking en plannings opties.  

Het is belang rijk dat u over voldoende distributie punten beschikt ter ondersteuning van de implementatie van besturings systemen op computers. Het is ook belang rijk dat u de plaatsing van deze distributie punten in uw hiërarchie plant. Zie [inhoud en infra structuur voor inhoud beheren](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)voor meer informatie. Dit artikel bevat enkele aanvullende plannings overwegingen voor distributie punten die specifiek zijn voor de implementatie van het besturings systeem.  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a>Aanvullende plannings overwegingen voor distributie punten  

De volgende items zijn aanvullende plannings overwegingen voor distributie punten:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Hoe kan ik ongewenste besturingssysteem implementaties voor komen?  
Configuration Manager maakt geen onderscheid tussen site servers en andere doel computers in een verzameling. Als u een vereiste taken reeks implementeert voor een verzameling die een site server bevat, wordt de taken reeks op dezelfde manier uitgevoerd als andere computers in de verzameling. Zorg ervoor dat de implementatie van het besturings systeem gebruikmaakt van een verzameling die de bedoelde clients bevat.  

Het gedrag voor implementaties van taken reeksen met een hoog risico beheren. Een implementatie met een hoog risico wordt automatisch op een client geïnstalleerd en heeft de potentie om ongewenste resultaten te veroorzaken. Bijvoorbeeld een taken reeks met het doel vereist voor het implementeren van een besturings systeem. Als u het risico van een implementatie met een ongewenst hoog risico wilt beperken, moet u de instellingen voor verificatie van de implementatie configureren. Zie [instellingen voor het beheren van implementaties met een hoog risico](../../core/servers/manage/settings-to-manage-high-risk-deployments.md)voor meer informatie.  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Hoeveel computers kunnen een installatie kopie van het besturings systeem op één keer van één distributie punt ontvangen?  
Als u wilt schatten hoeveel distributie punten u nodig hebt, moet u rekening houden met de volgende variabelen:  
- De verwerkings snelheid van het distributie punt
- De schijf snelheid van het distributie punt
- De beschik bare band breedte op het netwerk
- De grootte van het installatie kopie pakket   
  
Als u bijvoorbeeld geen rekening houdt met andere factoren voor Server bronnen, is dit het maximum aantal computers dat in één uur een installatie kopie pakket van 4 GB kan verwerken op een Ethernet-netwerk van 100 MB per seconde 11 computers.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Als u een besturings systeem moet implementeren op een specifiek aantal computers binnen een specifiek tijds bestek, distribueert u de installatie kopie naar een passend aantal distributie punten.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Kan ik een besturings systeem implementeren op een distributie punt?  
U kunt een besturings systeem implementeren op een distributie punt, maar de installatie kopie van het besturings systeem moet worden ontvangen van een ander distributie punt.  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> Distributiepunten configureren voor de acceptatie van PXE-aanvragen  

Als u besturings systemen wilt implementeren om clients te Configuration Manager die PXE-opstart aanvragen maken, configureert u een of meer distributie punten om PXE-aanvragen te accepteren. Zodra u het distributie punt configureert, reageert het op PXE-opstart aanvragen en bepaalt de juiste implementatie actie die moet worden uitgevoerd. Zie voor meer informatie [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a>De RamDisk TFTP-blok-en venster grootte aanpassen op distributie punten met PXE-functionaliteit  

U kunt de RamDisk TFTP-blok-en venster grootten aanpassen voor distributie punten met PXE-functionaliteit. Als u uw netwerk hebt aangepast, kan het downloaden van de opstart installatie kopie mislukken met een time-outfout vanwege een grote blok-of venster grootte. Met de aanpassingen van het RamDisk TFTP-blok en de venster grootte kunt u TFTP-verkeer optimaliseren wanneer u PXE gebruikt om te voldoen aan uw specifieke netwerk vereisten. Test de aangepaste instellingen in uw omgeving om te bepalen welke configuratie het meest efficiënt is.  

-   **TFTP-blok grootte**: de blok grootte is de grootte van de gegevens pakketten die de server verzendt naar de client die het bestand downloadt. Met een groter blok kan de server minder pakketten verzenden, waardoor er minder trajectvertraging optreedt tussen de server en de client. Een grote blok grootte leidt echter tot gefragmenteerde pakketten, die de meeste PXE-client implementaties niet ondersteunen.  

-   **TFTP-venstergrootte**: TFTP vereist een bevestigingspakket (ACK) voor elk gegevensblok dat wordt verzonden. De server verzendt het volgende blok in de reeks pas wanneer het ACK-pakket van het vorige blok is ontvangen. Met TFTP-venster kunt u definiëren hoeveel gegevens blokken er worden gebruikt voor het vullen van een venster. De server verzendt de gegevensblokken achter elkaar door tot het venster is gevuld. Daarna verzendt de client een ACK-pakket. Als u dit venster groter maakt, vermindert het het aantal vertragings vertragingen tussen de client en de server en wordt de totale vereiste tijd voor het downloaden van een opstart installatie kopie verlaagd.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>De grootte van het RamDisk TFTP-venster wijzigen  
Als u de grootte van het RamDisk TFTP-venster wilt aanpassen, voegt u de volgende register sleutel toe aan distributie punten met PXE-functionaliteit:  

- **Locatie**:`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Naam**: RamDiskTFTPWindowSize  
- **Type**: REG_DWORD  
- **Waarde**: (aangepaste venster grootte)  
    - De standaard waarde is **1** (één gegevens blok vult het venster in).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Wijzig de RamDisk TFTP-blok grootte  
Als u de grootte van het RamDisk TFTP-venster wilt aanpassen, voegt u de volgende register sleutel toe aan distributie punten met PXE-functionaliteit:  

- **Locatie**:`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Naam**: RamDiskTFTPBlockSize  
- **Type**: REG_DWORD  
- **Waarde**: (aangepaste blok grootte)  
    - De standaard waarde is **4096**.  

> [!Note]  
> Zowel Windows Deployment Services als de Configuration Manager PXE-responder-service ondersteunen deze TFTP-configuraties.  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a>Distributie punten configureren voor de ondersteuning van multi cast  

Multi cast is een methode voor netwerk optimalisatie. Gebruik het op distributie punten wanneer meerdere clients tegelijkertijd dezelfde installatie kopie van het besturings systeem downloaden. Wanneer u multi cast gebruikt, kunnen meerdere computers tegelijkertijd de installatie kopie van het besturings systeem downloaden als multi cast door het distributie punt. Zonder multi cast verzendt het distributie punt een kopie van de gegevens naar elke client via een afzonderlijke verbinding. Zie [multi cast gebruiken om Windows via het netwerk te implementeren](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md)voor meer informatie.  

Voordat u het besturings systeem implementeert, moet u een distributie punt configureren voor de ondersteuning van multi cast. Zie [distributie punten installeren en configureren](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast)voor meer informatie.



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> Statusmigratiepunt  

In het status migratie punt worden gebruikers status gegevens opgeslagen die door USMT op één computer worden vastgelegd en vervolgens op een andere computer hersteld. Wanneer u echter gebruikers instellingen voor een besturingssysteem implementatie op dezelfde computer vastlegt, zoals een implementatie waarbij u Windows op de doel computer vernieuwt, kunt u kiezen of u de gegevens op dezelfde computer wilt opslaan door gebruik te maken van vaste koppelingen of een status migratie punt te gebruiken. Bij sommige computer implementaties maakt Configuration Manager automatisch een koppeling tussen het status archief en de doel computer wanneer u de status opslag maakt. Houd bij het plannen van het status migratie punt rekening met de volgende factoren:    


### <a name="user-state-size"></a>Grootte van de gebruikersstatus  

De grootte van de gebruikersstatus is direct van invloed op de schijfopslag op het statusmigratiepunt en de netwerkprestaties tijdens de migratie. Houd rekening met de grootte van de gebruikersstatus en het aantal computers dat moet worden gemigreerd. Houd ook rekening met de instellingen die vanaf de computer moeten worden gemigreerd. Als er bijvoorbeeld al een back-up van de map **Mijn documenten** is gemaakt op een server, hoeft u deze wellicht niet te migreren als onderdeel van de implementatie van de installatie kopie. Door onnodige migraties te voor komen, blijft de algehele grootte van de gebruikers status kleiner en wordt het effect verlaagd dat anders zou hebben op de netwerk prestaties en schijf opslag op het status migratie punt.  


### <a name="user-state-migration-tool"></a>Hulpprogramma voor migratie van gebruikersstatus  

Als u de gebruikers status wilt vastleggen en herstellen tijdens de implementatie van de besturings systemen, gebruikt u een Hulpprogramma voor migratie van gebruikersstatus (USMT)-pakket dat verwijst naar de USMT-bron bestanden. Configuration Manager maakt dit pakket automatisch in de Configuration Manager-console in **software bibliotheek** > **toepassings beheer** > **pakketten**. Configuration Manager gebruikt USMT 10 om de gebruikers status van het ene besturings systeem vast te leggen en vervolgens terug te zetten op een andere. De Windows Assessment and Deployment Kit (Windows ADK) voor Windows 10 bevat USMT 10.

Zie [algemene migratie scenario's](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios) in de Windows-documentatie voor een beschrijving van verschillende migratie SCENARIO'S voor USMT 10.  


### <a name="retention-policy"></a>Bewaarbeleid  

Wanneer u het status migratie punt configureert, geeft u de tijds duur op voor het behoud van de gebruikers status gegevens die worden opgeslagen. Hoe lang de gegevens op het statusmigratiepunt moeten worden bewaard, is afhankelijk van twee afwegingen:  

-   Het effect dat de opgeslagen gegevens hebben op de schijfopslag.  

-   Het mogelijke vereiste dat de gegevens bepaalde tijd moeten worden bewaard voor het geval dat u de gegevens nogmaals moet migreren.  
  
  
Status migratie vindt plaats in twee fasen: het vastleggen van de gegevens en het herstellen van de gegevens. Wanneer u de gegevens vastlegt, worden de gebruikersstatusgegevens verzameld en opgeslagen op het statusmigratiepunt. Wanneer u de gegevens herstelt, worden de gebruikersstatusgegevens van het statusmigratiepunt opgehaald en naar de doelcomputer geschreven. Met de stap **Statusopslag vrijgeven** uit de takenreeks worden de opgeslagen gegevens vervolgens vrijgegeven. Wanneer de gegevens worden vrijgegeven, wordt de bewaartimer gestart. Als u de optie selecteert om gemigreerde gegevens onmiddellijk te verwijderen, worden de gebruikers status gegevens verwijderd zodra ze worden vrijgegeven. Als u de optie selecteert om de gegevens gedurende een bepaalde periode te behouden, worden de gegevens verwijderd zodra die periode is verstreken nadat de statusgegevens zijn vrijgegeven. Hoe langer u de Bewaar periode instelt, hoe meer schijf ruimte u waarschijnlijk nodig hebt.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Het station selecteren waarop u de migratiegegevens voor de gebruikersstatus wilt opslaan  

Wanneer u het status migratie punt configureert, geeft u het station op de server op om de migratie gegevens van de gebruikers status op te slaan. U kiest een station uit een vaste lijst met stations. Sommige van deze stations stellen mogelijk echter niet-schrijfbare stations voor, zoals het cd-station of een station dat niet tot de netwerkshare behoort. Sommige stationsletters zijn mogelijk niet toegewezen aan een station op de computer. Geef een Beschrijf bare, gedeelde schijf op wanneer u het status migratie punt configureert.  


### <a name="configure-a-state-migration-point"></a>Een statusmigratiepunt configureren  

Gebruik de volgende methoden om een status migratie punt te configureren om de gebruikers status gegevens op te slaan:  

-   Gebruik de **wizard Sitesysteemserver maken** om een nieuwe sitesysteemserver te maken voor het statusmigratiepunt.  

-   Gebruik de **wizard Sitesysteemrollen toevoegen** om een statusmigratiepunt toe te voegen aan een bestaande server.  

Wanneer u deze wizards gebruikt, wordt u gevraagd om de volgende informatie op te geven voor het status migratie punt:  

-   De mappen voor het opslaan van de gebruikersstatusgegevens.  

-   Het maximum aantal clients die gegevens op het statusmigratiepunt kunnen opslaan.  

-   De minimale hoeveelheid vrije schijfruimte voor het statusmigratiepunt om gebruikersstatusgegevens op te slaan.  

-   Het verwijderingsbeleid voor de rol. Geef op dat de gebruikers status gegevens onmiddellijk worden verwijderd nadat ze op een computer zijn hersteld, of na een bepaald aantal dagen nadat de gebruikers gegevens op een computer zijn hersteld.  

-   Of het statusmigratiepunt alleen moet reageren op aanvragen om gebruikersstatusgegevens terug te zetten. Wanneer u deze optie inschakelt, kunt u het status migratie punt niet gebruiken om de gebruikers status gegevens op te slaan.  

Zie [site systeem rollen toevoegen](../../core/servers/deploy/configure/add-site-system-roles.md)voor de stappen om een site systeemrol te installeren.  
