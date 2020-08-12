---
title: Ondersteuning voor Windows 10
titleSuffix: Configuration Manager
description: Meer informatie over de Windows 10-versies die worden ondersteund als clients of voor OSD met Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6a30fc55fb4129b8ea3493b76fd6871a2a62f881
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126736"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Ondersteuning voor Windows 10 in Configuration Manager  

*Van toepassing op: Configuration Manager (huidige vertakking)*

Meer informatie over de Windows 10-versies die Configuration Manager ondersteunt, waaronder:

- [Windows 10 als Configuration Manager-client](#windows-10-as-a-client)
- [De Windows Assessment and Deployment Kit (ADK) voor Windows 10](#windows-10-adk)

> [!TIP]
> Windows Server bouwt voort als een client die hetzelfde is als de bijbehorende Windows 10-versie. Windows Server 2016 is bijvoorbeeld dezelfde build-versie als Windows 10 LTSB 2016, en Windows Server versie 1803 is dezelfde build-versie als Windows 10 versie 1803.
>
> Zie [ondersteunde besturings systemen voor Configuration Manager-site systeem servers](supported-operating-systems-for-site-system-servers.md#bkmk_core)voor meer informatie over Windows Server als een site systeem.

## <a name="windows-10-as-a-client"></a>Windows 10 als client

Configuration Manager probeert zo snel mogelijk ondersteuning te bieden als een client voor elke nieuwe Windows 10-versie nadat deze weer beschikbaar is. Omdat de producten afzonderlijke ontwikkelings-en release planningen hebben, is de ondersteuning die Configuration Manager biedt, afhankelijk van wanneer deze beschikbaar wordt.

Een Configuration Manager versie valt buiten de matrix nadat de [ondersteuning voor die versie](../../servers/manage/current-branch-versions-supported.md) eindigt. Net als bij de ondersteuning voor Windows 10-versies zoals Enter prise 2015 LTSB of 1511 wordt de matrix niet meer ondersteund.

- De nieuwste versie van Configuration Manager current branch ontvangt zowel beveiliging als essentiële updates, die oplossingen kunnen bevatten voor problemen met Windows 10-versies. Wanneer micro soft een nieuwe versie van Configuration Manager current branch uitbrengt, ontvangen eerdere versies alleen beveiligings updates. Zie [ondersteuning voor Configuration Manager huidige branch-versies](../../servers/manage/current-branch-versions-supported.md)voor meer informatie.  

    > [!NOTE]
    > De beste manier om op de hoogte te blijven van Windows 10 is om op de hoogte te blijven van Configuration Manager. Zie [Configuration Manager en Windows as a Service](../../understand/configuration-manager-and-windows-as-service.md)voor meer informatie.  

- Deze informatie is een aanvulling [op ondersteunde besturings systemen voor clients en apparaten](supported-operating-systems-for-clients-and-devices.md).  

- Als u de Long-term Servicing vertakking van Configuration Manager gebruikt, raadpleegt u [ondersteunde configuraties voor de langlopende onderhouds vertakking](../../understand/supported-configurations-for-ltsb.md).  

De volgende tabel geeft een lijst van de versies van Windows 10 die u kunt gebruiken als een client met verschillende versies van Configuration Manager.

| Windows 10-versie | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 | ConfigMgr 2006 |
|---------------------|-----|-----|-----|-----|-----|-----|
| **1709**<br>(10.0.16299)   <!--10/13/2020-->   | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![Niet ondersteund](media/Red_X.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/10/2022-->   | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) |
| **2004**<br>(10.0.19041)   <!--12/14/2021-->   | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) |

Alle momenteel ondersteunde versies van Configuration Manager huidige branch ondersteunen de volgende edities van Windows 10 LTSB/LTSC:

- **Enter prise 2015 LTSB** <!--10/14/2025-->
- **Enter prise 2016 LTSB** <!--10/13/2026-->
- **Enter prise LTSC 2019** <!--01/09/2029-->

Zie het overzicht van [Windows levenscyclus](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)voor meer informatie over Windows lifecycle.

| Sleutel |
|--|
| ![Ondersteund ](media/green_check.png)  =  **Supported** ondersteund  |
| ![Niet ondersteund ](media/Red_X.png)  =  **niet** ondersteund |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a>Opmerkingen voor Windows 10-client ondersteuning

- Ondersteuning voor semi-Annual-kanaal versies van Windows 10 omvat de volgende edities: Enter prise, Pro, Education en Pro education.  

- Vanaf versie 1906 ondersteunt Configuration Manager Windows 10 Pro voor werk station.

- Voor Windows 10, versie 1909, wordt de versie van de besturingssysteem implementatie media weer gegeven als 10.0.18362.418.

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a>Windows 10 op ARM64

Configuration Manager ondersteunt de-client op Windows 10 ARM64-apparaten. Implementatie van het besturings systeem wordt niet ondersteund.<!-- 1353704 -->

Vanaf versie 2002,<!--5954175--> het **alle Windows 10-platform (ARM64)** is beschikbaar in de lijst met ondersteunde versies van besturings systemen voor objecten met vereisten regels of toepasings lijsten.

> [!NOTE]
> Als u eerder het **Windows 10** -platform van het hoogste niveau hebt geselecteerd, wordt met deze actie automatisch zowel **alle Windows 10-(64-bits)** als **alle Windows 10 (32-bits)** geselecteerd. Dit nieuwe platform wordt niet automatisch geselecteerd. Als u **alle Windows 10 (ARM64)** wilt toevoegen, selecteert u deze hand matig in de lijst.

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a>Ondersteuning voor Windows Insider

Vanaf Configuration Manager versie 1906 kunt u Windows Insider-builds [bijwerken en onderhouden](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB) . Deze mogelijkheid kan worden geboden door onze klanten. Hoewel deze functionaliteit zou moeten werken, is de ondersteuning hiervoor het beste. Configuration Manager kan mogelijk geen hotfix uitgeven voor deze functionaliteit als deze niet meer werkt.  

Als u feedback wilt geven over Windows Insider, gebruikt u de [feedback hub](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback).

## <a name="windows-10-adk"></a>Windows 10 ADK

Wanneer u besturings systemen met Configuration Manager implementeert, is Windows ADK een vereiste externe afhankelijkheid. Raadpleeg voor meer informatie de volgende artikelen:

- [Vereisten voor de infrastructuur voor besturingssysteemimplementatie](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [Download Windows ADK voor Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > Vanaf Windows 10 versie 1809 is Windows PE een afzonderlijk installatie programma. Anders is er geen functioneel verschil.
    >
    > Zorg ervoor dat u de **Windows ADk voor Windows 10** en de **Windows PE-invoeg toepassing voor de ADk**downloadt.

De volgende tabel geeft een lijst van de versies van Windows 10 ADK die u kunt gebruiken met verschillende versies van Configuration Manager.

| Windows 10 ADK-versie  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 | ConfigMgr 2006 |
|--------------------|-----|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![Niet ondersteund](media/Red_X.png)   | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Achterwaarts compatibel](media/blue_compat.png) | ![Achterwaarts compatibel](media/blue_compat.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Achterwaarts compatibel](media/blue_compat.png) | ![Achterwaarts compatibel](media/blue_compat.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![Niet ondersteund](media/Red_X.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) | ![Achterwaarts compatibel](media/blue_compat.png) |
| **2004**<br>(10.1.19041) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Niet ondersteund](media/Red_X.png) | ![Ondersteund](media/green_check.png) | ![Ondersteund](media/green_check.png) |

|Sleutel|
|--|
| ![Ondersteund ](media/green_check.png)  =  **Supported** ondersteund <br/> In deze tabel wordt alleen de Windows ADK-ondersteuning weer gegeven ten opzichte van de versie van Configuration Manager. Micro soft raadt aan de Windows ADK te gebruiken die overeenkomt met de versie van Windows die u implementeert. Gebruik de meest recente versie van Windows ADK bij het implementeren van de nieuwste versie van Windows 10. De nieuwste versie van Windows ADK kan ondersteuning bieden voor de implementatie van oudere versies van besturings systemen, zoals Windows 8,1.<!-- SCCMDocs issue 1229 --> Zie voor meer informatie over de ondersteuning van Windows ADK-onderdelen [DISM-ondersteunde platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) en [USMT-vereisten](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Achterwaarts compatibel ](media/blue_compat.png)   =  **achterwaarts compatibel** <br/> Deze combi natie wordt niet getest, maar zou moeten werken. Er worden bekende problemen of voor behoud gedocumenteerd. |
| ![Niet ondersteund ](media/Red_X.png)  =  **niet** ondersteund |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a>Windows 10 ADK-ondersteunings opmerkingen

- Configuration Manager ondersteunt alleen x86-en amd64-onderdelen van Windows 10 ADK. Het biedt momenteel geen ondersteuning voor ARM-of ARM64-onderdelen.

- Windows Server-builds hebben dezelfde Windows ADK-vereiste als de bijbehorende Windows 10-versie. Windows Server 2016 is bijvoorbeeld dezelfde build-versie als Windows 10 LTSB 2016.
