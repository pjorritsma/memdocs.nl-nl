---
title: Implementatie status van client bewaken
titleSuffix: Configuration Manager
description: Controleer de implementatie status van de client in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80cfa1576ae2cc4505147aee07a247e035b07ada
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713315"
---
# <a name="how-to-monitor-client-deployment-status-in-configuration-manager"></a>De client implementatie status in Configuration Manager bewaken

*Van toepassing op: Configuration Manager (huidige vertakking)*

Het kost tijd om clients te implementeren op uw site en sommige installaties lukken de eerste keer niet direct. De Configuration Manager-console biedt een manier om client implementaties binnen een verzameling te blijven door de client implementatie status in realtime te rapporteren.  

> [!NOTE]  
>  De beste en meest betrouw bare manier om de client implementatie te controleren is met behulp van de Configuration Manager-console (zoals beschreven in dit artikel). De sectie **Clientstatus** van de werkruimte **Bewaking** in de console bevat nauwkeurige en realtime informatie over de clientimplementatiestatus. U kunt clientimplementaties ook met andere hulpprogramma’s bewaken, zoals Server Manager in Windows Server of System Center Operations Manager; mogelijk ontvangt u dan ook waarschuwingen over normale clientinstallatieactiviteiten. Omdat het clientinstallatieprogramma (CCMSetup.exe) anders wordt uitgevoerd in verschillende omgevingen, kan het zijn dat er onrechtmatig waarschuwingen worden gegeven die geen goed beeld vormen van de daadwerkelijke status van clientimplementaties.  

 In de werkruimte **Bewaking** van de console kunt u de volgende statussen bewaken van clientimplementaties die plaatsvinden binnen een verzameling die u opgeeft:  

- Compatibel  

- Wordt uitgevoerd  

- Niet compatibel  

- Mislukt  

- Onbekend  

  Configuration Manager rapporteert over implementaties van productieclients of pre-productieclients. De Configuration Manager-console biedt ook een overzicht van clientimplementaties die gedurende een bepaalde periode zijn mislukt zodat u kunt bepalen of de acties die u onderneemt om problemen met implementaties op te lossen, het aantal geslaagde implementaties na verloop van tijd verbetert.  

## <a name="to-monitor-client-deployments"></a>Clientimplementaties bewaken  

- Klik in de Configuration Manager-console op **bewaking** > **client status**.  

- Klik op **Productieclientimplementatie** of **Pre-productieclientimplementatie**, afhankelijk van de versie van de client die u wilt bewaken.  

- Bekijk de overzichten van de clientimplementatiestatussen en van het aantal mislukte clientimplementaties.  

- Als u het bereik van het rapport wilt wijzigen, klikt u op **Bladeren...** en kiest u een andere verzameling.  

  Zie [Client upgrades testen in een pre-productie verzameling](../../../core/clients/manage/upgrade/test-client-upgrades.md)voor meer informatie over client implementaties voor preproductie.

  > [!NOTE]
  > De implementatie status op computers die site systeem rollen in een pre-productie verzameling hosten, kan worden gerapporteerd als **niet-compatibel** , zelfs als de client met succes is geïmplementeerd. Wanneer u promoveert naar productie, wordt de status van de implementatie correct gerapporteerd.   

  Zie [clients controleren voor meer informatie over](../../../core/clients/manage/monitor-clients.md) het controleren van de status van geïmplementeerde clients  

  U kunt Configuration Manager-rapporten gebruiken om meer informatie te krijgen over de status van clients in uw site. Zie [Introduction to Reporting](../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie over het uitvoeren van rapporten.  
