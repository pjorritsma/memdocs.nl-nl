---
title: Gereed voor Windows
titleSuffix: Configuration Manager
description: Over de buiten gebruiks telling van de kant-en-klare website van Windows
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 75dd74e3c1019c9819b44a0ffa8936eeb9eee366
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268348"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Veelgestelde vragen over het voorbereiden van moderne Desktop-pensioen

<!-- placeholder -->

## <a name="general"></a>Algemeen

### <a name="what-happened-to-the-ready-for-windows-website"></a>Wat is er gebeurd met de kant-en-klare website van Windows?

Veel klanten hebben problemen met het ophalen en blijven actueel van Windows 10 en Office 365 ProPlus. De primaire uitdaging is het testen van toepassingen, omdat dit proces doorgaans hand matig is. Het is tijdrovender dat IT-beheerders en toepassings eigenaren voortdurend bestaande toepassingen analyseren en vervolgens problemen oplossen die zich voordoen.

De lijst met kant-en- *klare bureau blad* -software oplossingen die worden ondersteund en in gebruik zijn op commerciële apparaten met Windows 10 en Office 365 ProPlus. De Directory helpt IT-beheerders die de nieuwste versies van Windows 10 en Office 365 voor hun implementaties overwegen.

Feedback van IT-managers is dat ze deze inzichten willen integreren met de hulpprogram ma's die ze al gebruiken om hun implementatie plannen te plannen. Gebruik [Desktop Analytics](https://aka.ms/dadocs) en [Office 365 ProPlus gereedheids functies](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) in Configuration Manager om uw Windows 10-en Office 365 ProPlus-upgrade projecten te plannen en te beheren. 

> [!Note]
> Vanaf 21 april 2020, wordt de naam van Office 365 ProPlus gewijzigd in **Microsoft 365 apps voor bedrijven**. Zie [name wijzigen voor Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change)voor meer informatie. Mogelijk ziet u nog steeds verwijzingen naar de oude naam in de Configuration Manager-console en de ondersteunende documentatie terwijl de-console wordt bijgewerkt.

### <a name="what-is-desktop-analytics"></a>Wat is Desktop Analytics?

[Desktop Analytics](https://aka.ms/dadocs) is een Cloud service die kan worden geïntegreerd met Configuration Manager. De service biedt inzicht en intelligentie waarmee u beter gefundeerde beslissingen kunt nemen over de update gereedheids van uw Windows-eind punten. Het combineert de gegevens die specifiek zijn voor uw organisatie met geaggregeerde inzichten van de miljoenen Windows-apparaten die zijn verbonden met de Cloud Services van micro soft.

-    Krijg een uitgebreid overzicht van de eind punten, toepassingen en stuur Programma's onder beheer in uw organisatie.

-    Bepaal de compatibiliteit van toepassingen en stuur Programma's met de nieuwste updates voor Windows-onderdelen. Krijg aanbevelingen voor het beperken van bekende problemen, evenals geavanceerde inzichten voor line-of-Business-Apps.

-    Gebruik kunst matige intelligentie (AI) van de micro soft-Cloud om de set pilot-apparaten te optimaliseren die uw hele omgeving afgeven.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Waarom moet ik Desktop Analytics gebruiken voor mijn Windows-implementatie plannen?

Desktop Analytics biedt de volgende voor delen:

-    **Hardware-en software-inventaris**: inventarisatie van belang rijke factoren zoals apps en versies van Windows.

-    **Pilot-identificatie**: identificatie van de kleinste set apparaten die de breedste dekking van factoren bieden. Het richt zich op de factoren die het belangrijkst zijn voor een pilot van Windows-upgrades en-updates. Als u er zeker van wilt zijn dat de pilot meer succes biedt, kunt u sneller en veiliger door gaan met grote implementaties in de productie omgeving.

-    **Probleem identificatie**: het gebruik van geaggregeerde markt gegevens en gegevens uit uw omgeving, de service voor spelt mogelijke problemen met het verkrijgen en blijven gebruiken van Windows. Vervolgens worden mogelijke oplossingen voorgesteld.

-    **Configuration Manager-integratie**: de IT-Cloud biedt uw bestaande on-premises infra structuur. Gebruik deze gegevens en analyse om Windows op uw apparaten te implementeren en te beheren.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>Wat heeft de status *gereed voor Windows* in Desktop Analytics?

De **status van de goed keuring** is gebaseerd op informatie van commerciële apparaten die gegevens delen met micro soft. De status is geïntegreerd met ondersteunings instructies van software leveranciers.

Desktop Analytics biedt de acceptatie status voor elke versie van een Asset die is gevonden op commerciële apparaten. Deze status bevat geen gegevens van consumenten apparaten of apparaten die geen gegevens delen. De status kan niet representatief zijn voor het acceptatie tempo van alle Windows 10-apparaten.

Zie [Compatibility Assessment](compat-assessment.md)(Engelstalig) voor meer informatie.

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Welke assets krijgt de status *gereed voor Windows* in Desktop Analytics? 

Activa hebben de status *gereed voor Windows* in Desktop Analytics als:

-    De software provider declareert ondersteuning voor de oplossing.
-    Klanten hebben het geïmplementeerd op een groot aantal commerciële Windows 10-apparaten die gegevens delen met micro soft.
-    De activa zijn relevant voor commerciële gebruikers.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Welke extra inzichten krijg ik in Desktop Analytics?

Desktop Analytics biedt een inventarisatie van de [apparaten en hun geïnstalleerde apps](about-assets.md), evenals [Geavanceerde inzichten](compat-assessment.md#advanced-insights) voor line-of-Business-Apps. 

## <a name="software-providers"></a>Software providers

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>Kan ik nog steeds mijn software oplossing in Desktop Analytics vermelden?

Publiceer een ondersteunings verklaring die uw product werkt met 32-bits of 64-bits Windows 10 of Office 365 ProPlus. Neem contact op met uw micro soft-contact persoon als u uw oplossingen in Desktop Analytics wilt presen teren.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Hoe kan ik mijn oplossingen voor delen?

Duizenden IT-beheerders beheren miljoenen apparaten met Configuration Manager en desktop Analytics. Ze gebruiken deze hulpprogram ma's om hun organisaties in vertrouwen te plannen en bij te werken naar de nieuwste versie van Windows 10 en Office 365 ProPlus. Ze gebruiken ze ook om aankoop beslissingen te nemen voor software oplossingen.

Micro soft integreert ondersteunings verklaringen van software leveranciers met de acceptatie gegevens die ze van commerciële apparaten ontvangen. Organisaties over de hele wereld gebruiken deze gegevens vervolgens in Desktop Analytics en Office Readiness-hulpprogram ma's. 

Neem contact op met uw micro soft-contact persoon als uw ondersteunings instructies niet goed zijn gekoppeld aan assets.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>Kan ik gedetailleerde metrische gegevens over prestaties op mijn assets bekijken?

Evalueer de prestaties van uw oplossingen met rapporten over de status en de metrische gegevens via het ontwikkelaars centrum: 

- [Windows Store](https://docs.microsoft.com/windows/uwp/publish/health-report)
- [Bureaublad](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
- [Office-invoegtoepassingen](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>Hoe kan ik compatibele assets ontwikkelen voor Windows 10 en Office 365 ProPlus?

Zorg ervoor dat uw desktop toepassingen nu compatibel zijn en blijf in de toekomst compatibel met Windows 10. Zie [toepassings compatibiliteit voor ontwikkel aars](https://developer.microsoft.com/windows/desktop/app-compatibility)voor meer informatie.

Als u oplossingen voor Office 365 ProPlus ontwikkelt, raadpleegt u [Aanbevolen procedures voor het ontwikkelen van com-, VSTO-en VBA-invoeg toepassingen in Office](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).
