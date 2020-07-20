---
title: Nieuwe functies in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Ontdekken wat er nieuw is in Intune Azure Portal
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/10/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: c9e65171c0eb723f338e87cdf1f7a99601c0833f
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240727"
---
# <a name="whats-new-in-microsoft-intune"></a>Wat is er nieuw in Microsoft Intune?

Ontdek elke week wat er nieuw is in Microsoft Intune in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431). U vindt hier ook [belangrijke kennisgevingen](#notices), [oudere releases](whats-new-archive.md) en informatie over [hoe service-updates voor Intune worden uitgebracht](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> Het kan voor elke [maandelijkse update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) tot drie dagen duren totdat deze wordt geïmplementeerd. Dit gebeurt in de volgende volgorde:
>
> - Dag 1: Azië en Stille Oceaan (APAC)
> - Dag 2: Europa, Midden-Oosten en Afrika (EMEA)
> - Dag 3: Noord-Amerika
> - Dag 4+: Intune for Government
>
> Sommige functies worden gedurende een aantal weken geïmplementeerd en zijn mogelijk niet voor alle gebruikers in de eerste week beschikbaar.
>
> Controleer de [pagina In ontwikkeling](in-development.md) voor een lijst met nieuwe functies in een versie.

**RSS-feed**: ontvang een melding wanneer deze pagina wordt bijgewerkt door de volgende URL in uw feedlezer te kopiëren en plakken: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Scripts


<!-- ########################## -->


## <a name="week-of-july-06-2020"></a>Week van 6 juli 2020

### <a name="device-enrollment"></a>Apparaatinschrijving

#### <a name="ios-company-portal-will-support-apples-automated-device-enrollment-without-user-affinity---7282707---"></a>iOS-bedrijfsportal biedt ondersteuning voor Automatische apparaatinschrijving van Apple zonder gebruikersaffiniteit<!-- 7282707 --> 
De iOS-bedrijfsportal wordt ondersteund op apparaten die zijn ingeschreven met behulp van Automatische apparaatinschrijving van Apple zonder dat een toegewezen gebruiker is vereist. Een eindgebruiker kan zich aanmelden bij de iOS-bedrijfsportal om zichzelf de primaire gebruiker te maken op een iOS-/iPadOS-apparaat dat is ingeschreven zonder apparaataffiniteit. Zie [iOS/iPadOS-apparaten automatisch inschrijven met automatische apparaatinschrijving van Apple](../enrollment/device-enrollment-program-enroll-ios.md) voor meer informatie over automatische apparaatinschrijving.

### <a name="app-management"></a>Appbeheer

#### <a name="update-to-device-icons-in-company-portal-and-intune-apps-on-android---6057023---"></a>Updates voor apparaatpictogrammen in de bedrijfsportal- en Intune-apps op Android<!-- 6057023 -->
We hebben de apparaatpictogrammen in de bedrijfsportal- en Intune-apps op Android-apparaten bijgewerkt, om een moderner uiterlijk te creëren en beter af te stemmen op het Microsoft Fluent Design-systeem. Raadpleeg [Updates voor pictogrammen in de bedrijfsportal-app voor iOS/iPadOS en macOS](../fundamentals/whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-) voor verwante informatie. 

### <a name="device-management"></a>Apparaatbeheer

#### <a name="tenant-attach-configmgr-client-details-in-the-admin-center-preview---7552762---"></a>Tenantkoppeling: Details van ConfigMgr-client in het beheercentrum (preview)<!-- 7552762 -->

U kunt nu ConfigMgr-clientgegevens weergeven, inclusief verzamelingen, lidmaatschap van grensgroepen en real-time clientinformatie voor een specifiek apparaat in het Microsoft Endpoint Manager-beheercentrum. Zie voor meer informatie [Tenant koppelen: details van ConfigMgr-client in het beheercentrum (preview)](../../configmgr/tenant-attach/client-details.md).

## <a name="week-of-june-22-2020"></a>Week van 22 juni 2020
### <a name="app-management"></a>Appbeheer

#### <a name="newly-available-protected-apps-for-intune---7248952---"></a>Nieuw beschikbare, beveiligde apps voor Intune<!-- 7248952 -->
De volgende beveiligde apps zijn nu beschikbaar:
- BlueJeans-videovergaderingen
- Cisco Jabber voor Intune
- Tableau Mobile voor Intune
- ZERO voor Intune

Zie [Met Microsoft Intune beveiligde apps](../apps/apps-supported-intune-apps.md) voor meer informatie over beveiligde apps.

### <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

#### <a name="use-endpoint-analytics-to-improve-user-productivity-and-reduce-it-support-costs---5653063---"></a>Eindpuntanalyse gebruiken om gebruikersproductiviteit te verbeteren en ondersteuningskosten voor IT te verlagen<!-- 5653063 --> 
Deze functie wordt de komende week geïmplementeerd. Eindpuntanalyse heeft als doel het verbeteren van de productiviteit van gebruikers en het verlagen van de kosten voor IT-ondersteuning, door inzicht te bieden in de gebruikerservaring. De inzichten stellen de IT-afdeling in staat om de eindgebruikerservaring te optimaliseren met proactieve ondersteuning, en om regressies in de gebruikerservaring te detecteren door de impact van configuratiewijzigingen voor de gebruiker te evalueren. Zie [Preview-versie van Eindpuntanalyse](https://aka.ms/uea) voor meer informatie.

#### <a name="proactively-remediate-end-user-device-issues-using-script-packages---5933328---"></a>Problemen met het apparaat van eindgebruikers proactief herstellen met behulp van scriptpakketten<!-- 5933328 -->
U kunt scriptpakketten maken en uitvoeren op apparaten van eindgebruikers om de belangrijkste ondersteuningsproblemen in uw organisatie proactief te vinden en op te lossen. Door scriptpakketten te implementeren, kunt u de ondersteuningsaanvragen verminderen. Kies ervoor om uw eigen scriptpakketten te maken of een van de scriptpakketten te implementeren die we in onze omgeving hebben geschreven en gebruikt om het aantal ondersteuningstickets te verminderen. Met Intune kunt u de status van uw geïmplementeerde scriptpakketten bekijken en de detectie- en herstelresultaten controleren. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) **Rapporten** > **Eindpuntanalyse** > **Proactieve herstelbewerkingen**. Zie [Proactieve herstelbewerkingen](https://aka.ms/uea_prs) voor meer informatie.

### <a name="device-security"></a>Apparaatbeveiliging

#### <a name="use-microsoft-defender-atp-in-compliance-policies-for-android---4425686----"></a>Microsoft Defender ATP gebruiken in nalevingsbeleid voor Android<!-- 4425686  -->

U kunt nu Intune gebruiken om [Android-apparaten in Microsoft Defender Advanced Threat Protection te onboarden](../protect/advanced-threat-protection.md#onboard-android-devices) (MicrosoftDefender ATP). Nadat de onboarding van uw ingeschreven apparaten is voltooid, kan uw nalevingsbeleid voor Android de *bedreigingsniveausignalen* van Microsoft Defender ATP gebruiken. Dit zijn dezelfde signalen die u eerder kon gebruiken voor Windows 10-apparaten.

#### <a name="configure-defender-atp-web-protection-for-android-devices---6185563-wnready---"></a>Defender ATP-webbeveiliging configureren voor Android-apparaten<!-- 6185563 WNReady -->

Wanneer u Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) gebruikt voor Android-apparaten, kunt u [ Microsoft Defender ATP-webbeveiliging](../protect/advanced-threat-protection.md#configure-web-protection-on-devices-that-run-android) configureren om de scanfunctie voor phishing uit te schakelen of te voorkomen dat de VPN door de scan wordt gebruikt.

Afhankelijk van hoe uw Android-apparaat wordt ingeschreven met Intune, zijn de volgende opties beschikbaar:

- Android-apparaatbeheerder: gebruik aangepaste OMA-URI-instellingen om de webbeveiligingsfunctie uit te schakelen of schakel alleen het gebruik van VPN's uit tijdens de scans.
- Android Enterprise-werkprofiel: gebruik een app-configuratieprofiel en de configuratieontwerper om alle webbeveiligingsmogelijkheden uit te schakelen.

## <a name="week-of-june-15-2020--2006-service-release"></a>Week van 15 juni 2020 (servicerelease van 2006)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer  

#### <a name="telecommunications-data-transfer-protection-for-managed-apps---6884491----"></a>Beveiliging van de gegevensoverdracht in telecommunicatie voor beheerde apps<!-- 6884491  -->
Wanneer een telefoonnummerkoppeling wordt gedetecteerd in een beveiligde app, controleert Intune of er een beveiligingsbeleid is toegepast waarmee het nummer kan worden overgedragen naar een kiezer-app. U kunt kiezen hoe u dit type inhoudsoverdracht wilt afhandelen wanneer deze wordt gestart vanuit een door een beleid beheerde app. Bij het maken van een app-beveiligingsbeleid in Microsoft Endpoint Manager, selecteert u een beheerde app-optie uit **Organisatiegegevens naar andere apps verzenden** en selecteert u een optie uit **Telecommunicatiegegevens overdragen naar**. Zie [Instellingen voor beveiligingsbeleid voor apps voor Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md) en [Instellingen voor beveiligingsbeleid voor apps in iOS](../apps/app-protection-policy-settings-ios.md) voor meer informatie over deze instelling voor gegevensbeveiliging. 

#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---7414033----"></a>Collectieve levering van Azure AD Enterprise- en Office Online-apps in de bedrijfsportal<!-- 7414033  -->
In het deelvenster **Aanpassing** van Intune kunt u in de Bedrijfsportal zowel van **toepassingen van Microsoft Azure AD** als van **toepassingen van Office Online** selecteren dat u deze wilt **Verbergen** of **Weergeven**. Elke eindgebruiker ziet de volledige toepassingscatalogus van de gekozen Microsoft-service. Standaard wordt elke extra app-bron ingesteld op **Verbergen**. Deze functie gaat van kracht op de Bedrijfsportal-website. Ondersteuning in de Windows-bedrijfsportal zal naar verwachting volgen. U vindt deze configuratie-instelling door in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) **Tenantbeheer** > **Aanpassing** te selecteren. Zie [De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen](../apps/company-portal-app.md) voor informatie.

#### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Verbeteringen in de Bedrijfsportal voor de registratie van macOS<!-- 6444452  -->
De bedrijfsportal voor macOS-registratie heeft een eenvoudiger registratieproces dat nauwkeuriger is afgestemd met de bedrijfsportal voor iOS-registratie. Gebruikers van het apparaat zien het volgende:  
- Een gestroomlijndere gebruikers interface.  
- Een verbeterde controlelijst voor registratie.  
- Duidelijkere instructies over het registreren van apparaten.  
- Verbeterde opties voor probleemoplossing.  

Zie [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md) (De Intune-bedrijfsportal-apps, Bedrijfsportal-website en Intune-app aanpassen) voor meer informatie over de Bedrijfsportal.

#### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001---"></a>Verbeteringen op de pagina Apparaten van Bedrijfsportal voor iOS/iPadOS en macOS<!-- 6055001 -->
Er zijn wijzigingen aangebracht op de pagina Bedrijfsportal **Apparaten** om de app-ervaring voor iOS/iPadOS- en Mac-gebruikers te verbeteren. Naast het creëren van een moderner uiterlijk, zijn de details van het apparaat gereorganiseerd onder een enkele kolom met gedefinieerde sectiekoppen, zodat het makkelijker is voor gebruikers om hun apparaatstatus te zien. Ook zijn duidelijkere berichten en stappen voor probleemoplossing toegevoegd voor gebruikers van wie de apparaten niet meer compatibel zijn. Zie [De Intune-bedrijfsportal-apps, Bedrijfsportal-website en Intune-app aanpassen](../apps/company-portal-app.md) voor meer informatie over Bedrijfsportal. Zie [Uw iOS-apparaat handmatig synchroniseren](../user-help/sync-your-device-manually-ios.md) voor meer informatie over het handmatig synchroniseren van een apparaat.  

#### <a name="cloud-setting-for-iosipados-company-portal-app---7071303----"></a>Cloudinstelling voor iOS/iPadOS Bedrijfsportal-app<!-- 7071303  -->
Een nieuwe **cloud**instelling voor de iOS/iPadOS Bedrijfsportal stelt gebruikers in staat hun verificatie om te leiden naar de juiste cloud voor uw organisatie. De instelling is standaard geconfigureerd op **Automatisch**, waardoor de verificatie naar de cloud automatisch wordt gedetecteerd door het apparaat van de gebruiker. Als de verificatie voor uw organisatie moet worden omgeleid naar een andere cloud dan de cloud die automatisch wordt gedetecteerd (zoals Openbaar of Overheid), kunnen uw gebruikers handmatig de juiste cloud selecteren door **Instellingen-app** > **Bedrijfsportal** > **Cloud** te selecteren. Uw gebruikers moeten de **cloudinstelling** **Automatisch** alleen wijzigen als ze zich vanaf een ander apparaat aanmelden en de betreffende cloud niet automatisch door hun apparaat wordt gedetecteerd. 

#### <a name="duplicate-apple-vpp-tokens---7101606----"></a>Dubbele Apple VPP-tokens<!-- 7101606  -->
Apple VPP-tokens met dezelfde **tokenlocatie** zijn nu gemarkeerd als **dubbel** en kunnen opnieuw worden gesynchroniseerd wanneer de dubbele token is verwijderd. U kunt nog steeds licenties toewijzen en intrekken voor tokens die als dubbel zijn gemarkeerd. Licenties voor nieuwe apps en boeken die zijn aangeschaft, worden mogelijk niet weergegeven wanneer een token is gemarkeerd als zijnde dubbel. Als u Apple VPP-tokens voor uw tenant wilt zoeken, selecteert u [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431), **Tenantbeheer** > **Connectors en tokens** > **Apple VPP-tokens**. Zie [iOS- en macOS-apps beheren die zijn aangeschaft via een Apple Volume Purchase Program met Microsoft Intune](../apps/vpp-apps-ios.md) voor meer informatie over VPP-tokens.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="add-multiple-root-certificates-for-eap-tls-authentication-in-wi-fi-profiles-on-macos-devices---2077871----"></a>Meerdere basiscertificaten voor EAP-TLS-verificatie toevoegen in Wi-Fi-profielen op macOS-apparaten<!-- 2077871  -->

Op macOS-apparaten kunt u een Wi-Fi-profiel maken en het verificatietype voor Extensible Authentication Protocol (EAP) selecteren (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **macOS** voor platform > **Wi-Fi** voor profiel > **Wi-Fi-type** ingesteld op Enterprise).

Wanneer u het **EAP-type** instelt op **EAP-TLS-** , **EAP-TTLS-** of **PEAP-** verificatie, kunt u meerdere basiscertificaten toevoegen. Voorheen kon u slechts één basiscertificaat toevoegen.

Zie [Wi-Fi-instellingen voor macOS-apparaten in Microsoft Intune toevoegen](../configuration/wi-fi-settings-macos.md) voor meer informatie over de instellingen die u kunt configureren.

Van toepassing op:
- macOS

#### <a name="use-pkcs-certificates-with-wi-fi-profiles-on-windows-10-and-newer-devices---3246388-----"></a>PKCS-certificaten met Wi-Fi-profielen gebruiken op Windows 10- en nieuwere apparaten<!-- 3246388   -->
U kunt Windows Wi-Fi-profielen met SCEP-certificaten verifiëren (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **Windows 10 en hoger** voor platform > **Wi-Fi** voor profieltype > **Enterprise** > **EAP-type**). U kunt nu PKCS-certificaten gebruiken met uw Windows Wi-Fi-profielen. Met deze functie kunnen gebruikers Wi-Fi-profielen verifiëren met behulp van nieuwe of bestaande PKCS-certificaatprofielen in uw tenant. 

Zie [Wi-Fi-instellingen toevoegen voor apparaten met Windows 10 en hoger in Intune](../configuration/wi-fi-settings-windows.md) voor meer informatie over de Wi-Fi-instellingen die u kunt configureren.

Van toepassing op:
- Windows 10 en nieuwer

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Configuratieprofielen voor een bekabeld netwerkapparaat voor macOS-apparaten<!-- 3508686  -->
Er is een nieuw configuratieprofiel voor macOS-apparaten beschikbaar waarmee bedrade netwerken kunnen worden geconfigureerd (**Apparaten** > **Configuratieprofielen > **Profiel maken** > **macOS** voor platform > **Bekabeld netwerk** voor profiel). Gebruik deze functie om 802.1x-profielen te maken om bekabelde netwerken te beheren en om deze bekabelde netwerken te implementeren op uw macOS-apparaten.

Zie [Bekabelde netwerken op macOS-apparaten](../configuration/wired-networks-configure.md)voor meer informatie over deze functie.

Van toepassing op:
- macOS

#### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976-----"></a>Microsoft Launcher gebruiken als het standaard startprogramma voor volledig beheerde Android Enterprise-apparaten<!-- 4927976   -->
Op Android Enterprise-apparaten met apparaateigenaar kunt u Microsoft Launcher instellen als het standaard startprogramma voor volledig beheerde apparaten (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** als platform > **Apparaateigenaar** > **Apparaatbeperkingen** als profiel > **Apparaatervaring**). Als u alle andere instellingen van Microsoft Launcher wilt configureren, gebruikt u het [configuratiebeleid voor apps.](../apps/configure-microsoft-launcher.md) 

Er zijn ook enkele andere UI-updates, zoals dat **Toegewezen apparaten** nu **Apparaatervaring** heet.

Zie[Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md) (Met Android Enterprise-apparaatinstellingen functies toestaan of beperken met behulp van Intune) als u alle instellingen die u kunt beperken wilt bekijken. 

Van toepassing op:
- Volledig beheerde apparaten van Android Enterprise-apparaateigenaar (COBO)

#### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-app-to-be-a-sign-insign-out-app---7055619-----"></a>Gebruik de instellingen voor Autonome modus voor één app om de iOS-bedrijfsportal-app te configureren als een app voor aanmelden/afmelden<!-- 7055619   -->
Op iOS/iPadOS-apparaten kunt u apps configureren om in de autonome modus voor één app te worden uitgevoerd (ASAM). De Bedrijfsportal-app ondersteunt nu ASAM en kan worden geconfigureerd als een app voor aanmelden/afmelden. Wanneer gebruikers zich in deze modus aanmelden bij de Bedrijfsportal-app, kunnen ze andere apps en de knop Startscherm op het apparaat gebruiken. Wanneer gebruikers zich afmelden bij de Bedrijfsportal-app, keert het apparaat terug naar de modus voor één app en wordt de Bedrijfsportal-app vergrendeld.

Als u de Bedrijfsportal in ASAM wilt configureren, gaat u naar **Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatbeperkingen** voor profiel > **Autonome modus voor één app**.

Zie [Autonome modus voor één app (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) en [modus voor één app](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (opent website van Apple).

Van toepassing op:
- iOS/iPadOS

#### <a name="configure-content-caching-on-macos-devices---7106872-----"></a>Cacheopslag van inhoud op macOS-apparaten configureren<!-- 7106872   -->
Op macOS-apparaten kunt u een configuratieprofiel maken waarmee de cacheopslag van inhoud wordt geconfigureerd (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **macOS** als platform > **Apparaatfuncties** als profiel). Gebruik deze instellingen voor het verwijderen van de cache, het toestaan van een gedeelde cache, het instellen van een cachelimiet op de schijf en meer.

Zie [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (opent de website van Apple) voor meer informatie over cacheopslag van inhoud.

Ga naar [Instellingen van macOS-apparaatfuncties in Intune](../configuration/macos-device-features-settings.md) om te zien welke instellingen u kunt configureren.

Van toepassing op:
- macOS

#### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386-----"></a>Nieuwe schema-instellingen toevoegen en zoeken naar bestaande schema-instellingen met behulp van OEMConfig in Android Enterprise<!-- 6394386   -->
U kunt OEMConfig in Intune gebruiken om instellingen op Android Enterprise-apparaten te beheren (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** als platform > **OEMConfig** als profiel). Wanneer u de **Configuration Designer** gebruikt, worden de eigenschappen in het app-schema weergegeven. In de **Configuration Designer** kunt u nu het volgende doen:

- Nieuwe instellingen toevoegen aan het app-schema.
- Naar nieuwe en bestaande instellingen zoeken in het app-schema.

Zie [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md) (Android Enterprise-apparaten gebruiken en beheren met OEMConfig in Microsoft Intune) voor meer informatie over OEMConfig-profielen in Intune.

Van toepassing op:
- Android Enterprise

#### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794----"></a>Tijdelijke sessies blokkeren op gedeelde iPad-apparaten<!-- 6613794  -->
Intune heef een nieuwe instelling, **Tijdelijke sessies blokkeren op gedeelde iPad-apparaten**, die tijdelijke sessies blokkeert op gedeelde iPad-apparaten (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** als platform > **Apparaatbeperkingen** als profieltype > **Gedeelde iPad**). Wanneer deze functie is ingeschakeld, kunnen eindgebruikers het gastaccount niet gebruiken. Ze moeten zich aanmelden bij het apparaat met hun beheerde Apple-id en wachtwoord. 

Zie [iOS- en iPadOS-apparaatinstellingen om functies toe te staan of te beperken](../configuration/device-restrictions-ios.md) voor meer informatie.

Van toepassing op:
- Gedeelde iPad-apparaten met iOS/iPadOS 13.4 of hoger

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Apparaatinschrijving

#### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344----"></a>Eigen apparaten kunnen voor het implementeren gebruikmaken van VPN<!--5015344  -->
Met de nieuwe wisselknop **Domeinconnectiviteitscontrole overslaan** voor het Autopilot-profiel kunt u Hybrid Azure AD Join-apparaten implementeren zonder toegang tot uw bedrijfsnetwerk door middel van uw eigen Win32 VPN-client van derden. Als u de nieuwe wisselknop wilt zien, gaat u naar het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten**  > **Windows** > **Windows-inschrijving** > **Implementatieprofielen** > **Profiel maken** > **OOBE (Out-of-Box Experience)** .

#### <a name="enrollment-status-page-profiles-can-be-set-to-device-groups--3952138---"></a>Profielen voor inschrijvingsstatuspagina kunnen worden ingesteld op apparaatgroepen<!--3952138 -->
Voorheen konden profielen voor inschrijvingsstatuspagina (ESP) alleen worden gericht op gebruikersgroepen. Nu kunt u ze ook instellen op doelapparaatgroepen. Zie [Een inschrijvingsstatuspagina instellen](../enrollment/windows-enrollment-status.md) voor meer informatie.

#### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Synchronisatiefouten bij Automatische apparaatinschrijving<!-- 6988214 -->
Er worden nieuwe fouten gerapporteerd voor iOS/iPadOS- en macOS-apparaten, waaronder:
- Het telefoonnummer bevat ongeldige tekens of dat veld is leeg. 
- De configuratienaam voor het profiel is ongeldig of leeg. 
- Ongeldige/verlopen cursorwaarde of er is geen cursor gevonden.
- Afgewezen of verlopen token. 
- Het veld Afdeling is leeg of de lengte is te lang. 
- Het profiel is niet gevonden door Apple en er moet een nieuwe worden gemaakt. 
- Er wordt een telling van verwijderde Apple Business Manager-apparaten toegevoegd aan de overzichtspagina, waar u de status van uw apparaten kunt bekijken.

#### <a name="shared-ipads-for-business--6367326-----"></a>Gedeelde iPads voor bedrijven<!--6367326   -->
U kunt Intune en Apple Business Manager gebruiken om snel en veilig Gedeelde iPad in te stellen, zodat meerdere werknemers apparaten kunnen delen. [Gedeelde iPad](https://developer.apple.com/education/shared-ipad/) van Apple biedt een persoonlijke ervaring voor meerdere gebruikers terwijl gebruikersgegevens behouden blijven. Wanneer gebruikers een beheerde Apple ID gebruiken, hebben ze toegang tot hun apps, gegevens en instellingen nadat ze zich hebben aangemeld bij een gedeelde iPad in hun organisatie. Gedeelde iPad werkt met federatieve identiteiten.

Ga naar [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **iOS** > **iOS-inschrijving** > **Registratieprogrammatokens** > kies een token** > **Profielen** > **Profiel maken** > **iOS** om deze functie te zien. Selecteer op de pagina **Beheerinstellingen** de optie **Inschrijven zonder gebruikersaffiniteit** en u ziet de optie **Gedeelde iPad**.

Vereist: iPadOS 13.4 en hoger. In deze release is ondersteuning toegevoegd voor tijdelijke sessies met Gedeelde iPad zodat gebruikers zonder een beheerde Apple ID toegang hebben tot een apparaat. Na afmelding worden alle gebruikersgegevens gewist zodat het apparaat direct gereed is voor gebruik. Het apparaat hoeft hierdoor niet meer te worden gewist. 

#### <a name="updated-user-interface-for-apples-automated-device-enrollment--7430322---"></a>De gebruikersinterface voor de automatische apparaatinschrijving van Apple is bijgewerkt<!--7430322 -->
De gebruikersinterface is bijgewerkt om het Device Enrollment Program van Apple te vervangen door automatische apparaatinschrijving om de Apple-terminologie weer te geven.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="device-remote-lock-pin-available-for-macos--7281557-----"></a>Pincodes voor vergrendelen van apparaten op afstand beschikbaar voor macOS<!--7281557   -->
De beschikbaarheid van de pincodes voor vergrendelen op afstand voor macOS-apparaten wordt verhoogd van 7 naar 30 dagen.

#### <a name="change-primary-user-on-co-managed-devices--7319183----"></a>Primaire gebruiker wijzigen op co-beheerde apparaten<!--7319183  -->
U kunt de primaire gebruiker van een apparaat wijzigen voor co-beheerde Windows-apparaten. Zie [Find the primary user of an Intune device](../remote-actions/find-primary-user.md) (De hoofdgebruiker van een Intune-apparaat zoeken) voor meer informatie over het zoeken en wijzigen van een gebruiker. Deze functie wordt geleidelijk in de komende weken geïmplementeerd.

#### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Als u de primaire gebruiker van Intune instelt, wordt ook de eigenschap Azure AD-eigenaar ingesteld<!--7319227 -->
Met deze nieuwe functie wordt de eigenschap Eigenaar automatisch ingesteld op de nieuw ingeschreven hybride Azure AD-gekoppelde apparaten als de primaire gebruiker van Intune wordt ingesteld. Zie [Find the primary user of an Intune device](../remote-actions/find-primary-user.md) (De hoofdgebruiker van een Intune-apparaat zoeken) voor meer informatie over de primaire gebruiker.

Dit is een wijziging in het inschrijvingsproces en is alleen van toepassing op nieuw ingeschreven apparaten. Voor bestaande hybride Azure AD-gekoppelde apparaten moet u de eigenschap Azure AD-eigenaar handmatig bijwerken. Hiervoor kunt u de functie [Primaire gebruiker wijzigen](../remote-actions/find-primary-user.md#change-a-devices-primary-user) of [een script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices) gebruiken.

Wanneer Windows 10-apparaten hybride Azure Directory-gekoppeld worden, wordt de eerste gebruiker van het apparaat de primaire gebruiker in Endpoint Manager.  Momenteel wordt de gebruiker niet ingesteld op het bijbehorende Azure AD-apparaatobject. Dit leidt tot een inconsistentie bij het vergelijken van de eigenschap *Eigenaar* van Azure AD-portal met de eigenschap *Primaire gebruiker* in het Microsoft Endpoint Manager-beheercentrum. De eigenschap Eigenaar van Azure AD wordt gebruikt voor het beveiligen van de toegang tot BitLocker-herstelsleutels. De eigenschap wordt niet ingevuld op hybride Azure AD-gekoppelde apparaten. Deze beperking voorkomt dat self-service van BitLocker-herstel vanuit Azure AD wordt ingesteld. Deze nieuwe functie lost deze beperking op.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Apparaatbeveiliging

#### <a name="hide-the-recovery-key-from-users-during-filevault-2-encryption-for-macos-devices---5459801----"></a>De herstelsleutel van gebruikers verbergen tijdens FileVault 2-versleuteling voor macOS-apparaten<!-- 5459801  -->
Een nieuwe instelling is toegevoegd aan de *FileVault*-categorie op de sjabloon [macOS-eindpuntbeveiliging](../protect/endpoint-protection-macos.md#filevault): **Herstelsleutel verbergen**. Door deze instelling wordt de persoonlijke sleutel tijdens de FileVault 2-versleuteling voor de eindgebruiker verborgen. 

Als u de persoonlijke herstelsleutel van een versleuteld macOS-apparaat wilt weergeven, gaat u als gebruiker van het apparaat naar een van de volgende locaties en klikt u op *Herstelsleutel ophalen* voor het macOS-apparaat: 

- De Bedrijfsportal-app voor iOS/iPadOS
- De Intune-app
- De bedrijfsportal-website
- De Bedrijfsportal-app voor Android

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android-fully-managed--5896415-----"></a>Ondersteuning voor S/MIME-ondertekening en versleutelingscertificaten met Outlook op volledig beheerde Android-apparaten<!--5896415   -->
U kunt nu certificaten voor S/MIME-ondertekening en -versleuteling gebruiken met Outlook op volledig beheerde Android-apparaten.

Hiermee wordt de ondersteuning uitgebreid die vorige maand is toegevoegd voor andere Android-versies (ondersteuning voor S/MIME-ondertekenings- en versleutelingscertificaten met Outlook op Android). U kunt deze certificaten inrichten door gebruik te maken van geïmporteerde certificaatprofielen SCEP en PKCS.

Zie [Vertrouwelijkheidslabels en -bescherming in Outlook voor iOS en Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) in de documentatie van Exchange voor meer informatie over deze ondersteuning.

#### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Een link naar de ondersteuningswebsite van uw bedrijf portal toevoegen aan e-mailberichten voor niet-naleving<!-- 7225498    -->
Wanneer u [een sjabloon voor een meldingsbericht configureert](../protect/actions-for-noncompliance.md#create-a-notification-message-template) voor het verzenden van e-mailmeldingen wegens niet-naleving, gebruikt u de nieuwe instelling **Koppeling naar Bedrijfsportalwebsite** om automatisch een koppeling naar uw Bedrijfsportalwebsite op te nemen. Met deze optie ingesteld op *Inschakelen*, kunnen gebruikers met niet-conforme apparaten die e-mail ontvangen op basis van deze sjabloon de koppeling gebruiken om naar een website te gaan voor meer informatie over de reden waarom hun apparaat niet-conform is. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="licensing"></a>Licentieverlening

#### <a name="admins-no-longer-require-an-intune-license-to-access-microsoft-endpoint-manager-admin-console--1335430---"></a>Beheerders hebben geen Intune-licentie meer nodig om toegang te krijgen tot de Microsoft Endpoint Manager-beheerconsole<!--1335430 -->
U kunt nu een tenantbrede wisselknop instellen die de Intune-licentievereiste voor beheerders verwijdert om toegang te krijgen tot de MEM-beheerconsole en API's van de query-grafiek. Nadat u de licentievereiste hebt verwijderd, kunt u deze nooit meer herstellen. 



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripts"></a>Scripts 

#### <a name="availability-of-shell-scripts-on-macos-devices---7134839----"></a>Beschikbaarheid van Shell-scripts op macOS-apparaten<!-- 7134839  -->
Shell-scripts voor macOS-apparaten zijn nu beschikbaar voor klanten in de cloudomgeving voor de overheid en China. Zie [Shell-scripts op macOS-apparaten gebruiken in Intune](../apps/macos-shell-scripts.md) voor meer informatie over Shell-scripts.



<!-- ########################## -->
## <a name="week-of-june-8-2020"></a>Week van 8 juni 2020   

### <a name="app-management"></a>Appbeheer  

#### <a name="updates-to-informational-screen-in-company-portal-for-iosipados---7032452---"></a>Updates voor het informatiescherm in Bedrijfsportal voor iOS/iPadOS <!--7032452 -->
Een informatief scherm is in Bedrijfsportal voor iOS/iPadOS bijgewerkt om beter te kunnen uitleggen wat een beheerder op apparaten kan zien en doen. Deze uitleg gaat alleen over apparaten in bedrijfseigendom. Alleen de tekst is bijgewerkt, er zijn geen wijzigingen aangebracht in wat de beheerder op gebruikersapparaten kan zien of doen. Als u de bijgewerkte vensters wilt zien, gaat u naar [UI-updates voor eindgebruikers-apps voor Intune](./whats-new-app-ui.md).

#### <a name="updated-android-app-conditional-launch-end-user-experience---5736084---"></a>Ervaring voor eindgebruiker van Android APP Voorwaardelijk starten is bijgewerkt<!-- 5736084 -->
In de 2006-versie van de Android-bedrijfsportal zijn wijzigingen ingevoerd die zijn gebaseerd op de updates van de 2005-versie. In 2005 hebben we een update uitgerold waarbij eindgebruikers van Android-apparaten die een waarschuwing krijgen, worden geblokkeerd of gewist door een app-beveiligingsbeleid, een bericht op een volledige pagina zien waarin de reden voor de waarschuwing, blokkering of het wissen en een oplossing voor het probleem worden beschreven. In 2006 zullen nieuwe gebruikers van Android-apps waaraan een app-beveiligingsbeleid is toegewezen door middel van een begeleide stroom worden geholpen om problemen op te lossen die de toegang tot hun app blokkeren. 

<!-- ########################## -->
## <a name="week-of-may-25-2020"></a>Week van 25 mei 2020

### <a name="app-management"></a>Appbeheer

#### <a name="windows-32-bit-x86-apps-on-arm64-devices---5477661---"></a>32-bits Windows-apps (x86) op ARM64-apparaten<!-- 5477661 -->
32-bits Windows-apps (x86) die zijn geïmplementeerd als beschikbaar voor ARM64-apparaten worden nu weergegeven in de bedrijfsportal. Zie [Intune Win32 app-beheer](../apps/apps-win32-app-management.md) voor meer informatie over 32-bits Windows-apps.

#### <a name="windows-company-portal-app-icon---7114635---"></a>Pictogram voor Windows-bedrijfsportal-app<!-- 7114635 -->
Het pictogram voor de Windows-bedrijfsportal-app is bijgewerkt. Zie [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md) (De Intune-bedrijfsportal-apps, Bedrijfsportal-website en Intune-app aanpassen) voor meer informatie over de Bedrijfsportal.


<!-- ########################## -->
## <a name="week-of-may-18-2020"></a>Week van 18 mei 2020

### <a name="app-management"></a>Appbeheer  

#### <a name="update-to-icons-in-company-portal-app-for-iosipados-and-macos--6057697---"></a>Bijgewerkte pictogrammen in de Bedrijfsportal-app voor iOS/iPadOS en macOS<!--6057697 -->
We hebben de pictogrammen in Bedrijfsportal bijgewerkt voor een moderner uiterlijk dat wordt ondersteund op apparaten met twee schermen en is afgestemd op het Microsoft Fluent Design-systeem. Als u de bijgewerkte pictogrammen wilt zien, gaat u naar [UI-updates voor Intune-apps voor eindgebruikers](./whats-new-app-ui.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Apparaatbeveiliging

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Eindpuntdetectie en antwoordbeleid gebruiken om apparaten te onboarden naar Defender ATP<!-- 7130165  -->

[Eindpuntbeveiligingsbeleid gebruiken voor eindpuntdetectie en -respons](../protect/endpoint-security-edr-policy.md) (EDR) om apparaten te onboarden en te configureren voor uw implementatie van Microsoft Defender Advanced Threat Protection (Defender ATP). EDR ondersteunt beleid voor Windows-apparaten die worden beheerd door Intune (MDM) en een afzonderlijk beleid voor Windows-apparaten die worden beheerd door Configuration Manager. 

Als u het beleid voor apparaten van Configuration Manager wilt gebruiken, moet u Configuration Manager [instellen voor de ondersteuning van het EDR-beleid](../protect/endpoint-security-edr-policy.md#set-up-configuration-manager-to-support-edr-policy). Instellen omvat:

- Configureer uw Configuration Manager voor *tenantkoppeling*.
- Installeer een module-update voor Configuration Manager om ondersteuning voor het EDR-beleid in te schakelen. Deze update is alleen van toepassing op hiërarchieën die *tenantkoppeling* hebben ingeschakeld.
- Synchroniseer uw apparaatverzamelingen van uw hiërarchie met het Beheercentrum voor Microsoft Endpoint Manager.


<!-- ########################## -->
## <a name="week-of-may-11-2020-2005-service-release"></a>Week van 11 mei 2020 (2005 servicerelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="customize-self-service-device-actions-in-the-company-portal--4393379---"></a>Selfservice-apparaatacties in de bedrijfsportal aanpassen<!--4393379 -->
U kunt de beschikbare self-serviceapparaatacties aanpassen die worden weergegeven aan eindgebruikers in de bedrijfsportal-app en -website. Als u onbedoelde apparaatacties wilt helpen voorkomen, kunt u deze instellingen configureren voor de bedrijfsportal-app door **Tenantbeheer** > **Aanpassing** te selecteren. Hiervoor zijn de volgende opties beschikbaar:
- Knop **Verwijderen** verbergen op zakelijke Windows-apparaten.
- Knop **Opnieuw instellen** verbergen op zakelijke Windows-apparaten.
- Knop **Opnieuw instellen** verbergen op zakelijke iOS-apparaten.
- Knop **Verwijderen** verbergen op zakelijke iOS-apparaten.
Raadpleeg [Selfservice-apparaatacties voor gebruikers van de bedrijfsportal](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal) voor meer informatie.

#### <a name="auto-update-vpp-available-apps---3640511----"></a>Beschikbare VPP-apps automatisch bijwerken<!-- 3640511  -->
Apps die zijn gepubliceerd als voor Volume Purchase Program (VPP) beschikbare apps, worden automatisch bijgewerkt wanneer **Automatische updates van apps** is ingeschakeld voor het VPP-token. Voorheen werden voor VPP beschikbare apps niet automatisch bijgewerkt. Eindgebruikers moesten in plaats daarvan naar de bedrijfsportal gaan en de app opnieuw installeren als er een nieuwere versie beschikbaar was. De vereiste apps blijven automatische updates wel ondersteunen.




#### <a name="android-company-portal-user-experience---5736084----"></a>Gebruikerservaring van de Android-bedrijfsportal<!-- 5736084  -->
In de 2005-release van de Android-bedrijfsportal zien eindgebruikers van Android-apparaten aan wie een waarschuwing, blokkering of verwijdering door een app-beveiligingsbeleid is uitgegeven, een nieuwe gebruikerservaring. In plaats van de huidige dialoogvensters zien eindgebruikers een bericht dat een volledige pagina beslaat met een beschrijving van de reden voor de waarschuwing, blokkering of verwijdering en de stappen om het probleem te verhelpen. Zie [App-beveiligingservaring voor Android-apparaten](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) en [Instellingen van app-beveiligingsbeleid voor Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md) voor meer informatie.

#### <a name="support-for-multiple-accounts-in-company-portal-for-macos---5779449----"></a>Ondersteuning voor meerdere accounts in de bedrijfsportal voor macOS<!-- 5779449  -->
Met de bedrijfsportal op macOS-apparaten worden gebruikersaccounts nu in de cache opgeslagen, waardoor het aanmelden eenvoudiger wordt. Gebruikers hoeven zich niet meer bij de bedrijfsportal aan te melden wanneer ze de toepassing starten. Daarnaast geeft de bedrijfsportal een accountkiezer weer als er meerdere gebruikersaccounts in de cache zijn opgeslagen, zodat gebruikers hun gebruikersnaam niet hoeven in te voeren. 

#### <a name="newly-available-protected-apps---7060934-----"></a>Nieuw beschikbare, beveiligde apps<!-- 7060934   -->
De volgende beveiligde apps zijn nu beschikbaar:
- Board Papers
- Breezy voor Intune
- Hearsay Relate voor Intune
- ISEC7 Mobile Exchange Delegate voor Intune
- Lexmark voor Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- ServiceNow® Onboarding - Intune
- Smartcrypt voor Intune
- Tact voor Intune
- Nul - e-mail voor advocaten

Zie [Met Microsoft Intune beveiligde apps](../apps/apps-supported-intune-apps.md) voor meer informatie over beveiligde apps.

#### <a name="search-the-intune-docs-from-the-company-portal---1736480-----"></a>De Intune-documentatie zoeken in de bedrijfsportal<!-- 1736480   -->
U kunt nu rechtstreeks vanaf de bedrijfsportal voor macOS-app zoeken in de Intune-documentatie. Selecteer in de menubalk **Help** > **Zoeken** en voer de trefwoorden van uw zoekopdracht in om snel antwoorden op uw vragen te vinden.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="improvements-to-oemconfig-support-for-zebra-technologies-devices---4184154---"></a>Verbeteringen in de ondersteuning van OEMConfig voor apparaten van Zebra Technologies<!-- 4184154 -->
Intune biedt volledige ondersteuning voor alle functies van Zebra OEMConfig. Klanten die apparaten van Zebra Technologies beheren met Android Enterprise en OEMConfig, kunnen op één apparaat meerdere profielen van OEMConfig implementeren. Klanten kunnen ook uitgebreide rapportages bekijken over de status van hun profielen van Zebra OEMConfig.

Zie [Meerdere profielen van OEMConfig Implementeren op apparaten van Zebra in Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md) voor meer informatie.

Er is geen wijziging in het gedrag van OEMConfig voor andere OEM's.

Van toepassing op:
- Android Enterprise
- Apparaten van Zebra Technologies die ondersteuning bieden voor OEMConfig. Neem contact op met Zebra voor specifieke informatie over ondersteuning.

#### <a name="configure-system-extensions-on-macos-devices---6255624---"></a>Systeemuitbreidingen op macOS-apparaten configureren<!-- 6255624 -->
Op macOS-apparaten kunt u een profiel voor kernelextensies maken om instellingen te configureren op kernelniveau (**Apparaten** > **Configuratieprofielen** > **macOS** voor platform > **Kernelextensies** voor profiel). In een toekomstige versie schaft Apple kernelextensies uiteindelijk af en vervangt deze door systeemextensies.

Systeemextensies worden uitgevoerd in de gebruikersruimte en hebben geen toegang tot de kernel. Het doel is de beveiliging te verhogen en de eindgebruiker meer controle te bieden, terwijl aanvallen op kernelniveau beperkt worden. Met zowel kernelextensies als systeemextensies kunnen gebruikers app-extensies installeren waarmee de systeemeigen mogelijkheden van het besturingssysteem worden uitgebreid.

In Intune kunt u zowel kernelextensies als systeemextensies configureren (**Apparaten** > **Configuratieprofielen** > **macOS** voor platform > **Systeemextensies** voor profiel). Kernelextensies zijn van toepassing op 10.13.2 en nieuwer. Systeemextensies zijn van toepassing op 10.15 en nieuwer. Vanaf macOS 10.15 tot macOS 10.15.4 kunnen kernelextensies en systeemextensies naast elkaar worden uitgevoerd. 

Zie [macOS-kernelextensies toevoegen](../configuration/kernel-extensions-overview-macos.md) voor meer informatie over deze extensies op apparaten van macOS.

Van toepassing op:
- macOS 10.15 of hoger

#### <a name="configure-app-and-process-privacy-preferences-on-macos-devices---2934232-----"></a>Privacyvoorkeuren voor apps en processen op apparaten van macOS configureren<!-- 2934232   --> 
Bij de release van macOS Catalina 10.15 zijn nieuwe beveiligings- en privacyverbeteringen toegevoegd. Standaard kunnen toepassingen en processen zonder toestemming van de gebruiker geen toegang krijgen tot specifieke gegevens. Als gebruikers geen toestemming geven, werken de toepassingen en processen mogelijk niet. Intune voegt ondersteuning toe voor instellingen waarmee IT-beheerders toestemming voor toegang tot gegevens namens eindgebruikers kunnen toestaan of weigeren op apparaten waarop macOS 10.14 of hoger wordt uitgevoerd. Door deze instellingen blijven toepassingen en processen goed werken en zijn er minder vaak prompts te zien. 

Zie [privacyvoorkeuren van macOS](../configuration/device-restrictions-macos.md#privacy-preferences) voor meer informatie over de instellingen die u kunt beheren.

Van toepassing op:
- macOS 10.14 en hoger

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Apparaatinschrijving

#### <a name="enrollment-restrictions-support-scope-tags--4209550----"></a>Inschrijvingsbeperkingen bieden ondersteuning voor bereiktags<!--4209550  -->
U kunt bereiktags nu toewijzen aan inschrijvingsbeperkingen. Ga hiervoor naar [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **Inschrijvingsbeperkingen** > **Beperking maken**. Maak een van beide typen beperkingen en u ziet de pagina **Bereiktags**. Zie [Inschrijvingsbeperkingen instellen](../enrollment/enrollment-restrictions-set.md) voor meer informatie.

#### <a name="autopilot-support-for-hololens-2-devices--6305220----"></a>Autopilot-ondersteuning voor Hololens 2-apparaten<!--6305220  -->
Windows Autopilot biedt nu ondersteuning voor Hololens 2-apparaten. Zie [Windows Autopilot voor HoloLens 2](https://docs.microsoft.com/hololens/hololens2-autopilot) voor meer informatie over het gebruik van Autopilot voor Hololens.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="use-sync-remote-action-in-bulk-for-ios--6440956--idmiss--"></a>Externe actie synchroniseren in bulk gebruiken voor iOS<!--6440956  idmiss-->
U kunt nu de externe actie synchroniseren op maximaal 100 apparaten van iOS tegelijk gebruiken. Ga naar [Beheercentrum voor Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **Alle apparaten** > **Bulkapparaatacties** om deze nieuwe functie weer te geven. 

#### <a name="automated-device-sync-interval-down-to-12-hours--3077535----"></a>Interval voor automatisch synchroniseren van apparaten verlaagd tot 12 uur<!--3077535  -->
Voor Automated Device Enrollment van Apple is het automatische synchronisatie-interval voor apparaten tussen Intune en Apple Business Manager gereduceerd van 24 uur tot 12 uur. Zie [Beheerde apparaten synchroniseren](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices) voor meer informatie over synchronisatie.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Apparaatbeveiliging

#### <a name="derived-credentials-support-for-disa-purebred-on-android-devices---6939073-------"></a>Ondersteuning voor afgeleide referenties voor DISA Purebred op Android-apparaten<!-- 6939073     -->
U kunt nu *DISA Purebred* op volledig beheerde Android Enterprise-apparaten gebruiken als provider van [afgeleide referenties](../protect/derived-credentials.md). Er wordt ook ondersteuning geboden voor het ophalen van een afgeleide referentie voor DISA Purebred. U kunt een afgeleide referentie gebruiken voor app-verificatie, Wi-Fi, VPN of voor S/MIME-ondertekening en/of versleuteling voor apps die dit ondersteunen. 

#### <a name="send-push-notifications-as-an-action-for-noncompliance----1733150-----"></a>Pushmeldingen verzenden als actie voor niet-naleving <!-- 1733150   -->
U kunt nu een [actie voor niet-naleving](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) configureren die een pushmelding naar een gebruiker verzendt wanneer het apparaat niet voldoet aan de voorwaarden van een compliancebeleid. De nieuwe actie is **Pushmelding verzenden naar eindgebruiker** en wordt ondersteund op Android- en iOS-apparaten.

Wanneer gebruikers de pushmelding op hun apparaat selecteren, wordt de Bedrijfsportal- of Intune-app geopend om gedetailleerd weer te geven waarom ze niet compatibel zijn.

#### <a name="endpoint-security-content-and-new-features---5720009-5892558-7130145-5653324-7140602----"></a>Inhoud van eindpuntbeveiliging en nieuwe functies<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

De documentatie voor Intune [Eindpuntbeveiliging](../protect/endpoint-security.md) is nu beschikbaar. In het knooppunt eindpuntbeveiliging van het Beheercentrum voor Microsoft Endpoint Manager kunt u het volgende doen:

- Gericht beveiligingsbeleid maken en implementeren op uw beheerde apparaten
- Integratie met Microsoft Defender Advanced Threat Protection configureren en beveiligingstaken beheren die helpen bij het herstellen van risico’s voor apparaten met een risico die als zodanig door uw ATP-team zijn geïdentificeerd
- Beveiligingsbasislijnen configureren
- Naleving van het apparaat en het beleid voor voorwaardelijke toegang beheren
- De nalevingsstatus voor al uw apparaten van zowel Intune als Configuration Manager bekijken wanneer Configuration Manager is geconfigureerd voor koppeling van de client.

Naast de beschikbaarheid van inhoud zijn de volgende punten deze maand nieuw voor Eindpuntbeveiliging:

- [**Eindpuntbeveiligingsbeleid**](../protect/endpoint-security-policy.md) **is niet meer in** ***preview*** en is nu klaar voor gebruik in productieomgevingen, als *algemeen beschikbaar*, met twee uitzonderingen:

  - In een nieuwe *openbare preview* kunt u het [**Microsoft Defender Firewall-regels** profiel](../protect/endpoint-security-firewall-policy.md#firewall-profiles) voor Windows 10 Firewallbeleid gebruiken. Met elk exemplaar van dit profiel kunt u maximaal 150 firewallregels configureren ter aanvulling van uw Microsoft Defender Firewall-profielen. 
  - Beveiligingsbeleid voor accountbeveiliging blijft in preview. 

- U kunt nu [**een duplicaat van eindpuntbeveiligingsbeleid maken**](../protect/endpoint-security-policy.md#duplicate-a-policy). Duplicaten behouden de instellingen van de configuratie van het oorspronkelijke beleid, maar krijgen een nieuwe naam. Het nieuwe beleidsexemplaar bevat geen toewijzingen aan groepen voordat u het nieuwe beleidsexemplaar bewerkt om deze toe te voegen. U kunt het volgende beleid dupliceren:
  - Antivirus
  - Schijfversleuteling
  - Firewall
  - Eindpuntdetectie en -respons
  - Kwetsbaarheid voor aanvallen verminderen
  - Accountbeveiliging

- U kunt nu [**een duplicaat van een beveiligingsbasislijn maken**](../protect/security-baselines.md#duplicate-a-security-baseline). Duplicaten behouden de instellingen van de configuratie van de oorspronkelijke basislijn, maar krijgen een nieuwe naam. Het nieuwe exemplaar van de basislijn bevat geen toewijzingen aan groepen voordat u het nieuwe exemplaar van de basislijn bewerkt om deze toe te voegen.

- Er is een nieuw rapport voor het antivirusbeleid van de eindpuntbeveiliging beschikbaar: [**Beschadigde eindpunten voor Windows 10**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). Dit rapport is een nieuwe pagina die u kunt selecteren wanneer u uw antivirusbeleid van de eindpuntbeveiliging bekijkt. In het rapport wordt de antivirusstatus van uw door MDM beheerde Windows 10-apparaten weergegeven.  

#### <a name="support-for-smime-signing-and-encryption-certificates-with-outlook-on-android---7207474----"></a>Ondersteuning voor S/MIME-ondertekening en versleutelingscertificaten met Outlook op Android<!-- 7207474  -->
U kunt nu certificaten voor S/MIME-ondertekening en versleuteling gebruiken met Outlook op Android. Met deze ondersteuning kunt u deze certificaten inrichten door gebruik te maken van SCEP, PKCS en van geïmporteerde certificaatprofielen van PKCS. De volgende platformen van Android worden ondersteund:

- Android Enterprise-werkprofiel
- Android-apparaatbeheerder

Ondersteuning voor volledig beheerde Android Enterprise-apparaten is binnenkort beschikbaar.

Zie [Vertrouwelijkheidslabels en -bescherming in Outlook voor iOS en Android](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) in de documentatie van Exchange voor meer informatie over deze ondersteuning.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

#### <a name="device-reports-ui-update---6269408---"></a>Apparaat rapporteert dat er een update is van de gebruikersinterface<!-- 6269408 -->
Het deelvenster rapportenoverzicht biedt nu een tabblad **Overzicht** en een tabblad **Rapporten**. Selecteer in het [Beheercentrum voor Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) **Rapporten**, selecteer vervolgens het tabblad **Rapporten** om de beschikbare rapporttypen te bekijken. Zie [Intune-rapporten](../fundamentals/reports.md) voor verwante gegevens.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="scripting"></a>Uitvoeren van scripts

#### <a name="macos-script-support---6376978----"></a>ondersteuning voor macOS-script<!-- 6376978  -->
Scriptondersteuning voor macOS is nu algemeen beschikbaar. Daarnaast is ondersteuning toegevoegd voor zowel door de gebruiker toegewezen scripts als macOS-apparaten die zijn ingeschreven bij Automatische apparaatinschrijving van Apple (voorheen Device Enrollment Program). Zie [Shell-scripts op macOS-apparaten gebruiken in Intune](../apps/macos-shell-scripts.md) voor meer informatie.


<!-- ########################## -->
## <a name="week-of-may-4-2020"></a>Week van 4 mei 2020  

### <a name="company-portal-for-android-guides-users-to-get-apps-after-work-profile-enrollment----6103999---"></a>Bedrijfsportal voor Android helpt gebruikers apps te verkrijgen na registratie van het werkprofiel <!-- 6103999 -->
De in-app-richtlijnen in de bedrijfsportal zijn verbeterd zodat gebruikers gemakkelijker apps kunnen zoeken en installeren. Nadat gebruikers zich hebben geregistreerd voor werkprofielbeheer, zien ze een bericht dat ze aanbevolen apps kunnen vinden in de Google Play-versie met badge. De laatste stap in [Apparaat inschrijven met Android-profiel](../user-help/enroll-device-android-work-profile.md) is bijgewerkt zodat het nieuwe bericht wordt weergegeven. Gebruikers zien ook de nieuwe koppeling **Apps downloaden** in de het linkerpaneel van de bedrijfsportal. Om ruimte te maken voor deze nieuwe en verbeterde ervaringen, is het tabblad **Apps** verwijderd. Als u de bijgewerkte vensters wilt zien, gaat u naar [UI-updates voor eindgebruikers-apps voor Intune](./whats-new-app-ui.md). 

<!-- ########################## -->
## <a name="week-of-april-20-2020"></a>Week van 20 april 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758----"></a>Microsoft Endpoint Manager-tenant koppelen: Synchronisatie van apparaten en apparaatacties<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager brengt Configuration Manager en Intune samen in één console. Vanaf Configuration Manager versie 2002 kunt u uw Configuration Manager-apparaten uploaden naar de cloudservice en er acties op uitvoeren in het beheercentrum. Raadpleeg voor meer informatie [Microsoft Endpoint Manager-tenant koppelen: Synchronisatie van apparaten en apparaatacties](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="microsoft-office-365-proplus-rename---6368143---"></a>Naamswijziging Microsoft Office 365 ProPlus<!-- 6368143 -->
De naam van Microsoft Office 365 ProPlus wordt gewijzigd in **Microsoft 365-apps voor ondernemingen**. Zie [Naamswijziging voor Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change) voor meer informatie. In onze documentatie verwijzen we er doorgaans naar met Microsoft 365-apps. In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) vindt u de apps door **Apps** > **Windows** > **Toevoegen** te selecteren. Zie [Apps toevoegen aan Microsoft Intune](../apps/apps-add.md) voor informatie over het toevoegen van apps.

<!-- ########################## -->
## <a name="week-of-april-13-2020-2004-service-release"></a>Week van 13 april 2020 (2004 servicerelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="manage-smime-settings-for-outlook-on-android-enterprise-devices---6517085-----"></a>S/MIME-instellingen voor Outlook op Android Enterprise-apparaten beheren<!-- 6517085   -->
U kunt met app-configuratiebeleid de S/MIME-instelling voor Outlook beheren op apparaten waarop Android Enterprise wordt uitgevoerd. U kunt ook kiezen of u wilt toestaan dat de apparaatgebruikers S/MIME in- of uitschakelen in de Outlook-instellingen. Ga in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) naar **Apps** > **App-configuratiebeleid** > **Toevoegen** > **Beheerde apparaten** om app-configuratiebeleid voor Android te gebruiken. Zie [Microsoft Outlook-configuratie-instellingen](../apps/app-configuration-policies-outlook.md) voor meer informatie over het configureren van instellingen voor Outlook.

#### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Testen voorafgaand aan de release voor beheerde Google Play-apps<!-- 2681933  -->
Organisaties die gebruikmaken van [gesloten testtrajecten van Google Play voor het testen van apps voorafgaand aan de release](https://support.google.com/googleplay/android-developer/answer/3131213) kunnen deze trajecten beheren met Intune. U kunt selectief apps die worden gepubliceerd naar de trajecten voorafgaand aan de productiefase van Google Play aan testgroepen toewijzen om tests uit te voeren. In Intune kunt u ook zien of er voor een app een testtraject voor een build voorafgaand aan de productiefase is gepubliceerd en u kunt dat traject ook toewijzen aan AAD-gebruikersgroepen of -apparaatgroepen. Deze functie is beschikbaar voor al onze momenteel ondersteunde Android Enterprise-scenario's (werkprofiel, volledig beheerd en toegewezen). In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) kunt u een Beheerde Google Play-app toevoegen door **Apps** > **Android** > **Toevoegen** te selecteren. Zie [Werken met gesloten testtrajecten van Beheerde Google Play](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks) voor meer informatie.

#### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams is nu opgenomen in het Office 365-pakket voor macOS<!-- 5903936  -->
Gebruikers aan wie Microsoft Office voor macOS is toegewezen in Microsoft Endpoint Manager krijgen nu naast de bestaande Microsoft Office-apps (Word, Excel, PowerPoint, Outlook en OneNote) ook Microsoft Teams. Intune herkent de bestaande Mac-apparaten waarop de andere Office voor macOS-apps zijn geïnstalleerd en probeert Microsoft Teams te installeren wanneer het apparaat de volgende keer bij Intune wordt ingecheckt. In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) vindt u het **Office 365-pakket** voor macOS door **Apps** > **macOS** > **Toevoegen** te selecteren. Zie [Office 365 toewijzen aan macOS-apparaten met Microsoft Intune](../apps/apps-add-office365-macos.md) voor meer informatie.

#### <a name="update-to-android-app-configuration-policies---6113334----"></a>Update voor configuratiebeleid voor Android-apps<!-- 6113334  -->
De configuratiebeleidsregels voor Android-apps zijn bijgewerkt, zodat beheerders het type apparaatinschrijving kunnen selecteren voordat een app-configuratieprofiel wordt gemaakt. De functionaliteit wordt toegevoegd aan het account voor certificaatprofielen die zijn gebaseerd op inschrijvingstype (werkprofiel of apparaateigenaar).  Deze update biedt het volgende:

1. Als er een nieuw profiel wordt gemaakt en Werkprofiel en Apparaateigenaarprofiel als het type apparaatinschrijving zijn geselecteerd, kunt u geen certificaatprofiel aan het app-configuratiebeleid koppelen.
2. Als er een nieuw profiel wordt gemaakt en alleen Werkprofiel is geselecteerd, kan Werkprofiel-certificaatbeleid dat is gemaakt onder Apparaatconfiguratie worden gebruikt.
3. Als er een nieuw profiel wordt gemaakt en alleen Apparaateigenaar is geselecteerd, kan Apparaateigenaar-certificaatbeleid dat is gemaakt onder Apparaatconfiguratie worden gebruikt. 

> [!IMPORTANT]
> Bestaand beleid dat is gemaakt voorafgaand aan de release van deze functie (release april 2020 - 2004) en waarvoor geen certificaatprofielen zijn gekoppeld aan het beleid, wordt voor het type apparaatinschrijving standaard ingesteld op Werkprofiel en Apparaateigenaarprofiel. Bestaand beleid dat is gemaakt voorafgaand aan de release van deze functie en waaraan certificaatprofielen zijn gekoppeld, wordt bovendien standaard ingesteld op uitsluitend Werkprofiel.

Daarnaast voegen we Gmail- en Nine-e-mailconfiguratieprofielen toe die worden gebruikt met zowel het inschrijvingstype Werkprofiel als het inschrijvingstype Apparaateigenaar, waaronder het gebruik van certificaatprofielen voor beide e-mailconfiguratietypen.  Gmail- of Nine-beleid dat u onder Apparaatconfiguratie voor werkprofielen hebt gemaakt, blijft van toepassing op het apparaat en het is niet nodig om ze te verplaatsen naar het app-configuratiebeleid.

In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) vindt u het app-configuratiebeleid door **Apps** > **App-configuratiebeleid** te selecteren. Zie [App-configuratiebeleid voor Microsoft Intune](../apps/app-configuration-policies-overview.md) voor meer informatie over app-configuratiebeleid.

#### <a name="push-notification-when-device-ownership-type-is-changed---5575875---"></a>Pushmelding wanneer verandering optreedt in eigendomstype voor het apparaat<!-- 5575875 -->
U kunt uit het oogpunt van privacy een pushmelding configureren die naar de gebruikers van zowel de Android- als de iOS-bedrijfsportal wordt verzonden wanneer het eigendomstype voor hun apparaat is gewijzigd van Persoonlijk naar Zakelijk. Deze pushmelding is standaard ingesteld op uitgeschakeld. U kunt de instelling vinden in Microsoft Endpoint Manager door **Tenantbeheer** > **Aanpassing** te selecteren. Zie [Eigendom van het apparaat wijzigen](../enrollment/corporate-identifiers-add.md#change-device-ownership) voor meer informatie over de wijze waarop het eigendom van het apparaat van invloed is op uw eindgebruikers.

#### <a name="group-targeting-support-for-customization-pane---4722837----"></a>Ondersteuning voor groepsdoelen voor het deelvenster Aanpassing<!-- 4722837  -->
U kunt de instellingen in het deelvenster **Aanpassing** toepassen op gebruikersgroepen. Ga voor deze instellingen in Intune naar het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en selecteer **Tenantbeheer** > **Aanpassing**. Zie [De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen](../apps/company-portal-app.md) voor meer informatie over aanpassing.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="multiple-evaluate-each-connection-attempt-on-demand-vpn-rules-supported-on-ios-ipados-and-macos---6424615----"></a>Meerdere on-demand VPN-regels met de actie 'Elke verbindingspoging evalueren' die worden ondersteund in iOS, iPadOS en macOS<!-- 6424615  -->
De gebruikerservaring van Intune maakt meerdere on-demand VPN-regels mogelijk in hetzelfde VPN-profiel met de actie **Elke verbindingspoging evalueren** (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** of **macOS** voor het platform > **VPN** voor profiel > **Automatische VPN** > **On-demand**).

Alleen de eerste regel in de lijst is gehonoreerd. Dit gedrag is vast, en in Intune worden alle regels in de lijst geëvalueerd. Elke regel wordt geëvalueerd in de volgorde waarin deze wordt weergegeven in de lijst met regels op aanvraag.

> [!NOTE]
> Als u beschikt over bestaande VPN-profielen die gebruikmaken van deze on-demand VPN-regels, geldt de oplossing voor de volgende keer dat u het VPN-profiel wijzigt. Maak bijvoorbeeld een kleine wijziging, wijzig bijvoorbeeld de naam van de verbinding, en sla het profiel op.
>
> Als u SCEP-certificaten gebruikt voor verificatie, zorgt deze wijziging ervoor dat de certificaten voor dit VPN-profiel opnieuw worden uitgegeven.

Van toepassing op:
- iOS/iPadOS
- macOS

Zie [VPN-profielen maken](../configuration/vpn-settings-configure.md) voor meer informatie over VPN-profielen.

#### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155-----"></a>Aanvullende opties in profielen voor eenmalige aanmelding en app-extensies voor eenmalige aanmelding op iOS- en iPadOS-apparaten<!-- 6504155   -->

Op iOS-/iPadOS-apparaten kunt u het volgende doen:
- Stel in profielen voor eenmalige aanmelding (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatfuncties** voor profiel > **Eenmalige aanmelding**) de principal-naam van Kerberos in op de SAM-accountnaam (Security Account Manager) in profielen voor eenmalige aanmelding. 
- Configureer in profielen voor app-extensies voor eenmalige aanmelding (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatfuncties** voor profieltype > **App-extensie voor eenmalige aanmelding**) de iOS/iPadOS Microsoft Azure AD-extensie met minder klikken door een nieuw type app-extensie voor eenmalige aanmelding te gebruiken. U kunt de Azure AD-extensie voor apparaten in de modus Gedeeld apparaat inschakelen en extensiespecifieke gegevens naar de extensie verzenden.

Van toepassing op:
- iOS/iPadOS 13.0+

Zie [Overzicht van app-extensies voor eenmalige aanmelding](../configuration/device-features-configure.md#single-sign-on-app-extension) en [Lijst met instellingen voor eenmalige aanmelding](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) voor meer informatie over het gebruik van eenmalige aanmelding op iOS-/iPadOS-apparaten.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Apparaatinschrijving

#### <a name="delete-apple-automated-device-enrollment-token-when-default-profile-is-present--6393220---"></a>Token voor automatische apparaatinschrijving van Apple verwijderen als standaardprofiel aanwezig is<!--6393220 -->
Voorheen kon u een standaardprofiel niet verwijderen. Dit betekende dat u het bijbehorende token voor automatische apparaatinschrijving niet kon verwijderen. Nu kunt u het token verwijderen als:
- er geen apparaten aan het token zijn toegewezen
- er een standaardprofiel aanwezig is. Hiervoor verwijdert u het standaardprofiel en vervolgens het bijbehorende token.
Zie [Een ADE-token uit Intune verwijderen](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-ade-token-from-intune) voor meer informatie.

#### <a name="scaled-up-support-for-apple-automated-device-enrollment-and-apple-configurator-2-devices-profiles-and-tokens--3542402---"></a>Uitgebreide ondersteuning voor apparaten, profielen en tokens voor Apple ADE en Apple Configurator 2<!--3542402 -->
Om gedistribueerde IT-afdelingen en -organisaties te helpen, ondersteunt Intune nu tot maximaal 1000 inschrijvingsprofielen per token, 2000 ADE-tokens (voorheen bekend als DEP) per Intune-account en 75.000 apparaten per token. Er is geen specifieke limiet voor apparaten per inschrijvingsprofiel, beneden het maximumaantal apparaten per token.

Intune ondersteunt nu tot maximaal 1000 Apple Configurator 2-profielen.

Ga voor meer informatie naar [Ondersteund volume](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### <a name="all-devices-page-column-entry-changes--6967616---"></a>Wijzigingen in kolomvermelding van alle apparaten<!--6967616 -->
Op de pagina **Alle apparaten** zijn de vermeldingen voor de kolom **Beheerd door** gewijzigd:
- Nu wordt *Intune* weergegeven in plaats van *MDM*
- Nu wordt *Co-beheer* weergegeven in plaats van *MDM/ConfigMgr-agent*

De exportwaarden zijn ongewijzigd.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="trusted-platform-manager-tpm-version-information-now-on-device-hardware-page--6224914-idmiss---"></a>Informatie over de versiegegevens van TPM (Trusted Platform Manager) op de pagina Apparaathardware<!--6224914 idmiss -->
U kunt nu het TPM-versienummer zien op de hardwarepagina van een apparaat ([Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > Kies een apparaat > **Hardware** > kijk onder **Systeembehuizing**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

#### <a name="collect-logs-to-better-troubleshoot-scripts-assigned-to-macos-devices---6359853----"></a>Logboeken verzamelen voor het beter oplossen van problemen in scripts die zijn toegewezen aan macOS-apparaten<!-- 6359853  -->
U kunt nu logboeken verzamelen voor het beter oplossen van problemen in scripts die zijn toegewezen aan macOS-apparaten. U kunt logboeken van maximaal 60 MB (gecomprimeerde) of 25 bestanden verzamelen, afhankelijk van wat zich het eerst voordoet. Zie [Problemen met macOS Shell-scriptbeleid oplossen met behulp van logboekverzameling](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection) voor meer informatie.
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Beveiliging

#### <a name="derived-credentials-to-provision-android-enterprise-fully-managed-devices-with-certificates--4839592------"></a>Afgeleide referenties voor het inrichten van volledig beheerde Android Enterprise-apparaten met certificaten<!--4839592    -->
Intune ondersteunt nu het gebruik van [afgeleide referenties](../protect/derived-credentials.md) als verificatiemethode voor Android-apparaten. Afgeleide referenties zijn een implementatie van de National Institute of Standards and Technology (NIST) 800-157-standaard voor het implementeren van certificaten op apparaten. Onze ondersteuning voor Android vormt een uitbreiding op onze ondersteuning voor apparaten met iOS/iPadOS.

Afgeleide referenties zijn afhankelijk van het gebruik van een Personal Identity Verification (PIV) of Common Access Card (CAC), zoals een smartcard. Om een afgeleide referentie voor een mobiele apparaat te verkrijgen, beginnen gebruikers in de Microsoft Intune-app en volgen ze een registratiewerkstroom die uniek is voor de provider die u gebruikt. Alle providers hebben met elkaar gemeen dat ze vereisen dat een smartcard voor verificatie bij de afgeleide referentieprovider. Deze provider verzendt vervolgens een certificaat naar het apparaat dat is afgeleid van de smartcard van de gebruiker.

U gebruikt afgeleide referenties als verificatiemethode voor configuratieprofielen voor apparaten voor VPN en Wi-Fi. U kunt ze ook gebruiken voor app-verificatie, S/MIME-ondertekening en versleuteling voor toepassingen die hiervoor ondersteuning bieden.

Intune biedt nu ondersteuning voor de volgende afgeleide referentieproviders bij Android:
- Entrust Datacard
- Intercede

In een toekomstige release komt een derde provider, DISA Purebred, beschikbaar voor Android.

#### <a name="microsoft-edge-security-baseline-is-now-generally-available--6586139---"></a>De functie Beveiligingsbasislijn van Microsoft Edge is nu algemeen beschikbaar<!--6586139 -->

Er is nu een nieuwe versie van de functie [Beveiligingsbasislijn van Microsoft Edge](../protect/security-baselines.md#available-security-baselines) beschikbaar. Deze wordt uitgebracht als algemeen beschikbaar (GA). De voorgaande Microsoft Edge-basislijn was in preview.  De nieuwe basislijnversie van april 2020 (Microsoft Edge versie 80 en hoger). 

Met de release van deze nieuwe basislijn is het niet meer mogelijk om profielen te maken op basis van de vorige basislijnversies, maar u kunt nog steeds profielen gebruiken die u hebt gemaakt met deze versies. U kunt er ook voor kiezen om [uw bestaande profielen bij te werken, zodat u de meest recente basislijnversie kunt gebruiken](../protect/security-baselines.md#change-the-baseline-version-for-a-profile). 

<!-- ########################## -->
## <a name="week-of-april-6-2020"></a>Week van 6 april 2020

#### <a name="new-shell-script-settings-for-macos-devices---6884363---"></a>Nieuwe instellingen voor shell-script voor macOS-apparaten<!-- 6884363 -->
Bij het configureren van shell-scripts voor macOS-apparaten kunt u nu de volgende nieuwe instellingen configureren: 
- Scriptmeldingen op apparaten verbergen
- Scriptfrequentie
- Maximum aantal keren dat het script opnieuw moet worden uitgevoerd als het script mislukt

Zie [Shell-scripts op macOS-apparaten gebruiken in Intune](../apps/macos-shell-scripts.md) voor meer informatie.

<!-- ########################## -->
## <a name="week-of-march-30-2020"></a>Week van 30 maart 2020

### <a name="new-url-for-the-microsoft-endpoint-manager-admin-center---3704810---"></a>Nieuwe URL voor het Microsoft Endpoint Manager-beheercentrum<!-- 3704810 -->
De URL voor het Microsoft Endpoint Manager-beheercentrum (voorheen Microsoft 365 Device Management) is gewijzigd in [https://endpoint.microsoft.com](https://endpoint.microsoft.com), zodat deze overeenkomt met de aankondiging van Microsoft Endpoint Manager op Ignite van vorig jaar. De URL voor het oude beheercentrum ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) werkt nog wel, maar het wordt aanbevolen de nieuwe URL te gebruiken voor het Microsoft Endpoint Manager-beheercentrum.

Zie [IT-taken vereenvoudigen met het Microsoft Endpoint Manager-beheercentrum](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center) voor meer informatie.  


### <a name="app-management"></a>Appbeheer  

#### <a name="company-portal-for-ios-supports-landscape-mode--6048329----"></a>Bedrijfsportal voor iOS biedt ondersteuning voor de liggende modus<!--6048329  -->   
Gebruikers kunnen hun apparaat nu inschrijven, apps zoeken en ondersteuning krijgen met hun favoriete schermstand. De app detecteert automatisch de stand en past de weergave aan de liggende of staande modus van het scherm aan, tenzij gebruikers het scherm vergrendelen in de staande modus.  

#### <a name="script-support-for-macos-devices-public-preview---4280361----"></a>Scriptondersteuning voor macOS-apparaten (openbare preview)<!-- 4280361  -->
U kunt scripts toevoegen en implementeren op macOS-apparaten. Dankzij deze ondersteuning hebt u meer mogelijkheden om macOS-apparaten te configureren buiten wat al mogelijk is, met behulp van systeemeigen MDM-mogelijkheden op macOS-apparaten. Zie [Shell-scripts op macOS-apparaten gebruiken in Intune](../apps/macos-shell-scripts.md) voor meer informatie.

<!-- ########################## -->
## <a name="week-of-march-24-2020"></a>Week van 24 maart 2020

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Verbeterde gebruikersinterface-ervaring bij het maken van profielen voor apparaatbeperkingen op Android- en Android Enterprise-apparaten<!-- 5841361 -->
Wanneer u een profiel voor Android- of Android Enterprise-apparaten maakt, wordt de ervaring in het Microsoft Endpoint Manager-beheercentrum bijgewerkt. Deze wijziging is van invloed op de volgende apparaatconfiguratieprofielen (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android-apparaatbeheerder** of **Android Enterprise** voor platform):

- Apparaatbeperkingen: Android-apparaatbeheerder
- Apparaatbeperkingen: Android Enterprise-apparaateigenaar
- Apparaatbeperkingen: Android Enterprise - Werkprofiel

Zie [Android-apparaatbeheerder](../configuration/device-restrictions-android.md) en [Android Enterprise](../configuration/device-restrictions-android-for-work.md) voor meer informatie over de apparaatbeperkingen die u kunt configureren.

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569002-5568997---"></a>Verbeterde gebruikersinterface-ervaring bij het maken van configuratieprofielen op iOS-/iPadOS- en macOS-apparaten<!-- 5569002 5568997 -->
Wanneer u een profiel voor iOS-of macOS-apparaten maakt, wordt de ervaring in het Microsoft Endpoint Manager-beheercentrum bijgewerkt. Deze wijziging is van invloed op de volgende apparaatconfiguratieprofielen (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** of **macOS** als platform):

- Aangepast: iOS/iPadOS, macOS
- Apparaatfuncties: iOS/iPadOS, macOS
- Apparaatbeperkingen: iOS/iPadOS, macOS
- Endpoint Protection: macOS
- Extensies: macOS
- Voorkeursbestand: macOS

### <a name="hide-from-user-configuration-setting-in-device-features-on-macos-devices---6524869---"></a>Verbergen in de instelling voor gebruikersconfiguratie in de apparaatfuncties op macOS-apparaten<!-- 6524869 -->

Wanneer u een configuratieprofiel voor apparaatfuncties maakt op macOS-apparaten, is er een nieuwe instelling beschikbaar, **Verbergen voor gebruikersconfiguratie**, (via **Apparaten** > **Configuratieprofielen** > **Profiel maken** > **macOS** voor platform > **Apparaatfuncties** voor profiel > **Aanmeldingsitems**).

Met deze functie wordt het selectievakje voor het verbergen van een app in de lijst **Gebruikers en groepen** in de lijst met aanmeldingsitems voor apps op macOS-apparaten ingesteld. Voor bestaande profielen wordt deze instelling in de lijst als niet-geconfigureerd weergegeven. Beheerders kunnen bestaande profielen bijwerken om deze instelling te configureren.

Als deze optie is ingesteld op **Verbergen**, wordt het selectievakje voor het verbergen van een app ingeschakeld. Gebruikers kunnen dit niet wijzigen. De app wordt ook verborgen voor gebruikers nadat ze zich aanmelden op hun apparaten.

> [!div class="mx-imgBorder"]
> ![Apps verbergen op macOS-apparaten nadat gebruikers zich aanmelden bij het apparaat in Microsoft Intune en Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

Zie [Instellingen van apparaatfuncties voor macOS in Intune](../configuration/macos-device-features-settings.md) voor meer informatie over de instelling die u kunt configureren.

Deze functie is van toepassing op:

- macOS

<!-- ########################## -->
## <a name="week-of-march-16-2020-2003-service-release"></a>Week van 16 maart 2020 (2003 servicerelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="macos-and-ios-company-portal-updates---5779439-5780234----"></a>Updates voor de macOS- en iOS-bedrijfsportal<!-- 5779439, 5780234  -->
Het deelvenster Profiel van de macOS- en iOS-bedrijfsportal is bijgewerkt met de knop Afmelden. Daarnaast is de gebruikersinterface van het deelvenster Profiel in de macOS-bedrijfsportal verbeterd. Raadpleeg [De bedrijfsportal-app van Microsoft Intune configureren](../apps/company-portal-app.md) voor meer informatie over de bedrijfsportal-app.

#### <a name="retarget-web-clips-to-microsoft-edge-on-ios-devices---5455276-----"></a>Microsoft Edge als nieuw doel opgeven voor webclips op iOS-apparaten<!-- 5455276   -->
Nieuw geïmplementeerde webclips (vastgemaakte web-apps) op iOS-apparaten die verplicht in een beveiligde browser moeten worden geopend, worden nu geopend in Microsoft Edge in plaats van in de Intune Managed Browser. U moet een nieuw doel opgeven voor reeds bestaande webclips om ervoor te zorgen dat deze worden geopend in Microsoft Edge, en niet in de Managed Browser. Zie [Webtoegang beheren met behulp van Microsoft Edge met Microsoft Intune](../apps/manage-microsoft-edge.md) en [Webtoepassingen toevoegen aan Microsoft Intune](../apps/web-app.md) voor meer informatie.

#### <a name="use-the-intune-diagnostic-tool-with-microsoft-edge-for-android---4735244----"></a>Het diagnostisch hulpprogramma van Intune met Microsoft Edge voor Android<!-- 4735244  -->
Microsoft Edge voor Android is nu geïntegreerd met het diagnostisch hulpprogramma van Intune. Net als in Microsoft Edge voor iOS kunt u 'about:intunehelp' in de URL-balk (het adresvak) van Microsoft Edge op het apparaat invoeren om het diagnostisch hulpprogramma van Intune te starten. Dit hulpprogramma verstrekt gedetailleerde logboeken. Gebruikers kunnen worden geholpen bij het verzamelen van deze logboeken en het verzenden ervan naar hun IT-afdeling, of bij het bekijken van MAM-logboeken voor specifieke apps.

#### <a name="updates-to-intune-branding-and-customization---5236032----"></a>Updates van Huisstijl en aanpassing van Intune<!-- 5236032  -->
Het Intune-deelvenster Huisstijl en aanpassing is bijgewerkt met enkele verbeteringen, zoals:

- De naam van het deelvenster wordt gewijzigd in **Aanpassing**.
- De rangschikking en het ontwerp van de instellingen wordt verbeterd.
- De tekst en knopinfo voor instellingen wordt verbeterd.

Ga voor deze instellingen in Intune naar het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en selecteer **Tenantbeheer** > **Aanpassing**. Zie [De bedrijfsportal-app van Microsoft Intune configureren](../apps/company-portal-app.md) voor informatie over bestaande aanpassingen.

#### <a name="users-personal-encrypted-recovery-key---6273943----"></a>Persoonlijke, versleutelde herstelsleutel van gebruiker<!-- 6273943  -->
Er is een nieuwe Intune-functie beschikbaar waarmee gebruikers hun persoonlijke, versleutelde **FileVault**-herstelsleutel voor Mac-apparaten kunnen downloaden via de bedrijfsportal-toepassing voor Android of via de Android Intune-toepassing. Zowel de bedrijfsportal-toepassing als de Intune-toepassing bevat een koppeling om de onlinebedrijfsportal in een Chrome-browser te openen. Hier kunnen gebruikers de **FileVault**-herstelsleutel zien die ze nodig hebben voor toegang tot hun Mac-apparaten. Zie [Apparaatversleuteling gebruiken met Intune](../protect/encrypt-devices.md) voor meer informatie over versleuteling.

#### <a name="optimized-dedicated-device-enrollment----6114580----"></a>Geoptimaliseerde inschrijving van toegewezen Android-apparaten <!-- 6114580  -->
We optimaliseren de inschrijving voor toegewezen Android Enterprise-apparaten en maken het gemakkelijker om SCEP-certificaten die aan Wi-Fi zijn gekoppeld, toe te passen op toegewezen apparaten die zijn ingeschreven vóór 22 november 2019. Voor nieuwe inschrijvingen wordt de Intune-app gewoon geïnstalleerd, maar eindgebruikers hoeven tijdens de registratie de stap **Intune-agent inschakelen** niet meer uit te voeren. De installatie wordt automatisch uitgevoerd op de achtergrond en SCEP-certificaten die zijn gekoppeld aan Wi-Fi, kunnen worden geïmplementeerd en ingesteld zonder interactie van de eindgebruiker.  

Deze wijzigingen worden in de loop van de maand maart gefaseerd ingevoerd terwijl de Intune-serviceback-end wordt geïmplementeerd. Eind maart vertonen alle tenants dit nieuwe gedrag. Zie [Ondersteuning voor SCEP-certificaten in toegewezen Android Enterprise-apparaten](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147) voor bijbehorende informatie.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="new-user-experience-when-creating-administrative-templates-on-windows-devices--5096036---"></a>Nieuwe gebruikerservaring bij het maken van beheersjablonen op Windows-apparaten<!--5096036 -->
Op basis van feedback van klanten en onze overstap naar de nieuwe Azure-ervaring in volledig scherm hebben we de profielervaring voor Beheersjablonen bijgewerkt met een mapweergave. Er zijn geen wijzigingen aangebracht in instellingen of bestaande profielen. Uw bestaande profielen zijn dus niet gewijzigd en kunnen in de nieuwe weergave worden gebruikt. U kunt nog steeds naar alle instellingsopties navigeren door **Alle instellingen** te selecteren en zoekopdrachten te gebruiken. De structuurweergave is onderverdeeld in Computer- en Gebruikersconfiguraties. U vindt instellingen voor Windows, Office en Edge in de betreffende mappen.  

Van toepassing op:
- Windows 10 en nieuwer

#### <a name="vpn-profiles-with-ikev2-vpn-connections-can-use-always-on-with-iosipados-devices---1947932-----"></a>Voor VPN-profielen met IKEv2 VPN-verbindingen kan AlwaysOn worden gebruikt voor iOS-/iPadOS-apparaten<!-- 1947932   -->
Op iOS-/iPadOS-apparaten kunt u een VPN-profiel maken dat gebruikmaakt van een IKEv2-verbinding (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** als platform > **VPN** als profieltype). Nu kunt u permanente VPN configureren met IKEv2. IKEv2 VPN-profielen maken, nadat deze zijn geconfigureerd, automatisch verbinding en blijven verbonden (of maken snel opnieuw verbinding) met het VPN. De verbinding blijft bestaan, ook bij wisselingen van netwerk of als apparaten opnieuw worden opgestart.

In iOS/iPadOS is AlwaysOn VPN beperkt tot IKEv2-profielen.

Als u wilt zien welke IKEv2-instellingen u momenteel kunt configureren, gaat u naar [VPN-instellingen toevoegen op iOS-apparaten in Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Van toepassing op:
- iOS/iPadOS

#### <a name="delete-bundles-and-bundle-arrays-in-oemconfig-device-configuration-profiles-on-android-enterprise-devices---5550355-----"></a>Bundels en gebundelde matrices verwijderen uit OEMConfig-apparaatconfiguratieprofielen op Android Enterprise-apparaten<!-- 5550355   -->
Op Android Enterprise-apparaten kunt u OEMConfig-profielen maken en bijwerken (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** als platform > **OEMConfig** als profieltype). Gebruikers kunnen bundels en gebundelde matrices verwijderen met behulp van de **Configuratieontwerper** in Intune.

Zie [Android Enterprise-apparaten gebruiken en beheren met OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md) voor meer informatie over OEMConfig-profielen.

Van toepassing op:
- Android Enterprise

#### <a name="configure-the-iosipados-microsoft-azure-ad-sso-app-extension---5672534-----"></a>De SSO-extensie van Microsoft Azure AD voor iOS/iPadOS-apps configureren<!-- 5672534   -->
Het Microsoft Azure AD-team heeft een app-extensie voor SSO (eenmalige aanmelding) voor omleiden gemaakt, zodat gebruikers van iOS en iPadOS 13.0 en hoger met eenmalige aanmelding toegang hebben tot Microsoft-apps en -websites. Alle apps waarvoor eerder brokered verificatie werd uitgevoerd met de app Microsoft Authenticator, behouden SSO met de nieuwe SSO-extensie. Met de release van de SSO-extensie van Azure AD kunt u de SSO-extensie configureren met het type SSO-extensie voor omleiding van apps (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** als platform > **Apparaatfuncties** als profieltype > **App-extensie voor eenmalige aanmelding**.

Van toepassing op:
- iOS 13.0 en hoger
- iPadOS 13.0 en hoger

Zie [App-extensie voor eenmalige aanmelding](../configuration/device-features-configure.md#single-sign-on-app-extension) voor meer informatie over app-extensies voor SSO voor iOS.

#### <a name="enterprise-app-trust-settings-modification-setting-is-removed-from-iosipados-device-restriction-profiles---6225131-----"></a>De instelling voor aanpassing van de vertrouwensinstellingen voor de Enterprise-app is verwijderd uit de profielen voor apparaatbeperking voor iOS/iPadOS<!-- 6225131   -->
U maakt een profiel met apparaatbeperkingen op het iOS/iPadOS-apparaat (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatbeperkingen** voor profieltype). De instelling **Aanpassing van de vertrouwensinstellingen voor de Enterprise-app** is door Apple verwijderd en uit Intune verwijderd. Als u deze instelling momenteel in een profiel gebruikt, heeft dit geen invloed. Deze wordt verwijderd uit bestaande profielen. Deze instelling is ook verwijderd uit rapporten in Intune.

Van toepassing op:
- iOS/iPadOS

Ga naar [iOS- en iPadOS-apparaatinstellingen om functies toe te staan of te beperken met Intune](../configuration/device-restrictions-ios.md) als u alle instellingen wilt bekijken die u kunt beperken.

#### <a name="troubleshooting-pending-mam-policy-notification-changed-to-informational-icon--6348954---"></a>Problemen oplossen: Melding van MAM-beleid in behandeling gewijzigd in informatiepictogram<!--6348954 -->
Het meldingspictogram op de blade Probleemoplossing voor een MAM-beleid dat in behandeling is, is gewijzigd in een informatiepictogram.

####  <a name="ui-update-when-configuring-compliance-policy---3961639------"></a>Update van gebruikersinterface tijdens de configuratie van het nalevingsbeleid<!-- 3961639    -->

De gebruikersinterface voor het [maken van nalevingsbeleid](../protect/create-compliance-policy.md#create-the-policy) in Microsoft Endpoint Manager is bijgewerkt (**Apparaten** > **Nalevingsbeleid** > **Beleidsregels** > **Beleid maken**). Er is een nieuwe gebruikerservaring die dezelfde instellingen en gegevens bevat als die u eerder gebruikte. De nieuwe ervaring volgt een wizard-achtig proces voor het maken van een nalevingsbeleid en bevat een pagina waarop u *Toewijzingen* voor het beleid kunt toevoegen, en een pagina *Beoordelen en maken* waarop u uw configuratie kunt controleren voordat u het beleid maakt.

#### <a name="retire-noncompliant-devices---1827291---------"></a>Niet-compatibele apparaten buiten gebruik stellen<!-- 1827291       -->
We hebben een nieuwe actie voor niet-compatibele apparaten toegevoegd die u aan elk beleid kunt toevoegen, om het [niet-compatibele apparaat buiten gebruik te stellen](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance).  De nieuwe actie, **Het niet-compatibele apparaat buiten gebruik stellen** heeft tot gevolg dat alle bedrijfsgegevens van het apparaat worden verwijderd en dat het apparaat wordt verwijderd uit Intune-beheer.  Deze actie wordt uitgevoerd wanneer de geconfigureerde waarde in dagen is bereikt. Op dat moment komt het apparaat in aanmerking voor buitengebruikstelling. De minimumwaarde is 30 dagen.  Expliciete goedkeuring van de IT-beheerder is vereist voor het buiten gebruik stellen van de apparaten met behulp van de sectie *buiten gebruik stellen van niet-compatibele apparaten*, waarbij beheerders alle in aanmerking komende apparaten buiten gebruik kunnen stellen.

#### <a name="support-for-wpa-and-wpa2-in-ios-enterprise-wi-fi-profiles--6215273-----"></a>Ondersteuning voor WPA en WPA2 in Enterprise Wi-Fi-profielen voor iOS<!--6215273   -->
[Enterprise Wi-Fi-profielen voor iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) biedt nu ondersteuning voor het veld *Beveiligingstype*. Bij *Beveiligingstype* kunt u **WPA Enterprise** of **WPA/WPA2 Enterprise** selecteren en vervolgens een *EAP-type* selecteren.  (**Apparaten** > **Configuratieprofielen** > **Profiel maken** en selecteer **iOS/iPadOS** als *Platform* en vervolgens **Wi-Fi** als *Profiel*). 

De nieuwe Enterprise-opties zijn vergelijkbaar met die voor een basis-Wi-Fi-profiel voor iOS.

#### <a name="new-user-experience-for-certificate-email-vpn-and-wi-fi-vpn-profiles---5615208-----"></a>Nieuwe gebruikerservaring voor certificaat-, e-mail-, VPN- en Wi-Fi-profielen<!-- 5615208   -->
De [gebruikerservaring](../configuration/device-profile-create.md) in het Beheercentrum voor Microsoft Endpoint Manager is bijgewerkt (**Apparaten** > **Configuratieprofielen** > **Profiel maken**) voor het maken en aanpassen van de volgende profieltypen. De nieuwe ervaring biedt dezelfde instellingen als voorheen, maar kent een wizardachtige methode waarvoor minder horizontaal bladeren is vereist. U hoeft bestaande configuraties niet bij te werken met de nieuwe ervaring.

- Afgeleide referentie
- E-mail
- PKCS-certificaat
- PKCS-geïmporteerd certificaat
- SCEP-certificaat
- Vertrouwd certificaat
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Apparaatinschrijving

#### <a name="configure-if-enrollment-is-available-in-company-portal-for-android-and-ios---4260128----"></a>Configureren bij inschrijving is beschikbaar in de bedrijfsportal voor Android en iOS<!-- 4260128  -->
U kunt configureren of apparaatinschrijving in de bedrijfsportal op Android- en iOS-apparaten beschikbaar is met prompts, beschikbaar is zonder prompts of niet beschikbaar is voor gebruikers. Ga naar het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) en selecteer **Tenantbeheer** > **Aanpassing** > **Bewerken** > **Apparaatinschrijving** om deze instellingen in Intune te zoeken.  

Voor ondersteuning van de instelling voor het inschrijven van apparaten moeten eindgebruikers beschikken over deze bedrijfsportalversies:
-    Bedrijfsportal op iOS: versie 4.4 of hoger
-    Bedrijfsportal op Android: versie 5.0.4715.0 of hoger

Raadpleeg [De bedrijfsportal-app van Microsoft Intune configureren](../apps/company-portal-app.md) voor meer informatie over de bestaande bedrijfsportal-aanpassingen.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="new-android-report-on-android-devices-overview-page---5435435-----"></a>Nieuw Android-rapport op de overzichtspagina Android-apparaten<!-- 5435435   -->
Er is een rapport aan de Microsoft Endpoint Manager-beheerconsole toegevoegd op de pagina met het overzicht van Android-apparaten waarop wordt weergegeven hoeveel Android-apparaten zijn ingeschreven in elke oplossing voor apparaatbeheer. In dit diagram (vergelijkbaar met hetzelfde diagram dat u al via de Azure-console hebt gemaakt) ziet u het aantal apparaten met werkprofiel, volledig beheerd, toegewezen en door de beheerder geregistreerd. Kies **Apparaten** > **Android** > **Overzicht** om het rapport weer te geven.

#### <a name="guide-users-from-android-device-administrator-management-to-work-profile-management--5857738-----"></a>Gebruikers doorsturen van Beheer door Android-apparaatbeheerder naar Beheer van werkprofielen<!--5857738   -->
Binnenkort wordt een nieuwe nalevingsinstelling uitgebracht voor het Android-apparaatbeheerplatform. Met behulp van deze instelling kunt u een apparaat niet-compatibel maken als dit apparaat door de apparaatbeheerder wordt beheerd.

Op deze niet-compatibele apparaten zien gebruikers op de pagina **Apparaatinstellingen bijwerken** het bericht **Verplaatsen naar nieuwe instelling voor apparaatbeheer**. Als de gebruikers op de knop **Oplossen** tikken, worden ze geholpen bij het volgende:

1. Uitschrijven bij Beheer door apparaatbeheerder
2. Inschrijven bij Beheer van werkprofielen
3. Problemen met naleving oplossen 
 
Google vermindert de ondersteuning voor apparaatbeheerders in nieuwe Android-versies in een poging om apparaatbeheer moderner, breder en veiliger te maken met behulp van Android Enterprise.  Intune biedt slechts tot het tweede kwartaal van 2020 nog ondersteuning voor Android-apparaten met Android 10 en hoger die door apparaatbeheerder worden beheerd. Apparaten die worden beheerd met apparaatbeheerder (m.u.v. Samsung) en waarop Android 10 of hoger wordt uitgevoerd, kunnen na dit moment niet langer volledig worden beheerd. Betrokken apparaten ontvangen met name geen nieuwe wachtwoordvereisten meer.

Meer informatie over deze instelling vindt u in [Android-apparaten verplaatsen van beheer door apparaatbeheerder naar werkprofielbeheer](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

#### <a name="the-data-warehouse-now-provides-the-mac-address---6123680----"></a>Het Data Warehouse bevat nu het MAC-adres<!-- 6123680  -->
Het Intune Data Warehouse levert het MAC-adres als een nieuwe eigenschap (`EthernetMacAddress`) in de `device`-entiteit, zodat beheerders het MAC-adres van de gebruiker kunnen relateren aan de host. Deze eigenschap is handig om specifieke gebruikers te bereiken en incidenten op te lossen die zich op het netwerk voordoen. Beheerders kunnen deze eigenschap ook gebruiken in [Power BI-rapporten](../developer/reports-proc-get-a-link-powerbi.md) om uitgebreidere rapporten te maken. Zie de [apparaat](../developer/intune-data-warehouse-collections.md#devices)-entiteit van het Intune Data Warehouse voor meer informatie.

#### <a name="additional-data-warehouse-device-inventory-properties---6125732----"></a>Aanvullende eigenschappen voor inventaris van Data Warehouse-apparaten<!-- 6125732  -->
Er zijn aanvullende eigenschappen voor de inventaris van apparaten beschikbaar met behulp van het Intune Data Warehouse. Via de bèta-verzameling [apparaten](../developer/reports-ref-devices.md#devices) zijn de volgende eigenschappen beschikbaar:
- `ethernetMacAddress` - De unieke netwerk-id van dit apparaat.
- `model` - Het apparaatmodel.
- `office365Version` - De versie van Office 365 die op het apparaat is geïnstalleerd.
- `windowsOsEdition` - De versie van het besturingssysteem.

Via de bèta-verzameling [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) zijn de volgende eigenschappen beschikbaar:
- `physicalMemoryInBytes` - Het fysieke geheugen in bytes.
- `totalStorageSpaceInBytes`: de totale opslagcapaciteit in bytes.

Zie [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md) voor meer informatie.

#### <a name="help-and-support-workflow-update-to-support-additional-services---5654170-----"></a>Update voor hulp en ondersteuning bij workflows ter ondersteuning van extra services<!-- 5654170   -->
De pagina Help en ondersteuning in het beheercentrum van Microsoft Endpoint Manager is bijgewerkt. U kunt daar nu [het beheertype kiezen dat u wilt gebruiken](../fundamentals/get-support.md#options-to-access-help-and-support). Dankzij deze wijziging kunt u de volgende beheertypen selecteren:

- Configuration Manager (bevat Desktop Analytics)
- Intune
- Co-beheer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Beveiliging

#### <a name="use-a-preview-of-security-administrator-focused-policies-as-part-of-endpoint-security--6131401----"></a>Een preview van een beleid voor beveiligingsbeheerders gebruiken als onderdeel van Endpoint Security<!--6131401  -->
Als openbare preview zijn er in het Microsoft Endpoint Management-beheercentrum meerdere nieuwe beleidsgroepen toegevoegd onder het Endpoint Security-knooppunt. Een beveiligingsbeheerder kan deze nieuwe beleidsregels gebruiken om zich te focussen op specifieke aspecten van apparaatbeveiliging, om afzonderlijke groepen gerelateerde instellingen te beheren zonder de overhead van de grotere hoofdtaak van het apparaatconfiguratiebeleid.

Met uitzondering van het nieuwe *Antivirus-beleid voor Microsoft Defender Antivirus* (zie hieronder), zijn de instellingen in deze nieuwe preview-beleidsregels en -profielen dezelfde als die u mogelijk al hebt geconfigureerd via [Apparaatconfiguratieprofielen](../configuration/device-profile-create.md).

Hieronder vindt u de nieuwe beleidstypen die allemaal in preview zijn, evenals de beschikbare profieltypen:

- **Antivirus (preview)** :
  - macOS:
    - **Antivirus**: beheer de instellingen van het [Antivirus-beleid](../protect/antivirus-microsoft-defender-settings-macos.md) voor macOS om [Microsoft Defender ATP voor Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) te beheren.

  - Windows 10 en hoger:
    - **Microsoft Defender Antivirus**: beheer de instellingen van het [Antivirus-beleid](../protect/antivirus-microsoft-defender-settings-windows.md) voor cloudbeveiliging, uitsluitingen voor Antivirus, herstel, scanopties, en meer.

      Het Antivirus-profiel voor *Microsoft Defender Antivirus* is een uitzondering waarmee een nieuw exemplaar van instellingen is geïntroduceerd. Ze vormen een onderdeel van een beperkingsprofiel voor apparaten. Deze nieuwe Antivirus-instellingen:

        - zijn dezelfde instellingen als die in de apparaatbeperkingen, maar ze ondersteunen een derde optie voor configuratie die niet beschikbaar is bij configuratie als een apparaatbeperking.
        - zijn van toepassing op apparaten die gezamenlijk worden beheerd met Configuration Manager en als de schuifregelaar [workload in co-beheer](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) voor Endpoint Protection is ingesteld op Intune.

     Plan het gebruik van het nieuwe *Antivirus-profiel van*  > *Microsoft Defender Antivirus* in plaats van het te configureren via een profiel voor apparaatbeperking.

  - **Windows Security-ervaring**: beheer welke instellingen van Windows Security eindgebruikers kunnen bekijken in het Microsoft Defender-beveiligingscentrum en welke meldingen ze ontvangen. Deze instellingen zijn niet gewijzigd ten opzichte van de instellingen die beschikbaar zijn als een Endpoint Protection-profiel voor apparaatconfiguratie.

- **Schijfversleuteling (preview)** :
  - macOS:
    - **FileVault**
  - Windows 10 en hoger:
    - **BitLocker**
- **Firewall (preview)** :
  - macOS:
    - **macOS-firewall**
  - Windows 10 en hoger:
    - **Microsoft Defender Firewall**
- **Eindpuntdetectie en -respons (preview)** :
  - Windows 10 en hoger: -**Windows 10 Intune**
- **Kwetsbaarheid voor aanvallen verminderen (preview)** :
  - Windows 10 en hoger:
    - **App- en browserisolatie**
    - **Webbeveiliging**
    - **Toepassingsbeheer**
    - **Regels voor het verminderen van kwetsbaarheid voor aanvallen**
    - **Apparaatbeheer**
    - **Exploit Protection**
- **Accountbeveiliging (preview)** :
  - Windows 10 en hoger:
    - **Accountbeveiliging**

<!-- ########################## -->
## <a name="week-of-march-9-2020"></a>Week van 9 maart 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945---"></a>Delivery Optimization-agent configureren tijdens het downloaden van inhoud voor de Win32-app<!-- 5410945 -->

U kunt de Delivery Optimization-agent configureren zodat inhoud voor de Win32-app op de achtergrond of op de voorgrond wordt gedownload op basis van de toewijzing. Voor bestaande Win32-apps wordt inhoud nog steeds op de achtergrond gedownload. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apps** > **Alle apps** >  *en selecteer de Win32-app* > **Eigenschappen**. Selecteer **Bewerken** naast **Toewijzingen**.  Bewerk de toewijzing door **Opnemen** te selecteren onder **Modus** in de sectie **Vereist**.  U vindt de nieuwe instelling in de sectie **App-instellingen**. Zie [Beheer van Win32-apps - Delivery Optimization](../apps/apps-win32-app-management.md#delivery-optimization) voor meer informatie over Delivery Optimization.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="change-primary-user-for-windows-devices---3794742-----"></a>Primaire gebruiker wijzigen voor Windows-apparaten<!-- 3794742   -->
U kunt de primaire gebruiker voor hybride Windows-apparaten en gekoppelde Azure AD-apparaten wijzigen. Ga hiervoor naar **Intune** > **Apparaten** > **Alle apparaten** > kies een apparaat > **Eigenschappen** > **Primaire gebruiker**. Zie [De hoofdgebruiker van een apparaat wijzigen](../remote-actions/find-primary-user.md#change-a-devices-primary-user) voor meer informatie.

Er is ook een nieuwe RBAC-machtiging (Beheerde apparaten/Hoofdgebruiker instellen) gemaakt voor deze taak. De machtiging is toegevoegd aan ingebouwde rollen, waaronder de Helpdeskoperator, Schoolbeheerder en Endpoint Security Manager.

Deze functie wordt als preview-versie uitgerold naar klanten wereldwijd. U kunt de functie in de komende weken tegenkomen.


<!-- ########################## -->
## <a name="week-of-march-2-2020"></a>Week van 2 maart 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions---6317104-cm3555758--"></a>Microsoft Endpoint Manager-tenant koppelen: Synchronisatie van apparaten en apparaatacties<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager brengt Configuration Manager en Intune samen in één console. Vanaf Configuration Manager Technical Preview versie 2002.2 kunt u uw Configuration Manager-apparaten uploaden naar de cloudservice en er acties op uitvoeren in het beheercentrum. Zie [Functies in Configuration Manager Technical Preview versie 2002.2](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach) voor meer informatie.

Raadpleeg het [artikel Configuration Manager Technical Preview](https://docs.microsoft.com/configmgr/core/get-started/technical-preview) voordat u deze update installeert. Dit artikel bevat een overzicht van de algemene vereisten en beperkingen voor het gebruik van een technische preview, hoe u versies bijwerkt en hoe u feedback geeft.

#### <a name="bulk-remote-actions--4576882--"></a>Externe bulkacties<!--4576882-->
U kunt nu bulkopdrachten uitgeven voor de volgende externe acties: opnieuw opstarten, naam wijzigen, Autopilot opnieuw instellen, wissen en verwijderen. Ga naar [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **Alle apparaten** > **Bulkacties** om de nieuwe bulkacties weer te geven.

#### <a name="all-devices-list-improved-search-sort-and-filter--6179023--"></a>De lijst met alle apparaten biedt verbeterde functionaliteit voor zoeken, sorteren en filteren<!--6179023-->
De lijst met alle apparaten is verbeterd voor betere prestaties en betere functionaliteit op het gebied van zoeken, sorteren en filteren. Voor meer informatie raadpleegt u [deze ondersteuningstip](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### <a name="app-management"></a>Appbeheer  
####  <a name="improved-sign-in-experience-in-company-portal-for-android"></a>Bijgewerkte aanmeldervaring voor de bedrijfsportal-app voor Android    
De indeling van diverse aanmeldingsschermen in de bedrijfsportal-app voor Android is bijgewerkt voor een modernere, eenvoudige en duidelijke ervaring voor gebruikers. Zie [Wat is er nieuw in de gebruikersinterface van de app?](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui) voor een overzicht van de verbeteringen.

<!-- ########################## -->
## <a name="week-of-february-24-2020"></a>Week van 24 februari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="macos-company-portal-user-experience-improvements---5568987---"></a>Verbeteringen in de gebruikerservaring met de Bedrijfsportal-app in macOS<!-- 5568987 -->
De ervaring met apparaatinschrijving in macOS en de Bedrijfsportal-app voor Mac is verbeterd. U ziet de volgende verbeteringen:
- Een betere Microsoft **AutoUpdate**-ervaring tijdens de inschrijving, zodat uw gebruikers over de nieuwste versie van de Bedrijfsportal beschikken.
- Een uitgebreide controlestap voor naleving tijdens de inschrijving.
- Ondersteuning voor gekopieerde incident-id's, zodat uw gebruikers sneller fouten vanaf hun apparaten kunnen verzenden naar het ondersteuningsteam van uw bedrijf.

Raadpleeg [Uw macOS-apparaat inschrijven met behulp van de Bedrijfsportal-app](../user-help/enroll-your-device-in-intune-macos-cp.md) voor meer informatie over inschrijven en de Bedrijfsportal-app voor Mac.

#### <a name="app-protection-policies-for-better-mobile-now-supports-ios-and-ipados---6224512----"></a>App-beveiligingsbeleid voor Better Mobile biedt nu ondersteuning voor iOS en iPadOS<!-- 6224512  -->

In oktober 2019 is aan het app-beveiligingsbeleid van Intune de mogelijkheid toegevoegd om gegevens van onze Microsoft Threat Defense-partners te gebruiken. Met deze update kunt u nu gebruikmaken van een app-beveiligingsbeleid om de bedrijfsgegevens van gebruikers te blokkeren of selectief te wissen, op basis van de status van een apparaat met behulp van Better Mobile op iOS en iPadOS.  Zie [App-beveiligingsbeleid voor Mobile Threat Defense maken met Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="exports-from-the-all-devices-list--now-in-zipped-csv-format--6343117--"></a>Exports uit de lijst met alle apparaten nu beschikbaar in ingepakte CSV-indeling<!--6343117-->
Exports op de pagina **Apparaten** > **Alle apparaten** zijn nu beschikbaar in ingepakte CSV-indeling.


<!-- ########################## -->
## <a name="week-of-february-17-2020-2002-service-release"></a>Week van 17 januari 2020 (servicerelease 2002)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="microsoft-defender-advanced-threat-protection-atp-app-for-macos---5424618---"></a>Microsoft Defender ATP-app (Advanced Threat Protection) voor macOS<!-- 5424618 -->
Intune biedt een eenvoudige manier om de Microsoft Defender ATP-app (Advanced Threat Protection) voor macOS te implementeren op beheerde Mac-apparaten. Zie [Microsoft Defender ATP toevoegen aan macOS-apparaten met behulp van Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) en [Microsoft Defender Advanced Threat Protection voor Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) voor meer informatie.  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="enable-network-access-control-nac-with-cisco-anyconnect-vpn-on-ios-devices---4860111----"></a>Netwerktoegangsbeheer (NAC) inschakelen met Cisco AnyConnect-VPN op iOS-apparaten<!-- 4860111  -->
Op iOS-apparaten kunt u een VPN-profiel maken en verschillende verbindingstypen gebruiken, waaronder Cisco AnyConnect (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **iOS** voor platform > **VPN** voor profieltype > **Cisco AnyConnect** voor het verbindingstype).

U kunt netwerktoegangsbeheer (NAC) inschakelen met Cisco AnyConnect. Om deze functie te gebruiken, moet u ook het volgende doen:

1. In de [beheerdershandleiding voor de Cisco Identity Services Engine](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html) volgt u de stappen in **Microsoft Intune configureren als MDM-server** om de Cisco Identity Services Engine (ISE) te configureren in Azure.
2. Selecteer in het profiel voor configuratie van Intune-apparaten de instelling **Netwerktoegangsbeheer (NAC) inschakelen**.

Ga naar [VPN-instellingen configureren op iOS-apparaten](../configuration/vpn-settings-ios.md) om de beschikbare VPN-instellingen te zien.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Apparaatinschrijving

#### <a name="serial-number-on-the-apple-mdm-push-certificate-page--5947765----"></a>Serienummer op de pagina Apple MDM-pushcertificaat<!--5947765  -->
Op de pagina Apple MDM-pushcertificaat wordt het serienummer weergegeven. Het serienummer is nodig om opnieuw toegang te krijgen tot het Apple MDM-pushcertificaat als u geen toegang meer hebt tot de Apple-id waarmee het certificaat is gemaakt. Als u het serienummer wilt zien, gaat u naar **Apparaten** > **iOS** > **iOS-inschrijving** > **Apple MDM-pushcertificaat**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="new-update-schedule-options-for-pushing-os-updates-to-enrolled-iosipados-devices--5879689----"></a>Nieuwe planningsopties voor updates om updates van het besturingssysteem te pushen naar ingeschreven iOS-/iPadOS-apparaten<!--5879689  -->
U kunt kiezen uit de volgende opties bij het plannen van updates van het besturingssysteem voor iOS-/iPadOS-apparaten. Deze opties zijn van toepassing op apparaten waarvoor het inschrijvingstype Apple Business Manager of Apple School Manager is gebruikt.
- Bijwerken wanneer de volgende keer wordt ingecheckt
- Bijwerken op gepland tijdstip
- Bijwerken buiten gepland tijdstip

Voor de laatste twee opties kunt u meerdere tijdvensters maken.

Als u de nieuwe opties wilt zien, gaat u naar MEM > **Apparaten** > **iOS** ** > Beleid voor IOS/iPadOS bijwerken** > **Profiel maken**.

#### <a name="choose-which-iosipados-updates-to-push-to-enrolled-devices--5879689----"></a>Kies welke iOS-/iPadOS-updates naar ingeschreven apparaten moeten worden gepusht<!--5879689  -->
U kunt een specifieke iOS-/iPadOS-update kiezen (behalve de meest recente update) om te pushen naar apparaten die zijn ingeschreven met Apple Business Manager of Apple School Manager. Op dergelijke apparaten moet configuratiebeleid voor apparaten zijn ingesteld om de zichtbaarheid van software-updates gedurende een aantal dagen te vertragen. Als u deze functie wilt zien, gaat u naar MEM > **Apparaten** > **iOS** ** > Beleid voor IOS/iPadOS bijwerken** > **Profiel maken**.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Apparaatbeveiliging

#### <a name="improved-intune-reporting-experience---3791418-----"></a>Verbeterde rapportagemogelijkheden van Intune<!-- 3791418   -->
Intune biedt nu verbeterde rapportagemogelijkheden, waaronder nieuwe rapporttypen, betere organisatie van rapporten, meer gerichte weergaven, verbeterde rapportfunctionaliteit, en consistente en actuele gegevens. De rapportageversie gaat van openbare preview naar GA (algemene beschikbaarheid). Daarnaast biedt de GA-release ondersteuning voor lokalisatie, oplossingen voor fouten, ontwerpverbeteringen, en samengevoegde apparaatnalevingsgegevens op tegels in het [Beheercentrum voor Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Nieuwe rapporttypen richten zich op de volgende informatie:

- **Operationeel**: bevat nieuwe records die zich richten op een negatieve status. 
- **Organisatorisch**: biedt een breder overzicht van de algemene status.
- **Historisch**: bevat patronen en trends gedurende een bepaalde periode.
- **Specialistisch**: hiermee kunt u onbewerkte gegevens gebruiken om uw eigen aangepaste rapporten te maken.

De eerste set nieuwe rapporten richt zich op de naleving van apparaten. Zie [Microsoft Intune Reporting Framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) (Rapportageframework van Microsoft Intune) en [Intune-rapporten](reports.md) voor meer informatie.

#### <a name="consolidated-the-location-of-security-baselines-in-the-ui---6177074-----"></a>De locatie van beveiligingsbasislijnen in de gebruikersinterface is geconsolideerd<!-- 6177074   -->
We hebben de paden geconsolideerd zodat u de [beveiligingsbasislijnen](../protect/security-baselines.md) kunt vinden in het beheercentrum voor Microsoft Eindpuntbeheer. Hiervoor zijn de *beveiligingsbasislijnen* van verschillende UI-locaties verwijderd. U kunt nu het volgende pad gebruiken om de beveiligingsbasislijnen te vinden:  **Eindpuntbeveiliging** > **Beveiligingsbasislijnen**.

#### <a name="expanded-support-for-imported-pkcs-certificates---6044197----"></a>Uitgebreide ondersteuning voor geïmporteerde PKCS-certificaten<!-- 6044197  -->
De ondersteuning voor het gebruik van [geïmporteerde PKCS-certificaten](../protect/certificates-imported-pfx-configure.md#supported-platforms) is uitgebreid zodat er ondersteuning wordt geboden voor *volledig beheerde Android Enterprise-apparaten*. Over het algemeen wordt het importeren van PFX-certificaten gebruikt voor S/MIME-versleutelingsscenario's, waarbij de versleutelingscertificaten van een gebruiker op al diens apparaten zijn vereist, zodat e-mails kunnen worden gedecodeerd.

De volgende platformen bieden ondersteuning voor het importeren van PFX-certificaten:

- Android - Apparaatbeheerder
- Android Enterprise - Volledig beheerd
- Android Enterprise - Werkprofiel
- iOS
- Mac
- Windows 10

#### <a name="view-the-endpoint-security-configuration-for-devices---6206460----"></a>De configuratie van eindpuntbeveiliging voor apparaten weergeven<!-- 6206460  -->
De naam van de optie in het beheercentrum voor Microsoft Eindpuntbeheer is bijgewerkt voor het weergeven van [eindpuntbeveiligingsconfiguraties die van toepassing zijn op een specifiek apparaat](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). De naam van deze optie wordt **Configuratie van eindpuntbeveiliging** omdat hierbij de toepasselijke beveiligingsbasislijnen en extra beleidsregels worden weergegeven die buiten de beveiligingsbasislijnen zijn gemaakt. Voorheen heette deze optie *Beveiligingsbasislijnen*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer

#### <a name="intune-roles-user-interface-changes-coming--5801612-----"></a>Wijzigingen in de gebruikersinterface van Intune-rollen zijn binnenkort beschikbaar<!--5801612   -->
De gebruikersinterface voor het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenantbeheer** > **Rollen** heeft nu een gebruiksvriendelijker en intuïtief ontwerp. Deze ervaring biedt dezelfde instellingen en gegevens als u nu gebruikt, maar werkt met een wizardachtige procedure.

<!-- ########################## -->
## <a name="week-of-february-17-2020"></a>Week van 17 februari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="microsofts-new-office-app---5859926---"></a>De nieuwe Office-app van Microsoft<!-- 5859926 -->
De nieuwe Office-app van Microsoft is nu algemeen beschikbaar en kan worden gedownload en gebruikt. De Office-app biedt een geconsolideerde ervaring waarbij uw gebruikers in één app in Word, Excel en PowerPoint kunnen werken. U kunt de app voorzien van een app-beveiligingsbeleid om ervoor te zorgen dat de gegevens die worden geopend, worden beveiligd.

Zie [Intune-app-beveiligingsbeleid inschakelen met de mobiele Office-app](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493) voor meer informatie.

<!-- ########################## -->

## <a name="week-of-february-10-2020"></a>Week van 10 februari 2020

### <a name="windows-7-ends-extended-support--3042987---"></a>Uitgebreide ondersteuning voor Windows 7 beëindigd<!--3042987 -->
Uitgebreide ondersteuning voor Windows 7 beëindigd op 14 januari 2020. Ondersteuning van Intune afgeschaft voor apparaten met Windows 7. Technische hulp en automatische updates die helpen bij het beschermen van uw pc zijn niet meer beschikbaar. Voer een upgrade uit naar Windows 10. Zie voor meer informatie de blogpost [Plan for Change](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="microsoft-edge-version-77-and-later-on-windows-10-devices---5843584---"></a>Microsoft Edge versie 77 of hoger op Windows 10-apparaten<!-- 5843584 -->
Intune biedt nu ondersteuning voor het verwijderen van Microsoft Edge versie 77 en hoger op Windows 10-apparaten. Raadpleeg [Microsoft Edge voor Windows 10 toevoegen aan Microsoft Intune](../apps/apps-windows-edge.md) voor meer informatie.

#### <a name="screen-removed-from-company-portal-android-work-profile-enrollment--6103987---"></a>Scherm verwijderd uit Bedrijfsportal, inschrijving van Android-werkprofiel<!--6103987 -->
Het scherm **Wat is de volgende stap?** is verwijderd uit de inschrijvingsstroom voor het Android-werkprofiel in de Bedrijfsportal om de gebruikerservaring te stroomlijnen. Ga naar [Inschrijven met Android-werkprofiel](../user-help/enroll-device-android-work-profile.md) om de bijgewerkte inschrijvingsstroom voor het Android-werkprofiel weer te geven.  

#### <a name="company-portal-app-improved-performance---6178652---"></a>Verbeterde prestaties van de Bedrijfsportal-app<!-- 6178652 -->
De Bedrijfsportal-app is bijgewerkt om de verbeterde prestaties te ondersteunen voor apparaten die gebruikmaken van ARM64-processors, zoals de Surface Pro X. Voorheen werkte de Bedrijfsportal in een geëmuleerde ARM32-modus. Nu, in versie 10.4.7080.0 en hoger, is de Bedrijfsportal-app systeemeigen gecompileerd voor ARM64. Raadpleeg [De Microsoft Intune-bedrijfsportal-app configureren](../apps/company-portal-app.md) voor meer informatie over de Bedrijfsportal-app.

## <a name="whats-new-archive"></a>Wat is er nieuw (archief)
Raadpleeg de sectie [Wat is er nieuw (archief)](whats-new-archive.md) voor eerdere maanden.

## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


