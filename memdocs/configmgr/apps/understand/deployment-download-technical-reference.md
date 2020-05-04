---
title: Technische documentatie voor het downloaden van toepassingen
titleSuffix: Configuration Manager
description: Problemen met het downloaden van toepassingen oplossen technische Naslag informatie voor Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: effa8115a5023a8e0611f6bc4245a101b3a47e38
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709808"
---
# <a name="application-download-in-configuration-manager"></a>Toepassing downloaden in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Voordat u doorgaat, moet u de [client onderdelen voor toepassings implementatie](client-components-technical-reference.md) bekijken om de taak verwerking van DCM en CI-agent te begrijpen.

## <a name="download-initiation"></a>Down load initiëren

Het downloaden van toepassings inhoud wordt gestart door het CI-agent onderdeel op de client tijdens de **StateDownloadingContents** -fase. Dit proces is hetzelfde, ongeacht of de toepassing wordt geïmplementeerd in een apparaat-of gebruikers verzameling.

- Voor **beschik bare** implementaties wordt de inhoud van de toepassing gedownload wanneer de gebruiker de installatie van de toepassing start vanuit software Center.
- Voor **vereiste** implementaties wordt de inhoud van de toepassing gedownload wanneer de toewijzing wordt geactiveerd en de toepassing na de evaluatie wordt gevonden. Als u wilt weten wanneer de toewijzing is geactiveerd, raadpleegt u de artikelen [toepassings implementatie naar apparaten verzamelingen](device-deployment-technical-reference.md) of [toepassing implementeren naar gebruikers verzamelingen](user-deployment-technical-reference.md) .

Wanneer CI agent het downloaden van inhoud initieert, wordt er een taak gemaakt die wordt verwerkt door het onderdeel CI taak beheer. CI Task Manager initieert vervolgens het downloaden van de inhoud. Deze activiteit kan worden gevolgd in het **CITaskMgr. log** met de unieke implementatie type-id.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Locatie van distributie punt

Alle download taken worden verwerkt door het onderdeel voor toegang tot inhoud, dat verantwoordelijk is voor het beheren van de client cache. Nadat de Download taak is gemaakt, controleert het onderdeel inhouds toegang of de inhoud al beschikbaar is in de-client cache. Als de inhoud niet beschikbaar is, wordt een locatie aanvraag gemaakt voor het ophalen van een lijst met distributie punten van waaruit de inhoud kan worden verkregen. Deze activiteit kan worden gevolgd in **CAS. log** en **bestand locationservices. log** op de client met behulp van de unieke id van de inhoud.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Hoewel het onderdeel locatie Services de locatie aanvragen verwerkt, worden er niet rechtstreeks locaties van het beheer punt aangevraagd. Alle aanvragen voor het beheer punt passeren doorgaans het onderdeel CCM Messa ging, dat zich aanmeldt bij **CcmMessaging. log**.

De locatie van de antwoord-XML bevat de lijst met distributie punten op basis van de grens groep van de client. Deze lijst wordt geparseerd en persistent gemaakt in WMI op de client volgens de [prioriteit van de inhouds bron](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#content-source-priority). Deze activiteit kan worden weer gegeven in **ContentTransferManager. log**, met behulp van de unieke id van `Persisted location`de inhoud en op zoek naar. 

Als het antwoord XML van de locatie geen distributie punten bevat, zou **ContentTransferManager. log** moeten laten zien `Received empty location update` en de client kan vastlopen op 0% tijdens het downloaden van de toepassing. Dit antwoord kan meestal worden veroorzaakt door problemen met de configuratie van de grens groep. Zie [fouten downloaden](../deploy-use/troubleshoot-application-deployment.md#download-failures)voor meer informatie.

## <a name="content-download"></a>Inhoud downloaden

Zodra de locaties van het distributie punt zijn verkregen, maakt het onderdeel inhouds toegang een taak voor inhouds overdracht. Deze activiteit kan worden gevolgd in **CAS. log** met de unieke id van de inhoud.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

Inhouds overdracht Manager maakt vervolgens een Gegevensoverdracht service taak om de inhoud te downloaden. Deze activiteit kan worden gevolgd in **ContentTransferManager. log** op de client met behulp van de unieke id van de inhoud.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Deze logboek vermelding kan worden gebruikt voor het identificeren van de CMT en de DTS-taak-ID, die kan worden gebruikt om de voortgang van de inhouds overdracht in **ContentTransferManager. log** en **bestand datatransferservice. log** bij te houden.

Gegevensoverdracht-service voert het downloaden van de toepassings inhoud uit door een Background Intelligent Transfer Service (BITS) taak te maken en te wachten tot de down load is voltooid. Deze activiteit kan worden gevolgd in **bestand datatransferservice. log** op de client met behulp van de DTS-taak-id die is verkregen van **ContentTransferService. log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

Wanneer het downloaden is voltooid, wordt het onderdeel voor toegang tot inhoud op de hoogte gesteld. Met het onderdeel inhouds toegang wordt vervolgens de gedownloade inhoud gecontroleerd om ervoor te zorgen dat de inhoud niet is gewijzigd tijdens het downloaden. Deze activiteit kan worden gevolgd in **CAS. log** met de unieke id van de inhoud.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Ten slotte ontvangt de CI-agent na het verifiëren van de inhoud de melding voltooide taak en wordt de CI agent-taak verplaatst naar de volgende fase.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Volgende stappen

- [Installatie van toepassing](deployment-install-technical-reference.md)
