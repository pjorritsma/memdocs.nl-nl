---
title: Apparaatbeperkingsinstellingen voor Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Bekijk een overzicht van alle instellingen en de bijbehorende beschrijvingen voor het maken van apparaatbeperkingen op apparaten met Windows 10 en hoger. Gebruik deze instellingen in een configuratieprofiel om controle te houden over schermopnamen, wachtwoordvereisten, instellingen voor de kioskmodus, apps in de store, de Microsoft Edge-browser, Microsoft Defender, toegang tot de cloud, het startmenu en meer in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f469d9646fad3b247743b6017f0ecbc7917f2cdf
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311167"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Apparaatinstellingen voor Windows 10 en hoger om functies toe te staan of te beperken met behulp van Intune

In dit artikel vindt u een overzicht en beschrijving van de verschillende instellingen die u kunt beheren op apparaten met Windows 10 en hoger. Gebruik deze instellingen als onderdeel van de MDM-oplossing (Mobile Device Management) om functies toe te staan of uit te schakelen, wachtwoordregels in te stellen, het vergrendelingsscherm aan te passen, Microsoft Defender te gebruiken en nog veel meer.

Deze instellingen worden toegevoegd aan een apparaatconfiguratieprofiel in Intune en vervolgens toegewezen aan of geïmplementeerd op uw Windows 10-apparaten.

> [!Note]
> Niet alle opties zijn beschikbaar in alle edities van Windows. Bekijk de ondersteunde edities op [Beleid-CSP's](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider) (wordt op een andere Microsoft-website geopend).

## <a name="before-you-begin"></a>Voordat u begint

[Een profiel voor beperkingen van Windows 10-apparaten maken](device-restrictions-configure.md#create-the-profile).

## <a name="app-store"></a>App Store

Deze instellingen gebruiken de [beleid-CSP ApplicationManagement](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **App Store (alleen mobiel)** : Met **Blokkeren** voorkomt u dat gebruikers toegang hebben tot de App Store op mobiele apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat gebruikers toegang hebben tot de App Store.
- **Apps uit de Store automatisch bijwerken**: met **Blokkeren** voorkomt u dat updates automatisch worden geïnstalleerd vanuit de Microsoft Store. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat apps die zijn geïnstalleerd vanuit de Microsoft Store, automatisch worden bijgewerkt.

  [ApplicationManagement/AllowAppStoreAutoUpdate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Installatie van vertrouwde app**: Stel in of apps die niet afkomstig zijn uit de Microsoft Store mogen worden geïnstalleerd. Dit wordt ook wel sideloaden genoemd. Sideloading is de installatie en het uitvoeren of testen van een app die niet door de Microsoft Store is gecertificeerd. Dit kan bijvoorbeeld een app zijn die alleen voor gebruik binnen het bedrijf is bedoeld. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Blokkeren**: Hiermee voorkomt u sideloaden. Apps die niet afkomstig zijn uit de Microsoft Store, kunnen niet worden geïnstalleerd.
  - **Toestaan**: Hiermee staat u sideloaden toe. Apps die niet afkomstig zijn uit de Microsoft Store, kunnen worden geïnstalleerd.

- **Ontgrendeling voor ontwikkelaars**: Toestaan dat gebruikers instellingen voor Windows-ontwikkelaars wijzigen, zoals het toestaan van sideloaden van apps. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Blokkeren**: Hiermee voorkomt u de ontwikkelaarsmodus en sideloaden.
  - **Toestaan**: Hiermee staat u de ontwikkelaarsmodus en sideloaden toe.

  In [Uw apparaat inschakelen voor ontwikkeling](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development) vindt u meer informatie over deze functie.
  
  [ApplicationManagement/AllowAllTrustedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Gedeelde app-gegevens voor gebruikers**: Kies **Toestaan** om toepassingsgegevens te delen tussen verschillende gebruikers van hetzelfde apparaat en met andere exemplaren van de app. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem ingesteld zijn dat gegevens niet met andere gebruikers en andere exemplaren van dezelfde app kunnen worden gedeeld.

  [ApplicationManagement/AllowSharedUserAppData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Alleen persoonlijke Store gebruiken**: Met **Toestaan** kunnen apps alleen uit een persoonlijke Store worden gedownload, niet vanuit de openbare Store. Dit geldt ook voor detailhandelcatalogi. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat apps mogen worden gedownload uit zowel een persoonlijke als openbare store.

  [ApplicationManagement/RequirePrivateStoreOnly CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Uit Store afkomstige app starten**: Met **Blokkeren** schakelt u alle apps uit die vooraf zijn geïnstalleerd op het apparaat of die zijn gedownload uit de Microsoft Store. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat deze apps mogen worden geopend.

  [ApplicationManagement/DisableStoreOriginatedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **App-gegevens installeren op systeemvolume**: Met **Blokkeren** kunnen er vanuit apps geen gegevens worden opgeslagen op het systeemvolume van het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem ingesteld zijn dat via apps gegevens op het systeemstationvolume mogen worden opgeslagen.

  [ApplicationManagement/RestrictAppDataToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Apps installeren op systeemstation**: Met **Blokkeren** kunnen er vanuit apps geen gegevens worden opgeslagen op het systeemstation van het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem ingesteld zijn dat via apps gegevens mogen worden geïnstalleerd op het systeemstation.

  [ApplicationManagement/RestrictAppToSystemVolume CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **Game DVR (alleen desktop)** : Met **Blokkeren** wordt het opnemen en uitzenden van Windows Game uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem ingesteld zijn dat het opnemen en uitzenden van games is toegestaan.

  [ApplicationManagement/AllowGameDVR CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Alleen apps uit de Store**: Met deze instelling bepaalt u de gebruikerservaring wanneer gebruikers apps van andere locaties dan de Microsoft Store installeren. U voorkomt er niet mee dat inhoud van USB-apparaten, netwerkshares of andere niet-internetbronnen wordt geïnstalleerd. Gebruik een betrouwbare browser om ervoor te zorgen dat deze beveiligingsmaatregelen naar verwachting werken.

  Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard kan in het besturingssysteem zijn ingesteld dat gebruikers apps van andere locaties dan de Microsoft Store mogen installeren, met inbegrip van apps die zijn gedefinieerd in andere beleidsinstellingen.  
  - **Overal**: Hiermee schakelt u de app-aanbevelingen uit en kunnen gebruikers apps vanaf elke locatie installeren.  
  - **Alleen Store**: De bedoeling is om te voorkomen dat schadelijke inhoud invloed heeft op uw gebruikersapparaten als er uitvoerbare inhoud van internet wordt gedownload. Wanneer gebruikers apps van internet proberen te installeren, wordt de installatie geblokkeerd. Gebruikers krijgen een bericht te zien waarin wordt aanbevolen apps te downloaden van de Microsoft Store.
  - **Aanbevelingen**: Wanneer gebruikers via internet een app willen installeren die beschikbaar is in de Microsoft Store, krijgen ze een bericht te zien waarin wordt aanbevolen de app vanuit de Store te downloaden.  
  - **Store heeft voorkeur**: Hiermee worden gebruikers gewaarschuwd wanneer ze apps van andere locaties dan de Microsoft Store installeren.

  [SmartScreen/EnableAppInstallControl CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **Gebruikerscontrole over installaties**: met **Blokkeren** voorkomt u dat gebruikers de installatieopties wijzigen die normaal gesproken zijn gereserveerd voor systeembeheerders, zoals het invoeren van de map voor de installatie van de bestanden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in Windows Installer ingesteld zijn dat gebruikers deze installatieopties niet kunnen wijzigen en dat bepaalde beveiligingsfuncties van Windows Installer worden omzeild.

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Apps installeren met verhoogde bevoegdheden**: **Blokkeren** geeft Windows Installer de opdracht om verhoogde bevoegdheden te gebruiken wanneer een programma op een systeem wordt geïnstalleerd. Deze bevoegdheden worden aan alle programma's aangeboden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kunnen door het systeem de machtigingen van de huidige gebruiker worden toegepast bij het installeren van programma's die een systeembeheerder niet implementeert of aanbiedt.

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Opstart-apps**: Voer een lijst met apps in die worden geopend nadat een gebruiker zich aanmeldt bij het apparaat. Gebruik een door puntkomma's gescheiden lijst met familienamen van pakketten (PFN) van Windows-toepassingen. Om dit beleid te doen functioneren moet het manifest in de Windows-apps gebruikmaken van een opstarttaak.

  [ApplicationManagement/LaunchAppAfterLogOn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>Mobiel en connectiviteit

Deze instellingen gebruiken de beleids-CPS's [Connectivity](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) en [Wi-Fi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi) met daarbij een overzicht van de ondersteunde Windows-edities.

- **Mobiel gegevenskanaal**: Hiermee kunt u instellen of gebruikers toegang hebben tot gegevens, bijvoorbeeld tijdens het surfen op internet, wanneer ze zijn verbonden met een mobiel netwerk. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. gebruikers kunnen dit uitschakelen.
  - **Blokkeren**: Het mobiele gegevenskanaal is niet toegestaan. Gebruikers kunnen dit niet inschakelen.
  - **Toestaan (niet-bewerkbaar)** : Het mobiele gegevenskanaal is toegestaan. Gebruikers kunnen dit niet uitschakelen.

- **Gegevensroaming**: Met **Blokkeren** is mobiele gegevensroaming op het apparaat niet mogelijk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Roaming tussen netwerken kan standaard worden toegestaan tijdens het ophalen van gegevens.
- **VPN via het mobiele netwerk**: Met **Blokkeren** heeft het apparaat geen toegang tot VPN-verbindingen wanneer het is verbonden met een mobiel netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem VPN toestaan om van elke verbinding gebruik te maken, inclusief mobiele verbindingen.
- **VPN-roaming via het mobiele netwerk**: Met **Blokkeren** heeft het apparaat geen toegang meer tot VPN-verbindingen tijdens roaming op een mobiel netwerk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat VPN-verbindingen zijn toegestaan tijdens het roamen.
- **Service voor verbonden apparaten**: Met **Blokkeren** schakelt u het onderdeel Platform voor verbonden apparaten (CDP) uit. Met CDP is detectie en verbinding met andere apparaten (via Bluetooth/LAN of de cloud) mogelijk voor het starten van externe apps, chatten op afstand, externe app-sessies en andere bewerkingen met meerdere apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat de service voor verbonden apparaten wordt toegestaan, waardoor detectie van en verbinding met andere Bluetooth-apparaten mogelijk is.
- **NFC**: Met **Blokkeren** zijn NFC-functies niet toegestaan. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat gebruikers NFC-functies op het apparaat inschakelen en configureren.
- **Wi-Fi**: Met **Blokkeren** kunnen gebruikers geen Wi-Fi-verbindingen op het apparaat inschakelen, configureren en gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat Wi-Fi-verbindingen zijn toegestaan.
- **Automatisch verbinding maken met Wi-Fi-hotspots**: Met **Blokkeren** wordt voorkomen dat apparaten automatisch verbinding maken met Wi-Fi-hotspots. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat apparaten automatisch verbinding mogen maken met gratis Wi-Fi-hotspots en automatisch de voorwaarden voor de verbinding mogen accepteren.
- **Handmatige Wi-Fi-configuratie**: Met **Blokkeren** wordt voorkomen dat apparaten verbinding maken met Wi-Fi buiten MDM-netwerken die door de server zijn geïnstalleerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem gebruikers toestaan hun eigen netwerk-SSID's voor Wi-Fi-verbindingen toe te voegen en te configureren.
- **Wi-Fi-scaninterval**: Voer in hoe vaak apparaten zoeken naar Wi-Fi-netwerken. Geef een waarde op tussen 1 (zo vaak mogelijk) en 500 (zo min mogelijk). Standaard ingesteld op `0` (nul).

### <a name="bluetooth"></a>Bluetooth

Voor deze instellingen wordt de [beleid-CSP Bluetooth](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth) gebruikt, waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Bluetooth**: Met **Blokkeren** wordt voorkomen dat gebruikers Bluetooth inschakelen. Met **Niet geconfigureerd** (standaard) kan Bluetooth op het apparaat worden gebruikt.
- **Bluetooth-detectie**: Met **Blokkeren** kan het apparaat niet worden gedetecteerd door andere Bluetooth-apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem andere Bluetooth-apparaten, zoals een headset, toestaan het apparaat te detecteren.

  [Bluetooth/AllowDiscoverableMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Vooraf koppelen van Bluetooth**: Met **Blokkeren** kunnen bepaalde Bluetooth-apparaten niet automatisch worden gekoppeld met een hostapparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem automatische koppeling met het hostapparaat toestaan.

  [Bluetooth/AllowPrepairing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **Bluetooth-promotie**: Met **Blokkeren** voorkomt u dat het apparaat Bluetooth-reclames verzendt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem het apparaat toestaan Bluetooth-aankondigingen te verzenden.

  [Bluetooth/AllowAdvertising CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **Services waarvoor Bluetooth is toegestaan**: U kunt een lijst met toegestane Bluetooth-services en -profielen **Toevoegen** in de vorm van hexadecimale tekenreeksen, zoals `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.

  [ServicesAllowedList usage guide](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) (Engelstalig) bevat meer informatie over de lijst met services.

  [Bluetooth/ServicesAllowedList CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## <a name="cloud-and-storage"></a>Cloud en opslag

Voor deze instellingen wordt de [beleid-CSP Accounts](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-accounts) gebruikt, waarbij ook de ondersteunde Windows-edities worden vermeld.

> [!IMPORTANT]
> Het blokkeren of uitschakelen van deze Microsoft-accountinstellingen kan invloed hebben op inschrijvingsscenario's waarvoor gebruikers zich moeten aanmelden bij Azure AD. Stel dat u gebruikmaakt van [AutoPilot-ondersteuning](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). Normaal gesproken krijgen gebruikers een Azure AD-aanmeldingsvenster te zien. Als deze instellingen zijn ingesteld op **Blokkeren** of **Uitschakelen**, wordt de Azure AD-aanmeldingsoptie mogelijk niet weergegeven. In plaats daarvan wordt gebruikers gevraagd om de gebruiksrechtovereenkomst te accepteren en een lokaal account te maken. Dit is mogelijk niet wat u wilt.

- **Microsoft-account**: Met **Blokkeren** kunnen gebruikers geen Microsoft-account aan het apparaat koppelen. Met **Blokkeren** kunnen ook enkele inschrijvingsscenario's worden beïnvloed die afhankelijk zijn van gebruikers om het inschrijvingsproces te voltooien. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem toestaan om een Microsoft-account toe te voegen en te gebruiken.
- **Niet-Microsoft-account**: Met **Blokkeren** kunnen gebruikers geen niet-Microsoft-accounts toevoegen via de gebruikersinterface. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem gebruikers toestaan e-mailaccounts toe te voegen die niet aan een Microsoft-account zijn gekoppeld.
- **Synchronisatie van instellingen voor Microsoft-accounts**: Met **Blokkeren** voorkomt u synchronisatie tussen apparaten van apparaat- en app-instellingen die aan een Microsoft-account zijn gekoppeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem deze synchronisatie toestaan.
- **Aanmeldhulp voor Microsoft-account toestaan**: Met deze service van het besturingssysteem kunnen gebruikers zich aanmelden bij hun Microsoft-account. Standaard kan het besturingssysteem gebruikers toestaan om de service **Aanmeldhulp voor Microsoft-account** (wlidsvc) te starten en te stoppen.
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard kan het besturingssysteem gebruikers toestaan om de service **Aanmeldhulp voor Microsoft-account** (wlidsvc) te starten en te stoppen.
  - **Uitgeschakeld**: Hiermee wordt de service Microsoft-aanmeldhulp (wlidsvc) ingesteld op Uitgeschakeld en wordt voorkomen dat gebruikers deze handmatig starten.

      Met **Uitschakelen** kunnen ook enkele inschrijvingsscenario's worden beïnvloed die afhankelijk zijn van gebruikers om de inschrijving te voltooien. Stel dat u gebruikmaakt van [AutoPilot-ondersteuning](https://docs.microsoft.com/windows/deployment/windows-autopilot/white-glove). Normaal gesproken krijgen gebruikers een Azure AD-aanmeldingsvenster te zien. Wanneer deze optie is ingesteld op **Uitschakelen**, wordt de optie voor aanmelden bij Microsoft Azure AD mogelijk niet weergegeven. In plaats daarvan wordt gebruikers gevraagd om de gebruiksrechtovereenkomst te accepteren en een lokaal account te maken. Dit is mogelijk niet wat u wilt.

## <a name="cloud-printer"></a>Cloudprinter

Voor deze instellingen wordt de [beleid-CSP EnterpriseCloudPrint](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint) gebruikt, waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Printerdetectie-URL**: Voer de URL in voor het vinden van cloudprinters. Voer bijvoorbeeld `https://cloudprinterdiscovery.contoso.com` in.
- **Verificatie-URL voor printertoegang**: Voer de URL van het verificatie-eindpunt in om OAuth-tokens op te halen. Voer bijvoorbeeld `https://azuretenant.contoso.com/adfs` in.
- **GUID van de systeemeigen client-app voor Azure**: Voer de GUID in waarmee de clienttoepassing wordt geïdentificeerd die gemachtigd is voor het ophalen van OAuth-tokens van OAuthAuthority. Voer bijvoorbeeld `E1CF1107-FF90-4228-93BF-26052DD2C714` in.
- **Resource-URI voor de afdrukservice**: Voer de OAuth-resource-URI in voor de afdrukservice zoals geconfigureerd in Azure Portal. Voer bijvoorbeeld `http://MicrosoftEnterpriseCloudPrint/CloudPrint` in.
- **Maximum aantal printers waarvoor een query moet worden uitgevoerd**: Voer het maximumaantal printers in waarvoor u een query wilt uitvoeren. De standaardwaarde is `20`.
- **Resource-URI voor de printerdetectieservice**: Voer de OAuth-resource-URI in voor de printerdetectieservice zoals geconfigureerd in Azure Portal. Voer bijvoorbeeld `http://MopriaDiscoveryService/CloudPrint` in.

> [!TIP]
> Na het instellen van een [Windows Server Hybrid Cloud Print](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview) kunt u deze instellingen configureren en vervolgens implementeren naar uw Windows-apparaten.

## <a name="control-panel-and-settings"></a>Configuratiescherm en instellingen

- **App Instellingen**: Met **Blokkeren** hebben gebruikers geen toegang tot de app Instellingen van Windows. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem gebruikers toestaan de app Instellingen op het apparaat te openen.
  - **Systeem**: Met **Blokkeren** wordt de toegang tot het gebied Systeem van de app Instellingen geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
    - **Instellingen voor in-/uitschakelen en slaapstand wijzigen** (alleen desktop): Met **Blokkeren** voorkomt u dat gebruikers de instellingen voor in-/uitschakelen en de slaapstand op het apparaat wijzigen. Met **Niet geconfigureerd** (standaard) kunnen gebruikers de instellingen voor in-/uitschakelen en de slaapstand wijzigen.
  - **Apparaten**: Met **Blokkeren** wordt de toegang tot het gebied Apparaten van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Netwerk en internet**: Met **Blokkeren** wordt de toegang tot het gebied Netwerk en internet van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Persoonlijke instellingen**: Met **Blokkeren** wordt de toegang tot het gebied Persoonlijke instellingen van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Apps**: Met **Blokkeren** wordt de toegang tot het gebied Apps van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Accounts**: Met **Blokkeren** wordt de toegang tot het gebied Accounts van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Tijd en taal**: Met **Blokkeren** wordt de toegang tot het gebied Tijd en taal van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
    - **Systeemtijd wijzigen**: Met **Blokkeren** kunnen gebruikers de datum en tijd van het apparaat niet wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Gebruikers kunnen deze instellingen wijzigen.
    - **Regio-instellingen wijzigen** (alleen desktop): Met **Blokkeren** kunnen gebruikers de regio-instellingen van het apparaat niet wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Gebruikers kunnen deze instellingen wijzigen.
    - **Taalinstellingen wijzigen (alleen desktop)** : Met **Blokkeren** kunnen gebruikers de taalinstellingen van het apparaat niet wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Gebruikers kunnen deze instellingen wijzigen.

      [Beleid-CSP Settings](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings)

  - **Gaming**: Met **Blokkeren** wordt de toegang tot het gebied Gaming van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Betere toegankelijkheid**: Met **Blokkeren** wordt de toegang tot het gebied Toegankelijkheid van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Privacy**: Met **Blokkeren** wordt de toegang tot het gebied Privacy van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
  - **Bijwerken en beveiliging**: Met **Blokkeren** wordt de toegang tot het gebied Bijwerken en beveiliging van de app Instellingen op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

## <a name="display"></a>Weergave

Voor deze instellingen wordt de [beleid-CSP Display](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-display) gebruikt, waarbij ook de ondersteunde Windows-edities worden vermeld.

Met GDI DPI-schaalbaarheid krijgen apps die geen DPI-status hebben, een per-monitor-DPI-status.

- **GDI-schaalbaarheid voor apps inschakelen**: U kunt de verouderde apps **Toevoegen** waarvoor u GDI DPI-schaalbaarheid wilt inschakelen. Voer bijvoorbeeld `filename.exe` of `%ProgramFiles%\Path\Filename.exe` in.

  GDI DPI-schaalbaarheid is ingeschakeld voor alle verouderde toepassingen in de lijst.

- **GDI-schaalbaarheid voor apps uitschakelen**: U kunt de verouderde apps **Toevoegen** waarvoor u GDI DPI-schaalbaarheid wilt uitschakelen. Voer bijvoorbeeld `filename.exe` of `%ProgramFiles%\Path\Filename.exe` in.

  GDI DPI-schaalbaarheid is uitgeschakeld voor alle verouderde apps in de lijst.

U kunt ook een CSV-bestand **importeren** van de lijst met apps.

## <a name="general"></a>Algemeen

Deze instellingen gebruiken de [beleid-CSP Experience](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience), waarbij ook de ondersteunde Windows-edities worden vermeld. 

- **Schermafbeelding** (alleen mobiel): Met **Blokkeren** kunnen gebruikers geen schermafbeeldingen op het apparaat maken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Kopiëren en plakken (alleen mobiel)** : Met **Blokkeren** kunnen gebruikers niet kopiëren en plakken tussen apps op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Handmatige uitschrijving**: Met **Blokkeren** kunnen gebruikers het werkplekaccount niet verwijderen met behulp van het configuratiescherm van de werkruimte op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  Deze beleidsinstelling is niet van toepassing als de computer is toegevoegd aan Azure AD en automatische inschrijving is ingeschakeld.

- **Handmatige installatie van het basiscertificaat** (alleen mobiel): Met **Blokkeren** voorkomt u dat gebruikers handmatig basiscertificaten en tussenliggende CAP-certificaten kunnen installeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Camera**: Met **Blokkeren** kunnen gebruikers de camera op het apparaat niet gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard toegang tot de camera van het apparaat toestaan.

  Intune beheert alleen de toegang tot de camera van het apparaat. Het heeft geen toegang tot afbeeldingen of video's.

  [Camera CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-camera)

- **Bestandssynchronisatie met OneDrive**: Met **Blokkeren** kunnen gebruikers geen bestanden synchroniseren naar OneDrive vanaf het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [System/DisableOneDriveFileSync CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **Verwisselbare opslag**: Met **Blokkeren** kunnen gebruikers geen externe opslagapparaten gebruiken, zoals SD-kaarten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Geolocatie**: Met **Blokkeren** kunnen gebruikers geen locatieservices op het apparaat inschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [System/AllowLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **Gedeeld internet**: Met **Blokkeren** kan de internetverbinding op het apparaat niet worden gedeeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Telefoon opnieuw instellen**: Met **Blokkeren** kunnen gebruikers de instellingen niet wissen en de fabrieksinstellingen op het apparaat niet terugzetten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **USB-verbinding**: Met **Blokkeren** is er geen toegang tot externe opslagapparaten via een USB-verbinding op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Opladen via USB wordt niet beïnvloed door deze instelling.

  [Connectivity/AllowUSBConnection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **Modus AntiTheft** (alleen mobiel): Met **Blokkeren** kunnen gebruikers de voorkeursinstelling voor de modus AntiTheft niet selecteren op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Cortana**: Met **Blokkeren** wordt de spraakassistent Cortana uitgeschakeld. Als Cortana is uitgeschakeld, kunnen gebruikers nog wel zoeken naar items op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem Cortana toestaan.

  [Experience/AllowCortana CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

- **Spraakopname** (alleen mobiel): Met **Blokkeren** kunnen gebruikers het spraakopnameapparaat van het apparaat niet gebruiken. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem spraakopname toestaan.
- **Apparaatnaam wijzigen** (alleen mobiel): Met **Blokkeren** kunnen gebruikers de naam van het apparaat niet wijzigen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Inrichtingspakketten toevoegen**: Met **Blokkeren** kan de runtime-configuratieagent geen inrichtingspakketten op het apparaat installeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Inrichtingspakketten verwijderen**: Met **Blokkeren** kan de runtime-configuratieagent geen inrichtingspakketten van het apparaat verwijderen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Apparaatdetectie**: Met **Blokkeren** kan het apparaat niet worden gedetecteerd door andere apparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Experience/AllowDeviceDiscovery](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **Taakwisselaar** (alleen mobiel): Met **Blokkeren** wordt de taakwisselaar op het apparaat geblokkeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.
- **Foutberichtvenster voor simkaart** (alleen mobiel): Met **Blokkeren** worden er geen foutberichten weergegeven op het apparaat als er geen simkaart wordt gedetecteerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem de foutberichten weergeven.
- **Werkruimte van Windows Ink**: Kies of en hoe de gebruiker toegang heeft tot de Ink-werkruimte. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard kan het besturingssysteem de Ink-werkruimte inschakelen en wordt het gebruikers toegestaan om deze te gebruiken boven het vergrendelingsscherm.
  - **Uitgeschakeld op het vergrendelingsscherm**: De Ink-werkruimte is ingeschakeld en de functie is ingeschakeld. Gebruikers hebben echter geen toegang tot de Ink-werkruimte boven het vergrendelingsscherm.
  - **Uitgeschakeld**: De toegang tot de Ink-werkruimte is uitgeschakeld. De functie is uitgeschakeld.

  [WindowsInkWorkspace policy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Autopilot opnieuw instellen**: Als u **Toestaan** kiest, kunnen gebruikers met beheerdersrechten alle gebruikersgegevens en -instellingen verwijderen met **CTRL + Win + R** op het vergrendelingsscherm van het apparaat. Het apparaat wordt automatisch opnieuw geconfigureerd en opnieuw ingeschreven bij het beheer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem het gebruik van deze functie niet toestaat.
- **Vereisen dat gebruikers verbinding met een netwerk maken tijdens de apparaatconfiguratie**: Kies **Vereisen** zodat het apparaat verbinding maakt met een netwerk alvorens verder te gaan na de netwerkpagina tijdens de installatie van Windows. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem gebruikers toestaan om voorbij de netwerkpagina te gaan, zelfs wanneer het apparaat niet is verbonden met een netwerk.

  De instelling wordt van kracht de volgende keer dat het apparaat wordt gewist of opnieuw wordt ingesteld. Net als bij elke andere Intune-configuratie moet het apparaat worden geregistreerd bij en worden beheerd door Intune om configuratie-instellingen te kunnen ontvangen. Als het apparaat echter eenmaal is geregistreerd en beleid ontvangt en u het apparaat vervolgens opnieuw instelt, wordt de instelling afgedwongen bij de volgende Windows-installatie.

  [TenantLockdown CSP](https://docs.microsoft.com/windows/client-management/mdm/tenantlockdown-csp)

- **Directe geheugentoegang**: **Blokkeren** blokkeert directe geheugentoegang (DMA) voor alle downstream hot-pluggable PCI-poorten totdat een gebruiker zich bij Windows aanmeldt. **Ingeschakeld** (standaard) staat toegang tot DMA toe, zelfs wanneer een gebruiker niet is aangemeld.

  [DataProtection/AllowDirectMemoryAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **Processen in Taakbeheer beëindigen**: Met deze instelling bepaalt u of niet-beheerders Taakbeheer kunnen gebruiken om taken te beëindigen. Met **Blokkeren** voorkomt u dat standaardgebruikers (niet-beheerders) processen of taken op het apparaat kunnen beëindigen met behulp van Taakbeheer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem standaardgebruikers toestaan processen of taken te beëindigen met behulp van Taakbeheer.

  [TaskManager/AllowEndTask CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## <a name="locked-screen-experience"></a>Vergrendeld scherm

- **Meldingen van het Actiecentrum (alleen mobiel)** : Met **Blokkeren** worden meldingen van Onderhoudscentrum niet op het vergrendelingsscherm van het apparaat weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem gebruikers toestaan te kiezen welke apps meldingen weergeven op het vergrendelingsscherm.

  [AboveLock/AllowActionCenterNotifications CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#AboveLock_AllowActionCenterNotifications)

- **Afbeeldings-URL vergrendelingsscherm (alleen desktop)** : Voer de URL in van een afbeelding in JPE-, JPEG- of PNG-indeling die wordt gebruikt als achtergrond van het Windows-vergrendelingsscherm. Voer bijvoorbeeld `https://contoso.com/image.png` in. Met deze instelling wordt de afbeelding vergrendeld en kan deze later niet meer worden gewijzigd.

  [Personalization/LockScreenImageUrl CSP](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp)

- **Time-out van het scherm die door de gebruiker kan worden ingesteld (alleen mobiel)** : Met **Toestaan** kunnen gebruikers de time-out van het scherm configureren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard biedt het besturingssysteem gebruikers deze optie mogelijk niet.

  [DeviceLock/AllowScreenTimeoutWhileLockedUserConfig CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana op vergrendeld scherm** (alleen desktop): Met **Blokkeren** hebben gebruikers geen interactie met Cortana wanneer het vergrendelingsscherm wordt weergegeven op het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan interactie met Cortana standaard toestaan.

  [AboveLock/AllowCortanaAboveLock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Pop-upmeldingen op vergrendeld scherm**: Met **Blokkeren** worden pop-upmeldingen niet op het vergrendelingsscherm van het apparaat weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard deze meldingen toestaan.

  [AboveLock/AllowToasts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **Time-out van het scherm (alleen mobiel)** : Hiermee stelt u de duur (in seconden) in van de schermvergrendeling totdat het scherm wordt uitgeschakeld. Ondersteunde waarden zijn 11-1800. Voer bijvoorbeeld `300` om deze time-out in te stellen op 5 minuten.

  [DeviceLock/ScreenTimeoutWhileLocked CSP](https://msdn.microsoft.com/ie/dn904962(v=vs.94)#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Berichten

Voor deze instellingen wordt de [beleid-CSP Messaging](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-messaging) gebruikt, waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Berichten synchroniseren (alleen mobiel)** : Met **Blokkeren** wordt er geen back-up gemaakt van sms-berichten en worden deze niet hersteld. Ook worden er geen sms-berichten gesynchroniseerd tussen Windows-apparaten. Als u deze optie uitschakelt, worden er geen gegevens opgeslagen op servers die niet door het bedrijf worden beheerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem gebruikers toestaan deze instellingen te wijzigen en hun berichten te synchroniseren.
- **Mms (alleen mobiel)** : Met **Blokkeren** wordt de functionaliteit voor het verzenden en ontvangen van mms-berichten op het apparaat uitgeschakeld. Ondernemingen kunnen dit beleid gebruiken om mms op apparaten uit te schakelen als onderdeel van de vereiste voor controle of beheer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem mms-berichten toestaan.
- **RCS (alleen mobiel)** : Met **Blokkeren** wordt de functionaliteit van Rich Communication Services (RCS) voor verzenden en ontvangen op het apparaat uitgeschakeld. Ondernemingen kunnen dit beleid gebruiken om RCS op apparaten uit te schakelen als onderdeel van de vereiste voor controle of beheer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem verzenden en ontvangen van RCS-berichten toestaan.

## <a name="microsoft-edge-browser"></a>Microsoft Edge-browser

Deze instellingen gebruiken de [beleid-CSP Browser](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser), waarbij ook de ondersteunde Windows-edities worden vermeld.

### <a name="use-microsoft-edge-kiosk-mode"></a>Gebruik van Microsoft Edge-kioskmodus

De beschikbare instellingen veranderen, afhankelijk van wat u kiest. Uw opties zijn:

- **Nee** (standaard): Microsoft Edge wordt niet uitgevoerd in de kioskmodus. U kunt alle Microsoft Edge-instellingen wijzigen en configureren.
- **Digitale/interactieve display (kiosk voor één app)** : Hiermee worden Microsoft Edge-instellingen gefilterd die van toepassing zijn op de Microsoft Edge-kioskmodus Digitale/interactieve display, alleen voor gebruik in Windows 10-kiosken voor één app. Kies deze instelling om een volledig URL-scherm te openen en alleen de inhoud op die website weer te geven. [Digitale displays instellen](https://docs.microsoft.com/windows/configuration/setup-digital-signage) biedt meer informatie over deze functie.
- **InPrivate openbaar bladeren (kiosk voor één app)** : Hiermee worden Microsoft Edge-instellingen gefilterd die van toepassing zijn op de Microsoft Edge-kioskmodus InPrivate openbaar bladeren voor gebruik in Windows 10-kiosken voor één app. Er wordt een versie met meerdere tabbladen van Microsoft Edge uitgevoerd.
- **Normale modus (kiosk voor meerdere apps)** : Hiermee worden Microsoft Edge-instellingen gefilterd die van toepassing zijn op de normale Microsoft Edge-kioskmodus. Er wordt een volledige versies van Microsoft Edge uitgevoerd met alle browserfuncties.
- **Openbaar bladeren (kiosk voor meerdere apps)** : Hiermee worden Microsoft Edge-instellingen gefilterd die van toepassing zijn op openbaar bladeren in een Windows 10-kiosk voor meerdere apps.  Er wordt een versie met meerdere tabbladen van Microsoft Edge InPrivate uitgevoerd.

> [!TIP]
> Zie [Configuratietypen van de Microsoft Edge-kioskmodus](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).voor meer informatie over deze opties.

Dit apparaatbeperkingsprofiel is direct gerelateerd aan het kioskprofiel dat u maakt met behulp van de [Windows-kioskinstellingen](kiosk-settings-windows.md). Samenvatting:

1. Maak het profiel [Windows-kioskinstellingen](kiosk-settings-windows.md) om het apparaat in de kioskmodus uit te voeren. Selecteer Microsoft Edge als de toepassing en stel de Microsoft Edge-kioskmodus in het Kioskprofiel in.
2. Maak het apparaatbeperkingsprofiel dat in dit artikel wordt beschreven en configureer specifieke functies en instellingen die zijn toegestaan in Microsoft Edge. Zorg ervoor dat u hetzelfde type Microsoft Edge-kioskmodus selecteert als is geselecteerd in uw kioskprofiel ([Windows-kioskinstellingen](kiosk-settings-windows.md)). 

    [Ondersteunde kioskmodusinstellingen](https://docs.microsoft.com/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) is een geweldige resource.

> [!IMPORTANT] 
> Zorg ervoor dat u dit Microsoft Edge-profiel toewijst aan de dezelfde apparaten als uw kioskprofiel ([Windows-kioskinstellingen](kiosk-settings-windows.md)).

[ConfigureKioskMode CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>Gebruikerservaring

- **Microsoft Edge starten met**: Kies welke pagina's worden geopend wanneer Microsoft Edge wordt gestart. Uw opties zijn:
  - **Aangepaste startpagina 's**: Geef de startpagina's op, bijvoorbeeld `http://www.contoso.com`. De startpagina's die u invoert, worden in Microsoft Edge geladen.
  - **Nieuwe tabbladpagina**: In Microsoft Edge wordt geladen wat er is gedefinieerd in de instelling **URL van nieuw tabblad**.
  - **Pagina van laatste sessie**: Microsoft Edge laden met de pagina van de laatste sessie.
  - **Startpagina's in lokale app-instellingen**: Microsoft Edge starten met de standaardstartpagina zoals gedefinieerd door het besturingssysteem.

- **Toestaan dat de gebruiker de startpagina's kan wijzigen**: Met **Ja** (standaard) kunnen gebruikers de startpagina's wijzigen. Beheerders kunnen gebruikmaken van de `EdgeHomepageUrls` om de startpagina's in te voeren die gebruikers standaard zien wanneer ze Microsoft Edge openen. Met **Nee** kunnen gebruikers de startpagina's niet wijzigen.
- **Webinhoud toestaan op nieuwe tabbladpagina**: Met **Ja** (standaard) wordt in Microsoft Edge de URL geopend die is gedefinieerd in de instelling **URL van nieuw tabblad**. Als **URL van nieuw tabblad** leeg is, wordt het nieuwe tabblad geopend dat is vermeld in de Microsoft Edge-instellingen. Gebruikers kunnen dit wijzigen. Als deze optie is ingesteld op **Nee**, wordt in Microsoft Edge een nieuw tabblad met een lege pagina geopend. Gebruikers kunnen dit niet wijzigen.
- **URL van nieuw tabblad**: Voer de URL in die moet worden geopend op de pagina Nieuw tabblad. Voer bijvoorbeeld `https://www.bing.com` of `https://www.contoso.com` in.

- **De knop Start**: U kunt selecteren wat er gebeurt wanneer de knop Start wordt geselecteerd. Uw opties zijn:
  - **Startpagina's**: Hiermee wordt de optie geopend die u hebt gekozen voor **Microsoft Edge starten met**
  - **Nieuwe tabbladpagina**: Hiermee opent u de URL die u hebt ingevoerd in **URL van nieuw tabblad**.
  - **URL van startknop**: Voer de te openen URL in. Voer bijvoorbeeld `https://www.bing.com` of `https://www.contoso.com` in.
  - **De knop Start verbergen**: Hiermee verbergt u de knop Start
- **Gebruikers toestaan om de knop Start te wijzigen**: Met **Ja** kunnen gebruikers de knop Start wijzigen. Met wijzigingen van de gebruiker worden instellingen van een beheerder voor de knop Start overschreven. Met **Geen** (standaard) kunnen gebruikers de indeling van de knop Start van de beheerder niet wijzigen.
- **Pagina voor first-run experience weergeven (alleen mobiel)** : Met **Ja** (standaard) wordt de eerste introductiepagina in Microsoft Edge weergegeven. Met **Nee** wordt de introductiepagina niet weergegeven wanneer Microsoft Edge de eerste keer wordt uitgevoerd. Bedrijven kunnen deze functie gebruiken om deze pagina te blokkeren, bijvoorbeeld omdat ze werken met 'zero configuration'.
- **Locatie van de lijst met URL's van first-run experience** (alleen Windows 10 Mobile): Voer de URL in die verwijst naar het XML-bestand met de URL('s) van de pagina voor eerste uitvoering. Voer bijvoorbeeld `https://www.contoso.com/sites.xml` in.

- **De browser vernieuwen na niet-actieve tijd**: Voer het aantal niet-actieve minuten, tussen 0 en 1440, in waarna de browser wordt vernieuwd. De standaard is `5` minuten. Als de waarde is ingesteld op `0` (nul), wordt de browser niet vernieuwd na inactiviteit.

  Deze instelling is alleen beschikbaar bij uitvoering in [Inprivate openbaar bladeren (kiosk voor één app)](#use-microsoft-edge-kiosk-mode).

- **Pop-ups toestaan** (alleen desktop): Met **Ja** (standaard) zijn pop-ups toegestaan in de webbrowser. Met **Nee** worden pop-upvensters niet in de browser weergegeven.
- **Intranetverkeer naar Internet Explorer sturen** (alleen desktop): Met **Ja** kunnen gebruikers intranetwebsites in Internet Explorer openen in plaats van in Microsoft Edge. Deze instelling is bedoeld voor achterwaartse compatibiliteit. Met **Nee** (standaard) kunnen gebruikers Microsoft Edge gebruiken.
- **Locatie van de lijst met websites van Bedrijfsmodus** (alleen desktop): Voer de URL in die wijst naar het XML-bestand met een lijst met websites die in Bedrijfsmodus worden geopend. Gebruikers kunnen deze lijst niet wijzigen. Voer bijvoorbeeld `https://www.contoso.com/sites.xml` in.
- **Bericht bij openen van sites in Internet Explorer**: Gebruik deze instelling om Microsoft Edge zo te configureren dat er een melding wordt weergeven voordat een site wordt geopend in Internet Explorer 11. Uw opties zijn:
  - **Bericht niet weergeven**: Het standaardgedrag van het besturingssysteem wordt gebruikt, waardoor er mogelijk geen bericht wordt weergegeven.
  - **Bericht weergeven dat de site wordt geopend in Internet Explorer 11**: Geef het bericht weer bij het openen van sites in Internet Explorer. Sites worden geopend in IE. 
  - **Bericht met de optie voor het openen van sites in Microsoft Edge weergeven**: Bericht weergeven bij openen van sites in Microsoft Edge. Het bericht bevat een koppeling **Verdergaan in Microsoft Edge**, zodat gebruikers Microsoft Edge kunnen kiezen in plaats van Internet Explorer.

  > [!IMPORTANT]
  > Voor deze instelling moet u de instelling **Locatie van de lijst met websites van Bedrijfsmodus**, de instelling **Intranetverkeer naar Internet Explorer sturen** of beide instellingen inschakelen.

- **Compatibiliteitslijst van Microsoft toestaan**: Met **Ja** (standaard) kan een compatibiliteitslijst van Microsoft worden gebruikt. Met **Nee**wordt de Microsoft-compatibiliteitslijst voorkomen in Microsoft Edge. Deze lijst van Microsoft helpt Microsoft Edge om sites met bekende compatibiliteitsproblemen toch goed weer te geven.
- **Startpagina's en nieuw tabblad vooraf laden**: Met **Ja** (standaard) wordt gebruikgemaakt van het standaardgedrag van het besturingssysteem, wat inhoudt dat deze pagina's mogelijk vooraf worden geladen. Vooraf laden minimaliseert de tijd voor het starten van Microsoft Edge en het laden van nieuwe tabbladen. Met **Nee** wordt voorkomen dat er vooraf startpagina's en een nieuw tabblad worden geladen door Microsoft Edge.
- **Startpagina's en nieuw tabblad vooraf starten**: Met **Ja** (standaard) wordt gebruikgemaakt van het standaardgedrag van het besturingssysteem, wat inhoudt dat deze pagina's mogelijk vooraf worden gestart. Vooraf starten verbetert de prestaties van Microsoft Edge en minimaliseert de tijd die nodig is om Microsoft Edge te starten. Met **Nee** wordt voorkomen dat er vooraf startpagina's en een nieuw tabblad worden gestart door Microsoft Edge.

### <a name="favorites-and-search"></a>Favorieten en zoeken

- **Werkbalk Favorieten weergeven**: Stel in wat er moet gebeuren met de werkbalk Favorieten op een pagina van Microsoft Edge. Uw opties zijn:
  - **Op startpagina en nieuwe tabbladen**: Hiermee wordt de werkbalk Favorieten weergegeven wanneer Microsoft Edge wordt gestart en op alle tabbladen. Gebruikers kunnen deze instelling wijzigen.
  - **Op alle pagina's**: Hiermee toont u de werkbalk Favorieten op alle pagina's. Gebruikers kunnen deze instelling niet wijzigen.
  - **Verborgen:** : Hiermee verbergt u de werkbalk Favorieten op alle pagina's. Gebruikers kunnen deze instelling niet wijzigen.
- **Wijzigingen in Favorieten toestaan**: Met **Ja** (standaard) wordt de standaardinstelling van het besturingssysteem gebruikt, waardoor gebruikers de lijst kunnen wijzigen. Met **Nee** wordt voorkomen dat gebruikers items aan de lijst met favorieten toevoegen, of de lijst importeren, sorteren of bewerken.
  - **Lijst met favorieten**: Voeg een lijst met URL's toe aan het bestand met favorieten. Voeg bijvoorbeeld `http://contoso.com/favorites.html` toe.
- **Favorieten synchroniseren tussen Microsoft-browsers** (alleen desktop): Met **Ja** stelt u in dat favorieten moeten worden gesynchroniseerd tussen Internet Explorer en Microsoft Edge. Toevoegingen, verwijderingen, aanpassingen en wijzigingen van de volgorde worden gedeeld tussen browsers.  Met **Nee** (standaard) wordt de standaardinstelling van het besturingssysteem gebruikt, zodat gebruikers mogelijk zelf kunnen bepalen of ze favorieten willen synchroniseren tussen de browsers.
- **Standaardzoekmachine**: Selecteer de zoekmachine die u standaard op het apparaat wilt gebruiken. Gebruikers kunnen deze waarde op elk moment wijzigen. Uw opties zijn:
  - Zoekmachine in de clientinstellingen voor Microsoft Edge
  - Bing
  - Google
  - Yahoo
  - Aangepaste waarde: Typ in **OpenSearch-Xml-URL** een HTTPS-URL met het XML-bestand dat ten minste de korte naam en de URL naar het zoekprogramma bevat. Voer bijvoorbeeld `https://www.contoso.com/opensearch.xml` in.
- **Zoeksuggesties weergeven**: Met **Ja** (standaard) stelt u in dat het zoekprogramma sites kan voorstellen wanneer u zoektermen typt op de adresbalk. Met **Nee** wordt deze functie geblokkeerd.
- **Zoekprogrammawijzigingen toestaan**: Met **Ja** (standaard) kunnen gebruikers nieuwe zoekprogramma's toevoegen of het standaardzoekprogramma in Microsoft Edge wijzigen. Kies **Nee** om te voorkomen dat gebruikers het zoekprogramma aanpassen.

  Deze instelling is alleen beschikbaar bij uitvoering in de [Normale modus (kiosk voor meerdere apps)](#use-microsoft-edge-kiosk-mode).

### <a name="privacy-and-security"></a>Privacy en beveiliging

- **InPrivate-browsing toestaan**: Met **Ja** (standaard) is InPrivate-browsing in Microsoft Edge toegestaan. Nadat alle InPrivate-tabbladen zijn gesloten, worden de browsegegevens van het apparaat verwijderd. Met **Nee** voorkomt u dat gebruikers InPrivate-navigatiesessies kunnen openen.
- **Browsegeschiedenis opslaan**: Met **Ja** (standaard) kan de browsegeschiedenis in Microsoft Edge worden opgeslagen. Met **Nee** kan de browsegeschiedenis niet worden opgeslagen.
- **Browsegegevens wissen bij afsluiten** (alleen desktop): Met **Ja** worden de geschiedenis en de browsegegevens gewist wanneer gebruikers Microsoft Edge afsluiten. Met **Nee** (standaard) wordt de standaardinstelling van het besturingssysteem gebruikt, waardoor de browsegegevens mogelijk in de cache worden opgeslagen.
- **Browserinstellingen synchroniseren tussen apparaten van gebruiker**: Geef aan hoe u browserinstellingen wilt synchroniseren tussen apparaten. Uw opties zijn:
  - **Toestaan**: Synchronisatie van Microsoft Edge-browserinstellingen tussen apparaten van de gebruiker toestaan
  - **Blokkeren en overschrijven door gebruiker inschakelen**: Synchronisatie van Microsoft Edge-browserinstellingen tussen apparaten van de gebruiker blokkeren. Gebruikers kunnen deze instelling wijzigen.
  - **Blokkeren**: De synchronisatie van Microsoft Edge-browserinstellingen tussen apparaten van de gebruiker wordt geblokkeerd. Gebruikers kunnen deze instelling niet wijzigen.

Als de functie is ingesteld op Blokkeren en overschrijven door gebruiker inschakelen, kan de gebruiker de toewijzing door een beheerder negeren.

- **Wachtwoordbeheer toestaan**: Met **Ja** (standaard) kan Wachtwoordbeheer worden gebruikt in Microsoft Edge, waardoor gebruikers wachtwoorden op het apparaat kunnen opslaan en beheren. Met **Nee** kan Wachtwoordbeheer niet in Microsoft Edge worden gebruikt.
- **Cookies**: Geef aan hoe cookies worden verwerkt in de browser. Uw opties zijn:
  - **Toestaan**: Cookies worden op het apparaat opgeslagen.
  - **Alle cookies blokkeren**: Cookies worden niet op het apparaat opgeslagen.
  - **Alleen cookies van derden blokkeren**: Cookies van derden of partners worden niet op het apparaat opgeslagen.
- **Automatisch invullen van formulieren toestaan**: Met **Ja** (standaard) kunnen gebruikers de instellingen voor automatisch invullen in de browser wijzigen en formuliervelden automatisch invullen. Met **Nee** wordt de functie Automatisch invullen uitgeschakeld in Microsoft Edge.
- **Do Not Track headers toestaan**: Met **Ja** worden Do Not Track-headers verzonden naar websites die traceringsgegevens aanvragen (aanbevolen). Met **Nee** (standaard) worden geen headers verzonden zodat websites de gebruiker kunnen volgen. Gebruikers kunnen deze instelling configureren.
- **Localhost IP-adres voor WebRTC weergeven**: Met **Ja** (standaard) kan het IP-adres van de Localhost van gebruikers worden weergegeven bij het plaatsen van telefoonoproepen met behulp van dit protocol. Met **Nee** wordt het localhost IP-adres van gebruikers niet weergegeven. 
- **Verzamelen van gegevens van Live-tegel toestaan**: Met **Ja** (standaard) kan Microsoft Edge gegevens verzamelen van Live-tegels die zijn vastgemaakt in het menu Start. Met **Nee** wordt voorkomen dat deze gegevens worden verzameld, waardoor de ervaring van gebruikers mogelijk wordt beperkt.
- **Gebruiker kan certificaatfouten negeren**: Met **Ja** (standaard) hebben gebruikers toegang tot websites met SSL- of TLS-fouten (Secure Sockets Layer/Transport Layer Security). Met **Nee** (aanbevolen voor een betere beveiliging) hebben gebruikers geen toegang tot dergelijke websites.

### <a name="additional"></a>Aanvullend

- **Microsoft Edge-browser toestaan (alleen mobiel)** : Met **Ja** (standaard) kan de webbrowser Microsoft Edge worden gebruikt op het apparaat. Met **Nee** is het gebruik van Microsoft Edge op apparaten niet toegestaan. Als u **Nee** kiest, gelden de afzonderlijke instellingen alleen voor het desktopapparaat.
- **Vervolgkeuzelijst van de adresbalk toestaan**: Met **Ja** (standaard) kan Microsoft Edge de vervolgkeuzelijst van de adresbalk met een lijst met suggesties weergeven. Met **Nee** voorkomt u dat er in Microsoft Edge een lijst met suggesties wordt weergegeven wanneer u typt in het invoervak van een vervolgkeuzelijst. Als deze optie is ingesteld op **Nee** kunt u:
  - De netwerkbandbreedte beperken die nodig is tussen Microsoft Edge en Microsoft-services.
  - Schakel **Zoek- en websitesuggesties weergeven terwijl ik typ** in Microsoft Edge > Instellingen uit.
- **Modus volledig scherm toestaan**: Met **Ja** (standaard) kan de modus Volledig scherm in Microsoft Edge worden gebruikt, waarbij alleen de webinhoud wordt weergegeven en de gebruikersinterface wordt verborgen. Met **Nee** kan de modus Volledig scherm niet worden ingeschakeld in Microsoft Edge.
- **De pagina about:flags toestaan**: Met **Ja** wordt het standaardgedrag van het besturingssysteem gebruikt, wat kan betekenen dat de pagina `about:flags` toegankelijk is. Op de pagina `about:flags` kunnen gebruikers instellingen voor ontwikkelaars wijzigen en experimentele functies inschakelen. Met **Nee** wordt voorkomen dat gebruikers toegang hebben tot de pagina `about:flags` in Microsoft Edge.
- **Ontwikkelhulpprogramma's toestaan**: Met **Ja** (standaard) kunnen gebruikers standaard de F12-ontwikkelhulpprogramma's gebruiken om webpagina's te maken en problemen op te sporen. Met **Nee** hebben gebruikers geen toegang tot de F12-ontwikkelhulpprogramma's.
- **JavaScript toestaan**: Met **Ja** (standaard) staat u de uitvoering van scripts, zoals JavaScript, toe in de Microsoft Edge-browser. Met **Nee** kunnen er geen JavaScripts worden uitgevoerd in de browser.
- **Gebruiker kan extensies installeren**: Met **Ja** (standaard) kunnen gebruikers extensies van Microsoft Edge installeren op apparaten. Met **Nee** wordt de installatie hiervan voorkomen.
- **Sideloaden van ontwikkelaarsuitbreidingen toestaan**: Met **Ja** (standaard) wordt het standaardgedrag van het besturingssysteem gebruikt, wat kan betekenen dat sideloaden is toegestaan. Met sideloading worden niet-geverifieerde extensies geïnstalleerd en uitgevoerd. Met **Nee** voorkomt u sideloading via de functie **Extensies laden**. Hiermee voorkomt u niet het sideloaden van extensies op andere manieren, zoals via PowerShell.
- **Vereiste extensies**: Kies welke extensies niet kunnen worden uitgeschakeld door gebruikers in Microsoft Edge. Voer de familienamen van pakketten in en selecteer **Toevoegen**. [Een PFN (Package Family Name) zoeken voor VPN per app](https://docs.microsoft.com/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn) bevat meer informatie.

  U kunt ook een CSV-bestand **importeren** met de familienamen van pakketten. Of u kunt de familienamen **exporteren** van pakketten die u invoert.

## <a name="network-proxy"></a>Netwerkproxy

Deze instellingen gebruiken de [beleid-CSP NetworkProxy](https://docs.microsoft.com/windows/client-management/mdm/networkproxy-csp), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Proxy-instellingen automatisch detecteren**: Met **Blokkeren** wordt de automatische detectie van een PAC-script (proxy auto config) op apparaten uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan deze functie standaard inschakelen en apparaten proberen het pad naar een PAC-script te vinden.
- **Proxyscript gebruiken**: Met **Toestaan** kunt u een pad naar uw PAC-script opgeven om de proxyserver te configureren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het is mogelijk dat het besturingssysteem u standaard geen URL naar een PAC-script laat invoeren.
  - **URL voor het installatiescriptadres**: Geef de URL op van een PAC-script dat u wilt gebruiken om de proxyserver te configureren.
- **Handmatige proxyserver gebruiken**: Kies **Toestaan** om handmatig de naam of het IP-adres en het TCP-poortnummer van een proxyserver in te voeren. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het is mogelijk dat het besturingssysteem u standaard geen gegevens van een proxyserver laat invoeren.
  - **Adres**: Voer de naam of het IP-adres van de proxyserver in.
  - **Poortnummer**: Voer het poortnummer van uw proxyserver in.
  - **Proxy-uitzonderingen**: Voer URL's in die geen gebruik mogen maken van de proxyserver. Scheid de items van elkaar met een puntkomma (`;`).
  - **Proxyserver niet gebruiken voor lokale adressen**: **Toestaan** maakt geen gebruik van de proxyserver voor lokale intranetadressen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem gebruikmaken van een proxyserver voor lokale adressen op uw intranet.

## <a name="password"></a>Wachtwoord

Deze instellingen gebruiken de [beleid-CSP DeviceLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Wachtwoord**: Met **Vereisen** moeten gebruikers een wachtwoord invoeren om toegang te krijgen tot het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem toegang tot apparaten zonder wachtwoord toestaat. Is alleen van toepassing op lokale accounts. Wachtwoorden van domeinaccounts blijven geconfigureerd door Active Directory (AD) en Azure AD.

  [DeviceLock/DevicePasswordEnabled CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - **Vereist wachtwoordtype**: Kies het type wachtwoord. Uw opties zijn:
    - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard kan het besturingssysteem toestaan dat het wachtwoord cijfers en letters bevat.
    - **Alfanumeriek**: Het wachtwoord moet een combinatie van cijfers en letters zijn.
    - **Numeriek**: Het wachtwoord mag alleen uit cijfers bestaan.

    [DeviceLock/AlphanumericDevicePasswordRequired CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - **Minimale wachtwoordlengte**: Voer het minimumaantal vereiste tekens (tussen 4 en 16 tekens) in. Voer bijvoorbeeld `6` in om in te stellen dat een wachtwoord minimaal 6 tekens bevat. Standaard kan dit in het besturingssysteem zijn ingesteld op `4`.
  
    [DeviceLock/MinDevicePasswordLength CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > Als de wachtwoordvereiste op een Windows-bureaublad wordt gewijzigd, heeft dit invloed op gebruikers de volgende keer dat ze zich aanmelden, omdat apparaten op dat moment van niet-actief naar actief gaat. Gebruikers met wachtwoorden die aan de vereisten voldoen, worden nog steeds gevraagd hun wachtwoord te wijzigen.

  - **Aantal mislukte aanmeldingen voordat een apparaat wordt gewist**: Voer het aantal onjuiste wachtwoorden in dat is toegestaan voordat het apparaat wordt gewist, maximaal elf keer. Het geldige nummer dat u invoert, is afhankelijk van de editie. Bij [DeviceLock/MaxDevicePasswordFailedAttempts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) vindt u een lijst met de ondersteunde waarden. Met `0` (nul) kan de functionaliteit voor het wissen van apparaten worden uitgeschakeld.

    Deze instelling heeft per editie een verschillend effect. Raadpleeg [DeviceLock/MaxDevicePasswordFailedAttempts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) voor meer informatie over deze instelling.

  - **Maximum aantal minuten van inactiviteit voordat het scherm wordt vergrendeld**: Voer de tijdsduur in dat een apparaat inactief moet zijn voordat het scherm wordt vergrendeld. Voer bijvoorbeeld `5` in om apparaten te vergrendelen nadat deze vijf minuten lang inactief zijn geweest. Wanneer dit is ingesteld op **Niet geconfigureerd**, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan dit in het besturingssysteem zijn ingesteld op `0` (nul). Dit is geen time-out.

    [DeviceLock/MaxInactivityTimeDeviceLock CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **Wachtwoordverlooptijd (dagen)** : Voer de tijdsduur in waarna het wachtwoord van een apparaat moet worden gewijzigd (tussen 1-365). Voer bijvoorbeeld `90` als u wilt dat het wachtwoord na 90 dagen verloopt. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan dit in het besturingssysteem zijn ingesteld op `0` (nul). Dit is geen vervaldatum.

    [DeviceLock/DevicePasswordExpiration CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **Wachtwoorden niet opnieuw gebruiken**: Voer het aantal eerder gebruikte wachtwoorden in dat niet opnieuw mag worden gebruikt, van 1 tot 24. Als u bijvoorbeeld `5` invoert, kan een gebruiker zijn nieuwe wachtwoord niet instellen op zijn huidige wachtwoord of een van zijn vier wachtwoorden daarvoor. Wanneer de waarde leeg is, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

    [DeviceLock/DevicePasswordHistory CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **Wachtwoord vereisen wanneer het apparaat wordt geactiveerd vanuit een niet-actieve status** (mobiel en Holographic): Met **Vereisen** moeten gebruikers een wachtwoord opgeven om het apparaat te ontgrendelen na een periode van inactiviteit. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem geen pincode of wachtwoord vereist.

    [DeviceLock/AllowIdleReturnWithoutPassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **Eenvoudige wachtwoorden**: Met **Blokkeren** voorkomt u dat gebruikers eenvoudige wachtwoorden kunnen maken, zoals `1234` of `1111`. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat gebruikers eenvoudige wachtwoorden mogen maken. Deze instelling blokkeert ook het gebruik van afbeeldingswachtwoorden.

    [DeviceLock/AllowSimpleDevicePassword CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **Automatische versleuteling tijdens AADJ**: Met **Blokkeren** voorkomt u automatische BitLocker-apparaatversleuteling wanneer apparaten worden voorbereid op het eerste gebruik en wanneer apparaten zijn toegevoegd aan Microsoft Azure AD. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat versleuteling is ingeschakeld.

  Zie [BitLocker-apparaatversleuteling](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **FIPS-beleid (Federal Information Processing Standard)** : Met **Toestaan** wordt gebruik gemaakt van het FIPS-beleid (Federal Information Processing Standard). Dit is een standaard van de Amerikaanse overheid voor versleuteling, hashing en ondertekening. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem geen Federal Information Processing Standard toestaat.

  [Cryptography/AllowFipsAlgorithmPolicy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Windows Hello-apparaatverificatie**: U kunt gebruikers **Toestaan** om zich via een Windows Hello-bedrijfsapparaat, zoals een telefoon, fitnessband of IoT-apparaat, aan te melden bij een Windows 10-computer. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem verhinderen dat Windows Hello-bedrijfsapparaten worden geverifieerd.

  [Authentication/AllowSecondaryAuthenticationDevice CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Azure Active Directory-voorkeurstenantdomein**: Voer een bestaande domeinnaam in uw Azure AD-organisatie in. Wanneer gebruikers in dit domein zich aanmelden, hoeven ze de domeinnaam niet te typen. Voer bijvoorbeeld `contoso.com` in. Gebruikers in het `contoso.com`-domein kunnen zich aanmelden met hun gebruikersnaam, bijvoorbeeld `abby` in plaats van `abby@contoso.com`.

  [Authentication/PreferredAadTenantDomainName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>Privacy-uitzonderingen per app

Apps **Toevoegen** die een ander privacybeleid moeten hebben dan wat u definieert als 'Standaardprivacy'.

- **Pakketnaam**: De familienaam van het pakket.
- **App-naam**: De naam van de app.

### <a name="exceptions"></a>Uitzonderingen

- **Accountgegevens**: Geef aan of deze app toegang heeft tot de gebruikersnaam, afbeelding en andere contactgegevens.
- **Achtergrond-apps**: Geef aan of deze app op de achtergrond kan worden uitgevoerd.
- **Agenda**: Geef aan of deze app toegang heeft tot de agenda.
- **Oproepgeschiedenis**: Geef aan of deze app toegang heeft tot mijn oproepgeschiedenis.
- **Camera**: Geef aan of deze app toegang heeft tot de camera.
- **Contactpersonen**: Geef aan of deze app toegang heeft tot contactpersonen.
- **E-mail**: Geef aan of deze app toegang heeft tot e-mail en of de app e-mail kan verzenden.
- **Locatie**: Geef aan of deze app toegang heeft tot locatiegegevens.
- **Berichten**: Geef aan of deze app sms- of mms-berichten kan lezen of verzenden.
- **Microfoon**: Geef aan of deze app de microfoon kan gebruiken.
- **Beweging**: Geef aan of deze app toegang heeft tot bewegingsinformatie van het apparaat.
- **Meldingen**: Geef aan of deze app toegang heeft tot meldingen.
- **Telefoon**: Geef aan of deze app toegang heeft tot de telefoon.
- **Radio's**: Sommige apps maken gebruik van radio's (bijvoorbeeld Bluetooth) in uw apparaat voor het verzenden en ontvangen van gegevens en moeten deze radio's kunnen in- of uitschakelen. Geef aan of deze app deze radio's kan beheren.
- **Taken**: Geef aan of deze app toegang heeft tot uw taken.
- **Vertrouwde apparaten**: Geef aan of deze app gebruik kan maken van vertrouwde apparaten. Onder vertrouwde apparaten wordt hardware verstaan die u al hebt aangesloten of die bij deze pc, tablet of telefoon wordt geleverd. Gebruik tv's, projectoren enzovoort bijvoorbeeld als vertrouwde apparaten.
- **Feedback en diagnostische gegevens**: Geef aan of deze app toegang heeft tot diagnostische gegevens.
- **Synchroniseren met apparaten**: Geef aan of deze app automatisch informatie kan delen en synchroniseren met draadloze apparaten die niet expliciet aan dit apparaat zijn gekoppeld.

## <a name="personalization"></a>Persoonlijke instellingen

Deze instellingen gebruiken de [beleid-CSP Personalization](https://docs.microsoft.com/windows/client-management/mdm/personalization-csp), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **URL achtergrondafbeelding Bureaublad (alleen desktop)** : Voer de URL in naar een afbeelding in JPG-, JPEG- of PNG-indeling die u wilt gebruiken als de achtergrond van het Windows-bureaublad. Gebruikers kunnen de afbeelding niet wijzigen. Voer bijvoorbeeld `https://contoso.com/logo.png` in.

  Als u dit leeg laat, wordt deze instelling niet gewijzigd of bijgewerkt door Intune.

## <a name="printer"></a>Printer

- **Printers**: Printers toevoegen met behulp van hun netwerkhostnamen (DNS-naam). Het besturingssysteem zoekt en installeert overeenkomende printerstuurprogramma's voor elke printer op het apparaat. Als u geen waarde invoert, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Education/PrinterNames CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-printernames)

- **Standaardprinter**: Voer de netwerkhostnaam (DNS-naam) in van een geïnstalleerde printer die moet worden gebruikt als de standaardprinter. Als u geen waarde invoert, wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Education/DefaultPrinterName CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **Nieuwe printers toevoegen**: Met **Blokkeren** voorkomt u dat gebruikers nieuwe printers kunnen toevoegen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem het toevoegen van nieuwe printers toestaan.

  [Education/PreventAddingNewPrinters CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## <a name="privacy"></a>Privacy

Deze instellingen gebruiken de [beleid-CSP Privacy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Privacy-ervaring**: Met **Blokkeren** wordt voorkomen dat de privacy-ervaring wordt geopend wanneer gebruikers zich aanmelden en dat nieuwe en bijgewerkte gebruikers worden geopend. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Privacy/DisablePrivacyExperience](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **Persoonlijke instellingen invoeren**: Met **Blokkeren** voorkomt u het gebruik van dicteren en communiceren met Cortana en andere apps die gebruikmaken van op de cloud gebaseerde spraakherkenning van Microsoft. Als deze optie is uitgeschakeld, kunnen gebruikers online spraakherkenning niet inschakelen via de instellingen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat het gebruikers is toegestaan te kiezen. Als u deze services toestaat, kan Microsoft spraakgegevens verzamelen voor het verbeteren van de service.

  [Privacy/AllowInputPersonalization CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **Automatische acceptatie van de goedkeuringsvensters voor koppelen en privacy**: Kies **Toestaan** zodat Windows automatisch toestemmingsberichten voor koppelen en privacy kan accepteren bij het uitvoeren van apps. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat automatische acceptatie wordt verhinderd.

  [Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **Gebruikersactiviteiten publiceren**: Met **Blokkeren** wordt voorkomen dat apps en het besturingssysteem gebruikersactiviteiten publiceren. Het voorkomt ook gedeelde ervaringen en detectie van recent gebruikte resources in de activiteitenfeed. Gebruikersactiviteiten volgen de status van de taken van een gebruiker in een app of het besturingssysteem. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem deze functie inschakelen, zodat apps gebruikersactiviteiten kunnen publiceren.

  [Privacy/PublishUserActivities CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **Alleen lokale activiteiten**: Met **Blokkeren** voorkomt u gedeelde ervaringen en de detectie van recent gebruikte resources in de taakwisselaar alleen op basis van de lokale activiteit. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

U kunt informatie configureren die voor alle apps op het apparaat toegankelijk is. Definieer ook uitzonderingen op een per-app basis met **Privacyuitzonderingen per app**.

### <a name="exceptions"></a>Uitzonderingen

- **Accountgegevens**: Geef aan of deze app toegang heeft tot de gebruikersnaam, afbeelding en andere contactgegevens.
- **Achtergrond-apps**: Geef aan of deze app op de achtergrond kan worden uitgevoerd.
- **Agenda**: Geef aan of deze app toegang heeft tot de agenda.
- **Oproepgeschiedenis**: Geef aan of deze app toegang heeft tot mijn oproepgeschiedenis.
- **Camera**: Geef aan of deze app toegang heeft tot de camera.
- **Contactpersonen**: Geef aan of deze app toegang heeft tot contactpersonen.
- **E-mail**: Geef aan of deze app toegang heeft tot e-mail en of de app e-mail kan verzenden.
- **Locatie**: Geef aan of deze app toegang heeft tot locatiegegevens.
- **Berichten**: Geef aan of deze app sms- of mms-berichten kan lezen of verzenden.
- **Microfoon**: Geef aan of deze app de microfoon kan gebruiken.
- **Beweging**: Geef aan of deze app toegang heeft tot bewegingsinformatie van het apparaat.
- **Meldingen**: Geef aan of deze app toegang heeft tot meldingen.
- **Telefoon**: Geef aan of deze app toegang heeft tot de telefoon.
- **Radio's**: Sommige apps maken gebruik van radio's (bijvoorbeeld Bluetooth) in uw apparaat voor het verzenden en ontvangen van gegevens en moeten deze radio's kunnen in- of uitschakelen. Geef aan of deze app deze radio's kan beheren.
- **Taken**: Geef aan of deze app toegang heeft tot uw taken.
- **Vertrouwde apparaten**: Geef aan of deze app gebruik kan maken van vertrouwde apparaten. Onder vertrouwde apparaten wordt hardware verstaan die u al hebt aangesloten of die bij deze pc, tablet of telefoon wordt geleverd. Gebruik tv's, projectoren enzovoort bijvoorbeeld als vertrouwde apparaten.
- **Feedback en diagnostische gegevens**: Geef aan of deze app toegang heeft tot diagnostische gegevens.
- **Synchroniseren met apparaten**: geef aan of deze app gegevens automatisch kan delen en synchroniseren met draadloze apparaten die niet expliciet aan deze pc, tablet of telefoon zijn gekoppeld.

## <a name="projection"></a>Projectie

Deze instellingen gebruiken de [beleid-CSP WirelessDisplay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Gebruikersinvoer van ontvangers van draadloze schermen**: Met **Blokkeren** wordt gebruikersinvoer van ontvangers van draadloze schermen voorkomen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem een draadloos scherm toestaan invoer van het toetsenbord, de muis, de pen en het touchoppervlak terug te sturen naar het bronapparaat.

  [WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **Projectie naar deze pc**: Met **Blokkeren** kunnen andere apparaten het projectieapparaat niet meer vinden en wordt projectie naar andere apparaten voorkomen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem apparaten toestaan om te worden gedetecteerd en kan naar het apparaat boven het vergrendelingsscherm worden geprojecteerd.

  [WirelessDisplay/AllowProjectionFromPC CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **Een pincode vereisen voor koppelen**: Met **Vereisen** wordt altijd een pincode vereist voor verbinding met een projectieapparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem geen pincode vereist om het apparaat te koppelen.

  [WirelessDisplay/RequirePinForPairing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## <a name="reporting-and-telemetry"></a>Rapportage en telemetrie

- **Gebruiksgegevens delen**: Kies het niveau van diagnostische gegevens die worden verzonden. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kiezen het niveau dat wordt verzonden. Standaard is het mogelijk dat het besturingssysteem geen gegevens deelt.
  - **Beveiliging**: Informatie die vereist is om Windows beter te beveiligen, inclusief gegevens over de instellingen voor de gevonden gebruikerservaring en telemetrie, het hulpprogramma voor verwijderen van schadelijke software en Microsoft Defender
  - **Standaard**: Basale apparaatgegevens, zoals gegevens met betrekking tot de kwaliteit, app-compatibiliteit, app-gebruiksgegevens en gegevens van het beveiligingsniveau
  - **Uitgebreid**: Extra inzichten, zoals hoe Windows, Windows Server, System Center en apps worden gebruikt, hoe deze presteren en geavanceerde betrouwbaarheidsgegevens, plus gegevens van de niveaus Standaard en Beveiliging
  - **Volledig**: Alle gegevens die nodig zijn om problemen op te sporen en op te lossen, plus gegevens van het niveaus Beveiliging, Standaard en Uitgebreid.

  [System/AllowTelemetry CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **Microsoft Edge-browsegegevens verzenden naar Microsoft 365 Analytics**: Als u deze functie wilt gebruiken, stelt u **Gebruiksgegevens delen** in op **Uitgebreid** of **Volledig**. Deze functie bepaalt welke gegevens Microsoft Edge verstuurt naar Microsoft 365 Analytics voor zakelijke apparaten met een geconfigureerde commerciële id. Uw opties zijn:
  - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard kan zo worden ingesteld dat het besturingssysteem geen browsegeschiedenisgegevens kan verzamelen of verzenden.
  - **Alleen intranetgegevens verzenden**: Hiermee kan de beheerder de geschiedenis van intranetgegevens verzenden.
  - **Alleen internetgegevens verzenden**: Hiermee kan de beheerder de geschiedenis van internetgegevens verzenden.
  - **Intranet- en internetgegevens verzenden**: Hiermee kan de beheerder de geschiedenis van intranet- en internetgegevens verzenden.

  [Browser/ConfigureTelemetryForMicrosoft365Analytics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Telemetrie-proxyserver**: Geef de Fully Qualified Domain Name (FQDN) of het IP-adres van een proxyserver op voor het doorsturen van Connected User Experiences en Telemetrie-aanvragen met behulp van een SSL-verbinding (Secure Sockets Layer). De indeling voor deze instelling is *server*:*poort*. Als de benoemde proxy niet werkt of als er geen proxy is opgegeven, worden de Connected User Experiences en Telemetriegegevens niet verzonden. Het blijft op het lokale apparaat.

  Als u geen waarde invoert, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de Connected User Experiences en Telemetriegegevens naar Microsoft verzenden met behulp van de standaard proxyconfiguratie.

  Voorbeelden van indelingen:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [System/TelemetryProxy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

## <a name="search"></a>Zoeken

Deze instellingen gebruiken de [beleid-CSP Search](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Veilig zoeken (alleen mobiel)** : Hiermee bepaalt u hoe Cortana inhoud voor volwassenen filtert in de zoekresultaten. Uw opties zijn:
  - **Door de gebruiker gedefinieerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kiezen hun eigen instellingen.
  - **Strikt**: De hoogste filtering tegen inhoud voor volwassenen
  - **Gemiddeld**: Gemiddelde filtering tegen inhoud voor volwassenen. Geldige zoekresultaten worden niet gefilterd.
- **Webresultaten weergeven in zoekopdracht**: Met **Blokkeren** voorkomt u dat gebruikers Windows Search kunnen gebruiken om te zoeken op internet en webresultaten worden niet weergegeven in Search. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem gebruikers toestaan op internet te zoeken en worden de resultaten weergegeven op het apparaat.
- **Diakritische tekens**: Met **Blokkeren** voorkomt u dat diakritische tekens in Windows Search worden weergegeven. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard diakritische tekens weergeven.

  [Search/AllowUsingDiacritics CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **Automatische taaldetectie**: Met **Blokkeren** voorkomt u dat Windows Search automatisch de taal detecteert bij het indexeren van inhoud of eigenschappen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.

  [Search/AlwaysUseAutoLangDetection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **Zoeklocatie**: Met **Blokkeren** voorkomt u dat Windows Search de locatie gebruikt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.

  [Search/AllowSearchToUseLocation CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **Uitstelfunctie van indexeerfunctie**: Met **Blokkeren** wordt de uitstelfunctie van indexeerfunctie uitgeschakeld. Het indexeren blijft op volledige snelheid, zelfs als de systeemactiviteit hoog is. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem de logica van de uitstelfunctie gebruiken om de indexeringsactiviteit te vertragen wanneer de systeemactiviteit hoog is.

  [Search/DisableBackoff CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **Indexering van verwisselbaar station**: Met **Blokkeren** voorkomt u dat locaties op verwisselbare stations worden toegevoegd aan bibliotheken en dat deze worden geïndexeerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem deze functie toestaat.

  [Search/DisableRemovableDriveIndexing CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **Indexering bij weinig schijfruimte**: Met **Inschakelen** staat u automatische indexering toe, zelfs wanneer er weinig schijfruimte is. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem automatisch indexeren uitschakelen wanneer de hardeschijfruimte 600 MB of minder is. Als apparaten in uw organisatie over beperkte ruimte op de vaste schijf beschikken, stelt u deze optie in op **Niet geconfigureerd**.

  [Search/PreventIndexingLowDiskSpaceMB CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **Externe query's**: Met **Inschakelen** kunnen externe query's van de index van het apparaat worden uitgevoerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard is het mogelijk dat het besturingssysteem gebruikers verhindert om op de index van het apparaat een query uit te voeren.

  [Search/PreventRemoteQueries CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## <a name="start"></a>start

Deze instellingen gebruiken de [beleid-CSP Start](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start), waarbij ook de ondersteunde Windows-edities worden vermeld.  

- **Indeling van het menu Start**: U kunt een XML-bestand met uw aanpassingen uploaden, inclusief de volgorde waarin de apps worden vermeld en meer. Het XML-bestand overschrijft de standaardindeling van het startmenu. Gebruikers kunnen de door u ingevoerde indeling van het menu Start niet wijzigen.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Start/StartLayout CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **Websites vastmaken aan tegels in het menu Start**: Importeer installatiekopieën van Microsoft Edge. Deze installatiekopieën worden als koppelingen weergegeven in het menu Start van Windows voor desktopapparaten. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Start/ImportEdgeAssets CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **Apps losmaken van de taakbalk**: Met **Blokkeren** voorkomt u dat gebruikers apps kunnen losmaken van de taakbalk. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat gebruikers apps van de taakbalk kunnen losmaken.

  [Start/NoPinningToTaskbar CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **Snelle gebruikerswisseling**: Met **Blokkeren** wordt schakeling tussen gebruikers die gelijkertijd zijn aangemeld voorkomen, zonder dat de gebruikers worden afgemeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn in gesteld dat **Gebruiker wisselen** wordt weergegeven op de tegel Gebruiker.

  [Start/HideSwitchAccount CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Meest gebruikte apps**: Met **Blokkeren** worden de meest gebruikte apps verborgen in het menu Start. Hiermee wordt ook de bijbehorende wisselknop in de Instellingen-app uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat de meest gebruikte apps worden weergegeven.

  [Start/HideFrequentlyUsedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **Onlangs toegevoegde apps**: Met **Blokkeren** worden onlangs toegevoegde apps verborgen in het menu Start. Hiermee wordt ook de bijbehorende wisselknop in de Instellingen-app uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat onlangs toegevoegde apps worden weergegeven in het menu Start.

  [Start/HideRecentlyAddedApps CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **Modus Startscherm**: Kies de grootte van het startscherm. Uw opties zijn:
  - **Door de gebruiker gedefinieerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen de grootte zelf instellen.
  - **Volledig scherm**: Het startscherm wordt schermvullend weergegeven.
  - **Niet-volledig scherm**: Het startscherm wordt gedwongen niet schermvullend weergegeven.

  [Start/ForceStartSize CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **Onlangs geopende items in jumplists**: Met **Blokkeren** worden recente jumplists verborgen in het menu Start en in de taakbalk. Hiermee wordt ook de bijbehorende wisselknop in de Instellingen-app uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat onlangs geopende items worden weergegeven in de jumplists.

  [Start/HideRecentJumplists CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **App-lijst**: Kies hoe de lijst met alle apps wordt weergegeven. Uw opties zijn:
  - **Door de gebruiker gedefinieerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kiezen zelf hoe de lijst met apps wordt weergegeven.
  - **Samenvouwen**: De lijst met alle apps wordt verborgen.
  - **De app Instellingen samenvouwen en uitschakelen**: De lijst met alle apps wordt verborgen en **Lijst met apps weergeven in het menu Start** wordt uitgeschakeld in de app Instellingen.
  - **De app Instellingen verwijderen en uitschakelen**: De lijst met alle apps wordt verborgen, de knop voor het weergeven van alle apps wordt verwijderd en **Lijst met apps weergeven in het menu Start** wordt uitgeschakeld in de app Instellingen.

  [Start/HideAppList CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **Aan/uit-knop**: Met **Blokkeren** wordt de aan/uit-knop niet weergegeven in het menu Start. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat de aan/uit-knop wordt weergegeven.

  [Start/HidePowerButton CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **De tegel Gebruiker**: Met **Blokkeren** wordt de tegel Gebruiker niet weergegeven in het menu Start. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard de tegel Gebruiker weergeven. Configureer de volgende instellingen:
  - **Vergrendelen**: Met **Blokkeren** wordt de optie **Vergrendelen** niet weergegeven op de tegel Gebruiker in het menu Start.  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat de optie **Vergrendelen** wordt weergegeven.
  - **Afmelden**: Met **Blokkeren** wordt de optie **Afmelden** niet weergegeven op de tegel Gebruiker in het menu Start. Met **Niet geconfigureerd** (standaard) wordt de optie **Afmelden** weergegeven.

  [Start/HideUserTile CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **Uitschakelen**: Met **Blokkeren** worden de opties **Bijwerken en afsluiten** en **Afsluiten** niet weergegeven in de aan/uit-knop in het menu Start. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Start/HideShutDown CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **Slaapstand**: Met **Blokkeren** wordt de optie **Slaapstand** niet weergegeven in de aan/uit-knop in het menu Start. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Start/HideSleep CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **Sluimerstand**: Met **Blokkeren** wordt de optie **Sluimerstand** niet weergegeven in de aan/uit-knop in het menu Start. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Start/HideHibernate CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **Account wisselen**: Met **Blokkeren** wordt de optie **Account wisselen** niet weergegeven op de tegel Gebruiker in het menu Start. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Start/HideSwitchAccount CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Opties voor opnieuw opstarten**:  Met **Blokkeren** worden de opties **Bijwerken en opnieuw opstarten** en **Opnieuw opstarten** niet weergegeven in de aan/uit-knop in het menu Start. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

  [Start/HideRestart CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **Documenten op het startscherm**: De map Documenten in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderDocuments CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **Downloads op het startscherm**: De map Downloads in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderDownloads CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **Bestandenverkenner op het startscherm**: Bestandenverkenner in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderFileExplorer CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **Thuisgroep op het startscherm**: De snelkoppeling Thuisgroep in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderHomeGroup CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **Muziek op het startscherm**: De map Muziek in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderMusic CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **Netwerk op het startscherm**: Netwerk op het startscherm in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderNetwork CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **Persoonlijke map op het startscherm**: De Persoonlijke map in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderPersonalFolder CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **Afbeeldingen op het startscherm**: De map Afbeeldingen in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderPictures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **Instellingen op het startscherm**: De snelkoppeling Instellingen in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderSettings CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **Video's op het startscherm**: De map voor video's in het menu Start van Windows weergeven of verbergen. Uw opties zijn:
  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen zelf kiezen of de snelkoppeling wordt weergegeven of verborgen.
  - **Verbergen**: De snelkoppeling wordt verborgen en de instelling in de app Instellingen wordt uitgeschakeld.
  - **Weergeven**: De snelkoppeling wordt weergegeven en de instelling in de app Instellingen wordt uitgeschakeld.

  [Start/AllowPinnedFolderVideos CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen voor Microsoft Edge**: Met **Vereisen** wordt Microsoft Defender SmartScreen ingeschakeld en kunnen gebruikers deze functie niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Het besturingssysteem kan standaard SmartScreen inschakelen en gebruikers toestaan deze in of uit te schakelen.

  Microsoft Edge gebruikt Microsoft Defender SmartScreen (ingeschakeld) om gebruikers tegen mogelijke oplichting door phishing en schadelijke software te beschermen.

  [Browser/AllowSmartScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Toegang tot schadelijke sites**: Met **Blokkeren** kunnen gebruikers de waarschuwingen van het Microsoft Defender SmartScreen-filter niet negeren en kunnen ze niet naar de site gaan. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat gebruikers de waarschuwingen mogen negeren en doorgaan naar de site.

  [Browser/PreventSmartScreenPromptOverride CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Niet-geverifieerd bestand downloaden**: Met **Blokkeren** kunnen gebruikers de Microsoft Defender SmartScreen-filterwaarschuwingen niet negeren en kunnen ze geen niet-geverifieerde bestanden downloaden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat gebruikers waarschuwingen mogen negeren en mogen doorgaan met het downloaden van niet-geverifieerde bestanden.

  [Browser/PreventSmartScreenPromptOverrideForFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Windows Spotlight

Deze instellingen gebruiken de [beleid-CSP Experience](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Windows Spotlight**: Met **Blokkeren** worden Windows-spotlight op het vergrendelingsscherm, Windows Tips, Microsoft-functies voor consumenten en andere gerelateerde functies uitgeschakeld. Als u het netwerkverkeer vanaf apparaten zoveel mogelijk wilt beperken, selecteert u vervolgens **Ja**. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat functies van Windows-spotlight zijn toegestaan en kunnen worden beheerd door gebruikers.

  [Experience/AllowWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  Als deze optie is ingesteld op **Niet geconfigureerd** kunt u de volgende instellingen ook toestaan of blokkeren:

  - **Windows Spotlight op vergrendelingsscherm**: Met**Blokkeren** geeft Windows Spotlight geen informatie weer op het vergrendelingsscherm van het apparaat. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat informatie van Windows-spotlight op het vergrendelingsscherm wordt weergegeven.

    [Experience/ConfigureWindowsSpotlightOnLockScreen CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Suggesties van derden in Windows-spotlight**: Met**Blokkeren** stelt Windows Spotlight geen inhoud voor die niet is gepubliceerd door Microsoft. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat app- en inhoudssuggesties van partners zijn toegestaan en aanbevolen apps worden weergeven in het menu Start en Windows-tips.

    [Experience/AllowThirdPartySuggestionsInWindowsSpotlight CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **Consumentenfuncties**: Met **Blokkeren** worden ervaringen uitgeschakeld die doorgaans voor consumenten worden gebruikt, zoals startsuggesties, lidmaatschapsmeldingen, post-out of box experience-app-installaties en omleidingstegels. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt.

    [Experience/AllowWindowsConsumerFeatures CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Windows Tips**: Met **Blokkeren** worden pop-ups van Windows Tips uitgeschakeld. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem toestaan dat de Windows-tips worden weergegeven.

    [Experience/AllowWindowsTips CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **Windows-spotlight in het Actiecentrum**: Met **Blokkeren** worden meldingen van Windows Spotlight niet weergegeven in Onderhoudscentrum. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat meldingen worden weergegeven in het Onderhoudscentrum, zoals suggesties voor nieuwe apps of functies waarmee gebruikers productiever kunnen zijn.

    [Experience/AllowWindowsSpotlightOnActionCenter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Persoonlijke instellingen voor Windows-Spotlight**: Met **Blokkeren** gebruikt Windows geen diagnostische gegevens om gebruikers aangepaste ervaringen te bieden. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat Microsoft diagnostische gegevens mag gebruiken om persoonlijke aanbevelingen te doen, tips te geven en aanbiedingen weer te geven die op de behoeften van de gebruiker zijn afgestemd.

    [Experience/AllowTailoredExperiencesWithDiagnosticData CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Welkomstbericht van Windows**: Met **Blokkeren** wordt het welkomstbericht van Windows Spotlight uitgeschakeld. Het welkomstbericht van Windows wordt niet weergegeven als er updates en wijzigingen in Windows en Windows-apps zijn. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat het welkomstbericht van Windows is toegestaan waarmee gebruikers worden geïnformeerd over nieuwe of bijgewerkte functies.

    [Experience/AllowWindowsSpotlightWindowsWelcomeExperience CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender Antivirus

Deze instellingen gebruiken de [beleid-CSP Defender](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender), waarbij ook de ondersteunde Windows-edities worden vermeld.

- **Realtimecontrole**: Met **Inschakelen** wordt het real-time scannen op malware, spyware en andere ongewenste software ingeschakeld. Gebruikers kunnen dit niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Deze functie wordt door het besturingssysteem standaard ingeschakeld. Dit kan door gebruikers worden gewijzigd.

  Als u deze instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowRealtimeMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Gedragscontrole**: Met **Inschakelen** worden gedragscontroles en controles op de aanwezigheid van bepaalde bekende patronen van verdachte activiteit op apparaten ingeschakeld. Gebruikers kunnen gedragscontrole niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem Gedragscontrole inschakelen en gebruikers toestaan dit te wijzigen.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowBehaviorMonitoring CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Netwerkinspectiesysteem (NIS)** : NIS helpt bij de bescherming van apparaten tegen aanvallen vanaf het netwerk. NIS maakt gebruik van handtekeningen van bekende beveiligingsproblemen uit het Microsoft Endpoint Protection Center om schadelijk netwerkverkeer te detecteren en blokkeren.

  - **Inschakelen**: Hiermee worden netwerkbeveiliging en netwerkblokkering ingeschakeld. Gebruikers kunnen dit niet uitschakelen. Wanneer deze functie is ingeschakeld, kunnen gebruikers geen verbinding maken met bekende beveiligingsproblemen.

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. NIS wordt door het besturingssysteem standaard ingeschakeld. Dit kan door gebruikers worden gewijzigd.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/EnableNetworkProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Alle downloads scannen**: U schakelt deze instelling in via **Inschakelen**. Hiermee worden door Defender alle bestanden gescand die van internet worden gedownload. Gebruikers kunnen deze instelling niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat deze instelling is ingeschakeld en dat gebruikers dit mogen wijzigen.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowIOAVProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Scripts scannen die in webbrowsers van Microsoft worden geladen**: Met **Inschakelen** laat u Defender scripts scannen die worden gebruikt in Internet Explorer. Gebruikers kunnen deze instelling niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat deze instelling is ingeschakeld en dat gebruikers dit mogen wijzigen.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowScriptScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Toegang van eindgebruikers tot Defender**: Met **Blokkeren** wordt de gebruikersinterface van Microsoft Defender voor gebruikers verborgen. Daarnaast worden alle meldingen van Microsoft Defender onderdrukt. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn in gesteld dat gebruikerstoegang tot de Microsoft Defender-gebruikersinterface is toegestaan en dat gebruikers dit mogen wijzigen.

  Als u de instelling blokkeert en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  Als deze instelling wordt gewijzigd, gaat de wijziging in wanneer het apparaat de volgende keer opnieuw wordt opgestart.

  [Defender/AllowUserUIAccess CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Update-interval voor beveiligingsinformatie (in uur)** : Geef het interval op waarmee Defender op nieuwe beveiligingsinformatie moet controleren (tussen 0-24). Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Volgens het standaardgedrag van het besturingssysteem kan elke 8 uur op updates worden gecontroleerd.
  - **Niet controleren**: Defender controleert niet op nieuwe beveiligingsupdates.
  - **1-24**: `1` controleert elk uur, `2` controleert elke twee uur, `24` controleert elke dag, enzovoort.
  
  [Defender/SignatureUpdateInterval CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Activiteiten van bestanden en programma's bewaken**: Hiermee staat u Defender toe om activiteiten van bestanden en programma's op apparaten te bewaken. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Volgens het standaardgedrag van het besturingssysteem kunnen alle bestanden worden bewaakt.
  - **Controleren is uitgeschakeld**
  - **Alle bestanden bewaken**
  - **Alleen inkomende bestanden controleren**
  - **Alleen uitgaande bestanden controleren**

  [Defender/RealTimeScanDirection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Het aantal dagen voordat in quarantaine geplaatste malware wordt verwijderd**: Hiermee kunt u gedurende het aantal dagen dat u invoert opgeloste malware laten bijhouden, zodat u handmatig eerder aangevallen apparaten kunt controleren. 

  Als u deze instelling niet configureert of als u deze instelt op `0` dagen, blijft de schadelijke software in de map Quarantaine en wordt deze niet automatisch verwijderd. Als de waarde is ingesteld op `90`, worden items in quarantaine 90 dagen bewaard op het systeem. Daarna worden de items verwijderd.

  [Defender/DaysToRetainCleanedMalware CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Limiet voor het CPU-gebruik tijdens het scannen**: Beperk de hoeveelheid CPU die scans mogen gebruiken, van `0` tot `100` procent. Standaard kan dit in het besturingssysteem zijn ingesteld op 50%.
- **Archiefbestanden scannen**: Met **Inschakelen** schakelt u Defender in, zodat gearchiveerde bestanden, zoals ZIP- of CAB-bestanden, worden gescand. Gebruikers kunnen deze instelling niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat deze scanfunctie is ingeschakeld en dat gebruikers dit mogen wijzigen.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowArchiveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Inkomende e-mailberichten scannen**: Met **Inschakelen** staat u toe dat Defender e-mailberichten scant wanneer deze op apparaten binnenkomen. Wanneer deze functie is ingeschakeld, parseert de engine het postvak en de e-mailbestanden voor het analyseren van de berichttekst en de bijlagen. U kunt de indelingen. pst (Outlook), .dbx, .mbx, MIME (Outlook Express) en BinHex (Mac) scannen.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Deze scanfunctie wordt door het besturingssysteem standaard uitgeschakeld. Dit kan door gebruikers worden gewijzigd.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowEmailScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Verwisselbare stations scannen tijdens een volledige scan**: Met **Inschakelen** worden Defender-scans van verwisselbare stations tijdens een volledige scan ingeschakeld. Gebruikers kunnen deze instelling niet uitschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat Defender verwisselbare stations zoals USB-sticks mag scannen. Deze instelling kan door gebruikers worden gewijzigd.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Tijdens een snelle scan kunnen verwisselbare stations nog steeds worden gescand.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowFullScanRemovableDriveScanning CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Toegewezen netwerkschijven scannen tijdens een volledige scan**: Met **Inschakelen** laat u Defender bestanden op een gekoppeld netwerkstation scannen. Als de bestanden op de schijf het kenmerk Alleen-lezen hebben, kan Defender eventueel gevonden malware niet verwijderen. Gebruikers kunnen deze instelling niet uitschakelen.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Deze functie wordt door het besturingssysteem standaard ingeschakeld. Dit kan door gebruikers worden gewijzigd.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden. 

  Tijdens een snelle scan kunnen gedeelde netwerkstations nog steeds worden gescand.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowFullScanOnMappedNetworkDrives CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Bestanden scannen die zijn geopend vanuit mappen op het netwerk**: Met **Inschakelen** scant Defender bestanden die vanuit netwerkmappen of gedeelde netwerkstations zijn geopend, bijvoorbeeld bestanden die via een UNC-pad toegankelijk zijn. Gebruikers kunnen deze instelling niet uitschakelen. Als de bestanden op de schijf het kenmerk Alleen-lezen hebben, kan Defender eventueel gevonden malware niet verwijderen.

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard worden bestanden die vanuit netwerkmappen zijn geopend door het besturingssysteem gescand. Dit kan door gebruikers worden gewijzigd.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowScanningNetworkFiles CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Cloudbeveiliging**: Met **Inschakelen** wordt ingeschakeld dat de Microsoft Active Protection Service informatie ontvangt over malware-activiteit op apparaten die u beheert. Gebruikers kunnen deze instelling niet wijzigen. 

  Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan de Microsoft Active Protection Service informatie ontvangen. Deze instelling kan door gebruikers worden gewijzigd.

  Als u de instelling inschakelt en vervolgens weer wijzigt in **Niet geconfigureerd**, blijft in Intune de eerder geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune uitgeschakeld. Als u deze functie wilt uitschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowCloudProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Gebruikers vragen voordat een voorbeeld wordt verzonden**: Hiermee bepaalt u of potentieel schadelijke bestanden waarvoor verdere analyse nodig is, automatisch naar Microsoft worden verzonden. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Het standaardgedrag van het besturingssysteem is dat er automatisch veilige voorbeelden kunnen worden verzonden.
  - **Altijd vragen**
  - **Vragen voordat persoonlijke gegevens worden verstuurd**
  - **Nooit gegevens verzenden**
  - **Alle gegevens verzenden zonder te vragen**: Gegevens worden automatisch verzonden.

  [Defender/SubmitSamplesConsent CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Tijd waarop een dagelijkse snelle scan moet worden uitgevoerd**: Kies het tijdstip waarop een dagelijkse snelle scan moet worden uitgevoerd. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld deze scan om 02:00 uur wordt uitgevoerd.

  Als u meer aanpassingsmogelijkheden wilt, dan configureert u de instelling **Type systeemscan dat moet worden uitgevoerd**.

  [Defender/ScheduleQuickScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Type systeemscan dat moet worden uitgevoerd**: Plan een systeemscan, waaronder het scanniveau en de dag en tijd waarop de scan moet worden uitgevoerd. Uw opties zijn:
  - **Niet geconfigureerd**: Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Er wordt geen instelling afgedwongen. Gebruikers kunnen handmatig scans uitvoeren op dat apparaat als ze dat nodig of gewenst vinden.
  - **Uitschakelen**: Alle systeemscans op apparaten worden uitgeschakeld. Selecteer deze optie als u een antivirusoplossing van een partner gebruikt om apparaten te scannen.
  - **Snelle scan**: De gebruikelijke locaties waar malware kan zijn geregistreerd worden bekeken, zoals registersleutels en bekende opstartmappen in Windows.
    - **Geplande dag**: Kies de dag waarop de scan moet worden uitgevoerd.
    - **Geplande tijd**: Kies de tijd waarop de scan moet worden uitgevoerd.
  - **Volledige scan**: De gebruikelijke locaties waar malware kan zijn geregistreerd worden bekeken en alle mappen en bestanden op het apparaat worden gescand.
    - **Geplande dag**: Kies de dag waarop de scan moet worden uitgevoerd.
    - **Geplande tijd**: Kies de tijd waarop de scan moet worden uitgevoerd.

  > [!TIP]
  > Deze instelling kan strijdig zijn met de instelling **Tijd waarop een dagelijkse snelle scan moet worden uitgevoerd**. Een aantal aanbevelingen:  
  >
  > - Als u een dagelijkse snelle scan en een wekelijkse volledige scan wilt plannen, gaat u als volgt te werk:
  >   1. Configureer de instelling **Tijd voor het uitvoeren van een dagelijkse snelle scan**.
  >   2. Configureer het **Type systeemscan dat moet worden uitgevoerd** om een volledige scan uit te voeren.
  > 
  > - Als u slechts dagelijks één snelle scan (geen volledige scan) wilt uitvoeren, gebruikt u een van de volgende instellingen: **Tijd waarop een dagelijkse snelle scan moet worden uitgevoerd** of **Type systeemscan dat moet worden uitgevoerd**. Als u bijvoorbeeld elke dinsdag om 06.00 uur een snelle scan wilt uitvoeren, configureert u de instelling **Type systeemscan dat moet worden uitgevoerd**.
  > 
  > - Configureer de instelling **Tijd waarop een dagelijkse snelle scan moet worden uitgevoerd** niet wanneer op hetzelfde moment **Type systeemscan dat moet worden uitgevoerd** is ingesteld op **Snelle scan**. Deze instellingen kunnen conflicteren, waardoor scans mogelijk niet worden uitgevoerd.

  [Defender/ScanParameter CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [Defender/ScheduleScanDay CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [Defender/ScheduleScanTime CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **Mogelijk ongewenste toepassingen detecteren**: Met deze functie worden mogelijk ongewenste toepassingen (PUA's) geïdentificeerd en geblokkeerd, zodat deze niet op uw netwerk worden gedownload of geïnstalleerd. Deze toepassingen worden niet beschouwd als virussen, malware of andere soorten bedreigingen. Ze kunnen echter wel acties uitvoeren op eindpunten die van invloed kunnen zijn op de prestaties of het gebruik ervan. Kies het niveau van beveiliging dat moet worden ingesteld als Windows PUA’s detecteert. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. In Microsoft Defender is deze functie mogelijk standaard uitgeschakeld.
  - **Uit**: PUA-beveiliging uit.
  - **Inschakelen**: Microsoft Defender detecteert PUA’s en gedetecteerde items worden geblokkeerd. Deze items worden weergegeven in de geschiedenis, samen met andere dreigingen.
  - **Controleren**: Microsoft Defender detecteert PUA’s, maar onderneemt geen actie. U kunt de gegevens bekijken van toepassingen waarvoor acties zouden worden ondernomen. Zoek bijvoorbeeld naar gebeurtenissen die door Microsoft Defender in Logboeken zijn vastgelegd.

  Zie [Detect and block potentially unwanted applications](https://docs.microsoft.com/windows/threat-protection/windows-defender-antivirus/detect-block-potentially-unwanted-apps-windows-defender-antivirus) (Mogelijk ongewenste toepassingen detecteren en blokkeren) voor meer informatie over mogelijk ongewenste apps.

  [Defender/PUAProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Toestemming voor voorbeelden verzenden**: Momenteel heeft deze instelling geen invloed. Gebruik deze instelling niet. Mogelijk wordt deze in een toekomstige versie verwijderd.

- **Beveiliging bij toegang**: Met **Blokkeren** voorkomt u dat bestanden die zijn geopend of gedownload, worden gescand. Gebruikers kunnen dit niet inschakelen. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan het besturingssysteem deze functie inschakelen en gebruikers toestaan deze te wijzigen.

  Als u de instelling blokkeert en vervolgens weer wijzigt in **Niet geconfigureerd**, dan blijft in Intune de eerder via het besturingssysteem geconfigureerde status van de instelling behouden.

  Deze functie wordt niet door Intune ingeschakeld. Als u deze functie wilt inschakelen, gebruikt u een aangepaste URI.

  [Defender/AllowOnAccessProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Acties voor gedetecteerde bedreiging van malware**: Selecteer **Inschakelen** om de acties te kiezen waarvan u wilt dat Defender deze uitvoert voor elk bedreigingsniveau dat het detecteert: laag, gemiddeld, hoog en ernstig. Wanneer dit is ingesteld op **Niet geconfigureerd** (standaard), wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan in het besturingssysteem zijn ingesteld dat Microsoft Defender de beste optie mag kiezen.

  Wanneer deze is ingesteld op **Inschakelen**, selecteert u de actie:
  
  - **Reinigen**
  - **Quarantaine**
  - **Verwijderen**
  - **Toestaan**
  - **Door de gebruiker gedefinieerd**
  - **Blokkeren**

  Als uw actie niet mogelijk is, kiest Microsoft Defender de beste optie om te garanderen dat de bedreiging wordt opgelost.

  [Defender/ThreatSeverityDefaultAction CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Uitsluitingen voor Microsoft Defender Antivirus

U kunt bepaalde bestanden uitsluiten van scans van Microsoft Defender Antivirus door uitsluitingslijsten te wijzigen. **Over het algemeen hoeft u geen uitsluitingen toe te passen**. Micro soft Defender Antivirus bevat een aantal automatische uitsluitingen op basis van bekend gedrag van besturingssystemen en typische beheerbestanden, zoals die worden gebruikt in bedrijfsbeheer, databasebeheer en andere bedrijfsscenario's en -situaties.

> [!WARNING]
> **Als u uitsluitingen definieert, vermindert dat de beveiliging die Microsoft Defender Antivirus biedt**. Evalueer altijd de risico's die zijn verbonden aan het implementeren van uitsluitingen. Sluit alleen bestanden uit waarvan u weet dat ze niet schadelijk zijn.

- **Bestanden en mappen die moeten worden uitgesloten van scans en de realtime-beveiliging**: Voegt aan de uitsluitingslijst een of meer bestanden en mappen toe, zoals **C:\pad** of **%ProgramFiles%\pad\bestandsnaam.exe**. Deze bestanden en mappen worden niet opgenomen in real-timescans of geplande scans.
- **Bestandsextensies die moeten worden uitgesloten van scans en de realtime-beveiliging**: Voeg aan de uitsluitingslijst een of meer bestandsextensies toe, zoals **jpg** of **txt**. Bestanden met deze extensies worden niet opgenomen in realtime-scans of geplande scans.
- **Processen die moeten worden uitgesloten van scans en de realtime-beveiliging**: Voeg aan de uitsluitingslijst een of meer processen toe van het type **.exe**, **.com** of **.scr**. Deze processen worden niet opgenomen in real-timescans of geplande scans.

## <a name="power-settings"></a>Energie-instellingen

Voor deze instellingen wordt het [energiebeleid-CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power) gebruikt, waarbij ook de ondersteunde Windows-edities worden vermeld.

### <a name="battery"></a>Accu

- **Accuniveau waarbij de energiebesparingsfunctie moet worden ingeschakeld**: Wanneer het apparaat gebruikmaakt van accustroom, voert u het oplaadniveau van de accu in waarbij energiebesparing moet worden ingeschakeld (tussen 0 en 100). Voer een percentage in dat het niveau van de acculading aangeeft. Wanneer u deze waarde bijvoorbeeld instelt op `80`, wordt energiebesparing ingeschakeld wanneer de accu over 80% lading of minder beschikt.

  Als u geen waarde invoert, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan dit in het besturingssysteem zijn ingesteld op 70%.

  [Power/EnergySaverBatteryThresholdOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Klep sluiten (alleen mobiel)** : Als het apparaat gebruikmaakt van accustroom, kiest u wat er gebeurt wanneer de klep wordt gesloten. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instelling beheren.
  - **Geen actie**: Het apparaat blijft actief en blijft accustroom gebruiken.
  - **Slaapstand**: Het apparaat wordt in de slaapstand gezet en gebruikt een kleine hoeveelheid accustroom. De computer is nog ingeschakeld en geopende apps en bestanden worden opgeslagen in het RAM-geheugen (Random Access Memory).
  - **Sluimerstand**: Het apparaat wordt in de sluimerstand gezet. Geopende apps en bestanden worden opgeslagen op de harde schijf en het apparaat wordt uitgeschakeld.
  - **Afsluiten**: Het apparaat wordt afgesloten. Geopende apps en bestanden worden gesloten zonder te worden opgeslagen.

  [Power/SelectLidCloseActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Aan/uit-knop**: Kies wat er gebeurt wanneer de knop aan/uit wordt geselecteerd wanneer het apparaat gebruikmaakt van accustroom. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instelling beheren.
  - **Geen actie**: Het apparaat blijft actief en blijft accustroom gebruiken.
  - **Slaapstand**: Het apparaat wordt in de slaapstand gezet en gebruikt een kleine hoeveelheid accustroom. De computer is nog ingeschakeld en geopende apps en bestanden worden opgeslagen in het RAM-geheugen (Random Access Memory).
  - **Sluimerstand**: Het apparaat wordt in de sluimerstand gezet. Geopende apps en bestanden worden opgeslagen op de harde schijf en het apparaat wordt uitgeschakeld.
  - **Afsluiten**: Het apparaat wordt afgesloten. Geopende apps en bestanden worden gesloten zonder te worden opgeslagen.

  [Power/SelectPowerButtonActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Knop Slaapstand**: Kies wat er gebeurt wanneer de slaapstand-knop wordt geselecteerd wanneer het apparaat gebruikmaakt van accustroom. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instelling beheren.
  - **Geen actie**: Het apparaat blijft actief en blijft accustroom gebruiken.
  - **Slaapstand**: Het apparaat wordt in de slaapstand gezet en gebruikt een klein deel van de accustroom. De computer is nog ingeschakeld en geopende apps en bestanden worden opgeslagen in het RAM-geheugen (Random Access Memory).
  - **Sluimerstand**: Het apparaat wordt in de sluimerstand gezet. Geopende apps en bestanden worden opgeslagen op de harde schijf en het apparaat wordt uitgeschakeld.
  - **Afsluiten**: Het apparaat wordt afgesloten. Geopende apps en bestanden worden gesloten zonder te worden opgeslagen.

  [Power/SelectSleepButtonActionOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Hybride slaapstand**: Wanneer het apparaat accustroom gebruikt, kiest u hybride slaapstand toestaan of uitschakelen.

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instelling beheren.
  - **Inschakelen**: Apparaten kunnen naar de hybride slaapstand gaan. Geopende apps en bestanden worden opgeslagen in het RAM-geheugen (Random Access Memory) en op de harde schijf. Er wordt een geringe hoeveelheid accustroom gebruikt.
  - **Uitschakelen**: Hiermee wordt voorkomen dat apparaten in de hybride slaapstand gaan.

  [Power/TurnOffHybridSleepOnBattery CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>PluggedIn

- **Accuniveau waarbij de energiebesparingsfunctie moet worden ingeschakeld**: Wanneer het apparaat op het lichtnet werkt, voert u het oplaadniveau van de accu in waarbij energiebesparing moet worden ingeschakeld (tussen 0 en 100). Voer een percentage in dat het niveau van de acculading aangeeft. Wanneer u deze waarde bijvoorbeeld instelt op `80`, wordt energiebesparing ingeschakeld wanneer de accu over 80% lading of minder beschikt.

  Als u geen waarde invoert, wordt deze instelling niet door Intune gewijzigd of bijgewerkt. Standaard kan dit in het besturingssysteem zijn ingesteld op 70%.

  [Power/EnergySaverBatteryThresholdPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Klep sluiten (alleen mobiel)** : Als het apparaat op het lichtnet werkt, kiest u wat er gebeurt wanneer de klep wordt gesloten. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Geen actie**: Het apparaat blijft actief.
  - **Slaapstand**: Het apparaat wordt in de slaapstand gezet. De computer is nog ingeschakeld en geopende apps en bestanden worden opgeslagen in het RAM-geheugen (Random Access Memory).
  - **Sluimerstand**: Het apparaat wordt in de sluimerstand gezet. Geopende apps en bestanden worden opgeslagen op de harde schijf en het apparaat wordt uitgeschakeld.
  - **Afsluiten**: Het apparaat wordt afgesloten. Geopende apps en bestanden worden gesloten zonder te worden opgeslagen.
  
    [Power/SelectLidCloseActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Aan/uit-knop**: Kies wat er gebeurt wanneer de Aan/uit-knop wordt geselecteerd wanneer het apparaat op het lichtnet werkt. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Geen actie**: Het apparaat blijft actief.
  - **Slaapstand**: Het apparaat wordt in de slaapstand gezet. De computer is nog ingeschakeld en geopende apps en bestanden worden opgeslagen in het RAM-geheugen (Random Access Memory).
  - **Sluimerstand**: Het apparaat wordt in de sluimerstand gezet. Geopende apps en bestanden worden opgeslagen op de harde schijf en het apparaat wordt uitgeschakeld.
  - **Afsluiten**: Het apparaat wordt afgesloten. Geopende apps en bestanden worden gesloten zonder te worden opgeslagen.

  [Power/SelectPowerButtonActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Knop Slaapstand**: Kies wat er gebeurt wanneer de Slaapstand-knop wordt geselecteerd wanneer het apparaat op het lichtnet werkt. Uw opties zijn:

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune.
  - **Geen actie**: Het apparaat blijft actief.
  - **Slaapstand**: Het apparaat wordt in de slaapstand gezet. De computer is nog ingeschakeld en geopende apps en bestanden worden opgeslagen in het RAM-geheugen (Random Access Memory).
  - **Sluimerstand**: Het apparaat wordt in de sluimerstand gezet. Geopende apps en bestanden worden opgeslagen op de harde schijf en het apparaat wordt uitgeschakeld.
  - **Afsluiten**: Het apparaat wordt afgesloten. Geopende apps en bestanden worden gesloten zonder te worden opgeslagen.

  [Power/SelectSleepButtonActionPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Hybride slaapstand**: Wanneer het apparaat is aangesloten, kiest u hybride slaapstand toestaan of uitschakelen.

  - **Niet geconfigureerd** (standaard): Deze instelling wordt niet gewijzigd of bijgewerkt door Intune. Standaard is het mogelijk dat het besturingssysteem toestaat dat gebruikers deze instelling beheren.
  - **Inschakelen**: Apparaten kunnen naar de hybride slaapstand gaan. Geopende apps en bestanden worden opgeslagen in het RAM-geheugen (Random Access Memory) en op de harde schijf.
  - **Uitschakelen**: Hiermee wordt voorkomen dat apparaten in de hybride slaapstand gaan.

  [Power/TurnOffHybridSleepPluggedIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Volgende stappen

Voor aanvullende technische details over elke instelling en welke edities van Windows worden ondersteund, raadpleegt u het naslagwerk [Windows 10 Policy CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider)

[Het profiel toewijzen](device-profile-assign.md) en [de status ervan controleren](device-profile-monitor.md).
