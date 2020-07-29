---
title: Problemen met Exchange Connector oplossen
titleSuffix: Microsoft Intune
description: Problemen met betrekking tot de Intune on-premises Exchange-connector oplossen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e7f9c984b81bbe98269b0123371d8097d960ffb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462130"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Problemen met Intune Exchange Connector oplossen

In dit artikel wordt beschreven hoe u problemen met betrekking tot de Intune Exchange-connector kunt oplossen.

> [!IMPORTANT]
>
> Vanaf juli 2020 wordt de ondersteuning voor de Exchange connector afgeschaft en vervangen door Exchange [HMA](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (Hybrid Modern Authentication, hybride moderne verificatie) en de mogelijkheid om een Exchange-connector toe te voegen aan Intune wordt verwijderd.
>
> Klanten die eerder de Exchange-connector hebben geconfigureerd en deze gebruiken, hebben nog steeds de ondersteuning voor de connector.


## <a name="before-you-start"></a>Voordat u begint

Voordat u begint met het oplossen van problemen met Exchange-connector in Intune, moet u enkele basisgegevens verzamelen, zodat u aan de slag gaat met een solide basis. Deze aanpak kan u helpen de aard van het probleem beter te begrijpen en het sneller te verhelpen.

- Controleer of het proces voldoet aan de installatievereisten. Zie [De on-premises Intune Exchange Connector instellen](exchange-connector-install.md).
- Controleer of uw account zowel Exchange- als Intune-beheerdersmachtigingen heeft.
- Let op de tekst van het volledige en exacte foutbericht, de details en waar het bericht wordt weergegeven.
- Stel vast wanneer het probleem is begonnen: 
  - Stelt u de connector voor de eerste keer in? 
  - Werkte de connector goed en daarna niet meer?
  - Welke wijzigingen zijn er aangebracht in de Intune-omgeving, de Exchange-omgeving of op de computer waarop de connectorsoftware wordt uitgevoerd, als deze wel werkte?
- Wat is de MDM-instantie?
- Welke versie van Exchange gebruikt u?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Powershell gebruiken om meer gegevens over problemen met de Exchange Connector te verkrijgen

- Gebruik `Get-ActiveSyncDeviceStatistics -mailbox mbx` om een lijst met alle mobiele apparaten voor een postvak op te halen
- Gebruik `Get-Mailbox -Identity user | select emailaddresses | fl` om een lijst met SMTP-adressen voor een postvak op te halen
- Gebruik `Get-CASMailbox <upn> | fl` om gedetailleerde informatie op te halen over de toegangsstatus van een apparaat

## <a name="review-the-connector-configuration"></a>De connectorconfiguratie controleren

Bekijk de [vereisten voor een on-premises Exchange-connector](exchange-connector-install.md#intune-exchange-connector-requirements) om ervoor te zorgen dat uw omgeving en de connector correct zijn geconfigureerd. 

### <a name="general-considerations-for-the-connector"></a>Algemene overwegingen voor de connector

- Zorg ervoor dat uw firewall en proxyservers communicatie toestaan tussen de server die als host fungeert voor de Intune Exchange-connector en de Intune-service.

- De computer die als host fungeert voor de Intune Exchange-connector en de Exchange-server voor clienttoegang (CAS) moet lid zijn van een domein en met hetzelfde LAN verbonden zijn. Zorg ervoor dat de vereiste machtigingen zijn toegevoegd voor het account dat door de Intune Exchange-connector wordt gebruikt.

- Het meldingsaccount wordt gebruikt om de instellingen voor *Automatisch opsporen* op te halen. Zie [Automatisch opsporen-service in Exchange Server](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016) voor meer informatie over Automatisch opsporen in Exchange.

- De Intune Exchange-connector verzendt met behulp van de referenties van het meldingsaccount een aanvraag naar de EWS-URL voor het verzenden van e-mailberichten met meldingen samen met de koppeling *Aan de slag* (om in te schrijven bij Intune). Het gebruik van de koppeling *Aan de slag* om u in te schrijven is verplicht voor Android-apparaten die niet van Knox zijn. Anders worden deze apparaten geblokkeerd door voorwaardelijke toegang.

### <a name="common-issues-for-connector-configurations"></a>Veelvoorkomende problemen bij connectorconfiguraties

- **Accountmachtigingen**: Zorg ervoor dat u in het dialoogvenster Microsoft Intune Exchange Connector een gebruikersaccount met de juiste machtigingen hebt opgegeven voor het uitvoeren van de [vereiste Windows PowerShell Exchange-cmdlets](exchange-connector-install.md#exchange-cmdlet-requirements).
- **E-mailberichten met meldingen**: Schakel meldingen in en geef een meldingsaccount op.
- **Synchronisatie van de server voor clienttoegang**: Wanneer u de Exchange-connector configureert, geeft u een CAS op met de laagst mogelijke netwerkvertraging naar de server die als host fungeert voor de Exchange-connector. Vertragingen in de communicatie tussen de CAS en de Exchange-connector kunnen leiden tot vertraging bij het detecteren van apparaten, vooral als Exchange Online Dedicated wordt gebruikt.
- **Synchronisatieplanning**: Mogelijk krijgt een gebruiker met een nieuw ingeschreven apparaat pas toegang nadat de Exchange-connector synchroniseert met de Exchange CAS. Een volledige synchronisatie vindt elke dag plaats en een (snelle) deltasynchronisatie vindt meerdere keren per dag plaats. U kunt [een snelle synchronisatie of volledige synchronisatie handmatig forceren](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync) om vertragingen te minimaliseren.

## <a name="next-steps"></a>Volgende stappen
De volgende artikelen kunnen helpen bij het oplossen van veelvoorkomende problemen en specifieke fouten:

- [Algemene problemen voor Intune Exchange Connector oplossen](troubleshoot-exchange-connector-common-problems.md).
- [Algemene fouten voor Intune Exchange Connector oplossen](troubleshoot-exchange-connector-common-errors.md).

Hulp krijgen van het ondersteuningsteam of van de Intune-community:

- Zie [Ondersteuning krijgen](../fundamentals/get-support.md) om de Intune-console te gebruiken voor het oplossen van het probleem of om een ondersteuningscase bij Microsoft te openen. 
- Plaats uw probleem in de [Microsoft Intune fora](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
