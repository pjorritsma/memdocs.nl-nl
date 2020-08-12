---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: ca735cde1da5d563b9a7772fdaa55834e307312e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125939"
---
### <a name="server-connectivity-endpoints"></a>Server connectiviteit-eind punten

Het service verbindings punt moet met de volgende eind punten communiceren:

| Eindpunt  | Functie  |
|-----------|-----------|
| `https://aka.ms` | Wordt gebruikt om de service te vinden |
| `https://graph.windows.net` | Wordt gebruikt om automatisch instellingen op te halen, zoals CommercialId wanneer u uw hiërarchie koppelt aan Desktop Analytics (op Configuration Manager server functie). Zie [Configure the proxy for a site System server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)(Engelstalig) voor meer informatie. |
| `https://*.manage.microsoft.com` | Wordt gebruikt voor het synchroniseren van lidmaatschappen van Apparaatsets, implementatie plannen en de gereedheids status van apparaten met Desktop Analytics (alleen op Configuration Manager server functie). Zie [Configure the proxy for a site System server](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)(Engelstalig) voor meer informatie. |
| `https://dc.services.visualstudio.com` | Voor diagnostische gegevens van een on-premises service connector om inzicht te krijgen in de status van Cloud-verbonden services.<!--7541816--> |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>Gebruikers ervaring en eind punten van diagnostische onderdelen

Client apparaten moeten met de volgende eind punten communiceren:

| Eindpunt  | Functie  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Eind punt voor verbonden gebruikers ervaring en diagnostische onderdelen. Wordt gebruikt door apparaten met Windows 10, versie 1809 of hoger of versie 1803 met de cumulatieve update van 2018-09 of later geïnstalleerd. |
| `https://v10.events.data.microsoft.com` | Eind punt voor verbonden gebruikers ervaring en diagnostische onderdelen. Wordt gebruikt door apparaten met Windows 10, versie 1803 _zonder_ dat de cumulatieve update van 2018-09 is geïnstalleerd. |
| `https://v10.vortex-win.data.microsoft.com` | Eind punt voor verbonden gebruikers ervaring en diagnostische onderdelen. Wordt gebruikt door apparaten met Windows 10, versie 1709 of eerder. |
| `https://vortex-win.data.microsoft.com` | Eind punt voor verbonden gebruikers ervaring en diagnostische onderdelen. Gebruikt door apparaten met Windows 7 en Windows 8,1 |

### <a name="client-connectivity-endpoints"></a>Client connectiviteits eindpunten

Client apparaten moeten met de volgende eind punten communiceren:

| Index | Eindpunt  | Functie  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | Hiermee wordt de compatibiliteits update ingeschakeld voor het verzenden van gegevens naar micro soft. |
| 2 | `http://adl.windows.com` | Hiermee kan de compatibiliteits update de meest recente compatibiliteits gegevens van micro soft ontvangen. |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows Foutrapportage (wer)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vereist voor het bewaken van de implementatie status in Windows 10, versie 1803 of eerder. |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows Foutrapportage (wer)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vereist voor status rapporten van apparaten in Windows 10, versie 1809 of hoger. |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows Foutrapportage (wer)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vereist voor het bewaken van de implementatie status in Windows 10, versie 1809 of hoger. |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows Foutrapportage (wer)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vereist voor het bewaken van de implementatie status in Windows 10, versie 1809 of hoger. |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows Foutrapportage (wer)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vereist voor het bewaken van de implementatie status in Windows 10, versie 1809 of hoger. |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows Foutrapportage (wer)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vereist voor het bewaken van de implementatie status in Windows 10, versie 1809 of hoger. |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows Foutrapportage (wer)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vereist voor het bewaken van de implementatie status in Windows 10, versie 1809 of hoger. |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows Foutrapportage (wer)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Vereist voor het bewaken van de implementatie status in Windows 10, versie 1809 of hoger. |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [Online Crash Analysis (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Vereist voor status rapporten van apparaten in Windows 10, versie 1809 of hoger. |
| 12 | `https://oca.telemetry.microsoft.com`  | [Online Crash Analysis (OCA)](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Vereist voor het bewaken van de implementatie status in Windows 10, versie 1803 of eerder. |
| 13 | `https://login.live.com` | Vereist om een betrouwbaardere apparaat-id voor desktop Analytics te bieden. <br> <br>Als u Microsoft-account toegang door eind gebruikers wilt uitschakelen, gebruikt u de beleids instellingen in plaats van dit eind punt te blok keren. Zie [de Microsoft-account in de onderneming](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)voor meer informatie. |
| 14 | `https://v20.events.data.microsoft.com` | Eind punt voor verbonden gebruikers ervaring en diagnostische onderdelen. |
