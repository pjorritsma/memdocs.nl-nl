---
title: In ontwikkeling - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-functies in ontwikkeling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b7f1a4280b409ec4a12c6371fd2e6cba8a571ca
ms.sourcegitcommit: 56a894edd291034510c144c31770cf09e20b2d6c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/10/2020
ms.locfileid: "88048018"
---
# <a name="in-development-for-microsoft-intune"></a>In ontwikkeling voor Microsoft Intune

Als hulp bij uw gereedheid en planning worden op deze pagina updates voor en functies van de Intune-gebruikersinterface vermeld die in ontwikkeling zijn, maar nog niet zijn uitgebracht. Naast de informatie op deze pagina geldt het volgende: 

- Als we verwachten dat u actie moet ondernemen vóór een wijziging, publiceren we een aanvullend bericht in het Office-berichtencentrum.
- Als een functie in productie gaat, of het nu gaat om een preview of algemene beschikbaarheid, wordt de functiebeschrijving verplaatst van deze pagina naar [Nieuwe functies](whats-new.md).
- Deze pagina en de pagina [Nieuwe functies](whats-new.md) worden regelmatig bijgewerkt. Controleer op andere updates.
- Raadpleeg de [Microsoft 365-roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) voor strategische producten en tijdlijnen.

> [!NOTE]
> Deze pagina bevat onze huidige verwachtingen over Intune-mogelijkheden in een aanstaande release. Datums en afzonderlijke functies kunnen worden gewijzigd. Op deze pagina worden niet alle functies in ontwikkeling beschreven.

**RSS-feed**: U ziet wanneer deze pagina wordt bijgewerkt door de volgende URL in uw feedlezer te kopiëren en plakken: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

**Dit artikel is voor het laatst bijgewerkt op de datum die wordt vermeld in de bovenstaande titel.**

<!--
## What's coming to Intune in the Azure portal 
## What's coming to Intune apps
## Notices
-->

<!-- Common categories:  
## App management
## Device configuration
## Device enrollment
## Device management
## Intune apps
## Monitor and troubleshoot
## Role-based access control
## Security

-->
 
<!-- ***********************************************-->
## <a name="app-management"></a>Appbeheer

### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023----"></a>Updates voor apparaatpictogrammen in de bedrijfsportal- en Intune-apps op Android<!-- 6057023  -->
We zijn bezig met het bijwerken van de apparaatpictogrammen in de bedrijfsportal- en Intune-apps op Android-apparaten, om een moderner uiterlijk te creëren, en beter af te stemmen op het Microsoft Fluent Design-systeem. Raadpleeg [Updates voor pictogrammen in de bedrijfsportal-app voor iOS/iPadOS en macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-) voor verwante informatie. 

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS-bedrijfsportal biedt ondersteuning voor Automatische apparaatinschrijving van Apple zonder gebruikersaffiniteit<!-- 7282707  --> 
iOS-bedrijfsportal wordt ondersteund op apparaten die zijn ingeschreven met behulp van Automatische apparaatinschrijving van Apple zonder dat een toegewezen gebruiker is vereist. Een eindgebruiker kan zich aanmelden bij de iOS-bedrijfsportal om zichzelf de primaire gebruiker te maken op een iOS-/iPadOS-apparaat dat is ingeschreven zonder apparaataffiniteit. Zie [iOS/iPadOS-apparaten automatisch inschrijven met automatische apparaatinschrijving van Apple](../enrollment/device-enrollment-program-enroll-ios.md) voor meer informatie over automatische apparaatinschrijving.

### <a name="the-windows-company-portal-adds-configuration-manager-application-support---4297660---"></a>De Windows-bedrijfsportal voegt ondersteuning voor Configuration Manager-toepassingen toe<!-- 4297660 -->
De Windows-bedrijfsportal biedt nu ondersteuning voor Configuration Manager-toepassingen. Met deze functie kunnen eindgebruikers zowel Configuration Manager-toepassingen als met Intune geïmplementeerde toepassingen zien in de Windows-bedrijfsportal voor co-beheerde klanten. Deze ondersteuning helpt beheerders bij het consolideren van de verschillende portal-ervaringen van eindgebruikers. Zie [De bedrijfsportal-app configureren op co-beheerde apparaten](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal) voor meer informatie.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Apparaatconfiguratie

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>De nalevingsstatus van apparaten van externe MDM-partners instellen<!-- 6361689   -->
Microsoft 365-klanten die eigenaar zijn van MDM-oplossingen van derden, kunnen beleid voor voorwaardelijke toegang afdwingen voor Microsoft 365-apps op iOS en Android via integratie met de service Microsoft Intune-apparaatcompatibiliteit. De MDM-leverancier van derden maakt gebruik van de service Intune-apparaatcompatibiliteit om nalevingsgegevens van apparaten naar Intune te verzenden. Intune evalueert vervolgens om te bepalen of het apparaat wordt vertrouwd en stelt de kenmerken voor voorwaardelijke toegang in Azure AD in.  Klanten moeten beleid voor voorwaardelijke toegang van Azure AD instellen in het Microsoft Endpoint Manager-beheercentrum of de Azure AD-portal.

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>PKCS-certificaatprofielen maken voor volledig beheerde Android Enterprise-apparaten (COBO)<!-- 4839686 -->
U kunt PKCS-certificaatprofielen maken om certificaten te implementeren op apparaten met een Android Enterprise-apparaateigenaar en -werkprofiel (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise > Alleen apparaateigenaar**, of **Android Enterprise > Alleen werkprofiel** voor platform > **PKCS** voor profiel).

Binnenkort kunt u PKCS-certificaatprofielen maken voor volledig beheerde Android-apparaten. De Intune PFX-certificaatconnector is vereist. Als u niet SCEP gebruikt en alleen PKCS gebruikt, kunt u de NDES-connector verwijderen nadat u de nieuwe PFX-connector hebt geïnstalleerd. De nieuwe PFX-connector importeert PFX-bestanden en implementeert PKCS-certificaten op alle platforms.

Zie [PKCS-certificaten configureren en gebruiken met Intune](../protect/certficates-pfx-configure.md) voor meer informatie over PKCS-certificaten.

Van toepassing op:
- Android Enterprise - volledig beheerd (COBO)

### <a name="use-netmotion-as-a-vpn-connection-type-for-iosipados-and-macos-devices---1333631---"></a>Netmotion gebruiken als een VPN-verbindings type voor iOS/iPadOS en macOS-apparaten<!-- 1333631 -->
Wanneer u een VPN-profiel maakt, is NetMotion beschikbaar als een VPN-verbindingstype (**Apparaten** > **Apparaatconfiguratie** > **Profiel maken** > **iOS/iPadOS** of **macOS** voor platform > **VPN** voor profiel > **NetMotion** voor verbindingstype).

Zie [VPN-profielen maken om verbinding te maken met VPN-servers](../configuration/vpn-settings-configure.md) voor meer informatie over VPN-profielen in Intune.

Van toepassing op:
- iOS/iPadOS
- macOS

### <a name="more-protected-extensible-authentication-protocol-peap-options-for-windows-10-wi-fi-profiles---3805024---"></a>Meer PEAP-opties (Protected Extensible Authentication Protocol) voor Wi-Fi-profielen voor Windows 10<!-- 3805024 -->
Op Windows 10-apparaten kunt u Wi-Fi-profielen maken en het verificatietype voor EAP (Extensible Authentication Protocol) selecteren om Wi-Fi-verbindingen te verifiëren (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Windows 10 en hoger** voor platform > **Wi-Fi** voor profiel > **Enterprise**). Wanneer u beveiligde EAP (PEAP) selecteert, zijn er nieuwe instellingen beschikbaar:

- **Servervalidatie uitvoeren in PEAP-fase 1**: In PEAP-onderhandelingsfase 1 valideren apparaten het certificaat en verifiëren ze de server.
  - **Gebruikersprompts voor servervalidatie uitschakelen in PEAP-fase 1**: In PEAP-onderhandelingsfase 1 worden gebruikersprompts met de vraag om nieuwe PEAP-servers voor vertrouwde certificeringsinstanties niet weergegeven.
- **Cryptografische binding vereisen**: Hiermee worden verbindingen met PEAP-servers die geen cryptobinding gebruiken tijdens de PEAP-onderhandeling voorkomen.

Ga naar [Wi-Fi-instellingen voor Windows 10- en nieuwere apparaten toevoegen](../configuration/wi-fi-settings-windows.md) voor een overzicht van de instellingen die u momenteel kunt configureren.

Van toepassing op: 
- Windows 10 en nieuwer

### <a name="configure-the-macos-microsoft-enterprise-sso-plug-in---5627576---"></a>De macOS Microsoft Enterprise SSO-invoegtoepassing configureren<!-- 5627576 -->
Het Microsoft Azure AD-team heeft een app-extensie voor eenmalige aanmelding (SSO) voor omleiden gemaakt waarmee gebruikers van macOS 10.15 +-toegang krijgen tot Microsoft-apps, organisatie-apps en websites die ondersteuning bieden voor de SSO-functie van Apple en verificatie met behulp van Azure AD, met één aanmelding. Met de release van de Microsoft Enterprise SSO-invoegtoepassing kunt u de SSO-extensie configureren met het nieuwe type app-extensie van Microsoft Azure AD (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **macOS** voor platform > **Apparaatfuncties** voor profiel > **App-extensie voor eenmalige aanmelding** > Type van app-extensie voor SSO > **Microsoft Azure AD**).

Gebruikers moeten de bedrijfsportal-app op hun macOS-apparaat installeren en zich aanmelden om eenmalige aanmelding met het type app-extensie voor SSO van Microsoft Azure AD te kunnen uitvoeren. 

Zie [App-extensie voor eenmalige aanmelding](../configuration/device-features-configure.md#single-sign-on-app-extension) voor meer informatie over app-extensies voor SSO voor macOS.

Van toepassing op:
- macOS 10.15 of hoger

### <a name="use-sso-app-extensions-on-more-iosipados-apps-with-the-microsoft-enterprise-sso-plug-in---7369991---"></a>App-extensies voor eenmalige aanmelding gebruiken voor meer iOS- en iPadOS-apps met de Microsoft Enterprise SSO-invoegtoepassing<!-- 7369991 -->
De [Microsoft Enterprise SSO-invoegtoepassing voor Apple-apparaten](https://docs.microsoft.com/azure/active-directory/develop/apple-sso-plugin) kan worden gebruikt met alle apps die ondersteuning bieden voor app-extensies voor SSO. In Intune betekent deze functie dat de invoegtoepassing werkt met mobiele iOS/iPadOS-apps die niet gebruikmaken van de Microsoft Authentication Library (MSAL) voor Apple-apparaten. De apps hoeven geen MSAL te gebruiken, maar ze moeten wel worden geverifieerd bij Azure AD-eindpunten.

Als u uw iOS-/iPadOS-apps wilt configureren voor het gebruik van SSO met de invoegtoepassing, voegt u de app-bundel-id's toe aan een iOS-/iPadOS-configuratieprofiel (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatfuncties** voor profiel > **App-extensie voor eenmalige aanmelding** > **Microsoft Azure AD** Type van app-extensie voor SSO > **App-bundel-IDs**).

Als u wilt zien welke extensie-instellingen voor SSO-apps u kunt configureren, gaat u naar [App-extensie voor eenmalige aanmelding](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Van toepassing op:
- iOS/iPadOS

<!-- ***********************************************-->
<!-- ## Device enrollment-->




<!-- ***********************************************-->
## <a name="device-management"></a>Apparaatbeheer

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Ondersteuning van PowerShell-scripts voor BYOD-apparaten<!-- 1862833  -->
PowerShell-scripts bieden ondersteuning voor apparaten die bij Azure AD zijn geregistreerd in Intune. Zie [PowerShell-scripts op Windows 10-apparaten gebruiken in Intune](../apps/intune-management-extension.md) voor meer informatie over PowerShell. Deze functionaliteit biedt geen ondersteuning voor apparaten waarop de Windows 10 Home-editie wordt uitgevoerd.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bevat een logboek met apparaatgegevens<!--6014987  -->
De logboeken voor Intune-apparaatgegevens vindt u in **Rapporten** > **Logboekanalyse**. U kunt apparaatgegevens met elkaar in verband brengen om aangepaste query's en Azure-werkmappen te maken.

### <a name="tenant-attach-device-timeline-in-the-admin-center--7220536-cm7141381---"></a>Tenantkoppeling: Tijdlijn van het apparaat in het beheercentrum<!--7220536, CM7141381 -->
Wanneer Configuration Manager een apparaat synchroniseert met Microsoft Endpoint Manager via een tenantkoppeling, kunt u een tijdlijn van gebeurtenissen bekijken. Deze tijdlijn toont eerdere activiteiten op het apparaat die u kunnen helpen bij het oplossen van problemen. Zie [Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_timeline) voor meer informatie.  

### <a name="tenant-attach-install-an-application-from-the-admin-center---7220536-cm6024389---"></a>Tenantkoppeling: Een toepassing installeren vanuit het beheercentrum<!-- 7220536, CM6024389 -->
Vanuit het Microsoft Endpoint Management-beheercentrum kunt u de installatie van een toepassing in realtime initiëren voor een apparaat dat is gekoppeld via een tenant. Zie [Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_apps) voor meer informatie.

### <a name="tenant-attach-cmpivot-from-the-admin-center--7220536-cm6024392---"></a>Tenantkoppeling: CMPivot vanuit het beheercentrum<!--7220536, CM6024392 -->
U kunt profiteren van alle voordelen van [CMPivot](../../configmgr/tenant-attach/cmpivot-overview-attached.md) in het Microsoft Endpoint Manager-beheercentrum. Sta aanvullende persona's, zoals Helpdesk, toe om vanuit de cloud realtimequery's te starten op een afzonderlijk, door ConfigMgr beheerd apparaat en de resultaten te retourneren naar het beheercentrum. Dit biedt alle traditionele voordelen van CMPivot, waarmee IT-beheerders en andere aangewezen personen de status van apparaten in hun omgeving snel kunnen beoordelen en actie kunnen ondernemen. Zie [Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_cmpivot) voor meer informatie. 

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Tenantkoppeling: Scripts uitvoeren vanuit het beheercentrum<!--7220536, CM6234688 -->
U kunt de krachtige on-premises functie [Scripts uitvoeren](../../configmgr/apps/deploy-use/create-deploy-scripts.md) van Configuration Manager in het Microsoft Endpoint Manager-beheercentrum gebruiken. Sta extra persona's, zoals Helpdesk, toe om PowerShell-scripts vanuit de cloud uit te voeren met een individueel door Configuration Manager beheerd apparaat. Hiermee krijgt u alle bekende voordelen van PowerShell-scripts die al zijn gedefinieerd en goedgekeurd door de Configuration Manager-beheerder voor deze nieuwe omgeving. Zie [Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts) voor meer informatie. 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Software-updates implementeren op macOS-apparaten <!-- 3194876 -->
U kunt software-updates implementeren voor groepen macOS-apparaten. Deze functie omvat essentiële updates, firmware-updates, configuratiebestanden en andere updates. U kunt updates verzenden de volgende keer dat het apparaat wordt ingecheckt, of een wekelijkse planning selecteren om updates te implementeren binnen of buiten tijdvensters die u instelt. Dit is handig als u apparaten wilt bijwerken buiten standaardwerkuren of wanneer de helpdesk werkt met een volledige bezetting. U krijgt ook een gedetailleerd rapport met alle macOS-apparaten waarop updates zijn geïmplementeerd. U kunt de rapportgegevens filteren per apparaat, om de status van bepaalde updates te bekijken.

### <a name="associated-licenses-revoked-before-deletion-of-apple-vpp-token--6195322---"></a>Gekoppelde licenties ingetrokken voordat het Apple VPP-token wordt verwijderd<!--6195322 -->
Wanneer u in een toekomstige update een Apple VPP-token verwijdert in Microsoft Endpoint Manager, worden alle aan dit token gekoppelde Intune-licenties automatisch ingetrokken vóór de verwijdering.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Sjabloon voor Power BI-nalevingsrapport BI V 2.0<!-- 636958  -->
Beheerders kunnen de sjabloonversie van het Power BI-compatibiliteitsrapport bijwerken van V 1.0 naar V 2.0. V 2.0 bevat een verbeterd ontwerp, evenals wijzigingen in de berekeningen en gegevens die worden opgehaald als onderdeel van de sjabloon. Zie [Verbinding maken met het datawarehouse met Power BI](../developer/reports-proc-get-a-link-powerbi.md) voor gerelateerde informatie.

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Beveiliging

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Ondersteuning voor app-beveiligingsbeleid voor Symantec Endpoint Security en Check Point Sandblast<!--  4452423, 4731168 -->

In oktober 2019 is aan het app-beveiligingsbeleid van Intune de mogelijkheid toegevoegd om gegevens van onze MTD-partners (Microsoft Threat Defense) te gebruiken. We voegen ondersteuning toe voor de volgende partners, voor gebruik van een app-beveiligingsbeleid om de bedrijfsgegevens van gebruikers te blokkeren of selectief te wissen, op basis van de status van een apparaat:

- **Check Point Sandblast** voor Android, iOS en iPadOS
- **Symantec Endpoint Security** voor Android, iOS en iPadOS

Raadpleeg [Mobile Threat Defense-app-beveiligingsbeleid maken met Intune](../protect/mtd-app-protection-policy.md) voor informatie over het gebruik van app-beveiligingsbeleid met MTD-partners.

### <a name="microsoft-defender-atp-creates-endpoint-manager-security-task-with-vulnerability-details---5568193----"></a>Microsoft Defender ATP maakt Endpoint Manager-beveiligingstaak met informatie over het beveiligingsprobleem<!-- 5568193  -->
Met Threat and Vulnerability Management (TVM) in Microsoft Defender ATP worden onjuist geconfigureerde beveiligingsinstellingen op apparaten gedetecteerd. Beheerders gebruiken deze informatie om kwetsbare apparaten bij te werken.

Binnenkort kan Microsoft Defender ATP een Endpoint Manager-beveiligingstaak (**Endpoint Manager** > **Eindpuntbeveiliging** > **Beveiligingstaken**) met de informatie over het beveiligingsprobleem genereren en de betreffende apparaten weergeven. IT-beheerders kunnen de beveiligingstaak accepteren en de vereiste configuratie implementeren. 

Zie [Intune gebruiken voor het oplossen van beveiligingsproblemen geïdentificeerd door Microsoft Defender ATP](../protect/atp-manage-vulnerabilities.md) voor meer informatie over beveiligingstaken.

### <a name="changes-for-endpoint-security-antivirus-policy-exclusions--5583940-6018119----"></a>Wijzigingen in uitsluitingen antiviurusbeleid voor eindpuntbeveiliging<!--5583940, 6018119  -->
We introduceren twee wijzigingen voor het beheren van de uitsluitingslijsten van Microsoft Defender Antivirus die u configureert als onderdeel van een antivirusbeleid voor eindpuntbeveiliging. (**Eindpuntbeveiliging** > **Antivirus** > **Beleid maken** > **Windows 10 en hoger** voor platform). Deze twee wijzigingen helpen conflicten tussen beleid te voorkomen en bestaande beleidsregels die conflicteerden, veroorzaken geen conflict meer voor de lijst met uitsluitingen:

- Eerst voegen we een nieuw profieltype toe voor Windows 10 en hoger; **Microsoft Defender Antivirus-uitsluitingen**.  Dit nieuwe profieltype bevat alleen de instellingen voor het opgeven van een lijst met *processen*, *bestandsextensies* en *bestanden* en *mappen* van Defender die niet door Microsoft Defender moeten worden gescand. Dit kan u helpen het beheer van uw uitsluitingslijsten te vereenvoudigen door deze te scheiden van andere beleidsconfiguraties.
- De tweede wijziging is dat de lijst met uitzonderingen die u in verschillende profielen definieert, wordt samengevoegd tot één lijst met uitsluitingen voor elk apparaat of elke gebruiker, op basis van de afzonderlijke beleidsregels die van toepassing zijn op een specifieke gebruiker of een specifiek apparaat. Wanneer u bijvoorbeeld een gebruiker met drie afzonderlijke beleidsregels hebt, worden de uitsluitingslijsten van die drie beleidsregels samengevoegd in één hoofdverzameling van Microsoft Defender Antivirus-uitsluitingen, die vervolgens worden toegepast op de gebruiker. Deze samenvoeging bevat de uitsluitingslijsten van het nieuwe profieltype die zijn toegevoegd, evenals de bestaande beleidsregels die u hebt geconfigureerd in een *Microsoft Defender Antivirus*-profiel.



<!-- ***********************************************-->
## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Zie tevens

Voor meer informatie over recente ontwikkelingen raadpleegt u [Wat is er nieuw in Microsoft Intune?](whats-new.md).
