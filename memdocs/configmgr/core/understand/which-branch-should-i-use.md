---
title: Welke vertakking moet ik gebruiken
titleSuffix: Configuration Manager
description: Meer informatie over de verschillen tussen de beschik bare vertakkingen van Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 542069b82ea4c68a48ccc47b79007fd2fa25322a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906014"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Welke vertakking van Configuration Manager moet ik gebruiken?

*Van toepassing op: Configuration Manager (huidige vertakking & Technical Preview-vertakking) & System Center Configuration Manager (onderhouds branche voor de lange termijn)*

Er zijn drie vertakkingen van Configuration Manager beschikbaar:

- Huidige vertakking
- Long-Term Servicing Branch
- Branch voor Technical Preview

Gebruik dit artikel om u te helpen bij het kiezen van de juiste vertakking.

> [!TIP]  
> Alle sites in een hiërarchie moeten dezelfde vertakking uitvoeren. Het is niet mogelijk om een hiërarchie met verschillende vertakkingen op verschillende sites te hebben.

## <a name="current-branch"></a>Huidige vertakking

Deze vertakking is gelicentieerd voor gebruik in een productie omgeving. Gebruik deze vertakking om de nieuwste functies en functionaliteiten te verkrijgen. Als u een van de volgende licenties hebt, kunt u deze vertakking gebruiken:  

- System Center Data Center
- System Center Standard
- System Center Configuration Manager
- Gelijkwaardige abonnements rechten  

Zie [Licentiëring en vertakkingen voor Configuration Manager](learn-more-editions.md) en [veelgestelde vragen over Configuration Manager vertakkingen en licenties](product-and-licensing-faq.md)voor meer informatie over de opties voor Software Assurance en licenties.

Micro soft is van plan om updates voor Configuration Manager huidige vertakking enkele keren per jaar uit te geven. Elke update versie blijft ondersteuning voor 18 maanden vanaf de release datum van de algemene Beschik baarheid (GA). Technische ondersteuning wordt geboden voor de gehele periode van ondersteuning. Onze ondersteunings structuur is echter dynamisch, waardoor er sprake is van twee verschillende onderhouds fasen die afhankelijk zijn van de beschik baarheid van de nieuwste versie van de huidige vertakking. (Zie [ondersteuning voor Configuration Manager huidige branch-versies](../servers/manage/current-branch-versions-supported.md)voor meer informatie. Updates voor nieuwere versies zijn beschikbaar als updates in de console.

Als u de huidige branch als een nieuwe site wilt installeren, gebruikt u [basislijn media](../servers/manage/updates.md#bkmk_Baselines). Gebruik basislijn media ook om een upgrade uit te kunnen uitvoeren van System Center 2012 Configuration Manager met Service Pack 2 of System Center 2012 R2 Configuration Manager met Service Pack 1. De toegang tot deze media is afhankelijk van hoe uw organisatie licenties Configuration Manager.

U kunt ook de basislijn media gebruiken om een nieuwe site te installeren die een evaluatie-editie van de huidige vertakking is. Voor de evaluatie versie is geen licentie vereist. U kunt de Evaluation Edition voor 180 dagen gebruiken. Het biedt ondersteuning voor een upgrade naar een gelicentieerde versie van de huidige vertakking. Als u alleen een Evaluation Edition wilt installeren, haalt u deze op uit het [evaluatie centrum](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

> [!NOTE]
> Gebruik Baseline media om sites te installeren voor een nieuwe Configuration Manager-hiërarchie. Als u eerder een basislijn versie hebt geïnstalleerd, gebruikt u de updates in de console om uw sites bij te werken naar een nieuwe versie.  
>
> Sites die worden bijgewerkt met updates in de console, resulteren in sites die gelijk zijn aan die van de nieuwe site, die zijn geïnstalleerd met behulp van de basislijn media.
>
> Zie [updates voor Configuration Manager](../servers/manage/updates.md)voor meer informatie.  

### <a name="features-of-the-current-branch"></a>Functies van de huidige vertakking

- Ontvangt [updates in de console](../servers/manage/install-in-console-updates.md) die nieuwe functies beschikbaar maken voor gebruik.
- Ontvangt updates in de console die beveiligings-en kwaliteits oplossingen leveren aan bestaande functies.
- Biedt ondersteuning voor out-of-band-updates wanneer dit nodig is. Zie [het hulp programma Registratie bijwerken gebruiken](../servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) of [het installatie programma voor hotfixes gebruiken](../servers/manage/use-the-hotfix-installer-to-install-updates.md)voor meer informatie.
- Kan worden geïntegreerd met Cloud Services.
- Ondersteunt de [migratie van gegevens](../migration/migrate-data-between-hierarchies.md) van en naar andere Configuration Manager-installaties.
- Ondersteunt upgrades van eerdere versies van Configuration Manager.
- Ondersteunt installatie als een evaluatie-editie, van waaruit u later een upgrade kunt uitvoeren naar een volledig gelicentieerde installatie.

Micro soft raadt u aan binnenkort na de release bij te werken naar de nieuwste versie. U kunt Maxi maal acht maanden wachten voordat u een update naar een nieuwere versie uitvoert. U kunt ook een update overs Laan om de nieuwste versie beschikbaar te maken. Omdat elke versie cumulatief is, kunt u, als u over een update overs laat en de nieuwste versie installeert, nog steeds toegang krijgen tot alle functies en verbeteringen van eerdere versies.

Zie [ondersteuning voor huidige branch-versies](../servers/manage/current-branch-versions-supported.md)voor meer informatie.

### <a name="current-branch-update-options"></a>Opties voor de huidige branch-update

- Met actieve Software Assurance kunt u updates in de console installeren voor huidige branch-versies.  
- Er is geen optie om de huidige vertakking te converteren naar een Technical Preview-vertakking. Technical Preview branches zijn afzonderlijke installaties waarvoor geen licentie nodig is.
- Er is geen optie om uw huidige vertakking te converteren naar de Long-term Servicing Branch (LTSB). U moet de huidige vertakking verwijderen en vervolgens de LTSB installeren als een nieuwe installatie.

## <a name="long-term-servicing-branch"></a>Long-Term Servicing Branch

Deze vertakking is gelicentieerd voor gebruik in productie voor Configuration Manager klanten die gebruikmaken van de huidige branch en hun Configuration Manager Software Assurance (SA) of gelijkwaardige abonnements rechten hebben toegestaan om te verlopen na 1 oktober 2016. Zie [Licentiëring en filialen voor Configuration Manager](learn-more-editions.md) en [veelgestelde vragen over Configuration Manager branches en licenties](product-and-licensing-faq.md)voor meer informatie over de opties voor Software Assurance en licenties.

De LTSB is gebaseerd op versie 1606. Deze vertakking ontvangt geen updates in de console die nieuwe functies leveren of bestaande mogelijkheden bijwerken. Er zijn echter essentiële beveiligingsfixes aanwezig. Als u de LTSB wilt installeren, moet u de [baseline-media](../servers/manage/updates.md#bkmk_Baselines) van versie 1606 gebruiken die u bij System Center 2016 ontvangt. Latere versies van de basis lijn bieden geen ondersteuning voor de installatie van de LTSB.

Als u de LTSB wilt installeren als een nieuwe site of als een upgrade van een ondersteunde System Center 2012 Configuration Manager-site, gebruikt u de versie 1606 [baseline media](../servers/manage/updates.md#bkmk_Baselines) die u bij System Center 2016 krijgt. U kunt basis lijn media gebruiken om een nieuwe site te installeren waarop versie 1606 van de huidige vertakking wordt uitgevoerd, of een nieuwe site die de langlopende onderhouds vertakking uitvoert.

> [!TIP]  
> Zie [System center 2016-documentatie](https://docs.microsoft.com/system-center/index)voor meer informatie over system Center 2016. In deze documentatie wordt ook beschreven hoe u System Center 2016 kunt ophalen. hiervoor is een micro soft-licentie overeenkomst of vergelijk bare rechten vereist.  
>  
> Als u Configuration Manager versie 1606 in het Volume Licensing Service Center (VLSC) wilt vinden, gaat u naar het tabblad **down loads en sleutels** van de [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), zoekt u naar `System Center 2016` en selecteert u **System Center 2016 Data Center** of **System Center 2016 Standard**.  
>  
> U kunt ook een Evaluation Edition van System Center 2016 ophalen uit het [Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  

### <a name="features-of-the-ltsb"></a>Functies van de LTSB

- Ontvangt updates in de console die essentiële beveiligingsfixes leveren.
- Biedt een installatie optie wanneer uw SA-overeenkomst of gelijkwaardige rechten voor Configuration Manager zijn verlopen.
- Ondersteunt upgrade (conversie) naar de huidige vertakking wanneer u een actuele SA-overeenkomst of gelijkwaardige rechten hebt voor Configuration Manager.

### <a name="ltsb-limitations"></a>LTSB-beperkingen

De LTSB is gebaseerd op de huidige branch versie 1606 en heeft de volgende beperkingen:

- De LTSB wordt ondersteund gedurende tien jaar kritieke beveiligings updates na de algemene Beschik baarheid (oktober 2016), waarna de ondersteuning voor deze vertakking verloopt. Zie [micro soft Lifecycle-beleid](https://support.microsoft.com/lifecycle)voor meer informatie over de levens cyclus van de ondersteuning.
- Ondersteunt een beperkte set lijst met server-en client besturingssystemen en gerelateerde technologieën, zoals SQL Server versies. Zie [ondersteunde configuraties voor de onderhouds branche voor de lange termijn](supported-configurations-for-ltsb.md)voor meer informatie.
- Er worden geen updates ontvangen voor nieuwe functies
- Biedt geen ondersteuning voor de volgende mogelijkheden:
  - Aan de Cloud gekoppelde functies, zoals co-beheer of desktop Analytics
  - On-premises MDM
  - Het Windows 10-onderhouds dashboard, onderhouds plannen of het semi-Annual-kanaal van Windows 10
  - Toekomstige releases van Windows 10 LTSB en Windows Server
  - Asset Intelligence
  - Alle functies van de voorlopige versie

### <a name="ltsb-update-options"></a>LTSB-Update opties

- U kunt uw LTSB-installatie converteren naar een huidige vertakkings installatie. Conversie naar de huidige vertakking wordt ondersteund vóór of na ondersteuning van de LTSB verloopt.

  Als u wilt converteren, moet u een actieve Software Assurance-overeenkomst met micro soft hebben. Raadpleeg voor meer informatie de volgende artikelen:

  - [De Long-term Servicing Branch upgraden naar de huidige vertakking](convert-to-current-branch.md)
  - [Licenties en vertakkingen voor Configuration Manager](learn-more-editions.md)
  - [Basis lijn-en update versies](../servers/manage/updates.md#bkmk_Baselines)

- Er is geen optie om de LTSB te converteren naar een Technical Preview-vertakking. Technical Preview branches zijn afzonderlijke installaties waarvoor geen licentie nodig is.

- U kunt een Evaluation Edition van de huidige vertakking niet upgraden naar een LTSB-installatie.

## <a name="technical-preview-branch"></a>Branch voor Technical Preview

De technische preview-vertakking is voor gebruik in een test omgeving. Meer informatie over de nieuwste functies die voor Configuration Manager worden ontwikkeld en hoe u deze kunt uitproberen. Het wordt niet ondersteund in een productie omgeving en u hebt geen licentie overeenkomst voor Software Assurance nodig.

Als u een nieuwe site wilt installeren waarop de Technical Preview-vertakking wordt uitgevoerd, gebruikt u de meest recente [basislijn media voor de Technical Preview-vertakking](../get-started/technical-preview.md#bkmk_install). Nadat u de Technical Preview-vertakking hebt geïnstalleerd, zijn nieuwe versies elke maand beschikbaar als console-updates.

### <a name="features-of-the-technical-preview-branch"></a>Functies van de Technical Preview-vertakking

- Gebaseerd op recente basislijn versies van de huidige vertakking
- Ontvangt updates in de console die uw installatie bijwerken naar de meest recente versie van de Technical Preview-vertakking
- Bevat nieuwe functies die worden ontwikkeld en waarvoor micro soft uw feedback wil
- Ontvangt updates die alleen van toepassing zijn op de Technical Preview-vertakking

### <a name="technical-preview-limitations"></a>Technische preview-beperkingen

- [Ondersteuning is beperkt](../get-started/technical-preview.md#bkmk_reqs), inclusief slechts één primaire site en Maxi maal 10 clients.  
- U kunt deze niet upgraden naar of migreren naar een huidige vertakking of LTSB-installatie.
- Biedt geen ondersteuning voor het volgende gedrag:
  - Migratie gebruiken om gegevens te importeren of exporteren naar een andere Configuration Manager-installatie
  - Upgrade uitvoeren van een eerdere versie van Configuration Manager
  - Installeren als een evaluatie-editie

Functies die voor het eerst in een Technical Preview-vertakking worden geïntroduceerd, worden vaak toegevoegd aan de huidige vertakking in een latere update. Elke nieuwe versie van de Technical Preview-vertakking bevat de functies van eerdere Technical Preview-filialen, zelfs nadat deze functies aan de huidige vertakking zijn toegevoegd.

Zie [Technical Preview voor Configuration Manager](../get-started/technical-preview.md)voor meer informatie.

### <a name="technical-preview-update-options"></a>Update opties voor Technical Preview

- U kunt elke update in de console installeren voor een nieuwe versie van de Technical Preview-vertakking.

- Er is geen optie om een technische preview-vertakking te converteren naar de huidige vertakking of LTSB.

## <a name="identify-your-version-and-branch"></a>Uw versie en vertakking identificeren

### <a name="version"></a>Versie

Als u de versie van uw site wilt controleren, gaat u in de-console naar **over Configuration Manager** in de linkerbovenhoek van de console. In dit dialoog venster wordt de **site versie**weer gegeven. Zie [basis lijn-en update versies](../servers/manage/updates.md#bkmk_Baselines)voor een lijst met site versies.

### <a name="branch"></a>Vertakking

Ga in de-console naar **beheer**  >  **site configuratie**  >  **sites**en open **hiërarchie-instellingen**om de vertakking van uw site te bevestigen. Als er een actieve optie is om te converteren naar de huidige vertakking, wordt de LTSB-versie uitgevoerd op de site. Wanneer de site de huidige vertakking uitvoert, schakelt de console deze optie uit.

Zie [basis lijn-en update versies](../servers/manage/updates.md#bkmk_Baselines)voor meer informatie over de verschillende versies van Configuration Manager.
