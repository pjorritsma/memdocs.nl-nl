---
title: Hybride Azure AD instellen
titleSuffix: Configuration Manager
description: Als uw omgeving momenteel is toegevoegd aan een domein van Windows 10-apparaten, moet u hybride Azure AD instellen voordat u co-beheer inschakelt.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8e2f7bbb51c72fa3d0f2a36e8a5419552d468b4c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711474"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Hybride Azure AD instellen voor co-beheer

Als u Windows 10-apparaten hebt gekoppeld aan on-premises Active Directory, moet u, voordat u co-beheer inschakelt in Configuration Manager, deze apparaten eerst toevoegen aan Azure Active Directory (Azure AD). Dit proces wordt hybride deelname aan Azure AD genoemd. 

In de volgende video is Senior Program Manager Sandeep Deo en product marketing manager Adam-haven voor het bespreken en bekijken van de configuratie van apparaten in azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Met het hybride proces van Azure AD-join worden automatisch uw on-premises aan het domein gekoppelde apparaten geregistreerd bij Azure AD. Zie de volgende artikelen voor meer informatie over dit proces:
- [Inleiding tot apparaatbeheer in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Uw hybride Azure AD-deelname plannen](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

Hybride Azure AD-deelname is een van de belangrijkste fundamenten voor co-beheer. Dit proces kan voor sommige klanten lastig zijn, bijvoorbeeld:
- Uw organisatie gebruikt een identiteits oplossing van derden 
- De complexiteit van het instellen van Active Directory Federation Services (ADFS)

Het oplossen van deze uitdagingen kan enige richt lijn zijn. Dit artikel helpt u bij het oplossen van vertragingen.


## <a name="how-to-do-it"></a>Hoe u dit doet

Apparaten zijn vergelijkbaar met gebruikers bij het maken van een identiteit die u wilt beveiligen. Als u de identiteit van een apparaat op elk gewenst moment en op elke locatie wilt beveiligen, moet u de identiteit van dat apparaat in azure AD zetten.

Op basis van het type domein dat u gebruikt, zijn er twee manieren om dit te doen. Hybride Azure AD-deelname configureren voor een van de volgende domein typen:  
- [Federatieve domeinen](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Beheerde domeinen](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

De twee voor gaande methoden bieden de beste ervaring. Raadpleeg de volgende artikelen voor meer gedetailleerde informatie, inclusief het volledig hand matige proces:
- [Hand matig aan hybride Azure AD gekoppelde apparaten configureren](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- AD [FS Pass-Through-verificatie voor hybride Azure AD](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), inclusief Azure AD-detectie  

Zie voor richt lijnen voor probleem oplossing de [Windows 10 Hybrid Azure AD Troubleshooting Guide (Engelstalig](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)).



## <a name="case-study"></a>Casestudy

Een groot Euro pees software bedrijf met meer dan 100.000 gebruikers in het netwerk heeft een granulaire en gefaseerde benadering geduurd om hybride Azure AD-deelname in te scha kelen.

Tijdens de plannings fase, omdat hybride Azure AD-deelname een belang rijk element is dat co-beheer ondersteunt, hebben de Configuration Manager beheerders gewerkt met het identiteits team. Dit software bedrijf heeft veel ADFS-regels en sommige zijn complex. Om deze uitdaging op te lossen, heeft het identiteits team de bestaande ADFS-regels gelezen voordat ze hybride Azure AD-deelname hebben ingeschakeld. Het IT-team heeft er ook voor gekozen om Azure AD Connect te upgraden naar de nieuwste versie. Azure AD Connect biedt nu een geautomatiseerde proces stroom voor het inschakelen van hybride deelname aan Azure AD.

Na een geslaagde implementatie en tests in de productie omgeving heeft deze klant hybride Azure AD-deelname ingeschakeld voor het hele productie-erfgoed. Binnen een week hadden ze elk apparaat met Windows 10-co-beheer.



## <a name="contact-fasttrack"></a>Contact opnemen met FastTrack

Als u hulp nodig hebt bij het instellen van Azure AD op een wille keurig moment in het proces, gaat u naar [Microsoft FastTrack](https://Microsoft.com/FastTrack/), meldt u zich aan en vraagt u om hulp. 

Zie voor meer informatie [hulp vragen van FastTrack](quickstart-fasttrack.md). 

