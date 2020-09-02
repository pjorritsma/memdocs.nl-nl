---
title: Wat is Microsoft Intune-apparaatinschrijving?
titleSuffix: Microsoft Intune
description: Meer informatie over registratie voor iOS-/iPadOS-, Android- en Windows-apparaten.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 4/24/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f67fcd2-5682-4f9c-8d74-d4ab69dc978c
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: a82eb416021e86347818c333e74f31318b0661ce
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908646"
---
# <a name="what-is-device-enrollment-in-intune"></a>Wat is apparaatinschrijving in Intune?
[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Met Intune kunt u de apparaten en apps van uw werknemers beheren en bepalen hoe zij toegang hebben tot uw bedrijfsgegevens. Om gebruik te kunnen maken van MDM (Mobile Device Management), moeten de apparaten eerst worden geregistreerd bij de Intune-service. Wanneer een apparaat is geregistreerd, wordt een MDM-certificaat voor het apparaat uitgegeven. Dit certificaat wordt gebruikt om te communiceren met de Intune-service.

Zoals u in de volgende tabellen ziet, zijn er verschillende methoden om de apparaten van uw werknemers in te schrijven. Elke methode is afhankelijk van het eigendom van het apparaat (persoonlijk of zakelijk), het apparaattype (iOS, Windows, Android), en de beheervereisten (opnieuw instellen, affiniteit, vergrendelen).

Standaard kunnen apparaten voor alle platforms worden ingeschreven in Intune. U kunt echter [apparaatbeperkingen opleggen per platform](enrollment-restrictions-set.md#create-a-device-type-restriction).

## <a name="iosipados-enrollment-methods"></a>iOS-/iPadOS-inschrijvingsmethoden

| **Methode** | **Opnieuw instellen vereist** | [**Gebruikersaffiniteit**](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile) | **Vergrendeld** | **Details** |
|:---:|:---:|:---:|:---:|:---:|
| | Apparaten worden gewist tijdens de registratie. | Hiermee wordt elk apparaat aan een gebruiker gekoppeld.| Zo ja, dan kunnen gebruikers apparaten niet uitschrijven. | |
|**[BYOD](#bring-your-own-device)** | Nee| Ja | Nee | [Meer informatie](apple-mdm-push-certificate-get.md)|
|**[DEM](#device-enrollment-manager)**| Nee |Nee |Nee | [Meer informatie](device-enrollment-manager-enroll.md)|
|**[ADE](#apple-automated-device-enrollment)**| Ja | Optioneel | Optioneel|[Meer informatie](device-enrollment-program-enroll-ios.md)|
|**[USB-SA](#usb-sa)**| Ja | Optioneel | Nee| [Meer informatie](apple-configurator-enroll-ios.md)|
|**[USB-Direct](#usb-direct)**| Nee | Nee | Nee|[Meer informatie](apple-configurator-enroll-ios.md)|

## <a name="macos-enrollment-methods"></a>macOS-inschrijvingsmethoden

| **Methode** |  **Opnieuw instellen vereist** |  **Gebruikersaffiniteit** | **Vergrendeld** | **Details**|
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#bring-your-own-device)** | Nee| Ja | Nee | [Meer informatie](macos-enroll.md)|
|**[DEM](#device-enrollment-manager)**| Nee |Nee |Nee  | [Meer informatie](device-enrollment-manager-enroll.md)|
|**[ADE](#apple-automated-device-enrollment)**| Ja | Optioneel | Optioneel|[Meer informatie](device-enrollment-program-enroll-macos.md)|

## <a name="windows-enrollment-methods"></a>Windows-registratiemethoden

| **Methode** | **Opnieuw instellen vereist** | **Gebruikersaffiniteit** | **Vergrendeld** | **Details**|
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#bring-your-own-device)** | Nee | Ja | Nee | [Meer informatie](windows-enroll.md)|
|**[DEM](#device-enrollment-manager)**| Nee |Nee |Nee |[Meer informatie](device-enrollment-manager-enroll.md)|
|**Automatisch inschrijven** | Nee |Ja |Nee | [Meer informatie](windows-enroll.md#enable-windows-10-automatic-enrollment)|
|**Autopilot** |Ja |Ja |Nee | [Meer informatie](../../autopilot/enrollment-autopilot.md)
|**Bulkregistratie** |Nee |Nee |Nee | [Meer informatie](windows-bulk-enroll.md) |
|**Co-beheer** |Nee |Ja |Nee | [Meer informatie](/configmgr/core/clients/manage/co-management-overview)
|**GPO** |Nee |Ja |Nee | [Meer informatie](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)

## <a name="android-enrollment-methods"></a>Android-registratiemethoden

| **Persoonlijk** | **Inschrijvingsmethoden** | **Opnieuw instellen vereist** | **Gebruikersaffiniteit** | **Vergrendeld** | **Details**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**Android-apparaatbeheer**|**Gebruiker geïnitieerd via bedrijfsportal** | Nee | Ja | Nee | [Meer informatie](../user-help/enroll-device-android-company-portal.md)|
|**Android Enterprise - Werkprofiel**|**Gebruiker geïnitieerd via bedrijfsportal**| Nee | Ja | Nee | [Meer informatie](android-work-profile-enroll.md)|


&nbsp;

| **Bedrijf** | **Inschrijvingsmethoden** | **Opnieuw instellen vereist** | **Gebruikersaffiniteit** | **Vergrendeld** | **Details**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**Android-apparaatbeheer**|**[DEM](#device-enrollment-manager) geïnitieerd via de bedrijfsportal**| Nee | Nee | Nee |[Meer informatie](device-enrollment-manager-enroll.md)|
|**Android-apparaatbeheer**|**(Vooraf gedeclareerde IMEI of SN) Door gebruiker geïnitieerd via bedrijfsportal**| Nee | Ja | Nee | [Meer informatie](corporate-identifiers-add.md)|
|**Android-apparaatbeheer met Zebra-mobiliteitsextensies**|**Door gebruiker of [DEM](#device-enrollment-manager) geïnitieerd via de bedrijfsportal**| Nee | Ja, als dit door de gebruiker is geïnitieerd, Nee als dit door [DEM](#device-enrollment-manager) is geïnitieerd | Nee | [Meer informatie](../configuration/android-zebra-mx-overview.md)|
|**Toegewezen Android Enterprise-apparaten**|**NFC, Token, QR-code, Zero Touch**| Ja | Nee | Configureerbaar via beleid | [Meer informatie](android-kiosk-enroll.md)|
|**Volledig beheerde Android Enterprise-apparaten**|**NFC, Token, QR-code, Zero Touch**| Ja | Ja | Configureerbaar via beleid | [Meer informatie](android-dedicated-devices-fully-managed-enroll.md)|
|**Android Enterprise in bedrijfseigendom met een werkprofiel** | **NFC, Token, QR-code, Zero Touch** | Ja | Ja | Configureerbaar via beleid | [Meer informatie](android-corporate-owned-work-profile-enroll.md)|

## <a name="bring-your-own-device"></a>Bring Your Own Device
BYOD-apparaten (Bring Your Own Devices) zijn persoonlijke telefoons, tablets en pc's. BYOD-gebruikers gebruiken de bedrijfsportal-app om hun apparaten te registreren. Met dit programma hebben gebruikers toegang tot de bedrijfsresources als e-mail.

## <a name="corporate-owned-device"></a>Apparaat in bedrijfseigendom
[Apparaten in bedrijfseigendom (COD)](corporate-identifiers-add.md) zijn telefoons, tablets en pc's die eigendom zijn van de organisatie en worden verdeeld onder de werknemers. Met registratie van COD's zijn scenario's mogelijk zoals automatische registratie, gedeelde apparaten en vooraf geautoriseerde registratievereisten. Een veelgebruikte manier voor de registratie van COD's is dat een beheerder of manager DEM (apparaatinschrijvingsmanager) gebruikt. iOS/iPadOS-apparaten kunnen rechtstreeks worden ingeschreven met de ADE-hulpprogramma's van Apple. Apparaten met een IMEI-nummer kunnen ook geïdentificeerd en getagd worden als bedrijfseigendom.

### <a name="device-enrollment-manager"></a>Apparaatinschrijvingsmanager
De apparaatinschrijvingsmanager (DEM) is een speciaal gebruikersaccount voor registratie en beheer van meerdere apparaten in bedrijfseigendom. Beheerders kunnen de bedrijfsportal installeren en veel apparaten zonder gebruiker registreren. Dergelijke apparaten zijn bijvoorbeeld geschikt voor gebruik bij een verkooppunt of met hulpprogramma-apps, maar niet voor gebruikers die toegang nodig hebben tot e-mail of bedrijfsresources. Meer informatie over [DEM](device-enrollment-manager-enroll.md).

### <a name="apple-automated-device-enrollment"></a>ADE (Automatische apparaatinschrijving) van Apple
Met ADE-beheer van Apple kunt u beleid maken en 'draadloos' implementeren op iOS-/iPadOS- en macOS-apparaten die met ADE worden gekocht en beheerd. Het apparaat wordt geregistreerd wanneer de gebruiker het apparaat de eerste keer inschakelt en de configuratieassistent uitvoert. Deze methode ondersteunt de supervisiemodus voor iOS/iPadOS, waarmee een apparaat kan worden geconfigureerd met een specifieke functionaliteit.

Meer informatie over ADE-inschrijving voor iOS/iPadOS-apparaten:

- [Kiezen hoe u iOS-/iPadOS-apparaten inschrijft](ios-enroll.md)
- [iOS-/iPadOS-apparaten inschrijven met het Device Enrollment Program](device-enrollment-program-enroll-ios.md)

### <a name="usb-sa"></a>USB-SA
IT-beheerders gebruiken Apple Configurator, via USB, om elk apparaat van het bedrijf handmatig voor te bereiden voor registratie met behulp van de Configuratieassistent. De IT-beheerder maakt een registratiebeleid en exporteert het beleid naar Apple Configurator. Wanneer gebruikers hun apparaat ontvangen, wordt hun gevraagd om Configuratieassistent uit te voeren om het apparaat in te schrijven. Deze methode ondersteunt de modus **iOS onder supervisie**, waarmee de volgende functies worden ingeschakeld:
- Vergrendelde registratie
- Kioskmodus en andere geavanceerde configuraties en beperkingen

Meer informatie over inschrijving van iOS-/iPadOS-apparaten met Apple Configurator en Configuratieassistent:

- [Bepalen hoe u iOS-/iPadOS-apparaten registreert](ios-enroll.md)
- [iOS-/iPadOS-apparaten inschrijven met Configurator en Configuratieassistent](apple-configurator-enroll-ios.md)

### <a name="usb-direct"></a>USB-Direct
Voor directe registratie moet de beheerder elk apparaat handmatig registreren door een registratiebeleid te maken en dit te exporteren naar Apple Configurator. Via USB aangesloten apparaten van het bedrijf worden direct geregistreerd zonder dat deze hoeven te worden gewist. De apparaten worden beheerd als apparaten zonder gebruiker. Ze zijn niet vergrendeld of onder supervisie en kunnen geen voorwaardelijke toegang, jailbreakdetectie en beheer van mobiele toepassingen ondersteunen.

Zie voor meer informatie over de iOS-/iPadOS-inschrijving:

- [Bepalen hoe u iOS-/iPadOS-apparaten registreert](ios-enroll.md)
- [iOS-/iPadOS-apparaten inschrijven met Configurator en directe inschrijving](apple-configurator-enroll-ios.md)

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Mobiele apparaten opschonen na de verloopdatum van het MDM-certificaat

Het MDM-certificaat wordt automatisch vernieuwd wanneer mobiele apparaten communiceren met de Intune-service. Als mobiele apparaten worden gewist of een bepaalde tijd niet kunnen communiceren met de Intune-service, wordt het MDM-certificaat niet vernieuwd.Als mobiele apparaten worden gewist of een bepaalde tijd niet kunnen communiceren met de Intune-service, wordt het MDM-certificaat niet vernieuwd. Het apparaat wordt 180 dagen nadat het MDM-certificaat is verlopen verwijderd uit de Azure Portal.