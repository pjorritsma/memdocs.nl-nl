---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590526"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a>Azure AD-verificatie werkt niet
<!--7569264-->
Configuration Manager het gebruik van de service voor beveiligings tokens van Azure Active Directory (Azure AD) werkt niet. Het **CCM_STS. log** op het beheer punt bevat een vermelding die lijkt op de volgende fout: `ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` Deze bevat ook de HRESULT-0x80131040.

Een ander symptoom is problemen met een CMG (Cloud Management Gateway). Als u de CMG Connection Analyzer uitvoert, mislukt de test het CMG-kanaal voor beheer punt met de volgende fout:`Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

Dit probleem wordt veroorzaakt door een versie verschil met een ondersteunende bibliotheek.

U kunt het probleem omzeilen door **System.IdentityModel.Tokens.JWT.dll** te kopiëren van de map \bin\X64 van de installatiemap op de site server naar de map SMS_CCM \ CCM_STS \Bin op het beheer punt.
