---
title: Technische documentatie over app-implementatie naar Device Collections
titleSuffix: Configuration Manager
description: Probleem oplossing voor toepassings implementaties op technische Naslag informatie over apparaten verzamelingen voor Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1965029a1933793057dc5768bacb391afd645404
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709759"
---
# <a name="application-deployment-for-device-collections"></a>Toepassings implementatie voor Apparaatsets

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer een toepassing wordt geïmplementeerd in een verzameling apparaten, is het beleid gericht op alle apparaten in de verzameling, ongeacht het implementatie doel. In dit artikel wordt uitgelegd hoe de verwerking van beleid en implementatie op de client wordt uitgevoerd.

> [!TIP]
> Alle informatie die nodig is om de client logboeken te controleren, kan worden verkregen door de SQL-query uit te voeren waarnaar wordt verwezen in de sectie [voordat u begint](app-deployment-technical-reference.md#before-you-begin) .

## <a name="policy-download"></a>Beleid downloaden

Nadat het beleid voor de toepassings implementatie is gericht op de client, zal de client het beleid downloaden bij de volgende beleids polling-cyclus. Wanneer het beleid door de client wordt gedownload, worden naast het implementatie beleid ook het bijbehorende beleid gedownload. Deze gerelateerde beleids regels bevatten het beleid voor de toepassing, het implementatie type, de globale voor waarden, enzovoort. De activiteit voor het downloaden van beleid kan worden gevolgd in de **Policy Agent. log** op de client met de unieke id van de toepassing of toewijzing.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

Nadat het beleid is gedownload op de client, maakt het Scheduler-onderdeel planningen voor activering en afdwinging van de implementatie.

## <a name="deployment-activation"></a>Activering van de implementatie

De evaluatie van de toepassing wordt gestart wanneer de implementatie wordt geactiveerd. Scheduler-onderdeel maakt een planning om de toewijzing te activeren op de beschik bare tijd die in de implementatie is geconfigureerd. Deze activiteit kan worden bijgehouden in **scheduler. log** op de client met behulp van de unieke id van de toepassings toewijzing.

- Voor **vereiste** implementaties wordt het activerings schema gemaakt, maar heeft dit een vertraging van Maxi maal twee uur om bron conflicten te voor komen op site servers en distributie punten. De vertraging helpt conflicten te voor komen omdat toepassings inhoud tijdens de evaluatie kan worden gedownload als de toepassing van toepassing is op basis van gedefinieerde regels voor vereisten.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- Voor **beschik bare** implementaties wordt het activerings schema gemaakt om te worden geactiveerd tijdens de beschik bare tijd die in de implementatie is geconfigureerd.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Wanneer de geplande tijd arriveert, stuurt scheduler-onderdeel het activerings bericht naar DCM agent om de toepassing uit te voeren.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

DCM-agent ontvangt het activerings bericht en maakt een taak om de toepassing te evalueren.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Implementatie afdwingen

De installatie van de toepassing wordt gestart wanneer de implementatie wordt afgedwongen.

- Voor **vereiste** implementaties maakt scheduler een deadline schema nadat het beleid is gedownload om de toepassing af te dwingen bij de implementatie deadline. De deadline planning is standaard niet wille keurig. Het gedrag van wille keurigheid voor activering kan worden bepaald door de client instelling [deadline voor wille keurigheid uitschakelen](../../core/clients/deploy/about-client-settings.md#disable-deadline-randomization) .

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    Op het tijdstip van de deadline verzendt scheduler-onderdeel het deadline bericht naar DCM agent. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    DCM-agent ontvangt het bericht deadline en maakt een taak om de toepassing af te dwingen.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > Voor implementaties met een deadline in het verleden wordt de toepassing geactiveerd en direct afgedwongen door dezelfde DCM agent-taak waarmee de evaluatie-, Download-en installatie acties worden uitgevoerd.

- Voor **beschik bare** implementaties is er geen deadline planning sinds de handhaving plaatsvindt wanneer de installatie van de toepassing wordt gestart door de gebruiker vanuit software Center. Wanneer de gebruiker een installatie start, wordt een DCM-agent taak gemaakt voor het uitvoeren van de evaluatie, het downloaden en de installatie van de toepassing. Deze activiteit kan worden gevolgd in **DCMAgent. log** op de client.

## <a name="next-steps"></a>Volgende stappen

- [Informatie over client onderdelen voor toepassings implementatie](client-components-technical-reference.md)
