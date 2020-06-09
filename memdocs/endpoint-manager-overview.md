---
title: Overzicht van Microsoft Endpoint Manager - Azure | Microsoft Docs
description: Endpoint Manager omvat Intune, Configuration Manager, co-beheer, Desktop Analytics, Windows Autopilot en het Beheercentrum waarmee alle apparaten kunnen worden beheerd, met inbegrip van on-premises apparaten.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/21/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: d9e3d03211907f31008b31d68c4ed5cd11ae1a6e
ms.sourcegitcommit: fb77170957f50aa386ff825fb4183b4fd9e3e488
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/22/2020
ms.locfileid: "83791731"
---
# <a name="microsoft-endpoint-manager-overview"></a>Overzicht van Microsoft Endpoint Manager

Microsoft Endpoint Manager zorgt dat op een moderne werkplek en met modern beheer gegevens beveiligd blijven, in de cloud en on-premises. Endpoint Manager omvat de services en hulpprogramma's die u gebruikt voor het beheren en bewaken van mobiele apparaten, desktopcomputers, virtuele machines, ingesloten apparaten en servers.

Endpoint Manager combineert services die u mogelijk al kent en gebruikt, zoals Microsoft Intune, Configuration Manager, Desktop Analytics, co-beheer en Windows Autopilot. Deze services maken deel uit van de Microsoft 365-stack en helpen u toegang te beveiligen, gegevens te beschermen en risico's te beheren.

Bekijk om te beginnen de volgende video van twee minuten van Brad Anderson, Corporate Vice President for Microsoft 365 bij Microsoft:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>Wat u krijgt

Endpoint Manager omvat onder andere de volgende services:

- **Microsoft Intune**: Intune is 100% een provider van cloudservices voor het beheren van mobiele apparaten (MDM of Mobile Device Management) en mobiele toepassingen (MAM of Mobile Application Management), voor uw apps en apparaten. U kunt er functies en instellingen op apparaten met Android, Android Enterprise, iOS/iPadOS, macOS en Windows 10 mee beheren. Intune kan worden geïntegreerd met andere services, waaronder Azure Active Directory (AD), verdedigingssoftware tegen mobiele bedreigingen, ADMX-sjablonen, Win32- en aangepaste LOB-apps en meer.

  Als u een on-premises infrastructuur hebt, zoals Exchange of Active Directory, zijn de Intune-connectors ook beschikbaar:

  - De **Intune Connector voor Active Directory** voegt vermeldingen toe aan uw on-premises Active Directory-domein voor computers die worden ingeschreven met Windows Autopilot. Zie [Hybride apparaten die aan Azure AD zijn toegevoegd](/mem/intune/enrollment/windows-autopilot-hybrid) voor meer informatie.
  - Met de **Intune Exchange Connector** kan de toegang tot uw Exchange-servers worden toegestaan (of geblokkeerd) mits apparaten bij Intune zijn ingeschreven en als ze voldoen aan uw beleidsregels. Zie [De on-premises Intune Exchange Connector instellen](/mem/intune/protect/exchange-connector-install).
  - Met de **Intune Certificate Connector** worden certificaataanvragen verwerkt van apparaten die voor verificatie gebruikmaken van certificaten en S/MIME-e-mailversleuteling. Zie [Certificaten gebruiken voor verificatie](/mem/intune/protect/certificates-configure) voor meer informatie.

  Gebruik Intune als onderdeel van Endpoint Manager om nalevingsregels te maken en controleren, om apps, functies en instellingen te implementeren op uw apparaten met behulp van de cloud.

  Zie [Wat is Microsoft Intune?](https://docs.microsoft.com/intune/fundamentals/what-is-intune) voor meer informatie.

- **Configuration Manager**: Configuration Manager is een on-premises oplossing voor het beheren van desktopcomputers, servers en laptops die zich op uw netwerk of op internet bevinden. U kunt ervoor kiezen om Configuration Manager in de cloud te gebruiken zodat integratie met Intune, Azure Active Directory (AD), Microsoft Defender ATP en andere cloudservices mogelijk is. Gebruik Configuration Manager om apps, software-updates en besturingssystemen te implementeren. U kunt ook naleving controleren, query's uitvoeren en in realtime op clients reageren, en nog veel meer.

  Omdat Configuration Manager onderdeel is van Endpoint Manager kunt u deze gewoon blijven gebruiken. Als u een aantal taken wilt verplaatsen naar de cloud, kunt u het gebruik van [co-beheer](https://docs.microsoft.com/configmgr/comanage/) overwegen.

  Zie [Wat is Configuration Manager?](https://docs.microsoft.com/configmgr/core/understand/introduction) voor meer informatie.

- **Co-beheer**: met co-beheer combineert u uw huidige investering in on-premises Configuration Manager met de cloud omdat er gebruik wordt gemaakt van Intune en andere Microsoft 365-cloudservices. U kunt kiezen of Configuration Manager of Intune de beheerinstantie is die voor de zeven verschillende workloadgroepen moet worden gebruikt.

  Als onderdeel van Endpoint Manager wordt bij co-beheer gebruikgemaakt van cloudfuncties, waaronder voorwaardelijke toegang. Een aantal taken blijft u on-premises uitvoeren, terwijl u andere taken in de cloud met Intune uitvoert.

  Zie [Wat is co-beheer?](https://docs.microsoft.com/configmgr/comanage/overview) voor meer informatie.

- **Desktop Analytics**: Desktop Analytics is een cloudservice die kan worden geïntegreerd met Configuration Manager. Desktop Analytics biedt inzicht en intelligentie zodat u beter geïnformeerde beslissingen kunt nemen over de updategereedheid van Windows. De service combineert gegevens van uw organisatie met gegevens die zijn verzameld van miljoenen apparaten die zijn verbonden met de Microsoft-cloud. Ze geeft informatie over beveiligingsupdates, apps en apparaten in uw organisatie, en identificeert compatibiliteitsproblemen met apps en stuurprogramma's. Voer een test uit met apparaten die waarschijnlijk de beste inzichten bieden in assets in uw organisatie.

  Als onderdeel van Endpoint Manager, kunt u inzichten uit de cloud die door Desktop Analytics zijn verzameld, gebruiken om Windows 10-apparaten up-to-date te houden.

  Zie [Wat is Desktop Analytics?](https://docs.microsoft.com/configmgr/desktop-analytics/overview) voor meer informatie.

- **Windows Autopilot**: met Windows Autopilot kunt u nieuwe apparaten installeren en vooraf configureren, zodat ze klaar zijn voor gebruik. Windows Autopilot is ontworpen om het gebruik van Windows-apparaten tijdens alle fasen van de levenscyclus te vereenvoudigen, voor zowel IT-medewerkers als eindgebruikers, vanaf de eerste implementatie tot het einde van de cyclus.

  Gebruik Autopilot als onderdeel van Endpoint Manager om apparaten vooraf te configureren en om ze automatisch in te schrijven in Intune. U kunt Autopilot ook integreren met Configuration Manager en co-beheer voor complexere configuraties van apparaten (preview-versie).

  Zie [Een overzicht van Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) en [Windows-apparaten inschrijven in Intune](/mem/intune/enrollment/enrollment-autopilot) voor meer informatie.

- **Azure Active Directory (AD)** : Azure AD wordt gebruikt door de eindpuntbeheerder voor de identiteit van apparaten, gebruikers, groepen en meervoudige verificatie (MFA). **Azure AD Premium**, wat extra kosten met zich meebrengt, heeft [extra functies](https://azure.microsoft.com/pricing/details/active-directory/) om apparaten, apps en gegevens te beschermen, met inbegrip van dynamische groepen, automatische inschrijving en voorwaardelijke toegang.

  Zie [gebruikers toevoegen](/mem/intune/fundamentals/users-add), [automatisch inschrijven instellen](/mem/intune/enrollment/windows-enroll) en [over voorwaardelijke toegang](/mem/intune/protect/conditional-access) voor meer informatie.

- **Endpoint Manager-beheercentrum**: het [beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) is een website die alles biedt wat u nodig hebt voor het maken van beleidsregels en het beheren van uw apparaten. Het maakt gebruikt van andere belangrijke services voor het beheer van apparaten, waaronder groepen, beveiliging, voorwaardelijke toegang en rapportage. In dit beheercentrum vindt u ook apparaten die worden beheerd door Configuration Manager en Intune (als preview-versie).

## <a name="choose-whats-right-for-you"></a>Kies wat het beste bij u past

Er zijn een aantal manieren om te bepalen wat het beste is voor uw organisatie. Welke volgende stappen u maakt, hangt af van waar uw organisatie naartoe wil. Denk na over wat u probeert te bereiken.

Bijvoorbeeld:

- Als u voortdurend nieuwe apparaten inricht, kunt u beginnen met Windows Autopilot.
- Als u regels en controle-instellingen voor uw gebruikers, apps en apparaten toevoegt, begin dan met Intune.
- Als u momenteel Configuration Manager gebruikt voor het implementeren van apps en u voorwaardelijke toegang wilt gebruiken op basis van beveiligingsvereisten, begin dan met co-beheer.
- Als u momenteel Configuration Manager gebruikt en u verantwoordelijk bent voor het up-to-date houden van Windows 10-apparaten, begin dan met Desktop Analytics.
- Als u aan de slag gaat met MDM en MAM, of als u ADMX-sjablonen gebruikt voor het beheren van Office-, Microsoft Edge -en Windows-instellingen, begin dan met Intune.

U kunt over Endpoint Manager ook drieledig denken: cloud, on-premises en cloud + on-premises:

- **Cloud**: alle gegevens worden opgeslagen in Azure. En, geen datacenters meer. Deze aanpak biedt u de voordelen van de cloud en de beveiligingsvoordelen van Azure.

- **On-premises**: als u een on-premises infrastructuur hebt waar Configuration Manager deel van uitmaakt, of nog niet klaar bent om de cloud te gebruiken, kunt u uw bestaande systemen blijven gebruiken.

- **Cloud + on-premises**: veel omgevingen zijn gemengd en gebruiken een aanpak waarbij sprake is van een koppeling met de cloud. Dat wil zeggen dat ze gebruikmaken van een combinatie van de cloud en on-premises. Gebruik voor nieuwe apparaten de voordelen van Intune om gegevens te openen en te beveiligen. Als u Configuration Manager gebruikt, maak dan verbinding met de cloud voor extra functionaliteit en analysemogelijkheden. Als u een aantal workloads naar de cloud wilt verplaatsen, is co-beheer een goede optie.

## <a name="what-you-need-to-get-started"></a>Wat u nodig hebt om te beginnen

Microsoft Endpoint Manager is een oplossingsplatform dat verschillende technologieën verenigt. Het is geen nieuwe licentie. De services worden in licentie gegeven in overeenstemming met de afzonderlijke licentievoorwaarden. Zie [Licentievoorwaarden voor het product](https://www.microsoft.com/licensing/product-licensing/products) voor meer informatie.

Als u momenteel Configuration Manager gebruikt, krijgt u ook Microsoft Intune om uw Windows-apparaten te beheren. Voor andere platforms, zoals iOS/iPadOS en Android, hebt u een afzonderlijke Intune-licentie nodig.

In de meeste gevallen is Microsoft 365 mogelijk de beste optie, omdat u dan ook Endpoint Manager en Office 365 hebt. Zie [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Gebruik de kracht van cloudintelligentie om IT en de overstap naar een moderne werkplek te vereenvoudigen en te versnellen ](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[Zelfstudie: Walkthrough voor Intune in Microsoft Endpoint Manager](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[Wat is Microsoft 365? Leermodule](https://docs.microsoft.com/learn/modules/what-is-m365/index)
