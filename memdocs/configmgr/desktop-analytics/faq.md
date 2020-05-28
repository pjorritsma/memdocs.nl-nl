---
title: Veelgestelde vragen over desktop Analytics
titleSuffix: Configuration Manager
description: Veelgestelde vragen over desktop Analytics.
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: d1f18c135f200b2a9e40b970871c73a0d98893a2
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429822"
---
# <a name="desktop-analytics-faq"></a>Veelgestelde vragen over Desktop Analytics

## <a name="prerequisites"></a>Vereisten

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a>Kan ik analyse in de Cloud gebruiken met apparaten die door intune worden beheerd?

Niet vandaag, maar zie de aankondiging van micro soft Ignite 2019 op inzichten op basis van het [beheer van apparaten](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions). Deze geplande oplossing is een opvolger van Apparaatstatus en Upgradegereedheid.

De meeste klanten die kunnen profiteren van de werk stroom voor desktop Analytics, gebruiken Configuration Manager om Windows te implementeren. We weten dat intune-klanten graag meer inzicht hebben in de analyse gegevens en we werken aan manieren om inzichten te delen met hen.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Het is meer dan 72 uur en de portal verwerkt nog steeds gegevens, wat dan nu?

Wanneer u Desktop Analytics voor het eerst instelt, worden de rapporten in Configuration Manager en de Desktop Analytics-Portal mogelijk niet meteen weer gegeven. Het kan 2-3 dagen duren voordat de gegevens zijn verwerkt door de service. Als er meer dan 72 uur is en de portal nog steeds gegevens verwerkt, voert u de volgende stappen uit:

- Gebruik het [dash board verbindings status](monitor-connection-health.md)om te controleren of de actieve apparaten op de juiste wijze zijn geconfigureerd. Dit dash board wordt niet in realtime bijgewerkt.
- Zorg ervoor dat apparaten diagnostische gegevens naar de Desktop Analytics-service verzenden. Zie voor meer informatie [delen van gegevens inschakelen](enable-data-sharing.md).
- Richt [Azure AD-toepassingen](troubleshooting.md#bkmk_AzureADApps) in op uw Azure AD.
- Controleer de apparaten die u in de afgelopen zeven dagen aan uw organisatie hebt gekoppeld. Ga in de [Desktop Analytics-Portal](https://aka.ms/desktopanalytics)naar het deel venster **verbonden services** . **Apparaten registreren**selecteren en **recente gegevens weer geven**

  > [!IMPORTANT]
  > De optie Desktop Analytics om **recente gegevens weer te geven** , is afgeschaft. Deze actie wordt verwijderd in een toekomstige versie van de Desktop Analytics-service. Zie [afgeschafte functies](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)voor meer informatie.<!--7080949-->  

[Neem contact op met micro soft ondersteuning](https://support.microsoft.com/hub/4343728/support-for-business)als apparaten correct zijn geconfigureerd en u nog steeds geen gegevens in uw werk ruimte ziet.

## <a name="connect-configuration-manager"></a>Verbinding maken met Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>Kan ik het doel of extra verzamelingen wijzigen?

Ja, gebruik het volgende proces:

- Ga in de Configuration Manager-console naar de werk ruimte **beheer** , vouw **Cloud Services**uit en selecteer het knoop punt **Azure-Services** . Open de eigenschappen voor de vermelding die aan uw Desktop Analytics-service is gekoppeld.

- Wijzig op het tabblad **verbinding met bureau blad Analytics** de **doel verzameling** of beheer de extra verzamelingen.

<!-- 7130169 -->
> [!Note]
> Voeg niet meer dan 20 verzamelingen toe aan de lijst met extra verzamelingen. Wees voorzichtig met het totale aantal apparaten in elke verzameling. Neem altijd uw [wereld wijde pilot op en sluit verzamelingen](deploy-pilot.md#bkmk_GlobalPilot)uit.  

> [!IMPORTANT]  
> Configuration Manager maakt gebruik van een instellingen beleid voor het configureren van apparaten in de doel verzameling. Dit beleid bevat de instellingen voor diagnostische gegevens om apparaten in staat te stellen gegevens naar micro soft te verzenden. Als u de doel verzameling wijzigt, wordt het instellingen beleid op apparaten die niet meer in de doel verzameling zijn, niet meer ongedaan gemaakt. Als u niet wilt dat uw apparaten diagnostische gegevens blijven verzenden, [configureert u de apparaten opnieuw](account-close.md#reconfigure-clients).

## <a name="windows-upgrade"></a>Windows-upgrade

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Kan ik een upgrade uitvoeren voor Windows en de architectuur wijzigen?

Desktop Analytics is ontworpen voor het beste ondersteunen van in-place upgrades. In-place Upgrades bieden geen ondersteuning voor migraties van een 32-bits-naar 64-bits architectuur. Als u computers in dit scenario wilt migreren, gebruikt u het vernieuwings scenario. Desktop Analytics Insights is nog steeds waardevol in dit scenario, maar u kunt upgrade-specifieke richt lijnen negeren.

Zie [een bestaande computer vernieuwen met een nieuwe versie van Windows](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)voor meer informatie.

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Kan ik overschakelen van BIOS naar UEFI bij het upgraden van Windows?

Ja. Zie [conversie van BIOS naar UEFI tijdens een in-place upgrade](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu)voor meer informatie.

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Kan ik Desktop Analytics gebruiken met Windows 10 LTSC?

Desktop Analytics biedt geen ondersteuning voor LTSC-apparaten (Long-term Servicing Channel) van Windows 10. Zie [Windows as a Service Overview](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)(Engelstalig) voor meer informatie.

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Kan ik de hoeveelheid tijd verminderen die nodig is voor het vernieuwen van gegevens in mijn bureau blad Analytics Portal?

Er zijn twee typen gegevens in de Desktop Analytics-portal: beheerders gegevens en diagnostische gegevens. Als u de beheerders gegevens op aanvraag wilt vernieuwen, opent u de vervolg keuze van de gegevens valuta en selecteert u **wijzigingen Toep assen**. Met deze actie wordt direct een eenmalige vernieuwing geactiveerd van wijzigingen in wachtende beheerders in uw werk ruimten. De wijzigingen worden door gegeven en zijn binnen 15-60 minuten algemeen beschikbaar. De timing is afhankelijk van de grootte van uw werk ruimte en het bereik van de in behandeling zijnde wijzigingen. U kunt Maxi maal zes keer binnen een periode van 24 uur een gegevens vernieuwing op aanvraag aanvragen.

Alle gegevens worden eenmaal per dag automatisch bijgewerkt, zelfs als u geen gegevens vernieuwing op aanvraag aanvraagt. Er is geen manier om een vernieuwing op aanvraag van diagnostische gegevens te activeren. Zie [Data latentie](troubleshooting.md#data-latency)voor meer informatie over de verschillende typen gegevens in Desktop Analytics.

## <a name="privacy"></a>Privacy

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Kan Desktop Analytics worden gebruikt zonder rechtstreekse client verbinding met de micro soft Gegevensbeheer-service?

Nee, de volledige service wordt mogelijk gemaakt door Diagnostische gegevens van Windows, waarvoor deze rechtstreekse connectiviteit vereist is voor apparaten.

### <a name="can-i-choose-the-data-center-location"></a>Kan ik de locatie van het Data Center kiezen?

Voor Azure Log Analytics: Ja, wanneer u Desktop Analytics instelt en de Log Analytics-werk ruimte maakt.

Voor de micro soft Gegevensbeheer-service en Analytics Azure Storage: Nee, deze twee services worden gehost in de Verenigde Staten.

### <a name="where-is-my-organizations-data-stored"></a>Waar worden de gegevens van mijn organisatie opgeslagen?

Windows diagnostische gegevens van uw computers zijn versleuteld, verzonden naar en verwerkt door door micro soft beheerde beveiligde data centers die zich in de Verenigde Staten bevinden. Micro soft biedt de analyse van de gegevens die betrekking hebben op het bureau blad Analytics door de oplossing voor desktop Analytics in de Azure Portal. Desktop Analytics wordt ondersteund in de meeste regio's waar [log Analytics beschikbaar is](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all). Als u een internationale Azure-regio selecteert, worden uw diagnostische gegevens nog steeds verzonden naar en verwerkt in de beveiligde data centers van micro soft in de Verenigde Staten.

## <a name="existing-windows-analytics-customers"></a>Bestaande Windows Analytics-klanten

> [!Important]  
> De Windows Analytics-service wordt vanaf 31 januari 2020 buiten gebruik gesteld.
>
> Zie [KB 4521815: Windows Analytics is buiten gebruik gesteld op 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement)voor meer informatie.

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>Kan ik Updatenaleving gebruiken in combi natie met Desktop Analytics?

Ja. Als u [Updatenaleving](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) in het Azure Portal vandaag gebruikt, kunt u dit nu nog verder doen en na januari 2020.

Zie [KB 4521815: Windows Analytics is buiten gebruik gesteld op 31 januari 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement)voor meer informatie.

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Zijn er Windows Analytics-functies die niet beschikbaar zijn in Desktop Analytics?

<!-- 3616924 -->
Ja, de volgende Windows Analytics-functies zijn buiten gebruik gesteld of nog niet beschikbaar in Desktop Analytics:

#### <a name="general"></a>Algemeen

- Ondersteuning voor scenario's waarvoor geen Configuration Manager nodig is. Voor beeld: [intune-ondersteuning](#bkmk_intune).
- Licentie vereisten voor een geldige Windows-licentie versus E3, E5
- Ondersteuning voor meerdere werk ruimten per Azure AD-Tenant
- Mogelijkheid om aangepaste query's uit te voeren en onbewerkte oplossings gegevens te exporteren
- Documentatie voor gegevens modellen voor aangepaste rapporten

#### <a name="upgrade-readiness"></a>Upgradegereedheid

- Site detectie gegevens van Internet Explorer
- Inzichten over Office-invoeg toepassingen (nu [beschikbaar in Configuration Manager](#bkmk_office))
- Inzichten over feedback hubs

#### <a name="update-compliance"></a>Updatenaleving

- Ondersteuning voor Windows Update voor bedrijven
- Inzichten voor leverings optimalisatie
- Ondersteuning voor LTSC (Long-term Servicing Channel) voor Windows 10
- Windows Insider-rapporten
- Status van Windows Defender

> [!Note]
> Alle bestaande Updatenaleving functies, met inbegrip van de onderdelen die niet beschikbaar zijn in Desktop Analytics, blijven beschikbaar in de [Updatenaleving](/windows/deployment/update/update-compliance-get-started) oplossing in de Azure Portal.

#### <a name="device-health"></a>Apparaatstatus

- Status van Stuur Programma's
- App-status (buiten een implementatie plan)
- Vaak vastgelopen apparaten of door Stuur Programma's veroorzaakte crashes
- Status van Windows-aanmelding
- Windows Information Protection
- Ondersteuning voor Windows Server

## <a name="other"></a>Anders

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a><a name="bkmk_office"></a>Kan ik Desktop Analytics voor mijn Office 365 ProPlus-upgrades gebruiken?

Nee, Desktop Analytics is gericht op Windows. Micro soft heeft Desktop Analytics ontwikkeld in nauwe samen werking met veel klanten. Feedback van klanten is het verbeteren van de manier waarop Desktop Analytics de mogelijkheid biedt om Windows-implementaties vertrouwen te beheren. Ze vertellen dat ze in Configuration Manager en intune meer willen weten over [office 365 ProPlus-gereedheid](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) met Office-beheer hulpprogramma's. Micro soft blijft investeren in deze gebieden en is gericht op Windows-scenario's in Desktop Analytics.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Hoe kan ik feedback geven over desktop Analytics?

Als u uw feedback over desktop Analytics wilt delen, selecteert u het pictogram **een glim lach verzenden** bovenaan de portal. Neem een scherm opname van uw inzending om micro soft te helpen uw feedback beter te begrijpen. U kunt ook product suggesties verzenden en andere ideeën op [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805)bijstemmen.

> [!Note]
> Deel nooit persoonlijke gegevens via een glim lach of UserVoice verzenden. Deze persoonlijke informatie bevat uw Tenant-id of commerciële id. micro soft biedt geen ondersteuning via de kanalen een glim lach verzenden of UserVoice. Als u hulp nodig hebt bij de werk ruimte voor desktop Analytics, selecteert u de koppeling **Help en ondersteuning** in het navigatie menu om een ondersteunings ticket te openen.
