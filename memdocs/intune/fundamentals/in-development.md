---
title: In ontwikkeling - Microsoft Intune
titleSuffix: ''
description: Microsoft Intune-functies in ontwikkeling
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.assetid: 25b3c26e-cf4e-4152-8306-bf4be4af2ad1
ms.reviewer: cacampbell
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2bb971da483cd86e143673b57e8e5e09f943a5
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764200"
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

### <a name="company-portal-for-android-will-guide-users-to-get-apps-after-work-profile-enrollment----6103999----"></a>Bedrijfsportal voor Android helpt gebruikers apps te verkrijgen na registratie van het werkprofiel <!-- 6103999  -->
De in-app-richtlijnen in de bedrijfsportal worden verbeterd zodat gebruikers gemakkelijker apps kunnen zoeken en installeren.  Nadat gebruikers zich hebben geregistreerd voor werkprofielbeheer, zien ze een bericht dat ze aanbevolen apps kunnen vinden in de Google Play-versie met badge. Gebruikers zien ook de nieuwe koppeling **Apps downloaden** in de bedrijfsportal-lade aan de linkerkant. Om ruimte te maken voor deze nieuwe en verbeterde ervaringen, wordt het tabblad **APPS** verwijderd. 

<!-- ***********************************************-->
## <a name="device-configuration"></a>Apparaatconfiguratie

### <a name="device-configuration-profile-settings-and-values-will-be-updated-for-windows-platforms---4091122---"></a>De instellingen en waarden voor apparaatconfiguratieprofielen worden bijgewerkt voor Windows-platformen<!-- 4091122 -->
Wanneer u apparaatconfiguratieprofielen voor Windows-platformen maakt (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > elke **Windows**-optie voor platform), wijken een aantal instellingen en de bijbehorende waarden af van de CSP; dit kan verwarrend zijn. De namen van instellingen en de bijbehorende waarden worden bijgewerkt zodat deze duidelijker zijn.

Van toepassing op:

- Configuratieprofielen voor Windows 10 en hoger
- Apparaatconfiguratieprofielen voor Windows Holographic voor Bedrijven
- Apparaatconfiguratieprofielen voor Windows 8.1
- Apparaatconfiguratieprofielen voor Windows Phone 8.1

### <a name="new-filevault-setting-for-macos-endpoint-protection-device-configuration-policy---5459801-----"></a>De nieuwe FileVault-instelling voor het apparaatconfiguratiebeleid voor eindpuntbeveiliging voor macOS<!-- 5459801   -->
Op de sjabloon [macOS-eindpuntbeveiliging](../protect/endpoint-protection-macos.md) wordt een nieuwe instelling aan de FileVault-categorie toegevoegd: Herstelsleutel verbergen. (**Apparaten** > **Configuratieprofielen** > **Profiel maken**, selecteer **macOS** als het *Platform* en kies vervolgens **Eindpuntbeveiliging** als het *Profieltype*). Door deze instelling wordt de persoonlijke sleutel tijdens de FileVault 2-versleuteling voor de eindgebruiker verborgen. Apparaatgebruikers kunnen hun persoonlijke herstelsleutel op elk gewenst moment weergeven via de bedrijfsportal-app voor iOS of via de bedrijfsportal-website voor het versleutelde macOS-apparaat. Ga naar Apparaatgegevens en klik op *Herstelsleutel ophalen* om de persoonlijke herstelsleutel weer te geven.

Deze instelling is niet beschikbaar in een eerder gemaakt beleid. U moet FileVault-beleidsregels opnieuw maken om deze instelling te configureren zodat u er gebruik van kunt maken. 


<!-- ***********************************************-->
## <a name="device-enrollment"></a>Apparaatinschrijving

### <a name="bring-your-own-devices-can-use-vpn-to-deploy--5015344---"></a>Eigen apparaten kunnen voor het implementeren gebruikmaken van VPN<!--5015344 -->
Deze functie wordt mogelijk vertraagd.

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


### <a name="duplicate-your-policies-in-endpoint-security---5892558-----"></a>Uw beleid dupliceren in Eindpuntbeveiliging<!-- 5892558   -->
U kunt een beleid selecteren dat u hebt gemaakt in het knooppunt Eindpuntbeveiliging van het Microsoft Endpoint Manager-beheercentrum en dit vervolgens dupliceren om een kopie te maken.  De beleidsregels die u kunt dupliceren, zijn onder andere de regels die u maakt voor: 

- Antivirus
- Schijfversleuteling
- Firewall
- Eindpuntdetectie en -respons
- Kwetsbaarheid voor aanvallen verminderen
- Accountbeveiliging

Met duplicatie maakt u een kopie van het oorspronkelijke beleid. U kunt dit vervolgens een andere naam geven en bewerken. De kopie bevat geen toewijzingen van het origineel.

### <a name="new-profile-for-endpoint-security-firewall-policy---5653324-----"></a>Nieuw profiel voor firewallbeleid van Eindpuntbeveiliging<!-- 5653324   -->
Als voorbeeld voegen we een extra profiel voor Windows 10 en hoger toe aan het firewallbeleid in Eindpuntbeveiliging van Intune (**Eindpuntbeveiliging** > **Firewall** > **Beleid maken** > **Windows 10 en hoger** selecteren). 

Elk exemplaar van dit nieuwe profiel ondersteunt maximaal 150 aangepaste *Microsoft Defender Firewall-regels*. Met het profiel van de Microsoft Defender Firewall-regels kunt u gedetailleerde Windows Firewall-regels definiëren om poorten en toepassingen in Windows 10 toe te staan of te blokkeren.

<!-- ***********************************************-->
## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]

## <a name="see-also"></a>Zie tevens

Voor meer informatie over recente ontwikkelingen raadpleegt u [Wat is er nieuw in Microsoft Intune?](whats-new.md).



