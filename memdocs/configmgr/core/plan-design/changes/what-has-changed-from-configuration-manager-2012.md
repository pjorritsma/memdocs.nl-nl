---
title: Wijzigingen van versie 2012
titleSuffix: Configuration Manager
description: Identificeer de wijzigingen en nieuwe mogelijkheden in Configuration Manager versus System Center 2012 Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0cd49eac95d9789fd11ba2bf1ca01b68b236628d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720826"
---
# <a name="whats-changed-from-system-center-2012-configuration-manager"></a>Wat is er gewijzigd in System Center 2012 Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

De huidige vertakking van Configuration Manager introduceert belang rijke wijzigingen van System Center 2012 Configuration Manager. In dit artikel worden belang rijke wijzigingen en nieuwe mogelijkheden van de oorspronkelijke basis versie 1511 van Configuration Manager current branch geïdentificeerd. Zie [Wat is er nieuw in Configuration Manager incrementele versies](whats-new-incremental-versions.md)voor meer informatie over de wijzigingen die zijn aangebracht in recente updates voor Configuration Manager.

> [!NOTE]
> Vanaf versie 1910 maakt Configuration Manager nu deel uit van micro soft Endpoint Manager. Zie [micro soft Endpoint Configuration Manager](whats-new-in-version-1910.md#bkmk_mem)voor meer informatie.

De release van december 2015 (versie 1511) van Configuration Manager was de eerste versie van het huidige Configuration Manager product van micro soft. Dit wordt meestal aangeduid als Configuration Manager huidige branch. *Huidige branch* geeft aan dat deze versie incrementele updates voor het product ondersteunt. Het biedt ook een manier om onderscheid te maken tussen deze release en eerdere releases van Configuration Manager.  

Huidige vertakking Configuration Manager:  

- Maakt geen gebruik van een jaar of product-id in de product naam, in tegens telling tot eerdere versies, zoals Configuration Manager 2007 of System Center 2012 Configuration Manager.  

- Biedt ondersteuning voor incrementele updates in het product, ook wel update versies genoemd. De eerste versie is versie 1511. Latere versies worden meerdere keren per jaar vrijgegeven als updates in de console, zoals versie 1910.  

- Wordt geïnstalleerd met een basislijn versie. Hoewel 1511 de oorspronkelijke basislijn versie was, worden nieuwe basislijn versies ook van tijd tot tijd vrijgegeven, zoals 2002. Basislijn versies kunnen worden gebruikt om een nieuwe Configuration Manager-site en-hiërarchie te installeren of om een upgrade uit te kunnen uitvoeren van een ondersteunde versie van System Center 2012 Configuration Manager.  

## <a name="in-console-updates"></a><a name="bkmk_updates"></a>Updates in de console

Configuration Manager maakt gebruik van een console service methode met de naam **updates en onderhoud** waarmee u gemakkelijk aanbevolen updates kunt zoeken en installeren.  

Sommige versies zijn alleen beschikbaar als updates voor bestaande sites in de Configuration Manager-console. U kunt deze updates niet gebruiken om een nieuwe Configuration Manager-site te installeren. De update 1910 is bijvoorbeeld alleen beschikbaar vanuit de Configuration Manager-console. Het wordt gebruikt voor het bijwerken van een site die al een ondersteunde versie van Configuration Manager uitvoert.

Er wordt regel matig een update versie uitgebracht als nieuwe *basislijn* versie. Update versie 2002 is bijvoorbeeld ook een basis lijn. Een basislijn versie gebruiken om een nieuwe site of hiërarchie te installeren. Begin niet met een oudere basislijn versie, zoals 1802, en voer een upgrade uit naar de meest recente versie. Altijd de laatste basis lijn gebruiken.

Raadpleeg voor meer informatie de volgende artikelen:

- [Updates voor Configuration Manager](../../servers/manage/updates.md)
- [Basis lijn-en update versies](../../servers/manage/updates.md#bkmk_Baselines)

## <a name="service-connection-point"></a><a name="bkmk_servicepoint"></a>Service verbindings punt  

Configuration Manager huidige vertakking bevat een nieuwe site systeemrol, het **service aansluitpunt**:  

- Een aanspreek punt voor veel functies die in de Cloud kunnen worden gebruikt

- Downloadt updates voor uw site

- Hiermee worden diagnostische en gebruiks gegevens over uw site geüpload naar de micro soft-Cloud

Deze site systeemrol ondersteunt zowel online als offline modi van de bewerking. Zie [about the Service Connection Point](../../servers/deploy/configure/about-the-service-connection-point.md)(Engelstalig) voor meer informatie.  

## <a name="diagnostics-and-usage-data"></a><a name="bkmk_usage"></a>Diagnostische en gebruiks gegevens

Configuration Manager verzamelt diagnostische en gebruiks gegevens over uw sites en infra structuur. Deze informatie wordt door het service aansluitpunt gecompileerd en verzonden naar de micro soft-Cloud service. Configuration Manager vereist deze gegevens om updates te downloaden die van toepassing zijn op uw omgeving. Wanneer u het service aansluitpunt instelt, kunt u het niveau van de gegevens die worden verzameld, opgeven en bepalen of de gegevens automatisch (online) of hand matig (offline) moeten worden verzonden.

Zie [diagnostiek en gebruiks gegevens](../diagnostics/diagnostics-and-usage-data.md)voor meer informatie.  

## <a name="deprecated-functionality"></a><a name="bkmk_out"></a>Afgeschafte functionaliteit  

Sommige functies, zoals systeem eigen [ondersteuning voor Intel Active Management Technology (Amt)](#bkmk_AMT) gebaseerde computers, worden verwijderd uit de Configuration Manager-console. Andere functies, zoals netwerk toegangs beveiliging, worden volledig verwijderd. Daarnaast worden sommige oudere micro soft-producten, zoals Windows Vista, Windows Server 2008 en SQL Server 2008, niet meer ondersteund.  

Zie [verwijderde en afgeschafte items](deprecated/removed-and-deprecated.md)voor een lijst met afgeschafte functies.  

Zie [ondersteunde configuraties](../configs/supported-configurations.md)voor meer informatie over ondersteunde producten, besturings systemen en configuraties.  

### <a name="support-for-intel-active-management-technology-amt"></a><a name="bkmk_AMT"></a> Ondersteuning voor Intel Active Management Technology (AMT)  

Configuration Manager huidige vertakking verwijdert systeem eigen ondersteuning voor op AMT gebaseerde computers vanuit de Configuration Manager-console. Op AMT gebaseerde computers blijven volledig beheerd wanneer u de [Intel SCS-invoeg toepassing voor micro soft-Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html)gebruikt. De invoeg toepassing biedt u toegang tot de nieuwste mogelijkheden voor het beheren van AMT, terwijl het verwijderen van de beperkingen die zijn geïntroduceerd totdat Configuration Manager deze wijzigingen kan opnemen.  

Het verwijderen van geïntegreerde AMT voor Configuration Manager omvat out-of-band-beheer. De site systeemrol van het out-of-band-beheer punt is niet meer beschikbaar.  

> [!Note]
> Deze wijziging heeft geen invloed op out-of-band-beheer in System Center 2012 Configuration Manager.

## <a name="changes-in-functionality"></a>Wijzigingen in functionaliteit

In de volgende secties vindt u een overzicht van enkele belang rijke wijzigingen in functie gebieden tussen System Center 2012 R2 Configuration Manager en versie 1511 versie van Configuration Manager current branch. Zie [Wat is er nieuw in incrementele versies](whats-new-incremental-versions.md)? voor meer informatie over de meest recente wijzigingen in functionaliteit.

### <a name="client-deployment"></a>Clientimplementatie  

Configuration Manager introduceert een nieuwe functie waarmee nieuwe versies van de Configuration Manager-client worden getest voordat de rest van de site met de nieuwe software wordt bijgewerkt. U kunt een pre-productie verzameling instellen waarin een nieuwe client kan worden gepiloteerd. Zodra u tevreden bent met de nieuwe client software in de pre-productie, kunt u de client promo veren om de rest van de site automatisch bij te werken met de nieuwe versie.  

Zie [Client upgrades testen in een pre-productie verzameling](../../clients/manage/upgrade/test-client-upgrades.md)voor meer informatie over het testen van clients.  

### <a name="os-deployment"></a>Besturingssysteemimplementatie  

Houd rekening met de volgende wijzigingen in de implementatie van het besturings systeem:

- In de wizard taken reeks maken is een nieuw taken reeks type beschikbaar: **een upgrade van een besturings systeem uitvoeren vanuit een upgrade pakket**. De stappen voor het maken van een upgrade van computers van Windows 7 of Windows 8,1 naar Windows 10. Zie [Windows upgraden naar de nieuwste versie](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)voor meer informatie.  

- Windows PE-peer-cache is nu beschikbaar wanneer u besturings systemen implementeert. Computers waarop een taken reeks wordt uitgevoerd om een besturings systeem te implementeren, kunnen gebruikmaken van Windows PE-peer-cache om inhoud te verkrijgen van een peer-cache bron, in plaats van inhoud te downloaden vanaf een distributie punt. Dit gedrag zorgt ervoor dat WAN-verkeer in filialen wordt geminimaliseerd wanneer er geen lokaal distributie punt is. Zie [Windows PE-peer-cache voorbereiden om WAN-verkeer te verminderen](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)voor meer informatie.  

- U kunt nu de status van Windows als een service in uw omgeving weer geven. U kunt ook onderhouds plannen maken voor het implementeren van implementatie ringen en ervoor zorgen dat de huidige branch-computers van Windows 10 up-to-date blijven wanneer er nieuwe builds worden uitgebracht. Daarnaast kunt u waarschuwingen weer geven wanneer Windows 10-clients aan het einde van de ondersteuning voor hun build zijn. Zie [Windows als een service beheren](../../../osd/deploy-use/manage-windows-as-a-service.md)voor meer informatie.  

### <a name="application-management"></a>Toepassingsbeheer  

Houd rekening met de volgende wijzigingen in toepassings beheer:

- Met Configuration Manager kunt u Universeel Windows-platform-apps (UWP) implementeren voor apparaten met Windows 10 of hoger. Zie [Windows-toepassingen maken](../../../apps/get-started/creating-windows-applications.md)voor meer informatie.  

- Software Center heeft een nieuwe, moderne vormgeving. Gebruikers beschik bare apps die eerder alleen in de Application Catalog zijn verschenen, worden nu weer gegeven in Software Center onder het tabblad toepassingen. Dit gedrag zorgt ervoor dat deze implementaties beter kunnen worden gedetecteerd en dat gebruikers niet kunnen verwijzen naar de afzonderlijke toepassings catalogus. Bovendien is een browser die geschikt is voor Silverlight niet meer vereist. Zie [toepassings beheer plannen en configureren](../../../apps/plan-design/plan-for-and-configure-application-management.md)voor meer informatie.  

- Met het nieuwe toepassingstype Windows Installer via MDM kunt u Windows Installer-apps maken en implementeren op ingeschreven pc's met Windows 10. Zie [Windows-toepassingen maken](../../../apps/get-started/creating-windows-applications.md)voor meer informatie.  

- Als u in Configuration Manager 2012 een koppeling naar een app in de Windows Store wilt opgeven, kunt u de koppeling rechtstreeks opgeven of bladeren naar een externe computer waarop de app is geïnstalleerd. In Configuration Manager huidige vertakking kunt u de koppeling toch rechtstreeks invoeren, maar nu kunt u in plaats van naar een referentie computer te bladeren, rechtstreeks vanuit de Configuration Manager-console naar de Store voor de app.  

### <a name="software-updates"></a>Software-updates  

Houd rekening met de volgende wijzigingen voor software-updates:

- Configuration Manager kan nu het verschil detecteren tussen methoden voor software-update beheer voor computers. Met name kan het onderscheid worden gemaakt tussen een Windows 10-computer die verbinding maakt met Windows Update for Business (WUfB) en een computer die is verbonden met WSUS. Het kenmerk **UseWUServer** is nieuw en geeft aan of de computer wordt beheerd met WUfB. U kunt deze instelling in een verzameling gebruiken om deze computers uit het software-updatebeheer te verwijderen. Zie [Integratie met Windows Update voor bedrijven in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)voor meer informatie.  

- U kunt nu de WSUS-opschoon taak plannen en uitvoeren vanuit de Configuration Manager-console. Wanneer u in de eigenschappen van **Software-update punt componenten** selecteert om de WSUS-opschoon taak uit te voeren, wordt deze uitgevoerd bij de volgende synchronisatie van software-updates. De verlopen software-updates worden ingesteld op de status geweigerd op de WSUS-server en de Windows Update-Agent op computers scant deze software-updates niet meer. Voor meer informatie, zie [De WSUS-opschoontaak plannen en uitvoeren](../../../sum/deploy-use/software-updates-maintenance.md).  

### <a name="compliance-settings"></a>Instellingen voor naleving  

Houd rekening met de volgende wijzigingen in de instellingen voor naleving:

- Configuration Manager verbetert de werk stroom voor het maken van configuratie-items. Wanneer u nu een configuratie-item maakt en ondersteunde platformen selecteert, zijn alleen de instellingen die relevant zijn voor dat platform beschikbaar . Zie [aan de slag met instellingen voor naleving](../../../compliance/get-started/get-started-with-compliance-settings.md).  

- Met de wizard **configuratie-item maken** kunt u het type configuratie-item dat u wilt maken, gemakkelijker selecteren. Daarnaast zijn er nieuwe en bijgewerkte configuratie-items beschikbaar voor:  

    - Windows 10-apparaten die worden beheerd met de Configuration Manager-client  

    - Mac OS X-apparaten die worden beheerd met de Configuration Manager-client  

    - Windows Desktop-en Server computers die worden beheerd met de Configuration Manager-client  

    - Windows 8,1-en Windows 10-apparaten die worden beheerd zonder de Configuration Manager-client  

    Zie [configuratie-items maken](../../../compliance/deploy-use/create-configuration-items.md)voor meer informatie.  

- Ondersteuning voor het beheren van instellingen op Mac OS X-computers die worden beheerd zonder de Configuration Manager-client.

### <a name="on-premises-mobile-device-management"></a>On-premises Mobile Device Management  

U kunt nu mobiele apparaten beheren met behulp van de on-premises Configuration Manager-infra structuur. Alle apparaat-en beheer gegevens worden on-premises verwerkt en maken geen deel uit van Microsoft Intune of andere Cloud Services. Voor dit type Apparaatbeheer is geen client software vereist. Configuration Manager beheert apparaten met functionaliteit die is ingebouwd in het besturings systeem van het apparaat.  

Zie [mobiele apparaten beheren met on-premises infra structuur](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Wat is er nieuw in incrementele versies](whats-new-incremental-versions.md)
