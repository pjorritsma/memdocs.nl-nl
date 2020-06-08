---
title: Apparaatbeheer in Microsoft 365
description: Microsoft 365 Enterprise bevat Microsoft Intune. Bekijk hoe op welke manier Intune Mobile Device Management en Mobile Application Management biedt voor uw organisatie. Lees algemene scenario's en gebruik Intune om Microsoft 365 in uw omgeving te implementeren.
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/28/2020
ms.topic: overview
audience: microsoft-business
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: 0649d310-43a7-4b01-85d2-da255d03e1da
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: microsoft-intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: 540faaca71d3694b95d32a24c947a977989a3223
ms.sourcegitcommit: 7b8921d3ea6a751de67315771d68e2d2750fa36f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223628"
---
# <a name="device-management-overview"></a>Overzicht van apparaatbeheer

Beheerders hebben de belangrijke taak om de resources en gegevens van en organisatie te beschermen en beveiligen. Dit heet *apparaatbeheer*. Gebruikers hebben veel apparaten waarop ze persoonlijke bestanden openen en delen, websites bezoeken en apps en games installeren. Diezelfde gebruikers zijn ook werknemers en studenten. Ze willen hun apparaten gebruiken om werk- en schoolresources te openen, zoals e-mail en OneNote.

Met apparaatbeheer kunnen organisaties hun resources en gegevens beschermen en beveiligen, vanaf verschillende apparaten.

Met een apparaatbeheerprovider kunnen organisaties ervoor zorgen dat alleen gemachtigde personen en apparaten toegang krijgen tot vertrouwelijke informatie. Op vergelijkbare manier kunnen apparaatgebruikers met een gerust hart gegevens op hun telefoon openen, omdat ze weten dat hun apparaat voldoet aan de beveiligingsvereisten van de organisatie. Als organisatie vraagt u zich misschien af **wat er moet worden gebruikt om de resources te beschermen.**

Het antwoord is [Microsoft Intune](what-is-intune.md). Intune biedt mogelijkheden voor Mobile Device Management (MDM) en Mobile Application Management (MAM). MDM- en MAM-oplossingen worden voor de volgende belangrijke zaken gebruikt:

- Het ondersteuning bieden voor een diverse mobiele omgeving en het veilig beheren van apparaten met iOS/iPadOS, Android, Windows en macOS.
- Ervoor zorgen dat apparaten en apps voldoen aan de beveiligingsvereisten van uw organisatie.
- Beleidsregels maken om de gegevens van uw organisatie te beveiligen op apparaten van de organisatie en persoonlijke apparaten.
- Eén uniforme mobiele oplossing gebruiken om dit beleid af te dwingen en helpen bij het beheren van apparaten, apps, gebruikers en groepen.
- Gegevens van uw bedrijf beschermen door te bepalen hoe uw werknemers toegang hebben tot de gegevens en deze delen.

Intune maakt deel uit van Microsoft Azure, Microsoft 365 en kan worden geïntegreerd in Azure Active Directory (Azure AD). Met Azure AD kunt u bepalen wie er toegang krijgt en waartoe deze personen toegang krijgen.

## <a name="microsoft-intune"></a>Microsoft Intune

Veel organisaties, zoals Microsoft zelf, maken gebruik van Intune om eigen gegevens te beveiligen waarvan gebruikers gebruikmaken op bedrijfs- en persoonlijke mobiele apparaten. Intune bevat configuratiebeleid voor apparaten en apps, software-updatebeleid en installatiestatussen (grafieken, tabellen en rapporten) zodat u de toegang tot gegevens kunt beveiligen en bewaken.

Het is gebruikelijk dat mensen meerdere apparaten hebben waarop gebruik wordt gemaakt van verschillende platforms. Mogelijk gebruikt een werknemer bijvoorbeeld Surface Pro voor het werk en een mobiel Android-apparaat voor privézaken. Het is ook gebruikelijk dat mensen bedrijfsresources, zoals Microsoft Outlook en SharePoint, gebruikt vanaf meerdere apparaten.

Met Intune kunt u meerdere apparaten voor één persoon beheren. Het is daarbij geen probleem als er verschillende platforms op de apparaten worden gebruikt, zoals iOS/iPadOS, macOS, Android en Windows. Beleidsregels en instellingen worden in Intune gescheiden per apparaatplatform. Hierdoor is het eenvoudig om apparaten van een specifiek platform te beheren en te bekijken.

**[Veelvoorkomende scenario's](common-scenarios.md)** is een uitstekende resource om te ontdekken hoe Intune met bepaalde kwesties omgaat ten aanzien van mobiele apparaten. Er zijn scenario's te vinden over:  

- E-mail beveiligen met on-premises Exchange
- Office 365 veilig gebruiken
- Persoonlijke apparaten gebruiken voor toegang tot bedrijfsresources

Raadpleeg [Wat is Intune?](what-is-intune.md) voor meer informatie over Intune.

## <a name="co-management"></a>Co-beheer

Veel organisaties gebruiken on-premises Configuration Manager om apparaten, met inbegrip van desktops en servers, te beheren. U kunt uw on-premises Configuration Manager in de cloud verbinden met Microsoft Intune. Wanneer u verbindt via de cloud, krijgt u de voordelen van Intune en de cloud, met inbegrip van [voorwaardelijke toegang](https://docs.microsoft.com/mem/configmgr/comanage/quickstart-conditional-access), [het uitvoeren van externe acties](https://docs.microsoft.com/mem/configmgr/comanage/quickstart-remote-actions), [het gebruiken van Windows Autopilot](https://docs.microsoft.com/mem/configmgr/comanage/quickstart-autopilot), en meer.

[Microsoft Endpoint Manager](https://docs.microsoft.com/mem/endpoint-manager-overview) is een oplossingsplatform dat verschillende technologieën verenigt. Het bevat [Microsoft Intune](what-is-intune.md) voor het apparaatbeheer in de cloud en [Configuration Manager + Intune](https://docs.microsoft.com/mem/configmgr/comanage/overview) voor het koppelen van apparaten in de cloud.

Als u Configuration Manager gebruikt en u klaar bent om sommige taken naar de cloud te verplaatsen, is co-beheer ideaal.

Zie [What is co-management](https://docs.microsoft.com/mem/configmgr/comanage/overview) (Wat is co-beheer?) voor meer informatie over het koppelen van Configuration Manager in de cloud.

## <a name="integration-with-secure-and-protect-services"></a>Integratie met services beveiligen en beschermen

Het is een belangrijke taak van elke apparaatbeheeroplossing om beveiliging en bescherming te bieden. Intune kan hiervoor uitstekend worden geïntegreerd in andere services. Bijvoorbeeld:

- **Microsoft 365** is belangrijk bij het vereenvoudigen van vaak uitgevoerde IT-taken. In het beheercentrum van Microsoft 365 kunt u gebruikers maken en groepen beheren. Ook krijgt u toegang tot andere services, zoals Intune, Microsoft Azure AD en meer.

  U kunt bijvoorbeeld een iOS-/iPadOS-apparaatgroep maken in Microsoft 365. Gebruik vervolgens Intune om beleid naar een iOS-/iPadOS-apparaatgroep te pushen waarin de focus ligt op iOS-/iPadOS-functies, zoals toegang tot de App Store, gebruikmaken van AirDrop, back-ups maken in iCloud, gebruikmaken van het webfilter van Apple, en meer.

- **Windows Defender** bevat veel beveiligingsfuncties ter bescherming van Windows 10-apparaten. Als u Intune en Windows Defender samen gebruikt, kunt u:

  - [Windows Defender SmartScreen](../protect/endpoint-protection-windows-10.md) inschakelen om te zoeken naar verdachte activiteit in bestanden en apps op mobiele apparaten.
  - Gebruik [Microsoft Defender Advanced Threat Protection (ATP)](../protect/advanced-threat-protection.md) om beveiligingsschending op mobiele apparaten te voorkomen. En beperk de gevolgen van een schending door een gebruiker te blokkeren vanuit bedrijfsresources.

- **Voorwaardelijke toegang** wordt mogelijk gemaakt door Azure Active Directory en kan prima worden geïntegreerd in Intune. Met [voorwaardelijke toegang](../protect/conditional-access.md) kunt u ervoor zorgen dat alleen apparaten die voldoen aan het beleid, toegang krijgen tot e-mail, SharePoint en andere apps.

## <a name="choose-the-device-management-solution-thats-right-for-you"></a>De apparaatbeheeroplossing kiezen die het beste bij uw behoeften past

Er zijn verschillende manieren om apparaten te beheren. Ten eerste kunt u verschillende aspecten van apparaten beheren met behulp van de ingebouwde functies van Intune. Deze aanpak heet **Mobile Device Management (MDM)** . Gebruikers 'registreren' hun apparaten en gebruiken certificaten om met Intune te communiceren. Als IT-beheerder kunt u apps naar apparaten pushen, apparaten alleen gebruik laten maken van een specifiek besturingssysteem, persoonlijke apparaten blokkeren en meer. Als een apparaat ooit verloren raakt of wordt gestolen, kunt u ook alle gegevens van het apparaat verwijderen.

Bij de tweede aanpak beheert u de apps op apparaten. Deze aanpak heet **Mobile Application Management (MAM)** . Gebruikers kunnen hun persoonlijke apparaten gebruiken om toegang te krijgen tot bedrijfsresources. Wanneer gebruikers een app openen, zoals hun Postvak IN of SharePoint, wordt gevraagd om aanvullende verificatie. Als een apparaat ooit verloren raakt of wordt gestolen, kunt u alle bedrijfsgegevens verwijderen uit de met Intune beheerde toepassingen.

U kunt ook een combinatie van [MDM en MAM](byod-technology-decisions.md) gebruiken.

Wanneer u Intune instelt, kunt u er ook voor kiezen om alleen Azure Portal te gebruiken voor het beheren van apparaten. U kunt er daarnaast voor kiezen om zowel Intune als Microsoft 365 te gebruiken voor het beheren van apparaten. [Mobile Device Management migreren naar Intune via Azure Portal](https://www.microsoft.com/itshowcase/Article/Content/1042/Migrating-mobile-device-management-to-Intune-in-the-Azure-portal) is een Microsoft IT-casestudy. In deze casestudy is te zien hoe Microsoft IT tot de keuze voor een moderne apparaatbeheeraanpak is gekomen en is te lezen welke kennis hierbij is opgedaan.

## <a name="simplify-it-tasks-using-the-device-management-admin-center"></a>IT-taken vereenvoudigen via het beheercentrum Apparaatbeheer

Het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) biedt alles wat u nodig hebt om taken voor uw mobiele apparaten te beheren en voltooien. Deze werkruimte biedt services voor apparaatbeheer (inclusief Intune en Azure Active Directory) en voor het beheren van apps van klanten.

In het beheercentrum voor apparaatbeheer kunt u:

- [Apparaten inschrijven](../enrollment/device-enrollment.md)
- [Apparaatcompatibiliteit instellen](../protect/device-compliance-get-started.md)
- [Apparaten beheren](../remote-actions/device-management.md)
- [Apps beheren](../apps/app-management.md)  
- [iOS eBooks](../apps/vpp-ebooks-ios.md)  
- [Exchange On-Premises Connector installeren](../protect/exchange-connector-install.md)  
- [Rollen beheren](role-based-access-control.md)  
- Software-updates beheren
  - [Windows 10-updates beheren](../protect/windows-update-for-business-configure.md)  
  - [iOS-/iPadOS-updates beheren](../protect/software-updates-ios.md)  
- [Azure Active Directory](https://docs.microsoft.com/azure/active-directory)  
- [Gebruikers beheren](https://docs.microsoft.com/azure/active-directory/fundamentals/add-users-azure-active-directory)
- [Groepen en leden beheren](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups)
- [Problemen oplossen](help-desk-operators.md)

## <a name="next-steps"></a>Volgende stappen

Wanneer u klaar bent om aan de slag te gaan met een MDM- of MAM-oplossing, doorloopt u de verschillende stappen voor het instellen van Intune, het inschrijven van apparaten en het maken van beleid. [Mobile Device Management voor Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/mobility-infrastructure) is ook een goede resource.
