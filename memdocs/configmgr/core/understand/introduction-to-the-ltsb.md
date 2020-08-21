---
title: Inleiding tot de LTSB
titleSuffix: Configuration Manager
description: Meer informatie over de lange termijn onderhouds vertakking van Configuration Manager.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1370c1bf80283ff30ad54378ad58ecd9a5d24d47
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699361"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-configuration-manager"></a>Inleiding tot de lange termijn onderhouds vertakking van Configuration Manager

*Van toepassing op: System Center Configuration Manager (onderhouds branche voor de lange termijn)*

De Long-term Servicing Branch (LTSB) van Configuration Manager is een afzonderlijke vertakking die is ontworpen als een installatie optie die beschikbaar is voor alle klanten. Het is echter de enige optie voor klanten die hun Software Assurance (SA) of gelijkwaardige abonnements rechten voor Configuration Manager laten vervallen.

Op basis van Configuration Manager versie 1606 heeft de LTSB verminderde functionaliteit in vergelijking met de huidige vertakking van Configuration Manager.

> [!TIP]   
> De Configuration Manager LTSB is niet gerelateerd aan het System Center Suite-onderhouds kanaal (LTSC). Zie [overzicht van de release opties van System Center](/system-center/ltsc-and-sac-overview)voor meer informatie.

## <a name="features-that-arent-available"></a>Functies die niet beschikbaar zijn

De huidige vertakking van Configuration Manager ondersteunt de volgende functionaliteit die niet beschikbaar is wanneer u de LTSB gebruikt:

- Updates in de console waarmee nieuwe functies en verbeteringen worden toegevoegd.
- Ondersteuning voor nieuw uitgebrachte besturings systemen voor gebruik als site servers en clients.
- On-premises MDM
- Het Windows 10-onderhouds dashboard en onderhouds plannen, inclusief ondersteuning voor recente versies van Windows 10.  
- Ondersteuning voor toekomstige releases van Windows Server en Windows 10 LTSB
- Asset Intelligence
- Clouddistributiepunten
- Exchange Online als Exchange-connector    

Hoewel ondersteuning voor deze functies niet beschikbaar is in de LTSB, blijven sommige functies zichtbaar in de Configuration Manager-console, maar kunnen ze niet worden geselecteerd of gebruikt.

Cloud integraties en functies die zijn opgenomen in Configuration Manager versie 1610 of hoger van de huidige branch, zijn niet beschikbaar voor de LTSB. Deze functies omvatten, maar zijn niet beperkt tot het volgende:<!--SCCMDocs#1823-->

- Co-beheer
- Desktop Analytics
- Cloudbeheergateway
- Integratie van Azure Active Directory
- Apps van de Microsoft Store voor bedrijven

## <a name="find-ltsb-documentation"></a>Documentatie voor LTSB zoeken

De LTSB is gebaseerd op de huidige branch versie 1606. Gebruik de [huidige branch-documentatie](../../index.yml)met aanvullende opmerkingen en beperkingen die specifiek zijn voor de LTSB. Deze voor behoud en beperkingen worden in de volgende artikelen aangeduid:

- [De LTSB installeren](install-the-ltsb.md)
- [De LTSB bijwerken naar de huidige vertakking](convert-to-current-branch.md)
- [Ondersteunde configuraties voor LTSB](supported-configurations-for-ltsb.md)
- [De LTSB van Configuration Manager beheren](manage-the-ltsb.md)

Wanneer u verwijst naar de huidige branch-documentatie voor de LTSB, zijn de details die van toepassing zijn op versie 1606 of eerder, ook van toepassing op de LTSB. Functies of Details die zijn geïntroduceerd in versie 1610 of hoger worden niet ondersteund door de LTSB.

## <a name="licensing-overview-for-the-ltsb"></a>Licentie overzicht voor de LTSB   

Klanten met actieve Software Assurance (SA) op Configuration Manager licenties, of met gelijkwaardige abonnements rechten vanaf 1 oktober 2016, hebben recht op het gebruik van de release van Configuration Manager van oktober 2016 versie 1606. Klanten met rechten voor het Configuration Manager op of na 1 oktober 2016, zullen tijdens de installatie twee gelicentieerde opties vinden: current branch en Long-term Servicing Branch (LTSB).

Klanten die over een permanente rechten beschikken voor System Center Configuration Manager of waarmee SA of het abonnement na 1 oktober vervalt, kunnen de versie van System Center Configuration Manager LTSB installeren die actueel is op het moment dat deze zich voordoet.

Zie voor meer informatie over deze licenties de [volledige voor waarden voor de producten die u aanschaft via micro soft Volume Licensing Program ma's](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).

Zie [Configuration Manager Licensing and branches](learn-more-editions.md)voor meer informatie over licenties voor Configuration Manager-filialen.

## <a name="next-steps"></a>Volgende stappen

Als u besluit dat de Configuration Manager LTSB de juiste vertakking voor uw omgeving is, [installeert u een nieuwe LTSB](install-the-ltsb.md#install-a-new-site) -site als onderdeel van een nieuwe hiërarchie, of [een upgrade van een System Center 2012 Configuration Manager-site](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager) en-hiërarchie.