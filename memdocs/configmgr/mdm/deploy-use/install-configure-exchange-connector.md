---
title: De Exchange-connector installeren
titleSuffix: Configuration Manager
description: Installeer en configureer de Exchange connector voor Configuration Manager voor het beheren van mobiele apparaten via ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0db550369ca2d81f42a25e68960b5f8f27be168
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700477"
---
# <a name="install-and-configure-the-exchange-connector"></a>De Exchange-connector installeren en configureren

*Van toepassing op: Configuration Manager (huidige vertakking)*

Gebruik deze procedure voor het installeren en configureren van een Exchange Server-connector voor het beheren van mobiele apparaten. Configuration Manager ondersteunt slechts één connector binnen een Exchange-organisatie.

Voordat u de Exchange Server-connector voor Configuration Manager installeert, moet u ervoor zorgen dat u de vereiste machtigingen en versies hebt. Zie [Apparaatbeheer met Exchange en Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites)voor meer informatie.

## <a name="exchange-connection-account"></a>Exchange-verbindings account

Besluit welk account u wilt verbinden met de Exchange Client Access-server om mobiele apparaten te beheren. Het account kan een computeraccount van de siteserver zijn of een Windows-gebruikersaccount.

Configureer dit account vervolgens in een Exchange-functie groep om de volgende Exchange Server-cmdlets uit te voeren:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Get-Mailbox**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Get-gebruiker**  

- **Set-ActiveSyncOrganizationSettings**  

De volgende Exchange Server-beheer rollen bevatten deze cmdlets:

- Ontvangers beheer
- Alleen-lezen organisatie beheer
- Server Management

Zie [Management Role groups](/exchange/understanding-management-role-groups-exchange-2013-help) in de Exchange Server 2013-documentatie voor meer informatie.

> [!TIP]  
> Als u de Exchange Server-connector probeert te installeren of gebruiken zonder de vereiste cmdlets, ziet u de volgende fout code in het bestand bestand easdisc. log op de site Server computer: `Invoking cmdlet <cmdlet> failed` .

## <a name="install-the-connector"></a>De connector installeren

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **hiërarchie configuratie**uit en selecteer vervolgens **Exchange Server-connectors**.

1. Klik op het tabblad **Start** van het lint in de groep **maken** op **Exchange server toevoegen**.

1. Selecteer op de pagina **Algemeen** van de wizard Exchange server toevoegen een van de Exchange Server-omgevingen:

    - **On-premises Exchange Server**: Geef één server of een server matrix voor client toegang op voor elke Active Directory-site.

        Als de server of matrix offline is, probeert Configuration Manager een server voor client toegang te detecteren die u wilt gebruiken. Als dat niet lukt, Configuration Manager terugvallen op het gebruik van een postvak server om verbinding te maken met een server voor client toegang. Wanneer de verbinding opnieuw probeert te worden uitgevoerd, worden de volgende waarschuwingen in het bestand bestand easdisc. log op de site Server computer geregistreerd: `Failed to open runspace for site <site_name>` .

    - **Gehoste Exchange-Server**: Geef het server adres op van uw Exchange Online-omgeving.

    Selecteer vervolgens de primaire site om de Exchange Server-connector uit te voeren.

1. Geef op de pagina **account** het account op waarmee verbinding wordt gemaakt met de Exchange-Server. Zie [Exchange Connection account](#exchange-connection-account)(Engelstalig) voor meer informatie.

1. Configureer de synchronisatie planning en-regels voor het zoeken naar apparaten op de pagina **detectie** .

1. Configureer op de pagina **instellingen** de instellingen voor mobiele apparaten in de volgende groepen:

    - **Algemeen**
    - **Wachtwoord**
    - **E-mail beheer**
    - **Beveiliging**
    - **Toepassing**

    Zie [Exchange connector-instellingen](manage-mobile-devices-with-exchange-activesync.md#policies)voor meer informatie.

    Als u ook mobiele apparaten registreert met behulp van Configuration Manager [on-premises MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md), schakelt u de optie in om **externe Mobile Device Management toe te staan**. Met deze instelling kunnen deze mobiele apparaten e-mail blijven ontvangen van Exchange nadat Configuration Manager ze heeft inge schreven.

1. Voltooi de wizard.

## <a name="verify-and-monitor"></a>Controleren en controleren

Controleer de installatie van de Exchange Server-connector met status berichten en logboek bestanden:

- Bevestig dat Site Component Manager de Exchange Server-connector correct hebt geïnstalleerd. Zoek naar de bericht status ID **1015** van het onderdeel **SMS_EXCHANGE_CONNECTOR** .

    De installatie kan mislukken als de opgegeven server voor client toegang offline is. Als Configuration Manager de connector niet goed kunt installeren, Configuration Manager wordt de installatie elke 60 minuten opnieuw geprobeerd. U kunt het opnieuw proberen totdat de installatie is geslaagd of u de Exchange Server-connector verwijdert.

- Controleer **SiteComp. log** op de site Server computer voor de volgende vermelding: `Component SMS_EXCHANGE_CONNECTOR flagged for installation` . Vervolgens wordt de geslaagde installatie geregistreerd met de volgende tekst: `STATMSG: ID=1015` .

Nadat u de installatie hebt voltooid, controleert u de mobiele apparaten die worden gevonden en beheerd door de connector. Bekijk de verzamelingen met mobiele apparaten en gebruik de rapporten voor mobiele apparaten.

> [!NOTE]  
> Configuration Manager genereert namen voor de mobiele apparaten die worden gevonden. Het maakt gebruik van de notatie *gebruikers naam*_*Apparaattype*. Bijvoorbeeld **jdoe_WindowsPhone**. Als een gebruiker meer dan één mobiel apparaat heeft dat hetzelfde type apparaat heeft, geeft Configuration Manager dezelfde naam weer voor deze mobiele apparaten in de-console en in rapporten.  

## <a name="see-also"></a>Zie ook

- [Poorten die worden gebruikt door Configuration-clients en site systemen](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Proxyserverondersteuning](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Beveiligings aanbevelingen voor mobiele apparaten](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Privacy-informatie voor mobiele apparaten die worden beheerd met de Exchange Server-connector](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)