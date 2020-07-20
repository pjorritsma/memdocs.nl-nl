---
title: Door Intune beheerd via 21Vianet in China
titleSuffix: ''
description: Door Intune beheerd via 21Vianet in China.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/07/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: ''
ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c4e567c7812f53a7497f368ded47d72640443f6
ms.sourcegitcommit: 678104677ad36b789630befdc5e0f1efc572c14b
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/08/2020
ms.locfileid: "86137389"
---
# <a name="intune-operated-by-21vianet-in-china"></a>Door Intune beheerd via 21Vianet in China  

Intune beheerd door 21Vianet is ontworpen om te voldoen aan veilige, betrouwbare en schaalbare cloudservices in China. Intune als een service is gebaseerd op Microsoft Azure. Microsoft Azure beheerd door 21Vianet is een fysiek gescheiden exemplaar van cloudservices die zich in China bevinden. Het wordt onafhankelijk beheerd en uitgevoerd door 21Vianet. Deze service wordt aangestuurd door technologie die Microsoft in licentie heeft gegeven aan 21Vianet.

Microsoft beheert de service zelf niet. 21Vianet beheert de levering van de service en voert de service uit. 21Vianet is een provider van online datacentrumservices in China. Het bedrijf biedt hosting, beheerde netwerkservices en infrastructuurservices met cloud-computing. 21Vianet gebruikt Microsoft-technologieën in licentie en beheert lokale datacentrums, zodat u de Intune-service kunt gebruiken terwijl uw gegevens in China bewaard blijven. 21Vianet biedt ook uw abonnements-, facturerings- en ondersteuningsservices.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## <a name="feature-differences-in-intune-operated-by-21vianet"></a>Functieverschillen in Intune beheerd door 21Vianet

Omdat de services in China worden beheerd door een partner vanuit China, zijn er enkele functieverschillen met Intune. 

- Intune beheerd door 21Vianet ondersteunt alleen zelfstandige implementaties. Ondersteuning voor co-beheer met System Center Configuration Manager is momenteel in ontwikkeling.
- Migraties van openbare clouds naar onafhankelijke clouds worden niet ondersteund. Klanten die willen overstappen naar Intune beheerd door 21Vianet, moeten handmatig worden gemigreerd.
- De functie voor het koppelen van tenants (het synchroniseren van apparaten met Intune zonder inschrijving in de cloudconsole) wordt momenteel niet ondersteund.
- Afgeleide referenties worden niet ondersteund met Intune beheerd door 21Vianet.
- Intune beheerd door 21Vianet biedt geen ondersteuning voor de Intune-agent en biedt daarom geen ondersteuning voor het beheer van verouderde pc's.
- Het beheer van Windows 10 wordt ondersteund met behulp van het moderne MDM-kanaal.
- Intune beheerd door 21Vianet biedt geen ondersteuning voor de on-premises Exchange connector.
- De functies van Windows Autopilot en Business Store zijn momenteel niet beschikbaar.
- Omdat Google Mobile Services niet beschikbaar is in China, kunnen klanten in Intune beheerd door 21Vianet geen functies gebruiken waarvoor Google Mobile Services is vereist. Het gaat om de volgende functies:
  - Google Play Protect mogelijkheden, zoals SafetyNet-apparaatbeveiliging.
  - Apps beheren vanuit de Google Play Store.
  - Android-bedrijfsmogelijkheden. Zie deze [Google-documentatie](https://support.google.com/work/android/answer/6270910?hl=en) voor meer informatie.
- De app Intune-bedrijfsportal voor Android maakt gebruik van Google Mobile Services om te communiceren met de Microsoft Intune-service. Omdat Google Play Services niet beschikbaar is in China, kan het tot acht uur duren voordat sommige taken zijn voltooid. Zie dit [artikel](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable) voor meer informatie. 
- De klantervaring met Intune (Bedrijfsportal-app) kan verschillen in China om lokale regelgeving na te volgen en verbeterde functionaliteit te bieden.
- Begrenzing is niet beschikbaar.
- De beschikbaarheid van Mobile Application Management (MAM) is afhankelijk van de beschikbaarheid van deze apps in de Volksrepubliek China.

## <a name="you-control-customer-data"></a>U beheert klantgegevens

In Microsoft Azure, Intune, Office 365 en Power BI beheerd door 21Vianet, hebt u volledige controle over uw gegevens:
- U weet waar klantgegevens zich bevinden.
- U beheert de toegang tot uw klantgegevens.
- U beheert uw klantgegevens als u de service verlaat.
- U hebt beheeropties voor de beveiliging van uw klantgegevens.

Met Microsoft Azure, Intune, Office 365 en Power BI beheerd door 21Vianet, bent u de eigenaar van uw gegevens:
- 21Vianet maakt geen gebruik van klantgegevens voor reclamedoeleinden.
- U bepaalt wie toegang heeft tot uw klantgegevens.
- We gebruiken logische isolatie om de gegevens van elke klant te scheiden.
- We bieden eenvoudige, transparante beleidsregels voor gegevensgebruik en krijgen onafhankelijke controles.
- Onze onderaannemers zijn contractueel verplicht om aan onze vereisten voor privacy te voldoen.

## <a name="data-subject-requests"></a>Aanvragen voor gegevens

De rol Tenant Administrator voor Intune beheerd door 21Vianet kan op de volgende manieren gegevens van personen opvragen:

- Met behulp van het Azure Active Directory-beheercentrum kan een Tenant Administrator een betrokkene permanent verwijderen uit Azure Active Directory en gerelateerde services. Zie [Azure Data Subject Requests - Delete](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-5-delete) (Azure-gegevensaanvragen - verwijderen) voor meer informatie
- Door het systeem gegenereerde logboeken voor Microsoft-services die door 21Vianet worden beheerd, kunnen worden geëxporteerd door Tenant Administrators met Data Log Export. Zie [Azure Data Subject Requests - Export](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-azure?view=o365-worldwide#step-6-export) (Azure-gegevensaanvragen - exporteren) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Meer informatie over door Intune ondersteunde configuraties](supported-devices-browsers.md)