---
title: Problemen met verbonden cache oplossen
titleSuffix: Configuration Manager
description: Technische Details voor micro soft Connected cache om u te helpen bij het oplossen van problemen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 121e0341-4f51-4d54-a357-732c26caf7c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a8c975798c506339a981e8648003387dc1e9838
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/27/2020
ms.locfileid: "83878103"
---
# <a name="troubleshoot-microsoft-connected-cache-in-configuration-manager"></a>Problemen met micro soft Connected cache in Configuration Manager oplossen

In dit artikel vindt u technische gegevens over micro soft Connected cache in Configuration Manager. Gebruik dit hulp programma om problemen op te lossen die in uw omgeving mogelijk zijn. Zie voor meer informatie over hoe het werkt en hoe u deze kunt gebruiken [micro soft Connected cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

> [!NOTE]
> Vanaf versie 1910 wordt deze functie nu **micro soft Connected cache**genoemd. Het was voorheen bekend als Delivery Optimization in-Network cache.

## <a name="verify"></a>Verifiëren

Wanneer u de cache server voor de bezorg optimalisatie correct installeert en clients correct configureert, worden ze gedownload vanaf de cache server die is geïnstalleerd op uw distributie punt in plaats van op internet.

Controleer dit gedrag [op een client](#bkmk_verify-client) of [op de server](#bkmk_verify-server).

### <a name="verify-on-a-client"></a><a name="bkmk_verify-client"></a>Controleren op een client

1. Op de client met Windows 10, versie 1809 of hoger, kunt u in de Cloud beheerde inhoud downloaden. Zie voor meer informatie over de typen inhoud die in de cache zijn opgeslagen, [gekoppelde cache verifiëren](../../../plan-design/hierarchy/microsoft-connected-cache.md#verify).

2. Open Power shell en voer de volgende opdracht uit:`Get-DeliveryOptimizationStatus`

Bijvoorbeeld:

```PowerShell
PS C:\> Get-DeliveryOptimizationStatus

FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
FileSize                    : 549064
TotalBytesDownloaded        : 549064
PercentPeerCaching          : 0
BytesFromPeers              : 0
BytesFromHttp               : 0
Status                      : Caching
Priority                    : Background
BytesFromCacheServer        : 549064
BytesFromLanPeers           : 0
BytesFromGroupPeers         : 0
BytesFromInternetPeers      : 0
BytesToLanPeers             : 0
BytesToGroupPeers           : 0
BytesToInternetPeers        : 0
DownloadDuration            : 00:00:00.0780000
HttpConnectionCount         : 2
LanConnectionCount          : 0
GroupConnectionCount        : 0
InternetConnectionCount     : 0
DownloadMode                : 99
SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                              atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
NumPeers                    : 0
PredefinedCallerApplication : WU Client Download
ExpireOn                    : 9/6/2019 8:36:19 AM
IsPinned                    : False
```

U ziet dat het `BytesFromCacheServer` kenmerk niet gelijk is aan nul.

Als de client onjuist is geconfigureerd of de cache server niet correct is geïnstalleerd, gaat de Delivery Optimization-client terug naar de oorspronkelijke Cloud bron. Het kenmerk BytesFromCacheServer is dan nul.

### <a name="verify-on-the-server"></a><a name="bkmk_verify-server"></a>Controleren op de server

Controleer eerst of de register eigenschappen correct zijn geconfigureerd: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache` . De locatie van de schijf cache is bijvoorbeeld `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294` , waar `PrimaryDrivesInput` meerdere stations kunnen zijn, zoals `C,D,E` .

Gebruik vervolgens de volgende methode om een client Download aanvraag naar de server met de verplichte headers te simuleren.

1. Open een 64-bits Power shell-venster als beheerder.
2. Voer de volgende opdracht uit en vervang de naam of het IP-adres van uw server voor `<DoincServer>` :

```PowerShell
Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
```

De uitvoer ziet er ongeveer uit als in het volgende voor beeld:

```PowerShell
PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


StatusCode        : 200
StatusDescription : OK
Content           : {71, 73, 70, 56...}
RawContent        : HTTP/1.1 200 OK
                    X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                    .p,1567797125.cds058.se2.p
                    X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                    t2.p,1567797125.cds058.se2.p], [X-CCC,
                    cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                    [X-CID, 100], [Accept-Ranges, bytes]...}
RawContentLength  : 969710
```

De volgende kenmerken duiden op geslaagd:

- `StatusCode : 200`
- `StatusDescription : OK`

## <a name="log-files"></a>Logboekbestanden

- Setup-logboek voor ARR:`%temp%\arr_setup.log`

- Logboek voor installatie van cache server: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` op het distributie punt en `DistMgr.log` op de site server

- Operationele logboeken van IIS: standaard`%SystemDrive%\inetpub\logs\LogFiles`

- Operationeel logboek van cache server:`C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Met dit logboek kunt u onder andere gebruikmaken van problemen met de connectiviteit met de micro soft-Cloud.

## <a name="setup-error-codes"></a>Fout codes voor Setup

Als Configuration Manager het verbonden cache onderdeel op het distributie punt installeert, worden in de volgende tabel de mogelijke fout codes vermeld die zich kunnen voordoen:

| Foutcode | Foutbeschrijving |
|------------|-------------------|
| 0x00000000 | Geslaagd |
| 0x00000BC2 | Geslaagd, opnieuw opstarten is vereist |
| 0x00000643 | Algemene installatie fout |
| 0x00D00001 | Setup van verbonden cache kan alleen worden uitgevoerd als Internet Information Services (IIS) is geïnstalleerd |
| 0x00D00002 | Setup van verbonden cache kan alleen worden uitgevoerd als een standaard website op de server bestaat |
| 0x00D00003 | U kunt geen verbonden cache installeren als Application Request Routing (ARR) al is geïnstalleerd |
| 0x00D00004 | Setup van verbonden cache kan alleen worden uitgevoerd als Application Request Routing (ARR) is geïnstalleerd door het script install. ps1 |
| 0x00D00005 | Setup van verbonden cache vereist een Power shell-sessie die wordt uitgevoerd als beheerder |
| 0x00D00006 | Setup van verbonden cache kan alleen worden uitgevoerd vanuit een 64-bits Power shell-omgeving |
| 0x00D00007 | Setup van verbonden cache kan alleen worden uitgevoerd op een Windows-Server |
| 0x00D00008 | Fout: het aantal opgegeven cache stations moet overeenkomen met het aantal opgegeven cache station grootte percentages |
| 0x00D00009 | Fout: er moet een geldige cache knooppunt-ID worden opgegeven |
| 0x00D0000A | Fout: er moet een geldige cache drive set worden opgegeven |
| 0x00D0000B | Fout: er moet een geldig percentage van de grootte van het cache station worden opgegeven |
| 0x00D0000C | Fout: er moet een geldige percentage van de grootte van het cache station of de grootte van het cache station in GB worden opgegeven |
| 0x00D0000D | Fout: een geldig percentage van de cache schijf grootte en de grootte van het cache station in GB kunnen niet beide worden opgegeven |
| 0x00D0000E | Fout: het aantal opgegeven cache stations moet overeenkomen met de grootte van het cache station in GB opgegeven |
| 0x00D0000F | Fout: kan geen back-up maken van het bestand ApplicationHost. config van $AppHostConfig naar $AppHostConfigDestinationName |
| 0x00D00010 | Fout: kan geen back-up maken van het web. config-bestand van de standaard website van $WebsiteConfigFilePath naar $WebConfigDestinationName |
| 0x00D00011 | Fout: er is een uitzonde ring opgetreden in SetupARRWebFarm. ps1 |
| 0x00D00012 | Fout: er is een uitzonde ring opgetreden in SetupARRWebFarmRewriteRules. ps1 |
| 0x00D00013 | Fout: er is een uitzonde ring opgetreden in SetupARRWebFarmProperties. ps1 |
| 0x00D00014 | Fout: er is een uitzonde ring opgetreden in SetupAllowableServerVariables. ps1 |
| 0x00D00015 | Fout: er is een uitzonde ring opgetreden in SetupFirewallRules. ps1 |
| 0x00D00016 | Fout: er is een uitzonde ring opgetreden in SetupAppPoolProperties. ps1 |
| 0x00D00017 | Fout: er is een uitzonde ring opgetreden in SetupARROutboundRules. ps1 |
| 0x00D00018 | Fout: er is een uitzonde ring opgetreden in SetupARRDiskCache. ps1 |
| 0x00D00019 | Fout: er is een uitzonde ring opgetreden in SetupARRProperties. ps1 |
| 0x00D0001A | Fout: er is een uitzonde ring opgetreden in SetupARRHealthProbes. ps1 |
| 0x00D0001B | Fout: er is een uitzonde ring opgetreden in VerifyIISSItesStarted. ps1 |
| 0x00D0001C | Fout: er is een uitzonde ring opgetreden in SetDrivesToHealthy. ps1 |
| 0x00D0001D | Fout: er is een uitzonde ring opgetreden in VerifyCacheNodeSetup. ps1 |
| 0x00D0001E | U kunt geen verbonden cache installeren als de standaard website zich niet op poort 80 bevindt |
| 0x00D0001F | Fout: de toewijzing van het cache station in percentage kan niet groter zijn dan 100 |
| 0x00D00020 | Fout: de toewijzing van het cache-station in GB kan niet groter zijn dan de beschik bare ruimte op het station |
| 0x00D00021 | Fout: de toewijzing van het cache-station in percentage moet groter dan 0 zijn |
| 0x00D00022 | Fout: de toewijzing van het cache-station in GB moet groter dan 0 zijn |
| 0x00D00023 | Fout: er is een uitzonde ring opgetreden in RegisterScheduledTask_CacheNodeKeepAlive |
| 0x00D00024 | Fout: er is een uitzonde ring opgetreden in RegisterScheduledTask_Maintenance |
| 0x00D00025 | Fout: er is een uitzonde ring opgetreden tijdens het instellen van de herschrijf regels voor de HTTPS-Farm: $FarmName |
| 0x00D00026 | Fout: er is een uitzonde ring opgetreden tijdens het instellen van de herschrijf regels voor de HTTP-Farm: $FarmName |
| 0x00D00027 | U kunt geen verbonden cache installeren omdat de installatie van de afhankelijke software Application Request Routing (ARR) is mislukt. Zie het logboek bestand dat zich bevindt in% Temp% \ arr_setup. log |

## <a name="iis-configurations"></a>IIS-configuraties

Bij de installatie van de cache server worden verschillende wijzigingen aangebracht in de IIS-configuratie op het distributie punt.

### <a name="application-request-routing"></a>Route ring van toepassings aanvragen

De DO cache server installeert en configureert IIS [Application Request Routing (arr)](https://www.iis.net/downloads/microsoft/application-request-routing). Om potentiële conflicten te voor komen, kan dit onderdeel niet al op het distributie punt zijn geïnstalleerd.

### <a name="allowed-server-variables"></a>Toegestane Server variabelen

Nadat u de cache server hebt geïnstalleerd, hebben de standaard website de volgende *lokale* Server variabelen:

- HTTP_HOST
- QUERY_STRING
- X-CC
- X-CID
- X-DOINC-UITGAAND

### <a name="rewrite-rules"></a>Regels opnieuw schrijven

De DO cache server voegt de volgende regels voor herschrijven toe:

#### <a name="inbound-rewrite-rules"></a>Regels voor binnenkomende herschrijven

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### <a name="outbound-rewrite-rules"></a>Regels voor uitgaande herschrijven

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

## <a name="manage-server-resources"></a>Server resources beheren

De benodigde schijf ruimte voor elke cache server kan variëren, afhankelijk van de update vereisten van uw organisatie. 100 GB moet voldoende ruimte hebben om de volgende inhoud in de cache op te slaan:

- Een onderdeel Update
- Twee tot drie maanden kwaliteits-en Office-updates
- Microsoft Intune apps en Windows-apps in het postvak in

De DO cache server mag niet veel systeem geheugen of processor tijd verbruiken. Nadat u de cache server hebt geïnstalleerd, moet u de IIS-en ARR-logboek bestanden analyseren als u belang rijk proces-of geheugen Resource verbruik ziet.

Als de IIS-en ARR-logboek bestanden te veel ruimte op de server in beslag nemen, zijn er verschillende methoden die u kunt gebruiken om de logboek bestanden te beheren. Zie [IIS-logboek File Storage beheren](https://docs.microsoft.com/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview)voor meer informatie.

## <a name="see-also"></a>Zie ook

[Met micro soft verbonden cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
