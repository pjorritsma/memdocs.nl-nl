---
title: Verificatie op basis van tokens voor CMG
titleSuffix: Configuration Manager
description: Registreer een client in het interne netwerk voor een uniek token of maak een bulk registratie token voor apparaten op internet.
ms.date: 04/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6b33027d67329b883f401168795c1b466ded1a7
ms.sourcegitcommit: dba89b827d7f89067dfa75a421119e0c973bb747
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/20/2020
ms.locfileid: "83709384"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Verificatie op basis van tokens voor Cloud beheer gateway

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--5686290-->

De Cloud Management Gateway (CMG) ondersteunt veel soorten clients, maar zelfs met [verbeterde http](../../plan-design/hierarchy/enhanced-http.md), hebben deze clients een [certificaat voor client verificatie](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway)nodig. Deze certificaat vereiste kan lastig zijn om in te richten op Internet-clients die niet vaak verbinding maken met het interne netwerk, geen lid kunnen worden van Azure Active Directory (Azure AD) en geen methode hebben voor het installeren van een door PKI uitgegeven certificaat.

Om deze problemen op te lossen, vanaf versie 2002, wordt de ondersteuning van het apparaat door Configuration Manager uitgebreid met de volgende methoden:

- Registreer u voor een uniek token op het interne netwerk

- Een token voor bulk registratie maken voor apparaten op Internet

Als u deze functie optimaal wilt benutten, moet u na het bijwerken van de site ook clients bijwerken naar de nieuwste versie. Het volledige scenario werkt pas als de client versie ook het meest recent is. Als dat nodig is, zorgt u ervoor dat u [de nieuwe client versie promoveert naar productie](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production).

De Configuration Manager-client samen met het beheer punt beheert dit token, dus er is geen besturingssysteem versie afhankelijkheid. Deze functie is beschikbaar voor alle [ondersteunde client besturingssysteem versies](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

> [!NOTE]
> Deze methoden bieden alleen ondersteuning voor apparaat gerichte beheer scenario's.
>
> Micro soft raadt aan om apparaten te koppelen aan Azure AD. Op internet gebaseerde apparaten kunnen Azure AD gebruiken om te verifiëren met Configuration Manager. Het schakelt ook zowel apparaat-als gebruikers scenario's in, ongeacht of het apparaat op internet is of is verbonden met het interne netwerk. Zie [de client installeren en registreren met Azure AD Identity](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)voor meer informatie.

## <a name="register-on-the-internal-network"></a>Registreren op het interne netwerk

Voor deze methode moet de client eerst worden geregistreerd bij het beheer punt op het interne netwerk. Client registratie gebeurt doorgaans direct na de installatie. Het beheer punt geeft de client een uniek token waarmee het een zelfondertekend certificaat gebruikt. Wanneer de client verbinding maakt met internet om te communiceren met de CMG, wordt het zelfondertekende certificaat gekoppeld aan het token dat door het beheer punt is uitgegeven. De client vernieuwt het token eenmaal per maand en is geldig gedurende 90 dagen.

Dit gedrag wordt standaard ingeschakeld door de site.

## <a name="create-a-bulk-registration-token"></a>Een bulk registratie token maken

Als u geen clients in het interne netwerk kunt installeren en registreren, maakt u een token voor bulk registratie. Gebruik dit token wanneer de client wordt geïnstalleerd op een op internet gebaseerd apparaat en registreert via de CMG. Het bulk registratie token heeft een korte geldigheids periode en wordt niet opgeslagen op de client of de site. Hiermee kan de client een uniek token genereren dat is gekoppeld aan het zelfondertekende certificaat, waarmee het kan worden geverifieerd met de CMG.

1. Meld u aan bij de site server op het hoogste niveau in de hiërarchie met lokale Administrator bevoegdheden.

1. Open een opdrachtprompt als beheerder.

1. Voer het hulp programma uit vanuit de `\bin\X64` map van de Configuration Manager-installatiemap op de site server: `BulkRegistrationTokenTool.exe` . Maak een nieuw token met de `/new` para meter. Bijvoorbeeld `BulkRegistrationTokenTool.exe /new`. Zie het gebruik van het [bulk registratie token](#bulk-registration-token-tool-usage)voor meer informatie.

1. Kopieer het token en sla het op een beveiligde locatie op.

1. Installeer de Configuration Manager-client op een op internet gebaseerd apparaat. Neem de para meter client installatie op: [**/regtoken**](about-client-installation-properties.md#regtoken). De volgende voorbeeld opdracht regel bevat de andere vereiste installatie parameters en eigenschappen:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Zie voor meer informatie over deze opdracht regel [de client installeren en registreren met behulp van Azure AD-identiteit](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Dit proces is vergelijkbaar, maar de Azure AD-eigenschappen worden niet gebruikt.

### <a name="known-issues"></a>Bekende problemen

U kunt geen bulk registratie token maken op een site die een site server in de passieve modus heeft.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Gebruik van het token voor bulk registratie

Het `BulkRegistrationTokenTool.exe` hulp programma bevindt zich in de `\bin\X64` map van de Configuration Manager-installatiemap op de site server. Meld u aan bij de site server en voer deze uit als beheerder. Het ondersteunt de volgende opdracht regel parameters:

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Deze gebruiks gegevens weer geven.

Voorbeeld: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/nieuwe

Maak een nieuw bulk registratie token.

Voorbeeld: `BulkRegistrationTokenTool.exe /new`

Het hulp programma geeft de volgende informatie weer:
  
- Een GUID die de site gebruikt om gepubliceerde tokens bij te houden
- De geldigheids duur van het token, dat standaard drie dagen is.
- Het bulk registratie token.

Het token is niet opgeslagen op de client of op de site. Kopieer het token van de opdracht prompt en sla het op een veilige locatie op.

#### <a name="lifetime"></a>/lifetime

Gebruik with `/new` para meter om de geldigheids periode van het token op te geven. Geef een geheel getal op in minuten. De standaard waarde is 4.320 (drie dagen). De maximum waarde is 10.080 (zeven dagen).

Voorbeeld: `BulkRegistrationTokenTool.exe /lifetime 4320`

## <a name="bulk-registration-token-management"></a>Token beheer voor bulk registratie

U kunt eerder gemaakte tokens voor bulk registratie en de levens duur ervan weer geven in de Configuration Manager-console en het gebruik ervan blok keren, indien nodig. De site database biedt echter geen bulk registratie tokens.

#### <a name="to-review-a-bulk-registration-token"></a>Een token voor bulk registratie controleren

1. Klik op **Beheer**in de Configuration Manager-console.

2. Vouw in de werk ruimte beheer het knoop punt **beveiliging**uit en klik op **certificaten**. In de-console wordt een lijst weer gegeven met alle site-gerelateerde certificaten en bulk registratie tokens in het detail venster.

3. Selecteer het bulk registratie token dat u wilt controleren.

U kunt specifieke bulk registratie tokens identificeren op basis van hun GUID. GUID'S voor bulk registratie tokens worden weer gegeven bij het maken van tokens. U kunt de kolom **type** ook filteren of sorteren als dat nodig is.

#### <a name="to-block-a-bulk-registration-token"></a>Een token voor bulk registratie blok keren

1. Klik op **Beheer**in de Configuration Manager-console.

2. Vouw in de werk ruimte beheer het knoop punt **beveiliging**uit, klik op **certificaten**en selecteer het bulk registratie token dat u wilt blok keren.

3. Selecteer op het tabblad **Start** van de lint balk of het menu met de rechter muisknop op inhoud **blok keren**. Daarentegen kunt u eerder geblokkeerde bulk registratie tokens deblokkeren door **blok kering** te selecteren op het tabblad **Start** van de lint balk of het menu met de rechter muisknop op inhoud.

## <a name="see-also"></a>Zie ook

- [Plan voor de Cloud beheer gateway](../manage/cmg/plan-cloud-management-gateway.md)

- [Configuration Manager Windows 10-clients installeren en toewijzen met behulp van Azure AD voor verificatie](deploy-clients-cmg-azure.md)
