---
title: Tenant koppeling-resource Verkenner het beheer centrum (preview-versie)
titleSuffix: Configuration Manager
description: Bekijk de hardware-inventaris voor het uploaden van Configuration Manager-apparaten met resource Explorer in het beheer centrum.
ms.date: 09/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: fabd91df79945580005e1c56893e78dec00d0202
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564304"
---
# <a name="tenant-attach-resource-explorer-in-the-admin-center-preview"></a><a name="bkmk_hinv"></a> Tenant attach: resource Explorer in het beheer centrum (preview-versie)
<!--cm 6479284 in 7220536 pubpreview Sept 8, 2020-->
*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]
> - Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen in één console met de naam **micro soft Endpoint Manager-beheer centrum**. Vanuit het micro soft endpoint management-beheer centrum kunt u de hardware-inventaris voor het uploaden van Configuration Manager-apparaten bekijken met resource Explorer.

   :::image type="content" source="media/6479284-resource-explorer.png" alt-text="Resource Explorer in het beheer centrum van micro soft Endpoint Manager" lightbox="media/6479284-resource-explorer.png":::

## <a name="prerequisites"></a>Vereisten

De volgende items zijn vereist voor het gebruik van resource Explorer vanuit het beheer centrum:

- Alle vereisten voor [Tenant koppeling: client Details ConfigMgr](client-details.md).
- Mini maal Configuration Manager versie 2006 en de bijbehorende versie van de console zijn geïnstalleerd.
- Voer een upgrade uit voor de doel apparaten naar de nieuwste versie van de Configuration Manager-client.

## <a name="permissions"></a>Machtigingen

Het gebruikers account heeft de volgende machtigingen nodig:

- De **Lees** machtiging voor de **verzameling** van het apparaat in Configuration Manager.
- De machtiging **resource lezen** voor de **verzameling** van het apparaat in Configuration Manager.
- De gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD.
  - Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt.

## <a name="launch-resource-explorer"></a><a name="bkmk_launch"></a> Resource Verkenner starten

1. Ga in een browser naar [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Selecteer **apparaten** en vervolgens **alle apparaten**.
1. Selecteer een apparaat dat is gesynchroniseerd vanuit Configuration Manager via [Tenant attach](device-sync-actions.md).
1. Selecteer **resource Verkenner (preview)** om de hardware-inventaris weer te geven.
1. Zoek of selecteer een klasse om informatie op te halen van de client.

   :::image type="content" source="media/6479284-resource-explorer-details.png" alt-text="Resource Explorer waarbij de moederbord klasse is geselecteerd" lightbox="media/6479284-resource-explorer-details.png":::

## <a name="close-resource-explorer"></a>Resource Explorer sluiten

Als u resource Explorer wilt sluiten en wilt terugkeren naar de apparaatgegevens, gebruikt u het `X` pictogram in de rechter bovenhoek van resource Explorer.

   :::image type="content" source="media/6479284-close-resource-explorer.png" alt-text="Resource Explorer sluiten met het pictogram x in het beheer centrum van micro soft Endpoint Manager" lightbox="media/6479284-close-resource-explorer.png":::

## <a name="next-steps"></a>Volgende stappen

[Problemen met resource Explorer oplossen](troubleshoot-resource-explorer.md)