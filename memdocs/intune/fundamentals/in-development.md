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
ms.openlocfilehash: b1f261d8d61fc2c4273ae8f137a43bb6c607430d
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002695"
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

<!-- ***********************************************-->
## <a name="intune-apps"></a>Intune-apps

### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-windows-company-portal---1817861----"></a>Collectieve levering van Azure AD Enterprise- en Office Online-apps in de Windows-bedrijfsportal<!-- 1817861  -->
In de release van 2006 hebben we de [collectieve levering van Azure AD Enterprise- en Office Online-apps in de bedrijfsportal](../fundamentals/whats-new.md) aangekondigd. Deze functie wordt ondersteund in de Windows-bedrijfsportal. In het deelvenster **Aanpassing** van Intune kunt u in de Windows-bedrijfsportal **Verbergen** of **Weergeven** selecteren voor zowel **Azure AD Enterprise-apps** als voor **Office Online-apps**. Elke eindgebruiker ziet de volledige toepassingscatalogus van de gekozen Microsoft-service. Standaard wordt elke extra app-bron ingesteld op **Verbergen**. In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) selecteert u **Tenantbeheer** > **Aanpassing** om deze configuratie-instelling te vinden. Zie [De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen](../apps/company-portal-app.md) voor informatie.
 

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



<!-- ***********************************************-->
## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Zie tevens

Voor meer informatie over recente ontwikkelingen raadpleegt u [Wat is er nieuw in Microsoft Intune?](whats-new.md).
