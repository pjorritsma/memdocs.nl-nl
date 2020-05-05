---
title: Problemen met de actie van het apparaat oplossen
titleSuffix: Configuration Manager
description: Problemen met Device actions oplossen technische Naslag informatie voor Configuration Manager
ms.date: 04/01/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 72da589a3f4213fb64b4123d5580cb1be945de0e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81717592"
---
# <a name="troubleshooting-device-actions-for-configuration-manager-devices"></a>Problemen met apparaatinstellingen voor Configuration Manager apparaten oplossen

*Van toepassing op: Configuration Manager (huidige vertakking)*

Vanaf Configuration Manager 2002 kunnen clients Configuration Manager worden gesynchroniseerd met het micro soft Endpoint Manager-beheer centrum. Sommige client acties kunnen worden uitgevoerd vanuit het micro soft Endpoint Manager-beheer centrum op de gesynchroniseerde clients.

De beschikbare acties zijn:
- Computer beleid synchroniseren
- Gebruikers beleid synchroniseren
- App-evaluatie cyclus


[![Overzicht van apparaten in het beheer centrum van micro soft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)
  
Wanneer een beheerder een actie uitvoert vanuit het micro soft Endpoint Manager-beheer centrum, wordt de meldings aanvraag doorgestuurd naar Configuration Manager-site en van de site naar de client.

## <a name="configuration-manager-components"></a>Configuration Manager onderdelen

- **SMS_SERVICE_CONNECTOR**: gebruikt de mede werker van de gateway melding voor het verwerken van de melding van het micro soft Endpoint Manager-beheer centrum.
- **SMS_NOTIFICATION_SERVER**: de melding wordt opgehaald en een client melding wordt gemaakt.
- **BgbAgent**: de client krijgt een taak en voert de aangevraagde actie uit.

## <a name="sms_service_connector"></a>SMS_SERVICE_CONNECTOR

Wanneer een actie vanuit het micro soft Endpoint Manager-beheer centrum wordt gestart, wordt de aanvraag door **CMGatewayNotificationWorker. log** verwerkt.  

```text
Received new notification. Validating basic notification details...
Validating device action message content...
Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
```
 
1. Er wordt een melding ontvangen van micro soft Endpoint Manager-beheer centrum.

   ```text
   Received new notification. Validating basic notification details..
   ```

1. Acties van gebruikers en apparaten worden gevalideerd.

   ```text
   Validating device action message content... 
   Authorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID:     a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2
   ```

1. De externe taak wordt doorgestuurd naar de SMS_NOTIFICATION_SERVER.

    ```text
   Forwarded BGB remote task. TemplateID: 1 TaskGuid: a43dd1b3-a006-4604-b012-5529380b3b6f TaskParam: TargetDeviceIDs: 1  
    ```


## <a name="sms_notification_server"></a>SMS_NOTIFICATION_SERVER

Zodra het bericht naar de SMS_NOTIFICATION_SERVER is verzonden, wordt een taak vanaf het beheer punt naar de bijbehorende client verzonden. U ziet het onderstaande in het **BgbServer. log**op het beheer punt:

```text
Get one push message from database.
Starting to send push task (PushID: 7 TaskID: 8 TaskGUID: A43DD1B3-A006-4604-B012-5529380B3B6F TaskType: 1 TaskParam: ) to 1 clients  with throttling (strategy: 1 param: 42)
```

## <a name="bgbagent"></a>BgbAgent

De laatste stap vindt plaats op de client en kan worden weer gegeven in **CcmNotificationAgent. log**. Zodra de taak is ontvangen, wordt scheduler gevraagd om de actie uit te voeren. Wanneer de actie wordt uitgevoerd, wordt er een bevestigings bericht weer gegeven:

```text
Receive task from server with pushid=7, taskid=8, taskguid=A43DD1B3-A006-4604-B012-5529380B3B6F, tasktype=1 and taskParam=

Send Task response message <BgbResponseMessage TimeStamp="2020-01-21T15:43:43Z"><PushID>8</PushID><TaskID>9</TaskID><ReturnCode>1</ReturnCode></BgbResponseMessage> successfully.
```

## <a name="common-issues"></a>Algemene problemen

Als de beheerder niet over de vereiste machtigingen beschikt in Configuration Manager, ziet u een `Unauthorized` reactie in **CMGatewayNotificationWorker. log**.

```text
Received new notification. Validating basic notification details..
Validating device action message content...
Unauthorized to perform client action. TemplateID: RequestMachinePolicy TenantId: a1b2c3a1-b2c3-d4a1-b2c3-d4a1b2c3a1b2 AADUserID: 3a1e89e6-e190-4615-9d38-a208b0eb1c78
```  

Zorg ervoor dat de gebruiker die de actie uitvoert vanuit het micro soft Endpoint Manager-beheer centrum over de vereiste machtigingen beschikt voor Configuration Manager-site. Zie voor meer informatie [micro soft Endpoint Manager-Tenant toevoegen van vereisten](device-sync-actions.md#prerequisites).

## <a name="next-steps"></a>Volgende stappen

[Schakel co-beheer](../comanage/overview.md) in om extra Cloud mogelijkheden te krijgen, zoals voorwaardelijke toegang.
