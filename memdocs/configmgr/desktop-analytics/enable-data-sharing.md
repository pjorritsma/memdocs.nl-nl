---
title: Gegevens delen inschakelen
titleSuffix: Configuration Manager
description: Een referentie gids voor het delen van diagnostische gegevens met Desktop Analytics.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 999d8441e8c97f0a4b7ad4a92c8175300dcc4ead
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696443"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Gegevens delen inschakelen voor desktop Analytics

Als u apparaten wilt registreren bij Desktop Analytics, moeten ze diagnostische gegevens verzenden naar micro soft. Als uw omgeving gebruikmaakt van een proxy server, gebruikt u deze informatie om de proxy te configureren.

## <a name="diagnostic-data-levels"></a>Niveaus van diagnostische gegevens

:::image type="content" source="media/diagnostic-data-levels.png" alt-text="Diagram van diagnostische gegevens niveaus voor desktop Analytics":::

Wanneer u Configuration Manager integreert met Desktop Analytics, kunt u deze ook gebruiken om het diagnostische gegevens niveau op apparaten te beheren. Gebruik Configuration Manager voor de beste ervaring.

> [!IMPORTANT]
> In de meeste gevallen gebruikt u Configuration Manager voor het configureren van deze instellingen. Deze instellingen zijn niet ook van toepassing op domein groeps beleidsobjecten. Zie [conflict oplossing](enroll-devices.md#conflict-resolution)voor meer informatie.

De basis functionaliteit van Desktop Analytics werkt op het **vereiste** [Diagnostische-gegevens niveau](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels). Als u het **optionele (beperkte)** niveau in Configuration Manager niet configureert, worden de volgende functies van Desktop Analytics niet weer geven:

- App-gebruik
- [Aanvullende app-inzichten](compat-assessment.md#additional-insights)
- [Implementatie status gegevens](deploy-prod.md#address-deployment-alerts)
- [Status bewakings gegevens](health-status-monitoring.md)

Micro soft raadt u aan het **optionele (beperkte)** diagnostische gegevens niveau in te scha kelen met Desktop Analytics om de voor delen van het apparaat te maximaliseren.

> [!TIP]
> De **optionele (beperkte)** instelling in Configuration Manager is dezelfde instelling als **uitgebreide diagnostische gegevens beperken tot de minimale vereisten die vereist zijn voor Windows Analytics** -beleid op apparaten met windows 10, versie 1709 en hoger.
>
> Apparaten met Windows 10, versie 1703 en lager, Windows 8,1 of Windows 7 hebben deze beleids instelling niet. Wanneer u de **optionele (beperkte)** instelling in Configuration Manager configureert, vallen deze apparaten terug naar het **vereiste** niveau.
>
> Apparaten met Windows 10, versie 1709 beschikken over deze beleids instelling. Wanneer u echter de **optionele (beperkte)** instelling in Configuration Manager configureert, vallen deze apparaten ook terug naar het **vereiste** niveau.
>
> In Configuration Manager versie 2002 en eerder hebben de instellingen verschillende namen:<!-- 7363467 -->
>
> | Versie 2006 en hoger | Versie 2002 en lager |
> |---------|---------|
> | Vereist | Basic |
> | Optioneel (beperkt) | Verbeterd (beperkt) |
> | N.v.t. | Verbeterd |
> | Optioneel | Volledig |
>
> Als u eerder apparaten op het niveau **verbeterd** hebt geconfigureerd, worden deze teruggezet naar **optioneel (beperkt)** wanneer u een upgrade uitvoert naar versie 2006. Ze verzenden minder gegevens naar micro soft. Deze wijziging is niet van invloed op wat u ziet in Desktop Analytics.

Zie voor meer informatie over diagnostische gegevens die met micro soft worden gedeeld met **optioneel (beperkt)** [Windows 10 uitgebreide diagnostische gegevens gebeurtenissen en velden](/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!IMPORTANT]
> Micro soft heeft een sterke toezeg ging voor het leveren van de hulpprogram ma's en resources die u in staat stellen om uw privacy te beheren. Als desktop Analytics ondersteunt Windows 8,1-apparaten, verzamelt micro soft geen diagnostische gegevens van Windows van Windows 8,1-apparaten die zich in Europese landen (EER en Zwitser land) bevinden.

Zie [privacy van Desktop Analytics](privacy.md)voor meer informatie.

De volgende artikelen zijn ook goede bronnen voor meer informatie over Windows diagnostische gegevens niveaus:

- [Windows 10 en de AVG voor IT-besluit vormers](/windows/privacy/gdpr-it-guidance)  

- [Windows diagnostische gegevens configureren in uw organisatie](/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!NOTE]
> Clients die zijn geconfigureerd voor het verzenden van **optionele (beperkte)** diagnostische gegevens verzenden ongeveer 2 MB aan gegevens naar de micro soft-Cloud op de eerste volledige scan. De dagelijkse Delta wijkt af van 250-400 KB per dag.
>
> De dagelijkse Delta scan wordt uitgevoerd om 3:00 uur (lokale tijd van het apparaat). Sommige gebeurtenissen worden verzonden op het eerste beschik bare tijdstip gedurende de hele dag. Deze tijden kunnen niet worden geconfigureerd.
>
> Zie [Diagnostische gegevens van Windows in uw organisatie configureren](https://aka.ms/enterprisetelemetry) voor meer informatie.  

## <a name="endpoints"></a>Eindpunten

Als u het delen van gegevens wilt inschakelen, moet u uw proxy server configureren voor het toestaan van de volgende Internet-eind punten.

> [!IMPORTANT]
> Voor privacy-en gegevens integriteit controleert Windows naar een micro soft SSL-certificaat (certificaat vastmaken) bij de communicatie met de eind punten van de diagnostische gegevens. SSL-onderscheping en-inspectie zijn niet mogelijk. Als u Desktop Analytics wilt gebruiken, moet u deze eind punten uitsluiten van SSL-inspectie.<!-- BUG 4647542 -->

Vanaf versie 2002, als de Configuration Manager-site geen verbinding kan maken met de vereiste eind punten voor een Cloud service, wordt een kritieke status bericht-ID 11488 gegenereerd. Wanneer er geen verbinding kan worden gemaakt met de service, wordt de status van het SMS_SERVICE_CONNECTOR onderdeel gewijzigd in kritiek. Bekijk de gedetailleerde status in het knoop punt [onderdeel status](../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorSystemStatus) van de Configuration Manager-console.<!-- 5566763 -->

> [!NOTE]
> Zie [open bare IP-adres ruimte van micro soft](https://www.microsoft.com/download/details.aspx?id=53602)voor meer informatie over de IP-adresbereiken van micro soft. Deze adressen worden regel matig bijgewerkt. Er is geen granulatie per service, elk IP-adres in deze bereiken kan worden gebruikt.

[!INCLUDE [Internet endpoints for Desktop Analytics](../core/plan-design/network/includes/internet-endpoints-desktop-analytics.md)]

## <a name="proxy-server-authentication"></a>Verificatie van de proxy server

Als uw organisatie verificatie van de proxy server gebruikt voor Internet toegang, moet u ervoor zorgen dat de diagnostische gegevens niet worden geblokkeerd door verificatie. Als uw proxy niet toestaat dat apparaten deze gegevens verzenden, worden ze niet weer gegeven in Desktop Analytics.

### <a name="bypass-recommended"></a>Bypass (aanbevolen)

Configureer uw proxy servers zo dat er geen proxy verificatie nodig is voor het verkeer naar de eind punten van de diagnostische gegevens. Deze optie is de meest uitgebreide oplossing. Het werkt voor alle versies van Windows 10.  

### <a name="user-proxy-authentication"></a>Verificatie van de gebruikers proxy

Apparaten configureren voor het gebruik van de context van de aangemelde gebruiker voor proxy verificatie. Voor deze methode zijn de volgende configuraties vereist:

- Apparaten hebben de huidige kwaliteits update voor een ondersteunde versie van Windows

- Configureer proxy op gebruikers niveau (WinINET-proxy) in **proxy-instellingen** in het netwerk & Internet groep Windows-instellingen. U kunt ook de verouderde Internet opties in het configuratie scherm gebruiken.

- Zorg ervoor dat de gebruikers over proxy machtigingen beschikken om de eind punten van de diagnostische gegevens te bereiken. Deze optie vereist dat de apparaten console gebruikers hebben met proxy machtigingen, zodat u deze methode niet kunt gebruiken met headless apparaten.

> [!IMPORTANT]
> De verificatie methode voor de gebruikers proxy is niet compatibel met het gebruik van micro soft Defender Advanced Threat Protection. Dit gedrag is omdat deze verificatie afhankelijk is van de **DisableEnterpriseAuthProxy** -register sleutel die is ingesteld op `0` , terwijl micro soft Defender ATP vereist dat deze is ingesteld op `1` . Zie [instellingen voor machine proxy en Internet connectiviteit configureren in micro soft Defender ATP](/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection)voor meer informatie.

### <a name="device-proxy-authentication"></a>Verificatie van Device proxy

Deze aanpak ondersteunt de volgende scenario's:

- Headless apparaten, waar geen gebruiker zich aanmeldt of gebruikers van het apparaat hebben geen toegang tot Internet

- Geverifieerde proxy's die geen geïntegreerde Windows-verificatie gebruiken

- Als u ook micro soft Defender Advanced Threat Protection gebruikt

Deze benadering is het meest gecompliceerd omdat hiervoor de volgende configuraties zijn vereist:

- Zorg ervoor dat apparaten de proxy server kunnen bereiken via WinHTTP in de context van het lokale systeem. Gebruik een van de volgende opties om dit gedrag te configureren:

  - De opdracht regel `netsh winhttp set proxy`

  - WPAD-protocol (Web Proxy Auto-Discovery)

  - Transparante proxy

  - WinINET-proxy voor het hele apparaat configureren met de volgende groeps beleids instelling: **proxy-instellingen per computer (in plaats van per gebruiker) maken** (ProxySettingsPerUser = `1` )

  - Gerouteerde verbinding of die gebruikmaakt van Network Address Translation (NAT)

- Configureer proxy servers zodanig dat de computer accounts in Active Directory toegang hebben tot de eind punten van de diagnostische gegevens. Voor deze configuratie zijn proxy servers vereist voor ondersteuning van geïntegreerde Windows-authenticatie.