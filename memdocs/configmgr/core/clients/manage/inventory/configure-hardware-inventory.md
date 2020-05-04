---
title: Hardware-inventarisatie configureren
titleSuffix: Configuration Manager
description: Hardware-inventaris instellen voor alle clients of voor een verzameling in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714435"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>Hardware-inventaris configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met deze procedure configureert u de standaardinstellingen voor de hardware-inventarisatie die voor alle clients in uw hiërarchie geldt. Als u wilt dat deze instellingen alleen van toepassing zijn op enkele clients, maakt u een aangepaste clientapparaatinstelling en wijst u deze toe aan een verzameling waartoe de apparaten behoren die u wilt inventariseren. Zie [client instellingen configureren voor meer informatie](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Als een clientapparaat instellingen voor hardware-inventarisatie van meerdere sets clientinstellingen ontvangt, worden de hardware-inventarisatieklassen van elke set instellingen samengevoegd wanneer de client hardware-inventarisatie rapporteert. Als een klasse niet wordt gecontroleerd in een aangepaste client instelling met een hogere prioriteit, wordt de client niet uitgeschakeld om die klasse te inventariseren. 

Als u een specifieke hardware-inventaris klasse wilt uitschakelen op een meerderheid van systemen, met uitzonde ring van enkele, moet de-klasse worden uitgeschakeld in de standaard instellingen van de client. Maak vervolgens een aangepaste client instelling om de klasse in te scha kelen en implementeer deze op de doel systemen.


### <a name="to-configure-hardware-inventory"></a>Hardware-inventarisatie configureren  

1.   > Kies > in de Configuration Manager-console de**client instellingen voor** **de client instellingen****standaard**.  

4.  Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

5.  Klik in het dialoog venster **standaard instellingen** op **Hardware-inventarisatie**.  

6.  In de lijst **Apparaatinstellingen** configureert u dan het volgende:  

    -   **Hardware-inventaris op clients inschakelen** : Selecteer **Ja**.  

    -   **Hardware-inventaris planning** : Klik op **planning** om het interval op te geven waarmee clients de hardware-inventaris verzamelen.  

7.  Configureer andere [client instellingen voor hardware-inventarisatie](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) die u nodig hebt.  

De volgende keer dat clientapparaten clientbeleid downloaden, worden deze instellingen geconfigureerd. Zie [clients beheren](../../../../core/clients/manage/manage-clients.md)om het ophalen van het beleid voor één client te initiëren.  
