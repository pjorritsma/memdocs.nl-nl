---
title: Technische documentatie voor toepassings implementatie beleid
titleSuffix: Configuration Manager
description: Problemen met toepassings implementatie beleid oplossen technische Naslag informatie voor Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709787"
---
# <a name="application-deployment-policy"></a>Toepassings implementatie beleid

*Van toepassing op: Configuration Manager (huidige vertakking)*

## <a name="policy-creation"></a>Beleid maken

Wanneer u een toepassing implementeert, wordt er een instantie van [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) klasse gemaakt waarmee de toewijzing van een toepassing aan een verzameling wordt aangeduid. Deze activiteit kan worden gevolgd in **SMSProv. log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

In de Configuration Manager-Data Base wordt deze informatie opgeslagen in `CI_CIAssignments` de tabel `AssignmentType` waarbij 2 staat voor een toepassings implementatie. Wanneer de toewijzing is gemaakt, detecteert het onderdeel SMS data base monitor een wijziging in de tabel en waarschuwt object Replication Manager om het beleid voor CI-toewijzing (CIA) te verwerken. Het onderdeel object Replication Manager maakt vervolgens het beleid voor de toepassings toewijzing in de data base, dat is `Policy` opgeslagen in de tabel in de data base en de beleids-id is gebaseerd op de unieke id van de toepassing. Deze activiteit kan worden gevolgd in het **objreplmgr. log** door te verwijzen naar de unieke toewijzings-id, die kan worden verkregen van de SQL-query waarnaar wordt verwezen in de sectie [voordat u begint](app-deployment-technical-reference.md#before-you-begin) .

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

Het beleid voor de toepassings toewijzing kan worden weer gegeven in de-data base met behulp van een SQL-query zoals hieronder.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Doel items van beleid

Nadat het beleid is gegenereerd, wijst het onderdeel beleids provider dit beleid toe aan de resources in de verzameling die is gericht op de implementatie van de toepassing. De gegevens van het doel van het beleid worden `ResPolicyMap` opgeslagen in de tabel in de-data base. U kunt de PADBID die wordt geretourneerd door de bovenstaande query gebruiken om deze activiteit bij te houden in **policypv. log**. De PADBID die is vastgelegd in het logboek, kan echter niet altijd overeenkomen met de PADBID die wordt geretourneerd door de bovenstaande query als er meerdere beleids regels tegelijkertijd worden verwerkt.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap`de tabel bevat geen doel informatie voor toepassingen die worden geïmplementeerd als **beschikbaar** voor gebruikers verzamelingen. Software Center voert een lijst van deze toepassingen uit vanaf het beheer punt en de informatie over beleids doelen voor deze toepassingen wordt dynamisch gegenereerd wanneer een gebruiker een toepassing aanvraagt vanuit software Center.

## <a name="next-steps"></a>Volgende stappen

- [Toepassings implementatie naar verzamelingen apparaten](device-deployment-technical-reference.md)
- [Toepassings implementatie voor gebruikers verzamelingen](user-deployment-technical-reference.md)
