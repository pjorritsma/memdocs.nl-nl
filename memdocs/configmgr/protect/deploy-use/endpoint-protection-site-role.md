---
title: Site systeemrol Endpoint Protection punt maken
titleSuffix: Configuration Manager
description: Meer informatie over het configureren van Endpoint Protection voor het beheren van beveiliging en malware op Configuration Manager-client computers.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a8714f5bacf97e440bae07834ee6df5430a3d37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710830"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Een sitesysteemrol maken voor het Endpoint Protection-punt

*Van toepassing op: Configuration Manager (huidige vertakking)*

De sitesysteemrol Endpoint Protection-punt moet zijn geïnstalleerd voordat u Endpoint Protection kunt gebruiken. Het moet slechts op één sitesysteemserver en op het hoogste niveau in de hiërarchie op een centrale beheersite of een zelfstandige primaire site worden geïnstalleerd.

Gebruik een van de volgende procedures, afhankelijk van het feit of u een nieuwe site systeem server voor Endpoint Protection wilt installeren of een bestaande site systeem server wilt gebruiken:
- [Installeren op een nieuwe site systeem server](#new-site-system-server)
- [Installeren op een bestaande site systeem server](#existing-site-system-server)

> [!IMPORTANT]
>  Wanneer u een Endpoint Protection punt installeert, wordt er een Endpoint Protection-client geïnstalleerd op de server die als host fungeert voor het Endpoint Protection punt. Services en scans op deze client worden uitgeschakeld zodat het in combinatie met een bestaande anti-malwareoplossing op de server kan worden gebruikt. Als u deze server later inschakelt voor beheer door Endpoint Protection en de optie selecteert om antimalware-oplossing van derden te verwijderen, wordt het product van derden niet verwijderd. U moet dit product handmatig verwijderen.

## <a name="new-site-system-server"></a>Nieuwe site systeem server

1.  Klik op **Beheer**in de Configuration Manager-console.

2.  Vouw in de werkruimte **Beheer****Siteconfiguratie**uit en klik op **Servers en sitesysteemrollen**.

3.  Klik op **Sitesysteemserver maken** in het tabblad **Start** , in de groep **Maken**.

4.  Configureer de algemene instellingen voor het sitesysteem op de pagina **Algemeen** en klik vervolgens op **Volgende**.

5.  Selecteer **Endpoint Protection-punt** in de lijst met beschikbare rollen op de pagina **Systeemrolselectie** en klik vervolgens op **Volgende**.

6.  Schakel op de pagina **Endpoint Protection** het selectievakje **Ik ga akkoord met de licentievoorwaarden van Endpoint Protection** in en klik vervolgens op **Volgende**.

    > [!IMPORTANT]
    >  U kunt Endpoint Protection niet gebruiken in Configuration Manager tenzij u akkoord gaat met de licentie voorwaarden.

7.  Selecteer op de pagina **Cloud Protection Service** het niveau van de informatie die u naar micro soft wilt verzenden om nieuwe definities te ontwikkelen en klik vervolgens op **volgende**.

    > [!NOTE]
    >  Met deze optie configureert u de instellingen van de Cloud Protection-Service (voorheen bekend als Microsoft Active Protection Service of MAPS) die standaard worden gebruikt. U kunt vervolgens aangepaste instellingen configureren voor elk beleid dat u maakt. Meld u aan bij de Cloud Protection-Service, zodat u uw computers beter kunt beveiligen door micro soft te voorzien van malware-voor beelden die micro soft helpen om antimalware-definities up-to-date te houden. Wanneer u deelneemt aan Cloud Protection Service, kan de Endpoint Protection-client bovendien de service voor dynamische hand tekeningen gebruiken om nieuwe definities te downloaden voordat ze naar Windows Update worden gepubliceerd. Zie [antimalware-beleid voor Endpoint Protection maken en implementeren](endpoint-antimalware-policies.md)voor meer informatie.

8.  Voltooi de wizard.


## <a name="existing-site-system-server"></a>Bestaande site systeem server

1.  Klik op **Beheer**in de Configuration Manager-console.

2.  Vouw **site configuratie**uit in de werk ruimte **beheer** , klik op **servers en site systeem rollen**en selecteer vervolgens de server die u wilt gebruiken voor Endpoint Protection.

3.  Klik op **Sitesysteemrollen toevoegen** in het tabblad **Start** in de groep **Server**.

4.  Configureer de algemene instellingen voor het sitesysteem op de pagina **Algemeen** en klik vervolgens op **Volgende**.

5.  Selecteer **Endpoint Protection-punt** in de lijst met beschikbare rollen op de pagina **Systeemrolselectie** en klik vervolgens op **Volgende**.

6.  Schakel op de pagina **Endpoint Protection** het selectievakje **Ik ga akkoord met de licentievoorwaarden van Endpoint Protection** in en klik vervolgens op **Volgende**.

    > [!IMPORTANT]
    >  U kunt Endpoint Protection niet gebruiken in Configuration Manager tenzij u akkoord gaat met de licentie voorwaarden.

7.  Selecteer op de pagina **Cloud Protection Service** het niveau van de informatie die u naar micro soft wilt verzenden om nieuwe definities te ontwikkelen en klik vervolgens op **volgende**.

    > [!NOTE]
    >  Met deze optie configureert u de instellingen van de Cloud Protection-Service (voorheen bekend als MAPS) die standaard worden gebruikt. U kunt aangepaste instellingen configureren voor elk anti-malwarebeleid dat u maakt. Zie [antimalware-beleid voor Endpoint Protection maken en implementeren](endpoint-antimalware-policies.md)voor meer informatie.

8.  Voltooi de wizard.
