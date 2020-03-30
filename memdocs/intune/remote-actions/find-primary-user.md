---
title: Zoek de hoofdgebruiker van een Microsoft Intune-apparaat.
titleSuffix: ''
description: Zoek de hoofdgebruiker (of gebruikersaffiniteit) van een Intune-apparaat.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 06d5e2163303b9766d41bcb0bd7581dc41bf6980
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/24/2020
ms.locfileid: "80219823"
---
# <a name="find-the-primary-user-of-an-intune-device"></a>De hoofdgebruiker van een Intune-apparaat zoeken

De hoofdgebruiker, ook wel de gebruikersaffiniteit van het apparaat, is een eigenschap van elk Intune-apparaat. Aan een Intune-apparaat kan ofwel geen of één hoofdgebruiker zijn toegewezen. Wanneer er geen hoofdgebruiker is toegewezen, wordt het apparaat aangeduid als een 'gedeeld apparaat'.

## <a name="find-a-devices-primary-user"></a>De hoofdgebruiker van een apparaat zoeken

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Selecteer **Apparaten** > Selecteer een apparaat.
3. Op de pagina **Overzicht** wordt de vermelde hoofdgebruiker weergegeven.

## <a name="change-a-devices-primary-user"></a>De hoofdgebruiker van een apparaat wijzigen

De primaire gebruiker van een apparaat kan worden bijgewerkt voor Windows 10-apparaten die zijn toegevoegd aan Azure AD of hybride Azure AD.

1. Meld u aan bij het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Kies **Apparaten** > **Alle apparaten** > kies een apparaat > **Eigenschappen** > **Primaire gebruiker wijzigen**.
3. Selecteer een nieuwe gebruiker en kies **Selecteren**.

Nadat de primaire gebruiker is bijgewerkt, wordt deze ook bijgewerkt in blades van Intune- en Azure AD-apparaten.
>[!NOTE]
>1. Het kan 10 minuten duren voor updates van de primaire gebruiker tussen Eindpuntbeheer en Azure AD worden weergegeven.
>2. De primaire gebruiker kan momenteel niet worden gewijzigd op Windows 10-apparaten die gezamenlijk worden beheerd. 
>3. Als u de primaire gebruiker van het apparaat wijzigt, worden er geen wijzigingen aangebracht in het lokale groepslidmaatschap, zoals het toevoegen of verwijderen van gebruikers uit de lokale groep Administrators
>4. Het wijzigen van de hoofdgebruiker heeft geen invloed op de 'Ingeschreven door'-gebruiker. 


## <a name="what-is-the-primary-user"></a>Wat is de hoofdgebruiker?
De eigenschap Hoofdgebruiker wordt gebruikt om een Intune-gebruiker met een licentie te koppelen aan hun apparaten in:
- De bedrijfsportal-app
- Websites van de eindgebruiker
- Gebruikerservaring voor IT-professionals, zoals probleemoplossingspagina's in de Azure-portal. Deze pagina's koppelen gebruikersaccounts aan apparaten met behulp van de hoofdgebruiker. 

### <a name="company-portal-app"></a>Bedrijfsportal-app
Voor de bedrijfsportal-app wordt aangenomen dat het gebruikersaccount waarmee wordt aangemeld bij de bedrijfsportal de hoofdgebruiker van het apparaat is. Als een andere gebruiker is toegewezen als hoofdgebruiker, wordt in de bedrijfsportal-app een waarschuwing weergegeven:

'Dit apparaat is al toegewezen aan iemand anders in uw organisatie. Neem contact op met uw bedrijfsondersteuning om hoofdgebruiker van het apparaat te worden. U kunt ook doorgaan naar de bedrijfsportal, maar de functionaliteit is dan beperkt.'

Als er geen hoofdgebruiker is toegewezen aan een Intune-apparaat, wordt dit door de bedrijfsportal-app gedetecteerd als een gedeeld apparaat. Gedeelde apparaten zijn visueel identificeerbaar aan de hand van het label 'Gedeeld' dat wordt weergegeven op de apparaattegel. In deze modus kan de bedrijfsportal-app nog steeds worden gebruikt om beschikbare apps aan te vragen en te installeren. Selfservice-acties (opnieuw instellen/naam wijzigen/buiten gebruik stellen) zijn echter niet beschikbaar.  

Apps moeten worden toegewezen aan een gebruikersgroep om voor gedeelde apparaten in de bedrijfsportal te worden weergegeven. Ze worden geïnstalleerd in de systeemcontext of in de gebruikerscontext, afhankelijk van hoe de app is geconfigureerd door de IT-beheerder. Zie voor meer informatie over app-context [Apps installeren op Windows 10-apparaten](../apps/apps-windows-10-app-deploy.md). Versie 10.3.4651.0 of hoger van de bedrijfsportal-app is vereist om deze functie te gebruiken.


## <a name="who-is-assigned-as-the-primary-user"></a>Wie is toegewezen als hoofdgebruiker?
Intune voegt tijdens of kort na de inschrijving automatisch een hoofdgebruiker toe aan apparaten. De registratiemethode bepaalt wanneer de hoofdgebruiker wordt toegevoegd aan een apparaat.

| Platform | Inschrijvingsmethode | Hoofdgebruiker toegewezen | Hoofdgebruiker wordt toegewezen |
| ---- | ---- | ---- | ---- |
| Windows | Werk- of schoolaccount toevoegen (door de gebruiker) | Gebruiker inschrijven | Tijdens inschrijving |   
| Windows | Moderne app-aanmelding (door de gebruiker) | Gebruiker inschrijven | Tijdens inschrijving | 
| Windows | Alleen inschrijven in MDM (door de gebruiker) | Gebruiker inschrijven | Tijdens inschrijving | 
| Windows | Azure AD-deelname (bij ingebruikname) | Gebruiker inschrijven | Tijdens inschrijving | 
| Windows | Azure AD-deelname (automatisch bij ingebruikname) | Gebruiker inschrijven | Tijdens inschrijving | 
| Windows | Alleen inschrijven in MDM | Gebruiker inschrijven | Tijdens inschrijving | 
| Windows | Hybride AADJ + automatische inschrijving GPO | Eerste gebruiker die zich aanmeldt bij Windows | Als de eerste gebruiker zich aanmeldt bij Windows| 
| Windows | Co-beheer | Eerste gebruiker die zich aanmeldt bij Windows | Als de eerste gebruiker zich aanmeldt bij Windows | 
| Windows | Azure AD-deelname (token voor bulkinschrijving) | Geen | Niet van toepassing | 
| Windows | Azure AD-deelname (modus voor automatische zelfimplementatie) | Geen | Niet van toepassing | 
| Platformoverschrijdend | Door gebruiker gestarte inschrijving met de bedrijfsportal-app | Gebruiker inschrijven | Tijdens inschrijving |
| Platformoverschrijdend | Apparaatinschrijvingsmanager (DEM) | DEM-gebruiker inschrijven | Tijdens inschrijving |
| iOS/iPadOS, macOS | Apple Automated Device Enrollment (DEP met gebruikersaffiniteit) | Gebruiker inschrijven | Tijdens inschrijving |
| iOS/iPadOS, macOS | Apple Automated Device Enrollment (DEP zonder gebruikersaffiniteit) | Geen | Niet van toepassing |
| Android | Android bij bedrijfseigendom, toegewezen apparaten | Geen | Niet van toepassing |

## <a name="primary-user-and-azure-ad-device-owner"></a>Hoofdgebruiker en de eigenaar van het Azure AD-apparaat
In sommige gevallen kan de hoofdgebruiker voor Intune verschillen van de eigenschap **Eigenaar** in Azure AD (te vinden via **Apparaten** > **Azure AD-apparaten**). De apparaateigenaar in Azure AD wordt toegevoegd tijdens de inschrijving van het apparaat in Azure Active Directory.

## <a name="next-steps"></a>Volgende stappen
[Beheer uw Intune-apparaten.](device-management.md)
