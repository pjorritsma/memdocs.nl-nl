---
title: Instellingen van het macOS Antivirus-beleid voor Microsoft Defender Antivirus voor Intune | Microsoft Docs
description: Bekijk een lijst met de instellingen in het Microsoft Defender Antivirus-profiel voor macOS. Dit profiel is een onderdeel van het antivirusbeleid voor eindpuntbeveiliging voor macOS in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: 9a0687b9e3938c93cfaebe0e064fd994077a92af
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086686"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Instellingen voor Microsoft Defender ATP voor Mac in Microsoft Intune

Bekijk de instellingen voor het *Antivirus*-profiel die u in Microsoft Intune kunt configureren voor Microsoft Defender ATP voor Mac. Zie [Microsoft Defender Advanced Threat Protection voor Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) in de Windows-documentatie voor meer informatie over deze instellingen.

**Microsoft Defender ATP**

- **Realtime-beveiliging**  
  Vereis dat Defender op macOS-apparaten gebruikmaakt van de realtime-bewakingsfunctionaliteit. Met realtime-bewaking wordt gezocht naar malware en wordt voorkomen dat deze op uw apparaat wordt geïnstalleerd of uitgevoerd. U kunt deze instelling gedurende een korte tijd uitschakelen, maar daarna wordt deze automatisch weer ingeschakeld.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Ingeschakeld**: het gebruik van realtime-bewaking wordt afgedwongen. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Uitgeschakeld**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Cloudbeveiliging**  
  Standaard stuurt Defender informatie naar Microsoft over eventuele gevonden problemen. Microsoft analyseert die gegevens om meer te weten te komen over problemen die u en andere klanten ondervinden, om verbeterde oplossingen te kunnen bieden. Beveiliging werkt het beste als *Automatische verzending van voorbeelden*  is ingeschakeld.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Ingeschakeld**: cloudbeveiliging is ingeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Uitgeschakeld**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Automatische verzending van voorbeelden**  
  Er worden voorbeeldbestanden naar Microsoft verzonden om gebruikers en uw organisatie te beschermen tegen mogelijke dreigingen.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Ingeschakeld**: cloudbeveiliging is ingeschakeld.  Apparaatgebruikers kunnen deze instelling niet wijzigen.
  - **Uitgeschakeld**: de instelling is uitgeschakeld. Apparaatgebruikers kunnen deze instelling niet wijzigen.

- **Diagnosegegevens verzamelen**

  Configureer hoe diagnostische en gebruiksgegevens worden gedeeld met Microsoft.

  - **Niet geconfigureerd** (*standaard*): de instelling wordt teruggezet op de systeemstandaard.
  - **Vereist**
  - **Optioneel**

- **Mappen die worden uitgesloten van scannen**  
  Selecteer **Toevoegen** en geef de mappen op die tijdens een scan moeten worden genegeerd.

- **Bestanden die worden uitgesloten van scannen**  
  Selecteer **Toevoegen** en geef de bestanden op die tijdens een scan moeten worden genegeerd.

- **Bestandstypen die worden uitgesloten van scannen**  
  Selecteer **Toevoegen** en geef de bestandsextensies op die tijdens een scan moeten worden genegeerd.

- **Processen die worden uitgesloten van scannen**  
  Selecteer **Toevoegen** en geef de processen op die tijdens een scan moeten worden genegeerd.
