---
title: Certificerings instanties verwijderen
titleSuffix: Configuration Manager
description: De centrale beheer site (CAS) verwijderen om uw Configuration Manager-infra structuur te vereenvoudigen op één zelfstandige primaire site.
ms.date: 06/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a1d9d4ce8cdd19efb440d4d73fafdc96a514bcd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699157"
---
# <a name="remove-the-central-administration-site"></a>De centrale beheer site verwijderen

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!-- 3607277 -->

Vanaf versie 2002, als de hiërarchie bestaat uit de centrale beheer site (CAS) en één onderliggende primaire site, kunt u de certificerings instanties verwijderen. Met deze actie wordt uw Configuration Manager-infra structuur vereenvoudigd tot één zelfstandige primaire site. Het verwijdert de complexiteit van site-naar-site-replicatie en richt zich op de beheer taken van de ene site.

> [!IMPORTANT]
> In deze versie van Configuration Manager is deze functie voorlopige versie en is deze niet standaard ingeschakeld. Het is momenteel beschikbaar voor klanten met micro soft premier.
>
> Als u deze functie wilt inschakelen, neemt u contact op met uw Technical Account Manager voor hulp:
>
> - Uw TAM opent een advies aanvraag, die uw micro soft premier-uren zal gebruiken.
> - U kunt de ernst van de situatie niet wijzigen.
> - Microsoft Ondersteuning bewaart deze advies gevallen tijdens normaal werk dagen.

## <a name="plan"></a>Plannen

- De hiërarchie moet bestaan uit de CA'S en één onderliggende primaire site. De primaire site kan secundaire sites hebben. Als u andere onderliggende primaire sites uit de hiërarchie wilt verwijderen, raadpleegt u de plannings stappen en vereisten voor het [verwijderen van een primaire site](uninstall-sites-and-hierarchies.md#bkmk_primary).

- Zorg ervoor dat de onderliggende primaire site voldoet aan de grootte-en schaal vereisten voor een zelfstandige [primaire site](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri).

- Site rollen op de CAS verplaatsen of buiten gebruik stellen, met uitzonde ring van het service aansluitpunt en het software-update punt. Configuration Manager Setup verwerkt deze twee rollen wanneer u de certificerings instanties verwijdert.

  De volgende rollen zijn het meest gebruikelijk bij de certificerings instanties, die u buiten gebruik wilt stellen of wilt verplaatsen naar de primaire site:

  - Asset Intelligence synchronisatie punt
  - Endpoint Protection-punt
  - Reporting Services-punt
  - Data Warehouse-service punt
  - Cloud beheer gateway (CMG)

    > [!NOTE]
    > Als u de CMG voor inhoud hebt ingeschakeld, moet u de inhoud opnieuw distribueren nadat u de CMG op de primaire site opnieuw hebt gemaakt.<!-- 6608659 -->

- Gedistribueerde weer gaven uitschakelen

- Configuration Manager het automatisch afhandelen van pakket bron locaties voor ingebouwde pakketten, zoals de Configuration Manager-client. Controleer alle andere inhouds bron locaties om er zeker van te zijn dat ze geen share op de CAS gebruiken.

- Stop alle actieve migratie taken en verwijder alle configuraties voor migratie. Zie de [actieve migratie van een andere hiërarchie stoppen](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy)voor meer informatie.

- Als u automatische implementatie regels voor software-updates gebruikt, maakt u deze opnieuw op de onderliggende primaire site.

- Als u Configuration Manager of System Center Updates Publisher gebruikt voor het beheren van [software-updates van derden](../../../../sum/deploy-use/third-party-software-updates.md), exporteert u het WSUS-handtekening certificaat van het software-update punt op de CAS.

  - Wacht tot de vereiste implementaties van software-updates van derden zijn uitgevoerd voordat u de CA'S verwijdert. Clients downloaden inhoud vooraf voor vereiste implementaties en wanneer u het software-update punt wijzigt, wordt de inhoud van de hash gewijzigd in de *lokale publicatie* van software-updates. (Dit gedrag heeft geen invloed op andere inhouds typen, alleen lokale publicatie van software-updates van derden.) Als u de certificerings instanties verwijdert met de vereiste implementaties die nog steeds worden uitgevoerd, mislukken de clients met een fout die niet overeenkomt met de hash.

- Controleer alle software van derden die mogelijk afhankelijk is van de CAS.

## <a name="prerequisites"></a>Vereisten

- De gebruiker met beheerders rechten die Configuration Manager Setup uitvoert, heeft de volgende beveiligings rechten nodig:

  - Lokale **Administrator** rechten op de CAS-server

  - Als de CAS-database server extern is van de site server, lokale **beheerders** rechten op de externe site database server voor de CAS.

  - **Sysadmin** -rechten op de CAS-site database

  - Lokale **beheerders** rechten op de primaire site server

  - Als de database server van de primaire site extern is van de primaire site server, lokale **beheerders** rechten op de externe site database server voor de primaire site.

  - **Sysadmin** -rechten voor de data base van de primaire site

  - De beveiligingsrol **infrastructuur beheerder** of **volledige beheerder** op de ca's en de primaire site

- Slechts één onderliggende primaire site in de hiërarchie. Zie [een primaire site verwijderen](uninstall-sites-and-hierarchies.md#bkmk_primary)voor meer informatie.

## <a name="process"></a>Proces

1. Start Configuration Manager Setup op de CAS-server met behulp van een van de volgende methoden:

    - Selecteer **Configuration Manager Setup**in het menu **Start** .

    - Open in de map voor de Configuration Manager- *installatie media* `\SMSSETUP\BIN\X64\setup.exe` . Zorg ervoor dat deze versie hetzelfde is als de site versie.

    - Open in de map waar Configuration Manager is *geïnstalleerd* `\BIN\X64\setup.exe` .

1. Lees de informatie op de pagina **voordat u begint** .

1. Selecteer op de pagina **aan de slag** de optie **site onderhoud uitvoeren of deze site opnieuw instellen**.

1. Selecteer op de pagina **site onderhoud** de optie **centrale beheer site verwijderen**. <!-- or is it still "delete"? -->

1. Op de pagina **bestaande site systeem rollen opnieuw configureren** :

    - **Service verbindings punt**: geef de Fully Qualified Domain name van het site systeem op de primaire site op die als host moet fungeren voor deze vereiste rol. Zie [about the Service Connection Point](../configure/about-the-service-connection-point.md)(Engelstalig) voor meer informatie.

    - **Software-update punt**: Selecteer een bestaand software-update punt op de primaire site. Setup configureert dit software-update punt om hetzelfde te synchroniseren als de CAS-configuratie.

    Setup controleert of de opgegeven servers voldoen aan de vereisten. Selecteer **installeren starten** wanneer u klaar bent om door te gaan.

Als er een probleem is met de installatie, gebruikt u de wizard om het proces opnieuw uit te voeren.

Wanneer het installatie programma is voltooid, wordt de primaire site opnieuw ingesteld. Zie [Run a site reset](../../manage/modify-your-infrastructure.md#bkmk_reset)(Engelstalig) voor meer informatie.

## <a name="monitor-and-verify"></a>Controleren en verifiëren

Controleer de volgende logboeken tijdens het installatie proces:

- `C:\ConfigMgrSetup.log` op de CAS-server

- **hman. log** in de map Configuration Manager logs op de primaire site server

Gebruik het knoop punt **site hiërarchie** in de werk ruimte **bewaking** om de wijzigingen in de hiërarchie te visualiseren. De volgende afbeelding toont bijvoorbeeld de voor-en na-vergelijking van de **verlegen was** -ca's, de primaire site van **Haw** en de secundaire **VWT** -site:

| Voor  | Na   |
|---------|---------|
|![Voor beeld van een site hiërarchie weergave van een certificerings instantie, primaire site en secundaire site](media/3607277-cas-primary-secondary.png)|![Voor beeld van een site hiërarchie weergave van een primaire site en secundaire site](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>Taken na installatie

Nadat u de certificerings instanties hebt verwijderd, controleert u de volgende stappen wanneer deze van toepassing zijn op uw omgeving.

- Verwijder het computer account van de CAS-server hand matig uit de lokale groepen van de primaire site.

- De vertrouwde basis sleutel is gewijzigd, waarvoor aanvullende acties kunnen worden vereist:

  - De opstart installatie kopieën van de besturingssysteem implementatie bijwerken met de meest recente Configuration Manager binaire bestanden.

  - Maak [media voor besturingssysteem implementatie](../../../../osd/deploy-use/create-task-sequence-media.md)opnieuw.

- Als u Configuration Manager verbindt met [Azure monitor](/azure/azure-monitor/platform/collect-sccm?context=/mem/configmgr/core/context/core-context), moet u de verbinding opnieuw instellen. De eerste stap voor het oplossen van problemen is [het vernieuwen van de geheime sleutel](../configure/azure-services-wizard.md#bkmk_renew). Als het probleem niet is opgelost, maakt u de verbinding opnieuw.<!-- 5584635 -->

- Als u in versie 2002 synchronisatie van Surface-Stuur Programma's inschakelt, moet u deze functie opnieuw configureren nadat u de CA'S hebt verwijderd. Zie voor meer informatie [micro soft Surface-Stuur Programma's en firmware-updates](../../../../sum/deploy-use/surface-drivers.md).<!-- 5728727 -->

- Als u software-updates van derden beheert:

  1. Exporteer het WSUS-handtekening certificaat van het software-update punt op de CAS, als u dat nog niet hebt gedaan.

  1. Voordat u nieuwe implementaties maakt, moet u de update verwijderen uit de bestaande implementaties en software-update pakketten.

  1. Als u de meta gegevens van software-updates wilt herstellen naar een bruikbare status, moet u geabonneerde catalogi opnieuw synchroniseren. U kunt ook wachten tot de Configuration Manager automatisch opnieuw wordt gesynchroniseerd.

  1. Start of wacht tot een normaal synchronisatie proces voor software-updates Configuration Manager met de huidige status van WSUS. Gebruik eventueel SCUP gemaakt of WSUS Power shell-cmdlets om updates te verwijderen en te lezen.

  1. Publiceer inhoud opnieuw voor updates die u moet implementeren.