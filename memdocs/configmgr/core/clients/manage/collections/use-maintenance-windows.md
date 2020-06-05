---
title: Onderhouds Vensters gebruiken
titleSuffix: Configuration Manager
description: Gebruik verzamelingen en onderhouds Vensters om clients effectief te beheren in Configuration Manager.
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b81599c6c5e4dda418b69c6e3c6d3b8cd144253
ms.sourcegitcommit: 92e6d2899b1cf986c29c532d0cd0555cad32bc0c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84428543"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Onderhouds Vensters gebruiken in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Onderhouds Vensters gebruiken om te definiëren wanneer Configuration Manager invloed op de taken kan uitvoeren op apparaten. Onderhouds Vensters helpen u ervoor te zorgen dat wijzigingen in de client configuratie plaatsvinden tijdens tijden die geen invloed hebben op de productiviteit. Met Software Center kunnen gebruikers het volgende onderhouds venster van het apparaat zien op het tabblad **installatie status** . <!--1358131-->

De volgende taken ondersteunen onderhouds Vensters:

- Implementaties van toepassingen en pakketten

- Software-update-implementaties

- Implementatie en beoordeling van instellingen voor naleving

- Implementaties van besturings systeem en aangepaste taken reeks

Configureer onderhouds Vensters met een ingangs datum, een start-en eind tijd en een terugkeer patroon. De maximale duur van een venster moet minder dan 24 uur zijn. De console staat niet meer dan 24 uur één onderhouds venster toe. Als u bijvoorbeeld onderhoud per dag en zondag wilt toestaan, maakt u voor elke dag een onderhouds venster van 2 24 uur.<!-- MEMDocs#310 -->

Standaard is het opnieuw opstarten van een computer als gevolg van een implementatie niet toegestaan buiten een onderhouds venster, maar u kunt de standaard instelling onderdrukken. Onderhouds Vensters zijn alleen van invloed op het tijdstip waarop de implementatie wordt uitgevoerd. Implementaties die u configureert om lokaal te downloaden en uit te voeren, kunnen inhoud buiten het venster downloaden.

Wanneer een client lid is van een verzameling apparaten die een onderhouds venster heeft, wordt een implementatie alleen uitgevoerd als de Maxi maal toegestane uitvoerings tijd de duur van het venster niet overschrijdt. Als de implementatie niet kan worden uitgevoerd, genereert de client een waarschuwing. Vervolgens wordt de implementatie opnieuw uitgevoerd tijdens het volgende geplande onderhouds venster dat beschik bare tijd heeft.

## <a name="multiple-maintenance-windows"></a>Meerdere onderhouds Vensters

Wanneer een client computer lid is van meerdere verzamelingen apparaten die onderhouds vensters hebben, gelden deze regels:  

- Als de onderhouds vensters elkaar niet overlappen, behandelt de client deze als twee onafhankelijke onderhouds Vensters.

- Als de onderhouds vensters elkaar overlappen, behandelt de client deze als één venster voor het hele tijdstip van Windows. U kunt bijvoorbeeld twee onderhouds vensters maken voor een verzameling. De eerste is van kracht van 6:00 tot 7:00 en de tweede is van kracht vanaf 6:30 tot 7:30. Omdat deze 30 minuten overlappen, is de daad werkelijke duur van het gecombineerde onderhouds venster 90 minuten van 6:00 tot 7:30.

Wanneer een gebruiker een toepassing installeert vanuit software Center, start de client deze onmiddellijk. Hiermee wordt de bedoeling van de gebruiker in de rang orde van de beheerder.

Als een toepassings implementatie met het doel **vereist** de installatie deadline bereikt tijdens de niet-kantoor uren die een gebruiker configureert in Software Center, installeert de-client de toepassing. Hiermee wordt de bedoeling van de beheerder van de gebruiker prioriteit.

Met meerdere onderhouds Vensters installeert de client standaard alleen software-updates tijdens **Software-update** type Windows. Alle onderhouds Vensters voor **implementaties** worden genegeerd, tenzij dit het enige type is. U kunt dit gedrag configureren met de volgende client instelling in de groep **software-updates** : **installatie van software-updates inschakelen in het onderhouds venster ' alle implementaties ' wanneer het onderhouds venster van software-update beschikbaar is**. Zie [over client instellingen](../../deploy/about-client-settings.md#bkmk_SUMMaint)voor meer informatie.<!-- SCCMDocs#1317 -->

> [!NOTE]
> Deze instelling is ook van toepassing op onderhouds Vensters die u configureert voor het Toep assen op **taken reeksen**.<!-- SCCMDocs-pr #4596 -->
>
> Als op de client alleen een venster met **implementaties** beschikbaar is, worden software-updates of taken reeksen nog steeds in dat venster geïnstalleerd.

## <a name="configure-maintenance-windows"></a>Onderhouds Vensters configureren

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** .

1. Selecteer het knoop punt **apparaat verzamelingen** en selecteer vervolgens een verzameling.

    > [!NOTE]
    > U kunt geen onderhouds vensters maken voor de verzameling **alle systemen** .

1. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.

1. Ga naar het tabblad **onderhouds Vensters** en selecteer het pictogram **Nieuw** .

    1. Geef een unieke **naam** op voor dit onderhouds venster voor de verzameling.

    1. De **tijd** instellingen configureren:

        - **Ingangs datum**: de datum waarop het onderhouds venster wordt gestart. De standaard waarde is de huidige datum.

        - **Begin** en **einde**: de begin-en eind tijd van het onderhouds venster. De **duur** van het venster wordt berekend. De minimale duur is vijf minuten en het maximum is 24 uur. De standaard duur is drie uur, van 01:00 tot 04:00.

        - **Coordinated Universal Time (UTC)**: Schakel deze optie in als de client de begin-en eind tijd in de UTC-tijd zone moet interpreteren. Voor regionale of wereld wijd gedistribueerde apparaten in dezelfde verzameling wordt met deze optie het onderhouds venster zo ingesteld dat het tegelijkertijd op alle apparaten in de verzameling wordt uitgevoerd. Schakel deze optie uit als de client de lokale tijd zone van het apparaat moet gebruiken. Deze optie is standaard uitgeschakeld.

    1. Het terugkeer patroon configureren. De standaard waarde is eenmaal per week op de huidige dag van de week.

    1. **Dit schema Toep assen op**: standaard is het venster van toepassing op **alle implementaties**. U kunt software- **updates** of **taken reeksen** selecteren om verder te bepalen welke implementaties tijdens dit venster worden uitgevoerd.

        > [!TIP]
        > Als u meerdere onderhouds Vensters van verschillende typen op dezelfde verzameling configureert, moet u ervoor zorgen dat u bekend bent met het gedrag van de client. Zie [meerdere onderhouds Vensters](#multiple-maintenance-windows)voor meer informatie.

1. Selecteer **OK** om op te slaan en het venster te sluiten.

Op het tabblad **onderhouds Vensters** van de verzameling eigenschappen worden alle geconfigureerde vensters weer gegeven.

## <a name="use-powershell"></a><a name="bkmk_powershell"></a>Power shell gebruiken

Power shell kan worden gebruikt voor het configureren van onderhouds Vensters. Raadpleeg voor meer informatie de volgende artikelen:

- [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow?view=sccm-ps)
- [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow?view=sccm-ps)
- [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow?view=sccm-ps)
- [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow?view=sccm-ps)
