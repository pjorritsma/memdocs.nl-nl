---
title: Asset Intelligence vereisten
titleSuffix: Configuration Manager
description: De vereisten voor het Asset Intelligence in Configuration Manager ophalen.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a7f87336c35c236a9e07d531469d65958d5d14e0
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906589"
---
# <a name="prerequisites-for-asset-intelligence-in-configuration-manager"></a>Vereisten voor het Asset Intelligence in Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Asset Intelligence in Configuration Manager heeft externe afhankelijkheden en afhankelijkheden binnen het product.  

## <a name="dependencies-external-to-configuration-manager"></a>Afhankelijkheden extern aan Configuration Manager  
 De volgende tabel bevat de afhankelijkheden voor Asset Intelligence die extern zijn voor Configuration Manager.  

|Afhankelijkheid|Meer informatie|  
|----------------|----------------------|  
|Controle van vereisten voor geslaagde aanmeldingsgebeurtenissen|Vier Asset Intelligence-rapporten bevatten gegevens die zijn verzameld uit de Windows-beveiligingslogboeken op clientcomputers. Als de beveiligingslogboeken niet zo zijn geconfigureerd dat alle geslaagde aanmeldingsgebeurtenissen worden geregistreerd, bevatten deze rapporten geen gegevens, ook niet als de juiste rapportageklasse voor hardware-inventarisatie is ingeschakeld.<br /><br /> De volgende Asset Intelligence-rapporten zijn afhankelijk van verzamelde gegevens uit het Windows-beveiligingslogboek:<br /><br /> -Hardware 03A-primaire computer gebruikers<br />-Hardware 03B-computers voor een specifieke primaire console gebruiker<br />-Hardwarematige 04A-gedeelde computers (meerdere gebruikers)<br />-Hardware 05A-console gebruikers op een specifieke computer<br /><br /> Als u de clientagent voor hardware-inventarisatie wilt inschakelen om te inventariseren welke gegevens vereist zijn ter ondersteuning van deze rapporten, moet u eerst de instellingen voor het Windows-beveiligingslogboek op clients wijzigen zodat alle geslaagde aanmeldingsgebeurtenissen worden geregistreerd. Vervolgens schakelt u de rapportageklasse **SMS_SystemConsoleUser** voor hardware-inventarisatie in. Zie [Enable auditing of success logon events](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents)voor meer informatie over het wijzigen van instellingen voor het beveiligingslogboek om alle geslaagde aanmeldingsgebeurtenissen te registreren.|  

> [!NOTE]  
>  In de **SMS_SystemConsoleUser** -rapportageklasse voor hardware-inventarisatie worden gegevens van geslaagde aanmeldingsgebeurtenissen alleen voor de afgelopen negentig dagen van het beveiligingslogboek bewaard, ongeacht de lengte van het logboek. Als het beveiligingslogboek minder dan negentig dagen aan gegevens bevat, wordt het hele logboek gelezen.  

## <a name="dependencies-internal-to-configuration-manager"></a>Afhankelijkheden intern aan Configuration Manager  
 De volgende tabel bevat de afhankelijkheden voor Asset Intelligence die intern zijn voor Configuration Manager.  

|Afhankelijkheid|Meer informatie|  
|----------------|----------------------|  
|Vereisten voor clientagents|De Asset Intelligence-rapporten zijn afhankelijk van clientgegevens die worden verkregen via clienthardware- en software-inventarisrapporten. U kunt de benodigde gegevens voor alle Asset Intelligence-rapporten ontvangen als de volgende clientagents zijn ingeschakeld:<br /><br /> -Client agent voor hardware-inventaris<br />-Client agent voor software meter|  
|Afhankelijkheden voor clientagent voor hardware-inventaris|Als u vereiste inventarisatiegegevens voor enkele Asset Intelligence-rapporten wilt verzamelen, moet de clientagent voor hardware-inventaris zijn ingeschakeld. Bovendien moeten bepaalde rapportageklassen voor hardware-inventarisatie, waarvan Asset Intelligence-rapporten afhankelijk zijn, ingeschakeld zijn op primaire siteservercomputers.<br /><br /> Zie [Hardware-inventarisatie uitbreiden](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)voor meer informatie over het inschakelen van de client agent voor hardware-inventarisatie.|  
|Afhankelijkheden voor clientagent voor softwaremeter|Een aantal Asset Intelligence-softwarerapporten is voor gegevens afhankelijk van de clientagent voor softwaremeter Zie [app-gebruik controleren met software meter](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)voor meer informatie over het inschakelen van de client agent voor software meter.<br /><br /> De volgende Asset Intelligence-rapporten zijn voor het leveren van gegevens afhankelijk van de clientagent voor softwaremeter:<br /><br /> -Software-07A-recent gebruikte uitvoer bare bestanden op aantal computers<br />-Software 07B-computers die recent een opgegeven uitvoerbaar bestand hebben gebruikt<br />-Software-07C-recent gebruikte uitvoer bare bestanden op een specifieke computer<br />-Software-08A-recent gebruikte uitvoer bare bestanden op aantal gebruikers<br />-Software 08B-gebruikers die recent een opgegeven uitvoerbaar bestand hebben gebruikt<br />-Software-08C-recent gebruikte uitvoer bare bestanden door een opgegeven gebruiker|  
|Vereisten voor Asset Intelligence-rapportageklassen voor hardware-inventarisatie|Asset Intelligence rapporten in Configuration Manager zijn afhankelijk van specifieke rapportage klassen voor hardware-inventarisatie. Tot de rapportageklassen voor hardware-inventarisatie zijn ingeschakeld en clients hardware-inventaris op basis van deze klassen hebben gerapporteerd, bevatten de bijbehorende Asset Intelligence-rapporten geen gegevens. U kunt de volgende rapportageklassen voor hardware-inventarisatie inschakelen ter ondersteuning van rapportagevereisten voor Asset Intelligence:<br /><br /> -SMS_SystemConsoleUsage<sup>1</sup><br />-SMS_SystemConsoleUser<sup>1</sup><br />-SMS_InstalledSoftware<br />-SMS_AutoStartSoftware<br />-SMS_BrowserHelperObject<br />-Win32_USBDevice<br />-SMS_InstalledExecutable<br />-SMS_SoftwareShortcut<br />-SoftwareLicensingService<br />-SoftwareLicensingProduct<br />-SMS_SoftwareTag<br /><br /> <sup>1</sup> Standaard zijn de Asset Intelligence-rapportageklassen voor hardware-inventarisatie **SMS_SystemConsoleUsage** en **SMS_SystemConsoleUser** ingeschakeld.<br /><br /> U kunt de Asset Intelligence-rapportage klassen voor hardware-inventarisatie bewerken in de Configuration Manager-console, in de werk ruimte **activa en naleving** , wanneer u op het knoop punt **Asset Intelligence** klikt. Zie de sectie [enable Asset Intelligence Hardware Inventory Reporting branches](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) in het onderwerp [Asset Intelligence configureren](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md) voor meer informatie.|  
|Reporting Services-punt|De sitesysteemrol Reporting Services-punt moet zijn geïnstalleerd om software-updaterapporten te kunnen weergeven. Zie [Configuring Reporting](../../../servers/manage/configuring-reporting.md)(Engelstalig configureren) voor meer informatie over het maken van een Reporting Services-punt.|  
