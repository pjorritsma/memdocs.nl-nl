---
title: Microsoft Defender ATP in Microsoft Intune gebruiken - Azure | Microsoft Docs
description: Gebruik Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) met Intune voor het instellen, configureren en onboarden van uw Intune-apparaten met ATP. Gebruik vervolgens een ATP-risicobeoordeling voor uw apparaten met Intune-beleid voor apparaatcompatibiliteit en voorwaardelijke toegang om uw netwerkresources te beveiligen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1420bf03fe236decba0345e299eb5d5893f96c93
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915106"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Naleving voor Microsoft Defender ATP met voorwaardelijke toegang in Intune afdwingen

U kunt Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) integreren met Microsoft Intune als een Mobile Threat Defense-oplossing. Dankzij integratie kunt u beveiligingsrisico's helpen voorkomen en de impact van beveiligingsschending binnen een organisatie beperken.

Microsoft Defender ATP werkt op apparaten waarop Windows 10 of hoger wordt uitgevoerd, en op Android-apparaten.

Voor effectieve bescherming gebruikt u een combinatie van de volgende configuraties:

- **Maak een service-naar-service-verbinding tussen Intune en Microsoft Defender ATP**. Met deze verbinding kan Microsoft Defender ATP gegevens verzamelen over risico's voor ondersteunde apparaten die u beheert met Intune.
- **Gebruik een profiel voor apparaatconfiguratie om apparaten te onboarden met Microsoft Defender ATP**. U kunt apparaten onboarden om deze te configureren zodat ze communiceren met Microsoft Defender ATP en de gegevens aanleveren om hun risiconiveau te bepalen.
- **Gebruik een nalevingsbeleid voor apparaten om het risiconiveau dat u wilt toestaan te bepalen**. Risiconiveaus worden gerapporteerd door Microsoft Defender ATP. Apparaten die het toegestane risiconiveau overschrijden, worden aangeduid als niet-compatibel.
- **Gebruik beleid voor voorwaardelijke toegang** om te voorkomen dat gebruikers toegang krijgen tot bedrijfsresources vanaf apparaten die niet-compatibel zijn.

Wanneer u Intune integreert met Microsoft Defender ATP, hebt u ook toegang tot Threat & Vulnerability Management (TVM) van Microsoft Defender ATP en kunt u [Intune gebruiken voor het wegnemen van beveiligingsproblemen die door TVM op eindpunten zijn geïdentificeerd](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Voorbeeld van het gebruik van Microsoft Defender ATP met Intune

In het volgende voorbeeld wordt uitgelegd hoe deze oplossingen samenwerken om uw organisatie te beschermen. Voor dit voorbeeld zijn Microsoft Defender ATP en Intune al geïntegreerd.

Denk bijvoorbeeld aan een situatie waarin iemand een Word-bijlage met ingesloten schadelijke code verzendt naar een gebruiker binnen uw organisatie.

- De gebruiker opent de bijlage en activeert de inhoud.
- Een aanval met verhoogde bevoegdheden wordt gestart en een aanvaller vanaf een externe computer heeft beheerdersrechten op het apparaat van het slachtoffer.
- De aanvaller krijgt vervolgens extern toegang tot de andere apparaten van de gebruiker. Deze beveiligingsschending kan invloed hebben op de hele organisatie.

Microsoft Defender ATP kan beveiligingsgebeurtenissen zoals dit scenario helpen oplossen.

- In ons voorbeeld detecteert Microsoft Defender ATP dat het apparaat abnormale code uitvoerde, een escalatie van procesbevoegdheden onderging, schadelijke code injecteerde en een verdachte remote shell uitgaf.
- Op basis van deze acties van het apparaat [classificeert Microsoft Defender ATP het apparaat als een hoog risico](/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) en wordt een gedetailleerd rapport over de verdachte activiteiten bijgevoegd in de portal van Microsoft Defender Security Center.

U kunt Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) integreren met Microsoft Intune als een Mobile Threat Defense-oplossing. Dankzij integratie kunt u beveiligingsrisico's helpen voorkomen en de impact van beveiligingsschending binnen een organisatie beperken.

Omdat u Intune-nalevingsbeleid voor apparaten gebruikt dat apparaten met *Medium* of *Hoog* risiconiveau als niet-compatibel classificeert, wordt het gecompromitteerde apparaat als niet-compatibel geclassificeerd. Deze classificatie zorgt ervoor dat het beleid voor voorwaardelijke toegang wordt toegepast en de toegang tot uw bedrijfsresources voor dit apparaat wordt geblokkeerd.

Voor apparaten met Android kunt u ook Intune-beleid gebruiken om de configuratie voor Microsoft Defender ATP op Android te wijzigen. Raadpleeg [Webbeveiliging van Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md) voor meer informatie.

## <a name="prerequisites"></a>Vereisten

Als u Microsoft Defender ATP met Intune wilt gebruiken, moet u het volgende geconfigureerd en klaar voor gebruik hebben:

- Tenant met licentie voor Enterprise Mobility + Security E3 en Windows E5 (of Microsoft 365 Enterprise E5)
- Microsoft Intune-omgeving met [door Intune-beheerde](../enrollment/windows-enroll.md) Windows 10- of Android-apparaten die ook aan Azure AD zijn toegevoegd
- [Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)-omgeving die toegang geeft tot Microsoft Defender Security Center (ATP-portal)

> [!NOTE]
> Microsoft Defender ATP wordt niet ondersteund met Intune-beleid voor app-beveiliging voor iOS/iPadOS en Android.

## <a name="next-steps"></a>Volgende stappen

- Zie [Microsoft Defender ATP configureren in Intune](../protect/advanced-threat-protection-configure.md) om Microsoft Defender ATP te verbinden met Intune, apparaten te onboarden en beleid voor voorwaardelijke toegang te configureren.

Meer informatie vindt u in de Intune-documentatie:

- [Beveiligingstaken gebruiken in combinatie met kwetsbaarheidsbeheer in ATP om problemen op apparaten op te lossen](atp-manage-vulnerabilities.md)
- [Aan de slag met apparaatnalevingsbeleid](device-compliance-get-started.md)

Meer informatie vindt u in de Microsoft Defender ATP-documentatie:

- [Voorwaardelijke toegang van Microsoft Defender ATP](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP-risicodashboard](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)