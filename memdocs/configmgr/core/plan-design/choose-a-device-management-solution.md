---
title: Een oplossing voor apparaatbeheer kiezen
titleSuffix: Configuration Manager
description: Meer informatie over de oplossingen die door micro soft worden geboden voor het beheren van Pc's, servers en apparaten.
ms.date: 01/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877345e64045530193a4cdd735cdd399235b90c7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700262"
---
# <a name="choose-a-device-management-solution"></a>Een oplossing voor apparaatbeheer kiezen

Micro soft biedt verschillende oplossingen voor het beheren van Pc's, servers en apparaten. Deze oplossingen zijn beschikbaar op locatie, op basis van de Cloud, of een combi natie van beide. Kies de oplossing die het beste past bij de zakelijke vereisten van uw organisatie. Baseer uw beslissing op de platformen die u wilt beheren en de beheer functionaliteit die u nodig hebt.

## <a name="overview"></a>Overzicht

Er zijn verschillende micro soft-oplossingen die in verschillende scenario's het beste kunnen worden gebruikt. U hoeft slechts één te kiezen.

- Voor een kleine organisatie is een hulp programma zoals het Windows-beheer centrum een geweldig probleem.
- Ongeveer 75% van de IT-organisaties gebruiken Configuration Manager om hun apparaten te beheren.
- Microsoft Azure biedt verschillende oplossingen vanuit de Cloud of on-premises met Azure Stack die voornamelijk doel server beheer zijn.
- Microsoft Intune biedt Cloud beheer van-clients.
- U kunt Configuration Manager en intune combi neren met co-beheer.

Gebruik de volgende tabel om deze beheer technologieën te vergelijken:

|  | Alleen cloud | Cloud gekoppeld | On-premises | Ontkoppeld |
|---------|---------|---------|---------|---------|
| **Hyper-V-host** | Niet van toepassing | -Azure Stack<br/> -Windows-beheer centrum<br/> -Virtual Machine Manager | -Azure Stack<br/> -Windows-beheer centrum<br/> -Virtual Machine Manager | -Azure Stack<br/> -Windows-beheer centrum<br/> -Virtual Machine Manager |
| **Windows Server** | -Azure-beheer<br/> -Configuration Manager | -Azure-beheer<br/> -Configuration Manager | -Azure-beheer<br/> -Configuration Manager | Configuration Manager |
| **Linux-server** | Azure-beheer | Azure-beheer | Azure-beheer |  |
| **Windows 10** | -InTune<br/> -Configuration Manager | -InTune<br/> -Configuration Manager | -InTune<br/> -Configuration Manager | Configuration Manager |
| **Windows 7 of 8,1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Windows Virtual Desktop** | Configuration Manager | Niet van toepassing | Niet van toepassing | Niet van toepassing |

Raadpleeg voor meer informatie de volgende artikelen:

- [Wat is Azure Stack?](/azure-stack/operator/azure-stack-overview)
- [Wat is Windows-beheer centrum?](/windows-server/manage/windows-admin-center/understand/what-is)
- [Wat is Virtual Machine Manager?](/system-center/vmm/overview)
- [Azure-beheer producten](/azure/)
- [Wat is Windows Virtual Desktop?](/azure/virtual-desktop/overview)

Ga naar de volgende sectie voor meer informatie over de Configuration Manager-en intune-oplossingen.

## <a name="client-management"></a>Clientbeheer

In deze sectie worden de volgende vier oplossingen voor client beheer vergeleken:

- [Configuration Manager-client](#bkmk_sccm)
- [On-premises Mobile Device Management (MDM) met Configuration Manager](#bkmk_opmdm)
- [Co-beheer met Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

U kunt deze oplossingen zelfstandig of in combi natie met elkaar gebruiken. Gebruik bijvoorbeeld de aanpak op basis van een client om de computers en servers in uw organisatie te beheren en gebruik Daarnaast co-beheer voor het beheren van op internet gebaseerde laptops. Door benaderingen op deze manier te combi neren, kunt u al uw behoeften voor Apparaatbeheer bedekken.  

Er zijn ook twee tabellen die de beheer oplossingen vergelijken met de volgende factoren:

- [Vergelijken met ondersteunde platforms](#bkmk_comp1)
- [Vergelijken op beheer functionaliteit](#bkmk_comp2)

### <a name="configuration-manager-client"></a><a name="bkmk_sccm"></a> Configuration Manager-client  

Voor deze optie moet de Configuration Manager-client op apparaten zijn geïnstalleerd. Het biedt de meeste functies voor het beheren van Pc's, servers en andere apparaten in uw omgeving.

Zie [client installatie methoden](../clients/deploy/plan/client-installation-methods.md)voor meer informatie.  

### <a name="on-premises-mdm"></a><a name="bkmk_opmdm"></a> On-premises MDM  

Deze optie maakt gebruik van de mogelijkheden voor Apparaatbeheer die zijn ingebouwd in Windows 10. Hoewel het niet zo volledig werkt als op client gebaseerd beheer, biedt on-premises MDM een lichtere aanraak benadering voor beheer. Het maakt gebruik van on-premises Configuration Manager resources voor het beheren van apparaten.  

Zie [mobiele apparaten beheren met on-premises infra structuur](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)voor meer informatie.  

### <a name="co-management-with-microsoft-intune"></a><a name="bkmk_comanage"></a> Co-beheer met Microsoft Intune

Co-beheer is een van de belangrijkste manieren om uw bestaande Configuration Manager-implementatie aan de Microsoft 365 Cloud te koppelen. Hiermee kunt u Windows 10-apparaten gelijktijdig beheren door gebruik te maken van zowel Configuration Manager als Microsoft Intune. Met co-beheer kunt u uw bestaande investering in Configuration Manager koppelen door nieuwe functionaliteit toe te voegen.

Zie [Wat is co-beheer?](../../comanage/overview.md) voor meer informatie.  

### <a name="microsoft-exchange"></a><a name="bkmk_exchange"></a> Micro soft Exchange  

Deze optie maakt gebruik van de Exchange Server-connector om meerdere Exchange-servers te verbinden met Configuration Manager. Het centraliseert het beheer van apparaten die verbinding kunnen maken met Exchange ActiveSync. U kunt Exchange Mobile Device Management-functies configureren via de Configuration Manager-console. Voor beelden van functies zijn het wissen van externe apparaten en het besturings element instellingen voor meerdere Exchange-servers.

Zie [mobiele apparaten beheren met Configuration Manager en Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)voor meer informatie.  

### <a name="compare-solutions-by-supported-platforms"></a><a name="bkmk_comp1"></a> Oplossingen vergelijken met ondersteunde platforms  

|Platform|Configuration Manager-client|On-premises MDM|Configuration Manager met Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Ja| Ja |
|iOS| | |Ja| Ja |
|Mac OS X|Ja| |Ja| Ja |
|Windows 10|Ja|Ja|Ja| Ja |
|Windows 10 Mobile| |Ja|Ja| Ja |
|Windows (vorige versies)|Ja| |Ja|  |
|Windows Server|Ja| |Ja|  |
|Windows Embedded|Ja| | |  |

Raadpleeg de volgende artikelen voor een volledige lijst met ondersteunde platforms:

- [Ondersteunde besturings systemen voor clients en apparaten voor Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)
- [Door intune ondersteunde configuraties](/intune/supported-devices-browsers)

Micro soft raadt aan om intune te gebruiken voor het beheren van mobiele apparaten met Android, iOS en Windows 10. Zie [Wat is Microsoft intune?](/intune/what-is-intune)voor meer informatie.

### <a name="compare-solutions-by-management-functionality"></a><a name="bkmk_comp2"></a> Oplossingen vergelijken op basis van de beheer functionaliteit  

|Beheer functionaliteit|Configuration Manager-client|On-premises MDM|Configuration Manager met Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Wederzijdse verificatie op basis van een certificaat|Ja|Ja| |
|Clientinstallatie|Ja| | |
|Ondersteuning via Internet|Ja| | |
|Detectie|Ja| |Ja|
|Hardware-inventaris|Ja|Ja|Ja|
|Software-inventaris|Ja| |Ja|
|Instellingen|Ja|Ja|Ja|
|Software-implementatie|Ja|Ja| |
|Beheer van software-updates|Ja| | |
|Besturingssysteemimplementatie|Ja| | |
|Configuration Manager blok keren|Ja|Ja| |
|Van Exchange Server (en Configuration Manager) in quarantaine plaatsen en blok keren| | |Ja|
|Wissen op afstand| |Ja|Ja|