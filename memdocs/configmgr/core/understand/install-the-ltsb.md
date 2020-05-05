---
title: 'Een site installeren met behulp van de 1606-Baseline media '
titleSuffix: Configuration Manager
description: Installeer of upgrade naar de LTSB voor System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722800"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Installeren en upgraden met de versie 1606-basis lijn media

*Van toepassing op: System Center Configuration Manager (onderhouds branche voor de lange termijn)*

Wanneer u Setup uitvoert vanaf de baseline media van versie 1606 voor Configuration Manager, kunt u een langlopende onderhouds branche site van System Center Configuration Manager installeren.

De basislijn media zijn beschikbaar op DVD als onderdeel van micro soft System Center 2016, of van de System Center Configuration Manager Long-term Servicing Branch versie 1606. Zie [basis lijn-en update versies](../servers/manage/updates.md#bkmk_Baselines)voor meer informatie over basislijn media.


Wanneer u versie 1606-basis media gebruikt, is de site die u installeert of waarmee u een upgrade uitvoert:
- Een *Current Branch site* die gelijk is aan een site die voor het eerst is geïnstalleerd met behulp van de 1511-basislijn media en vervolgens is bijgewerkt naar versie 1606 plus het 1606 Hotfix Rollup-KB3186654.
- Een *LTSB-site* die gelijk is aan de current branch-site waarop versie 1606 plus de 1606 Hotfix Rollup-KB3186654 wordt uitgevoerd. De basislijn media bevatten al het hotfixcombinatiepakket.  Maar de LTSB biedt geen ondersteuning voor alle functies en mogelijkheden die beschikbaar zijn met de Current Branch, zoals wordt beschreven in [Inleiding tot de lange termijn onderhouds vertakking van System Center Configuration Manager](introduction-to-the-ltsb.md).

Als u niet bekend bent met de verschillende branches van Configuration Manager, raadpleegt u [welke vertakking van Configuration Manager moet ik gebruiken](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Wijzigingen in Setup met de 1606-basis lijn media
De 1606-Baseline Media introduceert de volgende wijzigingen in de configuratie voor Configuration Manager.

### <a name="branch-and-edition"></a>Vertakking en editie
Wanneer u het installatie programma uitvoert, wordt u nu weer gegeven met een licentie pagina waar u de vertakking van Configuration Manager kunt selecteren die u wilt installeren. U kunt kiezen voor de Current Branch of LTSB als een gelicentieerde installatie, of u kunt een evaluatie versie van de Current Branch kiezen als een niet-gelicentieerde installatie.

Zie [Licentiëring en vertakkingen voor Configuration Manager](learn-more-editions.md)voor meer informatie.

### <a name="software-assurance-expiration"></a>Verval datum Software Assurance
Tijdens de installatie hebt u de mogelijkheid om de waarde voor de **verval datum van de Software Assurance** in te voeren. Dit is een optionele waarde die u kunt opgeven als een handige herinnering.

> [!NOTE]
> Micro soft valideert niet de verval datum die u invoert en gebruikt deze datum niet voor het valideren van licenties.  In plaats daarvan kunt u deze gebruiken als herinnering voor uw verval datum. Dit is handig omdat Configuration Manager regel matig controleert of er online nieuwe software-updates beschikbaar zijn en dat de licentie status van uw Software Assurance actueel moet zijn om deze aanvullende updates te kunnen gebruiken.    

- U kunt de datum waarde opgeven op de pagina **product code** van de installatie wizard wanneer u het installatie programma uitvoert vanaf de Configuration Manager versie 1606-Baseline media.
- U kunt deze datum ook opgeven door de **Eigenschappen** > van de hiërarchie-instellingen te**selecteren in de** Configuration Manager-console.

Zie ' Software Assurance agreements ' in [licenties en filialen voor Configuration Manager](learn-more-editions.md)voor meer informatie.


### <a name="additional-pre-upgrade-configurations"></a>Aanvullende configuraties vóór de upgrade
Voordat u een upgrade van System Center 2012 Configuration Manager naar de LTSB, moet u de volgende aanvullende stappen uitvoeren als onderdeel van de controle lijst vóór de upgrade.  
Verwijder de site systeem rollen die niet worden ondersteund door de LTSB:
- Asset Intelligence-synchronisatiepunt
- Microsoft Intune-connector
- Clouddistributiepunten

Zie [upgrade naar Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md)voor meer informatie.


### <a name="new-scripted-installation-options"></a>Nieuwe installatie opties met script
De versie 1606-Baseline Media ondersteunt een nieuwe sleutel voor een script bestand voor installatie zonder toezicht voor installaties van een nieuwe site op het hoogste niveau. Dit geldt voor het installeren van een nieuwe zelfstandige primaire site of het toevoegen van een centrale beheer site als onderdeel van een scenario voor site-uitbrei ding.

Wanneer u een gelicentieerde vertakking installeert met behulp van een script zonder toezicht, moet u de volgende sectie, sleutel namen en waarden toevoegen aan de sectie opties van uw script. U hoeft deze waarden niet te gebruiken om een script te maken voor de installatie van een Evaluation Edition van de Current Branch:  

 **SABranchOptions**
- **Naam sleutel: SAActive**
  - Waarden: 0 of 1.  
  - Details: 0 installeert een niet-gelicentieerde evaluatie versie van Current Branch en 1 installeert een gelicentieerde versie.   

- **CurrentBranch**
  - Waarden: 0 of 1.  
  - Details: 0 Hiermee wordt de Long-term Servicing-vertakking geïnstalleerd en 1 de Current Branch geïnstalleerd.  

Als u bijvoorbeeld een gelicentieerde Current Branch-editie wilt installeren, gebruikt u:

**Naam sleutel: SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** werkt alleen met de installatie van de basislijn media. Het is niet van toepassing wanneer u het installatie programma uitvoert vanaf de CD. Meest recente map van een site die u eerder hebt geïnstalleerd met behulp van versie 1606 Baseline media.
>
> **SABranchOptions** is niet van toepassing op script upgrades van System Center 2012 Configuration Manager en resulteert altijd in de current branch.

Zie [een opdracht regel gebruiken voor het installeren van Configuration Manager-sites](../servers/deploy/install/use-a-command-line-to-install-sites.md)voor meer informatie.


## <a name="install-a-new-site"></a>Een nieuwe site installeren
Wanneer u de 1606-basis lijn gebruikt om een nieuwe site van een van beide vertakkingen te installeren, gebruikt u de procedures voor het plannen, voorbereiden en installeren van sites die worden beschreven in het onderwerp [installatie van Configuration Manager sites](../servers/deploy/install/installing-sites.md) met de toevoeging van de volgende overwegingen voor Setup:

- Tijdens de installatie moet u de vertakking van Configuration Manager kiezen die u wilt installeren, en kunt u details opgeven voor uw Software Assurance-overeenkomst.
- Alle sites in dezelfde hiërarchie moeten dezelfde vertakking uitvoeren. Het is niet mogelijk om een hiërarchie te hebben met een combi natie van LTSB en Current Branch op verschillende sites.
- Nieuwe script installatie. Zie ' nieuwe script installatie opties ' eerder in dit artikel voor meer informatie.

## <a name="expand-a-stand-alone-primary-site"></a>Een zelfstandige primaire site uitbreiden
U kunt een zelfstandige primaire site uitbreiden waarop de LTSB wordt uitgevoerd.  Het proces is niet anders dan dat voor een Current Branch site wordt gebruikt met één voor behoud:

- Wanneer u de nieuwe centrale beheer site installeert, moet u het installatie programma gebruiken vanaf de oorspronkelijke bron media die u hebt gebruikt om de LTSB-site te installeren. Setup uitvoeren vanaf de CD. De meest recente map voor dit scenario wordt niet ondersteund.

Zie ' een zelfstandige primaire site uitbreiden ' in [een site installeren met de wizard Setup](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md)voor meer informatie over het uitbreiden van een site.

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Upgrade van System Center 2012 Configuration Manager
Wanneer u een upgrade uitvoert van System Center 2012 Configuration Manager, gebruikt u de site planning, voor bereiding en procedures zoals beschreven in het onderwerp [upgraden naar Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md) , maar met de volgende wijzigingen:

**Voer een upgrade uit naar de Current Branch:**
- Tijdens de installatie moet u de Current Branch kiezen en kunt u details opgeven voor uw Software Assurance-overeenkomst.
- Nieuwe script installatie. Zie ' nieuwe script installatie opties ' eerder in dit artikel voor meer informatie.

**Voer een upgrade uit naar de LTSB:**  
- Aanvullende stappen die u moet volgen in de controle lijst vóór de upgrade.
- Tijdens de installatie moet u de LTSB kiezen en kunt u details opgeven voor uw Software Assurance-overeenkomst.
- U kunt alleen een site bijwerken waarop System Center 2012 Configuration Manager met Service Pack 1, System Center 2012 Configuration Manager met Service Pack 2, System Center 2012 R2 Configuration Manager met Service Pack 1 of System Center 2012 R2 Configuration Manager zonder Service Pack wordt uitgevoerd.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>In-place upgrade paden voor de 1606-basislijn media
U kunt de 1606-basislijn media gebruiken om het volgende bij te werken naar een gelicentieerde versie van Configuration Manager:
- System Center 2012 R2 Configuration Manager met Service Pack 1
- System Center 2012 R2 Configuration Manager zonder Service Pack (hiervoor is het gebruik van de basislijn media vereist voor versie 1606 die opnieuw is uitgebracht op 15 december 2016.)
- System Center 2012 Configuration Manager met Service Pack 2
- System Center 2012 Configuration Manager met Service Pack 1 (hiervoor is het gebruik van de basislijn media vereist voor versie 1606 die opnieuw is uitgebracht op 15 december 2016.)


U kunt deze media ook gebruiken om een niet-gelicentieerde evaluatie versie van Current Branch te upgraden naar een volledig gelicentieerde versie van de Current Branch.

Deze media biedt geen ondersteuning voor de upgrade van:
- Andere versies van System Center 2012 Configuration Manager.
- Configuration Manager 2007 of eerder.
- Een release Candi date-installatie van Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Over de CD. Meest recente map en de LTSB
Hier volgen enkele beperkingen voor het gebruik van het medium dat Configuration Manager maakt in de CD. Meest recente map op de site server. Deze limieten zijn van toepassing op sites waarop de LTSB wordt uitgevoerd:

Media op de CD. De meest recente map wordt ondersteund voor:
- Site Recovery.
- Site onderhoud.
- Extra onderliggende primaire sites installeren.

Media op de CD. De meest recente map wordt niet ondersteund voor:  
- Een centrale beheer site installeren als onderdeel van een scenario voor site-uitbrei ding.

Zie de CD voor meer informatie [. Meest recente map](../servers/manage/the-cd.latest-folder.md).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Back-ups maken, herstellen en site onderhoud voor de LTSB
Voor het maken van een back-up, het herstellen of uitvoeren van site onderhoud op een site waarop de LTSB wordt uitgevoerd, gebruikt u de richt lijnen en procedures van [back-up en herstel voor Configuration Manager](../servers/manage/backup-and-recovery.md).  

Gebruik Configuration Manager Setup vanaf de CD. Meest recente map van de back-up van uw LTSB-site.
