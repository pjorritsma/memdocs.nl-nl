---
title: Symantec Endpoint Protection Mobile-connector gebruiken met Microsoft Intune
titleSuffix: Microsoft Intune
description: Meer informatie over de integratie van Intune met Symantec Endpoint Protection Mobile om de toegang van mobiele apparaten tot bedrijfsresources te beheren.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: df4ce3f6-a093-432c-ab86-7a83865e389e
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b078996ba5c7822ce9d8273be1df96a7aad0248b
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330964"
---
# <a name="symantec-endpoint-protection-mobile-connector"></a>Symantec Endpoint Protection Mobile-connector

U kunt de toegang van mobiele apparaten tot bedrijfsresources beheren door middel van voorwaardelijke toegang op basis van een risicoanalyse die wordt uitgevoerd in SEP Mobile (Symantec Endpoint Protection Mobile), een oplossing voor de beveiliging tegen bedreigingen op mobiele apparaten die met Microsoft Intune is geïntegreerd. Risico's worden beoordeeld op basis van telemetrische gegevens die zijn verzameld op apparaten waarop SEP Mobile wordt uitgevoerd, zoals:

- Fysieke beveiliging

- Netwerkbeveiliging

- Toepassingsbeveiliging

- Beveiliging tegen zwakke plekken

U kunt SEP Mobile-risicoanalyse inschakelen via het Intune-nalevingsbeleid voor apparaten. Vervolgens kunt u voorwaardelijk toegangsbeleid gebruiken om de toegang tot bedrijfsresources voor niet-conforme apparaten toe te staan of te blokkeren op basis van de gedetecteerde bedreigingen.

> [!NOTE]
> Deze Mobile Threat Defense-leverancier wordt niet ondersteund voor niet-ingeschreven apparaten.

## <a name="supported-platforms"></a>Ondersteunde platforms

- **Android 4.1 en hoger**

- **iOS 8 en hoger**

## <a name="pre-requisites"></a>Vereisten

- Azure Active Directory Premium

- Microsoft Intune-abonnement

- Symantec Endpoint Protection Mobile-abonnement

Ga naar de [Symantec-website](https://help.symantec.com/cs/sep_mobile/SEPMOBILE/v131237277_v127904070/Integrating-Microsoft-Intune-with-Endpoint-Protection-Mobile?locale=EN_US) voor meer informatie.

## <a name="how-do-intune-and-sep-mobile-help-protect-your-company-resources"></a>Hoe kunt u met Intune en SEP Mobile uw bedrijfsresources beter beveiligen?

Met de mobiele Android- of iOS-/iPadOS-app voor SEP Mobile worden telemetriegegevens vastgelegd over het bestandssysteem, de netwerkstack, apparaten en apps waar dergelijke gegevens beschikbaar zijn. Met de app worden die gegevens vervolgens verzonden naar de SEP Mobile-cloudservice om te bepalen hoe groot het risico van bedreigingen is voor het mobiele apparaat.

Het Intune-nalevingsbeleid voor apparaten bevat een regel voor SEP Mobile die is gebaseerd op de SEP Mobile-risicoanalyse. Als deze regel is ingeschakeld, controleert Intune of het apparaat voldoet aan het beleid dat u hebt ingeschakeld.

Als het apparaat niet aan het beleid blijkt te voldoen, wordt de toegang tot resources als Exchange Online en SharePoint Online geblokkeerd. Gebruikers op geblokkeerde apparaten ontvangen richtlijnen van de mobiele app voor SEP Mobile zodat ze het probleem kunnen oplossen en weer toegang kunnen krijgen tot bedrijfsresources.

Intune biedt ondersteuning voor twee integratiemodi met SEP Mobile:

- **Basisinstallatie** op basis van een modus voor alleen-lezen waarbij voor SEP Mobile de apparaten in Intune worden weergegeven.

- **Volledige integratie** waarbij met SEP Mobile apparaatrisico- en beveiligingsincidentgegevens kunnen worden gemeld aan Intune.

## <a name="sample-scenarios"></a>Voorbeeldscenario's

Hier volgen enkele veelvoorkomende scenario's:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Toegangsbeheer op basis van bedreigingen van schadelijke apps

Als er op apparaten schadelijke apps zoals malware worden gedetecteerd, kunt u apparaten blokkeren totdat de bedreiging is opgelost:

- Verbinding met bedrijfs-e-mail

- Synchronisatie van bedrijfsbestanden met de app OneDrive voor werk

- Toegang tot bedrijfs-apps

*Blokkeren wanneer er schadelijke apps zijn gedetecteerd:*

![Conceptafbeelding van detectie van schadelijke apps](./media/skycure-mobile-threat-defense-connector/symantec-arch-1.png)

*Toegang na herstel:*

![Afbeelding van toegang die wordt verleend na herstel nadat schadelijke apps zijn gedetecteerd](./media/skycure-mobile-threat-defense-connector/symantec-arch-2.png)

### <a name="control-access-based-on-threat-to-network"></a>Toegangsbeheer op basis van bedreigingen voor het netwerk

Detecteer bedreigingen zoals **man-in-the-middle**-aanvallen in het netwerk en beveilig de toegang tot Wi-Fi-netwerken op basis van het apparaatrisico.

*Netwerktoegang via Wi-Fi blokkeren:*

![Netwerktoegang via Wi-Fi blokkeren](./media/skycure-mobile-threat-defense-connector/symantec-arch-3.png)

*Toegang na herstel:*

![Toegang na herstel](./media/skycure-mobile-threat-defense-connector/symantec-arch-4.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Toegangsbeheer voor SharePoint Online op basis van bedreigingen voor het netwerk

Detecteer bedreigingen zoals **man-in-the-middle**-aanvallen in het netwerk en voorkom synchronisatie van bedrijfsbestanden op basis van het apparaatrisico.

*SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd:*

![SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd](./media/skycure-mobile-threat-defense-connector/symantec-arch-5.png)

*Toegang na herstel:*

![Voorbeeld waarin na herstel toegang is verleend aan Sharepoint](./media/skycure-mobile-threat-defense-connector/symantec-arch-6.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Symantec Endpoint Protection Mobile Threat Defense solution considers a device to be infected:
![App protection policy blocks due to detected malware](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/skycure-mobile-threat-defense-connector/symantec-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Volgende stappen

Hier volgen de stappen die u moet uitvoeren om Intune met SEP Mobile te integreren:

- [SEP Mobile-integratie met Intune instellen](skycure-mtd-connector-integration.md)

- [SEP Mobile-apps, Microsoft Authenticator en het configuratiebeleid voor iOS-/iPadOS-apps toevoegen en toewijzen](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [SEP Mobile-nalevingsbeleid voor apparaten met Intune maken](mtd-device-compliance-policy-create.md)

- [De SEP Mobile MTD-connector in Intune inschakelen](mtd-connector-enable.md)
