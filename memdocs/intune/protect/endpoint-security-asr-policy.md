---
title: Instellingen voor kwetsbaarheid tegen aanvallen verminderen beheren met eindpuntbeveiligingsbeleid in Microsoft Intune | Microsoft Docs
description: Configureer en implementeer beleidsregels voor apparaten die u beheert met eindpuntbeveiligingsinstellingen voor het beleid om kwetsbaarheid voor aanvallen te verminderen in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/3/2020
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
ms.openlocfilehash: 303acae2eba275907b70fcc52660217568913c62
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432520"
---
# <a name="attack-surface-reduction-policy-for-endpoint-security-in-intune"></a>Beleid om kwetsbaarheid voor aanvallen te verminderen voor eindpuntbeveiliging in Intune

Wanneer Defender-antivirus wordt gebruikt op uw Windows 10-apparaten, kunt u Intune-eindpuntbeveiligingsbeleid gebruiken voor het verminderen van de kwetsbaarheid voor aanvallen om die instellingen voor uw apparaten te beheren.

Met het beleid voor het verminderen van kwetsbaarheid voor aanvallen kunt u uw kwetsbare voor aanvallen verminderen door de locaties te minimaliseren waar uw organisatie kwetsbaar is voor cyberdreigingen en aanvallen. Zie voor meer informatie [Overzicht van kwetsbaarheid voor aanvallen verminderen]( /windows/security/threat-protection/microsoft-defender-atp/overview-attack-surface-reduction) in de documentatie Windows-bescherming tegen bedreigingen.

U kunt het eindpuntbeveiligingsbeleid vinden bij kwetsbaarheid voor aanvallen verminderen onder *Beheren* in het knooppunt **Eindpuntbeveiliging** van het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431). Elk *profiel* voor het verminderen van kwetsbaarheid voor aanvallen beheert instellingen voor een bepaald gebied van een Windows 10-apparaat.

Bekijk [instellingen voor profielen die kwetsbaarheid voor aanvallen verminderen](../protect/endpoint-security-asr-profile-settings.md).

## <a name="prerequisites-for-attack-surface-reduction-profiles"></a>Vereisten voor profielen die kwetsbaarheid voor aanvallen verminderen

- Windows 10 of hoger
- Defender-antivirus moet primair zijn op het apparaat

## <a name="attack-surface-reduction-profiles"></a>Profielen om kwetsbaarheid voor aanvallen te verminderen

**Windows 10-profielen**:

- **App-en browser isolatie**: instellingen voor Windows Defender Application Guard (Application Guard) beheren als onderdeel van de Defender-ATP. Application Guard helpt oude en nieuw aanvallen te voorkomen en kan door bedrijven gedefinieerde sites isoleren als niet-vertrouwd terwijl er ook wordt gedefinieerd welke sites, cloudbronnen en interne netwerken worden vertrouwd.

  Zie [Application Guard](/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview) in de Microsoft Defender ATP-documentatie voor meer informatie.

- **Webbeveiliging**: instellingen die u kunt beheren voor webbeveiliging in Microsoft Defender ATP netwerkbeveiliging configureren om uw computers te beveiligen tegen bedreigingen op internet. Door te integreren met Microsoft Edge en populaire browsers van derden, zoals Chrome en Firefox, worden webbeveiligingen zonder een webproxy gestopt en kunnen computers worden beschermd wanneer ze afwezig of on-premises zijn. Webbeveiliging stopt de toegang tot:
  - Phishing-sites
  - Malware-vectoren
  - Exploitatiesites
  - Niet-vertrouwde of sites met een slechte reputatie
  - Sites die u hebt geblokkeerd in uw aangepaste indicatorlijst.

  Zie [Webbeveiliging](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) in de Microsoft Defender ATP-documentatie voor meer informatie.

- **Toepassingsbeheer**: Instellingen voor toepassingsbeheer kunnen helpen beveiligingsrisico's te beperken door de toepassingen te beperken die gebruikers kunnen uitvoeren en de code die wordt uitgevoerd in de systeemkern (kernel). Instellingen beheren waarmee niet-ondertekende scripts en MSI’s kunnen worden geblokkeerd en Windows PowerShell kan worden beperkt om te worden uitgevoerd in de modus gebonden taal.

  Zie [Toepassingscontrole](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) in de Microsoft Defender ATP-documentatie voor meer informatie.
  
    > [!NOTE]
    > Als u deze instelling gebruikt, vraagt AppLocker CSP de eindgebruiker op dit moment om de computer opnieuw op te starten wanneer er beleid wordt geïmplementeerd.

- **Regels voor het verminderen van kwetsbaarheid voor aanvallen**: instellingen configureren voor beperkingsregels voor kwetsbaarheid voor aanvallen verminderen die gericht zijn op gedrag dat schadelijke software en schadelijke apps doorgaans gebruiken om computers te infecteren, waaronder:
  - Uitvoerbare bestanden en scripts die worden gebruikt in Office-apps of webmail en proberen bestanden te downloaden of uit te voeren
  - Verborgen of anderszins verdachte scripts
  - Gedrag dat apps normaal gesproken niet starten tijdens normale dagelijkse werkzaamheden waarbij uw kwetsbaarheid voor aanvallen wordt verkleind, betekent dat aanvallers minder manieren hebben om aanvallen uit te voeren.

  Zie [Regels die kwetsbaarheid voor aanvallen verminderen](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) in de Microsoft Defender ATP-documentatie voor meer informatie.

- **Apparaatbesturing**: met instellingen voor apparaatbesturing kunt u apparaten voor een gelaagde benadering configureren voor het beveiligen van verwisselbare media. Microsoft Defender ATP biedt meerdere bewakings-en controlefuncties waarmee wordt voorkomen dat niet-gemachtigde randapparaten uw apparaten schaden.

  Zie [Hoe u USB-apparaten en andere verwisselbare media beheert met behulp van Microsoft Defender ATP](/windows/security/threat-protection/device-control/control-usb-devices-using-intune) in de Microsoft Defender ATP-documentatie voor meer informatie.

- **Exploit Protection**: Exploit Protection-instellingen kunnen helpen beveiligen tegen malware die gebruikmaakt van exploits om apparaten te infecteren en dit te verspreiden. Exploit Protection bestaat uit een aantal beperkingen die kunnen worden toegepast op het besturingssysteem of afzonderlijke apps.

  Zie [Exploit Protection inschakelen](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) in de Microsoft Defender ATP-documentatie voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Eindpuntbeveiligingsbeleid configureren](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
