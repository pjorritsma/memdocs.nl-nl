---
title: De LTSB beheren
titleSuffix: Configuration Manager
description: Beheer verschillen voor de LTSB van System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86e7579832a5a59c3609d24744eb646e1a4c1fd1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722702"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>De Long Term Servicing Branch van Configuration Manager beheren

*Van toepassing op: System Center Configuration Manager (onderhouds branche voor de lange termijn)*

Wanneer u de Long-term Servicing Branch (LTSB) van System Center Configuration Manager gebruikt, kunt u aan de hand van de volgende belang rijke wijzigingen begrijpen die van invloed zijn op hoe u uw infra structuur beheert.

Omdat de LTSB gelijk is aan Current Branch versie 1606 (met enkele uitzonde ringen zoals intune-integratie en Cloud functies), zijn de meeste taken die u voor planning, implementatie, configuratie en dagelijks beheer gebruikt.

De LTSB ondersteunt bijvoorbeeld hetzelfde aantal sites, site typen, clients en algemene infra structuur als de Current Branch. Daarom gebruikt u de richt lijnen die zijn gevonden in de onderwerpen over het plannen en ontwerpen van sites en hiërarchieën voor de Current Branch. Op vergelijk bare wijze, voor functies met de LTSB die door beide branches worden ondersteund, zoals software-updates of implementatie van het besturings systeem, gebruikt u de richt lijnen in deze secties van de Current Branch documentatie met de voor behoud van geen toegang tot de functie wijzigingen die zijn geïntroduceerd na versie 1606 van de Current Branch.

De volgende secties bevatten informatie over het beheren van taken die niet vergelijkbaar zijn.

## <a name="updates-and-servicing"></a>Updates en onderhoud
Alleen essentiële beveiligings updates worden beschikbaar gesteld als updates in de console in de LTSB.  

Informatie over regel matige updates voor de volgende Current Branch releases is zichtbaar in de-console, maar worden niet beschikbaar gesteld voor de LTSB. Ze worden niet gedownload en kunnen niet worden geïnstalleerd.

Ter ondersteuning van updates in de console voor kritieke beveiligingsfixes, moet een LTSB-site het gebruik van [het service verbindings punt](../servers/deploy/configure/about-the-service-connection-point.md)gebruiken. U kunt deze site systeemrol in de modus offline of online configureren, zoals wordt gedaan voor de Current Branch. De LTSB verzamelt en verzendt dezelfde telemetrie en gebruiks gegevens als de Current Branch.

De LTSB ondersteunt het gebruik van het installatie programma voor hotfixes en het hulp programma voor het registreren van updates, zoals gedocumenteerd voor de Current Branch.

Zie [updates voor Configuration Manager](../servers/manage/updates.md)voor algemene informatie over updates en onderhoud.


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Wijzigingen voor site-uitbrei ding en de CD. Meest recente map
Wanneer u de LTSB uitvoert en een zelfstandige primaire site uitbreidt door een nieuwe centrale beheer site te installeren, moet u Setup en de bron bestanden van versie 1606 Baseline media gebruiken. Voor de Current Branch voert u Setup uit en gebruikt u de bron bestanden van de CD. Meest recente map.

Hoewel u Setup niet uitvoert voor site-uitbrei ding vanaf de CD. Meest recente map, kunt u de CD blijven gebruiken. De meest recente map voor site Recovery en voor het installeren van een nieuwe onderliggende primaire site wanneer uw eerste LTSB-site een centrale beheer site is.

Zie [een zelfstandige primaire site uitbreiden](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)voor meer informatie over site-uitbrei ding. Voor meer informatie over de CD. Meest recente map, raadpleegt u [de cd. Meest recente map](../servers/manage/the-cd.latest-folder.md).


## <a name="recovery"></a>Herstel
Wanneer u een site herstelt, moet u de site of site database herstellen naar de oorspronkelijke vertakking. U kunt een Current Branch-site database niet herstellen naar een LTSB-installatie of andersom.
