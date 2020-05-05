---
title: Gegevens en site-infrastructuur beveiligen
titleSuffix: Configuration Manager
description: Meer informatie over hoe u de resources van uw organisatie kunt beschermen tegen bloot stelling of kwaad aardige aanvallen met Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 381f9d190b1d73bbbab6142fd9587e881d0870ce
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81723913"
---
# <a name="protect-data-and-site-infrastructure"></a>Gegevens en site-infrastructuur beveiligen

*Van toepassing op: Configuration Manager (huidige vertakking)*

U wilt dat uw gebruikers veilig toegang hebben tot de resources van uw organisatie. Beveilig zowel uw infra structuur als uw gegevens tegen bloot stelling of kwaad aardige aanvallen. Gebruik Configuration Manager om toegang in te scha kelen en de resources van uw organisatie te beschermen.  

- Met [Endpoint Protection](../deploy-use/endpoint-protection.md) kunt u de volgende micro soft Defender-beleids regels voor client computers beheren:

  - Micro soft Defender antimalware
  - Micro soft Defender firewall
  - Microsoft Defender Advanced Threat Protection
  - Micro soft Defender exploit Guard
  - Microsoft Defender Application Guard
  - Microsoft Defender-toepassingsbeheer

  > [!TIP]
  > Als u Endpoint Protection wilt beheren op met co beheerde Windows 10-apparaten met behulp van de micro soft Endpoint Manager-Cloud service, schakelt u de [ **Endpoint Protection** workload](../../comanage/workloads.md#endpoint-protection) over naar intune. Zie [Endpoint Protection voor Microsoft intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10)voor meer informatie.

- Beveilig gegevens die zijn opgeslagen op on-premises Windows-clients met BitLocker-stationsversleuteling (BDE). Configuration Manager biedt een volledig beheer van de BitLocker-levenscyclus waarmee het gebruik van micro soft BitLocker Administration and monitoring (MBAM) kan worden vervangen. Zie voor meer informatie [plannen voor BitLocker-beheer](../plan-design/bitlocker-management.md).

- Schakel in plaats van traditionele wacht woorden alternatieve aanmeldings methoden in op Windows 10-apparaten met Windows hello voor bedrijven. Zie [Windows hello voor bedrijven-instellingen](../deploy-use/windows-hello-for-business-settings.md)voor meer informatie.

- Minimaliseer de inspanningen van uw gebruikers om verbinding te maken met bronnen door VPN-verbindingen via VPN-profielen in te scha kelen. Zie [VPN-profielen](../deploy-use/vpn-profiles.md)voor meer informatie.  

- Wi-Fi-profielen bieden een set hulpprogram ma's en bronnen waarmee u instellingen voor draadloze netwerken op apparaten in uw organisatie kunt beheren. Door deze instellingen te implementeren, beperkt u de moeite die eind gebruikers nodig hebben om verbinding te maken met draadloze netwerken. Zie [Wi-Fi-profielen](../deploy-use/create-wifi-profiles.md)voor meer informatie.  

- Apparaten inrichten met de certificaten die gebruikers nodig hebben om verbinding te maken met resources. Zie [certificaat profielen](../deploy-use/introduction-to-certificate-profiles.md)voor meer informatie.  
