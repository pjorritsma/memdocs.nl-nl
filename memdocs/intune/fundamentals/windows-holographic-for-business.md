---
title: Windows Holographic-apparaten gebruiken met Microsoft Intune - Azure | Microsoft Docs
description: Met Microsoft Intune kunt u verschillende taken uitvoeren en beheren op apparaten met Windows Holographic for Business en HoloLens, zoals de bedrijfsportal configureren, een nalevingsbeleid maken, OMA-URI-instellingen wijzigen, apps implementeren, apparaten in groepen categoriseren, profielen maken, apparaten beperken, software-updates inschakelen, voorwaarden instellen, VPN- en Wi-Fi-instellingen configureren en Hello voor Bedrijven gebruiken.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 585a2f17-106b-4f02-adf7-05f08a92dbc1
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b7486fa6770db03bb47ccf3e069499c02c6d598c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88916041"
---
# <a name="manage-and-use-different-device-management-features-on-windows-holographic-and-hololens-devices-with-intune"></a>Verschillende apparaatbeheerfuncties beheren en gebruiken op Windows Holographic- en HoloLens-apparaten met Intune

Microsoft Intune bevat veel functies waarmee u apparaten met Windows Holographic for Business kunt beheren, zoals de [Microsoft HoloLens](/hololens/). Met Intune kunt u bevestigen dat apparaten compatibel zijn met de regels van uw organisatie, en u kunt het apparaat aanpassen door een VPN- of Wi-Fi-profiel toe te voegen. Een andere belangrijke functie is dat het apparaat kan worden gebruikt als een kiosk en dat met het apparaat een specifieke app of set apps kan worden uitgevoerd.

De taken in dit artikel helpen u bij het beheren, aanpassen en beveiligen van uw apparaten met Windows Holographic for Business, inclusief software-updates en het gebruik van Windows Hello for Business.

Maak een editie-upgrade-profiel om Windows Holographic-apparaten te gebruiken met Intune. Met dit upgradeprofiel werkt u de apparaten bij van Windows Holographic naar Windows Holographic for Business. Voor Microsoft HoloLens kunt u de Commercial Suite kopen om de vereiste licentie voor de upgrade te krijgen. Zie [Apparaten met Windows Holographic upgraden naar Windows Holographic for Business](../configuration/holographic-upgrade.md) voor meer informatie.

## <a name="azure-active-directory"></a>Azure Active Directory

Azure Active Directory (AD) is een geweldige resource voor het beheren en bedienen van uw apparaten waarop Windows Holographic voor Bedrijven wordt uitgevoerd. Met behulp van Intune en Azure AD kunt u: 

- **[Apparaten toevoegen in Azure Active Directory](/azure/active-directory/devices/azureadjoin-plan)** : In Azure Active Directory (AD) kunt u uw Windows 10-apparaten voor zakelijk gebruik toevoegen, waaronder apparaten waarop Windows Holographic for Business wordt uitgevoerd. Via deze functie kan Azure AD het apparaat beheren. Hiermee kunt u bevestigen dat uw gebruikers toegang tot uw bedrijfsresources hebben vanaf apparaten die aan uw beveiligings en nalevingsnormen voldoen.

  Zie [Apparaatbeheer in Azure AD](/azure/active-directory/devices/overview) voor meer informatie.

- **[Bulkregistratie voor Windows-apparaten](../enrollment/windows-bulk-enroll.md)** : Als beheerder kunt u grote aantallen nieuwe Windows-apparaten toevoegen aan Azure Active Directory (AD) en Intune. Deze functie wordt bulkregistratie genoemd. Hiervoor worden inrichtingspakketten gebruikt. Deze pakketten koppelen de apparaten waarop Windows Holographic voor Bedrijven wordt uitgevoerd met uw Azure AD-tenant en registreren deze in Intune.

## <a name="company-portal"></a>Bedrijfsportal

**[De bedrijfsportal-app configureren](../apps/company-portal-app.md)**

Intune biedt gebruikers de bedrijfsportal-app, waarmee zij toegang hebben tot bedrijfsgegevens, apparaten registreren, apps installeren, contact opnemen met uw IT-afdeling en meer. U kunt de bedrijfsportal-app aanpassen voor uw apparaten met Windows Holographic for Business.

U kunt ook een de volgende acties uitvoeren met behulp van de bedrijfsportal-app:

- [Een apparaat uit Intune verwijderen](../user-help/unenroll-your-device-from-intune-windows.md) met behulp van de instellingen-app of de bedrijfsportal-app
- [De naam van een apparaat wijzigen](../user-help/rename-your-device-cpapp.md)
- [Apps installeren](../user-help/install-apps-cpapp-windows.md) op een apparaat
- [Apparaten handmatig synchroniseren](../user-help/sync-your-device-manually-windows.md) vanuit de instellingen-app of de bedrijfsportal-app

## <a name="compliance-policy"></a>Nalevingsbeleid

**[Een nalevingsbeleid voor apparaten maken](../protect/compliance-policy-create-windows.md)**

Nalevingsbeleid zijn regels en instellingen waaraan apparaten moeten voldoen om compatibel te zijn. Gebruik deze beleidsregels met voorwaardelijke toegang om toegang tot bedrijfsresources te blokkeren voor apparaten die niet compatibel zijn. Maak in Intune nalevingsbeleid om toegang voor apparaten met Windows Holographic for Business toe te staan of te blokkeren. U kunt bijvoorbeeld een beleid maken waarvoor BitLocker moet zijn ingeschakeld.

Zie ook **[Aan de slag met nalevingsbeleid](../protect/device-compliance-get-started.md)** .

## <a name="deploy-and-manage-apps"></a>Apps implementeren en beheren

**[Apps toevoegen aan Intune](../apps/apps-add.md)**

Met Intune kunt u apps toevoegen aan uw apparaten met Windows Holographic for Business. Apps kunnen op verschillende manieren worden geïmplementeerd. Voorbeelden hiervan zijn:

- [Microsoft Store-apps toevoegen](../apps/store-apps-windows.md)
- [Apps toevoegen die u maakt](../apps/lob-apps-windows.md)
- [Apps aan groepen toewijzen](../apps/apps-deploy.md)

Microsoft Intune kan universele Windows-apps implementeren op Microsoft HoloLens-apparaten waarop Windows Holographic for Business wordt uitgevoerd. U kunt uw app-pakketten rechtstreeks uploaden in Intune Azure Portal of implementeren vanuit de Microsoft Store voor Bedrijven. Zie de volgende artikelen voor meer informatie:
- Zie [Windows Line-Of-Business-apps toevoegen aan Microsoft Intune](../apps/lob-apps-windows.md) voor het implementeren van Line-of-Business-apps (LOB) met behulp van Intune Azure Portal.

    > [!NOTE]
    > In Intune is een maximale pakketgrootte van 8 GB toegestaan. Deze pakketgrootte is alleen beschikbaar voor LOB-apps die zijn geüpload naar Intune.

- Zie [Apps die u hebt aangeschaft in Microsoft Store voor Bedrijven beheren met Microsoft Intune](../apps/windows-store-for-business.md) voor het implementeren van apps via de Microsoft Store voor Bedrijven. 
- Zie [Wat is appbeheer in Microsoft Intune?](../apps/app-management.md) voor meer informatie over het beheer van apps met Microsoft Intune.
- Zie [Apps met gemengde realiteit voor Microsoft HoloLens](https://www.microsoft.com/hololens/apps) voor meer informatie over het ontwikkelen van apps voor Microsoft HoloLens. 

> [!NOTE]
> HoloLens-apparaten met Windows 10 Holographic voor bedrijven 1607 ondersteunen geen apps met een online licentie uit de Microsoft Store voor Bedrijven. Zie [Apps installeren op HoloLens](/hololens/holographic-store-apps) voor meer informatie.

## <a name="device-actions"></a>Apparaatacties

In Intune worden een aantal ingebouwde acties gebruikt waarmee IT-beheerders verschillende taken kunnen uitvoeren. Dit kan lokaal op het apparaat maar ook extern met behulp van Intune in Azure Portal. Gebruikers kunnen ook vanuit de Intune-bedrijfsportal op afstand een opdracht geven voor persoonlijke apparaten die bij Intune zijn ingeschreven.

De volgende acties kunnen worden gebruikt wanneer u apparaten gebruikt waarop Windows Holographic voor Bedrijven wordt uitgevoerd: 

- **[Wissen](../remote-actions/devices-wipe.md#wipe)** : Met de actie **Wissen** wordt het apparaat uit Intune verwijderd en worden de standaardfabrieksinstellingen van het apparaat hersteld. Gebruik deze actie voordat u het apparaat aan een nieuwe gebruiker geeft of wanneer het apparaat is verloren of gestolen.

- **[Buiten gebruik stellen](../remote-actions/devices-wipe.md#retire)** : Met de actie **Buiten gebruik stellen** wordt het apparaat uit Intune verwijderd. Hiermee verwijdert u ook beheerde app-gegevens, instellingen en e-mailprofielen die zijn toegewezen door Intune. De persoonlijke gegevens van de gebruiker blijven op het apparaat.

- **[Apparaten synchroniseren om het meest recente beleid en de meest recente acties te verkrijgen](../remote-actions/device-sync.md)** : Met de actie **Synchroniseren** wordt het geselecteerde apparaat direct ingecheckt bij Intune. Wanneer een apparaat wordt ingecheckt, worden direct eventuele openstaande acties of toegewezen beleidsregels ontvangen die eraan zijn toegewezen. Met deze functie kunt u toegewezen beleid controleren en in het geval van problemen direct aanpassen, zonder dat u hoeft te wachten op de volgende geplande check-in.

**[Wat is Microsoft Intune-apparaatbeheer?](../remote-actions/device-management.md)** is een goede resource voor meer informatie over het beheer van apparaten via Azure Portal. 

## <a name="device-categories-and-groups"></a>Apparaatcategorieën en -groepen

**[Apparaten categoriseren in groepen](../enrollment/device-group-mapping.md)**

Met Intune kunt u apparaatcategorieën maken om apparaten automatisch toe te voegen aan groepen op basis van categorieën die u instelt, zoals Verkoop, Boekhouding, Human Resources, enzovoort. Het idee is om het beheer van uw apparaten met Windows Holographic for Business te vereenvoudigen.

## <a name="device-configuration-profiles"></a>Apparaatconfiguratieprofielen

**[Aan de slag met configuratieprofielen](../configuration/device-profiles.md) en [profieloverzicht](../configuration/device-profile-create.md)**

Intune omvat instellingen en functies die u op verschillende apparaten binnen uw organisatie kunt in- of uitschakelen. Deze instellingen en functies worden beheerd met behulp van profielen. U kunt bijvoorbeeld een profiel maken waarmee Cortana wordt ingeschakeld, of een profiel dat Microsoft Defender Smart Screen gebruikt op uw apparaten met Windows Holographic for Business.

U kunt OMA-URI in uw profielen gebruiken om een aantal instellingen aan te passen, apparaatbeperkingen in te stellen en een virtueel particulier netwerk (VPN) en Wi-Fi te configureren.

### <a name="custom-device-settings"></a>[Aangepaste apparaatinstellingen](../configuration/custom-settings-windows-holographic.md)

Als u instellingen voor OMA-URI (Open Mobile Alliance Uniform Resource Identifier) wilt configureren, kunt u een aangepast profiel maken in Intune. Met de OMA-URI-instellingen kunt u verschillende functies beheren op uw apparaten met Windows Holographic for Business, zoals VPN inschakelen of controleren op updates van Microsoft Update.

Bekijk een [voorbeeld](../configuration/custom-profile-hololens.md) dat gebruikmaakt van de [Windows Defender Application Control (WDAC) CSP](/windows/client-management/mdm/applicationcontrol-csp) om te voorkomen dat apps kunnen worden geopend op Windows-apparaten met HoloLens 2.

### <a name="configure-kiosk-mode"></a>[Kioskmodus configureren](../configuration/kiosk-settings-holographic.md)

Met behulp van de gedeelde of gastfuncties van de pc die beschikbaar zijn in Intune kunt u Windows Holographic for Business-apparaten in de kioskmodus uitvoeren. Deze apparaten kunnen één app (één app in de kioskmodus) of meerdere apps uitvoeren (meerdere apps in de kioskmodus).

### <a name="device-restrictions"></a>[Apparaatbeperkingen](../configuration/device-restrictions-windows-holographic.md)

Met apparaatbeperkingen kunt u verschillende instellingen en functies op uw apparaten beheren, zoals een wachtwoord vereisen, apps installeren apps uit de [Microsoft Store](https://www.microsoft.com/store/apps/windows?icid=CNavAppsWindowsApps), Bluetooth inschakelen en meer. Deze beperkingen worden gemaakt in een Intune-profiel. Dit profiel kan worden toegepast op meerdere apparaten met Windows Holographic for Business.

### <a name="configure-vpn"></a>[VPN configureren](../configuration/vpn-settings-configure.md)

Met virtuele particuliere netwerken (VPN's) geeft u uw gebruikers veilige externe toegang tot uw bedrijfsnetwerk. U kunt in Intune een VPN-profiel maken met specifieke instellingen voor uw apparaten met Windows Holographic for Business. U kunt bijvoorbeeld een VPN-profiel maken zodat alle apparaten met Windows Holographic for Business Citrix-VPN gebruiken als verbindingstype.

### <a name="configure-wi-fi"></a>[Wi-Fi configureren](../configuration/wi-fi-settings-configure.md)

U kunt in Intune ook een Wi-Fi-profiel maken om draadloze netwerkinstellingen toe te wijzen aan apparaten met Windows Holographic for Business. Als u een Wi-Fi-profiel toewijst, krijgen uw eindgebruikers zonder netwerkconfiguratie toegang tot het bedrijfsnetwerk. U kunt bijvoorbeeld een Wi-Fi-netwerk uitsluitend voor apparaten met Windows Holographic for Business maken.

## <a name="shared-multi-user-devices"></a>Gedeelde apparaten voor meerdere gebruikers

[Gedeelde apparaten](../configuration/shared-user-device-settings-windows-holographic.md)

Apparaten met Windows Holographic for Business, zoals de Microsoft HoloLens, kunnen meerdere gebruikers hebben. Intune bevat instellingen waarmee verschillende functies op deze gedeelde apparaten kunnen worden beheerd, zoals energiebeheer, het gebruik van lokale opslag en accountbeheer. De configuratieprofielen kunnen ook worden toegepast op apparaten met verschillende besturingssystemen. De groep met apparaten kan bijvoorbeeld zowel RS2- als RS3-apparaten bevatten.

## <a name="software-updates"></a>Software-updates

**[Software-updates beheren](../protect/windows-update-for-business-configure.md)**

Intune heeft de functie update-ringen voor Windows 10-apparaten. Deze update-ringen bevatten een groep instellingen waarmee u bepaalt hoe updates worden geïnstalleerd. U kunt bijvoorbeeld een onderhoudsvenster maken om updates te installeren of instellen dat opnieuw moet worden opgestart nadat updates zijn geïnstalleerd. De update-ring kan worden toegepast op meerdere apparaten met Windows Holographic for Business.

## <a name="terms-and-conditions"></a>Voorwaarden

**[De voorwaarden voor gebruikerstoegang van uw bedrijf instellen](../enrollment/terms-and-conditions-create.md)**

Voordat gebruikers apparaten registreren en toegang hebben tot uw bedrijfsapps, waaronder e-mail, kunt u vereisen dat gebruikers de voorwaarden van uw bedrijf accepteren. Definieer in Intune hoe de voorwaarden worden weergegeven in de bedrijfsportal en wijs deze voorwaarden ook toe aan apparaten met Windows Holographic for Business.

## <a name="windows-hello-for-business"></a>Windows Hello voor Bedrijven

**[Windows Hello voor Bedrijven gebruiken](../protect/windows-hello.md)**

Hello voor Bedrijven biedt een alternatieve aanmeldingsmethode waarbij een Azure Active Directory-account wordt gebruikt om een wachtwoord, smartcard of virtuele smartcard te vervangen. Met Hello voor Bedrijven kunnen apparaten met Windows Holographic for Business zich aanmelden met een pincode met een door u ingestelde minimale lengte.

## <a name="next-steps"></a>Volgende stappen

[Intune instellen](setup-steps.md).