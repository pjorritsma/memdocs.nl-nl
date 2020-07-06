---
title: Configuratieframework voor beveiliging van Android Enterprise
titleSuffix: Microsoft Intune
description: Krijg meer informatie over de beperkingen en instellingen die zijn voorgesteld voor standaardbeveiliging en hoge beveiliging voor Android Enterprise-apparaten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502933"
---
# <a name="android-enterprise-security-configuration-framework"></a>Configuratieframework voor beveiliging van Android Enterprise

Het configuratieframework voor beveiliging van Android Enterprise is een reeks aanbevelingen voor instellingen voor apparaatnaleving en configuratiebeleid. Met deze aanbevelingen kunt u de beveiliging voor mobiele apparaten in uw organisatie aanpassen aan uw specifieke behoeften.

In beveiligingsbewuste organisaties wordt gezocht naar manieren om bedrijfsgegevens op mobiele apparaten te beveiligen. Een methode die wordt gebruikt om deze gegevens te beveiligen, is via apparaatinschrijving. Apparaatinschrijving helpt organisaties:
- Nalevingsbeleid te implementeren (zoals de sterkte van pincodes, validatie van opengebroken/geroote apparaten, enzovoort).
- Configuratiebeleid te implementeren (zoals Wi-Fi, certificaten, VPN).
- De levenscyclus van apps te beheren.

Microsoft heeft een nieuwe taxonomie geïntroduceerd voor [beveiligingsconfiguraties in Windows 10](https://aka.ms/secconframework) om u te helpen een volledig beveiligingsscenario op te stellen. Intune maakt gebruik van een soortgelijke taxonomie voor het configuratieframework voor beveiliging van Android Enterprise. Deze omvatten aanbevolen beveiligingsinstellingen voor apparaatnaleving en apparaatbeperking (standaard, uitgebreid en hoog). Deze taxonomie wordt uitgelegd in de volgende artikelen:

1. [Methodologie voor framework-implementatie voor Android Enterprise](framework-deployment-methodology.md): Een aanbevolen methodologie voor het implementeren van het configuratieframework voor beveiliging.
2. [Beperkingen voor Android-apparaatinschrijving](device-enrollment-restrictions.md): Beperkingen bij apparaatinschrijving vooraf voor Android Enterprise-apparaten.
3. [App-configuratiebeleid instellen voor Android Enterprise-apparaten](android-app-configuration-policies.md): Configureer apps op de apparaten om persoonlijke accounts niet toe te staan.
4. [Beveiligingsinstellingen voor Android Enterprise-werkprofiel](android-work-profile-security-settings.md): Specifieke configuratie-instellingen voor standaardbeveiliging en hoge beveiliging op apparaten met een werkprofiel.
5. [Volledig beheerde instellingen voor Android Enterprise-beveiliging](android-fully-managed-security-settings.md): Specifieke configuratie-instellingen voor standaardbeveiliging, en uitgebreide en hoge beveiliging, op volledig beheerde apparaten.

## <a name="android-enterprise-enrollment-modes"></a>Android Enterprise-inschrijvingsmodi

Met Android 5.0 heeft Google Android Enterprise geïntroduceerd, dat twee inschrijvingsmodi omvat. Het configuratieframework voor beveiliging van Android Enterprise biedt aanbevelingen voor beide modi.
- [Volledig beheerde apparaten (apparaateigenaar)](android-fully-managed-enroll.md): Voor bedrijfseigendom, gekoppeld aan één gebruiker. Dergelijke apparaten zijn uitsluitend bedoeld voor werk, en niet voor persoonlijk gebruik.
- [Werkprofiel (profieleigenaar)](android-work-profile-enroll.md): Doorgaans voor apparaten die persoonlijk eigendom zijn, waarbij de IT-afdeling een duidelijke scheiding wil tussen zakelijke en persoonlijke gegevens. Op basis van beleid beheerd door de IT-afdeling kunnen zakelijke gegevens niet worden overgebracht naar het persoonlijke profiel.


## <a name="next-steps"></a>Volgende stappen

[Methodologie voor framework-implementatie voor Android Enterprise](framework-deployment-methodology.md)