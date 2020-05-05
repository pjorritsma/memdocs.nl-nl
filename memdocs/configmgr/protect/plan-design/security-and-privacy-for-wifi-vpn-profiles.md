---
title: Wi-Fi-en VPN-profiel beveiliging en privacy
titleSuffix: Configuration Manager
description: Meer informatie over de beveiligings aanbevelingen voor het beheren van Wi-Fi-en VPN-profielen voor apparaten in Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81722065"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Beveiliging en privacy voor Wi-Fi-en VPN-profielen in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

## <a name="security-recommendations"></a>Aanbevelingen voor beveiliging

Gebruik de volgende aanbevolen beveiligings procedures wanneer u Wi-Fi-en VPN-profielen voor apparaten beheert.

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>Kies de veiligste opties die uw Wi-Fi-en VPN-infra structuur en client besturingssystemen kunnen ondersteunen

Wi-Fi-en VPN-profielen bieden een handige methode om Wi-Fi-en VPN-instellingen die uw apparaten al ondersteunen, centraal te distribueren en te beheren. Configuration Manager voegt geen Wi-Fi-of VPN-functionaliteit toe. Bepaal, implementeer en volg alle beveiligings aanbevelingen voor uw apparaten en infra structuur.

## <a name="privacy-information"></a>Privacy-informatie

U kunt Wi-Fi-en VPN-profielen gebruiken om te configureren dat client apparaten verbinding maken met Wi-Fi-en VPN-servers. Gebruik vervolgens Configuration Manager om te evalueren of die apparaten compatibel worden nadat de profielen zijn toegepast. De compatibiliteitsinformatie wordt door het beheerpunt naar de siteserver verzonden en deze informatie wordt opgeslagen in de sitedatabase. De informatie wordt versleuteld wanneer apparaten deze naar het beheer punt verzenden, maar deze wordt niet in een versleutelde indeling opgeslagen in de site database. Informatie wordt bewaard in de database en wordt na negentig dagen verwijderd door de siteonderhoudstaak **Verouderde gegevens van Configuration Manager verwijderen** . Het standaardinterval voor verwijderen is 90 dagen, maar dit kunt u wijzigen. Er wordt geen compatibiliteits informatie naar micro soft verzonden.

Standaard worden Wi-Fi-en VPN-profielen niet door apparaten geëvalueerd. Daarnaast moet u de profielen configureren en vervolgens implementeren voor gebruikers.  

Voordat u Wi-Fi-of VPN-profielen configureert, moet u rekening houden met uw privacy-vereisten.  
