---
title: Resource Explorer gebruiken
titleSuffix: Configuration Manager
description: Resource Explorer gebruiken om de hardware-inventaris in Configuration Manager weer te geven.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: daa673169825638474fea05156fd837acbf0ba98
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710676"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Resource Explorer gebruiken om hardware-inventaris in Configuration Manager weer te geven

*Van toepassing op: Configuration Manager (huidige vertakking)*

Resource Explorer in Configuration Manager gebruiken om informatie over hardware-inventarisatie weer te geven. De site verzamelt deze gegevens van clients in uw hiërarchie.  

> [!Tip]  
>  In resource Explorer worden geen gegevens weer gegeven totdat een hardware-inventarisatie fase is uitgevoerd op de client waarmee u verbinding maakt.  



## <a name="overview"></a>Overzicht

Resource Explorer heeft de volgende secties die betrekking hebben op Hardware-inventarisatie:  

- **Hardware**: bevat de meest recente hardware-inventaris die is verzameld van het opgegeven client apparaat.  

    - Het knoop punt **status van werk station** bevat de tijd en datum van de laatste hardware-inventaris van het apparaat.  

- **Hardware geschiedenis**: een geschiedenis van geïnventariseerde items die zijn gewijzigd sinds de laatste hardware-inventarisatie fase.  

    - Vouw een item uit om een **Huidig** knoop punt en een of meer knoop punten met de historische datum weer te geven. Vergelijk de informatie in het huidige knoop punt met een van de historische knoop punten om de items te zien die zijn gewijzigd.  

> [!NOTE]  
> Configuration Manager verwijdert standaard hardware-inventarisatie gegevens die 90 dagen inactief zijn. Pas dit aantal dagen aan in de onderhouds taak **verouderde inventaris geschiedenis verwijderen** . Zie [onderhouds taken](../../../servers/manage/maintenance-tasks.md)voor meer informatie.  



## <a name="how-to-open-resource-explorer"></a><a name="bkmk_open"></a>Resource Explorer openen   

1.  Ga in de Configuration Manager-console naar de werk ruimte **activa en naleving** en selecteer het knoop punt **apparaten** . U kunt ook een wille keurige verzameling selecteren in het knoop punt **apparaat Collections** .  

2.  Selecteer een apparaat. Klik op het lint op het tabblad **Start** en op de groep **apparaten** op **Start**en selecteer vervolgens **resource Verkenner**.   

> [!Tip]  
> Klik in resource Explorer met de rechter muisknop op een item in het rechterdeel venster met resultaten voor aanvullende acties. Klik op **Eigenschappen** om dat item in een andere indeling weer te geven.  



## <a name="use-of-large-integer-values"></a><a name="bkmk_bigint"></a>Gebruik van grote waarden met gehele getallen
<!--1357880-->
In Configuration Manager versies 1802 en eerder heeft de hardware-inventarisatie een limiet voor gehele getallen groter dan 4.294.967.296 (2 ^ 32). Deze limiet kan worden bereikt voor kenmerken zoals de grootte van harde schijven in bytes. Het beheer punt verwerkt geen gehele waarden boven deze limiet, dus er wordt geen waarde opgeslagen in de data base. 

Vanaf versie 1806 wordt de limiet verhoogd naar 18446744073709551616 (2 ^ 64). 

Voor een eigenschap met een waarde die niet verandert, zoals de totale schijf grootte, ziet u de waarde na het uitvoeren van de upgrade van de site mogelijk niet onmiddellijk. De meeste hardware-inventarisatie is een Delta-rapport. De client verzendt alleen gewijzigde waarden. U kunt dit probleem omzeilen door een andere eigenschap aan dezelfde klasse toe te voegen. Deze bewerking zorgt ervoor dat de client alle eigenschappen van de gewijzigde klasse bijwerkt. 



## <a name="see-also"></a>Zie ook

Zie [clients controleren voor Linux-en UNIX-servers](../monitor-clients-for-linux-and-unix-servers.md)voor meer informatie over het weer geven van hardware-inventarisatie van clients met Linux en UNIX.  

Resource Explorer toont ook software-inventarisatie. Zie [resource Explorer gebruiken om software-inventaris weer te geven](use-resource-explorer-to-view-software-inventory.md)voor meer informatie.
