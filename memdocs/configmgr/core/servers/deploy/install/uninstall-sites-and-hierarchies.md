---
title: Sites verwijderen
titleSuffix: Configuration Manager
description: Een hand leiding voor het verwijderen van functies, en verwijderen van sites en hiërarchieën
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a90d6f34370b8c3167272bce1a0a673cc5074094
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81718047"
---
# <a name="uninstall-roles-sites-and-hierarchies-in-configuration-manager"></a>Rollen, sites en hiërarchieën verwijderen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik dit artikel als richt lijn voor het verwijderen van een Configuration Manager site systeemrol, site of hiërarchie.

Vanaf versie 2002 kunt u de centrale beheer site (CAS) ook uit een hiërarchie verwijderen, maar de primaire site blijven gebruiken.

## <a name="site-system-role"></a><a name="bkmk_role"></a>Site systeemrol

U kunt het beste een rol verwijderen van een site systeem server om de volgende redenen:

- Grotere wijzigingen in de infra structuur, zoals netwerk of fysieke locaties
- De onderliggende server buiten gebruik stellen
- Rollen samen voegen om de kosten en complexiteit te verlagen
- De site rollen opnieuw configureren of opnieuw ontwerpen
- Gebruik van de functie die rol ondersteunt, wordt stopgezet

Wanneer u besluit een rol te verwijderen, moet u eerst uw antwoorden op de volgende vragen beantwoorden:

- Hebt u nog steeds de rol nodig in de-site? Als dat het geval is, heeft een ander site systeem al de rol?

- Zijn er andere site systemen met deze rol op de juiste manier formaat ter ondersteuning van uw bedrijfs vereisten voor prestaties en beschik baarheid?

- Zijn alle clients al opnieuw geconfigureerd voor het gebruik van een andere rol? Vertrouwt u op het standaard gedrag van de client om terug te vallen of een andere server te ontdekken?

### <a name="procedure-to-remove-a-site-system-role"></a>Procedure voor het verwijderen van een site systeemrol

Gebruik de volgende procedure om een rol te verwijderen:

1. Ga in de **Configuration Manager** -console naar de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer vervolgens het knoop punt **servers en site systeem rollen** .

1. Selecteer de site systeem server met de rol die u wilt verwijderen. Selecteer de doel functie in het detail venster **site systeem rollen** .

1. Selecteer op het lint op het tabblad **siterol** in de groep **Siterol** de optie **rol verwijderen**. Bevestig dat u de rol wilt verwijderen.

### <a name="additional-information-for-specific-roles"></a>Aanvullende informatie voor specifieke rollen

Sommige rollen hebben mogelijk extra stappen en overwegingen.

#### <a name="software-update-point"></a>Software-updatepunt

Nadat u het software-update punt hebt verwijderd, wordt door Configuration Manager het client beleid bijgewerkt om het software-update punt uit de lijst te verwijderen. Wanneer u het laatste software-update punt op de site verwijdert, bevat de lijst software-update punt geen software-update punten. Als er geen rollen beschikbaar zijn, wordt het beheer van software-updates in feite uitgeschakeld op de site.

Als u meer dan één software-update punt op een primaire site hebt en u het software-update punt verwijdert dat de synchronisatie bron is, kiest u een ander software-update punt op de site als nieuwe synchronisatie bron.

## <a name="secondary-site"></a><a name="bkmk_secondary"></a>Secundaire site  

Anders dan wanneer u [een hiërarchie buiten gebruik](#bkmk_hierarchy)stelt, is de belangrijkste reden voor het verwijderen van een secundaire site het gevolg van een bredere wijziging van de infra structuur, zoals netwerk-of fysieke locaties. Bekijk ook de redenen voor het [kiezen van een secundaire site](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary).

Wanneer u besluit een secundaire site te verwijderen, moet u eerst uw antwoorden op de volgende vragen beantwoorden:

- Hebt u alle site systeem rollen van de site server verwijderd?

- Zijn er grenzen of grens groepen die zijn gekoppeld aan de secundaire site? Configureer grenzen opnieuw voordat u de site verwijdert.

- Bevinden clients zich nog steeds op de locatie?

- Hebt u andere opties voor inhouds beheer, zoals [peer-caching](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies), geconfigureerd?

### <a name="options-to-delete-secondary-sites"></a>Opties voor het verwijderen van secundaire sites

U kunt een secundaire site niet verplaatsen naar of opnieuw toewijzen aan een andere primaire site. Wanneer u een secundaire site verwijdert uit de directe bovenliggende site, kiest u of u deze wilt verwijderen of verwijderen.

#### <a name="uninstall-the-secondary-site"></a>De secundaire site verwijderen

Gebruik deze optie om een functionele secundaire site te verwijderen die toegankelijk is vanaf het netwerk. Met deze optie verwijdert u Configuration Manager van de secundaire site server. Vervolgens worden alle gegevens over de site en de bijbehorende resources verwijderd uit de Configuration Manager-site.

Als Configuration Manager SQL Server Express voor de secundaire site hebt geïnstalleerd, Configuration Manager de installatie van SQL Express ook ongedaan maken. Als u SQL Server Express hebt geïnstalleerd voordat u de secundaire site hebt geïnstalleerd, Configuration Manager de installatie van SQL Server Express niet ongedaan maken.

#### <a name="delete-the-secondary-site"></a>De secundaire site verwijderen

Gebruik deze optie in de volgende situaties:

- De installatie is mislukt

- Nadat u deze hebt verwijderd, wordt de secundaire site nog steeds weer gegeven in de Configuration Manager-console

    Met deze optie worden alle gegevens over de site en de bijbehorende resources verwijderd uit de Configuration Manager hiërarchie, maar worden er geen wijzigingen aangebracht op de site server.

    > [!TIP]
    >  U kunt ook het hiërarchie-onderhouds programma met de optie **/DELSITE** gebruiken om een secundaire site te verwijderen. Zie het [hulp programma voor hiërarchie-onderhoud (preinst. exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md)voor meer informatie.

### <a name="prerequisites-to-delete-a-secondary-site"></a>Vereisten voor het verwijderen van een secundaire site

De gebruiker met beheerders rechten die Configuration Manager Setup uitvoert, heeft de volgende beveiligings rechten nodig:

- Lokale **beheerders** rechten op de secundaire site server

- Als de database server van de primaire site extern is van de primaire site server, lokale **beheerders** rechten op de externe site database server voor de primaire site.

- De beveiligingsrol **infrastructuur beheerder** of **volledige beheerder** op de bovenliggende primaire site

- **Sysadmin** -rechten op de secundaire site database

### <a name="procedure-to-delete-a-secondary-site"></a>Procedure voor het verwijderen van een secundaire site

Gebruik de volgende procedure om een secundaire site te verwijderen of verwijderen:

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit en selecteer vervolgens het knoop punt **sites** .

1. Selecteer de secundaire site server die u wilt verwijderen. Selecteer in het lint op het tabblad **Start** in de groep **site** de optie **verwijderen**.

1. Selecteer op de pagina **Algemeen** of u de secundaire site wilt verwijderen of verwijderen.

1.  Voltooi de wizard.

## <a name="primary-site"></a><a name="bkmk_primary"></a>Primaire site  

U kunt het beste een primaire site verwijderen uit uw hiërarchie om de volgende redenen:

- Consolideer sites om de kosten en complexiteit te verlagen
- De sites van de hiërarchie opnieuw configureren of opnieuw ontwerpen

Voordat u een onderliggende primaire site verwijdert die gebruikmaakt van [gedistribueerde weer gaven](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) voor de replicatie koppeling naar de CAS, moet u eerst gedistribueerde weer gaven uitschakelen in uw hiërarchie. Zie [Een primaire site verwijderen die is geconfigureerd met gedistribueerde weergaven](#bkmk_distviews)voor meer informatie.

### <a name="plan-to-uninstall-a-primary-site"></a><a name="bkmk_pri-plan"></a>Het verwijderen van een primaire site plannen

Voordat u een primaire site verwijdert, controleert u de volgende taken:

- Grenzen, grens groepen en terugval relaties controleren. Als u clients toewijst aan een nieuwe site, maar niet de grenzen wijzigt, kunnen ze als roaming worden beschouwd. Zie [site grenzen en grens groepen definiëren](../configure/define-site-boundaries-and-boundary-groups.md)voor meer informatie.

- Zorg ervoor dat alle actieve clients opnieuw worden toegewezen aan een andere primaire site in de hiërarchie. Clients worden niet meer beheerd nadat u de site hebt verwijderd. Zie [clients toewijzen aan een site](../../../clients/deploy/assign-clients-to-a-site.md)voor meer informatie.

  - Bekijk de lijst met site rollen om ervoor te zorgen dat de nieuwe site hetzelfde service niveau biedt.

  - Zorg ervoor dat u de grootte van de andere site systemen met deze rol op de andere site juist hebt aangepast. Ze moeten uw bedrijfs vereisten voor prestaties en beschik baarheid met de extra clients ondersteunen.

  - Als deze site veel clients heeft, kunt u ze in fasen opnieuw toewijzen. Database replicatie bewaken wanneer clients volledige inventarisatie en andere locatiespecifieke gegevens vernieuwen. Als u software-updates beheert, worden clients toegewezen aan een nieuw software-update punt. Dit gedrag zorgt voor een volledige scan op update naleving.

  - Het opnieuw toewijzen van een client kan invloed hebben op rapporten en query's die afhankelijk zijn van inventaris gegevens en naleving op basis van de status. Overweeg het tijdelijk aanpassen van alle client cycli tijdens de overgang.

  - Controleer alle client toewijzings methoden om er zeker van te zijn dat er geen verwijzingen naar deze primaire site zijn.

- Controleer of er actief gebruikte objecten in de hiërarchie statische verwijzingen naar de site code hebben. Bijvoorbeeld verzamelings query's, taken reeksen of beheer scripts.

- Als de hiërarchie een [terugval site](../configure/boundary-group-procedures.md#bkmk_site-fallback) voor automatische site toewijzing gebruikt, controleert u of deze geen verwijzing naar deze primaire site bevat.

- Configureer alle [client installatie methoden](../../../clients/deploy/plan/client-installation-methods.md) die kunnen verwijzen naar een statische-site code.

- Als deze primaire site site-specifieke Cloud-gekoppelde services bevat, moet u deze verwijderen. Als u nog steeds de cloud resources nodig hebt, verplaatst u ze naar een andere primaire site in de hiërarchie. Verwijder ze van de primaire site die u gaat verwijderen en voeg ze toe aan een andere primaire site.

- Als deze primaire site [detectie methoden](../configure/run-discovery.md) heeft voor de hiërarchie, verplaatst u ze naar een andere site.

- Buiten gebruik stellen op sites gebaseerde [besturingssysteem implementatie media](../../../../osd/deploy-use/create-task-sequence-media.md).

- Verwijder alle site systeem rollen van de site en de site server. Zie [site systeem rollen verwijderen](#bkmk_role)voor meer informatie. Hoewel deze voorbereidings stap niet is vereist, kunt u aanvullende afhankelijkheden identificeren voordat u de site verwijdert.

- Verwijder alle secundaire sites onder deze primaire site. Zie de sectie [secundaire site](#bkmk_secondary) voor meer informatie.

### <a name="prerequisites-to-uninstall-a-primary-site"></a><a name="bkmk_pri-prereq"></a>Vereisten voor het verwijderen van een primaire site

De gebruiker met beheerders rechten die Configuration Manager Setup uitvoert, heeft de volgende beveiligings rechten nodig:

- Lokale **Administrator** rechten op de CAS-server

- Als de CAS-database server extern is van de site server, lokale **beheerders** rechten op de externe site database server voor de CAS.

- **Sysadmin** -rechten op de CAS-site database

- Lokale **beheerders** rechten op de primaire site server

- Als de database server van de primaire site extern is van de primaire site server, lokale **beheerders** rechten op de externe site database server voor de primaire site.

- De beveiligingsrol **infrastructuur beheerder** of **volledige beheerder** op de CAS

### <a name="procedure-to-uninstall-a-primary-site"></a><a name="bkmk_pri-process"></a>Procedure voor het verwijderen van een primaire site

U voert Configuration Manager Setup uit om een primaire site te verwijderen waaraan geen secundaire site is gekoppeld. Gebruik de volgende procedure om een primaire site te verwijderen:

> [!TIP]
> Als de primaire site server niet langer beschikbaar is, gebruikt u het hulp programma voor hiërarchie onderhoud op de certificerings instantie om de primaire site uit de site database te verwijderen. Zie het [hulp programma voor hiërarchie-onderhoud (preinst. exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md)voor meer informatie.

1. Start Configuration Manager Setup op de primaire site server met behulp van een van de volgende methoden:

    - Selecteer **Configuration Manager Setup**in het menu **Start** .

    - Open `\SMSSETUP\BIN\X64\setup.exe`in de map voor de Configuration Manager- *installatie media*. Zorg ervoor dat deze versie hetzelfde is als de site versie.

    - Open `\BIN\X64\setup.exe`in de map waar Configuration Manager is *geïnstalleerd*.

1. Lees de informatie op de pagina **voordat u begint** .

1. Selecteer op de pagina **aan de slag** de optie **een Configuration Manager site verwijderen**.

    > [!IMPORTANT]  
    >  Als er een secundaire site aan de primaire site gekoppeld is, moet u eerst de secundaire site verwijderen voordat u de primaire site kunt deïnstalleren.  

1. Op de pagina **Configuration Manager site verwijderen** worden de volgende opties standaard ingeschakeld:

    - De site database van de primaire site server verwijderen
    - De Configuration Manager-console verwijderen

1. Selecteer **Ja** om te bevestigen dat de Configuration Manager primaire site moet worden verwijderd.

### <a name="uninstall-a-primary-site-that-uses-distributed-views"></a><a name="bkmk_distviews"></a>Een primaire site verwijderen die gebruikmaakt van gedistribueerde weer gaven

1. Voordat u een onderliggende primaire site verwijdert, moet u gedistribueerde weer gaven uitschakelen op elke koppeling in de hiërarchie tussen de CA'S en een primaire site.

1. Nadat u gedistribueerde weer gaven op elke koppeling hebt uitgeschakeld, controleert u of de gegevens van de primaire site zijn herinitialiseert bij de CAS. Zie [replicatie controleren](../../manage/monitor-replication.md)als u de initialisatie van gegevens wilt bewaken.

1. Nadat de gegevens opnieuw zijn geïnitialiseerd met de certificerings instantie, kunt u [de primaire site verwijderen](#bkmk_pri-process).

1. Wanneer de primaire site wordt verwijderd, kunt u gedistribueerde weer gaven op koppelingen van de CA'S naar andere primaire sites opnieuw configureren.

    > [!IMPORTANT]
    > Als u de primaire site verwijdert voordat u gedistribueerde weer gaven op elke site uitschakelt, of voordat de gegevens van de primaire site opnieuw zijn geïnitialiseerd bij de certificerings instantie, kan de gegevens replicatie mislukken.

## <a name="decommission-a-hierarchy"></a><a name="bkmk_hierarchy"></a>Een hiërarchie buiten gebruik stellen

Sommige organisaties hebben meerdere hiërarchieën vanwege fusies, verwervingen, test omgevingen of andere zakelijke vereisten. Als u het beheer aan één hiërarchie consolideert, kan deze actie de kosten en complexiteit helpen verlagen. Een andere reden om de hiërarchie buiten gebruik te stellen, is dat u migreert naar een Cloud beheer service, zoals Microsoft Intune, en klaar is om uw on-premises infra structuur te verwijderen.

Als u een hiërarchie met meerdere sites buiten gebruik wilt stellen, is de volg orde van de verwijdering belang rijk. Begin met het verwijderen van de sites aan de onderkant van de hiërarchie en ga vervolgens omhoog:

1. Verwijder secundaire sites die aan primaire sites zijn gekoppeld.
2. Primaire sites verwijderen.
3. Nadat u alle primaire sites hebt verwijderd, kunt u de certificerings instanties verwijderen.

Zie de volgende secties voor meer informatie:

- [Een secundaire site verwijderen](#bkmk_secondary)
- [Een primaire site verwijderen](#bkmk_primary)
- [De certificerings instanties verwijderen](#bkmk_uninstall-cas)

### <a name="uninstall-the-cas"></a><a name="bkmk_uninstall-cas"></a>De certificerings instanties verwijderen

De laatste stap voor het buiten gebruik stellen van een hiërarchie is het verwijderen van de CAS. Voer Configuration Manager Setup uit om de CA'S te verwijderen die geen onderliggende primaire sites hebben.

#### <a name="prerequisites-to-uninstall-the-cas"></a>Vereisten voor het verwijderen van de CAS

De gebruiker met beheerders rechten die Configuration Manager Setup uitvoert, heeft de volgende beveiligings rechten nodig:

- Lokale **Administrator** rechten op de CAS-server

- Als de CAS-database server extern is van de site server, lokale **beheerders** rechten op de externe site database server voor de CAS.

#### <a name="procedure-to-uninstall-the-cas"></a>Procedure voor het verwijderen van de CAS

1. Start Configuration Manager Setup op de CAS-server met behulp van een van de volgende methoden:

    - Selecteer **Configuration Manager Setup**in het menu **Start** .

    - Open `\SMSSETUP\BIN\X64\setup.exe`in de map voor de Configuration Manager- *installatie media*. Zorg ervoor dat deze versie hetzelfde is als de site versie.

    - Open `\BIN\X64\setup.exe`in de map waar Configuration Manager is *geïnstalleerd*.

1. Lees de informatie op de pagina **voordat u begint** .

1. Selecteer op de pagina **aan de slag** de optie **een Configuration Manager site verwijderen**.

    > [!IMPORTANT]  
    >  Verwijder alle onderliggende primaire sites voordat u de certificerings instanties kunt verwijderen.  

1. Op de pagina **Configuration Manager site verwijderen** worden de volgende opties standaard ingeschakeld:

    - De site database verwijderen van de CAS-server
    - De Configuration Manager-console verwijderen

1. Selecteer **Ja** om te bevestigen dat de Configuration Manager centrale beheer site (CAS) wordt verwijderd.

## <a name="remove-the-cas"></a><a name="bkmk_remove-cas"></a>De CA'S verwijderen

<!-- 3607277 -->

Vanaf versie 2002, als de hiërarchie bestaat uit de CA'S en één onderliggende primaire site, kunt u de certificerings instanties verwijderen. Met deze actie wordt uw Configuration Manager-infra structuur vereenvoudigd tot één zelfstandige primaire site. Het verwijdert de complexiteit van site-naar-site-replicatie en richt zich op de beheer taken van de ene site.

Zie [de certificerings instanties verwijderen](remove-central-administration-site.md)voor meer informatie.
