---
title: Upgradegereedheid
titleSuffix: Configuration Manager
description: Integreer Upgradegereedheid met Configuration Manager om toegang te krijgen tot de compatibiliteits gegevens voor Windows 10 en de doel apparaten voor upgrades of herstel.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/31/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 6d9bd7aabb36895160ba8aa740c28155105e196a
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693400"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Upgradegereedheid integreren met Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!Important]  
> De Windows Analytics-service wordt vanaf 31 januari 2020 buiten gebruik gesteld. Zie [KB 4521815: Windows Analytics is buiten gebruik gesteld op 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement)voor meer informatie.
>
> Desktop Analytics is de ontwikkeling van Windows Analytics. Zie [Wat is Desktop Analytics](../../../desktop-analytics/overview.md)? voor meer informatie.

Als uw Configuration Manager-site verbinding heeft met Upgradegereedheid, moet u deze verwijderen en clients opnieuw configureren.

## <a name="remove-upgrade-readiness-connection"></a><a name="bkmk_remove"></a> Upgradegereedheid verbinding verwijderen

1. Open de Configuration Manager-console als gebruiker met de rol **volledige beheerder** .

1. Ga naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** .

1. De Windows Analytics-service verwijderen.

## <a name="reconfigure-clients"></a>Clients opnieuw configureren

### <a name="unenroll-devices"></a>Inschrijving van apparaten ongedaan maken

Controleer eerst de standaard instellingen van de site of eventuele aangepaste client apparaatinstellingen in de **Windows Analytics** -groep. Schakel bijvoorbeeld de volgende instelling uit: **Windows-telemetrie-instellingen beheren met Configuration Manager**.

> [!IMPORTANT]
> Als u van plan bent bureau blad Analytics te gebruiken, worden de instellingen voor diagnostische gegevens van Windows op clients geconfigureerd. Gebruik de wizard verbinding met Azure-Services om deze instellingen te configureren voor gebruik met Desktop Analytics. Zie [How to connect Configuration Manager with Desktop Analytics](../../../desktop-analytics/connect-configmgr.md)(Engelstalig) voor meer informatie.

Verwijder op geregistreerde apparaten de waarde CommercialID uit de volgende Windows-register sleutels:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuratie van Windows diagnostische gegevens

Als u niet wilt dat uw apparaten diagnostische gegevens gaan verzenden:

- Windows 10: Stel het niveau van diagnostische gegevens in op **beveiliging**
- Windows 7 SP1 of 8,1: de **opt-in-sleutel voor commerciële gegevens** uitschakelen

Stel deze waarden in met een van de volgende methoden:

- Groeps beleid, in **computer configuratie**  >  **Beheersjablonen**van  >  **Windows Components**  >  **gegevens verzameling en Preview-versies** van Windows-onderdelen
- Beheer van mobiele apparaten (MDM), zoals [Microsoft intune](/intune/device-restrictions-windows-10#reporting-and-telemetry)

Zie [Diagnostische gegevens van Windows in uw organisatie configureren](/windows/privacy/configure-windows-diagnostic-data-in-your-organization) voor meer informatie.

> [!NOTE]  
> Wanneer u deze wijzigingen toepast, stoppen apparaten direct met het verzenden van diagnostische gegevens. Het kan 24-48 uur duren voordat micro soft het verwerken van inzichten voor uw werk ruimte stopt. Micro soft verwijdert deze gegevens binnen 30 dagen of minder in de Cloud Services.

<!--
Upgrade Readiness is a part of [Windows Analytics](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). It allows you to assess and analyze the readiness of devices in your environment for an upgrade to Windows 10. Integrate Upgrade Readiness with Configuration Manager to access client upgrade compatibility data in the Configuration Manager console. Then use this data to create collections, and target devices for upgrade or remediation.



## Configure clients

Upgrade Readiness relies on Windows Analytics data. In order for Upgrade Readiness to receive sufficient data, configure the following prerequisites:

- Configure all clients with a *commercial ID key*  

- Configure Windows 10 clients for Windows Analytics to report at least basic level data  

- For clients running Windows 7 or 8.1:  

    - Install the updates as described in [Get started with Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started)  

    - Enable Windows Analytics client settings  

Configure these settings using Configuration Manager client settings. For more information, see [Use Windows Analytics](monitor-windows-analytics.md).

> [!NOTE]  
> Deploying the correct prerequisite updates and configuring client settings should be sufficient in most environments. If you encounter issues with Upgrade Readiness not receiving data from devices in your environment, then some of these issues may be addressed by using the [Upgrade Readiness deployment script](/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## Connect Configuration Manager to Upgrade Readiness

Use the [Azure services wizard](../../servers/deploy/configure/azure-services-wizard.md) to simplify the process of configuring Azure services you use with Configuration Manager. To connect Configuration Manager with Upgrade Readiness, create an Azure Active Directory (Azure AD) app registration of type *Web app / API* in the [Azure portal](https://portal.azure.com). For more information about how to create an app registration, see [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration). 

In the Azure portal, give following permissions to your newly registered web app:
- *Reader* permissions to the resource group that contains the Log Analytics workspace with your Upgrade Readiness data
- *Contributor* permissions to the Log Analytics workspace that hosts your Upgrade Readiness data

The Azure services wizard uses this app registration to allow Configuration Manager to communicate securely with Azure AD and connect your infrastructure to your Upgrade Readiness data.

> [!IMPORTANT]  
> Grant permissions to the app itself, not to an Azure AD user identity. It's the registered app that accesses the data on behalf of your Configuration Manager infrastructure. To grant the permissions, search for the name of the app registration in the **Add users** area when assigning the permission. 
> 
> This process is the same as when providing Configuration Manager with permissions to Log Analytics. These steps must be completed before the app registration is imported into Configuration Manager with the *Azure services wizard*.
> 
> For more information, see [Connect Configuration Manager to Log Analytics](/azure/log-analytics/log-analytics-sccm).


### Use the Azure Wizard to create the connection

Follow the instructions in [Configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) to create a connection to Upgrade Readiness by importing the web app registration you created above. 

If the web app import was successful and the correct permissions are assigned in the Azure portal, the *Configuration* page pre-populates the following values:   
-  Azure subscriptions  
-  Azure resource group  
-  Windows Analytics workspace  

More than one resource group or workspace is available in the following circumstances: 
- If the registered Azure AD web app has *Contributor* permissions on more than one resource group   
- If the selected resource group has more than one Log Analytics workspace  



## View and use Upgrade Readiness information in Configuration Manager

After you've integrated Upgrade Readiness with Configuration Manager, you can view the analysis of your clients' upgrade readiness.

1. In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Upgrade Readiness** node.  

2. Review the data. For example:  
    - The upgrade readiness state  
    - The percent of Windows devices that are reporting data  

3. Filter the dashboard to view data for devices in specific collections.  

4. View the devices in a particular readiness state, and then create a dynamic collection for those devices. Then use that collection to upgrade those devices, or take action to remediate devices that are in a blocked state.  

> [!Note]  
> The site synchronizes data with Upgrade Readiness once a week. To manually trigger synchronization:
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  
> 2. Select the Upgrade Readiness connection from the list.  
> 3. In the ribbon, select the option to synchronize.  



## Next steps

- [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)  
- [Create a task sequence to upgrade an OS](../../../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)  
- [Create phased deployments](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)