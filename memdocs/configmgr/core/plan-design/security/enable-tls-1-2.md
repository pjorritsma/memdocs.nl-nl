---
title: Overzicht van het inschakelen van Transport Layer Security (TLS) 1,2
titleSuffix: Configuration Manager
description: Overzicht van het inschakelen van TLS 1,2 voor Configuration Manager.
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e1334603bcf60ea3eb8c3d18b73d511570cdc5d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699735"
---
# <a name="how-to-enable-tls-12"></a>TLS 1,2 inschakelen

*Van toepassing op: Configuration Manager (Current Branch)*

Transport Layer Security (TLS), zoals Secure Sockets Layer (SSL), is een versleutelings protocol dat is bedoeld om gegevens veilig te houden wanneer ze via een netwerk worden overgedragen. In deze artikelen worden de stappen beschreven die u moet uitvoeren om ervoor te zorgen dat Configuration Manager beveiligde communicatie gebruikmaakt van het TLS 1,2-protocol. In deze artikelen worden ook de update vereisten beschreven voor veelgebruikte onderdelen en voor het oplossen van veelvoorkomende problemen.

## <a name="enabling-tls-12"></a>TLS 1.2 inschakelen

Configuration Manager is afhankelijk van een aantal verschillende onderdelen voor beveiligde communicatie. Het protocol dat wordt gebruikt voor een bepaalde verbinding, is afhankelijk van de mogelijkheden van de relevante onderdelen op de client-en server zijde. Als een onderdeel verouderd is of niet juist is geconfigureerd, kan de communicatie gebruikmaken van een ouder, minder beveiligd protocol. Als u Configuration Manager wilt inschakelen voor de ondersteuning van TLS 1,2 voor alle beveiligde communicatie, moet u TLS 1,2 inschakelen voor alle vereiste onderdelen. De vereiste onderdelen zijn afhankelijk van uw omgeving en de Configuration Manager functies die u gebruikt.

> [!IMPORTANT]
> Start dit proces met de-clients, met name vorige versies van Windows. Alvorens TLS 1,2 in te scha kelen en de oudere protocollen op de Configuration Manager-servers uit te scha kelen, moet u ervoor zorgen dat alle clients TLS 1,2 ondersteunen. Anders kunnen de clients niet communiceren met de servers en kan deze zwevend worden.


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Taken voor Configuration Manager-clients, site servers en externe site systemen

Als u TLS 1,2 wilt inschakelen voor onderdelen waarvan Configuration Manager afhankelijk is voor beveiligde communicatie, moet u meerdere taken uitvoeren op de clients en de site servers.

### <a name="enable-tls-12-for-configuration-manager-clients"></a>TLS 1,2 inschakelen voor Configuration Manager-clients

- [Windows en WinHTTP bijwerken op Windows 8,0, Windows Server 2012 (niet-R2) en eerdere versies](enable-tls-1-2-client.md#bkmk_winhttp)
- [Zorg ervoor dat TLS 1,2 is ingeschakeld als een protocol voor SChannel op het niveau van het besturings systeem](enable-tls-1-2-client.md#bkmk_protocol)
- [De .NET Framework bijwerken en configureren ter ondersteuning van TLS 1,2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>Schakel TLS 1,2 in voor Configuration Manager site servers en externe site systemen

- [Zorg ervoor dat TLS 1,2 is ingeschakeld als een protocol voor SChannel op het niveau van het besturings systeem](enable-tls-1-2-server.md#bkmk_protocol)
- [De .NET Framework bijwerken en configureren ter ondersteuning van TLS 1,2](enable-tls-1-2-server.md#bkmk_net)
- [SQL Server en de SQL Native Client bijwerken](enable-tls-1-2-server.md#bkmk_sql)
- [Windows Server Update Services bijwerken (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>Onderdelen en scenario afhankelijkheden

In deze sectie worden de afhankelijkheden voor specifieke functies en scenario's van Configuration Manager beschreven. Zoek de items die van toepassing zijn op uw omgeving om de volgende stappen te bepalen.

|Functie of scenario|Taken bijwerken|
|--- |--- |
|Site servers (centraal, primair of secundair)| - [.NET Framework bijwerken](enable-tls-1-2-server.md#bkmk_net)<br/> -Sterke crypto grafie-instellingen verifiëren|
|Sitedatabaseserver|[SQL Server en de bijbehorende client onderdelen bijwerken](enable-tls-1-2-server.md#bkmk_sql)|
|Secundaire site servers|[SQL Server en de bijbehorende client onderdelen bijwerken](enable-tls-1-2-server.md#bkmk_sql) naar een compatibele versie van SQL Express|
|Sitesysteemrollen| - [.NET Framework bijwerken](enable-tls-1-2-server.md#bkmk_net) en sterke crypto grafie-instellingen verifiëren <br/> - [Update SQL Server en de bijbehorende client onderdelen](enable-tls-1-2-server.md#bkmk_sql) op rollen waarvoor deze nodig is, inclusief de [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client)|
|Reporting Services-punt|- [.NET Framework](enable-tls-1-2-server.md#bkmk_net) op de site server, de SQL Reporting Services-servers en elke computer met de console bijwerken<br/> -De SMS_Executive-service indien nodig opnieuw opstarten|
|Software-updatepunt|[WSUS bijwerken](enable-tls-1-2-server.md#bkmk_wsus)|
|Cloudbeheergateway|[Enforce TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Configuration Manager-console| - [.NET Framework bijwerken](enable-tls-1-2-client.md#bkmk_net)<br/> -Sterke crypto grafie-instellingen verifiëren|
|Configuration Manager-client met HTTPS-site systeem rollen|[Windows bijwerken om TLS 1,2 voor client-server communicatie te ondersteunen met behulp van WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)|
|Software Center| - [.NET Framework bijwerken](enable-tls-1-2-client.md#bkmk_net)<br/> -Sterke crypto grafie-instellingen verifiëren|
|Windows 7-clients| *Voordat* u TLS 1,2 op Server onderdelen inschakelt, [moet u Windows bijwerken om TLS 1,2 voor client-server communicatie te ondersteunen met behulp van WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp). Als u TLS 1,2 op Server onderdelen eerst inschakelt, kunt u eerdere versies van clients zweven.|

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="why-use-tls-12-with-configuration-manager"></a>Waarom TLS 1,2 gebruiken met Configuration Manager?

TLS 1,2 is veiliger dan de vorige cryptografische protocollen, zoals SSL 2,0, SSL 3,0, TLS 1,0 en TLS 1,1. In feite blijven TLS 1,2 gegevens veilig over het netwerk verzonden.

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Waar Configuration Manager het gebruik van versleutelings protocollen zoals TLS 1,2?

Er zijn in feite vijf gebieden die Configuration Manager gebruikmaken van versleutelings protocollen zoals TLS 1,2:

- Client communicatie met Site Server functies op basis van IIS wanneer de rol is geconfigureerd voor het gebruik van HTTPS. Voor beelden van deze rollen zijn onder andere distributie punten, software-update punten en beheer punten.
- Communicatie met beheer punt, SMS Executive en SMS-provider met SQL. Configuration Manager versleutelt altijd SQL-communicatie.
- Communicatie van de site server naar WSUS als WSUS is geconfigureerd voor het gebruik van HTTPS.
- De Configuration Manager-console naar SQL Reporting Services (SSRS) als SSRS is geconfigureerd voor het gebruik van HTTPS.
- Alle verbindingen met op internet gebaseerde services. Voor beelden zijn de Cloud beheer gateway (CMG), de synchronisatie van het service aansluitpunt en de synchronisatie van meta gegevens van de update van Microsoft Update.

### <a name="what-determines-which-encryption-protocol-is-used"></a>Wat bepaalt welk versleutelings protocol wordt gebruikt?

HTTPS zal altijd onderhandelen over de hoogste Protocol versie die door zowel de client als de server wordt ondersteund in een versleutelde conversatie. Wanneer een verbinding tot stand is gebracht, verzendt de client een bericht naar de server met het hoogste beschik bare protocol. Als de server dezelfde versie ondersteunt, verzendt het een bericht met deze versie. Deze onderhandelde versie is het nummer dat wordt gebruikt voor de verbinding. Als de-server de versie die door de client wordt gepresenteerd niet ondersteunt, geeft het server bericht de hoogste versie op die kan worden gebruikt. Zie [een beveiligde sessie tot stand brengen met behulp van TLS](/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls)voor meer informatie over het TLS-hand Shake protocol.

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>Wat bepaalt welke Protocol versie door de client en server kan worden gebruikt?

Over het algemeen kunnen de volgende items bepalen welke Protocol versie wordt gebruikt:

- De toepassing kan bepalen welke specifieke protocol versies moeten worden onderhandeld.
  - Aanbevolen procedures om te voor komen dat specifieke protocol versies op toepassings niveau worden vastgelegd en om de configuratie te volgen die is gedefinieerd op het niveau van het onderdeel en het besturings systeem.
  - Configuration Manager volgt deze best practice.
- Voor toepassingen die zijn geschreven met behulp van de .NET Framework, is de standaard protocol versie afhankelijk van de versie van het Framework waarop ze zijn gebaseerd.  
  - .NET-versies vóór 4.6.3 waren TLS 1,1 en 1,2 in de lijst met protocollen voor onderhandeling standaard niet inbegrepen.
- Toepassingen die gebruikmaken van WinHTTP voor HTTPS-communicatie, zoals de Configuration Manager-client, zijn afhankelijk van de versie van het besturings systeem, het patch niveau en de configuratie voor Protocol versie ondersteuning.


## <a name="additional-resources"></a>Aanvullende bronnen

- [Technische naslaginformatie voor cryptografische besturingselementen](cryptographic-controls-technical-reference.md)
- [Aanbevolen procedures voor trans port Layer Security (TLS) met de .NET Framework](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244: TLS 1,2-ondersteuning voor Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>Volgende stappen

- [TLS 1.2 inschakelen op clients](enable-tls-1-2-client.md)
- [TLS 1,2 inschakelen op de site servers](enable-tls-1-2-server.md)