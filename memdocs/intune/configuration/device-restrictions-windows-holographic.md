---
title: Instellingen voor apparaten met Windows Holographic for Business in Microsoft Intune - Azure | Microsoft Docs
description: Meer informatie over de configuratie van instellingen voor apparaatbeperkingen in Microsoft Intune voor Windows Holographic for Business. Beheer van uitschrijving, geolocatie, wachtwoorden, apps installeren uit de App Store, cookies en pop-ups in Microsoft Edge, Microsoft Defender, zoeken, cloud en opslag, bluetooth-connectiviteit, systeemtijd en gebruiksgegevens.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2cd769b8e3ca4497c095210ea266d225354db24c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912828"
---
# <a name="windows-holographic-for-business-device-settings-to-allow-or-restrict-features-using-intune"></a>Windows Holographic for Business-apparaatinstellingen voor het toestaan of beperken van functies met behulp van Intune

Dit artikel bevat een overzicht en beschrijving van de verschillende instellingen die u kunt beheren op Windows Holographic for Business-apparaten, zoals Microsoft Hololens. Gebruik deze instellingen als onderdeel van de oplossing Mobile Device Management (MDM) voor het toestaan of uitschakelen van functies, het beheren van de beveiliging en nog veel meer.

Als Intune-beheerder kunt u deze instellingen maken en toewijzen aan uw apparaten.

## <a name="before-you-begin"></a>Voordat u begint

[Maak een Windows 10-configuratieprofiel voor apparaatbeperkingen](device-restrictions-configure.md#create-the-profile).

Wanneer u een Windows 10-configuratieprofiel voor apparaatbeperkingen maakt, zijn er meer instellingen dan in dit artikel worden vermeld. De instellingen in dit artikel worden ondersteund op apparaten met Windows Holographic for Business.

## <a name="app-store"></a>App Store

- **Apps uit de Store automatisch bijwerken**: met **Blokkeren** voorkomt u dat updates automatisch worden geïnstalleerd vanuit de Microsoft Store. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat apps die zijn geïnstalleerd vanuit de Microsoft Store, automatisch worden bijgewerkt.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Installatie van vertrouwde app**: Stel in of apps die niet afkomstig zijn uit de Microsoft Store mogen worden geïnstalleerd. Dit wordt ook wel sideloaden genoemd. Sideloading is de installatie en het uitvoeren of testen van een app die niet door de Microsoft Store is gecertificeerd. Dit kan bijvoorbeeld een app zijn die alleen voor gebruik binnen het bedrijf is bedoeld. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Blokkeren**: Hiermee voorkomt u sideloaden. Apps die niet afkomstig zijn uit de Microsoft Store, kunnen niet worden geïnstalleerd.
  - **Toestaan**: Hiermee staat u sideloaden toe. Apps die niet afkomstig zijn uit de Microsoft Store, kunnen worden geïnstalleerd.

  [ApplicationManagement/AllowAllTrustedApps CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Ontgrendeling voor ontwikkelaars**: Toestaan dat gebruikers instellingen voor Windows-ontwikkelaars wijzigen, zoals het toestaan van sideloaden van apps. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Blokkeren**: Hiermee voorkomt u de ontwikkelaarsmodus en sideloaden.
  - **Toestaan**: Hiermee staat u de ontwikkelaarsmodus en sideloaden toe.

  [ApplicationManagement/AllowDeveloperUnlock CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowdeveloperunlock)

## <a name="cellular-and-connectivity"></a>Mobiel en connectiviteit

- **Bluetooth**: Met **Blokkeren** wordt voorkomen dat gebruikers Bluetooth inschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem Bluetooth op het apparaat toestaat.

  [Connectivity/AllowBluetooth CSP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowbluetooth)

- **Bluetooth-detectie**: Met **Blokkeren** kan het apparaat niet worden gedetecteerd door andere Bluetooth-apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat andere Bluetooth-apparaten, zoals een headset, het apparaat detecteren.

  [Bluetooth/AllowDiscoverableMode CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Bluetooth-promotie**: Met **Blokkeren** voorkomt u dat het apparaat Bluetooth-reclames verzendt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat het apparaat Bluetooth-reclames verzendt.

  [Bluetooth/AllowAdvertising CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

## <a name="cloud-and-storage"></a>Cloud en opslag

- **Microsoft-account**: Met **Blokkeren** kunnen gebruikers geen Microsoft-account aan het apparaat koppelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat een Microsoft-account wordt toegevoegd en gebruikt.

  [Accounts/AllowMicrosoftAccountConnection CSP](/windows/client-management/mdm/policy-csp-accounts#accounts-allowmicrosoftaccountconnection)

## <a name="control-panel-and-settings"></a>Configuratiescherm en instellingen

- **Systeemtijd wijzigen**: Met **Blokkeren** kunnen gebruikers de datum en tijd van het apparaat niet wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instellingen wijzigen.

  [Settings/AllowDateTime CSP](/windows/client-management/mdm/policy-csp-settings#settings-allowdatetime)

## <a name="general"></a>Algemeen

- **Handmatige uitschrijving**: Met **Blokkeren** kunnen gebruikers het werkplekaccount niet verwijderen met behulp van het configuratiescherm van de werkruimte op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Experience/AllowManualMDMUnenrollment CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowmanualmdmunenrollment)

- **Geolocatie**: Met **Blokkeren** kunnen gebruikers geen locatieservices op het apparaat inschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Experience/AllowFindMyDevice CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowfindmydevice)

- **Cortana**: Met **Blokkeren** wordt de spraakassistent Cortana op het apparaat uitgeschakeld. Als Cortana is uitgeschakeld, kunnen gebruikers nog wel zoeken naar items op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem Cortana toestaat.

  [Experience/AllowCortana CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

## <a name="microsoft-edge-browser"></a>Microsoft Edge-browser

- **Startervaring** > **Pop-ups toestaan**: Met **Ja** (standaard) zijn pop-ups toegestaan in de webbrowser. Met **Nee** worden pop-upvensters niet in de browser weergegeven.

  [Browser/AllowPopups CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)

- **Favorieten en zoeken** > **Zoeksuggesties weergeven**: Met **Ja** (standaardwaarde) stelt u in dat het zoekprogramma sites kan voorstellen wanneer u zoektermen in de adresbalk typt. Met **Nee** wordt deze functie geblokkeerd.

  [Browser/AllowSearchSuggestionsinAddressBar CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)

- **Privacy en beveiliging** > **wachtwoordbeheer toestaan**: Met **Ja** (standaard) kan Wachtwoordbeheer worden gebruikt in Microsoft Edge, waardoor gebruikers wachtwoorden op het apparaat kunnen opslaan en beheren. Met **Nee** kan Wachtwoordbeheer niet in Microsoft Edge worden gebruikt.

  [Browser/AllowPasswordManager CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)

- **Privacy en beveiliging** > **Cookies**: Geef aan hoe cookies worden verwerkt in de browser. Uw opties zijn:
  - **Toestaan**: Cookies worden op het apparaat opgeslagen.
  - **Alle cookies blokkeren**: Cookies worden niet op het apparaat opgeslagen.
  - **Alleen cookies van derden blokkeren**: Cookies van derden of partners worden niet op het apparaat opgeslagen.

  [Browser/AllowCookies CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)

- **Privacy en beveiliging** > **Do Not Track-headers verzenden**: Met **Ja** worden Do Not Track-headers verzonden naar websites die traceringsgegevens aanvragen (aanbevolen). Met **Nee** (standaardwaarde) worden geen headers verzonden zodat websites de gebruiker kunnen volgen. Gebruikers kunnen deze instelling configureren.

  [Browser/AllowDoNotTrack CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen voor Microsoft Edge**: Met **Vereisen** wordt Microsoft Defender SmartScreen ingeschakeld en kunnen gebruikers deze functie niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard SmartScreen inschakelen en gebruikers toestaan deze in of uit te schakelen.

  [Browser/AllowSmartScreen CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

## <a name="password"></a>Wachtwoord

- **Wachtwoord**: Met **Vereisen** moeten gebruikers een wachtwoord invoeren om toegang te krijgen tot het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot apparaten zonder wachtwoord toestaat. Is alleen van toepassing op lokale accounts. Wachtwoorden van domeinaccounts blijven geconfigureerd door Active Directory (AD) en Azure AD.

  [DeviceLock/DevicePasswordEnabled CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

- **Wachtwoord vereisen wanneer het apparaat wordt geactiveerd vanuit een niet-actieve status**: Met **Vereisen** moeten gebruikers een wachtwoord opgeven om het apparaat te ontgrendelen na een periode van inactiviteit. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem geen pincode of wachtwoord vereist.

  [DeviceLock/AllowIdleReturnWithoutPassword CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

## <a name="reporting-and-telemetry"></a>Rapportage en telemetrie

- **Gebruiksgegevens delen**: Kies het niveau van diagnostische gegevens die worden verzonden. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kiezen het niveau dat wordt verzonden. Standaard is het mogelijk dat het besturingssysteem geen gegevens deelt.
  - **Beveiliging**: Informatie die vereist is om Windows beter te beveiligen, inclusief gegevens over de instellingen voor de gevonden gebruikerservaring en telemetrie, het hulpprogramma voor verwijderen van schadelijke software en Microsoft Defender
  - **Standaard**: Basale apparaatgegevens, zoals gegevens met betrekking tot de kwaliteit, app-compatibiliteit, app-gebruiksgegevens en gegevens van het beveiligingsniveau
  - **Uitgebreid**: Extra inzichten, zoals hoe Windows, Windows Server, System Center en apps worden gebruikt, hoe deze presteren en geavanceerde betrouwbaarheidsgegevens, plus gegevens van de niveaus Standaard en Beveiliging
  - **Volledig**: Alle gegevens die nodig zijn om problemen op te sporen en op te lossen, plus gegevens van het niveaus Beveiliging, Standaard en Uitgebreid.

  [System/AllowTelemetry CSP](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

## <a name="search"></a>Zoeken

- **Zoeklocatie**: Met **Blokkeren** voorkomt u dat Windows Search de locatie gebruikt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.

  [Search/AllowSearchToUseLocation CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

## <a name="next-steps"></a>Volgende stappen

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).