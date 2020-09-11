---
title: In ontwikkeling - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-functies in ontwikkeling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9ec657e7d2ee83f3f4f54f9a33a5a350faa4229
ms.sourcegitcommit: 7f71d6f776df3ac28e5da3f8c926c88626483ce9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89564241"
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


<!-- ***********************************************-->
## <a name="device-configuration"></a>Apparaatconfiguratie

### <a name="create-pkcs-certificate-profiles-for-android-enterprise-fully-managed-devices-cobo---4839686---"></a>PKCS-certificaatprofielen maken voor volledig beheerde Android Enterprise-apparaten (COBO)<!-- 4839686 -->
U kunt PKCS-certificaatprofielen maken om certificaten te implementeren op apparaten met een Android Enterprise-apparaateigenaar en -werkprofiel (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise > Alleen apparaateigenaar**, of **Android Enterprise > Alleen werkprofiel** voor platform > **PKCS** voor profiel).

Binnenkort kunt u PKCS-certificaatprofielen maken voor volledig beheerde Android-apparaten. De Intune PFX-certificaatconnector is vereist. Als u niet SCEP gebruikt en alleen PKCS gebruikt, kunt u de NDES-connector verwijderen nadat u de nieuwe PFX-connector hebt geïnstalleerd. De nieuwe PFX-connector importeert PFX-bestanden en implementeert PKCS-certificaten op alle platforms.

Zie [PKCS-certificaten configureren en gebruiken met Intune](../protect/certficates-pfx-configure.md) voor meer informatie over PKCS-certificaten.

Van toepassing op:
- Android Enterprise - volledig beheerd (COBO)

### <a name="support-for-certificates-with-a-key-size-of-4096-on-ios-and-macos-devices---7659175-----"></a>Ondersteuning voor certificaten met een sleutelgrootte van 4096 op iOS- en macOS-apparaten<!-- 7659175   -->
Intune ondersteunt binnenkort het gebruik van een sleutelgrootte van 4096 bits voor SCEP-certificaatprofielen. (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > *selecteer een platform* > *Profiel* = **SCEP-certificaat**)

Ondersteuning voor 4096-bits sleutels geldt voor de volgende platforms: 
- iOS 14 en hoger
- macOS 11 en hoger    

### <a name="new-setting-for-password-complexity-for-android-10-and-later---7992114----"></a>Nieuwe instelling voor wachtwoordcomplexiteit voor Android 10 en hoger<!-- 7992114  -->
Ter ondersteuning van nieuwe opties voor Android 10 en hoger voegen we een nieuwe instelling toe met de naam **Wachtwoordcomplexiteit** aan zowel het beleid voor *apparaatnaleving* als het beleid voor *apparaatbeperking*. (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Apparaatbeperkingen** en  **Apparaten** > **Nalevingsbeleid** > **Beleid maken**) Met deze instelling kunt u de mate van de wachtwoordsterkte beheren, waarbij rekening wordt gehouden met het type, de lengte en de kwaliteit van het wachtwoord. 

De volgende complexiteitsniveaus worden ondersteund:
- **Geen**: geen wachtwoord
- **Laag**: het wachtwoord voldoet aan een van de volgende eigenschappen:
  - Patroon
  - Pincode met een herhalende reeks (4444) of reeks met bepaalde volgorde (1234, 4321, 2468)
- **Gemiddeld**: het wachtwoord voldoet aan een van de volgende eigenschappen:
  - Pincode zonder een herhalende reeks (4444) of reeks met bepaalde volgorde (1234, 4321, 2468), lengte van minimaal vier tekens
  - Alfabetisch, lengte van minimaal vier tekens
  - Alfanumeriek, lengte van minimaal vier tekens
- **Hoog**: het wachtwoord voldoet aan een van de volgende eigenschappen:
  - Pincode zonder een herhalende reeks (4444) of reeks met bepaalde volgorde (1234, 4321, 2468), lengte van minimaal acht tekens
  - Alfabetisch, lengte van minimaal zes tekens
  - Alfanumeriek, lengte van minimaal zes tekens

Wachtwoordcomplexiteit is niet van toepassing op Samsung Knox-apparaten met Android 10 of hoger. Op deze apparaten wordt de wachtwoordcomplexiteit overschreven door de instellingen voor wachtwoordlengte en/of wachtwoordtype.

### <a name="cope-preview-update-new-settings-to-create-requirements-for-the-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile--7088355---"></a>Update van COPE-preview: Nieuwe instellingen voor het maken van vereisten voor het werkprofielwachtwoord voor Android Enterprise-apparaten in bedrijfseigendom met een werkprofiel<!--7088355 -->
Toekomstige instellingen bieden beheerders de mogelijkheid om vereisten in te stellen voor het werkprofielwachtwoord voor Android Enterprise-apparaten in bedrijfseigendom met een werkprofiel.  (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** voor platform > **Volledig beheerd en toegewezen werkprofiel in bedrijfseigendom** >  **Apparaatbeperkingen** voor profiel > **Werkprofielwachtwoord**):

- Vereist wachtwoordtype
- Minimale wachtwoordlengte
- Het aantal dagen totdat het wachtwoord verloopt
- Het vereiste aantal wachtwoorden voordat de gebruiker een wachtwoord opnieuw kan gebruiken
- Aantal mislukte aanmeldingen voordat een apparaat wordt gewist


### <a name="new-settings-using-per-app-vpn-or-on-demand-vpn-on-iosipados-and-macos-devices---7758772-7758837-7758886----"></a>Nieuwe instellingen bij gebruik van VPN per app of on-demand VPN op iOS-/iPadOS- en macOS-apparaten<!-- 7758772 7758837 7758886  -->
- **Voorkomen dat gebruikers automatische VPN uitschakelen**: Bij het maken van een automatische verbinding voor **VPN per app** of **on-demand VPN** kunt u gebruikers verplichten om de automatische VPN-verbinding ingeschakeld en actief te laten.
- **Gekoppelde domeinen**: Wanneer u een automatische verbinding voor **VPN per app** maakt, kunt u de gekoppelde domeinen in het VPN-profiel opgeven waarmee de VPN-verbinding automatisch wordt gestart. 
- **Uitgesloten domeinen**: Wanneer u een automatische verbinding voor **VPN per app** maakt, kunt u een lijst met domeinen maken die de VPN-verbinding kunnen omzeilen wanneer VPN per app wordt verbonden.

U kunt automatische VPN-profielen configureren in **Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** of **macOS** voor platform > **VPN** voor profiel > **Automatische VPN**.

Zie [Gekoppelde domeinen](../configuration/device-features-configure.md#associated-domains) voor meer informatie over gekoppelde domeinen.

Zie [VPN per app instellen voor iOS/iPadOS-apparaten](../configuration/vpn-setting-configure-per-app.md#create-a-per-app-vpn-profile) om de instellingen te bekijken die u kunt instellen.

Van toepassing op:
- iOS/iPadOS 14 en hoger
- macOS Big Sur (macOS 11)

### <a name="cope-preview-update-new-settings-to-configure-the-personal-profile-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7086356----"></a>Update van COPE-preview: Nieuwe instellingen voor het configureren van het persoonlijke profiel voor Android Enterprise-apparaten in bedrijfseigendom met een werkprofiel<!-- 7086356  -->
Voor Android Enterprise-apparaten in bedrijfseigendom met een werkprofiel kunnen er nieuwe instellingen worden geconfigureerd die alleen van toepassing zijn op het persoonlijke profiel (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** voor platform > **Volledig beheerd en toegewezen werkprofiel in bedrijfseigendom** >  **Apparaatbeperkingen** voor profiel > **Persoonlijk profiel**):

- **Camera**: Gebruik deze instelling om de toegang tot de camera te blokkeren tijdens persoonlijk gebruik.
- **Schermopname**: Gebruik deze instelling om schermopnamen te blokkeren tijdens persoonlijk gebruik.
- **Gebruikers toestaan om apps uit onbekende bronnen te installeren in het persoonlijke profiel**: Gebruik deze instelling om gebruikers toe te staan om apps uit onbekende bronnen te installeren in het persoonlijke profiel. 

Ga naar [Android Enterprise-apparaatinstellingen voor het toestaan of beperken van functies](../configuration/device-restrictions-android-for-work.md) om de huidige instellingen te bekijken die u kunt configureren.

### <a name="block-app-clips-on-iosipados-and-defer-non-os-software-updates-on-macos-devices---7518422----"></a>App-fragmenten in iOS/iPadOS blokkeren en andere updates dan besturingssysteemsoftware-updates uitstellen op macOS-apparaten<!-- 7518422  -->
Wanneer u een beperkingsprofiel voor apparaten maakt op iOS-/iPadOS- en macOS-apparaten, zijn er enkele nieuwe instellingen:

**App-fragmenten blokkeren in iOS/iPadOS 14.0 en hoger**
- Is van toepassing op iOS/iPadOS 14.0 en hoger.
- Apparaten moeten worden ingeschreven met apparaatinschrijving of geautomatiseerde apparaatinschrijving (apparaten onder supervisie).
- Met de instelling **App-fragmenten blokkeren** blokkeert u app-fragmenten op beheerde apparaten (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatbeperkingen** voor profiel > **Algemeen**). Wanneer deze functie wordt geblokkeerd, kunnen gebruikers geen app-fragmenten toevoegen en worden bestaande app-fragmenten van het apparaat verwijderd.  

**Software-updates uitstellen voor macOS 11 en hoger**
- Is van toepassing op macOS 11 en hoger. Op macOS-apparaten onder supervisie moet de apparaatinschrijving voor het apparaat door de gebruiker zijn goedgekeurd of moet het apparaat zijn ingeschreven via automatische apparaatinschrijving.
- Met de instelling **Software-updates uitstellen** wordt de weergave van andere updates dan besturingssysteemsoftware-updates voor gebruikers uitgesteld (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **macOS** voor platform > **Apparaatbeperkingen** voor profiel > **Algemeen**). Als u deze updates uitstelt, worden onlangs uitgebrachte updates pas voor gebruikers weergegeven na de uitstelperiode die is geconfigureerd met behulp van de instellingen voor **Weergave van software-updates uitstellen**. Het uitstellen van andere updates dan besturingssysteemsoftware-updates heeft geen invloed op geplande updates.
- De bestaande instelling voor **Software-updates uitstellen** wordt gecombineerd met deze nieuwe instelling. Met de nieuwe instelling kunt u besturingssysteemsoftware-updates en andere updates dan besturingssysteemsoftware-updates uitstellen. U blijft de instelling **Weergave van software-updates uitstellen** gebruiken om het aantal dagen in te stellen dat van toepassing is op beide instellingen voor het uitstellen van software-updates.
- Het gedrag van bestaande beleidsregels wordt niet gewijzigd, beïnvloed of verwijderd. Bestaande beleidsregels worden automatisch naar de nieuwe instelling gemigreerd met dezelfde configuratie.

### <a name="disable-mac-address-randomization-on-wi-fi-networks-on-iosipados-devices---7758689----"></a>Willekeurige MAC-adressen uitschakelen in Wi-Fi-netwerken op iOS- en iPadOS-apparaten<!-- 7758689  -->
Vanaf iOS/iPadOS 14 wordt voor apparaten standaard een willekeurig MAC-adres weergegeven in plaats van het fysieke MAC-adres wanneer u verbinding maakt met een netwerk. Dit gedrag wordt aanbevolen voor privacy, omdat het moeilijker is om een apparaat te traceren op basis van het MAC-adres. Deze functie breekt ook met de functionaliteit die afhankelijk is van een statisch MAC-adres, waaronder netwerktoegangsbeheer. 

U kunt willekeurige MAC-adressen per netwerk uitschakelen in Wi-Fi-profielen (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Wi-Fi** voor profiel > **Basic** of **Enterprise** voor Wi-Fi-type).

Ga naar [Wi-Fi-instellingen voor iOS- en iPadOS-apparaten toevoegen](../configuration/wi-fi-settings-ios.md) voor een overzicht van de instellingen die u momenteel kunt configureren.

Van toepassing op:
- iOS/iPadOS 14 en hoger

### <a name="set-maximum-transmission-unit-for-ikev2-vpn-connections-on-iosipados-devices---7758937----"></a>Maximale verzendeenheid instellen voor IKEv2 VPN-verbindingen op iOS- en iPadOS-apparaten<!-- 7758937  -->
Voor apparaten met iOS/iPadOS 14 en hoger kunt u een aangepaste maximale verzendeenheid (MTU) configureren wanneer u gebruikmaakt van IKEv2 VPN-verbindingen (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **VPN** voor profiel -> IKEv2 voor het verbindingstype).

Zie [IKEv2-instellingen](../configuration/vpn-settings-ios.md#ikev2-settings) voor meer informatie over de instellingen die u kunt configureren.

Van toepassing op:
- iOS/iPadOS 14 en hoger

### <a name="per-account-vpn-connection-for-email-profiles-on-iosipados-devices---7759116----"></a>VPN-verbinding per account voor e-mailprofielen op iOS- en iPadOS-apparaten<!-- 7759116  -->
Vanaf iOS/iPadOS 14 kan het e-mailverkeer voor de systeemeigen e-mail-app via een VPN worden doorgestuurd op basis van het account dat de gebruiker gebruikt. U kunt nu een VPN-profiel per app opgeven dat moet worden gebruikt voor deze VPN-verbinding die is gebaseerd op een account.  De VPN-verbinding per app wordt automatisch ingeschakeld wanneer gebruikers hun organisatieaccount in de e-mail-app gebruiken.

Ga naar [Instellingen voor e-mail voor iOS- en iPadOS-apparaten toevoegen](../configuration/email-settings-ios.md) voor een overzicht van de instellingen die u momenteel kunt configureren.

Van toepassing op:
- iOS/iPadOS 14 en hoger

### <a name="use-netmotion-as-a-vpn-connection-type-for-android-enterprise-work-profile-devices---7764263---"></a>Net\Motion gebruiken als een VPN-verbindingstype voor Android Enterprise-werkprofielapparaten<!-- 7764263 -->
Wanneer u een VPN-profiel maakt, is NetMotion beschikbaar als een VPN-verbindingstype (**Apparaten** > **Apparaatconfiguratie** > **Profiel maken** > **Android Enterprise-werkprofiel** voor platform > **VPN** voor profiel > **NetMotion** voor verbindingstype).

Zie [VPN-profielen maken om verbinding te maken met VPN-servers](../configuration/vpn-settings-configure.md) voor meer informatie over VPN-profielen in Intune.

Van toepassing op:
- Android Enterprise - Werkprofiel

### <a name="changes-for-password-settings-in-device-restriction-profiles-for-android-device-administrator---7662279----"></a>Wijzigingen voor wachtwoordinstellingen in apparaatbeperkingsprofielen voor Android-apparaatbeheerder<!-- 7662279  --> 
Er wordt een aantal wijzigingen voor wachtwoordinstellingen geïntroduceerd voor het beleid voor *apparaatbeperking* en *naleving* voor de *Android-apparaatbeheerder*. (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Apparaatbeperkingen** en **Apparaten** > **Nalevingsbeleid** > **Beleid maken**) Deze wijzigingen zorgen ervoor dat Intune wordt aangepast aan de wijzigingen in Android versie 10 en hoger, zodat de instellingen voor wachtwoorden op de gebruikelijke wijzen blijven gelden voor apparaten.
 
De wijzigingen zijn onder andere:
- Verwijdering van de optie op het hoogste niveau voor **Wachtwoord**.  
- Instellingen worden opnieuw ingedeeld in secties die zijn gebaseerd op de apparaten waarop ze van toepassing zijn.
- De **Minimale wachtwoordlengte** wordt uitgeschakeld voor gebruik, tenzij **Wachtwoordtype** is geconfigureerd met een waarde waarvoor de wachtwoordlengte van toepassing is.
- Aanvullende updates voor labels en voorbeeldtekst.

Deze wijzigingen zijn van toepassing op de gebruikersinterface voor instellingen en hebben geen invloed op bestaande profielen. 

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Apparaatinschrijving

### <a name="ending-support-for-ios-11--7327321---"></a>Ondersteuning voor iOS 11 wordt beëindigd<!--7327321 -->
Na het uitbrengen van iOS 14 bieden de Intune-inschrijving en bedrijfsportal-app ondersteuning voor iOS-versies 12 en hoger. Oudere versies worden niet ondersteund, maar blijven beleidsregels ontvangen.

### <a name="ending-support-for-macos-1012--7327326---"></a>Ondersteuning voor macOS 10.12 wordt beëindigd<!--7327326 -->
Na het uitbrengen van macOS 11 bieden de Intune-inschrijving en bedrijfsportal ondersteuning voor macOS-versies 10.13 en hoger. Oudere versies worden niet ondersteund.


<!-- ***********************************************-->
## <a name="device-management"></a>Apparaatbeheer

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Ondersteuning van PowerShell-scripts voor BYOD-apparaten<!-- 1862833  -->
PowerShell-scripts bieden ondersteuning voor apparaten die bij Azure AD zijn geregistreerd in Intune. Zie [PowerShell-scripts op Windows 10-apparaten gebruiken in Intune](../apps/intune-management-extension.md) voor meer informatie over PowerShell. Deze functionaliteit biedt geen ondersteuning voor apparaten waarop de Windows 10 Home-editie wordt uitgevoerd.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bevat een logboek met apparaatgegevens<!--6014987  -->
De logboeken voor Intune-apparaatgegevens vindt u in **Rapporten** > **Logboekanalyse**. U kunt apparaatgegevens met elkaar in verband brengen om aangepaste query's en Azure-werkmappen te maken.

### <a name="tenant-attach-run-scripts-from-the-admin-center--7220536-cm6234688---"></a>Tenantkoppeling: Scripts uitvoeren vanuit het beheercentrum<!--7220536, CM6234688 -->
U kunt de krachtige on-premises functie [Scripts uitvoeren](../../configmgr/apps/deploy-use/create-deploy-scripts.md) van Configuration Manager in het Microsoft Endpoint Manager-beheercentrum gebruiken. Sta extra persona's, zoals Helpdesk, toe om PowerShell-scripts vanuit de cloud uit te voeren met een individueel door Configuration Manager beheerd apparaat. Hiermee krijgt u alle bekende voordelen van PowerShell-scripts die al zijn gedefinieerd en goedgekeurd door de Configuration Manager-beheerder voor deze nieuwe omgeving. Zie [Configuration Manager Technical Preview 2005](../../configmgr/core/get-started/2020/technical-preview-2005.md#bkmk_scripts) voor meer informatie. 

### <a name="deploy-software-updates-to-macos-devices----3194876---"></a>Software-updates implementeren op macOS-apparaten <!-- 3194876 -->
U kunt software-updates implementeren voor groepen macOS-apparaten. Deze functie omvat essentiële updates, firmware-updates, configuratiebestanden en andere updates. U kunt updates verzenden de volgende keer dat het apparaat wordt ingecheckt, of een wekelijkse planning selecteren om updates te implementeren binnen of buiten tijdvensters die u instelt. Dit is handig als u apparaten wilt bijwerken buiten standaardwerkuren of wanneer de helpdesk werkt met een volledige bezetting. U krijgt ook een gedetailleerd rapport met alle macOS-apparaten waarop updates zijn geïmplementeerd. U kunt de rapportgegevens filteren per apparaat, om de status van bepaalde updates te bekijken.

### <a name="cope-preview-update-reset-work-profile-password-for-android-enterprise-corporate-owned-devices-with-a-work-profile---7217228---"></a>Update van COPE-preview: Het werkprofielwachtwoord opnieuw instellen voor Android Enterprise-apparaten in bedrijfseigendom met een werkprofiel <!--7217228 -->
Met een toekomstige beheerdersactie kunnen beheerders het werkprofielwachtwoord voor Android Enterprise-apparaten in bedrijfseigendom met een werkprofiel opnieuw instellen.

### <a name="rename-a-co-managed-device-that-is-azure-active-directory-joined--7728043---"></a>De naam wijzigen van een gezamenlijk beheerd apparaat dat is toegevoegd aan Azure Active Directory<!--7728043 -->
U kunt de naam wijzigen van een gezamenlijk beheerd apparaat dat is toegevoegd aan Azure AD. Als u dit wilt doen, gaat u naar **Apparaten** > **Alle apparaten** > kies een apparaat > **...**  > **Naam van apparaat wijzigen**.

### <a name="support-for-powerprecision-and-powerprecision-batteries-for-zebra-devices--3724987---"></a>Ondersteuning voor PowerPrecision- en PowerPrecision+-batterijen voor Zebra-apparaten<!--3724987 -->
Op de pagina met hardwaregegevens van een apparaat wordt de volgende informatie weergegeven over Zebra-apparaten die gebruikmaken van PowerPrecision- en PowerPrecision+-batterijen:
- Beoordeling van de status zoals deze is bepaald door Zebra (alleen PowerPrecision+-batterijen)
- Aantal verbruikte cycli voor een volledige lading
- De datum van de laatste check-in voor de batterij die het laatst in het apparaat is gevonden
- Serienummer van de oplaadbare batterij die het laatst in het apparaat is gevonden

<!-- ***********************************************-->
## <a name="intune-apps"></a>Intune-apps

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Collectieve levering van Azure AD Enterprise- en Office Online-apps in de Windows-bedrijfsportal<!-- 1817861  -->
In de release van 2006 hebben we de [collectieve levering van Azure AD Enterprise- en Office Online-apps in de bedrijfsportal](../fundamentals/whats-new.md#unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal) aangekondigd. Deze functie wordt ondersteund in de Windows-bedrijfsportal. In het deelvenster **Aanpassing** van Intune kunt u in de Windows-bedrijfsportal **Verbergen** of **Weergeven** selecteren voor zowel **Azure AD Enterprise-apps** als voor **Office Online-apps**. Elke eindgebruiker ziet de volledige toepassingscatalogus van de gekozen Microsoft-service. Standaard wordt elke extra app-bron ingesteld op **Verbergen**. In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) selecteert u **Tenantbeheer** > **Aanpassing** om deze configuratie-instelling te vinden. Zie [De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen](../apps/company-portal-app.md) voor informatie.
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
## <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

### <a name="power-bi-compliance-report-template-v20---636958----"></a>Sjabloon voor Power BI-nalevingsrapport BI V 2.0<!-- 636958  -->
Beheerders kunnen de sjabloonversie van het Power BI-compatibiliteitsrapport bijwerken van V 1.0 naar V 2.0. V 2.0 bevat een verbeterd ontwerp, evenals wijzigingen in de berekeningen en gegevens die worden opgehaald als onderdeel van de sjabloon. Zie [Verbinding maken met het datawarehouse met Power BI](../developer/reports-proc-get-a-link-powerbi.md) voor gerelateerde informatie.


### <a name="new-and-improved-microsoft-defender-antivirus-reporting-for-windows-10-and-newer---6018169----"></a>Nieuwe en verbeterde Microsoft Defender Antivirus-rapportage voor Windows 10 en hoger<!-- 6018169  -->
We voegen vier nieuwe rapporten toe aan Microsoft Defender Antivirus in Windows 10, onder **Eindpuntbeveiliging** > **Antivirus**.
- Twee operationele rapporten: *Apparaten met gedetecteerde malware* en *Agentstatus*.
- Twee organisatierapporten: *Gedetecteerde malware* en *Agentstatus*.

In het operationele rapport *Agentstatus* kunt u bijvoorbeeld in één oogopslag de apparaatnaam, gebruikersnaam, het e-mailadres en de UPN van de gebruiker bekijken en zien of realtime beveiliging en netwerkbeveiliging zijn ingeschakeld. Wanneer deze rapporten beschikbaar zijn voor gebruik wordt meer informatie verstrekt.

Zie [Eindpuntbeveiliging beheren in Microsoft Intune](../protect/endpoint-security.md) voor meer informatie over eindpuntbeveiliging in Microsoft Intune.

### <a name="analyze-your-on-premises-gpos-using-group-policy-analytics-preview--7200950---"></a>Uw on-premises groepsbeleidsobjecten analyseren met groepsbeleidsanalyse (preview)<!--7200950 -->
In **Apparaten** > **Groepsbeleidsanalyse (preview)** kunt u uw groepsbeleidsobjecten (GPO's) importeren in het beheercentrum van Microsoft Endpoint Manager. Wanneer u het groepsbeleidsobject importeert, analyseert Intune dit automatisch en geeft het de beleidsregels weer die equivalente instellingen hebben in Intune. Het geeft ook groepsbeleidsobjecten weer die zijn afgeschaft of niet meer worden ondersteund.

Van toepassing op:
- Windows 10 en nieuwer

#### <a name="new-windows-10-feature-update-report---6473128----"></a>Nieuw rapport met functie-updates voor Windows 10<!-- 6473128  -->
Het rapport **Functie-updates voor Windows** bevat een algemeen overzicht van de naleving voor apparaten waarvoor het beleid **Functie-updates voor Windows 10** geldt. In het [beheercentrum van Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selecteert u **Rapporten** > **Windows-updates (preview)**  > **Fouten bij functie-updates** om de samenvatting voor dit rapport weer te geven. Als u rapporten voor specifieke beleidsregels wilt weergeven, selecteert u het tabblad **Rapporten** en opent u het **rapport Functie-updates voor Windows**. 

#### <a name="new-windows-10-feature-failures-update-report---6473121-----"></a>Nieuw updaterapport met functieproblemen voor Windows 10<!-- 6473121   -->
Het rapport **Fouten bij functie-updates** bevat foutgegevens voor apparaten waarvoor een beleid voor **functie-updates voor Windows 10** geldt en waarvoor is geprobeerd om een update uit te voeren. In het [beheercentrum van Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) selecteert u **Apparaten** > **Controleren** > **Fouten bij functie-updates** om dit rapport weer te geven."

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

### <a name="improved-certificate-deployment-for-android-enterprise----6296499----"></a>Verbeterde implementatie van certificaten voor Android Enterprise <!-- 6296499  -->
Apparaten met Android Enterprise-werkprofielen in bedrijfseigendom die volledig worden beheerd en zijn toegewezen, kunnen binnenkort gebruikmaken van S/MIME-certificaten voor Outlook zonder dat de gebruiker van een apparaat toegang moet toestaan. S/MIME-certificaten worden geïmplementeerd met behulp van een geïmporteerd PKCS-certificaatprofiel voor apparaatconfiguratie. (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** > **Geïmporteerd PKCS-certificaat** uit de categorie voor *Volledig beheerd en toegewezen werkprofiel in bedrijfseigendom*).

### <a name="tri-state-options-for-settings-are-coming-to-endpoint-security-firewall-policy---6586159-----"></a>Instellingen met drie statusopties zijn beschikbaar voor Endpoint Security Firewall-beleid<!-- 6586159   -->
Er wordt een derde configuratiestatus toegevoegd voor instellingen in het Endpoint Security Firewall-beleid, waar het platform (Windows of macOS) ondersteuning kan bieden voor de extra optie (**Endpoint Security** > **Firewall**).

Waar voor een instelling momenteel bijvoorbeeld **Niet geconfigureerd** en **Ja** kan worden gekozen, wordt de optie **Nee** toegevoegd, als deze wordt ondersteund door het platform.

### <a name="new-security-baseline-for-office---3150261----"></a>Nieuwe beveiligingsbasislijn voor Office<!-- 3150261  -->
Er wordt een nieuwe beveiligingsbasislijn toegevoegd (**Eindpuntbeveiliging** > **Beveiligingsbasislijnen**) om de instellingen voor *Microsoft Office O365* te beheren. De instellingen in de basislijn bevatten configuraties voor Office-apps, zoals *Beheer van invoegtoepassingen*, *MIME-verwerking*, enzovoort.

### <a name="improved-status-details-in-security-baseline-reports---7221051------"></a>Verbeterde statusgegevens in beveiligingsbasislijnrapporten<!-- 7221051    -->
We verbeteren de statusgegevens die worden weergegeven wanneer u de resultaten van uw geïmplementeerde beveiligingsbasislijnen bekijkt. (**Eindpuntbeveiliging** > **Beveiligingsbasislijnen** >  *selecteer een type beveiligingsbasislijn, zoals* **Windows 10-beveiligingsbasislijnen** > **Profielen** > *selecteer een instantie van dat profiel om de status weer te geven* > *selecteer een profielrapport, zoals* **Apparaatstatus**)

Met de verbeteringen worden de veelvoorkomende labels en definities die we gebruiken voor de status aangepast, zodat deze beter passen bij de bedoeling van de status. Bijvoorbeeld:
- **Komt overeen met de basislijn** wordt bijgewerkt naar **Komt overeen met de standaardinstellingen**, wat een betere omschrijving geeft van de bedoeling om vast te stellen wanneer de configuratie van een apparaat overeenkomt met de standaardbasislijnconfiguratie (ongewijzigd).
- **Onjuist geconfigureerd** wordt opgedeeld in meer specifieke details, zoals **Fout**, **Conflict** en **In behandeling**. De nieuwe statussen zorgen voor consistentie in andere onderdelen van de console.

### <a name="expanded-rbac-permissions-for-the-endpoint-security-role--7312374--idstaged---"></a>Uitgebreide RBAC-machtigingen voor de rol eindpuntbeveiliging<!--7312374  idstaged -->
De rol **Endpoint Security Manager** voor Intune ontvangt aanvullende RBAC-machtigingen (op rollen gebaseerd toegangsbeheer) voor externe taken. Deze rol verleent toegang tot het beheercentrum van Microsoft Endpoint Manager en kan worden gebruikt door personen die de beveiligings- en nalevingsfuncties beheren, met inbegrip van de beveiligingsbasislijnen, apparaatnaleving, voorwaardelijke toegang en Microsoft Defender Advanced Threat Protection.

Als u de machtiging voor een Intune RBAC-rol wilt weergeven, gaat u naar (**Tenantbeheerder** > **Intune-rollen** > *selecteert u een rol* > **Machtigingen**).

Voorbeelden van uitgebreide machtigingen voor externe taken zijn:

- Nu opnieuw opstarten
- Vergrendelen op afstand
- BitLockerKeys rouleren (preview)
- FileVault-sleutel roteren
- Apparaten synchroniseren
- Microsoft Defender
- Een Configuration Manager-actie starten

### <a name="updates-for-security-baselines---7102146-7103916----"></a>Updates voor beveiligingsbasislijnen<!-- 7102146, 7103916  -->
Er worden binnenkort updates uitgebracht voor de volgende beveiligingsbasislijnen (**Eindpuntbeveiliging** > **Beveiligingsbasislijnen**):
- **MDM-beveiligingsbasislijn** (Windows 10 Security)
- **Microsoft Defender ATP-basislijn**

Bijgewerkte basislijnversies bieden ondersteuning voor recente instellingen zodat u de configuraties die worden aanbevolen door de betreffende productteams beter kunt onderhouden.

### <a name="use-endpoint-security-configuration-details-to-identify-the-source-of-policy-conflicts-for-devices---7567503--idstaged----"></a>Aan de hand van eindpuntbeveiligingsconfiguratiegegevens vaststellen wat de bron van beleidsconflicten voor apparaten is<!-- 7567503  idstaged  -->
Ter ondersteuning van de conflictoplossing kunt u binnenkort inzoomen via een beveiligingsbasislijnprofiel om de *eindpuntbeveiligingsconfiguratie* voor een geselecteerd apparaat weer te geven. Hierin kunt u instellingen selecteren die een *conflict* of *fout* weergeven en verdergaan met Inzoomen om een lijst met details te bekijken die de profielen en het beleid bevat die deel uitmaken van het conflict. Als u vervolgens een beleid selecteert dat een conflict veroorzaakt, opent Intune het deelvenster Overzicht voor dat beleid waarin u de beleidsconfiguratie kunt controleren of wijzigen. (**Apparaten** > *selecteer een apparaat* > **Eindpuntbeveiligingsconfiguratie** > *selecteer een profiel of basislijn* > *Een instelling selecteren in de lijst met instellingen die op het apparaat worden toegepast*).

De volgende beleidstypen kunnen als bron van een conflict worden vastgesteld wanneer u inzoomt via een beveiligingsbasislijn:
- Apparaatconfiguratiebeleid
- Eindpuntbeveiligingsbeleid

### <a name="new-details-in-the-endpoint-security-configuration-for-a-device---7745029-----"></a>Nieuwe details in de eindpuntbeveiligingsconfiguratie voor een apparaat<!-- 7745029   -->
Er worden nieuwe details toegevoegd voor apparaten die kunnen worden weergegeven als onderdeel van de eindpuntbeveiligingsconfiguratie voor apparaten. (**Eindpuntbeveiliging** > **Beveiligingsbasislijnen** > *geselecteerde basislijn* > **Profielen** > *geselecteerd profiel* > **Apparaatstatus** > **Eindpuntbeveiligingsconfiguratie**). De nieuwe details:

- **UPN** (principalnaam van gebruiker): De UPN geeft aan welk eindpuntbeveiligingsprofiel wordt toegewezen aan een bepaalde gebruiker op het apparaat. Dit is nuttig om onderscheid te maken tussen meerdere gebruikers op een apparaat en meerdere vermeldingen van een profiel dat of een basislijn die is toegewezen aan het apparaat. 
- **Slechtste status**: Dit detail geeft de ongunstigste statusvoorwaarde voor het apparaat aan. Als deze status de waarde **Geslaagd** heeft, heeft het apparaat geen beleidsconflicten of fouten.

### <a name="android-11-deprecates-deployment-of-trusted-root-certificates-to-device-administrator-enrolled-devices--7662775----"></a>Met Android 11 wordt de implementatie van vertrouwde basiscertificaten op apparaten die zijn ingeschreven door apparaatbeheerders afgeschaft<!--7662775  -->
In Android 11 kunnen vertrouwde basiscertificaten niet meer worden geïmplementeerd op apparaten die zijn Ingeschreven als *Android-apparaatbeheerder*. Deze wijziging is niet van invloed op Samsung Knox-apparaten vanwege de integratie van Intune met het Knox-platform. Voor andere apparaten dan Samsung-apparaten moeten gebruikers het vertrouwde basiscertificaat handmatig op het apparaat installeren. 

Wanneer het vertrouwde basiscertificaat handmatig op een apparaat is geïnstalleerd, kunt u SCEP gebruiken om certificaten in te richten op het apparaat. In dit scenario moet u nog steeds een beleid voor *vertrouwde certificaten* maken en implementeren op het apparaat en dat beleid koppelen aan het *SCEP-certificaat*profiel.

- Als het vertrouwde basiscertificaat op het apparaat staat, wordt het SCEP-certificaatprofiel geïnstalleerd. 
- Als het vertrouwde certificaat niet wordt gevonden, mislukt het SCEP-certificaatprofiel.

<!-- ***********************************************-->
## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Zie tevens

Voor meer informatie over recente ontwikkelingen raadpleegt u [Wat is er nieuw in Microsoft Intune?](whats-new.md).
