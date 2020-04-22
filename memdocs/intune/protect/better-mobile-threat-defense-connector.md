---
title: Better Mobile Threat Defense-connector met Intune
titleSuffix: Intune on Azure
description: Stel Better Mobile Threat Defense-connector in met Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05dec05cdc5a16078328d736d2f622cea1b2aa00
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "79353980"
---
# <a name="better-mobile-threat-defense-connector-with-intune"></a>Better Mobile Threat Defense-connector met Intune

U kunt de toegang van mobiele apparaten tot bedrijfsresources beheren met voorwaardelijke toegang op basis van een risicoanalyse die wordt uitgevoerd door Better Mobile, een MDT-oplossing (Mobile Threat Defense) die in Microsoft Intune is geïntegreerd. Risico's worden beoordeeld op basis van telemetrische gegevens die zijn verzameld op apparaten waarop de Better Mobile-app wordt uitgevoerd.

U kunt beleidsregels voor voorwaardelijke toegang configureren op basis van de Better Mobile-risicoanalyse die via het Intune-nalevingsbeleid voor apparaten wordt ingeschakeld voor ingeschreven apparaten. U kunt met dit beleid de toegang tot bedrijfsresources voor niet-conforme apparaten toestaan of blokkeren op basis van de gedetecteerde bedreigingen. Voor niet-ingeschreven apparaten kunt u app-beveiligingsbeleid gebruiken om het blokkeren of selectief wissen af te dwingen op basis van gedetecteerde bedreigingen.

## <a name="how-do-intune-and-better-mobile-help-protect-your-company-resources"></a>Hoe kunt u met Intune en Better Mobile uw bedrijfsresources beter beveiligen?

De Better Mobile-app wordt geïnstalleerd en uitgevoerd op mobiele apparaten. Met deze app legt u telemetrische gegevens vast over het bestandssysteem, de netwerkstack, het apparaat en de apps waar dergelijke gegevens beschikbaar zijn, en verzendt u die gegevens naar Better Mobile om te bepalen hoe groot het risico's voor het apparaat op mobiele bedreigingen is.

- **Ondersteuning voor ingeschreven apparaten**: Het nalevingsbeleid voor Intune-apparaten bevat een regel voor verdediging tegen mobiele dreigingen. Voor dit beleid kan informatie over risicoanalyse van Better Mobile worden gebruikt. Als de MTD-regel is ingeschakeld, controleert Intune of het apparaat voldoet aan het beleid dat u hebt ingeschakeld. Als het apparaat niet aan het beleid blijkt te voldoen, wordt de toegang van gebruikers tot resources als Exchange Online en SharePoint Online geblokkeerd. Gebruikers ontvangen ook richtlijnen van de Better Mobile-app die op hun apparaat is geïnstalleerd, zodat ze het probleem kunnen oplossen en weer toegang kunnen krijgen tot bedrijfsresources. Voor ondersteuning van Better Mobile voor ingeschreven apparaten:
  - [MTD-apps aan apparaten toevoegen](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Nalevingsbeleid voor apparaten maken dat MTD ondersteunt](../protect/mtd-device-compliance-policy-create.md)
  - [De MTD-connector in Intune inschakelen](../protect/mtd-connector-enable.md)

- **Ondersteuning voor uitgeschreven apparaten**: Intune kan de gegevens van de risicoanalyse van de Better Mobile-app gebruiken voor uitgeschreven apparaten wanneer u beveiligingsbeleidsregels voor Intune-apps gebruikt. Beheerders kunnen deze combinatie gebruiken om bedrijfsgegevens te beschermen binnen een [met Microsoft Intune beveiligde app](../apps/apps-supported-intune-apps.md). Beheerders kunnen bedrijfsgegevens op deze ingeschreven apparaten ook blokkeren of selectief wissen. Voor ondersteuning van Better Mobile voor niet-ingeschreven apparaten:
  - [De MTD-app toevoegen aan niet-ingeschreven apparaten](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Beveiligingsbeleid voor Mobile Threat Defense-apps maken](../protect/mtd-app-protection-policy.md)
  - [De MTD-connector in Intune inschakelen voor niet-ingeschreven apparaten](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Ondersteunde platforms

- **Android 4.1 en hoger**

- **iOS 8.0 en hoger**

## <a name="prerequisites"></a>Vereisten

- Azure Active Directory Premium

- Microsoft Intune-abonnement

- Better Mobile Threat Defense-abonnement

  - Zie de [Better Mobile-website](https://www.better.mobi/) voor meer informatie.

## <a name="sample-scenarios"></a>Voorbeeldscenario's

Hier volgen enkele veelvoorkomende scenario's.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Toegangsbeheer op basis van bedreigingen van schadelijke apps

Als er op apparaten schadelijke apps zoals malware worden gedetecteerd, kunt u apparaten blokkeren tegen acties als de volgende totdat de bedreiging is opgelost:

- Verbinding met bedrijfs-e-mail

- Synchronisatie van bedrijfsbestanden met de app OneDrive voor werk

- Toegang tot bedrijfs-apps

Blokkeren wanneer er schadelijke apps zijn gedetecteerd:

![Afbeelding waarin gedetecteerde schadelijke apps worden weergegeven](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png)

Toegang wordt verleend na herstel:

![Toegang verleend nadat schadelijke apps zijn gedetecteerd](./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Toegangsbeheer op basis van bedreigingen voor het netwerk

Bedreigingen voor uw netwerk worden gedetecteerd, zoals **man-in-the-middle-aanvallen**, en de toegang tot Wi-Fi-netwerken wordt beveiligd op basis van apparaatrisico.

Netwerktoegang via Wi-Fi blokkeren:

![Netwerktoegang via Wi-Fi blokkeren](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png)

Toegang wordt verleend na herstel:

![Afbeelding waarin verleende toegang na herstel wordt weergegeven](./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Toegangsbeheer voor SharePoint Online op basis van bedreigingen voor het netwerk

Bedreigingen voor uw netwerk worden gedetecteerd, zoals **man-in-the-middle-aanvallen**, en synchronisatie van bedrijfsbestanden wordt voorkomen op basis van het apparaatrisico.

SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd:

![SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png)

Toegang na herstel:

![Voorbeeld waarin na herstel toegang is verleend aan Sharepoint](./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png)

### <a name="control--access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Toegangsbeheer voor niet-ingeschreven apparaten op basis van bedreigingen van schadelijke apps

Wanneer de BETTER Mobile Threat Defense-oplossing een apparaat beschouwt als geïnfecteerd: ![App-beveiligingsbeleid blokkeert vanwege gedetecteerde malware](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png)

Toegang wordt verleend na herstel:

![Er wordt toegang verleend na herstel voor App-beveiligingsbeleid](./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Volgende stappen

- [Better Mobile integreren met Intune](better-mobile-mtd-connector-integration.md)

- [Better Mobile-apps instellen](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Better Mobile-nalevingsbeleid voor apparaten maken](mtd-device-compliance-policy-create.md)

- [Better Mobile MTD-connector inschakelen](mtd-connector-enable.md)

- [Een beveiligingsbeleid voor MTD-apps maken](mtd-app-protection-policy.md) 
