---
title: Pradeo Mobile Threat Defense-connector met Intune
titleSuffix: Intune on Azure
description: Meer informatie over de integratie van Intune met de connector Pradeo Mobile Threat Defense om toegang tot uw bedrijfsresources met mobiele apparaten te beheren.
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
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cde4c4e90004dd9bb287b9e86f9dfcc541e4a33
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984956"
---
# <a name="pradeo-mobile-threat-defense-connector-with-intune"></a>Pradeo Mobile Threat Defense-connector met Intune

U kunt de toegang van mobiele apparaten tot bedrijfsresources beheren met voorwaardelijke toegang op basis van een risicoanalyse die wordt uitgevoerd door Pradeo, een MTD-oplossing (Mobile Threat Defense) die in Microsoft Intune is geïntegreerd. Risico's worden beoordeeld op basis van telemetrische gegevens die zijn verzameld op apparaten waarop de Pradeo-app wordt uitgevoerd.

U kunt beleidsregels voor voorwaardelijke toegang configureren op basis van de Pradeo-risicoanalyse die via het Intune-nalevingsbeleid voor apparaten wordt ingeschakeld. U kunt met dit beleid de toegang tot bedrijfsresources voor niet-conforme apparaten toestaan of blokkeren op basis van de gedetecteerde bedreigingen.

> [!NOTE]
> Deze Mobile Threat Defense-leverancier wordt niet ondersteund voor niet-ingeschreven apparaten.

## <a name="supported-platforms"></a>Ondersteunde platforms

- **Android 4.0.3 en hoger**

- **iOS 7 en hoger**

## <a name="prerequisites"></a>Vereisten

- Azure Active Directory Premium

- Microsoft Intune-abonnement

- Pradeo Security for Mobile Threat Defense-abonnement

  - Zie de [Pradeo-website](https://www.pradeo.com/en-US/mobile-threat-protection) voor meer informatie.

## <a name="how-do-intune-and-pradeo-help-protect-your-company-resources"></a>Hoe kunt u met Intune en Pradeo uw bedrijfsresources beter beveiligen?

De Pradeo-app voor Android of iOS/iPadOS legt telemetriegegevens vast over het bestandssysteem, de netwerkstack, apparaten en apps waar dergelijke gegevens beschikbaar zijn. De app verzendt die gegevens vervolgens naar de Pradeo-cloudservice om te bepalen hoe groot het risico van bedreigingen is voor het mobiele apparaat.

Het Intune-nalevingsbeleid voor apparaten bevat een regel voor Pradeo Mobile Threat Defense die is gebaseerd op de Pradeo-risicoanalyse. Als deze regel is ingeschakeld, controleert Intune of het apparaat voldoet aan het beleid dat u hebt ingeschakeld. Als het apparaat niet aan het beleid blijkt te voldoen, wordt de toegang van gebruikers tot resources als Exchange Online en SharePoint Online geblokkeerd. Gebruikers ontvangen ook richtlijnen van de Pradeo-app die op hun apparaat is geïnstalleerd, zodat ze het probleem kunnen oplossen en weer toegang kunnen krijgen tot bedrijfsresources.

## <a name="sample-scenarios"></a>Voorbeeldscenario's

Hier volgen enkele veelvoorkomende scenario's.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Toegangsbeheer op basis van bedreigingen van schadelijke apps

Als er op apparaten schadelijke apps zoals malware worden gedetecteerd, kunt u apparaten blokkeren tegen acties als de volgende totdat de bedreiging is opgelost:

- Verbinding met bedrijfs-e-mail

- Synchronisatie van bedrijfsbestanden met de app OneDrive voor werk

- Toegang tot bedrijfs-apps

*Blokkeren wanneer er schadelijke apps zijn gedetecteerd:*

![Conceptafbeelding van detectie van schadelijke apps](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png)

*Toegang na herstel:*

![Toegang verleend nadat schadelijke apps zijn gedetecteerd](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Toegangsbeheer op basis van bedreigingen voor het netwerk

Bedreigingen voor uw netwerk worden gedetecteerd, zoals **man-in-the-middle-aanvallen**, en de toegang tot Wi-Fi-netwerken wordt beveiligd op basis van apparaatrisico.

*Netwerktoegang via Wi-Fi blokkeren:*

![Netwerktoegang via Wi-Fi blokkeren](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png)

*Toegang na herstel:*

![Conceptafbeelding van toegewezen toegang bij herstel](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Toegangsbeheer voor SharePoint Online op basis van bedreigingen voor het netwerk

Bedreigingen voor uw netwerk worden gedetecteerd, zoals **man-in-the-middle-aanvallen**, en synchronisatie van bedrijfsbestanden wordt voorkomen op basis van het apparaatrisico.

*SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd:*

![SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png)

*Toegang na herstel:*

![Conceptafbeelding waarin na herstel toegang is verleend aan Sharepoint](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Pradeo Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Volgende stappen

- [Pradeo integreren met Intune](pradeo-mtd-connector-integration.md)

- [Pradeo-apps instellen](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Pradeo-nalevingsbeleid voor apparaten maken](mtd-device-compliance-policy-create.md)

- [Pradeo MTD-connector inschakelen](mtd-connector-enable.md)
