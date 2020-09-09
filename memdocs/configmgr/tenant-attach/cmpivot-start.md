---
title: Aan de Tenant gekoppelde CMPivot (preview-versie) starten
titleSuffix: Configuration Manager
description: Start CMPivot voor aan micro soft Endpoint Manager gekoppelde apparaten.
ms.date: 09/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae6c0c83-2299-4463-958d-5555e3fcbdbe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 88fe50bd75fff73604c78125b0cd7599aa1afa4f
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564313"
---
# <a name="launch-cmpivot-from-the-admin-center-preview"></a><a name="bkmk_cmpivot"></a> CMPivot starten vanuit het beheer centrum (preview-versie)

*Van toepassing op: Configuration Manager (huidige vertakking)* 

> [!Important]
> - Deze informatie is gekoppeld aan een preview-functie die aanzienlijk kan worden gewijzigd voordat deze commercieel wordt uitgebracht. Microsoft biedt geen enkele expliciete of impliciete garanties met betrekking tot de informatie die hier wordt verstrekt.

<!--6024392-->
Breng de kracht van on-premises [CMPivot](../core/servers/manage/cmpivot.md) naar het micro soft Endpoint Manager-beheer centrum. Sta aanvullende persona's, zoals Helpdesk, toe om vanuit de cloud realtimequery's te starten op een afzonderlijk, door ConfigMgr beheerd apparaat en de resultaten te retourneren naar het beheercentrum. Dit biedt alle traditionele voordelen van CMPivot, waarmee IT-beheerders en andere aangewezen personen de status van apparaten in hun omgeving snel kunnen beoordelen en actie kunnen ondernemen.

## <a name="prerequisites"></a>Vereisten

De volgende items zijn vereist voor het gebruik van CMPivot van het beheer centrum:

- Alle vereisten voor [Tenant koppeling: client Details ConfigMgr](client-details.md)
- Mini maal Configuration Manager versie 2002 van de [Update Rollup](https://support.microsoft.com/help/4560496/) en de bijbehorende versie van de console geïnstalleerd.
- Voer een upgrade uit voor de doel apparaten naar de nieuwste versie van de Configuration Manager-client.  
- Voor doel-clients is mini maal Power shell-versie 4 vereist.
- Om gegevens te verzamelen voor de volgende entiteiten, is voor de doel-clients mini maal Power shell-versie 5,0 vereist:  
  - Beheerders
  - Verbinding
  - IP
  - SMBConfig

## <a name="permissions"></a>Machtigingen

Het gebruikers account heeft de volgende machtigingen nodig:

- De **Lees** machtiging voor de **verzameling** van het apparaat in Configuration Manager.
- De machtiging **CMPivot uitvoeren** voor de **verzameling** in Configuration Manager
- De gebruikersrol **beheerder** voor de Configuration Manager micro service-toepassing in azure AD.
  - Voeg de rol in azure AD toe uit **bedrijfs toepassingen**  >  **Configuration Manager micro service**-  >  **gebruikers en-groepen**  >  **gebruiker toevoegen**. Groepen worden ondersteund als u Azure AD Premium hebt.


## <a name="launch-cmpivot"></a><a name="bkmk_launch"></a> CMPivot starten

1. Ga in een browser naar [https://endpoint.microsoft.com](https://endpoint.microsoft.com) .
1. Selecteer **apparaten** en vervolgens **alle apparaten**.
1. Selecteer een apparaat dat is gesynchroniseerd vanuit Configuration Manager via [Tenant attach](device-sync-actions.md).
1. Selecteer **CMPivot (preview)**.
1. Typ uw query in het deel venster script en selecteer vervolgens **uitvoeren**.

## <a name="close-cmpivot"></a>CMPivot sluiten

Gebruik het `X` pictogram in de rechter bovenhoek van CMPivot om CMPivot te sluiten en terug te keren naar de apparaatgegevens.

   :::image type="content" source="media/6024392-close-cmpivot.png" alt-text="CMPivot sluiten met het X-pictogram in het micro soft Endpoint Manager-beheer centrum" lightbox="media/6024392-close-cmpivot.png":::

## <a name="next-steps"></a>Volgende stappen

- Zie [CMPivot-voorbeeld scripts](cmpivot-samples-attached.md)voor query voorbeelden.
- Zie [overzicht van CMPivot-gebruik](cmpivot-overview-attached.md)voor meer informatie over CMPivot-entiteiten,-Opera tors en-functies.
- [Problemen oplossen met CMPivot](troubleshoot-cmpivot.md) voor apparaten die zijn geüpload naar het beheer centrum.