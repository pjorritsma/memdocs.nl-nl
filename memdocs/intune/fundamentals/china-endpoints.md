---
title: Implementeren van China-netwerkeindpunten - Microsoft Intune
titleSuffix: ''
description: Controleer de China-eindpunten voor Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: b5551e537716ed12a0a5b5de19b747ffc7c4dcac
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347335"
---
# <a name="china-endpoints-for-microsoft-intune"></a>China-netwerkeindpunten voor Microsoft Intune

Op deze pagina worden de China-eindpunten vermeld die nodig zijn voor de proxy-instellingen in uw Intune-implementaties.

Als u apparaten wilt beheren die zich achter firewalls en proxyservers bevinden, moet u communicatie voor Intune inschakelen.

- De proxyserver moet zowel **HTTP (80)** als **HTTPS (443)** ondersteunen omdat Intune-clients beide protocollen gebruiken
- Voor bepaalde taken, zoals het downloaden van software en updates, is in Intune niet-geverifieerde proxyservertoegang vereist tot manage.microsoft.com

U kunt de instellingen voor proxyservers wijzigen op afzonderlijke clientcomputers. U kunt ook de instellingen voor groepsbeleid gebruiken om de instellingen te wijzigen voor alle clientcomputers die zich achter een bepaalde proxyserver bevinden.

Voor beheerde apparaten zijn configuraties vereist waarmee **alle gebruikers** via firewalls toegang krijgen tot services.

Zie [Registratie instellen voor Windows-apparaten](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration) voor meer informatie over de automatische registratie van Windows 10 en apparaatregistratie voor klanten in China.

De volgende tabel bevat de poorten en services waartoe de Intune-client toegang heeft:

|**Eindpunt**|**IP-adres**|
|---------------------|-----------|
|*.manage.microsoft.cn | 40.73.38.143<br>139.217.97.81<br>52.130.80.24<br>40.73.41.162<br>40.73.58.153<br>139.217.95.85 |


## <a name="intune-customer-designated-endpoints-in-china"></a>Door de klant aangewezen China-eindpunten voor Intune
- Azure-portal: https:\//portal.azure.cn/
- Office 365: https:\//portal.partner.microsoftonline.cn/
- Intune-bedrijfsportal: https:\//portal.manage.microsoftonline.cn/
- Microsoft Endpoint Manager-beheercentrum: https:\//endpoint.microsoftonline.cn/


## <a name="partner-service-endpoints"></a>Service-eindpunten van partners

Intune beheerd door 21Vianet is afhankelijk van de volgende service-eindpunten van partners:
- Azure AD Sync-service: https:\//syncservice.partner.microsoftonline.cn/DirectoryService.svc
- Evo-STS: https:\//login.chinacloudapi.cn/
- Azure AD Graph: https:\//graph.chinacloudapi.us
- MS Graph: https:\//microsoftgraph.chinacloudapi.cn
- ADRS: https:\//enterpriseregistration.partner.microsoftonline.cn

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over Intune beheerd door 21Vianet in China](china.md)

