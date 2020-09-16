---
title: Netwerkeindpunten voor Microsoft Intune
titleSuffix: ''
description: Lees de tekst over eindpunten voor Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: e30ec0c695483b493a9df603f5c7501d494c6aec
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574844"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Netwerkeindpunten voor Microsoft Intune  

Op deze pagina worden de IP-adressen en poortinstellingen vermeld die nodig zijn voor de proxy-instellingen in uw Intune-implementaties.

Intune is een service die zich alleen in de cloud bevindt, en hiervoor is geen on-premises infrastructuur, zoals servers of gateways, vereist.

## <a name="access-for-managed-devices"></a>Toegang voor beheerde apparaten  

Als u apparaten wilt beheren die zich achter firewalls en proxyservers bevinden, moet u communicatie voor Intune inschakelen.

> [!NOTE]
> De informatie in deze sectie is ook van toepassing op de Microsoft Intune Certificate Connector. De connector heeft dezelfde netwerkvereisten als beheerde apparaten

- De proxyserver moet zowel **HTTP (80)** als **HTTPS (443)** ondersteunen omdat Intune-clients beide protocollen gebruiken. Windows Information Protection gebruikt poort 444.
- Voor bepaalde taken, zoals het downloaden van software-updates voor de klassieke pc-agent, is in Intune niet-geverifieerde proxyservertoegang vereist tot manage.microsoft.com

U kunt de instellingen voor proxyservers wijzigen op afzonderlijke clientcomputers. U kunt ook de instellingen voor groepsbeleid gebruiken om de instellingen te wijzigen voor alle clientcomputers die zich achter een bepaalde proxyserver bevinden.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

Voor beheerde apparaten zijn configuraties vereist waarmee **alle gebruikers** via firewalls toegang krijgen tot services.


De volgende tabel bevat de poorten en services waartoe de Intune-client toegang heeft:

|Domains    |Het IP-adres      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | Meer informatie [Office 365-URL's en IP-adresbereiken](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com<br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com<br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com<br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com<br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com<br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com<br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0202.manage.microsoft.com<br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com<br>m.fei.amsua0402.manage.microsoft.com<br>portal.fei.amsua0801.manage.microsoft.com<br>portal.fei.msua08.manage.microsoft.com<br>m.fei.msua08.manage.microsoft.com<br>m.fei.amsua0801.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com<br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com<br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com<br>portal.fei.msub02.manage.microsoft.com<br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com<br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com<br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com<br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com<br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com<br>portal.fei.amsub0601.manage.microsoft.com<br>m.fei.amsub0601.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua01.manage.microsoft.com|138.91.243.97|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>Netwerkvereisten voor PowerShell-scripts en Win32-apps  

Als u Intune gebruikt voor het implementeren van PowerShell-scripts of Win32-apps, moet u ook toegang verlenen tot eindpunten waarin uw tenant zich momenteel bevindt.

|ASU | Naam van opslag | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Windows Push Notification Services (WNS)  

Bij Windows-apparaten die door Intune worden beheerd met behulp van Mobile Device Management (MDM) moet voor apparaatacties en andere directe activiteiten Windows Push Notification Services (WNS) worden gebruikt. Zie [Allowing Windows Notification traffic through enterprise firewalls](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config) (Windows Notification-verkeer via de bedrijfsfirewalls toestaan) voor meer informatie.  

## <a name="delivery-optimization-port-requirements"></a>Delivery Optimization-poortvereisten  

### <a name="port-requirements"></a>Poortvereisten  

Voor peer-to-peerverkeer gebruikt Delivery Optimization 7680 voor TCP/IP of 3544 voor NAT Traversal (eventueel Teredo). Voor communicatie tussen client en service wordt HTTP of HTTPS via poort 80/443 gebruikt.

### <a name="proxy-requirements"></a>Proxyvereisten  

Als u Delivery Optimization wilt gebruiken, moet u aanvragen van bytebereiken toestaan. Zie [Proxy requirements for Windows Update](/windows/deployment/update/windows-update-troubleshooting) (Proxyvereisten voor Windows Update) voor meer informatie.

### <a name="firewall-requirements"></a>Firewallvereisten  

Sta de volgende hostnamen via uw firewall toe voor de ondersteuning van Delivery Optimization.
Voor communicatie tussen clients en de Delivery Optimization-cloudservice:
- \*.do.dsp.mp.microsoft.com

Voor Delivery Optimization-metagegevens:
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Netwerkgegevens voor Apple-apparaten  

|Gebruikt voor|Hostnaam (IP-adres/subnet)|Protocol|Poort|
|-----|--------|------|-------|
|Inhoud van Apple-servers ophalen en weergeven|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|Communicatie met APNS-servers|#-courier.push.apple.com<br># is een willekeurig getal van 0 tot en met 50.|    TCP     |  5223 en 443  |
|Verschillende functies waaronder toegang tot internet, de iTunes Store, de MacOS App Store, iCloud, berichten, enzovoort. |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 of 443   |

Zie voor meer informatie de documentatie van Apple: [TCP and UDP ports used by Apple software products](https://support.apple.com/HT202944) (TCP- en UDP-poorten die worden gebruikt voor Apple-softwareproducten), [About macOS, iOS/iPadOS, and iTunes server host connections and iTunes background processes](https://support.apple.com/HT201999) (Over serververbindingen van macOS-, iOS-/iPadOS- en iTunes-hosts, en iTunes-achtergrondprocessen), en [If your macOS and iOS/iPadOS clients aren't getting Apple push notifications](https://support.apple.com/HT203609) (Als uw macOS- en iOS-/iPadOS-clients geen Apple-pushmeldingen ontvangen).  

## <a name="android-port-information"></a>Informatie over Android-poort

Afhankelijk van de keuze om Android-apparaten te beheren, moet u mogelijk de Google Android Enterprise-poorten en/of de Android-pushmelding openen. Raadpleeg de [documentatie voor Android-inschrijving](../enrollment/android-enroll.md) voor meer informatie over de ondersteunde Android-beheermethoden. 

> [!NOTE]
> Omdat Google Mobile Services niet beschikbaar is in China, kunnen apparaten in China beheerd door Intune geen functies gebruiken waarvoor Google Mobile Services is vereist. Het gaat om de volgende functies: Google Play-mogelijkheden voor beveiliging, zoals apparaatbevestiging van SafetyNet, het beheren van apps vanuit de Google Play Store, Android Enterprise-mogelijkheden (zie deze [Google-documentatie](https://support.google.com/work/android/answer/6270910)). De app Intune-bedrijfsportal voor Android maakt daarnaast gebruik van Google Mobile Services om te communiceren met de Microsoft Intune-service. Omdat Google Play Services niet beschikbaar is in China, kan het tot acht uur duren voordat sommige taken zijn voltooid. Zie dit [artikel](../apps/manage-without-gms.md#limitations-of-intune-device-administrator-management-when-gms-is-unavailable) voor meer informatie.

### <a name="google-android-enterprise"></a>Google Android Enterprise 

Google biedt documentatie over de vereiste netwerkpoorten en namen van doelhosts in hun [Android Enterprise Bluebook](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf), onder de sectie **Firewall** van het document. 

### <a name="android-push-notification"></a>Pushmelding van Android

Intune maakt gebruik van Google Firebase Cloud Messaging (FCM) voor pushmeldingen om acties van apparaten en inchecken te activeren. Dit is vereist voor Android-apparaatbeheerder en Android Enterprise. Voor informatie over FCM-netwerkvereisten raadpleegt u de [FCM-poorten en uw firewall](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall) van Google.

## <a name="endpoint-analytics"></a>Eindpuntanalyse

Zie [Proxyconfiguratie voor eindpuntanalyse](../../analytics/troubleshoot.md#bkmk_endpoints) voor meer informatie over de vereiste eindpunten voor eindpuntanalyse.