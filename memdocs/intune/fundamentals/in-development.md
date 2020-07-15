---
title: In ontwikkeling - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-functies in ontwikkeling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/26/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5afca831e2f3cbcda69150adcbbcff996bf99554
ms.sourcegitcommit: 01c1ca337e82c5e8e92153079ed89f79e20bde9e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/09/2020
ms.locfileid: "86157804"
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

### <a name="smime-for-outlook-on-ios-and-android-enterprise-devices-managed-without-enrollment---6517155----"></a>S/MIME voor Outlook op iOS- en Android Enterprise-apparaten die worden beheerd zonder inschrijving<!-- 6517155  -->
U kunt S/MIME voor Outlook op iOS- en Android Enterprise-apparaten inschakelen met behulp van app-configuratiebeleid voor apparaten die worden beheerd zonder inschrijving. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apps** > **App-configuratiebeleid** > **Toevoegen** > **Beheerde apps**. Bovendien kunt u eventueel toestaan dat gebruikers deze instelling wijzigen in Outlook. Zie [Microsoft Outlook-configuratie-instellingen](../apps/app-configuration-policies-outlook.md) voor meer informatie over Outlook-configuratie-instellingen.

### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707----"></a>iOS-bedrijfsportal biedt ondersteuning voor Automatische apparaatinschrijving van Apple zonder gebruikersaffiniteit<!-- 7282707  --> 
iOS-bedrijfsportal wordt ondersteund op apparaten die zijn ingeschreven met behulp van Automatische apparaatinschrijving van Apple zonder dat een toegewezen gebruiker is vereist. Een eindgebruiker kan zich aanmelden bij de iOS-bedrijfsportal om zichzelf de primaire gebruiker te maken op een iOS-/iPadOS-apparaat dat is ingeschreven zonder apparaataffiniteit. Zie [iOS/iPadOS-apparaten automatisch inschrijven met automatische apparaatinschrijving van Apple](../enrollment/device-enrollment-program-enroll-ios.md) voor meer informatie over automatische apparaatinschrijving.

### <a name="win32-app-installation-notifications-and-the-company-portal---7485945----"></a>Meldingen over Win32-app-installatie en de bedrijfsportal<!-- 7485945  -->
Eindgebruikers kunnen bepalen of de toepassingen die worden weergegeven in de [Microsoft Intune-webbedrijfsportal](https://portal.manage.microsoft.com/) moeten worden geopend met de bedrijfsportal-app of via de webbedrijfsportal. Deze optie is alleen beschikbaar als de eindgebruiker de bedrijfsportal-app heeft geïnstalleerd en een webbedrijfsportal-toepassing start buiten een browser.

### <a name="the-company-portal-adds-configuration-manager-application-support---4297660---"></a>De bedrijfsportal voegt ondersteuning voor Configuration Manager-toepassingen toe<!-- 4297660 -->
De bedrijfsportal biedt nu ondersteuning voor Configuration Manager-toepassingen. Met deze functie kunnen eindgebruikers zowel Configuration Manager-toepassingen als met Intune geïmplementeerde toepassingen zien in de bedrijfsportal voor co-beheerde klanten. Deze ondersteuning helpt beheerders bij het consolideren van de verschillende portal-ervaringen van eindgebruikers. Zie [De bedrijfsportal-app configureren op co-beheerde apparaten](https://docs.microsoft.com/mem/configmgr/core/get-started/2020/technical-preview-2006#bkmk_portal) voor meer informatie.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Apparaatconfiguratie

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>De nalevingsstatus van apparaten van externe MDM-partners instellen<!-- 6361689   -->
Microsoft 365-klanten die eigenaar zijn van MDM-oplossingen van derden, kunnen beleid voor voorwaardelijke toegang afdwingen voor Microsoft 365-apps op iOS en Android via integratie met de service Microsoft Intune-apparaatcompatibiliteit. De MDM-leverancier van derden maakt gebruik van de service Intune-apparaatcompatibiliteit om nalevingsgegevens van apparaten naar Intune te verzenden. Intune evalueert vervolgens om te bepalen of het apparaat wordt vertrouwd en stelt de kenmerken voor voorwaardelijke toegang in Azure AD in.  Klanten moeten beleid voor voorwaardelijke toegang van Azure AD instellen in het Microsoft Endpoint Manager-beheercentrum of de Azure AD-portal.  


### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nieuwe VPN-instellingen voor Windows 10-apparaten en nieuwere apparaten<!-- 6602122  -->
Wanneer u een VPN-profiel maakt met behulp van het IKEv2-verbindingstype, kunt u nieuwe instellingen configureren (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Windows 10 en hoger** als platform > **VPN** als profiel > **Basis-VPN**):

- **Apparaattunnel**: Hiermee kunnen apparaten automatisch verbinding maken met VPN zonder tussenkomst van de gebruiker, waaronder aanmelding. Voor deze functie moet u **AlwaysOn**inschakelen en **Machinecertificaten** als verificatiemethode gebruiken.
- Instellingen van Cryptography-suite: Configureer de algoritmen die worden gebruikt voor het beveiligen van IKE- en onderliggende beveiligingskoppelingen, waarmee u de client- en serverinstellingen kunt afstemmen.

Ga naar [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md) (Windows-apparaatinstellingen om VPN-verbindingen toe te voegen met Intune) voor een overzicht van de instellingen die u kunt configureren.

Van toepassing op:
- Windows 10 en nieuwer

### <a name="new-features-for-managed-home-screen-on-android-enterprise-device-owner-dedicated-devices-cosu---7414175-7133328-7133720-7134873-7135184----"></a>Nieuwe functies voor het beheerde startscherm op toegewezen apparaten van Android Enterprise-apparaateigenaar (COSU)<!-- 7414175 7133328 7133720 7134873 7135184  -->
Op Android Enterprise-apparaten kunnen beheerders configuratieprofielen voor apparaten gebruiken om het beheerde startscherm aan te passen op toegewezen apparaten, met behulp van de kioskmodus voor meerdere apps (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** voor platform > **Alleen apparaateigenaar** > **Apparaatbeperkingen** voor profiel > **Apparaatervaring**).

Meer specifiek, u kunt:

- Pictogrammen aanpassen, de schermstand wijzigen, en app-meldingen op badgepictogrammen weergeven <!--7414175-->
- Het ingangspunt voor beheerde instellingen verbergen <!--7133328-->
- Eenvoudiger toegang krijgen tot het foutopsporingsmenu <!--7133720-->
- Een lijst met toegestane Wi-Fi-netwerken maken <!-- 7134873-->
- Eenvoudiger toegang krijgen tot apparaatgegevens <!-- 7135184-->

Zie [Android Enterprise-apparaatinstellingen voor beheer van functies](../configuration/device-restrictions-android-for-work.md) voor meer informatie.

Van toepassing op:

- Toegewezen apparaten van Android Enterprise-apparaateigenaar (COSU)

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Apparaatinschrijving

### <a name="corporate-owned-personally-enabled-devices-preview--4442275---"></a>Persoonlijke apparaten in bedrijfseigendom (preview)<!--4442275 -->
Intune biedt ondersteuning voor Android Enterprise-apparaten in bedrijfseigendom met een werkprofiel voor OS-versies Android 8 en hoger. Apparaten in bedrijfseigendom met een werkprofiel is een van de bedrijfsbeheerscenario's in de set met Android Enterprise-oplossingen. Dit scenario geldt voor apparaten met één gebruiker, die zijn bedoeld voor zakelijk en persoonlijk gebruik. Dit scenario in bedrijfseigendom, ingeschakeld voor persoonlijk gebruik (COPE), biedt:

- containeropslag voor zakelijk en persoonlijk profiel
- beheer op apparaatniveau voor beheerders
- een garantie voor eindgebruikers dat hun persoonlijke gegevens en toepassingen privé blijven

De eerste openbare preview-versie bevat een subset met functies die worden opgenomen in de algemeen beschikbare versie. Extra functies worden gefaseerd toegevoegd. De functies die beschikbaar zijn in de eerste preview zijn onder andere:

- Inschrijving: Beheerders kunnen meerdere inschrijvingsprofielen maken met unieke tokens die niet verlopen. Apparaatregistratie kan worden uitgevoerd via NFC, tokenvermelding, QR-code, Zero Touch, of Knox Mobile Enrollment.
- Apparaatconfiguratie: Een subset met de bestaande volledig beheerde en toegewezen apparaatinstellingen.
- Apparaatnaleving: Nalevingsbeleid dat momenteel beschikbaar is voor volledig beheerde apparaten.
- Apparaatacties: Apparaat verwijderen (fabrieksinstellingen terugzetten), apparaat opnieuw opstarten en apparaat vergrendelen.  
- App-beheer: App-toewijzingen, app-configuratie en de bijbehorende rapportagemogelijkheden 
- Voorwaardelijke toegang



<!-- ***********************************************-->
## <a name="device-management"></a>Apparaatbeheer

### <a name="device-compliance-logs-now-in-english--6014904---"></a>Logboeken voor apparaatnaleving, nu in het Engels<!--6014904 -->
De IntuneDeviceComplianceOrg-logboeken bevatten alleen opsommingen voor ComplianceState, OwnerType en DeviceHealthThreatLevel. In een toekomstige update bevatten deze logboeken Engelse informatie in de kolommen.

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

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nieuwe samenvoeglogica voor Windows 10-apparaten<!--179048-->
Als een klant nu de installatiekopie terugzet op een apparaat en het vervolgens opnieuw inschrijft, worden er meerdere records voor het apparaat weergegeven in de beheerconsole van Microsoft Endpoint Manager. Er wordt een nieuwe samenvoeglogica ontwikkeld voor het samenvoegen van dergelijke dubbele records voor Windows 10-apparaten.

### <a name="updates-to-the-remote-lock-action-for-macos-devices--7032805---"></a>Updates voor de actie voor extern vergrendelen voor macOS-apparaten<!--7032805 -->
Updates voor de actie voor extern vergrendelen voor macOS-apparaten omvatten:
- De herstelpincode wordt 30 dagen vóór het verwijderen weergegeven (in plaats van zeven dagen).
- Als een beheerder een tweede browser heeft geopend en de opdracht opnieuw probeert te activeren vanuit een ander tabblad of een andere browser, mag deze opdracht worden uitgevoerd in Intune. Maar de rapportagestatus wordt ingesteld op mislukt, in plaats van dat er een nieuwe pincode wordt gegenereerd.
- De beheerder kan geen andere externe vergrendelingsopdracht uitvoeren als de vorige opdracht nog in behandeling is of als het apparaat niet opnieuw is ingecheckt.
Deze wijzigingen zijn ontworpen om te voorkomen dat de juiste pincode wordt overschreven na meerdere opdrachten voor extern vergrendelen.

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Software-updates implementeren op macOS-apparaten <!-- 3194876 -->
U kunt software-updates implementeren voor groepen macOS-apparaten. Deze functie omvat essentiële updates, firmware-updates, configuratiebestanden en andere updates. U kunt updates verzenden de volgende keer dat het apparaat wordt ingecheckt, of een wekelijkse planning selecteren om updates te implementeren binnen of buiten tijdvensters die u instelt. Dit is handig als u apparaten wilt bijwerken buiten standaardwerkuren of wanneer de helpdesk werkt met een volledige bezetting. U krijgt ook een gedetailleerd rapport met alle macOS-apparaten waarop updates zijn geïmplementeerd. U kunt de rapportgegevens filteren per apparaat, om de status van bepaalde updates te bekijken.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

### <a name="additional-data-warehouse-v10-properties---6125732-----"></a>Aanvullende Data Warehouse v1.0-eigenschappen<!-- 6125732   -->
Er zijn aanvullende eigenschappen beschikbaar met behulp van Intune Data Warehouse v1.0. Via de entiteit [apparaten](../developer/reports-ref-devices.md#devices) zijn nu de volgende eigenschappen beschikbaar:
- `ethernetMacAddress` - De unieke netwerk-id van dit apparaat.
- `office365Version` - De versie van Office 365 die op het apparaat is geïnstalleerd.

Via de entiteit [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) zijn nu de volgende eigenschappen beschikbaar:
- `physicalMemoryInBytes` - Het fysieke geheugen in bytes.
- `totalStorageSpaceInBytes`: de totale opslagcapaciteit in bytes.

Zie [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md) voor meer informatie.

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Sjabloon voor Power BI-nalevingsrapport BI V 2.0<!-- 636958  -->
Beheerders kunnen de sjabloonversie van het Power BI-compatibiliteitsrapport bijwerken van V 1.0 naar V 2.0. V 2.0 bevat een verbeterd ontwerp, evenals wijzigingen in de berekeningen en gegevens die worden opgehaald als onderdeel van de sjabloon. Zie [Verbinding maken met het datawarehouse met Power BI](../developer/reports-proc-get-a-link-powerbi.md) voor gerelateerde informatie.

<!-- ***********************************************-->
## <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer

### <a name="scope-tag-support-for-customization-policies--6182440---"></a>Ondersteuning voor bereiktags voor aanpassingsbeleid<!--6182440 -->
U kunt bereiktags toewijzen aan aanpassingsbeleid. Als u dit wilt doen, gaat u naar het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenantbeheer**> **Aanpassing**. Hier ziet u de configuratieopties voor **Bereiktags**.

### <a name="assign-profile-and-update-profile-permission-changes--7177586---"></a>Wijzigingen in de machtigingen voor Profiel toewijzen en Profiel bijwerken<!--7177586 -->
Op rollen gebaseerd toegangsbeheer wordt gewijzigd voor Profiel toewijzen en Profiel bijwerken:
- Profiel toewijzen: Beheerders met deze machtiging kunnen de profielen ook toewijzen aan tokens, en kunnen een standaardprofiel toewijzen aan een token.
- Profiel bijwerken: Beheerders met deze machtiging kunnen alleen bestaande profielen bijwerken.

<!-- ***********************************************-->
## <a name="security"></a>Beveiliging

### <a name="app-protection-policy-support-for-symantec-endpoint-security-and-check-point-sandblast----4452423-4731168---"></a>Ondersteuning voor app-beveiligingsbeleid voor Symantec Endpoint Security en Check Point Sandblast<!--  4452423, 4731168 -->

In oktober 2019 is aan het app-beveiligingsbeleid van Intune de mogelijkheid toegevoegd om gegevens van onze MTD-partners (Microsoft Threat Defense) te gebruiken. We voegen ondersteuning toe voor de volgende partners, voor gebruik van een app-beveiligingsbeleid om de bedrijfsgegevens van gebruikers te blokkeren of selectief te wissen, op basis van de status van een apparaat:

- **Check Point Sandblast** voor Android, iOS en iPadOS
- **Symantec Endpoint Security** voor Android, iOS en iPadOS

Raadpleeg [Mobile Threat Defense-app-beveiligingsbeleid maken met Intune](../protect/mtd-app-protection-policy.md) voor informatie over het gebruik van app-beveiligingsbeleid met MTD-partners.

### <a name="store-the-recovery-key-for-a-macos-device-that-was-encrypted-with-filevault-before-enrolling-with-intune--5239424-----"></a>De herstelsleutel opslaan voor een macOS-apparaat dat is versleuteld met FileVault vóór inschrijving bij Intune<!--5239424   -->
Binnenkort hoeven eindgebruikers van een macOS-apparaat dat niet is versleuteld op basis van FileVault-beleid van Intune, of dat is versleuteld vóór inschrijving bij Intune, hun apparaat niet meer te ontsleutelen zodat het vervolgens opnieuw kan worden versleuteld met Intune. In plaats hiervan blijft de huidige versleuteling behouden. De gebruiker kan naar de website van de bedrijfsportal gaan en daar *Herstelsleutel opslaan* kiezen om hun persoonlijke herstelsleutel voor het versleutelde macOS-apparaat te verzenden. Bij het verzenden van een geldige sleutel wordt de persoonlijke sleutel in Intune gewisseld om een nieuwe sleutel te genereren, die beschikbaar blijft voor de gebruiker via de website van de bedrijfsportal, de iOS-bedrijfsportal, de Android-bedrijfsportal of de Intune-app. Gebruikers hebben vervolgens vanaf elk apparaat toegang tot deze locaties om de sleutel weer te geven wanneer hun macOS-apparaat is vergrendeld.

### <a name="hide-the-personal-recovery-key-from-a-device-user-during-macos-filevault-disk-encryption----5475632----"></a>De persoonlijke herstelsleutel verbergen voor een apparaatgebruiker tijdens macOS FileVault-schijfversleuteling<!--  5475632  -->
We voegen een nieuwe instelling, genaamd *Herstelsleutel verbergen*, toe aan het schijfversleutelingsbeleid voor eindpuntbeveiliging voor FileVault (**Eindpuntbeveiliging** > **Schijfversleuteling** > **Profiel maken** > **macOS** > **FileVault**). Wanneer u de nieuwe instelling inschakelt, wordt de persoonlijke herstelsleutel tijdens de versleuteling in Intune verborgen voor de gebruiker van het macOS-apparaat. Door de sleutel op dit moment te verbergen blijft deze beveiligd, omdat gebruikers deze niet kunnen noteren terwijl ze wachten tot het apparaat is versleuteld. In plaats hiervan kan een gebruiker, wanneer herstel is vereist, altijd een willekeurig apparaat gebruiken om de persoonlijke herstelsleutel weer te geven op de website van de Intune-bedrijfsportal.

### <a name="improved-view-of-security-baseline-details-for-devices---5536846-----"></a>Verbeterde weergave van details voor beveiligingsbasislijn voor apparaten<!-- 5536846   -->
We werken aan het verbeteren van de weergave van details voor de instellingen voor de beveiligingsbasislijn, wanneer u inzoomt op de details voor een apparaat (**Eindpuntbeveiliging** > **Apparaten**).  Voor elke toegewezen beveiligingsbasislijn kunt u een platte lijst met details bekijken voor elke instelling die instellingscategorieën, instellingsnamen, en de status van elke instelling op het desbetreffende apparaat bevat.

### <a name="manage-source-locations-for-definition-updates-with-endpoint-security-antivirus-policy-for-windows-10-devices---6347801----"></a>Bronlocaties beheren voor definitie-updates met antivirusbeleid voor eindpuntbeveiliging voor Windows 10-apparaten<!-- 6347801  -->  
Er worden twee nieuwe instellingen toegevoegd aan de categorie *Updates* van het antivirusbeleid voor eindpuntbeveiliging voor Windows 10-apparaten. Deze kunnen u helpen te beheren hoe apparaten updatedefinities ophalen (**Eindpuntbeveiliging** > ** Antivirus** > **Beleid maken** > **Windows 10 en hoger** > **Microsoft Defender Antivirus**).

Met de nieuwe instellingen kunt u UNC-bestandsshares toevoegen als bronlocaties voor downloads van definitie-updates, en de volgorde definiëren waarin contact wordt opgenomen met de verschillende bronlocaties. Met de nieuwe instellingen worden de volgende Defender CSP's beheerd:

- [signatureupdatefilesharessources](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)
- [signatureupdatefallbackorder](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

### <a name="endpoint-detection-and-response-policy-for-onboarding-tenant-attached-devices-to-mdatp-is-moving-out-of-preview---7303816-----"></a>Eindpuntdetectie en -respons om aan een tenant gekoppelde apparaten te onboarden bij MDATP verlaat binnenkort de preview-fase<!-- 7303816   -->
Als onderdeel van eindpuntbeveiliging in Intune verlaat de ondersteuning van EDR-beleid (eindpuntdetectie en -respons) voor gebruik met apparaten die worden beheerd met Configuration Manager, binnenkort de preview-fase en wordt algemeen beschikbaar (**Eindpuntbeveiliging** > **Eindpuntdetectie en -respons** > **Beleid maken** > **Windows 10 en Windows Server**). Wanneer u [Tenantkoppeling voor Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md) beheert, kunt u vervolgens EDR-beleid gebruiken om apparaten die worden beheerd met Configuration Manager, te onboarden bij Microsoft Defender ATP (Advanced Threat Protection). 

### <a name="improvements-for-the-security-baselines-node---7433136-----"></a>Verbeteringen in het knooppunt voor beveiligingsbasislijnen<!-- 7433136   -->
Om de bruikbaarheid van het knooppunt voor beveiligingsbasislijnen te verbeteren in het Microsoft Endpoint Manager-beheercentrum wordt het tabblad *Overzicht* voor elke basislijn verwijderd. In plaats hiervan wordt het tabblad **Profiel** beschikbaar (**Eindpuntbeveiliging** > **Beveiligingsbasislijnen** > *basislijn*).

Op de *Overzichtspagina* voor elke basislijn worden grafieken en tegels weergegeven waarin de resultaten worden samengevoegd uit de basislijnversie die u hebt geïmplementeerd. Deze informatie wordt gedupliceerd uit wat u ziet wanneer u inzoomt op een versie voor meer details. Nadat de *Overzichtspagina* is verwijderd, blijven deze grafieken en samengevoegde details beschikbaar wanneer u rechtstreeks inzoomt op de versie.  

### <a name="firewall-rule-migration-tool-preview---6423187----"></a>Preview-versie van het migratiehulpprogramma voor firewallregels<!-- 6423187  -->
Als openbare preview werken we aan een hulpprogramma op basis van PowerShell waarmee Windows Defender Firewall-regels worden gemigreerd. Wanneer u het hulpprogramma installeert en uitvoert, worden automatisch beleidsregels voor firewallregels voor eindpuntbeveiliging gemaakt voor Intune, die zijn gebaseerd op de huidige configuratie van een Windows 10-client.

### <a name="new-settings-for-the-device-control-profile-in-endpoint-security-attack-surface-reduction-policy--7032084---"></a>Nieuwe instellingen voor het Attack Surface Reduction-beleid (kwetsbaarheid voor aanvallen verminderen) voor het profiel Apparaatbeheer in eindpuntbeveiliging<!--7032084 -->
Er worden verschillende instellingen voor Windows 10-apparaten toegevoegd aan het Attack Surface Reduction-beleid voor het profiel Apparaatbeheer in eindpuntbeveiliging (**Eindpuntbeveiliging** > **Attack Surface Reduction** > **Beleid maken** > **Windows 10 en hoger** > **Apparaatbeheer**). 

De nieuwe instelling is gelijk aan de instellingen die op dit moment beschikbaar zijn in [Profielen voor apparaatbeperking ](../configuration/device-restrictions-windows-10.md) voor *Apparaatconfiguratie*. De instellingen die worden toegevoegd aan het profiel *Apparaatbeheer*, moeten verschillende Bluetooth-instellingen omvatten.  


<!-- ***********************************************-->
## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Zie tevens

Voor meer informatie over recente ontwikkelingen raadpleegt u [Wat is er nieuw in Microsoft Intune?](whats-new.md).
