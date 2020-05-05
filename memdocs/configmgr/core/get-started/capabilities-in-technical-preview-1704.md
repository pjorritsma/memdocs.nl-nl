---
title: Mogelijkheden van Technical Preview 1704
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview voor Configuration Manager, versie 1704.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721407"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1704 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1704. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u het inleidende onderwerp, [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md), om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.    


**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Android-apps configureren met het app-configuratie beleid
U kunt het app-configuratie beleid in Configuration Manager gebruiken om instellingen te distribueren die mogelijk vereist zijn wanneer een gebruiker een app uitvoert op Android for work-apparaten. Het configuratie beleid voor Android-apps is alleen beschikbaar op apparaten met Android for work en is van toepassing op goedgekeurde apps in de Play for work-Store.

### <a name="try-it-out"></a>Uitproberen                 

Kies in de Configuration Manager-console **software bibliotheek** > **toepassings beheer** > **app configuratie beleid** en kies **app-configuratie beleid maken**. Op de pagina **Algemeen** van de wizard kunt u nu **een type configuratie beleid selecteren**. Geef het platform op waarop het app-configuratie beleid is gericht: **configuratie beleid voor Android for work-apps**. U kunt vervolgens **naam-en waardeparen opgeven** of **naar een JSON-bestand met een eigenschappen lijst bladeren**. Het nieuwe app-configuratie beleid wordt weer gegeven in de werk ruimte **software bibliotheek** in het knoop punt **app-configuratie beleid** . Als u een app-configuratie beleid wilt koppelen aan de implementatie van een Android for work-app, implementeert u de toepassing zoals u dat normaal zou doen met behulp van de procedure in het onderwerp [toepassingen implementeren](../../apps/deploy-use/deploy-applications.md) .

## <a name="hardware-inventory-collects-secure-boot-information"></a>Hardware-inventaris verzamelt informatie over beveiligd opstarten
Met de hardware-inventarisatie wordt nu informatie verzameld over of beveiligd opstarten is ingeschakeld op clients. Deze informatie wordt opgeslagen in de klasse **SMS_Firmware** (geïntroduceerd in versie 1702) en is standaard ingeschakeld in hardware-inventaris. Zie [hardware-inventaris configureren](../clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over hardware-inventarisatie.

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Onderliggende taken reeksen toevoegen aan een taken reeks
In deze versie kunt u een nieuwe taken reeks stap toevoegen waarmee een andere taken reeks wordt uitgevoerd, waarmee een bovenliggende/onderliggende relatie tussen de taken reeksen wordt gemaakt. Zo kunt u meer modulaire taken reeksen maken die u opnieuw kunt gebruiken.  

Houd rekening met het volgende wanneer u een onderliggende taken reeks toevoegt aan een taken reeks:

- De bovenliggende en onderliggende taken reeks worden effectief gecombineerd tot één beleid dat door de client wordt uitgevoerd.
- Het is niet mogelijk om een onderliggende taken reeks toe te voegen die een bovenliggend item is van een andere taken reeks.
- De omgeving is wereld wijd. Als een variabele bijvoorbeeld is ingesteld door de bovenliggende taken reeks en vervolgens wordt gewijzigd door de onderliggende taken reeks, blijft de variabele gewijzigd. Als de onderliggende taken reeks een nieuwe variabele maakt, is de variabele ook beschikbaar voor de resterende stappen in de bovenliggende taken reeks.
- Status berichten worden per normale verzen ding verzonden voor een enkele taken reeks bewerking.
- De taken reeksen schrijven vermeldingen naar het bestand bestand smsts. log, met nieuwe logboek vermeldingen die duidelijk worden gemaakt wanneer een onderliggende taken reeks wordt gestart.
- In de Technical Preview voor Configuration Manager versie 1704, als de onderliggende taken reeksen naar een pakket verwijzen en u de bovenliggende taken reeks uitvoert vanuit software Center, wordt de inhoud van het pakket niet door de client gevonden wanneer de onderliggende taken reeks wordt uitgevoerd. In dit scenario moet u de taken reeks uitvoeren vanaf media (opstart media, PXE, enz.).  

    Als de onderliggende taken reeks gebruikmaakt van stappen als **opdracht regel uitvoeren** (zonder pakket verwijzing), **Format**, **BitLocker**, enzovoort, wordt de taken reeks uitgevoerd vanuit software Center.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Een onderliggende taken reeks toevoegen aan een taken reeks
1. Klik in de taken reeks editor op **toevoegen**, selecteer **Algemeen**en klik op **taken reeks uitvoeren**.
2. Klik op **Bladeren** om de onderliggende taken reeks te selecteren.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Opstart installatie kopieën opnieuw laden met de huidige versie van Windows PE
Wanneer u **Update distributie punten** op een geselecteerde opstart installatie kopie uitvoert, kunt u nu de nieuwste versie van Windows PE (uit de installatiemap van Windows ADk) in de opstart installatie kopie opnieuw laden. Op de pagina **Algemeen** van de wizard vindt u informatie over de Windows ADk-versie die is geïnstalleerd op de site server, de Windows ADk-versie van waaruit Windows PE is gebruikt in de opstart installatie kopie en de versie van de Configuration Manager-client. U kunt deze informatie gebruiken om u te helpen beslissen of u de opstart installatie kopie opnieuw wilt laden. Er is ook een nieuwe kolom (**client versie**) toegevoegd wanneer u opstart installatie kopieën bekijkt in het knoop punt **opstart installatie kopieën** , zodat u weet welke versie van de Configuration Manager-client elke opstart installatie kopie gebruikt.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Een opstart installatie kopie opnieuw laden met de huidige versie van Windows PE

1. Ga in de Configuration Manager-console naar installatie**kopieën**van het**besturings systeem** >  **software bibliotheek** > .
2. Selecteer een installatie kopie en klik op **distributie punten bijwerken**.
3. Selecteer op de pagina **Algemeen** van de wizard **opstart installatie kopie opnieuw laden met de huidige versie van Windows PE van de geïnstalleerde Windows ADk**.

## <a name="improvements-to-operating-system-deployment"></a>Verbeteringen in de implementatie van besturings systemen
We hebben de volgende verbeteringen aangebracht in de implementatie van het besturings systeem, die het resultaat zijn van de feedback van uw gebruikers stem.

- [Nieuwe kolom met de **besturingssysteem versie** voor installatie kopieën van besturings systemen](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f): er is een nieuwe kolom met **de naam van** het besturings systeem toegevoegd voor het weer geven van de besturingssysteem versie voor de installatie kopie wanneer u gegevens in de knoop punten **installatie kopieën van besturings systeem** en **upgrade pakketten voor het besturings systeem** bekijkt. Alleen de versie van de eerste index in de. WIM wordt weer gegeven. Ga naar het tabblad **Details** voor de installatie kopie om de versies van het besturings systeem voor andere indexen te controleren.

- [Efficiëntere logboek registratie in bestand smsts. log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless): vanaf deze versie schrijven we geen vermeldingen meer naar het bestand bestand smsts. log voor informatie over CCM_CIVersionInfo. PolicyID. Vóór deze versie kunnen er veel vermeldingen worden gemaakt met deze informatie, waardoor het moeilijk is om meer relevante informatie te vinden in het logboek bestand.
