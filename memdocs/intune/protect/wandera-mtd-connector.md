---
title: Wandera Mobile Security instellen met Intune
titleSuffix: Intune on Azure
description: Lees hoe u Wandera Mobile Security met Microsoft Intune instelt om de toegang van mobiele apparaten tot uw bedrijfsresources te beheren.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/2/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c0911ff9250fb1b2832df4b7e269f192ee8cda
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057518"
---
# <a name="wandera-mobile-threat-defense-connector-with-intune"></a>Wandera Mobile Threat Defense-connector met Intune  

Beheer de toegang van mobiele apparaten tot zakelijke resources met behulp van voorwaardelijke toegang op basis van een risicoanalyse door Wandera. Wandera is een Mobile Threat Defense-oplossing (MTD) die kan worden geïntegreerd met Microsoft Intune.  Risico's worden beoordeeld op basis van telemetrische gegevens die afkomstig zijn van apparaten die door de Wandera-service zijn verzameld:
- Beveiligingsproblemen voor besturingssystemen
- Schadelijke apps geïnstalleerd
- Schadelijke netwerkprofielen
- Cryptojacking

U kunt beleid voor *voorwaardelijke toegang* configureren dat is gebaseerd op de risicoanalyse van Wandera en dat via Intune-nalevingsbeleid wordt ingeschakeld. Met beleid voor risicoanalyse kunt u apparaten die niet conform zijn op basis van gedetecteerde bedreigingen toegang weigeren tot bedrijfsresources.  

## <a name="how-do-intune-and-wandera-mobile-threat-defense-help-protect-your-company-resources"></a>Hoe kunnen uw bedrijfsresources worden beveiligd met Intune en Wandera Mobile Threat Defense?  

De mobiele app van Wandera wordt met Microsoft Intune moeiteloos geïnstalleerd. De app legt het bestandssysteem, de netwerkstacks en de apparaat- en toepassingstelemetrie vast (indien beschikbaar). Deze informatie wordt gesynchroniseerd met de Wandera-cloudservice om het risico van het apparaat met betrekking tot mobiele bedreigingen te beoordelen. De classificaties van het risiconiveau zijn in de Wandera-console, RADAR, naar wens te configureren.

Het compliancebeleid in Intune omvat een regel voor MTD op basis van de risicobeoordeling van Wandera. Als deze regel is ingeschakeld, controleert Intune of het apparaat voldoet aan het beleid dat u hebt ingeschakeld.

Voor apparaten die niet-compatibel zijn, kan toegang tot resources als Microsoft 365 worden geblokkeerd. Gebruikers van een geblokkeerd apparaat ontvangen richtlijnen van de Wandera-app, zodat ze het probleem kunnen oplossen en weer toegang kunnen krijgen.

Met Wandera wordt Intune bijgewerkt met het meest recente bedreigingsniveau (Beveiligd, Laag, Gemiddeld of Hoog) wanneer het wordt gewijzigd. Dit bedreigingsniveau wordt voortdurend herberekend door de Wandera Security Cloud en is gebaseerd op de status van het apparaat, de netwerkactiviteit en tal van mobiele bedreigingsinformatiefeeds over verschillende bedreigingscategorieën.

Deze categorieën en de bijbehorende bedreigingsniveaus kunnen worden geconfigureerd in de RADAR-console van Wandera, zodat het totale berekende bedreigingsniveau voor elk apparaat kan worden aangepast aan de beveiligingsvereisten van uw organisatie. Aan de hand van het bedreigingsniveau zijn er twee beleidstypen van Intune die deze informatie gebruiken om de toegang tot bedrijfsgegevens te beheren:

* Met behulp van **Apparaatnalevingsbeleid** met voorwaardelijke toegang stellen beheerders beleidsregels in om een beheerd apparaat automatisch te markeren als niet-conform op basis van het door Wandera gerapporteerde bedreigingsniveau. Deze nalevingsvlag stuurt vervolgens beleidsregels voor voorwaardelijke toegang aan om toegang tot toepassingen die moderne verificatie gebruiken toe te staan of te weigeren.  Zie [MTD-nalevingsbeleid (Mobile Threat Defense) voor apparaten maken](../protect/mtd-device-compliance-policy-create.md) met Intune voor configuratiedetails.

* Met behulp van **beleid voor app-beveiliging** met voorwaardelijke toegang kunnen beheerders beleidsregels instellen die worden afgedwongen op het niveau van de systeemeigen app (bijvoorbeeld Android- en iOS-/iPadOS-apps zoals Outlook, OneDrive, enzovoort) op basis van het door Wandera gerapporteerde bedreigingsniveau.  Deze beleidsregels kunnen ook worden gebruikt met niet-beheerde apparaten (MAM-WE) om uniform beleid te bieden voor alle platformen en eigendomsmodi. Zie [App-beveiligingsbeleid voor Mobile Threat Defense maken](../protect/mtd-app-protection-policy.md) met Intune voor configuratiedetails.

## <a name="supported-platforms"></a>Ondersteunde platforms  

De volgende platforms worden door Wandera ondersteund bij inschrijving in Intune:

- Android 5.0 en hoger  
- iOS 10.2 en hoger 

Raadpleeg voor meer informatie over platforms en apparaten de [website van Wandera](https://www.wandera.com/mobile-threat-defense/).

## <a name="prerequisites"></a>Vereisten  

- Microsoft Intune-abonnement  
- Azure Active Directory  
- Wandera Mobile Threat Defense (voorheen Wandera Secure)  

Raadpleeg voor meer informatie [Wandera Mobile Security](https://www.wandera.com/mobile-security/).
 
## <a name="sample-scenarios"></a>Voorbeeldscenario's

Hier vindt u algemene scenario's voor wanneer u Wandera MTD met Intune gebruikt.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Toegangsbeheer op basis van bedreigingen van schadelijke apps  

Als er op een apparaat schadelijke apps (bijvoorbeeld malware) worden gedetecteerd, kunt u de toegang van het apparaat tot veelgebruikte hulpprogramma's blokkeren totdat de bedreiging is geëlimineerd. Veelvoorkomende blokkeringen zijn onder meer:  
- Verbinding met bedrijfs-e-mail  
- Synchronisatie van bedrijfsbestanden met de app OneDrive voor werk  
- Toegang tot bedrijfs-apps  

*Blokkeren wanneer er schadelijke apps zijn gedetecteerd*:

![Conceptafbeelding van detectie van schadelijke apps](./media/wandera-mtd-connector/wandera-malicious-apps-blocked.png)  

*Toegang na herstel*: 

![Conceptafbeelding van verleende toegang na herstel](./media/wandera-mtd-connector/wandera-malicious-apps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Toegangsbeheer op basis van bedreigingen voor het netwerk  

Detecteer bedreigingen voor uw netwerk, zoals man-in-the-middle-aanvallen, en beveilig de toegang tot wifinetwerken op basis van het apparaatrisico.  

*Netwerktoegang via Wi-Fi blokkeren*:  

![Netwerktoegang via Wi-Fi blokkeren](./media/wandera-mtd-connector/wandera-network-wifi-blocked.png)

*Toegang na herstel*:  

![Toegang na herstel](./media/wandera-mtd-connector/wandera-network-wifi-unblocked.png)  

## <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Toegangsbeheer voor SharePoint Online op basis van bedreigingen voor het netwerk

Bedreigingen voor uw netwerk worden gedetecteerd, zoals man-in-the-middle-aanvallen, en synchronisatie van bedrijfsbestanden wordt voorkomen op basis van het apparaatrisico.

*SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd*:  

![SharePoint Online blokkeren wanneer netwerkbedreigingen worden gedetecteerd](./media/wandera-mtd-connector/wandera-network-spo-blocked.png)  

*Toegang na herstel*:  

![Voorbeeld waarin na herstel toegang is verleend aan SharePoint](./media/wandera-mtd-connector/wandera-network-spo-unblocked.png)  

### <a name="control-access-on-unenrolled-devices-based-on-threats-from-malicious-apps"></a>Toegangsbeheer voor uitgeschreven apparaten op basis van bedreigingen van schadelijke apps

Wanneer de oplossing Wandera Mobile Threat Defense een apparaat als geïnfecteerd beschouwt:

![App-beveiligingsbeleid wordt geblokkeerd vanwege gedetecteerde malware](./media/wandera-mtd-connector/wandera-mobile-app-policy-block.png)

Toegang wordt verleend na herstel:

![Er wordt toegang verleend na herstel voor App-beveiligingsbeleid](./media/wandera-mtd-connector/wandera-mobile-app-policy-remediated.png)

## <a name="next-steps"></a>Volgende stappen

- [Wandera integreren met Intune](wandera-mtd-connector-integration.md)
- [Wandera-apps instellen](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Wandera-nalevingsbeleid voor apparaten maken](mtd-device-compliance-policy-create.md)
- [Wandera MTD-connector inschakelen](mtd-connector-enable.md)
