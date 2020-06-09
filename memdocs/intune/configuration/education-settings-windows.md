---
title: Onderwijsinstellingen voor Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Een lijst met alle onderwijsinstellingen voor Windows 10-apparaten weergeven. Gebruik deze instellingen in een apparaatconfiguratieprofiel met de app Toets maken, kies hoe gebruikers of studenten zich aanmelden, controleer het scherm tijdens de toets, en meer in Intune.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55e38ac8b5503e98df4878529ac892b55a52be47
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429624"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>De app Toets maken configureren op Windows 10-apparaten in Microsoft Intune

Met de app Toets maken kunt u veilig onlinetests beheren op de Windows 10-apparaten van uw klas. Als u de app Toets maken wilt instellen, moet u een apparaatconfiguratieprofiel in Intune maken en de instellingen voor veilige evaluatie configureren. In dit artikel worden de instellingen voor de app Toets maken beschreven. 

Nadat u het profiel hebt geconfigureerd, wijst u het toe aan en implementeert u het voor uw studenten. 

In [De app Toets maken in Intune](education-settings-configure.md) vindt u meer informatie over deze functie.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een apparaatconfiguratieprofiel](education-settings-configure.md#create-a-device-profile).

## <a name="take-a-test-settings"></a>Instellingen voor Toets maken

- **Accounttype**: kies hoe gebruikers zich aanmelden voor de toets. Uw opties zijn:
  - Microsoft Azure Active Directory-account
  - Domeinaccount
  - Lokaal account
  - Lokaal gastaccount: Alleen beschikbaar op apparaten met Windows 10, versie 1903 en hoger.
- **Gebruikersnaam voor account**: voer de gebruikersnaam in voor het account dat wordt gebruikt voor de app Toets maken. U kunt accounts in de volgende indeling invoeren:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Accountnaam**: U stelt een lokaal gastaccounttype in door de naam in te voeren van het account dat wordt gebruikt voor de app Toets maken. De accountnaam wordt weergegeven als tegel in het aanmeldingsscherm. Studenten klikken op de tegel om de toets te starten.  
- **URL van de toets**: geef de URL op van de toets die de gebruikers moeten afleggen. Zie de [documentatie van Toets maken](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) voor meer informatie over het ophalen van de URL.
- **Printerverbinding**: met **Vereisen** wordt alleen toegang tot de app Toets maken toegestaan vanaf apparaten die zijn verbonden met een printer. Met deze instelling wordt ook de afdrukknop van de app beschikbaar gemaakt voor toetsmakers. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk toegestaan dat studenten toegang krijgen tot de app vanaf apparaten die niet zijn verbonden met een printer.  
- **Schermcontrole**: met **Toestaan** worden de schermactiviteiten gecontroleerd terwijl de gebruikers een toets afleggen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard wordt het mogelijk verhinderd dat u het scherm controleert tijdens de toets.
- **Tekstsuggesties**: kies **Toestaan** om makers van de toets toe te staan tekstsuggesties te zien. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard worden tekstsuggesties terwijl de gebruikers een toets afleggen mogelijk geblokkeerd.

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).

Meer informatie over de [app Toets maken](education-settings-configure.md).
