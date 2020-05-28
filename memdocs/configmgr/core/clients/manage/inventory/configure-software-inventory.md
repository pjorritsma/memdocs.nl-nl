---
title: Software-inventarisatie configureren
titleSuffix: Configuration Manager
description: Software-inventaris configureren en mappen uitsluiten van software-inventaris in Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f6fcf4736c30d8743d0d26b52aac60ef12b5c9cd
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906297"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>Software-inventaris configureren in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Met deze procedure configureert u de standaard client instellingen voor software-inventaris en geldt dit voor alle computers in uw hiërarchie. Als u deze instellingen wilt Toep assen op enkele computers, maakt u een aangepaste apparaatclient en wijst u deze toe aan een verzameling. Zie [client instellingen configureren](../../../../core/clients/deploy/configure-client-settings.md)voor meer informatie over het maken van aangepaste apparaatinstellingen.   

## <a name="to-configure-software-inventory"></a>De software-inventarisatie configureren  

1. Kies in de Configuration Manager-console de client instellingen voor **de client instellingen**  >  **Client Settings****standaard**.    

2. Klik op het tabblad **Start** in de groep **Eigenschappen** op **Eigenschappen**.  

3. Kies in het dialoog venster **standaard instellingen** de optie **software-inventarisatie**.  

4. Configureer de volgende waarden in de lijst **Apparaatinstellingen** :  

   -   **Software-inventaris op clients inschakelen** : Selecteer **waar**in de vervolg keuzelijst.  

   -   Planning van **software-inventaris en verzamelen van bestanden** : Hiermee configureert u het interval waarmee clients de software-inventaris en bestanden verzamelen.   

5. Configureer de clientinstellingen die u nodig hebt. De sectie [software-inventarisatie](../../../../core/clients/deploy/about-client-settings.md#software-inventory) van het artikel [about client settings](../../../../core/clients/deploy/about-client-settings.md) bevat een lijst met de client instellingen.  

   Clientcomputers zullen worden geconfigureerd met deze instellingen wanneer ze de volgende keer het clientbeleid downloaden. Zie [clients beheren](../../../../core/clients/manage/manage-clients.md)om het ophalen van het beleid voor één client te initiëren.  

   > [!TIP]
   >   Fout code 80041006 in inventoryprovider. log betekent dat er onvoldoende geheugen beschikbaar is voor de WMI-provider. Dat wil zeggen dat de geheugen quotum limiet voor een provider is bereikt en dat de inventaris provider niet kan door gaan.
   > In dit geval maakt de inventaris agent een rapport met 0 vermeldingen, zodat er geen inventaris-items worden gerapporteerd. <br/>
   > Een mogelijke oplossing voor deze fout is het verminderen van het bereik van de software-inventaris verzameling. In omstandigheden wanneer de fout optreedt nadat het inventarisatie bereik is beperkt, kan het verhogen van de eigenschap [MemoryPerHost](https://techcommunity.microsoft.com/t5/ask-the-performance-team/memory-and-handle-quotas-in-the-wmi-provider-service/ba-p/373319) die is gedefinieerd in de klasse [_ProviderHostQuotaConfiguration](https://docs.microsoft.com/windows/win32/wmisdk/--providerhostquotaconfiguration) , een oplossing bieden.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Mappen uitsluiten van software-inventaris  

1.  Met behulp van Notepad.exe maakt u een leeg bestand met de naam **Skpswi.dat**.  

2.  Klik met de rechter muisknop op het bestand **bestand skpswi. dat** en klik op **Eigenschappen**. Selecteer in de eigenschappen van het bestand Skpswi.dat het kenmerk **Verborgen** .  

3.  Plaats het bestand **Skpswi.dat** in de hoofdmap van elke harde schijf van een client of elke mapstructuur die u wilt uitsluiten van software-inventaris.  

> [!NOTE]  
>  Met software-inventaris wordt het station van de client niet opnieuw geïnventariseerd tenzij dit bestand wordt verwijderd uit het station op de clientcomputer.
