---
title: In ontwikkeling - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-functies in ontwikkeling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5562ef1eaa1cc98e3f5a654e90e4779e228768b6
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311200"
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

### <a name="improvements-to-devices-page-of-iosipados-and-macos-company-portals---6055001----"></a>Verbeteringen op de pagina Apparaten van Bedrijfsportal voor iOS/iPadOS en macOS<!-- 6055001  -->
Er zijn verschillende verbeteringen aangebracht in de gebruikerservaring van de pagina **Apparaten** van de Bedrijfsportal-app voor iOS/iPadOS en Mac. We hebben de pagina **Apparaten** pagina een modernere uitstraling gegeven en de apparaatgegevens beter georganiseerd. Door gebruik te maken van één kolom met vaste sectietitels, kunnen de iOS-iPadOS- en macOS-gebruikers van uw organisatie de status van hun apparaten gemakkelijk controleren om ervoor te zorgen dat ze veilig blijven en de toegang tot de resources van de organisatie houden. Daarnaast hebben we duidelijkere berichten en aanvullende stappen voor probleemoplossing toegevoegd voor gebruikers van wie de apparaten niet meer compatibel zijn. Zie [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md) (De Intune-bedrijfsportal-apps, Bedrijfsportal-website en Intune-app aanpassen) voor meer informatie over de Bedrijfsportal.

### <a name="improvements-to-the-company-portal-for-macos-enrollment-experience---6444452----"></a>Verbeteringen in de Bedrijfsportal voor de registratie van macOS<!-- 6444452  -->
De registratie voor macOS in de Bedrijfsportal heeft een eenvoudiger registratieproces dat meer is afgestemd op de registratie van iOS in de Bedrijfsportal. Gebruikers van het apparaat zien het volgende:  
- Een gestroomlijndere gebruikers interface.  
- Een verbeterde controlelijst voor registratie.  
- Duidelijkere instructies over het registreren van apparaten.  
- Verbeterde opties voor probleemoplossing.  

Zie [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md) (De Intune-bedrijfsportal-apps, Bedrijfsportal-website en Intune-app aanpassen) voor meer informatie over de Bedrijfsportal.

### <a name="use-autonomous-single-app-mode-settings-to-configure-the-ios-company-portal-to-be-a-sign-insign-out-app---7055619----"></a>Gebruik de instellingen voor Autonome modus voor één app om de iOS-bedrijfsportal te configureren als een app voor aanmelden/afmelden<!-- 7055619  -->
U kunt de iOS-bedrijfsportal configureren voor gebruik van de modus Autonome modus voor één app (ASAM). U kunt de ASAM-instellingen in de Microsoft Endpoint Manager-console gebruiken om de iOS-bedrijfsportal te configureren om in en uit de modus voor één app te gaan bij het afmelden en aanmelden. Wanneer ASAM is ingeschakeld voor de Bedrijfsportal, kunnen gebruikers geen andere apps of de knop Start op het apparaat gebruiken totdat ze zich aanmelden bij de Bedrijfsportal. Bij het afmelden gaat de Bedrijfsportal terug naar de modus voor één app. 

Als u de Bedrijfsportal wilt configureren voor ASAM in Microsoft Endpoint Manager, selecteert u **Apparaten** > **Configuratieprofielen** > **Profiel maken**. Selecteer **iOS-iPadOS** als platform en selecteer **Apparaatbeperkingen** als profiel. Selecteer op het tabblad **Configuratie-instellingen** de optie **Autonome modus voor één app**. Stel de **App-naam** in op `Company Portal` en stel de **App-bundel-id** in op `com.app.CompanyPortal`. Zie [Autonomous single app mode (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) (Autonome modus voor één app (ASAM)) en [single app mode](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (Modus voor één app) voor meer informatie.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Apparaatconfiguratie

### <a name="set-device-compliance-state-from-third-party-mdm-partners---6361689-----"></a>De nalevingsstatus van apparaten van externe MDM-partners instellen<!-- 6361689   -->
Binnenkort kunt u toestaan dat de nalevingsstatus van iOS- of Android-apparaten die worden beheerd door externe MDM-partners (Mobile Device Management), kan worden ingesteld in Azure Active Directory (Azure AD).

Wanneer Intune is geconfigureerd voor partnercompatibiliteit, worden de compatibiliteitsgegevens voor apparaten die worden beheerd door de externe MDM-partner verzonden naar Intune voor nalevingsbeoordeling. De resultaten worden vervolgens doorgegeven aan Azure AD, waar de compatibiliteitsgegevens worden gebruikt voor het afdwingen van uw beleid voor voorwaardelijke toegang voor die apparaten.

Er komt binnenkort ondersteuning voor de volgende partners:
- VMware WorkspaceONE (voorheen bekend als AirWatch)

Als u een nalevingspartner voor apparaten wilt inschakelen, gebruikt u een nieuw knooppunt in het beheercentrum van Microsoft Endpoint Manager: **Tenantbeheer** > **Connectors en tokens** > **Partnernalevingsbeheer** waar u **Nalevingspartner toevoegen** selecteert.

### <a name="add-a-link-to-your-company-portal-support-website-to-emails-for-noncompliance---7225498------"></a>Een link naar de ondersteuningswebsite van uw bedrijf portal toevoegen aan e-mailberichten voor niet-naleving<!-- 7225498    -->
We voegen een nieuwe instelling toe aan de sjabloon voor e-mailmeldingen waarmee de link naar de website van de bedrijfsportal wordt toegevoegd aan e-mailmeldingen die worden verzonden naar gebruikers van niet-conforme apparaten. (**Eindpuntbeveiliging** > **Apparaatnaleving** > **Meldingen** > **Melding maken**).  Gebruikers die een e-mail ontvangen als gevolg omdat ze een niet-conform apparaat hebben, kunnen de link gebruiken om een website te openen voor meer informatie over waarom het apparaat niet conform is.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>De nieuwe FileVault-instelling voor het apparaatconfiguratiebeleid voor eindpuntbeveiliging voor macOS<!-- 5459801   -->
Op de sjabloon [macOS-eindpuntbeveiliging](../protect/endpoint-protection-macos.md) wordt een nieuwe instelling aan de FileVault-categorie toegevoegd: Herstelsleutel verbergen. (**Apparaten** > **Configuratieprofielen** > **Profiel maken**, selecteer **macOS** als het *Platform* en kies vervolgens **Eindpuntbeveiliging** als het *Profieltype*). Door deze instelling wordt de persoonlijke sleutel tijdens de FileVault 2-versleuteling voor de eindgebruiker verborgen. Apparaatgebruikers kunnen hun persoonlijke herstelsleutel op elk gewenst moment weergeven via de bedrijfsportal-app voor iOS of via de bedrijfsportal-website voor het versleutelde macOS-apparaat. Ga naar Apparaatgegevens en klik op *Herstelsleutel ophalen* om de persoonlijke herstelsleutel weer te geven.

Deze instelling is niet beschikbaar in een eerder gemaakt beleid. U moet FileVault-beleidsregels opnieuw maken om deze instelling te configureren zodat u er gebruik van kunt maken. 

### <a name="configure-content-caching-on-macos-devices---7106872---"></a>Cacheopslag van inhoud op macOS-apparaten configureren<!-- 7106872 -->
Op macOS-apparaten kunt u een configuratieprofiel maken waarmee de cacheopslag van inhoud wordt geconfigureerd (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **macOS** als platform > **Apparaatfuncties** als profiel). Gebruik deze instellingen voor het verwijderen van de cache, het toestaan van een gedeelde cache, het instellen van een cachelimiet op de schijf en meer.

Zie [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (opent de website van Apple) voor meer informatie over cacheopslag van inhoud.

Ga naar [Instellingen van macOS-apparaatfuncties in Intune](../configuration/macos-device-features-settings.md) om te zien welke instellingen u momenteel kunt configureren.

Van toepassing op:
- macOS

### <a name="new-vpn-settings-for-windows-10-and-newer-devices---6602122----"></a>Nieuwe VPN-instellingen voor Windows 10-apparaten en nieuwere apparaten<!-- 6602122  -->
Wanneer u een VPN-profiel maakt met behulp van het IKEv2-verbindingstype, kunt u nieuwe instellingen configureren (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Windows 10 en hoger** als platform > **VPN** als profiel > **Basis-VPN**):

- **Apparaattunnel**: Hiermee kunnen apparaten automatisch verbinding maken met VPN zonder tussenkomst van de gebruiker, waaronder aanmelding. Voor deze functie moet u **AlwaysOn**inschakelen en **Machinecertificaten** als verificatiemethode gebruiken.
- Instellingen van Cryptography-suite: Configureer de algoritmen die worden gebruikt voor het beveiligen van IKE- en onderliggende beveiligingskoppelingen, waarmee u de client- en serverinstellingen kunt afstemmen.

Ga naar [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md) (Windows-apparaatinstellingen om VPN-verbindingen toe te voegen met Intune) voor een overzicht van de instellingen die u kunt configureren.

Van toepassing op:
- Windows 10 en nieuwer

### <a name="block-shared-ipad-temporary-sessions-on-shared-ipad-devices---6613794---"></a>Tijdelijke sessies blokkeren op gedeelde iPad-apparaten<!-- 6613794 -->
Intune heef een nieuwe instelling, **Tijdelijke sessies blokkeren op gedeelde iPad-apparaten**, die tijdelijke sessies blokkeert op gedeelde iPad-apparaten (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** als platform > **Apparaatbeperkingen** als profieltype > **Gedeelde iPad**). Wanneer deze functie is ingeschakeld, kunnen eindgebruikers het gastaccount niet gebruiken. Ze moeten zich aanmelden bij het apparaat met hun beheerde Apple-id en wachtwoord. 

Zie [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md) (iOS- en iPadOS-apparaatinstellingen om functies toe te staan of te beperken) voor meer informatie over de configureerbare instellingen.

Van toepassing op:
- Gedeelde iPad-apparaten met iOS/iPadOS 13.4 of hoger

### <a name="use-microsoft-launcher-as-the-default-launcher-for-fully-managed-android-enterprise-devices---4927976----"></a>Microsoft Launcher gebruiken als het standaard startprogramma voor volledig beheerde Android Enterprise-apparaten<!-- 4927976  -->
Op Android Enterprise-apparaten met apparaateigenaar kunt u Microsoft Launcher instellen als het standaard startprogramma voor volledig beheerde apparaten (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** als platform > **Apparaateigenaar** > **Apparaatbeperkingen** als profiel > **Apparaatervaring**). Als u alle andere instellingen van Microsoft Launcher wilt configureren, gebruikt u het configuratiebeleid voor apps. 

Er zijn ook enkele andere UI-updates, zoals dat **Toegewezen apparaten** nu **Apparaatervaring** heet.

Zie[Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md) (Met Android Enterprise-apparaatinstellingen functies toestaan of beperken met behulp van Intune) als u alle instellingen die u kunt beperken wilt bekijken. 

Van toepassing op:
- Volledig beheerde apparaten van Android Enterprise-apparaateigenaar (COBO)

### <a name="add-new-schema-settings-and-search-for-existing-schema-settings-using-oemconfig-on-android-enterprise---6394386----"></a>Nieuwe schema-instellingen toevoegen en zoeken naar bestaande schema-instellingen met behulp van OEMConfig in Android Enterprise<!-- 6394386  -->
U kunt OEMConfig in Intune gebruiken om instellingen op Android Enterprise-apparaten te beheren (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** als platform > **OEMConfig** als profiel). Wanneer u de **Configuration Designer** gebruikt, worden de eigenschappen in het app-schema weergegeven. In de **Configuration Designer** kunt u nu het volgende doen:
- Nieuwe instellingen toevoegen aan het app-schema.
- Naar nieuwe en bestaande instellingen zoeken in het app-schema.

Zie [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md) (Android Enterprise-apparaten gebruiken en beheren met OEMConfig in Microsoft Intune) voor meer informatie over OEMConfig-profielen in Intune.

Van toepassing op:
- Android Enterprise

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Apparaatinschrijving

### <a name="automated-device-enrollment-sync-errors---6988214---"></a>Synchronisatiefouten bij Automatische apparaatinschrijving<!-- 6988214 -->
Er worden nieuwe fouten gerapporteerd voor iOS/iPadOS- en macOS-apparaten, waaronder:
- Het telefoonnummer bevat ongeldige tekens of dat veld is leeg. 
- De configuratienaam voor het profiel is ongeldig of leeg. 
- Ongeldige/verlopen cursorwaarde of er is geen cursor gevonden.
- Afgewezen of verlopen token. 
- Het veld Afdeling is leeg of de lengte is te lang. 
- Het profiel is niet gevonden door Apple en er moet een nieuwe worden gemaakt. 
- Er wordt een telling van verwijderde Apple Business Manager-apparaten toegevoegd aan de overzichtspagina, waar u de status van uw apparaten kunt bekijken.

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Eigen apparaten kunnen voor het implementeren gebruikmaken van VPN<!--5015344 -->
Deze functie wordt mogelijk vertraagd.

### <a name="shared-ipads-for-business--6367326---"></a>Gedeelde iPads voor bedrijven<!--6367326 -->
U kunt Intune en Apple Business Manager gebruiken om snel en veilig Gedeelde iPad in te stellen, zodat meerdere werknemers apparaten kunnen delen. [Gedeelde iPad](https://developer.apple.com/education/shared-ipad/) van Apple biedt een persoonlijke ervaring voor meerdere gebruikers terwijl gebruikersgegevens behouden blijven. Wanneer gebruikers een beheerde Apple ID gebruiken, hebben ze toegang tot hun apps, gegevens en instellingen nadat ze zich hebben aangemeld bij een gedeelde iPad in hun organisatie. Gedeelde iPad werkt met federatieve identiteiten.

Ga naar [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **iOS** > **iOS-inschrijving** > **Registratieprogrammatokens** > kies een token > **Profielen** > **Profiel maken** > **iOS** om deze functie te zien. Selecteer op de pagina **Beheerinstellingen** de optie **Inschrijven zonder gebruikersaffiniteit** en u ziet de optie **Gedeelde iPad**.

**Van toepassing op:** iPadOS 13.4 en hoger. In deze release is ondersteuning toegevoegd voor tijdelijke sessies met Gedeelde iPad zodat gebruikers zonder een beheerde Apple ID toegang hebben tot een apparaat. Na afmelding worden alle gebruikersgegevens gewist zodat het apparaat direct gereed is voor gebruik. Het apparaat hoeft hierdoor niet meer te worden gewist. 

<!-- ***********************************************-->
## <a name="device-management"></a>Apparaatbeheer

### <a name="change-primary-user-on-co-managed-devices--7319183---"></a>Primaire gebruiker wijzigen op co-beheerde apparaten<!--7319183 -->
U kunt de primaire gebruiker van een apparaat wijzigen voor co-beheerde Windows-apparaten. Zie [Find the primary user of an Intune device](../remote-actions/find-primary-user.md) (De hoofdgebruiker van een Intune-apparaat zoeken) voor meer informatie over het zoeken en wijzigen van een gebruiker.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Ondersteuning van PowerShell-scripts voor BYOD-apparaten<!-- 1862833  -->
PowerShell-scripts bieden ondersteuning voor apparaten die bij Azure AD zijn geregistreerd in Intune. Zie [PowerShell-scripts op Windows 10-apparaten gebruiken in Intune](../apps/intune-management-extension.md) voor meer informatie over PowerShell. Deze functionaliteit biedt geen ondersteuning voor apparaten waarop de Windows 10 Home-editie wordt uitgevoerd.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bevat een logboek met apparaatgegevens<!--6014987  -->
De logboeken voor Intune-apparaatgegevens vindt u in **Rapporten** > **Logboekanalyse**. U kunt apparaatgegevens met elkaar in verband brengen om aangepaste query's en Azure-werkmappen te maken.

### <a name="setting-the-intune-primary-user-also-sets-the-azure-ad-owner-property--7319227---"></a>Als u de primaire gebruiker van Intune instelt, wordt ook de eigenschap Azure AD-eigenaar ingesteld<!--7319227 -->
Met deze nieuwe functie wordt de eigenschap Eigenaar automatisch ingesteld op de nieuw ingeschreven hybride Azure AD-gekoppelde apparaten als de primaire gebruiker van Intune wordt ingesteld. Zie [Find the primary user of an Intune device](../remote-actions/find-primary-user.md) (De hoofdgebruiker van een Intune-apparaat zoeken) voor meer informatie over de primaire gebruiker.

Dit is een wijziging in het inschrijvingsproces en is alleen van toepassing op nieuw ingeschreven apparaten. Voor bestaande hybride Azure AD-gekoppelde apparaten moet u de eigenschap Azure AD-eigenaar handmatig bijwerken. Hiervoor kunt u de functie [Primaire gebruiker wijzigen](../remote-actions/find-primary-user.md#change-a-devices-primary-user) of [een script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices) gebruiken.

Wanneer Windows 10-apparaten hybride Azure Directory-gekoppeld worden, wordt de eerste gebruiker van het apparaat de primaire gebruiker in Endpoint Manager.  Momenteel wordt de gebruiker niet ingesteld op het bijbehorende Azure AD-apparaatobject. Dit leidt tot een inconsistentie bij het vergelijken van de eigenschap *Eigenaar* van Azure AD-portal met de eigenschap *Primaire gebruiker* in het Microsoft Endpoint Manager-beheercentrum. De eigenschap Eigenaar van Azure AD wordt gebruikt voor het beveiligen van de toegang tot BitLocker-herstelsleutels. De eigenschap wordt niet ingevuld op hybride Azure AD-gekoppelde apparaten. Deze beperking voorkomt dat self-service van BitLocker-herstel vanuit Azure AD wordt ingesteld. Deze nieuwe functie lost deze beperking op.

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

### <a name="remote-lock-pin-availability-for-macos-devices--7281557--"></a>Beschikbaarheid van pincodes voor vergrendelen op afstand voor macOS-apparaten<!--7281557-->
De beschikbaarheid van de pincodes voor vergrendelen op afstand voor macOS-apparaten wordt verhoogd van 7 dagen tot 30 dagen.

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
<!--## Security-->


<!-- ***********************************************-->
## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Zie tevens

Voor meer informatie over recente ontwikkelingen raadpleegt u [Wat is er nieuw in Microsoft Intune?](whats-new.md).
