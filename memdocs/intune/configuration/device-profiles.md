---
title: Apparaatfuncties en -instellingen gebruiken in Microsoft Intune - Azure | Microsoft Docs
description: Overzicht van de verschillende Microsoft Intune-apparaatprofielen. Krijg informatie over functies, beperkingen, e-mail, Wi-Fi, VPN, onderwijs, certificaten, Windows 10-upgrade, BitLocker en Microsoft Defender, Windows Information Protection, beheersjablonen en aangepaste configuratie-instellingen voor apparaten in het beheercentrum voor Microsoft Endpoint Manager. Gebruik deze profielen om gegevens en apparaten in uw bedrijf te beheren en te beveiligen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43101602defab75c15c542ec922cba6f2bf96cf0
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146317"
---
# <a name="apply-features-and-settings-on-your-devices-using-device-profiles-in-microsoft-intune"></a>Functies en instellingen toepassen op uw apparaten met apparaatprofielen in Microsoft Intune

Microsoft Intune omvat instellingen en functies die u op verschillende apparaten binnen uw organisatie kunt in- of uitschakelen. Deze instellingen en functies worden toegevoegd aan 'configuratieprofielen'. U kunt profielen voor verschillende apparaten en verschillende platforms maken, waaronder iOS/iPadOS, Android-apparaatbeheer, Android Enterprise en Windows. Gebruik vervolgens Intune om het profiel toe te passen of toe te wijzen aan de apparaten.

Als onderdeel van uw MDM-oplossing (Mobile Device Management) kunt u deze configuratieprofielen gebruiken om verschillende taken te voltooien. Enkele profielvoorbeelden zijn:

- Gebruik op Windows 10-apparaten een profielsjabloon die ActiveX-besturingselementen blokkeert in Internet Explorer.
- Sta gebruikers van iOS-/iPadOS- en macOS-apparaten toe om in uw organisatie AirPrint-printers te gebruiken.
- Sta wel of geen toegang toe tot bluetooth op het apparaat.
- Maak een Wi-Fi of VPN-profiel waarmee verschillende apparaten toegang hebben tot uw bedrijfsnetwerk.
- Beheer software-updates, inclusief het moment wanneer deze worden geïnstalleerd.
- Voer een Android-apparaat uit als een speciaal kioskapparaat dat één app kan uitvoeren of veel apps kan uitvoeren.

Dit artikel biedt een overzicht van de verschillende typen profielen die u kunt maken. Gebruik deze profielen om bepaalde functies op de apparaten al dan niet toe te staan.

## <a name="administrative-templates"></a>Beheersjablonen

[Beheersjablonen](administrative-templates-windows.md) bevatten honderden instellingen die u kunt configureren voor Internet Explorer, Microsoft Edge, OneDrive, extern bureaublad, Word, Excel en andere Office-programma's.

Deze sjablonen bieden beheerders een vereenvoudigde weergave van instellingen die vergelijkbaar zijn met groepsbeleid, maar ze zijn voor 100% gebaseerd op de cloud.

Deze functie ondersteunt:

- Windows 10 en hoger

## <a name="certificates"></a>Certificaten

Via [Certificaten](../protect/certificates-configure.md) worden vertrouwde , SCEP- en PKCS-certificaten geconfigureerd die zijn toegewezen aan apparaten. Met deze certificaten worden WiFi-, VPN- en e-mailprofielen geverifieerd.

Deze functie ondersteunt:

- Android-apparaatbeheerder
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1
- Windows 10 en hoger

## <a name="custom-profile"></a>Aangepast profiel

Met [Aangepaste instellingen](custom-settings-configure.md) kunnen beheerders apparaatinstellingen toewijzen die niet zijn ingebouwd in Intune. Op Android-apparaten kunt u OMA-URI-waarden invoeren. Voor iOS-/iPadOS-apparaten kunt u een configuratiebestand importeren dat u in Apple Configurator hebt gemaakt.

Deze functie ondersteunt:

- Android-apparaatbeheerder
- Android Enterprise
- iOS/iPadOS
- macOS

## <a name="delivery-optimization"></a>Delivery Optimization

[Delivery optimization](delivery-optimization-windows.md) biedt een betere ervaring voor het leveren van software-updates. Deze instellingen vervangen de instellingen **Software-Updates** > **Windows 10-updatering**.

Gebruik deze instellingen om te bepalen hoe software-updates worden gedownload naar apparaten in uw organisatie. U kunt bijvoorbeeld gebruikers krijgen hun eigen updates laten downloaden of updates binnenhalen met behulp van de cloudservices voor delivery optimization in een apparaatprofiel.

Deze functie ondersteunt:

- Windows 10 en hoger

## <a name="derived-credential"></a>Afgeleide referentie

[Afgeleide referenties](../protect/derived-credentials.md) zijn certificaten op smartcards die kunnen worden geverifieerd, ondertekend en versleuteld. In Intune kunt u profielen maken met deze referenties voor gebruik in apps, e-mailprofielen, verbinding maken met VPN, S/MIME en Wi-Fi.

Deze functie ondersteunt:

- Android Enterprise
- iOS/iPadOS

## <a name="device-features"></a>Apparaatfuncties

Met [Apparaatfuncties](device-features-configure.md) kunt u functies op iOS-/iPadOS- en macOS-apparaten beheren, zoals AirPrint, meldingen en berichten voor schermvergrendeling.

Deze functie ondersteunt:

- iOS/iPadOS
- macOS

## <a name="device-firmware-configuration-interface"></a>Configuratie-interface voor apparaatfirmware

Met de [configuratie-interface voor apparaatfirmware](device-firmware-configuration-interface-windows.md) (DFCI) kunnen beheerders UEFI-instellingen (BIOS) in- of uitschakelen met Intune. Gebruik deze instellingen om de beveiliging op firmwareniveau te verbeteren. Dit is meestal beter bestand tegen schadelijke aanvallen.

Deze functie ondersteunt:

- Windows 10 1809 en hoger op ondersteunde firmware

## <a name="device-restrictions"></a>Apparaatbeperkingen

[Apparaatbeperkingen](device-restrictions-configure.md) beheert beveiliging, hardware, delen van gegevens en meer instellingen op de apparaten. U kunt bijvoorbeeld een apparaatbeperkingsprofiel maken waarmee wordt voorkomen dat gebruikers van iOS-/iPadOS-apparaten de camera van het apparaat gebruiken. 

Deze functie ondersteunt:

- Android-apparaatbeheerder
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 10 en hoger
- Windows 10 Team

## <a name="domain-join"></a>Domeindeelname

Met [Domeindeelname](domain-join-configure.md) configureert u on-premises Active Directory-domeingegevens. Deze informatie wordt geïmplementeerd op hybride apparaten die zijn toegevoegd aan Azure AD wanneer deze zijn ingericht met behulp van Windows Autopilot en Intune. Dit profiel biedt informatie voor apparaten aan welk domein en welke OE deze moeten deelnemen.

Deze functie ondersteunt:

- Windows 10 en hoger

## <a name="edition-upgrade-and-mode-switch"></a>Editie-upgrade en modusschakelaar

[Windows 10-editie-upgrades](edition-upgrade-configure-windows-10.md) voert automatisch een upgrade naar een nieuwere functie uit op apparaten waarop een bepaalde versie van Windows 10 wordt uitgevoerd.

Deze functie ondersteunt:

- Windows 10 en hoger

## <a name="education"></a>Education

Met [Onderwijsinstellingen - Windows 10](education-settings-configure.md) kunt u opties configureren voor de [Windows-app Toets maken](https://docs.microsoft.com/education/windows/take-tests-in-windows-10). Wanneer u deze opties configureert, kunnen er geen andere apps op het apparaat worden uitgevoerd totdat de toets is voltooid.

Met [Onderwijsinstellingen - iOS/iPadOS](../fundamentals/education-settings-configure-ios-shared.md) kunt u de iOS-/iPadOS-app Classroom gebruiken om het leren te begeleiden en de apparaten van studenten in het leslokaal te beheren. U kunt iPads zo configureren dat meerdere studenten één apparaat kunnen delen.

## <a name="email"></a>E-mail

[E-mailinstellingen](email-settings-configure.md) maakt en bewaakt de e-mailinstellingen voor Exchange ActiveSync op de apparaten en wijst deze toe. E-mailprofielen helpen met consistentie, verminderen het aantal ondersteuningsaanvragen en bieden uw eindgebruikers toegang tot bedrijfse-mail op hun eigen apparaten zonder dat ze instellingen hoeven op te geven. 

Deze functie ondersteunt:

- Android-apparaatbeheerder
- Android Enterprise
- iOS/iPadOS
- Windows 10 en hoger

## <a name="endpoint-protection"></a>Endpoint Protection

Met [Endpoint Protection](../protect/endpoint-protection-configure.md) configureert u BitLocker- en Microsoft Defender-instellingen voor Windows 10-apparaten. En configureer de firewall, gateway en andere resources op macOS-apparaten.

Zie het Engelstalige artikel [Configure endpoints using Mobile Device Management (MDM) tools](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-mdm) (Eindpunten configureren met MDM-hulpprogramma's (Mobile Device Management)) als u Microsoft Defender Advanced Threat Protection (WDATP) wilt vrijgeven met Microsoft Intune.

Deze functie ondersteunt:

- macOS
- Windows 10 en hoger

## <a name="esim-cellular---public-preview"></a>eSIM - Openbare preview

Met [mobiele eSIM-profielen](esim-device-configuration.md) kunnen beheerders mobiele data-abonnementen op uw beheerde apparaten configureren voor toegang tot internet en gegevens. Nadat u activeringscodes van uw mobiele operator hebt ontvangen, kunt u deze activeringscodes met Intune importeren en vervolgens toewijzen aan apparaten die geschikt zijn voor eSIM.

Deze functie ondersteunt:

- Windows 10 Fall Creators Update en hoger

## <a name="extensions"></a>Uitbreidingen

Met [macOS-systeemextensies en -kernelextensies](kernel-extensions-overview-macos.md) kunnen beheerders functies of programma's toevoegen waarmee de systeemeigen mogelijkheden van het besturingssysteem worden uitgebreid. Configureer deze instellingen voor het vertrouwen van alle extensies van een specifieke ontwikkelaar of partner, of sta specifieke extensies toe.

Deze functie ondersteunt:

- macOS

## <a name="identity-protection"></a>Identiteitsbescherming

Met [Identiteitsbescherming](../protect/identity-protection-configure.md) beheert u de Windows Hello voor Bedrijven-ervaring op Windows 10-apparaten. Configureer deze instellingen om Windows Hello voor Bedrijven beschikbaar maken voor gebruikers en apparaten, en om de vereisten op te geven voor pincodes en gebaren voor apparaten.  

Deze functie ondersteunt:  

- Windows 10 en hoger
- Windows Holographic for Business  

## <a name="kiosk"></a>Kiosk

Het profiel [Kiosk-instellingen](kiosk-settings.md) configureert een apparaat om één app uit te voeren of om verschillende apps uit te voeren. U kunt ook andere functies op uw kiosks aanpassen, waaronder een startmenu en een webbrowser.

Deze functie ondersteunt:

- Windows 10 en hoger

Kiosk-instellingen zijn ook beschikbaar als apparaatbeperkingen voor [Android](device-restrictions-android.md#kiosk), [Android Enterprise](device-restrictions-android-for-work.md#device-experience) en [iOS/iPadOS](device-restrictions-ios.md#kiosk).

## <a name="mx-profile-zebra"></a>MX-profiel (Zebra)

[Mobiliteitsextensies (MX)](android-zebra-mx-overview.md) breiden de ingebouwde Intune-instellingen uit om meer instellingen aan te passen of toe te voegen speciaal voor Zebra-apparaten. Zebra-apparaten worden meestal gebruikt op fabrieks-en detailhandelsomgevingen. Als u honderden of duizenden Zebra-apparaten hebt, kunt u Intune gebruiken om deze apparaten te configureren en te beheren.

Deze functie ondersteunt:

- Android-apparaatbeheerder

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

[Microsoft Defender Advanced Threat Protection (ATP)](../protect/advanced-threat-protection.md) is met Intune geïntegreerd om apparaten te bewaken en te beveiligen. U stelt risiconiveaus in en bepaalt wat er gebeurt als apparaten dit niveau overschrijden. Wanneer u dit combineert met voorwaardelijke toegang, kunt u hiermee schadelijke activiteiten in uw organisatie voorkomen.

Deze functie ondersteunt:

- Windows 10 en hoger

## <a name="oemconfig"></a>OEMConfig

Op Android Enterprise-apparaten, is [OEMConfig](android-oem-configuration-overview.md) een standaard waarmee OEM's (Original Equipment Manufacturers) en EMMs (Enterprise Mobility Management) OEM-specifieke functies op een gestandaardiseerde manier kunnen bouwen en ondersteunen. Met OEMConfig kunnen OEM's een schema maken waarin OEM-specifieke beheerfuncties worden gedefinieerd en dat insluiten in een app die wordt geüpload naar Google Play. Het schema van de app wordt ingelezen in Intune en zorgt dat Intune-beheerders de instellingen in het schema kunnen configureren.

Deze functie ondersteunt:

- Android Enterprise (OEMConfig)

## <a name="powershell-scripts"></a>PowerShell-scripts

[PowerShell-scripts](../apps/intune-management-extension.md) gebruiken de Intune-beheerextensie om uw PowerShell-scripts te uploaden naar Intune en deze scripts vervolgens uit te voeren op uw apparaten. Zie ook de vereisten voor het gebruik van de extensie, hoe u deze toevoegt aan Intune, en andere belangrijke informatie.

Deze functie ondersteunt:

- Windows 10 en hoger
- Windows Holographic for Business

## <a name="preference-file"></a>Voorkeursbestand

[Voorkeursbestanden](preference-file-settings-macos.md) op macOS-apparaten bevatten informatie over apps. U kunt bijvoorbeeld voorkeursbestanden gebruiken voor het beheren van webbrowserinstellingen, het aanpassen van apps en nog veel meer.

Deze functie ondersteunt:

- macOS

## <a name="shared-multi-user-device"></a>Gedeelde apparaat voor meerdere gebruikers

[Windows 10](shared-user-device-settings-windows.md) en [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md) omvatten instellingen voor het beheren van apparaten met meerdere gebruikers, ook wel bekend als gedeelde apparaten of gedeelde pc's. Wanneer een gebruiker zich aanmeldt met het apparaat, kiest u of de gebruiker de opties voor slaapstand kan wijzigen of bestanden op het apparaat kan opslaan. In een ander voorbeeld kunt u, om ruimte te besparen, een profiel maken waarmee inactieve referenties van Windows HoloLens-apparaten worden verwijderd.

Via deze instellingen voor gedeelde apparaten voor meerdere gebruikers kan een beheerder bepaalde apparaatfuncties beheren en deze gedeelde apparaten met Intune beheren.

Deze functie ondersteunt:

- Windows 10 en hoger
- Windows Holographic for Business

## <a name="update-policies"></a>Updatebeleid

In [Updatebeleid voor iOS/iPadOS](../protect/software-updates-ios.md) ziet u hoe u iOS-/iPadOS-beleid maakt en toewijst om software-updates te installeren op uw iOS-/iPadOS-apparaten. U kunt ook de status van de installatie bekijken.

Zie [Delivery optimization](delivery-optimization-windows.md) voor updatebeleid op Windows-apparaten. 

Deze functie ondersteunt:

- iOS/iPadOS

## <a name="vpn"></a>VPN

[VPN-instellingen](vpn-settings-configure.md) wijst VPN-profielen toe aan gebruikers en apparaten in uw organisatie, zodat deze gemakkelijk en veilig verbinding met het netwerk kunnen maken. 

Met virtuele particuliere netwerken (VPN's) hebben gebruikers veilige externe toegang tot uw bedrijfsnetwerk. Apparaten gebruiken een VPN-verbindingsprofiel om een verbinding met uw VPN-server op te zetten. 

Deze functie ondersteunt: 

- Android-apparaatbeheerder
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1
- Windows 10 en hoger

## <a name="wi-fi"></a>Wi-Fi

[Wi-Fi-instellingen](wi-fi-settings-configure.md) wijst instellingen voor draadloze netwerken toe aan gebruikers en apparaten. Wanneer u een Wi-Fi-profiel toewijst, hebben uw gebruikers toegang tot uw zakelijke Wi-Fi zonder dat ze dit zelf hoeven te configureren. 

Deze functie ondersteunt:

- Android-apparaatbeheerder
- Android Enterprise
- iOS/iPadOS
- macOS
- Windows 8.1 (alleen importeren)
- Windows 10 en hoger

## <a name="wired-networks"></a>Bedrade netwerken

Met [bekabelde netwerken](wired-networks-configure.md) kunt u bekabelde 802.1 x-verbindingen maken en beheren voor macOS-desktopcomputers. In uw profiel kiest u de netwerkinterface, selecteert u de geaccepteerde EAP-typen en voert u de instellingen voor de vertrouwensinstelling van de server in, met inbegrip van PKCS-en SCEP-certificaten.

Wanneer u het profiel toewijst, hebben uw macOs-desktopgebruikers toegang tot uw zakelijke bekabelde netwerk zonder dat ze dit zelf hoeven te configureren.

Deze functie ondersteunt:

- macOS

## <a name="zebra-mobility-extensions-mx"></a>Zebra Mobility Extensions (MX)

Met [Zebra Mobility Extensions (MX)](android-zebra-mx-overview.md) kunnen beheerders Zebra-apparaten gebruiken en beheren in Intune. In de instellingen kunt u StageNow-profielen maken, en vervolgens Intune gebruiken om deze profielen toe te wijzen aan en te implementeren op uw Zebra-apparaten. De documentatie [StageNow-logboeken en veelvoorkomende problemen](android-zebra-mx-logs-troubleshoot.md) is een handige resource voor het oplossen van problemen met profielen, en voor inzicht in potentiële problemen bij het gebruik van StageNow.

Deze functie ondersteunt:

- Android-apparaatbeheer (mobiliteitsextensies)

## <a name="manage-and-troubleshoot"></a>Beheren en problemen oplossen

[Beheer uw profielen](device-profile-monitor.md) om de status van apparaten te controleren en te bekijken welke profielen zijn toegewezen. U kunt hiermee ook conflicten oplossen: u ziet welke instellingen leiden tot een conflict en welke profielen deze instellingen bevatten. De documentatie [Veelvoorkomende problemen en oplossingen](device-profile-troubleshoot.md) helpt beheerders bij het werken met profielen. Hierin wordt beschreven wat er gebeurt wanneer u een profiel verwijdert, waarom meldingen worden verzonden naar apparaten, en meer.

## <a name="next-steps"></a>Volgende stappen

Kies uw platform en ga aan de slag.
