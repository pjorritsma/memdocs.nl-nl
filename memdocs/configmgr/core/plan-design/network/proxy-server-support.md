---
title: Proxyserverondersteuning
titleSuffix: Configuration Manager
description: Meer informatie over hoe Configuration Manager-site systeem servers proxy servers gebruiken.
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 89a2f76f394d3bdf8fd6785429ae0ae60302537a
ms.sourcegitcommit: 14d7dd0a99ebd526c9274d5781c298c828323ebf
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/05/2020
ms.locfileid: "82802086"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Ondersteuning van proxy server in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Sommige Configuration Manager-site systeem servers hebben verbindingen met internet nodig. Als uw omgeving Internet verkeer vereist voor het gebruik van een proxy server, configureert u deze site systeem rollen om de proxy te gebruiken.  

- Een computer die als host fungeert voor een site systeem server ondersteunt één configuratie van een proxy server. Alle site systeem rollen op die computer delen dezelfde proxy configuratie. Als u afzonderlijke proxy servers nodig hebt voor verschillende rollen of instanties van een rol, plaatst u deze rollen op afzonderlijke site systeem servers.  

- Wanneer u nieuwe proxyserver instellingen configureert voor een site systeem server die al een proxyserver configuratie heeft, wordt de oorspronkelijke configuratie overschreven.  

- Verbindingen met de proxy gebruiken standaard het **systeem** account van de computer die als host fungeert voor de site systeemrol.  

- Als het computer account niet kan worden geverifieerd, kan de site systeem Server gebruikers referenties opslaan om verbinding te maken met de proxy server. Deze referenties zijn het **Server account van het site systeem**.  

## <a name="site-system-roles-that-use-a-proxy"></a>Site systeem rollen die gebruikmaken van een proxy

De volgende site systeem rollen maken verbinding met internet en kunnen, indien nodig, een proxy server gebruiken:  

### <a name="asset-intelligence-synchronization-point"></a>Asset Intelligence-synchronisatiepunt

Deze site systeemrol maakt verbinding met micro soft en gebruikt een proxyserver configuratie op de computer die als host fungeert voor het Asset Intelligence synchronisatie punt.  

### <a name="cloud-distribution-point"></a>Cloud distributiepunt

De rol van het Cloud distributiepunt wordt uitgevoerd in Microsoft Azure. U kunt deze site systeemrol niet configureren voor het gebruik van een proxy. Stel de proxy configuratie in op de primaire site server die het Cloud distributiepunt beheert.  

Voor deze configuratie moet de primaire siteserver:  

- U moet verbinding kunnen maken met Microsoft Azure om inhoud in te stellen, te bewaken en te distribueren naar het Cloud distributiepunt.  

- Maakt standaard gebruik van het **systeem** account van de computer om verbinding te maken. Het kan ook het site systeem proxyserver account gebruiken, indien nodig.  

- Maakt gebruik van Windows web browser-Api's.  

### <a name="cloud-management-gateway-connection-point"></a>Verbindings punt van de Cloud beheer gateway

Het CMG-verbindings punt (Cloud Management Gateway) is een on-premises rol die communiceert met de CMG-service in Azure. Zie [plan for the CMG](../../clients/manage/cmg/plan-cloud-management-gateway.md)voor meer informatie.

### <a name="distribution-point"></a>Distributiepunt

<!-- 5856396 -->

Als u vanaf versie 2002 een Configuration Manager distributie punt voor micro soft Connected cache inschakelt, kan het communiceren via een niet-geverifieerde proxy server voor Internet toegang. Zie [micro soft Connected cache](../hierarchy/microsoft-connected-cache.md)(Engelstalig) voor meer informatie.

### <a name="exchange-server-connector"></a>Exchange Server-connector

Deze site systeemrol maakt verbinding met een Exchange-Server. Er wordt een proxy server configuratie gebruikt op de computer die als host fungeert voor de Exchange Server-connector.  

### <a name="service-connection-point"></a>Serviceverbindingspunt

Deze site systeemrol maakt verbinding met de Configuration Manager Cloud service om versie-updates te downloaden voor Configuration Manager. Er wordt gebruikgemaakt van een proxy server die is geconfigureerd op de computer die het service verbindings punt host.  

### <a name="software-update-point"></a>Software-updatepunt

Deze site systeemrol maakt gebruik van de proxy wanneer deze verbinding maakt met Microsoft Update om patches te downloaden en informatie over updates te synchroniseren. Net als bij elke andere site systeemrol configureert u eerst de proxy-instellingen van het site systeem. Configureer vervolgens de volgende opties die specifiek zijn voor het software-update punt:  

- **Gebruik een proxyserver bij het synchroniseren van software-updates**  

- **Gebruik een proxyserver bij het downloaden van inhoud met behulp van automatische implementatieregels**  

    > [!NOTE]
    > Deze instelling wordt niet gebruikt door software-update punten op secundaire sites terwijl deze beschikbaar is voor gebruik.  

Deze instellingen bevinden zich op het tabblad **proxy-en account instellingen** van de eigenschappen van het software-update punt.  

> [!NOTE]
> Wanneer de automatische implementatie regels worden uitgevoerd, wordt standaard het **systeem** account op de site server van de site waarop een automatische implementatie regel is gemaakt, gebruikt om verbinding te maken met internet en software-updates te downloaden. U kunt ook het account van de proxy server van het site systeem configureren en gebruiken. 
>
> Als dit account geen toegang heeft tot internet, kunnen software-updates niet worden gedownload. De volgende vermelding wordt vastgelegd in **bestand ruleengine. log**:  
> `Failed to download the update from internet. Error = 12007.`  

## <a name="other-features-that-use-the-proxy-for-a-site-system-server"></a><a name="bkmk_other"></a>Andere functies die gebruikmaken van de proxy voor een site systeem server

*(Geïntroduceerd in versie 2002)*

Vanaf Configuration Manager versie 2002 gebruiken de volgende functies de proxy van het site systeem dat als host fungeert voor de rol van het [service aansluitpunt](#service-connection-point) : <!--5913817-->

- [Gebruikers detectie van Azure Active Directory (Azure AD)](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- [Detectie van Azure AD-gebruikers groepen](../../servers/deploy/configure/about-discovery-methods.md#bkmk_azuregroupdisco)
- [De resultaten van het verzamelings lidmaatschap synchroniseren met Azure Active Directory groepen](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync)

## <a name="configure-the-proxy-for-a-site-system-server"></a>De proxy configureren voor een site systeem server  

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **site configuratie**uit en selecteer vervolgens het knoop punt **servers en site systeem rollen** .  

2. Selecteer de site systeem server die u wilt bewerken. Klik in het detail venster met de rechter muisknop op de **site systeemrol** en selecteer **Eigenschappen**.  

3. Ga in site systeem eigenschappen naar het tabblad **proxy** . Configureer de volgende proxy-instellingen:  

    - **Een proxy server gebruiken bij het synchroniseren van gegevens van Internet**: Selecteer deze optie om de site systeem server in te scha kelen voor gebruik van een proxy server.  

    - **Proxyserver naam**: Geef de HOSTNAAM of FQDN op van de proxy server in uw omgeving.  

    - **Poort**: Geef de netwerk poort op waarop moet worden gecommuniceerd met de proxy server. Dit maakt standaard gebruik van poort **80**.  

    - **Referenties gebruiken om verbinding te maken met de proxy server**: voor veel proxy servers moet een gebruiker worden geverifieerd. De site systeem server gebruikt standaard het computer account om verbinding te maken met de proxy server. Indien nodig, schakelt u deze optie in, klikt u op **instellen**en kiest u vervolgens een **bestaand account** of geeft u een **Nieuw account**op. Deze referenties zijn het **Server account van het site systeem**.  Zie [accounts die worden gebruikt in Configuration Manager](../hierarchy/accounts.md)voor meer informatie.  

4. Kies **OK** om de nieuwe proxyserver configuratie op te slaan.  

## <a name="next-steps"></a>Volgende stappen

Als uw organisatie netwerk communicatie met Internet beperkt met behulp van een firewall of proxy apparaat, moet u toegang tot internet-eind punten toestaan. Zie [vereisten voor Internet toegang](internet-endpoints.md)voor meer informatie.
