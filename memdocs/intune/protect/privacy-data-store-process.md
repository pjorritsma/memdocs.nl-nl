---
title: Opslag en verwerking van gegevens in Intune
titleSuffix: Microsoft Intune
description: Informatie over de opslag en verwerking van persoonlijke gegevens in Intune.
keywords: gegevens, privacy
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: edb07842-6a16-482e-8c1d-541a29e169a8
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c7c597a6d196ab5f8c3170cd5880682a280e73
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076060"
---
# <a name="data-storage-and-processing-in-intune"></a>Opslag en verwerking van gegevens in Intune

### <a name="storing-customer-data"></a>Klantgegevens opslaan

Nadat Intune [de gegevens heeft verzameld](privacy-data-collect.md), volgt Intune het standaardbeleid voor gegevensverwerking voor Microsoft 365 waarin staat aangegeven hoe klantgegevens worden opgeslagen en verwerkt. Zie [Opslag van uw Microsoft 365-klantgegevens](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations). Persoonsgegevens worden verwerkt binnen de gecontroleerde compliancegrens van de Intune-service volgens de technische veiligheidsmaatregelen die zijn gewaarborgd via [Microsoft OST (Voorwaarden voor Online Diensten)](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

### <a name="storage-locations"></a>Opslaglocaties

Microsoft biedt in veel regio's wereldwijd Intune-services aan. Intune respecteert de opslaglocaties die zijn gekozen door de beheerder voor klantgegevens.

Zie [Locaties van gegevenscentra](https://docs.microsoft.com/microsoft-365/enterprise/o365-data-locations?view=o365-worldwide#data-center-locations)voor meer informatie

### <a name="personal-data-retention"></a>Persoonlijke gegevens bewaren

Standaardbeleid van Microsoft 365-gegevensverwerking geeft aan hoe lang klantgegevens na verwijdering behouden blijven. Er zijn twee scenario's waarin klantgegevens worden verwijderd:

-**Actieve verwijdering**: De tenant heeft een actief abonnement en een gebruiker of beheerder verwijdert gegevens, of beheerders verwijderen een gebruiker.
-**Passieve verwijdering**: Het tenantabonnement is beëindigd.

Zie [Gegevensretentie, -verwijdering en -vernietiging in Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/microsoft-365-data-retention-deletion-and-destruction-overview?view=o365-worldwide) voor elk van de verwijderingsscenario's.  

Over het algemeen worden persoonsgegevens die door Intune zijn verzameld, binnen 30 dagen na verwijdering verwijderd. Auditlogboeken worden maximaal één jaar bewaard voor beveiligingsdoeleinden. 


## <a name="processing-personal-data"></a>Persoonlijke gegevens verwerken

Intune verwerkt persoonlijke gegevens conform ISO-gecertificeerde systemen. Zie [Service Trust Portal](https://www.microsoft.com/en-us/TrustCenter/stp) voor meer informatie.

### <a name="profiling-and-marketing"></a>Profilering en marketing

Microsoft Intune gebruikt geen persoonlijke gegevens die zijn verzameld als onderdeel van de service voor profilerings- of marketingdoeleinden. 

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe Intune persoonlijke gegevens [beveiligt en deelt](privacy-data-secure-share.md). 
