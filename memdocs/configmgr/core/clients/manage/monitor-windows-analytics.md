---
title: Clients controleren met Windows Analytics
titleSuffix: Configuration Manager
description: Windows Analytics is een reeks oplossingen waarmee u waardevol inzicht kunt krijgen in de huidige status van uw omgeving.
ms.date: 01/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2cb35b7cf14b14f4a200fd2caa0547f0e2a9bb16
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692754"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Gebruik Windows Analytics met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> De Windows Analytics-service wordt vanaf 31 januari 2020 buiten gebruik gesteld. Zie [KB 4521815: Windows Analytics is buiten gebruik gesteld op 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement)voor meer informatie.
>
> Desktop Analytics is de ontwikkeling van Windows Analytics. Zie [Wat is Desktop Analytics](../../../desktop-analytics/overview.md)? voor meer informatie.

Als uw Configuration Manager-site verbinding heeft met Upgradegereedheid, moet u deze verwijderen en clients opnieuw configureren. Zie [Upgradegereedheid-verbinding verwijderen](upgrade-readiness.md#bkmk_remove)voor meer informatie.

<!--
[Windows Analytics](/windows/deployment/update/windows-analytics-overview) is a set of solutions that allow you to gain insight into the current state of your environment. Windows devices in your environment report data to Microsoft, which you can access and analyze through these solutions. For example, connect [Upgrade Readiness](upgrade-readiness.md) to Configuration Manager to directly access the data in the **Monitoring** workspace of the Configuration Manager console.

The data used by Windows Analytics isn't transferred directly to the Configuration Manager site server. Client computers send data to the Windows cloud service. This service then transfers the relevant data to Windows Analytics solutions hosted in one of your organization's workspaces. Configuration Manager then directs you to relevant data in the web portal with in-context links. It can also directly display data that's part of solutions that you connect to Configuration Manager.

> [!Important]  
> Configuration Manager reports diagnostics and usage data to Microsoft. This data is separate from Windows Analytics data. For more information, see [Diagnostics and usage data](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  



## Configure Clients to report data to Windows Analytics

For client devices to report data to Windows Analytics, configure them with a *commercial ID key*. This key is Azure Log Analytics workspace that hosts your Windows Analytics data. Also configure devices to report data at a level appropriate for the specific solutions that you want to use. 

### Configure Windows Analytics client settings
To configure Windows Analytics: 
1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.  
2. In the ribbon, select **Create Custom Device Client Settings**.  
3. Add the **Windows Analytics** group to this custom device client settings policy.  

For more information on creating custom device client settings, see [How to configure client settings](../deploy/configure-client-settings.md).

Select the **Windows Analytics** settings tab, and configure the following settings:  

#### Manage Windows telemetry settings with Configuration Manager
Configure this setting to **Yes** to configure Windows diagnostic data settings on Windows clients.   

#### Commercial ID key
The commercial ID key maps information from devices you manage to the Log Analytics workspace that hosts your organization's Windows Analytics data. If you've already configured a commercial ID key for use with Upgrade Readiness, use that ID. If you don't yet have a commercial ID key, see [Copy your commercial ID key](/windows/deployment/update/windows-analytics-get-started#copy-your-commercial-id-key).

#### Windows 10 telemetry
For more information, see [Configure Windows diagnostic data in your organization](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels).

> [!Note]  
> You can also set the Windows 10 data collection level to **Enhanced (Limited)**. This setting enables you to gain actionable insight about devices in your environment without devices reporting all of the data in the **Enhanced** level with Windows 10 version 1709 or later. The Enhanced (Limited) level includes metrics from the Basic level, as well as a subset of data collected from the Enhanced level relevant to Windows Analytics.

#### Windows 8.1 and earlier telemetry   
For more information, see [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965).

#### Enable Windows 8.1 and earlier Internet Explorer data collection
On devices running Windows 8.1 or earlier, Internet Explorer can collect data about web apps. This data can allow Upgrade Readiness to detect web application incompatibilities that could prevent a smooth upgrade to Windows 10. Enable Internet Explorer data collection based on the internet zone. For more information about internet zones, see [About URL Security Zones](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537183\(v=vs.85\)).



## Use Upgrade Readiness to identify Windows 10 compatibility issues

Upgrade Readiness enables you to analyze device readiness and compatibility with Windows 10. This assessment allows for smoother upgrades. After connecting Configuration Manager to Upgrade Readiness, access this client upgrade compatibility data directly in the Configuration Manager console. Then target devices for upgrade or remediation from the device list.

For more information and details on how to configure and connect to Upgrade Readiness, see [Upgrade Readiness](upgrade-readiness.md).



## Use Windows Analytics to identify gaps in Windows Information Protection Policies

You can configure Windows 10 version 1703 and later devices with a [Windows Information Protection](/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) policy. They report diagnostic data on applications that access corporate data in your environment but aren't included in the policy application rules. Users may need these applications to stay productive, but WIP blocks the users' access. This information is useful to maintain your Windows Information Protection policies in Configuration Manager. 

-->