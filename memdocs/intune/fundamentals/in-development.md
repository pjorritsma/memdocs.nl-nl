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
ms.openlocfilehash: 107ac1e2aef18bcb72a6fe1f94eade23c3f85319
ms.sourcegitcommit: 79ffc8afed164c408db6994806d71f64d1fc0b8f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 06/23/2020
ms.locfileid: "85216515"
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
<!--## App management-->


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


<!-- ***********************************************-->
<!--## Device enrollment-->



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

### <a name="new-merge-logic-for-windows-10-devices--179048--"></a>Nieuwe samenvoeglogica voor Windows 10-apparaten<!--179048-->
Als een klant nu de installatiekopie terugzet op een apparaat en het vervolgens opnieuw inschrijft, worden er meerdere records voor het apparaat weergegeven in de beheerconsole van Microsoft Endpoint Manager. Er wordt een nieuwe samenvoeglogica ontwikkeld voor het samenvoegen van dergelijke dubbele records voor Windows 10-apparaten.

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
