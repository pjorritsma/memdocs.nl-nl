---
title: Windows Information Protection-instellingen in Microsoft Intune
titleSuffix: Microsoft Intune
description: In dit onderwerp vindt u meer informatie over de Microsoft Intune-instellingen die u kunt gebruiken om Windows-gegevensbescherming te beheren.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/18/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 008f750fd15caeac8da9397a1c3ff0684cdf28f7
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914664"
---
# <a name="how-to-configure-windows-information-protection-in-microsoft-intune"></a>Windows Information Protection configureren in Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Met de toename van apparaten in de onderneming die het eigendom zijn van werknemers, is ook het risico toegenomen op het onbedoeld lekken van gegevens via apps en services, zoals e-mail, sociale media en de openbare cloud, die zich buiten de invloedssfeer van de onderneming bevinden. Bijvoorbeeld wanneer een medewerker de nieuwste technische afbeeldingen via een persoonlijke e-mailaccount verstuurt, productinformatie kopieert en in een tweet plakt, of een conceptversie van een verkooprapport opslaat in de openbare cloud.

**Windows-gegevensbeveiliging** helpt bij de bescherming tegen deze potentiële gegevenslekken zonder dat de gebruikerservaring van werknemers hierdoor wordt beïnvloed. Het helpt tevens zakelijke apps en gegevens te beschermen tegen onbedoelde gegevenslekken op apparaten die eigendom zijn van de onderneming en persoonlijke apparaten die werknemers meenemen naar het werk, zonder dat hiervoor wijzigingen nodig zijn aan uw omgeving of andere apps.

Dit Intune-beleid beheert de lijst met apps die zijn beveiligd door Windows Information Protection, de bedrijfsnetwerklocaties, het beveiligingsniveau en de versleutelingsinstellingen.

>[!NOTE]
> Als u de bedrijfsportal-app voor Windows 10 met Windows Information Protection wilt gebruiken, moet u de bedrijfsportal-app toevoegen in de modus Windows Information Protection van **Uitgesloten**. 

Zie voor meer informatie:
- [Uw ondernemingsgegevens beveiligen met Windows Information Protection](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).
- [Een WIP-beleid (Windows Information Protection) maken met de klassieke console voor Microsoft Intune](/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune)
- [Een WIP-beleid (Windows Information Protection) maken met MDM via Azure Portal voor Microsoft Intune](/windows/threat-protection/windows-information-protection/create-wip-policy-using-intune-azure)
- [Een WIP-beleid (Windows Information Protection) maken met MAM via Azure Portal voor Microsoft Intune](/windows/threat-protection/windows-information-protection/create-wip-policy-using-mam-intune-azure)