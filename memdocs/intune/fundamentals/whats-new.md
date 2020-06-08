---
title: Nieuwe functies in Microsoft Intune - Azure | Microsoft Docs
titleSuffix: ''
description: Ontdekken wat er nieuw is in Intune Azure Portal
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/22/2020
ms.topic: conceptual
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
ms.openlocfilehash: ca3ec1605bd4d63c182511c32297da0bdb503d8b
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/24/2020
ms.locfileid: "83824163"
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

<!-- ########################## -->

## <a name="week-of-may-18-2020"></a>Week van 18 mei 2020

### <a name="device-security"></a>Apparaatbeveiliging

#### <a name="use-endpoint-detection-and-response-policy-to-onboard-devices-to-defender-atp---7130165----"></a>Eindpuntdetectie en antwoordbeleid gebruiken om apparaten te onboarden naar Defender ATP<!-- 7130165  -->

[Eindpuntbeveiligingsbeleid gebruiken voor eindpuntdetectie en -respons](../protect/endpoint-security-edr-policy.md) (EDR) om apparaten te onboarden en te configureren voor uw implementatie van Microsoft Defender Advanced Threat Protection (Defender ATP). EDR ondersteunt beleid voor Windows-apparaten die worden beheerd door Intune (MDM) en een afzonderlijk beleid voor Windows-apparaten die worden beheerd door Configuration Manager. 

Als u het beleid voor apparaten van Configuration Manager wilt gebruiken, moet u Configuration Manager [instellen voor de ondersteuning van het EDR-beleid](../protect/endpoint-security-edr-policy.md#set-up-configuration-manager-to-support-edr-policy). Instellen omvat:

- Configureer uw Configuration Manager voor *tenantkoppeling*.
- Installeer een module-update voor Configuration Manager om ondersteuning voor het EDR-beleid in te schakelen. Deze update is alleen van toepassing op hiërarchieën die *tenantkoppeling* hebben ingeschakeld.
- Synchroniseer uw apparaatverzamelingen van uw hiërarchie met het Beheercentrum voor Microsoft Endpoint Manager.


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


#### <a name="unified-delivery-of-azure-ad-enterprise-and-office-online-applications-in-the-company-portal---4404429-----"></a>Collectieve levering van Azure AD Enterprise- en Office Online-apps in de bedrijfsportal<!-- 4404429   -->
*Deze functie is vertraagd.*
In het deelvenster **Aanpassing** van Intune kunt u in de Bedrijfsportal zowel van **toepassingen van Microsoft Azure AD** als van **toepassingen van Office Online** selecteren dat u deze wilt **Verbergen** of **Weergeven**. Elke eindgebruiker ziet de volledige toepassingscatalogus van de gekozen Microsoft-service. Standaard wordt elke extra app-bron ingesteld op **Verbergen**. Deze functie gaat van kracht op de bedrijfsportal-website; ondersteuning in de Windows-, iOS/iPadOS- en macOS-bedrijfsportals zal naar verwachting volgen. U vindt deze configuratie-instelling door in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) **Tenantbeheer** > **Aanpassing** te selecteren. Zie [De Intune-bedrijfsportal-apps, de bedrijfsportalwebsite en de Intune-app aanpassen](../apps/company-portal-app.md) voor informatie.

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

Er is nu een nieuwe versie van de functie [Beveiligingsbasislijn van Microsoft Edge](../protect/security-baselines.md#available-security-baselines) beschikbaar. Deze wordt uitgebracht als algemeen beschikbaar (GA). De voorgaande Edge-basislijn was in preview.  De nieuwe basislijnversie van april 2020 (Edge versie 80 en hoger). 

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

<!-- ########################## -->
## <a name="week-of-january-27-2020"></a>De week van 27 januari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="intune-support-for-additional-microsoft-edge-version-77-deployment-channel-for-macos---5983950----"></a>Intune-ondersteuning voor het extra implementatiekanaal van Microsoft Edge-versie 77 voor macOS<!-- 5983950  -->
Microsoft Intune biedt nu ondersteuning voor het extra **stabiele** implementatiekanaal voor de Microsoft Edge-app voor macOS. Het **stabiele** kanaal is het aanbevolen kanaal voor een brede implementatie van Microsoft Edge in Enterprise-omgevingen. Het wordt elke zes weken bijgewerkt en elke release bevat verbeteringen uit het **Beta**-kanaal. Naast het **stabiele** kanaal en het **Beta**-kanaal, biedt Intune ook ondersteuning voor een **Dev**-kanaal. De openbare preview-versie biedt een stabiel kanaal en een Dev-kanaal voor Microsoft Edge-versie 77 en hoger voor macOS. Automatische updates van de browser zijn standaard ingeschakeld. Raadpleeg [Microsoft Edge toevoegen aan macOS-apparaten met behulp van Microsoft Intune](../apps/apps-edge-macos.md) voor meer informatie.

#### <a name="retirement-of-intune-managed-browser--5728447---"></a>Buiten gebruik stellen van Microsoft Intune Managed Browser<!--5728447 -->
De Intune Managed Browser wordt buiten gebruik gesteld. Gebruik Microsoft Edge als uw beveiligde Intune-browser. 

<!-- ########################## -->
## <a name="week-of-january-20-2020-2001-service-release"></a>Week van 20 januari 2020 (2001 servicerelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="user-experience-change-when-adding-apps-to-intune---4705829-----"></a>Wijziging in gebruikerservaring bij het toevoegen van apps aan Intune<!-- 4705829   -->
U ziet een nieuwe gebruikerservaring wanneer u apps toevoegt via Intune. Deze ervaring biedt dezelfde instellingen en gegevens die u eerder hebt gebruikt. De nieuwe ervaring volgt echter stappen die vergelijkbaar zijn met die van een wizard voordat een app wordt toegevoegd aan Intune. Deze nieuwe ervaring biedt ook een controlepagina voordat u de app toevoegt. Selecteer vanuit het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de opties **Apps** > **Alle apps** > **Toevoegen**. Zie [Web-apps toevoegen aan Microsoft Intune](../apps/apps-add.md) voor meer informatie.

#### <a name="require-win32-apps-to-restart----5622282-----"></a>Vereisen dat Win32-apps opnieuw worden gestart <!-- 5622282   -->
U kunt vereisen dat een Win32-app opnieuw moet worden gestart na een geslaagde installatie. U kunt ook de hoeveelheid tijd (de respijtperiode) kiezen, voordat opnieuw wordt gestart.

#### <a name="user-experience-change-when-configuring-apps-in-intune---4207990-----"></a>Wijziging in gebruikerservaring bij het configureren van apps in Intune<!-- 4207990   -->
U ziet een nieuwe gebruikerservaring bij het maken van app-configuratiebeleid in Intune. Deze ervaring biedt dezelfde instellingen en gegevens die u eerder hebt gebruikt. De nieuwe ervaring volgt echter stappen die vergelijkbaar zijn met die van een wizard voordat beleid wordt toegevoegd aan Intune. Selecteer in het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) de optie **Apps** > **App-configuratiebeleid** > **Toevoegen**. Zie [App-configuratiebeleidsregels voor Microsoft Intune](../apps/app-configuration-policies-overview.md) voor meer informatie. 

#### <a name="intune-support-for-additional-microsoft-edge-for-windows-10-deployment-channel---5861774---"></a>Intune-ondersteuning voor het extra implementatiekanaal van Microsoft Edge voor Windows 10<!-- 5861774 -->
Microsoft Intune biedt nu ondersteuning voor het extra **stabiele** implementatiekanaal voor de app Microsoft Edge (versie 77 en hoger) voor Windows 10. Het **stabiele** kanaal is het aanbevolen kanaal voor een brede implementatie van Microsoft Edge voor Windows 10 in Enterprise-omgevingen. Dit kanaal wordt elke zes weken bijgewerkt en elke release bevat verbeteringen uit het **Beta**-kanaal. Naast het **stabiele** kanaal en het **Beta**-kanaal, biedt Intune ook ondersteuning voor een **Dev**-kanaal. Raadpleeg [Microsoft Edge voor Windows 10 - App-instellingen configureren](../apps/apps-windows-edge.md#configure-app-settings) voor meer informatie.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="improved-user-interface-experience-when-configuring-exchange-activesync-on-premises-connector-ui---5695492-----"></a>Verbeterde ervaring voor de gebruikersinterface bij het configureren van de UI voor de on-premises Exchange ActiveSync-connector<!-- 5695492   -->
We hebben de ervaring voor het [configureren van de on-premises Exchange ActiveSync-connector](../protect/exchange-connector-install.md) bijgewerkt. De bijgewerkte ervaring maakt gebruik van één deelvenster voor het configureren, bewerken en samenvatten van de details van uw on-premises connectors.

#### <a name="add-automatic-proxy-settings-to-wi-fi-profiles-for-android-enterprise-work-profiles---4490822-----"></a>Automatische proxyinstellingen toevoegen aan Wi-Fi-profielen voor Android Enterprise-werkprofielen<!-- 4490822   -->
Op apparaten met een Android Enterprise-werkprofiel kunt u Wi-Fi-profielen maken. Wanneer u het type Wi-Fi Enterprise kiest, kunt u ook het type EAP (Extensible Authentication Protocol) invoeren dat in uw Wi-Fi-netwerk wordt gebruikt.

Wanneer u nu het Enterprise-type kiest, kunt u ook automatische proxyinstellingen invoeren, inclusief een proxyserver-URL, zoals `proxy.contoso.com`.

Ga naar [Wi-Fi-instellingen voor apparaten met Android Enterprise en Android Kiosk in Microsoft Intune toevoegen](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only) om de huidige Wi-Fi-instellingen te zien die u kunt configureren.

Van toepassing op:
- Android Enterprise - Werkprofiel

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-enrollment"></a>Apparaatinschrijving

#### <a name="block-android-enrollments-by-device-manufacturer--5197392----"></a>Android-inschrijvingen blokkeren op apparaatfabrikant<!--5197392  -->
U kunt inschrijven van bepaalde apparaten blokkeren, op basis van de fabrikant van het apparaat. Deze functie is van toepassing op apparaten met werkprofielen voor Android-apparaatbeheerder en Android Enterprise. Ga naar [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **Inschrijvingsbeperkingen** om de inschrijvingsbeperkingen te zien.

#### <a name="improvements-to-the-iosipados-create-enrollment-type-profile-ui---6055005---"></a>Verbeteringen in de UI voor het iOS/iPadOS-profielinschrijvingstype maken<!-- 6055005 -->
Voor iOS/iPadOS-gebruikersinschrijving is de pagina **Profielinschrijvingstype maken** **Instellingen** gestroomlijnd om het keuzeproces voor **Inschrijvingstype** te verbeteren met behoud van dezelfde functionaliteit. Als u de nieuwe UI wilt bekijken, gaat u naar het [Microsoft Endpoint Manager-beheercentrum](https://go.microsoft.com/fwlink/?linkid=2109431) > **Apparaten** > **iOS** > **iOS-inschrijving** > **Inschrijvingstypen** > **Profiel maken** >  pagina **Instellingen**. Raadpleeg [Een gebruikersinschrijvingsprofiel maken in Intune](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune) voor meer informatie.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="new-information-in-device-details---4471759-5604099----"></a>Nieuwe informatie in apparaatdetails<!-- 4471759 5604099  -->
De pagina **Overzicht** voor apparaten bevat nu de volgende informatie:
- Geheugencapaciteit (hoeveelheid fysiek geheugen op het apparaat)
- Geheugenopslag (hoeveelheid fysieke opslag op het apparaat) 
- CPU-architectuur

#### <a name="ios-bypass-activation-lock-remote-action-renamed-to-disable-activation-lock---5904591----"></a>De externe actie iOS-activeringsvergrendeling overslaan heet nu Activeringsvergrendeling uitschakelen <!--5904591  -->
De externe actie **Activeringsvergrendeling overslaan** heeft een nieuwe naam gekregen en heet nu **Activeringsvergrendeling uitschakelen**. Raadpleeg [iOS-activeringsvergrendeling met Intune uitschakelen](../remote-actions/device-activation-lock-disable.md) voor meer informatie.

#### <a name="windows-10-feature-update-deployment-support-for-autopilot-devices---5948137-----"></a>Ondersteuning voor implementatie van Windows 10-onderdelenupdate voor Autopilot-apparaten<!-- 5948137   -->
Intune biedt nu ondersteuning voor geregistreerde Autopilot-apparaten met behulp van [implementaties van Windows 10-onderdelenupdates](../protect/windows-update-for-business-configure.md#windows-10-feature-updates).

Beleidsregels voor de Windows 10-onderdelenupdates kunnen niet worden toegepast tijdens de OOBE (Out of Box Experience) van Autopilot en worden alleen toegepast nadat de eerste scan van Windows Update is uitgevoerd nadat een apparaat is ingericht (doorgaans een dag).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

#### <a name="windows-autopilot-deployment-reports-preview----3856172-----"></a>Windows Autopilot-implementatierapporten (preview) <!-- 3856172   -->
In een nieuw rapport kunt u de details bekijken van elk apparaat dat via Windows Autopilot is geïmplementeerd. Zie [Autopilot-implementatierapport](../enrollment/enrollment-autopilot.md#autopilot-deployments-report) voor meer informatie.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer

#### <a name="new-intune-built-in-role-endpoint-security-manager--4253397-----"></a>Nieuwe ingebouwde Intune-rol Eindpuntbeveiligingsbeheerder<!--4253397   -->
Er is een nieuwe ingebouwde Intune-rol beschikbaar: Eindpuntbeveiligingsbeheerder. Deze nieuwe rol biedt beheerders volledige toegang tot het knooppunt Eindpuntbeheer in Intune en alleen-lezentoegang tot andere gebieden. De rol is een uitbreiding van de rol Beveiligingsbeheerder van Azure AD. Als u momenteel alleen Algemene beheerder als rol gebruikt, zijn er geen wijzigingen nodig. Als u rollen gebruikt en u de granulariteit wilt gebruiken die de rol Eindpuntbeveiligingsbeheerder biedt, wijst u die rol toe wanneer deze beschikbaar is. Zie [Op rollen gebaseerd toegangsbeheer](role-based-access-control.md) voor meer informatie over ingebouwde rollen.

<!-- ########################## -->
## <a name="week-of-january-6-2020"></a>De week van 6 januari 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="smime-support-for-microsoft-outlook-for-ios---2669398---"></a>S/MIME-ondersteuning voor Microsoft Outlook voor iOS<!-- 2669398 -->
Intune biedt ondersteuning voor het leveren van S/MIME-ondertekening- en versleutelingscertificaten die kunnen worden gebruikt met Outlook voor iOS op iOS-apparaten. Zie [Sensitivity labeling and protection in Outlook for iOS and Android](https://aka.ms/omsmime) (Gevoeligheidslabels en -bescherming in Outlook voor iOS en Android) voor meer informatie.

#### <a name="cache-win32-app-content-using-microsoft-connected-cache-server---6030314---"></a>Win32-app-inhoud in de cache opslaan met Microsoft Connected Cache-server<!-- 6030314 -->
U kunt een Microsoft Connected Cache-server op uw Configuration Manager-distributiepunten installeren om inhoud van Intune Win32-apps op te slaan in de cache. Zie [Microsoft Connected Cache in Configuration Manager: ondersteuning voor Intune Win32-apps](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune) voor meer informatie.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer

#### <a name="windows-10-administrative-templates-admx-profiles-now-support-scope-tags---5137390---"></a>Profielen voor Windows 10-beheersjablonen (ADMX) ondersteunen nu bereiktags <!--5137390 -->
U kunt nu bereiktags toewijzen aan beheersjabloonprofielen (ADMX). Ga hiervoor naar **Intune** > **Apparaten** > **Configuratieprofielen** > kies een beheersjabloonprofiel in de lijst > **Eigenschappen** > **Bereiktags**. Zie [Assign scope tags to other objects](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects) (bereiktags toewijzen aan andere objecten) voor meer informatie over bereiktags.

<!-- ########################## -->
## <a name="week-of-december-30-2019"></a>Week van 30 december 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="retrieve-personal-recovery-key-from-mem-encrypted-macos-devices---4851745---"></a>Persoonlijke herstelsleutel ophalen van met MEM versleutelde macOS-apparaten<!-- 4851745 -->
Eindgebruikers kunnen hun persoonlijke herstelsleutel (FileVault Key) ophalen met behulp van de Bedrijfsportal-app voor iOS. Het apparaat met de persoonlijke herstelsleutel moet zijn geregistreerd bij Intune en moet zijn versleuteld met FileVault via intune. Met de Bedrijfsportal-app voor iOS kan een eindgebruiker zijn persoonlijke herstelsleutel ophalen op zijn versleutelde macOS-apparaat door te klikken op **Herstelsleutel ophalen**. U kunt de herstelsleutel ook ophalen uit Intune door **Apparaten** > *het versleutelde en geregistreerde macOS-apparaat* > **Herstelsleutel ophalen** te selecteren. Zie [FileVault-versleuteling voor macOS](../protect/encrypt-devices-filevault.md) voor meer informatie over FileVault.

#### <a name="ios-and-ipados-user-licensed-vpp-apps---5619268---"></a>VPP-apps met gebruikerslicenties voor iOS- en iPadOS<!-- 5619268 -->
Op door de gebruiker ingeschreven iOS- en iPadOS-apparaten krijgen eindgebruikers niet langer pas gemaakte VPP-toepassingen met apparaatlicenties te zien die zijn geïmplementeerd als beschikbaar. Eindgebruikers blijven echter alle gebruikerslicenties voor VPP in de Bedrijfsportal zien. Zie [iOS- en macOS-apps beheren die zijn aangeschaft via een Apple Volume Purchase Program met Microsoft Intune](../apps/vpp-apps-ios.md) voor meer informatie over VPP-apps.

<!-- ########################## -->
## <a name="week-of-december-23-2019"></a>Week van 23 december 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="notice---windows-10-1703-rs2-will-be-moving-out-of-support----5026679---"></a>Kennisgeving: Windows 10 1703 (RS2) wordt binnenkort niet meer ondersteund <!-- 5026679 -->
Vanaf 9 oktober 2018, biedt Microsoft geen ondersteuning meer voor de edities Home, Pro en Pro voor werkstations van Windows 10 1703 (RS2). Voor de edities Enterprise en Education van Windows 10 1703 (RS2) wordt sinds 8 oktober 2019 geen ondersteuning meer geboden. Vanaf 26 december 2019 wordt de minimale versie van de Windows Bedrijfsportal-app bijgewerkt naar Windows 10 1709 (RS3). Op computers met versies van vóór 1709 worden bijgewerkte versies van de app niet meer ontvangen via de Microsoft Store. We hebben deze wijziging eerder meegedeeld aan klanten die oudere versies van Windows 10 beheren via het berichtencentrum. Zie het [informatieblad over de levenscyclus van Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) voor meer informatie.

<!-- ########################## -->

## <a name="week-of-december-16-2019"></a>Week van 16 december 2019

### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="updates-to-administrative-templates-for-windows-10-devices----5941568---"></a>Updates voor Beheersjablonen voor Windows 10-apparaten <!-- 5941568 -->

U kunt ADMX-sjablonen in Microsoft Intune gebruiken om de instellingen voor Microsoft Edge, Office en Windows te beheren. De volgende updates zijn doorgevoerd door beleidsinstellingen van Beheersjablonen in Intune:

- Er is ondersteuning toegevoegd voor de versies 78 en 79 van Microsoft Edge.
- Omvat de ADMX-bestanden van 11 november 2019 in [Beheersjabloon-bestanden (ADMX/ADML) en het hulpprogramma voor het aanpassen van Office voor Office 365 ProPlus, Office 2019 en Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

Bekijk voor meer informatie over ADMX-sjablonen in Intune het artikel [Windows 10-sjablonen gebruiken voor het configureren van instellingen voor groepsbeleid in Microsoft Intune](../configuration/administrative-templates-windows.md).

Van toepassing op:

- Windows 10 en hoger

## <a name="week-of-december-9-2019-1912-service-release"></a>Week van 9 december 2019 (1912 servicerelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="migrating-to-microsoft-edge-for-managed-browsing-scenarios---5173762---"></a>Migreren naar Microsoft Edge voor beheerdebrowserscenario's<!-- 5173762 -->
Met het naderen van de buitengebruikstelling van de Intune Managed Browser zijn wijzigingen aangebracht in het beveiligingsbeleid voor apps om de benodigde stappen voor het migreren van uw gebruikers naar Edge te vereenvoudigen. De opties voor de instelling **Overdracht van webinhoud met andere apps beperken** van het beveiligingsbeleid voor apps zijn gewijzigd naar de volgende opties:

- Elke app
- Intune Managed Browser
- Microsoft Edge
- Niet-beheerde browser 

Wanneer u **Microsoft Edge** selecteert, ontvangen uw eindgebruikers een melding over voorwaardelijke toegang, waarin wordt aangegeven dat Microsoft Edge vereist is voor beheerdebrowserscenario's. Ze worden gevraagd om Microsoft Edge te downloaden en zich aan te melden met hun AAD-account, als ze dit nog niet hebben gedaan.  Dit is kan worden vergeleken met de instelling van de app-configuratie-instellingen `com.microsoft.intune.useEdge` op **waar** voor uw MAM-apps. Voor bestaand beveiligingsbeleid voor apps dat gebruikmaakte van de **door beleid beheerde browsers** wordt nu **Intune Managed Browser** geselecteerd. Het gedrag zal niet wijzigen. Dit betekent dat uw gebruikers via berichten zal worden gevraagd Microsoft Edge te gebruiken als u de app-configuratie-instelling **useEdge** hebt ingesteld op **Waar**. We stimuleren alle klanten aan om hun app-beveiligingsbeleid bij te werken met **Overdracht van webinhoud met andere apps beperken** om ervoor te zorgen dat gebruikers de juiste richtlijnen zien voor de overgang naar Microsoft Edge, ongeacht vanuit welke app koppelingen worden gestart. 

#### <a name="configure-app-notification-content-for-organization-accounts---2576686----"></a>Inhoud van app-meldingen voor organisatieaccounts configureren<!-- 2576686  -->
Met beveiligingsbeleid voor apps in Intune (APP) op Android- en iOS-apparaten kunt u inhoud voor app-meldingen beheren voor organisatieaccounts. U kunt een optie selecteren (Toestaan, Organisatiegegevens blokkeren of Geblokkeerd) om op te geven hoe meldingen voor organisatieaccounts voor de geselecteerde app worden weergegeven. Deze functie vereist ondersteuning vanuit toepassingen en is mogelijk niet beschikbaar voor alle APP-toepassingen. Outlook voor iOS 4.15.0 (of hoger) en Outlook voor Android 4.83.0 (of hoger) biedt ondersteuning voor deze instelling. De instelling is beschikbaar in de console, maar de functionaliteit wordt pas van kracht na 16 december 2019. Zie [Wat is beveiligingsbeleid voor apps?](../apps/app-protection-policy.md) voor meer informatie over APP.

#### <a name="microsoft-app-icons-update--4677605----"></a>Nieuwe pictogrammen voor Microsoft-apps<!--4677605  -->
De pictogrammen die worden gebruikt voor Microsoft-apps in het deelvenster met apps voor het app-beveiligingsbeleid en het app-configuratiebeleid zijn bijgewerkt.

#### <a name="require-use-of-approved-keyboards-on-android--4761794----"></a>Vereist gebruik van goedgekeurde toetsenborden in Android<!--4761794  -->
Als onderdeel van een beveiligingsbeleid voor apps kunt u de instelling [**Goedgekeurde toetsenborden**](../apps/app-protection-policy-settings-android.md#data-protection) opgeven om te beheren welke Android-toetsenborden kunnen worden gebruikt met beheerde Android-apps. Wanneer een gebruiker de beheerde app opent en nog geen een goedgekeurd toetsenbord voor die app gebruikt, wordt hij gevraagd om over te schakelen naar een van de goedgekeurde toetsenborden die al op het apparaat zijn geïnstalleerd. Als het nodig is, wordt er een koppeling weergegeven om een goedgekeurd toetsenbord te downloaden uit de Google Play Store, die de gebruiker kan installeren en instellen. De gebruiker kan alleen tekstvelden in een beheerde app bewerken wanneer het actieve toetsenbord niet een van de goedgekeurde toetsenborden is.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="updated-single-sign-on-experience-for-apps-and-websites-on-your-ios-ipados-and-macos-devices---4999578----"></a>Nieuwe ervaring met eenmalige aanmelding voor apps en websites op iOS-, iPadOS- en macOS-apparaten<!-- 4999578  -->
Intune heeft meer instellingen voor eenmalige aanmelding (SSO) toegevoegd voor iOS-, iPadOS-en macOS-apparaten. U kunt nu SSO-extensies voor omleiding configureren die zijn geschreven door uw organisatie of door uw id-provider. Gebruik deze instellingen on naadloze eenmalige aanmelding te configureren voor apps en websites die gebruikmaken van moderne verificatiemethodes, zoals OAuth en SAML2. 

Deze nieuwe instellingen zijn een uitbreiding van de vorige instellingen voor SSO-app-extensies en de ingebouwde Kerberos-uitbreiding van Apple (**Apparaten** > **Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **iOS/iPadOS** of **macOS** voor het platformtype > **Apparaatfuncties** voor het profieltype). 

Ga naar [SSO op iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) en [SSO op macOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension) voor een overzicht van de instellingen voor SSO-app-extensies die u kunt configureren.

Van toepassing op:

- iOS/iPadOS
- macOS

#### <a name="we-have-updated-two-device-restriction-settings-for-ios-and-ipados-devices-to-correct-their-behavior---5701352------"></a>Er zijn twee instellingen voor apparaatbeperking voor iOS- en iPadOS-apparaten bijgewerkt om het gedrag ervan te corrigeren<!-- 5701352    -->
Voor iOS-apparaten kunt u beperkingsprofielen voor apparaten maken die **Draadloze PKI-updates toestaan** en **Beperkte USB-modus blokkeren** (**Apparaten** > **Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **iOS/iPadOS** voor platform > **Apparaatbeperkingen** voor het profieltype). Vóór deze release waren de instellingen en beschrijvingen van de gebruikersinterface voor de volgende instellingen onjuist. Deze zijn nu gecorrigeerd. Vanaf deze release is het gedrag van de instellingen als volgt:

**Draadloze PKI-updates blokkeren**: **Blokkeren** voorkomt dat uw gebruikers software-updates ontvangen tenzij het apparaat is verbonden met een computer. **Niet geconfigureerd** (standaard): hiermee staat u toe dat een apparaat software-updates ontvangt zonder dat het verbonden is met een computer.
- Voorheen kon u met deze instelling het volgende configureren: Met **Toestaan** konden uw gebruikers software-updates ontvangen zonder dat hun apparaten zijn aangesloten op een computer.
**USB-accessoires toestaan terwijl het apparaat is vergrendeld**: Met **Toestaan** kunnen USB-accessoires gegevens uitwisselen met een apparaat dat al meer dan een uur is vergrendeld. **Niet geconfigureerd** (standaard) werkt de beperkte USB-modus niet bij op het apparaat en USB-accessoires kunnen geen gegevens overdragen vanaf het apparaat als het meer dan een uur is vergrendeld.
- Voorheen kon u met deze instelling het volgende configureren: Met **Blokkeren** kon u de beperkte USB-modus uitschakelen op apparaten in de supervisiemodus.

Zie [iOS- en iPadOS-apparaatinstellingen om functies toe te staan of te beperken met Intune](../configuration/device-restrictions-ios.md) voor meer informatie over de configureerbare instellingen.

Deze functie is van toepassing op:

- OS/iPadOS

#### <a name="wired-network-device-configuration-profiles-for-macos-devices---3508686----"></a>Configuratieprofielen voor een bekabeld netwerkapparaat voor macOS-apparaten<!-- 3508686  -->
   > [!NOTE]
   > Deze functie is vertraagd, maar wordt binnenkort vrijgegeven.

#### <a name="block-users-from-configuring-certificate-credentials-in-the-managed-keystore-on-android-enterprise-device-owner-devices---3311998---"></a>Voorkomen dat gebruikers certificaatreferenties configureren in de beheerde sleutelopslag op Android Enterprise-apparaten van eigenaars<!-- 3311998 -->
Op Android Enterprise-apparaten van een eigenaar kunt u een nieuwe instelling configureren die voorkomt dat gebruikers hun certificaatreferenties configureren in de beheerde keystore (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **Android Enterprise** voor platform > **Alleen apparaateigenaar > Apparaatbeperkingen** voor profieltype > **Gebruikers en accounts**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="protected-wipe-action-now-available--51150000---"></a>De actie Beveiligd wissen is nu beschikbaar<!--51150000 -->
U hebt nu de mogelijkheid om de actie Apparaat wissen te gebruiken om een apparaat beveiligd te wissen. Beveiligd wissen werkt hetzelfde als standaard wissen, behalve dat deze actie niet kan worden omzeild door het apparaat uit te schakelen. Als de opdracht Beveiligd wissen is gegeven, wordt het apparaat gereset totdat de opdracht is uitgevoerd. In sommige configuraties kan deze actie ervoor zorgen dat het apparaat niet opnieuw kan worden opgestart. Zie [Apparaten buiten gebruik stellen of wissen](../remote-actions/devices-wipe.md) voor meer informatie.

#### <a name="device-ethernet-mac-address-added-to-devices-overview-page--5562275---"></a>Ethernet MAC-adres van apparaat toegevoegd aan de overzichtspagina van het apparaat<!--5562275 -->
U kunt nu het Ethernet MAC-adres van een apparaat zien op de pagina met details van het apparaat (**Apparaten** > **Alle apparaten** > een apparaat kiezen > **Overzicht**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Apparaatbeveiliging

#### <a name="improved-experience-on-a-shared-device-when-device-based-conditional-access-policies-are-enabled---1734096----"></a>Verbeterde ervaring op een gedeeld apparaat wanneer op apparaten gebaseerd beleid voor voorwaardelijke toegang is ingeschakeld<!-- 1734096  -->
We hebben de ervaring verbeterd op een gedeeld apparaat met meerdere gebruikers die op apparaten gebaseerd beleid voor voorwaardelijke toegang gebruiken. Dit hebben we gedaan door de nieuwste nalevingsevaluatie voor de gebruiker te controleren bij het afdwingen van het beleid. Zie de volgende overzichtsartikelen voor meer informatie:
- [Overzicht van voorwaardelijke toegang in Azure](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Overzicht van apparaatnaleving in Intune](../protect/device-compliance-get-started.md)

#### <a name="use-pkcs-certificate-profiles-to-provision-devices-with-certificates---2317124-2317130-2317139-2340517-2340528-2340529----"></a>PKCS-certificaatprofielen gebruiken om apparaten in te richten met certificaten<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
U kunt nu PKCS-certificaatprofielen gebruiken om certificaten uit te geven aan *apparaten* met Android for Work, iOS/iPadOS en Windows. Dit geldt wanneer deze zijn gekoppeld aan profielen zoals die voor Wi-Fi en VPN. Voorheen ondersteunden deze drie platformen alleen op gebruikers gebaseerde certificaten. Ondersteuning op basis wat alleen beschikbaar op macOS.

> [!NOTE]
> PKCS-certificaatprofielen worden niet ondersteund met Wi-Fi-profielen. Gebruik in plaats daarvan SCEP-certificaatprofielen wanneer u een [EAP-type](../configuration/wi-fi-settings-windows.md#enterprise-profile)gebruikt.

Als u een certificaat op basis van een apparaat wilt gebruiken wanneer u [een PKCS-certificaatprofiel maakt](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) voor de ondersteunde platformen, selecteert u **Instellingen**. U ziet nu de instelling voor **Certificaattype**, die ondersteuning biedt voor de opties Apparaat en Gebruiker.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

#### <a name="centralized-audit-logs--5603185-5697164---"></a>Gecentraliseerde auditlogboeken<!--5603185, 5697164 -->
Een nieuwe gecentraliseerde functie voor auditlogboeken verzamelt nu auditlogboeken voor alle categorieën op één pagina. U kunt de logboeken filteren om de gegevens op te halen die u zoekt. Als u de auditlogboeken wilt bekijken, gaat u naar **Tenantbeheer** > **Auditlogboeken**. 

#### <a name="scope-tag-information-included-in-audit-log-activity-details--5763534---"></a>Informatie over bereiktags opgenomen in de details van auditlogboeken<!--5763534 -->
De details van de activiteiten in het auditlogboek bevatten nu informatie over bereiktags (voor Intune-objecten die ondersteuning bieden voor bereiktags). Zie [Auditlogboeken gebruiken om gebeurtenissen bij te houden en te controleren](monitor-audit-logs.md) voor meer informatie over auditlogboeken.

<!-- ########################## -->
## <a name="week-of-december-2-2019"></a>Week van 2 december 2019

#### <a name="new-microsoft-endpoint-configuration-manager-co-management-licensing--5027281--"></a>Nieuw co-beheer met Microsoft Endpoint Configuration Manager-licentiëring<!--5027281-->
Configuration Manager-klanten met Software Assurance hebben toegang tot Intune-co-beheer voor Windows 10-pc's zonder dat ze een extra Intune-licentie voor co-beheer hoeven aan te schaffen. Klanten hoeven geen afzonderlijke Intune/EMS-licenties meer toe te wijzen aan hun eindgebruikers voor het co-beheer van Windows 10.
- Apparaten die worden beheerd door Configuration Manager en die zijn ingeschreven bij co-beheer hebben bijna dezelfde rechten als zelfstandige door Intune beheerde pc's. Na het opnieuw instellen kunnen ze echter niet opnieuw worden ingericht met behulp van Autopilot.
- Voor Windows 10-apparaten die via een andere methode zijn ingeschreven bij Intune zijn volledige Intune-licenties vereist.
- Voor apparaten op andere platforms zijn nog steeds volledige Intune-licenties vereist.

Zie [Licentievoorwaarden](https://www.microsoft.com/en-us/Licensing/product-licensing/products) voor meer informatie.

<!-- ########################## -->
## <a name="week-of-november-18-2019-1911-service-release"></a>Week van 18 november 2019 (1911 servicerelease)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer

#### <a name="ui-update-when-selectively-wiping-app-data---4102028---"></a>Update van gebruikersinterface bij selectief wissen van app-gegevens<!-- 4102028 -->
De gebruikersinterface voor het selectief wissen van app-gegevens in Intune is bijgewerkt. De gebruikersinterface wordt onder andere op deze punten gewijzigd:
- Een vereenvoudigde ervaring in de vorm van een wizard, beknopt weergegeven binnen één deelvenster.
- Een update van de maakstroom om toewijzingen toe te voegen.
- Een samenvattingspagina van alle items die zijn ingesteld bij het weergeven van eigenschappen, vóór het maken van een nieuw beleid of bij het bewerken van een eigenschap. Tijdens het bewerken van eigenschappen toont de samenvatting ook alleen een lijst met items in de categorie met eigenschappen die wordt bewerkt.

Zie [Alleen zakelijke gegevens wissen uit door Intune beheerde apps](../apps/apps-selective-wipe.md) voor meer informatie.

#### <a name="ios-and-ipados-third-party-keyboard-support---4922950---"></a>Toetsenbordondersteuning voor iOS en iPadOS van derden<!-- 4922950 -->
In maart 2019 is aangekondigd dat de instelling voor iOS-beleid voor appbeveiliging Toetsenborden van derden niet meer wordt ondersteund. De functie keert in Intune terug met ondersteuning voor iOS en iPadOS. U kunt deze instelling inschakelen via het tabblad **Gegevensbescherming** van een nieuw of bestaand iOS-/iPadOS-beleid voor appbeveiliging. Zoek de instelling **Toetsenborden van derden** onder **Gegevensoverdracht**.

Het gedrag van deze beleidsinstelling wijkt enigszins af van de vorige implementatie. In apps met meerdere identiteiten met SDK-versie 12.0.16 en hoger, gericht op beleid voor app-beveiliging waarbij deze instelling is ingesteld op **Blokkeren**, kunnen eindgebruikers voor hun organisatie- en persoonlijke accounts geen toetsenborden van derden kiezen. Apps met SDK-versies 12.0.12 en eerder blijven het gedrag vertonen dat is vastgelegd in de titel van de blogpost, [Bekend probleem: toetsenborden van derden worden in iOS niet geblokkeerd voor persoonlijke accounts](https://aka.ms/3rdparty_iOS_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-configuration"></a>Apparaatconfiguratie

#### <a name="target-macos-user-groups-to-require-jamf-management---4061739----"></a>Richten op macOS-gebruikersgroepen waarvoor Jamf-beheer is vereist<!-- 4061739  --> 
U kunt zich op specifieke groepen gebruikers richten die hun [macOS-apparaten laten beheren door Jamf](../protect/conditional-access-integrate-jamf.md). Door deze gerichtheid kunt u de integratie van Jamf-naleving toepassen op een subset van macOS-apparaten, terwijl andere apparaten door Intune worden beheerd. Als u de Jamf-integratie al gebruikt, zijn alle gebruikers standaard bedoeld voor de integratie.

#### <a name="new-exchange-activesync-settings-when-creating-an-email-device-configuration-profile-on-ios-devices---4892824-----"></a>Nieuwe Exchange ActiveSync-instellingen bij het maken van een configuratieprofiel voor een e-mailapparaat op iOS-apparaten<!-- 4892824   --> 
U kunt op iOS/iPadOS-apparaten e-mailconnectiviteit configureren in een apparaatconfiguratieprofiel (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **iOS/iPadOS** als platform > **E-mail** als profieltype). 

Er zijn nieuwe Exchange ActiveSync-instellingen beschikbaar, waaronder:
- **Exchange-gegevens om te synchroniseren**: Kies de Exchange-services voor het synchroniseren (of blokkeren van de synchronisatie) van de agenda, contactpersonen, herinneringen, notities en e-mail.
- **Gebruikers toestaan om de synchronisatie-instellingen te wijzigen**: Gebruikers toestaan (weigeren) de synchronisatie-instellingen voor deze services op hun apparaten te wijzigen.  

Ga naar [E-mailprofielinstellingen voor iOS-apparaten in Intune](../configuration/email-settings-ios.md) voor meer informatie over deze instellingen. 

Van toepassing op:

- iOS 13.0 en hoger
- iPadOS 13.0 en hoger

#### <a name="prevent-users-from-adding-personal-google-accounts-to-android-enterprise-fully-managed-and-dedicated-devices---5353228-----"></a>Voorkomen dat gebruikers persoonlijke Google-accounts toevoegen aan volledig beheerde en toegewezen Android Enterprise-apparaten<!-- 5353228   -->
Op volledig beheerde en toegewezen Android Enterprise-apparaten is een nieuwe instelling aanwezig waarmee wordt voorkomen dat gebruikers persoonlijke Google-accounts kunnen maken (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **Android Enterprise** als platform > **Alleen apparaateigenaar > Apparaatbeperkingen** als profieltype > **Instellingen voor gebruikers en accounts** > **Persoonlijke Google-accounts**).

Ga naar [Met Android Enterprise-apparaatinstellingen functies toestaan of beperken met behulp van Intune](../configuration/device-restrictions-android-for-work.md) als u alle configureerbare instellingen wilt bekijken.

Van toepassing op:

- Volledig beheerde Android Enterprise-apparaten
- Toegewezen Android Enterprise-apparaten

#### <a name="server-side-logging-for-siri-commands-setting-is-removed-in-iosipados-device-restrictions-profile----5468501-----"></a>De instelling Logboekregistratie op de server voor Siri-opdrachten wordt verwijderd in het profiel voor iOS-/iPadOS-apparaatbeperkingen <!-- 5468501   -->
Op iOS- en iPadOS-apparaten wordt de instelling **Logboekregistratie op de server voor Siri-opdrachten** uit de Microsoft Endpoint Manager-beheerconsole verwijderd (**Apparaatconfiguratie** > **Profielen** > **Profiel maken** > **iOS/iPadOS** als platform > **Apparaatbeperkingen** als profieltype > **Ingebouwde apps**). 

Deze instelling heeft geen effect op apparaten. Als u de instelling van bestaande profielen wilt verwijderen, opent u het profiel, brengt u de gewenste wijzigingen aan en slaat u het profiel op. Het profiel wordt bijgewerkt en de instelling wordt van de apparaten verwijderd.

Zie [iOS- en iPadOS-apparaatinstellingen om functies toe te staan of te beperken met Intune](../configuration/device-restrictions-ios.md) als u alle configureerbare instellingen wilt bekijken.

Van toepassing op:

- iOS/iPadOS

#### <a name="windows-10-feature-updates-public-preview---2384877---"></a>Windows 10-onderdelenupdates (openbare preview)<!-- 2384877 -->
U kunt nu [Windows 10-onderdelenupdates](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) implementeren op Windows 10-apparaten. Windows 10-onderdelenupdates zijn een nieuw beleid voor software-updates waarmee de versie van Windows 10 wordt ingesteld die door apparaten moet worden geïnstalleerd en op het systeem blijft. U kunt dit nieuwe beleidstype samen met uw bestaande Windows 10-updateringen gebruiken.

Op apparaten die het beleid voor Windows 10-onderdelenupdates ontvangen, wordt de opgegeven versie van Windows geïnstalleerd en blijft deze versie tot het beleid wordt gewijzigd of verwijderd. Apparaten waarop een nieuwere versie van Windows wordt uitgevoerd, houden de huidige versie. Op apparaten die op een specifieke versie van Windows worden gehouden, kunnen kwaliteits- en beveiligingsupdates voor die versie nog steeds worden geïnstalleerd via Windows 10-updateringen.

Dit nieuwe type beleid wordt vanaf deze week voor tenants geïmplementeerd. Als dit beleid nog niet beschikbaar is voor uw tenant, komt het binnenkort.

#### <a name="add-and-change-key-information-in-plist-files-for-macos-applications---4736278---"></a>Belangrijke informatie toevoegen en wijzigen in PLIST-bestanden voor macOS-toepassingen<!-- 4736278 -->
Op macOS-apparaten kunt u nu een apparaatconfiguratieprofiel maken dat een eigenschappenlijstbestand (.plist) uploadt dat aan een app of het apparaat is gekoppeld (**Apparaten** > **Configuratieprofielen** > **Profiel maken** > **macOS** als platform > **Voorkeursbestand** als profieltype).

Alleen bepaalde apps ondersteunen beheerde voorkeuren. In deze apps kunt u mogelijk niet alle instellingen beheren. Upload een bestand met een eigenschappenlijstbestand waarmee apparaatkanaalinstellingen worden geconfigureerd, geen gebruikerskanaalinstellingen.

Zie [Een eigenschappenlijstbestand toevoegen aan macOS-apparaten met behulp van Microsoft Intune](../configuration/preference-file-settings-macos.md) voor meer informatie over deze functie.

Van toepassing op:

- macOS-apparaten met 10.7 en hoger

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-management"></a>Apparaatbeheer

#### <a name="edit-device-name-value-for-autopilot-devices---2640074---"></a>Waarde van apparaatnaam bewerken voor Autopilot-apparaten<!-- 2640074 -->
U kunt de waarde van de apparaatnaam voor aan Azure AD gekoppelde Autopilot-apparaten bewerken.  Zie [Kenmerken van Autopilot-apparaten bewerken](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes) voor meer informatie.

#### <a name="edit-group-tag-value-for-autopilot-devices---4816775-----"></a>Waarde van groepstag bewerken voor Autopilot-apparaten<!-- 4816775   -->
U kunt de waarde van groepstag bewerken voor Autopilot-apparaten. Zie [Kenmerken van Autopilot-apparaten bewerken](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes) voor meer informatie.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="monitor-and-troubleshoot"></a>Bewaken en problemen oplossen

#### <a name="updated-support-experience---5012398---"></a>Bijgewerkte ondersteuningservaring<!-- 5012398 -->

Met ingang van vandaag wordt een bijgewerkte en gestroomlijnde console-ervaring voor het [verkrijgen van help en ondersteuning voor Intune](get-support.md) voor tenants geïmplementeerd. Als deze nieuwe ervaring nog niet beschikbaar is voor u, komt dit binnenkort.

We hebben de in-console-zoekfunctie en de feedbackfunctie voor veelvoorkomende problemen verbeterd, evenals de workflow voor het opnemen van contact met de ondersteuning. Bij het openen van een supportprobleem ziet u realtime schattingen van wanneer u een antwoord via telefoon of e-mail kunt verwachten. Klanten met Premier- en Unified-ondersteuning kunnen eenvoudig een ernst van hun probleem specificeren om sneller ondersteuning te krijgen.

#### <a name="improved-intune-reporting-experience-public-preview----3791418---"></a>Verbeterde rapportering van Intune (openbare preview) <!-- 3791418 -->
Intune biedt nu verbeterde rapportagemogelijkheden, waaronder nieuwe rapporttypen, betere organisatie van rapporten, meer gerichte weergaven, verbeterde rapportfunctionaliteit, en consistente en actuele gegevens. Nieuwe rapporttypen richten zich op het volgende:

- **Operationeel**: bevat nieuwe records die zich richten op een negatieve status. 
- **Organisatorisch**: biedt een breder overzicht van de algemene status.
- **Historisch**: bevat patronen en trends gedurende een bepaalde periode.
- **Specialistisch**: hiermee kunt u onbewerkte gegevens gebruiken om uw eigen aangepaste rapporten te maken.

De eerste set nieuwe rapporten richt zich op de naleving van apparaten. Zie [Microsoft Intune Reporting Framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) (Rapportageframework van Microsoft Intune) en [Intune-rapporten](reports.md) voor meer informatie.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="role-based-access-control"></a>Op rollen gebaseerd toegangsbeheer

#### <a name="duplicate-custom-or-built-in-roles----1081938-----"></a>Dubbele aangepaste of ingebouwde rollen <!-- 1081938   -->
U kunt voortaan ingebouwde als aangepaste rollen kopiëren. Zie [Rol kopiëren](../fundamentals/create-custom-role.md#copy-a-role) voor meer informatie.

#### <a name="new-permissions-for-school-administrator-role----5621805----"></a>Nieuwe machtigingen voor de rol Schoolbeheerder <!-- 5621805  -->  
De twee nieuwe machtigingen **Profiel toewijzen** en **Apparaat synchroniseren** zijn aan de rol Schoolbeheerder toegevoegd > **Machtigingen** > **Inschrijvingsprogramma's**. Met de machtiging Apparaat synchroniseren kunnen groepsbeheerders Windows Autopilot-apparaten synchroniseren. Met de machtiging Profiel toewijzen kunnen ze door de gebruiker geïnitieerde Apple-inschrijvingsprofielen verwijderen. Het verleent ook machtigingen voor het beheren van Autopilot-apparaattoewijzingen en Autopilot-implementatieprofieltoewijzingen. Zie [Groepsbeheerders toewijzen](https://docs.microsoft.com/intune-education/group-admin-delegate) voor een lijst met alle machtigingen van de schoolbeheerder/groepsbeheerder.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="security"></a>Beveiliging

#### <a name="bitlocker-key-rotation---2564951----"></a>BitLocker-sleutelrotatie<!-- 2564951  -->
U kunt een Intune-apparaatactie gebruiken om [BitLocker-herstelsleutels](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys) op afstand te roteren voor beheerde apparaten met Windows versie 1909 of hoger. Apparaten moeten worden geconfigureerd voor het ondersteunen van de rotatie van herstelsleutels om in aanmerking te komen voor het roteren van herstelsleutels.  

#### <a name="updates-to-dedicated-device-enrollment-to-support-scep-device-certificate-deployment----5198878----"></a>Updates voor de inschrijving van toegewezen apparaten ter ondersteuning van de implementatie van SCEP-apparaatcertificaten <!-- 5198878  -->
Intune biedt nu ondersteuning voor de implementatie van SCEP-apparaatcertificaten op toegewezen Android Enterprise-apparaten voor op certificaten gebaseerde toegang tot Wi-Fi-profielen. De implementatie werkt alleen als de app Microsoft Intune op het apparaat aanwezig is. Als gevolg hiervan hebben we de inschrijving voor toegewezen Android Enterprise-apparaten bijgewerkt. Nieuwe inschrijvingen worden nog steeds op dezelfde manier gestart (met QR, NFC, Zero-touch of apparaat-id), maar bevatten nu een stap waarvoor gebruikers de Intune-app moeten installeren. De app wordt automatisch en op voortschrijdende basis op bestaande apparaten geïnstalleerd.

#### <a name="intune-audit-logs-for-business-to-business-collaboration--5670211---"></a>Intune-auditlogboeken voor business-to-business-samenwerking<!--5670211 -->
Met B2B-samenwerking (business-to-business) kunt u de toepassingen en services van uw bedrijf veilig delen met gastgebruikers van andere organisaties, zonder dat u de controle verliest over uw eigen bedrijfsgegevens. Intune biedt nu ondersteuning voor auditlogboeken voor B2B-gastgebruikers. Als gastgebruikers bijvoorbeeld wijzigingen aanbrengen, kunnen deze gegevens worden vastgelegd via auditlogboeken. Zie [Wat is gastgebruikerstoegang in Azure Active Directory B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b) voor meer informatie

<!-- ########################## -->
## <a name="week-of-november-11-2019"></a>Week van 11 november 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="app-management"></a>Appbeheer  

#### <a name="improved-macos-enrollment-experience-in-company-portal----5074349----"></a>Verbeterde macOS-registratie in bedrijfsportal <!-- 5074349  -->  
De bedrijfsportal voor macOS-registratie heeft een eenvoudiger registratieproces dat nauwkeuriger is afgestemd met de bedrijfsportal voor iOS-registratie. Apparaatgebruikers zien nu het volgende:  

- Een gestroomlijndere gebruikers interface.  
- Een verbeterde controlelijst voor registratie.  
- Duidelijkere instructies over het registreren van apparaten.  
- Verbeterde opties voor probleemoplossing.  

#### <a name="web-apps-launched-from-the-windows-company-portal-app---5030972---"></a>Web-apps starten vanuit de Windows-bedrijfsportal-app<!-- 5030972 -->
Eindgebruikers kunnen web-apps nu direct vanuit de Windows-bedrijfsportal-app starten. Eindgebruikers kunnen de web-app selecteren en vervolgens de optie **In browser openen** kiezen. De gepubliceerde web-URL wordt rechtstreeks in een webbrowser geopend. Deze functionaliteit wordt de komende week doorgevoerd. Zie [Web-apps toevoegen aan Microsoft Intune](../apps/web-app.md) voor meer informatie over het toevoegen van web-apps.  

#### <a name="new-assignment-type-column-in-company-portal-for-windows-10----5459950----"></a>Nieuwe kolom voor toewijzingstype in bedrijfsportal voor Windows 10 <!-- 5459950  -->
De naam van de kolom Bedrijfsportal > **Geïnstalleerde apps** > **Toewijzingstype** is gewijzigd in **Vereist door uw organisatie**.  Onder die kolom zien gebruikers de waarde **Ja** of **Nee** staan om aan te geven dat een app vereist is of optioneel is gemaakt door hun organisatie. Deze wijzigingen zijn aangebracht, omdat de apparaatgebruikers in de war raakten van het concept van beschikbare apps. Uw gebruikers kunnen meer informatie vinden over het installeren van apps via de bedrijfsportal in [Apps installeren en delen op uw apparaat](../user-help/install-apps-cpapp-windows.md). Zie [De app Microsoft Intune-bedrijfsportal configureren](../apps/company-portal-app.md) voor meer informatie over het configureren van de bedrijfsportal-app voor uw gebruikers.  

<!-- ########################## -->
## <a name="week-of-november-4-2019"></a>Week van 4 november 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### <a name="device-security"></a>Apparaatbeveiliging

#### <a name="security-baselines-are-supported-on-microsoft-azure-government---4062552---"></a>Beveiligingsbasislijnen worden ondersteund op Microsoft Azure Government<!-- 4062552 -->

In exemplaren van Intune die worden gehost op *Microsoft Azure Government* kunt u nu [beveiligingsbasislijnen](../protect/security-baselines.md) gebruiken om uw gebruikers en apparaten te beveiligen en beschermen.

## <a name="whats-new-archive"></a>Wat is er nieuw (archief)
Raadpleeg de sectie [Wat is er nieuw (archief)](whats-new-archive.md) voor eerdere maanden.

## <a name="notices"></a>Mededelingen

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


