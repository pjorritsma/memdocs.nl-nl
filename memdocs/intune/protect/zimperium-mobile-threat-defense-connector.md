---
title: Zimperium MTD-connector met Intune
titleSuffix: Intune on Azure
description: Meer informatie over de integratie van Intune met Zimperium Mobile Threat Defense om toegang tot uw bedrijfsresources met mobiele apparaten te bepalen.
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
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b443f922b31523ec6f27971648ba1ea9c5123867
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989400"
---
# <a name="zimperium-mobile-threat-defense-connector-with-intune"></a>Zimperium Mobile Threat Defense-connector inschakelen met Intune

U kunt de toegang van mobiele apparaten tot bedrijfsresources beheren door middel van voorwaardelijke toegang op basis van een risicoanalyse die wordt uitgevoerd door Zimperium, een oplossing voor de beveiliging tegen bedreigingen op mobiele apparaten (MTD) die met Microsoft Intune is geïntegreerd. Risico's worden beoordeeld op basis van telemetrische gegevens die zijn verzameld op apparaten waarop de Zimperium-app wordt uitgevoerd.

U kunt het beleid voor voorwaardelijke toegang configureren op basis van de Zimperium-risicoanalyse die via het Intune-nalevingsbeleid voor apparaten wordt ingeschakeld. U kunt met dit beleid de toegang tot bedrijfsresources voor niet-compatibele apparaten toestaan of blokkeren op basis van de gedetecteerde bedreigingen. Voor niet-ingeschreven apparaten kunt u app-beveiligingsbeleid gebruiken om het blokkeren of selectief wissen af te dwingen op basis van gedetecteerde bedreigingen.

## <a name="supported-platforms"></a>Ondersteunde platforms

- **Android 4.1 en hoger**

- **iOS 8 en hoger**

## <a name="prerequisites"></a>Vereisten

- Azure Active Directory Premium

- Microsoft Intune-abonnement

- Zimperium Mobile Threat Defense-abonnement

  - Raadpleeg de [Zimperium-website](https://www.zimperium.com/zips-mobile-ips) voor meer informatie.

## <a name="how-do-intune-and-zimperium-help-protect-your-company-resources"></a>Hoe kunt u met Intune en Zimperium uw bedrijfsresources beter beveiligen?

De Zimperium-app voor Android of iOS/iPadOS legt telemetriegegevens vast over het bestandssysteem, de netwerkstack, apparaten en apps waar dergelijke gegevens beschikbaar zijn. De app verzendt die gegevens vervolgens naar de Zimperium-cloudservice om te bepalen hoe groot het risico van bedreigingen is voor het mobiele apparaat.

- **Ondersteuning voor ingeschreven apparaten**: Het Intune-nalevingsbeleid voor apparaten bevat een regel voor de beveiliging van mobiele bedreigingen (MTD; Mobile Threat Defense), die risicoanalysegegevens van Zimperium kan gebruiken. Als de MTD-regel is ingeschakeld, controleert Intune of het apparaat voldoet aan het beleid dat u hebt ingeschakeld. Als het apparaat niet aan het beleid blijkt te voldoen, wordt de toegang van gebruikers tot resources als Exchange Online en SharePoint Online geblokkeerd. Gebruikers ontvangen ook richtlijnen van de Zimperium-app die op hun apparaat is geïnstalleerd, zodat ze het probleem kunnen oplossen en weer toegang kunnen krijgen tot bedrijfsresources. Ondersteuning van Zimperium voor ingeschreven apparaten:
  - [MTD-apps aan apparaten toevoegen](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Nalevingsbeleid voor apparaten maken dat MTD ondersteunt](../protect/mtd-device-compliance-policy-create.md)
  - [De MTD-connector in Intune inschakelen](../protect/mtd-connector-enable.md)

- **Ondersteuning voor uitgeschreven apparaten**: Intune kan de gegevens van de risicoanalyse van de Zimperium-app gebruiken voor uitgeschreven apparaten wanneer u beveiligingsbeleidsregels voor Intune-apps gebruikt. Beheerders kunnen deze combinatie gebruiken om bedrijfsgegevens te beschermen binnen een [met Microsoft Intune beveiligde app](../apps/apps-supported-intune-apps.md). Beheerders kunnen bedrijfsgegevens op deze ingeschreven apparaten ook blokkeren of selectief wissen. Ondersteuning van Zimperium voor uitgeschreven apparaten:
  - [De MTD-app toevoegen aan niet-ingeschreven apparaten](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Beveiligingsbeleid voor Mobile Threat Defense-apps maken](../protect/mtd-app-protection-policy.md)
  - [De MTD-connector in Intune inschakelen voor uitgeschreven apparaten](../protect/mtd-enable-unenrolled-devices.md)
  
## <a name="sample-scenarios"></a>Voorbeeldscenario's

Zie onderstaande scenario's bij het integreren van Zimperium met Intune:

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Toegangsbeheer op basis van bedreigingen van schadelijke apps

Als er op apparaten schadelijke apps zoals malware worden gedetecteerd, kunt u apparaten blokkeren totdat de bedreiging is opgelost:

- Verbinding met bedrijfs-e-mail

- Synchronisatie van bedrijfsbestanden met de app OneDrive voor werk

- Toegang tot bedrijfs-apps

*Blokkeren wanneer er schadelijke apps zijn gedetecteerd:*

> [!div class="mx-imgBorder"]
> ![Conceptafbeelding van detectie van schadelijke apps](./media/zimperium-mobile-threat-defense-connector/Maliciousapps-blocked-zimperium.png)

*Toegang na herstel:*

> [!div class="mx-imgBorder"]
> ![Conceptafbeelding van verleende toegang na herstel](./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png)

### <a name="control-access-based-on-threat-to-network"></a>Toegangsbeheer op basis van bedreigingen voor het netwerk

Detecteer bedreigingen zoals **man-in-the-middle**-aanvallen in het netwerk en beveilig de toegang tot Wi-Fi-netwerken op basis van het apparaatrisico.

*Netwerktoegang via Wi-Fi blokkeren:*

> [!div class="mx-imgBorder"]
> ![Netwerktoegang via Wi-Fi blokkeren](./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png)

*Toegang na herstel:*

> [!div class="mx-imgBorder"]
> ![Toegang na herstel](./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Toegangsbeheer voor SharePoint Online op basis van bedreigingen voor het netwerk

Detecteer bedreigingen zoals **man-in-the-middle**-aanvallen in het netwerk en voorkom synchronisatie van bedrijfsbestanden op basis van het apparaatrisico.

*SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd:*

> [!div class="mx-imgBorder"]
> ![SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd](./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png)

*Toegang na herstel:*

> [!div class="mx-imgBorder"]
> ![Voorbeeld waarin na herstel toegang is verleend aan Sharepoint](./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Toegangsbeheer voor uitgeschreven apparaten op basis van bedreigingen van schadelijke apps

Wanneer de MTD-oplossing (Mobile Threat Defense) van Zimperium een apparaat als geïnfecteerd beschouwt:

> [!div class="mx-imgBorder"]
> ![App-beveiligingsbeleid blokkeert vanwege gedetecteerde malware](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png)

Toegang wordt verleend na herstel:

> [!div class="mx-imgBorder"]
> ![Er wordt toegang verleend na herstel voor App-beveiligingsbeleid](./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Volgende stappen

- [Zimperium integreren met Intune](zimperium-mtd-connector-integration.md)

- [Zimperium-apps instellen](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Een nalevingsbeleid voor Zimperium-apparaten maken](mtd-device-compliance-policy-create.md)

- [Zimperium MTD-connector inschakelen](mtd-connector-enable.md)

- [Een beveiligingsbeleid voor MTD-apps maken](../protect/mtd-app-protection-policy.md)
