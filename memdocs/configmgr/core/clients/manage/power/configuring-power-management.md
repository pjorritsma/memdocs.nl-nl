---
title: Energie beheer configureren
titleSuffix: Configuration Manager
description: Energie beheer instellen in Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3146c753e2d84001c162c653cc09af654e6a170a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715240"
---
# <a name="configure-power-management-in-configuration-manager"></a>Energie beheer configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

In dit artikel wordt uitgelegd hoe u energie beheer instelt in Configuration Manager.

## <a name="enable-and-configure-client-settings"></a>Client instellingen inschakelen en configureren

Met deze procedure configureert u de *standaard client instellingen* voor energie beheer. Deze is van toepassing op alle computers in uw hiërarchie.

Als u deze instellingen wilt Toep assen op enkele computers, maakt u een *aangepaste client instelling*. Wijs deze vervolgens toe aan een verzameling die de computers bevat voor energie beheer. Zie [client instellingen configureren](../../deploy/configure-client-settings.md)voor meer informatie.  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , selecteer het knoop punt **client instellingen** en selecteer **standaard client instellingen**.

1. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.  

1. Selecteer de groep **energie beheer** .  

1. Schakel de client instelling in om het **energie beheer van apparaten toe te staan**.

1. Configureer de aanvullende client instellingen die u nodig hebt. Zie [client instellingen-energie beheer](../../deploy/about-client-settings.md#power-management)voor meer informatie.  

Clients configureren deze instellingen wanneer ze de volgende keer het client beleid downloaden. Zie [clients beheren](../manage-clients.md#BKMK_PolicyRetrieval)om het ophalen van het beleid voor één client te initiëren.  

## <a name="exclude-computers"></a>Computers uitsluiten

U kunt voorkomen dat verzamelingen computers energiebeheerinstellingen ontvangen. Als een computer lid *is van een* verzameling die u uitsluit van energiebeheer instellingen, past die computer geen energiebeheer instellingen toe. Dit gedrag geldt ook als het een lid is van een andere verzameling waarop Energiebeheer instellingen worden toegepast.  

U kunt computers het beste uitsluiten van energie beheer om de volgende redenen:  

- Als er een zakelijke vereiste is om computers altijd ingeschakeld te hebben.  

- U hebt een controle verzameling computers waarop u geen energiebeheer instellingen wilt Toep assen.  

- Als u bepaalde computers hebt waarop geen energiebeheerinstellingen kunnen worden toegepast.  

- Als u computers wilt uitsluiten waarop Windows Server met energiebeheer wordt uitgevoerd.  

> [!NOTE]  
> Als u de client instelling configureert om **gebruikers toe te staan hun apparaat uit te sluiten van energie beheer**, kunnen gebruikers hun eigen computers uitsluiten van energie beheer via Software Center.  

Als u wilt weten welke computers zijn uitgesloten van energie beheer, voert u het rapport **uitgesloten computers**uit. Zie [energie beheer bewaken en plannen](monitor-and-plan-for-power-management.md#BKMK_Excluded)voor meer informatie over dit rapport.  

> [!IMPORTANT]  
> Het uitsluiten van een computer uit energie beheer zorgt ervoor dat alle energie-instellingen worden teruggezet naar de oorspronkelijke waarden. Het is niet mogelijk oorspronkelijke waarden van afzonderlijke energie-instellingen te herstellen.  

### <a name="how-to-exclude-a-collection-of-computers-from-power-management"></a>Een verzameling computers uitsluiten van energie beheer  

1. Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **Apparaatsets** .  

1. Selecteer de verzameling die u wilt uitsluiten van energie beheer. Klik op het tabblad **Start** van het lint in de groep **Eigenschappen** op **Eigenschappen**.  

1. Ga naar het tabblad **energie beheer** en selecteer **nooit Energiebeheer instellingen Toep assen op computers in deze verzameling**.  

## <a name="next-steps"></a>Volgende stappen

[Energiebeheerschema's maken en toepassen](create-and-apply-power-plans.md)

[Energiebeheer bewaken en plannen](monitor-and-plan-for-power-management.md)
