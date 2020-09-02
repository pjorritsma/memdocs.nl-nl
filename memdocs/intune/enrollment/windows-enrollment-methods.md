---
title: Intune-inschrijvingsmethoden voor Windows-apparaten
titleSuffix: Microsoft Intune
description: Informatie over de verschillende manieren waarop u Windows-apparaten in Intune kunt inschrijven
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/18/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: ''
ms.openlocfilehash: c91c0f776ee46ddebbbb7bc27895b0f8795ae975
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911587"
---
# <a name="intune-enrollment-methods-for-windows-devices"></a>Intune-inschrijvingsmethoden voor Windows-apparaten

Als u apparaten in Intune wilt beheren, moeten ze eerst worden ingeschreven bij de Intune-service. U kunt zowel persoonlijke als zakelijke apparaten inschrijven voor Intune-beheer. 

U kunt apparaten op twee manieren in Intune inschrijven:
- Gebruikers kunnen hun Windows-pc's zelf inschrijven 
- Beheerders kunnen beleidsregels configureren om automatische inschrijving af te dwingen, zonder tussenkomst van een gebruiker

## <a name="user-self-enrollment-in-intune"></a>Zelfinschrijving voor gebruikers in Intune

Gebruikers kunnen hun eigen Windows-apparaat zelf inschrijven via een van deze methoden:

- [BYOD (Bring Your Own Device)](../user-help/enroll-windows-10-device.md): Gebruikers schrijven hun persoonlijke apparaten in door de **Bedrijfsportal-app** te downloaden en te installeren. Dit proces:
  - Het apparaat wordt bij Azure Active Directory ingeschreven voor toegang tot zakelijke resources, zoals e-mail.
  - Het apparaat wordt als persoonlijk apparaat (BYOD) in Intune ingeschreven.
Als een beheerder Automatische inschrijving heeft geconfigureerd (beschikbaar voor Azure AD Premium-abonnementen), hoeft de gebruiker zijn of haar referenties maar eenmaal in te voeren. Anders moet hij of zij zich afzonderlijk inschrijven via Alleen MDM-inschrijving en de referenties opnieuw invoeren.  
- **Alleen MDM-inschrijving**: hiermee kunnen gebruikers een bestaande werkgroep, Active Directory of een aan de Azure Active Directory toegevoegde pc in Intune inschrijven. Gebruikers voeren de inschrijving uit via Instellingen op hun bestaande Windows-pc. Deze methode wordt echter niet aanbevolen, aangezien het apparaat hiermee niet bij Azure Active Directory wordt geregistreerd. Ook kunnen bepaalde functies zoals Voorwaardelijke toegang niet worden gebruikt.
- [Azure Active Directory (Azure AD) Join](/azure/active-directory/user-help/user-help-join-device-on-network): hiermee voegt u het apparaat toe aan Azure Active Directory en kunnen gebruikers zich bij Windows aanmelden met hun Azure AD-referenties. Als Automatische inschrijving is ingeschakeld, wordt het apparaat automatisch in Intune ingeschreven. Het voordeel van automatische inschrijving is dat de gebruiker maar één stap hoeft uit te voeren. Anders moet hij of zij zich afzonderlijk inschrijven via Alleen MDM-inschrijving en de referenties opnieuw invoeren. Gebruikers kunnen zich ofwel tijdens de initiële Windows OOBE of bij Instellingen op deze manier inschrijven. Het apparaat wordt als een zakelijk apparaat in Intune gemarkeerd.
- [Autopilot](../../autopilot/enrollment-autopilot.md): deze functie zorgt ervoor dat gebruikers automatisch aan Azure AD worden toegevoegd en dat nieuwe zakelijke apparaten bij Intune worden ingeschreven. Met deze methode zorgt wordt de out-of-the-boxervaring vereenvoudigd. Bovendien hoeven er geen aangepaste installatiekopieën van het besturingssysteem meer op de apparaten te worden toegepast. Als beheerders Intune gebruiken om Autopilot-apparaten te beheren, kunnen ze beleidsregels, profielen, apps en meer beheren op apparaten nadat ze zijn ingeschreven.  Er zijn vier typen Autopilot-implementatie: [Zelfimplementatiemodus](/windows/deployment/windows-autopilot/self-deploying) (voor kiosken, digitale borden of een gedeeld apparaat), [Door gebruiker gestuurde modus](/windows/deployment/windows-autopilot/user-driven) (voor traditionele gebruikers), [White label](/windows/deployment/windows-autopilot/white-glove) waarmee partners of IT-medewerkers een Windows 10-pc alvast kunnen inrichten, zodat deze volledig is geconfigureerd en klaar is voor gebruik en [Autopilot voor bestaande apparaten](/windows/deployment/windows-autopilot/existing-devices) waarmee u gemakkelijk de meest recente versie van Windows 10 op uw bestaande apparaten kunt implementeren.

## <a name="administrator-based-enrollment-in-intune"></a>Op beheerders gebaseerde inschrijving in Intune

Beheerders kunnen de volgende inschrijvingsmethoden instellen waarvoor geen gebruikersinteractie is vereist:

- Met [Hybrid Azure AD Join](/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) kunnen beheerders het groepsbeleid voor Active Directory zo instellen dat apparaten die met hybride Azure AD zijn samengevoegd automatisch worden ingeschreven.
- Met [Co-beheer van Configuration Manager](/configmgr/comanage/overview) kunnen beheerders hun bestaande via Configuration Manager beheerde apparaten bij Intune inschrijven om te profiteren van zowel de voordelen van Intune als die van Configuration Manager.
- [Apparaatinschrijvingsmanager](device-enrollment-manager-enroll.md) (Device enrollment manager, DEM) is een speciaal serviceaccount. DEM-accounts beschikken over machtigingen waarmee gemachtigde gebruikers meerdere apparaten in bedrijfseigendom kunnen inschrijven en beheren. Dergelijke apparaten zijn bijvoorbeeld geschikt voor gebruik bij een verkooppunt of met hulpprogramma-apps, maar niet voor gebruikers die toegang nodig hebben tot e-mail of bedrijfsresources. Bij deze methode is het gebruik van functies, zoals Voorwaardelijke toegang, niet toegestaan. 
- Met [Bulksgewijs inschrijven](windows-bulk-enroll.md) kunnen gemachtigde gebruikers grote aantallen nieuwe apparaten in bedrijfseigendom samenvoegen met Azure Active Directory en Intune. U maakt een inrichtingspakket met de app Windows Configuration Designer (WCD). Vervolgens kunt u, met behulp van USB-sticks tijdens de initiële Windows OOBE-ervaring of vanaf een bestaande Windows-pc, het inrichtingspakket installeren zodat de apparaten automatisch in Intune worden ingeschreven. Bij deze methode is het gebruik van Voorwaardelijke toegang niet toegestaan.
- [Inschrijven van apparaten met Windows IoT Core](/windows/iot-core/manage-your-device/intunedeviceenrollment) is mogelijk met door het apparaat voor te bereiden met behulp van het Windows IoT Core-dashboard en vervolgens Windows Configuration Designer te gebruiken om een inrichtingspakket te maken. Dit inrichtingspakket wordt tijdens het opstarten dan vanaf een SD-kaart uitgevoerd om de apparaten automatisch bij Intune te registreren.

## <a name="next-steps"></a>Volgende stappen

[Meer informatie over de mogelijkheden van de Windows-inschrijvingsmethoden](enrollment-method-capab.md)