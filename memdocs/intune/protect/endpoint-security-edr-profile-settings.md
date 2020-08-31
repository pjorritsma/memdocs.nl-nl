---
title: Instellingen voor Eindpuntdetectie en -respons van Intune-eindpuntbeveiliging | Microsoft Docs
description: Instellingen voor Eindpuntdetectie en -respons van eindpuntbeveiliging in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: e7896d2b5dff7132056ed004443e7fa3623f016e
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820014"
---
# <a name="endpoint-detection-and-response-policy-settings-for-endpoint-security-in-intune"></a>Instellingen voor het beleid voor eindpuntdetectie en -reactie van eindpuntbeveiliging in Intune

Bekijk de instellingen die u kunt configureren in profielen voor [beleid voor eindpuntdetectie en -respons](../protect/endpoint-security-edr-policy.md) in het knooppunt voor eindpuntbeveiliging van Intune.

Ondersteunde platformen en profielen:

- **Windows 10 en hoger**: Gebruik dit platform voor het beleid dat u wilt implementeren op apparaten die worden beheerd met Intune.
  - Profiel: **Eindpuntdetectie en -respons (MDM)**

- **Windows 10 en Windows Server (ConfigMgr)** : Gebruik dit platform voor het beleid dat u wilt implementeren op apparaten die worden beheerd door Configuration Manager.
  - Profiel: **Eindpuntdetectie en -respons (ConfigMgr)**

## <a name="endpoint-detection-and-response-mdm"></a>Eindpuntdetectie en -respons (MDM)

**Eindpuntdetectie en -respons**:

- **Type clientconfiguratiepakket voor Microsoft Defender ATP**

  Een ondertekend configuratiepakket uploaden dat wordt gebruikt om de Microsoft Defender ATP-client te onboarden.

  - **Niet geconfigureerd** (*standaard*)
  - **Onboarding-blob**  
  - **Offboarding-blob**  

  Als de optie is ingesteld op *Onboarding-blob*, kunt u de volgende instellingen configureren:

  - **Advanced Threat Protection-onboarding-blob**  
    Klik op **Onboardingbestand selecteren** om het deelvenster *Onboardingbestand selecteren* te openen waar u een `.onboarding`-bestand kunt opgeven.

  Als de optie is ingesteld op *Offboarding-blob*, kunt u de volgende instellingen configureren:
  
  - **Advanced Threat Protection-offboarding-blob**  
     Klik op **Offboardingbestand selecteren** om het deelvenster *Offboardingbestand selecteren* te openen waar u een `.offboarding`-bestand kunt opgeven.

- **Voorbeelddeling voor alle bestanden**  

  Hiermee wordt de configuratieparameter van de voorbeelddeling van Microsoft Defender Advanced Threat Protection geretourneerd of ingesteld.  
  - **Niet-geconfigureerd**   (*default*)
  - **Ja**

- **Frequentie van telemetrierapporten versnellen**

  - **Niet-geconfigureerd**   (*default*)
  - **Ja** - De frequentie van telemetrierapporten van Microsoft Defender Advanced Threat Protection versnellen.

## <a name="endpoint-detection-and-response-configmgr"></a>Eindpuntdetectie en -respons (ConfigMgr)

**Eindpuntdetectie en -respons**:

- **Voorbeelddeling voor alle bestanden**  

  Hiermee wordt de configuratieparameter van de voorbeelddeling van Microsoft Defender Advanced Threat Protection geretourneerd of ingesteld.  
  - **Niet-geconfigureerd**   (*default*)
  - **Ja**

- **Frequentie van telemetrierapporten versnellen**

  - **Niet-geconfigureerd**   (*default*)
  - **Ja** - De frequentie van telemetrierapporten van Microsoft Defender Advanced Threat Protection versnellen.

## <a name="next-steps"></a>Volgende stappen

[Instellingen voor eindpuntbeveiliging voor EDR](../protect/endpoint-security-edr-policy.md)
