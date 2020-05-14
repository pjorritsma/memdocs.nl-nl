---
title: In ontwikkeling - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-functies in ontwikkeling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7827c85585d630f64ba9c6d342b6275fca506b1d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906962"
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

### <a name="support-for-multiple-accounts-in-company-portal-for-mac---5779449----"></a>Ondersteuning voor meerdere accounts in de bedrijfsportal voor Mac<!-- 5779449  -->
Met de bedrijfsportal op macOS-apparaten worden gebruikersaccounts nu in de cache opgeslagen, waardoor het aanmelden eenvoudiger wordt. Gebruikers hoeven zich niet meer bij de bedrijfsportal aan te melden wanneer ze de toepassing starten. Daarnaast geeft de bedrijfsportal een accountkiezer weer als er meerdere gebruikersaccounts in de cache zijn opgeslagen, zodat gebruikers hun gebruikersnaam niet hoeven in te voeren. 

### <a name="auto-update-vpp-available-apps---3640511----"></a>Beschikbare VPP-apps automatisch bijwerken<!-- 3640511  -->
Apps die zijn gepubliceerd als voor Volume Purchase Program (VPP) beschikbare apps, worden automatisch bijgewerkt wanneer **Automatische updates van apps** is ingeschakeld voor het VPP-token. Momenteel worden voor VPP beschikbare apps niet automatisch bijgewerkt. Eindgebruikers moeten in plaats daarvan naar de bedrijfsportal gaan en de app opnieuw installeren als er een nieuwere versie beschikbaar is. De vereiste apps ondersteunen momenteel echter wel automatische updates.

### <a name="customize-self-service-device-actions-in-the-company-portal--4393379----"></a>Selfservice-apparaatacties in de bedrijfsportal aanpassen<!--4393379  -->
U kunt de beschikbare selfservice-apparaatacties aanpassen die worden weergegeven aan eindgebruikers in de bedrijfsportal-app en -website. Als u onbedoelde apparaatacties wilt helpen voorkomen, kunt u deze instellingen configureren voor de bedrijfsportal-app door **Tenantbeheer** > **Aanpassing** > **Maken** > **Functies verbergen** te selecteren. Hiervoor zijn de volgende opties beschikbaar:
- Knop **Verwijderen** verbergen op zakelijke Windows-apparaten.
- Knop **Opnieuw instellen** verbergen op zakelijke Windows-apparaten.
- Knop **Opnieuw instellen** verbergen op zakelijke iOS-apparaten.
- Knop **Verwijderen** verbergen op zakelijke iOS-apparaten.

Raadpleeg [Selfservice-apparaatacties voor gebruikers van de bedrijfsportal](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal) voor meer informatie.

### <a name="unified-delivery-of-azure-ad-enterprise-or-office-online-applications-in-the-company-portal--4404429---"></a>Unified delivery van Azure AD Enterprise- of Office Online-apps in de bedrijfsportal<!--4404429 -->
U kunt de weergave van Azure AD Enterprise-of Office Online-apps in de bedrijfsportal in- of uitschakelen (**Verbergen** of **Weergeven**). Elke gebruiker ziet de volledige toepassingscatalogus van de gekozen Microsoft-service. Standaard wordt elke extra app-bron ingesteld op **Verbergen**. Deze functie gaat van kracht op de bedrijfsportal-website in de 2005-release; ondersteuning in de Windows-, iOS/iPadOS- en macOS-bedrijfsportals zal naar verwachting volgen. U vindt deze toekomstige instelling door in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) **Tenantbeheer** > **Aanpassing** te selecteren. Zie [De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen](../apps/company-portal-app.md) voor informatie.

### <a name="search-the-intune-docs-from-the-company-portal---1736480---"></a>De Intune-documentatie zoeken in de bedrijfsportal<!-- 1736480 -->
U kunt nu rechtstreeks vanaf de bedrijfsportal voor macOS-app zoeken in de Intune-documentatie. Selecteer in de menubalk **Help** > **Zoeken** en voer de trefwoorden van uw zoekopdracht in om snel antwoorden op uw vragen te vinden.

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Bedrijfsportal voor Android helpt gebruikers apps te verkrijgen na registratie van het werkprofiel <!-- 6103999  -->
De in-app-richtlijnen in de bedrijfsportal worden verbeterd zodat gebruikers gemakkelijker apps kunnen zoeken en installeren.  Nadat gebruikers zich hebben geregistreerd voor werkprofielbeheer, zien ze een bericht dat ze aanbevolen apps kunnen vinden in de Google Play-versie met badge. Gebruikers zien ook de nieuwe koppeling **Apps downloaden** in de bedrijfsportal-lade aan de linkerkant. Om ruimte te maken voor deze nieuwe en verbeterde ervaringen, wordt het tabblad **APPS** verwijderd. 

### <a name="android-company-portal-user-experience---5736084---"></a>Gebruikerservaring van de Android-bedrijfsportal<!-- 5736084 -->
In de 2005-release van de Android-bedrijfsportal zien eindgebruikers van Android-apparaten aan wie een waarschuwing, blokkering of verwijdering door een app-beveiligingsbeleid is uitgegeven, een nieuwe gebruikerservaring. In plaats van de huidige dialoogvensters zien eindgebruikers een bericht dat een volledige pagina beslaat met een beschrijving van de reden voor de waarschuwing, blokkering of verwijdering en de stappen om het probleem te verhelpen. Zie [App-beveiligingservaring voor Android-apparaten](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) en [Instellingen van app-beveiligingsbeleid voor Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md) voor meer informatie.


<!-- ***********************************************-->
## <a name="device-configuration"></a>Apparaatconfiguratie

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>De instellingen en waarden voor apparaatconfiguratieprofielen worden bijgewerkt voor Windows-platformen<!-- 4091122 -->
Wanneer u apparaatconfiguratieprofielen voor Windows-platformen maakt (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > elke **Windows**-optie voor platform), wijken een aantal instellingen en de bijbehorende waarden af van de CSP; dit kan verwarrend zijn. De namen van instellingen en de bijbehorende waarden worden bijgewerkt zodat deze duidelijker zijn.

Van toepassing op:

- Configuratieprofielen voor Windows 10 en hoger
- Apparaatconfiguratieprofielen voor Windows Holographic voor Bedrijven
- Apparaatconfiguratieprofielen voor Windows 8.1
- Apparaatconfiguratieprofielen voor Windows Phone 8.1

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>De Microsoft Defender ATP-app configureren voor macOS  <!-- 5520115  -->
Binnenkort kunt u de [instellingen](../protect/endpoint-protection-macos.md) configureren voor de Microsoft Defender ATP-app voor apparaten waarop macOS wordt uitgevoerd als onderdeel van een apparaatconfiguratieprofiel voor eindpuntbeveiliging (**Apparaten** > **Configuratieprofielen** > **Profiel maken**, selecteer **macOS** als *Platform* en kies vervolgens **Eindpuntbeveiliging** als *Profieltype*). Voor de configuratie van macOS-apparaten zijn acht instellingen beschikbaar. 

Defender ATP wordt ondersteund op apparaten met macOS 10.13 (High Sierra) en hoger. Bovendien moet de [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md)-app worden geïmplementeerd *nadat* deze instellingen zijn toegepast. De instellingen moeten naar het apparaat worden verzonden voordat de app wordt geïmplementeerd. Bètaversies van macOS worden niet ondersteund.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>De nieuwe FileVault-instelling voor het apparaatconfiguratiebeleid voor eindpuntbeveiliging voor macOS<!-- 5459801   -->
Op de sjabloon [macOS-eindpuntbeveiliging](../protect/endpoint-protection-macos.md) wordt een nieuwe instelling aan de FileVault-categorie toegevoegd: Herstelsleutel verbergen. (**Apparaten** > **Configuratieprofielen** > **Profiel maken**, selecteer **macOS** als het *Platform* en kies vervolgens **Eindpuntbeveiliging** als het *Profieltype*). Door deze instelling wordt de persoonlijke sleutel tijdens de FileVault 2-versleuteling voor de eindgebruiker verborgen. Apparaatgebruikers kunnen hun persoonlijke herstelsleutel op elk gewenst moment weergeven via de bedrijfsportal-app voor iOS of via de bedrijfsportal-website voor het versleutelde macOS-apparaat. Ga naar Apparaatgegevens en klik op *Herstelsleutel ophalen* om de persoonlijke herstelsleutel weer te geven.

Deze instelling is niet beschikbaar in een eerder gemaakt beleid. U moet FileVault-beleidsregels opnieuw maken om deze instelling te configureren zodat u er gebruik van kunt maken. 

### <a name="configure-system-extensions-on-macos-devices---6255624----"></a>Systeemuitbreidingen op macOS-apparaten configureren<!-- 6255624  -->
Op macOS-apparaten kunt u een profiel voor kernelextensies maken om instellingen te configureren op kernelniveau (**Apparaten** > **Configuratieprofielen** > **macOS** voor platform > **Kernelextensies** voor profiel). In een toekomstige versie schaft Apple kernelextensies uiteindelijk af en vervangt deze door systeemextensies. Systeemextensies worden uitgevoerd in de gebruikersruimte en geven geen toegang tot de kernel. Het doel is de beveiliging te verhogen en de eindgebruiker meer controle te bieden, terwijl aanvallen op kernelniveau beperkt worden. Met zowel kernelextensies als systeemextensies kunnen gebruikers app-extensies installeren waarmee de systeemeigen mogelijkheden van het besturingssysteem worden uitgebreid.

In Intune kunt u zowel kernelextensies als systeemextensies configureren (**Apparaten** > **Configuratieprofielen** > **macOS** voor platform > **Systeemextensies** voor profiel). Kernelextensies zijn van toepassing op 10.13.2 en nieuwer. Systeemextensies zijn van toepassing op 10.15 en nieuwer. Vanaf macOS 10.15 tot macOS 10.15.4 kunnen kernelextensies en systeemextensies naast elkaar worden uitgevoerd. 

Zie [macOS-kernelextensies toevoegen](../configuration/kernel-extensions-overview-macos.md) voor meer informatie over kernelextensies op macOS-apparaten.

Van toepassing op:
- macOS 10.15 of hoger

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Apparaatinschrijving

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Eigen apparaten kunnen voor het implementeren gebruikmaken van VPN<!--5015344 -->
Deze functie wordt mogelijk vertraagd.

### <a name="automated-device-sync-interval-down-to-12-hours--3077535---"></a>Interval voor automatisch synchroniseren van apparaten verlaagd tot 12 uur<!--3077535 -->
Voor Automated Device Enrollment van Apple wordt het automatische synchronisatie-interval voor apparaten tussen Intune en Apple Business Manager gereduceerd van 24 uur tot 12 uur. Zie [Beheerde apparaten synchroniseren](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices) voor meer informatie over synchronisatie.

### <a name="autopilot-support-for-hololens-2-devices--6305220--"></a>Autopilot-ondersteuning voor Hololens 2-apparaten<!--6305220-->
Windows Autopilot biedt ondersteuning voor Hololens 2-apparaten. Zie [Windows-apparaten in Intune inschrijven met Windows Autopilot](../enrollment/enrollment-autopilot.md) voor meer informatie over het gebruik van Autopilot in Intune.

### <a name="enrollment-restrictions-will-support-scope-tags--4209550---"></a>Inschrijvingsbeperkingen bieden ondersteuning voor bereiktags<!--4209550 -->
U kunt bereiktags toewijzen aan inschrijvingsbeperkingen. Ga hiervoor naar [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **Inschrijvingsbeperkingen** > **Beperking maken**. Maak een van beide typen beperkingen en u ziet de pagina **Bereiktags**.

### <a name="shared-ipads-for-business--6367326---"></a>Gedeelde iPads voor bedrijven<!--6367326 -->
U kunt Intune en Apple Business Manager gebruiken om snel en veilig Gedeelde iPad in te stellen, zodat meerdere werknemers apparaten kunnen delen. [Gedeelde iPad](https://developer.apple.com/education/shared-ipad/) van Apple biedt een persoonlijke ervaring voor meerdere gebruikers terwijl gebruikersgegevens behouden blijven. Wanneer gebruikers een beheerde Apple ID gebruiken, hebben ze toegang tot hun apps, gegevens en instellingen nadat ze zich hebben aangemeld bij een gedeelde iPad in hun organisatie. Gedeelde iPad werkt met federatieve identiteiten.

Ga naar [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **iOS** > **iOS-inschrijving** > **Registratieprogrammatokens** > kies een token** > **Profielen** > **Profiel maken** > **iOS** om deze functie te zien. Selecteer op de pagina **Beheerinstellingen** de optie **Inschrijven zonder gebruikersaffiniteit** en u ziet de optie **Gedeelde iPad**.

**Van toepassing op:** iPadOS 13.4 en hoger. In deze release is ondersteuning toegevoegd voor tijdelijke sessies met Gedeelde iPad zodat gebruikers zonder een beheerde Apple ID toegang hebben tot een apparaat. Na afmelding worden alle gebruikersgegevens gewist zodat het apparaat direct gereed is voor gebruik. Het apparaat hoeft hierdoor niet meer te worden gewist. 

<!-- ***********************************************-->
## <a name="device-management"></a>Apparaatbeheer

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Ondersteuning van PowerShell-scripts voor BYOD-apparaten<!-- 1862833  -->
PowerShell-scripts bieden ondersteuning voor apparaten die bij Azure AD zijn geregistreerd in Intune. Zie [PowerShell-scripts op Windows 10-apparaten gebruiken in Intune](../apps/intune-management-extension.md) voor meer informatie over PowerShell. Deze functionaliteit biedt geen ondersteuning voor apparaten waarop de Windows 10 Home-editie wordt uitgevoerd.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bevat een logboek met apparaatgegevens<!--6014987  -->
De logboeken voor Intune-apparaatgegevens vindt u in **Rapporten** > **Logboekanalyse**. U kunt apparaatgegevens met elkaar in verband brengen om aangepaste query's en Azure-werkmappen te maken.


### <a name="macos-script-support---6376978----"></a>ondersteuning voor macOS-script<!-- 6376978  -->
Scriptondersteuning voor macOS is nu algemeen beschikbaar. Daarnaast wordt er ondersteuning toegevoegd voor zowel door de gebruiker toegewezen scripts als macOS-apparaten die zijn ingeschreven bij Automated Device Enrollment van Apple (voorheen Device Enrollment Program). Zie [Shell-scripts op macOS-apparaten gebruiken in Intune](../apps/macos-shell-scripts.md) voor meer informatie.

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

### <a name="derived-credentials-support-for-disa-purebred-on-android-devices--4839592---"></a>Ondersteuning voor afgeleide referenties voor DISA Purebred op Android-apparaten<!--4839592 -->
U kunt *DISA Purebred* gebruiken als provider van [afgeleide referenties](../protect/derived-credentials.md) in volledig beheerde Android Enterprise-apparaten (**Tenantbeheer** > **Connectors en tokens** > **Afgeleide referenties**). Er wordt ondersteuning opgenomen voor het ophalen van een afgeleide referentie voor DISA Purebred. U kunt een afgeleide referentie gebruiken voor appverificatie, Wi-Fi, VPN of voor S/MIME-ondertekening en/of versleuteling voor apps die dit ondersteunen. 

In april is in Intune ondersteuning toegevoegd voor *Entrust Datacard* en *Intercede* als providers van afgeleide referenties. 

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Voorkeursinstellingen voor privacy voor macOS-apparaten<!-- 2934232 --> 
Bij de release van macOS Catalina 10.15 zijn nieuwe beveiligings- en privacyverbeteringen toegevoegd. Standaard kunnen toepassingen en processen zonder toestemming van de gebruiker geen toegang krijgen tot specifieke gegevens. Als gebruikers geen toestemming geven, werken de toepassingen en processen mogelijk niet. Intune voegt ondersteuning toe voor instellingen waarmee IT-beheerders toestemming voor toegang tot gegevens namens eindgebruikers kunnen toestaan of weigeren op apparaten waarop macOS 10.14 of hoger wordt uitgevoerd. Door deze instellingen blijven toepassingen en processen goed werken en krijgen eindgebruikers minder vaak prompts te zien.


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Uw beleid dupliceren in Eindpuntbeveiliging<!-- 5892558   -->
U kunt een beleid selecteren dat u hebt gemaakt in het knooppunt Eindpuntbeveiliging van het Microsoft Endpoint Manager-beheercentrum en dit vervolgens dupliceren om een kopie te maken.  De beleidsregels die u kunt dupliceren, zijn onder andere de regels die u maakt voor: 

- Antivirus
- Schijfversleuteling
- Firewall
- Eindpuntdetectie en -respons
- Kwetsbaarheid voor aanvallen verminderen
- Accountbeveiliging

Met duplicatie maakt u een kopie van het oorspronkelijke beleid. U kunt dit vervolgens een andere naam geven en bewerken. De kopie bevat geen toewijzingen van het origineel.

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Pushmeldingen verzenden als actie voor niet-naleving <!-- 1733150   -->
Voor iOS- en Android-platformen wordt een nieuwe actie voor niet-naleving toegevoegd waarmee een app-pushmelding wordt verzonden via de bedrijfsportal-app. Gebruikers kunnen op de meldingen klikken, waarna de bedrijfsportal-app wordt gestart waarin de reden voor de niet-naleving wordt weergegeven. Beheerders kunnen deze nieuwe actie voor niet-naleving configureren in het Microsoft Endpoint Manager-beheercentrum door naar **Apparaten** > **Nalevingsbeleid** > **Beleid maken** te gaan en vervolgens de *actie* te selecteren om een app-pushmelding te verzenden. 

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Nieuw profiel voor firewallbeleid van Eindpuntbeveiliging<!-- 5653324   -->
Als voorbeeld voegen we een extra profiel voor Windows 10 en hoger toe aan het firewallbeleid in Eindpuntbeveiliging van Intune (**Eindpuntbeveiliging** > **Firewall** > **Beleid maken** > **Windows 10 en hoger** selecteren). 

Elk exemplaar van dit nieuwe profiel ondersteunt maximaal 150 aangepaste *Microsoft Defender Firewall-regels*. Met het profiel van de Microsoft Defender Firewall-regels kunt u gedetailleerde Windows Firewall-regels definiëren om poorten en toepassingen in Windows 10 toe te staan of te blokkeren.

<!-- ***********************************************-->
## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Zie tevens

Voor meer informatie over recente ontwikkelingen raadpleegt u [Wat is er nieuw in Microsoft Intune?](whats-new.md).



