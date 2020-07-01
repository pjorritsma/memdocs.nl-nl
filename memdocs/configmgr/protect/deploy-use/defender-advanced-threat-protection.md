---
title: Microsoft Defender Advanced Threat Protection
titleSuffix: Configuration Manager
description: Meer informatie over het beheren en bewaken van micro soft Defender Advanced Threat Protection, een nieuwe service die ondernemingen helpt bij het reageren op geavanceerde aanvallen.
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cbf7dd3e35db8d2020e96e2511017e43863f724e
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/01/2020
ms.locfileid: "85613489"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender Advanced Threat Protection

*Van toepassing op: Configuration Manager (huidige vertakking)*

Endpoint Protection kunt [micro soft Defender Advanced Threat Protection (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (voorheen bekend als Windows Defender ATP) beheren en bewaken. Micro soft Defender ATP helpt ondernemingen bij het detecteren, onderzoeken en reageren op geavanceerde aanvallen op hun netwerken. Met Configuration Manager-beleid kunt u Windows 10-clients voorbereiden en bewaken.

Micro soft Defender ATP is een service in [micro soft defender Security Center](https://securitycenter.windows.com). Als u een configuratie bestand voor het voorbereiden van de client toevoegt en implementeert, kunt Configuration Manager de status van de implementatie en de status van micro soft Defender ATP-agent bewaken. Micro soft Defender ATP wordt ondersteund op Pc's met de Configuration Manager-client of worden [beheerd door Microsoft intune](https://docs.microsoft.com/intune/protect/advanced-threat-protection).

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
Vanaf Configuration Manager versie 2002 kunt u de volgende besturings systemen onboarden:

- Windows 8.1
- Windows 10, versie 1607 of hoger
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016, versie 1803 of hoger
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>Over het onboarden naar ATP met Configuration Manager

Verschillende besturings systemen hebben verschillende behoeften voor het voorbereiden op ATP. Windows 8,1 en andere besturings systeem apparaten met een lagere versie moeten de **werkruimte sleutel** en **werk ruimte-id** voor onboarding hebben. Voor apparaten op het hoogste niveau, zoals Windows Server versie 1803, is het onboarding-configuratie bestand nodig. Configuration Manager installeert ook de micro soft Monitoring Agent (MMA) wanneer dit nodig is voor onboarded apparaten, maar de agent wordt niet automatisch bijgewerkt.

Besturings systemen op een hoger niveau zijn:
- Windows 10, versie 1607 en hoger
- Windows Server 2016, versie 1803 of hoger
- Windows Server 2019

Besturings systemen van lager niveau zijn onder andere:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, versie 1709 en lager

Wanneer u apparaten uitschakelt tot ATP met Configuration Manager, implementeert u het ATP-beleid naar een doel verzameling of meerdere verzamelingen. Soms bevat de doel verzameling apparaten met een wille keurig aantal ondersteunde besturings systemen. De instructies voor het onboarden van deze apparaten variëren, afhankelijk van of u een verzameling hebt die apparaten bevat met besturings systemen met een hoger niveau, lager niveau of beide.

- Als uw doel verzameling apparaten op hoger niveau en lagere niveaus bevat, gebruikt u de instructies voor het [onboarden van apparaten waarop een ondersteund besturings systeem wordt uitgevoerd](#bkmk_any_os) (aanbevolen).
- Als uw verzameling alleen apparaten op het hoogste niveau bevat, kunt u de [instructies voor onboarding op het hoogste niveau](#bkmk_uplevel)gebruiken.
- Als uw verzameling alleen apparaten van een lager niveau bevat, kunt u de [onboarding-instructies van het lagere niveau](#bkmk_downlevel)gebruiken.

> [!Warning]
> - Als uw doel verzameling apparaten op het hoogste niveau bevat, en u de instructies voor apparaten op een lager niveau gebruikt, worden de op het niveau van de apparaten op het upniveau niet uitgevoerd.
> - Als uw doel verzameling apparaten van een lager niveau bevat en u de instructies voor apparaten op het hoogste niveau gebruikt, worden de Down Level-apparaten niet meer onboarded.

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a>Onboarding van apparaten met elk ondersteund besturings systeem naar ATP (aanbevolen)
 U kunt apparaten met een van de [ondersteunde besturings systemen](#bkmk_os) op ATP onboarden door het configuratie bestand, de **werkruimte sleutel**en de **werk ruimte-id** op te geven Configuration Manager.

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>Het configuratie bestand, de werk ruimte-ID en de werkruimte sleutel ophalen

1. Ga naar de [micro soft Defender ATP online-service](https://securitycenter.windows.com/) en meld u aan.
1. Selecteer **instellingen**en selecteer vervolgens **onboarding** onder de kop **Apparaatbeheer** .
1. Selecteer voor het besturings systeem **Windows 10**.
1. Kies **micro soft Endpoint Configuration Manager huidige vertakking en later** voor de implementatie methode.
1. Klik op **pakket downloaden**.
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="Down load van configuratie bestand voor onboarding" lightbox="media/5229962-onboarding-configuration.png":::
1. Down load het gecomprimeerde archief bestand (. zip) en pak de inhoud uit.
1. Selecteer **instellingen**en selecteer vervolgens **onboarding** onder de kop **Apparaatbeheer** .
1. Voor het besturings systeem selecteert u **Windows 7 SP1 en 8,1** of **Windows Server 2008 R2 SP1, 2012 R2 en 2016** uit de lijst.
   - De **werkruimte sleutel** en **werk ruimte-id** zijn hetzelfde, ongeacht de opties die u kiest.
1. Kopieer de waarden voor de **werkruimte sleutel** en **werk ruimte-id** uit de sectie **verbinding configureren** .

   > [!IMPORTANT]
   > Het configuratie bestand van micro soft Defender ATP bevat gevoelige informatie die veilig moet worden bewaard.


### <a name="onboard-the-devices"></a>De apparaten onboarden

1. Ga in de Configuration Manager-console naar **activa en naleving**  >  **Endpoint Protection**  >  **micro soft Defender ATP-beleid**.
1. Selecteer **micro soft Defender ATP-beleid maken** om de wizard micro soft Defender ATP-beleid te openen. 
1. Typ de **naam** en **Beschrijving** voor het micro soft Defender ATP-beleid en selecteer **onboarding**.
1. **Blader** naar het configuratie bestand dat u hebt geëxtraheerd uit het gedownloade zip-bestand.
1. Geef de **werkruimte sleutel** en **werk ruimte-id** op en klik op **volgende**.

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="Wizard micro soft Defender ATP-beleid maken" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. Geef de bestands voorbeelden op die worden verzameld en gedeeld met beheerde apparaten voor analyse.  
   - **Geen**
   - **Alle bestands typen**  
1. Bekijk de samen vatting en voltooi de wizard.  
1. Klik met de rechter muisknop op het beleid dat u hebt gemaakt en selecteer vervolgens **implementeren** om het micro soft Defender ATP-beleid te richten op clients.

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a>Onboarding van apparaten met besturings systemen op het niveau van ATP

Op up-Level-clients is een voorbereidings configuratie bestand vereist voor onboarding naar ATP. Besturings systemen op een hoger niveau zijn:
- Windows 10, versie 1607 en hoger 
- Windows Server 2016, versie 1803 en hoger
- Windows Server 2019

Als uw doel verzameling apparaten op niveau van hoger of lager niveau bevat, of als u niet zeker weet, gebruikt u de instructies voor het [onboarden van apparaten waarop een ondersteund besturings systeem wordt uitgevoerd (aanbevolen)](#bkmk_any_os).

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>Een onboarding-configuratie bestand voor apparaten op het hoogste niveau ophalen

1. Ga naar de [micro soft Defender ATP online-service](https://securitycenter.windows.com/) en meld u aan.
1. Selecteer **instellingen**en selecteer vervolgens **onboarding** onder de kop **Apparaatbeheer** .
1. Selecteer voor het besturings systeem **Windows 10**.
1. Kies **micro soft Endpoint Configuration Manager huidige vertakking en later** voor de implementatie methode.
1. Klik op **pakket downloaden**.
1. Down load het gecomprimeerde archief bestand (. zip) en pak de inhoud uit.

> [!IMPORTANT]
> Het configuratie bestand van micro soft Defender ATP bevat gevoelige informatie die veilig moet worden bewaard.


### <a name="onboard-the-up-level-devices"></a>Onboarding van de apparaten op het hoogste niveau

1. Ga in de Configuration Manager-console naar **activa en naleving**  >  **Endpoint Protection**  >  **micro soft Defender ATP-beleid** en selecteer **micro soft Defender ATP-beleid maken**. De wizard micro soft Defender ATP-beleid wordt geopend.  
1. Typ de **naam** en **Beschrijving** voor het micro soft Defender ATP-beleid en selecteer **onboarding**.
1. **Blader** naar het configuratie bestand dat u hebt geëxtraheerd uit het gedownloade zip-bestand.
   > [!Note]
   > Voor Configuration Manager versie 2002 hebt u de **werkruimte sleutel** en **werk ruimte-id** nodig, zelfs als u alleen apparaten op het hoogste niveau voorbereidt. U kunt deze waarden ophalen door **instellingen**te selecteren die  >  Windows 7 en 8,1 van de micro soft Defender ATP online-service**onboarding**hebben  >  **Windows 7 and 8.1** . [Microsoft Defender ATP online service](https://securitycenter.windows.com/) <!--7054188-->
1. Geef de bestands voorbeelden op die worden verzameld en gedeeld met beheerde apparaten voor analyse.  
   - **Geen**
   - **Alle bestands typen**  
1. Bekijk de samen vatting en voltooi de wizard.  
1. Klik met de rechter muisknop op het beleid dat u hebt gemaakt en selecteer vervolgens **implementeren** om het micro soft Defender ATP-beleid te richten op clients.

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a>Onboarding van apparaten met lagere besturings systemen naar ATP

Down Level-clients vereisen de **werkruimte sleutel** en **werk ruimte-id** voor het voorbereiden op ATP. Besturings systemen van lager niveau zijn onder andere:
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016, versie 1709 en lager

Als uw doel verzameling apparaten op niveau van hoger of lager niveau bevat, of als u niet zeker weet, gebruikt u de instructies voor het [onboarden van apparaten waarop een ondersteund besturings systeem wordt uitgevoerd (aanbevolen)](#bkmk_any_os).

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>De werk ruimte-ID en werkruimte sleutel ophalen voor apparaten op een lager niveau

1. Ga naar de [micro soft Defender ATP online-service](https://securitycenter.windows.com/) en meld u aan.
1. Selecteer **instellingen**en selecteer vervolgens **onboarding** onder de kop **Apparaatbeheer** .
1. Voor het besturings systeem selecteert u **Windows 7 SP1 en 8,1** of **Windows Server 2008 R2 SP1, 2012 R2 en 2016** uit de lijst.
   - De **werkruimte sleutel** en **werk ruimte-id** zijn hetzelfde, ongeacht de opties die u kiest.
1. Kopieer de waarden voor de **werkruimte sleutel** en **werk ruimte-id** uit de sectie **verbinding configureren** .

### <a name="onboard-the-down-level-devices"></a>De Down Level-apparaten onboarden

1. Ga in de Configuration Manager-console naar **activa en naleving**  >  **Endpoint Protection**  >  **micro soft Defender ATP-beleid** en selecteer **micro soft Defender ATP-beleid maken**. De wizard micro soft Defender ATP-beleid wordt geopend.  
1. Typ de **naam** en **Beschrijving** voor het micro soft Defender ATP-beleid en selecteer **onboarding**.
1. Geef de **werkruimte sleutel** en **werk ruimte-id**op.
   > [!Note]
   > - Voor Configuration Manager versie 2002 hebt u het configuratie bestand nodig, zelfs als u alleen apparaten met een lager niveau ophaalt. U kunt deze waarden ophalen door **instellingen**te selecteren voor  >  **Onboarding**  >  **Windows 10** in de [online micro soft Defender ATP-service](https://securitycenter.windows.com/). <!--7054188--> 
   > - Het configuratie bestand van micro soft Defender ATP bevat gevoelige informatie die veilig moet worden bewaard.
1. Geef de bestands voorbeelden op die worden verzameld en gedeeld met beheerde apparaten voor analyse.  
   - **Geen**
   - **Alle bestands typen**  
1. Bekijk de samen vatting en voltooi de wizard.  
1. Klik met de rechter muisknop op het beleid dat u hebt gemaakt en selecteer vervolgens **implementeren** om het micro soft Defender ATP-beleid te richten op clients.


## <a name="monitor"></a>Controleren

1. Navigeer in de Configuration Manager-console naar **bewakings**  >  **beveiliging** en selecteer vervolgens **micro soft Defender ATP**.  

1. Bekijk het micro soft Defender Advanced Threat Protection-dash board.  

    - **Status van onboarding van micro soft Defender ATP-agent**: het aantal en percentage van de in aanmerking komende beheerde client computers met actief micro soft Defender ATP-beleid, onboarded  

    - **Micro soft Defender atp status van agent**: percentage van de rapportage status van client computers voor de micro soft Defender ATP-agent  

        - **Healthy** Goed werkt correct  

        - **Inactief** : er zijn geen gegevens naar de service verzonden tijdens de tijds periode  

        - **Agent status** : de systeem service voor de agent in Windows is niet actief  

        - **Geen onboarding** -beleid is toegepast, maar de agent heeft het beleid niet in de onboarding opgenomen  

## <a name="create-an-offboarding-configuration-file"></a>Een offboarding-configuratie bestand maken  

1. Meld u aan bij de [micro soft Defender ATP-online service](https://securitycenter.windows.com/).
1. Selecteer **instellingen**en selecteer vervolgens **Offboarding** onder de kop **Apparaatbeheer** .
1. Selecteer **Windows 10** voor het besturings systeem en **micro soft endpoint Configuration Manager huidige vertakking en later** voor de implementatie methode.
   - Als u de optie **Windows 10** gebruikt, zorgt u ervoor dat alle apparaten in de verzameling offboarded zijn en dat de MMA worden verwijderd wanneer dat nodig is.
1. Down load het gecomprimeerde archief bestand (. zip) en pak de inhoud uit. Offboarding-bestanden zijn 30 dagen geldig.

1. Ga in de Configuration Manager-console naar **activa en naleving**  >  **Endpoint Protection**  >  **micro soft Defender ATP-beleid** en selecteer **micro soft Defender ATP-beleid maken**. De wizard micro soft Defender ATP-beleid wordt geopend.  

1. Typ de **naam** en **Beschrijving** voor het micro soft Defender ATP-beleid en selecteer **Offboarding**.

1. **Blader** naar het configuratie bestand dat u hebt geëxtraheerd uit het gedownloade zip-bestand.

1. Bekijk de samen vatting en voltooi de wizard.  

Selecteer **implementeren** om het micro soft Defender ATP-beleid te richten op clients.  

> [!IMPORTANT]
> De configuratie bestanden van micro soft Defender ATP bevatten gevoelige informatie die veilig moet worden bewaard.

## <a name="next-steps"></a>Volgende stappen

- [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Problemen met onboarding van micro soft Defender Advanced Threat Protection oplossen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
