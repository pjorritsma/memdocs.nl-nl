---
title: Tips voor het oplossen van app-implementaties
titleSuffix: Configuration Manager
description: Tips voor het oplossen van problemen met toepassings implementaties in Configuration Manager
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710585"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>Tips voor probleem oplossing voor toepassings implementaties

*Van toepassing op: Configuration Manager (huidige vertakking)*

Veelvoorkomende problemen met toepassings implementaties vallen in een van de volgende categorieën:

- Fouten bij het downloaden van toepassingen

- Compatibiliteit van toepassings implementatie vastgelopen op 0%

Als u een van deze problemen ondervindt, bevat dit artikel enkele stappen die u kunt gebruiken om problemen op te lossen. Zie [probleem oplossing voor technische Naslag informatie over het oplossen van toepassings implementaties](../understand/app-deployment-technical-reference.md)voor uitgebreidere probleem oplossing.


## <a name="download-failures"></a>Fouten bij het downloaden

Fouten bij het downloaden van toepassingen zijn de volgende:

- De client is vastgelopen bij het downloaden van een toepassing

- De client kan de toepassings inhoud niet downloaden

- De client ontvangt een vastgelopen waarde van 0% tijdens het downloaden van de toepassing

Het eerste wat u moet controleren wanneer u problemen met het downloaden van toepassingen ondervindt, is voor ontbrekende of niet-geconfigureerde grenzen en grens groepen. Als de-client zich bijvoorbeeld op het intranet bevindt en niet is geconfigureerd voor client beheer via internet, moet de netwerk locatie zich in een geconfigureerde grens. Er moet ook een grens groep aan deze grens worden toegewezen, zodat de client inhoud kan downloaden. Zie [site grenzen en grens groepen definiëren](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)voor meer informatie.

Als u een grens voor een client niet kunt configureren, of als een specifieke grens groep geen lid kan zijn van een andere grens groep:

1. Open in de Configuration Manager-console de eigenschappen van het **implementatie type**.  

1. Ga naar het tabblad **inhoud** .

1. Wijzig in de sectie voor het gebruik van een distributie punt van een grens groep in de nabijheid of de standaard site grens groep de **implementatie opties** om **inhoud te downloaden vanaf een distributie punt en lokaal**uit te voeren. (Standaard is deze instelling **geen inhoud te downloaden**.)

Als de-client de inhoud van de toepassing niet kan downloaden, moet u ervoor zorgen dat deze wordt gedistribueerd naar een distributie punt. U kunt deze configuratie controleren met behulp van de functies in de console voor het bewaken van de distributie van inhoud naar de distributie punten. Zie [inhoud bewaken die u hebt gedistribueerd](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md)voor meer informatie.  


## <a name="compliance-stuck-at-0"></a>Naleving vastgelopen bij 0%

Wanneer de compatibiliteit van de implementatie van de toepassing 0% is, controleert u de implementatie status voor de toepassing in de werk ruimte **bewaking** onder het knoop punt **implementaties** .

- Wordt uitgevoerd: de client is vastgelopen **bij**het downloaden van [inhoud](#download-failures)

- **Fout**: Zie voor meer informatie over het oplossen van dit probleem het volgende blog bericht: [Tips en trucs: actie ondernemen op activa die een mislukte implementatie melden](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Onbekend**: deze status betekent meestal dat de client geen beleid heeft ontvangen. Vernieuw het client beleid hand matig om te zien of de client het ontvangt. Zie [het ophalen van beleid initiëren voor een Configuration Manager-client](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)voor meer informatie.
  
Als u het probleem niet kunt oplossen met deze acties, controleert u de status van de client. Er is mogelijk een dieper onderliggend probleem met de client. Zie [clients controleren](../../core/clients/manage/monitor-clients.md)voor meer informatie.


## <a name="next-steps"></a>Volgende stappen

- [Toepassingen bewaken](monitor-applications-from-the-console.md)
- [Toepassingen implementeren](deploy-applications.md)
- [Beheer taken voor toepassingen](management-tasks-applications.md)
- [Technische Naslag informatie over het oplossen van toepassings implementaties](../understand/app-deployment-technical-reference.md)
