---
title: Microsoft verbonden cache
titleSuffix: Configuration Manager
description: Uw Configuration Manager-distributie punt gebruiken als lokale cache server voor leverings optimalisatie
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e718e62f097a9fec20d7b29deb9f03453931188a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81714967"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Met micro soft verbonden cache in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

<!--3555764-->

Vanaf versie 1906 kunt u een micro soft Connected cache-server op uw distributie punten installeren. Door deze inhoud on-premises in de cache te plaatsen, kunnen uw clients profiteren van de functie voor Delivery Optimization, maar kunt u WAN-koppelingen helpen beveiligen.

> [!NOTE]
> Vanaf versie 1910 wordt deze functie nu **micro soft Connected cache**genoemd. Voorheen bekend als Delivery Optimization in-Network cache (DOINC).

Deze cache server fungeert als transparante cache op aanvraag voor inhoud die wordt gedownload door Delivery Optimization. Gebruik client instellingen om te controleren of deze server alleen wordt aangeboden aan de leden van de lokale Configuration Manager grens groep.

Deze cache is gescheiden van de inhoud van het distributie punt van Configuration Manager. Als u hetzelfde station kiest als de distributiepunt rol, wordt de inhoud afzonderlijk opgeslagen.

> [!Note]  
> De verbonden cache server is een toepassing die is geïnstalleerd op Windows Server. Deze toepassing is nog in ontwikkeling.

## <a name="how-it-works"></a>Hoe werkt het?

Wanneer u clients configureert voor het gebruik van de verbonden cache server, vragen ze geen door micro soft Cloud beheerde inhoud meer via internet. Clients vragen deze inhoud van de cache server die is geïnstalleerd op het distributie punt. De on-premises server slaat deze inhoud op in de cache met behulp van de IIS-functie voor Application Request Routing (ARR). Vervolgens kan de cache server snel reageren op toekomstige aanvragen voor dezelfde inhoud. Als de verbonden cache server niet beschikbaar is, of als de inhoud nog niet in de cache is opgeslagen, downloaden clients de inhoud van het internet. Clients gebruiken ook Delivery Optimization, dus downloaden delen van de inhoud van peers in hun netwerk.

![Diagram van de werking van de verbonden cache](media/3555764-microsoft-connected-cache.png)

1. Client controleert op updates en haalt het adres op voor het Content Delivery Network (CDN).

2. Configuration Manager configureert instellingen voor Delivery Optimization (DO) op de client, met inbegrip van de naam van de cache server.

3. Client A vraagt de inhoud van de cache server.

4. Als de cache de inhoud niet bevat, wordt deze door de cache server opgehaald uit het CDN.

5. Als de cache server niet reageert, downloadt de client de inhoud van het CDN.

6. Clients gebruiken om delen van de inhoud van peers te verkrijgen.

## <a name="prerequisites-and-limitations"></a>Vereisten en beperkingen

- Een *on-premises* distributie punt met de volgende configuraties:

  - Met Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 of Windows Server 2019

  - De standaard website ingeschakeld op poort 80

  - Installeer de functie IIS [Application Request Routing](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (arr) niet vooraf. Verbonden cache installeert ARR en configureert de instellingen. Micro soft kan niet garanderen dat de verbindings configuratie van de verbonden cache niet in conflict is met andere toepassingen op de server waarop ook deze functie wordt gebruikt.

  - Het distributie punt vereist Internet toegang tot de micro soft-Cloud. De specifieke Url's kunnen variëren, afhankelijk van de specifieke Cloud inhoud. Zie [vereisten voor Internet toegang](../network/internet-endpoints.md)voor meer informatie.

  - Vanaf versie 2002 kan de toepassing voor de verbonden cache een niet-geverifieerde proxy server gebruiken voor Internet toegang. Zie [Configure the proxy for a site System server](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)(Engelstalig) voor meer informatie.<!-- 5856396 -->

- Clients met Windows 10 versie 1709 of hoger

## <a name="enable-connected-cache"></a>Verbonden cache inschakelen

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** en selecteer het knoop punt **distributie punten** .

1. Selecteer een *on-premises* distributie punt en selecteer vervolgens in het lint **Eigenschappen**.

1. Configureer de volgende instellingen in de eigenschappen van de distributiepunt rol op het tabblad **Algemeen** :  

    1. Schakel de optie in om **Dit distributie punt in te scha kelen voor gebruik als micro soft Connected cache server**  

        De licentie voorwaarden weer geven en accepteren.

    2. **Te gebruiken lokaal station**: Selecteer de schijf die moet worden gebruikt voor de cache. **Automatisch** is de standaard waarde, die gebruikmaakt van de schijf met de meeste vrije ruimte. <sup> [Opmerking 1](#bkmk_note1)</sup>  

        > [!Note]  
        > U kunt dit station later wijzigen. Alle inhoud in de cache gaat verloren, tenzij u deze naar het nieuwe station kopieert.

    3. **Schijf ruimte**: Selecteer de hoeveelheid schijf ruimte die moet worden gereserveerd in GB of een percentage van de totale schijf ruimte. Deze waarde is standaard 100 GB.

        > [!Note]  
        > De standaard cache grootte moet voldoende zijn voor de meeste klanten. U kunt de cache grootte later aanpassen.
        >
        > Als de cache grootte op schijf de toegewezen ruimte overschrijdt, wordt de ruimte door de inhoud verwijderd op basis van de ingebouwde heuristiek.<!-- SCCMDocs#2045 -->

    4. **Cache behouden bij uitschakelen van de verbonden cache server**: als u de cache server verwijdert en u deze optie inschakelt, behoudt de server de inhoud van de cache op de schijf.  

1. Configureer in client instellingen in de groep **Delivery Optimization** de instelling zodat **apparaten die worden beheerd door Configuration Manager, gebruik kunnen maken van micro soft Connected cache servers voor het downloaden van inhoud**.  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a>Opmerking 1: station selecteren

Als u **automatisch**selecteert en het verbonden cache onderdeel wordt geïnstalleerd door Configuration Manager, wordt het **no_sms_on_drive. SMS** -bestand geaccepteerd. Het distributie punt heeft bijvoorbeeld het bestand `C:\no_sms_on_drive.sms`. Zelfs als de station C: de meeste vrije ruimte heeft, configureert Configuration Manager verbonden cache om een ander station te gebruiken voor de cache.

Als u een specifiek station selecteert dat al het bestand **no_sms_on_drive. SMS** bevat, wordt het bestand door Configuration Manager genegeerd. Configureren van verbonden cache voor gebruik van dat station is een expliciete intentie. Het distributie punt heeft bijvoorbeeld het bestand `F:\no_sms_on_drive.sms`. Wanneer u de eigenschappen van het distributie punt expliciet configureert voor het gebruik van het station **f:** , Configuration Manager configureert verbonden cache om het station f: te gebruiken voor de cache.

Het station wijzigen nadat u de verbonden cache hebt geïnstalleerd:

- Configureer hand matig de eigenschappen van het distributie punt voor het gebruik van een specifieke stationsletter.

- Als deze is ingesteld op automatisch, moet u eerst het **no_sms_on_drive. SMS** -bestand maken. Breng vervolgens een wijziging aan in de eigenschappen van het distributie punt om een configuratie wijziging te activeren.

## <a name="verify"></a>Verifiëren

Wanneer clients door de Cloud beheerde inhoud downloaden, gebruiken ze Delivery Optimization van de cache server die is geïnstalleerd op uw distributie punt. Cloud-beheerde inhoud bevat de volgende typen:

- Microsoft Store-apps
- Windows-onderdelen op aanvraag, zoals talen
- Als u [Windows Update voor bedrijfs beleid](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)inschakelt: Windows 10-onderdelen en kwaliteits updates
- Voor [werk belastingen voor co-beheer](../../../comanage/workloads.md):
  - Windows Update voor bedrijven: Windows 10-onderdelen en kwaliteits updates
  - Office klik-en-klaar-apps: Office-apps en-updates
  - Client-apps: Microsoft Store apps en updates
  - Endpoint Protection: definitie-updates voor Windows Defender

Controleer op Windows 10 versie 1809 of hoger dit gedrag met de Windows Power shell **-cmdlet Get-DeliveryOptimizationStatus** . Controleer de **BytesFromCacheServer** -waarde in de uitvoer van de cmdlet. Zie [Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization)voor meer informatie.

Als de cache server een HTTP-fout retourneert, valt de Delivery Optimization-client terug naar de oorspronkelijke Cloud bron.

Zie [problemen met micro soft Connected cache in Configuration Manager oplossen](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)voor meer informatie.

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a>Ondersteuning voor intune Win32-apps

<!--5032900-->

Vanaf versie 1910, wanneer u verbonden cache inschakelt op uw Configuration Manager-distributie punten, kunnen ze Microsoft Intune Win32-apps gebruiken voor gezamenlijk beheerde clients.

### <a name="prerequisites"></a>Vereisten

#### <a name="client"></a>Client

- Werk de client bij naar de nieuwste versie.

- Het client apparaat moet ten minste 4 GB geheugen hebben.

    > [!TIP]
    > Gebruik de volgende groeps beleids instelling: computer configuratie > Beheersjablonen > Windows-onderdelen > Delivery Optimization > **Mini maal RAM-geheugen vereist om het gebruik van peer-caching (in GB) in te scha kelen**.

#### <a name="site"></a>Site

- Verbonden cache inschakelen op een distributie punt. Zie [micro soft Connected cache](microsoft-connected-cache.md)(Engelstalig) voor meer informatie.

- De client en het verbonden distributie punt met de cache-instelling moeten zich in dezelfde grens groep bevinden.

- Schakel de volgende client instellingen in de groep [**Delivery Optimization**](../../clients/deploy/about-client-settings.md#delivery-optimization) in:

  - **Configuration Manager grens groepen gebruiken voor de ID van de leverings optimalisatie groep**
  - **Apparaten die door Configuration Manager worden beheerd, kunnen gebruikmaken van micro soft Connected cache-servers voor het downloaden van inhoud**

- Schakel de voorlopige versie van de **client-apps in voor gezamenlijk beheerde apparaten**. Zie functies van de [voorlopige versie](../../servers/manage/pre-release-features.md)voor meer informatie.

- Schakel co-beheer in en schakel de workload van de **client-apps** over naar **intune** of **intune**. Raadpleeg voor meer informatie de volgende artikelen:

  - [Workloads-client-apps](../../../comanage/workloads.md#client-apps)
  - [Co-beheer inschakelen](../../../comanage/how-to-enable.md)
  - [Workloads overhevelen naar Intune](../../../comanage/how-to-switch-workloads.md)

    Als u in pilot bent, voegt u de client toe aan de pilot verzameling voor client-apps.

#### <a name="intune"></a>Intune

- Deze functie ondersteunt alleen het type van de intune Win32-app.

  - Een nieuwe app maken en toewijzen (implementeren) in intune voor dit doel einde. (Apps die zijn gemaakt voor versie 1811 van intune werken niet.) Zie [intune Win32 app Management](https://docs.microsoft.com/intune/apps/apps-win32-app-management)voor meer informatie.

  - De app moet ten minste 100 MB groot zijn.
  
    > [!TIP]
    > Gebruik de volgende groeps beleids instelling: computer configuratie > Beheersjablonen > Windows-onderdelen > bezorgings optimalisatie > **minimale grootte van het inhouds bestand van de peer-cache (in MB)**.

## <a name="see-also"></a>Zie ook

[Windows 10-updates optimaliseren met Delivery Optimization](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Problemen met micro soft Connected cache in Configuration Manager oplossen](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
