---
title: Intune-eindpuntbeveiligingsinstellingen voor accountbeveiligingsbeleid | Microsoft Docs
description: Eindpuntbeveiligingsinstellingen voor accountbeveiligingsbeleid in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
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
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431992"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Instellingen voor accountbeveiligingsbeleid voor eindpuntbeveiliging in Intune

Bekijk de instellingen die u kunt configureren in profielen voor beleid voor *Accountbeveiliging* in het knooppunt voor eindpuntbeveiliging van Intune als onderdeel van een [eindpuntbeveiligingsbeleid](../protect/endpoint-security-policy.md).

Ondersteunde platforms en profielen:

- **Windows 10 en hoge**:
  - Profiel: **Accountbeveiliging** *(preview)*


## <a name="account-protection-profile"></a>Accountbeveiligingsprofiel

### <a name="account-protection"></a>Accountbeveiliging

- **Windows Hello voor Bedrijven blokkeren**

  Windows Hello voor Bedrijven is een alternatieve aanmeldmethode voor Windows die wachtwoorden, smartcards en virtuele smartcards vervangt.
  - **Niet geconfigureerd** (*standaardinstelling*): op apparaten wordt Windows Hello voor Bedrijven ingericht.
  - **Uitgeschakeld**: op apparaten wordt Windows Hello voor Bedrijven ingericht.
  - **Ingeschakeld**: op apparaten wordt Windows Hello voor Bedrijven niet ingericht voor gebruikers.
  
- **Inschakelen voor gebruik van beveiligingssleutels voor aanmelding**

  Schakel de Windows Hello-beveiligingssleutel in als aanmeldingsreferentie voor alle pc's in de tenant.
  - **Niet geconfigureerd** (*standaard*)
  - **Ja**

- **Credential Guard inschakelen**  
  [CSP: []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard maakt gebruik van Windows Hypervisor om beveiliging te leveren. Credential Guard vereist hardwareondersteuning voor beveiligd opstarten en DMA-beveiliging. Deze instelling heeft alleen effect op apparaten die voldoen aan de hardwarevereisten.
  - **Niet-geconfigureerd** *(standaardinstelling*): het gebruik van Credential Guard uitschakelen. Dit is de Windows-standaardinstelling.
  - **Inschakelen met UEFI-vergrendeling**: Credential Guard inschakelen en blokkeren dat de functie extern wordt uitgeschakeld. De permanente UEFI-configuratie moet namelijk handmatig worden gewist.
  - **Inschakelen zonder UEFI-vergrendeling**: Credential Guard inschakelen en toestaan dat deze wordt uitgeschakeld zonder fysieke toegang tot de computer.

## <a name="next-steps"></a>Volgende stappen

[Eindpuntbeveiligingsbeleid voor accountbeveiliging](../protect/endpoint-security-account-protection-policy.md)
