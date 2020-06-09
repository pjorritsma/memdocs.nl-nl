---
title: Meer informatie over beperkingen voor apparaatlimiet tussen Intune en Azure
titleSuffix: ''
description: Inzicht in de verschillen tussen beperkingen voor apparaatlimiet van Intune en beperkingen voor apparaatlimiet van Azure AD.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8610b619a4ac05f37b893060b3b3a2bcb1dae528
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864851"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Meer informatie over Beperkingen voor apparaatlimieten van Intune en Azure AD

Beperkingen voor het aantal apparaten kunnen op twee manieren worden geconfigureerd:
- Intune-inschrijving
- Azure Active Directory (AD) gekoppeld of Azure AD geregistreerd

In dit artikel wordt duidelijk wanneer deze limieten worden toegepast op basis van uw configuratie.

## <a name="intune-device-limit-restrictions"></a>Apparaatlimietbeperkingen van Intune instellen

De apparaatlimietbeperkingen van Intune stelt het maximum aantal apparaten in dat een gebruiker kan gebruiken (maximaal 15). Om de **Apparaatlimiet** in te stellen, ga naar [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **Beperking maken**. Zie [Een beperking voor apparaatlimiet maken](enrollment-restrictions-set.md#create-a-device-limit-restriction) voor meer informatie

## <a name="azure-device-limit-restriction"></a>Beperking voor apparaatlimiet van Azure

Beperkingen voor Azure-apparaatlimieten stelt het maximum aantal apparaten in dat door Azure AD wordt toegevoegd of Azure AD wordt geregistreerd. Als u het **maximum aantal apparaten per gebruiker** wilt instellen, gaat u naar de Azure-portal > **Azure Active Directory** > **Apparaten**. Zie [Apparaatinstellingen configureren](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal) voor meer informatie

## <a name="settings-applied-based-on-user-affinity"></a>Instellingen die zijn toegepast op basis van gebruikersaffiniteit

Als u zowel apparaatlimietbeperkingen voor Intune en Azure hebt ingesteld, wordt in de volgende tabel weergegeven wat er wordt toegepast op basis van de instelling voor gebruikersaffiniteit.

| Apparaatplatform | Gebruikersaffiniteit | Azure is toegepast | Intune is toegepast |
| ----- | ----- | ----- | ----- | ----- |
| Android Enterprise - Werkprofiel | Ja | Ja | Ja|
| Toegewezen Android Enterprise-apparaat | Nee | Nee | Nee |
| Volledig beheerde Android Enterprise-apparaten | Ja | Ja | Ja |
| Android-apparaatbeheerder | Ja | Ja | Ja |
| Android-apparaatbeheerder DEM | Nee | | Nee | 
| iOS/macOS BYOD | Ja | Ja | Ja |
| Automatische apparaatinschrijving (Automated Device Enrollment of ADE) van iOs/macOS | Ja | Ja | Ja |
| iOS/macOS ADE | Nee | Ja | Nee |
| Windows BYOD | Ja | Ja | Ja |
| Alleen Windows MD | | Ja | Ja |
| Windows Azure AD gekoppeld| Ja | Ja | Nee |
| Windows Autopilot | Ja | Ja | Nee |
| Apparaat is hybride Windows AD-gekoppeld | Nee | Nee | Ja |
| Co-beheer Windows inschakelen | Nee | Ja | Nee |
| Windows DEM | Nee | Ja | Nee |
| Windows-bulkinschrijving | Nee | Ja | Nee |


## <a name="android-and-ios-devices"></a>Android- en iOS-apparaten

### <a name="ios-or-android-devices-example-1"></a>iOS-of Android-apparaten voorbeeld 1

- De instelling voor het **Maximum aantal apparaten per gebruiker** in Azure is ingesteld op 3.
- De instelling voor **apparaatlimiet** in Intune is ingesteld op 5.
 
**Resultaat:** Het maximum aantal is per gebruiker. Als u bijvoorbeeld drie Intune-apparaten inschrijft, mislukt de Azure-registratie voor het vierde apparaat vanwege de instellingen om het aantal registraties voor de apparaten te beperken.

### <a name="ios-or-android-devices-example-2"></a>iOS-of Android-apparaten voorbeeld 2

- De instelling voor het **Maximum aantal apparaten per gebruiker** in Azure is ingesteld op 20.
- De instelling voor **apparaatlimiet** in Intune is ingesteld op 2.

**Resultaat:** U kunt nu twee apparaten registreren en inschrijven. De Intune-inschrijving wordt geblokkeerd voor extra apparaten. ADE zonder gebruikersaffiniteit wordt beperkt door de registratielimieten van Azure-apparaat, hoewel deze niet aan een gebruiker zijn gekoppeld.

## <a name="windows-devices"></a>Windows-apparaten

Apparaatlimietbeperkingen van Intune zijn niet van toepassing op de volgende typen Windows-inschrijvingen:
- Gezamenlijk beheerde inschrijvingen
- Inschrijvingen voor groepsbeleidsobject (GPO)
- Gekoppelde inschrijvingen voor Azure AD
- Gekoppelde bulkinschrijvingen voor Azure AD
- Autopilot-inschrijvingen
- Inschrijvingen met Apparaatinschrijvingsmanager

U kunt apparaatlimietbeperkingen niet afdwingen voor deze inschrijvingstypen, omdat ze worden beschouwd als gedeelde apparaten. U kunt in Azure Active Directory vaste limieten instellen voor deze typen inschrijvingen.

Voor de apparaatlimietbeperking in Azure is de instelling **Maximum aantal apparaten per gebruiker** van toepassing op apparaten die zijn opgenomen in Azure AD-gekoppeld of Azure AD-geregistreerd. Deze instellingen zijn niet van toepassing op hybride Azure AD-gekoppelde apparaten.

### <a name="windows-10-example-1"></a>Windows 10 voorbeeld 1

- De instelling voor het **Maximum aantal apparaten per gebruiker** in Azure is ingesteld op 5.
- De instelling voor **apparaatlimiet** in Intune is ingesteld op 3.
- De apparaten zijn hybride Azure AD-gekoppeld en worden automatisch geregistreerd (GPO-geconfigureerd).

**Resultaat:** Omdat de inschrijving via GPO wordt gepusht, is de limiet voor de registratie van Azure-apparaten niet van toepassing.  De limiet voor Intune-apparaten is ook niet van toepassing.

### <a name="windows-10-example-2"></a>Windows 10 voorbeeld 2

- De instelling voor het **Maximum aantal apparaten per gebruiker** in Azure is ingesteld op 5.
- De instelling voor **apparaatlimiet** in Intune is ingesteld op 2.
- De apparaten zijn gekoppeld aan het lokale domein en zijn ingeschreven met behulp van **Instellingen** > **Toegang werk of school** > **Verbinding te maken**.

**Resultaat:** U kunt maar twee apparaten inschrijven voordat ze worden geblokkeerd. U kunt maximaal vijf apparaten registreren.


## <a name="next-steps"></a>Volgende stappen

- [Een beperking voor apparaatlimiet maken in Azure.](https://docs.microsoft.com/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Apparaatinstellingen configureren in Azure.](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [Meer informatie over registratie en domein toegevoegd.](https://docs.microsoft.com/azure/active-directory/devices/overview#getting-devices-in-azure-ad)
