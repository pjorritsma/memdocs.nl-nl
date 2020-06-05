---
title: Netwerkeindpunten voor US Government-implementaties - Microsoft Intune
titleSuffix: ''
description: Lees de tekst over US Government-eindpunten voor Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/30/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5f6682cb-5fcd-4018-b7f7-71768ad3152e
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1574e07ca58debaef5bbc134a86d76aa21778a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347241"
---
# <a name="us-government-endpoints-for-microsoft-intune"></a>US Government-eindpunten voor Microsoft Intune

Op deze pagina worden de US Government-eindpunten vermeld die nodig zijn voor de proxy-instellingen in uw Intune-implementaties.

Als u apparaten wilt beheren die zich achter firewalls en proxyservers bevinden, moet u communicatie voor Intune inschakelen.

- De proxyserver moet zowel **HTTP (80)** als **HTTPS (443)** ondersteunen omdat Intune-clients beide protocollen gebruiken
- Voor bepaalde taken, zoals het downloaden van software en updates, is in Intune niet-geverifieerde proxyservertoegang vereist tot manage.microsoft.com

U kunt de instellingen voor proxyservers wijzigen op afzonderlijke clientcomputers. U kunt ook de instellingen voor groepsbeleid gebruiken om de instellingen te wijzigen voor alle clientcomputers die zich achter een bepaalde proxyserver bevinden.

Voor beheerde apparaten zijn configuraties vereist waarmee **alle gebruikers** via firewalls toegang krijgen tot services.

Zie [Registratie instellen voor Windows-apparaten](../enrollment/windows-enroll.md#windows-10-auto-enrollment-and-device-registration) voor meer informatie over de automatische registratie van Windows 10 en apparaatregistratie voor Amerikaanse overheidsklanten.

De volgende tabel bevat de poorten en services waartoe de Intune-client toegang heeft:

|**Eindpunt**|**IP-adres**|
|---------------------|-----------|
|*.manage.microsoft.us | 52.243.26.209 <br> 52.247.173.11 <br> 52.227.183.12 <br>52.227.180.205 <br> 52.227.178.107 <br> 13.72.185.168 <br> 52.227.173.179 <br> 52.227.175.242 <br> 13.72.39.209 <br> 52.243.26.209 <br> 52.247.173.11 |
| enterpriseregistration.microsoftonline.us | 13.72.188.239 <br> 13.72.55.179 |

## <a name="us-government-customer-designated-endpoints"></a>Eindpunten die aan US Government-klanten zijn toegewezen:
- Azure Portal: https:\//portal.azure.us/ 
- Office 365: https:\//portal.office365.us/ 
- Intune-bedrijfsportal: https:\//portal.manage.microsoft.us/ 
- Microsoft Endpoint Manager-beheercentrum: https:\//endpoint.microsoft.us/

## <a name="partner-service-endpoints-that-intune-depends-on"></a>Service-eindpunten voor partners waarvan Intune afhankelijk is:
- AAD Sync Services: https:\//syncservice.gov.us.microsoftonline.com/DirectoryService.svc
- Evo STS: https:\//login.microsoftonline.us
- Directoryproxy: https:\//directoryproxy.microsoftazure.us/DirectoryProxy.svc
- AAD Graph: https:\//directory.microsoftazure.us en https:\//graph.microsoftazure.us
- MS Graph: https:\//graph.microsoft.us
- ADRS: https:\//enterpriseregistration.microsoftonline.us

[!INCLUDE [Intune notices](../includes/windows-push-notification-services.md)]

[!INCLUDE [Intune notices](../includes/apple-device-network-information.md)]

## <a name="next-steps"></a>Volgende stappen
[Netwerkeindpunten voor Microsoft Intune](intune-endpoints.md)

