---
title: Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Meer informatie over de beschik bare functies in de Technical Preview-versie 1710 voor Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3dd4c3f22a0f2c24153e6d26be2e3098511c5dc4
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905313"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Mogelijkheden van Technical Preview 1710 voor Configuration Manager

*Van toepassing op: Configuration Manager (technische preview-vertakking)*

Dit artikel bevat een inleiding tot de functies die beschikbaar zijn in de Technical Preview voor Configuration Manager, versie 1710. U kunt deze versie installeren om nieuwe mogelijkheden bij te werken en toe te voegen aan uw Configuration Manager Technical Preview-site. Voordat u deze versie van de Technical Preview installeert, raadpleegt u [Technical Preview voor Configuration Manager](../../core/get-started/technical-preview.md) om vertrouwd te raken met algemene vereisten en beperkingen voor het gebruik van een technische preview, het bijwerken van versies en het geven van feedback over de functies in een technische preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bekende problemen in deze technische preview:**
- **Ondersteuning voor Windows 10, versie 1709 (ook wel bekend als de update voor het najaar van makers)**.  Vanaf deze Windows-versie bevat Windows Media meerdere edities. Bij het configureren van een taken reeks voor het gebruik van een upgrade pakket voor een besturings systeem of een installatie kopie van een besturings systeem, moet u ervoor zorgen dat u een [editie selecteert die wordt ondersteund voor gebruik door Configuration Manager](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Bijwerken naar een nieuwe preview-versie mislukt wanneer u een site server in de passieve modus hebt**. Wanneer u een preview-versie met een [primaire site server in de passieve modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability)uitvoert, moet u de site server van de passieve modus verwijderen voordat u uw preview-site kunt bijwerken naar deze nieuwe preview-versie. U kunt de site server van de passieve modus opnieuw installeren nadat de update door de site is voltooid.

  De site server van de passieve modus verwijderen:
  1. Ga in de-console naar **beheer**  >  **overzicht**  >  **site configuratie**  >  **servers en site systeem rollen**en selecteer vervolgens de site server passieve modus.
  2. Klik in het deel venster **site systeem rollen** met de rechter muisknop op de **site** serverrol en kies vervolgens **rol verwijderen**.
  3. Klik met de rechter muisknop op de site server in de passieve modus en kies **verwijderen**.
  4. Nadat de installatie van de site server ongedaan is gemaakt, start u de service **CONFIGURATION_MANAGER_UPDATE**opnieuw op de actieve primaire site server.

**Hier volgen enkele nieuwe functies die u kunt uitproberen met deze versie.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Verbeteringen voor het implementeren van Power shell-scripts van Configuration Manager
In deze release ondersteunen Power shell-scripts die u nu implementeert het gebruik van de volgende verbeteringen: 
- **Beveiligingsbereiken**.  Scripts maken nu gebruik van beveiligingsbereiken om het ontwerpen en uitvoeren van scripts te beheren. Dit doet u door labels toe te wijzen die gebruikers groepen vertegenwoordigen. Zie op [rollen gebaseerd beheer configureren voor Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)voor meer informatie over het gebruik van beveiligingsbereiken.
- **Real-time bewaking**. Wanneer u de uitvoering van een script bewaakt, is het nu in realtime tijdens het uitvoeren van het script.
- **Validatie van de para meter**. Elke para meter in het script bevat een dialoog venster **Eigenschappen van script parameter** waarmee u validatie voor die para meter kunt toevoegen. Nadat u validatie hebt toegevoegd, moet u fouten ontvangen als u een waarde invoert voor een para meter die niet aan de validatie voldoet.

De implementatie van Power shell-scripts werd voor het eerst geïntroduceerd in Technical Preview [tech preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console). Er zijn aanvullende verbeteringen geleverd met [tech preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) en vervolgens [Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Probeer het nu!

Zie [scripts maken en uitvoeren](../../apps/deploy-use/create-deploy-scripts.md)voor meer informatie over het gebruik van de functie scripts uitvoeren.



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Beperk de uitgebreide Windows 10-gegevens zodat alleen gegevens worden verzonden die relevant zijn voor Windows Analytics Apparaatstatus
<!-- 1356148 -->

Met deze versie kunt u nu het verzamelings niveau voor Windows 10 diagnostische gegevens instellen op **verbeterd (beperkt)**. Met deze instelling kunt u geavanceerde inzichten krijgen over apparaten in uw omgeving zonder dat apparaten alle gegevens in het **verbeterde** niveau rapporteren met Windows 10 versie 1709 of hoger.

Het verbeterde niveau (beperkt) bevat metrische gegevens van het basis niveau en een subset van de verzamelde informatie van het **uitgebreide** niveau dat relevant is voor Windows Analytics.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Met Software Center worden pictogrammen die groter zijn dan 250x250 niet meer vervormd  
<!-- 1356194 -->

Met deze versie vervormt Software Center niet langer pictogrammen die groter zijn dan 250x250. Met Software Center worden dergelijke pictogrammen wazig weer gegeven. U kunt nu een pictogram met een pixel afmetingen van Maxi maal 512 x 512 instellen en het wordt zonder vervorming weer gegeven.

### <a name="try-it-out"></a>Probeer het nu!
Voeg een pictogram voor uw app toe in Software Center. Zie [toepassingen maken](../../apps/deploy-use/create-applications.md)om het uit te proberen.


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Naleving van software Center controleren op apparaten die gezamenlijk worden beheerd
<!-- 1356374 -->
In deze release kunnen gebruikers software Center gebruiken om de naleving van hun door co beheerde Windows 10-apparaten te controleren, zelfs wanneer voorwaardelijke toegang wordt beheerd door intune. Zie voor meer informatie [co-beheer voor Windows 10-apparaten](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Ondersteuning voor exploit Guard
Deze release voegt ondersteuning toe voor Windows Defender exploit Guard. U kunt beleid configureren en implementeren waarmee alle vier de onderdelen van exploit Guard worden beheerd. Deze onderdelen zijn onder andere:
-   Kwetsbaarheid voor aanvallen verminderen
-   Gecontroleerde mappentoegang
-   Exploit Protection
-   Netwerk beveiliging

Compatibiliteits gegevens voor de implementatie van exploit Guard-beleid zijn beschikbaar vanuit de Configuration Manager-console.

Zie [Windows Defender exploit Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) in de Windows-documentatie bibliotheek voor meer informatie over Exploit Guard en specifieke onderdelen en regels.

### <a name="prerequisites"></a>Vereisten
Op beheerde apparaten moet Windows 10 1709 worden bijgewerkt of later en voldoen aan de volgende vereisten, afhankelijk van de geconfigureerde onderdelen en regels:

|Onderdeel voor exploit Guard |Aanvullende vereisten|
|------------------------|------------------------|
| Kwetsbaarheid voor aanvallen verminderen  | Op apparaten moet [Windows Defender AV-real-time-beveiliging]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) zijn ingeschakeld.  |
| Gecontroleerde mappentoegang  | Op apparaten moet [Windows Defender AV-real-time-beveiliging]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) zijn ingeschakeld.   |
| Exploit Protection  | Geen  |
| Netwerk beveiliging  |  Op apparaten moet [Windows Defender AV-real-time-beveiliging]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) zijn ingeschakeld.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Een exploit Guard-beleid maken  <!--1355468 -->
1. Ga in de Configuration Manager-console naar **activa en nalevings**  >  **Endpoint Protection**en klik vervolgens op **Windows Defender exploit Guard**.
2. Klik op het tabblad **Start** in de groep **maken** op **exploit beleid maken**.
3. Geef op de pagina **Algemeen** van de **Wizard Configuratie-item maken** een naam en een optionele beschrijving voor het configuratie-item op.
4. Selecteer vervolgens de onderdelen voor exploit Guard die u met dit beleid wilt beheren. Voor elk onderdeel dat u selecteert, kunt u aanvullende details configureren.
   - Kwets baarheid voor **aanvallen verminderen:** Configureer de Office Threat, scripting dreigingen en e-mail bedreigingen die u wilt blok keren of controleren. U kunt ook specifieke bestanden of mappen uit deze regel uitsluiten.
   - **Beheerde mappen toegang:** Configureer blok keren of controleren en voeg vervolgens apps toe die dit beleid kunnen overs Laan.  U kunt ook extra mappen opgeven die niet standaard worden beveiligd.
   - **Exploit Protection:**  Geef een XML-bestand op dat instellingen bevat voor het beperken van misbruik van systeem processen en apps. U kunt deze instellingen exporteren vanuit de Windows Defender Security Center-app op een Windows 10-apparaat.
   - **Netwerk beveiliging:** Netwerk beveiliging instellen om toegang tot verdachte domeinen te blok keren of te controleren.
5. Voltooi de wizard om het beleid te maken, dat u later op apparaten kunt implementeren.

### <a name="deploy-an-exploit-guard-policy"></a>Een exploit Guard-beleid implementeren     
Nadat u exploit Guard-beleids regels hebt gemaakt, gebruikt u de wizard exploit Guard-beleid implementeren om ze te implementeren. Hiervoor opent u de Configuration Manager-console naar **activa en nalevings**  >  **Endpoint Protection**en klikt u vervolgens op **exploit Guard-beleid implementeren**.

## <a name="limited-support-for-cng-certificates"></a>Beperkte ondersteuning voor CNG-certificaten
<!-- 1356191 -->
Vanaf deze versie kunt u nu [crypto GRAFIE API: Next Generation (CNG)](https://docs.microsoft.com/windows/win32/seccng/cng-features) -certificaat sjablonen gebruiken voor de volgende scenario's:

- Client registratie en communicatie met een HTTPS-beheer punt.   
- Software distributie en toepassings implementatie met een HTTPS-distributie punt.   
- Implementatie van besturingssysteem.  
- SDK voor client berichten (met de nieuwste update) en ISV-proxy.   
- Cloudbeheergateway configuratie.  

Als u CNG-certificaten wilt gebruiken, moet uw certificerings instantie (CA) CNG-certificaat sjablonen opgeven voor doel computers.  De sjabloon details variëren afhankelijk van het scenario. de volgende eigenschappen zijn echter vereist:

- **Compatibiliteit met eerdere versies** tabblad

    - De **certificerings instantie** moet Windows Server 2008 of hoger zijn. (Windows Server 2012 wordt aanbevolen.)

    - De ontvanger van het **certificaat** moet Windows Vista/Server 2008 of hoger zijn. (Windows 8/Windows Server 2012 wordt aanbevolen.)

- **Cryptografie** tabblad

    - **Provider categorie** moet een **sleutelarchiefprovider zijn.**  Lang

Voor de beste resultaten raden we u aan om de onderwerpnaam te bouwen op basis van Active Directory informatie.  Gebruik de DNS-naam voor de indeling van de **onderwerpnaam** en voeg de DNS-naam toe aan de naam van het alternatieve onderwerp.  Anders moet u deze informatie opgeven wanneer het apparaat wordt Inge schreven in het certificaat profiel.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Verbeterde beschrijvingen voor het opnieuw opstarten van de computer in behandeling   <!--1356283 -->
In [Technical preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)hebben we de mogelijkheid toegevoegd om apparaten te identificeren waarvoor opnieuw opstarten in behandeling is vanuit de Configuration Manager-console.

Met ingang van deze technische preview wordt de-console weer gegeven met aanvullende informatie over het proces of de actie die het opnieuw opstarten aanvraagt.

## <a name="device-guard-policy-changes----1355092---"></a>Wijzigingen in Device Guard-beleid <!-- 1355092 -->
Met de 1710 Technical Preview-build zijn de volgende drie wijzigingen aangebracht in verband met het Device Guard-beleid:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>De naam van het Device Guard-beleid is gewijzigd in Windows Defender Application Control-beleid
De naam van het Device Guard-beleid is gewijzigd in Windows Defender Application Control-beleid. De **wizard Device Guard-beleid maken** heeft nu bijvoorbeeld de naam **wizard Windows Defender-toepassings beheer beleid maken**.

### <a name="restart-is-not-required-to-apply-policies"></a>Opnieuw opstarten is niet vereist voor het Toep assen van beleid
Vanaf de update voor het najaar van makers voor Windows versie 1709, hoeven apparaten die gebruikmaken van de nieuwe versie van Windows niet opnieuw te worden opgestart om het Windows Defender Application Control-beleid toe te passen.

Opnieuw opstarten is de standaard instelling.

#### <a name="try-it-out"></a>Probeer het nu!  

Als u het opnieuw opstarten wilt uitschakelen, voert u de volgende stappen uit:

1.  Open de wizard **beleid voor Windows Defender-toepassings beheer maken** .
2.  Schakel op het tabblad **Algemeen** het selectie vakje uit voor het **afdwingen van het opnieuw opstarten van apparaten zodat dit beleid kan worden afgedwongen voor alle processen**.
3.  Klik op **volgende** totdat de wizard is voltooid.

Voor oudere versies van Windows wordt een geautomatiseerde herstart nog steeds afgedwongen.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Software die wordt vertrouwd door de Intelligent Security Graph automatisch uitvoeren

Beheerders hebben nu de mogelijkheid om vergrendelde apparaten toe te staan om vertrouwde software uit te voeren met een goede reputatie, zoals bepaald door de Microsoft Intelligent Security Graph (ISG). De ISG bestaat uit Windows Defender SmartScreen en andere micro soft-Services.

Op de apparaten moet Windows Defender SmartScreen worden uitgevoerd om de software te kunnen vertrouwen.

#### <a name="try-it-out"></a>Probeer het nu!  

Ga als volgt te werk om een apparaat met Windows Defender SmartScreen vertrouwde software uit te voeren:

1.  Open de **wizard beleid voor Windows Defender-toepassings beheer maken**.
2.  Schakel op de pagina **insluitingen** het selectie vakje in voor het **autoriseren van software die wordt vertrouwd door de Intelligent Security Graph**.
3.  Voeg in het vak **vertrouwde bestanden of map** de bestanden en mappen toe die u wilt vertrouwen.
4.  Klik op **volgende** totdat de wizard is voltooid.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Windows Defender Application Guard-beleid configureren en implementeren <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) is een nieuwe Windows-functie waarmee u uw gebruikers kunt beschermen door niet-vertrouwde websites te openen in een beveiligde geïsoleerde container die niet toegankelijk is voor andere onderdelen van het besturings systeem. In deze Technical Preview hebt u ondersteuning toegevoegd om deze functie te configureren met behulp van Configuration Manager nalevings instellingen die u configureert, en vervolgens implementeert u deze in een verzameling. Deze functie wordt uitgebracht als Preview voor de 64-bits versie van de update van Windows 10 Maker. Als u deze functie nu wilt testen, moet u een preview-versie van deze update gebruiken.

### <a name="before-you-start"></a>Voordat u begint
Als u Windows Defender Application Guard-beleid wilt maken en implementeren, moeten de Windows 10-apparaten waarop u het beleid implementeert, worden geconfigureerd met een netwerk isolatie beleid. Zie voor meer informatie het blog bericht dat later wordt verwezen. Deze functie werkt alleen met huidige Windows 10 Insider-builds. Om het te testen, moeten uw clients een recente Windows 10 Insider-build uitvoeren.

### <a name="try-it-out"></a>Probeer het nu!

Lees [het blog bericht](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97)voor meer informatie over de basis beginselen van Windows Defender Application Guard.

Een beleid maken en bladeren door de beschik bare instellingen:
1. Kies in de **Configuration Manager** -console **activa en naleving**.
2. Kies **overzicht**Endpoint Protection **Assets and Compliance**  >  **Endpoint Protection**  >  **Windows Defender Application Guard**in de werk ruimte activa en naleving.
3. Klik op het tabblad **Start** in de groep **maken** op **Windows Defender Application Guard-beleid maken**.
4. Als u het blog bericht als referentie wilt gebruiken, kunt u door de beschik bare instellingen bladeren en deze configureren om de functie uit te proberen.
5. In deze release hebben we de nieuwe netwerk definitie pagina aan de wizard toegevoegd. Hier geeft u de bedrijfs identiteit op en definieert u de grens van uw bedrijfs netwerk.

    > [!NOTE]
    > Windows 10-Pc's slaan slechts één netwerk isolatie lijst op de client op. In deze release kunt u twee verschillende soorten netwerk isolatie lijsten maken (één van Windows Information Protection en één van Windows Defender Application Guard) en implementeren op de client. Als u beide beleids regels implementeert, moeten deze netwerk isolatie lijsten overeenkomen. Als u lijsten implementeert die niet overeenkomen met dezelfde client, mislukt de implementatie.

    Meer informatie over het opgeven van netwerk definities vindt u in de [Windows Information Protection-documentatie]- [uw ondernemings gegevens beveiligen met behulp van Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr).

6. Wanneer u klaar bent, voltooit u de wizard en implementeert u het beleid op een of meer Windows 10-apparaten.

### <a name="further-reading"></a>Meer informatie

Zie [dit blog bericht](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97)voor meer informatie over Windows Defender Application Guard. Zie [dit blog bericht](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903)voor meer informatie over de zelfstandige Windows Defender Application Guard-modus.

## <a name="next-steps"></a>Volgende stappen
Zie [Technical Preview voor Configuration Manager voor](technical-preview.md)meer informatie over het installeren of bijwerken van de technische preview-vertakking.    
