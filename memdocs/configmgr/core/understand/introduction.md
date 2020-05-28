---
title: Wat is Configuration Manager?
titleSuffix: Configuration Manager
description: Meer informatie over de basis principes van micro soft endpoint Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 13c3be302ecefad36d7be8617a4cc9354db1b685
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906060"
---
# <a name="what-is-configuration-manager"></a>Wat is Configuration Manager?

*Van toepassing op: Configuration Manager (huidige vertakking)*

Vanaf versie 1910 maakt Configuration Manager nu deel uit van micro soft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Micro soft Endpoint Manager is een geïntegreerde oplossing voor het beheer van al uw apparaten. Micro soft brengt Configuration Manager en intune samen, zonder een ingewikkelde migratie en met vereenvoudigde licenties. Blijf gebruikmaken van uw bestaande Configuration Manager investeringen, terwijl u profiteert van de kracht van de micro soft-Cloud in uw eigen tempo.

De volgende micro soft-beheer oplossingen maken nu deel uit van het merk van **micro soft Endpoint Manager** :

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Andere functies in de beheer [console voor Apparaatbeheer](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Zie [Veelgestelde vragen over micro soft Endpoint Configuration Manager](microsoft-endpoint-manager-faq.md)voor meer informatie.

## <a name="introduction"></a>Inleiding

Gebruik Configuration Manager om u te helpen met de volgende activiteiten voor systeem beheer:

- Verhoog de productiviteit en efficiëntie door hand matige taken te verminderen en u te concentreren op projecten met een grote waarde.  
- Behaal de investeringen van hardware en software.  
- Bied de productiviteit van gebruikers aan door de juiste software op het juiste moment te bieden.  

Configuration Manager helpt u bij het leveren van effectievere IT-Services door het volgende in te scha kelen:

- Veilige en schaal bare implementatie van toepassingen, software-updates en besturings systemen.
- Real-time acties op beheerde apparaten.
- Analyse en beheer in de Cloud voor on-premises en op internet gebaseerde apparaten.
- Beheer van instellingen voor naleving.  
- Uitgebreid beheer van servers, Desk tops en laptops.

Configuration Manager uitbrei ding en werkt naast allerlei technologieën en oplossingen van micro soft. Configuration Manager kan bijvoorbeeld worden geïntegreerd met:  

- Microsoft Intune een groot aantal verschillende platformen voor mobiele apparaten gezamenlijk te beheren
- Microsoft Azure om Cloud Services te hosten om uw beheer services uit te breiden
- WSUS (Windows Server Update Services) voor het beheren van software-updates
- Certificate Services
- Exchange Server en Exchange Online
- Groepsbeleid
- DNS
- Het pakket voor automatische Windows-installaties (Windows ADK) en de Hulpprogramma voor migratie van gebruikersstatus (USMT)
- Windows Deployment Services (WDS)
- Extern bureaublad en Hulp op afstand

Configuration Manager gebruikt ook:  

- Active Directory Domain Services en Azure Active Directory voor beveiliging, service locatie, configuratie en voor het detecteren van de gebruikers en apparaten die u wilt beheren.  
- Microsoft SQL Server als een gedistribueerde Data Base voor wijzigings beheer, en integreert met SQL Server Reporting Services (SSRS) om rapporten te maken voor het bewaken en bijhouden van beheer activiteiten.  
- Site systeem rollen die de beheer functionaliteit uitbreiden en gebruikmaken van de webservices van Internet Information Services (IIS).
- Bezorgings optimalisatie, Windows-lage extra vertraging op achtergrond transport (LEDBAT), Background Intelligent Transfer Service (BITS), BranchCache en andere peer-caching-technologieën om inhoud op uw netwerken en tussen apparaten te beheren.

Als u wilt slagen met Configuration Manager in een productie omgeving, moet u de beheer functies grondig plannen en testen. Configuration Manager is een krachtige beheer toepassing, met de mogelijkheid om alle computers in uw organisatie te beïnvloeden. Wanneer u Configuration Manager implementeert en beheert met een zorgvuldige planning en goed keuring van uw bedrijfs vereisten, kan Configuration Manager uw administratieve overhead en total cost of ownership verlagen.  

## <a name="user-interfaces"></a>Gebruikers interfaces

### <a name="the-configuration-manager-console"></a><a name="BKMK_Console"></a>De Configuration Manager-console

Nadat u Configuration Manager hebt geïnstalleerd, kunt u met de Configuration Manager-console sites en clients configureren en beheer taken uitvoeren en controleren. Deze console is het belangrijkste beheer punt, waarmee u meerdere sites kunt beheren.  

U kunt de Configuration Manager-console op extra computers installeren, de toegang beperken en beperken wat gebruikers met beheerders rechten in de console kunnen zien door gebruik te maken van Configuration Manager op rollen gebaseerd beheer.  

Zie [de Configuration Manager-console gebruiken](../servers/manage/admin-console.md)voor meer informatie.

### <a name="software-center"></a><a name="BKMK_ApplicationCatalog"></a>Software Center

**Software Center** is een toepassing die wordt geïnstalleerd wanneer u de Configuration Manager-client op een Windows-apparaat installeert. Gebruikers gebruiken software Center om software te vragen en te installeren die u implementeert. Met Software Center kunnen gebruikers de volgende acties uitvoeren:  

- Toepassingen, software-updates en nieuwe versies van het besturings systeem zoeken en installeren
- De software-aanvraag geschiedenis weer geven
- Apparaatcompatibiliteit weer geven op basis van het beleid van uw organisatie

U kunt ook aangepaste tabbladen in Software Center weer geven om te voldoen aan aanvullende zakelijke vereisten.

Zie de [Gebruikers handleiding voor Software Center](software-center.md)voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

Voordat u Configuration Manager installeert, moet u vertrouwd zijn met de basis begrippen en voor waarden:

- Als u bekend bent met System Center 2012 Configuration Manager, raadpleegt u [Wat is gewijzigd in System center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- Zie [Fundamentals of Configuration Manager](fundamentals.md)voor een technisch overzicht van Configuration Manager op hoog niveau.

Wanneer u bekend bent met de basis concepten, gebruikt u deze documentatie bibliotheek om u te helpen bij het implementeren en gebruiken van Configuration Manager. Begin met de volgende artikelen:

- [Functies en mogelijkheden van Configuration Manager](../plan-design/changes/features-and-capabilities.md)  
- [Een oplossing voor apparaatbeheer kiezen](../plan-design/choose-a-device-management-solution.md)  
- [Configuration Manager evalueren door uw eigen test omgeving te bouwen](../get-started/set-up-your-lab.md)
- [Hulp zoeken voor het gebruik van Configuration Manager](find-help.md)  
