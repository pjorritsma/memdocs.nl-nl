---
title: Implementaties met een hoog risico beheren
titleSuffix: Configuration Manager
description: Configureer site-instellingen voor de implementatie verificatie in Configuration Manager om beheerders te waarschuwen als ze een implementatie met een hoog risico maken.
ms.date: 02/26/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f1498c383f9b02f7f322de3ba5708351e84c3b7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81719986"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Instellingen voor het beheren van implementaties met een hoog risico voor Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met Configuration Manager kunt u site-instellingen voor de *implementatie verificatie* configureren. Met deze instellingen worden beheerders gewaarschuwd als ze een taken reeks implementatie met een hoog risico maken. Een implementatie met een hoog risico is:  

- Een implementatie die automatisch wordt geïnstalleerd  

- Een implementatie die potentieel ongewenste gevolgen kan hebben  

Een taken reeks met het doel **vereist** voor het implementeren van een besturings systeem wordt bijvoorbeeld beschouwd als een hoog risico.  

> [!WARNING]
> Als u PXE-implementaties gebruikt en de hardware van het apparaat configureert met de netwerk adapter als het eerste opstart apparaat, kunnen deze apparaten automatisch een taken reeks voor besturingssysteem implementatie starten zonder tussen komst van de gebruiker. Deze configuratie wordt niet beheerd door implementatie verificatie. Hoewel deze configuratie het proces kan vereenvoudigen en de gebruikers interactie vermindert, wordt het apparaat voor een groter risico voor onbedoelde herinstallatie kopieën geplaatst.

## <a name="deployment-verification-settings"></a><a name="bkmk_settings"></a>Instellingen voor verificatie van implementatie

Om het risico van een implementatie met een ongewenst hoog risico te beperken, kunt u grootte limieten configureren in de instellingen voor de verificatie van de implementatie:  

- **Limieten voor verzamelings grootte**: wanneer u een implementatie maakt, moet u verzamelingen verbergen die meer clients bevatten dan uw limiet.  

  - **Standaard grootte**: wanneer u een implementatie maakt, worden in deze instelling standaard verzamelingen verborgen die meer clients bevatten dan deze limiet. U kunt deze verzamelingen nog steeds zien tijdens het maken van de implementatie, maar deze worden standaard verborgen. De standaard waarde is **100**. Als u deze instelling wilt negeren, voert u de waarde **0**in.  

  - **Maximum grootte**: wanneer u een implementatie maakt, worden verzamelingen die meer clients overschrijden, altijd verborgen. De standaard waarde is **0**, waarmee deze instelling wordt genegeerd. De waarde voor **Maximumgrootte** moet groter zijn dan de waarde voor **Standaardgrootte** .  

    Stel bijvoorbeeld de **standaard grootte** in op 100 en de **maximale grootte** op 1000. Wanneer u een implementatie met een hoog risico maakt, worden in het venster **verzameling selecteren** alleen verzamelingen weer gegeven die minder dan 100 clients bevatten. Als u de instelling uitschakelt om **verzamelingen te verbergen met een aantal leden dat groter is dan de minimale configuratie van de site**, worden in het venster verzamelingen weer gegeven die minder dan 1000 clients bevatten.  

- **Verzamelingen met site systeem servers**: wanneer de doel verzameling een computer met een site systeemrol bevat, blok keren implementaties of vereisen verificatie voordat de implementatie wordt gemaakt. Wanneer een implementatie wordt geblokkeerd, selecteert u een andere verzameling die voldoet aan de verificatie criteria voor de implementatie om door te gaan met het maken van de implementatie.  

> [!NOTE]
> Implementaties met een hoog risico zijn altijd beperkt tot aangepaste verzamelingen, verzameling die uzelf maakt en de ingebouwde verzameling **Onbekende computers** . Wanneer u een implementatie met een hoog risico maakt, kunt u geen ingebouwde verzameling selecteren, zoals **alle systemen**.  

## <a name="configure-deployment-verification"></a>Verificatie van de implementatie configureren

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **site configuratie**uit, selecteer **sites**en selecteer vervolgens de primaire site die u wilt configureren.

2. Selecteer in het lint **Eigenschappen**en schakel vervolgens over naar het tabblad **verificatie van implementatie** .

3. Configureer de [instellingen](#bkmk_settings) die u wilt gebruiken en selecteer **OK** om de configuratie op te slaan en de eigenschappen te sluiten.

## <a name="next-steps"></a>Volgende stappen

[Taken reeksen beheren-instellingen voor hoge impact](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#high-impact-settings)

[Sites en hiërarchieën configureren](../deploy/configure/configure-sites-and-hierarchies.md)
