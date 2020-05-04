---
title: 'Hardware-inventaris '
titleSuffix: Configuration Manager
description: Krijg kennis met hardware-inventarisatie in Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7baf6bad80fbccb698278602c519f3a75b8a4b5f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714407"
---
# <a name="introduction-to-hardware-inventory-in-configuration-manager"></a>Inleiding tot hardware-inventarisatie in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik hardware-inventaris in Configuration Manager om informatie te verzamelen over de hardwareconfiguratie van client apparaten in uw organisatie. Als u de hardware-inventaris wilt verzamelen, moet u de instelling **hardware-inventaris op clients inschakelen** in de client instellingen selecteren.  

 Nadat de hardware-inventarisatie is ingeschakeld en de client een hardware-inventarisatie cyclus uitvoert, stuurt de client de gegevens naar een beheer punt in de site van de client. Het beheer punt stuurt de inventarisatie gegevens vervolgens door naar de Configuration Manager-site server, die de inventarisatie gegevens in de site database opslaat. Hardware-inventarisatie wordt op clients uitgevoerd volgens het schema dat u in de clientinstellingen opgeeft.  
## <a name="view-hardware-inventory"></a>Hardware-inventaris weer geven 

 U kunt verschillende methoden gebruiken om de hardware-inventarisatie gegevens weer te geven die Configuration Manager verzameld, waaronder de volgende methoden:  

- [Query's maken die apparaten retour neren die zijn gebaseerd op een specifieke hardwareconfiguratie](../../../../core/servers/manage/introduction-to-queries.md).  

- Op [query's gebaseerde verzamelingen maken die zijn gebaseerd op een specifieke hardwareconfiguratie](../../../../core/clients/manage/collections/introduction-to-collections.md). Op query's gebaseerde verzamelinglidmaatschappen worden automatisch volgens een schema bijgewerkt. U kunt verzamelingen gebruiken voor verschillende taken, waaronder software-implementatie.

- [Rapporten uitvoeren waarin specifieke details over hardwareconfiguraties in uw organisatie worden weer gegeven](../../../servers/manage/introduction-to-reporting.md).

- [Resource Explorer gebruiken](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) om gedetailleerde informatie weer te geven over de hardware-inventaris die wordt verzameld van client apparaten.

Wanneer een hardware-inventarisatie op een clientapparaat wordt uitgevoerd, omvatten de inventarisgegevens die door de client worden geretourneerd altijd een volledige inventarisatie. Volgende inventaris gegevens bevatten alleen informatie over Delta-inventarisatie. De site server verwerkt informatie over de Delta-inventaris in de ontvangen bestelling. Als er geen Delta gegevens voor een client ontbreken, worden door de site server aanvullende Delta gegevens geweigerd en wordt de client doorgestuurd om een volledige inventarisatie cyclus uit te voeren.  

 Configuration Manager biedt beperkte ondersteuning voor dual-boot-computers. Configuration Manager kan dual-boot-computers detecteren, maar inventarisatie gegevens worden alleen geretourneerd vanuit het besturings systeem dat actief is wanneer de inventarisatie cyclus wordt uitgevoerd.  

> [!NOTE]  
>  Voor informatie over het gebruik van hardware-inventaris met clients met Linux en UNIX raadpleegt u [hardware-inventaris voor Linux en UNIX](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Hardware-inventarisatie in Configuration Manager uitbreiden  
 Naast de ingebouwde hardware-inventaris in Configuration Manager, kunt u ook een van de volgende methoden gebruiken om de hardware-inventaris uit te breiden om meer informatie te verzamelen:  

- Inventaris klassen voor hardware-inventarisatie in de Configuration Manager-console inschakelen, uitschakelen, toevoegen en verwijderen.  
- Gebruik NOIDMIF-bestanden voor het verzamelen van informatie over client apparaten die niet kunnen worden geïnventariseerd door Configuration Manager. Het is bijvoorbeeld mogelijk dat u informatie wilt verzamelen over het activumnummer van een apparaat, dat alleen als label bestaat op het apparaat. NOIDMIF-inventarisatie is automatisch gekoppeld aan het clientapparaat waarvan deze is verzameld.  
- Gebruik IDMIF-bestanden om informatie te verzamelen over assets die niet zijn gekoppeld aan een Configuration Manager-client, bijvoorbeeld projectors, kopieer apparaten en netwerk printers.


## <a name="next-steps"></a>Volgende stappen
Zie [hardware-inventaris configureren](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)voor meer informatie over het gebruik van deze methoden om Configuration Manager hardware-inventaris uit te breiden.  
