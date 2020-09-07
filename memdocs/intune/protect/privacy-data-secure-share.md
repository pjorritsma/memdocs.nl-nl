---
title: Gegevens in Intune beveiligen en delen
titleSuffix: Microsoft Intune
description: Lees informatie over de beveiliging en het delen van persoonlijke gegevens in Intune.
keywords: privacy, data
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 68921fd6-5f50-456c-a3af-83d7bc4b134b
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fba72c89676d8974f5e7f9aac25d3365b69f61c7
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286251"
---
# <a name="data-security-and-sharing-in-intune"></a>Gegevens in Intune beveiligen en delen


## <a name="data-security"></a>Gegevens beveiligen

Microsoft Intune is een belangrijk onderdeel van de Microsoft Enterprise Mobility- en Security Suite-cloudservice. In navolging van de [gegevensbeheerstrategie](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) zijn alle cloudservices van Microsoft ontwikkeld met [Microsoft Privacy](https://www.microsoft.com/en-us/trustcenter/privacy)- en [Microsoft Security](https://www.microsoft.com/en-us/trustcenter/security/)-methodologieën.  

Microsoft Intune volgt dezelfde technische en organisatorische maatregelen die Microsoft Azure-serviceteams nemen voor de beveiliging tegen lekken.

Zie [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp) voor meer informatie.

### <a name="data-breach-reporting"></a>Rapportage van een datalek

Wanneer een CRSI (Customer-Reportable Security Incident) wordt geïdentificeerd, worden klanten hiervan op de hoogte gebracht. In dit proces wordt samen met het Microsoft 365-team melding gedaan van het lek aan de gebruikers van Microsoft 365 met Intune.

## <a name="data-sharing"></a>Gegevens delen

Wanneer bepaalde functies (zoals het Apple Device Enrollment Program) door tenantbeheerders worden ingeschakeld, wordt in Microsoft Intune toestemming van de beheerder verkregen voor het delen van gegevens met de juiste derden. In dergelijke gevallen kan Intune persoonlijke gegevens delen met:

- Derden die fungeren als Microsoft agent.
- Derden die niet fungeren als Microsoft agent, maar alleen wanneer tenantbeheerders hiervoor expliciet machtigingen geven voor Intune.

Alle derden die fungeren als Microsoft-agent zijn opgenomen in de [lijst toeleveranciers voor Online Services](https://aka.ms/Online_Serv_Subcontractor_List).

Het delen van gegevens met dergelijke entiteiten wordt gedaan ter ondersteuning van de klant en de technische ondersteuning, voor service-onderhoud en andere bewerkingen.

De persoonlijke gegevens van Intune die in de service van de derde partij aanwezig zijn, zijn onderhevig aan het contract van de tenant met de derde partij. Ook heeft Intune toestemming om de gegevens te verzenden naar de service van de derde partij.  

Raadpleeg de volgende artikelen voor informatie over gegevens die worden gedeeld met bepaalde derden:
- [Gegevens die Intune naar Apple verzendt](data-intune-sends-to-apple.md)
- [Gegevens die Intune naar Google verzendt](data-intune-sends-to-google.md)
- [Gegevens die Apple verzendt naar Intune](data-apple-sends-to-intune.md)
- [Gegevens die Google verzendt naar Intune](data-google-sends-to-intune.md)
- [Gegevens die Jamf Pro verzendt naar Intune](data-jamf-sends-to-intune.md)

### <a name="microsoft-endpoint-configuration-manager-data-sharing"></a>Gegevens delen met Microsoft Endpoint Configuration Manager

Microsoft Intune deelt geen gegevens met Configuration Manager. Configuration Manager is een on-premises product dat rechtstreeks door de klant wordt geïmplementeerd, beheerd en uitgevoerd. De diagnostische gegevens en gebruiksgegevens die door Configuration Manager worden verzameld, worden alleen gebruikt om de installatie-ervaring, kwaliteit en beveiliging van toekomstige releases te verbeteren.

Zie [Diagnostische gegevens en gebruiksgegevens voor Configuration Manager](/configmgr/core/plan-design/diagnostics/diagnostics-and-usage-data) voor meer informatie. 


## <a name="next-steps"></a>Volgende stappen

Ontdek hoe u persoonlijke gegevens in Intune kunt [weergeven en corrigeren](privacy-data-view-correct.md).