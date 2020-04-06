---
title: In ontwikkeling - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-functies in ontwikkeling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a807a90cdca18d79e7b92b4efeb56d341da2596
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438722"
---
# <a name="in-development-for-microsoft-intune---april-2020"></a>In ontwikkeling voor Microsoft Intune - april 2020

Als hulp bij uw gereedheid en planning worden op deze pagina updates voor en functies van de Intune-gebruikersinterface vermeld die in ontwikkeling zijn, maar nog niet zijn uitgebracht. Naast de informatie op deze pagina geldt het volgende: 

- Als we verwachten dat u actie moet ondernemen vóór een wijziging, publiceren we een aanvullend bericht in het Office-berichtencentrum.
- Als een functie in productie gaat, of het nu gaat om een preview of algemene beschikbaarheid, wordt de functiebeschrijving verplaatst van deze pagina naar [Nieuwe functies](whats-new.md).
- Deze pagina en de pagina [Nieuwe functies](whats-new.md) worden regelmatig bijgewerkt. Controleer op andere updates.
- Raadpleeg de [Microsoft 365-roadmap](https://www.microsoft.com/microsoft-365/roadmap?rtc=2&filters=EMS) voor strategische producten en tijdlijnen.

> [!NOTE]
> Deze pagina bevat onze huidige verwachtingen over Intune-mogelijkheden in een toekomstige release. Datums en afzonderlijke functies kunnen worden gewijzigd. Op deze pagina worden niet alle functies in ontwikkeling beschreven.

**RSS-feed**: U ziet wanneer deze pagina wordt bijgewerkt door de volgende URL in uw feedlezer te kopiëren en plakken: `https://docs.microsoft.com/api/search/rss?search=%22in+development+-+microsoft+intune%22&locale=en-us`

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

### <a name="update-to-android-app-configuration-policies---6113334----"></a>Update voor configuratiebeleid voor Android-apps<!-- 6113334  -->
Het configuratiebeleid voor Android-apps wordt bijgewerkt zodat beheerders het type apparaatinschrijving kunnen selecteren voordat een app-configuratieprofiel wordt gemaakt. De functionaliteit wordt toegevoegd aan het account voor certificaatprofielen die zijn gebaseerd op inschrijvingstype (werkprofiel of apparaateigenaar).  Bij de release vindt het volgende plaats:

- Bestaand beleid dat is gemaakt voorafgaand aan de release van deze functie en waarvoor geen certificaatprofielen zijn gekoppeld aan het beleid, wordt voor het type apparaatinschrijving standaard ingesteld op Werkprofiel en Apparaateigenaarprofiel.
- Bestaand beleid dat is gemaakt voorafgaand aan de release van deze functie en waaraan certificaatprofielen zijn gekoppeld, wordt standaard ingesteld op uitsluitend Werkprofiel.
- Als er een nieuw profiel wordt gemaakt en Werkprofiel en Apparaateigenaarprofiel als het type apparaatinschrijving zijn geselecteerd, kunt u geen certificaatprofiel aan het app-configuratiebeleid koppelen.
- Als er een nieuw profiel wordt gemaakt en alleen Werkprofiel is geselecteerd, kan Werkprofiel-certificaatbeleid dat is gemaakt onder Apparaatconfiguratie worden gebruikt.
- Als er een nieuw profiel wordt gemaakt en alleen Apparaateigenaar is geselecteerd, kan Apparaateigenaar-certificaatbeleid dat is gemaakt onder Apparaatconfiguratie worden gebruikt.

Met bestaand beleid worden geen nieuwe certificaten hersteld of uitgegeven.

Daarnaast voegen we Gmail- en Nine-e-mailconfiguratieprofielen toe die worden gebruikt met zowel het inschrijvingstype Werkprofiel als het inschrijvingstype Apparaateigenaar, waaronder het gebruik van certificaatprofielen voor beide e-mailconfiguratietypen.  Gmail- of Nine-beleid dat u onder Apparaatconfiguratie voor werkprofielen hebt gemaakt, blijft van toepassing op het apparaat en het is niet nodig om ze te verplaatsen naar het app-configuratiebeleid.

In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) vindt u het app-configuratiebeleid door **Apps** > **App-configuratiebeleid** te selecteren. Zie [App-configuratiebeleid voor Microsoft Intune](../apps/app-configuration-policies-overview.md) voor meer informatie over app-configuratiebeleid.

### <a name="microsoft-teams-is-now-included-in-the-office-365-suite-for-macos---5903936----"></a>Microsoft Teams is nu opgenomen in het Office 365-pakket voor macOS<!-- 5903936  -->
Gebruikers aan wie Microsoft Office voor macOS is toegewezen in Microsoft Endpoint Manager krijgen nu naast de bestaande Microsoft Office-apps (Word, Excel, PowerPoint, Outlook en OneNote) ook Microsoft Teams. Intune herkent de bestaande Mac-apparaten waarop de andere Office voor macOS-apps zijn geïnstalleerd en probeert Microsoft Teams te installeren wanneer het apparaat de volgende keer bij Intune wordt ingecheckt. In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) vindt u het **Office 365-pakket** voor macOS door **Apps** > **macOS** > **Toevoegen** te selecteren. Zie [Office 365 toewijzen aan macOS-apparaten met Microsoft Intune](../apps/apps-add-office365-macos.md) voor meer informatie.

### <a name="group-targeting-support-for-customization-pane----4722837----"></a>Ondersteuning voor groepsdoelen voor het deelvenster Aanpassing <!-- 4722837  -->
U kunt de instellingen in het deelvenster Aanpassing toepassen op gebruikersgroepen. Selecteer in de Intune-portal **Client-apps** > **Aanpassing**. Zie [De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen](company-portal-app.md] voor meer informatie.

<!-- ***********************************************-->
## <a name="device-configuration"></a>Apparaatconfiguratie

### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Configuratieprofielen voor een bekabeld netwerkapparaat voor macOS-apparaten<!-- 3508686  -->
Er wordt een nieuw configuratieprofiel voor macOS-apparaten beschikbaar gemaakt om bekabelde netwerken te configureren (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **macOS** als platform > **Bekabeld netwerk** als profieltype). Gebruik deze functie om 802.1x-profielen te maken om bekabelde netwerken te beheren en om deze bekabelde netwerken te implementeren op uw macOS-apparaten.

Van toepassing op:
- macOS

### <a name="improved-user-interface-experience-when-creating-configuration-profiles-on-iosipados-and-macos-devices---5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984----"></a>Verbeterde gebruikersinterface-ervaring bij het maken van configuratieprofielen op iOS-/iPadOS- en macOS-apparaten<!-- 5569008-5569039-5569057-5569110-5569116-5569131-5569139-5569153-5859984  -->
Wanneer u een profiel voor iOS-/iPadOS- of macOS-apparaten maakt, wordt de ervaring in het Beheercentrum voor Eindpuntbeheer bijgewerkt. Deze wijziging is van invloed op de volgende apparaatconfiguratieprofielen (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS** of **macOS** als platform):

- Aangepast: iOS/iPadOS, macOS
- Apparaatfuncties: iOS/iPadOS, macOS
- Apparaatbeperkingen: iOS/iPadOS, macOS
- Endpoint Protection: macOS
- Extensies: macOS
- Voorkeursbestand: macOS

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

### <a name="send-push-notifications-as-an-action-for-non-compliance----1733150-----"></a>Pushmeldingen verzenden als actie voor niet-naleving <!-- 1733150   -->
Voor iOS- en Android-platformen wordt een nieuwe actie voor niet-naleving toegevoegd waarmee een app-pushmelding wordt verzonden via de bedrijfsportal-app. Gebruikers kunnen op de meldingen klikken, waarna de bedrijfsportal-app wordt gestart waarin de reden voor de niet-naleving wordt weergegeven. Beheerders kunnen deze nieuwe actie voor niet-naleving configureren in het Microsoft Endpoint Manager-beheercentrum door naar **Apparaten** > **Nalevingsbeleid** > **Beleid maken** te gaan en vervolgens de *actie* te selecteren om een app-pushmelding te verzenden.

### <a name="pre-release-testing-for-managed-google-play-apps---2681933----"></a>Testen voorafgaand aan de release voor beheerde Google Play-apps<!-- 2681933  -->
Organisaties die gebruikmaken van [gesloten testtrajecten van Google Play voor het testen van apps voorafgaand aan de release](https://support.google.com/googleplay/android-developer/answer/3131213) kunnen deze trajecten beheren met Intune. U kunt selectief Line-Of-Business-apps toewijzen die worden gepubliceerd naar de trajecten voorafgaand aan de productiefase van Google Play, naar testgroepen, om tests uit te voeren. In Intune kunt u ook zien of er voor een app een testtraject voor een build voorafgaand aan de productiefase is gepubliceerd en u kunt dat traject ook toewijzen aan AAD-gebruikersgroepen of -apparaatgroepen. Deze functie is beschikbaar voor al onze momenteel ondersteunde Android Enterprise-scenario's (werkprofiel, volledig beheerd en toegewezen). In het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) kunt u een beheerde Google Play-app toevoegen door **Apps** > **Android** > **Toevoegen** te selecteren. Zie [Beheerde Google Play-apps toevoegen aan Android Enterprise-apparaten met Intune](../apps/apps-add-android-for-work.md) voor meer informatie.

### <a name="manage-smime-settings-for-outlook-on-android---6517085-----"></a>S/MIME-instellingen voor Outlook in Android beheren<!-- 6517085   -->
U kunt met app-configuratiebeleid de S/MIME-instelling voor Outlook beheren op apparaten waarop Android Enterprise wordt uitgevoerd. U kunt ook kiezen of u wilt toestaan dat de apparaatgebruikers S/MIME in- of uitschakelen in de Outlook-instellingen. Ga in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) naar **Apps** > **App-configuratiebeleid** > **Toevoegen** > **Beheerde apparaten** om app-configuratiebeleid voor Android te gebruiken.

### <a name="additional-options-in-sso-and-sso-app-extension-profiles-on-iosipados-devices---6504155----"></a>Aanvullende opties in profielen voor eenmalige aanmelding en app-extensies voor eenmalige aanmelding op iOS- en iPadOS-apparaten<!-- 6504155  -->
Op iOS-/iPadOS-apparaten kunt u het volgende doen:

- Stel in profielen voor eenmalige aanmelding (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatfuncties** voor profiel > **Eenmalige aanmelding**) de principal-naam van Kerberos in op de SAM-accountnaam (Security Account Manager) in profielen voor eenmalige aanmelding. 
- Configureer in profielen voor app-extensies voor eenmalige aanmelding (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatfuncties** voor profieltype > **App-extensie voor eenmalige aanmelding**) de iOS/iPadOS Microsoft Azure AD-extensie met minder klikken door een nieuw type app-extensie voor eenmalige aanmelding te gebruiken. U kunt de Azure AD-extensie voor gedeelde apparaten inschakelen en extensiespecifieke gegevens naar de extensie verzenden.

Van toepassing op:
- iOS/iPadOS 13.0+

Zie [Overzicht van app-extensies voor eenmalige aanmelding](../configuration/device-features-configure.md#single-sign-on-app-extension) en [Lijst met instellingen voor eenmalige aanmelding](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) voor meer informatie over het gebruik van eenmalige aanmelding op iOS-/iPadOS-apparaten.

<!-- ***********************************************-->
## <a name="device-enrollment"></a>Apparaatinschrijving

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Eigen apparaten kunnen voor het implementeren gebruikmaken van VPN<!--5015344 -->
Met de nieuwe wisselknop **Domeinconnectiviteitscontrole overslaan** voor het Autopilot-profiel kunt u Hybrid Azure AD Join-apparaten implementeren zonder toegang tot uw bedrijfsnetwerk door middel van uw eigen Win32 VPN-client van derden. Als u de nieuwe wisselknop wilt zien, gaat u naar het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten**  > **Windows** > **Windows-inschrijving** > **Implementatieprofielen** > **Profiel maken** > **OOBE (Out-of-Box Experience)** .

<!-- ***********************************************-->
## <a name="device-management"></a>Apparaatbeheer

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Ondersteuning van PowerShell-scripts voor BYOD-apparaten<!-- 1862833  -->
PowerShell-scripts bieden ondersteuning voor apparaten die bij Azure AD zijn geregistreerd in Intune. Zie [PowerShell-scripts op Windows 10-apparaten gebruiken in Intune](../apps/intune-management-extension.md) voor meer informatie over PowerShell. Deze functionaliteit biedt geen ondersteuning voor apparaten waarop de Windows 10 Home-editie wordt uitgevoerd.

### <a name="script-support-for-macos-devices---4280361----"></a>Scriptondersteuning voor macOS-apparaten<!-- 4280361  -->
U kunt scripts toevoegen en implementeren op macOS-apparaten. Dankzij deze ondersteuning hebt u meer mogelijkheden om macOS-apparaten te configureren buiten wat al mogelijk is, met behulp van systeemeigen MDM-mogelijkheden op macOS-apparaten.

### <a name="log-analytics-will-include-device-details-log--6014987----"></a>Log Analytics bevat een logboek met apparaatgegevens<!--6014987  -->
De logboeken voor Intune-apparaatgegevens vindt u in **Rapporten** > **Logboekanalyse**. U kunt apparaatgegevens met elkaar in verband brengen om aangepaste query's en Azure-werkmappen te maken.

### <a name="push-notification-when-device-ownership-type-is-changed---5575875----"></a>Pushmelding wanneer verandering optreedt in eigendomstype voor het apparaat<!-- 5575875  -->
U kunt uit het oogpunt van privacy een pushmelding configureren die naar de gebruikers van zowel de Android- als de iOS-bedrijfsportal wordt verzonden wanneer het eigendomstype voor hun apparaat is gewijzigd van Persoonlijk naar Zakelijk. U kunt deze instelling vinden in Microsoft Endpoint Manager door **Tenantbeheer** > **Aanpassing** te selecteren. Zie [Eigendom van het apparaat wijzigen](../enrollment/corporate-identifiers-add.md#change-device-ownership) voor meer informatie over de wijze waarop het eigendom van het apparaat van invloed is op uw eindgebruikers.

<!-- ***********************************************-->
<!--## Intune apps-->
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--
## Monitor and troubleshoot
-->

<!-- ***********************************************-->
<!--
## Role-based access control
-->

<!-- ***********************************************-->
## <a name="security"></a>Beveiliging

### <a name="derived-credentials-support-on-android-fully-managed-devices--4839592--"></a>Ondersteuning voor afgeleide referenties op volledig beheerde Android-apparaten<!--4839592-->
U kunt afgeleide referenties gebruiken op volledig beheerde Android Enterprise-apparaten. Ondersteuning wordt opgenomen voor het ophalen van een afgeleide referentie voor Entrust Datacard, Intercede en DISA Purebred. U kunt een afgeleide referentie gebruiken voor appverificatie, Wi-Fi, VPN of voor S/MIME-ondertekening en/of versleuteling voor apps die dit ondersteunen.

### <a name="privacy-preferences-settings-for-macos-devices---2934232---"></a>Voorkeursinstellingen voor privacy voor macOS-apparaten<!-- 2934232 --> 
Bij de release van macOS Catalina 10.15 zijn nieuwe beveiligings- en privacyverbeteringen toegevoegd. Standaard kunnen toepassingen en processen zonder toestemming van de gebruiker geen toegang krijgen tot specifieke gegevens. Als gebruikers geen toestemming geven, werken de toepassingen en processen mogelijk niet. Intune voegt ondersteuning toe voor instellingen waarmee IT-beheerders toestemming voor toegang tot gegevens namens eindgebruikers kunnen toestaan of weigeren op apparaten waarop macOS 10.14 of hoger wordt uitgevoerd. Door deze instellingen blijven toepassingen en processen goed werken en krijgen eindgebruikers minder vaak prompts te zien.

### <a name="updated-ui-text-and-labels-for-windows-10-endpoint-protection-profile-settings---5983747---"></a>Bijgewerkte tekst en labels voor gebruikersinterface voor instellingen van het Windows 10-eindpuntbeveiligingsprofiel<!-- 5983747 -->
De tekst wordt bijgewerkt voor diverse instellingen die u als Windows 10-apparaatconfiguratieprofielen configureert, zodat u beter begrijpt wat het beoogde gebruik en de beoogde resultaten van de instellingen zijn.

De instellingen die worden bijgewerkt, zijn onder andere Windows 10-apparaatconfiguratieprofielen voor:

- [Apparaatbeperkingen](../configuration/device-restrictions-windows-10.md#microsoft-defender-antivirus) > Microsoft Defender Antivirus  
- [Endpoint Protection](../protect/endpoint-protection-windows-10.md) > Microsoft Defender Antivirus

De instellingen die door Intune worden ondersteund, worden niet gewijzigd. Alleen de tekst van de gebruikersinterface in het Beheercentrum voor Microsoft-eindpuntbeheer wordt hierdoor bijgewerkt.

<!-- ***********************************************-->
## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Zie tevens

Voor meer informatie over recente ontwikkelingen raadpleegt u [Wat is er nieuw in Microsoft Intune?](whats-new.md).



