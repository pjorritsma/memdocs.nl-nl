---
title: Intune-beveiligingsbasislijninstellingen voor Microsoft Edge
titleSuffix: Microsoft Intune
description: Beveiligingsbasislijninstellingen die door Intune worden ondersteund voor het beheren van Microsoft Edge-browser
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: edge-baseline-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 861d7f526711f2169e8fd03b3df09659440523b9
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693443"
---
<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end
-->

# <a name="microsoft-edge-baseline-settings-for-intune"></a>Basislijninstellingen van Microsoft Edge voor Intune

Bekijk de basislijninstellingen van de Edge-webbrowser die worden ondersteund door Microsoft Intune. De standaardinstellingen van de basislijn van Microsoft Edge vertegenwoordigen de aanbevolen configuratie voor Microsoft Edge-browsers en komen mogelijk niet overeen met de standaardinstellingen voor andere beveiligingsbasislijnen.

::: zone pivot="edge-october-2019"

> [!NOTE]
> De Microsoft Edge-basislijn voor oktober 2019 is in openbare preview.

::: zone-end
::: zone pivot="edge-april-2020"

*Deze nieuwe basislijn wordt in de komende weken geïmplementeerd op tenants. We verwachten dat alle tenants deze nieuwe basislijn begin mei zullen hebben.*
Als u wilt weten wat er is veranderd in deze versie van de basislijn vergeleken met eerdere versies, gebruikt u de actie [Basislijnen vergelijken](../protect/security-baselines.md#compare-baseline-versions) die beschikbaar is wanneer het paneel *Versies* voor deze basislijn wordt weergegeven. Als u wilt weten wat er is veranderd in deze versie van de basislijn vergeleken met eerdere versies, gebruikt u de actie [Basislijnen vergelijken](../protect/security-baselines.md#compare-baseline-versions) die beschikbaar is wanneer het paneel *Versies* voor deze basislijn wordt weergegeven.

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020"

## <a name="microsoft-edge"></a>Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020"

- **Ondersteunde verificatieschema's**  
  Hiermee geeft u op welke HTTP-verificatieschema's worden ondersteund. U kunt het beleid configureren met behulp van de volgende waarden: *Standaard*, *Samenvatting*, *NTLM* en *Onderhandelen*. Meerdere waarden scheiden met komma's. Als u dit beleid niet configureert, worden alle vier de schema's gebruikt.

  - **Ingeschakeld** (*standaard*): de schema's die u selecteert, worden gebruikt.
  - **Uitgeschakeld**
  - **Niet geconfigureerd**: alle vier de schema's worden gebruikt.
  
  Wanneer deze optie is ingesteld op *Ingeschakeld* kunt u de volgende instelling configureren, waarbij u selecteert welke verificatie u wilt gebruiken:

  - **Ondersteunde verificatieschema's**  
    Maak een keuze uit de volgende opties:
    - **Standaard**
    - **Samenvatting**
    - **NLTM** *(standaard geselecteerd)*
    - **Onderhandelen** *(standaard geselecteerd)*

- **Standaardinstelling voor Adobe Flash**  
  CSP: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) en [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  Schakel toegang tot de volgende instelling in, waarmee u gedrag kunt configureren voor het uitvoeren van de Adobe Flash-invoegtoepassing.  

  - **Ingeschakeld** *(standaard)*
  - **Uitgeschakeld**
  - **Niet geconfigureerd**

  Als de optie is ingesteld op *Ingeschakeld*, kunt u de volgende instelling configureren.

  - **Standaardinstelling voor Adobe Flash**

    - **De Adobe Flash-invoegtoepassing blokkeren** (*standaard*): Adobe Flash wordt op alle sites geblokkeerd
    - **Klik om af te spelen**: Adobe Flash wordt uitgevoerd, maar kan alleen worden gestart als de gebruiker de optie selecteert.

- **Bepalen welke extensies niet kunnen worden geïnstalleerd**  
  Schakel het gebruik in van een lijst met extensies die gebruikers niet in Microsoft Edge kunnen installeren. Wanneer de lijst in gebruik is, worden alle instellingen in de lijst die eerder zijn geïnstalleerd uitgeschakeld en kan de gebruiker deze niet inschakelen. Als u een item uit de lijst met geblokkeerde extensies verwijdert, wordt deze extensie automatisch opnieuw ingeschakeld overal waar deze eerder is geïnstalleerd.

  - **Ingeschakeld** (*standaard*): hiermee schakelt u het gebruik van de lijst in om extensies te blokkeren.
  - **Uitgeschakeld**
  - **Niet geconfigureerd**: gebruikers kunnen elke extensie installeren in Microsoft Edge.
  
  Wanneer deze optie is ingesteld op *Ingeschakeld*, kunt u de volgende instelling configureren, waarmee de lijst met te blokkeren extensies wordt gedefinieerd.

  - **Extensie-id's die de gebruiker niet mag installeren (of * voor alle id's)**

    Selecteer **Toevoegen** en geef aanvullende extensies op. **\*** is standaard geselecteerd.

- **Systeemeigen berichtenhosts op gebruikersniveau toestaan (geïnstalleerd zonder beheerdersmachtigingen)**  
  Hiermee wordt installatie op gebruikersniveau van systeemeigen berichtenhosts ingeschakeld.

  - **Ingeschakeld**
  - **Uitgeschakeld** (*standaard*): in Microsoft Edge worden alleen systeemeigen berichtenhosts gebruikt die op systeemniveau zijn geïnstalleerd.
  - **Niet geconfigureerd**: standaard is in Microsoft Edge het gebruik van systeemeigen berichtenhosts op gebruikersniveau toegestaan.

- **Opslaan van wachtwoorden in wachtwoordbeheer inschakelen**  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Laat Microsoft Edge gebruikerswachtwoorden opslaan.

  - **Ingeschakeld**: gebruikers kunnen hun wachtwoorden opslaan in Microsoft Edge. De volgende keer dat ze de site bezoeken, wordt het wachtwoord automatisch door Microsoft Edge ingevoerd. Gebruikers kunnen dit beleid niet wijzigen of overschrijven in Microsoft Edge.
  - **Uitgeschakeld** (*standaard*): gebruikers kunnen geen nieuwe wachtwoorden opslaan, maar kunnen eerder opgeslagen wachtwoorden wel blijven gebruiken. Gebruikers kunnen dit beleid niet wijzigen of overschrijven in Microsoft Edge.
  - **Niet geconfigureerd**: gebruikers kunnen wachtwoorden opslaan en deze functie uitschakelen.

- **Overslaan van Microsoft Defender SmartScreen-prompts voor sites voorkomen**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Bepaal of gebruikers de waarschuwingen van Microsoft Defender SmartScreen over mogelijk schadelijke websites kunnen negeren.

  - **Ingeschakeld** (*standaard*): gebruikers kunnen de waarschuwingen van Microsoft Defender SmartScreen niet negeren en kunnen niet doorgaan naar de site.
  - **Uitgeschakeld**: gebruikers kunnen de waarschuwingen van Microsoft Defender SmartScreen negeren en doorgaan naar de site.
  - **Niet geconfigureerd**: gebruikers kunnen de waarschuwingen van Microsoft Defender SmartScreen negeren en doorgaan naar de site

- **Overslaan van Microsoft Defender SmartScreen-waarschuwingen over downloads voorkomen**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Bepaal of gebruikers Microsoft Defender SmartScreen-waarschuwingen over niet-geverifieerde downloads kunnen negeren.

  - **Ingeschakeld** (*standaard*): gebruikers in uw organisatie kunnen Microsoft Defender SmartScreen-waarschuwingen niet negeren en de niet-geverifieerde downloads niet voltooien.
  - **Uitgeschakeld**: gebruikers kunnen Microsoft Defender SmartScreen-waarschuwingen negeren en niet-geverifieerde downloads voltooien.
  - **Niet geconfigureerd**: gebruikers kunnen Microsoft Defender SmartScreen-waarschuwingen negeren en niet-geverifieerde downloads voltooien.

- **Site-isolatie inschakelen voor elke site**  
  Configureer site-isolatie om te voorkomen dat gebruikers afzien van het standaardgedrag dat alle sites worden geïsoleerd.
  
  - **Ingeschakeld** (*standaard*): gebruikers kunnen niet afzien van het standaardgedrag dat elke site wordt uitgevoerd in een eigen proces.
  - **Uitgeschakeld**: gebruikers kunnen afzien van site-isolatie. Site-isolatie wordt niet uitgeschakeld.
  - **Niet geconfigureerd**: gebruikers kunnen afzien van site-isolatie. Site-isolatie wordt niet uitgeschakeld.

  In Microsoft Edge wordt ook het beleid [IsolateOrigins](https://docs.microsoft.com/deployedge/microsoft-edge-policies#isolateorigins) ondersteund, waarmee aanvullende, gedetailleerdere oorsprongen kunnen worden geïsoleerd.  Intune biedt geen ondersteuning voor het configureren van het IsolateOrigins-beleid.
  
- **Microsoft Defender SmartScreen configureren**  
  CSP: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Microsoft Defender SmartScreen geeft waarschuwingsberichten weer om gebruikers te beschermen tegen mogelijke oplichting door phishing en schadelijke software. Microsoft Defender SmartScreen is standaard ingeschakeld.
  
  - **Ingeschakeld** (*standaard*): Microsoft Defender SmartScreen is ingeschakeld en kan niet door gebruikers worden uitgeschakeld.
  - **Uitgeschakeld**: Microsoft Defender SmartScreen is uitgeschakeld en kan niet door gebruikers worden ingeschakeld.
  - **Niet geconfigureerd**: gebruikers kunnen kiezen of ze Microsoft Defender SmartScreen willen gebruiken.

  Dit beleid is alleen beschikbaar voor Windows-instanties die zijn toegevoegd aan een Microsoft Active Director-domein of op Windows 10 Pro-of Enterprise-instanties die zijn geregistreerd voor apparaatbeheer.

- **Microsoft Defender SmartScreen configureren om mogelijk ongewenste apps te blokkeren**  
    Configureer Microsoft Defender SmartScreen-gedrag voor het blokkeren van mogelijk ongewenste apps. Via Microsoft Defender SmartScreen kunnen waarschuwingsberichten worden weergegeven om gebruikers te beschermen tegen adware, coin miners, bundleware en andere apps met een lage reputatie die worden gehost door websites. Het blokkeren van mogelijk ongewenste apps in Microsoft Defender SmartScreen is standaard uitgeschakeld.

  - **Ingeschakeld** (*standaard*): mogelijk ongewenste apps worden geblokkeerd.
  - **Uitgeschakeld**: mogelijk ongewenste apps worden niet geblokkeerd.
  - **Niet geconfigureerd**: gebruikers kunnen kiezen of ze willen gebruikmaken van het blokkeren van mogelijk ongewenste apps in Microsoft Defender SmartScreen.

  Dit beleid is alleen beschikbaar voor Windows-instanties die zijn toegevoegd aan een Microsoft Active Director-domein of op Windows 10 Pro-of Enterprise-instanties die zijn geregistreerd voor apparaatbeheer.

- **Gebruikers toestaan om door te gaan vanaf de SSL-waarschuwingspagina**  
   CSP: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge toont een waarschuwingspagina wanneer gebruikers sites met SSL-fouten bezoeken.
  - **Ingeschakeld**: gebruikers kunnen door de waarschuwingspagina's klikken.
  - **Uitgeschakeld** (*standaard*): gebruikers kunnen niet door waarschuwingspagina's klikken.
  - **Niet geconfigureerd**: gebruikers kunnen door deze waarschuwingspagina's klikken.

- **Minimumversie van SSL ingeschakeld**  
  Schakel de optie in om een minimaal ondersteunde versie van SSL in te stellen.

  - **Ingeschakeld** (*standaard*): schakel toegang tot de volgende instelling in, waarbij u de minimale versie van TLS opgeeft die moet worden gebruikt.
  - **Uitgeschakeld**
  - **Niet geconfigureerd**: in Microsoft Edge wordt standaard de minimale versie *TLS 1.0* gebruikt.

  Als de optie is ingesteld op *Ingeschakeld*, kunt u TLS instellen door de volgende instelling te gebruiken.

  - **Minimumversie van SSL ingeschakeld** Stel de minimale versie van TLS in die moet worden gebruikt. In Microsoft Edge wordt geen SSL/TLS-versie gebruikt die lager is dan de opgegeven versie.
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2** (*standaard*)

::: zone-end

::: zone pivot="edge-october-2019"

- **Overslaan van Microsoft Defender SmartScreen-prompts voor sites voorkomen**  
  **Standaardinstelling**: Ingeschakeld  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Met deze beleidsinstelling kunt u bepalen of gebruikers de waarschuwingen van Microsoft Defender SmartScreen over mogelijk schadelijke websites kunnen negeren. 
  - Als u deze instelling inschakelt, kunnen gebruikers de waarschuwingen van Microsoft Defender SmartScreen niet negeren en kunnen ze niet doorgaan naar de site. 
  - Als u deze instelling uitschakelt of niet configureert, kunnen gebruikers de waarschuwingen van Microsoft Defender SmartScreen negeren en doorgaan naar de site.

- **Minimumversie van SSL ingeschakeld**  
  **Standaardinstelling**: Ingeschakeld  

  Stel een minimaal ondersteunde versie van SSL in. Als u dit beleid instelt op *Niet geconfigureerd*, gebruikt Microsoft Edge een standaard minimale versie van *TLS 1.0*. Wanneer deze optie is ingesteld op *Ingeschakeld*, kunt u een minimumversie selecteren uit de volgende waarden:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **Minimumversie van SSL ingeschakeld**  
    **Standaardinstelling**: TLS 1.2

- **Overslaan van Microsoft Defender SmartScreen-waarschuwingen over downloads voorkomen**  
  **Standaardinstelling**: Ingeschakeld  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Met dit beleid kunt u bepalen of gebruikers Microsoft Defender SmartScreen-waarschuwingen over niet-geverifieerde downloads kunnen negeren.
  - Als u dit beleid inschakelt, kunnen gebruikers in uw organisatie Microsoft Defender SmartScreen-waarschuwingen niet negeren en kunnen ze de niet-geverifieerde downloads niet voltooien.
  - Als u dit beleid uitschakelt of niet configureert, kunnen gebruikers de waarschuwingen van Microsoft Defender SmartScreen negeren en doorgaan naar de site.

- **Gebruikers toestaan om door te gaan vanaf de SSL-waarschuwingspagina**  
  **Standaardinstelling**: Uitgeschakeld  
  Microsoft Edge CSP: [Browser/PreventCertErrorOverrides](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge toont een waarschuwingspagina wanneer gebruikers sites met SSL-fouten bezoeken. Als u dit beleid instelt op *Ingeschakeld* of op *Niet geconfigureerd*, kunnen gebruikers door deze waarschuwingspagina's klikken. Wanneer dit beleid is *Uitgeschakeld*, worden gebruikers geblokkeerd en kunnen ze niet doorklikken op een waarschuwingspagina. 

- **Standaardinstelling voor Adobe Flash**  
  **Standaardinstelling**: Ingeschakeld  
  Microsoft Edge CSP: [Browser/AllowFlash](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflash) en [Browser/AllowFlashClickToRun](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  Hiermee wordt bepaald of websites die niet worden gedekt door PluginsAllowedForUrls of PluginsBlockedForUrls automatisch de Adobe Flash-invoegtoepassing kunnen uitvoeren. 

  - Selecteer BlockPlugins om Adobe Flash op alle sites te blokkeren
  - Selecteer ClickToPlay om Adobe Flash uit te voeren, maar vereis dat de gebruiker op de tijdelijke aanduiding klikt om deze te starten.
  
  In elk geval hebben de beleidsregels PluginsAllowedForUrls en PluginsBlockedForUrls prioriteit boven DefaultPluginsSetting. Automatisch afspelen is alleen toegestaan voor domeinen die expliciet worden vermeld in het beleid PluginsAllowedForUrls. 
   Als u automatisch afspelen voor alle sites wilt inschakelen, kunt u http://* en https://* toevoegen aan deze lijst.

  - Als u dit beleid instelt op *Niet geconfigureerd*, kan de gebruiker deze instelling handmatig wijzigen. * 2 = De Adobe Flash-invoegtoepassing blokkeren * 3 = Klikken om de eerste optie 1 in te stellen op alles toestaan af te spelen, maar deze functie wordt nu alleen verwerkt door het beleid PluginsAllowedForUrls. Bestaande beleidsregels die 1 gebruiken, worden in de modus klikken om af te spelen uitgevoerd.  

  - **Standaardinstelling voor Adobe Flash**  
    **Standaardinstelling**: De Adobe Flash-invoegtoepassing blokkeren

- **Site-isolatie inschakelen voor elke site**  
  **Standaardinstelling**: Ingeschakeld  

  Het beleid SitePerProcess kan worden gebruikt om te voorkomen dat gebruikers afzien van het standaardgedrag van het isoleren van alle sites. U kunt ook het beleid IsolateOrigins gebruiken om aanvullende, nauwkeurigere oorsprongen te isoleren.

  - Wanneer dit beleid is ingesteld op *Ingeschakeld*, kunnen gebruikers niet afzien van het standaardgedrag waarbij elke site wordt uitgevoerd in een eigen proces. 
  - Als u *Uitgeschakeld* of *Niet geconfigureerd* gebruikt, kan een gebruiker afzien van site-isolatie. (Door bijvoorbeeld de vermelding Site-isolatie uitschakelen in edge://flags te gebruiken.) Als u het beleid uitschakelt of het beleid niet configureert, wordt Site-isolatie niet uitgeschakeld.

- **Ondersteunde verificatieschema's**  
  **Standaardinstelling**: Ingeschakeld  

  Hiermee geeft u op welke HTTP-verificatieschema's worden ondersteund. U kunt het beleid configureren met behulp van de volgende waarden: basic, digest, ntlm en negotiate. Meerdere waarden scheiden met komma's. Als u dit beleid niet configureert, worden alle vier de schema's gebruikt.

  - **Ondersteunde verificatieschema's**  
    Maak een keuze uit de volgende opties:
    - Basic
    - Samenvatting
    - NLTM *(standaard geselecteerd)*
    - Onderhandelen  *(Standaard geselecteerd)*

- **Opslaan van wachtwoorden in wachtwoordbeheer inschakelen**  
  **Standaardinstelling**: Uitgeschakeld  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Laat Microsoft Edge gebruikerswachtwoorden opslaan.
  - Als u dit beleid inschakelt, kunnen gebruikers hun wachtwoord opslaan in Microsoft Edge. De volgende keer dat ze de site bezoeken, wordt het wachtwoord automatisch door Microsoft Edge ingevoerd.
  - Als u dit beleid uitschakelt, kunnen gebruikers geen nieuwe wachtwoorden opslaan, maar wel eerder opgeslagen wachtwoorden gebruiken.
  
  Wanneer u dit beleid instelt op *Ingeschakeld* of *Uitgeschakeld*, kunnen gebruikers dit beleid niet wijzigen of negeren in Microsoft Edge.
  
  Als u dit instelt op *Niet geconfigureerd*, kunnen gebruikers wachtwoorden opslaan en deze functie uitschakelen.

- **Bepalen welke extensies niet kunnen worden geïnstalleerd**  
  **Standaardinstelling**: Ingeschakeld  

  Er wordt een lijst weergegeven van de specifieke extensies die gebruikers niet in Microsoft Edge kunnen installeren. Wanneer u dit beleid implementeert, worden alle extensies in deze lijst die eerder zijn geïnstalleerd, uitgeschakeld en kan de gebruiker deze niet inschakelen. Als u een item uit de lijst met geblokkeerde extensies verwijdert, wordt deze extensie automatisch opnieuw ingeschakeld overal waar deze eerder is geïnstalleerd.
  
  Gebruik **\*** om alle extensies te blokkeren die niet expliciet worden vermeld in de acceptatielijst. Als dit beleid is ingesteld op *Niet geconfigureerd*, kunnen gebruikers een willekeurige extensie installeren in Microsoft Edge.
  
  Voorbeeldwaarde: extension_id1 extension_id2.  
  <br>
  - **Extensie-id's die de gebruiker niet mag installeren (of * voor alle id's)**  
    Selecteer **Toevoegen** en geef aanvullende extensies op. **\*** is standaard geselecteerd.

- **Microsoft Defender SmartScreen configureren**  
  **Standaardinstelling**: Ingeschakeld  
  Microsoft Edge CSP: [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  Met deze beleidsinstelling kunt u configureren of Microsoft Defender SmartScreen moet worden ingeschakeld. Microsoft Defender SmartScreen geeft waarschuwingsberichten weer om uw gebruikers te beschermen tegen mogelijke oplichting door phishing en schadelijke software.
  
  - Microsoft Defender SmartScreen is standaard ingeschakeld. Als u deze instelling inschakelt, is Microsoft Defender SmartScreen ingeschakeld en kunnen gebruikers het niet uitschakelen.
  - Als u deze instelling uitschakelt, is Microsoft Defender SmartScreen uitgeschakeld en kunnen gebruikers het niet inschakelen.
  - Wanneer deze optie is ingesteld op *Niet geconfigureerd*, kunnen gebruikers kiezen of ze Microsoft Defender SmartScreen willen gebruiken.
  
  Dit beleid is alleen beschikbaar voor Windows-instanties die zijn toegevoegd aan een Microsoft Active Director-domein of op Windows 10 Pro-of Enterprise-instanties die zijn geregistreerd voor apparaatbeheer.

- **Systeemeigen berichtenhosts op gebruikersniveau toestaan (geïnstalleerd zonder beheerdersmachtigingen)**  
  **Standaardinstelling**: Uitgeschakeld

  Hiermee wordt installatie op gebruikersniveau van systeemeigen berichtenhosts ingeschakeld. 
  - Als u dit beleid uitschakelt, gebruikt Microsoft Edge alleen systeemeigen berichtenhosts die op het systeemniveau zijn geïnstalleerd. Als u dit beleid niet configureert, kan Microsoft Edge standaard het gebruik van systeemeigen berichtenhosts op gebruikersniveau toestaan.

::: zone-end

## <a name="next-steps"></a>Volgende stappen

- [Meer informatie over beveiligingsbasislijnen](security-baselines.md)
- [Conflicten voorkomen](security-baselines.md#avoid-conflicts)
- [Beleidsregels en profielen voor het oplossen van problemen in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
