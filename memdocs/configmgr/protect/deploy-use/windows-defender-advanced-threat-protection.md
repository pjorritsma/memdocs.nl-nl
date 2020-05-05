---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Meer informatie over het beheren en bewaken van micro soft Defender Advanced Threat Protection, een nieuwe service die ondernemingen helpt bij het reageren op geavanceerde aanvallen.
ms.date: 04/27/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a635ae36875984537c18c4850a3526d57ffceb31
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210142"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Van toepassing op: Configuration Manager (huidige vertakking)*

Endpoint Protection kunt [micro soft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (voorheen bekend als Windows Defender ATP) beheren en bewaken. Micro soft Defender ATP helpt ondernemingen bij het detecteren, onderzoeken en reageren op geavanceerde aanvallen op hun netwerken. Met Configuration Manager-beleid kunt u Windows 10-clients voorbereiden en bewaken.

Micro soft Defender ATP is een service in de [Security Center van Windows Defender](https://securitycenter.windows.com). Als u een configuratie bestand voor het voorbereiden van de client toevoegt en implementeert, kunt Configuration Manager de status van de implementatie en de status van micro soft Defender ATP-agent bewaken. Micro soft Defender ATP wordt ondersteund op Pc's met de Configuration Manager-client of worden [beheerd door Microsoft intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

## <a name="prerequisites"></a>Vereisten

- Abonnement op de micro soft Defender Advanced Threat Protection-online service  
- Clients computers waarop de Configuration Manager-client wordt uitgevoerd
- Clients die een besturings systeem gebruiken dat wordt vermeld in de sectie [ondersteunde client besturingssystemen](#bkmk_os) .

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a>Ondersteunde client besturingssystemen
Op basis van de versie van Configuration Manager die u uitvoert, kunnen de volgende client besturingssystemen onboarding worden uitgevoerd:

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager versie 1910 en eerder

- Clients met Windows 10, versie 1607 en hoger

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager versie 2002 en hoger
<!--5229962-->
- Windows 7 SP1
- Windows 8.1
- Windows 10, versie 1607 of hoger
- Windows Server 2008 R2 SP1
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, versie 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>Een onboarding-configuratie bestand maken

1. Ga naar de [micro soft Defender ATP online-service](https://securitycenter.windows.com/) en meld u aan.
1. Selecteer **machine beheer** onder **instellingen**en selecteer vervolgens **onboarding**.
1. Selecteer de besturings systemen die u wilt vrijgeven uit de lijst.
   - Als u een onboarding van Windows 10, Windows Server 1803 en Windows Server 2019 hebt:
      1. Selecteer **Configuration Manager (huidige vertakking) versie 1606** en selecteer **pakket downloaden**.
      1. Down load het gecomprimeerde archief bestand (. zip) en pak de inhoud uit.
   - Als u een ander Windows-besturings systeem wilt voorbereiden: 
      1. Selecteer de besturings systemen die u wilt vrijgeven uit de lijst. Kies bijvoorbeeld **Windows 7 en 8,1** of **Windows Server 2008 R2 SP1, 2012 R2 en 2016**.
      1. Kopieer de waarden voor de **werkruimte sleutel** en **werk ruimte-id** van de sectie **verbinding configureren** zodra het proces is voltooid.

> [!IMPORTANT]
> - Het configuratie bestand van micro soft Defender ATP bevat gevoelige informatie die veilig moet worden bewaard.

## <a name="onboard-devices"></a>Apparaten onboarden

1. Ga in de Configuration Manager-console naar **activa en naleving** > **Endpoint Protection** > **Windows Defender ATP-beleid** en selecteer **Windows Defender ATP-beleid maken**. De wizard micro soft Defender ATP-beleid wordt geopend.  
1. Typ de **naam** en **Beschrijving** voor het micro soft Defender ATP-beleid en selecteer **onboarding**.
1. **Blader** naar het configuratie bestand dat is opgenomen in de micro soft Defender ATP Cloud service-Tenant van uw organisatie.
   - Voor **Windows 7 en 8,1** of **Windows Server 2008 R2 SP1, 2012 R2 en 2016**, geeft u de **werkruimte sleutel** en **werk ruimte-id**op.
   - Voor Configuration Manager versie 2002 hebt u de **werkruimte sleutel** en **werk ruimte-id** nodig, zelfs als u alleen apparaten met Windows Server 2019 en Windows Server 1803 of hoger gebruikt. U kunt deze waarden ophalen door **instellingen** > te selecteren die**Windows 7 en 8,1** van de [micro soft Defender ATP online-service](https://securitycenter.windows.com/)**onboarding** > hebben. <!--7054188-->
1. Geef de bestands voorbeelden op die worden verzameld en gedeeld met beheerde apparaten voor analyse.  

   - **Geen**

   - **Alle bestands typen**  
1. Bekijk de samen vatting en voltooi de wizard.  

Selecteer **implementeren** om het micro soft Defender ATP-beleid te richten op clients.

## <a name="monitor"></a>Controleren

1. Navigeer in de Configuration Manager-console naar **bewakings** > **beveiliging** en selecteer vervolgens **Windows Defender ATP**.  

1. Bekijk het micro soft Defender Advanced Threat Protection-dash board.  

    - **Implementatie status van de Windows Defender-agent**: het aantal en percentage van de in aanmerking komende beheerde client computers met actief micro soft Defender ATP-beleid onboarded  

    - **Windows Defender atp status van agent**: percentage van de rapportage status van client computers voor de micro soft Defender ATP-agent  

        - **Healthy** Goed werkt correct  

        - **Inactief** : er zijn geen gegevens naar de service verzonden tijdens de tijds periode  

        - **Agent status** : de systeem service voor de agent in Windows is niet actief  

        - **Geen onboarding** -beleid is toegepast, maar de agent heeft het beleid niet in de onboarding opgenomen  

## <a name="create-an-offboarding-configuration-file"></a>Een offboarding-configuratie bestand maken  

1. Meld u aan bij de [micro soft Defender ATP-online service](https://securitycenter.windows.com/).

1. Selecteer **machine beheer** onder **instellingen**en selecteer vervolgens **onboarding**.  

1. Selecteer **Configuration Manager (huidige vertakking) versie 1606** en selecteer het **eind punt offboarding**.  

1. Down load het gecomprimeerde archief bestand (. zip) en pak de inhoud uit. Offboarding-bestanden zijn 30 dagen geldig.

1. Ga in de Configuration Manager-console naar **activa en naleving** > **Endpoint Protection** > **Windows Defender ATP-beleid** en selecteer **Windows Defender ATP-beleid maken**. De wizard micro soft Defender ATP-beleid wordt geopend.  

1. Typ de **naam** en **Beschrijving** voor het micro soft Defender ATP-beleid en selecteer **Offboarding**.

1. **Blader** naar het configuratie bestand dat is opgenomen in de micro soft Defender ATP Cloud service-Tenant van uw organisatie.

1. Bekijk de samen vatting en voltooi de wizard.  

Selecteer **implementeren** om het micro soft Defender ATP-beleid te richten op clients.  

> [!IMPORTANT]
> De configuratie bestanden van micro soft Defender ATP bevatten gevoelige informatie die veilig moet worden bewaard.

## <a name="next-steps"></a>Volgende stappen

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Problemen met onboarding van micro soft Defender Advanced Threat Protection oplossen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
