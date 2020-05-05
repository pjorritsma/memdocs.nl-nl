---
title: VPN-profielen
titleSuffix: Configuration Manager
description: Meer informatie over hoe u VPN-profielen in Configuration Manager kunt gebruiken om VPN-instellingen te implementeren voor gebruikers in uw organisatie.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9463d857599e676da6267313df575c8881436f93
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722254"
---
# <a name="vpn-profiles-in-configuration-manager"></a>VPN-profielen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--1283610-->
Gebruik VPN-profielen in Configuration Manager om VPN-instellingen te implementeren voor gebruikers in uw organisatie. Door het implementeren van deze instellingen minimaliseert u de eindgebruikersinspanningen die vereist zijn om verbinding te maken met resources op het bedrijfsnetwerk.  

U wilt bijvoorbeeld alle Windows 10-apparaten configureren met de instellingen die vereist zijn om verbinding te maken met een bestands share op het interne netwerk. Maak een VPN-profiel met de instellingen die nodig zijn om verbinding te maken met het interne netwerk. Implementeer vervolgens dit profiel voor alle gebruikers met apparaten met Windows 10. Deze gebruikers zien de VPN-verbinding in de lijst met beschik bare netwerken en kunnen moeiteloos verbinding maken.

Wanneer u een VPN-profiel maakt, kunt u een breed scala aan beveiligings instellingen toevoegen. Deze instellingen omvatten certificaten voor Server validatie en client verificatie die u inricht met Configuration Manager-certificaat profielen. Zie [certificaat profielen](introduction-to-certificate-profiles.md)voor meer informatie.

> [!Note]
> Configuration Manager schakelt deze optionele functie standaard niet in. U moet deze functie inschakelen voordat u deze kunt gebruiken. Zie voor meer informatie [Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="supported-platforms"></a>Ondersteunde platforms

De volgende tabel beschrijft de VPN-profielen die u voor verschillende platformen kunt configureren.

|Type verbinding|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|
|---------------|-----------|----------|--------------|----------|
|**Pulse Secure**|Ja|Nee|Ja|Ja|
|**F5 Edge Client**|Ja|Nee|Ja|Ja|
|**Dell SonicWALL Mobile Connect**|Ja|Nee|Ja|Ja|
|**Check Point Mobile VPN**|Ja|Nee|Ja|Ja|
|**Microsoft SSL (SSTP)**|Ja|Ja|Ja|Nee|
|**Microsoft Automatic**|Ja|Ja|Ja|Nee|
|**IKEv2**|Ja|Ja|Ja|Nee|
|**PPTP**|Ja|Ja|Ja|Nee|
|**L2TP**|Ja|Ja|Ja|Nee|

## <a name="next-step"></a>Volgende stap

> [!div class="nextstepaction"]
> [VPN-profielen maken](create-vpn-profiles.md)

## <a name="see-also"></a>Zie ook

- [Vereisten voor VPN-profielen](../plan-design/prerequisites-for-wifi-vpn-profiles.md)

- [Beveiliging en privacy voor VPN-profielen](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
