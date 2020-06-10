---
title: Lookout Mobile Endpoint integreren met Microsoft Intune
titleSuffix: Microsoft Intune
description: Meer informatie over de integratie van Intune met Lookout Mobile Threat Defense (MTD) om toegang tot uw bedrijfsbronnen met mobiele apparaten te bepalen.
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
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788
ms.reviewer: davera
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1083e195cee20c3df9572db94395d462f9531a39
ms.sourcegitcommit: 42a4a4454e56fa681f0ad39f5e585492dfbad286
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330947"
---
# <a name="lookout-mobile-endpoint-security-connector-with-intune"></a>Lookout Mobile Endpoint Security-connector met Intune

U kunt de toegang van mobiele apparaten tot bedrijfsresources beheren op basis van een risicoanalyse die door Lookout wordt uitgevoerd. Lookout is een Mobile Threat Defense-oplossing die met Microsoft Intune is geïntegreerd. Risico's worden beoordeeld op basis van telemetrische gegevens afkomstig van apparaten die door Lookout-service zijn verzameld:
- Beveiligingsproblemen voor besturingssystemen
- Schadelijke apps geïnstalleerd
- Schadelijke netwerkprofielen

U kunt beleidsregels voor voorwaardelijke toegang configureren op basis van de risicoanalyse van Lookout die via het Intune-nalevingsbeleid voor ingeschreven apparaten wordt ingeschakeld. U kunt met dit beleid de toegang tot bedrijfsresources voor niet-conforme apparaten toestaan of blokkeren op basis van de gedetecteerde bedreigingen. Voor niet-ingeschreven apparaten kunt u app-beveiligingsbeleid gebruiken om het blokkeren of selectief wissen af te dwingen op basis van gedetecteerde bedreigingen.

## <a name="how-do-intune-and-lookout-mobile-endpoint-security-help-protect-company-resources"></a>Hoe kunnen bedrijfsresources worden beveiligd met Intune en Lookout Mobile Endpoint Security?

De mobiele app van Lookout, **Lookout for Work**, wordt geïnstalleerd en uitgevoerd op mobiele apparaten. Deze app legt telemetrische gegevens vast over het bestandssysteem, de netwerkstack, apparaten en apps waar dergelijke gegevens beschikbaar zijn, en verzendt die gegevens naar de Lookout-cloudservice om te bepalen welke risico's het apparaat loopt met mobiele bedreigingen. U kunt de classificaties van het risiconiveau voor bedreigingen in de Lookout-console wijzigen op basis van uw vereisten.

- **Ondersteuning voor ingeschreven apparaten**: nalevingsbeleid voor Intune-apparaatcompatibiliteit bevat een regel voor de beveiliging van mobiele bedreigingen (MTD), die informatie over risicobeoordeling kan gebruiken van Lookout for Work. Als de MTD-regel is ingeschakeld, controleert Intune of het apparaat voldoet aan het beleid dat u hebt ingeschakeld. Als het apparaat niet aan het beleid blijkt te voldoen, wordt de toegang van gebruikers tot resources als Exchange Online en SharePoint Online geblokkeerd. Gebruikers ontvangen ook richtlijnen van de Lookout for Work-app die op hun apparaat is geïnstalleerd, zodat ze het probleem kunnen oplossen en weer toegang kunnen krijgen tot bedrijfsresources. Ondersteuning bieden met Lookout for Work met ingeschreven apparaten:
  - [MTD-apps aan apparaten toevoegen](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Nalevingsbeleid voor apparaten maken dat MTD ondersteunt](../protect/mtd-device-compliance-policy-create.md)
  - [De MTD-connector in Intune inschakelen](../protect/mtd-connector-enable.md)

- **Ondersteuning voor uitgeschreven apparaten**: Intune kan de gegevens van de risicoanalyse van de Lookout for Work-app gebruiken voor uitgeschreven apparaten wanneer u beveiligingsbeleidsregels voor Intune-apps gebruikt. Beheerders kunnen deze combinatie gebruiken om bedrijfsgegevens te beschermen binnen een [met Microsoft Intune beveiligde app](../apps/apps-supported-intune-apps.md). Beheerders kunnen bedrijfsgegevens op deze ingeschreven apparaten ook blokkeren of selectief wissen. Ondersteuning bieden Lookout for Work met niet-ingeschreven apparaten:
  - [De MTD-app toevoegen aan niet-ingeschreven apparaten](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Beveiligingsbeleid voor Mobile Threat Defense-apps maken](../protect/mtd-app-protection-policy.md)
  - [De MTD-connector in Intune inschakelen voor niet-ingeschreven apparaten](../protect/mtd-enable-unenrolled-devices.md)

## <a name="supported-platforms"></a>Ondersteunde platforms

De volgende platformen worden ondersteund door Lookout wanneer deze geregistreerd zijn in Intune:

- **Android 4.1 en hoger**  
- **iOS 8 en hoger**  

Meer informatie over ondersteunde platformen en talen kunt u vinden op de [website van Lookout](https://personal.support.lookout.com/hc/articles/114094140253).  

## <a name="prerequisites"></a>Vereisten

- Enterprise-abonnement op Lookout Mobile EndPoint Security  
- Microsoft Intune-abonnement
- Azure Active Directory Premium
- EMS (Enterprise Mobility en Security) E3 of E5, met aan gebruikers toegewezen licenties.  

Zie [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security) voor meer informatie

## <a name="sample-scenarios"></a>Voorbeeldscenario's

Hier vindt u veelvoorkomende scenario's als u Mobile Endpoint Security met Intune gebruikt.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Toegangsbeheer op basis van bedreigingen van schadelijke apps

Als er op apparaten schadelijke apps zoals malware worden gedetecteerd, kunt u apparaten blokkeren tegen zaken als de volgende totdat de bedreiging is opgelost:

- Verbinding met bedrijfs-e-mail
- Synchronisatie van bedrijfsbestanden met de app OneDrive voor werk
- Toegang tot bedrijfs-apps

*Blokkeren wanneer er schadelijke apps zijn gedetecteerd:*

> [!div class="mx-imgBorder"]
> ![Conceptafbeelding van beleidsmatig geblokkeerde toegang vanwege schadelijke apps](./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png)

*Toegang na herstel:*

> [!div class="mx-imgBorder"]
> ![Conceptafbeelding van verleende toegang tot apparaten na herstel](./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Toegangsbeheer op basis van bedreigingen voor het netwerk

Bedreigingen voor uw netwerk worden gedetecteerd, zoals man-in-the-middle-aanvallen, en de toegang tot Wi-Fi-netwerken wordt beveiligd op basis van apparaatrisico.

*Netwerktoegang via Wi-Fi blokkeren:*

> [!div class="mx-imgBorder"]
> ![Afbeelding met blokkering van Wi-Fi-toegang op basis van netwerkbedreigingen](./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png)

*Toegang na herstel:*

> [!div class="mx-imgBorder"]
> ![Conceptafbeelding van voorwaardelijke toegang voor toegang na herstel](./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Toegangsbeheer voor SharePoint Online op basis van bedreigingen voor het netwerk

Bedreigingen voor uw netwerk worden gedetecteerd, zoals man-in-the-middle-aanvallen, en synchronisatie van bedrijfsbestanden wordt voorkomen op basis van het apparaatrisico.

*SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd:*

> [!div class="mx-imgBorder"]
> ![Conceptafbeelding van blokkering van toegang tot SharePoint Online](./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png)

*Toegang na herstel:*

> [!div class="mx-imgBorder"]
> ![Conceptafbeelding die laat zien hoe de toegang na verwijdering van de netwerkbedreiging wordt verleend met voorwaardelijke toegang](./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png)

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Toegangsbeheer voor uitgeschreven apparaten op basis van bedreigingen van schadelijke apps

Wanneer de Lookout Mobile Threat Defense-oplossing een apparaat beschouwt als geïnfecteerd:
> [!div class="mx-imgBorder"]
> ![App-beveiligingsbeleid blokkeert vanwege gedetecteerde malware](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png)

Toegang wordt verleend na herstel:

> [!div class="mx-imgBorder"]
> ![Er wordt toegang verleend na herstel voor App-beveiligingsbeleid](./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png)

## <a name="next-steps"></a>Volgende stappen

Hier volgen de belangrijkste stappen voor het implementeren van deze oplossing:

- [De integratie van Lookout instellen](lookout-mtd-connector-integration.md)
- [Mobile Endpoint Security in Intune inschakelen](mtd-connector-enable.md)
- [De Lookout for Work-app toevoegen en toewijzen](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Het nalevingsbeleid voor Lookout-apparaten configureren](mtd-device-compliance-policy-create.md)
- [Een beveiligingsbeleid voor MTD-apps maken](mtd-app-protection-policy.md)
