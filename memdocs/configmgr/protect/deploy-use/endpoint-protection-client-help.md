---
title: Help bij Endpoint Protection-client
titleSuffix: Configuration Manager
description: Meer informatie over functies en verbeteringen in Endpoint Protection waarmee u uw computer beter kunt beschermen tegen bedreigingen.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eba7de1705212bb5cb329282bc407317995b82f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724340"
---
# <a name="endpoint-protection-client-help"></a>Help bij Endpoint Protection-client

*Van toepassing op: Configuration Manager (huidige vertakking)*


Deze versie van Windows Defender of Endpoint Protection bevat de volgende functies om uw computer te beschermen tegen bedreigingen:  

-   **Integratie van Windows Firewall.** Tijdens de setup van Endpoint Protection kunt u Windows Firewall in- of uitschakelen.  
-   **netwerkinspectiesysteem.** Deze functie verhoogt de real-timebeveiliging door netwerkverkeer te inspecteren om proactief te voorkomen dat misbruik wordt gemaakt van bekende beveiligingslekken in het netwerk.  
-   **Beveiligings engine.** Met realtime-beveiliging wordt het installeren of uitvoeren van malware op uw PC gedetecteerd en gestopt. De bijgewerkte engine biedt verbeterde detectie en opschoningsmogelijkheden met betere prestaties.  

Windows Defender wordt geleverd als onderdeel van het Windows 10-besturings systeem.  In eerdere versies van Windows kan uw beheerder Windows Defender of Endpoint Protection bieden met behulp van beheer software.

U kunt ook een lijst met [Veelgestelde vragen over Windows Defender en Endpoint Protection](endpoint-protection-client-faq.md)vinden. Zie [problemen met Windows Defender of Endpoint Protection client oplossen](troubleshoot-endpoint-client.md)voor meer informatie over het oplossen van problemen. Zie [what's New Windows Defender client](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender)(Engelstalig) voor een lijst met nieuwe functies.

## <a name="windows-firewall-integration"></a>Windows Firewall-integratie  
 Windows Firewall voorkomt dat aanvallers of schadelijke software toegang krijgen tot uw computer via internet of een netwerk. Wanneer u nu Endpoint Protection installeert, controleert de installatiewizard of Windows Firewall is ingeschakeld. Als u Windows Firewall met opzet hebt uitgeschakeld, kunt u voorkomen dat deze wordt ingeschakeld door een selectievakje te wissen. U kunt de Windows Firewall-instellingen op elk gewenst moment wijzigen via Systeem en beveiligingsinstellingen in het Configuratiescherm.  

## <a name="network-inspection-system"></a>Netwerkinspectiesysteem  
 Aanvallers voeren steeds vaker aanvallen via het netwerk uit op basis van blootgestelde beveiligingslekken voordat softwareleveranciers beveiligingsupdates kunnen ontwikkelen en distribueren. Onderzoek naar beveiligingslekken toont aan dat het een maand of langer kan duren vanaf de eerste melding van een aanval voordat een geschikte beveiligingsupdate is ontwikkeld, getest en vrijgegeven. Door dit gat in de beveiliging zijn veel computers gedurende lange tijd kwetsbaar voor aanvallen en misbruik. Netwerkinspectiesysteem werkt met real-timebeveiliging om u beter te beschermen tegen aanvallen vanuit het netwerk door de tijd tussen de detectie van een beveiligingslek en de implementatie van een update fors te verkorten van weken tot enkele uren.  

## <a name="award-winning-protection-engine"></a>Bekroonde beschermingsengine  
 Onder de schermen van Windows Defender of Endpoint Protection is de bekroonde beschermings engine die regel matig wordt bijgewerkt. De engine wordt ondersteund door een team van onderzoekers naar schadelijke software van het Microsoft Malware Protection Center, dat 24 uur per dag reageert op de nieuwste bedreigingen van schadelijke software.  

## <a name="windows-defender-settings"></a>Windows Defender-instellingen
Met Windows Defender-instellingen kunt u instellingen inschakelen waarmee uw PC wordt beschermd tegen schadelijke software. De beheerder kan sommige Windows Defender-instellingen voor u beheren. U kunt anderen beheren met de instellingen van Windows Defender. U wordt aangeraden Windows Defender-instellingen in te scha kelen om uw PC en gegevens te beveiligen.

Als u de Windows Defender-instellingen wilt `Windows Defender` weer geven, zoekt u op uw PC. Open **Windows Defender** en selecteer **instellingen**. Windows Defender-instellingen omvatten:
- **Realtime-beveiliging** -schadelijke software kan niet worden geïnstalleerd of uitgevoerd op uw PC.
- **Cloud beveiliging** : Windows Defender stuurt informatie over potentiële beveiligings Risico's naar micro soft.
- **Automatische verzen ding** van voor beelden: toestaan dat Windows Defender voor beelden van verdachte bestanden naar micro soft verzendt om detectie van malware te helpen verbeteren.
- **Uitsluitingen** : u kunt specifieke bestanden, mappen, bestands extensies of processen van Windows Defender Scanning uitsluiten.
- **Uitgebreide melding** : Hiermee worden meldingen met informatie over de status van uw PC. U **ontvangt** zelfs essentiële meldingen.
- **Windows Defender offline** : u kunt Windows Defender offline uitvoeren om schadelijke software te vinden en te verwijderen. Met deze scan wordt uw PC opnieuw opgestart en duurt ongeveer 15 minuten.

### <a name="see-also"></a>Zie ook  
 [Veelgestelde vragen over Endpoint Protection-client](endpoint-protection-client-faq.md)   
 [Problemen met Windows Defender of Endpoint Protection-client oplossen](troubleshoot-endpoint-client.md)
