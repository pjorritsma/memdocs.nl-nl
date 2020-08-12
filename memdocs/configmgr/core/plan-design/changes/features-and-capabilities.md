---
title: Functies en mogelijkheden
titleSuffix: Configuration Manager
description: Meer informatie over de primaire beheer functies van Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 74b150b5a2157104b6a380489202fd309224a3bb
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129032"
---
# <a name="features-and-capabilities-of-configuration-manager"></a>Functies en mogelijkheden van Configuration Manager

*Van toepassing op: Configuration Manager (huidige vertakking)*

Dit artikel bevat een overzicht van de primaire beheer functies van Configuration Manager. Elke functie heeft zijn eigen vereisten en hoe u elk gebruikt, kan van invloed zijn op het ontwerp en de implementatie van uw Configuration Manager-hiërarchie. Als u bijvoorbeeld software-updates wilt implementeren op apparaten in uw hiërarchie, hebt u een site systeemrol van het software-update punt nodig.  

Zie voor [bereidingen voor Configuration Manager](../get-ready.md)voor meer informatie over het plannen en installeren van Configuration Manager om deze beheer mogelijkheden in uw omgeving te ondersteunen.  

## <a name="co-management"></a>Co-beheer

Co-beheer is een van de belangrijkste manieren om uw bestaande Configuration Manager-implementatie aan de Microsoft 365 Cloud te koppelen. Hiermee kunt u Windows 10-apparaten gelijktijdig beheren door gebruik te maken van zowel Configuration Manager als Microsoft Intune. Met co-beheer kunt u uw bestaande investering in Configuration Manager koppelen door nieuwe functionaliteit toe te voegen, zoals voorwaardelijke toegang. Zie [Wat is co-beheer](../../../comanage/overview.md)? voor meer informatie.

## <a name="desktop-analytics"></a>Desktop Analytics

Desktop Analytics is een Cloud service die kan worden geïntegreerd met Configuration Manager. De service biedt inzicht en intelligentie waarmee u meer weloverwogen beslissingen kunt nemen over de update gereedheids van uw Windows-clients. Gegevens uit uw organisatie worden gecombineerd met gegevens die zijn geaggregeerd van miljoenen apparaten die zijn verbonden met micro soft-Cloud Services. Zie [Wat is Desktop Analytics](../../../desktop-analytics/overview.md)? voor meer informatie.

## <a name="cloud-attached-management"></a>Aan cloud gekoppeld beheer

Gebruik functies als de cloudbeheergateway, clouddistributiepunten en Azure Active Directory om clients op internet te beheren.

Raadpleeg voor meer informatie de volgende artikelen:

- [Clients op internet beheren](../../clients/manage/manage-clients-internet.md)
- [Azure AD plannen](../security/plan-for-security.md#bkmk_planazuread)
- [Azure-services](../../servers/deploy/configure/azure-services-wizard.md)

## <a name="real-time-management"></a>Real-time beheer

Gebruik CMPivot om direct online apparaten te doorzoeken en vervolgens de gegevens te filteren en te groeperen op diepere inzichten. Gebruik ook de Configuration Manager-console voor het beheren en implementeren van Windows Power shell-scripts voor clients. Zie [CMPivot](../../servers/manage/cmpivot.md) en [Power shell-scripts maken en uitvoeren](../../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie.

## <a name="application-management"></a>Toepassingsbeheer

Helpt u bij het maken, beheren, implementeren en bewaken van toepassingen naar een bereik van verschillende apparaten die u beheert. Microsoft 365-Apps implementeren, bijwerken en beheren via de Configuration Manager-console. Daarnaast kan Configuration Manager worden geïntegreerd met de Microsoft Store voor bedrijven en onderwijs voor het leveren van Cloud-apps. Zie [Inleiding tot toepassings beheer](../../../apps/understand/introduction-to-application-management.md)voor meer informatie.

## <a name="os-deployment"></a>Besturingssysteemimplementatie

Een in-place upgrade van Windows 10 implementeren of installatie kopieën van besturings systemen vastleggen en implementeren. Implementatie van installatie kopieën kan gebruikmaken van PXE, multi cast of opstart bare media. Het kan ook helpen om bestaande apparaten opnieuw te implementeren met behulp van Windows auto pilot. Zie [Introduction to OS Deployment](../../../osd/understand/introduction-to-operating-system-deployment.md)(Engelstalig) voor meer informatie.  

## <a name="software-updates"></a>Software-updates

Software-updates in de organisatie beheren, implementeren en controleren. Integreer met Windows Delivery Optimization en andere peer-caching-technologieën om het netwerk gebruik te helpen beheren. Zie [Introduction to software updates](../../../sum/understand/software-updates-introduction.md)(Engelstalig) voor meer informatie.  

## <a name="company-resource-access"></a>Toegang tot bedrijfsbronnen

Hiermee kunt u gebruikers in uw organisatie toegang verlenen tot gegevens en toepassingen vanaf externe locaties. Deze functie omvat Wi-Fi-, VPN-, e-mail-en certificaat profielen. Zie [gegevens en site-infra structuur beveiligen](../../../protect/understand/protect-data-and-site-infrastructure.md)voor meer informatie.

## <a name="compliance-settings"></a>Instellingen voor naleving

Helpt u bij het beoordelen, bijhouden en herstellen van de configuratie naleving van client apparaten in de organisatie. Daarnaast kunt u nalevings instellingen gebruiken om een aantal functies en beveiligings instellingen te configureren op apparaten die u beheert. Zie apparaatcompatibiliteit [controleren](../../../compliance/understand/ensure-device-compliance.md)voor meer informatie.  

## <a name="endpoint-protection"></a>Endpoint Protection

Biedt beveiliging, antimalware en Windows Firewall beheer voor computers in uw organisatie. Dit gebied omvat het beheer en de integratie met de volgende functies van Windows Defender Suite:

- Windows Defender Antivirus
- Microsoft Defender Advanced Threat Protection
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Windows Defender Application Control
- Windows Defender Firewall

Zie [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)voor meer informatie.  

## <a name="inventory"></a>Inventaris

Helpt u bij het identificeren en bewaken van assets.

### <a name="hardware-inventory"></a>Hardware-inventaris

Verzamelt gedetailleerde informatie over de hardware van apparaten in uw organisatie. Zie [Inleiding op Hardware-inventarisatie](../../clients/manage/inventory/introduction-to-hardware-inventory.md)voor meer informatie.  

### <a name="software-inventory"></a>Software-inventaris

Verzamelt en rapporteert informatie over de bestanden die zijn opgeslagen op client computers in uw organisatie. Zie [Inleiding tot software-inventarisatie](../../clients/manage/inventory/introduction-to-software-inventory.md)voor meer informatie.  

### <a name="asset-intelligence"></a>Asset Intelligence

Voorziet in hulpprogram ma's voor het verzamelen van inventaris gegevens en het controleren van het gebruik van software licenties in uw organisatie. Zie [Inleiding tot Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)voor meer informatie.  

## <a name="on-premises-mobile-device-management"></a>On-premises Mobile Device Management

Registreert en beheert apparaten met behulp van de on-premises Configuration Manager-infra structuur met de beheer functionaliteit die is ingebouwd in de platformen. (Normaal beheer maakt gebruik van een afzonderlijk geïnstalleerde Configuration Manager-client.) Deze functie biedt momenteel ondersteuning voor het beheren van Windows 10 Enter prise-en Windows 10 Mobile-apparaten. Zie [mobiele apparaten beheren met on-premises infra structuur](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)voor meer informatie.  

## <a name="power-management"></a>Energiebeheer

Het energie verbruik van client computers in de organisatie beheren en bewaken. Configureer energiebeheer schema's en gebruik Wake-on-LAN voor onderhoud buiten kantoor uren. Zie [Introduction to Power Management](../../clients/manage/power/introduction-to-power-management.md)(Engelstalig) voor meer informatie.  

## <a name="remote-control"></a>Extern beheer

Voorziet in hulpprogram ma's voor het extern beheren van client computers vanuit de Configuration Manager-console. Zie [Inleiding tot beheer op afstand](../../clients/manage/remote-control/introduction-to-remote-control.md)voor meer informatie.  

## <a name="reporting"></a>Rapporten

Gebruik de geavanceerde rapportage mogelijkheden van SQL Server Reporting Services van de Configuration Manager-console. Deze functie biedt honderden standaard rapporten. Zie [Introduction to Reporting](../../servers/manage/introduction-to-reporting.md)(Engelstalig) voor meer informatie.  

## <a name="software-metering"></a>Softwarelicentiecontrole

Software gebruiks gegevens van Configuration Manager-clients bewaken en verzamelen. U kunt deze gegevens gebruiken om te bepalen of software wordt gebruikt nadat deze is geïnstalleerd. Zie [app-gebruik controleren met software meter](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)voor meer informatie.  
