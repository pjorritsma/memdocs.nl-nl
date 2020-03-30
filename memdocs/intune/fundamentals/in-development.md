---
title: In ontwikkeling - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-functies in ontwikkeling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 18b42dffc2c34adea1f70c4587b5eb5384d0a778
ms.sourcegitcommit: 795e8a6aca41e1a0690b3d0d55ba3862f8a683e7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/24/2020
ms.locfileid: "80220129"
---
# <a name="in-development-for-microsoft-intune---march-2020"></a>In ontwikkeling voor Microsoft Intune: maart 2020

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

### <a name="company-portal-for-ios-to-support-landscape-mode--6048329----"></a>Bedrijfsportal voor iOS ter ondersteuning van liggende modus<!--6048329  -->
Gebruikers kunnen hun apparaat inschrijven, apps zoeken en ondersteuning krijgen met hun favoriete schermstand. De app detecteert automatisch de stand en past de weergave aan de liggende of staande modus van het scherm aan, tenzij gebruikers het scherm vergrendelen in de staande modus.

### <a name="improved-sign-in-experience-in-company-portal-for-android---6103997----"></a>Bijgewerkte aanmeldervaring voor de bedrijfsportal-app voor Android<!-- 6103997  -->
De indeling van diverse aanmeldingsschermen in de bedrijfsportal-app voor Android wordt momenteel bijgewerkt voor een modernere, eenvoudige en duidelijke ervaring voor gebruikers.

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

### <a name="improved-user-interface-experience-when-creating-oemconfig-configuration-profiles-on-android-enterprise-devices---5568645-----"></a>Verbeterde gebruikersinterface-ervaring bij het maken van OEMConfig-configuratieprofielen op Android Enterprise-apparaten<!-- 5568645   -->
Wanneer u een OEMConfig-profiel voor Android Enterprise-apparaten maakt of bewerkt, wordt de ervaring in het Beheercentrum voor Eindpuntbeheer bijgewerkt. De bijgewerkte ervaring biedt in één oogopslag een overzicht van de instellingen die u hebt geconfigureerd. Deze wijziging is van invloed op het OEMConfig-apparaatconfiguratieprofiel (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android Enterprise** als platform > **OEMConfig** als profieltype).

Deze functie is van toepassing op:
- Android Enterprise 

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>De instellingen en waarden voor apparaatconfiguratieprofielen worden bijgewerkt voor Windows-platformen<!-- 4091122 -->
Wanneer u apparaatconfiguratieprofielen voor Windows-platformen maakt (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > elke **Windows**-optie voor platform), wijken een aantal instellingen en de bijbehorende waarden af van de CSP; dit kan verwarrend zijn. De namen van instellingen en de bijbehorende waarden worden bijgewerkt zodat ze duidelijker zijn.

Van toepassing op:

- Configuratieprofielen voor Windows 10 en hoger
- Apparaatconfiguratieprofielen voor Windows Holographic voor Bedrijven
- Apparaatconfiguratieprofielen voor Windows 8.1
- Apparaatconfiguratieprofielen voor Windows Phone 8.1

### <a name="improved-user-interface-experience-when-creating-device-restrictions-profiles-on-android-and-android-enterprise-devices---5841361---"></a>Verbeterde gebruikersinterface-ervaring bij het maken van profielen voor apparaatbeperkingen op Android- en Android Enterprise-apparaten<!-- 5841361 -->
Wanneer u een profiel voor Android- of Android Enterprise-apparaten maakt, wordt de ervaring in het Beheercentrum voor Eindpuntbeheer bijgewerkt. Deze wijziging is van invloed op de volgende apparaatconfiguratieprofielen (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **Android-apparaatbeheerder** of **Android Enterprise** voor platform):

- Apparaatbeperkingen: Android-apparaatbeheerder
- Apparaatbeperkingen: Android Enterprise-apparaateigenaar
- Apparaatbeperkingen: Android Enterprise - Werkprofiel

Zie [Android-apparaatbeheerder](../configuration/device-restrictions-android.md) en [Android Enterprise](../configuration/device-restrictions-android-for-work.md) voor meer informatie over de apparaatbeperkingen die u kunt configureren.

### <a name="configure-the-microsoft-defender-atp-app-for-macos-----5520115----"></a>De Microsoft Defender ATP-app configureren voor macOS  <!-- 5520115  -->
Binnenkort kunt u de [instellingen](../protect/endpoint-protection-macos.md) configureren voor de Microsoft Defender ATP-app voor apparaten waarop macOS wordt uitgevoerd als onderdeel van een apparaatconfiguratieprofiel voor eindpuntbeveiliging (**Apparaten** > **Configuratieprofielen** > **Profiel maken**, selecteer **macOS** als *Platform* en kies vervolgens **Eindpuntbeveiliging** als *Profieltype*). Voor de configuratie van macOS-apparaten zijn acht instellingen beschikbaar. 

Defender ATP wordt ondersteund op apparaten met macOS 10.13 (High Sierra) en hoger. Bovendien moet de [Microsoft Defender ATP](../apps/apps-advanced-threat-protection-macos.md)-app worden geïmplementeerd *nadat* deze instellingen zijn toegepast. De instellingen moeten naar het apparaat worden verzonden voordat de app wordt geïmplementeerd. Bètaversies van macOS worden niet ondersteund.

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>De nieuwe FileVault-instelling voor het apparaatconfiguratiebeleid voor eindpuntbeveiliging voor macOS<!-- 5459801   -->
Op de sjabloon [macOS-eindpuntbeveiliging](../protect/endpoint-protection-macos.md) wordt een nieuwe instelling aan de FileVault-categorie toegevoegd: Herstelsleutel verbergen. (**Apparaten** > **Configuratieprofielen** > **Profiel maken**, selecteer **macOS** als het *Platform* en kies vervolgens **Eindpuntbeveiliging** als het *Profieltype*). Door deze instelling wordt de persoonlijke sleutel tijdens de FileVault 2-versleuteling voor de eindgebruiker verborgen. Apparaatgebruikers kunnen hun persoonlijke herstelsleutel op elk gewenst moment weergeven via de bedrijfsportal-app voor iOS of via de bedrijfsportal-website voor het versleutelde macOS-apparaat. Ga naar Apparaatgegevens en klik op *Herstelsleutel ophalen* om de persoonlijke herstelsleutel weer te geven.

Deze instelling is niet beschikbaar in een eerder gemaakt beleid. U moet FileVault-beleidsregels opnieuw maken om deze instelling te configureren zodat u er gebruik van kunt maken. 

### <a name="configure-delivery-optimization-agent-when-downloading-win32-app-content---5410945----"></a>Delivery Optimization-agent configureren tijdens het downloaden van inhoud voor de Win32-app<!-- 5410945  -->
U kunt de Delivery Optimization-agent configureren zodat inhoud voor de Win32-app op de achtergrond of op de voorgrond wordt gedownload op basis van de toewijzing. Voor bestaande Win32-apps wordt inhoud nog steeds op de achtergrond gedownload. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apps** > **Alle apps** >  *en selecteer de Win32-app* > **Eigenschappen**. Selecteer **Bewerken** naast **Toewijzingen**.  Bewerk de toewijzing door **Opnemen** te selecteren onder **Modus** in de sectie **Vereist**.  U vindt de nieuwe instelling in de sectie **App-instellingen** wanneer deze beschikbaar wordt. Zie [Beheer van Win32-apps - Delivery Optimization](../apps/apps-win32-app-management.md#delivery-optimization) voor meer informatie over Delivery Optimization.

<!-- ***********************************************-->
<!--## Device enrollment-->

<!-- ***********************************************-->
## <a name="device-management"></a>Apparaatbeheer

### <a name="change-primary-user-for-windows-devices----3794742---"></a>Primaire gebruiker wijzigen voor Windows-apparaten <!-- 3794742 -->
U kunt de primaire gebruiker voor hybride Windows-apparaten en gekoppelde Azure AD-apparaten wijzigen. Ga hiervoor naar **Intune** > **Apparaten** > **Alle apparaten** > kies een apparaat > **Eigenschappen** > **Primaire gebruiker**.

### <a name="powershell-scripts-support-for-byod-devices---1862833----"></a>Ondersteuning van PowerShell-scripts voor BYOD-apparaten<!-- 1862833  -->
PowerShell-scripts bieden ondersteuning voor apparaten die bij Azure AD zijn geregistreerd in Intune. Zie [PowerShell-scripts op Windows 10-apparaten gebruiken in Intune](../apps/intune-management-extension.md) voor meer informatie over PowerShell. Deze functionaliteit biedt geen ondersteuning voor apparaten waarop de Windows 10 Home-editie wordt uitgevoerd.

### <a name="new-information-in-device-details---5604099---"></a>Nieuwe informatie in apparaatdetails<!-- 5604099 -->
De pagina **Overzicht** voor apparaten bevat de volgende informatie:

- Opslagcapaciteit (hoeveelheid fysieke opslag op het apparaat)
- Geheugencapaciteit (hoeveelheid fysiek geheugen op het apparaat)

### <a name="script-support-for-macos-devices---4280361----"></a>Scriptondersteuning voor macOS-apparaten<!-- 4280361  -->
U kunt scripts toevoegen en implementeren op macOS-apparaten. Dankzij deze ondersteuning hebt u meer mogelijkheden om macOS-apparaten te configureren buiten wat al mogelijk is, met behulp van systeemeigen MDM-mogelijkheden op macOS-apparaten.

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
