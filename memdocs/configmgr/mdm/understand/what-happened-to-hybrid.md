---
title: Wat is er gebeurd met hybride MDM?
titleSuffix: Configuration Manager
description: Meer informatie over de afschaffing van hybride Mobile Device Management (MDM) in Configuration Manager
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d07a014cdcb3f371a90028ec09be3c0c939b8424
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721813"
---
# <a name="what-happened-to-hybrid-mdm"></a>Wat is er gebeurd met hybride MDM?

*Van toepassing op: Configuration Manager (huidige vertakking)*

> [!WARNING]
> Micro soft heeft het Hybrid MDM-service-aanbod vanaf 1 september 2019 buiten gebruik gesteld. Alle andere hybride MDM-apparaten ontvangen geen beleid, apps of beveiligings updates.

## <a name="remove-hybrid-mdm"></a>Hybride MDM verwijderen

Als uw Configuration Manager-site een Microsoft Intune-abonnement had, moet u het verwijderen.

1. Ga in de Configuration Manager-console naar de werk ruimte **beheer** . Vouw **Cloud Services**uit en selecteer het knoop punt **Microsoft intune abonnement** . Verwijder uw bestaande intune-abonnement.

1. Selecteer in de **Wizard Microsoft intune abonnement verwijderen**de optie om **Microsoft Intune abonnement van Configuration Manager te verwijderen**en klik vervolgens op **volgende**.

1. Voltooi de wizard.

## <a name="deprecation-announcement"></a>Aankondiging van afschaffing

De volgende opmerking is de oorspronkelijke aankondiging van de afschaffing:

> [!NOTE]  
> Vanaf 14 augustus 2018 is hybride Mobile Device Management een [afgeschafte functie](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Vanaf de 1902-release van de intune-service, die aan het einde van februari 2019 werd verwacht, kunnen nieuwe klanten geen nieuwe hybride verbinding maken.
> <!--Intune feature 2683117-->  
> Sinds de Lance ring op Azure is een jaar geleden honderden nieuwe door de klant aangevraagde en toonaangevende service mogelijkheden toegevoegd aan intune. Het biedt nu veel meer mogelijkheden dan die worden aangeboden via Hybrid Mobile Device Management (MDM). InTune in Azure biedt een meer geïntegreerde, gestroomlijnde administratieve ervaring voor uw zakelijke mobiliteits behoeften.
>
> Als gevolg hiervan kiezen de meeste klanten intune op Azure via hybride MDM. Het aantal klanten dat hybride MDM gebruikt, blijft dalen naarmate er meer klanten worden verplaatst naar de Cloud. Daarom zal micro soft op 1 september 2019 het hybride MDM-service-aanbod buiten gebruik stellen.
>
> Deze wijziging heeft geen invloed op on-premises Configuration Manager of [co-beheer voor Windows 10-apparaten](../../comanage/overview.md). Als u niet zeker weet of u hybride MDM gebruikt, gaat u naar de werk ruimte **beheer** van de Configuration Manager-console, vouwt u **Cloud Services**uit en selecteert u **Microsoft intune abonnementen**. Als u een Microsoft Intune abonnement hebt ingesteld, wordt uw Tenant geconfigureerd voor hybride MDM.
>
> **Wat betekent dit voor mij?**
>
> - Micro soft zal uw hybride MDM-gebruik voor het volgende jaar ondersteunen. De functie blijft belang rijke fouten oplossingen ontvangen. Micro soft biedt ondersteuning voor de bestaande functionaliteit van nieuwe versies van besturings systemen, zoals inschrijving op iOS 12. Er zijn geen nieuwe functies voor hybride MDM.  
>
> - Als u vóór het einde van de hybride MDM-aanbieding naar intune migreert in azure, mag dit geen invloed hebben op de eind gebruiker.  
>
> - Op 1 september 2019 zullen alle andere hybride MDM-apparaten geen beleid, apps of beveiligings updates meer ontvangen.  
>
> - Licentie verlening blijft hetzelfde. InTune op Azure-licenties zijn opgenomen in hybride MDM.  
>
> - De functie on-premises MDM in Configuration Manager is niet afgeschaft. Vanaf Configuration Manager versie 1810 kunt u een on-premises MDM zonder intune-verbinding gebruiken. Zie voor meer informatie [een intune-verbinding is niet langer vereist voor nieuwe on-premises MDM-implementaties](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm).
>
> - De functie voor on-premises voorwaardelijke toegang van Configuration Manager is ook afgeschaft met hybride MDM. Als u voorwaardelijke toegang gebruikt op apparaten die worden beheerd met de Configuration Manager-client, moet u ervoor zorgen dat deze zijn beveiligd voordat u migreert.
>     1. Beleid voor voorwaardelijke toegang instellen in azure
>     2. Nalevings beleid instellen in de intune-Portal
>     3. Hybride migratie volt ooien en de MDM-instantie instellen op intune
>     4. Co-beheer inschakelen
>     5. De werk belasting van het nalevings beleid voor co-beheer verplaatsen naar intune
>
>     Zie [voorwaardelijke toegang met co-beheer](../../comanage/quickstart-conditional-access.md)voor meer informatie.
>
> **Wat moet ik doen om me voor te bereiden op deze wijziging?**
>
> - Begin met het plannen van de migratie voor MDM vanuit de Configuration Manager-console naar Azure. Veel klanten, waaronder micro soft IT, hebben dit proces door lopen. Zie deze [micro soft](https://aka.ms/Intune_MSFT)-casestudy voor meer informatie.  
>
> - Neem contact op met uw partner of FastTrack voor hulp. [FastTrack voor Microsoft 365](https://aka.ms/hybrid_fasttrack) kan helpen bij de migratie van hybride MDM naar intune op Azure.
>
> Zie [het blog bericht intune-ondersteuning](https://aka.ms/hybrid_notification)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

Zie de volgende artikelen voor meer informatie over ondersteunde functies voor het beheren van MDM-apparaten:

- [Wat is Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)
- [Wat is on-premises MDM?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Apparaatbeheer met Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
