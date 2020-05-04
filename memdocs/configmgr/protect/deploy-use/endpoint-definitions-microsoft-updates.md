---
title: Definities van micro soft downloaden
titleSuffix: Configuration Manager
description: Meer informatie over het inschakelen van het downloaden van Endpoint Protection malware-definities van micro soft-updates voor Configuration Manager.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715688"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>Definities van Endpoint Protection schadelijke software inschakelen voor het downloaden van micro soft-updates

*Van toepassing op: Configuration Manager (huidige vertakking)*

Wanneer u selecteert om definitie-updates te downloaden van Microsoft Update, controleren clients de Microsoft Update site op basis van het interval dat is gedefinieerd in de sectie **beveiligings updates** van het dialoog venster antimalwarebeleid.

 Deze methode kan nuttig zijn wanneer de client geen verbinding heeft met de Configuration Manager site of wanneer u wilt dat gebruikers definitie-updates kunnen initiëren.

> [!IMPORTANT]
> - Clients moeten toegang hebben tot Microsoft Update op internet om via deze methode definitie-updates te downloaden.
> - De sectie **definitie-updates** is gewijzigd in **beveiligings updates** die beginnen met Configuration Manager versie 1902.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Definities downloaden met Microsoft Malware Protection Center
 U kunt clients configureren voor het downloaden van definitie-updates van Microsoft Malware Protection Center. Deze optie wordt gebruikt door Endpoint Protection-clients om definitie-updates te downloaden als ze geen updates van een andere bron kunnen downloaden. Deze update methode kan nuttig zijn als er een probleem is met uw Configuration Manager-infra structuur die het leveren van updates voor komt.

> [!IMPORTANT]
>  Clients moeten toegang hebben tot Microsoft Update op internet om via deze methode definitie-updates te downloaden.
> 
> 
> [!div class="button"]
> [Volgende stap >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Terug >](endpoint-configure-alerts.md)
