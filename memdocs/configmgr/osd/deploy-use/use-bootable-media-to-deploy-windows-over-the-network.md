---
title: Opstartbare media gebruiken om Windows te implementeren via het netwerk
titleSuffix: Configuration Manager
description: Gebruik opstart bare media-implementaties in Configuration Manager om het besturings systeem te implementeren wanneer de doel computer wordt gestart.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124753"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Opstart bare media gebruiken om Windows via het netwerk te implementeren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Opstart bare media bevatten alleen de opstart installatie kopie en een verwijzing naar de taken reeks. De installatie kopie van het besturings systeem en andere inhoud waarnaar wordt verwezen, wordt gedownload van het netwerk. Omdat het opstart bare medium niet veel inhoud bevat, kunt u de taken reeks en de meeste inhoud bijwerken zonder dat u de media hoeft te vervangen.

Implementeer besturings systemen via het netwerk met opstart media in de volgende scenario's:

- [Een bestaande computer vernieuwen met een nieuwe versie van Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Een nieuwe versie van Windows op een nieuwe computer (bare-metal) installeren](install-new-windows-version-new-computer-bare-metal.md)

- [Een bestaande computer vervangen en de instellingen overzetten](replace-an-existing-computer-and-transfer-settings.md)

Voer de stappen in een van de implementatie scenario's voor besturings systemen uit en gebruik vervolgens de volgende secties om opstart bare media te gebruiken om het besturings systeem te implementeren.

## <a name="configure-deployment-settings"></a>Implementatie-instellingen configureren

Wanneer u opstart bare media gebruikt om het implementatie proces van het besturings systeem te starten, moet u de implementatie van de taken reeks configureren om het besturings systeem beschikbaar te maken voor de media. Stel deze optie in op de pagina **implementatie-instellingen** van de implementatie. Selecteer een van de volgende opties voor de instelling **beschikbaar maken voor de volgende** :

- Configuration Manager-clients, media en PXE

- Alleen media en PXE

- Alleen media en PXE (verborgen)

Zie [Een takenreeks implementeren](deploy-a-task-sequence.md)voor meer informatie.

## <a name="create-the-bootable-media"></a>De opstartbare media maken

Wanneer u opstart bare media maakt, geeft u op of het een USB-flash station of een CD/DVD-set is. De computer die de media start, moet ondersteuning bieden voor de optie die u kiest als een opstartbaar station. Zie [opstart bare media maken](create-bootable-media.md)voor meer informatie.

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a>Het besturings systeem installeren vanaf opstart bare media

Als u het besturings systeem wilt installeren, plaatst u het opstart bare medium en schakelt u de computer in.

## <a name="support-for-cloud-based-content"></a>Ondersteuning voor Cloud inhoud

<!--6209223-->

Vanaf versie 2006 kunnen opstart bare media op basis van de Cloud inhoud downloaden. U kunt bijvoorbeeld een USB-sleutel naar een gebruiker op een extern kantoor verzenden om de installatie kopie van het apparaat te versleutelen. Of een kantoor met een lokale PXE-server, maar u wilt dat apparaten zo veel mogelijk Cloud Services priori teren. In plaats van het WAN verder te belasten om grote implementatie-inhoud voor het besturings systeem te downloaden, kunnen opstart media en PXE-implementaties nu inhoud ophalen van Cloud bronnen. Bijvoorbeeld een CMG (Cloud Management Gateway) waarmee u inhoud kunt delen.

> [!NOTE]
> Het apparaat heeft nog steeds een intranet verbinding met het beheer punt nodig.

Wanneer de taken reeks wordt uitgevoerd, wordt inhoud uit de Cloud bronnen gedownload. Controleer **bestand smsts. log** op de client.

### <a name="prerequisites"></a>Vereisten

- Schakel de volgende client instelling in in de groep **Cloud Services** : **toegang tot Cloud distributiepunt toestaan**. Zorg ervoor dat de client instelling wordt geïmplementeerd op de doel-clients. Zie [over client instellingen-Cloud Services](../../core/clients/deploy/about-client-settings.md#cloud-services)voor meer informatie.

- Voor de grens groep waarin de client zich bevindt:

  - Koppel de CMG of site systemen van het Cloud distributiepunt aan de inhouds voorzieningen. Zie [een grens groep configureren](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config)voor meer informatie.

  - Schakel de volgende optie in: Geef de **voor keur aan Cloud bronnen over on-premises bronnen**. Zie voor meer informatie [Opties voor grens groepen voor het downloaden van peers](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Distribueer de inhoud waarnaar wordt verwezen door de taken reeks naar het CMG-of Cloud distributiepunt dat is ingeschakeld voor inhoud.

## <a name="next-steps"></a>Volgende stappen

[Gebruikerservaring voor implementatie van besturingssysteem](../understand/user-experience.md#task-sequence-wizard)
